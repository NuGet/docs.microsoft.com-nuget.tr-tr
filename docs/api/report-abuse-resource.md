---
title: Uygunsuz kullanım URL şablonunu bildir, NuGet API
description: Uygunsuz kullanım URL 'SI şablonu, istemcilerin Kullanıcı arabiriminde kötü bir rapor uygunsuz bağlantı görüntülemesini sağlar.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: b36058c9c841e2cca6eb61121ada8275f1525a8f
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775226"
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="e9ae0-103">Uygunsuz kullanım URL şablonunu raporla</span><span class="sxs-lookup"><span data-stu-id="e9ae0-103">Report abuse URL template</span></span>

<span data-ttu-id="e9ae0-104">Bir istemcinin belirli bir paket hakkında uygunsuz kullanımı raporlamak için Kullanıcı tarafından kullanılabilecek bir URL oluşturması mümkündür.</span><span class="sxs-lookup"><span data-stu-id="e9ae0-104">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="e9ae0-105">Bu, bir paket kaynağı tüm istemci deneyimlerini (hatta 3. taraf), çok kişili raporların paket kaynağına atamasını sağlamak istediğinde yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="e9ae0-105">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="e9ae0-106">Bu URL 'YI oluşturmak için kullanılan kaynak, `ReportAbuseUriTemplate` [hizmet dizininde](service-index.md)bulunan kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="e9ae0-106">The resource used for building this URL is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="e9ae0-107">Sürüm Oluşturma</span><span class="sxs-lookup"><span data-stu-id="e9ae0-107">Versioning</span></span>

<span data-ttu-id="e9ae0-108">Aşağıdaki `@type` değerler kullanılır:</span><span class="sxs-lookup"><span data-stu-id="e9ae0-108">The following `@type` values are used:</span></span>

<span data-ttu-id="e9ae0-109">@type deeri</span><span class="sxs-lookup"><span data-stu-id="e9ae0-109">@type value</span></span>                       | <span data-ttu-id="e9ae0-110">Notlar</span><span class="sxs-lookup"><span data-stu-id="e9ae0-110">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="e9ae0-111">ReportAbuseUriTemplate/3.0.0-Beta</span><span class="sxs-lookup"><span data-stu-id="e9ae0-111">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="e9ae0-112">İlk yayın</span><span class="sxs-lookup"><span data-stu-id="e9ae0-112">The initial release</span></span>
<span data-ttu-id="e9ae0-113">ReportAbuseUriTemplate/3.0.0-RC</span><span class="sxs-lookup"><span data-stu-id="e9ae0-113">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="e9ae0-114">Diğer adı `ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="e9ae0-114">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="e9ae0-115">URL şablonu</span><span class="sxs-lookup"><span data-stu-id="e9ae0-115">URL template</span></span>

<span data-ttu-id="e9ae0-116">Aşağıdaki API 'nin URL 'SI, `@id` belirtilen kaynak değerlerinden biriyle ilişkili özelliğin değeridir `@type` .</span><span class="sxs-lookup"><span data-stu-id="e9ae0-116">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="e9ae0-117">HTTP yöntemleri</span><span class="sxs-lookup"><span data-stu-id="e9ae0-117">HTTP methods</span></span>

<span data-ttu-id="e9ae0-118">İstemci kullanıcı adına uygunsuz kullanım URL 'sine istek yapmaya yönelik değildir, ancak Web sayfası, `GET` tıklanan BIR URL 'nin bir Web tarayıcısında kolayca açılmasını sağlamak için yöntemini desteklemelidir.</span><span class="sxs-lookup"><span data-stu-id="e9ae0-118">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="e9ae0-119">URL 'YI oluşturun</span><span class="sxs-lookup"><span data-stu-id="e9ae0-119">Construct the URL</span></span>

<span data-ttu-id="e9ae0-120">Bilinen bir paket KIMLIĞI ve sürümü verildiğinde, istemci uygulama bir Web arabirimine erişmek için kullanılan bir URL oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="e9ae0-120">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="e9ae0-121">İstemci uygulamasının bu oluşturulmuş URL 'yi (veya tıklatılabilir bağlantıyı) kullanıcıya URL 'ye bir Web tarayıcısı açmasına ve gerekli uygunsuz kullanım raporu yapmasına izin vererek görüntülemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="e9ae0-121">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="e9ae0-122">Uygunsuz kullanım raporu formunun uygulanması sunucu uygulamasına göre belirlenir.</span><span class="sxs-lookup"><span data-stu-id="e9ae0-122">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="e9ae0-123">Öğesinin değeri, `@id` aşağıdaki yer tutucu belirteçlerinden herhangi birini içeren BIR URL dizesidir:</span><span class="sxs-lookup"><span data-stu-id="e9ae0-123">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="e9ae0-124">URL yer tutucuları</span><span class="sxs-lookup"><span data-stu-id="e9ae0-124">URL placeholders</span></span>

<span data-ttu-id="e9ae0-125">Ad</span><span class="sxs-lookup"><span data-stu-id="e9ae0-125">Name</span></span>        | <span data-ttu-id="e9ae0-126">Tür</span><span class="sxs-lookup"><span data-stu-id="e9ae0-126">Type</span></span>    | <span data-ttu-id="e9ae0-127">Gerekli</span><span class="sxs-lookup"><span data-stu-id="e9ae0-127">Required</span></span> | <span data-ttu-id="e9ae0-128">Notlar</span><span class="sxs-lookup"><span data-stu-id="e9ae0-128">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="e9ae0-129">string</span><span class="sxs-lookup"><span data-stu-id="e9ae0-129">string</span></span>  | <span data-ttu-id="e9ae0-130">hayır</span><span class="sxs-lookup"><span data-stu-id="e9ae0-130">no</span></span>       | <span data-ttu-id="e9ae0-131">Kötüye kullanımı raporlamak için paket KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="e9ae0-131">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="e9ae0-132">string</span><span class="sxs-lookup"><span data-stu-id="e9ae0-132">string</span></span>  | <span data-ttu-id="e9ae0-133">hayır</span><span class="sxs-lookup"><span data-stu-id="e9ae0-133">no</span></span>       | <span data-ttu-id="e9ae0-134">Kötüye kullanımı raporlamak için paket sürümü</span><span class="sxs-lookup"><span data-stu-id="e9ae0-134">The package version to report abuse for</span></span>

<span data-ttu-id="e9ae0-135">`{id}` `{version}` Sunucu uygulamasının yorumlandığı ve değerleri, büyük/küçük harfe duyarsız olmalıdır ve sürüm normalleştirilip normalleştirilmemelidir.</span><span class="sxs-lookup"><span data-stu-id="e9ae0-135">The `{id}` and `{version}` values interpreted by the server implementation must be case insensitive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="e9ae0-136">Örneğin, NuGet. org 'ın uygunsuz kullanımı şablonu şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="e9ae0-136">For example, nuget.org's report abuse template looks like this:</span></span>

```
https://www.nuget.org/packages/{id}/{version}/ReportAbuse
```

<span data-ttu-id="e9ae0-137">İstemci uygulamasının NuGet. sürümlendirme için uygunsuz kullanım formunun bir bağlantısını görüntülemesi gerekiyorsa, aşağıdaki URL 'YI oluşturur ve kullanıcıya sağlar:</span><span class="sxs-lookup"><span data-stu-id="e9ae0-137">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

```
https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
```
