---
title: 2.2.1 NuGet sürüm notları
description: NuGet 2.2.1 dahil etmek için sürüm notları, sorunları, hata düzeltmeleri, eklenen özellikler ve dcr bilinir.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: abbd3a9d9c51132477ceb236fed22cb63ccda209
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550704"
---
# <a name="nuget-221-release-notes"></a>2.2.1 NuGet sürüm notları

[NuGet 2.2 sürüm notları](../release-notes/nuget-2.2.md) | [NuGet 2.5 sürüm notları](../release-notes/nuget-2.5.md)

NuGet 2.2.1 15 Şubat 2013 tarihinde yayınlanmıştır.  VS uzantısı sürüm numarasını 2.2.40116.9051 ' dir.

## <a name="localization-refresh"></a>Yerelleştirme yenileme
NuGet, Visual Studio 2012 bir parçası olarak gönderildiğini, tamamen yerelleştirilmiş İngilizce + 13 dilde.  O tarihten sonra NuGet 2.1 ve 2.2 gönderildi ancak yerelleştirme değil yenilenir.  NuGet 2.2.1 sürüm bizim yerelleştirme yeniler.

NuGet'ın kullanıcı Arabirimi ve PowerShell konsolunda aşağıdaki dilde yerelleştirilmiş:

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

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a>Visual Studio şablonları birden çok önceden yüklenmiş paket Depolarınızın destekler.
Visual Studio şablonları oluşturmak, için NuGet kullanabilirsiniz [önceden paketleri](../visual-studio-extensibility/visual-studio-templates.md) şablonunun bir parçası olarak.  Şimdiye kadar bu özellik bir sınırlama sahip tüm paketler aynı kaynaktan geldiği için gerekli.  2.2.1 NuGet ile birden çok depolarından (içinde şablon, bir VSIX veya kayıt defterinde tanımlanan diskte bir klasörü) yüklü paketleri yine de olabilir.

Bu özellik için ana senaryo özel ASP.NET proje şablonları ' dir.  Önceden yüklenmiş paketler, yerel disk paketlerden çekme yerleşik ASP.NET şablonları kullanın.  Şimdi, ASP.NET tarafından yüklenmiş var olan paketleri kullanan özel bir ASP.NET proje şablonu oluşturma ancak ek NuGet paketlerini şablonunuza ekleyin.

## <a name="bug-fixes"></a>Hata Düzeltmeleri
NuGet 2.2.1 birkaç hedeflenen hata düzeltmeleri içerir. İş listesi için öğeleri Nuget'te 2.2.1, lütfen görünümü sabit [bu sürüm için NuGet sorun İzleyicisi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).


## <a name="known-issues"></a>Bilinen Sorunlar

ASP.NET proje şablonları uzatıyoruz. Gerekirse, tüm önceden yüklenmiş paket depolarınızın için aynı değeri kullanmalısınız `isPreunzipped` özniteliği.
