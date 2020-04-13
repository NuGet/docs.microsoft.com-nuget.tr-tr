---
title: NuGet Paketleri için çoklu hedefleme
description: Tek bir NuGet paketinin içinden birden fazla .NET Framework sürümlerini hedefleyen çeşitli yöntemlerin açıklaması.
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: 34f7c6132ba6050e20114642932ccf29a5ec088d
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79429012"
---
# <a name="support-multiple-net-versions"></a>Birden çok .NET sürümü destekleyin

Birçok kitaplık .NET Framework'ün belirli bir sürümünü hedeflemektedir. Örneğin, kitaplığınızın UWP'ye özgü bir sürümü ve .NET Framework 4.6'daki özelliklerden yararlanan başka bir sürümü olabilir. Bunu karşılamak için NuGet, aynı kitaplığın birden çok sürümüne tek bir pakete koymayı destekler.

Bu makalede, paket veya derlemelerin nasıl inşa edildiğine bakılmaksızın bir NuGet paketinin düzeni açıklanır (diğer bir süre önce düzen, birden fazla SDK tarzı olmayan *.csproj* dosyası ve özel bir *.nuspec* dosyası veya tek bir çok hedefli SDK stili *.csproj*kullanarak aynıdır). Bir SDK tarzı proje için, NuGet [paketi hedefleri](../reference/msbuild-targets.md) paketin nasıl döşenmesi gerektiğini bilir ve derlemeleri doğru lib klasörlerine koyarak ve her hedef çerçevesi (TFM) için bağımlılık grupları oluşturmayı otomatikleştirir. Ayrıntılı yönergeler için [proje dosyanızdaki birden çok .NET Framework sürümüne](multiple-target-frameworks-project-file.md)bakın.

[Paket Oluşturma'da](../create-packages/creating-a-package.md#from-a-convention-based-working-directory)açıklanan kural tabanlı çalışma dizini yöntemini kullanırken paketi bu makalede açıklandığı şekilde el ile oluşturmanız gerekir. SDK tarzı bir proje için otomatik yöntem önerilir, ancak paketi bu makalede açıklandığı şekilde el ile birlikte vermeyi de seçebilirsiniz.

## <a name="framework-version-folder-structure"></a>Çerçeve sürüm klasör yapısı

Kitaplığın yalnızca bir sürümünü içeren veya birden çok çerçeveyi hedef alan bir `lib` paket oluştururken, her zaman aşağıdaki kuralı içeren farklı büyük/küçük harf duyarlı çerçeve adlarını kullanarak alt klasörler oluşturursunuz:

    lib\{framework name}[{version}]

Desteklenen adların tam listesi için [Hedef Çerçeveler başvurusuna](../reference/target-frameworks.md#supported-frameworks)bakın.

Kitaplığın bir çerçeveye özgü olmayan ve doğrudan kök `lib` klasörüne yerleştirilen bir sürümü olmamalıdır. (Bu özellik yalnızca ile `packages.config`desteklenmiştir). Bunu yapmak, kitaplığı herhangi bir hedef çerçeveyle uyumlu hale getirecek ve herhangi bir yere yüklenmesini sağlayarak beklenmeyen çalışma zamanı hatalarına neden olur. Kök klasöre (örneğin) `lib\abc.dll`veya alt klasörlere (örneğin) `lib\abc\abc.dll`derleme ler eklemek amortismana kaldırıldı ve PackagesReference biçimini kullanırken yoksayılıyor.

Örneğin, aşağıdaki klasör yapısı çerçeveye özgü bir derlemenin dört sürümü destekler:

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

Paketi kurarken tüm bu dosyaları kolayca eklemek için aşağıdaki `**` bölüme `<files>` özyinelemeli `.nuspec`bir joker karakter kullanın:

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a>Mimariye özel klasörler

Mimariye özgü derlemeler, yani ARM, x86 ve x64'ü hedefleyen ayrı derlemeler varsa, `runtimes` bunları alt klasörler `{platform}-{architecture}\lib\{framework}` `{platform}-{architecture}\native`içinde adı verilen bir klasöre yerleştirmeniz gerekir veya . Örneğin, aşağıdaki klasör yapısı, Windows 10'u ve çerçeveyi `uap10.0` hedefleyen hem yerel hem de yönetilen DL'leri barındırır:

    \runtimes
        \win10-arm
            \native
            \lib\uap10.0
        \win10-x86
            \native
            \lib\uap10.0
        \win10-x64
            \native
            \lib\uap10.0

Bu derlemeler yalnızca çalışma zamanında kullanılabilir, bu nedenle ilgili derleme zaman derlemesini `AnyCPU` sağlamak `/ref/{tfm}` istiyorsanız klasörde derleme niz de vardır. 

Lütfen unutmayın, NuGet her zaman bu derleme veya çalışma zamanı varlıklarını tek `/ref` bir `/lib` klasörden seçer, bu nedenle o zamana kadar uyumlu varlıklar varsa derleme zamanı derlemeleri eklemek için göz ardı edilecektir. Benzer şekilde, o zaman bazı `/runtimes` uyumlu `/lib` varlıklar varsa da çalışma süresi için yoksayılır.

Bu dosyaları bildirimde başvurmak için [UWP Paketleri](../guides/create-uwp-packages.md) `.nuspec` Oluştur'a bakın.

Ayrıca, Bkz. [NuGet ile Windows mağazası uygulama bileşeni paketleme](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2)

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a>Bir projedeki montaj sürümlerini ve hedef çerçeveyi eşleştirme

NuGet birden çok derleme sürümü olan bir paket yüklediğinde, derlemenin çerçeve adını projenin hedef çerçevesiyle eşleştirmeye çalışır.

Bir eşleşme bulunamazsa, NuGet varsa, projenin hedef çerçevesinden daha az veya projenin hedef çerçevesine eşit olan en yüksek sürüm için derlemeyi kopyalar. Uyumlu derleme bulunamazsa, NuGet uygun bir hata iletisi döndürür.

Örneğin, bir pakette aşağıdaki klasör yapısını göz önünde bulundurun:

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

Bu paketi .NET Framework 4.6'yı hedefleyen bir projeye yüklerken, `net45` NuGet derlemeyi klasöre yükler, çünkü bu 4,6'dan daha az veya eşit olan kullanılabilir sürümdür.

Proje .NET Framework 4.6.1'i hedefliyorsa, diğer taraftan, NuGet derlemeyi `net461` klasöre yükler.

Proje .NET framework 4.0 ve daha öncesini hedefliyorsa, NuGet uyumlu derlemeyi bulamadığı için uygun bir hata iletisi atar.

## <a name="grouping-assemblies-by-framework-version"></a>Derlemeleri çerçeve sürümüne göre gruplandırma

NuGet, paketteki tek bir kitaplık klasöründen derlemeleri kopyalar. Örneğin, bir paketin aşağıdaki klasör yapısına sahip olduğunu varsayalım:

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

Paket .NET Framework 4.5'i hedefleyen bir projeye `MyAssembly.dll` yüklendiğinde, (v2.0) yüklenen tek derlemedir. `MyAssembly.Core.dll``net45` (v1.0) klasörde listelenmediği için yüklenmez. NuGet bu şekilde işlemktedir, çünkü `MyAssembly.Core.dll` sürüm 2.0'da `MyAssembly.dll`birleştirilmiş olabilir.

.NET `MyAssembly.Core.dll` Framework 4.5 için yüklü olmak istiyorsanız, bir `net45` kopyasını klasöre yerleştirin.

## <a name="grouping-assemblies-by-framework-profile"></a>Derlemeleri çerçeve profiline göre gruplandırma

NuGet ayrıca, bir tire ve profil adını klasörün sonuna ekleyerek belirli bir çerçeve profilini hedeflemeyi de destekler.

    lib\{framework name}-{profile}

Desteklenen profiller aşağıdaki gibidir:

- `client`: Müşteri Profili
- `full`: Tam Profil
- `wp`: Windows Phone
- `cf`: Kompakt Çerçeve

## <a name="declaring-dependencies-advanced"></a>Bağımlılıkları bildirme (Gelişmiş)

Bir proje dosyasını paketlerken, NuGet projedeki bağımlılıkları otomatik olarak oluşturmaya çalışır. Bağımlılıkları bildirmek için *.nuspec* dosyası kullanma yla ilgili bu bölümdeki bilgiler genellikle yalnızca gelişmiş senaryolar için gereklidir.

*(Sürüm 2.0+)* Öğe içindeki `<group>` `<dependencies>` öğeleri kullanarak hedef projenin hedef çerçevesine karşılık gelen *.nuspec'teki* paket bağımlılıklarını bildirebilirsiniz. Daha fazla bilgi için [bağımlılıklar öğesine](../reference/nuspec.md#dependencies-element)bakın.

Her grubun adında `targetFramework` bir özniteliği vardır `<dependency>` ve sıfır veya daha fazla öğe içerir. Hedef çerçeve projenin çerçeve profiliyle uyumlu olduğunda bu bağımlılıklar birlikte yüklenir. Tam çerçeve tanımlayıcıları için [Hedef çerçevelerine](../reference/target-frameworks.md) bakın.

*Lib/* ve *ref/* klasörlerdeki dosyalar için Hedef Çerçeve Moniker (TFM) başına bir grup kullanmanızı öneririz.

Aşağıdaki örnek, öğenin `<group>` farklı varyasyonlarını gösterir:

```xml
<dependencies>

    <group targetFramework="net472">
        <dependency id="jQuery" version="1.10.2" />
        <dependency id="WebActivatorEx" version="2.2.0" />
    </group>

    <group targetFramework="net20">
    </group>

</dependencies>
```

## <a name="determining-which-nuget-target-to-use"></a>Hangi NuGet hedefini kullanacağını belirleme

Taşınabilir Sınıf Kitaplığı'nı hedefleyen kitaplıkları paketlemekitaplarını klasör adlarınızda ve `.nuspec` dosyanızda kullanmanız gereken NuGet hedefini belirlemek zor olabilir, özellikle de PCL'nin yalnızca bir alt kümesini hedefliyorsanız. Aşağıdaki dış kaynaklar bu size yardımcı olacaktır:

- [.NET 'deki çerçeve profilleri](https://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephencleary.com)
- [Taşınabilir Sınıf Kitaplığı profilleri](https://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): PCL profillerini ve eşdeğernu NuGet hedeflerini tablo yakan
- [Taşınabilir Sınıf Kitaplığı profilleri aracı](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): sisteminizde bulunan PCL profillerini belirlemek için komut satırı aracı

## <a name="content-files-and-powershell-scripts"></a>İçerik dosyaları ve PowerShell komut dosyaları

> [!Warning]
> Mutable içerik dosyaları ve komut `packages.config` dosyası yürütme yalnızca biçimi ile kullanılabilir; diğer tüm biçimlerle birlikte amortismana alınır ve yeni paketler için kullanılmamalıdır.

Ile, `packages.config`içerik dosyaları ve PowerShell komut dosyaları hedef çerçeve ve `content` `tools` klasörler içinde aynı klasör kuralı kullanılarak gruplandırılabilir. Örneğin:

    \content
        \net46
            \MyContent.txt
        \net461
            \MyContent461.txt
        \uap
            \MyUWPContent.html
        \netcore
    \tools
        init.ps1
        \net46
            install.ps1
            uninstall.ps1
        \uap
            install.ps1
            uninstall.ps1

Bir çerçeve klasörü boş bırakılırsa, NuGet derleme başvuruları veya içerik dosyaları eklemez veya bu çerçeve için PowerShell komut dosyalarını çalıştırmaz.

> [!Note]
> Çözüm `init.ps1` düzeyinde yürütüldüğünden ve `tools` projeye bağlı değil, doğrudan klasörün altına yerleştirilmesi gerekir. Bir çerçeve klasörü altına yerleştirilirse yoksayılır.
