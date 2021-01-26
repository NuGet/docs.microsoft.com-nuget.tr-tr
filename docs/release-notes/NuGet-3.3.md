---
title: NuGet 3,3 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 3,3 sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cd3f8c9c4586c608d41e7b8bfc413acfc6aff497
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776506"
---
# <a name="nuget-33-release-notes"></a>NuGet 3,3 sürüm notları

[NuGet 3.2.1 sürüm notları](../release-notes/nuget-3.2.1.md)  |  [NuGet 3,4-RC sürüm notları](../release-notes/nuget-3.4-RC.md)

NuGet 3,3, önemli sayıda kullanıcı arabirimi güncelleştirmesi ve komut satırı özelliği ve NuGet istemcilerinde yararlı düzeltmelerin toplanması ile 30 Kasım 2015 ' de yayımlanmıştır.

## <a name="new-features"></a>Yeni Özellikler

* NuGet komut satırı istemcilerinin kimliği doğrulanmış bir akış ile sorunsuz bir şekilde çalışmasına izin veren kimlik bilgileri sağlayıcıları tanıtılmıştır. [Visual Studio Team Services kimlik bilgisi sağlayıcısının nasıl yükleneceğine ](../reference/extensibility/nuget-exe-credential-providers.md) ve NuGet istemcilerinin onu kullanmak üzere nasıl yapılandırılacağına Ilişkin yönergeler NuGet docs ' da kullanılabilir.

## <a name="new-user-interface-features"></a>Yeni Kullanıcı arabirimi özellikleri

* Ayrı tarama, yükleme ve güncelleştirmeleri kullanılabilir sekmeleri
* Kullanılabilir güncelleştirmeleri olan paket sayısını gösteren rozet 'yi güncelleştirir
* Paket, paketin yüklenip yüklenmediğini veya kullanılabilir bir güncelleştirme olup olmadığını belirtmek için paket listesinde
* Paket listesine eklenen indirme sayısı ve yazar
* Paket listesinde en yüksek kullanılabilir sürüm numarası ve yüklü olan sürüm numarası
* Paket listesinden hızlı yüklemeye, güncelleştirmeye ve kaldırmaya izin veren eylem düğmeleri
* Paket ayrıntısı panelinde eylem düğmelerini daha net olarak göster
* Paket ayrıntı panelinde paket güncelleştirme tarihi
* Çözüm görünümünde Birleştirme paneli
* Çözüm görünümündeki proje ve yüklü sürüm numaraları için sıralanabilir kılavuz

## <a name="new-command-line-features"></a>Yeni komut satırı özellikleri

Bu sürümde, `add` `init` [nuget.exe başvurusunda](../reference/nuget-exe-cli-reference.md)açıklandığı gibi klasör tabanlı depoları başlatmak için ve komutlarını geliştirdik. Bu klasör yapısıyla oluşturulan ve tutulan depolar, blogumuza göre [önemli performans avantajları sunar](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) .

## <a name="contentfiles"></a>ContentFiles

İçerik artık `project.json` Yeni `contentFiles` klasör ve `.nuspec` öğe gösterimi aracılığıyla yönetilen projelerde desteklenmektedir `contentFiles` .  Bu içerik, proje sistemleriyle etkileşimler için paket yazarı tarafından daha doğrudan belirtilebilir.  Bir belgedeki contentFiles 'ın nasıl yapılandırılacağı hakkında daha fazla bilgi `.nuspec` [. nuspec başvurusunda](../reference/nuspec.md)bulunabilir.

## <a name="nuget-locals-cache-management"></a>NuGet Yereller önbellek yönetimi

NuGet komut satırı, bir iş istasyonunda yerel önbellekleri yönetme hakkında bilgi içerecek şekilde güncelleştirilmiştir.  Yerel öğeler komutu hakkında daha fazla bilgi [NuGet komut satırı başvurusunda](../reference/cli-reference/cli-ref-locals.md)bulunabilir.

## <a name="fixed-issues"></a>Düzeltilen Sorunlar

**Önemli sorunlar**

* NuGet komut satırı, mono- [1543](https://github.com/NuGet/Home/issues/1543) ' de çözüm dosyası ile paket geri yükleme desteğini geri yükledi

3,3 sürümünde ele alınan sorunların tüm listesi, GitHub 'da [3,3 kilometre taşı](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed)altında bulunabilir.

3,3 komut satırı sürümünde düzeltilen sorunların listesi [3,3 Command-Line kilometre taşına](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline)kaydedilir.

## <a name="known-issues"></a>Bilinen Sorunlar

GitHub sorunları listesindeki sorunları şurada izlemeye devam ediyoruz: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)