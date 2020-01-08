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
# <a name="create-nuget-packages-that-contain-com-interop-assemblies"></a>COM birlikte çalışma derlemelerini içeren NuGet paketleri oluşturma

COM birlikte çalışma derlemelerini içeren paketlerin, doğru `EmbedInteropTypes` meta verilerin PackageReference biçimi kullanılarak projelere eklenmesi için uygun bir [hedefler dosyası](creating-a-package.md#include-msbuild-props-and-targets-in-a-package) içermesi gerekir. Varsayılan olarak, PackageReference kullanıldığında tüm derlemeler için `EmbedInteropTypes` meta verileri her zaman false olur, bu nedenle hedefler dosyası bu meta verileri açıkça ekler. Çakışmaları önlemek için hedef adı benzersiz olmalıdır; ideal olarak, paket adınızın ve katıştırılmakta olan derlemenin bir birleşimini kullanın ve aşağıdaki örnekteki `{InteropAssemblyName}` bu değerle değiştirin. (Ayrıca bkz. [NuGet. Samples. Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) bir örnek için.)

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

`packages.config` yönetim biçimi kullanılırken, paketlerden derlemelere başvurular eklemek, NuGet ve Visual Studio 'Nun COM birlikte çalışma derlemelerini denetlemesini ve proje dosyasında `EmbedInteropTypes` true olarak ayarlamanızı sağlar. Bu durumda, hedefler geçersiz kılınır.

Ayrıca, varsayılan olarak, [derleme varlıkları geçişli olarak akış içermez](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets). Burada açıklandığı şekilde yazılan paketler, bir projeden proje başvurusuna geçişli bir bağımlılık olarak çekildiklerinde farklı şekilde çalışır. Paket tüketicisi, Privatevarlıkların varsayılan değerini derleme dahil değil olarak değiştirerek akışla izin verebilir.

<a name="creating-the-package"></a>