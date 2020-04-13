---
title: NuGet 4.6 RTM Yayın Notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve DCR'ler dahil olmak üzere NuGet 4.6.0 için sürüm notları.
author: anangaur
ms.author: anangaur
ms.date: 3/7/2018
ms.topic: conceptual
ms.openlocfilehash: eacd29d4c9340a0f015fcdf6c5b9dd41bf781419
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64498678"
---
# <a name="nuget-46-release-notes"></a>NuGet 4.6 Yayın Notları

[Visual Studio 2017 15.6 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) [NuGet 4.6.0](https://dist.nuget.org/win-x86-commandline/v4.6.0/nuget.exe)ile geliyor.

## <a name="summary-whats-new-in-460"></a>Özeti: 4.6.0 Yenilikler

* [İmza paketleri](../create-packages/sign-a-package.md)için destek ekledik.
* Visual Studio 2017 ve nuget.exe şimdi paket bütünlüğünü yüklemeden önce doğrular, [imzalı paketler](../reference/signed-packages-reference.md)için paketleri geri.
* Art arda geri yüklemelerin performansını artırdık.

## <a name="summary-whats-new-in-463"></a>Özeti: 4.6.3 Yenilikler

* Güvenlik Düzeltmesi: ~/.nuget içinde oluşturulan dosyalardaki izinler [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757) [#7673](https://github.com/NuGet/Home/issues/7673) çok açıktır

## <a name="summary-whats-new-in-464"></a>Özeti: 4.6.4 Yenilikler

* Güvenlik Düzeltmesi: NUPKG'lerin içindeki [dosyalar,](https://github.com/NuGet/Home/issues/7906) NUPKG dizininin üzerinde göreli bir yola sahip olabilir #7906

## <a name="known-issues"></a>Bilinen sorunlar

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>.NET Framework & NuGet ile .NET Standard 2.0 ile ilgili sorunlar 

.NET Standard & .NET Framework 4.6.1'i hedefleyen projeler ,NET Standard 2.0 veya daha önce hedefleyen NuGet paketlerini & projeleri tüketebilecek şekilde tasarlanmıştır. [Bu belge,](https://github.com/dotnet/standard/issues/481) bu senaryonun etrafındaki sorunları, bunları ele alma planını ve araç lamanın bugünkü durumuyla dağıtabileceğiniz geçici geçici işleri özetler.

## <a name="top-issues-fixed-in-this-release"></a>Bu sürümde düzeltilen en önemli sorunlar

**Performans düzeltmeleri**

* Değişiklik olmadığında varlık dosyalarını yazmayın - [#6491](https://github.com/NuGet/Home/issues/6491)
* Geri yükleme, alt projelerin TFM'si ana projenin - [#6311](https://github.com/NuGet/Home/issues/6311) ile eşleşmediğinde ekstra MSBuild değerlendirmeleri neden olur
* Bağımlılık grafiği spec oluşturma optimize ederek NoOp geri perf geri geliştirin - [#6252](https://github.com/NuGet/Home/issues/6252)

**Hata**

* Yerel klasöre itin nupkg kilitli bırakır - [#6325](https://github.com/NuGet/Home/issues/6325)
* NuGet Plugin uygulaması: birden fazla sorun - [#6149](https://github.com/NuGet/Home/issues/6149)
* UIHang - VSSolutionManager'da MEF başlatma dan sorgu hizmeti çağrısını kaldırma - [#6110](https://github.com/NuGet/Home/issues/6110)
* İptal edilen paket indirme görevi için hata bildirme özel durumu - [#6096](https://github.com/NuGet/Home/issues/6096)
* NuGet.exe montaj adına '+' yerine '%2B' - [#5956](https://github.com/NuGet/Home/issues/5956)
* Fn+F1 PM UI ve Console için doğru yardım sayfasına almaz - [#5912](https://github.com/NuGet/Home/issues/5912)
* VS NuGet belirli koşullar altında proje dosyalarına mutlak yollar yazıyor - [#5888](https://github.com/NuGet/Home/issues/5888)
* Fix 4.3 regresyon - Placeholders $product$ ve $AssemblyGuid $ dönüşüm yoluyla contentfile değiştirilmez - [#5880](https://github.com/NuGet/Home/issues/5880)
* birden fazla kaynak çöküyor ile dotnet geri - [#5817](https://github.com/NuGet/Home/issues/5817)
* Pack git sürümüne izin vermek için proje sürümlerini yeniden değerlendirmeli - [#4790](https://github.com/NuGet/Home/issues/4790)
* Uyumsuz bir paket yüklediğinizde anlaşılması zor hataları geliştirme - [#4555](https://github.com/NuGet/Home/issues/4555)
* TemplateWizard paketleri PackageReferences olarak yüklemek için seçenek gerekir - [#4549](https://github.com/NuGet/Home/issues/4549)
* MSBuild.exe geliştirici komut istemi dışından çalıştırıldığında göz ardı edilen paket teslim sahne dosyaları - [#4530](https://github.com/NuGet/Home/issues/4530)
* Proje için geçerli olmayan .NET Standart Kitaplığı'na başvururken kötü hata iletisini düzeltme - [#4423](https://github.com/NuGet/Home/issues/4423)
* dotnet paketi küçük rehberlik ile taşınabilir profil hedefleme için başarısız paketi eklemek - [#4349](https://github.com/NuGet/Home/issues/4349)
* dotnet paketi - ProjectReference'dan eksik sürüm soneki - [#4337](https://github.com/NuGet/Home/issues/4337)
* .NET Core şablonu ile hata oluşturma ve VS çökmesi - [#3973](https://github.com/NuGet/Home/issues/3973)
* Kaynak için hizmet dizininin yüklenememesi https:* - [#3681](https://github.com/NuGet/Home/issues/3681)
* nuget.exe listesi -allversions çalışmıyor - [#3441](https://github.com/NuGet/Home/issues/3441)
* Yanıltıcı bağımlılık çözümlü hata iletisi - [#2984](https://github.com/NuGet/Home/issues/2984)
* nuget.exe geri yükleme .props ve .targets dosyaları üretmez .msbuildproj (v3.3.0-3.4.4 yükseltme de gerileme) - [#2921](https://github.com/NuGet/Home/issues/2921)
* XAML dosyası açık bir NuGet paketini güncellerken ui gecikmesi - [#2878](https://github.com/NuGet/Home/issues/2878)
* IIS'den WebSite projesi, yoldaki yasadışı karakterlerle başarısız oldu - [#2798](https://github.com/NuGet/Home/issues/2798)
* Nuget centos askıda eklemek - [#2708](https://github.com/NuGet/Home/issues/2708)
* packagesavemode -nupkg ile geri json.net için başarısız - [#2706](https://github.com/NuGet/Home/issues/2706)
* Geri yükleme komutu için vs çıkış penceresinde Paket Yöneticisi filtresi kullanılamıyor - [#2704](https://github.com/NuGet/Home/issues/2704)

[Bu sürümde düzeltilen tüm sorunların listesi](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.6")
