---
title: CLI NuGet Paketi komutu
description: Nuget.exe paketi komut başvurusu
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: c3a01b7747be96f02f7b93b3bf66f5d1783ceed7
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842547"
---
# <a name="pack-command-nuget-cli"></a>Paketi komut (NuGet CLI)

**İçin geçerlidir:** paket oluşturma &bullet; **desteklenen sürümler:** 2.7+

Belirtilen temel bir NuGet paketi oluşturur `.nuspec` ya da proje dosyası. `dotnet pack` Komut (bkz [dotnet komutları](dotnet-Commands.md)) ve `msbuild -t:pack` (bkz [MSBuild hedefleri](../reference/msbuild-targets.md)) alternatifler kullanılabilir.

> [!Important]
> Mono altında bir proje dosyasından paket oluşturma desteklenmiyor. Ayrıca yerel olmayan yollarında ayarlamanız gereken `.nuspec` nuget.exe Windows yol adlarını kendi Dönüştürülmeyen olarak UNIX stili yollara, dosya.

## <a name="usage"></a>Kullanım

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

Burada `<nuspecPath>` ve `<projectPath>` belirtin `.nuspec` veya proje dosyası, sırasıyla.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| BasePath | Temel yol içinde tanımlanan tüm dosyaların ayarlar `.nuspec` dosya. |
| Yapı | Projenin paket oluşturulmadan önce oluşturulması gerektiğini belirtir. |
| Hariç tutma | Bir paket oluştururken hariç tutmak için bir veya daha fazla joker karakter düzeni belirtir. Birden fazla düzenini belirtmek için yineleyin Exclude bayrağı. Aşağıdaki örneğe bakın. |
| ExcludeEmptyDirectories | Boş dizinleri dahil edilmesi, paket oluştururken engeller. |
| ForceEnglishOutput | *(3.5 +)*  Nuget.exe sabit, İngilizce tabanlı bir kültürü kullanarak çalışmaya zorlar. |
| ConfigFile | Paketi komut için yapılandırma dosyası belirtin. |
| Help | Bilgi komut için yardımı görüntüler. |
| IncludeReferencedProjects | Yerleşik paket bağımlılıkları veya paketinin bir parçası olarak başvurulan projeler içermelidir gösterir. Başvurulan projenin karşılık gelen varsa `.nuspec` başvurulan proje bir bağımlılık olarak eklendikten sonra proje ile aynı ada sahip bir dosya. Aksi takdirde, başvurulan projenin paketinin bir parçası eklenir. |
| MinClientVersion | Ayarlama *minClientVersion* oluşturulan bir paket için özniteliği. Bu değer mevcut değerini geçersiz kılar *minClientVersion* (varsa) özniteliğini `.nuspec` dosya. |
| MSBuildPath | *(4.0 +)*  Önceliği alma komutu ile kullanılacak MSBuild yolunu belirtir `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)*  Bu komutla birlikte kullanılacak MSBuild sürümünü belirtir. Desteklenen değerler şunlardır: 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15,8, 15.9. Yolunuza Msbuild'de çekilir varsayılan olarak, aksi takdirde MSBuild yüksek yüklü sürümü varsayar. |
| NoDefaultExcludes | Varsayılan dışlama nuget engelleyen paket dosyalarını ve dosya ve klasörleri gibi bir noktayla başlayan `.svn` ve `.gitignore`. |
| NoPackageAnalysis | Paketi paket analiz paketini oluşturduktan sonra çalışmaması gerektiğini belirtir. |
| OutputDirectory | Oluşturulan bir paket depolandığı klasörü belirtir. Klasör belirtilirse, geçerli klasörde kullanılır. |
| Özellikler | Diğer seçeneklerden sonra komut satırında son görünmelidir. Geçersiz kılma değerleri proje dosyasında özelliklerin bir listesini belirtir. bkz: [yaygın MSBuild proje özellikleri](/visualstudio/msbuild/common-msbuild-project-properties) özellik adları. Burada özellikleri bağımsız değişkeni bir belirteç listesidir. = değer çiftleri noktalı virgülle ayrılmış, burada her geçtiği `$token$` içinde `.nuspec` dosya verilen değer ile değiştirilecek. Dizeleri tırnak işaretleri içindeki değerleri olabilir. "Debug" "Yapılandırma" özelliği için varsayılan olduğunu unutmayın. Bir yayın yapılandırmasına değiştirmek için kullanın `-Properties Configuration=Release`. |
| Son eki | *(3.4.4+)*  Genellikle derleme veya diğer yayın öncesi tanımlayıcıları ekleme için kullanılan dahili olarak oluşturulan sürüm numarası, bir sonek ekler. Örneğin, kullanarak `-suffix nightly` ile bir sürüm numarası benzer bir paket oluşturacak `1.2.3-nightly`. Sonekleri uyarılar, hatalar ve farklı sürümlerini NuGet ve NuGet Paket Yöneticisi ile olası uyumsuzluklar önlemek için bir harf ile başlaması gerekir. |
| Simgeleri | Paket kaynakları ve semboller içerdiğini belirtir. İle kullanıldığında bir `.nuspec` dosyası bu oluşturur normal bir NuGet paketi dosyası ve karşılık gelen paket simgeleri. Varsayılan olarak oluşturduğu bir [eski sembol paketi](../create-packages/Symbol-Packages.md). Sembol paketleri yeni Önerilen biçimi .snupkg değil. Bkz: [sembol paketleri (.snupkg) oluşturma](../create-packages/Symbol-Packages-snupkg.md). |
| SymbolPackageFormat | Semboller paketin biçimini belirtir: *symbols.nupkg* (eski) veya *snupkg* (önerilir). Varsayılan olarak oluşturduğu bir [eski sembol paketi](../create-packages/Symbol-Packages.md). Bkz: [sembol paketleri (.snupkg) oluşturma](../create-packages/Symbol-Packages-snupkg.md). |
| Aracı | Projenin çıkış dosyalarının içinde yerleştirilmesi gerektiğini belirtir `tool` klasör. |
| Verbosity | Çıktıda gösterilen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |
| Sürüm | Sürüm numarasını geçersiz kılmalar `.nuspec` dosya. |

Ayrıca bkz: [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="excluding-development-dependencies"></a>Geliştirme bağımlılıkları hariç

NuGet paketlerinden bazıları kendi kitaplığı yazma yardımcı, ancak mutlaka asıl Paket bağımlılıkları olarak gerekmeyen geliştirme bağımlılık olarak yararlıdır.

`pack` Komut yoksayar `package` girişleri `packages.config` sahip `developmentDependency` özniteliğini `true`. Bu girişler değil dahil edilecek öğeleri oluşturulan paketi bir bağımlılık olarak.

Örneğin, aşağıdakileri dikkate alın `packages.config` kaynak proje dosyasında:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

Bu proje için paket tarafından oluşturulan `nuget pack` bağımlılığa sahip `jQuery` ve `microsoft-web-helpers` ama `netfx-Guard`.

## <a name="examples"></a>Örnekler

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -MSBuildVersion 12 -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.nuspec and the corresponding symbol package using the new recommended format .snupkg
nuget pack foo.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
