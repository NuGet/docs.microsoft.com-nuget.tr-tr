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
# <a name="create-nuget-packages-that-contain-com-interop-assemblies"></a>COM interop montajları içeren NuGet paketleri oluşturma

COM interop derlemeleri içeren paketler, [targets file](creating-a-package.md#include-msbuild-props-and-targets-in-a-package) PackageReference biçimini `EmbedInteropTypes` kullanarak projelere doğru meta verilerin eklenmesi için uygun bir hedef dosyası içermelidir. Varsayılan olarak, `EmbedInteropTypes` PackageReference kullanıldığında meta veriler tüm derlemeler için her zaman yanlıştır, bu nedenle hedefler dosyası bu meta verileri açıkça ekler. Çakışmaları önlemek için hedef adı benzersiz olmalıdır; ideal olarak, paket adınızın ve montajın gömülü olmasının `{InteropAssemblyName}` bir birleşimini kullanarak aşağıdaki örnekte bu değerle değiştirin. (Ayrıca bir örnek için [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) bakın.)

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

`packages.config` Yönetim biçimini kullanırken, paketlerden derlemelere referans lar eklemek NuGet ve Visual Studio'nun COM interop derlemelerini denetlemesine ve proje dosyasında doğru olarak ayarlamasına `EmbedInteropTypes` neden olur. Bu durumda, hedefler geçersiz kılınmış.

Ayrıca, varsayılan olarak [yapı varlıkları geçişli olarak akmaz.](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets) Burada açıklandığı şekilde yazılmış paketler, projeden proje başvurusuna geçişli bağımlılık olarak çekildiğinde farklı çalışır. Paket tüketicisi, PrivateAssets varsayılan değerini yapıyı içermeyecek şekilde değiştirerek akış yapmalarına izin verebilir.

<a name="creating-the-package"></a>