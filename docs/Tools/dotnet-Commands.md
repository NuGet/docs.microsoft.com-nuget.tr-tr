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
# <a name="dotnet-commands"></a>dotNet komutları

Windows, Mac OS X ve Linux üzerinde çalışır, DotNet komut satırı arabirimi, aşağıda listelenen gerekli nuget.exe komutları sayısını sağlar. İstenen komutların dotnet sağlar burada nuget.exe karşıdan yüklemek gerekli değildir.

- [**DotNet paketi**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): kod içinde bir NuGet paketi paketleri. NuGet 4.0 itibariyle, bu aynı kodunu çalıştırır `nuget pack`.
- [**DotNet geri yükleme**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): projenin araçları ve bağımlılıklar geri yükler. NuGet 4.0 itibariyle, bu aynı kodunu çalıştırır `nuget restore`.
- [**DotNet nuget Yereller**](/dotnet/core/tools/dotnet-nuget-locals): temizler veya istek http gibi yerel NuGet kaynakları listeler önbelleği, geçici önbelleği veya makine genelinde genel paketler klasörü.
- [**DotNet nuget itme**](/dotnet/core/tools/dotnet-nuget-push): bir sunucuya bir paket gönderir ve onu, nuget.org, Visual Studio Team Services ya da herhangi bir üçüncü taraf NuGet sunucu yayımlar.
- [**DotNet nuget silmek**](/dotnet/core/tools/dotnet-nuget-delete): nuget.org, Visual Studio Team Services veya herhangi bir üçüncü taraf NuGet sunucu için geçerli bir sunucu paketinden unlists veya siler.
