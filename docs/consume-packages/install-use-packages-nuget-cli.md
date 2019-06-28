---
title: Nuget.exe CLI kullanarak NuGet paketlerini Yönet
description: Nuget.exe CLI NuGet paketleri ile çalışmak için kullanma yönergeleri.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: e60bca8fe2f80b044e466db2a100d6c6d167edb7
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427631"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a><span data-ttu-id="ca339-103">Nuget.exe CLI kullanarak paketleri yönetme</span><span class="sxs-lookup"><span data-stu-id="ca339-103">Manage packages using the nuget.exe CLI</span></span>

<span data-ttu-id="ca339-104">CLI aracı kolayca güncelleştirmek ve projelerde ve çözümlerde NuGet paketlerini geri yüklemenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="ca339-104">The CLI tool allows you to easily update and restore NuGet packages in projects and solutions.</span></span> <span data-ttu-id="ca339-105">Bu araç tüm NuGet özellikleri Windows üzerinde sağlar ve ayrıca özelliklerinin çoğu Mac ve Linux üzerinde Mono altında çalışırken sağlar.</span><span class="sxs-lookup"><span data-stu-id="ca339-105">This tool provides all NuGet capabilities on Windows, and also provides most features on Mac and Linux when running under Mono.</span></span>

<span data-ttu-id="ca339-106">Nuget.exe CLI, .NET Framework projesi ve SDK stili projeleri (örneğin, bir .NET standart kitaplıkları hedefleyen) içindir.</span><span class="sxs-lookup"><span data-stu-id="ca339-106">The nuget.exe CLI is for your .NET Framework project and non-SDK-style projects (for example, one that targets .NET Standard libraries).</span></span> <span data-ttu-id="ca339-107">İçin geçirilmiş olan bir SDK stili projesi kullanıyorsanız `PackageReference`, bunun yerine ' % s'dotnet CLI kullanın.</span><span class="sxs-lookup"><span data-stu-id="ca339-107">If you are using a non-SDK-style project that has been migrated to `PackageReference`, use the dotnet CLI instead.</span></span> <span data-ttu-id="ca339-108">NuGet CLI gerektiren bir [packages.config](../reference/packages-config.md) paket başvuruları için dosya.</span><span class="sxs-lookup"><span data-stu-id="ca339-108">The NuGet CLI requires a [packages.config](../reference/packages-config.md) file for package references.</span></span>

> [!NOTE]
> <span data-ttu-id="ca339-109">Çoğu senaryoda öneririz [SDK stili projeleri geçirme](../reference/migrate-packages-config-to-package-reference.md) kullanan `packages.config` PackageReference için ve ardından dotnet CLI kullanabileceğiniz yerine `nuget.exe` CLI.</span><span class="sxs-lookup"><span data-stu-id="ca339-109">In most scenarios, we recommend [migrating non-SDK-style projects](../reference/migrate-packages-config-to-package-reference.md) that use `packages.config` to PackageReference, and then you can use the dotnet CLI instead of the `nuget.exe` CLI.</span></span> <span data-ttu-id="ca339-110">Geçiş, C++ ve ASP.NET projeleri için şu anda kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="ca339-110">Migration is not currently available for C++ and ASP.NET projects.</span></span>

<span data-ttu-id="ca339-111">Bu makalede en yaygın nuget.exe CLI komutlarına birkaç temel kullanımını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ca339-111">This article shows you basic usage for a few of the most common nuget.exe CLI commands.</span></span> <span data-ttu-id="ca339-112">Bir proje dosyası komutta belirtilmediği sürece bu komutların çoğu için CLI aracı bir proje dosyasını geçerli dizinde arar.</span><span class="sxs-lookup"><span data-stu-id="ca339-112">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command.</span></span> <span data-ttu-id="ca339-113">Komut ve bağımsız değişkenler kullanabilirsiniz tam listesi için bkz: [nuget.exe CLI başvurusu](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="ca339-113">For a complete list of commands and the arguments you may use, see the [nuget.exe CLI reference](../tools/nuget-exe-cli-reference.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ca339-114">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="ca339-114">Prerequisites</span></span>

- <span data-ttu-id="ca339-115">Yükleme `nuget.exe` ondan indirerek CLI [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), kaydetme `.exe` uygun bir klasöre dosya ve klasörün PATH ortam değişkeninize ekleme.</span><span class="sxs-lookup"><span data-stu-id="ca339-115">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="ca339-116">Paket yükleme</span><span class="sxs-lookup"><span data-stu-id="ca339-116">Install a package</span></span>

<span data-ttu-id="ca339-117">[Yükleme](../tools/cli-ref-install.md) komut indirir ve belirtilen paket kaynaklarını kullanan geçerli klasöre varsayarak, bir projeye bir paketi yükler.</span><span class="sxs-lookup"><span data-stu-id="ca339-117">The [install](../tools/cli-ref-install.md) command downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span> <span data-ttu-id="ca339-118">Yeni paketler halinde yükleme *paketleri* klasöründe proje kök dizini.</span><span class="sxs-lookup"><span data-stu-id="ca339-118">Install new packages into the *packages* folder in your project root directory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ca339-119">`install`Komutu, bir proje dosyası değiştirmez veya *packages.config*; benzer şekilde, bu şekilde `restore` yalnızca diske paketleri ekler ancak bir proje bağımlılıklarınızı değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="ca339-119">The `install`command does not modify a project file or *packages.config*; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="ca339-120">Bir bağımlılık eklemek için Visual Studio'da Paket Yöneticisi kullanıcı Arabirimi veya konsol üzerinden paket ekleme veya değiştirme *packages.config* ve ya da çalıştırın `install` veya `restore`.</span><span class="sxs-lookup"><span data-stu-id="ca339-120">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify *packages.config* and then run either `install` or `restore`.</span></span>

1. <span data-ttu-id="ca339-121">Bir komut satırı açın ve proje dosyanızı içeren dizine geçin.</span><span class="sxs-lookup"><span data-stu-id="ca339-121">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="ca339-122">Bir NuGet paketini yüklemek için aşağıdaki komutu kullanın *paketleri* klasör.</span><span class="sxs-lookup"><span data-stu-id="ca339-122">Use the following command to install a NuGet package to the *packages* folder.</span></span>

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    <span data-ttu-id="ca339-123">Yüklenecek `Newtonsoft.json` paketini *paketleri* klasörüne aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="ca339-123">To install the `Newtonsoft.json` package to the *packages* folder, use the following command:</span></span>

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

<span data-ttu-id="ca339-124">Alternatif olarak, var olan bir bir NuGet paketini yüklemek için aşağıdaki komutu kullanabilirsiniz `packages.config` dosyasını *paketleri* klasör.</span><span class="sxs-lookup"><span data-stu-id="ca339-124">Alternatively, you can use the following command to install a NuGet package using an existing `packages.config` file to the *packages* folder.</span></span> <span data-ttu-id="ca339-125">Bu paket proje bağımlılıklarınızı eklemez, ancak yerel olarak yükler.</span><span class="sxs-lookup"><span data-stu-id="ca339-125">This does not add the package to your project dependencies, but installs it locally.</span></span>

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="ca339-126">Bir paketi belirli bir sürümünü yükleme</span><span class="sxs-lookup"><span data-stu-id="ca339-126">Install a specific version of a package</span></span>

<span data-ttu-id="ca339-127">Kullandığınız sürüm belirtilmezse [yükleme](../tools/cli-ref-install.md) komutu, NuGet paketinin en son sürümünü yükler.</span><span class="sxs-lookup"><span data-stu-id="ca339-127">If the version is not specified when you use the [install](../tools/cli-ref-install.md) command, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="ca339-128">Bir Nuget paketi belirli bir sürümünü de yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ca339-128">You can also install a specific version of a Nuget package:</span></span>

```cli
nuget install <packageID | configFilePath> -Version <version>
```

<span data-ttu-id="ca339-129">Örneğin, 12.0.1 sürümünü eklemek için `Newtonsoft.json` paketi, bu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="ca339-129">For example, to add version 12.0.1 of the `Newtonsoft.json` package, use this command:</span></span>

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

<span data-ttu-id="ca339-130">Sınırlamalar ve davranışı hakkında daha fazla bilgi için `install`, bkz: [paket yükleme](#install-a-package).</span><span class="sxs-lookup"><span data-stu-id="ca339-130">For more information on the limitations and behavior of `install`, see [Install a package](#install-a-package).</span></span>

## <a name="remove-a-package"></a><span data-ttu-id="ca339-131">Paket kaldırma</span><span class="sxs-lookup"><span data-stu-id="ca339-131">Remove a package</span></span>

<span data-ttu-id="ca339-132">Bir veya daha fazla paket silmek için kaldırmak istediğiniz paketleri silmek *paketleri* klasör.</span><span class="sxs-lookup"><span data-stu-id="ca339-132">To delete one or more packages, delete the packages you want to remove from the *packages* folder.</span></span>

<span data-ttu-id="ca339-133">Paketleri yeniden yüklemek istiyorsanız, kullanın `restore` veya `install` komutu.</span><span class="sxs-lookup"><span data-stu-id="ca339-133">If you want to reinstall packages, use the `restore` or `install` command.</span></span>

## <a name="list-packages"></a><span data-ttu-id="ca339-134">Liste paketleri</span><span class="sxs-lookup"><span data-stu-id="ca339-134">List packages</span></span>

<span data-ttu-id="ca339-135">Kullanarak belirtilen kaynak paketlerinin listesini görüntüleyebileceğiniz [listesi](../tools/cli-ref-list.md) komutu.</span><span class="sxs-lookup"><span data-stu-id="ca339-135">You can display a list of packages from a given source using the [list](../tools/cli-ref-list.md) command.</span></span> <span data-ttu-id="ca339-136">Kullanım `-Source` arama kısıtlamak için seçeneği.</span><span class="sxs-lookup"><span data-stu-id="ca339-136">Use the `-Source` option to restrict the search.</span></span>

```cli
nuget list -Source <source>
```

<span data-ttu-id="ca339-137">Örneğin, paketleri listesi *paketleri* klasör.</span><span class="sxs-lookup"><span data-stu-id="ca339-137">For example, list packages in the *packages* folder.</span></span>

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

<span data-ttu-id="ca339-138">Bir arama terimi kullanırsanız, arama, paketler, etiketler ve paket açıklamaları adlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="ca339-138">If you use a search term, the search includes names of packages, tags, and package descriptions.</span></span>

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a><span data-ttu-id="ca339-139">Tek bir paket güncelleştirmesi</span><span class="sxs-lookup"><span data-stu-id="ca339-139">Update an individual package</span></span>

<span data-ttu-id="ca339-140">NuGet paketinin en son sürümünü yükler kullandığınızda `install` Paket sürümü belirtmediğiniz sürece komutu.</span><span class="sxs-lookup"><span data-stu-id="ca339-140">NuGet installs the latest version of the package when you use the `install` command unless you specify the package version.</span></span>

## <a name="update-all-packages"></a><span data-ttu-id="ca339-141">Tüm paketleri güncelleştir</span><span class="sxs-lookup"><span data-stu-id="ca339-141">Update all packages</span></span>

<span data-ttu-id="ca339-142">Kullanım [güncelleştirme](../tools/cli-ref-update.md) tüm paketleri Güncelleştir komutu.</span><span class="sxs-lookup"><span data-stu-id="ca339-142">Use the [update](../tools/cli-ref-update.md) command to update all packages.</span></span> <span data-ttu-id="ca339-143">Güncelleştirmeleri bir projedeki tüm paketleri (kullanarak `packages.config`), en son kullanılabilir sürümler için.</span><span class="sxs-lookup"><span data-stu-id="ca339-143">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="ca339-144">Çalıştırmak için önerilen `restore` çalıştırmadan önce `update`.</span><span class="sxs-lookup"><span data-stu-id="ca339-144">It is recommended to run `restore` before running `update`.</span></span>

```cli
nuget update
```

## <a name="restore-packages"></a><span data-ttu-id="ca339-145">Paketleri geri yükle</span><span class="sxs-lookup"><span data-stu-id="ca339-145">Restore packages</span></span>

<span data-ttu-id="ca339-146">Kullanım [geri](../tools/cli-ref-restore.md) indirir ve yükler gelen eksik herhangi bir paket komutu *paketleri* klasör.</span><span class="sxs-lookup"><span data-stu-id="ca339-146">Use the [restore](../tools/cli-ref-restore.md) command, which downloads and installs any packages missing from the *packages* folder.</span></span>

<span data-ttu-id="ca339-147">`restore` Yalnızca disk paketleri ekler, ancak bir proje bağımlılıklarınızı değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="ca339-147">`restore` only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="ca339-148">Proje bağımlılıkları geri yüklemek için değiştirme `packages.config`, ardından `restore` komutu.</span><span class="sxs-lookup"><span data-stu-id="ca339-148">To restore project dependencies, modify `packages.config`, then use the `restore` command.</span></span>

<span data-ttu-id="ca339-149">Bir paketi kullanarak geri yüklemek için `restore`:</span><span class="sxs-lookup"><span data-stu-id="ca339-149">To restore a package using `restore`:</span></span>

```cli
nuget restore MySolution.sln
```