---
title: NuGet 3,0 beta sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 3,0 beta sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 7970c3d81c724edc743d7b2d38c4c157237a0271
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776621"
---
# <a name="nuget-30-beta-release-notes"></a>NuGet 3,0 beta sürüm notları

[NuGet 3,0 Preview sürüm notları](../release-notes/nuget-3.0-preview.md)  |  [NuGet 3,0 RC sürüm notları](../release-notes/nuget-3.0-rc.md)

NuGet 3,0 Beta, Visual Studio 2015 CTP 6 sürümü için 23 Şubat 2015 ' de yayımlanmıştır. Bu sürüm, paylaşılacak bir dizi mimariye ve performans iyileştirmelerine sahip olduğumuz ve nuget.org hizmetimizde performans ayarlarını ayarlamaya başlayacağız.

Bu yeni sürümü yüklemeden önce NuGet Visual Studio 2015 uzantısının önceki sürümlerini kaldırmanızı kesinlikle öneririz.  Uzantının bu sürümü ile ilgili herhangi bir sorununuz varsa, Visual Studio 2015 Preview ile kullanmak için [önceki sürüme](http://nuget.codeplex.com/downloads/get/909582) döndürmeniz önerilir.

## <a name="visual-studio-2012"></a>Visual Studio 2012 +

Bu NuGet 3,0 Beta sürümü Visual Studio 2015 CTP 6 uzantı Galerisi ' nde yüklenmeye hazırdır. Visual Studio 2012 ve çok yakında Visual Studio 2013 Önizleme altına almak için çalışıyoruz. Daha önce [Visual Studio 2010 güncelleştirmelerini sona erdirme](http://blog.nuget.org/20141002/visual-studio-2010.html)amacımızı paylaştık ve bu zor kararı veriyoruz.

## <a name="new-clientserver-api"></a>Yeni Istemci/sunucu API 'SI

NuGet istemci/sunucu protokolü için bazı uygulama ayrıntıları üzerinde çalışıyoruz. Yaptığımız iş, paket geri yükleme ve paketleri yükleme gibi kritik senaryolar için yüksek kullanılabilirlik çevresinde tasarlanan NuGet için "API v3" oluşturmaktır. Yeni API, REST ve hiper medyayı temel alır ve kaynak biçimimiz olarak [JSON-ld](http://json-ld.org) ' i seçtik.

NuGet 3,0 Beta bitleriyle, paket kaynak açılan menüsünde "api.nuget.org" adlı yeni bir paket kaynağı görürsünüz.   Bu paket kaynağını seçerseniz, nuget.org 'e bağlanmak yerine yeni API 'imizi kullanacağız. NuGet 3,0 RC 'de, bu yeni API v3 tabanlı paket kaynağı v2 tabanlı "nuget.org" paket kaynağının yerini alır.  Diğer tüm ortak paket kaynaklarını devre dışı bırakmayı ve yalnızca ortak paket deponuzun yalnızca api.nuget.org bırakmayı öneririz.

V3 API 'imizi oluşturmaya çok zaman koyduk ve ortak depoya erişmek isteyen eski istemciler için standart v2 API 'sini sürdürmeye devam edecektir.

## <a name="updated-ui"></a>Güncelleştirilmiş Kullanıcı arabirimi

Bu sürümdeki Kullanıcı arabirimini, paketle birlikte yapılacak bir eylem seçmenize ve ekranın seçenekler alanında Önizleme düğmesini bir onay kutusu içine geçirlemenize imkan tanıyan bir açılan kutu içerecek şekilde geliştirdik.  Seçenekler alanı artık daraltılabilir değildir ve artık kullanılabilir seçenekleri açıklayan bir yardım bağlantısı sağlar.

![Yeni NuGet Kullanıcı arabirimi](./media/NuGet-3.0-Beta/updated-ui.png)


### <a name="operation-logging"></a>İşlem günlüğü

Yükleme veya kaldırma sırasında hızla belirebilir ve gizleyecek olan günlük bilgileriyle kalıcı pencereyi kaldırdık.  Bu pencere, bilgileri görmek veya onu kopyalayıp yapıştırmak istediğinizde hiçbir değer ekledi.  Bunun yerine, artık çıkış penceresinin Paket Yöneticisi bölmesine çıkış günlüğü 'nün tümünü yönlendirdik.  Bunun daha rahat olduğunu ve incelemek istediğiniz tipik bir yapı raporuna benzetireceğiz.


### <a name="focus-on-performance"></a>Performansa odaklanın

NuGet aramalarının performansını iyileştirme adında çok sayıda değişiklik yaptık ve bunu getirir.  Bu, müşterilerimizden bir sorun olması ve bu yayında sorunu ele aldığınızdan emin olmak istiyorduk.  Sunucularımızdan yararlandık, yeni bir CDN oluşturdunuz ve sorgu eşleştirme mantığını geliştirdik, böylece daha ilgili ve daha hızlı bir şekilde paket arama sonuçları elde ederiz.

NuGet 3,0 geliştirmenin bu aşamasında ilerliyoruz, gelişmiş bir deneyim sunduğumuz için nuget.org hizmetini ayarlamamız ve izleyeceğiz.  Herhangi bir kesinti süresi boyunca katılım planlıyoruz, ancak hizmette kaynak eklemek ve değiştirmek olacaktır.  Hizmet yapılandırmasını değiştirdiğimiz sırada Ayrıntılar için [Twitter akışımıza](http://twitter.com/nuget) göz önünde bulundurun.

## <a name="building-nuget-with-nuget"></a>NuGet ile NuGet oluşturma

NuGet istemcilerimizi NuGet paketlerinde yerleşik olarak bulunan çeşitli bileşenlere yeniden geliştirdik. Kendi kitaplıklarımızın bu yeniden kullanımı, yeniden kullanılabilir olan ve düzgün paketlenebilecek bileşenler oluşturmaya zorlar.  Yinelenen kodu ortadan kaldırdık ve uygulamalarımız genelinde paket oluşturma ihtiyacını desteklemek için geliştirme sürecimizi nasıl daha iyi yapılandıracağınızı öğrendiniz.  Kod projelerinin nasıl yapılandırıldığı ve derleme sürecimizin nasıl çalıştığı hakkında konuşacak bir blog gönderisine göz atın.

## <a name="stay-tuned"></a>Ayarlanmış durumda kal

NuGet 3,0 için daha fazla ilerleme ve duyuru için lütfen [blogumuza](http://blog.nuget.org) göz önünde bulundurun!
