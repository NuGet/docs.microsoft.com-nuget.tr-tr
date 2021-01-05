---
title: NuGet PackageReference biçimi (proje dosyalarındaki paket başvuruları)
description: NuGet 4.0 + ve VS2017 ve .NET Core 2,0 tarafından desteklenen proje dosyalarında NuGet PackageReference ile ilgili ayrıntılar
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 1127e7aee27d57abd5f14dd3bea82dfff3ba6d93
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699786"
---
# <a name="package-references-packagereference-in-project-files"></a>Proje dosyalarında paket başvuruları (PackageReference)

Paket başvuruları, düğümü kullanarak `PackageReference` , NuGet bağımlılıklarını doğrudan proje dosyaları içinde (ayrı bir `packages.config` dosyanın aksine) yönetir. Çağrılan, PackageReference kullanarak NuGet 'in diğer yönlerini etkilemez; Örneğin, `NuGet.config` dosyalardaki (paket kaynakları dahil) ayarlar, [ortak NuGet yapılandırmalarında](configuring-nuget-behavior.md)açıklandığı gibi hala uygulanır.

PackageReference ile, MSBuild koşullarını hedef çerçeve başına paket başvurularını veya diğer gruplandırmaları seçmek için de kullanabilirsiniz. Ayrıca bağımlılıklar ve içerik akışı üzerinde ayrıntılı denetim sağlar. (Daha fazla ayrıntı Için bkz. [NuGet paketi ve geri yükleme MSBuild hedefleri olarak](../reference/msbuild-targets.md).)

## <a name="project-type-support"></a>Proje türü desteği

Varsayılan olarak, PackageReference, .NET Core projeleri, .NET Standard projeleri ve Windows 10 Build 15063 (Creators Update) ve üstünü hedefleyen UWP projeleri için, C++ UWP projeleri dışında kullanılır. .NET Framework projeler, PackageReference destekler, ancak şu anda varsayılan olarak `packages.config` . PackageReference kullanmak için, [](../consume-packages/migrate-packages-config-to-package-reference.md) bağımlılıkları `packages.config` proje dosyanıza geçirin ve ardından packages.config kaldırın.

Tam .NET Framework hedefleyen uygulamalar, PackageReference için yalnızca [sınırlı desteği](https://github.com/NuGet/Home/issues/5877) içerir. C++ ve JavaScript proje türleri desteklenmez.

## <a name="adding-a-packagereference"></a>PackageReference ekleme

Aşağıdaki sözdizimini kullanarak proje dosyanıza bir bağımlılık ekleyin:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a>Bağımlılık sürümünü denetleme

Bir paketin sürümünü belirtme kuralı, kullanırken olduğu gibi aynıdır `packages.config` :

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

Yukarıdaki örnekte 3.6.0, [paket sürümü oluşturma](../concepts/package-versioning.md#version-ranges)bölümünde açıklandığı gibi en düşük sürüm için tercihe sahip >= 3.6.0 olan herhangi bir sürüm anlamına gelir.

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a>Packagereferde olmayan bir proje için PackageReference kullanma

Gelişmiş: bir projede yüklü paketleriniz yoksa (proje dosyasında ve hiçbir packages.config dosyası yoksa), ancak projenin PackageReference stili olarak geri yüklenmesini istiyorsanız, bir proje özelliği olarak bir proje özelliği olarak, proje dosyanızda PackageReference olarak ayarlayabilirsiniz.

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```

Bu, PackageReference stilli (mevcut csproj veya SDK stili projeler) projelere başvuru yaparsanız yararlı olabilir. Bu, bu projelerin başvurduğu paketleri projeniz tarafından "geçişli" olacak şekilde sağlayacak şekilde etkinleştirir.

## <a name="packagereference-and-sources"></a>PackageReference ve kaynakları

PackageReference projelerinde, geçişli bağımlılık sürümleri geri yükleme sırasında çözümlenir. Bu nedenle, PackageReference projelerinde tüm kaynakların tüm geri yüklemeler için kullanılabilir olması gerekir. 

## <a name="floating-versions"></a>Kayan sürümler

[Kayan sürümler](../concepts/dependency-resolution.md#floating-versions) ile desteklenir `PackageReference` :

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a>Bağımlılık varlıklarını denetleme

Yalnızca bir geliştirme bandı olarak bir bağımlılık kullanıyor olabilirsiniz ve bunu paketinizi kullanacak projelere göstermek istemeyebilirsiniz. Bu senaryoda, `PrivateAssets` Bu davranışı denetlemek için meta verileri kullanabilirsiniz.

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

Aşağıdaki meta veri etiketleri denetim bağımlılığı varlıkları:

| Etiket | Açıklama | Varsayılan değer |
| --- | --- | --- |
| Includevarlıklarını | Bu varlıklar tüketilecektir | tümü |
| Excludevarlıklarının | Bu varlıklar tüketilmeyecek | yok |
| Privatevarlıkların | Bu varlıklar tüketilecektir, ancak üst projeye akamaz | ContentFiles; çözümleyiciler; derleme |

Bu etiketler için izin verilen değerler aşağıdaki gibidir: ile, ve arasında bir noktalı virgülle ayrılmış birden çok değer `all` ve `none` kendileri tarafından görünmesi gerekir:

| Değer | Açıklama |
| --- | ---
| derle | `lib`Klasörün içeriği ve projenizin içindeki derlemelere göre derleyemeyeceğini denetler |
| çalışma zamanı | `lib`Ve `runtimes` klasörünün içeriği ve bu derlemelerin derleme çıkış dizinine kopyalanıp kopyalanmayacağını denetler |
| contentFiles | `contentfiles`Klasörün içeriği |
| derleme | `.props` ve `.targets` `build` klasörü |
| Buildmultihedefleme | *(4,0)* `.props` ve `.targets` `buildMultitargeting` klasöründe, platformlar arası hedefleme için |
| buildTransitive | *(5.0 +)* `.props` ve `.targets` `buildTransitive` klasörü, her bir tüketen projeye geçişli olarak akan varlıklar içindir. Bkz. [özellik](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) sayfası. |
| Çözümleyicileri | .NET çözümleyicileri |
| yerel | `native`Klasörün içeriği |
| yok | Yukarıdakilerin hiçbiri kullanılmaz. |
| tümü | Yukarıdakilerin tümü (hariç `none` ) |

Aşağıdaki örnekte, paketteki içerik dosyaları hariç her şey proje tarafından, içerik dosyaları ve çözümleyiciler hariç her şey üst projeye akacaktır.

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

`build`İle birlikte dahil edilmediğinden `PrivateAssets` , hedefler ve props ana projeye akacağından  emin olmanız gerekir. Örneğin, yukarıdaki başvurunun Appgünlükçü adlı bir NuGet paketi oluşturan bir projede kullanıldığını göz önünde bulundurun. Appgünlükçü, `Contoso.Utility.UsefulStuff` Appgünlükçü kullanan projeler gibi, öğesinden hedefleri ve props 'ı kullanabilir.

> [!NOTE]
> `developmentDependency` `true` , Bir dosyada olarak ayarlandığında `.nuspec` , paketin diğer paketlere bağımlılık olarak eklenmesini önleyen bir paketi yalnızca geliştirme bağımlılığı olarak işaretler. PackageReference *(NuGet 4.8 +)* ile bu bayrak Ayrıca derleme zamanı varlıklarını derlemeden dışlayacak anlamına gelir. Daha fazla bilgi için bkz. [PackageReference Için Developmentdependency desteği](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).

## <a name="adding-a-packagereference-condition"></a>PackageReference koşulu ekleme

Bir paketin dahil edilip edilmeyeceğini denetlemek için bir koşul kullanabilirsiniz. burada koşullar herhangi bir MSBuild değişkeni veya hedefler veya props dosyasında tanımlanan bir değişken kullanabilir. Ancak şu anda yalnızca `TargetFramework` değişken desteklenir.

Örneğin, hedeflentiğinizi ve `netstandard1.4` `net452` yalnızca için geçerli olan bir bağımlılığa sahip olduğunuzu varsayalım `net452` . Bu durumda, `netstandard1.4` paketinize tüketen bir projenin bu gereksiz bağımlılığı eklemesini istemezsiniz. Bunu engellemek için aşağıdaki şekilde bir koşul belirtirsiniz `PackageReference` :

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

Bu proje kullanılarak oluşturulan bir paket, üzerinde Newtonsoft.Js, yalnızca bir hedefin bağımlılığı olarak ekleneceğini gösterir `net452` :

![VS2017 ile PackageReference üzerinde koşul uygulamanın sonucu](media/PackageReference-Condition.png)

Koşullar da `ItemGroup` düzeyde uygulanabilir ve tüm alt öğeler için geçerli olacaktır `PackageReference` :

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="generatepathproperty"></a>GeneratePathProperty

Bu özellik NuGet **5,0** veya sonraki sürümlerde ve Visual Studio 2019 **16,0** veya üzeri sürümlerde kullanılabilir.

Bazen bir MSBuild hedefinden bir paketteki dosyalara başvurulmasına tercih edilir.
`packages.config`Tabanlı projelerde, paketler proje dosyası ile ilişkili bir klasöre yüklenir. Ancak, PackageReference içinde paketler, makineden makineye değişebilen *küresel paketler* [klasöründen kullanılır.](../concepts/package-installation-process.md)

Bu boşluğu bağlamak için, NuGet paketin tükettiği konuma işaret eden bir özellik sunmuştur.

Örnek:

```xml
  <ItemGroup>
      <PackageReference Include="Some.Package" Version="1.0.0" GeneratePathProperty="true" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgSome_Package)\something.exe" />
  </Target>
````

Ayrıca NuGet, bir Araçlar klasörü içeren paketler için otomatik olarak Özellikler oluşturacaktır.

```xml
  <ItemGroup>
      <PackageReference Include="Package.With.Tools" Version="1.0.0" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgPackage_With_Tools)\tools\tool.exe" />
  </Target>
```

MSBuild özellikleri ve paket kimlikleri aynı kısıtlamalara sahip değildir, bu nedenle paket kimliğinin, sözcüğün ön eki olan MSBuild kolay adına değiştirilmesi gerekir `Pkg` .
Oluşturulan özelliğin tam adını doğrulamak için, oluşturulan [NuGet. g. props](../reference/msbuild-targets.md#restore-outputs) dosyasına bakın.

## <a name="packagereference-aliases"></a>PackageReference diğer adları

Nadir bazı örneklerde farklı paketler aynı ad alanındaki sınıfları içerecektir. NuGet 5,7 ' den başlayarak, ProjectReference ile eşdeğer olan Visual Studio 2019 güncelleştirme 7 &, PackageReference desteklenir [`Aliases`](/dotnet/api/microsoft.codeanalysis.projectreference.aliases) .
Varsayılan olarak, diğer ad sağlanmaz. Bir diğer ad belirtildiğinde, ek açıklamalı paketten gelen *Tüm* derlemeler bir diğer adla başvurulmalıdır.

[Nuget\samples](https://github.com/NuGet/Samples/tree/master/PackageReferenceAliasesExample) ' da örnek kullanıma bakabilirsiniz

Proje dosyasında, diğer adları aşağıdaki gibi belirtin:

```xml
  <ItemGroup>
    <PackageReference Include="NuGet.Versioning" Version="5.8.0" Aliases="ExampleAlias" />
  </ItemGroup>
```

kodda, bunu aşağıdaki gibi kullanın:

```cs
extern alias ExampleAlias;

namespace PackageReferenceAliasesExample
{
...
        {
            var version = ExampleAlias.NuGet.Versioning.NuGetVersion.Parse("5.0.0");
            Console.WriteLine($"Version : {version}");
        }
...
}

```

## <a name="nuget-warnings-and-errors"></a>NuGet uyarıları ve hataları

*Bu özellik NuGet **4,3** veya sonraki sürümlerde ve Visual Studio 2017 **15,3** veya üzeri sürümlerde kullanılabilir.*

Birçok paket ve geri yükleme senaryosunda, tüm NuGet uyarıları ve hataları kodlanır ve ile başlar `NU****` . Tüm NuGet uyarıları ve hataları [başvuru](../reference/errors-and-warnings.md) belgelerinde listelenmiştir.

NuGet obonu aşağıdaki uyarı özelliklerine hizmet eder:

- `TreatWarningsAsErrors`, tüm uyarıları hata olarak değerlendir
- `WarningsAsErrors`, belirli uyarıları hata olarak değerlendir
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

### <a name="suppressing-nuget-warnings"></a>NuGet uyarılarını gizleme

Paket ve geri yükleme işlemleri sırasında tüm NuGet uyarılarını çözmeniz önerilir, ancak bazı durumlarda bunların garanti edilir.
Bir uyarı projesini genelinde gizlemek için şunları yapmayı düşünün:

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
    <NoWarn>$(NoWarn);NU5104</NoWarn>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1"/>
</ItemGroup>
```

Bazen uyarılar yalnızca grafikteki belirli bir paket için geçerlidir. PackageReference öğesine bir ekleyerek bu uyarının daha seçmeli şekilde görüntülenmesini seçebiliriz `NoWarn` . 

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1" NoWarn="NU1603" />
</ItemGroup>
```

#### <a name="suppressing-nuget-package-warnings-in-visual-studio"></a>Visual Studio 'da NuGet paket uyarılarını gizleme

Visual Studio 'da Ayrıca, uyarıları IDE aracılığıyla da [gizleyebilirsiniz](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) .

## <a name="locking-dependencies"></a>Bağımlılıkları kilitleme

*Bu özellik NuGet **4,9** veya sonraki sürümlerde ve Visual Studio 2017 **15,9** veya üzeri sürümlerde kullanılabilir.*

NuGet geri yükleme girdisi, proje dosyasından (en üst düzey veya doğrudan bağımlılıklar) paket başvuruları kümesidir ve çıkış geçişli bağımlılıklar dahil olmak üzere tüm paket bağımlılıklarının tam bir kapasitesinden oluşur. NuGet, giriş PackageReference listesi değişmediğinde paket bağımlılıklarının her zaman aynı tam kapatılmasını üretmeye çalışır. Ancak, bunu yapamaması gereken bazı senaryolar vardır. Örneğin:

* Gibi kayan sürümler kullandığınızda `<PackageReference Include="My.Sample.Lib" Version="4.*"/>` . Buradaki amaç paketlerin her geri yükleme işlemi için en son sürüme kaymalıdır, ancak kullanıcıların grafiğin belirli bir en son sürüme kilitlenmesini gerektiren senaryolar vardır ve açık bir hareket üzerine varsa, daha sonraki bir sürüme float olur.
* Bir paketin, PackageReference sürümü gereksinimleriyle eşleşen daha yeni bir sürümü yayımlandı. Örneğin 

  * 1. gün: `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` ancak NuGet depolarında kullanılabilen sürümler 4.1.0, 4.2.0 ve 4.3.0 olarak belirtilmiştir. Bu durumda, NuGet 4.1.0 (en yakın minimum sürüm) olarak çözümlenmelidir

  * 2. gün: sürüm 4.0.0 yayımlandı. NuGet artık tam eşleşmeyi bulacak ve 4.0.0 'e çözümlemeyi başlatacak

* Belirli bir paket sürümü depodan kaldırılır. Nuget.org, paket silmeleri için izin vermediği halde tüm paket depolarında bu kısıtlamalar yoktur. Bu, NuGet 'e, silinen sürüme çözümleyemediği zaman en iyi eşleşmeyi bulma sonucu verir.

### <a name="enabling-lock-file"></a>Kilit dosyası etkinleştiriliyor

Paket bağımlılıklarının tam kapatılmasını kalıcı hale getirmek için, projeniz için MSBuild özelliğini ayarlayarak dosya kilitle özelliğini kabul edebilirsiniz `RestorePackagesWithLockFile` :

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

Bu özellik ayarlandıysa, NuGet geri yükleme `packages.lock.json` Proje kök dizininde tüm paket bağımlılıklarını listeleyen bir kilit dosya dosyası oluşturacaktır. 

> [!Note]
> Bir projenin `packages.lock.json` kök dizininde dosyası varsa, özellik ayarlanmamışsa bile kilit dosyası her zaman restore ile birlikte kullanılır `RestorePackagesWithLockFile` . Bu nedenle, bu özelliği kabul etmenin başka bir yolu `packages.lock.json` da projenin kök dizininde kukla boş bir dosya oluşturmaktır.

### <a name="restore-behavior-with-lock-file"></a>`restore` kilit dosyası ile davranış
Proje için bir kilit dosyası varsa, NuGet bu kilit dosyasını çalıştırmak için kullanır `restore` . NuGet, paket bağımlılıklarında proje dosyasında (veya bağımlı proje dosyaları) bahsedildiği gibi herhangi bir değişiklik olup olmadığını görmek için hızlı bir denetim yapar ve değişiklik yapılmadığında yalnızca kilit dosyasında bahsedilen paketleri geri yükler. Paket bağımlılıklarının yeniden değerlendirilmesi yoktur.

NuGet, proje dosyasında bahsedildiği gibi tanımlanan bağımlılıklarda bir değişiklik algılarsa, paket grafiğini yeniden değerlendirir ve kilit dosyasını proje için yeni paket kapanışını yansıtacak şekilde güncelleştirir.

CI/CD ve diğer senaryolar için, anında paket bağımlılıklarını değiştirmek istemediğiniz için, ' yi ' e ayarlayarak bunu yapabilirsiniz `lockedmode` `true` :

dotnet.exe için şunu çalıştırın:

```
> dotnet.exe restore --locked-mode
```

msbuild.exe için şunu çalıştırın:

```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

Bu koşullu MSBuild özelliğini, proje dosyanızda de ayarlayabilirsiniz:

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

Kilitli mod ise geri yükleme işlemi, kilit `true` dosyası oluşturulduktan sonra, proje için tanımlanan paket bağımlılıklarını güncelleştirdikten sonra tam paketleri kilit dosyasında listelenen şekilde geri yükler ya da başarısız olur.

### <a name="make-lock-file-part-of-your-source-repository"></a>Kaynak deponuzun kilit dosyası parçasını oluşturma
Bir uygulama oluşturuyorsanız, bir çalıştırılabilir dosya ve söz konusu proje, bağımlılık zincirinin başlangıcında yer alıyorsa, NuGet 'in geri yükleme sırasında kullanabilmesi için kilit dosyasını kaynak kodu deposuna iade edin.

Ancak, projeniz sevk ettiğiniz bir kitaplık projem veya diğer projelerin bağımlı olduğu ortak bir kod projesi ise, kilit dosyasını kaynak kodunuzun bir parçası olarak iade etmeniz **gerekir** . Kilit dosyası tutulmayan bir sorun yoktur ancak ortak kod projesi için kilitli paket bağımlılıkları, bu ortak kod projesine bağlı bir projenin geri yükleme/oluşturma işlemi sırasında kilit dosyasında listelendiği gibi kullanılamaz.

Örn.

```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```

Bir `ProjectA` sürüme bağımlılığının yanı `PackageX` `2.0.0` sıra `ProjectB` sürüme bağlı olan başvurular varsa `PackageX` `1.0.0` , için kilit dosyası `ProjectB` sürüme bir bağımlılık listeleyecek `PackageX` `1.0.0` . Ancak, yapılandırıldığında `ProjectA` kilit dosyası, `PackageX` **`2.0.0`**  `1.0.0` için kilit dosyasında listelenenlerin değil, sürüm için bir bağımlılık içerecektir `ProjectB` . Bu nedenle, ortak bir kod projesinin kilit dosyası, kendisine bağımlı olan projeler için çözümlenen paketlerin üzerinde çok daha fazla bilgiye sahiptir.

### <a name="lock-file-extensibility"></a>Kilit dosyası genişletilebilirliği

Aşağıda açıklandığı gibi kilit dosyası ile geri yükleme davranışlarını çeşitli davranışlar için denetleyebilirsiniz:

| NuGet.exe seçeneği | DotNet seçeneği | MSBuild eşdeğer seçeneği | Açıklama |
|:--- |:--- |:--- |:--- |
| `-UseLockFile` |`--use-lock-file` | RestorePackagesWithLockFile | Bir kilit dosyasının kullanımıyla ilgili olarak. |
| `-LockedMode` | `--locked-mode` | RestoreLockedMode | Geri yükleme için kilitli modu etkinleştirilir. Bu, yinelenebilir derlemeler istediğiniz CI/CD senaryolarında kullanışlıdır.|   
| `-ForceEvaluate` | `--force-evaluate` | Restoreforcedeğerlendir | Bu seçenek, projede tanımlanmış kayan sürüme sahip paketlerle faydalıdır. Varsayılan olarak, NuGet geri yükleme, bu seçenekle geri yükleme çalıştırılmadığınız takdirde, her geri yükleme sırasında paket sürümünü otomatik olarak güncelleştirmez. |
| `-LockFilePath` | `--lock-file-path` | NuGetLockFilePath | Bir proje için özel bir kilit dosyası konumu tanımlar. Varsayılan olarak, NuGet `packages.lock.json` kök dizinde destekler. Aynı dizinde birden çok projeniz varsa, NuGet projeye özgü kilit dosyasını destekler `packages.<project_name>.lock.json` |
