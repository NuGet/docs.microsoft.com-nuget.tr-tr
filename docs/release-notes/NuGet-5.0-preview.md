---
title: NuGet 5.0-preview sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, yeni özellikler ve dcr dahil olmak üzere NuGet 5.0 Önizleme için sürüm notları.
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: ed3294f88ff99d5e26f630bdbca03aa8446b6e7f
ms.sourcegitcommit: 0cb4c9853cde3647291062eadee2298dd273311e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2019
ms.locfileid: "55084954"
---
# <a name="nuget-50-preview-release-notes"></a>NuGet 5.0 Preview sürüm notları

## <a name="summary-whats-new-in-50-preview-2"></a>Özet: 5.0 Önizleme 2'de yenilikler nelerdir?

### <a name="issues-fixed-in-this-release"></a>Bu sürümde giderilen sorunlar

#### <a name="bugs"></a>Hataları:

* VS 16,0'ın NuGet kullanıcı Arabirimi olan renk sorunları - nedeniyle okunamaz sekmeleri [#7735](https://github.com/NuGet/Home/issues/7735)

* NuGet.Core & NuGet.Clients License.txt açıklama - [#7629](https://github.com/NuGet/Home/issues/7629)

* Geri yükleme türü - belirlemek için gereksiz yere genel bir paket klasörüne numaralandırır [#7596](https://github.com/NuGet/Home/issues/7596)

* Kilit dosya zorlama hatalarından görünmesini Hata Listesi penceresinde - [#7429](https://github.com/NuGet/Home/issues/7429)

* NuGet.Configuration sorunlarını gidermek [#7326](https://github.com/NuGet/Home/issues/7326)

* MSBuild güncelleştirmeye uyarlar bunu kullanıcının yükleme konumu.  - [#7325](https://github.com/NuGet/Home/issues/7325)

* Bir geliştirme bağımlılığı - NuGet.Build.Tasks.Pack olmalıdır [#7249](https://github.com/NuGet/Home/issues/7249)

* Dahil etmek için paketi uzantı noktası ekleme hata ayıklama sembolleri - [#7234](https://github.com/NuGet/Home/issues/7234)

* DotNet paketi bağımlılık sürüm aralığında oluşturulan nupkg korumak. (kayan sürümü kullanılıyorsa bile) - [#7232](https://github.com/NuGet/Home/issues/7232)

* DotNet restore başarısız kaynak kimliği doğrulanmış kullanıcı düzeyinde yapılandırma kaynağı - olduğunda [#7209](https://github.com/NuGet/Home/issues/7209)

* Paketi için içerik dosyaları - BuildActions kümesini değil kısıtlama [#7155](https://github.com/NuGet/Home/issues/7155)

* Başarılı olması AssetTargetFallback gerektiren bir projectreference kullanarak bildirmelisiniz. - [#7137](https://github.com/NuGet/Home/issues/7137)

* CPS (CommonProjectSystem) - çağırırken iş parçacığı oluşturma sorunları nedeniyle kilitlenme [#7103](https://github.com/NuGet/Home/issues/7103)

* DotNet ekleme paket yerel yapılandırmada - belirtilen bir kaynak için kimlik bilgilerini genel yapılandırmadan kullanmayacağınız [#6935](https://github.com/NuGet/Home/issues/6935)

* İş parçacığı oluşturma sorunları olan MEF ile zaman uyumsuz yollarında üzerinde - adlı [#6771](https://github.com/NuGet/Home/issues/6771)

* İmzalama: iki kez ve çağrı yığını - olmadan bildirilen hata [#6455](https://github.com/NuGet/Home/issues/6455)

* Güvenilmeyen bir imzalama sertifikasıyla imzalanmış paket yükleme hatası: göstermelidir [#6318](https://github.com/NuGet/Home/issues/6318)

* NuGet geri yükleme yanlış Noop'ler obj dizinindeki - 2 projeleri paylaşırken [#6114](https://github.com/NuGet/Home/issues/6114)

* Kimliği doğrulanmış akışındaki - paketleri ile Linux'ta dotnet restore PAT kullanamazsınız [#5651](https://github.com/NuGet/Home/issues/5651)

* DotNet restore başarısız akışı - devre dışı makine nedeniyle geniş [#5410](https://github.com/NuGet/Home/issues/5410)

#### <a name="dcrs"></a>Dcr

* NuGet 5.0 derlemeleri (TFM değişiklik) - .NET 4.7.2 gerektirecek şekilde [#7510](https://github.com/NuGet/Home/issues/7510)

* NuGetLicenseData NuGet.Packaging gelen genel bir tür olmalıdır. Spdx alınan lisans meta verileri güncelleştirin. - [#7471](https://github.com/NuGet/Home/issues/7471)

* Eski ayarları API'ler - kaldırma [#7294](https://github.com/NuGet/Home/issues/7294)

* Geçici çözüm geri yükleme zaman aşımı 1 ile sistemlerinde cpu - [#6742](https://github.com/NuGet/Home/issues/6742)

* NuGet, NTLM kimlik doğrulamasını olsa bile kimlik bilgilerini NuGet.config içinde tercih - kimlik - bilgileri için kimlik doğrulama türlerini filtreleme yapılandırma seçeneği ekleme [#5286](https://github.com/NuGet/Home/issues/5286)

* PackageReference için (eşleşen Packages.Config yeteneği) - EmbedInteropTypes etkinleştirmek [#2365](https://github.com/NuGet/Home/issues/2365)

[Bu yayın 5.0.0-preview2 içinde düzeltilen tüm sorunlara listesi](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")


## <a name="known-issues"></a>Bilinen sorunlar

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a>DotNet nuget push--etkileşimli Mac üzerinde bir hata verir. - [#7519](https://github.com/NuGet/Home/issues/7519)

#### <a name="issue"></a>Sorun
`--interactive` Bağımsız değişken dotnet CLI tarafından iletilmez değil ve hataya neden olur `error: Missing value for option 'interactive'`

#### <a name="workaround"></a>Geçici Çözüm
Etkileşimli seçeneğiyle gibi diğer dotnet komutu çalıştırmak `dotnet restore --interactive` ve kimlik doğrulaması. Ardından kimlik doğrulama kimlik bilgisi sağlayıcı tarafından önbelleğe alınabilir. Ardından çalıştırın `dotnet nuget push`.

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>.NET Core SDK'sı tarafından yüklenen FallbackFolders paketlerinde özel olarak yüklü olan ve imza doğrulaması başarısız. - [#7414](https://github.com/NuGet/Home/issues/7414)

#### <a name="issue"></a>Sorun
DotNet.exe kullanırken bir proje bu çok hedefleri netcoreapp geri yüklemek için 2.x 1.x ve netcoreapp 2.x, geri dönüş klasörüne bir dosya akışı olarak kabul edilir. Bunun anlamı geri yüklerken, NuGet geri dönüş klasöründen paketi seçin ve genel paketleri klasörüne yükleyin ve başarısız her zamanki imza doğrulama yapmak deneyin.

#### <a name="workaround"></a>Geçici Çözüm
Geri dönüş klasör kullanımı ayarlayarak devre dışı bırakmanız `RestoreAdditionalProjectSources` Nothing. `<RestoreAdditionalProjectSources/>` Bu dikkatli olmalıdır aksi halde, NuGet.org adresinden yüklenecek paketler birçok neden olacak şekilde geri yüklendi geri dönüş klasöründen kullanın.
