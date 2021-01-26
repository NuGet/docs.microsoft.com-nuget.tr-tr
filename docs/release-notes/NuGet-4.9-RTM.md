---
title: NuGet 4,9 RTM sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, yeni özellikler ve CCR 'ler dahil olmak üzere NuGet 4,9 sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: 429218fa4968d572ef187ef1dbfacac8a3bde2b4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780143"
---
# <a name="nuget-49-release-notes"></a>NuGet 4,9 sürüm notları

NuGet dağıtım araçlar:

| NuGet sürümü | Visual Studio sürümünde kullanılabilir| .NET SDK 'ları 'nda kullanılabilir|
|:---|:---|:---|
| [**4.9.0**](https://nuget.org/downloads) | [Visual Studio 2017 sürüm 15.9.0](https://visualstudio.microsoft.com/downloads/) | [2.1.500, 2.2.100](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [**4.9.1**](https://nuget.org/downloads) | yok | yok |
| [**4.9.2**](https://nuget.org/downloads) |[Visual Studio 2017 sürüm 15.9.4](https://visualstudio.microsoft.com/downloads/) | [2.1.502, 2.2.101](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [**4.9.3 &**](https://nuget.org/downloads) |[Visual Studio 2017 sürüm 15.9.6](https://visualstudio.microsoft.com/downloads/) | [2.1.504, 2.2.104](https://www.microsoft.com/net/download/visual-studio-sdks) |


## <a name="summary-whats-new-in-490"></a>Özet: 4.9.0 'deki yenilikler

* İmzalama: NuGet.Config- [#6961](https://github.com/NuGet/Home/issues/6961), [blog gönderisine](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html) göre listelenen bir güvenilen yazar ve depo kümesinin kullanımını gerektirmek Için clientpolicies 'yi etkinleştirin

* ". snupkg" dosyalarını paket içinde simgeler içerecek şekilde oluşturma--sembol sunucusu için snupkg dosyalarını kabul etmek üzere NuGet protokolünü anlama- [#6878](https://github.com/NuGet/Home/issues/6878), [blog gönderisi](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)

* NuGet kimlik bilgisi eklentisi v2- [#6642](https://github.com/NuGet/Home/issues/6642)

* Self-Contained NuGet paketleri-lisans- [#4628](https://github.com/NuGet/Home/issues/4628), [duyuru](https://github.com/NuGet/Announcements/issues/32)

* "Foo. Bar\1.0 \" dizinine- [#6949](https://github.com/NuGet/Home/issues/6949) paket başına MSBuild özelliği oluşturmak Için bir packagereference üzerinde opt" generatepathproperty "meta verilerini etkinleştirin

* NuGet işlemleri ile müşteri başarısını geliştirme- [#7108](https://github.com/NuGet/Home/issues/7108)

* Bir kilit dosyası kullanarak yinelenebilir paket geri yüklemelerini etkinleştirme- [#5602](https://github.com/NuGet/Home/issues/5602), [duyuru](https://github.com/NuGet/Announcements/issues/28), [blog gönderisi](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)

### <a name="issues-fixed-in-this-release"></a>Bu sürümde giderilen sorunlar

* Packageayıklama tarafından oluşturulan hatalara (WarnAsErrors aracılığıyla) yapılan uyarılar asla ayıklanan paketi [#7445](https://github.com/NuGet/Home/issues/7445) bırakmamalıdır

* Hatalı imzalı paketler genel paketler klasöründe sonlanmamalıdır- [#7423](https://github.com/NuGet/Home/issues/7423)

* bağlama yeniden yönlendirme oluşturması façlade derlemelerini atmamalıdır- [#7393](https://github.com/NuGet/Home/issues/7393)

* VersionRange eşittir, kayan aralıkları karşılaştırmıyor- [#7324](https://github.com/NuGet/Home/issues/7324)

* Geri yükleme: yeni .NET Core 2,1 HTTP Stack kullanarak performans gerileme- [#7314](https://github.com/NuGet/Home/issues/7314)

* Bir paketin güncelleştirilmesi, PackageReference- [#7285](https://github.com/NuGet/Home/issues/7285) privatevarlıklarını değiştirmemelidir

* İmzalama: bir pakette çok fazla paket girişi varsa imzalama başarısız olur (>65534)- [#7248](https://github.com/NuGet/Home/issues/7248)

* "DotNet NuGet Push" kod yolu yeni kimlik bilgisi sağlayıcısını desteklemelidir- [#7233](https://github.com/NuGet/Home/issues/7233)

* Sabit kültür ile eklentileri yürütmeyi destekleme (Docker 'da olduğu gibi)- [#7223](https://github.com/NuGet/Home/issues/7223)

* NuGet kaynakları ekleme NuGet.config kimlik bilgilerini silmemelidir [#7200](https://github.com/NuGet/Home/issues/7200)

* devDependency PackageReference yüklemesi, excludelabs için varsayılan değer olmalıdır = derle- [#7084](https://github.com/NuGet/Home/issues/7084)

* Tüm projeler için Migrator seçeneğini düzeltir ve proje uyumsuz ise hatayı göster- [#6958](https://github.com/NuGet/Home/issues/6958)

* "DotNet Add Package", yaptığı geri yükleme işlemini varlıklar dosyasına yürütmelidir- [#6928](https://github.com/NuGet/Home/issues/6928)

* İmzalama: imzalamayı, ilişkili hata iletilerini geliştirme- [#6906](https://github.com/NuGet/Home/issues/6906)

* [Test hatası] [zh-TW] "Paket Yöneticisi konsolu" dizesi, Paket Yöneticisi konsolunda yerelleştirmez- [#6381](https://github.com/NuGet/Home/issues/6381)

* "Proje bilgileri bulunamıyor" etrafındaki hata iletisi VS- [#5350](https://github.com/NuGet/Home/issues/5350) içinde biraz daha belirli olmalıdır

* NuGet paketinin nuspec sürüm etiketi kullanılırken hatalı bir hata iletisi- [#2714](https://github.com/NuGet/Home/issues/2714)

* DCR-Imzalama: NuGet protokolünü destekler: kayıt/4.9.0 kaynağı- [#7421](https://github.com/NuGet/Home/issues/7421)

* DCR-. nupkg. Metadata dosyası artık paket ayıklama sırasında oluşturulacak-"Content-hash"- [#7283](https://github.com/NuGet/Home/issues/7283) içerir

* DCR-mono [#7222](https://github.com/NuGet/Home/issues/7222) yürütülürken eklentiler için Authenticode doğrulamasını atlama

[Bu yayında düzeltilen tüm sorunların listesi 4.9.0](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a>Özet: 4.9.1 'deki yenilikler

* Yeni bir komut ile nuget.config yazma desteği ekleyin- [#7480](https://github.com/NuGet/Home/issues/7480)

### <a name="issues-fixed-in-this-release"></a>Bu sürümde giderilen sorunlar

* Lisans bağlantısı oluşturmayı onarma- [#7515](https://github.com/NuGet/Home/issues/7515)

* İmzaları doğrulamak için hata kodları gerileme- [#7492](https://github.com/NuGet/Home/issues/7492)

* NuGet. Build. Tasks. Pack paketinde lisans bilgisi yok- [#7379](https://github.com/NuGet/Home/issues/7379)

[Bu yayında düzeltilen tüm sorunların listesi 4.9.1](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a>Özet: 4.9.2 'deki yenilikler

### <a name="issues-fixed-in-this-release"></a>Bu sürümde giderilen sorunlar

* Kaynak adı bir boşluk içeriyorsa VS/dotnet.exe/nuget.exe/msbuild.exe geri yükleme kimlik bilgileri kullanmaz- [#7517](https://github.com/NuGet/Home/issues/7517)

* LicenseAcceptanceWindow ve LicenseFileWindow erişilebilirlik sorunları- [#7452](https://github.com/NuGet/Home/issues/7452)

* DateTime içinde FormatException dönüştürücüsünü düzeltir- [#7539](https://github.com/NuGet/Home/issues/7539)

[Bu yayında düzeltilen tüm sorunların listesi 4.9.2](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="summary-whats-new-in-493"></a>Özet: 4.9.3 & 'deki yenilikler

### <a name="issues-fixed-in-this-release"></a>Bu sürümde giderilen sorunlar
#### <a name="repeatable-package-restores-using-a-lock-file-issues"></a>"Yinelenebilir paket bir kilit dosyası kullanarak geri yükler" sorunlar

* Daha önce önbelleğe alınmış paketler için karma yanlış hesaplandığından kilitli mod çalışmıyor- [#7682](https://github.com/NuGet/Home/issues/7682)

* Restore, `packages.lock.json` dosya [#7667](https://github.com/NuGet/Home/issues/7667) tanımlı olandan farklı bir sürüme çözümleniyor

* '--kilitlendi-Mode/RestoreLockedMode ', ProjectReferences dahil edildiğinde smerak eden geri yükleme hatalarıyla neden olur [#7646](https://github.com/NuGet/Home/issues/7646)

* MSBuild SDK 'Sı çözümleyici, [#7599](https://github.com/NuGet/Home/issues/7599) packages.lock.jskullanırken geri yükleme başarısız olan bir SDK PAKETI için SHA doğrulaması yapmayı dener

#### <a name="lock-down-your-dependencies-using-configurable-trust-policies-issues"></a>"Yapılandırılabilir güven Ilkeleri kullanarak bağımlılıklarınızı kilitleme" sorunlar
* dotnet.exe imzalı paketler desteklenmediğinden, güvenilen imzalayanlar değerlendirilmemelidir- [#7574](https://github.com/NuGet/Home/issues/7574)

* Yapılandırma dosyasındaki trustedSigners 'ın sırası, güven değerlendirmesini etkiler- [#7572](https://github.com/NuGet/Home/issues/7572)

* Isettings uygulanamıyor [ayarları güven Ilkeleri desteklemek için yeniden düzenleme API 'Leri nedeniyle oluşur]- [#7614](https://github.com/NuGet/Home/issues/7614)

#### <a name="improved-debugging-experience-issues"></a>"Geliştirilmiş hata ayıklama deneyimi" sorunları

* .NET Core küresel aracı için sembol paketi yayımlanamıyor- [#7632](https://github.com/NuGet/Home/issues/7632)

#### <a name="self-contained-nuget-packages---license-issues"></a>"Kendi Içinde bulunan NuGet paketleri-Lisans" sorunları

* Katıştırılmış lisans dosyası kullanılırken symbol. snupkg paketi oluşturulurken hata- [#7591](https://github.com/NuGet/Home/issues/7591)

[Bu yayında düzeltilen tüm sorunların listesi 4.9.3 &](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.3")

## <a name="summary-whats-new-in-494"></a>Özet: 4.9.4 'deki yenilikler

* Güvenlik onarımı: ~/. NuGet içinde oluşturulan dosyalardaki Izinler çok açık [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)


## <a name="known-issues"></a>Bilinen sorunlar

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519"></a>DotNet NuGet Push--Interactive, Mac 'te bir hata veriyor. - [#7519](https://github.com/NuGet/Home/issues/7519)

#### <a name="issue"></a>Sorun
`--interactive`Bağımsız değişken DotNet CLI tarafından iletilmiyor ve hata ile sonuçlanıyor`error: Missing value for option 'interactive'`

#### <a name="workaround"></a>Geçici çözüm
Diğer bir DotNet komutunu, gibi etkileşimli seçenekle çalıştırın `dotnet restore --interactive` ve kimlik doğrulaması yapın. Kimlik doğrulaması daha sonra kimlik bilgisi sağlayıcısı tarafından önbelleğe alınmış olabilir. Ardından `dotnet nuget push` komutunu çalıştırın.

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a>.NET Core SDK tarafından yüklenen FallbackFolders paketleri özel olarak yüklenir ve imza doğrulaması başarısız olur. - [#7414](https://github.com/NuGet/Home/issues/7414)

#### <a name="issue"></a>Sorun
Birden çok hedef netcoreapp 1. x ve netcoreapp 2. x ' i hedefleyen bir projeyi geri yüklemek için dotnet.exe 2. x kullanırken, geri dönüş klasörü bir dosya akışı olarak kabul edilir. Bu, geri yükleme sırasında NuGet paketini geri dönüş klasöründen seçer ve genel paketler klasörüne yüklemeyi dener ve hata veren olağan imza doğrulamasını yapmak için kullanılır.

#### <a name="workaround"></a>Geçici çözüm
Geri dönüş klasörünün kullanımını, öğesini Nothing olarak ayarlayarak devre dışı bırakın `RestoreAdditionalProjectSources` . `<RestoreAdditionalProjectSources/>` Bu durum, geri dönüş klasöründen geri yüklenmiş olabilecek NuGet.org 'ten çok sayıda paket indirileceği için bunu dikkatle kullanın.
