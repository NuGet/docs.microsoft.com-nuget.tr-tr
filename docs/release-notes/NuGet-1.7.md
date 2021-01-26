---
title: NuGet 1,7 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 1,7 sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 50eb326c5ada4f74685b07c0d1b0f84b14e547ac
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777073"
---
# <a name="nuget-17-release-notes"></a>NuGet 1,7 sürüm notları

[NuGet 1,6 sürüm notları](../release-notes/nuget-1.6.md)  |  [NuGet 1,8 sürüm notları](../release-notes/nuget-1.8.md)

NuGet 1,7, 4 Nisan 2012 ' de yayımlanmıştır.

## <a name="known-installation-issue"></a>Bilinen yükleme sorunu
VS 2010 SP1 çalıştırıyorsanız, daha eski bir sürümü yüklüyse NuGet 'i yükseltmeye çalışırken yükleme hatası ile karşılaşabilirsiniz.

Geçici çözüm, NuGet 'i kaldırmak ve ardından VS uzantısı galerisinden yüklemek olacaktır.  Daha fazla bilgi edinmek için bkz. <https://support.microsoft.com/kb/2581019>.

Note: Visual Studio uzantıyı kaldırmanızı izin vermediğinden (kaldırma düğmesi devre dışıdır), büyük olasılıkla "yönetici olarak çalıştır" seçeneğini kullanarak Visual Studio 'Yu yeniden başlatmanız gerekir.

## <a name="features"></a>Özellikler

### <a name="support-opening-readmetxt-file-after-installation"></a>Yüklemeden sonra readme.txt dosyası açmayı destekleme
1,7 ' de yeni, paketiniz `readme.txt` paketin kökünde bir dosya içeriyorsa, bu dosya paketinizi yükleme bittikten sonra otomatik olarak bu dosyayı açar.

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a>NuGet Paketlerini Yönet iletişim kutusunda yayın öncesi paketleri göster
NuGet Paketlerini Yönet iletişim kutusu artık, ön sürüm paketlerini gösterme seçeneği sağlayan bir açılan menü içerir.

![Ön sürüm paketleri gösteriliyor](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a>Paket dosyaları eksik olduğunda paket geri yükleme düğmesini göster
Paket Yöneticisi konsolunu veya yönetici NuGet paketleri iletişim kutusunu açtığınızda, NuGet geçerli çözümün paket geri yükleme modunu etkinleştirmiştir ve klasörde herhangi bir paket dosyası eksikse, bu çözüm denetlenir `packages` . Bu iki koşul karşılanıyorsa, NuGet size bildirimde bulunur ve uygun bir geri yükleme düğmesi gösterir. Bu düğmeye tıkladığınızda, tüm eksik paketleri geri yüklemek için NuGet tetiklenecek.

![İletişim kutusunda paket geri yükleme düğmesi](./media/packagerestore-dialog.png)

![Konsolda paket geri yükleme düğmesi](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a>Çözüm düzeyi packages.config dosyası Ekle
NuGet 'in önceki sürümlerinde her proje, `packages.config` Bu projeye hangi NuGet paketlerinin yüklendiğini izleyen bir dosya içerir. Ancak çözüm düzeyinde çözüm düzeyinde paketleri izlemek için benzer bir dosya yoktu. Sonuç olarak, çözüm düzeyi paketleri geri yüklemenin bir yolu yoktu.
Bu özellik artık NuGet 1,7 ' de uygulanır. Çözüm düzeyi dosya, `packages.config` `.nuget` çözüm kökü altındaki klasörün altına yerleştirilir ve yalnızca çözüm düzeyi paketleri depolar.

### <a name="remove-new-package-command"></a>New-Package komutu kaldır
Düşük kullanım nedeniyle New-Package komutu kaldırılmıştır. Geliştiricilerin, paketler oluşturmak için nuget.exe veya yararlı NuGet paket Gezginini kullanması önerilir.

## <a name="bug-fixes"></a>Hata Düzeltmeleri
NuGet 1,7, paket geri yükleme iş akışı ve ağ/kaynak denetimi senaryolarında birçok hatayı düzeltti.

NuGet 1,7 ' de düzeltilen iş öğelerinin tam listesi için lütfen [Bu sürüm Için NuGet sorun İzleyicisi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)' ni görüntüleyin.
