---
title: Proje tarafından başvurulan bütünleştirilmiş kodları seçin
description: Tüm derlemeleri çalışma zamanında kullanılabilir ancak paketteki kümesini derleyici kullanılabilir hale getirmek.
author: zivkan
ms.author: zivkan
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: b32075c3f2c06c15c07d36602bdabdaee8b9405a
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427661"
---
# <a name="select-assemblies-referenced-by-projects"></a>Proje tarafından başvurulan bütünleştirilmiş kodları seçin

Açık derleme başvurularını tüm derlemeleri çalışma zamanında kullanılabilir ancak derleme ve IntelliSense için kullanılacak bir kümesini sağlar. `PackageReference` ve `packages.config` farklı çalışır ve bunun sonucunda paket yazarlarının ilgileniriz iki proje türü ile uyumlu olacak şekilde paketi oluşturmak için gerekir.

> [!Note]
> Açık derleme başvurularını .NET derlemeleri için ilgilidir. P/çağrılan yönetilen bir derlemeye olan yerel derlemeleri dağıtmak için bir yöntem değil.

## <a name="packagereference-support"></a>`PackageReference` Destek

Bir proje olan bir pakete kullandığında `PackageReference` ve paketi içeren bir `ref\<tfm>\` NuGet dizin sınıflandırmak bu derleme zamanı varlıklar çeviren sırada `lib\<tfm>\` derlemeler çalışma zamanı varlıklar sınıflandırılan. Derlemelerde `ref\<tfm>\` çalışma zamanında kullanılmaz. Bu, herhangi bir derleme için gerekli olduğu anlamına gelir `ref\<tfm>\` eşleşen derleme ya da için `lib\<tfm>\` veya ilgili `runtime\` dizin, aksi takdirde çalışma zamanı hataları büyük olasılıkla oluşur. Derlemelerde beri `ref\<tfm>\` kullanılmayan çalışma zamanında, bunlar olabilir [yalnızca meta veri bütünleştirilmiş kodları](https://github.com/dotnet/roslyn/blob/master/docs/features/refout.md) paket boyutunu küçültmek için.

> [!Important]
> Bir paket bir nuspec içeriyorsa `<references>` öğesi (tarafından kullanılan `packages.config`, aşağıya bakın) ve derlemeleri içermiyor `ref\<tfm>\`, NuGet sınıflandırmalarına listelenen derlemeleri tanıtır `<references>` öğesi derleme ve çalışma zamanı varlıklar olarak. Başvurulan derlemeleri diğer herhangi bir derlemede yük gerektiğinde, çalışma zamanı özel durumları olacağı anlamına gelir `lib\<tfm>\` dizin.

> [!Note]
> Paket içeriyorsa bir `runtime\` dizin, NuGet varlıkları kullanamazsınız `lib\` dizin.

## <a name="packagesconfig-support"></a>`packages.config` Destek

Kullanarak projeleri `packages.config` NuGet yönetmek için paketleri normalde tüm derlemelerin başvurularını eklemek `lib\<tfm>\` dizin. `ref\` Dizin desteklemek için eklenen `PackageReference` ve bu nedenle kullanırken dikkate değil `packages.config`. Hangi derlemelerin kullanarak projeleri için başvurulan açıkça ayarlamak için `packages.config`, paket kullanmalısınız [ `<references>` soubor nuspec öğesinde](../reference/nuspec.md#explicit-assembly-references). Örneğin:

```xml
<references>
    <group targetFramework="net45">
        <reference file="MyLibrary.dll" />
    </group>
</references>
```

> [!Note]
> `packages.config` adlı bir işlem proje kullanım [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/master/documentation/wiki/ResolveAssemblyReference.md) derlemeleri kopyalamak için `bin\<configuration>\` çıkış dizini. Proje derleme kopyalanır, ardından derleme sistemi, başvurulan derlemeler için derleme bildirimini inceler ve ardından bu derlemeleri kopyalar ve yinelemeli olarak tüm derlemeler için yinelenir. Bu durumlarda derlemelerin hiçbirini anlamına gelir, `lib\<tfm>\` herhangi diğer derleme bildiriminde bağımlılık olarak dizin listelenmez (derleme çalışma zamanı kullanarak yüklü ise `Assembly.Load`, MEF veya başka bir bağımlılık ekleme framework), sonra çalışmıyor olabilir projenizin kopyalanan `bin\<configuration>\` işlemlerle rağmen çıkış dizinine `bin\<tfm>\`.

## <a name="example"></a>Örnek

Paketimle üç derlemeleri içerir `MyLib.dll`, `MyHelpers.dll` ve `MyUtilities.dll`, .NET Framework 4.7.2 hedefleme. `MyUtilities.dll` Bu sınıfların IntelliSense içinde ya da derleme zamanında paketimle kullanarak projeleri için kullanılabilmesini istemediğiniz için yalnızca diğer iki derlemeler tarafından kullanılmak üzere sınıfları içerir. My `nuspec` dosya aşağıdaki XML öğeleri içeren gerekir:

```xml
<references>
    <group targetFramework="net472">
        <reference file="MyLib.dll" />
        <reference file="MyHelpers.dll" />
    </group>
</references>
```

ve paketteki dosyaların olacaktır:

```text
lib\net472\MyLib.dll
lib\net472\MyHelpers.dll
lib\net472\MyUtilities.dll
ref\net472\MyLib.dll
ref\net472\MyHelpers.dll
```
