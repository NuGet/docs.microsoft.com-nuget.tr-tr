---
title: NuGet İstemci SDK’sı
description: API gelişiyor ve henüz belgelenmemiştir, ancak örnek, bave Glick 'in blogundan bulunabilir.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 39a4de4071eec70c88a2add158f2a3a734f7d7b7
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622934"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="85993-103">NuGet İstemci SDK’sı</span><span class="sxs-lookup"><span data-stu-id="85993-103">NuGet Client SDK</span></span>

<span data-ttu-id="85993-104">*NuGet istemci SDK 'sı* bir NuGet paketleri grubunu ifade eder:</span><span class="sxs-lookup"><span data-stu-id="85993-104">The *NuGet Client SDK* refers to a group of NuGet packages:</span></span>

* <span data-ttu-id="85993-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) -HTTP ve dosya tabanlı NuGet akışlarıyla etkileşim kurmak için kullanılır</span><span class="sxs-lookup"><span data-stu-id="85993-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Used to interact with HTTP and file-based NuGet feeds</span></span>
* <span data-ttu-id="85993-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) -NuGet paketleri ile etkileşim kurmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="85993-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Used to interact with NuGet packages.</span></span> <span data-ttu-id="85993-107">`NuGet.Protocol` Bu pakete bağımlıdır</span><span class="sxs-lookup"><span data-stu-id="85993-107">`NuGet.Protocol` depends on this package</span></span>

<span data-ttu-id="85993-108">Bu paketlerin kaynak kodunu [NuGet/NuGet. Client](https://github.com/NuGet/NuGet.Client) GitHub deposunda bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85993-108">You can find the source code for these packages in the [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) GitHub repository.</span></span>

> [!Note]
> <span data-ttu-id="85993-109">NuGet sunucu protokolü hakkındaki belgeler için lütfen [NuGet sunucu API](~/api/overview.md)'sine bakın.</span><span class="sxs-lookup"><span data-stu-id="85993-109">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="getting-started"></a><span data-ttu-id="85993-110">Başlarken</span><span class="sxs-lookup"><span data-stu-id="85993-110">Getting started</span></span>

### <a name="install-the-packages"></a><span data-ttu-id="85993-111">Paketleri yükler</span><span class="sxs-lookup"><span data-stu-id="85993-111">Install the packages</span></span>

```ps1
dotnet add package NuGet.Protocol  # interact with HTTP and folder-based NuGet package feeds, includes NuGet.Packaging

dotnet add package NuGet.Packaging # interact with .nupkg and .nuspec files from a stream
```

## <a name="examples"></a><span data-ttu-id="85993-112">Örnekler</span><span class="sxs-lookup"><span data-stu-id="85993-112">Examples</span></span>

<span data-ttu-id="85993-113">Bu örnekleri GitHub 'da [NuGet. Protocol. Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) projesinde bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85993-113">You can find these examples on the [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) project on GitHub.</span></span>

### <a name="list-package-versions"></a><span data-ttu-id="85993-114">Paket sürümlerini Listele</span><span class="sxs-lookup"><span data-stu-id="85993-114">List package versions</span></span>

<span data-ttu-id="85993-115">[NuGet V3 paketi IÇERIK API](../api/package-base-address-resource.md#enumerate-package-versions)'sini kullanarak tüm Newtonsoft.Jssürümlerini bulun:</span><span class="sxs-lookup"><span data-stu-id="85993-115">Find all versions of Newtonsoft.Json using the [NuGet V3 Package Content API](../api/package-base-address-resource.md#enumerate-package-versions):</span></span>

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a><span data-ttu-id="85993-116">Paket indir</span><span class="sxs-lookup"><span data-stu-id="85993-116">Download a package</span></span>

<span data-ttu-id="85993-117">[NuGet V3 paketi IÇERIK API](../api/package-base-address-resource.md)'sini kullanarak v 12.0.1 üzerinde Newtonsoft.Jsindirin:</span><span class="sxs-lookup"><span data-stu-id="85993-117">Download Newtonsoft.Json v12.0.1 using the [NuGet V3 Package Content API](../api/package-base-address-resource.md):</span></span>

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a><span data-ttu-id="85993-118">Paket meta verilerini al</span><span class="sxs-lookup"><span data-stu-id="85993-118">Get package metadata</span></span>

<span data-ttu-id="85993-119">[NuGet V3 paketi meta veri API 'sini](../api/registration-base-url-resource.md)kullanarak "Newtonsoft.Json" paketine ait meta verileri alın:</span><span class="sxs-lookup"><span data-stu-id="85993-119">Get the metadata for the "Newtonsoft.Json" package using the [NuGet V3 Package Metadata API](../api/registration-base-url-resource.md):</span></span>

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a><span data-ttu-id="85993-120">Paketleri ara</span><span class="sxs-lookup"><span data-stu-id="85993-120">Search packages</span></span>

<span data-ttu-id="85993-121">[NuGet v3 arama API](../api/search-query-service-resource.md)'sini kullanarak "JSON" paketleri arayın:</span><span class="sxs-lookup"><span data-stu-id="85993-121">Search for "json" packages using the [NuGet V3 Search API](../api/search-query-service-resource.md):</span></span>

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="create-a-package"></a><span data-ttu-id="85993-122">Paket oluşturma</span><span class="sxs-lookup"><span data-stu-id="85993-122">Create a package</span></span>

<span data-ttu-id="85993-123">Bir paket oluşturun, meta veri ayarlayın ve kullanarak bağımlılıklar ekleyin [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="85993-123">Create a package, set metadata, and add dependencies using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="85993-124">NuGet paketlerinin resmi NuGet **araçları kullanılarak oluşturulması ve bu** alt düzey API 'nin kullanılması önemle önerilir.</span><span class="sxs-lookup"><span data-stu-id="85993-124">It is strongly recommended that NuGet packages are created using the official NuGet tooling and **not** using this low-level API.</span></span> <span data-ttu-id="85993-125">İyi biçimlendirilmiş bir paket için önemli özellikler vardır ve araç en son sürümü bu en iyi uygulamaların sağlanmasına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="85993-125">There are a variety of characteristics important for a well-formed package and the latest version of tooling helps incorporate these best practices.</span></span>
> 
> <span data-ttu-id="85993-126">NuGet paketleri oluşturma hakkında daha fazla bilgi için bkz. [paket oluşturma iş akışına](../create-packages/overview-and-workflow.md) genel bakış ve resmi paket araçları (örneğin, [DotNet CLI kullanılarak](../create-packages/creating-a-package-dotnet-cli.md)) belgeleri.</span><span class="sxs-lookup"><span data-stu-id="85993-126">For more information about creating NuGet packages, see the overview of the [package creation workflow](../create-packages/overview-and-workflow.md) and the documentation for official pack tooling (for example, [using the dotnet CLI](../create-packages/creating-a-package-dotnet-cli.md)).</span></span>

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a><span data-ttu-id="85993-127">Paket okuma</span><span class="sxs-lookup"><span data-stu-id="85993-127">Read a package</span></span>

<span data-ttu-id="85993-128">Kullanarak bir dosya akışından paket okuyun [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="85993-128">Read a package from a file stream using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

## <a name="third-party-documentation"></a><span data-ttu-id="85993-129">Üçüncü taraf belgeleri</span><span class="sxs-lookup"><span data-stu-id="85993-129">Third-party documentation</span></span>

<span data-ttu-id="85993-130">Aşağıdaki blog serisindeki bazı API 'ler için örnekler ve belgeler için Glick, yayımlanan 2016:</span><span class="sxs-lookup"><span data-stu-id="85993-130">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="85993-131">NuGet v3 kitaplıklarını keşfetme, 1. Bölüm: giriş ve kavramlar</span><span class="sxs-lookup"><span data-stu-id="85993-131">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="85993-132">NuGet v3 kitaplıklarını keşfetme, Bölüm 2: paketleri arama</span><span class="sxs-lookup"><span data-stu-id="85993-132">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="85993-133">NuGet v3 kitaplıklarını keşfetme, 3. Bölüm: paketleri yükleme</span><span class="sxs-lookup"><span data-stu-id="85993-133">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="85993-134">Bu blog gönderileri, NuGet istemci SDK paketlerinin **3.4.3** sürümü yayımlandıktan kısa bir süre sonra yazıldı.</span><span class="sxs-lookup"><span data-stu-id="85993-134">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="85993-135">Paketlerin daha yeni sürümleri, blog gönderilerinin bilgileriyle uyumsuz olabilir.</span><span class="sxs-lookup"><span data-stu-id="85993-135">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="85993-136">Marve Glick 'in blog serisine, NuGet paketlerini yüklemek için NuGet Istemci SDK 'sını kullanma konusunda farklı bir yaklaşım tanıtan bir izleme blog gönderisi Björkström.</span><span class="sxs-lookup"><span data-stu-id="85993-136">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK to install NuGet packages:</span></span>

- [<span data-ttu-id="85993-137">NuGet v3 kitaplıklarını yeniden ziyaret etme</span><span class="sxs-lookup"><span data-stu-id="85993-137">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
