---
title: Visual Studio için NuGet kimlik bilgisi sağlayıcıları
description: NuGet kimlik bilgisi sağlayıcıları, Visual Studio Uzantısı'nda IVsCredentialProvider arabirimi uygulayarak akışları ile kimlik doğrulaması.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 740df87b0d663aac482d888e916662528ce27030
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a>Visual Studio akışlarında NuGet kimlik bilgisi sağlayıcıları ile kimlik doğrulaması

NuGet Visual Studio Uzantısı 3.6 + kimliği doğrulanmış akışlarıyla çalışmak NuGet etkinleştirme kimlik bilgisi sağlayıcılarını destekler.
Visual Studio için NuGet kimlik bilgileri sağlayıcısı yükledikten sonra NuGet Visual Studio uzantısı otomatik olarak edinmeli ve gerektiği gibi kimliği doğrulanmış akışları için kimlik bilgilerinizi yenileyin.

Örnek uygulama bulunabilir [VsCredentialProvider örnek](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

> [!Note]
> Visual Studio için NuGet kimlik bilgisi sağlayıcıları normal bir Visual Studio uzantısı olarak yüklenmelidir ve ister [Visual Studio 2017](https://aka.ms/vs/15/preview/vs_enterprise) (şu anda önizlemede) veya üstü.
>
> Visual Studio için NuGet kimlik bilgisi sağlayıcıları yalnızca Visual Studio'da (değil dotnet geri yüklemek veya nuget.exe) çalışır. Nuget.exe ile kimlik bilgisi sağlayıcıları için bkz: [nuget.exe kimlik bilgisi sağlayıcıları](nuget-exe-Credential-providers.md).

## <a name="available-nuget-credential-providers-for-visual-studio"></a>Visual Studio için kullanılabilir NuGet kimlik bilgisi sağlayıcıları

Visual Studio Team Services desteklemek için Visual Studio NuGet uzantısına yerleşik bir kimlik bilgisi sağlayıcısı yok.

NuGet Visual Studio uzantısı iç kullanan `VsCredentialProviderImporter` hangi tarar eklenti kimlik bilgisi sağlayıcıları için. Bu eklenti kimlik bilgisi sağlayıcıları bulunabilirlik bir MEF Export türü `IVsCredentialProvider`.

Kullanılabilir Eklenti kimlik bilgisi sağlayıcıları içerir:

- [Visual Studio 2017 için MyGet Kimlik Bilgileri Sağlayıcısı](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a>Visual Studio için NuGet kimlik bilgisi sağlayıcısı oluşturma

NuGet Visual Studio Uzantısı 3.6 + kimlik bilgilerini almak için kullanılan bir iç CredentialService uygular. CredentialService yerleşik ve eklenti kimlik bilgisi sağlayıcıları listesi vardır. Kimlik bilgileri elde edilen kadar her sağlayıcı sırayla denenir.

Kimlik bilgisi alma sırasında kimlik bilgileri hizmeti kimlik bilgileri elde edilen hemen durdurma aşağıdaki sırayla kimlik bilgisi sağlayıcıları dener:

1. Kimlik bilgileri NuGet yapılandırma dosyalarından alınan (yerleşik kullanarak `SettingsCredentialProvider`).
1. Paket kaynağı Visual Studio Team Services ise `VisualStudioAccountProvider` kullanılır.
1. Diğer tüm eklenti kimlik bilgisi sağlayıcıları sırayla denenir.
1. Kimlik bilgisi henüz almış olması durumunda, kullanıcı için bir standart temel kimlik doğrulaması iletişim kutusunu kullanarak kimlik bilgileri istenir.

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a>IVsCredentialProvider.GetCredentialsAsync uygulama

Visual Studio için NuGet kimlik bilgileri sağlayıcısı oluşturmak için bir ortak MEF Export uygulama sunan Visual Studio uzantısı oluşturun `IVsCredentialProvider` yazın ve aşağıda belirtilen kurallara uyar.

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

Örnek uygulama bulunabilir [VsCredentialProvider örnek](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

Visual Studio için her bir NuGet kimlik bilgisi sağlayıcısı gerekir:

1. Bu kimlik bilgileri hedeflenen URI'sini kimlik bilgisi edinme başlatmadan önce sağlayıp sağlayamayacağını belirler. Sağlayıcı hedeflenen kaynağı için kimlik bilgileri sağlayamazsınız sonra döndürme zorunluluğu `null`.
1. Sağlayıcı için hedeflenen URI istekleri işlemek, ancak kimlik bilgileri sağlayamazsınız, bir özel durum.

Visual Studio için özel bir NuGet kimlik bilgisi sağlayıcısı uygulamalıdır `IVsCredentialProvider` arabirimi kullanılabilir [NuGet.VisualStudio paket](https://www.nuget.org/packages/NuGet.VisualStudio/).

#### <a name="getcredentialasync"></a>GetCredentialAsync

| Giriş parametresi |Açıklama|
| ----------------|-----------|
| URI URI | Kimlik bilgilerini isteyen paket kaynak URI'si.|
| IWebProxy proxy | Ağ üzerinde iletişim kurarken kullanması için web proxy. Yapılandırılmış hiçbir proxy kimlik doğrulaması yoksa null. |
| bool isProxyRequest | Proxy kimlik doğrulaması kimlik bilgilerini almak için bu isteği ise true. Uygulama proxy kimlik bilgilerini alma için geçerli değilse null döndürülmelidir. |
| bool isRetry | Kimlik bilgileri daha önce bu URI'sini istendi, ancak sağlanan kimlik bilgileri yetkili erişimi izin verme, true. |
| bool etkileşimsiz | TRUE ise, kimlik bilgileri sağlayıcısı tüm kullanıcı sorulmasını önlemek ve varsayılan değerleri kullanmanız gerekir. |
| CancellationToken cancellationToken | Kimlik bilgilerini isteyen işlemi iptal edildi belirlemek için bu iptal belirteci denetlenmesi. |

**Dönüş değeri**: kimlik bilgileri uygulama nesnesi [ `System.Net.ICredentials` arabirimi](/dotnet/api/system.net.icredentials?view=netstandard-2.0).
