---
title: "NuGet 2.7.2 sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr NuGet 2.7.2 dahil etmek için sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 2.7.2 sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8fe9acc3ad9c1c368fc750694ea523ac845995c5
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-272-release-notes"></a>NuGet 2.7.2 sürüm notları

[NuGet 2.7.1 sürüm notları](../release-notes/nuget-2.7.1.md) | [NuGet 2.8 sürüm notları](../release-notes/nuget-2.8.md)

NuGet 2.7.2 11 Kasım 2013'te yayımlanmıştır.

## <a name="noteworthy-bug-fixes-and-features"></a>Önemli hata düzeltmeleri ve özellikleri

### <a name="license-text"></a>Lisans metni
Oldukça süre için Microsoft Visual Studio Web Uygulama projeleri için varsayılan şablonları bir parçası olarak birkaç popüler açık kaynak kitaplıkları NuGet paketlerini eklemiştir. jQuery büyük olasılıkla en iyi bilinen bu tür kitaplığının örnektir. Bir ürün ile birlikte sunulur bileşenleri ile ilişkili destek sözleşmesi nedeniyle ortak nuget.org galeride aynı pakette bulunan komut dosyasından farklı lisans metin paketin komut dosyası içerir. Bu farkı metin farklı içerik karması değerlere sahip komut dosyaları neden farklı lisans metin blokları sonucunda ilerlemesini paket güncelleştirmesi engelleyebilir (ve bu nedenle kabul edilmesi için proje içinde değiştirilebilir).

Bu sorunu azaltmak için aşağıdaki gibi görünen özel olarak işaretlenmiş bir bölüme lisans metin blokta dahil etmek betik Yazar NuGet 2.7.2 sağlar.

    /************** NUGET: BEGIN LICENSE TEXT **************
     * The following code is licensed under the MIT license
     * Additional license information below is informational
     * only.
     ************** NUGET: END LICENSE TEXT ***************/

Paket içeriği güncelleştirilirken bu bloğu içeren dosyaları NuGet değil NuGet galerisinde sürüm ile karşılaştırma içine blok içeriğini faktörü bu nedenle silmek ve özgün kopya eşleşen gibi sorgulamanıza içerik dosyasını güncelleştirin.

Bu bloğu metin "NUGET: başlamak lisans metin" ve "NUGET: son lisans herhangi bir yerden başlayarak gerçekleşen ve satırları bitiş metin" tanımlanır.  Bu özellik herhangi bir türde metin dosyası dil bağımsız olarak kullanılmak üzere izin vererek diğer biçimlendirme gereksinimleri mevcut.

### <a name="add-binding-redirects-for-non-framework-assemblies"></a>Bağlama yeniden yönlendirmelerini Framework olmayan derlemeler için ekleme
.NET Framework'ün parçasıdır derlemeler için NuGet, ekleme bağlama yeniden yönlendirmeleri paket güncelleştirirken uygulamanın yapılandırma dosyasına atlar. Bu düzeltme adresleri NuGet bu derlemeler olmasa da yapabildiği bağlama yeniden yönlendirmeleri bazı derlemeler için eklenmedi 2.7'teki bir gerileme .NET Framework'ün bir parçası olarak kabul. NuGet 2.7.2 önceki NuGet 2.5 ve 2.6 davranışını geri yükler ve bağlama yeniden yönlendirmelerini ekler.

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a>Xamarin araçları yüklü olan taşınabilir kitaplıkları yükleme
Xamarin'ın geliştirme araçları bir makinede yüklü olduğunda, var olan hedef framework birleşimleri ve Xamarin çerçeveleri uyumluluğu belirtmek için desteklenen çerçeveleri yapılandırma verilerini değiştirin. Sürüm 2.7.2, NuGet artık bu örtük uyumluluk kuralları kullanan ve bu nedenle, Xamarin ile uyumlu olan, ancak açıkça işaretlenmiş taşınabilir kitaplıklara pakette şekilde yüklemek Xamarin platformları hedefleyen geliştiriciler için kolaylaştırır Meta veriler kendisi.

### <a name="machine-wide-configuration-settings-honored"></a>Makine genelinde yapılandırma ayarlarını dikkate alınır
Hiyerarşik Nuget.Config dosyaları kullanırken repositoryPath anahtar Nuget.Config dosyaları çözümün köküne yakın dikkate alınır değil. Visual Studio 2013'te NuGet "Microsoft .NET ve" Paket kaynağı eklemek için bir özel %ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config Nuget.Config dosyasını yükler. Sonuç olarak, aynı zamanda "Microsoft .NET ve" Paket kaynağı kaldırma amacı makine düzeyinde Nuget.Config - silmek için iş-özel repositoryPath bir çözümde kullanmak için geçici oluştu. NuGet 2.7.2 hiyerarşik Nuget.Config dosyaları kullanırken repositoryPath öncelik kuralları şimdi geliştirir.

## <a name="all-changes"></a>Tüm değişiklikleri
Tam bir listesi için iş öğeleri NuGet 2.7.2, lütfen Görünüm sabit [NuGet sorun İzleyicisi bu sürüm için](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed).
