---
title: NuGet 2.6.1 WebMatrix sürüm notları | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere WebMatrix için NuGet 2.6.1 için sürüm notları.
keywords: WebMatrix sürüm notları, hata düzeltmeleri ve bilinen sorunlar için NuGet 2.6.1 özellikleri, dcr ekledi
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 505054e42234f313bade496315e94ad485050dbb
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-261-for-webmatrix-release-notes"></a>NuGet 2.6.1 WebMatrix sürüm notları

[NuGet 2.6 sürüm notları](../release-notes/nuget-2.6.md) | [NuGet 2.7 Sürüm Notları](../release-notes/nuget-2.7.md)

NuGet takım güncelleştirilmiş bir NuGet Paket Yöneticisi uzantısı WebMatrix için 26 Mart 2014'te yayımladı.  Bu güncelleştirme yüklenebilir [WebMatrix uzantı Galerisi](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) aşağıdaki adımları kullanarak:

1. WebMatrix 3 açın
1. Giriş Şeritte uzantıları simgesine tıklayın
1. Güncelleştirmeler sekmesini seçin
1. 2.6.1 için NuGet Paket Yöneticisi güncelleştirmek için tıklatın
1. Kapatın ve WebMatrix 3 başlatın

## <a name="notable-changes"></a>Önemli değişiklikleri

En büyük sorunları kullanıcıların bu uzantı güncelleştirme adresini iki WebMatrix içindeki Süren NuGet paketleri karşılaştığı.  NuGet şeması sürüm hatası ilk ve ikinci sıfır bayt DLL'lerde önde gelen bir hata şeklindeydi `bin` klasör.

### <a name="nuget-schema-version-error"></a>NuGet şeması sürüm hatası

WebMatrix 3 yayımlandıktan yeni özellikler, yeni bir şema sürümüne yönelik NuGet paketlerini gerektiren NuGet içine tanıtılmıştır.  Web sitenizde NuGet paketlerinizi yönetmenizi çalışırken bu yeni paketleri Webmatrix'te gördüğünüz hatalara yol açabilir.

![Bir hata oluşmuştur. Şema sürümü uyumlu değil. Lütfen NuGet en son sürüme yükseltin.](./media/NuGet-2.8/webmatrix-schema-version.png)

Bu en son sürüm bu hata meydana gelmesini önleme yeni NuGet paketleri ile uyumluluk sağlar. Microsoft.AspNet.WebPages dahil olmak üzere paketleri yeni sürümleri artık Webmatrix'te yüklenebilir.  Bu paketleri bazıları NuGet özellikleri gibi kullandığınız [XDT config dönüştüren](../release-notes/nuget-2.6.md#xdt), şimdiye kadar Webmatrix'te desteklenen değildi.

### <a name="zero-byte-dlls-in-bin-folder"></a>Bin klasörü sıfır bayt DLL'leri

NuGet yükleme eklemek gözü için bu kopyalanan DLL'leri Webmatrix'te DLL'leri Göster içinde paketler sonra bazı kullanıcılar, raporladı `bin` klasörü 0 baytlık dosyaları olarak.  Bu uygulamanın çalışma zamanında keser.

[Bu sorunu](https://nuget.codeplex.com/workitem/4060) şimdi düzeltilmiştir.

## <a name="other-recent-improvements"></a>Son diğer geliştirmeler

Ayrıca, Visual Studio için NuGet Paket Yöneticisi 2.8 yayımlandığında, NuGet Paket Yöneticisi 2.5.0 WebMatrix için yayımladı.  Bu belirtilen sırada [NuGet 2.8 sürüm notları](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), biz belirli yeni özellikleri sunulan bu güncelleştirmeyi Bahsediyor alamadık.

### <a name="update-all"></a>Tümünü Güncelleştir

Tüm tek bir adımda, web sitenizin paketlerin şimdi güncelleştirebilirsiniz!  WebMatrix NuGet uzantısı açtığınızda Galerisi, yüklediyseniz ve kullanılabilir güncelleştirmeleri raporlarla tüm paketlerin listesini görürsünüz.  Daha önce her paketi tek tek güncelleştirilmesi gerekiyor ancak şimdi Güncelleştirmeler sekmesinde görüntülenir yararlı bir "Tümünü Güncelleştir" düğmesi yoktur.

![Tüm kullanılabilir güncelleştirmelerle tüm paketler güncelleştirmek için Güncelleştir'i tıklatın](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a>Var olan dosyaların üzerine yaz

Web sitenizde zaten mevcut dosyaların içeren paketleri yüklerken, NuGet (varolan dosyalarınızı tek başına bırakarak) bu dosyaları her zaman sadece sessizce yoksaydı.  Bu bir paket yüklenir veya doğru olduğunda aslında ancak değildi güncelleştirilmiş izlenim neden olabilir.  NuGet şimdi dosyaların üzerine yazılmasına ister.

![Dosya çakışma çözümü](./media/NuGet-2.8/webmatrix-overwrite-file.png)
