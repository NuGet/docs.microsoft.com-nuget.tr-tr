---
title: Paket ayrıntıları URL şablonu, NuGet API 'SI
description: Paket ayrıntıları URL 'SI şablonu, istemcilerin Kullanıcı arabiriminde daha fazla paket ayrıntılarına görüntülenmesini sağlar
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 3102cb9a20f354e92a0da8bba6457dc2ad0f0f2d
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610952"
---
# <a name="package-details-url-template"></a><span data-ttu-id="07c02-103">Paket ayrıntıları URL şablonu</span><span class="sxs-lookup"><span data-stu-id="07c02-103">Package details URL template</span></span>

<span data-ttu-id="07c02-104">Bir istemcinin, Web tarayıcılarında daha fazla paket ayrıntılarını görmek için Kullanıcı tarafından kullanılabilecek bir URL oluşturması mümkündür.</span><span class="sxs-lookup"><span data-stu-id="07c02-104">It is possible for a client to build a URL that can be used by the user to see more package details in their web browser.</span></span> <span data-ttu-id="07c02-105">Bu, bir paket kaynağı, NuGet istemci uygulamasının gösterdiği işlem kapsamında sığmayan bir paket hakkında ek bilgiler göstermek istediğinde yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="07c02-105">This is useful when a package source wants to show additional information about a package that may not fit within the scope of what the NuGet client application shows.</span></span>

<span data-ttu-id="07c02-106">Bu URL 'YI oluşturmak için kullanılan kaynak, [hizmet dizininde](service-index.md)bulunan `PackageDetailsUriTemplate` kaynağıdır.</span><span class="sxs-lookup"><span data-stu-id="07c02-106">The resource used for building this URL is the `PackageDetailsUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="07c02-107">Sürüm Oluşturma</span><span class="sxs-lookup"><span data-stu-id="07c02-107">Versioning</span></span>

<span data-ttu-id="07c02-108">Aşağıdaki `@type` değerleri kullanılır:</span><span class="sxs-lookup"><span data-stu-id="07c02-108">The following `@type` values are used:</span></span>

<span data-ttu-id="07c02-109">@type değeri</span><span class="sxs-lookup"><span data-stu-id="07c02-109">@type value</span></span>                     | <span data-ttu-id="07c02-110">Notlar</span><span class="sxs-lookup"><span data-stu-id="07c02-110">Notes</span></span>
------------------------------- | -----
<span data-ttu-id="07c02-111">PackageDetailsUriTemplate/5.1.0</span><span class="sxs-lookup"><span data-stu-id="07c02-111">PackageDetailsUriTemplate/5.1.0</span></span> | <span data-ttu-id="07c02-112">İlk yayın</span><span class="sxs-lookup"><span data-stu-id="07c02-112">The initial release</span></span>

## <a name="url-template"></a><span data-ttu-id="07c02-113">URL şablonu</span><span class="sxs-lookup"><span data-stu-id="07c02-113">URL template</span></span>

<span data-ttu-id="07c02-114">Aşağıdaki API 'nin URL 'SI, belirtilen kaynak `@type` değerlerinden biriyle ilişkili `@id` özelliğinin değeridir.</span><span class="sxs-lookup"><span data-stu-id="07c02-114">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="07c02-115">HTTP yöntemleri</span><span class="sxs-lookup"><span data-stu-id="07c02-115">HTTP methods</span></span>

<span data-ttu-id="07c02-116">İstemci, Kullanıcı adına paket ayrıntıları URL 'sine istek yapmaya yönelik değildir, ancak Web sayfası, tıklanan bir URL 'nin bir Web tarayıcısında kolayca açılmasını sağlamak için `GET` yöntemini desteklemelidir.</span><span class="sxs-lookup"><span data-stu-id="07c02-116">Although the client is not intended to make requests to the package details URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="07c02-117">URL 'YI oluşturun</span><span class="sxs-lookup"><span data-stu-id="07c02-117">Construct the URL</span></span>

<span data-ttu-id="07c02-118">Bilinen bir paket KIMLIĞI ve sürümü verildiğinde, istemci uygulama bir Web arabirimine erişmek için kullanılan bir URL oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="07c02-118">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="07c02-119">İstemci uygulamasının bu oluşturulmuş URL 'yi (veya tıklatılabilir bağlantıyı) kullanıcıya URL 'ye bir Web tarayıcısı açmasına ve paket hakkında daha fazla bilgi edinmesine izin verecek şekilde görüntülemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="07c02-119">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and to learn more about the package.</span></span> <span data-ttu-id="07c02-120">Paket ayrıntıları sayfasının içeriği sunucu uygulamasına göre belirlenir.</span><span class="sxs-lookup"><span data-stu-id="07c02-120">The contents of the package details page is determined by the server implementation.</span></span>

<span data-ttu-id="07c02-121">URL 'nin mutlak bir URL olması ve düzenin (protokol) HTTPS olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="07c02-121">The URL must be an absolute URL and the scheme (protocol) must be HTTPS.</span></span>

<span data-ttu-id="07c02-122">Hizmet dizinindeki `@id` değeri, aşağıdaki yer tutucu belirteçlerinden herhangi birini içeren bir URL dizesidir:</span><span class="sxs-lookup"><span data-stu-id="07c02-122">The value of the `@id` in the service index is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="07c02-123">URL yer tutucuları</span><span class="sxs-lookup"><span data-stu-id="07c02-123">URL placeholders</span></span>

<span data-ttu-id="07c02-124">Name</span><span class="sxs-lookup"><span data-stu-id="07c02-124">Name</span></span>        | <span data-ttu-id="07c02-125">Tür</span><span class="sxs-lookup"><span data-stu-id="07c02-125">Type</span></span>    | <span data-ttu-id="07c02-126">Gerekli</span><span class="sxs-lookup"><span data-stu-id="07c02-126">Required</span></span> | <span data-ttu-id="07c02-127">Notlar</span><span class="sxs-lookup"><span data-stu-id="07c02-127">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="07c02-128">dize</span><span class="sxs-lookup"><span data-stu-id="07c02-128">string</span></span>  | <span data-ttu-id="07c02-129">eşleşen</span><span class="sxs-lookup"><span data-stu-id="07c02-129">no</span></span>       | <span data-ttu-id="07c02-130">Ayrıntıları almak için paket KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="07c02-130">The package ID to get details for</span></span>
`{version}` | <span data-ttu-id="07c02-131">dize</span><span class="sxs-lookup"><span data-stu-id="07c02-131">string</span></span>  | <span data-ttu-id="07c02-132">eşleşen</span><span class="sxs-lookup"><span data-stu-id="07c02-132">no</span></span>       | <span data-ttu-id="07c02-133">Ayrıntıları alınacak paket sürümü</span><span class="sxs-lookup"><span data-stu-id="07c02-133">The package version to get details for</span></span>

<span data-ttu-id="07c02-134">Sunucu, herhangi bir büyük küçük harf ile `{id}` ve `{version}` değerlerini kabul etmelidir.</span><span class="sxs-lookup"><span data-stu-id="07c02-134">The server should accept `{id}` and `{version}` values with any casing.</span></span> <span data-ttu-id="07c02-135">Buna ek olarak, sunucu, sürümünün [normalleştirilme](https://docs.microsoft.com/nuget/concepts/package-versioning#normalized-version-numbers)olup olmadığına duyarlı olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="07c02-135">In addition, the server should not be sensitive to whether the version is [normalized](https://docs.microsoft.com/nuget/concepts/package-versioning#normalized-version-numbers).</span></span> <span data-ttu-id="07c02-136">Diğer bir deyişle, sunucu kabul edilmelidir, ayrıca Normalleştirilmemiş sürümleri kabul etmelidir.</span><span class="sxs-lookup"><span data-stu-id="07c02-136">In other words, the server should accept also accept non-normalized versions.</span></span>

<span data-ttu-id="07c02-137">Örneğin, NuGet. org 'ın paket ayrıntıları şablonu şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="07c02-137">For example, nuget.org's package details template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}

<span data-ttu-id="07c02-138">İstemci uygulamasının NuGet. sürümlendirme 4.3.0 için paket ayrıntılarına bir bağlantı görüntülemesi gerekiyorsa, aşağıdaki URL 'YI oluşturur ve kullanıcıya sağlar:</span><span class="sxs-lookup"><span data-stu-id="07c02-138">If the client implementation needs to display a link to the package details for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
