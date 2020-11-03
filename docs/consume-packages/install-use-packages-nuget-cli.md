---
title: nuget.exe CLı kullanarak NuGet paketlerini yönetme
description: NuGet paketleriyle çalışmak için nuget.exe CLı kullanma yönergeleri.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 7039dd27f2dddebc3c84e5ad35d5efec59547792
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237393"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a><span data-ttu-id="e74f0-103">nuget.exe CLı kullanarak paketleri yönetme</span><span class="sxs-lookup"><span data-stu-id="e74f0-103">Manage packages using the nuget.exe CLI</span></span>

<span data-ttu-id="e74f0-104">CLı Aracı, projelerde ve çözümlerinde NuGet paketlerini kolayca güncelleştirmenize ve geri yüklemenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="e74f0-104">The CLI tool allows you to easily update and restore NuGet packages in projects and solutions.</span></span> <span data-ttu-id="e74f0-105">Bu araç Windows üzerinde tüm NuGet yeteneklerini sağlar ve ayrıca Mono altında çalışırken Mac ve Linux özelliklerinin çoğunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="e74f0-105">This tool provides all NuGet capabilities on Windows, and also provides most features on Mac and Linux when running under Mono.</span></span>

<span data-ttu-id="e74f0-106">`nuget.exe`Clı .NET Framework projeniz ve SDK olmayan bir stil projem (örneğin, .NET Standard kitaplıklarını hedefleyen SDK olmayan bir stil Projesi) içindir.</span><span class="sxs-lookup"><span data-stu-id="e74f0-106">The `nuget.exe` CLI is for your .NET Framework project and non-SDK-style projects (for example, a non-SDK style project that targets .NET Standard libraries).</span></span> <span data-ttu-id="e74f0-107">Öğesine geçirilmiş SDK olmayan bir proje kullanıyorsanız `PackageReference` `dotnet` bunun yerine CLI kullanın.</span><span class="sxs-lookup"><span data-stu-id="e74f0-107">If you are using a non-SDK-style project that has been migrated to `PackageReference`, use the `dotnet` CLI instead.</span></span> <span data-ttu-id="e74f0-108">`nuget.exe`CLI, paket başvuruları için bir [packages.config](../reference/packages-config.md) dosyası gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e74f0-108">The `nuget.exe` CLI requires a [packages.config](../reference/packages-config.md) file for package references.</span></span>

> [!NOTE]
> <span data-ttu-id="e74f0-109">Çoğu senaryoda, PackageReference için kullanılan [SDK olmayan projeler arasında geçiş](../consume-packages/migrate-packages-config-to-package-reference.md) `packages.config` yapmanızı öneririz ve `dotnet` CLI yerine CLI kullanabilirsiniz `nuget.exe` .</span><span class="sxs-lookup"><span data-stu-id="e74f0-109">In most scenarios, we recommend [migrating non-SDK-style projects](../consume-packages/migrate-packages-config-to-package-reference.md) that use `packages.config` to PackageReference, and then you can use the `dotnet` CLI instead of the `nuget.exe` CLI.</span></span> <span data-ttu-id="e74f0-110">Geçiş Şu anda C++ ve ASP.NET projeleri için kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="e74f0-110">Migration is not currently available for C++ and ASP.NET projects.</span></span>

<span data-ttu-id="e74f0-111">Bu makalede, en sık kullanılan CLI komutlarının birçoğuna ilişkin temel kullanım gösterilmektedir `nuget.exe` .</span><span class="sxs-lookup"><span data-stu-id="e74f0-111">This article shows you basic usage for a few of the most common `nuget.exe` CLI commands.</span></span> <span data-ttu-id="e74f0-112">Bu komutların çoğu için, komutta bir proje dosyası belirtilmediği takdirde CLı aracı geçerli dizinde bir proje dosyası arar.</span><span class="sxs-lookup"><span data-stu-id="e74f0-112">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command.</span></span> <span data-ttu-id="e74f0-113">Komutların ve kullanabileceğiniz bağımsız değişkenlerin tamamı listesi için [nuget.exe CLI başvurusuna](../reference/nuget-exe-cli-reference.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="e74f0-113">For a complete list of commands and the arguments you may use, see the [nuget.exe CLI reference](../reference/nuget-exe-cli-reference.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e74f0-114">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="e74f0-114">Prerequisites</span></span>

- <span data-ttu-id="e74f0-115">`nuget.exe` [NuGet.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe)adresinden indirerek, bu `.exe` dosyayı uygun bir klasöre KAYDEDEREK ve bu klasörü PATH ortam değişkeninizden ekleyerek CLI 'yı yükleme.</span><span class="sxs-lookup"><span data-stu-id="e74f0-115">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="e74f0-116">Paketi yükleme</span><span class="sxs-lookup"><span data-stu-id="e74f0-116">Install a package</span></span>

<span data-ttu-id="e74f0-117">[Install](../reference/cli-reference/cli-ref-install.md) komutu, belirtilen paket kaynaklarını kullanarak bir paketi indirir ve geçerli klasörü varsayılan olarak bir projeye yükler.</span><span class="sxs-lookup"><span data-stu-id="e74f0-117">The [install](../reference/cli-reference/cli-ref-install.md) command downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span> <span data-ttu-id="e74f0-118">Yeni paketleri proje kök dizininizde *paketler* klasörüne yükler.</span><span class="sxs-lookup"><span data-stu-id="e74f0-118">Install new packages into the *packages* folder in your project root directory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e74f0-119">`install`Komut bir proje dosyasını veya *packages.config* değiştirmez; buna benzer şekilde, `restore` yalnızca paketleri diske eklemektedir ancak projenin bağımlılıklarını değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="e74f0-119">The `install`command does not modify a project file or *packages.config* ; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="e74f0-120">Bir bağımlılık eklemek için, Visual Studio 'da Paket Yöneticisi Kullanıcı arabirimi veya konsolundan bir paket ekleyin veya *packages.config* değiştirin ve sonra ya da çalıştırın `install` `restore` .</span><span class="sxs-lookup"><span data-stu-id="e74f0-120">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify *packages.config* and then run either `install` or `restore`.</span></span>

1. <span data-ttu-id="e74f0-121">Bir komut satırı açın ve proje dosyanızı içeren dizine geçiş yapın.</span><span class="sxs-lookup"><span data-stu-id="e74f0-121">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="e74f0-122">*Packages* klasörüne bir NuGet paketi yüklemek için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="e74f0-122">Use the following command to install a NuGet package to the *packages* folder.</span></span>

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    <span data-ttu-id="e74f0-123">`Newtonsoft.json`Paketi *paketler* klasörüne yüklemek için şu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="e74f0-123">To install the `Newtonsoft.json` package to the *packages* folder, use the following command:</span></span>

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

<span data-ttu-id="e74f0-124">Alternatif olarak, paketler klasörüne var olan bir dosyayı kullanarak bir NuGet paketini yüklemek için aşağıdaki komutu kullanabilirsiniz `packages.config` . *packages*</span><span class="sxs-lookup"><span data-stu-id="e74f0-124">Alternatively, you can use the following command to install a NuGet package using an existing `packages.config` file to the *packages* folder.</span></span> <span data-ttu-id="e74f0-125">Bu, paketi proje bağımlılıklarınızla eklemez, ancak yerel olarak yüklemez.</span><span class="sxs-lookup"><span data-stu-id="e74f0-125">This does not add the package to your project dependencies, but installs it locally.</span></span>

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="e74f0-126">Bir paketin belirli bir sürümünü yükler</span><span class="sxs-lookup"><span data-stu-id="e74f0-126">Install a specific version of a package</span></span>

<span data-ttu-id="e74f0-127">[Yükleme](../reference/cli-reference/cli-ref-install.md) komutunu kullandığınızda sürüm belirtilmemişse, NuGet paketin en son sürümünü yükler.</span><span class="sxs-lookup"><span data-stu-id="e74f0-127">If the version is not specified when you use the [install](../reference/cli-reference/cli-ref-install.md) command, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="e74f0-128">Ayrıca, bir NuGet paketinin belirli bir sürümünü de yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e74f0-128">You can also install a specific version of a Nuget package:</span></span>

```cli
nuget install <packageID | configFilePath> -Version <version>
```

<span data-ttu-id="e74f0-129">Örneğin, paketin sürüm 12.0.1 ' i eklemek için `Newtonsoft.json` Şu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="e74f0-129">For example, to add version 12.0.1 of the `Newtonsoft.json` package, use this command:</span></span>

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

<span data-ttu-id="e74f0-130">Sınırlamaları ve davranışı hakkında daha fazla bilgi için `install` bkz. [paket yüklemesi](#install-a-package).</span><span class="sxs-lookup"><span data-stu-id="e74f0-130">For more information on the limitations and behavior of `install`, see [Install a package](#install-a-package).</span></span>

## <a name="remove-a-package"></a><span data-ttu-id="e74f0-131">Bir paketi kaldırma</span><span class="sxs-lookup"><span data-stu-id="e74f0-131">Remove a package</span></span>

<span data-ttu-id="e74f0-132">Bir veya daha fazla paketi silmek için, *paketler* klasöründen kaldırmak istediğiniz paketleri silin.</span><span class="sxs-lookup"><span data-stu-id="e74f0-132">To delete one or more packages, delete the packages you want to remove from the *packages* folder.</span></span>

<span data-ttu-id="e74f0-133">Paketleri yeniden yüklemek istiyorsanız `restore` veya `install` komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="e74f0-133">If you want to reinstall packages, use the `restore` or `install` command.</span></span>

## <a name="list-packages"></a><span data-ttu-id="e74f0-134">Paketleri Listele</span><span class="sxs-lookup"><span data-stu-id="e74f0-134">List packages</span></span>

<span data-ttu-id="e74f0-135">[Liste](../reference/cli-reference/cli-ref-list.md) komutunu kullanarak belirli bir kaynaktaki paketlerin listesini görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e74f0-135">You can display a list of packages from a given source using the [list](../reference/cli-reference/cli-ref-list.md) command.</span></span> <span data-ttu-id="e74f0-136">`-Source`Aramayı kısıtlamak için seçeneğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="e74f0-136">Use the `-Source` option to restrict the search.</span></span>

```cli
nuget list -Source <source>
```

<span data-ttu-id="e74f0-137">Örneğin *, paketler klasöründeki paketleri* listeleyin.</span><span class="sxs-lookup"><span data-stu-id="e74f0-137">For example, list packages in the *packages* folder.</span></span>

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

<span data-ttu-id="e74f0-138">Arama terimi kullanırsanız, arama paket, etiket ve paket açıklamalarının adlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="e74f0-138">If you use a search term, the search includes names of packages, tags, and package descriptions.</span></span>

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a><span data-ttu-id="e74f0-139">Tek bir paketi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="e74f0-139">Update an individual package</span></span>

<span data-ttu-id="e74f0-140">Paket sürümünü belirtmediğiniz takdirde NuGet, komutunu kullandığınızda paketin en son sürümünü yüklenir `install` .</span><span class="sxs-lookup"><span data-stu-id="e74f0-140">NuGet installs the latest version of the package when you use the `install` command unless you specify the package version.</span></span>

## <a name="update-all-packages"></a><span data-ttu-id="e74f0-141">Tüm paketleri Güncelleştir</span><span class="sxs-lookup"><span data-stu-id="e74f0-141">Update all packages</span></span>

<span data-ttu-id="e74f0-142">Tüm paketleri güncelleştirmek için [Güncelleştir](../reference/cli-reference/cli-ref-update.md) komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="e74f0-142">Use the [update](../reference/cli-reference/cli-ref-update.md) command to update all packages.</span></span> <span data-ttu-id="e74f0-143">Projedeki tüm paketleri (kullanarak `packages.config` ) en son kullanılabilir sürümlerine güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="e74f0-143">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="e74f0-144">Çalıştırılmadan önce çalıştırılması önerilir `restore` `update` .</span><span class="sxs-lookup"><span data-stu-id="e74f0-144">It is recommended to run `restore` before running `update`.</span></span>

```cli
nuget update
```

## <a name="restore-packages"></a><span data-ttu-id="e74f0-145">Paketleri geri yükleme</span><span class="sxs-lookup"><span data-stu-id="e74f0-145">Restore packages</span></span>

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]

## <a name="get-the-cli-version"></a><span data-ttu-id="e74f0-146">CLı sürümünü al</span><span class="sxs-lookup"><span data-stu-id="e74f0-146">Get the CLI version</span></span>

<span data-ttu-id="e74f0-147">Şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e74f0-147">Use this command:</span></span>

```cli
nuget help
```

<span data-ttu-id="e74f0-148">Yardım çıkışının ilk satırı sürümü gösterir.</span><span class="sxs-lookup"><span data-stu-id="e74f0-148">The first line in the help output shows the version.</span></span> <span data-ttu-id="e74f0-149">Yukarı kaydırmayı önlemek için `nuget help | more` bunun yerine kullanın.</span><span class="sxs-lookup"><span data-stu-id="e74f0-149">To avoid scrolling up, use `nuget help | more` instead.</span></span>