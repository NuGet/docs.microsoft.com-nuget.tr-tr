---
title: NuGet 2.2.1 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr NuGet 2.2.1 dahil etmek için sürüm notları.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fddeb4e8c9fb2d85ba1876360862461e8ef025af
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-221-release-notes"></a>NuGet 2.2.1 sürüm notları

[NuGet 2.2 sürüm notları](../release-notes/nuget-2.2.md) | [NuGet 2.5 sürüm notları](../release-notes/nuget-2.5.md)

NuGet 2.2.1 15 Şubat 2013'te yayımlanmıştır.  VS uzantısı sürüm 2.2.40116.9051 sayısıdır.

## <a name="localization-refresh"></a>Yerelleştirme yenileme
NuGet Visual Studio 2012 bir parçası olarak gönderilir, bunu tamamen yerelleştirilmiş İngilizce + 13 diğer diller.  O tarihten sonra NuGet 2.1 ve 2.2 gönderilen ancak yerelleştirme değil yenilenir.  NuGet 2.2.1 sürüm bizim yerelleştirme yeniler.

NuGet'ın kullanıcı Arabirimi ve PowerShell konsolunda aşağıdaki dillere yerelleştirilmiştir:

1. ve
1. seçenekleri yerine
1. Çekçe
1. İngilizce
1. Fransızca
1. Almanca
1. İtalyanca
1. Japonca
1. Kore Dili
1. Lehçe
1. Portekizce (Brezilya)
1. Rusça
1. İspanyolca
1. Türkçe

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a>Visual Studio şablonları birden çok önceden yüklenmiş paket depoları desteği
Visual Studio şablonları oluşturmak, için NuGet kullanabilirsiniz [önceden paketleri](../visual-studio-extensibility/visual-studio-templates.md) şablonunun parçası olarak.  Şimdiye kadar bu özellik bir sınırlama sahip tüm paketler aynı kaynaktan geldiği gerekiyordu.  2.2.1 NuGet ile yine de (içinde şablonu, bir VSIX veya kayıt defterinde tanımlanan diskteki bir klasöre) birden çok depoları yüklenen paketler olabilir.

Bu özellik için ana senaryo özel ASP.NET proje şablonları ' dir.  Yerel disk paketlerinden çekme önceden yüklenen paketler yerleşik ASP.NET şablonları kullanın.  Şimdi, ASP.NET tarafından yüklenen var olan paketler kullanan bir özel ASP.NET proje şablonu oluşturma ancak şablonunuza fazladan NuGet paketleri ekleyin.

## <a name="bug-fixes"></a>Hata Düzeltmeleri
NuGet 2.2.1 birkaç hedeflenen hata düzeltmeleri içerir. İş listesi için öğeleri NuGet 2.2.1, lütfen Görünüm sabit [NuGet sorun İzleyicisi bu sürüm için](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).


## <a name="known-issues"></a>Bilinen Sorunlar

ASP.NET proje şablonları genişletme, tüm önceden yüklenmiş paket depoları için aynı değeri kullanmalısınız `isPreunzipped` özniteliği.
