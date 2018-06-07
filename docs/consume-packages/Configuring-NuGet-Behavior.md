---
title: NuGet davranışını yapılandırma
description: NuGet.Config dosyaları, hem genel hem de proje başına temelinde NuGet davranışını denetlemek ve nuget config komutu ile değiştirilmelidir.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 10/25/2017
ms.topic: conceptual
ms.openlocfilehash: a4a73f671bc02fa8fb0b0fa28cad26da2e520097
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817749"
---
# <a name="configuring-nuget-behavior"></a>NuGet davranışını yapılandırma

NuGet davranışı güdümlü bir veya daha fazla birikmiş ayarlar tarafından `NuGet.Config` proje-, kullanıcı- ve bilgisayar genelinde düzeyinde bulunabilir (XML) dosyaları. Bir genel `NuGetDefaults.Config` dosyası, özellikle de paket kaynaklarını yapılandırır. Ayarlar CLI, Paket Yöneticisi konsolu ve Paket Yöneticisi kullanıcı Arabirimi yürütülen tüm komutlar için geçerlidir.

## <a name="config-file-locations-and-uses"></a>Config dosya konumları ve kullanır

| Kapsam | NuGet.Config dosya konumu | Açıklama |
| --- | --- | --- |
| Proje | Geçerli klasör (diğer adıyla proje klasörü) veya sürücü kök kadar herhangi bir klasör.| Bir proje klasöründe ayarlar yalnızca bu proje için geçerlidir. Birden çok proje alt klasör içeren üst klasörlerde ayarlar bu klasörlerdeki tüm projeleri için geçerlidir. |
| Kullanıcı | Windows: `%appdata%\NuGet\NuGet.Config`<br/>Mac/Linux: `~/.config/NuGet/NuGet.Config` veya `~/.nuget/NuGet/NuGet.Config` (işletim sistemi dağıtım göre farklılık gösterir) | Ayarları tüm işlemleri için geçerlidir, ancak herhangi bir proje düzeyi ayarı tarafından geçersiz kılınır. |
| Bilgisayar | Windows: `%ProgramFiles(x86)%\NuGet\Config`<br/>Mac/Linux: `$XDG_DATA_HOME`. Varsa `$XDG_DATA_HOME` null veya boş, `~/.local/share` veya `/usr/local/share` kullanılacak (işletim sistemi dağıtım göre farklılık gösterir)  | Ayarları, bilgisayarda tüm işlemleri için geçerlidir, ancak herhangi bir kullanıcı veya proje düzeyi ayarı tarafından geçersiz kılınır. |

NuGet'ın önceki sürümlerini için Notlar:
- NuGet 3.3 ve daha önce kullanılan bir `.nuget` çözüm genelindeki ayarları için klasör. Bu dosya NuGet 3.4 + kullanılmaz.
- 3.x için NuGet 2.6 için Windows bilgisayar düzeyinde yapılandırma dosyası % ProgramData%\NuGet\Config bulunamadı [\\{IDE} [\\{Version} [\\{SKU}]]]\NuGet.Config, burada *{IDE}* olabilir *Visual Studio*, *{Version}* Visual Studio sürümü gibi edildi *14.0*, ve *{SKU}* ya *topluluk*, *Pro*, veya *Kurumsal*. Nuget'e 4.0 + ayarlarını geçirmek için yapılandırma dosyası % ProgramFiles(x86) % \NuGet\Config kopyalayın. Linux üzerinde /etc/opt, önceki bu konumda olan ve Mac, Library/Application Support.

## <a name="changing-config-settings"></a>Yapılandırma ayarlarını değiştirme

A `NuGet.Config` dosyasıdır açıklandığı gibi anahtar/değer çiftleri içeren basit bir XML metin dosyası [NuGet yapılandırma ayarlarını](../reference/nuget-config-file.md) konu.

Ayarları NuGet CLI kullanarak yönetilen [config komutunu](../tools/cli-ref-config.md):
- Varsayılan olarak, kullanıcı düzeyinde yapılandırma dosyasına değişiklik yapılmaz.
- Farklı bir dosya ayarlarını değiştirmek için kullanmak `-configFile` geçin. Bu durumda dosyalarını dosya kullanabilirsiniz.
- Anahtarları her zaman büyük/küçük harfe duyarlıdır.
- Yükseltme, bilgisayar düzeyinde ayarları dosyasında ayarlarını değiştirmek için gereklidir.

> [!Warning]
> Herhangi bir metin düzenleyicisi, NuGet dosyasında yapılandırabilseniz (v3.4.3 ve sonraki sürümler) hatalı biçimlendirilmiş XML (eşleşmeyen etiketler, geçersiz tırnak işaretleri, vb.) içeriyorsa, tüm yapılandırma dosyası sessizce yok sayar. Kullanarak yönetmek için tercih edilir bu yüzden `nuget config`.

### <a name="setting-a-value"></a>Bir değer ayarlanması

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
> NuGet 3.4 ve daha sonra herhangi bir değer ortam değişkenleri olarak kullanabileceğiniz `repositoryPath=%PACKAGEHOME%` (Windows) ve `repositoryPath=%PACKAGEHOME` (Mac/Linux).

### <a name="removing-a-value"></a>Bir değer kaldırma

Bir değer kaldırmak için bir anahtar ile boş bir değer belirtin.

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a>Yeni bir yapılandırma dosyası oluşturma

Aşağıdaki şablonu yeni dosyaya kopyalayın ve ardından `nuget config -configFile <filename>` değerlerini ayarlamak için:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a>Ayarları nasıl uygulanır

Birden çok `NuGet.Config` dosyaları tek bir proje, bir grup projesini veya tüm projeleri için geçerli olacak şekilde farklı konumlarda ayarlarını depolamak izin verir. Bu ayarlar, topluca "en yakın" bir proje veya öncelik alma geçerli klasörde mevcut ayarlarla komut satırından veya Visual Studio'dan çağrılan herhangi bir NuGet işlemi için geçerlidir.

Özellikle, NuGet aşağıdaki sırayla farklı yapılandırma dosyalarından ayarları yükler:

1. [NuGetDefaults.Config dosya](#nuget-defaults-file), yalnızca paket kaynaklarını ilgili ayarları içerir.
1. Bilgisayar düzeyinde dosya.
1. Kullanıcı düzeyinde dosya.
1. Belirtilen dosya `-configFile`.
1. Her yolu geçerli bir klasör (burada nuget.exe çağrılır veya Visual Studio projeyi içeren klasörü) sürücüsünün kök klasöründe bulunan dosyaları. Örneğin, bir komut içinde c:\A\B\C çağrılırsa, NuGet arar ve c: yapılandırma dosyalarını yükler\, sonra c:\A, ardından c:\A\B ve son olarak c:\A\B\C.

NuGet bu dosyalarda ayarları buldukça, bunlar aşağıdaki gibi uygulanır:

1. Tek öğeli öğeleri için NuGet aynı anahtar için daha önce bulunan değeri değiştirildi. Bu, "geçerli klasörde veya projesini yakın" ayarlarını herhangi diğer daha önce bulunan geçersiz kılmak anlamına gelir. Örneğin, `defaultPushSource` ayarı `NuGetDefaults.Config` başka bir yapılandırma dosyasında varsa geçersiz kılınır.

1. Koleksiyon öğeleri için (gibi `<packageSources>`), NuGet tek bir koleksiyona tüm yapılandırma dosyalarını değerleri birleştirir.

1. Zaman `<clear />` mevcut olduğu için belirli bir düğüm, bu düğüm için önceden tanımlanmış yapılandırma değerlerini NuGet yoksayar.

### <a name="settings-walkthrough"></a>Ayarları gözden geçirme

İki ayrı sürücü üzerinde aşağıdaki klasör yapısına sahip varsayalım:

    disk_drive_1
        User
    disk_drive_2
       Project1
         Source
       Project2
         Source
       tmp

Dört sonra sahip `NuGet.Config` dosyaları aşağıdaki konumlarda verilen içeriğe sahip. (Bilgisayar düzeyinde dosya bu örnekte yer almaz, ancak kullanıcı düzeyinde dosyasına benzer şekilde davranacaktır.)

A. kullanıcı düzeyinde dosyası, (`%appdata%\NuGet\NuGet.Config` , Windows'da `~/.config/NuGet/NuGet.Config` Mac/Linux'ta):

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

B. disk_drive_2/NuGet.Config dosya:

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

C. dosya disk_drive_2/Project1/NuGet.Config:

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

NuGet sonra yükler ve burada çağrılır bağlı olarak aşağıdaki gibi ayarları uygular:

- **Disk_drive_1/kullanıcılardan çağrılan**: disk_drive_1 üzerinde bulunan yalnızca dosya olduğu için kullanıcı düzeyinde yapılandırma dosyasında (A) listelenen varsayılan depo kullanılır.

- **Disk_drive_2 çağrılan / veya disk_drive_/tmp**: kullanıcı düzeyinde dosya (A) ilk olarak, yüklendikten sonra NuGet disk_drive_2 kök dizinine gider ve bulur dosyası (B). NuGet de tmp yapılandırma dosyasında görünüyor, ancak bir bulmaz. Sonuç olarak, nuget.org varsayılan havuzda kullanıldığında, paket geri yükleme etkin ve paketleri disk_drive_2/tmp genişletilmiş.

- **Disk_drive_2/Project1 veya Project1/disk_drive_2/kaynağından çağrılan**: kullanıcı düzeyinde dosya (A) önce yüklenir, ardından NuGet yükleri (B) ve ardından disk_drive_2 kök dosyası (C). (C) ayarları geçersiz kılar (B) ve (A), böylece `repositoryPath` disk_drive_2/Project1/dış/paketleri yerine olan paketler yüklendiği *disk_drive_2/tmp*. Ayrıca, (C) temizler çünkü `<packageSources>`, nuget.org yalnızca bırakarak kaynağı olarak kullanılabilir artık `https://MyPrivateRepo/ES/nuget`.

- **Disk_drive_2/Project2 veya Project2/disk_drive_2/kaynağından çağrılan**: kullanıcı düzeyinde dosya (A) ilk dosyası (B) ve tarafından dosyası (D) ve ardından yüklenir. Çünkü `packageSources` değil işaretli değilse, her ikisi de `nuget.org` ve `https://MyPrivateRepo/DQ/nuget` kaynakları olarak kullanılabilir. Paketleri disk_drive_2/tmp (B) belirtildiği gibi genişletilmiş.

## <a name="nuget-defaults-file"></a>NuGet Varsayılanları dosyası

`NuGetDefaults.Config` Dosyasından içinden paketleri yüklü ve güncelleştirilmiş paket kaynaklarını belirtin ve paketlerle yayımlamak için varsayılan hedef denetlemek için `nuget push`. Yöneticiler kolaylıkla bakımından (örneğin Grup İlkesi kullanılarak) tutarlı dağıtmak `NuGetDefaults.Config` Geliştirici ve yapı makineleri dosyalara, bir yönetici şunları yapabilir kuruluştaki herkesin nuget.org yerine doğru paket kaynaklarını kullandığını sağlama.

> [!Important]
> `NuGetDefaults.Config` Dosyasının hiçbir zaman bir geliştiricinin NuGet yapılandırmasından kaldırmak bir paket kaynağı neden olur. Geliştirici NuGet zaten kullandı ve bu yüzden nuget.org paket kaynağı varsa, yani kayıtlı oluşturulmasından sonra kaldırılmadan olmaz bir `NuGetDefaults.Config` dosyası.
>
> Ayrıca, hiçbiri `NuGetDefaults.Config` veya başka bir mekanizma NuGet içinde nuget.org gibi paket kaynaklarına erişimi engelleyebilir. Bu tür erişimi engellemek bir kuruluş isterse, bu çok güvenlik duvarları gibi diğer yollarla Bunu yapmak için kullanın.

### <a name="nugetdefaultsconfig-location"></a>NuGetDefaults.Config konumu

Aşağıdaki tabloda nerede tanımlar `NuGetDefaults.Config` dosyasının saklanması gereken, işletim sistemi hedef bağlı olarak:

| İşletim sistemi platformu  | NuGetDefaults.Config konumu |
| --- | --- |
| Windows      | **Visual Studio 2017 veya NuGet 4.x+:** `%ProgramFiles(x86)%\NuGet\Config` <br />**Visual Studio 2015 ve önceki ya da NuGet 3.x ve önceki sürümleri:** `%PROGRAMDATA%\NuGet` |
| Mac/Linux    | `$XDG_DATA_HOME` (genellikle `~/.local/share` veya `/usr/local/share`işletim sistemi dağıtım bağlı olarak)|

### <a name="nugetdefaultsconfig-settings"></a>NuGetDefaults.Config ayarları

- `packageSources`: Bu koleksiyonun aynı anlamı taşır `packageSources` normal olarak yapılandırma dosyaları ve varsayılan kaynakları belirtir. NuGet kullandığı kaynakları yükleme ya da kullanarak projeleri paketlerinde güncelleştirilirken sırayla `packages.config` yönetim biçimi. PackageReference biçimi kullanarak projeleri için NuGet yerel kaynakları ilk kullanır ve ardından ağ paylaşımları ve yapılandırma dosyalarını sırayla bakılmaksızın HTTP kaynakları üzerindeki kaynakları. NuGet her zaman geri yükleme işlemleri kaynaklarıyla sırasını yok sayar.

- `disabledPackageSources`: Bu koleksiyonun ayrıca olarak ile aynı anlamı taşır `NuGet.Config` dosyaları, burada her etkilenen kaynak listelenir adını ve belirten bir true/false değerine tarafından devre dışı bırakılıp bırakılmayacağını. Bu kaynak adı ve URL içinde kalmasını sağlar `packageSources` gerek kalmadan, varsayılan olarak açıktır. Her bir geliştirici daha sonra tekrar etkinleştirebilirsiniz kaynak false diğer kaynağın değeri ayarlayarak `NuGet.Config` doğru URL'yi yeniden bulmak zorunda kalmadan dosyaları. Bu da geliştiricilerin iç kaynak URL'lerini varsayılan olarak yalnızca tek bir ekibin kaynağı etkinleştirme sırasında bir kuruluş için tam bir listesi ile sağlamak kullanışlıdır.

- `defaultPushSource`: için varsayılan hedef belirtir `nuget push` nuget.org yerleşik varsayılan geçersiz kılma işlemleri. Yöneticiler, yanlışlıkla, ortak nuget.org iç paketleri yayımlama önlemek için bu ayarı dağıtabilir, geliştiriciler özel olarak kullanmak gerek duyduğunuz `nuget push -Source` için nuget.org yayımlamak için.

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
