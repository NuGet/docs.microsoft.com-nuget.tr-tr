---
title: NuGet 1,6 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 1,6 sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 08b1cb3736e645d6efcc33f920f521c9c0fc7507
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777011"
---
 # <a name="nuget-16-release-notes"></a>NuGet 1,6 sürüm notları

[NuGet 1,5 sürüm notları](../release-notes/nuget-1.5.md)  |  [NuGet 1,7 sürüm notları](../release-notes/nuget-1.7.md)

NuGet 1,6, 13 Aralık 2011 tarihinde yayınlandı.

## <a name="known-installation-issue"></a>Bilinen yükleme sorunu
VS 2010 SP1 çalıştırıyorsanız, daha eski bir sürümü yüklüyse NuGet 'i yükseltmeye çalışırken yükleme hatası ile karşılaşabilirsiniz.

Geçici çözüm, NuGet 'i kaldırmak ve ardından VS uzantısı galerisinden yüklemek olacaktır.  Daha fazla bilgi edinmek için bkz. <https://support.microsoft.com/kb/2581019>.

Note: Visual Studio uzantıyı kaldırmanızı izin vermediğinden (kaldırma düğmesi devre dışıdır), büyük olasılıkla "yönetici olarak çalıştır" seçeneğini kullanarak Visual Studio 'Yu yeniden başlatmanız gerekir.

## <a name="features"></a>Özellikler

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a>Anlamsal sürüm oluşturma ve ön sürüm paketleri desteği
NuGet 1,6 anlam sürümü oluşturma (SemVer) için destek sunar. SemVer 'in nasıl kullanıldığı hakkında daha fazla bilgi için [sürüm oluşturma belgelerini](../create-packages/prerelease-packages.md)okuyun.

### <a name="using-nuget-without-checking-in-packages-package-restore"></a>Paketleri Iade etmeden NuGet kullanma (paket geri yükleme)
NuGet 1,6 artık, NuGet paketlerinin kaynak denetimine eklendiği iş akışı için birinci sınıf desteğe sahiptir, bunun yerine derleme zamanında geri yüklenir. Daha fazla ayrıntı için, [paketi kaynak denetimine kaydetmeden NuGet kullanma](../consume-packages/packages-and-source-control.md) konusunu okuyun.

### <a name="item-templates-that-install-nuget-packages"></a>NuGet paketlerini yükleyen öğe şablonları
Visual Studio proje şablonlarına önceden yüklenmiş NuGet paketini desteklemeye yönelik iş üzerinde oluşturma, NuGet 1,6, Visual Studio öğe şablonları için de destek ekler. Öğe şablonlarında, bir şablon çağrıldığında yüklenen ilişkili NuGet paketleri olabilir.

NuGet paketlerini yüklemek için bir proje/öğe şablonunu değiştirme hakkında daha fazla bilgi için, [Visual Studio şablonlarındaki paketler](../visual-studio-extensibility/visual-studio-templates.md) konusunu okuyun.

### <a name="support-for-disabling-package-sources"></a>Paket kaynaklarını devre dışı bırakma desteği
Birden çok paket kaynağı yapılandırıldığında, NuGet bir paket yükleme sırasında paketler için her birine bakar. Bir nedenden dolayı çalışan bir paket kaynağı, NuGet 'i ciddi ölçüde yavaşlatabilir.

NuGet 1,6 ' den önce, paket kaynağını kaldırabilir, ancak sonra geri eklemek istediğiniz zaman ayrıntılarını hatırlamanız gerekir.

NuGet 1,6, bir paket kaynağının devre dışı bırakılacağını kaldırmak, ancak geçici bir çözüm olmasını sağlar.

![Bir paketi devre dışı bırakma](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a>Hata Düzeltmeleri
NuGet 1,6, Toplam 106 iş öğesine sahipti. Bunlar hata olarak sınıflandırılmıştı ve bu özelliklerin 10 ' dur. 95

NuGet 1,6 ' de düzeltilen iş öğelerinin tam listesi için lütfen [Bu sürüm Için NuGet sorun İzleyicisi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)' ni görüntüleyin.
