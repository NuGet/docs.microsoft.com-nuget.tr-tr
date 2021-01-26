---
title: 3,5 RC sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 3,5 RC için sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 04ec402df5ff993b405bb710abf26e1cdc850703
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780201"
---
# <a name="nuget-35-rc-release-notes"></a>NuGet 3,5 RC sürüm notları

[NuGet 3,5-beta2 sürüm notları](../release-notes/nuget-3.5-Beta2.md)  |  [NuGet 3,5-RTM sürüm notları](../release-notes/nuget-3.5-RTM.md)

3,5 sürümü, NuGet istemcilerinin kalitesini ve performansını geliştirmeye odaklanılmıştır. Ayrıca, [geri dönüş klasörleri](https://github.com/NuGet/Home/issues/2899)için destek, ve ' de [PackageType](https://github.com/NuGet/Home/issues/2476) desteği gibi birkaç özelliği sunuyoruz `.nuspec` .

[Sorun listesi](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a>Hata Düzeltmeleri

* Bir paketin yükleme/geri yükleme işlemi "paket birden çok dosya içeriyor" ile başarısız olur `.nuspec` . - [#3231](https://github.com/NuGet/Home/issues/3231)

* NuGet paketi, `.tt` ne tür bir içeriğe bakılmaksızın dosyaları içerik klasörüne zorla ekler [#3203](https://github.com/NuGet/Home/issues/3203)

* `project.json`json dosyasında packOptions ve sahip olmadığında NuGet Pack csproj (WITH) kilitleniyor- [#3180](https://github.com/NuGet/Home/issues/3180)

* için NuGet paketi `project.json` , Summary, yazarlar, Owners vs- [#3161](https://github.com/NuGet/Home/issues/3161) gibi packoptions etiketlerini yoksayar

* NuGet paketi `.nuspec` `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145) için çıkışta bağımlılıkları yoksayar

* Birden çok paketin geri alma ile güncelleştirilmesi, projeyi bozuk bir durumda bırakır- [#3139](https://github.com/NuGet/Home/issues/3139)

* Netstandart projeler için any altındaki ContentFiles eklenmez- [#3118](https://github.com/NuGet/Home/issues/3118)

* .NET Standard için kitaplık hedeflemesi doğru paketlenemez- [#3108](https://github.com/NuGet/Home/issues/3108)

* Dosya-> yeni proje-> sınıf kitaplığı (taşınabilir) projesi VS2015 ve Dev15- [#3094](https://github.com/NuGet/Home/issues/3094) içinde başarısız oluyor

* NuGet hatası-1.0.0-* geçerli bir sürüm dizesi değil- [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-Package görüntülenemiyor ancak Install-Package çalışmaları [#3068](https://github.com/NuGet/Home/issues/3068)

* Dev15- [#3061](https://github.com/NuGet/Home/issues/3061) "Install-Package jQuery. Validation" hatası

* Bir VS 2015 güncelleştirme 3 ' ü, NuGet sürümü 3.5.0 hatası oluşursa [#3053](https://github.com/NuGet/Home/issues/3053)

* Paket Yöneticisi Kullanıcı arabirimi: bir paket güncelleştirildikten sonra yeni sürüm gösterme- [#3041](https://github.com/NuGet/Home/issues/3041)

* -Delete komut satırındaki ApiKey, 3.5.0-Beta- [#3037](https://github.com/NuGet/Home/issues/3037) içinde okunamaz/gönderilmez

* Hatalı dize: paketin kararlı bir sürümü bir ön sürüm bağımlılığı üzerinde olmamalıdır. - [#3030](https://github.com/NuGet/Home/issues/3030)

* PCL (net46 ve Windows 10) projesi oluşturma NullRef özel durumu. - [#3014](https://github.com/NuGet/Home/issues/3014)

* Daha yüksek bir sürüm allowedVersions kısıtlaması tarafından kısıtlanmışsa NuGet güncelleştirmesi bilgilendirici ileti sağlamalıdır- [#3013](https://github.com/NuGet/Home/issues/3013)

* Kimlik bilgisi eklentisi hata ile çıkıldı-1/birden çok kaynağa sahip kimlik bilgisi sağlayıcıları kullanılırken paket indirme hatası- [#2885](https://github.com/NuGet/Home/issues/2885)

* NuGet paketi-paket bağımlılığında Newtonsoft.Jseksik [#2876](https://github.com/NuGet/Home/issues/2876)

* Linux/MacOS + mono- [#2860](https://github.com/NuGet/Home/issues/2860) ExecuteSynchronizedCore 'da hata

* VS yolunda ortam değişkenlerini desteklemez (nuget.exe)- [#2763](https://github.com/NuGet/Home/issues/2763)

* Erişilebilirlik sorunlarını giderme- [#2745](https://github.com/NuGet/Home/issues/2745)

* Hecelenmiş profiller içeren taşınabilir çerçeveler reddedilir. - [#2734](https://github.com/NuGet/Home/issues/2734)

* NuGet Paket Yöneticisi, paket ayrıntılarındaki seçenekler listesinin #2665 için uygulanmadığından emin olması gerekir `project.json`  -  [](https://github.com/NuGet/Home/issues/2665)

* NuGet 3.3.0 Güncelleştirmesi ' ek bir kısıtlama ile başarısız oluyor... packages.config tanımlı bu işlemi engelliyor. ' - [#1816](https://github.com/NuGet/Home/issues/1816)

* Mevcut olmayan bir yerel kaynaktan paket yükleme, sahte bir ileti oluşturur [#1674](https://github.com/NuGet/Home/issues/1674)

* "Upgrade vailable" filtresi, sürüm kısıtlamasını ihlal eden yükseltmeleri gösterir- [#1094](https://github.com/NuGet/Home/issues/1094)

## <a name="performance-improvements"></a>Performans Geliştirmeleri

* Performans: ContentModel hedef çerçevesi ayrıştırmayı geliştirme- [#3162](https://github.com/NuGet/Home/issues/3162)

* Performans: `runtime.json` RID 'ler [#3150](https://github.com/NuGet/Home/issues/3150)olmayan geri yüklemeler Için dosyaları okumaktan kaçının. CI makinelerinde, örnek bir ASP.NET Web uygulamasının geri yüklenmesi 15 saniye ile 3 saniye arasında azaltılır.

* Performans: Paket Yöneticisi konsolu init.ps1 yükleme süresi [#2956](https://github.com/NuGet/Home/issues/2956). 1 milyon ' den 10 ' a kadar bazı durumlarda iyileştirilmiş PackageManagerConsole 'ı açma süresi.

* NuGet Update 'de ReSharper performans sorunlarını çözün- [#3044](https://github.com/NuGet/Home/issues/3044): örnek bir projede, paket 140S 'den 68s 'ye düşürüldü.

## <a name="dcrs"></a>DCR

* NuGet 'in kullanıcılara bir DotNet TFM tabanlı PCL 'de yükseltmenin/yüklemenin sorun oluşmasına neden olduğunu bilmesini sağlaması gerekir [#3138](https://github.com/NuGet/Home/issues/3138)

* "DotNet" projesi için hatalı yüklemeyi/yükseltmeyi uyar = "DotNet"- [#3137](https://github.com/NuGet/Home/issues/3137)

* Netcoreapp11 ve netstandard17 desteği ekleme- [#2998](https://github.com/NuGet/Home/issues/2998)

* nuget.exe- [#2934](https://github.com/NuGet/Home/issues/2934) NuGet-Warning üst bilgi içeriğini konsola yazdırma

* Belirteç değişiklikleri için AssemblyMetadata özniteliğiyle yararlanın `.nuspec` - [#2851](https://github.com/NuGet/Home/issues/2851)

* Kilitli özelliği kilit dosyasından kaldır- [#2379](https://github.com/NuGet/Home/issues/2379)

* Sembol paketleri, install veya Update #2807 hiçbir zaman kullanılmamalıdır

## <a name="features"></a>Özellikler

* Geri dönüş paketi klasörleri için destek- [#2899](https://github.com/NuGet/Home/issues/2899)

* Araç paketlerini desteklemek için bir paket türü kavramı tasarlama ve uygulama- [#2476](https://github.com/NuGet/Home/issues/2476)

* Genel paketler klasörünün yolunu almak için API- [#2403](https://github.com/NuGet/Home/issues/2403)

* Yerel paketler güncelleştirme desteği- [#1291](https://github.com/NuGet/Home/issues/1291)
