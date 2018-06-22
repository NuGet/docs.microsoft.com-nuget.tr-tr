---
title: Rapor kötüye URL şablonu, NuGet API
description: Rapor kötüye URL şablonu rapor kötüye bağlantısı kendi kullanıcı Arabiriminde görüntülenecek istemcilerin sağlar.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 15cf0953391489d9dd9b5d609c3f4c8f66748f19
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31818473"
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="767da-103">Rapor kötüye URL şablonu</span><span class="sxs-lookup"><span data-stu-id="767da-103">Report abuse URL template</span></span>

<span data-ttu-id="767da-104">Belirli bir paket hakkında bildirmek için kullanıcı tarafından kullanılabilecek bir URL oluşturmak bir istemci mümkündür.</span><span class="sxs-lookup"><span data-stu-id="767da-104">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="767da-105">Paket kaynağında Uygunsuz kullanım raporları paket kaynağına temsilci seçmek tüm istemci deneyimleri (hatta 3. taraf) etkinleştirmek istediğinde, bu yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="767da-105">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="767da-106">Paket içeriğini getirmek için kullanılan kaynak `ReportAbuseUriTemplate` kaynak bulunan [Hizmeti dizini](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="767da-106">The resource used for fetching package content is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="767da-107">Sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="767da-107">Versioning</span></span>

<span data-ttu-id="767da-108">Aşağıdaki `@type` değerler kullanılır:</span><span class="sxs-lookup"><span data-stu-id="767da-108">The following `@type` values are used:</span></span>

<span data-ttu-id="767da-109">@type Değer</span><span class="sxs-lookup"><span data-stu-id="767da-109">@type value</span></span>                       | <span data-ttu-id="767da-110">Notlar</span><span class="sxs-lookup"><span data-stu-id="767da-110">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="767da-111">ReportAbuseUriTemplate/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="767da-111">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="767da-112">İlk sürüm</span><span class="sxs-lookup"><span data-stu-id="767da-112">The initial release</span></span>
<span data-ttu-id="767da-113">ReportAbuseUriTemplate/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="767da-113">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="767da-114">Diğer adı `ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="767da-114">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="767da-115">URL şablonu</span><span class="sxs-lookup"><span data-stu-id="767da-115">URL template</span></span>

<span data-ttu-id="767da-116">Aşağıdaki API için URL değeri `@id` yukarıda sözü edilen kaynak biri ile ilişkili özelliği `@type` değerleri.</span><span class="sxs-lookup"><span data-stu-id="767da-116">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="767da-117">HTTP yöntemleri</span><span class="sxs-lookup"><span data-stu-id="767da-117">HTTP methods</span></span>

<span data-ttu-id="767da-118">İstemci kullanıcı adına rapor kötüye URL'ye istekte amaçlanmamıştır rağmen web sayfası desteklemelidir `GET` yöntemi bir web tarayıcısında kolayca açılması için tıklatılan URL izin vermek için.</span><span class="sxs-lookup"><span data-stu-id="767da-118">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="767da-119">URL oluşturmak</span><span class="sxs-lookup"><span data-stu-id="767da-119">Construct the URL</span></span>

<span data-ttu-id="767da-120">Verilen bilinen paket kimliği ve sürüm, istemci uygulama bir web arabirimi erişmek için kullanılan bir URL oluşturur.</span><span class="sxs-lookup"><span data-stu-id="767da-120">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="767da-121">İstemci uygulaması, bu oluşturulan URL'si (veya tıklatılabilir bir bağlantı) URL bir web tarayıcısı açın ve tüm gerekli Uygunsuz kullanım raporu yapmak için vermeden kullanıcı görüntülemelidir.</span><span class="sxs-lookup"><span data-stu-id="767da-121">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="767da-122">Uygunsuz kullanım raporu form uyarlamasını sunucu uygulaması tarafından belirlenir.</span><span class="sxs-lookup"><span data-stu-id="767da-122">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="767da-123">Değeri `@id` olan aşağıdaki yer tutucu belirteçleri birini içeren bir URL dizesi:</span><span class="sxs-lookup"><span data-stu-id="767da-123">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="767da-124">URL yer tutucuları</span><span class="sxs-lookup"><span data-stu-id="767da-124">URL placeholders</span></span>

<span data-ttu-id="767da-125">Ad</span><span class="sxs-lookup"><span data-stu-id="767da-125">Name</span></span>        | <span data-ttu-id="767da-126">Tür</span><span class="sxs-lookup"><span data-stu-id="767da-126">Type</span></span>    | <span data-ttu-id="767da-127">Gerekli</span><span class="sxs-lookup"><span data-stu-id="767da-127">Required</span></span> | <span data-ttu-id="767da-128">Notlar</span><span class="sxs-lookup"><span data-stu-id="767da-128">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="767da-129">dize</span><span class="sxs-lookup"><span data-stu-id="767da-129">string</span></span>  | <span data-ttu-id="767da-130">Yok</span><span class="sxs-lookup"><span data-stu-id="767da-130">no</span></span>       | <span data-ttu-id="767da-131">Paket kimliği için bildirmek için</span><span class="sxs-lookup"><span data-stu-id="767da-131">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="767da-132">dize</span><span class="sxs-lookup"><span data-stu-id="767da-132">string</span></span>  | <span data-ttu-id="767da-133">Yok</span><span class="sxs-lookup"><span data-stu-id="767da-133">no</span></span>       | <span data-ttu-id="767da-134">Paket sürümü için bildirmek için</span><span class="sxs-lookup"><span data-stu-id="767da-134">The package version to report abuse for</span></span>

<span data-ttu-id="767da-135">`{id}` Ve `{version}` büyük küçük harfe duyarlı ve sürüm olup olmadığı normalleştirmesini için hassas sunucu uygulaması tarafından yorumlanan değerleri olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="767da-135">The `{id}` and `{version}` values interpreted by the server implementation must be case insensitive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="767da-136">Örneğin, nuget.org rapor kötüye şablonu şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="767da-136">For example, nuget.org's report abuse template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

<span data-ttu-id="767da-137">İstemci uygulaması bir bağlantıyı rapor kötüye formun NuGet.Versioning 4.3.0 görüntülemek gerekirse, aşağıdaki URL'yi oluşturur ve kullanıcıya sağlamak:</span><span class="sxs-lookup"><span data-stu-id="767da-137">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
