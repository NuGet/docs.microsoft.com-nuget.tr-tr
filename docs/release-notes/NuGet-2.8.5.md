---
title: NuGet 2.8.5 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 2.8.5 için sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f729092bc964b286a007564bd3bbd8c79bc895c9
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780356"
---
# <a name="nuget-285-release-notes"></a>NuGet 2.8.5 sürüm notları

[NuGet 2.8.3 sürüm notları](../release-notes/nuget-2.8.3.md)  |  [NuGet 2.8.6 sürüm notları](../release-notes/nuget-2.8.6.md)

NuGet 2.8.5 30 Mart 2015 ' de yayımlanmıştır. 2.8.3 VSıX 'in bazı hedeflenen düzeltmeleri içeren küçük bir güncelleştirmedir.

Bu sürümde, [DNX hedef çerçeve adları](https://github.com/aspnet/dnx)Için NuGet paket yöneticisi desteği iletişim kutusu eklenmiştir.  Desteklenen bu yeni çerçeve bilinen adları şunlardır:

* **core50** -çekirdek clr ile uyumlu bir ' Base ' hedef çerçeve bilinen adı (tfd).
* **dnx452** -Framework 'ün tam 4.5.2 sürümünü kullanarak DNX tabanlı uygulamalara özel bir tfd
* **dnx46** -Framework 'ün tam 4,6 sürümünü kullanarak DNX tabanlı uygulamalara özel bir tfd
* **adlar** -Framework 'ün Core 5,0 sürümünü kullanarak DNX tabanlı uygulamalara özel bir tfd

Paketlerin FSharp projelerine düzgün şekilde yüklenmesini önleyen bir hata düzeltildi:

https://nuget.codeplex.com/workitem/4400