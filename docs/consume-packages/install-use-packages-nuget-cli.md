---
title: NuGet. exe CLı kullanarak NuGet paketlerini yönetme
description: NuGet paketleri ile çalışmak için NuGet. exe CLı kullanma yönergeleri.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 9eefed6f2c1a362f27c4a5d33d07645d743379fa
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317741"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a><span data-ttu-id="68e39-103">NuGet. exe CLı kullanarak paketleri yönetme</span><span class="sxs-lookup"><span data-stu-id="68e39-103">Manage packages using the nuget.exe CLI</span></span>

<span data-ttu-id="68e39-104">CLı Aracı, projelerde ve çözümlerinde NuGet paketlerini kolayca güncelleştirmenize ve geri yüklemenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="68e39-104">The CLI tool allows you to easily update and restore NuGet packages in projects and solutions.</span></span> <span data-ttu-id="68e39-105">Bu araç Windows üzerinde tüm NuGet yeteneklerini sağlar ve ayrıca Mono altında çalışırken Mac ve Linux özelliklerinin çoğunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="68e39-105">This tool provides all NuGet capabilities on Windows, and also provides most features on Mac and Linux when running under Mono.</span></span>

<span data-ttu-id="68e39-106">`nuget.exe` CLI .NET Framework projeniz ve SDK olmayan bir stil projem (örneğin, .NET Standard kitaplıklarını hedefleyen SDK olmayan bir stil Projesi) içindir.</span><span class="sxs-lookup"><span data-stu-id="68e39-106">The `nuget.exe` CLI is for your .NET Framework project and non-SDK-style projects (for example, a non-SDK style project that targets .NET Standard libraries).</span></span> <span data-ttu-id="68e39-107">Öğesine `PackageReference`geçirilmiş SDK olmayan bir proje kullanıyorsanız bunun yerine `dotnet` CLI kullanın.</span><span class="sxs-lookup"><span data-stu-id="68e39-107">If you are using a non-SDK-style project that has been migrated to `PackageReference`, use the `dotnet` CLI instead.</span></span> <span data-ttu-id="68e39-108">CLI `nuget.exe` , paket başvuruları için bir [Packages. config](../reference/packages-config.md) dosyası gerektirir.</span><span class="sxs-lookup"><span data-stu-id="68e39-108">The `nuget.exe` CLI requires a [packages.config](../reference/packages-config.md) file for package references.</span></span>

> [!NOTE]
> <span data-ttu-id="68e39-109">Çoğu senaryoda, packagereference için kullanılan `packages.config` [SDK olmayan projeler arasında geçiş](../reference/migrate-packages-config-to-package-reference.md) `dotnet` yapmanızı öneririz ve `nuget.exe` CLI yerine CLI kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="68e39-109">In most scenarios, we recommend [migrating non-SDK-style projects](../reference/migrate-packages-config-to-package-reference.md) that use `packages.config` to PackageReference, and then you can use the `dotnet` CLI instead of the `nuget.exe` CLI.</span></span> <span data-ttu-id="68e39-110">Geçiş Şu anda ve ASP.NET projeleri C++ için kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="68e39-110">Migration is not currently available for C++ and ASP.NET projects.</span></span>

<span data-ttu-id="68e39-111">Bu makalede, en sık kullanılan `nuget.exe` CLI komutlarının birçoğuna ilişkin temel kullanım gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="68e39-111">This article shows you basic usage for a few of the most common `nuget.exe` CLI commands.</span></span> <span data-ttu-id="68e39-112">Bu komutların çoğu için, komutta bir proje dosyası belirtilmediği takdirde CLı aracı geçerli dizinde bir proje dosyası arar.</span><span class="sxs-lookup"><span data-stu-id="68e39-112">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command.</span></span> <span data-ttu-id="68e39-113">Komutların ve kullanabileceğiniz bağımsız değişkenlerin tamamı listesi için bkz. [NuGet. exe CLI başvurusu](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="68e39-113">For a complete list of commands and the arguments you may use, see the [nuget.exe CLI reference](../reference/nuget-exe-cli-reference.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68e39-114">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="68e39-114">Prerequisites</span></span>

- <span data-ttu-id="68e39-115">[NuGet.org adresinden](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe)indirerek, bu `.exe` dosyayı uygun bir klasöre kaydederek ve bu klasörü PATH ortam değişkeninizden ekleyerek CLI'yıyükleme.`nuget.exe`</span><span class="sxs-lookup"><span data-stu-id="68e39-115">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="68e39-116">Paket yükler</span><span class="sxs-lookup"><span data-stu-id="68e39-116">Install a package</span></span>

<span data-ttu-id="68e39-117">[Install](../reference/cli-reference/cli-ref-install.md) komutu, belirtilen paket kaynaklarını kullanarak bir paketi indirir ve geçerli klasörü varsayılan olarak bir projeye yükler.</span><span class="sxs-lookup"><span data-stu-id="68e39-117">The [install](../reference/cli-reference/cli-ref-install.md) command downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span> <span data-ttu-id="68e39-118">Yeni paketleri proje kök dizininizde *paketler* klasörüne yükler.</span><span class="sxs-lookup"><span data-stu-id="68e39-118">Install new packages into the *packages* folder in your project root directory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="68e39-119">Komut bir proje dosyasını veya *Packages. config*; bu şekilde, yalnızca paketleri diske eklemesine, ancak projenin bağımlılıklarını `restore` değiştirmediğinden bu şekilde değişiklik yapmaz. `install`</span><span class="sxs-lookup"><span data-stu-id="68e39-119">The `install`command does not modify a project file or *packages.config*; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="68e39-120">Bir bağımlılık eklemek için, Visual Studio 'da Paket Yöneticisi Kullanıcı arabirimi veya konsolundan bir paket ekleyin veya *Packages. config dosyasını* değiştirip ya `install` `restore`da çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="68e39-120">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify *packages.config* and then run either `install` or `restore`.</span></span>

1. <span data-ttu-id="68e39-121">Bir komut satırı açın ve proje dosyanızı içeren dizine geçiş yapın.</span><span class="sxs-lookup"><span data-stu-id="68e39-121">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="68e39-122">*Packages* klasörüne bir NuGet paketi yüklemek için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="68e39-122">Use the following command to install a NuGet package to the *packages* folder.</span></span>

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    <span data-ttu-id="68e39-123">`Newtonsoft.json` Paketi *paketler* klasörüne yüklemek için şu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="68e39-123">To install the `Newtonsoft.json` package to the *packages* folder, use the following command:</span></span>

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

<span data-ttu-id="68e39-124">Alternatif olarak, `packages.config` *paketler* klasörüne var olan bir dosyayı kullanarak bir NuGet paketini yüklemek için aşağıdaki komutu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="68e39-124">Alternatively, you can use the following command to install a NuGet package using an existing `packages.config` file to the *packages* folder.</span></span> <span data-ttu-id="68e39-125">Bu, paketi proje bağımlılıklarınızla eklemez, ancak yerel olarak yüklemez.</span><span class="sxs-lookup"><span data-stu-id="68e39-125">This does not add the package to your project dependencies, but installs it locally.</span></span>

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="68e39-126">Bir paketin belirli bir sürümünü yükler</span><span class="sxs-lookup"><span data-stu-id="68e39-126">Install a specific version of a package</span></span>

<span data-ttu-id="68e39-127">[Yükleme](../reference/cli-reference/cli-ref-install.md) komutunu kullandığınızda sürüm belirtilmemişse, NuGet paketin en son sürümünü yükler.</span><span class="sxs-lookup"><span data-stu-id="68e39-127">If the version is not specified when you use the [install](../reference/cli-reference/cli-ref-install.md) command, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="68e39-128">Ayrıca, bir NuGet paketinin belirli bir sürümünü de yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="68e39-128">You can also install a specific version of a Nuget package:</span></span>

```cli
nuget install <packageID | configFilePath> -Version <version>
```

<span data-ttu-id="68e39-129">Örneğin, `Newtonsoft.json` paketin sürüm 12.0.1 ' i eklemek için şu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="68e39-129">For example, to add version 12.0.1 of the `Newtonsoft.json` package, use this command:</span></span>

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

<span data-ttu-id="68e39-130">Sınırlamaları ve davranışı `install`hakkında daha fazla bilgi için bkz. [paket yüklemesi](#install-a-package).</span><span class="sxs-lookup"><span data-stu-id="68e39-130">For more information on the limitations and behavior of `install`, see [Install a package](#install-a-package).</span></span>

## <a name="remove-a-package"></a><span data-ttu-id="68e39-131">Bir paketi kaldırma</span><span class="sxs-lookup"><span data-stu-id="68e39-131">Remove a package</span></span>

<span data-ttu-id="68e39-132">Bir veya daha fazla paketi silmek için, *paketler* klasöründen kaldırmak istediğiniz paketleri silin.</span><span class="sxs-lookup"><span data-stu-id="68e39-132">To delete one or more packages, delete the packages you want to remove from the *packages* folder.</span></span>

<span data-ttu-id="68e39-133">Paketleri yeniden yüklemek istiyorsanız `restore` veya `install` komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="68e39-133">If you want to reinstall packages, use the `restore` or `install` command.</span></span>

## <a name="list-packages"></a><span data-ttu-id="68e39-134">Paketleri Listele</span><span class="sxs-lookup"><span data-stu-id="68e39-134">List packages</span></span>

<span data-ttu-id="68e39-135">[Liste](../reference/cli-reference/cli-ref-list.md) komutunu kullanarak belirli bir kaynaktaki paketlerin listesini görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="68e39-135">You can display a list of packages from a given source using the [list](../reference/cli-reference/cli-ref-list.md) command.</span></span> <span data-ttu-id="68e39-136">Aramayı kısıtlamak için seçeneğini kullanın. `-Source`</span><span class="sxs-lookup"><span data-stu-id="68e39-136">Use the `-Source` option to restrict the search.</span></span>

```cli
nuget list -Source <source>
```

<span data-ttu-id="68e39-137">Örneğin, *paketler klasöründeki paketleri* listeleyin.</span><span class="sxs-lookup"><span data-stu-id="68e39-137">For example, list packages in the *packages* folder.</span></span>

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

<span data-ttu-id="68e39-138">Arama terimi kullanırsanız, arama paket, etiket ve paket açıklamalarının adlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="68e39-138">If you use a search term, the search includes names of packages, tags, and package descriptions.</span></span>

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a><span data-ttu-id="68e39-139">Tek bir paketi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="68e39-139">Update an individual package</span></span>

<span data-ttu-id="68e39-140">Paket sürümünü belirtmediğiniz takdirde NuGet, `install` komutunu kullandığınızda paketin en son sürümünü yüklenir.</span><span class="sxs-lookup"><span data-stu-id="68e39-140">NuGet installs the latest version of the package when you use the `install` command unless you specify the package version.</span></span>

## <a name="update-all-packages"></a><span data-ttu-id="68e39-141">Tüm paketleri Güncelleştir</span><span class="sxs-lookup"><span data-stu-id="68e39-141">Update all packages</span></span>

<span data-ttu-id="68e39-142">Tüm paketleri güncelleştirmek için [Güncelleştir](../reference/cli-reference/cli-ref-update.md) komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="68e39-142">Use the [update](../reference/cli-reference/cli-ref-update.md) command to update all packages.</span></span> <span data-ttu-id="68e39-143">Projedeki tüm paketleri (kullanarak `packages.config`) en son kullanılabilir sürümlerine güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="68e39-143">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="68e39-144">`restore` Çalıştırılmadan`update`önce çalıştırılması önerilir.</span><span class="sxs-lookup"><span data-stu-id="68e39-144">It is recommended to run `restore` before running `update`.</span></span>

```cli
nuget update
```

## <a name="restore-packages"></a><span data-ttu-id="68e39-145">Paketleri geri yükle</span><span class="sxs-lookup"><span data-stu-id="68e39-145">Restore packages</span></span>

<span data-ttu-id="68e39-146">*Paketler* klasöründe eksik olan paketleri indiren ve yükleyen [restore](../reference/cli-reference/cli-ref-restore.md) komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="68e39-146">Use the [restore](../reference/cli-reference/cli-ref-restore.md) command, which downloads and installs any packages missing from the *packages* folder.</span></span>

<span data-ttu-id="68e39-147">`restore`yalnızca paketleri diske ekler ancak projenin bağımlılıklarını değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="68e39-147">`restore` only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="68e39-148">Proje bağımlılıklarını geri yüklemek için, `packages.config`öğesini değiştirin, sonra `restore` komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="68e39-148">To restore project dependencies, modify `packages.config`, then use the `restore` command.</span></span>

<span data-ttu-id="68e39-149">Diğer `nuget.exe` CLI komutlarında olduğu gibi, önce bir komut satırını açın ve proje dosyanızı içeren dizine geçiş yapın.</span><span class="sxs-lookup"><span data-stu-id="68e39-149">As with the other `nuget.exe` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="68e39-150">Paketini kullanarak `restore`geri yüklemek için:</span><span class="sxs-lookup"><span data-stu-id="68e39-150">To restore a package using `restore`:</span></span>

```cli
nuget restore MySolution.sln
```