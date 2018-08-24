---
title: Visual Studio için NuGet kimlik bilgileri sağlayıcısı
description: NuGet kimlik bilgisi sağlayıcıları akışlarıyla IVsCredentialProvider arabirimi Visual Studio Uzantısı'nda uygulama tarafından kimlik doğrulaması.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: e8d8ae22300b55b93badb65864163d959105dca2
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42793909"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a>Visual Studio Özet akışları NuGet kimlik bilgisi sağlayıcıları ile kimlik doğrulaması

NuGet Visual Studio Uzantısı 3.6 + etkinleştiren kimliği doğrulanmış akışları ile çalışmak NuGet kimlik bilgisi sağlayıcılarını destekler.
Bir Visual Studio için NuGet kimlik bilgisi sağlayıcı yükledikten sonra NuGet Visual Studio uzantısı otomatik olarak almak ve gerekli olarak kimliği doğrulanmış akışları için kimlik bilgilerini yenileyin.

Örnek uygulama bulunabilir [VsCredentialProvider örnek](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).

4.8 + ile başlayarak, Visual Studio'da NuGet yeni platformlar arası kimlik doğrulaması eklentileri de destekler ancak performansı artırmak için önerilen yaklaşım değildir.

> [!Note]
> Visual Studio için NuGet kimlik bilgisi sağlayıcısı normal bir Visual Studio uzantısı yüklenmeli ve gerektirecek [Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) veya üzeri.
>
> Visual Studio için NuGet kimlik bilgisi sağlayıcısı yalnızca Visual Studio (değil, dotnet restore veya nuget.exe) çalışır. Nuget.exe ile kimlik bilgisi sağlayıcıları için bkz: [nuget.exe kimlik bilgileri sağlayıcısı](nuget-exe-Credential-providers.md).
> Kimlik bilgisi için bkz: dotnet ve msbuild sağlayıcıları [NuGet çapraz platform eklentileri](nuget-cross-platform-authentication-plugin.md)

## <a name="available-nuget-credential-providers-for-visual-studio"></a>Visual Studio için NuGet kimlik bilgisi sağlayıcısı kullanılabilir

Visual Studio Team Services'ı desteklemek için Visual Studio NuGet uzantısı'na yerleşik bir kimlik bilgisi sağlayıcısı yok.

Bir iç NuGet Visual Studio uzantısı kullanan `VsCredentialProviderImporter` hangi tarar için eklenti kimlik bilgileri sağlayıcısı. Bu eklenti kimlik bilgisi sağlayıcıları bulunabilirlik bir MEF dışarı aktarma türü `IVsCredentialProvider`.

Kullanılabilir Eklenti kimlik bilgisi sağlayıcıları içerir:

- [Visual Studio 2017 için MyGet Kimlik Bilgileri Sağlayıcısı](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a>Bir Visual Studio için NuGet kimlik bilgisi sağlayıcı oluşturma

NuGet Visual Studio Uzantısı 3.6 + kimlik bilgilerini almak için kullanılan bir iç CredentialService uygular. CredentialService yerleşik ve eklenti kimlik sağlayıcılarının bir listesine sahiptir. Her bir sağlayıcı, kimlik bilgileri elde edilen kadar sırayla denenir.

Kimlik bilgisi alımı sırasında kimlik bilgisi hizmet kimlik bilgisi sağlayıcılarını aşağıdaki sırayla kimlik bilgileri elde edilen sürede durdurma deneyecek:

1. Kimlik bilgileri NuGet yapılandırma dosyalarından getirilecek (yerleşik kullanarak `SettingsCredentialProvider`).
1. Paket kaynağı Visual Studio Team Services üzerinde ise `VisualStudioAccountProvider` kullanılır.
1. Tüm diğer eklenti Visual Studio kimlik bilgisi sağlayıcıları sırayla denenir.
1. Çapraz platform kimlik bilgisi sağlayıcıları tüm NuGet sıralı olarak kullanmayı deneyin.
1. Kimlik bilgisi henüz alındı kullanıcı standart temel kimlik doğrulaması iletişim kutusunu kullanarak kimlik bilgileri istenir.

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a>IVsCredentialProvider.GetCredentialsAsync uygulama

Visual Studio için NuGet kimlik bilgisi sağlayıcı oluşturmak için bir ortak MEF Dışarı Aktar uygulama sunan Visual Studio uzantısı oluşturma `IVsCredentialProvider` yazın ve için aşağıda belirtilen kurallara uyar.

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

Her Visual Studio için NuGet kimlik bilgisi sağlayıcısı gerekir:

1. Bu kimlik bilgileri hedeflenen URI için kimlik bilgilerini almayı başlatmadan önce sağlayıp sağlayamayacağını belirleyin. Hedef kaynağı için kimlik bilgileri sağlayıcısı sağlayamazsınız sonra döndürmelidir `null`.
1. Sağlayıcı istekleri hedeflenen URI'sini ele alıyor, ancak kimlik bilgileri sağlayamazsınız, bir özel durum.

Visual Studio için özel bir NuGet kimlik bilgisi sağlayıcı uygulamalıdır `IVsCredentialProvider` arabirimi kullanılabilir [NuGet.VisualStudio paket](https://www.nuget.org/packages/NuGet.VisualStudio/).

#### <a name="getcredentialasync"></a>GetCredentialAsync

| Giriş parametresi |Açıklama|
| ----------------|-----------|
| URI URI'si | Kimlik bilgileri istendiğinde paket kaynak URI'si.|
| IWebProxy proxy | Ağ üzerinde iletişim kurarken kullanması için web proxy. Yapılandırılmış hiçbir proxy kimlik doğrulaması yoksa null. |
| bool isProxyRequest | Proxy kimlik doğrulama bilgilerini almak için bu isteği ise true. Uygulama proxy'si kimlik bilgilerini alma için geçerli değilse null döndürülmelidir. |
| bool isRetry | Doğru kimlik bilgilerini bu URI için daha önce istendi, ancak sağlanan kimlik bilgileri yetki verilen erişim izin vermedi. |
| Etkileşimli olmayan bool | TRUE ise, kimlik bilgisi sağlayıcı tüm kullanıcı komut istemleri gösterme ve bunun yerine varsayılan değerleri kullanın. |
| CancellationToken cancellationToken | Kimlik bilgileri isteme işlemi, edildi belirlemek için bu iptal belirteci denetlenmelidir. |

**Dönüş değeri**: kimlik bilgileri nesnesi uygulayan [ `System.Net.ICredentials` arabirimi](/dotnet/api/system.net.icredentials?view=netstandard-2.0).
