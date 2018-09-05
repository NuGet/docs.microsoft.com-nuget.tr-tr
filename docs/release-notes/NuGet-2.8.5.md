---
title: 2.8.5 NuGet sürüm notları
description: NuGet 2.8.5 dahil etmek için sürüm notları, sorunları, hata düzeltmeleri, eklenen özellikler ve dcr bilinir.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: aa03b00a0043a4805f33900124c13b0777c2b7a3
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548631"
---
# <a name="nuget-285-release-notes"></a>2.8.5 NuGet sürüm notları

[NuGet 2.8.3 sürüm notlarına](../release-notes/nuget-2.8.3.md) | [2.8.6 NuGet sürüm notları](../release-notes/nuget-2.8.6.md)

NuGet 2.8.5, 30 Mart 2015 kullanıma sunuldu. Küçük bir güncelleştirmesidir bizim 2.8.3 için VSIX bazı düzeltmeleri hedeflenen.

NuGet Paket Yöneticisi iletişim kutusu için destek eklendi bu sürümde, [DNX hedef çerçeve bilinen adlar](https://github.com/aspnet/dnx).  Desteklenen bu yeni framework takma adlar şunlardır:

* **core50** - A 'base' hedef çerçeve adı (TFM) Core CLR ile uyumludur.
* **dnx452** - tam 4.5.2 kullanarak bir TFM belirli DNX tabanlı uygulamaları framework sürümü
* **dnx46** - framework'ün tam 4.6 sürümünü kullanarak bir TFM DNX tabanlı özel uygulamalar
* **dnxcore50** - framework Core 5.0 sürümü kullanarak bir TFM DNX tabanlı özel uygulamalar

Bir hatanın düzeltilip FSharp projelere düzgün bir şekilde yüklenmesini önlenmiş bu paketleri:

https://nuget.codeplex.com/workitem/4400