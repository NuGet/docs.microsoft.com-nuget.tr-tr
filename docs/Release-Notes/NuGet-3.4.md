---
title: "NuGet 3.4 sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere NuGet 3.4 için sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 3.4 sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 515fb888aca2a8eb138c8fea1fb5b3f5a8f4e275
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-34-release-notes"></a>NuGet 3.4 sürüm notları

[NuGet 3.4 RC sürüm notları](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 sürüm notları](../release-notes/nuget-3.4.1.md)

NuGet 3.4 30 Mart 2016 Visual Studio 2015 güncelleştirme 2 ve Visual Studio 15 Preview sürümü bir parçası olarak yayımlanmıştır ve minds içinde birkaç tenets ile oluşturuldu:

*  Platformlar arası desteği
*  Performans iyileştirmeleri
*  İkincil UI geliştirmeleri

Aşağıdaki özellikler RC önceden eklendi ve güncelleştirildi veya 3.4 sürüm için tamamlandı:

## <a name="new-features"></a>Yeni Özellikler

* Gzip içerik kodlamasına depoları gelen NuGet istemcileri artık destekler
* Xproj projelerindeki paketlerden PDB'leri için destek
* İOS ve Android derleme eylemleri contentFiles öğesindeki desteği
* Netstandard ve netstandardapp bilinen adları framework adları için destek

## <a name="new-user-interface-features"></a>Yeni kullanıcı arabirimi özellikleri

* Özellikle, yüklü, güncelleştirmeleri ve birleştirme sekmelerde önemli performans geliştirmeleri
* Birleşik 'Tüm paket kaynaklarını' kaynak uygun arama sonucu birleştirme ile kullanılabilir
* Yüklü ve güncelleştirmeleri sekmeler şimdi alfabetik olarak sıralanır.
* Yenilenecek bir arama özelliğine imkan tanıyan bir Yenile düğmesini eklendi
* Sürüm listenin en son derleme seçenekleri

## <a name="updates-and-improvements"></a>Güncelleştirmeleri ve geliştirmeleri

* Başvurulan paketleri `project.json` sahip bir kayan sürüm üzerinde her yapı güncelleştirmez. Bunun yerine, bunlar yalnızca geri yükleme, temizleme, yeniden oluşturmak veya değiştirmek için zorlandığında güncelleştirecektir `project.json`.
* NuGet yapılandırma kullanıcı Arabirimi kullandığınızda nuget.org depo kaynakları artık bir proje yapılandırma zorlanır.
* Artık NuGet paketleri paylaşılan projelerinde yükler veya kilit dosyası yazar.
* Biz, ağ hatası geliştirildi ve işleme erişilemiyor veya yanıt ile yavaş sunucuları için yeniden deneyin.
* Klavye ve fare davranışları Visual Studio Paket Yöneticisi Arabiriminde geliştirildi.
* En son artık desteklenmektedir `project.json` DNX şemada.

## <a name="breaking-changes"></a>Yeni Değişiklikler

* Paket sürüm numaralarını şimdi biçimine normalleştirilmiş *ana*. *küçük*. *Düzeltme Eki*-*ön* her birincil, ikincil ve düzeltme eki tamsayı olarak kabul edilir ve hiçbir 2f3b bırakın.  Yayın öncesi bilgiler bir dize olarak kabul edilir ve hiçbir değişiklik için uygulanır. Bu sayı sorgularda NuGet istemcileri ve nuget.org hizmeti tarafından sağlanan arama tarafından kullanılır.  Daha fazla ayrıntı NuGet belgeleri altında bulunabilir [yayın öncesi sürümleri](../create-packages/prerelease-packages.md).

## <a name="known-issues"></a>Bilinen Sorunlar

* **Sorun:** sorunları veya hatta bir Visual Studio kilitlenme Visual Studio'da Powershell ile aşağıdaki senaryolarda Windows 10 v1511 kullanıcılar karşılaşabilirsiniz:
    * Yükleme / kaldırma install.ps1 sahip paketleri / uninstall.ps1 komut dosyaları
    * Init.ps1 betiği (gibi EntityFramework) projeleri yükleniyor
    * Yayımlama web içeriği

* **Geçici çözüm:** Windows 10 yüklemenizi uygulanan en son düzeltme eklerini, expecially (KB 3124263) Ocak 2016 veya sonraki bir güncelleştirme olduğundan emin olun.  Daha fazla ayrıntı kullanılabilir [GitHub sorunu #1638](http://github.com/nuget/home/issues/1638)

* **Sorun:** NuGet v2 protokolü yeniden yönlendirmeleri bozuk.
İstekleri alternatif bir konağa yönlendiren özel NuGet depoları, yeniden yönlendirme isteğini yerine getirmiyor.
* **Geçici çözüm:** bu sorunu çözmek için ayarlardaki Paket Deposu URI yeniden yönlendirilen sunucu konumunu gösterecek şekilde yapılandırın.
Daha fazla bilgi için bkz: [GitHub çekme isteği #387](https://github.com/NuGet/NuGet.Client/pull/387).

Bizim GitHub sorunları listedeki konumunda bulunan sorunları izlemek devam: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)