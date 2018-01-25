---
title: "NuGet 3.4.3 sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr NuGet 3.4.3 dahil etmek için sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 3.4.3 sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 68aab607659d15f96aefeab7bb90afc787710824
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-343-release-notes"></a>NuGet 3.4.3 sürüm notları

[NuGet 3.4.2 sürüm notları](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 sürüm notları](../release-notes/nuget-3.4.4.md)

NuGet 3.4.3 22 Nisan, 3.4 ve sonraki sürümlerde belirlendi birkaç sorunlarını gidermek üzere 2016 yayımlandı.

VSIX ve nuget.exe indirebilirsiniz [burada](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Güncelleştirmeleri ve geliştirmeleri

* Geliştirilmiş Visual Studio güvenilirlik. Visual Studio'da kilitlenme nedeniyle NuGet biz bazı sorunlar sabit.

## <a name="fixes"></a>Düzeltmeler

* Bazı yetkilendirme sorunları parola korumalı özel nuget ile akışları sabit.
* PCL ait gelen geri yüklemek erişememe geçici bir sorun sabit `project.json` belirtilen çalışma zamanları ile.
* Bazı müşteriler, paketleri yüklerken aralıklı hatalar çalışıyordu. Bu, artık bu sürümde düzeltilmiştir.
* Geri yükleme hataları C + neden olan sorunu sabit +/ CLI projeleri ile `project.json`.
* Burada değil olan doğru nuget mono seçeneğini kullandığınızda sıkıştırması açılmış bazı paketler (örneğin ModernHttpClient). Bu, artık bu sürümde düzeltilmiştir.

Düzeltmeler ve bu sürümdeki yenilikleri tam listesi için sorunların listesini kontrol [burada](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).