---
title: nuget.exe sürümlerini bulmak için tools.json
description: Uç nokta için
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: 6184fe8e987e0637cb912999f2e3fa3a3dc9b4ba
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546941"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a><span data-ttu-id="e4368-103">nuget.exe sürümlerini bulmak için tools.json</span><span class="sxs-lookup"><span data-stu-id="e4368-103">tools.json for discovering nuget.exe versions</span></span>

<span data-ttu-id="e4368-104">Bugün, kodlanabilir bir biçimde makinenizde nuget.exe en son sürümünü almak için birkaç yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="e4368-104">Today, there are a few ways to get the latest version of nuget.exe on your machine in a scriptable fashion.</span></span> <span data-ttu-id="e4368-105">Örneğin, size indirme ayıklayın ve [ `NuGet.CommandLine` ](https://www.nuget.org/packages/NuGet.CommandLine/) nuget.org paketinden. Ya da nuget.exe sahip olduğunuz gerekir çünkü bu bazı karmaşıklığa sahiptir (için `nuget.exe install`) veya temel unzip aracını kullanarak .nupkg sıkıştırmasını açın ve ikili iç bulun.</span><span class="sxs-lookup"><span data-stu-id="e4368-105">For example, you can download and extract the [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package from nuget.org. This has some complexity since it either requires that you already have nuget.exe (for `nuget.exe install`) or you have to unzip the .nupkg using a basic unzip tool and find the binary inside.</span></span>

<span data-ttu-id="e4368-106">Nuget.exe zaten varsa, ayrıca kullanabileceğiniz `nuget.exe update -self`, ancak bu aynı zamanda bir kopyasının nuget.exe sahip gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e4368-106">If you already have nuget.exe, you can also use `nuget.exe update -self`, however this also requires having an existing copy of nuget.exe.</span></span> <span data-ttu-id="e4368-107">Bu yaklaşım ayrıca en son sürüme güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="e4368-107">This approach also updates you to the latest version.</span></span> <span data-ttu-id="e4368-108">Belirli bir sürümü kullanımına izin vermez.</span><span class="sxs-lookup"><span data-stu-id="e4368-108">It does not allow the use of a specific version.</span></span>

<span data-ttu-id="e4368-109">`tools.json` Uç noktası kullanılabilir hem önyükleme sorunu çözmek ve indirdiğiniz nuget.exe sürümünün denetiminin kendilerinde olmasına.</span><span class="sxs-lookup"><span data-stu-id="e4368-109">The `tools.json` endpoint is available to both solve the bootstrapping problem and to give control of the version of nuget.exe that you download.</span></span> <span data-ttu-id="e4368-110">Bu CI/CD ortamlarda veya özel komut dosyaları bulmak ve nuget.exe yayımlanan herhangi bir sürümünü indirmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e4368-110">This can be used in CI/CD environments or in custom scripts to discover and download any released version of nuget.exe.</span></span>

<span data-ttu-id="e4368-111">`tools.json` Uç noktası getirilen kimliği doğrulanmamış bir HTTP isteği kullanarak (örneğin `Invoke-WebRequest` PowerShell'de veya `wget`).</span><span class="sxs-lookup"><span data-stu-id="e4368-111">The `tools.json` endpoint can be fetched using an unauthenticated HTTP request (e.g. `Invoke-WebRequest` in PowerShell or `wget`).</span></span> <span data-ttu-id="e4368-112">JSON seri durumdan çıkarıcının kullanarak ayrıştırılabilir ve HTTP isteklerini izleyen nuget.exe indirme URL'leri kullanarak da getirilebilir kimliği doğrulanmamış.</span><span class="sxs-lookup"><span data-stu-id="e4368-112">It can be parsed using a JSON deserializer and subsequent nuget.exe download URLs can also be fetched using unauthenticated HTTP requests.</span></span>

<span data-ttu-id="e4368-113">Uç nokta kullanarak getirilebilir `GET` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="e4368-113">The endpoint can be fetched using the `GET` method:</span></span>

    GET https://dist.nuget.org/tools.json

<span data-ttu-id="e4368-114">[JSON şeması](http://json-schema.org/) için uç nokta şuradan ulaşabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e4368-114">The [JSON schema](http://json-schema.org/) for the endpoint is available here:</span></span>

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a><span data-ttu-id="e4368-115">Yanıt</span><span class="sxs-lookup"><span data-stu-id="e4368-115">Response</span></span>

<span data-ttu-id="e4368-116">Tüm kullanılabilir sürümlerini nuget.exe içeren bir JSON belgesi yanıttır.</span><span class="sxs-lookup"><span data-stu-id="e4368-116">The response is a JSON document containing all of the available versions of nuget.exe.</span></span>

<span data-ttu-id="e4368-117">Kök JSON nesnesinin aşağıdaki özellik vardır:</span><span class="sxs-lookup"><span data-stu-id="e4368-117">The root JSON object has the following property:</span></span>

<span data-ttu-id="e4368-118">Ad</span><span class="sxs-lookup"><span data-stu-id="e4368-118">Name</span></span>      | <span data-ttu-id="e4368-119">Tür</span><span class="sxs-lookup"><span data-stu-id="e4368-119">Type</span></span>             | <span data-ttu-id="e4368-120">Gerekli</span><span class="sxs-lookup"><span data-stu-id="e4368-120">Required</span></span>
--------- | ---------------- | --------
<span data-ttu-id="e4368-121">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="e4368-121">nuget.exe</span></span> | <span data-ttu-id="e4368-122">Nesne dizisi</span><span class="sxs-lookup"><span data-stu-id="e4368-122">array of objects</span></span> | <span data-ttu-id="e4368-123">Evet</span><span class="sxs-lookup"><span data-stu-id="e4368-123">yes</span></span>

<span data-ttu-id="e4368-124">Her bir nesnenin `nuget.exe` dizi aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="e4368-124">Each object in the `nuget.exe` array has the following properties:</span></span>

<span data-ttu-id="e4368-125">Ad</span><span class="sxs-lookup"><span data-stu-id="e4368-125">Name</span></span>     | <span data-ttu-id="e4368-126">Tür</span><span class="sxs-lookup"><span data-stu-id="e4368-126">Type</span></span>   | <span data-ttu-id="e4368-127">Gerekli</span><span class="sxs-lookup"><span data-stu-id="e4368-127">Required</span></span> | <span data-ttu-id="e4368-128">Notlar</span><span class="sxs-lookup"><span data-stu-id="e4368-128">Notes</span></span>
-------- | ------ | -------- | -----
<span data-ttu-id="e4368-129">sürüm</span><span class="sxs-lookup"><span data-stu-id="e4368-129">version</span></span>  | <span data-ttu-id="e4368-130">dize</span><span class="sxs-lookup"><span data-stu-id="e4368-130">string</span></span> | <span data-ttu-id="e4368-131">Evet</span><span class="sxs-lookup"><span data-stu-id="e4368-131">yes</span></span>      | <span data-ttu-id="e4368-132">Bir SemVer 2.0.0 dize</span><span class="sxs-lookup"><span data-stu-id="e4368-132">A SemVer 2.0.0 string</span></span>
<span data-ttu-id="e4368-133">URL</span><span class="sxs-lookup"><span data-stu-id="e4368-133">url</span></span>      | <span data-ttu-id="e4368-134">dize</span><span class="sxs-lookup"><span data-stu-id="e4368-134">string</span></span> | <span data-ttu-id="e4368-135">Evet</span><span class="sxs-lookup"><span data-stu-id="e4368-135">yes</span></span>      | <span data-ttu-id="e4368-136">Nuget.exe bu sürümü karşıdan yüklemek için bir mutlak URL</span><span class="sxs-lookup"><span data-stu-id="e4368-136">An absolute URL for downloading this version of nuget.exe</span></span>
<span data-ttu-id="e4368-137">Aşama</span><span class="sxs-lookup"><span data-stu-id="e4368-137">stage</span></span>    | <span data-ttu-id="e4368-138">dize</span><span class="sxs-lookup"><span data-stu-id="e4368-138">string</span></span> | <span data-ttu-id="e4368-139">Evet</span><span class="sxs-lookup"><span data-stu-id="e4368-139">yes</span></span>      | <span data-ttu-id="e4368-140">Bir sabit dize</span><span class="sxs-lookup"><span data-stu-id="e4368-140">An enum string</span></span>
<span data-ttu-id="e4368-141">Karşıya yüklendi</span><span class="sxs-lookup"><span data-stu-id="e4368-141">uploaded</span></span> | <span data-ttu-id="e4368-142">dize</span><span class="sxs-lookup"><span data-stu-id="e4368-142">string</span></span> | <span data-ttu-id="e4368-143">Evet</span><span class="sxs-lookup"><span data-stu-id="e4368-143">yes</span></span>      | <span data-ttu-id="e4368-144">Ne zaman sürümü kullanıma sunuldu, yaklaşık bir zaman damgası</span><span class="sxs-lookup"><span data-stu-id="e4368-144">An approximate timestamp of when the version was made available</span></span>

<span data-ttu-id="e4368-145">Dizideki öğe azalan sırada, SemVer 2.0.0 sırada sıralanacaktır.</span><span class="sxs-lookup"><span data-stu-id="e4368-145">The items in the array will be sorted in descending, SemVer 2.0.0 order.</span></span> <span data-ttu-id="e4368-146">Bu garanti yükünü en yeni sürümüne bakan bir istemci için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="e4368-146">This guarantee is meant to ease the burden on a client looking for the latest version.</span></span> 

<span data-ttu-id="e4368-147">`stage` Özelliği nasıl vettect aracının bu sürümü olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="e4368-147">The `stage` property indicates how vettect this version of the tool is.</span></span> 

<span data-ttu-id="e4368-148">Aşama</span><span class="sxs-lookup"><span data-stu-id="e4368-148">Stage</span></span>              | <span data-ttu-id="e4368-149">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e4368-149">Meaning</span></span>
------------------ | ------
<span data-ttu-id="e4368-150">EarlyAccessPreview</span><span class="sxs-lookup"><span data-stu-id="e4368-150">EarlyAccessPreview</span></span> | <span data-ttu-id="e4368-151">Henüz üzerinde görünür [indirme web sayfasına](https://www.nuget.org/downloads) ve iş ortakları tarafından doğrulanması gerekir</span><span class="sxs-lookup"><span data-stu-id="e4368-151">Not yet visible on the [download web page](https://www.nuget.org/downloads) and should be validated by partners</span></span>
<span data-ttu-id="e4368-152">Yayımlanan</span><span class="sxs-lookup"><span data-stu-id="e4368-152">Released</span></span>           | <span data-ttu-id="e4368-153">İndirme sitesinde kullanılabilir ancak değil ancak geniş yayılım tüketimi için önerilen</span><span class="sxs-lookup"><span data-stu-id="e4368-153">Available on the download site but is not yet recommended for wide-spread consumption</span></span>
<span data-ttu-id="e4368-154">ReleasedAndBlessed</span><span class="sxs-lookup"><span data-stu-id="e4368-154">ReleasedAndBlessed</span></span> | <span data-ttu-id="e4368-155">İndirme sitesinde kullanılabilir ve tüketimi için önerilir</span><span class="sxs-lookup"><span data-stu-id="e4368-155">Available on the download site and is recommended for consumption</span></span>

<span data-ttu-id="e4368-156">Önerilen sürüm en son sahip olmak için bir basit yaklaşım ise ilk sürümü olan listesinde yapılacak `stage` değerini `ReleasedAndBlessed`.</span><span class="sxs-lookup"><span data-stu-id="e4368-156">One simple approach for having the latest, recommended version is to take the first version in the list that has the `stage` value of `ReleasedAndBlessed`.</span></span>

<span data-ttu-id="e4368-157">`NuGet.CommandLine` Nuget.org üzerinde paket genellikle yalnızca güncelleştirilen ile `ReleasedAndBlessed` sürümleri.</span><span class="sxs-lookup"><span data-stu-id="e4368-157">The `NuGet.CommandLine` package on nuget.org is typically only updated with `ReleasedAndBlessed` versions.</span></span>

### <a name="sample-request"></a><span data-ttu-id="e4368-158">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="e4368-158">Sample request</span></span>

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a><span data-ttu-id="e4368-159">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="e4368-159">Sample response</span></span>

[!code-JSON [tools-json.json](./_data/tools-json.json)]
