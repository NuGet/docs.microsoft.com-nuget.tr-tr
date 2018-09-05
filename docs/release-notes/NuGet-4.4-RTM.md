---
title: NuGet 4.4 RTM sürüm notları
description: NuGet bilinen sorunları, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr 4.3 RTM için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 9ea11ad5476b02940b171fdc69ac0bf56598418d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548420"
---
# <a name="nuget-44-rtm-release-notes"></a>NuGet 4.4 RTM sürüm notları

[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) 4.4 NuGet RTM ile birlikte gelir.

## <a name="known-issues"></a>Bilinen sorunlar

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>.NET Framework ve NuGet ile .NET Standard 2.0 ile ilgili sorunlar 

.NET standard ve kendi araçlar .NET Framework 4.6.1'i hedefleyen projeleri NuGet paketlerini & .NET Standard 2.0 veya önceki bir sürümünü hedefleyen projelerin tüketebileceği olacak şekilde tasarlanmıştır. [Bu belgede](https://github.com/dotnet/standard/issues/481) bu senaryo, bunları ve geçici çözümler günümüzün araçları durumuyla dağıtabileceğiniz çözmeye yönelik plan etrafında sorunları özetler.

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

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a>.NET Core projesinde geçersiz imzalı bir derleme içeren bir paket, sonsuz bir geri yükleme döngüsünü tetikleyebiliyor

#### <a name="issue"></a>Sorun

Bazen, geçersiz imzalı veya paket sürümü 'DateTime' değeriyle ayarlandığında bir derlemeyi içeren bir paket kullandığınızda, paket otomatik-sonsuz bir döngüde (dotnet/project-system #1457) çalıştırmak geri neden olur.

#### <a name="workaround"></a>Geçici Çözüm

Şu anda bu sorunun geçici çözümü yoktur.

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a>4.4 NuGet RTM zaman çerçevesinde giderilen sorunlar

[NuGet 4.3 RTM sürüm notları](../release-notes/nuget-4.3-RTM.md) -4.3 NuGet RTM için sabit tüm sorunları listeler

### <a name="features"></a>Özellikler

- Basit çözüm yükü desteği senaryolarda - PMC ve NuGet PM UI [#5180](https://github.com/NuGet/Home/issues/5180)

- Msbuild paketi hedef kendisini önce-çalışan kullanıcı hedefleri için ortak bir kancası olmalıdır [#5143](https://github.com/NuGet/Home/issues/5143)

- Özellik: nuget yüklemesi için - dependencyVersion anahtar ekleme [#1806](https://github.com/NuGet/Home/issues/1806)

- uap10.0.TODO.0 .NET Standard 2.0 NuGet için - harita [#5684](https://github.com/NuGet/Home/issues/5684)

- Msbuild/t: Restore ile - Visual Studio derleme araçları SKU'nun Destek [#5562](https://github.com/NuGet/Home/issues/5562)

- .NET Standard 2.0 gerekli ancak yüklenmeyen - .NET 4.6.1 desteği, geri yükleme sırasında bir hata oluşturur. [#5325](https://github.com/NuGet/Home/issues/5325)

- Paket kimliği ön eki ayırma istemci kullanıcı Arabirimi - [#5572](https://github.com/NuGet/Home/issues/5572)

- yerelleştirilmiş nuget bileşenlerini dotnet.exe yerelleştirme - desteklemek için teslim [#4336](https://github.com/NuGet/Home/issues/4336)

### <a name="bugs"></a>Hatalar

- Farklı proje yolu büyük, geri yükleme - PackageReferences kaybetmesine neden olabilir [#5855](https://github.com/NuGet/Home/issues/5855)

- Hata aralığı - uyarı numaralarını hata kodlarıyla taşıma [#5824](https://github.com/NuGet/Home/issues/5824)

- .NET Standard sürümünü hedef çerçeve ile - uyumlu olacak şekilde bilinmiyor, hata yanıltıcı [#5818](https://github.com/NuGet/Home/issues/5818)

- Test dosyaları kafa karıştırıcı lisansların - [#5776](https://github.com/NuGet/Home/issues/5776)

- Şablonlar - EndToEnd eksik lisans üstbilgilerinde test [#5774](https://github.com/NuGet/Home/issues/5774)

- Packages.config geri yükleme - NU1000 hatalar gösterir [#5743](https://github.com/NuGet/Home/issues/5743)

- nuget.exe yüklemesi üzerinde mono - DisableParallelProcessing olmalıdır [#5741](https://github.com/NuGet/Home/issues/5741)

- nuget.exe yüklemesi hatalı devre dışı bırakır önbelleğe alma - [#5737](https://github.com/NuGet/Home/issues/5737)

- Yanlış ileti - geri yükleme devre dışı bırakıldığında packages.config görüntüler için restore komutu çalıştıran VS [#5718](https://github.com/NuGet/Home/issues/5718)

- VS; Geri yükleme devre dışı bırakıldığında geri yükleme komutu çalıştırılarak - kafa karıştırıcı bir ileti görüntüler [#5659](https://github.com/NuGet/Home/issues/5659)

- Başarısız GetRestoreDotnetCliToolsTask sürümü meta veriler eksik - [#5716](https://github.com/NuGet/Home/issues/5716)

- DotNet
  - dotnetcore ekleme paket bir csproj - boş satırları temizleyerek [#5697](https://github.com/NuGet/Home/issues/5697)

- Kimlik bilgileri ayarları NuGet.Config içinde kaynak adlarını büyük küçük harfe duyarlıdır - [#5695](https://github.com/NuGet/Home/issues/5695)

- Silinmiş paketler - tüm geçmişim GeneratePackageOnBuild etkinleştirme [#5676](https://github.com/NuGet/Home/issues/5676)

- Geri yükleme mono.cecil veya semver paketleri geri yüklemez, ancak diğer tüm paketleri geri. - [#5649](https://github.com/NuGet/Home/issues/5649)

- Hataları ve Uyarıları - hatalı hata bir kaynak zaman içinde kullanılamaz.  - [#5644](https://github.com/NuGet/Home/issues/5644)

- [DesignConsistency] Şu anda NuGet yüklemesi durum metni koyu tema doğru görünmüyor. - [#5642](https://github.com/NuGet/Home/issues/5642)

- Güncelleştirme paketleri, çözüm güncelleştirmeleri/yükler için tüm projeleri için - [#5508](https://github.com/NuGet/Home/issues/5508)

- DotNet
  - dotnetcore paketi TargetFramework vs TargetFrameworks - bağlı olarak farklı şekilde davranan [#5281](https://github.com/NuGet/Home/issues/5281)

- DLL Araçlar klasörü throw uyarıları - dahil [#5020](https://github.com/NuGet/Home/issues/5020)

- NuGet.ContentModel - dize işlemleri için çok fazla bellek tüketir [#4714](https://github.com/NuGet/Home/issues/4714)

- RuntimeEnvironmentHelper.IsLinux true döndürürse OSX için - [#4648](https://github.com/NuGet/Home/issues/4648)

- 'dotnet paketi' obj obj\Debug - yerine altında nuspec koyar [#4644](https://github.com/NuGet/Home/issues/4644)

- Nuget paket yükseltmesi - çok yavaş [#4534](https://github.com/NuGet/Home/issues/4534)

- Geri yükleme işlemi (Basit çözüm geri yükleme) - LSL üzerinde açık henüz büyük çözümleri ile eşitlenmemiş CPS [#4307](https://github.com/NuGet/Home/issues/4307)

- 2.0 - SemVer nuget paketi ile sağlanan sürüm meta verileri (3.5.0-rtm-1938) - yoksayar [#3643](https://github.com/NuGet/Home/issues/3643)

- Nuget.exe (3. +), sürüm numarasıyla paketini yükleyin ve ExcludeVersion bayrağı olmayan güncelleştirme paketinin daha yeni bir sürüme - [#2405](https://github.com/NuGet/Home/issues/2405)

- Project.JSON geri yükleme üst düzey paketleri kısıtlamaları - ihlal olduğunda uyar [#2358](https://github.com/NuGet/Home/issues/2358)

- -ConfigFile ayarlamıyor özel yapılandırma yükleme komutunda - [#1646](https://github.com/NuGet/Home/issues/1646)

- nuget.exe yüklemesi değil dikkate '-DisableParallelProcessing' anahtarı - [#1556](https://github.com/NuGet/Home/issues/1556)

- Hala DotNet.exe veya msbuild.exe - tarafından kullanılan kaynakları devre dışı [#5704](https://github.com/NuGet/Home/issues/5704)

- LSL senaryoda - askıda düzeltme [#5685](https://github.com/NuGet/Home/issues/5685)

### <a name="dcrs"></a>Dcr

- nuget.exe TargetFramework desteği - yükleme [#5736](https://github.com/NuGet/Home/issues/5736)

- Farklı bir msbuild görevi UserAgent dizeleri (netcore vs Masaüstü msbuild) - ekleme [#5709](https://github.com/NuGet/Home/issues/5709)

- PackagePathResolver.GetPackageDirectoryName sanal - [#5700](https://github.com/NuGet/Home/issues/5700)

- [DesignConsistency] Bir NuGet paketi - eklerken ileti kafa karıştırıcı [#5641](https://github.com/NuGet/Home/issues/5641)

- [Uyarılar ve hatalar] NoWarn akan geçişli P2P başvuruları - [#5501](https://github.com/NuGet/Home/issues/5501)

- Basit çözüm yükü: Ortak çekirdek PM Kullanıcı Arabirimi, PMC ve Iv'lerin-- [#5057](https://github.com/NuGet/Home/issues/5057)

- Basit çözüm yükü: Desteği - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)

- İçin destek ekleyerek Visual Studio tetikler - MSBuild hedefi önceden geri [#4781](https://github.com/NuGet/Home/issues/4781)

- Ortak bir hedef BeforeTargets kullanılarak başvurulabilen NuGet.targets Ekle- [#4634](https://github.com/NuGet/Home/issues/4634)

- Paketi hedef oluşturamıyor contentFiles yapı eylemleri ile doğru şekilde - [#4166](https://github.com/NuGet/Home/issues/4166)

- İş parçacığı havuzu iş parçacıkları - RestoreOperationLogger.Do engeller [#5663](https://github.com/NuGet/Home/issues/5663)

### <a name="docs"></a>Docs

- Docs yüklenmesi için komut bayrakları DependencyVersion ve Framework - [#5858](https://github.com/NuGet/Home/issues/5858)

- Güncelleştirme için NuGet uyarı ve hataları - docs [#5857](https://github.com/NuGet/Home/issues/5857)

## <a name="links-to-github-issues-fixed-in-44-rtm"></a>GitHub sorunları 4.4 RTM'de sabit bağlantılar

[1 sorunları listeler](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[2 sorunları listeler](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[3 sorunları listeler](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
