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
# <a name="dotnet-commands"></a>DotNet komutları

`dotnet` Windows, Mac OS X ve Linux'ta çalışan, komut satırı arabirimi, aşağıda listelenen gerekli nuget.exe komut sayısını sağlar. DotNet gereksinimlerinizi karşılayıp karşılamadığını kullanmak gerekli değildir `nuget.exe`.

Hakkında eksiksiz bilgiler için `dotnet`, bkz: [.NET Core komut satırı arabirimi (CLI) araçlarını](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Paket tüketim

- [**DotNet paketini ekleyin**](/dotnet/core/tools/dotnet-add-package): proje dosyasına bir paket başvurusu ekler ve ardından çalışan `dotnet restore` paketi yükleyin.
- [**DotNet paketi kaldırma**](/dotnet/core/tools/dotnet-remove-package): bir paket başvurusu proje dosyasından kaldırır.
- [**DotNet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): projenin Araçlar ve bağımlılıkları yükler. Bu NuGet 4.0 itibariyle, aynı kodu çalıştıran `nuget restore`.
- [**DotNet nuget Yereller**](/dotnet/core/tools/dotnet-nuget-locals): konumlarını listeler *genel paketleri*, *http önbellek*, ve *temp* klasör ve içeriğini temizler Bu klasörleri.

## <a name="package-creation"></a>Paket oluşturma

- [**DotNet paketi**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): kod bir NuGet paketi paketleri. Bu NuGet 4.0 itibariyle, aynı kodu çalıştıran `nuget pack`.
- [**DotNet nuget anında iletme**](/dotnet/core/tools/dotnet-nuget-push): bir sunucuya bir paket gönderir ve bunu, nuget.org, Visual Studio Team Services ve üçüncü taraf NuGet sunucularını geçerli yayımlar.
- [**DotNet nuget Sil**](/dotnet/core/tools/dotnet-nuget-delete): nuget.org, Visual Studio Team Services ve üçüncü taraf NuGet sunucuları için geçerli bir ana paketten unlists veya siler.
