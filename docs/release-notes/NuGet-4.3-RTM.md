---
title: NuGet 4.3 RTM sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere NuGet 4.3 RTM için sürüm notları.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: cb44f47ef0b3bd086f0a681cb2fedc7c5afc42fa
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-43-rtm-release-notes"></a>NuGet 4.3 RTM sürüm notları

[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) NuGet 4.3 .NET standart 2.0/.NET Core 2.0 gibi yeni senaryolara desteği birçok kalite düzeltmeleri içerir ve performansı artırır ekleyen RTM ile birlikte gelir. Bu sürüm ayrıca anlamsal sürüm oluşturma 2.0.0, MSBuild tümleştirme için destek gibi çeşitli iyileştirmeler NuGet uyarıları ve hataları ve daha fazla getirir.

## <a name="known-issues"></a>Bilinen sorunlar

### <a name="nuget-restore-may-treat-disabled-package-sources-as-enabled-in-some-cases"></a>NuGet geri yükleme bazı durumlarda devre dışı bırakılan paket kaynaklarını etkin olarak değerlendirebilir

#### <a name="issue"></a>Sorun

Aşağıdaki geri yükleme komut satırı teknikleri devre dışı bırakılan paketler kaynakları etkin olarak kabul eder. [NuGet#5704](https://github.com/NuGet/Home/issues/5704)
- `msbuild /t:restore`
- `dotnet restore` (VS veya bir ile birlikte dotnet.exe ile birlikte gelen 2.0.0 NetCore SDK ile birlikte)

#### <a name="workaround"></a>Geçici Çözüm

1. Visual Studio (2017 15.3 veya üzeri) ya da NuGet.exe (v4.3.0 veya üzeri) kullanın
1. Devre dışı bırakılmış kaynağınızı silin ve msbuild veya dotnet.exe kullanmaya devam edin.
1. Çözümünüz için, NuGet.config içinde "Clear" kullanabilir ve daha sonra bu çözüm için gerekli kaynakları tanımlayabilirsiniz.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>Paket Yöneticisi Konsolu’nu kullanırken, 'Enter' tuşu çalışmayabilir

#### <a name="issue"></a>Sorun

Bazen Paket Yöneticisi Konsolu’nda Enter tuşu çalışmıyor. Bunu görürseniz, lütfen düzeltmeye yönelik ilerlemeye göz atın ve yeniden oluşturma adımlarınız hakkında yararlı olabilecek ek bilgileri paylaşın. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Geçici Çözüm

Visual Studio’yu yeniden başlatın ve çözümü açmadan önce PMC’yi açın. Alternatif olarak, silmeyi deneyin `project.lock.json` ve yeniden geri yükleme.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Görüntüleme, ekleme ya da DotNetCLITools, Nuget Paket Yöneticisi'ni kullanarak güncelleştirme

#### <a name="issue"></a>Sorun

NuGet Paket Yöneticisi DotNetCLITools’u görüntülemez ve eklemeye/güncelleştirmeye izin vermez. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>Geçici Çözüm

Proje dosyanızda DotNetCLIToolReferences el ile düzenlenmelidir.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>Hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir

#### <a name="issue"></a>Sorun

Visual Studio’da hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir. Bu durum, paket yöneticisi biçimi olarak PackageReferences kullandığınızda ortaya çıkar. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Geçici Çözüm

El ile geri yükleme yapın.

## <a name="issues-fixed-in-nuget-43-rtm-timeframe"></a>4.3 NuGet RTM zaman çerçevesinde giderilen sorunlar

[NuGet 4.0 RTM sürüm notları](../release-notes/nuget-4.0-RTM.md) -NuGet 4.0 RTM için sabit tüm sorunları listeler

### <a name="features"></a>Özellikler

- NuGet Restore Perf - uygulama akıllı sekmeyi komut satırı geri yükleme - ve VS artırmak [#5080](https://github.com/NuGet/Home/issues/5080)

- NET çekirdek 2.0: VS/Dotnet CLI varolan NuGet işlevini kullanarak başlamanız gerekir: geri dönüş klasörleri - [#4939](https://github.com/NuGet/Home/issues/4939)

- NET çekirdek 2.0: Etkinleştirmek belirli geri yükleme uyarılarını gözardı (veya hata yükseltmek) - kullanıcılar [#4898](https://github.com/NuGet/Home/issues/4898)

- NET çekirdek 2.0: CLI yerelleştirilmiş derlemeler - [#4896](https://github.com/NuGet/Home/issues/4896)

- NET çekirdek 2.0: tüm uyarılar/hataları (PackageTargetFallback dahil) - varlıklar dosyaya Kaydet [#4895](https://github.com/NuGet/Home/issues/4895)

- TFM desteğini etkinleştirin: NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)

- NuGet.Core NuGet.Client projeleri (ve dolayısıyla DLL'ler) - sayısını azaltın [#2446](https://github.com/NuGet/Home/issues/2446)

- Nuget uyarıları hata - olarak işaretlemek için özelliğini ekler [#2395](https://github.com/NuGet/Home/issues/2395)

### <a name="bugs"></a>Hatalar

- MSBuild /t:pack başarısız "DevelopmentDependency" parametresi "PackTask" görevi tarafından - desteklenmiyor [#5584](https://github.com/NuGet/Home/issues/5584)

- İçerik dosyaları için dizin yapısını düzleştirilmiş Windows dizin ayırıcı ise PackagePath - sonunda eklenmiyor varsa [#4795](https://github.com/NuGet/Home/issues/4795)

- netcore projeleri ayarı developmentDependency - olarak desteklemez [#4694](https://github.com/NuGet/Home/issues/4694)

- RestoreManagerPackage yükleniyor zaman uyumlu olarak engellenen kullanıcı Arabirimi iş parçacığı ve VS - karşılıklı [#4679](https://github.com/NuGet/Home/issues/4679)

- DotNet
  - dotnetcore geri yükleme (ve bu nedenle msbuild /t:restore) bir açık çözüm proje bağımlılığı projelerle atlar [#4578](https://github.com/NuGet/Home/issues/4578)

- Çözümünüzü farklı büyük/küçük harf, aynı projenin başvurduğu projectreferences varsa geri yükleme çalışmayabilir. Bu da büyük/küçük harf - fark olmadan farklı göreli yollar etkiler [#4574](https://github.com/NuGet/Home/issues/4574)

- NuGet paketleri geri yürütülebilir .NET Core 2.0 ile - yürütülebilir dosyalar artık [#4424](https://github.com/NuGet/Home/issues/4424)

- Çözüm dosyası - ayrıştırılırken özel durum ayrıntılarını NuGet.exe yuttuğu [#4411](https://github.com/NuGet/Home/issues/4411)

- Paketi Windows - '/' ile biten bir yolu ContentTargetFolders içeriyorsa, bu içerik dosyalarını yanlış konuma yerleştirir [#4407](https://github.com/NuGet/Home/issues/4407)

- Bu hedefleri netcoreapp1.1 - bir Araçları Paketi için bir DotNetCliToolReference geri yükleyemezsiniz [#4396](https://github.com/NuGet/Home/issues/4396)

- Proje dosyası (C++) - Nuget güncelleştirme CLI bırakır eski Paket sürümü koşulu [#2449](https://github.com/NuGet/Home/issues/2449)

### <a name="dcrs"></a>Dcr

- CPS nomation - gelen okuma DotnetCliToolTargetFramework [#5397](https://github.com/NuGet/Home/issues/5397)

- TPMinV onay pj stili UWP - çalışmalıdır [#4763](https://github.com/NuGet/Home/issues/4763)

- AutoReferenced paketler - UI açıklamasını artırmak [#4471](https://github.com/NuGet/Home/issues/4471)

- NuGet restore derleme varlıklar çalışma zamanı bölümünden seçmektir. - [#4207](https://github.com/NuGet/Home/issues/4207)

- Bağımlılık tanılama kilit dosyası - put [#1599](https://github.com/NuGet/Home/issues/1599)

## <a name="links-to-github-issues-fixed-in-43-rtm"></a>GitHub sorunları 4.3 RTM'de sabit bağlantılar

[Konu listesi](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")
