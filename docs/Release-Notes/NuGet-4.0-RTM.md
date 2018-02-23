---
title: "NuGet 4.0 RC sürüm notları | Microsoft Docs"
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 03/03/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere NuGet 4.0 RTM için sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 4.0 RTM sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d1ab89f0decb64a64d04dc293e5273b577e8398b
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/20/2018
---
# <a name="nuget-40-rtm-release-notes"></a>NuGet 4.0 RTM sürüm notları

[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) NuGet 4.0 ile .NET Core için destek ekler, kalite düzeltmeler bir grup vardır ve performansı artırır. Bu sürüm ayrıca PackageReference desteği, NuGet komutlarını MSBuild hedefleri, arka plan paket geri yükler ve daha fazlasını olarak gibi çeşitli iyileştirmeler getirir.

## <a name="known-issues"></a>Bilinen sorunlar

### <a name="nuget-restore-may-fail-when-you-have-multiple-projects-referencing-another-project-in-a-solution"></a>Çözümdeki başka bir projeye başvuruda bulunan birden çok projeniz olduğunda NuGet geri yükleme başarısız olabilir

#### <a name="issue"></a>Sorun

Bir çözümde aynı projeye farklı büyük/küçük harf kullanımı veya farklı göreli yollarla birden çok proje başvurusu yapılıyorsa, NuGet geri yükleme çalışmayabilir. [NuGet#4574](https://github.com/NuGet/Home/issues/4574)

#### <a name="workaround"></a>Geçici Çözüm

Büyük/küçük harf kullanımını veya göreli yolları düzelterek tüm proje başvurularında aynı olmalarını sağlayın.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>Paket Yöneticisi Konsolu’nu kullanırken, 'Enter' tuşu çalışmayabilir

#### <a name="issue"></a>Sorun

Bazen Paket Yöneticisi Konsolu’nda Enter tuşu çalışmıyor. Bunu görürseniz, lütfen düzeltmeye yönelik ilerlemeye göz atın ve yeniden oluşturma adımlarınız hakkında yararlı olabilecek ek bilgileri paylaşın. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Geçici Çözüm

Visual Studio’yu yeniden başlatın ve çözümü açmadan önce PMC’yi açın. Alternatif olarak, silmeyi deneyin `project.lock.json` ve yeniden geri yükleme.

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a>.NET Core projelerinde, geçersiz imzalı bir bütünleştirilmiş kod içeren bir paket kullandığınızda sınırsız geri yükleme döngüsüne girebilirsiniz

#### <a name="issue"></a>Sorun

Bazen, geçersiz imzalı bir bütünleştirilmiş kod içeren bir paket kullandığınızda veya paket sürümü 'DateTime' onaylayıcısıyla ayarlandığında, bu durum paket otomatik geri yüklemesinin sınırsız bir döngüde çalışmasına neden olur. [NuGet#4542](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a>Geçici Çözüm

Şu anda bu sorunun geçici çözümü yoktur.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Görüntüleme, ekleme ya da DotNetCLITools, Nuget Paket Yöneticisi'ni kullanarak güncelleştirme

#### <a name="issue"></a>Sorun

NuGet Paket Yöneticisi DotNetCLITools’u görüntülemez ve eklemeye/güncelleştirmeye izin vermez. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>Geçici Çözüm

Proje dosyanızda DotNetCLIToolReferences el ile düzenlenmelidir.

### <a name="nuget-restore-will-fail-when-you-set-packageid-property-for-projects"></a>Projeler için PackageId özelliğini ayarladığınızda NuGet geri yüklemesi başarısız olur

#### <a name="issue"></a>Sorun

.NET Core projeleri için, Visual Studio’da NuGet geri yükleme projelerin PackageId özelliğini kabul etmez. [NuGet#4586](https://github.com/NuGet/Home/issues/4586)

#### <a name="workaround"></a>Geçici Çözüm

Geri yükleme komutunu, komut satırını kullanarak çalıştırın.

### <a name="when-your-project-does-not-have-obj-folder-package-restore-may-fail"></a>Projenizde 'obj' klasörü olmadığında, paket geri yükleme başarısız olabilir

#### <a name="issue"></a>Sorun

'obj' klasörü silindiğinde Visual Studio PackageReferences’ı geri yükleyemez. [NuGet#4528](https://github.com/NuGet/Home/issues/4528)

#### <a name="workaround"></a>Geçici Çözüm

'obj' klasörünü el ile oluşturursanız, geri yükleme çalışacaktır.

### <a name="manually-updating-packages-using-update-package-in-console-may-fail"></a>Konsolda Update-Package kullanarak paketleri el ile güncelleştirme işlemi başarısız olabilir

#### <a name="issue"></a>Sorun

Konsolda ile Update-Package kullanımı, yeni dönüştürülmüş PackageReferences projeleri için tek bir kez çalışır. [NuGet#4431](https://github.com/NuGet/Home/issues/4431)

#### <a name="workaround"></a>Geçici Çözüm

Şu anda bu sorunun geçici çözümü yoktur.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>Hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir

#### <a name="issue"></a>Sorun

Visual Studio’da hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir. Bu durum, paket yöneticisi biçimi olarak PackageReferences kullandığınızda ortaya çıkar. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Geçici Çözüm

El ile geri yükleme yapın.

### <a name="msbuild-trestore-fails-when-a-project-targeting-net461-references-another-project-targeting-netstandard"></a>.NET461’i hedefleyen bir proje, .NETStandard’ı hedefleyen başka bir projeye başvuruda bulunduğunda, msbuild /t:restore başarısız olur

#### <a name="issue"></a>Sorun

.NET461’i hedefleyen PackageReference tabanlı bir proje, .NETStandard’ı hedefleyen PackageReference tabanlı başka bir projeye başvuruda bulunduğunda, msbuild /t:restore başarısız olur.  [NuGet#4532](https://github.com/NuGet/Home/issues/4532)

#### <a name="workaround"></a>Geçici Çözüm

Şu anda bu sorunun geçici çözümü yoktur.

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a>NuGet 4.0 RTM zaman çerçevesinde giderilen sorunlar

[NuGet 4.0 RC sürüm notları](../release-notes/nuget-4.0-RC.md) -NuGet 4.0 RC için düzeltilen tüm sorunları listeler

### <a name="features"></a>Özellikler

- NuGet.Core.sln - dizeleri yerelleştirme [#2041](https://github.com/NuGet/Home/issues/2041)

- Nuget zorlar LSL modunda - web uygulama projeleri yüklemek için [#4258](https://github.com/NuGet/Home/issues/4258)

- Blok sürüme AutoReferenced PackageReference destek değişiklikleri kullanıcı Arabiriminde "yüklü SDK'sı" paketler için - [#4044](https://github.com/NuGet/Home/issues/4044)

- PackageSpec.Version (PackageRef) - proje bağımlılıkları için doğru bir şekilde iletişim [#3902](https://github.com/NuGet/Home/issues/3902)

- Destek başvuruyu kaldırmak için `.csproj` commandline(s) - gelen [#4101](https://github.com/NuGet/Home/issues/4101)

- Geri yükleme PackageReference projeleri (normal ve xplat) ve basit çözüm yük - desteği [#4003](https://github.com/NuGet/Home/issues/4003)

- Destek içine başvurular eklemek için `.csproj` commandline(s) - gelen [#3751](https://github.com/NuGet/Home/issues/3751)

- Basit çözüm yük için NuGet geri yükleme desteği `packages.config` veya `project.json`  -  [#3711](https://github.com/NuGet/Home/issues/3711)

- Content dosyaları destek oluşturulan nuget hedefleri dosyasında - [#3683](https://github.com/NuGet/Home/issues/3683)

- Mono CI Mac üzerinde nuget.exe doğrulama için kurmak MSBuild - kullanma [#3646](https://github.com/NuGet/Home/issues/3646)

- NuGet v2 NuGet.Core bağımlılıkları dışına - taşıma [#3645](https://github.com/NuGet/Home/issues/3645)

### <a name="bugs"></a>Hatalar

- Visual Studio'da NuGet restore saygı projeleri - PackageId özelliği [#4586](https://github.com/NuGet/Home/issues/4586)

- Paket VSIX paketi - eklerken NuGet ProjectSystemCache hata [#4545](https://github.com/NuGet/Home/issues/4545)

- Paketi IncludeSource birden çok TFMs - projeyle kullanılıyorsa özel durum oluşturur [#4536](https://github.com/NuGet/Home/issues/4536)

- Çözüm genelinde Update'ten kullanma VS 2017 RC3 kilitlenme paket Yönetimi - [#4474](https://github.com/NuGet/Home/issues/4474)

- Yeni yüklenen paket - kaldıramazsınız [#4435](https://github.com/NuGet/Home/issues/4435)

- İçin PackageRef geçirirken, karma çözümleri garip geri yükleme davranışını - sahip [#4433](https://github.com/NuGet/Home/issues/4433)

- En kısa sürede NuGet başlattıktan sonra oluşturma işlemi (yükleme, güncelleştirme, geri yükleme) neden olabilecek VS kilitlenmesine - [#4420](https://github.com/NuGet/Home/issues/4420)

- UI askıda - NuGet.SolutionRestoreManager.RestoreManagerPackage başlatma kilitlenme [#4371](https://github.com/NuGet/Home/issues/4371)

- Paketi komutu sürüm öğesi - yerine özniteliği olarak ekleyin [#4325](https://github.com/NuGet/Home/issues/4325)

- Foo.sln--dotnet geri yükleme başarısız olur SLN yapılandırmalarında (ancak, fark config) yinelenen projeleri geri yükleme grafiğinde - neden [#4316](https://github.com/NuGet/Home/issues/4316)

- Yalnızca paketler - içerik [#3668](https://github.com/NuGet/Home/issues/3668)

- Varsayılan olarak paket biçimi Seçici seçeneği dışında - opt [#4468](https://github.com/NuGet/Home/issues/4468)

- Perf: CreateUAP_CSharp_VS.01.1.Create Proje 3,153.570 ms (%149.1) tarafından Duration_TotalElapsedTime gerileyen. Taban çizgisi 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)

- Perf: ManagedLangs_CS_DDRIT.0300.Rebuild çözüm tarafından 1,5 sn Duration_TotalElapsedTime gerileyen. Taban çizgisi 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)

- Adaylığı başarısız çoklu TFM projelerinde - [#4419](https://github.com/NuGet/Home/issues/4419)

- Perf: WebForms_DDRIT.1200.Close çözüm 3.000 sayısı (% 0,5) tarafından VM_ImagesInMemory_Total_devenv gerileyen. Taban çizgisi 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)

- vsfeedback - netcoreapp1.1 hedeflerken paketi uyarılar - [#4397](https://github.com/NuGet/Home/issues/4397)

- Bir NuGet paketi için boş ASP.NET Core web uygulaması - eklenmeye çalışılırken PathTooLongException [#4391](https://github.com/NuGet/Home/issues/4391)

- Paketi çalıştıran çok sık--orada ile dotnet paketi başarısız olduğu hedef bağımlılık grafiği içeren hedef "Paketi" - Döngüsel bir bağımlılıkla [#4381](https://github.com/NuGet/Home/issues/4381)

- Paketi çalıştıran çok sık--oluşturmak NuGet paketi, tüm yapılandırmaları - içermez [#4380](https://github.com/NuGet/Home/issues/4380)

- NullReferenceException ekleme nuget C++ projesinde - packageref ile [#4378](https://github.com/NuGet/Home/issues/4378)

- Erişilebilirlik: Ekran okuyucusu - paketi yüklemek için projeleri seçmek için onay kutusunu ile Anlat değil [#4366](https://github.com/NuGet/Home/issues/4366)

- NuGet VS17 düzensiz aralıklarla hataya başarısız - VS hata 365798 - VSO/VSTS akışları bağlanma [#4365](https://github.com/NuGet/Home/issues/4365)

- Content dosyaları alırsanız yanlış konuma çıktı ise PackagePath "Content dosyaları" - olarak yolunu belirtir, [#4348](https://github.com/NuGet/Home/issues/4348)

- Paketi hedef ekler VersionSuffix - PackageVersion özelliğiyle [#4324](https://github.com/NuGet/Home/issues/4324)

- Paket yolu dotnet paketiyle - işe yaramazsa belirtme [#4321](https://github.com/NuGet/Home/issues/4321)

- Geri yükleme sırasında - NuGet çıkarır yinelenen içeri aktarmaları hakkında uyarılar bir grup [#4304](https://github.com/NuGet/Home/issues/4304)

- "NuGet Paket Yöneticisi Format" iletişim koyu tema altında - bozuk görünüyor seçin [#4300](https://github.com/NuGet/Home/issues/4300)

- VS kilitlenme yapı geri yükleme - [#4298](https://github.com/NuGet/Home/issues/4298)

- Visual Studio kilitlenmeleri targetframeworks içinde TFM eklerseniz kaydedin, sonra oluşturun. Süre - % 10 [#4295](https://github.com/NuGet/Home/issues/4295)

- nuget paketi, Proje başarıyla - paket üzerinde başarı iletisi çıktı değil [#4294](https://github.com/NuGet/Home/issues/4294)

- PackTask System.IO.Compression 4.1 değil olması nedeniyle başarısız bulunamadı - [#4290](https://github.com/NuGet/Home/issues/4290)

- Paketi çalıştıran çok sık--PackTask sık sık başarısız dosya erişim çakışma - [#4289](https://github.com/NuGet/Home/issues/4289)

- NuGet arka plan geri yükleme sırasında - çıktı penceresi açar [#4274](https://github.com/NuGet/Home/issues/4274)

- (Hangi kilitlenmesine neden) tehlikeli kodlama düzeni - ServiceProvider ortadan [#4268](https://github.com/NuGet/Home/issues/4268)

- Perf/UIHang - DownloadTimeoutStream okuma - artırmak [#4266](https://github.com/NuGet/Home/issues/4266)

- Visual Studio kilitlenmeleri NuGet geri yüklemesi bitmeden önce - bir projeyi kapatın çalışırsanız [#4257](https://github.com/NuGet/Home/issues/4257)

- PackTask ve paketleme ile ilgili sorunları `.nuspec`  -  [#4250](https://github.com/NuGet/Home/issues/4250)

- [vsfeedback] Yeni Proje (visual studio yeniden başlatma gerekir) - nuget paketlerini çözümlenemiyor [#4217](https://github.com/NuGet/Home/issues/4217)

- [vsfeedback] "Sürüm" açılan listesi kullanılabilir paket sürümlerinin kalmak için struggles içinde eşitleme seçili nuGet paketi ile birlikte... - gösteren [#4198](https://github.com/NuGet/Home/issues/4198)

- Nuget.Client kullanması gereken CPS JoinableTaskFactory ile CPS kullanılırken kilitlenmeleri - önlemek için [#4185](https://github.com/NuGet/Home/issues/4185)

- NuGet 3.5.0 değil paketi açılırken `.targets` - paketten [#4171](https://github.com/NuGet/Home/issues/4171)

- DotNet paketi başlığında desteklemediği `.csproj`  -  [#4150](https://github.com/NuGet/Home/issues/4150)

- Hata iletişim kutusunda VS2017 RC - Install-Package sonuçlanıyor [#4127](https://github.com/NuGet/Home/issues/4127)

- Kullanıcı arabirimini CPS güncelleştirme nominate açılmıyor gibi .net core proje için bir paket güncelleştirme çalışmıyor için görünür. - [#4035](https://github.com/NuGet/Home/issues/4035)

- Çözümlenmemiş başvuru uyarısı - artırmak [#3955](https://github.com/NuGet/Home/issues/3955)

- DotNet paketi - ProjectReference kaybeder sürüm bilgilerini - [#3953](https://github.com/NuGet/Home/issues/3953)

- UWP uygulaması oluşturma projesi oluşturun ve geçen toplam süre gerileme - yeniden [#3873](https://github.com/NuGet/Home/issues/3873)

- Başarıyla geri ileti geri yükleme sırasında bile hatasından sonra görüntülenir. - [#3799](https://github.com/NuGet/Home/issues/3799)

- Nuget.CommandLine 3.4.4 Nuget.org için-yeniden yayımlayın [#2931](https://github.com/NuGet/Home/issues/2931)

- Projeleri geçirme üzerinde çıkarılıp `project.json` için `.csproj` ---geri yükleme başarısız - [#4297](https://github.com/NuGet/Home/issues/4297)

- Yeni oluşturulan xunit Test projede - geri yükleme başarısız [#4296](https://github.com/NuGet/Home/issues/4296)

- Çekirdek projeleri askıda, UI - açık kilitlemek [#4269](https://github.com/NuGet/Home/issues/4269)

- derleme görevleri - hedefleri dosyasını düzeltmek [#4267](https://github.com/NuGet/Home/issues/4267)

- Hata listesi başvurulan proje - unload yapı çözümü sonra hata sahip [#4208](https://github.com/NuGet/Home/issues/4208)

- MSB4057: "_GenerateRestoreGraphProjectEntry" hedef projede mevcut değil. - [#4194](https://github.com/NuGet/Home/issues/4194)

- vsfeedback: çözüm için nuget Yöneticisi kullanıcı arabirimi çöküyor tüm projeleri - seçtiğinizde [#4191](https://github.com/NuGet/Home/issues/4191)

- nuget.exe msbuildpath başarısız eğik - olduğunda [#4180](https://github.com/NuGet/Home/issues/4180)

- vsfeedback: NuGet restore vermek LinqToTwitter proje için-birkaç proje başvurusu uyarıları [#4156](https://github.com/NuGet/Home/issues/4156)

- Gelen paket `.csproj` minClientVersion özniteliği - içermez [#4135](https://github.com/NuGet/Home/issues/4135)

- NuGet.Build.Tasks.Pack.dll sevk VS2017 içinde imzalı gecikme (d15rel 26014.00)- [#4122](https://github.com/NuGet/Home/issues/4122)

- VSFeedback: 3.7.1 - CMake ile oluşturulan bir VS 2015 projesi için geri yükleme başarısız [#4114](https://github.com/NuGet/Home/issues/4114)

- VSFeedback: Derleme sunabilir - daha ayrıntılı hata iletilerini geri yükleme hatalarını soyutlamaması [#4113](https://github.com/NuGet/Home/issues/4113)

- [VSFeedback] Web projesi için NuGet paketleri geri yüklenirken hata oluştu: değer null olamaz. - [#4092](https://github.com/NuGet/Home/issues/4092)

- Geçiş oluşturur "nesne başvurusu özel durumu NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker içinde - nesnenin" [#4067](https://github.com/NuGet/Home/issues/4067)

- DotNet pack Araçları Paketi karşı - oluşturulan sürümlerle [#4063](https://github.com/NuGet/Home/issues/4063)

- Yeni arka plan geri yükleme durum çubuğunda zaman geri yüklemek için - saniye sürer milisaniye Yazar [#4036](https://github.com/NuGet/Home/issues/4036)

- Üzerinde yazım hatası başarısız tüm proje başvuruları - çözümlemek [#4018](https://github.com/NuGet/Home/issues/4018)

- Paket başvuru senaryolarda - PCM iş akışlarını etkinleştirin [#4016](https://github.com/NuGet/Home/issues/4016)

- Yüklü paketler Yöneticisi kullanıcı Arabirimi - paketinde bulunamıyor [#4015](https://github.com/NuGet/Home/issues/4015)

- DotNet paketi başarısız ise PackagePath boş - olduğunda [#3993](https://github.com/NuGet/Home/issues/3993)

- Bir Çoklu kullanıcı senaryosunda - görev başarısız geri [#3897](https://github.com/NuGet/Home/issues/3897)

- NuGet paketi görevini kullanarak paket içerik türü değiştirilemiyor- [#3895](https://github.com/NuGet/Home/issues/3895)

- Content varsayılan Kopyala'dosyaları için MsBuild /t:pack - yanlış [#3894](https://github.com/NuGet/Home/issues/3894)

- Yükleme paketi geri yüklemesi çift günlüklerini geri yükleme paketleri iletisi - [#3785](https://github.com/NuGet/Home/issues/3785)

- Guardrails - kaldırma geri yükleme "çalışma zamanları" bölümünün yalnızca geçerli projeye - uygulanması [#3768](https://github.com/NuGet/Home/issues/3768)

- Paketi görevi koyar içerik dosyalarının ikisi de ' içeriği /' ve ' Content dosyaları /'- [#3718](https://github.com/NuGet/Home/issues/3718)

- DotNet pack3 çok etiket bölme - [#3701](https://github.com/NuGet/Home/issues/3701)

- DotNet paketi: Paket projelerle sevk başvuran yinelenen alma uyarı - sonuçlarında [#3665](https://github.com/NuGet/Home/issues/3665)

- Geri yükleme VS günlüğü değil her zaman göster - [#3633](https://github.com/NuGet/Home/issues/3633)

- nuget Yereller Yardım metni hala paketleri önbellek - belirtilen [#3592](https://github.com/NuGet/Home/issues/3592)

- Restore3 PackageReferences TargetFrameworks ile tüm çiftler. - [#3504](https://github.com/NuGet/Home/issues/3504)

- Nuget Çekmeleri MSBuild beklenmeyen sürümü VS "15" Preview 4 istisnası command prompt - [#3408](https://github.com/NuGet/Home/issues/3408)

- Hedefleri/özellik dosyaları geri yükleme başarısız - out yazma [#3399](https://github.com/NuGet/Home/issues/3399)

- VS 15 Komut İstemi'nde - çalıştırırken, geri yükleme sırasında NuGet MSBuild olarak aynı compat dolgular saygı değil [#3387](https://github.com/NuGet/Home/issues/3387)

- PackFromProjectWithDevelopmentDependencySet VS15 için - yeniden etkinleştirmek [#3272](https://github.com/NuGet/Home/issues/3272)

- Harmanlama NuGet - sorun [#4043](https://github.com/NuGet/Home/issues/4043)

- 4.0.0.2067 RC2 ile - dağıtmayı CLI ve SDK depoları şekilde entegre [#4029](https://github.com/NuGet/Home/issues/4029)

- Yeni çekirdek konsol uygulaması, Kapat çözümü, çözüm açmak ve Kapat çözüm - oluşturduğunuzda, VS askıda [#4008](https://github.com/NuGet/Home/issues/4008)

- D15prerel.25916.01 karşı-kilitlenebilir açılış proje basarsa [#3982](https://github.com/NuGet/Home/issues/3982)

- Belge/Yardım iletisi - dotnet/nuget.exe Yereller düzeltme [#3919](https://github.com/NuGet/Home/issues/3919)

- Başında veya sonunda boşluk - sorunlarını PackTask incelemek [#3906](https://github.com/NuGet/Home/issues/3906)

- DotNet paketi obj değil depo - paket [#3880](https://github.com/NuGet/Home/issues/3880)

- DotNet paketi her zaman görünüyor ProjectReference sürümü 1.0.0 için - Ayarla [#3874](https://github.com/NuGet/Home/issues/3874)

- DotNet paketi proje başvuruları ile başarısız olur ve <TargetFramework>  -  [#3865](https://github.com/NuGet/Home/issues/3865)

- LockRecursionException in ProjectSystemCache.TryGetProjectNameByShortName - [#3861](https://github.com/NuGet/Home/issues/3861)

- MSBuild özellikleri - boşlukları kırpma [#3819](https://github.com/NuGet/Home/issues/3819)

- Proje yükünü - oluşturulan iki proje olaylara birleştirmek [#3759](https://github.com/NuGet/Home/issues/3759)

- P2p kitaplıklarında `project.assets.json` dosyanız yanlış sürümü - [#3748](https://github.com/NuGet/Home/issues/3748)

- Yanıt akışı ve kullanılabilir paket - nedeniyle kilitlenme geri [#3672](https://github.com/NuGet/Home/issues/3672)

- nuget.exe MSBuild hata çıktısı - büyük miktarda üzerinde telefonu kapatın [#3572](https://github.com/NuGet/Home/issues/3572)

- Derleme üzerinde geri yükleme karışım ilk kez başarısız için ikinci kez (VS senaryo sabit) - başarılı [#2121](https://github.com/NuGet/Home/issues/2121)

### <a name="dcrs"></a>Dcr

- VSIX v3 VSIX için - v2 VSIX geçirmek [#4196](https://github.com/NuGet/Home/issues/4196)

- NuGet yolu almak için bir mekanizma olmalıdır MSBuild - lock dosyasında [#3351](https://github.com/NuGet/Home/issues/3351)

- Yapı varlıklar TFM uyumluluk denetimi ve varlıklar - eklemek [#3296](https://github.com/NuGet/Home/issues/3296)

- Yeni ProjectCapability "Paketi" paketinde tanımlamak paketi etkinleştirme hedefleri ilgili özellikleri - [#4146](https://github.com/NuGet/Home/issues/4146)

- Bir post yapı olarak "GeneratePackageOnBuild" MSBuild özellikte - söylediğinizde hedef paketi çalıştırmak [#4145](https://github.com/NuGet/Home/issues/4145)

- NuGet özelliği RestoreProjectStyle belirli NuGet proje - oluşturulacağı [#4134](https://github.com/NuGet/Home/issues/4134)

- Geçişli proje başvuruları değiştirmek için - geri yükleme uyum [#4076](https://github.com/NuGet/Home/issues/4076)

- Hedef dosyada olmayan UWP projeleri - NuGet özellikleri ekleme [#4030](https://github.com/NuGet/Home/issues/4030)

- UWP TargetPlatformVersion desteği - [#3923](https://github.com/NuGet/Home/issues/3923)

- NuGet proje sistemine - proje başvuru meta verisi iletişim [#3922](https://github.com/NuGet/Home/issues/3922)

- İçin paketleme modu - kullanıcı Arabirimi eklemek [#3921](https://github.com/NuGet/Home/issues/3921)

- Eski `.csproj` NugetTargetMoniker ve proj/hedefleri - ayarlamak RuntimeIdentifiers gereken [#3854](https://github.com/NuGet/Home/issues/3854)

- Yükleme paketi-restore - otomatik çakışıyor [#3836](https://github.com/NuGet/Home/issues/3836)

- Bağlam menüsü QueryStatus değil durum VSPackage değil yüklendiğinde - [#3835](https://github.com/NuGet/Home/issues/3835)

- Çözüm geri yükleme ve yapı geri hala iletişim kutuları - Göster [#3789](https://github.com/NuGet/Home/issues/3789)

- NuGet.Clients çözümü derleme - yalıtmak VSSDK sürümünde [#3890](https://github.com/NuGet/Home/issues/3890)

## <a name="links-to-github-issues-fixed-in-rtm"></a>GitHub sorunları RTM'de sabit bağlantılar
[Konu listesi 1](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RTM")  
[Konu listesi 2](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC4")  
[Konu listesi 3](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC3")  
[Konu listesi 4](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC2")  
[Konu listesi 5](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0 RC")
