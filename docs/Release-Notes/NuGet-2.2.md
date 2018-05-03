---
title: NuGet 2.2 sürüm notları
description: NuGet bilinen sorunları, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere 2.2 için sürüm notları.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 21f212de53da5faf1ec0762f97a840968b615b19
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-22-release-notes"></a>NuGet 2.2 sürüm notları

[NuGet 2.1 sürüm notları](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 sürüm notları](../release-notes/nuget-2.2.1.md)

NuGet 2.2 12 Aralık 2012'de serbest bırakıldı.

## <a name="visual-studio-quick-launch"></a>Visual Studio Hızlı Başlat
Visual Studio 2012'de eklenen yeni özellikler biri [Hızlı Başlatma iletişim](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box). NuGet 2.2 Hızlı Başlatma girilen arama terimlerini Paket Yöneticisi iletişim kutusu başlatılmaya izin vererek bu iletişim kutusunu genişletir. Örneğin, 'jquery' hızlı başlatma şimdi girerek bir seçenek 'jquery' ile eşleşen NuGet paketlerini arama sonuçlarında içerir.

![NuGet Visual Studio hızlı başlatma içinde](./media/quick-launch.png)

Bu seçeneğin belirlenmesi, standart NuGet Paket Yöneticisi arama deneyimi 'jquery' terim için başlatır.

![Önceden doldurulmuş haldedir NuGet Paket Yöneticisi iletişim kutusu](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a>Paket içeriği için tüm klasörü belirtin
NuGet 2.2 şimdi tüm bir klasörde belirtmenize olanak verir `<file>` öğesinin `.nuspec` tüm bu klasörün içeriğini içerecek şekilde dosya. Örneğin, aşağıdaki tüm betikler paket bir projeye yüklendiğinde contents\scripts klasörüne eklenecek paket betikleri klasöründeki neden olur.

```xml
<file src="scripts\" target="content\scripts"/>
```

**24/6/16 güncelleştirin: "içerik" klasöründeki boş klasörler paket yüklerken yoksayılır.**

## <a name="known-issues"></a>Bilinen Sorunlar

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a>Paket Yöneticisi konsolu kullanılırken F # projeleri için paket yükleme başarısız oluyor
Bir NuGet paketi Paket Yöneticisi konsolu kullanılarak bir F # projeye yüklemeye çalışırken, bir InvalidOperationException atılır. Bu sorunu çözmek için F # ekibi ile etkin olarak çalışıyoruz ancak bu arada, F # projelerine Konsolu yerine NuGet Paket Yöneticisi iletişim kutusu üzerinden NuGet paketlerini yüklemek için geçici bir çözüm değildir. [Daha fazla bilgi CodePlex üzerinde kullanılabilir](http://nuget.codeplex.com/workitem/2873).


## <a name="bug-fixes"></a>Hata Düzeltmeleri
NuGet 2.2 birçok hata düzeltmeleri içerir. İş tam listesi için öğeleri NuGet 2.2 Lütfen görünüm sabit [NuGet sorun İzleyicisi bu sürüm için](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).
