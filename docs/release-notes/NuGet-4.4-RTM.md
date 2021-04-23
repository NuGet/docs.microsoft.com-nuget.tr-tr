---
title: NuGet 4,4 RTM sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 4,4 RTM için sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 980afffcd4202e019ffa87de5dccf947300a9c13
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901713"
---
# <a name="nuget-44-release-notes"></a>NuGet 4,4 sürüm notları

[Visual Studio 2017 15,4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) , NUGET 4,4 RTM ile gelir.

## <a name="summary-whats-new-in-440"></a>Özet: 4.4.0 'deki yenilikler

## <a name="summary-whats-new-in-442"></a>Özet: 4.4.2 'deki yenilikler

* Güvenlik onarımı: ~/. NuGet içinde oluşturulan dosyalardaki Izinler çok açık [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)

## <a name="summary-whats-new-in-443"></a>Özet: 4.4.3 'deki yenilikler

* Güvenlik onarımı: NUPKGs içindeki dosyaların, NUPKG dizininin üzerinde göreli bir yolu olabilir [#7906](https://github.com/NuGet/Home/issues/7906)

## <a name="known-issues"></a>Bilinen sorunlar

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>.NET Framework & NuGet ile .NET Standard 2,0 ile ilgili sorunlar 

.NET Standard & aracı .NET Framework, .NET Standard 2,0 veya önceki sürümleri hedefleyen projeler & NuGet paketlerini tüketebileceği şekilde tasarlanmıştır. [Bu belgede, bu](https://github.com/dotnet/standard/issues/481) senaryonun etrafındaki sorunlar, bunları ele almak için plan ve BT 'nin araç durumuyla birlikte dağıtabileceğiniz geçici çözümler özetlenmektedir.

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

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a>.NET Core projesinde geçersiz imzalı bir derleme içeren bir paket, sonsuz bir geri yükleme döngüsünü tetikleyebiliyor

#### <a name="issue"></a>Sorun

Bazen, geçersiz imzalı bütünleştirilmiş kod içeren bir paket kullandığınızda veya paket sürümü 'DateTime' değeriyle ayarlandığında, bu durum paket otomatik geri yüklemesinin sonsuz döngüde çalışmasına neden oluyor (dotnet/project-system#1457).

#### <a name="workaround"></a>Geçici çözüm

Şu anda bu sorunun geçici çözümü yoktur.

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a>NuGet 4,4 RTM zaman diliminde düzeltilen sorunlar

[Nuget 4,3 RTM sürüm notları](../release-notes/nuget-4.3-RTM.md) -NUGET 4,3 RTM için düzeltilen tüm sorunları listeler

### <a name="features"></a>Özellikler

- PMC ve NuGet PM Kullanıcı arabirimi senaryolarında basit çözüm yükü desteği- [#5180](https://github.com/NuGet/Home/issues/5180)

- MSBuild paketi hedefinin, Kullanıcı hedeflerini kendisinden önce çalıştırmak için ortak bir kancası olmalıdır [#5143](https://github.com/NuGet/Home/issues/5143)

- Özellik: NuGet yüklemesine dependencyVersion anahtarı ekleme- [#1806](https://github.com/NuGet/Home/issues/1806)

- uıap 10.0. TODO. 0, NuGet- [#5684](https://github.com/NuGet/Home/issues/5684) için .NET Standard 2,0 ile eşleşmelidir

- MSBuild/t: restore- [#5562](https://github.com/NuGet/Home/issues/5562) Ile Visual Studio derleme araçları SKU desteği

- Geri yükleme sırasında .NET Standard 2,0 için .NET 4.6.1 desteği gerekliyse ancak yüklü değilse bir hata oluşturun [#5325](https://github.com/NuGet/Home/issues/5325)

- Paket KIMLIĞI ön ek ayırma istemci kullanıcı arabirimi- [#5572](https://github.com/NuGet/Home/issues/5572)

- dotnet.exe yerelleştirmeyi desteklemek için yerelleştirilmiş NuGet bileşenleri sunun [#4336](https://github.com/NuGet/Home/issues/4336)

### <a name="bugs"></a>Hatalar

- Farklı proje yolu casler, geri yüklemenin Packagereferleri kaybetmesine neden olabilir [#5855](https://github.com/NuGet/Home/issues/5855)

- Hata aralığına uyarı numarası ile hata kodları taşıma- [#5824](https://github.com/NuGet/Home/issues/5824)

- .NET Standard sürümünün hedef Framework ile uyumlu olduğu bilinmediği için yanıltıcı hata [#5818](https://github.com/NuGet/Home/issues/5818)

- Dosyaları kafa karıştırıcı lisanslarla test etme- [#5776](https://github.com/NuGet/Home/issues/5776)

- EndToEnd test şablonlarında eksik lisans üstbilgileri- [#5774](https://github.com/NuGet/Home/issues/5774)

- packages.config geri yükleme hataları NU1000 olarak gösterir- [#5743](https://github.com/NuGet/Home/issues/5743)

- nuget.exe yüklemesi, mono [#5741](https://github.com/NuGet/Home/issues/5741) üzerinde DisableParallelProcessing içermelidir

- nuget.exe yüklemesi, önbelleğe almayı yanlışlıkla devre dışı bırakır- [#5737](https://github.com/NuGet/Home/issues/5737)

- Geri yükleme devre dışı olduğunda packages.config için restore komutunun çalıştırılması, yanlış ileti [#5718](https://github.com/NuGet/Home/issues/5718) görüntülüyor

- ANLARA Restore devre dışı bırakıldığında restore komutunun çalıştırılması, karışık bir ileti [#5659](https://github.com/NuGet/Home/issues/5659) görüntüler.

- GetRestoreDotnetCliToolsTask eksik sürüm meta verileri olmadığında başarısız olur [#5716](https://github.com/NuGet/Home/issues/5716)

- dotnet
  - dotnetcore ekleme paketi, bir csproj [#5697](https://github.com/NuGet/Home/issues/5697) boş satırları temizleyebilir

- NuGet.Config kimlik bilgileri ayarlarının kaynak adları büyük/küçük harfe duyarlıdır [#5695](https://github.com/NuGet/Home/issues/5695)

- GeneratePackageOnBuild etkinleştiriliyor, tüm paket geçmişimin silinmesini- [#5676](https://github.com/NuGet/Home/issues/5676)

- Restore, mono. Cecil veya semver paketlerini geri yüklemeden, ancak diğer tüm paketler geri yüklenir. - [#5649](https://github.com/NuGet/Home/issues/5649)

- Hatalar ve uyarılar-bir kaynak kullanılamadığında hatalı hata.  - [#5644](https://github.com/NuGet/Home/issues/5644)

- [Designtutarlılığı] NuGet yükleme durumu metni şu anda koyu Temada doğru görünmüyor. - [#5642](https://github.com/NuGet/Home/issues/5642)

- Tüm projeler için çözüm güncelleştirmelerinde/yüklemelerde paketleri Güncelleştir- [#5508](https://github.com/NuGet/Home/issues/5508)

- dotnet
  - dotnetcore paketi, TargetFramework vs Targetçerçeveler 'e göre farklı davranır- [#5281](https://github.com/NuGet/Home/issues/5281)

- Araçlar klasörünün içindeki dahil edilen dll 'Ler uyarı oluştur- [#5020](https://github.com/NuGet/Home/issues/5020)

- NuGet. ContentModel dize işlemleri için çok fazla bellek tüketir- [#4714](https://github.com/NuGet/Home/issues/4714)

- RuntimeEnvironmentHelper. ıslinux, OSX [#4648](https://github.com/NuGet/Home/issues/4648) için true döndürüyor

- ' DotNet Pack ', nuspec öğesini obj\Debug- [#4644](https://github.com/NuGet/Home/issues/4644) yerine obj altına koyar

- NuGet son derece yavaş paket yükseltmesi- [#4534](https://github.com/NuGet/Home/issues/4534)

- CPS, LSL (hafif çözüm geri yükleme) ile etkinleştirilmemiş daha büyük çözümlerle geri yükleme ile eşitlenmemiş. [#4307](https://github.com/NuGet/Home/issues/4307)

- SemVer 2,0-belirtilen sürüme sahip bir NuGet paketi meta verileri yoksayar (3.5.0-RTM-1938)- [#3643](https://github.com/NuGet/Home/issues/3643)

- Nuget.exe (3. +) sürüm numarası ve ExcludeVersion bayrağıyla paket yüklemesi, paketi daha yeni sürüme güncelleştirmez [#2405](https://github.com/NuGet/Home/issues/2405)

- En üst düzey paketler kısıtlamaları ihlal ediyor durumunda geri yükleme Project.jsuyarı almalıdır [#2358](https://github.com/NuGet/Home/issues/2358)

- -ConfigFile, install komutunda özel yapılandırma ayarlamadır- [#1646](https://github.com/NuGet/Home/issues/1646)

- nuget.exe yüklemesi '-DisableParallelProcessing ' anahtarını kabul etmez [#1556](https://github.com/NuGet/Home/issues/1556)

- DotNet.exe veya msbuild.exe tarafından hala kullanılan devre dışı kaynaklar [#5704](https://github.com/NuGet/Home/issues/5704)

- LSL senaryosunda onarım kilitleniyor- [#5685](https://github.com/NuGet/Home/issues/5685)

### <a name="dcrs"></a>DCR

- nuget.exe TargetFramework desteğini Install- [#5736](https://github.com/NuGet/Home/issues/5736)

- Farklı MSBuild görev UserAgent dizeleri (netcore vs Desktop MSBuild) ekleme- [#5709](https://github.com/NuGet/Home/issues/5709)

- PackagePathResolver. GetPackageDirectoryName sanal- [#5700](https://github.com/NuGet/Home/issues/5700) olmalıdır

- [Designtutarlılığı] NuGet paketi eklenirken kafa karıştırıcı iletisi- [#5641](https://github.com/NuGet/Home/issues/5641)

- [Uyarılar ve hatalar] NoWarn, P2P başvuruları aracılığıyla geçişli olarak akış yapmaz [#5501](https://github.com/NuGet/Home/issues/5501)

- Hafif çözüm yükü: PM Kullanıcı arabirimi, PMC ve IVS-- [#5057](https://github.com/NuGet/Home/issues/5057) Için ortak çekirdek

- Hafif çözüm yükü: destek-PMC- [#5053](https://github.com/NuGet/Home/issues/5053)

- Visual Studio 'Nun tetiklediği ön geri yükleme MSBuild hedefi için destek ekleme ( [#4781](https://github.com/NuGet/Home/issues/4781) )

- NuGet. targets öğesine BeforeTargets kullanılarak başvurulabilen bir genel hedef ekleyin- [#4634](https://github.com/NuGet/Home/issues/4634)

- Paket hedefi, derleme eylemleri doğru şekilde contentFiles oluşturamaz- [#4166](https://github.com/NuGet/Home/issues/4166)

- RestoreOperationLogger.Do blokları iş parçacığı havuzu iş parçacıkları- [#5663](https://github.com/NuGet/Home/issues/5663)

### <a name="docs"></a>Docs

- Install komutu DependencyVersion ve Framework bayrakları- [#5858](https://github.com/NuGet/Home/issues/5858)

- NuGet uyarıları ve hatalarıyla ilgili belgeleri güncelleştirme- [#5857](https://github.com/NuGet/Home/issues/5857)

## <a name="links-to-github-issues-fixed-in-44-rtm"></a>4,4 RTM 'de düzeltilen GitHub sorunlarına yönelik bağlantılar

[Sorun listesi 1](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[Sorun listesi 2](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[Sorun listesi 3](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
