---
title: dotNet NuGet komutlarını | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: NuGet ile ilgili komutları dotnet komut satırı arabirimi kullanarak için kısa bir başvuru.
keywords: DotNet NuGet komutlarını, dotnet paketi, dotnet geri yükleme, dotnet nuget yerel öğeler, dotnet nuget itme, dotnet nuget Sil
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 352145701fba509e21e774a429d227e7427a1f0d
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="dotnet-commands"></a><span data-ttu-id="827c0-104">dotNet komutları</span><span class="sxs-lookup"><span data-stu-id="827c0-104">dotNet commands</span></span>

<span data-ttu-id="827c0-105">`dotnet` Windows, Mac OS X ve Linux üzerinde çalışır, komut satırı arabirimi, aşağıda listelenen gerekli nuget.exe komutları sayısını sağlar.</span><span class="sxs-lookup"><span data-stu-id="827c0-105">The `dotnet` command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="827c0-106">DotNet gereksinimlerinizi karşılamazsa, kullanmak ise gerekli değildir `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="827c0-106">If dotnet satisfies your needs, it's not necessary to use `nuget.exe`.</span></span>

<span data-ttu-id="827c0-107">Hakkında tam bilgi için `dotnet`, bkz: [.NET Core komut satırı arabirimi (CLI) araçları](/dotnet/core/tools/?tabs=netcore2x).</span><span class="sxs-lookup"><span data-stu-id="827c0-107">For complete information on `dotnet`, see [.NET Core command-line interface (CLI) tools](/dotnet/core/tools/?tabs=netcore2x).</span></span>

## <a name="package-consumption"></a><span data-ttu-id="827c0-108">Paket tüketimi</span><span class="sxs-lookup"><span data-stu-id="827c0-108">Package consumption</span></span>

- <span data-ttu-id="827c0-109">[**DotNet eklemek paket**](/dotnet/core/tools/dotnet-add-package): Proje dosyası için bir paket başvuru ekler ve sonra çalışan `dotnet restore` paketi yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="827c0-109">[**dotnet add package**](/dotnet/core/tools/dotnet-add-package): Adds a package reference to the project file, then runs `dotnet restore` to install the package.</span></span>
- <span data-ttu-id="827c0-110">[**DotNet kaldırmak paket**](/dotnet/core/tools/dotnet-remove-package): bir paket başvuru proje dosyasından kaldırır.</span><span class="sxs-lookup"><span data-stu-id="827c0-110">[**dotnet remove package**](/dotnet/core/tools/dotnet-remove-package): Removes a package reference from the project file.</span></span>
- <span data-ttu-id="827c0-111">[**DotNet geri yükleme**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): projenin araçları ve bağımlılıklar geri yükler.</span><span class="sxs-lookup"><span data-stu-id="827c0-111">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="827c0-112">NuGet 4.0 itibariyle, bu aynı kodunu çalıştırır `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="827c0-112">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="827c0-113">[**DotNet nuget Yereller**](/dotnet/core/tools/dotnet-nuget-locals): listeler konumlarını *paketleri genel*, *http önbellek*, ve *temp* klasör ve içeriğini temizler Bu klasörleri.</span><span class="sxs-lookup"><span data-stu-id="827c0-113">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Lists locations of the *global-packages*, *http-cache*, and *temp* folders and clears the contents of those folders.</span></span>

## <a name="package-creation"></a><span data-ttu-id="827c0-114">Paket oluşturma</span><span class="sxs-lookup"><span data-stu-id="827c0-114">Package creation</span></span>

- <span data-ttu-id="827c0-115">[**DotNet paketi**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): kod içinde bir NuGet paketi paketleri.</span><span class="sxs-lookup"><span data-stu-id="827c0-115">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="827c0-116">NuGet 4.0 itibariyle, bu aynı kodunu çalıştırır `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="827c0-116">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="827c0-117">[**DotNet nuget itme**](/dotnet/core/tools/dotnet-nuget-push): bir sunucuya bir paket gönderir ve onu nuget.org, Visual Studio Team Services ve üçüncü taraf NuGet sunucularına uygulanabilir yayımlar.</span><span class="sxs-lookup"><span data-stu-id="827c0-117">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
- <span data-ttu-id="827c0-118">[**DotNet nuget silmek**](/dotnet/core/tools/dotnet-nuget-delete): bir paket nuget.org, Visual Studio Team Services ve üçüncü taraf NuGet sunucular için geçerli bir ana bilgisayardan unlists veya siler.</span><span class="sxs-lookup"><span data-stu-id="827c0-118">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a host, applicable to nuget.org, Visual Studio Team Services, and third-party NuGet servers.</span></span>
