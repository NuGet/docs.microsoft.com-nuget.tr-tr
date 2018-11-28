---
title: NuGet 4.9 RTM sürüm notları
description: NuGet bilinen sorunları, hata düzeltmeleri, yeni özellikler ve dcr dahil olmak üzere 4.9 için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: 3da1056f64b76f27afa662d879ef9f85868e2a07
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453823"
---
# <a name="nuget-49-release-notes"></a>NuGet 4.9 sürüm notları

[Visual Studio 2017 15.9.0 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) NuGet 4.9.0 işlevselliği ile birlikte gelir.


Aynı işlevlere komut satırı sürümleri de mevcuttur:
* NuGet.exe 4.9.x - [nuget.org/downloads](https://nuget.org/downloads)
* DotNet.exe - [.NET Core SDK'sı 2.1.500](https://www.microsoft.com/net/download/visual-studio-sdks)


## <a name="summary-whats-new-in-490"></a>Özet: 4.9.0 yenilikler

* İmzalama: Etkinleştirme güvenilen yazarlar ve depoları NuGet.Config içinde - listelenen bir dizi kullanımını zorunlu ClientPolicies [#6961](https://github.com/NuGet/Home/issues/6961)

* Paketi sembolleri içeren--snupkg dosyalar için Sembol sunucusu - kabul etmek için nuget Protokolü anlamak için anında iletme geliştirmek için ".snupkg" dosyaları oluşturma [#6878](https://github.com/NuGet/Home/issues/6878)

* NuGet kimlik bilgisi eklentisi V2 - [#6642](https://github.com/NuGet/Home/issues/6642)

* Müstakil NuGet paketleri - lisans - [#4628](https://github.com/NuGet/Home/issues/4628)

* Kabul etme "GeneratePathProperty" meta verilerini oluşturmak için PackageReference etkinleştirme bir paket MSBuild özelliği için başına "Foo.Bar\1.0\" dizin - [#6949](https://github.com/NuGet/Home/issues/6949)

* Müşteri başarı ile NuGet işlemleri - geliştirmek [#7108](https://github.com/NuGet/Home/issues/7108)

### <a name="issues-fixed-in-this-release"></a>Bu sürümde giderilen sorunlar

* Uyarıları PackageExtraction tarafından oluşturulan hatalara (aracılığıyla WarnAsErrors) yükseltilmiş etrafında - ayıklanan paket asla terk [#7445](https://github.com/NuGet/Home/issues/7445)

* Hatalı imzalanmış paketleri sone ermemlidir genel paketleri klasöründe - [#7423](https://github.com/NuGet/Home/issues/7423)

* bağlama yeniden yönlendirme oluşturma atlamayın cephe derlemeleri - [#7393](https://github.com/NuGet/Home/issues/7393)

* Kayan aralıkları - VersionRange eşittir karşılaştırma değil [#7324](https://github.com/NuGet/Home/issues/7324)

* Geri yükleme: yeni .NET Core 2.1 HTTP kullanarak performans gerilemesi yığınını - [#7314](https://github.com/NuGet/Home/issues/7314)

* Güncelleştirme paketi değişiklik PrivateAssets - PackageReference'nın [#7285](https://github.com/NuGet/Home/issues/7285)

* İmzalama: bir paket çok fazla paket giriş varsa imzalama başarısız olması (> 65534)- [#7248](https://github.com/NuGet/Home/issues/7248)

* "dotnet nuget anında iletme" kod yolu, yeni kimlik bilgisi sağlayıcısı - desteklemelidir [#7233](https://github.com/NuGet/Home/issues/7233)

* Yürütme eklentileri (gibi docker gerçekleşir) sabit kültür ile-destek [#7223](https://github.com/NuGet/Home/issues/7223)

* nuget kaynağı ekleme NuGet.config - kimlik bilgilerinin silemediğini [#7200](https://github.com/NuGet/Home/issues/7200)

* bir devDependency PackageReference yükleme excludeassets için varsayılan derleme - = [#7084](https://github.com/NuGet/Home/issues/7084)

* Proje uyumsuz - ise tüm projeler ve hatayı Göster görüntülenecek migrator seçeneği düzeltme [#6958](https://github.com/NuGet/Home/issues/6958)

* "dotnet Paketi Ekle" varlıklar dosyasına - gerçekleştirdiği geri işlemesi gerektiğini [#6928](https://github.com/NuGet/Home/issues/6928)

* İmzalama: imzalama ilgili hata iletileri - geliştirmek [#6906](https://github.com/NuGet/Home/issues/6906)

* [Test hatası] zh-TW Dize "Paket Yöneticisi Konsolu" Paket Yöneticisi konsolu - yerelleştirmek değil [#6381](https://github.com/NuGet/Home/issues/6381)

* "Proje bilgileri bulmak için yapılandırılamıyor" geçici hata iletisi ve iç karşılaştırması - biraz daha belirli [#5350](https://github.com/NuGet/Home/issues/5350)

* Nuget paketinin - nuspec sürüm etiketi yanlış kullanırken faydasız hata iletisi [#2714](https://github.com/NuGet/Home/issues/2714)

* DCR - imzalama: NuGet protokolünü destekleyen: RepositorySignatures/4.9.0 kaynak - [#7421](https://github.com/NuGet/Home/issues/7421)

* -DCR. nupkg.metadata dosya artık - içerir "içerik-hash" - Paket ayıklama sırasında oluşturulur [#7283](https://github.com/NuGet/Home/issues/7283)

* -Mono üzerinde yürütülürken authenticode Doğrulamayı atla eklentileri için - DCR [#7222](https://github.com/NuGet/Home/issues/7222)

[Bu sürümde 4.9.0 düzeltilen tüm sorunlara listesi](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a>Özet: 4.9.1 yenilikler

* Bir yazma okumak için destek eklemek için bir yeni komut güvenilen-İmzalayanları - aracılığıyla nuget.config [#7480](https://github.com/NuGet/Home/issues/7480)

### <a name="issues-fixed-in-this-release"></a>Bu sürümde giderilen sorunlar

* Lisans bağlantı oluşturma - düzeltme [#7515](https://github.com/NuGet/Home/issues/7515)

* Hata kodları imzaları doğrulamak için gerileme- [#7492](https://github.com/NuGet/Home/issues/7492)

* Lisans bilgileri - NuGet.Build.Tasks.Pack paket yok [#7379](https://github.com/NuGet/Home/issues/7379)

[Bu sürümde 4.9.1 düzeltilen tüm sorunlara listesi](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="known-issues"></a>Bilinen sorunlar

### <a name="dotnetexenugetexe-doesnt-use-credentials-when-source-name-contains-a-whitespace---7517httpsgithubcomnugethomeissues7517"></a>bir boşluk - kaynak adı içerdiğinde dotnet.exe/nuget.exe kimlik bilgilerini kullanmaz [#7517](https://github.com/NuGet/Home/issues/7517)

#### <a name="issue"></a>Sorun
Kaynak adı bir boşluk olduğunda nuget.exe gibi bir hata oluşturur. `The ' ' character, hexadecimal value 0x20, cannot be included in a name.`

#### <a name="workaround"></a>Geçici Çözüm
Bir boşluk içermemelidir kaynağının adını değiştirin.

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a>DotNet nuget push--etkileşimli Mac üzerinde bir hata verir. - [#7519](https://github.com/NuGet/Home/issues/7519)

#### <a name="issue"></a>Sorun
`--interactive` Bağımsız değişken dotnet CLI tarafından iletilmez değil ve hataya neden olur `error: Missing value for option 'interactive'`

#### <a name="workaround"></a>Geçici Çözüm
Etkileşimli seçeneğiyle gibi diğer dotnet komutu çalıştırmak `dotnet restore --interactive` ve kimlik doğrulaması. Ardından kimlik doğrulama kimlik bilgisi sağlayıcı tarafından önbelleğe alınabilir. Ardından çalıştırın `dotnet nuget push`.

### <a name="licenseacceptancewindow-and-licensefilewindow-accessibility-issues---7452httpsgithubcomnugethomeissues7452"></a>LicenseAcceptanceWindow ve LicenseFileWindow erişilebilirlik sorunları - [#7452](https://github.com/NuGet/Home/issues/7452)

#### <a name="issue"></a>Sorun
Lisans kabulü ve lisans dosyası penceresinde klavye ile gezinme erişilebilirlik sorunları ve ekran okuyucu ve JAWS anlatım vardır.

#### <a name="workaround"></a>Geçici Çözüm
Geçici çözüm yok.

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>.NET Core SDK'sı tarafından yüklenen FallbackFolders paketlerinde özel olarak yüklü olan ve imza doğrulaması başarısız. - [#7414](https://github.com/NuGet/Home/issues/7414)

#### <a name="issue"></a>Sorun
DotNet.exe kullanırken bir proje bu çok hedefleri netcoreapp geri yüklemek için 2.x 1.x ve netcoreapp 2.x, geri dönüş klasörüne bir dosya akışı olarak kabul edilir. Bunun anlamı geri yüklerken, NuGet geri dönüş klasöründen paketi seçin ve genel paketleri klasörüne yükleyin ve başarısız her zamanki imza doğrulama yapmak deneyin.

#### <a name="workaround"></a>Geçici Çözüm
Geri dönüş klasör kullanımı ayarlayarak devre dışı bırakmanız `RestoreAdditionalProjectSources` Nothing. `<RestoreAdditionalProjectSources/>` Bu dikkatli olmalıdır aksi halde, NuGet.org adresinden yüklenecek paketler birçok neden olacak şekilde geri yüklendi geri dönüş klasöründen kullanın.
