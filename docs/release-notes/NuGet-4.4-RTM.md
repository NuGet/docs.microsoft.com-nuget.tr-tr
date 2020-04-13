---
title: NuGet 4.4 RTM Yayın Notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve DCR'ler dahil olmak üzere NuGet 4.3 RTM için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 3be24a86cc92c4e6d07fcae1dc625a150f28d7b4
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64498694"
---
# <a name="nuget-44-release-notes"></a>NuGet 4.4 Yayın Notları

[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) NuGet 4.4 RTM ile birlikte geliyor.

## <a name="summary-whats-new-in-440"></a>Özeti: 4.4.0 Yenilikler

## <a name="summary-whats-new-in-442"></a>Özeti: 4.4.2 Yenilikler

* Güvenlik Düzeltmesi: ~/.nuget içinde oluşturulan dosyalardaki izinler [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757) [#7673](https://github.com/NuGet/Home/issues/7673) çok açıktır

## <a name="summary-whats-new-in-443"></a>Özeti: 4.4.3 Yenilikler

* Güvenlik Düzeltmesi: NUPKG'lerin içindeki [dosyalar,](https://github.com/NuGet/Home/issues/7906) NUPKG dizininin üzerinde göreli bir yola sahip olabilir #7906

## <a name="known-issues"></a>Bilinen sorunlar

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>.NET Framework & NuGet ile .NET Standard 2.0 ile ilgili sorunlar 

.NET Standard & .NET Framework 4.6.1'i hedefleyen projeler ,NET Standard 2.0 veya daha önce hedefleyen NuGet paketlerini & projeleri tüketebilecek şekilde tasarlanmıştır. [Bu belge,](https://github.com/dotnet/standard/issues/481) bu senaryonun etrafındaki sorunları, bunları ele alma planını ve araç lamanın bugünkü durumuyla dağıtabileceğiniz geçici geçici işleri özetler.

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

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a>.NET Core projesinde geçersiz imzalı bir derleme içeren bir paket, sonsuz bir geri yükleme döngüsünü tetikleyebiliyor

#### <a name="issue"></a>Sorun

Bazen, geçersiz imzalı bütünleştirilmiş kod içeren bir paket kullandığınızda veya paket sürümü 'DateTime' değeriyle ayarlandığında, bu durum paket otomatik geri yüklemesinin sonsuz döngüde çalışmasına neden oluyor (dotnet/project-system#1457).

#### <a name="workaround"></a>Geçici çözüm

Şu anda bu sorunun geçici çözümü yoktur.

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a>NuGet 4.4 RTM zaman diliminde düzeltilen sorunlar

[NuGet 4.3 RTM Yayın Notları](../release-notes/nuget-4.3-RTM.md) - NuGet 4.3 RTM için düzeltilen tüm sorunları listeler

### <a name="features"></a>Özellikler

- PMC ve NuGet PM UI senaryolarında Hafif Çözüm Yükü Desteği - [#5180](https://github.com/NuGet/Home/issues/5180)

- msbuild paketi hedef kendisinden önce kullanıcı hedefleri çalıştırmak için bir kamu kanca olmalıdır - [#5143](https://github.com/NuGet/Home/issues/5143)

- Özellik: Nuget yüklemeye bağımlılıkeklemeSürümü anahtarı - [#1806](https://github.com/NuGet/Home/issues/1806)

- uap10.0.TODO.0 NuGet için .NET Standart 2.0 haritası - [#5684](https://github.com/NuGet/Home/issues/5684)

- Destek Visual Studio Build Tools SKU ile msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)

- Geri yükleme sırasında .NET Standart 2.0 için .NET 4.6.1 desteği gerekiyorsa ancak yüklü değilse hata oluşturma - [#5325](https://github.com/NuGet/Home/issues/5325)

- Paket Kimlik öneki rezervasyon istemcisi UI - [#5572](https://github.com/NuGet/Home/issues/5572)

- dotnet.exe yerelleştirmeyi desteklemek için yerelleştirilmiş nuget bileşenleri sunmak - [#4336](https://github.com/NuGet/Home/issues/4336)

### <a name="bugs"></a>Hatalar

- Farklı proje yolu kovanları PackageReferences kaybetmek geri yükleme neden olabilir - [#5855](https://github.com/NuGet/Home/issues/5855)

- Uyarı numaraları yla hata kodlarını hata aralığına taşıma - [#5824](https://github.com/NuGet/Home/issues/5824)

- .NET Standart sürümünün hedef çerçeveyle uyumlu olduğu bilinmediğinde yanıltıcı hata - [#5818](https://github.com/NuGet/Home/issues/5818)

- Kafa karıştırıcı lisansları olan test dosyaları - [#5776](https://github.com/NuGet/Home/issues/5776)

- EndToEnd test şablonlarında eksik lisans başlıkları - [#5774](https://github.com/NuGet/Home/issues/5774)

- packages.config geri yükleme NU1000 olarak hataları gösterir - [#5743](https://github.com/NuGet/Home/issues/5743)

- nuget.exe yüklemek mono üzerinde DisableParallelProcessing olmalıdır - [#5741](https://github.com/NuGet/Home/issues/5741)

- nuget.exe yüklemek yanlış önbelleğe alma devre dışı - [#5737](https://github.com/NuGet/Home/issues/5737)

- VS Geri Yükleme devre dışı bırakıldığında packages.config için geri yükleme komutunu çalıştırma yanlış ileti görüntüler - [#5718](https://github.com/NuGet/Home/issues/5718)

- VS; Geri Yükleme devre dışı bırakıldığında geri yükleme komutunu çalıştırma kafa karıştırıcı bir ileti görüntüler - [#5659](https://github.com/NuGet/Home/issues/5659)

- GetRestoreDotnetCliToolsTask sürüm meta veri eksik başarısız olur - [#5716](https://github.com/NuGet/Home/issues/5716)

- dotnet
  - dotnetcore paketi eklemek bir csproj boş satırları temizleyebilirsiniz - [#5697](https://github.com/NuGet/Home/issues/5697)

- NuGet.Config'deki kimlik bilgisi ayarlarının kaynak adları büyük/küçük harf duyarlıdır - [#5695](https://github.com/NuGet/Home/issues/5695)

- Enableing GeneratePackageOnBuild tüm paket geçmişimi sildi - [#5676](https://github.com/NuGet/Home/issues/5676)

- Geri yükleme mono.cecil veya semver paketleri geri olmaz, ancak diğer tüm paketler geri olsun. - [#5649](https://github.com/NuGet/Home/issues/5649)

- Hatalar ve Uyarılar - bir kaynak kullanılamıyorsa hatalı hata.  - [#5644](https://github.com/NuGet/Home/issues/5644)

- [DesignTutarlılık] NuGet Yükleme durum metni şu anda karanlık tema üzerinde doğru görünmüyor. - [#5642](https://github.com/NuGet/Home/issues/5642)

- Tüm projeler için çözüm güncellemelerinde/yüklemelerinde paketleri güncelleştirin - [#5508](https://github.com/NuGet/Home/issues/5508)

- dotnet
  - dotnetcore paketi TargetFramework vs TargetFrameworks bağlı olarak farklı çalışır - [#5281](https://github.com/NuGet/Home/issues/5281)

- Araçlar klasörü içinde DLs dahil uyarılar atmak - [#5020](https://github.com/NuGet/Home/issues/5020)

- NuGet.ContentModel dize işlemleri için çok fazla bellek tüketir - [#4714](https://github.com/NuGet/Home/issues/4714)

- RuntimeEnvironmentHelper.IsLinux OSX için doğru döndürür - [#4648](https://github.com/NuGet/Home/issues/4648)

- 'dotnet paketi' obj\Debug yerine obj altında nuspec koyar - [#4644](https://github.com/NuGet/Home/issues/4644)

- Nuget son derece yavaş paket yükseltme - [#4534](https://github.com/NuGet/Home/issues/4534)

- CpS, LSL'yi (hafif çözüm geri yükleme) olmayan daha büyük çözümlerle Geri Yükleme ile senkronize değildir - [#4307](https://github.com/NuGet/Home/issues/4307)

- SemVer 2.0 - sağlanan sürümü ile nuget paketi meta verileri (3.5.0-rtm-1938) yok sayar - [#3643](https://github.com/NuGet/Home/issues/3643)

- Nuget.exe (3.+) Sürüm numarası ve ExcludeVersion bayrağı ile paketi yüklemek yeni sürüme paketi güncellemez - [#2405](https://github.com/NuGet/Home/issues/2405)

- Project.json geri yüklemesi, üst düzey paketler kısıtlamaları ihlal ettiğinde uyarmalıdır - [#2358](https://github.com/NuGet/Home/issues/2358)

- -ConfigFile yükleme komutu özel config ayar değil - [#1646](https://github.com/NuGet/Home/issues/1646)

- nuget.exe yüklemek '-DisableParallelProcessing' anahtarı onurlandırmaz - [#1556](https://github.com/NuGet/Home/issues/1556)

- Hala DotNet.exe veya msbuild.exe tarafından kullanılan engelli kaynakları - [#5704](https://github.com/NuGet/Home/issues/5704)

- Düzeltme LSL senaryoda asılı - [#5685](https://github.com/NuGet/Home/issues/5685)

### <a name="dcrs"></a>DCRs

- nuget.exe install TargetFramework desteği - [#5736](https://github.com/NuGet/Home/issues/5736)

- Farklı msbuild görev UserAgent dizeleri (netcore vs masaüstü msbuild) ekleyin - [#5709](https://github.com/NuGet/Home/issues/5709)

- PackagePathResolver.GetPackageDirectoryName sanal olmalıdır - [#5700](https://github.com/NuGet/Home/issues/5700)

- [DesignTutarlılık] NuGet paketi eklerken kafa karıştırıcı ileti - [#5641](https://github.com/NuGet/Home/issues/5641)

- [Uyarılar ve hatalar] NoWarn, P2P referansları aracılığıyla geçişli olarak akmaz - [#5501](https://github.com/NuGet/Home/issues/5501)

- Hafif Çözüm Yükü: PM UI, PMC ve IV'ler için ortak çekirdek- - [#5057](https://github.com/NuGet/Home/issues/5057)

- Hafif Çözüm Yükü: Destek - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)

- Visual Studio'nun tetiklediği MSBuild hedefini geri yüklemeden önce destek ekleyin - [#4781](https://github.com/NuGet/Home/issues/4781)

- Önce Hedefler kullanarak başvurulan nuget.hedeflerine ortak bir hedef ekleyin - [#4634](https://github.com/NuGet/Home/issues/4634)

- Paket hedefi, yapı eylemleri yle içerik OluşturamazDosyaları doğru bir şekilde oluşturamaz - [#4166](https://github.com/NuGet/Home/issues/4166)

- RestoreOperationLogger.Do bloklar iplik havuzu konuları - [#5663](https://github.com/NuGet/Home/issues/5663)

### <a name="docs"></a>Docs

- Yükleme komutu Bağımlılık ve Çerçeve bayrakları için Dokümanlar - [#5858](https://github.com/NuGet/Home/issues/5858)

- NuGet uyarı ve hataları yla ilgili dokümanlara güncelleme - [#5857](https://github.com/NuGet/Home/issues/5857)

## <a name="links-to-github-issues-fixed-in-44-rtm"></a>4.4 RTM'de düzeltilen GitHub sorunlarına bağlantılar

[Sorunlar Listesi 1](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[Sorunlar Listesi 2](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[Sorunlar Listesi 3](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
