---
title: NuGet PackageReference biçimi (proje dosyalarındaki paket başvuruları)
description: NuGet 4.0 + ve VS2017 ve .NET Core 2,0 tarafından desteklenen proje dosyalarında NuGet PackageReference ile ilgili ayrıntılar
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 892483760a9f3568da7101663e93c69ce3d70b96
ms.sourcegitcommit: 8a424829b1f70cf7590e95db61997af6ae2d7a41
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72510804"
---
# <a name="package-references-packagereference-in-project-files"></a>Proje dosyalarında paket başvuruları (PackageReference)

@No__t-0 düğümünü kullanarak paket başvuruları, NuGet bağımlılıklarını doğrudan proje dosyaları içinde yönetin (ayrı bir `packages.config` dosyasına karşılık). Çağrılan, PackageReference kullanarak NuGet 'in diğer yönlerini etkilemez; Örneğin, `NuGet.config` dosyalarındaki (paket kaynakları dahil) ayarlar, [ortak NuGet yapılandırmalarında](configuring-nuget-behavior.md)açıklandığı gibi hala uygulanır.

PackageReference ile, MSBuild koşullarını hedef çerçeve, yapılandırma, platform veya diğer gruplandırmalar için paket başvuruları seçmek üzere de kullanabilirsiniz. Ayrıca bağımlılıklar ve içerik akışı üzerinde ayrıntılı denetim sağlar. (Daha fazla ayrıntı Için bkz. [NuGet paketi ve geri yükleme MSBuild hedefleri olarak](../reference/msbuild-targets.md).)

## <a name="project-type-support"></a>Proje türü desteği

Varsayılan olarak, PackageReference, .NET Core projeleri, .NET Standard projeleri ve Windows 10 Build 15063 (Creators Update) ve üstünü hedefleyen UWP projeleri için, C++ UWP projelerinin dışında kullanılır. .NET Framework projeler, PackageReference destekler, ancak şu anda varsayılan olarak `packages.config` ' dır. PackageReference kullanmak için, `packages.config` ' den bağımlılıkları proje dosyanıza [geçirin](../consume-packages/migrate-packages-config-to-package-reference.md) , sonra Packages. config ' i kaldırın.

Tam .NET Framework hedefleyen uygulamalar, PackageReference için yalnızca [sınırlı desteği](https://github.com/NuGet/Home/issues/5877) içerir. C++ve JavaScript proje türleri desteklenmez.

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

Bir paketin sürümünü belirtme kuralı, @no__t kullanırken olduğu gibi,-0:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

Yukarıdaki örnekte 3.6.0, [paket sürümü oluşturma](../concepts/package-versioning.md#version-ranges-and-wildcards)bölümünde açıklandığı gibi en düşük sürüm için tercihe sahip > = 3.6.0 olan herhangi bir sürüm anlamına gelir.

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a>Packagereferde olmayan bir proje için PackageReference kullanma
Gelişmiş: bir projede yüklü paketleriniz yoksa (proje dosyasında ve paket. config dosyası yoksa), ancak projenin PackageReference stili olarak geri yüklenmesini istiyorsanız, bir proje özelliği RestoreProjectStyle ' ı PackageReference olarak ayarlayabilirsiniz. Proje dosyanız.
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
Bu, PackageReference stilli (mevcut csproj veya SDK stili projeler) projelere başvuru yaparsanız yararlı olabilir. Bu, bu projelerin başvurduğu paketleri projeniz tarafından "geçişli" olacak şekilde sağlayacak şekilde etkinleştirir.

## <a name="floating-versions"></a>Kayan sürümler

[Kayan sürümler](../concepts/dependency-resolution.md#floating-versions) `PackageReference` ile desteklenir:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a>Bağımlılık varlıklarını denetleme

Yalnızca bir geliştirme bandı olarak bir bağımlılık kullanıyor olabilirsiniz ve bunu paketinizi kullanacak projelere göstermek istemeyebilirsiniz. Bu senaryoda, bu davranışı denetlemek için `PrivateAssets` meta verilerini kullanabilirsiniz.

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

| Etiket | Açıklama | Varsayılan Değer |
| --- | --- | --- |
| Includevarlıklarını | Bu varlıklar tüketilecektir | tüm |
| Excludevarlıklarının | Bu varlıklar tüketilmeyecek | yok |
| Privatevarlıkların | Bu varlıklar tüketilecektir, ancak üst projeye akamaz | ContentFiles; çözümleyiciler; derleme |

Bu etiketler için izin verilen değerler, `all` ve `none` dışında noktalı virgülle ayrılmış birden çok değer olan aşağıdaki gibidir:

| Değer | Açıklama |
| --- | ---
| Se | @No__t-0 klasörünün içeriği ve projenizin, klasör içindeki derlemelere göre derleyemeyeceğini denetler |
| çalışma zamanı | @No__t-0 ve `runtimes` klasörünün içeriği ve bu derlemelerin derleme çıkış dizinine kopyalanıp kopyalanmayacağını denetler |
| contentFiles | @No__t-0 klasörünün içeriği |
| derleme | `.props` ve `.targets` `build` klasöründe |
| Buildmultihedefleme | *(4,0)* `.props` ve `.targets` `buildMultitargeting` klasöründe, platformlar arası hedefleme için |
| buildTransitive | *(5.0 +)* `.props` ve `.targets` `buildTransitive` klasöründe, her bir tüketen projeye geçişli olarak akan varlıklar içindir. Bkz. [özellik](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) sayfası. |
| Çözümleyicileri | .NET Çözümleyicileri |
| yerel | @No__t-0 klasörünün içeriği |
| yok | Yukarıdakilerin hiçbiri kullanılmaz. |
| tüm | Yukarıdakilerin tümü (`none` dışında) |

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

@No__t-0 `PrivateAssets` ' e dahil edilmediğinden, hedeflerin *ve props üst projeye akacağından emin* olmak. Örneğin, yukarıdaki başvurunun Appgünlükçü adlı bir NuGet paketi oluşturan bir projede kullanıldığını göz önünde bulundurun. Appgünlükçü, Appgünlükçü kullanan projeler gibi `Contoso.Utility.UsefulStuff` ' dan hedefleri ve props 'ı kullanabilir.

> [!NOTE]
> @No__t-0 ' ı bir `.nuspec` dosyasında `true` olarak ayarlandığında, bu bir paketi yalnızca geliştirme bağımlılığı olarak işaretler, bu da paketin diğer paketlere bağımlılık olarak eklenmesini önler. PackageReference *(NuGet 4.8 +)* ile bu bayrak Ayrıca derleme zamanı varlıklarını derlemeden dışlayacak anlamına gelir. Daha fazla bilgi için bkz. [PackageReference Için Developmentdependency desteği](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).

## <a name="adding-a-packagereference-condition"></a>PackageReference koşulu ekleme

Bir paketin dahil edilip edilmeyeceğini denetlemek için bir koşul kullanabilirsiniz. burada koşullar herhangi bir MSBuild değişkeni veya hedefler veya props dosyasında tanımlanan bir değişken kullanabilir. Ancak şu anda yalnızca `TargetFramework` değişkeni desteklenir.

Örneğin, `netstandard1.4` ' ı ve `net452` ' i hedeflediğiniz, ancak yalnızca `net452` için geçerli olan bir bağımlılığa sahip olduğunuzu varsayalım. Bu durumda, bu gereksiz bağımlılığı eklemek için paketinizi kullanan `netstandard1.4` projesi istemezsiniz. Bunu engellemek için `PackageReference` ' da aşağıdaki şekilde bir koşul belirtirsiniz:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

Bu proje kullanılarak oluşturulan bir paket, Newtonsoft. json ' ın yalnızca bir `net452` hedefi için bağımlılık olarak ekleneceğini gösterir:

![VS2017 ile PackageReference üzerinde koşul uygulamanın sonucu](media/PackageReference-Condition.png)

Koşullar `ItemGroup` düzeyinde de uygulanabilir ve tüm alt `PackageReference` öğeleri için geçerli olur:

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="locking-dependencies"></a>Bağımlılıkları kilitleme
*Bu özellik NuGet **4,9** veya sonraki sürümlerde ve Visual Studio 2017 **15,9** veya üzeri sürümlerde kullanılabilir.*

NuGet geri yükleme girdisi, proje dosyasından (en üst düzey veya doğrudan bağımlılıklar) paket başvuruları kümesidir ve çıkış geçişli bağımlılıklar dahil olmak üzere tüm paket bağımlılıklarının tam bir kapasitesinden oluşur. NuGet, giriş PackageReference listesi değişmediğinde paket bağımlılıklarının her zaman aynı tam kapatılmasını üretmeye çalışır. Ancak, bunu yapamaması gereken bazı senaryolar vardır. Örneğin:

* @No__t-0 gibi kayan sürümler kullandığınızda. Buradaki amaç paketlerin her geri yükleme işlemi için en son sürüme kaymalıdır, ancak kullanıcıların grafiğin belirli bir en son sürüme kilitlenmesini gerektiren senaryolar vardır ve açık bir hareket üzerine varsa, daha sonraki bir sürüme float olur.
* Bir paketin, PackageReference sürümü gereksinimleriyle eşleşen daha yeni bir sürümü yayımlandı. DomainName. 

  * 1\. gün: `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` belirttiyseniz, ancak NuGet depolarında bulunan sürümler 4.1.0, 4.2.0 ve 4.3.0 olarak belirtilmiştir. Bu durumda, NuGet 4.1.0 (en yakın minimum sürüm) olarak çözümlenmelidir

  * 2\. gün: sürüm 4.0.0 yayımlandı. NuGet artık tam eşleşmeyi bulacak ve 4.0.0 'e çözümlemeyi başlatacak

* Belirli bir paket sürümü depodan kaldırılır. Nuget.org, paket silmeleri için izin vermediği halde tüm paket depolarında bu kısıtlamalar yoktur. Bu, NuGet 'e, silinen sürüme çözümleyemediği zaman en iyi eşleşmeyi bulma sonucu verir.

### <a name="enabling-lock-file"></a>Kilit dosyası etkinleştiriliyor
Paket bağımlılıklarının tam kapatılmasını sürdürmek için, projeniz için `RestorePackagesWithLockFile` MSBuild özelliğini ayarlayarak dosya kilitle özelliğini kabul edebilirsiniz:

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

Bu özellik ayarlandıysa, NuGet geri yükleme proje kök dizininde tüm paket bağımlılıklarını listeleyen bir kilit dosyası-`packages.lock.json` dosyası oluşturacaktır. 

> [!Note]
> Bir projede kök dizininde `packages.lock.json` dosyası varsa, `RestorePackagesWithLockFile` özelliği ayarlanmamışsa bile kilit dosyası her zaman restore ile birlikte kullanılır. Bu nedenle, bu özelliği kabul etmenin başka bir yolu da projenin kök dizininde kukla bir boş `packages.lock.json` dosyası oluşturmaktır.

### <a name="restore-behavior-with-lock-file"></a>kilit dosyası ile 0 @no__t davranışı
Proje için bir kilit dosyası varsa, NuGet bu kilit dosyasını `restore` ' ı çalıştırmak için kullanır. NuGet, paket bağımlılıklarında proje dosyasında (veya bağımlı proje dosyaları) bahsedildiği gibi herhangi bir değişiklik olup olmadığını görmek için hızlı bir denetim yapar ve değişiklik yapılmadığında yalnızca kilit dosyasında bahsedilen paketleri geri yükler. Paket bağımlılıklarının yeniden değerlendirilmesi yoktur.

NuGet, proje dosyasında bahsedildiği gibi tanımlanan bağımlılıklarda bir değişiklik algılarsa, paket grafiğini yeniden değerlendirir ve kilit dosyasını proje için yeni paket kapanışını yansıtacak şekilde güncelleştirir.

CI/CD ve diğer senaryolar için, anında paket bağımlılıklarını değiştirmek istemediğiniz durumlarda `lockedmode` ' ı `true` ' e ayarlayarak bunu yapabilirsiniz:

DotNet. exe için şunu çalıştırın:
```
> dotnet.exe restore --locked-mode
```

MSBuild. exe için şunu çalıştırın:
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

Kilitli mod `true` ise, geri yükleme işlemi kilit dosyasında listelenen paketleri tam olarak geri yükler veya kilit dosyası oluşturulduktan sonra proje için tanımlanan paket bağımlılıklarını güncelleştirdiyseniz başarısız olur.

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
@No__t-0 ' a bir `PackageX` sürümü `2.0.0` ' ye bağımlıysa ve aynı zamanda `PackageX` sürümüne `1.0.0` ' e bağlı `ProjectB` ' e başvuruyorsa, `ProjectB` için kilit dosyası `PackageX` sürümüne bir bağımlılık listeleyecek `1.0.0`. Ancak, `ProjectA` yapılandırıldığında, kilit dosyası @no__t- **3 sürümü `2.0.0`** ' te bir bağımlılık içerir ve `ProjectB` için kilit dosyasında listelenen `1.0.0` **değildir** . Bu nedenle, ortak bir kod projesinin kilit dosyası, kendisine bağımlı olan projeler için çözümlenen paketlerin üzerinde çok daha fazla bilgiye sahiptir.

### <a name="lock-file-extensibility"></a>Kilit dosyası genişletilebilirliği

Aşağıda açıklandığı gibi kilit dosyası ile geri yükleme davranışlarını çeşitli davranışlar için denetleyebilirsiniz:

| Seçenek | MSBuild eşdeğer seçeneği | Açıklama|
|:---  |:--- |:--- |
| `--use-lock-file` | RestorePackagesWithLockFile | Bir kilit dosyasının kullanımıyla ilgili olarak. | 
| `--locked-mode` | RestoreLockedMode | Geri yükleme için kilitli modu etkinleştirilir. Bu, yinelenebilir derlemeler istediğiniz CI/CD senaryolarında kullanışlıdır.|   
| `--force-evaluate` | Restoreforcedeğerlendir | Bu seçenek, projede tanımlanmış kayan sürüme sahip paketlerle faydalıdır. Varsayılan olarak, NuGet geri yükleme, bu seçenekle geri yükleme çalıştırılmadığınız takdirde, her geri yükleme sırasında paket sürümünü otomatik olarak güncelleştirmez. |
| `--lock-file-path` | NuGetLockFilePath | Bir proje için özel bir kilit dosyası konumu tanımlar. Varsayılan olarak, NuGet kök dizinde `packages.lock.json` ' ı destekler. Aynı dizinde birden çok projeniz varsa, NuGet projeye özgü kilit dosyası @no__t destekler-0 |
