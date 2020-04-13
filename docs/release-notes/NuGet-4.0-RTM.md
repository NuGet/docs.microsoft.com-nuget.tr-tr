---
title: NuGet 4.0 RC Yayın Notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve DCR'ler dahil olmak üzere NuGet 4.0 RTM için sürüm notları.
author: anangaur
ms.author: anangaur
ms.date: 03/03/2017
ms.topic: conceptual
ms.openlocfilehash: c27d0aa2e5c9af9cb15d2f487b93e93aca666214
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496599"
---
# <a name="nuget-40-rtm-release-notes"></a>NuGet 4.0 RTM Yayın Notları

[Visual Studio 2017,](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) .NET Core'a destek sağlayan, bir sürü kalite düzeltmesi olan ve performansı artıran NuGet 4.0 ile birlikte geliyor. Bu sürüm aynı zamanda PackageReference desteği, MSBuild hedefleri olarak NuGet komutları, arka plan paketi geri yüklemesi ve daha fazlası gibi çeşitli iyileştirmeler de getirir.

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

Visual Studio’yu yeniden başlatın ve çözümü açmadan önce PMC’yi açın. Alternatif olarak, silme `project.lock.json` ve yeniden geri deneyin.

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a>.NET Core projelerinde, geçersiz imzalı bir bütünleştirilmiş kod içeren bir paket kullandığınızda sınırsız geri yükleme döngüsüne girebilirsiniz

#### <a name="issue"></a>Sorun

Bazen, geçersiz imzalı bir bütünleştirilmiş kod içeren bir paket kullandığınızda veya paket sürümü 'DateTime' onaylayıcısıyla ayarlandığında, bu durum paket otomatik geri yüklemesinin sınırsız bir döngüde çalışmasına neden olur. [NuGet#4542](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a>Geçici çözüm

Şu anda bu sorunun geçici çözümü yoktur.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Nuget Package Manager'ı kullanarak DotNetCLITools'u görüntüleyemiyor, ekleyemiyor veya güncelleştiremiyorsunuz

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

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a>NuGet 4.0 RTM zaman diliminde düzeltilen sorunlar

[NuGet 4.0 RC Yayın Notları](../release-notes/nuget-4.0-RC.md) - NuGet 4.0 RC için düzeltilen tüm sorunları listeler

### <a name="features"></a>Özellikler

- NuGet.Core.sln'de dizeleri [yerelleştirin](https://github.com/NuGet/Home/issues/2041) - #2041

- Nuget kuvvetleri LSL modunda web uygulama projeleri yüklemek için - [#4258](https://github.com/NuGet/Home/issues/4258)

- "sdk yüklü" paketler için UI sürüm değişikliklerini engellemek için AutoReferenced PackageReference desteği - [#4044](https://github.com/NuGet/Home/issues/4044)

- Doğru herhangi bir proje bağımlılıkları (PackageRef) için PackageSpec.Version iletişim - [#3902](https://github.com/NuGet/Home/issues/3902)

- komut satırından(lar)a `.csproj` başvuruları kaldırmak için destek - [#4101](https://github.com/NuGet/Home/issues/4101)

- PackageReference projeleri (normal ve xplat) ve Hafif Çözüm Yükü için destek geri [yüklemesi](https://github.com/NuGet/Home/issues/4003) - #4003

- commandline(lar) `.csproj` içine referanseklemek için destek - [#3751](https://github.com/NuGet/Home/issues/3751)

- Destek NuGet geri yükleme `packages.config` için `project.json`  - hafif çözüm yükü için veya [#3711](https://github.com/NuGet/Home/issues/3711)

- contentFiles nuget oluşturulan hedefler dosyasında destek - [#3683](https://github.com/NuGet/Home/issues/3683)

- MSBuild kullanarak Mac'te nuget.exe doğrulaması için mono ci [-#3646](https://github.com/NuGet/Home/issues/3646)

- Move NuGet off v2 NuGet.Core bağımlılıkları - [#3645](https://github.com/NuGet/Home/issues/3645)

### <a name="bugs"></a>Hatalar

- NuGet geri Visual Studio projelerin PackageId özelliğine saygı duymaz - [#4586](https://github.com/NuGet/Home/issues/4586)

- VSIX paketine paket eklerken NuGet ProjectSystemCache hatası - [#4545](https://github.com/NuGet/Home/issues/4545)

- IncludeSource birden fazla TFM'si olan bir projede kullanılıyorsa paket özel durum atar - [#4536](https://github.com/NuGet/Home/issues/4536)

- VS 2017 RC3, Solution genelindeki paket yönetiminden gelen güncellemeyi kullanarak çöküyor - [#4474](https://github.com/NuGet/Home/issues/4474)

- Yeni yüklenen paketi kaldıramıyorum - [#4435](https://github.com/NuGet/Home/issues/4435)

- PackageRef'e geçiş yaparken, karma çözümler garip geri yükleme davranışına sahiptir - [#4433](https://github.com/NuGet/Home/issues/4433)

- NuGet işlemine başladıktan kısa bir süre sonra bina (yükleme, güncelleme, geri yükleme), VS'nin Hang'a neden olabilir - [#4420](https://github.com/NuGet/Home/issues/4420)

- UI Hang - NuGet.SolutionRestoreManager.RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371) başlatma Deadlock

- paket komutu ekle öğe yerine öznitelik olarak sürüm eklemelidir - [#4325](https://github.com/NuGet/Home/issues/4325)

- dotnet
  - dotnetcore Geri Yükleme foo.sln - SLN yapılandırmaları geri yükleme grafiğiyineleme (ama diff config) projelere neden olduğunda başarısız olur - [#4316](https://github.com/NuGet/Home/issues/4316)

- İçerik sadece paketler - [#3668](https://github.com/NuGet/Home/issues/3668)

- Varsayılan olarak paket biçimi seçici seçeneğini devre dışı bırakma - [#4468](https://github.com/NuGet/Home/issues/4468)

- Perf: CreateUAP_CSharp_VS.01.1.Create projesi Duration_TotalElapsedTime 3.153.570 ms (%149.1) geriledi. Taban Çizgisi 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)

- Perf: ManagedLangs_CS_DDRIT.0300.Rebuild Çözüm 1.5sec tarafından Duration_TotalElapsedTime geriledi. Temel 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)

- Çoklu TFM projelerinde adaylık başarısız oldu - [#4419](https://github.com/NuGet/Home/issues/4419)

- Perf: WebForms_DDRIT.1200.Close Solution VM_ImagesInMemory_Total_devenv 3.000 Sayı (%0.5) geriledi. Taban çizgisi 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)

- vsfeedback - netcoreapp1.1 hedeflenirken paketleri uyarılar - [#4397](https://github.com/NuGet/Home/issues/4397)

- PathTooLongException boş ASP.NET Core web uygulamasına bir NuGet paketi eklemeye çalışırken - [#4391](https://github.com/NuGet/Home/issues/4391)

- Sürü çok sık çalışır -- dotnet
  - dotnetcore paketi ile başarısız hedef "Paketi" içeren hedef bağımlılık grafiğinde dairesel bir bağımlılık var - [#4381](https://github.com/NuGet/Home/issues/4381)

- Paket çok sık çalışır -- Generate NuGet paketi tüm yapılandırmaları içermez - [#4380](https://github.com/NuGet/Home/issues/4380)

- NullReferenceExceptionC++ projesinde packageref ile nuget ekleme - [#4378](https://github.com/NuGet/Home/issues/4378)

- Erişilebilirlik : Ekran okuyucupaketi yüklemek için projeleri seçmek için onay kutusunu anlatmaz - [#4366](https://github.com/NuGet/Home/issues/4366)

- NuGet VS17, VSO/VSTS beslemelerine ( VS Bug 365798 - [#4365](https://github.com/NuGet/Home/issues/4365)

- contentFiles, PackagePath yolu "contentFiles" olarak belirtirse çıktıyı yanlış konuma getirin - [#4348](https://github.com/NuGet/Home/issues/4348)

- Pack hedef SürümSuffix ile PackageVersion özelliği ekler - [#4324](https://github.com/NuGet/Home/issues/4324)

- Paket yolunu belirtme dotnet paketiile çalışmaz - [#4321](https://github.com/NuGet/Home/issues/4321)

- NuGet geri yükleme sırasında yinelenen içeri almalar hakkında bir sürü uyarı çıktısı #4304 [#4304](https://github.com/NuGet/Home/issues/4304)

- "NuGet Package Manager Format" iletişim kutusunu seçin karanlık tema altında kötü görünüyor - [#4300](https://github.com/NuGet/Home/issues/4300)

- VS çarpışma inşa geri yükleme - [#4298](https://github.com/NuGet/Home/issues/4298)

- Hedef çerçevelere TFM eklerseniz Visual Studio kilitlenir, kaydedin, sonra oluşturun. Zaman% 10 - [#4295](https://github.com/NuGet/Home/issues/4295)

- nuget paketi başarıyla bir proje ambalaj başarı mesajı çıktı değil - [#4294](https://github.com/NuGet/Home/issues/4294)

- PackTask System.IO.Compression 4.1 bulunamadı nedeniyle başarısız olur - [#4290](https://github.com/NuGet/Home/issues/4290)

- Paket çok sık çalışır - PackTask sık sık dosya erişim çakışması ile başarısız olur - [#4289](https://github.com/NuGet/Home/issues/4289)

- NuGet arka plan geri yükleme sırasında çıkış penceresini açar - [#4274](https://github.com/NuGet/Home/issues/4274)

- ServiceProvider'ı tehlikeli kodlama deseni olarak ortadan kaldırın (askıda kalmasına neden olabilir) - [#4268](https://github.com/NuGet/Home/issues/4268)

- Perf /UIHang - DownloadTimeoutStream geliştirin okur - [#4266](https://github.com/NuGet/Home/issues/4266)

- NuGet geri yüklemesi tamamlanmadan önce bir projeyi kapatmaya çalışırsanız Visual Studio kilitlenir - [#4257](https://github.com/NuGet/Home/issues/4257)

- PackTask ve ambalaj `.nuspec`  -  [#4250](https://github.com/NuGet/Home/issues/4250) ile ilgili sorunlar

- [vsfeedback] Yeni projede nuget paketleri çözemez (visual studio yeniden başlatmaihtiyacı) - [#4217](https://github.com/NuGet/Home/issues/4217)

- [vsfeedback] Kullanılabilir paket sürümlerini gösteren "Sürüm" açılır, seçilen nuGet paketi ile senkronize kalmak için mücadele eder... - [#4198](https://github.com/NuGet/Home/issues/4198)

- Nuget.Client kilitlenmeleri önlemek için CPS ile etkileşimde cps JoinableTaskFactory kullanmalıdır - [#4185](https://github.com/NuGet/Home/issues/4185)

- NuGet 3.5.0 `.targets` paketten ambalajı açılmaz - [#4171](https://github.com/NuGet/Home/issues/4171)

- dotnet
  - dotnetcore paketi `.csproj`  -  [#4150](https://github.com/NuGet/Home/issues/4150) başlık desteklemiyor

- VS2017 RC'de hata iletişim kutusunda yükleme-Paket sonuçları - [#4127](https://github.com/NuGet/Home/issues/4127)

- .net çekirdek projesi için bir paketi güncelleştirme, kullanıcı arabirimi tarafından CPS güncelleştirmesini alamadığı için işe yaramıyor gibi görünüyor. - [#4035](https://github.com/NuGet/Home/issues/4035)

- Çözülmemiş başvuru uyarısını geliştirin - [#3955](https://github.com/NuGet/Home/issues/3955)

- dotnet
  - dotnetcore paketi - ProjectReference sürüm bilgilerini kaybeder - [#3953](https://github.com/NuGet/Home/issues/3953)

- UWP uygulaması oluşturma & toplam geçen süre gerilemelerini yeniden oluşturma - [#3873](https://github.com/NuGet/Home/issues/3873)

- Başarılı geri yükleme iletisi geri yükleme sırasında hata sonra bile görüntülenir. - [#3799](https://github.com/NuGet/Home/issues/3799)

- yeniden Yayımla Nuget.CommandLine 3.4.4 to Nuget.org - [#2931](https://github.com/NuGet/Home/issues/2931)

- Geçir'de, projeler `project.json` `.csproj` --- geri yükleme başarısız olur - [#4297](https://github.com/NuGet/Home/issues/4297)

- Yeni oluşturulan xunit Test projesinde başarısız olan geri yükleme - [#4296](https://github.com/NuGet/Home/issues/4296)

- Çekirdek projeler asabilir, açık ui kilitlemek - [#4269](https://github.com/NuGet/Home/issues/4269)

- yapı görevleri için hedefler dosyayı düzeltme - [#4267](https://github.com/NuGet/Home/issues/4267)

- Hata listesinde başvurulan projeyi boşaltan yapı çözümünden sonra hata var - [#4208](https://github.com/NuGet/Home/issues/4208)

- MSB4057: Projede "_GenerateRestoreGraphProjectEntry" hedefi yok. - [#4194](https://github.com/NuGet/Home/issues/4194)

- vsfeedback: tüm projeleri seçtiğinizde çözüm çöküyor için nuget manager ui - [#4191](https://github.com/NuGet/Home/issues/4191)

- nuget.exe msbuildpath bir iz çizgi olduğunda başarısız olur - [#4180](https://github.com/NuGet/Home/issues/4180)

- vsfeedback: NuGet geri LinqToTwitter projesi için çeşitli proje referans uyarıları vermek geri - [#4156](https://github.com/NuGet/Home/issues/4156)

- Paket `.csproj` minClientVersion özniteliği içermez - [#4135](https://github.com/NuGet/Home/issues/4135)

- NuGet.Build.Tasks.Pack.dll sevk gecikmesi VS2017 (d15rel 26014.00) - [#4122](https://github.com/NuGet/Home/issues/4122)

- VSFeedback: CMake 3.7.1 ile oluşturulan VS 2015 projesi için geri yükleme başarısız oldu - [#4114](https://github.com/NuGet/Home/issues/4114)

- VSFeedback: Geri yükleme hataları oluşturmak verebilir daha tam hata iletileri gizleyebilirsiniz - [#4113](https://github.com/NuGet/Home/issues/4113)

- [VSFeedback] Web sitesi projesi için NuGet paketlerini geri alırken hata oluştu: Değer null olamaz. - [#4092](https://github.com/NuGet/Home/issues/4092)

- Geçiş NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker "Nesne başvuru Özel Durum" atar - [#4067](https://github.com/NuGet/Home/issues/4067)

- dotnet
  - dotnetcore paketi paketi karşı inşa edilmiş sürümleri ile araçları paketi gerekir - [#4063](https://github.com/NuGet/Home/issues/4063)

- Yeni arka plan geri yüklemesi, saniyeler zaman zaman durum çubuğuna milisaniye yazar - [#4036](https://github.com/NuGet/Home/issues/4036)

- Yazım hatası tüm proje referansları çözmek için başarısız oldu - [#4018](https://github.com/NuGet/Home/issues/4018)

- Paket başvuru senaryolarında PCM iş akışlarını etkinleştirin - [#4016](https://github.com/NuGet/Home/issues/4016)

- Paket yöneticisi UI yüklü paketleri bulamıyorum - [#4015](https://github.com/NuGet/Home/issues/4015)

- dotnet
  - PackagePath boş olduğunda dotnetcore paketi başarısız olur - [#3993](https://github.com/NuGet/Home/issues/3993)

- Geri yükleme görevi çok kullanıcılı bir senaryoda başarısız olur - [#3897](https://github.com/NuGet/Home/issues/3897)

- NuGet Pack Task kullanarak ambalajlarken İçerik türünü değiştiremezsiniz - [#3895](https://github.com/NuGet/Home/issues/3895)

- İçerik Dosyalarının Varsayılan Kopyası MsBuild /t:pack için yanlış - [#3894](https://github.com/NuGet/Home/issues/3894)

- Paketi geri yükleyin çift günlükleri geri paketleri mesajı - [#3785](https://github.com/NuGet/Home/issues/3785)

- Guardrails kaldırın - "runtimes" bölümünün geri yükleme sadece geçerli proje için geçerli olmalıdır - [#3768](https://github.com/NuGet/Home/issues/3768)

- Paket görevi içerik dosyalarını hem 'içerik/' hem de 'contentFiles/' olarak koyar - [#3718](https://github.com/NuGet/Home/issues/3718)

- dotnet
  - dotnetcore pack3 ekstra etiket bölme yok - [#3701](https://github.com/NuGet/Home/issues/3701)

- dotnet
  - dotnetcore paketi: paket referansları ile ambalaj projeleri yinelenen ithalat uyarısı sonuçları - [#3665](https://github.com/NuGet/Home/issues/3665)

- VS'de günlük geri yükleme her zaman görünmüyor - [#3633](https://github.com/NuGet/Home/issues/3633)

- nuget yerliler metin hala belirtilen paketleri önbellek yardım - [#3592](https://github.com/NuGet/Home/issues/3592)

- TargetFrameworks ile Restore3 çiftler PackageReferences. - [#3504](https://github.com/NuGet/Home/issues/3504)

- Nuget VS MSBuild beklenmedik sürümünü seçer "15" Önizleme 4 dev. komut istemi - [#3408](https://github.com/NuGet/Home/issues/3408)

- Başarısız geri yüklemede hedef/sahne dosyalarını yazma - [#3399](https://github.com/NuGet/Home/issues/3399)

- Geri yükleme sırasında NuGet VS 15 komut istemi çalışırken MSBuild ile aynı compat shims saygı yok - [#3387](https://github.com/NuGet/Home/issues/3387)

- VS15 için PackFromProjectWithDevelopmentDependencySet'i yeniden etkinleştirin - [#3272](https://github.com/NuGet/Home/issues/3272)

- NuGet ile sorunları karıştırın - [#4043](https://github.com/NuGet/Home/issues/4043)

- 4.0.0.2067'yi CLI ve SDK depolarına entegre edin - [#4029](https://github.com/NuGet/Home/issues/4029)

- Yeni Core Console App, Close Solution, Open Solution ve Close Solution Oluştururken VS Askıda Kalır - [#4008](https://github.com/NuGet/Home/issues/4008)

- D15prerel.25916.01 karşı asmak açılış projesi isabet - [#3982](https://github.com/NuGet/Home/issues/3982)

- dotnet/nuget.exe locals doc/help message 'ı düzelt [- #3919](https://github.com/NuGet/Home/issues/3919)

- PackTask'ı izleme veya önde gelen beyaz alanla ilgili sorunlar için denetleyin - [#3906](https://github.com/NuGet/Home/issues/3906)

- dotnet
  - dotnetcore paketi obj değil bin ambalaj - [#3880](https://github.com/NuGet/Home/issues/3880)

- dotnet
  - dotnetcore paketi her zaman 1.0.0 ProjectReference sürümünü ayarlamak gibi görünüyor - [#3874](https://github.com/NuGet/Home/issues/3874)

- dotnet
  - dotnetcore paketi proje referansları ve <TargetFramework>  -  [#3865](https://github.com/NuGet/Home/issues/3865) ile başarısız

- ProjectSystemCache.TryGetProjectNameByShortName içinde LockRecursionException - [#3861](https://github.com/NuGet/Home/issues/3861)

- MSBuild özelliklerinden beyaz boşluğu kırpın - [#3819](https://github.com/NuGet/Home/issues/3819)

- Proje yükü yle toplanan iki proje olayını birleştirin - [#3759](https://github.com/NuGet/Home/issues/3759)

- Dosyadaki P2P kitaplıklarında `project.assets.json` yanlış Sürüm var - [#3748](https://github.com/NuGet/Home/issues/3748)

- Yanıt vermeyen besleme ve kullanılamayan paket nedeniyle kilitlenmeyi geri yükleme - [#3672](https://github.com/NuGet/Home/issues/3672)

- nuget.exe MSBuild hata çıkışı büyük miktarda asmak olabilir - [#3572](https://github.com/NuGet/Home/issues/3572)

- Blend için geri yükleme-on-build ilk kez başarısız olur, ikinci kez başarılı (VS senaryo sabit) - [#2121](https://github.com/NuGet/Home/issues/2121)

### <a name="dcrs"></a>DCRs

- v2 vsix v3 vsix için vsix göç - [#4196](https://github.com/NuGet/Home/issues/4196)

- NuGet MSBuild kilit dosyasına yol almak için bir mekanizma olmalıdır - [#3351](https://github.com/NuGet/Home/issues/3351)

- TFM uyumluluk denetimine ve varlıklar dosyasına yapı varlıkları ekleme - [#3296](https://github.com/NuGet/Home/issues/3296)

- Paketle ilgili yetenekleri etkinleştirmek için Paket hedeflerinde yeni bir ProjectCapability "Pack" tanımlayın - [#4146](https://github.com/NuGet/Home/issues/4146)

- "GeneratePackageOnBuild" MSBuild özelliği koşullu bir sonrası inşa hedef olarak Çalıştır ın - [#4145](https://github.com/NuGet/Home/issues/4145)

- Belirli NuGet projesi oluşturmak için NuGet özelliği RestoreProjectStyle'ı kullanın - [#4134](https://github.com/NuGet/Home/issues/4134)

- Geçişli Proje Başvuruları değişikliği için Geri Yükleme'yi [uyarla](https://github.com/NuGet/Home/issues/4076) - #4076

- UWP olmayan projeler için hedef dosyaya NuGet özellikleri ekleme - [#4030](https://github.com/NuGet/Home/issues/4030)

- UWP TargetPlatformVersion desteği - [#3923](https://github.com/NuGet/Home/issues/3923)

- Proje referans meta verilerini NuGet proje sistemine [iletin](https://github.com/NuGet/Home/issues/3922) - #3922

- Paketleme modu için UI ekle - [#3921](https://github.com/NuGet/Home/issues/3921)

- Eski `.csproj` proj / hedefler ayarlanmış NugetTargetMoniker ve RuntimeIdentifiers ihtiyacı - [#3854](https://github.com/NuGet/Home/issues/3854)

- Yükleme paketi otomatik geri yükleme ile çakışabilir - [#3836](https://github.com/NuGet/Home/issues/3836)

- Bağlam menüsü QueryStatus VSPackage yüklenmediği zaman gerçekleşmez - [#3835](https://github.com/NuGet/Home/issues/3835)

- Çözüm Geri Yükle ve Oluştur Geri Yükleme hala iletişim lerini gösterir - [#3789](https://github.com/NuGet/Home/issues/3789)

- NuGet.Clients çözüm yapısında VSSDK sürümünü yalıt - [#3890](https://github.com/NuGet/Home/issues/3890)

## <a name="links-to-github-issues-fixed-in-rtm"></a>RTM'de düzeltilen GitHub sorunlarına bağlantılar
[Sorunlar listesi 1](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RTM")  
[Sorunlar listesi 2](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC4")  
[Sorunlar listesi 3](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC3")  
[Sorunlar listesi 4](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC2")  
[Sorunlar listesi 5](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC")
