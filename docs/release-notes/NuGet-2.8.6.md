---
title: NuGet 2.8.6 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 2.8.6 için sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ea291bdf7a5b6cc3ac3bde526030e517db4632d7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776708"
---
# <a name="nuget-286-release-notes"></a>NuGet 2.8.6 sürüm notları

[NuGet 2.8.5 sürüm notları](../release-notes/nuget-2.8.5.md)  |  [NuGet 2.8.7 sürüm notları](../release-notes/nuget-2.8.7.md)

NuGet 2.8.6, Windows 10 UWP geliştirme modeli desteğiyle birlikte sunulan paketleri desteklemek için bazı hedeflenen düzeltmeler ve geliştirmeler ile 2.8.5 VSıX 2015 Temmuz ' den yayımlanmıştır.

NuGet Paket Yöneticisi uzantısının bu sürümü yalnızca Visual Studio 2013 için destek sağlar.

Bu sürümde, NuGet Paket Yöneticisi iletişim kutusunda için destek eklenmiştir:

* Windows 10 uygulama geliştirmeyi desteklemek için UıAP hedef Framework bilinen adı kullanıma sunulmuştur.
* NuGet protokol sürümü 3 uç noktaları
* Depo kaynaklarında [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion özniteliği için destek. Varsayılan değer "2"
* Gerekli bir paket sürümü yerel önbellekte yoksa uzak depoya geri dönülüyor