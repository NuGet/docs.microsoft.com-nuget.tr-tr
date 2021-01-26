---
title: NuGet 4,0 RTM sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 4,0 RTM için sürüm notları.
author: anangaur
ms.author: anangaur
ms.date: 03/03/2017
ms.topic: conceptual
ms.openlocfilehash: c3ec5c20e5175edd315de20ca98c7a106c51809e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776274"
---
# <a name="nuget-40-rtm-release-notes"></a>NuGet 4,0 RTM sürüm notları

[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) , .NET Core desteği ekleyen NuGet 4,0 ile birlikte gelir, bir dizi kalite düzeltmesine sahiptir ve performansı geliştirir. Bu sürümde, PackageReference için destek, MSBuild hedefleri olarak NuGet komutları, arka plan paketi geri yüklemeleri ve daha fazlası gibi çeşitli geliştirmeler de yer alır.

## <a name="known-issues"></a>Bilinen sorunlar

### <a name="nuget-restore-may-fail-when-you-have-multiple-projects-referencing-another-project-in-a-solution"></a>Çözümdeki başka bir projeye başvuruda bulunan birden çok projeniz olduğunda NuGet geri yükleme başarısız olabilir

#### <a name="issue"></a>Sorun

Bir çözümde aynı projeye farklı büyük/küçük harf kullanımı veya farklı göreli yollarla birden çok proje başvurusu yapılıyorsa, NuGet geri yükleme çalışmayabilir. [NuGet#4574](https://github.com/NuGet/Home/issues/4574)

#### <a name="workaround"></a>Geçici çözüm

Büyük/küçük harf kullanımını veya göreli yolları düzelterek tüm proje başvurularında aynı olmalarını sağlayın.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>Paket Yöneticisi Konsolu’nu kullanırken, 'Enter' tuşu çalışmayabilir

#### <a name="issue"></a>Sorun

Bazen Paket Yöneticisi Konsolu’nda Enter tuşu çalışmıyor. Bunu görürseniz, lütfen düzeltmeye yönelik ilerlemeye göz atın ve yeniden oluşturma adımlarınız hakkında yararlı olabilecek ek bilgileri paylaşın. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Geçici çözüm

Visual Studio’yu yeniden başlatın ve çözümü açmadan önce PMC’yi açın. Alternatif olarak, ' yi silmeyi `project.lock.json` ve geri yüklemeyi yeniden deneyin.

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a>.NET Core projelerinde, geçersiz imzalı bir bütünleştirilmiş kod içeren bir paket kullandığınızda sınırsız geri yükleme döngüsüne girebilirsiniz

#### <a name="issue"></a>Sorun

Bazen, geçersiz imzalı bir bütünleştirilmiş kod içeren bir paket kullandığınızda veya paket sürümü 'DateTime' onaylayıcısıyla ayarlandığında, bu durum paket otomatik geri yüklemesinin sınırsız bir döngüde çalışmasına neden olur. [NuGet#4542](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a>Geçici çözüm

Şu anda bu sorunun geçici çözümü yoktur.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>NuGet Paket Yöneticisi 'Ni kullanarak Dotnetclıtools 'u görüntüleyemez, ekleyemez veya güncelleştiremezsiniz

#### <a name="issue"></a>Sorun

NuGet Paket Yöneticisi DotNetCLITools’u görüntülemez ve eklemeye/güncelleştirmeye izin vermez. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>Geçici çözüm

Proje dosyanızda DotNetCLIToolReferences el ile düzenlenmelidir.

### <a name="nuget-restore-will-fail-when-you-set-packageid-property-for-projects"></a>Projeler için PackageId özelliğini ayarladığınızda NuGet geri yüklemesi başarısız olur

#### <a name="issue"></a>Sorun

.NET Core projeleri için, Visual Studio’da NuGet geri yükleme projelerin PackageId özelliğini kabul etmez. [NuGet#4586](https://github.com/NuGet/Home/issues/4586)

#### <a name="workaround"></a>Geçici çözüm

Geri yükleme komutunu, komut satırını kullanarak çalıştırın.

### <a name="when-your-project-does-not-have-obj-folder-package-restore-may-fail"></a>Projenizde 'obj' klasörü olmadığında, paket geri yükleme başarısız olabilir

#### <a name="issue"></a>Sorun

'obj' klasörü silindiğinde Visual Studio PackageReferences’ı geri yükleyemez. [NuGet#4528](https://github.com/NuGet/Home/issues/4528)

#### <a name="workaround"></a>Geçici çözüm

'obj' klasörünü el ile oluşturursanız, geri yükleme çalışacaktır.

### <a name="manually-updating-packages-using-update-package-in-console-may-fail"></a>Konsolda Update-Package kullanarak paketleri el ile güncelleştirme işlemi başarısız olabilir

#### <a name="issue"></a>Sorun

Konsolda ile Update-Package kullanımı, yeni dönüştürülmüş PackageReferences projeleri için tek bir kez çalışır. [NuGet#4431](https://github.com/NuGet/Home/issues/4431)

#### <a name="workaround"></a>Geçici çözüm

Şu anda bu sorunun geçici çözümü yoktur.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>Hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir

#### <a name="issue"></a>Sorun

Visual Studio’da hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir. Bu durum, paket yöneticisi biçimi olarak PackageReferences kullandığınızda ortaya çıkar. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Geçici çözüm

El ile geri yükleme yapın.

### <a name="msbuild-trestore-fails-when-a-project-targeting-net461-references-another-project-targeting-netstandard"></a>.NET461’i hedefleyen bir proje, .NETStandard’ı hedefleyen başka bir projeye başvuruda bulunduğunda, msbuild /t:restore başarısız olur

#### <a name="issue"></a>Sorun

.NET461’i hedefleyen PackageReference tabanlı bir proje, .NETStandard’ı hedefleyen PackageReference tabanlı başka bir projeye başvuruda bulunduğunda, msbuild /t:restore başarısız olur.  [NuGet#4532](https://github.com/NuGet/Home/issues/4532)

#### <a name="workaround"></a>Geçici çözüm

Şu anda bu sorunun geçici çözümü yoktur.

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a>NuGet 4,0 RTM zaman diliminde düzeltilen sorunlar

[Nuget 4,0 RC sürüm notları](../release-notes/nuget-4.0-RC.md) -NUGET 4,0 RC için düzeltilen tüm sorunları listeler

### <a name="features"></a>Özellikler

- NuGet. Core. sln- [#2041](https://github.com/NuGet/Home/issues/2041) dizeleri yerelleştirin

- NuGet, Web uygulaması projelerini LSL modunda yüklemeye zorlar- [#4258](https://github.com/NuGet/Home/issues/4258)

- "SDK yüklü" paketlere yönelik kullanıcı arabiriminde sürüm değişikliklerini engellemek için, oto başvurulan PackageReference desteği- [#4044](https://github.com/NuGet/Home/issues/4044)

- Herhangi bir proje bağımlılığı için PackageSpec. Version doğru şekilde iletişim kurar (PackageRef)- [#3902](https://github.com/NuGet/Home/issues/3902)

- `.csproj`komut satırı (ler) e- [#4101](https://github.com/NuGet/Home/issues/4101) başvuruları kaldırma desteği

- PackageReference projeleri (normal ve xplat) ve hafif çözüm yükü- [#4003](https://github.com/NuGet/Home/issues/4003) için geri yükleme desteği

- `.csproj`komut satırı (ler) e- [#3751](https://github.com/NuGet/Home/issues/3751) başvuru ekleme desteği

- `packages.config`Veya `project.json`  -  [#3711](https://github.com/NuGet/Home/issues/3711) için hafif çözüm yükü için NuGet geri yüklemeyi destekleme

- NuGet tarafından oluşturulan hedef dosya [#3683](https://github.com/NuGet/Home/issues/3683) ContentFiles desteği

- MSBuild- [#3646](https://github.com/NuGet/Home/issues/3646) kullanarak Mac 'te nuget.exe doğrulaması IÇIN mono CI oluşturma

- NuGet 'i v2 NuGet. Core bağımlılıklarından Taşı- [#3645](https://github.com/NuGet/Home/issues/3645)

### <a name="bugs"></a>Hatalar

- Visual Studio 'da NuGet geri yükleme projelerin PackageID özelliğine uymuyor- [#4586](https://github.com/NuGet/Home/issues/4586)

- VSIX paketine paket eklenirken NuGet ProjectSystemCache hatası- [#4545](https://github.com/NuGet/Home/issues/4545)

- Includesource birden çok TFMs içeren bir projede kullanılıyorsa, paket özel durum oluşturur [#4536](https://github.com/NuGet/Home/issues/4536)

- VS 2017 RC3, çözüm genelinde paket yönetimi 'nden güncelleştirme kullanma ile kilitleniyor- [#4474](https://github.com/NuGet/Home/issues/4474)

- Yeni yüklenen paket [#4435](https://github.com/NuGet/Home/issues/4435) kaldırılamıyor

- PackageRef 'e geçiş yaparken, karma çözümlerin garip geri yükleme davranışı vardır- [#4433](https://github.com/NuGet/Home/issues/4433)

- NuGet işlemini başlattıktan hemen sonra oluşturma (yükleme, güncelleştirme, geri yükleme), askıda kalmasına neden olabilir [#4420](https://github.com/NuGet/Home/issues/4420)

- UI askıda-kilitlenme NuGet. SolutionRestoreManager. RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371) başlatılıyor

- Add Package komutu, element- [#4325](https://github.com/NuGet/Home/issues/4325) yerine Attribute olarak eklenmelidir

- dotnet
  - dotnetcore geri yükleme foo. sln--SLN içindeki yapılandırma, restore Graph 'te yinelenen (ancak fark yapılandırması) projelere neden olduğunda başarısız olur- [#4316](https://github.com/NuGet/Home/issues/4316)

- Yalnızca içerik paketleri- [#3668](https://github.com/NuGet/Home/issues/3668)

- Varsayılan olarak, paket biçimi seçici seçeneğini devre dışı bırak- [#4468](https://github.com/NuGet/Home/issues/4468)

- Perf: CreateUAP_CSharp_VS. 01.1.3.153,570 MS (149,1%) tarafından proje gerilediğini Duration_TotalElapsedTime oluşturun. Taban çizgisi 26129,02- [#4452](https://github.com/NuGet/Home/issues/4452)

- Perf: ManagedLangs_CS_DDRIT .0300. yeniden derleme çözümü Duration_TotalElapsedTime 1.5 sn tarafından yeniden derleyin. Taban çizgisi 26105- [#4441](https://github.com/NuGet/Home/issues/4441)

- Birden çok TFA projesinde aday başarısız oldu- [#4419](https://github.com/NuGet/Home/issues/4419)

- Perf: WebForms_DDRIT .1200. Close çözüm gerilediğini VM_ImagesInMemory_Total_devenv 3,000 sayı (0,5%). Taban çizgisi 26123,04- [#4408](https://github.com/NuGet/Home/issues/4408)

- vsfeedback-netcoreapp 1.1 'i hedeflerken paket uyarıları- [#4397](https://github.com/NuGet/Home/issues/4397)

- Boş ASP.NET Core Web uygulamasına bir NuGet paketi eklenmeye çalışılırken PathTooLongException- [#4391](https://github.com/NuGet/Home/issues/4391)

- Paket çok sık çalışır--DotNet
  - dotnetcore paketi, target "Pack" ile ilgili hedef bağımlılık grafiğinde döngüsel bağımlılık olduğundan başarısız oluyor [#4381](https://github.com/NuGet/Home/issues/4381)

- Paket çok sık çalışır--NuGet paketi oluşturma tüm konfigürasyonları içermez- [#4380](https://github.com/NuGet/Home/issues/4380)

- C++ projesinde packageref ile NuGet ekleme- [#4378](https://github.com/NuGet/Home/issues/4378)

- Erişilebilirlik: ekran okuyucusu, paketi [#4366](https://github.com/NuGet/Home/issues/4366) paketi yükleyecek projeleri seçme onay kutusunu göstermez

- NuGet VS17 sporadsoysal, VSO/VSTS akışlarına bağlanma başarısız oluyor-VS hatası 365798- [#4365](https://github.com/NuGet/Home/issues/4365)

- PackagePath yolu "contentFiles" olarak belirtiyorsa contentFiles yanlış konuma çıkış alır- [#4348](https://github.com/NuGet/Home/issues/4348)

- Paket hedefi bir PackageVersion özelliğini VersionSuffix ile ekler- [#4324](https://github.com/NuGet/Home/issues/4324)

- Paket yolunun belirtilmesi DotNet Pack ile çalışmıyor- [#4321](https://github.com/NuGet/Home/issues/4321)

- NuGet geri yükleme sırasında yinelenen içeri aktarmalar hakkında bir uyarı verir- [#4304](https://github.com/NuGet/Home/issues/4304)

- "NuGet Paket Yöneticisi biçimi" iletişim kutusu Koyu tema altında hatalı görünüyor- [#4300](https://github.com/NuGet/Home/issues/4300)

- Derleme geri yükleme sırasında VS kilitlenmesi- [#4298](https://github.com/NuGet/Home/issues/4298)

- TargetFramework 'e tfd eklerseniz, bu durumda Visual Studio kilitlenmeleri, kaydedebilir ve derdir. %10 zaman [#4295](https://github.com/NuGet/Home/issues/4295)

- NuGet paketi bir projeyi başarıyla paketleme sırasında başarı iletisini çıktı değil- [#4294](https://github.com/NuGet/Home/issues/4294)

- System. ıO. Compression 4,1 bulunamadığı için Pacbir SK başarısız oldu- [#4290](https://github.com/NuGet/Home/issues/4290)

- Paket çok sık çalışır; dosya erişimi çakışmasıyla birlikte Packısk sık başarısız olur- [#4289](https://github.com/NuGet/Home/issues/4289)

- NuGet arka plan geri yükleme sırasında çıkış penceresini açar- [#4274](https://github.com/NuGet/Home/issues/4274)

- ServiceProvider tehlikeli kodlama düzeniyle (askıda kalmasına neden olabilir) kaldırın [#4268](https://github.com/NuGet/Home/issues/4268)

- Perf/Uıaskıda-#4266 DownloadTimeoutStream okumaları- [](https://github.com/NuGet/Home/issues/4266)

- NuGet geri yükleme işlemi tamamlanmadan önce bir projeyi kapatmaya çalışırsanız, Visual Studio kilitlenmeler- [#4257](https://github.com/NuGet/Home/issues/4257)

- Pacbir SK ve paketleme `.nuspec`  -  [#4250](https://github.com/NuGet/Home/issues/4250) sorunları

- [vsfeedback] Yeni projedeki NuGet paketleri çözümlenemiyor (Visual Studio 'nun yeniden başlatılması gerekiyor)- [#4217](https://github.com/NuGet/Home/issues/4217)

- [vsfeedback] Kullanılabilir paket sürümlerini gösteren "sürüm" açılan penceresinde, seçili nuGet paketiyle eşitlenmiş halde kalmak için bir sorun var...- [#4198](https://github.com/NuGet/Home/issues/4198)

- NuGet. Client, [#4185](https://github.com/NuGet/Home/issues/4185) kilitlenmeleri engellemek için CPS ile etkileşerek CPS JoinableTaskFactory kullanmalıdır

- NuGet 3.5.0 paketten paketten `.targets` açma- [#4171](https://github.com/NuGet/Home/issues/4171)

- dotnet
  - dotnetcore paketi `.csproj`  -  [#4150](https://github.com/NuGet/Home/issues/4150) başlığını desteklemiyor

- VS2017 RC 'de hata iletişim kutusunda Install-Package sonuçları [#4127](https://github.com/NuGet/Home/issues/4127)

- .NET Core projesi için bir paketi güncelleştirme, Kullanıcı arabirimi aday 'dan CPS güncelleştirmesini almamasına yönelik olarak görünür. - [#4035](https://github.com/NuGet/Home/issues/4035)

- Çözümlenmemiş başvuruyu İyileştirme Uyarısı- [#3955](https://github.com/NuGet/Home/issues/3955)

- dotnet
  - dotnetcore paketi-ProjectReference sürüm bilgilerini kaybeder- [#3953](https://github.com/NuGet/Home/issues/3953)

- UWP uygulaması oluşturma proje oluşturma & toplam geçen süre gerilemesi- [#3873](https://github.com/NuGet/Home/issues/3873)

- Geri yükleme sırasında hata sonrasında bile başarılı geri yükleme iletisi görüntülenir. - [#3799](https://github.com/NuGet/Home/issues/3799)

- NuGet. CommandLine 3.4.4 to Nuget.org- [#2931](https://github.com/NuGet/Home/issues/2931) yeniden yayımlayın

- Geçiş sırasında projeler `project.json` `.csproj` ---geri yükleme başarısız olur- [#4297](https://github.com/NuGet/Home/issues/4297)

- Yeni oluşturulan xUnit Test projesinde geri yükleme başarısız oldu- [#4296](https://github.com/NuGet/Home/issues/4296)

- Temel projeler askıda kalabilir, açık [#4269](https://github.com/NuGet/Home/issues/4269) Kullanıcı arabirimini kilitleyebilir

- derleme görevleri için hedef dosyasını düzeltir- [#4267](https://github.com/NuGet/Home/issues/4267)

- Hata listesi, başvurulan projeyi kaldırmak için derleme çözümünü tamamladıktan sonra hata oluştu- [#4208](https://github.com/NuGet/Home/issues/4208)

- MSB4057: "_GenerateRestoreGraphProjectEntry" hedefi projede yok. - [#4194](https://github.com/NuGet/Home/issues/4194)

- vsfeedback: tüm projeler ' i seçtiğinizde çözüm kilitlenmeleri için NuGet Yöneticisi Kullanıcı arabirimi- [#4191](https://github.com/NuGet/Home/issues/4191)

- Sondaki eğik çizgi olduğunda MSBuildPath nuget.exe başarısız olur [#4180](https://github.com/NuGet/Home/issues/4180)

- vsfeedback: NuGet geri yüklemesi, LinqToTwitter projesi için çeşitli proje başvurusu uyarıları sağlar- [#4156](https://github.com/NuGet/Home/issues/4156)

- Paketi `.csproj` , minClientVersion özniteliğini içermez- [#4135](https://github.com/NuGet/Home/issues/4135)

- VS2017 içinde oturum açılan NuGet.Build.Tasks.Pack.dll gönderilen gecikme (d15rel 26014,00)- [#4122](https://github.com/NuGet/Home/issues/4122)

- VSFeedback: CMake 3.7.1 ile oluşturulan VS 2015 projesinde geri yükleme başarısız oluyor [#4114](https://github.com/NuGet/Home/issues/4114)

- VSFeedback: geri yükleme hataları, derleme [#4113](https://github.com/NuGet/Home/issues/4113) verebilmesi için daha fazla tam hata iletisi içerebilir

- [VSFeedback] Web sitesi projesi için NuGet paketleri geri yüklenirken hata oluştu: değer null olamaz. - [#4092](https://github.com/NuGet/Home/issues/4092)

- Geçiş, NuGet. PackageManagement. VisualStudio. SolutionRestoreWorker- [#4067](https://github.com/NuGet/Home/issues/4067) Içinde "nesne başvurusu özel durumu" oluşturur

- dotnet
  - dotnetcore Pack, paketin [#4063](https://github.com/NuGet/Home/issues/4063) karşı derlenme sürümlerine sahip araçları paketlemelidir.

- Yeni arka plan geri yükleme, geri yükleme için saniye sürerse süreyi durum çubuğuna yazar- [#4036](https://github.com/NuGet/Home/issues/4036)

- Typo on, tüm proje başvurularını çözümleyemedi- [#4018](https://github.com/NuGet/Home/issues/4018)

- Paket başvuru senaryolarında PCM iş akışlarını Etkinleştir- [#4016](https://github.com/NuGet/Home/issues/4016)

- Paket Yöneticisi Kullanıcı arabiriminde yüklü paketler bulunamıyor- [#4015](https://github.com/NuGet/Home/issues/4015)

- dotnet
  - PackagePath boş olduğunda dotnetcore paketi başarısız olur- [#3993](https://github.com/NuGet/Home/issues/3993)

- Birden çok Kullanıcı senaryosunda geri yükleme görevi başarısız oluyor- [#3897](https://github.com/NuGet/Home/issues/3897)

- NuGet paketi kullanılırken Içerik türü değiştirilemez- [#3895](https://github.com/NuGet/Home/issues/3895)

- MsBuild/t: Pack- [#3894](https://github.com/NuGet/Home/issues/3894) Için varsayılan ContentFiles kopyası hatalı

- Paketi Yükle geri yükleme paket geri yükleme geri yükleme paketleri iletisi- [#3785](https://github.com/NuGet/Home/issues/3785)

- Guardrayları kaldır-"çalışma zamanları" bölümünün geri yüklenmesi yalnızca geçerli projeye uygulanmalıdır- [#3768](https://github.com/NuGet/Home/issues/3768)

- Paket görevi, içerik dosyalarını hem ' content/' hem de ' contentFiles/' öğesine koyar- [#3718](https://github.com/NuGet/Home/issues/3718)

- dotnet
  - dotnetcore Pack3, ek etiket bölme [#3701](https://github.com/NuGet/Home/issues/3701)

- dotnet
  - dotnetcore paketi: paket başvuruları olan paketleme projeleri, yinelenen içeri aktarma uyarısı ile sonuçlanır. [#3665](https://github.com/NuGet/Home/issues/3665)

- VS 'de geri yükleme günlüğü her zaman [#3633](https://github.com/NuGet/Home/issues/3633) gösterme

- NuGet Yereller yardım metni hala bahsedilen paketler cache- [#3592](https://github.com/NuGet/Home/issues/3592)

- TargetFramework ile Restore3 bağles Packagereferles. - [#3504](https://github.com/NuGet/Home/issues/3504)

- NuGet, VS "15" Preview 4 dev sürümünde MSBuild 'in beklenmedik sürümünü seçer. komut istemi- [#3408](https://github.com/NuGet/Home/issues/3408)

- Başarısız geri yükleme sırasında hedef/özellik dosyalarını yaz- [#3399](https://github.com/NuGet/Home/issues/3399)

- Geri yükleme sırasında NuGet, VS 15 komut isteminde çalışırken MSBuild ile aynı uyumlu değildir- [#3387](https://github.com/NuGet/Home/issues/3387)

- VS15- [#3272](https://github.com/NuGet/Home/issues/3272) Için PackFromProjectWithDevelopmentDependencySet 'i yeniden etkinleştirin

- NuGet ile sorunları Blend- [#4043](https://github.com/NuGet/Home/issues/4043)

- 4.0.0.2067 ile birlikte çalışmak için CLı ve SDK depolarıyla tümleştirin- [#4029](https://github.com/NuGet/Home/issues/4029)

- Yeni çekirdek konsol uygulaması oluşturduğunuzda, çözümü kapatıp çözümü açıp çözümü kapattığınızda VS askıda kalıyor. [#4008](https://github.com/NuGet/Home/issues/4008)

- D15prerel. 25916.01- [#3982](https://github.com/NuGet/Home/issues/3982) karşı projenin açılmasını kapatma

- DotNet/nuget.exe Yereller belgesi/yardım iletisi- [#3919](https://github.com/NuGet/Home/issues/3919) düzeltir

- Sondaki veya önde gelen boşluklar ile ilgili sorunlar için Paclorsk 'yi inceleyin- [#3906](https://github.com/NuGet/Home/issues/3906)

- dotnet
  - dotnetcore paketi obj 'den Not [#3880](https://github.com/NuGet/Home/issues/3880)

- dotnet
  - dotnetcore paketi her zaman ProjectReference sürümünü 1.0.0- [#3874](https://github.com/NuGet/Home/issues/3874) olarak ayarlanmış görünüyor

- dotnet
  - dotnetcore paketi proje başvuruları ve <TargetFramework>  -  [#3865](https://github.com/NuGet/Home/issues/3865) başarısız oluyor

- ProjectSystemCache. TryGetProjectNameByShortName- [#3861](https://github.com/NuGet/Home/issues/3861) Içindeki LockRecursionException özel durumu

- MSBuild özelliklerinden boşluğu Kırp- [#3819](https://github.com/NuGet/Home/issues/3819)

- Proje yükleme- [#3759](https://github.com/NuGet/Home/issues/3759) oluşturulan iki proje olayını birleştirin

- Dosyadaki P2P kitaplıklarının `project.assets.json` sürümü yanlış [#3748](https://github.com/NuGet/Home/issues/3748)

- Yanıt vermeyen akış ve kullanılamıyor paketi nedeniyle kilitlenme geri yükleme- [#3672](https://github.com/NuGet/Home/issues/3672)

- nuget.exe, büyük miktarda MSBuild hata çıkışı üzerinden askıda kalabilir [#3572](https://github.com/NuGet/Home/issues/3572)

- Blend için geri yükleme, ilk kez başarısız oldu, ikinci kez başarılı oldu (VS senaryosu düzeltildi)- [#2121](https://github.com/NuGet/Home/issues/2121)

### <a name="dcrs"></a>DCR

- VSIX 'i v2 VSIX 'ten v3 VSIX 'e geçirin- [#4196](https://github.com/NuGet/Home/issues/4196)

- NuGet, MSBuild- [#3351](https://github.com/NuGet/Home/issues/3351) kilit dosyasının yolunu almak için bir mekanizmaya sahip olmalıdır

- TFD uyumluluk denetimi ve varlık dosyasına derleme varlıkları ekleme- [#3296](https://github.com/NuGet/Home/issues/3296)

- Pakette ilgili özellikleri etkinleştirmek için paket hedeflerinde yeni bir ProjectCapability "Pack" tanımlayın- [#4146](https://github.com/NuGet/Home/issues/4146)

- Paketi "GeneratePackageOnBuild" MSBuild özelliğinde koşullu bir post derlemesi hedefi olarak Çalıştır- [#4145](https://github.com/NuGet/Home/issues/4145)

- Belirli bir NuGet projesi oluşturmak için, RestoreProjectStyle NuGet özelliğini kullanın- [#4134](https://github.com/NuGet/Home/issues/4134)

- Geçişli proje başvuruları değişikliğini uyarlayın- [#4076](https://github.com/NuGet/Home/issues/4076)

- UWP olmayan projeler için hedef dosyada NuGet özellikleri ekleme- [#4030](https://github.com/NuGet/Home/issues/4030)

- UWP TargetPlatformVersion desteği- [#3923](https://github.com/NuGet/Home/issues/3923)

- Proje başvurusu meta verilerini NuGet proje sistemiyle iletişim [#3922](https://github.com/NuGet/Home/issues/3922)

- Paketleme modu için Kullanıcı arabirimi ekleme- [#3921](https://github.com/NuGet/Home/issues/3921)

- Eski adı `.csproj` , PROJ/targets- [#3854](https://github.com/NuGet/Home/issues/3854) ayarlanan Nugettargetbilinen ad ve runtimetanımlayıcılarına ihtiyaç duyuyor

- Yükleme paketi, otomatik geri yükleme ile çakışabilir [#3836](https://github.com/NuGet/Home/issues/3836)

- VSPackage yüklü olmadığında bağlam menüsü QueryStatus gerçekleşmiyor- [#3835](https://github.com/NuGet/Home/issues/3835)

- Çözüm geri yükleme ve derleme geri yükleme hala iletişim kutularını göster- [#3789](https://github.com/NuGet/Home/issues/3789)

- NuGet 'de VSSDK sürümünü yalıtın. clients çözüm derlemesi- [#3890](https://github.com/NuGet/Home/issues/3890)

## <a name="links-to-github-issues-fixed-in-rtm"></a>RTM 'de düzeltilen GitHub sorunlarına bağlantılar
[Sorun listesi 1](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RTM")  
[Sorun listesi 2](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC4")  
[Sorun listesi 3](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC3")  
[Sorun listesi 4](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC2")  
[Sorun listesi 5](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC")
