---
title: NuGet paketleri için Çoklu hedefleme
description: Tek bir NuGet paketinin içinden birden çok .NET Framework sürümünü hedeflemek için çeşitli yöntemlerin açıklaması.
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: 69e12ce1c78f8d4d50cbad7a0237d767064193ab
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610647"
---
# <a name="support-multiple-net-versions"></a>Çoklu .NET sürümlerini destekler

Birçok kitaplık .NET Framework belirli bir sürümünü hedefleyin. Örneğin, kitaplıkınızın, UWP 'e özgü bir sürümüne ve .NET Framework 4,6 ' deki özelliklerden yararlanan başka bir sürüme sahip olabilirsiniz. NuGet buna uyum sağlamak için, aynı kitaplığın birden çok sürümünü tek bir pakette yerleştirmeyi destekler.

Bu makalede, paketin veya derlemelerin nasıl oluşturulduğuna bakılmaksızın bir NuGet paketinin düzeni açıklanmaktadır (yani, düzen birden çok SDK olmayan *. csproj* dosyası ve özel bir *. nuspec* dosyası ya da tek bir çok hedefli SDK stili *. csproj*). Bir SDK stili proje için, NuGet [paketi](../reference/msbuild-targets.md) , paketin nasıl oluşturulması gerektiğini bilir ve derlemeleri doğru lib klasörlerine yerleştirmeyi ve her hedef çerçeve (tfd) için bağımlılık grupları oluşturmayı otomatikleştirir. Ayrıntılı yönergeler için bkz. [proje dosyanızdaki çoklu .NET Framework sürümlerini destekleme](multiple-target-frameworks-project-file.md).

[Paket oluşturma](../create-packages/creating-a-package.md#from-a-convention-based-working-directory)bölümünde açıklanan kural tabanlı çalışma dizini yöntemi kullanılırken bu makalede açıklandığı gibi paketi el ile oluşturmanız gerekir. SDK stili bir proje için otomatik yöntem önerilir, ancak paketi bu makalede açıklandığı gibi el ile düzenlemek de tercih edebilirsiniz.

## <a name="framework-version-folder-structure"></a>Framework sürüm klasörü yapısı

Bir kitaplığın yalnızca bir sürümünü içeren veya birden çok çerçeveyi hedefleyen bir paket oluştururken, aşağıdaki kurala sahip farklı büyük/küçük harf duyarlı çerçeve adlarını kullanarak her zaman alt klasörleri `lib` altında yaparsınız:

    lib\{framework name}[{version}]

Desteklenen adların tüm listesi için bkz. [hedef çerçeveler başvurusu](../reference/target-frameworks.md#supported-frameworks).

Bir çerçeveye özgü olmayan ve doğrudan kök `lib` klasörüne yerleştirilmiş bir kitaplık sürümüne sahip olmanız gerekir. (Bu özellik yalnızca `packages.config` ile desteklenir). Bunu yapmak, kitaplığı herhangi bir hedef çerçeve ile uyumlu hale getirir ve büyük olasılıkla beklenmedik çalışma zamanı hatalarına neden olur. Kök klasörde (örneğin, `lib\abc.dll`) veya alt klasörlerde (`lib\abc\abc.dll` gibi) derlemeler eklendiğinde kullanım dışı bırakılmıştır ve PackagesReference biçimi kullanılırken yok sayılır.

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

Paketi oluştururken tüm bu dosyaları kolayca dahil etmek için `.nuspec` ' nin `<files>` bölümünde özyinelemeli bir `**` joker karakteri kullanın:

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a>Mimariye özgü klasörler

Mimariye özgü derlemeleriniz, yani ARM, x86 ve x64 'u hedefleyen ayrı derlemeler varsa, bunları `{platform}-{architecture}\lib\{framework}` veya `{platform}-{architecture}\native` adlı alt klasörler içinde `runtimes` adlı bir klasöre yerleştirmeniz gerekir. Örneğin, aşağıdaki klasör yapısı, Windows 10 ' u ve `uap10.0` çerçevesini hedefleyen hem yerel hem de yönetilen DLL 'Leri kapsayabilmelidir:

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

Bu derlemeler yalnızca çalışma zamanında kullanılabilir. bu nedenle, ilgili derleme zamanı derlemesini sağlamak ve `/ref/{tfm}` klasöründe `AnyCPU` derlemesi sağlamak istiyorsanız. 

Lütfen NuGet her zaman bu derleme veya çalışma zamanı varlıklarını tek bir klasörden seçer. bu nedenle `/ref` ' dan bazı uyumlu varlıklar varsa, derleme zamanı derlemelerini eklemek için `/lib` yok sayılır. Benzer şekilde, `/runtime` ' dan bazı uyumlu varlıklar varsa, çalışma zamanı için de `/lib` yok sayılır.

`.nuspec` bildiriminde bu dosyalara başvurma örneği için bkz. [UWP paketleri oluşturma](../guides/create-uwp-packages.md) .

Ayrıca bkz. [NuGet Ile Windows Mağazası uygulama bileşeni paketleme](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2)

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a>Bir projede derleme sürümlerini ve hedef Framework 'ü eşleştirme

NuGet birden çok derleme sürümüne sahip bir paket yüklediğinde, derlemenin çerçeve adını projenin hedef çerçevesiyle eşleştirmeye çalışır.

Bir eşleşme bulunmazsa, NuGet derlemeyi, varsa projenin hedef çerçevesine eşit veya daha küçük olan en yüksek sürüm için kopyalar. Uyumlu derleme bulunamazsa, NuGet uygun bir hata iletisi döndürür.

Örneğin, bir pakette aşağıdaki klasör yapısını göz önünde bulundurun:

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

Bu paketi, .NET Framework 4,6 ' i hedefleyen bir projede yüklerken, en yüksek kullanılabilir sürüm 4,6 ' den küçük veya buna eşit olduğu için NuGet, derlemeyi `net45` klasörüne yüklenir.

Proje, diğer taraftan .NET Framework 4.6.1 hedefliyorsa, NuGet derlemeyi `net461` klasörüne yüklenir.

Proje, .NET Framework 4,0 ve öncesini hedefliyorsa, NuGet uyumlu derlemeyi bulmayan uygun bir hata iletisi oluşturur.

## <a name="grouping-assemblies-by-framework-version"></a>Derlemeleri Framework sürümüne göre gruplandırma

NuGet, derlemeleri yalnızca paketteki tek bir kitaplık klasöründen kopyalar. Örneğin, bir paketin aşağıdaki klasör yapısına sahip olduğunu varsayalım:

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

Paket, .NET Framework 4,5 ' i hedefleyen bir projeye yüklendiğinde, tek derleme yüklü olan `MyAssembly.dll` (v 2.0) olur. `MyAssembly.Core.dll` (v 1.0), `net45` klasöründe listelenmediğinden yüklenmedi. `MyAssembly.Core.dll`, `MyAssembly.dll`sürüm 2,0 ' de birleştirilmiş olabileceğinden NuGet bu şekilde davranır.

.NET Framework 4,5 için `MyAssembly.Core.dll` ' ın yüklenmesini istiyorsanız, bir kopyayı `net45` klasörüne yerleştirin.

## <a name="grouping-assemblies-by-framework-profile"></a>Derlemeleri çerçeve profiline göre gruplandırma

NuGet Ayrıca, klasörün sonuna bir tire ve profil adı ekleyerek belirli bir çerçeve profilinin hedeflenmesini destekler.

    lib\{framework name}-{profile}

Desteklenen profiller şunlardır:

- `client`: Istemci profili
- `full`: tam profil
- `wp`: Windows Phone
- `cf`: Compact Framework

## <a name="declaring-dependencies-advanced"></a>Bağımlılıkları bildirme (Gelişmiş)

Bir proje dosyası paketleme sırasında, NuGet otomatik olarak projeden bağımlılıkları oluşturmaya çalışır. Bağımlılıkları bildirmek için bir *. nuspec* dosyası kullanma hakkında bu bölümdeki bilgiler genellikle yalnızca gelişmiş senaryolar için gereklidir.

*(Sürüm 2.0 +)* `<dependencies>` öğesi içinde `<group>` öğeleri kullanarak, hedef projenin hedef çerçevesine karşılık gelen *. nuspec* içinde paket bağımlılıklarını bildirebilirsiniz. Daha fazla bilgi için bkz. [Dependencies öğesi](../reference/nuspec.md#dependencies-element).

Her grup `targetFramework` adlı bir özniteliğe sahiptir ve sıfır veya daha fazla `<dependency>` öğesi içerir. Hedef Framework, projenin çerçeve profiliyle uyumlu olduğunda bu bağımlılıklar birlikte yüklenir. Tam çerçeve tanımlayıcıları için bkz. [hedef çerçeveler](../reference/target-frameworks.md) .

*LIB/* ve *ref/* klasörlerdeki dosyalar için hedef çerçeve bilinen adı (tfd) başına bir grup kullanmanızı öneririz.

Aşağıdaki örnek `<group>` öğesinin farklı çeşitlemelerini gösterir:

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

Taşınabilir sınıf kitaplığını hedefleyen paketleme kitaplıklarında, özellikle yalnızca bir PCL alt kümesini hedeflerken, klasör adlarında ve `.nuspec` dosyasında kullanmanız gereken NuGet hedefini tespit etmek karmaşık olabilir. Aşağıdaki dış kaynaklar bu konuda size yardımcı olur:

- [.Net 'Teki çerçeve profilleri](https://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephencleary.com)
- [Taşınabilir sınıf kitaplığı profilleri](https://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): PCL profillerini ve bunların eşdeğer NuGet hedeflerini numaralandırma tablosu
- [Taşınabilir sınıf kitaplığı profilleri aracı](https://github.com/StephenCleary/PortableLibraryProfiles) (GitHub.com): SISTEMINIZDE bulunan PCL profillerinin belirlenmesi için komut satırı aracı

## <a name="content-files-and-powershell-scripts"></a>İçerik dosyaları ve PowerShell betikleri

> [!Warning]
> Kesilebilir içerik dosyaları ve betik yürütme yalnızca `packages.config` biçiminde kullanılabilir; Bunlar diğer tüm biçimleriyle kullanımdan kaldırılmıştır ve yeni paketler için kullanılmamalıdır.

`packages.config`, içerik dosyaları ve PowerShell betikleri, `content` ve `tools` klasörlerindeki aynı klasör kuralına göre hedef çerçeveye göre gruplanabilir. Örneğin:

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
> `init.ps1` çözüm düzeyinde yürütüldüğü ve projeye bağımlı olmadığından, doğrudan `tools` klasörünün altına yerleştirilmesi gerekir. Çerçeve klasörü altına yerleştirildiğinde yok sayılır.
