---
title: NuGet 3.5 Beta sürüm notları
description: NuGet bilinen sorunları, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere 3.5 için sürüm notları.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cdb540229cae0e6e952ac2a0c00c8801ccbbb28d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822597"
---
# <a name="nuget-35-release-notes"></a>NuGet 3.5 sürüm notları

[NuGet 3.5 RC sürüm notları](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC sürüm notları](../release-notes/nuget-4.0-RC.md)

## <a name="bug-fixes"></a>Hata Düzeltmeleri

* Paketi mono üzerinde - MSBuild 14.1 kullanıyorsanız değil [#3550](https://github.com/NuGet/Home/issues/3550)

* Bunun yerine select geçerli yüklü sürümü - güncelleştirmek için en son sürüme güncelleştirme sekmesini seçin değil [#3498](https://github.com/NuGet/Home/issues/3498)

* Kilitlenme MyGet akış özel v2 kimlik doğrulaması ve "Daha fazla sonuç x Göster" düğmesini sonra düzeltme- [#3469](https://github.com/NuGet/Home/issues/3469)

* Günlük iletilerini gözükmüyor ters sırada için kullanıcı Arabirimi - [#3446](https://github.com/NuGet/Home/issues/3446)

* V3.4.4 - Nuget restore oluşturur "verilen yolun biçimi desteklenmiyor" - [#3442](https://github.com/NuGet/Home/issues/3442)

* NuGet cmdLine 3.6 beta dikkate almayabilir - Prop yapılandırma yayın - = [#3432](https://github.com/NuGet/Home/issues/3432)

* Nuget IKVM yavaş yüklemek büyük projede - [#3428](https://github.com/NuGet/Home/issues/3428)

* nuget.exe - Self tutar üzerinde güncelleştirme kendisini - güncelleştirme [#3395](https://github.com/NuGet/Home/issues/3395)

* 3.5 yükleme/geri yükleme UNC paylaşımından sahip performansı regresyon 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)

* Moq net451 proje - paket Yönetimi kullanıcı Arabirimi yüklenirken bir hata oluştu [#3349](https://github.com/NuGet/Home/issues/3349)

* Çözüm düzeyinde yükleme sekmesini paketin sürümü - göster değil [#3339](https://github.com/NuGet/Home/issues/3339)

* xproj `project.json` yüklü sekmesinden güncelleştirme durumunu - kaybederse [#3303](https://github.com/NuGet/Home/issues/3303)

* NuGet paketine `.csproj` boş dosyaları öğesinde yoksayar `.nuspec` dosyası - [#3257](https://github.com/NuGet/Home/issues/3257)

* IIS barındırılan Web sitesi projelerine neden olmaz geri yükleme başarısız olmasına - [#3235](https://github.com/NuGet/Home/issues/3235)

* Kimlik bilgileri v3 uç noktası için v2 - yönlendirildiklerinde Nuget.Config alınmamış [#3179](https://github.com/NuGet/Home/issues/3179)

* NuGet paketi başarısız taşınabilir derleme meta verilerini - alınırken derleme çözülemedi [#3128](https://github.com/NuGet/Home/issues/3128)

* Nuget bulamıyor `msbuild.exe` Mono üzerinde- [#3085](https://github.com/NuGet/Home/issues/3085)

* nuget.exe paketi numaralarıyla - başlayan bir yayım öncesi etiketi izin vermez [#1743](https://github.com/NuGet/Home/issues/1743)

* nuget paketi yüklemesi başarısız VS2015E üzerinde - [#1298](https://github.com/NuGet/Home/issues/1298)

* allowedVersions filtre değil çalışma çözüm düzeyinde - [#333](https://github.com/NuGet/Home/issues/333)

* Geri yükleme rastgele başarısız bir öğesiyle aynı anahtarı zaten eklenmiş. - [#2646](https://github.com/NuGet/Home/issues/2646)

* İçinde Nuget.Common yükleyemezsiniz `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)

* Kullanıcı arabirimini kullanarak V2 kaynak aramak için iki kez her kimliği için - FindPackagesById adlı [#2517](https://github.com/NuGet/Home/issues/2517)

* Paketler projelerde - bağımlı [#2490](https://github.com/NuGet/Home/issues/2490)

* -Exclude belgelenen ancak desteklenmiyor - nuget.exe paketi [#2284](https://github.com/NuGet/Home/issues/2284)

* Hata ile ilgili sorunları iletileri 'Content ' dosyaları bölümünü `.nuspec` geçersiz - [#1686](https://github.com/NuGet/Home/issues/1686)

* Anında iletme her zaman gönderir tüm paketi iki kez ile kimlik doğrulaması paket kaynaklarını - [#1501](https://github.com/NuGet/Home/issues/1501)

* Proje sırasında nuget.exe güncelleştirme *.csproj çağırma olmadığı zaman hiçbir bilgi verilen bir `packages.config`  -  [#1496](https://github.com/NuGet/Home/issues/1496)

* `packages.config` geri yükleme 5xx durum kodları V2 kaynaklardan - yeniden [#1217](https://github.com/NuGet/Home/issues/1217)

* Dosya src çift nokta `.nuspec` çalışmıyor - [#2947](https://github.com/NuGet/Home/issues/2947)

* CoreCLR geri yükleme gereken şifreleme - akışlarıyla yoksaymak [#2942](https://github.com/NuGet/Home/issues/2942)

* nuget.exe push - yanlış kimlik bilgileri - 403 işleme [#2910](https://github.com/NuGet/Home/issues/2910)

* NuGet Paket Yöneticisi Update'de kaldırır özelliklerinden `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)

* NuGet.PackageManagement.VisualStudio deneyin "NuGet.TeamFoundationServer14" ancak DLL adı "NuGet.TeamFoundationServer" - değiştirilen yüklemek [#2857](https://github.com/NuGet/Home/issues/2857)

* Paket Yöneticisi kullanıcı Arabirimi olmayan Göster yeni güncelleştirilmiş sürümünü - [#2828](https://github.com/NuGet/Home/issues/2828)

* güncelleştirme paketi PackageId, kullanmayı denemek yerine package.version - sürüm [#2771](https://github.com/NuGet/Home/issues/2771)

* nuget restore csproj gereken hata nuget proje kullanıyorsa (`packages.config` veya `project.json`)- [#2766](https://github.com/NuGet/Home/issues/2766)

* TFS hata "[dosya] çalışma alanında bulunan olmaması veya erişmek için izniniz yok" sırasında yükseltmeniz veya kaldırmanız için TFS kaynak denetimindeki - çözüm/proje bağlandığında [#2739](https://github.com/NuGet/Home/issues/2739)

* güncelleştirme paketi hedef olmayan paket için-bağımlılıklar açılmıyor [#2724](https://github.com/NuGet/Home/issues/2724)

* Nuget Paket Yöneticisi kullanıcı Arabirimi eylemlerini - günlükleri ayrıntı düzeyini ayarlamak için bir yolu yoktur [#2705](https://github.com/NuGet/Home/issues/2705)

* nuget yapılandırması geçersiz - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)

* İçinde DefaultPushSource `NuGetDefaults.Config` (`ProgramData\NuGet`) çalışmıyor - [#2653](https://github.com/NuGet/Home/issues/2653)

* nuget 3.4.3 yayın - değerini alırken üzerinde paket oluşturma - null olamaz [#2648](https://github.com/NuGet/Home/issues/2648)

* geri yükleme için VSTS akışları - Nuget.Config depolanan kimlik bilgilerini değil kullanıyor [#2647](https://github.com/NuGet/Home/issues/2647)

* [dotnet geri yükleme]--configfile olan proje dir cmd dir - yerine göre [#2639](https://github.com/NuGet/Home/issues/2639)

* Sürüm karşılaştırma kodu - aşırı ayırma [#2632](https://github.com/NuGet/Home/issues/2632)

* Birden çok örneğini aynı yüklemeye çalıştığınız nuget.exe içinde paralel nedenler çift yazma - paketini [#2628](https://github.com/NuGet/Home/issues/2628)

* Birden çok proje işlemleri için - bağımlılık bilgileri önbelleğe alınmaz [#2619](https://github.com/NuGet/Home/issues/2619)

* Yükleme ve güncelleştirme yükleme paketleri paketler klasörü önce - denetlemeden [#2618](https://github.com/NuGet/Home/issues/2618)

* Paket kaynak liste boşsa, kullanıcı Arabirimi aracılığıyla paket kaynağı eklenemiyor (NuGet 3.4.x)- [#2617](https://github.com/NuGet/Home/issues/2617)

* Tasarım zamanı cepheleri üzerinde - bağlıdır paketini yüklemeye çalışırken hata yanıltıcı [#2594](https://github.com/NuGet/Home/issues/2594)

* Bir paketi "Tümü" ayar PackageManager konsolundan yükleme çalışır yalnızca ilk kaynak - [#2557](https://github.com/NuGet/Home/issues/2557)

* Değil olan son beta ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)

* Kendi kendine yerleşik NuGet 3.4.1 - başlangıçta VS2015 kilitlenme [#2419](https://github.com/NuGet/Home/issues/2419)

* Güncelleştirme komutu i gerçekleştiremezler... - olmasını isteyin, biraz daha ayrıntılı olabilir [#2418](https://github.com/NuGet/Home/issues/2418)

* Yerel olarak oluşturulmuş VSIX aynı DLL'ler ve dosyaları CI yapı olması gerekir. - [#2401](https://github.com/NuGet/Home/issues/2401)

* Yapı - NuGet indirgeme uyarılarını düzeltmenize [#2396](https://github.com/NuGet/Home/issues/2396)

* Paket kaynağı (3 kez) kimlik doğrulaması gerçekleştiremeyen engellenmiş sonsuza kadar - [#2362](https://github.com/NuGet/Home/issues/2362)

* Paket içeriğini yüklenemez doğru bir paket bir nuget v3.3 +'dan yükleme bağımsız değişkeniyle akış zaman - NoCache paketi içeriyorsa `.nupkg` dosyaları - [#2354](https://github.com/NuGet/Home/issues/2354)

* Tüm paket kaynaklarını, ancak paket 1 kaynağından eksik olan Nuget yükleme başarısız - [#2322](https://github.com/NuGet/Home/issues/2322)

* [PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll! NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+*lt; &gt;c__DisplayClass_0 +&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)

* Tek bir kaynak yetkilendirme - blokları yükleyin [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` Aralık - IncludeReferencedProjects sürümü - geçersiz kıl sürüm [#1983](https://github.com/NuGet/Home/issues/1983)

* Güncelleştirme paketi Süper yavaş - "bağımlılık bilgileri toplanmaya çalışılıyor" - [#1909](https://github.com/NuGet/Home/issues/1909)

* Gizlilik downgrades NuGet paketini toplu bağımlılıklarını - güncelleştirme [#1903](https://github.com/NuGet/Home/issues/1903)

* nuget.exe güncelleştirme derleme tanımlayıcı adı ve özel öznitelik bırakır. - [#1778](https://github.com/NuGet/Home/issues/1778)

* "DefaultPushSource" - için göreli dosya yolu [#1746](https://github.com/NuGet/Home/issues/1746)

* Çözümleyici hata iletileri - artırmak [#1373](https://github.com/NuGet/Home/issues/1373)

* v3 güncelleştirme paketine başarısız değil, belirtilen kaynak - paketleriyle [#1013](https://github.com/NuGet/Home/issues/1013)

* Paket kaynaklarını için göreli yollar kullanılarak kullanılacak - sorunlu [#865](https://github.com/NuGet/Home/issues/865)

* Eksik bağımlılık NUPKG dosyasına dolaylı bağımlılık ile daha düşük bir sürüm gereksinimini - zaten varsa projeden oluşturulan [#759](https://github.com/NuGet/Home/issues/759)

* Bir projeyi silmek, karşılık gelen UI penceresi kapanır, ancak projeyi yeniden adlandırma UI pencere yeniden adlandırmak değil. Not PMC projeyi yeniden adlandırma ile proje kaldırma olaylarını - dinler [#670](https://github.com/NuGet/Home/issues/670)

* [Willow Web iş yükü] Razor v3 WSP oluşturma askıda - [#3241](https://github.com/NuGet/Home/issues/3241)

* "Birden fazla nuspec dosyası pakette ile." belirli bir paketin yükleme/geri yükleme başarısız olur - [#3231](https://github.com/NuGet/Home/issues/3231)

* Küçük harf kimlikleri & `packages.config` senaryoları - [#3209](https://github.com/NuGet/Home/issues/3209)

* [3.5-beta2] Paket geri yüklemesi başarısız "eski" paketlerini - geri yüklemek [#3208](https://github.com/NuGet/Home/issues/3208)

* nuget paketi zorla ekler .tt dosyaları içerik klasörüne - ne olursa olsun [#3203](https://github.com/NuGet/Home/issues/3203)

* güncelleştirme paketi, ASP.NET web uygulaması oluşturur dosyasına ilgili uyarı: kaynak - [#3194](https://github.com/NuGet/Home/issues/3194)

* nuget paketi csproj (ile `project.json`) hiçbir packOptions ve JSON dosyasında - sahibi varsa çöküyor [#3180](https://github.com/NuGet/Home/issues/3180)

* nuget paketini `project.json` packOptions etiketleri özeti, yazarlar, sahipleri vb. - gibi yoksayar [#3161](https://github.com/NuGet/Home/issues/3161)

* NullReferenceException NuGet.Packaging.PhysicalPackageFile.GetStream - aracılığıyla [#3160](https://github.com/NuGet/Home/issues/3160)

* NuGet paketi yoksayar çıkış bağımlılıkları `.nuspec` için `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)

* Bozuk durumda - bırakır projeyi geri alma ile birden çok paket güncelleştirme [#3139](https://github.com/NuGet/Home/issues/3139)

* Content altında bulunan dosyaları netstandard projelerde - eklenmedi [#3118](https://github.com/NuGet/Home/issues/3118)

* .NET hedefleme kitaplığı paketleyemez standart doğru - [#3108](https://github.com/NuGet/Home/issues/3108)

* Dosya -> Yeni Proje VS2015 ve Dev15 - sınıf kitaplığı (taşınabilir) proje başarısız -> [#3094](https://github.com/NuGet/Home/issues/3094)

* nuGet hata - 1.0.0-* geçerli bir sürüm dizesi - değil [#3070](https://github.com/NuGet/Home/issues/3070)

* Bul-Package başarısız görünen ancak Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)

* Hata olduğunda "Install-Package jquery.validation" dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)

* xproj nuget paketi için geçersiz hedef yol - varsayarak [#3060](https://github.com/NuGet/Home/issues/3060)

* Yüklü VS 2015 sürüm 3.5.0 hatası oluşur - NuGet kullanan bir VS 3 güncelleştirdiğinizde [#3053](https://github.com/NuGet/Home/issues/3053)

* "Packages.config tarafından engellendi" `project.json` (UWP, tümleşik a.k.a yapı) proje - [#3046](https://github.com/NuGet/Home/issues/3046)

* Resmi preview2 yapıdır preview2-003121, yapı komut dosyası tarafından yüklenen dotnet CLI güncelleştirin. - [#3045](https://github.com/NuGet/Home/issues/3045)

* Paket Yöneticisi kullanıcı Arabirimi: bir paket güncelleştirdikten sonra yeni sürümü görüntülemez- [#3041](https://github.com/NuGet/Home/issues/3041)

* -Apikey ile yapılan Sil komut satırında okuma/gönderilmez 3.5.0-beta içinde - [#3037](https://github.com/NuGet/Home/issues/3037)

* Yanlış dize: bir paketin durağan sürümü bir ön sürüm bağımlılığı olmamalıdır. - [#3030](https://github.com/NuGet/Home/issues/3030)

* OptimizedZipPackage önbellek bırakır boş klasörler - [#3029](https://github.com/NuGet/Home/issues/3029)

* PCL (net46 ve windows 10) proje get NullRef özel durum oluşturuluyor. - [#3014](https://github.com/NuGet/Home/issues/3014)

* Daha yüksek bir sürüm allowedVersions kısıtlaması tarafından - sınırlı olduğunda, Nuget güncelleştirme bilgilendirici ileti temin etmelidir [#3013](https://github.com/NuGet/Home/issues/3013)

* Nuget v3 geri yükleme sorunları - [#2891](https://github.com/NuGet/Home/issues/2891)

* Kimlik Bilgisi Eklentisi -1 hata ile çıkıldı / hata indirme paketini kimlik bilgisi sağlayıcıları birden çok kaynaklarıyla - kullanırken [#2885](https://github.com/NuGet/Home/issues/2885)

* `project.json` nuget restore neden olan bir şey olduğunda değiştirilen - yeniden derlenmek [#2817](https://github.com/NuGet/Home/issues/2817)

* Simgeler paketleri hiç olmamalıdır yükleme veya güncelleştirme - kullanılan [#2807](https://github.com/NuGet/Home/issues/2807)

* VS repositoryPath içinde ortam değişkenlerini desteklemez (nuget.exe yapar) - [#2763](https://github.com/NuGet/Home/issues/2763)

* Paket Yöneticisi arabiriminde etiketlenmemiş UIElements için erişilebilirlik - etiket [#2745](https://github.com/NuGet/Home/issues/2745)

* Tirelenmiş profilleriyle taşınabilir çerçeveleri reddedilir. - [#2734](https://github.com/NuGet/Home/issues/2734)

* NuGet Paket Yöneticisi, bu paketleri ayrıntı için geçerli olmayan Seçenekler listesinde temizleyin olmalısınız `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)

* nuget.exe itme/silme, API anahtarı - kullanmayacağınız [#2627](https://github.com/NuGet/Home/issues/2627)

* Kilit dosyasından - kilitli özelliği kaldırmak [#2379](https://github.com/NuGet/Home/issues/2379)

* NuGet 3.3.0 güncelleştirme başarısız olan '... ek kısıtlama tanımlanan packages.config bu işlemi engelliyor.' - [#1816](https://github.com/NuGet/Home/issues/1816)

* Sahte bir ileti - paketini atar mevcut olmayan yerel bir kaynaktan yükleme [#1674](https://github.com/NuGet/Home/issues/1674)

* "Kullanılabilir yükseltme" filtre gösterir - sürüm kısıtlamayı ihlal yükseltmeler [#1094](https://github.com/NuGet/Home/issues/1094)

* Yerel paketler - güncelleştirilemiyor [#1291](https://github.com/NuGet/Home/issues/1291)


## <a name="features"></a>Özellikler

* NuGet tarafından - eklenen başvuruları false ayarı CopyLocal desteği [#329](https://github.com/NuGet/Home/issues/329)

* MSBuild 15 - nuget.exe desteği [#1937](https://github.com/NuGet/Home/issues/1937)

* Paketi desteği.`csproj` + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)

* Yürütülmekte olan kullanıcı eylemlerini olduğunda kullanıcı eylemi devre dışı bırak- [#1440](https://github.com/NuGet/Home/issues/1440)

* NuGet desteği ekleme `runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)

* NuGet içinde eksik framework uyumluluğunu ekleyin (olan zaten 3.x içinde) 2.x - [#2720](https://github.com/NuGet/Home/issues/2720)

* Geri dönüş paketi klasörlerinin - desteği [#2899](https://github.com/NuGet/Home/issues/2899)

* Aracı paketler - desteklemek için paket türü kavramını tasarlayıp [#2476](https://github.com/NuGet/Home/issues/2476)

* Genel paketler klasörüne - yolu bir API ekleme [#2403](https://github.com/NuGet/Home/issues/2403)

* SemVer 2.0.0 paketinde - etkinleştirmek [#3356](https://github.com/NuGet/Home/issues/3356)

## <a name="dcrs"></a>Dcr

* nuget.exe push - zaman aşımı parametresi işe yaramazsa - [#2785](https://github.com/NuGet/Home/issues/2785)

* Paket açıklama metnini seçilebilir - [#1769](https://github.com/NuGet/Home/issues/1769)

* Üretmek nuget.exe etkinleştirmek `.props` ve `.targets` dosyalarını `.nuproj` projeleri [#2711](https://github.com/NuGet/Home/issues/2711)

* Genişletilebilirlik içeri aktarmalar - çerçeveleri karşılaştırmak için API'sı ekleme [#2633](https://github.com/NuGet/Home/issues/2633)

* Bağımlılık seçeneklerini kullanırken Gizle `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)

* Ayrıntılı bir çıkış - nuget.exe sürüm üstbilgisinde çıkışı yazdırma [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet gereken yükseltme/yükleme dayalı dotnet tfm PCL sorunları - neden olabilecek olduğunu bilmesini sağlamak üzere [#3138](https://github.com/NuGet/Home/issues/3138)

* Hatalı yükleme/yükseltme tfm içeren projesi için uyar "dotnet" - = [#3137](https://github.com/NuGet/Home/issues/3137)

* Güncelleştirmesi - ReShaper ve NuGet ile performans sorunlarını çözün [#3044](https://github.com/NuGet/Home/issues/3044)

* Netcoreapp11 ve netstandard17 desteği - eklemek [#2998](https://github.com/NuGet/Home/issues/2998)

* Dengeleme AssemblyMetadata özniteliği için `.nuspec` belirteci değişikliklerini - [#2851](https://github.com/NuGet/Home/issues/2851)
