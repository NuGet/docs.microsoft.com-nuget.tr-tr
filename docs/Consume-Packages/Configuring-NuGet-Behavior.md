---
title: "NuGet davranışını yapılandırma | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet.Config dosyaları, hem genel hem de proje başına temelinde NuGet davranışını denetlemek ve nuget config komutu ile değiştirilmelidir."
keywords: "NuGet yapılandırma dosyaları, NuGet yapılandırması, NuGet davranış ayarları, NuGet ayarları, Nuget.Config, NuGetDefaults.Config, Varsayılanları"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2ab3e6dad852214ac9bb93f7df0a8c3fef10b9dc
ms.sourcegitcommit: df21fe770900644d476d51622a999597a6f20ef8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/12/2018
---
# <a name="configuring-nuget-behavior"></a><span data-ttu-id="652d6-104">NuGet davranışını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="652d6-104">Configuring NuGet behavior</span></span>

<span data-ttu-id="652d6-105">NuGet davranışı güdümlü bir veya daha fazla birikmiş ayarlar tarafından `NuGet.Config` proje-, kullanıcı- ve bilgisayar genelinde düzeyinde bulunabilir (XML) dosyaları.</span><span class="sxs-lookup"><span data-stu-id="652d6-105">NuGet's behavior is driven by the accumulated settings in one or more `NuGet.Config` (XML) files that can exist at project-, user-, and computer-wide levels.</span></span> <span data-ttu-id="652d6-106">Bir genel `NuGetDefaults.Config` dosyası, özellikle de paket kaynaklarını yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="652d6-106">A global `NuGetDefaults.Config` file also specifically configures package sources.</span></span> <span data-ttu-id="652d6-107">Ayarlar CLI, Paket Yöneticisi konsolu ve Paket Yöneticisi kullanıcı Arabirimi yürütülen tüm komutlar için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="652d6-107">Settings apply to all commands issued in the CLI, the Package Manager Console, and the Package Manager UI.</span></span>

## <a name="config-file-locations-and-uses"></a><span data-ttu-id="652d6-108">Config dosya konumları ve kullanır</span><span class="sxs-lookup"><span data-stu-id="652d6-108">Config file locations and uses</span></span>

| <span data-ttu-id="652d6-109">Kapsam</span><span class="sxs-lookup"><span data-stu-id="652d6-109">Scope</span></span> | <span data-ttu-id="652d6-110">NuGet.Config dosya konumu</span><span class="sxs-lookup"><span data-stu-id="652d6-110">NuGet.Config file location</span></span> | <span data-ttu-id="652d6-111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="652d6-111">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="652d6-112">Proje</span><span class="sxs-lookup"><span data-stu-id="652d6-112">Project</span></span> | <span data-ttu-id="652d6-113">Geçerli klasör (diğer adıyla proje klasörü) veya sürücü kök kadar herhangi bir klasör.</span><span class="sxs-lookup"><span data-stu-id="652d6-113">Current folder (aka Project folder) or any folder up to the drive root.</span></span>| <span data-ttu-id="652d6-114">Bir proje klasöründe ayarlar yalnızca bu proje için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="652d6-114">In a project folder, settings apply only to that project.</span></span> <span data-ttu-id="652d6-115">Birden çok proje alt klasör içeren üst klasörlerde ayarlar bu klasörlerdeki tüm projeleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="652d6-115">In parent folders that contain multiple projects subfolders, settings apply to all projects in those subfolders.</span></span> |
| <span data-ttu-id="652d6-116">Kullanıcı</span><span class="sxs-lookup"><span data-stu-id="652d6-116">User</span></span> | <span data-ttu-id="652d6-117">Windows: %APPDATA%\NuGet\NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="652d6-117">Windows: %APPDATA%\NuGet\NuGet.Config</span></span><br/><span data-ttu-id="652d6-118">Mac/Linux: ~/.nuget/NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="652d6-118">Mac/Linux: ~/.nuget/NuGet.Config</span></span> | <span data-ttu-id="652d6-119">Ayarları tüm işlemleri için geçerlidir, ancak herhangi bir proje düzeyi ayarı tarafından geçersiz kılınır.</span><span class="sxs-lookup"><span data-stu-id="652d6-119">Settings apply to all operations, but are overridden by any project-level settings.</span></span> |
| <span data-ttu-id="652d6-120">Bilgisayar</span><span class="sxs-lookup"><span data-stu-id="652d6-120">Computer</span></span> | <span data-ttu-id="652d6-121">Windows: %ProgramFiles(x86)%\NuGet\Config</span><span class="sxs-lookup"><span data-stu-id="652d6-121">Windows: %ProgramFiles(x86)%\NuGet\Config</span></span><br/><span data-ttu-id="652d6-122">Mac/Linux: $XDG_DATA_HOME (typically ~/.local/share)</span><span class="sxs-lookup"><span data-stu-id="652d6-122">Mac/Linux: $XDG_DATA_HOME (typically ~/.local/share)</span></span> | <span data-ttu-id="652d6-123">Ayarlar bilgisayar üzerinde tüm işlemler için geçerli olan, ancak herhangi bir kullanıcı veya proje düzeyi ayarı tarafından kılınmadı.</span><span class="sxs-lookup"><span data-stu-id="652d6-123">Settings apply to all operations on the computer, but are overriden by any user- or project-level settings.</span></span> |

<span data-ttu-id="652d6-124">NuGet'ın önceki sürümlerini için Notlar:</span><span class="sxs-lookup"><span data-stu-id="652d6-124">Notes for earlier versions of NuGet:</span></span>
- <span data-ttu-id="652d6-125">NuGet 3.3 ve daha önce kullanılan bir `.nuget` çözüm genelindeki ayarları için klasör.</span><span class="sxs-lookup"><span data-stu-id="652d6-125">NuGet 3.3 and earlier used a `.nuget` folder for solution-wide settings.</span></span> <span data-ttu-id="652d6-126">Bu dosya NuGet 3.4 + kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="652d6-126">This file is not used in NuGet 3.4+.</span></span>
- <span data-ttu-id="652d6-127">3.x için NuGet 2.6 için Windows bilgisayar düzeyinde yapılandırma dosyası % ProgramData%\NuGet\Config bulunamadı [\\{IDE} [\\{Version} [\\{SKU}]]]\NuGet.Config, burada *{IDE}* olabilir *Visual Studio*, *{Version}* Visual Studio sürümü gibi edildi *14.0*, ve *{SKU}* ya *topluluk*, *Pro*, veya *Kurumsal*.</span><span class="sxs-lookup"><span data-stu-id="652d6-127">For NuGet 2.6 to 3.x, the computer-level config file on Windows was located in %ProgramData%\NuGet\Config[\\{IDE}[\\{Version}[\\{SKU}]]]\NuGet.Config, where *{IDE}* can be *VisualStudio*, *{Version}* was the Visual Studio version such as *14.0*, and *{SKU}* is either *Community*, *Pro*, or *Enterprise*.</span></span> <span data-ttu-id="652d6-128">Nuget'e 4.0 + ayarlarını geçirmek için yapılandırma dosyası % ProgramFiles(x86) % \NuGet\Config kopyalayın. Linux üzerinde /etc/opt, önceki bu konumda olan ve Mac, Library/Application Support.</span><span class="sxs-lookup"><span data-stu-id="652d6-128">To migrate settings to NuGet 4.0+, simply copy the config file to %ProgramFiles(x86)%\NuGet\Config. On Linux, this previous location was /etc/opt, and on Mac, /Library/Application Support.</span></span>

## <a name="changing-config-settings"></a><span data-ttu-id="652d6-129">Yapılandırma ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="652d6-129">Changing config settings</span></span>

<span data-ttu-id="652d6-130">A `NuGet.Config` dosyasıdır açıklandığı gibi anahtar/değer çiftleri içeren basit bir XML metin dosyası [NuGet yapılandırma ayarlarını](../reference/nuget-config-file.md) konu.</span><span class="sxs-lookup"><span data-stu-id="652d6-130">A `NuGet.Config` file is a simple XML text file containing key/value pairs as described in the [NuGet Configuration Settings](../reference/nuget-config-file.md) topic.</span></span>

<span data-ttu-id="652d6-131">Ayarları NuGet CLI kullanarak yönetilen [config komutunu](../tools/cli-ref-config.md):</span><span class="sxs-lookup"><span data-stu-id="652d6-131">Settings are managed using the NuGet CLI [config command](../tools/cli-ref-config.md):</span></span>
- <span data-ttu-id="652d6-132">Varsayılan olarak, kullanıcı düzeyinde yapılandırma dosyasına değişiklik yapılmaz.</span><span class="sxs-lookup"><span data-stu-id="652d6-132">By default, changes are made to the user-level config file.</span></span>
- <span data-ttu-id="652d6-133">Farklı bir dosya ayarlarını değiştirmek için kullanmak `-configFile` geçin.</span><span class="sxs-lookup"><span data-stu-id="652d6-133">To change settings in a different file, use the `-configFile` switch.</span></span> <span data-ttu-id="652d6-134">Bu durumda dosyalarını dosya kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="652d6-134">In this case files can use any filename.</span></span>
- <span data-ttu-id="652d6-135">Anahtarları her zaman büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="652d6-135">Keys are always case sensitive.</span></span>
- <span data-ttu-id="652d6-136">Yükseltme, bilgisayar düzeyinde ayarları dosyasında ayarlarını değiştirmek için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="652d6-136">Elevation is required to change settings in the computer-level settings file.</span></span>

> [!Warning]
> <span data-ttu-id="652d6-137">Herhangi bir metin düzenleyicisi, NuGet dosyasında yapılandırabilseniz (v3.4.3 ve sonraki sürümler) hatalı biçimlendirilmiş XML (eşleşmeyen etiketler, geçersiz tırnak işaretleri, vb.) içeriyorsa, tüm yapılandırma dosyası sessizce yok sayar.</span><span class="sxs-lookup"><span data-stu-id="652d6-137">Although you can modify the file in any text editor, NuGet (v3.4.3 and later) silently ignores the entire configuration file if it contains malformed XML (mismatched tags, invalid quotation marks, etc.).</span></span> <span data-ttu-id="652d6-138">Kullanarak yönetmek için tercih edilir bu yüzden `nuget config`.</span><span class="sxs-lookup"><span data-stu-id="652d6-138">This is why it's preferable to manage setting using `nuget config`.</span></span>

### <a name="setting-a-value"></a><span data-ttu-id="652d6-139">Bir değer ayarlanması</span><span class="sxs-lookup"><span data-stu-id="652d6-139">Setting a value</span></span>

<span data-ttu-id="652d6-140">Windows:</span><span class="sxs-lookup"><span data-stu-id="652d6-140">Windows:</span></span>

```cli
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\NuGet.Config
```

<span data-ttu-id="652d6-141">Mac/Linux:</span><span class="sxs-lookup"><span data-stu-id="652d6-141">Mac/Linux:</span></span>

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
> <span data-ttu-id="652d6-142">NuGet 3.4 ve daha sonra herhangi bir değer ortam değişkenleri olarak kullanabileceğiniz `repositoryPath=%PACKAGEHOME%` (Windows) ve `repositoryPath=%PACKAGEHOME` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="652d6-142">In NuGet 3.4 and later you can use environment variables in any value, as in `repositoryPath=%PACKAGEHOME%` (Windows) and `repositoryPath=%PACKAGEHOME` (Mac/Linux).</span></span>

### <a name="removing-a-value"></a><span data-ttu-id="652d6-143">Bir değer kaldırma</span><span class="sxs-lookup"><span data-stu-id="652d6-143">Removing a value</span></span>

<span data-ttu-id="652d6-144">Bir değer kaldırmak için bir anahtar ile boş bir değer belirtin.</span><span class="sxs-lookup"><span data-stu-id="652d6-144">To remove a value, specify a key with an empty value.</span></span>

```cli
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a><span data-ttu-id="652d6-145">Yeni bir yapılandırma dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="652d6-145">Creating a new config file</span></span>

<span data-ttu-id="652d6-146">Aşağıdaki şablonu yeni dosyaya kopyalayın ve ardından `nuget config --configFile <filename>` değerlerini ayarlamak için:</span><span class="sxs-lookup"><span data-stu-id="652d6-146">Copy the template below into the new file and then use `nuget config --configFile <filename>` to set values:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

## <a name="how-settings-are-applied"></a><span data-ttu-id="652d6-147">Ayarları nasıl uygulanır</span><span class="sxs-lookup"><span data-stu-id="652d6-147">How settings are applied</span></span>

<span data-ttu-id="652d6-148">Birden çok `NuGet.Config` dosyaları tek bir proje, bir grup projesini veya tüm projeleri için geçerli olacak şekilde farklı konumlarda ayarlarını depolamak izin verir.</span><span class="sxs-lookup"><span data-stu-id="652d6-148">Multiple `NuGet.Config` files allow you to store settings in different locations so that they apply to a single project, a group of projects, or all projects.</span></span> <span data-ttu-id="652d6-149">Bu ayarlar, topluca "en yakın" bir proje veya öncelik alma geçerli klasörde mevcut ayarlarla komut satırından veya Visual Studio'dan çağrılan herhangi bir NuGet işlemi için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="652d6-149">These settings collectively apply to any NuGet operation invoked from the command line or from Visual Studio, with settings that exist "closest" to a project or the current folder taking precedence.</span></span>

<span data-ttu-id="652d6-150">Özellikle, NuGet aşağıdaki sırayla farklı yapılandırma dosyalarından ayarları yükler:</span><span class="sxs-lookup"><span data-stu-id="652d6-150">Specifically, NuGet loads settings from the different config files in the following order:</span></span>

1. <span data-ttu-id="652d6-151">[NuGetDefaults.Config dosya](#nuget-defaults-file), yalnızca paket kaynaklarını ilgili ayarları içerir.</span><span class="sxs-lookup"><span data-stu-id="652d6-151">The [NuGetDefaults.Config file](#nuget-defaults-file), which contains settings related only to package sources.</span></span>
1. <span data-ttu-id="652d6-152">Bilgisayar düzeyinde dosya.</span><span class="sxs-lookup"><span data-stu-id="652d6-152">The computer-level file.</span></span>
1. <span data-ttu-id="652d6-153">Kullanıcı düzeyinde dosya.</span><span class="sxs-lookup"><span data-stu-id="652d6-153">The user-level file.</span></span>
1. <span data-ttu-id="652d6-154">Belirtilen dosya `-configFile`.</span><span class="sxs-lookup"><span data-stu-id="652d6-154">The file specified with `-configFile`.</span></span>
1. <span data-ttu-id="652d6-155">Her yolu geçerli bir klasör (burada nuget.exe çağrılır veya Visual Studio projeyi içeren klasörü) sürücüsünün kök klasöründe bulunan dosyaları.</span><span class="sxs-lookup"><span data-stu-id="652d6-155">Files found in every folder in the path from the drive root to the current folder (where nuget.exe is invoked or the folder containing the Visual Studio project).</span></span> <span data-ttu-id="652d6-156">Örneğin, bir komut içinde c:\A\B\C çağrılırsa, NuGet arar ve c: yapılandırma dosyalarını yükler\, sonra c:\A, ardından c:\A\B ve son olarak c:\A\B\C.</span><span class="sxs-lookup"><span data-stu-id="652d6-156">For example, if a command is invoked in c:\A\B\C, NuGet looks for and loads config files in c:\, then c:\A, then c:\A\B, and finally c:\A\B\C.</span></span>

<span data-ttu-id="652d6-157">NuGet bu dosyalarda ayarları buldukça, bunlar aşağıdaki gibi uygulanır:</span><span class="sxs-lookup"><span data-stu-id="652d6-157">As NuGet finds settings in these files, they are applied as follows:</span></span>

1. <span data-ttu-id="652d6-158">Tek öğeli öğeleri için NuGet aynı anahtar için daha önce bulunan değeri değiştirildi.</span><span class="sxs-lookup"><span data-stu-id="652d6-158">For single-item elements, NuGet replaced any previously-found value for the same key.</span></span> <span data-ttu-id="652d6-159">Bu, "geçerli klasörde veya projesini yakın" ayarlarını herhangi diğer daha önce bulunan geçersiz kılmak anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="652d6-159">This means that settings that are "closest" to the current folder or project override any others found earlier.</span></span> <span data-ttu-id="652d6-160">Örneğin, `defaultPushSource` ayarı `NuGetDefaults.Config` başka bir yapılandırma dosyasında varsa geçersiz kılınır.</span><span class="sxs-lookup"><span data-stu-id="652d6-160">For example, the `defaultPushSource` setting in `NuGetDefaults.Config` is overridden if it exists in any other config file.</span></span>

1. <span data-ttu-id="652d6-161">Koleksiyon öğeleri için (gibi `<packageSources>`), NuGet tek bir koleksiyona tüm yapılandırma dosyalarını değerleri birleştirir.</span><span class="sxs-lookup"><span data-stu-id="652d6-161">For collection elements (such as `<packageSources>`), NuGet combines the values from all configuration files into a single collection.</span></span>

1. <span data-ttu-id="652d6-162">Zaman `<clear />` mevcut olduğu için belirli bir düğüm, bu düğüm için önceden tanımlanmış yapılandırma değerlerini NuGet yoksayar.</span><span class="sxs-lookup"><span data-stu-id="652d6-162">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span>

### <a name="settings-walkthrough"></a><span data-ttu-id="652d6-163">Ayarları gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="652d6-163">Settings walkthrough</span></span>

<span data-ttu-id="652d6-164">İki ayrı sürücü üzerinde aşağıdaki klasör yapısına sahip varsayalım:</span><span class="sxs-lookup"><span data-stu-id="652d6-164">Let's say you have the following folder structure on two separate drives:</span></span>

    disk_drive_1
        User
    disk_drive_2
       Project1
         Source
       Project2
         Source
       tmp

<span data-ttu-id="652d6-165">Dört sonra sahip `NuGet.Config` dosyaları aşağıdaki konumlarda verilen içeriğe sahip.</span><span class="sxs-lookup"><span data-stu-id="652d6-165">You then have four `NuGet.Config` files in the following locations with the given content.</span></span> <span data-ttu-id="652d6-166">(Bilgisayar düzeyinde dosya bu örnekte yer almaz, ancak kullanıcı düzeyinde dosyasına benzer şekilde davranacaktır.)</span><span class="sxs-lookup"><span data-stu-id="652d6-166">(The computer-level file is not included in this example, but would behave similarly to the user-level file.)</span></span>

<span data-ttu-id="652d6-167">A. kullanıcı düzeyinde dosyası, (Windows, Mac/Linux'ta ~/.nuget/NuGet.Config %APPDATA%\NuGet\NuGet.Config):</span><span class="sxs-lookup"><span data-stu-id="652d6-167">File A. User-level file, (%APPDATA%\NuGet\NuGet.Config on Windows, ~/.nuget/NuGet.Config on Mac/Linux):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="652d6-168">File B. disk_drive_2/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="652d6-168">File B. disk_drive_2/NuGet.Config:</span></span>

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

<span data-ttu-id="652d6-169">File C. disk_drive_2/Project1/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="652d6-169">File C. disk_drive_2/Project1/NuGet.Config:</span></span>

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

<span data-ttu-id="652d6-170">File D. disk_drive_2/Project2/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="652d6-170">File D. disk_drive_2/Project2/NuGet.Config:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

<span data-ttu-id="652d6-171">NuGet sonra yükler ve burada çağrılır bağlı olarak aşağıdaki gibi ayarları uygular:</span><span class="sxs-lookup"><span data-stu-id="652d6-171">NuGet then loads and applies settings as follows, depending on where it's invoked:</span></span>

- <span data-ttu-id="652d6-172">**Disk_drive_1/kullanıcılardan çağrılan**: disk_drive_1 üzerinde bulunan yalnızca dosya olduğu için kullanıcı düzeyinde yapılandırma dosyasında (A) listelenen varsayılan depo kullanılır.</span><span class="sxs-lookup"><span data-stu-id="652d6-172">**Invoked from disk_drive_1/users**: Only the default repository listed in the user-level configuration file (A) is used, because that's the only file found on disk_drive_1.</span></span>

- <span data-ttu-id="652d6-173">**Disk_drive_2 çağrılan / veya disk_drive_/tmp**: kullanıcı düzeyinde dosya (A) ilk olarak, yüklendikten sonra NuGet disk_drive_2 kök dizinine gider ve bulur dosyası (B).</span><span class="sxs-lookup"><span data-stu-id="652d6-173">**Invoked from disk_drive_2/ or disk_drive_/tmp**: The user-level file (A) is loaded first, then NuGet goes to the root of disk_drive_2 and finds file (B).</span></span> <span data-ttu-id="652d6-174">NuGet de tmp yapılandırma dosyasında görünüyor, ancak bir bulmaz.</span><span class="sxs-lookup"><span data-stu-id="652d6-174">NuGet also looks for a configuration file in /tmp but does not find one.</span></span> <span data-ttu-id="652d6-175">Sonuç olarak, nuget.org varsayılan havuzda kullanıldığında, paket geri yükleme etkin ve paketleri disk_drive_2/tmp genişletilmiş.</span><span class="sxs-lookup"><span data-stu-id="652d6-175">As a result, the default repository on nuget.org is used, package restore is enabled, and packages get expanded in disk_drive_2/tmp.</span></span>

- <span data-ttu-id="652d6-176">**Disk_drive_2/Project1 veya Project1/disk_drive_2/kaynağından çağrılan**: kullanıcı düzeyinde dosya (A) önce yüklenir, ardından NuGet yükleri (B) ve ardından disk_drive_2 kök dosyası (C).</span><span class="sxs-lookup"><span data-stu-id="652d6-176">**Invoked from disk_drive_2/Project1 or disk_drive_2/Project1/Source**: The user-level file (A) is loaded first, then NuGet loads file (B) from the root of disk_drive_2, followed by file (C).</span></span> <span data-ttu-id="652d6-177">(C) ayarları geçersiz kılar (B) ve (A), böylece `repositoryPath` disk_drive_2/Project1/dış/paketleri yerine olan paketler yüklendiği *disk_drive_2/tmp*.</span><span class="sxs-lookup"><span data-stu-id="652d6-177">Settings in (C) override those in (B) and (A), so the `repositoryPath` where packages get installed is disk_drive_2/Project1/External/Packages instead of *disk_drive_2/tmp*.</span></span> <span data-ttu-id="652d6-178">Ayrıca, (C) temizler çünkü `<packageSources>`, nuget.org yalnızca bırakarak kaynağı olarak kullanılabilir artık `https://MyPrivateRepo/ES/nuget`.</span><span class="sxs-lookup"><span data-stu-id="652d6-178">Also, because (C) clears `<packageSources>`, nuget.org is no longer available as a source leaving only `https://MyPrivateRepo/ES/nuget`.</span></span>

- <span data-ttu-id="652d6-179">**Disk_drive_2/Project2 veya Project2/disk_drive_2/kaynağından çağrılan**: kullanıcı düzeyinde dosya (A) ilk dosyası (B) ve tarafından dosyası (D) ve ardından yüklenir.</span><span class="sxs-lookup"><span data-stu-id="652d6-179">**Invoked from disk_drive_2/Project2 or disk_drive_2/Project2/Source**: The user-level file (A) is loaded first followed by file (B) and file (D).</span></span> <span data-ttu-id="652d6-180">Çünkü `packageSources` değil işaretli değilse, her ikisi de `nuget.org` ve `https://MyPrivateRepo/DQ/nuget` kaynakları olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="652d6-180">Because `packageSources` is not cleared, both `nuget.org` and `https://MyPrivateRepo/DQ/nuget` are available as sources.</span></span> <span data-ttu-id="652d6-181">Paketleri disk_drive_2/tmp (B) belirtildiği gibi genişletilmiş.</span><span class="sxs-lookup"><span data-stu-id="652d6-181">Packages get expanded in disk_drive_2/tmp as specified in (B).</span></span>

## <a name="nuget-defaults-file"></a><span data-ttu-id="652d6-182">NuGet Varsayılanları dosyası</span><span class="sxs-lookup"><span data-stu-id="652d6-182">NuGet defaults file</span></span>

<span data-ttu-id="652d6-183">`NuGetDefaults.Config` Dosyasından içinden paketleri yüklü ve güncelleştirilmiş paket kaynaklarını belirtin ve paketlerle yayımlamak için varsayılan hedef denetlemek için `nuget push`.</span><span class="sxs-lookup"><span data-stu-id="652d6-183">The `NuGetDefaults.Config` file exists to specify package sources from which packages are installed and updated, and to control the default target for publishing packages with `nuget push`.</span></span> <span data-ttu-id="652d6-184">Yöneticiler kolaylıkla bakımından (örneğin Grup İlkesi kullanılarak) tutarlı dağıtmak `NuGetDefaults.Config` Geliştirici ve yapı makineleri dosyalara, bir yönetici şunları yapabilir kuruluştaki herkesin nuget.org yerine doğru paket kaynaklarını kullandığını sağlama.</span><span class="sxs-lookup"><span data-stu-id="652d6-184">Because administrators can conveniently (using Group Policy, for example) deploy consistent `NuGetDefaults.Config` files to developer and build machines, they can ensuring that everyone in the organization is using the correct package sources rather than nuget.org.</span></span>

> [!Important]
> <span data-ttu-id="652d6-185">`NuGetDefaults.Config` Dosyasının hiçbir zaman bir geliştiricinin NuGet yapılandırmasından kaldırmak bir paket kaynağı neden olur.</span><span class="sxs-lookup"><span data-stu-id="652d6-185">The `NuGetDefaults.Config` file never causes a package source to be removed from a developer's NuGet configuration.</span></span> <span data-ttu-id="652d6-186">Geliştirici NuGet zaten kullandı ve bu yüzden nuget.org paket kaynağı varsa, yani kayıtlı oluşturulmasından sonra kaldırılmadan olmaz bir `NuGetDefaults.Config` dosyası.</span><span class="sxs-lookup"><span data-stu-id="652d6-186">That means if the developer has already used NuGet and therefore has the nuget.org package source registered, it won't be removed after the creation of a `NuGetDefaults.Config` file.</span></span>
>
> <span data-ttu-id="652d6-187">Ayrıca, hiçbiri `NuGetDefaults.Config` veya başka bir mekanizma NuGet içinde nuget.org gibi paket kaynaklarına erişimi engelleyebilir. Bu tür erişimi engellemek bir kuruluş isterse, bu çok güvenlik duvarları gibi diğer yollarla Bunu yapmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="652d6-187">Furthermore, neither `NuGetDefaults.Config` nor any other mechanism in NuGet can prevent access to package sources like nuget.org. If an organization wishes to block such access, it much use other means such as firewalls to do so.</span></span>

### <a name="nugetdefaultsconfig-location"></a><span data-ttu-id="652d6-188">NuGetDefaults.Config konumu</span><span class="sxs-lookup"><span data-stu-id="652d6-188">NuGetDefaults.Config location</span></span>

<span data-ttu-id="652d6-189">Aşağıdaki tabloda nerede tanımlar `NuGetDefaults.Config` dosyasının saklanması gereken, işletim sistemi hedef bağlı olarak:</span><span class="sxs-lookup"><span data-stu-id="652d6-189">The following table describes where the `NuGetDefaults.Config` file should be stored, depending on the target OS:</span></span>

| <span data-ttu-id="652d6-190">İşletim sistemi platformu</span><span class="sxs-lookup"><span data-stu-id="652d6-190">OS Platform</span></span>  | <span data-ttu-id="652d6-191">NuGetDefaults.Config Location</span><span class="sxs-lookup"><span data-stu-id="652d6-191">NuGetDefaults.Config Location</span></span> |
| --- | --- |
| <span data-ttu-id="652d6-192">Windows</span><span class="sxs-lookup"><span data-stu-id="652d6-192">Windows</span></span>      | <span data-ttu-id="652d6-193">**Visual Studio 2017 veya NuGet 4.x+:** % ProgramFiles (x86) %\NuGet\Config</span><span class="sxs-lookup"><span data-stu-id="652d6-193">**Visual Studio 2017 or NuGet 4.x+:** %ProgramFiles(x86)%\NuGet\Config</span></span> <br /><span data-ttu-id="652d6-194">**Visual Studio 2015 ve önceki ya da NuGet 3.x ve daha önceki sürümlerde:** %PROGRAMDATA%\NuGet</span><span class="sxs-lookup"><span data-stu-id="652d6-194">**Visual Studio 2015 and earlier or NuGet 3.x and earlier:** %PROGRAMDATA%\NuGet</span></span> |
| <span data-ttu-id="652d6-195">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="652d6-195">Mac/Linux</span></span>    | <span data-ttu-id="652d6-196">$XDG_DATA_HOME (genellikle ~/.local/share)</span><span class="sxs-lookup"><span data-stu-id="652d6-196">$XDG_DATA_HOME (typically ~/.local/share)</span></span>|

### <a name="nugetdefaultsconfig-settings"></a><span data-ttu-id="652d6-197">NuGetDefaults.Config ayarları</span><span class="sxs-lookup"><span data-stu-id="652d6-197">NuGetDefaults.Config settings</span></span>

- <span data-ttu-id="652d6-198">`packageSources`: Bu koleksiyonun aynı anlamı taşır `packageSources` normal olarak yapılandırma dosyaları ve varsayılan kaynakları belirtir.</span><span class="sxs-lookup"><span data-stu-id="652d6-198">`packageSources`: this collection has the same meaning as `packageSources` in regular config files and specifies the default sources.</span></span> <span data-ttu-id="652d6-199">NuGet kullandığı kaynakları yükleme ya da kullanarak projeleri paketlerinde güncelleştirilirken sırayla `packages.config` başvuru biçimi.</span><span class="sxs-lookup"><span data-stu-id="652d6-199">NuGet uses the sources in order when installing or updating packages in projects using the `packages.config` reference format.</span></span> <span data-ttu-id="652d6-200">PackageReference biçimi kullanarak projeleri için NuGet yerel kaynakları ilk kullanır ve ardından ağ paylaşımları ve yapılandırma dosyalarını sırayla bakılmaksızın HTTP kaynakları üzerindeki kaynakları.</span><span class="sxs-lookup"><span data-stu-id="652d6-200">For projects using the PackageReference format, NuGet uses local sources first, then sources on network shares, then HTTP sources, regardless of the order in the configuration files.</span></span> <span data-ttu-id="652d6-201">NuGet her zaman geri yükleme işlemleri kaynaklarıyla sırasını yok sayar.</span><span class="sxs-lookup"><span data-stu-id="652d6-201">NuGet always ignores the order of sources with restore operations.</span></span>

- <span data-ttu-id="652d6-202">`disabledPackageSources`: Bu koleksiyonun ayrıca olarak ile aynı anlamı taşır `NuGet.Config` dosyaları, burada her etkilenen kaynak listelenir adını ve belirten bir true/false değerine tarafından devre dışı bırakılıp bırakılmayacağını.</span><span class="sxs-lookup"><span data-stu-id="652d6-202">`disabledPackageSources`: this collection also has the same meaning as in `NuGet.Config` files, where each affected source is listed by its name and a true/false value indicating whether it's disabled.</span></span> <span data-ttu-id="652d6-203">Bu kaynak adı ve URL içinde kalmasını sağlar `packageSources` gerek kalmadan, varsayılan olarak açıktır.</span><span class="sxs-lookup"><span data-stu-id="652d6-203">This allows the source name and URL to remain in `packageSources` without having it turned on by default.</span></span> <span data-ttu-id="652d6-204">Her bir geliştirici daha sonra tekrar etkinleştirebilirsiniz kaynak false diğer kaynağın değeri ayarlayarak `NuGet.Config` doğru URL'yi yeniden bulmak zorunda kalmadan dosyaları.</span><span class="sxs-lookup"><span data-stu-id="652d6-204">Individual developers can then re-enable the source by setting the source's value to false in other `NuGet.Config` files without having to find the correct URL again.</span></span> <span data-ttu-id="652d6-205">Bu da geliştiricilerin iç kaynak URL'lerini varsayılan olarak yalnızca tek bir ekibin kaynağı etkinleştirme sırasında bir kuruluş için tam bir listesi ile sağlamak kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="652d6-205">This is also useful to supply developers with a full list of internal source URLs for an organization while enabling only an individual team's source by default.</span></span>

- <span data-ttu-id="652d6-206">`defaultPushSource`: için varsayılan hedef belirtir `nuget push` nuget.org yerleşik varsayılan geçersiz kılma işlemleri. Yöneticiler, yanlışlıkla, ortak nuget.org iç paketleri yayımlama önlemek için bu ayarı dağıtabilir, geliştiriciler özel olarak kullanmak gerek duyduğunuz `nuget push -Source` için nuget.org yayımlamak için.</span><span class="sxs-lookup"><span data-stu-id="652d6-206">`defaultPushSource`: specifies the default target for `nuget push` operations, overriding the built-in default of nuget.org. Administrators can deploy this setting to avoid publishing internal packages to the public nuget.org by accident, as developers specifically need to use `nuget push -Source` to publish to nuget.org.</span></span>

### <a name="example-nugetdefaultsconfig-and-application"></a><span data-ttu-id="652d6-207">Örnek NuGetDefaults.Config ve uygulama</span><span class="sxs-lookup"><span data-stu-id="652d6-207">Example NuGetDefaults.Config and application</span></span>

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
