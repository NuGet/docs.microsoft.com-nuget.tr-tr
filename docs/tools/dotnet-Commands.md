---
title: DotNet NuGet komutları
description: NuGet ile ilgili komutları dotnet komut satırı arabirimi kullanarak için kısa bir başvuru.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/23/2018
ms.topic: conceptual
ms.openlocfilehash: fe49274af339c987d5e090c99edd78f62f59ce47
ms.sourcegitcommit: 5fcd6d664749aa720359104ef7a66d38aeecadc2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/27/2018
---
# <a name="dotnet-commands"></a><span data-ttu-id="d17f4-103">DotNet komutları</span><span class="sxs-lookup"><span data-stu-id="d17f4-103">dotnet commands</span></span>

<span data-ttu-id="d17f4-104">`dotnet` Windows, Mac OS X ve Linux üzerinde çalışır, komut satırı arabirimi, aşağıda listelenen gerekli nuget.exe komutları sayısını sağlar.</span><span class="sxs-lookup"><span data-stu-id="d17f4-104">The `dotnet` command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="d17f4-105">DotNet gereksinimlerinizi karşılamazsa, kullanmak ise gerekli değildir `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="d17f4-105">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="d17f4-106">Hakkında tam bilgi için `dotnet`, bkz: [.NET Core komut satırı arabirimi (CLI) araçları](/dotnet/core/tools/?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="d17f4-106">For complete information on `dotnet`, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="d17f4-107">Paket tüketimi</span><span class="sxs-lookup"><span data-stu-id="d17f4-107">Package consumption</span></span>

- <span data-ttu-id="d17f4-108">[**DotNet eklemek paket**](/dotnet/core/tools/dotnet-add-package): Proje dosyası için bir paket başvuru ekler ve sonra çalışan `dotnet restore` paketi yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="d17f4-108">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="d17f4-109">[**DotNet kaldırmak paket**](/dotnet/core/tools/dotnet-remove-package): bir paket başvuru proje dosyasından kaldırır.</span><span class="sxs-lookup"><span data-stu-id="d17f4-109">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="d17f4-110">[**DotNet geri yükleme**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): projenin araçları ve bağımlılıklar geri yükler.</span><span class="sxs-lookup"><span data-stu-id="d17f4-110">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="d17f4-111">NuGet 4.0 itibariyle, bu aynı kodunu çalıştırır `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="d17f4-111">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="d17f4-112">[**DotNet nuget Yereller**](/dotnet/core/tools/dotnet-nuget-locals): listeler konumlarını *paketleri genel*, *http önbellek*, ve *temp* klasör ve içeriğini temizler Bu klasörleri.</span><span class="sxs-lookup"><span data-stu-id="d17f4-112">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>

## <a name="package-creation"></a><span data-ttu-id="d17f4-113">Paket oluşturma</span><span class="sxs-lookup"><span data-stu-id="d17f4-113">Package creation</span></span>

- <span data-ttu-id="d17f4-114">[**DotNet paketi**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): kod içinde bir NuGet paketi paketleri.</span><span class="sxs-lookup"><span data-stu-id="d17f4-114">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="d17f4-115">NuGet 4.0 itibariyle, bu aynı kodunu çalıştırır `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="d17f4-115">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="d17f4-116">[**DotNet nuget itme**](/dotnet/core/tools/dotnet-nuget-push): bir sunucuya bir paket gönderir ve onu nuget.org, Visual Studio Team Services ve üçüncü taraf NuGet sunucularına uygulanabilir yayımlar.</span><span class="sxs-lookup"><span data-stu-id="d17f4-116">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="d17f4-117">[**DotNet nuget silmek**](/dotnet/core/tools/dotnet-nuget-delete): bir paket nuget.org, Visual Studio Team Services ve üçüncü taraf NuGet sunucular için geçerli bir ana bilgisayardan unlists veya siler.</span><span class="sxs-lookup"><span data-stu-id="d17f4-117">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
