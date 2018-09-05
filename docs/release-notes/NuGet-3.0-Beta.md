---
title: NuGet 3.0 Beta sürüm notları
description: NuGet 3.0 bilinen sorunları, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr Beta için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 9f9fec6a1af8dfbcfdcfa05a301ff52409521228
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550919"
---
# <a name="nuget-30-beta-release-notes"></a>NuGet 3.0 Beta sürüm notları

[NuGet 3.0 Önizleme sürüm notları](../release-notes/nuget-3.0-preview.md) | [NuGet 3.0 RC sürüm notları](../release-notes/nuget-3.0-rc.md)

NuGet 3.0 Beta 23 Şubat 2015'te Visual Studio 2015 CTP 6 sürümüyle yayımlanmıştır. Bu sürümdeki birkaç paylaşmak için mimarisi ve performans iyileştirmeleri sunuyoruz ve nuget.org hizmetimiz Performans Ayarları'nı başlatmak heyecan duyuyoruz ekibimize, çok anlamına gelir.

Bu yeni sürümü yüklemeden önce Visual Studio 2015 için NuGet uzantısı herhangi bir önceki sürümünü kaldırmanız önerilir.  Bu sürüm uzantının herhangi bir sorun varsa, dönmek için öneririz [önceki sürümünü](http://nuget.codeplex.com/downloads/get/909582) Visual Studio 2015 önizlemesi ile kullanmak için.

## <a name="visual-studio-2012"></a>Visual Studio 2012+

Bu NuGet 3.0 Beta, Visual Studio 2015 CTP 6 uzantısı galeride yüklemek kullanılabilir. Önizleme düşme Visual Studio 2012 ve Visual Studio 2013 için çok yakında ulaşmak için çalışıyoruz. Biz Amacımız için daha önce paylaşılan [Visual Studio 2010 için güncelleştirmeleri bulunmayarak](http://blog.nuget.org/20141002/visual-studio-2010.html), ve biz zor kararı yaptı.

## <a name="new-clientserver-api"></a>Yeni istemci/sunucu API

Biz NuGet'ın istemci/sunucu protokolü için bazı uygulama ayrıntıları üzerinde yoğun çalışmalar. Yaptığımız iş "API v3" için paket geri yükleme ve paketlerin yüklenmesi gibi kritik senaryolar için yüksek kullanılabilirlik geçici olarak tasarlanmış olan NuGet oluşturmaktır. Yeni API REST üzerinde temel alır ve iletilir ve seçtiğiniz [JSON-LD](http://json-ld.org) bizim kaynak biçimi olarak.

NuGet 3.0 Beta bitler, paket kaynak açılır menüde "api.nuget.org" adlı yeni bir paket kaynağı bakın.   Bu paket kaynağını seçerseniz, yeni API'mizi yerine nuget.org için bağlanmak için kullanacağız. NuGet 3.0 rc'de Yenilik olarak, bu yeni API v3 tabanlı paket kaynağı v2 tabanlı "nuget.org" Paket kaynağı yerini alır.  Biz, tüm diğer genel paket kaynakları devre dışı bırakılması önerilir ve yalnızca api.nuget.org, yalnızca genel Paket Deposu bırakın.

Biz, çok zaman v3 API'mizi oluşturmamızı yerleştirdiğiniz ve genel deponun erişmek isteyen eski istemciler için standart v2 API'si sürdürmek devam eder.

## <a name="updated-ui"></a>Güncelleştirilmiş kullanıcı Arabirimi

Bu sürümde, paket ile gerçekleştirilecek bir eylem seçmenizi sağlayacak ve ekranın seçenekleri alanını onay kutusu içine Önizleme düğmesini geçirileceğini combobox'ı dahil etmek için kullanıcı arabirimi geliştirdik.  Seçenekler alanı artık daraltılabilir ve artık kullanılabilir seçenekleri açıklayan bir Yardım bağlantısını sağlar.

![Yeni NuGet kullanıcı Arabirimi](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a>İşlem günlüğü

Kalıcı pencere ile hızlıca görünür ve yükleme veya kaldırma Gizle günlük bilgileri kaldırdık.  Bu pencere bilgi veya kopyalayabilir ve yapıştırabilirsiniz istediğinizden emin hiçbir değer eklenmesi.  Bunun yerine, biz artık tüm çıkış penceresi Paket Yöneticisi bölmesine günlüğü çıktının yönlendireceğiniz.  Bu daha rahat ve incelemek istediğiniz bir tipik yapı rapora benzer düşünüyoruz.


### <a name="focus-on-performance"></a>Performans üzerinde odaklanın

Çok sayıda NuGet aramalar ve getirmeler performansını iyileştirme adını değişiklikler yaptık.  Bu bizim bir numaralı önemli müşterilerimiz oldu ve emin olmak için Biz bu sürümde giderilen istedik.  Size yeni bir CDN yerleşik sunucularımızı ayarlanmış yaptım ve eşleştirme mantığını Umarım daha ilgili size sunmak için sorgu geliştirilmiş ve daha hızlı paket arama sonuçları.

Biz bu NuGet 3.0 geliştirme aşamasında devam ederken eder ayarlama ve size geliştirilmiş bir deneyim sunmak sağlamak nuget.org hizmetini izleme.  Biz değil kapalı kalma süresi, etkileşim kurmak planlama ancak ekleme ve hizmet kaynakları değiştirme.  Gözünüzü bizim [twitter akışı](http://twitter.com/nuget) biz hizmet yapılandırmasını değiştirdiğinizde ilişkin ayrıntılar için.

## <a name="building-nuget-with-nuget"></a>NuGet ile yapı NuGet

Biz artık NuGet müşterilerimizin kendilerini NuGet paketlerine oluşturulmakta olan çeşitli bileşenleri içine rearchitected. Bu yeniden kullanımını kendi kitaplıkları, yeniden kullanılabilir ve düzgün şekilde paketlenmesi bileşenleri oluşturmak için bize zorlar.  Yinelenen kodu ortadan kaldırarak kodlama işini daha iyi geliştirme sürecimiz Çözümlerimiz boyunca paketleri oluşturmak için gereken destekleyecek şekilde yapılandırmak nasıl ölçeklendireceğini öğrendi da mümkün olmuştur.  Burada size kod projelerini nasıl yapılandırılmıştır ve bizim yapı işleminin nasıl çalıştığı hakkında konuşur yakında bir blog gönderisine bakın.

## <a name="stay-tuned"></a>Bizi izlemeye devam edin

Lütfen gözünüzü [blogumuzu](http://blog.nuget.org) daha fazla ilerleme ve NuGet 3.0 duyuruları!
