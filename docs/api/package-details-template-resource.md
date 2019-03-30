---
title: Paket Ayrıntıları URL şablonu, NuGet API'si
description: Paket Ayrıntıları URL şablonu, bunların kullanıcı arabiriminde bir web bağlantısı için daha fazla paket ayrıntılarını görüntülemek istemcilerin
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: c01fd35c5d96c44279c9d0254f89d8b1b9fe59d8
ms.sourcegitcommit: 2af17c8bb452a538977794bf559cdd78d58f2790
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/29/2019
ms.locfileid: "58638089"
---
# <a name="package-details-url-template"></a><span data-ttu-id="86b95-103">Paket Ayrıntıları URL şablonu</span><span class="sxs-lookup"><span data-stu-id="86b95-103">Package details URL template</span></span>

<span data-ttu-id="86b95-104">Web tarayıcısında daha fazla paket ayrıntılarını görmek için kullanıcı tarafından kullanılan bir URL oluşturmak bir istemci mümkündür.</span><span class="sxs-lookup"><span data-stu-id="86b95-104">It is possible for a client to build a URL that can be used by the user to see more package details in their web browser.</span></span> <span data-ttu-id="86b95-105">Paket kaynağı olmayan bir çözüm paketi hakkında ek bilgi ne NuGet istemci uygulaması gösterir, kapsam içinde gösterilecek istediğinde, bu yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="86b95-105">This is useful when a package source wants to show additional information about a package that may not fit within the scope of what the NuGet client application shows.</span></span>

<span data-ttu-id="86b95-106">Bu URL'yi oluşturmak için kullanılan kaynak `PackageDetailsUriTemplate` kaynak bulunan [hizmet dizini](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="86b95-106">The resource used for building this URL is the `PackageDetailsUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="86b95-107">Sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="86b95-107">Versioning</span></span>

<span data-ttu-id="86b95-108">Aşağıdaki `@type` değerleri kullanılır:</span><span class="sxs-lookup"><span data-stu-id="86b95-108">The following `@type` values are used:</span></span>

<span data-ttu-id="86b95-109">@type Değer</span><span class="sxs-lookup"><span data-stu-id="86b95-109">@type value</span></span>                     | <span data-ttu-id="86b95-110">Notlar</span><span class="sxs-lookup"><span data-stu-id="86b95-110">Notes</span></span>
------------------------------- | -----
<span data-ttu-id="86b95-111">PackageDetailsUriTemplate/5.1.0</span><span class="sxs-lookup"><span data-stu-id="86b95-111">PackageDetailsUriTemplate/5.1.0</span></span> | <span data-ttu-id="86b95-112">İlk yayın</span><span class="sxs-lookup"><span data-stu-id="86b95-112">The initial release</span></span>

## <a name="url-template"></a><span data-ttu-id="86b95-113">URL şablonu</span><span class="sxs-lookup"><span data-stu-id="86b95-113">URL template</span></span>

<span data-ttu-id="86b95-114">Aşağıdaki API URL'si değeri `@id` yukarıda sözü edilen kaynak biriyle ilişkili özelliği `@type` değerleri.</span><span class="sxs-lookup"><span data-stu-id="86b95-114">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="86b95-115">HTTP yöntemleri</span><span class="sxs-lookup"><span data-stu-id="86b95-115">HTTP methods</span></span>

<span data-ttu-id="86b95-116">İstemci isteğinde Paket Ayrıntıları URL'sini kullanıcı adına yönelik değildir ancak web sayfası desteklemelidir `GET` bir web tarayıcısından kolayca açılması tıklanan URL izin vermek için yöntemi.</span><span class="sxs-lookup"><span data-stu-id="86b95-116">Although the client is not intended to make requests to the package details URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="86b95-117">URL'sini oluşturun</span><span class="sxs-lookup"><span data-stu-id="86b95-117">Construct the URL</span></span>

<span data-ttu-id="86b95-118">Verilen bir bilinen paket kimliği ve sürüm, istemci uygulama bir web arabirimine erişmek için kullanılan bir URL oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="86b95-118">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="86b95-119">İstemci uygulama, bunları izin vererek kullanıcıya URL'sine bir web tarayıcısı açın ve paket hakkında daha fazla bilgi için bu oluşturulmuş URL (veya tıklatılabilir bir bağlantı) görüntülemelidir.</span><span class="sxs-lookup"><span data-stu-id="86b95-119">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and to learn more about the package.</span></span> <span data-ttu-id="86b95-120">Paket Ayrıntıları sayfasına içeriğini sunucu uygulaması tarafından belirlenir.</span><span class="sxs-lookup"><span data-stu-id="86b95-120">The contents of the package details page is determined by the server implementation.</span></span>

<span data-ttu-id="86b95-121">URL, mutlak bir URL olmalıdır ve (Protokolü) şeması HTTPS olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="86b95-121">The URL must be an absolute URL and the scheme (protocol) must be HTTPS.</span></span>

<span data-ttu-id="86b95-122">Değerini `@id` hizmetinde aşağıdaki yer tutucu belirteçler birini içeren bir URL dizesi dizinidir:</span><span class="sxs-lookup"><span data-stu-id="86b95-122">The value of the `@id` in the service index is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="86b95-123">URL yer tutucuları</span><span class="sxs-lookup"><span data-stu-id="86b95-123">URL placeholders</span></span>

<span data-ttu-id="86b95-124">Ad</span><span class="sxs-lookup"><span data-stu-id="86b95-124">Name</span></span>        | <span data-ttu-id="86b95-125">Tür</span><span class="sxs-lookup"><span data-stu-id="86b95-125">Type</span></span>    | <span data-ttu-id="86b95-126">Gerekli</span><span class="sxs-lookup"><span data-stu-id="86b95-126">Required</span></span> | <span data-ttu-id="86b95-127">Notlar</span><span class="sxs-lookup"><span data-stu-id="86b95-127">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="86b95-128">dize</span><span class="sxs-lookup"><span data-stu-id="86b95-128">string</span></span>  | <span data-ttu-id="86b95-129">Yok</span><span class="sxs-lookup"><span data-stu-id="86b95-129">no</span></span>       | <span data-ttu-id="86b95-130">Bilgi almak için paket kimliği</span><span class="sxs-lookup"><span data-stu-id="86b95-130">The package ID to get details for</span></span>
`{version}` | <span data-ttu-id="86b95-131">dize</span><span class="sxs-lookup"><span data-stu-id="86b95-131">string</span></span>  | <span data-ttu-id="86b95-132">Yok</span><span class="sxs-lookup"><span data-stu-id="86b95-132">no</span></span>       | <span data-ttu-id="86b95-133">Bilgi almak için Paket sürümü</span><span class="sxs-lookup"><span data-stu-id="86b95-133">The package version to get details for</span></span>

<span data-ttu-id="86b95-134">Sunucu kabul etmelidir `{id}` ve `{version}` tüm büyük/küçük harf değerleri.</span><span class="sxs-lookup"><span data-stu-id="86b95-134">The server should accept `{id}` and `{version}` values with any casing.</span></span> <span data-ttu-id="86b95-135">Ayrıca, sunucu sürümü olup duyarlı olmamalıdır [normalleştirilmiş](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#normalized-version-numbers).</span><span class="sxs-lookup"><span data-stu-id="86b95-135">In addition, the server should not be sensitive to whether the version is [normalized](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#normalized-version-numbers).</span></span> <span data-ttu-id="86b95-136">Diğer bir deyişle, sunucunun kabul etmelidir normale olmayan sürümleri de kabul.</span><span class="sxs-lookup"><span data-stu-id="86b95-136">In other words, the server should accept also accept non-normalized versions.</span></span>

<span data-ttu-id="86b95-137">Örneğin, nuget.org Paket Ayrıntıları şablon şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="86b95-137">For example, nuget.org's package details template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}

<span data-ttu-id="86b95-138">İstemci uygulama bir bağlantı için NuGet.Versioning 4.3.0 için Paket ayrıntılarını görüntülemek gerekiyorsa, aşağıdaki URL'yi oluşturur ve kullanıcıya sağlamak:</span><span class="sxs-lookup"><span data-stu-id="86b95-138">If the client implementation needs to display a link to the package details for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
