---
title: Dotnet CLI'yi kullanarak NuGet paketlerini yükleyin ve yönetin
description: NuGet paketleri ile çalışmak için dotnet CLI kullanma talimatları.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 67cca81c48970c7f2e2cf0a64ee5ba57704a31e2
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "74825167"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a><span data-ttu-id="17b8e-103">Dotnet CLI kullanarak paketleri yükleme ve yönetme</span><span class="sxs-lookup"><span data-stu-id="17b8e-103">Install and manage packages using the dotnet CLI</span></span>

<span data-ttu-id="17b8e-104">CLI aracı, projelerde ve çözümlerde NuGet paketlerini kolayca yüklemenize, kaldırmanıza ve güncellemenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="17b8e-104">The CLI tool allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="17b8e-105">Windows, Mac OS X ve Linux'ta çalışır.</span><span class="sxs-lookup"><span data-stu-id="17b8e-105">It runs on Windows, Mac OS X, and Linux.</span></span>

<span data-ttu-id="17b8e-106">Dotnet CLI, .NET Core ve .NET Standard projenizde (SDK tarzı proje türleri) ve diğer SDK tarzı projelerde (örneğin, .NET Framework'ü hedefleyen SDK tarzı bir proje) kullanım içindir.</span><span class="sxs-lookup"><span data-stu-id="17b8e-106">The dotnet CLI is for use in your .NET Core and .NET Standard project (SDK-style project types), and for any other SDK-style projects (for example, an SDK-style project that targets .NET Framework).</span></span> <span data-ttu-id="17b8e-107">Daha fazla bilgi için Bkz. [SDK özniteliği.](/dotnet/core/tools/csproj#additions)</span><span class="sxs-lookup"><span data-stu-id="17b8e-107">For more information, see [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span>

<span data-ttu-id="17b8e-108">Bu makalede, en yaygın nokta CLI komutlarından birkaçı için temel kullanım gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="17b8e-108">This article shows you basic usage for a few of the most common dotnet CLI commands.</span></span> <span data-ttu-id="17b8e-109">Bu komutların çoğunda CLI aracı, komutta bir proje dosyası belirtilmedikçe (proje dosyası isteğe bağlı bir anahtardır) geçerli dizinde bir proje dosyası arar.</span><span class="sxs-lookup"><span data-stu-id="17b8e-109">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command (the project file is an optional switch).</span></span> <span data-ttu-id="17b8e-110">Komutların ve kullanabileceğiniz bağımsız değişkenlerin tam listesi için [.NET Core komut satırı arabirimi (CLI) araçlarına](../reference/dotnet-commands.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="17b8e-110">For a complete list of commands and the arguments you may use, see the [.NET Core command-line interface (CLI) tools](../reference/dotnet-commands.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="17b8e-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="17b8e-111">Prerequisites</span></span>

- <span data-ttu-id="17b8e-112">Komut satırı aracını `dotnet` sağlayan [.NET Core SDK.](https://www.microsoft.com/net/download/)</span><span class="sxs-lookup"><span data-stu-id="17b8e-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="17b8e-113">Visual Studio 2017'den itibaren dotnet CLI,.NET Core ile ilgili iş yükleriyle otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="17b8e-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="17b8e-114">Paket yükleme</span><span class="sxs-lookup"><span data-stu-id="17b8e-114">Install a package</span></span>

<span data-ttu-id="17b8e-115">[dotnet ekle paketi](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) proje dosyasına bir paket `dotnet restore` başvurusu ekler, sonra paketi yüklemek için çalışır.</span><span class="sxs-lookup"><span data-stu-id="17b8e-115">[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>

1. <span data-ttu-id="17b8e-116">Bir komut satırı açın ve proje dosyanızı içeren dizine geçin.</span><span class="sxs-lookup"><span data-stu-id="17b8e-116">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="17b8e-117">Nuget paketi yüklemek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="17b8e-117">Use the following command to install a Nuget package:</span></span>

    ```dotnetcli
    dotnet add package <PACKAGE_NAME>
    ```

    <span data-ttu-id="17b8e-118">Örneğin, `Newtonsoft.Json` paketi yüklemek için aşağıdaki komutu kullanın</span><span class="sxs-lookup"><span data-stu-id="17b8e-118">For example, to install the `Newtonsoft.Json` package, use the following command</span></span>

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

3. <span data-ttu-id="17b8e-119">Komut tamamlandıktan sonra, paketin yüklü olduğundan emin olmak için proje dosyasına bakın.</span><span class="sxs-lookup"><span data-stu-id="17b8e-119">After the command completes, look at the project file to make sure the package was installed.</span></span>

   <span data-ttu-id="17b8e-120">Eklenen başvuruyu `.csproj` görmek için dosyayı açabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="17b8e-120">You can open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="17b8e-121">Paketin belirli bir sürümünü yükleme</span><span class="sxs-lookup"><span data-stu-id="17b8e-121">Install a specific version of a package</span></span>

<span data-ttu-id="17b8e-122">Sürüm belirtilmemişse, NuGet paketin en son sürümünü yükler.</span><span class="sxs-lookup"><span data-stu-id="17b8e-122">If the version is not specified, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="17b8e-123">Nuget paketinin belirli bir sürümünü yüklemek için [dotnet ekle paket](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) komutunu da kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="17b8e-123">You can also use the [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) command to install a specific version of a Nuget package:</span></span>

```dotnetcli
dotnet add package <PACKAGE_NAME> -v <VERSION>
```

<span data-ttu-id="17b8e-124">Örneğin, `Newtonsoft.Json` paketin 12.0.1 sürümünü eklemek için şu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="17b8e-124">For example, to add version 12.0.1 of the `Newtonsoft.Json` package, use this command:</span></span>

```dotnetcli
dotnet add package Newtonsoft.Json -v 12.0.1
```

## <a name="list-package-references"></a><span data-ttu-id="17b8e-125">Paket referanslarını listele</span><span class="sxs-lookup"><span data-stu-id="17b8e-125">List package references</span></span>

<span data-ttu-id="17b8e-126">Projenizin paket başvurularını [dotnet listesi paket](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) komutunu kullanarak listeleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="17b8e-126">You can list the package references for your project using the [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) command.</span></span>

```dotnetcli
dotnet list package
```

## <a name="remove-a-package"></a><span data-ttu-id="17b8e-127">Paketi kaldırma</span><span class="sxs-lookup"><span data-stu-id="17b8e-127">Remove a package</span></span>

<span data-ttu-id="17b8e-128">Proje dosyasından paket başvurusu kaldırmak için [dotnet kaldır paket](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="17b8e-128">Use the [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) command to remove a package reference from the project file.</span></span>

```dotnetcli
dotnet remove package <PACKAGE_NAME>
```

<span data-ttu-id="17b8e-129">Örneğin, `Newtonsoft.Json` paketi kaldırmak için aşağıdaki komutu kullanın</span><span class="sxs-lookup"><span data-stu-id="17b8e-129">For example, to remove the `Newtonsoft.Json` package, use the following command</span></span>

```dotnetcli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a><span data-ttu-id="17b8e-130">Paketi güncelleştir</span><span class="sxs-lookup"><span data-stu-id="17b8e-130">Update a package</span></span>

<span data-ttu-id="17b8e-131">NuGet, paket sürümünü (anahtar) `dotnet add package` `-v` belirtmediğiniz sürece komutu kullandığınızda paketin en son sürümünü yükler.</span><span class="sxs-lookup"><span data-stu-id="17b8e-131">NuGet installs the latest version of the package when you use the `dotnet add package` command unless you specify the package version (`-v` switch).</span></span>

## <a name="restore-packages"></a><span data-ttu-id="17b8e-132">Paketleri geri yükleme</span><span class="sxs-lookup"><span data-stu-id="17b8e-132">Restore packages</span></span>

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]
