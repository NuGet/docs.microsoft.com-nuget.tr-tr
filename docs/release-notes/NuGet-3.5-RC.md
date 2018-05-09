---
title: 3.5 RC sürüm notları
description: NuGet 3.5 bilinen sorunları, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere RC sürüm notları.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d620a8b8d97f9a52cb2bc93a91eb393130a42898
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/28/2018
---
# <a name="nuget-35-rc-release-notes"></a>NuGet 3.5 RC sürüm notları

[NuGet 3.5 Beta2 sürüm notları](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-sürüm notları RTM](../release-notes/nuget-3.5-RTM.md)

NuGet istemcileri, kalite ve performansını geliştirmeye 3.5 sürüm odaklanmıştır. Ayrıca, biz desteği gibi birkaç özellikleri gönderilen [geri dönüş klasörleri](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) desteklemek `.nuspec` ve daha fazlası.

[Konu listesi](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a>Hata Düzeltmeleri

* Paketi yükle/geri yükleme başarısız oluyor "pakette birden çok `.nuspec` dosyaları." - [#3231](https://github.com/NuGet/Home/issues/3231)

* nuget paketi zorla ekler `.tt` dosyaları içerik klasörüne - ne olursa olsun [#3203](https://github.com/NuGet/Home/issues/3203)

* nuget paketi csproj (ile `project.json`) hiçbir packOptions ve JSON dosyasında - sahibi varsa çöküyor [#3180](https://github.com/NuGet/Home/issues/3180)

* nuget paketini `project.json` packOptions etiketleri özeti, yazarlar, sahipleri vb. - gibi yoksayar [#3161](https://github.com/NuGet/Home/issues/3161)

* nuget paketi yoksayar çıkış bağımlılıkları `.nuspec` için `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* Bozuk durumda - bırakır projeyi geri alma ile birden çok paket güncelleştirme [#3139](https://github.com/NuGet/Home/issues/3139)

* Content altında bulunan dosyaları netstandard projelerde - eklenmedi [#3118](https://github.com/NuGet/Home/issues/3118)

* .NET hedefleme kitaplığı paketleyemez standart doğru - [#3108](https://github.com/NuGet/Home/issues/3108)

* Dosya -> Yeni Proje VS2015 ve Dev15 - sınıf kitaplığı (taşınabilir) proje başarısız -> [#3094](https://github.com/NuGet/Home/issues/3094)

* nuGet hata - 1.0.0-* geçerli bir sürüm dizesi - değil [#3070](https://github.com/NuGet/Home/issues/3070)

* Bul-Package başarısız görünen ancak Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)

* Hata olduğunda "Install-Package jquery.validation" dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)

* Yüklü VS 2015 sürüm 3.5.0 hatası oluşur - NuGet kullanan bir VS 3 güncelleştirdiğinizde [#3053](https://github.com/NuGet/Home/issues/3053)

* Paket Yöneticisi kullanıcı Arabirimi: bir paket güncelleştirdikten sonra yeni sürümü görüntülemez- [#3041](https://github.com/NuGet/Home/issues/3041)

* -Apikey ile yapılan Sil komut satırında okuma/gönderilmez 3.5.0-beta içinde - [#3037](https://github.com/NuGet/Home/issues/3037)

* Yanlış dize: bir paketin durağan sürümü bir ön sürüm bağımlılığı olmamalıdır. - [#3030](https://github.com/NuGet/Home/issues/3030)

* PCL (net46 ve windows 10) proje get NullRef özel durum oluşturuluyor. - [#3014](https://github.com/NuGet/Home/issues/3014)

* Daha yüksek bir sürüm allowedVersions kısıtlaması tarafından - sınırlı olduğunda, Nuget güncelleştirme bilgilendirici ileti temin etmelidir [#3013](https://github.com/NuGet/Home/issues/3013)

* Kimlik Bilgisi Eklentisi -1 hata ile çıkıldı / hata indirme paketini kimlik bilgisi sağlayıcıları birden çok kaynaklarıyla - kullanırken [#2885](https://github.com/NuGet/Home/issues/2885)

* nuget paketi - eksik Newtonsoft.Json paket bağımlılığı - [#2876](https://github.com/NuGet/Home/issues/2876)

* Linux/MacOS + Mono - üzerinde ExecuteSynchronizedCore hatada [#2860](https://github.com/NuGet/Home/issues/2860)

* VS repositoryPath içinde ortam değişkenlerini desteklemez (nuget.exe yapar) - [#2763](https://github.com/NuGet/Home/issues/2763)

* Erişilebilirlik sorunları - [#2745](https://github.com/NuGet/Home/issues/2745)

* Tirelenmiş profilleriyle taşınabilir çerçeveleri reddedilir. - [#2734](https://github.com/NuGet/Home/issues/2734)

* NuGet Paket Yöneticisi, bu paketleri ayrıntı için geçerli olmayan Seçenekler listesinde temizleyin olmalısınız `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* NuGet 3.3.0 güncelleştirme başarısız olan '... ek kısıtlama tanımlanan packages.config bu işlemi engelliyor.' - [#1816](https://github.com/NuGet/Home/issues/1816)

* Sahte bir ileti - paketini atar mevcut olmayan yerel bir kaynaktan yükleme [#1674](https://github.com/NuGet/Home/issues/1674)

* "Yükseltme ullanılabilir" filtre gösterir - sürüm kısıtlamayı ihlal yükseltmeler [#1094](https://github.com/NuGet/Home/issues/1094)

## <a name="performance-improvements"></a>Performans Geliştirmeleri

* : ContentModel hedef framework ayrıştırma - performansı [#3162](https://github.com/NuGet/Home/issues/3162)

* Performans: Okuma kaçının `runtime.json` RID olmayan geri yükleme dosyaları [#3150](https://github.com/NuGet/Home/issues/3150). CI makinelerde 3 saniye için 15 saniye aşırı derecede ASP.NET Web uygulaması sınırlı bir örnek geri yükleyin.

* Performans: Paket Yöneticisi konsolu init.ps1 yükleme süresi [#2956](https://github.com/NuGet/Home/issues/2956). Bazı durumlarda 132s'den 10'luk için PackageManagerConsole açmak zaman geliştirilmiş.

* NuGet güncelleştirmesi - ReSharper performans sorunları çözmek [#3044](https://github.com/NuGet/Home/issues/3044): bir örnek proje üzerinde paketleri yüklemek için harcanan süre sınırlı 140s 68s için.

## <a name="dcrs"></a>Dcr

* NuGet gereken yükseltme/yükleme dayalı dotnet tfm PCL sorunları - neden olabilecek olduğunu bilmesini sağlamak üzere [#3138](https://github.com/NuGet/Home/issues/3138)

* Hatalı yükleme/yükseltme tfm içeren projesi için uyar "dotnet" - = [#3137](https://github.com/NuGet/Home/issues/3137)

* Netcoreapp11 ve netstandard17 desteği - eklemek [#2998](https://github.com/NuGet/Home/issues/2998)

* Nuget.exe içinde - konsol için NuGet uyarı üstbilgi içeriği Yazdır [#2934](https://github.com/NuGet/Home/issues/2934)

* Dengeleme AssemblyMetadata özniteliği için `.nuspec` belirteci değişikliklerini - [#2851](https://github.com/NuGet/Home/issues/2851)

* Kilit dosyasından - kilitli özelliği kaldırmak [#2379](https://github.com/NuGet/Home/issues/2379)

* Sembol paketlerini yüklemek için hiç kullanılmamalıdır veya #2807 güncelleştir

## <a name="features"></a>Özellikler

* Geri dönüş paketi klasörlerinin - desteği [#2899](https://github.com/NuGet/Home/issues/2899)

* Aracı paketler - desteklemek için paket türü kavramını tasarlayıp [#2476](https://github.com/NuGet/Home/issues/2476)

* Genel paketler klasörüne - yolu API [#2403](https://github.com/NuGet/Home/issues/2403)

* Güncelleştirme desteği - yerel paketleri [#1291](https://github.com/NuGet/Home/issues/1291)
