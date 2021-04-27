---
title: NuGethedef olarak Paketle ve geri yükle MSBuild
description: NuGet Paketleme ve geri yükleme, MSBuild 4.0 + ile doğrudan hedef olarak çalışabilir NuGet .
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
no-loc:
- NuGet
- MSBuild
- .nuspec
- nuspec
ms.openlocfilehash: 8ebf0329f9dc7af09a59f1498a934754842df365
ms.sourcegitcommit: 08c5b2c956a1a45f0ea9fb3f50f55e41312d8ce3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/27/2021
ms.locfileid: "108067316"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>NuGethedef olarak Paketle ve geri yükle MSBuild

*NuGet 4.0 +*

[Packagereference](../consume-packages/package-references-in-project-files.md) biçimiyle NuGet 4.0 +, tüm bildirim meta verilerini ayrı bir dosya kullanmak yerine doğrudan proje dosyası içinde depolayabilirler `.nuspec` .

MSBuild15.1 + ile, NuGet MSBuild `pack` aşağıda açıklandığı gibi, ve hedefleriyle birlikte birinci sınıf bir vatandaşlık `restore` . Bu hedefler, ile NuGet diğer herhangi bir MSBuild görev veya hedefle yaptığınız gibi çalışmanıza olanak sağlar. Kullanarak paket oluşturma yönergeleri için NuGet MSBuild bkz. [ NuGet kullanarak MSBuild paket oluşturma ](../create-packages/creating-a-package-msbuild.md). (İçin NuGet 3. x ve önceki sürümlerde, bunun yerine CLI aracılığıyla [paketle](../reference/cli-reference/cli-ref-pack.md) ve [geri yükleme](../reference/cli-reference/cli-ref-restore.md) komutlarını kullanırsınız NuGet .)

## <a name="target-build-order"></a>Hedef derleme sırası

`pack`Ve `restore` hedefleri olduğundan MSBuild , iş akışınızı iyileştirmek için bunlara erişebilirsiniz. Örneğin, paketledikten sonra paketinizi bir ağ paylaşımında kopyalamak istediğinizi varsayalım. Bunu, proje dosyanıza aşağıdakileri ekleyerek yapabilirsiniz:

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

Benzer şekilde, bir görev yazabilir MSBuild , kendi hedefini yazabilir ve NuGet görevde özellikleri kullanabilirsiniz MSBuild .

> [!NOTE]
> `$(OutputPath)` görelidir ve bu komutu proje kökünden çalıştırdığınız için bekliyor.

## <a name="pack-target"></a>paket hedefi

Biçimini kullanan .NET projeleri için `PackageReference` , `msbuild -t:pack` bir paket oluştururken kullanmak üzere proje dosyasından girişler çizer NuGet .

Aşağıdaki tabloda, MSBuild ilk düğüm içindeki bir proje dosyasına eklenebilen özellikler açıklanmaktadır `<PropertyGroup>` . Bu düzenlemeleri Visual Studio 2017 ve sonraki sürümlerde kolayca yaparak, projeye sağ tıklayıp bağlam menüsünde **{Project_Name} Düzenle** ' yi seçerek yapabilirsiniz. Kolaylık sağlaması için tablo, bir [ `.nuspec` dosyadaki](../reference/nuspec.md)denk özelliğe göre düzenlenir.

> [!NOTE]
> `Owners` ve `Summary` özellikleri `.nuspec` ile desteklenmez MSBuild .

| Öznitelik/ nuspec değer | MSBuild Özelliði | Varsayılan | Notlar |
|--------|--------|--------|--------|
| `Id` | `PackageId` | `$(AssemblyName)` | `$(AssemblyName)` Kaynak MSBuild |
| `Version` | `PackageVersion` | Sürüm | Bu, örneğin, veya gibi bir semver uyumludur. `1.0.0` `1.0.0-beta``1.0.0-beta-00345` |
| `VersionPrefix` | `PackageVersionPrefix` | empty | `PackageVersion`Üzerine yazma ayarları`PackageVersionPrefix` |
| `VersionSuffix` | `PackageVersionSuffix` | empty | `$(VersionSuffix)` öğesinden MSBuild . `PackageVersion`Üzerine yazma ayarları`PackageVersionSuffix` |
| `Authors` | `Authors` | Geçerli kullanıcının Kullanıcı adı | Nuget.org üzerindeki profil adlarıyla eşleşen paket yazarları için noktalı virgülle ayrılmış bir liste. Bunlar, NuGet NuGet.org üzerindeki galeride görüntülenir ve aynı yazarlara göre çapraz başvuru için kullanılır. |
| `Owners` | Yok | İçinde yok nuspec | |
| `Title` | `Title` | `PackageId` | Genellikle, Kullanıcı arabiriminde kullanılan ve Visual Studio 'da paket yöneticisi olarak görüntülenen, paketin kolay bir başlığı. |
| `Description` | `Description` | "Paket açıklaması" | Derleme için uzun bir açıklama. `PackageDescription`Belirtilmezse, bu özellik paketin açıklaması olarak da kullanılır. |
| `Copyright` | `Copyright` | empty | Paket için telif hakkı ayrıntıları. |
| `RequireLicenseAcceptance` | `PackageRequireLicenseAcceptance` | `false` | İstemcinin paketi yüklemeden önce paket lisansını kabul etmesini isteyip istemeyeceğini belirten bir Boole değeri. |
| `license` | `PackageLicenseExpression` | empty | Öğesine karşılık gelir `<license type="expression">` . Bkz. [Lisans ifadesi veya lisans dosyası paketleme](#packing-a-license-expression-or-a-license-file). |
| `license` | `PackageLicenseFile` | empty | Özel bir lisans veya bir SPDX tanımlayıcısı atanmamış bir lisans kullanıyorsanız paket içindeki bir lisans dosyasının yolu. Başvurulan lisans dosyasını açık bir şekilde paketetmeniz gerekir. Öğesine karşılık gelir `<license type="file">` . Bkz. [Lisans ifadesi veya lisans dosyası paketleme](#packing-a-license-expression-or-a-license-file). |
| `LicenseUrl` | `PackageLicenseUrl` | empty | `PackageLicenseUrl` kullanım dışıdır. `PackageLicenseExpression` `PackageLicenseFile` Bunun yerine veya kullanın. |
| `ProjectUrl` | `PackageProjectUrl` | empty | |
| `Icon` | `PackageIcon` | empty | Paket simgesi olarak kullanılacak paketteki bir görüntünün yolu. Başvurulan simge görüntü dosyasını açıkça paketetmeniz gerekir. Daha fazla bilgi için bkz. [paketleme bir simge görüntü dosyası](#packing-an-icon-image-file) ve [ `icon` meta verileri](./nuspec.md#icon). |
| `IconUrl` | `PackageIconUrl` | empty | `PackageIconUrl` kullanım dışı bırakılmıştır `PackageIcon` . Ancak, en iyi alt düzey deneyim için öğesine ek olarak belirtmeniz gerekir `PackageIconUrl` `PackageIcon` . |
| `Readme` | `PackageReadmeFile` | empty | Başvurulan Benioku dosyasını açıkça paketetmeniz gerekir.|
| `Tags` | `PackageTags` | empty | Paketi atayan etiketlerin noktalı virgülle ayrılmış listesi. |
| `ReleaseNotes` | `PackageReleaseNotes` | empty | Paket için sürüm notları. |
| `Repository/Url` | `RepositoryUrl` | empty | Kaynak kodu kopyalamak veya almak için kullanılan depo URL 'SI. Örnek: *https://github.com/ NuGet / NuGet . Client. git*. |
| `Repository/Type` | `RepositoryType` | empty | Depo türü. Örnekler: `git` (varsayılan), `tfs` . |
| `Repository/Branch` | `RepositoryBranch` | empty | İsteğe bağlı depo dalı bilgileri. `RepositoryUrl` Bu özelliğin dahil edilmesini sağlamak için de belirtilmesi gerekir. Örnek: *Master* ( NuGet 4.7.0 +). |
| `Repository/Commit` | `RepositoryCommit` | empty | Paketin hangi kaynağa göre oluşturulduğunu göstermek için isteğe bağlı depo kaydı veya değişiklik kümesi. `RepositoryUrl` Bu özelliğin dahil edilmesini sağlamak için de belirtilmesi gerekir. Örnek: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0 +). |
| `PackageType` | `<PackageType>CustomType1, 1.0.0.0;CustomType2</PackageType>` | | Paketin amaçlanan kullanımını gösterir. Paket türleri paket kimlikleri ile aynı biçimi kullanır ve tarafından sınırlandırılır `;` . Paket türleri bir ve dizesi eklenerek sürümlenebilir `,` [`Version`](/dotnet/api/system.version) . Bkz. [ NuGet paket türünü ayarlama](../create-packages/set-package-type.md) ( NuGet 3.5.0 +). |
| `Summary` | Desteklenmez | | |

### <a name="pack-target-inputs"></a>Paket hedef girişleri

| Özellik | Açıklama |
| - | - |
| `IsPackable` | Projenin paketlenemeyeceğini belirten bir Boole değeri. `true` varsayılan değerdir. |
| `SuppressDependenciesWhenPacking` | `true`Oluşturulan paketten paket bağımlılıklarını göstermemek için olarak ayarlayın NuGet . |
| `PackageVersion` | Elde edilen paketin sahip olacağı sürümü belirtir. Tüm sürüm dizesi biçimlerini kabul eder NuGet . Varsayılan değeri,, `$(Version)` Yani, projedeki özelliğinin değeridir `Version` . |
| `PackageId` | Sonuç paketinin adını belirtir. Belirtilmemişse, `pack` işlem varsayılan `AssemblyName` olarak paketin adı ile veya dizin adını kullanacaktır. |
| `PackageDescription` | UI görüntüleme paketinin uzun açıklaması. |
| `Authors` | Nuget.org üzerindeki profil adlarıyla eşleşen paket yazarları için noktalı virgülle ayrılmış bir liste. Bunlar, NuGet NuGet.org üzerindeki galeride görüntülenir ve aynı yazarlara göre çapraz başvuru için kullanılır. |
| `Description` | Derleme için uzun bir açıklama. `PackageDescription`Belirtilmezse, bu özellik paketin açıklaması olarak da kullanılır. |
| `Copyright` | Paket için telif hakkı ayrıntıları. |
| `PackageRequireLicenseAcceptance` | İstemcinin paketi yüklemeden önce paket lisansını kabul etmesini isteyip istemeyeceğini belirten bir Boole değeri. Varsayılan değer: `false`. |
| `DevelopmentDependency` | Paketin bir yalnızca geliştirme bağımlılığı olarak işaretlenip işaretlenmediğini belirten ve paketin diğer paketlere bağımlılık olarak eklenmesini önleyen bir Boole değeri. `PackageReference`( NuGet 4.8 +) ile bu bayrak, derleme zamanı varlıklarının derlemeden dışlandığı anlamına gelir. Daha fazla bilgi için bkz. [PackageReference Için Developmentdependency desteği](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference). |
| `PackageLicenseExpression` | Örneğin, bir [Spdx lisans tanımlayıcısı](https://spdx.org/licenses/) veya ifadesi `Apache-2.0` . Daha fazla bilgi için bkz. [Lisans ifadesi veya lisans dosyası paketleme](#packing-a-license-expression-or-a-license-file). |
| `PackageLicenseFile` | Özel bir lisans veya bir SPDX tanımlayıcısı atanmamış bir lisans kullanıyorsanız paket içindeki bir lisans dosyasının yolu. |
| `PackageLicenseUrl` | `PackageLicenseUrl` kullanım dışıdır. `PackageLicenseExpression` `PackageLicenseFile` Bunun yerine veya kullanın. |
| `PackageProjectUrl` | |
| `PackageIcon` | Paketin köküne göre paket simge yolunu belirtir. Daha fazla bilgi için bkz. [paketleme a Icon Image File](#packing-an-icon-image-file). |
| `PackageReleaseNotes` | Paket için sürüm notları. |
| `PackageReadmeFile` | Paket için README. |
| `PackageTags` | Paketi atayan etiketlerin noktalı virgülle ayrılmış listesi. |
| `PackageOutputPath` | Paketlenmiş paketin bırakılacak çıkış yolunu belirler. `$(OutputPath)` varsayılan değerdir. |
| `IncludeSymbols` | Bu Boole değeri, paketin proje paketedildiğinde ek bir sembol paketi oluşturup oluşturmayacağını gösterir. Semboller paketinin biçimi, özelliği tarafından denetlenir `SymbolPackageFormat` . Daha fazla bilgi için bkz. [ıncludesymbols](#includesymbols). |
| `IncludeSource` | Bu Boole değeri, paket işleminin bir kaynak paketi oluşturup oluşturmayacağını gösterir. Kaynak paket, kitaplığın kaynak kodunu ve PDB dosyalarını içerir. Kaynak dosyalar, `src/ProjectName` elde edilen paket dosyasındaki dizinin altına yerleştirilir. Daha fazla bilgi için bkz. [ıncludesource](#includesource). |
| `PackageType` | |
| `IsTool` | Tüm çıkış dosyalarının *lib* klasörü yerine *Araçlar* klasörüne kopyalanıp kopyalanmayacağını belirtir. Daha fazla bilgi için bkz. [ISTool](#istool). |
| `RepositoryUrl` | Kaynak kodu kopyalamak veya almak için kullanılan depo URL 'SI. Örnek: *https://github.com/ NuGet / NuGet . Client. git*. |
| `RepositoryType` | Depo türü. Örnekler: `git` (varsayılan), `tfs` . |
| `RepositoryBranch` | İsteğe bağlı depo dalı bilgileri. `RepositoryUrl` Bu özelliğin dahil edilmesini sağlamak için de belirtilmesi gerekir. Örnek: *Master* ( NuGet 4.7.0 +). |
| `RepositoryCommit` | Paketin hangi kaynağa göre oluşturulduğunu göstermek için isteğe bağlı depo kaydı veya değişiklik kümesi. `RepositoryUrl` Bu özelliğin dahil edilmesini sağlamak için de belirtilmesi gerekir. Örnek: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0 +). |
| `SymbolPackageFormat` | Semboller paketinin biçimini belirtir. "Symbols. nupkg" ise, pdb 'leri, dll 'Ler ve diğer çıktı dosyalarını içeren *. Symbols. nupkg* Uzantısı ile eski bir sembol paketi oluşturulur. "Snupkg" ise, taşınabilir pdb 'leri içeren bir snupkg sembol paketi oluşturulur. Varsayılan değer "symbols. nupkg" dır. |
| `NoPackageAnalysis` | `pack`Paketi derlemeden sonra paket analizini çalıştırmamalıdır. |
| `MinClientVersion` | NuGetnuget.exe ve Visual Studio Paket Yöneticisi tarafından zorlanan bu paketi yükleyesağlayan istemcinin en düşük sürümünü belirtir. |
| `IncludeBuildOutput` | Bu Boole değeri, derleme çıkış derlemelerinin *. nupkg* dosyasına paketedilip edilmeyeceğini belirtir. |
| `IncludeContentInPack` | Bu Boole değeri, türü olan herhangi bir öğenin `Content` elde edilen pakete otomatik olarak dahil edilip edilmeyeceğini belirtir. Varsayılan değer: `true`. |
| `BuildOutputTargetFolder` | Çıkış derlemelerinin yerleştirileceği klasörü belirtir. Çıkış derlemeleri (ve diğer çıkış dosyaları) ilgili çerçeve klasörlerine kopyalanır. Daha fazla bilgi için bkz. [Çıkış derlemeleri](#output-assemblies). |
| `ContentTargetFolders` | Kendileri için belirtilmemişse, tüm içerik dosyalarının gitmesi gereken varsayılan konumu belirtir `PackagePath` . Varsayılan değer "Content; contentFiles" dır. Daha fazla bilgi için bkz. [bir paketteki Içerik ekleme](#including-content-in-a-package). |
| `NuspecFile` | *.nuspec* Paketleme için kullanılan dosyanın göreli veya mutlak yolu. Belirtilmişse, **yalnızca** paketleme bilgileri için kullanılır ve projelerdeki tüm bilgiler kullanılmaz. Daha fazla bilgi için bkz. [Using a .nuspec paketleme ](#packing-using-a-nuspec-file). |
| `NuspecBasePath` | Dosya için temel yol *.nuspec* . Daha fazla bilgi için bkz. [Using a .nuspec paketleme ](#packing-using-a-nuspec-file). |
| `NuspecProperties` | Anahtar = değer çiftlerinin noktalı virgülle ayrılmış listesi. Daha fazla bilgi için bkz. [Using a .nuspec paketleme ](#packing-using-a-nuspec-file). |

## <a name="pack-scenarios"></a>paket senaryoları

### <a name="suppressing-dependencies"></a>Gizleme bağımlılıkları

Oluşturulan paketten paket bağımlılıklarını bastırmak için NuGet , olarak ayarlayın `SuppressDependenciesWhenPacking` ve `true` oluşturulan nupkg dosyasından tüm bağımlılıkların atlanmasını sağlar.

### `PackageIconUrl`

`PackageIconUrl` özelliği kullanım dışı bırakılmıştır [`PackageIcon`](#packageicon) . NuGet5,3 ve Visual Studio 2019 sürüm 16,3 ' den başlayarak, `pack` paket meta verileri yalnızca belirtiyorsa [NU5048](./errors-and-warnings/nu5048.md) uyarı oluşturur `PackageIconUrl` .

### `PackageIcon`

> [!Tip]
> Henüz desteklemeyen istemcilerle ve kaynaklarla geriye dönük uyumluluk sağlamak için hem hem `PackageIcon` de belirtin `PackageIcon` `PackageIconUrl` . Visual Studio, `PackageIcon` Klasör tabanlı bir kaynaktan gelen paketler için destekler.

#### <a name="packing-an-icon-image-file"></a>Simge görüntüsü dosyası paketleme

Bir simge görüntü dosyası paketleme sırasında, `PackageIcon` paketin köküne göre simge dosya yolunu belirtmek için özelliğini kullanın. Ayrıca, dosyanın pakete eklendiğinden emin olun. Görüntü dosyası boyutu 1 MB ile sınırlıdır. Desteklenen dosya biçimleri JPEG ve PNG içerir. 128x128 görüntü çözümlemesi yapmanızı öneririz.

Örnek:

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

[Paket simgesi örneği](https://github.com/NuGet/Samples/tree/main/PackageIconExample).

nuspecEşdeğer bir deyişle, [ nuspec simgeye yönelik başvuruya](nuspec.md#icon)göz atın.

### <a name="packagereadmefile"></a>PackageReadmeFile

***NuGet 5.10.0 Preview 2**  /  **.NET SDK 5.0.300** ve üstü ile desteklenir*

Bir Benioku dosyası paketleme sırasında, paketin `PackageReadmeFile` köküne göre paket yolunu belirtmek için özelliğini kullanmanız gerekir. Buna ek olarak, dosyanın pakete eklendiğinden emin olmanız gerekir. Desteklenen dosya biçimleri yalnızca Marklt (*. MD*) içerir.

Örnek:

```xml
<PropertyGroup>
    ...
    <PackageReadmeFile>readme.md</PackageReadmeFile>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="docs\readme.md" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

nuspecEşdeğer olarak, [ nuspec Benioku için başvuruya](nuspec.md#readme)göz atın.

### <a name="output-assemblies"></a>Çıkış derlemeleri

`nuget pack` çıktı dosyalarını,,,, ve uzantılarına kopyalar `.exe` `.dll` `.xml` `.winmd` `.json` `.pri` . Kopyalanan çıkış dosyaları MSBuild hedeften neler sundığına bağlıdır `BuiltOutputProjectGroup` .

MSBuildÇıktı derlemelerinin nerede olduğunu denetlemek için, proje dosyanızda veya komut satırında kullanabileceğiniz iki özellik vardır:

- `IncludeBuildOutput`: Derleme çıkış derlemelerinin pakete dahil edilip edilmeyeceğini belirleyen bir Boole değeri.
- `BuildOutputTargetFolder`: Çıkış derlemelerinin yerleştirilmesi gereken klasörü belirtir. Çıkış derlemeleri (ve diğer çıkış dosyaları) ilgili çerçeve klasörlerine kopyalanır.

### <a name="package-references"></a>Paket başvuruları

Bkz. [Proje dosyalarındaki paket başvuruları](../consume-packages/package-references-in-project-files.md).

### <a name="project-to-project-references"></a>Projeden projeye başvurular

Proje başvurularına proje başvuruları, paket başvuruları olarak varsayılan olarak kabul edilir NuGet . Örnek:

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

Tüm içeriğinizi yalnızca belirli bir kök klasöre ( `content` ve her ikisi yerine) kopyalamak istiyorsanız, `contentFiles` Varsayılan olarak MSBuild `ContentTargetFolders` "Content; ContentFiles" olarak ayarlanmış ancak başka bir klasör adına ayarlanabilir özelliğini kullanabilirsiniz. Yalnızca `ContentTargetFolders` dosyaları ' ın altında `contentFiles\any\<target_framework>` veya `contentFiles\<language>\<target_framework>` temel alarak "ContentFiles" seçeneğinin belirtildiğine unutmayın `buildAction` .

`PackagePath` noktalı virgülle ayrılmış bir hedef yolları kümesi olabilir. Boş bir paket yolu belirtilmesi, dosyayı paketin köküne ekler. Örneğin, aşağıdaki, `libuv.txt` `content\myfiles` `content\samples` ve paket köküne ekler:

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

Ayrıca MSBuild `$(IncludeContentInPack)` , varsayılan olarak olan bir özellik vardır `true` . Bu, `false` herhangi bir projede olarak ayarlandıysa, bu projeden içerik NuGet paketine dahil edilmez.

Yukarıdaki öğelerin herhangi birine ayarlayabileceğiniz diğer paketine özgü meta veriler de dahil olmak üzere ```<PackageCopyToOutput>``` ```<PackageFlatten>``` ```CopyToOutput``` ```Flatten``` ```contentFiles``` , çıktı içindeki giriş ve değer değerlerini içerir nuspec .

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

Bir lisans ifadesi kullanırken, `PackageLicenseExpression` özelliğini kullanın. Bir örnek için bkz. [Lisans ifadesi örneği](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample).

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

Lisans ifadeleri ve. org tarafından kabul edilen lisanslar hakkında daha fazla bilgi edinmek için NuGet bkz. [Lisans meta verileri](nuspec.md#license).

Bir lisans dosyası paketleme sırasında, paketin `PackageLicenseFile` köküne göre paket yolunu belirtmek için özelliğini kullanın. Ayrıca, dosyanın pakete eklendiğinden emin olun. Örnek:

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

Bir örnek için bkz. [Lisans dosyası örneği](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample).

> [!NOTE]
> Tek seferde,, ve yalnızca biri `PackageLicenseExpression` `PackageLicenseFile` `PackageLicenseUrl` belirtilebilir.

### <a name="packing-a-file-without-an-extension"></a>Uzantı olmadan dosya paketleme

Bir lisans dosyası paketleme gibi bazı senaryolarda, uzantısı olmayan bir dosya eklemek isteyebilirsiniz.
Geçmiş nedenlerle, NuGet  &  MSBuild bir uzantısı olmayan yolları dizin olarak değerlendirin.

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

[Dosya uzantı örneği olmadan](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/).

### <a name="istool"></a>IsTool

Kullanırken `MSBuild -t:pack -p:IsTool=true` , [Çıkış derlemeleri](#output-assemblies) senaryosunda belirtilen tüm çıkış dosyaları, `tools` klasörü yerine klasörüne kopyalanır `lib` . Bunun, `DotNetCliTool` içindeki dosyasını ayarlayarak belirtilen öğesinden farklı olduğunu unutmayın `PackageType` `.csproj` .

### <a name="packing-using-a-nuspec-file"></a>Dosya kullanarak paketleme `.nuspec`

Bunun yerine genellikle proje dosyasındaki dosyada bulunan [tüm özellikleri eklemeniz](../reference/msbuild-targets.md#pack-target) önerilse de `.nuspec` , `.nuspec` projenizi paketlebilmeniz için bir dosya kullanmayı seçebilirsiniz. Tarafından kullanılan SDK olmayan bir proje için `PackageReference` , paket görevinin yürütülebilmesi için içeri aktarmanız gerekir `NuGet.Build.Tasks.Pack.targets` . Bir dosyayı paketetmeden önce projeyi geri yüklemeniz gerekir nuspec . (SDK stili bir proje varsayılan olarak paket hedeflerini içerir.)

Proje dosyasının hedef çerçevesi ilgisizdir ve bir paketleme sırasında kullanılmaz nuspec . Aşağıdaki üç MSBuild özellik, ile paketleme için geçerlidir `.nuspec` :

1. `NuspecFile`: `.nuspec` paketleme için kullanılan dosyanın göreli veya mutlak yolu.
1. `NuspecProperties`: Key = değer çiftleri için noktalı virgülle ayrılmış bir liste. MSBuildKomut satırı ayrıştırması çalışma yöntemi nedeniyle, birden çok özellik şu şekilde belirtilmelidir: `-p:NuspecProperties="key1=value1;key2=value2"` .  
1. `NuspecBasePath`: Dosyanın temel yolu `.nuspec` .

`dotnet.exe`Projenizi paketmek için kullanıyorsanız, aşağıdaki gibi bir komut kullanın:

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

MSBuildProjenizi paketmek için kullanıyorsanız, aşağıdaki gibi bir komut kullanın:

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

nuspecdotnet.exe veya MSBuild kullanan paketleme, projenin varsayılan olarak oluşturulmasına da neden olduğuna emin olun. Bu, proje dosyanızdaki ```--no-build``` ```<NoBuild>true</NoBuild> ``` ayar ile birlikte proje dosyanızdaki ayarın eşdeğeri olan dotnet.exe özelliği ' a geçirerek kaçınılabilir ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` .

Bir dosyayı paketetmek için *. csproj* dosyası örneği nuspec :

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

#### `TargetsForTfmSpecificBuildOutput`

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

#### `TargetsForTfmSpecificContentInPackage`

Özel bir hedef yazın ve özelliğin değeri olarak belirtin `$(TargetsForTfmSpecificContentInPackage)` . Pakete dahil edilecek tüm dosyalar için, hedef bu dosyaları ItemGroup 'a yazmalıdır `TfmSpecificPackageFile` ve aşağıdaki isteğe bağlı meta verileri ayarlar:

- `PackagePath`: Dosyanın pakette çıkış olması gereken yol. NuGet aynı paket yoluna birden fazla dosya eklenirse bir uyarı verir.
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
1. MSBuild.Build.Tasks.dll verileri geçirme NuGet
1. Geri yüklemeyi Çalıştır
1. Paketleri İndir
1. Varlıklar dosyası, hedefler ve props yazma

`restore`Hedef, PackageReference biçimini kullanan projeler için geçerlidir.
`MSBuild 16.5+` Ayrıca, biçim için [kabul desteği](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) de vardır `packages.config` .

> [!NOTE]
> `restore`Hedef, hedefle birlikte [çalıştırılmamalıdır](#restoring-and-building-with-one-msbuild-command) `build` .

### <a name="restore-properties"></a>Özellikleri geri yükle

Ek geri yükleme ayarları MSBuild Proje dosyasındaki özelliklerden gelebilir. Değerler, anahtar kullanılarak komut satırından da ayarlanabilir `-p:` (aşağıdaki örneklere bakın).

| Özellik | Açıklama |
|--------|--------|
| `RestoreSources` | Paket kaynaklarının noktalı virgülle ayrılmış listesi. |
| `RestorePackagesPath` | Kullanıcı paketleri klasör yolu. |
| `RestoreDisableParallel` | İndirmeleri tek seferde bir ile sınırlayın. |
| `RestoreConfigFile` | `Nuget.Config`Uygulanacak dosyanın yolu. |
| `RestoreNoCache` | Doğru ise, önbelleğe alınmış paketlerin kullanılmasını önler. Bkz. [genel paketleri ve önbellek klasörlerini yönetme](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| `RestoreIgnoreFailedSources` | Doğru ise, başarısız veya eksik paket kaynaklarını yoksayar. |
| `RestoreFallbackFolders` | Geri dönüş klasörleri, Kullanıcı paketleri klasörüyle aynı şekilde kullanılır. |
| `RestoreAdditionalProjectSources` | Geri yükleme sırasında kullanılacak ek kaynaklar. |
| `RestoreAdditionalProjectFallbackFolders` | Geri yükleme sırasında kullanılacak ek geri dönüş klasörleri. |
| `RestoreAdditionalProjectFallbackFoldersExcludes` | İçinde belirtilen geri dönüş klasörlerini dışlar `RestoreAdditionalProjectFallbackFolders` |
| `RestoreTaskAssemblyFile` | Yolu `NuGet.Build.Tasks.dll` . |
| `RestoreGraphProjectInput` | Geri yüklenecek projelerin, mutlak yollar içermesi gereken, noktalı virgülle ayrılmış listesi. |
| `RestoreUseSkipNonexistentTargets`  | Projeler aracılığıyla toplandığında, MSBuild iyileştirme kullanılarak toplanıp toplanmayacağını belirler `SkipNonexistentTargets` . Ayarlanmazsa, varsayılan olarak olur `true` . Projenin hedefleri içeri aktarılmadığı zaman, sonuç hızlı bir davranıştır. |
| `MSBuildProjectExtensionsPath` | Çıkış klasörü, varsayılan olarak `BaseIntermediateOutputPath` ve `obj` klasörü. |
| `RestoreForce` | PackageReference tabanlı projelerde, son geri yükleme başarılı olsa bile tüm bağımlılıkların çözülmesini zorlar. Bu bayrağın belirtilmesi, dosyanın silinmesine benzer `project.assets.json` . Bu, http-cache ' i atlar. |
| `RestorePackagesWithLockFile` | Bir kilit dosyasının kullanımıyla ilgili olarak. |
| `RestoreLockedMode` | Geri yüklemeyi kilitli modda çalıştırın. Bu, geri yüklemenin bağımlılıkları yeniden değerlendirmeyeceği anlamına gelir. |
| `NuGetLockFilePath` | Kilit dosyası için özel bir konum. Varsayılan konum projenin yanında bulunur ve adlandırılır `packages.lock.json` . |
| `RestoreForceEvaluate` | Bağımlılıkları yeniden hesaplamak ve herhangi bir uyarı olmadan kilit dosyasını güncelleştirmek için geri yüklemeyi zorlar. |
| `RestorePackagesConfig` | packages.config olan projeleri geri yükleyen bir kabul etme anahtarı. Yalnızca ile desteklenir `MSBuild -t:restore` . |
| `RestoreUseStaticGraphEvaluation` | Standart değerlendirme yerine statik grafik değerlendirmesini kullanmak için bir tercih MSBuild edilen anahtar. Statik grafik değerlendirmesi, büyük depolar ve çözümler için önemli ölçüde daha hızlı olan deneysel bir özelliktir. |

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

| Dosya | Description |
|--------|--------|
| `project.assets.json` | Tüm paket başvurularının bağımlılık grafiğini içerir. |
| `{projectName}.projectFileExtension.nuget.g.props` | MSBuildPaketlerde bulunan props 'a başvurular |
| `{projectName}.projectFileExtension.nuget.g.targets` | MSBuildPaketlerde bulunan hedeflere başvurular |

### <a name="restoring-and-building-with-one-msbuild-command"></a>Tek bir komutla geri yükleme ve oluşturma MSBuild

NuGetHedefleri ve props 'ı getiren paketleri geri yükleyen olgu nedeniyle MSBuild , geri yükleme ve derleme değerlendirmeleri farklı genel özelliklerle çalıştırılır.
Bu, aşağıdakilerin öngörülemeyen ve genellikle yanlış bir davranışa sahip olacağı anlamına gelir.

```cli
msbuild -t:restore,build
```

 Bunun yerine önerilen yaklaşım şunlardır:

```cli
msbuild -t:build -restore
```

Aynı Logic şuna benzer diğer hedefler için de geçerlidir `build` .

### <a name="restoring-packagereference-and-packagesconfig-projects-with-msbuild"></a>İle PackageReference ve packages.config projelerini geri yükleme MSBuild

MSBuild16.5 + ile packages.config de desteklenir `msbuild -t:restore` .

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> `packages.config` restore yalnızca ile kullanılabilir `MSBuild 16.5+` ve `dotnet.exe`

### <a name="restoring-with-msbuild-static-graph-evaluation"></a>MSBuildStatik grafik değerlendirmesi ile geri yükleme

> [!NOTE]
> MSBuild16.6 + ile, NuGet büyük depolar için geri yükleme süresini önemli ölçüde artıran komut satırından statik grafik değerlendirmesi kullanmak için deneysel bir özellik eklemiştir.

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
> Visual Studio 2019. x ve NuGet 5. x itibariyle, bu özellik deneysel ve kabul edilmelidir. Bu özelliğin varsayılan olarak etkinleştirileceği hakkında daha fazla bilgi için [ NuGet /Home # 9803](https://github.com/NuGet/Home/issues/9803) izleyin.

Statik grafik geri yükleme, geri yükleme 'nin MSBuild bölümünü, Proje okuma ve değerlendirme, ancak geri yükleme algoritmasını etkilemez! Geri yükleme algoritması tüm NuGet araçlarda ( NuGet . exe, MSBuild . exe, dotnet.exe ve Visual Studio) aynıdır.

Birçok senaryoda, statik grafik geri yükleme geçerli geri yüklemeden farklı davranabilir ve belirtilen bazı Packagereferklu veya ProjectReferences eksik olabilir.

Bir kez göz önünde bulundurmanız için, statik grafik geri yüklemeye geçiş yaparken şunu çalıştırmayı göz önünde bulundurun:

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

NuGet hiçbir *değişiklik raporlanmamalıdır* . Bir tutarsızlık görürseniz, lütfen [ NuGet /Home](https://github.com/nuget/home/issues/new)'ta bir sorun bildirin.

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
