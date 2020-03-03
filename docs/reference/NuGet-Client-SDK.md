---
title: NuGet Istemci SDK 'Sı
description: API gelişiyor ve henüz belgelenmemiştir, ancak örnek, bave Glick 'in blogundan bulunabilir.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: a5c542379318f24ee35ccf25651d0e8de91253ba
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231246"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="0b032-103">NuGet Istemci SDK 'Sı</span><span class="sxs-lookup"><span data-stu-id="0b032-103">NuGet Client SDK</span></span>

<span data-ttu-id="0b032-104">*NuGet istemci SDK 'sı* bir NuGet paketleri grubunu ifade eder:</span><span class="sxs-lookup"><span data-stu-id="0b032-104">The *NuGet Client SDK* refers to a group of NuGet packages:</span></span>

* <span data-ttu-id="0b032-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) -http ve dosya tabanlı NuGet akışlarıyla etkileşim kurmak için kullanılır</span><span class="sxs-lookup"><span data-stu-id="0b032-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Used to interact with HTTP and file-based NuGet feeds</span></span>
* <span data-ttu-id="0b032-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) -NuGet paketleriyle etkileşim kurmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0b032-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Used to interact with NuGet packages.</span></span> <span data-ttu-id="0b032-107">`NuGet.Protocol` bu pakete bağlıdır</span><span class="sxs-lookup"><span data-stu-id="0b032-107">`NuGet.Protocol` depends on this package</span></span>

<span data-ttu-id="0b032-108">Bu paketlerin kaynak kodunu [NuGet/NuGet. Client](https://github.com/NuGet/NuGet.Client) GitHub deposunda bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0b032-108">You can find the source code for these packages in the [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) GitHub repository.</span></span>

> [!Note]
> <span data-ttu-id="0b032-109">NuGet sunucu protokolü hakkındaki belgeler için lütfen [NuGet sunucu API](~/api/overview.md)'sine bakın.</span><span class="sxs-lookup"><span data-stu-id="0b032-109">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="getting-started"></a><span data-ttu-id="0b032-110">Başlarken</span><span class="sxs-lookup"><span data-stu-id="0b032-110">Getting started</span></span>

### <a name="install-the-package"></a><span data-ttu-id="0b032-111">Paketi yükler</span><span class="sxs-lookup"><span data-stu-id="0b032-111">Install the package</span></span>

```ps1
dotnet add package NuGet.Protocol
```

## <a name="examples"></a><span data-ttu-id="0b032-112">Örnekler</span><span class="sxs-lookup"><span data-stu-id="0b032-112">Examples</span></span>

<span data-ttu-id="0b032-113">Bu örnekleri GitHub 'da [NuGet. Protocol. Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) projesinde bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0b032-113">You can find these examples on the [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) project on GitHub.</span></span>

### <a name="list-package-versions"></a><span data-ttu-id="0b032-114">Paket sürümlerini Listele</span><span class="sxs-lookup"><span data-stu-id="0b032-114">List package versions</span></span>

<span data-ttu-id="0b032-115">[NuGet V3 paketi IÇERIK API](../api/package-base-address-resource.md#enumerate-package-versions)'Sini kullanarak Newtonsoft. json ' nin tüm sürümlerini bulun:</span><span class="sxs-lookup"><span data-stu-id="0b032-115">Find all versions of Newtonsoft.Json using the [NuGet V3 Package Content API](../api/package-base-address-resource.md#enumerate-package-versions):</span></span>

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a><span data-ttu-id="0b032-116">Paket indir</span><span class="sxs-lookup"><span data-stu-id="0b032-116">Download a package</span></span>

<span data-ttu-id="0b032-117">[NuGet V3 paketi IÇERIK API](../api/package-base-address-resource.md)'Sini kullanarak Newtonsoft. JSON v 12.0.1 ' ni indirin:</span><span class="sxs-lookup"><span data-stu-id="0b032-117">Download Newtonsoft.Json v12.0.1 using the [NuGet V3 Package Content API](../api/package-base-address-resource.md):</span></span>

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a><span data-ttu-id="0b032-118">Paket meta verilerini al</span><span class="sxs-lookup"><span data-stu-id="0b032-118">Get package metadata</span></span>

<span data-ttu-id="0b032-119">[NuGet V3 paketi meta veri API 'sini](../api/registration-base-url-resource.md)kullanarak "Newtonsoft. JSON" paketine ait meta verileri alın:</span><span class="sxs-lookup"><span data-stu-id="0b032-119">Get the metadata for the "Newtonsoft.Json" package using the [NuGet V3 Package Metadata API](../api/registration-base-url-resource.md):</span></span>

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a><span data-ttu-id="0b032-120">Paketleri ara</span><span class="sxs-lookup"><span data-stu-id="0b032-120">Search packages</span></span>

<span data-ttu-id="0b032-121">[NuGet v3 arama API](../api/search-query-service-resource.md)'sini kullanarak "JSON" paketleri arayın:</span><span class="sxs-lookup"><span data-stu-id="0b032-121">Search for "json" packages using the [NuGet V3 Search API](../api/search-query-service-resource.md):</span></span>

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

## <a name="third-party-documentation"></a><span data-ttu-id="0b032-122">Üçüncü taraf belgeleri</span><span class="sxs-lookup"><span data-stu-id="0b032-122">Third-party documentation</span></span>

<span data-ttu-id="0b032-123">Aşağıdaki blog serisindeki bazı API 'ler için örnekler ve belgeler için Glick, yayımlanan 2016:</span><span class="sxs-lookup"><span data-stu-id="0b032-123">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="0b032-124">NuGet v3 kitaplıklarını keşfetme, 1. Bölüm: giriş ve kavramlar</span><span class="sxs-lookup"><span data-stu-id="0b032-124">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="0b032-125">NuGet v3 kitaplıklarını keşfetme, Bölüm 2: paketleri arama</span><span class="sxs-lookup"><span data-stu-id="0b032-125">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="0b032-126">NuGet v3 kitaplıklarını keşfetme, 3. Bölüm: paketleri yükleme</span><span class="sxs-lookup"><span data-stu-id="0b032-126">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="0b032-127">Bu blog gönderileri, NuGet istemci SDK paketlerinin **3.4.3** sürümü yayımlandıktan kısa bir süre sonra yazıldı.</span><span class="sxs-lookup"><span data-stu-id="0b032-127">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="0b032-128">Paketlerin daha yeni sürümleri, blog gönderilerinin bilgileriyle uyumsuz olabilir.</span><span class="sxs-lookup"><span data-stu-id="0b032-128">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="0b032-129">Marve Glick 'in blog serisine, NuGet paketlerini yüklemek için NuGet Istemci SDK 'sını kullanma konusunda farklı bir yaklaşım tanıtan bir izleme blog gönderisi Björkström.</span><span class="sxs-lookup"><span data-stu-id="0b032-129">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK to install NuGet packages:</span></span>

- [<span data-ttu-id="0b032-130">NuGet v3 kitaplıklarını yeniden ziyaret etme</span><span class="sxs-lookup"><span data-stu-id="0b032-130">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
