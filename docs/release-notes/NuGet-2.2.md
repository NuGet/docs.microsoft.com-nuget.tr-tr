---
title: NuGet 2.2 sürüm notları
description: NuGet bilinen sorunları, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr 2.2 için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a968ced3c58b7187a8bd9a8b14baa92f61f0140f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545998"
---
# <a name="nuget-22-release-notes"></a>NuGet 2.2 sürüm notları

[2.1 NuGet sürüm notları](../release-notes/nuget-2.1.md) | [2.2.1 NuGet sürüm notları](../release-notes/nuget-2.2.1.md)

NuGet 2.2 12 Aralık 2012 tarihinde yayınlanmıştır.

## <a name="visual-studio-quick-launch"></a>Visual Studio hızlı başlatma
Visual Studio 2012'de eklenen yeni özellikler biriydi [Hızlı Başlatma iletişim](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box). 2.2 NuGet Paket Yöneticisi iletişim kutusu içinde hızlı başlatma girdiğiniz arama terimi ile başlatmak izin bu iletişim kutusunu genişletir. Örneğin, 'jquery' içinde hızlı başlatma şimdi girerek bir seçeneği 'jquery' eşleşen NuGet paketleri aramak için sonuçları içerir.

![NuGet, Visual Studio hızlı başlatma](./media/quick-launch.png)

Bu seçeneğin belirlenmesi, standart NuGet Paket Yöneticisi arama deneyimi bir dönem 'jquery' başlatılır.

![Önceden doldurulmuş NuGet Paket Yöneticisi iletişim kutusu](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a>Paket içeriği için tüm klasörü belirtin
NuGet 2.2 artık klasörün tamamını belirtmenize olanak verir `<file>` öğesinin `.nuspec` tüm bu klasörün içeriğine dahil edilecek dosyası. Örneğin, aşağıdaki tüm betikler paketin betikleri klasöründe projeye paketi yüklendiğinde contents\scripts klasörüne eklenecek neden olur.

```xml
<file src="scripts\" target="content\scripts"/>
```

**6/24/16 güncelleştirin: "içerik" klasöründeki boş klasörler paketi yüklerken yoksayılır.**

## <a name="known-issues"></a>Bilinen Sorunlar

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a>Paket Yöneticisi konsolu kullanılırken F # projeleri için paket yüklemesi başarısız oluyor
Paket Yöneticisi konsolu kullanarak bir F # projesi bir NuGet paketi yüklemeye çalışırken, bir InvalidOperationException oluşturulur. Bu sorunu çözmek için F # ekip ile etkin olarak çalışıyoruz ancak bu arada, çözüm Konsolu yerine, NuGet Paket Yöneticisi iletişim kutusu aracılığıyla F # projeleri NuGet paketlerini yükleme olabilir. [Daha fazla bilgi Codeplex'te kullanılabilir](http://nuget.codeplex.com/workitem/2873).


## <a name="bug-fixes"></a>Hata Düzeltmeleri
NuGet 2.2 birçok hata düzeltmeleri içerir. Tam bir listesi için iş öğeleri NuGet 2.2 içinde lütfen görünümü sabit [bu sürüm için NuGet sorun İzleyicisi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
