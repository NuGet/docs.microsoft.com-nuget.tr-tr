---
title: 2.8.1 NuGet sürüm notları
description: NuGet 2.8.1 dahil etmek için sürüm notları, sorunları, hata düzeltmeleri, eklenen özellikler ve dcr bilinir.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 39fb7db00e18e32eef15adc11764a122c97ddfd5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545245"
---
# <a name="nuget-281-release-notes"></a>2.8.1 NuGet sürüm notları

[NuGet 2.8 sürüm notları](../release-notes/nuget-2.8.md) | [2.8.2 NuGet sürüm notları](../release-notes/nuget-2.8.2.md)

NuGet 2.8.1 2 Nisan 2014'te yayımlanmıştır.

## <a name="notable-features-in-the-release"></a>Sürümündeki önemli özelliklere

### <a name="support-for-windows-phone-81-projects"></a>Windows Phone 8.1 projeleri için destek
Bu sürüm, artık hedef Windows Phone 8.1 projeleri için kullanılabilen aşağıdaki yeni hedef çerçeve bilinen adlar destekler:

* WindowsPhone81 / WP81 (Windows Phone Silverlight tabanlı projelerde)
* WindowsPhoneApp81 / WPA81 (Windows Phone Uygulama WinRT tabanlı projelerde)

### <a name="update-of-the-nuget-webmatrix-extension"></a>NuGet WebMatrix genişletmesi güncelleştirme
Bu sürüm için WebMatrix bulunan NuGet istemcisi güncelleştirmelerini [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 ve getirir ile XDT dönüşümleri gibi özellikleri. 2.6.1 daha da önemlisi, çekirdek güncelleştirme sağlar, daha yeni sürümlerini içeren NuGet paketlerini yüklemek WebMatrix istemci `.nuspec` ASP.NET NuGet paketlerini içeren şema.

WebMatrix genişletmesi güncelleştirme hakkında daha fazla bilgi için bu belirli bkz [sürüm notları](../release-notes/nuget-2.6.1-for-WebMatrix.md).

### <a name="bug-fixes"></a>Hata Düzeltmeleri
Bu özelliklerin yanı sıra, bu sürüm nuget diğer hata düzeltmeleri içerir. Sürümünde giderilen 16 toplam sorunlar oluştu. Tam bir listesi için iş öğeleri Nuget'te 2.8.1, lütfen görünümü sabit [bu sürüm için NuGet sorun İzleyicisi](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).

### <a name="reshipping-with-visual-studio-14-ctp"></a>Visual Studio "14" CTP reshipping
3 Haziran 2014'te yayımlanan Visual Studio "14" CTP içinde NuGet 2.8.1 kutuya sevk edilir. Par destekleyen özellikler kalan diğer 2.8.1 ile VSIXes gibi Visual Studio 2013 için.
