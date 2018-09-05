---
title: Visual Studio için NuGet kimlik bilgileri sağlayıcısı
description: NuGet kimlik bilgisi sağlayıcıları akışlarıyla IVsCredentialProvider arabirimi Visual Studio Uzantısı'nda uygulama tarafından kimlik doğrulaması.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: abe009fee5863c55a188f4d7c71ed0924dd067ff
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547960"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="5f135-103">Visual Studio Özet akışları NuGet kimlik bilgisi sağlayıcıları ile kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="5f135-103">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="5f135-104">NuGet Visual Studio Uzantısı 3.6 + etkinleştiren kimliği doğrulanmış akışları ile çalışmak NuGet kimlik bilgisi sağlayıcılarını destekler.</span><span class="sxs-lookup"><span data-stu-id="5f135-104">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="5f135-105">Bir Visual Studio için NuGet kimlik bilgisi sağlayıcı yükledikten sonra NuGet Visual Studio uzantısı otomatik olarak almak ve gerekli olarak kimliği doğrulanmış akışları için kimlik bilgilerini yenileyin.</span><span class="sxs-lookup"><span data-stu-id="5f135-105">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="5f135-106">Örnek uygulama bulunabilir [VsCredentialProvider örnek](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="5f135-106">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="5f135-107">4.8 + ile başlayarak, Visual Studio'da NuGet yeni platformlar arası kimlik doğrulaması eklentileri de destekler ancak performansı artırmak için önerilen yaklaşım değildir.</span><span class="sxs-lookup"><span data-stu-id="5f135-107">Starting with 4.8+ NuGet in Visual Studio supports the new cross platform authentication plugins as well, but they are not the recommended approach for performance reasons.</span></span>

> [!Note]
> <span data-ttu-id="5f135-108">Visual Studio için NuGet kimlik bilgisi sağlayıcısı normal bir Visual Studio uzantısı yüklenmeli ve gerektirecek [Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) veya üzeri.</span><span class="sxs-lookup"><span data-stu-id="5f135-108">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) or above.</span></span>
>
> <span data-ttu-id="5f135-109">Visual Studio için NuGet kimlik bilgisi sağlayıcısı yalnızca Visual Studio (değil, dotnet restore veya nuget.exe) çalışır.</span><span class="sxs-lookup"><span data-stu-id="5f135-109">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="5f135-110">Nuget.exe ile kimlik bilgisi sağlayıcıları için bkz: [nuget.exe kimlik bilgileri sağlayıcısı](nuget-exe-Credential-providers.md).</span><span class="sxs-lookup"><span data-stu-id="5f135-110">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>
> <span data-ttu-id="5f135-111">Kimlik bilgisi için bkz: dotnet ve msbuild sağlayıcıları [NuGet çapraz platform eklentileri](nuget-cross-platform-authentication-plugin.md)</span><span class="sxs-lookup"><span data-stu-id="5f135-111">For credential providers in dotnet and msbuild see [NuGet cross platform plugins](nuget-cross-platform-authentication-plugin.md)</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="5f135-112">Visual Studio için NuGet kimlik bilgisi sağlayıcısı kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="5f135-112">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="5f135-113">Visual Studio Team Services'ı desteklemek için Visual Studio NuGet uzantısı'na yerleşik bir kimlik bilgisi sağlayıcısı yok.</span><span class="sxs-lookup"><span data-stu-id="5f135-113">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="5f135-114">Bir iç NuGet Visual Studio uzantısı kullanan `VsCredentialProviderImporter` hangi tarar için eklenti kimlik bilgileri sağlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="5f135-114">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="5f135-115">Bu eklenti kimlik bilgisi sağlayıcıları bulunabilirlik bir MEF dışarı aktarma türü `IVsCredentialProvider`.</span><span class="sxs-lookup"><span data-stu-id="5f135-115">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="5f135-116">Kullanılabilir Eklenti kimlik bilgisi sağlayıcıları içerir:</span><span class="sxs-lookup"><span data-stu-id="5f135-116">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="5f135-117">Visual Studio 2017 için MyGet Kimlik Bilgileri Sağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="5f135-117">MyGet Credential Provider for Visual Studio 2017</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="5f135-118">Bir Visual Studio için NuGet kimlik bilgisi sağlayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5f135-118">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="5f135-119">NuGet Visual Studio Uzantısı 3.6 + kimlik bilgilerini almak için kullanılan bir iç CredentialService uygular.</span><span class="sxs-lookup"><span data-stu-id="5f135-119">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="5f135-120">CredentialService yerleşik ve eklenti kimlik sağlayıcılarının bir listesine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="5f135-120">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="5f135-121">Her bir sağlayıcı, kimlik bilgileri elde edilen kadar sırayla denenir.</span><span class="sxs-lookup"><span data-stu-id="5f135-121">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="5f135-122">Kimlik bilgisi alımı sırasında kimlik bilgisi hizmet kimlik bilgisi sağlayıcılarını aşağıdaki sırayla kimlik bilgileri elde edilen sürede durdurma deneyecek:</span><span class="sxs-lookup"><span data-stu-id="5f135-122">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="5f135-123">Kimlik bilgileri NuGet yapılandırma dosyalarından getirilecek (yerleşik kullanarak `SettingsCredentialProvider`).</span><span class="sxs-lookup"><span data-stu-id="5f135-123">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="5f135-124">Paket kaynağı Visual Studio Team Services üzerinde ise `VisualStudioAccountProvider` kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5f135-124">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="5f135-125">Tüm diğer eklenti Visual Studio kimlik bilgisi sağlayıcıları sırayla denenir.</span><span class="sxs-lookup"><span data-stu-id="5f135-125">All other plug-in Visual Studio credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="5f135-126">Çapraz platform kimlik bilgisi sağlayıcıları tüm NuGet sıralı olarak kullanmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="5f135-126">Try to use all NuGet cross platform credential providers sequentially.</span></span>
1. <span data-ttu-id="5f135-127">Kimlik bilgisi henüz alındı kullanıcı standart temel kimlik doğrulaması iletişim kutusunu kullanarak kimlik bilgileri istenir.</span><span class="sxs-lookup"><span data-stu-id="5f135-127">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="5f135-128">IVsCredentialProvider.GetCredentialsAsync uygulama</span><span class="sxs-lookup"><span data-stu-id="5f135-128">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="5f135-129">Visual Studio için NuGet kimlik bilgisi sağlayıcı oluşturmak için bir ortak MEF Dışarı Aktar uygulama sunan Visual Studio uzantısı oluşturma `IVsCredentialProvider` yazın ve için aşağıda belirtilen kurallara uyar.</span><span class="sxs-lookup"><span data-stu-id="5f135-129">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

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

<span data-ttu-id="5f135-130">Örnek uygulama bulunabilir [VsCredentialProvider örnek](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="5f135-130">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="5f135-131">Her Visual Studio için NuGet kimlik bilgisi sağlayıcısı gerekir:</span><span class="sxs-lookup"><span data-stu-id="5f135-131">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="5f135-132">Bu kimlik bilgileri hedeflenen URI için kimlik bilgilerini almayı başlatmadan önce sağlayıp sağlayamayacağını belirleyin.</span><span class="sxs-lookup"><span data-stu-id="5f135-132">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="5f135-133">Hedef kaynağı için kimlik bilgileri sağlayıcısı sağlayamazsınız sonra döndürmelidir `null`.</span><span class="sxs-lookup"><span data-stu-id="5f135-133">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="5f135-134">Sağlayıcı istekleri hedeflenen URI'sini ele alıyor, ancak kimlik bilgileri sağlayamazsınız, bir özel durum.</span><span class="sxs-lookup"><span data-stu-id="5f135-134">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="5f135-135">Visual Studio için özel bir NuGet kimlik bilgisi sağlayıcı uygulamalıdır `IVsCredentialProvider` arabirimi kullanılabilir [NuGet.VisualStudio paket](https://www.nuget.org/packages/NuGet.VisualStudio/).</span><span class="sxs-lookup"><span data-stu-id="5f135-135">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="5f135-136">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="5f135-136">GetCredentialAsync</span></span>

| <span data-ttu-id="5f135-137">Giriş parametresi</span><span class="sxs-lookup"><span data-stu-id="5f135-137">Input Parameter</span></span> |<span data-ttu-id="5f135-138">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5f135-138">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="5f135-139">URI URI'si</span><span class="sxs-lookup"><span data-stu-id="5f135-139">Uri uri</span></span> | <span data-ttu-id="5f135-140">Kimlik bilgileri istendiğinde paket kaynak URI'si.</span><span class="sxs-lookup"><span data-stu-id="5f135-140">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="5f135-141">IWebProxy proxy</span><span class="sxs-lookup"><span data-stu-id="5f135-141">IWebProxy proxy</span></span> | <span data-ttu-id="5f135-142">Ağ üzerinde iletişim kurarken kullanması için web proxy.</span><span class="sxs-lookup"><span data-stu-id="5f135-142">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="5f135-143">Yapılandırılmış hiçbir proxy kimlik doğrulaması yoksa null.</span><span class="sxs-lookup"><span data-stu-id="5f135-143">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="5f135-144">bool isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="5f135-144">bool isProxyRequest</span></span> | <span data-ttu-id="5f135-145">Proxy kimlik doğrulama bilgilerini almak için bu isteği ise true.</span><span class="sxs-lookup"><span data-stu-id="5f135-145">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="5f135-146">Uygulama proxy'si kimlik bilgilerini alma için geçerli değilse null döndürülmelidir.</span><span class="sxs-lookup"><span data-stu-id="5f135-146">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="5f135-147">bool isRetry</span><span class="sxs-lookup"><span data-stu-id="5f135-147">bool isRetry</span></span> | <span data-ttu-id="5f135-148">Doğru kimlik bilgilerini bu URI için daha önce istendi, ancak sağlanan kimlik bilgileri yetki verilen erişim izin vermedi.</span><span class="sxs-lookup"><span data-stu-id="5f135-148">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="5f135-149">Etkileşimli olmayan bool</span><span class="sxs-lookup"><span data-stu-id="5f135-149">bool nonInteractive</span></span> | <span data-ttu-id="5f135-150">TRUE ise, kimlik bilgisi sağlayıcı tüm kullanıcı komut istemleri gösterme ve bunun yerine varsayılan değerleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="5f135-150">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="5f135-151">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="5f135-151">CancellationToken cancellationToken</span></span> | <span data-ttu-id="5f135-152">Kimlik bilgileri isteme işlemi, edildi belirlemek için bu iptal belirteci denetlenmelidir.</span><span class="sxs-lookup"><span data-stu-id="5f135-152">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="5f135-153">**Dönüş değeri**: kimlik bilgileri nesnesi uygulayan [ `System.Net.ICredentials` arabirimi](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span><span class="sxs-lookup"><span data-stu-id="5f135-153">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span></span>
