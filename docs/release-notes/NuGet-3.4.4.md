---
title: NuGet 3.4.4 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 3.4.4 için sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4e5e635432147afba4809562035bc8c762d31af4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780229"
---
# <a name="nuget-344-release-notes"></a>NuGet 3.4.4 sürüm notları

[NuGet 3.4.3 sürüm notları](../release-notes/nuget-3.4.3.md)  |  [NuGet 3,5-Beta sürüm notları](../release-notes/nuget-3.5-Beta.md)

Bu yayının birincil odağında, Visual Studio uzantısı için birkaç düzeltme ile nuget.exe 3.4.3 sürümünün kalitesi geliştirılmıştır.

Hem VSıX hem [de nuget.exe yükleyebilirsiniz](https://dist.nuget.org/index.html).

## <a name="344-rtm-2016-05-19"></a>[3.4.4-RTM](https://github.com/NuGet/NuGet.Client/tree/3.4.4-rtm) (2016-05-19)

[Tam changelog](https://github.com/NuGet/NuGet.Client/compare/3.5.0-beta-final...3.4.4-rtm)

[Sorunların listesi](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.4+is%3Aclosed)

### <a name="changes"></a>Değişiklikler

- Paket geliştirmeleri: paketleme `project.json` ve daha fazla [ \# 606](https://github.com/NuGet/NuGet.Client/pull/606) Ile paketleme simgeleri için geliştirmeler
- Update komutunda projeler bulunurken hata oluştu [ \# 605] (https://github.com/NuGet/NuGet.Client/pull/605
- Girişte paket türünü oku `.nuspec` ve `project.json` paketleme [ \# 603](https://github.com/NuGet/NuGet.Client/pull/603)
- NuGet. Shared bir proje değil. [\#602](https://github.com/NuGet/NuGet.Client/pull/602)
- HTTP yanıt zaman aşımı [ \# 599](https://github.com/NuGet/NuGet.Client/pull/599) olarak gönderme zaman aşımını kullanın
- Gelecekteki sürelerle paket dosyalarının süresi kullanılmayacak [ \# 597](https://github.com/NuGet/NuGet.Client/pull/597)
- `NuGet.Core.dll`XML sorununu onarmak için sürüm 2.12.0 güncelleştiriliyor [ \# 594](https://github.com/NuGet/NuGet.Client/pull/594)
- Support./NuGet.CommandLine.XPlat-v \<verbosity\> \<mode\> [ \# 593](https://github.com/NuGet/NuGet.Client/pull/593)
- `project.json`Veya `packages.config` [ \# 590](https://github.com/NuGet/NuGet.Client/pull/590) olmadan geri yükleme hatasını görüntüle
- Gerekli sürümler farklı olduğunda bağımlılık sürümleri düzeltiliyor [ \# 559](https://github.com/NuGet/NuGet.Client/pull/559)