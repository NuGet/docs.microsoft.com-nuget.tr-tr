---
title: NuGet. exe CLı kullanarak bir NuGet paketi oluşturma
description: Dosyalar ve sürüm oluşturma gibi önemli karar noktaları da dahil olmak üzere bir NuGet paketi tasarlama ve oluşturma işlemine yönelik ayrıntılı kılavuz.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 12ecfb8374c43a04d57d32575556adebc991d053
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610700"
---
# <a name="create-a-package-using-the-nugetexe-cli"></a>NuGet. exe CLı kullanarak paket oluşturma

Paketinizin ne olduğunu veya hangi kodun içerdiğini bağımsız olarak, söz konusu işlevselliği bir dizi başka geliştirici tarafından paylaşılabilen ve kullanılabilecek bir bileşene paketlemek için `nuget.exe` veya `dotnet.exe` CLı araçlarından birini kullanırsınız. NuGet CLı araçları 'nı yüklemek için bkz. [NuGet istemci araçları 'Nı yüklemek](../install-nuget-client-tools.md). Visual Studio 'Nun otomatik olarak bir CLı aracı içermediği unutulmamalıdır.

- SDK olmayan stil projeleri için genellikle projeleri .NET Framework, bir paket oluşturmak için bu makalede açıklanan adımları izleyin. Visual Studio ve `nuget.exe` CLı kullanarak adım adım yönergeler için, bkz. [.NET Framework paketi oluşturma ve yayımlama](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md).

- .NET Core .NET Standard ve [SDK stili biçimi](../resources/check-project-format.md)kullanan projeleri ve diğer SDK stili projeleri için, bkz. [DotNet CLI kullanarak bir NuGet paketi oluşturma](creating-a-package-dotnet-cli.md).

- `packages.config`, [Packagereference](../consume-packages/package-references-in-project-files.md)'a geçirilen projeler için [MSBuild-t:Pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration)kullanın.

Teknik olarak, bir NuGet paketi yalnızca `.nupkg` uzantısıyla yeniden adlandırılan ve içeriği belirli kurallara uyan bir ZIP dosyasıdır. Bu konuda, bu kuralları karşılayan bir paket oluşturmanın ayrıntılı süreci açıklanmaktadır.

Paketleme, derlenmiş kod (derlemeler), semboller ve/veya paket olarak teslim etmek istediğiniz diğer dosyaları (bkz. [genel bakış ve iş akışı](overview-and-workflow.md)) ile başlar. Bu işlem, derlenmiş derlemeleri ve paketleri eşitlenmiş halde tutmak için bir proje dosyasındaki bilgilerden çizim yapabilmenize rağmen, derleme ' den bağımsız olan dosyaları derlemeden veya oluşturmadan bağımsızdır.

> [!Important]
> Bu konu SDK olmayan projeler için geçerlidir, genellikle .NET Core dışındaki projeler ve Visual Studio 2017 ve daha yeni sürümleri ve NuGet 4.0 + kullanan projeler .NET Standard.

## <a name="decide-which-assemblies-to-package"></a>Hangi derlemelerin paketlenecek olduğuna karar verin

Genel amaçlı paketlerin çoğu, diğer geliştiricilerin kendi projelerinde kullanabileceği bir veya daha fazla derleme içerir.

- Genel olarak, her derlemenin bağımsız olarak yararlı olması şartıyla her bir derleme için tek bir derlemeye sahip olmak en iyisidir. Örneğin, `Parser.dll`bağımlı bir `Utilities.dll` varsa ve `Parser.dll` kendi kendine yararlıdır ve her biri için bir paket oluşturun. Bunun yapılması, geliştiricilerin `Utilities.dll` ' den bağımsız olarak `Parser.dll` kullanmasına izin verir.

- Kitaplığınız bağımsız olarak yararlı olmayan birden çok derlemeden oluşuyorsa, bunları tek bir pakette birleştirmek iyi olur. Önceki örneği kullanarak, `Parser.dll` yalnızca `Utilities.dll` tarafından kullanılan kodu içeriyorsa, `Parser.dll` ' yi aynı pakette tutmak iyi olur.

- Benzer şekilde, `Utilities.dll` `Utilities.resources.dll` ' e bağımlıysa, tekrar ikinci olarak yararlı değildir ve her ikisini de aynı pakete koyun.

Kaynaklar aslında özel bir durumdur. Bir paket projeye yüklendiğinde NuGet otomatik olarak paketin dll 'Lerine derleme başvuruları ekler, çünkü yerelleştirilmiş uydu derlemeleri oldukları Varsayı`.resources.dll` *lanlar (* bkz. [yerelleştirilmiş paketler oluşturma ](creating-localized-packages.md)). Bu nedenle, başka bir şekilde temel paket kodu içeren dosyalar için `.resources.dll` kullanmaktan kaçının.

Kitaplığınız COM birlikte çalışma derlemelerini içeriyorsa, [com birlikte çalışma Derlemeleriyle paket oluşturma](author-packages-with-com-interop-assemblies.md)' daki ek yönergeleri izleyin.

## <a name="the-role-and-structure-of-the-nuspec-file"></a>. Nuspec dosyasının rolü ve yapısı

Hangi dosyaları paketlemek istediğinizi öğrendikten sonra, bir sonraki adım `.nuspec` XML dosyasında bir paket bildirimi oluşturmaktır.

Bildirim:

1. Paketin içeriğini açıklar ve pakete dahil edilmiştir.
1. Hem paketin oluşturulmasını hem de paketin bir projeye nasıl yükleneceğine ilişkin NuGet 'e yöneltir. Örneğin, bildirim diğer paket bağımlılıklarını tanımlar, bu da ana paket yüklendiğinde NuGet bu bağımlılıkları yükleyebilir.
1. Aşağıda açıklandığı gibi hem gerekli hem de isteğe bağlı özellikleri içerir. Burada bahsedilen diğer özellikler dahil olmak üzere tam Ayrıntılar için bkz [. nuspec başvurusu](../reference/nuspec.md).

Gerekli Özellikler:

- Paketi barındıran Galeri genelinde benzersiz olması gereken paket tanımlayıcısı.
- *Birincil. ikincil. Patch [-suffix]* biçiminde belirli bir sürüm numarası; burada *-suffix* [yayın öncesi sürümlerini](prerelease-packages.md) tanımlar
- Paket başlığı konakta görüntülenecek şekilde (nuget.org gibi)
- Yazar ve sahip bilgileri.
- Paketin uzun açıklaması.

Ortak isteğe bağlı özellikler:

- Sürüm notları
- Telif hakkı bilgileri
- [Visual Studio 'Da Paket Yöneticisi Kullanıcı arabirimi](../consume-packages/install-use-packages-visual-studio.md) için kısa bir açıklama
- Yerel ayar KIMLIĞI
- Proje URL 'SI
- Bir ifade veya dosya olarak lisans (`licenseUrl` kullanım dışı, [`license` nuspec meta veri öğesini](../reference/nuspec.md#license)kullanın)
- Simge URL 'SI
- Bağımlılıklar ve başvuru listeleri
- Galeri aramalarında yardımcı olan Etiketler

Aşağıda, özellikleri açıklayan yorumlarla tipik bir (ancak kurgusal) `.nuspec` dosyası verilmiştir:

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
        <!-- The identifier that must be unique within the hosting gallery -->
        <id>Contoso.Utility.UsefulStuff</id>

        <!-- The package version number that is used when resolving dependencies -->
        <version>1.8.3-beta</version>

        <!-- Authors contain text that appears directly on the gallery -->
        <authors>Dejana Tesic, Rajeev Dey</authors>

        <!-- 
            Owners are typically nuget.org identities that allow gallery
            users to easily find other packages by the same owners.  
        -->
        <owners>dejanatc, rjdey</owners>
        
         <!-- Project URL provides a link for the gallery -->
        <projectUrl>http://github.com/contoso/UsefulStuff</projectUrl>

         <!-- License information is displayed on the gallery -->
        <license type="expression">Apache-2.0</license>
        

        <!-- The icon is used in Visual Studio's package manager UI -->
        <iconUrl>http://github.com/contoso/UsefulStuff/nuget_icon.png</iconUrl>

        <!-- 
            If true, this value prompts the user to accept the license when
            installing the package. 
        -->
        <requireLicenseAcceptance>false</requireLicenseAcceptance>

        <!-- Any details about this particular release -->
        <releaseNotes>Bug fixes and performance improvements</releaseNotes>

        <!-- 
            The description can be used in package manager UI. Note that the
            nuget.org gallery uses information you add in the portal. 
        -->
        <description>Core utility functions for web applications</description>

        <!-- Copyright information -->
        <copyright>Copyright ©2016 Contoso Corporation</copyright>

        <!-- Tags appear in the gallery and can be used for tag searches -->
        <tags>web utility http json url parsing</tags>

        <!-- Dependencies are automatically installed when the package is installed -->
        <dependencies>
            <dependency id="Newtonsoft.Json" version="9.0" />
        </dependencies>
    </metadata>

    <!-- A readme.txt to display when the package is installed -->
    <files>
        <file src="readme.txt" target="" />
    </files>
</package>
```

Bağımlılıkları bildirme ve sürüm numaralarını belirtme hakkında ayrıntılar için bkz. [Packages. config](../reference/packages-config.md) ve [Package sürümü oluşturma](../concepts/package-versioning.md). Ayrıca, `dependency` öğesinde `include` ve `exclude` özniteliklerini kullanarak doğrudan pakette bulunan bağımlılıklardan yüzeylerden yüzey mümkündür. Bkz [. nuspec başvurusu-bağımlılıklar](../reference/nuspec.md#dependencies).

Bildirim bundan oluşturulan pakete eklendiğinden, var olan paketleri inceleyerek istediğiniz sayıda ek örnek bulabilirsiniz. İyi bir kaynak, bilgisayarınızdaki *genel paketler* klasörüdür ve aşağıdaki komut tarafından döndürülen konumudur:

```cli
nuget locals -list global-packages
```

Herhangi bir *package\version* klasörüne gidin, `.nupkg` dosyasını `.zip` dosyasına kopyalayın, ardından bu `.zip` dosyasını açın ve içindeki `.nuspec` ' ü inceleyin.

> [!Note]
> Visual Studio projesinden bir `.nuspec` oluştururken, bildirim, paket oluşturulduğunda projedeki bilgilerle değiştirilmiş belirteçleri içerir. Bkz. [Visual Studio projesinden. nuspec oluşturma](#from-a-visual-studio-project).

## <a name="create-the-nuspec-file"></a>. Nuspec dosyası oluşturma

Tam bir bildirim oluşturmak, genellikle aşağıdaki yöntemlerden biri kullanılarak oluşturulan temel bir `.nuspec` dosyası ile başlar:

- [Kural tabanlı çalışma dizini](#from-a-convention-based-working-directory)
- [Derleme DLL 'SI](#from-an-assembly-dll)
- [Bir Visual Studio projesi](#from-a-visual-studio-project)    
- [Varsayılan değerlere sahip yeni dosya](#new-file-with-default-values)

Ardından dosyayı el ile düzenleyerek son pakette istediğiniz içeriğin tam olarak oluşturulmasını sağlayabilirsiniz.

> [!Important]
> Oluşturulan `.nuspec` dosyaları, paketi `nuget pack` komutuyla oluşturmadan önce değiştirilmesi gereken yer tutucuları içerir. `.nuspec` herhangi bir yer tutucu içeriyorsa, bu komut başarısız olur.

### <a name="from-a-convention-based-working-directory"></a>Kural tabanlı çalışma dizininden

Bir NuGet paketi yalnızca `.nupkg` uzantısıyla yeniden adlandırılmış bir ZIP dosyası olduğundan, yerel dosya sisteminizde istediğiniz klasör yapısını oluşturmanız ve ardından doğrudan bu yapıyla `.nuspec` dosyasını oluşturmanız daha kolay olur. `nuget pack` komutu, bu klasör yapısındaki tüm dosyaları otomatik olarak ekler (`.`ile başlayan tüm klasörler hariç) ve özel dosyaları aynı yapıda tutmanıza olanak sağlar.

Bu yaklaşımın avantajı, pakete dahil etmek istediğiniz dosyaları (Bu konunun ilerleyen kısımlarında açıklandığı gibi) belirtmeniz gerekmez. Yapı işleminizin pakete giden tam klasör yapısını oluşturması, aksi takdirde bir projenin parçası olmayan diğer dosyaları kolayca dahil edebilirsiniz:

- Hedef projeye eklenmesi gereken içerik ve kaynak kodu.
- PowerShell komut dosyaları
- Bir projedeki mevcut yapılandırma ve kaynak kod dosyalarına dönüşümler.

Klasör kuralları aşağıdaki gibidir:

| Klasör | Açıklama | Paket yüklendikten sonra gerçekleştirilecek eylem |
| --- | --- | --- |
| Asıl | Readme. txt konumu | Paket yüklendiğinde, Visual Studio paket kökünde bir Readme. txt dosyası görüntüler. |
| LIB/{tfd} | Verilen hedef çerçeve bilinen adı için derleme (`.dll`), belge (`.xml`) ve sembol (`.pdb`) dosyaları (tfd) | Derlemeler derleme ve çalışma zamanı için başvurular olarak eklenir; `.xml` ve `.pdb` proje klasörlerine kopyalanmış. Bkz. çerçeve hedefine özgü alt klasörler oluşturmak için [birden çok hedef çerçeve destekleme](supporting-multiple-target-frameworks.md) . |
| ref/{tfd} | Verilen hedef çerçeve bilinen adı için bütünleştirilmiş kod (`.dll`) ve sembol (`.pdb`) dosyaları (TFı) | Derlemeler yalnızca derleme süresi için başvuru olarak eklenir; Bu nedenle proje bin klasörüne hiçbir şey kopyalanmayacak. |
| zamanları | Mimariye özgü derleme (`.dll`), simge (`.pdb`) ve yerel kaynak (`.pri`) dosyaları | Derlemeler yalnızca çalışma zamanı için başvuru olarak eklenir; diğer dosyalar proje klasörlerine kopyalanır. Karşılık gelen derleme zamanı derlemesini sağlamak için `/ref/{tfm}` klasörü altında her zaman karşılık gelen (tfd) `AnyCPU` ' a özgü derleme olmalıdır. Bkz. [birden çok hedef çerçeveyi destekleme](supporting-multiple-target-frameworks.md). |
| içerik | Rastgele dosyalar | İçerikler proje köküne kopyalanır. **İçerik** klasörünü, son olarak paketi tüketen hedef uygulamanın kökü olarak düşünün. Paketin uygulamanın */Images* klasörüne görüntü eklemesi için, paketin *içerik/görüntüler* klasörüne yerleştirin. |
| derleme | *(3. x +)* MSBuild `.targets` ve `.props` dosyaları | Projeye otomatik olarak ekleniyor. |
| Buildmultihedefleme | *(4.0 +)* Çapraz çerçeve hedefleme için MSBuild `.targets` ve `.props` dosyaları | Projeye otomatik olarak ekleniyor. |
| buildTransitive | *(5.0 +)* MSBuild `.targets` ve `.props` dosyaları, herhangi bir tüketen projeye geçişli olarak akar. Bkz. [özellik](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) sayfası. | Projeye otomatik olarak ekleniyor. |
| araçlar | Paket Yöneticisi konsolundan erişilebilen PowerShell betikleri ve programları | `tools` klasörü, yalnızca Paket Yöneticisi konsolu için `PATH` ortam değişkenine eklenir (özellikle, proje oluşturulurken MSBuild için ayarlanan `PATH` için *değildir* ). |

Klasör yapınız herhangi bir sayıda hedef çerçeve için herhangi bir sayıda derleme içerebildiğinden, bu yöntem birden çok çerçeveyi destekleyen paketler oluştururken gereklidir.

Herhangi bir durumda, istenen klasör yapısına sahip olduğunuzda, `.nuspec` dosyasını oluşturmak için bu klasörde aşağıdaki komutu çalıştırın:

```cli
nuget spec
```

Yine, oluşturulan `.nuspec` klasör yapısındaki dosyalara açık başvuru içermez. NuGet, Paket oluşturulduğu zaman otomatik olarak tüm dosyaları içerir. Bununla birlikte, bildirimin diğer bölümlerinde yer tutucu değerlerini de düzenlemeniz gerekir.

### <a name="from-an-assembly-dll"></a>Bir derleme DLL 'sinden

Derlemeden bir paket oluşturduğunuzda, aşağıdaki komutu kullanarak derlemedeki meta verilerden bir `.nuspec` dosyası oluşturabilirsiniz:

```cli
nuget spec <assembly-name>.dll
```

Bu formun kullanılması, bildirimdeki bazı yer tutucuları derlemedeki belirli değerlerle değiştirir. Örneğin, `<id>` özelliği derleme adına ayarlanır ve `<version>` derleme sürümü olarak ayarlanır. Ancak bildirimde bulunan diğer özellikler, derlemede eşleşen değerlere sahip değildir ve bu nedenle yine de yer tutucu içerir.

### <a name="from-a-visual-studio-project"></a>Visual Studio projesinden

Bu projeye yüklenmiş olan diğer paketlere otomatik olarak bağımlılık olarak başvurulduğundan, bir `.csproj` veya `.vbproj` dosyasından `.nuspec` oluşturmak kullanışlıdır. Aşağıdaki komutu, proje dosyasıyla aynı klasörde kullanmanız yeterlidir:

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

Elde edilen `<project-name>.nuspec` dosyası, daha önce yüklenmiş olan diğer paketlere yönelik başvurular da dahil olmak üzere, paketleme sırasında değişen *belirteçleri* içerir.

*. Nuspec*'e dahil etmek için paket bağımlılıklarınız varsa `nuget pack` kullanın ve oluşturulan *. nupkg* dosyasının içinden *. nuspec* dosyasını alın. Örneğin, aşağıdaki komutu kullanın.

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget pack myproject.csproj
```

Belirteç, proje özelliğinin her iki tarafında da `$` sembolleri ile ayrılır. Örneğin, bu şekilde oluşturulan bir bildirimde `<id>` değeri, genellikle aşağıdaki gibi görünür:

```xml
<id>$id$</id>
```

Bu belirteç, paket zamanında proje dosyasındaki `AssemblyName` değeriyle değiştirilmiştir. Proje değerlerinin `.nuspec` belirteçlerine tam eşlemesi için, [değiştirme belirteçleri başvurusuna](../reference/nuspec.md#replacement-tokens)bakın.

Belirteçler, projeyi güncelleştirdiğinizde `.nuspec` ' daki sürüm numarası gibi önemli değerleri güncelleştirmek zorunda kalduymasını sağlar. (İsterseniz belirteçleri, her zaman değişmez değerlerle değiştirebilirsiniz). 

Visual Studio projesinden çalışırken, daha sonra [. nupkg dosyasını oluşturmak için NuGet paketini çalıştırma](#run-nuget-pack-to-generate-the-nupkg-file) bölümünde açıklandığı gibi, bir Visual Studio projesinden çalışırken kullanılabilecek birkaç ek paketleme seçeneği olduğunu unutmayın.

#### <a name="solution-level-packages"></a>Çözüm düzeyi paketler

*Yalnızca NuGet 2. x. NuGet 3.0 + ' da kullanılamaz.*

NuGet 2. x, Paket Yöneticisi konsoluna yönelik araçları veya ek komutları (`tools` klasörünün içeriği) yükleyen, ancak başvuru, içerik veya yapılandırma özelleştirmelerini, içindeki herhangi bir projeye eklemez çözümden. Bu tür paketler doğrudan `lib`, `content` veya `build` klasörlerinde dosya içermez ve bağımlılıklarından hiçbirinin ilgili `lib`, `content` veya `build` klasörlerinde dosyaları yoktur.

NuGet, çözüm düzeyindeki paketleri projenin `packages.config` dosyası yerine `.nuget` klasöründeki bir `packages.config` dosyasında izler.

### <a name="new-file-with-default-values"></a>Varsayılan değerlere sahip yeni dosya

Aşağıdaki komut, uygun dosya yapısıyla başlayabilmenizi sağlayan yer tutucuları olan varsayılan bir bildirim oluşturur:

```cli
nuget spec [<package-name>]
```

\<paket adı\>atlarsanız, elde edilen dosya `Package.nuspec`. `Contoso.Utility.UsefulStuff`gibi bir ad sağlarsanız, dosya `Contoso.Utility.UsefulStuff.nuspec`.

Sonuç `.nuspec` `projectUrl` gibi değerler için yer tutucular içerir. Son `.nupkg` dosyasını oluşturmak için dosyayı kullanmadan önce düzenlemeyi unutmayın.

## <a name="choose-a-unique-package-identifier-and-setting-the-version-number"></a>Benzersiz bir paket tanımlayıcısı seçin ve sürüm numarasını ayarla

Paket tanımlayıcısı (`<id>` öğesi) ve sürüm numarası (`<version>` öğesi), pakette bulunan tam kodu benzersiz bir şekilde tanımladıklarından bildirimde en önemli iki değerden oluşur.

**Paket tanımlayıcısı için en iyi uygulamalar:**

- **Benzersizlik**: tanımlayıcı, NuGet.org genelinde benzersiz olmalıdır veya paketi barındıran Galeri. Bir tanımlayıcıya karar vermeden önce, adın zaten kullanımda olup olmadığını denetlemek için ilgili galeride arama yapın. Çakışmaları önlemek için, `Contoso.` gibi, tanımlayıcının ilk parçası olarak şirketinizin adını kullanmak iyi bir modeldir.
- **Ad alanı benzeri adlar**: kısa çizgi yerine nokta gösterimini kullanarak .net 'teki ad alanlarına benzer bir model izleyin. Örneğin, `Contoso-Utility-UsefulStuff` veya `Contoso_Utility_UsefulStuff`yerine `Contoso.Utility.UsefulStuff` kullanın. Tüketiciler ayrıca, paket tanımlayıcısı kodda kullanılan ad alanları ile eşleştiğinde yararlı olduğunu bulur.
- **Örnek paketler**: başka bir paketin nasıl kullanılacağını gösteren bir örnek kod paketi oluşturursanız, `Contoso.Utility.UsefulStuff.Sample` ' de olduğu gibi `.Sample` ' i tanımlayıcıda sonek olarak ekleyin. (Örnek paketin, diğer pakete bağımlılığı vardır.) Örnek bir paket oluştururken, daha önce açıklanan kural tabanlı çalışma dizini yöntemini kullanın. `content` klasöründe, örnek kodu `\Samples\Contoso.Utility.UsefulStuff.Sample`gibi `\Samples\<identifier>` adlı bir klasörde düzenleyin.

**Paket sürümü için en iyi uygulamalar:**

- Genel olarak, paketin sürümünü kitaplıkla eşleşecek şekilde ayarlayın, ancak bu kesinlikle gerekli değildir. Bu, [Hangi derlemelerin paketlenecek olduğuna karar verirken](#decide-which-assemblies-to-package)daha önce açıklandığı gibi, bir paketi tek bir derlemeyle sınırlandırdığınızda bu basit bir işlemdir. Genel olarak, NuGet 'in derleme sürümlerini değil, bağımlılıkları çözümlerken Paket sürümleriyle uğraşır olduğunu unutmayın.
- Standart olmayan bir sürüm düzeni kullanırken, [paket sürümü oluşturma](../concepts/package-versioning.md)bölümünde açıklandığı gibi NuGet sürüm oluşturma kurallarını dikkate aldığınızdan emin olun.

> Aşağıdaki kısa blog gönderisi serisi, sürüm oluşturmayı anlamak için de yararlıdır:
>
> - [1. Bölüm: DLL Hell üzerinde alma](https://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [2. Bölüm: çekirdek algoritması](https://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [3. kısım: bağlama yeniden yönlendirmeleri aracılığıyla birleşme](https://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="add-a-readme-and-other-files"></a>Benioku dosyası ve diğer dosyaları ekleme

Pakete dahil edilecek dosyaları doğrudan belirtmek için, `<metadata>` etiketini *izleyen* `.nuspec` dosyasında `<files>` düğümünü kullanın:

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
    <!-- ... -->
    </metadata>
    <files>
        <!-- Add a readme -->
        <file src="readme.txt" target="" />

        <!-- Add files from an arbitrary folder that's not necessarily in the project -->
        <file src="..\..\SomeRoot\**\*.*" target="" />
    </files>
</package>
```

> [!Tip]
> Kural tabanlı çalışma dizini yaklaşımını kullanırken Readme. txt dosyasını paket köküne ve `content` klasöründeki diğer içeriklere yerleştirebilirsiniz. Bildirimde `<file>` öğesi gerekli değildir.

Paket kökünde `readme.txt` adlı bir dosya eklediğinizde Visual Studio, paketi doğrudan yükledikten hemen sonra bu dosyanın içeriğini düz metin olarak görüntüler. (Benioku dosyaları, bağımlılıklar olarak yüklenen paketler için gösterilmez). Örneğin, HtmlAgilityPack paketinin Benioku dosyası şöyle görünür:

![Yükleme sonrasında bir NuGet paketi için Benioku dosyası görüntüleme](media/Create_01-ShowReadme.png)

> [!Note]
> `.nuspec` dosyasında boş bir `<files>` düğümü eklerseniz, NuGet pakette `lib` klasörü dışında başka bir içerik de içermez.

## <a name="include-msbuild-props-and-targets-in-a-package"></a>Bir pakete MSBuild props ve hedefleri dahil etme

Bazı durumlarda, özel bir araç veya derleme sırasında işlem çalıştırma gibi paketinizi kullanan projelere özel yapı hedefleri veya özellikler eklemek isteyebilirsiniz. Bu, dosyaları `<package_id>.targets` veya `<package_id>.props` (`Contoso.Utility.UsefulStuff.targets`gibi) projenin `\build` klasörü içinde yerleştirerek yapabilirsiniz.

Kök `\build` klasöründeki dosyalar tüm hedef çerçeveler için uygun kabul edilir. Çerçeveye özgü dosyalar sağlamak için, önce bunları aşağıdaki gibi uygun alt klasörlere yerleştirin:

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

Sonra `.nuspec` dosyasında, `<files>` düğümündeki bu dosyalara başvurduğunuzdan emin olun:

```xml
<?xml version="1.0"?>
<package >
    <metadata minClientVersion="2.5">
    <!-- ... -->
    </metadata>
    <files>
        <!-- Include everything in \build -->
        <file src="build\**" target="build" />

        <!-- Other files -->
        <!-- ... -->
    </files>
</package>
```

Bir paketteki MSBuild props ve hedefleri de dahil olmak üzere [NuGet 2,5 ile birlikte sunulmuştur](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files). bu nedenle, paketi kullanmak için gereken en düşük NuGet istemci sürümünü göstermek için `minClientVersion="2.5"` özniteliğini `metadata` öğesine eklemeniz önerilir.

NuGet, `\build` dosyaları içeren bir paket yüklediğinde, proje dosyasına `.targets` ve `.props` dosyalarını işaret eden MSBuild `<Import>` öğeleri ekler. (`.props`, proje dosyasının üst kısmına eklenir; `.targets` en alta eklenir.) Her hedef çerçeve için ayrı bir koşullu MSBuild `<Import>` öğesi eklenir.

Çapraz çerçeve hedefleme için MSBuild `.props` ve `.targets` dosyaları `\buildMultiTargeting` klasörüne yerleştirilebilir. Paket yüklemesi sırasında NuGet, karşılık gelen `<Import>` öğelerini koşulla birlikte proje dosyasına ekler; hedef Framework ayarlanmadı (MSBuild özelliği `$(TargetFramework)` boş olmalıdır).

NuGet 3. x ile, hedefler projeye eklenmez, ancak bunun yerine `{projectName}.nuget.g.targets` ve `{projectName}.nuget.g.props` aracılığıyla kullanılabilir hale getirilir.

## <a name="run-nuget-pack-to-generate-the-nupkg-file"></a>. Nupkg dosyasını oluşturmak için NuGet paketini çalıştırın

Bir derlemeyi veya kural tabanlı çalışma dizinini kullanırken, `.nuspec` dosyanız ile `nuget pack` çalıştırarak bir paket oluşturun ve `<project-name>` ' yi özel dosya adıyla değiştirin:

```cli
nuget pack <project-name>.nuspec
```

Bir Visual Studio projesi kullanırken, proje dosyası ile `nuget pack` ' ı çalıştırarak projenin `.nuspec` dosyasını otomatik olarak yükler ve içindeki belirteçleri proje dosyasındaki değerleri kullanarak değiştirir:

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> Projenin belirteç değerlerinin kaynağı olduğundan, belirteç değişikliği için proje dosyasını doğrudan kullanmak gereklidir. Bir `.nuspec` dosyası ile `nuget pack` kullanırsanız, belirteç değiştirme gerçekleşmez.

Her durumda, `nuget pack` `.git` veya `.hg` gibi bir noktayla başlayan klasörleri dışlar.

NuGet, bildirimde yer tutucu değerlerini değiştirme gibi, düzeltilmesi gereken `.nuspec` dosyasında herhangi bir hata olup olmadığını gösterir.

`nuget pack` başarılı olduktan sonra, [paket yayımlama](../nuget-org/publish-a-package.md)konusunda açıklandığı gibi uygun bir galeride yayımlayacağınız bir `.nupkg` dosyanız vardır.

> [!Tip]
> Paketi oluşturduktan sonra, [Paket Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) aracında açmak için yararlı bir yol. Bu, paket içeriklerinin ve bildiriminin grafik görünümünü sağlar. Ayrıca, elde edilen `.nupkg` dosyasını bir `.zip` dosyasına yeniden adlandırabilir ve içeriğini doğrudan keşfedebilirsiniz.

### <a name="additional-options"></a>Ek seçenekler

Dosyaları dışlamak, bildirimdeki sürüm numarasını geçersiz kılmak ve çıkış klasörünü diğer özellikler arasında değiştirmek için `nuget pack` ile çeşitli komut satırı anahtarlarını kullanabilirsiniz. Tüm liste için, [paket komut başvurusuna](../reference/cli-reference/cli-ref-pack.md)bakın.

Aşağıdaki seçenekler, Visual Studio projeleriyle yaygın olarak karşılaşılan birkaç seçenek vardır:

- **Başvurulan projeler**: proje diğer projelere başvuruyorsa, `-IncludeReferencedProjects` seçeneğini kullanarak başvurulan projeleri paketin parçası olarak veya bağımlılıklar olarak ekleyebilirsiniz:

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    Bu içerme işlemi özyinelemeli, yani `MyProject.csproj` projelere B ve C başvuruları varsa ve bu projelere D, E ve F başvurusu varsa, B, C, D, E ve F 'ye ait dosyalar pakete dahil edilir.

    Başvurulan bir proje kendi kendine ait bir `.nuspec` dosyası içeriyorsa, NuGet bu başvurulan projeyi bunun yerine bağımlılık olarak ekler.  Bu projeyi ayrı ayrı paketleyip yayımlamanız gerekir.

- **Derleme yapılandırması**: varsayılan olarak, NuGet proje dosyasında varsayılan derleme yapılandırma kümesini kullanır, genellikle *hata ayıklayın*. *Yayın*gibi farklı bir derleme yapılandırmasından dosya paketetmek için, yapılandırma ile `-properties` seçeneğini kullanın:

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- **Semboller**: tüketicilerin hata ayıklayıcıdaki paket kodunuzda ilerlemenize izin veren sembolleri dahil etmek için `-Symbols` seçeneğini kullanın:

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="test-package-installation"></a>Test paketi yüklemesi

Bir paketi yayımlamadan önce, genellikle bir projeye paket yükleme işlemini test etmek istersiniz. Testler, projenin proje içinde doğru konumlarında tüm dosyaları sonlandırmış olduğundan emin olmanızı ister.

Yüklemeleri, Visual Studio 'da veya normal [paket yükleme adımlarını](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package)kullanarak komut satırında el ile test edebilirsiniz.

Otomatikleştirilmiş test için temel işlem aşağıdaki gibidir:

1. `.nupkg` dosyasını yerel bir klasöre kopyalayın.
1. `nuget sources add -name <name> -source <path>` komutunu kullanarak, klasörü paket kaynaklarınıza ekleyin (bkz. [NuGet kaynakları](../reference/cli-reference/cli-ref-sources.md)). Bu yerel kaynağı yalnızca belirli bir bilgisayarda bir kez ayarlamanız gerektiğini unutmayın.
1. Bu kaynaktan paketi, `<name>` `nuget sources`verilen kaynak adı ile eşleşen `nuget install <packageID> -source <name>` kullanarak yükler. Kaynağı belirtmek paketin o kaynaktan yalnızca yüklenmesini sağlar.
1. Dosyaların doğru şekilde yüklenip yüklenmediğini denetlemek için dosya sisteminizi inceleyin.

## <a name="next-steps"></a>Sonraki Adımlar

Bir `.nupkg` dosyası olan bir paket oluşturduktan sonra, [paketi yayımlama](../nuget-org/publish-a-package.md)konusunda açıklandığı gibi istediğiniz Galeri ile yayımlayabilirsiniz.

Ayrıca, aşağıdaki konularda açıklandığı gibi, paketinizin yeteneklerini genişletmek veya diğer senaryoları desteklemek isteyebilirsiniz:

- [Paket sürümü oluşturma](../concepts/package-versioning.md)
- [Birden çok hedef çerçeveyi destekleme](../create-packages/supporting-multiple-target-frameworks.md)
- [Kaynak ve yapılandırma dosyalarının dönüştürmeleri](../create-packages/source-and-config-file-transformations.md)
- [Yerelleştirme](../create-packages/creating-localized-packages.md)
- [Yayın öncesi sürümler](../create-packages/prerelease-packages.md)
- [Paket türünü ayarlama](../create-packages/set-package-type.md)
- [COM birlikte çalışma Derlemeleriyle paket oluşturma](../create-packages/author-packages-with-COM-interop-assemblies.md)

Son olarak, bilmeniz için ek paket türleri vardır:

- [Yerel Paketler](../guides/native-packages.md)
- [Sembol Paketleri](../create-packages/symbol-packages-snupkg.md)
