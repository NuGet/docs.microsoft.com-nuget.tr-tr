---
title: nuget.exe CLI kullanarak bir NuGet paketi oluşturun
description: Dosyaları ve sürüm gibi önemli karar noktaları da dahil olmak üzere bir NuGet paketi tasarlama ve oluşturma sürecine ilişkin ayrıntılı bir kılavuz.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: b3e6f0efc9e2e12de186ffd4ce29d496d07d5fc4
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428949"
---
# <a name="create-a-package-using-the-nugetexe-cli"></a>nuget.exe CLI kullanarak bir paket oluşturma

Paketiniz ne yaparsa yapsın veya hangi kodu içerse içersin, `dotnet.exe`bu işlevselliği diğer geliştiricilerle paylaşılabilen ve diğer geliştiriciler tarafından kullanılabilecek bir bileşene dönüştürmek için CLI araçlarından `nuget.exe` birini kullanırsınız. NuGet CLI araçlarını yüklemek için [NuGet istemci araçlarını yükleyin.](../install-nuget-client-tools.md) Visual Studio'nun otomatik olarak bir CLI aracı içermediğini unutmayın.

- Genellikle .NET Framework projeleri olan SDK tarzı olmayan projeler de bir paket oluşturmak için bu makalede açıklanan adımları izleyin. Visual Studio ve `nuget.exe` CLI'yi kullanarak adım adım talimatlar için bir [.NET Framework paketi oluştur ve yayımla'ya](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)bakın.

- [SDK stili biçimini](../resources/check-project-format.md)kullanan .NET Core ve .NET Standard projeleri ve diğer SDK tarzı projeler için [bkz.](creating-a-package-dotnet-cli.md)

- `packages.config` [PackageReference'a](../consume-packages/package-references-in-project-files.md)geçirilen projeler için [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration)kullanın.

Teknik olarak konuşursak, NuGet paketi, `.nupkg` uzantıyla birlikte yeniden adlandırılan ve içeriği belirli kurallarla eşleşen bir ZIP dosyasıdır. Bu konu, bu kuralları karşılayan bir paket oluşturma nın ayrıntılı işlemini açıklar.

Ambalaj, paket olarak sunmak istediğiniz derlenmiş kod (derlemeler), semboller ve/veya diğer dosyalarla başlar (bkz. [Genel Bakış ve iş akışı).](overview-and-workflow.md) Derlenen derlemeleri ve paketleri eşit tutmak için proje dosyasındaki bilgilerden yararlanabilmekle birlikte, bu işlem pakete giren dosyaları derlemekten veya başka bir şekilde oluşturmaktan bağımsızdır.

> [!Important]
> Bu konu, Visual Studio 2017 ve daha yüksek sürümler ve NuGet 4.0+ kullanarak genellikle .NET Core ve .NET Standard projeleri dışındaki projeler olan SDK tarzı olmayan projeler için geçerlidir.

## <a name="decide-which-assemblies-to-package"></a>Hangi derlemelerin paketlenenene karar vereceğine karar verin

Genel amaçlı paketlerin çoğu, diğer geliştiricilerin kendi projelerinde kullanabilecekleri bir veya daha fazla derleme içerir.

- Genel olarak, her derlemenin bağımsız olarak yararlı olması koşuluyla, NuGet paketi başına bir derleme olması en iyisidir. Örneğin, kendi başına `Utilities.dll` buna bağlı `Parser.dll`ve `Parser.dll` yararlı olan bir paketiniz varsa, her biri için bir paket oluşturun. Bunu yapmak, geliştiricilerin `Parser.dll` `Utilities.dll`'' den bağımsız olarak kullanmasına olanak tanır.

- Kitaplığınız bağımsız olarak yararlı olmayan birden çok derlemeden oluşuyorsa, bunları tek bir pakette birleştirmek te sorun değildir. Önceki örneği kullanarak, `Parser.dll` yalnızca kullanılan `Utilities.dll`kod içeriyorsa, aynı pakette `Parser.dll` tutmak iyidir.

- Benzer şekilde, `Utilities.dll` eğer `Utilities.resources.dll`bağlıdır , nerede tekrar ikincisi kendi başına yararlı değildir, o zaman aynı pakette her ikisini de koyun.

Kaynaklar aslında özel bir durum. Bir paket projeye yüklendiğinde, NuGet otomatik olarak yerelleştirilmiş uydu derlemeleri olarak *excluding* kabul edildikleri için `.resources.dll` adı geçenler hariç olmak üzere paketin DL'lerine montaj başvuruları ekler (bkz. [yerelleştirilmiş paketler oluşturma).](creating-localized-packages.md) Bu nedenle, aksi `.resources.dll` takdirde temel paket kodu içeren dosyalar için kullanmaktan kaçının.

Kitaplığınız COM interop derlemeleri içeriyorsa, [COM interop derlemeleri ile paketleri oluştur'daki](author-packages-with-com-interop-assemblies.md)ek yönergeleri izleyin.

## <a name="the-role-and-structure-of-the-nuspec-file"></a>.nuspec dosyasının rolü ve yapısı

Hangi dosyaları paketlemek istediğinizi bildiğinizde, bir sonraki adım `.nuspec` XML dosyasında bir paket bildirimi oluşturmaktır.

Manifesto:

1. Paketin içeriğini açıklar ve paketin kendisi dahildir.
1. Paketin oluşturulmasını hem sürücüler hem de NuGet'e paketi projeye nasıl yükleyeceklerine ilişkin talimat verir. Örneğin, bildirim, NuGet'in ana paket yüklendiğinde bu bağımlılıkları da yükleyebileceği diğer paket bağımlılıklarını tanımlar.
1. Aşağıda açıklandığı gibi hem gerekli hem de isteğe bağlı özellikleri içerir. Burada belirtilmeyen diğer özellikler de dahil olmak üzere tam ayrıntılar için [.nuspec başvurusuna](../reference/nuspec.md)bakın.

Gerekli özellikler:

- Paketi barındıran galeride benzersiz olması gereken paket tanımlayıcısı.
- *Major.Minor.Patch[-Soneki]* formunda *-Sonek* ön sürüm [sürümlerini](prerelease-packages.md) tanımlayan belirli bir sürüm numarası
- Ana bilgisayarda görünmesi gerektiği gibi paket başlığı (nuget.org gibi)
- Yazar ve sahip bilgileri.
- Paketin uzun bir açıklaması.

Yaygın isteğe bağlı özellikler:

- Sürüm notları
- Telif hakkı bilgileri
- [Visual Studio'da Paket Yöneticisi UI](../consume-packages/install-use-packages-visual-studio.md) için kısa bir açıklama
- Yerel kimlik
- Proje URL'si
- İfade veya dosya olarak`licenseUrl` lisans (amortismana uymaktadır, [ `license` nuspec meta veri öğesini](../reference/nuspec.md#license)kullanın )
- Simge URL'si
- Bağımlılıklar ve referanslar listeleri
- Galeri aramalarına yardımcı olan etiketler

Aşağıdaki özellikleri açıklayan yorumlar ile tipik `.nuspec` (ama hayali) bir dosya:

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
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

Bağımlılıkları bildirme ve sürüm numaralarını belirtme hakkında ayrıntılı bilgi için [packages.config](../reference/packages-config.md) ve [Package sürümüne](../concepts/package-versioning.md)bakın. Ayrıca, öğedeki `include` öznitelikleri ve `exclude` öznitelikleri kullanarak varlıkları doğrudan paketteki bağımlılıklardan yüzeye çıkarmak da mümkündür. `dependency` [Bkz..nuspec Başvuru - Bağımlılıklar](../reference/nuspec.md#dependencies).

Bildirim, oluşturulan pakete dahil olduğundan, varolan paketleri inceleyerek istediğiniz sayıda ek örnek bulabilirsiniz. İyi bir kaynak, bilgisayarınızdaki *genel paketler* klasörüdür ve konumu aşağıdaki komutla döndürülür:

```cli
nuget locals -list global-packages
```

Herhangi bir *paket\sürüm* klasörüne `.nupkg` gidin, `.zip` dosyayı bir `.zip` dosyaya `.nuspec` kopyalayın, sonra dosyayı açın ve dosyanın içini inceleyin.

> [!Note]
> Bir Visual `.nuspec` Studio projesinden bir oluşturma yaparken, bildirim, paket oluşturulduğunda projedeki bilgilerle değiştirilen belirteçler içerir. Bkz. [Bir Visual Studio projesinden .nuspec oluşturma.](#from-a-visual-studio-project)

## <a name="create-the-nuspec-file"></a>.nuspec dosyasını oluşturma

Tam bir bildirim oluşturma genellikle `.nuspec` aşağıdaki yöntemlerden biri aracılığıyla oluşturulan temel bir dosya ile başlar:

- [Kongre tabanlı çalışma dizini](#from-a-convention-based-working-directory)
- [Bir montaj DLL](#from-an-assembly-dll)
- [Görsel Stüdyo projesi](#from-a-visual-studio-project)    
- [Varsayılan değerlere sahip yeni dosya](#new-file-with-default-values)

Daha sonra, son pakette istediğiniz içeriği tam olarak açıklayabilmek için dosyayı elle düzenlemeniz.

> [!Important]
> Oluşturulan `.nuspec` `nuget pack` dosyalar, komutla paketi oluşturmadan önce değiştirilmesi gereken yer tutucular içerir. Herhangi bir yer `.nuspec` tutucu içeriyorsa bu komut başarısız olur.

### <a name="from-a-convention-based-working-directory"></a>Sözleşme tabanlı çalışma dizininden

NuGet paketi `.nupkg` yalnızca uzantıyla yeniden adlandırılabilen bir ZIP dosyası olduğundan, yerel dosya sisteminizde istediğiniz klasör yapısını oluşturmak `.nuspec` ve ardından dosyayı doğrudan bu yapıdan oluşturmak genellikle en kolayıdır. Komut `nuget pack` daha sonra otomatik olarak bu klasör yapısına tüm dosyaları `.`ekler (ile başlayan tüm klasörler hariç , aynı yapıda özel dosyaları tutmak için izin).

Bu yaklaşımın avantajı, pakete hangi dosyaları eklemek istediğinizi (bu konuda daha sonra açıklandığı gibi) bildirimde belirtmeniz gerekmemelidir. Yapı işleminizin pakete giren tam klasör yapısını oluşturmasını sağlayabilir ve aksi takdirde projenin parçası olmayan diğer dosyaları kolayca ekleyebilirsiniz:

- Hedef projeye enjekte edilmesi gereken içerik ve kaynak kodu.
- PowerShell komut dosyaları
- Projedeki varolan yapılandırma ve kaynak kodu dosyalarına dönüşümler.

Klasör kuralları aşağıdaki gibidir:

| Klasör | Açıklama | Paket yükleme üzerine eylem |
| --- | --- | --- |
| (kök) | readme.txt için konum | Visual Studio, paket yüklendiğinde paket kökünde bir readme.txt dosyası görüntüler. |
| lib/{tfm} | Verilen`.dll`Hedef Çerçeve`.xml`Takma (TFM) için Derleme ( ), belgeler ve sembol (`.pdb`) dosyaları | Derleme için referans olarak derleme ve çalışma zamanı olarak derleme derleme ler eklenir; `.xml` ve `.pdb` proje klasörlerine kopyalanır. Bkz. Çerçeve hedefe özgü alt klasörler oluşturmak için [birden çok hedef çerçeveyi destekleme.](supporting-multiple-target-frameworks.md) |
| ref/{tfm} | Verilen`.dll`Hedef Çerçeve`.pdb`Takma (TFM) için Montaj ( ), ve sembol ( ) dosyaları | Derlemeler yalnızca derleme süresi için referans olarak eklenir; Böylece hiçbir şey proje kutusu klasörüne kopyalanır. |
| Çalıştırma | Mimariye özgü`.dll`derleme (`.pdb`), sembolü`.pri`( ), ve yerel kaynak ( ) dosyaları | Derlemeler yalnızca çalışma süresi için başvuru olarak eklenir; diğer dosyalar proje klasörlerine kopyalanır. Her zaman ilgili derleme zaman `AnyCPU` derlemesağlamak `/ref/{tfm}` için klasör altında karşılık gelen (TFM) özel bir derleme olmalıdır. Bkz. [Birden çok hedef çerçeveyi destekleme.](supporting-multiple-target-frameworks.md) |
| content | Rasgele dosyalar | İçerikler proje köküne kopyalanır. **İçerik** klasörünü, sonuçta paketi tüketen hedef uygulamanın kökü olarak düşünün. Paketin uygulamanın */images* klasörüne bir resim eklemesini sağlamak için, paketin *içerik/resim* klasörüne yerleştirin. |
| derleme | *(3.x+)* MSBuild `.targets` `.props` ve dosyalar | Projeye otomatik olarak eklenir. |
| buildMultiTargeting | *(4.0+)* MSBuild `.targets` `.props` ve çerçeveler arası hedefleme için dosyalar | Projeye otomatik olarak eklenir. |
| buildGeçişive | *(5.0+)* MSBuild `.targets` `.props` ve herhangi bir tüketen projeye geçişli olarak akan dosyalar. [Özellik](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) sayfasına bakın. | Projeye otomatik olarak eklenir. |
| araçlar | Powershell komut dosyaları ve programlara Package Manager Konsolu'ndan erişilebiliyor | Klasör `tools` yalnızca Paket `PATH` Yöneticisi Konsolu için ortam değişkenine *not* eklenir `PATH` (özellikle, projeyi oluştururken MSBuild için ayarlanan aküme değil). |

Klasör yapınız herhangi bir sayıda hedef çerçeve için herhangi bir sayıda derleme içerebileceğinden, birden çok çerçeveyi destekleyen paketler oluştururken bu yöntem gereklidir.

Her durumda, istediğiniz klasör yapısını yerleştirdikten sonra, dosyayı oluşturmak için `.nuspec` bu klasörde aşağıdaki komutu çalıştırın:

```cli
nuget spec
```

Yine, oluşturulan `.nuspec` klasör yapısında dosyalara açık başvurular içerir. Paket oluşturulduğunda NuGet tüm dosyaları otomatik olarak içerir. Ancak, yine de bildirimin diğer bölümlerinde yer tutucu değerlerini de yapmanız gerekir.

### <a name="from-an-assembly-dll"></a>Bir montaj DLL gönderen

Derlemeden paket oluşturma basit durumda, aşağıdaki komutu `.nuspec` kullanarak derlemedeki meta verilerden bir dosya oluşturabilirsiniz:

```cli
nuget spec <assembly-name>.dll
```

Bu formu kullanmak, bildirimdeki birkaç yer tutucunun yerine derlemeden belirli değerler le birlikte çıkar. Örneğin, `<id>` özellik derleme adına ayarlanır ve `<version>` derleme sürümüne ayarlanır. Ancak, bildirimdeki diğer özellikler derlemede eşleşen değerlere sahip değildir ve bu nedenle yine de yer tutucular içerir.

### <a name="from-a-visual-studio-project"></a>Görsel Stüdyo projesinden

Bu `.nuspec` projeye `.csproj` yüklenen `.vbproj` diğer paketler otomatik olarak bağımlılık olarak başvurulduğundan, bir veya dosyadan bir dosya oluşturmak uygundur. Proje dosyasıyla aynı klasörde aşağıdaki komutu kullanmanız yeterlidir:

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

Ortaya çıkan `<project-name>.nuspec` dosya, paketleme sırasında projedeki değerlerle değiştirilen *belirteçler* içerir ve bu belirteçler, önceden yüklenmiş diğer paketlere yapılan atıflar da dahil olmak üzere.

*.nuspec'e*eklemek için paket bağımlılıklarınız `nuget pack`varsa, bunun yerine kullanın ve *.nuspec* dosyasını oluşturulan *.nupkg* dosyasının içinden alın. Örneğin, aşağıdaki komutu kullanın.

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget pack myproject.csproj
```

Bir belirteç, `$` proje özelliğinin her iki tarafındaki sembollerle sınırlandırılır. Örneğin, bu `<id>` şekilde oluşturulan bir bildirimdeki değer genellikle aşağıdaki gibi görünür:

```xml
<id>$id$</id>
```

Bu belirteç, paketleme `AssemblyName` sırasında proje dosyasındaki değerle değiştirilir. Proje değerlerinin `.nuspec` belirteçlere tam eşlenemi [için, Yedek Belirteçler başvurusuna](../reference/nuspec.md#replacement-tokens)bakın.

Belirteçler, projeyi `.nuspec` güncellediğiniz sürüm numarası gibi önemli değerleri güncelleştirmegereksinimini giderir. (İstenirse belirteçleri her zaman gerçek değerlerle değiştirebilirsiniz). 

Bir Visual Studio projesinde [çalışırken,.nupkg dosyasını](#run-nuget-pack-to-generate-the-nupkg-file) daha sonra oluşturmak için Running nuget paketinde açıklandığı gibi birkaç ek paketleme seçeneği nin mevcut olduğunu unutmayın.

#### <a name="solution-level-packages"></a>Çözüm düzeyinde paketler

*NuGet 2.x sadece. NuGet 3.0+ adresinde kullanılamaz.*

NuGet 2.x, Paket Yöneticisi Konsolu `tools` (klasörün içeriği) için araçlar veya ek komutlar yükleyen, ancak çözümdeki herhangi bir projeye referans, içerik eklemeyen veya özelleştirmeler oluşturmayan çözüm düzeyinde bir paket kavramını desteklemektedir. Bu tür paketler `lib`doğrudan , `content`, `build` veya klasörlerinde hiçbir dosya içermez ve `lib`bağımlılıklarının hiçbirinde ilgili , `content`veya `build` klasörlerinde dosya bulunmaz.

NuGet, yüklü çözüm düzeyi paketlerini `packages.config` projenin `.nuget` `packages.config` dosyası yerine klasördeki bir dosyada izler.

### <a name="new-file-with-default-values"></a>Varsayılan değerlere sahip yeni dosya

Aşağıdaki komut, uygun dosya yapısıyla başlamanızı sağlayan yer tutucularla varsayılan bir bildirim oluşturur:

```cli
nuget spec [<package-name>]
```

Paket adını \<\>atlarsanız, ortaya çıkan dosya `Package.nuspec`. Gibi bir ad `Contoso.Utility.UsefulStuff`sağlarsanız, dosya `Contoso.Utility.UsefulStuff.nuspec`.

Elde edilen `.nuspec` yer tutucular. `projectUrl` Son `.nupkg` dosyayı oluşturmak için kullanmadan önce dosyayı yeniden oluşturduğundan emin olun.

## <a name="choose-a-unique-package-identifier-and-setting-the-version-number"></a>Benzersiz bir paket tanımlayıcısı seçin ve sürüm numarasını ayarlama

Paket tanımlayıcısı (öğe)`<id>` ve sürüm numarası`<version>` (öğe) pakette bulunan tam kodu benzersiz olarak tanımladıkları için bildirimdeki en önemli iki değerdir.

**Paket tanımlayıcısı için en iyi uygulamalar:**

- **Teklik**: Tanımlayıcı, nuget.org veya pakete ev sahipliği yapan galeride benzersiz olmalıdır. Tanımlayıcıya karar vermeden önce, adın zaten kullanIlip kullanılmadığını kontrol etmek için ilgili galeride arama yapın. Çakışmaları önlemek için, iyi bir desen gibi tanımlayıcının ilk bölümü olarak şirket `Contoso.`adınızı kullanmaktır.
- **Ad alanı benzeri adlar**: Tire yerine nokta gösterimi kullanarak .NET'teki ad boşluklarına benzer bir desen izleyin. Örneğin, kullanmak `Contoso.Utility.UsefulStuff` yerine `Contoso-Utility-UsefulStuff` `Contoso_Utility_UsefulStuff`veya . Tüketiciler, paket tanımlayıcısı kodda kullanılan ad alanlarıyla eşleştiğinde de yararlı olur.
- **Örnek Paketler**: Başka bir paketin nasıl kullanılacağını gösteren bir `.Sample` örnek kod paketi üretirseniz, tanımlayıcıya sonek `Contoso.Utility.UsefulStuff.Sample`olarak iliştirin. (Örnek paket elbette diğer pakete bağımlı olacaktır.) Örnek bir paket oluştururken, daha önce açıklanan kural tabanlı çalışma dizini yöntemini kullanın. Klasörde, `content` örnek kodu ' da `\Samples\<identifier>` olarak `\Samples\Contoso.Utility.UsefulStuff.Sample`adlandırılan bir klasörde düzenleyin.

**Paket sürümü için en iyi uygulamalar:**

- Genel olarak, bu kesinlikle gerekli olmasa da, kitaplık maç için paketin sürümünü ayarlayın. Bu, bir paketi tek bir derlemeyle sınırladığınızda, [hangi derlemelerin paketlenecene karar](#decide-which-assemblies-to-package)verirken açıklandığı gibi basit bir konudur. Genel olarak, NuGet'in derleme sürümlerini değil, bağımlılıkları çözerken paket sürümleriyle ilgili olduğunu unutmayın.
- Standart olmayan bir sürüm şeması kullanırken, [Paket sürümde](../concepts/package-versioning.md)açıklandığı gibi NuGet sürüm kurallarını dikkate almayı unutmayın.

> Kısa blog gönderileri aşağıdaki dizi de sürüm anlamak için yararlıdır:
>
> - [Bölüm 1: DLL Hell alma](https://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [Bölüm 2: Çekirdek algoritması](https://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [Bölüm 3: Bağlayıcı Yönlendirmelerle Birleşme](https://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="add-a-readme-and-other-files"></a>Okuma mem ve diğer dosyalar ekleme

Pakete dahil olacak dosyaları doğrudan belirtmek `<files>` için, `.nuspec` `<metadata>` etiketi *izleyen* dosyadaki düğümü kullanın:

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
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
> Kural tabanlı çalışma dizini yaklaşımını kullanırken, readme.txt'yi paket köküne ve `content` diğer içeriğe klasöre yerleştirebilirsiniz. Bildirimde hiçbir öğe gerekli değildir. `<file>`

Paket köküne bir `readme.txt` dosya eklediğinizde, Visual Studio paketi doğrudan yükledikten hemen sonra dosyanın içeriğini düz metin olarak görüntüler. (Bağımlılık olarak yüklenen paketler için Okuma dosyaları görüntülenmez). Örneğin, HtmlAgilityPack paketinin okuma sı şu şekilde görünür:

![Yükleme üzerine NuGet paketi için okuma dosyasının görüntülenmesi](media/Create_01-ShowReadme.png)

> [!Note]
> Dosyaya boş `<files>` bir düğüm eklerseniz, NuGet `lib` pakete klasördekinden başka içerik eklemez. `.nuspec`

## <a name="include-msbuild-props-and-targets-in-a-package"></a>MSBuild sahne ve hedeflerini bir pakete dahil et

Bazı durumlarda, paketinizi tüketen projelere (örneğin, yapı sırasında özel bir araç veya işlem çalıştırmak gibi) özel yapı hedefleri veya özellikleri eklemek isteyebilirsiniz. `<package_id>.targets` Bunu, dosyaları projeye `<package_id>.props` veya (örneğin) `Contoso.Utility.UsefulStuff.targets`proje `\build` klasörüne yerleştirerek yaparsınız.

Kök `\build` klasördeki dosyalar tüm hedef çerçeveler için uygun kabul edilir. Çerçeveye özgü dosyaları sağlamak için, öncelikle bunları aşağıdakiler gibi uygun alt klasörlere yerleştirin:

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

Daha sonra `.nuspec` dosyada, `<files>` düğümdeki bu dosyalara başvurup bakın:

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

Bir pakette MSBuild sahne ve hedefleri dahil [NuGet 2.5 ile tanıtıldı](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), `minClientVersion="2.5"` bu nedenle `metadata` paketi tüketmek için gerekli minimum NuGet istemci sürümü belirtmek için, öğeözeklemek için tavsiye edilir.

NuGet `\build` dosyaları içeren bir paket yüklediğinde, `<Import>` proje dosyasına `.props` ve `.targets` dosyaları işaret eden MSBuild öğeleri ni ekler. (`.props` proje dosyasının üst kısmında eklenir; `.targets` alt kısmında eklenir.) Her hedef çerçeve `<Import>` için ayrı bir koşullu MSBuild öğesi eklenir.

MSBuild `.props` `.targets` ve çerçeveler arası hedefleme dosyaları `\buildMultiTargeting` klasöre yerleştirilebilir. Paket yükleme sırasında NuGet, `<Import>` hedef çerçevenin ayarlanmadığını (MSBuild özelliğinin `$(TargetFramework)` boş olması gerekir) koşuluyla proje dosyasına karşılık gelen öğeleri ekler.

NuGet 3.x ile hedefler projeye eklenmez, bunun `{projectName}.nuget.g.targets` yerine `{projectName}.nuget.g.props`kullanılabilir hale getirilir ve .

## <a name="run-nuget-pack-to-generate-the-nupkg-file"></a>.nupkg dosyasını oluşturmak için nuget paketini çalıştırın

Bir derleme veya kural tabanlı çalışma dizini kullanırken, `nuget pack` dosyanızla `.nuspec` birlikte `<project-name>` çalışarak, belirli dosya adınızı değiştirerek bir paket oluşturun:

```cli
nuget pack <project-name>.nuspec
```

Visual Studio projesi kullanırken, proje `nuget pack` `.nuspec` dosyasını otomatik olarak yükleyen ve proje dosyasındaki değerleri kullanarak içindeki belirteçleri değiştiren proje dosyanızla çalıştırın:

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> Proje belirteç değerlerinin kaynağı olduğundan, proje dosyasının doğrudan belirteç değişimi için kullanılması gereklidir. Bir `nuget pack` `.nuspec` dosyayla kullanırsanız belirteç değiştirme gerçekleşmez.

Her durumda, `nuget pack` bir dönemle başlayan klasörleri hariç `.git` `.hg`tutar, örneğin.

NuGet, `.nuspec` dosyada düzeltmesi gereken (örneğin, bildirimdeki yer tutucu değerlerini değiştirmeyi unutmagibi) herhangi bir hata olup olmadığını gösterir.

Başarılı `nuget pack` olduktan sonra, `.nupkg` [Paketi Yayımlama'da](../nuget-org/publish-a-package.md)açıklandığı gibi uygun bir galeride yayımlayabileceğiniz bir dosyanız vardır.

> [!Tip]
> Bir paketi oluşturduktan sonra incelemenin yararlı bir yolu, [paketi Paket Gezgini](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) aracında açmaktır. Bu, paket içeriğinin ve manifestosunun grafiksel bir görünümünü sağlar. Ayrıca, ortaya çıkan `.nupkg` dosyayı bir `.zip` dosyaya yeniden adlandırabilir ve içeriğini doğrudan keşfedebilirsiniz.

### <a name="additional-options"></a>Ek seçenekler

Dosyaları hariç tutmak, bildirimdeki `nuget pack` sürüm numarasını geçersiz kılmak ve diğer özelliklerin yanı sıra çıktı klasörünü değiştirmek için çeşitli komut satırı anahtarlarını kullanabilirsiniz. Tam liste için paket [komutu başvurusuna](../reference/cli-reference/cli-ref-pack.md)bakın.

Aşağıdaki seçenekler Visual Studio projeleri ile ortak birkaçıdır:

- **Başvurulan projeler**: Proje diğer projelere başvuruyorsa, başvurulan projeleri paketin bir parçası olarak `-IncludeReferencedProjects` veya bağımlılık olarak, seçeneği kullanarak ekleyebilirsiniz:

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    Bu ekleme işlemi özyinelemelidir, `MyProject.csproj` bu nedenle başvurular B ve C projeleri yse ve bu projeler D, E ve F'ye başvuruyorsa, B, C, D, E ve F'den dosyalar pakete dahil edilir.

    Başvurulan bir `.nuspec` proje kendi dosyasını içeriyorsa, NuGet başvurulan projeyi bağımlılık olarak ekler.  Bu projeyi ayrı olarak paketlemeniz ve yayınlamanız gerekir.

- **Yapı yapılandırması**: NuGet varsayılan olarak proje dosyasındaki varsayılan yapı yapılandırma kümesini kullanır, genellikle *Hata Ayıklama.* *Sürüm*gibi farklı bir yapı yapılandırmasından dosyaları `-properties` paketlemek için yapılandırma seçeneğini kullanın:

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- **Semboller**: tüketicilerin paket kodunuzu hata ayıklayıcıya eklemesine olanak `-Symbols` tanıyan sembolleri eklemek için aşağıdaki seçeneği kullanın:

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="test-package-installation"></a>Test paketi kurulumu

Paket yayımlamadan önce, genellikle bir projeye paket yükleme işlemini sınamak istersiniz. Testler, zorunlu dosyaların tümünden inin projedeki doğru yerlerinde sonunun olmasını sağlar.

Yüklemeleri Visual Studio'da veya komut satırında normal [paket yükleme adımlarını](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package)kullanarak el ile test edebilirsiniz.

Otomatik sınama için temel işlem aşağıdaki gibidir:

1. Dosyayı `.nupkg` yerel bir klasöre kopyalayın.
1. Komutu kullanarak `nuget sources add -name <name> -source <path>` klasörü paket kaynaklarınıza ekleyin [(nuget kaynaklarına](../reference/cli-reference/cli-ref-sources.md)bakın). Bu yerel kaynağı herhangi bir bilgisayarda yalnızca bir kez ayarlamanız gerektiğini unutmayın.
1. Verilen kaynağınızın adı `nuget install <packageID> -source <name>` ile `<name>` eşleşen bir yerde kullanarak `nuget sources`paketi o kaynaktan yükleyin. Kaynağın belirtilmesi, paketin tek başına o kaynaktan yüklenmesini sağlar.
1. Dosyaların doğru yüklenmesini denetlemek için dosya sisteminizi inceleyin.

## <a name="next-steps"></a>Sonraki Adımlar

Bir dosya olan bir `.nupkg` paket oluşturduktan sonra, paketi [Yayımlama'da](../nuget-org/publish-a-package.md)açıklandığı gibi istediğiniz galeride yayınlayabilirsiniz.

Ayrıca paketinizin yeteneklerini genişletmek veya aşağıdaki konularda açıklandığı gibi diğer senaryoları desteklemek de isteyebilirsiniz:

- [Paket sürüm](../concepts/package-versioning.md)
- [Birden çok hedef çerçeveyi destekleme](../create-packages/supporting-multiple-target-frameworks.md)
- [Kaynak ve yapılandırma dosyalarının dönüşümleri](../create-packages/source-and-config-file-transformations.md)
- [Yerelleştirme](../create-packages/creating-localized-packages.md)
- [Ön sürüm sürümleri](../create-packages/prerelease-packages.md)
- [Paket türünü ayarlama](../create-packages/set-package-type.md)
- [COM interop montajları ile paketler oluşturma](../create-packages/author-packages-with-COM-interop-assemblies.md)

Son olarak, dikkat edilmesi gereken ek paket türleri vardır:

- [Yerli Paketler](../guides/native-packages.md)
- [Sembol Paketleri](../create-packages/symbol-packages-snupkg.md)
