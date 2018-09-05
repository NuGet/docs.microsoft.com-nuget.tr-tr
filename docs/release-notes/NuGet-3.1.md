---
title: NuGet 3.1 sürüm notları
description: NuGet bilinen sorunları, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr 3.1 sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 779567d94a5a9a1b3eacddaa4c882201a446cb4b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545353"
---
# <a name="nuget-31-release-notes"></a>NuGet 3.1 sürüm notları

[NuGet 3.0 sürüm notları](../release-notes/nuget-3.0.0.md) | [3.1.1 NuGet sürüm notları](../release-notes/nuget-3.1.1.md)

NuGet 3.1 27 Temmuz 2015 tarihinde Visual Studio 2015 için evrensel Windows Platform SDK'sı ile birlikte gelen bir uzantısı olarak yayımlanmıştır. Daha önce başlatılmış NuGet platformlar arası iş yararlanmak Windows geliştirme deneyimi böylece Biz bu sürüm Windows Platform SDK'sı ile teslim. Bu NuGet uzantısı sürüm, yalnızca Visual Studio 2015 için kullanılabilir.

Biz her zaman güncelleştirmeleri hata düzeltmeleri ve yeni özelliklerle yayımlamayı gibi kullanılabilir en son sürümü için Visual Studio Galerisi Update'e erişecek bu geliştiriciler öneririz.

## <a name="nuget-visual-studio-extension"></a>NuGet Visual Studio uzantısı

Sorunları ve özellikler bu sürümde ile github'da etiketli ["3.1 RTM UWP geçişli desteği" aşama](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+) toplam biz 3.1 sürümündeki 67 sorunları kapatıldı.

### <a name="new-features"></a>Yeni Özellikler

* `project.json` Windows UWP ve ASP.NET 5 desteği için destek
* Geçişli paket yükleme

Açıklama ve bu özelliklerin tanımı başka bir yerde belgelerinde bulunabilir.

### <a name="deprecated"></a>kullanım dışı

Aşağıdaki özellikler artık Visual Studio 2015 için kullanılabilir:

* Çözüm düzeyinde paketleri artık yüklenebilir

Aşağıdaki özellikler artık Visual Studio 2015 ve kullanan projeler için kullanılabilir `project.json` belirtimi

* `install.ps1` ve `uninstall.ps1` -bu komut dosyaları paket yükleme sırasında yok sayılacak, geri yükleme, güncelleştirme ve kaldırma
* Yapılandırma dönüşümleri yoksayılır.
* İçerik yürütülüyor ancak projeye kopyalanmaz.
    * Ekibi bu özelliği yeniden uygulamanız ve tartışmayı izlemek, ilerleme çalışıyor: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)


### <a name="known-issues"></a>Bilinen Sorunlar

Bu sürümle birlikte sunulan bilinen sorunlar vardı.

* Yükleme 3.1 sürümüne ait Windows 10 SDK'sı NuGet uzantısı, daha önce yüklü olduğu herhangi bir sürümünü indirilecektir.

## <a name="nuget-command-line"></a>NuGet komut satırı

NuGet komut satırı yürütülebilir dosyasını güncelleştirildi ve kullanılabilir olmasını nuget.exe adet geçmiş sürümü devam edebilmesi için yeni dağıtılabilir bir konuma taşındı.  Nuget.exe 3.1 beta sürümü Windows için yükleyebilirsiniz: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)

Bu şablon aşağıdaki klasör yapısı ile dist.nuget.org ana bilgisayarda dağıtılabilir konuma bulunur:

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a>Yeni Özellikler

* nuget.exe geri yükleyebilir ve kullanan projeler paketlerini yüklemek bir `project.json` dosya.
* nuget.exe bağlanabilir ve kullanma, NuGet v3 protokolü: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)

## <a name="known-issues"></a>Bilinen Sorunlar ##

1.    Paketi karşı yürütülemiyor bir `project.json` dosya - [928](https://github.com/NuGet/Home/issues/928)
2.    Mono üzerinde - desteklenmeyen [1059](https://github.com/NuGet/Home/issues/1059)
3.    Yerelleştirilmez - [1058](https://github.com/NuGet/Home/issues/1058), [1057](https://github.com/NuGet/Home/issues/1057)
4.    , Yalnızca mevcut gibi imzalanmamış http://nuget.org/nuget.exe  -  [1073](https://github.com/NuGet/Home/issues/1073)
