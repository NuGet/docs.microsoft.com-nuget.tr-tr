---
title: COM birlikte çalışma Derlemeleriyle paket oluşturma
description: COM birlikte çalışma derlemelerini içeren paketlerin nasıl oluşturulacağını açıklar
author: JonDouglas
ms.author: jodou
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: b12672e81a974e113ffbda80560c9d3eede9c69d
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859128"
---
# <a name="create-nuget-packages-that-contain-com-interop-assemblies"></a><span data-ttu-id="d4eb2-103">COM birlikte çalışma derlemelerini içeren NuGet paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="d4eb2-103">Create NuGet packages that contain COM interop assemblies</span></span>

<span data-ttu-id="d4eb2-104">COM birlikte çalışma derlemelerini içeren paketlerin [](creating-a-package.md#include-msbuild-props-and-targets-in-a-package) `EmbedInteropTypes` , packagereference biçimi kullanılarak projelere doğru meta veriler eklenebilmesi için uygun bir hedefler dosyası içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="d4eb2-104">Packages that contain COM interop assemblies must include an appropriate [targets file](creating-a-package.md#include-msbuild-props-and-targets-in-a-package) so that the correct `EmbedInteropTypes` metadata is added to projects using the PackageReference format.</span></span> <span data-ttu-id="d4eb2-105">Varsayılan olarak, `EmbedInteropTypes` PackageReference kullanıldığında tüm derlemeler için meta veriler her zaman false olur, bu nedenle hedefler dosyası bu meta verileri açıkça ekler.</span><span class="sxs-lookup"><span data-stu-id="d4eb2-105">By default, the `EmbedInteropTypes` metadata is always false for all assemblies when PackageReference is used, so the targets file adds this metadata explicitly.</span></span> <span data-ttu-id="d4eb2-106">Çakışmaları önlemek için hedef adı benzersiz olmalıdır; ideal olarak, paket adınızın ve katıştırılmakta olan derlemenin birleşimini kullanın ve `{InteropAssemblyName}` Aşağıdaki örnekte bulunan öğesini bu değerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d4eb2-106">To avoid conflicts, the target name should be unique; ideally, use a combination of your package name and the assembly being embedded, replacing the `{InteropAssemblyName}` in the example below with that value.</span></span> <span data-ttu-id="d4eb2-107">(Ayrıca bkz. [NuGet. Samples. Interop](https://github.com/NuGet/Samples/tree/main/NuGet.Samples.Interop) bir örnek için.)</span><span class="sxs-lookup"><span data-stu-id="d4eb2-107">(Also see [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/main/NuGet.Samples.Interop) for an example.)</span></span>

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

<span data-ttu-id="d4eb2-108">`packages.config`Yönetim biçimi kullanılırken, paketlerden derlemelere başvurular eklemek NuGet ve Visual Studio 'NUN com birlikte çalışma derlemelerini denetlemesini ve `EmbedInteropTypes` Proje dosyasında true olarak ayarlayabileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d4eb2-108">Note that when using the `packages.config` management format, adding references to the assemblies from the packages causes NuGet and Visual Studio to check for COM interop assemblies and set the `EmbedInteropTypes` to true in the project file.</span></span> <span data-ttu-id="d4eb2-109">Bu durumda, hedefler geçersiz kılınır.</span><span class="sxs-lookup"><span data-stu-id="d4eb2-109">In this case, the targets are overridden.</span></span>

<span data-ttu-id="d4eb2-110">Ayrıca, varsayılan olarak, [derleme varlıkları geçişli olarak akış içermez](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="d4eb2-110">Additionally, by default the [build assets do not flow transitively](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span> <span data-ttu-id="d4eb2-111">Burada açıklandığı şekilde yazılan paketler, bir projeden proje başvurusuna geçişli bir bağımlılık olarak çekildiklerinde farklı şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="d4eb2-111">Packages authored as described here work differently when they are pulled as a transitive dependency from a project to project reference.</span></span> <span data-ttu-id="d4eb2-112">Paket tüketicisi, Privatevarlıkların varsayılan değerini derleme dahil değil olarak değiştirerek akışla izin verebilir.</span><span class="sxs-lookup"><span data-stu-id="d4eb2-112">The package consumer can allow them to flow by modifying the PrivateAssets default value to not include build.</span></span>

<a name="creating-the-package"></a>