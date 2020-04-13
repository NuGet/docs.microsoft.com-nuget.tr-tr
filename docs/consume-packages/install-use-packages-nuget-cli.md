---
title: Nuget.exe CLI'yi kullanarak NuGet paketlerini yönetin
description: NuGet paketleri ile çalışmak için nuget.exe CLI kullanma talimatları.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 7039dd27f2dddebc3c84e5ad35d5efec59547792
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428690"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a><span data-ttu-id="98828-103">nuget.exe CLI kullanarak paketleri yönetme</span><span class="sxs-lookup"><span data-stu-id="98828-103">Manage packages using the nuget.exe CLI</span></span>

<span data-ttu-id="98828-104">CLI aracı, projelerde ve çözümlerde NuGet paketlerini kolayca güncellemenize ve geri yüklemenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="98828-104">The CLI tool allows you to easily update and restore NuGet packages in projects and solutions.</span></span> <span data-ttu-id="98828-105">Bu araç, Windows'daki tüm NuGet özelliklerini sağlar ve Mono altında çalışırken Mac ve Linux'taki birçok özelliği de sağlar.</span><span class="sxs-lookup"><span data-stu-id="98828-105">This tool provides all NuGet capabilities on Windows, and also provides most features on Mac and Linux when running under Mono.</span></span>

<span data-ttu-id="98828-106">`nuget.exe` CLI, .NET Framework projeniz ve SDK tarzı olmayan projeleriniz içindir (örneğin, .NET Standart kitaplıklarını hedefleyen SDK tarzı olmayan bir proje).</span><span class="sxs-lookup"><span data-stu-id="98828-106">The `nuget.exe` CLI is for your .NET Framework project and non-SDK-style projects (for example, a non-SDK style project that targets .NET Standard libraries).</span></span> <span data-ttu-id="98828-107">Geçiş yapılan SDK tarzı olmayan bir proje `PackageReference`kullanıyorsanız, bunun `dotnet` yerine CLI'yi kullanın.</span><span class="sxs-lookup"><span data-stu-id="98828-107">If you are using a non-SDK-style project that has been migrated to `PackageReference`, use the `dotnet` CLI instead.</span></span> <span data-ttu-id="98828-108">`nuget.exe` CLI, paket başvuruları için bir [packages.config](../reference/packages-config.md) dosyası gerektirir.</span><span class="sxs-lookup"><span data-stu-id="98828-108">The `nuget.exe` CLI requires a [packages.config](../reference/packages-config.md) file for package references.</span></span>

> [!NOTE]
> <span data-ttu-id="98828-109">Çoğu senaryoda, PackageReference için kullanılan `packages.config` [SDK tarzı olmayan projeleri geçirmenizi](../consume-packages/migrate-packages-config-to-package-reference.md) öneririz `dotnet` ve ardından `nuget.exe` CLI yerine CLI'yi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98828-109">In most scenarios, we recommend [migrating non-SDK-style projects](../consume-packages/migrate-packages-config-to-package-reference.md) that use `packages.config` to PackageReference, and then you can use the `dotnet` CLI instead of the `nuget.exe` CLI.</span></span> <span data-ttu-id="98828-110">Geçiş şu anda C++ ve ASP.NET projeleri için kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="98828-110">Migration is not currently available for C++ and ASP.NET projects.</span></span>

<span data-ttu-id="98828-111">Bu makalede, en yaygın `nuget.exe` CLI komutlarından birkaçı için temel kullanım gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="98828-111">This article shows you basic usage for a few of the most common `nuget.exe` CLI commands.</span></span> <span data-ttu-id="98828-112">Bu komutların çoğu nda, komutta bir proje dosyası belirtilmediği sürece CLI aracı geçerli dizinde bir proje dosyası arar.</span><span class="sxs-lookup"><span data-stu-id="98828-112">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command.</span></span> <span data-ttu-id="98828-113">Komutların ve kullanabileceğiniz bağımsız değişkenlerin tam listesi için [nuget.exe CLI başvurusuna](../reference/nuget-exe-cli-reference.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="98828-113">For a complete list of commands and the arguments you may use, see the [nuget.exe CLI reference](../reference/nuget-exe-cli-reference.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="98828-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="98828-114">Prerequisites</span></span>

- <span data-ttu-id="98828-115">CLI'yi `nuget.exe` [nuget.org'dan](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe)indirerek yükleyin, dosyayı `.exe` uygun bir klasöre kaydedin ve bu klasörü PATH ortamı değişkeninize eklediniz.</span><span class="sxs-lookup"><span data-stu-id="98828-115">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="98828-116">Paket yükleme</span><span class="sxs-lookup"><span data-stu-id="98828-116">Install a package</span></span>

<span data-ttu-id="98828-117">[Install](../reference/cli-reference/cli-ref-install.md) komutu, belirtilen paket kaynaklarını kullanarak geçerli klasöre varsayılan olarak bir paketi indirir ve projeye yükler.</span><span class="sxs-lookup"><span data-stu-id="98828-117">The [install](../reference/cli-reference/cli-ref-install.md) command downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span> <span data-ttu-id="98828-118">Proje kök dizininizdeki *paketler* klasörüne yeni paketler yükleyin.</span><span class="sxs-lookup"><span data-stu-id="98828-118">Install new packages into the *packages* folder in your project root directory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="98828-119">Komut, `install`proje dosyasını veya *packages.config'i*değiştirmez; bu şekilde, `restore` yalnızca diske paket eklediği, ancak projenin bağımlılıklarını değiştirmemesi benzer.</span><span class="sxs-lookup"><span data-stu-id="98828-119">The `install`command does not modify a project file or *packages.config*; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="98828-120">Bağımlılık eklemek için Visual Studio'daki Paket Yöneticisi UI veya Console üzerinden paket ekleyin veya *packages.config'i* değiştirin ve sonra ya da `install` `restore`çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="98828-120">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify *packages.config* and then run either `install` or `restore`.</span></span>

1. <span data-ttu-id="98828-121">Bir komut satırı açın ve proje dosyanızı içeren dizine geçin.</span><span class="sxs-lookup"><span data-stu-id="98828-121">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="98828-122">*Paketler* klasörüne bir NuGet paketi yüklemek için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="98828-122">Use the following command to install a NuGet package to the *packages* folder.</span></span>

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    <span data-ttu-id="98828-123">Paketi `Newtonsoft.json` *paketler* klasörüne yüklemek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="98828-123">To install the `Newtonsoft.json` package to the *packages* folder, use the following command:</span></span>

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

<span data-ttu-id="98828-124">Alternatif olarak, `packages.config` *paketler* klasörüne varolan bir dosyayı kullanarak bir NuGet paketi yüklemek için aşağıdaki komutu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98828-124">Alternatively, you can use the following command to install a NuGet package using an existing `packages.config` file to the *packages* folder.</span></span> <span data-ttu-id="98828-125">Bu, paketi proje bağımlılıklarınıza eklemez, ancak yerel olarak yükler.</span><span class="sxs-lookup"><span data-stu-id="98828-125">This does not add the package to your project dependencies, but installs it locally.</span></span>

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="98828-126">Paketin belirli bir sürümünü yükleme</span><span class="sxs-lookup"><span data-stu-id="98828-126">Install a specific version of a package</span></span>

<span data-ttu-id="98828-127">[Yükleme](../reference/cli-reference/cli-ref-install.md) komutunu kullandığınızda sürüm belirtilmemişse, NuGet paketin en son sürümünü yükler.</span><span class="sxs-lookup"><span data-stu-id="98828-127">If the version is not specified when you use the [install](../reference/cli-reference/cli-ref-install.md) command, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="98828-128">Nuget paketinin belirli bir sürümünü de yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="98828-128">You can also install a specific version of a Nuget package:</span></span>

```cli
nuget install <packageID | configFilePath> -Version <version>
```

<span data-ttu-id="98828-129">Örneğin, `Newtonsoft.json` paketin 12.0.1 sürümünü eklemek için şu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="98828-129">For example, to add version 12.0.1 of the `Newtonsoft.json` package, use this command:</span></span>

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

<span data-ttu-id="98828-130">Sınırlamalar ve davranışlar hakkında `install`daha fazla bilgi için [bkz.](#install-a-package)</span><span class="sxs-lookup"><span data-stu-id="98828-130">For more information on the limitations and behavior of `install`, see [Install a package](#install-a-package).</span></span>

## <a name="remove-a-package"></a><span data-ttu-id="98828-131">Paketi kaldırma</span><span class="sxs-lookup"><span data-stu-id="98828-131">Remove a package</span></span>

<span data-ttu-id="98828-132">Bir veya daha fazla paketi silmek *için, paketler* klasöründen kaldırmak istediğiniz paketleri silin.</span><span class="sxs-lookup"><span data-stu-id="98828-132">To delete one or more packages, delete the packages you want to remove from the *packages* folder.</span></span>

<span data-ttu-id="98828-133">Paketleri yeniden yüklemek istiyorsanız, `restore` komutu `install` kullanın.</span><span class="sxs-lookup"><span data-stu-id="98828-133">If you want to reinstall packages, use the `restore` or `install` command.</span></span>

## <a name="list-packages"></a><span data-ttu-id="98828-134">Paketleri listele</span><span class="sxs-lookup"><span data-stu-id="98828-134">List packages</span></span>

<span data-ttu-id="98828-135">[Liste](../reference/cli-reference/cli-ref-list.md) komutunu kullanarak belirli bir kaynaktan gelen paketlerin listesini görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98828-135">You can display a list of packages from a given source using the [list](../reference/cli-reference/cli-ref-list.md) command.</span></span> <span data-ttu-id="98828-136">Aramayı `-Source` kısıtlama seçeneğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="98828-136">Use the `-Source` option to restrict the search.</span></span>

```cli
nuget list -Source <source>
```

<span data-ttu-id="98828-137">Örneğin, *paketleri paketler* klasörüne listeleyin.</span><span class="sxs-lookup"><span data-stu-id="98828-137">For example, list packages in the *packages* folder.</span></span>

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

<span data-ttu-id="98828-138">Arama terimi kullanıyorsanız, arama paketlerin, etiketlerin ve paket açıklamalarının adlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="98828-138">If you use a search term, the search includes names of packages, tags, and package descriptions.</span></span>

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a><span data-ttu-id="98828-139">Tek bir paketi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="98828-139">Update an individual package</span></span>

<span data-ttu-id="98828-140">NuGet, paket sürümünü belirtmediğiniz sürece `install` komutu kullandığınızda paketin en son sürümünü yükler.</span><span class="sxs-lookup"><span data-stu-id="98828-140">NuGet installs the latest version of the package when you use the `install` command unless you specify the package version.</span></span>

## <a name="update-all-packages"></a><span data-ttu-id="98828-141">Tüm paketleri güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="98828-141">Update all packages</span></span>

<span data-ttu-id="98828-142">Tüm paketleri güncelleştirmek için [güncelleştirme](../reference/cli-reference/cli-ref-update.md) komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="98828-142">Use the [update](../reference/cli-reference/cli-ref-update.md) command to update all packages.</span></span> <span data-ttu-id="98828-143">Projedeki (kullanarak) `packages.config`tüm paketleri en son kullanılabilir sürümleriyle güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="98828-143">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="98828-144">Çalıştırmadan önce `restore` çalıştırılması `update`önerilir.</span><span class="sxs-lookup"><span data-stu-id="98828-144">It is recommended to run `restore` before running `update`.</span></span>

```cli
nuget update
```

## <a name="restore-packages"></a><span data-ttu-id="98828-145">Paketleri geri yükleme</span><span class="sxs-lookup"><span data-stu-id="98828-145">Restore packages</span></span>

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]

## <a name="get-the-cli-version"></a><span data-ttu-id="98828-146">CLI sürümünü alın</span><span class="sxs-lookup"><span data-stu-id="98828-146">Get the CLI version</span></span>

<span data-ttu-id="98828-147">Bu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="98828-147">Use this command:</span></span>

```cli
nuget help
```

<span data-ttu-id="98828-148">Yardım çıkışındaki ilk satır sürümü gösterir.</span><span class="sxs-lookup"><span data-stu-id="98828-148">The first line in the help output shows the version.</span></span> <span data-ttu-id="98828-149">Yukarı kaydırmayı önlemek `nuget help | more` için bunun yerine kullanın.</span><span class="sxs-lookup"><span data-stu-id="98828-149">To avoid scrolling up, use `nuget help | more` instead.</span></span>