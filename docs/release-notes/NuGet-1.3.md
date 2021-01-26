---
title: NuGet 1,3 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 1,3 sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 54eda149352810eacc1d6340ad16cec1b03194e3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777119"
---
# <a name="nuget-13-release-notes"></a>NuGet 1,3 sürüm notları

[NuGet 1,2 sürüm notları](../release-notes/nuget-1.2.md)  |  [NuGet 1,4 sürüm notları](../release-notes/nuget-1.4.md)

NuGet 1,3, 25 Nisan 2011 ' de yayımlanmıştır.

## <a name="new-features"></a>Yeni Özellikler

### <a name="streamlined-package-creation-with-symbol-server-integration"></a>Sembol sunucusu tümleştirmesiyle kolaylaştırılmış paket oluşturma

NuGet ekibi, kaynaklarınızı ve PDB 'yi paketinizle birlikte yayımlamanın gerçekten basit bir yolunu sunmak için [SymbolSource.org](http://www.symbolsource.org/) adresindeki katlarla işbirliği yapar. Bu, paketinizin tüketicilerinin hata ayıklayıcıdaki paketinizin kaynağına ilerlemenize olanak tanır. Daha fazla ayrıntı için, [bir sembol paketini oluşturma ve yayımlama](../create-packages/symbol-packages.md) hakkında bilgi edinmek için, kaynak ile NuGet paketlerini yayımlamanın kolay yolunu okuyun. Ayrıca, Mix11 adresindeki NuGet 'in bir parçası olarak bu özelliğin canlı bir gösterimini izleyebilirsiniz. Bu özellik, videonun 20 dakikalık işaretiyle başlayarak tam olarak gösterilmiştir.

### <a name="open-packagepage-command"></a>`Open-PackagePage` Komutundaki

Bu komut, paket yöneticisi konsolundan bir paketin proje sayfasına almayı kolaylaştırır. Ayrıca, paket için lisans URL 'sini ve kötüye kullanımı raporla sayfasını açma seçenekleri de sağlar.
Komutun sözdizimi şöyledir:

```
Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]
```

`-PassThru`Seçeneği, BELIRTILEN URL 'nin değerini döndürmek için kullanılır.

Örnekler:

```
PM> Open-PackagePage Ninject
```

Nekleme paketinde belirtilen proje URL 'SI için bir tarayıcı açar.

```
PM> Open-PackagePage Ninject -License
```

Nekleme paketinde belirtilen lisans URL 'SI için bir tarayıcı açar.

```
PM> Open-PackagePage Ninject -ReportAbuse
```

Belirtilen paket için kötüye kullanımı raporlamak üzere kullanılan geçerli paket kaynağında URL 'ye bir tarayıcı açar.

```
PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru
```

URL 'yi bir tarayıcıda açmadan $url, lisans URL 'sini değişkenine atar.

### <a name="performance-improvements"></a>Performans Geliştirmeleri

NuGet 1,3, çok sayıda performans geliştirmesi sunmaktadır. NuGet 1,3, Yerel Kullanıcı başına önbellek ekleyerek aynı paketin aynı sürümünü birden çok kez indirmeyi önler. Önbellek, Paket Yöneticisi ayarları iletişim kutusu aracılığıyla erişilebilir ve temizlenir:

![Paket önbelleği ayarlarıyla NuGet seçenekleri Iletişim kutusu](./media/nuget-options.png)

Diğer performans geliştirmeleri, HTTP sıkıştırması desteği ekleme ve Visual Studio içinde paket yükleme hızını geliştirme içerir.

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a>Visual Studio ve nuget.exe aynı paket kaynakları listesini kullanır

NuGet 1,3 ' den önce, nuget.exe ve NuGet Visual Studio Add-In tarafından kullanılan paket kaynaklarının listesi aynı yerde depolanmaz. NuGet 1,3 artık her iki yerde de aynı listeyi kullanır. Liste ' de depolanır `NuGet.Config` ve AppData klasöründe depolanır.

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a>nuget.exe, varsayılan olarak '. ' ile başlayan dosyaları ve klasörleri yoksayar

NuGet işini alt sürüm ve Mercurial gibi kaynak denetim sistemleriyle iyi hale getirmek için nuget.exe, paketler oluştururken '. ' karakteriyle başlayan klasörleri ve dosyaları yoksayar. Bu, iki yeni bayrak kullanılarak geçersiz kılınabilir:

* __-Nodefaultexcludes__ , bu ayarı geçersiz kılmak ve tüm dosyaları dahil etmek için kullanılır.
* __-Exclude__ , bir model kullanılarak dışlanacak diğer dosya/klasörleri eklemek için kullanılır. Örneğin, '. bak ' dosya uzantısına sahip tüm dosyaları dışlamak için

```cli
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

_Not: varsayılan olarak, model özyinelemeli değildir._

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a>WiX projeleri ve .NET mikro Framework desteği

NuGet, topluluk katkılarına yönelik olarak WiX proje türlerinin yanı sıra .NET mikro Framework için de destek içerir.

## <a name="bug-fixes"></a>Hata Düzeltmeleri

Hata düzeltmelerinin tam listesi için lütfen [Bu sürüm Için NuGet sorun İzleyicisi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)' ni görüntüleyin.

## <a name="bug-fixes-worth-noting"></a>Hata düzeltmeleri dikkat edilecek değer

* Kaynak dosyaları olan paketler her iki Web sitesinde ve Web uygulaması projelerinde çalışır.
Web siteleri için kaynak dosyalar `App_Code` klasörüne kopyalanır
