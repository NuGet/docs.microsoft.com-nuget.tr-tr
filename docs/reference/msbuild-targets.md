---
title: NuGet paketi ve geri yükleme MSBuild hedefleri olarak
description: NuGet paketi ve geri yükleme, NuGet 4.0 + ile doğrudan MSBuild hedefleri olarak çalışabilir.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 922fc0b25664dede59e33c6cd012dfeedcad0397
ms.sourcegitcommit: 415c70d7014545c1f65271a2debf8c3c1c5eb688
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/06/2020
ms.locfileid: "77036935"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>NuGet paketi ve geri yükleme MSBuild hedefleri olarak

*NuGet 4.0 +*

[Packagereference](../consume-packages/package-references-in-project-files.md) biçimi sayesinde, NuGet 4.0 + tüm bildirim meta verilerini ayrı bir `.nuspec` dosyası kullanmak yerine doğrudan proje dosyası içinde depolayabilirler.

MSBuild 15.1 + ile NuGet, aşağıda açıklandığı gibi `pack` ve `restore` hedefleri ile birinci sınıf MSBuild vatandaşlık. Bu hedefler, diğer herhangi bir MSBuild görevi veya hedefi ile yaptığınız gibi NuGet ile çalışmanıza olanak sağlar. MSBuild kullanarak bir NuGet paketi oluşturma yönergeleri için bkz. [MSBuild kullanarak NuGet paketi oluşturma](../create-packages/creating-a-package-msbuild.md). (NuGet 3. x ve öncesi için, bunun yerine NuGet CLı aracılığıyla [paketle](../reference/cli-reference/cli-ref-pack.md) ve [geri yükleme](../reference/cli-reference/cli-ref-restore.md) komutlarını kullanırsınız.)

## <a name="target-build-order"></a>Hedef derleme sırası

`pack` ve `restore` MSBuild hedefleri olduğundan, iş akışınızı iyileştirmek için bunlara erişebilirsiniz. Örneğin, paketledikten sonra paketinizi bir ağ paylaşımında kopyalamak istediğinizi varsayalım. Bunu, proje dosyanıza aşağıdakileri ekleyerek yapabilirsiniz:

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

PackageReference biçimini kullanan .NET Standard projeleri için `msbuild -t:pack` kullanarak, bir NuGet paketi oluştururken kullanılacak proje dosyasından girişler çizer.

Aşağıdaki tabloda, ilk `<PropertyGroup>` düğümü içindeki bir proje dosyasına eklenebilen MSBuild özellikleri açıklanmaktadır. Bu düzenlemeleri Visual Studio 2017 ve sonraki sürümlerde kolayca yaparak, projeye sağ tıklayıp bağlam menüsünde **{Project_Name} Düzenle** ' yi seçerek yapabilirsiniz. Kolaylık sağlaması için tablo, bir [`.nuspec` dosyasındaki](../reference/nuspec.md)denk özelliğe göre düzenlenir.

`.nuspec` `Owners` ve `Summary` özelliklerinin MSBuild ile desteklenmediğini unutmayın.

| Öznitelik/NuSpec değeri | MSBuild özelliği | Varsayılan | Notlar |
|--------|--------|--------|--------|
| Kimlik | PackageId | AssemblyName | MSBuild 'ten $ (AssemblyName) |
| Sürüm | PackageVersion | Sürüm | Bu semver uyumludur, örneğin "1.0.0", "1.0.0-Beta" veya "1.0.0-Beta-00345" |
| VersionPrefix | PackageVersionPrefix | empty | PackageVersion ayarı PackageVersionPrefix üzerine yazıyor |
| VersionSuffix | PackageVersionSuffix | empty | MSBuild 'ten $ (VersionSuffix). PackageVersion ayarı PackageVersionSuffix üzerine yazıyor |
| Yazarlar | Yazarlar | Geçerli kullanıcının Kullanıcı adı | |
| Sahipler | Yok | NuSpec içinde yok | |
| Başlık | Başlık | PackageID| |
| Açıklama | Açıklama | "Paket açıklaması" | |
| Yaptırımlar | Yaptırımlar | empty | |
| Requirelicensekabulünü | PackageRequireLicenseAcceptance | false | |
| lisan | PackageLicenseExpression | empty | `<license type="expression">` karşılık gelir |
| lisan | PackageLicenseFile | empty | `<license type="file">`karşılık gelir. Başvurulan lisans dosyasını açık bir şekilde paketetmeniz gerekir. |
| LicenseUrl | PackageLicenseUrl | empty | `PackageLicenseUrl` kullanım dışı, PackageLicenseExpression veya PackageLicenseFile özelliğini kullanın |
| ProjectUrl | PackageProjectUrl | empty | |
| Simge | Packageıcon | empty | Başvurulan simge görüntü dosyasını açıkça paketetmeniz gerekir.|
| IconUrl | PackageIconUrl | empty | En iyi alt düzey deneyim için, `PackageIcon`ek olarak `PackageIconUrl` belirtilmelidir. Daha uzun vadeli `PackageIconUrl` kullanım dışı bırakılır. |
| Etiketler | PackageTags | empty | Etiketler noktalı virgülle ayrılır. |
| Relet 'ler | PackageReleaseNotes | empty | |
| Depo/URL | Depourl 'Si | empty | Kaynak kodu kopyalamak veya almak için kullanılan depo URL 'SI. Örnek: *https://github.com/NuGet/NuGet.Client.git* |
| Depo/tür | Repositorytype parametrelerinin sağlanması | empty | Depo türü. Örnekler: *Git*, *TFS*. |
| Depo/dal | Depodalı | empty | İsteğe bağlı depo dalı bilgileri. Bu özelliğin dahil olması için aynı zamanda bir *Depo-URL* belirtilmelidir. Örnek: *Master* (NuGet 4.7.0 +) |
| Depo/kayıt | Kayıt yapma | empty | Paketin hangi kaynağa göre oluşturulduğunu göstermek için isteğe bağlı depo kaydı veya değişiklik kümesi. Bu özelliğin dahil olması için aynı zamanda bir *Depo-URL* belirtilmelidir. Örnek: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +) |
| PackageType | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| Özet | Desteklenmiyor | | |

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

Oluşturulan NuGet paketinden paket bağımlılıklarını bastırmak için `SuppressDependenciesWhenPacking`, oluşturulan nupkg dosyasından tüm bağımlılıkların atlanmasını sağlayacak `true` olarak ayarlayın.

### <a name="packageiconurl"></a>PackageIconUrl

`PackageIconUrl`, yeni [`PackageIcon`](#packageicon) özelliğinin yararına kullanım dışı olacaktır.

NuGet 5,3 & Visual Studio 2019 sürüm 16,3 ' den başlayarak, paket meta verileri yalnızca `PackageIconUrl`belirtiyorsa, `pack` [NU5048](./errors-and-warnings/nu5048.md) uyarı verecek.

### <a name="packageicon"></a>Packageıcon

> [!Tip]
> Henüz `PackageIcon`desteklemeyen istemcilerle ve kaynaklarla geriye dönük uyumluluk sağlamak için hem `PackageIcon` hem de `PackageIconUrl` belirtmeniz gerekir. Visual Studio, gelecekteki sürümlerde bulunan klasör tabanlı bir kaynaktan gelen paketlere yönelik `PackageIcon` destekleyecektir.

#### <a name="packing-an-icon-image-file"></a>Simge görüntüsü dosyası paketleme

Bir simge resim dosyası paketleme sırasında, paketin köküne göre paket yolunu belirtmek için `PackageIcon` özelliğini kullanmanız gerekir. Ayrıca, dosyanın pakete eklendiğinden emin olmanız gerekir. Görüntü dosyası boyutu 1 MB ile sınırlıdır. Desteklenen dosya biçimleri JPEG ve PNG içerir. 128x128 görüntü çözümlemesi yapmanızı öneririz.

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

[Paket simgesi örneği](https://github.com/NuGet/Samples/tree/master/PackageIconExample).

Nuspec eşdeğeri için, [simgenin nuspec başvurusuna](nuspec.md#icon)göz atın.

### <a name="output-assemblies"></a>Çıkış derlemeleri

`nuget pack`, `.exe`, `.dll`, `.xml`, `.winmd`, `.json`ve `.pri`uzantılı çıktı dosyalarını kopyalar. Kopyalanan çıkış dosyaları, `BuiltOutputProjectGroup` hedeften MSBuild 'in sağladığı öğesine bağlıdır.

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

İçerik eklemek için varolan `<Content>` öğesine ek meta veriler ekleyin. Varsayılan olarak, aşağıdaki gibi girdilerle geçersiz kılmadığınız müddetçe "Içerik" türünde her şey pakete dahil edilir:

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

Tüm içeriğinizi yalnızca belirli bir kök klasöre (`content` ve `contentFiles` her ikisi de) kopyalamak istiyorsanız, "Content; contentFiles" varsayılan olarak ayarlanan ancak diğer herhangi bir klasör adına ayarlanabilir MSBuild `ContentTargetFolders`özelliğini kullanabilirsiniz. Yalnızca `ContentTargetFolders` ' de "contentFiles" öğesinin belirtildiğine, `buildAction`göre `contentFiles\any\<target_framework>` veya `contentFiles\<language>\<target_framework>` altına dosya yerleştirdiğine unutmayın.

`PackagePath`, noktalı virgülle ayrılmış bir hedef yolları kümesi olabilir. Boş bir paket yolu belirtilmesi, dosyayı paketin köküne ekler. Örneğin, aşağıdaki `content\myfiles`, `content\samples`ve paket köküne `libuv.txt` ekler:

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

Ayrıca, `true`varsayılan olarak `$(IncludeContentInPack)`bir MSBuild özelliği de vardır. Bu, herhangi bir projede `false` olarak ayarlandıysa, bu projeden içerik NuGet paketine dahil edilmez.

Yukarıdaki öğelerin herhangi birinde ayarlayabileceğiniz diğer paketine özgü meta veriler, ```CopyToOutput``` ve ```Flatten``` değerlerini, çıkış nuspec içindeki ```contentFiles``` girişi üzerinde ayarlayan ```<PackageCopyToOutput>``` ve ```<PackageFlatten>``` içerir.

> [!Note]
> Içerik öğelerinden ayrı olarak, `<Pack>` ve `<PackagePath>` meta verileri de derleme, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, Paketleresource veya None derleme eylemine sahip dosyalar üzerinde de ayarlanabilir.
>
> Glob desenleri kullanılırken dosya adını paket yolunuza eklemek için paket yolu, klasör ayırıcı karakteriyle bitmelidir; Aksi takdirde, paket yolu dosya adı dahil tam yol olarak değerlendirilir.

### <a name="includesymbols"></a>Includesymbols

`MSBuild -t:pack -p:IncludeSymbols=true`kullanırken, karşılık gelen `.pdb` dosyaları diğer çıkış dosyalarıyla birlikte kopyalanır (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`). `IncludeSymbols=true` ayarlamanın düzenli bir paket *ve* bir semboller paketi oluşturduğunu unutmayın.

### <a name="includesource"></a>IncludeSource

Bu, `IncludeSymbols`ile aynıdır, ancak `.pdb` dosyalarla birlikte kaynak dosyalarını kopyalar. `Compile` türündeki tüm dosyalar, elde edilen paketteki göreli yol klasörü yapısını koruyarak `src\<ProjectName>\` üzerine kopyalanır. Aynı zamanda, `false``TreatAsPackageReference` ayarlanmış tüm `ProjectReference` kaynak dosyaları için de aynı olur.

Derleme türünde bir dosya proje klasörünün dışındaysa, bu, `src\<ProjectName>\`sonuna eklenmiştir.

### <a name="packing-a-license-expression-or-a-license-file"></a>Lisans ifadesi veya lisans dosyası paketleme

Bir lisans ifadesi kullanılırken PackageLicenseExpression özelliğinin kullanılması gerekir. 
[Lisans ifadesi örneği](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

[NuGet.org tarafından kabul edilen lisans ifadeleri ve lisanslar hakkında daha fazla bilgi edinin](nuspec.md#license).

Bir lisans dosyası paketleme sırasında, paketin köküne göre paket yolunu belirtmek için PackageLicenseFile özelliğini kullanmanız gerekir. Ayrıca, dosyanın pakete eklendiğinden emin olmanız gerekir. Örnek:

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

`MSBuild -t:pack -p:IsTool=true`kullanırken, [Çıkış derlemeleri](#output-assemblies) senaryosunda belirtilen tüm çıkış dosyaları `lib` klasörü yerine `tools` klasörüne kopyalanır. Bu, `.csproj` dosyasında `PackageType` ayarlanarak belirtilen `DotNetCliTool` farklı olduğunu unutmayın.

### <a name="packing-using-a-nuspec"></a>. Nuspec kullanarak paketleme

Bunun yerine, genellikle proje dosyasındaki `.nuspec` dosyasında bulunan [tüm özellikleri eklemeniz](../reference/msbuild-targets.md#pack-target) önerilse de, projenizi paketetmek için bir `.nuspec` dosyası kullanmayı tercih edebilirsiniz. `PackageReference`kullanan SDK olmayan bir proje için, paket görevinin yürütülebilmesi için `NuGet.Build.Tasks.Pack.targets` içeri aktarmanız gerekir. Bir nuspec dosyası paketetmeden önce projeyi geri yüklemeniz gerekir. (SDK stili bir proje varsayılan olarak paket hedeflerini içerir.)

Proje dosyasının hedef çerçevesi ilgisizdir ve bir nuspec paketleme sırasında kullanılmaz. Aşağıdaki üç MSBuild özelliği, `.nuspec`kullanarak paketleme ile ilgilidir:

1. `NuspecFile`: paketleme için kullanılan `.nuspec` dosyasının göreli veya mutlak yolu.
1. `NuspecProperties`: anahtar = değer çiftleri için noktalı virgülle ayrılmış bir liste. MSBuild komut satırı ayrıştırması çalışma yöntemi nedeniyle, birden çok özellik şu şekilde belirtilmelidir: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.  
1. `NuspecBasePath`: `.nuspec` dosyasının temel yolu.

Projenizi paketmek için `dotnet.exe` kullanıyorsanız, aşağıdaki gibi bir komut kullanın:

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Projenizi paketmek için MSBuild kullanıyorsanız, aşağıdaki gibi bir komut kullanın:

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Lütfen DotNet. exe veya MSBuild kullanarak bir nuspec paketleme, projenin varsayılan olarak oluşturulmasına da neden olduğunu unutmayın. Bu, proje dosyasında ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` ayarı ile birlikte ```--no-build``` özelliği DotNet. exe ' ye geçirilerek ve proje dosyasındaki ```<NoBuild>true</NoBuild> ``` ayarlamaya eşittir.

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

`pack` hedefi, iç, hedef çerçeveye özgü derlemede çalışan iki uzantı noktası sağlar. Uzantı noktaları, hedef çerçeveye özgü içerik ve derlemelerin bir pakete dahil edilmesi için destek:

- `TargetsForTfmSpecificBuildOutput` target: `lib` klasörü veya `BuildOutputTargetFolder`kullanılarak belirtilen bir klasör içindeki dosyalar için kullanın.
- `TargetsForTfmSpecificContentInPackage` hedefi: `BuildOutputTargetFolder`dışındaki dosyalar için kullanın.

#### <a name="targetsfortfmspecificbuildoutput"></a>TargetsForTfmSpecificBuildOutput

Özel bir hedef yazın ve `$(TargetsForTfmSpecificBuildOutput)` özelliğinin değeri olarak belirtin. `BuildOutputTargetFolder` olması gereken tüm dosyalar için (varsayılan olarak LIB), hedef bu dosyaları ItemGroup `BuildOutputInPackage` içine yazmalıdır ve aşağıdaki iki meta veri değerini ayarlamış olmalıdır:

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

#### <a name="targetsfortfmspecificcontentinpackage"></a>TargetsForTfmSpecificContentInPackage

Özel bir hedef yazın ve `$(TargetsForTfmSpecificContentInPackage)` özelliğinin değeri olarak belirtin. Pakete dahil edilecek tüm dosyalar için, hedef bu dosyaları ItemGroup 'a yazmalıdır `TfmSpecificPackageFile` ve aşağıdaki isteğe bağlı meta verileri ayarlar:

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

`MSBuild -t:restore` (`nuget restore` ve `dotnet restore` .NET Core projeleriyle birlikte kullanılır), proje dosyasında başvurulan paketleri aşağıdaki şekilde geri yükler:

1. Proje başvurularına tüm projeyi oku
1. Ara klasörünü ve hedef çerçeveleri bulmak için proje özelliklerini okuyun
1. MSBuild verilerini NuGet. Build. Tasks. dll dosyasına geçir
1. Geri yüklemeyi Çalıştır
1. Paketleri İndir
1. Varlıklar dosyası, hedefler ve props yazma

`restore` hedefi **yalnızca** packagereference biçimini kullanan projeler için kullanılabilir. `packages.config` biçimi kullanan projeler **için çalışmaz;** Bunun yerine [NuGet geri yükleme](../reference/cli-reference/cli-ref-restore.md) kullanın.

### <a name="restore-properties"></a>Özellikleri geri yükle

Ek geri yükleme ayarları proje dosyasındaki MSBuild özelliklerinden gelebilir. Değerler, `-p:` anahtarı kullanılarak komut satırından da ayarlanabilir (aşağıdaki örneklere bakın).

| Özellik | Açıklama |
|--------|--------|
| RestoreSources | Paket kaynaklarının noktalı virgülle ayrılmış listesi. |
| RestorePackagesPath | Kullanıcı paketleri klasör yolu. |
| RestoreDisableParallel | İndirmeleri tek seferde bir ile sınırlayın. |
| RestoreConfigFile | Uygulanacak `Nuget.Config` dosyasının yolu. |
| RestoreNoCache | Doğru ise, önbelleğe alınmış paketlerin kullanılmasını önler. Bkz. [genel paketleri ve önbellek klasörlerini yönetme](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| RestoreIgnoreFailedSources | Doğru ise, başarısız veya eksik paket kaynaklarını yoksayar. |
| RestoreFallbackFolders | Geri dönüş klasörleri, Kullanıcı paketleri klasörüyle aynı şekilde kullanılır. |
| Restoreaddıtionalprojectsources | Geri yükleme sırasında kullanılacak ek kaynaklar. |
| Restoreaddıtionalprojectfallbackfolders | Geri yükleme sırasında kullanılacak ek geri dönüş klasörleri. |
| RestoreAdditionalProjectFallbackFoldersExcludes | `RestoreAdditionalProjectFallbackFolders` belirtilen geri dönüş klasörlerini dışlar |
| RestoreTaskAssemblyFile | `NuGet.Build.Tasks.dll`yolu. |
| RestoreGraphProjectInput | Geri yüklenecek projelerin, mutlak yollar içermesi gereken, noktalı virgülle ayrılmış listesi. |
| Restoreuseskipnontenttargets  | Projeler MSBuild aracılığıyla toplandığında, `SkipNonexistentTargets` iyileştirmesi kullanılarak toplanıp toplanmayacağını belirler. Ayarlanmazsa, varsayılan olarak `true`olur. Projenin hedefleri içeri aktarılmadığı zaman, sonuç hızlı bir davranıştır. |
| Msbuildprojeclarsionspath | Çıkış klasörü, `BaseIntermediateOutputPath` ve `obj` klasörü ayarlanıyor. |
| Restorezorlamalı | PackageReference tabanlı projelerde, son geri yükleme başarılı olsa bile tüm bağımlılıkların çözülmesini zorlar. Bu bayrağın belirtilmesi `project.assets.json` dosyasını silmeye benzerdir. Bu, http-cache ' i atlar. |
| RestorePackagesWithLockFile | Bir kilit dosyasının kullanımıyla ilgili olarak. |
| RestoreLockedMode | Geri yüklemeyi kilitli modda çalıştırın. Bu, geri yüklemenin bağımlılıkları yeniden değerlendirmeyeceği anlamına gelir. |
| NuGetLockFilePath | Kilit dosyası için özel bir konum. Varsayılan konum, projenin yanında `packages.lock.json`olarak adlandırılır. |
| Restoreforcedeğerlendir | Bağımlılıkları yeniden hesaplamak ve herhangi bir uyarı olmadan kilit dosyasını güncelleştirmek için geri yüklemeyi zorlar. | 

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

Aynı mantık `build`benzer diğer hedefler için de geçerlidir.

### <a name="packagetargetfallback"></a>PackageTargetFallback

`PackageTargetFallback` öğesi, paketler geri yüklenirken kullanılacak bir dizi uyumlu hedef belirtmenize olanak tanır. DotNet [TXD](../reference/target-frameworks.md) kullanan paketlere, DotNet TXD bildirmeyin uyumlu paketlerle çalışmak üzere tasarlanmıştır. Diğer bir deyişle, projeniz DotNet TXD kullanıyorsa, DotNet olmayan platformların DotNet ile uyumlu olmasını sağlamak için `<PackageTargetFallback>` projenize eklemediğiniz sürece tüm paketlerin DotNet TXD olması gerekir.

Örneğin, proje TXD `netstandard1.6` kullanıyorsa ve bağımlı bir paket yalnızca `lib/net45/a.dll` ve `lib/portable-net45+win81/a.dll`içeriyorsa, proje derlenmeyecektir. İçine getirmek istediğiniz değer ikinci DLL ise, `portable-net45+win81` DLL 'nin uyumlu olduğunu söylemek için `PackageTargetFallback` aşağıdaki gibi ekleyebilirsiniz:

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

Projenizdeki tüm hedeflere geri dönüş bildirmek için `Condition` özniteliğini bırakın. Ayrıca, aşağıda gösterildiği gibi `$(PackageTargetFallback)` ekleyerek mevcut `PackageTargetFallback` genişletebilirsiniz:

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a>Bir geri yükleme grafiğinden bir kitaplığı değiştirme

Geri yükleme yanlış derlemeyi alıyorsa, bu paketlerin varsayılan seçeneğini hariç tutabilir ve kendi seçimiyle değiştirin. Önce üst düzey `PackageReference`, tüm varlıkları hariç tut:

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

Ardından, DLL 'nin uygun yerel kopyasına kendi başvurunuz ekleyin:

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
