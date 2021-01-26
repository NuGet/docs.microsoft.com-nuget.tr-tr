---
title: Ortak NuGet yapılandırmaları
description: NuGet.Config dosyalar, NuGet 'in hem genel hem de proje başına temelinde denetimini denetler ve NuGet yapılandırma komutuyla değiştirilir.
author: JonDouglas
ms.author: jodou
ms.date: 10/25/2017
ms.topic: conceptual
ms.openlocfilehash: 35339626b0a20ccfceafa89fef94fb3187013fd7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774861"
---
# <a name="common-nuget-configurations"></a>Ortak NuGet yapılandırmaları

NuGet davranışı `NuGet.Config` , proje, Kullanıcı ve bilgisayar genelindeki düzeylerde bulunabilir bir veya daha fazla (XML) dosyada birikmiş ayarlar tarafından yönlendirilir. Genel bir `NuGetDefaults.Config` Dosya Ayrıca paket kaynaklarını özellikle yapılandırır. Ayarlar, CLı, Paket Yöneticisi konsolu ve Paket Yöneticisi Kullanıcı arabiriminde verilen tüm komutlara uygulanır.

## <a name="config-file-locations-and-uses"></a>Yapılandırma dosyası konumları ve kullanımları

| Kapsam | NuGet.Config dosya konumu | Açıklama |
| --- | --- | --- |
| Çözüm | Geçerli klasör (diğer adıyla, çözüm klasörü) veya sürücü köküne kadar herhangi bir klasör.| Bir çözüm klasöründe, ayarlar alt klasörlerdeki tüm projelere uygulanır. Bir yapılandırma dosyası bir proje klasörüne yerleştirilmişse, projenin bu proje üzerinde hiçbir etkisi olmadığını unutmayın. |
| Kullanıcı | **Windows:**`%appdata%\NuGet\NuGet.Config`<br/>**Mac/Linux:** `~/.config/NuGet/NuGet.Config` veya `~/.nuget/NuGet/NuGet.Config` (işletim sistemi dağıtımına göre farklılık gösterir) <br/>Ek yapılandırmaları tüm platformlarda desteklenir. Bu config 'ler araç tarafından düzenlenemez. </br> **Windows:**`%appdata%\NuGet\config\*.Config` <br/>**Mac/Linux:** `~/.config/NuGet/config/*.config` veya `~/.nuget/config/*.config` | Ayarlar tüm işlemlere uygulanır, ancak proje düzeyindeki tüm ayarlar tarafından geçersiz kılınır. |
| Bilgisayar | **Windows:**`%ProgramFiles(x86)%\NuGet\Config`<br/>**Mac/Linux:** `$XDG_DATA_HOME` . `$XDG_DATA_HOME`Null veya boş ise ya da `~/.local/share` `/usr/local/share` kullanılacaksa (OS dağıtımına göre değişir)  | Ayarlar bilgisayardaki tüm işlemlere uygulanır, ancak herhangi bir kullanıcı veya proje düzeyi ayar tarafından geçersiz kılınır. |

NuGet 'in önceki sürümleri için notlar:
- NuGet 3,3 ve önceki sürümleri `.nuget` çözüm genelinde ayarlar için bir klasör kullandı. Bu klasör NuGet 3.4 + ' de kullanılmaz.
- NuGet 2,6 için 3. x olarak, Windows üzerindeki bilgisayar düzeyi yapılandırma dosyası%ProgramData%\NuGet\Config [ \\ {IDE} [{ \\ Version} [ \\ {SKU}]]] \NuGet.Config. burada *{IDE}* *VisualStudio*, *{Version}* , *14,0* gibi Visual Studio sürümü ve *{SKU}* ise *Community*, *Pro* veya *Enterprise*. Ayarları NuGet 4.0 + ' ya geçirmek için yapılandırma dosyasını% ProgramFiles (x86)% \ Nuget\configkonumuna kopyalamanız yeterlidir. Linux 'ta, bu önceki konum/etc/opt ve Mac üzerinde/Library/Application Support desteği idi.

## <a name="changing-config-settings"></a>Yapılandırma ayarlarını değiştirme

`NuGet.Config`Dosya, [NuGet yapılandırma ayarları](../reference/nuget-config-file.md) konusunda açıklandığı gibi anahtar/değer çiftlerini IÇEREN basit bir XML metin dosyasıdır.

Ayarlar, NuGet CLı [yapılandırma komutu](../reference/cli-reference/cli-ref-config.md)kullanılarak yönetilir:
- Varsayılan olarak, değişiklikler Kullanıcı düzeyi yapılandırma dosyasında yapılır.
- Farklı bir dosyadaki ayarları değiştirmek için `-configFile` anahtarını kullanın. Bu durumda, dosyalar herhangi bir dosya adını kullanabilir.
- Anahtarlar her zaman büyük/küçük harfe duyarlıdır.
- Bilgisayar düzeyi ayarları dosyasındaki ayarları değiştirmek için yükseltme gereklidir.

> [!Warning]
> Dosyayı herhangi bir metin düzenleyicisinde değiştirebilseniz de, NuGet (v 3.4.3 ve üzeri), hatalı biçimlendirilmiş XML (eşleşmeyen Etiketler, geçersiz tırnak işaretleri vb.) içeriyorsa tüm yapılandırma dosyalarını sessizce yoksayar. Bu, ayarının kullanılarak yönetilmesi tercih edilir `nuget config` .

### <a name="setting-a-value"></a>Değer ayarlama

Windows:

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\Config\NuGet.Config
```

Mac/Linux:

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=/home/packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=/home/projects/packages -configfile /home/my.Config
nuget config -set repositoryPath=/home/packages -configfile home/myApp/NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=/home/packages -configfile $XDG_DATA_HOME/NuGet.Config
```

> [!Note]
> NuGet 3,4 ve üzeri sürümlerde, `repositoryPath=%PACKAGEHOME%` (Windows) ve `repositoryPath=$PACKAGEHOME` (Mac/Linux) içinde olduğu gibi, ortam değişkenlerini herhangi bir değer içinde kullanabilirsiniz.

### <a name="removing-a-value"></a>Değer kaldırma

Bir değeri kaldırmak için, boş bir değere sahip bir anahtar belirtin.

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a>Yeni bir yapılandırma dosyası oluşturma

Aşağıdaki şablonu yeni dosyaya kopyalayın ve ardından `nuget config -configFile <filename>` değerleri ayarlamak için kullanın:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a>Ayarlar nasıl uygulanır

Birden çok `NuGet.Config` Dosya, tek bir projeye, bir proje grubuna veya tüm projelere uygulanabilmeleri için ayarları farklı konumlarda depolamanızı sağlar. Bu ayarlar, bir projeye veya geçerli klasöre "en yakın" olan ayarlar ile, komut satırından veya Visual Studio 'dan çağrılan herhangi bir NuGet işleminde toplu olarak uygulanır.

Özellikle, NuGet ayarları farklı yapılandırma dosyalarından aşağıdaki sırada yükler:

1. Yalnızca paket kaynaklarıyla ilgili ayarları içeren [NuGetDefaults.Config dosyası](#nuget-defaults-file).
1. Bilgisayar düzeyindeki dosya.
1. Kullanıcı düzeyi dosyası.
1. İle belirtilen dosya `-configFile` .
1. Sürücü kökünden, geçerli klasöre (nuget.exe çağrıldığında veya Visual Studio projesini içeren klasörde) yoldaki her klasörde bulunan dosyalar. Örneğin, bir komut c:\A\B\C içinde çağrılırsa, NuGet yapılandırma dosyalarını şuna bakar ve yükler: \, c:\A, ardından c:\A\B ve son olarak c:\A\B\C.

NuGet bu dosyalardaki ayarları bulduğundan, bunlar aşağıdaki gibi uygulanır:

1. Tek öğe öğelerinde, NuGet aynı anahtar için önceden bulunan tüm değeri değiştirdi. Bu, geçerli klasöre veya projeye "en yakın" olan ayarların daha önce bulduğu diğer tüm diğerlerini geçersiz kıldığı anlamına gelir. Örneğin, `defaultPushSource` içindeki ayarı `NuGetDefaults.Config` başka herhangi bir yapılandırma dosyasında varsa geçersiz kılınır.

1. Koleksiyon öğeleri (gibi) için `<packageSources>` , NuGet tüm yapılandırma dosyalarındaki değerleri tek bir koleksiyon olarak birleştirir.

1. `<clear />`Belirli bir düğüm için olduğunda, NuGet bu düğüm için önceden tanımlanmış yapılandırma değerlerini yoksayar.

### <a name="settings-walkthrough"></a>Ayarlar izlenecek yol

İki ayrı sürücüde aşağıdaki klasör yapısına sahip olduğunu varsayalım:

```
disk_drive_1
    User
disk_drive_2
    Project1
        Source
    Project2
        Source
    tmp
```

Ardından, `NuGet.Config` belirtilen içeriğe sahip aşağıdaki konumlarda dört dosya vardır. (Bilgisayar düzeyindeki dosya bu örneğe dahil değildir, ancak kullanıcı düzeyindeki dosyada benzer şekilde davranır.)

Dosya A. Kullanıcı düzeyi dosyası, ( `%appdata%\NuGet\NuGet.Config` Windows 'ta, `~/.config/NuGet/NuGet.Config` Mac 'Te/Linux 'ta):

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

Dosya B. disk_drive_2/NuGet.Config:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <add key="repositoryPath" value="disk_drive_2/tmp" />
    </config>
    <packageRestore>
        <add key="enabled" value="True" />
    </packageRestore>
</configuration>
```

Dosya C. disk_drive_2/Project1/NuGet.Config:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <add key="repositoryPath" value="External/Packages" />
        <add key="defaultPushSource" value="https://MyPrivateRepo/ES/api/v2/package" />
    </config>
    <packageSources>
        <clear /> <!-- ensure only the sources defined below are used -->
        <add key="MyPrivateRepo - ES" value="https://MyPrivateRepo/ES/nuget" />
    </packageSources>
</configuration>
```

Dosya D. disk_drive_2/Project2/NuGet.Config:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

Ardından NuGet, çağrıldığı yere bağlı olarak ayarları yükler ve aşağıdaki gibi uygular:

- **Disk_drive_1/Users 'Den çağrılır**: yalnızca Kullanıcı düzeyi yapılandırma dosyasında (A) listelenen varsayılan depo, disk_drive_1 üzerinde bulunan tek dosya olduğu için kullanılır.

- **Disk_drive_2/veya disk_drive_/tmp**: önce Kullanıcı düzeyi dosya (A) yüklenir, ardından NuGet disk_drive_2 köküne gider ve dosyayı bulur (B). NuGet Ayrıca/tmp ' de bir yapılandırma dosyası arar ancak bir tane bulmaz. Sonuç olarak, nuget.org üzerindeki varsayılan depo kullanılır, paket geri yükleme etkinleştirilir ve paketler disk_drive_2/tmpa 'da genişletilir.

- **Disk_drive_2/Project1 veya disk_drive_2/Project1/Source: ' dan çağrıldığında**, önce Kullanıcı düzeyi dosya (A) yüklenir, ardından NuGet dosyayı (B) disk_drive_2 kökünden, ardından dosyayı (C) yükler. (C) içindeki ayarlar, (B) ve (A) içindeki ayarları geçersiz kılar, bu nedenle `repositoryPath` paketlerin yüklendiği yer, *disk_drive_2/tmp* yerine disk_drive_2/Project1/External/Packages. Ayrıca, (C) temizleyen `<packageSources>` , NuGet.org artık yalnızca bir kaynak olarak kullanılamaz `https://MyPrivateRepo/ES/nuget` .

- **Disk_drive_2/Project2 veya disk_drive_2/Project2/Source**: ' dan önce dosya (b) ve dosya (D) ile birlikte Kullanıcı düzeyi dosya (A) yüklenir. `packageSources`Temizlenmediği için her ikisi de `nuget.org` `https://MyPrivateRepo/DQ/nuget` kaynak olarak kullanılabilir. Paketler, (B) ' de belirtildiği gibi disk_drive_2/tmp ' de genişletilir.

## <a name="additional-user-wide-configuration"></a>Ek Kullanıcı genelindeki yapılandırma

NuGet, 5,7 ile başlayarak ek Kullanıcı genelindeki yapılandırma dosyaları için destek ekledi. Bu, üçüncü taraf satıcıların yükseltme olmadan ek Kullanıcı yapılandırma dosyaları eklemesine olanak tanır.
Bu yapılandırma dosyaları, bir alt klasör içindeki standart Kullanıcı genelindeki yapılandırma klasöründe bulunur `config` .
Veya ile biten tüm `.config` dosyalar `.Config` göz önünde bulundurulacaktır.
Bu dosyalar Standart araç tarafından düzenlenemez.

| İşletim sistemi platformu  | Ek yapılandırma |
| --- | --- |
| Windows      | `%appdata%\NuGet\config\*.Config` |
| Mac/Linux    | `~/.config/NuGet/config/*.config` veya `~/.nuget/config/*.config` |

## <a name="nuget-defaults-file"></a>NuGet Varsayılanları dosyası

`NuGetDefaults.Config`Dosya, paketlerin yüklendiği ve güncelleştirildiği paket kaynaklarını belirtmek ve paketleri ile yayımlamak için varsayılan hedefi denetlemek için vardır `nuget push` . Yöneticiler uygun bir şekilde (örneğin grup ilkesi kullanarak) `NuGetDefaults.Config` Geliştirici ve derleme makineleri için tutarlı dosyalar dağıtıp, kuruluştaki herkesin NuGet.org yerine doğru paket kaynaklarını kullandığından emin olabilirler.

> [!Important]
> `NuGetDefaults.Config`Dosya hiçbir şekilde bir geliştiricinin NuGet yapılandırmasından bir paket kaynağının kaldırılmasına neden olmaz. Yani, geliştirici zaten NuGet kullanıyorsa ve bu nedenle nuget.org paket kaynağı kayıtlıysa, bir dosya oluşturulduktan sonra kaldırılmaz `NuGetDefaults.Config` .
>
> Ayrıca, `NuGetDefaults.Config` NuGet 'deki başka hiçbir mekanizma, NuGet.org gibi paket kaynaklarına erişimi engelleyebilir. Bir kuruluş söz konusu erişimi engellemeyi istiyorsa, bunun için güvenlik duvarları gibi diğer yollarla kullanılması gerekir.

### <a name="nugetdefaultsconfig-location"></a>NuGetDefaults.Config konumu

Aşağıdaki tabloda `NuGetDefaults.Config` , hedef işletim sistemine bağlı olarak dosyanın depolanacağı konum açıklanmaktadır:

| İşletim sistemi platformu  | NuGetDefaults.Config konumu |
| --- | --- |
| Windows      | **Visual Studio 2017 veya NuGet 4. x +:**`%ProgramFiles(x86)%\NuGet\Config` <br />**Visual Studio 2015 ve öncesi ya da NuGet 3. x ve öncesi:**`%PROGRAMDATA%\NuGet` |
| Mac/Linux    | `$XDG_DATA_HOME` (genellikle `~/.local/share` veya `/usr/local/share` , işletim sistemi dağıtımına bağlı olarak)|

### <a name="nugetdefaultsconfig-settings"></a>NuGetDefaults.Config ayarları

- `packageSources`: Bu koleksiyon, `packageSources` Normal yapılandırma dosyaları ile aynı anlama sahiptir ve varsayılan kaynakları belirtir. NuGet, yönetim biçimini kullanarak projelerdeki paketleri yükleme veya güncelleştirme sırasında kaynakları kullanır `packages.config` . , PackageReference biçimini kullanan projeler için, NuGet önce yerel kaynakları, ardından ağ paylaşımlarında kaynakları, sonra da yapılandırma dosyalarındaki sıra ne olursa olsun HTTP kaynaklarını kullanır. NuGet, geri yükleme işlemlerine sahip kaynakların sırasını her zaman yoksayar.

- `disabledPackageSources`: Bu koleksiyonda ayrıca `NuGet.Config` , etkilenen her kaynağın adı ve devre dışı olup olmadığını gösteren bir doğru/yanlış değeri tarafından listelenen dosyalardaki gibi aynı anlamı vardır. Bu, kaynak adının ve URL 'nin `packageSources` Varsayılan olarak açık olmadan ' de kalmasına izin verir. Bireysel geliştiriciler daha sonra `NuGet.Config` doğru URL 'yi bulmaya gerek kalmadan kaynağın değerini diğer dosyalardaki false olarak ayarlayarak kaynağı yeniden etkinleştirebilir. Bu, geliştiricilere yalnızca bireysel ekibin kaynağını varsayılan olarak etkinleştirirken bir kuruluşun iç kaynak URL 'lerinin tam listesini sağlamak için de kullanışlıdır.

- `defaultPushSource`: `nuget push` NuGet.org 'in yerleşik varsayılan öğesini geçersiz kılarak, işlemler için varsayılan hedefi belirtir. Yöneticiler, özellikle nuget.org ' de yayımlamak için kullanması gerektiği için, şirket içi paketlerin yanlışlıkla yanlışlıkla, genel nuget.org yayınlanmasını önlemek üzere bu ayarı dağıtabilir `nuget push -Source` .

### <a name="example-nugetdefaultsconfig-and-application"></a>Örnek NuGetDefaults.Config ve uygulama

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <!-- defaultPushSource key works like the 'defaultPushSource' key of NuGet.Config files. -->
    <!-- This can be used by administrators to prevent accidental publishing of packages to nuget.org. -->
    <config>
        <add key="defaultPushSource" value="https://contoso.com/packages/" />
    </config>

    <!-- Default Package Sources; works like the 'packageSources' section of NuGet.Config files. -->
    <!-- This collection cannot be deleted or modified but can be disabled/enabled by users. -->
    <packageSources>
        <add key="Contoso Package Source" value="https://contoso.com/packages/" />
        <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />
    </packageSources>

    <!-- Default Package Sources that are disabled by default. -->
    <!-- Works like the 'disabledPackageSources' section of NuGet.Config files. -->
    <!-- Sources cannot be modified or deleted either but can be enabled/disabled by users. -->
    <disabledPackageSources>
        <add key="nuget.org" value="true" />
    </disabledPackageSources>
</configuration>
```
