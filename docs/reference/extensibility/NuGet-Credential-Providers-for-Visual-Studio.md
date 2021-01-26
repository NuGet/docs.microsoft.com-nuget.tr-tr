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
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="89379-103">NuGet kimlik bilgisi sağlayıcılarıyla Visual Studio 'da akışlara kimlik doğrulama</span><span class="sxs-lookup"><span data-stu-id="89379-103">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="89379-104">NuGet Visual Studio Uzantısı 3.6 + kimlik bilgisi sağlayıcılarını destekler, bu da NuGet 'nin kimliği doğrulanmış akışlarla çalışmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="89379-104">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="89379-105">Visual Studio için bir NuGet kimlik bilgisi sağlayıcısı yükledikten sonra, NuGet Visual Studio uzantısı gerektiğinde kimliği doğrulanmış akışlar için kimlik bilgilerini otomatik olarak elde eder ve yeniler.</span><span class="sxs-lookup"><span data-stu-id="89379-105">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="89379-106">Örnek bir uygulama [VsCredentialProvider örneğinde](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="89379-106">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="89379-107">NuGet, Visual Studio içinde `VsCredentialProviderImporter` eklenti kimlik bilgisi sağlayıcılarını da tarayan bir dahili kullanır.</span><span class="sxs-lookup"><span data-stu-id="89379-107">Within Visual Studio, NuGet uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="89379-108">Bu eklenti kimlik bilgisi sağlayıcılarının türü MEF dışarı aktarma olarak bulunabilir olması gerekir `IVsCredentialProvider` .</span><span class="sxs-lookup"><span data-stu-id="89379-108">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="89379-109">Visual Studio 'da 4.8 + NuGet ile başlayarak yeni platformlar arası kimlik doğrulama eklentileri de desteklenir, ancak performans nedenleriyle bu önerilen yaklaşımlar değildir.</span><span class="sxs-lookup"><span data-stu-id="89379-109">Starting with 4.8+ NuGet in Visual Studio supports the new cross platform authentication plugins as well, but they are not the recommended approach for performance reasons.</span></span>

> [!Note]
> <span data-ttu-id="89379-110">Visual Studio için NuGet kimlik bilgileri sağlayıcıları, düzenli bir Visual Studio uzantısı olarak yüklenmelidir ve [Visual studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe) veya üstünü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="89379-110">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe) or above.</span></span>
>
> <span data-ttu-id="89379-111">Visual Studio için NuGet kimlik bilgileri sağlayıcıları yalnızca Visual Studio 'da çalışır (dotnet restore veya nuget.exe değil).</span><span class="sxs-lookup"><span data-stu-id="89379-111">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="89379-112">nuget.exe olan kimlik bilgileri sağlayıcıları için bkz. [nuget.exe kimlik bilgileri sağlayıcıları](nuget-exe-Credential-providers.md).</span><span class="sxs-lookup"><span data-stu-id="89379-112">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>
> <span data-ttu-id="89379-113">DotNet ve MSBuild 'teki kimlik bilgileri sağlayıcıları için bkz. [NuGet platformlar arası eklentileri](nuget-cross-platform-authentication-plugin.md)</span><span class="sxs-lookup"><span data-stu-id="89379-113">For credential providers in dotnet and msbuild see [NuGet cross platform plugins](nuget-cross-platform-authentication-plugin.md)</span></span>

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="89379-114">Visual Studio için NuGet kimlik bilgileri sağlayıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="89379-114">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="89379-115">NuGet Visual Studio Uzantısı 3.6 + kimlik bilgilerini almak için kullanılan bir iç CredentialService uygular.</span><span class="sxs-lookup"><span data-stu-id="89379-115">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="89379-116">CredentialService, yerleşik ve eklenti kimlik bilgisi sağlayıcılarının bir listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="89379-116">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="89379-117">Her sağlayıcı, kimlik bilgileri alınana kadar sırayla denenir.</span><span class="sxs-lookup"><span data-stu-id="89379-117">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="89379-118">Kimlik bilgisi alma sırasında kimlik bilgisi hizmeti kimlik bilgisi sağlayıcılarını aşağıdaki sırayla dener, kimlik bilgileri elde edilir almaz durdurulur:</span><span class="sxs-lookup"><span data-stu-id="89379-118">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="89379-119">Kimlik bilgileri NuGet yapılandırma dosyalarından alınacaktır (yerleşik kullanılarak `SettingsCredentialProvider` ).</span><span class="sxs-lookup"><span data-stu-id="89379-119">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="89379-120">Paket kaynağı Visual Studio Team Services ise, kullanılacaktır `VisualStudioAccountProvider` .</span><span class="sxs-lookup"><span data-stu-id="89379-120">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="89379-121">Diğer tüm eklenti Visual Studio kimlik bilgileri sağlayıcıları sırayla denenecek.</span><span class="sxs-lookup"><span data-stu-id="89379-121">All other plug-in Visual Studio credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="89379-122">Tüm NuGet platformlar arası kimlik bilgisi sağlayıcılarını sırayla kullanmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="89379-122">Try to use all NuGet cross platform credential providers sequentially.</span></span>
1. <span data-ttu-id="89379-123">Henüz kimlik bilgileri alınmadıysa, kullanıcıdan standart temel kimlik doğrulama iletişim kutusu kullanılarak kimlik bilgileri istenir.</span><span class="sxs-lookup"><span data-stu-id="89379-123">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="89379-124">IVsCredentialProvider. GetCredentialsAsync uygulama</span><span class="sxs-lookup"><span data-stu-id="89379-124">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="89379-125">Visual Studio için bir NuGet kimlik bilgisi sağlayıcısı oluşturmak için, türü uygulayan bir genel MEF dışa aktarma Işlemini kullanıma sunan bir Visual Studio uzantısı oluşturun `IVsCredentialProvider` ve aşağıda özetlenen ilkelere uyar.</span><span class="sxs-lookup"><span data-stu-id="89379-125">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

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

<span data-ttu-id="89379-126">Örnek bir uygulama [VsCredentialProvider örneğinde](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="89379-126">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="89379-127">Visual Studio için her NuGet kimlik bilgisi sağlayıcısı şunları vermelidir:</span><span class="sxs-lookup"><span data-stu-id="89379-127">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="89379-128">Kimlik bilgilerinin alımı başlatmadan önce hedeflenen URI için kimlik bilgileri sağlayıp sağlayamayacağını belirleme.</span><span class="sxs-lookup"><span data-stu-id="89379-128">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="89379-129">Sağlayıcı, hedeflenen kaynak için kimlik bilgilerini sağlaya, sonra döndürmelidir `null` .</span><span class="sxs-lookup"><span data-stu-id="89379-129">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="89379-130">Sağlayıcı hedeflenen URI için istekleri işler, ancak kimlik bilgilerini sağlayamadığında, bir özel durum oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="89379-130">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="89379-131">Visual Studio için özel bir NuGet kimlik bilgisi sağlayıcısı, `IVsCredentialProvider` [NuGet. VisualStudio paketinde](https://www.nuget.org/packages/NuGet.VisualStudio/)kullanılabilir arabirimi uygulamalıdır.</span><span class="sxs-lookup"><span data-stu-id="89379-131">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="89379-132">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="89379-132">GetCredentialAsync</span></span>

| <span data-ttu-id="89379-133">Giriş parametresi</span><span class="sxs-lookup"><span data-stu-id="89379-133">Input Parameter</span></span> |<span data-ttu-id="89379-134">Açıklama</span><span class="sxs-lookup"><span data-stu-id="89379-134">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="89379-135">URI URI 'si</span><span class="sxs-lookup"><span data-stu-id="89379-135">Uri uri</span></span> | <span data-ttu-id="89379-136">Kimlik bilgilerinin istenmekte olduğu paket kaynak URI 'Si.</span><span class="sxs-lookup"><span data-stu-id="89379-136">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="89379-137">IWebProxy ara sunucusu</span><span class="sxs-lookup"><span data-stu-id="89379-137">IWebProxy proxy</span></span> | <span data-ttu-id="89379-138">Ağ üzerinde iletişim kurarken kullanılacak Web proxy 'si.</span><span class="sxs-lookup"><span data-stu-id="89379-138">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="89379-139">Yapılandırılmış bir proxy kimlik doğrulaması yoksa null.</span><span class="sxs-lookup"><span data-stu-id="89379-139">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="89379-140">bool ıproxyrequest</span><span class="sxs-lookup"><span data-stu-id="89379-140">bool isProxyRequest</span></span> | <span data-ttu-id="89379-141">Bu istek proxy kimlik doğrulama kimlik bilgilerini almak ise true.</span><span class="sxs-lookup"><span data-stu-id="89379-141">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="89379-142">Uygulama proxy kimlik bilgilerini almak için geçerli değilse, null döndürülmelidir.</span><span class="sxs-lookup"><span data-stu-id="89379-142">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="89379-143">bool ısretry</span><span class="sxs-lookup"><span data-stu-id="89379-143">bool isRetry</span></span> | <span data-ttu-id="89379-144">Bu URI için önceden kimlik bilgileri isteniyorsa true, ancak sağlanan kimlik bilgileri yetkili erişime izin vermedi.</span><span class="sxs-lookup"><span data-stu-id="89379-144">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="89379-145">bool etkileşimsiz</span><span class="sxs-lookup"><span data-stu-id="89379-145">bool nonInteractive</span></span> | <span data-ttu-id="89379-146">True ise, kimlik bilgisi sağlayıcısı tüm Kullanıcı istemlerini bastırmalıdır ve bunun yerine varsayılan değerleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="89379-146">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="89379-147">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="89379-147">CancellationToken cancellationToken</span></span> | <span data-ttu-id="89379-148">Kimlik bilgilerini isteme işleminin iptal edilip edilmediğine yönelik bu iptal belirtecinin denetlenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="89379-148">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="89379-149">**Dönüş değeri**: [ `System.Net.ICredentials` arabirimi](/dotnet/api/system.net.icredentials?view=netstandard-2.0)uygulayan bir kimlik bilgileri nesnesi.</span><span class="sxs-lookup"><span data-stu-id="89379-149">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span></span>
