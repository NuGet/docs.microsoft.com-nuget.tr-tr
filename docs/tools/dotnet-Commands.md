---
title: DotNet CLI NuGet komutları
description: Dotnet komut satırı arabirimi kullanarak NuGet ile ilgili komutları için kısa bir başvuru.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: ff011e60d3de3b0999db56e1e30e97e538bd9fb4
ms.sourcegitcommit: 2a9d149bc6f5ff76b0b657324820bd0429cddeef
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/01/2019
ms.locfileid: "67496473"
---
# <a name="dotnet-cli-commands"></a><span data-ttu-id="b0a7d-103">DotNet CLI komutları</span><span class="sxs-lookup"><span data-stu-id="b0a7d-103">dotnet CLI commands</span></span>

<span data-ttu-id="b0a7d-104">`dotnet` Komut satırı, Windows, Mac OS X ve Linux'ta çalışan, arabirimi (CLI) paketleri yayımlama yükleme ve geri yükleme gibi temel komutlar sağlar.</span><span class="sxs-lookup"><span data-stu-id="b0a7d-104">The `dotnet` command-line interface (CLI), which runs on Windows, Mac OS X, and Linux, provides a number of essential commands such as installing, restoring, and publishing packages.</span></span> <span data-ttu-id="b0a7d-105">DotNet gereksinimlerinizi karşılayıp karşılamadığını kullanmak gerekli değildir `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="b0a7d-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="b0a7d-106">Paketleri kullanmak için şu komutları kullanarak örnekleri için bkz: [yükleyin ve dotnet CLI kullanarak paketleri yönetme](../consume-packages/install-use-packages-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b0a7d-106">For examples of using these commands to consume packages, see [Install and manage packages using the dotnet CLI](../consume-packages/install-use-packages-dotnet-cli.md).</span></span> <span data-ttu-id="b0a7d-107">Paketleri oluşturmak için şu komutları kullanarak örnekleri için bkz: [oluştur ve dotnet CLI kullanarak bir paket yayımlama](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b0a7d-107">For examples of using these commands to create packages, see [Create and publish a package using the dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

<span data-ttu-id="b0a7d-108">Tam komut başvurusu üzerinde için `dotnet` CLI bkz [.NET Core komut satırı arabirimi (CLI) araçlarını](/dotnet/core/tools/?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="b0a7d-108">For the complete command reference on `dotnet` CLI, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="b0a7d-109">Paket tüketim</span><span class="sxs-lookup"><span data-stu-id="b0a7d-109">Package consumption</span></span>

- <span data-ttu-id="b0a7d-110">[**DotNet paketini ekleyin**](/dotnet/core/tools/dotnet-add-package): Proje dosyasına bir paket başvurusu ekler ve ardından çalışan `dotnet restore` paketi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b0a7d-110">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="b0a7d-111">[**DotNet paketi kaldırma**](/dotnet/core/tools/dotnet-remove-package): Paket başvurusu proje dosyasından kaldırır.</span><span class="sxs-lookup"><span data-stu-id="b0a7d-111">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="b0a7d-112">[**DotNet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Bir projenin Araçlar ve bağımlılıkları yükler.</span><span class="sxs-lookup"><span data-stu-id="b0a7d-112">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="b0a7d-113">Bu NuGet 4.0 itibariyle, aynı kodu çalıştıran `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="b0a7d-113">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="b0a7d-114">[**DotNet nuget Yereller**](/dotnet/core/tools/dotnet-nuget-locals): Listeler konumlarını *genel paketleri*, *http önbellek*, ve *temp* klasörleri ve bu klasörlerin içeriğini temizler.</span><span class="sxs-lookup"><span data-stu-id="b0a7d-114">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>
- <span data-ttu-id="b0a7d-115">[**DotNet yeni nugetconfig**](/dotnet/core/tools/dotnet-new): Oluşturur bir [ `nuget.config` ](../reference/nuget-config-file.md) NuGet davranışını yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="b0a7d-115">[**dotnet new nugetconfig**](/dotnet/core/tools/dotnet-new): Creates a [`nuget.config`](../reference/nuget-config-file.md) file to configure NuGet's behavior.</span></span>

## <a name="package-creation"></a><span data-ttu-id="b0a7d-116">Paket oluşturma</span><span class="sxs-lookup"><span data-stu-id="b0a7d-116">Package creation</span></span>

- <span data-ttu-id="b0a7d-117">[**DotNet paketi**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Kod, bir NuGet paketine paketleri.</span><span class="sxs-lookup"><span data-stu-id="b0a7d-117">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span>
- <span data-ttu-id="b0a7d-118">[**DotNet nuget anında iletme**](/dotnet/core/tools/dotnet-nuget-push): Bir paket için bir NuGet sunucusu yayımlar.</span><span class="sxs-lookup"><span data-stu-id="b0a7d-118">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Publishes a package to a NuGet server.</span></span> <span data-ttu-id="b0a7d-119">Nuget.org, Azure yapıları için geçerlidir ve [üçüncü taraf NuGet sunucularını](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="b0a7d-119">Applicable to nuget.org, Azure Artifacts, and [third-party NuGet servers](../hosting-packages/overview.md).</span></span>
- <span data-ttu-id="b0a7d-120">[**DotNet nuget Sil**](/dotnet/core/tools/dotnet-nuget-delete): NuGet sunucusu paketinden unlists veya siler.</span><span class="sxs-lookup"><span data-stu-id="b0a7d-120">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a NuGet server.</span></span> <span data-ttu-id="b0a7d-121">Nuget.org, Azure yapıları için geçerlidir ve [üçüncü taraf NuGet sunucularını](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="b0a7d-121">Applicable to nuget.org, Azure Artifacts, and [third-party NuGet servers](../hosting-packages/overview.md).</span></span>
