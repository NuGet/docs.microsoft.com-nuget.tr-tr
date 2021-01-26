---
title: NuGet 2.7.2 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 2.7.2 için sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 7643bf930bca39684eb626fe737001bc3e3ea769
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776777"
---
# <a name="nuget-272-release-notes"></a>NuGet 2.7.2 sürüm notları

[NuGet 2.7.1 sürüm notları](../release-notes/nuget-2.7.1.md)  |  [NuGet 2,8 sürüm notları](../release-notes/nuget-2.8.md)

NuGet 2.7.2, 11 Kasım 2013 ' de yayımlanmıştır.

## <a name="noteworthy-bug-fixes-and-features"></a>Dikkate değer hata düzeltmeleri ve özellikleri

### <a name="license-text"></a>Lisans metni
Microsoft, belirli bir süre boyunca, Visual Studio 'daki Web uygulaması projelerine yönelik varsayılan şablonların bir parçası olarak çeşitli popüler açık kaynaklı kitaplıklara yönelik NuGet paketlerini içeriyordu. jQuery büyük olasılıkla bu tür kitaplığın en iyi bilinen örneğidir. Bir ürünle birlikte sunulan bileşenlerle ilişkili destek sözleşmesi nedeniyle, paketin betik dosyası genel nuget.org galerisinde aynı pakette bulunan betik dosyasından farklı lisans metni içerir. Metindeki bu fark, farklı lisans metin bloklarının bir sonucu olarak, komut dosyalarının farklı içerik karması değerlerine sahip olmasına neden olan (ve dolayısıyla proje içinde değiştirilmiş olarak değerlendirilme gibi), paket güncelleştirmelerinin devam etmelerini engelleyebilir.

NuGet 2.7.2, bu sorunu azaltmak için betik yazarının lisans metin bloğunu özel olarak işaretlenmiş bir bölüme dahil etmesine izin verir ve aşağıdaki gibi görünür.

```
/************** NUGET: BEGIN LICENSE TEXT **************
    * The following code is licensed under the MIT license
    * Additional license information below is informational
    * only.
    ************** NUGET: END LICENSE TEXT ***************/
```

Bu bloğu içeren içerik dosyaları olan paketleri güncelleştirirken NuGet, bloğunun içeriğini NuGet galerisindeki sürümle karşılaştırmaya katmaz ve bu nedenle içerik dosyasını özgün kopyayla eşleşen bir şekilde silip güncelleştirebilir.

Bu blok, "NUGET: BEGIN LISANS METNI" ve "NUGET: son LISANS METNI" metni tarafından, başlangıç ve bitiş satırlarında herhangi bir yerde meydana gelen bir şekilde tanımlanır.  Başka hiçbir biçimlendirme gereksinimi yoktur, bu özelliğin dilden bağımsız olarak herhangi bir metin dosyasında kullanılmasına izin verilir.

### <a name="add-binding-redirects-for-non-framework-assemblies"></a>Framework olmayan derlemeler için bağlama yeniden yönlendirmeleri ekleme
.NET Framework parçası olan derlemeler için, NuGet paketin güncelleştirilmesi sırasında uygulamanın yapılandırma dosyasına bağlama yeniden yönlendirmeleri eklemeyi atlar. Bu onarım NuGet 2,7 ' de, bu derlemeler .NET Framework bir parçası olarak değerlendirilmese de, bazı derlemeler için bağlama yeniden yönlendirmeleri eklenmemekte olan bir gerileme ele alınmaktadır. NuGet 2.7.2, önceki NuGet 2,5 ve 2,6 davranışını geri yükler ve bağlama yeniden yönlendirmelerini ekler.

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a>Xamarin araçları yüklü olan taşınabilir kitaplıkları yükleme
Xamarin 'in geliştirme araçları bir makineye yüklendiğinde, mevcut hedef Framework birleşimleri ve Xamarin çerçeveleri arasındaki uyumluluğu belirtmek için desteklenen çerçeveler yapılandırma verilerini değiştirir. Sürüm 2.7.2 ile NuGet artık bu örtük uyumluluk kurallarından haberdar olduğundan, Xamarin platformlarını hedefleyen geliştiricilerin Xamarin ile uyumlu olan, ancak paket meta verilerinde açıkça işaretlenmemiş olan taşınabilir kitaplıkları yüklemesini kolaylaştırmaktadır.

### <a name="machine-wide-configuration-settings-honored"></a>Makine genelinde yapılandırma ayarları kabul edilir
Hiyerarşik Nuget.Config dosyaları kullanılırken, çözüm köküne en yakın Nuget.Config dosyalar için Depoyolu anahtarı kabul edilmez. Visual Studio 2013, NuGet "Microsoft ve .NET" paket kaynağını eklemek için% ProgramData% \NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config konumunda özel bir Nuget.Config dosyası yüklüyor. Sonuç olarak, bir çözümde özel bir yeniden yol kullanmak için çözüm, "Microsoft ve .NET" paket kaynağını da kaldıran makine düzeyinde Nuget.Config silmektir. NuGet 2.7.2, hiyerarşik Nuget.Config dosyaları kullanırken, şimdi de depolama yolu için öncelik kuralları verir.

## <a name="all-changes"></a>Tüm değişiklikler
NuGet 2.7.2 'te düzeltilen iş öğelerinin tam listesi için lütfen [Bu sürüm Için NuGet sorun İzleyicisi](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed)' ni görüntüleyin.
