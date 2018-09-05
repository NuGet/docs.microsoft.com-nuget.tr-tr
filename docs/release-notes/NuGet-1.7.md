---
title: NuGet 1.7 Sürüm Notları
description: NuGet bilinen sorunları, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr 1.7 için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 07cd541ef215d2a1bacc45995a22dadb6dfeac6d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551473"
---
# <a name="nuget-17-release-notes"></a>NuGet 1.7 Sürüm Notları

[1.6 NuGet sürüm notları](../release-notes/nuget-1.6.md) | [1.8 NuGet sürüm notları](../release-notes/nuget-1.8.md)

NuGet 1.7 4 Nisan 2012 tarihinde yayınlanmıştır.

## <a name="known-installation-issue"></a>Bilinen yükleme sorunu
VS 2010 SP1 çalıştırıyorsanız, yüklü eski bir sürümü varsa, NuGet yükseltmeye çalışırken bir yükleme hata ile karşılaşabilirsiniz.

Geçici çözüm, yalnızca NuGet kaldırıp VS uzantısı Galeriden yükleyin sağlamaktır.  Bkz: [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) daha fazla bilgi için.

Not: Visual Studio (Kaldır düğmesi devre dışıdır) uzantıyı kaldırmak izin vermiyor olasılıkla "Yönetici olarak çalıştır" kullanarak Visual Studio'yu yeniden başlatmanız gerekir

## <a name="features"></a>Özellikler

### <a name="support-opening-readmetxt-file-after-installation"></a>Yükleme sonrasında Readme.txt dosyasını açma desteği
Paketiniz varsa 1.7, yeni bir `readme.txt` dosyası NuGet paket kökünde otomatik olarak açılır bu dosya, paket yükleme tamamlandıktan sonra.

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a>Manage NuGet paketleri iletişim kutusunda yayın öncesi paketleri Göster
NuGet paketlerini Yönet iletişim kutusunda yayın öncesi paketleri göstermek için seçeneği sağlayan bir açılan artık içerir.

![Yayın öncesi paketleri gösteriliyor](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a>Paket dosyaları eksik olduğunda, paket geri düğmesini göster
Paket Yöneticisi konsolu veya iletişim Yöneticisi NuGet paketleri, NuGet geçerli çözüm paket geri yükleme modu etkin olmadığını denetler ve herhangi bir paket dosyaları eksik olması durumunda `packages` klasör. Bu iki koşul karşılanıyorsa, NuGet size bildirir ve uygun bir Ekranı Kapla düğmesini gösterir. Bu düğmeye tıklandığında, tüm eksik paketleri geri yüklemek için NuGet tetikler.

![İletişim kutusundaki paket Geri Yükle düğmesi](./media/packagerestore-dialog.png)

![Konsolunda paket Geri Yükle düğmesi](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a>Çözüm düzeyinde packages.config dosyası ekleme
NuGet önceki sürümlerinde, her proje içeren bir `packages.config` dosyasını o proje içinde NuGet paketleri yüklü izler. Ancak, çözüm düzeyinde paketlerini izlemek için çözüm düzeyinde benzer dosya vardı. Sonuç olarak, çözüm düzeyinde paketlerini geri yüklemek için hiçbir yolu yoktu.
Bu özellik artık NuGet 1.7 içinde uygulanır. Çözüm düzeyinde `packages.config` dosya altına yerleştirilir `.nuget` klasörü altında çözüm kök ve yalnızca çözüm düzeyinde paketleri depolar.

### <a name="remove-new-package-command"></a>New-Package komutunu Kaldır
Düşük kullanım nedeniyle, New-Package komutu kaldırıldı. Geliştiriciler, nuget.exe veya kullanışlı NuGet paket Gezgini, paket oluşturmak üzere kullanmak için önerilir.

## <a name="bug-fixes"></a>Hata Düzeltmeleri
NuGet 1.7 paket geri yükleme iş akışı ve ağ/kaynak denetimi senaryoları birçok hataları düzeltmiştir.

Tam bir listesi için iş öğeleri NuGet 1.7 Lütfen görünümü sabit [bu sürüm için NuGet sorun İzleyicisi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
