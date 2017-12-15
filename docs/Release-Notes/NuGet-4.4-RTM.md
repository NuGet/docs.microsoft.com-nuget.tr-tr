---
title: "NuGet 4.4 RTM sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: unniravindranathan
ms.date: 08/14/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 5ffca6f6-a126-4407-b22f-1323e7dc44a3
description: "Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere NuGet 4.3 RTM için sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 4.3 RTM sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: 479f14db0b402476eccab23283a029a839cf51dd
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="44-rtm-release-notes"></a>4.4 sürüm notları RTM

[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) NuGet 4.4 RTM ile birlikte gelir.

## <a name="known-issues"></a>Bilinen sorunlar

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>.NET Framework & NuGet ile .NET standart 2.0 ile ilgili sorunları 
.NET standart & kendi araç proje .NET Framework 4.6.1 hedefleme NuGet paketlerini & Proje .NET Standard 2.0 veya önceki sürümünü hedefleme tüketebileceği şekilde tasarlanmıştır. [Bu belge](https://github.com/dotnet/standard/issues/481) sorunlarını bu senaryo, bunları ve geçici çözümler bugünün araç durumuyla dağıtabileceğiniz adresleme planı geçici özetler.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>Paket Yöneticisi Konsolu’nu kullanırken, 'Enter' tuşu çalışmayabilir

#### <a name="issue"></a>Sorun:
Bazen Paket Yöneticisi Konsolu’nda Enter tuşu çalışmıyor. Bunu görürseniz, lütfen düzeltmeye yönelik ilerlemeye göz atın ve yeniden oluşturma adımlarınız hakkında yararlı olabilecek ek bilgileri paylaşın. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Geçici çözüm:
Visual Studio’yu yeniden başlatın ve çözümü açmadan önce PMC’yi açın. Alternatif olarak, silmeyi deneyin `project.lock.json` ve yeniden geri yükleme.

### <a name="you-will-be-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Nuget Paket Yöneticisi’ni kullanarak DotNetCLITools’u görüntüleyemez, ekleyemez veya güncelleştiremezsiniz

#### <a name="issue"></a>Sorun:
NuGet Paket Yöneticisi DotNetCLITools’u görüntülemez ve eklemeye/güncelleştirmeye izin vermez. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>Geçici çözüm:
Proje dosyanızda DotNetCLIToolReferences el ile düzenlenmelidir.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>Hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir

#### <a name="issue"></a>Sorun:
Visual Studio’da hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir. Bu durum, paket yöneticisi biçimi olarak PackageReferences kullandığınızda ortaya çıkar. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Geçici çözüm:
El ile geri yükleme yapın.


### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a>.NET Core projesinde geçersiz imzalı bir derleme içeren bir paket, sonsuz bir geri yükleme döngüsünü tetikleyebiliyor

#### <a name="issue"></a>Sorun:
Bazen, bir derlemeyi imzası geçersiz olan veya paket sürümü ile 'DateTime' borsa takip ayarlandığında içeren bir paket kullandığınızda, paket otomatik-sonsuz bir döngüde (dotnet/project-sistem #1457) çalıştırmak geri yükle neden olur.

#### <a name="workaround"></a>Geçici çözüm:
Şu anda bu sorunun geçici çözümü yoktur.


## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a>4.4 NuGet RTM zaman çerçevesinde giderilen sorunlar

[NuGet 4.3 RTM sürüm notları](../release-notes/nuget-4.3-RTM.md) -NuGet 4.3 RTM için sabit tüm sorunları listeler

**Özellik:**

* Basit çözüm yük desteği senaryolarda - PMC ve NuGet PM UI [#5180](https://github.com/NuGet/Home/issues/5180)

* Msbuild paketi hedef kendisini önce-çalışan kullanıcı hedefleri için ortak bir kancası olmalıdır [#5143](https://github.com/NuGet/Home/issues/5143)

* Özelliği: nuget yüklemek için - dependencyVersion anahtar eklemek [#1806](https://github.com/NuGet/Home/issues/1806)

* uap10.0.TODO.0 .NET standart 2.0 için NuGet - eşleme [#5684](https://github.com/NuGet/Home/issues/5684)

* Msbuild /t:restore ile - Visual Studio derleme araçları SKU Destek [#5562](https://github.com/NuGet/Home/issues/5562)

* .NET standart 2.0 gerekli ancak yüklenmeyen - .NET 4.6.1 desteği olursa geri yükleme sırasında bir hata oluştur [#5325](https://github.com/NuGet/Home/issues/5325)

* Paket kimliği öneki ayırma istemci UI - [#5572](https://github.com/NuGet/Home/issues/5572)

* yerelleştirilmiş nuget bileşenleri dotnet.exe yerelleştirme - desteklemek için teslim [#4336](https://github.com/NuGet/Home/issues/4336)

**Hata:**

* Farklı proje yolu kasası geri PackageReferences - kaybetmesine neden olabilir [#5855](https://github.com/NuGet/Home/issues/5855)

* Hata kodları uyarı numaralarıyla hata aralığa - taşıma [#5824](https://github.com/NuGet/Home/issues/5824)

* .NET standart sürümü ile hedef framework - uyumlu olacak şekilde bilinmiyor olduğunda hata yanıltıcı [#5818](https://github.com/NuGet/Home/issues/5818)

* Test dosyalarını kafa karıştırıcı lisansların - [#5776](https://github.com/NuGet/Home/issues/5776)

* EndToEnd eksik lisans üstbilgilerinde test şablonları - [#5774](https://github.com/NuGet/Home/issues/5774)

* Packages.config geri yükleme hataları NU1000 - gösterir [#5743](https://github.com/NuGet/Home/issues/5743)

* nuget.exe yükleme mono üzerinde - DisableParallelProcessing olmalıdır [#5741](https://github.com/NuGet/Home/issues/5741)

* nuget.exe yükleme yanlış devre dışı bırakır önbelleğe alma - [#5737](https://github.com/NuGet/Home/issues/5737)

* Geri yükleme devre dışı bırakıldığında packages.config hatalı ileti - görüntüler için restore komutu çalıştıran VS [#5718](https://github.com/NuGet/Home/issues/5718)

* VS; Geri yükleme devre dışı bırakıldığında geri yükleme komutu çalıştırılarak görüntüler kafa karıştırıcı bir ileti - [#5659](https://github.com/NuGet/Home/issues/5659)

* GetRestoreDotnetCliToolsTask başarısız eksik sürüm meta verileri - [#5716](https://github.com/NuGet/Home/issues/5716)

* DotNet eklemek paket csproj - boş satırları temizlemek [#5697](https://github.com/NuGet/Home/issues/5697)

* NuGet.Config kimlik bilgisi ayarları kaynak adları büyük küçük harf duyarlı - [#5695](https://github.com/NuGet/Home/issues/5695)

* Silinen paketler - tüm my geçmişini GeneratePackageOnBuild etkinleştirme [#5676](https://github.com/NuGet/Home/issues/5676)

* Geri yükleme mono.cecil veya semver paket geri yüklemez, ancak diğer tüm paketler geri. - [#5649](https://github.com/NuGet/Home/issues/5649)

* Hatalar ve uyarılar - bozuk hata bir kaynak yokken kullanılamaz.  - [#5644](https://github.com/NuGet/Home/issues/5644)

* [DesignConsistency] Şu anda NuGet yükleme durumu metni koyu tema doğru görünmüyor. - [#5642](https://github.com/NuGet/Home/issues/5642)

* Güncelleştirme paketleri çözüm güncelleştirmeleri/yüklemelerinde tüm projeleri - adresindeki [#5508](https://github.com/NuGet/Home/issues/5508)

* DotNet paketi TargetFramework vs TargetFrameworks - bağlı olarak farklı şekilde davranan [#5281](https://github.com/NuGet/Home/issues/5281)

* DLL'leri içinde Araçlar klasörü throw uyarılar - dahil [#5020](https://github.com/NuGet/Home/issues/5020)

* NuGet.ContentModel dize işlemleri için-çok fazla bellek tüketir [#4714](https://github.com/NuGet/Home/issues/4714)

* RuntimeEnvironmentHelper.IsLinux döndürür true OSX için - [#4648](https://github.com/NuGet/Home/issues/4648)

* 'dotnet pack' koyar obj obj\Debug - yerine altında nuspec [#4644](https://github.com/NuGet/Home/issues/4644)

* Nuget paket yükseltme - son derece yavaş [#4534](https://github.com/NuGet/Home/issues/4534)

* Geri yükleme (Basit çözüm geri yükle) - LSL üzerinde açık henüz büyük çözümlerle ile eşitlenmemiş CPS [#4307](https://github.com/NuGet/Home/issues/4307)

* SemVer 2.0 - nuget paketi ile meta veriler (3.5.0-rtm-1938) - sürüm yoksayar sağlanan [#3643](https://github.com/NuGet/Home/issues/3643)

* Nuget.exe (3. +), sürüm numarasıyla paketini yükleyin ve ExcludeVersion bayrağı değil güncelleştirme paketinin daha yeni sürüme - [#2405](https://github.com/NuGet/Home/issues/2405)

* Project.JSON geri yükleme üst düzey paketleri kısıtlamaları - ihlal olduğunda uyar [#2358](https://github.com/NuGet/Home/issues/2358)

* -ConfigFile değil ayarı özel yapılandırma yükleme komutunda - [#1646](https://github.com/NuGet/Home/issues/1646)

* nuget.exe yükleme dikkate değil '-DisableParallelProcessing' geçiş - [#1556](https://github.com/NuGet/Home/issues/1556)

* Devre dışı hala DotNet.exe veya msbuild.exe - tarafından kullanılan kaynakları [#5704](https://github.com/NuGet/Home/issues/5704)

* Askıda LSL senaryoda - düzeltme [#5685](https://github.com/NuGet/Home/issues/5685)

**DCR:**

* nuget.exe yükleme TargetFramework desteği - [#5736](https://github.com/NuGet/Home/issues/5736)

* Farklı msbuild görev UserAgent dizeleri (netcore vs Masaüstü msbuild) - eklemek [#5709](https://github.com/NuGet/Home/issues/5709)

* PackagePathResolver.GetPackageDirectoryName sanal - [#5700](https://github.com/NuGet/Home/issues/5700)

* [DesignConsistency] Bir NuGet paketi - eklerken ileti kafa karıştırıcı [#5641](https://github.com/NuGet/Home/issues/5641)

* [Uyarı ve hataların] NoWarn akan geçişli P2P başvurular arasında - [#5501](https://github.com/NuGet/Home/issues/5501)

* Basit çözüm yük: Ortak çekirdek PM UI, PMC ve Iv'ler * - [#5057](https://github.com/NuGet/Home/issues/5057)

* Basit çözüm yük: Destek - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)

* İçin destek eklemek Visual Studio tetikler - MSBuild hedef önceden geri [#4781](https://github.com/NuGet/Home/issues/4781)

* Ortak bir hedef BeforeTargets kullanarak başvurulabilir NuGet.targets Ekle- [#4634](https://github.com/NuGet/Home/issues/4634)

* Paketi hedef oluşturamıyor Content dosyaları yapı eylemleri ile doğru - [#4166](https://github.com/NuGet/Home/issues/4166)

* RestoreOperationLogger.Do engeller iş parçacığı havuzu iş parçacıkları - [#5663](https://github.com/NuGet/Home/issues/5663)

**Belgeler:**

* Yükleme için belgeleri komut DependencyVersion ve Framework bayrakları - [#5858](https://github.com/NuGet/Home/issues/5858)

* Belgeleri NuGet uyarıları ve hataları - güncelleştirmeye [#5857](https://github.com/NuGet/Home/issues/5857)

## <a name="link-to-github-issues-fixed-in-44-rtm"></a>Düzeltilen 4,4 RTM GitHub bağlantı sorunları

[1 sorunları listeler](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[2 sorunları listeler](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[3 sorunları listeler](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
