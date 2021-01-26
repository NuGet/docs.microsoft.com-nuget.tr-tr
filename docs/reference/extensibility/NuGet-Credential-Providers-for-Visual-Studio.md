---
title: Visual Studio için NuGet kimlik bilgileri sağlayıcısı
description: NuGet kimlik bilgisi sağlayıcıları bir Visual Studio uzantısında IVsCredentialProvider arabirimini uygulayarak akışlarla kimlik doğrular.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: f324f1e27e0d718571525152fcf16b55b900dbaa
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777753"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a>NuGet kimlik bilgisi sağlayıcılarıyla Visual Studio 'da akışlara kimlik doğrulama

NuGet Visual Studio Uzantısı 3.6 + kimlik bilgisi sağlayıcılarını destekler, bu da NuGet 'nin kimliği doğrulanmış akışlarla çalışmasını sağlar.
Visual Studio için bir NuGet kimlik bilgisi sağlayıcısı yükledikten sonra, NuGet Visual Studio uzantısı gerektiğinde kimliği doğrulanmış akışlar için kimlik bilgilerini otomatik olarak elde eder ve yeniler.

Örnek bir uygulama [VsCredentialProvider örneğinde](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)bulunabilir.

NuGet, Visual Studio içinde `VsCredentialProviderImporter` eklenti kimlik bilgisi sağlayıcılarını da tarayan bir dahili kullanır. Bu eklenti kimlik bilgisi sağlayıcılarının türü MEF dışarı aktarma olarak bulunabilir olması gerekir `IVsCredentialProvider` .

Visual Studio 'da 4.8 + NuGet ile başlayarak yeni platformlar arası kimlik doğrulama eklentileri de desteklenir, ancak performans nedenleriyle bu önerilen yaklaşımlar değildir.

> [!Note]
> Visual Studio için NuGet kimlik bilgileri sağlayıcıları, düzenli bir Visual Studio uzantısı olarak yüklenmelidir ve [Visual studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe) veya üstünü gerektirir.
>
> Visual Studio için NuGet kimlik bilgileri sağlayıcıları yalnızca Visual Studio 'da çalışır (dotnet restore veya nuget.exe değil). nuget.exe olan kimlik bilgileri sağlayıcıları için bkz. [nuget.exe kimlik bilgileri sağlayıcıları](nuget-exe-Credential-providers.md).
> DotNet ve MSBuild 'teki kimlik bilgileri sağlayıcıları için bkz. [NuGet platformlar arası eklentileri](nuget-cross-platform-authentication-plugin.md)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a>Visual Studio için NuGet kimlik bilgileri sağlayıcısı oluşturma

NuGet Visual Studio Uzantısı 3.6 + kimlik bilgilerini almak için kullanılan bir iç CredentialService uygular. CredentialService, yerleşik ve eklenti kimlik bilgisi sağlayıcılarının bir listesini içerir. Her sağlayıcı, kimlik bilgileri alınana kadar sırayla denenir.

Kimlik bilgisi alma sırasında kimlik bilgisi hizmeti kimlik bilgisi sağlayıcılarını aşağıdaki sırayla dener, kimlik bilgileri elde edilir almaz durdurulur:

1. Kimlik bilgileri NuGet yapılandırma dosyalarından alınacaktır (yerleşik kullanılarak `SettingsCredentialProvider` ).
1. Paket kaynağı Visual Studio Team Services ise, kullanılacaktır `VisualStudioAccountProvider` .
1. Diğer tüm eklenti Visual Studio kimlik bilgileri sağlayıcıları sırayla denenecek.
1. Tüm NuGet platformlar arası kimlik bilgisi sağlayıcılarını sırayla kullanmayı deneyin.
1. Henüz kimlik bilgileri alınmadıysa, kullanıcıdan standart temel kimlik doğrulama iletişim kutusu kullanılarak kimlik bilgileri istenir.

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a>IVsCredentialProvider. GetCredentialsAsync uygulama

Visual Studio için bir NuGet kimlik bilgisi sağlayıcısı oluşturmak için, türü uygulayan bir genel MEF dışa aktarma Işlemini kullanıma sunan bir Visual Studio uzantısı oluşturun `IVsCredentialProvider` ve aşağıda özetlenen ilkelere uyar.

```cs
public interface IVsCredentialProvider
{
    Task<ICredentials> GetCredentialsAsync(
        Uri uri,
        IWebProxy proxy,
        bool isProxyRequest,
        bool isRetry,
        bool nonInteractive,
        CancellationToken cancellationToken);
}
```

Örnek bir uygulama [VsCredentialProvider örneğinde](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)bulunabilir.

Visual Studio için her NuGet kimlik bilgisi sağlayıcısı şunları vermelidir:

1. Kimlik bilgilerinin alımı başlatmadan önce hedeflenen URI için kimlik bilgileri sağlayıp sağlayamayacağını belirleme. Sağlayıcı, hedeflenen kaynak için kimlik bilgilerini sağlaya, sonra döndürmelidir `null` .
1. Sağlayıcı hedeflenen URI için istekleri işler, ancak kimlik bilgilerini sağlayamadığında, bir özel durum oluşturulmalıdır.

Visual Studio için özel bir NuGet kimlik bilgisi sağlayıcısı, `IVsCredentialProvider` [NuGet. VisualStudio paketinde](https://www.nuget.org/packages/NuGet.VisualStudio/)kullanılabilir arabirimi uygulamalıdır.

#### <a name="getcredentialasync"></a>GetCredentialAsync

| Giriş parametresi |Açıklama|
| ----------------|-----------|
| URI URI 'si | Kimlik bilgilerinin istenmekte olduğu paket kaynak URI 'Si.|
| IWebProxy ara sunucusu | Ağ üzerinde iletişim kurarken kullanılacak Web proxy 'si. Yapılandırılmış bir proxy kimlik doğrulaması yoksa null. |
| bool ıproxyrequest | Bu istek proxy kimlik doğrulama kimlik bilgilerini almak ise true. Uygulama proxy kimlik bilgilerini almak için geçerli değilse, null döndürülmelidir. |
| bool ısretry | Bu URI için önceden kimlik bilgileri isteniyorsa true, ancak sağlanan kimlik bilgileri yetkili erişime izin vermedi. |
| bool etkileşimsiz | True ise, kimlik bilgisi sağlayıcısı tüm Kullanıcı istemlerini bastırmalıdır ve bunun yerine varsayılan değerleri kullanır. |
| CancellationToken cancellationToken | Kimlik bilgilerini isteme işleminin iptal edilip edilmediğine yönelik bu iptal belirtecinin denetlenmesi gerekir. |

**Dönüş değeri**: [ `System.Net.ICredentials` arabirimi](/dotnet/api/system.net.icredentials?view=netstandard-2.0)uygulayan bir kimlik bilgileri nesnesi.
