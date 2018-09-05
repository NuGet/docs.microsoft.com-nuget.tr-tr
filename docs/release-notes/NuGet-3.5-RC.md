---
title: 3.5 RC sürüm notları
description: NuGet 3.5 bilinen sorunları, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr RC sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 52c443ecd79c9108203f5a3c327078ce9e28b95b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548544"
---
# <a name="nuget-35-rc-release-notes"></a>NuGet 3.5 RC sürüm notları

[NuGet 3.5-Beta2 sürüm notları](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM sürüm notları](../release-notes/nuget-3.5-RTM.md)

sürüm 3.5 kalitesini ve NuGet istemcilerinin performansını geliştirmeye odaklanır. Ayrıca, biz desteği gibi bazı özellikler gönderildi [geri dönüş klasörleri](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) desteklemek `.nuspec` ve daha fazlası.

[Sorun listesi](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a>Hata Düzeltmeleri

* Paketi yükle/geri yükleme başarısız oluyor "pakette birden çok `.nuspec` dosyalarını." - [#3231](https://github.com/NuGet/Home/issues/3231)

* nuget paketi zorla ekler `.tt` dosyaları içerik klasörüne - ne olursa olsun [#3203](https://github.com/NuGet/Home/issues/3203)

* nuget paketi csproj (ile `project.json`) hiçbir packOptions ve JSON dosyasında - sahibi varsa kilitleniyor [#3180](https://github.com/NuGet/Home/issues/3180)

* nuget paketi için `project.json` packOptions etiketleri özeti, yazarlar, sahipleri - vb. gibi yoksayar [#3161](https://github.com/NuGet/Home/issues/3161)

* nuget paketi yoksayar çıkış bağımlılıkları `.nuspec` için `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* Geri alma ile birden çok paketlerin güncelleştirilmesi, bozuk bir durumda - proje bırakır [#3139](https://github.com/NuGet/Home/issues/3139)

* ContentFiles herhangi netstandard projeleri için - eklenmedi [#3118](https://github.com/NuGet/Home/issues/3118)

* Kitaplık .net targeting paketlenemiyor standart doğru - [#3108](https://github.com/NuGet/Home/issues/3108)

* Dosya -> Yeni Proje -> sınıf kitaplığı (taşınabilir) proje başarısız VS2015 ve - Dev15 [#3094](https://github.com/NuGet/Home/issues/3094)

* NuGet hata - 1.0.0-* geçerli bir sürüm dizesi - değil [#3070](https://github.com/NuGet/Home/issues/3070)

* Bul-Package başarısız görünen ancak works Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)

* Hata olduğunda "Install-Package jquery.validation" - dev15 [#3061](https://github.com/NuGet/Home/issues/3061)

* Yüklü VS 2015 sürümü 3.5.0 hatası oluşur - NuGet kullanan bir VS 3 güncelleştirdiğinizde [#3053](https://github.com/NuGet/Home/issues/3053)

* Paket Yöneticisi kullanıcı Arabirimi: bir paket güncelleştirdikten sonra yeni sürüm görüntülemez- [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey Sil komut satırında okuma/gönderilmez 3.5.0-beta içinde - [#3037](https://github.com/NuGet/Home/issues/3037)

* Yanlış dize: bir paketin kararlı bir sürüm öncesi bir bağımlılık olmamalıdır. - [#3030](https://github.com/NuGet/Home/issues/3030)

* PCL (net46 ve windows 10) proje get NullRef özel durumu oluşturuluyor. - [#3014](https://github.com/NuGet/Home/issues/3014)

* Nuget güncelleştirmesi, bilgilendirici ileti sağlamalıdır, daha yüksek bir sürüm allowedVersions kısıtlaması tarafından - sınırlı olduğunda [#3013](https://github.com/NuGet/Home/issues/3013)

* Kimlik Bilgisi Eklentisi -1 hata ile çıkıldı / kimlik bilgisi sağlayıcıları ile birden çok kaynakları - kullanırken paket indirilirken hata [#2885](https://github.com/NuGet/Home/issues/2885)

* nuget paketi - paketi bağımlılığı eksik Newtonsoft.Json - [#2876](https://github.com/NuGet/Home/issues/2876)

* Linux/MacOS + Mono - ExecuteSynchronizedCore hatada [#2860](https://github.com/NuGet/Home/issues/2860)

* VS içinde repositoryPath ortam değişkenlerini desteklemez (yapar. nuget.exe) - [#2763](https://github.com/NuGet/Home/issues/2763)

* Erişilebilirlik sorunlarını gidermek [#2745](https://github.com/NuGet/Home/issues/2745)

* Taşınabilir çerçeveleri tirelerle profilleriyle reddedilir. - [#2734](https://github.com/NuGet/Home/issues/2734)

* NuGet Paket Yöneticisi, bu seçenekler listesinde paketleri ayrıntısı için geçerli değildir Temizle olmalısınız `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* NuGet 3.3.0 güncelleştirmesi başarısız ' bir ek kısıtlama... tanımlanan packages.config bu işlemi engeller.' - [#1816](https://github.com/NuGet/Home/issues/1816)

* Sahte bir ileti - paket oluşturur mevcut olmayan bir yerel kaynaktan yükleme [#1674](https://github.com/NuGet/Home/issues/1674)

* "Yükseltme kullanılabilir" filtre gösterir - sürüm kısıtlamasını ihlal eden yükseltmeler [#1094](https://github.com/NuGet/Home/issues/1094)

## <a name="performance-improvements"></a>Performans Geliştirmeleri

* : ContentModel hedef framework ayrıştırma - performansı [#3162](https://github.com/NuGet/Home/issues/3162)

* Performans: Okuma önlemek `runtime.json` RID'ler olmayan geri yüklemeler için dosyaları [#3150](https://github.com/NuGet/Home/issues/3150). Örnek projelerimizin 15 saniye 3 saniye için ASP.NET Web uygulaması sınırlı bir CI makinelerde geri.

* Performans: Paket Yöneticisi konsolu init.ps1 yükleme süresi [#2956](https://github.com/NuGet/Home/issues/2956). Bazı durumlarda 132s'den 10'luk bloklar için PackageManagerConsole açmak zaman geliştirildi.

* NuGet güncelleştirmede - ReSharper performans sorunlarını çözün [#3044](https://github.com/NuGet/Home/issues/3044): örnek proje üzerinde paketleri yüklemek için harcanan süre sınırlı 140s 68s için.

## <a name="dcrs"></a>Dcr

* Yükseltme/yükleme tabanlı bir dotnet tfm PCL sorunları - neden olabileceğini kullanıcılarınıza gereken NuGet [#3138](https://github.com/NuGet/Home/issues/3138)

* Hatalı yüklemesi/yükseltmesi tfm ile proje için uyar = "dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)

* Netcoreapp11 ve netstandard17 desteği - ekleyerek [#2998](https://github.com/NuGet/Home/issues/2998)

* Nuget.exe içinde - konsol için NuGet uyarı üst bilgi içeriği Yazdır [#2934](https://github.com/NuGet/Home/issues/2934)

* Gücünden yararlanarak AssemblyMetadata özniteliği için `.nuspec` belirteç değiştirme - [#2851](https://github.com/NuGet/Home/issues/2851)

* Kilitli özelliğin kilit dosyanın - kaldırmak [#2379](https://github.com/NuGet/Home/issues/2379)

* Sembol paketleri yüklemede hiç kullanılmamalıdır veya #2807 güncelleştir

## <a name="features"></a>Özellikler

* Geri dönüş paket klasörleri - desteği [#2899](https://github.com/NuGet/Home/issues/2899)

* Paket türü bir kavramı destek aracı paketlerinin - tasarlayıp [#2476](https://github.com/NuGet/Home/issues/2476)

* -Genel paketleri klasörüne olan yolu almak için API [#2403](https://github.com/NuGet/Home/issues/2403)

* Yerel paketler güncelleştirmesi desteği - [#1291](https://github.com/NuGet/Home/issues/1291)
