---
title: NuGet 3,1 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 3,1 sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e1dc31e2543610b1da395f77fd2424bd85d985ef
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776533"
---
# <a name="nuget-31-release-notes"></a>NuGet 3,1 sürüm notları

[NuGet 3,0 sürüm notları](../release-notes/nuget-3.0.0.md)  |  [NuGet 3.1.1 sürüm notları](../release-notes/nuget-3.1.1.md)

NuGet 3,1, Visual Studio 2015 için Evrensel Windows Platformu SDK 'Sı için paketlenmiş bir uzantı olarak 27 Temmuz 2015 tarihinde yayımlanmıştır. Windows geliştirme deneyiminin daha önce başlatılmış olan NuGet platformlar arası çalışmanın avantajlarından yararlanması için, bu sürümü Windows platformu SDK ile birlikte sunuyoruz. Bu NuGet uzantısı sürümü yalnızca Visual Studio 2015 için kullanılabilir.

Her zaman hata düzeltmeleri ve yeni özelliklerle güncelleştirmeler yayımladığımızda, Visual Studio Galerisi güncelleştirmesine erişimi olan geliştiricilerin, mevcut en son sürüme erişmesini öneririz.

## <a name="nuget-visual-studio-extension"></a>NuGet Visual Studio uzantısı

Bu sürümdeki sorunlar ve özellikler, GitHub 'da ["3,1 RTM UWP geçişli destek" kilometre taşına](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  göre etiketlendi ve 3,1 sürümündeki 67 sorunlarını kapattık.

### <a name="new-features"></a>Yeni Özellikler

* `project.json` Windows UWP ve ASP.NET 5 desteği desteği
* Geçişli paket yüklemesi

Bu özelliklerin açıklaması ve tanımı belgelerde başka bir yerde bulunabilir.

### <a name="deprecated"></a>Kullanım Dışı

Aşağıdaki özellikler artık Visual Studio 2015 için kullanılamaz:

* Çözüm düzeyi paketler artık yüklenemez

Aşağıdaki özellikler artık Visual Studio 2015 ve belirtimi kullanan projeler için kullanılamaz `project.json`

* `install.ps1` ve `uninstall.ps1` -Bu betikler paket yükleme, geri yükleme, güncelleştirme ve kaldırma işlemi sırasında yok sayılır
* Yapılandırma dönüştürmeleri yoksayılacak
* İçerik taşınır, ancak bir projeye kopyalanmaz.
    * Takım, bu özelliği yeniden uygulamak için çalışıyor, tartışma ve ilerleme durumunu takip eden: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)


### <a name="known-issues"></a>Bilinen Sorunlar

Bu sürümle birlikte sunulan bazı bilinen sorunlar oluştu.

* Windows 10 SDK ile 3,1 sürümünün yüklenmesi, daha önce yüklenmiş olan herhangi bir NuGet uzantısı sürümünün indirgenmesini sağlayacak

## <a name="nuget-command-line"></a>NuGet komut satırı

NuGet komut satırı yürütülebilir dosyası güncelleştirildi ve yeni bir dağıtılabilir konuma taşındı nuget.exe geçmiş sürümlerinin kullanılabilir hale getirilmeye devam edebilmesi için.  Windows için nuget.exe 'nin 3,1 Beta sürümünü şu adreste indirebilirsiniz: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)

Yeni dağıtılabilir konum dist.nuget.org konağında bulunur ve bu şablonu izleyen bir klasör yapısıdır:

```
{platform supported}/{version}/nuget.exe
```

### <a name="new-features"></a>Yeni Özellikler

* nuget.exe, paketleri bir dosya kullanan projelere geri yükleyebilir ve yükleyebilir `project.json` .
* nuget.exe, şu adreste bulunan NuGet v3 protokolüne bağlanabilir ve bunları kullanabilir: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)

## <a name="known-issues"></a>Bilinen Sorunlar ##

1.    Paket bir dosyaya karşı yürütülemiyor `project.json` - [928](https://github.com/NuGet/Home/issues/928)
2.    Mono- [1059](https://github.com/NuGet/Home/issues/1059) ' de desteklenmez
3.    Yerelleştirilmiş değil- [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)
4.    , Tıpkı var olan http://nuget.org/nuget.exe  -  [1073](https://github.com/NuGet/Home/issues/1073) gibi imzalanmadı
