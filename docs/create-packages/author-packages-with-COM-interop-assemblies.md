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
# <a name="create-nuget-packages-that-contain-com-interop-assemblies"></a>COM birlikte çalışma derlemelerini içeren NuGet paketleri oluşturma

COM birlikte çalışma derlemelerini içeren paketlerin [](creating-a-package.md#include-msbuild-props-and-targets-in-a-package) `EmbedInteropTypes` , packagereference biçimi kullanılarak projelere doğru meta veriler eklenebilmesi için uygun bir hedefler dosyası içermesi gerekir. Varsayılan olarak, `EmbedInteropTypes` PackageReference kullanıldığında tüm derlemeler için meta veriler her zaman false olur, bu nedenle hedefler dosyası bu meta verileri açıkça ekler. Çakışmaları önlemek için hedef adı benzersiz olmalıdır; ideal olarak, paket adınızın ve katıştırılmakta olan derlemenin birleşimini kullanın ve `{InteropAssemblyName}` Aşağıdaki örnekte bulunan öğesini bu değerle değiştirin. (Ayrıca bkz. [NuGet. Samples. Interop](https://github.com/NuGet/Samples/tree/main/NuGet.Samples.Interop) bir örnek için.)

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

`packages.config`Yönetim biçimi kullanılırken, paketlerden derlemelere başvurular eklemek NuGet ve Visual Studio 'NUN com birlikte çalışma derlemelerini denetlemesini ve `EmbedInteropTypes` Proje dosyasında true olarak ayarlayabileceğini unutmayın. Bu durumda, hedefler geçersiz kılınır.

Ayrıca, varsayılan olarak, [derleme varlıkları geçişli olarak akış içermez](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets). Burada açıklandığı şekilde yazılan paketler, bir projeden proje başvurusuna geçişli bir bağımlılık olarak çekildiklerinde farklı şekilde çalışır. Paket tüketicisi, Privatevarlıkların varsayılan değerini derleme dahil değil olarak değiştirerek akışla izin verebilir.

<a name="creating-the-package"></a>