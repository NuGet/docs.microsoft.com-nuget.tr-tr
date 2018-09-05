---
title: WebMatrix sürüm notları için NuGet 2.6.1
description: Bilinen sorunlar, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr WebMatrix için NuGet 2.6.1 için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 10d80a921cbc34b537f91644da97efc44530fa75
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550323"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a>WebMatrix sürüm notları için NuGet 2.6.1

[NuGet 2.6 sürüm notları](../release-notes/nuget-2.6.md) | [NuGet 2.7 Sürüm Notları](../release-notes/nuget-2.7.md)

NuGet takım, 26 Mart 2014'te WebMatrix için güncelleştirilmiş bir NuGet paket yöneticisini uzantısı yayımladı.  Bu güncelleştirme yüklenebilir [WebMatrix uzantı Galerisi](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) aşağıdaki adımları kullanarak:

1. WebMatrix 3'ı açın
1. Giriş şeridinde uzantıları simgesine tıklayın
1. Güncelleştirmeler sekmesini seçin.
1. 2.6.1 için NuGet Paket Yöneticisi güncelleştirmek için tıklayın
1. WebMatrix 3'ü yeniden başlatın ve kapatın

## <a name="notable-changes"></a>Önemli değişiklikler

Bu uzantı güncelleştirme adreslerini iki büyük sorunları kullanıcılar webmatrix'de alıcı NuGet paketlerini karşılaştığı.  İlk NuGet şema sürümü hatası ve ikinci sıfır bayt DLL'ler için önde gelen bir hatayı şeklindeydi `bin` klasör.

### <a name="nuget-schema-version-error"></a>NuGet şema sürümü hatası

WebMatrix 3'ü yayınlandıktan sonra yeni bir şema sürümüne yönelik NuGet paketlerini gerektiren NuGet içine yeni özellikler tanıtılmıştır.  NuGet paketlerinizi web sitenizi yönetmek çalışırken, bu yeni paketler Webmatrix'te gördüğünüz hatalara yol açabilir.

![Bir hata oluşmuştur. Şema sürümü uyumlu değil. Lütfen NuGet en son sürüme yükseltin.](./media/NuGet-2.8/webmatrix-schema-version.png)

Bu en son sürüm, bu hata oluşmasını engelliyor en yeni NuGet paketleri ile uyumluluk sağlar. Microsoft.AspNet.WebPages dahil olmak üzere paketlerin yeni sürümlerini Webmatrix'te artık yüklenebilir.  Bu paketler bazıları NuGet özellikleri gibi kullandığınız [XDT yapılandırma dönüşümleri](../release-notes/nuget-2.6.md#xdt), şimdiye kadar Webmatrix'te desteklenen değildi.

### <a name="zero-byte-dlls-in-bin-folder"></a>Bin klasörü sıfır bayt DLL'leri

NuGet yükleme depo, kopyalanmasını DLL'leri içermektedir Webmatrix'te DLL'leri Göster, paketleri sonra bazı kullanıcılar, bildirdiniz `bin` 0 bayt dosyalarıyla klasörde.  Bu uygulama çalışma zamanında keser.

[Bu sorunu](https://nuget.codeplex.com/workitem/4060) artık düzeltildi.

## <a name="other-recent-improvements"></a>Son diğer iyileştirmeler

Visual Studio için NuGet Paket Yöneticisi 2.8 yayımlandığında, WebMatrix için NuGet Paket Yöneticisi 2.5.0 de yayımlandı.  Bu içinde bahsedilen sırada [NuGet 2.8 sürüm notları](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), şu yeni özellikleri kullanıma sunulan bu güncelleştirmeyi belirli bahsetmek kaydetmedi.

### <a name="update-all"></a>Tümünü Güncelleştir

Ayrıca, tüm web sitenizin paketleri tek bir adımda şimdi güncelleştirebilirsiniz!  Webmatrix'te NuGet uzantısı açtığınızda, Galeri, yüklenenler ve güncelleştirmeleri kullanılabilir olanlarla tüm paketlerin listesi görürsünüz.  Daha önce her paket, ayrı ayrı olarak güncelleştirilmesi gerekir, ancak artık Güncelleştirmeler sekmesinde gösterilir kullanışlı bir "Tümünü Güncelleştir" düğmesi yoktur.

![Tüm kullanılabilir güncelleştirmeleri tüm paketleri güncelleştirmek için Güncelleştir'e tıklayın](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a>Varolan dosyaların üzerine yaz

Web sitenizdeki mevcut dosyaları içeren paketleri yüklerken, NuGet (varolan dosyalarınızı tek başına bırakarak) bu dosyaları her zaman sadece sessizce yoksaydı.  Bu, bir paket yüklenip yüklenmediğini veya doğru aslında bölümdü güncelleştirilmiş izlenim neden olabilir.  NuGet artık dosyaların üzerine için ister.

![Dosya çakışması çözümleme](./media/NuGet-2.8/webmatrix-overwrite-file.png)
