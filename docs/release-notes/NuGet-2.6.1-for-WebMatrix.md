---
title: WebMatrix için NuGet 2.6.1 sürüm notları
description: ", Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil, WebMatrix için NuGet 2.6.1 sürüm notları."
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: de568829efd5060f3b02c3129ccfee2b27782821
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780426"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a>WebMatrix için NuGet 2.6.1 sürüm notları

[NuGet 2,6 sürüm notları](../release-notes/nuget-2.6.md)  |  [NuGet 2,7 sürüm notları](../release-notes/nuget-2.7.md)

NuGet ekibi, 26 Mart 2014 ' de WebMatrix için güncelleştirilmiş bir NuGet Paket Yöneticisi uzantısı yayımlamıştır.  Bu güncelleştirme, aşağıdaki adımlar kullanılarak [WebMatrix uzantı galerisinden](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) yüklenebilir:

1. WebMatrix 'i aç 3
1. Giriş şeridinde uzantılar simgesine tıklayın
1. Güncelleştirmeler sekmesini seçin
1. NuGet paket yöneticisini 2.6.1 olarak güncelleştirmek için tıklayın
1. WebMatrix 'i kapat ve yeniden Başlat 3

## <a name="notable-changes"></a>Önemli değişiklikler

Bu uzantı güncelleştirme, kullanıcıların WebMatrix içinde NuGet paketleri tüketen karşılaştığı en büyük sorunlardan ikisi ele alır.  Birincisi bir NuGet şema sürümü hatasıdır ve ikincisi, klasördeki sıfır baytlık dll 'Ler için bir hata ile önde gelen bir hatadır `bin` .

### <a name="nuget-schema-version-error"></a>NuGet şema sürümü hatası

WebMatrix 3 yayınlandığından, NuGet paketleri için yeni bir şema sürümü gerektiren NuGet 'e yeni özellikler eklenmiştir.  Web sitenizde NuGet paketlerinizi yönetmeye çalışırken, bu yeni paketler WebMatrix 'te gördüğünüz hatalara yol açabilir.

![Bir hata oluşmuştur. Şema sürümü uyumsuz. Lütfen NuGet 'i en son sürüme yükseltin.](./media/NuGet-2.8/webmatrix-schema-version.png)

Bu en yeni sürüm en yeni NuGet paketleriyle uyumluluk sağlar ve bu hatanın oluşmasını önler. Microsoft. AspNet. Web sayfaları da dahil olmak üzere paketlerin yeni sürümleri, artık WebMatrix 'e yüklenebilir.  Bu paketlerin bazıları, artık WebMatrix 'te desteklenmeyen [xdt yapılandırma dönüştürmeleri](../release-notes/nuget-2.6.md#xdt)gibi NuGet özelliklerini kullanıyor.

### <a name="zero-byte-dlls-in-bin-folder"></a>Bin klasöründe Zero-Byte dll 'Leri

Bazı kullanıcılar, bin 'e kopyalanan dll 'Leri içeren WebMatrix 'e NuGet paketleri yükledikten sonra, dll 'Lerin `bin` klasörde 0 baytlık dosyalar olarak görünür olduğunu raporladı.  Bu, çalışma zamanında uygulamayı keser.

[Bu sorun](https://nuget.codeplex.com/workitem/4060) artık düzeltildi.

## <a name="other-recent-improvements"></a>Diğer son geliştirmeler

NuGet Paket Yöneticisi 2,8, Visual Studio için yayınlandığında, WebMatrix için NuGet Paket Yöneticisi 2.5.0 de yayımlandık.  Bu, [NuGet 2,8 sürüm notlarında](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates)bahsedilirken, bu güncelleştirmenin tanıtılmasıyla ilgili yeni özelliklerden bahsetmedik.

### <a name="update-all"></a>Tümünü Güncelleştir

Artık tüm Web sitenizin paketlerini tek bir adımda güncelleştirebilirsiniz!  NuGet uzantısını WebMatrix 'te açtığınızda, galerideki tüm paketlerin listesini, yüklü olanları ve güncelleştirmeleri kullanılabilir olanları görürsünüz.  Daha önce her paketin ayrı ayrı güncelleştirilmesi gerekir, ancak artık Güncelleştirmeler sekmesinde görüntülenen faydalı bir "Tümünü Güncelleştir" düğmesi vardır.

![Tüm paketleri kullanılabilir güncelleştirmelerle güncelleştirmek için Tümünü Güncelleştir ' e tıklayın](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a>Varolan dosyaların üzerine yaz

Web sitenizde zaten var olan dosyaları içeren paketleri yüklerken, NuGet bu dosyaları her zaman sessizce yok saymıştır (var olan dosyaları tek başına bırakır).  Bu, aslında bir paketin yüklenmiş veya aslında doğru şekilde güncelleştirildiği izlenimi ortaya çıkmasına neden olabilir.  NuGet artık dosyaların üzerine yazılmasını ister.

![Dosya çakışması çözümü](./media/NuGet-2.8/webmatrix-overwrite-file.png)
