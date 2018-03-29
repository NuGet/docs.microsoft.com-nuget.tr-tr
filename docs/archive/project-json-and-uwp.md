---
title: NuGet project.json dosyası UWP projeleri | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 07/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Evrensel Windows Platformu (UWP) projelerinde NuGet bağımlılıkları izlemek için project.json dosyasına nasıl kullanıldığı açıklaması.
keywords: NuGet bağımlılıkları, NuGet ve UWP, UWP ve project.json, NuGet project.json dosyası
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 453a38456670db850d3d2845b23bd4ad36fc8fd2
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="projectjson-and-uwp"></a>Project.JSON ve UWP

> [!Important]
> Bu içerik kullanım dışı bırakılmıştır. Projeleri ya da kullanması gereken `packages.config` veya PackageReference biçimleri.

Bu belge NuGet 3 + özelliklerinde (2015 ve sonraki Visual Studio) kullanan paket yapısını açıklar. `minClientVersion` Özelliği, `.nuspec` için 3.1 ayarlayarak burada açıklanan özellikleri gerektirir durum için kullanılabilir.

## <a name="adding-uwp-support-to-an-existing-package"></a>Varolan paketini UWP desteği ekleme

Var olan bir paket varsa ve UWP uygulamalar için destek eklemek istediğiniz, burada açıklanan paketleme biçimine uyar gerekmez. Yalnızca özelliklerini açıklar ve NuGet istemci sürümüne 3 + güncelleyen istemcileri ile çalışma konusunda istekli gerekiyorsa bu biçim benimsemeyi gerekir.

## <a name="i-already-target-netcore45"></a>I zaten netcore45 hedef

Hedefliyorsanız `netcore45` zaten ve özelliklerinden burada yapmanıza gerek yoktur, Eylem gerekmiyor. `netcore45` paketleri UWP uygulamaları tarafından kullanılabilecek.

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a>Windows 10 özel API'leri yararlanmak istiyorum

Bu durumda, eklemeniz gerekir `uap10.0` framework bilinen ad (TFM veya TxM) paketiniz için hedef. Paketinize yeni bir klasör oluşturun ve bu klasöre Windows 10 ile çalışmak için derlenmiş derleme ekleyin.

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a>Windows 10 özel API'leri, gerek yoktur, ancak yeni .NET özellikleri istediğiniz veya netcore45 zaten yok

Bu durumda, eklediğiniz `dotnet` TxM paketiniz için. Diğer TxMs aksine `dotnet` yüzey alanını ya da platform anlamına değil. Bu, paketinizi bağımlılıklarınızı çalıştığı herhangi bir platformda çalışan belirten olur. Olan bir paket oluştururken `dotnet` TxM, pek çok daha fazla TxM özgü bağımlılıkları vardır büyük olasılıkla, `.nuspec`gibi bağımlı BCL paketleri tanımlamanız gibi `System.Text`, `System.Xml`vb. Bu bağımlılıklar çalıştığı konumlarını paketinizi çalıştığı tanımlayın.

### <a name="how-do-i-find-out-my-dependencies"></a>My bağımlılıkları nasıl bulabilirim

Listelemek için hangi bağımlılıkları bulmak için iki yolu vardır:

1. Kullanım [NuSpec bağımlılık Oluşturucu](https://github.com/onovotny/ReferenceGenerator) **3. taraf** aracı. Aracı işlemi ve güncelleştirmeleri otomatikleştirir, `.nuspec` yapı bağımlı paketleriyle dosyada. Bir NuGet paketi kullanılabilir [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).

1. (Sabit yolu) Kullanım `ILDasm` bakmak için `.dll` hangi derlemelerin çalışma zamanında gerçekten gerekli olan görmek için. Sonra her geliyor hangi NuGet paketi belirleyin.

Bkz: [ `project.json` ](project-json.md) destekleyen bir paket oluşturulmasında yardımcı olan özellikler hakkında ayrıntılı bilgi için konu `dotnet` TxM.

> [!Important]
> Paketinizi PCL projelerle çalışmak için amaçlanıyorsa oluşturmak için öneririz bir `dotnet` uyarılar ve olası uyumluluk sorunları önlemek için klasör.

## <a name="directory-structure"></a>Dizin yapısı

NuGet paketlerini bu biçimi kullanarak aşağıdaki bilinen klasör ve davranışları vardır:

| Klasör | Davranışlar |
| --- | --- |
| Derleme | MSBuild içeren hedefleri ve özellik dosyalarını bu klasöre farklı projeye tümleşik ancak Aksi halde değişiklik yoktur. |
| Araçlar | `install.ps1` ve `uninstall.ps1` çalıştırılamaz. `init.ps1` her zaman olduğu gibi çalışır. |
| İçerik | İçeriği otomatik olarak bir kullanıcının projeye kopyalanmaz. Projedeki içerik ekleme desteği için sonraki bir sürümü planlanmaktadır. |
| Lib | Çoğu paketlere ilişkin `lib` NuGet içinde mevcut aynı şekilde çalışır 2.x, ancak hangi adları için genişletilmiş seçenekleriyle kullanılabilir ve daha iyi mantığı içinde doğru alt klasörü paketler kullanırken çekme. Ancak, ile birlikte kullanıldığında `ref`, `lib` klasörde derlemelerde tarafından tanımlanan yüzey alanını uygulamak derlemeler `ref` klasör. |
| Ref | `ref` Ortak tanımlama .NET derlemelerini içeren bir isteğe bağlı klasördür karşı derlemek bir uygulama için yüzey (Genel türleri ve yöntemleri). Bu klasör derlemelerde uygulaması olabilir, bunlar tamamen derleyici yüzey alanını tanımlamak için kullanılır. Paket Hayır varsa `ref` klasörü, sonra `lib` referans derlemesini ve uygulaması derleme. |
| Çalışma zamanları | `runtimes` CPU mimarisi ve işletim sistemi belirli veya başka türlü platforma bağımlı ikili dosyaları gibi belirli işletim sistemi kodu içeren bir isteğe bağlı klasördür. |

## <a name="msbuild-targets-and-props-files-in-packages"></a>MSBuild hedefleri ve özellik dosyalarını paketler

NuGet paketlerini içerebilir `.targets` ve `.props` paket içine yüklenir herhangi MSBuild proje içeri aktarılan dosyalar. NuGet içinde 2.x, bu yapıldı ekleyerek `<Import>` deyimleri `.csproj` dosya, NuGet 3. 0'belirli "projesine yükleme" eylemi yok. Bunun yerine paket geri yükleme işlemi iki dosya Yazar `[projectname].nuget.props` ve `[projectname].NuGet.targets`.

MSBuild için bu iki dosyayı aramak için bilir ve başına yakın ve proje oluşturma işlemi sona otomatik olarak alır. Bu Nuget'e çok benzer bir davranış sağlar 2.x, ancak temel farklardan biri ile: *var. hedefler/özellik dosyaları yok garantili sırası bu durumda*. MSBuild yolu sipariş hedefleri ancak sunar `BeforeTargets` ve `AfterTargets` özniteliklerini `<Target>` tanımı (bkz [hedef öğesi (MSBuild)](/visualstudio/msbuild/target-element-msbuild).

## <a name="lib-and-ref"></a>LIB ve Ref

Davranışını `lib` klasörü kurmadı değiştirilen önemli ölçüde NuGet v3. Ancak, tüm derlemelerde bir TxM sonra adlı alt klasörler içinde olmalıdır ve artık doğrudan altında yerleştirilebilir `lib` klasör. Bir TxM bir paketteki belirli bir varlık için iş gerektiği bir platform adıdır. Mantıksal bir uzantı hedef Framework adlar (TFM) Örneğin bunlar `net45`, `net46`, `netcore50`, ve `dnxcore50` TxMs tüm örnekleri (bkz [hedef çerçeveyi](../reference/target-frameworks.md). TxM bir çerçeve (TFM) yanı sıra diğer platforma özgü yüzey alanlara başvurabilir. Örneğin UWP TxM (`uap10.0`) UWP uygulamaları Windows yüzey alanını yanı sıra .NET yüzey alanını temsil eder.

Bir örnek lib yapısı:

    lib
    ├───net40
    │       MyLibrary.dll
    └───wp81
            MyLibrary.dll

`lib` Klasörü çalışma zamanında kullanılan derlemelerini içerir. Çoğu için paketler altında bir klasör `lib` her hedef TxMs gerekli olan tüm için.

## <a name="ref"></a>Ref

Bazı durumlarda farklı bir derleme (.NET başvuru derlemeleri do bu Bugün) derleme sırasında nerede kullanılması gereken durumlar vardır. Bu gibi durumlarda adlı bir üst düzey klasör kullanmak `ref` (kısaltması "başvuru derlemeleri").

Çoğu paketi yazarları gerektirmeyen `ref` klasör. Derleme ve IntelliSense için tutarlı bir yüzey alanını sağlar ancak farklı TxMs için farklı uygulama olması gereken paketleri için kullanışlıdır. Bu öğeler büyük kullanım örneği `System.*` sevkiyat .NET Core NuGet üzerinde bir parçası olarak oluşturulan paketler. Bu paketleri ref derlemelerin tutarlı bir kümesini birleşik çeşitli uygulamaları sahiptir.

Derlemeleri mekanik olarak, dahil `ref` klasöründe derleyiciye geçirilen başvuru derlemeleri alır. Biz geçirme için derlemeler için olanlar csc.exe kullanmış olduğunuz bunlar [C# / Reference seçeneği](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) geçin.

Yapısını `ref` klasördür aynı `lib`, örneğin:

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

Bu örnekte derlemelerde `ref` dizinler tüm olacaktır aynı.

## <a name="runtimes"></a>Çalışma zamanları

Çalışma zamanları klasör derlemeler ve "işletim sistemi ve CPU mimarisine göre genellikle tanımlanmış olan belirli çalışma zamanları", üzerinde çalıştırmak için gerekli yerel kitaplıkları içerir. Bu çalışma zamanları kullanılarak tanımlanır [çalışma zamanı tanımlayıcıları (RID)](/dotnet/core/rid-catalog) gibi `win`, `win-x86`, `win7-x86`, `win8-64`vb.

## <a name="native-helpers-to-use-platform-specific-apis"></a>Platforma özgü API'ları kullanmak için yerel Yardımcıları

Aşağıdaki örnek, çeşitli platformlar için tamamen yönetilen bir uygulama olsa da, Windows 8'i Windows 8 özgü yerel API burada çağırabilirsiniz yerel Yardımcıları kullanan bir paket gösterir.

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

Yukarıdaki paket aşağıdakiler gerçekleşir:

- Windows 8'deki ne zaman `lib/net40/MyLibrary.dll` derleme kullanılır.

- Windows 8 ne zaman `runtimes/win8-<architecture>/lib/MyLibrary.dll` kullanılır ve `native/MyNativeHelper.dll` yapınızın çıkışına kopyalanır.

Yukarıdaki örnekte `lib/net40` derlemedir tamamen yönetilen kod, Windows 8 özel API'leri çağırmak için yerel Yardımcısı derlemesini p/Invoke çalışma zamanları klasörü derlemelerde olacak adımında.

Yalnızca tek bir `lib` klasör olan herhangi bir zamanda olması Çekildi, çalışma zamanı belirli bir klasörde ise çalışma zamanı olmayan özel seçilir şekilde `lib`. Yerel klasör, varsa ADDITIVE yapı çıkışına kopyalanır.

## <a name="managed-wrapper"></a>Yönetilen sarmalayıcı

Çalışma zamanları kullanmak için başka bir yerel derleme tamamen yönetilen sarmalayıcı bir paket dağıtmayı yoludur. Bu senaryoda aşağıdaki gibi bir paket oluşturun:

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

Bu durumda olduğundan en üst düzey `lib` klasördür orada olarak bu klasör olarak hiçbir uygulama karşılık gelen yerel derleme üzerinde kullanmaz bu paketi. Yönetilen derleme `MyLibrary.dll`, biz bu bir üst düzey koyabilirsiniz sonra tam olarak her iki durumda aynı olan `lib` klasörü, ancak yerel derleme eksikliği paket bir platformda yüklenmişse, yükleme başarısız olmasına neden değil, Win-x86 veya win x64 en üst düzey lib kullanılır, ancak yerel derleme kopyalanır sonra değildi.

## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a>NuGet 2 ve 3 NuGet paketleri yazma

Kullanarak projeleri tarafından kullanılabilecek bir paket oluşturmak isteyip istemediğinizi `packages.config` de olarak paketleri kullanarak `project.json` sonra aşağıdaki Uygula:

- Ref ve çalışma zamanları yalnızca NuGet 3'te çalışır. NuGet 2 ile hem de yoksayılır.

- Bağlı olamaz `install.ps1` veya `uninstall.ps1` işlevi. Bu dosyaları kullanırken yürütme `packages.config`, ile göz ardı edilir, ancak `project.json`. Paketinizi onlar olmadan kullanılabilir olması gereken şekilde çalışıyor. `init.ps1` hala NuGet 3'te çalışır.

- Hedefleri ve özellik yükleme farklıdır, bu nedenle paketinizi hem de istemcilerde beklendiği gibi çalıştığından emin olun.

- LIB alt dizinleri TxM NuGet 3 olmalıdır. Kitaplıkları kökünde yerleştirilemiyor `lib` klasör.

- İçerik NuGet 3 ile otomatik olarak kopyalanmaz. Tüketiciler, paketi, dosyaları kendileri kopyalama veya dosyaları kopyalanıyor otomatikleştirmek için görev Çalıştırıcı gibi bir araç kullanın.

- Kaynak ve yapılandırma dosyası dönüşümler NuGet 3 ile çalışmaz.

NuGet 2 ve 3 destekleniyorsa sonra `minClientVersion` paketinizi çalışır NuGet 2 istemci en düşük sürümü olmalıdır. Var olan bir paket olması durumunda onu değiştirmeniz gerekmez.
