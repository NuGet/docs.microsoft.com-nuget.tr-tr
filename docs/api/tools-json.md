---
title: nuget.exe sürümlerini bulmak için tools.json
description: Uç nokta için
author: jver
ms.author: jver
manager: skofman
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: d11e79cd9109e1760189e848e35ff322be026a4d
ms.sourcegitcommit: c643dd2c44e085601551ff7079d696bcc3ad2b49
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/21/2018
ms.locfileid: "40248917"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a><span data-ttu-id="a4a23-103">nuget.exe sürümlerini bulmak için tools.json</span><span class="sxs-lookup"><span data-stu-id="a4a23-103">tools.json for discovering nuget.exe versions</span></span>

<span data-ttu-id="a4a23-104">Bugün, kodlanabilir bir biçimde makinenizde nuget.exe en son sürümünü almak için birkaç yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="a4a23-104">Today, there are a few ways to get the latest version of nuget.exe on your machine in a scriptable fashion.</span></span> <span data-ttu-id="a4a23-105">Örneğin, size indirme ayıklayın ve [ `NuGet.CommandLine` ](https://www.nuget.org/packages/NuGet.CommandLine/) nuget.org paketinden. Ya da nuget.exe sahip olduğunuz gerekir çünkü bu bazı karmaşıklığa sahiptir (için `nuget.exe install`) veya temel unzip aracını kullanarak .nupkg sıkıştırmasını açın ve ikili iç bulun.</span><span class="sxs-lookup"><span data-stu-id="a4a23-105">For example, you can download and extract the [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package from nuget.org. This has some complexity since it either requires that you already have nuget.exe (for `nuget.exe install`) or you have to unzip the .nupkg using a basic unzip tool and find the binary inside.</span></span>

<span data-ttu-id="a4a23-106">Nuget.exe zaten varsa, ayrıca kullanabileceğiniz `nuget.exe update -self`, ancak bu aynı zamanda bir kopyasının nuget.exe sahip gerektirir.</span><span class="sxs-lookup"><span data-stu-id="a4a23-106">If you already have nuget.exe, you can also use `nuget.exe update -self`, however this also requires having an existing copy of nuget.exe.</span></span> <span data-ttu-id="a4a23-107">Bu yaklaşım ayrıca en son sürüme güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="a4a23-107">This approach also updates you to the latest version.</span></span> <span data-ttu-id="a4a23-108">Belirli bir sürümü kullanımına izin vermez.</span><span class="sxs-lookup"><span data-stu-id="a4a23-108">It does not allow the use of a specific version.</span></span>

<span data-ttu-id="a4a23-109">`tools.json` Uç noktası kullanılabilir hem önyükleme sorunu çözmek ve indirdiğiniz nuget.exe sürümünün denetiminin kendilerinde olmasına.</span><span class="sxs-lookup"><span data-stu-id="a4a23-109">The `tools.json` endpoint is available to both solve the bootstrapping problem and to give control of the version of nuget.exe that you download.</span></span> <span data-ttu-id="a4a23-110">Bu CI/CD ortamlarda veya özel komut dosyaları bulmak ve nuget.exe yayımlanan herhangi bir sürümünü indirmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a4a23-110">This can be used in CI/CD environments or in custom scripts to discover and download any released version of nuget.exe.</span></span>

<span data-ttu-id="a4a23-111">`tools.json` Uç noktası getirilen kimliği doğrulanmamış bir HTTP isteği kullanarak (örneğin `Invoke-WebRequest` PowerShell'de veya `wget`).</span><span class="sxs-lookup"><span data-stu-id="a4a23-111">The `tools.json` endpoint can be fetched using an unauthenticated HTTP request (e.g. `Invoke-WebRequest` in PowerShell or `wget`).</span></span> <span data-ttu-id="a4a23-112">JSON seri durumdan çıkarıcının kullanarak ayrıştırılabilir ve HTTP isteklerini izleyen nuget.exe indirme URL'leri kullanarak da getirilebilir kimliği doğrulanmamış.</span><span class="sxs-lookup"><span data-stu-id="a4a23-112">It can be parsed using a JSON deserializer and subsequent nuget.exe download URLs can also be fetched using unauthenticated HTTP requests.</span></span>

<span data-ttu-id="a4a23-113">Uç nokta kullanarak getirilebilir `GET` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="a4a23-113">The endpoint can be fetched using the `GET` method:</span></span>

    GET https://dist.nuget.org/tools.json

<span data-ttu-id="a4a23-114">[JSON şeması](http://json-schema.org/) için uç nokta şuradan ulaşabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a4a23-114">The [JSON schema](http://json-schema.org/) for the endpoint is available here:</span></span>

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a><span data-ttu-id="a4a23-115">Yanıt</span><span class="sxs-lookup"><span data-stu-id="a4a23-115">Response</span></span>

<span data-ttu-id="a4a23-116">Tüm kullanılabilir sürümlerini nuget.exe içeren bir JSON belgesi yanıttır.</span><span class="sxs-lookup"><span data-stu-id="a4a23-116">The response is a JSON document containing all of the available versions of nuget.exe.</span></span>

<span data-ttu-id="a4a23-117">Kök JSON nesnesinin aşağıdaki özellik vardır:</span><span class="sxs-lookup"><span data-stu-id="a4a23-117">The root JSON object has the following property:</span></span>

<span data-ttu-id="a4a23-118">Ad</span><span class="sxs-lookup"><span data-stu-id="a4a23-118">Name</span></span>      | <span data-ttu-id="a4a23-119">Tür</span><span class="sxs-lookup"><span data-stu-id="a4a23-119">Type</span></span>             | <span data-ttu-id="a4a23-120">Gerekli</span><span class="sxs-lookup"><span data-stu-id="a4a23-120">Required</span></span>
--------- | ---------------- | --------
<span data-ttu-id="a4a23-121">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="a4a23-121">nuget.exe</span></span> | <span data-ttu-id="a4a23-122">Nesne dizisi</span><span class="sxs-lookup"><span data-stu-id="a4a23-122">array of objects</span></span> | <span data-ttu-id="a4a23-123">Evet</span><span class="sxs-lookup"><span data-stu-id="a4a23-123">yes</span></span>

<span data-ttu-id="a4a23-124">Her bir nesnenin `nuget.exe` dizi aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="a4a23-124">Each object in the `nuget.exe` array has the following properties:</span></span>

<span data-ttu-id="a4a23-125">Ad</span><span class="sxs-lookup"><span data-stu-id="a4a23-125">Name</span></span>     | <span data-ttu-id="a4a23-126">Tür</span><span class="sxs-lookup"><span data-stu-id="a4a23-126">Type</span></span>   | <span data-ttu-id="a4a23-127">Gerekli</span><span class="sxs-lookup"><span data-stu-id="a4a23-127">Required</span></span> | <span data-ttu-id="a4a23-128">Notlar</span><span class="sxs-lookup"><span data-stu-id="a4a23-128">Notes</span></span>
-------- | ------ | -------- | -----
<span data-ttu-id="a4a23-129">sürüm</span><span class="sxs-lookup"><span data-stu-id="a4a23-129">version</span></span>  | <span data-ttu-id="a4a23-130">dize</span><span class="sxs-lookup"><span data-stu-id="a4a23-130">string</span></span> | <span data-ttu-id="a4a23-131">Evet</span><span class="sxs-lookup"><span data-stu-id="a4a23-131">yes</span></span>      | <span data-ttu-id="a4a23-132">Bir SemVer 2.0.0 dize</span><span class="sxs-lookup"><span data-stu-id="a4a23-132">A SemVer 2.0.0 string</span></span>
<span data-ttu-id="a4a23-133">URL</span><span class="sxs-lookup"><span data-stu-id="a4a23-133">url</span></span>      | <span data-ttu-id="a4a23-134">dize</span><span class="sxs-lookup"><span data-stu-id="a4a23-134">string</span></span> | <span data-ttu-id="a4a23-135">Evet</span><span class="sxs-lookup"><span data-stu-id="a4a23-135">yes</span></span>      | <span data-ttu-id="a4a23-136">Nuget.exe bu sürümü karşıdan yüklemek için bir mutlak URL</span><span class="sxs-lookup"><span data-stu-id="a4a23-136">An absolute URL for downloading this version of nuget.exe</span></span>
<span data-ttu-id="a4a23-137">Aşama</span><span class="sxs-lookup"><span data-stu-id="a4a23-137">stage</span></span>    | <span data-ttu-id="a4a23-138">dize</span><span class="sxs-lookup"><span data-stu-id="a4a23-138">string</span></span> | <span data-ttu-id="a4a23-139">Evet</span><span class="sxs-lookup"><span data-stu-id="a4a23-139">yes</span></span>      | <span data-ttu-id="a4a23-140">Bir sabit dize</span><span class="sxs-lookup"><span data-stu-id="a4a23-140">An enum string</span></span>
<span data-ttu-id="a4a23-141">Karşıya yüklendi</span><span class="sxs-lookup"><span data-stu-id="a4a23-141">uploaded</span></span> | <span data-ttu-id="a4a23-142">dize</span><span class="sxs-lookup"><span data-stu-id="a4a23-142">string</span></span> | <span data-ttu-id="a4a23-143">Evet</span><span class="sxs-lookup"><span data-stu-id="a4a23-143">yes</span></span>      | <span data-ttu-id="a4a23-144">Ne zaman sürümü kullanıma sunuldu, yaklaşık bir zaman damgası</span><span class="sxs-lookup"><span data-stu-id="a4a23-144">An approximate timestamp of when the version was made available</span></span>

<span data-ttu-id="a4a23-145">Dizideki öğe azalan sırada, SemVer 2.0.0 sırada sıralanacaktır.</span><span class="sxs-lookup"><span data-stu-id="a4a23-145">The items in the array will be sorted in descending, SemVer 2.0.0 order.</span></span> <span data-ttu-id="a4a23-146">Bu garanti yükünü en yeni sürümüne bakan bir istemci için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="a4a23-146">This guarantee is meant to ease the burden on a client looking for the latest version.</span></span> 

<span data-ttu-id="a4a23-147">`stage` Özelliği nasıl vettect aracının bu sürümü olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="a4a23-147">The `stage` property indicates how vettect this version of the tool is.</span></span> 

<span data-ttu-id="a4a23-148">Aşama</span><span class="sxs-lookup"><span data-stu-id="a4a23-148">Stage</span></span>              | <span data-ttu-id="a4a23-149">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a4a23-149">Meaning</span></span>
------------------ | ------
<span data-ttu-id="a4a23-150">EarlyAccessPreview</span><span class="sxs-lookup"><span data-stu-id="a4a23-150">EarlyAccessPreview</span></span> | <span data-ttu-id="a4a23-151">Henüz üzerinde görünür [indirme web sayfasına](https://www.nuget.org/downloads) ve iş ortakları tarafından doğrulanması gerekir</span><span class="sxs-lookup"><span data-stu-id="a4a23-151">Not yet visible on the [download web page](https://www.nuget.org/downloads) and should be validated by partners</span></span>
<span data-ttu-id="a4a23-152">Yayımlanan</span><span class="sxs-lookup"><span data-stu-id="a4a23-152">Released</span></span>           | <span data-ttu-id="a4a23-153">İndirme sitesinde kullanılabilir ancak değil ancak geniş yayılım tüketimi için önerilen</span><span class="sxs-lookup"><span data-stu-id="a4a23-153">Available on the download site but is not yet recommended for wide-spread consumption</span></span>
<span data-ttu-id="a4a23-154">ReleasedAndBlessed</span><span class="sxs-lookup"><span data-stu-id="a4a23-154">ReleasedAndBlessed</span></span> | <span data-ttu-id="a4a23-155">İndirme sitesinde kullanılabilir ve tüketimi için önerilir</span><span class="sxs-lookup"><span data-stu-id="a4a23-155">Available on the download site and is recommended for consumption</span></span>

<span data-ttu-id="a4a23-156">Önerilen sürüm en son sahip olmak için bir basit yaklaşım ise ilk sürümü olan listesinde yapılacak `stage` değerini `ReleasedAndBlessed`.</span><span class="sxs-lookup"><span data-stu-id="a4a23-156">One simple approach for having the latest, recommended version is to take the first version in the list that has the `stage` value of `ReleasedAndBlessed`.</span></span>

<span data-ttu-id="a4a23-157">`NuGet.CommandLine` Nuget.org üzerinde paket genellikle yalnızca güncelleştirilen ile `ReleasedAndBlessed` sürümleri.</span><span class="sxs-lookup"><span data-stu-id="a4a23-157">The `NuGet.CommandLine` package on nuget.org is typically only updated with `ReleasedAndBlessed` versions.</span></span>

### <a name="sample-request"></a><span data-ttu-id="a4a23-158">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="a4a23-158">Sample request</span></span>

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a><span data-ttu-id="a4a23-159">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="a4a23-159">Sample response</span></span>

[!code-JSON [tools-json.json](./_data/tools-json.json)]
