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
# <a name="dotnet-commands"></a>dotNet komutları

`dotnet` Windows, Mac OS X ve Linux üzerinde çalışır, komut satırı arabirimi, aşağıda listelenen gerekli nuget.exe komutları sayısını sağlar. DotNet gereksinimlerinizi karşılamazsa, kullanmak ise gerekli değildir `nuget.exe`.

Hakkında tam bilgi için `dotnet`, bkz: [.NET Core komut satırı arabirimi (CLI) araçları](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Paket tüketimi

- [**DotNet eklemek paket**](/dotnet/core/tools/dotnet-add-package): Proje dosyası için bir paket başvuru ekler ve sonra çalışan `dotnet restore` paketi yüklemek için.
- [**DotNet kaldırmak paket**](/dotnet/core/tools/dotnet-remove-package): bir paket başvuru proje dosyasından kaldırır.
- [**DotNet geri yükleme**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): projenin araçları ve bağımlılıklar geri yükler. NuGet 4.0 itibariyle, bu aynı kodunu çalıştırır `nuget restore`.
- [**DotNet nuget Yereller**](/dotnet/core/tools/dotnet-nuget-locals): listeler konumlarını *paketleri genel*, *http önbellek*, ve *temp* klasör ve içeriğini temizler Bu klasörleri.

## <a name="package-creation"></a>Paket oluşturma

- [**DotNet paketi**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): kod içinde bir NuGet paketi paketleri. NuGet 4.0 itibariyle, bu aynı kodunu çalıştırır `nuget pack`.
- [**DotNet nuget itme**](/dotnet/core/tools/dotnet-nuget-push): bir sunucuya bir paket gönderir ve onu nuget.org, Visual Studio Team Services ve üçüncü taraf NuGet sunucularına uygulanabilir yayımlar.
- [**DotNet nuget silmek**](/dotnet/core/tools/dotnet-nuget-delete): bir paket nuget.org, Visual Studio Team Services ve üçüncü taraf NuGet sunucular için geçerli bir ana bilgisayardan unlists veya siler.
