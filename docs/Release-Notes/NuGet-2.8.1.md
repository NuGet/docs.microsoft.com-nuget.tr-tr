---
title: "NuGet 2.8.1 ile sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: eebbbae4-fc6a-4c05-9102-4ec66b4c64a4
description: "Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr NuGet 2.8.1 ile dahil etmek için sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 2.8.1 ile sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ac33369644d312591bfe8c06540935b2c6063c5d
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-281-release-notes"></a>NuGet 2.8.1 ile sürüm notları

[NuGet 2.8 sürüm notları](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 sürüm notları](../release-notes/nuget-2.8.2.md)

NuGet 2.8.1 ile 2 Nisan 2014'te yayımlanmıştır.

## <a name="notable-features-in-the-release"></a>Sürümdeki dikkat çekici özellikleri

### <a name="support-for-windows-phone-81-projects"></a>Windows Phone 8.1 projeleri için desteği
Bu sürümde artık hedef Windows Phone 8.1 projeleri için kullanılabilen aşağıdaki yeni hedef framework adlar destekler:

* WindowsPhone81 / WP81 (Windows Phone Silverlight tabanlı projelerde)
* WindowsPhoneApp81 / WPA81 (Windows Phone Uygulama WinRT tabanlı projelerde)

### <a name="update-of-the-nuget-webmatrix-extension"></a>NuGet WebMatrix uzantısının güncelleştirilmesi
Bu sürüm için WebMatrix bulunan NuGet istemcisi güncelleştirmelerini [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 ve getirir ile XDT dönüşümleri gibi özellikleri. Daha da önemlisi, 2.6.1 çekirdek güncelleştirme sağlar, daha yeni sürümlerinde içeren NuGet paketlerini yüklemek WebMatrix istemci `.nuspec` şeması, ASP.NET NuGet paketlerini içerir.

WebMatrix genişletmesi güncelleştirme hakkında daha fazla bilgi için belirli bir olanlar bkz [sürüm notları](../release-notes/nuget-2.6.1-for-WebMatrix.md).

### <a name="bug-fixes"></a>Hata Düzeltmeleri
Bu özelliklerine ek olarak, bu sürümü NuGet, diğer hata düzeltmeleri içerir. Sürümde ele 16 toplam sorunları vardı. Tam bir listesi için iş öğeleri NuGet 2.8.1 ile Lütfen görünüm sabit [NuGet sorun İzleyicisi bu sürüm için](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).

### <a name="reshipping-with-visual-studio-14-ctp"></a>Visual Studio ile "14" CTP reshipping
3 Haziran 2014'te yayımlanan Visual Studio "14" TEM'de, kutusuna NuGet 2.8.1 ile birlikte sağlanır. Destekleyen özellikler nominal kalır diğer 2.8.1 ile birlikte bir Visual Studio 2013 gibi VSIXes.
