---
title: NuGet 3,0 RC sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 3,0 RC için sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 19bc51a278425295811db253ca3f4ba4366ccf49
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776569"
---
# <a name="nuget-30-rc-release-notes"></a>NuGet 3,0 RC sürüm notları

[NuGet 3,0 beta sürüm notları](../release-notes/nuget-3.0-beta.md)  |  [NuGet 3,0 RC2 sürüm notları](../release-notes/nuget-3.0-RC2.md)

NuGet 3,0 RC, Visual Studio 2015 RC sürümü ile 29 Nisan 2015 tarihinde yayınlanmıştır. Bu sürümde, yeni çerçeveleri desteklemeye yönelik bazı önemli hata düzeltmeleri, performans geliştirmeleri ve güncelleştirmeler bulunur.  Yalnızca Visual Studio 2015 için kullanılabilir.

### <a name="continued-focus-on-performance"></a>Performansa devam eden odak

NuGet sorgularının kararlılığı ve performansı, odaklandığımız bir sıcak konu olarak devam eder.  Bu sürümle birlikte, NuGet Kullanıcı arabiriminde ve Web sitesinde çok hızlı arama işlemlerini görmeniz gerekir.  Hizmeti ve hizmeti nasıl kullanacağınızı, bu işlemleri ayarlamaya devam edebilmemiz için izliyoruz.

## <a name="significant-issues-resolved"></a>Çözümlenen önemli sorunlar

NuGet istemcilerinin kararlı olması için, bu yayının bir parçası olarak birçok sorunu çöztik.  Aşağıda, çözümlenmiş bazı önemli sorunların kısa bir listesi verilmiştir:

* ASP.NET 5 için K çerçevesinin yeniden adlandırılması kapsamında, çerçeve takma adları DNX ve dnxcore [bağlantısını](https://github.com/NuGet/Home/issues/215) işleyecek şekilde güncelleştirilmiştir
* Visual Studio UI [bağlantısı](https://github.com/NuGet/Home/issues/232) 'ndaki bağlantılardan yardım belgeleri eklendi
* `.nuspec`Virgülle ayrılmış çerçeve başvuruları [bağlantısı](https://github.com/NuGet/Home/issues/276) ile içinde karmaşık başvuruların daha iyi işlenmesi
* Japonca kültürler için sabit destek [bağlantısı](https://github.com/NuGet/Home/issues/253)
* ASP.NET 5 projelerinin Yeni v3 uç noktaları [bağlantısı](https://github.com/NuGet/Home/issues/219) kullanmasına izin vermek için istemci güncelleştirildi
* Kaynak denetimi [bağlantısı](https://github.com/NuGet/Home/issues/56) ile paket klasörünü daha iyi işleyecek şekilde güncelleştirildi
* Uydu paketleri için sabit destek [bağlantısı](https://github.com/NuGet/Home/issues/17)
* Çerçeveye özgü içerik dosyaları [bağlantısı](https://github.com/NuGet/Home/issues/18) için düzeltilen destek

## <a name="github-presence-overhaul"></a>GitHub varlık fazla mesafe

[GitHub 'da kaynak kodu depolarımızda](http://github.com/nuget/home)bazı değişiklikler yaptık.  NuGet Visual Studio istemcisiyle ilgili herhangi bir sorununuz varsa, PowerShell komutları veya komut satırı yürütülebilir dosyası varsa, bu sorunları günlüğe kaydedebilir ve [GitHub giriş deposu sorunları listenizde](http://github.com/nuget/home/issues)ilerlemesini izleyebilirsiniz.  [GitHub NuGetGallery deponuzdaki](http://github.com/nuget/NuGetGallery/issues)galerinin sorunlarını izliyoruz.


## <a name="stay-tuned"></a>Ayarlanmış durumda kal

NuGet 3,0 için daha fazla ilerleme ve duyuru için lütfen [blogumuza](http://blog.nuget.org) göz önünde bulundurun!