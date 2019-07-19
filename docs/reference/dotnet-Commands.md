---
title: DotNet CLı NuGet komutları
description: DotNet komut satırı arabirimini kullanan NuGet ile ilgili komutlar için kısa bir başvuru.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: ff011e60d3de3b0999db56e1e30e97e538bd9fb4
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328251"
---
# <a name="dotnet-cli-commands"></a><span data-ttu-id="464c3-103">DotNet CLı komutları</span><span class="sxs-lookup"><span data-stu-id="464c3-103">dotnet CLI commands</span></span>

<span data-ttu-id="464c3-104">Windows, Mac OS X ve Linux üzerinde çalışan komutsatırıarabirimi(CLI),paketyükleme,geriyüklemeveyayımlamagibibirtakımönemlikomutlarısağlar.`dotnet`</span><span class="sxs-lookup"><span data-stu-id="464c3-104">The `dotnet` command-line interface (CLI), which runs on Windows, Mac OS X, and Linux, provides a number of essential commands such as installing, restoring, and publishing packages.</span></span> <span data-ttu-id="464c3-105">DotNet gereksinimlerinize uygunsa, kullanılması `nuget.exe`gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="464c3-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="464c3-106">Paketleri kullanmak için bu komutları kullanma örnekleri için bkz. [DotNet CLI kullanarak paketleri yüklemek ve yönetmek](../consume-packages/install-use-packages-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="464c3-106">For examples of using these commands to consume packages, see [Install and manage packages using the dotnet CLI](../consume-packages/install-use-packages-dotnet-cli.md).</span></span> <span data-ttu-id="464c3-107">Paketler oluşturmak için bu komutları kullanma örnekleri için bkz. [DotNet CLI kullanarak paket oluşturma ve yayımlama](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="464c3-107">For examples of using these commands to create packages, see [Create and publish a package using the dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

<span data-ttu-id="464c3-108">CLI 'daki `dotnet` tam komut başvurusu için bkz. [.NET Core komut satırı arabirimi (CLI) araçları](/dotnet/core/tools/?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="464c3-108">For the complete command reference on `dotnet` CLI, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="464c3-109">Paket tüketimi</span><span class="sxs-lookup"><span data-stu-id="464c3-109">Package consumption</span></span>

- <span data-ttu-id="464c3-110">[**DotNet Add paketi**](/dotnet/core/tools/dotnet-add-package): Proje dosyasına bir paket başvurusu ekler ve sonra paketi yüklemek için `dotnet restore` çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="464c3-110">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="464c3-111">[**DotNet kaldırma paketi**](/dotnet/core/tools/dotnet-remove-package): Proje dosyasından bir paket başvurusunu kaldırır.</span><span class="sxs-lookup"><span data-stu-id="464c3-111">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="464c3-112">[**DotNet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Bir projenin bağımlılıklarını ve araçlarını geri yükler.</span><span class="sxs-lookup"><span data-stu-id="464c3-112">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="464c3-113">NuGet 4,0 itibariyle bu, ile `nuget restore`aynı kodu çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="464c3-113">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="464c3-114">[**DotNet NuGet Yereller**](/dotnet/core/tools/dotnet-nuget-locals): *Genel paketler*, *http önbelleği*ve *geçici* klasörlerin konumlarını listeler ve bu klasörlerin içeriğini temizler.</span><span class="sxs-lookup"><span data-stu-id="464c3-114">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>
- <span data-ttu-id="464c3-115">[**DotNet yeni nugetconfig**](/dotnet/core/tools/dotnet-new): NuGet davranışını [`nuget.config`](../reference/nuget-config-file.md) yapılandırmak için bir dosya oluşturur.</span><span class="sxs-lookup"><span data-stu-id="464c3-115">[**dotnet new nugetconfig**](/dotnet/core/tools/dotnet-new): Creates a [`nuget.config`](../reference/nuget-config-file.md) file to configure NuGet's behavior.</span></span>

## <a name="package-creation"></a><span data-ttu-id="464c3-116">Paket oluşturma</span><span class="sxs-lookup"><span data-stu-id="464c3-116">Package creation</span></span>

- <span data-ttu-id="464c3-117">[**DotNet paketi**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Kodu bir NuGet paketine paketler.</span><span class="sxs-lookup"><span data-stu-id="464c3-117">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span>
- <span data-ttu-id="464c3-118">[**DotNet NuGet Push**](/dotnet/core/tools/dotnet-nuget-push): Bir NuGet sunucusuna paket yayımlar.</span><span class="sxs-lookup"><span data-stu-id="464c3-118">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Publishes a package to a NuGet server.</span></span> <span data-ttu-id="464c3-119">Nuget.org, Azure Artifacts ve [üçüncü taraf NuGet sunucuları](../hosting-packages/overview.md)için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="464c3-119">Applicable to nuget.org, Azure Artifacts, and [third-party NuGet servers](../hosting-packages/overview.md).</span></span>
- <span data-ttu-id="464c3-120">[**DotNet NuGet silme**](/dotnet/core/tools/dotnet-nuget-delete): NuGet sunucusundan bir paketi siler veya listesini kaldırır.</span><span class="sxs-lookup"><span data-stu-id="464c3-120">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a NuGet server.</span></span> <span data-ttu-id="464c3-121">Nuget.org, Azure Artifacts ve [üçüncü taraf NuGet sunucuları](../hosting-packages/overview.md)için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="464c3-121">Applicable to nuget.org, Azure Artifacts, and [third-party NuGet servers](../hosting-packages/overview.md).</span></span>
