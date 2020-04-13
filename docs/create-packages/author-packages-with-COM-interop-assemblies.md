---
title: COM interop montajları ile paketler oluşturma
description: COM interop derlemeleri içeren paketlerin nasıl oluşturulacaklarını açıklar
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: de164b136a1636b89f674b8626613094fc53e04c
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "75385578"
---
# <a name="create-nuget-packages-that-contain-com-interop-assemblies"></a><span data-ttu-id="6fd2a-103">COM interop montajları içeren NuGet paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="6fd2a-103">Create NuGet packages that contain COM interop assemblies</span></span>

<span data-ttu-id="6fd2a-104">COM interop derlemeleri içeren paketler, [targets file](creating-a-package.md#include-msbuild-props-and-targets-in-a-package) PackageReference biçimini `EmbedInteropTypes` kullanarak projelere doğru meta verilerin eklenmesi için uygun bir hedef dosyası içermelidir.</span><span class="sxs-lookup"><span data-stu-id="6fd2a-104">Packages that contain COM interop assemblies must include an appropriate [targets file](creating-a-package.md#include-msbuild-props-and-targets-in-a-package) so that the correct `EmbedInteropTypes` metadata is added to projects using the PackageReference format.</span></span> <span data-ttu-id="6fd2a-105">Varsayılan olarak, `EmbedInteropTypes` PackageReference kullanıldığında meta veriler tüm derlemeler için her zaman yanlıştır, bu nedenle hedefler dosyası bu meta verileri açıkça ekler.</span><span class="sxs-lookup"><span data-stu-id="6fd2a-105">By default, the `EmbedInteropTypes` metadata is always false for all assemblies when PackageReference is used, so the targets file adds this metadata explicitly.</span></span> <span data-ttu-id="6fd2a-106">Çakışmaları önlemek için hedef adı benzersiz olmalıdır; ideal olarak, paket adınızın ve montajın gömülü olmasının `{InteropAssemblyName}` bir birleşimini kullanarak aşağıdaki örnekte bu değerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="6fd2a-106">To avoid conflicts, the target name should be unique; ideally, use a combination of your package name and the assembly being embedded, replacing the `{InteropAssemblyName}` in the example below with that value.</span></span> <span data-ttu-id="6fd2a-107">(Ayrıca bir örnek için [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) bakın.)</span><span class="sxs-lookup"><span data-stu-id="6fd2a-107">(Also see [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) for an example.)</span></span>

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

<span data-ttu-id="6fd2a-108">`packages.config` Yönetim biçimini kullanırken, paketlerden derlemelere referans lar eklemek NuGet ve Visual Studio'nun COM interop derlemelerini denetlemesine ve proje dosyasında doğru olarak ayarlamasına `EmbedInteropTypes` neden olur.</span><span class="sxs-lookup"><span data-stu-id="6fd2a-108">Note that when using the `packages.config` management format, adding references to the assemblies from the packages causes NuGet and Visual Studio to check for COM interop assemblies and set the `EmbedInteropTypes` to true in the project file.</span></span> <span data-ttu-id="6fd2a-109">Bu durumda, hedefler geçersiz kılınmış.</span><span class="sxs-lookup"><span data-stu-id="6fd2a-109">In this case, the targets are overridden.</span></span>

<span data-ttu-id="6fd2a-110">Ayrıca, varsayılan olarak [yapı varlıkları geçişli olarak akmaz.](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)</span><span class="sxs-lookup"><span data-stu-id="6fd2a-110">Additionally, by default the [build assets do not flow transitively](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span> <span data-ttu-id="6fd2a-111">Burada açıklandığı şekilde yazılmış paketler, projeden proje başvurusuna geçişli bağımlılık olarak çekildiğinde farklı çalışır.</span><span class="sxs-lookup"><span data-stu-id="6fd2a-111">Packages authored as described here work differently when they are pulled as a transitive dependency from a project to project reference.</span></span> <span data-ttu-id="6fd2a-112">Paket tüketicisi, PrivateAssets varsayılan değerini yapıyı içermeyecek şekilde değiştirerek akış yapmalarına izin verebilir.</span><span class="sxs-lookup"><span data-stu-id="6fd2a-112">The package consumer can allow them to flow by modifying the PrivateAssets default value to not include build.</span></span>

<a name="creating-the-package"></a>