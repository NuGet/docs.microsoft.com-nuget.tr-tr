---
title: NuGet 5,6 sürüm notları
description: Yeni özellikler, hata düzeltmeleri ve DTU 'lar dahil olmak üzere NuGet 5,6 sürüm notları.
author: chgill-msft
ms.author: chgill
ms.date: 05/19/2020
ms.topic: conceptual
ms.openlocfilehash: e8d80a247da1cd18b53b35c51fb3d3dcf1cf68fa
ms.sourcegitcommit: 3529348ed394595d0fa01271486b831af9c97597
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/21/2020
ms.locfileid: "83727823"
---
# <a name="nuget-56-release-notes"></a>NuGet 5,6 sürüm notları

NuGet dağıtım araçlar:

| NuGet sürümü | Visual Studio sürümünde kullanılabilir| .NET SDK 'ları 'nda kullanılabilir|
|:---|:---|:---|
| [**5.6.0**](https://nuget.org/downloads) | [Visual Studio 2019 sürüm 16,6](https://visualstudio.microsoft.com/downloads/) | [3.1.300](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> .NET Core iş yüküne sahip Visual Studio 2019 ile yüklendi

## <a name="summary-whats-new-in-56"></a>Özet: 5,6 sürümündeki yenilikler

* Kayan sürümler içeren ön sürüm paketlerini destekler. `Version="*-*"`, `Version="1.*-*"` ve, belirtilen Aralık içinde ön sürüm sürümleri de dahil olmak üzere en son sürümlere benzer float [#912](https://github.com/NuGet/Home/issues/912)

### <a name="issues-fixed-in-this-release"></a>Bu sürümde giderilen sorunlar

**Hatalar:**

* `nuget push *.nupkg`snupkg yoksa başarısız olur- [#8148](https://github.com/NuGet/Home/issues/8148)

* Paket ve diğer birçok kod yolu, yerel ayara bağımlı olur. RegexOptions. CultureInvariant- [#8246](https://github.com/NuGet/Home/issues/8246) kullanın

* Perf: kaldırılan proje senaryoları için DG Spec Önizleme geri yüklemeler- [#8793](https://github.com/NuGet/Home/issues/8793) yazılmamalıdır

* Geri yükle: önbelleğe alma çözüm bağımlılığı Graph spec- [#9201](https://github.com/NuGet/Home/issues/9201)

* PM konsolu ile bir paket yüklendikten sonra, PM Kullanıcı arabirimi SDK stil projeleri için çalışmıyor- [#9203](https://github.com/NuGet/Home/issues/9203)

* Katıştırılmış simge, yerel paket akışı ile PM Kullanıcı arabiriminde gösterilemez; bağlı/vs \- [#9225](https://github.com/NuGet/Home/issues/9225)

* Ayrıştırma başarısız olursa, NuGetVersion. TryParseStrict () yanlış döndürmelidir [#9255](https://github.com/NuGet/Home/issues/9255)

* `nuget.exe push`kaynak `-source` URL 'si değil, kaynak adı kullanımının önerilmeye yönelik yardım. [#9265](https://github.com/NuGet/Home/issues/9265)

* `dotnet nuget add package SourceUri`Hatalı varsayılan paket kaynağı adı oluşturur- [#9277](https://github.com/NuGet/Home/issues/9277)

* Ekran okuyucu "arama..." duyurusu yapmaz sekmeleri değiştirirken ileti- [#9307](https://github.com/NuGet/Home/issues/9307)

* Erişilebilirlik: odak dikdörtgeni rengine erişilebilir değil koyu temadaki Kullanıcı arabirimi sekmeleri [#9336](https://github.com/NuGet/Home/issues/9336)

* NuGet. exe 5,5, MSBuild 14 veya altında geri yükleme yapamıyor- [#9458](https://github.com/NuGet/Home/issues/9458)

* Geri yükleme iletilerinde milisaniyelik süreleri günlüğe kaydetme- [#8977](https://github.com/NuGet/Home/issues/8977)

* Ioutputconsole zaman uyumsuz yap- [#9268](https://github.com/NuGet/Home/issues/9268)

* MSBuild sürüm seçme, İngilizce olmayan bazı kültürler üzerinde kötü bir şekilde çalışacak [#9322](https://github.com/NuGet/Home/issues/9322)

* #9337 için varsayılan biçim yok `dotnet nuget list source`  -  [#9337](https://github.com/NuGet/Home/issues/9337)

* Perf: Restoreoperationgünlükçü gereksiz iş parçacığı benzeşimine sahip- [#9288](https://github.com/NuGet/Home/issues/9288)

* Komutlar için otomatik belgeler oluşturma `dotnet nuget` - [#9146](https://github.com/NuGet/Home/issues/9146)

* Varsayılan ayrıntı düzeyi her projenin noop geri yükleme- [#8792](https://github.com/NuGet/Home/issues/8792) raporlanmamalıdır

* `-DependencyVersion`İçin destek parametresi `NuGet.exe update` , install komutuna benzer- [#7694](https://github.com/NuGet/Home/issues/7694)


**DCR**

* NET 5.0 hedef çerçevesi için başlangıç desteğini ekleme- [#9584](https://github.com/NuGet/Home/issues/9584)

* PM UI- [#9278](https://github.com/NuGet/Home/issues/9278) Updates SEKMESINDE paketleri kimliğe göre sırala


**[Bu yayında düzeltilen tüm sorunların listesi-5,6](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e3b2080c4b30708e48bf9f3)**
