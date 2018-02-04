---
title: "Visual Studio için NuGet kimlik bilgisi sağlayıcıları | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet kimlik bilgisi sağlayıcıları, Visual Studio Uzantısı'nda IVsCredentialProvider arabirimi uygulayarak akışları ile kimlik doğrulaması."
keywords: "NuGet kimlik bilgisi sağlayıcıları, akış ile kimlik doğrulaması, NuGet visual studio uzantısı Galerisi ile kimlik doğrulaması"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ff143526c814c69f1a133a62c1ad1a8f5fbedd60
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/02/2018
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="49a1c-104">Visual Studio akışlarında NuGet kimlik bilgisi sağlayıcıları ile kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="49a1c-104">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="49a1c-105">NuGet Visual Studio Uzantısı 3.6 + kimliği doğrulanmış akışlarıyla çalışmak NuGet etkinleştirme kimlik bilgisi sağlayıcılarını destekler.</span><span class="sxs-lookup"><span data-stu-id="49a1c-105">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="49a1c-106">Visual Studio için NuGet kimlik bilgileri sağlayıcısı yükledikten sonra NuGet Visual Studio uzantısı otomatik olarak edinmeli ve gerektiği gibi kimliği doğrulanmış akışları için kimlik bilgilerinizi yenileyin.</span><span class="sxs-lookup"><span data-stu-id="49a1c-106">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="49a1c-107">Örnek uygulama bulunabilir [VsCredentialProvider örnek](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="49a1c-107">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

> [!Note]
> <span data-ttu-id="49a1c-108">Visual Studio için NuGet kimlik bilgisi sağlayıcıları normal bir Visual Studio uzantısı olarak yüklenmelidir ve ister [Visual Studio 2017](https://aka.ms/vs/15/preview/vs_enterprise) (şu anda önizlemede) veya üstü.</span><span class="sxs-lookup"><span data-stu-id="49a1c-108">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](https://aka.ms/vs/15/preview/vs_enterprise) (currently in preview) or above.</span></span>
>
> <span data-ttu-id="49a1c-109">Visual Studio için NuGet kimlik bilgisi sağlayıcıları yalnızca Visual Studio'da (değil dotnet geri yüklemek veya nuget.exe) çalışır.</span><span class="sxs-lookup"><span data-stu-id="49a1c-109">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="49a1c-110">Nuget.exe ile kimlik bilgisi sağlayıcıları için bkz: [nuget.exe kimlik bilgisi sağlayıcıları](nuget-exe-Credential-providers.md).</span><span class="sxs-lookup"><span data-stu-id="49a1c-110">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="49a1c-111">Visual Studio için kullanılabilir NuGet kimlik bilgisi sağlayıcıları</span><span class="sxs-lookup"><span data-stu-id="49a1c-111">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="49a1c-112">Visual Studio Team Services desteklemek için Visual Studio NuGet uzantısına yerleşik bir kimlik bilgisi sağlayıcısı yok.</span><span class="sxs-lookup"><span data-stu-id="49a1c-112">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="49a1c-113">NuGet Visual Studio uzantısı iç kullanan `VsCredentialProviderImporter` hangi tarar eklenti kimlik bilgisi sağlayıcıları için.</span><span class="sxs-lookup"><span data-stu-id="49a1c-113">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="49a1c-114">Bu eklenti kimlik bilgisi sağlayıcıları bulunabilirlik bir MEF Export türü `IVsCredentialProvider`.</span><span class="sxs-lookup"><span data-stu-id="49a1c-114">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="49a1c-115">Kullanılabilir Eklenti kimlik bilgisi sağlayıcıları içerir:</span><span class="sxs-lookup"><span data-stu-id="49a1c-115">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="49a1c-116">Visual Studio 2017 için MyGet Kimlik Bilgileri Sağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="49a1c-116">MyGet Credential Provider for Visual Studio 2017</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="49a1c-117">Visual Studio için NuGet kimlik bilgisi sağlayıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="49a1c-117">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="49a1c-118">NuGet Visual Studio Uzantısı 3.6 + kimlik bilgilerini almak için kullanılan bir iç CredentialService uygular.</span><span class="sxs-lookup"><span data-stu-id="49a1c-118">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="49a1c-119">CredentialService yerleşik ve eklenti kimlik bilgisi sağlayıcıları listesi vardır.</span><span class="sxs-lookup"><span data-stu-id="49a1c-119">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="49a1c-120">Kimlik bilgileri elde edilen kadar her sağlayıcı sırayla denenir.</span><span class="sxs-lookup"><span data-stu-id="49a1c-120">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="49a1c-121">Kimlik bilgisi alma sırasında kimlik bilgileri hizmeti kimlik bilgileri elde edilen hemen durdurma aşağıdaki sırayla kimlik bilgisi sağlayıcıları dener:</span><span class="sxs-lookup"><span data-stu-id="49a1c-121">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="49a1c-122">Kimlik bilgileri NuGet yapılandırma dosyalarından alınan (yerleşik kullanarak `SettingsCredentialProvider`).</span><span class="sxs-lookup"><span data-stu-id="49a1c-122">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="49a1c-123">Paket kaynağı Visual Studio Team Services ise `VisualStudioAccountProvider` kullanılır.</span><span class="sxs-lookup"><span data-stu-id="49a1c-123">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="49a1c-124">Diğer tüm eklenti kimlik bilgisi sağlayıcıları sırayla denenir.</span><span class="sxs-lookup"><span data-stu-id="49a1c-124">All other plug-in credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="49a1c-125">Kimlik bilgisi henüz almış olması durumunda, kullanıcı için bir standart temel kimlik doğrulaması iletişim kutusunu kullanarak kimlik bilgileri istenir.</span><span class="sxs-lookup"><span data-stu-id="49a1c-125">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="49a1c-126">IVsCredentialProvider.GetCredentialsAsync uygulama</span><span class="sxs-lookup"><span data-stu-id="49a1c-126">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="49a1c-127">Visual Studio için NuGet kimlik bilgileri sağlayıcısı oluşturmak için bir ortak MEF Export uygulama sunan Visual Studio uzantısı oluşturun `IVsCredentialProvider` yazın ve aşağıda belirtilen kurallara uyar.</span><span class="sxs-lookup"><span data-stu-id="49a1c-127">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

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

<span data-ttu-id="49a1c-128">Örnek uygulama bulunabilir [VsCredentialProvider örnek](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span><span class="sxs-lookup"><span data-stu-id="49a1c-128">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="49a1c-129">Visual Studio için her bir NuGet kimlik bilgisi sağlayıcısı gerekir:</span><span class="sxs-lookup"><span data-stu-id="49a1c-129">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="49a1c-130">Bu kimlik bilgileri hedeflenen URI'sini kimlik bilgisi edinme başlatmadan önce sağlayıp sağlayamayacağını belirler.</span><span class="sxs-lookup"><span data-stu-id="49a1c-130">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="49a1c-131">Sağlayıcı hedeflenen kaynağı için kimlik bilgileri sağlayamazsınız sonra döndürme zorunluluğu `null`.</span><span class="sxs-lookup"><span data-stu-id="49a1c-131">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="49a1c-132">Sağlayıcı için hedeflenen URI istekleri işlemek, ancak kimlik bilgileri sağlayamazsınız, bir özel durum.</span><span class="sxs-lookup"><span data-stu-id="49a1c-132">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="49a1c-133">Visual Studio için özel bir NuGet kimlik bilgisi sağlayıcısı uygulamalıdır `IVsCredentialProvider` arabirimi kullanılabilir [NuGet.VisualStudio paket](https://www.nuget.org/packages/NuGet.VisualStudio/).</span><span class="sxs-lookup"><span data-stu-id="49a1c-133">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="49a1c-134">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="49a1c-134">GetCredentialAsync</span></span>

| <span data-ttu-id="49a1c-135">Giriş parametresi</span><span class="sxs-lookup"><span data-stu-id="49a1c-135">Input Parameter</span></span> |<span data-ttu-id="49a1c-136">Açıklama</span><span class="sxs-lookup"><span data-stu-id="49a1c-136">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="49a1c-137">URI URI</span><span class="sxs-lookup"><span data-stu-id="49a1c-137">Uri uri</span></span> | <span data-ttu-id="49a1c-138">Kimlik bilgilerini isteyen paket kaynak URI'si.</span><span class="sxs-lookup"><span data-stu-id="49a1c-138">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="49a1c-139">IWebProxy proxy</span><span class="sxs-lookup"><span data-stu-id="49a1c-139">IWebProxy proxy</span></span> | <span data-ttu-id="49a1c-140">Ağ üzerinde iletişim kurarken kullanması için web proxy.</span><span class="sxs-lookup"><span data-stu-id="49a1c-140">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="49a1c-141">Yapılandırılmış hiçbir proxy kimlik doğrulaması yoksa null.</span><span class="sxs-lookup"><span data-stu-id="49a1c-141">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="49a1c-142">bool isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="49a1c-142">bool isProxyRequest</span></span> | <span data-ttu-id="49a1c-143">Proxy kimlik doğrulaması kimlik bilgilerini almak için bu isteği ise true.</span><span class="sxs-lookup"><span data-stu-id="49a1c-143">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="49a1c-144">Uygulama proxy kimlik bilgilerini alma için geçerli değilse null döndürülmelidir.</span><span class="sxs-lookup"><span data-stu-id="49a1c-144">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="49a1c-145">bool isRetry</span><span class="sxs-lookup"><span data-stu-id="49a1c-145">bool isRetry</span></span> | <span data-ttu-id="49a1c-146">Kimlik bilgileri daha önce bu URI'sini istendi, ancak sağlanan kimlik bilgileri yetkili erişimi izin verme, true.</span><span class="sxs-lookup"><span data-stu-id="49a1c-146">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="49a1c-147">bool etkileşimsiz</span><span class="sxs-lookup"><span data-stu-id="49a1c-147">bool nonInteractive</span></span> | <span data-ttu-id="49a1c-148">TRUE ise, kimlik bilgileri sağlayıcısı tüm kullanıcı sorulmasını önlemek ve varsayılan değerleri kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="49a1c-148">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="49a1c-149">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="49a1c-149">CancellationToken cancellationToken</span></span> | <span data-ttu-id="49a1c-150">Kimlik bilgilerini isteyen işlemi iptal edildi belirlemek için bu iptal belirteci denetlenmesi.</span><span class="sxs-lookup"><span data-stu-id="49a1c-150">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="49a1c-151">**Dönüş değeri**: kimlik bilgileri uygulama nesnesi [ `System.Net.ICredentials` arabirimi](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span><span class="sxs-lookup"><span data-stu-id="49a1c-151">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span></span>
