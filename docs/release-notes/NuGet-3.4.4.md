---
title: NuGet 3.4.4 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr NuGet 3.4.4 dahil etmek için sürüm notları.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 891d5c7ee884d31f405118739b57a169b9cd93b3
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820873"
---
# <a name="nuget-344-release-notes"></a>NuGet 3.4.4 sürüm notları

[NuGet 3.4.3 Sürüm Notları](../release-notes/nuget-3.4.3.md) | [NuGet 3.5 Beta sürüm notları](../release-notes/nuget-3.5-Beta.md)

Bu sürümü birincil odağı 3.4.3 kalitesini düzenlenmesiydi nuget.exe de Visual Studio uzantısı için birkaç düzeltmeleriyle sürümü.

VSIX ve nuget.exe indirebilirsiniz [burada](https://dist.nuget.org/index.html).

## <a name="344-rtmhttpsgithubcomnugetnugetclienttree344-rtm-2016-05-19"></a>[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)

[Tam bir değişim günlüğü](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[Sorunların listesi](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a>Değişiklikler

- Paketi iyileştirmeleri: ile paket sembolleri sevk geliştirmeleri `project.json` ve daha fazla [ \#606](https://github.com/NuGet/NuGet.Client/pull/606)
- Güncelleştirme komutunda projeleri bulunurken bir hata olduğunda özel durumu görüntüleme [\#605] ()https://github.com/NuGet/NuGet.Client/pull/605
- Paket türü girdiden okunan `.nuspec` ve `project.json` sevk [ \#603](https://github.com/NuGet/NuGet.Client/pull/603)
- Bir proje NuGet.Shared olun. [\#602](https://github.com/NuGet/NuGet.Client/pull/602)
- HTTP yanıtı zaman aşımı olarak gönderme zaman aşımı kullanmak [ \#599](https://github.com/NuGet/NuGet.Client/pull/599)
- Paket dosyaları gelecekteki sürelerine sahip kullanılan zamanları sahip olmaz [ \#597](https://github.com/NuGet/NuGet.Client/pull/597)
- Güncelleştirme `NuGet.Core.dll` XML sorunu düzeltmek için 2.12.0 sürüme [ \#594](https://github.com/NuGet/NuGet.Client/pull/594)
- ./NuGet.CommandLine.XPlat - v Destek \<ayrıntı\> \<modu\> [ \#593](https://github.com/NuGet/NuGet.Client/pull/593)
- Görüntü olmadan geri yükleme `project.json` veya `packages.config` [ \#590](https://github.com/NuGet/NuGet.Client/pull/590)
- Gerekli sürümlerinden farklı olduğunda bağımlılık sürümleri düzelttikten [ \#559](https://github.com/NuGet/NuGet.Client/pull/559)