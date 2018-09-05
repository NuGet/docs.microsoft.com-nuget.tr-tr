---
title: DotNet NuGet komutları
description: Dotnet komut satırı arabirimi kullanarak NuGet ile ilgili komutları için kısa bir başvuru.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: conceptual
ms.openlocfilehash: 88e058be674ecddc500665bfa3517f19acde0cd7
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546322"
---
# <a name="dotnet-commands"></a><span data-ttu-id="22f4d-103">DotNet komutları</span><span class="sxs-lookup"><span data-stu-id="22f4d-103">dotnet commands</span></span>

<span data-ttu-id="22f4d-104">`dotnet` Windows, Mac OS X ve Linux'ta çalışan, komut satırı arabirimi, aşağıda listelenen gerekli nuget.exe komut sayısını sağlar.</span><span class="sxs-lookup"><span data-stu-id="22f4d-104">The `dotnet` command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="22f4d-105">DotNet gereksinimlerinizi karşılayıp karşılamadığını kullanmak gerekli değildir `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="22f4d-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="22f4d-106">Hakkında eksiksiz bilgiler için `dotnet`, bkz: [.NET Core komut satırı arabirimi (CLI) araçlarını](/dotnet/core/tools/?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="22f4d-106">For complete information on `dotnet`, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="22f4d-107">Paket tüketim</span><span class="sxs-lookup"><span data-stu-id="22f4d-107">Package consumption</span></span>

- <span data-ttu-id="22f4d-108">[**DotNet paketini ekleyin**](/dotnet/core/tools/dotnet-add-package): proje dosyasına bir paket başvurusu ekler ve ardından çalışan `dotnet restore` paketi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="22f4d-108">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="22f4d-109">[**DotNet paketi kaldırma**](/dotnet/core/tools/dotnet-remove-package): bir paket başvurusu proje dosyasından kaldırır.</span><span class="sxs-lookup"><span data-stu-id="22f4d-109">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="22f4d-110">[**DotNet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): projenin Araçlar ve bağımlılıkları yükler.</span><span class="sxs-lookup"><span data-stu-id="22f4d-110">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="22f4d-111">Bu NuGet 4.0 itibariyle, aynı kodu çalıştıran `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="22f4d-111">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="22f4d-112">[**DotNet nuget Yereller**](/dotnet/core/tools/dotnet-nuget-locals): konumlarını listeler *genel paketleri*, *http önbellek*, ve *temp* klasör ve içeriğini temizler Bu klasörleri.</span><span class="sxs-lookup"><span data-stu-id="22f4d-112">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>

## <a name="package-creation"></a><span data-ttu-id="22f4d-113">Paket oluşturma</span><span class="sxs-lookup"><span data-stu-id="22f4d-113">Package creation</span></span>

- <span data-ttu-id="22f4d-114">[**DotNet paketi**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): kod bir NuGet paketi paketleri.</span><span class="sxs-lookup"><span data-stu-id="22f4d-114">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="22f4d-115">Bu NuGet 4.0 itibariyle, aynı kodu çalıştıran `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="22f4d-115">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="22f4d-116">[**DotNet nuget anında iletme**](/dotnet/core/tools/dotnet-nuget-push): bir sunucuya bir paket gönderir ve bunu, nuget.org, Visual Studio Team Services ve üçüncü taraf NuGet sunucularını geçerli yayımlar.</span><span class="sxs-lookup"><span data-stu-id="22f4d-116">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="22f4d-117">[**DotNet nuget Sil**](/dotnet/core/tools/dotnet-nuget-delete): nuget.org, Visual Studio Team Services ve üçüncü taraf NuGet sunucuları için geçerli bir ana paketten unlists veya siler.</span><span class="sxs-lookup"><span data-stu-id="22f4d-117">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
