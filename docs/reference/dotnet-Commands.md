---
title: DotNet CLı NuGet komutları
description: DotNet komut satırı arabirimini kullanan NuGet ile ilgili komutlar için kısa bir başvuru.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: 87cb3c8153931a0917338de9f7001406b5e12dfc
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699823"
---
# <a name="dotnet-cli-commands"></a>dotnet CLI komutları

`dotnet`Windows, Mac OS X ve Linux üzerinde çalışan komut satırı arabirimi (CLI), paket yükleme, geri yükleme ve yayımlama gibi birtakım önemli komutları sağlar. DotNet gereksinimlerinize uygunsa, kullanılması gerekli değildir `nuget.exe` .

Paketleri kullanmak için bu komutları kullanma örnekleri için bkz. [DotNet CLI kullanarak paketleri yüklemek ve yönetmek](../consume-packages/install-use-packages-dotnet-cli.md). Paketler oluşturmak için bu komutları kullanma örnekleri için bkz. [DotNet CLI kullanarak paket oluşturma ve yayımlama](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).

CLI 'daki tam komut başvurusu için `dotnet` bkz. [.NET Core komut satırı ARABIRIMI (CLI) araçları](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Paket tüketimi

- [**DotNet Add paketi**](/dotnet/core/tools/dotnet-add-package): proje dosyasına bir paket başvurusu ekler ve ardından `dotnet restore` paketi yüklemek için çalıştırılır.
- [**DotNet Remove paketi**](/dotnet/core/tools/dotnet-remove-package): proje dosyasından bir paket başvurusunu kaldırır.
- [**DotNet restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): bir projenin bağımlılıklarını ve araçlarını geri yükler. NuGet 4,0 itibariyle bu, ile aynı kodu çalıştırır `nuget restore` .
- [**DotNet NuGet Yereller**](/dotnet/core/tools/dotnet-nuget-locals): *genel paketler*, *http önbelleği* ve *geçici* klasörlerin konumlarını listeler ve bu klasörlerin içeriğini temizler.
- [**DotNet New nugetconfig**](/dotnet/core/tools/dotnet-new): [`nuget.config`](../reference/nuget-config-file.md) NuGet davranışını yapılandırmak için bir dosya oluşturur.

## <a name="package-creation"></a>Paket oluşturma

- [**DotNet Pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): kodu bir NuGet paketine paketler.
- [**DotNet NuGet Push**](/dotnet/core/tools/dotnet-nuget-push): bir NuGet sunucusuna paket yayımlar. Nuget.org, Azure Artifacts ve [üçüncü taraf NuGet sunucuları](../hosting-packages/overview.md)için geçerlidir.
- [**DotNet NuGet Delete**](/dotnet/core/tools/dotnet-nuget-delete): bir NuGet sunucusundan bir paketi siler veya listesini kaldırır. Nuget.org, Azure Artifacts ve [üçüncü taraf NuGet sunucuları](../hosting-packages/overview.md)için geçerlidir.
- [**DotNet NuGet doğrulaması**](/dotnet/core/tools/dotnet-nuget-verify): Imzalı bir NuGet paketini doğrular.
