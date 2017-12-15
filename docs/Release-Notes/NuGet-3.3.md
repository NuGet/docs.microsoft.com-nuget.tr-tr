---
title: "NuGet 3.3 sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 4110a36a-cffe-4038-8da4-e841bce6e94b
description: "NuGet bilinen sorunları, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere 3.3 için sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 3.3 sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f35f7621db324957b0af8329cf9faa11493835e2
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-33-release-notes"></a>NuGet 3.3 sürüm notları

[NuGet 3.2.1 sürüm notları](../release-notes/nuget-3.2.1.md) | [NuGet 3.4 RC sürüm notları](../release-notes/nuget-3.4-RC.md)

NuGet 3.3 30 Kasım 2015 çok sayıda kullanışlı düzeltmeleri NuGet istemcilere koleksiyonu yanı sıra kullanıcı arabirimi güncelleştirmeleri ve komut satırı özellikleri ile serbest bırakıldı.

## <a name="new-features"></a>Yeni Özellikler

* Kimlik bilgisi sağlayıcıları sorunsuz bir şekilde kimliği doğrulanmış bir akış ile çalışabilmek için NuGet komut satırı istemcilerin sağlayan tanıtılmıştır. [Visual Studio Team Services yükleme konusunda yönergeler kimlik bilgisi sağlayıcısı ](../API/nuget-exe-Credential-Providers.md) ve NuGet yapılandırma kullanmak için istemciler üzerinde NuGet belgeleri kullanılabilir.

## <a name="new-user-interface-features"></a>Yeni kullanıcı arabirimi özellikleri

* Ayrı Gözat, yüklü ve güncelleştirmeleri kullanılabilir sekmeler
* Kullanılabilir güncelleştirme içeren paketler sayısını gösteren kullanılabilir rozet güncelleştirir
* Paket paketin yüklü olup olmadığını belirtmek için paket listesinde rozetleri veya güncelleştirmesi mevcut
* Sayı ve paket listesine eklenen Yazar indirin
* Yüksek kullanılabilir sürüm numarası ve paket listesi üzerinde şu anda yüklü olan sürüm numarası
* Hızlı yükleme izin vermek için eylem düğmeleri güncelleştirin ve paket listeden kaldırın
* Paket ayrıntı panelindeki daha anlaşılır eylem düğmeleri
* Paket ayrıntı panelindeki paket güncelleştirme tarihi
* Çözüm Görünümü panelinde birleştirin
* Proje ve çözüm görünümü yüklü sürüm numaralarında sıralanabilir kılavuz

## <a name="new-command-line-features"></a>Yeni komut satırı özellikleri

Bu sürümde gösterdiğimizi `add` ve `init` açıklandığı gibi klasör tabanlı depoları başlatmak için komutları [nuget.exe başvuru](../tools/nuget-exe-cli-reference.md). Oluşturulan ve bu klasörü ile korunan depoları yapısı [önemli performans avantajı teslim](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) bizim blogunda özetlendiği gibi.

## <a name="contentfiles"></a>Content dosyaları

İçerik desteklenen şimdi `project.json` yönetilen projeleri yeni aracılığıyla `contentFiles` klasör ve `.nuspec` `contentFiles` öğesi gösterimi.  Bu içerik daha doğrudan proje sistemlerle etkileşim için paket yazarına tarafından belirtilebilir.  Content dosyaları içinde yapılandırma hakkında daha fazla bilgi bir `.nuspec` belge bulunabilir [.nuspec başvuru](../schema/nuspec.md).

## <a name="nuget-locals-cache-management"></a>NuGet yerel yönetim önbelleğe alma

Komut satırı NuGet, bir iş istasyonunda yerel önbellekleri yönetme hakkında bilgiler eklenerek güncelleştirildi.  Yerel öğeler komut hakkında daha fazla bilgi kullanılabilir [NuGet komut satırı başvurusu](../tools/cli-ref-locals.md).

## <a name="fixed-issues"></a>Giderilen sorunlar

**Önem düzeyindeki sorunlar**

* Mono - bir çözüm dosyasını içeren paketleri geri yüklemek için NuGet komut satırı geri yüklenen desteği [1543](https://github.com/NuGet/Home/issues/1543)

3.3 sürümde değinilen sorunların tam listesi GitHub altında bulunabilir [3.3 Kilometre Taşı](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).

3.3 komut satırı sürümde giderilen sorunların listesi kaydedilir [3.3 komut satırı Kilometre Taşı](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).

## <a name="known-issues"></a>Bilinen Sorunlar

Bizim GitHub sorunları listedeki konumunda bulunan sorunları izlemek devam: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)