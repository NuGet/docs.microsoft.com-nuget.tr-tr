---
title: NuGet 4.3 RTM sürüm notları
description: NuGet bilinen sorunları, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr 4.3 RTM için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 4bee32995884f4c003ebb963d2fd5b2d04363bab
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551630"
---
# <a name="nuget-43-rtm-release-notes"></a>NuGet 4.3 RTM sürüm notları

[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) NuGet 4.3 desteği gibi .NET Standard 2.0/.NET Core 2.0, yeni senaryolar için birçok kalite düzeltmeleri içerir ve performansı geliştirir ekleyen RTM ile birlikte gelir. Bu sürüm ayrıca NuGet uyarıları ve hataları ve daha fazlasını Semantic Versioning 2.0.0, MSBuild tümleştirmesi için destek gibi çeşitli iyileştirmeler getirir.

## <a name="known-issues"></a>Bilinen sorunlar

### <a name="nuget-restore-may-treat-disabled-package-sources-as-enabled-in-some-cases"></a>NuGet geri yükleme bazı durumlarda devre dışı bırakılan paket kaynaklarını etkin olarak değerlendirebilir

#### <a name="issue"></a>Sorun

Aşağıdaki geri yükleme komut satırı teknikleri, devre dışı paket kaynaklarını etkin olarak değerlendirin. [NuGet#5704](https://github.com/NuGet/Home/issues/5704)
- `msbuild /t:restore`
- `dotnet restore` (VS ile birlikte gelen dotnet.exe veya NetCore SDK 2.0.0 ile birlikte gelen bir ikisiyle)

#### <a name="workaround"></a>Geçici Çözüm

1. Visual Studio (2017 15.3 veya üzeri) ya da NuGet.exe (v4.3.0 veya üzeri) kullanın
1. Devre dışı bırakılmış kaynağınızı silin ve msbuild veya dotnet.exe kullanmaya devam edin.
1. Çözümünüz için, NuGet.config içinde "Clear" kullanabilir ve daha sonra bu çözüm için gerekli kaynakları tanımlayabilirsiniz.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>Paket Yöneticisi Konsolu’nu kullanırken, 'Enter' tuşu çalışmayabilir

#### <a name="issue"></a>Sorun

Bazen Paket Yöneticisi Konsolu’nda Enter tuşu çalışmıyor. Bunu görürseniz, lütfen düzeltmeye yönelik ilerlemeye göz atın ve yeniden oluşturma adımlarınız hakkında yararlı olabilecek ek bilgileri paylaşın. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Geçici Çözüm

Visual Studio’yu yeniden başlatın ve çözümü açmadan önce PMC’yi açın. Alternatif olarak, silmeyi deneyin `project.lock.json` ve yeniden geri yüklemeyi.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Görüntülenemiyor, eklenemiyor veya Nuget Paket Yöneticisi'ni kullanarak dotnetclıtools'u başlatamadı

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

- NuGet geri yükleme Perf - komut satırı geri yüklemeler için uygulama daha akıllı NoOp - ve VS geliştirmek [#5080](https://github.com/NuGet/Home/issues/5080)

- NET Core 2.0: VS/Dotnet CLI mevcut NuGet işlevini kullanarak başlamanız gerekir: geri dönüş klasörleri - [#4939](https://github.com/NuGet/Home/issues/4939)

- NET Core 2.0: Belirli bir geri yükleme uyarılarını gözardı (veya hataya yükseltmek) - kullanıcılar etkinleştirme [#4898](https://github.com/NuGet/Home/issues/4898)

- NET Core 2.0: CLI yerelleştirilmiş derlemeleri - [#4896](https://github.com/NuGet/Home/issues/4896)

- NET Core 2.0: tüm uyarılar/hatalar (PackageTargetFallback dahil) - varlıklar dosyaya Kaydet [#4895](https://github.com/NuGet/Home/issues/4895)

- TFM desteğini etkinleştir: NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)

- NuGet.Core NuGet.Client projeleri (ve bu nedenle DLL'ler) - sayısını azaltın [#2446](https://github.com/NuGet/Home/issues/2446)

- Nuget uyarıları hata - olarak işaretlemek için yapabilmenizi [#2395](https://github.com/NuGet/Home/issues/2395)

### <a name="bugs"></a>Hatalar

- MSBuild /t:pack başarısız "DevelopmentDependency" parametresi "PackTask" görev tarafından - desteklenmeyen [#5584](https://github.com/NuGet/Home/issues/5584)

- İçerik dosyaları için dizin yapısı, Windows dizin ayırıcı PackagePath - sonunda değil ekliyorsanız düzleştirilmiş [#4795](https://github.com/NuGet/Home/issues/4795)

- netcore projeleri ayarı developmentDependency - olarak desteklemez [#4694](https://github.com/NuGet/Home/issues/4694)

- RestoreManagerPackage yüklenme zaman uyumlu olarak engellenen kullanıcı Arabirimi iş parçacığı ve VS - kilitlendiğini [#4679](https://github.com/NuGet/Home/issues/4679)

- DotNet
  - dotnetcore geri yükleme (ve bu nedenle msbuild/t: Restore) bir açık çözüm proje bağımlılığı projeleriyle atlar [#4578](https://github.com/NuGet/Home/issues/4578)

- Aynı projeye farklı büyük/küçük harf, başvuran başvuruları çözümünüz varsa, geri yükleme çalışmayabilir. Bu da büyük/küçük harf - fark olmadan farklı göreli yollarla etkiler [#4574](https://github.com/NuGet/Home/issues/4574)

- NuGet paketleri geri yürütülebilir ile .NET Core 2.0 - yürütülebilir dosyalar artık [#4424](https://github.com/NuGet/Home/issues/4424)

- NuGet.exe - çözüm dosyası ayrıştırılırken özel durumun ayrıntılarını bastırır [#4411](https://github.com/NuGet/Home/issues/4411)

- Paketi ContentTargetFolders üzerinde Windows - '/' ile biten bir yolu içeriyorsa, bu içerik dosyalarını yanlış konuma koyar [#4407](https://github.com/NuGet/Home/issues/4407)

- Bu hedefleri netcoreapp1.1 - bir Araçları Paketi için bir DotNetCliToolReference geri yükleyemezsiniz [#4396](https://github.com/NuGet/Home/issues/4396)

- Nuget güncelleştirme CLI (C++) - proje dosyasında eski Paket sürümü koşul bırakır [#2449](https://github.com/NuGet/Home/issues/2449)

### <a name="dcrs"></a>Dcr

- CPS nomation - gelen okuma DotnetCliToolTargetFramework [#5397](https://github.com/NuGet/Home/issues/5397)

- UWP - pj stili TPMinV onay iş [#4763](https://github.com/NuGet/Home/issues/4763)

- Kullanıcı Arabirimi açıklama AutoReferenced paketlerinin - geliştirmek [#4471](https://github.com/NuGet/Home/issues/4471)

- NuGet geri yükleme, çalışma zamanı bölümünden derleme varlıklar seçmektir. - [#4207](https://github.com/NuGet/Home/issues/4207)

- Bağımlılık tanılama kilit dosyasında - put [#1599](https://github.com/NuGet/Home/issues/1599)

## <a name="links-to-github-issues-fixed-in-43-rtm"></a>GitHub sorunları 4.3 RTM'de sabit bağlantılar

[Sorun listesi](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")
