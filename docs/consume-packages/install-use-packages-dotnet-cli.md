---
title: Yükleme ve dotnet CLI kullanarak NuGet paketlerini Yönet
description: NuGet paketleri ile çalışmak için dotnet CLI kullanma yönergeleri.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 64f3a1978cd336064a77c9f3872357e65c37fc10
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842353"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a><span data-ttu-id="24720-103">Yükleme ve dotnet CLI kullanarak paketleri yönetme</span><span class="sxs-lookup"><span data-stu-id="24720-103">Install and manage packages using the dotnet CLI</span></span>

<span data-ttu-id="24720-104">CLI aracı, kolayca yükleme, kaldırma ve projelerde ve çözümlerde NuGet paketlerini güncelleştirme olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="24720-104">The CLI tool allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="24720-105">İşlem, Windows, Mac OS X ve Linux üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="24720-105">It runs on Windows, Mac OS X, and Linux.</span></span>

<span data-ttu-id="24720-106">Dotnet CLI projenizde .NET Core ve .NET Standard (SDK stilinde proje türleri) için ve tüm diğer SDK stili projeleri (örneğin, .NET Framework hedefleyen bir SDK stilinde Proje) içindir.</span><span class="sxs-lookup"><span data-stu-id="24720-106">The dotnet CLI is for use in your .NET Core and .NET Standard project (SDK-style project types), and for any other SDK-style projects (for example, an SDK-style project that targets .NET Framework).</span></span> <span data-ttu-id="24720-107">Daha fazla bilgi için [SDK özniteliği](/dotnet/core/tools/csproj#additions).</span><span class="sxs-lookup"><span data-stu-id="24720-107">For more information, see [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span>

<span data-ttu-id="24720-108">Bu makalede en yaygın dotnet CLI komutları birkaç temel kullanımını gösterir.</span><span class="sxs-lookup"><span data-stu-id="24720-108">This article shows you basic usage for a few of the most common dotnet CLI commands.</span></span> <span data-ttu-id="24720-109">Bir proje dosyası (isteğe bağlı bir anahtar proje dosyasıdır) komutta belirtilmediği sürece bu komutların çoğu için CLI aracı bir proje dosyasını geçerli dizinde arar.</span><span class="sxs-lookup"><span data-stu-id="24720-109">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command (the project file is an optional switch).</span></span> <span data-ttu-id="24720-110">Komut ve bağımsız değişkenler kullanabilirsiniz tam listesi için bkz: [.NET Core komut satırı arabirimi (CLI) araçlarını](../tools/dotnet-commands.md).</span><span class="sxs-lookup"><span data-stu-id="24720-110">For a complete list of commands and the arguments you may use, see the [.NET Core command-line interface (CLI) tools](../tools/dotnet-commands.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24720-111">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="24720-111">Prerequisites</span></span>

- <span data-ttu-id="24720-112">[.NET Core SDK'sı](https://www.microsoft.com/net/download/), sağlayan `dotnet` komut satırı aracı.</span><span class="sxs-lookup"><span data-stu-id="24720-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="24720-113">Dotnet CLI herhangi bir .NET Core ile otomatik olarak yüklenir, Visual Studio 2017'de başlayarak, iş yüklerini ilgili.</span><span class="sxs-lookup"><span data-stu-id="24720-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="24720-114">Paket yükleme</span><span class="sxs-lookup"><span data-stu-id="24720-114">Install a package</span></span>

<span data-ttu-id="24720-115">[DotNet paketini ekleyin](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) proje dosyasına bir paket başvurusu ekler ve ardından çalışan `dotnet restore` paketi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="24720-115">[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>

1. <span data-ttu-id="24720-116">Bir komut satırı açın ve proje dosyanızı içeren dizine geçin.</span><span class="sxs-lookup"><span data-stu-id="24720-116">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="24720-117">Bir Nuget paketini yüklemek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="24720-117">Use the following command to install a Nuget package:</span></span>

    ```cli
    dotnet add package <PACKAGE_NAME>
    ```

    <span data-ttu-id="24720-118">Örneğin, yükleme için `Newtonsoft.Json` paket, aşağıdaki komutu kullanın</span><span class="sxs-lookup"><span data-stu-id="24720-118">For example, to install the `Newtonsoft.Json` package, use the following command</span></span>

    ```cli
    dotnet add package Newtonsoft.Json
    ```

3. <span data-ttu-id="24720-119">Komut tamamlandıktan sonra paket emin olmak için proje dosyasını göz yüklendi.</span><span class="sxs-lookup"><span data-stu-id="24720-119">After the command completes, look at the project file to make sure the package was installed.</span></span>

   <span data-ttu-id="24720-120">Açabileceğiniz `.csproj` dosya eklendi başvuru görmek için:</span><span class="sxs-lookup"><span data-stu-id="24720-120">You can open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="24720-121">Bir paketi belirli bir sürümünü yükleme</span><span class="sxs-lookup"><span data-stu-id="24720-121">Install a specific version of a package</span></span>

<span data-ttu-id="24720-122">Sürüm belirtilmezse, NuGet paketinin en son sürümünü yükler.</span><span class="sxs-lookup"><span data-stu-id="24720-122">If the version is not specified, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="24720-123">Ayrıca [dotnet paketini ekleyin](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) bir Nuget paketi belirli bir sürümünü yüklemek için komutu:</span><span class="sxs-lookup"><span data-stu-id="24720-123">You can also use the [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) command to install a specific version of a Nuget package:</span></span>

```cli
dotnet add package <PACKAGE_NAME> -v <VERSION>
```

<span data-ttu-id="24720-124">Örneğin, 12.0.1 sürümünü eklemek için `Newtonsoft.Json` paketi, bu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="24720-124">For example, to add version 12.0.1 of the `Newtonsoft.Json` package, use this command:</span></span>

```cli
dotnet add package Newtonsoft.Json -v 12.0.1
```

## <a name="list-package-references"></a><span data-ttu-id="24720-125">Liste paket başvuruları</span><span class="sxs-lookup"><span data-stu-id="24720-125">List package references</span></span>

<span data-ttu-id="24720-126">Paket başvuruları için kullanarak projenize listeleyebilirsiniz [dotnet paket listeleme](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) komutu.</span><span class="sxs-lookup"><span data-stu-id="24720-126">You can list the package references for your project using the [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) command.</span></span>

```cli
dotnet list package
```

## <a name="remove-a-package"></a><span data-ttu-id="24720-127">Paket kaldırma</span><span class="sxs-lookup"><span data-stu-id="24720-127">Remove a package</span></span>

<span data-ttu-id="24720-128">Kullanım [dotnet paketi kaldırma](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) proje dosyasından bir paket başvurusu kaldırmak için komutu.</span><span class="sxs-lookup"><span data-stu-id="24720-128">Use the [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) command to remove a package reference from the project file.</span></span>

```cli
dotnet remove package <PACKAGE_NAME>
```

<span data-ttu-id="24720-129">Örneğin, kaldırmak için `Newtonsoft.Json` paket, aşağıdaki komutu kullanın</span><span class="sxs-lookup"><span data-stu-id="24720-129">For example, to remove the `Newtonsoft.Json` package, use the following command</span></span>

```cli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a><span data-ttu-id="24720-130">Güncelleştirme paketi</span><span class="sxs-lookup"><span data-stu-id="24720-130">Update a package</span></span>

<span data-ttu-id="24720-131">NuGet paketinin en son sürümünü yükler kullandığınızda `dotnet add package` Paket sürümü belirtmediğiniz sürece komutu (`-v` geçiş).</span><span class="sxs-lookup"><span data-stu-id="24720-131">NuGet installs the latest version of the package when you use the `dotnet add package` command unless you specify the package version (`-v` switch).</span></span>

## <a name="restore-packages"></a><span data-ttu-id="24720-132">Paketleri geri yükle</span><span class="sxs-lookup"><span data-stu-id="24720-132">Restore packages</span></span>

<span data-ttu-id="24720-133">Kullanım [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) komutu, proje dosyasında listelenen paketleri geri yükler (bkz [PackageReference](../consume-packages/package-references-in-project-files.md)).</span><span class="sxs-lookup"><span data-stu-id="24720-133">Use the [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) command, which restores packages listed in the project file (see [PackageReference](../consume-packages/package-references-in-project-files.md)).</span></span> <span data-ttu-id="24720-134">.NET Core 2.0 ve daha sonra geri yükleme ile otomatik olarak gerçekleştirilir `dotnet build` ve `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="24720-134">With .NET Core 2.0 and later, restore is done automatically with `dotnet build` and `dotnet run`.</span></span> <span data-ttu-id="24720-135">Bu NuGet 4.0 itibariyle, aynı kodu çalıştıran `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="24720-135">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>

<span data-ttu-id="24720-136">Olan diğer `dotnet` CLI komutları, ilk olarak bir komut satırı açın ve proje dosyanızı içeren dizine geçin.</span><span class="sxs-lookup"><span data-stu-id="24720-136">As with the other `dotnet` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="24720-137">Bir paketi kullanarak geri yüklemek için `dotnet restore`:</span><span class="sxs-lookup"><span data-stu-id="24720-137">To restore a package using `dotnet restore`:</span></span>

```cli
dotnet restore 
```
