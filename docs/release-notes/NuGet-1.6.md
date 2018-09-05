---
title: NuGet 1.6 sürüm notları
description: NuGet bilinen sorunları, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr 1.6 için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 351303ca3ae27a37c19e59d84dfc9b4629fe0ca5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549018"
---
 # <a name="nuget-16-release-notes"></a>NuGet 1.6 sürüm notları

[1.5 NuGet sürüm notları](../release-notes/nuget-1.5.md) | [1.7 NuGet sürüm notları](../release-notes/nuget-1.7.md)

NuGet 1.6 13 Aralık 2011'de yayınlanmıştır.

## <a name="known-installation-issue"></a>Bilinen yükleme sorunu
VS 2010 SP1 çalıştırıyorsanız, yüklü eski bir sürümü varsa, NuGet yükseltmeye çalışırken bir yükleme hata ile karşılaşabilirsiniz.

Geçici çözüm, yalnızca NuGet kaldırıp VS uzantısı Galeriden yükleyin sağlamaktır.  Bkz: [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) daha fazla bilgi için.

Not: Visual Studio (Kaldır düğmesi devre dışıdır) uzantıyı kaldırmak izin vermiyor olasılıkla "Yönetici olarak çalıştır" kullanarak Visual Studio'yu yeniden başlatmanız gerekir

## <a name="features"></a>Özellikler

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a>Semantic Versioning ve yayın öncesi paketleri için destek
NuGet 1.6 Semantic Versioning (SemVer) için destek sunuyor. SemVer kullanma hakkında ayrıntılı bilgi için okuma [sürüm belgeleri](../create-packages/prerelease-packages.md).

### <a name="using-nuget-without-checking-in-packages-package-restore"></a>NuGet paketleri (paket geri yükleme) denetlemeden kullanma
NuGet 1.6 artık hangi NuGet paketleri kaynak denetimine eklenmez ancak bunun yerine derleme zamanında eksikse geri yüklenir iş akışı için birinci sınıf desteğe sahiptir. Daha fazla bilgi edinmek için [NuGet paketleri kaynak denetimine yürüten olmadan kullanarak](../consume-packages/packages-and-source-control.md) konu.

### <a name="item-templates-that-install-nuget-packages"></a>NuGet paketlerini yükleme öğesi şablonları
Önceden yüklenmiş NuGet paketini Visual Studio Proje şablonları desteklemek için iş oluşturma, NuGet 1.6 ayrıca Visual Studio öğe şablonları için destek ekler. Öğe şablonları şablonda çağrıldığında, yüklü olan NuGet paketlerini ilişkili.

NuGet paketlerini yüklemek için bir proje/öğe şablon değiştirme hakkında daha fazla ayrıntı için okuma [Visual Studio şablonları paketlerinde](../visual-studio-extensibility/visual-studio-templates.md) konu.

### <a name="support-for-disabling-package-sources"></a>Paket kaynaklarını devre dışı bırakma desteği
Birden çok paket kaynaklarını yapılandırıldığında, NuGet paketleri için her biri bir paketi ve bağımlılıkları yükleme sırasında bakar. Herhangi bir nedenle NuGet ciddi bir şekilde yavaş aşağı doğru için kapalı bir paket kaynağı.

NuGet 1.6 önce paket kaynağı kaldırabilirsiniz, ancak ayrıntıları eklemek istediğiniz zaman geri anımsamak zorunda sonra.

NuGet 1.6 devre dışı bırakır, ancak geçici olarak saklamak için bir paket kaynağı işaretini verir.

![Bir paketi devre dışı bırakma](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a>Hata Düzeltmeleri
NuGet 1.6 106 toplam iş öğeleri sabit vardı. Bu 95 hataları olarak sınıflandırılan ve 10 bu özellikleri silindi.

Tam bir listesi için iş öğeleri NuGet 1.6 Lütfen görünümü sabit [bu sürüm için NuGet sorun İzleyicisi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
