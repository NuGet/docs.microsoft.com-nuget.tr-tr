---
title: NuGet paketi ve geri yükleme MSBuild hedefleri olarak
description: NuGet paketi ve geri yükleme, NuGet 4.0 + ile doğrudan MSBuild hedefleri olarak çalışabilir.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 3093761bda456ff5463f708c4d2d12f606dcecbd
ms.sourcegitcommit: 7dba5be7b983ff508834c60caaa8b504f5fa1ae8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72393009"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>NuGet paketi ve geri yükleme MSBuild hedefleri olarak

*NuGet 4.0 +*

[Packagereference](../consume-packages/package-references-in-project-files.md) biçimi sayesinde, NuGet 4.0 + tüm bildirim meta verilerini ayrı bir `.nuspec` dosyası kullanmak yerine doğrudan proje dosyası içinde depolayabilirler.

MSBuild 15.1 + ile NuGet, aşağıda açıklandığı gibi `pack` ve `restore` hedeflerine sahip birinci sınıf MSBuild vatandaşlık. Bu hedefler, diğer herhangi bir MSBuild görevi veya hedefi ile yaptığınız gibi NuGet ile çalışmanıza olanak sağlar. MSBuild kullanarak bir NuGet paketi oluşturma yönergeleri için bkz. [MSBuild kullanarak NuGet paketi oluşturma](../create-packages/creating-a-package-msbuild.md). (NuGet 3. x ve öncesi için, bunun yerine NuGet CLı aracılığıyla [paketle](../reference/cli-reference/cli-ref-pack.md) ve [geri yükleme](../reference/cli-reference/cli-ref-restore.md) komutlarını kullanırsınız.)

## <a name="target-build-order"></a>Hedef derleme sırası

@No__t-0 ve `restore` MSBuild hedefleri olduğundan, iş akışınızı geliştirmek için bunlara erişebilirsiniz. Örneğin, paketledikten sonra paketinizi bir ağ paylaşımında kopyalamak istediğinizi varsayalım. Bunu, proje dosyanıza aşağıdakileri ekleyerek yapabilirsiniz:

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

.NET Standard projeler için, `msbuild -t:pack` ' ı kullanarak, bir NuGet paketi oluştururken kullanılacak proje dosyasından girişler çizer.

Aşağıdaki tabloda, ilk `<PropertyGroup>` düğümü içindeki bir proje dosyasına eklenebilen MSBuild özellikleri açıklanmaktadır. Projeyi sağ tıklayıp bağlam menüsünde **{Project_Name} Düzenle** ' yi seçerek Visual Studio 2017 ve sonraki sürümlerde bu düzenlemeleri kolayca yapabilirsiniz. Kolaylık sağlaması için tablo, [`.nuspec` dosyasındaki](../reference/nuspec.md)denk özelliğe göre düzenlenir.

@No__t-2 ' den `Owners` ve `Summary` özelliklerinin MSBuild ile desteklenmediğini unutmayın.

| Öznitelik/NuSpec değeri | MSBuild özelliği | Varsayılan | Notlar |
|--------|--------|--------|--------|
| Numarasını | PackageID | AssemblyName | MSBuild 'ten $ (AssemblyName) |
| Version | PackageVersion | Version | Bu semver uyumludur, örneğin "1.0.0", "1.0.0-Beta" veya "1.0.0-Beta-00345" |
| VersionPrefix | PackageVersionPrefix | empty | PackageVersion ayarı PackageVersionPrefix üzerine yazıyor |
| VersionSuffix | PackageVersionSuffix | empty | MSBuild 'ten $ (VersionSuffix). PackageVersion ayarı PackageVersionSuffix üzerine yazıyor |
| Yazarlar | Yazarlar | Geçerli kullanıcının Kullanıcı adı | |
| lere | Yok | NuSpec içinde yok | |
| Başlık | Başlık | PackageID| |
| Açıklama | Açıklama | "Paket açıklaması" | |
| yaptırımlar | yaptırımlar | empty | |
| Requirelicensekabulünü | Packagerequirelicensekabulünü | false | |
| lisan | PackageLicenseExpression | empty | @No__t karşılık gelir-0 |
| lisan | PackageLicenseFile | empty | @No__t-0 ' a karşılık gelir. Başvurulan lisans dosyasını açık bir şekilde paketetmeniz gerekebilir. |
| licenseUrl | PackageLicenseUrl 'Si | empty | `PackageLicenseUrl` kullanım dışıdır, PackageLicenseExpression veya PackageLicenseFile özelliğini kullanın |
| projectUrl | PackageProjectUrl | empty | |
| Simge | Packageıcon | empty | Başvurulan simge görüntü dosyasını açıkça paketetmeniz gerekebilir.|
| Iurl | PackageIconUrl 'Si | empty | `PackageIconUrl` kullanım dışıdır, Packageıcon özelliğini kullanın |
| Etiketler | PackageTags | empty | Etiketler noktalı virgülle ayrılır. |
| relet 'ler | PackageReleaseNotes | empty | |
| Depo/URL | Depourl 'Si | empty | Kaynak kodu kopyalamak veya almak için kullanılan depo URL 'SI. Örnek: *https://github.com/NuGet/NuGet.Client.git* |
| Depo/tür | Repositorytype parametrelerinin sağlanması | empty | Depo türü. Örnekler: *Git*, *TFS*. |
| Depo/dal | Depodalı | empty | İsteğe bağlı depo dalı bilgileri. Bu özelliğin dahil olması için aynı zamanda bir *Depo-URL* belirtilmelidir. Örnek: *Master* (NuGet 4.7.0 +) |
| Depo/kayıt | Kayıt yapma | empty | Paketin hangi kaynağa göre oluşturulduğunu göstermek için isteğe bağlı depo kaydı veya değişiklik kümesi. Bu özelliğin dahil olması için aynı zamanda bir *Depo-URL* belirtilmelidir. Örnek: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +) |
| PackageType | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| Özet | Desteklenmez | | |

### <a name="pack-target-inputs"></a>Paket hedef girişleri

- Ispackable
- Suppressbağımlıcıeswhenpaketleme
- PackageVersion
- PackageID
- Yazarlar
- Açıklama
- yaptırımlar
- Packagerequirelicensekabulünü
- developmentDependency
- PackageLicenseExpression
- PackageLicenseFile
- PackageLicenseUrl 'Si
- PackageProjectUrl
- PackageIconUrl 'Si
- PackageReleaseNotes
- PackageTags
- PackageOutputPath
- Includesymbols
- Includesource
- packageTypes
- IsTool
- Depourl 'Si
- Repositorytype parametrelerinin sağlanması
- Depodalı
- Kayıt yapma
- NoPackageAnalysis
- MinClientVersion
- IncludeBuildOutput
- Includecontentınpack
- BuildOutputTargetFolder
- ContentTargetFolders
- Nusguus dosyası
- Nusgubasepath
- Nus, Properties

## <a name="pack-scenarios"></a>paket senaryoları

### <a name="suppress-dependencies"></a>Bağımlılıkları gösterme

Oluşturulan NuGet paketinden paket bağımlılıklarını bastırmak için `SuppressDependenciesWhenPacking` ' ı `true` olarak ayarlayın. Bu, oluşturulan nupkg dosyasından tüm bağımlılıkların atlanmasını sağlar.

### <a name="packageiconurl"></a>PackageIconUrl 'Si

> [!Important]
> PackageIconUrl, NuGet 5.3 + & Visual Studio 2019 Version 16.3 + ile kullanım dışıdır. Bunun yerine [Packageıcon](#packing-an-icon-image-file) kullanın.

### <a name="packing-an-icon-image-file"></a>Simge görüntüsü dosyası paketleme

Bir simge resim dosyası paketleme sırasında, paketin köküne göre paket yolunu belirtmek için Packageıcon özelliğini kullanmanız gerekir. Ayrıca, dosyanın pakete eklendiğinden emin olmanız gerekir. Görüntü dosyası boyutu 1 MB ile sınırlıdır. Desteklenen dosya biçimleri JPEG ve PNG içerir. 64x64 görüntü çözünürlüğü önerilir.

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

`nuget pack`, `.exe`, `.dll`, `.xml`, `.winmd`, `.json` ve `.pri` uzantılarına sahip çıktı dosyalarını kopyalar. Kopyalanan çıkış dosyaları, `BuiltOutputProjectGroup` hedeften MSBuild 'in sağladığı öğesine bağlıdır.

Çıktı derlemelerinin nerede olduğunu denetlemek için, proje dosyanızda veya komut satırında kullanabileceğiniz iki MSBuild özelliği vardır:

- `IncludeBuildOutput`: derleme çıkış derlemelerinin pakete dahil edilip edilmeyeceğini belirleyen bir Boole değeri.
- `BuildOutputTargetFolder`: çıkış derlemelerinin yerleştirilmesi gereken klasörü belirtir. Çıkış derlemeleri (ve diğer çıkış dosyaları) ilgili çerçeve klasörlerine kopyalanır.

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

İçerik eklemek için var olan `<Content>` öğesine ek meta veriler ekleyin. Varsayılan olarak, aşağıdaki gibi girdilerle geçersiz kılmadığınız müddetçe "Içerik" türünde her şey pakete dahil edilir:

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

Varsayılan olarak, her şey bir paket içinde `content` ve `contentFiles\any\<target_framework>` klasörünün köküne eklenir ve bir paket yolu belirtmediğiniz takdirde göreli klasör yapısını korur:

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

Tüm içeriğinizi yalnızca belirli bir kök klasöre (`content` ve `contentFiles` yerine) kopyalamak istiyorsanız, "Content; contentFiles" varsayılan olan ancak başka bir klasör adı olarak ayarlanabilir olan `ContentTargetFolders` MSBuild özelliğini kullanabilirsiniz. Yalnızca `ContentTargetFolders` ' daki "contentFiles" belirtildiğinde dosyaları `contentFiles\any\<target_framework>` veya `contentFiles\<language>\<target_framework>` ' ye `buildAction` ' ü temel alarak koyar.

`PackagePath`, noktalı virgülle ayrılmış bir hedef yolları kümesi olabilir. Boş bir paket yolu belirtilmesi, dosyayı paketin köküne ekler. Örneğin, aşağıdaki `libuv.txt` `content\myfiles`, `content\samples` ve paket köküne ekler:

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

Ayrıca, `true` ' i varsayılan olan-0 @no__t bir MSBuild özelliği de vardır. Bu, herhangi bir projede `false` olarak ayarlandıysa, söz konusu projeden içerik NuGet paketine dahil edilmez.

Yukarıdaki öğelerin hiçbirinde ayarlayabileceğiniz diğer paketine özgü meta veriler ```<PackageCopyToOutput>``` ve ```<PackageFlatten>``` ' i içerir. Bu, çıktı nuspec içindeki ```contentFiles``` girişinde ```CopyToOutput``` ve ```Flatten``` değerlerini ayarlar.

> [!Note]
> Içerik öğelerinden ayrı olarak, `<Pack>` ve `<PackagePath>` meta verileri de derleme, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes oluşturma eylemi olan dosyalarda ayarlanabilir. CodeAnalysisDictionary, AndroidAsset, AndroidResource, paketleme Leresource veya None.
>
> Glob desenleri kullanılırken dosya adını paket yolunuza eklemek için paket yolu, klasör ayırıcı karakteriyle bitmelidir; Aksi takdirde, paket yolu dosya adı dahil tam yol olarak değerlendirilir.

### <a name="includesymbols"></a>Includesymbols

@No__t-0 kullanılırken, karşılık gelen `.pdb` dosyaları diğer çıkış dosyalarıyla birlikte kopyalanır (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`). @No__t-0 ayarının normal bir paket *ve* bir semboller paketi oluşturduğunu unutmayın.

### <a name="includesource"></a>Includesource

Bu `IncludeSymbols` ile aynıdır, ancak kaynak dosyalarını ve `.pdb` dosyalarla birlikte kopyalar. @No__t-0 türündeki tüm dosyalar, elde edilen paketteki göreli yol klasörü yapısını koruyarak `src\<ProjectName>\` ' e kopyalanır. Aynı zamanda, `TreatAsPackageReference` ' in `false` ' ye ayarlandığı `ProjectReference` ' ın kaynak dosyaları için de aynı olur.

Derleme türünde bir dosya proje klasörünün dışındaysa, `src\<ProjectName>\` ' a eklenir.

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

@No__t-0 kullanılırken, [Çıkış derlemeleri](#output-assemblies) senaryosunda belirtilen tüm çıkış dosyaları `lib` klasörü yerine `tools` klasörüne kopyalanır. Bu, `.csproj` dosyasında `PackageType` ayarlanarak belirtilen `DotNetCliTool` ' dan farklı olduğunu unutmayın.

### <a name="packing-using-a-nuspec"></a>. Nuspec kullanarak paketleme

Bunun yerine, genellikle proje dosyasındaki `.nuspec` dosyasında bulunan [tüm özellikleri eklemeniz](../reference/msbuild-targets.md#pack-target) önerilir, ancak projenizi paketetmek için bir `.nuspec` dosyası kullanmayı tercih edebilirsiniz. @No__t-0 kullanan SDK olmayan bir proje için, paket görevinin yürütülebilmesi için `NuGet.Build.Tasks.Pack.targets` ' i içeri aktarmanız gerekir. Bir nuspec dosyası paketetmeden önce projeyi geri yüklemeniz gerekir. (SDK stili bir proje varsayılan olarak paket hedeflerini içerir.)

Proje dosyasının hedef çerçevesi ilgisizdir ve bir nuspec paketleme sırasında kullanılmaz. Aşağıdaki üç MSBuild özelliği @no__t ile paketleme ile ilgilidir: 0:

1. `NuspecFile`: paketleme için kullanılan `.nuspec` dosyasının göreli veya mutlak yolu.
1. `NuspecProperties`: anahtar = değer çiftleri için noktalı virgülle ayrılmış bir liste. MSBuild komut satırı ayrıştırması çalışma yöntemi nedeniyle, birden çok özellik şu şekilde belirtilmelidir: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.  
1. `NuspecBasePath`: `.nuspec` dosyasının temel yolu.

Projenizi paketmek için `dotnet.exe` kullanıyorsanız, aşağıdaki gibi bir komut kullanın:

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Projenizi paketmek için MSBuild kullanıyorsanız, aşağıdaki gibi bir komut kullanın:

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Lütfen DotNet. exe veya MSBuild kullanarak bir nuspec paketleme, projenin varsayılan olarak oluşturulmasına da neden olduğunu unutmayın. Bu, proje dosyasında ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` ayarıyla birlikte ```--no-build``` özelliği DotNet. exe @no__t ' ye geçirilerek kaçınılmaz.

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

@No__t-0 hedefi, iç, hedef çerçeveye özgü derlemede çalışan iki uzantı noktası sağlar. Uzantı noktaları, hedef çerçeveye özgü içerik ve derlemelerin bir pakete dahil edilmesi için destek:

- `TargetsForTfmSpecificBuildOutput` hedefi: `lib` klasörünün içindeki dosyalar veya `BuildOutputTargetFolder` kullanılarak belirtilen bir klasör için kullanın.
- `TargetsForTfmSpecificContentInPackage` hedefi: `BuildOutputTargetFolder` dışındaki dosyalar için kullanın.

#### <a name="targetsfortfmspecificbuildoutput"></a>TargetsForTfmSpecificBuildOutput

Özel bir hedef yazın ve `$(TargetsForTfmSpecificBuildOutput)` özelliğinin değeri olarak belirtin. @No__t-0 ' a (varsayılan olarak lib) gitmesi gereken tüm dosyalar için, hedef bu dosyaları ItemGroup `BuildOutputInPackage` ' e yazmalıdır ve aşağıdaki iki meta veri değerini ayarlamış olmalıdır:

- `FinalOutputPath`: dosyanın mutlak yolu; sağlanmazsa, kimlik kaynak yolunu değerlendirmek için kullanılır.
- `TargetPath`: (Isteğe bağlı) dosyanın, ilgili kültür klasörlerinin altında yer alan uydu derlemeleri gibi `lib\<TargetFramework>` içindeki bir alt klasöre gitmesi gerektiğinde ayarlanır. Varsayılan olarak dosyanın adıdır.

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

Özel bir hedef yazın ve `$(TargetsForTfmSpecificContentInPackage)` özelliğinin değeri olarak belirtin. Pakete dahil edilecek herhangi bir dosya için, hedef bu dosyaları ItemGroup `TfmSpecificPackageFile` ' a yazıp, aşağıdaki isteğe bağlı meta verileri ayarlamanız gerekir:

- `PackagePath`: dosyanın pakette çıkış olması gereken yol. Aynı paket yoluna birden fazla dosya eklenirse NuGet bir uyarı verir.
- `BuildAction`: dosyaya atanacak derleme eylemi, yalnızca paket yolu `contentFiles` klasörsde olduğunda gereklidir. Varsayılan "none" olarak belirlenmiştir.

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

`MSBuild -t:restore` (`nuget restore` ve @no__t-.NET Core projeleriyle birlikte kullanılan), proje dosyasında başvurulan paketleri aşağıdaki şekilde geri yükler:

1. Proje başvurularına tüm projeyi oku
1. Ara klasörünü ve hedef çerçeveleri bulmak için proje özelliklerini okuyun
1. MSBuild verilerini NuGet. Build. Tasks. dll dosyasına geçir
1. Geri yüklemeyi Çalıştır
1. Paketleri İndir
1. Varlıklar dosyası, hedefler ve props yazma

@No__t-0 hedefi **yalnızca** packagereference biçimi kullanan projeler için kullanılabilir. @No__t-1 biçimini kullanan projeler **için çalışmaz;** Bunun yerine [NuGet geri yükleme](../reference/cli-reference/cli-ref-restore.md) kullanın.

### <a name="restore-properties"></a>Özellikleri geri yükle

Ek geri yükleme ayarları proje dosyasındaki MSBuild özelliklerinden gelebilir. Değerler, `-p:` anahtarı kullanılarak komut satırından da ayarlanabilir (aşağıdaki örneklere bakın).

| Özellik | Açıklama |
|--------|--------|
| RestoreSources | Paket kaynaklarının noktalı virgülle ayrılmış listesi. |
| RestorePackagesPath | Kullanıcı paketleri klasör yolu. |
| RestoreDisableParallel | İndirmeleri tek seferde bir ile sınırlayın. |
| RestoreConfigFile | Uygulanacak `Nuget.Config` dosyasının yolu. |
| RestoreNoCache | Doğru ise, önbelleğe alınmış paketlerin kullanılmasını önler. Bkz. [genel paketleri ve önbellek klasörlerini yönetme](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| Restoreıgnorefailedsources | Doğru ise, başarısız veya eksik paket kaynaklarını yoksayar. |
| RestoreFallbackFolders | Geri dönüş klasörleri, Kullanıcı paketleri klasörüyle aynı şekilde kullanılır. |
| Restoreaddıtionalprojectsources | Geri yükleme sırasında kullanılacak ek kaynaklar. |
| Restoreaddıtionalprojectfallbackfolders | Geri yükleme sırasında kullanılacak ek geri dönüş klasörleri. |
| RestoreAdditionalProjectFallbackFoldersExcludes | @No__t belirtilen geri dönüş klasörlerini dışlar-0 |
| RestoreTaskAssemblyFile | @No__t-0 için yol. |
| Restoregraphprojectınput | Geri yüklenecek projelerin, mutlak yollar içermesi gereken, noktalı virgülle ayrılmış listesi. |
| Restoreuseskipnontenttargets  | Projeler MSBuild aracılığıyla toplandığında, bunların `SkipNonexistentTargets` iyileştirmesi kullanılarak toplanıp toplanmayacağını belirler. Ayarlanmazsa, varsayılan olarak `true` olur. Projenin hedefleri içeri aktarılmadığı zaman, sonuç hızlı bir davranıştır. |
| Msbuildprojeclarsionspath | Çıkış klasörü, `BaseIntermediateOutputPath` ve `obj` klasörü ayarlanıyor. |
| Restorezorlamalı | PackageReference tabanlı projelerde, son geri yükleme başarılı olsa bile tüm bağımlılıkların çözülmesini zorlar. Bu bayrağın belirtilmesi `project.assets.json` dosyasını silmeye benzerdir. Bu, http-cache ' i atlar. |

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

Restore, derleme `obj` klasöründe aşağıdaki dosyaları oluşturur:

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

Aynı mantık `build` ' a benzer diğer hedefler için de geçerlidir.

### <a name="packagetargetfallback"></a>PackageTargetFallback

@No__t-0 öğesi, paketler geri yüklenirken kullanılacak bir dizi uyumlu hedef belirtmenize olanak tanır. DotNet [TXD](../reference/target-frameworks.md) kullanan paketlere, DotNet TXD bildirmeyin uyumlu paketlerle çalışmak üzere tasarlanmıştır. Diğer bir deyişle, projeniz DotNet TXD 'yi kullanıyorsa, DotNet olmayan platformların DotNet ile uyumlu olmasını sağlamak üzere projenize `<PackageTargetFallback>` ' ı eklemediğiniz sürece, bağımlı olduğu tüm paketlerin DotNet TXD olması gerekir.

Örneğin, proje `netstandard1.6` TXI kullanıyorsa ve bağımlı bir paket yalnızca `lib/net45/a.dll` ve `lib/portable-net45+win81/a.dll` içeriyorsa, projenin derlenmesi başarısız olur. İçine getirmek istediğiniz değer ikinci DLL ise, `portable-net45+win81` DLL 'inin uyumlu olduğunu söylemek için `PackageTargetFallback` ' ı aşağıdaki şekilde ekleyebilirsiniz:

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

Projenizdeki tüm hedeflere geri dönüş bildirmek için `Condition` özniteliğini bırakın. Ayrıca, burada gösterildiği gibi, `$(PackageTargetFallback)` ekleyerek var olan @no__t de genişletebilirsiniz:

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a>Bir geri yükleme grafiğinden bir kitaplığı değiştirme

Geri yükleme yanlış derlemeyi alıyorsa, bu paketlerin varsayılan seçeneğini hariç tutabilir ve kendi seçimiyle değiştirin. İlk olarak @no__t en üst düzey olan-0, tüm varlıkları hariç tut:

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

Ardından, DLL 'nin uygun yerel kopyasına kendi başvurunuz ekleyin:

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
