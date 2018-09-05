---
title: NuGet 3.4 sürüm notları
description: NuGet 3.4 bilinen sorunları, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 77c0117fc40031a327e8dcb0aac5cd4045239e97
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551197"
---
# <a name="nuget-34-release-notes"></a>NuGet 3.4 sürüm notları

[NuGet 3.4 RC sürüm notları](../release-notes/nuget-3.4-RC.md) | [3.4.1 NuGet sürüm notları](../release-notes/nuget-3.4.1.md)

NuGet 3.4, 30 Mart 2016'dan Visual Studio 2015 güncelleştirme 2 ve Visual Studio 15 Preview sürümü bir parçası olarak yayımlanmıştır ve aklını içinde birkaç sacayakları derlendiği:

* Platformlar arası destek
* Performans iyileştirmeleri
* Küçük bir kullanıcı Arabirimi geliştirmeleri

Aşağıdaki özellikler RC'de daha önce eklenen ve güncelleştirildi veya 3.4 sürümü için tamamlandı:

## <a name="new-features"></a>Yeni Özellikler

* NuGet istemcileri artık gzip içerik kodlamasını depolarından destekler
* Xproj projelerindeki paketlerden PDB'leri için destek
* Derleme eylemleri contentFiles öğesinde iOS ve Android desteği
* Netstandard ve netstandardapp framework bilinen adlar için destek

## <a name="new-user-interface-features"></a>Yeni kullanıcı arabirimi özellikleri

* Yüklü, güncelleştirmeleri ve birleştirme sekmelerinde özellikle önemli performans geliştirmeleri
* Toplama 'Tüm paket kaynakları' kaynak uygun arama sonucu birleştirme ile kullanılabilir
* Yüklü ve güncelleştirmeleri sekmeleri artık alfabetik olarak sıralanır.
* Sağlayan bir arama yenilenmesi yenile düğmesine eklendi
* Sürüm listenin üst kısmındaki en son derleme seçenekleri

## <a name="updates-and-improvements"></a>Güncelleştirmeler ve iyileştirmeler

* Başvurulan paketleri `project.json` sahip kayan sürüm her derleme üzerinde güncelleştirmez. Bunun yerine, bunlar yalnızca geri yükleme, temizleme, yeniden oluşturmak veya değiştirmek için zorlandığında güncelleştirecek `project.json`.
* NuGet Yapılandırması kullanıcı Arabirimi kullandığınızda nuget.org depo kaynakları artık bir proje yapılandırması zorlanır.
* NuGet artık paylaşılan projelerde paketleri geri yükler veya bir kilit dosyası yazar.
* Biz, ağ hatası geliştirdik ve işleme erişilemiyor veya yanıt ile yavaş sunucuları için yeniden deneyin.
* Klavye ve fare davranışlar Visual Studio Paket Yöneticisi Arabiriminde geliştirildi.
* En son artık desteklenmektedir `project.json` DNX şemasında.

## <a name="breaking-changes"></a>Yeni Değişiklikler

* Paket sürüm numaraları artık biçimine normalleştirilmiş *ana*. *küçük*. *Düzeltme Eki*-*ön* her birincil, ikincil ve düzeltme eki tamsayı olarak kabul edilir ve hiçbir 2f3b bırakın.  Yayın öncesi bilgiler bir dize olarak kabul edilir ve değişiklikler için uygulanmaz. Bu numaraları NuGet istemcileri ve nuget.org hizmet tarafından sağlanan arama sorguları kullanılır.  NuGet belgeleri altında daha fazla ayrıntı bulunabilir [yayın öncesi sürümler](../create-packages/prerelease-packages.md).

## <a name="known-issues"></a>Bilinen Sorunlar

* **Sorun:** sorunları veya hatta bir Visual Studio kilitlenmesi Visual Studio'da Powershell ile aşağıdaki senaryolarda Windows 10 v1511 kullanıcıları karşılaşabilirsiniz:
    * Yükleme / kaldırma install.ps1 olan paketleri / uninstall.ps1 betikleri
    * (EntityFramework gibi) bir init.ps1 betiği içeren projeleri yükleniyor
    * Web içerik yayımlama

* **Geçici çözüm:** Windows 10 yüklemenizi uygulanan en son düzeltme eklerinin, expecially Ocak 2016 (KB 3124263) veya daha yeni bir güncelleştirme olduğundan emin olun.  Daha fazla bilgi edinilebilir [GitHub sorunu #1638](http://github.com/nuget/home/issues/1638)

* **Sorun:** NuGet v2 protokolü yeniden yönlendirmeleri bozuk.
İstekleri alternatif bir konağa yönlendiren özel NuGet depoları, yeniden yönlendirme isteğini yerine getirmiyor.
* **Geçici çözüm:** bu sorunu çözmek için yeniden yönlendirilen sunucu konumunu gösterecek şekilde ayarlardaki Paket Deposu URI yapılandırın.
Daha fazla bilgi için [GitHub çekme isteği #387](https://github.com/NuGet/NuGet.Client/pull/387).

Şurada bulunabilir bizim GitHub sorunlar listesinde sorunları izlemek devam ediyoruz: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)