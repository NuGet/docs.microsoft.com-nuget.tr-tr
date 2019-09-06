---
title: Visual Studio için NuGet kimlik bilgileri sağlayıcısı
description: NuGet kimlik bilgisi sağlayıcıları bir Visual Studio uzantısında IVsCredentialProvider arabirimini uygulayarak akışlarla kimlik doğrular.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 4e781a2462871bceeb1c7f02220320daabdab98a
ms.sourcegitcommit: a0807671386782021acb7588741390e6f07e94e1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/05/2019
ms.locfileid: "70384425"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="3496e-103">NuGet kimlik bilgisi sağlayıcılarıyla Visual Studio 'da akışlara kimlik doğrulama</span><span class="sxs-lookup"><span data-stu-id="3496e-103">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="3496e-104">NuGet Visual Studio Uzantısı 3.6 + kimlik bilgisi sağlayıcılarını destekler, bu da NuGet 'nin kimliği doğrulanmış akışlarla çalışmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="3496e-104">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="3496e-105">Visual Studio için bir NuGet kimlik bilgisi sağlayıcısı yükledikten sonra, NuGet Visual Studio uzantısı gerektiğinde kimliği doğrulanmış akışlar için kimlik bilgilerini otomatik olarak elde eder ve yeniler.</span><span class="sxs-lookup"><span data-stu-id="3496e-105">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="3496e-106">Örnek bir uygulama [VsCredentialProvider örneğinde](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="3496e-106">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="3496e-107">Visual Studio 'da 4.8 + NuGet ile başlayarak yeni platformlar arası kimlik doğrulama eklentileri de desteklenir, ancak performans nedenleriyle bu önerilen yaklaşımlar değildir.</span><span class="sxs-lookup"><span data-stu-id="3496e-107">Starting with 4.8+ NuGet in Visual Studio supports the new cross platform authentication plugins as well, but they are not the recommended approach for performance reasons.</span></span>

> [!Note]
> <span data-ttu-id="3496e-108">Visual Studio için NuGet kimlik bilgileri sağlayıcıları, düzenli bir Visual Studio uzantısı olarak yüklenmelidir ve [Visual studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) veya üstünü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="3496e-108">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) or above.</span></span>
>
> <span data-ttu-id="3496e-109">Visual Studio için NuGet kimlik bilgileri sağlayıcıları yalnızca Visual Studio 'da çalışır (dotnet restore veya NuGet. exe ' de değildir).</span><span class="sxs-lookup"><span data-stu-id="3496e-109">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="3496e-110">NuGet. exe olan kimlik bilgisi sağlayıcıları için bkz. [NuGet. exe kimlik bilgileri sağlayıcıları](nuget-exe-Credential-providers.md).</span><span class="sxs-lookup"><span data-stu-id="3496e-110">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>
> <span data-ttu-id="3496e-111">DotNet ve MSBuild 'teki kimlik bilgileri sağlayıcıları için bkz. [NuGet platformlar arası eklentileri](nuget-cross-platform-authentication-plugin.md)</span><span class="sxs-lookup"><span data-stu-id="3496e-111">For credential providers in dotnet and msbuild see [NuGet cross platform plugins](nuget-cross-platform-authentication-plugin.md)</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="3496e-112">Visual Studio için kullanılabilir NuGet kimlik bilgileri sağlayıcıları</span><span class="sxs-lookup"><span data-stu-id="3496e-112">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="3496e-113">Visual Studio Team Services desteklemek için Visual Studio NuGet uzantısında yerleşik olarak bulunan bir kimlik bilgisi sağlayıcısı vardır.</span><span class="sxs-lookup"><span data-stu-id="3496e-113">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="3496e-114">NuGet Visual Studio uzantısı, eklenti kimlik bilgisi `VsCredentialProviderImporter` sağlayıcılarını da tarayan bir dahili kullanır.</span><span class="sxs-lookup"><span data-stu-id="3496e-114">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="3496e-115">Bu eklenti kimlik bilgisi sağlayıcılarının türü `IVsCredentialProvider`MEF dışarı aktarma olarak bulunabilir olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3496e-115">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="3496e-116">Kullanılabilir eklenti kimlik bilgileri sağlayıcıları şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="3496e-116">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="3496e-117">Visual Studio için MyGet kimlik bilgileri sağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="3496e-117">MyGet Credential Provider for Visual Studio</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="3496e-118">Visual Studio için NuGet kimlik bilgileri sağlayıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3496e-118">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="3496e-119">NuGet Visual Studio Uzantısı 3.6 + kimlik bilgilerini almak için kullanılan bir iç CredentialService uygular.</span><span class="sxs-lookup"><span data-stu-id="3496e-119">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="3496e-120">CredentialService, yerleşik ve eklenti kimlik bilgisi sağlayıcılarının bir listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="3496e-120">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="3496e-121">Her sağlayıcı, kimlik bilgileri alınana kadar sırayla denenir.</span><span class="sxs-lookup"><span data-stu-id="3496e-121">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="3496e-122">Kimlik bilgisi alma sırasında kimlik bilgisi hizmeti kimlik bilgisi sağlayıcılarını aşağıdaki sırayla dener, kimlik bilgileri elde edilir almaz durdurulur:</span><span class="sxs-lookup"><span data-stu-id="3496e-122">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="3496e-123">Kimlik bilgileri NuGet yapılandırma dosyalarından alınacaktır (yerleşik `SettingsCredentialProvider`kullanılarak).</span><span class="sxs-lookup"><span data-stu-id="3496e-123">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="3496e-124">Paket kaynağı Visual Studio Team Services `VisualStudioAccountProvider` ise, kullanılacaktır.</span><span class="sxs-lookup"><span data-stu-id="3496e-124">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="3496e-125">Diğer tüm eklenti Visual Studio kimlik bilgileri sağlayıcıları sırayla denenecek.</span><span class="sxs-lookup"><span data-stu-id="3496e-125">All other plug-in Visual Studio credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="3496e-126">Tüm NuGet platformlar arası kimlik bilgisi sağlayıcılarını sırayla kullanmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="3496e-126">Try to use all NuGet cross platform credential providers sequentially.</span></span>
1. <span data-ttu-id="3496e-127">Henüz kimlik bilgileri alınmadıysa, kullanıcıdan standart temel kimlik doğrulama iletişim kutusu kullanılarak kimlik bilgileri istenir.</span><span class="sxs-lookup"><span data-stu-id="3496e-127">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="3496e-128">IVsCredentialProvider. GetCredentialsAsync uygulama</span><span class="sxs-lookup"><span data-stu-id="3496e-128">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="3496e-129">Visual Studio için bir NuGet kimlik bilgisi sağlayıcısı oluşturmak için, `IVsCredentialProvider` türü uygulayan bir genel MEF dışa aktarma işlemini kullanıma sunan bir Visual Studio uzantısı oluşturun ve aşağıda özetlenen ilkelere uyar.</span><span class="sxs-lookup"><span data-stu-id="3496e-129">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

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

<span data-ttu-id="3496e-130">Örnek bir uygulama [VsCredentialProvider örneğinde](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="3496e-130">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="3496e-131">Visual Studio için her NuGet kimlik bilgisi sağlayıcısı şunları vermelidir:</span><span class="sxs-lookup"><span data-stu-id="3496e-131">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="3496e-132">Kimlik bilgilerinin alımı başlatmadan önce hedeflenen URI için kimlik bilgileri sağlayıp sağlayamayacağını belirleme.</span><span class="sxs-lookup"><span data-stu-id="3496e-132">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="3496e-133">Sağlayıcı, hedeflenen kaynak için kimlik bilgilerini sağlaya, sonra döndürmelidir `null`.</span><span class="sxs-lookup"><span data-stu-id="3496e-133">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="3496e-134">Sağlayıcı hedeflenen URI için istekleri işler, ancak kimlik bilgilerini sağlayamadığında, bir özel durum oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3496e-134">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="3496e-135">Visual Studio için özel bir NuGet kimlik bilgisi sağlayıcısı, `IVsCredentialProvider` [NuGet. VisualStudio paketinde](https://www.nuget.org/packages/NuGet.VisualStudio/)kullanılabilir arabirimi uygulamalıdır.</span><span class="sxs-lookup"><span data-stu-id="3496e-135">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="3496e-136">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="3496e-136">GetCredentialAsync</span></span>

| <span data-ttu-id="3496e-137">Giriş parametresi</span><span class="sxs-lookup"><span data-stu-id="3496e-137">Input Parameter</span></span> |<span data-ttu-id="3496e-138">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3496e-138">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="3496e-139">URI URI 'si</span><span class="sxs-lookup"><span data-stu-id="3496e-139">Uri uri</span></span> | <span data-ttu-id="3496e-140">Kimlik bilgilerinin istenmekte olduğu paket kaynak URI 'Si.</span><span class="sxs-lookup"><span data-stu-id="3496e-140">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="3496e-141">IWebProxy ara sunucusu</span><span class="sxs-lookup"><span data-stu-id="3496e-141">IWebProxy proxy</span></span> | <span data-ttu-id="3496e-142">Ağ üzerinde iletişim kurarken kullanılacak Web proxy 'si.</span><span class="sxs-lookup"><span data-stu-id="3496e-142">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="3496e-143">Yapılandırılmış bir proxy kimlik doğrulaması yoksa null.</span><span class="sxs-lookup"><span data-stu-id="3496e-143">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="3496e-144">bool ıproxyrequest</span><span class="sxs-lookup"><span data-stu-id="3496e-144">bool isProxyRequest</span></span> | <span data-ttu-id="3496e-145">Bu istek proxy kimlik doğrulama kimlik bilgilerini almak ise true.</span><span class="sxs-lookup"><span data-stu-id="3496e-145">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="3496e-146">Uygulama proxy kimlik bilgilerini almak için geçerli değilse, null döndürülmelidir.</span><span class="sxs-lookup"><span data-stu-id="3496e-146">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="3496e-147">bool ısretry</span><span class="sxs-lookup"><span data-stu-id="3496e-147">bool isRetry</span></span> | <span data-ttu-id="3496e-148">Bu URI için önceden kimlik bilgileri isteniyorsa true, ancak sağlanan kimlik bilgileri yetkili erişime izin vermedi.</span><span class="sxs-lookup"><span data-stu-id="3496e-148">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="3496e-149">bool etkileşimsiz</span><span class="sxs-lookup"><span data-stu-id="3496e-149">bool nonInteractive</span></span> | <span data-ttu-id="3496e-150">True ise, kimlik bilgisi sağlayıcısı tüm Kullanıcı istemlerini bastırmalıdır ve bunun yerine varsayılan değerleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="3496e-150">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="3496e-151">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="3496e-151">CancellationToken cancellationToken</span></span> | <span data-ttu-id="3496e-152">Kimlik bilgilerini isteme işleminin iptal edilip edilmediğine yönelik bu iptal belirtecinin denetlenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="3496e-152">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="3496e-153">**Dönüş değeri**: Arabirimi uygulayan bir kimlik bilgileri nesnesi. [ `System.Net.ICredentials` ](/dotnet/api/system.net.icredentials?view=netstandard-2.0)</span><span class="sxs-lookup"><span data-stu-id="3496e-153">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span></span>
