---
title: Kimliği doğrulanmış akışlardan paketleri kullanma
description: Tüm NuGet istemci senaryolarında kimliği doğrulanmış akışlardan paketleri kullanma
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: e76fefaf4d3c86aa15cf279090c0adb8ed779aab
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901518"
---
# <a name="consuming-packages-from-authenticated-feeds"></a><span data-ttu-id="313cc-103">Kimliği doğrulanmış akışlardan paketleri kullanma</span><span class="sxs-lookup"><span data-stu-id="313cc-103">Consuming packages from authenticated feeds</span></span>

<span data-ttu-id="313cc-104">Nuget.org [genel akışına](https://api.nuget.org/v3/index.json)ek olarak, NuGet istemcilerinin dosya akışlarıyla ve özel http akışlarıyla etkileşim kurma olanağı vardır.</span><span class="sxs-lookup"><span data-stu-id="313cc-104">In addition to the nuget.org [public feed](https://api.nuget.org/v3/index.json), NuGet clients have the ability to interact with file feeds and private http feeds.</span></span>


<span data-ttu-id="313cc-105">Özel http akışlarıyla kimlik doğrulaması yapmak için 2 yaklaşımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="313cc-105">To authenticate with private http feeds, the 2 approaches are:</span></span>

* <span data-ttu-id="313cc-106">[NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials) kimlik bilgilerini ekleme</span><span class="sxs-lookup"><span data-stu-id="313cc-106">Add credentials in the [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)</span></span>
* <span data-ttu-id="313cc-107">Kullanılan istemciye bağlı olarak birçok genişletilebilirlik modelinden birini kullanarak kimlik doğrulaması yapın.</span><span class="sxs-lookup"><span data-stu-id="313cc-107">Authenticate using one of the many extensibility models depending on the client used.</span></span>

## <a name="nuget-clients-authentication-extensibility"></a><span data-ttu-id="313cc-108">NuGet istemcilerinin kimlik doğrulama genişletilebilirliği</span><span class="sxs-lookup"><span data-stu-id="313cc-108">NuGet clients' authentication extensibility</span></span>

<span data-ttu-id="313cc-109">Çeşitli NuGet istemcileri için, özel akış sağlayıcısı kimlik doğrulamasından sorumludur.</span><span class="sxs-lookup"><span data-stu-id="313cc-109">For the various NuGet clients, the private feed provider itself is responsible for authentication.</span></span>
<span data-ttu-id="313cc-110">Tüm NuGet istemcilerinin bunu desteklemeye yönelik genişletilebilirlik yöntemleri vardır.</span><span class="sxs-lookup"><span data-stu-id="313cc-110">All NuGet clients have extensibility methods to support this.</span></span> <span data-ttu-id="313cc-111">Bunlar, kimlik bilgilerini almak için NuGet ile iletişim kurabilen bir Visual Studio uzantısıdır veya bir eklentidir.</span><span class="sxs-lookup"><span data-stu-id="313cc-111">These are either a Visual Studio extension or a plugin that can communicate with NuGet to retrieve credentials.</span></span>

### <a name="visual-studio"></a><span data-ttu-id="313cc-112">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="313cc-112">Visual Studio</span></span>

<span data-ttu-id="313cc-113">NuGet, Visual Studio 'da akış sağlayıcılarının müşterilerine uygulayabilen ve sunabilmeniz için bir arabirim sunar.</span><span class="sxs-lookup"><span data-stu-id="313cc-113">In Visual Studio, NuGet exposes an interface that feed providers can implement and provide to their customers.</span></span> <span data-ttu-id="313cc-114">Daha fazla ayrıntı için lütfen [Visual Studio kimlik bilgisi sağlayıcısı oluşturma](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md)hakkındaki belgelere bakın.</span><span class="sxs-lookup"><span data-stu-id="313cc-114">For more details, please refer to the documentation on [how to create a Visual Studio credential provider](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).</span></span>

#### <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="313cc-115">Visual Studio için kullanılabilir NuGet kimlik bilgileri sağlayıcıları</span><span class="sxs-lookup"><span data-stu-id="313cc-115">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="313cc-116">Azure DevOps 'u desteklemek için Visual Studio 'da yerleşik olarak bulunan bir kimlik bilgisi sağlayıcısı vardır.</span><span class="sxs-lookup"><span data-stu-id="313cc-116">There is a credential provider built into Visual Studio to support Azure DevOps.</span></span>


<span data-ttu-id="313cc-117">Kullanılabilir eklenti kimlik bilgileri sağlayıcıları şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="313cc-117">Available plug-in credential providers include:</span></span>

* [<span data-ttu-id="313cc-118">Visual Studio için MyGet kimlik bilgileri sağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="313cc-118">MyGet Credential Provider for Visual Studio</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a><span data-ttu-id="313cc-119">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="313cc-119">nuget.exe</span></span>

<span data-ttu-id="313cc-120">`nuget.exe`Bir akış ile kimlik doğrulaması yapmak için kimlik bilgileri gerektiğinde, bunları aşağıdaki şekilde arar:</span><span class="sxs-lookup"><span data-stu-id="313cc-120">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="313cc-121">Dosyalardaki kimlik bilgilerini arayın `NuGet.config` .</span><span class="sxs-lookup"><span data-stu-id="313cc-121">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="313cc-122">V2 eklenti kimlik bilgisi sağlayıcılarını kullanma</span><span class="sxs-lookup"><span data-stu-id="313cc-122">Use V2 plug-in credential providers</span></span>
1. <span data-ttu-id="313cc-123">V1 eklenti kimlik bilgisi sağlayıcılarını kullanma</span><span class="sxs-lookup"><span data-stu-id="313cc-123">Use V1 plug-in credential providers</span></span>
1. <span data-ttu-id="313cc-124">Ardından NuGet, kullanıcıdan komut satırında kimlik bilgilerini ister.</span><span class="sxs-lookup"><span data-stu-id="313cc-124">NuGet then prompts the user for credentials on the command line.</span></span>

#### <a name="nugetexe-and-v2-credential-providers"></a><span data-ttu-id="313cc-125">nuget.exe ve v2 kimlik bilgileri sağlayıcıları</span><span class="sxs-lookup"><span data-stu-id="313cc-125">nuget.exe and V2 credential providers</span></span>

<span data-ttu-id="313cc-126">Sürüm `4.8` NuGet sürümünde yeni bir kimlik doğrulama eklentisi mekanizması tanımlanmış ve bundan sonra v2 kimlik bilgileri sağlayıcıları olarak anılacaktır.</span><span class="sxs-lookup"><span data-stu-id="313cc-126">In version `4.8` NuGet defined a new authentication plugin mechanism, hereafter referred to as V2 credential providers.</span></span>
<span data-ttu-id="313cc-127">Bu sağlayıcıların yüklenmesi ve bulunması için bkz. [NuGet platformlar arası eklentileri](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="313cc-127">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="nugetexe-and-v1-credential-providers"></a><span data-ttu-id="313cc-128">nuget.exe ve v1 kimlik bilgileri sağlayıcıları</span><span class="sxs-lookup"><span data-stu-id="313cc-128">nuget.exe and V1 credential providers</span></span>

<span data-ttu-id="313cc-129">Sürüm `3.3` NuGet sürümünde kimlik doğrulama eklentileri 'nin ilk sürümü tanıtılmıştır.</span><span class="sxs-lookup"><span data-stu-id="313cc-129">In version `3.3` NuGet introduced the first version of authentication plugins.</span></span>
<span data-ttu-id="313cc-130">Bu sağlayıcıların yüklenmesi ve bulunması için [nuget.exe kimlik bilgileri sağlayıcılarına](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery) başvurur</span><span class="sxs-lookup"><span data-stu-id="313cc-130">For the installation and discovery of those providers refer to [nuget.exe credential providers](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)</span></span>

#### <a name="available-credential-providers-for-nugetexe"></a><span data-ttu-id="313cc-131">nuget.exe için kullanılabilir kimlik bilgileri sağlayıcıları</span><span class="sxs-lookup"><span data-stu-id="313cc-131">Available credential providers for nuget.exe</span></span>

* <span data-ttu-id="313cc-132">[Azure DevOps v2 kimlik bilgileri sağlayıcıları](/azure/devops/artifacts/nuget/nuget-exe#add-a-feed-to-nuget-482-or-later) veya [Azure Artifacts kimlik bilgisi sağlayıcısı](https://github.com/microsoft/artifacts-credprovider)</span><span class="sxs-lookup"><span data-stu-id="313cc-132">[Azure DevOps V2 Credential Providers](/azure/devops/artifacts/nuget/nuget-exe#add-a-feed-to-nuget-482-or-later) or [Azure Artifacts Credential Provider](https://github.com/microsoft/artifacts-credprovider)</span></span>

<span data-ttu-id="313cc-133">Visual Studio 2017 sürüm 15,9 ve sonraki sürümlerde, Azure DevOps kimlik bilgisi sağlayıcısı Visual Studio 'da paketlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="313cc-133">With Visual Studio 2017 version 15.9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span>
<span data-ttu-id="313cc-134">`nuget.exe`Bu belirli Visual Studio araç takımından MSBuild kullanıyorsa, eklenti otomatik olarak keşfedilir.</span><span class="sxs-lookup"><span data-stu-id="313cc-134">If `nuget.exe` uses MSBuild from that specific Visual Studio toolset, then the plugin will be discovered automatically.</span></span>

### <a name="dotnetexe"></a><span data-ttu-id="313cc-135">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="313cc-135">dotnet.exe</span></span>

<span data-ttu-id="313cc-136">`dotnet.exe`Bir akış ile kimlik doğrulaması yapmak için kimlik bilgileri gerektiğinde, bunları aşağıdaki şekilde arar:</span><span class="sxs-lookup"><span data-stu-id="313cc-136">When `dotnet.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="313cc-137">Dosyalardaki kimlik bilgilerini arayın `NuGet.config` .</span><span class="sxs-lookup"><span data-stu-id="313cc-137">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="313cc-138">V2 eklenti kimlik bilgisi sağlayıcılarını kullanma</span><span class="sxs-lookup"><span data-stu-id="313cc-138">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="313cc-139">, Varsayılan olarak `dotnet.exe` etkileşimli değildir, bu nedenle, `--interactive` kimlik doğrulaması için engelleme aracını almak üzere bir bayrak geçirmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="313cc-139">By default `dotnet.exe` is not interactive, so you might need to pass an `--interactive` flag to get the tool to block for authentication.</span></span>

#### <a name="dotnetexe-and-v2-credential-providers"></a><span data-ttu-id="313cc-140">dotnet.exe ve v2 kimlik bilgileri sağlayıcıları</span><span class="sxs-lookup"><span data-stu-id="313cc-140">dotnet.exe and V2 credential providers</span></span>

<span data-ttu-id="313cc-141">SDK sürümünde `2.2.100` , NuGet tüm istemcilerde çalışacak bir kimlik doğrulama eklentisi mekanizması tanımladı.</span><span class="sxs-lookup"><span data-stu-id="313cc-141">In version `2.2.100` of the SDK, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="313cc-142">Bu sağlayıcıların yüklenmesi ve bulunması için bkz. [NuGet platformlar arası eklentileri](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="313cc-142">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-dotnetexe"></a><span data-ttu-id="313cc-143">dotnet.exe için kullanılabilir kimlik bilgileri sağlayıcıları</span><span class="sxs-lookup"><span data-stu-id="313cc-143">Available credential providers for dotnet.exe</span></span>

* [<span data-ttu-id="313cc-144">Azure Artifacts kimlik bilgisi sağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="313cc-144">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a><span data-ttu-id="313cc-145">MSBuild.exe</span><span class="sxs-lookup"><span data-stu-id="313cc-145">MSBuild.exe</span></span>

<span data-ttu-id="313cc-146">`MSBuild.exe`Bir akış ile kimlik doğrulaması yapmak için kimlik bilgileri gerektiğinde, bunları aşağıdaki şekilde arar:</span><span class="sxs-lookup"><span data-stu-id="313cc-146">When `MSBuild.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="313cc-147">Dosyalardaki kimlik bilgilerini ara `NuGet.config`</span><span class="sxs-lookup"><span data-stu-id="313cc-147">Look for credentials in `NuGet.config` files</span></span>
1. <span data-ttu-id="313cc-148">V2 eklenti kimlik bilgisi sağlayıcılarını kullanma</span><span class="sxs-lookup"><span data-stu-id="313cc-148">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="313cc-149">Varsayılan olarak `MSBuild.exe` etkileşimli değildir, bu nedenle, bir `/p:NuGetInteractive=true` Aracı kimlik doğrulama için engellemek için özelliği ayarlamanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="313cc-149">By default `MSBuild.exe` is not interactive, so you might need to set the `/p:NuGetInteractive=true` property to get the tool to block for authentication.</span></span>

#### <a name="msbuildexe-and-v2-credential-providers"></a><span data-ttu-id="313cc-150">MSBuild.exe ve v2 kimlik bilgileri sağlayıcıları</span><span class="sxs-lookup"><span data-stu-id="313cc-150">MSBuild.exe and V2 credential providers</span></span>

<span data-ttu-id="313cc-151">Visual Studio 2019 güncelleştirme 9 ' da, NuGet tüm istemcilerde çalışacak bir kimlik doğrulama eklentisi mekanizması tanımladı.</span><span class="sxs-lookup"><span data-stu-id="313cc-151">In Visual Studio 2019 Update 9, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="313cc-152">Bu sağlayıcıların yüklenmesi ve bulunması için bkz. [NuGet platformlar arası eklentileri](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span><span class="sxs-lookup"><span data-stu-id="313cc-152">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-msbuildexe"></a><span data-ttu-id="313cc-153">MSBuild.exe için kullanılabilir kimlik bilgileri sağlayıcıları</span><span class="sxs-lookup"><span data-stu-id="313cc-153">Available credential providers for MSBuild.exe</span></span>

* [<span data-ttu-id="313cc-154">Azure Artifacts kimlik bilgisi sağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="313cc-154">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

<span data-ttu-id="313cc-155">Visual Studio 2017 güncelleştirme 9 ve üzeri sürümlerde, Azure DevOps kimlik bilgisi sağlayıcısı Visual Studio 'da paketlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="313cc-155">With Visual Studio 2017 Update 9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span> <span data-ttu-id="313cc-156">Ek adım gerekmez.</span><span class="sxs-lookup"><span data-stu-id="313cc-156">No additional steps are required.</span></span>
