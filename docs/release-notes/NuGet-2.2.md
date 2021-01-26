---
title: NuGet 2,2 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 2,2 sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cc81d0ff53a5e8ac8b632a08c3cfe0b8b59c9bd7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780440"
---
# <a name="nuget-22-release-notes"></a>NuGet 2,2 sürüm notları

[NuGet 2,1 sürüm notları](../release-notes/nuget-2.1.md)  |  [NuGet 2.2.1 sürüm notları](../release-notes/nuget-2.2.1.md)

NuGet 2,2, 12 Aralık 2012 ' de yayımlanmıştır.

## <a name="visual-studio-quick-launch"></a>Visual Studio hızlı başlatma
Visual Studio 2012 ' de eklenen yeni özelliklerden biri [Hızlı başlatma iletişim kutusu](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box)idi. NuGet 2,2, bu iletişim kutusunu genişleterek Paket Yöneticisi iletişim kutusunu hızlı başlatmaya girilen arama koşullarına göre başlatabilir. Örneğin, hızlı başlatma ' ya ' jQuery ' girildiğinde, ' jQuery ' ile eşleşen NuGet paketlerini aramak için sonuçlara bir seçenek de eklenmiştir.

![Visual Studio hızlı başlatma 'da NuGet](./media/quick-launch.png)

Bu seçeneğin belirlenmesi, ' jQuery ' terimi için standart NuGet Paket Yöneticisi arama deneyimini başlatacaktır.

![Önceden doldurulmuş NuGet Paket Yöneticisi Iletişim kutusu](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a>Paket Içeriği için tüm klasörü belirt
NuGet 2,2, `<file>` `.nuspec` Bu klasörün tüm içeriğini dahil etmek için dosyanın öğesinde bir klasörün tamamını belirtmenizi sağlar. Örneğin, aşağıdaki, paket bir projeye yüklendiğinde paketin komut dosyaları klasöründeki tüm betiklerin contents\scripts klasörüne eklenmesine neden olur.

```xml
<file src="scripts\" target="content\scripts"/>
```

**Güncelleştirme 6/24/16: paket yüklenirken "içerik" klasöründeki boş klasörler yok sayılır.**

## <a name="known-issues"></a>Bilinen Sorunlar

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a>Paket Yöneticisi konsolu kullanılırken F # projeleri için paket yükleme başarısız oluyor
Paket Yöneticisi konsolunu kullanarak bir bir NuGet paketini F # projesine yüklemeye çalışırken bir InvalidOperationException atılır. Sorunu çözmek için F # ekibiyle etkin bir şekilde çalışıyoruz, ancak bu arada geçici çözüm, NuGet paketlerini konsol yerine NuGet 'in Paket Yöneticisi iletişim kutusu aracılığıyla F # projelerine yüklemektir. [CodePlex üzerinde daha fazla bilgi bulabilirsiniz](http://nuget.codeplex.com/workitem/2873).


## <a name="bug-fixes"></a>Hata Düzeltmeleri
NuGet 2,2 birçok hata düzeltmesi içerir. NuGet 2,2 ' de düzeltilen iş öğelerinin tam listesi için lütfen [Bu sürüm Için NuGet sorun İzleyicisi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)' ni görüntüleyin.
