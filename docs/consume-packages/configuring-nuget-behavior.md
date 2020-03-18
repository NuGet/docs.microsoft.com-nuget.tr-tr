---
title: Ortak NuGet yapılandırması
description: NuGet. config dosyaları, NuGet 'in hem genel hem de proje başına temelinde denetimini denetler ve NuGet yapılandırma komutuyla değiştirilir.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: conceptual
ms.openlocfilehash: 89127203df0aa1eb24f36b8ec64c5bb4a4d59319
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428914"
---
# <a name="common-nuget-configurations"></a>Ortak NuGet yapılandırması

NuGet davranışı, proje, Kullanıcı ve bilgisayar genelindeki düzeylerde bulunabilir bir veya daha fazla `NuGet.Config` (XML) dosyasında birikmiş ayarlar tarafından çalıştırılır. Genel bir `NuGetDefaults.Config` dosyası, paket kaynaklarını da özellikle yapılandırır. Ayarlar, CLı, Paket Yöneticisi konsolu ve Paket Yöneticisi Kullanıcı arabiriminde verilen tüm komutlara uygulanır.

## <a name="config-file-locations-and-uses"></a>Yapılandırma dosyası konumları ve kullanımları

| Kapsam | NuGet. config dosyası konumu | Açıklama |
| --- | --- | --- |
| Çözüm | Geçerli klasör (diğer adıyla, çözüm klasörü) veya sürücü köküne kadar herhangi bir klasör.| Bir çözüm klasöründe, ayarlar alt klasörlerdeki tüm projelere uygulanır. Bir yapılandırma dosyası bir proje klasörüne yerleştirilmişse, projenin bu proje üzerinde hiçbir etkisi olmadığını unutmayın. |
| Kullanıcı | Windows: `%appdata%\NuGet\NuGet.Config`<br/>Mac/Linux: `~/.config/NuGet/NuGet.Config` veya `~/.nuget/NuGet/NuGet.Config` (işletim sistemi dağıtımına göre değişir) | Ayarlar tüm işlemlere uygulanır, ancak proje düzeyindeki tüm ayarlar tarafından geçersiz kılınır. |
| Bilgisayar | Windows: `%ProgramFiles(x86)%\NuGet\Config`<br/>Mac/Linux: `$XDG_DATA_HOME`. `$XDG_DATA_HOME` null veya boş ise, `~/.local/share` veya `/usr/local/share` kullanılır (işletim sistemi dağıtımına göre değişir)  | Ayarlar bilgisayardaki tüm işlemlere uygulanır, ancak herhangi bir kullanıcı veya proje düzeyi ayar tarafından geçersiz kılınır. |

NuGet 'in önceki sürümleri için notlar:
- NuGet 3,3 ve önceki sürümleri, çözüm genelinde ayarlar için bir `.nuget` klasörü kullandı. Bu klasör NuGet 3.4 + ' de kullanılmaz.
- NuGet 2,6 için 3. x, Windows üzerindeki bilgisayar düzeyi yapılandırma dosyası%ProgramData%\NuGet\Config [\\{IDE} [\\{Version} [\\{SKU}]]] \Nuget.exe} konumunda bulunuyor; burada *{IDE}* *VisualStudio*, *{Version}* , *14,0*gibi Visual Studio sürümüdür ve *{SKU}* *Community*, *Pro*ya da *Enterprise*. Ayarları NuGet 4.0 + ' ya geçirmek için yapılandırma dosyasını% ProgramFiles (x86)% \ Nuget\configkonumuna kopyalamanız yeterlidir. Linux 'ta, bu önceki konum/etc/opt ve Mac üzerinde/Library/Application Support desteği idi.

## <a name="changing-config-settings"></a>Yapılandırma ayarlarını değiştirme

`NuGet.Config` dosyası, [NuGet yapılandırma ayarları](../reference/nuget-config-file.md) konusunda açıklandığı gibi anahtar/değer çiftlerini içeren basıt bir XML metin dosyasıdır.

Ayarlar, NuGet CLı [yapılandırma komutu](../reference/cli-reference/cli-ref-config.md)kullanılarak yönetilir:
- Varsayılan olarak, değişiklikler Kullanıcı düzeyi yapılandırma dosyasında yapılır.
- Farklı bir dosyadaki ayarları değiştirmek için `-configFile` anahtarını kullanın. Bu durumda, dosyalar herhangi bir dosya adını kullanabilir.
- Anahtarlar her zaman büyük/küçük harfe duyarlıdır.
- Bilgisayar düzeyi ayarları dosyasındaki ayarları değiştirmek için yükseltme gereklidir.

> [!Warning]
> Dosyayı herhangi bir metin düzenleyicisinde değiştirebilseniz de, NuGet (v 3.4.3 ve üzeri), hatalı biçimlendirilmiş XML (eşleşmeyen Etiketler, geçersiz tırnak işaretleri vb.) içeriyorsa tüm yapılandırma dosyalarını sessizce yoksayar. `nuget config`kullanılarak ayarların yönetilmesi tercih edilir.

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
> NuGet 3,4 ve üzeri sürümlerde, `repositoryPath=%PACKAGEHOME%` (Windows) ve `repositoryPath=$PACKAGEHOME` (Mac/Linux) gibi herhangi bir değerde ortam değişkenlerini kullanabilirsiniz.

### <a name="removing-a-value"></a>Değer kaldırma

Bir değeri kaldırmak için, boş bir değere sahip bir anahtar belirtin.

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a>Yeni bir yapılandırma dosyası oluşturma

Aşağıdaki şablonu yeni dosyaya kopyalayın ve sonra değerleri ayarlamak için `nuget config -configFile <filename>` kullanın:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a>Ayarlar nasıl uygulanır

Birden çok `NuGet.Config` dosyası, tek bir projeye, bir proje grubuna veya tüm projelere uygulanabilmeleri için ayarları farklı konumlarda depolamanızı sağlar. Bu ayarlar, bir projeye veya geçerli klasöre "en yakın" olan ayarlar ile, komut satırından veya Visual Studio 'dan çağrılan herhangi bir NuGet işleminde toplu olarak uygulanır.

Özellikle, NuGet ayarları farklı yapılandırma dosyalarından aşağıdaki sırada yükler:

1. Yalnızca paket kaynaklarıyla ilgili ayarları içeren [Nugetdefaults. config dosyası](#nuget-defaults-file).
1. Bilgisayar düzeyindeki dosya.
1. Kullanıcı düzeyi dosyası.
1. `-configFile`ile belirtilen dosya.
1. Sürücü kökünden geçerli klasöre (NuGet. exe ' nin çağrıldığı veya Visual Studio projesini içeren klasör) yoldaki her klasörde bulunan dosyalar. Örneğin, bir komut c:\A\B\C içinde çağrılırsa, NuGet c:\, sonra c:\A, ardından c:\A\B ve son olarak c:\A\B\C. içindeki yapılandırma dosyalarını arar ve yükler.

NuGet bu dosyalardaki ayarları bulduğundan, bunlar aşağıdaki gibi uygulanır:

1. Tek öğe öğelerinde, NuGet aynı anahtar için önceden bulunan tüm değeri değiştirdi. Bu, geçerli klasöre veya projeye "en yakın" olan ayarların daha önce bulduğu diğer tüm diğerlerini geçersiz kıldığı anlamına gelir. Örneğin, `NuGetDefaults.Config` `defaultPushSource` ayarı başka herhangi bir yapılandırma dosyasında varsa geçersiz kılınır.

1. Koleksiyon öğeleri için (örneğin, `<packageSources>`), NuGet tüm yapılandırma dosyalarındaki değerleri tek bir koleksiyon olarak birleştirir.

1. Belirli bir düğüm için `<clear />` mevcut olduğunda, NuGet bu düğüm için önceden tanımlanmış yapılandırma değerlerini yoksayar.

### <a name="settings-walkthrough"></a>Ayarlar izlenecek yol

İki ayrı sürücüde aşağıdaki klasör yapısına sahip olduğunu varsayalım:

    disk_drive_1
        User
    disk_drive_2
       Project1
         Source
       Project2
         Source
       tmp

Daha sonra, belirtilen içeriğe sahip aşağıdaki konumlarda dört `NuGet.Config` dosyası vardır. (Bilgisayar düzeyindeki dosya bu örneğe dahil değildir, ancak kullanıcı düzeyindeki dosyada benzer şekilde davranır.)

Dosya A. Kullanıcı düzeyi dosya, (Windows üzerinde`%appdata%\NuGet\NuGet.Config`, Mac/Linux 'ta `~/.config/NuGet/NuGet.Config`):

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

Dosya B. disk_drive_2/NuGet.exe:

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

Dosya C. disk_drive_2/Project1/NuGet,config:

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

Dosya D. disk_drive_2/Project2/NuGet.exe:

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

- **Disk_drive_2/Project1 veya disk_drive_2/Project1/Source: ' dan çağrıldığında**, önce Kullanıcı düzeyi dosya (A) yüklenir, ardından NuGet dosyayı (B) disk_drive_2 kökünden, ardından dosyayı (C) yükler. (C) içindeki ayarlar, (B) ve (A) içindeki ayarları geçersiz kılar, bu nedenle paketlerin yüklendiği `repositoryPath`/Project1/External/Packages *disk_drive_2/tmp*yerine disk_drive_2. Ayrıca, (C) `<packageSources>`temizlemediğinden, nuget.org artık `https://MyPrivateRepo/ES/nuget`yalnızca bir kaynak olarak kullanılamaz.

- **Disk_drive_2/Project2 veya disk_drive_2/Project2/Source**: ' dan önce dosya (b) ve dosya (D) ile birlikte Kullanıcı düzeyi dosya (A) yüklenir. `packageSources` temizlenmediği için hem `nuget.org` hem de `https://MyPrivateRepo/DQ/nuget` kaynak olarak kullanılabilir. Paketler, (B) ' de belirtildiği gibi disk_drive_2/tmp ' de genişletilir.

## <a name="nuget-defaults-file"></a>NuGet Varsayılanları dosyası

`NuGetDefaults.Config` dosyası, paketlerin yüklendiği ve güncelleştirildiği paket kaynaklarını belirtmek ve paketleri `nuget push`ile yayımlamaya yönelik varsayılan hedefi denetlemek için bulunur. Yöneticiler uygun şekilde (örneğin grup ilkesi kullanarak), tutarlı `NuGetDefaults.Config` dosyalarını geliştirici ve derleme makinelerine dağıtmak için, kuruluştaki herkesin nuget.org yerine doğru paket kaynaklarını kullandığından emin olabilirler.

> [!Important]
> `NuGetDefaults.Config` dosyası hiçbir şekilde bir geliştiricinin NuGet yapılandırmasından bir paket kaynağının kaldırılmasına neden olmaz. Yani, geliştirici zaten NuGet kullanıyorsa ve bu nedenle nuget.org paket kaynağı kayıtlıysa, bir `NuGetDefaults.Config` dosyası oluşturulduktan sonra kaldırılmaz.
>
> Ayrıca, NuGet 'de ne `NuGetDefaults.Config` ne de başka bir mekanizma nuget.org gibi paket kaynaklarına erişimi engelleyebilir. Bir kuruluş söz konusu erişimi engellemeyi istiyorsa, bunun için güvenlik duvarları gibi diğer yollarla kullanılması gerekir.

### <a name="nugetdefaultsconfig-location"></a>NuGetDefaults. config konumu

Aşağıdaki tabloda, hedef işletim sistemine bağlı olarak `NuGetDefaults.Config` dosyasının nerede saklanacağı açıklanmaktadır:

| İşletim sistemi platformu  | NuGetDefaults. config konumu |
| --- | --- |
| Windows      | **Visual Studio 2017 veya NuGet 4. x +:** `%ProgramFiles(x86)%\NuGet\Config` <br />**Visual Studio 2015 ve öncesi ya da NuGet 3. x ve öncesi:** `%PROGRAMDATA%\NuGet` |
| Mac/Linux    | `$XDG_DATA_HOME` (genellikle `~/.local/share` veya `/usr/local/share`, işletim sistemi dağıtımına bağlı olarak)|

### <a name="nugetdefaultsconfig-settings"></a>NuGetDefaults. config ayarları

- `packageSources`: Bu koleksiyon, normal yapılandırma dosyalarındaki `packageSources` aynı anlama sahiptir ve varsayılan kaynakları belirtir. NuGet, `packages.config` yönetim biçimini kullanarak projelerdeki paketleri yükleme veya güncelleştirme sırasında kaynakları kullanır. , PackageReference biçimini kullanan projeler için, NuGet önce yerel kaynakları, ardından ağ paylaşımlarında kaynakları, sonra da yapılandırma dosyalarındaki sıra ne olursa olsun HTTP kaynaklarını kullanır. NuGet, geri yükleme işlemlerine sahip kaynakların sırasını her zaman yoksayar.

- `disabledPackageSources`: Bu koleksiyonda ayrıca, etkilenen her kaynağın adı ve devre dışı olup olmadığını gösteren bir doğru/yanlış değeri tarafından listelenen `NuGet.Config` dosyaları ile aynı anlamı vardır. Bu, kaynak adının ve URL 'nin varsayılan olarak açık olmadan `packageSources` devam etmesine izin verir. Bireysel geliştiriciler daha sonra doğru URL 'yi bulmayı gerektirmeden kaynağın değerini diğer `NuGet.Config` dosyalarında false olarak ayarlayarak kaynağı yeniden etkinleştirebilir. Bu, geliştiricilere yalnızca bireysel ekibin kaynağını varsayılan olarak etkinleştirirken bir kuruluşun iç kaynak URL 'lerinin tam listesini sağlamak için de kullanışlıdır.

- `defaultPushSource`: `nuget push` işlemleri için varsayılan hedefi belirtir, nuget.org 'in yerleşik varsayılan öğesini geçersiz kılar. Yöneticiler, nuget.org ' a yayımlamak için özellikle `nuget push -Source` kullanmaları gerektiğinde, iç paketlerin yanlışlıkla yanlışlıkla, genel yayımlamasını önlemek için bu ayarı dağıtabilir.

### <a name="example-nugetdefaultsconfig-and-application"></a>Örnek NuGetDefaults. config ve uygulama

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
