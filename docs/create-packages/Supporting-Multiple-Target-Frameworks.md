---
title: NuGet paketleri için çoklu sürüm desteği
description: Tek bir NuGet paketi birden çok .NET Framework sürümlerini hedeflemek için çeşitli yöntemler açıklaması.
author: karann-msft
ms.author: karann
ms.date: 09/27/2017
ms.topic: conceptual
ms.openlocfilehash: a755438c1f63d33271f636cb663cc5b51a5aecbc
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324818"
---
# <a name="supporting-multiple-net-framework-versions"></a>Birden çok .NET framework sürümleri destekleme

*NuGet 4.0 + kullanarak .NET Core projeleri için bkz: [NuGet paketi ve geri yükleme, MSBuild hedefleri](../reference/msbuild-targets.md) çapraz hedefleme hakkında ayrıntılı bilgi için.*

Birçok kitaplıkları belirli bir .NET Framework sürümünü hedefler. Örneğin, kitaplığınıza UWP için belirli bir sürümünü ve .NET Framework 4. 6'içinde özelliklerinden yararlanır başka bir sürümü olabilir.

Bu, birden çok sürümünü aynı kitaplığı tek bir paket içinde açıklanan dayanan çalışma dizini yöntemi kullanılırken koyarak NuGet destekler uyum sağlayacak şekilde [paket oluşturma](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).

## <a name="framework-version-folder-structure"></a>Framework sürümü klasör yapısı

Her zaman tek bir kitaplığı veya hedef sürümünü içeren bir paket birden çok çerçeveyi oluştururken, alt yapmanız `lib` farklı büyük/küçük harfe framework adları ile aşağıdaki kural kullanılarak:

    lib\{framework name}[{version}]

Desteklenen adlarının tam bir listesi için bkz. [hedef çerçeve başvurusu](../reference/target-frameworks.md#supported-frameworks).

Hiçbir zaman doğrudan kök yerleştirilmiştir ve bir çerçeve özel değil kitaplığı sürümünü olmalıdır `lib` klasör. (Bu özellik yalnızca desteklenen `packages.config`). Bunun yapılması kitaplığı herhangi bir hedef çerçevesi ile uyumlu hale getirmek ve her yerden yüklenmesi için büyük olasılıkla beklenmeyen çalışma zamanı hatalarıyla kaynaklanan izin. Derleme kök klasöründe ekleme (gibi `lib\abc.dll`) veya alt klasörleri (gibi `lib\abc\abc.dll`) kullanım dışı bırakıldı ve PackagesReference biçimi kullanılırken göz ardı edilir.

Örneğin, aşağıdaki klasör yapısına çerçeveye özgü dört derleme sürümlerini destekler:

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

Bu dosyalar paket oluştururken kolayca dahil etmek için bir özyinelemeli kullanın `**` joker karakterin `<files>` bölümünü, `.nuspec`:

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a>Mimariye özel klasörler

Mimariye özel derlemeler, diğer bir deyişle, ARM, x 86 ve x64, hedef ayrı derlemeler varsa bunları adlı bir klasörde yerleştirmelisiniz `runtimes` alt klasörleri içinde `{platform}-{architecture}\lib\{framework}` veya `{platform}-{architecture}\native`. Örneğin, Windows 10 hedefleyen yerel ve yönetilen DLL'leri aşağıdaki klasör yapısına kapsayan ve `uap10.0` framework:

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

Böylece karşılık gelen sağlamak istiyorsanız derleme zamanı derlemesi de sonra bu derlemeler yalnızca çalışma zamanında kullanılabilir `AnyCPU` derlemede `/ref{tfm}` klasör. 

Lütfen unutmayın, NuGet her zaman seçer bu derleme veya çalışma zamanı varlıklar bir klasörden bunu uyumlu bazı varlıklarından varsa `/ref` ardından `/lib` derleme zamanı derlemeleri eklemek için yok sayılacak. Benzer şekilde, bazı uyumlu varlıklarından varsa `/runtime` aynı zamanda `/lib` için çalışma zamanı yok sayılacak.

Bkz: [UWP paketleri oluşturma](../guides/create-uwp-packages.md) içinde bu dosyaları başvuran bir örnek için `.nuspec` bildirimi.

Ayrıca bkz [bir Windows mağazası uygulama bileşeni NuGet ile paketleme](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2)

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a>Eşleşen derleme sürümlerini ve hedef Framework'ü bir projedeki

NuGet birden çok bütünleştirilmiş kod sürümü olan bir paketi yüklendiğinde, derlemenin framework adı projenin hedef çerçevesi ile eşleştirmeyi dener.

Bir eşleşme bulunmazsa, NuGet derleme varsa ya da projenin hedef çerçevesi eşit olan en yüksek sürüm için kopyalar. Uyumlu hiçbir derleme tespit edilirse, NuGet uygun bir hata iletisi döndürür.

Örneğin, bir paket içinde aşağıdaki klasör yapısına göz önünde bulundurun:

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

Bu paket, .NET Framework 4.6 hedefleyen bir proje içinde yüklerken, NuGet derleme içinde yükler `net45` klasöründe, 4.6 küçük veya ona eşit olan en yüksek kullanılabilir olduğu.

Öte yandan, projenin hedeflediği .NET Framework 4.6.1, NuGet derleme içinde yükler `net461` klasör.

Projenin hedeflediği .NET framework 4.0 ve daha önceki NuGet uyumlu bütünleştirilmiş bulma değil için uygun bir hata iletisi oluşturur.

## <a name="grouping-assemblies-by-framework-version"></a>Framework sürümüne göre gruplandırma derlemeleri

NuGet paketinde yalnızca tek kitaplığı klasör derlemeleri kopyalar. Örneğin, bir paketi aşağıdaki klasör yapısına olduğunu varsayın:

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

.NET Framework 4.5 hedefleyen bir proje içinde paketi yüklendiğinde `MyAssembly.dll` (v2.0) yüklü tek bir derleme olduğundan. `MyAssembly.Core.dll` içinde listelenmediğinden (v1.0) yüklü değil `net45` klasör. NuGet, çünkü bu şekilde davranır `MyAssembly.Core.dll` sürümüne 2.0 birleştirilmiş `MyAssembly.dll`.

İsterseniz `MyAssembly.Core.dll` .NET Framework 4.5 için yüklenecek bir kopyasını yerleştirmek `net45` klasör.

## <a name="grouping-assemblies-by-framework-profile"></a>Derlemeleri framework profile göre gruplandırma

NuGet, tire ve profil adına klasörü sonuna ekleyerek belirli framework profili hedefleyen da destekler.

    lib\{framework name}-{profile}

Desteklenen profilleri aşağıdaki gibidir:

- `client`: İstemci profili
- `full`: Tam profil
- `wp`: Windows Phone
- `cf`: Compact Framework'te

## <a name="determining-which-nuget-target-to-use"></a>Kullanmak için hangi NuGet hedef belirleme

Ne zaman taşınabilir sınıf kitaplığı hedefleyen paketleme kitaplıkları olabilir hangi NuGet hedef klasör adlarınızı kullanmanız gerektiğini belirlemek zor ve `.nuspec` , özellikle de yalnızca bir alt kümesini PCL hedefleyen dosyası. Aşağıdaki dış kaynaklar bu konuda yardımcı olur:

- [.NET Framework profillerinde](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephencleary.com)
- [Taşınabilir sınıf kitaplığı profilleri](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): PCL profilleri ile eşdeğer NuGet hedeflerine numaralandırma tablo
- [Taşınabilir sınıf kitaplığı profilleri aracı](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): PCL belirlemek için komut satırı aracını sisteminizde kullanılabilir profiller

## <a name="content-files-and-powershell-scripts"></a>İçerik dosyaları ve PowerShell betikleri

> [!Warning]
> Mutable içerik dosyaları ve komut dosyası yürütme bulunan `packages.config` yalnızca biçimini; sahip diğer biçimlere kullanım dışıdır ve yeni tüm paketler için kullanılmamalıdır.

İle `packages.config`, içeriği içinde aynı klasör kuralı kullanarak hedef Framework'ü göre dosyaları ve PowerShell betiklerini gruplandırılabilir `content` ve `tools` klasörleri. Örneğin:

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

Çerçeve klasörü boş bırakılırsa, NuGet derleme başvuruları veya içerik dosyalarını eklemek değil veya bu çerçeve için PowerShell betikleri çalıştırın.

> [!Note]
> Çünkü `init.ps1` yürütülür çözüm düzeyinde ve proje bağımlı olmayan, bunu doğrudan altında yerleştirilmelidir `tools` klasör. Bir çerçeve klasörü altında yerleştirdiyseniz göz ardı edilir.
