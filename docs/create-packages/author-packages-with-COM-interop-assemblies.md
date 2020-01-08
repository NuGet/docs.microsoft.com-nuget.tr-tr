---
title: COM birlikte çalışma Derlemeleriyle paket oluşturma
description: COM birlikte çalışma derlemelerini içeren paketlerin nasıl oluşturulacağını açıklar
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: de164b136a1636b89f674b8626613094fc53e04c
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75385578"
---
# <a name="create-nuget-packages-that-contain-com-interop-assemblies"></a><span data-ttu-id="b0568-103">COM birlikte çalışma derlemelerini içeren NuGet paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="b0568-103">Create NuGet packages that contain COM interop assemblies</span></span>

<span data-ttu-id="b0568-104">COM birlikte çalışma derlemelerini içeren paketlerin, doğru `EmbedInteropTypes` meta verilerin PackageReference biçimi kullanılarak projelere eklenmesi için uygun bir [hedefler dosyası](creating-a-package.md#include-msbuild-props-and-targets-in-a-package) içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0568-104">Packages that contain COM interop assemblies must include an appropriate [targets file](creating-a-package.md#include-msbuild-props-and-targets-in-a-package) so that the correct `EmbedInteropTypes` metadata is added to projects using the PackageReference format.</span></span> <span data-ttu-id="b0568-105">Varsayılan olarak, PackageReference kullanıldığında tüm derlemeler için `EmbedInteropTypes` meta verileri her zaman false olur, bu nedenle hedefler dosyası bu meta verileri açıkça ekler.</span><span class="sxs-lookup"><span data-stu-id="b0568-105">By default, the `EmbedInteropTypes` metadata is always false for all assemblies when PackageReference is used, so the targets file adds this metadata explicitly.</span></span> <span data-ttu-id="b0568-106">Çakışmaları önlemek için hedef adı benzersiz olmalıdır; ideal olarak, paket adınızın ve katıştırılmakta olan derlemenin bir birleşimini kullanın ve aşağıdaki örnekteki `{InteropAssemblyName}` bu değerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b0568-106">To avoid conflicts, the target name should be unique; ideally, use a combination of your package name and the assembly being embedded, replacing the `{InteropAssemblyName}` in the example below with that value.</span></span> <span data-ttu-id="b0568-107">(Ayrıca bkz. [NuGet. Samples. Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) bir örnek için.)</span><span class="sxs-lookup"><span data-stu-id="b0568-107">(Also see [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) for an example.)</span></span>

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

<span data-ttu-id="b0568-108">`packages.config` yönetim biçimi kullanılırken, paketlerden derlemelere başvurular eklemek, NuGet ve Visual Studio 'Nun COM birlikte çalışma derlemelerini denetlemesini ve proje dosyasında `EmbedInteropTypes` true olarak ayarlamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="b0568-108">Note that when using the `packages.config` management format, adding references to the assemblies from the packages causes NuGet and Visual Studio to check for COM interop assemblies and set the `EmbedInteropTypes` to true in the project file.</span></span> <span data-ttu-id="b0568-109">Bu durumda, hedefler geçersiz kılınır.</span><span class="sxs-lookup"><span data-stu-id="b0568-109">In this case, the targets are overridden.</span></span>

<span data-ttu-id="b0568-110">Ayrıca, varsayılan olarak, [derleme varlıkları geçişli olarak akış içermez](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="b0568-110">Additionally, by default the [build assets do not flow transitively](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span> <span data-ttu-id="b0568-111">Burada açıklandığı şekilde yazılan paketler, bir projeden proje başvurusuna geçişli bir bağımlılık olarak çekildiklerinde farklı şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="b0568-111">Packages authored as described here work differently when they are pulled as a transitive dependency from a project to project reference.</span></span> <span data-ttu-id="b0568-112">Paket tüketicisi, Privatevarlıkların varsayılan değerini derleme dahil değil olarak değiştirerek akışla izin verebilir.</span><span class="sxs-lookup"><span data-stu-id="b0568-112">The package consumer can allow them to flow by modifying the PrivateAssets default value to not include build.</span></span>

<a name="creating-the-package"></a>