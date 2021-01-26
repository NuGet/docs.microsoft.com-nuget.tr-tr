---
title: NuGet 2.8.1 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 2.8.1 için sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4dcd8ab140026c39345f850ac00a7a5f26a0e62c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776767"
---
# <a name="nuget-281-release-notes"></a>NuGet 2.8.1 sürüm notları

[NuGet 2,8 sürüm notları](../release-notes/nuget-2.8.md)  |  [NuGet 2.8.2 sürüm notları](../release-notes/nuget-2.8.2.md)

NuGet 2.8.1, 2 Nisan 2014 ' de yayımlanmıştır.

## <a name="notable-features-in-the-release"></a>Yayındaki önemli özellikler

### <a name="support-for-windows-phone-81-projects"></a>Windows Phone 8,1 projeleri için destek
Bu sürüm artık Windows Phone 8,1 projelerini hedeflemek için kullanılabilecek aşağıdaki yeni hedef çerçeve bilinen adlarını desteklemektedir:

* WindowsPhone81/WP81 (Silverlight tabanlı Windows Phone projeleri için)
* WindowsPhoneApp81/WPA81 (WinRT tabanlı Windows Phone uygulama projeleri için)

### <a name="update-of-the-nuget-webmatrix-extension"></a>NuGet WebMatrix uzantısının güncelleştirilmesi
Bu sürüm WebMatrix 'te bulunan NuGet istemcisini [NuGet. Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 olarak güncelleştirir ve xdt dönüştürmeleri gibi BT özellikleriyle birlikte getirir. Daha da önemlisi, 2.6.1 Core Update, WebMatrix istemcisinin, `.nuspec` ASP.net NuGet paketlerini içeren, şemanın daha yeni sürümlerini Içeren NuGet paketlerini yüklemesini sağlar.

WebMatrix uzantısı güncelleştirmesi hakkında daha fazla bilgi için, bkz. ilgili [sürüm notları](../release-notes/nuget-2.6.1-for-WebMatrix.md).

### <a name="bug-fixes"></a>Hata Düzeltmeleri
Bu özelliklere ek olarak, NuGet 'in bu sürümü diğer hata düzeltmelerini içerir. Yayında oluşan 16 Toplam sorun oluştu. NuGet 2.8.1 'te düzeltilen iş öğelerinin tam listesi için lütfen [Bu sürüm Için NuGet sorun İzleyicisi](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)' ni görüntüleyin.

### <a name="reshipping-with-visual-studio-14-ctp"></a>Visual Studio "14" CTP ile reshipping
Visual Studio "14" CTP 'de 3 Haziran 2014 ' de yayınlanan NuGet 2.8.1, kutuya gönderilir. Desteklediği özellikler, Visual Studio 2013 için bir diğeri gibi diğer 2.8.1 sanal parçalar ile eşit olarak kalır.
