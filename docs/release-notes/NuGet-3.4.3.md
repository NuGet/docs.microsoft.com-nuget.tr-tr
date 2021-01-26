---
title: NuGet 3.4.3 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 3.4.3 için sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f0d9740aaf0a82b9e4023b5e4990c8f4adbea63c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776473"
---
# <a name="nuget-343-release-notes"></a>NuGet 3.4.3 sürüm notları

[NuGet 3.4.2 sürüm notları](../release-notes/nuget-3.4.2.md)  |  [NuGet 3.4.4 sürüm notları](../release-notes/nuget-3.4.4.md)

NuGet 3.4.3, 3,4 Nisan 2016 ' de, ve sonraki sürümlerde tanımlanmış birçok sorunu gidermek için yayımlanmıştır.

Hem VSıX hem [de nuget.exe yükleyebilirsiniz](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Güncelleştirmeler ve geliştirmeler

* Geliştirilmiş Visual Studio güvenilirliği. NuGet 'de Visual Studio 'da kilitlenmelere neden olan bazı sorunlar düzeltildi.

## <a name="fixes"></a>Düzeltmeler

* Parola korumalı özel NuGet akışlarıyla bazı yetkilendirme sorunları düzeltildi.
* PCL 'in `project.json` belirtilen çalışma zamanları ile birlikte geri yükleme sorunu düzeltildi.
* Bazı müşteriler, paket yüklenirken aralıklı hatalara karşı çalışmaktadır. Bu, şimdi bu sürümde düzeltildi.
* C++/CLı projelerinde ile geri yükleme hatalarının oluşmasına neden olan bir sorun düzeltildi `project.json` .
* Mono 'da NuGet kullandığınızda bazı paketler (ör. ModernHttpClient), sıkıştırılmayan bir biçimde. Bu, şimdi bu sürümde düzeltildi.

Bu sürümdeki düzeltmelerin ve geliştirmelerin tüm listesi için [buradaki](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed)sorun listesini inceleyin.