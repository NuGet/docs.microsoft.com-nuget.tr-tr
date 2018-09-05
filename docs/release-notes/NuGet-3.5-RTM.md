---
title: NuGet 3.5 Beta sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr NuGet 3.5 için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d8df2cb51ddcc03fb3922d9e9def17b39fccc661
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550690"
---
# <a name="nuget-35-release-notes"></a>NuGet 3.5 sürüm notları

[NuGet 3.5 RC sürüm notları](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC sürüm notları](../release-notes/nuget-4.0-RC.md)

## <a name="bug-fixes"></a>Hata Düzeltmeleri

* Paketi üzerinde mono - MSBuild 14.1 kullanmaz [#3550](https://github.com/NuGet/Home/issues/3550)

* Bunun yerine geçerli seçim yüklü sürümü - güncelleştirmek için kullanılabilir en son sürüme güncelleştirme sekmesini seçin değil [#3498](https://github.com/NuGet/Home/issues/3498)

* MyGet akışı özel bir v2 kimlik doğrulaması ve "X daha fazla sonuç Göster" düğmesini sonra kilitlenme sorunu düzeltildi- [#3469](https://github.com/NuGet/Home/issues/3469)

* Günlük iletilerini görünüyor için kullanıcı Arabirimi - ters sırada olacak şekilde [#3446](https://github.com/NuGet/Home/issues/3446)

* Nuget geri yükleme - v3.4.4 oluşturur "verilen yolun biçimi desteklenmiyor" - [#3442](https://github.com/NuGet/Home/issues/3442)

* NuGet komut satırı 3.6 beta değil dikkate - Prop yapılandırma yayın - = [#3432](https://github.com/NuGet/Home/issues/3432)

* Nuget IKVM yavaş yükleme büyük projede - [#3428](https://github.com/NuGet/Home/issues/3428)

* nuget.exe - kendi kendine tutar üzerinde güncelleştirme kendisini - güncelleştirme [#3395](https://github.com/NuGet/Home/issues/3395)

* 3.5 yükleme/geri yükleme UNC paylaşımı sahip 3.4.4 - performansı regresyon [#3355](https://github.com/NuGet/Home/issues/3355)

* Moq - net451 projesi için paket Yönetimi kullanıcı Arabirimi yüklenirken bir hata oluştu [#3349](https://github.com/NuGet/Home/issues/3349)

* Çözüm düzeyinde yükleme sekmesi, paketin sürümü - göster değil [#3339](https://github.com/NuGet/Home/issues/3339)

* xproj `project.json` güncelleştirme yüklü sekmesinden kaybetmesi durumu - [#3303](https://github.com/NuGet/Home/issues/3303)

* NuGet paketine `.csproj` boş dosyaları öğesinde yoksayar `.nuspec` dosya - [#3257](https://github.com/NuGet/Home/issues/3257)

* IIS'de barındırılan bir Web sitesi projelerini - geri yüklemenin başarısız olmasına neden [#3235](https://github.com/NuGet/Home/issues/3235)

* Kimlik bilgileri - v2 v3 uç noktası yönlendirir, Nuget.Config alınmamış [#3179](https://github.com/NuGet/Home/issues/3179)

* NuGet paketi başarısız taşınabilir derleme meta verileri - alınırken derleme çözülemedi [#3128](https://github.com/NuGet/Home/issues/3128)

* Nuget bulamıyor `msbuild.exe` Mono üzerinde- [#3085](https://github.com/NuGet/Home/issues/3085)

* nuget.exe paketi numaralarıyla - başlatan bir yayın öncesi etiketi izin vermez [#1743](https://github.com/NuGet/Home/issues/1743)

* nuget paketi yüklemesi başarısız VS2015E üzerinde - [#1298](https://github.com/NuGet/Home/issues/1298)

* allowedVersions filtre değil - çözüm düzeyinde çalışma [#333](https://github.com/NuGet/Home/issues/333)

* Geri yükleme rastgele başarısız olan bir öğe ile aynı anahtar zaten eklendi. - [#2646](https://github.com/NuGet/Home/issues/2646)

* İçinde Nuget.Common yükleyemezsiniz `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)

* V2 kaynak aramak için kullanıcı arabirimini kullanarak, iki kez her kimliği için - FindPackagesById çağrılır [#2517](https://github.com/NuGet/Home/issues/2517)

* Paketleri projelerde - bağlı olamaz [#2490](https://github.com/NuGet/Home/issues/2490)

* -Exclude belgelenen ancak desteklenmiyor - nuget.exe paketi [#2284](https://github.com/NuGet/Home/issues/2284)

* Hata ile ilgili sorunlar iletileri 'contentFiles' bölümünü `.nuspec` geçersiz - [#1686](https://github.com/NuGet/Home/issues/1686)

* Anında iletme her zaman gönderdiği tüm paket iki kez ile kimliği doğrulanmış paket kaynaklarını - [#1501](https://github.com/NuGet/Home/issues/1501)

* Proje sırasında nuget.exe güncelleştirme *.csproj çağırma yoksa hiçbir bilgi verilen bir `packages.config`  -  [#1496](https://github.com/NuGet/Home/issues/1496)

* `packages.config` geri yükleme - V2 kaynaklardan 5xx durum kodları yeniden [#1217](https://github.com/NuGet/Home/issues/1217)

* Dosya src içine çift nokta `.nuspec` işe yaramazsa - [#2947](https://github.com/NuGet/Home/issues/2947)

* Şifreleme - akışlarıyla yoksay gerekiyor CoreCLR geri yükleme [#2942](https://github.com/NuGet/Home/issues/2942)

* nuget.exe push - yanlış kimlik bilgileri istendiği - 403 işleme [#2910](https://github.com/NuGet/Home/issues/2910)

* NuGet Paket Yöneticisi Update'de kaldırır özelliklerinden `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)

* NuGet.PackageManagement.VisualStudio deneyin "NuGet.TeamFoundationServer14" ancak DLL adı "NuGet.TeamFoundationServer" - değiştiğini yüklenecek [#2857](https://github.com/NuGet/Home/issues/2857)

* Paket Yöneticisi UI olmayan Göster yeni güncelleştirilmiş sürümünü - [#2828](https://github.com/NuGet/Home/issues/2828)

* Update-package PackageId, kullanmayı denemek yerine package.version - sürüm [#2771](https://github.com/NuGet/Home/issues/2771)

* nuget geri yükleme csproj proje nuget kullanıyorsa hata gerekir (`packages.config` veya `project.json`)- [#2766](https://github.com/NuGet/Home/issues/2766)

* TFS hata "[file] çalışma alanınızda bulunan olmaması ya da ona erişmek için izniniz yok" sırasında yükseltme veya çözüm/proje - TFS kaynak denetimine bağlı olduğunda kaldırma [#2739](https://github.com/NuGet/Home/issues/2739)

* güncelleştirme paketi hedef olmayan paketler - bağımlılıkları açılmıyor [#2724](https://github.com/NuGet/Home/issues/2724)

* Nuget Paket Yöneticisi UI eylemlerini - günlükleri ayrıntı düzeyini ayarlamak için bir yolu yoktur [#2705](https://github.com/NuGet/Home/issues/2705)

* nuget yapılandırması geçersiz - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)

* İçinde DefaultPushSource `NuGetDefaults.Config` (`ProgramData\NuGet`) işe yaramazsa - [#2653](https://github.com/NuGet/Home/issues/2653)

* nuget 3.4.3 yayın - değer alma üzerinde paket derleme - null olamaz [#2648](https://github.com/NuGet/Home/issues/2648)

* geri yükleme için VSTS akışlarındaki - Nuget.Config depolanan kimlik bilgilerini değil kullanıyor [#2647](https://github.com/NuGet/Home/issues/2647)

* [dotnet restore]--configfile olan cmd dir - yerine Proje dizini göreli [#2639](https://github.com/NuGet/Home/issues/2639)

* Sürüm karşılaştırma kodu - aşırı ayırma [#2632](https://github.com/NuGet/Home/issues/2632)

* Nuget.exe aynı yüklemeye çalışan birden çok örneği paralel nedenlerdeki çift yazma - paket [#2628](https://github.com/NuGet/Home/issues/2628)

* Birden çok proje işlemleri için - bağımlılık bilgileri önbelleğe alınmaz [#2619](https://github.com/NuGet/Home/issues/2619)

* Yükleme ve güncelleştirme yükleme paketleri denetlemeden önce - packages klasörünü [#2618](https://github.com/NuGet/Home/issues/2618)

* Paket kaynak liste boşsa, kullanıcı Arabirimi aracılığıyla, paket kaynağına eklenemiyor (NuGet 3.4.x)- [#2617](https://github.com/NuGet/Home/issues/2617)

* Tasarım zamanı cepheleri üzerinde - bağlıdır paket yüklemeye çalışırken hata yanıltıcı [#2594](https://github.com/NuGet/Home/issues/2594)

* "Tüm" ayarı ile PackageManager konsolundan bir paket yükleme, yalnızca ilk kaynak - çalışır [#2557](https://github.com/NuGet/Home/issues/2557)

* En son beta değil sıkıştırması açılırken ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)

* Başlangıçta kendi NuGet 3.4.1 - VS2015 kilitlenme [#2419](https://github.com/NuGet/Home/issues/2419)

* Güncelleştirme komut i dizininiz.. - olmasını isteyin, biraz daha ayrıntılı olabilir [#2418](https://github.com/NuGet/Home/issues/2418)

* Yerel olarak oluşturulmuş VSIX CI derleme olarak aynı DLL'ler ve dosyaları olmalıdır. - [#2401](https://github.com/NuGet/Home/issues/2401)

* Yapı - NuGet indirgeme uyarıları düzeltin [#2396](https://github.com/NuGet/Home/issues/2396)

* Paket kaynağı (3 kez) kimlik doğrulaması gerçekleştiremeyen engellenir sonsuza kadar - [#2362](https://github.com/NuGet/Home/issues/2362)

* Paket içeriğini yüklenemez doğru bir paket bir nuget v3.3 + yükleme bağımsız değişkeniyle akışı güncelleştirildiğinde - NoCache paketi içeriyorsa `.nupkg` dosyalar - [#2354](https://github.com/NuGet/Home/issues/2354)

* Paket kaynaklarının tümüne, ancak 1 kaynağından eksik paketi ile Nuget yüklemesi başarısız - [#2322](https://github.com/NuGet/Home/issues/2322)

* [PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll! NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+*lt; &gt;c__DisplayClass_0 +&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)

* Tek bir kaynak yetkilendirme - başarısız olursa blokları yükleme [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` Sürüm - IncludeReferencedProjects sürüm - aralık geçersiz kılmalıdır [#1983](https://github.com/NuGet/Home/issues/1983)

* Update-Package Süper yavaş - "bağımlılıkları bilgileri toplanmaya çalışılırken" - [#1909](https://github.com/NuGet/Home/issues/1909)

* NuGet gizli eski sürümü yükleme işlemleri paketini batch bağımlılıklarını - güncelleştirme [#1903](https://github.com/NuGet/Home/issues/1903)

* nuget.exe güncelleştirme derleme tanımlayıcı adı ve özel öznitelik bırakır. - [#1778](https://github.com/NuGet/Home/issues/1778)

* Göreli dosya yolu için "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)

* Çözümleyici hatası iletileri - geliştirmek [#1373](https://github.com/NuGet/Home/issues/1373)

* Update-package v3 başarısız değil, belirtilen kaynak - paketleriyle [#1013](https://github.com/NuGet/Home/issues/1013)

* Göreli yollar için paket kaynaklarını kullanan kullanılacak - sorunlu [#865](https://github.com/NuGet/Home/issues/865)

* Eksik bağımlılık NUPKG dosyasında daha düşük bir sürüm gereksinimi ile - dolaylı bir bağımlılığı varsa projeden oluşturulan [#759](https://github.com/NuGet/Home/issues/759)

* Bir proje silme karşılık gelen kullanıcı Arabirimi penceresi kapanır, ancak bir projesinin yeniden adlandırılması UI pencere adlandırmaz. PMC projeyi yeniden adlandırma ve kaldırma olayları proje - dinler Not [#670](https://github.com/NuGet/Home/issues/670)

* [Willow Web iş yükü] Razor v3 WSP oluşturma askıda - [#3241](https://github.com/NuGet/Home/issues/3241)

* "Paket birden çok nuspec dosyaları içeren ile." belirli bir paketin yükleme/geri yükleme başarısız - [#3231](https://github.com/NuGet/Home/issues/3231)

* Küçük harf kimlikleri & `packages.config` senaryoları - [#3209](https://github.com/NuGet/Home/issues/3209)

* [3.5-beta2] Paket geri yükleme başarısız - "eski" paketlerini geri yüklemek [#3208](https://github.com/NuGet/Home/issues/3208)

* nuget paketi zorla ekler .tt dosyaları içerik klasörüne - ne olursa olsun [#3203](https://github.com/NuGet/Home/issues/3203)

* güncelleştirme paketi, ASP.NET web uygulamasının dosyayla ilgili bir uyarı üretir: kaynak - [#3194](https://github.com/NuGet/Home/issues/3194)

* nuget paketi csproj (ile `project.json`) hiçbir packOptions ve JSON dosyasında - sahibi varsa kilitleniyor [#3180](https://github.com/NuGet/Home/issues/3180)

* nuget paketi için `project.json` packOptions etiketleri özeti, yazarlar, sahipleri - vb. gibi yoksayar [#3161](https://github.com/NuGet/Home/issues/3161)

* NullReferenceException NuGet.Packaging.PhysicalPackageFile.GetStream - aracılığıyla [#3160](https://github.com/NuGet/Home/issues/3160)

* NuGet paketi yoksayar çıkış bağımlılıkları `.nuspec` için `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* Geri alma ile birden çok paketlerin güncelleştirilmesi, bozuk bir durumda - proje bırakır [#3139](https://github.com/NuGet/Home/issues/3139)

* ContentFiles herhangi netstandard projeleri için - eklenmedi [#3118](https://github.com/NuGet/Home/issues/3118)

* Kitaplık .net targeting paketlenemiyor standart doğru - [#3108](https://github.com/NuGet/Home/issues/3108)

* Dosya -> Yeni Proje -> sınıf kitaplığı (taşınabilir) proje başarısız VS2015 ve - Dev15 [#3094](https://github.com/NuGet/Home/issues/3094)

* NuGet hata - 1.0.0-* geçerli bir sürüm dizesi - değil [#3070](https://github.com/NuGet/Home/issues/3070)

* Bul-Package başarısız görünen ancak works Install-Package - [#3068](https://github.com/NuGet/Home/issues/3068)

* Hata olduğunda "Install-Package jquery.validation" - dev15 [#3061](https://github.com/NuGet/Home/issues/3061)

* xproj nuget paketi için geçersiz hedef yol - varsayarak [#3060](https://github.com/NuGet/Home/issues/3060)

* Yüklü VS 2015 sürümü 3.5.0 hatası oluşur - NuGet kullanan bir VS 3 güncelleştirdiğinizde [#3053](https://github.com/NuGet/Home/issues/3053)

* "Packages.config tarafından engellenir" `project.json` (UWP, tümleşik a.k.a derleme) takım projesi - [#3046](https://github.com/NuGet/Home/issues/3046)

* dotnet CLI resmi preview2 derleme preview2-003121, yapı komut dosyası tarafından yüklenen güncelleştirin. - [#3045](https://github.com/NuGet/Home/issues/3045)

* Paket Yöneticisi kullanıcı Arabirimi: bir paket güncelleştirdikten sonra yeni sürüm görüntülemez- [#3041](https://github.com/NuGet/Home/issues/3041)

* -ApiKey Sil komut satırında okuma/gönderilmez 3.5.0-beta içinde - [#3037](https://github.com/NuGet/Home/issues/3037)

* Yanlış dize: bir paketin kararlı bir sürüm öncesi bir bağımlılık olmamalıdır. - [#3030](https://github.com/NuGet/Home/issues/3030)

* Boş klasörler - OptimizedZipPackage önbellek bırakır [#3029](https://github.com/NuGet/Home/issues/3029)

* PCL (net46 ve windows 10) proje get NullRef özel durumu oluşturuluyor. - [#3014](https://github.com/NuGet/Home/issues/3014)

* Nuget güncelleştirmesi, bilgilendirici ileti sağlamalıdır, daha yüksek bir sürüm allowedVersions kısıtlaması tarafından - sınırlı olduğunda [#3013](https://github.com/NuGet/Home/issues/3013)

* Nuget v3 geri yükleme sorunları - [#2891](https://github.com/NuGet/Home/issues/2891)

* Kimlik Bilgisi Eklentisi -1 hata ile çıkıldı / kimlik bilgisi sağlayıcıları ile birden çok kaynakları - kullanırken paket indirilirken hata [#2885](https://github.com/NuGet/Home/issues/2885)

* `project.json` nuget geri yükleme neden olan bir şey olduğunda değiştirilen - yeniden derleme [#2817](https://github.com/NuGet/Home/issues/2817)

* Sembol paketleri sürekli olmamalıdır yükleme veya güncelleştirme - kullanılan [#2807](https://github.com/NuGet/Home/issues/2807)

* VS içinde repositoryPath ortam değişkenlerini desteklemez (yapar. nuget.exe) - [#2763](https://github.com/NuGet/Home/issues/2763)

* Paket Yöneticisi kullanıcı arabiriminde etiketlenmemiş Uıelements'i için erişilebilirlik - etiket [#2745](https://github.com/NuGet/Home/issues/2745)

* Taşınabilir çerçeveleri tirelerle profilleriyle reddedilir. - [#2734](https://github.com/NuGet/Home/issues/2734)

* NuGet Paket Yöneticisi, bu seçenekler listesinde paketleri ayrıntısı için geçerli değildir Temizle olmalısınız `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* nuget.exe anında iletme/silme, API anahtarı - kullanmayacağınız [#2627](https://github.com/NuGet/Home/issues/2627)

* Kilitli özelliğin kilit dosyanın - kaldırmak [#2379](https://github.com/NuGet/Home/issues/2379)

* NuGet 3.3.0 güncelleştirmesi başarısız ' bir ek kısıtlama... tanımlanan packages.config bu işlemi engeller.' - [#1816](https://github.com/NuGet/Home/issues/1816)

* Sahte bir ileti - paket oluşturur mevcut olmayan bir yerel kaynaktan yükleme [#1674](https://github.com/NuGet/Home/issues/1674)

* "Yükseltme kullanılabilir" filtre gösterir - sürüm kısıtlamasını ihlal eden yükseltmeler [#1094](https://github.com/NuGet/Home/issues/1094)

* Yerel paketler - güncelleştirilemiyor [#1291](https://github.com/NuGet/Home/issues/1291)


## <a name="features"></a>Özellikler

* NuGet tarafından - eklenen başvuruları false ayarı CopyLocal desteği [#329](https://github.com/NuGet/Home/issues/329)

* MSBuild 15 - nuget.exe desteği [#1937](https://github.com/NuGet/Home/issues/1937)

* Paketi desteği.`csproj` + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)

* Yürütülmekte olan kullanıcı eylemlerini olduğunda kullanıcı eylemini devre dışı bırak- [#1440](https://github.com/NuGet/Home/issues/1440)

* NuGet için destek ekleme `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)

* Framework uyumluluğunu eksik Nuget'te ekleyin (Bu durumda 3.x içinde) 2.x - [#2720](https://github.com/NuGet/Home/issues/2720)

* Geri dönüş paket klasörleri - desteği [#2899](https://github.com/NuGet/Home/issues/2899)

* Paket türü bir kavramı destek aracı paketlerinin - tasarlayıp [#2476](https://github.com/NuGet/Home/issues/2476)

* -Genel paketleri klasörüne olan yolu almak için bir API eklemek [#2403](https://github.com/NuGet/Home/issues/2403)

* Pack - SemVer 2.0.0 etkinleştirme [#3356](https://github.com/NuGet/Home/issues/3356)

## <a name="dcrs"></a>Dcr

* nuget.exe push - zaman aşımı parametresi işe yaramazsa - [#2785](https://github.com/NuGet/Home/issues/2785)

* Paket açıklaması metni seçilebilir - [#1769](https://github.com/NuGet/Home/issues/1769)

* Nuget.exe üretmek etkinleştirme `.props` ve `.targets` dosyaları `.nuproj` projeleri [#2711](https://github.com/NuGet/Home/issues/2711)

* Genişletilebilirlik çerçeveleri içeri aktarmalar ile-karşılaştırmak için API Ekle [#2633](https://github.com/NuGet/Home/issues/2633)

* Bağımlılık seçeneklerini kullanırken Gizle `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Nuget.exe sürüm üst bilgisi içinde ayrıntılı çıkış - out yazdırma [#1887](https://github.com/NuGet/Home/issues/1887)

* Yükseltme/yükleme tabanlı bir dotnet tfm PCL sorunları - neden olabileceğini kullanıcılarınıza gereken NuGet [#3138](https://github.com/NuGet/Home/issues/3138)

* Hatalı yüklemesi/yükseltmesi tfm ile proje için uyar = "dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)

* Güncelleştirmesi için - ReShaper ve NuGet ile performans sorunlarını çözün [#3044](https://github.com/NuGet/Home/issues/3044)

* Netcoreapp11 ve netstandard17 desteği - ekleyerek [#2998](https://github.com/NuGet/Home/issues/2998)

* Gücünden yararlanarak AssemblyMetadata özniteliği için `.nuspec` belirteç değiştirme - [#2851](https://github.com/NuGet/Home/issues/2851)
