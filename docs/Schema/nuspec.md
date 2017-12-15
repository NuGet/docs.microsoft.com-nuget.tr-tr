---
title: "NuGet için'.nuspec dosyası başvurusu | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 8/29/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: d4a4db9b-5c2d-46aa-9107-d2b01733df7c
description: ".Nuspec dosyası bir paketi ve paket tüketicilere bilgi sağlamak için oluştururken kullanılan paket meta verileri içerir."
keywords: "nuspec başvurusu, NuGet paket meta verileri, NuGet paket bildirimi, nuspec şeması"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: 91efd4b4cd2ec0bee4425ab66e0152e580e7975c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="nuspec-reference"></a>.nuspec başvurusu

A `.nuspec` paket meta verileri içeren bir XML bildiriminden bir dosyadır. Bu bildirim paketi oluşturmak ve bilgileri tüketicilere sağlamak için kullanılır. Bildirim her zaman bir pakete dahil edilir.

Bu konuda:

- [Genel form ve şema](#general-form-and-schema)
- [Değiştirme belirteçleri](#replacement-tokens) (Visual Studio projesi ile kullanıldığında)
- [Bağımlılıklar](#dependencies)
- [Açık derleme başvuruları](#explicit-assembly-references)
- [Framework'te derleme başvuruları](#framework-assembly-references)
- [Derleme dosyaları dahil olmak üzere](#including-assembly-files)
- [İçerik dosyaları dahil olmak üzere](#including-content-files)
- [Örnekler](#examples)

## <a name="general-form-and-schema"></a>Genel form ve şema

Geçerli `nuspec.xsd` şema dosyası bulunabilir [NuGet GitHub deposunu](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).

Bu şemayı içinde bir `.nuspec` dosyası aşağıdaki genel biçime sahiptir:

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

Şema NET bir görsel gösterimi için şema dosyasını Visual Studio'da Tasarım modunda açın ve tıklayın **XML Şeması Explorer** bağlantı. Alternatif olarak, kod olarak dosyasını açın, Düzenleyicisi'nde sağ tıklatın ve seçin **Göster XML Şeması Explorer**. Her iki şekilde (çoğunlukla genişletildiğinde) bir görünüm aşağıdaki gibi alın:

![Visual Studio şema Gezgini ile nuspec.xsd Aç](media/SchemaExplorer.png)

### <a name="metadata-attributes"></a>Meta veri öznitelikleri

`<metadata>` Öğesi aşağıdaki tabloda açıklanan öznitelikleri destekler.

| Öznitelik | Gerekli | Açıklama |
| --- | --- | --- | 
| **minClientVersion** | Hayır | *(2.5 +)*  Nuget.exe ve Visual Studio Paket Yöneticisi tarafından zorlanan, bu paketi yükleyebilmek için NuGet istemci en düşük sürümünü belirtir. Bu paket belirli özelliklerine bağlıdır her kullanılır `.nuspec` belirli bir NuGet istemci sürümünün eklenen dosya. Örneğin, bir paketini kullanarak `developmentDependency` özniteliği için "2.8" belirtmelidir `minClientVersion`. Benzer şekilde, bir paketini kullanarak `contentFiles` öğesi (sonraki bölüme bakın) ayarlamalıdır `minClientVersion` "3.3" için. NuGet istemcileri 2.5 önce bu bayrak tanımıyor çünkü Ayrıca bunlar *her zaman* ne olursa olsun paketini yüklemek Reddet `minClientVersion` içerir. |

### <a name="required-metadata-elements"></a>Gerekli meta veri öğeleri

Aşağıdaki öğeler bir paket için en düşük gereksinimler olsa da, eklemeyi düşünmelisiniz [isteğe bağlı meta veri öğeleri](#optional-metadata-elements) genel deneyimini geliştirmek için geliştiricilere paketinizle birlikte sahip.

Bu öğeleri içinde görünmesi gereken bir `<metadata>` öğesi.

| Öğe | Açıklama |
| --- | --- |
| **id** | Nuget.org ya da ihtiyacınız arasında benzersiz olması büyük küçük harf duyarsız paket tanımlayıcısı galeri paketi bulunur. Kimlikleri değil boşluk ya da bir URL için geçerli olmayan karakterler içeren ve genellikle .NET ad alanı kuralları izleyin. Bkz: [benzersiz paket tanımlayıcısı seçme](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) Kılavuzu. |
| **Sürüm** | Aşağıdaki şekilde paketin sürümü *major.minor.patch* düzeni. Sürüm numaraları, yayın öncesi soneki içerebilir, açıklandığı gibi [paket sürüm](../reference/package-versioning.md#pre-release-versions). |
| **Açıklama** | Paket UI görüntü için uzun bir açıklaması. |
| **yazarları** | Nuget.org profil adları eşleşen paketleri yazarlar, virgülle ayrılmış listesi. Bunlar nuget.org NuGet galerisinde görüntülenir ve paketleri çapraz başvuru için aynı yazarlar tarafından kullanılır. |

### <a name="optional-metadata-elements"></a>İsteğe bağlı meta veri öğeleri

Bu öğeleri içinde görünmesi gereken bir `<metadata>` öğesi.

#### <a name="single-elements"></a>Tek öğeleri

| Öğe | Açıklama |
| --- | --- |
| **Başlık** | Nuget.org ve Visual Studio'da Paket Yöneticisi gibi UI görünümlerde genellikle kullanılan paket, bir insan kolay başlığı. Belirtilmezse, paket kimliği kullanılır. |
| **sahipleri** | Nuget.org üzerinde profil adları kullanarak paket oluşturucuları virgülle ayrılmış listesi. Bu genellikle aynı olarak listesidir `authors`ve paket için nuget.org karşıya yüklenirken göz ardı edilir. Bkz: [yönetme paket sahipleri nuget.org üzerinde](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg). |
| **projectUrl** | Paketin giriş sayfası, genellikle kullanıcı Arabiriminde gösterilen URL'sini nuget.org yanı sıra görüntüler. |
| **licenseUrl** | Genellikle nuget.org yanı sıra kullanıcı Arabirimi görüntüler gösterilen paketin lisans URL'sini. |
| **iconUrl** | UI görüntü paketinde simgesi olarak kullanılacak bir URL 64 x 64 görüntünün saydamlık arka plana sahip. Bu öğe içerdiğinden emin olun *resim URL'si doğrudan* ve görüntüyü içeren bir web sayfasının URL değil. Örneğin, görüntüyü github'dan, URL gibi raw dosyasını kullanmayı `https://github.com/<username>/<repository>/raw/<branch>/<logo.png>`. |
| **requireLicenseAcceptance** | İstemci paketi lisans paketi yüklemeden önce kabul etmek için tüketici sor olup olmadığını belirten bir Boole değeri. |
| **developmentDependency** | *(2.8 +)*  Paket olup olmadığını belirten bir Boolean değeri bir geliştirme-yalnızca-paket diğer paketler bağımlılık olarak dahil önleyen bağımlılık olarak işaretlenir. |
| **Özet** | UI görüntülenmesi için paket kısa bir açıklaması. Atlanırsa, kesilmiş bir sürümünü `description` kullanılır. |
| **releaseNotes** | *(1.5 +)*  Kullanıcı arabiriminde gibi sık kullanılan şekilde paketin bu sürümde yapılan değişikliklerin bir açıklaması **güncelleştirmeleri** sekmesi, Visual Studio Paket Yöneticisi ve Paket açıklaması yerine. |
| **Telif Hakkı** | *(1.5 +)*  Paket ayrıntılarını telif hakkı. |
| **Dil** | Paketi için yerel ayar kimliği. Bkz: [yerelleştirilmiş paketleri oluşturma](../create-packages/creating-localized-packages.md). |
| **etiketleri** | Etiketleri ve paketler arama ve filtreleme aracılığıyla paket ve yardımcı bulunabilirliğini açıklayan anahtar sözcükleri boşlukla ayrılmış listesi. |
| **Hizmet verilebilen** | *(3.3 +)*  İç NuGet için kullanım içindir. |

#### <a name="collection-elements"></a>Koleksiyon öğeleri

| Öğe | Açıklama |
| --- | --- |
**packageTypes** | *(3.3 +)*  Sıfır veya daha fazla koleksiyonu `<packageType>` geleneksel bağımlılık paketi varsa dışında paket türünü belirleyen öğeleri. Her packageType öznitelikleri *adı* ve *sürüm*. Bkz: [ayar paket türü](../create-packages/creating-a-package.md#setting-a-package-type). |
| **Bağımlılıklar** | Sıfır veya daha fazla koleksiyonu `<dependency>` öğeleri paketi için bağımlılıklar belirtme. Her bir bağımlılığın öznitelikleri *kimliği*, *sürüm*, *dahil* (3.x+) ve *hariç* (3.x+). Bkz: [bağımlılıkları](#dependencies) aşağıda. |
| **frameworkAssemblies** | *(1.2 +)*  Sıfır veya daha fazla koleksiyonu `<frameworkAssembly>` öğeleri, bu paket için gerekli .NET Framework derleme başvurularını tanımlayan da sağlar başvuruları paketi kullanan projeler için eklenir. Her frameworkAssembly sahip *assemblyName* ve *targetFramework* öznitelikleri. Bkz: [framework derlemeyi belirtmeyi başvuran GAC](#specifying-framework-assembly-references-gac) aşağıda. |
| **başvuruları** | *(1.5 +)*  Sıfır veya daha fazla koleksiyonu `<reference>` paketin derlemelerde adlandırma öğeleri `lib` proje başvuruları eklenen klasör. Her başvurusu olan bir *dosya* özniteliği. `<references>`Ayrıca içerebilir bir `<group>` öğesi ile bir *targetFramework* sonra içeren öznitelik `<reference>` öğeleri. Atlanırsa, tüm başvuruları `lib` dahil edilir. Bkz: [açık derleme başvurularını belirtme](#specifying-explicit-assembly-references) aşağıda. |
| **Content dosyaları** | *(3.3 +)*  Koleksiyonu `<files>` tüketim projeye dahil etmek için içerik dosyaları belirlemek öğeleri. Bu dosyalar, proje sistem içinde bunların nasıl kullanılacağını açıklayan özniteliklerinin kümesiyle belirtilir. Bkz: [pakete eklenecek dosyaları belirtme](#specifying-files-to-include-in-the-package) aşağıda. |

### <a name="files-element"></a>Dosyalar öğesi

`<package>` Düğüm içerebilir bir `<files>` düğümü bir eşdüzeyi olarak `<metadata>`ve bir ya da `<contentFiles>` altındaki `<metadata>`, pakete eklenecek hangi derleme ve içerik dosyaları belirtmek için. Bkz: [derleme dosyaları dahil olmak üzere](#including-assembly-files) ve [içerik dosyaları dahil olmak üzere](#including-content-files) Ayrıntılar için bu konudaki sonraki.

## <a name="replacement-tokens"></a>Değiştirme belirteçleri

Bir paket oluştururken [ `nuget pack` komutu](../tools/cli-ref-pack.md) $ayrılmış belirteçlerinde değiştirir `.nuspec` dosyanın `<metadata>` herhangi birinden bir proje dosyası değerlerini düğümle veya `pack` komutunun `-properties`geçin.

Komut satırında belirttiğiniz belirteci değerlerle `nuget pack -properties <name>=<value>;<name>=<value>`. Örneğin, bir belirteç gibi kullanabilir `$owners$` ve `$desc$` içinde `.nuspec` ve saat gibi sevk adresindeki değerlerini belirtin:

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

Bir projeye ait değerleri kullanmak için aşağıdaki tabloda açıklanan belirteçleri belirtin (AssemblyInfo başvuruyor dosyasında `Properties` gibi `AssemblyInfo.cs` veya `AssemblyInfo.vb`).

Bu belirteçler kullanmak için çalıştırın `nuget pack` proje dosyası yerine yalnızca `.nuspec`. Örneğin aşağıdaki komutu kullanarak, `$id$` ve `$version$` içinde belirteçler bir `.nuspec` dosyası, projenin değiştirilir `AssemblyName` ve `AssemblyVersion` değerler:

```ps
nuget pack MyProject.csproj
```

Genellikle, sahip olduğunuz bir proje oluşturduğunuzda `.nuspec` başlangıçta kullanarak `nuget spec MyProject.csproj` otomatik olarak içeren bazı standart bu belirteçleri. Ancak, bir proje için değerler eksikse gerekli `.nuspec` öğeleri, ardından `nuget pack` başarısız olur. Ayrıca, proje değerleri değiştirirseniz, paket oluşturmadan önce yeniden emin olun; Bu paketi komutunun ile kolayca yapılabilir `build` geçin.

Dışında `$configuration$`, projedeki değerleri herhangi bir komut satırında aynı belirtecine atanmış yerine kullanılır.

| Belirteç | Değer kaynağı | Değer
| --- | --- | ---
| **$id$** | Proje dosyası | Proje dosyasından AssemblyName |
| **$version$** | AssemblyInfo | Assemblyınformationalversion bütünleştirilmiş varsa, aksi takdirde AssemblyVersion |
| **$author$** | AssemblyInfo | AssemblyCompany |
| **$description$** | AssemblyInfo | AssemblyDescription |
| **$copyright$** | AssemblyInfo | AssemblyCopyright |
| **$configuration$** | Derleme DLL | Hata ayıklama için varsayılan değer olarak, derleme için kullanılan yapılandırma. Bir yayın Yapılandırması'nı kullanarak bir paket oluşturmak için her zaman kullanmanız gerektiğini unutmayın `-properties Configuration=Release` komut satırında. |

Belirteçleri de dahil, yolları çözümlemek için kullanılabilir [derleme dosyalarını](#including-assembly-files) ve [içerik dosyaları](#including-content-files). Belirteçleri yapı yapılandırmasına bağlı olarak eklenecek dosyaları seçin edinerek MSBuild özellikleri olarak aynı ada sahip. Örneğin, aşağıdaki belirteçlerinde kullanırsanız `.nuspec` dosyası:

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

Ve bir derleme, `AssemblyName` olan `LoggingLibrary` ile `Release` MSBuild, sonuçta elde edilen satırları yapılandırmasında `.nuspec` paket dosyasında aşağıdaki gibidir:

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies"></a>Bağımlılıklar

`<dependencies>` Öğesi içinde `<metadata>` herhangi bir sayıda içeren `<dependency>` en üst düzey paketinin bağımlı olduğu diğer paketleri belirleyin öğeleri. Her özniteliklerini `<dependency>` aşağıdaki gibidir:

| Öznitelik | Açıklama |
| --- | --- | 
| `id` | (Gerekli) Bağımlılık paket kimliği. |
| `version` | (Gerekli) Sürümleri bağımlılık olarak kabul edilebilir aralık. Bkz: [paket sürüm](../reference/package-versioning.md#version-ranges-and-wildcards) söz dizimi için. |
| include | Virgülle ayrılmış listesini içeren/çıkarma (aşağıya bakın) son pakete dahil etmek bağımlılığın belirten etiketler. Varsayılan değer `none` şeklindedir. |
| exclude | Virgülle ayrılmış listesini içeren/çıkarma (aşağıya bakın) son paketinde dışlanacak bağımlılığın belirten etiketler. Varsayılan değer `all`. İle belirtilen etiketleri `exclude` ile belirtilen önceliklidir `include`. Örneğin, `include="runtime, compile" exclude="compile"` aynı `include="runtime"`. |

| Etiket dahil etme/hariç tutma | Hedef etkilenen klasörler |
| --- | --- |
| Content dosyaları | İçerik  |
| çalışma zamanı | Çalışma zamanı, kaynakları ve FrameworkAssemblies  |
| Derleme | LIB |
| derleme | derleme (MSBuild özellik ve hedefleri) |
| yerel | yerel |
| yok | Klasör yok |
| tüm | Tüm klasörleri |

Örneğin, aşağıdaki satırları üzerinde bağımlılıkları göstermek `PackageA` sürüm 1.1.0 veya daha yüksek ve `PackageB` sürüm 1.x.

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

Aşağıdaki satırları aynı paketleri bağımlılıkları gösterir, ancak dahil edileceğini belirtin `contentFiles` ve `build` klasörleri `PackageA` ve her şeyi ancak `native` ve `compile` klasörleri `PackageB`"

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

Not: oluştururken bir `.nuspec` kullanarak proje `nuget spec`, bu proje bağımlılıkları otomatik olarak eklenir kaynaklanan `.nuspec` dosya.

### <a name="dependency-groups"></a>Bağımlılık grupları

*Sürüm 2.0 +*

Tek düz bir liste için alternatif olarak, proje hedef kullanmanın framework profili göre bağımlılıkları belirtilebilir `<group>` içinde öğelerin `<dependencies>`.

Her Grup adlı bir özniteliği olan `targetFramework` ve sıfır veya daha fazla içeren `<dependency>` öğeleri. Hedef Framework'ü projenin framework profiliyle uyumlu olduğunda bu bağımlılıkların birlikte yüklenir.

`<group>` Öğesi olmadan bir `targetFramework` özniteliği bağımlılıkları varsayılan ya da geri dönüş liste olarak kullanılır. Bkz: [hedef çerçeveler](../schema/target-frameworks.md) tam framework tanımlayıcıları için.

> [!Important]
> Grup biçimi ile düz bir liste intermixed olamaz.

Aşağıdaki örnek, farklı varyasyonları gösterir `<group>` öğe:

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a>Açık derleme başvuruları

`<references>` Öğesi açıkça hedef projeyi paket kullanırken başvurması gereken derlemeleri belirtir. Bu öğe varsa, NuGet yalnızca listelenen derlemelerine başvurular ekleyin; Bu başvurular için herhangi bir paketin derlemelerde eklemez `lib` klasör.

Örneğin, aşağıdaki `<references>` öğesi bildirir yalnızca başvuruları eklemek için NuGet `xunit.dll` ve `xunit.extensions.dll` olsa bile ek derlemeler pakette:

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

Açık başvurular genellikle tasarım zamanı yalnızca derlemeler için kullanılır. Kullanırken [kod sözleşmeleri](https://docs.microsoft.com/dotnet/framework/debug-trace-profile/code-contracts), örneğin, sözleşme derlemeleri bunlar artırabilir ve böylece Visual Studio bulmalarını çalışma zamanı derlemeleri yanındaki olması gerekiyor, ancak sözleşme derlemeleri olmaması gereken proje tarafından başvurulan veya kopyalama projenin içine `bin` klasör.

Benzer şekilde, açık başvurular derlemeleri çalışma zamanı derlemeleri yanında bulunan, ancak proje başvuruları dahil gerekmez mu araçlarını gereken XUnit gibi birim test çerçevelerini için kullanılabilir.

### <a name="reference-groups"></a>Başvuru grupları

*Sürüm 2.5 +*

Tek düz bir liste için alternatif olarak, proje hedef kullanmanın framework profili göre başvuruları belirtilebilir `<group>` içinde öğelerin `<references>`.

Her Grup adlı bir özniteliği olan `targetFramework` ve sıfır veya daha fazla içeren `<reference>` öğeleri. Hedef Framework'ü projenin framework profiliyle uyumlu olduğunda bu başvuruları projeye eklenir.

`<group>` Öğesi olmadan bir `targetFramework` özniteliği başvuruları varsayılan ya da geri dönüş liste olarak kullanılır. Bkz: [hedef çerçeveler](../schema/target-frameworks.md) tam framework tanımlayıcıları için.

> [!Important]
> Grup biçimi ile düz bir liste intermixed olamaz.

Aşağıdaki örnek, farklı varyasyonları gösterir `<group>` öğe:

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

## <a name="framework-assembly-references"></a>Framework'te derleme başvuruları

Çerçeve derlemesi .NET framework'ün parçasıdır ve genel derleme önbelleğinde (GAC) belirli bir makine zaten olmalıdır izinlerdir. Bu derleme içinde tanımlayan tarafından `<frameworkAssemblies>` öğesi, bir paket emin olun proje zaten bu başvuruları yok gerektiğinde, gerekli başvuruları projeye eklenir. Bu tür derlemeler doğal olarak, bir pakette doğrudan dahil edilmez.

`<frameworkAssemblies>` Sıfır veya daha fazla öğe içeriyor `<frameworkAssembly>` öğeleri, her biri aşağıdaki öznitelikler belirtir:

| Öznitelik | Açıklama |
| --- | --- |
| **assemblyName** | (Gerekli) Tam nitelikli derleme adı. |
| **targetFramework** | (İsteğe bağlı) Bu başvuru uygulandığı hedef Framework'ü belirtir. Atlanırsa, başvuru tüm çerçeveler için geçerli olduğunu gösterir. Bkz: [hedef çerçeveler](../schema/target-frameworks.md) tam framework tanımlayıcıları için. |

Aşağıdaki örnek, başvuru gösterir `System.Net` tüm çerçeveler ve başvuru hedef için `System.ServiceModel` yalnızca .NET Framework 4.0 için:

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a>Derleme dosyaları dahil olmak üzere

Açıklanan kuralları izlerseniz [paket oluşturma](../create-packages/creating-a-package.md), dosyaların listesini açıkça belirtmek zorunda değilsiniz `.nuspec` dosya. `nuget pack` Komutu, gerekli dosyaları otomatik olarak seçer.

> [!Important]
> Bir paket bir projeye yüklendiğinde, NuGet paket DLL'leri derleme başvuruları otomatik olarak ekler. *hariç* adlandırıldığı o `.resources.dll` yerleştirilmiş yardımcı derlemeler olarak kabul olduğundan. Bu nedenle, kullanmaktan kaçının `.resources.dll` , aksi takdirde temel paket kodu içeren dosyaları için.

Bu otomatik davranışı atlayıp açıkça hangi dosyaların bir pakete dahil edilen denetlemek için yerleştirin bir `<files>` öğesi bir alt öğesi olarak `<package>` (ve bir eşdüzeyi `<metadata>`), her dosya ayrı bir tanımlayan `<file>` öğesi. Örneğin:

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

NuGet ile 2.x ve önceki sürümleri ve kullanarak projeleri `packages.config`, `<files>` öğesi bir paket yüklendiğinde değişmez içerik dosyalarını eklemek için de kullanılır. NuGet 3.3 + ve kullanarak projeleri ile `project.json` pr PackageReference, `<contentFiles>` öğe yerine kullanılır. Bkz: [içerik dosyaları dahil olmak üzere](#including-content-files) aşağıda Ayrıntılar için.

### <a name="file-element-attributes"></a>Dosya öğesi öznitelikleri

Her `<file>` öğesi aşağıdaki özniteliklere belirtir:

| Öznitelik | Açıklama |
| --- | --- |
| **src** | Dosya veya dosyalar tarafından belirtilen Dışlamalar tabi dahil etmek için konumunu `exclude` özniteliği. Göreli yol olduğundan `.nuspec` mutlak bir yol belirtilmediği sürece dosya. Joker karakter `*` izin verilir ve çift joker karakter `**` özyinelemeli klasör arama anlamına gelir. |
| **Hedef** | Göreli yolu ile başlamalı, kaynak dosyaları yerleştirilir, paket içindeki klasöre `lib`, `content`, `build`, veya `tools`. Bkz: [kurala dayalı bir çalışma dizininden bir .nuspec oluşturma](../Create-Packages/Creating-a-Package.md#from-a-convention-based-working-directory). |
| **hariç tutma** | Dosya veya dosya desenlerinin ayarlayacağım noktalı virgülle ayrılmış listesini `src` konumu. Joker karakter `*` izin verilir ve çift joker karakter `**` özyinelemeli klasör arama anlamına gelir. |

### <a name="examples"></a>Örnekler

**Tek derleme**

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

**Bir hedef framework belirli tek derleme**

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

**Joker karakter kullanarak DLL'leri kümesi**

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

**Farklı çerçeveleri DLL'leri**

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
        \tools\*.bak
        \tools\*.log
        \tools\build\*.log

    .nuspec entries:
        <file src="tools\*.*" target="tools" exclude="tools\*.bak" />
        <file src="tools\**\*.*" target="tools" exclude="**\*.log" />

    Package result:
        (no files)

## <a name="including-content-files"></a>İçerik dosyaları dahil olmak üzere

İçerik dosyaları bir proje eklemek için bir paket gereken değişmez dosyalarıdır. Değişmez olmasının, bunlar Süren projenin değiştirilecek amaçlanmamıştır. Örnek içerik dosyalarını içerir:

- Kaynaklar olarak katıştırılmış görüntüler
- Önceden derlenmiş kaynak dosyaları
- Proje derleme çıktı ile dahil edilmesi gereken komut
- Projeye dahil edilmesi gereken ancak projeye özgü değişiklikleri gerekmeyen bir paket için yapılandırma dosyaları

İçerik dosyalarını kullanarak bir paket dahil edilir `<files>` öğesini belirterek `content` klasöründe `target` özniteliği. Paket kullanarak bir projeye yüklendiğinde ancak, bu tür dosyaları göz ardı edilir `project.json` yerine kullanan sistem NuGet 3.3 + ya da NuGet 4 + PackageReference `<contentFiles>` öğesi.

Projeleri kullanma ile en fazla uyumluluk için bir paket içerik dosyalarını ideal olarak her iki öğelerinde belirtir.

### <a name="using-the-files-element-for-content-files"></a>Dosyalar öğesi için içerik dosyalarını kullanma

İçerik dosyaları için yalnızca derleme dosyaları için olduğu gibi aynı biçimi kullanır, ancak belirtin `content` temel klasör olarak `target` özniteliği aşağıdaki örneklerde gösterildiği gibi.

**Temel içerik dosyaları**

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

**İçerik dosyaları dizin yapısı**

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

**İçerik dosyası için bir hedef çerçevesine özgü**

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

**İçerik dosyası adında nokta olan bir klasöre kopyalanır**

Bu durumda, NuGet, görür uzantı `target` uzantı eşleşmiyor `src` ve bu nedenle adı kısmı değerlendirir `target` bir klasör olarak:

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

**İçerik dosyaları uzantısız**

Bir uzantısı olmayan dosyaları eklemek için kullanın `*` veya `**` joker karakterler:

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

**Derin yolu ve derin hedefi olan içerik dosyaları**

Bu durumda, kaynak ve hedef dosya uzantılarını eşleştiğinden NuGet hedef dosya adını ve bir klasör olduğunu varsayar:

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

**Paketteki içerik dosyasını yeniden adlandırma**

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

### <a name="using-the-contentfiles-element-for-content-files"></a>Content dosyaları öğesi için içerik dosyalarını kullanma

*Sürümüyle 3.3 + project.json ve 4.0 + PackageReference ile*

Varsayılan olarak, bir paket içeriği yerleştirir bir `contentFiles` klasörü (aşağıya bakın) ve `nuget pack` varsayılan özniteliklerini kullanarak bu klasördeki tüm dosyaları dahil. Bu durumda dahil etmek gerekli değildir bir `contentFiles` düğümünde `.nuspec` hiç.

Hangi dosyaların dahil olduğunu denetlemek için `<contentFiles>` öğesi belirttiğinden bir koleksiyonu `<files>` tam dosyaları belirlemek öğeler içerir.

Bu dosyalar, proje sistem içinde bunların nasıl kullanılacağını açıklayan özniteliklerinin kümesiyle belirtilir:

| Öznitelik | Açıklama |
| --- | --- |
| **içerir** | (Gerekli) Dosya veya dosyalar tarafından belirtilen Dışlamalar tabi dahil etmek için konumunu `exclude` özniteliği. Göreli yol olduğundan `.nuspec` mutlak bir yol belirtilmediği sürece dosya. Joker karakter `*` izin verilir ve çift joker karakter `**` özyinelemeli klasör arama anlamına gelir. |
| **hariç tutma** | Dosya veya dosya desenlerinin ayarlayacağım noktalı virgülle ayrılmış listesini `src` konumu. Joker karakter `*` izin verilir ve çift joker karakter `**` özyinelemeli klasör arama anlamına gelir. |
| **buildAction** | MSBuild için içerik öğesine gibi atanacak yapı eylemi `Content`, `None`, `Embedded Resource`, `Compile`vb. Varsayılan, `Compile` değeridir. |
| **copyToOutput** | İçerik öğeleri yapı çıktı klasörüne kopyalanıp kopyalanmayacağını gösteren bir Boole değeri. Varsayılan olarak yanlıştır. |
| **düzleştirme** | İçerik öğeleri yapı çıktı (true) tek bir klasöre kopyalayın veya klasör yapısı (false) paketindeki korumak için gösteren bir Boole değeri. Varsayılan olarak yanlıştır. |

Bir paket yüklerken, alt öğelerini NuGet geçerlidir `<contentFiles>` yukarıdan aşağıya. Aynı dosyanın eşleşen birden fazla giriş varsa tüm girişleri uygulanır. Aynı öznitelik için bir çakışma varsa en üstteki girişi alt girişleri geçersiz kılar.

#### <a name="package-folder-structure"></a>Paket klasör yapısı

Paket proje şu biçimi kullanarak içerik yapısı:

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- `codeLanguages`olabilir `cs`, `vb`, `fs`, `any`, veya küçük harf denk bir verilen`$(ProjectLanguage)`
- `TxM`NuGet destekleyen tüm yasal hedef framework addır (bkz [hedef çerçeveler](../schema/target-frameworks.md)).
- Herhangi bir klasör yapısını bu söz dizimini sonuna eklenmiş.

Örneğin:

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

Boş klasörler kullanabileceğiniz `.` dil ve TxM, belirli bir kombinasyonu için içerik örneğin sağlama dışında kabul etmek için:

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a>Örnek Content dosyaları bölümüne

```xml
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
```

## <a name="example-nuspec-files"></a>Örnek .nuspec dosyası

**Basit bir `.nuspec` , bağımlılıkları veya dosyaları belirtmiyor**

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
    <licenseUrl>http://xunit.codeplex.com/license</licenseUrl>
    </metadata>
</package>
```

**A `.nuspec` bağımlılıkları**

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

**A `.nuspec` dosyalarla**

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

**A `.nuspec` framework derlemeler ile**

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

Bu örnekte, belirli bir proje hedefleri için aşağıdaki yüklenir:

- . NET4 -> `System.Web`,`System.Net`
- . NET4 İstemci profili ->`System.Net`
- Silverlight 3 ->`System.Json`
- Silverlight 4 ->`System.Windows.Controls.DomainServices`
- WindowsPhone ->`Microsoft.Devices.Sensors`
