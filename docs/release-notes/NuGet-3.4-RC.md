---
title: NuGet 3,4-RC sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 3,4 RC için sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3023dd3727c7c585212032d38c042bded4135c1e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780235"
---
# <a name="nuget-34-rc-release-notes"></a>NuGet 3,4-RC sürüm notları

[NuGet 3,3 sürüm notları](../release-notes/nuget-3.3.md)  |  [NuGet 3,4 sürüm notları](../release-notes/nuget-3.4.md)

NuGet 3,4-RC, Visual Studio 2015 güncelleştirme 2 RC 'nin yanı sıra 3 Mart 2016 ' de yayımlanmıştır ve fikirlerini içinde birkaç tenetle oluşturulmuştur:

* Platformlar arası destek
* Performans geliştirmeleri
* Küçük Kullanıcı arabirimi geliştirmeleri

3,4 son sürümü için daha planlı olan bu RC 'de aşağıdaki özellikler mevcuttur.

## <a name="new-features"></a>Yeni Özellikler

* NuGet istemcileri artık depolardaki gzip içerik kodlamasını destekliyor
* Xproj projelerindeki paketlerin pdb 'leri desteği
* ContentFiles öğesinde iOS ve Android derleme eylemleri için destek
* Netstandard ve netstandardapp Framework takma adları için destek

## <a name="new-user-interface-features"></a>Yeni Kullanıcı arabirimi özellikleri

* Özellikle yüklü, güncelleştirmeler ve birleştirme sekmelerinde önemli performans geliştirmeleri
* Yüklü ve güncelleştirmeler sekmeleri artık alfabetik olarak sıralanmıştır
* Bir aramanın yenilenmesini sağlayan bir yenileme düğmesi eklendi

## <a name="updates-and-improvements"></a>Güncelleştirmeler ve geliştirmeler

* ' De `project.json` bir kayan sürüme başvuruda bulunulan paketler her derlemede güncelmeyecektir. Bunun yerine, yalnızca geri yükleme, Temizleme, yeniden oluşturma veya değiştirme zorlandığında güncelleyirler `project.json` .
* NuGet yapılandırma kullanıcı arabirimini kullandığınızda, nuget.org Repository Kaynakları artık proje yapılandırmasına zorlanmaz.
* NuGet artık paylaşılan projelerdeki paketleri geri yüklemez ve bir kilit dosyası yazar.
* Ağ hatasını geliştirdik ve erişilemeyen ya da yavaş yanıt veren sunucular için işlemeyi yeniden deneyin.
* Klavye ve fare davranışları, Visual Studio Paket Yöneticisi Kullanıcı arabiriminde geliştirilmiştir.
* Artık `project.json` DNX 'teki en son şemayı destekliyoruz.

## <a name="known-issues"></a>Bilinen Sorunlar

GitHub sorunları listesindeki sorunları şurada izlemeye devam ediyoruz: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)