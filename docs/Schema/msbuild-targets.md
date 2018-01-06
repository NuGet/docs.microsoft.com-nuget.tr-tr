---
title: "NuGet paketi ve geri yükleme MSBuild hedefleri olarak | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 4/3/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 86f7e724-2509-4d7d-aa8d-4a3fb913ded6
description: "NuGet paketi ve geri yükleme, doğrudan NuGet 4.0 + ile MSBuild hedefleri olarak çalışabilir."
keywords: "NuGet ve MSBuild, NuGet paketi hedef, NuGet geri yükleme hedefi"
ms.reviewer: karann-msft
ms.openlocfilehash: d4778a21a96de6d76d7a20ff9a305960dd6c2bf1
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>NuGet paketi ve MSBuild hedefleri olarak geri yükleme

*NuGet 4.0 +*

NuGet 4.0 +, bilgileri ile doğrudan çalışabilir bir `.csproj` ayrı bir gerektirmeden dosya `.nuspec` veya `project.json` dosyası. Bu yapılandırma dosyaları daha önce depolanan tüm meta veriler yerine depolanabilir `.csproj` doğrudan, burada açıklandığı gibi dosya.

MSBuild ile 15.1 +, NuGet birinci sınıf MSBuild vatandaşı ile aynı zamanda olan `pack` ve `restore` aşağıda açıklandığı gibi hedefler. Bu hedeflerde, diğer MSBuild görev veya hedef ile olduğu gibi NuGet ile çalışmanıza olanak sağlar. (NuGet için 3.x ve daha önce kullandığınız [paketi](../tools/cli-ref-pack.md) ve [geri](../tools/cli-ref-restore.md) NuGet CLI aracılığıyla yerine komutları.)

Bu konuda:

- [Hedef derleme sırası](#target-build-order)
- [paketi hedef](#pack-target)
- [Paketi senaryoları](#pack-scenarios)
- [geri yükleme hedefi](#restore-target)
- [PackageTargetFallback](#packagetargetfallback)

## <a name="target-build-order"></a>Hedef derleme sırası

Olduğundan `pack` ve `restore` MSBuild hedefleri şunlardır akışınızı artırmak için bunları erişebilirsiniz. Örneğin, paket sonra bir ağ paylaşımına paketinizi kopyalamak istediğiniz varsayalım. Bunu, proje dosyasında aşağıdaki ekleyerek yapabilirsiniz:

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
    <Copy
        SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
        DestinationFolder="\\myshare\packageshare\"
        />
</Target>
```

Benzer şekilde, bir MSBuild görev yazabileceğiniz, kendi hedef yazma ve MSBuild görevi NuGet özelliklerinde kullanabilir.

## <a name="pack-target"></a>paketi hedef

Diğer bir deyişle, paketi hedef kullanırken `msbuild /t:pack`, MSBuild çizer girdilerinden gelen `.csproj` dosya yerine `project.json` veya `.nuspec` dosyaları. Aşağıdaki tabloda eklenebilir MSBuild özellikleri açıklanmaktadır bir `.csproj` ilk dosyasında `<PropertyGroup>` düğümü. Bu düzenlemeler kolayca Visual Studio 2017 ve daha sonra projeye sağ tıklayıp seçerek yapabileceğiniz **{project_name} Düzenle** bağlam menüsünde. Kolaylık olması için tablo eşdeğer özelliği tarafından düzenlenir bir [ `.nuspec` dosya](../schema/nuspec.md).

Unutmayın `Owners` ve `Summary` özelliklerinden `.nuspec` MSBuild ile desteklenmez.


| Öznitelik/NuSpec değeri | MSBuild özelliği | Varsayılan | Notlar |
|--------|--------|--------|--------|
| Kimliği | Paket kimliği | AssemblyName | MSBuild gelen $(AssemblyName) |
| Sürüm | PackageVersion | Sürüm | Bu semver örnek "1.0.0", "1.0.0-beta" veya "1.0.0-beta-00345" için uyumlu değil |
| VersionPrefix | PackageVersionPrefix | empty | PackageVersion ayarı PackageVersionPrefix üzerine yazar |
| VersionSuffix | PackageVersionSuffix | empty | MSBuild gelen $(VersionSuffix). PackageVersion ayarı PackageVersionSuffix üzerine yazar | 
| Yazarlar | Yazarlar | Geçerli kullanıcının kullanıcı adı | |
| Sahipleri | Yok | NuSpec içinde mevcut olmayan | |
| Başlık | Başlık | Paket kimliği| |
| Açıklama | Açıklama | "Paketi" | |
| Telif Hakkı | Telif Hakkı | empty | |
| RequireLicenseAcceptance | PackageRequireLicenseAcceptance | false | |
| licenseUrl | PackageLicenseUrl | empty | |
| projectUrl | PackageProjectUrl | empty | |
| iconUrl | PackageIconUrl | empty | |
| Etiketler | PackageTags | empty | Etiketleri noktalı virgülle ayrılmış olan. |
| ReleaseNotes | PackageReleaseNotes | empty | |
| RepositoryUrl | RepositoryUrl | empty | |
| RepositoryType | RepositoryType | empty | |
| PackageType | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| Özet | Desteklenmez | | |


### <a name="pack-target-inputs"></a>paketi hedef girişleri

- IsPackable
- PackageVersion
- Paket kimliği
- Yazarlar
- Açıklama
- Telif Hakkı
- PackageRequireLicenseAcceptance
- DevelopmentDependency
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

### <a name="packageiconurl"></a>PackageIconUrl

Değişikliğin parçası olarak [NuGet sorunu 2582](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` sonunda değiştirilecek `PackageIconUri` ve sonuçta elde edilen paketin kökünde bulunan bir simge dosyası için göreli bir yol olabilir.

### <a name="output-assemblies"></a>Çıktı derlemeler

`nuget pack`kopya çıktı uzantılara sahip dosyaları `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, ve `.pri`. MSBuild gelen sağladıkları üzerinde kopyalanır ve çıkış dosyalarının bağımlı `BuiltOutputProjectGroup` hedef.

Çıkış derlemelerinin nereye proje dosyası veya komut satırı denetlemek için kullanabileceğiniz iki MSBuild özellikleri şunlardır:

- `IncludeBuildOutput`: Derleme çıktı derlemelerinin pakete dahil edilip edilmeyeceğini belirler bir Boole değeri.
- `BuildOutputTargetFolder`: Çıktı derlemelerinin yerleştirilmelidir klasörü belirtir. Çıktı derlemelerinin (ve diğer çıktı dosyaları) ilgili framework klasörlerine kopyalanır.

### <a name="package-references"></a>Paket referanslarını

Bkz: [paketini proje dosyalarını başvurularında](../consume-packages/package-references-in-project-files.md).

### <a name="project-to-project-references"></a>Proje başvuruları projeye

Proje başvuruları projeye değerlendirilir varsayılan olarak nuget paket referanslarını, örneğin:

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

Ayrıca, aşağıdaki meta verileri, proje başvurusu ekleyebilirsiniz:

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a>Bir paketteki içerik dahil olmak üzere

İçerik eklemek için fazladan meta verileri, mevcut eklemek `<Content>` öğesi. Varsayılan olarak girişlerle geçersiz kılma sürece "İçerik" paketinde türünde her şeyi ister aşağıdakiler:

 ```xml
    <Content Include="..\win7-x64\libuv.txt">
        <Pack>false</Pack>
    </Content>
 ```

Varsayılan olarak, her şeyi köküne eklenen `content` ve `contentFiles\any\<target_framework>` bir paket ve korur klasördeki göreli klasör yapısı, bir paket yolu belirtmediğiniz sürece:

```xml
<Content Include="..\win7-x64\libuv.txt">        
    <Pack>true</Pack>
    <PackagePath>content\myfiles\</PackagePath>
</Content>
```

Yalnızca belirli bir tüm içeriğinizi kopyalamak isterseniz klasörlerde kök (yerine `content` ve `contentFiles` her ikisi de), MSBuild özelliği kullanabilirsiniz `ContentTargetFolders`, varsayılan olarak "içerik; Content dosyaları" ancak başka bir klasör adı için ayarlanabilir. Not "Content dosyaları" belirterek, yalnızca `ContentTargetFolders` altında dosyaları koyan `contentFiles\any\<target_framework>` veya `contentFiles\<language>\<target_framework>` göre `buildAction`.

`PackagePath`hedef yolları noktalı virgülle ayrılmış bir kümesi olabilir. Bir boş paket yolu belirterek dosya paket köküne ekleyin. Örneğin, aşağıdaki ekler `libuv.txt` için `content\myfiles`, `content\samples`ve paket kök:

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

Ayrıca bir MSBuild özelliği olan `$(IncludeContentInPack)`, varsayılan olarak `true`. Bu ayarlanırsa `false` hiçbir projede sonra proje içerikten eklenmemiştir nuget paketi.

Yukarıdaki öğelerin hiçbirinde ayarlayabilirsiniz diğer paketi belirli meta verileri içeren ```<PackageCopyToOutput>``` ve ```<PackageFlatten>``` hangi kümeleri ```CopyToOutput``` ve ```Flatten``` üzerinde değerleri ```contentFiles``` çıkış nuspec girişi.


> [!Note]
> İçerik öğeleri dışında `<Pack>` ve `<PackagePath>` meta verileri de ayarlanabilir derleme, EmbeddedResource, ApplicationDefinition, sayfa, kaynak, KarşılamaEkranı, DesignData, DesignDataWithDesignTimeCreatableTypes, yapı eylemiyle dosyalarda CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource veya yok.
>
> Dosya adı, paket yolu genelleme desenleri kullanırken eklenecek paketi için paket yolu paket yoluyla dosya adını içeren tam yol kabul edilir klasör ayırıcı karakter, aksi takdirde ile bitmesi gerekir.

### <a name="includesymbols"></a>IncludeSymbols

Kullanırken `MSBuild /t:pack /p:IncludeSymbols=true`, karşılık gelen `.pdb` dosyaları, diğer çıkış dosyalarının yanı sıra kopyalanır (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`). Bu ayarı Not `IncludeSymbols=true` normal bir paket oluşturur *ve* simge paketi.

### <a name="includesource"></a>IncludeSource

Bu aynı sonucu verir `IncludeSymbols`ile birlikte kaynak dosyalarını kopyalar dışında `.pdb` da dosyaları. Tüm dosya türlerini `Compile` üzerinden kopyalanır `src\<ProjectName>\` elde edilen paketindeki göreli yol klasör yapısı korunarak. Aynı kaynak dosyaları herhangi da yapılır `ProjectReference` olan `TreatAsPackageReference` kümesine `false`.

Dosya türü derlemek için yeni eklenen sonra proje klasörünün dışında varsa, `src\<ProjectName>\`.

### <a name="istool"></a>IsTool

Kullanırken `MSBuild /t:pack /p:IsTool=true`, tüm dosyaları belirtilen çıktı [çıkış derlemelerinin](#output-assemblies) senaryosu, kopyalanır `tools` klasörü yerine `lib` klasör. Bu farklı olduğuna dikkat edin bir `DotNetCliTool` , belirtilen ayarlayarak `PackageType` içinde `.csproj` dosya.

### <a name="packing-using-a-nuspec"></a>Bir .nuspec kullanarak paketleme

Kullanabileceğiniz bir `.nuspec` içeri aktarmak için bir proje dosyasına sahip olması koşuluyla, projenizin paketi dosyaya `NuGet.Build.Tasks.Pack.targets` böylece paketi görevi çalıştırılabilir. Aşağıdaki üç MSBuild özellikleri kullanarak paket için uygun olan bir `.nuspec`:

1. `NuspecFile`: göreli veya mutlak bir yol `.nuspec` paketleme için kullanılan dosya.
1. `NuspecProperties`: noktalı virgülle ayrılmış listesini anahtar = değer çiftleri. MSBuild komut satırı ayrıştırma works yöntemi nedeniyle birden çok özellikleri şu şekilde belirtilmelidir: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.  
1. `NuspecBasePath`: Temel yolu `.nuspec` dosya.

Kullanıyorsanız `dotnet.exe` projenizi paketi için bir komut aşağıdaki gibi kullanın:

```
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

MSBuild projenizi Paketi kullanıyorsanız, aşağıdaki gibi bir komutu kullanın:

```
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

## <a name="restore-target"></a>geri yükleme hedefi

`MSBuild /t:restore`(hangi `nuget restore` ve `dotnet restore` .NET Core projeleriyle kullanmak), proje dosyasında aşağıdaki gibi başvurduğu paketleri yükler:

1. Tüm proje için proje başvuruları okuma
1. Ara klasörü ve hedef çerçeveleri bulmak için proje özelliklerini okuma
1. Msbuild veri NuGet.Build.Tasks.dll geçirmek
1. Geri yükleme çalıştırma
1. Paketleri indirin
1. Varlıklar dosya, hedefleri ve özellik yazma


### <a name="restore-properties"></a>Özellikler geri yükleme

Ek geri yükleme ayarlarını MSBuild proje dosyası özelliklerinde alınması. Değerleri de ayarlanabilir kullanarak komut satırından `/p:` geçiş (aşağıdaki örneklere bakın).

| Özellik | Açıklama |
|--------|--------|
| RestoreSources | Paket kaynaklarını noktalı virgülle ayrılmış listesi. |
| RestorePackagesPath | Kullanıcı paketleri klasör yolu. |
| RestoreDisableParallel | Bir seferde bir sınır indirir. |
| RestoreConfigFile | Yol için bir `Nuget.Config` uygulamak için dosya. |
| RestoreNoCache | TRUE ise, web önbelleği kullanılarak önler. |
| RestoreIgnoreFailedSources | TRUE ise, başarısız olan veya eksik paket kaynaklarını yok sayar. |
| RestoreTaskAssemblyFile | Yolu `NuGet.Build.Tasks.dll`. |
| RestoreGraphProjectInput | Mutlak yollar içermesi gereken geri yüklemek için projeleri noktalı virgülle ayrılmış listesi. |
| RestoreOutputPath | Çıkış klasörüne varsayarak, `obj` klasörü. |

**Örnekler**

Komut satırı:

```
msbuild /t:restore /p:RestoreConfigFile=<path>
```

Proje dosyası:

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
<PropertyGroup>
```

### <a name="restore-outputs"></a>Çıkış geri yükleme

Geri yükleme yapı aşağıdaki dosyaları oluşturur `obj` klasörü:

| Dosya | Açıklama |
|--------|--------|
| `project.assets.json` | Daha önce`project.lock.json` |
| `{projectName}.projectFileExtension.nuget.g.props` | MSBuild özellik paketlerinde bulunan başvurular |
| `{projectName}.projectFileExtension.nuget.g.targets` | MSBuild hedefleri paketlerinde bulunan başvurular |


### <a name="packagetargetfallback"></a>PackageTargetFallback 

`PackageTargetFallback` Öğesi paketleri geri yüklenirken kullanılacak uyumlu hedefleri kümesi belirtmenize olanak verir (denk [ `imports` içinde `project.json` ](../schema/project-json.md#imports)). Bir dotnet kullanmak paketleri izin vermek için tasarlanmış [TxM](../schema/target-frameworks.md) dotnet TxM bildirmeyin uyumlu paketlerle çalışmak için. Projeniz TxM dotnet kullanıyorsa, eklediğiniz sürece diğer bir deyişle, daha sonra bağlı olduğu gereken üzerinde de tüm paketler dotnet TxM, olması `<PackageTargetFallback>` dotnet ile uyumlu olacak şekilde dotnet olmayan platformları izin vermek üzere projenize. 

Proje kullanıyorsa, örneğin, `netstandard1.6` TxM ve bağımlı paketi içeren yalnızca `lib/net45/a.dll` ve `lib/portable-net45+win81/a.dll`, projeyi oluşturmak başarısız olur. Getirileceğini istediğiniz ikinci DLL'dir sonra ekleyebileceğiniz bir `PackageTargetFallback` gibi söylemek için `portable-net45+win81` DLL uyumludur:

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

Projenizdeki tüm hedefler için bir geri dönüş bildirmek için devre dışı bırakın `Condition` özniteliği. Var olan genişletebilirsiniz `PackageTargetFallback` ekleyerek `$(PackageTargetFallback)` aşağıda gösterildiği gibi:

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```


### <a name="replacing-one-library-from-a-restore-graph"></a>Bir geri yükleme grafik bir kitaplıktan değiştirme

Bir geri yükleme yanlış derleme getiren, paketleri seçim varsayılan ve kendi seçimi ile değiştir dışlamak mümkündür. Üst düzey ile ilk `PackageReference`, tüm varlıklar çıkar:

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
    <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

Ardından, DLL uygun yerel kopyasını kendi başvuru ekleyin:

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
