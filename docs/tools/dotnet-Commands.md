---
title: DotNet CLI NuGet komutları
description: Dotnet komut satırı arabirimi kullanarak NuGet ile ilgili komutları için kısa bir başvuru.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: cc99b327c0edb4aeb573dfa8c2f9b9dba7b8cc38
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426011"
---
# <a name="dotnet-cli-commands"></a><span data-ttu-id="4937e-103">DotNet CLI komutları</span><span class="sxs-lookup"><span data-stu-id="4937e-103">dotnet CLI commands</span></span>

<span data-ttu-id="4937e-104">`dotnet` Komut satırı, Windows, Mac OS X ve Linux'ta çalışan, arabirimi (CLI) paketleri yayımlama yükleme ve geri yükleme gibi temel komutlar sağlar.</span><span class="sxs-lookup"><span data-stu-id="4937e-104">The `dotnet` command-line interface (CLI), which runs on Windows, Mac OS X, and Linux, provides a number of essential commands such as installing, restoring, and publishing packages.</span></span> <span data-ttu-id="4937e-105">DotNet gereksinimlerinizi karşılayıp karşılamadığını kullanmak gerekli değildir `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="4937e-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="4937e-106">Paketleri kullanmak için şu komutları kullanarak örnekleri için bkz: [yükleyin ve dotnet CLI kullanarak paketleri yönetme](../consume-packages/install-use-packages-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="4937e-106">For examples of using these commands to consume packages, see [Install and manage packages using the dotnet CLI](../consume-packages/install-use-packages-dotnet-cli.md).</span></span> <span data-ttu-id="4937e-107">Paketleri oluşturmak için şu komutları kullanarak örnekler için bkz [oluştur ve dotnet CLI kullanarak bir paket yayımlama]... / quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="4937e-107">For examples of using these commands to create packages, see [Create and publish a package using the dotnet CLI]../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

<span data-ttu-id="4937e-108">Tam komut başvurusu üzerinde için `dotnet` CLI bkz [.NET Core komut satırı arabirimi (CLI) araçlarını](/dotnet/core/tools/?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="4937e-108">For the complete command reference on `dotnet` CLI, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="4937e-109">Paket tüketim</span><span class="sxs-lookup"><span data-stu-id="4937e-109">Package consumption</span></span>

- <span data-ttu-id="4937e-110">[**DotNet paketini ekleyin**](/dotnet/core/tools/dotnet-add-package): Proje dosyasına bir paket başvurusu ekler ve ardından çalışan `dotnet restore` paketi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="4937e-110">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="4937e-111">[**DotNet paketi kaldırma**](/dotnet/core/tools/dotnet-remove-package): Paket başvurusu proje dosyasından kaldırır.</span><span class="sxs-lookup"><span data-stu-id="4937e-111">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="4937e-112">[**DotNet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Bir projenin Araçlar ve bağımlılıkları yükler.</span><span class="sxs-lookup"><span data-stu-id="4937e-112">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="4937e-113">Bu NuGet 4.0 itibariyle, aynı kodu çalıştıran `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="4937e-113">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="4937e-114">[**DotNet nuget Yereller**](/dotnet/core/tools/dotnet-nuget-locals): Listeler konumlarını *genel paketleri*, *http önbellek*, ve *temp* klasörleri ve bu klasörlerin içeriğini temizler.</span><span class="sxs-lookup"><span data-stu-id="4937e-114">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>

## <a name="package-creation"></a><span data-ttu-id="4937e-115">Paket oluşturma</span><span class="sxs-lookup"><span data-stu-id="4937e-115">Package creation</span></span>

- <span data-ttu-id="4937e-116">[**DotNet paketi**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Kod, bir NuGet paketine paketleri.</span><span class="sxs-lookup"><span data-stu-id="4937e-116">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="4937e-117">Bu NuGet 4.0 itibariyle, aynı kodu çalıştıran `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="4937e-117">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="4937e-118">[**DotNet nuget anında iletme**](/dotnet/core/tools/dotnet-nuget-push): Bir sunucuya bir paket gönderir ve bunu, nuget.org, Visual Studio Team Services ve üçüncü taraf NuGet sunucularını geçerli yayımlar.</span><span class="sxs-lookup"><span data-stu-id="4937e-118">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="4937e-119">[**DotNet nuget Sil**](/dotnet/core/tools/dotnet-nuget-delete): Nuget.org, Visual Studio Team Services ve üçüncü taraf NuGet sunucuları için geçerli bir ana paketten unlists veya siler.</span><span class="sxs-lookup"><span data-stu-id="4937e-119">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
