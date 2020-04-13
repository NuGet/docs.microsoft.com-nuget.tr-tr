---
title: NuGet 4.3 RTM Yayın Notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve DCR'ler dahil olmak üzere NuGet 4.3 RTM için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 72d707cb9bacd8abbac873ee10b2fd00f233d3cc
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496588"
---
# <a name="nuget-43-release-notes"></a>NuGet 4.3 Sürüm Notları

[Visual Studio 2017 15.3 RTW,](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) .NET Standard 2.0/.NET Core 2.0 gibi yeni senaryolara destek ekleyen, birçok kalite düzeltmesi içeren ve performansı artıran NuGet 4.3 RTM ile birlikte geliyor. Bu sürüm aynı zamanda Anlamsal Sürüm 2.0.0, NuGet uyarı ve hatalarımsbuild entegrasyonu ve daha fazlası için destek gibi çeşitli iyileştirmeler getiriyor.

## <a name="summary-whats-new-in-430"></a>Özeti: 4.3.0 Yenilikler

## <a name="summary-whats-new-in-431"></a>Özet: 4.3.1'de Yenilikler

* Güvenlik Düzeltmesi: ~/.nuget içinde oluşturulan dosyalardaki izinler [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757) [#7673](https://github.com/NuGet/Home/issues/7673) çok açıktır
* Güvenlik Düzeltmesi: NUPKG'lerin içindeki [dosyalar,](https://github.com/NuGet/Home/issues/7906) NUPKG dizininin üzerinde göreli bir yola sahip olabilir #7906

## <a name="known-issues"></a>Bilinen sorunlar

### <a name="nuget-restore-may-treat-disabled-package-sources-as-enabled-in-some-cases"></a>NuGet geri yükleme bazı durumlarda devre dışı bırakılan paket kaynaklarını etkin olarak değerlendirebilir

#### <a name="issue"></a>Sorun

Aşağıdaki geri yükleme komut satırı teknikleri devre dışı bırakılan paket kaynaklarını etkin olarak ele alır. [NuGet#5704](https://github.com/NuGet/Home/issues/5704)
- `msbuild /t:restore`
- `dotnet restore`(ya dotnet.exe ile vs ile gemi, ya da NetCore SDK 2.0.0 ile birlikte gelen)

#### <a name="workaround"></a>Geçici çözüm

1. Visual Studio (2017 15.3 veya üzeri) ya da NuGet.exe (v4.3.0 veya üzeri) kullanın
1. Devre dışı bırakılmış kaynağınızı silin ve msbuild veya dotnet.exe kullanmaya devam edin.
1. Çözümünüz için, NuGet.config içinde "Clear" kullanabilir ve daha sonra bu çözüm için gerekli kaynakları tanımlayabilirsiniz.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>Paket Yöneticisi Konsolu’nu kullanırken, 'Enter' tuşu çalışmayabilir

#### <a name="issue"></a>Sorun

Bazen Paket Yöneticisi Konsolu’nda Enter tuşu çalışmıyor. Bunu görürseniz, lütfen düzeltmeye yönelik ilerlemeye göz atın ve yeniden oluşturma adımlarınız hakkında yararlı olabilecek ek bilgileri paylaşın. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Geçici çözüm

Visual Studio’yu yeniden başlatın ve çözümü açmadan önce PMC’yi açın. Alternatif olarak, silme `project.lock.json` ve yeniden geri deneyin.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Nuget Package Manager'ı kullanarak DotNetCLITools'u görüntüleyemiyor, ekleyemiyor veya güncelleştiremiyorsunuz

#### <a name="issue"></a>Sorun

NuGet Paket Yöneticisi DotNetCLITools’u görüntülemez ve eklemeye/güncelleştirmeye izin vermez. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>Geçici çözüm

Proje dosyanızda DotNetCLIToolReferences el ile düzenlenmelidir.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>Hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir

#### <a name="issue"></a>Sorun

Visual Studio’da hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir. Bu durum, paket yöneticisi biçimi olarak PackageReferences kullandığınızda ortaya çıkar. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Geçici çözüm

El ile geri yükleme yapın.

## <a name="issues-fixed-in-nuget-43-rtm-timeframe"></a>NuGet 4.3 RTM zaman diliminde düzeltilen sorunlar

[NuGet 4.0 RTM Yayın Notları](../release-notes/nuget-4.0-RTM.md) - NuGet 4.0 RTM için düzeltilen tüm sorunları listeler

### <a name="features"></a>Özellikler

- NuGet Geri Yükleme Perf'i geliştirin - Komut satırı geri yüklemeleri ve VS için akıllı NoOp [uygulayın](https://github.com/NuGet/Home/issues/5080) - #5080

- NET Core 2.0: VS/Dotnet CLI mevcut NuGet işlevselliğini kullanmaya başlamalı: FallBack klasörleri - [#4939](https://github.com/NuGet/Home/issues/4939)

- NET Core 2.0: Kullanıcıların belirli geri yükleme uyarılarını (veya hataya yükseltmeyi) yok saymalarını sağlama [- #4898](https://github.com/NuGet/Home/issues/4898)

- NET Core 2.0: CLI lokalize derlemeler - [#4896](https://github.com/NuGet/Home/issues/4896)

- NET Core 2.0: tüm uyarıları/hataları varlık dosyasına kaydedin (PackageTargetFallback dahil) - [#4895](https://github.com/NuGet/Home/issues/4895)

- TFM desteğini etkinleştirin: NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)

- NuGet.Core ve NuGet.Client projelerinin (ve dolayısıyla DL'lerin) sayısını #2446 [#2446](https://github.com/NuGet/Home/issues/2446)

- Nuget uyarılarını hata olarak işaretleme özelliği ekleme - [#2395](https://github.com/NuGet/Home/issues/2395)

### <a name="bugs"></a>Hatalar

- msbuild /t:pack "DevelopmentDependency" parametresi ile başarısız olur "PackTask" görevi tarafından desteklenmez - [#5584](https://github.com/NuGet/Home/issues/5584)

- PackagePath sonunda Windows dizin ayırıcı sıyrık değilse düzleştirilmiş içerik dosyaları için dizin yapısı - [#4795](https://github.com/NuGet/Home/issues/4795)

- netcore projeleri kalkınmaBağımlılık olarak ayarı desteklemiyor - [#4694](https://github.com/NuGet/Home/issues/4694)

- RestoreManagerPackage, Kullanıcı BirA ipliği ve kilitlenmemiş VS'yi engelleyen senkronize olarak yükleniyor - [#4679](https://github.com/NuGet/Home/issues/4679)

- dotnet
  - dotnetcore Geri Yükleme (& nedenle msbuild /t:restore) açık bir çözüm proje bağımlılığı ile projeleri atlar [#4578](https://github.com/NuGet/Home/issues/4578)

- Çözümünüzde aynı projeye atıfta bulunan ve farklı kasalarla başvuru yapan proje referansları varsa, geri yükleme çalışmayabilir. Bu da kasa bir fark olmadan, farklı göreli yolları etkiler - [#4574](https://github.com/NuGet/Home/issues/4574)

- NuGet paketlerinden geri yüklenen çalıştırılabilir ler artık .NET Core 2.0 ile çalıştırılamaz - [#4424](https://github.com/NuGet/Home/issues/4424)

- NuGet.exe çözüm dosyasını ayrıştırken istisnanın ayrıntılarını yutar - [#4411](https://github.com/NuGet/Home/issues/4411)

- ContentTargetFolders Windows'da '/' ile biten bir yol içeriyorsa Paket içerik dosyalarını yanlış konuma getirir - [#4407](https://github.com/NuGet/Home/issues/4407)

- Netcoreapp1.1 hedefleyen bir araç paketi için Bir DotNetCliToolReference geri [yükleyemezsiniz](https://github.com/NuGet/Home/issues/4396) - #4396

- Nuget güncelleştirmecli proje dosyasında (C++) eski paket sürüm koşulu bırakır - [#2449](https://github.com/NuGet/Home/issues/2449)

### <a name="dcrs"></a>DCRs

- CPS nomation gelen DotnetCliToolTargetFramework okuyun - [#5397](https://github.com/NuGet/Home/issues/5397)

- TPMinV kontrol pj tarzı UWP için çalışması gerekir - [#4763](https://github.com/NuGet/Home/issues/4763)

- Otomatik Başvurulan paketler için Ara Kullanma Arabirimi açıklamasını geliştirme - [#4471](https://github.com/NuGet/Home/issues/4471)

- NuGet geri yükleme çalışma zamanı bölümünden varlıkları derleme seçiyor. - [#4207](https://github.com/NuGet/Home/issues/4207)

- Bağımlılık tanılamayı kilit dosyasına koyun - [#1599](https://github.com/NuGet/Home/issues/1599)

## <a name="links-to-github-issues-fixed-in-43-rtm"></a>4.3 RTM'de düzeltilen GitHub sorunlarına bağlantılar

[Sorunlar Listesi](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")
