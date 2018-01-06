---
title: "dotNet NuGet komutlarını | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 0c81dbc4-2c14-4ec8-b87a-b802a899c3ea
description: "NuGet ile ilgili komutları dotnet komut satırı arabirimi kullanarak için kısa bir başvuru."
keywords: "DotNet NuGet komutlarını, dotnet paketi, dotnet geri yükleme, dotnet nuget yerel öğeler, dotnet nuget itme, dotnet nuget Sil"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d020e62b8bd04c8f4a75756fb30ebcf13ffdb1b3
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/05/2018
---
# <a name="dotnet-commands"></a><span data-ttu-id="c403f-104">dotNet komutları</span><span class="sxs-lookup"><span data-stu-id="c403f-104">dotNet commands</span></span>

<span data-ttu-id="c403f-105">Windows, Mac OS X ve Linux üzerinde çalışır, DotNet komut satırı arabirimi, aşağıda listelenen gerekli nuget.exe komutları sayısını sağlar.</span><span class="sxs-lookup"><span data-stu-id="c403f-105">The DotNet command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="c403f-106">İstenen komutların dotnet sağlar burada nuget.exe karşıdan yüklemek gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="c403f-106">Where dotnet provides the desired commands, it's not necessary to download nuget.exe.</span></span>

- <span data-ttu-id="c403f-107">[**DotNet paketi**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): kod içinde bir NuGet paketi paketleri.</span><span class="sxs-lookup"><span data-stu-id="c403f-107">[**dotnet pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs the code into a NuGet package.</span></span> <span data-ttu-id="c403f-108">NuGet 4.0 itibariyle, bu aynı kodunu çalıştırır `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="c403f-108">As of NuGet 4.0, this runs the same code as `nuget pack`.</span></span>
- <span data-ttu-id="c403f-109">[**DotNet geri yükleme**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): projenin araçları ve bağımlılıklar geri yükler.</span><span class="sxs-lookup"><span data-stu-id="c403f-109">[**dotnet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="c403f-110">NuGet 4.0 itibariyle, bu aynı kodunu çalıştırır `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="c403f-110">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="c403f-111">[**DotNet nuget Yereller**](/dotnet/core/tools/dotnet-nuget-locals): temizler veya istek http gibi yerel NuGet kaynakları listeler önbelleği, geçici önbelleği veya makine genelinde genel paketler klasörü.</span><span class="sxs-lookup"><span data-stu-id="c403f-111">[**dotnet nuget locals**](/dotnet/core/tools/dotnet-nuget-locals): Clears or lists local NuGet resources such as http the -request cache, temporary cache, or machine-wide global packages folder.</span></span>
- <span data-ttu-id="c403f-112">[**DotNet nuget itme**](/dotnet/core/tools/dotnet-nuget-push): bir sunucuya bir paket gönderir ve onu, nuget.org, Visual Studio Team Services ya da herhangi bir üçüncü taraf NuGet sunucu yayımlar.</span><span class="sxs-lookup"><span data-stu-id="c403f-112">[**dotnet nuget push**](/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, or any third-party NuGet servers.</span></span>
- <span data-ttu-id="c403f-113">[**DotNet nuget silmek**](/dotnet/core/tools/dotnet-nuget-delete): nuget.org, Visual Studio Team Services veya herhangi bir üçüncü taraf NuGet sunucu için geçerli bir sunucu paketinden unlists veya siler.</span><span class="sxs-lookup"><span data-stu-id="c403f-113">[**dotnet nuget delete**](/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a  server, applicable to nuget.org, Visual Studio Team Services, or any third-party NuGet servers.</span></span>
