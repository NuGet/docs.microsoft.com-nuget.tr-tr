---
title: NuGet 1.3 sürüm notları
description: NuGet bilinen sorunları, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere 1.3 için sürüm notları.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c0284fe0afb11bf6465897132cccd160674ea3e1
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31821154"
---
# <a name="nuget-13-release-notes"></a>NuGet 1.3 sürüm notları

[NuGet 1.2 sürüm notları](../release-notes/nuget-1.2.md) | [NuGet 1.4 sürüm notları](../release-notes/nuget-1.4.md)

NuGet 1.3 25 Nisan 2011'de serbest bırakıldı.

## <a name="new-features"></a>Yeni Özellikler

### <a name="streamlined-package-creation-with-symbol-server-integration"></a>Sembol sunucu Tümleştirmesi ile kolaylaştırılmış paketi oluşturma

NuGet takım işbirliği çok kişi ile [SymbolSource.org](http://www.symbolsource.org/) kaynakları ve PDB'ın yayımlama yanı sıra, paketi gerçekten basit bir yol sunmak için. Bu hata ayıklayıcı paketinize kaynağı adımla tüketicilerin paketinin sağlar. Daha fazla ayrıntı için okuma [oluşturma ve yayımlama sembol paketi](../create-packages/symbol-packages.md) kaynaklarıyla NuGet paketlerini yayımlamak için en kolay yolu. Mix11 konuşun dinamik gösterimini bu özellik derinlemesine NuGet bir parçası olarak da izleyebilirsiniz. Bu özellik, video 20 dakika işaretinde başlatma tam olarak gösterilmiştir.

### <a name="open-packagepage-command"></a>`Open-PackagePage` komutu

Bu komut Paket Yöneticisi Konsolu içinden paketinden proje sayfasına almak kolaylaştırır. Ayrıca, lisans URL'sini ve paketi için rapor kötüye sayfası açmak için seçenekler sağlar.
Komut sözdizimi aşağıdaki gibidir:

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

`-PassThru` Seçeneği, belirtilen URL değeri döndürmek için kullanılır.

Örnekler:

    PM> Open-PackagePage Ninject

Ninject paketinde belirtilen proje URL'sini bir tarayıcı açar.

    PM> Open-PackagePage Ninject -License

Ninject paketinde belirtilen lisans URL'sini bir tarayıcı açar.

    PM> Open-PackagePage Ninject -ReportAbuse

Rapor Uygunsuz kullanım için belirtilen paket için kullanılan geçerli paket kaynağında URL'sini bir tarayıcı penceresinde açar.

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

Lisans URL'sini $url değişkenine URL'yi bir tarayıcıda açmadan atar.

### <a name="performance-improvements"></a>Performans Geliştirmeleri

NuGet 1.3 çok fazla performans geliştirmeleri tanıtır. NuGet 1.3 bir yerel kullanıcı başına önbellek dahil olmak üzere birden çok kez aynı bir paketin sürümü indirme önler. Önbellek erişilen ve paket Yönetimi Ayarları iletişim kutusu temizlenmiş:

![Paket önbelleği ayarları ile NuGet Seçenekleri iletişim kutusu](./media/nuget-options.png)

HTTP sıkıştırma desteği ekleme ve Visual Studio içindeki paketi yükleme hızı artırma diğer performans iyileştirmeleri içerir.

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a>Visual Studio ve nuget.exe kullanan paket kaynaklarını aynı listesi

NuGet 1.3 önce nuget.exe ve NuGet Visual Studio eklentisi tarafından kullanılan paket kaynaklarını listesi depolanmadığını aynı yerde. NuGet 1.3 artık her iki yerde de aynı listesini kullanır. Listenin depolanan `NuGet.Config` ve AppData klasöründe depolanır.

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a>nuget.exe yoksayar dosyaları ve başlayın klasörleri '.' varsayılan olarak

Bu tür alt sürüme ve Mercurial de kaynak denetimi sistemleriyle iş NuGet yapmak için nuget.exe ile başlayan dosya ve klasörleri yoksayar '.' karakteri paket oluştururken. Bu iki yeni bayrakları kullanılarak geçersiz kılınabilir:

* __-NoDefaultExcludes__ bu ayarını geçersiz kılmak ve tüm dosyaları dahil etmek için kullanılır.
* __-Hariç__ diğer dosyalar/desen kullanarak hariç tutulacak klasörleri eklemek için kullanılır. Örneğin, '.bak' dosya uzantısına sahip tüm dosyaları dışlayın

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

_Not: düzeni varsayılan özyinelemeli değil._

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a>WiX projeleri ve mikro .NET Framework desteği

Topluluk Katkıları sayesinde NuGet .NET mikro Framework yanı sıra WiX proje türleri için destek içerir.

## <a name="bug-fixes"></a>Hata Düzeltmeleri

Hata düzeltmeleri tam bir listesi için lütfen görüntülemek [NuGet sorun İzleyicisi bu sürüm için](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Eşitlenmeyeceği hata düzeltmeleri

* Her iki Web siteleri ve Web Uygulama projeleri paket kaynak dosyaları ile çalışır.
Web siteleri için kaynak dosyaları içine kopyalanır `App_Code` klasörü
