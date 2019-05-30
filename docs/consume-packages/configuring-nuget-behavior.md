---
title: NuGet davranışını yapılandırma
description: NuGet.Config dosyaları hem genel hem de proje başına temelinde NuGet davranışını denetleyen ve nuget config komutu ile değiştirilir.
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: conceptual
ms.openlocfilehash: 963d1d59ea7e65e3d75bc7105b8864e3e4045938
ms.sourcegitcommit: ef08f376688f0191a8d3d873b6a4386afd799373
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/28/2019
ms.locfileid: "66266345"
---
# <a name="configuring-nuget-behavior"></a><span data-ttu-id="23784-103">NuGet davranışını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="23784-103">Configuring NuGet behavior</span></span>

<span data-ttu-id="23784-104">NuGet'ın davranışı, bir veya daha fazla birikmiş ayarları tarafından yönlendirilir `NuGet.Config` proje-, kullanıcı- ve bilgisayar genelinde düzeyinde bulunabilir (XML) dosyaları.</span><span class="sxs-lookup"><span data-stu-id="23784-104">NuGet's behavior is driven by the accumulated settings in one or more `NuGet.Config` (XML) files that can exist at project-, user-, and computer-wide levels.</span></span> <span data-ttu-id="23784-105">Genel bir `NuGetDefaults.Config` dosyası, özellikle de paket kaynaklarını yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="23784-105">A global `NuGetDefaults.Config` file also specifically configures package sources.</span></span> <span data-ttu-id="23784-106">CLI, Paket Yöneticisi konsolu ve Paket Yöneticisi UI tüm komutlar için ayarları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="23784-106">Settings apply to all commands issued in the CLI, the Package Manager Console, and the Package Manager UI.</span></span>

## <a name="config-file-locations-and-uses"></a><span data-ttu-id="23784-107">Config dosya konumları ve kullanır</span><span class="sxs-lookup"><span data-stu-id="23784-107">Config file locations and uses</span></span>

| <span data-ttu-id="23784-108">Kapsam</span><span class="sxs-lookup"><span data-stu-id="23784-108">Scope</span></span> | <span data-ttu-id="23784-109">NuGet.Config dosyası konumu</span><span class="sxs-lookup"><span data-stu-id="23784-109">NuGet.Config file location</span></span> | <span data-ttu-id="23784-110">Açıklama</span><span class="sxs-lookup"><span data-stu-id="23784-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="23784-111">Çözüm</span><span class="sxs-lookup"><span data-stu-id="23784-111">Solution</span></span> | <span data-ttu-id="23784-112">Geçerli klasör (Çözüm klasörü olarak da bilinir) veya sürücü kök kadar herhangi bir klasör.</span><span class="sxs-lookup"><span data-stu-id="23784-112">Current folder (aka Solution folder) or any folder up to the drive root.</span></span>| <span data-ttu-id="23784-113">Bir çözüm klasöründe ayarları uygulamak klasörlerdeki tüm projeler için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="23784-113">In a solution folder, settings apply apply to all projects in subfolders.</span></span> <span data-ttu-id="23784-114">Bir yapılandırma dosyası bir proje klasörüne konur, proje üzerinde etkiye sahip olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="23784-114">Note that if a config file is placed in a project folder, it has no effect on that project.</span></span> |
| <span data-ttu-id="23784-115">Kullanıcı</span><span class="sxs-lookup"><span data-stu-id="23784-115">User</span></span> | <span data-ttu-id="23784-116">Windows: `%appdata%\NuGet\NuGet.Config`</span><span class="sxs-lookup"><span data-stu-id="23784-116">Windows: `%appdata%\NuGet\NuGet.Config`</span></span><br/><span data-ttu-id="23784-117">Mac/Linux: `~/.config/NuGet/NuGet.Config` veya `~/.nuget/NuGet/NuGet.Config` (işletim sistemi dağıtım göre değişiklik gösterir)</span><span class="sxs-lookup"><span data-stu-id="23784-117">Mac/Linux: `~/.config/NuGet/NuGet.Config` or `~/.nuget/NuGet/NuGet.Config` (varies by OS distribution)</span></span> | <span data-ttu-id="23784-118">Ayarları tüm işlemler için geçerlidir, ancak herhangi bir proje düzeyi ayarı tarafından geçersiz kılınır.</span><span class="sxs-lookup"><span data-stu-id="23784-118">Settings apply to all operations, but are overridden by any project-level settings.</span></span> |
| <span data-ttu-id="23784-119">Bilgisayar</span><span class="sxs-lookup"><span data-stu-id="23784-119">Computer</span></span> | <span data-ttu-id="23784-120">Windows: `%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="23784-120">Windows: `%ProgramFiles(x86)%\NuGet\Config`</span></span><br/><span data-ttu-id="23784-121">Mac/Linux: `$XDG_DATA_HOME`.</span><span class="sxs-lookup"><span data-stu-id="23784-121">Mac/Linux: `$XDG_DATA_HOME`.</span></span> <span data-ttu-id="23784-122">Varsa `$XDG_DATA_HOME` null veya boş `~/.local/share` veya `/usr/local/share` kullanılacak (işletim sistemi dağıtım göre değişiklik gösterir)</span><span class="sxs-lookup"><span data-stu-id="23784-122">If `$XDG_DATA_HOME` is null or empty, `~/.local/share` or `/usr/local/share` will be used (varies by OS distribution)</span></span>  | <span data-ttu-id="23784-123">Ayarları bilgisayar üzerindeki tüm işlemler için geçerlidir, ancak herhangi bir kullanıcı veya proje düzeyi ayarı tarafından geçersiz kılınır.</span><span class="sxs-lookup"><span data-stu-id="23784-123">Settings apply to all operations on the computer, but are overridden by any user- or project-level settings.</span></span> |

<span data-ttu-id="23784-124">NuGet'ın önceki sürümleri için Notlar:</span><span class="sxs-lookup"><span data-stu-id="23784-124">Notes for earlier versions of NuGet:</span></span>
- <span data-ttu-id="23784-125">NuGet 3.3 ve daha önce kullanılmış bir `.nuget` çözüm genelindeki ayarları için klasör.</span><span class="sxs-lookup"><span data-stu-id="23784-125">NuGet 3.3 and earlier used a `.nuget` folder for solution-wide settings.</span></span> <span data-ttu-id="23784-126">Bu dosya NuGet 3.4 + kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="23784-126">This file is not used in NuGet 3.4+.</span></span>
- <span data-ttu-id="23784-127">3.x için NuGet 2.6 için Windows bilgisayar düzeyinde yapılandırma dosyasını % ProgramData%\NuGet\Config konumunda [\\{IDE} [\\{Version} [\\{SKU}]]]\NuGet.Config, burada *{IDE}* olabilir *VisualStudio*, *{Version}* gibi Visual Studio sürümü olan *14.0*, ve *{SKU}* ya da *topluluk*, *Pro*, veya *Kurumsal*.</span><span class="sxs-lookup"><span data-stu-id="23784-127">For NuGet 2.6 to 3.x, the computer-level config file on Windows was located in %ProgramData%\NuGet\Config[\\{IDE}[\\{Version}[\\{SKU}]]]\NuGet.Config, where *{IDE}* can be *VisualStudio*, *{Version}* was the Visual Studio version such as *14.0*, and *{SKU}* is either *Community*, *Pro*, or *Enterprise*.</span></span> <span data-ttu-id="23784-128">İçin NuGet 4.0 + ayarlarını geçirmek için yapılandırma dosyası için % ProgramFiles(x86) % \NuGet\Config kopyalayın. Linux üzerinde /etc/opt, önceki bu konumda olan ve Mac'te Library/Application Support.</span><span class="sxs-lookup"><span data-stu-id="23784-128">To migrate settings to NuGet 4.0+, simply copy the config file to %ProgramFiles(x86)%\NuGet\Config. On Linux, this previous location was /etc/opt, and on Mac, /Library/Application Support.</span></span>

## <a name="changing-config-settings"></a><span data-ttu-id="23784-129">Yapılandırma ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="23784-129">Changing config settings</span></span>

<span data-ttu-id="23784-130">A `NuGet.Config` dosyasıdır açıklandığı gibi anahtar/değer çiftleri içeren basit bir XML metin dosyasını [NuGet yapılandırma ayarlarını](../reference/nuget-config-file.md) konu.</span><span class="sxs-lookup"><span data-stu-id="23784-130">A `NuGet.Config` file is a simple XML text file containing key/value pairs as described in the [NuGet Configuration Settings](../reference/nuget-config-file.md) topic.</span></span>

<span data-ttu-id="23784-131">Ayarları NuGet CLI'yı kullanarak yönetilen [config komutu](../tools/cli-ref-config.md):</span><span class="sxs-lookup"><span data-stu-id="23784-131">Settings are managed using the NuGet CLI [config command](../tools/cli-ref-config.md):</span></span>
- <span data-ttu-id="23784-132">Varsayılan olarak, kullanıcı düzeyinde yapılandırma dosyasına değişiklikler yapılır.</span><span class="sxs-lookup"><span data-stu-id="23784-132">By default, changes are made to the user-level config file.</span></span>
- <span data-ttu-id="23784-133">Farklı bir dosya ayarlarını değiştirmek için kullanın `-configFile` geçin.</span><span class="sxs-lookup"><span data-stu-id="23784-133">To change settings in a different file, use the `-configFile` switch.</span></span> <span data-ttu-id="23784-134">Bu durumda dosyalarını dosya kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="23784-134">In this case files can use any filename.</span></span>
- <span data-ttu-id="23784-135">Anahtarları her zaman büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="23784-135">Keys are always case sensitive.</span></span>
- <span data-ttu-id="23784-136">Bilgisayar düzeyinde ayarlar dosyasındaki ayarları değiştirmek için yükseltme gereklidir.</span><span class="sxs-lookup"><span data-stu-id="23784-136">Elevation is required to change settings in the computer-level settings file.</span></span>

> [!Warning]
> <span data-ttu-id="23784-137">Dosyasını bir metin düzenleyicisinde NuGet yapılandırabilseniz (v3.4.3 ve üzeri) hatalı biçimlendirilmiş XML (eşleşmeyen etiketleri, geçersiz bir tırnak işareti, vb.) içeriyorsa, tüm yapılandırma dosyası sessizce yoksayar.</span><span class="sxs-lookup"><span data-stu-id="23784-137">Although you can modify the file in any text editor, NuGet (v3.4.3 and later) silently ignores the entire configuration file if it contains malformed XML (mismatched tags, invalid quotation marks, etc.).</span></span> <span data-ttu-id="23784-138">Bu nedenle kullanarak yönetmek için tercih edilir, `nuget config`.</span><span class="sxs-lookup"><span data-stu-id="23784-138">This is why it's preferable to manage setting using `nuget config`.</span></span>

### <a name="setting-a-value"></a><span data-ttu-id="23784-139">Bir değer ayarlama</span><span class="sxs-lookup"><span data-stu-id="23784-139">Setting a value</span></span>

<span data-ttu-id="23784-140">Windows:</span><span class="sxs-lookup"><span data-stu-id="23784-140">Windows:</span></span>

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\Config\NuGet.Config
```

<span data-ttu-id="23784-141">Mac/Linux:</span><span class="sxs-lookup"><span data-stu-id="23784-141">Mac/Linux:</span></span>

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
> <span data-ttu-id="23784-142">NuGet 3.4 ve üzeri gibi herhangi bir değer olarak ortam değişkenlerini kullanabilirsiniz `repositoryPath=%PACKAGEHOME%` (Windows) ve `repositoryPath=$PACKAGEHOME` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="23784-142">In NuGet 3.4 and later you can use environment variables in any value, as in `repositoryPath=%PACKAGEHOME%` (Windows) and `repositoryPath=$PACKAGEHOME` (Mac/Linux).</span></span>

### <a name="removing-a-value"></a><span data-ttu-id="23784-143">Bir değer kaldırılıyor</span><span class="sxs-lookup"><span data-stu-id="23784-143">Removing a value</span></span>

<span data-ttu-id="23784-144">Bir değer kaldırmak için bir anahtar ile boş bir değer belirtin.</span><span class="sxs-lookup"><span data-stu-id="23784-144">To remove a value, specify a key with an empty value.</span></span>

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a><span data-ttu-id="23784-145">Yeni bir yapılandırma dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="23784-145">Creating a new config file</span></span>

<span data-ttu-id="23784-146">Şablon aşağıdaki yeni dosyaya kopyalayın ve ardından `nuget config -configFile <filename>` değerlerini ayarlamak için:</span><span class="sxs-lookup"><span data-stu-id="23784-146">Copy the template below into the new file and then use `nuget config -configFile <filename>` to set values:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a><span data-ttu-id="23784-147">Ayarları nasıl uygulanır</span><span class="sxs-lookup"><span data-stu-id="23784-147">How settings are applied</span></span>

<span data-ttu-id="23784-148">Birden çok `NuGet.Config` dosyaları tek bir proje, projelerin bir grup veya tüm projeler için geçerli olacak şekilde farklı konumlarda ayarlarını depolamak izin verir.</span><span class="sxs-lookup"><span data-stu-id="23784-148">Multiple `NuGet.Config` files allow you to store settings in different locations so that they apply to a single project, a group of projects, or all projects.</span></span> <span data-ttu-id="23784-149">Bu ayarlar, topluca "yakın.", bir proje ya da Öncelik Alma geçerli klasörde mevcut ayarlarla komut satırından veya Visual Studio'dan çağrılmasını herhangi bir NuGet işlemi için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="23784-149">These settings collectively apply to any NuGet operation invoked from the command line or from Visual Studio, with settings that exist "closest" to a project or the current folder taking precedence.</span></span>

<span data-ttu-id="23784-150">Özellikle, NuGet aşağıdaki sırayla farklı bir yapılandırma dosyalarından ayarları yükler:</span><span class="sxs-lookup"><span data-stu-id="23784-150">Specifically, NuGet loads settings from the different config files in the following order:</span></span>

1. <span data-ttu-id="23784-151">[NuGetDefaults.Config dosya](#nuget-defaults-file), yalnızca paket kaynaklarını ilgili ayarları içerir.</span><span class="sxs-lookup"><span data-stu-id="23784-151">The [NuGetDefaults.Config file](#nuget-defaults-file), which contains settings related only to package sources.</span></span>
1. <span data-ttu-id="23784-152">Bilgisayar düzeyinde dosya.</span><span class="sxs-lookup"><span data-stu-id="23784-152">The computer-level file.</span></span>
1. <span data-ttu-id="23784-153">Kullanıcı düzeyinde dosya.</span><span class="sxs-lookup"><span data-stu-id="23784-153">The user-level file.</span></span>
1. <span data-ttu-id="23784-154">İle belirtilen dosyayı `-configFile`.</span><span class="sxs-lookup"><span data-stu-id="23784-154">The file specified with `-configFile`.</span></span>
1. <span data-ttu-id="23784-155">Her sürücünün kök yolu geçerli bir klasöre (burada nuget.exe çağrılan veya Visual Studio projeyi içeren klasörü) klasöründe bulunan dosyaları.</span><span class="sxs-lookup"><span data-stu-id="23784-155">Files found in every folder in the path from the drive root to the current folder (where nuget.exe is invoked or the folder containing the Visual Studio project).</span></span> <span data-ttu-id="23784-156">Örneğin, bir komut c:\A\B\C çağrılırsa, NuGet arar ve c: yapılandırma dosyalarını yükler\, ardından c:\A, ardından c:\A\B ve son olarak c:\A\B\C.</span><span class="sxs-lookup"><span data-stu-id="23784-156">For example, if a command is invoked in c:\A\B\C, NuGet looks for and loads config files in c:\, then c:\A, then c:\A\B, and finally c:\A\B\C.</span></span>

<span data-ttu-id="23784-157">NuGet içinde bu dosyaları ayarları buldukça, şu şekilde uygulanır:</span><span class="sxs-lookup"><span data-stu-id="23784-157">As NuGet finds settings in these files, they are applied as follows:</span></span>

1. <span data-ttu-id="23784-158">Tek öğeli öğeleri için aynı anahtar için herhangi bir önceden bulunan değer NuGet değiştirildi.</span><span class="sxs-lookup"><span data-stu-id="23784-158">For single-item elements, NuGet replaced any previously-found value for the same key.</span></span> <span data-ttu-id="23784-159">Başka bir deyişle, "geçerli klasör veya proje için en yakın" ayarları daha önce bulunan diğerleri geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="23784-159">This means that settings that are "closest" to the current folder or project override any others found earlier.</span></span> <span data-ttu-id="23784-160">Örneğin, `defaultPushSource` ayarı `NuGetDefaults.Config` varsa başka bir yapılandırma dosyasında geçersiz kılınır.</span><span class="sxs-lookup"><span data-stu-id="23784-160">For example, the `defaultPushSource` setting in `NuGetDefaults.Config` is overridden if it exists in any other config file.</span></span>

1. <span data-ttu-id="23784-161">Koleksiyon öğeleri için (gibi `<packageSources>`), NuGet tüm yapılandırma dosyalarını değerleri tek bir koleksiyon birleştirir.</span><span class="sxs-lookup"><span data-stu-id="23784-161">For collection elements (such as `<packageSources>`), NuGet combines the values from all configuration files into a single collection.</span></span>

1. <span data-ttu-id="23784-162">Zaman `<clear />` var. belirli bir düğümde, NuGet bu düğüm için daha önce tanımlanan yapılandırma değerleri yok sayar.</span><span class="sxs-lookup"><span data-stu-id="23784-162">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span>

### <a name="settings-walkthrough"></a><span data-ttu-id="23784-163">Ayarları gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="23784-163">Settings walkthrough</span></span>

<span data-ttu-id="23784-164">İki ayrı sürücülere aşağıdaki klasör yapısına sahip varsayalım:</span><span class="sxs-lookup"><span data-stu-id="23784-164">Let's say you have the following folder structure on two separate drives:</span></span>

    disk_drive_1
        User
    disk_drive_2
       Project1
         Source
       Project2
         Source
       tmp

<span data-ttu-id="23784-165">Ardından dört sahip `NuGet.Config` dosyaları aşağıdaki konumlarda verilen içeriğe sahip.</span><span class="sxs-lookup"><span data-stu-id="23784-165">You then have four `NuGet.Config` files in the following locations with the given content.</span></span> <span data-ttu-id="23784-166">(Bilgisayar düzeyinde dosya bu örnekte yer almaz, ancak kullanıcı düzeyi dosyasına benzer şekilde davranır.)</span><span class="sxs-lookup"><span data-stu-id="23784-166">(The computer-level file is not included in this example, but would behave similarly to the user-level file.)</span></span>

<span data-ttu-id="23784-167">A. kullanıcı düzeyi dosyası, (`%appdata%\NuGet\NuGet.Config` , Windows üzerinde `~/.config/NuGet/NuGet.Config` Mac/Linux üzerinde):</span><span class="sxs-lookup"><span data-stu-id="23784-167">File A. User-level file, (`%appdata%\NuGet\NuGet.Config` on Windows, `~/.config/NuGet/NuGet.Config` on Mac/Linux):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="23784-168">File B. disk_drive_2/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="23784-168">File B. disk_drive_2/NuGet.Config:</span></span>

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

<span data-ttu-id="23784-169">File C. disk_drive_2/Project1/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="23784-169">File C. disk_drive_2/Project1/NuGet.Config:</span></span>

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

<span data-ttu-id="23784-170">File D. disk_drive_2/Project2/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="23784-170">File D. disk_drive_2/Project2/NuGet.Config:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

<span data-ttu-id="23784-171">NuGet sonra yükler ve gösterildiği gibi burada çağrılan bağlı olarak ayarlarını uygular:</span><span class="sxs-lookup"><span data-stu-id="23784-171">NuGet then loads and applies settings as follows, depending on where it's invoked:</span></span>

- <span data-ttu-id="23784-172">**Disk_drive_1/kullanıcılardan çağrılan**: (A) kullanıcı düzeyi yapılandırma dosyasında listelenen varsayılan depo, üzerinde disk_drive_1 bulunan tek dosya olduğundan kullanılır.</span><span class="sxs-lookup"><span data-stu-id="23784-172">**Invoked from disk_drive_1/users**: Only the default repository listed in the user-level configuration file (A) is used, because that's the only file found on disk_drive_1.</span></span>

- <span data-ttu-id="23784-173">**Disk_drive_2 çağrılan / veya disk_drive_/tmp**: Kullanıcı düzeyinde dosya ilk olarak yüklenir (A) sonra NuGet disk_drive_2 köküne gider ve bulur (B) dosya.</span><span class="sxs-lookup"><span data-stu-id="23784-173">**Invoked from disk_drive_2/ or disk_drive_/tmp**: The user-level file (A) is loaded first, then NuGet goes to the root of disk_drive_2 and finds file (B).</span></span> <span data-ttu-id="23784-174">NuGet, ayrıca bir yapılandırma dosyası/tmp dizininde arar ancak bir bulamaz.</span><span class="sxs-lookup"><span data-stu-id="23784-174">NuGet also looks for a configuration file in /tmp but does not find one.</span></span> <span data-ttu-id="23784-175">Sonuç olarak, varsayılan depo nuget.org üzerinde kullanıldığında, paket geri yükleme etkin ve paketleri disk_drive_2/tmp genişletilmiş.</span><span class="sxs-lookup"><span data-stu-id="23784-175">As a result, the default repository on nuget.org is used, package restore is enabled, and packages get expanded in disk_drive_2/tmp.</span></span>

- <span data-ttu-id="23784-176">**Disk_drive_2/Project1 veya disk_drive_2/Project1/kaynağından çağrılan**: NuGet yükleri dosyası (B) kökünden disk_drive_2, ardından daha sonra (C) kullanıcı düzeyinde dosyanın ilk olarak yüklenir (A).</span><span class="sxs-lookup"><span data-stu-id="23784-176">**Invoked from disk_drive_2/Project1 or disk_drive_2/Project1/Source**: The user-level file (A) is loaded first, then NuGet loads file (B) from the root of disk_drive_2, followed by file (C).</span></span> <span data-ttu-id="23784-177">(C) ayarları geçersiz kılar (B) ve (A), böylece `repositoryPath` disk_drive_2/Project1/dış/paketleri yerine olan paketleri nereye yükleneceğini *disk_drive_2/tmp*.</span><span class="sxs-lookup"><span data-stu-id="23784-177">Settings in (C) override those in (B) and (A), so the `repositoryPath` where packages get installed is disk_drive_2/Project1/External/Packages instead of *disk_drive_2/tmp*.</span></span> <span data-ttu-id="23784-178">Ayrıca, (C) temizler çünkü `<packageSources>`, nuget.org çıkmadan yalnızca bir kaynak olarak kullanılabilir artık `https://MyPrivateRepo/ES/nuget`.</span><span class="sxs-lookup"><span data-stu-id="23784-178">Also, because (C) clears `<packageSources>`, nuget.org is no longer available as a source leaving only `https://MyPrivateRepo/ES/nuget`.</span></span>

- <span data-ttu-id="23784-179">**Disk_drive_2/Project2 veya disk_drive_2/Project2/kaynağından çağrılan**: Kullanıcı düzeyinde dosyanın ilk dosyası (B) ve (D) dosya ardından yüklenir (A).</span><span class="sxs-lookup"><span data-stu-id="23784-179">**Invoked from disk_drive_2/Project2 or disk_drive_2/Project2/Source**: The user-level file (A) is loaded first followed by file (B) and file (D).</span></span> <span data-ttu-id="23784-180">Çünkü `packageSources` değil işaretli değilse, her ikisi de `nuget.org` ve `https://MyPrivateRepo/DQ/nuget` kaynakları olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="23784-180">Because `packageSources` is not cleared, both `nuget.org` and `https://MyPrivateRepo/DQ/nuget` are available as sources.</span></span> <span data-ttu-id="23784-181">Paketleri disk_drive_2/tmp (B) belirtilen Genişletilmiş.</span><span class="sxs-lookup"><span data-stu-id="23784-181">Packages get expanded in disk_drive_2/tmp as specified in (B).</span></span>

## <a name="nuget-defaults-file"></a><span data-ttu-id="23784-182">NuGet Varsayılanları dosyası</span><span class="sxs-lookup"><span data-stu-id="23784-182">NuGet defaults file</span></span>

<span data-ttu-id="23784-183">`NuGetDefaults.Config` İçinden paketleri yüklü ve güncelleştirilmiş paket kaynaklarını belirtin ve paketlerle yayımlamak için varsayılan hedef denetlemek için dosya var. `nuget push`.</span><span class="sxs-lookup"><span data-stu-id="23784-183">The `NuGetDefaults.Config` file exists to specify package sources from which packages are installed and updated, and to control the default target for publishing packages with `nuget push`.</span></span> <span data-ttu-id="23784-184">Yöneticiler bir kolayca, çünkü (örneğin, Grup İlkesi kullanarak) tutarlı dağıtma `NuGetDefaults.Config` dosya Geliştirici ve derleme makinesi, bunlar sağlayabilirsiniz kuruluşunuzdaki herkes nuget.org yerine doğru paket kaynaklarını kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="23784-184">Because administrators can conveniently (using Group Policy, for example) deploy consistent `NuGetDefaults.Config` files to developer and build machines, they can ensure that everyone in the organization is using the correct package sources rather than nuget.org.</span></span>

> [!Important]
> <span data-ttu-id="23784-185">`NuGetDefaults.Config` Dosya hiçbir zaman bir geliştiricinin NuGet yapılandırmasından kaldırılacak paket kaynağını neden olur.</span><span class="sxs-lookup"><span data-stu-id="23784-185">The `NuGetDefaults.Config` file never causes a package source to be removed from a developer's NuGet configuration.</span></span> <span data-ttu-id="23784-186">Geliştirici NuGet zaten kullandı ve bu nedenle nuget.org paket kaynağı olan anlamına kayıtlı, oluşturulmasından sonra kaldırılmaz bir `NuGetDefaults.Config` dosya.</span><span class="sxs-lookup"><span data-stu-id="23784-186">That means if the developer has already used NuGet and therefore has the nuget.org package source registered, it won't be removed after the creation of a `NuGetDefaults.Config` file.</span></span>
>
> <span data-ttu-id="23784-187">Ayrıca, ne `NuGetDefaults.Config` ya da başka bir mekanizma nuget'te nuget.org gibi paket kaynaklarına erişimi engelleyebilirsiniz. Bir kuruluşun bu tür erişimin engellenmesini sağlayan isterse, güvenlik duvarları gibi başka bir yolla Bunu yapmak için kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="23784-187">Furthermore, neither `NuGetDefaults.Config` nor any other mechanism in NuGet can prevent access to package sources like nuget.org. If an organization wishes to block such access, it must use other means such as firewalls to do so.</span></span>

### <a name="nugetdefaultsconfig-location"></a><span data-ttu-id="23784-188">NuGetDefaults.Config konumu</span><span class="sxs-lookup"><span data-stu-id="23784-188">NuGetDefaults.Config location</span></span>

<span data-ttu-id="23784-189">Aşağıdaki tablo nerede tanımlar `NuGetDefaults.Config` dosya depolanması, hedef işletim sistemi bağlı olarak:</span><span class="sxs-lookup"><span data-stu-id="23784-189">The following table describes where the `NuGetDefaults.Config` file should be stored, depending on the target OS:</span></span>

| <span data-ttu-id="23784-190">İşletim sistemi platformu</span><span class="sxs-lookup"><span data-stu-id="23784-190">OS Platform</span></span>  | <span data-ttu-id="23784-191">NuGetDefaults.Config konumu</span><span class="sxs-lookup"><span data-stu-id="23784-191">NuGetDefaults.Config Location</span></span> |
| --- | --- |
| <span data-ttu-id="23784-192">Windows</span><span class="sxs-lookup"><span data-stu-id="23784-192">Windows</span></span>      | <span data-ttu-id="23784-193">**Visual Studio 2017 veya NuGet 4.x+:** `%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="23784-193">**Visual Studio 2017 or NuGet 4.x+:** `%ProgramFiles(x86)%\NuGet\Config`</span></span> <br /><span data-ttu-id="23784-194">**Visual Studio 2015 veya önceki veya NuGet 3.x ve önceki sürümleri:** `%PROGRAMDATA%\NuGet`</span><span class="sxs-lookup"><span data-stu-id="23784-194">**Visual Studio 2015 and earlier or NuGet 3.x and earlier:** `%PROGRAMDATA%\NuGet`</span></span> |
| <span data-ttu-id="23784-195">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="23784-195">Mac/Linux</span></span>    | <span data-ttu-id="23784-196">`$XDG_DATA_HOME` (genellikle `~/.local/share` veya `/usr/local/share`işletim sistemi dağıtım bağlı olarak)</span><span class="sxs-lookup"><span data-stu-id="23784-196">`$XDG_DATA_HOME` (typically `~/.local/share` or `/usr/local/share`, depending on OS distribution)</span></span>|

### <a name="nugetdefaultsconfig-settings"></a><span data-ttu-id="23784-197">NuGetDefaults.Config ayarları</span><span class="sxs-lookup"><span data-stu-id="23784-197">NuGetDefaults.Config settings</span></span>

- <span data-ttu-id="23784-198">`packageSources`: Bu koleksiyona sahip aynı anlamı `packageSources` normal olarak yapılandırma dosyaları ve varsayılan kaynakları belirtir.</span><span class="sxs-lookup"><span data-stu-id="23784-198">`packageSources`: this collection has the same meaning as `packageSources` in regular config files and specifies the default sources.</span></span> <span data-ttu-id="23784-199">NuGet yüklerken veya güncellerken kullanarak projelerinde paketler sırayla kaynakları kullanan `packages.config` yönetim biçimi.</span><span class="sxs-lookup"><span data-stu-id="23784-199">NuGet uses the sources in order when installing or updating packages in projects using the `packages.config` management format.</span></span> <span data-ttu-id="23784-200">PackageReference biçimini kullanarak projeleri için NuGet öncelikle yerel kaynakları kullanır, sonra ağ paylaşımları ve yapılandırma dosyalarını sıraya bakılmaksızın HTTP kaynakları üzerindeki kaynakları.</span><span class="sxs-lookup"><span data-stu-id="23784-200">For projects using the PackageReference format, NuGet uses local sources first, then sources on network shares, then HTTP sources, regardless of the order in the configuration files.</span></span> <span data-ttu-id="23784-201">NuGet geri yükleme işlemleri kaynaklarıyla sırasını her zaman yok sayar.</span><span class="sxs-lookup"><span data-stu-id="23784-201">NuGet always ignores the order of sources with restore operations.</span></span>

- <span data-ttu-id="23784-202">`disabledPackageSources`: Bu koleksiyon da aynı olarak anlamı `NuGet.Config` burada her etkilenen kaynak listelendiğini adını ve gösteren bir true/false değeri tarafından devre dışı bırakılıp bırakılmayacağını dosyaları.</span><span class="sxs-lookup"><span data-stu-id="23784-202">`disabledPackageSources`: this collection also has the same meaning as in `NuGet.Config` files, where each affected source is listed by its name and a true/false value indicating whether it's disabled.</span></span> <span data-ttu-id="23784-203">Bu kaynak adı ve URL içinde kalmasını sağlar `packageSources` zorunda kalmadan, varsayılan olarak açıktır.</span><span class="sxs-lookup"><span data-stu-id="23784-203">This allows the source name and URL to remain in `packageSources` without having it turned on by default.</span></span> <span data-ttu-id="23784-204">Bireysel geliştiriciler daha sonra tekrar etkinleştirebilirsiniz kaynak kaynağın diğer yanlış ayarlayarak `NuGet.Config` doğru URL'yi yeniden bulmak zorunda kalmadan dosyaları.</span><span class="sxs-lookup"><span data-stu-id="23784-204">Individual developers can then re-enable the source by setting the source's value to false in other `NuGet.Config` files without having to find the correct URL again.</span></span> <span data-ttu-id="23784-205">Ayrıca varsayılan olarak yalnızca tek bir takımın kaynak etkinleştirme sırasında bir kuruluş için iç kaynak URL'lerin tam listesini geliştiricilere sağlamak kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="23784-205">This is also useful to supply developers with a full list of internal source URLs for an organization while enabling only an individual team's source by default.</span></span>

- <span data-ttu-id="23784-206">`defaultPushSource`: varsayılan hedefi belirleyen `nuget push` nuget.org yerleşik varsayılan geçersiz kılma işlemleri. Yöneticiler, iç paketler için genel nuget.org yanlışlıkla, yayımlama önlemek için bu ayarı dağıtabilir, geliştiriciler özel olarak kullanılacak gerektiği `nuget push -Source` nuget.org için yayımlanacak.</span><span class="sxs-lookup"><span data-stu-id="23784-206">`defaultPushSource`: specifies the default target for `nuget push` operations, overriding the built-in default of nuget.org. Administrators can deploy this setting to avoid publishing internal packages to the public nuget.org by accident, as developers specifically need to use `nuget push -Source` to publish to nuget.org.</span></span>

### <a name="example-nugetdefaultsconfig-and-application"></a><span data-ttu-id="23784-207">Örnek NuGetDefaults.Config ve uygulama</span><span class="sxs-lookup"><span data-stu-id="23784-207">Example NuGetDefaults.Config and application</span></span>

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
