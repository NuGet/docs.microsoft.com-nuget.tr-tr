---
title: NuGet 1.3 sürüm notları
description: NuGet bilinen sorunları, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr 1.3 için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fa89af100096356c2ffb4d6c501c4a34296ad0ea
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551357"
---
# <a name="nuget-13-release-notes"></a>NuGet 1.3 sürüm notları

[NuGet 1.2 sürüm notları](../release-notes/nuget-1.2.md) | [1.4 NuGet sürüm notları](../release-notes/nuget-1.4.md)

NuGet 1.3 25 Nisan 2011'de yayınlanmıştır.

## <a name="new-features"></a>Yeni Özellikler

### <a name="streamlined-package-creation-with-symbol-server-integration"></a>Sembol sunucusu tümleştirme kolaylaştırılmış paket oluşturma

NuGet takım iş Birliği yaparak yeni başlayanlar ile [SymbolSource.org](http://www.symbolsource.org/) kaynakları ve PDB'ın yanı sıra, paket yayımlama gerçekten çok basit bir yol sunuyor. Bu, paket hata ayıklayıcı kaynağı adımla tüketicilerin paketinizin sağlar. Daha fazla bilgi edinmek için [oluşturma ve bir sembol Paketi Yayımlama](../create-packages/symbol-packages.md) kaynaklarıyla NuGet paketlerini yayımlamak için kolay bir yol. Mix11 konuşma bir canlı tanıtım bu özelliğin NuGet derinlemesine bir parçası olarak da izleyebilirsiniz. Bu özellik, tam olarak 20 dakikalık video işaretinde gösterilmiştir.

### <a name="open-packagepage-command"></a>`Open-PackagePage` Komutu

Bu komut Paket Yöneticisi Konsolu içinden bir paket için proje sayfasına ulaşmak kolaylaştırır. Ayrıca, lisans URL'sini ve paket için rapor kötüye sayfasını açmak için seçenekler sağlar.
Komutu için sözdizimi aşağıdaki gibidir:

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

`-PassThru` Seçeneği, belirtilen URL değerini döndürmek için kullanılır.

Örnekler:

    PM> Open-PackagePage Ninject

Ninject paketinde belirtilen proje URL'sini bir tarayıcı açar.

    PM> Open-PackagePage Ninject -License

Ninject paketinde belirtilen lisans URL'sini bir tarayıcı açar.

    PM> Open-PackagePage Ninject -ReportAbuse

Uygunsuz kullanımı için belirtilen paket için kullanılan geçerli paket kaynağı URL'SİNDE bir tarayıcı açar.

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

Lisans URL'sini bir tarayıcıda URL'yi açmaya gerek kalmadan $url, değişkenine atar.

### <a name="performance-improvements"></a>Performans Geliştirmeleri

NuGet 1.3 birçok performans geliştirmeleri sunar. Bir yerel kullanıcı başına önbellek dahil olmak üzere birden çok kez aynı sürümüne sahip bir paket indiriliyor NuGet 1.3 önler. Önbellek, erişilebilir ve Paket Yöneticisi Ayarları iletişim kutusu temizlenmiş:

![Paket önbelleği ayarları ile NuGet Seçenekleri iletişim](./media/nuget-options.png)

Diğer performans geliştirmelerine, HTTP sıkıştırma desteği eklemeyi ve Visual Studio içindeki paketi yükleme hızını geliştirmek içerir.

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a>Visual Studio ve nuget.exe kullandığı aynı paket kaynaklarının listesi

NuGet 1.3 önce nuget.exe ve NuGet Visual Studio eklentisi tarafından kullanılan paket kaynaklarının listesi depolanmamış aynı yerde. NuGet 1.3, artık her iki yerde de aynı listesini kullanır. Listenin depolanan `NuGet.Config` ve AppData klasöründe depolanır.

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a>nuget.exe dosyaları yoksayar ve ile başlayan Klasörler '.' varsayılan olarak

NuGet Subversion ve Mercurial gibi kaynak denetimi sistemleriyle de çalışır hale getirmek için nuget.exe başlayan dosya ve klasörler yoksayar '.' karakteri paket oluştururken. Bu iki yeni bayrakları kullanılarak geçersiz kılınabilir:

* __-NoDefaultExcludes__ tüm dosyaları içerir ve bu ayarı geçersiz kılmak için kullanılır.
* __-Hariç__ diğer dosyaları/bir desen kullanarak hariç tutulacak klasörler eklemek için kullanılır. Örneğin, '.bak' dosya uzantısına sahip tüm dosyaları dışarıda bırak

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

_Not: desen varsayılan özyinelemeli değildir._

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a>WiX projeleri ve mikro .NET Framework desteği

Topluluk Katkıları sayesinde NuGet .NET mikro Framework yanı sıra WiX proje türleri için destek içerir.

## <a name="bug-fixes"></a>Hata Düzeltmeleri

Hata düzeltmeleri tam bir listesi için lütfen [bu sürüm için NuGet sorun İzleyicisi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).

## <a name="bug-fixes-worth-noting"></a>Önemli hata düzeltmeleri

* Her iki Web siteleri ve Web Uygulama projeleri paket kaynak dosyaları ile çalışma.
Web siteleri için kaynak dosyaları içine kopyalanır `App_Code` klasörü
