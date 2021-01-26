---
title: nuget.exe sürümlerini keşfetmek için tools.js
description: İçin uç nokta
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: eb28ccbc4460663b0f149d2d08e9b47dd69847c7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773823"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a><span data-ttu-id="4a543-103">nuget.exe sürümlerini keşfetmek için tools.js</span><span class="sxs-lookup"><span data-stu-id="4a543-103">tools.json for discovering nuget.exe versions</span></span>

<span data-ttu-id="4a543-104">Bugün, makinenizde nuget.exe en son sürümünü bir komut dosyası biçiminde almak için birkaç yol vardır.</span><span class="sxs-lookup"><span data-stu-id="4a543-104">Today, there are a few ways to get the latest version of nuget.exe on your machine in a scriptable fashion.</span></span> <span data-ttu-id="4a543-105">Örneğin, [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) NuGet.org adresinden paketi indirebilir ve ayıklayabilirsiniz. Bu, zaten nuget.exe (için) sahip olmanızı gerektirdiğinden `nuget.exe install` ya da temel bir unzip aracı kullanarak. nupkg 'yi açmak ve içinde ikilileri bulmak için bazı karmaşıklığa sahiptir.</span><span class="sxs-lookup"><span data-stu-id="4a543-105">For example, you can download and extract the [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package from nuget.org. This has some complexity since it either requires that you already have nuget.exe (for `nuget.exe install`) or you have to unzip the .nupkg using a basic unzip tool and find the binary inside.</span></span>

<span data-ttu-id="4a543-106">Zaten nuget.exe varsa, bunu da kullanabilirsiniz `nuget.exe update -self` , ancak bunun için de nuget.exe bir kopyasının olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4a543-106">If you already have nuget.exe, you can also use `nuget.exe update -self`, however this also requires having an existing copy of nuget.exe.</span></span> <span data-ttu-id="4a543-107">Bu yaklaşım, sizi en son sürüme de güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="4a543-107">This approach also updates you to the latest version.</span></span> <span data-ttu-id="4a543-108">Belirli bir sürümün kullanılmasına izin vermez.</span><span class="sxs-lookup"><span data-stu-id="4a543-108">It does not allow the use of a specific version.</span></span>

<span data-ttu-id="4a543-109">`tools.json`Uç nokta her ikisi de önyükleme sorununu çözüyor ve indireceğiniz nuget.exe sürümünün denetimini sağlamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="4a543-109">The `tools.json` endpoint is available to both solve the bootstrapping problem and to give control of the version of nuget.exe that you download.</span></span> <span data-ttu-id="4a543-110">Bu, CI/CD ortamlarında veya nuget.exe yayınlanan herhangi bir sürümünü bulup indirmek için özel betiklerin içinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="4a543-110">This can be used in CI/CD environments or in custom scripts to discover and download any released version of nuget.exe.</span></span>

<span data-ttu-id="4a543-111">`tools.json`Uç nokta, kimliği doğrulanmamış BIR http isteği (örn. `Invoke-WebRequest` PowerShell veya) kullanılarak getirilebilir `wget` .</span><span class="sxs-lookup"><span data-stu-id="4a543-111">The `tools.json` endpoint can be fetched using an unauthenticated HTTP request (e.g. `Invoke-WebRequest` in PowerShell or `wget`).</span></span> <span data-ttu-id="4a543-112">JSON seri hale getirici kullanılarak ayrıştırılabilir ve sonraki nuget.exe indirme URL 'Leri, kimliği doğrulanmamış HTTP istekleri kullanılarak da getirilebilir.</span><span class="sxs-lookup"><span data-stu-id="4a543-112">It can be parsed using a JSON deserializer and subsequent nuget.exe download URLs can also be fetched using unauthenticated HTTP requests.</span></span>

<span data-ttu-id="4a543-113">Uç nokta, yöntemi kullanılarak getirilebilir `GET` :</span><span class="sxs-lookup"><span data-stu-id="4a543-113">The endpoint can be fetched using the `GET` method:</span></span>

```
GET https://dist.nuget.org/tools.json
```

<span data-ttu-id="4a543-114">Uç nokta için [JSON şemasına](https://json-schema.org/) buradan ulaşılabilir:</span><span class="sxs-lookup"><span data-stu-id="4a543-114">The [JSON schema](https://json-schema.org/) for the endpoint is available here:</span></span>

```
GET https://dist.nuget.org/tools.schema.json
```

## <a name="response"></a><span data-ttu-id="4a543-115">Yanıt</span><span class="sxs-lookup"><span data-stu-id="4a543-115">Response</span></span>

<span data-ttu-id="4a543-116">Yanıt, tüm kullanılabilir nuget.exe sürümlerini içeren bir JSON belgesidir.</span><span class="sxs-lookup"><span data-stu-id="4a543-116">The response is a JSON document containing all of the available versions of nuget.exe.</span></span>

<span data-ttu-id="4a543-117">Kök JSON nesnesi aşağıdaki özelliğe sahiptir:</span><span class="sxs-lookup"><span data-stu-id="4a543-117">The root JSON object has the following property:</span></span>

<span data-ttu-id="4a543-118">Ad</span><span class="sxs-lookup"><span data-stu-id="4a543-118">Name</span></span>      | <span data-ttu-id="4a543-119">Tür</span><span class="sxs-lookup"><span data-stu-id="4a543-119">Type</span></span>             | <span data-ttu-id="4a543-120">Gerekli</span><span class="sxs-lookup"><span data-stu-id="4a543-120">Required</span></span>
--------- | ---------------- | --------
<span data-ttu-id="4a543-121">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="4a543-121">nuget.exe</span></span> | <span data-ttu-id="4a543-122">nesne dizisi</span><span class="sxs-lookup"><span data-stu-id="4a543-122">array of objects</span></span> | <span data-ttu-id="4a543-123">evet</span><span class="sxs-lookup"><span data-stu-id="4a543-123">yes</span></span>

<span data-ttu-id="4a543-124">Dizideki her bir nesne `nuget.exe` aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="4a543-124">Each object in the `nuget.exe` array has the following properties:</span></span>

<span data-ttu-id="4a543-125">Ad</span><span class="sxs-lookup"><span data-stu-id="4a543-125">Name</span></span>     | <span data-ttu-id="4a543-126">Tür</span><span class="sxs-lookup"><span data-stu-id="4a543-126">Type</span></span>   | <span data-ttu-id="4a543-127">Gerekli</span><span class="sxs-lookup"><span data-stu-id="4a543-127">Required</span></span> | <span data-ttu-id="4a543-128">Notlar</span><span class="sxs-lookup"><span data-stu-id="4a543-128">Notes</span></span>
-------- | ------ | -------- | -----
<span data-ttu-id="4a543-129">sürüm</span><span class="sxs-lookup"><span data-stu-id="4a543-129">version</span></span>  | <span data-ttu-id="4a543-130">string</span><span class="sxs-lookup"><span data-stu-id="4a543-130">string</span></span> | <span data-ttu-id="4a543-131">evet</span><span class="sxs-lookup"><span data-stu-id="4a543-131">yes</span></span>      | <span data-ttu-id="4a543-132">Bir SemVer 2.0.0 dizesi</span><span class="sxs-lookup"><span data-stu-id="4a543-132">A SemVer 2.0.0 string</span></span>
<span data-ttu-id="4a543-133">url</span><span class="sxs-lookup"><span data-stu-id="4a543-133">url</span></span>      | <span data-ttu-id="4a543-134">string</span><span class="sxs-lookup"><span data-stu-id="4a543-134">string</span></span> | <span data-ttu-id="4a543-135">evet</span><span class="sxs-lookup"><span data-stu-id="4a543-135">yes</span></span>      | <span data-ttu-id="4a543-136">Bu nuget.exe sürümünü indirmek için mutlak URL</span><span class="sxs-lookup"><span data-stu-id="4a543-136">An absolute URL for downloading this version of nuget.exe</span></span>
<span data-ttu-id="4a543-137">sahna</span><span class="sxs-lookup"><span data-stu-id="4a543-137">stage</span></span>    | <span data-ttu-id="4a543-138">string</span><span class="sxs-lookup"><span data-stu-id="4a543-138">string</span></span> | <span data-ttu-id="4a543-139">evet</span><span class="sxs-lookup"><span data-stu-id="4a543-139">yes</span></span>      | <span data-ttu-id="4a543-140">Bir sabit listesi dizesi</span><span class="sxs-lookup"><span data-stu-id="4a543-140">An enum string</span></span>
<span data-ttu-id="4a543-141">açma</span><span class="sxs-lookup"><span data-stu-id="4a543-141">uploaded</span></span> | <span data-ttu-id="4a543-142">string</span><span class="sxs-lookup"><span data-stu-id="4a543-142">string</span></span> | <span data-ttu-id="4a543-143">evet</span><span class="sxs-lookup"><span data-stu-id="4a543-143">yes</span></span>      | <span data-ttu-id="4a543-144">Sürümün kullanılabilir hale getirilme yaklaşık ISO 8601 zaman damgası</span><span class="sxs-lookup"><span data-stu-id="4a543-144">An approximate ISO 8601 timestamp of when the version was made available</span></span>

<span data-ttu-id="4a543-145">Dizideki öğeler azalan, SemVer 2.0.0 sırasına göre sıralanır.</span><span class="sxs-lookup"><span data-stu-id="4a543-145">The items in the array will be sorted in descending, SemVer 2.0.0 order.</span></span> <span data-ttu-id="4a543-146">Bu garanti, en yüksek sürüm numarasıyla ilgilenen bir istemcinin yükünü azaltmaya yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="4a543-146">This guarantee is meant to reduce the burden of a client that is interested in highest version number.</span></span> <span data-ttu-id="4a543-147">Ancak bu, listenin kronolojik sırada sıralanmadığını ifade etmez.</span><span class="sxs-lookup"><span data-stu-id="4a543-147">However this does mean that the list is not sorted in chronological order.</span></span> <span data-ttu-id="4a543-148">Örneğin, daha yüksek bir ana sürümden daha sonraki bir tarihte daha düşük bir ana sürüm servise alınmış ise, bu hizmet verilen sürüm listenin en üstünde görünmez.</span><span class="sxs-lookup"><span data-stu-id="4a543-148">For example, if a lower major version is serviced at a date later than a higher major version, this serviced version will not appear at the top of the list.</span></span> <span data-ttu-id="4a543-149">En son sürümün *zaman damgasıyla* serbest bırakılacağını istiyorsanız diziyi dize ile sıralayın `uploaded` .</span><span class="sxs-lookup"><span data-stu-id="4a543-149">If you want the latest version released by *timestamp*, simply sort the array by the `uploaded` string.</span></span> <span data-ttu-id="4a543-150">Bu, `uploaded` zaman damgası [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) biçiminde olduğundan, bir lexicografik sıralaması kullanılarak kronolojik olarak sıralanabilen (basit bir dize sıralaması) bu işe yarar.</span><span class="sxs-lookup"><span data-stu-id="4a543-150">This works because the `uploaded` timestamp is in the [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format which can be sorted chronologically by using a lexicographical sort (i.e. a simple string sort).</span></span>

<span data-ttu-id="4a543-151">`stage`Özelliği, aracın bu sürümünün ne olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="4a543-151">The `stage` property indicates how vetted this version of the tool is.</span></span> 

<span data-ttu-id="4a543-152">Aşama</span><span class="sxs-lookup"><span data-stu-id="4a543-152">Stage</span></span>              | <span data-ttu-id="4a543-153">Anlamı</span><span class="sxs-lookup"><span data-stu-id="4a543-153">Meaning</span></span>
------------------ | ------
<span data-ttu-id="4a543-154">EarlyAccessPreview</span><span class="sxs-lookup"><span data-stu-id="4a543-154">EarlyAccessPreview</span></span> | <span data-ttu-id="4a543-155">Henüz [indirme web sayfasında](https://www.nuget.org/downloads) görünmez ve iş ortakları tarafından doğrulanması gerekir</span><span class="sxs-lookup"><span data-stu-id="4a543-155">Not yet visible on the [download web page](https://www.nuget.org/downloads) and should be validated by partners</span></span>
<span data-ttu-id="4a543-156">Yayınlandı</span><span class="sxs-lookup"><span data-stu-id="4a543-156">Released</span></span>           | <span data-ttu-id="4a543-157">İndirme sitesinde kullanılabilir ancak geniş yayılmış tüketim için henüz önerilmez</span><span class="sxs-lookup"><span data-stu-id="4a543-157">Available on the download site but is not yet recommended for wide-spread consumption</span></span>
<span data-ttu-id="4a543-158">ReleasedAndBlessed</span><span class="sxs-lookup"><span data-stu-id="4a543-158">ReleasedAndBlessed</span></span> | <span data-ttu-id="4a543-159">İndirme sitesinde kullanılabilir ve tüketim için önerilir</span><span class="sxs-lookup"><span data-stu-id="4a543-159">Available on the download site and is recommended for consumption</span></span>

<span data-ttu-id="4a543-160">En son, önerilen sürüme sahip olmanın bir basit yaklaşımı, bu değeri içeren listedeki ilk sürümü kullanmaktır `stage` `ReleasedAndBlessed` .</span><span class="sxs-lookup"><span data-stu-id="4a543-160">One simple approach for having the latest, recommended version is to take the first version in the list that has the `stage` value of `ReleasedAndBlessed`.</span></span> <span data-ttu-id="4a543-161">Sürümler SemVer 2.0.0 Order içinde sıralandığından bu işe yarar.</span><span class="sxs-lookup"><span data-stu-id="4a543-161">This works because the versions are sorted in SemVer 2.0.0 order.</span></span>

<span data-ttu-id="4a543-162">`NuGet.CommandLine`NuGet.org üzerindeki paket genellikle yalnızca `ReleasedAndBlessed` sürümleriyle güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="4a543-162">The `NuGet.CommandLine` package on nuget.org is typically only updated with `ReleasedAndBlessed` versions.</span></span>

### <a name="sample-request"></a><span data-ttu-id="4a543-163">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="4a543-163">Sample request</span></span>

```
GET https://dist.nuget.org/tools.json
```

### <a name="sample-response"></a><span data-ttu-id="4a543-164">Örnek yanıt</span><span class="sxs-lookup"><span data-stu-id="4a543-164">Sample response</span></span>

[!code-JSON [tools-json.json](./_data/tools-json.json)]
