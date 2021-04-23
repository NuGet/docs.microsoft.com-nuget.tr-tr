---
title: Ortak NuGet yapılandırmaları
description: NuGet.Config dosyalar, NuGet 'in hem genel hem de proje başına temelinde denetimini denetler ve NuGet yapılandırma komutuyla değiştirilir.
author: JonDouglas
ms.author: jodou
ms.date: 10/25/2017
ms.topic: conceptual
ms.openlocfilehash: 18e3af7145495b5753b5900915ffb4b07942b856
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901489"
---
# <a name="common-nuget-configurations"></a><span data-ttu-id="8ef34-103">Ortak NuGet yapılandırmaları</span><span class="sxs-lookup"><span data-stu-id="8ef34-103">Common NuGet configurations</span></span>

<span data-ttu-id="8ef34-104">NuGet davranışı `NuGet.Config` , proje, Kullanıcı ve bilgisayar genelindeki düzeylerde bulunabilir bir veya daha fazla (XML) dosyada birikmiş ayarlar tarafından yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="8ef34-104">NuGet's behavior is driven by the accumulated settings in one or more `NuGet.Config` (XML) files that can exist at project-, user-, and computer-wide levels.</span></span> <span data-ttu-id="8ef34-105">Genel bir `NuGetDefaults.Config` Dosya Ayrıca paket kaynaklarını özellikle yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="8ef34-105">A global `NuGetDefaults.Config` file also specifically configures package sources.</span></span> <span data-ttu-id="8ef34-106">Ayarlar, CLı, Paket Yöneticisi konsolu ve Paket Yöneticisi Kullanıcı arabiriminde verilen tüm komutlara uygulanır.</span><span class="sxs-lookup"><span data-stu-id="8ef34-106">Settings apply to all commands issued in the CLI, the Package Manager Console, and the Package Manager UI.</span></span>

## <a name="config-file-locations-and-uses"></a><span data-ttu-id="8ef34-107">Yapılandırma dosyası konumları ve kullanımları</span><span class="sxs-lookup"><span data-stu-id="8ef34-107">Config file locations and uses</span></span>

| <span data-ttu-id="8ef34-108">Kapsam</span><span class="sxs-lookup"><span data-stu-id="8ef34-108">Scope</span></span> | <span data-ttu-id="8ef34-109">`NuGet.Config` dosya konumu</span><span class="sxs-lookup"><span data-stu-id="8ef34-109">`NuGet.Config` file location</span></span> | <span data-ttu-id="8ef34-110">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ef34-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8ef34-111">Çözüm</span><span class="sxs-lookup"><span data-stu-id="8ef34-111">Solution</span></span> | <span data-ttu-id="8ef34-112">Geçerli klasör (diğer adıyla, çözüm klasörü) veya sürücü köküne kadar herhangi bir klasör.</span><span class="sxs-lookup"><span data-stu-id="8ef34-112">Current folder (aka Solution folder) or any folder up to the drive root.</span></span>| <span data-ttu-id="8ef34-113">Bir çözüm klasöründe, ayarlar alt klasörlerdeki tüm projelere uygulanır.</span><span class="sxs-lookup"><span data-stu-id="8ef34-113">In a solution folder, settings apply to all projects in subfolders.</span></span> <span data-ttu-id="8ef34-114">Bir yapılandırma dosyası bir proje klasörüne yerleştirilmişse, projenin bu proje üzerinde hiçbir etkisi olmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8ef34-114">Note that if a config file is placed in a project folder, it has no effect on that project.</span></span> |
| <span data-ttu-id="8ef34-115">Kullanıcı</span><span class="sxs-lookup"><span data-stu-id="8ef34-115">User</span></span> | <span data-ttu-id="8ef34-116">**Windows:**`%appdata%\NuGet\NuGet.Config`</span><span class="sxs-lookup"><span data-stu-id="8ef34-116">**Windows:** `%appdata%\NuGet\NuGet.Config`</span></span><br/><span data-ttu-id="8ef34-117">**Mac/Linux:** `~/.config/NuGet/NuGet.Config` veya `~/.nuget/NuGet/NuGet.Config` (işletim sistemi dağıtımına göre farklılık gösterir)</span><span class="sxs-lookup"><span data-stu-id="8ef34-117">**Mac/Linux:** `~/.config/NuGet/NuGet.Config` or `~/.nuget/NuGet/NuGet.Config` (varies by OS distribution)</span></span> <br/><span data-ttu-id="8ef34-118">Ek yapılandırmaları tüm platformlarda desteklenir.</span><span class="sxs-lookup"><span data-stu-id="8ef34-118">Additional configs are supported on all platforms.</span></span> <span data-ttu-id="8ef34-119">Bu config 'ler araç tarafından düzenlenemez.</span><span class="sxs-lookup"><span data-stu-id="8ef34-119">These configs cannot be edited by the tooling.</span></span> </br> <span data-ttu-id="8ef34-120">**Windows:**`%appdata%\NuGet\config\*.Config`</span><span class="sxs-lookup"><span data-stu-id="8ef34-120">**Windows:** `%appdata%\NuGet\config\*.Config`</span></span> <br/><span data-ttu-id="8ef34-121">**Mac/Linux:** `~/.config/NuGet/config/*.config` veya `~/.nuget/config/*.config`</span><span class="sxs-lookup"><span data-stu-id="8ef34-121">**Mac/Linux:** `~/.config/NuGet/config/*.config` or `~/.nuget/config/*.config`</span></span> | <span data-ttu-id="8ef34-122">Ayarlar tüm işlemlere uygulanır, ancak proje düzeyindeki tüm ayarlar tarafından geçersiz kılınır.</span><span class="sxs-lookup"><span data-stu-id="8ef34-122">Settings apply to all operations, but are overridden by any project-level settings.</span></span> |
| <span data-ttu-id="8ef34-123">Bilgisayar</span><span class="sxs-lookup"><span data-stu-id="8ef34-123">Computer</span></span> | <span data-ttu-id="8ef34-124">**Windows:**`%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="8ef34-124">**Windows:** `%ProgramFiles(x86)%\NuGet\Config`</span></span><br/><span data-ttu-id="8ef34-125">**Mac/Linux:** `$XDG_DATA_HOME` .</span><span class="sxs-lookup"><span data-stu-id="8ef34-125">**Mac/Linux:** `$XDG_DATA_HOME`.</span></span> <span data-ttu-id="8ef34-126">`$XDG_DATA_HOME`Null veya boş ise ya da `~/.local/share` `/usr/local/share` kullanılacaksa (OS dağıtımına göre değişir)</span><span class="sxs-lookup"><span data-stu-id="8ef34-126">If `$XDG_DATA_HOME` is null or empty, `~/.local/share` or `/usr/local/share` will be used (varies by OS distribution)</span></span>  | <span data-ttu-id="8ef34-127">Ayarlar bilgisayardaki tüm işlemlere uygulanır, ancak herhangi bir kullanıcı veya proje düzeyi ayar tarafından geçersiz kılınır.</span><span class="sxs-lookup"><span data-stu-id="8ef34-127">Settings apply to all operations on the computer, but are overridden by any user- or project-level settings.</span></span> |

<span data-ttu-id="8ef34-128">NuGet 'in önceki sürümleri için notlar:</span><span class="sxs-lookup"><span data-stu-id="8ef34-128">Notes for earlier versions of NuGet:</span></span>
- <span data-ttu-id="8ef34-129">NuGet 3,3 ve önceki sürümleri `.nuget` çözüm genelinde ayarlar için bir klasör kullandı.</span><span class="sxs-lookup"><span data-stu-id="8ef34-129">NuGet 3.3 and earlier used a `.nuget` folder for solution-wide settings.</span></span> <span data-ttu-id="8ef34-130">Bu klasör NuGet 3.4 + ' de kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="8ef34-130">This folder is not used in NuGet 3.4+.</span></span>
- <span data-ttu-id="8ef34-131">NuGet 2,6 için 3. x, Windows üzerindeki bilgisayar düzeyi yapılandırma dosyası ' de yer alır; `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]\NuGet.Config` burada,, gibi `{IDE}` `VisualStudio` `{Version}` Visual Studio sürümünüz `14.0` ve, veya, `{SKU}` `Community` `Pro` ya `Enterprise` da olabilir.</span><span class="sxs-lookup"><span data-stu-id="8ef34-131">For NuGet 2.6 to 3.x, the computer-level config file on Windows was located in `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]\NuGet.Config`, where `{IDE}` can be `VisualStudio`, `{Version}` was the Visual Studio version such as `14.0`, and `{SKU}` is either `Community`, `Pro`, or `Enterprise`.</span></span> <span data-ttu-id="8ef34-132">Ayarları NuGet 4.0 + ' ya geçirmek için yapılandırma dosyasını ' a kopyalamanız yeterlidir `%ProgramFiles(x86)%\NuGet\Config` .</span><span class="sxs-lookup"><span data-stu-id="8ef34-132">To migrate settings to NuGet 4.0+, simply copy the config file to `%ProgramFiles(x86)%\NuGet\Config`.</span></span> <span data-ttu-id="8ef34-133">Linux 'ta, bu önceki konum `/etc/opt` ve Mac üzerinde `/Library/Application Support` .</span><span class="sxs-lookup"><span data-stu-id="8ef34-133">On Linux, this previous location was `/etc/opt`, and on Mac, `/Library/Application Support`.</span></span>

## <a name="changing-config-settings"></a><span data-ttu-id="8ef34-134">Yapılandırma ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="8ef34-134">Changing config settings</span></span>

<span data-ttu-id="8ef34-135">`NuGet.Config`Dosya, [NuGet yapılandırma ayarları](../reference/nuget-config-file.md) konusunda açıklandığı gibi anahtar/değer çiftlerini IÇEREN basit bir XML metin dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="8ef34-135">A `NuGet.Config` file is a simple XML text file containing key/value pairs as described in the [NuGet Configuration Settings](../reference/nuget-config-file.md) topic.</span></span>

<span data-ttu-id="8ef34-136">Ayarlar, NuGet CLı [yapılandırma komutu](../reference/cli-reference/cli-ref-config.md)kullanılarak yönetilir:</span><span class="sxs-lookup"><span data-stu-id="8ef34-136">Settings are managed using the NuGet CLI [config command](../reference/cli-reference/cli-ref-config.md):</span></span>
- <span data-ttu-id="8ef34-137">Varsayılan olarak, değişiklikler Kullanıcı düzeyi yapılandırma dosyasında yapılır.</span><span class="sxs-lookup"><span data-stu-id="8ef34-137">By default, changes are made to the user-level config file.</span></span>
- <span data-ttu-id="8ef34-138">Farklı bir dosyadaki ayarları değiştirmek için `-configFile` anahtarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="8ef34-138">To change settings in a different file, use the `-configFile` switch.</span></span> <span data-ttu-id="8ef34-139">Bu durumda, dosyalar herhangi bir dosya adını kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="8ef34-139">In this case files can use any filename.</span></span>
- <span data-ttu-id="8ef34-140">Anahtarlar her zaman büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="8ef34-140">Keys are always case sensitive.</span></span>
- <span data-ttu-id="8ef34-141">Bilgisayar düzeyi ayarları dosyasındaki ayarları değiştirmek için yükseltme gereklidir.</span><span class="sxs-lookup"><span data-stu-id="8ef34-141">Elevation is required to change settings in the computer-level settings file.</span></span>

> [!Warning]
> <span data-ttu-id="8ef34-142">Dosyayı herhangi bir metin düzenleyicisinde değiştirebilseniz de, NuGet (v 3.4.3 ve üzeri), hatalı biçimlendirilmiş XML (eşleşmeyen Etiketler, geçersiz tırnak işaretleri vb.) içeriyorsa tüm yapılandırma dosyalarını sessizce yoksayar.</span><span class="sxs-lookup"><span data-stu-id="8ef34-142">Although you can modify the file in any text editor, NuGet (v3.4.3 and later) silently ignores the entire configuration file if it contains malformed XML (mismatched tags, invalid quotation marks, etc.).</span></span> <span data-ttu-id="8ef34-143">Bu, ayarının kullanılarak yönetilmesi tercih edilir `nuget config` .</span><span class="sxs-lookup"><span data-stu-id="8ef34-143">This is why it's preferable to manage setting using `nuget config`.</span></span>

### <a name="setting-a-value"></a><span data-ttu-id="8ef34-144">Değer ayarlama</span><span class="sxs-lookup"><span data-stu-id="8ef34-144">Setting a value</span></span>

<span data-ttu-id="8ef34-145">Windows:</span><span class="sxs-lookup"><span data-stu-id="8ef34-145">Windows:</span></span>

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\Config\NuGet.Config
```

<span data-ttu-id="8ef34-146">Mac/Linux:</span><span class="sxs-lookup"><span data-stu-id="8ef34-146">Mac/Linux:</span></span>

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
> <span data-ttu-id="8ef34-147">NuGet 3,4 ve üzeri sürümlerde, `repositoryPath=%PACKAGEHOME%` (Windows) ve `repositoryPath=$PACKAGEHOME` (Mac/Linux) içinde olduğu gibi, ortam değişkenlerini herhangi bir değer içinde kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ef34-147">In NuGet 3.4 and later you can use environment variables in any value, as in `repositoryPath=%PACKAGEHOME%` (Windows) and `repositoryPath=$PACKAGEHOME` (Mac/Linux).</span></span>

### <a name="removing-a-value"></a><span data-ttu-id="8ef34-148">Değer kaldırma</span><span class="sxs-lookup"><span data-stu-id="8ef34-148">Removing a value</span></span>

<span data-ttu-id="8ef34-149">Bir değeri kaldırmak için, boş bir değere sahip bir anahtar belirtin.</span><span class="sxs-lookup"><span data-stu-id="8ef34-149">To remove a value, specify a key with an empty value.</span></span>

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a><span data-ttu-id="8ef34-150">Yeni bir yapılandırma dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="8ef34-150">Creating a new config file</span></span>

<span data-ttu-id="8ef34-151">Aşağıdaki şablonu yeni dosyaya kopyalayın ve ardından `nuget config -configFile <filename>` değerleri ayarlamak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="8ef34-151">Copy the template below into the new file and then use `nuget config -configFile <filename>` to set values:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a><span data-ttu-id="8ef34-152">Ayarlar nasıl uygulanır</span><span class="sxs-lookup"><span data-stu-id="8ef34-152">How settings are applied</span></span>

<span data-ttu-id="8ef34-153">Birden çok `NuGet.Config` Dosya, tek bir projeye, bir proje grubuna veya tüm projelere uygulanabilmeleri için ayarları farklı konumlarda depolamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="8ef34-153">Multiple `NuGet.Config` files allow you to store settings in different locations so that they apply to a single project, a group of projects, or all projects.</span></span> <span data-ttu-id="8ef34-154">Bu ayarlar, bir projeye veya geçerli klasöre "en yakın" olan ayarlar ile, komut satırından veya Visual Studio 'dan çağrılan herhangi bir NuGet işleminde toplu olarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="8ef34-154">These settings collectively apply to any NuGet operation invoked from the command line or from Visual Studio, with settings that exist "closest" to a project or the current folder taking precedence.</span></span>

<span data-ttu-id="8ef34-155">Özellikle, NuGet ayarları farklı yapılandırma dosyalarından aşağıdaki sırada yükler:</span><span class="sxs-lookup"><span data-stu-id="8ef34-155">Specifically, NuGet loads settings from the different config files in the following order:</span></span>

1. <span data-ttu-id="8ef34-156">Yalnızca paket kaynaklarıyla ilgili ayarları içeren [ `NuGetDefaults.Config` Dosya](#nuget-defaults-file).</span><span class="sxs-lookup"><span data-stu-id="8ef34-156">The [`NuGetDefaults.Config` file](#nuget-defaults-file), which contains settings related only to package sources.</span></span>
1. <span data-ttu-id="8ef34-157">Bilgisayar düzeyindeki dosya.</span><span class="sxs-lookup"><span data-stu-id="8ef34-157">The computer-level file.</span></span>
1. <span data-ttu-id="8ef34-158">Kullanıcı düzeyi dosyası.</span><span class="sxs-lookup"><span data-stu-id="8ef34-158">The user-level file.</span></span>
1. <span data-ttu-id="8ef34-159">İle belirtilen dosya `-configFile` .</span><span class="sxs-lookup"><span data-stu-id="8ef34-159">The file specified with `-configFile`.</span></span>
1. <span data-ttu-id="8ef34-160">Sürücü kökünden geçerli klasöre ( `nuget.exe` çağrıldığında veya Visual Studio projesini içeren klasör) yoldaki her klasörde bulunan dosyalar.</span><span class="sxs-lookup"><span data-stu-id="8ef34-160">Files found in every folder in the path from the drive root to the current folder (where `nuget.exe` is invoked or the folder containing the Visual Studio project).</span></span> <span data-ttu-id="8ef34-161">Örneğin, bir komut ' de çağrılırsa, `c:\A\B\C` NuGet ' de yapılandırma dosyalarını arar ve yükler, sonra, `c:\` `c:\A` `c:\A\B` ve son olarak `c:\A\B\C` .</span><span class="sxs-lookup"><span data-stu-id="8ef34-161">For example, if a command is invoked in `c:\A\B\C`, NuGet looks for and loads config files in `c:\`, then `c:\A`, then `c:\A\B`, and finally `c:\A\B\C`.</span></span>

<span data-ttu-id="8ef34-162">NuGet bu dosyalardaki ayarları bulduğundan, bunlar aşağıdaki gibi uygulanır:</span><span class="sxs-lookup"><span data-stu-id="8ef34-162">As NuGet finds settings in these files, they are applied as follows:</span></span>

1. <span data-ttu-id="8ef34-163">Tek öğe öğelerinde, NuGet aynı anahtar için önceden bulunan tüm değeri değiştirdi.</span><span class="sxs-lookup"><span data-stu-id="8ef34-163">For single-item elements, NuGet replaced any previously-found value for the same key.</span></span> <span data-ttu-id="8ef34-164">Bu, geçerli klasöre veya projeye "en yakın" olan ayarların daha önce bulduğu diğer tüm diğerlerini geçersiz kıldığı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="8ef34-164">This means that settings that are "closest" to the current folder or project override any others found earlier.</span></span> <span data-ttu-id="8ef34-165">Örneğin, `defaultPushSource` içindeki ayarı `NuGetDefaults.Config` başka herhangi bir yapılandırma dosyasında varsa geçersiz kılınır.</span><span class="sxs-lookup"><span data-stu-id="8ef34-165">For example, the `defaultPushSource` setting in `NuGetDefaults.Config` is overridden if it exists in any other config file.</span></span>
1. <span data-ttu-id="8ef34-166">Koleksiyon öğeleri (gibi) için `<packageSources>` , NuGet tüm yapılandırma dosyalarındaki değerleri tek bir koleksiyon olarak birleştirir.</span><span class="sxs-lookup"><span data-stu-id="8ef34-166">For collection elements (such as `<packageSources>`), NuGet combines the values from all configuration files into a single collection.</span></span>
1. <span data-ttu-id="8ef34-167">`<clear />`Belirli bir düğüm için olduğunda, NuGet bu düğüm için önceden tanımlanmış yapılandırma değerlerini yoksayar.</span><span class="sxs-lookup"><span data-stu-id="8ef34-167">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span>

### <a name="settings-walkthrough"></a><span data-ttu-id="8ef34-168">Ayarlar izlenecek yol</span><span class="sxs-lookup"><span data-stu-id="8ef34-168">Settings walkthrough</span></span>

<span data-ttu-id="8ef34-169">İki ayrı sürücüde aşağıdaki klasör yapısına sahip olduğunu varsayalım:</span><span class="sxs-lookup"><span data-stu-id="8ef34-169">Let's say you have the following folder structure on two separate drives:</span></span>

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

<span data-ttu-id="8ef34-170">Ardından, `NuGet.Config` belirtilen içeriğe sahip aşağıdaki konumlarda dört dosya vardır.</span><span class="sxs-lookup"><span data-stu-id="8ef34-170">You then have four `NuGet.Config` files in the following locations with the given content.</span></span> <span data-ttu-id="8ef34-171">(Bilgisayar düzeyindeki dosya bu örneğe dahil değildir, ancak kullanıcı düzeyindeki dosyada benzer şekilde davranır.)</span><span class="sxs-lookup"><span data-stu-id="8ef34-171">(The computer-level file is not included in this example, but would behave similarly to the user-level file.)</span></span>

<span data-ttu-id="8ef34-172">Dosya A. Kullanıcı düzeyi dosyası, ( `%appdata%\NuGet\NuGet.Config` Windows 'ta, `~/.config/NuGet/NuGet.Config` Mac 'Te/Linux 'ta):</span><span class="sxs-lookup"><span data-stu-id="8ef34-172">File A. User-level file, (`%appdata%\NuGet\NuGet.Config` on Windows, `~/.config/NuGet/NuGet.Config` on Mac/Linux):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="8ef34-173">B dosyası. `disk_drive_2/NuGet.Config` :</span><span class="sxs-lookup"><span data-stu-id="8ef34-173">File B. `disk_drive_2/NuGet.Config`:</span></span>

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

<span data-ttu-id="8ef34-174">Dosya C. `disk_drive_2/Project1/NuGet.Config` :</span><span class="sxs-lookup"><span data-stu-id="8ef34-174">File C. `disk_drive_2/Project1/NuGet.Config`:</span></span>

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

<span data-ttu-id="8ef34-175">Dosya D. `disk_drive_2/Project2/NuGet.Config` :</span><span class="sxs-lookup"><span data-stu-id="8ef34-175">File D. `disk_drive_2/Project2/NuGet.Config`:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

<span data-ttu-id="8ef34-176">Ardından NuGet, çağrıldığı yere bağlı olarak ayarları yükler ve aşağıdaki gibi uygular:</span><span class="sxs-lookup"><span data-stu-id="8ef34-176">NuGet then loads and applies settings as follows, depending on where it's invoked:</span></span>

- <span data-ttu-id="8ef34-177">Çağrılan: yalnızca, üzerinde bulunan tek dosya olduğundan, Kullanıcı düzeyi yapılandırma dosyasında (A) listelenen varsayılan depo kullanılır. **`disk_drive_1/users`** `disk_drive_1`</span><span class="sxs-lookup"><span data-stu-id="8ef34-177">**Invoked from `disk_drive_1/users`**: Only the default repository listed in the user-level configuration file (A) is used, because that's the only file found on `disk_drive_1`.</span></span>

- <span data-ttu-id="8ef34-178">**`disk_drive_2/` Ya da `disk_drive_/tmp` çağrılır**: önce Kullanıcı düzeyi dosya (A) yüklenir, ardından NuGet kök öğesine gider `disk_drive_2` ve dosyayı bulur (B).</span><span class="sxs-lookup"><span data-stu-id="8ef34-178">**Invoked from `disk_drive_2/` or `disk_drive_/tmp`**: The user-level file (A) is loaded first, then NuGet goes to the root of `disk_drive_2` and finds file (B).</span></span> <span data-ttu-id="8ef34-179">NuGet Ayrıca ' de bir yapılandırma dosyası arar `/tmp` ancak bir yapılandırma dosyası bulamaz.</span><span class="sxs-lookup"><span data-stu-id="8ef34-179">NuGet also looks for a configuration file in `/tmp` but does not find one.</span></span> <span data-ttu-id="8ef34-180">Sonuç olarak, üzerindeki varsayılan depo `nuget.org` kullanılır, paket geri yükleme etkinleştirilir ve paketler ' de genişletilir `disk_drive_2/tmp` .</span><span class="sxs-lookup"><span data-stu-id="8ef34-180">As a result, the default repository on `nuget.org` is used, package restore is enabled, and packages get expanded in `disk_drive_2/tmp`.</span></span>

- <span data-ttu-id="8ef34-181">**`disk_drive_2/Project1` Ya da `disk_drive_2/Project1/Source` çağrılır**: önce Kullanıcı düzeyi dosya (A) yüklenir, ardından NuGet dosyayı (B) kökünden sonra `disk_drive_2` dosya (C) ile yükler.</span><span class="sxs-lookup"><span data-stu-id="8ef34-181">**Invoked from `disk_drive_2/Project1` or `disk_drive_2/Project1/Source`**: The user-level file (A) is loaded first, then NuGet loads file (B) from the root of `disk_drive_2`, followed by file (C).</span></span> <span data-ttu-id="8ef34-182">(C) içindeki ayarlar, (B) ve (A) içindeki ayarları geçersiz kılar, bu nedenle `repositoryPath` paketlerin yüklendiği yer `disk_drive_2/Project1/External/Packages` `disk_drive_2/tmp` .</span><span class="sxs-lookup"><span data-stu-id="8ef34-182">Settings in (C) override those in (B) and (A), so the `repositoryPath` where packages get installed is `disk_drive_2/Project1/External/Packages` instead of `disk_drive_2/tmp`.</span></span> <span data-ttu-id="8ef34-183">Ayrıca, (C) temizleyen `<packageSources>` , NuGet.org artık yalnızca bir kaynak olarak kullanılamaz `https://MyPrivateRepo/ES/nuget` .</span><span class="sxs-lookup"><span data-stu-id="8ef34-183">Also, because (C) clears `<packageSources>`, nuget.org is no longer available as a source leaving only `https://MyPrivateRepo/ES/nuget`.</span></span>

- <span data-ttu-id="8ef34-184">**`disk_drive_2/Project2` Ya `disk_drive_2/Project2/Source` da çağrılır**: Kullanıcı düzeyi dosya (A) önce yüklenir ve ardından dosya (b) ve dosya (D) gelir.</span><span class="sxs-lookup"><span data-stu-id="8ef34-184">**Invoked from `disk_drive_2/Project2` or `disk_drive_2/Project2/Source`**: The user-level file (A) is loaded first followed by file (B) and file (D).</span></span> <span data-ttu-id="8ef34-185">`packageSources`Temizlenmediği için her ikisi de `nuget.org` `https://MyPrivateRepo/DQ/nuget` kaynak olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8ef34-185">Because `packageSources` is not cleared, both `nuget.org` and `https://MyPrivateRepo/DQ/nuget` are available as sources.</span></span> <span data-ttu-id="8ef34-186">Paketler ' `disk_drive_2/tmp` de belirtilen şekilde genişletilir (B).</span><span class="sxs-lookup"><span data-stu-id="8ef34-186">Packages get expanded in `disk_drive_2/tmp` as specified in (B).</span></span>

## <a name="additional-user-wide-configuration"></a><span data-ttu-id="8ef34-187">Ek Kullanıcı genelindeki yapılandırma</span><span class="sxs-lookup"><span data-stu-id="8ef34-187">Additional user wide configuration</span></span>

<span data-ttu-id="8ef34-188">NuGet, 5,7 ile başlayarak ek Kullanıcı genelindeki yapılandırma dosyaları için destek ekledi.</span><span class="sxs-lookup"><span data-stu-id="8ef34-188">Starting with 5.7, NuGet has added support for additional user wide configuration files.</span></span> <span data-ttu-id="8ef34-189">Bu, üçüncü taraf satıcıların yükseltme olmadan ek Kullanıcı yapılandırma dosyaları eklemesine olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="8ef34-189">This allows third-party vendors to add additional user configuration files without elevation.</span></span>
<span data-ttu-id="8ef34-190">Bu yapılandırma dosyaları, bir alt klasör içindeki standart Kullanıcı genelindeki yapılandırma klasöründe bulunur `config` .</span><span class="sxs-lookup"><span data-stu-id="8ef34-190">These configuration files are found in the standard user wide configuration folder within a `config` subfolder.</span></span>
<span data-ttu-id="8ef34-191">Veya ile biten tüm `.config` dosyalar `.Config` göz önünde bulundurulacaktır.</span><span class="sxs-lookup"><span data-stu-id="8ef34-191">All files ending with `.config` or `.Config` will be considered.</span></span>
<span data-ttu-id="8ef34-192">Bu dosyalar Standart araç tarafından düzenlenemez.</span><span class="sxs-lookup"><span data-stu-id="8ef34-192">These files cannot be edited by the standard tooling.</span></span>

| <span data-ttu-id="8ef34-193">İşletim sistemi platformu</span><span class="sxs-lookup"><span data-stu-id="8ef34-193">OS Platform</span></span>  | <span data-ttu-id="8ef34-194">Ek yapılandırma</span><span class="sxs-lookup"><span data-stu-id="8ef34-194">Additional Configurations</span></span> |
| --- | --- |
| <span data-ttu-id="8ef34-195">Windows</span><span class="sxs-lookup"><span data-stu-id="8ef34-195">Windows</span></span>      | `%appdata%\NuGet\config\*.Config` |
| <span data-ttu-id="8ef34-196">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="8ef34-196">Mac/Linux</span></span>    | <span data-ttu-id="8ef34-197">`~/.config/NuGet/config/*.config` veya `~/.nuget/config/*.config`</span><span class="sxs-lookup"><span data-stu-id="8ef34-197">`~/.config/NuGet/config/*.config` or `~/.nuget/config/*.config`</span></span> |

## <a name="nuget-defaults-file"></a><span data-ttu-id="8ef34-198">NuGet Varsayılanları dosyası</span><span class="sxs-lookup"><span data-stu-id="8ef34-198">NuGet defaults file</span></span>

<span data-ttu-id="8ef34-199">`NuGetDefaults.Config`Dosya, paketlerin yüklendiği ve güncelleştirildiği paket kaynaklarını belirtmek ve paketleri ile yayımlamak için varsayılan hedefi denetlemek için vardır `nuget push` .</span><span class="sxs-lookup"><span data-stu-id="8ef34-199">The `NuGetDefaults.Config` file exists to specify package sources from which packages are installed and updated, and to control the default target for publishing packages with `nuget push`.</span></span> <span data-ttu-id="8ef34-200">Yöneticiler uygun bir şekilde (örneğin grup ilkesi kullanarak) `NuGetDefaults.Config` Geliştirici ve derleme makineleri için tutarlı dosyalar dağıtıp, kuruluştaki herkesin NuGet.org yerine doğru paket kaynaklarını kullandığından emin olabilirler.</span><span class="sxs-lookup"><span data-stu-id="8ef34-200">Because administrators can conveniently (using Group Policy, for example) deploy consistent `NuGetDefaults.Config` files to developer and build machines, they can ensure that everyone in the organization is using the correct package sources rather than nuget.org.</span></span>

> [!Important]
> <span data-ttu-id="8ef34-201">`NuGetDefaults.Config`Dosya hiçbir şekilde bir geliştiricinin NuGet yapılandırmasından bir paket kaynağının kaldırılmasına neden olmaz.</span><span class="sxs-lookup"><span data-stu-id="8ef34-201">The `NuGetDefaults.Config` file never causes a package source to be removed from a developer's NuGet configuration.</span></span> <span data-ttu-id="8ef34-202">Yani, geliştirici zaten NuGet kullanıyorsa ve bu nedenle nuget.org paket kaynağı kayıtlıysa, bir dosya oluşturulduktan sonra kaldırılmaz `NuGetDefaults.Config` .</span><span class="sxs-lookup"><span data-stu-id="8ef34-202">That means if the developer has already used NuGet and therefore has the nuget.org package source registered, it won't be removed after the creation of a `NuGetDefaults.Config` file.</span></span>
>
> <span data-ttu-id="8ef34-203">Ayrıca, `NuGetDefaults.Config` NuGet 'deki başka hiçbir mekanizma, NuGet.org gibi paket kaynaklarına erişimi engelleyebilir. Bir kuruluş söz konusu erişimi engellemeyi istiyorsa, bunun için güvenlik duvarları gibi diğer yollarla kullanılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8ef34-203">Furthermore, neither `NuGetDefaults.Config` nor any other mechanism in NuGet can prevent access to package sources like nuget.org. If an organization wishes to block such access, it must use other means such as firewalls to do so.</span></span>

### <a name="nugetdefaultsconfig-location"></a><span data-ttu-id="8ef34-204">`NuGetDefaults.Config` konumuna</span><span class="sxs-lookup"><span data-stu-id="8ef34-204">`NuGetDefaults.Config` location</span></span>

<span data-ttu-id="8ef34-205">Aşağıdaki tabloda `NuGetDefaults.Config` , hedef işletim sistemine bağlı olarak dosyanın depolanacağı konum açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="8ef34-205">The following table describes where the `NuGetDefaults.Config` file should be stored, depending on the target OS:</span></span>

| <span data-ttu-id="8ef34-206">İşletim sistemi platformu</span><span class="sxs-lookup"><span data-stu-id="8ef34-206">OS Platform</span></span>  | <span data-ttu-id="8ef34-207">`NuGetDefaults.Config` Konumuna</span><span class="sxs-lookup"><span data-stu-id="8ef34-207">`NuGetDefaults.Config` Location</span></span> |
| --- | --- |
| <span data-ttu-id="8ef34-208">Windows</span><span class="sxs-lookup"><span data-stu-id="8ef34-208">Windows</span></span>      | <span data-ttu-id="8ef34-209">**Visual Studio 2017 veya NuGet 4. x +:**`%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="8ef34-209">**Visual Studio 2017 or NuGet 4.x+:** `%ProgramFiles(x86)%\NuGet\Config`</span></span> <br /><span data-ttu-id="8ef34-210">**Visual Studio 2015 ve öncesi ya da NuGet 3. x ve öncesi:**`%PROGRAMDATA%\NuGet`</span><span class="sxs-lookup"><span data-stu-id="8ef34-210">**Visual Studio 2015 and earlier or NuGet 3.x and earlier:** `%PROGRAMDATA%\NuGet`</span></span> |
| <span data-ttu-id="8ef34-211">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="8ef34-211">Mac/Linux</span></span>    | <span data-ttu-id="8ef34-212">`$XDG_DATA_HOME` (genellikle `~/.local/share` veya `/usr/local/share` , işletim sistemi dağıtımına bağlı olarak)</span><span class="sxs-lookup"><span data-stu-id="8ef34-212">`$XDG_DATA_HOME` (typically `~/.local/share` or `/usr/local/share`, depending on OS distribution)</span></span>|

### <a name="nugetdefaultsconfig-settings"></a><span data-ttu-id="8ef34-213">NuGetDefaults.Config ayarları</span><span class="sxs-lookup"><span data-stu-id="8ef34-213">NuGetDefaults.Config settings</span></span>

- <span data-ttu-id="8ef34-214">`packageSources`: Bu koleksiyon, `packageSources` Normal yapılandırma dosyaları ile aynı anlama sahiptir ve varsayılan kaynakları belirtir.</span><span class="sxs-lookup"><span data-stu-id="8ef34-214">`packageSources`: this collection has the same meaning as `packageSources` in regular config files and specifies the default sources.</span></span> <span data-ttu-id="8ef34-215">NuGet, yönetim biçimini kullanarak projelerdeki paketleri yükleme veya güncelleştirme sırasında kaynakları kullanır `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="8ef34-215">NuGet uses the sources in order when installing or updating packages in projects using the `packages.config` management format.</span></span> <span data-ttu-id="8ef34-216">, PackageReference biçimini kullanan projeler için, NuGet önce yerel kaynakları, ardından ağ paylaşımlarında kaynakları, sonra da yapılandırma dosyalarındaki sıra ne olursa olsun HTTP kaynaklarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="8ef34-216">For projects using the PackageReference format, NuGet uses local sources first, then sources on network shares, then HTTP sources, regardless of the order in the configuration files.</span></span> <span data-ttu-id="8ef34-217">NuGet, geri yükleme işlemlerine sahip kaynakların sırasını her zaman yoksayar.</span><span class="sxs-lookup"><span data-stu-id="8ef34-217">NuGet always ignores the order of sources with restore operations.</span></span>

- <span data-ttu-id="8ef34-218">`disabledPackageSources`: Bu koleksiyonda ayrıca `NuGet.Config` , etkilenen her kaynağın adına ve `true` / `false` devre dışı olup olmadığını gösteren bir değere göre listelendiği, dosyalardaki gibi aynı anlamı vardır.</span><span class="sxs-lookup"><span data-stu-id="8ef34-218">`disabledPackageSources`: this collection also has the same meaning as in `NuGet.Config` files, where each affected source is listed by its name and a `true`/`false` value indicating whether it's disabled.</span></span> <span data-ttu-id="8ef34-219">Bu, kaynak adının ve URL 'nin `packageSources` Varsayılan olarak açık olmadan ' de kalmasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="8ef34-219">This allows the source name and URL to remain in `packageSources` without having it turned on by default.</span></span> <span data-ttu-id="8ef34-220">Bireysel geliştiriciler daha sonra `false` `NuGet.Config` doğru URL 'yi bulmaya gerek kalmadan kaynağın değerini diğer dosyalarda olarak ayarlayarak kaynağı yeniden etkinleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="8ef34-220">Individual developers can then re-enable the source by setting the source's value to `false` in other `NuGet.Config` files without having to find the correct URL again.</span></span> <span data-ttu-id="8ef34-221">Bu, geliştiricilere yalnızca bireysel ekibin kaynağını varsayılan olarak etkinleştirirken bir kuruluşun iç kaynak URL 'lerinin tam listesini sağlamak için de kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="8ef34-221">This is also useful to supply developers with a full list of internal source URLs for an organization while enabling only an individual team's source by default.</span></span>

- <span data-ttu-id="8ef34-222">`defaultPushSource`: `nuget push` yerleşik varsayılanı geçersiz kılan işlemler için varsayılan hedefi belirtir `nuget.org` .</span><span class="sxs-lookup"><span data-stu-id="8ef34-222">`defaultPushSource`: specifies the default target for `nuget push` operations, overriding the built-in default of `nuget.org`.</span></span> <span data-ttu-id="8ef34-223">Yöneticiler `nuget.org` , özellikle ' de yayımlamak üzere kullanmaları gereken şekilde, iç paketleri yanlışlıkla yanlışlıkla herkese yayınlayamaması için bu ayarı dağıtabilir `nuget push -Source` `nuget.org` .</span><span class="sxs-lookup"><span data-stu-id="8ef34-223">Administrators can deploy this setting to avoid publishing internal packages to the public `nuget.org` by accident, as developers specifically need to use `nuget push -Source` to publish to `nuget.org`.</span></span>

### <a name="example-nugetdefaultsconfig-and-application"></a><span data-ttu-id="8ef34-224">Örnek NuGetDefaults.Config ve uygulama</span><span class="sxs-lookup"><span data-stu-id="8ef34-224">Example NuGetDefaults.Config and application</span></span>

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
