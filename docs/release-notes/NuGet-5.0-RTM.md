---
title: NuGet 5.0 RTM sürüm notları
description: NuGet bilinen sorunları, hata düzeltmeleri, yeni özellikler ve dcr dahil olmak üzere 5.0 için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 7e719a3bb5069c461820c6f884487af1eb04bf86
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610665"
---
# <a name="nuget-50-release-notes"></a>NuGet 5.0 sürüm notları

NuGet dağıtım araçları:

| NuGet sürüm | Visual Studio sürümü içinde kullanılabilir| .NET SDK'sı sürümünü kullanılabilir|
|:---|:---|:---|
| [**5.0.0**](https://nuget.org/downloads) | [Visual Studio 2019 16,0 sürümü](https://visualstudio.microsoft.com/downloads/) | [2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |
| [**5.0.2**](https://nuget.org/downloads) | [Visual Studio 2019 16.0.4 sürümü](https://visualstudio.microsoft.com/downloads/) | [2.1.60X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup>.NET Core iş yüküyle Visual Studio 2019 ile yüklü 

<sup>2</sup>.NET Core iş yüküyle Visual Studio 2019 ile isteğe bağlı bir yükleme olarak kullanılabilir

## <a name="summary-whats-new-in-50"></a>Özet: 5. 0'yenilikler nelerdir?

* Geri yükleme desteği [çözümleri filtrelenmiş](https://docs.microsoft.com/en-us/visualstudio/ide/filtered-solutions?view=vs-2019) Visual Studio 2019 içinde- [#5820](https://github.com/NuGet/Home/issues/5820)
* `BuildTransitive` Klasör sağlayan geçişli hedefleri/özellikler - ana projeye katkıda bulunmak paketleri [#6091](https://github.com/NuGet/Home/issues/6091)
* NuGet Iv'ler API'lerindeki - PackageReference senaryoları için daha iyi destek [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)
* `nuget.exe pack project.json` kullanım dışı - [#7928](https://github.com/NuGet/Home/issues/7928)
* 1. nesil kimlik bilgisi sağlayıcı eklentisi yerini tarafından [Gen 2](https://aka.ms/nuget-cross-platform-authentication-plugin) ve yakında kullanımdan - [#7819](https://github.com/NuGet/Home/issues/7819)

## <a name="issues-fixed-in-this-release"></a>Bu sürümde giderilen sorunlar

**Hataları**

* NoOp geri yükleme yaparken önlemek *. obj dizinindeki - dgspec.json yazma [#7854](https://github.com/NuGet/Home/issues/7854)

* ~/.Nuget içinde oluşturulan dosyalarda izinleri çok açık - [#7673](https://github.com/NuGet/Home/issues/7673)

* `dotnet list package --outdated` kimlik doğrulama - gereken kaynakları ile işe yaramazsa [#7605](https://github.com/NuGet/Home/issues/7605)

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

* `nuget.exe /?` doğru msbuild sürümler - listelemelidir [#7794](https://github.com/NuGet/Home/issues/7794)

* NuGet.targets(498,5): hata: Yolun bir bölümü bulunamadı. ' / tmp/NuGetScratch - mono üzerinde- [#7793](https://github.com/NuGet/Home/issues/7793)

* geri yükleme - makine önbelleğinde başvurulan paketin tüm sürümlerini içeriğini gereksiz yere numaralandırır [#7639](https://github.com/NuGet/Home/issues/7639)

* MSBuild otomatik algılamayı 2019 yükleme Önizleme sonra - 16,0 her zaman seçer [#7621](https://github.com/NuGet/Home/issues/7621)

* yinelenen girişler için framework - dotnet bir çözüm üzerinde paket listeleme çıkarır [#7607](https://github.com/NuGet/Home/issues/7607)

* Özel durum "boş yol adı değil yasal" ne zaman eski üzerinde arama IVsPackageInstaller.InstallPackage projeleri ve klasörü paketler yok. - [#5936](https://github.com/NuGet/Home/issues/5936)

* MSBuild/t: Restore en az ayrıntı düzeyi daha az - [#4695](https://github.com/NuGet/Home/issues/4695)

* VS 16,0'ın NuGet kullanıcı Arabirimi olan renk sorunları - nedeniyle okunamaz sekmeleri [#7735](https://github.com/NuGet/Home/issues/7735)

* NuGet.Core & NuGet.Clients License.txt açıklama - [#7629](https://github.com/NuGet/Home/issues/7629)

* Geri yükleme türü - belirlemek için gereksiz yere genel bir paket klasörüne numaralandırır [#7596](https://github.com/NuGet/Home/issues/7596)

* Kilit dosya zorlama hatalarından görünmesini Hata Listesi penceresinde - [#7429](https://github.com/NuGet/Home/issues/7429)

* NuGet.Configuration sorunlarını gidermek [#7326](https://github.com/NuGet/Home/issues/7326)

* MSBuild'e, yükleme güncelleştirme uyum konumu - [#7325](https://github.com/NuGet/Home/issues/7325)

* Bir geliştirme bağımlılığı - NuGet.Build.Tasks.Pack olmalıdır [#7249](https://github.com/NuGet/Home/issues/7249)

* Dahil etmek için paketi uzantı noktası ekleme hata ayıklama sembolleri - [#7234](https://github.com/NuGet/Home/issues/7234)

* `dotnet pack` oluşturulan nupkg bağımlılık sürüm aralığında (kayan sürümü kullanılıyorsa bile) - korumak [#7232](https://github.com/NuGet/Home/issues/7232)

* `dotnet restore` Kullanıcı düzeyinde yapılandırma kaynağı - varken kimliği doğrulanmış kaynak başarısız [#7209](https://github.com/NuGet/Home/issues/7209)

* Paketi için içerik dosyaları - BuildActions kümesini değil kısıtlama [#7155](https://github.com/NuGet/Home/issues/7155)

* Başarılı olması AssetTargetFallback gerektiren bir ProjectReference kullanarak bildirmelisiniz. - [#7137](https://github.com/NuGet/Home/issues/7137)

* CPS (CommonProjectSystem) - çağırırken iş parçacığı oluşturma sorunları nedeniyle kilitlenme [#7103](https://github.com/NuGet/Home/issues/7103)

* `dotnet add package` Yerel yapılandırmada - belirtilen bir kaynak için kimlik bilgilerini genel yapılandırmadan kullanmaz [#6935](https://github.com/NuGet/Home/issues/6935)

* MEF zaman uyumsuz olarak çağrılan ile iş parçacığı oluşturma sorunları kod yolları - [#6771](https://github.com/NuGet/Home/issues/6771)

* İmzalama: iki kez ve çağrı yığını - olmadan bildirilen hata [#6455](https://github.com/NuGet/Home/issues/6455)

* Güvenilmeyen bir imzalama sertifikasıyla imzalanmış paket yükleme hatası: göstermelidir [#6318](https://github.com/NuGet/Home/issues/6318)

* NuGet geri yükleme yanlış Noop'ler obj dizinindeki - 2 projeleri paylaşırken [#6114](https://github.com/NuGet/Home/issues/6114)

* PAT ile kullanamazsınız `dotnet restore` kimliği doğrulanmış akışındaki - paketleri ile Linux'ta [#5651](https://github.com/NuGet/Home/issues/5651)

* DotNet restore başarısız akışı - devre dışı makine nedeniyle geniş [#5410](https://github.com/NuGet/Home/issues/5410)

**Dcr**

* "Dotnet paketi project.json" - gelecekteki kaldırılmasını uyar [#7928](https://github.com/NuGet/Home/issues/7928)
 
* Bir Gen1 kimlik bilgisi eklentisi için-kullanımdan kaldırılma uyarısı Ekle [#7819](https://github.com/NuGet/Home/issues/7819)
 
* İmzalama: Etkin depo depo olarak her paketi, istemci doğrulama gerektirecek şekilde imzalanmış--RepositorySignatures/5.0.0 kaynağı aracılığıyla - [#7759](https://github.com/NuGet/Home/issues/7759)

* http isteği aracılığıyla NuGet.Config - kaynak sayısı sınırlamak [#4538](https://github.com/NuGet/Home/issues/4538)

* NuGet (temizleme VSIX'in 16,0 derleme yardımcı olmak için) Net472 - hedef [#7143](https://github.com/NuGet/Home/issues/7143)

* PMC: -OpenPackagePage komutu kaldırmak [#7384](https://github.com/NuGet/Home/issues/7384)

* NetStandard 2.1 - yapma NetCoreApp 3.0 eşlemesine [#7762](https://github.com/NuGet/Home/issues/7762)

* NuGet.* paketlere - netstandard2.0 desteği Ekle [#6516](https://github.com/NuGet/Home/issues/6516)

* Derleme varlıklar geçişli davranışı - tanımlamak paket yazarlarının [#6091](https://github.com/NuGet/Home/issues/6091)

* VS 2019 çözüm filtreleme özelliğini destekler. Ayrıca, proje çözümde değil veya yüklenmemiş projeleri destekler. Eksiksiz bir çözüm (aracılığıyla, CLI veya VS) ilk - geri yüklemeniz [#5820](https://github.com/NuGet/Home/issues/5820)

* NuGet 5.0 derlemeleri (TFM değişiklik) - .NET 4.7.2 gerektirecek şekilde [#7510](https://github.com/NuGet/Home/issues/7510)

* NuGetLicenseData NuGet.Packaging gelen genel bir tür olmalıdır. Spdx alınan lisans meta verileri güncelleştirin. - [#7471](https://github.com/NuGet/Home/issues/7471)

* Eski ayarları API'ler - kaldırma [#7294](https://github.com/NuGet/Home/issues/7294)

* Geçici çözüm geri yükleme zaman aşımı 1 ile sistemlerinde cpu - [#6742](https://github.com/NuGet/Home/issues/6742)

* NuGet, NTLM kimlik doğrulamasını olsa bile kimlik bilgilerini NuGet.config içinde tercih - kimlik - bilgileri için kimlik doğrulama türlerini filtreleme yapılandırma seçeneği ekleme [#5286](https://github.com/NuGet/Home/issues/5286)

* PackageReference için (eşleşen Packages.Config yeteneği) - EmbedInteropTypes etkinleştirmek [#2365](https://github.com/NuGet/Home/issues/2365)

**[Bu sürümde - 5.0 RTM düzeltilen tüm sorunlara listesi](https://github.com/NuGet/Home/milestone/84?closed=1)**

## <a name="summary-whats-new-in-502"></a>Özet: 5.0.2 yenilikler

* Güvenlik - (dotnet.exe veya mono.exe aracılığıyla çalıştırdığınızda) obj klasörü doğru izinler ile oluşturulması gereken [#7908](https://github.com/NuGet/Home/issues/7908)

* mono/macos'ta nuget.exe geri yükleme ile özel nuget.config başarısız olur ve `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)


## <a name="known-issues"></a>Bilinen sorunlar

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a>.NET Core SDK'sı tarafından yüklenen FallbackFolders paketlerinde özel olarak yüklü olan ve imza doğrulaması başarısız. - [#7414](https://github.com/NuGet/Home/issues/7414)
#### <a name="issue"></a>Sorun
DotNet.exe kullanırken bir proje bu çok hedefleri netcoreapp geri yüklemek için 2.x 1.x ve netcoreapp 2.x, geri dönüş klasörüne bir dosya akışı olarak kabul edilir. Bunun anlamı geri yüklerken, NuGet geri dönüş klasöründen paketi seçin ve genel paketleri klasörüne yükleyin ve başarısız her zamanki imza doğrulama yapmak deneyin.<br>
#### <a name="workaround"></a>Geçici Çözüm
Geri dönüş klasör kullanımı ayarlayarak devre dışı bırakmanız `RestoreAdditionalProjectSources` Nothing:

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

Geri dönüş klasöründen geri paketleri NuGet.org adresinden artık yüklenebilir olarak bunu dikkatli kullanın.
