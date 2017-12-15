---
title: "NuGet davranışını yapılandırma | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: c1e34826-d07d-4609-a0fd-123459ae89c5
description: "NuGet.Config dosyaları, hem genel hem de proje başına temelinde NuGet davranışını denetlemek ve nuget config komutu ile değiştirilmelidir."
keywords: "NuGet yapılandırma dosyaları, NuGet yapılandırması, NuGet davranış ayarları, NuGet ayarları, Nuget.Config, NuGetDefaults.Config, Varsayılanları"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f9e56b68f70387435cdaa1537db503abb912fd2a
ms.sourcegitcommit: 122bf7ce308365ea45da018b0768f0536de76a1f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="configuring-nuget-behavior"></a><span data-ttu-id="b15b1-104">NuGet davranışını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b15b1-104">Configuring NuGet behavior</span></span>

<span data-ttu-id="b15b1-105">NuGet davranışı güdümlü bir veya daha fazla birikmiş ayarlar tarafından `NuGet.Config` proje-, kullanıcı- ve bilgisayar genelinde düzeyinde bulunabilir (XML) dosyaları.</span><span class="sxs-lookup"><span data-stu-id="b15b1-105">NuGet's behavior is driven by the accumulated settings in one or more `NuGet.Config` (XML) files that can exist at project-, user-, and computer-wide levels.</span></span> <span data-ttu-id="b15b1-106">Bir genel `NuGetDefaults.Config` dosyası (2.7 +), özellikle de paket kaynaklarını yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="b15b1-106">A global `NuGetDefaults.Config` file (2.7+) also specifically configures package sources.</span></span> <span data-ttu-id="b15b1-107">Ayarlar CLI, Paket Yöneticisi konsolu ve Paket Yöneticisi kullanıcı Arabirimi yürütülen tüm komutlar için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="b15b1-107">Settings apply to all commands issued in the CLI, the Package Manager Console, and the Package Manager UI.</span></span>

<span data-ttu-id="b15b1-108">Bu konuda:</span><span class="sxs-lookup"><span data-stu-id="b15b1-108">In this topic:</span></span>

- [<span data-ttu-id="b15b1-109">NuGet.Config dosya konumları ve kullanır</span><span class="sxs-lookup"><span data-stu-id="b15b1-109">NuGet.Config file locations and uses</span></span>](#config-file-locations-and-uses)
- [<span data-ttu-id="b15b1-110">Ayarları değiştirme</span><span class="sxs-lookup"><span data-stu-id="b15b1-110">Changing settings</span></span>](#changing-config-settings)
- [<span data-ttu-id="b15b1-111">Ayarları nasıl uygulanır</span><span class="sxs-lookup"><span data-stu-id="b15b1-111">How settings are applied</span></span>](#how-settings-are-applied)
- [<span data-ttu-id="b15b1-112">NuGetDefaults.Config dosyası</span><span class="sxs-lookup"><span data-stu-id="b15b1-112">NuGetDefaults.Config file</span></span>](#nuget-defaults-file)

## <a name="config-file-locations-and-uses"></a><span data-ttu-id="b15b1-113">Config dosya konumları ve kullanır</span><span class="sxs-lookup"><span data-stu-id="b15b1-113">Config file locations and uses</span></span>

| <span data-ttu-id="b15b1-114">Kapsam</span><span class="sxs-lookup"><span data-stu-id="b15b1-114">Scope</span></span> | <span data-ttu-id="b15b1-115">NuGet.Config dosya konumu</span><span class="sxs-lookup"><span data-stu-id="b15b1-115">NuGet.Config file location</span></span> | <span data-ttu-id="b15b1-116">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b15b1-116">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b15b1-117">Project</span><span class="sxs-lookup"><span data-stu-id="b15b1-117">Project</span></span> | <span data-ttu-id="b15b1-118">Proje klasörünü veya sürücü kök kadar herhangi bir klasör</span><span class="sxs-lookup"><span data-stu-id="b15b1-118">Project folder or any folder up to the drive root</span></span> | <span data-ttu-id="b15b1-119">Bir proje klasöründe ayarlar yalnızca bu proje için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="b15b1-119">In a project folder, settings apply only to that project.</span></span> <span data-ttu-id="b15b1-120">Birden çok proje alt klasör içeren üst klasörlerde ayarlar bu klasörlerdeki tüm projeleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="b15b1-120">In parent folders that contain multiple projects subfolders, settings apply to all projects in those subfolders.</span></span> |
| <span data-ttu-id="b15b1-121">Kullanıcı</span><span class="sxs-lookup"><span data-stu-id="b15b1-121">User</span></span> | <span data-ttu-id="b15b1-122">Windows: %APPDATA%\NuGet\NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="b15b1-122">Windows: %APPDATA%\NuGet\NuGet.Config</span></span><br/><span data-ttu-id="b15b1-123">Mac/Linux: ~/.nuget/NuGet.Config</span><span class="sxs-lookup"><span data-stu-id="b15b1-123">Mac/Linux: ~/.nuget/NuGet.Config</span></span> | <span data-ttu-id="b15b1-124">Ayarları tüm işlemleri için geçerlidir, ancak herhangi bir proje düzeyi ayarı tarafından geçersiz kılınır.</span><span class="sxs-lookup"><span data-stu-id="b15b1-124">Settings apply to all operations, but are overridden by any project-level settings.</span></span> <span data-ttu-id="b15b1-125">CLI komutları kullanırken, farklı yapılandırma dosyası kullanarak belirtebilirsiniz `-configFile` varsayılan kullanıcı düzeyinde dosyasında herhangi bir ayarı yok saymak için anahtar.</span><span class="sxs-lookup"><span data-stu-id="b15b1-125">When using CLI commands, you can specify a different config file using the `-configFile` switch to ignore any settings in the default user-level file.</span></span> |
| <span data-ttu-id="b15b1-126">Bilgisayar</span><span class="sxs-lookup"><span data-stu-id="b15b1-126">Computer</span></span> | <span data-ttu-id="b15b1-127">Windows: % ProgramFiles (x86) %\NuGet\Config</span><span class="sxs-lookup"><span data-stu-id="b15b1-127">Windows: %ProgramFiles(x86)%\NuGet\Config</span></span><br/><span data-ttu-id="b15b1-128">Mac/Linux: $XDG_DATA_HOME (genellikle ~/.local/share)</span><span class="sxs-lookup"><span data-stu-id="b15b1-128">Mac/Linux: $XDG_DATA_HOME (typically ~/.local/share)</span></span> | <span data-ttu-id="b15b1-129">Ayarlar bilgisayar üzerinde tüm işlemler için geçerli olan, ancak herhangi bir kullanıcı veya proje düzeyi ayarı tarafından kılınmadı.</span><span class="sxs-lookup"><span data-stu-id="b15b1-129">Settings apply to all operations on the computer, but are overriden by any user- or project-level settings.</span></span> |

<span data-ttu-id="b15b1-130">NuGet'ın önceki sürümlerini için Notlar:</span><span class="sxs-lookup"><span data-stu-id="b15b1-130">Notes for earlier versions of NuGet:</span></span>
- <span data-ttu-id="b15b1-131">NuGet 3.3 ve daha önce kullanılan bir `.nuget` çözüm genelindeki ayarları için klasör.</span><span class="sxs-lookup"><span data-stu-id="b15b1-131">NuGet 3.3 and earlier used a `.nuget` folder for solution-wide settings.</span></span> <span data-ttu-id="b15b1-132">Bu dosya NuGet 3.4 + kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="b15b1-132">This file not used in NuGet 3.4+.</span></span>
- <span data-ttu-id="b15b1-133">3.x için NuGet 2.6 için Windows bilgisayar düzeyinde yapılandırma dosyası % ProgramData%\NuGet\Config bulunamadı [\\{IDE} [\\{Version} [\\{SKU}]]]\NuGet.Config, burada *{IDE}* olabilir *Visual Studio*, *{Version}* Visual Studio sürümü gibi edildi *14.0*, ve *{SKU}* ya *topluluk*, *Pro*, veya *Kurumsal*.</span><span class="sxs-lookup"><span data-stu-id="b15b1-133">For NuGet 2.6 to 3.x, the computer-level config file on Windows was located in %ProgramData%\NuGet\Config[\\{IDE}[\\{Version}[\\{SKU}]]]\NuGet.Config, where *{IDE}* can be *VisualStudio*, *{Version}* was the Visual Studio version such as *14.0*, and *{SKU}* is either *Community*, *Pro*, or *Enterprise*.</span></span> <span data-ttu-id="b15b1-134">Nuget'e 4.0 + ayarlarını geçirmek için yapılandırma dosyası % ProgramFiles(x86) % \NuGet\Config kopyalayın. Linus üzerinde /etc/opt, önceki bu konumda olan ve Mac, Library/Application Support.</span><span class="sxs-lookup"><span data-stu-id="b15b1-134">To migrate settings to NuGet 4.0+, simply copy the config file to %ProgramFiles(x86)%\NuGet\Config. On Linus, this previous location was /etc/opt, and on Mac, /Library/Application Support.</span></span>

## <a name="changing-config-settings"></a><span data-ttu-id="b15b1-135">Yapılandırma ayarlarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="b15b1-135">Changing config settings</span></span>

<span data-ttu-id="b15b1-136">A `NuGet.Config` dosyasıdır açıklandığı gibi anahtar/değer çiftleri içeren basit bir XML metin dosyası [NuGet yapılandırma ayarlarını](../Schema/nuget-config-file.md) konu.</span><span class="sxs-lookup"><span data-stu-id="b15b1-136">A `NuGet.Config` file is a simple XML text file containing key/value pairs as described in the [NuGet Configuration Settings](../Schema/nuget-config-file.md) topic.</span></span>

<span data-ttu-id="b15b1-137">Ayarları NuGet CLI kullanarak yönetilen [config komutunu](../tools/cli-ref-config.md):</span><span class="sxs-lookup"><span data-stu-id="b15b1-137">Settings are managed using the NuGet CLI [config command](../tools/cli-ref-config.md):</span></span>
- <span data-ttu-id="b15b1-138">Varsayılan olarak, kullanıcı düzeyinde yapılandırma dosyasına değişiklik yapılmaz.</span><span class="sxs-lookup"><span data-stu-id="b15b1-138">By default, changes are made to the user-level config file.</span></span>
- <span data-ttu-id="b15b1-139">Farklı bir dosya ayarlarını değiştirmek için kullanmak `-configFile` geçin.</span><span class="sxs-lookup"><span data-stu-id="b15b1-139">To change settings in a different file, use the `-configFile` switch.</span></span> <span data-ttu-id="b15b1-140">Bu durumda dosyalarını dosya kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b15b1-140">In this case files can use any filename.</span></span>
- <span data-ttu-id="b15b1-141">Anahtarları her zaman büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="b15b1-141">Keys are always case sensitive.</span></span>
- <span data-ttu-id="b15b1-142">Yükseltme, bilgisayar düzeyinde ayarları dosyasında ayarlarını değiştirmek için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="b15b1-142">Elevation is required to change settings in the computer-level settings file.</span></span>

> [!Warning]
> <span data-ttu-id="b15b1-143">Herhangi bir metin düzenleyicisi, NuGet dosyasında yapılandırabilseniz (v3.4.3 ve sonraki sürümler) hatalı biçimlendirilmiş XML (eşleşmeyen etiketler, geçersiz tırnak işaretleri, vb.) içeriyorsa, tüm yapılandırma dosyası sessizce yok sayar.</span><span class="sxs-lookup"><span data-stu-id="b15b1-143">Although you can modify the file in any text editor, NuGet (v3.4.3 and later) silently ignores the entire configuration file if it contains malformed XML (mismatched tags, invalid quotation marks, etc.).</span></span> <span data-ttu-id="b15b1-144">Kullanarak yönetmek için tercih edilir bu yüzden `nuget config`.</span><span class="sxs-lookup"><span data-stu-id="b15b1-144">This is why it's preferable to manage setting using `nuget config`.</span></span>

### <a name="setting-a-value"></a><span data-ttu-id="b15b1-145">Bir değer ayarlanması</span><span class="sxs-lookup"><span data-stu-id="b15b1-145">Setting a value</span></span>

<span data-ttu-id="b15b1-146">Windows:</span><span class="sxs-lookup"><span data-stu-id="b15b1-146">Windows:</span></span>

```
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=c:\packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=c:\packages -configfile c:\my.Config
nuget config -set repositoryPath=c:\packages -configfile .\myApp\NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=c:\packages -configfile %ProgramFiles(x86)%\NuGet\NuGet.Config
```

<span data-ttu-id="b15b1-147">Mac/Linux:</span><span class="sxs-lookup"><span data-stu-id="b15b1-147">Mac/Linux:</span></span>

```
# Set repositoryPath in the user-level config file
nuget config -set repositoryPath=/home/packages 

# Set repositoryPath in project-level files
nuget config -set repositoryPath=/home/projects/packages -configfile /home/my.Config
nuget config -set repositoryPath=/home/packages -configfile home/myApp/NuGet.Config

# Set repositoryPath in the computer-level file (requires elevation)
nuget config -set repositoryPath=/home/packages -configfile $XDG_DATA_HOME/NuGet.Config
```

> [!Note]
> <span data-ttu-id="b15b1-148">NuGet 3.4 ve daha sonra herhangi bir değer ortam değişkenleri olarak kullanabileceğiniz `repositoryPath=%PACKAGEHOME%` (Windows) ve `repositoryPath=%PACKAGEHOME` (Mac/Linux).</span><span class="sxs-lookup"><span data-stu-id="b15b1-148">In NuGet 3.4 and later you can use environment variables in any value, as in `repositoryPath=%PACKAGEHOME%` (Windows) and `repositoryPath=%PACKAGEHOME` (Mac/Linux).</span></span>

### <a name="removing-a-value"></a><span data-ttu-id="b15b1-149">Bir değer kaldırma</span><span class="sxs-lookup"><span data-stu-id="b15b1-149">Removing a value</span></span>

<span data-ttu-id="b15b1-150">Bir değer kaldırmak için bir anahtar ile boş bir değer belirtin.</span><span class="sxs-lookup"><span data-stu-id="b15b1-150">To remove a value, specify a key with an empty value.</span></span>

```
# Windows
nuget config -set repositoryPath= -configfile c:\my.Config

# Mac/Linux
nuget config -set repositoryPath= -configfile /home/my.Config
```

### <a name="creating-a-new-config-file"></a><span data-ttu-id="b15b1-151">Yeni bir yapılandırma dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="b15b1-151">Creating a new config file</span></span>

<span data-ttu-id="b15b1-152">Aşağıdaki şablonu yeni dosyaya kopyalayın ve ardından `nuget config --configFile <filename>` değerlerini ayarlamak için:</span><span class="sxs-lookup"><span data-stu-id="b15b1-152">Copy the template below into the new file and then use `nuget config --configFile <filename>` to set values:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
</configuration>
```

<br/>

## <a name="how-settings-are-applied"></a><span data-ttu-id="b15b1-153">Ayarları nasıl uygulanır</span><span class="sxs-lookup"><span data-stu-id="b15b1-153">How settings are applied</span></span>

<span data-ttu-id="b15b1-154">Birden çok `NuGet.Config` dosyaları tek bir proje, bir grup projesini veya tüm projeleri için geçerli olacak şekilde farklı konumlarda ayarlarını depolamak izin verir.</span><span class="sxs-lookup"><span data-stu-id="b15b1-154">Multiple `NuGet.Config` files allow you to store settings in different locations so that they apply to a single project, a group of projects, or all projects.</span></span> <span data-ttu-id="b15b1-155">Bu ayarlar, topluca "en yakın" bir proje veya öncelik alma geçerli klasörde mevcut ayarlarla komut satırından veya Visual Studio'dan çağrılan herhangi bir NuGet işlemi için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="b15b1-155">These settings collectively apply to any NuGet operation invoked from the command line or from Visual Studio, with settings that exist "closest" to a project or the current folder taking precedence.</span></span>

<span data-ttu-id="b15b1-156">Özellikle, NuGet aşağıdaki sırayla farklı yapılandırma dosyalarından ayarları yükler:</span><span class="sxs-lookup"><span data-stu-id="b15b1-156">Specifically, NuGet loads settings from the different config files in the following order:</span></span>

1. <span data-ttu-id="b15b1-157">[NuGetDefaults.Config dosya](#nuget-defaults-file), yalnızca paket kaynaklarını ilgili ayarları içerir.</span><span class="sxs-lookup"><span data-stu-id="b15b1-157">The [NuGetDefaults.Config file](#nuget-defaults-file), which contains settings related only to package sources.</span></span>
1. <span data-ttu-id="b15b1-158">Bilgisayar düzeyinde dosya.</span><span class="sxs-lookup"><span data-stu-id="b15b1-158">The computer-level file.</span></span>
1. <span data-ttu-id="b15b1-159">Kullanıcı düzeyinde dosya.</span><span class="sxs-lookup"><span data-stu-id="b15b1-159">The user-level file.</span></span>
1. <span data-ttu-id="b15b1-160">Belirtilen dosya `-configFile`.</span><span class="sxs-lookup"><span data-stu-id="b15b1-160">The file specified with `-configFile`.</span></span>
1. <span data-ttu-id="b15b1-161">Her yolu geçerli bir klasör (burada nuget.exe çağrılır veya Visual Studio projeyi içeren klasörü) sürücüsünün kök klasöründe bulunan dosyaları.</span><span class="sxs-lookup"><span data-stu-id="b15b1-161">Files found in every folder in the path from the drive root to the current folder (where nuget.exe is invoked or the folder containing the Visual Studio project).</span></span> <span data-ttu-id="b15b1-162">Örneğin, bir komut içinde c:\A\B\C çağrılırsa, NuGet arar ve c: yapılandırma dosyalarını yükler\, sonra c:\A, ardından c:\A\B ve son olarak c:\A\B\C.</span><span class="sxs-lookup"><span data-stu-id="b15b1-162">For example, if a command is invoked in c:\A\B\C, NuGet looks for and loads config files in c:\, then c:\A, then c:\A\B, and finally c:\A\B\C.</span></span>

<span data-ttu-id="b15b1-163">NuGet bu dosyalarda ayarları buldukça, bunlar aşağıdaki gibi uygulanır:</span><span class="sxs-lookup"><span data-stu-id="b15b1-163">As NuGet finds settings in these files, they are applied as follows:</span></span>

1. <span data-ttu-id="b15b1-164">Tek öğeli öğeleri için NuGet aynı anahtar için daha önce bulunan değeri değiştirildi.</span><span class="sxs-lookup"><span data-stu-id="b15b1-164">For single-item elements, NuGet replaced any previously-found value for the same key.</span></span> <span data-ttu-id="b15b1-165">Bu, "geçerli klasörde veya projesini yakın" ayarlarını herhangi diğer daha önce bulunan geçersiz kılmak anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="b15b1-165">This means that settings that are "closest" to the current folder or project override any others found earlier.</span></span> <span data-ttu-id="b15b1-166">Örneğin, `defaultPushSource` ayarı `NuGetDefaults.Config` başka bir yapılandırma dosyasında varsa geçersiz kılınır.</span><span class="sxs-lookup"><span data-stu-id="b15b1-166">For example, the `defaultPushSource` setting in `NuGetDefaults.Config` is overridden if it exists in any other config file.</span></span>

1. <span data-ttu-id="b15b1-167">Koleksiyon öğeleri için (gibi `<packageSources>`), NuGet tek bir koleksiyona tüm yapılandırma dosyalarını değerleri birleştirir.</span><span class="sxs-lookup"><span data-stu-id="b15b1-167">For collection elements (such as `<packageSources>`), NuGet combines the values from all configuration files into a single collection.</span></span>

1. <span data-ttu-id="b15b1-168">Zaman `<clear />` mevcut olduğu için belirli bir düğüm, bu düğüm için önceden tanımlanmış yapılandırma değerlerini NuGet yoksayar.</span><span class="sxs-lookup"><span data-stu-id="b15b1-168">When `<clear />` is present for a given node, NuGet ignores previously defined configuration values for that node.</span></span>

### <a name="settings-walkthrough"></a><span data-ttu-id="b15b1-169">Ayarları gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="b15b1-169">Settings walkthrough</span></span>

<span data-ttu-id="b15b1-170">İki ayrı sürücü üzerinde aşağıdaki klasör yapısına sahip varsayalım:</span><span class="sxs-lookup"><span data-stu-id="b15b1-170">Let's say you have the following folder structure on two separate drives:</span></span>

    disk_drive_1
        User
    disk_drive_2
       Project1
         Source
       Project2
         Source
       tmp

<span data-ttu-id="b15b1-171">Dört sonra sahip `NuGet.Config` dosyaları aşağıdaki konumlarda verilen içeriğe sahip.</span><span class="sxs-lookup"><span data-stu-id="b15b1-171">You then have four `NuGet.Config` files in the following locations with the given content.</span></span> <span data-ttu-id="b15b1-172">(Bilgisayar düzeyinde dosya bu örnekte yer almaz, ancak kullanıcı düzeyinde dosyasına benzer şekilde davranacaktır.)</span><span class="sxs-lookup"><span data-stu-id="b15b1-172">(The computer-level file is not included in this example, but would behave similarly to the user-level file.)</span></span>

<span data-ttu-id="b15b1-173">A. kullanıcı düzeyinde dosyası, (Windows, Mac/Linux'ta ~/.nuget/NuGet.Config %APPDATA%\NuGet\NuGet.Config):</span><span class="sxs-lookup"><span data-stu-id="b15b1-173">File A. User-level file, (%APPDATA%\NuGet\NuGet.Config on Windows, ~/.nuget/NuGet.Config on Mac/Linux):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <activePackageSource>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="b15b1-174">B. disk_drive_2/NuGet.Config dosya:</span><span class="sxs-lookup"><span data-stu-id="b15b1-174">File B. disk_drive_2/NuGet.Config:</span></span>

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

<span data-ttu-id="b15b1-175">C. dosya disk_drive_2/Project1/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="b15b1-175">File C. disk_drive_2/Project1/NuGet.Config:</span></span>

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

<span data-ttu-id="b15b1-176">Dosya D. disk_drive_2/Project2/NuGet.Config:</span><span class="sxs-lookup"><span data-stu-id="b15b1-176">File D. disk_drive_2/Project2/NuGet.Config:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <packageSources>
        <!-- Add this repository to the list of available repositories -->
        <add key="MyPrivateRepo - DQ" value="https://MyPrivateRepo/DQ/nuget" />
    </packageSources>
</configuration>
```

<span data-ttu-id="b15b1-177">NuGet sonra yükler ve burada çağrılır bağlı olarak aşağıdaki gibi ayarları uygular:</span><span class="sxs-lookup"><span data-stu-id="b15b1-177">NuGet then loads and applies settings as follows, depending on where it's invoked:</span></span>

- <span data-ttu-id="b15b1-178">**Disk_drive_1/kullanıcılardan çağrılan**: disk_drive_1 üzerinde bulunan yalnızca dosya olduğu için kullanıcı düzeyinde yapılandırma dosyasında (A) listelenen varsayılan depo kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b15b1-178">**Invoked from disk_drive_1/users**: Only the default repository listed in the user-level configuration file (A) is used, because that's the only file found on disk_drive_1.</span></span>

- <span data-ttu-id="b15b1-179">**Disk_drive_2 çağrılan / veya disk_drive_/tmp**: kullanıcı düzeyinde dosya (A) ilk olarak, yüklendikten sonra NuGet disk_drive_2 kök dizinine gider ve bulur dosyası (B).</span><span class="sxs-lookup"><span data-stu-id="b15b1-179">**Invoked from disk_drive_2/ or disk_drive_/tmp**: The user-level file (A) is loaded first, then NuGet goes to the root of disk_drive_2 and finds file (B).</span></span> <span data-ttu-id="b15b1-180">NuGet de tmp yapılandırma dosyasında görünüyor, ancak bir bulmaz.</span><span class="sxs-lookup"><span data-stu-id="b15b1-180">NuGet also looks for a configuration file in /tmp but does not find one.</span></span> <span data-ttu-id="b15b1-181">Sonuç olarak, nuget.org varsayılan havuzda kullanıldığında, paket geri yükleme etkin ve paketleri disk_drive_2/tmp genişletilmiş.</span><span class="sxs-lookup"><span data-stu-id="b15b1-181">As a result, the default repository on nuget.org is used, package restore is enabled, and packages get expanded in disk_drive_2/tmp.</span></span>

- <span data-ttu-id="b15b1-182">**Disk_drive_2/Project1 veya Project1/disk_drive_2/kaynağından çağrılan**: kullanıcı düzeyinde dosya (A) önce yüklenir, ardından NuGet yükleri (B) ve ardından disk_drive_2 kök dosyası (C).</span><span class="sxs-lookup"><span data-stu-id="b15b1-182">**Invoked from disk_drive_2/Project1 or disk_drive_2/Project1/Source**: The user-level file (A) is loaded first, then NuGet loads file (B) from the root of disk_drive_2, followed by file (C).</span></span> <span data-ttu-id="b15b1-183">(C) ayarları geçersiz kılar (B) ve (A), böylece `repositoryPath` disk_drive_2/Project1/dış/paketleri yerine olan paketler yüklendiği *disk_drive_2/tmp*.</span><span class="sxs-lookup"><span data-stu-id="b15b1-183">Settings in (C) override those in (B) and (A), so the `repositoryPath` where packages get installed is disk_drive_2/Project1/External/Packages instead of *disk_drive_2/tmp*.</span></span> <span data-ttu-id="b15b1-184">Ayrıca, (C) temizler çünkü `<packageSources>`, nuget.org yalnızca bırakarak kaynağı olarak kullanılabilir artık `https://MyPrivateRepo/ES/nuget`.</span><span class="sxs-lookup"><span data-stu-id="b15b1-184">Also, because (C) clears `<packageSources>`, nuget.org is no longer available as a source leaving only `https://MyPrivateRepo/ES/nuget`.</span></span>

- <span data-ttu-id="b15b1-185">**Disk_drive_2/Project2 veya Project2/disk_drive_2/kaynağından çağrılan**: kullanıcı düzeyinde dosya (A) ilk dosyası (B) ve tarafından dosyası (D) ve ardından yüklenir.</span><span class="sxs-lookup"><span data-stu-id="b15b1-185">**Invoked from disk_drive_2/Project2 or disk_drive_2/Project2/Source**: The user-level file (A) is loaded first followed by file (B) and file (D).</span></span> <span data-ttu-id="b15b1-186">Çünkü `packageSources` değil işaretli değilse, her ikisi de `nuget.org` ve `https://MyPrivateRepo/DQ/nuget` kaynakları olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b15b1-186">Because `packageSources` is not cleared, both `nuget.org` and `https://MyPrivateRepo/DQ/nuget` are available as sources.</span></span> <span data-ttu-id="b15b1-187">Paketleri disk_drive_2/tmp (B) belirtildiği gibi genişletilmiş.</span><span class="sxs-lookup"><span data-stu-id="b15b1-187">Packages get expanded in disk_drive_2/tmp as specified in (B).</span></span>

## <a name="nuget-defaults-file"></a><span data-ttu-id="b15b1-188">NuGet Varsayılanları dosyası</span><span class="sxs-lookup"><span data-stu-id="b15b1-188">NuGet defaults file</span></span>

<span data-ttu-id="b15b1-189">`NuGetDefaults.Config` Dosyasından içinden paketleri yüklü ve güncelleştirilmiş paket kaynaklarını belirtin ve paketlerle yayımlamak için varsayılan hedef denetlemek için `nuget push`.</span><span class="sxs-lookup"><span data-stu-id="b15b1-189">The `NuGetDefaults.Config` file exists to specify package sources from which packages are installed and updated, and to control the default target for publishing packages with `nuget push`.</span></span> <span data-ttu-id="b15b1-190">Yöneticiler kolaylıkla bakımından (örneğin Grup İlkesi kullanılarak) tutarlı dağıtmak `NuGetDefaults.Config` Geliştirici ve yapı makineleri dosyalara, bir yönetici şunları yapabilir kuruluştaki herkesin nuget.org yerine doğru paket kaynaklarını kullandığını sağlama.</span><span class="sxs-lookup"><span data-stu-id="b15b1-190">Because administrators can conveniently (using Group Policy, for example) deploy consistent `NuGetDefaults.Config` files to developer and build machines, they can ensuring that everyone in the organization is using the correct package sources rather than nuget.org.</span></span>

> [!Important]
> <span data-ttu-id="b15b1-191">`NuGetDefaults.Config` Dosyasının hiçbir zaman bir geliştiricinin NuGet yapılandırmasından kaldırmak bir paket kaynağı neden olur.</span><span class="sxs-lookup"><span data-stu-id="b15b1-191">The `NuGetDefaults.Config` file never causes a package source to be removed from a developer's NuGet configuration.</span></span> <span data-ttu-id="b15b1-192">Geliştirici NuGet zaten kullandı ve bu yüzden nuget.org paket kaynağı varsa, yani kayıtlı oluşturulmasından sonra kaldırılmadan olmaz bir `NuGetDefaults.Config` dosyası.</span><span class="sxs-lookup"><span data-stu-id="b15b1-192">That means if the developer has already used NuGet and therefore has the nuget.org package source registered, it won't be removed after the creation of a `NuGetDefaults.Config` file.</span></span>
>
> <span data-ttu-id="b15b1-193">Ayrıca, hiçbiri `NuGetDefaults.Config` veya başka bir mekanizma NuGet içinde nuget.org gibi paket kaynaklarına erişimi engelleyebilir. Bu tür erişimi engellemek bir kuruluş isterse, bu çok güvenlik duvarları gibi diğer yollarla Bunu yapmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="b15b1-193">Furthermore, neither `NuGetDefaults.Config` nor any other mechanism in NuGet can prevent access to package sources like nuget.org. If an organization wishes to block such access, it much use other means such as firewalls to do so.</span></span>

### <a name="nugetdefaultsconfig-location"></a><span data-ttu-id="b15b1-194">NuGetDefaults.Config konumu</span><span class="sxs-lookup"><span data-stu-id="b15b1-194">NuGetDefaults.Config location</span></span>

<span data-ttu-id="b15b1-195">Windows: % ProgramFiles (x86) %\NuGet\Config (NuGet için NuGet 2.7 3.x: % PROGRAMDATA%\NuGet\NuGetDefaults.Config) Mac/Linux: $XDG_DATA_HOME (genellikle ~/.local/share)</span><span class="sxs-lookup"><span data-stu-id="b15b1-195">Windows: %ProgramFiles(x86)%\NuGet\Config (NuGet 2.7 to NuGet 3.x: %PROGRAMDATA%\NuGet\NuGetDefaults.Config) Mac/Linux: $XDG_DATA_HOME (typically ~/.local/share)</span></span> 

### <a name="nugetdefaultsconfig-settings"></a><span data-ttu-id="b15b1-196">NuGetDefaults.Config ayarları</span><span class="sxs-lookup"><span data-stu-id="b15b1-196">NuGetDefaults.Config settings</span></span>

- <span data-ttu-id="b15b1-197">`packageSources`: Bu koleksiyonun aynı anlamı taşır `packageSources` normal olarak yapılandırma dosyaları ve bunların tercih edilen sırayla varsayılan kaynakları belirtir.</span><span class="sxs-lookup"><span data-stu-id="b15b1-197">`packageSources`: this collection has the same meaning as `packageSources` in regular config files and specifies the default sources in their preferred order.</span></span> <span data-ttu-id="b15b1-198">Bu ayar bulunması durumunda `NuGetDefaults.Config`, NuGet nuget.org varsayılan paket kaynağı olarak kullanmayı desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="b15b1-198">If this setting exists in `NuGetDefaults.Config`, then NuGet doesn't use nuget.org as a default package source.</span></span> <span data-ttu-id="b15b1-199">Bir yönetici, böylece herkes bu dosyayı kullanarak aynı kaynakları ile çalışma ve isterseniz nuget.org kullanarak önler emin olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b15b1-199">An administrator can thus make sure that everyone using this file is working with the same sources and avoids using nuget.org if desired.</span></span>

- <span data-ttu-id="b15b1-200">`disabledPackageSources`: Bu koleksiyonun ayrıca olarak ile aynı anlamı taşır `NuGet.Config` dosyaları, burada her etkilenen kaynak listelenir adını ve belirten bir true/false değerine tarafından devre dışı bırakılıp bırakılmayacağını.</span><span class="sxs-lookup"><span data-stu-id="b15b1-200">`disabledPackageSources`: this collection also has the same meaning as in `NuGet.Config` files, where each affected source is listed by its name and a true/false value indicating whether it's disabled.</span></span> <span data-ttu-id="b15b1-201">Bu kaynak adı ve URL içinde kalmasını sağlar `packageSources` gerek kalmadan, varsayılan olarak açıktır.</span><span class="sxs-lookup"><span data-stu-id="b15b1-201">This allows the source name and URL to remain in `packageSources` without having it turned on by default.</span></span> <span data-ttu-id="b15b1-202">Her bir geliştirici daha sonra tekrar etkinleştirebilirsiniz kaynak false diğer kaynağın değeri ayarlayarak `NuGet.Config` doğru URL'yi yeniden bulmak zorunda kalmadan dosyaları.</span><span class="sxs-lookup"><span data-stu-id="b15b1-202">Individual developers can then re-enable the source by setting the source's value to false in other `NuGet.Config` files without having to find the correct URL again.</span></span> <span data-ttu-id="b15b1-203">Bu da geliştiricilerin iç kaynak URL'lerini varsayılan olarak yalnızca tek bir ekibin kaynağı etkinleştirme sırasında bir kuruluş için tam bir listesi ile sağlamak kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="b15b1-203">This is also useful to supply developers with a full list of internal source URLs for an organization while enabling only an individual team's source by default.</span></span>

- <span data-ttu-id="b15b1-204">`defaultPushSource`: için varsayılan hedef belirtir `nuget push` nuget.org yerleşik varsayılan geçersiz kılma işlemleri. Yöneticiler, yanlışlıkla, ortak nuget.org iç paketleri yayımlama önlemek için bu ayarı dağıtabilir, geliştiriciler özel olarak kullanmak gerek duyduğunuz `nuget push -Source` için nuget.org yayımlamak için.</span><span class="sxs-lookup"><span data-stu-id="b15b1-204">`defaultPushSource`: specifies the default target for `nuget push` operations, overriding the built-in default of nuget.org. Administrators can deploy this setting to avoid publishing internal packages to the public nuget.org by accident, as developers specifically need to use `nuget push -Source` to publish to nuget.org.</span></span>

### <a name="example-nugetdefaultsconfig-and-application"></a><span data-ttu-id="b15b1-205">Örnek NuGetDefaults.Config ve uygulama</span><span class="sxs-lookup"><span data-stu-id="b15b1-205">Example NuGetDefaults.Config and application</span></span>

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
