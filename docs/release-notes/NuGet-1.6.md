---
title: NuGet 1.6 sürüm notları
description: NuGet bilinen sorunları, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere 1.6 için sürüm notları.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0345e180893a56302385d27792c4e15ba5d96989
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820605"
---
 # <a name="nuget-16-release-notes"></a>NuGet 1.6 sürüm notları

[NuGet 1.5 sürüm notları](../release-notes/nuget-1.5.md) | [NuGet 1.7 Sürüm Notları](../release-notes/nuget-1.7.md)

NuGet 1.6 13 Aralık 2011'de serbest bırakıldı.

## <a name="known-installation-issue"></a>Bilinen yükleme sorunu
VS 2010 SP1 çalıştırıyorsanız, yüklü eski bir sürüm varsa, NuGet yükseltmeye çalışırken yükleme hatayla karşılaşabilirsiniz.

Yalnızca NuGet kaldırın ve VS uzantısı Galeriden yükleyin için geçici bir çözüm değildir.  Bkz: [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) daha fazla bilgi için.

Not: Visual Studio (Kaldır düğmesi devre dışıdır) uzantısını Kaldır izin vermiyor olasılıkla "Yönetici olarak çalıştır" kullanarak Visual Studio yeniden başlatmanız gerekir

## <a name="features"></a>Özellikler

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a>Anlamsal sürüm oluşturma ve ön sürüm paketlerini desteği
NuGet 1.6 anlamsal sürüm oluşturma (SemVer) için destek sunar. SemVer kullanma hakkında daha fazla ayrıntı için okuma [sürüm belgeleri](../create-packages/prerelease-packages.md).

### <a name="using-nuget-without-checking-in-packages-package-restore"></a>NuGet paketleri (paket geri yükleme) denetlemeden kullanma
NuGet 1.6 artık hangi NuGet içinde paketler için kaynak denetimi eklenmez, ancak bunun yerine derleme zamanında eksikse geri iş akışı için birinci sınıf desteğe sahiptir. Daha fazla ayrıntı için okuma [kullanarak paketler için kaynak denetimi yürüten olmadan NuGet](../consume-packages/packages-and-source-control.md) konu.

### <a name="item-templates-that-install-nuget-packages"></a>NuGet paketi yüklemesi öğe şablonları
Visual Studio Proje şablonları için önceden yüklenmiş NuGet paketi desteklemek için iş oluşturma, NuGet 1.6 de Visual Studio öğe şablonları için destek ekler. Öğe şablonları şablonda çağrıldığında, yüklü olan NuGet paketlerini ilişkili.

NuGet paketlerini yüklemek için bir proje/öğesi şablonu değiştirme hakkında daha fazla ayrıntı için okuma [Visual Studio şablonları paketlerinde](../visual-studio-extensibility/visual-studio-templates.md) konu.

### <a name="support-for-disabling-package-sources"></a>Paket kaynaklarını devre dışı bırakma desteği
Birden çok paket kaynaklarını yapılandırıldığında, NuGet paketleri için her biri bir paketi ve bağımlılıklarını yüklenmesi sırasında bakar. Herhangi bir nedenle ciddi bir şekilde yavaş NuGet aşağı için kapalı bir paket kaynağı.

NuGet 1.6 önce paket kaynağı kaldırabilirsiniz, ancak ardından eklemek istediğiniz zaman ilgili ayrıntıları geri anımsamak zorunda.

NuGet 1.6 devre dışı bırakın, ancak geçici kalmasını sağlamak için bir paket kaynağı işaretini kaldırdığınızda sağlar.

![Bir paket devre dışı bırakma](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a>Hata Düzeltmeleri
NuGet 1.6 iş öğeleri sabit 106 toplam vardı. Bu 95 hataları sınıflandırılan ve bu 10 özellikleri silindi.

Tam bir listesi için iş öğeleri NuGet 1.6 Lütfen görünüm sabit [NuGet sorun İzleyicisi bu sürüm için](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
