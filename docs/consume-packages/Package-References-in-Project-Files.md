---
title: NuGet PackageReference formatı (proje dosyalarındaki paket başvuruları)
description: NuGet 4.0+ ve VS2017 ve .NET Core 2.0 tarafından desteklenen proje dosyalarında NuGet PackageReference ile ilgili ayrıntılar
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: a5833df60c5f7905359f421141347b1237f45d86
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428872"
---
# <a name="package-references-packagereference-in-project-files"></a>Proje dosyalarındaki paket referansları (PackageReference)

Paket başvuruları, `PackageReference` düğümü kullanarak, NuGet bağımlılıklarını doğrudan proje dosyaları içinde `packages.config` yönetin (ayrı bir dosyanın aksine). PackageReference'ı kullanmak, nuget'in diğer yönlerini etkilemez; örneğin, dosyalardaki `NuGet.config` ayarlar (paket kaynakları dahil) Ortak [NuGet yapılandırmalarında](configuring-nuget-behavior.md)açıklandığı gibi hala uygulanır.

PackageReference ile, hedef çerçeve veya diğer gruplandırmalar başına paket başvuruları seçmek için MSBuild koşullarını da kullanabilirsiniz. Ayrıca bağımlılıklar ve içerik akışı üzerinde ince taneli kontrol sağlar. (Daha fazla bilgi için [NuGet paketi ve MSBuild hedefleri olarak geri yükleyin](../reference/msbuild-targets.md).)

## <a name="project-type-support"></a>Proje türü desteği

Varsayılan olarak PackageReference, C++ UWP projeleri dışında Windows 10 Build 15063 (Creators Update) ve daha sonrasını hedefleyen .NET Core projeleri, .NET Standard projeleri ve UWP projeleri için kullanılır. .NET Framework projeleri PackageReference'ı `packages.config`destekler, ancak şu anda varsayılan . PackageReference'ı kullanmak için, bağımlılıkları `packages.config` proje dosyanıza [geçirin](../consume-packages/migrate-packages-config-to-package-reference.md) ve ardından packages.config'i kaldırın.

ASP.NET .NET Framework'u hedefleyen uygulamalar, PackageReference için [yalnızca sınırlı destek](https://github.com/NuGet/Home/issues/5877) içerir. C++ ve JavaScript proje türleri desteklenmez.

## <a name="adding-a-packagereference"></a>PackageReference Ekleme

Aşağıdaki sözdizimini kullanarak proje dosyanıza bağımlılık ekleyin:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a>Bağımlılık sürümünü denetleme

Bir paketin sürümünü belirtmek için sözleşme kullanırken `packages.config`aynıdır:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

Yukarıdaki örnekte, 3.6.0, [Paket sürümünde](../concepts/package-versioning.md#version-ranges)açıklandığı gibi, en düşük sürümü tercih eden >=3.6.0 olan herhangi bir sürüm anlamına gelir.

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a>PackageReferences olmayan bir proje için PackageReference kullanma

Gelişmiş: Bir projede yüklü paketleriniz yoksa (proje dosyasında Paket Başvurusu yok ve packages.config dosyası yok) ancak projenin PackageReference stili olarak geri yüklenmesini istiyorsanız, proje dosyanızda PackageReference için Project özelliği RestoreProjectStyle ayarlayabilirsiniz.

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```

Bu, PackageReference stilinde olan projelere (mevcut csproj veya SDK tarzı projeler) başvurursanız yararlı olabilir. Bu, bu projelerin atıfta bulunduğu paketlerin projeniz tarafından "geçişli" olarak başvurulmasını sağlar.

## <a name="packagereference-and-sources"></a>PackageReference ve kaynaklar

PackageReference projelerinde, geçişli bağımlılık sürümleri geri yükleme zamanında çözülür. Bu nedenle, PackageReference projelerinde tüm kaynakların tüm geri yüklemeler için kullanılabilir olması gerekir. 

## <a name="floating-versions"></a>Kayan Sürümler

[Kayan sürümler:](../concepts/dependency-resolution.md#floating-versions) `PackageReference`

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a>Bağımlılık varlıklarını denetleme

Bir bağımlılığı tamamen geliştirme donanımı olarak kullanıyor olabilirsiniz ve bunu paketinizi tüketecek projelere maruz bırakmak istemeyebilirsiniz. Bu senaryoda, bu `PrivateAssets` davranışı denetlemek için meta verileri kullanabilirsiniz.

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

Aşağıdaki meta veri etiketleri bağımlılık varlıklarını denetler:

| Etiket | Açıklama | Varsayılan Değer |
| --- | --- | --- |
| Dahil Varlıklar | Bu varlıklar tüketilecek | tümü |
| Varlıkları Hariç Tutma | Bu varlıklar tüketilmeyecek | yok |
| Özel Varlıklar | Bu varlıklar tüketilecek, ancak ana projeye akmayacak | contentfiles;analyzers;build |

Bu etiketler için izin verilen değerler aşağıdaki gibidir, birden çok `all` `none` değer bir yarı kolon ile ayrılmış dışında ve kendi kendine görünmesi gerekir:

| Değer | Açıklama |
| --- | ---
| derle | Klasörün `lib` içeriği ve projenizin klasör içindeki derlemelere karşı derlenip derlenip derlemeyeceğini denetler |
| çalışma zamanı | Klasörün `lib` içeriği `runtimes` ve içeriği ve bu derlemelerin yapı çıktı dizini için kopyalanıp kopyalanmayacağını denetler |
| içerikDosyalar | Klasörün `contentfiles` içeriği |
| derleme | `.props`ve `.targets` klasörde `build` |
| buildMultitargeting | *(4.0)* `.props` `.targets` ve `buildMultitargeting` klasörde, çapraz çerçeve hedefleme için |
| buildGeçişive | *(5.0+)* `.props` `.targets` ve `buildTransitive` klasörde, herhangi bir tüketen projeye geçişli olarak akan varlıklar için. [Özellik](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) sayfasına bakın. |
| Analizörleri | .NET analizörleri |
| yerel | Klasörün `native` içeriği |
| yok | Yukarıdakilerin hiçbiri kullanılmaz. |
| tümü | Yukarıdakilerin tümü (hariç) `none` |

Aşağıdaki örnekte, paketteki içerik dosyaları dışındaki her şey proje tarafından tüketilir ve içerik dosyaları ve çözümleyiciler dışındaki her şey ana projeye akar.

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <IncludeAssets>all</IncludeAssets>
        <ExcludeAssets>contentFiles</ExcludeAssets>
        <PrivateAssets>contentFiles;analyzers</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

`build` Dahil `PrivateAssets`olmadığından, hedeflerin ve sahne desteklerinin ana projeye *akacağını* unutmayın. Örneğin, yukarıdaki başvurunun AppLogger adlı bir NuGet paketi oluşturan bir projede kullanıldığını göz önünde bulundurun. AppLogger hedefleri ve sahne tüketebilir `Contoso.Utility.UsefulStuff`, AppLogger tüketen projeler gibi.

> [!NOTE]
> Bir `developmentDependency` `.nuspec` `true` dosyada ayarlandığında, bu paket yalnızca geliştirme bağımlılığı olarak işaretler ve bu da paketin diğer paketlere bağımlılık olarak eklenmesini engeller. PackageReference *(NuGet 4.8+)* ile bu bayrak, derleme zamanı varlıklarını derlemeden hariç tutacağı anlamına da gelir. Daha fazla bilgi [için PackageReference için DevelopmentDependency desteğine](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)bakın.

## <a name="adding-a-packagereference-condition"></a>PackageReference koşulu ekleme

Bir paketin dahil edilip edilemeyeceğini, koşulların herhangi bir MSBuild değişkenini veya hedefler veya sahne dosyasında tanımlanan bir değişkeni kullanabildiği bir koşul kullanabilirsiniz. Ancak, şu anda `TargetFramework` yalnızca değişken desteklenir.

Örneğin, hedeflediğinizi, `netstandard1.4` `net452` ancak yalnızca `net452`. Bu durumda, paketinizi tüketen bir `netstandard1.4` projenin bu gereksiz bağımlılık eklemesini istemezsiniz. Bunu önlemek için aşağıdaki `PackageReference` gibi bir koşul belirtirsiniz:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

Bu proje kullanılarak oluşturulmuş bir paket Newtonsoft.Json'ın yalnızca bir `net452` hedef için bağımlılık olarak dahil edildiğini gösterir:

![VS2017 ile PackageReference Koşulu uygulama nın sonucu](media/PackageReference-Condition.png)

Koşullar aynı `ItemGroup` düzeyde de uygulanabilir ve tüm `PackageReference` çocuklar için geçerli olacaktır:

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="generatepathproperty"></a>PathÖzelliği Ni Oluştur

Bu özellik NuGet **5.0** ve üzeri ve Visual Studio 2019 **16.0** ve üzeri ile kullanılabilir.

Bazen bir MSBuild hedefinden bir paketteki dosyalara başvurmak istenir.
Tabanlı `packages.config` projelerde, paketler proje dosyasına göre bir klasöre yüklenir. Ancak PackageReference'da paketler, makineden makineye değişebilen *küresel paketler* klasöründen [tüketilir.](../concepts/package-installation-process.md)

Bu boşluğu kapatmak için NuGet, paketin tüketileceği yeri gösteren bir özellik sundu.

Örnek:

```xml
  <ItemGroup>
      <PackageReference Include="Some.Package" Version="1.0.0" GeneratePathProperty="true" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgSome_Package)\something.exe" />
  </Target>
````

Ayrıca NuGet, bir araç klasörü içeren paketler için otomatik olarak özellikler oluşturur.

```xml
  <ItemGroup>
      <PackageReference Include="Package.With.Tools" Version="1.0.0" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgPackage_With_Tools)\tools\tool.exe" />
  </Target>
````

MSBuild özellikleri ve paket kimlikleri aynı kısıtlamalara sahip değildir, bu nedenle paket kimliğinin sözcük `Pkg`tarafından önceden belirlenmiş bir MSBuild dostu adı ile değiştirilmesi gerekir.
Oluşturulan özelliğin tam adını doğrulamak için oluşturulan [nuget.g.prop](../reference/msbuild-targets.md#restore-outputs) dosyasına bakın.

## <a name="nuget-warnings-and-errors"></a>NuGet uyarıları ve hataları

*Bu özellik NuGet **4.3** ve üzeri ve Visual Studio 2017 **15.3** ve üzeri ile kullanılabilir.*

Birçok paket ve geri yükleme senaryoları için, tüm NuGet `NU****`uyarıları ve hataları kodlanır ve . Tüm NuGet uyarıları ve hataları [başvuru](../reference/errors-and-warnings.md) belgelerinde listelenir.

NuGet aşağıdaki uyarı özelliklerini gözlemler:

- `TreatWarningsAsErrors`, tüm uyarıları hata olarak ele
- `WarningsAsErrors`, belirli uyarıları hata olarak ele
- `NoWarn`, proje genelinde veya paket genelinde belirli uyarıları gizleyin.

Örnekler:

```xml
<PropertyGroup>
    <TreatWarningsAsErrors>true</TreatWarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <WarningsAsErrors>$(WarningsAsErrors);NU1603;NU1605</WarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <NoWarn>$(NoWarn);NU5124</NoWarn>
</PropertyGroup>
...
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0" NoWarn="NU1605" />
</ItemGroup>
```

### <a name="suppressing-nuget-warnings"></a>NuGet uyarılarını bastırma

Paketiniz sırasında tüm NuGet uyarılarını çözmeniz ve işlemleri geri yüklemeniz önerilirken, bazı durumlarda bunları bastırmanız garanti edilir.
Bir uyarı projesini geniş bir şekilde bastırmak için şunları yapmayı düşünün:

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
    <NoWarn>$(NoWarn);NU5104</NoWarn>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1"/>
</ItemGroup>
```

Bazen uyarılar yalnızca grafikteki belirli bir paketiçin geçerlidir. PackageReference öğesine bir tane `NoWarn` ekleyerek bu uyarıyı daha seçici bir şekilde bastırmayı seçebiliriz. 

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1" NoWarn="NU1603" />
</ItemGroup>
```

#### <a name="suppressing-nuget-package-warnings-in-visual-studio"></a>Visual Studio'da NuGet paket uyarılarını bastırma

Visual Studio'da, [IDE](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) aracılığıyla uyarıları da bastırabilirsiniz.

## <a name="locking-dependencies"></a>Kilitleme bağımlılıkları

*Bu özellik NuGet **4.9** ve üzeri ve Visual Studio 2017 **15.9** ve üzeri ile kullanılabilir.*

NuGet geri yükleme girişi, proje dosyasından (üst düzey veya doğrudan bağımlılıklar) paket başvuruları kümesidir ve çıktı, geçişli bağımlılıklar da dahil olmak üzere tüm paket bağımlılıklarının tam olarak kapatılmasıdır. NuGet, paket Başvuru listesi değişmediyse, paket bağımlılıklarının her zaman aynı tam kapatılmasını sağlamaya çalışır. Ancak, bunu yapamaz bazı senaryolar vardır. Örneğin:

* Gibi kayan sürümleri `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`kullandığınızda . Buradaki amaç, paketlerin her geri yüklemesinde en son sürüme float etmek olsa da, kullanıcıların grafiğin belirli bir son sürüme kilitlenmesini ve varsa açık bir hareketle daha sonraki bir sürüme doğru yüzdürülmesi gereken senaryolar vardır.
* PackageReference sürüm gereksinimlerini eşleştiren paketin daha yeni bir sürümü yayımlanır. Örneğin 

  * 1. Gün: `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` NuGet depolarında bulunan sürümleri n için belirtirseniz 4.1.0, 4.2.0 ve 4.3.0 idi. Bu durumda, NuGet 4.1.0 (en yakın minimum sürüm) olarak çözülmüş olurdu

  * 2. Gün: Sürüm 4.0.0 yayınlanır. NuGet şimdi tam eşleşmeyi bulacak ve 4.0.0'a çözmeye başlayacak

* Belirli bir paket sürümü depodan kaldırılır. nuget.org paket silmelere izin vermese de, tüm paket depolarında bu kısıtlamalar yoktur. Bu, NuGet'in silinen sürüme çözüm leyemediği zaman en iyi eşleşmeyi bulmasıyla sonuçlanır.

### <a name="enabling-lock-file"></a>Kilit dosyasını etkinleştirme

Paket bağımlılıklarının tamamen kapatılmasını sürdürmek için, projeniz için MSBuild özelliğini `RestorePackagesWithLockFile` ayarlayarak kilit dosyası özelliğini seçebilirsiniz:

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

Bu özellik ayarlanırsa, NuGet geri yüklemesi, tüm paket bağımlılıklarını listeleyen proje kök dizininde bir kilit dosyası - `packages.lock.json` dosya oluşturur. 

> [!Note]
> Bir proje `packages.lock.json` kök dizininde dosya varsa, özellik ayarlanmasa `RestorePackagesWithLockFile` bile kilit dosyası her zaman geri yükleme ile kullanılır. Bu nedenle, bu özelliği kabul etmenin başka bir `packages.lock.json` yolu da projenin kök dizininde sahte boş bir dosya oluşturmaktır.

### <a name="restore-behavior-with-lock-file"></a>`restore`kilit dosyası ile davranış
Proje için bir kilit dosyası varsa, NuGet çalıştırmak `restore`için bu kilit dosyasını kullanır. NuGet, proje dosyasında (veya bağımlı projelerin dosyalarında) belirtildiği gibi paket bağımlılıklarında herhangi bir değişiklik olup olmadığını görmek için hızlı bir denetim yapar ve herhangi bir değişiklik yoksa, kilit dosyasında belirtilen paketleri geri yüklenir. Paket bağımlılıklarının yeniden değerlendirilmesi yoktur.

NuGet, proje dosyasında(lar) belirtilen tanımlı bağımlılıklarda bir değişiklik algılarsa, paket grafiğini yeniden değerlendirir ve kilit dosyasını proje için yeni paket kapanışını yansıtacak şekilde güncelleştirir.

Anında paket bağımlılıklarını değiştirmek istemediğiniz CI/CD ve diğer senaryolar `lockedmode` için `true`şunları ayarlayarak bunu yapabilirsiniz:

dotnet.exe için, çalıştırın:

```
> dotnet.exe restore --locked-mode
```

msbuild.exe için çalıştırın:

```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

Bu koşullu MSBuild özelliğini proje dosyanızda da ayarlayabilirsiniz:

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

Kilitli mod `true`varsa, kilit dosyası oluşturulduktan sonra proje için tanımlanan paket bağımlılıklarını güncellediyseniz, kilit dosyasında listelenen tam paketleri geri yükleyin veya başarısız olur.

### <a name="make-lock-file-part-of-your-source-repository"></a>Kilit dosyanızı kaynak deponuzun bir parçası yapma
Bir uygulama, yürütülebilir bir uygulama oluşturuyorsanız ve söz konusu proje bağımlılık zincirinin başındaysa, NuGet'in geri yükleme sırasında bu uygulamadan yararlanabilmesi için kilit dosyasını kaynak kodu deposuna iade edin.

Ancak, projeniz göndermediğiniz bir kitaplık projesi veya diğer projelerin bağlı olduğu ortak bir kod projesiyse, kaynak kodunuzun bir parçası olarak kilit dosyasını iade **etmemelisiniz.** Kilit dosyasını tutmanın bir sakıncası yoktur, ancak bu ortak kod projesine bağlı olan bir projenin geri yüklenir/oluşturulması sırasında kilit dosyasında listelenen ortak kod projesi için kilitli paket bağımlılıkları kullanılamaz.

Örn.

```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```

Bir `ProjectA` `PackageX` `2.0.0` sürüme bağımlıysa ve `ProjectB` `PackageX` aynı zamanda sürüme `1.0.0`bağlı olarak başvurular `ProjectB` da varsa, `PackageX` kilit `1.0.0`dosyası sürüme bir bağımlılık listeleyecek. Ancak, `ProjectA` ne zaman inşa edilir, onun kilit `PackageX` **`2.0.0`** dosyası sürümü bir bağımlılık içerir `ProjectB`ve kilit dosyasında listelenen **değil.** `1.0.0` Bu nedenle, ortak bir kod projesinin kilit dosyası, bağlı olan projeler için çözülen paketler üzerinde çok az söz hakkı vardır.

### <a name="lock-file-extensibility"></a>Dosya genişletilebilirliğini kilitle

Aşağıda açıklandığı gibi kilit dosyası ile geri yükleme çeşitli davranışları denetleyebilirsiniz:

| NuGet.exe seçeneği | dotnet seçeneği | MSBuild eşdeğer seçeneği | Açıklama |
|:--- |:--- |:--- |:--- |
| `-UseLockFile` |`--use-lock-file` | Geri YüklemePaketleriWithLockFile | Kilit dosyasının kullanımını seçer. |
| `-LockedMode` | `--locked-mode` | RestoreLockedMode | Geri yükleme için kilitli modu sağlar. Bu, yinelenebilir yapılar istediğiniz CI/CD senaryolarında yararlıdır.|   
| `-ForceEvaluate` | `--force-evaluate` | Geri YüklemeGücü Değerlendirin | Bu seçenek, projede tanımlanan kayan sürümü olan paketler için yararlıdır. Varsayılan olarak, NuGet geri yüklemesi, bu seçenekle geri yükleme çalıştırmadığınız sürece paket sürümünü her geri yüklemede otomatik olarak güncelleştirmez. |
| `-LockFilePath` | `--lock-file-path` | NuGetLockFilePath | Proje için özel bir kilit dosyası konumunu tanımlar. Varsayılan olarak, NuGet kök dizininde destekler. `packages.lock.json` Aynı dizinde birden çok projeniz varsa, NuGet projeye özgü kilit dosyasını destekler`packages.<project_name>.lock.json` |
