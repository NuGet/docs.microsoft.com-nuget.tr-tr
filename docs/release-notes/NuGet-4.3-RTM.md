---
title: NuGet 4,3 RTM sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 4,3 RTM için sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: e9b6d15584d875f59ed64fe662944db3e37aeabb
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780173"
---
# <a name="nuget-43-release-notes"></a>NuGet 4,3 sürüm notları

[Visual Studio 2017 15,3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) , .NET Standard 2.0/. NET Core 2,0 gibi yeni senaryolar için destek ekleyen NUGET 4,3 RTM ile gelir ve birçok kalite düzeltmesi içerir ve performansı geliştirir. Bu sürüm ayrıca, anlamsal sürüm oluşturma 2.0.0, NuGet uyarıları ve hatalarının MSBuild tümleştirmesi ve daha fazlası için destek gibi çeşitli geliştirmeler de getirir.

## <a name="summary-whats-new-in-430"></a>Özet: 4.3.0 'deki yenilikler

## <a name="summary-whats-new-in-431"></a>Özet: 4.3.1 'deki yenilikler

* Güvenlik onarımı: ~/. NuGet içinde oluşturulan dosyalardaki Izinler çok açık [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)
* Güvenlik onarımı: NUPKGs içindeki dosyaların, NUPKG dizininin üzerinde göreli bir yolu olabilir [#7906](https://github.com/NuGet/Home/issues/7906)

## <a name="known-issues"></a>Bilinen sorunlar

### <a name="nuget-restore-may-treat-disabled-package-sources-as-enabled-in-some-cases"></a>NuGet geri yükleme bazı durumlarda devre dışı bırakılan paket kaynaklarını etkin olarak değerlendirebilir

#### <a name="issue"></a>Sorun

Aşağıdaki geri yükleme komut satırı teknikleri devre dışı paket kaynaklarını etkin olarak değerlendirir. [NuGet#5704](https://github.com/NuGet/Home/issues/5704)
- `msbuild /t:restore`
- `dotnet restore` (VS ile birlikte gelen dotnet.exe veya NetCore SDK 2.0.0 ile birlikte gelen bir ile birlikte)

#### <a name="workaround"></a>Geçici çözüm

1. Visual Studio (2017 15.3 veya üzeri) ya da NuGet.exe (v4.3.0 veya üzeri) kullanın
1. Devre dışı bırakılmış kaynağınızı silin ve msbuild veya dotnet.exe kullanmaya devam edin.
1. Çözümünüz için, NuGet.config içinde "Clear" kullanabilir ve daha sonra bu çözüm için gerekli kaynakları tanımlayabilirsiniz.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>Paket Yöneticisi Konsolu’nu kullanırken, 'Enter' tuşu çalışmayabilir

#### <a name="issue"></a>Sorun

Bazen Paket Yöneticisi Konsolu’nda Enter tuşu çalışmıyor. Bunu görürseniz, lütfen düzeltmeye yönelik ilerlemeye göz atın ve yeniden oluşturma adımlarınız hakkında yararlı olabilecek ek bilgileri paylaşın. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Geçici çözüm

Visual Studio’yu yeniden başlatın ve çözümü açmadan önce PMC’yi açın. Alternatif olarak, ' yi silmeyi `project.lock.json` ve geri yüklemeyi yeniden deneyin.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>NuGet Paket Yöneticisi 'Ni kullanarak Dotnetclıtools 'u görüntüleyemez, ekleyemez veya güncelleştiremezsiniz

#### <a name="issue"></a>Sorun

NuGet Paket Yöneticisi DotNetCLITools’u görüntülemez ve eklemeye/güncelleştirmeye izin vermez. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>Geçici çözüm

Proje dosyanızda DotNetCLIToolReferences el ile düzenlenmelidir.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>Hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir

#### <a name="issue"></a>Sorun

Visual Studio’da hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir. Bu durum, paket yöneticisi biçimi olarak PackageReferences kullandığınızda ortaya çıkar. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Geçici çözüm

El ile geri yükleme yapın.

## <a name="issues-fixed-in-nuget-43-rtm-timeframe"></a>NuGet 4,3 RTM zaman diliminde düzeltilen sorunlar

[Nuget 4,0 RTM sürüm notları](../release-notes/nuget-4.0-RTM.md) -NUGET 4,0 RTM için düzeltilen tüm sorunları listeler

### <a name="features"></a>Özellikler

- NuGet geri yükleme performansını iyileştirme-komut satırı geri yüklemeleri ve VS- [#5080](https://github.com/NuGet/Home/issues/5080) için daha akıllı noop uygulayın

- NET Core 2,0: VS/DotNet CLı var olan NuGet işlevlerini kullanmaya başlamalıdır: geri dönüş klasörleri- [#4939](https://github.com/NuGet/Home/issues/4939)

- NET Core 2,0: kullanıcıların belirli geri yükleme uyarılarını yok saymasını sağlama (veya hataya yükseltme)- [#4898](https://github.com/NuGet/Home/issues/4898)

- NET Core 2,0: CLı yerelleştirilmiş derlemeler- [#4896](https://github.com/NuGet/Home/issues/4896)

- NET Core 2,0: varlıklar dosyasına tüm uyarıları/hataları Kaydet (PackageTargetFallback dahil)- [#4895](https://github.com/NuGet/Home/issues/4895)

- TFı desteğini etkinleştir: NetStandard 2.0, Tizen- [#4892](https://github.com/NuGet/Home/issues/4892)

- NuGet. Core ve NuGet. Client projelerinin (ve bu nedenle dll 'Ler) sayısını azaltın- [#2446](https://github.com/NuGet/Home/issues/2446)

- NuGet uyarılarını hata olarak işaretleme özelliği ekleyin- [#2395](https://github.com/NuGet/Home/issues/2395)

### <a name="bugs"></a>Hatalar

- MSBuild/t: paket "DevelopmentDependency" parametresi ile başarısız olur "Pacgörevinin SK" görevi- [#5584](https://github.com/NuGet/Home/issues/5584)

- PackagePath- [#4795](https://github.com/NuGet/Home/issues/4795) sonunda Windows dizin ayırıcı EKİF ise düzleştirilmiş içerik dosyaları için dizin yapısı

- netcore projeleri, [#4694](https://github.com/NuGet/Home/issues/4694) developmentDependency olarak ayarlamayı desteklemiyor.

- RestoreManagerPackage, engellenen UI iş parçacığı ve kilitlenen VS- [#4679](https://github.com/NuGet/Home/issues/4679) zaman uyumlu olarak yüklendi

- dotnet
  - dotnetcore geri yükleme (& bu nedenle MSBuild/t: restore) açık bir çözüm proje bağımlılığı olan projeleri atlar [#4578](https://github.com/NuGet/Home/issues/4578)

- Çözümünüz farklı bir büyük harfe sahip aynı projeye başvuruda bulunan başvuruları 'a sahipse, geri yükleme çalışmayabilir. Bu, büyük/küçük harf farklılığı olmadan farklı göreli yolları da etkiler [#4574](https://github.com/NuGet/Home/issues/4574)

- NuGet paketlerinden geri yüklenen yürütülebilir dosyalar artık .NET Core 2,0 ile yürütülebilir değildir [#4424](https://github.com/NuGet/Home/issues/4424)

- NuGet.exe SWA, çözüm dosyası ayrıştırılırken özel durumun ayrıntılarına izin veriyor- [#4411](https://github.com/NuGet/Home/issues/4411)

- ContentTargetFolders, Windows 'de '/' ile biten bir yol içeriyorsa, paket içerik dosyalarını yanlış konuma koyar. [#4407](https://github.com/NuGet/Home/issues/4407)

- Netcoreapp 1.1 'i hedefleyen bir Araçlar paketi için Dotnetclientoolreference geri yüklenemiyor- [#4396](https://github.com/NuGet/Home/issues/4396)

- NuGet güncelleştirme CLı, proje dosyasında (C++) eski paket sürümü koşulunu bırakır- [#2449](https://github.com/NuGet/Home/issues/2449)

### <a name="dcrs"></a>DCR

- CPS nouç- [#5397](https://github.com/NuGet/Home/issues/5397) DotnetCliToolTargetFramework 'ü okuyun

- TPMinV Check, PJ stili UWP- [#4763](https://github.com/NuGet/Home/issues/4763) için çalışmalıdır

- Oto başvurulan paketler için Kullanıcı arabirimi açıklamasını iyileştirme- [#4471](https://github.com/NuGet/Home/issues/4471)

- NuGet geri yükleme, çalışma zamanı 'ndan varlıkları derle bölümünde seçiliyor. - [#4207](https://github.com/NuGet/Home/issues/4207)

- Kilit dosyasına bağımlılık tanılamayı yerleştir- [#1599](https://github.com/NuGet/Home/issues/1599)

## <a name="links-to-github-issues-fixed-in-43-rtm"></a>4,3 RTM 'de düzeltilen GitHub sorunlarına yönelik bağlantılar

[Sorun listesi](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")
