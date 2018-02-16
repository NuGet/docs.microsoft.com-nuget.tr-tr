---
title: "NuGet 3.0 Beta sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere NuGet 3.0 Beta için sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 3.0 Beta sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3a595d002e385ff0330c2eebd0e8439f5dbefbd9
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/14/2018
---
# <a name="nuget-30-beta-release-notes"></a>NuGet 3.0 Beta sürüm notları

[NuGet 3.0 Preview sürüm notları](../release-notes/nuget-3.0-preview.md) | [NuGet 3.0 RC sürüm notları](../release-notes/nuget-3.0-rc.md)

NuGet 3.0 Beta 23 Şubat 2015 tarihinde Visual Studio 2015 CTP 6 sürümü için yayımlanmıştır. Bu sürüm paylaşmak için Mimari ve performans geliştirmeleri sayısı sahibiz ve performans ayarlarını nuget.org hizmetimizi ayarlama yapmaya başlamak üzere Çoğalması ki ekibimiz için çok anlamına gelir.

Bu yeni sürümü yüklemeden önce NuGet Visual Studio 2015 uzantısı'nın herhangi bir önceki sürümünü kaldırmanız önerilir.  Uzantısı'nın bu sürümü ile herhangi bir sorun varsa, geri dönmek için önerilir [önceki sürüm](http://nuget.codeplex.com/downloads/get/909582) Visual Studio 2015 preview ile kullanım için.

## <a name="visual-studio-2012"></a>Visual Studio 2012+

Bu NuGet 3.0 Beta Visual Studio 2015 CTP 6 uzantısı Galerisi'nde yüklemek kullanılabilir. Önizleme düşme Visual Studio 2012 ve Visual Studio 2013 için çok yakında ulaşmak için çalışıyoruz. Bizim hedefi daha önce paylaşılmıştı [Visual Studio 2010 için güncelleştirmeleri Durdur](http://blog.nuget.org/20141002/visual-studio-2010.html), ve zor kararı vermiyoruz.

## <a name="new-clientserver-api"></a>Yeni istemci/sunucu API'si

Biz NuGet istemci/sunucu protokolü için bazı uygulama ayrıntılarını çalışmakta. Biz yaptığınız işi "API v3" için paket geri yüklemesi ve paketlerin yüklenmesi gibi kritik senaryolar için yüksek kullanılabilirlik geçici tasarlanmış NuGet oluşturmaktır. Yeni API REST üzerinde temel alır ve iletilir ve biz seçtiğiniz [JSON-LD](http://json-ld.org) bizim kaynak biçiminde.

NuGet 3.0 Beta bitleri paket kaynağı açılır listede "api.nuget.org" adlı yeni bir paket kaynağı bakın.   Bu paket kaynağını seçerseniz, yeni API'mize yerine nuget.org için bağlanmak için kullanacağız. NuGet 3.0 RC'de bu yeni API v3 tabanlı paket kaynağı v2 tabanlı "nuget.org" Paket kaynağı yerini alır.  Biz, tüm diğer ortak paket kaynaklarını devre dışı bırakılması önerilir ve yalnızca api.nuget.org, yalnızca genel Paket Deposu bırakın.

Biz çok zaman v3 API'mize oluşturmakla yerleştirdiğiniz ve genel depo erişmek isteyen eski istemcileri için standart v2 API sürdürmek devam eder.

## <a name="updated-ui"></a>Güncelleştirilmiş kullanıcı Arabirimi

Biz bu sürümde paket ile gerçekleştirilecek bir eylem seçmenizi sağlar ve bir onay ekranı seçenekleri alanı içine Önizleme düğmesini geçti combobox dahil etmek için kullanıcı arabirimi Gelişmiş.  Seçenekler alanı artık daraltılabilir ve artık kullanılabilir seçenekleri açıklayan bir Yardım bağlantısını sağlar.

![Yeni NuGet kullanıcı Arabirimi](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a>İşlem günlüğü

Biz, hızlı bir şekilde görünür ve yükleme veya kaldırma sırasında gizleme günlük bilgileri ile kalıcı pencere kaldırıldı.  Bu pencere hiçbir değer eklenmesi veya ondan kopyalayıp kurabilmesi bilgileri görmek gerçekten istiyor.  Bunun yerine, biz şimdi tüm çıktı penceresi Paket Yöneticisi bölmesine günlüğü çıkış yönlendireceğiniz.  Bu daha rahat ve incelemek istediğiniz bir tipik yapı raporuna benzer biçimde düşünün.


### <a name="focus-on-performance"></a>Performans üzerinde odaklanmak

Biz çok NuGet arar ve öğesinden performansını iyileştirme adına değişiklikler yaptınız.  Bu müşterilerimizden bizim numara bir sorun oluştu ve biz emin olmak için size bu sürümde ele istedik.  Yeni bir CDN yerleşik sunucularımızda olarak ayarlanmış ve eşleştirme mantığını umarız daha ilgili size sunmak için sorgu geliştirilmiş ve ekledik daha hızlı paket arama sonuçları.

NuGet 3.0 geliştirme bu aşamasında ilerlemeden gibi biz ayarlama ve olması biz Gelişmiş bir deneyim sunmak sağlamak için nuget.org hizmeti izleme.  Biz olmayan herhangi bir kapalı kalma süresi içinde bulunmaya planlama ancak ekleme ve olması hizmetindeki kaynaklara değiştirme.  Takip bizim [akış twitter](http://twitter.com/nuget) biz hizmet yapılandırmasını değiştirdiğinizde hakkında bilgi.

## <a name="building-nuget-with-nuget"></a>Yapı NuGet NuGet ile

Biz şimdi NuGet müşterilerimizin kendileri NuGet paketlerine oluşturulması birkaç bileşenlere rearchitected. Bu yeniden kullanımını kendi kitaplıkları bize yeniden kullanılabilir olduğunu ve düzgün şekilde paketlenmesi bileşenleri oluşturmaya zorlar.  Yinelenen kod ortadan kaldırabilir ve daha iyi bizim geliştirme işlemi, bizim çözümleri boyunca paketleri oluşturmak için gereken destekleyecek şekilde yapılandırmak nasıl öğrendiniz mümkün olmuştur.  En kısa sürede bir blog gönderisini burada size kod projeleri nasıl yapılandırıldığı ve bizim derleme işleminin nasıl çalıştığı hakkında konuşur arayın.

## <a name="stay-tuned"></a>Bizi izlemeye devam edin

Lütfen takip [bizim blog](http://blog.nuget.org) daha fazla ilerleme ve duyuruları NuGet 3.0 için!
