---
title: 3.4.4 NuGet sürüm notları
description: NuGet 3.4.4 dahil etmek için sürüm notları, sorunları, hata düzeltmeleri, eklenen özellikler ve dcr bilinir.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 44a9f21c61f0552fdc21aab24f48eee993654b01
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547479"
---
# <a name="nuget-344-release-notes"></a>3.4.4 NuGet sürüm notları

[NuGet 3.4.3 Sürüm Notları](../release-notes/nuget-3.4.3.md) | [NuGet 3.5 Beta sürüm notları](../release-notes/nuget-3.5-Beta.md)

Bu yayının birincil odağı olan 3.4.3 kalitesi geliştirmeleri ile Visual Studio uzantısını da birkaç düzeltmeler nuget.exe sürümü.

VSIX ve nuget.exe indirebileceğiniz [burada](https://dist.nuget.org/index.html).

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a>[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)

[Tam bir Changelog](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[Sorunların listesi](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a>Değişiklikler

- Paketi iyileştirmeleri: ile paketleme, sembol paketleme geliştirmeleri `project.json` ve daha fazla [ \#606](https://github.com/NuGet/NuGet.Client/pull/606)
- Güncelleştirme komutunda projeleri bulunurken bir hata olduğunda özel durumu görüntüleme [\#605](https://github.com/NuGet/NuGet.Client/pull/605)
- Paket türü girdiden okunan `.nuspec` ve `project.json` sevk [ \#603](https://github.com/NuGet/NuGet.Client/pull/603)
- Bir proje NuGet.Shared olun. [\#602](https://github.com/NuGet/NuGet.Client/pull/602)
- Gönderme zaman aşımı kullanan HTTP yanıt zaman aşımı olarak [ \#599](https://github.com/NuGet/NuGet.Client/pull/599)
- Paket dosyaları geleceğe ile kullanılan süreleri sahip olmaz [ \#597](https://github.com/NuGet/NuGet.Client/pull/597)
- Güncelleştirme `NuGet.Core.dll` 2.12.0 XML sorunu gidermek için sürüm [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)
- ./NuGet.CommandLine.XPlat - v desteği \<ayrıntı\> \<modu\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)
- Görüntü olmadan hata geri `project.json` veya `packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)
- Gerekli sürümlerinden farklı olduğunda bağımlılığı sürümlerini düzeltme [ \#559](https://github.com/NuGet/NuGet.Client/pull/559)