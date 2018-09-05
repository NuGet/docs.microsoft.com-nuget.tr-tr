---
title: NuGet 3.3 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr NuGet 3.3 sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5fb840ab6a1329611e9cf417724bcdcd75efe2df
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546653"
---
# <a name="nuget-33-release-notes"></a>NuGet 3.3 sürüm notları

[NuGet 3.2.1 sürüm notları](../release-notes/nuget-3.2.1.md) | [NuGet 3.4 RC sürüm notları](../release-notes/nuget-3.4-RC.md)

NuGet 3.3, 30 Kasım 2015 ile çok sayıda kullanışlı düzeltmeleri NuGet istemcilere koleksiyonunu yanı sıra kullanıcı arabirimi güncelleştirmeleri ve komut satırı özellikleri olarak yayımlanmıştır.

## <a name="new-features"></a>Yeni Özellikler

* Sorunsuz bir şekilde kimliği doğrulanmış bir akışı ile çalışmak komut satırı istemcilerin NuGet kimlik bilgisi sağlayıcıları tanıtılmıştır. [Visual Studio Team Services'ı yüklemek yönergeler kimlik bilgisi sağlayıcısı ](../api/nuget-exe-credential-providers.md) ve NuGet yapılandırma kullanmak için istemcileri üzerinde NuGet belgeleri kullanılabilir.

## <a name="new-user-interface-features"></a>Yeni kullanıcı arabirimi özellikleri

* Göz atma, yüklü ve güncelleştirmeleri kullanılabilir ayrı sekmeler
* Kullanılabilir güncelleştirmeleri olan paketleri sayısını gösteren güncelleştirmeleri kullanılabilir rozeti
* Paket yüklü değil veya güncelleştirmesi mevcut olmadığını belirtmek için paket listesinde paket rozetlerini
* Sayısı ve paket listesine Yazar indirin
* Yüksek kullanılabilir sürüm numarasını ve paket listesi üzerinde şu anda yüklü sürüm numarası
* Hızlı yükleme izin vermek için komut düğmeleri güncelleştirmek ve paketi listeden kaldırma
* Paket Ayrıntıları paneline üzerinde NET eylem düğmeleri
* Paket Ayrıntıları paneline paket güncelleştirme tarihi
* Çözüm görünümünde panelinde birleştirin
* Proje ve çözüm görünümü üzerinde yüklü sürüm numaraları sıralanabilir kılavuz

## <a name="new-command-line-features"></a>Yeni komut satırı özellikleri

Bu sürümde sunduk `add` ve `init` açıklandığı gibi klasör tabanlı depoları başlatmak için komutları [nuget.exe başvurusu](../tools/nuget-exe-cli-reference.md). Oluşturulur ve bu klasörü tutulan depolar yapısı [önemli performans avantajlarının teslim](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) blogumuzu özetlenen.

## <a name="contentfiles"></a>contentFiles

İçerik desteklenen artık `project.json` projelerini yeni aracılığıyla yönetilen `contentFiles` klasörü ve `.nuspec` `contentFiles` öğesi gösterimi.  Bu içerik daha doğrudan proje sistemleri ile etkileşim için paket yazarı tarafından belirtilebilir.  ContentFiles içinde yapılandırma hakkında daha fazla bilgi bir `.nuspec` belge bulunabilir [.nuspec başvuru](../reference/nuspec.md).

## <a name="nuget-locals-cache-management"></a>Yönetim NuGet yerel önbellek

NuGet komut satırı, bir iş istasyonundaki yerel önbelleklerini nasıl yönetecekleri hakkındaki bilgileri içerecek şekilde güncelleştirildi.  Yerel öğeler komut hakkında daha fazla bilgi kullanılabilir [NuGet komut satırı başvurusu](../tools/cli-ref-locals.md).

## <a name="fixed-issues"></a>Giderilen sorunlar

**Önemli sorunlar**

* Geri yükleme için NuGet komut satırı geri yüklenen desteği paketleri ile bir çözüm dosyası üzerinde Mono - [1543](https://github.com/NuGet/Home/issues/1543)

3.3 sürümünde giderilen sorunların tam listesi altında github'da bulunabilir [3.3 kilometre](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).

3.3 komut satırı sürümde giderilen sorunlar listesinde kaydedilir [3.3 komut satırı kilometre](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).

## <a name="known-issues"></a>Bilinen Sorunlar

Şurada bulunabilir bizim GitHub sorunlar listesinde sorunları izlemek devam ediyoruz: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)