---
title: DotNet CLı NuGet komutları
description: DotNet komut satırı arabirimini kullanan NuGet ile ilgili komutlar için kısa bir başvuru.
author: JonDouglas
ms.author: jodou
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: 5438354729ccc851bbbae6c0e7b9394d4226da52
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779987"
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
