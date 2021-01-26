---
title: NuGet 5,0 RTM sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, yeni özellikler ve CCR 'ler dahil olmak üzere NuGet 5,0 sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 637db1ae128ce020c33e54e56148c848a5f905a5
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776225"
---
# <a name="nuget-50-release-notes"></a>NuGet 5,0 sürüm notları

NuGet dağıtım araçlar:

| NuGet sürümü | Visual Studio sürümünde kullanılabilir| .NET SDK 'ları 'nda kullanılabilir|
|:---|:---|:---|
| [**5.0.0**](https://nuget.org/downloads) | [Visual Studio 2019 sürüm 16,0](https://visualstudio.microsoft.com/downloads/) | [2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |
| [**5.0.2**](https://nuget.org/downloads) | [Visual Studio 2019 sürüm 16.0.4](https://visualstudio.microsoft.com/downloads/) | [2.1.60 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup> .NET Core iş yüküne sahip Visual Studio 2019 ile yüklendi 

<sup>2</sup> .NET Core iş yüküne sahip Visual Studio 2019 ile isteğe bağlı bir install olarak kullanılabilir

## <a name="summary-whats-new-in-50"></a>Özet: 5,0 sürümündeki yenilikler

* Visual Studio 2019- [#5820](https://github.com/NuGet/Home/issues/5820) [filtrelenmiş çözümleri](/visualstudio/ide/filtered-solutions?view=vs-2019) geri yükleme desteği
* `BuildTransitive` klasör, paketlerin, ana bilgisayar projesine hedefe/props 'ın geçişli olarak katkıda bulunmasına olanak sağlar- [#6091](https://github.com/NuGet/Home/issues/6091)
* NuGet IVS API 'Lerinde PackageReference senaryoları için daha iyi destek [](https://github.com/NuGet/Home/issues/7005)-#7005 [#7493](https://github.com/NuGet/Home/issues/7493)
* `nuget.exe pack project.json` kullanım dışı bırakıldı- [#7928](https://github.com/NuGet/Home/issues/7928)
* Gen 1 kimlik bilgisi sağlayıcısı eklentisinin yerini [Gen 2](../reference/extensibility/nuget-cross-platform-authentication-plugin.md) ' den geçti ve yakında kullanım dışı bırakılacak [#7819](https://github.com/NuGet/Home/issues/7819)

## <a name="issues-fixed-in-this-release"></a>Bu sürümde giderilen sorunlar

**Hata**

* Bir NoOp geri yükleme işlemi yaparken, obj dizininde yazma sırasında * .dgspec.jsönleyin- [#7854](https://github.com/NuGet/Home/issues/7854)

* ~/5nuget içinde oluşturulan dosyalardaki izinler çok açık [#7673](https://github.com/NuGet/Home/issues/7673)

* `dotnet list package --outdated` kimlik doğrulaması gerektiren kaynaklarla çalışmaz [#7605](https://github.com/NuGet/Home/issues/7605)

* NuGet. VisualStudio. Ivspackageınstaller-Package başvuruları olmayan bir projede çağırmak, varsayılan, PackageReference- [#7005](https://github.com/NuGet/Home/issues/7005) olarak ayarlanmış olsa bile her zaman packages.config kullanır

* PMC: listelenen paketlerde yeniden yükleme Update-Package başarısız olur ("paket bulunamıyor"). - [#7268](https://github.com/NuGet/Home/issues/7268)

* Deponuz ve VSıX- [#7409](https://github.com/NuGet/Home/issues/7409) üçüncü taraf bildirimi ekleme

* Verilen sürüm olmadığında NuGet. VisualStudio. Ivspackageınstaller. InstallPackage en son sürümü yüklemelidir [#7493](https://github.com/NuGet/Home/issues/7493)

* --DotNet NuGet Push için etkileşimli destek- [#7519](https://github.com/NuGet/Home/issues/7519)

* Kilit dosyası ile geri yüklenirken, NU1603 uyarısı çıkarılmamalıdır. - [#7529](https://github.com/NuGet/Home/issues/7529)

* NuGet, en az günlük kaydı ile geri yükleme sırasında proje yolunu yazdırmamalıdır [#7647](https://github.com/NuGet/Home/issues/7647)

* --DotNet Remove Package- [#7727](https://github.com/NuGet/Home/issues/7727) için etkileşimli destek

* TypeForwardedTo attrs- [#7768](https://github.com/NuGet/Home/issues/7768) ile NuGet. paketleme. Core ' u geri ekleyin

* plugins_cache iyi çalışmak için daha kısa bir yol gerektirir [#7770](https://github.com/NuGet/Home/issues/7770)

* Kullanıcı belirli MSBuild sürümü için sorun olmadıysa MSBuild Discovery yolunu tercih et- [#7786](https://github.com/NuGet/Home/issues/7786)

* `nuget.exe /?` doğru MSBuild sürümlerini listelemelidir- [#7794](https://github.com/NuGet/Home/issues/7794)

* NuGet. targets (498, 5): hata: '/T MP/nugetkaralama-mono- [#7793](https://github.com/NuGet/Home/issues/7793) yolunun bir parçası bulunamadı

* geri yükleme, makine önbelleğinde başvurulan paketin tüm sürümlerinin içeriğini gereksiz şekilde numaralandırır [#7639](https://github.com/NuGet/Home/issues/7639)

* MSBuild otomatik algılama, VS 2019 Preview- [#7621](https://github.com/NuGet/Home/issues/7621) yüklendikten sonra her zaman 16,0 seçer.

* bir çözümde DotNet liste paketi çerçeve [#7607](https://github.com/NuGet/Home/issues/7607) için yinelenen girdileri çıktı

* Ispackageınstaller. InstallPackage eski projelerde ve paketler klasöründe çağrılırken "boş yol adı geçerli değil" özel durumu yok. - [#5936](https://github.com/NuGet/Home/issues/5936)

* MSBuild/t: geri yükleme minimum ayrıntı düzeyi daha az olmalıdır- [#4695](https://github.com/NuGet/Home/issues/4695)

* VS 16.0 'in NuGet Kullanıcı arabirimi, renk sorunları nedeniyle okunamaz sekmeye sahip- [#7735](https://github.com/NuGet/Home/issues/7735)

* NuGet. Core & NuGet. clients License.txt Açıklama- [#7629](https://github.com/NuGet/Home/issues/7629)

* Restore, Type- [#7596](https://github.com/NuGet/Home/issues/7596) belirleme denemesi sırasında genel paket klasörünü gereksiz şekilde numaralandırır

* Kilit dosyası zorlamasının hataları Hata Listesi pencere [#7429](https://github.com/NuGet/Home/issues/7429) göstermelidir

* NuGet.Configurlama sorunlarını giderme- [#7326](https://github.com/NuGet/Home/issues/7326)

* MSBuild 'e, yüklemesinin konumunu güncelleştirme- [#7325](https://github.com/NuGet/Home/issues/7325)

* NuGet. Build. Tasks. Pack bir geliştirme bağımlılığı olmalıdır- [#7249](https://github.com/NuGet/Home/issues/7249)

* Hata ayıklama sembolleri dahil olmak üzere paket uzantı noktası Ekle- [#7234](https://github.com/NuGet/Home/issues/7234)

* `dotnet pack` oluşturulan nupkg 'daki bağımlılık sürümü aralığının korunması gerekir (kayan sürüm kullanılıyorsa bile)- [#7232](https://github.com/NuGet/Home/issues/7232)

* `dotnet restore`Kullanıcı düzeyinde yapılandırma da kaynak [#7209](https://github.com/NuGet/Home/issues/7209) olduğunda kimliği doğrulanmış kaynakta başarısız olur

* Paket, içerik dosyaları için giriş kümesini kısıtlamamalıdır- [#7155](https://github.com/NuGet/Home/issues/7155)

* AssetTargetFallback 'nin başarılı olmasını gerektiren bir ProjectReference kullanmak, uyarı almalıdır. - [#7137](https://github.com/NuGet/Home/issues/7137)

* CPS (CommonProjectSystem)- [#7103](https://github.com/NuGet/Home/issues/7103) çağrılırken iş parçacığı sorunları nedeniyle kilitlenme

* `dotnet add package` Yerel yapılandırmada belirtilen bir kaynak için genel yapılandırmadan kimlik bilgileri kullanmaz- [#6935](https://github.com/NuGet/Home/issues/6935)

* Zaman uyumsuz kod yollarında MEF ile ilgili sorunları akıtma- [#6771](https://github.com/NuGet/Home/issues/6771)

* İmzalama: iki kez ve çağrı yığını olmadan hata bildirildi- [#6455](https://github.com/NuGet/Home/issues/6455)

* Güvenilir olmayan imzalama sertifikasıyla imzalı bir paketin yüklenmesi hata [#6318](https://github.com/NuGet/Home/issues/6318) göstermelidir

* NuGet geri yükleme 2 proje obj dizinini paylaşırken yanlış bir NoOps [#6114](https://github.com/NuGet/Home/issues/6114)

* `dotnet restore`Kimliği doğrulanmış akıştaki paketlerle Linux üzerinde with ile birlikte kullanılamaz- [#5651](https://github.com/NuGet/Home/issues/5651)

* dotnet restore devre dışı bırakılmış makine genelindeki akış nedeniyle başarısız olur [#5410](https://github.com/NuGet/Home/issues/5410)

**DCR**

* "DotNet Pack project.jsüzerinde"- [#7928](https://github.com/NuGet/Home/issues/7928) kaldırma işleminin daha sonra uyarı
 
* Gen1 Credential eklentisi için bir kullanımdan kaldırma uyarısı ekleyin- [#7819](https://github.com/NuGet/Home/issues/7819)
 
* İmzalama: yeniden depo imzalı olarak her pakette istemci doğrulaması gerektirmek için depoyu devre dışı bırak--yeniden Depoimzalar/5.0.0 kaynak- [#7759](https://github.com/NuGet/Home/issues/7759)

* NuGet.Config ile kaynak başına http istek sayısını sınırla [#4538](https://github.com/NuGet/Home/issues/4538)

* NuGet, Net472 target (VSıX 'in 16,0 derlemesini temizlemesine yardımcı olmak için). [#7143](https://github.com/NuGet/Home/issues/7143)

* PMC: OpenPackagePage komutunu kaldırma- [#7384](https://github.com/NuGet/Home/issues/7384)

* NetCoreApp 3,0 eşlemesini NetStandard 2,1- [#7762](https://github.com/NuGet/Home/issues/7762) yapın

* NuGet. * Packages- [#6516](https://github.com/NuGet/Home/issues/6516) için Netstandard 2.0 desteği ekleyin

* Paket yazarlarının derleme varlıkları geçişli davranış tanımlamasına izin ver- [#6091](https://github.com/NuGet/Home/issues/6091)

* Destek VS 2019 çözüm filtresi özelliği. Ayrıca, proje çözüm içinde değil veya yüklü projeleri destekler. Tüm çözümü geri yüklemeniz gerekiyor (CLı veya VS aracılığıyla) ilk [#5820](https://github.com/NuGet/Home/issues/5820)

* .NET 4.7.2 gerektirmek için NuGet 5,0 derlemeleri (tfd değişikliği aracılığıyla)- [#7510](https://github.com/NuGet/Home/issues/7510)

* NuGet. paketleme 'daki NuGetLicenseData ortak bir tür olmalıdır. Spdx 'den alınan lisans meta verilerini güncelleştirin. - [#7471](https://github.com/NuGet/Home/issues/7471)

* Eski ayarları kaldır API 'Leri [#7294](https://github.com/NuGet/Home/issues/7294)

* 1 CPU- [#6742](https://github.com/NuGet/Home/issues/6742) sistemlerdeki geçici çözüm geri yükleme zaman aşımları

* NuGet, kimlik bilgileri için kimlik doğrulama türlerini filtrelemek için NuGet.config-yapılandırma Ekle seçeneğinde kimlik bilgileri olsa da NTLM kimlik doğrulamasını tercih eder- [#5286](https://github.com/NuGet/Home/issues/5286)

* PackageReference için EmbedInteropTypes 'ı etkinleştirin (eşleşen Packages.Config özelliği)- [#2365](https://github.com/NuGet/Home/issues/2365)

**[Bu yayında düzeltilen tüm sorunların listesi-5,0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**

## <a name="summary-whats-new-in-502"></a>Özet: 5.0.2 'deki yenilikler

* Güvenlik (dotnet.exe veya mono.exe aracılığıyla çalıştırıldığında)-obj klasörü doğru izinlerle oluşturulmalıdır [#7908](https://github.com/NuGet/Home/issues/7908)

* Mono/MacOS üzerinde geri yükleme nuget.exe özel nuget.config ve `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011) başarısız oluyor


## <a name="known-issues"></a>Bilinen sorunlar

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a>.NET Core SDK tarafından yüklenen FallbackFolders paketleri özel olarak yüklenir ve imza doğrulaması başarısız olur. - [#7414](https://github.com/NuGet/Home/issues/7414)
#### <a name="issue"></a>Sorun
Birden çok hedef netcoreapp 1. x ve netcoreapp 2. x ' i hedefleyen bir projeyi geri yüklemek için dotnet.exe 2. x kullanırken, geri dönüş klasörü bir dosya akışı olarak kabul edilir. Bu, geri yükleme sırasında NuGet paketini geri dönüş klasöründen seçer ve genel paketler klasörüne yüklemeyi dener ve hata veren olağan imza doğrulamasını yapmak için kullanılır.<br>
#### <a name="workaround"></a>Geçici çözüm
Geri dönüş klasörünün kullanımını hiçbir şey olarak ayarlayarak devre dışı bırakın `RestoreAdditionalProjectSources` :

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

Geri dönüş klasöründen geri yüklenecek paketler artık NuGet.org adresinden indirileceği için bunu dikkatli kullanın.