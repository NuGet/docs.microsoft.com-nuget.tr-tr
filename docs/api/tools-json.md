---
title: nuget.exe sürümlerini bulmak için tools.json
description: Uç nokta için
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: 003139abac7808dbdaef4aa66119e09772db2b4f
ms.sourcegitcommit: b6efd4b210d92bf163c67e412ca9a5a018d117f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/26/2019
ms.locfileid: "56852539"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a><span data-ttu-id="d856c-103">nuget.exe sürümlerini bulmak için tools.json</span><span class="sxs-lookup"><span data-stu-id="d856c-103">tools.json for discovering nuget.exe versions</span></span>

<span data-ttu-id="d856c-104">Bugün, kodlanabilir bir biçimde makinenizde nuget.exe en son sürümünü almak için birkaç yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="d856c-104">Today, there are a few ways to get the latest version of nuget.exe on your machine in a scriptable fashion.</span></span> <span data-ttu-id="d856c-105">Örneğin, size indirme ayıklayın ve [ `NuGet.CommandLine` ](https://www.nuget.org/packages/NuGet.CommandLine/) nuget.org paketinden. Ya da nuget.exe sahip olduğunuz gerekir çünkü bu bazı karmaşıklığa sahiptir (için `nuget.exe install`) veya temel unzip aracını kullanarak .nupkg sıkıştırmasını açın ve ikili iç bulun.</span><span class="sxs-lookup"><span data-stu-id="d856c-105">For example, you can download and extract the [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package from nuget.org. This has some complexity since it either requires that you already have nuget.exe (for `nuget.exe install`) or you have to unzip the .nupkg using a basic unzip tool and find the binary inside.</span></span>

<span data-ttu-id="d856c-106">Nuget.exe zaten varsa, ayrıca kullanabileceğiniz `nuget.exe update -self`, ancak bu aynı zamanda bir kopyasının nuget.exe sahip gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d856c-106">If you already have nuget.exe, you can also use `nuget.exe update -self`, however this also requires having an existing copy of nuget.exe.</span></span> <span data-ttu-id="d856c-107">Bu yaklaşım ayrıca en son sürüme güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="d856c-107">This approach also updates you to the latest version.</span></span> <span data-ttu-id="d856c-108">Belirli bir sürümü kullanımına izin vermez.</span><span class="sxs-lookup"><span data-stu-id="d856c-108">It does not allow the use of a specific version.</span></span>

<span data-ttu-id="d856c-109">`tools.json` Uç noktası kullanılabilir hem önyükleme sorunu çözmek ve indirdiğiniz nuget.exe sürümünün denetiminin kendilerinde olmasına.</span><span class="sxs-lookup"><span data-stu-id="d856c-109">The `tools.json` endpoint is available to both solve the bootstrapping problem and to give control of the version of nuget.exe that you download.</span></span> <span data-ttu-id="d856c-110">Bu CI/CD ortamlarda veya özel komut dosyaları bulmak ve nuget.exe yayımlanan herhangi bir sürümünü indirmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d856c-110">This can be used in CI/CD environments or in custom scripts to discover and download any released version of nuget.exe.</span></span>

<span data-ttu-id="d856c-111">`tools.json` Uç noktası getirilen kimliği doğrulanmamış bir HTTP isteği kullanarak (örneğin `Invoke-WebRequest` PowerShell'de veya `wget`).</span><span class="sxs-lookup"><span data-stu-id="d856c-111">The `tools.json` endpoint can be fetched using an unauthenticated HTTP request (e.g. `Invoke-WebRequest` in PowerShell or `wget`).</span></span> <span data-ttu-id="d856c-112">JSON seri durumdan çıkarıcının kullanarak ayrıştırılabilir ve HTTP isteklerini izleyen nuget.exe indirme URL'leri kullanarak da getirilebilir kimliği doğrulanmamış.</span><span class="sxs-lookup"><span data-stu-id="d856c-112">It can be parsed using a JSON deserializer and subsequent nuget.exe download URLs can also be fetched using unauthenticated HTTP requests.</span></span>

<span data-ttu-id="d856c-113">Uç nokta kullanarak getirilebilir `GET` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="d856c-113">The endpoint can be fetched using the `GET` method:</span></span>

    GET https://dist.nuget.org/tools.json

<span data-ttu-id="d856c-114">[JSON şeması](http://json-schema.org/) için uç nokta şuradan ulaşabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d856c-114">The [JSON schema](http://json-schema.org/) for the endpoint is available here:</span></span>

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a><span data-ttu-id="d856c-115">Yanıt</span><span class="sxs-lookup"><span data-stu-id="d856c-115">Response</span></span>

<span data-ttu-id="d856c-116">Tüm kullanılabilir sürümlerini nuget.exe içeren bir JSON belgesi yanıttır.</span><span class="sxs-lookup"><span data-stu-id="d856c-116">The response is a JSON document containing all of the available versions of nuget.exe.</span></span>

<span data-ttu-id="d856c-117">Kök JSON nesnesinin aşağıdaki özellik vardır:</span><span class="sxs-lookup"><span data-stu-id="d856c-117">The root JSON object has the following property:</span></span>

<span data-ttu-id="d856c-118">Ad</span><span class="sxs-lookup"><span data-stu-id="d856c-118">Name</span></span>      | <span data-ttu-id="d856c-119">Tür</span><span class="sxs-lookup"><span data-stu-id="d856c-119">Type</span></span>             | <span data-ttu-id="d856c-120">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d856c-120">Required</span></span>
--------- | ---------------- | --------
<span data-ttu-id="d856c-121">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="d856c-121">nuget.exe</span></span> | <span data-ttu-id="d856c-122">Nesne dizisi</span><span class="sxs-lookup"><span data-stu-id="d856c-122">array of objects</span></span> | <span data-ttu-id="d856c-123">evet</span><span class="sxs-lookup"><span data-stu-id="d856c-123">yes</span></span>

<span data-ttu-id="d856c-124">Her bir nesnenin `nuget.exe` dizi aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="d856c-124">Each object in the `nuget.exe` array has the following properties:</span></span>

<span data-ttu-id="d856c-125">Ad</span><span class="sxs-lookup"><span data-stu-id="d856c-125">Name</span></span>     | <span data-ttu-id="d856c-126">Tür</span><span class="sxs-lookup"><span data-stu-id="d856c-126">Type</span></span>   | <span data-ttu-id="d856c-127">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d856c-127">Required</span></span> | <span data-ttu-id="d856c-128">Notlar</span><span class="sxs-lookup"><span data-stu-id="d856c-128">Notes</span></span>
-------- | ------ | -------- | -----
<span data-ttu-id="d856c-129">sürüm</span><span class="sxs-lookup"><span data-stu-id="d856c-129">version</span></span>  | <span data-ttu-id="d856c-130">dize</span><span class="sxs-lookup"><span data-stu-id="d856c-130">string</span></span> | <span data-ttu-id="d856c-131">evet</span><span class="sxs-lookup"><span data-stu-id="d856c-131">yes</span></span>      | <span data-ttu-id="d856c-132">Bir SemVer 2.0.0 dize</span><span class="sxs-lookup"><span data-stu-id="d856c-132">A SemVer 2.0.0 string</span></span>
<span data-ttu-id="d856c-133">url</span><span class="sxs-lookup"><span data-stu-id="d856c-133">url</span></span>      | <span data-ttu-id="d856c-134">dize</span><span class="sxs-lookup"><span data-stu-id="d856c-134">string</span></span> | <span data-ttu-id="d856c-135">evet</span><span class="sxs-lookup"><span data-stu-id="d856c-135">yes</span></span>      | <span data-ttu-id="d856c-136">Nuget.exe bu sürümü karşıdan yüklemek için bir mutlak URL</span><span class="sxs-lookup"><span data-stu-id="d856c-136">An absolute URL for downloading this version of nuget.exe</span></span>
<span data-ttu-id="d856c-137">Aşama</span><span class="sxs-lookup"><span data-stu-id="d856c-137">stage</span></span>    | <span data-ttu-id="d856c-138">dize</span><span class="sxs-lookup"><span data-stu-id="d856c-138">string</span></span> | <span data-ttu-id="d856c-139">evet</span><span class="sxs-lookup"><span data-stu-id="d856c-139">yes</span></span>      | <span data-ttu-id="d856c-140">Bir sabit dize</span><span class="sxs-lookup"><span data-stu-id="d856c-140">An enum string</span></span>
<span data-ttu-id="d856c-141">Karşıya yüklendi</span><span class="sxs-lookup"><span data-stu-id="d856c-141">uploaded</span></span> | <span data-ttu-id="d856c-142">dize</span><span class="sxs-lookup"><span data-stu-id="d856c-142">string</span></span> | <span data-ttu-id="d856c-143">evet</span><span class="sxs-lookup"><span data-stu-id="d856c-143">yes</span></span>      | <span data-ttu-id="d856c-144">Ne zaman sürümü kullanıma sunuldu, yaklaşık bir ISO 8601 zaman</span><span class="sxs-lookup"><span data-stu-id="d856c-144">An approximate ISO 8601 timestamp of when the version was made available</span></span>

<span data-ttu-id="d856c-145">Dizideki öğe azalan sırada, SemVer 2.0.0 sırada sıralanacaktır.</span><span class="sxs-lookup"><span data-stu-id="d856c-145">The items in the array will be sorted in descending, SemVer 2.0.0 order.</span></span> <span data-ttu-id="d856c-146">Bu garanti en yüksek sürüm numarasını ilgileniyor bir istemci yükünü azaltmak için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="d856c-146">This guarantee is meant to reduce the burden of a client that is interested in highest version number.</span></span> <span data-ttu-id="d856c-147">Ancak bu liste kronolojik sırada sıralanır değil anlamına gelmez.</span><span class="sxs-lookup"><span data-stu-id="d856c-147">However this does mean that the list is not sorted in chronological order.</span></span> <span data-ttu-id="d856c-148">Örneğin, daha düşük bir sürümle daha yüksek bir ana sürüm belirtilenden sonraki bir tarihte bakım yapılır, bu hizmet verilen sürüm listenin en üstünde görünmez.</span><span class="sxs-lookup"><span data-stu-id="d856c-148">For example, if a lower major version is serviced at a date later than a higher major version, this serviced version will not appear at the top of the list.</span></span> <span data-ttu-id="d856c-149">Tarafından yayımlanan en son sürümü istiyorsanız *zaman damgası*, yalnızca dizi tarafından sıralama `uploaded` dize.</span><span class="sxs-lookup"><span data-stu-id="d856c-149">If you want the latest version released by *timestamp*, simply sort the array by the `uploaded` string.</span></span> <span data-ttu-id="d856c-150">Bunun çalışmasının nedeni `uploaded` zaman damgası olan [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) lexicographical sıralama (yani basit dize sıralama) kullanarak tarih sırasına göre sıralanabilir biçimi.</span><span class="sxs-lookup"><span data-stu-id="d856c-150">This works because the `uploaded` timestamp is in the [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format which can be sorted chronologically by using a lexicographical sort (i.e. a simple string sort).</span></span>

<span data-ttu-id="d856c-151">`stage` Özelliği nasıl denetlenen Aracı'nın bu sürümü olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="d856c-151">The `stage` property indicates how vetted this version of the tool is.</span></span> 

<span data-ttu-id="d856c-152">Aşama</span><span class="sxs-lookup"><span data-stu-id="d856c-152">Stage</span></span>              | <span data-ttu-id="d856c-153">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d856c-153">Meaning</span></span>
------------------ | ------
<span data-ttu-id="d856c-154">EarlyAccessPreview</span><span class="sxs-lookup"><span data-stu-id="d856c-154">EarlyAccessPreview</span></span> | <span data-ttu-id="d856c-155">Henüz üzerinde görünür [indirme web sayfasına](https://www.nuget.org/downloads) ve iş ortakları tarafından doğrulanması gerekir</span><span class="sxs-lookup"><span data-stu-id="d856c-155">Not yet visible on the [download web page](https://www.nuget.org/downloads) and should be validated by partners</span></span>
<span data-ttu-id="d856c-156">Yayımlanan</span><span class="sxs-lookup"><span data-stu-id="d856c-156">Released</span></span>           | <span data-ttu-id="d856c-157">İndirme sitesinde kullanılabilir ancak değil ancak geniş yayılım tüketimi için önerilen</span><span class="sxs-lookup"><span data-stu-id="d856c-157">Available on the download site but is not yet recommended for wide-spread consumption</span></span>
<span data-ttu-id="d856c-158">ReleasedAndBlessed</span><span class="sxs-lookup"><span data-stu-id="d856c-158">ReleasedAndBlessed</span></span> | <span data-ttu-id="d856c-159">İndirme sitesinde kullanılabilir ve tüketimi için önerilir</span><span class="sxs-lookup"><span data-stu-id="d856c-159">Available on the download site and is recommended for consumption</span></span>

<span data-ttu-id="d856c-160">Önerilen sürüm en son sahip olmak için bir basit yaklaşım ise ilk sürümü olan listesinde yapılacak `stage` değerini `ReleasedAndBlessed`.</span><span class="sxs-lookup"><span data-stu-id="d856c-160">One simple approach for having the latest, recommended version is to take the first version in the list that has the `stage` value of `ReleasedAndBlessed`.</span></span> <span data-ttu-id="d856c-161">Sürümler SemVer 2.0.0 düzende sıralanır için bu çalışır.</span><span class="sxs-lookup"><span data-stu-id="d856c-161">This works because the versions are sorted in SemVer 2.0.0 order.</span></span>

<span data-ttu-id="d856c-162">`NuGet.CommandLine` Nuget.org üzerinde paket genellikle yalnızca güncelleştirilen ile `ReleasedAndBlessed` sürümleri.</span><span class="sxs-lookup"><span data-stu-id="d856c-162">The `NuGet.CommandLine` package on nuget.org is typically only updated with `ReleasedAndBlessed` versions.</span></span>

### <a name="sample-request"></a><span data-ttu-id="d856c-163">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="d856c-163">Sample request</span></span>

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a><span data-ttu-id="d856c-164">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="d856c-164">Sample response</span></span>

[!code-JSON [tools-json.json](./_data/tools-json.json)]
