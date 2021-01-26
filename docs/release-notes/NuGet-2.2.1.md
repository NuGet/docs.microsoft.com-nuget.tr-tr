---
title: NuGet 2.2.1 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 2.2.1 için sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b6058fd596e32d38042aa75027640a5e5baca472
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776812"
---
# <a name="nuget-221-release-notes"></a>NuGet 2.2.1 sürüm notları

[NuGet 2,2 sürüm notları](../release-notes/nuget-2.2.md)  |  [NuGet 2,5 sürüm notları](../release-notes/nuget-2.5.md)

NuGet 2.2.1 15 Şubat 2013 ' de yayımlanmıştır.  VS uzantısı sürüm numarası 2.2.40116.9051 ' dir.

## <a name="localization-refresh"></a>Yerelleştirme yenilemesi
NuGet, Visual Studio 2012 ' in bir parçası olarak sevk edildiğinde, Ingilizce + 13 diğer dillere tamamen yerelleştirildi.  Bu tarihten sonra, NuGet 2,1 ve 2,2 sevk edildi ancak yerelleştirme yenilenmedi.  NuGet 2.2.1 sürümü yerelleştirmeyi yeniler.

NuGet 'in Kullanıcı arabirimi ve PowerShell konsolu aşağıdaki dillerde yerelleştirilir:

1. Basitleştirilmiş Çince
1. Geleneksel Çince
1. Çekçe
1. İngilizce
1. Fransızca
1. Almanca
1. İtalyanca
1. Japonca
1. Korece
1. Lehçe
1. Portekizce (Brezilya)
1. Rusça
1. İspanyolca
1. Türkçe

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a>Visual Studio şablonları birden çok önceden yüklenmiş paket depolarını destekler
Visual Studio şablonları oluşturursanız, bir şablon parçası olarak [paketleri önceden yüklemek](../visual-studio-extensibility/visual-studio-templates.md) için NuGet kullanabilirsiniz.  Bu özellik şu anda aynı kaynaktan gelmesi için gereken tüm paketlerin bir sınırlaması içeriyordu.  NuGet 2.2.1 de, birden çok depodan (şablon, bir VSıX veya kayıt defterinde tanımlanan disk üzerinde bir klasör) paketlerin yüklü olmasını sağlayabilirsiniz.

Bu özelliğin ana senaryosu özel ASP.NET proje şablonlarıdır.  Yerleşik ASP.NET şablonları önceden yüklenmiş paketleri kullanarak yerel diskten paket çekmesini kullanır.  Artık ASP.NET tarafından yüklenen mevcut paketleri kullanan özel bir ASP.NET proje şablonu oluşturabilir, ancak şablonunuza ek NuGet paketleri ekleyebilirsiniz.

## <a name="bug-fixes"></a>Hata Düzeltmeleri
NuGet 2.2.1, bazı hedeflenen hata düzeltmelerini içerir. NuGet 2.2.1 'te düzeltilen iş öğelerinin listesi için lütfen [Bu sürüm Için NuGet sorun İzleyicisi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)' ni görüntüleyin.


## <a name="known-issues"></a>Bilinen Sorunlar

ASP.NET proje şablonlarını uzatıyorsunuz, önceden yüklenmiş tüm paket depolarında öznitelik için aynı değer kullanılmalıdır `isPreunzipped` .
