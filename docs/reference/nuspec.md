---
title: NuGet için. nuspec dosya başvurusu
description: . Nuspec dosyası, bir paket oluştururken ve paket tüketicilere bilgi sağlamak için kullanılan paket meta verilerini içerir.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: f931ed297a6a1e9e24ce5eb30a8158f59925bb39
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488678"
---
# <a name="nuspec-reference"></a>. nuspec başvurusu

`.nuspec` Dosya, paket meta verilerini içeren bir XML bildirimidir. Bu bildirim her ikisi de paketini derlemek ve tüketicilere bilgi sağlamak için kullanılır. Bildirim her zaman bir pakete dahildir.

Bu konuda:

- [Genel form ve şema](#general-form-and-schema)
- [Değiştirme belirteçleri](#replacement-tokens) (bir Visual Studio projesiyle kullanıldığında)
- [Bağımlılıklar](#dependencies)
- [Açık bütünleştirilmiş kod başvuruları](#explicit-assembly-references)
- [Framework derleme başvuruları](#framework-assembly-references)
- [Derleme dosyalarını dahil etme](#including-assembly-files)
- [İçerik dosyalarını dahil etme](#including-content-files)
- [Örnek nuspec dosyaları](#example-nuspec-files)

## <a name="project-type-compatibility"></a>Proje türü uyumluluğu

- Kullanan `.nuspec` SDK `nuget.exe pack` olmayan projeler`packages.config`için ile kullanın.

- `.nuspec` [SDK stilindeki projelere](../resources/check-project-format.md) yönelik paketler oluşturmak için bir dosya gerekli değildir (genellikle .NET Core ve [SDK özniteliğini](/dotnet/core/tools/csproj#additions)kullanan .NET Standard projeler). (Paketi oluşturduğunuzda bir `.nuspec` ' nin oluşturulduğunu unutmayın.)

   Veya `dotnet.exe pack` kullanarak`msbuild pack target`bir paket oluşturuyorsanız, bunun yerine genellikle proje dosyasındaki `.nuspec` dosyada bulunan [tüm özellikleri dahil](../reference/msbuild-targets.md#pack-target) etmenizi öneririz. Ancak, bunun yerine [veya `.nuspec` `dotnet.exe` `msbuild pack target`kullanarak paketbir dosya kullanmayı ](../reference/msbuild-targets.md#packing-using-a-nuspec)seçebilirsiniz.

- ' Den `packages.config` [packagereference](../consume-packages/package-references-in-project-files.md)'a geçirilen projeler için, `.nuspec` paketi oluşturmak için bir dosya gerekli değildir. Bunun yerine, [MSBuild-t:Pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration)kullanın.

## <a name="general-form-and-schema"></a>Genel form ve şema

Geçerli `nuspec.xsd` şema dosyası [NuGet GitHub deposunda](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd)bulunabilir.

Bu şema içinde, bir `.nuspec` dosya aşağıdaki genel biçime sahiptir:

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- Required elements-->
        <id></id>
        <version></version>
        <description></description>
        <authors></authors>

        <!-- Optional elements -->
        <!-- ... -->
    </metadata>
    <!-- Optional 'files' node -->
</package>
```

Şemanın net bir görsel temsili için, şema dosyasını Visual Studio 'da tasarım modunda açın ve **XML şema Gezgini** bağlantısına tıklayın. Alternatif olarak, dosyayı kod olarak açın, düzenleyicide sağ tıklayın ve **XML şeması Gezginini göster**' i seçin. Aşağıdakilerden biri gibi bir görünüm alacağınız şekilde (çoğunlukla genişletilir):

![Nuspec. xsd Open ile Visual Studio şema Gezgini](media/SchemaExplorer.png)

### <a name="required-metadata-elements"></a>Gerekli meta veri öğeleri

Aşağıdaki öğeler bir paket için en düşük gereksinimlerdir, ancak geliştiricilerin paketinize sahip olduğu genel deneyimi geliştirmek için [isteğe bağlı meta veri öğelerini](#optional-metadata-elements) eklemeyi göz önünde bulundurmanız gerekir. 

Bu öğelerin bir `<metadata>` öğesi içinde görünmesi gerekir.

#### <a name="id"></a>kimlik 
Nuget.org genelinde benzersiz olması gereken büyük/küçük harf duyarsız paket tanımlayıcısı veya paketin bulunduğu Galeri. Kimlikler, URL için geçerli olmayan boşluk veya karakterler içeremez ve genellikle .NET ad alanı kurallarını izler. Bkz. rehberlik için [benzersiz bir paket tanımlayıcısı seçme](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) .
#### <a name="version"></a>sürüm
*Ana. Minor. Patch* deseninin ardından paketin sürümü. Sürüm numaraları, [paket sürümü oluşturma](../concepts/package-versioning.md#pre-release-versions)bölümünde açıklandığı gibi bir ön sürüm son eki içerebilir. 
#### <a name="description"></a>açıklama
UI görüntüleme paketinin uzun açıklaması. 
#### <a name="authors"></a>düzenliyor
Nuget.org üzerindeki profil adlarıyla eşleşen paket yazarları için virgülle ayrılmış bir liste. Bunlar, nuget.org üzerindeki NuGet galerisinde görüntülenir ve aynı yazarlara göre çapraz başvuru için kullanılır. 

### <a name="optional-metadata-elements"></a>İsteğe bağlı meta veri öğeleri

#### <a name="owners"></a>lere
Nuget.org üzerindeki profil adlarını kullanan paket oluşturucularının virgülle ayrılmış listesi. Bu, genellikle ile aynı listeyle `authors`aynıdır ve paket NuGet.org 'e yüklenirken yok sayılır. Bkz. [NuGet.org üzerinde paket sahiplerini yönetme](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg). 

#### <a name="projecturl"></a>projectUrl
Genellikle kullanıcı arabiriminde gösterildiği gibi, paketin ana sayfası için bir URL de nuget.org görüntülenir. 

#### <a name="licenseurl"></a>licenseUrl
> [!Important]
> licenseUrl kullanım dışı bırakılıyor. Bunun yerine lisans kullanın.

Genellikle Unuget.org gibi gösterilen paket lisansının URL 'SI.

#### <a name="license"></a>lisan
Bir SPDX lisans ifadesi veya paket içindeki bir lisans dosyasının yolu, genellikle Usıs nuget.org gibidir. Paketi MıT veya BSD-2 yan tümcesi gibi ortak bir lisans altında lisansladıysanız, ilişkili [Spdx lisans tanımlayıcısını](https://spdx.org/licenses/)kullanın. Örneğin:

`<license type="expression">MIT</license>`

> [!Note]
> NuGet.org yalnızca açık kaynak girişimi veya ücretsiz yazılım temeli tarafından onaylanan lisans ifadelerini kabul eder.

Paketinizin birden çok ortak lisans kapsamında lisansı varsa, [Spdx Expression sözdizimi 2,0 sürümünü](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60)kullanarak bileşik bir lisans belirtebilirsiniz. Örneğin:

`<license type="expression">BSD-2-Clause OR MIT</license>`

Lisans ifadeleri tarafından desteklenmeyen özel bir lisans kullanıyorsanız, lisans metniyle bir `.txt` veya `.md` dosyasını paketleyebilir. Örneğin:

```xml
<package>
  <metadata>
    ...
    <license type="file">LICENSE.txt</license>
    ...
  </metadata>
  <files>
    ...
    <file src="licenses\LICENSE.txt" target="" />
    ...
  </files>
</package>
```

MSBuild eşdeğeri için [Lisans ifadesi veya lisans dosyası paketleme](msbuild-targets.md#packing-a-license-expression-or-a-license-file)konusuna göz atın.

NuGet 'in lisans ifadelerinin tam sözdizimi aşağıda, [Abnf](https://tools.ietf.org/html/rfc5234)' de açıklanmıştır.
```cli
license-id            = <short form license identifier from https://spdx.org/spdx-specification-21-web-version#h.luq9dgcle9mo>

license-exception-id  = <short form license exception identifier from https://spdx.org/spdx-specification-21-web-version#h.ruv3yl8g6czd>

simple-expression = license-id / license-id”+”

compound-expression =  1*1(simple-expression /
                simple-expression "WITH" license-exception-id /
                compound-expression "AND" compound-expression /
                compound-expression "OR" compound-expression ) /                
                "(" compound-expression ")" )

license-expression =  1*1(simple-expression / compound-expression / UNLICENSED)
```

#### <a name="iconurl"></a>Iurl
Kullanıcı arabirimi görüntüsündeki paketin simgesi olarak kullanılacak saydam arka planlı bir 64x64 görüntüsünün URL 'SI. Bu öğenin, görüntüyü içeren bir Web sayfasının URL 'sini değil *doğrudan görüntü URL* 'sini içerdiğinden emin olun. Örneğin, GitHub 'dan bir görüntü kullanmak için, gibi <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>ham dosya URL 'sini kullanın. 

#### <a name="requirelicenseacceptance"></a>Requirelicensekabulünü
İstemcinin paketi yüklemeden önce, tüketicinin paket lisansını kabul etmesini isteyip istemeyeceğini belirten bir Boole değeri.

#### <a name="developmentdependency"></a>developmentDependency
*(2.8+)* Paket olup olmadığını belirten bir Boole değeri, bir geliştirme-yalnızca-paket bağımlılık diğer paketleri olarak eklenmesini engelleyen bağımlılık olarak işaretlenir. PackageReference (NuGet 4.8 +) ile bu bayrak Ayrıca derleme zamanı varlıklarını derlemeden dışlayacak anlamına gelir. [PackageReference için bkz. Developmentdependency desteği](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)

#### <a name="summary"></a>özet
UI görüntülemesi için paketin kısa bir açıklaması. Atlanırsa, kesilen bir sürümü `description` kullanılır.

#### <a name="releasenotes"></a>relet 'ler
*(1.5+)* Kullanıcı arabiriminde gibi sık kullanılan paketin bu sürümde yapılan değişikliklerin bir açıklaması **güncelleştirmeleri** sekmesini, Visual Studio Paket Yöneticisi ve Paket açıklaması yerine.

#### <a name="copyright"></a>telif hakkı
*(1.5+)* Ayrıntıları paketi için telif hakkı.

#### <a name="language"></a>dil
Paket için yerel ayar KIMLIĞI. Bkz. [yerelleştirilmiş paketler oluşturma](../create-packages/creating-localized-packages.md).

#### <a name="tags"></a>etiketler
Paketi tanımlayan ve arama ve filtreleme aracılığıyla paketlerin bulunabilirliğini sağlayan, boşlukla ayrılmış etiketlerin ve anahtar kelimelerin bir listesi. 

#### <a name="serviceable"></a>hizmet verebilir 
*(3.3+)* Yalnızca iç NuGet için kullanın.

#### <a name="repository"></a>depo
Dört isteğe bağlı öznitelikten oluşan depo meta verileri `type` : `url` ve *(4.0 +)* ve `branch` ve `commit` *(4.6 +)* . Bu öznitelikler, `.nupkg` kendisini oluşturan depoya eşlemenize olanak tanır. Bu, tek bir dal adı olarak daha ayrıntılı bir şekilde ele alınır ve/veya paketi oluşturan SHA-1 karmasını işleyin. Bu, doğrudan bir sürüm denetim yazılımıyla çağrılabilen, genel olarak kullanılabilir bir URL olmalıdır. Bu, bilgisayar için amaçlanmış olduğu için bir HTML sayfası olmamalıdır. Proje sayfasına bağlantı için, bunun yerine `projectUrl` alanını kullanın.

Örneğin:
```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2016/06/nuspec.xsd">
    <metadata>
        ...
        <repository type="git" url="https://github.com/NuGet/NuGet.Client.git" branch="dev" commit="e1c65e4524cd70ee6e22abe33e6cb6ec73938cb3" />
        ...
    </metadata>
</package>
```

#### <a name="title"></a>title
Paketin bazı Kullanıcı arabiriminde kullanılabilen, okunabilir bir başlığı. (nuget.org ve Visual Studio 'da Paket Yöneticisi başlık gösterme)

#### <a name="collection-elements"></a>Koleksiyon öğeleri

#### <a name="packagetypes"></a>packageTypes
*(3,5 +)* Geleneksel bir bağımlılık paketi dışında paketin `<packageType>` türünü belirten sıfır veya daha fazla öğe koleksiyonu. Her packageType 'ın *ad* ve *Sürüm*öznitelikleri vardır. Bkz. [paket türünü ayarlama](../create-packages/set-package-type.md).
#### <a name="dependencies"></a>bağımlılıklar
Paketin bağımlılıklarını belirten sıfır veya daha `<dependency>` fazla öğe koleksiyonu. Her bağımlılığın *kimliği*, *sürümü*, *içerme* (3. x +) ve *exclude* (3. x +) öznitelikleri vardır. Aşağıdaki [bağımlılıklara](#dependencies-element) bakın.
#### <a name="frameworkassemblies"></a>frameworkAssemblies
*(1.2 +)* Bu paketin gerektirdiği .NET Framework bütünleştirilmiş kod `<frameworkAssembly>` başvurularını tanımlayan sıfır veya daha fazla öğe koleksiyonu, bu, başvuruların paketi kullanan projelere eklenmesini sağlar. Her frameworkAssembly *AssemblyName* ve *TargetFramework* öznitelikleri vardır. Aşağıdaki [Framework derleme BAŞVURULARı GAC 'Yi belirtme](#specifying-framework-assembly-references-gac) bölümüne bakın. |
#### <a name="references"></a>başvurular
*(1,5 +)* Paket klasöründeki, proje başvuruları olarak `<reference>` eklenen derlemeleri adlandırarak sıfır veya daha fazla öğe koleksiyonu. `lib` Her başvurunun bir *Dosya* özniteliği vardır. `<references>`Ayrıca, öğeleri içeren `<group>` `<reference>` bir *TargetFramework* özniteliği içeren bir öğe içerebilir. Atlanırsa, içindeki `lib` tüm başvurular dahil edilir. Aşağıda [Açık derleme başvurularını belirtme](#specifying-explicit-assembly-references) bölümüne bakın.
#### <a name="contentfiles"></a>contentFiles
*(3.3 +)* Tüketim projesinde içerilecek `<files>` içerik dosyalarını tanımlayan öğelerin koleksiyonu. Bu dosyalar, proje sistemi içinde nasıl kullanılması gerektiğini betimleyen bir öznitelikler kümesiyle belirtilmiştir. Aşağıdaki [pakete dahil edilecek dosyaları belirtme](#specifying-files-to-include-in-the-package) bölümüne bakın.
#### <a name="files"></a>dosyaları 
`<metadata>` `<files>` `<metadata>` `<contentFiles>` Düğüm, pakete dahil edilecek derleme ve içerik dosyalarını belirtmek için eşdüzey öğesi olarak bir düğüm ve altında bir alt öğe içerebilir. `<package>` Ayrıntılar için bu konunun ilerleyen kısımlarında [derleme dosyalarını](#including-assembly-files) ve [içerik dosyalarını](#including-content-files) dahil etme bölümüne bakın.

### <a name="metadata-attributes"></a>meta veri öznitelikleri

#### <a name="minclientversion"></a>minClientVersion
NuGet. exe ve Visual Studio Paket Yöneticisi tarafından zorlanan, bu paketi yükleyesağlayan NuGet istemcisinin en düşük sürümünü belirtir. Bu, paket, NuGet istemcisinin belirli bir sürümünde eklenmiş olan `.nuspec` dosyanın belirli özelliklerine bağlı olduğunda kullanılır. Örneğin, `developmentDependency` özniteliğini kullanan bir paket için `minClientVersion`"2,8" belirtmelidir. Benzer şekilde, `contentFiles` öğesini kullanan bir paket (sonraki bölüme bakın) "3,3" `minClientVersion` olarak ayarlanmalıdır. Ayrıca, 2,5 ' den önceki NuGet istemcileri bu bayrağı tanımadığı için, *her zaman* ne `minClientVersion` içermesi gerektiğine bakılmaksızın paketi yüklemeyi reddeder.

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/01/nuspec.xsd">
    <metadata minClientVersion="100.0.0.1">
        <id>dasdas</id>
        <version>2.0.0</version>
        <title />
        <authors>dsadas</authors>
        <owners />
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>My package description.</description>
    </metadata>
    <files>
        <file src="content\one.txt" target="content\one.txt" />
    </files>
</package>
```

## <a name="replacement-tokens"></a>Değiştirme belirteçleri

Bir paket oluştururken, `.nuspec` [ `nuget pack` komut](../reference/cli-reference/cli-ref-pack.md) dosyanın `<metadata>` düğümündeki $-Delimited belirteçlerini bir proje dosyasından veya `pack` komutun `-properties` anahtarından değiştirir.

Komut satırında belirteç değerlerini ile `nuget pack -properties <name>=<value>;<name>=<value>`belirtirsiniz. Örneğin, `$owners$` ve `$desc$` içinde `.nuspec` gibi bir belirteç kullanabilir ve değerlerini paketleme zamanında aşağıdaki şekilde sağlayabilirsiniz:

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

Bir projeden değerleri kullanmak için, aşağıdaki tabloda açıklanan belirteçleri belirtin (AssemblyInfo, dosyanın `Properties` `AssemblyInfo.cs` veya `AssemblyInfo.vb`gibi).

Bu belirteçleri kullanmak için, `nuget pack` `.nuspec`yalnızca yerine proje dosyası ile çalıştırın. Örneğin, `$id$` aşağıdaki komutu kullanırken, bir `.nuspec` dosyadaki ve `$version$` belirteçleri proje `AssemblyName` ve `AssemblyVersion` değerleriyle değiştirilmiştir:

```ps
nuget pack MyProject.csproj
```

Genellikle, bir projeniz olduğunda, bu standart belirteçlerden bazılarını `.nuspec` otomatik olarak `nuget spec MyProject.csproj` içeren ilk kullanımı oluşturursunuz. Ancak, bir proje gerekli `.nuspec` öğeler için değerler eksikse `nuget pack` , başarısız olur. Ayrıca, proje değerlerini değiştirirseniz, paketi oluşturmadan önce yeniden oluşturmayı unutmayın; Bu, paket komutunun `build` anahtarıyla kolayca yapılabilir.

Özel durumu `$configuration$`ile, projedeki değerler, komut satırında aynı belirtece atanmış herhangi bir tercih halinde kullanılır.

| Belirteç | Değer kaynağı | Değer
| --- | --- | ---
| **$id $** | Proje dosyası | Proje dosyasından AssemblyName (title) |
| **$version $** | AssemblyInfo | Varsa Assemblyformationalversion, yoksa AssemblyVersion |
| **$author $** | AssemblyInfo | AssemblyCompany |
| **$title $** | AssemblyInfo | AssemblyTitle |
| **$description $** | AssemblyInfo | AssemblyDescription |
| **$copyright $** | AssemblyInfo | Assemblytelif hakkı |
| **$configuration $** | Derleme DLL 'SI | Derlemeyi oluşturmak için kullanılan yapılandırma, hata ayıklamayı varsayılan olarak ayarlanıyor. Yayın yapılandırması kullanarak bir paket oluşturmak için her zaman komut satırında ' ı kullanın `-properties Configuration=Release` . |

Belirteçler, [derleme dosyalarını](#including-assembly-files) ve [içerik dosyalarını](#including-content-files)dahil ettiğinizde yolları çözümlemek için de kullanılabilir. Belirteçler, MSBuild özellikleriyle aynı adlara sahiptir ve geçerli derleme yapılandırmasına bağlı olarak dahil edilecek dosyaları seçmenizi mümkün hale getirir. Örneğin, `.nuspec` dosyasında aşağıdaki belirteçleri kullanıyorsanız:

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

`AssemblyName` Ve MSBuild `LoggingLibrary` 'deyapılandırma`Release` ile olan bir derleme oluşturduğunuzda, paketteki dosyadakisonuççizgileriaşağıdakigibidir:`.nuspec`

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a>Dependencies öğesi

`<dependency>` İçindeki `<dependencies>` öğesi,üstdüzeypaketinbağımlıolduğudiğerpaketleritanımlayanherhangibirsayıdaöğeiçerir.`<metadata>` Her biri `<dependency>` için öznitelikleri aşağıdaki gibidir:

| Öznitelik | Açıklama |
| --- | --- |
| `id` | Istenir "EntityFramework" ve "NUnit" gibi bağımlılığın paket KIMLIĞI, nuget.org paketinin adı bir paket sayfasında gösterilmektedir. |
| `version` | Istenir Bağımlılık olarak kabul edilebilir sürüm aralığı. Tam sözdizimi için [paket sürümü oluşturma](../concepts/package-versioning.md#version-ranges-and-wildcards) bölümüne bakın. Joker karakter (kayan) sürümleri desteklenmez. |
| include | Son pakete dahil edilecek bağımlılığı belirten, etiketleri ekle/çıkar (aşağıya bakın) listesi. Varsayılan değer `all` şeklindedir. |
| exclude | Son pakette hariç tutulacak bağımlılığı belirten, etiketleri dahil et/hariç tut (aşağıya bakın) listesi. Varsayılan değer `build,analyzers` , üzerine yazılabilir. Ancak `content/ ContentFiles` , üzerine yazılabilir olmayan son pakette da örtük olarak hariç tutulur. İle belirtilen Etiketler `exclude` , ile `include`belirtilen değerlere göre önceliğe sahip olacak şekilde belirlenir. Örneğin, `include="runtime, compile" exclude="compile"` ile `include="runtime"`aynıdır. |

| Dahil etme/hariç tutma etiketi | Hedefin etkilenen klasörleri |
| --- | --- |
| contentFiles | İçerik |
| çalışma zamanı | Çalışma zamanı, kaynaklar ve FrameworkAssemblies |
| se | LIB |
| derleme | Build (MSBuild props ve targets) |
| yerel | yerel |
| yok | Klasör yok |
| tüm | Tüm klasörler |

Örneğin, aşağıdaki satırlar `PackageA` sürüm 1.1.0 veya üzeri ve `PackageB` sürüm 1. x bağımlılıklarını gösterir.

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

Aşağıdaki satırlar aynı paketlere `contentFiles` `PackageA` `build` `PackageB`yönelik bağımlılıklarıgösterir,ancakveklasörlerininyanısıra,veklasörlerinindadahiledileceğinibelirtir.`native` `compile`

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

> [!Important]
> `.nuspec` Kullanarak `.nuspec` birprojedenoluştururken,buprojedevarolanbağımlılıklareldeedilendosyayaotomatikolarakeklenmez.`nuget spec` Bunun yerine, `nuget pack myproject.csproj`öğesini kullanın ve oluşturulan *. nupkg* dosyasının içinden *. nuspec* dosyasını alın. Bu *. nuspec* , bağımlılıkları içerir.

### <a name="dependency-groups"></a>Bağımlılık grupları

*Sürüm 2.0 +*

Tek bir düz listeye alternatif olarak, bağımlılıklar içindeki `<group>` `<dependencies>`öğeleri kullanarak hedef projenin çerçeve profiline göre belirtilebilir.

Her grup adlı `targetFramework` bir özniteliğe sahiptir ve sıfır veya daha fazla `<dependency>` öğe içerir. Hedef Framework, projenin çerçeve profiliyle uyumlu olduğunda bu bağımlılıklar birlikte yüklenir.

Özniteliği olmayan öğe, bağımlılıkların varsayılan veya geri dönüş listesi olarak kullanılır. `<group>` `targetFramework` Tam çerçeve tanımlayıcıları için bkz. [hedef çerçeveler](../reference/target-frameworks.md) .

> [!Important]
> Grup biçimi düz bir liste ile birlikte karıştırılamaz.

Aşağıdaki örnek, `<group>` öğesinin farklı çeşitlemelerini göstermektedir:

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" version="1.6.2" />
        <dependency id="WebActivator" version="1.4.4" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a>Açık bütünleştirilmiş kod başvuruları

Öğesi, paket kullanılırken hedef projenin başvurması `packages.config` gereken derlemeleri açıkça belirtmek için kullanan projeler tarafından kullanılır. `<references>` Açık başvurular genellikle yalnızca tasarım zamanı derlemeler için kullanılır. Daha fazla bilgi için bkz. [projeler tarafından başvurulan derlemeleri seçme](../create-packages/select-assemblies-referenced-by-projects.md) hakkında daha fazla bilgi için bu sayfaya bakın.

Örneğin, aşağıdaki `<references>` öğe, NuGet 'e `xunit.extensions.dll` yalnızca `xunit.dll` başvuru eklemesi için, pakette ek derlemeler olsa bile:

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a>Başvuru grupları

Tek bir düz listeye alternatif olarak, başvurular, içindeki `<group>` `<references>`öğeleri kullanarak hedef projenin çerçeve profiline göre belirtilebilir.

Her grup adlı `targetFramework` bir özniteliğe sahiptir ve sıfır veya daha fazla `<reference>` öğe içerir. Hedef çerçeve projenin çerçeve profiliyle uyumluysa, bu başvurular bir projeye eklenir.

Özniteliği olmayan öğe, başvuru varsayılan veya geri dönüş listesi olarak kullanılır. `<group>` `targetFramework` Tam çerçeve tanımlayıcıları için bkz. [hedef çerçeveler](../reference/target-frameworks.md) .

> [!Important]
> Grup biçimi düz bir liste ile birlikte karıştırılamaz.

Aşağıdaki örnek, `<group>` öğesinin farklı çeşitlemelerini göstermektedir:

```xml
<references>
    <group>
        <reference file="a.dll" />
    </group>

    <group targetFramework="net45">
        <reference file="b45.dll" />
    </group>

    <group targetFramework="netcore45">
        <reference file="bcore45.dll" />
    </group>
</references>
```

<a name="specifying-framework-assembly-references-gac"></a>

## <a name="framework-assembly-references"></a>Framework derleme başvuruları

Framework derlemeleri, .NET Framework 'ün bir parçası olan ve belirli bir makine için genel derleme önbelleğinde (GAC) olması gereken olanlardır. Bir paket, `<frameworkAssemblies>` öğesi içindeki bu derlemeleri tanımlayarak, gerekli başvuruların projenin bu tür başvurularına sahip olmadığı olayda bir projeye eklendiğinden emin olabilir. Kuşkusuz bu tür derlemeler doğrudan bir pakete dahil edilmez.

Öğesi, her biri aşağıdaki öznitelikleri `<frameworkAssembly>` belirten sıfır veya daha fazla öğe içeriyor: `<frameworkAssemblies>`

| Öznitelik | Açıklama |
| --- | --- |
| **assemblyName** | Istenir Tam nitelikli derleme adı. |
| **targetFramework** | Seçim Bu başvurunun uygulandığı hedef çerçeveyi belirtir. Atlanırsa, başvurunun tüm çerçeveler için geçerli olduğunu gösterir. Tam çerçeve tanımlayıcıları için bkz. [hedef çerçeveler](../reference/target-frameworks.md) . |

Aşağıdaki örnekte, tüm hedef çerçeveler `System.Net` için bir başvuru ve yalnızca .NET Framework 4,0 `System.ServiceModel` için bir başvuru gösterilmektedir:

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a>Derleme dosyalarını dahil etme

[Paket oluşturma](../create-packages/creating-a-package.md)bölümünde açıklanan kuralları izlerseniz, `.nuspec` dosyadaki dosyaların listesini açıkça belirtmeniz gerekmez. Komut `nuget pack` , gerekli dosyaları otomatik olarak seçer.

> [!Important]
> Bir paket projeye yüklendiğinde NuGet otomatik olarak paketin dll 'lerine derleme başvuruları ekler, `.resources.dll` çünkü bu, yerelleştirilmiş uydu derlemeleri oldukları varsayılacaktır. Bu nedenle, başka bir şekilde `.resources.dll` temel paket kodu içeren dosyalar için kullanmaktan kaçının.

Bu otomatik davranışı atlamak ve bir pakete hangi dosyaların ekleneceğini açıkça denetlemek `<files>` için, bir öğeyi bir `<package>` alt öğesi `<metadata>`(ve eşdüzey) olarak yerleştirin ve her bir dosyayı ayrı `<file>` bir öğeyle tanımlayarak. Örneğin:

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

NuGet 2. x ve öncesiyle ve kullanan `packages.config` `<files>` projelerde, bir paket yüklendiğinde değişmez içerik dosyalarını dahil etmek için de kullanılır. NuGet 3.3 + ve projeleri packagereference ile, `<contentFiles>` bunun yerine öğesi kullanılır. Ayrıntılar için aşağıdaki [içerik dosyalarını ekleme](#including-content-files) bölümüne bakın.

### <a name="file-element-attributes"></a>Dosya öğesi öznitelikleri

Her `<file>` öğe aşağıdaki öznitelikleri belirtir:

| Öznitelik | Açıklama |
| --- | --- |
| **YN** | `exclude` Özniteliği tarafından belirtilen Dışlamalar ile ilgili olarak içerilecek dosyanın veya dosyaların konumu. Mutlak bir yol belirtilmediği takdirde yol `.nuspec` dosyayla ilişkilidir. Joker karaktere `*` izin verilir ve çift joker `**` karakter özyinelemeli bir klasör aramasını ifade etmenizi gerektirir. |
| **hedef** | Kaynak dosyaların yerleştirildiği,, `lib`, veya `tools`ile `content` `build`başlaması gereken paket içindeki klasörün göreli yolu. Bkz. [kural tabanlı çalışma dizininden. nuspec oluşturma](../create-packages/creating-a-package.md#from-a-convention-based-working-directory). |
| **amaz** | `src` Konumdan hariç tutulacak dosyaların veya dosya desenlerinin noktalı virgülle ayrılmış listesi. Joker karaktere `*` izin verilir ve çift joker `**` karakter özyinelemeli bir klasör aramasını ifade etmenizi gerektirir. |

### <a name="examples"></a>Örnekler

**Tek derleme**

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

**Hedef çerçeveye özgü tek bütünleştirilmiş kod**

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

**Joker karakter kullanan DLL 'Ler kümesi**

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

**Farklı çerçeveler için dll 'Ler**

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

**Dosyaları dışlama**

    Source files:
        \tools\fileA.bak
        \tools\fileB.bak
        \tools\fileA.log
        \tools\build\fileB.log

    .nuspec entries:
        <file src="tools\*.*" target="tools" exclude="tools\*.bak" />
        <file src="tools\**\*.*" target="tools" exclude="**\*.log" />

    Package result:
        (no files)

## <a name="including-content-files"></a>İçerik dosyalarını dahil etme

İçerik dosyaları, bir paketin bir projeye eklemesi gereken sabit dosyalardır. Sabit olması, tüketim projesi tarafından değiştirilmeleri amaçlanmamıştır. Örnek içerik dosyaları şunlardır:

- Kaynak olarak gömülü görüntüler
- Zaten derlenmiş kaynak dosyaları
- Projenin derleme çıktısına dahil olması gereken betikler
- Projeye dahil olması gereken ancak projeye özgü değişikliklere gerek gerektirmeyen paket için yapılandırma dosyaları

İçerik dosyaları, `<files>` `target` özniteliğinde `content` klasörü belirtilerek öğesini kullanarak bir pakete dahil edilir. Ancak, bu tür dosyalar, bir paket bir projeye yüklendiğinde, bunun yerine `<contentFiles>` öğesini kullanarak yok sayılır.

Tüketen projelerle maksimum uyumluluk için, her iki öğe içinde içerik dosyalarını ideal bir paket belirler.

### <a name="using-the-files-element-for-content-files"></a>İçerik dosyaları için Files öğesini kullanma

İçerik dosyaları için yalnızca derleme dosyaları için aynı biçimi kullanın, ancak aşağıdaki örneklerde gösterildiği gibi `content` `target` özniteliğinde temel klasör olarak belirtin.

**Temel içerik dosyaları**

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

**Dizin yapısıyla içerik dosyaları**

    Source files:
        css\mobile\style.css
        css\mobile\wp7\style.css
        css\browser\style.css

    .nuspec entry:
        <file src="css\**\*.css" target="content\css" />

    Packaged result:
        content\css\mobile\style.css
        content\css\mobile\wp7\style.css
        content\css\browser\style.css

**Hedef çerçeveye özgü içerik dosyası**

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

**İçerik dosyası ada sahip bir klasöre kopyalanmış**

Bu durumda, ' deki uzantının `target` içindeki `src` uzantıyla eşleşmediği ve bu nedenle adın bu `target` bölümünü bir klasör olarak değerlendirmiş olduğunu görür:

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

**Uzantısız içerik dosyaları**

Uzantısı olmayan dosyaları dahil etmek için, `*` veya `**` joker karakterleri kullanın:

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

**Derin yolu ve derin hedefi olan içerik dosyaları**

Bu durumda, kaynak ve hedef için dosya uzantıları eşleştiğinden, NuGet hedefin bir klasör değil bir dosya adı olduğunu varsayar:

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

**Paketteki bir içerik dosyasını yeniden adlandırma**

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

**Dosyaları dışlama**

    Source file:
        docs\*.txt (multiple files)

    .nuspec entry:
        <file src="docs\*.txt" target="content\docs" exclude="docs\admin.txt" />
        or
        <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />

    Packaged result:
        All .txt files from docs except admin.txt (first example)
        All .txt files from docs except admin.txt and log.txt (second example)

<a name="using-contentfiles-element-for-content-files"></a>

### <a name="using-the-contentfiles-element-for-content-files"></a>İçerik dosyaları için contentFiles öğesini kullanma

*PackageReference ile NuGet 4.0 +*

Varsayılan olarak, bir paket içeriği bir `contentFiles` klasöre koyar (aşağıya bakın) ve `nuget pack` varsayılan öznitelikleri kullanarak bu klasördeki tüm dosyaları içerir. Bu durumda, `contentFiles` `.nuspec` ' a bir düğüm eklemek gerekli değildir.

Hangi dosyaların ekleneceğini denetlemek için, `<contentFiles>` öğesi, tam dosyaları içeren `<files>` öğelerin bir koleksiyonu olduğunu belirler.

Bu dosyalar, proje sistemi içinde nasıl kullanılması gerektiğini betimleyen bir öznitelikler kümesiyle belirtilir:

| Öznitelik | Açıklama |
| --- | --- |
| **include** | Istenir `exclude` Özniteliği tarafından belirtilen Dışlamalar ile ilgili olarak içerilecek dosyanın veya dosyaların konumu. Mutlak bir yol belirtilmediği takdirde yol `contentFiles` klasöre göre değişir. Joker karaktere `*` izin verilir ve çift joker `**` karakter özyinelemeli bir klasör aramasını ifade etmenizi gerektirir. |
| **amaz** | `src` Konumdan hariç tutulacak dosyaların veya dosya desenlerinin noktalı virgülle ayrılmış listesi. Joker karaktere `*` izin verilir ve çift joker `**` karakter özyinelemeli bir klasör aramasını ifade etmenizi gerektirir. |
| **buildAction** | ,,, `Content`Vb. gibi MSBuild `None` `Embedded Resource` `Compile`için içerik öğesine atanacak yapı eylemi. Varsayılan, `Compile` değeridir. |
| **copyToOutput** | İçerik öğelerinin derleme (veya yayımlama) çıkış klasörüne kopyalanıp kopyalanmayacağını gösteren bir Boole değeri. Varsayılan olarak yanlıştır. |
| **flatten** | İçerik öğelerinin derleme çıkışında tek bir klasöre mi kopyalanacağını (true) veya paketteki klasör yapısını korumayı (false) gösteren bir Boole değeri. Bu bayrak yalnızca copyToOutput bayrağı true olarak ayarlandığında kullanılabilir. Varsayılan olarak yanlıştır. |

Bir paket yüklenirken NuGet, alt öğelerini `<contentFiles>` yukarıdan aşağıya uygular. Aynı dosyayla birden çok giriş eşleşiyorsa, tüm girişler uygulanır. Aynı öznitelik için bir çakışma varsa en üstteki girdi alt girişleri geçersiz kılar.

#### <a name="package-folder-structure"></a>Paket klasörü yapısı

Paket projesi, aşağıdaki kalıbı kullanarak içerik yapısını almalıdır:

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- `codeLanguages`,,, veya belirli bir `cs` `vb` `fs` `any``$(ProjectLanguage)`
- `TxM`NuGet tarafından desteklenen geçerli bir hedef çerçeve adıdır (bkz. [hedef çerçeveler](../reference/target-frameworks.md)).
- Bu söz dizimi sonuna herhangi bir klasör yapısı eklenebilir.

Örneğin:

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

Boş klasörler `.` , belirli dil birleşimleri ve TXM için içerik sağlamayı devre dışı bırakmak için kullanılabilir. Örneğin:

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a>Örnek contentFiles bölümü

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        ...
        <contentFiles>
            <!-- Embed image resources -->
            <files include="any/any/images/dnf.png" buildAction="EmbeddedResource" />
            <files include="any/any/images/ui.png" buildAction="EmbeddedResource" />

            <!-- Embed all image resources under contentFiles/cs/ -->
            <files include="cs/**/*.png" buildAction="EmbeddedResource" />

            <!-- Copy config.xml to the root of the output folder -->
            <files include="cs/uap/config/config.xml" buildAction="None" copyToOutput="true" flatten="true" />

            <!-- Copy run.cmd to the output folder and keep the directory structure -->
            <files include="cs/commands/run.cmd" buildAction="None" copyToOutput="true" flatten="false" />

            <!-- Include everything in the scripts folder except exe files -->
            <files include="cs/net45/scripts/*" exclude="**/*.exe"  buildAction="None" copyToOutput="true" />
        </contentFiles>
        </metadata>
</package>
```

## <a name="example-nuspec-files"></a>Örnek nuspec dosyaları

**Bağımlılıklar veya `.nuspec` dosyalar belirtmeyen bir basit**

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.2.3</version>
        <authors>Kim Abercrombie, Franck Halmaert</authors>
        <description>Sample exists only to show a sample .nuspec file.</description>
        <language>en-US</language>
        <projectUrl>http://xunit.codeplex.com/</projectUrl>
        <license type="expression">MIT</license>
    </metadata>
</package>
```

**Bağımlılıkları `.nuspec` olan A**

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.0.0</version>
        <authors>Microsoft</authors>
        <dependencies>
            <dependency id="another-package" version="3.0.0" />
            <dependency id="yet-another-package" version="1.0.0" />
        </dependencies>
    </metadata>
</package>
```

**Dosyalarla `.nuspec` birlikte**

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>routedebugger</id>
        <version>1.0.0</version>
        <authors>Jay Hamlin</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Route Debugger is a little utility I wrote...</description>
    </metadata>
    <files>
        <file src="bin\Debug\*.dll" target="lib" />
    </files>
</package>
```

**Bir `.nuspec` Framework Derlemeleriyle**

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>PackageWithGacReferences</id>
        <version>1.0</version>
        <authors>Author here</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>
            A package that has framework assemblyReferences depending
            on the target framework.
        </description>
        <frameworkAssemblies>
            <frameworkAssembly assemblyName="System.Web" targetFramework="net40" />
            <frameworkAssembly assemblyName="System.Net" targetFramework="net40-client, net40" />
            <frameworkAssembly assemblyName="Microsoft.Devices.Sensors" targetFramework="sl4-wp" />
            <frameworkAssembly assemblyName="System.Json" targetFramework="sl3" />
        </frameworkAssemblies>
    </metadata>
</package>
```

Bu örnekte, belirli proje hedefleri için aşağıdakiler yüklenir:

- . NET4-> `System.Web`,`System.Net`
- . NET4 Istemci profili->`System.Net`
- Silverlight 3->`System.Json`
- WindowsPhone->`Microsoft.Devices.Sensors`
