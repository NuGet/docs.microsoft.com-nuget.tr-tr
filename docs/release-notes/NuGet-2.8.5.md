---
title: NuGet 2.8.5 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr NuGet 2.8.5 dahil etmek için sürüm notları.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 40557035e445d07e7acf301e34b750b329ba9990
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820085"
---
# <a name="nuget-285-release-notes"></a>NuGet 2.8.5 sürüm notları

[NuGet 2.8.3 Sürüm Notları](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 sürüm notları](../release-notes/nuget-2.8.6.md)

NuGet 2.8.5, 30 Mart 2015 yayımlanmıştır. Küçük bir güncelleştirmesidir bizim 2.8.3 VSIX bazı düzeltmeler hedeflenen.

Bu sürümde için NuGet Paket Yöneticisi iletişim için destek eklenmiştir [DNX hedef Framework adlar](https://github.com/aspnet/dnx).  Desteklenen bu yeni framework adları şunlardır:

* **core50** - A 'base' hedef framework ad (TFM) çekirdek CLR ile uyumludur.
* **dnx452** - tam 4.5.2 kullanarak A TFM DNX tabanlı belirli uygulamaları framework sürümü
* **dnx46** - framework'ün tam 4.6 sürümünü kullanarak bir TFM DNX tabanlı belirli uygulamaları
* **dnxcore50** - framework çekirdek 5.0 sürümünü kullanarak bir TFM DNX tabanlı belirli uygulamaları

Bir hata FSharp projelere düzgün şekilde yüklenmesini önlenmiş bu paketleri düzeltildi:

https://nuget.codeplex.com/workitem/4400