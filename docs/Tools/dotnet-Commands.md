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
ms.openlocfilehash: 7ff4779f46db102f1384650d82118b34fedd4413
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="dotnet-commands"></a><span data-ttu-id="9d67a-104">dotNet komutları</span><span class="sxs-lookup"><span data-stu-id="9d67a-104">dotNet commands</span></span>

<span data-ttu-id="9d67a-105">Windows, Mac OS X ve Linux üzerinde çalışır, DotNet komut satırı arabirimi, aşağıda listelenen gerekli nuget.exe komutları sayısını sağlar.</span><span class="sxs-lookup"><span data-stu-id="9d67a-105">The DotNet command-line interface, which runs on Windows, Mac OS X, and Linux, provides a number of essential nuget.exe commands as listed below.</span></span> <span data-ttu-id="9d67a-106">İstenen komutların dotnet sağlar burada nuget.exe karşıdan yüklemek gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="9d67a-106">Where dotnet provides the desired commands, it is not necessary to download nuget.exe.</span></span>

- <span data-ttu-id="9d67a-107">[**DotNet paketi**](https://docs.microsoft.com/dotnet/core/tools/dotnet-pack?tabs=netcore2x): paketleri kod için NETCore SDK projeleri bir NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="9d67a-107">[**dotnet pack**](https://docs.microsoft.com/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packs code for NETCore SDK projects into a NuGet package.</span></span> <span data-ttu-id="9d67a-108">Diğer tüm proje türleri kullanmanız gerekir[`nuget pack`](cli-ref-pack.md)</span><span class="sxs-lookup"><span data-stu-id="9d67a-108">All other project types should use [`nuget pack`](cli-ref-pack.md)</span></span>
- <span data-ttu-id="9d67a-109">[**DotNet geri yükleme**](https://docs.microsoft.com/dotnet/core/tools/dotnet-restore?tabs=netcore2x): projenin araçları ve bağımlılıklar geri yükler.</span><span class="sxs-lookup"><span data-stu-id="9d67a-109">[**dotnet restore**](https://docs.microsoft.com/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Restores the dependencies and tools of a project.</span></span> <span data-ttu-id="9d67a-110">NuGet 4.0 itibariyle, bu aynı kodunu çalıştırır `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="9d67a-110">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>
- <span data-ttu-id="9d67a-111">[**DotNet nuget Yereller**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-locals): temizler veya istek http gibi yerel NuGet kaynakları listeler önbelleği, geçici önbelleği veya makine genelinde genel paketler klasörü.</span><span class="sxs-lookup"><span data-stu-id="9d67a-111">[**dotnet nuget locals**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-locals): Clears or lists local NuGet resources such as http the -request cache, temporary cache, or machine-wide global packages folder.</span></span>
- <span data-ttu-id="9d67a-112">[**DotNet nuget itme**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-push): bir sunucuya bir paket gönderir ve onu, nuget.org, Visual Studio Team Services ya da herhangi bir üçüncü taraf NuGet sunucu yayımlar.</span><span class="sxs-lookup"><span data-stu-id="9d67a-112">[**dotnet nuget push**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-push): Pushes a package to a server and publishes it, applicable to nuget.org, Visual Studio Team Services, or any third-party NuGet servers.</span></span>
- <span data-ttu-id="9d67a-113">[**DotNet nuget silmek**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-delete): nuget.org, Visual Studio Team Services veya herhangi bir üçüncü taraf NuGet sunucu için geçerli bir sunucu paketinden unlists veya siler.</span><span class="sxs-lookup"><span data-stu-id="9d67a-113">[**dotnet nuget delete**](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-delete): Deletes or unlists a package from a  server, applicable to nuget.org, Visual Studio Team Services, or any third-party NuGet servers.</span></span>
