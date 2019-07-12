---
title: COM birlikte çalışma derlemeleriyle paketleri oluşturma
description: COM birlikte çalışma derlemelerini içeren paketleri oluşturmayı açıklar
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: d0e368f43171ce71abc60b3e09d08b010d2d8880
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67843532"
---
## <a name="create-nuget-packages-that-contain-com-interop-assemblies"></a>COM birlikte çalışma derlemelerini içeren NuGet paketleri oluşturun

COM birlikte çalışma derlemelerini içeren paketleri uygun bir içermelidir [hedefler dosyası](creating-a-package.md#include-msbuild-props-and-targets-in-a-package) böylece doğru `EmbedInteropTypes` PackageReference biçimini kullanan projeler için meta veriler eklenir. Varsayılan olarak, `EmbedInteropTypes` meta verileri olduğundan her zaman tüm derlemeler için false PackageReference kullanıldığında, bu meta veriler, açıkça hedefler dosyası ekler. Çakışmaları önlemek için hedef adı benzersiz olmalıdır; İdeal olarak, paket adınızla ve katıştırılmış, değiştirilmesini olan derleme birleşimini kullanın `{InteropAssemblyName}` aşağıdaki örnekte bu değere sahip. (Ayrıca bkz: [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) bir örnek.)

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

Kullanırken dikkat `packages.config` yönetim biçimi paketlerinden derlemelerine başvurular ekleme oluyor NuGet ve Visual Studio için COM birlikte çalışma derlemeleri denetleyin ve ayarlamak `EmbedInteropTypes` proje dosyasındaki true. Bu durumda geçersiz kılınmış hedeflerdir.

Ayrıca, varsayılan olarak [derleme varlıklar akan geçişli](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets). Geçişli bağımlılık gelen bir projeden projeye başvuru olarak çekildiğinde burada iş farklı bir şekilde açıklandığı yazılan paketler. Paket kullanıcısı PrivateAssets varsayılan değer, derleme içermeyecek şekilde değiştirerek akmasına izin verebilirsiniz.

<a name="creating-the-package"></a>