---
title: Projelere Göre Başvurulan Meclisleri Seçin
description: Tüm derlemeler çalışma zamanında kullanılabilirken, paketteki derlemelerin bir alt kümesini derleyicinin kullanımına sun.
author: zivkan
ms.author: zivkan
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: b32075c3f2c06c15c07d36602bdabdaee8b9405a
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427661"
---
# <a name="select-assemblies-referenced-by-projects"></a>Projelere Göre Başvurulan Meclisleri Seçin

Açık montaj başvuruları, intelliSense ve derleme için bir derleme alt kümesinin kullanılmasına olanak sağlarken, tüm derlemeler çalışma zamanında kullanılabilir. `PackageReference`ve `packages.config` farklı çalışma ve sonuç olarak paket yazarları her iki proje türleri ile uyumlu olacak şekilde paketi oluşturmak için dikkat etmek gerekir.

> [!Note]
> Açık montaj başvuruları .NET derlemeleri ile ilgilidir. Yönetilen bir derleme tarafından P/Invoked olan yerel derlemeleri dağıtmak için bir yöntem değildir.

## <a name="packagereference-support"></a>`PackageReference`Destek

Bir proje ile `PackageReference` bir paket kullandığında `ref\<tfm>\` ve paket bir dizin içeriyorsa, NuGet bu derlemeleri derleme zamanı varlıkları olarak sınıflandırılırken, `lib\<tfm>\` derlemeler çalışma zamanı varlıkları olarak sınıflandırılır. Montajlar `ref\<tfm>\` çalışma zamanında kullanılmaz. Bu, herhangi bir derlemenin `ref\<tfm>\` eşleşen bir derlemenin `lib\<tfm>\` veya `runtime\` ilgili bir dizinde olması gerektiği anlamına gelir, aksi takdirde çalışma zamanı hataları büyük olasılıkla oluşacaktır. Çalışma `ref\<tfm>\` zamanında derlemeler kullanılmadığından, paket boyutunu azaltmak için [yalnızca meta veri derlemeleri](https://github.com/dotnet/roslyn/blob/master/docs/features/refout.md) olabilir.

> [!Important]
> Bir `<references>` paket nuspec öğesi içeriyorsa (aşağıda görmek `packages.config`te, aşağıya `ref\<tfm>\`bakın) ve derlemeler içermiyorsa, NuGet nuspec `<references>` öğesinde listelenen derlemelerin hem derleme hem de çalışma zamanı varlıkları olarak tanıtılacaktır. Bu, başvurulan derlemelerin `lib\<tfm>\` dizindeki diğer derlemeleri yüklemesi gerektiğinde çalışma zamanı özel durumları olacağı anlamına gelir.

> [!Note]
> Paketbir `runtime\` dizin içeriyorsa, NuGet `lib\` dizindeki varlıkları kullanamaz.

## <a name="packagesconfig-support"></a>`packages.config`Destek

NuGet `packages.config` paketlerini yönetmek için kullanan projeler normalde `lib\<tfm>\` dizindeki tüm derlemelere başvurular ekler. Dizin `ref\` destek `PackageReference` eklendi ve bu nedenle kullanırken `packages.config`dikkate alınmadı. Hangi derlemelerin kullanılan `packages.config`projeler için başvurulmasını açıkça ayarlamak için, paketin [ `<references>` nuspec dosyasındaki öğeyi](../reference/nuspec.md#explicit-assembly-references)kullanması gerekir. Örneğin:

```xml
<references>
    <group targetFramework="net45">
        <reference file="MyLibrary.dll" />
    </group>
</references>
```

> [!Note]
> `packages.config``bin\<configuration>\` proje, derlemeleri çıktı dizinine kopyalamak için [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/master/documentation/wiki/ResolveAssemblyReference.md) adlı bir işlem kullanın. Projenizin derlemesi kopyalanır, sonra yapı sistemi başvurulan derlemeler için derleme bildirimine bakar, ardından bu derlemeleri kopyalar ve tüm derlemeler için özyinelemeli olarak yineler. `lib\<tfm>\` Bu, dizininizdeki derlemelerden herhangi birinin başka bir derlemenin bildiriminde bağımlılık olarak listelenmemesi durumunda (derleme `Assembly.Load`çalışma zamanında , MEF veya başka bir bağımlılık enjeksiyon çerçevesi kullanılarak `bin\<configuration>\` yükleniyorsa), `bin\<tfm>\`içinde olmasına rağmen projenizin çıktı dizinine kopyalanamayabileceği anlamına gelir.

## <a name="example"></a>Örnek

Paketim,.NET `MyLib.dll` `MyHelpers.dll` `MyUtilities.dll`Framework 4.7.2'yi hedefleyen üç derleme içerir. `MyUtilities.dll`yalnızca diğer iki derleme tarafından kullanılmak üzere tasarlanmış sınıfları içerir, bu nedenle bu sınıfları IntelliSense'de kullanılabilir hale getirmek veya paketimi kullanarak projelere zaman derlemek istemiyorum. Dosyamın `nuspec` aşağıdaki XML öğelerini içermesi gerekir:

```xml
<references>
    <group targetFramework="net472">
        <reference file="MyLib.dll" />
        <reference file="MyHelpers.dll" />
    </group>
</references>
```

ve paketteki dosyalar:

```text
lib\net472\MyLib.dll
lib\net472\MyHelpers.dll
lib\net472\MyUtilities.dll
ref\net472\MyLib.dll
ref\net472\MyHelpers.dll
```
