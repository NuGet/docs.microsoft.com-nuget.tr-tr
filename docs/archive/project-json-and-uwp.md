---
title: NuGet project.json dosyasını içeren UWP projeleri
description: Project.json dosyasını NuGet bağımlılıklarını Evrensel Windows Platformu (UWP) projelerindeki izlemek için nasıl kullanıldığını açıklaması.
author: karann-msft
ms.author: karann
ms.date: 07/17/2017
ms.topic: conceptual
ms.openlocfilehash: ac3c137dd0ba50571737093eef11c8ab0ef932b2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548670"
---
# <a name="projectjson-and-uwp"></a>Project.JSON ve UWP

> [!Important]
> Bu içerik kullanım dışı bırakılmıştır. Projeleri ya da kullanması gereken `packages.config` veya PackageReference biçimleri.

Bu belge, özellikleri NuGet 3 + (Visual Studio 2015 veya üzeri) kullanır paket yapısını açıklar. `minClientVersion` Özelliği, `.nuspec` 3.1 için ayarlayarak burada açıklanan özellikler ihtiyacınız olan durum için kullanılabilir.

## <a name="adding-uwp-support-to-an-existing-package"></a>Var olan bir pakete eklenirken podpora UWP

Var olan bir paket varsa ve UWP uygulamaları için desteği eklemek istiyorsanız, burada açıklanan paketleme biçimini benimseyin gerekmez. Tanımlar ve yalnızca NuGet istemci sürümüne 3 + güncelleştirilmiş istemciler çalışmak istediğiniz özellikler gerektiriyorsa, bu biçim benimsemek yeterlidir.

## <a name="i-already-target-netcore45"></a>Ben zaten netcore45 hedef

Hedefliyorsanız `netcore45` zaten ve özelliklerden burada yapmanız gerekmez, Eylem gerekmiyor. `netcore45` paketleri UWP uygulamaları tarafından kullanılabilir.

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a>Windows 10 özel API'ların yararlanmak istiyorum

Bu durumda, eklemeniz gereken `uap10.0` hedef çerçeve adı (TFM veya TxM) paketi. Paketiniz yeni bir klasör oluşturun ve bu klasöre Windows 10 ile çalışmak için derlenmiş bütünleştirilmiş kod ekleyin.

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a>Windows 10 özel API'ler, ihtiyacınız yoktur, ancak yeni .NET özellikleri istediğiniz veya netcore45 yoksa

Bu durumda, eklediğiniz `dotnet` TxM paketi. Diğer TxMs aksine `dotnet` yüzey veya platform açık değil. Bu, paket bağımlılıklarınızı üzerinde çalışan herhangi bir platformda çalışan belirten olur. Sahip bir paket oluştururken `dotnet` TxM, büyük olasılıkla pek çok daha fazla TxM özel bağımlılıklar vardır uygulamanızın `.nuspec`, gibi bağımlı BCL paketleri tanımlamak gerek duyduğunuz `System.Text`, `System.Xml`vb. Burada paketinizi çalışır, bu bağımlılıkların çalıştığı konumları tanımlayın.

### <a name="how-do-i-find-out-my-dependencies"></a>Bağımlılıkların nasıl bulabilirim

Listelemek için hangi bağımlılıkların anlamak için iki yolu vardır:

1. Kullanım [NuSpec bağımlılık Oluşturucu](https://github.com/onovotny/ReferenceGenerator) **3. taraf** aracı. Aracı işlemini ve güncelleştirmeleri otomatikleştirir, `.nuspec` derlemede bağımlı paketlerin dosya. Bir NuGet paketi kullanılabilir [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).

1. (Zor olan yolu) Kullanım `ILDasm` bakmak için `.dll` hangi derlemeleri çalışma zamanında gerçekten gerekli olup olmadığını görmek için. Ardından gelir her hangi bir NuGet paketi belirler.

Bkz: [ `project.json` ](project-json.md) destekleyen bir paketin oluşturmaya yardımcı olan özellikler hakkında ayrıntılı bilgi için konu `dotnet` TxM.

> [!Important]
> Paketiniz PCL projeleri ile kullanılmak üzere tasarlanmış, yüksek oranda oluşturmak için önerilir bir `dotnet` uyarıları ve olası uyumluluk sorunları önlemek için klasör.

## <a name="directory-structure"></a>Dizin yapısı

NuGet paketlerini şu biçimi kullanarak aşağıdaki bilinen bir klasörü ve davranışları vardır:

| Klasör | Davranışlar |
| --- | --- |
| Derleme | İçeren MSBuild hedeflerini ve özellik dosyalarını bu klasöre projeye farklı şekilde tümleştirilir, ancak Aksi halde bir değişiklik yoktur. |
| Araçlar | `install.ps1` ve `uninstall.ps1` çalıştırılamaz. `init.ps1` her zaman olduğu gibi çalışır. |
| İçerik | İçeriği bir kullanıcının projesine otomatik olarak kopyalanır değil. Sonraki bir sürümü için içerik ekleme projedeki desteği planlanmaktadır. |
| lib | Birçok paketler için `lib` Nuget'te yaptığı aynı şekilde çalışan 2.x, ancak hangi adları için genişletilmiş seçenekler ile kullanılabilir ve daha iyi mantıksal paketleri tüketildiğinde doğru alt klasörü seçmek için. Ancak, birlikte kullanıldığında `ref`, `lib` klasörünü içeren derlemeler tarafından tanımlanan yüzey uygulayan derlemeler `ref` klasör. |
| başvuru | `ref` genel tanımlama .NET derlemelerini içeren isteğe bağlı bir klasördür karşı derleme olanağı, bir uygulama için surface (Genel türleri ve yöntemleri). Bu klasör derlemelerde uygulaması bulunmuyor, bunlar tamamen derleyici yüzey alanını tanımlamak için kullanılır. Paket Hayır varsa `ref` klasörü, ardından `lib` başvuru bütünleştirilmiş kodu hem uygulama derleme. |
| Çalışma zamanları | `runtimes` CPU mimarisi ve işletim sistemi belirli veya başka türlü platforma bağımlı ikili dosyalar gibi belirli işletim sistemi kodu içeren bir isteğe bağlı bir klasördür. |

## <a name="msbuild-targets-and-props-files-in-packages"></a>MSBuild hedeflerini ve özellik dosyalarını paketler

NuGet paketlerini içerebilir `.targets` ve `.props` içine paketinin yüklü olduğu herhangi bir MSBuild Projesi içeri aktarılan dosyaları. Nuget'te 2.x, bu silme işleminin ekleyerek `<Import>` açıklamaalarını `.csproj` dosya, NuGet 3.0 özel "Kurulum" projesi için bir eylem yok. Bunun yerine paket geri yükleme işlemi iki dosyalarını Yazar `[projectname].nuget.props` ve `[projectname].NuGet.targets`.

MSBuild, bu iki dosyaları aramak için bilir ve başlangıcı yakınında ve proje derleme işleminin sonunda otomatik olarak alır. Bu çok benzer bir davranış için NuGet sağlar 2.x, ancak temel farklardan biri: *yoktur yürütülme sırası belirli hedefleri/özellik dosyaları bu durumda*. MSBuild yolu sipariş hedeflere sağlar ancak `BeforeTargets` ve `AfterTargets` özniteliklerini `<Target>` tanımı (bkz [hedef öğe (MSBuild)](/visualstudio/msbuild/target-element-msbuild).

## <a name="lib-and-ref"></a>LIB ve başvuru

Davranışını `lib` klasörü henüz değiştirilen önemli ölçüde NuGet v3 sürümünde. Ancak, tüm derlemelerin bir TxM sonra alt klasörleri içinde olmalıdır ve artık doğrudan altında yerleştirilebilir `lib` klasör. Bir TxM bir paket içinde belirli bir varlık için iş geç bir platform adıdır. Mantıksal bir uzantı hedef çerçeve bilinen adlar (TFM) Örneğin bunlar `net45`, `net46`, `netcore50`, ve `dnxcore50` TxMs tüm örnekleri (bkz [hedef çerçeve](../reference/target-frameworks.md). TxM bir çerçeve (TFM) yanı sıra diğer platforma özgü yüzey alanlarına başvurabilirsiniz. Örneğin UWP TxM (`uap10.0`) UWP uygulamaları için Windows yüzey alanını yanı sıra .NET yüzey alanını temsil eder.

Bir örnek LIB yapısı:

    lib
    ├───net40
    │       MyLibrary.dll
    └───wp81
            MyLibrary.dll

`lib` Klasörü, çalışma zamanında kullanılan derlemeleri içerir. En altında bir klasör paketleri `lib` her hedef TxMs gerekli olan tüm için.

## <a name="ref"></a>başvuru

Bazı durumlarda farklı bir derleme (.NET başvuru derlemeleri yapın bu Bugün) derleme sırasında burada kullanılması gereken durumlar da vardır. Bu gibi durumlarda adlı en üst düzey bir klasör kullanan `ref` (kısaltması "başvuru bütünleştirilmiş kodlarını").

Çoğu paket yazarlarının gerektirmeyen `ref` klasör. Derleme ve IntelliSense için tutarlı bir yüzey alanını sağlar ancak ardından farklı TxMs için farklı bir uygulama için gereksinim paketlerin için kullanışlıdır. Bu olan büyük kullanım örneği `System.*` sevkiyat .NET Core NuGet üzerindeki bir parçası olarak oluşturulan paketler. Bu paketler, ref derlemelerin tutarlı bir kümesini birleşik çeşitli uygulamalara sahip.

Derlemeleri mekanik olarak, dahil `ref` klasörü olduğu için derleyici geçirilen başvuru bütünleştirilmiş kodları. Biz için kaçı derlemeleri olanlar csc.exe kullanmış için bunlar [C# / Reference seçeneği](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) geçin.

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

Bu örnekte derlemelerde `ref` dizinleri tüm aynı olması.

## <a name="runtimes"></a>Çalışma zamanları

Çalışma zamanları klasörü, derlemeleri ve "genellikle işletim sistemi ve CPU mimarisine göre tanımlanan özel çalışma zamanları", üzerinde çalıştırmak için gerekli yerel kitaplıkları içerir. Bu çalışma zamanları kullanılarak tanımlanır [çalışma zamanı tanımlayıcılarının (RID'ler)](/dotnet/core/rid-catalog) gibi `win`, `win-x86`, `win7-x86`, `win8-64`vb.

## <a name="native-helpers-to-use-platform-specific-apis"></a>Platforma özel API'leri kullanmak için yerel Yardımcıları

Aşağıdaki örnek, çeşitli platformlar için tamamen yönetilen bir uygulamasını var, ancak Windows 8'i Windows 8 özgü yerel API'lere burada çağırabilirsiniz yerel Yardımcıları kullanan bir paket gösterir.

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

- Windows 8'de ne zaman `lib/net40/MyLibrary.dll` derleme kullanılır.

- Windows 8 ne zaman `runtimes/win8-<architecture>/lib/MyLibrary.dll` kullanılır ve `native/MyNativeHelper.dll` yapı çıkışını kopyalanır.

Yukarıdaki örnekte `lib/net40` derlemedir, tamamen yönetilen kod, Windows 8 özel API'leri çağırmak için yerel Yardımcısı derlemesini p/Invoke derlemeler çalışma zamanları klasöründe olacaktır artırabileceksiniz.

Yalnızca tek bir `lib` klasör olduğu hiç olmadığı kadar olması Çekildi, çalışma zamanı belirli bir klasöre ise çalışma zamanı olmayan özel seçilir şekilde `lib`. Yerel klasör, varsa eklenebilir, yapı çıkışını kopyalanır.

## <a name="managed-wrapper"></a>Yönetilen sarmalayıcı

Çalışma zamanı kullanmak için başka bir yerel bir derleme üzerinde tamamen yönetilen bir sarmalayıcı olan bir paket göndermeye yoludur. Bu senaryoda aşağıdaki gibi bir paket oluşturun:

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

Bu durumda olduğu en üst düzey `lib` klasördür orada olarak bu klasör olarak hiçbir uygulama bu paketinin karşılık gelen yerel derleme üzerinde içermez. Yönetilen bütünleştirilmiş kod `MyLibrary.dll`, biz bunu bir üst düzey yerleştirebilirsiniz sonra tam olarak her iki durumda aynı olan `lib` klasörü, ancak yerel bir derleme eksikliği paket bir platformda yüklediyseniz yükleme başarısız olmasına neden olmaz, Win-x86 veya win x64 üst düzey LIB kullanılır ancak hiçbir yerel derleme kopyalanacak değildi.

## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a>NuGet 2 ve 3 NuGet paketleri yazma

Kullanarak projeleri tarafından kullanılabilen bir paket oluşturmak istiyorsanız `packages.config` de olarak paketleri kullanarak `project.json` sonra aşağıdaki Uygula:

- Yalnızca ref ve çalışma zamanları NuGet 3'te çalışır. Bunlar her ikisi de NuGet 2 tarafından yoksayılır.

- Üzerinde güvenemezsiniz `install.ps1` veya `uninstall.ps1` işlevi. Bu dosyaları kullanırken yürütmek `packages.config`, ile göz ardı edilir ancak `project.json`. Paketiniz onlar olmadan kullanılabilir olması gerekir çalışıyor. `init.ps1` yine de NuGet 3'te çalışır.

- Hedeflerini ve özellik yükleme farklıdır, bu nedenle paketinizi hem de istemcilerde beklendiği gibi çalıştığından emin olun.

- LIB alt dizinleri NuGet 3'te bir TxM olması gerekir. Kitaplıkları kökünde yerleştirilemiyor `lib` klasör.

- İçeriği NuGet 3 ile otomatik olarak kopyalanır değil. Tüketiciler paketinizin, dosyaları kopyalayın veya dosyaları kopyalama otomatikleştirmek için görev Çalıştırıcı gibi bir araç kullanın.

- Kaynak ve yapılandırma dosyası dönüşümleri NuGet 3 ile çalışmaz.

NuGet 2 ve 3 destekleniyorsa sonra `minClientVersion` paketinizi çalışır NuGet 2 istemci en düşük sürümü olmalıdır. Söz konusu olduğunda var olan bir paketi bunu değiştirmeniz gerekmez.
