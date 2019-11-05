---
title: NuGet. exe sürümlerini bulmak için Tools. JSON
description: İçin uç nokta
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: a186db9727bdfd1b55bf73a1f29283352555dede
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73611028"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a><span data-ttu-id="ba04b-103">NuGet. exe sürümlerini bulmak için Tools. JSON</span><span class="sxs-lookup"><span data-stu-id="ba04b-103">tools.json for discovering nuget.exe versions</span></span>

<span data-ttu-id="ba04b-104">Bugün, makinenizde bulunan NuGet. exe ' nin en son sürümünü komut dosyası biçiminde bir biçimde almanın birkaç yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="ba04b-104">Today, there are a few ways to get the latest version of nuget.exe on your machine in a scriptable fashion.</span></span> <span data-ttu-id="ba04b-105">Örneğin, nuget.org adresinden [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) paketini indirebilir ve ayıklayabilirsiniz. Bu, zaten NuGet. exe ' ye sahip olmanızı gerektirdiğinden (`nuget.exe install`için) veya temel bir unzip aracı kullanarak. nupkg 'yi açmak ve içinde ikilileri bulmak için bazı karmaşıklığa sahiptir.</span><span class="sxs-lookup"><span data-stu-id="ba04b-105">For example, you can download and extract the [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package from nuget.org. This has some complexity since it either requires that you already have nuget.exe (for `nuget.exe install`) or you have to unzip the .nupkg using a basic unzip tool and find the binary inside.</span></span>

<span data-ttu-id="ba04b-106">Zaten NuGet. exe ' ye sahipseniz `nuget.exe update -self`de kullanabilirsiniz, ancak bunun için aynı NuGet. exe kopyasının olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ba04b-106">If you already have nuget.exe, you can also use `nuget.exe update -self`, however this also requires having an existing copy of nuget.exe.</span></span> <span data-ttu-id="ba04b-107">Bu yaklaşım, sizi en son sürüme de güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="ba04b-107">This approach also updates you to the latest version.</span></span> <span data-ttu-id="ba04b-108">Belirli bir sürümün kullanılmasına izin vermez.</span><span class="sxs-lookup"><span data-stu-id="ba04b-108">It does not allow the use of a specific version.</span></span>

<span data-ttu-id="ba04b-109">`tools.json` uç noktası her ikisi de önyükleme sorununu çözüyor ve indireceğiniz NuGet. exe sürümünün denetimini vermek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ba04b-109">The `tools.json` endpoint is available to both solve the bootstrapping problem and to give control of the version of nuget.exe that you download.</span></span> <span data-ttu-id="ba04b-110">Bu, bir NuGet. exe ' nin yayınlanan sürümünü bulup indirmek için CI/CD ortamlarında veya özel betikte kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ba04b-110">This can be used in CI/CD environments or in custom scripts to discover and download any released version of nuget.exe.</span></span>

<span data-ttu-id="ba04b-111">`tools.json` uç noktası, kimliği doğrulanmamış bir HTTP isteği (örn. `Invoke-WebRequest` PowerShell veya `wget`) kullanılarak getirilebilir.</span><span class="sxs-lookup"><span data-stu-id="ba04b-111">The `tools.json` endpoint can be fetched using an unauthenticated HTTP request (e.g. `Invoke-WebRequest` in PowerShell or `wget`).</span></span> <span data-ttu-id="ba04b-112">JSON seri hale getirici kullanılarak ayrıştırılabilir ve sonraki NuGet. exe indirme URL 'Leri, kimliği doğrulanmamış HTTP istekleri kullanılarak da getirilebilir.</span><span class="sxs-lookup"><span data-stu-id="ba04b-112">It can be parsed using a JSON deserializer and subsequent nuget.exe download URLs can also be fetched using unauthenticated HTTP requests.</span></span>

<span data-ttu-id="ba04b-113">Uç nokta `GET` yöntemi kullanılarak getirilebilir:</span><span class="sxs-lookup"><span data-stu-id="ba04b-113">The endpoint can be fetched using the `GET` method:</span></span>

    GET https://dist.nuget.org/tools.json

<span data-ttu-id="ba04b-114">Uç nokta için [JSON şemasına](https://json-schema.org/) buradan ulaşılabilir:</span><span class="sxs-lookup"><span data-stu-id="ba04b-114">The [JSON schema](https://json-schema.org/) for the endpoint is available here:</span></span>

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a><span data-ttu-id="ba04b-115">Yanıtıyla</span><span class="sxs-lookup"><span data-stu-id="ba04b-115">Response</span></span>

<span data-ttu-id="ba04b-116">Yanıt, NuGet. exe ' nin tüm kullanılabilir sürümlerini içeren bir JSON belgesidir.</span><span class="sxs-lookup"><span data-stu-id="ba04b-116">The response is a JSON document containing all of the available versions of nuget.exe.</span></span>

<span data-ttu-id="ba04b-117">Kök JSON nesnesi aşağıdaki özelliğe sahiptir:</span><span class="sxs-lookup"><span data-stu-id="ba04b-117">The root JSON object has the following property:</span></span>

<span data-ttu-id="ba04b-118">Name</span><span class="sxs-lookup"><span data-stu-id="ba04b-118">Name</span></span>      | <span data-ttu-id="ba04b-119">Tür</span><span class="sxs-lookup"><span data-stu-id="ba04b-119">Type</span></span>             | <span data-ttu-id="ba04b-120">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ba04b-120">Required</span></span>
--------- | ---------------- | --------
<span data-ttu-id="ba04b-121">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="ba04b-121">nuget.exe</span></span> | <span data-ttu-id="ba04b-122">nesne dizisi</span><span class="sxs-lookup"><span data-stu-id="ba04b-122">array of objects</span></span> | <span data-ttu-id="ba04b-123">Yes</span><span class="sxs-lookup"><span data-stu-id="ba04b-123">yes</span></span>

<span data-ttu-id="ba04b-124">`nuget.exe` dizisindeki her bir nesne aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="ba04b-124">Each object in the `nuget.exe` array has the following properties:</span></span>

<span data-ttu-id="ba04b-125">Name</span><span class="sxs-lookup"><span data-stu-id="ba04b-125">Name</span></span>     | <span data-ttu-id="ba04b-126">Tür</span><span class="sxs-lookup"><span data-stu-id="ba04b-126">Type</span></span>   | <span data-ttu-id="ba04b-127">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ba04b-127">Required</span></span> | <span data-ttu-id="ba04b-128">Notlar</span><span class="sxs-lookup"><span data-stu-id="ba04b-128">Notes</span></span>
-------- | ------ | -------- | -----
<span data-ttu-id="ba04b-129">sürüm</span><span class="sxs-lookup"><span data-stu-id="ba04b-129">version</span></span>  | <span data-ttu-id="ba04b-130">dize</span><span class="sxs-lookup"><span data-stu-id="ba04b-130">string</span></span> | <span data-ttu-id="ba04b-131">Yes</span><span class="sxs-lookup"><span data-stu-id="ba04b-131">yes</span></span>      | <span data-ttu-id="ba04b-132">Bir SemVer 2.0.0 dizesi</span><span class="sxs-lookup"><span data-stu-id="ba04b-132">A SemVer 2.0.0 string</span></span>
<span data-ttu-id="ba04b-133">'deki</span><span class="sxs-lookup"><span data-stu-id="ba04b-133">url</span></span>      | <span data-ttu-id="ba04b-134">dize</span><span class="sxs-lookup"><span data-stu-id="ba04b-134">string</span></span> | <span data-ttu-id="ba04b-135">Yes</span><span class="sxs-lookup"><span data-stu-id="ba04b-135">yes</span></span>      | <span data-ttu-id="ba04b-136">NuGet. exe ' nin bu sürümünü indirmek için mutlak URL</span><span class="sxs-lookup"><span data-stu-id="ba04b-136">An absolute URL for downloading this version of nuget.exe</span></span>
<span data-ttu-id="ba04b-137">Aşama</span><span class="sxs-lookup"><span data-stu-id="ba04b-137">stage</span></span>    | <span data-ttu-id="ba04b-138">dize</span><span class="sxs-lookup"><span data-stu-id="ba04b-138">string</span></span> | <span data-ttu-id="ba04b-139">Yes</span><span class="sxs-lookup"><span data-stu-id="ba04b-139">yes</span></span>      | <span data-ttu-id="ba04b-140">Bir sabit listesi dizesi</span><span class="sxs-lookup"><span data-stu-id="ba04b-140">An enum string</span></span>
<span data-ttu-id="ba04b-141">açma</span><span class="sxs-lookup"><span data-stu-id="ba04b-141">uploaded</span></span> | <span data-ttu-id="ba04b-142">dize</span><span class="sxs-lookup"><span data-stu-id="ba04b-142">string</span></span> | <span data-ttu-id="ba04b-143">Yes</span><span class="sxs-lookup"><span data-stu-id="ba04b-143">yes</span></span>      | <span data-ttu-id="ba04b-144">Sürümün kullanılabilir hale getirilme yaklaşık ISO 8601 zaman damgası</span><span class="sxs-lookup"><span data-stu-id="ba04b-144">An approximate ISO 8601 timestamp of when the version was made available</span></span>

<span data-ttu-id="ba04b-145">Dizideki öğeler azalan, SemVer 2.0.0 sırasına göre sıralanır.</span><span class="sxs-lookup"><span data-stu-id="ba04b-145">The items in the array will be sorted in descending, SemVer 2.0.0 order.</span></span> <span data-ttu-id="ba04b-146">Bu garanti, en yüksek sürüm numarasıyla ilgilenen bir istemcinin yükünü azaltmaya yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="ba04b-146">This guarantee is meant to reduce the burden of a client that is interested in highest version number.</span></span> <span data-ttu-id="ba04b-147">Ancak bu, listenin kronolojik sırada sıralanmadığını ifade etmez.</span><span class="sxs-lookup"><span data-stu-id="ba04b-147">However this does mean that the list is not sorted in chronological order.</span></span> <span data-ttu-id="ba04b-148">Örneğin, daha yüksek bir ana sürümden daha sonraki bir tarihte daha düşük bir ana sürüm servise alınmış ise, bu hizmet verilen sürüm listenin en üstünde görünmez.</span><span class="sxs-lookup"><span data-stu-id="ba04b-148">For example, if a lower major version is serviced at a date later than a higher major version, this serviced version will not appear at the top of the list.</span></span> <span data-ttu-id="ba04b-149">En son sürümün *zaman damgasıyla*serbest bırakılacağını istiyorsanız diziyi `uploaded` dize ile sıralayın.</span><span class="sxs-lookup"><span data-stu-id="ba04b-149">If you want the latest version released by *timestamp*, simply sort the array by the `uploaded` string.</span></span> <span data-ttu-id="ba04b-150">Bu, `uploaded` zaman damgası [ıso 8601](https://www.iso.org/iso-8601-date-and-time-format.html) biçiminde olduğundan, bir lexicografik sıralaması kullanılarak kronolojik olarak sıralanabilen (yani basit bir dize sıralaması) bu işe yarar.</span><span class="sxs-lookup"><span data-stu-id="ba04b-150">This works because the `uploaded` timestamp is in the [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format which can be sorted chronologically by using a lexicographical sort (i.e. a simple string sort).</span></span>

<span data-ttu-id="ba04b-151">`stage` özelliği, aracın bu sürümünün ne olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="ba04b-151">The `stage` property indicates how vetted this version of the tool is.</span></span> 

<span data-ttu-id="ba04b-152">Aşama</span><span class="sxs-lookup"><span data-stu-id="ba04b-152">Stage</span></span>              | <span data-ttu-id="ba04b-153">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ba04b-153">Meaning</span></span>
------------------ | ------
<span data-ttu-id="ba04b-154">EarlyAccessPreview</span><span class="sxs-lookup"><span data-stu-id="ba04b-154">EarlyAccessPreview</span></span> | <span data-ttu-id="ba04b-155">Henüz [indirme web sayfasında](https://www.nuget.org/downloads) görünmez ve iş ortakları tarafından doğrulanması gerekir</span><span class="sxs-lookup"><span data-stu-id="ba04b-155">Not yet visible on the [download web page](https://www.nuget.org/downloads) and should be validated by partners</span></span>
<span data-ttu-id="ba04b-156">Yayınlandı</span><span class="sxs-lookup"><span data-stu-id="ba04b-156">Released</span></span>           | <span data-ttu-id="ba04b-157">İndirme sitesinde kullanılabilir ancak geniş yayılmış tüketim için henüz önerilmez</span><span class="sxs-lookup"><span data-stu-id="ba04b-157">Available on the download site but is not yet recommended for wide-spread consumption</span></span>
<span data-ttu-id="ba04b-158">ReleasedAndBlessed</span><span class="sxs-lookup"><span data-stu-id="ba04b-158">ReleasedAndBlessed</span></span> | <span data-ttu-id="ba04b-159">İndirme sitesinde kullanılabilir ve tüketim için önerilir</span><span class="sxs-lookup"><span data-stu-id="ba04b-159">Available on the download site and is recommended for consumption</span></span>

<span data-ttu-id="ba04b-160">En son önerilen sürüme sahip olmanın tek bir yaklaşımı, listenin `ReleasedAndBlessed``stage` değerine sahip ilk sürümü kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="ba04b-160">One simple approach for having the latest, recommended version is to take the first version in the list that has the `stage` value of `ReleasedAndBlessed`.</span></span> <span data-ttu-id="ba04b-161">Sürümler SemVer 2.0.0 Order içinde sıralandığından bu işe yarar.</span><span class="sxs-lookup"><span data-stu-id="ba04b-161">This works because the versions are sorted in SemVer 2.0.0 order.</span></span>

<span data-ttu-id="ba04b-162">Nuget.org üzerindeki `NuGet.CommandLine` paketi genellikle yalnızca `ReleasedAndBlessed` sürümleriyle güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="ba04b-162">The `NuGet.CommandLine` package on nuget.org is typically only updated with `ReleasedAndBlessed` versions.</span></span>

### <a name="sample-request"></a><span data-ttu-id="ba04b-163">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="ba04b-163">Sample request</span></span>

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a><span data-ttu-id="ba04b-164">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="ba04b-164">Sample response</span></span>

[!code-JSON [tools-json.json](./_data/tools-json.json)]
