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
# <a name="dotnet-cli-commands"></a>DotNet CLI komutları

`dotnet` Komut satırı, Windows, Mac OS X ve Linux'ta çalışan, arabirimi (CLI) paketleri yayımlama yükleme ve geri yükleme gibi temel komutlar sağlar. DotNet gereksinimlerinizi karşılayıp karşılamadığını kullanmak gerekli değildir `nuget.exe`.

Paketleri kullanmak için şu komutları kullanarak örnekleri için bkz: [yükleyin ve dotnet CLI kullanarak paketleri yönetme](../consume-packages/install-use-packages-dotnet-cli.md). Paketleri oluşturmak için şu komutları kullanarak örnekleri için bkz: [oluştur ve dotnet CLI kullanarak bir paket yayımlama](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).

Tam komut başvurusu üzerinde için `dotnet` CLI bkz [.NET Core komut satırı arabirimi (CLI) araçlarını](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Paket tüketim

- [**DotNet paketini ekleyin**](/dotnet/core/tools/dotnet-add-package): Proje dosyasına bir paket başvurusu ekler ve ardından çalışan `dotnet restore` paketi yükleyin.
- [**DotNet paketi kaldırma**](/dotnet/core/tools/dotnet-remove-package): Paket başvurusu proje dosyasından kaldırır.
- [**DotNet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Bir projenin Araçlar ve bağımlılıkları yükler. Bu NuGet 4.0 itibariyle, aynı kodu çalıştıran `nuget restore`.
- [**DotNet nuget Yereller**](/dotnet/core/tools/dotnet-nuget-locals): Listeler konumlarını *genel paketleri*, *http önbellek*, ve *temp* klasörleri ve bu klasörlerin içeriğini temizler.
- [**DotNet yeni nugetconfig**](/dotnet/core/tools/dotnet-new): Oluşturur bir [ `nuget.config` ](../reference/nuget-config-file.md) NuGet davranışını yapılandırma dosyası.

## <a name="package-creation"></a>Paket oluşturma

- [**DotNet paketi**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Kod, bir NuGet paketine paketleri.
- [**DotNet nuget anında iletme**](/dotnet/core/tools/dotnet-nuget-push): Bir paket için bir NuGet sunucusu yayımlar. Nuget.org, Azure yapıları için geçerlidir ve [üçüncü taraf NuGet sunucularını](../hosting-packages/overview.md).
- [**DotNet nuget Sil**](/dotnet/core/tools/dotnet-nuget-delete): NuGet sunucusu paketinden unlists veya siler. Nuget.org, Azure yapıları için geçerlidir ve [üçüncü taraf NuGet sunucularını](../hosting-packages/overview.md).
