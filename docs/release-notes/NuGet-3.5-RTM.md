---
title: NuGet 3,5 RTM sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 3,5 sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 158373fb62f57fe6947fb863a1eef8122399959a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776351"
---
# <a name="nuget-35-release-notes"></a>NuGet 3,5 sürüm notları

[NuGet 3,5-RC sürüm notları](../release-notes/nuget-3.5-RC.md)  |  [NuGet 4,0 RC sürüm notları](../release-notes/nuget-4.0-RC.md)

## <a name="bug-fixes"></a>Hata Düzeltmeleri

* Paket, mono [#3550](https://github.com/NuGet/Home/issues/3550) üzerinde MSBuild 14,1 kullanmaz

* Güncelleştirme sekmesi, güncelleştirmek için kullanılabilir en son sürümü seçmeyin, bunun yerine geçerli yüklü sürümü seçin- [#3498](https://github.com/NuGet/Home/issues/3498)

* Özel v2 MyGet akışı doğrulandıktan sonra ve "x daha fazla sonuç göster [#3469](https://github.com/NuGet/Home/issues/3469) " seçeneğine tıklayarak kilitlenmeyi düzeltir

* Günlük iletileri UI- [#3446](https://github.com/NuGet/Home/issues/3446) için ters sırada görünüyor

* v 3.4.4-NuGet restore "verilen yolun biçimi desteklenmiyor"- [#3442](https://github.com/NuGet/Home/issues/3442)

* NuGet komut 3,6 Beta,-Prop Configuration = Release- [#3432](https://github.com/NuGet/Home/issues/3432)

* Büyük projede NuGet ıKVM yavaş yüklemesi- [#3428](https://github.com/NuGet/Home/issues/3428)

* nuget.exe güncelleştirme-kendi kendini güncelleştirme üzerinde devam eder [#3395](https://github.com/NuGet/Home/issues/3395)

* 3,5 UNC paylaşımından yükleme/geri yükleme için 3.4.4- [#3355](https://github.com/NuGet/Home/issues/3355) performans gerileme bulunur

* Bir net451 projesi için paket yönetimi kullanıcı arabiriminden moq yüklenirken hata- [#3349](https://github.com/NuGet/Home/issues/3349)

* Çözüm düzeyinde Install Tab, paketin sürüm- [#3339](https://github.com/NuGet/Home/issues/3339) göstermiyor

* `project.json`yüklü sekmeden xproj güncelleştirmesi durum [#3303](https://github.com/NuGet/Home/issues/3303) kaybeder

* Üzerinde NuGet paketi `.csproj` , `.nuspec` dosyadaki dosya [#3257](https://github.com/NuGet/Home/issues/3257) boş dosya öğesini yoksayar

* IIS 'de barındırılan Web sitesi projeleri geri yüklemenin başarısız olmasına neden olmamalıdır- [#3235](https://github.com/NuGet/Home/issues/3235)

* V3 uç noktası v2 'ye yeniden yönlendirirse Nuget.Config kimlik bilgileri alınmadı- [#3179](https://github.com/NuGet/Home/issues/3179)

* NuGet paketi, taşınabilir derleme meta verilerini alırken derlemeyi çözemedi- [#3128](https://github.com/NuGet/Home/issues/3128)

* NuGet `msbuild.exe` Mono [#3085](https://github.com/NuGet/Home/issues/3085) bulamıyor

* nuget.exe Pack, [#1743](https://github.com/NuGet/Home/issues/1743) sayılarla başlayan yayın öncesi etiketine izin vermiyor

* NuGet paketi yüklemesi VS2015E- [#1298](https://github.com/NuGet/Home/issues/1298) başarısız oluyor

* allowedVersions filtresi çözüm düzeyinde çalışmıyor- [#333](https://github.com/NuGet/Home/issues/333)

* Aynı anahtara sahip bir öğe zaten eklenmiş şekilde geri yükleme rastgele başarısız olur. - [#2646](https://github.com/NuGet/Home/issues/2646)

* NuGet. Common `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635) yüklenemiyor

* Bir v2 kaynağını aramak için Kullanıcı arabirimini kullanırken, Findpackagesbyıd her KIMLIK için iki kez çağırılır [#2517](https://github.com/NuGet/Home/issues/2517)

* Paketler projelere bağımlı olamaz- [#2490](https://github.com/NuGet/Home/issues/2490)

* nuget.exe Pack-exclude belgelenmiştir ancak desteklenmez- [#2284](https://github.com/NuGet/Home/issues/2284)

* ' ContentFiles ' bölümü geçersiz olduğunda hata iletileri ile ilgili sorunlar `.nuspec` geçersiz- [#1686](https://github.com/NuGet/Home/issues/1686)

* Gönderim her zaman kimliği doğrulanmış paket kaynaklarıyla tüm paketi iki kez gönderir [#1501](https://github.com/NuGet/Home/issues/1501)

* Projede bir #1496 olmadığında nuget.exe Update *. csproj çağrılırken hiçbir bilgi verilmedi `packages.config`  -  [](https://github.com/NuGet/Home/issues/1496)

* `packages.config` yükleme, v2 kaynaklarından 5 xx durum kodu üzerinde yeniden denenmez- [#1217](https://github.com/NuGet/Home/issues/1217)

* Kaynak dosyasında çift nokta `.nuspec` çalışmıyor- [#2947](https://github.com/NuGet/Home/issues/2947)

* CoreCLR geri yüklemenin, şifreleme ile akışları yoksayması gerekiyor [#2942](https://github.com/NuGet/Home/issues/2942)

* nuget.exe Push 403 işleme-kimlik bilgileri için yanlış istem- [#2910](https://github.com/NuGet/Home/issues/2910)

* Paket Yöneticisi üzerinden NuGet güncelleştirmesi `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888) özellikleri kaldırır

* NuGet. PackageManagement. VisualStudio "NuGet. TeamFoundationServer14" öğesini yüklemeyi deneyin, ancak bu DLL adı "NuGet. TeamFoundationServer" olarak değiştirildi- [#2857](https://github.com/NuGet/Home/issues/2857)

* Paket Yöneticisi Kullanıcı arabirimi yeni güncelleştirilmiş sürümü göstermiyor [#2828](https://github.com/NuGet/Home/issues/2828)

* güncelleştirme-Package. Version- [#2771](https://github.com/NuGet/Home/issues/2771) yerine PackageID, Version kullanmaya çalışan paket.

* Proje NuGet (veya) kullanıyorsa NuGet geri yükleme csproj hatası olmalıdır `packages.config` `project.json` - [#2766](https://github.com/NuGet/Home/issues/2766)

* "[File] TFS hatası, çalışma alanınızda bulunamadı veya çözüm/proje TFS kaynak denetimine bağlandığında yükseltme veya kaldırma işlemi sırasında" erişim izniniz yok- [#2739](https://github.com/NuGet/Home/issues/2739)

* güncelleştirme paketi, hedef olmayan paketler için bağımlılıklar almaz- [#2724](https://github.com/NuGet/Home/issues/2724)

* NuGet Paket Yöneticisi Kullanıcı Arabirimi eylemleri için günlük ayrıntı düzeyi ayarlama yolu yoktur- [#2705](https://github.com/NuGet/Home/issues/2705)

* NuGet yapılandırması geçersiz-VS 2015 VSıX (v 3.4.3)- [#2667](https://github.com/NuGet/Home/issues/2667)

* () İçindeki DefaultPushSource `NuGetDefaults.Config` `ProgramData\NuGet` çalışmıyor- [#2653](https://github.com/NuGet/Home/issues/2653)

* NuGet 3.4.3 Release-değer alma paket derlemesinde null olamaz- [#2648](https://github.com/NuGet/Home/issues/2648)

* restore, VSTS akışları için Nuget.Config depolanan kimlik bilgilerini kullanmıyor [#2647](https://github.com/NuGet/Home/issues/2647)

* [dotnet restore]--ConfigFile, cmd dir- [#2639](https://github.com/NuGet/Home/issues/2639) yerine proje dizini 'ne göredir

* Sürüm karşılaştırmalarda aşırı kullanım kodu- [#2632](https://github.com/NuGet/Home/issues/2632)

* Aynı paketi paralel olarak yüklemeye çalışan nuget.exe birden çok örneği, Çift yazma [#2628](https://github.com/NuGet/Home/issues/2628) neden olur

* Bağımlılık bilgileri çoklu proje işlemleri için önbelleğe alınmaz- [#2619](https://github.com/NuGet/Home/issues/2619)

* Önce paketler klasörünü denetlemeden yükleme paketlerini yükle ve Güncelleştir- [#2618](https://github.com/NuGet/Home/issues/2618)

* Paket kaynak listesi boşsa, Kullanıcı arabirimi (NuGet 3.4. x) aracılığıyla paket kaynağı eklenemiyor [#2617](https://github.com/NuGet/Home/issues/2617)

* Tasarım zamanı cephe 'e bağlı paketi yüklemeye çalışırken yanıltıcı hata oluştu- [#2594](https://github.com/NuGet/Home/issues/2594)

* PackageManager konsolundan paket yükleme "All" ayarı yalnızca ilk kaynak- [#2557](https://github.com/NuGet/Home/issues/2557) çalışır

* En son beta ModernHttpClient- [#2518](https://github.com/NuGet/Home/issues/2518)

* VS2015 otomatik olarak oluşturulan NuGet 3.4.1- [#2419](https://github.com/NuGet/Home/issues/2419)

* Bunu sorsam, Update komutu biraz daha ayrıntılı olabilir...- [#2418](https://github.com/NuGet/Home/issues/2418)

* Yerel olarak oluşturulan VSıX, CI derlemesi ile aynı dll 'Lere ve dosyalara sahip olmalıdır. - [#2401](https://github.com/NuGet/Home/issues/2401)

* Derleme [#2396](https://github.com/NuGet/Home/issues/2396) NuGet düşürme uyarılarını çözme

* Paket kaynağının kimlik doğrulaması başarısız (3 kez), süresiz olarak engellendi [#2362](https://github.com/NuGet/Home/issues/2362)

* Paket dosyaları içerdiğinde-NoCache bağımsız değişkenine sahip bir NuGet v 3.3 + akışından bir paket yüklenirken paket içeriği doğru şekilde geri yüklenmedi `.nupkg` - [#2354](https://github.com/NuGet/Home/issues/2354)

* Tüm paket kaynaklarıyla NuGet yüklemesi, ancak 1 kaynakta paket eksik, başarısız- [#2322](https://github.com/NuGet/Home/issues/2322)

* [PerfWatson] Uıdelay: nuget.packagemanagement.visualstudio.dll! NuGet. PackageManagement. VisualStudio. VSMSBuildNuGetProjectSystem + * lt; &gt; c__DisplayClass_0 + &lt; &lt; addreference &gt; B__ &gt; d. MoveNext- [#2285](https://github.com/NuGet/Home/issues/2285)

* Tek bir kaynak yetkilendirme başarısız olursa blokları yükler- [#2034](https://github.com/NuGet/Home/issues/2034)

* `.nuspec` sürüm aralığı geçersiz kılınmalıdır-ınclukıd proje sürümü- [#1983](https://github.com/NuGet/Home/issues/1983)

* Update-Package Super yavaş-"bağımlılık bilgilerini toplamaya çalışılıyor"- [#1909](https://github.com/NuGet/Home/issues/1909)

* Toplu işlem, bağımlılıklarını güncelleştirirken NuGet gizli eski sürüme sahip des paketi- [#1903](https://github.com/NuGet/Home/issues/1903)

* nuget.exe güncelleştirme, bütünleştirilmiş kod tanımlayıcı adı ve Private özniteliği bırakır. - [#1778](https://github.com/NuGet/Home/issues/1778)

* "DefaultPushSource" için göreli dosya yolu- [#1746](https://github.com/NuGet/Home/issues/1746)

* Çözümleyici hata iletilerini geliştirme- [#1373](https://github.com/NuGet/Home/issues/1373)

* v3 'teki güncelleştirme paketi, belirtilen kaynak [#1013](https://github.com/NuGet/Home/issues/1013) olmayan paketlerle başarısız oluyor

* Paket kaynakları için göreli yolların kullanılması sorunlu [#865](https://github.com/NuGet/Home/issues/865)

* Daha düşük bir sürüm gereksinimiyle zaten bir dolaylı bağımlılık varsa, projeden oluşturulan NUPKG-File içinde eksik bağımlılık var- [#759](https://github.com/NuGet/Home/issues/759)

* Bir projenin silinmesi, ilgili Kullanıcı arabirimi penceresini kapatır, ancak projenin yeniden adlandırılması Kullanıcı arabirimi penceresini yeniden adlandırmaz. PMC 'nin proje yeniden adlandırma ve proje kaldırma olaylarını dinler- [#670](https://github.com/NuGet/Home/issues/670)

* [Soldüşük Web Iş yükü] Razor V3 WSP kilitleniyor- [#3241](https://github.com/NuGet/Home/issues/3241)

* Belirli bir paketi yükleme/geri yükleme işlemi "Package birden çok nuspec dosyası içeriyor" ile başarısız olur. - [#3231](https://github.com/NuGet/Home/issues/3231)

* Küçük kodlar & `packages.config` senaryolar- [#3209](https://github.com/NuGet/Home/issues/3209)

* [3,5-beta2] Paket geri yükleme "eski" paketleri geri yüklemeyi yapamıyor- [#3208](https://github.com/NuGet/Home/issues/3208)

* NuGet Pack,. tt dosyalarını, ne tür şeyler [#3203](https://github.com/NuGet/Home/issues/3203) , içerik klasörüne zorla ekler

* Update-ASP.NET Web App paketi, dosyayla ilgili bir uyarı oluşturur: kaynak- [#3194](https://github.com/NuGet/Home/issues/3194)

* `project.json`json dosyasında packOptions ve sahip olmadığında NuGet Pack csproj (WITH) kilitleniyor- [#3180](https://github.com/NuGet/Home/issues/3180)

* için NuGet paketi `project.json` , Summary, yazarlar, Owners vs- [#3161](https://github.com/NuGet/Home/issues/3161) gibi packoptions etiketlerini yoksayar

* NuGet. paketleme. PhysicalPackageFile. GetStream- [#3160](https://github.com/NuGet/Home/issues/3160) aracılığıyla NullReferenceException

* NuGet paketi `.nuspec` `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145) için çıkışta bağımlılıkları yoksayar

* Birden çok paketin geri alma ile güncelleştirilmesi, projeyi bozuk bir durumda bırakır- [#3139](https://github.com/NuGet/Home/issues/3139)

* Netstandart projeler için any altındaki ContentFiles eklenmez- [#3118](https://github.com/NuGet/Home/issues/3118)

* .NET Standard için kitaplık hedeflemesi doğru paketlenemez- [#3108](https://github.com/NuGet/Home/issues/3108)

* Dosya-> yeni proje-> sınıf kitaplığı (taşınabilir) projesi VS2015 ve Dev15- [#3094](https://github.com/NuGet/Home/issues/3094) içinde başarısız oluyor

* nuGet hatası-1.0.0-* geçerli bir sürüm dizesi değil- [#3070](https://github.com/NuGet/Home/issues/3070)

* Find-Package görüntülenemiyor ancak Install-Package çalışmaları [#3068](https://github.com/NuGet/Home/issues/3068)

* Dev15- [#3061](https://github.com/NuGet/Home/issues/3061) "Install-Package jQuery. Validation" hatası

* xproj NuGet paketi geçersiz hedef yoluna sahip- [#3060](https://github.com/NuGet/Home/issues/3060)

* Bir VS 2015 güncelleştirme 3 ' ü, NuGet sürümü 3.5.0 hatası oluşursa [#3053](https://github.com/NuGet/Home/issues/3053)

* İçindeki "packages.config tarafından engellendi" `project.json` (UWP, a. k. derleme tümleşik) projesi- [#3046](https://github.com/NuGet/Home/issues/3046)

* derleme betiği tarafından yüklenen DotNet CLI, resmi preview2 derlemesi olan preview2-003121 öğesine güncelleştirin. - [#3045](https://github.com/NuGet/Home/issues/3045)

* Paket Yöneticisi Kullanıcı arabirimi: bir paket güncelleştirildikten sonra yeni sürüm gösterme- [#3041](https://github.com/NuGet/Home/issues/3041)

* -Delete komut satırındaki ApiKey, 3.5.0-Beta- [#3037](https://github.com/NuGet/Home/issues/3037) içinde okunamaz/gönderilmez

* Hatalı dize: paketin kararlı bir sürümü bir ön sürüm bağımlılığı üzerinde olmamalıdır. - [#3030](https://github.com/NuGet/Home/issues/3030)

* OptimizedZipPackage önbelleği boş klasörleri bırakır- [#3029](https://github.com/NuGet/Home/issues/3029)

* PCL (net46 ve Windows 10) projesi oluşturma NullRef özel durumu. - [#3014](https://github.com/NuGet/Home/issues/3014)

* Daha yüksek bir sürüm allowedVersions kısıtlaması tarafından kısıtlanmışsa NuGet güncelleştirmesi bilgilendirici ileti sağlamalıdır- [#3013](https://github.com/NuGet/Home/issues/3013)

* NuGet v3 geri yükleme sorunları- [#2891](https://github.com/NuGet/Home/issues/2891)

* Kimlik bilgisi eklentisi hata ile çıkıldı-1/birden çok kaynağa sahip kimlik bilgisi sağlayıcıları kullanılırken paket indirme hatası- [#2885](https://github.com/NuGet/Home/issues/2885)

* `project.json` NuGet geri yükleme hiçbir şey değiştirilmezse yeniden derlemeye neden olur- [#2817](https://github.com/NuGet/Home/issues/2817)

* Semboller paketleri, Install veya Update- [#2807](https://github.com/NuGet/Home/issues/2807) içinde hiç kullanılmamalıdır

* VS yolunda ortam değişkenlerini desteklemez (nuget.exe)- [#2763](https://github.com/NuGet/Home/issues/2763)

* Erişilebilirlik için Package Manager Kullanıcı arabirimindeki etiketli UIElements 'i etiketleme- [#2745](https://github.com/NuGet/Home/issues/2745)

* Hecelenmiş profiller içeren taşınabilir çerçeveler reddedilir. - [#2734](https://github.com/NuGet/Home/issues/2734)

* NuGet Paket Yöneticisi, paket ayrıntılarındaki seçenekler listesinin #2665 için uygulanmadığından emin olması gerekir `project.json`  -  [](https://github.com/NuGet/Home/issues/2665)

* nuget.exe gönderme/silme API anahtarını kullanmaz- [#2627](https://github.com/NuGet/Home/issues/2627)

* Kilitli özelliği kilit dosyasından kaldır- [#2379](https://github.com/NuGet/Home/issues/2379)

* NuGet 3.3.0 Güncelleştirmesi ' ek bir kısıtlama ile başarısız oluyor... packages.config tanımlı bu işlemi engelliyor. ' - [#1816](https://github.com/NuGet/Home/issues/1816)

* Mevcut olmayan bir yerel kaynaktan paket yükleme, sahte bir ileti oluşturur [#1674](https://github.com/NuGet/Home/issues/1674)

* "Yükseltme kullanılabilir" filtresi, sürüm kısıtlamasını ihlal eden yükseltmeleri gösterir- [#1094](https://github.com/NuGet/Home/issues/1094)

* Yerel paketler güncelleştirilemiyor- [#1291](https://github.com/NuGet/Home/issues/1291)


## <a name="features"></a>Özellikler

* NuGet- [#329](https://github.com/NuGet/Home/issues/329) tarafından eklenen başvurularda CopyLocal ayarını false olarak ayarlama desteği

* MSBuild 15 için nuget.exe desteği [#1937](https://github.com/NuGet/Home/issues/1937)

* İçin paket desteği.`csproj` + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)

* Yürütülen kullanıcı eylemleri olduğunda kullanıcı eylemini devre dışı bırak- [#1440](https://github.com/NuGet/Home/issues/1440)

* NuGet #2782 için destek eklemesi gerekir `runtimes/{rid}/nativeassets/{txm}/`  -  [](https://github.com/NuGet/Home/issues/2782)

* NuGet 2. x (zaten 3. x içinde olan) ile uyumlu çerçeve uyumluluk ekleme- [#2720](https://github.com/NuGet/Home/issues/2720)

* Geri dönüş paketi klasörleri için destek- [#2899](https://github.com/NuGet/Home/issues/2899)

* Araç paketlerini desteklemek için bir paket türü kavramı tasarlama ve uygulama- [#2476](https://github.com/NuGet/Home/issues/2476)

* Genel paketler klasörünün yolunu almak için bir API ekleyin- [#2403](https://github.com/NuGet/Home/issues/2403)

* [#3356](https://github.com/NuGet/Home/issues/3356) semver 2.0.0 'ı etkinleştirin

## <a name="dcrs"></a>DCR

* nuget.exe Push-timeout parametresi çalışmıyor- [#2785](https://github.com/NuGet/Home/issues/2785)

* Paket açıklama metni seçilebilir olmalıdır [#1769](https://github.com/NuGet/Home/issues/1769)

* nuget.exe `.props` ve `.targets` projeleri için dosyalar oluşturmak üzere `.nuproj` etkinleştirin [#2711](https://github.com/NuGet/Home/issues/2711)

* Çerçeveleri içeri aktarmaları ile karşılaştırmak için genişletilebilirlik API 'SI ekleme- [#2633](https://github.com/NuGet/Home/issues/2633)

* #2486 kullanırken bağımlılık seçeneklerini gizle `project.json`  -  [](https://github.com/NuGet/Home/issues/2486)

* Ayrıntılı çıkışta nuget.exe sürüm üst bilgisini Yazdır- [#1887](https://github.com/NuGet/Home/issues/1887)

* NuGet 'in kullanıcılara bir DotNet TFM tabanlı PCL 'de yükseltmenin/yüklemenin sorun oluşmasına neden olduğunu bilmesini sağlaması gerekir [#3138](https://github.com/NuGet/Home/issues/3138)

* "DotNet" projesi için hatalı yüklemeyi/yükseltmeyi uyar = "DotNet"- [#3137](https://github.com/NuGet/Home/issues/3137)

* Güncelleştirme için yeniden şekilsiz ve NuGet ile performans sorunlarını giderin- [#3044](https://github.com/NuGet/Home/issues/3044)

* Netcoreapp11 ve netstandard17 desteği ekleme- [#2998](https://github.com/NuGet/Home/issues/2998)

* Belirteç değişiklikleri için AssemblyMetadata özniteliğiyle yararlanın `.nuspec` - [#2851](https://github.com/NuGet/Home/issues/2851)
