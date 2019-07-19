---
title: DotNet CLı NuGet komutları
description: DotNet komut satırı arabirimini kullanan NuGet ile ilgili komutlar için kısa bir başvuru.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: ff011e60d3de3b0999db56e1e30e97e538bd9fb4
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328251"
---
# <a name="dotnet-cli-commands"></a>DotNet CLı komutları

Windows, Mac OS X ve Linux üzerinde çalışan komutsatırıarabirimi(CLI),paketyükleme,geriyüklemeveyayımlamagibibirtakımönemlikomutlarısağlar.`dotnet` DotNet gereksinimlerinize uygunsa, kullanılması `nuget.exe`gerekli değildir.

Paketleri kullanmak için bu komutları kullanma örnekleri için bkz. [DotNet CLI kullanarak paketleri yüklemek ve yönetmek](../consume-packages/install-use-packages-dotnet-cli.md). Paketler oluşturmak için bu komutları kullanma örnekleri için bkz. [DotNet CLI kullanarak paket oluşturma ve yayımlama](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).

CLI 'daki `dotnet` tam komut başvurusu için bkz. [.NET Core komut satırı arabirimi (CLI) araçları](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Paket tüketimi

- [**DotNet Add paketi**](/dotnet/core/tools/dotnet-add-package): Proje dosyasına bir paket başvurusu ekler ve sonra paketi yüklemek için `dotnet restore` çalıştırılır.
- [**DotNet kaldırma paketi**](/dotnet/core/tools/dotnet-remove-package): Proje dosyasından bir paket başvurusunu kaldırır.
- [**DotNet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Bir projenin bağımlılıklarını ve araçlarını geri yükler. NuGet 4,0 itibariyle bu, ile `nuget restore`aynı kodu çalıştırır.
- [**DotNet NuGet Yereller**](/dotnet/core/tools/dotnet-nuget-locals): *Genel paketler*, *http önbelleği*ve *geçici* klasörlerin konumlarını listeler ve bu klasörlerin içeriğini temizler.
- [**DotNet yeni nugetconfig**](/dotnet/core/tools/dotnet-new): NuGet davranışını [`nuget.config`](../reference/nuget-config-file.md) yapılandırmak için bir dosya oluşturur.

## <a name="package-creation"></a>Paket oluşturma

- [**DotNet paketi**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Kodu bir NuGet paketine paketler.
- [**DotNet NuGet Push**](/dotnet/core/tools/dotnet-nuget-push): Bir NuGet sunucusuna paket yayımlar. Nuget.org, Azure Artifacts ve [üçüncü taraf NuGet sunucuları](../hosting-packages/overview.md)için geçerlidir.
- [**DotNet NuGet silme**](/dotnet/core/tools/dotnet-nuget-delete): NuGet sunucusundan bir paketi siler veya listesini kaldırır. Nuget.org, Azure Artifacts ve [üçüncü taraf NuGet sunucuları](../hosting-packages/overview.md)için geçerlidir.
