---
title: UWP projeleri ile dosyada NuGet project.js
description: Evrensel Windows Platformu (UWP) projelerinde NuGet bağımlılıklarını izlemek için project.jsdosyanın nasıl kullanıldığına ilişkin açıklama.
author: JonDouglas
ms.author: jodou
ms.date: 07/17/2017
ms.topic: conceptual
ms.openlocfilehash: 30e2272aafb5d2ea8d932e3cb0209d97c30b3209
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773801"
---
# <a name="projectjson-and-uwp"></a>project.json ve UWP

> [!Important]
> Bu içerik kullanımdan kaldırılmıştır. Projeler ya `packages.config` ya da PackageReference biçimlerini kullanmalıdır.

Bu belgede, NuGet 3 + (Visual Studio 2015 ve üzeri) özelliklerini kullanan paket yapısı açıklanmaktadır. ' `minClientVersion` In özelliği, `.nuspec` burada açıklanan özelliklerin 3,1 olarak ayarlanarak gerekli olduğunu belirten bir durum için kullanılabilir.

## <a name="adding-uwp-support-to-an-existing-package"></a>Mevcut bir pakete UWP desteği ekleniyor

Mevcut bir paketiniz varsa ve UWP uygulamaları için destek eklemek istiyorsanız, burada açıklanan paketleme biçimini benimsemeniz gerekmez. Bu biçimi yalnızca, açıkladığı özellikleri gerektiriyorsa ve yalnızca NuGet istemcisinin sürüm 3 + ' e güncelleştirilmiş istemcilerle çalışmak istiyorsanız benimsemeniz gerekir.

## <a name="i-already-target-netcore45"></a>Netcore45 zaten hedefdim

`netcore45`Zaten hedefleyin ve buradaki özelliklerden faydalanmanız gerekmiyorsa, hiçbir işlem yapmanız gerekmez. `netcore45` paketler UWP uygulamaları tarafından tüketilebilir.

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a>Windows 10 ' un belirli API 'lerden faydalanmak istiyorum

Bu durumda, `uap10.0` hedef Framework bilinen adını (tfd veya TXD) paketinize eklemeniz gerekir. Paketinizdeki yeni bir klasör oluşturun ve derlenen derlemeyi bu klasöre Windows 10 ile çalışacak şekilde ekleyin.

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a>Windows 10 ' a özel API 'Lere ihtiyacım var, ancak yeni .NET özellikleri mi yoksa yoksa netcore45 'e sahip değil

Bu durumda, `dotnet` TXD 'yi paketinize eklersiniz. Diğer TxMs 'lerin aksine `dotnet` bir yüzey alanı veya platformu göstermez. Bu, paketinizin, bağımlılıklarınızın üzerinde çalıştığı tüm platformlarda çalıştığını ifade edilir. TXD ile bir paket oluştururken, `dotnet` `.nuspec` bağlı olduğunuz BCL paketlerini ( `System.Text` vb.) tanımlamanız gerektiği gibi, sizin Için çok sayıda TXE özel bağımlılığı olması olasıdır `System.Xml` . Bu bağımlılıkların üzerinde çalıştığı konumlar, paketinizin nerede çalıştığını tanımlar.

### <a name="how-do-i-find-out-my-dependencies"></a>Bağımlılıklarımı bulma Nasıl yaparım?

Hangi bağımlılıkların listeye göre olduğunu anlamak için iki yol vardır:

1. [Nuspec bağımlılık Oluşturucu](https://github.com/onovotny/ReferenceGenerator) **3. taraf** aracını kullanın. Araç işlemi otomatikleştirir ve `.nuspec` derleme üzerindeki bağımlı paketlerle dosyanızı güncelleştirir. Bu, [Nuspec. ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/)adlı bir NuGet paketi ile kullanılabilir.

1. (Sabit yol) `ILDasm` `.dll` Çalışma zamanında hangi derlemelerin gerçekten gerekli olduğunu görmek için ' i kullanın. Ardından bunların her birinin nereden geldiği NuGet paketini saptayın.

[`project.json`](project-json.md)TXD 'yi destekleyen bir paket oluşturulmasına yardımcı olan özellikler hakkındaki ayrıntılar için konusuna bakın `dotnet` .

> [!Important]
> Paketinizin PCL projeleriyle çalışmayı amaçlıyorsa, `dotnet` uyarı ve potansiyel Uyumluluk sorunlarından kaçınmak için bir klasör oluşturmanız önerilir.

## <a name="directory-structure"></a>Dizin yapısı

Bu biçimi kullanan NuGet paketleri, aşağıdaki iyi bilinen klasör ve davranışlara sahiptir:

| Klasör | Davranışlar |
| --- | --- |
| Oluşturma | Bu klasördeki MSBuild hedeflerini ve props dosyalarını içerir, ancak başka bir değişiklik yoktur. |
| Araçlar | `install.ps1` ve `uninstall.ps1` çalıştırılmaz. `init.ps1` her zaman sahip olduğu için geçerlidir. |
| Content | İçerik, kullanıcının projesine otomatik olarak kopyalanmaz. Projeye dahil içerik ekleme desteği sonraki bir sürüm için planlanmaktadır. |
| LIB | Birçok paket için, `lib` NuGet 2. x içinde yaptığı gibi, ancak içinde hangi adların kullanılabileceği ve paketler kullanılırken doğru alt klasörü seçmek için daha iyi bir mantık ile aynı şekilde çalışacak. Ancak, ile birlikte kullanıldığında, klasörü, `ref` `lib` klasördeki derlemeler tarafından tanımlanan yüzey alanını uygulayan derlemeler içerir `ref` . |
| Ref | `ref` , bir uygulamanın derlenmesi için ortak yüzeyi (genel türler ve Yöntemler) tanımlayan .NET derlemelerini içeren isteğe bağlı bir klasördür. Bu klasördeki derlemeler uygulamaya sahip olmayabilir, yalnızca derleyicinin yüzey alanını tanımlamak için kullanılır. Pakette hiçbir klasör yoksa, `ref` `lib` hem başvuru derlemesi hem de uygulama bütünleştirilmiş kodu olur. |
| Zamanları | `runtimes` , CPU mimarisi ve işletim sistemine özel veya başka türlü platforma bağımlı ikili dosyalar gibi işletim sistemi özel kodu içeren isteğe bağlı bir klasördür. |

## <a name="msbuild-targets-and-props-files-in-packages"></a>Paketlerindeki MSBuild hedefleri ve props dosyaları

NuGet paketleri `.targets` ve `.props` paketin yüklendiği herhangi bir MSBuild projesine aktarılan dosyalar içerebilir. NuGet 2. x sürümünde, bu ekleme `<Import>` deyimleri `.csproj` dosyada yapıldı, NuGet 3,0 ' de belirli bir "projeye yükleme" eylemi yok. Bunun yerine, paket geri yükleme işlemi iki dosya `[projectname].nuget.props` ve yazar `[projectname].NuGet.targets` .

MSBuild, bu iki dosyanın arandığını bilir ve bunları otomatik olarak proje yapı işleminin sonuna ve sonuna yakın bir şekilde içeri aktarır. Bu, NuGet 2. x için çok benzer bir davranış sağlar, ancak bir büyük farklılık *vardır: Bu durumda hiçbir garanti edilen hedef/props dosyası* yoktur. Bununla birlikte, MSBuild, tanımlamayı ve özniteliklerini kullanarak sıralama yollarını `BeforeTargets` sağlar `AfterTargets` `<Target>` (bkz. [target öğesi (MSBuild)](/visualstudio/msbuild/target-element-msbuild).

## <a name="lib-and-ref"></a>LIB ve ref

`lib`NuGet v3 'de klasörün davranışı önemli ölçüde değişmemiştir. Ancak, tüm derlemeler bir TXD adlı alt klasörler içinde olmalıdır ve artık doğrudan klasörün altına yerleştirilemez `lib` . TXD, bir paketteki belirli bir varlığın çalışması beklenen platformun adıdır. Mantıksal olarak bunlar hedef çerçeve adları (TFM) uzantısıdır,,, `net45` `net46` `netcore50` ve `dnxcore50` Tüm txms örnekleridir (bkz. [hedef çerçeveler](../reference/target-frameworks.md). TXD, bir çerçeveye (TFA) ve diğer platforma özgü yüzey alanları için de başvurabilir. Örneğin UWP TXA (), `uap10.0` .net Surface alanını ve UWP uygulamaları Için Windows Surface alanını temsil eder.

Örnek LIB yapısı:

```
lib
├───net40
│       MyLibrary.dll
└───wp81
        MyLibrary.dll
```

`lib`Klasör, çalışma zamanında kullanılan derlemeleri içerir. Çoğu paket için, `lib` her hedef TxMs 'nin altındaki bir klasör gereklidir.

## <a name="ref"></a>Ref

Bazen derleme sırasında farklı bir derlemenin kullanılması gereken durumlar vardır (.NET başvuru derlemeleri bunu bugün yapın). Bu gibi durumlarda, `ref` ("başvuru derlemeleri" için kısa) adlı bir üst düzey klasör kullanın.

Çoğu paket yazarı klasöre gerek kalmaz `ref` . Derleme ve IntelliSense için tutarlı bir yüzey alanı sağlaması gereken, ancak farklı TxMs için farklı bir uygulamaya sahip olan paketler için yararlıdır. Bunun en büyük kullanım durumu, `System.*` NuGet üzerinde .NET Core gönderimi kapsamında üretilen paketlerdir. Bu paketlerin, tutarlı bir başvuru derlemeleri kümesiyle birleştirilmiş çeşitli uygulamaları vardır.

Genel olarak, klasöre eklenen derlemeler `ref` derleyiciye geçirilen başvuru derlemelerdir. csc.exe kullananlar için [C#/Reference seçenek](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) anahtarına geçirdiğimiz derlemelerdir.

Klasörün yapısı, `ref` `lib` Örneğin:

```
└───MyImageProcessingLib
        ├───lib
        │   ├───net40
        │   │       MyImageProcessingLibrary.dll
        │   │
        │   ├───net451
        │   │       MyImageProcessingLibrary.dll
        │   │
        │   └───win81
        │           MyImageProcessingLibrary.dll
        │
        └───ref
            ├───net40
            │       MyImageProcessingLibrary.dll
            │
            └───portable-net451-win81
                    MyImageProcessingLibrary.dll
```

Bu örnekte, `ref` dizinlerdeki derlemelerin hepsi aynı olur.

## <a name="runtimes"></a>Zamanları

Çalışma zamanları klasörü, genellikle Işletim sistemi ve CPU mimarisine göre tanımlanan belirli "çalışma zamanları" üzerinde çalışmak için gereken derlemeleri ve yerel kitaplıkları içerir. Bu çalışma zamanları,,, vb. [çalışma zamanı tanımlayıcıları (RID 'ler)](/dotnet/core/rid-catalog) kullanılarak tanımlanır `win` `win-x86` `win7-x86` `win8-64` .

## <a name="native-helpers-to-use-platform-specific-apis"></a>Platforma özgü API 'Leri kullanmak için yerel yardımcılar

Aşağıdaki örnek, birkaç platform için tamamen yönetilen bir uygulamaya sahip olan bir paketi gösterir, ancak Windows 8 ' de Windows 8 ' e özgü yerel API 'lerde çağırabildiği yerel yardımcıları kullanır.

```
└───MyLibrary
        ├───lib
        │   └───net40
        │           MyLibrary.dll
        │
        └───runtimes
            ├───win8-x64
            │   ├───lib
            │   │   └───net40
            │   │           MyLibrary.dll
            │   │
            │   └───native
            │           MyNativeLibrary.dll
            │
            └───win8-x86
                ├───lib
                │   └───net40
                │           MyLibrary.dll
                │
                └───native
                        MyNativeLibrary.dll
```

Yukarıdaki paket verildiğinde aşağıdaki şeyler meydana gelir:

- Windows 8 ' de değilse, `lib/net40/MyLibrary.dll` derleme kullanılır.

- Windows 8 ' de `runtimes/win8-<architecture>/lib/MyLibrary.dll` kullanılır ve `native/MyNativeHelper.dll` derleme çıktısına kopyalanır.

Derlemenin Yukarıdaki örnekte, çalışma `lib/net40` zamanları klasöründeki derlemeler, Windows 8 ' e özgü API 'leri çağırmak için yerel yardımcı derlemeye p/Invoke olarak ayarlanır.

Yalnızca tek bir `lib` klasör çekilir, bu nedenle çalışma zamanına özgü bir klasör varsa, çalışma zamanında özel olmayan bir klasör seçilir `lib` . Yerel klasör, varsa, derleme çıktısına kopyalanır.

## <a name="managed-wrapper"></a>Yönetilen sarmalayıcı

Çalışma zamanlarını kullanmanın başka bir yolu da, yerel bir derleme üzerinde yalnızca yönetilen bir sarmalayıcı olan bir paket göndermektedir. Bu senaryoda, aşağıdaki gibi bir paket oluşturursunuz:

```
└───MyLibrary
        └───runtimes
            ├───win8-x64
            │   ├───lib
            │   │   └───net451
            │   │           MyLibrary.dll
            │   │
            │   └───native
            │           MyImplementation.dll
            │
            └───win8-x86
                ├───lib
                │   └───net451
                │           MyLibrary.dll
                │
                └───native
                        MyImplementation.dll
```

Bu durumda, `lib` ilgili yerel derlemeye bağlı olmayan bu pakette hiçbir uygulama olmadığı için, bu klasörde en üst düzey bir klasör yoktur. Yönetilen derleme, `MyLibrary.dll` her iki durumda da tam olarak aynıysa, bunu en üst düzey klasöre koyabiliriz `lib` , ancak yerel bir derlemenin olmaması, paketin, Win-x86 veya Win-x64 olmayan bir platforma yüklenmişse paketin yükleme başarısız olmasına neden olmadığı için, en üst düzey lib kullanılır ancak hiçbir yerel derleme kopyalanmaz.

## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a>NuGet 2 ve NuGet 3 için yazma paketleri

Çalıştıran projeler tarafından, ve kullanarak paketler tarafından tüketilen bir paket oluşturmak istiyorsanız `packages.config` `project.json` aşağıdakiler geçerlidir:

- Ref ve çalışma zamanları yalnızca NuGet 3 ' te çalışır. Bunlar her ikisi de NuGet 2 tarafından yok sayılır.

- Kullanamazsınız `install.ps1` veya `uninstall.ps1` çalışamaz. Bu dosyalar kullanılırken yürütülür `packages.config` , ancak ile yok sayılır `project.json` . Bu nedenle, paketinizin çalışır duruma girmeden kullanılabilir olması gerekir. `init.ps1` NuGet 3 ' te hala çalışır.

- Hedefler ve props yüklemesi farklıdır, bu nedenle paketinizin her iki istemcide de beklendiği gibi çalıştığından emin olun.

- LIB alt dizinleri NuGet 3 ' te bir TXD olmalıdır. Kitaplıkları klasörün köküne yerleştirebilirsiniz `lib` .

- İçerik NuGet 3 ile otomatik olarak kopyalanmaz. Paketinizin tüketicileri dosyaları kopyalayabilir veya bir görev Çalıştırıcısı gibi bir aracı kullanarak dosyaları kopyalamayı otomatik hale getirebilir.

- Kaynak ve yapılandırma dosyası dönüştürmeleri NuGet 3 tarafından çalıştırılmaz.

NuGet 2 ve 3 ' ü destekliyorsanız, `minClientVersion` paketinizin üzerinde çalıştığından NuGet 2 istemcisinin en düşük sürümü olmanız gerekir. Var olan bir pakette değişiklik olması gerekmez.
