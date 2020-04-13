---
title: Kimlik doğrulama akışlarından paketleri tüketme
description: Tüm NuGet istemci senaryolarında kimlik doğrulama akışlarından paketleri tüketme
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: bb624ec6987dd5c6ee38d5bb7e01200487dd4bed
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231793"
---
# <a name="consuming-packages-from-authenticated-feeds"></a><span data-ttu-id="258fa-103">Kimlik doğrulama akışlarından paketleri tüketme</span><span class="sxs-lookup"><span data-stu-id="258fa-103">Consuming packages from authenticated feeds</span></span>

<span data-ttu-id="258fa-104">[nuget.org genel beslemeye](https://api.nuget.org/v3/index.json)ek olarak, NuGet istemcileri dosya akışları ve özel http akışları ile etkileşim yeteneğine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="258fa-104">In addition to the nuget.org [public feed](https://api.nuget.org/v3/index.json), NuGet clients have the ability to interact with file feeds and private http feeds.</span></span>


<span data-ttu-id="258fa-105">Özel http beslemeleri ile doğrulamak için, 2 yaklaşımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="258fa-105">To authenticate with private http feeds, the 2 approaches are:</span></span>

* <span data-ttu-id="258fa-106">[NuGet.config'e](../reference/nuget-config-file.md#packagesourcecredentials) kimlik bilgileri ekleme</span><span class="sxs-lookup"><span data-stu-id="258fa-106">Add credentials in the [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)</span></span>
* <span data-ttu-id="258fa-107">Kullanılan istemciye bağlı olarak birçok genişletilebilirlik modellerinden birini kullanarak kimlik doğrulaması yapın.</span><span class="sxs-lookup"><span data-stu-id="258fa-107">Authenticate using one of the many extensibility models depending on the client used.</span></span>

## <a name="nuget-clients-authentication-extensibility"></a><span data-ttu-id="258fa-108">NuGet istemcilerinin kimlik doğrulama genişletilebilirliği</span><span class="sxs-lookup"><span data-stu-id="258fa-108">NuGet clients' authentication extensibility</span></span>

<span data-ttu-id="258fa-109">Çeşitli NuGet istemcileri için, özel özet akışı sağlayıcısının kendisi kimlik doğrulamadan sorumludur.</span><span class="sxs-lookup"><span data-stu-id="258fa-109">For the various NuGet clients, the private feed provider itself is responsible for authentication.</span></span>
<span data-ttu-id="258fa-110">Tüm NuGet istemcilerinin bunu desteklemek için genişletilebilirlik yöntemleri vardır.</span><span class="sxs-lookup"><span data-stu-id="258fa-110">All NuGet clients have extensibility methods to support this.</span></span> <span data-ttu-id="258fa-111">Bunlar, kimlik bilgilerini almak için NuGet ile iletişim kurabilen bir Visual Studio uzantısı veya eklentidir.</span><span class="sxs-lookup"><span data-stu-id="258fa-111">These are either a Visual Studio extension or a plugin that can communicate with NuGet to retrieve credentials.</span></span>

### <a name="visual-studio"></a><span data-ttu-id="258fa-112">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="258fa-112">Visual Studio</span></span>

<span data-ttu-id="258fa-113">Visual Studio'da NuGet, besleme sağlayıcılarının müşterilerine uygulayabileceği ve sağlayabileceği bir arabirimi ortaya çıkarır.</span><span class="sxs-lookup"><span data-stu-id="258fa-113">In Visual Studio, NuGet exposes an interface that feed providers can implement and provide to their customers.</span></span> <span data-ttu-id="258fa-114">Daha fazla bilgi için lütfen [Visual Studio kimlik bilgileri sağlayıcısının nasıl oluşturulabildiğini](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md)gösteren belgelere bakın.</span><span class="sxs-lookup"><span data-stu-id="258fa-114">For more details, please refer to the documentation on [how to create a Visual Studio credential provider](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).</span></span>

#### <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="258fa-115">Visual Studio için kullanılabilir NuGet kimlik bilgileri sağlayıcıları</span><span class="sxs-lookup"><span data-stu-id="258fa-115">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="258fa-116">Azure DevOps'leri desteklemek için Visual Studio'da yerleşik bir kimlik bilgisi sağlayıcısı vardır.</span><span class="sxs-lookup"><span data-stu-id="258fa-116">There is a credential provider built into Visual Studio to support Azure DevOps.</span></span>


<span data-ttu-id="258fa-117">Kullanılabilir eklenti kimlik bilgileri sağlayıcıları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="258fa-117">Available plug-in credential providers include:</span></span>

* [<span data-ttu-id="258fa-118">Visual Studio için MyGet Kimlik Sağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="258fa-118">MyGet Credential Provider for Visual Studio</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a><span data-ttu-id="258fa-119">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="258fa-119">nuget.exe</span></span>

<span data-ttu-id="258fa-120">Bir `nuget.exe` özet akışıyla kimlik bilgilerinin doğrulanması gerektiğinde, bunları aşağıdaki şekilde arar:</span><span class="sxs-lookup"><span data-stu-id="258fa-120">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="258fa-121">Dosyalardaki kimlik `NuGet.config` bilgilerine bakın.</span><span class="sxs-lookup"><span data-stu-id="258fa-121">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="258fa-122">V2 eklenti kimlik bilgileri sağlayıcılarını kullanma</span><span class="sxs-lookup"><span data-stu-id="258fa-122">Use V2 plug-in credential providers</span></span>
1. <span data-ttu-id="258fa-123">V1 eklenti kimlik bilgileri sağlayıcılarını kullanma</span><span class="sxs-lookup"><span data-stu-id="258fa-123">Use V1 plug-in credential providers</span></span>
1. <span data-ttu-id="258fa-124">NuGet daha sonra komut satırında kimlik bilgileri için kullanıcı ister.</span><span class="sxs-lookup"><span data-stu-id="258fa-124">NuGet then prompts the user for credentials on the command line.</span></span>

#### <a name="nugetexe-and-v2-credential-providers"></a><span data-ttu-id="258fa-125">nuget.exe ve V2 kimlik bilgileri sağlayıcıları</span><span class="sxs-lookup"><span data-stu-id="258fa-125">nuget.exe and V2 credential providers</span></span>

<span data-ttu-id="258fa-126">Sürümde `4.8` NuGet yeni bir kimlik doğrulama eklentisi mekanizması tanımlı, bundan sonra V2 kimlik bilgileri sağlayıcıları olarak anılacaktır.</span><span class="sxs-lookup"><span data-stu-id="258fa-126">In version `4.8` NuGet defined a new authentication plugin mechanism, hereafter referred to as V2 credential providers.</span></span>
<span data-ttu-id="258fa-127">Bu sağlayıcıların kurulumu ve keşfi için [NuGet çapraz platform eklentilerine](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)bakın.</span><span class="sxs-lookup"><span data-stu-id="258fa-127">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="nugetexe-and-v1-credential-providers"></a><span data-ttu-id="258fa-128">nuget.exe ve V1 kimlik bilgileri sağlayıcıları</span><span class="sxs-lookup"><span data-stu-id="258fa-128">nuget.exe and V1 credential providers</span></span>

<span data-ttu-id="258fa-129">Sürümde `3.3` NuGet kimlik doğrulama eklentilerinin ilk sürümünü tanıttı.</span><span class="sxs-lookup"><span data-stu-id="258fa-129">In version `3.3` NuGet introduced the first version of authentication plugins.</span></span>
<span data-ttu-id="258fa-130">Bu sağlayıcıların kurulumu ve keşfi için [nuget.exe kimlik bilgileri sağlayıcılarına](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery) başvurun</span><span class="sxs-lookup"><span data-stu-id="258fa-130">For the installation and discovery of those providers refer to [nuget.exe credential providers](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)</span></span>

#### <a name="available-credential-providers-for-nugetexe"></a><span data-ttu-id="258fa-131">nuget.exe için kullanılabilir kimlik bilgileri sağlayıcıları</span><span class="sxs-lookup"><span data-stu-id="258fa-131">Available credential providers for nuget.exe</span></span>

* <span data-ttu-id="258fa-132">[Azure DevOps V2 Kimlik Bilgileri Sağlayıcıları](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) veya [Azure Yapıları Kimlik Bilgileri Sağlayıcısı](https://github.com/microsoft/artifacts-credprovider)</span><span class="sxs-lookup"><span data-stu-id="258fa-132">[Azure DevOps V2 Credential Providers](/azure/devops/artifacts/nuget/nuget-exe?view=azure-devops#add-a-feed-to-nuget-482-or-later) or [Azure Artifacts Credential Provider](https://github.com/microsoft/artifacts-credprovider)</span></span>

<span data-ttu-id="258fa-133">Visual Studio 2017 sürüm 15.9 ve sonraki sürümlerle Azure DevOps kimlik bilgileri sağlayıcısı Visual Studio'da birlikte sunulur.</span><span class="sxs-lookup"><span data-stu-id="258fa-133">With Visual Studio 2017 version 15.9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span>
<span data-ttu-id="258fa-134">Belirli `nuget.exe` bir Visual Studio araç setinden MSBuild kullanıyorsa, eklenti otomatik olarak keşfedilir.</span><span class="sxs-lookup"><span data-stu-id="258fa-134">If `nuget.exe` uses MSBuild from that specific Visual Studio toolset, then the plugin will be discovered automatically.</span></span>

### <a name="dotnetexe"></a><span data-ttu-id="258fa-135">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="258fa-135">dotnet.exe</span></span>

<span data-ttu-id="258fa-136">Bir `dotnet.exe` özet akışıyla kimlik bilgilerinin doğrulanması gerektiğinde, bunları aşağıdaki şekilde arar:</span><span class="sxs-lookup"><span data-stu-id="258fa-136">When `dotnet.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="258fa-137">Dosyalardaki kimlik `NuGet.config` bilgilerine bakın.</span><span class="sxs-lookup"><span data-stu-id="258fa-137">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="258fa-138">V2 eklenti kimlik bilgileri sağlayıcılarını kullanma</span><span class="sxs-lookup"><span data-stu-id="258fa-138">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="258fa-139">Varsayılan `dotnet.exe` olarak etkileşimli değildir, bu nedenle `--interactive` aracı kimlik doğrulaması için engellemek için bir bayrak geçirmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="258fa-139">By default `dotnet.exe` is not interactive, so you might need to pass an `--interactive` flag to get the tool to block for authentication.</span></span>

#### <a name="dotnetexe-and-v2-credential-providers"></a><span data-ttu-id="258fa-140">dotnet.exe ve V2 kimlik bilgileri sağlayıcıları</span><span class="sxs-lookup"><span data-stu-id="258fa-140">dotnet.exe and V2 credential providers</span></span>

<span data-ttu-id="258fa-141">SDK `2.2.100` sürümünde, NuGet tüm istemcilerde çalışan bir kimlik doğrulama eklentisi mekanizması tanımlamıştır.</span><span class="sxs-lookup"><span data-stu-id="258fa-141">In version `2.2.100` of the SDK, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="258fa-142">Bu sağlayıcıların kurulumu ve keşfi için [NuGet çapraz platform eklentilerine](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)bakın.</span><span class="sxs-lookup"><span data-stu-id="258fa-142">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-dotnetexe"></a><span data-ttu-id="258fa-143">dotnet.exe için kullanılabilir kimlik bilgileri sağlayıcıları</span><span class="sxs-lookup"><span data-stu-id="258fa-143">Available credential providers for dotnet.exe</span></span>

* [<span data-ttu-id="258fa-144">Azure Yapıları Kimlik Bilgileri Sağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="258fa-144">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a><span data-ttu-id="258fa-145">Msbuild.exe</span><span class="sxs-lookup"><span data-stu-id="258fa-145">MSBuild.exe</span></span>

<span data-ttu-id="258fa-146">Bir `MSBuild.exe` özet akışıyla kimlik bilgilerinin doğrulanması gerektiğinde, bunları aşağıdaki şekilde arar:</span><span class="sxs-lookup"><span data-stu-id="258fa-146">When `MSBuild.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="258fa-147">Dosyalarda `NuGet.config` kimlik bilgilerini arama</span><span class="sxs-lookup"><span data-stu-id="258fa-147">Look for credentials in `NuGet.config` files</span></span>
1. <span data-ttu-id="258fa-148">V2 eklenti kimlik bilgileri sağlayıcılarını kullanma</span><span class="sxs-lookup"><span data-stu-id="258fa-148">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="258fa-149">Varsayılan `MSBuild.exe` olarak etkileşimli değildir, bu nedenle `/p:NuGetInteractive=true` aracı kimlik doğrulaması için engellemek için özelliği ayarlamanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="258fa-149">By default `MSBuild.exe` is not interactive, so you might need to set the `/p:NuGetInteractive=true` property to get the tool to block for authentication.</span></span>

#### <a name="msbuildexe-and-v2-credential-providers"></a><span data-ttu-id="258fa-150">MSBuild.exe ve V2 kimlik bilgileri sağlayıcıları</span><span class="sxs-lookup"><span data-stu-id="258fa-150">MSBuild.exe and V2 credential providers</span></span>

<span data-ttu-id="258fa-151">Visual Studio 2019 Update 9'da NuGet, tüm istemcilerde çalışan bir kimlik doğrulama eklentisi mekanizması tanımladı.</span><span class="sxs-lookup"><span data-stu-id="258fa-151">In Visual Studio 2019 Update 9, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="258fa-152">Bu sağlayıcıların kurulumu ve keşfi için [NuGet çapraz platform eklentilerine](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)bakın.</span><span class="sxs-lookup"><span data-stu-id="258fa-152">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-msbuildexe"></a><span data-ttu-id="258fa-153">MSBuild.exe için kullanılabilir kimlik bilgileri sağlayıcıları</span><span class="sxs-lookup"><span data-stu-id="258fa-153">Available credential providers for MSBuild.exe</span></span>

* [<span data-ttu-id="258fa-154">Azure Yapıları Kimlik Bilgileri Sağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="258fa-154">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

<span data-ttu-id="258fa-155">Visual Studio 2017 Update 9 ve sonraki bilgileriyle Azure DevOps kimlik bilgileri sağlayıcısı Visual Studio'da birlikte sunulur.</span><span class="sxs-lookup"><span data-stu-id="258fa-155">With Visual Studio 2017 Update 9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span> <span data-ttu-id="258fa-156">Ek adım gerekmez.</span><span class="sxs-lookup"><span data-stu-id="258fa-156">No additional steps are required.</span></span>
