---
title: DotNet CLı kullanarak NuGet paketlerini yükleyip yönetme
description: NuGet paketleriyle çalışmak için DotNet CLı kullanma yönergeleri.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: fecf14f0f04d5063f89080b2756f988739c1412c
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859271"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a><span data-ttu-id="d08df-103">DotNet CLı kullanarak paketleri yükleyip yönetme</span><span class="sxs-lookup"><span data-stu-id="d08df-103">Install and manage packages using the dotnet CLI</span></span>

<span data-ttu-id="d08df-104">CLı Aracı, projelerde ve çözümlerde NuGet paketlerini kolayca yüklemenize, kaldırmanıza ve güncelleştirmenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="d08df-104">The CLI tool allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="d08df-105">Windows, Mac OS X ve Linux üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="d08df-105">It runs on Windows, Mac OS X, and Linux.</span></span>

<span data-ttu-id="d08df-106">DotNet CLı, .NET Core ve .NET Standard projesi (SDK stili proje türleri) ve diğer SDK stilindeki projeler (örneğin, .NET Framework hedefleyen SDK stili bir proje) için kullanım içindir.</span><span class="sxs-lookup"><span data-stu-id="d08df-106">The dotnet CLI is for use in your .NET Core and .NET Standard project (SDK-style project types), and for any other SDK-style projects (for example, an SDK-style project that targets .NET Framework).</span></span> <span data-ttu-id="d08df-107">Daha fazla bilgi için bkz. [SDK özniteliği](/dotnet/core/tools/csproj#additions).</span><span class="sxs-lookup"><span data-stu-id="d08df-107">For more information, see [SDK attribute](/dotnet/core/tools/csproj#additions).</span></span>

<span data-ttu-id="d08df-108">Bu makalede, en yaygın DotNet CLı komutlarının birçoğuna ilişkin temel kullanım gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="d08df-108">This article shows you basic usage for a few of the most common dotnet CLI commands.</span></span> <span data-ttu-id="d08df-109">Bu komutların çoğu için, komutta bir proje dosyası belirtilmediği takdirde (proje dosyası isteğe bağlı bir anahtardır) CLı aracı geçerli dizinde proje dosyası arar.</span><span class="sxs-lookup"><span data-stu-id="d08df-109">For most of these commands, the CLI tool looks for a project file in the current directory, unless a project file is specified in the command (the project file is an optional switch).</span></span> <span data-ttu-id="d08df-110">Komutların ve kullanabileceğiniz bağımsız değişkenlerin tam listesi için bkz. [.NET Core komut satırı arabirimi (CLI) araçları](../reference/dotnet-commands.md).</span><span class="sxs-lookup"><span data-stu-id="d08df-110">For a complete list of commands and the arguments you may use, see the [.NET Core command-line interface (CLI) tools](../reference/dotnet-commands.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d08df-111">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="d08df-111">Prerequisites</span></span>

- <span data-ttu-id="d08df-112">[](https://www.microsoft.com/net/download/) `dotnet` Komut satırı aracını sağlayan .NET Core SDK.</span><span class="sxs-lookup"><span data-stu-id="d08df-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="d08df-113">Visual Studio 2017 ' den başlayarak DotNet CLı, .NET Core ile ilgili iş yükleriyle otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="d08df-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="install-a-package"></a><span data-ttu-id="d08df-114">Paketi yükleme</span><span class="sxs-lookup"><span data-stu-id="d08df-114">Install a package</span></span>

<span data-ttu-id="d08df-115">[DotNet Add paketi](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) proje dosyasına bir paket başvurusu ekler ve ardından `dotnet restore` paketi yüklemek için çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="d08df-115">[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>

1. <span data-ttu-id="d08df-116">Bir komut satırı açın ve proje dosyanızı içeren dizine geçiş yapın.</span><span class="sxs-lookup"><span data-stu-id="d08df-116">Open a command line and switch to the directory that contains your project file.</span></span>

2. <span data-ttu-id="d08df-117">Bir NuGet paketini yüklemek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="d08df-117">Use the following command to install a Nuget package:</span></span>

    ```dotnetcli
    dotnet add package <PACKAGE_NAME>
    ```

    <span data-ttu-id="d08df-118">Örneğin, paketini yüklemek için `Newtonsoft.Json` aşağıdaki komutu kullanın</span><span class="sxs-lookup"><span data-stu-id="d08df-118">For example, to install the `Newtonsoft.Json` package, use the following command</span></span>

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

3. <span data-ttu-id="d08df-119">Komut tamamlandıktan sonra, paketin yüklendiğinden emin olmak için proje dosyasına bakın.</span><span class="sxs-lookup"><span data-stu-id="d08df-119">After the command completes, look at the project file to make sure the package was installed.</span></span>

   <span data-ttu-id="d08df-120">`.csproj`Eklenen başvuruyu görmek için dosyayı açabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d08df-120">You can open the `.csproj` file to see the added reference:</span></span>

    ```xml
    <ItemGroup>
      <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
    </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a><span data-ttu-id="d08df-121">Bir paketin belirli bir sürümünü yükler</span><span class="sxs-lookup"><span data-stu-id="d08df-121">Install a specific version of a package</span></span>

<span data-ttu-id="d08df-122">Sürüm belirtilmemişse, NuGet paketin en son sürümünü yüklenir.</span><span class="sxs-lookup"><span data-stu-id="d08df-122">If the version is not specified, NuGet installs the latest version of the package.</span></span> <span data-ttu-id="d08df-123">Ayrıca, bir NuGet paketinin belirli bir sürümünü yüklemek için [DotNet Add Package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) komutunu da kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d08df-123">You can also use the [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) command to install a specific version of a Nuget package:</span></span>

```dotnetcli
dotnet add package <PACKAGE_NAME> --version <VERSION>
```

<span data-ttu-id="d08df-124">Örneğin, paketin sürüm 12.0.1 ' i eklemek için `Newtonsoft.Json` Şu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="d08df-124">For example, to add version 12.0.1 of the `Newtonsoft.Json` package, use this command:</span></span>

```dotnetcli
dotnet add package Newtonsoft.Json --version 12.0.1
```

## <a name="list-package-references"></a><span data-ttu-id="d08df-125">Paket başvurularını Listele</span><span class="sxs-lookup"><span data-stu-id="d08df-125">List package references</span></span>

<span data-ttu-id="d08df-126">[DotNet List Package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) komutunu kullanarak projenizin paket başvurularını listeleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d08df-126">You can list the package references for your project using the [dotnet list package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) command.</span></span>

```dotnetcli
dotnet list package
```

## <a name="remove-a-package"></a><span data-ttu-id="d08df-127">Bir paketi kaldırma</span><span class="sxs-lookup"><span data-stu-id="d08df-127">Remove a package</span></span>

<span data-ttu-id="d08df-128">Proje dosyasından bir paket başvurusunu kaldırmak için [DotNet Remove Package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="d08df-128">Use the [dotnet remove package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) command to remove a package reference from the project file.</span></span>

```dotnetcli
dotnet remove package <PACKAGE_NAME>
```

<span data-ttu-id="d08df-129">Örneğin, paketini kaldırmak için `Newtonsoft.Json` aşağıdaki komutu kullanın</span><span class="sxs-lookup"><span data-stu-id="d08df-129">For example, to remove the `Newtonsoft.Json` package, use the following command</span></span>

```dotnetcli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a><span data-ttu-id="d08df-130">Bir paketi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="d08df-130">Update a package</span></span>

<span data-ttu-id="d08df-131">`dotnet add package`Paket sürümünü (anahtar) belirtmediğiniz takdirde NuGet, komutunu kullandığınızda paketin en son sürümünü yükleme `-v` .</span><span class="sxs-lookup"><span data-stu-id="d08df-131">NuGet installs the latest version of the package when you use the `dotnet add package` command unless you specify the package version (`-v` switch).</span></span>

## <a name="restore-packages"></a><span data-ttu-id="d08df-132">Paketleri geri yükleme</span><span class="sxs-lookup"><span data-stu-id="d08df-132">Restore packages</span></span>

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]
