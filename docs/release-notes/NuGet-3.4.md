---
title: NuGet 3,4 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 3,4 sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 794b25e2d81d7a2c297a185bdb34a7cf68535723
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776412"
---
# <a name="nuget-34-release-notes"></a>NuGet 3,4 sürüm notları

[NuGet 3,4-RC sürüm notları](../release-notes/nuget-3.4-RC.md)  |  [NuGet 3.4.1 sürüm notları](../release-notes/nuget-3.4.1.md)

NuGet 3,4, Visual Studio 2015 güncelleştirme 2 ve Visual Studio 15 Preview sürümünün bir parçası olarak 30 Mart 2016 ' de yayımlanmıştır ve fikirlerini ' de birkaç tenetle oluşturulmuştur:

* Platformlar arası destek
* Performans geliştirmeleri
* Küçük Kullanıcı arabirimi geliştirmeleri

Aşağıdaki özellikler daha önce RC 'ye eklenmiştir ve 3,4 sürümü için güncelleştirilmiştir veya tamamlanmıştır:

## <a name="new-features"></a>Yeni Özellikler

* NuGet istemcileri artık depolardaki gzip içerik kodlamasını destekliyor
* Xproj projelerindeki paketlerin pdb 'leri desteği
* ContentFiles öğesinde iOS ve Android derleme eylemleri için destek
* Netstandard ve netstandardapp Framework takma adları için destek

## <a name="new-user-interface-features"></a>Yeni Kullanıcı arabirimi özellikleri

* Özellikle yüklü, güncelleştirmeler ve birleştirme sekmelerinde önemli performans geliştirmeleri
* Toplu ' tüm paket kaynakları ' kaynağı uygun arama sonucu birleştirme ile kullanılabilir
* Yüklü ve güncelleştirmeler sekmeleri artık alfabetik olarak sıralanmıştır
* Bir aramanın yenilenmesini sağlayan bir yenileme düğmesi eklendi
* Sürüm listesinin en üstünde bulunan en son derleme seçenekleri

## <a name="updates-and-improvements"></a>Güncelleştirmeler ve geliştirmeler

* ' De `project.json` bir kayan sürüme başvuruda bulunulan paketler her derlemede güncelmeyecektir. Bunun yerine, yalnızca geri yükleme, Temizleme, yeniden oluşturma veya değiştirme zorlandığında güncelleyirler `project.json` .
* NuGet yapılandırma kullanıcı arabirimini kullandığınızda, nuget.org Repository Kaynakları artık proje yapılandırmasına zorlanmaz.
* NuGet artık paylaşılan projelerdeki paketleri geri yüklemez ve bir kilit dosyası yazar.
* Ağ hatasını geliştirdik ve erişilemeyen ya da yavaş yanıt veren sunucular için işlemeyi yeniden deneyin.
* Klavye ve fare davranışları, Visual Studio Paket Yöneticisi Kullanıcı arabiriminde geliştirilmiştir.
* Artık `project.json` DNX 'teki en son şemayı destekliyoruz.

## <a name="breaking-changes"></a>Hataya Neden Olan Değişiklikler

* Paket sürüm numaraları artık *birincil* biçime normalleştirilir. *küçük*. *Düzeltme Eki* - *ön sürüm*   Ana, alt ve yayama her biri tamsayılar olarak değerlendirilir ve öndeki sıfırlar kaldırılır.  Ön sürüm bilgileri bir dize olarak değerlendirilir ve buna hiçbir değişiklik uygulanmaz. Bu sayılar, NuGet istemcilerine ve nuget.org hizmeti tarafından sunulan aramaya göre sorgularda kullanılır.  Daha fazla ayrıntı, NuGet belgeleri altında [yayın öncesi sürümler](../create-packages/prerelease-packages.md)altında bulunabilir.

## <a name="known-issues"></a>Bilinen Sorunlar

* **Sorun:** Windows 10 v1511 kullanıcıları, aşağıdaki senaryolarda, Visual Studio 'da PowerShell ile birlikte Visual Studio kilitlenmesi veya sorunlar yaşayabilir:
    * install.ps1/uninstall.ps1 betiklerine sahip paketleri yükleme/kaldırma
    * init.ps1 betiği olan projeler (EntityFramework gibi) yükleniyor
    * Web içeriği yayımlanıyor

* **Geçici çözüm:** Windows 10 yüklemesinin en son düzeltme eklerinin uygulanmış olduğundan emin olun, expecially Ocak 2016 (KB 3124263) veya sonraki bir güncelleştirme.  [GitHub sorunundan](http://github.com/nuget/home/issues/1638) daha fazla ayrıntı bulabilirsiniz #1638

* **Sorun:** NuGet v2 protokolü yeniden yönlendirmeleri bozuk.
İstekleri alternatif bir konağa yönlendiren özel NuGet depoları, yeniden yönlendirme isteğini yerine getirmiyor.
* **Geçici çözüm:**  Bu sorunu geçici olarak çözmek için, Ayarlar ' da paket deposu URI 'sini yeniden yönlendirilen sunucu konumunu gösterecek şekilde yapılandırın.
Daha fazla bilgi için bkz. [GitHub çekme isteği #387](https://github.com/NuGet/NuGet.Client/pull/387).

GitHub sorunları listesindeki sorunları şurada izlemeye devam ediyoruz: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)