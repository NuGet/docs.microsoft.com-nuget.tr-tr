---
title: NuGet 4.9 RTM Yayın Notları
description: Bilinen sorunlar, hata düzeltmeleri, yeni özellikler ve DCR'ler dahil olmak üzere NuGet 4.9 için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: e0dea74fe179c0dce4996f3e498185bb3a491856
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496459"
---
# <a name="nuget-49-release-notes"></a>NuGet 4.9 Yayın Notları

NuGet dağıtım araçları:

| NuGet sürümü | Visual Studio sürümünde mevcuttur| .NET SDK(ler) adresinde mevcuttur|
|:---|:---|:---|
| [**4.9.0**](https://nuget.org/downloads) | [Visual Studio 2017 sürümü 15.9.0](https://visualstudio.microsoft.com/downloads/) | [2.1.500, 2.2.100](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [**4.9.1**](https://nuget.org/downloads) | yok | yok |
| [**4.9.2**](https://nuget.org/downloads) |[Visual Studio 2017 sürümü 15.9.4](https://visualstudio.microsoft.com/downloads/) | [2.1.502, 2.2.101](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [**4.9.3**](https://nuget.org/downloads) |[Visual Studio 2017 sürümü 15.9.6](https://visualstudio.microsoft.com/downloads/) | [2.1.504, 2.2.104](https://www.microsoft.com/net/download/visual-studio-sdks) |


## <a name="summary-whats-new-in-490"></a>Özeti: 4.9.0 Yenilikler

* İmzalama: Müşteri İlkelerinin NuGet.Config'de listelenen Güvenilir Yazarlar ve Depolar kümesinin kullanılmasını gerektirmesini etkinleştirin - [#6961](https://github.com/NuGet/Home/issues/6961), [blog gönderisi](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)

* pakette semboller içeren ".snupkg" dosyaları oluşturun - sembol sunucusu için snupkg dosyaları kabul etmek nuget protokolünü anlamak için itme geliştirmek - [#6878](https://github.com/NuGet/Home/issues/6878), [blog yazısı](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)

* NuGet kimlik bilgileri eklentisi V2 - [#6642](https://github.com/NuGet/Home/issues/6642)

* Müstakil NuGet Paketleri - Lisans - [#4628](https://github.com/NuGet/Home/issues/4628), [duyuru](https://github.com/NuGet/Announcements/issues/32)

* "Foo.Bar\1.0\" dizini " için paket başına MSBuild özelliği oluşturmak için bir PackageReference üzerinde "GeneratePathProperty" meta verileri etkinleştirin - [#6949](https://github.com/NuGet/Home/issues/6949)

* NuGet işlemleri ile müşteri başarısını artırın - [#7108](https://github.com/NuGet/Home/issues/7108)

* Bir kilit dosyası kullanarak tekrarlanabilir paket geri yüklemeleri etkinleştirin - [#5602](https://github.com/NuGet/Home/issues/5602), [duyuru](https://github.com/NuGet/Announcements/issues/28), [blog yazısı](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)

### <a name="issues-fixed-in-this-release"></a>Bu sürümde giderilen sorunlar

* PackageExtraction tarafından yükseltilen hatalara yükseltilen uyarılar (WarnAsErrors aracılığıyla) ayıklanan paketi asla çevrede bırakmamalıdır - [#7445](https://github.com/NuGet/Home/issues/7445)

* Kötü imzalanmış paketler küresel paketler klasöründe sona ermemelidir - [#7423](https://github.com/NuGet/Home/issues/7423)

* bağlama yönlendirme üretimi cephe montajları atlamamalıdır - [#7393](https://github.com/NuGet/Home/issues/7393)

* VersionRange Equals kayan aralıkları karşılaştırmaz - [#7324](https://github.com/NuGet/Home/issues/7324)

* Geri yükleme: yeni .NET Core 2.1 HTTP yığını nı kullanarak performans regresyonu - [#7314](https://github.com/NuGet/Home/issues/7314)

* Paketin Güncellemesi, Bir Paket Referansının PrivateAssets'ini değiştirmemelidir - [#7285](https://github.com/NuGet/Home/issues/7285)

* İmzalama: bir paketçok fazla paket girişi varsa imzalama başarısız olmalıdır (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)

* "dotnet nuget push" codepath yeni kimlik sağlayıcısı desteklemelidir - [#7233](https://github.com/NuGet/Home/issues/7233)

* Değişmez kültüre sahip eklentileri yürütmeyi destekleme (docker'da olduğu gibi) - [#7223](https://github.com/NuGet/Home/issues/7223)

* nuget kaynakları nuget.config gelen kimlik bilgilerini silmek gerekir eklemek - [#7200](https://github.com/NuGet/Home/issues/7200)

* devDependency PackageReference yükleme varsayılan excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)

* tüm projeler için görüntülenecek göçmen seçeneğini düzeltin ve proje uyumsuzsa hata gösterin - [#6958](https://github.com/NuGet/Home/issues/6958)

* "dotnet paketi ekle" varlıklar dosyasına gerçekleştirdiği geri yükleme işlemek gerekir - [#6928](https://github.com/NuGet/Home/issues/6928)

* İmzalama: ilgili hata iletilerini imzalamayı geliştirme - [#6906](https://github.com/NuGet/Home/issues/6906)

* [Test Hatası] [zh-TW] String "Package Manager Console" Package Manager Console'da yerelleştirilmese - [#6381](https://github.com/NuGet/Home/issues/6381)

* "Proje bilgilerini bulamıyor" etrafında hata iletisi VS içinde biraz daha spesifik olmalıdır - [#5350](https://github.com/NuGet/Home/issues/5350)

* Nuget paketinin nuspec sürüm etiketini yanlış kullanırken yardımcı olmayan hata [iletisi](https://github.com/NuGet/Home/issues/2714) - #2714

* DCR - İmzalama: destek NuGet protokolü: Depoİmzalar/4.9.0 kaynak - [#7421](https://github.com/NuGet/Home/issues/7421)

* DCR - .nupkg.metadata dosyası artık paket çıkarma sırasında oluşturulacak - "içerik-karma" içerir - [#7283](https://github.com/NuGet/Home/issues/7283)

* DCR - Mono'da çalışırken eklentiler için authenticode doğrulamasını atlayın - [#7222](https://github.com/NuGet/Home/issues/7222)

[Bu sürümde düzeltilen tüm sorunların listesi 4.9.0](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a>Özeti: Yenilikler 4.9.1

* Nuget.config yeni bir komut güvenilir-imzalayanlar aracılığıyla bir yazı okuma için destek ekleyin - [#7480](https://github.com/NuGet/Home/issues/7480)

### <a name="issues-fixed-in-this-release"></a>Bu sürümde giderilen sorunlar

* Lisans bağlantısı oluşturma düzeltme - [#7515](https://github.com/NuGet/Home/issues/7515)

* İmzaları doğrulamak için hata kodları regresyon - [#7492](https://github.com/NuGet/Home/issues/7492)

* NuGet.Build.Tasks.Pack paketinin lisans bilgileri yok - [#7379](https://github.com/NuGet/Home/issues/7379)

[Bu sürümde düzeltilen tüm sorunların listesi 4.9.1](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a>Özeti: Yenilikler 4.9.2

### <a name="issues-fixed-in-this-release"></a>Bu sürümde giderilen sorunlar

* VS/dotnet.exe/nuget.exe/msbuild.exe geri yükleme kaynak adı bir boşluk içeriyorsa kimlik bilgileri kullanmaz - [#7517](https://github.com/NuGet/Home/issues/7517)

* LisansKabulPencere ve LisansFileWindow Erişilebilirlik sorunları - [#7452](https://github.com/NuGet/Home/issues/7452)

* DateTimeConverter'dan DateTime.Parse'de Biçimözel durumu düzelt - [#7539](https://github.com/NuGet/Home/issues/7539)

[Bu sürümde düzeltilen tüm sorunların listesi 4.9.2](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="summary-whats-new-in-493"></a>Özeti: Yenilikler 4.9.3

### <a name="issues-fixed-in-this-release"></a>Bu sürümde giderilen sorunlar
#### <a name="repeatable-package-restores-using-a-lock-file-issues"></a>"Yinelenen Paket Kilit Dosyalarını Kullanarak Geri Yüklenir" Sorunları

* Karma olarak çalışmayan kilitli mod, önceden önbelleğe alınmış paketler için yanlış hesaplanır - [#7682](https://github.com/NuGet/Home/issues/7682)

* Geri yükleme, dosyada `packages.lock.json` tanımlanandan farklı bir sürüme gider - [#7667](https://github.com/NuGet/Home/issues/7667)

* '--kilitli mod / RestoreLockedMode' ProjectReferences söz konusu olduğunda sahte Geri Yükleme hatalarıneden olur - [#7646](https://github.com/NuGet/Home/issues/7646)

* MSBuild SDK çözümleyicisi packages.lock.json kullanırken geri başarısız bir SDK paketi için SHA doğrulamak için çalışır - [#7599](https://github.com/NuGet/Home/issues/7599)

#### <a name="lock-down-your-dependencies-using-configurable-trust-policies-issues"></a>"Yapılandırılabilir Güven İlkelerini Kullanarak Bağımlılıklarınızı Kilitleyin" Sorunları
* dotnet.exe imzalı paketler desteklenmezken güvenilir imzalayanları değerlendirmemelidir - [#7574](https://github.com/NuGet/Home/issues/7574)

* Config dosyasındaki güvenilir Signers sırası güven değerlendirmesini etkiler - [#7572](https://github.com/NuGet/Home/issues/7572)

* ISettings uygulayamıyorum [Güven İlkeleri özelliğini desteklemek için ayarlar API'lerinin yeniden dizilme neden olur] - [#7614](https://github.com/NuGet/Home/issues/7614)

#### <a name="improved-debugging-experience-issues"></a>"Geliştirilmiş Hata Ayıklama Deneyimi" Sorunları

* .NET Core Global Tool için sembol paketi yayınlayamıyor - [#7632](https://github.com/NuGet/Home/issues/7632)

#### <a name="self-contained-nuget-packages---license-issues"></a>"Müstakil NuGet Paketleri - Lisans" Sorunları

* Gömülü lisans dosyası kullanılırken hata oluşturma sembolü .snupkg paketi - [#7591](https://github.com/NuGet/Home/issues/7591)

[Bu sürümde düzeltilen tüm sorunların listesi 4.9.3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.3")

## <a name="summary-whats-new-in-494"></a>Özeti: Yenilikler 4.9.4

* Güvenlik Düzeltmesi: ~/.nuget içinde oluşturulan dosyalardaki izinler [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757) [#7673](https://github.com/NuGet/Home/issues/7673) çok açıktır


## <a name="known-issues"></a>Bilinen sorunlar

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519"></a>dotnet nuget push --interactive Mac'te bir hata verir. - [#7519](https://github.com/NuGet/Home/issues/7519)

#### <a name="issue"></a>Sorun
Bağımsız `--interactive` değişken dotnet cli tarafından iletilmiyor ve hatayla sonuçlanıyor`error: Missing value for option 'interactive'`

#### <a name="workaround"></a>Geçici çözüm
Gibi etkileşimli seçeneği ile başka bir `dotnet restore --interactive` dotnet komutu çalıştırın ve kimlik doğrulaması. Kimlik doğrulaması daha sonra kimlik bilgisi sağlayıcısı tarafından önbelleğe alınabilir. Ardından `dotnet nuget push` komutunu çalıştırın.

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a>.NET Core SDK tarafından yüklenen FallbackFolders paketleri özel yüklü ve başarısız imza doğrulama. - [#7414](https://github.com/NuGet/Home/issues/7414)

#### <a name="issue"></a>Sorun
netcoreapp 1.x ve netcoreapp 2.x'i hedefleyen bir projeyi geri yüklemek için dotnet.exe 2.x kullanırken, geri dönüş klasörü bir dosya akışı olarak kabul edilir. Bu, geri yükleme sırasında, NuGet geri dönüş klasöründen paketi almak ve küresel paketler klasörüne yüklemek ve başarısız olağan imza doğrulama yapmak çalışacağız anlamına gelir.

#### <a name="workaround"></a>Geçici çözüm
Geri dönüş klasörünün kullanımını hiçbir şeye `RestoreAdditionalProjectSources` ayarlayarak devre dışı k. `<RestoreAdditionalProjectSources/>`Aksi takdirde geri dönüş klasöründen geri olurdu NuGet.org gelen bir çok paket indirilebilir bir sürü neden olacak gibi dikkatli bir şekilde kullanın.
