---
title: Rapor kötüye URL şablonu, NuGet API'si
description: Rapor kötüye URL şablonu, bunların kullanıcı Arabiriminde bir rapor kötüye bağlantı görüntüler etmesine olanak tanır.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: b1fd65b12590a6c5eeb23d946eec6ca4a1c661bc
ms.sourcegitcommit: e9c58dbfc1af2876337dcc37b1b070e8ddec0388
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/09/2018
ms.locfileid: "40020446"
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="d78d8-103">Rapor kötüye URL şablonu</span><span class="sxs-lookup"><span data-stu-id="d78d8-103">Report abuse URL template</span></span>

<span data-ttu-id="d78d8-104">Uygunsuz kullanımı hakkında belirli bir paket için bir kullanıcı tarafından kullanılabilecek bir URL oluşturmak bir istemci mümkündür.</span><span class="sxs-lookup"><span data-stu-id="d78d8-104">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="d78d8-105">Uygunsuz kullanım raporları paket kaynağına temsilci seçmek tüm istemci deneyimleri (hatta 3. taraf) etkinleştirmek bir paket kaynağı istediğinde, bu yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="d78d8-105">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="d78d8-106">Bu URL'yi oluşturmak için kullanılan kaynak `ReportAbuseUriTemplate` kaynak bulunan [hizmet dizini](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="d78d8-106">The resource used for building this URL is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="d78d8-107">Sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="d78d8-107">Versioning</span></span>

<span data-ttu-id="d78d8-108">Aşağıdaki `@type` değerleri kullanılır:</span><span class="sxs-lookup"><span data-stu-id="d78d8-108">The following `@type` values are used:</span></span>

<span data-ttu-id="d78d8-109">@type Değer</span><span class="sxs-lookup"><span data-stu-id="d78d8-109">@type value</span></span>                       | <span data-ttu-id="d78d8-110">Notlar</span><span class="sxs-lookup"><span data-stu-id="d78d8-110">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="d78d8-111">ReportAbuseUriTemplate/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="d78d8-111">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="d78d8-112">İlk yayın</span><span class="sxs-lookup"><span data-stu-id="d78d8-112">The initial release</span></span>
<span data-ttu-id="d78d8-113">ReportAbuseUriTemplate/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="d78d8-113">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="d78d8-114">Diğer adı `ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="d78d8-114">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="d78d8-115">URL şablonu</span><span class="sxs-lookup"><span data-stu-id="d78d8-115">URL template</span></span>

<span data-ttu-id="d78d8-116">Aşağıdaki API URL'si değeri `@id` yukarıda sözü edilen kaynak biriyle ilişkili özelliği `@type` değerleri.</span><span class="sxs-lookup"><span data-stu-id="d78d8-116">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="d78d8-117">HTTP yöntemleri</span><span class="sxs-lookup"><span data-stu-id="d78d8-117">HTTP methods</span></span>

<span data-ttu-id="d78d8-118">İstemci istekleri için rapor Uygunsuz kullanım bildirme URL'si kullanıcı adına yapmak için tasarlanmamıştır olsa da, web sayfası desteklemelidir `GET` bir web tarayıcısından kolayca açılması tıklanan URL izin vermek için yöntemi.</span><span class="sxs-lookup"><span data-stu-id="d78d8-118">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="d78d8-119">URL'sini oluşturun</span><span class="sxs-lookup"><span data-stu-id="d78d8-119">Construct the URL</span></span>

<span data-ttu-id="d78d8-120">Verilen bir bilinen paket kimliği ve sürüm, istemci uygulama bir web arabirimine erişmek için kullanılan bir URL oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d78d8-120">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="d78d8-121">İstemci uygulaması, bu oluşturulan URL (veya tıklatılabilir bir bağlantı) URL'sine bir web tarayıcısı açın ve tüm gerekli kötüye rapor yapmak için bunları izin vererek kullanıcıya görüntülemelidir.</span><span class="sxs-lookup"><span data-stu-id="d78d8-121">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="d78d8-122">Uygunsuz kullanım raporu form uygulaması sunucu uygulaması tarafından belirlenir.</span><span class="sxs-lookup"><span data-stu-id="d78d8-122">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="d78d8-123">Değerini `@id` herhangi bir aşağıdaki yer tutucu belirteçler içeren bir URL dize:</span><span class="sxs-lookup"><span data-stu-id="d78d8-123">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="d78d8-124">URL yer tutucuları</span><span class="sxs-lookup"><span data-stu-id="d78d8-124">URL placeholders</span></span>

<span data-ttu-id="d78d8-125">Ad</span><span class="sxs-lookup"><span data-stu-id="d78d8-125">Name</span></span>        | <span data-ttu-id="d78d8-126">Tür</span><span class="sxs-lookup"><span data-stu-id="d78d8-126">Type</span></span>    | <span data-ttu-id="d78d8-127">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d78d8-127">Required</span></span> | <span data-ttu-id="d78d8-128">Notlar</span><span class="sxs-lookup"><span data-stu-id="d78d8-128">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="d78d8-129">dize</span><span class="sxs-lookup"><span data-stu-id="d78d8-129">string</span></span>  | <span data-ttu-id="d78d8-130">Yok</span><span class="sxs-lookup"><span data-stu-id="d78d8-130">no</span></span>       | <span data-ttu-id="d78d8-131">Uygunsuz kullanımı için paket kimliği</span><span class="sxs-lookup"><span data-stu-id="d78d8-131">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="d78d8-132">dize</span><span class="sxs-lookup"><span data-stu-id="d78d8-132">string</span></span>  | <span data-ttu-id="d78d8-133">Yok</span><span class="sxs-lookup"><span data-stu-id="d78d8-133">no</span></span>       | <span data-ttu-id="d78d8-134">Uygunsuz kullanımı için için Paket sürümü</span><span class="sxs-lookup"><span data-stu-id="d78d8-134">The package version to report abuse for</span></span>

<span data-ttu-id="d78d8-135">`{id}` Ve `{version}` sunucu uygulaması tarafından yorumlanan değerler büyük küçük harfe duyarlı ve duyarlı olup sürüm normalleştirilmiştir için olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d78d8-135">The `{id}` and `{version}` values interpreted by the server implementation must be case insensitive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="d78d8-136">Örneğin, nuget.org rapor kötüye şablonu şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="d78d8-136">For example, nuget.org's report abuse template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

<span data-ttu-id="d78d8-137">İstemci uygulaması 4.3.0 NuGet.Versioning için rapor kötüye formuna bir bağlantı görüntülenecek gerekiyorsa aşağıdaki URL'yi oluşturur ve kullanıcıya sağlamak:</span><span class="sxs-lookup"><span data-stu-id="d78d8-137">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
