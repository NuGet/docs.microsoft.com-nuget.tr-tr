---
title: "Çoklu sürüm desteği için NuGet paketleri | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 09/27/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Tek bir NuGet paketi birden çok .NET Framework sürümü hedeflemek için çeşitli yöntemler açıklaması."
keywords: "NuGet paketi, NuGet ve .NET, .NET Framework sürümleri hedefleme hedefleme çoklu çerçevelerine, NuGet paketi oluşturma"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 723dbcc12ecc4e16d2ba4662559f107b9b22e2c2
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/14/2018
---
# <a name="supporting-multiple-net-framework-versions"></a>Birden çok .NET framework sürümleri destekleme

*NuGet 4.0 + kullanarak .NET Core projeleri için bkz: [NuGet paketi ve geri yükleme MSBuild hedefleri olarak](../reference/msbuild-targets.md) arası hedefleme hakkında ayrıntılı bilgi için.*

Birçok kitaplıkları belirli bir .NET Framework sürümünü hedefleyin. Örneğin, kitaplığınızın UWP için belirli bir sürüm ve .NET Framework 4.6 özelliklerinden yararlanır başka bir sürümü olabilir.

Bu, açıklanan kurala dayalı çalışma dizini yöntemi kullanırken, tek bir pakette aynı kitaplığı birden fazla sürümünü koyma NuGet destekler uyum sağlayacak şekilde [paket oluşturma](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).

## <a name="framework-version-folder-structure"></a>Framework'te sürüm klasör yapısı

Bir kitaplık veya hedef yalnızca bir sürümü içeren bir paket birden çok çerçeveyi oluştururken, her zaman klasörleriyle yaptığınız `lib` farklı büyük/küçük harfe framework adları ile aşağıdaki kural kullanılarak:

    lib\{framework name}[{version}]

Desteklenen ad tam bir listesi için bkz: [hedef çerçeveyi başvuru](../reference/target-frameworks.md#supported-frameworks).

Hiçbir zaman bir çerçeve özgüdür ve doğrudan kök olarak yerleştirilen kitaplığı bir sürümüne sahip olmalıdır `lib` klasör. (Bu özellik yalnızca destekleniyordu `packages.config`). Ve tüm hedef framework ile uyumlu hale olması izin verin Bunun yapılması her yerden, büyük olasılıkla beklenmeyen çalışma zamanı hataları kaynaklanan yüklü. Kök klasöründe derlemeler ekleme (gibi `lib\abc.dll`) veya alt klasörlerinde (gibi `lib\abc\abc.dll`) kullanım dışı bırakıldı ve PackagesReference biçimi kullanılırken göz ardı edilir.

Örneğin, aşağıdaki klasör yapısını bir derlemeyi çerçeveye özel dört sürümlerini destekler:

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

Bu dosyalar paket oluştururken kolayca eklemek için bir özyinelemeli kullanın `**` joker karakter olarak `<files>` bölümü, `.nuspec`:

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a>Mimariye özel klasörler

Mimariye özel derlemeler, diğer bir deyişle, ARM, hedef x 86 ve x64, ayrı derlemeler varsa bunları adlı bir klasörde yerleştirmelisiniz `runtimes` adlı alt klasörlerdeki `{platform}-{architecture}\lib\{framework}` veya `{platform}-{architecture}\native`. Örneğin, aşağıdaki klasör yapısını Windows 10 hedefleme yerel ve yönetilen DLL'leri kapsayan ve `uap10.0` framework:

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

Bkz: [UWP paketleri oluşturmak](../guides/create-uwp-packages.md) bu dosyalarda başvuran bir örnek için `.nuspec` bildirimi.

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a>Derleme sürümlerini ve bir proje hedef çerçevesi eşleştirme

NuGet birden çok derleme sürümü olan bir paketi yüklendiğinde, projenin hedef çerçevesini derlemenin framework adla eşleşecek şekilde çalışır.

Bir eşleşme bulunmazsa, NuGet projenin hedef çerçevesi eşit veya daha az kullanılabilir ise en yüksek sürüm için derleme kopyalar. Uyumlu derleme bulunursa, NuGet uygun bir hata iletisi döndürür.

Örneğin, bir paketi aşağıdaki klasör yapısındaki göz önünde bulundurun:

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

.NET Framework 4.6 hedefleyen bir projede bu paket yükleme sırasında derlemede NuGet yükler `net45` klasörü, 4.6 küçük veya buna eşit olan en yüksek kullanılabilir olduğu için.

Diğer taraftan, projeniz .NET Framework 4.6.1 hedefliyorsa, derlemede NuGet yükler `net461` klasör.

Projeniz .NET framework 4.0 ve önceki hedefliyorsa, NuGet uyumlu derleme paylaşımın için uygun bir hata iletisi oluşturur.

## <a name="grouping-assemblies-by-framework-version"></a>Framework sürümüne göre gruplandırma derlemeler

NuGet yalnızca tek kitaplığı klasöründe paket derlemeleri kopyalar. Örneğin, bir paketi aşağıdaki klasör yapısını olduğunu varsayın:

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

.NET Framework 4. 5'i hedefleyen bir projede paketi yüklendiğinde `MyAssembly.dll` (v2.0) yalnızca derlemesinin yüklü olmalıdır. `MyAssembly.Core.dll` (v1.0) içinde listelenmediğinden yüklü değil `net45` klasör. NuGet, çünkü bu şekilde davranır `MyAssembly.Core.dll` sürümüne 2.0 birleştirilmiş sahip `MyAssembly.dll`.

İsterseniz `MyAssembly.Core.dll` için .NET Framework 4.5 yüklü olması için bir kopyasını koyun `net45` klasör.

## <a name="grouping-assemblies-by-framework-profile"></a>Derlemeleri framework profile göre gruplandırma

NuGet, bir tire ve profil adı klasörü sonuna ekleyerek belirli framework profili hedefleme de destekler.

    lib\{framework name}-{profile}

Desteklenen profiller aşağıdaki gibidir:

- `client`: İstemci profili
- `full`: Tam profili
- `wp`: Windows Phone
- `cf`: Compact Framework

## <a name="determining-which-nuget-target-to-use"></a>Kullanmak için hangi NuGet hedef belirleme

Ne zaman hedefleyen taşınabilir sınıf kitaplığı paketleme kitaplıkları olabilir, klasör adlarında kullandığınız hangi NuGet hedef belirlemek hassas ve `.nuspec` , özellikle yalnızca bir alt kümesini PCL hedefleme dosyası. Aşağıdaki dış kaynaklara bu yardımcı olur:

- [.NET Framework profillerinde](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)
- [Taşınabilir sınıf kitaplığı profilleri](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Tablo PCL profilleri ve eşdeğer NuGet hedeflerine numaralandırma
- [Taşınabilir sınıf kitaplığı profilleri aracı](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com'u): PCL belirlemek için komut satırı aracı sisteminizde profilleri

## <a name="content-files-and-powershell-scripts"></a>İçerik dosyaları ve PowerShell betikleri

> [!Warning]
> Değişebilir içerik dosyaları ve komut dosyası yürütme ile kullanılabilir `packages.config` yalnızca biçimini; diğer biçimlere kullanım dışıdır ve herhangi bir yeni paket kullanılmamalıdır.

İle `packages.config`, içeriği içinde aynı klasörü kuralını kullanarak hedef framework tarafından dosyaları ve PowerShell komut dosyaları gruplandırılabilir `content` ve `tools` klasörler. Örneğin:

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

Bir çerçeve klasörünün boş bırakılırsa, NuGet değil derleme başvurusu veya içerik dosyası ekleyin veya bu çerçevesi için PowerShell komut dosyasını çalıştırın.

> [!Note]
> Çünkü `init.ps1` yürütülür düzeyi ve proje bağımlı çözüm için bunu doğrudan altında yerleştirilmelidir `tools` klasör. Bir çerçeve klasörünün yerleştirilmiş durumunda yoksayılır.
