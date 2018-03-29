---
title: NuGet CLI paketi komut | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Nuget.exe paketi komut başvurusu
keywords: nuget paketi başvurusu, paketi komutu
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 14ecf724477f652275eb68a090bb57b8640d4a8a
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="pack-command-nuget-cli"></a>Paketi komut (NuGet CLI)

**Uygulandığı öğe:** paketini oluşturma &bullet; **desteklenen sürümler:** 2.7 +

Belirtilen temel bir NuGet paketi oluşturur `.nuspec` veya proje dosyası. `dotnet pack` Komutu (bkz [dotnet komutları](dotnet-Commands.md)) ve `msbuild /t:pack` (bkz [MSBuild hedefleri](../reference/msbuild-targets.md)) alternatifler kullanılabilir.

> [!Important]
> Mono altında bir proje dosyasından paket oluşturma desteklenmiyor. Ayrıca yerel olmayan yollarında ayarlamak gereken `.nuspec` dosya UNIX stili yollara nuget.exe Windows yol adları kendisini Dönüştürülmeyen gibi.

## <a name="usage"></a>Kullanım

```cli
nuget pack <nuspecPath | projectPath> [options]
```

Burada `<nuspecPath>` ve `<projectPath>` belirtin `.nuspec` veya proje dosyası, sırasıyla.

## <a name="options"></a>Seçenekler

| Seçenek | Açıklama |
| --- | --- |
| BasePath | Tanımlanan dosyalarının temel yolunu ayarlar `.nuspec` dosya. |
| Derleme | Proje paket oluşturmadan önce oluşturulmalıdır belirtir. |
| Exclude | Bir paket oluştururken çıkarılacak bir veya daha fazla joker karakter düzenleri belirtir. Birden fazla desen belirtmek için yineleyin Exclude bayrağı. Aşağıdaki örneğe bakın. |
| ExcludeEmptyDirectories | Boş dizinleri dahil edilmesi paket oluştururken engeller. |
| ForceEnglishOutput | *(3.5 +)*  Değişmez, İngilizce tabanlı kültürü kullanarak çalışacak şekilde nuget.exe zorlar. |
| Yardım | Bilgi komutu için yardımı görüntüler. |
| IncludeReferencedProjects | Yerleşik paket bağımlılıkları veya paketinin bir parçası olarak başvurulan projeleri içermelidir gösterir. Başvurulan bir projenin karşılık gelen varsa `.nuspec` başvurulan proje bağımlılık olarak eklendikten sonra proje aynı ada sahip dosya. Aksi takdirde, başvurulan proje paketinin bir parçası eklenir. |
| MinClientVersion | Ayarlama *minClientVersion* özniteliği için oluşturulan paketi. Bu değer var olan değerini geçersiz kılar *minClientVersion* (varsa) özniteliğini `.nuspec` dosya. |
| MSBuildPath | *(4.0 +)*  Öncelik Alma komutuyla kullanmak için MSBuild yolunu belirtir `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)*  Bu komutla birlikte kullanılacak MSBuild sürümünü belirtir. Değerleri, 4, 12, 14, 15 desteklenir. MSBuild yolda çekilir varsayılan olarak, aksi takdirde MSBuild yüksek yüklü sürümü varsayar. |
| NoDefaultExcludes | Varsayılan dışlama olan NuGet engelleyen paket dosyaları, dosya ve klasörleri gibi bir noktayla başlayan `.svn` ve `.gitignore`. |
| NoPackageAnalysis | Paketi paket analiz paketi oluşturduktan sonra çalışmayacağını belirtir. |
| Çıktıdizini | Oluşturulan paket depolandığı klasörü belirtir. Bir klasör bulunmadığından belirtilmezse, geçerli klasörde kullanılır. |
| Özellikler | Proje dosyasında değerleri geçersiz kılmak özellikler listesini belirtir; bkz: [yaygın MSBuild proje özellikleri](/visualstudio/msbuild/common-msbuild-project-properties) özellik adları. Burada özellikleri bağımsız değişkeni bir belirteç listesidir noktalı virgülle ayrılmış değer çiftleri = burada her oluşumu `$token$` içinde `.nuspec` dosya verilen değer ile değiştirilecek. Değerleri tırnak işaretleri içindeki dizeleri olabilir. "Hata ayıklama" "Yapılandırma" özelliği için varsayılan olduğunu unutmayın. Bir yayın yapılandırmasını değiştirmek için kullanın `-Properties Configuration=Release`. |
| Son eki | *(3.4.4+)*  Genellikle yapı ya da diğer yayın öncesi tanımlayıcıları ekleme için kullanılan dahili olarak oluşturulan sürüm numarası bir sonek ekler. Örneğin, kullanarak `-suffix nightly` ile bir sürüm numarası benzer bir paket oluşturacak `1.2.3-nightly`. Sonekleri uyarılar, hatalar ve farklı sürümlerini NuGet ve NuGet Paket Yöneticisi ile olası uyumsuzlukları önlemek için bir harf ile başlamalıdır. |
| Simgeleri | Paket kaynaklarını ve simgeleri içerdiğini belirtir. İle kullanıldığında bir `.nuspec` dosyası, bu bir normal NuGet paket dosyası oluşturur ve karşılık gelen paket simgeler. |
| Aracı | Proje çıktı dosyalarını içinde yerleştirilmesi gerektiğini belirtir `tool` klasör. |
| Ayrıntı Düzeyi | Çıktıda görüntülenen ayrıntı miktarını belirtir: *normal*, *sessiz*, *ayrıntılı*. |
| Sürüm | Sürüm numarasını geçersiz kılmaları `.nuspec` dosya. |

Ayrıca bkz. [ortam değişkenleri](cli-ref-environment-variables.md)

## <a name="excluding-development-dependencies"></a>Hariç geliştirme bağımlılıkları

Bazı NuGet paketleri kendi kitaplığı yazma yardımcı olur, ancak mutlaka asıl Paket bağımlılıklar olarak gerekmeyen geliştirme bağımlılık faydalıdır.

`pack` Komutu yoksayar `package` girişleri `packages.config` sahip `developmentDependency` özniteliği kümesine `true`. Bu girişler değil dahil edilecek öğeleri bir bağımlılık olarak oluşturulan paketi.

Örneğin, aşağıdakileri göz önünde bulundurun `packages.config` kaynak proje dosyasında:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

Bu proje için paket tarafından oluşturulan `nuget pack` bir bağımlılığa sahip olur `jQuery` ve `microsoft-web-helpers` ama `netfx-Guard`.

## <a name="examples"></a>Örnekler

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5" -MSBuildVersion 12

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
