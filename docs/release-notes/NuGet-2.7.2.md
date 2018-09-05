---
title: 2.7.2 NuGet sürüm notları
description: NuGet 2.7.2 dahil etmek için sürüm notları, sorunları, hata düzeltmeleri, eklenen özellikler ve dcr bilinir.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3e63944a05f66d5dadf17c5d4b91d3bc4478bb33
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550076"
---
# <a name="nuget-272-release-notes"></a>2.7.2 NuGet sürüm notları

[NuGet 2.7.1 sürüm notları](../release-notes/nuget-2.7.1.md) | [NuGet 2.8 sürüm notları](../release-notes/nuget-2.8.md)

NuGet 2.7.2 11 Kasım 2013 tarihinde yayınlanmıştır.

## <a name="noteworthy-bug-fixes-and-features"></a>Önemli hata düzeltmesi ve özellik

### <a name="license-text"></a>Lisans metni
Oldukça biraz zaman için Microsoft Visual Studio Web Uygulama projeleri için varsayılan şablonları bir parçası olarak birkaç popüler açık kaynak kitaplıkları için NuGet paketlerini eklemiştir. jQuery büyük olasılıkla en iyi bilinen bu tür kitaplığı bir örnektir. Bir ürün ile birlikte sunulan bileşenleri ile ilişkili bir destek sözleşmesi nedeniyle aynı pakette genel nuget.org galeride bulunan komut dosyasından farklı lisans metin paketin komut dosyası içerir. Metinde bu fark, paket güncelleştirmelerini farklı içerik karması değerlere sahip komut dosyaları neden farklı lisans metin blokları sonucunda ilerlemesini engelleyebilir (ve bu nedenle olarak kabul edilmesini proje içinde değiştirilebilir).

Bu sorunu gidermek için NuGet 2.7.2 lisans metin bloğu içinde şu şekilde görünür, özel olarak işaretlenmiş bir bölüm eklemek betik Yazar sağlar.

    /************** NUGET: BEGIN LICENSE TEXT **************
     * The following code is licensed under the MIT license
     * Additional license information below is informational
     * only.
     ************** NUGET: END LICENSE TEXT ***************/

Paketler içeriği güncelleştirilirken bu bloğu içeren dosyaları NuGet değil NuGet galerisindeki sürümünde ile karşılaştırma içine blok içeriği faktörü ve bu nedenle silebilir ve özgün kopya eşleşir ancak içerik dosyasını güncelleştirin.

Bu blok metin "NUGET: başlamak lisans metin" ve "NUGET: son lisans herhangi bir yere tarihinden itibaren gerçekleşen ve satır sonlandırma metin" tanımlanır.  Metin dosyası diline bakılmaksızın herhangi bir türde kullanılmak üzere bu özelliği sağlayan diğer biçimlendirme gereksinimleri vardır.

### <a name="add-binding-redirects-for-non-framework-assemblies"></a>Bağlama yeniden yönlendirmelerini Framework olmayan derlemeler için ekleyin
.NET Framework'ün parçasıdır derlemeler için NuGet, ekleme bağlama yeniden yönlendirmeleri paketi güncelleştirilirken uygulamanın yapılandırma dosyasına atlar. Bu düzeltme adresleri NuGet bu derlemeleri olmasa da yapabildiği bağlama yeniden yönlendirmeleri bazı derlemeler için eklenmedi 2.7'teki bir gerileme .NET Framework'ün bir parçası olarak kabul. NuGet 2.7.2 önceki NuGet 2.5 ve 2.6 davranışını geri yükler ve bağlama yeniden yönlendirmeleri ekler.

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a>Xamarin araçları yüklü taşınabilir kitaplıkları yükleme
Xamarin'in geliştirme araçları bir makinede yüklü olduğunda bunlar mevcut hedef framework birleşimleri ve Xamarin çerçeveleri uyumluluğu belirtmek için desteklenen çerçeveler yapılandırmasını değiştirin. 2.7.2 sürümü ile NuGet artık bu örtük uyumluluk kurallarını kullanan ve bu nedenle, Xamarin ile uyumlu olan, ancak açıkça işaretlenmiş taşınabilir kitaplıklarını pakette şekilde yüklemek Xamarin platformlarını hedefleyen geliştiriciler için kolaylaştırır meta verileri kendisini.

### <a name="machine-wide-configuration-settings-honored"></a>Makine genelindeki yapılandırma ayarlarını dikkate alınır
Hiyerarşik Nuget.Config dosyalarını kullanırken repositoryPath anahtar Nuget.Config dosyaları çözüm kök en yakın kabul değil. NuGet, Visual Studio 2013'te "Microsoft ve .NET" Paket kaynağı eklemek için bir özel %ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config Nuget.Config dosyasını yükler. Sonuç olarak, "Microsoft ve .NET" Paket kaynağını kaldırarak ayrıca geliyordu makine düzeyinde Nuget.Config - silmek için bir çözüm içindeki özel dosyasının repositorypath ayarı kullanmak için geçici oluştu. NuGet 2.7.2 artık hiyerarşik Nuget.Config dosyalarını kullanırken öncelik kuralları için repositoryPath geliştirir.

## <a name="all-changes"></a>Tüm değişiklikler
Tam bir listesi için iş öğeleri Nuget'te 2.7.2, lütfen görünümü sabit [bu sürüm için NuGet sorun İzleyicisi](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed).
