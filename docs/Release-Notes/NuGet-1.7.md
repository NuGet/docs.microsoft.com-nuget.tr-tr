---
title: NuGet 1,7 Sürüm Notları
description: NuGet bilinen sorunları, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere 1.7 için sürüm notları.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 81db81642ac21b7dd41f5940dfba919d0871ec01
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-17-release-notes"></a>NuGet 1,7 Sürüm Notları

[NuGet 1.6 sürüm notları](../release-notes/nuget-1.6.md) | [NuGet 1.8 sürüm notları](../release-notes/nuget-1.8.md)

NuGet 1.7 4 Nisan 2012'de serbest bırakıldı.

## <a name="known-installation-issue"></a>Bilinen yükleme sorunu
VS 2010 SP1 çalıştırıyorsanız, yüklü eski bir sürüm varsa, NuGet yükseltmeye çalışırken yükleme hatayla karşılaşabilirsiniz.

Yalnızca NuGet kaldırın ve VS uzantısı Galeriden yükleyin için geçici bir çözüm değildir.  Bkz: [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) daha fazla bilgi için.

Not: Visual Studio (Kaldır düğmesi devre dışıdır) uzantısını Kaldır izin vermiyor olasılıkla "Yönetici olarak çalıştır" kullanarak Visual Studio yeniden başlatmanız gerekir

## <a name="features"></a>Özellikler

### <a name="support-opening-readmetxt-file-after-installation"></a>Yükleme sonrasında Readme.txt dosyası açılırken desteği
Paketiniz varsa 1.7, yeni bir `readme.txt` dosyası NuGet paketi kökünde otomatik olarak açılır bu dosya, paket yükleme tamamlandıktan sonra.

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a>Manage NuGet paketlerini iletişim kutusundaki ön sürüm paketlerini Göster
NuGet paketlerini Yönet iletişim kutusu artık ön sürüm paketlerini göstermek için seçeneği sağlayan bir açılır içerir.

![Ön sürüm paketlerini gösterme](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a>Paket dosyaları eksik olduğunda paket geri düğmesini göster
Paket Yöneticisi Konsolu'nu açın veya iletişim Yöneticisi NuGet paketleri, NuGet geçerli çözümü paket geri yükleme modu etkin olmadığını denetler ve paket dosyaları eksik olması durumunda `packages` klasör. Bu iki koşul karşılanıyorsa NuGet size bildirir ve uygun Geri Yükle düğmesi gösterilir. Bu düğmeye tıkladığınızda, tüm eksik paketleri geri yüklemek için NuGet tetikler.

![İletişim kutusundaki paket Geri Yükle düğmesi](./media/packagerestore-dialog.png)

![Konsolunda paket Geri Yükle düğmesi](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a>Çözüm düzeyi packages.config dosyasına Ekle
NuGet önceki sürümlerinde her proje içeren bir `packages.config` bu projede yüklü hangi NuGet paketlerini izler dosya. Ancak, çözüm düzeyi paketleri izlemek için çözüm düzeyinde benzer dosya vardı. Sonuç olarak, çözümü düzeyi paketlerini geri yüklemek için hiçbir yolu yoktu.
Bu özellik artık NuGet 1.7 uygulanır. Çözüm düzeyi `packages.config` dosya altında yerleştirilir `.nuget` çözüm altında klasör kök ve yalnızca çözüm düzeyi paketleri depolar.

### <a name="remove-new-package-command"></a>Yeni paket komutu kaldırın
Düşük kullanım nedeniyle, yeni paketi komutu kaldırılmıştır. Geliştiriciler, nuget.exe ya da kullanışlı NuGet paketi Gezgini'nden paketleri oluşturmak üzere kullanmak için önerilir.

## <a name="bug-fixes"></a>Hata Düzeltmeleri
NuGet 1.7 birçok ağ/kaynak denetimi senaryoları ve paket geri yükleme iş akışını geçici düzeltilen.

Tam bir listesi için iş öğeleri NuGet 1.7 Lütfen görünüm sabit [NuGet sorun İzleyicisi bu sürüm için](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
