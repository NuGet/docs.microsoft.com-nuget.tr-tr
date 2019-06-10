---
title: NuGet Packagereference'a biçimi (proje dosyalarında paket başvuruları)
description: NuGet 4.0 + ve VS2017 ve .NET Core 2.0 tarafından desteklenen proje dosyalarında NuGet PackageReference hakkında ayrıntılar
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: c2dfce8de6b28aaee99e3d5ab75cd28950a8cb0f
ms.sourcegitcommit: b8c63744252a5a37a2843f6bc1d5917496ee40dd
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812845"
---
# <a name="package-references-packagereference-in-project-files"></a>Proje dosyalarında paket başvuruları (PackageReference)

Paket başvuruları kullanılarak, `PackageReference` düğümü, NuGet bağımlılıklarını doğrudan proje dosyaları içinde yönetme (ayrı bir aksine `packages.config` dosya). PackageReference, kullanarak çağrılır, NuGet diğer yönleri etkilemez; Örneğin, ayarlarında `NuGet.config` (paket kaynaklarını dahil) dosyaları yine de açıklandığı gibi uygulanan [NuGet davranışını yapılandırma](configuring-nuget-behavior.md).

PackageReference ile paket başvuruları her hedef çerçeve, yapılandırma, platform veya diğer grupları seçmek için MSBuild koşulları kullanabilirsiniz. Ayrıca bağımlılıkları ve içerik akışı üzerinde ayrıntılı denetim sağlar. (Daha fazla ayrıntı için [NuGet paketi ve geri yükleme, MSBuild hedefleri](../reference/msbuild-targets.md).)

## <a name="project-type-support"></a>Proje türü desteği

Varsayılan olarak, .NET Core projeleri, .NET Standard projelerine ve Windows 10 derleme 15063 (Creators Update) hedefleyen UWP projeleri için ve sonraki sürümlerinde, C++ UWP projeleri hariç PackageReference kullanılır. .NET framework projeleri PackageReference destekler, ancak şu anda varsayılan `packages.config`. PackageReference, kullanılacak [geçirme](../reference/migrate-packages-config-to-package-reference.md) bağımlılıklardan `packages.config` proje dosyanıza ardından packages.config kaldırın.

.NET Framework'ün tamamını hedefleyen ASP.NET uygulamaları dahil yalnızca [sınırlı destek](https://github.com/NuGet/Home/issues/5877) PackageReference için. C++ve JavaScript proje türleri desteklenmez.

## <a name="adding-a-packagereference"></a>PackageReference ekleme

Bir bağımlılık aşağıdaki sözdizimini kullanarak proje dosyanıza ekleyin:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a>Bağımlılık sürümünü denetleme

Bir paketin sürümü belirtmek için kural aynı kullanıldığında `packages.config`:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

Yukarıdaki örnekte, 3.6.0 olan herhangi bir sürümü anlamına gelir > üzerinde açıklandığı 3.6.0 tercih en düşük sürümü ile = [Paket sürümü oluşturma](../reference/package-versioning.md#version-ranges-and-wildcards).

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a>Hiçbir packagereferences'ı içeren bir proje için PackageReference kullanma
Gelişmiş: Artık paketler, bir projede (proje dosyasında hiçbir PackageReferences) ve hiçbir packages.config dosyası yüklü olan, ancak projesi stili Packagereference'a geri yüklenmesini istiyorsanız, projenizde bir proje özelliğini RestoreProjectStyle Packagereference'a ayarlayabilirsiniz dosya.
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
(Mevcut csproj veya SDK stili projeleri) stili Packagereference'a olan projeleri başvuruyorsa yararlı olabilir. Bu projelerdeki "geçişli" projeniz tarafından başvurulabilmesi için başvuran paketleri olanak sağlar.

## <a name="floating-versions"></a>Kayan sürümleri

[Kayan sürümleri](../consume-packages/dependency-resolution.md#floating-versions) ile desteklenen `PackageReference`:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a>Bağımlılık varlıkları denetleme

Bir bağımlılık yalnızca bir geliştirme bandı kullanabilecek ve, paketiniz tüketecektir projeler için kullanıma sunmak istemeyebilirsiniz. Bu senaryoda kullanabileceğiniz `PrivateAssets` bu davranışını denetlemek için meta verileri.

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

Şu meta veri etiketleri bağımlılık varlıklar kontrol edin:

| Etiket | Açıklama | Varsayılan Değer |
| --- | --- | --- |
| IncludeAssets | Bu varlıklar tarafından kullanılabilir | tüm |
| ExcludeAssets | Bu varlıklar tüketilir değil | yok |
| PrivateAssets | Bu varlıklar tarafından kullanılabilir ancak üst projeye akış olmaz | contentfiles, çözümleyiciler; derleme |

Bu etiketler için izin verilen değerler aşağıdaki gibidir, dışında noktalı virgül ile ayırarak birden çok değer ile `all` ve `none` gerekir göründüğü başlarına:

| Değer | Açıklama |
| --- | ---
| Derleme | İçeriğini `lib` klasörü ve denetimleri klasördeki derlemelere karşı olup projenizi derleyin |
| çalışma zamanı | İçeriğini `lib` ve `runtimes` klasörü ve denetimleri bu derlemeler için derleme olup kopyalanacak çıktı dizini |
| contentFiles | İçeriğini `contentfiles` klasörü |
| derleme | Özellikler ve hedeflediğini `build` klasörü |
| Çözümleyiciler | .NET çözümleyiciler |
| yerel | İçeriğini `native` klasörü |
| yok | Yukarıdakilerin hiçbiri kullanılır. |
| tüm | Yukarıdakilerin tümü (dışında `none`) |

Aşağıdaki örnekte, içerik dosyalarını paketinden dışında her şeyi proje tarafından tüketilen ve içerik dosyaları ve çözümleyiciler dışında her şeyi üst projeye akış.

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

Dikkat edin çünkü `build` ile bulunmaz `PrivateAssets`, hedeflerini ve özellik *olur* üst projeye akış. Örneğin, yukarıdaki başvuru AppLogger adlı bir NuGet paketi oluşturan bir projesinde kullanıldığını düşünün. AppLogger hedeflerini ve özellik gelen kullanabileceği `Contoso.Utility.UsefulStuff`, AppLogger kullanan projeler gibi.

## <a name="adding-a-packagereference-condition"></a>PackageReference koşul ekleme

Koşullar herhangi bir MSBuild değişken kullanabilirsiniz veya bir değişkeni hedefler ya da Özellikler dosyasında tanımlanan bir paket dahil olup olmadığını denetlemek için bir koşul kullanabilirsiniz. Ancak, şu anda, yalnızca `TargetFramework` değişkeni desteklenir.

Örneğin, hedefleyen düşünelim `netstandard1.4` yanı `net452` ancak yalnızca için geçerli olan bir bağımlılığa sahip `net452`. Bu durumda istemediğiniz bir `netstandard1.4` paketiniz, gereksiz bağımlılık eklemek için kullanan bir proje. Bunu önlemek için bir koşul belirttiğiniz `PackageReference` gibi:

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

Bu proje kullanılarak oluşturulan bir paket Newtonsoft.Json yalnızca bağımlılık olarak dahil olduğunu gösterir bir `net452` hedef:

![Bir koşul ile VS2017 PackageReference üzerinde sonucu](media/PackageReference-Condition.png)

Koşul da uygulanabilir `ItemGroup` düzeyi ve tüm alt öğelere uygulanacak `PackageReference` öğeleri:

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="locking-dependencies"></a>Kilitleme bağımlılıkları
*Bu özellik, NuGet ile kullanılabilir **4.9** veya yukarıda ve Visual Studio 2017 ile **15.9** veya üzeri.*

Giriş olarak NuGet geri yükleme, paket başvurularının proje dosyası (üst düzey veya doğrudan bağımlılıkları) kümesidir ve tam bir kapanış geçişli bağımlılıklar dahil olmak üzere tüm paket bağımlılıklarının çıkış alınır. NuGet Packagereference'a listesi girişi değiştirilmediyse her zaman paket bağımlılıklarının aynı tam kapatma üretmek çalışır. Ancak, bunu yapmanız mümkün olduğu bazı senaryolar vardır. Örneğin:

* Kayan kullandığınızda sürümleri ister `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`. Burada amaç, her geri yükleme paketlerinin en son sürüme kaydırmak için olsa da burada kullanıcıların grafiğin belirli en son sürümü ve sonraki bir sürüme kayan nokta varsa, açık bir hareket üzerine kilitlenmesine gerektiren senaryolar vardır.
* Paket eşleşen PackageReference sürüm gereksinimleri daha yeni bir sürümü yayımlandı. Örneğin 

  * 1. günü: belirttiyseniz `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` ancak NuGet depolarda sürüm 4.1.0, 4.2.0 ve 4.3.0 olmuştur. Bu durumda, NuGet (en yakın en düşük sürüm) 4.1.0 çözümlendi

  * 2. gün: Sürüm 4.0.0 yayımlanan. NuGet şimdi tam eşleşme bulmak ve 4.0.0 için çözülmeye başlanacağı

* Belirtilen Paket sürümü depodan kaldırılır. Tüm paket depolarınızın nuget.org paket silme izin vermez ancak bu bir kısıtlama söz konusu. En iyi eşleşen silinen sürümüne çözümleyemediğinde bulma NuGet sonuçlanır.

### <a name="enabling-lock-file"></a>Etkinleştirme kilidi dosyası
Tam kapatma, kabul etme kilidi dosya özelliğini MSBuild özelliğini ayarlayarak paket bağımlılıklarının kalıcı hale getirmek için `RestorePackagesWithLockFile` projeniz için:

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

Bu özelliği ayarlarsanız, NuGet geri yükleme bir kilit dosyası - oluşturur `packages.lock.json` dosya proje kök dizininde tüm paket bağımlılıkları listeler. 

> [!Note]
> Bir proje olduğunda `packages.lock.json` kök dizinde, kilit dosyanın dosyasındadır her zaman özelliği geri yükleme bile ile kullanılan `RestorePackagesWithLockFile` ayarlı değil. İşlevsiz bir boş oluşturmak için kabul etmek için bu özellik için başka bir yolu, bu nedenle `packages.lock.json` proje kök dizinine dosyasında.

### <a name="restore-behavior-with-lock-file"></a>`restore` Kilit dosyasıyla davranışı
Proje için bir kilit dosyası varsa, NuGet bu kilit dosyasını çalıştırmak için kullanır. `restore`. NuGet Paket bağımlılıklarını proje dosyası (veya bağımlı proje dosyalarının) belirtildiği gibi herhangi bir değişiklik yoktu ve herhangi bir değişiklik varsa, yalnızca kilit dosyasında belirtilen paketleri geri yükler görmek için hızlı bir denetimi yapar. Hiçbir Paket bağımlılıklarını değerlendirmeleri yoktur.

Proje dosyasında belirtildiği gibi bir değişiklik NuGet içinde tanımlanan bağımlılıklar algılar, paket grafiği yeniden değerlendirir ve kilit dosyası proje için yeni paket kapanış yansıtacak şekilde güncelleştirir.

CI/CD ve değil istediğiniz paket bağımlılıklarını hareket halindeyken değiştirmek için diğer senaryolar için ayarlayarak bunu yapabilirsiniz `lockedmode` için `true`:

DotNet.exe için çalıştırın:
```
> dotnet.exe restore --locked-mode
```

MSBuild.exe için çalıştırın:
```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

Ayrıca, proje dosyanızda koşullu bu MSBuild özelliği ayarlayabilir:
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

Kilitli modda ise `true`, geri yükleme ya da kilit dosyasında listelenen tam paketler geri veya proje için tanımlanmış Paket bağımlılıklarını kilit dosyası oluşturulduktan sonra güncelleştirdiyseniz başarısız.

### <a name="make-lock-file-part-of-your-source-repository"></a>Kilit dosya kaynak deponuza parçası olun
NuGet yapabilmeleri için yürütülebilir bir uygulama oluşturuyorsanız ve söz konusu bağımlılık zincirinden başlangıcında projedir kilit dosyanın kaynak kod deposuna iade edin geri yükleme sırasında bunu kullanın.

Projenizi gönderilen bir kitaplık projesi veya hangi diğer ortak bir kod projesi varsa ancak projeleri bağlı bağlıdır **barındırmamalıdır** kaynak kodunuzu bir parçası olarak kilit dosyasında denetleyin. Kilit dosyası tutma içinde hiçbir zarar yoktur, ancak ortak kod projesi için kilitli paket bağımlılıkları, bu ortak kod projesi üzerinde bağımlı bir proje geri yükleme/derleme sırasında kilit dosyasında listelenen kullanılamaz.

Örn.
```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```
Varsa `ProjectA` bir bağımlılığa sahip bir `PackageX` sürüm `2.0.0` ve ayrıca başvuran `ProjectB` , bağımlı `PackageX` sürüm `1.0.0`, ardından kilit dosyası için `ProjectB` üzerinde bir bağımlılık listeler `PackageX` Sürüm `1.0.0`. Ancak, `ProjectA` yapılandırıldığında, kendi kilit dosya çubuğunda bir bağımlılık içerecek `PackageX` sürüm **`2.0.0`** ve **değil** `1.0.0` kilitdosyasındalistelenen`ProjectB`. Bu nedenle, ortak bir kod projesi kilit dosyanın bağımlı projeler için çözülmüş paketleri üzerinde çok az say sahiptir.

### <a name="lock-file-extensibility"></a>Kilit dosya genişletilebilirliği
Aşağıda açıklandığı gibi çeşitli geri yükleme davranışlarını kilit dosyasıyla denetleyebilirsiniz:

| Seçenek | MSBuild eşdeğer seçeneği | 
|:---  |:--- |
| `--use-lock-file` | Bir proje için kilit dosyasının bootstraps kullanın. Alternatif olarak ayarlayabilirsiniz `RestorePackagesWithLockFile` proje dosyasındaki özelliği | 
| `--locked-mode` | Geri yükleme modunu etkinleştirir kilitli. Bu, yinelenebilir derlemeleri almak istediğiniz CI/CD senaryolarda yararlıdır. Bu ayarlayarak olabilir `RestoreLockedMode` MSBuild özelliği `true` |  
| `--force-evaluate` | Bu seçenek projede tanımlanan kayan sürümüyle paketlerle yararlıdır. Geri yükleme işlemi çalıştırmadığınız sürece varsayılan olarak NuGet geri yükleme Paket sürümü her geri yükleme sırasında otomatik olarak güncelleştirmez `--force-evaluate` seçeneği. |
| `--lock-file-path` | Bir proje için özel kilit dosya konumu tanımlar. Bu ayrıca MSBuild özelliği ayarlanarak sağlanabilir `NuGetLockFilePath`. Varsayılan olarak, NuGet destekler `packages.lock.json` kök dizininde. Aynı dizinde birden çok proje varsa, NuGet proje belirli kilit dosyası destekler. `packages.<project_name>.lock.json` |
