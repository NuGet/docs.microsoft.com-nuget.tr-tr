---
title: Projeler tarafından başvurulan derlemeleri seçin
description: Paketteki tüm derlemeler çalışma zamanında kullanılabilir olduğunda, paketteki derlemelerin bir alt kümesini oluşturun.
author: zivkan
ms.author: zivkan
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: b2202946d0060e09828250d240f931044d1bf485
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859037"
---
# <a name="select-assemblies-referenced-by-projects"></a>Projeler tarafından başvurulan derlemeleri seçin

Açık derleme başvuruları, tüm derlemeler çalışma zamanında kullanılabilir olduğunda, IntelliSense ve derleme için derlemelerin bir alt kümesinin kullanılmasına izin verir. `PackageReference` ve `packages.config` farklı şekilde çalışır ve bir sonuç paketi yazarlarının her iki proje türüyle uyumlu olacak şekilde paketi oluşturması gerekir.

> [!Note]
> Açık derleme başvuruları .NET Derlemeleriyle ilgilidir. Yönetilen bir derleme tarafından P/çağrılan yerel derlemeleri dağıtmak için bir yöntem değildir.

## <a name="packagereference-support"></a>`PackageReference` support

Bir proje ile paket kullandığında `PackageReference` ve paket bir `ref\<tfm>\` Dizin Içerdiğinde, NuGet bu çeviricileri derleme zamanı varlıkları olarak sınıflandırır, ancak `lib\<tfm>\` derlemeler çalışma zamanı varlıkları olarak sınıflandırılacaktır. İçindeki derlemeler `ref\<tfm>\` çalışma zamanında kullanılmaz. Bu, ' deki herhangi bir derlemenin ya `ref\<tfm>\` da ilgili bir dizinde eşleşen bir derlemeye sahip olması gerektiği anlamına gelir `lib\<tfm>\` `runtime\` , aksi takdirde çalışma zamanı hataları meydana gelir. İçindeki derlemeler `ref\<tfm>\` çalışma zamanında kullanılmadığından, paket boyutunu azaltmak için [yalnızca meta veri derlemeleri](https://github.com/dotnet/roslyn/blob/main/docs/features/refout.md) olabilir.

> [!Important]
> Bir paket nuspec `<references>` öğesini (tarafından kullanılır `packages.config` , aşağıdaki gibi) içeriyorsa ve içinde derleme içermiyorsa `ref\<tfm>\` , NuGet nuspec öğesinde listelenen derlemeleri `<references>` hem derleme hem de çalışma zamanı varlıkları olarak duyuracaktır. Bu, başvurulan derlemelerin dizindeki diğer bir derlemeyi yüklemesi gerektiğinde çalışma zamanı özel durumları olacağı anlamına gelir `lib\<tfm>\` .

> [!Note]
> Paket bir `runtime\` Dizin içeriyorsa, NuGet dizindeki varlıkları kullanamaz `lib\` .

## <a name="packagesconfig-support"></a>`packages.config` support

`packages.config`NuGet paketlerini yönetmek için kullanan projeler normalde dizindeki tüm derlemelere başvurular ekler `lib\<tfm>\` . `ref\`Dizin, destek için eklenmiştir `PackageReference` ve bu nedenle kullanılırken dikkate alınmamasıdır `packages.config` . Kullanılarak projeler için hangi derlemelerin başvurulduğunu açıkça ayarlamak için `packages.config` , paketin [ `<references>` nuspec dosyasındaki öğesini](../reference/nuspec.md#explicit-assembly-references)kullanması gerekir. Örnek:

```xml
<references>
    <group targetFramework="net45">
        <reference file="MyLibrary.dll" />
    </group>
</references>
```

> [!Note]
> `packages.config` Proje, derlemeleri çıkış dizinine kopyalamak için [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/main/documentation/wiki/ResolveAssemblyReference.md) adlı bir işlem kullanın `bin\<configuration>\` . Projenizin derlemesi kopyalanır, ardından derleme sistemi başvurulan derlemeler için derleme bildirimine bakar, ardından bu derlemeleri kopyalar ve tüm derlemeler için yinelemeli olarak yinelenir. Bu, dizininizdeki derlemelerin herhangi birinin `lib\<tfm>\` bağımlılık olarak başka herhangi bir derlemede listelenmediği anlamına gelir (derleme çalışma zamanında `Assembly.Load` , MEF veya başka bir bağımlılık ekleme çerçevesi kullanılarak yükleniyorsa), bu durumda, `bin\<configuration>\` içinde olmasına rağmen projenizin çıkış dizinine kopyalanmayabilir `bin\<tfm>\` .

## <a name="example"></a>Örnek

Pakem, `MyLib.dll` `MyHelpers.dll` ve `MyUtilities.dll` .NET Framework 4.7.2 hedefleyen üç derleme içerir. `MyUtilities.dll` yalnızca diğer iki derleme tarafından kullanılmak üzere tasarlanan sınıfları içerir, bu nedenle bu sınıfları IntelliSense 'te veya paketmi kullanan projelere derleme zamanında kullanılabilir hale getirmek istemiyorum. My `nuspec` dosyası AŞAĞıDAKI XML öğelerini içermelidir:

```xml
<references>
    <group targetFramework="net472">
        <reference file="MyLib.dll" />
        <reference file="MyHelpers.dll" />
    </group>
</references>
```

ve Paketteki dosyalar şu şekilde olacaktır:

```text
lib\net472\MyLib.dll
lib\net472\MyHelpers.dll
lib\net472\MyUtilities.dll
ref\net472\MyLib.dll
ref\net472\MyHelpers.dll
```
