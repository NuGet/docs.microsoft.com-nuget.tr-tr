---
title: Ortak NuGet yapılandırması
description: NuGet. config dosyaları, NuGet 'in hem genel hem de proje başına temelinde denetimini denetler ve NuGet yapılandırma komutuyla değiştirilir.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: conceptual
ms.openlocfilehash: 5309d94fafea9cdfc3699d443393be5d381dd145
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317727"
---
# <a name="common-nuget-configurations"></a>Ortak NuGet yapılandırması

NuGet davranışı, proje, Kullanıcı ve bilgisayar genelindeki düzeylerde bulunabilir bir veya `NuGet.Config` daha fazla (XML) dosyada birikmiş ayarlar tarafından yönlendirilir. Genel `NuGetDefaults.Config` bir dosya Ayrıca paket kaynaklarını özellikle yapılandırır. Ayarlar, CLı, Paket Yöneticisi konsolu ve Paket Yöneticisi Kullanıcı arabiriminde verilen tüm komutlara uygulanır.

## <a name="config-file-locations-and-uses"></a>Yapılandırma dosyası konumları ve kullanımları

| Kapsam | NuGet. config dosyası konumu | Açıklama |
| --- | --- | --- |
| Çözüm | Geçerli klasör (diğer adıyla, çözüm klasörü) veya sürücü köküne kadar herhangi bir klasör.| Bir çözüm klasöründe, ayarlar alt klasörlerdeki tüm projelere uygulanır. Bir yapılandırma dosyası bir proje klasörüne yerleştirilmişse, projenin bu proje üzerinde hiçbir etkisi olmadığını unutmayın. |
| Kullanıcı | Windows: `%appdata%\NuGet\NuGet.Config`<br/>Mac/Linux: `~/.config/NuGet/NuGet.Config` veya `~/.nuget/NuGet/NuGet.Config` (OS dağıtımına göre farklılık gösterir) | Ayarlar tüm işlemlere uygulanır, ancak proje düzeyindeki tüm ayarlar tarafından geçersiz kılınır. |
| Bilgisayar | Windows: `%ProgramFiles(x86)%\NuGet\Config`<br/>Mac/Linux: `$XDG_DATA_HOME`. Null veya boş ise ya `/usr/local/share` da `~/.local/share` kullanılacaksa (OS dağıtımına göre değişir) `$XDG_DATA_HOME`  | Ayarlar bilgisayardaki tüm işlemlere uygulanır, ancak herhangi bir kullanıcı veya proje düzeyi ayar tarafından geçersiz kılınır. |

NuGet 'in önceki sürümleri için notlar:
- NuGet 3,3 ve önceki sürümleri çözüm `.nuget` genelinde ayarlar için bir klasör kullandı. Bu dosya NuGet 3.4 + ' de kullanılmaz.
- NuGet 2,6 için 3. x, Windows üzerindeki bilgisayar\\düzeyi yapılandırma dosyası%ProgramData%\nuget\config [{IDE} [\\{Version} [\\{SKU}]]] \nuget.exe konumunda konumlandı; burada *{IDE}* *VisualStudio*olabilir, *{ Version}* , *14,0*gibi Visual Studio Sürümiydi ve *{SKU}* *Community*, *Pro*ya da *Enterprise*. Ayarları NuGet 4.0 + ' ya geçirmek için yapılandırma dosyasını% ProgramFiles (x86)% \ Nuget\configkonumuna kopyalamanız yeterlidir. Linux 'ta, bu önceki konum/etc/opt ve Mac üzerinde/Library/Application Support desteği idi.

## <a name="changing-config-settings"></a>Yapılandırma ayarlarını değiştirme

Dosya, [NuGet yapılandırma ayarları](../reference/nuget-config-file.md) konusunda açıklandığı gibi anahtar/değer çiftlerini içeren basit bir XML metin dosyasıdır. `NuGet.Config`

Ayarlar, NuGet CLı [yapılandırma komutu](../reference/cli-reference/cli-ref-config.md)kullanılarak yönetilir:
- Varsayılan olarak, değişiklikler Kullanıcı düzeyi yapılandırma dosyasında yapılır.
- Farklı bir dosyadaki ayarları değiştirmek için `-configFile` anahtarını kullanın. Bu durumda, dosyalar herhangi bir dosya adını kullanabilir.
- Anahtarlar her zaman büyük/küçük harfe duyarlıdır.
- Bilgisayar düzeyi ayarları dosyasındaki ayarları değiştirmek için yükseltme gereklidir.

> [!Warning]
> Dosyayı herhangi bir metin düzenleyicisinde değiştirebilseniz de, NuGet (v 3.4.3 ve üzeri), hatalı biçimlendirilmiş XML (eşleşmeyen Etiketler, geçersiz tırnak işaretleri vb.) içeriyorsa tüm yapılandırma dosyalarını sessizce yoksayar. Bu, ayarının kullanılarak `nuget config`yönetilmesi tercih edilir.

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
> NuGet 3,4 ve üzeri sürümlerde, (Windows) ve `repositoryPath=%PACKAGEHOME%` `repositoryPath=$PACKAGEHOME` (Mac/Linux) içinde olduğu gibi, ortam değişkenlerini herhangi bir değer içinde kullanabilirsiniz.

### <a name="removing-a-value"></a>Değer kaldırma

Bir değeri kaldırmak için, boş bir değere sahip bir anahtar belirtin.

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a>Yeni bir yapılandırma dosyası oluşturma

Aşağıdaki şablonu yeni dosyaya kopyalayın ve ardından değerleri ayarlamak için kullanın `nuget config -configFile <filename>` :

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a>Ayarlar nasıl uygulanır

Birden `NuGet.Config` çok dosya, tek bir projeye, bir proje grubuna veya tüm projelere uygulanabilmeleri için ayarları farklı konumlarda depolamanızı sağlar. Bu ayarlar, bir projeye veya geçerli klasöre "en yakın" olan ayarlar ile, komut satırından veya Visual Studio 'dan çağrılan herhangi bir NuGet işleminde toplu olarak uygulanır.

Özellikle, NuGet ayarları farklı yapılandırma dosyalarından aşağıdaki sırada yükler:

1. Yalnızca paket kaynaklarıyla ilgili ayarları içeren [Nugetdefaults. config dosyası](#nuget-defaults-file).
1. Bilgisayar düzeyindeki dosya.
1. Kullanıcı düzeyi dosyası.
1. İle `-configFile`belirtilen dosya.
1. Sürücü kökünden geçerli klasöre (NuGet. exe ' nin çağrıldığı veya Visual Studio projesini içeren klasör) yoldaki her klasörde bulunan dosyalar. Örneğin, bir komut c:\a\b\c içinde çağrılırsa, NuGet yapılandırma dosyalarını şuna bakar ve yükler:\, c:\a, ardından c:\A\B ve son olarak c:\a\b\c.

NuGet bu dosyalardaki ayarları bulduğundan, bunlar aşağıdaki gibi uygulanır:

1. Tek öğe öğelerinde, NuGet aynı anahtar için önceden bulunan tüm değeri değiştirdi. Bu, geçerli klasöre veya projeye "en yakın" olan ayarların daha önce bulduğu diğer tüm diğerlerini geçersiz kıldığı anlamına gelir. Örneğin, `defaultPushSource` içindeki `NuGetDefaults.Config` ayarı başka herhangi bir yapılandırma dosyasında varsa geçersiz kılınır.

1. Koleksiyon öğeleri (gibi `<packageSources>`) için, NuGet tüm yapılandırma dosyalarındaki değerleri tek bir koleksiyon olarak birleştirir.

1. Belirli `<clear />` bir düğüm için olduğunda, NuGet bu düğüm için önceden tanımlanmış yapılandırma değerlerini yoksayar.

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

Ardından, belirtilen içeriğe `NuGet.Config` sahip aşağıdaki konumlarda dört dosya vardır. (Bilgisayar düzeyindeki dosya bu örneğe dahil değildir, ancak kullanıcı düzeyindeki dosyada benzer şekilde davranır.)

Dosya A. Kullanıcı düzeyi dosyası, (`%appdata%\NuGet\NuGet.Config` Windows 'ta, `~/.config/NuGet/NuGet.Config` Mac 'te/Linux 'ta):

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

Dosya B. disk_drive_2/NuGet. config:

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

C. disk_drive_2/Project1/NuGet. config dosyası:

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

D. disk_drive_2/Project2/NuGet. config dosyası:

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

- **Disk_drive_1/kullanıcılarından çağrılır**: Yalnızca Kullanıcı düzeyi yapılandırma dosyasında (A) listelenen varsayılan depo, disk_drive_1 konumunda bulunan tek dosya olduğu için kullanılır.

- **Disk_drive_2/veya disk_drive_/tmp öğesinden çağrılır**: Önce Kullanıcı düzeyi dosya (A) yüklenir, ardından NuGet disk_drive_2 köküne gider ve dosyayı bulur (B). NuGet Ayrıca/tmp ' de bir yapılandırma dosyası arar ancak bir tane bulmaz. Sonuç olarak, nuget.org üzerindeki varsayılan depo kullanılır, paket geri yükleme etkinleştirilir ve paketler disk_drive_2/tmp içinde genişletilir.

- **Disk_drive_2/Project1 veya disk_drive_2/Project1/Source öğesinden çağrılır**: Önce Kullanıcı düzeyi dosya (A) yüklenir, ardından NuGet dosyayı (B) disk_drive_2 kökünün kökünden sonra dosyayı (C) yükler. (C) içindeki ayarlar, (B) ve (A) içindeki ayarları geçersiz kılar, `repositoryPath` bu nedenle paketlerin yüklendiği yer, *disk_drive_2/tmp*yerine disk_drive_2/Project1/External/Packages. Ayrıca, (C) temizleyen `<packageSources>`, NuGet.org artık yalnızca `https://MyPrivateRepo/ES/nuget`bir kaynak olarak kullanılamaz.

- **Disk_drive_2/Project2 veya disk_drive_2/Project2/Source öğesinden çağrılır**: Önce dosya (B) ve dosya (D) tarafından izlenen Kullanıcı düzeyi dosya (A) yüklenir. Temizlenmediği `nuget.org` için`https://MyPrivateRepo/DQ/nuget` her ikisi de kaynak olarak kullanılabilir. `packageSources` Paketler, (B) içinde belirtilen disk_drive_2/tmp içinde genişletilir.

## <a name="nuget-defaults-file"></a>NuGet Varsayılanları dosyası

Dosya, paketlerin yüklendiği ve güncelleştirildiği paket kaynaklarını belirtmek ve paketleri ile `nuget push`yayımlamak için varsayılan hedefi denetlemek için vardır. `NuGetDefaults.Config` Yöneticiler uygun bir şekilde (örneğin Grup İlkesi kullanarak) geliştirici ve derleme makineleri `NuGetDefaults.Config` için tutarlı dosyalar dağıtıp, kuruluştaki herkesin NuGet.org yerine doğru paket kaynaklarını kullandığından emin olabilirler.

> [!Important]
> `NuGetDefaults.Config` Dosya hiçbir şekilde bir geliştiricinin NuGet yapılandırmasından bir paket kaynağının kaldırılmasına neden olmaz. Yani, geliştirici zaten NuGet kullanıyorsa ve bu nedenle NuGet.org paket kaynağı kayıtlıysa, bir `NuGetDefaults.Config` Dosya oluşturulduktan sonra kaldırılmaz.
>
> Ayrıca, NuGet `NuGetDefaults.Config` 'deki başka hiçbir mekanizma, NuGet.org gibi paket kaynaklarına erişimi engelleyebilir. Bir kuruluş söz konusu erişimi engellemeyi istiyorsa, bunun için güvenlik duvarları gibi diğer yollarla kullanılması gerekir.

### <a name="nugetdefaultsconfig-location"></a>NuGetDefaults. config konumu

Aşağıdaki tabloda, hedef işletim sistemine `NuGetDefaults.Config` bağlı olarak dosyanın depolanacağı konum açıklanmaktadır:

| İşletim sistemi platformu  | NuGetDefaults. config konumu |
| --- | --- |
| Windows      | **Visual Studio 2017 veya NuGet 4. x +:** `%ProgramFiles(x86)%\NuGet\Config` <br />**Visual Studio 2015 ve öncesi ya da NuGet 3. x ve öncesi:** `%PROGRAMDATA%\NuGet` |
| Mac/Linux    | `$XDG_DATA_HOME`(genellikle `~/.local/share` veya `/usr/local/share`, işletim sistemi dağıtımına bağlı olarak)|

### <a name="nugetdefaultsconfig-settings"></a>NuGetDefaults. config ayarları

- `packageSources`: Bu koleksiyon, normal yapılandırma dosyaları ile `packageSources` aynı anlama sahiptir ve varsayılan kaynakları belirtir. NuGet, `packages.config` yönetim biçimini kullanarak projelerdeki paketleri yükleme veya güncelleştirme sırasında kaynakları kullanır. , PackageReference biçimini kullanan projeler için, NuGet önce yerel kaynakları, ardından ağ paylaşımlarında kaynakları, sonra da yapılandırma dosyalarındaki sıra ne olursa olsun HTTP kaynaklarını kullanır. NuGet, geri yükleme işlemlerine sahip kaynakların sırasını her zaman yoksayar.

- `disabledPackageSources`: Bu koleksiyonda ayrıca, etkilenen her kaynağın adı ve `NuGet.Config` devre dışı olup olmadığını gösteren bir doğru/yanlış değeri tarafından listelenen dosyalardaki gibi aynı anlamı vardır. Bu, kaynak adının ve URL 'nin varsayılan olarak açık `packageSources` olmadan ' de kalmasına izin verir. Bireysel geliştiriciler daha sonra doğru URL 'yi bulmaya gerek kalmadan kaynağın değerini diğer `NuGet.Config` dosyalardaki false olarak ayarlayarak kaynağı yeniden etkinleştirebilir. Bu, geliştiricilere yalnızca bireysel ekibin kaynağını varsayılan olarak etkinleştirirken bir kuruluşun iç kaynak URL 'lerinin tam listesini sağlamak için de kullanışlıdır.

- `defaultPushSource`: NuGet.org 'in yerleşik varsayılan öğesini `nuget push` geçersiz kılarak, işlemler için varsayılan hedefi belirtir. Yöneticiler, özellikle NuGet.org ' de yayımlamak için kullanması `nuget push -Source` gerektiği için, şirket içi paketlerin yanlışlıkla yanlışlıkla, genel NuGet.org yayınlanmasını önlemek üzere bu ayarı dağıtabilir.

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
