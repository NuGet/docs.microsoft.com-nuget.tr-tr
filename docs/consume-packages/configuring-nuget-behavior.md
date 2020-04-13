---
title: Ortak NuGet yapılandırmaları
description: NuGet.Config dosyaları NuGet'in davranışını hem genel olarak hem de proje başına denetler ve nuget config komutuyla değiştirilir.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: conceptual
ms.openlocfilehash: 89127203df0aa1eb24f36b8ec64c5bb4a4d59319
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428914"
---
# <a name="common-nuget-configurations"></a>Ortak NuGet yapılandırmaları

NuGet'in davranışı, proje, kullanıcı ve `NuGet.Config` bilgisayar genelinde ki düzeylerde bulunabilen bir veya daha fazla (XML) dosyadaki birikmiş ayarlar tarafından yönlendirilir. Genel `NuGetDefaults.Config` bir dosya da özellikle paket kaynaklarını yapılandırır. Ayarlar CLI, Package Manager Console ve Paket Yöneticisi UI'de verilen tüm komutlar için geçerlidir.

## <a name="config-file-locations-and-uses"></a>Config dosya konumları ve kullanımları

| Kapsam | NuGet.Config dosya konumu | Açıklama |
| --- | --- | --- |
| Çözüm | Geçerli klasör (aka Solution klasörü) veya sürücü köküne kadar herhangi bir klasör.| Çözüm klasöründe ayarlar alt klasörlerdeki tüm projeleriçin geçerlidir. Bir config dosyası proje klasörüne yerleştirilirse, bunun bu proje üzerinde hiçbir etkisi olmadığını unutmayın. |
| Kullanıcı | Windows:`%appdata%\NuGet\NuGet.Config`<br/>Mac/Linux: `~/.config/NuGet/NuGet.Config` `~/.nuget/NuGet/NuGet.Config` veya (işletim sistemi dağılımına göre değişir) | Ayarlar tüm işlemler için geçerlidir, ancak proje düzeyi ayarları tarafından geçersiz kılınan. |
| Bilgisayar | Windows:`%ProgramFiles(x86)%\NuGet\Config`<br/>Mac/Linux: `$XDG_DATA_HOME`. Null `$XDG_DATA_HOME` veya boş `~/.local/share` ise `/usr/local/share` veya kullanılacaksa (işletim sistemi dağılımına göre değişir)  | Ayarlar bilgisayardaki tüm işlemler için geçerlidir, ancak herhangi bir kullanıcı veya proje düzeyi ayarları tarafından geçersiz kılınan. |

NuGet'in önceki sürümleri için notlar:
- NuGet 3.3 ve `.nuget` daha önce çözüm genelinde ayarlar için bir klasör kullanılır. Bu klasör NuGet 3.4+ için kullanılmaz.
- NuGet 2.6 ile 3.x için, Windows'daki bilgisayar düzeyindeki config dosyası\\%ProgramData%\NuGet\Config[ {IDE}[ {Version}]\\\\\{SKU}]]]]\NuGet.Config, *{IDE}* 14.0 gibi Visual *Studio*sürümü , *{Sürüm}* *14.0*gibi Visual Studio sürümü ve *{SKU}* topluluk , *Pro*, veya *Enterprise*. *Community* Ayarları NuGet 4.0+'ya geçirmek için config dosyasını %ProgramFiles(x86)%\NuGet\Config'e kopyalamanız yeterlidir. Linux'ta, bu önceki konum /etc/opt ve Mac, /Library/Application Support'tu.

## <a name="changing-config-settings"></a>Config ayarlarını değiştirme

`NuGet.Config` Dosya, [NuGet Yapılandırma Ayarları](../reference/nuget-config-file.md) konusunda açıklandığı gibi anahtar/değer çiftleri içeren basit bir XML metin dosyasıdır.

Ayarlar NuGet CLI [config komutu](../reference/cli-reference/cli-ref-config.md)kullanılarak yönetilir:
- Varsayılan olarak, kullanıcı düzeyinde config dosyasında değişiklikler yapılır.
- Farklı bir dosyadaki ayarları değiştirmek `-configFile` için anahtarı kullanın. Bu durumda dosyalar herhangi bir dosya adı kullanabilirsiniz.
- Anahtarlar her zaman büyük/küçük harf duyarlıdır.
- Bilgisayar düzeyindeki ayarlar dosyasındaki ayarları değiştirmek için yükseklik gereklidir.

> [!Warning]
> Dosyayı herhangi bir metin düzenleyicisinde değiştirebiliyor olsanız da, NuGet (v3.4.3 ve sonrası) hatalı biçimlendirilmiş XML (eşleşmemiş etiketler, geçersiz tırnak işaretleri, vb.) içeriyorsa, tüm yapılandırma dosyasını sessizce yok sayar. Bu nedenle ayarı kullanarak `nuget config`yönetmek tercih edilir.

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
> NuGet 3.4 ve daha sonra `repositoryPath=%PACKAGEHOME%` (Windows) ve `repositoryPath=$PACKAGEHOME` (Mac/Linux) gibi herhangi bir değerde ortam değişkenlerini kullanabilirsiniz.

### <a name="removing-a-value"></a>Bir değeri kaldırma

Bir değeri kaldırmak için boş değeri olan bir anahtar belirtin.

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a>Yeni bir config dosyası oluşturma

Aşağıdaki şablonu yeni dosyaya kopyalayın ve değerleri ayarlamak için kullanın: `nuget config -configFile <filename>`

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a>Ayarlar nasıl uygulanır?

Birden `NuGet.Config` çok dosya, ayarları tek bir projeye, bir proje grubuna veya tüm projelere uygulanabilmesi için farklı konumlarda depolamanıza olanak tanır. Bu ayarlar, komut satırından veya Visual Studio'dan çağrılan herhangi bir NuGet işlemi için topluca geçerlidir ve bir projeye veya geçerli klasöre "en yakın" ayarlar önceliklidir.

Özellikle, NuGet aşağıdaki sırayla farklı config dosyalarından ayarları yükler:

1. [NuGetDefaults.Config dosyası,](#nuget-defaults-file)yalnızca paket kaynaklarıyla ilgili ayarları içerir.
1. Bilgisayar düzeyindeki dosya.
1. Kullanıcı düzeyindedosya.
1. ' ile `-configFile`belirtilen dosya
1. Sürücü kökünden geçerli klasöre giden yoldaki her klasörde bulunan dosyalar (nuget.exe'nin çağrıldığı veya Visual Studio projesini içeren klasör). Örneğin, c:\A\B\C'de bir komut çağrılırsa, NuGet arar ve\, c'de config dosyalarını yükler: sonra c:\A, sonra c:\A\B ve son olarak c:\A\B\C.

NuGet bu dosyalardaki ayarları bulduğunda aşağıdaki gibi uygulanır:

1. Tek öğeli öğeler için NuGet, aynı anahtar için önceden bulunan herhangi bir değeri değiştirmiş. Bu, geçerli klasöre veya projeye "en yakın" ayarların daha önce bulunan diğer ayarları geçersiz kaktığı anlamına gelir. Örneğin, başka `defaultPushSource` bir `NuGetDefaults.Config` config dosyasında varsa, ayar geçersiz kılındı.

1. Koleksiyon öğeleri (örneğin), `<packageSources>`NuGet tüm yapılandırma dosyalarının değerlerini tek bir koleksiyonda birleştirir.

1. Belirli `<clear />` bir düğüm için mevcut olduğunda, NuGet bu düğüm için daha önce tanımlanmış yapılandırma değerlerini yoksa.

### <a name="settings-walkthrough"></a>Ayarları walkthrough

İki ayrı sürücüde aşağıdaki klasör yapısına sahip olduğunuzu varsayalım:

    disk_drive_1
        User
    disk_drive_2
       Project1
         Source
       Project2
         Source
       tmp

Daha sonra `NuGet.Config` verilen içerik ile aşağıdaki yerlerde dört dosya var. (Bilgisayar düzeyindeki dosya bu örneğe dahil edilmez, ancak kullanıcı düzeyindeki dosyaya benzer şekilde olur.)

Dosya A. Kullanıcı düzeyinde`%appdata%\NuGet\NuGet.Config` dosya, `~/.config/NuGet/NuGet.Config` (Windows' da, Mac/Linux' ta):

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

Dosya C. disk_drive_2/Proje1/NuGet.Config:

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

Dosya D. disk_drive_2/Proje2/NuGet.Config:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

NuGet daha sonra çağrıldığı yere bağlı olarak ayarları aşağıdaki gibi yükler ve uygular:

- **disk_drive_1/kullanıcılardan çağrılan**: disk_drive_1 bulunan tek dosya bu olduğundan, yalnızca kullanıcı düzeyindeyapılandırma dosyasında (A) listelenen varsayılan depo kullanılır.

- **disk_drive_2/ veya disk_drive_/tmp'den çağrılan**: Kullanıcı düzeyindeki dosya (A) önce yüklenir, sonra NuGet disk_drive_2 köküne gider ve (B) dosyasını bulur. NuGet ayrıca /tmp'de bir yapılandırma dosyası arar, ancak budosyayı bulamaz. Sonuç olarak, nuget.org varsayılan depo kullanılır, paket geri yüklemesi etkinleştirilir ve paketler disk_drive_2/tmp'de genişletilir.

- **disk_drive_2/Project1 veya disk_drive_2/Project1/Source:** Kullanıcı düzeyindeki dosya (A) önce yüklenir, ardından NuGet disk_drive_2 kökünden yüklenir ve ardından dosya (C) yüklenir. (C) 'deki ayarlar (B) ve (A)'dakileri geçersiz kılar, böylece paketlerin `repositoryPath` yüklendiği yer *disk_drive_2/tmp*yerine disk_drive_2/Project1/External/Packages olur. Ayrıca, (C) temizler `<packageSources>`çünkü, nuget.org artık kaynak `https://MyPrivateRepo/ES/nuget`olarak kullanılabilir sadece bırakarak .

- **disk_drive_2/Project2 veya disk_drive_2/Project2/Source :** Kullanıcı düzeyindeki dosya (A) önce (B) ve dosya (D) tarafından yüklenir. Çünkü `packageSources` temizlenmedi, `nuget.org` `https://MyPrivateRepo/DQ/nuget` her ikisi de ve kaynak olarak mevcuttur. Paketler (B)'de belirtildiği şekilde disk_drive_2/tmp cinsinden genişletilir.

## <a name="nuget-defaults-file"></a>NuGet varsayılan dosya

Dosya, `NuGetDefaults.Config` paketlerin yüklü ve güncelleştirildiği paket kaynaklarını belirtmek ve `nuget push`paketleri yayınlamak için varsayılan hedefi denetlemek için var. Yöneticiler uygun bir şekilde (örneğin Grup İlkesi'ni kullanarak) tutarlı `NuGetDefaults.Config` dosyaları geliştiriciye dağıtabildiklerinden ve makineler oluşturabildiklerinden, kuruluştaki herkesin nuget.org yerine doğru paket kaynaklarını kullandığından emin olabilirler.

> [!Important]
> Dosya `NuGetDefaults.Config` hiçbir zaman bir paket kaynağının geliştiricinin NuGet yapılandırmasından kaldırılmasına neden olmaz. Bu, geliştirici zaten NuGet kullanmış sa yılmışsa ve bu nedenle nuget.org paket `NuGetDefaults.Config` kaynağı kayıtlıysa, dosya oluşturulduktan sonra kaldırılmaz.
>
> Ayrıca, NuGet'deki ne `NuGetDefaults.Config` de başka bir mekanizma nuget.org gibi paket kaynaklarına erişimi engelleyebilir. Bir kuruluş bu tür erişimi engellemek istiyorsa, bunu yapmak için güvenlik duvarları gibi başka yollar kullanmalıdır.

### <a name="nugetdefaultsconfig-location"></a>NuGetDefaults.Config konumu

Aşağıdaki tabloda, `NuGetDefaults.Config` hedef işletim sistemi bağlı olarak dosyanın nerede depolanması gerektiği açıklanmaktadır:

| İşletim Sistemi Platformu  | NuGetDefaults.Config Yeri |
| --- | --- |
| Windows      | **Visual Studio 2017 veya NuGet 4.x+:**`%ProgramFiles(x86)%\NuGet\Config` <br />**Visual Studio 2015 ve önceki veya NuGet 3.x ve daha önceki:**`%PROGRAMDATA%\NuGet` |
| Mac/Linux    | `$XDG_DATA_HOME`(genellikle `~/.local/share` veya, `/usr/local/share`işletim sistemi dağılımına bağlı olarak)|

### <a name="nugetdefaultsconfig-settings"></a>NuGetDefaults.Config ayarları

- `packageSources`: Bu koleksiyon normal `packageSources` config dosyalarındakiyle aynı anlama gelir ve varsayılan kaynakları belirtir. NuGet, `packages.config` yönetim biçimini kullanarak projelerdeki paketleri yüklerken veya güncellerken kaynakları sırayla kullanır. PackageReference biçimini kullanan projelerde NuGet, yapılandırma dosyalarındaki siparişe bakılmaksızın önce yerel kaynakları, ardından ağ paylaşımları kaynaklarını, ardından HTTP kaynaklarını kullanır. NuGet her zaman geri yükleme işlemleri ile kaynakların sırasını yok sayar.

- `disabledPackageSources`: Bu koleksiyon, etkilenen her `NuGet.Config` kaynağın kendi adıyla listelendiği dosyalarla aynı anlama ve devre dışı kalıp olmadığını gösteren doğru/yanlış bir değere de sahiptir. Bu, kaynak adın ve `packageSources` URL'nin varsayılan olarak açık kalmadan içinde kalmasını sağlar. Tek tek geliştiriciler daha sonra kaynağın değerini doğru URL'yi `NuGet.Config` yeniden bulmak zorunda kalmadan diğer dosyalarda false olarak ayarlayarak kaynağı yeniden etkinleştirebilir. Bu, geliştiricilere varsayılan olarak yalnızca tek bir takımın kaynağını etkinleştirirken bir kuruluş için dahili kaynak URL'lerinin tam listesini sağlamak için de yararlıdır.

- `defaultPushSource`: işlemler için `nuget push` varsayılan hedefi belirtir ve yerleşik varsayılan nuget.org geçersiz kılın. Geliştiricilerin özellikle nuget.org yayınlamak için kullanmaları `nuget push -Source` gerektiğinden, yöneticiler bu ayarı, dahili paketleri yanlışlıkla genel nuget.org yayımlamamak için dağıtabilir.

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
