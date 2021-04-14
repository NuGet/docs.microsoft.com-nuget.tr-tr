---
title: NuGet İstemci SDK’sı
description: API gelişiyor ve henüz belgelenmemiştir, ancak örnek, bave Glick 'in blogundan bulunabilir.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 6417c971dc13cf9ed05dcec4e4156af94c0ea058
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387393"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="ddbd8-103">NuGet İstemci SDK’sı</span><span class="sxs-lookup"><span data-stu-id="ddbd8-103">NuGet Client SDK</span></span>

<span data-ttu-id="ddbd8-104">*NuGet istemci SDK 'sı* bir NuGet paketleri grubunu ifade eder:</span><span class="sxs-lookup"><span data-stu-id="ddbd8-104">The *NuGet Client SDK* refers to a group of NuGet packages:</span></span>

* <span data-ttu-id="ddbd8-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) -HTTP ve dosya tabanlı NuGet akışlarıyla etkileşim kurmak için kullanılır</span><span class="sxs-lookup"><span data-stu-id="ddbd8-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Used to interact with HTTP and file-based NuGet feeds</span></span>
* <span data-ttu-id="ddbd8-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) -NuGet paketleri ile etkileşim kurmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ddbd8-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Used to interact with NuGet packages.</span></span> <span data-ttu-id="ddbd8-107">`NuGet.Protocol` Bu pakete bağımlıdır</span><span class="sxs-lookup"><span data-stu-id="ddbd8-107">`NuGet.Protocol` depends on this package</span></span>

<span data-ttu-id="ddbd8-108">Bu paketlerin kaynak kodunu [NuGet/NuGet. Client](https://github.com/NuGet/NuGet.Client) GitHub deposunda bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ddbd8-108">You can find the source code for these packages in the [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) GitHub repository.</span></span>
<span data-ttu-id="ddbd8-109">Bu örneklerin kaynak kodunu GitHub 'daki [NuGet. Protocol. Samples](https://github.com/NuGet/Samples/tree/main/NuGetProtocolSamples) projesinde bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ddbd8-109">You can find the source code for these examples on the [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/main/NuGetProtocolSamples) project on GitHub.</span></span>

> [!Note]
> <span data-ttu-id="ddbd8-110">NuGet sunucu protokolü hakkındaki belgeler için lütfen [NuGet sunucu API](~/api/overview.md)'sine bakın.</span><span class="sxs-lookup"><span data-stu-id="ddbd8-110">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="nugetprotocol"></a><span data-ttu-id="ddbd8-111">NuGet. Protocol</span><span class="sxs-lookup"><span data-stu-id="ddbd8-111">NuGet.Protocol</span></span>

<span data-ttu-id="ddbd8-112">`NuGet.Protocol`Http ve klasör tabanlı NuGet paket akışlarıyla etkileşim kurmak için paketini yükler:</span><span class="sxs-lookup"><span data-stu-id="ddbd8-112">Install the `NuGet.Protocol` package to interact with HTTP and folder-based NuGet package feeds:</span></span>

```ps1
dotnet add package NuGet.Protocol
```

> [!Tip]
> <span data-ttu-id="ddbd8-113">`Repository.Factory` ad alanında tanımlanmıştır `NuGet.Protocol.Core.Types` ve `GetCoreV3` yöntemi ad alanında tanımlanan bir genişletme yöntemidir `NuGet.Protocol` .</span><span class="sxs-lookup"><span data-stu-id="ddbd8-113">`Repository.Factory` is defined in the `NuGet.Protocol.Core.Types` namespace, and the `GetCoreV3` method is an extension method defined in the `NuGet.Protocol` namespace.</span></span> <span data-ttu-id="ddbd8-114">Bu nedenle, `using` her iki ad alanı için deyimler eklemeniz gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="ddbd8-114">Therefore, you will need to add `using` statements for both namespaces.</span></span>

### <a name="list-package-versions"></a><span data-ttu-id="ddbd8-115">Paket sürümlerini Listele</span><span class="sxs-lookup"><span data-stu-id="ddbd8-115">List package versions</span></span>

<span data-ttu-id="ddbd8-116">[NuGet V3 paketi IÇERIK API](../api/package-base-address-resource.md#enumerate-package-versions)'sini kullanarak tüm Newtonsoft.Jssürümlerini bulun:</span><span class="sxs-lookup"><span data-stu-id="ddbd8-116">Find all versions of Newtonsoft.Json using the [NuGet V3 Package Content API](../api/package-base-address-resource.md#enumerate-package-versions):</span></span>

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a><span data-ttu-id="ddbd8-117">Paket indir</span><span class="sxs-lookup"><span data-stu-id="ddbd8-117">Download a package</span></span>

<span data-ttu-id="ddbd8-118">[NuGet V3 paketi IÇERIK API](../api/package-base-address-resource.md)'sini kullanarak v 12.0.1 üzerinde Newtonsoft.Jsindirin:</span><span class="sxs-lookup"><span data-stu-id="ddbd8-118">Download Newtonsoft.Json v12.0.1 using the [NuGet V3 Package Content API](../api/package-base-address-resource.md):</span></span>

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a><span data-ttu-id="ddbd8-119">Paket meta verilerini al</span><span class="sxs-lookup"><span data-stu-id="ddbd8-119">Get package metadata</span></span>

<span data-ttu-id="ddbd8-120">[NuGet V3 paketi meta veri API 'sini](../api/registration-base-url-resource.md)kullanarak "Newtonsoft.Json" paketine ait meta verileri alın:</span><span class="sxs-lookup"><span data-stu-id="ddbd8-120">Get the metadata for the "Newtonsoft.Json" package using the [NuGet V3 Package Metadata API](../api/registration-base-url-resource.md):</span></span>

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a><span data-ttu-id="ddbd8-121">Paketleri ara</span><span class="sxs-lookup"><span data-stu-id="ddbd8-121">Search packages</span></span>

<span data-ttu-id="ddbd8-122">[NuGet v3 arama API](../api/search-query-service-resource.md)'sini kullanarak "JSON" paketleri arayın:</span><span class="sxs-lookup"><span data-stu-id="ddbd8-122">Search for "json" packages using the [NuGet V3 Search API](../api/search-query-service-resource.md):</span></span>

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="push-a-package"></a><span data-ttu-id="ddbd8-123">Paket gönder</span><span class="sxs-lookup"><span data-stu-id="ddbd8-123">Push a package</span></span>

<span data-ttu-id="ddbd8-124">[NuGet v3 Push ve DELETE API](../api/package-publish-resource.md)kullanarak bir paketi gönderin:</span><span class="sxs-lookup"><span data-stu-id="ddbd8-124">Push a package using the [NuGet V3 Push and Delete API](../api/package-publish-resource.md):</span></span>

[!code-csharp[PushPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=PushPackage)]

### <a name="delete-a-package"></a><span data-ttu-id="ddbd8-125">Paket silme</span><span class="sxs-lookup"><span data-stu-id="ddbd8-125">Delete a package</span></span>

<span data-ttu-id="ddbd8-126">[NuGet v3 Push ve DELETE API 'yi](../api/package-publish-resource.md)kullanarak bir paketi silme:</span><span class="sxs-lookup"><span data-stu-id="ddbd8-126">Delete a package using the [NuGet V3 Push and Delete API](../api/package-publish-resource.md):</span></span>

> [!Note]
> <span data-ttu-id="ddbd8-127">NuGet sunucuları bir paket silme isteğini "sabit silme", "geçici silme" veya "listeden kaldır" olarak yorumlamaya ücretsizdir.</span><span class="sxs-lookup"><span data-stu-id="ddbd8-127">NuGet servers are free to interpret a package delete request as a "hard delete", "soft delete", or "unlist".</span></span>
> <span data-ttu-id="ddbd8-128">Örneğin, nuget.org paket silme isteğini "Unlist" olarak yorumlar.</span><span class="sxs-lookup"><span data-stu-id="ddbd8-128">For example, nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="ddbd8-129">Bu uygulama hakkında daha fazla bilgi için bkz. [paketleri silme](../nuget-org/policies/deleting-packages.md) ilkesi.</span><span class="sxs-lookup"><span data-stu-id="ddbd8-129">For more information about this practice, see the [Deleting Packages](../nuget-org/policies/deleting-packages.md) policy.</span></span>

[!code-csharp[DeletePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DeletePackage)]

### <a name="work-with-authenticated-feeds"></a><span data-ttu-id="ddbd8-130">Kimliği doğrulanmış akışlarla çalışma</span><span class="sxs-lookup"><span data-stu-id="ddbd8-130">Work with authenticated feeds</span></span>

<span data-ttu-id="ddbd8-131">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol)Kimliği doğrulanmış akışlarla çalışmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="ddbd8-131">Use [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) to work with authenticated feeds.</span></span>

[!code-csharp[AuthenticatedFeed](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=AuthenticatedFeed)]

## <a name="nugetpackaging"></a><span data-ttu-id="ddbd8-132">NuGet. paketleme</span><span class="sxs-lookup"><span data-stu-id="ddbd8-132">NuGet.Packaging</span></span>

<span data-ttu-id="ddbd8-133">`NuGet.Packaging`İle etkileşimde bulunmak için paketi yükler `.nupkg` ve `.nuspec` bir akıştan dosyalar:</span><span class="sxs-lookup"><span data-stu-id="ddbd8-133">Install the `NuGet.Packaging` package to interact with `.nupkg` and `.nuspec` files from a stream:</span></span>

```ps1
dotnet add package NuGet.Packaging
```

### <a name="create-a-package"></a><span data-ttu-id="ddbd8-134">Paket oluşturma</span><span class="sxs-lookup"><span data-stu-id="ddbd8-134">Create a package</span></span>

<span data-ttu-id="ddbd8-135">Bir paket oluşturun, meta veri ayarlayın ve kullanarak bağımlılıklar ekleyin [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="ddbd8-135">Create a package, set metadata, and add dependencies using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ddbd8-136">NuGet paketlerinin resmi NuGet **araçları kullanılarak oluşturulması ve bu** alt düzey API 'nin kullanılması önemle önerilir.</span><span class="sxs-lookup"><span data-stu-id="ddbd8-136">It is strongly recommended that NuGet packages are created using the official NuGet tooling and **not** using this low-level API.</span></span> <span data-ttu-id="ddbd8-137">İyi biçimlendirilmiş bir paket için önemli özellikler vardır ve araç en son sürümü bu en iyi uygulamaların sağlanmasına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="ddbd8-137">There are a variety of characteristics important for a well-formed package and the latest version of tooling helps incorporate these best practices.</span></span>
> 
> <span data-ttu-id="ddbd8-138">NuGet paketleri oluşturma hakkında daha fazla bilgi için bkz. [paket oluşturma iş akışına](../create-packages/overview-and-workflow.md) genel bakış ve resmi paket araçları (örneğin, [DotNet CLI kullanılarak](../create-packages/creating-a-package-dotnet-cli.md)) belgeleri.</span><span class="sxs-lookup"><span data-stu-id="ddbd8-138">For more information about creating NuGet packages, see the overview of the [package creation workflow](../create-packages/overview-and-workflow.md) and the documentation for official pack tooling (for example, [using the dotnet CLI](../create-packages/creating-a-package-dotnet-cli.md)).</span></span>

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a><span data-ttu-id="ddbd8-139">Paket okuma</span><span class="sxs-lookup"><span data-stu-id="ddbd8-139">Read a package</span></span>

<span data-ttu-id="ddbd8-140">Kullanarak bir dosya akışından paket okuyun [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="ddbd8-140">Read a package from a file stream using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

## <a name="third-party-documentation"></a><span data-ttu-id="ddbd8-141">Üçüncü taraf belgeleri</span><span class="sxs-lookup"><span data-stu-id="ddbd8-141">Third-party documentation</span></span>

<span data-ttu-id="ddbd8-142">Aşağıdaki blog serisindeki bazı API 'ler için örnekler ve belgeler için Glick, yayımlanan 2016:</span><span class="sxs-lookup"><span data-stu-id="ddbd8-142">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="ddbd8-143">NuGet v3 kitaplıklarını keşfetme, 1. Bölüm: giriş ve kavramlar</span><span class="sxs-lookup"><span data-stu-id="ddbd8-143">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="ddbd8-144">NuGet v3 kitaplıklarını keşfetme, Bölüm 2: paketleri arama</span><span class="sxs-lookup"><span data-stu-id="ddbd8-144">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="ddbd8-145">NuGet v3 kitaplıklarını keşfetme, 3. Bölüm: paketleri yükleme</span><span class="sxs-lookup"><span data-stu-id="ddbd8-145">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="ddbd8-146">Bu blog gönderileri, NuGet istemci SDK paketlerinin **3.4.3** sürümü yayımlandıktan kısa bir süre sonra yazıldı.</span><span class="sxs-lookup"><span data-stu-id="ddbd8-146">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="ddbd8-147">Paketlerin daha yeni sürümleri, blog gönderilerinin bilgileriyle uyumsuz olabilir.</span><span class="sxs-lookup"><span data-stu-id="ddbd8-147">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="ddbd8-148">Marve Glick 'in blog serisine, NuGet paketlerini yüklemek için NuGet Istemci SDK 'sını kullanma konusunda farklı bir yaklaşım tanıtan bir izleme blog gönderisi Björkström.</span><span class="sxs-lookup"><span data-stu-id="ddbd8-148">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK to install NuGet packages:</span></span>

- [<span data-ttu-id="ddbd8-149">NuGet v3 kitaplıklarını yeniden ziyaret etme</span><span class="sxs-lookup"><span data-stu-id="ddbd8-149">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
