---
title: NuGet paketi ve geri yükleme MSBuild hedefleri olarak
description: NuGet paketi ve geri yükleme, NuGet 4.0 + ile doğrudan MSBuild hedefleri olarak çalışabilir.
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 0c32978baf6146f10c262ba7af94f61fee22272d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777723"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>NuGet paketi ve geri yükleme MSBuild hedefleri olarak

*NuGet 4.0 +*

[Packagereference](../consume-packages/package-references-in-project-files.md) biçimi sayesinde, NuGet 4.0 + tüm bildirim meta verilerini ayrı bir dosya kullanmak yerine doğrudan proje dosyası içinde depolayabilirler `.nuspec` .

MSBuild 15.1 + ile NuGet, `pack` aşağıda açıklandığı gibi, ve hedefleri ile birinci sınıf MSBuild vatandaşlık da vardır `restore` . Bu hedefler, diğer herhangi bir MSBuild görevi veya hedefi ile yaptığınız gibi NuGet ile çalışmanıza olanak sağlar. MSBuild kullanarak bir NuGet paketi oluşturma yönergeleri için bkz. [MSBuild kullanarak NuGet paketi oluşturma](../create-packages/creating-a-package-msbuild.md). (NuGet 3. x ve öncesi için, bunun yerine NuGet CLı aracılığıyla [paketle](../reference/cli-reference/cli-ref-pack.md) ve [geri yükleme](../reference/cli-reference/cli-ref-restore.md) komutlarını kullanırsınız.)

## <a name="target-build-order"></a>Hedef derleme sırası

`pack`Ve `restore` MSBuild hedefleri olduğundan, iş akışınızı geliştirmek için bunlara erişebilirsiniz. Örneğin, paketledikten sonra paketinizi bir ağ paylaşımında kopyalamak istediğinizi varsayalım. Bunu, proje dosyanıza aşağıdakileri ekleyerek yapabilirsiniz:

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

Benzer şekilde, MSBuild görevinde bir MSBuild görevi yazabilir, kendi hedefini yazabilir ve NuGet özelliklerini kullanabilirsiniz.

> [!NOTE]
> `$(OutputPath)` görelidir ve bu komutu proje kökünden çalıştırdığınız için bekliyor.

## <a name="pack-target"></a>paket hedefi

Biçimini kullanan .NET projeleri için `PackageReference` , `msbuild -t:pack` bir NuGet paketi oluştururken kullanılacak proje dosyasından girişler çizer.

Aşağıdaki tabloda, ilk düğüm içindeki bir proje dosyasına eklenebilen MSBuild özellikleri açıklanmaktadır `<PropertyGroup>` . Bu düzenlemeleri Visual Studio 2017 ve sonraki sürümlerde kolayca yaparak, projeye sağ tıklayıp bağlam menüsünde **{Project_Name} Düzenle** ' yi seçerek yapabilirsiniz. Kolaylık sağlaması için tablo, bir [ `.nuspec` dosyadaki](../reference/nuspec.md)denk özelliğe göre düzenlenir.

`Owners`Ve `Summary` özelliklerinin `.nuspec` MSBuild ile desteklenmediğini unutmayın.

| Öznitelik/NuSpec değeri | MSBuild özelliği | Varsayılan | Notlar |
|--------|--------|--------|--------|
| Id | PackageID | AssemblyName | MSBuild 'ten $ (AssemblyName) |
| Sürüm | PackageVersion | Sürüm | Bu semver uyumludur, örneğin "1.0.0", "1.0.0-Beta" veya "1.0.0-Beta-00345" |
| VersionPrefix | PackageVersionPrefix | empty | PackageVersion ayarı PackageVersionPrefix üzerine yazıyor |
| VersionSuffix | PackageVersionSuffix | empty | MSBuild 'ten $ (VersionSuffix). PackageVersion ayarı PackageVersionSuffix üzerine yazıyor |
| Yazarlar | Yazarlar | Geçerli kullanıcının Kullanıcı adı | Nuget.org üzerindeki profil adlarıyla eşleşen paket yazarları için noktalı virgülle ayrılmış bir liste. Bunlar, nuget.org üzerindeki NuGet galerisinde görüntülenir ve aynı yazarlara göre çapraz başvuru için kullanılır. |
| Sahipler | Yok | NuSpec içinde yok | |
| Başlık | Başlık | PackageID| Genellikle, Kullanıcı arabiriminde kullanılan ve Visual Studio 'da paket yöneticisi olarak görüntülenen, paketin kolay bir başlığı. |
| Açıklama | Açıklama | "Paket açıklaması" | Derleme için uzun bir açıklama. `PackageDescription`Belirtilmezse, bu özellik paketin açıklaması olarak da kullanılır. |
| Telif Hakkı | Telif Hakkı | empty | Paket için telif hakkı ayrıntıları. |
| Requirelicensekabulünü | Packagerequirelicensekabulünü | yanlış | İstemcinin paketi yüklemeden önce paket lisansını kabul etmesini isteyip istemeyeceğini belirten bir Boole değeri. |
| lisans | PackageLicenseExpression | empty | Öğesine karşılık gelir `<license type="expression">` . Bkz. [Lisans ifadesi veya lisans dosyası paketleme](#packing-a-license-expression-or-a-license-file). |
| lisans | PackageLicenseFile | empty | Özel bir lisans veya bir SPDX tanımlayıcısı atanmamış bir lisans kullanıyorsanız paket içindeki bir lisans dosyasının yolu. Başvurulan lisans dosyasını açık bir şekilde paketetmeniz gerekir. Öğesine karşılık gelir `<license type="file">` . Bkz. [Lisans ifadesi veya lisans dosyası paketleme](#packing-a-license-expression-or-a-license-file). |
| LicenseUrl | PackageLicenseUrl 'Si | empty | `PackageLicenseUrl` kullanım dışıdır. `PackageLicenseExpression` `PackageLicenseFile` Bunun yerine veya kullanın. |
| ProjectUrl | PackageProjectUrl | empty | |
| Simge | Packageıcon | empty | Paket simgesi olarak kullanılacak paketteki bir görüntünün yolu. Başvurulan simge görüntü dosyasını açıkça paketetmeniz gerekir. Daha fazla bilgi için bkz. [paketleme bir simge görüntü dosyası](#packing-an-icon-image-file) ve [ `icon` meta verileri](/nuget/reference/nuspec#icon). |
| Iurl | PackageIconUrl 'Si | empty | `PackageIconUrl` kullanım dışı bırakılmıştır `PackageIcon` . Ancak, en iyi alt düzey deneyim için öğesine ek olarak belirtmeniz gerekir `PackageIconUrl` `PackageIcon` . |
| Etiketler | PackageTags | empty | Paketi atayan etiketlerin noktalı virgülle ayrılmış listesi. |
| Relet 'ler | PackageReleaseNotes | empty | Paket için sürüm notları. |
| Depo/URL | Depourl 'Si | empty | Kaynak kodu kopyalamak veya almak için kullanılan depo URL 'SI. Örnek: *https://github.com/NuGet/NuGet.Client.git* . |
| Depo/tür | Repositorytype parametrelerinin sağlanması | empty | Depo türü. Örnekler: `git` (varsayılan), `tfs` . |
| Depo/dal | Depodalı | empty | İsteğe bağlı depo dalı bilgileri. `RepositoryUrl` Bu özelliğin dahil edilmesini sağlamak için de belirtilmesi gerekir. Örnek: *Master* (NuGet 4.7.0 +). |
| Depo/kayıt | Kayıt yapma | empty | Paketin hangi kaynağa göre oluşturulduğunu göstermek için isteğe bağlı depo kaydı veya değişiklik kümesi. `RepositoryUrl` Bu özelliğin dahil edilmesini sağlamak için de belirtilmesi gerekir. Örnek: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +). |
| PackageType | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| Özet | Desteklenmez | | |

### <a name="pack-target-inputs"></a>Paket hedef girişleri

| Özellik | Açıklama |
| - | - |
| Ispackable | Projenin paketlenemeyeceğini belirten bir Boole değeri. `true` varsayılan değerdir. |
| Suppressbağımlıcıeswhenpaketleme | `true`Oluşturulan NuGet paketinden paket bağımlılıklarını bastırmak için olarak ayarlayın. |
| PackageVersion | Elde edilen paketin sahip olacağı sürümü belirtir. Tüm NuGet sürüm dizesi formlarını kabul eder. Varsayılan değeri,, `$(Version)` Yani, projedeki özelliğinin değeridir `Version` . |
| PackageID | Sonuç paketinin adını belirtir. Belirtilmemişse, `pack` işlem varsayılan `AssemblyName` olarak paketin adı ile veya dizin adını kullanacaktır. |
| PackageDescription | UI görüntüleme paketinin uzun açıklaması. |
| Yazarlar | Nuget.org üzerindeki profil adlarıyla eşleşen paket yazarları için noktalı virgülle ayrılmış bir liste. Bunlar, nuget.org üzerindeki NuGet galerisinde görüntülenir ve aynı yazarlara göre çapraz başvuru için kullanılır. |
| Açıklama | Derleme için uzun bir açıklama. `PackageDescription`Belirtilmezse, bu özellik paketin açıklaması olarak da kullanılır. |
| Telif Hakkı | Paket için telif hakkı ayrıntıları. |
| Packagerequirelicensekabulünü | İstemcinin paketi yüklemeden önce paket lisansını kabul etmesini isteyip istemeyeceğini belirten bir Boole değeri. Varsayılan değer: `false`. |
| DevelopmentDependency | Paketin bir yalnızca geliştirme bağımlılığı olarak işaretlenip işaretlenmediğini belirten ve paketin diğer paketlere bağımlılık olarak eklenmesini önleyen bir Boole değeri. `PackageReference`(NuGet 4.8 +) ile bu bayrak, derleme zamanı varlıklarının derlemeden dışlandığı anlamına gelir. Daha fazla bilgi için bkz. [PackageReference Için Developmentdependency desteği](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference). |
| PackageLicenseExpression | Örneğin, bir [Spdx lisans tanımlayıcısı](https://spdx.org/licenses/) veya ifadesi `Apache-2.0` . Daha fazla bilgi için bkz. [Lisans ifadesi veya lisans dosyası paketleme](#packing-a-license-expression-or-a-license-file). |
| PackageLicenseFile | Özel bir lisans veya bir SPDX tanımlayıcısı atanmamış bir lisans kullanıyorsanız paket içindeki bir lisans dosyasının yolu. |
| PackageLicenseUrl 'Si | `PackageLicenseUrl` kullanım dışıdır. `PackageLicenseExpression` `PackageLicenseFile` Bunun yerine veya kullanın. |
| PackageProjectUrl | |
| Packageıcon | Paketin köküne göre paket simge yolunu belirtir. Daha fazla bilgi için bkz. [paketleme a Icon Image File](#packing-an-icon-image-file). |
| PackageReleaseNotes| Paket için sürüm notları. |
| PackageTags | Paketi atayan etiketlerin noktalı virgülle ayrılmış listesi. |
| PackageOutputPath | Paketlenmiş paketin bırakılacak çıkış yolunu belirler. `$(OutputPath)` varsayılan değerdir. |
| Includesymbols | Bu Boole değeri, paketin proje paketedildiğinde ek bir sembol paketi oluşturup oluşturmayacağını gösterir. Semboller paketinin biçimi, özelliği tarafından denetlenir `SymbolPackageFormat` . Daha fazla bilgi için bkz. [ıncludesymbols](#includesymbols). |
| Includesource | Bu Boole değeri, paket işleminin bir kaynak paketi oluşturup oluşturmayacağını gösterir. Kaynak paket, kitaplığın kaynak kodunu ve PDB dosyalarını içerir. Kaynak dosyalar, `src/ProjectName` elde edilen paket dosyasındaki dizinin altına yerleştirilir. Daha fazla bilgi için bkz. [ıncludesource](#includesource). |
| PackageTypes
| IsTool | Tüm çıkış dosyalarının *lib* klasörü yerine *Araçlar* klasörüne kopyalanıp kopyalanmayacağını belirtir. Daha fazla bilgi için bkz. [ISTool](#istool). |
| Depourl 'Si | Kaynak kodu kopyalamak veya almak için kullanılan depo URL 'SI. Örnek: *https://github.com/NuGet/NuGet.Client.git* . |
| Repositorytype parametrelerinin sağlanması | Depo türü. Örnekler: `git` (varsayılan), `tfs` . |
| Depodalı | İsteğe bağlı depo dalı bilgileri. `RepositoryUrl` Bu özelliğin dahil edilmesini sağlamak için de belirtilmesi gerekir. Örnek: *Master* (NuGet 4.7.0 +). |
| Kayıt yapma | Paketin hangi kaynağa göre oluşturulduğunu göstermek için isteğe bağlı depo kaydı veya değişiklik kümesi. `RepositoryUrl` Bu özelliğin dahil edilmesini sağlamak için de belirtilmesi gerekir. Örnek: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +). |
| SymbolPackageFormat | Semboller paketinin biçimini belirtir. "Symbols. nupkg" ise, pdb 'leri, dll 'Ler ve diğer çıktı dosyalarını içeren *. Symbols. nupkg* Uzantısı ile eski bir sembol paketi oluşturulur. "Snupkg" ise, taşınabilir pdb 'leri içeren bir snupkg sembol paketi oluşturulur. Varsayılan değer "symbols. nupkg" dır. |
| NoPackageAnalysis | `pack`Paketi derlemeden sonra paket analizini çalıştırmamalıdır. |
| MinClientVersion | Bu paketi yükleyecan nuget.exe ve Visual Studio Paket Yöneticisi tarafından zorlanan NuGet istemcisinin en düşük sürümünü belirtir. |
| IncludeBuildOutput | Bu Boole değeri, derleme çıkış derlemelerinin *. nupkg* dosyasına paketedilip edilmeyeceğini belirtir. |
| Includecontentınpack | Bu Boole değeri, türü olan herhangi bir öğenin `Content` elde edilen pakete otomatik olarak dahil edilip edilmeyeceğini belirtir. Varsayılan değer: `true`. |
| BuildOutputTargetFolder | Çıkış derlemelerinin yerleştirileceği klasörü belirtir. Çıkış derlemeleri (ve diğer çıkış dosyaları) ilgili çerçeve klasörlerine kopyalanır. Daha fazla bilgi için bkz. [Çıkış derlemeleri](#output-assemblies). |
| ContentTargetFolders | Kendileri için belirtilmemişse, tüm içerik dosyalarının gitmesi gereken varsayılan konumu belirtir `PackagePath` . Varsayılan değer "Content; contentFiles" dır. Daha fazla bilgi için bkz. [bir paketteki Içerik ekleme](#including-content-in-a-package). |
| Nusguus dosyası | Paketleme için kullanılan *. nuspec* dosyasının göreli veya mutlak yolu. Belirtilmişse, **yalnızca** paketleme bilgileri için kullanılır ve projelerdeki tüm bilgiler kullanılmaz. Daha fazla bilgi için bkz [.. nuspec kullanarak paketleme](#packing-using-a-nuspec). |
| Nusgubasepath | *. Nuspec* dosyasının temel yolu. Daha fazla bilgi için bkz [.. nuspec kullanarak paketleme](#packing-using-a-nuspec). |
| Nus, Properties | Anahtar = değer çiftlerinin noktalı virgülle ayrılmış listesi. Daha fazla bilgi için bkz [.. nuspec kullanarak paketleme](#packing-using-a-nuspec). |

## <a name="pack-scenarios"></a>paket senaryoları

### <a name="suppress-dependencies"></a>Bağımlılıkları gösterme

Oluşturulan NuGet paketinden paket bağımlılıklarını bastırmak için, olarak ayarlayın `SuppressDependenciesWhenPacking` ve `true` oluşturulan nupkg dosyasından tüm bağımlılıkların atlanmasını sağlar.

### <a name="packageiconurl"></a>PackageIconUrl 'Si

`PackageIconUrl` özelliği kullanım dışı bırakılmıştır [`PackageIcon`](#packageicon) . NuGet 5,3 ve Visual Studio 2019 sürüm 16,3 ' den başlayarak, `pack` paket meta verileri yalnızca belirtiyorsa [NU5048](./errors-and-warnings/nu5048.md) uyarısını yayınlar `PackageIconUrl` .

### <a name="packageicon"></a>Packageıcon

> [!Tip]
> Henüz desteklemeyen istemcilerle ve kaynaklarla geriye dönük uyumluluk sağlamak için hem hem `PackageIcon` de belirtin `PackageIcon` `PackageIconUrl` . Visual Studio, `PackageIcon` Klasör tabanlı bir kaynaktan gelen paketler için destekler.

#### <a name="packing-an-icon-image-file"></a>Simge görüntüsü dosyası paketleme

Bir simge görüntü dosyası paketleme sırasında, `PackageIcon` paketin köküne göre simge dosya yolunu belirtmek için özelliğini kullanın. Ayrıca, dosyanın pakete eklendiğinden emin olun. Görüntü dosyası boyutu 1 MB ile sınırlıdır. Desteklenen dosya biçimleri JPEG ve PNG içerir. 128x128 görüntü çözümlemesi yapmanızı öneririz.

Örneğin:

```xml
<PropertyGroup>
    ...
    <PackageIcon>icon.png</PackageIcon>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="images\icon.png" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

[Paket simgesi örneği](https://github.com/NuGet/Samples/tree/master/PackageIconExample).

Nuspec eşdeğeri için, [simgenin nuspec başvurusuna](nuspec.md#icon)göz atın.

### <a name="output-assemblies"></a>Çıkış derlemeleri

`nuget pack` çıktı dosyalarını,,,, ve uzantılarına kopyalar `.exe` `.dll` `.xml` `.winmd` `.json` `.pri` . Kopyalanan çıkış dosyaları, hedef tarafından MSBuild 'in sağladığı şuna bağlıdır `BuiltOutputProjectGroup` .

Çıktı derlemelerinin nerede olduğunu denetlemek için, proje dosyanızda veya komut satırında kullanabileceğiniz iki MSBuild özelliği vardır:

- `IncludeBuildOutput`: Derleme çıkış derlemelerinin pakete dahil edilip edilmeyeceğini belirleyen bir Boole değeri.
- `BuildOutputTargetFolder`: Çıkış derlemelerinin yerleştirilmesi gereken klasörü belirtir. Çıkış derlemeleri (ve diğer çıkış dosyaları) ilgili çerçeve klasörlerine kopyalanır.

### <a name="package-references"></a>Paket başvuruları

Bkz. [Proje dosyalarındaki paket başvuruları](../consume-packages/package-references-in-project-files.md).

### <a name="project-to-project-references"></a>Projeden projeye başvurular

Proje başvuruları, varsayılan olarak NuGet paket başvuruları olarak değerlendirilir, örneğin:

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

Ayrıca, proje başvurunuz için aşağıdaki meta verileri de ekleyebilirsiniz:

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a>Bir paketteki içerik ekleme

İçerik eklemek için var olan öğeye ek meta veriler ekleyin `<Content>` . Varsayılan olarak, aşağıdaki gibi girdilerle geçersiz kılmadığınız müddetçe "Içerik" türünde her şey pakete dahil edilir:

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

Varsayılan olarak, her şey `content` `contentFiles\any\<target_framework>` bir paket içindeki ve klasörünün köküne eklenir ve bir paket yolu belirtmediğiniz takdirde göreli klasör yapısını korur:

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

Tüm içeriğinizi yalnızca belirli bir kök klasöre ( `content` ve her ikisi yerine) kopyalamak istiyorsanız, `contentFiles` Varsayılan olarak `ContentTargetFolders` "Content; ContentFiles" olan, ancak başka bir klasör adına ayarlanabilir MSBuild özelliğini kullanabilirsiniz. Yalnızca `ContentTargetFolders` dosyaları ' ın altında `contentFiles\any\<target_framework>` veya `contentFiles\<language>\<target_framework>` temel alarak "ContentFiles" seçeneğinin belirtildiğine unutmayın `buildAction` .

`PackagePath` noktalı virgülle ayrılmış bir hedef yolları kümesi olabilir. Boş bir paket yolu belirtilmesi, dosyayı paketin köküne ekler. Örneğin, aşağıdaki, `libuv.txt` `content\myfiles` `content\samples` ve paket köküne ekler:

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

Ayrıca `$(IncludeContentInPack)` , varsayılan olarak olan MSBuild özelliği de vardır `true` . Bu, `false` herhangi bir projede olarak ayarlandıysa, bu projeden içerik NuGet paketine dahil edilmez.

Yukarıdaki öğelerin herhangi birine ayarlayabileceğiniz diğer paketine özgü meta veriler içerir ```<PackageCopyToOutput>``` ve ```<PackageFlatten>``` ```CopyToOutput``` ```Flatten``` ```contentFiles``` Çıkış nuspec içindeki giriş üzerinde ve değerlerini belirler.

> [!Note]
> Içerik öğelerinden ayrı olarak, `<Pack>` ve `<PackagePath>` meta veriler de derleme, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, Designdata, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, Paketleresource veya None derleme eylemine sahip dosyalar üzerinde de ayarlanabilir.
>
> Glob desenleri kullanılırken dosya adını paket yolunuza eklemek için paket yolu, klasör ayırıcı karakteriyle bitmelidir; Aksi takdirde, paket yolu dosya adı dahil tam yol olarak değerlendirilir.

### <a name="includesymbols"></a>Includesymbols

Kullanırken `MSBuild -t:pack -p:IncludeSymbols=true` , karşılık gelen `.pdb` dosyalar diğer çıkış dosyalarıyla birlikte kopyalanır ( `.dll` ,,, `.exe` `.winmd` `.xml` , `.json` , `.pri` ). Ayarın `IncludeSymbols=true` düzenli bir paket *ve* bir semboller paketi oluşturduğunu unutmayın.

### <a name="includesource"></a>Includesource

Bu, `IncludeSymbols` ile aynıdır, ancak kaynak dosyalarını da dosyalarla birlikte kopyalar `.pdb` . Tüm dosya türleri, `Compile` `src\<ProjectName>\` elde edilen paketteki göreli yol klasörü yapısını korumak için üzerine kopyalanır. Aynı zamanda, olarak ayarlanmış herhangi bir kaynak dosyası için de aynı olur `ProjectReference` `TreatAsPackageReference` `false` .

Derleme türü bir dosya proje klasörünün dışında ise, ' ye eklenmiştir `src\<ProjectName>\` .

### <a name="packing-a-license-expression-or-a-license-file"></a>Lisans ifadesi veya lisans dosyası paketleme

Bir lisans ifadesi kullanırken, `PackageLicenseExpression` özelliğini kullanın. Bir örnek için bkz. [Lisans ifadesi örneği](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

NuGet.org tarafından kabul edilen lisans ifadeleri ve lisanslar hakkında daha fazla bilgi için bkz. [Lisans meta verileri](nuspec.md#license).

Bir lisans dosyası paketleme sırasında, paketin `PackageLicenseFile` köküne göre paket yolunu belirtmek için özelliğini kullanın. Ayrıca, dosyanın pakete eklendiğinden emin olun. Örneğin:

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

Bir örnek için bkz. [Lisans dosyası örneği](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).

> [!NOTE]
> Tek seferde,, ve yalnızca biri `PackageLicenseExpression` `PackageLicenseFile` `PackageLicenseUrl` belirtilebilir.

### <a name="packing-a-file-without-an-extension"></a>Uzantı olmadan dosya paketleme

Bir lisans dosyası paketleme gibi bazı senaryolarda, uzantısı olmayan bir dosya eklemek isteyebilirsiniz.
Geçmiş nedenlerle NuGet & MSBuild, bir uzantısı olmayan yolları dizin olarak değerlendirir.

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

[Dosya uzantı örneği olmadan](https://github.com/NuGet/Samples/blob/master/PackageLicenseFileExtensionlessExample/).
### <a name="istool"></a>IsTool

Kullanırken `MSBuild -t:pack -p:IsTool=true` , [Çıkış derlemeleri](#output-assemblies) senaryosunda belirtilen tüm çıkış dosyaları, `tools` klasörü yerine klasörüne kopyalanır `lib` . Bunun, `DotNetCliTool` içindeki dosyasını ayarlayarak belirtilen öğesinden farklı olduğunu unutmayın `PackageType` `.csproj` .

### <a name="packing-using-a-nuspec"></a>. Nuspec kullanarak paketleme

Bunun yerine genellikle proje dosyasındaki dosyada bulunan [tüm özellikleri eklemeniz](../reference/msbuild-targets.md#pack-target) önerilse de `.nuspec` , `.nuspec` projenizi paketlebilmeniz için bir dosya kullanmayı seçebilirsiniz. Tarafından kullanılan SDK olmayan bir proje için `PackageReference` , paket görevinin yürütülebilmesi için içeri aktarmanız gerekir `NuGet.Build.Tasks.Pack.targets` . Bir nuspec dosyası paketetmeden önce projeyi geri yüklemeniz gerekir. (SDK stili bir proje varsayılan olarak paket hedeflerini içerir.)

Proje dosyasının hedef çerçevesi ilgisizdir ve bir nuspec paketleme sırasında kullanılmaz. Aşağıdaki üç MSBuild özelliği, ile paketleme ile ilgilidir `.nuspec` :

1. `NuspecFile`: `.nuspec` paketleme için kullanılan dosyanın göreli veya mutlak yolu.
1. `NuspecProperties`: Key = değer çiftleri için noktalı virgülle ayrılmış bir liste. MSBuild komut satırı ayrıştırması çalışma yöntemi nedeniyle, birden çok özellik şu şekilde belirtilmelidir: `-p:NuspecProperties="key1=value1;key2=value2"` .  
1. `NuspecBasePath`: Dosyanın temel yolu `.nuspec` .

`dotnet.exe`Projenizi paketmek için kullanıyorsanız, aşağıdaki gibi bir komut kullanın:

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Projenizi paketmek için MSBuild kullanıyorsanız, aşağıdaki gibi bir komut kullanın:

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

dotnet.exe veya MSBuild kullanarak bir nuspec paketleme, projenin varsayılan olarak oluşturulmasına da neden olduğuna lütfen emin olun. Bu, proje dosyanızdaki ```--no-build``` ```<NoBuild>true</NoBuild> ``` ayar ile birlikte proje dosyanızdaki ayarın eşdeğeri olan dotnet.exe özelliği ' a geçirerek kaçınılabilir ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` .

Bir nuspec dosyası paketiçin bir *. csproj* dosyası örneği:

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <NoBuild>true</NoBuild>
    <IncludeBuildOutput>false</IncludeBuildOutput>
    <NuspecFile>PATH_TO_NUSPEC_FILE</NuspecFile>
    <NuspecProperties>add nuspec properties here</NuspecProperties>
    <NuspecBasePath>optional to provide</NuspecBasePath>
  </PropertyGroup>
</Project>
```

### <a name="advanced-extension-points-to-create-customized-package"></a>Özelleştirilmiş paket oluşturmak için gelişmiş uzantı noktaları

`pack`Hedef, iç, hedef çerçeveye özgü derlemede çalışan iki uzantı noktası sağlar. Uzantı noktaları, hedef çerçeveye özgü içerik ve derlemelerin bir pakete dahil edilmesi için destek:

- `TargetsForTfmSpecificBuildOutput` target: klasör içindeki dosyaları `lib` veya kullanılarak belirtilen klasörü kullanın `BuildOutputTargetFolder` .
- `TargetsForTfmSpecificContentInPackage` target: dışındaki dosyalar için kullanın `BuildOutputTargetFolder` .

#### <a name="targetsfortfmspecificbuildoutput"></a>TargetsForTfmSpecificBuildOutput

Özel bir hedef yazın ve özelliğin değeri olarak belirtin `$(TargetsForTfmSpecificBuildOutput)` . (Varsayılan olarak LIB) öğesine gitmesi gereken tüm dosyalar için `BuildOutputTargetFolder` , hedef bu dosyaları ItemGroup 'a yazmalıdır `BuildOutputInPackage` ve aşağıdaki iki meta veri değerini ayarlamış olmalıdır:

- `FinalOutputPath`: Dosyanın mutlak yolu; sağlanmazsa, kimlik kaynak yolunu değerlendirmek için kullanılır.
- `TargetPath`: (İsteğe bağlı) dosyanın içindeki bir alt klasöre gitmesi gerektiğinde ayarlanır `lib\<TargetFramework>` . Bu, ilgili kültür klasörlerinin altına giten uydu derlemeleri gibi. Varsayılan olarak dosyanın adıdır.

Örnek:

```xml
<PropertyGroup>
  <TargetsForTfmSpecificBuildOutput>$(TargetsForTfmSpecificBuildOutput);GetMyPackageFiles</TargetsForTfmSpecificBuildOutput>
</PropertyGroup>

<Target Name="GetMyPackageFiles">
  <ItemGroup>
    <BuildOutputInPackage Include="$(OutputPath)cs\$(AssemblyName).resources.dll">
        <TargetPath>cs</TargetPath>
    </BuildOutputInPackage>
  </ItemGroup>
</Target>
```

#### <a name="targetsfortfmspecificcontentinpackage"></a>Targetsfortfmspecificcontenınpackage

Özel bir hedef yazın ve özelliğin değeri olarak belirtin `$(TargetsForTfmSpecificContentInPackage)` . Pakete dahil edilecek tüm dosyalar için, hedef bu dosyaları ItemGroup 'a yazmalıdır `TfmSpecificPackageFile` ve aşağıdaki isteğe bağlı meta verileri ayarlar:

- `PackagePath`: Dosyanın pakette çıkış olması gereken yol. Aynı paket yoluna birden fazla dosya eklenirse NuGet bir uyarı verir.
- `BuildAction`: Dosyaya atanacak derleme eylemi, yalnızca paket yolu `contentFiles` klasörsise gereklidir. Varsayılan "none" olarak belirlenmiştir.

Örnek:
```xml
<PropertyGroup>
  <TargetsForTfmSpecificContentInPackage>$(TargetsForTfmSpecificContentInPackage);CustomContentTarget</TargetsForTfmSpecificContentInPackage>
</PropertyGroup>

<Target Name="CustomContentTarget">
  <ItemGroup>
    <TfmSpecificPackageFile Include="abc.txt">
      <PackagePath>mycontent/$(TargetFramework)</PackagePath>
    </TfmSpecificPackageFile>
    <TfmSpecificPackageFile Include="Extensions/ext.txt" Condition="'$(TargetFramework)' == 'net46'">
      <PackagePath>net46content</PackagePath>
    </TfmSpecificPackageFile>  
  </ItemGroup>
</Target>  
```

## <a name="restore-target"></a>hedefi geri yükle

`MSBuild -t:restore` ( `nuget restore` `dotnet restore` .NET Core projeleriyle birlikte kullanılması), proje dosyasında başvurulan paketleri aşağıdaki şekilde geri yükler:

1. Proje başvurularına tüm projeyi oku
1. Ara klasörünü ve hedef çerçeveleri bulmak için proje özelliklerini okuyun
1. MSBuild verilerini NuGet.Build.Tasks.dll geçirin
1. Geri yüklemeyi Çalıştır
1. Paketleri İndir
1. Varlıklar dosyası, hedefler ve props yazma

`restore`Hedef, PackageReference biçimini kullanan projeler için geçerlidir.
`MSBuild 16.5+` Ayrıca, biçim için [kabul desteği](#restoring-packagereference-and-packagesconfig-with-msbuild) de vardır `packages.config` .

> [!NOTE]
> `restore`Hedef, hedefle birlikte [çalıştırılmamalıdır](#restoring-and-building-with-one-msbuild-command) `build` .

### <a name="restore-properties"></a>Özellikleri geri yükle

Ek geri yükleme ayarları proje dosyasındaki MSBuild özelliklerinden gelebilir. Değerler, anahtar kullanılarak komut satırından da ayarlanabilir `-p:` (aşağıdaki örneklere bakın).

| Özellik | Açıklama |
|--------|--------|
| RestoreSources | Paket kaynaklarının noktalı virgülle ayrılmış listesi. |
| RestorePackagesPath | Kullanıcı paketleri klasör yolu. |
| RestoreDisableParallel | İndirmeleri tek seferde bir ile sınırlayın. |
| RestoreConfigFile | `Nuget.Config`Uygulanacak dosyanın yolu. |
| RestoreNoCache | Doğru ise, önbelleğe alınmış paketlerin kullanılmasını önler. Bkz. [genel paketleri ve önbellek klasörlerini yönetme](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| Restoreıgnorefailedsources | Doğru ise, başarısız veya eksik paket kaynaklarını yoksayar. |
| RestoreFallbackFolders | Geri dönüş klasörleri, Kullanıcı paketleri klasörüyle aynı şekilde kullanılır. |
| Restoreaddıtionalprojectsources | Geri yükleme sırasında kullanılacak ek kaynaklar. |
| Restoreaddıtionalprojectfallbackfolders | Geri yükleme sırasında kullanılacak ek geri dönüş klasörleri. |
| RestoreAdditionalProjectFallbackFoldersExcludes | İçinde belirtilen geri dönüş klasörlerini dışlar `RestoreAdditionalProjectFallbackFolders` |
| RestoreTaskAssemblyFile | Yolu `NuGet.Build.Tasks.dll` . |
| Restoregraphprojectınput | Geri yüklenecek projelerin, mutlak yollar içermesi gereken, noktalı virgülle ayrılmış listesi. |
| Restoreuseskipnontenttargets  | Projeler MSBuild aracılığıyla toplandığında, iyileştirme kullanılarak toplanıp toplanmayacağını belirler `SkipNonexistentTargets` . Ayarlanmazsa, varsayılan olarak olur `true` . Projenin hedefleri içeri aktarılmadığı zaman, sonuç hızlı bir davranıştır. |
| Msbuildprojeclarsionspath | Çıkış klasörü, varsayılan olarak `BaseIntermediateOutputPath` ve `obj` klasörü. |
| Restorezorlamalı | PackageReference tabanlı projelerde, son geri yükleme başarılı olsa bile tüm bağımlılıkların çözülmesini zorlar. Bu bayrağın belirtilmesi, dosyanın silinmesine benzer `project.assets.json` . Bu, http-cache ' i atlar. |
| RestorePackagesWithLockFile | Bir kilit dosyasının kullanımıyla ilgili olarak. |
| RestoreLockedMode | Geri yüklemeyi kilitli modda çalıştırın. Bu, geri yüklemenin bağımlılıkları yeniden değerlendirmeyeceği anlamına gelir. |
| NuGetLockFilePath | Kilit dosyası için özel bir konum. Varsayılan konum projenin yanında bulunur ve adlandırılır `packages.lock.json` . |
| Restoreforcedeğerlendir | Bağımlılıkları yeniden hesaplamak ve herhangi bir uyarı olmadan kilit dosyasını güncelleştirmek için geri yüklemeyi zorlar. |
| RestorePackagesConfig | packages.config olan projeleri geri yükleyen bir kabul etme anahtarı. Yalnızca ile desteklenir `MSBuild -t:restore` . |
| Restoreusestaticgraphedeğerleme | Standart değerlendirme yerine statik grafik MSBuild değerlendirmesi kullanmak için bir tercih edilen anahtar. Statik grafik değerlendirmesi, büyük depolar ve çözümler için önemli ölçüde daha hızlı olan deneysel bir özelliktir. |

#### <a name="examples"></a>Örnekler

Komut satırı:

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

Proje dosyası:

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a>Çıkışları geri yükleme

Restore derleme klasöründe aşağıdaki dosyaları oluşturur `obj` :

| Dosya | Açıklama |
|--------|--------|
| `project.assets.json` | Tüm paket başvurularının bağımlılık grafiğini içerir. |
| `{projectName}.projectFileExtension.nuget.g.props` | Paketlerde bulunan MSBuild props 'a başvurular |
| `{projectName}.projectFileExtension.nuget.g.targets` | Paketlerde bulunan MSBuild hedeflerine başvurular |

### <a name="restoring-and-building-with-one-msbuild-command"></a>Tek bir MSBuild komutuyla geri yükleme ve oluşturma

NuGet, MSBuild hedeflerini ve props 'ı getiren paketleri geri yükleyebilir, geri yükleme ve derleme değerlendirmeleri farklı genel özelliklerle çalıştırılır.
Bu, aşağıdakilerin öngörülemeyen ve genellikle yanlış bir davranışa sahip olacağı anlamına gelir.

```cli
msbuild -t:restore,build
```

 Bunun yerine önerilen yaklaşım şunlardır:

```cli
msbuild -t:build -restore
```

Aynı Logic şuna benzer diğer hedefler için de geçerlidir `build` .

### <a name="restoring-packagereference-and-packagesconfig-with-msbuild"></a>MSBuild ile PackageReference ve packages.config geri yükleme

MSBuild 16.5 + ile packages.config de desteklenir `msbuild -t:restore` .

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> `packages.config` restore yalnızca ile kullanılabilir `MSBuild 16.5+` ve `dotnet.exe`

### <a name="restoring-with-msbuild-static-graph-evaluation"></a>MSBuild statik Graph değerlendirmesi ile geri yükleme

> [!NOTE]
> MSBuild 16.6 + ile, NuGet, büyük depolar için geri yükleme süresini önemli ölçüde artıran komut satırından statik grafik değerlendirmesi kullanmak için deneysel bir özellik eklemiştir.

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

Alternatif olarak, bir dizin. Build. props içindeki özelliği ayarlayarak bunu etkinleştirebilirsiniz.

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> Visual Studio 2019. x ve NuGet 5. x itibariyle, bu özellik deneysel ve kabul edilmelidir. Bu özelliğin varsayılan olarak etkinleştirileceği hakkında daha fazla bilgi için [NuGet/Home # 9803](https://github.com/NuGet/Home/issues/9803) izleyin.

Statik grafik geri yükleme, geri yükleme 'nin MSBuild bölümünü, Proje okuma ve değerlendirme, ancak geri yükleme algoritmasını etkilemez! Geri yükleme algoritması tüm NuGet araçları (NuGet.exe, MSBuild.exe, dotnet.exe ve Visual Studio) genelinde aynıdır.

Birçok senaryoda, statik grafik geri yükleme geçerli geri yüklemeden farklı davranabilir ve belirtilen bazı Packagereferklu veya ProjectReferences eksik olabilir.

Bir kez göz önünde bulundurmanız için, statik grafik geri yüklemeye geçiş yaparken şunu çalıştırmayı göz önünde bulundurun:

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

NuGet hiçbir *değişiklik bildirmemelidir* . Bir tutarsızlık görürseniz lütfen [NuGet/evde](https://github.com/nuget/home/issues/new)bir sorun bildirin.

### <a name="replacing-one-library-from-a-restore-graph"></a>Bir geri yükleme grafiğinden bir kitaplığı değiştirme

Geri yükleme yanlış derlemeyi alıyorsa, bu paketlerin varsayılan seçeneğini hariç tutabilir ve kendi seçimiyle değiştirin. Birincisi, en üst düzeyle `PackageReference` , tüm varlıkları hariç tut:

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

Ardından, DLL 'nin uygun yerel kopyasına kendi başvurunuz ekleyin:

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
