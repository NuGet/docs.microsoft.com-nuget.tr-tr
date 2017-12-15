---
title: "NuGet 3.1 sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 0fc4d89a-ccca-4d63-85bf-461cd9ced882
description: "NuGet bilinen sorunları, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere 3.1 için sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 3.1 sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: eef2b2c1af99671c7ae3874c2c12130f104e88eb
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-31-release-notes"></a>NuGet 3.1 sürüm notları

[NuGet 3.0 sürüm notları](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 sürüm notları](../release-notes/nuget-3.1.1.md)

NuGet 3.1 27 Temmuz 2015 tarihinde Visual Studio 2015 için evrensel Windows Platform SDK'sının ile birlikte gelen bir uzantısı olarak yayımlanmıştır. Windows geliştirme deneyimi daha önce başlatılmış NuGet platformlar arası iş avantajlarından ele geçirebilir böylece Biz bu sürüm Windows Platform SDK'sı teslim. Bu NuGet uzantısı sürüm yalnızca Visual Studio 2015 için kullanılabilir.

Visual Studio Galerisi güncelleştirme biz her zaman hata düzeltmeleri ve yeni özelliklerle güncelleştirmeleri yayımlama olarak kullanılabilir olan, en son sürüme erişimi bu geliştiriciler öneririz.

## <a name="nuget-visual-studio-extension"></a>NuGet Visual Studio uzantısı

Sorunlar ve bu sürümdeki özellikleri etiketli ile github'da ["3.1 RTM UWP geçişli desteği" Kilometre Taşı](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+) toplam, biz 3.1 sürümdeki 67 sorunlara kapalı.

### <a name="new-features"></a>Yeni Özellikler

* `project.json`Windows UWP ve ASP.NET 5 desteği için destek
* Geçişli paket yükleme

Başka bir yerde açıklama ve bu özelliklerin tanımı belgelerinde bulunabilir.

### <a name="deprecated"></a>Kullanım dışı

Aşağıdaki özellikler artık Visual Studio 2015 için kullanılabilir:

* Çözüm düzeyi paketlerini artık yüklenebilir

Aşağıdaki özellikleri artık Visual Studio 2015 ve kullanmak projeleri için kullanılabilir `project.json` belirtimi

* `install.ps1`ve `uninstall.ps1` -bu komut dosyalarını paket yükleme sırasında yok sayılacak, geri yükleme, güncelleştirme ve kaldırma
* Yapılandırma dönüşümler göz ardı edilir
* İçeriği taşınan ancak bir projeye kopyalanmaz.
    * Bu özellik yeniden uygulamak, tartışmayı izlemek ve adresindeki ilerleme takım çalışma: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)


### <a name="known-issues"></a>Bilinen Sorunlar

Bu sürüm ile birlikte sunulan bilinen sorunlar vardı.

* Windows 10 SDK'sı 3.1 sürümünün yüklemesini herhangi bir sürümünü önceden yüklenmiş olan NuGet uzantısı düşürmek

## <a name="nuget-command-line"></a>NuGet komut satırı

NuGet komut satırı yürütülebilir dosyasını güncelleştirildi ve geçmiş sürümleri nuget.exe kullanılabilir duruma getirilmek üzere devam edebilmesi için bu yeni dağıtılabilir bir konuma taşındı.  Windows için nuget.exe 3.1 beta sürümü yükleyebilirsiniz: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)

Bu şablon izleyen bir klasör yapısı ile dist.nuget.org ana bilgisayarda yeni dağıtılabilir konumu bulunur:

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a>Yeni Özellikler

* nuget.exe geri yüklemek ve kullanmak projelere paketlerini yüklemek bir `project.json` dosyası.
* nuget.exe bağlanmak ve konumundaki NuGet v3 Protokolü kullanma: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)

## <a name="known-issues"></a>Bilinen Sorunlar ##

1.    Paketi karşı yürütülemiyor bir `project.json` dosyası - [928](https://github.com/NuGet/Home/issues/928)
2.    Mono üzerinde - desteklenmeyen [1059](https://github.com/NuGet/Home/issues/1059)
3.    Yerelleştirilmiş değil - [1058](https://github.com/NuGet/Home/issues/1058), [1057](https://github.com/NuGet/Home/issues/1057)
4.    , Yalnızca mevcut http://nuget.org/nuget.exe gibi - imzalanmamış [1073](https://github.com/NuGet/Home/issues/1073)
