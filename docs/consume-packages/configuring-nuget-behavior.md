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
# <a name="common-nuget-configurations"></a><span data-ttu-id="bb8e7-103">Ortak NuGet yapılandırmaları</span><span class="sxs-lookup"><span data-stu-id="bb8e7-103">Common NuGet configurations</span></span>

<span data-ttu-id="bb8e7-104">NuGet'in davranışı, proje, kullanıcı ve `NuGet.Config` bilgisayar genelinde ki düzeylerde bulunabilen bir veya daha fazla (XML) dosyadaki birikmiş ayarlar tarafından yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-104">NuGet's behavior is driven by the accumulated settings in one or more `NuGet.Config` (XML) files that can exist at project-, user-, and computer-wide levels.</span></span> <span data-ttu-id="bb8e7-105">Genel `NuGetDefaults.Config` bir dosya da özellikle paket kaynaklarını yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-105">A global `NuGetDefaults.Config` file also specifically configures package sources.</span></span> <span data-ttu-id="bb8e7-106">Ayarlar CLI, Package Manager Console ve Paket Yöneticisi UI'de verilen tüm komutlar için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-106">Settings apply to all commands issued in the CLI, the Package Manager Console, and the Package Manager UI.</span></span>

## <a name="config-file-locations-and-uses"></a><span data-ttu-id="bb8e7-107">Config dosya konumları ve kullanımları</span><span class="sxs-lookup"><span data-stu-id="bb8e7-107">Config file locations and uses</span></span>

| <span data-ttu-id="bb8e7-108">Kapsam</span><span class="sxs-lookup"><span data-stu-id="bb8e7-108">Scope</span></span> | <span data-ttu-id="bb8e7-109">NuGet.Config dosya konumu</span><span class="sxs-lookup"><span data-stu-id="bb8e7-109">NuGet.Config file location</span></span> | <span data-ttu-id="bb8e7-110">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bb8e7-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bb8e7-111">Çözüm</span><span class="sxs-lookup"><span data-stu-id="bb8e7-111">Solution</span></span> | <span data-ttu-id="bb8e7-112">Geçerli klasör (aka Solution klasörü) veya sürücü köküne kadar herhangi bir klasör.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-112">Current folder (aka Solution folder) or any folder up to the drive root.</span></span>| <span data-ttu-id="bb8e7-113">Çözüm klasöründe ayarlar alt klasörlerdeki tüm projeleriçin geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-113">In a solution folder, settings apply to all projects in subfolders.</span></span> <span data-ttu-id="bb8e7-114">Bir config dosyası proje klasörüne yerleştirilirse, bunun bu proje üzerinde hiçbir etkisi olmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-114">Note that if a config file is placed in a project folder, it has no effect on that project.</span></span> |
| <span data-ttu-id="bb8e7-115">Kullanıcı</span><span class="sxs-lookup"><span data-stu-id="bb8e7-115">User</span></span> | <span data-ttu-id="bb8e7-116">Windows:`%appdata%\NuGet\NuGet.Config`</span><span class="sxs-lookup"><span data-stu-id="bb8e7-116">Windows: `%appdata%\NuGet\NuGet.Config`</span></span><br/><span data-ttu-id="bb8e7-117">Mac/Linux: `~/.config/NuGet/NuGet.Config` `~/.nuget/NuGet/NuGet.Config` veya (işletim sistemi dağılımına göre değişir)</span><span class="sxs-lookup"><span data-stu-id="bb8e7-117">Mac/Linux: `~/.config/NuGet/NuGet.Config` or `~/.nuget/NuGet/NuGet.Config` (varies by OS distribution)</span></span> | <span data-ttu-id="bb8e7-118">Ayarlar tüm işlemler için geçerlidir, ancak proje düzeyi ayarları tarafından geçersiz kılınan.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-118">Settings apply to all operations, but are overridden by any project-level settings.</span></span> |
| <span data-ttu-id="bb8e7-119">Bilgisayar</span><span class="sxs-lookup"><span data-stu-id="bb8e7-119">Computer</span></span> | <span data-ttu-id="bb8e7-120">Windows:`%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="bb8e7-120">Windows: `%ProgramFiles(x86)%\NuGet\Config`</span></span><br/><span data-ttu-id="bb8e7-121">Mac/Linux: `$XDG_DATA_HOME`.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-121">Mac/Linux: `$XDG_DATA_HOME`.</span></span> <span data-ttu-id="bb8e7-122">Null `$XDG_DATA_HOME` veya boş `~/.local/share` ise `/usr/local/share` veya kullanılacaksa (işletim sistemi dağılımına göre değişir)</span><span class="sxs-lookup"><span data-stu-id="bb8e7-122">If `$XDG_DATA_HOME` is null or empty, `~/.local/share` or `/usr/local/share` will be used (varies by OS distribution)</span></span>  | <span data-ttu-id="bb8e7-123">Ayarlar bilgisayardaki tüm işlemler için geçerlidir, ancak herhangi bir kullanıcı veya proje düzeyi ayarları tarafından geçersiz kılınan.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-123">Settings apply to all operations on the computer, but are overridden by any user- or project-level settings.</span></span> |

<span data-ttu-id="bb8e7-124">NuGet'in önceki sürümleri için notlar:</span><span class="sxs-lookup"><span data-stu-id="bb8e7-124">Notes for earlier versions of NuGet:</span></span>
- <span data-ttu-id="bb8e7-125">NuGet 3.3 ve `.nuget` daha önce çözüm genelinde ayarlar için bir klasör kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-125">NuGet 3.3 and earlier used a `.nuget` folder for solution-wide settings.</span></span> <span data-ttu-id="bb8e7-126">Bu klasör NuGet 3.4+ için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-126">This folder is not used in NuGet 3.4+.</span></span>
- <span data-ttu-id="bb8e7-127">NuGet 2.6 ile 3.x için, Windows'daki bilgisayar düzeyindeki config dosyası\\%ProgramData%\NuGet\Config[ {IDE}[ {Version}]\\\\\{SKU}]]]]\NuGet.Config, *{IDE}* 14.0 gibi Visual *Studio*sürümü , *{Sürüm}* *14.0*gibi Visual Studio sürümü ve *{SKU}* topluluk , *Pro*, veya *Enterprise*. *Community*</span><span class="sxs-lookup"><span data-stu-id="bb8e7-127">For NuGet 2.6 to 3.x, the computer-level config file on Windows was located in %ProgramData%\NuGet\Config[\\{IDE}[\\{Version}[\\{SKU}]]]\NuGet.Config, where *{IDE}* can be *VisualStudio*, *{Version}* was the Visual Studio version such as *14.0*, and *{SKU}* is either *Community*, *Pro*, or *Enterprise*.</span></span> <span data-ttu-id="bb8e7-128">Ayarları NuGet 4.0+'ya geçirmek için config dosyasını %ProgramFiles(x86)%\NuGet\Config'e kopyalamanız yeterlidir. Linux'ta, bu önceki konum /etc/opt ve Mac, /Library/Application Support'tu.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-128">To migrate settings to NuGet 4.0+, simply copy the config file to %ProgramFiles(x86)%\NuGet\Config. On Linux, this previous location was /etc/opt, and on Mac, /Library/Application Support.</span></span>

## <a name="changing-config-settings"></a><span data-ttu-id="bb8e7-129">Config ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="bb8e7-129">Changing config settings</span></span>

<span data-ttu-id="bb8e7-130">`NuGet.Config` Dosya, [NuGet Yapılandırma Ayarları](../reference/nuget-config-file.md) konusunda açıklandığı gibi anahtar/değer çiftleri içeren basit bir XML metin dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-130">A `NuGet.Config` file is a simple XML text file containing key/value pairs as described in the [NuGet Configuration Settings](../reference/nuget-config-file.md) topic.</span></span>

<span data-ttu-id="bb8e7-131">Ayarlar NuGet CLI [config komutu](../reference/cli-reference/cli-ref-config.md)kullanılarak yönetilir:</span><span class="sxs-lookup"><span data-stu-id="bb8e7-131">Settings are managed using the NuGet CLI [config command](../reference/cli-reference/cli-ref-config.md):</span></span>
- <span data-ttu-id="bb8e7-132">Varsayılan olarak, kullanıcı düzeyinde config dosyasında değişiklikler yapılır.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-132">By default, changes are made to the user-level config file.</span></span>
- <span data-ttu-id="bb8e7-133">Farklı bir dosyadaki ayarları değiştirmek `-configFile` için anahtarı kullanın.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-133">To change settings in a different file, use the `-configFile` switch.</span></span> <span data-ttu-id="bb8e7-134">Bu durumda dosyalar herhangi bir dosya adı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-134">In this case files can use any filename.</span></span>
- <span data-ttu-id="bb8e7-135">Anahtarlar her zaman büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-135">Keys are always case sensitive.</span></span>
- <span data-ttu-id="bb8e7-136">Bilgisayar düzeyindeki ayarlar dosyasındaki ayarları değiştirmek için yükseklik gereklidir.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-136">Elevation is required to change settings in the computer-level settings file.</span></span>

> [!Warning]
> <span data-ttu-id="bb8e7-137">Dosyayı herhangi bir metin düzenleyicisinde değiştirebiliyor olsanız da, NuGet (v3.4.3 ve sonrası) hatalı biçimlendirilmiş XML (eşleşmemiş etiketler, geçersiz tırnak işaretleri, vb.) içeriyorsa, tüm yapılandırma dosyasını sessizce yok sayar.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-137">Although you can modify the file in any text editor, NuGet (v3.4.3 and later) silently ignores the entire configuration file if it contains malformed XML (mismatched tags, invalid quotation marks, etc.).</span></span> <span data-ttu-id="bb8e7-138">Bu nedenle ayarı kullanarak `nuget config`yönetmek tercih edilir.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-138">This is why it's preferable to manage setting using `nuget config`.</span></span>

### <a name="setting-a-value"></a><span data-ttu-id="bb8e7-139">Değer ayarlama</span><span class="sxs-lookup"><span data-stu-id="bb8e7-139">Setting a value</span></span>

<span data-ttu-id="bb8e7-140">Windows:</span><span class="sxs-lookup"><span data-stu-id="bb8e7-140">Windows:</span></span>

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\Config\NuGet.Config
```

<span data-ttu-id="bb8e7-141">Mac/Linux:</span><span class="sxs-lookup"><span data-stu-id="bb8e7-141">Mac/Linux:</span></span>

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
> <span data-ttu-id="bb8e7-142">NuGet 3.4 ve daha sonra `repositoryPath=%PACKAGEHOME%` (Windows) ve `repositoryPath=$PACKAGEHOME` (Mac/Linux) gibi herhangi bir değerde ortam değişkenlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-142">In NuGet 3.4 and later you can use environment variables in any value, as in `repositoryPath=%PACKAGEHOME%` (Windows) and `repositoryPath=$PACKAGEHOME` (Mac/Linux).</span></span>

### <a name="removing-a-value"></a><span data-ttu-id="bb8e7-143">Bir değeri kaldırma</span><span class="sxs-lookup"><span data-stu-id="bb8e7-143">Removing a value</span></span>

<span data-ttu-id="bb8e7-144">Bir değeri kaldırmak için boş değeri olan bir anahtar belirtin.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-144">To remove a value, specify a key with an empty value.</span></span>

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a><span data-ttu-id="bb8e7-145">Yeni bir config dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="bb8e7-145">Creating a new config file</span></span>

<span data-ttu-id="bb8e7-146">Aşağıdaki şablonu yeni dosyaya kopyalayın ve değerleri ayarlamak için kullanın: `nuget config -configFile <filename>`</span><span class="sxs-lookup"><span data-stu-id="bb8e7-146">Copy the template below into the new file and then use `nuget config -configFile <filename>` to set values:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a><span data-ttu-id="bb8e7-147">Ayarlar nasıl uygulanır?</span><span class="sxs-lookup"><span data-stu-id="bb8e7-147">How settings are applied</span></span>

<span data-ttu-id="bb8e7-148">Birden `NuGet.Config` çok dosya, ayarları tek bir projeye, bir proje grubuna veya tüm projelere uygulanabilmesi için farklı konumlarda depolamanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-148">Multiple `NuGet.Config` files allow you to store settings in different locations so that they apply to a single project, a group of projects, or all projects.</span></span> <span data-ttu-id="bb8e7-149">Bu ayarlar, komut satırından veya Visual Studio'dan çağrılan herhangi bir NuGet işlemi için topluca geçerlidir ve bir projeye veya geçerli klasöre "en yakın" ayarlar önceliklidir.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-149">These settings collectively apply to any NuGet operation invoked from the command line or from Visual Studio, with settings that exist "closest" to a project or the current folder taking precedence.</span></span>

<span data-ttu-id="bb8e7-150">Özellikle, NuGet aşağıdaki sırayla farklı config dosyalarından ayarları yükler:</span><span class="sxs-lookup"><span data-stu-id="bb8e7-150">Specifically, NuGet loads settings from the different config files in the following order:</span></span>

1. <span data-ttu-id="bb8e7-151">[NuGetDefaults.Config dosyası,](#nuget-defaults-file)yalnızca paket kaynaklarıyla ilgili ayarları içerir.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-151">The [NuGetDefaults.Config file](#nuget-defaults-file), which contains settings related only to package sources.</span></span>
1. <span data-ttu-id="bb8e7-152">Bilgisayar düzeyindeki dosya.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-152">The computer-level file.</span></span>
1. <span data-ttu-id="bb8e7-153">Kullanıcı düzeyindedosya.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-153">The user-level file.</span></span>
1. <span data-ttu-id="bb8e7-154">' ile `-configFile`belirtilen dosya</span><span class="sxs-lookup"><span data-stu-id="bb8e7-154">The file specified with `-configFile`.</span></span>
1. <span data-ttu-id="bb8e7-155">Sürücü kökünden geçerli klasöre giden yoldaki her klasörde bulunan dosyalar (nuget.exe'nin çağrıldığı veya Visual Studio projesini içeren klasör).</span><span class="sxs-lookup"><span data-stu-id="bb8e7-155">Files found in every folder in the path from the drive root to the current folder (where nuget.exe is invoked or the folder containing the Visual Studio project).</span></span> <span data-ttu-id="bb8e7-156">Örneğin, c:\A\B\C'de bir komut çağrılırsa, NuGet arar ve\, c'de config dosyalarını yükler: sonra c:\A, sonra c:\A\B ve son olarak c:\A\B\C.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-156">For example, if a command is invoked in c:\A\B\C, NuGet looks for and loads config files in c:\, then c:\A, then c:\A\B, and finally c:\A\B\C.</span></span>

<span data-ttu-id="bb8e7-157">NuGet bu dosyalardaki ayarları bulduğunda aşağıdaki gibi uygulanır:</span><span class="sxs-lookup"><span data-stu-id="bb8e7-157">As NuGet finds settings in these files, they are applied as follows:</span></span>

1. <span data-ttu-id="bb8e7-158">Tek öğeli öğeler için NuGet, aynı anahtar için önceden bulunan herhangi bir değeri değiştirmiş.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-158">For single-item elements, NuGet replaced any previously-found value for the same key.</span></span> <span data-ttu-id="bb8e7-159">Bu, geçerli klasöre veya projeye "en yakın" ayarların daha önce bulunan diğer ayarları geçersiz kaktığı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-159">This means that settings that are "closest" to the current folder or project override any others found earlier.</span></span> <span data-ttu-id="bb8e7-160">Örneğin, başka `defaultPushSource` bir `NuGetDefaults.Config` config dosyasında varsa, ayar geçersiz kılındı.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-160">For example, the `defaultPushSource` setting in `NuGetDefaults.Config` is overridden if it exists in any other config file.</span></span>

1. <span data-ttu-id="bb8e7-161">Koleksiyon öğeleri (örneğin), `<packageSources>`NuGet tüm yapılandırma dosyalarının değerlerini tek bir koleksiyonda birleştirir.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-161">For collection elements (such as `<packageSources>`), NuGet combines the values from all configuration files into a single collection.</span></span>

1. <span data-ttu-id="bb8e7-162">Belirli `<clear />` bir düğüm için mevcut olduğunda, NuGet bu düğüm için daha önce tanımlanmış yapılandırma değerlerini yoksa.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-162">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span>

### <a name="settings-walkthrough"></a><span data-ttu-id="bb8e7-163">Ayarları walkthrough</span><span class="sxs-lookup"><span data-stu-id="bb8e7-163">Settings walkthrough</span></span>

<span data-ttu-id="bb8e7-164">İki ayrı sürücüde aşağıdaki klasör yapısına sahip olduğunuzu varsayalım:</span><span class="sxs-lookup"><span data-stu-id="bb8e7-164">Let's say you have the following folder structure on two separate drives:</span></span>

    disk_drive_1
        User
    disk_drive_2
       Project1
         Source
       Project2
         Source
       tmp

<span data-ttu-id="bb8e7-165">Daha sonra `NuGet.Config` verilen içerik ile aşağıdaki yerlerde dört dosya var.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-165">You then have four `NuGet.Config` files in the following locations with the given content.</span></span> <span data-ttu-id="bb8e7-166">(Bilgisayar düzeyindeki dosya bu örneğe dahil edilmez, ancak kullanıcı düzeyindeki dosyaya benzer şekilde olur.)</span><span class="sxs-lookup"><span data-stu-id="bb8e7-166">(The computer-level file is not included in this example, but would behave similarly to the user-level file.)</span></span>

<span data-ttu-id="bb8e7-167">Dosya A. Kullanıcı düzeyinde`%appdata%\NuGet\NuGet.Config` dosya, `~/.config/NuGet/NuGet.Config` (Windows' da, Mac/Linux' ta):</span><span class="sxs-lookup"><span data-stu-id="bb8e7-167">File A. User-level file, (`%appdata%\NuGet\NuGet.Config` on Windows, `~/.config/NuGet/NuGet.Config` on Mac/Linux):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="bb8e7-168">Dosya B. disk_drive_2/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="bb8e7-168">File B. disk_drive_2/NuGet.Config:</span></span>

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

<span data-ttu-id="bb8e7-169">Dosya C. disk_drive_2/Proje1/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="bb8e7-169">File C. disk_drive_2/Project1/NuGet.Config:</span></span>

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

<span data-ttu-id="bb8e7-170">Dosya D. disk_drive_2/Proje2/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="bb8e7-170">File D. disk_drive_2/Project2/NuGet.Config:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

<span data-ttu-id="bb8e7-171">NuGet daha sonra çağrıldığı yere bağlı olarak ayarları aşağıdaki gibi yükler ve uygular:</span><span class="sxs-lookup"><span data-stu-id="bb8e7-171">NuGet then loads and applies settings as follows, depending on where it's invoked:</span></span>

- <span data-ttu-id="bb8e7-172">**disk_drive_1/kullanıcılardan çağrılan**: disk_drive_1 bulunan tek dosya bu olduğundan, yalnızca kullanıcı düzeyindeyapılandırma dosyasında (A) listelenen varsayılan depo kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-172">**Invoked from disk_drive_1/users**: Only the default repository listed in the user-level configuration file (A) is used, because that's the only file found on disk_drive_1.</span></span>

- <span data-ttu-id="bb8e7-173">**disk_drive_2/ veya disk_drive_/tmp'den çağrılan**: Kullanıcı düzeyindeki dosya (A) önce yüklenir, sonra NuGet disk_drive_2 köküne gider ve (B) dosyasını bulur.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-173">**Invoked from disk_drive_2/ or disk_drive_/tmp**: The user-level file (A) is loaded first, then NuGet goes to the root of disk_drive_2 and finds file (B).</span></span> <span data-ttu-id="bb8e7-174">NuGet ayrıca /tmp'de bir yapılandırma dosyası arar, ancak budosyayı bulamaz.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-174">NuGet also looks for a configuration file in /tmp but does not find one.</span></span> <span data-ttu-id="bb8e7-175">Sonuç olarak, nuget.org varsayılan depo kullanılır, paket geri yüklemesi etkinleştirilir ve paketler disk_drive_2/tmp'de genişletilir.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-175">As a result, the default repository on nuget.org is used, package restore is enabled, and packages get expanded in disk_drive_2/tmp.</span></span>

- <span data-ttu-id="bb8e7-176">**disk_drive_2/Project1 veya disk_drive_2/Project1/Source:** Kullanıcı düzeyindeki dosya (A) önce yüklenir, ardından NuGet disk_drive_2 kökünden yüklenir ve ardından dosya (C) yüklenir.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-176">**Invoked from disk_drive_2/Project1 or disk_drive_2/Project1/Source**: The user-level file (A) is loaded first, then NuGet loads file (B) from the root of disk_drive_2, followed by file (C).</span></span> <span data-ttu-id="bb8e7-177">(C) 'deki ayarlar (B) ve (A)'dakileri geçersiz kılar, böylece paketlerin `repositoryPath` yüklendiği yer *disk_drive_2/tmp*yerine disk_drive_2/Project1/External/Packages olur.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-177">Settings in (C) override those in (B) and (A), so the `repositoryPath` where packages get installed is disk_drive_2/Project1/External/Packages instead of *disk_drive_2/tmp*.</span></span> <span data-ttu-id="bb8e7-178">Ayrıca, (C) temizler `<packageSources>`çünkü, nuget.org artık kaynak `https://MyPrivateRepo/ES/nuget`olarak kullanılabilir sadece bırakarak .</span><span class="sxs-lookup"><span data-stu-id="bb8e7-178">Also, because (C) clears `<packageSources>`, nuget.org is no longer available as a source leaving only `https://MyPrivateRepo/ES/nuget`.</span></span>

- <span data-ttu-id="bb8e7-179">**disk_drive_2/Project2 veya disk_drive_2/Project2/Source :** Kullanıcı düzeyindeki dosya (A) önce (B) ve dosya (D) tarafından yüklenir.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-179">**Invoked from disk_drive_2/Project2 or disk_drive_2/Project2/Source**: The user-level file (A) is loaded first followed by file (B) and file (D).</span></span> <span data-ttu-id="bb8e7-180">Çünkü `packageSources` temizlenmedi, `nuget.org` `https://MyPrivateRepo/DQ/nuget` her ikisi de ve kaynak olarak mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-180">Because `packageSources` is not cleared, both `nuget.org` and `https://MyPrivateRepo/DQ/nuget` are available as sources.</span></span> <span data-ttu-id="bb8e7-181">Paketler (B)'de belirtildiği şekilde disk_drive_2/tmp cinsinden genişletilir.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-181">Packages get expanded in disk_drive_2/tmp as specified in (B).</span></span>

## <a name="nuget-defaults-file"></a><span data-ttu-id="bb8e7-182">NuGet varsayılan dosya</span><span class="sxs-lookup"><span data-stu-id="bb8e7-182">NuGet defaults file</span></span>

<span data-ttu-id="bb8e7-183">Dosya, `NuGetDefaults.Config` paketlerin yüklü ve güncelleştirildiği paket kaynaklarını belirtmek ve `nuget push`paketleri yayınlamak için varsayılan hedefi denetlemek için var.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-183">The `NuGetDefaults.Config` file exists to specify package sources from which packages are installed and updated, and to control the default target for publishing packages with `nuget push`.</span></span> <span data-ttu-id="bb8e7-184">Yöneticiler uygun bir şekilde (örneğin Grup İlkesi'ni kullanarak) tutarlı `NuGetDefaults.Config` dosyaları geliştiriciye dağıtabildiklerinden ve makineler oluşturabildiklerinden, kuruluştaki herkesin nuget.org yerine doğru paket kaynaklarını kullandığından emin olabilirler.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-184">Because administrators can conveniently (using Group Policy, for example) deploy consistent `NuGetDefaults.Config` files to developer and build machines, they can ensure that everyone in the organization is using the correct package sources rather than nuget.org.</span></span>

> [!Important]
> <span data-ttu-id="bb8e7-185">Dosya `NuGetDefaults.Config` hiçbir zaman bir paket kaynağının geliştiricinin NuGet yapılandırmasından kaldırılmasına neden olmaz.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-185">The `NuGetDefaults.Config` file never causes a package source to be removed from a developer's NuGet configuration.</span></span> <span data-ttu-id="bb8e7-186">Bu, geliştirici zaten NuGet kullanmış sa yılmışsa ve bu nedenle nuget.org paket `NuGetDefaults.Config` kaynağı kayıtlıysa, dosya oluşturulduktan sonra kaldırılmaz.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-186">That means if the developer has already used NuGet and therefore has the nuget.org package source registered, it won't be removed after the creation of a `NuGetDefaults.Config` file.</span></span>
>
> <span data-ttu-id="bb8e7-187">Ayrıca, NuGet'deki ne `NuGetDefaults.Config` de başka bir mekanizma nuget.org gibi paket kaynaklarına erişimi engelleyebilir. Bir kuruluş bu tür erişimi engellemek istiyorsa, bunu yapmak için güvenlik duvarları gibi başka yollar kullanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-187">Furthermore, neither `NuGetDefaults.Config` nor any other mechanism in NuGet can prevent access to package sources like nuget.org. If an organization wishes to block such access, it must use other means such as firewalls to do so.</span></span>

### <a name="nugetdefaultsconfig-location"></a><span data-ttu-id="bb8e7-188">NuGetDefaults.Config konumu</span><span class="sxs-lookup"><span data-stu-id="bb8e7-188">NuGetDefaults.Config location</span></span>

<span data-ttu-id="bb8e7-189">Aşağıdaki tabloda, `NuGetDefaults.Config` hedef işletim sistemi bağlı olarak dosyanın nerede depolanması gerektiği açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="bb8e7-189">The following table describes where the `NuGetDefaults.Config` file should be stored, depending on the target OS:</span></span>

| <span data-ttu-id="bb8e7-190">İşletim Sistemi Platformu</span><span class="sxs-lookup"><span data-stu-id="bb8e7-190">OS Platform</span></span>  | <span data-ttu-id="bb8e7-191">NuGetDefaults.Config Yeri</span><span class="sxs-lookup"><span data-stu-id="bb8e7-191">NuGetDefaults.Config Location</span></span> |
| --- | --- |
| <span data-ttu-id="bb8e7-192">Windows</span><span class="sxs-lookup"><span data-stu-id="bb8e7-192">Windows</span></span>      | <span data-ttu-id="bb8e7-193">**Visual Studio 2017 veya NuGet 4.x+:**`%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="bb8e7-193">**Visual Studio 2017 or NuGet 4.x+:** `%ProgramFiles(x86)%\NuGet\Config`</span></span> <br /><span data-ttu-id="bb8e7-194">**Visual Studio 2015 ve önceki veya NuGet 3.x ve daha önceki:**`%PROGRAMDATA%\NuGet`</span><span class="sxs-lookup"><span data-stu-id="bb8e7-194">**Visual Studio 2015 and earlier or NuGet 3.x and earlier:** `%PROGRAMDATA%\NuGet`</span></span> |
| <span data-ttu-id="bb8e7-195">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="bb8e7-195">Mac/Linux</span></span>    | <span data-ttu-id="bb8e7-196">`$XDG_DATA_HOME`(genellikle `~/.local/share` veya, `/usr/local/share`işletim sistemi dağılımına bağlı olarak)</span><span class="sxs-lookup"><span data-stu-id="bb8e7-196">`$XDG_DATA_HOME` (typically `~/.local/share` or `/usr/local/share`, depending on OS distribution)</span></span>|

### <a name="nugetdefaultsconfig-settings"></a><span data-ttu-id="bb8e7-197">NuGetDefaults.Config ayarları</span><span class="sxs-lookup"><span data-stu-id="bb8e7-197">NuGetDefaults.Config settings</span></span>

- <span data-ttu-id="bb8e7-198">`packageSources`: Bu koleksiyon normal `packageSources` config dosyalarındakiyle aynı anlama gelir ve varsayılan kaynakları belirtir.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-198">`packageSources`: this collection has the same meaning as `packageSources` in regular config files and specifies the default sources.</span></span> <span data-ttu-id="bb8e7-199">NuGet, `packages.config` yönetim biçimini kullanarak projelerdeki paketleri yüklerken veya güncellerken kaynakları sırayla kullanır.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-199">NuGet uses the sources in order when installing or updating packages in projects using the `packages.config` management format.</span></span> <span data-ttu-id="bb8e7-200">PackageReference biçimini kullanan projelerde NuGet, yapılandırma dosyalarındaki siparişe bakılmaksızın önce yerel kaynakları, ardından ağ paylaşımları kaynaklarını, ardından HTTP kaynaklarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-200">For projects using the PackageReference format, NuGet uses local sources first, then sources on network shares, then HTTP sources, regardless of the order in the configuration files.</span></span> <span data-ttu-id="bb8e7-201">NuGet her zaman geri yükleme işlemleri ile kaynakların sırasını yok sayar.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-201">NuGet always ignores the order of sources with restore operations.</span></span>

- <span data-ttu-id="bb8e7-202">`disabledPackageSources`: Bu koleksiyon, etkilenen her `NuGet.Config` kaynağın kendi adıyla listelendiği dosyalarla aynı anlama ve devre dışı kalıp olmadığını gösteren doğru/yanlış bir değere de sahiptir.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-202">`disabledPackageSources`: this collection also has the same meaning as in `NuGet.Config` files, where each affected source is listed by its name and a true/false value indicating whether it's disabled.</span></span> <span data-ttu-id="bb8e7-203">Bu, kaynak adın ve `packageSources` URL'nin varsayılan olarak açık kalmadan içinde kalmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-203">This allows the source name and URL to remain in `packageSources` without having it turned on by default.</span></span> <span data-ttu-id="bb8e7-204">Tek tek geliştiriciler daha sonra kaynağın değerini doğru URL'yi `NuGet.Config` yeniden bulmak zorunda kalmadan diğer dosyalarda false olarak ayarlayarak kaynağı yeniden etkinleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-204">Individual developers can then re-enable the source by setting the source's value to false in other `NuGet.Config` files without having to find the correct URL again.</span></span> <span data-ttu-id="bb8e7-205">Bu, geliştiricilere varsayılan olarak yalnızca tek bir takımın kaynağını etkinleştirirken bir kuruluş için dahili kaynak URL'lerinin tam listesini sağlamak için de yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-205">This is also useful to supply developers with a full list of internal source URLs for an organization while enabling only an individual team's source by default.</span></span>

- <span data-ttu-id="bb8e7-206">`defaultPushSource`: işlemler için `nuget push` varsayılan hedefi belirtir ve yerleşik varsayılan nuget.org geçersiz kılın. Geliştiricilerin özellikle nuget.org yayınlamak için kullanmaları `nuget push -Source` gerektiğinden, yöneticiler bu ayarı, dahili paketleri yanlışlıkla genel nuget.org yayımlamamak için dağıtabilir.</span><span class="sxs-lookup"><span data-stu-id="bb8e7-206">`defaultPushSource`: specifies the default target for `nuget push` operations, overriding the built-in default of nuget.org. Administrators can deploy this setting to avoid publishing internal packages to the public nuget.org by accident, as developers specifically need to use `nuget push -Source` to publish to nuget.org.</span></span>

### <a name="example-nugetdefaultsconfig-and-application"></a><span data-ttu-id="bb8e7-207">Örnek NuGetDefaults.Config ve uygulama</span><span class="sxs-lookup"><span data-stu-id="bb8e7-207">Example NuGetDefaults.Config and application</span></span>

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
