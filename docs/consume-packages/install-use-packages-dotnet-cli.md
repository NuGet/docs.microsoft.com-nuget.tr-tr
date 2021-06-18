---
title: dotnet CLI kullanarak NuGet paketlerini yükleme ve yönetme
description: NuGet paketleriyle çalışmak için dotnet CLI kullanma yönergeleri.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 62c05aad388c25120d5b9f5143017a2f4f3b276b
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323615"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a><span data-ttu-id="aa365-103">dotnet CLI kullanarak paketleri yükleme ve yönetme</span><span class="sxs-lookup"><span data-stu-id="aa365-103">Install and manage packages using the dotnet CLI</span></span>

<span data-ttu-id="aa365-104">CLI aracı, projelerde ve çözümlerde NuGet paketlerini kolayca yüklemenizi, kaldırmanızı ve güncelleştirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="aa365-104">The CLI tool allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="aa365-105">Windows, Mac OS X ve Linux üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="aa365-105">It runs on Windows, Mac OS X, and Linux.</span></span>

<span data-ttu-id="aa365-106">dotnet CLI, .NET Core ve .NET Standard projesinde (SDK stili proje türleri) ve diğer SDK stili projeler (örneğin, .NET Framework'i hedef alan SDK stilinde bir proje) için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="aa365-106">The dotnet CLI is for use in your .NET Core and .NET Standard project (SDK-style project types), and for any other SDK-style projects (for example, an SDK-style project that targets .NET Framework).</span></span> <span data-ttu-id="aa365-107">Daha fazla bilgi için bkz. [SDK özniteliği.](/dotnet/core/tools/csproj#additions)</span><span class="sxs-lookup"><span data-stu-id="aa365-107">For more information, see [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span>

<span data-ttu-id="aa365-108">Bu makalede, en yaygın dotnet CLI komutlarından birkaçı için temel kullanım bilgileri velanmıştır.</span><span class="sxs-lookup"><span data-stu-id="aa365-108">This article shows you basic usage for a few of the most common dotnet CLI commands.</span></span> <span data-ttu-id="aa365-109">Bu komutların çoğunda, komutta bir proje dosyası belirtilmemişse (proje dosyası isteğe bağlı bir anahtardır) CLI aracı geçerli dizinde bir proje dosyası olarak görünür.</span><span class="sxs-lookup"><span data-stu-id="aa365-109">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command (the project file is an optional switch).</span></span> <span data-ttu-id="aa365-110">Kullanabileceğiniz komutların ve bağımsız değişkenlerin tam listesi için bkz. [.NET Core komut satırı arabirimi (CLI) araçları.](../reference/dotnet-commands.md)</span><span class="sxs-lookup"><span data-stu-id="aa365-110">For a complete list of commands and the arguments you may use, see the [.NET Core command-line interface (CLI) tools](../reference/dotnet-commands.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa365-111">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="aa365-111">Prerequisites</span></span>

- <span data-ttu-id="aa365-112">Komut [.NET Core SDK](https://www.microsoft.com/net/download/)sağlayan komut `dotnet` satırı aracı.</span><span class="sxs-lookup"><span data-stu-id="aa365-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="aa365-113">2017'Visual Studio itibaren dotnet CLI, .NET Core ile ilgili tüm iş yükleriyle otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="aa365-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="aa365-114">Paketi yükleme</span><span class="sxs-lookup"><span data-stu-id="aa365-114">Install a package</span></span>

<span data-ttu-id="aa365-115">[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) proje dosyasına bir paket başvurusu ekler, sonra paketi `dotnet restore` yüklemek için çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="aa365-115">[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>

1. <span data-ttu-id="aa365-116">Bir komut satırı açın ve proje dosyanızı içeren dizine geçiş.</span><span class="sxs-lookup"><span data-stu-id="aa365-116">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="aa365-117">NuGet paketini yüklemek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="aa365-117">Use the following command to install a NuGet package:</span></span>

    ```dotnetcli
    dotnet add package <PACKAGE_NAME>
    ```

    <span data-ttu-id="aa365-118">Örneğin, paketi yüklemek `Newtonsoft.Json` için aşağıdaki komutu kullanın</span><span class="sxs-lookup"><span data-stu-id="aa365-118">For example, to install the `Newtonsoft.Json` package, use the following command</span></span>

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

3. <span data-ttu-id="aa365-119">Komut tamamlandıktan sonra, paketin yüklü olduğundan emin olmak için proje dosyasına bakın.</span><span class="sxs-lookup"><span data-stu-id="aa365-119">After the command completes, look at the project file to make sure the package was installed.</span></span>

   <span data-ttu-id="aa365-120">Eklenen başvuruya `.csproj` görmek için dosyayı açabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="aa365-120">You can open the `.csproj` file to see the added reference:</span></span>

    ```xml
    <ItemGroup>
      <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
    </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="aa365-121">Paketin belirli bir sürümünü yükleme</span><span class="sxs-lookup"><span data-stu-id="aa365-121">Install a specific version of a package</span></span>

<span data-ttu-id="aa365-122">Sürüm belirtilmezse NuGet paketin en son sürümünü yüklür.</span><span class="sxs-lookup"><span data-stu-id="aa365-122">If the version is not specified, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="aa365-123">Bir NuGet paketinin belirli bir sürümünü yüklemek için [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) komutunu da kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="aa365-123">You can also use the [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) command to install a specific version of a NuGet package:</span></span>

```dotnetcli
dotnet add package <PACKAGE_NAME> --version <VERSION>
```

<span data-ttu-id="aa365-124">Örneğin, paketin 12.0.1 sürümünü eklemek `Newtonsoft.Json` için şu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="aa365-124">For example, to add version 12.0.1 of the `Newtonsoft.Json` package, use this command:</span></span>

```dotnetcli
dotnet add package Newtonsoft.Json --version 12.0.1
```

## <a name="list-package-references"></a><span data-ttu-id="aa365-125">Paket başvurularını listele</span><span class="sxs-lookup"><span data-stu-id="aa365-125">List package references</span></span>

<span data-ttu-id="aa365-126">dotnet list package komutunu kullanarak projenizin paket [başvurularını listeebilirsiniz.](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x)</span><span class="sxs-lookup"><span data-stu-id="aa365-126">You can list the package references for your project using the [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) command.</span></span>

```dotnetcli
dotnet list package
```

## <a name="remove-a-package"></a><span data-ttu-id="aa365-127">Paketi kaldırma</span><span class="sxs-lookup"><span data-stu-id="aa365-127">Remove a package</span></span>

<span data-ttu-id="aa365-128">Proje [dosyasından paket başvurularını](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) kaldırmak için dotnet remove package komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="aa365-128">Use the [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) command to remove a package reference from the project file.</span></span>

```dotnetcli
dotnet remove package <PACKAGE_NAME>
```

<span data-ttu-id="aa365-129">Örneğin, paketi kaldırmak `Newtonsoft.Json` için aşağıdaki komutu kullanın</span><span class="sxs-lookup"><span data-stu-id="aa365-129">For example, to remove the `Newtonsoft.Json` package, use the following command</span></span>

```dotnetcli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a><span data-ttu-id="aa365-130">Paketi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="aa365-130">Update a package</span></span>

<span data-ttu-id="aa365-131">NuGet, komutunu kullanarak paket sürümünü ( `dotnet add package` anahtarı) belirtmedikçe paketin en son sürümünü `-v` yüklür.</span><span class="sxs-lookup"><span data-stu-id="aa365-131">NuGet installs the latest version of the package when you use the `dotnet add package` command unless you specify the package version (`-v` switch).</span></span>

## <a name="restore-packages"></a><span data-ttu-id="aa365-132">Paketleri geri yükleme</span><span class="sxs-lookup"><span data-stu-id="aa365-132">Restore packages</span></span>

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]
