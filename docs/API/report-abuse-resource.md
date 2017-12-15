---
title: "Rapor kötüye URL şablonu, NuGet API | Microsoft Docs"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 148d743a-09e5-4539-8454-675be11902db
description: "Rapor kötüye URL şablonu rapor kötüye bağlantısı kendi kullanıcı Arabiriminde görüntülenecek istemcilerin sağlar."
keywords: "NuGet API rapor kötüye, NuGet API dosya uyumlu, NuGet.org rapor URL şablonu"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 7b3413297f5a7fcf0e2c7757036b1f240ed0058a
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="92d1f-104">Rapor kötüye URL şablonu</span><span class="sxs-lookup"><span data-stu-id="92d1f-104">Report Abuse URL Template</span></span>

<span data-ttu-id="92d1f-105">Belirli bir paket hakkında bildirmek için kullanıcı tarafından kullanılabilecek bir URL oluşturmak bir istemci mümkündür.</span><span class="sxs-lookup"><span data-stu-id="92d1f-105">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="92d1f-106">Paket kaynağında Uygunsuz kullanım raporları paket kaynağına temsilci seçmek tüm istemci deneyimleri (hatta 3. taraf) etkinleştirmek istediğinde, bu yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="92d1f-106">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="92d1f-107">Paket içeriğini getirmek için kullanılan kaynak `ReportAbuseUriTemplate` kaynak bulunan [Hizmeti dizini](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="92d1f-107">The resource used for fetching package content is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="92d1f-108">Sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="92d1f-108">Versioning</span></span>

<span data-ttu-id="92d1f-109">Aşağıdaki `@type` değerler kullanılır:</span><span class="sxs-lookup"><span data-stu-id="92d1f-109">The following `@type` values are used:</span></span>

<span data-ttu-id="92d1f-110">@typedeğer</span><span class="sxs-lookup"><span data-stu-id="92d1f-110">@type value</span></span>                       | <span data-ttu-id="92d1f-111">Notlar</span><span class="sxs-lookup"><span data-stu-id="92d1f-111">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="92d1f-112">ReportAbuseUriTemplate/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="92d1f-112">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="92d1f-113">İlk sürüm</span><span class="sxs-lookup"><span data-stu-id="92d1f-113">The initial release</span></span>
<span data-ttu-id="92d1f-114">ReportAbuseUriTemplate/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="92d1f-114">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="92d1f-115">Diğer adı`ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="92d1f-115">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="92d1f-116">URL şablonu</span><span class="sxs-lookup"><span data-stu-id="92d1f-116">URL template</span></span>

<span data-ttu-id="92d1f-117">Aşağıdaki API için URL değeri `@id` yukarıda sözü edilen kaynak biri ile ilişkili özelliği `@type` değerleri.</span><span class="sxs-lookup"><span data-stu-id="92d1f-117">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="92d1f-118">HTTP yöntemleri</span><span class="sxs-lookup"><span data-stu-id="92d1f-118">HTTP methods</span></span>

<span data-ttu-id="92d1f-119">İstemci kullanıcı adına rapor kötüye URL'ye istekte amaçlanmamıştır rağmen web sayfası desteklemelidir `GET` yöntemi bir web tarayıcısında kolayca açılması için tıklatılan URL izin vermek için.</span><span class="sxs-lookup"><span data-stu-id="92d1f-119">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="92d1f-120">URL oluşturmak</span><span class="sxs-lookup"><span data-stu-id="92d1f-120">Construct the URL</span></span>

<span data-ttu-id="92d1f-121">Verilen bilinen paket kimliği ve sürüm, istemci uygulama bir web arabirimi erişmek için kullanılan bir URL oluşturur.</span><span class="sxs-lookup"><span data-stu-id="92d1f-121">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="92d1f-122">İstemci uygulaması, bu oluşturulan URL'si (veya tıklatılabilir bir bağlantı) URL bir web tarayıcısı açın ve tüm gerekli Uygunsuz kullanım raporu yapmak için vermeden kullanıcı görüntülemelidir.</span><span class="sxs-lookup"><span data-stu-id="92d1f-122">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="92d1f-123">Uygunsuz kullanım raporu form uyarlamasını sunucu uygulaması tarafından belirlenir.</span><span class="sxs-lookup"><span data-stu-id="92d1f-123">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="92d1f-124">Değeri `@id` olan aşağıdaki yer tutucu belirteçleri birini içeren bir URL dizesi:</span><span class="sxs-lookup"><span data-stu-id="92d1f-124">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="92d1f-125">URL yer tutucuları</span><span class="sxs-lookup"><span data-stu-id="92d1f-125">URL placeholders</span></span>

<span data-ttu-id="92d1f-126">Ad</span><span class="sxs-lookup"><span data-stu-id="92d1f-126">Name</span></span>        | <span data-ttu-id="92d1f-127">Tür</span><span class="sxs-lookup"><span data-stu-id="92d1f-127">Type</span></span>    | <span data-ttu-id="92d1f-128">Gerekli</span><span class="sxs-lookup"><span data-stu-id="92d1f-128">Required</span></span> | <span data-ttu-id="92d1f-129">Notlar</span><span class="sxs-lookup"><span data-stu-id="92d1f-129">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="92d1f-130">dize</span><span class="sxs-lookup"><span data-stu-id="92d1f-130">string</span></span>  | <span data-ttu-id="92d1f-131">Yok</span><span class="sxs-lookup"><span data-stu-id="92d1f-131">no</span></span>       | <span data-ttu-id="92d1f-132">Paket kimliği için bildirmek için</span><span class="sxs-lookup"><span data-stu-id="92d1f-132">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="92d1f-133">dize</span><span class="sxs-lookup"><span data-stu-id="92d1f-133">string</span></span>  | <span data-ttu-id="92d1f-134">Yok</span><span class="sxs-lookup"><span data-stu-id="92d1f-134">no</span></span>       | <span data-ttu-id="92d1f-135">Paket sürümü için bildirmek için</span><span class="sxs-lookup"><span data-stu-id="92d1f-135">The package version to report abuse for</span></span>

<span data-ttu-id="92d1f-136">`{id}` Ve `{version}` sunucu uygulaması tarafından yorumlanan değerleri büyük/küçük harfe duyarlı olması gerekir ve sürüm olup olmadığı normalleştirmesini için önemli.</span><span class="sxs-lookup"><span data-stu-id="92d1f-136">The `{id}` and `{version}` values interpreted by the server implementation must be case insenstive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="92d1f-137">Örneğin, nuget.org rapor kötüye şablonu şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="92d1f-137">For example, nuget.org's report abuse template looks like this:</span></span>

```
https://www.nuget.org/packages/{id}/{version}/ReportAbuse
```

<span data-ttu-id="92d1f-138">İstemci uygulaması bir bağlantıyı rapor kötüye formun NuGet.Versioning 4.3.0 görüntülemek gerekirse, aşağıdaki URL'yi oluşturur ve kullanıcıya sağlamak:</span><span class="sxs-lookup"><span data-stu-id="92d1f-138">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

```
https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
```