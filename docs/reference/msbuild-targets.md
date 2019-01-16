---
title: NuGet paketi ve MSBuild hedefleri olarak geri yükleme
description: NuGet paketi ve geri yükleme, MSBuild hedefleri NuGet 4.0 + ile doğrudan olarak çalışabilir.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 8132595cbfaf553736fbcc81aada283a44d6cdbf
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324857"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>NuGet paketi ve MSBuild hedefleri olarak geri yükleme

*NuGet 4.0+*

PackageReference biçimiyle tüm bildirim meta verileri doğrudan içinde bir proje dosyası yerine ayrı bir NuGet 4.0 + depolayabilirsiniz `.nuspec` dosya.

MSBuild ile 15.1 +, NuGet ile birinci sınıf bir MSBuild Vatandaşlık Ayrıca, `pack` ve `restore` aşağıda açıklandığı gibi hedefler. Bu hedefler, başka MSBuild görevi veya hedef ile olduğu gibi NuGet ile çalışmanıza olanak sağlar. (İçin NuGet 3.x ve daha önce kullandığınız [paketi](../tools/cli-ref-pack.md) ve [geri](../tools/cli-ref-restore.md) yerine aracılığıyla NuGet CLI komutları.)

## <a name="target-build-order"></a>Hedef derleme sırası

Çünkü `pack` ve `restore` MSBuild hedefleri olan iş akışınızı geliştirmek için erişebilirsiniz. Örneğin, paketinizin bir ağ paylaşımına paketleme sonra kopyalamak istediğiniz varsayalım. Proje dosyanızda aşağıdaki ekleyerek bunu yapabilirsiniz:

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

Benzer şekilde, bir MSBuild görevi yazabilir, kendi hedefleyin ve MSBuild görevindeki NuGet özelliklerini kullanma.

## <a name="pack-target"></a>paketi hedef

PackageReference biçimini kullanarak, kullanarak .NET Standard projeleri için `msbuild -t:pack` bir NuGet paketi oluşturmak için Proje dosyasındaki girişleri çizer.

Aşağıdaki tabloda, bir proje dosyası birinci içinde eklenebilir MSBuild özellikleri tanımlar `<PropertyGroup>` düğümü. Bu düzenlemeler kolayca Visual Studio 2017'de ve daha sonra projeyi sağ tıklayıp tarafından yapabileceğiniz **{project_name} Düzenle** bağlam menüsünde. Kolaylık olması için tablo eşdeğer özelliği tarafından düzenlenir bir [ `.nuspec` dosya](../reference/nuspec.md).

Unutmayın `Owners` ve `Summary` özelliklerinden `.nuspec` MSBuild ile desteklenmez.

| Öznitelik/NuSpec değeri | MSBuild özelliği | Varsayılan | Notlar |
|--------|--------|--------|--------|
| Kimliği | PackageId | AssemblyName | MSBuild gelen $(AssemblyName) |
| Sürüm | PackageVersion | Sürüm | Bu örnek "1.0.0", "1.0.0-beta" veya "1.0.0-beta-00345" uyumlu semver |
| VersionPrefix | PackageVersionPrefix | empty | PackageVersionPrefix PackageVersion ayarını geçersiz kılar |
| VersionSuffix | PackageVersionSuffix | empty | MSBuild gelen $(VersionSuffix). PackageVersionSuffix PackageVersion ayarını geçersiz kılar |
| Yazarlar | Yazarlar | Geçerli kullanıcının kullanıcı adı | |
| Sahipleri | Yok | Sınıflandırmalarına yok | |
| Başlık | Başlık | PackageId| |
| Açıklama | Açıklama | "Paketi" | |
| Telif Hakkı | Telif Hakkı | empty | |
| RequireLicenseAcceptance | PackageRequireLicenseAcceptance | false | |
| Lisans | PackageLicenseExpression | empty | Karşılık gelen `<license type="expression">` |
| Lisans | PackageLicenseFile | empty | Karşılık gelen `<license type="file">`. Başvurulan lisans dosyasını açıkça paketi gerekebilir. |
| LicenseUrl | PackageLicenseUrl | empty | `licenseUrl` olduğundan kullanımdan kaldırılıyor PackageLicenseExpression veya PackageLicenseFile özelliğini kullanın |
| ProjectUrl | PackageProjectUrl | empty | |
| IconUrl | PackageIconUrl | empty | |
| Etiketler | PackageTags | empty | Etiketleri noktalı virgülle ayrılmış olan. |
| ReleaseNotes | PackageReleaseNotes | empty | |
| Depo/URL'si | RepositoryUrl | empty | Kopyalayın veya kaynak kodu almak için kullanılan depo URL'si. Örnek: *https://github.com/NuGet/NuGet.Client.git* |
| Depo/türü | RepositoryType | empty | Depo türü. Örnekler: *git*, *tfs*. |
| Depo/dal | RepositoryBranch | empty | İsteğe bağlı bir depo dalı bilgileri. *RepositoryUrl* dahil edilmek üzere bu özellik için de belirtilmelidir. Örnek: *ana* (NuGet 4.7.0+) |
| Depo/yürütme | RepositoryCommit | empty | İsteğe bağlı depo işleme veya değişiklik kümesi, paket kaynak belirtmek için karşı hazırlanmıştır. *RepositoryUrl* dahil edilmek üzere bu özellik için de belirtilmelidir. Örnek: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+) |
| PackageType | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| Özet | Desteklenmez | | |

### <a name="pack-target-inputs"></a>paketi hedef girişleri

- IsPackable
- SuppressDependenciesWhenPacking
- PackageVersion
- PackageId
- Yazarlar
- Açıklama
- Telif Hakkı
- PackageRequireLicenseAcceptance
- DevelopmentDependency
- PackageLicenseExpression
- PackageLicenseFile
- PackageLicenseUrl
- PackageProjectUrl
- PackageIconUrl
- PackageReleaseNotes
- PackageTags
- PackageOutputPath
- IncludeSymbols
- IncludeSource
- PackageTypes
- IsTool
- RepositoryUrl
- RepositoryType
- RepositoryBranch
- RepositoryCommit
- NoPackageAnalysis
- MinClientVersion
- IncludeBuildOutput
- IncludeContentInPack
- BuildOutputTargetFolder
- ContentTargetFolders
- NuspecFile
- NuspecBasePath
- NuspecProperties

## <a name="pack-scenarios"></a>Paketi senaryoları

### <a name="suppress-dependencies"></a>Bağımlılıkları gösterme

Paket bağımlılıklarını üretilen NuGet paketinden bastırmak için ayarlanmış `SuppressDependenciesWhenPacking` için `true` olanak tanıyan oluşturulan nupkg dosyasından tüm bağımlılıkları atlanıyor.

### <a name="packageiconurl"></a>PackageIconUrl

Değişikliğin parçası olarak [NuGet sorunu 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` sonunda değiştirilecek `PackageIconUri` ve sonuçta elde edilen paketin kökünde dahil bir simge dosyası için göreli yol olabilir.

### <a name="output-assemblies"></a>Çıkış bütünleştirilmiş kodları

`nuget pack` kopya çıkış uzantılara sahip dosyalar `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, ve `.pri`. Kopyalanan çıkış dosyalarının ne MSBuild sağlıyor üzerinde bağımlı `BuiltOutputProjectGroup` hedef.

Çıkış derlemeleri nereye proje dosyası veya komut satırı denetimi için kullanabileceğiniz iki MSBuild özellikleri vardır:

- `IncludeBuildOutput`: Yapı çıkış derlemeleri pakete dahil edilip edilmeyeceğini belirleyen bir Boole değeri.
- `BuildOutputTargetFolder`: Çıktı derlemelerinin yerleştirilmelidir klasörü belirtir. Çıkış bütünleştirilmiş kodları (ve diğer çıktı dosyalarının) ilgili framework klasörlerine kopyalanır.

### <a name="package-references"></a>Paket başvuruları

Bkz: [paket başvuruları proje dosyalarındaki](../consume-packages/package-references-in-project-files.md).

### <a name="project-to-project-references"></a>Proje Proje başvurular

Proje başvuruları projeye değerlendirilir varsayılan nuget paket başvuruları, örneğin:

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

Ayrıca aşağıdaki meta verileri, proje başvurusu eklenebilir mi:

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a>Bir içerik paketine

İçerik dahil etmek varolan fazladan meta verileri ekleme `<Content>` öğesi. Varsayılan olarak her şeyi girişlerle yazmadığınız sürece "İçerik" paketinde türü ister aşağıdakiler:

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

Varsayılan olarak, her şeyi köküne eklenen `content` ve `contentFiles\any\<target_framework>` klasördeki bir paket ve korur göreli klasör yapısı, bir paket yolu belirtmediğiniz sürece:

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

Klasörleri yalnızca belirli için tüm içeriğinizi kopyalamak istiyorsanız kök (yerine `content` ve `contentFiles` her ikisi de), MSBuild özelliğini kullanabilirsiniz `ContentTargetFolders`, varsayılan olarak "içerik; contentFiles" ancak herhangi bir klasör adı için ayarlanabilir. Not, yalnızca "contentFiles" belirterek `ContentTargetFolders` altındaki dosyaları yerleştirir `contentFiles\any\<target_framework>` veya `contentFiles\<language>\<target_framework>` göre `buildAction`.

`PackagePath` hedef yolları noktalı virgül ile ayrılmış bir dizi olabilir. Bir boş paket yolu belirterek dosya paket köküne eklersiniz. Örneğin, aşağıdaki ekler `libuv.txt` için `content\myfiles`, `content\samples`ve paket kök:

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

Bir MSBuild özelliği de mevcuttur `$(IncludeContentInPack)`, bunun varsayılan `true`. Bu ayarlanırsa `false` hiçbir projede, ardından bu projeye ait içeriği dahil değildir nuget paketinin.

Yukarıdaki öğelerden birini ayarlayabilirsiniz diğer paketi belirli meta veriler içeren ```<PackageCopyToOutput>``` ve ```<PackageFlatten>``` hangi kümeleri ```CopyToOutput``` ve ```Flatten``` üzerinde değerleri ```contentFiles``` çıkış nuspec girişi.

> [!Note]
> İçerik öğeleri dışında `<Pack>` ve `<PackagePath>` meta verileri de ayarlanabilir derleme, EmbeddedResource, ApplicationDefinition, sayfa, kaynak, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes derleme eylemiyle dosyaları , CodeAnalysisDictionary AndroidAsset, AndroidResource, BundleResource veya yok.
>
> Glob desenlerinin kullanırken paket yolunuza dosya eklemek paketi için paket yolu, dosya adı dahil olmak üzere tam yolu kabul edilir klasör ayırıcı karakteri ile aksi takdirde, paket yolu bitmelidir.

### <a name="includesymbols"></a>IncludeSymbols

Kullanırken `MSBuild -t:pack -p:IncludeSymbols=true`, karşılık gelen `.pdb` dosyaların yanı sıra diğer çıktı dosyalarının kopyalandığından (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`). Bu ayarı Not `IncludeSymbols=true` normal bir paket oluşturan *ve* bir sembol paketi.

### <a name="includesource"></a>IncludeSource

Aynı budur `IncludeSymbols`dışında kaynak dosyaları ile birlikte kopyalar `.pdb` dosyalar. Tüm dosya türü `Compile` üzerinden kopyalanır `src\<ProjectName>\` sonuç paketine göreli yol klasör yapısında korur. Aynı kaynak dosyaları herhangi da yapılır `ProjectReference` olduğu `TreatAsPackageReference` kümesine `false`.

Dosya türü ile derleme yaparsanız, proje klasörünün dışında olduğu için yeni eklenen sonra `src\<ProjectName>\`.

### <a name="packing-a-license-expression-or-a-license-file"></a>Bir lisans ifadesi veya bir lisans dosyası

Lisans ifade kullanılırken PackageLicenseExpression özelliği kullanılmalıdır. 
[Lisans ifade örnek](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

[Lisans ifadeleri ve NuGet.org tarafından kabul edilen lisansları hakkında daha fazla bilgi edinin](nuspec.md#license).

Lisans dosyası paketleme, PackageLicenseFile özelliği paket köküne paket yolu belirtmek için kullanmanız gerekir. Ayrıca, dosyanın pakete dahil olduğunu emin olmanız gerekir. Örneğin:

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```
[Lisans dosyası örneği](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).

### <a name="istool"></a>IsTool

Kullanırken `MSBuild -t:pack -p:IsTool=true`, tüm çıktı dosyaları, belirtilen [çıkış derlemeleri](#output-assemblies) senaryosu, kopyalanır `tools` klasörü yerine `lib` klasör. Bu farklı olduğunu unutmayın bir `DotNetCliTool` , belirtilen ayarlayarak `PackageType` içinde `.csproj` dosya.

### <a name="packing-using-a-nuspec"></a>Bir .nuspec kullanarak paketleme

Kullanabileceğiniz bir `.nuspec` projenize SDK proje dosyasını içeri aktarmak için sahip olması koşuluyla paketlemek için dosya `NuGet.Build.Tasks.Pack.targets` böylece paketi görevi yürütülebilir. Yine de soubor nuspec paketi önce projeyi geri yüklemeniz gerekir. Hedef Çerçeve proje dosyasının ilgisizdir ve paket bir nuspec iletişim kurulurken kullanılmaz. Aşağıdaki üç MSBuild özellikleri kullanarak paket için uygun olan bir `.nuspec`:

1. `NuspecFile`: göreli veya mutlak yolunu `.nuspec` paketleme için kullanılan dosya.
1. `NuspecProperties`: noktalı virgülle ayrılmış listesini anahtar = değer çiftleri. MSBuild komut satırı Ayrıştırmada works yöntemi nedeniyle birden çok özellikleri şu şekilde belirtilmelidir: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.  
1. `NuspecBasePath`: Temel yolunu `.nuspec` dosya.

Kullanıyorsanız `dotnet.exe` projenizi paketlemek için aşağıdakine benzer bir komut kullanın:

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

MSBuild proje paketi için kullanılıyorsa, aşağıdakine benzer bir komut kullanın:

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Paket bir nuspec dotnet.exe veya msbuild'ı kullanarak da varsayılan olarak proje oluşturmak için müşteri adayları olduğunu lütfen unutmayın. Bu geçirerek önlenebilir ```--no-build``` ayarı denk olan dotnet.exe özelliğini ```<NoBuild>true</NoBuild> ``` ayarı ile birlikte proje dosyanızda ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` proje dosyasındaki

Soubor nuspec paketlenecek csproj dosyasının bir örnektir:

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

### <a name="advanced-extension-points-to-create-customized-package"></a>Gelişmiş özelleştirilmiş paketi oluşturmak için uzantı noktaları

`pack` Hedef iç, hedef framework belirli derlemede çalıştırılan iki uzantı noktaları sağlar. Belirli içerik hedef framework ve derlemeleri pakete dahil olmak üzere genişletme noktaları destekler:

- `TargetsForTfmSpecificBuildOutput` Hedef: İçindeki dosyaları kullanıma `lib` klasör veya kullanılarak belirtilen bir klasör `BuildOutputTargetFolder`.
- `TargetsForTfmSpecificContentInPackage` Hedef: Dosyaları dışında kullanıma `BuildOutputTargetFolder`.

#### <a name="targetsfortfmspecificbuildoutput"></a>TargetsForTfmSpecificBuildOutput

Özel bir hedefleyin ve değeri olarak belirtin `$(TargetsForTfmSpecificBuildOutput)` özelliği. Gitmesi gereken tüm dosyalara `BuildOutputTargetFolder` (LIB) varsayılan olarak hedef dosyaları ItemGroup yazmanız gerekir `BuildOutputInPackage` aşağıdaki iki meta veri değerleri ayarlayın:

- `FinalOutputPath`: Dosyanın mutlak yolu; sağlanmazsa, kimlik kaynak yolu değerlendirmek için kullanılır.
- `TargetPath`:  (İsteğe bağlı) Dosya içinde bir alt kısımlarda gerektiğinde ayarlamak `lib\<TargetFramework>` derlemeleri ilgili kültür klasörlerine altında ötesine uydu gibi. Varsayılan ayar dosyasının adı.

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

#### <a name="targetsfortfmspecificcontentinpackage"></a>TargetsForTfmSpecificContentInPackage

Özel bir hedefleyin ve değeri olarak belirtin `$(TargetsForTfmSpecificContentInPackage)` özelliği. Tüm dosyalar paket içerisine dâhil etmek, hedef dosyaları ItemGroup yazmanız gerekir `TfmSpecificPackageFile` ve aşağıdaki isteğe bağlı meta verileri ayarlayın:

- `PackagePath`: Yolu, dosya paketinde çıkış burada olmalıdır. Birden fazla dosya aynı paket yolu eklediyseniz NuGet bir uyarı verir.
- `BuildAction`: Paket yolu ise dosyasına atanacak yapı eylemi yalnızca gerekli `contentFiles` klasör. Varsayılan olarak "None".

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

## <a name="restore-target"></a>geri yükleme hedefi

`MSBuild -t:restore` (hangi `nuget restore` ve `dotnet restore` .NET Core projeleriyle kullanın), aşağıdaki gibi proje dosyasında başvurulan paketleri geri yükler:

1. Tüm projeden projeye başvurular okuyun
1. Ara klasörü ve hedef çerçeveleri bulmak için proje özellikleri okuma
1. NuGet.Build.Tasks.dll msbuild veri geçişi
1. Geri yükleme
1. Paketleri indirin
1. Varlıklar dosyasını, hedef ve Özellikler Yaz

`restore` Hedef works **yalnızca** PackageReference biçimini kullanan projeler için. Mevcut **değil** kullanarak projeleri için iş `packages.config` biçimini; kullanma [nuget geri yükleme](../tools/cli-ref-restore.md) yerine.

### <a name="restore-properties"></a>Özellikler geri yükleme

Ek geri yükleme ayarlarını MSBuild proje dosyası özelliklerinde gelir. Değerleri de ayarlanabilir kullanılarak komut satırından `-p:` geçiş (aşağıdaki örneklere bakın).

| Özellik | Açıklama |
|--------|--------|
| RestoreSources | Noktalı virgül ile ayrılmış paket kaynaklarının listesi. |
| RestorePackagesPath | Kullanıcı paketleri klasör yolu. |
| RestoreDisableParallel | Bir kerede sınırı indirir. |
| RestoreConfigFile | Yol için bir `Nuget.Config` uygulamak için dosya. |
| RestoreNoCache | TRUE ise, önbelleğe eklenen paketler kullanılmasını önlemiş olursunuz. Bkz: [genel paketleri ve önbellek klasörlerini yönetme](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| RestoreIgnoreFailedSources | TRUE ise, başarısız veya eksik paket kaynaklarını yok sayar. |
| RestoreTaskAssemblyFile | Yolu `NuGet.Build.Tasks.dll`. |
| RestoreGraphProjectInput | Noktalı virgül ile ayrılmış mutlak yollar içermelidir geri yüklemek için projeler listesi. |
| RestoreOutputPath | Varsayarak, çıkış dosyasının `obj` klasör. |

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

### <a name="restore-outputs"></a>Çıktıları geri yükleme

Geri yükleme, yapı aşağıdaki dosyaları oluşturur `obj` klasörü:

| Dosya | Açıklama |
|--------|--------|
| `project.assets.json` | Tüm paket başvuruları bağımlılık grafiği içerir. |
| `{projectName}.projectFileExtension.nuget.g.props` | MSBuild özellikler paketlerde yer alan başvuruları |
| `{projectName}.projectFileExtension.nuget.g.targets` | MSBuild hedefleri paketlerde yer alan başvuruları |

### <a name="packagetargetfallback"></a>PackageTargetFallback

`PackageTargetFallback` Öğesi, bir dizi paketler geri yüklenirken kullanılacak uyumlu hedefleri belirtmenize olanak sağlar. Bir dotnet kullanan paketleri izin vermek için tasarlanmış [TxM](../reference/target-frameworks.md) bir dotnet TxM bildirmeyin uyumlu paketlerle çalışmak için. Projenizin kullandığı dotnet TxM eklediğiniz sürece diğer bir deyişle, ardından bu bağlıdır üzerinde gerekir ayrıca tüm paketleri bir dotnet TxM, varsa `<PackageTargetFallback>` dotnet ile uyumlu olacak şekilde dotnet olmayan platformlar için projenize.

Örneğin, proje kullanıyorsanız `netstandard1.6` TxM ve bağımlı paketi içeren yalnızca `lib/net45/a.dll` ve `lib/portable-net45+win81/a.dll`, Proje yapı başarısız olur. Almak istediğiniz ikinci alan DLL'dir sonra ekleyebileceğiniz bir `PackageTargetFallback` şu şekilde söylemek `portable-net45+win81` DLL uyumludur:

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

Bir geri dönüş için projenizdeki tüm hedefleri bildirmek üzere bırakın `Condition` özniteliği. Ayrıca var olan tüm genişletebilirsiniz `PackageTargetFallback` ekleyerek `$(PackageTargetFallback)` burada gösterildiği gibi:

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a>Bir geri yükleme grafik bir kitaplıktan değiştirme

Bir geri yükleme, yanlış derleme getiriyor, tutma paketleri istediğiniz varsayılan ve kendi yönteminizi değiştirmek mümkündür. Üst düzey ile ilk `PackageReference`, tüm varlıkları dışla:

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

Ardından, DLL uygun yerel kopyasını kendi başvuru ekleyin:

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
