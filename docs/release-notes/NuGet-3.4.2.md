---
title: NuGet 3.4.2 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 3.4.2 için sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6e6aa174582d059faa5bef9469cd83b19da51cf3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780254"
---
# <a name="nuget-342-release-notes"></a>NuGet 3.4.2 sürüm notları

[NuGet 3.4.1 sürüm notları](../release-notes/nuget-3.4.1.md)  |  [NuGet 3.4.3 sürüm notları](../release-notes/nuget-3.4.3.md)

NuGet 3.4.2, 3,4 Nisan 2016 ' de ve 3.4.1 sürümünde tanımlanan çeşitli sorunları gidermek için yayımlanmıştır.

## <a name="nugetexe-342-rc-is-now-available"></a>nuget.exe 3.4.2 RC artık kullanılabilir

nuget.exe 3.4.2 sürüm adayını [buradan](https://dist.nuget.org/index.html)indirebilirsiniz.

## <a name="updates-and-improvements"></a>Güncelleştirmeler ve geliştirmeler

* Belirli bir senaryoda güncelleştirmelerin performansını önemli ölçüde geliştirdik. Bu durumda, ayrıntılı bağımlılık grafiklerine sahip paketlerin güncelleştirmeleri gerçekten uzun zaman aldığı ve Visual Studio 'Yu askıya aldık.
* ağ trafiği olmayan NuGet geri yükleme işlemi, Visual Studio içinde 2,5 x-3x daha hızlıdır.
* Bu değişikliğe ek olarak, VS Kullanıcı arabirimindeki güncelleştirme sayısını alırken ağı iki kez vurduğumuz bir sorunu düzelttik. Bu, 3.4/3.4.1 ' de karşılaşılan bazı zaman aşımı sorunları için kısmen sorumludur.
* No_proxy ayarı için destek eklendi

## <a name="fixes"></a>Düzeltmeler

* 3.4.1 'e güncelleştirildikten sonra NuGet ayarlarında veya yapılandırmada nuget.org kaynağının bulunmadığı bir sorun düzeltildi.
* 3.4.1 sonlarının Artifactory içindeki Findpackagesbyıd 'e büyük küçük harf değişikliği sorunu düzeltildi.
* nuget.exe ile NuGet geri yükleme hatalarıyla kaynaklanan FIPS ile ilgili bir sorun düzeltildi.
* Geçersiz simge URL 'SI olan kaynaklara göz atarken kilitlenme düzeltildi.
* ' Tüm kaynaklar ' ile ilgili sürümleri ve girdileri birleştirmeye yönelik sorunlar düzeltildi.

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a>3.4.2 Windows x86 komut satırı 'nda (RC) bilinen sorunlar

Bu sorunlar, RTM 'ye vurmadan önce sonraki haftada bir daha erken düzeltilecektir.

*  Çözüm dosyası proje dosyalarından daha düşük bir klasör hiyerarşisine yerleştirilirse çözüm üzerinde NuGet geri yükleme çalıştırmak başarısız olur.
*  V2 akışını kullanan bir pakette NuGet Delete komutunun çalıştırılması başarısız olur. Bunun yerine v3 akışını kullanın.


Bu sürümdeki düzeltmelerin ve geliştirmelerin tüm listesi için [buradaki](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+)sorun listesini inceleyin.