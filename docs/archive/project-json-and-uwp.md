---
title: UWP projeleri ile NuGet project.json dosyası
description: Universal Windows Platform (UWP) projelerindeki NuGet bağımlılıklarını izlemek için project.json dosyasının nasıl kullanıldığının açıklaması.
author: karann-msft
ms.author: karann
ms.date: 07/17/2017
ms.topic: conceptual
ms.openlocfilehash: ac3c137dd0ba50571737093eef11c8ab0ef932b2
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64494365"
---
# <a name="projectjson-and-uwp"></a>project.json ve UWP

> [!Important]
> Bu içerik amortismana hazırdır. Projeler `packages.config` de PackageReference biçimlerini kullanmalıdır.

Bu belge, NuGet 3+ (Visual Studio 2015 ve sonrası) özellikleri kullanan paket yapısını açıklar. Özelliğiniz, `minClientVersion` `.nuspec` burada açıklanan özelliklere 3.1 olarak ayarlayarak ihtiyaç duyduğunuzu belirtmek için kullanılabilir.

## <a name="adding-uwp-support-to-an-existing-package"></a>Varolan bir pakete UWP desteği ekleme

Varolan bir paketiniz varsa ve UWP uygulamaları için destek eklemek istiyorsanız, burada açıklanan ambalaj biçimini benimsemeniz gerekmez. Yalnızca açıkladığı özelliklere ihtiyaç duyuyorsanız ve yalnızca NuGet istemcisinin sürüm 3+ sürümüne güncelleştirilmiş istemcilerle çalışmak istiyorsanız bu biçimi benimsemeniz gerekir.

## <a name="i-already-target-netcore45"></a>Zaten netcore45 hedef

Zaten hedef `netcore45` alırsanız ve buradaki özelliklerden yararlanmanız gerekmiyorsa, herhangi bir işlem yapmanız gerekmez. `netcore45`paketleri UWP uygulamaları tarafından tüketilebilir.

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a>Windows 10'a özgü API'lerden yararlanmak istiyorum

Bu durumda, hedef çerçeve `uap10.0` takma aparatı (TFM veya TxM) paketinize eklemeniz gerekir. Paketinizde yeni bir klasör oluşturun ve Windows 10 ile çalışmak üzere derlenen derlemeyi bu klasöre ekleyin.

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a>Windows 10 özel API'ler gerekmez, ama yeni .NET özellikleri istiyorum ya da netcore45 zaten yok

Bu durumda, TxM'yi `dotnet` paketinize eklersiniz. Diğer TxM'lerden farklı olarak, `dotnet` bir yüzey alanı veya platform anlamına gelmez. Paketinizin bağımlılıklarınızın üzerinde çalıştığı herhangi bir platformda çalıştığını belirtir. `dotnet` TxM ile bir paket inşa ederken, size bağlı BCL paketleri tanımlamak `.nuspec`için gereken gibi, çok daha fazla TxM özgü bağımlılıkları olması muhtemeldir, vb. `System.Text` `System.Xml` Bu bağımlılıkların üzerinde çalıştığı konumlar paketinizin nerede çalıştığını tanımlar.

### <a name="how-do-i-find-out-my-dependencies"></a>Bağımlılıklarımı nasıl öğrenebilirim?

Hangi bağımlılıkların listelenemeye ne kadar yol olduğunu anlamanın iki yolu vardır:

1. [NuSpec Bağımlılık Jeneratörü](https://github.com/onovotny/ReferenceGenerator) **3.** Araç işlemi otomatikleştirir ve `.nuspec` dosyanızı yapıdaki bağımlı paketlerle güncelleştirir. Bir NuGet paketi, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/)üzerinden kullanılabilir.

1. (Zor yol) Çalışma `ILDasm` zamanında hangi `.dll` derlemelerin gerçekten gerekli olduğunu görmek için bakmak için kullanın. Ardından, her birinin hangi NuGet paketinden geldiğini belirleyin.

TxM'yi destekleyen bir paketin oluşturulmasına yardımcı olan özellikler le ilgili ayrıntılar için [`project.json`](project-json.md) konuya bakın. `dotnet`

> [!Important]
> Paketiniz PCL projeleri ile çalışmak üzere tasarlanmıştırsa, `dotnet` uyarılardan ve olası uyumluluk sorunlarını önlemek için bir klasör oluşturmanızı şiddetle öneririz.

## <a name="directory-structure"></a>Dizin yapısı

Bu biçimi kullanan NuGet paketleri aşağıdaki iyi bilinen klasöre ve davranışlara sahiptir:

| Klasör | Davranışlar |
| --- | --- |
| Yapı | Bu klasördeki MSBuild hedefleri ve sahne dosyaları projeye farklı olarak entegre edilmiştir, ancak aksi takdirde değişiklik yoktur. |
| Araçlar | `install.ps1`ve `uninstall.ps1` çalıştırılmayız. `init.ps1`her zaman olduğu gibi çalışır. |
| İçerik | İçerik otomatik olarak kullanıcının projesine kopyalanmaz. Projeye içerik ekleme desteğinin daha sonra yayınlanması planlanmaktadır. |
| Lib | Birçok paket `lib` için NuGet 2.x'te olduğu gibi çalışır, ancak içinde hangi adların kullanılabileceğinin genişletilmiş seçenekleri ve paketleri tüketirken doğru alt klasörü seçmek için daha iyi bir mantık la çalışır. Ancak, klasör ile `ref`birlikte `lib` kullanıldığında, `ref` klasör klasördeki derlemeler tarafından tanımlanan yüzey alanını uygulayan derlemeler içerir. |
| Referans | `ref`karşı derlemek için bir uygulama için ortak yüzeyi (genel türleri ve yöntemleri) tanımlayan .NET derlemeleri içeren isteğe bağlı bir klasördür. Bu klasördeki derlemeler hiçbir uygulama olabilir, onlar tamamen derleyici için yüzey alanı tanımlamak için kullanılır. Paketin klasörü `ref` yoksa, hem `lib` başvuru derlemesi hem de uygulama derlemesi olur. |
| Çalıştırma | `runtimes`CPU mimarisi ve işletim sistemi belirli veya başka bir platforma bağımlı ikililer gibi işletim sistemi özgü kodu içeren isteğe bağlı bir klasördür. |

## <a name="msbuild-targets-and-props-files-in-packages"></a>MSBuild dosyaları paketler halinde hedefler ve sahne

NuGet paketleri, `.targets` `.props` paketin yüklü olduğu herhangi bir MSBuild projesine içe aktarılan dosyaları ve dosyaları içerebilir. NuGet 2.x'te bu durum `<Import>` dosyaya `.csproj` ekstreler enjekte edilerek yapıldı, NuGet 3.0'da belirli bir "projeye yükleme" eylemi yoktur. Bunun yerine paket geri `[projectname].nuget.props` yükleme `[projectname].NuGet.targets`işlemi iki dosya yazar ve .

MSBuild bu iki dosyayı aramayı ve bunları proje oluşturma sürecinin başlangıcına ve sonuna yakın otomatik olarak içe aktarmayı bilir. Bu NuGet 2.x çok benzer bir davranış sağlar, ancak büyük bir fark ile: *Bu durumda hedef / sahne dosyaları nın garantili bir sırası yoktur.* Ancak, `BeforeTargets` MSBuild `AfterTargets` `<Target>` tanımı ve öznitelikleri ile hedefleri sipariş etmek için yollar sağlar [(Bkz. Hedef Öğesi (MSBuild)](/visualstudio/msbuild/target-element-msbuild).

## <a name="lib-and-ref"></a>Lib ve Ref

NuGet v3'te klasörün `lib` davranışı önemli ölçüde değişmedi. Ancak, tüm derlemeler TxM'den sonra adlandırılan alt klasörlerde olmalıdır ve artık `lib` doğrudan klasörün altına yerleştirilememelidir. TxM, paketteki belirli bir varlığın çalışması gereken bir platformun adıdır. Mantıksal olarak bunlar Hedef Çerçeve Monikers 'in (TFM) `net45` `net46`bir `netcore50`uzantısıdır, örneğin, , , ve `dnxcore50` Tüm TxM örnekleridir (Bkz. [Hedef Çerçeveler.](../reference/target-frameworks.md) TxM bir çerçeve (TFM) yanı sıra diğer platforma özgü yüzey alanları başvurabilirsiniz. Örneğin UWP TxM`uap10.0`( ) UWP uygulamaları için Windows yüzey alanının yanı sıra .NET yüzey alanını da temsil eder.

Bir örnek lib yapısı:

    lib
    ├───net40
    │       MyLibrary.dll
    └───wp81
            MyLibrary.dll

Klasör, `lib` çalışma zamanında kullanılan derlemeleri içerir. Çoğu paket için `lib` hedef TxM'lerin her biri için altında bir klasör gereklidir.

## <a name="ref"></a>Referans

Derleme sırasında farklı bir derlemenin kullanılması gereken durumlar bazen vardır (.NET Başvuru Derlemeleri bunu bugün yapar). Bu gibi durumlarda, ("Başvuru `ref` Derlemeleri"nin kısaltması) adlı üst düzey bir klasör kullanın.

Çoğu paket yazarı klasörü `ref` gerektirmez. Derleme ve IntelliSense için tutarlı bir yüzey alanı sağlaması gereken ancak daha sonra farklı TxM'ler için farklı bir uygulamaya sahip paketler için yararlıdır. Bunun en büyük kullanım `System.*` örneği NuGet'de .NET Core taşımacılığının bir parçası olarak üretilen paketlerdir. Bu paketler, tutarlı bir ref derlemeleri kümesi tarafından birleştirilmiş olan çeşitli uygulamalara sahiptir.

Mekanik olarak, `ref` klasörde yer alan derlemeler derleyiciye geçirilen başvuru derlemeleridir. CSC.exe kullananlar için bunlar [C# /reference option](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) switch'e aktardığımız montajlardır.

Klasörün `ref` yapısı, örneğin aşağıdakiyle `lib`aynıdır:

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

Bu örnekte dizinlerde `ref` derlemeler tüm özdeş olacaktır.

## <a name="runtimes"></a>Çalıştırma

Runtimes klasörü, genellikle İşletim Sistemi ve CPU mimarisi tarafından tanımlanan belirli "çalışma zamanlarında" çalışması için gereken derlemeleri ve yerel kitaplıkları içerir. Bu çalışma süreleri [Runtime Tanımlayıcıları (RIDs)](/dotnet/core/rid-catalog) gibi `win`, `win-x86`, `win7-x86` `win8-64`, , vb kullanılarak tanımlanır.

## <a name="native-helpers-to-use-platform-specific-apis"></a>Platforma özgü API'leri kullanmak için yerel yardımcılar

Aşağıdaki örnek, çeşitli platformlar için tamamen yönetilen bir uygulamaya sahip, ancak Windows 8'e özgü yerel API'leri arayabildiği Windows 8'de yerel yardımcıları kullanan bir paketi gösterir.

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

Yukarıdaki paket göz önüne alındığında aşağıdaki şeyler olur:

- Windows 8'de `lib/net40/MyLibrary.dll` olmadığında derleme kullanılır.

- Windows 8'de `runtimes/win8-<architecture>/lib/MyLibrary.dll` kullanıldığında ve `native/MyNativeHelper.dll` yapınızın çıktısına kopyalanır.

Yukarıdaki örnekte `lib/net40` derleme tamamen yönetilen kod iken, runtimes klasöründeki derlemeler Windows 8'e özgü API'leri çağırmak için yerel yardımcı derlemeye başvurur.

Yalnızca tek `lib` bir klasör seçilir, bu nedenle çalışma zamanı belirli bir klasör varsa, `lib`çalışma zamanı olmayan belirli bir klasör seçilir. Yerel klasör katkı maddesidir, varsa yapının çıktısına kopyalanır.

## <a name="managed-wrapper"></a>Yönetilen sarıcı

Çalışma sürelerini kullanmanın başka bir yolu da, tamamen yerel bir derleme üzerinde yönetilen bir ambalaj olan bir paketi sevk etmektir. Bu senaryoda aşağıdaki gibi bir paket oluşturursunuz:

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

Bu durumda, ilgili yerel `lib` derlemeye dayanmayan bu paketin uygulanması olmadığı için, bu klasör olarak üst düzey klasör yoktur. Yönetilen derleme, `MyLibrary.dll`, her iki durumda da tam olarak aynı olsaydı o `lib` zaman bir üst düzey klasöre koyabilirsiniz, ancak bir yerel derleme eksikliği bir paket win-x86 veya win-x64 sonra üst düzey lib kullanılan ama hiçbir yerel derleme kopyalanmış olsaydı yükleme başarısız olmasına neden olmaz çünkü.

## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a>NuGet 2 ve NuGet 3 için yazma paketleri

Aşağıdakileri kullanarak `packages.config` paketlerin yanı sıra projeler tarafından da tüketilebilen bir paket oluşturmak istiyorsanız aşağıdakileri uygulayın: `project.json`

- Ref ve çalışma süreleri yalnızca NuGet 3'te çalışır. Her ikisi de NuGet 2 tarafından göz ardı edilir.

- Buna `install.ps1` güvenemezsiniz `uninstall.ps1` ya da çalışamazsınız. Bu dosyalar kullanırken `packages.config`yürütülür, ancak . `project.json` Bu nedenle paketinizin onlar çalışmadan kullanılabilir olması gerekir. `init.ps1`hala NuGet 3'te çalışır.

- Hedefler ve Sahne Yüklemesi farklıdır, bu nedenle paketinizin her iki istemcide de beklendiği gibi çalıştığından emin olun.

- Lib alt dizinleri NuGet 3'te bir TxM olmalıdır. Kitaplıkları `lib` klasörün köküne yerleştiremezsiniz.

- İçerik NuGet 3 ile otomatik olarak kopyalanmaz. Paketinizin tüketicileri dosyaları kendileri kopyalayabilir veya dosyaları kopyalamayı otomatikleştirmek için görev koşucusu gibi bir araç kullanabilir.

- Kaynak ve config dosya dönüşümleri NuGet 3 tarafından çalıştırılmez.

NuGet 2 ve 3'ü destekliyorsanız, paketinizin üzerinde çalıştığı NuGet 2 istemcisinin en düşük sürümü `minClientVersion` olmalıdır. Varolan bir paket söz konusu olduğunda, bu paketin değişmesi gerekmez.
