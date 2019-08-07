---
title: NuGet paketi ve geri yükleme MSBuild hedefleri olarak
description: NuGet paketi ve geri yükleme, NuGet 4.0 + ile doğrudan MSBuild hedefleri olarak çalışabilir.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 8403ae38b5d2e907c6f06b162a18cdcd5425565b
ms.sourcegitcommit: 5aa49478dc466c67db5c3edda7c6ce8dcd8ae033
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2019
ms.locfileid: "68817528"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>NuGet paketi ve geri yükleme MSBuild hedefleri olarak

*NuGet 4.0 +*

[Packagereference](../consume-packages/package-references-in-project-files.md) biçimi sayesinde, NuGet 4.0 + tüm bildirim meta verilerini ayrı `.nuspec` bir dosya kullanmak yerine doğrudan proje dosyası içinde depolayabilirler.

MSBuild 15.1 + ile NuGet, aşağıda açıklandığı gibi, `pack` ve `restore` hedefleri ile birinci sınıf MSBuild vatandaşlık da vardır. Bu hedefler, diğer herhangi bir MSBuild görevi veya hedefi ile yaptığınız gibi NuGet ile çalışmanıza olanak sağlar. MSBuild kullanarak bir NuGet paketi oluşturma yönergeleri için bkz. [MSBuild kullanarak NuGet paketi oluşturma](../create-packages/creating-a-package-msbuild.md). (NuGet 3. x ve öncesi için, bunun yerine NuGet CLı aracılığıyla [paketle](../reference/cli-reference/cli-ref-pack.md) ve [geri yükleme](../reference/cli-reference/cli-ref-restore.md) komutlarını kullanırsınız.)

## <a name="target-build-order"></a>Hedef derleme sırası

`pack` Ve`restore` MSBuild hedefleri olduğundan, iş akışınızı geliştirmek için bunlara erişebilirsiniz. Örneğin, paketledikten sonra paketinizi bir ağ paylaşımında kopyalamak istediğinizi varsayalım. Bunu, proje dosyanıza aşağıdakileri ekleyerek yapabilirsiniz:

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

Benzer şekilde, MSBuild görevinde bir MSBuild görevi yazabilir, kendi hedefini yazabilir ve NuGet özelliklerini kullanabilirsiniz.

## <a name="pack-target"></a>paket hedefi

Packagereference biçimini kullanan .NET Standard projeler için, `msbuild -t:pack` bir NuGet paketi oluştururken kullanılacak proje dosyasından girişler çizer.

Aşağıdaki tabloda, ilk `<PropertyGroup>` düğüm içindeki bir proje dosyasına eklenebilen MSBuild özellikleri açıklanmaktadır. Projeyi sağ tıklayıp bağlam menüsünde **{Project_Name} Düzenle** ' yi seçerek Visual Studio 2017 ve sonraki sürümlerde bu düzenlemeleri kolayca yapabilirsiniz. Kolaylık olması için tablo, bir [ `.nuspec` dosyadaki](../reference/nuspec.md)denk özelliğe göre düzenlenir.

`Owners` Ve özelliklerininMSBuild`.nuspec`iledesteklenmediğiniunutmayın. `Summary`

| Öznitelik/NuSpec değeri | MSBuild özelliği | Varsayılan | Notlar |
|--------|--------|--------|--------|
| Id | PackageId | AssemblyName | MSBuild 'ten $ (AssemblyName) |
| Sürüm | PackageVersion | Sürüm | Bu semver uyumludur, örneğin "1.0.0", "1.0.0-Beta" veya "1.0.0-Beta-00345" |
| VersionPrefix | PackageVersionPrefix | empty | PackageVersion ayarı PackageVersionPrefix üzerine yazıyor |
| VersionSuffix | PackageVersionSuffix | empty | MSBuild 'ten $ (VersionSuffix). PackageVersion ayarı PackageVersionSuffix üzerine yazıyor |
| Yazarlar | Yazarlar | Geçerli kullanıcının Kullanıcı adı | |
| Lere | Yok | NuSpec içinde yok | |
| Başlık | Başlık | PackageID| |
| Açıklama | Açıklama | "Paket açıklaması" | |
| Yaptırımlar | Yaptırımlar | empty | |
| Requirelicensekabulünü | PackageRequireLicenseAcceptance | false | |
| lisan | PackageLicenseExpression | empty | Karşılık gelen`<license type="expression">` |
| lisan | PackageLicenseFile | empty | Öğesine `<license type="file">`karşılık gelir. Başvurulan lisans dosyasını açık bir şekilde paketetmeniz gerekebilir. |
| LicenseUrl | PackageLicenseUrl | empty | `licenseUrl`kullanım dışı bırakılıyor, PackageLicenseExpression veya PackageLicenseFile özelliğini kullanın |
| ProjectUrl | PackageProjectUrl | empty | |
| IconUrl | PackageIconUrl | empty | |
| Etiketler | PackageTags | empty | Etiketler noktalı virgülle ayrılır. |
| Relet 'ler | PackageReleaseNotes | empty | |
| Depo/URL | Depourl 'Si | empty | Kaynak kodu kopyalamak veya almak için kullanılan depo URL 'SI. Örneğinde *https://github.com/NuGet/NuGet.Client.git* |
| Depo/tür | Repositorytype parametrelerinin sağlanması | empty | Depo türü. Örnekler: *Git*, *TFS*. |
| Depo/dal | Depodalı | empty | İsteğe bağlı depo dalı bilgileri. Bu özelliğin dahil olması için aynı zamanda bir *Depo-URL* belirtilmelidir. Örnek: *Master* (NuGet 4.7.0 +) |
| Depo/kayıt | Kayıt yapma | empty | Paketin hangi kaynağa göre oluşturulduğunu göstermek için isteğe bağlı depo kaydı veya değişiklik kümesi. Bu özelliğin dahil olması için aynı zamanda bir *Depo-URL* belirtilmelidir. Örnek: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +) |
| PackageType | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| Özet | Desteklenmez | | |

### <a name="pack-target-inputs"></a>Paket hedef girişleri

- Ispackable
- Suppressbağımlıcıeswhenpaketleme
- PackageVersion
- PackageId
- Yazarlar
- Açıklama
- Yaptırımlar
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
- Includesymbols
- IncludeSource
- PackageTypes
- IsTool
- Depourl 'Si
- Repositorytype parametrelerinin sağlanması
- Depodalı
- Kayıt yapma
- NoPackageAnalysis
- MinClientVersion
- IncludeBuildOutput
- IncludeContentInPack
- BuildOutputTargetFolder
- ContentTargetFolders
- Nusguus dosyası
- Nusgubasepath
- Nus, Properties

## <a name="pack-scenarios"></a>paket senaryoları

### <a name="suppress-dependencies"></a>Bağımlılıkları gösterme

Oluşturulan NuGet paketinden paket bağımlılıklarını bastırmak için, olarak `SuppressDependenciesWhenPacking` `true` ayarlayın ve oluşturulan nupkg dosyasından tüm bağımlılıkların atlanmasını sağlar.

### <a name="packageiconurl"></a>PackageIconUrl

[NuGet sorunu 352](https://github.com/NuGet/Home/issues/352)değişikliğinin bir parçası olarak, `PackageIconUrl` sonunda olarak `PackageIconUri` değiştirilir ve sonuç paketinin köküne dahil edilecek bir simge dosyasının göreli yolu olabilir.

### <a name="output-assemblies"></a>Çıkış derlemeleri

`nuget pack`çıktı dosyalarını,,, `.exe`, `.dll`ve `.xml` `.winmd` uzantılarınakopyalar`.json`. `.pri` Kopyalanan çıkış dosyaları, `BuiltOutputProjectGroup` hedef tarafından MSBuild 'in sağladığı şuna bağlıdır.

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

İçerik eklemek için var olan `<Content>` öğeye ek meta veriler ekleyin. Varsayılan olarak, aşağıdaki gibi girdilerle geçersiz kılmadığınız müddetçe "Içerik" türünde her şey pakete dahil edilir:

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

Varsayılan olarak, her şey bir paket içindeki `content` ve `contentFiles\any\<target_framework>` klasörünün köküne eklenir ve bir paket yolu belirtmediğiniz takdirde göreli klasör yapısını korur:

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

Tüm içeriğinizi yalnızca belirli bir kök klasöre ( `content` ve `contentFiles` her ikisi yerine) kopyalamak istiyorsanız, varsayılan olarak "Content; ContentFiles" olan, ancak başka bir klasör `ContentTargetFolders`adına ayarlanabilir MSBuild özelliğini kullanabilirsiniz. Yalnızca dosyaları ' ın `ContentTargetFolders` altında veya `contentFiles\<language>\<target_framework>` temel alarak `buildAction`"ContentFiles" `contentFiles\any\<target_framework>` seçeneğinin belirtildiğine unutmayın.

`PackagePath`noktalı virgülle ayrılmış bir hedef yolları kümesi olabilir. Boş bir paket yolu belirtilmesi, dosyayı paketin köküne ekler. Örneğin, aşağıdaki, ve paket `libuv.txt` köküne `content\myfiles`ekler `content\samples`:

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

Ayrıca, varsayılan olarak `$(IncludeContentInPack)` `true`olan MSBuild özelliği de vardır. Bu, herhangi bir projede `false` olarak ayarlandıysa, bu projeden içerik NuGet paketine dahil edilmez.

Yukarıdaki öğelerin herhangi birine ayarlayabileceğiniz diğer paketine özgü meta veriler içerir ```<PackageCopyToOutput>``` ve ```<PackageFlatten>``` çıkış nuspec içindeki ```contentFiles``` giriş ```CopyToOutput``` üzerinde ```Flatten``` ve değerlerini belirler.

> [!Note]
> İçerik öğelerinden ayrı olarak `<Pack>` , ve `<PackagePath>` meta veriler de derleme, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, designdata, designdatawithdesigntimecreateabletypes derleme eylemine sahip dosyalarda ayarlanabilir , CodeAnalysisDictionary, AndroidAsset, AndroidResource, paketleme Leresource veya None.
>
> Glob desenleri kullanılırken dosya adını paket yolunuza eklemek için paket yolu, klasör ayırıcı karakteriyle bitmelidir; Aksi takdirde, paket yolu dosya adı dahil tam yol olarak değerlendirilir.

### <a name="includesymbols"></a>Includesymbols

`MSBuild -t:pack -p:IncludeSymbols=true`Kullanırken, karşılık gelen`.dll` `.winmd` `.pri` dosyalardiğer`.json`çıkış dosyalarıylabirlikte`.exe`kopyalanır (,,, ,,).`.xml` `.pdb` Ayarın `IncludeSymbols=true` düzenli bir paket *ve* bir semboller paketi oluşturduğunu unutmayın.

### <a name="includesource"></a>IncludeSource

Bu, ile `IncludeSymbols` `.pdb` aynıdır, ancak kaynak dosyalarını da dosyalarla birlikte kopyalar. Tüm dosya türleri `Compile` , elde edilen paketteki göreli `src\<ProjectName>\` yol klasörü yapısını korumak için üzerine kopyalanır. Aynı zamanda, olarak `ProjectReference` `TreatAsPackageReference` `false`ayarlanmış herhangi bir kaynak dosyası için de aynı olur.

Derleme türü bir dosya proje klasörünün dışında ise, ' ye `src\<ProjectName>\`eklenmiştir.

### <a name="packing-a-license-expression-or-a-license-file"></a>Lisans ifadesi veya lisans dosyası paketleme

Bir lisans ifadesi kullanılırken PackageLicenseExpression özelliğinin kullanılması gerekir. 
[Lisans ifadesi örneği](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

[NuGet.org tarafından kabul edilen lisans ifadeleri ve lisanslar hakkında daha fazla bilgi edinin](nuspec.md#license).

Bir lisans dosyası paketleme sırasında, paketin köküne göre paket yolunu belirtmek için PackageLicenseFile özelliğini kullanmanız gerekir. Ayrıca, dosyanın pakete eklendiğinden emin olmanız gerekir. Örneğin:

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

Kullanırken `MSBuild -t:pack -p:IsTool=true`, [Çıkış derlemeleri](#output-assemblies) senaryosunda belirtilen tüm çıkış dosyaları, `tools` `lib` klasörü yerine klasörüne kopyalanır. Bunun, `DotNetCliTool` `PackageType` içindeki dosyasınıayarlayarakbelirtilenöğesindenfarklıolduğunuunutmayın.`.csproj`

### <a name="packing-using-a-nuspec"></a>. Nuspec kullanarak paketleme

Bunun yerine genellikle `.nuspec` proje dosyasındaki dosyada bulunan [tüm özellikleri eklemeniz](../reference/msbuild-targets.md#pack-target) önerilse de, projenizi paketlebilmeniz için bir `.nuspec` dosya kullanmayı seçebilirsiniz. Tarafından kullanılan `PackageReference`SDK olmayan bir proje için, paket görevinin yürütülebilmesi için içeri aktarmanız `NuGet.Build.Tasks.Pack.targets` gerekir. Bir nuspec dosyası paketetmeden önce projeyi geri yüklemeniz gerekir. (SDK stili bir proje varsayılan olarak paket hedeflerini içerir.)

Proje dosyasının hedef çerçevesi ilgisizdir ve bir nuspec paketleme sırasında kullanılmaz. Aşağıdaki üç MSBuild özelliği, ile `.nuspec`paketleme ile ilgilidir:

1. `NuspecFile`: paketleme için kullanılan `.nuspec` dosyanın göreli veya mutlak yolu.
1. `NuspecProperties`: Key = değer çiftleri için noktalı virgülle ayrılmış bir liste. MSBuild komut satırı ayrıştırması çalışma yöntemi nedeniyle, birden çok özellik şu şekilde belirtilmelidir: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.  
1. `NuspecBasePath`: `.nuspec` Dosya için temel yol.

Projenizi paketmek için kullanıyorsanız `dotnet.exe` , aşağıdaki gibi bir komut kullanın:

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Projenizi paketmek için MSBuild kullanıyorsanız, aşağıdaki gibi bir komut kullanın:

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Lütfen DotNet. exe veya MSBuild kullanarak bir nuspec paketleme, projenin varsayılan olarak oluşturulmasına da neden olduğunu unutmayın. Bu, proje dosyasında ayarı ```--no-build``` ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` ile birlikte proje dosyanızdaki ayarın ```<NoBuild>true</NoBuild> ``` eşdeğeri olan DotNet. exe ' ye geçirilerek kaçınılabilir.

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

`pack` Hedef, iç, hedef çerçeveye özgü derlemede çalışan iki uzantı noktası sağlar. Uzantı noktaları, hedef çerçeveye özgü içerik ve derlemelerin bir pakete dahil edilmesi için destek:

- `TargetsForTfmSpecificBuildOutput`hedef `lib` Klasörü veya kullanılarak `BuildOutputTargetFolder`belirtilen bir klasörü içindeki dosyalar için kullanın.
- `TargetsForTfmSpecificContentInPackage`hedef Dışındaki dosyalar için kullanın `BuildOutputTargetFolder`.

#### <a name="targetsfortfmspecificbuildoutput"></a>TargetsForTfmSpecificBuildOutput

Özel bir hedef yazın ve `$(TargetsForTfmSpecificBuildOutput)` özelliğin değeri olarak belirtin. `BuildOutputTargetFolder` (Varsayılan olarak LIB) öğesine gitmesi gereken tüm dosyalar için, hedef bu dosyaları ItemGroup `BuildOutputInPackage` 'a yazmalıdır ve aşağıdaki iki meta veri değerini ayarlamış olmalıdır:

- `FinalOutputPath`: Dosyanın mutlak yolu; sağlanmazsa, kimlik kaynak yolunu değerlendirmek için kullanılır.
- `TargetPath`:  Seçim Dosyanın içinde `lib\<TargetFramework>` , ilgili kültür klasörlerinin altında yer alan uydu derlemeleri gibi bir alt klasöre gitmesi gerektiğinde ayarlanır. Varsayılan olarak dosyanın adıdır.

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

Özel bir hedef yazın ve `$(TargetsForTfmSpecificContentInPackage)` özelliğin değeri olarak belirtin. Pakete dahil edilecek tüm dosyalar için, hedef bu dosyaları ItemGroup `TfmSpecificPackageFile` 'a yazmalıdır ve aşağıdaki isteğe bağlı meta verileri ayarlar:

- `PackagePath`: Dosyanın pakette çıkış olması gereken yol. Aynı paket yoluna birden fazla dosya eklenirse NuGet bir uyarı verir.
- `BuildAction`: Dosyaya atanacak derleme eylemi, yalnızca paket yolu `contentFiles` klasörsaise gereklidir. Varsayılan "none" olarak belirlenmiştir.

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

`MSBuild -t:restore`(.NETCoreprojeleriylebirliktekullanılması),projedosyasındabaşvurulanpaketleriaşağıdakişekildegeriyükler:`nuget restore` `dotnet restore`

1. Proje başvurularına tüm projeyi oku
1. Ara klasörünü ve hedef çerçeveleri bulmak için proje özelliklerini okuyun
1. MSBuild verilerini NuGet. Build. Tasks. dll dosyasına geçir
1. Geri yüklemeyi Çalıştır
1. Paketleri İndir
1. Varlıklar dosyası, hedefler ve props yazma

Hedef yalnızca packagereference biçimini kullanan projeler için kullanılabilir. `restore` Bu, `packages.config` biçimi kullanan projeler için çalışmaz; bunun yerine [NuGet geri yüklemeyi](../reference/cli-reference/cli-ref-restore.md) kullanın.

### <a name="restore-properties"></a>Özellikleri geri yükle

Ek geri yükleme ayarları proje dosyasındaki MSBuild özelliklerinden gelebilir. Değerler, `-p:` anahtar kullanılarak komut satırından da ayarlanabilir (aşağıdaki örneklere bakın).

| Özellik | Açıklama |
|--------|--------|
| RestoreSources | Paket kaynaklarının noktalı virgülle ayrılmış listesi. |
| RestorePackagesPath | Kullanıcı paketleri klasör yolu. |
| RestoreDisableParallel | İndirmeleri tek seferde bir ile sınırlayın. |
| RestoreConfigFile | `Nuget.Config` Uygulanacak dosyanın yolu. |
| RestoreNoCache | Doğru ise, önbelleğe alınmış paketlerin kullanılmasını önler. Bkz. [genel paketleri ve önbellek klasörlerini yönetme](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| RestoreIgnoreFailedSources | Doğru ise, başarısız veya eksik paket kaynaklarını yoksayar. |
| RestoreFallbackFolders | Geri dönüş klasörleri, Kullanıcı paketleri klasörüyle aynı şekilde kullanılır. |
| Restoreaddıtionalprojectsources | Geri yükleme sırasında kullanılacak ek kaynaklar. |
| Restoreaddıtionalprojectfallbackfolders | Geri yükleme sırasında kullanılacak ek geri dönüş klasörleri. |
| RestoreAdditionalProjectFallbackFoldersExcludes | İçinde belirtilen geri dönüş klasörlerini dışlar`RestoreAdditionalProjectFallbackFolders` |
| RestoreTaskAssemblyFile | `NuGet.Build.Tasks.dll`Yolu. |
| RestoreGraphProjectInput | Geri yüklenecek projelerin, mutlak yollar içermesi gereken, noktalı virgülle ayrılmış listesi. |
| Restoreuseskipnontenttargets  | Projeler MSBuild aracılığıyla toplandığında, `SkipNonexistentTargets` iyileştirme kullanılarak toplanıp toplanmayacağını belirler. Ayarlanmazsa, varsayılan olarak `true`olur. Projenin hedefleri içeri aktarılmadığı zaman, sonuç hızlı bir davranıştır. |
| Msbuildprojeclarsionspath | Çıkış klasörü, varsayılan olarak `BaseIntermediateOutputPath` `obj` ve klasörü. |

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

Restore derleme `obj` klasöründe aşağıdaki dosyaları oluşturur:

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

Aynı Logic şuna benzer `build`diğer hedefler için de geçerlidir.

### <a name="packagetargetfallback"></a>PackageTargetFallback

Öğesi `PackageTargetFallback` , paketler geri yüklenirken kullanılacak bir dizi uyumlu hedef belirtmenize olanak tanır. DotNet [TXD](../reference/target-frameworks.md) kullanan paketlere, DotNet TXD bildirmeyin uyumlu paketlerle çalışmak üzere tasarlanmıştır. Diğer bir deyişle, projeniz DotNet TXI kullanıyorsa, bu durumda, `<PackageTargetFallback>` DotNet olmayan platformların DotNet ile uyumlu olmasını sağlamak için projeye eklemediğiniz sürece bağımlı olduğu tüm paketler DotNet TXD olmalıdır.

Örneğin, proje `netstandard1.6` TXI kullanıyorsa ve bağımlı bir paket yalnızca `lib/net45/a.dll` ve `lib/portable-net45+win81/a.dll`içeriyorsa, proje derlenmeyecektir. İçine getirmek istediğiniz değer ikinci dll ise, `PackageTargetFallback` `portable-net45+win81` dll 'nin uyumlu olduğunu söylemek için aşağıdaki gibi bir ekleyebilirsiniz:

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

Projenizdeki tüm hedeflere yönelik bir geri dönüş bildirmek için, `Condition` özniteliği devre dışı bırakın. Ayrıca, burada gösterildiği `PackageTargetFallback` `$(PackageTargetFallback)` gibi, var olan varsa de genişletebilirsiniz:

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a>Bir geri yükleme grafiğinden bir kitaplığı değiştirme

Geri yükleme yanlış derlemeyi alıyorsa, bu paketlerin varsayılan seçeneğini hariç tutabilir ve kendi seçimiyle değiştirin. Birincisi, en üst düzeyle `PackageReference`, tüm varlıkları hariç tut:

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

Ardından, DLL 'nin uygun yerel kopyasına kendi başvurunuz ekleyin:

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
