---
title: NuGet paketleri için Çoklu hedefleme
description: Tek bir NuGet paketinin içinden birden çok .NET Framework sürümünü hedeflemek için çeşitli yöntemlerin açıklaması.
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: 7c0da38ab4059b89c9693ecbece2bc8ed1a775ec
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237951"
---
# <a name="support-multiple-net-versions"></a>Çoklu .NET sürümlerini destekler

Birçok kitaplık .NET Framework belirli bir sürümünü hedefleyin. Örneğin, kitaplıkınızın, UWP 'e özgü bir sürümüne ve .NET Framework 4,6 ' deki özelliklerden yararlanan başka bir sürüme sahip olabilirsiniz. NuGet buna uyum sağlamak için, aynı kitaplığın birden çok sürümünü tek bir pakette yerleştirmeyi destekler.

Bu makalede, paketin veya derlemelerin nasıl oluşturulduğuna bakılmaksızın bir NuGet paketinin düzeni açıklanmaktadır (yani, düzen birden çok SDK olmayan *. csproj* dosyası ve özel bir *. nuspec* dosyası ya da tek bir çok hedefli SDK stili *. csproj* ) kullanmanın yanı sıra, düzen aynı olur. Bir SDK stili proje için, NuGet [paketi](../reference/msbuild-targets.md) , paketin nasıl oluşturulması gerektiğini bilir ve derlemeleri doğru lib klasörlerine yerleştirmeyi ve her hedef çerçeve (tfd) için bağımlılık grupları oluşturmayı otomatikleştirir. Ayrıntılı yönergeler için bkz. [proje dosyanızdaki çoklu .NET Framework sürümlerini destekleme](multiple-target-frameworks-project-file.md).

[Paket oluşturma](../create-packages/creating-a-package.md#from-a-convention-based-working-directory)bölümünde açıklanan kural tabanlı çalışma dizini yöntemi kullanılırken bu makalede açıklandığı gibi paketi el ile oluşturmanız gerekir. SDK stili bir proje için otomatik yöntem önerilir, ancak paketi bu makalede açıklandığı gibi el ile düzenlemek de tercih edebilirsiniz.

## <a name="framework-version-folder-structure"></a>Framework sürüm klasörü yapısı

Bir kitaplığın yalnızca bir sürümünü içeren veya birden çok çerçeveyi hedefleyen bir paket oluştururken, her zaman `lib` aşağıdaki kurala sahip farklı büyük/küçük harf duyarlı çerçeve adları kullanarak alt klasörler yaparsınız:

    lib\{framework name}[{version}]

Desteklenen adların tüm listesi için bkz. [hedef çerçeveler başvurusu](../reference/target-frameworks.md#supported-frameworks).

Bir çerçeveye özgü olmayan ve doğrudan kök klasöre yerleştirilebilecek bir kitaplığın sürümüne sahip olmanız gerekir `lib` . (Bu özellik yalnızca ile desteklenir `packages.config` ). Bunu yapmak, kitaplığı herhangi bir hedef çerçeve ile uyumlu hale getirir ve büyük olasılıkla beklenmedik çalışma zamanı hatalarına neden olur. Derlemeleri kök klasöre (gibi `lib\abc.dll` ) veya alt klasörlere (gibi) eklemek `lib\abc\abc.dll` kullanım dışı bırakılmıştır ve PackagesReference biçimi kullanılırken yok sayılır.

Örneğin, aşağıdaki klasör yapısı çerçeveye özgü bir derlemenin dört sürümünü destekler:

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

Paketi oluştururken tüm bu dosyaları kolayca dahil etmek için, ' `**` ın bölümünde özyinelemeli bir joker karakter kullanın `<files>` `.nuspec` :

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a>Mimariye özgü klasörler

Mimariye özgü derlemeleriniz, yani ARM, x86 ve x64 'u hedefleyen ayrı derlemeler varsa, bunları `runtimes` veya adlı alt klasörler içindeki adlı bir klasöre yerleştirmeniz gerekir `{platform}-{architecture}\lib\{framework}` `{platform}-{architecture}\native` . Örneğin, aşağıdaki klasör yapısı, Windows 10 ve Framework 'ü hedefleyen hem yerel hem de yönetilen DLL 'Leri kapsayabilmelidir `uap10.0` :

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

Bu derlemeler yalnızca çalışma zamanında kullanılabilir. bu nedenle, ilgili derleme zamanı derlemesini ve sonra da klasöründe derlemeye sahip olmak istiyorsanız `AnyCPU` `/ref/{tfm}` . 

Lütfen NuGet bu derleme veya çalışma zamanı varlıklarını her zaman bir klasörden seçer, bundan sonra bazı uyumlu varlıklar varsa `/ref` `/lib` derleme zamanı derlemelerini eklemek için yok sayılır. Benzer şekilde, öğesinden bazı uyumlu varlıklar varsa, `/runtimes` `/lib` çalışma zamanı için de yok sayılır.

Bildirimde bu dosyalara başvurma örneği için bkz. [UWP paketleri oluşturma](../guides/create-uwp-packages.md) `.nuspec` .

Ayrıca bkz. [NuGet Ile Windows Mağazası uygulama bileşeni paketleme](/archive/blogs/mim/packaging-a-windows-store-apps-component-with-nuget-part-2)

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a>Bir projede derleme sürümlerini ve hedef Framework 'ü eşleştirme

NuGet birden çok derleme sürümüne sahip bir paket yüklediğinde, derlemenin çerçeve adını projenin hedef çerçevesiyle eşleştirmeye çalışır.

Bir eşleşme bulunmazsa, NuGet derlemeyi, varsa projenin hedef çerçevesine eşit veya daha küçük olan en yüksek sürüm için kopyalar. Uyumlu derleme bulunamazsa, NuGet uygun bir hata iletisi döndürür.

Örneğin, bir pakette aşağıdaki klasör yapısını göz önünde bulundurun:

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

Bu paketi, .NET Framework 4,6 ' i hedefleyen bir projeye yüklerken, `net45` en yüksek kullanılabilir sürüm 4,6 ' e eşit veya daha düşük olan en yüksek sürüm olan NuGet, derlemeyi klasöre yüklüyor.

Proje .NET Framework 4.6.1 hedefliyorsa, diğer yandan NuGet, derlemeyi `net461` klasörüne yüklenir.

Proje, .NET Framework 4,0 ve öncesini hedefliyorsa, NuGet uyumlu derlemeyi bulmayan uygun bir hata iletisi oluşturur.

## <a name="grouping-assemblies-by-framework-version"></a>Derlemeleri Framework sürümüne göre gruplandırma

NuGet, derlemeleri yalnızca paketteki tek bir kitaplık klasöründen kopyalar. Örneğin, bir paketin aşağıdaki klasör yapısına sahip olduğunu varsayalım:

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

Paket, .NET Framework 4,5 ' i hedefleyen bir projeye yüklendiğinde, `MyAssembly.dll` (v 2.0) yüklü tek derleme olur. `MyAssembly.Core.dll` (v 1.0) klasöründe listelenmediğinden yüklenmedi `net45` . NuGet bu şekilde davranır çünkü `MyAssembly.Core.dll` sürüm 2,0 ' de birleştirilmiş olabilir `MyAssembly.dll` .

`MyAssembly.Core.dll`.NET Framework 4,5 için yüklemek istiyorsanız, klasöre bir kopya yerleştirin `net45` .

## <a name="grouping-assemblies-by-framework-profile"></a>Derlemeleri çerçeve profiline göre gruplandırma

NuGet Ayrıca, klasörün sonuna bir tire ve profil adı ekleyerek belirli bir çerçeve profilinin hedeflenmesini destekler.

    lib\{framework name}-{profile}

Desteklenen profiller şunlardır:

- `client`: İstemci profili
- `full`: Tam profil
- `wp`: Windows Phone
- `cf`: Compact Framework

## <a name="declaring-dependencies-advanced"></a>Bağımlılıkları bildirme (Gelişmiş)

Bir proje dosyası paketleme sırasında, NuGet otomatik olarak projeden bağımlılıkları oluşturmaya çalışır. Bağımlılıkları bildirmek için bir *. nuspec* dosyası kullanma hakkında bu bölümdeki bilgiler genellikle yalnızca gelişmiş senaryolar için gereklidir.

*(Sürüm 2.0 +)* Öğesi içindeki öğeleri kullanarak hedef projenin hedef çerçevesine karşılık gelen *. nuspec* içinde paket bağımlılıklarını bildirebilirsiniz `<group>` `<dependencies>` . Daha fazla bilgi için bkz. [Dependencies öğesi](../reference/nuspec.md#dependencies-element).

Her grup adlı bir özniteliğe sahiptir `targetFramework` ve sıfır veya daha fazla `<dependency>` öğe içerir. Hedef Framework, projenin çerçeve profiliyle uyumlu olduğunda bu bağımlılıklar birlikte yüklenir. Tam çerçeve tanımlayıcıları için bkz. [hedef çerçeveler](../reference/target-frameworks.md) .

*LIB/* ve *ref/* klasörlerdeki dosyalar için hedef çerçeve bilinen adı (tfd) başına bir grup kullanmanızı öneririz.

Aşağıdaki örnek, öğesinin farklı çeşitlemelerini göstermektedir `<group>` :

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

## <a name="determining-which-nuget-target-to-use"></a>Hangi NuGet hedefinin kullanılacağını belirleme

Taşınabilir sınıf kitaplığını hedefleyen paketleme kitaplıkları, `.nuspec` özellikle de yalnızca BIR PCL alt kümesini hedeflerken, klasör adlarında ve dosyanızda hangi NuGet hedefini kullanacağınızı tespit etmek için karmaşık olabilir. Aşağıdaki dış kaynaklar bu konuda size yardımcı olur:

- [.Net 'Teki çerçeve profilleri](https://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephencleary.com)
- [Taşınabilir sınıf kitaplığı profilleri](https://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): PCL profillerini ve bunların eşdeğer NuGet hedeflerini numaralandırma tablosu
- [Taşınabilir sınıf kitaplığı profilleri aracı](https://github.com/StephenCleary/PortableLibraryProfiles) (GitHub.com): SISTEMINIZDE bulunan PCL profillerinin belirlenmesi için komut satırı aracı

## <a name="content-files-and-powershell-scripts"></a>İçerik dosyaları ve PowerShell betikleri

> [!Warning]
> Kesilebilir içerik dosyaları ve betik yürütme yalnızca biçimlendirme ile kullanılabilir `packages.config` ; diğer tüm formatlarda kullanım dışı bırakılmıştır ve yeni paketler için kullanılmamalıdır.

İle `packages.config` , içerik dosyaları ve PowerShell betikleri, ve klasörlerinde aynı klasör kuralına göre hedef çerçeveye göre gruplanabilir `content` `tools` . Örneğin:

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

Bir çerçeve klasörü boş bırakılırsa NuGet, derleme başvuruları veya içerik dosyaları eklemez ya da bu çerçeve için PowerShell betikleri çalıştırmaz.

> [!Note]
> , `init.ps1` Çözüm düzeyinde yürütüldüğü ve projeye bağımlı olmadığından, doğrudan klasörün altına yerleştirilmesi gerekir `tools` . Çerçeve klasörü altına yerleştirildiğinde yok sayılır.