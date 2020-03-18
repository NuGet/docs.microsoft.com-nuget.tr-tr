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
# <a name="common-nuget-configurations"></a><span data-ttu-id="ef33a-103">Ortak NuGet yapılandırması</span><span class="sxs-lookup"><span data-stu-id="ef33a-103">Common NuGet configurations</span></span>

<span data-ttu-id="ef33a-104">NuGet davranışı, proje, Kullanıcı ve bilgisayar genelindeki düzeylerde bulunabilir bir veya daha fazla `NuGet.Config` (XML) dosyasında birikmiş ayarlar tarafından çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="ef33a-104">NuGet's behavior is driven by the accumulated settings in one or more `NuGet.Config` (XML) files that can exist at project-, user-, and computer-wide levels.</span></span> <span data-ttu-id="ef33a-105">Genel bir `NuGetDefaults.Config` dosyası, paket kaynaklarını da özellikle yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="ef33a-105">A global `NuGetDefaults.Config` file also specifically configures package sources.</span></span> <span data-ttu-id="ef33a-106">Ayarlar, CLı, Paket Yöneticisi konsolu ve Paket Yöneticisi Kullanıcı arabiriminde verilen tüm komutlara uygulanır.</span><span class="sxs-lookup"><span data-stu-id="ef33a-106">Settings apply to all commands issued in the CLI, the Package Manager Console, and the Package Manager UI.</span></span>

## <a name="config-file-locations-and-uses"></a><span data-ttu-id="ef33a-107">Yapılandırma dosyası konumları ve kullanımları</span><span class="sxs-lookup"><span data-stu-id="ef33a-107">Config file locations and uses</span></span>

| <span data-ttu-id="ef33a-108">Kapsam</span><span class="sxs-lookup"><span data-stu-id="ef33a-108">Scope</span></span> | <span data-ttu-id="ef33a-109">NuGet. config dosyası konumu</span><span class="sxs-lookup"><span data-stu-id="ef33a-109">NuGet.Config file location</span></span> | <span data-ttu-id="ef33a-110">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ef33a-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ef33a-111">Çözüm</span><span class="sxs-lookup"><span data-stu-id="ef33a-111">Solution</span></span> | <span data-ttu-id="ef33a-112">Geçerli klasör (diğer adıyla, çözüm klasörü) veya sürücü köküne kadar herhangi bir klasör.</span><span class="sxs-lookup"><span data-stu-id="ef33a-112">Current folder (aka Solution folder) or any folder up to the drive root.</span></span>| <span data-ttu-id="ef33a-113">Bir çözüm klasöründe, ayarlar alt klasörlerdeki tüm projelere uygulanır.</span><span class="sxs-lookup"><span data-stu-id="ef33a-113">In a solution folder, settings apply to all projects in subfolders.</span></span> <span data-ttu-id="ef33a-114">Bir yapılandırma dosyası bir proje klasörüne yerleştirilmişse, projenin bu proje üzerinde hiçbir etkisi olmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ef33a-114">Note that if a config file is placed in a project folder, it has no effect on that project.</span></span> |
| <span data-ttu-id="ef33a-115">Kullanıcı</span><span class="sxs-lookup"><span data-stu-id="ef33a-115">User</span></span> | <span data-ttu-id="ef33a-116">Windows: `%appdata%\NuGet\NuGet.Config`</span><span class="sxs-lookup"><span data-stu-id="ef33a-116">Windows: `%appdata%\NuGet\NuGet.Config`</span></span><br/><span data-ttu-id="ef33a-117">Mac/Linux: `~/.config/NuGet/NuGet.Config` veya `~/.nuget/NuGet/NuGet.Config` (işletim sistemi dağıtımına göre değişir)</span><span class="sxs-lookup"><span data-stu-id="ef33a-117">Mac/Linux: `~/.config/NuGet/NuGet.Config` or `~/.nuget/NuGet/NuGet.Config` (varies by OS distribution)</span></span> | <span data-ttu-id="ef33a-118">Ayarlar tüm işlemlere uygulanır, ancak proje düzeyindeki tüm ayarlar tarafından geçersiz kılınır.</span><span class="sxs-lookup"><span data-stu-id="ef33a-118">Settings apply to all operations, but are overridden by any project-level settings.</span></span> |
| <span data-ttu-id="ef33a-119">Bilgisayar</span><span class="sxs-lookup"><span data-stu-id="ef33a-119">Computer</span></span> | <span data-ttu-id="ef33a-120">Windows: `%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="ef33a-120">Windows: `%ProgramFiles(x86)%\NuGet\Config`</span></span><br/><span data-ttu-id="ef33a-121">Mac/Linux: `$XDG_DATA_HOME`.</span><span class="sxs-lookup"><span data-stu-id="ef33a-121">Mac/Linux: `$XDG_DATA_HOME`.</span></span> <span data-ttu-id="ef33a-122">`$XDG_DATA_HOME` null veya boş ise, `~/.local/share` veya `/usr/local/share` kullanılır (işletim sistemi dağıtımına göre değişir)</span><span class="sxs-lookup"><span data-stu-id="ef33a-122">If `$XDG_DATA_HOME` is null or empty, `~/.local/share` or `/usr/local/share` will be used (varies by OS distribution)</span></span>  | <span data-ttu-id="ef33a-123">Ayarlar bilgisayardaki tüm işlemlere uygulanır, ancak herhangi bir kullanıcı veya proje düzeyi ayar tarafından geçersiz kılınır.</span><span class="sxs-lookup"><span data-stu-id="ef33a-123">Settings apply to all operations on the computer, but are overridden by any user- or project-level settings.</span></span> |

<span data-ttu-id="ef33a-124">NuGet 'in önceki sürümleri için notlar:</span><span class="sxs-lookup"><span data-stu-id="ef33a-124">Notes for earlier versions of NuGet:</span></span>
- <span data-ttu-id="ef33a-125">NuGet 3,3 ve önceki sürümleri, çözüm genelinde ayarlar için bir `.nuget` klasörü kullandı.</span><span class="sxs-lookup"><span data-stu-id="ef33a-125">NuGet 3.3 and earlier used a `.nuget` folder for solution-wide settings.</span></span> <span data-ttu-id="ef33a-126">Bu klasör NuGet 3.4 + ' de kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="ef33a-126">This folder is not used in NuGet 3.4+.</span></span>
- <span data-ttu-id="ef33a-127">NuGet 2,6 için 3. x, Windows üzerindeki bilgisayar düzeyi yapılandırma dosyası%ProgramData%\NuGet\Config [\\{IDE} [\\{Version} [\\{SKU}]]] \Nuget.exe} konumunda bulunuyor; burada *{IDE}* *VisualStudio*, *{Version}* , *14,0*gibi Visual Studio sürümüdür ve *{SKU}* *Community*, *Pro*ya da *Enterprise*.</span><span class="sxs-lookup"><span data-stu-id="ef33a-127">For NuGet 2.6 to 3.x, the computer-level config file on Windows was located in %ProgramData%\NuGet\Config[\\{IDE}[\\{Version}[\\{SKU}]]]\NuGet.Config, where *{IDE}* can be *VisualStudio*, *{Version}* was the Visual Studio version such as *14.0*, and *{SKU}* is either *Community*, *Pro*, or *Enterprise*.</span></span> <span data-ttu-id="ef33a-128">Ayarları NuGet 4.0 + ' ya geçirmek için yapılandırma dosyasını% ProgramFiles (x86)% \ Nuget\configkonumuna kopyalamanız yeterlidir. Linux 'ta, bu önceki konum/etc/opt ve Mac üzerinde/Library/Application Support desteği idi.</span><span class="sxs-lookup"><span data-stu-id="ef33a-128">To migrate settings to NuGet 4.0+, simply copy the config file to %ProgramFiles(x86)%\NuGet\Config. On Linux, this previous location was /etc/opt, and on Mac, /Library/Application Support.</span></span>

## <a name="changing-config-settings"></a><span data-ttu-id="ef33a-129">Yapılandırma ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="ef33a-129">Changing config settings</span></span>

<span data-ttu-id="ef33a-130">`NuGet.Config` dosyası, [NuGet yapılandırma ayarları](../reference/nuget-config-file.md) konusunda açıklandığı gibi anahtar/değer çiftlerini içeren basıt bir XML metin dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="ef33a-130">A `NuGet.Config` file is a simple XML text file containing key/value pairs as described in the [NuGet Configuration Settings](../reference/nuget-config-file.md) topic.</span></span>

<span data-ttu-id="ef33a-131">Ayarlar, NuGet CLı [yapılandırma komutu](../reference/cli-reference/cli-ref-config.md)kullanılarak yönetilir:</span><span class="sxs-lookup"><span data-stu-id="ef33a-131">Settings are managed using the NuGet CLI [config command](../reference/cli-reference/cli-ref-config.md):</span></span>
- <span data-ttu-id="ef33a-132">Varsayılan olarak, değişiklikler Kullanıcı düzeyi yapılandırma dosyasında yapılır.</span><span class="sxs-lookup"><span data-stu-id="ef33a-132">By default, changes are made to the user-level config file.</span></span>
- <span data-ttu-id="ef33a-133">Farklı bir dosyadaki ayarları değiştirmek için `-configFile` anahtarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="ef33a-133">To change settings in a different file, use the `-configFile` switch.</span></span> <span data-ttu-id="ef33a-134">Bu durumda, dosyalar herhangi bir dosya adını kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="ef33a-134">In this case files can use any filename.</span></span>
- <span data-ttu-id="ef33a-135">Anahtarlar her zaman büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="ef33a-135">Keys are always case sensitive.</span></span>
- <span data-ttu-id="ef33a-136">Bilgisayar düzeyi ayarları dosyasındaki ayarları değiştirmek için yükseltme gereklidir.</span><span class="sxs-lookup"><span data-stu-id="ef33a-136">Elevation is required to change settings in the computer-level settings file.</span></span>

> [!Warning]
> <span data-ttu-id="ef33a-137">Dosyayı herhangi bir metin düzenleyicisinde değiştirebilseniz de, NuGet (v 3.4.3 ve üzeri), hatalı biçimlendirilmiş XML (eşleşmeyen Etiketler, geçersiz tırnak işaretleri vb.) içeriyorsa tüm yapılandırma dosyalarını sessizce yoksayar.</span><span class="sxs-lookup"><span data-stu-id="ef33a-137">Although you can modify the file in any text editor, NuGet (v3.4.3 and later) silently ignores the entire configuration file if it contains malformed XML (mismatched tags, invalid quotation marks, etc.).</span></span> <span data-ttu-id="ef33a-138">`nuget config`kullanılarak ayarların yönetilmesi tercih edilir.</span><span class="sxs-lookup"><span data-stu-id="ef33a-138">This is why it's preferable to manage setting using `nuget config`.</span></span>

### <a name="setting-a-value"></a><span data-ttu-id="ef33a-139">Değer ayarlama</span><span class="sxs-lookup"><span data-stu-id="ef33a-139">Setting a value</span></span>

<span data-ttu-id="ef33a-140">Windows:</span><span class="sxs-lookup"><span data-stu-id="ef33a-140">Windows:</span></span>

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\Config\NuGet.Config
```

<span data-ttu-id="ef33a-141">Mac/Linux:</span><span class="sxs-lookup"><span data-stu-id="ef33a-141">Mac/Linux:</span></span>

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
> <span data-ttu-id="ef33a-142">NuGet 3,4 ve üzeri sürümlerde, `repositoryPath=%PACKAGEHOME%` (Windows) ve `repositoryPath=$PACKAGEHOME` (Mac/Linux) gibi herhangi bir değerde ortam değişkenlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef33a-142">In NuGet 3.4 and later you can use environment variables in any value, as in `repositoryPath=%PACKAGEHOME%` (Windows) and `repositoryPath=$PACKAGEHOME` (Mac/Linux).</span></span>

### <a name="removing-a-value"></a><span data-ttu-id="ef33a-143">Değer kaldırma</span><span class="sxs-lookup"><span data-stu-id="ef33a-143">Removing a value</span></span>

<span data-ttu-id="ef33a-144">Bir değeri kaldırmak için, boş bir değere sahip bir anahtar belirtin.</span><span class="sxs-lookup"><span data-stu-id="ef33a-144">To remove a value, specify a key with an empty value.</span></span>

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a><span data-ttu-id="ef33a-145">Yeni bir yapılandırma dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="ef33a-145">Creating a new config file</span></span>

<span data-ttu-id="ef33a-146">Aşağıdaki şablonu yeni dosyaya kopyalayın ve sonra değerleri ayarlamak için `nuget config -configFile <filename>` kullanın:</span><span class="sxs-lookup"><span data-stu-id="ef33a-146">Copy the template below into the new file and then use `nuget config -configFile <filename>` to set values:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a><span data-ttu-id="ef33a-147">Ayarlar nasıl uygulanır</span><span class="sxs-lookup"><span data-stu-id="ef33a-147">How settings are applied</span></span>

<span data-ttu-id="ef33a-148">Birden çok `NuGet.Config` dosyası, tek bir projeye, bir proje grubuna veya tüm projelere uygulanabilmeleri için ayarları farklı konumlarda depolamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="ef33a-148">Multiple `NuGet.Config` files allow you to store settings in different locations so that they apply to a single project, a group of projects, or all projects.</span></span> <span data-ttu-id="ef33a-149">Bu ayarlar, bir projeye veya geçerli klasöre "en yakın" olan ayarlar ile, komut satırından veya Visual Studio 'dan çağrılan herhangi bir NuGet işleminde toplu olarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="ef33a-149">These settings collectively apply to any NuGet operation invoked from the command line or from Visual Studio, with settings that exist "closest" to a project or the current folder taking precedence.</span></span>

<span data-ttu-id="ef33a-150">Özellikle, NuGet ayarları farklı yapılandırma dosyalarından aşağıdaki sırada yükler:</span><span class="sxs-lookup"><span data-stu-id="ef33a-150">Specifically, NuGet loads settings from the different config files in the following order:</span></span>

1. <span data-ttu-id="ef33a-151">Yalnızca paket kaynaklarıyla ilgili ayarları içeren [Nugetdefaults. config dosyası](#nuget-defaults-file).</span><span class="sxs-lookup"><span data-stu-id="ef33a-151">The [NuGetDefaults.Config file](#nuget-defaults-file), which contains settings related only to package sources.</span></span>
1. <span data-ttu-id="ef33a-152">Bilgisayar düzeyindeki dosya.</span><span class="sxs-lookup"><span data-stu-id="ef33a-152">The computer-level file.</span></span>
1. <span data-ttu-id="ef33a-153">Kullanıcı düzeyi dosyası.</span><span class="sxs-lookup"><span data-stu-id="ef33a-153">The user-level file.</span></span>
1. <span data-ttu-id="ef33a-154">`-configFile`ile belirtilen dosya.</span><span class="sxs-lookup"><span data-stu-id="ef33a-154">The file specified with `-configFile`.</span></span>
1. <span data-ttu-id="ef33a-155">Sürücü kökünden geçerli klasöre (NuGet. exe ' nin çağrıldığı veya Visual Studio projesini içeren klasör) yoldaki her klasörde bulunan dosyalar.</span><span class="sxs-lookup"><span data-stu-id="ef33a-155">Files found in every folder in the path from the drive root to the current folder (where nuget.exe is invoked or the folder containing the Visual Studio project).</span></span> <span data-ttu-id="ef33a-156">Örneğin, bir komut c:\A\B\C içinde çağrılırsa, NuGet c:\, sonra c:\A, ardından c:\A\B ve son olarak c:\A\B\C. içindeki yapılandırma dosyalarını arar ve yükler.</span><span class="sxs-lookup"><span data-stu-id="ef33a-156">For example, if a command is invoked in c:\A\B\C, NuGet looks for and loads config files in c:\, then c:\A, then c:\A\B, and finally c:\A\B\C.</span></span>

<span data-ttu-id="ef33a-157">NuGet bu dosyalardaki ayarları bulduğundan, bunlar aşağıdaki gibi uygulanır:</span><span class="sxs-lookup"><span data-stu-id="ef33a-157">As NuGet finds settings in these files, they are applied as follows:</span></span>

1. <span data-ttu-id="ef33a-158">Tek öğe öğelerinde, NuGet aynı anahtar için önceden bulunan tüm değeri değiştirdi.</span><span class="sxs-lookup"><span data-stu-id="ef33a-158">For single-item elements, NuGet replaced any previously-found value for the same key.</span></span> <span data-ttu-id="ef33a-159">Bu, geçerli klasöre veya projeye "en yakın" olan ayarların daha önce bulduğu diğer tüm diğerlerini geçersiz kıldığı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="ef33a-159">This means that settings that are "closest" to the current folder or project override any others found earlier.</span></span> <span data-ttu-id="ef33a-160">Örneğin, `NuGetDefaults.Config` `defaultPushSource` ayarı başka herhangi bir yapılandırma dosyasında varsa geçersiz kılınır.</span><span class="sxs-lookup"><span data-stu-id="ef33a-160">For example, the `defaultPushSource` setting in `NuGetDefaults.Config` is overridden if it exists in any other config file.</span></span>

1. <span data-ttu-id="ef33a-161">Koleksiyon öğeleri için (örneğin, `<packageSources>`), NuGet tüm yapılandırma dosyalarındaki değerleri tek bir koleksiyon olarak birleştirir.</span><span class="sxs-lookup"><span data-stu-id="ef33a-161">For collection elements (such as `<packageSources>`), NuGet combines the values from all configuration files into a single collection.</span></span>

1. <span data-ttu-id="ef33a-162">Belirli bir düğüm için `<clear />` mevcut olduğunda, NuGet bu düğüm için önceden tanımlanmış yapılandırma değerlerini yoksayar.</span><span class="sxs-lookup"><span data-stu-id="ef33a-162">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span>

### <a name="settings-walkthrough"></a><span data-ttu-id="ef33a-163">Ayarlar izlenecek yol</span><span class="sxs-lookup"><span data-stu-id="ef33a-163">Settings walkthrough</span></span>

<span data-ttu-id="ef33a-164">İki ayrı sürücüde aşağıdaki klasör yapısına sahip olduğunu varsayalım:</span><span class="sxs-lookup"><span data-stu-id="ef33a-164">Let's say you have the following folder structure on two separate drives:</span></span>

    disk_drive_1
        User
    disk_drive_2
       Project1
         Source
       Project2
         Source
       tmp

<span data-ttu-id="ef33a-165">Daha sonra, belirtilen içeriğe sahip aşağıdaki konumlarda dört `NuGet.Config` dosyası vardır.</span><span class="sxs-lookup"><span data-stu-id="ef33a-165">You then have four `NuGet.Config` files in the following locations with the given content.</span></span> <span data-ttu-id="ef33a-166">(Bilgisayar düzeyindeki dosya bu örneğe dahil değildir, ancak kullanıcı düzeyindeki dosyada benzer şekilde davranır.)</span><span class="sxs-lookup"><span data-stu-id="ef33a-166">(The computer-level file is not included in this example, but would behave similarly to the user-level file.)</span></span>

<span data-ttu-id="ef33a-167">Dosya A. Kullanıcı düzeyi dosya, (Windows üzerinde`%appdata%\NuGet\NuGet.Config`, Mac/Linux 'ta `~/.config/NuGet/NuGet.Config`):</span><span class="sxs-lookup"><span data-stu-id="ef33a-167">File A. User-level file, (`%appdata%\NuGet\NuGet.Config` on Windows, `~/.config/NuGet/NuGet.Config` on Mac/Linux):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="ef33a-168">Dosya B. disk_drive_2/NuGet.exe:</span><span class="sxs-lookup"><span data-stu-id="ef33a-168">File B. disk_drive_2/NuGet.Config:</span></span>

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

<span data-ttu-id="ef33a-169">Dosya C. disk_drive_2/Project1/NuGet,config:</span><span class="sxs-lookup"><span data-stu-id="ef33a-169">File C. disk_drive_2/Project1/NuGet.Config:</span></span>

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

<span data-ttu-id="ef33a-170">Dosya D. disk_drive_2/Project2/NuGet.exe:</span><span class="sxs-lookup"><span data-stu-id="ef33a-170">File D. disk_drive_2/Project2/NuGet.Config:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

<span data-ttu-id="ef33a-171">Ardından NuGet, çağrıldığı yere bağlı olarak ayarları yükler ve aşağıdaki gibi uygular:</span><span class="sxs-lookup"><span data-stu-id="ef33a-171">NuGet then loads and applies settings as follows, depending on where it's invoked:</span></span>

- <span data-ttu-id="ef33a-172">**Disk_drive_1/Users 'Den çağrılır**: yalnızca Kullanıcı düzeyi yapılandırma dosyasında (A) listelenen varsayılan depo, disk_drive_1 üzerinde bulunan tek dosya olduğu için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ef33a-172">**Invoked from disk_drive_1/users**: Only the default repository listed in the user-level configuration file (A) is used, because that's the only file found on disk_drive_1.</span></span>

- <span data-ttu-id="ef33a-173">**Disk_drive_2/veya disk_drive_/tmp**: önce Kullanıcı düzeyi dosya (A) yüklenir, ardından NuGet disk_drive_2 köküne gider ve dosyayı bulur (B).</span><span class="sxs-lookup"><span data-stu-id="ef33a-173">**Invoked from disk_drive_2/ or disk_drive_/tmp**: The user-level file (A) is loaded first, then NuGet goes to the root of disk_drive_2 and finds file (B).</span></span> <span data-ttu-id="ef33a-174">NuGet Ayrıca/tmp ' de bir yapılandırma dosyası arar ancak bir tane bulmaz.</span><span class="sxs-lookup"><span data-stu-id="ef33a-174">NuGet also looks for a configuration file in /tmp but does not find one.</span></span> <span data-ttu-id="ef33a-175">Sonuç olarak, nuget.org üzerindeki varsayılan depo kullanılır, paket geri yükleme etkinleştirilir ve paketler disk_drive_2/tmpa 'da genişletilir.</span><span class="sxs-lookup"><span data-stu-id="ef33a-175">As a result, the default repository on nuget.org is used, package restore is enabled, and packages get expanded in disk_drive_2/tmp.</span></span>

- <span data-ttu-id="ef33a-176">**Disk_drive_2/Project1 veya disk_drive_2/Project1/Source: ' dan çağrıldığında**, önce Kullanıcı düzeyi dosya (A) yüklenir, ardından NuGet dosyayı (B) disk_drive_2 kökünden, ardından dosyayı (C) yükler.</span><span class="sxs-lookup"><span data-stu-id="ef33a-176">**Invoked from disk_drive_2/Project1 or disk_drive_2/Project1/Source**: The user-level file (A) is loaded first, then NuGet loads file (B) from the root of disk_drive_2, followed by file (C).</span></span> <span data-ttu-id="ef33a-177">(C) içindeki ayarlar, (B) ve (A) içindeki ayarları geçersiz kılar, bu nedenle paketlerin yüklendiği `repositoryPath`/Project1/External/Packages *disk_drive_2/tmp*yerine disk_drive_2.</span><span class="sxs-lookup"><span data-stu-id="ef33a-177">Settings in (C) override those in (B) and (A), so the `repositoryPath` where packages get installed is disk_drive_2/Project1/External/Packages instead of *disk_drive_2/tmp*.</span></span> <span data-ttu-id="ef33a-178">Ayrıca, (C) `<packageSources>`temizlemediğinden, nuget.org artık `https://MyPrivateRepo/ES/nuget`yalnızca bir kaynak olarak kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="ef33a-178">Also, because (C) clears `<packageSources>`, nuget.org is no longer available as a source leaving only `https://MyPrivateRepo/ES/nuget`.</span></span>

- <span data-ttu-id="ef33a-179">**Disk_drive_2/Project2 veya disk_drive_2/Project2/Source**: ' dan önce dosya (b) ve dosya (D) ile birlikte Kullanıcı düzeyi dosya (A) yüklenir.</span><span class="sxs-lookup"><span data-stu-id="ef33a-179">**Invoked from disk_drive_2/Project2 or disk_drive_2/Project2/Source**: The user-level file (A) is loaded first followed by file (B) and file (D).</span></span> <span data-ttu-id="ef33a-180">`packageSources` temizlenmediği için hem `nuget.org` hem de `https://MyPrivateRepo/DQ/nuget` kaynak olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ef33a-180">Because `packageSources` is not cleared, both `nuget.org` and `https://MyPrivateRepo/DQ/nuget` are available as sources.</span></span> <span data-ttu-id="ef33a-181">Paketler, (B) ' de belirtildiği gibi disk_drive_2/tmp ' de genişletilir.</span><span class="sxs-lookup"><span data-stu-id="ef33a-181">Packages get expanded in disk_drive_2/tmp as specified in (B).</span></span>

## <a name="nuget-defaults-file"></a><span data-ttu-id="ef33a-182">NuGet Varsayılanları dosyası</span><span class="sxs-lookup"><span data-stu-id="ef33a-182">NuGet defaults file</span></span>

<span data-ttu-id="ef33a-183">`NuGetDefaults.Config` dosyası, paketlerin yüklendiği ve güncelleştirildiği paket kaynaklarını belirtmek ve paketleri `nuget push`ile yayımlamaya yönelik varsayılan hedefi denetlemek için bulunur.</span><span class="sxs-lookup"><span data-stu-id="ef33a-183">The `NuGetDefaults.Config` file exists to specify package sources from which packages are installed and updated, and to control the default target for publishing packages with `nuget push`.</span></span> <span data-ttu-id="ef33a-184">Yöneticiler uygun şekilde (örneğin grup ilkesi kullanarak), tutarlı `NuGetDefaults.Config` dosyalarını geliştirici ve derleme makinelerine dağıtmak için, kuruluştaki herkesin nuget.org yerine doğru paket kaynaklarını kullandığından emin olabilirler.</span><span class="sxs-lookup"><span data-stu-id="ef33a-184">Because administrators can conveniently (using Group Policy, for example) deploy consistent `NuGetDefaults.Config` files to developer and build machines, they can ensure that everyone in the organization is using the correct package sources rather than nuget.org.</span></span>

> [!Important]
> <span data-ttu-id="ef33a-185">`NuGetDefaults.Config` dosyası hiçbir şekilde bir geliştiricinin NuGet yapılandırmasından bir paket kaynağının kaldırılmasına neden olmaz.</span><span class="sxs-lookup"><span data-stu-id="ef33a-185">The `NuGetDefaults.Config` file never causes a package source to be removed from a developer's NuGet configuration.</span></span> <span data-ttu-id="ef33a-186">Yani, geliştirici zaten NuGet kullanıyorsa ve bu nedenle nuget.org paket kaynağı kayıtlıysa, bir `NuGetDefaults.Config` dosyası oluşturulduktan sonra kaldırılmaz.</span><span class="sxs-lookup"><span data-stu-id="ef33a-186">That means if the developer has already used NuGet and therefore has the nuget.org package source registered, it won't be removed after the creation of a `NuGetDefaults.Config` file.</span></span>
>
> <span data-ttu-id="ef33a-187">Ayrıca, NuGet 'de ne `NuGetDefaults.Config` ne de başka bir mekanizma nuget.org gibi paket kaynaklarına erişimi engelleyebilir. Bir kuruluş söz konusu erişimi engellemeyi istiyorsa, bunun için güvenlik duvarları gibi diğer yollarla kullanılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ef33a-187">Furthermore, neither `NuGetDefaults.Config` nor any other mechanism in NuGet can prevent access to package sources like nuget.org. If an organization wishes to block such access, it must use other means such as firewalls to do so.</span></span>

### <a name="nugetdefaultsconfig-location"></a><span data-ttu-id="ef33a-188">NuGetDefaults. config konumu</span><span class="sxs-lookup"><span data-stu-id="ef33a-188">NuGetDefaults.Config location</span></span>

<span data-ttu-id="ef33a-189">Aşağıdaki tabloda, hedef işletim sistemine bağlı olarak `NuGetDefaults.Config` dosyasının nerede saklanacağı açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="ef33a-189">The following table describes where the `NuGetDefaults.Config` file should be stored, depending on the target OS:</span></span>

| <span data-ttu-id="ef33a-190">İşletim sistemi platformu</span><span class="sxs-lookup"><span data-stu-id="ef33a-190">OS Platform</span></span>  | <span data-ttu-id="ef33a-191">NuGetDefaults. config konumu</span><span class="sxs-lookup"><span data-stu-id="ef33a-191">NuGetDefaults.Config Location</span></span> |
| --- | --- |
| <span data-ttu-id="ef33a-192">Windows</span><span class="sxs-lookup"><span data-stu-id="ef33a-192">Windows</span></span>      | <span data-ttu-id="ef33a-193">**Visual Studio 2017 veya NuGet 4. x +:** `%ProgramFiles(x86)%\NuGet\Config`</span><span class="sxs-lookup"><span data-stu-id="ef33a-193">**Visual Studio 2017 or NuGet 4.x+:** `%ProgramFiles(x86)%\NuGet\Config`</span></span> <br /><span data-ttu-id="ef33a-194">**Visual Studio 2015 ve öncesi ya da NuGet 3. x ve öncesi:** `%PROGRAMDATA%\NuGet`</span><span class="sxs-lookup"><span data-stu-id="ef33a-194">**Visual Studio 2015 and earlier or NuGet 3.x and earlier:** `%PROGRAMDATA%\NuGet`</span></span> |
| <span data-ttu-id="ef33a-195">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="ef33a-195">Mac/Linux</span></span>    | <span data-ttu-id="ef33a-196">`$XDG_DATA_HOME` (genellikle `~/.local/share` veya `/usr/local/share`, işletim sistemi dağıtımına bağlı olarak)</span><span class="sxs-lookup"><span data-stu-id="ef33a-196">`$XDG_DATA_HOME` (typically `~/.local/share` or `/usr/local/share`, depending on OS distribution)</span></span>|

### <a name="nugetdefaultsconfig-settings"></a><span data-ttu-id="ef33a-197">NuGetDefaults. config ayarları</span><span class="sxs-lookup"><span data-stu-id="ef33a-197">NuGetDefaults.Config settings</span></span>

- <span data-ttu-id="ef33a-198">`packageSources`: Bu koleksiyon, normal yapılandırma dosyalarındaki `packageSources` aynı anlama sahiptir ve varsayılan kaynakları belirtir.</span><span class="sxs-lookup"><span data-stu-id="ef33a-198">`packageSources`: this collection has the same meaning as `packageSources` in regular config files and specifies the default sources.</span></span> <span data-ttu-id="ef33a-199">NuGet, `packages.config` yönetim biçimini kullanarak projelerdeki paketleri yükleme veya güncelleştirme sırasında kaynakları kullanır.</span><span class="sxs-lookup"><span data-stu-id="ef33a-199">NuGet uses the sources in order when installing or updating packages in projects using the `packages.config` management format.</span></span> <span data-ttu-id="ef33a-200">, PackageReference biçimini kullanan projeler için, NuGet önce yerel kaynakları, ardından ağ paylaşımlarında kaynakları, sonra da yapılandırma dosyalarındaki sıra ne olursa olsun HTTP kaynaklarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="ef33a-200">For projects using the PackageReference format, NuGet uses local sources first, then sources on network shares, then HTTP sources, regardless of the order in the configuration files.</span></span> <span data-ttu-id="ef33a-201">NuGet, geri yükleme işlemlerine sahip kaynakların sırasını her zaman yoksayar.</span><span class="sxs-lookup"><span data-stu-id="ef33a-201">NuGet always ignores the order of sources with restore operations.</span></span>

- <span data-ttu-id="ef33a-202">`disabledPackageSources`: Bu koleksiyonda ayrıca, etkilenen her kaynağın adı ve devre dışı olup olmadığını gösteren bir doğru/yanlış değeri tarafından listelenen `NuGet.Config` dosyaları ile aynı anlamı vardır.</span><span class="sxs-lookup"><span data-stu-id="ef33a-202">`disabledPackageSources`: this collection also has the same meaning as in `NuGet.Config` files, where each affected source is listed by its name and a true/false value indicating whether it's disabled.</span></span> <span data-ttu-id="ef33a-203">Bu, kaynak adının ve URL 'nin varsayılan olarak açık olmadan `packageSources` devam etmesine izin verir.</span><span class="sxs-lookup"><span data-stu-id="ef33a-203">This allows the source name and URL to remain in `packageSources` without having it turned on by default.</span></span> <span data-ttu-id="ef33a-204">Bireysel geliştiriciler daha sonra doğru URL 'yi bulmayı gerektirmeden kaynağın değerini diğer `NuGet.Config` dosyalarında false olarak ayarlayarak kaynağı yeniden etkinleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="ef33a-204">Individual developers can then re-enable the source by setting the source's value to false in other `NuGet.Config` files without having to find the correct URL again.</span></span> <span data-ttu-id="ef33a-205">Bu, geliştiricilere yalnızca bireysel ekibin kaynağını varsayılan olarak etkinleştirirken bir kuruluşun iç kaynak URL 'lerinin tam listesini sağlamak için de kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="ef33a-205">This is also useful to supply developers with a full list of internal source URLs for an organization while enabling only an individual team's source by default.</span></span>

- <span data-ttu-id="ef33a-206">`defaultPushSource`: `nuget push` işlemleri için varsayılan hedefi belirtir, nuget.org 'in yerleşik varsayılan öğesini geçersiz kılar. Yöneticiler, nuget.org ' a yayımlamak için özellikle `nuget push -Source` kullanmaları gerektiğinde, iç paketlerin yanlışlıkla yanlışlıkla, genel yayımlamasını önlemek için bu ayarı dağıtabilir.</span><span class="sxs-lookup"><span data-stu-id="ef33a-206">`defaultPushSource`: specifies the default target for `nuget push` operations, overriding the built-in default of nuget.org. Administrators can deploy this setting to avoid publishing internal packages to the public nuget.org by accident, as developers specifically need to use `nuget push -Source` to publish to nuget.org.</span></span>

### <a name="example-nugetdefaultsconfig-and-application"></a><span data-ttu-id="ef33a-207">Örnek NuGetDefaults. config ve uygulama</span><span class="sxs-lookup"><span data-stu-id="ef33a-207">Example NuGetDefaults.Config and application</span></span>

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
