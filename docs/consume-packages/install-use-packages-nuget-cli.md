---
title: NuGet. exe CLı kullanarak NuGet paketlerini yönetme
description: NuGet paketleri ile çalışmak için NuGet. exe CLı kullanma yönergeleri.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 7039dd27f2dddebc3c84e5ad35d5efec59547792
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428690"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a><span data-ttu-id="7e792-103">NuGet. exe CLı kullanarak paketleri yönetme</span><span class="sxs-lookup"><span data-stu-id="7e792-103">Manage packages using the nuget.exe CLI</span></span>

<span data-ttu-id="7e792-104">CLı Aracı, projelerde ve çözümlerinde NuGet paketlerini kolayca güncelleştirmenize ve geri yüklemenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="7e792-104">The CLI tool allows you to easily update and restore NuGet packages in projects and solutions.</span></span> <span data-ttu-id="7e792-105">Bu araç Windows üzerinde tüm NuGet yeteneklerini sağlar ve ayrıca Mono altında çalışırken Mac ve Linux özelliklerinin çoğunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="7e792-105">This tool provides all NuGet capabilities on Windows, and also provides most features on Mac and Linux when running under Mono.</span></span>

<span data-ttu-id="7e792-106">`nuget.exe` CLı, .NET Framework projeniz ve SDK olmayan bir stil projesi (örneğin, .NET Standard kitaplıklarını hedefleyen SDK olmayan bir stil Projesi) içindir.</span><span class="sxs-lookup"><span data-stu-id="7e792-106">The `nuget.exe` CLI is for your .NET Framework project and non-SDK-style projects (for example, a non-SDK style project that targets .NET Standard libraries).</span></span> <span data-ttu-id="7e792-107">`PackageReference`'e geçirilmiş SDK olmayan bir proje kullanıyorsanız bunun yerine `dotnet` CLı kullanın.</span><span class="sxs-lookup"><span data-stu-id="7e792-107">If you are using a non-SDK-style project that has been migrated to `PackageReference`, use the `dotnet` CLI instead.</span></span> <span data-ttu-id="7e792-108">`nuget.exe` CLı, paket başvuruları için bir [Packages. config](../reference/packages-config.md) dosyası gerektirir.</span><span class="sxs-lookup"><span data-stu-id="7e792-108">The `nuget.exe` CLI requires a [packages.config](../reference/packages-config.md) file for package references.</span></span>

> [!NOTE]
> <span data-ttu-id="7e792-109">Çoğu senaryoda, `packages.config` kullanan [SDK olmayan projelerin](../consume-packages/migrate-packages-config-to-package-reference.md) packagereference 'a geçirilmesini öneririz ve sonra `nuget.exe` clı yerıne `dotnet` CLI kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e792-109">In most scenarios, we recommend [migrating non-SDK-style projects](../consume-packages/migrate-packages-config-to-package-reference.md) that use `packages.config` to PackageReference, and then you can use the `dotnet` CLI instead of the `nuget.exe` CLI.</span></span> <span data-ttu-id="7e792-110">Geçiş Şu anda ve ASP.NET projeleri C++ için kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="7e792-110">Migration is not currently available for C++ and ASP.NET projects.</span></span>

<span data-ttu-id="7e792-111">Bu makale, en sık kullanılan `nuget.exe` CLı komutlarının bir bölümünü temel olarak gösterir.</span><span class="sxs-lookup"><span data-stu-id="7e792-111">This article shows you basic usage for a few of the most common `nuget.exe` CLI commands.</span></span> <span data-ttu-id="7e792-112">Bu komutların çoğu için, komutta bir proje dosyası belirtilmediği takdirde CLı aracı geçerli dizinde bir proje dosyası arar.</span><span class="sxs-lookup"><span data-stu-id="7e792-112">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command.</span></span> <span data-ttu-id="7e792-113">Komutların ve kullanabileceğiniz bağımsız değişkenlerin tamamı listesi için bkz. [NuGet. exe CLI başvurusu](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="7e792-113">For a complete list of commands and the arguments you may use, see the [nuget.exe CLI reference](../reference/nuget-exe-cli-reference.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e792-114">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="7e792-114">Prerequisites</span></span>

- <span data-ttu-id="7e792-115">[NuGet.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe)adresinden INDIREREK `nuget.exe` CLI yükleme, bu `.exe` dosyayı uygun bir klasöre kaydetme ve bu klasörü PATH ortam değişkeninizden ekleme.</span><span class="sxs-lookup"><span data-stu-id="7e792-115">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="7e792-116">Paket yükler</span><span class="sxs-lookup"><span data-stu-id="7e792-116">Install a package</span></span>

<span data-ttu-id="7e792-117">[Install](../reference/cli-reference/cli-ref-install.md) komutu, belirtilen paket kaynaklarını kullanarak bir paketi indirir ve geçerli klasörü varsayılan olarak bir projeye yükler.</span><span class="sxs-lookup"><span data-stu-id="7e792-117">The [install](../reference/cli-reference/cli-ref-install.md) command downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span> <span data-ttu-id="7e792-118">Yeni paketleri proje kök dizininizde *paketler* klasörüne yükler.</span><span class="sxs-lookup"><span data-stu-id="7e792-118">Install new packages into the *packages* folder in your project root directory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7e792-119">`install`komutu bir proje dosyası veya *Packages. config*dosyasını değiştirmez; Bu şekilde, yalnızca paketleri diske eklemesi, ancak projenin bağımlılıklarını değiştirmediğinden `restore` benzerdir.</span><span class="sxs-lookup"><span data-stu-id="7e792-119">The `install`command does not modify a project file or *packages.config*; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="7e792-120">Bir bağımlılık eklemek için, Visual Studio 'da Paket Yöneticisi Kullanıcı arabirimi veya konsolundan bir paket ekleyin veya *Packages. config dosyasını* değiştirip `install` ya da `restore`çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7e792-120">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify *packages.config* and then run either `install` or `restore`.</span></span>

1. <span data-ttu-id="7e792-121">Bir komut satırı açın ve proje dosyanızı içeren dizine geçiş yapın.</span><span class="sxs-lookup"><span data-stu-id="7e792-121">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="7e792-122">*Packages* klasörüne bir NuGet paketi yüklemek için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="7e792-122">Use the following command to install a NuGet package to the *packages* folder.</span></span>

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    <span data-ttu-id="7e792-123">*Paketler* klasörüne `Newtonsoft.json` paketini yüklemek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="7e792-123">To install the `Newtonsoft.json` package to the *packages* folder, use the following command:</span></span>

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

<span data-ttu-id="7e792-124">Alternatif olarak, *paketler* klasörüne mevcut bir `packages.config` dosyasını kullanarak bir NuGet paketini yüklemek için aşağıdaki komutu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e792-124">Alternatively, you can use the following command to install a NuGet package using an existing `packages.config` file to the *packages* folder.</span></span> <span data-ttu-id="7e792-125">Bu, paketi proje bağımlılıklarınızla eklemez, ancak yerel olarak yüklemez.</span><span class="sxs-lookup"><span data-stu-id="7e792-125">This does not add the package to your project dependencies, but installs it locally.</span></span>

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="7e792-126">Bir paketin belirli bir sürümünü yükler</span><span class="sxs-lookup"><span data-stu-id="7e792-126">Install a specific version of a package</span></span>

<span data-ttu-id="7e792-127">[Yükleme](../reference/cli-reference/cli-ref-install.md) komutunu kullandığınızda sürüm belirtilmemişse, NuGet paketin en son sürümünü yükler.</span><span class="sxs-lookup"><span data-stu-id="7e792-127">If the version is not specified when you use the [install](../reference/cli-reference/cli-ref-install.md) command, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="7e792-128">Ayrıca, bir NuGet paketinin belirli bir sürümünü de yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7e792-128">You can also install a specific version of a Nuget package:</span></span>

```cli
nuget install <packageID | configFilePath> -Version <version>
```

<span data-ttu-id="7e792-129">Örneğin, `Newtonsoft.json` paketinin 12.0.1 sürümünü eklemek için şu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="7e792-129">For example, to add version 12.0.1 of the `Newtonsoft.json` package, use this command:</span></span>

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

<span data-ttu-id="7e792-130">`install`kısıtlamaları ve davranışı hakkında daha fazla bilgi için bkz. [paket yüklemesi](#install-a-package).</span><span class="sxs-lookup"><span data-stu-id="7e792-130">For more information on the limitations and behavior of `install`, see [Install a package](#install-a-package).</span></span>

## <a name="remove-a-package"></a><span data-ttu-id="7e792-131">Bir paketi kaldırma</span><span class="sxs-lookup"><span data-stu-id="7e792-131">Remove a package</span></span>

<span data-ttu-id="7e792-132">Bir veya daha fazla paketi silmek için, *paketler* klasöründen kaldırmak istediğiniz paketleri silin.</span><span class="sxs-lookup"><span data-stu-id="7e792-132">To delete one or more packages, delete the packages you want to remove from the *packages* folder.</span></span>

<span data-ttu-id="7e792-133">Paketleri yeniden yüklemek istiyorsanız `restore` veya `install` komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="7e792-133">If you want to reinstall packages, use the `restore` or `install` command.</span></span>

## <a name="list-packages"></a><span data-ttu-id="7e792-134">Paketleri Listele</span><span class="sxs-lookup"><span data-stu-id="7e792-134">List packages</span></span>

<span data-ttu-id="7e792-135">[Liste](../reference/cli-reference/cli-ref-list.md) komutunu kullanarak belirli bir kaynaktaki paketlerin listesini görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e792-135">You can display a list of packages from a given source using the [list](../reference/cli-reference/cli-ref-list.md) command.</span></span> <span data-ttu-id="7e792-136">Aramayı kısıtlamak için `-Source` seçeneğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="7e792-136">Use the `-Source` option to restrict the search.</span></span>

```cli
nuget list -Source <source>
```

<span data-ttu-id="7e792-137">Örneğin *, paketler klasöründeki paketleri* listeleyin.</span><span class="sxs-lookup"><span data-stu-id="7e792-137">For example, list packages in the *packages* folder.</span></span>

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

<span data-ttu-id="7e792-138">Arama terimi kullanırsanız, arama paket, etiket ve paket açıklamalarının adlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="7e792-138">If you use a search term, the search includes names of packages, tags, and package descriptions.</span></span>

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a><span data-ttu-id="7e792-139">Tek bir paketi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="7e792-139">Update an individual package</span></span>

<span data-ttu-id="7e792-140">Paket sürümünü belirtmediğiniz takdirde NuGet, `install` komutunu kullandığınızda paketin en son sürümünü yüklenir.</span><span class="sxs-lookup"><span data-stu-id="7e792-140">NuGet installs the latest version of the package when you use the `install` command unless you specify the package version.</span></span>

## <a name="update-all-packages"></a><span data-ttu-id="7e792-141">Tüm paketleri Güncelleştir</span><span class="sxs-lookup"><span data-stu-id="7e792-141">Update all packages</span></span>

<span data-ttu-id="7e792-142">Tüm paketleri güncelleştirmek için [Güncelleştir](../reference/cli-reference/cli-ref-update.md) komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="7e792-142">Use the [update](../reference/cli-reference/cli-ref-update.md) command to update all packages.</span></span> <span data-ttu-id="7e792-143">Projedeki tüm paketleri (`packages.config`kullanarak) en son kullanılabilir sürümlerine güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="7e792-143">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="7e792-144">`update`çalıştırılmadan önce `restore` çalıştırılması önerilir.</span><span class="sxs-lookup"><span data-stu-id="7e792-144">It is recommended to run `restore` before running `update`.</span></span>

```cli
nuget update
```

## <a name="restore-packages"></a><span data-ttu-id="7e792-145">Paketleri geri yükle</span><span class="sxs-lookup"><span data-stu-id="7e792-145">Restore packages</span></span>

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]

## <a name="get-the-cli-version"></a><span data-ttu-id="7e792-146">CLı sürümünü al</span><span class="sxs-lookup"><span data-stu-id="7e792-146">Get the CLI version</span></span>

<span data-ttu-id="7e792-147">Şu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="7e792-147">Use this command:</span></span>

```cli
nuget help
```

<span data-ttu-id="7e792-148">Yardım çıkışının ilk satırı sürümü gösterir.</span><span class="sxs-lookup"><span data-stu-id="7e792-148">The first line in the help output shows the version.</span></span> <span data-ttu-id="7e792-149">Yukarı kaydırmaktan kaçınmak için, bunun yerine `nuget help | more` kullanın.</span><span class="sxs-lookup"><span data-stu-id="7e792-149">To avoid scrolling up, use `nuget help | more` instead.</span></span>