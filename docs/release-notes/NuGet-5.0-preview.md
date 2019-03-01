---
title: NuGet 5.0-preview sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, yeni özellikler ve dcr dahil olmak üzere NuGet 5.0 Önizleme için sürüm notları.
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: 57b66b347ac47a3d05907a4bb237002de8981ecc
ms.sourcegitcommit: 85bf94e0efcfcee1f914650bdc142309ef3e06d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57196206"
---
# <a name="nuget-50-preview-release-notes"></a>NuGet 5.0 Preview sürüm notları

## <a name="nuget-50-preview-releases"></a>NuGet 5.0 Önizleme sürümleri

* 27 Şubat 2010 - [NuGet 5.0 Preview 4](#summary-whats-new-in-50-preview-4)
* 13 Şubat 2019 - [NuGet 5.0 Preview 3](#summary-whats-new-in-50-preview-3)
* 23 Ocak 2019 - [NuGet 5.0 Önizleme 2](#summary-whats-new-in-50-preview-2)

## <a name="summary-whats-new-in-nuget-50-preview-4"></a>Özet: NuGet 5.0 Preview 4 sürümünde yenilikler nelerdir?

### <a name="issues-fixed-in-this-release"></a>Bu sürümde giderilen sorunlar

**Hataları:**

* NuGet.VisualStudio.IVsPackageInstaller - arama bir projede yok Paketle başvuran her zaman kullandığı packages.config Packagereference'a - varsayılan olarak ayarlanmış olsa bile [#7005](https://github.com/NuGet/Home/issues/7005)

* PMC: Update-Package başarısız olursa ("paketi bulmak için yapılandırılamıyor") delisted paketleri yeniden yükleyin. - [#7268](https://github.com/NuGet/Home/issues/7268)

* Bizim depo ve VSIX - üçüncü taraf bildirimi eklemek [#7409](https://github.com/NuGet/Home/issues/7409)

* NuGet.VisualStudio.IVsPackageInstaller.InstallPackage verilen - sürüm, en son sürümünü yüklemelisiniz [#7493](https://github.com/NuGet/Home/issues/7493)

* --dotnet nuget gönderim için etkileşimli desteği - [#7519](https://github.com/NuGet/Home/issues/7519)

* Kilit dosyasıyla geri yüklerken NU1603 uyarı oluşturuldu olmamalıdır. - [#7529](https://github.com/NuGet/Home/issues/7529)

* NuGet yazdırma proje yolu en az günlük ile-geri yükleme işlemi sırasında [#7647](https://github.com/NuGet/Home/issues/7647)

* --dotnet etkileşimli desteğini kaldırmak paket - [#7727](https://github.com/NuGet/Home/issues/7727)

* Ekleme ile TypeForwardedTo attrs - NuGet.Packaging.Core geri [#7768](https://github.com/NuGet/Home/issues/7768)

* plugins_cache iyi - çalışması için daha kısa bir yol gerekiyor [#7770](https://github.com/NuGet/Home/issues/7770)

* Kullanıcı için belirli msbuild sürümü - istememiş msbuild bulma yolunu tercih [#7786](https://github.com/NuGet/Home/issues/7786)

**Dcr:**

* http isteği aracılığıyla NuGet.Config - kaynak sayısı sınırlamak [#4538](https://github.com/NuGet/Home/issues/4538)

* NuGet (temizleme VSIX'in 16,0 derleme yardımcı olmak için) Net472 - hedef [#7143](https://github.com/NuGet/Home/issues/7143)

* PMC: -OpenPackagePage komutu kaldırmak [#7384](https://github.com/NuGet/Home/issues/7384)

* NetStandard 2.1 - yapma NetCoreApp 3.0 eşlemesine [#7762](https://github.com/NuGet/Home/issues/7762)

* NuGet.* paketlere - netstandard2.0 desteği Ekle [#6516](https://github.com/NuGet/Home/issues/6516)


## <a name="summary-whats-new-in-nuget-50-preview-3"></a>Özet: NuGet 5.0 Preview 3 yenilikler nelerdir?

### <a name="issues-fixed-in-this-release"></a>Bu sürümde giderilen sorunlar 

**Hataları:**

* nuget.exe /? doğru msbuild sürümler - listelemelidir [#7794](https://github.com/NuGet/Home/issues/7794)

* NuGet.targets(498,5): hata: Yolun bir bölümü bulunamadı. ' / tmp/NuGetScratch - mono üzerinde- [#7793](https://github.com/NuGet/Home/issues/7793)

* geri yükleme - makine önbelleğinde başvurulan paketin tüm sürümlerini içeriğini gereksiz yere numaralandırır [#7639](https://github.com/NuGet/Home/issues/7639)

* MSBuild otomatik algılamayı 2019 yükleme Önizleme sonra - 16,0 her zaman seçer [#7621](https://github.com/NuGet/Home/issues/7621)

* yinelenen girişler için framework - dotnet bir çözüm üzerinde paket listeleme çıkarır [#7607](https://github.com/NuGet/Home/issues/7607)

* Özel durum "boş yol adı değil yasal" ne zaman eski üzerinde arama IVsPackageInstaller.InstallPackage projeleri ve klasörü paketler yok. - [#5936](https://github.com/NuGet/Home/issues/5936)

* MSBuild/t: Restore en az ayrıntı düzeyi daha az - [#4695](https://github.com/NuGet/Home/issues/4695)

**Dcr:**

* Derleme varlıklar geçişli davranışı - tanımlamak paket yazarlarının [#6091](https://github.com/NuGet/Home/issues/6091)

* Proje çözümün bir parçası değil veya yüklü değil, ancak daha önce yüklendi - başarılı olması için VS geri yükleme etkinleştirme [#5820](https://github.com/NuGet/Home/issues/5820)


## <a name="summary-whats-new-in-50-preview-2"></a>Özet: 5.0 Önizleme 2'de yenilikler nelerdir?

### <a name="issues-fixed-in-this-release"></a>Bu sürümde giderilen sorunlar

**Hataları:**

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

**Dcr:**

* NuGet 5.0 derlemeleri (TFM değişiklik) - .NET 4.7.2 gerektirecek şekilde [#7510](https://github.com/NuGet/Home/issues/7510)

* NuGetLicenseData NuGet.Packaging gelen genel bir tür olmalıdır. Spdx alınan lisans meta verileri güncelleştirin. - [#7471](https://github.com/NuGet/Home/issues/7471)

* Eski ayarları API'ler - kaldırma [#7294](https://github.com/NuGet/Home/issues/7294)

* Geçici çözüm geri yükleme zaman aşımı 1 ile sistemlerinde cpu - [#6742](https://github.com/NuGet/Home/issues/6742)

* NuGet, NTLM kimlik doğrulamasını olsa bile kimlik bilgilerini NuGet.config içinde tercih - kimlik - bilgileri için kimlik doğrulama türlerini filtreleme yapılandırma seçeneği ekleme [#5286](https://github.com/NuGet/Home/issues/5286)

* PackageReference için (eşleşen Packages.Config yeteneği) - EmbedInteropTypes etkinleştirmek [#2365](https://github.com/NuGet/Home/issues/2365)

[Bu yayın 5.0.0-preview2 içinde düzeltilen tüm sorunlara listesi](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

### <a name="known-issues"></a>Bilinen sorunlar

#### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>.NET Core SDK'sı tarafından yüklenen FallbackFolders paketlerinde özel olarak yüklü olan ve imza doğrulaması başarısız. - [#7414](https://github.com/NuGet/Home/issues/7414)
**Sorunu** dotnet.exe kullanırken bir proje bu çok hedefleri netcoreapp geri yüklemek için 2.x 1.x ve netcoreapp 2.x, geri dönüş klasörüne bir dosya akışı olarak kabul edilir. Bunun anlamı geri yüklerken, NuGet geri dönüş klasöründen paketi seçin ve genel paketleri klasörüne yükleyin ve başarısız her zamanki imza doğrulama yapmak deneyin.
**Geçici çözüm** ayarlayarak geri dönüş klasörü kullanımını devre dışı `RestoreAdditionalProjectSources` Nothing. `<RestoreAdditionalProjectSources/>` Bu dikkatli olmalıdır aksi halde, NuGet.org adresinden yüklenecek paketler birçok neden olacak şekilde geri yüklendi geri dönüş klasöründen kullanın.
