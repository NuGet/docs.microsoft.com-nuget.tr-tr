---
title: NuGet PackageReference biçimi (proje dosyalarındaki paket başvuruları)
description: NuGet 4.0 + ve VS2017 ve .NET Core 2,0 tarafından desteklenen proje dosyalarında NuGet PackageReference ile ilgili ayrıntılar
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 05ece5f36ff7ae5920960c42cfde8b271dc3e712
ms.sourcegitcommit: fc1b716afda999148eb06d62beedb350643eb346
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69020007"
---
# <a name="package-references-packagereference-in-project-files"></a>Proje dosyalarında paket başvuruları (PackageReference)

Paket başvuruları, `PackageReference` düğümü kullanarak, NuGet bağımlılıklarını doğrudan proje dosyaları içinde (ayrı `packages.config` bir dosyanın aksine) yönetir. Çağrılan, PackageReference kullanarak NuGet 'in diğer yönlerini etkilemez; Örneğin, `NuGet.config` dosyalardaki (paket kaynakları dahil) ayarlar, [ortak NuGet yapılandırmalarında](configuring-nuget-behavior.md)açıklandığı gibi hala uygulanır.

PackageReference ile, MSBuild koşullarını hedef çerçeve, yapılandırma, platform veya diğer gruplandırmalar için paket başvuruları seçmek üzere de kullanabilirsiniz. Ayrıca bağımlılıklar ve içerik akışı üzerinde ayrıntılı denetim sağlar. (Daha fazla ayrıntı Için bkz. [NuGet paketi ve geri yükleme MSBuild hedefleri olarak](../reference/msbuild-targets.md).)

## <a name="project-type-support"></a>Proje türü desteği

Varsayılan olarak, PackageReference, .NET Core projeleri, .NET Standard projeleri ve Windows 10 Build 15063 (Creators Update) ve üstünü hedefleyen UWP projeleri için, C++ UWP projelerinin dışında kullanılır. .NET Framework projeler, PackageReference destekler, ancak şu anda `packages.config`varsayılan olarak. Packagereference kullanmak için, [](../reference/migrate-packages-config-to-package-reference.md) bağımlılıkları `packages.config` proje dosyanıza geçirin, sonra Packages. config 'i kaldırın.

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

Bir paketin sürümünü belirtme kuralı, kullanırken `packages.config`olduğu gibi aynıdır:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

Yukarıdaki örnekte 3.6.0, [paket sürümü oluşturma](../reference/package-versioning.md#version-ranges-and-wildcards)bölümünde açıklandığı gibi en düşük sürüm için tercihe sahip > = 3.6.0 olan herhangi bir sürüm anlamına gelir.

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a>Packagereferde olmayan bir proje için PackageReference kullanma
İleri Bir projede yüklü paketleriniz yoksa (proje dosyasında ve hiçbir paket. config dosyası yoksa), ancak projenin PackageReference stili olarak geri yüklenmesini istiyorsanız, bir proje özelliği RestoreProjectStyle öğesini projenizde PackageReference olarak ayarlayabilirsiniz dosyasýný.
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
Bu, PackageReference stilli (mevcut csproj veya SDK stili projeler) projelere başvuru yaparsanız yararlı olabilir. Bu, bu projelerin başvurduğu paketleri projeniz tarafından "geçişli" olacak şekilde sağlayacak şekilde etkinleştirir.

## <a name="floating-versions"></a>Kayan sürümler

[Kayan sürümler](../consume-packages/dependency-resolution.md#floating-versions) ile `PackageReference`desteklenir:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a>Bağımlılık varlıklarını denetleme

Yalnızca bir geliştirme bandı olarak bir bağımlılık kullanıyor olabilirsiniz ve bunu paketinizi kullanacak projelere göstermek istemeyebilirsiniz. Bu senaryoda, bu davranışı denetlemek için `PrivateAssets` meta verileri kullanabilirsiniz.

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

Bu etiketler için izin verilen değerler aşağıdaki gibidir: ile `all` , ve arasında bir noktalı virgülle ayrılmış birden çok değer ve `none` kendileri tarafından görünmesi gerekir:

| Değer | Açıklama |
| --- | ---
| se | `lib` Klasörün içeriği ve projenizin içindeki derlemelere göre derleyemeyeceğini denetler |
| çalışma zamanı | `lib` Ve`runtimes` klasörünün içeriği ve bu derlemelerin derleme çıkış dizinine kopyalanıp kopyalanmayacağını denetler |
| contentFiles | `contentfiles` Klasörün içeriği |
| derleme | `.props`ve `.targets` klasörü`build` |
| Buildmultihedefleme | `.props`ve `.targets`klasöründe,platformlar arasıhedeflemeiçin`buildMultitargeting` |
| buildTransitive | *(5.0 +)* `.props` ve`.targets` klasörü, her bir tüketen projeye geçişli olarak akan varlıklar içindir. `buildTransitive` Bkz. [özellik](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) sayfası. |
| Çözümleyicileri | .NET Çözümleyicileri |
| yerel | `native` Klasörün içeriği |
| yok | Yukarıdakilerin hiçbiri kullanılmaz. |
| tüm | Yukarıdakilerin tümü (hariç `none`) |

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

İle `build` birlikte`PrivateAssets`dahil edilmediğinden, hedefler ve props ana projeye akacağından emin olmanız gerekir. Örneğin, yukarıdaki başvurunun Appgünlükçü adlı bir NuGet paketi oluşturan bir projede kullanıldığını göz önünde bulundurun. Appgünlükçü, appgünlükçü kullanan projeler gibi, `Contoso.Utility.UsefulStuff`öğesinden hedefleri ve props 'ı kullanabilir.

## <a name="adding-a-packagereference-condition"></a>PackageReference koşulu ekleme

Bir paketin dahil edilip edilmeyeceğini denetlemek için bir koşul kullanabilirsiniz. burada koşullar herhangi bir MSBuild değişkeni veya hedefler veya props dosyasında tanımlanan bir değişken kullanabilir. Ancak şu anda yalnızca `TargetFramework` değişken desteklenir.

Örneğin, hedeflentiğinizi `netstandard1.4` `net452` ve yalnızca için `net452`geçerli olan bir bağımlılığa sahip olduğunuzu varsayalım. Bu durumda, paketinize tüketen bir `netstandard1.4` projenin bu gereksiz bağımlılığı eklemesini istemezsiniz. Bunu engellemek için aşağıdaki `PackageReference` şekilde bir koşul belirtirsiniz:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

Bu proje kullanılarak oluşturulan bir paket, Newtonsoft. json ' ın yalnızca bir `net452` hedef için bağımlılık olarak ekleneceğini gösterir:

![VS2017 ile PackageReference üzerinde koşul uygulamanın sonucu](media/PackageReference-Condition.png)

Koşullar da `ItemGroup` düzeyde uygulanabilir ve tüm alt `PackageReference` öğeler için geçerli olacaktır:

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

* Gibi `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`kayan sürümler kullandığınızda. Buradaki amaç paketlerin her geri yükleme işlemi için en son sürüme kaymalıdır, ancak kullanıcıların grafiğin belirli bir en son sürüme kilitlenmesini gerektiren senaryolar vardır ve açık bir hareket üzerine varsa, daha sonraki bir sürüme float olur.
* Bir paketin, PackageReference sürümü gereksinimleriyle eşleşen daha yeni bir sürümü yayımlandı. Örneğin 

  * 1\. gün: ancak NuGet `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` depolarında kullanılabilen sürümler 4.1.0, 4.2.0 ve 4.3.0 olarak belirtilmiştir. Bu durumda, NuGet 4.1.0 (en yakın minimum sürüm) olarak çözümlenmelidir

  * Gün 2: Sürüm 4.0.0 yayımlandı. NuGet artık tam eşleşmeyi bulacak ve 4.0.0 'e çözümlemeyi başlatacak

* Belirli bir paket sürümü depodan kaldırılır. Nuget.org, paket silmeleri için izin vermediği halde tüm paket depolarında bu kısıtlamalar yoktur. Bu, NuGet 'e, silinen sürüme çözümleyemediği zaman en iyi eşleşmeyi bulma sonucu verir.

### <a name="enabling-lock-file"></a>Kilit dosyası etkinleştiriliyor
Paket bağımlılıklarının tam kapatılmasını kalıcı hale getirmek için, projeniz için MSBuild özelliğini `RestorePackagesWithLockFile` ayarlayarak dosya kilitle özelliğini kabul edebilirsiniz:

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

Bu özellik ayarlandıysa, NuGet geri yükleme proje kök dizininde tüm paket bağımlılıklarını listeleyen `packages.lock.json` bir kilit dosya dosyası oluşturacaktır. 

> [!Note]
> Bir projenin kök dizininde `packages.lock.json` dosyası varsa, özellik `RestorePackagesWithLockFile` ayarlanmamışsa bile kilit dosyası her zaman restore ile birlikte kullanılır. Bu nedenle, bu özelliği kabul etmenin başka bir yolu da projenin kök dizininde kukla boş `packages.lock.json` bir dosya oluşturmaktır.

### <a name="restore-behavior-with-lock-file"></a>`restore`kilit dosyası ile davranış
Proje için bir kilit dosyası varsa, NuGet bu kilit dosyasını çalıştırmak `restore`için kullanır. NuGet, paket bağımlılıklarında proje dosyasında (veya bağımlı proje dosyaları) bahsedildiği gibi herhangi bir değişiklik olup olmadığını görmek için hızlı bir denetim yapar ve değişiklik yapılmadığında yalnızca kilit dosyasında bahsedilen paketleri geri yükler. Paket bağımlılıklarının yeniden değerlendirilmesi yoktur.

NuGet, proje dosyasında bahsedildiği gibi tanımlanan bağımlılıklarda bir değişiklik algılarsa, paket grafiğini yeniden değerlendirir ve kilit dosyasını proje için yeni paket kapanışını yansıtacak şekilde güncelleştirir.

CI/CD ve diğer senaryolar için, anında paket bağımlılıklarını değiştirmek istemediğiniz için, ' yi ' `lockedmode` e `true`ayarlayarak bunu yapabilirsiniz:

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

Kilitli mod ise `true`geri yükleme işlemi, kilit dosyası oluşturulduktan sonra, proje için tanımlanan paket bağımlılıklarını güncelleştirdikten sonra tam paketleri kilit dosyasında listelenen şekilde geri yükler ya da başarısız olur.

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
Bir `ProjectA` `PackageX` sürüme bağımlılığının`ProjectB` yanı sıra `ProjectB` `PackageX` sürüme bağlı`1.0.0`olan başvurular varsa, için kilit dosyası şuna bir bağımlılık listeleyecek `PackageX` `2.0.0` Sürüm `1.0.0`. Ancak, `ProjectA` yapılandırıldığında kilit dosyası, için kilit dosyasında listelenenlerin **değil** `1.0.0` , `PackageX` sürüm **`2.0.0`** için `ProjectB`bir bağımlılık içerecektir. Bu nedenle, ortak bir kod projesinin kilit dosyası, kendisine bağımlı olan projeler için çözümlenen paketlerin üzerinde çok daha fazla bilgiye sahiptir.

### <a name="lock-file-extensibility"></a>Kilit dosyası genişletilebilirliği
Aşağıda açıklandığı gibi kilit dosyası ile geri yükleme davranışlarını çeşitli davranışlar için denetleyebilirsiniz:

| Seçenek | MSBuild eşdeğer seçeneği | 
|:---  |:--- |
| `--use-lock-file` | Önyükleme bir proje için kilit dosyası kullanımı. Alternatif olarak proje dosyasında `RestorePackagesWithLockFile` özelliği ayarlayabilirsiniz | 
| `--locked-mode` | Geri yükleme için kilitli modu etkinleştirilir. Bu, yinelenebilir derlemeleri almak istediğiniz CI/CD senaryolarında yararlıdır. Bu, `RestoreLockedMode` MSBuild özelliğinin ' i olarak ayarlanmasına de izin verebilir`true` |  
| `--force-evaluate` | Bu seçenek, projede tanımlanmış kayan sürüme sahip paketlerle faydalıdır. Varsayılan olarak, geri yükle seçeneğini birlikte `--force-evaluate` çalıştırmadığınız takdirde NuGet geri yükleme, her geri yükleme sırasında paket sürümünü otomatik olarak güncelleştirmez. |
| `--lock-file-path` | Bir proje için özel bir kilit dosyası konumu tanımlar. Bu, MSBuild özelliği `NuGetLockFilePath`ayarlanarak da elde edilebilir. Varsayılan olarak, NuGet kök `packages.lock.json` dizinde destekler. Aynı dizinde birden çok projeniz varsa, NuGet projeye özgü kilit dosyasını destekler`packages.<project_name>.lock.json` |
