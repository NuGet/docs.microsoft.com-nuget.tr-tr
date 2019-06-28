---
title: NuGet yapılandırmaların
description: NuGet.Config dosyaları hem genel hem de proje başına temelinde NuGet davranışını denetleyen ve nuget config komutu ile değiştirilir.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: conceptual
ms.openlocfilehash: 57b7f29b533a8e6d7db2710c7e42a239f50199a1
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426661"
---
# <a name="common-nuget-configurations"></a>NuGet yapılandırmaların

NuGet'ın davranışı, bir veya daha fazla birikmiş ayarları tarafından yönlendirilir `NuGet.Config` proje-, kullanıcı- ve bilgisayar genelinde düzeyinde bulunabilir (XML) dosyaları. Genel bir `NuGetDefaults.Config` dosyası, özellikle de paket kaynaklarını yapılandırır. CLI, Paket Yöneticisi konsolu ve Paket Yöneticisi UI tüm komutlar için ayarları uygulayın.

## <a name="config-file-locations-and-uses"></a>Config dosya konumları ve kullanır

| Kapsam | NuGet.Config dosyası konumu | Açıklama |
| --- | --- | --- |
| Çözüm | Geçerli klasör (Çözüm klasörü olarak da bilinir) veya sürücü kök kadar herhangi bir klasör.| Bir çözüm klasörü içinde ayarlar alt klasörlerdeki tüm projeler için geçerlidir. Bir yapılandırma dosyası bir proje klasörüne konur, proje üzerinde etkiye sahip olduğunu unutmayın. |
| Kullanıcı | Windows: `%appdata%\NuGet\NuGet.Config`<br/>Mac/Linux: `~/.config/NuGet/NuGet.Config` veya `~/.nuget/NuGet/NuGet.Config` (işletim sistemi dağıtım göre değişiklik gösterir) | Ayarları tüm işlemler için geçerlidir, ancak herhangi bir proje düzeyi ayarı tarafından geçersiz kılınır. |
| Bilgisayar | Windows: `%ProgramFiles(x86)%\NuGet\Config`<br/>Mac/Linux: `$XDG_DATA_HOME`. Varsa `$XDG_DATA_HOME` null veya boş `~/.local/share` veya `/usr/local/share` kullanılacak (işletim sistemi dağıtım göre değişiklik gösterir)  | Ayarları bilgisayar üzerindeki tüm işlemler için geçerlidir, ancak herhangi bir kullanıcı veya proje düzeyi ayarı tarafından geçersiz kılınır. |

NuGet'ın önceki sürümleri için Notlar:
- NuGet 3.3 ve daha önce kullanılmış bir `.nuget` çözüm genelindeki ayarları için klasör. Bu dosya NuGet 3.4 + kullanılmaz.
- 3\.x için NuGet 2.6 için Windows bilgisayar düzeyinde yapılandırma dosyasını % ProgramData%\NuGet\Config konumunda [\\{IDE} [\\{Version} [\\{SKU}]]]\NuGet.Config, burada *{IDE}* olabilir *VisualStudio*, *{Version}* gibi Visual Studio sürümü olan *14.0*, ve *{SKU}* ya da *topluluk*, *Pro*, veya *Kurumsal*. İçin NuGet 4.0 + ayarlarını geçirmek için yapılandırma dosyası için % ProgramFiles(x86) % \NuGet\Config kopyalayın. Linux üzerinde /etc/opt, önceki bu konumda olan ve Mac'te Library/Application Support.

## <a name="changing-config-settings"></a>Yapılandırma ayarlarını değiştirme

A `NuGet.Config` dosyasıdır açıklandığı gibi anahtar/değer çiftleri içeren basit bir XML metin dosyasını [NuGet yapılandırma ayarlarını](../reference/nuget-config-file.md) konu.

Ayarları NuGet CLI'yı kullanarak yönetilen [config komutu](../tools/cli-ref-config.md):
- Varsayılan olarak, kullanıcı düzeyinde yapılandırma dosyasına değişiklikler yapılır.
- Farklı bir dosya ayarlarını değiştirmek için kullanın `-configFile` geçin. Bu durumda dosyalarını dosya kullanabilirsiniz.
- Anahtarları her zaman büyük/küçük harfe duyarlıdır.
- Bilgisayar düzeyinde ayarlar dosyasındaki ayarları değiştirmek için yükseltme gereklidir.

> [!Warning]
> Dosyasını bir metin düzenleyicisinde NuGet yapılandırabilseniz (v3.4.3 ve üzeri) hatalı biçimlendirilmiş XML (eşleşmeyen etiketleri, geçersiz bir tırnak işareti, vb.) içeriyorsa, tüm yapılandırma dosyası sessizce yoksayar. Bu nedenle kullanarak yönetmek için tercih edilir, `nuget config`.

### <a name="setting-a-value"></a>Bir değer ayarlama

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
> NuGet 3.4 ve üzeri gibi herhangi bir değer olarak ortam değişkenlerini kullanabilirsiniz `repositoryPath=%PACKAGEHOME%` (Windows) ve `repositoryPath=$PACKAGEHOME` (Mac/Linux).

### <a name="removing-a-value"></a>Bir değer kaldırılıyor

Bir değer kaldırmak için bir anahtar ile boş bir değer belirtin.

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a>Yeni bir yapılandırma dosyası oluşturma

Şablon aşağıdaki yeni dosyaya kopyalayın ve ardından `nuget config -configFile <filename>` değerlerini ayarlamak için:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a>Ayarları nasıl uygulanır

Birden çok `NuGet.Config` dosyaları tek bir proje, projelerin bir grup veya tüm projeler için geçerli olacak şekilde farklı konumlarda ayarlarını depolamak izin verir. Bu ayarlar, topluca "yakın.", bir proje ya da Öncelik Alma geçerli klasörde mevcut ayarlarla komut satırından veya Visual Studio'dan çağrılmasını herhangi bir NuGet işlemi için geçerlidir.

Özellikle, NuGet aşağıdaki sırayla farklı bir yapılandırma dosyalarından ayarları yükler:

1. [NuGetDefaults.Config dosya](#nuget-defaults-file), yalnızca paket kaynaklarını ilgili ayarları içerir.
1. Bilgisayar düzeyinde dosya.
1. Kullanıcı düzeyinde dosya.
1. İle belirtilen dosyayı `-configFile`.
1. Her sürücünün kök yolu geçerli bir klasöre (burada nuget.exe çağrılan veya Visual Studio projeyi içeren klasörü) klasöründe bulunan dosyaları. Örneğin, bir komut c:\A\B\C çağrılırsa, NuGet arar ve c: yapılandırma dosyalarını yükler\, ardından c:\A, ardından c:\A\B ve son olarak c:\A\B\C.

NuGet içinde bu dosyaları ayarları buldukça, şu şekilde uygulanır:

1. Tek öğeli öğeleri için aynı anahtar için herhangi bir önceden bulunan değer NuGet değiştirildi. Başka bir deyişle, "geçerli klasör veya proje için en yakın" ayarları daha önce bulunan diğerleri geçersiz kılar. Örneğin, `defaultPushSource` ayarı `NuGetDefaults.Config` varsa başka bir yapılandırma dosyasında geçersiz kılınır.

1. Koleksiyon öğeleri için (gibi `<packageSources>`), NuGet tüm yapılandırma dosyalarını değerleri tek bir koleksiyon birleştirir.

1. Zaman `<clear />` var. belirli bir düğümde, NuGet bu düğüm için daha önce tanımlanan yapılandırma değerleri yok sayar.

### <a name="settings-walkthrough"></a>Ayarları gözden geçirme

İki ayrı sürücülere aşağıdaki klasör yapısına sahip varsayalım:

    disk_drive_1
        User
    disk_drive_2
       Project1
         Source
       Project2
         Source
       tmp

Ardından dört sahip `NuGet.Config` dosyaları aşağıdaki konumlarda verilen içeriğe sahip. (Bilgisayar düzeyinde dosya bu örnekte yer almaz, ancak kullanıcı düzeyi dosyasına benzer şekilde davranır.)

A. kullanıcı düzeyi dosyası, (`%appdata%\NuGet\NuGet.Config` , Windows üzerinde `~/.config/NuGet/NuGet.Config` Mac/Linux üzerinde):

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

File B. disk_drive_2/NuGet.Config:

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

File C. disk_drive_2/Project1/NuGet.Config:

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

File D. disk_drive_2/Project2/NuGet.Config:

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

NuGet sonra yükler ve gösterildiği gibi burada çağrılan bağlı olarak ayarlarını uygular:

- **Disk_drive_1/kullanıcılardan çağrılan**: (A) kullanıcı düzeyi yapılandırma dosyasında listelenen varsayılan depo, üzerinde disk_drive_1 bulunan tek dosya olduğundan kullanılır.

- **Disk_drive_2 çağrılan / veya disk_drive_/tmp**: Kullanıcı düzeyinde dosya ilk olarak yüklenir (A) sonra NuGet disk_drive_2 köküne gider ve bulur (B) dosya. NuGet, ayrıca bir yapılandırma dosyası/tmp dizininde arar ancak bir bulamaz. Sonuç olarak, varsayılan depo nuget.org üzerinde kullanıldığında, paket geri yükleme etkin ve paketleri disk_drive_2/tmp genişletilmiş.

- **Disk_drive_2/Project1 veya disk_drive_2/Project1/kaynağından çağrılan**: NuGet yükleri dosyası (B) kökünden disk_drive_2, ardından daha sonra (C) kullanıcı düzeyinde dosyanın ilk olarak yüklenir (A). (C) ayarları geçersiz kılar (B) ve (A), böylece `repositoryPath` disk_drive_2/Project1/dış/paketleri yerine olan paketleri nereye yükleneceğini *disk_drive_2/tmp*. Ayrıca, (C) temizler çünkü `<packageSources>`, nuget.org çıkmadan yalnızca bir kaynak olarak kullanılabilir artık `https://MyPrivateRepo/ES/nuget`.

- **Disk_drive_2/Project2 veya disk_drive_2/Project2/kaynağından çağrılan**: Kullanıcı düzeyinde dosyanın ilk dosyası (B) ve (D) dosya ardından yüklenir (A). Çünkü `packageSources` değil işaretli değilse, her ikisi de `nuget.org` ve `https://MyPrivateRepo/DQ/nuget` kaynakları olarak kullanılabilir. Paketleri disk_drive_2/tmp (B) belirtilen Genişletilmiş.

## <a name="nuget-defaults-file"></a>NuGet Varsayılanları dosyası

`NuGetDefaults.Config` İçinden paketleri yüklü ve güncelleştirilmiş paket kaynaklarını belirtin ve paketlerle yayımlamak için varsayılan hedef denetlemek için dosya var. `nuget push`. Yöneticiler bir kolayca, çünkü (örneğin, Grup İlkesi kullanarak) tutarlı dağıtma `NuGetDefaults.Config` dosya Geliştirici ve derleme makinesi, bunlar sağlayabilirsiniz kuruluşunuzdaki herkes nuget.org yerine doğru paket kaynaklarını kullanıyor.

> [!Important]
> `NuGetDefaults.Config` Dosya hiçbir zaman bir geliştiricinin NuGet yapılandırmasından kaldırılacak paket kaynağını neden olur. Geliştirici NuGet zaten kullandı ve bu nedenle nuget.org paket kaynağı olan anlamına kayıtlı, oluşturulmasından sonra kaldırılmaz bir `NuGetDefaults.Config` dosya.
>
> Ayrıca, ne `NuGetDefaults.Config` ya da başka bir mekanizma nuget'te nuget.org gibi paket kaynaklarına erişimi engelleyebilirsiniz. Bir kuruluşun bu tür erişimin engellenmesini sağlayan isterse, güvenlik duvarları gibi başka bir yolla Bunu yapmak için kullanmanız gerekir.

### <a name="nugetdefaultsconfig-location"></a>NuGetDefaults.Config konumu

Aşağıdaki tablo nerede tanımlar `NuGetDefaults.Config` dosya depolanması, hedef işletim sistemi bağlı olarak:

| İşletim sistemi platformu  | NuGetDefaults.Config konumu |
| --- | --- |
| Windows      | **Visual Studio 2017 veya NuGet 4.x+:** `%ProgramFiles(x86)%\NuGet\Config` <br />**Visual Studio 2015 veya önceki veya NuGet 3.x ve önceki sürümleri:** `%PROGRAMDATA%\NuGet` |
| Mac/Linux    | `$XDG_DATA_HOME` (genellikle `~/.local/share` veya `/usr/local/share`işletim sistemi dağıtım bağlı olarak)|

### <a name="nugetdefaultsconfig-settings"></a>NuGetDefaults.Config ayarları

- `packageSources`: Bu koleksiyona sahip aynı anlamı `packageSources` normal olarak yapılandırma dosyaları ve varsayılan kaynakları belirtir. NuGet yüklerken veya güncellerken kullanarak projelerinde paketler sırayla kaynakları kullanan `packages.config` yönetim biçimi. PackageReference biçimini kullanarak projeleri için NuGet öncelikle yerel kaynakları kullanır, sonra ağ paylaşımları ve yapılandırma dosyalarını sıraya bakılmaksızın HTTP kaynakları üzerindeki kaynakları. NuGet geri yükleme işlemleri kaynaklarıyla sırasını her zaman yok sayar.

- `disabledPackageSources`: Bu koleksiyon da aynı olarak anlamı `NuGet.Config` burada her etkilenen kaynak listelendiğini adını ve gösteren bir true/false değeri tarafından devre dışı bırakılıp bırakılmayacağını dosyaları. Bu kaynak adı ve URL içinde kalmasını sağlar `packageSources` zorunda kalmadan, varsayılan olarak açıktır. Bireysel geliştiriciler daha sonra tekrar etkinleştirebilirsiniz kaynak kaynağın diğer yanlış ayarlayarak `NuGet.Config` doğru URL'yi yeniden bulmak zorunda kalmadan dosyaları. Ayrıca varsayılan olarak yalnızca tek bir takımın kaynak etkinleştirme sırasında bir kuruluş için iç kaynak URL'lerin tam listesini geliştiricilere sağlamak kullanışlıdır.

- `defaultPushSource`: varsayılan hedefi belirleyen `nuget push` nuget.org yerleşik varsayılan geçersiz kılma işlemleri. Yöneticiler, iç paketler için genel nuget.org yanlışlıkla, yayımlama önlemek için bu ayarı dağıtabilir, geliştiriciler özel olarak kullanılacak gerektiği `nuget push -Source` nuget.org için yayımlanacak.

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
