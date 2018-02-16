---
title: "NuGet 2.7 Sürüm Notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet bilinen sorunları, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere 2.7 için sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 2.7 Sürüm Notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 43638626661ae034bb0a1cc28958a2e2929f047f
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/14/2018
---
# <a name="nuget-27-release-notes"></a>NuGet 2.7 Sürüm Notları

[WebMatrix sürüm notları için NuGet 2.6.1](../release-notes/nuget-2.6.1-for-webmatrix.md) | [NuGet 2.7.1 sürüm notları](../release-notes/nuget-2.7.1.md)

NuGet 2.7 22 Ağustos 2013'te yayımlanmıştır.

## <a name="acknowledgements"></a>Katkıda Bulunanlar

Aşağıdaki dış Katkıda Bulunanlar, önemli ölçüde katkıda NuGet 2.7 için teşekkür ederiz ister misiniz:

1. [Mike Roth](http://www.codeplex.com/site/users/view/mxrss) ([@mxrss](https://twitter.com/mxrss))
    - Paketler ve ayrıntı listeleme zaman ayrıntılı lisans URL'sini gösterir.
1. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#1956](http://nuget.codeplex.com/workitem/1956) -developmentDependency özniteliğe eklemek `packages.config` ve yalnızca çalışma zamanı paketleri dahil etmek paketi komutunu kullanın
1. [Rafael Nicoletti](http://www.codeplex.com/site/users/view/tkrafael) ([@tkrafael](https://twitter.com/tkrafael))
    - Yinelenen özellikler anahtar nuget.exe paketi komutta kaçının.
1. [Ben Phegan](http://www.codeplex.com/site/users/view/benphegan) ([@BenPhegan](https://twitter.com/benphegan))
    - [#2610](http://nuget.codeplex.com/workitem/2610) -200 makine önbellek boyutunu artırın.
1. [Slava Trenogin](http://www.codeplex.com/site/users/view/derigel) ([@derigel](https://twitter.com/derigel))
    - [#3217](http://nuget.codeplex.com/workitem/3217) -yanlış sekmede güncelleştirmeleri gösteren düzeltme NuGet iletişim
    - Düzeltme Project.TargetFramework ProjectManager içinde null olabilir
    - [#3248](http://nuget.codeplex.com/workitem/3248) - Fix SharedPackageRepository FindPackage/FindPackagesById will fail on non-existent packageId
1. [Kevin Boyle](http://www.codeplex.com/site/users/view/KevinBoyleRG) ([@kevfromireland](https://twitter.com/kevfromireland))
    - [#3234](http://nuget.codeplex.com/workitem/3234) -Nomad proje desteğini etkinleştir
1. [Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie) ([@corinblaikie](https://twitter.com/corinblaikie))
    - [#3252](http://nuget.codeplex.com/workitem/3252) -düzeltme itme komutu başarısız çıkış kodu 0 dosya yok olduğunda.
1. [Martin Veselý](http://www.codeplex.com/site/users/view/veselkamartin)
    - [#3226](http://nuget.codeplex.com/workitem/3226) -proje veritabanı projesi başvurduğunda Ekle BindingRedirect komutuyla düzeltme hata.
1. [Miroslav Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#2891](http://nuget.codeplex.com/workitem/2891) -joker 'dışlama' özniteliğinde yanlış ayrıştırma nuget.pack, düzeltme hata.
1. [Justin Dearing](http://www.codeplex.com/site/users/view/zippy1981) ([@zippy1981](https://twitter.com/zippy1981))
    - [#3307](http://nuget.codeplex.com/workitem/3307) -düzeltme hata `NuGet.targets` $(Platform) nuget.exe için paketler geri yüklerken iletmez.
1. [Brian Federici](http://www.codeplex.com/site/users/view/benerdin)
    - [#3294](http://nuget.codeplex.com/workitem/3294) -düzeltme hatada sonunda "Öğe zaten var." özel duruma neden farklı büyük/küçük harf, ancak aynı adı dosyalarıyla ekleme izin nuget.exe paket komutu.
1. [Daniel Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino) ([@kzu](https://twitter.com/kzu))
    - [#2990](http://nuget.codeplex.com/workitem/2990) -NetPortableProfile sınıfına sürüm ekleme özelliği.
1. [David Simner](https://www.codeplex.com/site/users/view/DavidSimner)
    - [#3460](https://nuget.codeplex.com/workitem/3460) -hata NullReferenceException varsa düzeltme requireApiKey = true ancak üst bilgisi X-NUGET-apikey ile yapılan mevcut değil
1. [Michael Friis](https://www.codeplex.com/site/users/view/friism) ([@friism](https://twitter.com/friism))
    - [#3278](https://nuget.codeplex.com/workitem/3278) -MonoDevelop üzerinde doğru şekilde çalışmasını giderir NuGet.Build hedefleri dosya
1. [Pranav Krishnamoorthy](https://www.codeplex.com/site/users/view/pranavkm) ([@pranav_km](https://twitter.com/pranav_km))
    - Geri yükleme komutu paralelleştirme artırarak performansı

## <a name="notable-features-in-the-release"></a>Sürümdeki dikkat çekici özellikleri

### <a name="package-restore-by-default-with-implicit-consent"></a>Paket geri yüklemesi varsayılan (olarak tanımlanabilen)

NuGet 2.7 paket geri yükleme için yeni bir yaklaşım sunmaktadır ve ayrıca büyük hurdle üstesinden gelen: paket geri yükleme izni artık varsayılan olarak açıktır! Yeni bir yaklaşım ve tanımlanabilen birleşimi paket geri yükleme senaryoları büyük ölçüde basitleştirir.

#### <a name="implicit-consent"></a>Tanımlanabilen

NuGet sürümleriyle 2.0, 2.1, 2.2, 2.5 ve 2.6, açıkça NuGet sırasında eksik paketleri indirmesine izin vermek için gerekli kullanıcıları oluşturun. Bu onayı sahipse değil, kullanıcıya izin verilip kadar oluşturmak paket geri yükleme etkin çözümleri başarısız olacağı sonra açıkça, verilmiş.

NuGet 2.7 ile başlayarak, paket geri yükleme izni üzerinde varsayılan olarak kullanıcılara açıkça izin verirken olan *çıkma* istenirse, Visual Studio'da NuGet ayarlarında onay kutusunu kullanarak, paket geri yükleme. Bu değişiklik tanımlanabilen için NuGet aşağıdaki ortamlarda etkiler:

* Visual Studio 2013 Preview
* Visual Studio 2012
* Visual Studio 2010
* nuget.exe Command-Line Utility

#### <a name="automatic-package-restore-in-visual-studio"></a>Visual Studio'da otomatik paket geri yüklemesi

Paket geri yüklemesi için çözüm açıkça etkinleştirilmedi olsa bile NuGet 2.7 ile başlayarak, NuGet otomatik olarak eksik paketleri Visual Studio'da derleme sırasında indirir. Bu otomatik geri yükleme paketini Visual Studio'da bir proje veya çözüm oluşturduğunuzda, ancak MSBuild çağrılmadan önce gerçekleşir. Bu, birkaç önemli avantajlar verir:

1. Başka çözümünüzü üzerinde "Etkinleştirme NuGet paket geri yükleme" hareketi kullanmanıza gerek
1. Projeleri değiştirilmesine gerek yoktur ve NuGet paket geri yüklemesi etkinleştirildiğinden emin olmak için projenize değişiklik olmaz
1. MSBuild içeri aktarmalar özellik/hedef dosyaları için dahil olanlar dahil olmak üzere tüm NuGet paketleri geri *önce* MSBuild çağrıldığında, bu özellik/hedefleri düzgün derleme sırasında tanınan sağlama

Visual Studio'da otomatik paket geri yükleme kullanabilmeniz için yalnızca birinde () eylem yapılması gerekir:

1. İade değil, `packages` klasörü

Atlamak için çeşitli yolları vardır, `packages` kaynak denetiminden klasör. Daha fazla bilgi için bkz: [paketler ve kaynak denetimi](../consume-packages/packages-and-source-control.md) konu.

Tüm kullanıcılar örtük olarak çalışırken otomatik paket geri yükleme izni seçti, kolayca Visual Studio'da Paket Yöneticisi Ayarları aracılığıyla iptal edilebilir.

![Paket yönetimi ayarları](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a>Komut satırından Basitleştirilmiş paket geri yüklemesi

NuGet 2.7 nuget.exe için yeni bir özellik sunar: `nuget.exe restore`

Bu yeni Restore komutu kolayca tüm paketleri tek bir komutla bir çözüm için çözüm dosya veya klasör bağımsız değişken olarak kabul ederek geri yüklemenize olanak sağlar. Ayrıca, geçerli klasörde yalnızca tek bir çözüm olduğunda bu bağımsız değişken uygulanmaktadır. Aşağıdaki tüm tek çözüm dosyasını (MySolution.sln) içeren bir klasörden iş anlamına gelir:

1. nuget.exe restore MySolution.sln
1. nuget.exe restore .
1. nuget.exe restore

Restore komutu, çözüm dosyasını açın ve tüm projeleri çözüm içinde bulun. Buradan, onu bulacaksınız `packages.config` dosyaları her proje ve geri yükleme tüm paketler bulunamadı. Ayrıca bulunan çözüm düzeyi paketleri geri yükler `.nuget\packages.config` dosya. Yeni Restore komutu hakkında daha fazla bilgi bulunabilir [komut satırı başvurusu](../tools/cli-ref-restore.md).

#### <a name="the-new-package-restore-workflow"></a>Yeni paket geri yükleme iş akışı

Yeni bir iş akışı tanıtır gibi biz paket geri yükleme, bu değişiklikler hakkında Mutluluk duyuyoruz. Kaynak denetiminden paketlerinizi atlamak istiyorsanız, yalnızca yürütme yok `packages` klasör. Açın ve çözümü derleme visual Studio kullanıcılar otomatik olarak geri paketleri görürsünüz. Komut satırı derlemeleri için basitçe çağırma `nuget.exe restore` çağırmadan önce `msbuild`. Artık, çözüm üzerinde "Etkinleştirme NuGet paket geri yükleme" hareketi kullanmayı unutmayın gerek ve biz artık projelerinizi yapı alter değiştirmeniz gerekir. Ve bu da özellikle için NuGet son özelliği aracılığıyla eklenen içeri aktarmalar için MSBuild içeri aktarmaları içeren paketler için daha gelişmiş bir deneyim verir [otomatik olarak içeri aktarma özellik/hedefleri dosyaları](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files) \build klasöründen.

Biz kendisini çalışmanın yanı sıra, aynı zamanda bu yeni bir yaklaşım yuvarlanacak bazı önemli iş ortaklarıyla çalışıyoruz. Biz somut zaman çizelgelerini bunları herhangi biri için henüz sunulmadı, ancak her bir ortak yeni yaklaşımı hakkında duyuyoruz olarak Çoğalması.

* Team Foundation Service - bunlar çalıştığınız çağrısı tümleştirmek için `nuget.exe restore` senaryoları varsayılan derleme.
* Windows Azure Web siteleri - bunlar çalıştığınız, projenizin Azure'a gönderin ve izin vermek için `nuget.exe restore` web sitenizi oluşturulmadan önce çağrılır.
* TeamCity - bunlar güncelleştirdiğiniz kendi NuGet Yükleyicisi eklentisi için TeamCity 8.x
* AppHarbor - bunlar çalıştığınız, depodaki AppHarbor için anında iletme ve izin vermek için `nuget.exe restore` çözümünüzü yapıdır önce çağrılır.

Her iş ortaklarının yukarıdaki nuget.exe kendi kopyasını kullanırsınız ve nuget.exe çözümünüzde gerçekleştirmek zorunda kalmaz.

#### <a name="known-issues"></a>Bilinen Sorunlar

İlk 2.7 sürümüyle nuget.exe geri yükleme ile ilgili iki bilinen sorunlar vardı, ancak 6/9/2013 için bir güncelleştirme ile düzeltilen [NuGet.CommandLine paket](http://www.nuget.org/packages/NuGet.CommandLine/).  Bu güncelleştirme de kullanılabilir [NuGet 2.7 İndirme sayfası](https://nuget.codeplex.com/releases/view/107605) CodePlex üzerinde.  Çalışan `nuget.exe update -self` en son sürümüne güncelleştirir.

Sabit olan:

1. [Yeni paket geri yüklemesi üzerinde Mono SLN dosyası kullanıldığında çalışmıyor](https://nuget.codeplex.com/workitem/3596)
1. [Yeni paket geri yüklemesi Wix projelerle çalışmamaktadır.](https://nuget.codeplex.com/workitem/3598)

Ayrıca bir bilinen sorun olmadığından yeni paket geri yükleme iş akışı yapabildiği [otomatik paketi geri yüklemesi çalışmıyor çözüm klasörünün altında projeleri için](https://nuget.codeplex.com/workitem/3625). Bu sorun, NuGet 2.7.1 giderilmiştir.

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a>Projeyi yeniden hedefleme ve yükseltme hatalar/uyarılar oluştur

Birçok kez yeniden hedefleme veya projenizi yükselttikten sonra bazı NuGet paketleri düzgün olmayan bulun. Ne yazık ki, bu bir gösterge yoktur ve ardından herhangi bir yönerge yoktur ele nasıl. NuGet 2.7 ile şimdi bazı Visual Studio olayları, güncellendiyse veya projenizin yüklü NuGet paketlerinizi etkiler şekilde yükseltme tanımak için kullanırız.

Paketlerinizi birini yeniden hedefleme veya yükseltme tarafından etkilendi belirlersek biz size bildirmek için hemen derleme hataları üretmek. Hemen derleme hatası ek olarak, biz de kalıcı bir `requireReinstallation="true"` içinde bayrak, `packages.config` dosyasını Visual Studio'da yeniden hedefleme tarafından etkilenen ve daha sonraki tüm paketleri oluşturmak için Yükselt bu paketleri için derleme uyarıları.

NuGet etkilenen paketler yeniden yüklemek için otomatik eylem alamıyor, bu göstergesi umuyoruz ve uyarı Yardım rehberlik sağlar ancak paketler yeniden gerektiğinde bulur. Ayrıca üzerinde çalıştığımız [paketini yeniden yükleme kılavuzu belgelerine](../consume-packages/reinstalling-and-updating-packages.md) bu hata iletileri için sizi yönlendirir.

### <a name="nuget-configuration-defaults"></a>NuGet yapılandırması varsayılan

Birçok şirketin NuGet dahili olarak kullanıyorsanız, ancak nuget.org yerine iç paket kaynaklarını kullanmak için geliştiriciler yönlendirmede sabit bir süre beklendiğinden. NuGet 2.7 için belirtilmesi makine genelinde Varsayılanları sağlayan bir yapılandırma varsayılanlarını özelliği sunar:

1. Etkin paket kaynaklarının
1. Kayıtlı ancak devre dışı bırakılan paket kaynaklarını
1. Varsayılan nuget.exe itme kaynağı

Bunların her biri konumunda bulunan bir dosya içinde artık yapılandırılabilir `%ProgramData%\NuGet\NuGetDefaults.Config`. Bu yapılandırma dosyası paket kaynaklarını belirtir sonra varsayılan nuget.org paket kaynağı otomatik olarak kaydedilmez ve Listedekilerin `NuGetDefaults.Config` yerine kaydedilir.

Bu özelliği kullanmak için gerekli olmasa da, şirketler dağıtmak için bekliyoruz `NuGetDefaults.Config` Grup İlkesi kullanarak dosyaları.

*Bu özellik, bir geliştiricinin NuGet ayarlarından kaldırılmış için bir paket kaynağı hiçbir zaman neden olacak unutmayın. Geliştirici NuGet zaten kullandı ve bu yüzden nuget.org paket kaynağı varsa, yani kayıtlı oluşturulmasından sonra kaldırılmadan olmaz bir `NuGetDefaults.Config` dosyası.*

Bkz: [NuGet yapılandırma varsayılanları](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file) bu özellik hakkında daha fazla bilgi için.

### <a name="renaming-the-default-package-source"></a>Varsayılan paket kaynağı yeniden adlandırma

NuGet her zaman "için nuget.org işaret NuGet resmi bir paket kaynağı" olarak adlandırılan varsayılan paket kaynağına kaydettirildi. Bu ad ayrıntılı ve ayrıca burada da gerçekte işaret eden belirtin alamadık. Bu iki sorunları gidermek için yalnızca "nuget.org" kullanıcı arabiriminde bu paket kaynağına değiştirdiniz. Paket kaynağının URL'sini de "www." içerecek şekilde değiştirildi. önek. NuGet 2.7 kullandıktan sonra varolan "NuGet resmi bir paket kaynağı" otomatik olarak ad olarak "nuget.org" ve "https://www.nuget.org/api/v2/" URL olarak güncelleştirilir.

### <a name="performance-improvements"></a>Performans Geliştirmeleri

Biz, daha küçük bellek alanını, daha az disk kullanımı ve daha hızlı paket yükleme sunacak 2.7 bazı performans geliştirmesi yapılan. Biz de akıllı sorguları, genel yükü azaltır OData tabanlı akışlarına yapılan.

### <a name="new-extensibility-apis"></a>Yeni genişletilebilirlik API

Genişletilebilirlik hizmetlerimizle eksik işlevler boşluğu önceki sürümlerde doldurmak için bazı yeni API'leri eklediğimiz.

#### <a name="ivspackageinstallerservices"></a>IVsPackageInstallerServices

    ```cs
    // Checks if a NuGet package with the specified Id and version is installed in the specified project.
    bool IsPackageInstalledEx(Project project, string id, string versionString);

    // Get the list of NuGet packages installed in the specified project.
    IEnumerable<IVsPackageMetadata> GetInstalledPackages(Project project);
    ```

#### <a name="ivspackageinstaller"></a>IVsPackageInstaller

    ```cs
    // Installs one or more packages that exist on disk in a folder defined in the registry.
    void InstallPackagesFromRegistryRepository(string keyName, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);

    // Installs one or more packages that are embedded in a Visual Studio Extension Package.
    void InstallPackagesFromVSExtensionRepository(string extensionId, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);
    ```

### <a name="development-only-dependencies"></a>Yalnızca geliştirme bağımlılıkları

Bu özellik tarafından katkıda bulunan [Adam Ralph](https://twitter.com/adamralph) ve yalnızca geliştirme sırasında kullanılan bağımlılıkları süresi ve Paket bağımlılıklarını gerektirmeyen bildirmek paket belirtmelerini sağlar. Ekleyerek bir `developmentDependency="true"` özniteliği pakete `packages.config`, `nuget.exe pack` artık o paketi bir bağımlılık olarak dahil edilir.

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a>Windows Phone için Visual Studio 2010 Express için destek kaldırılmıştır

2.7 yeni paket geri yükleme modelinde ana NuGet VSPackage farklı olan yeni bir VSPackage tarafından uygulanır. Teknik bir sorun nedeniyle, bu yeni VSPackage içinde düzgün çalışmıyor *Visual Studio 2010 Express için Windows Phone* SKU aynı kod tabanını diğer biz paylaşımı şeklinde desteklenen Visual Studio SKU'ları. Bu nedenle, NuGet 2.7 ile başlayarak, biz desteği atar *Visual Studio 2010 Express için Windows Phone* yayımlanan uzantı. Desteği *için Visual Studio 2010 Express Web* Visual Studio uzantı Galerisi'ne yayımlanan birincil uzantısı hala bulunmaktadır.

Biz kaç geliştiriciler NuGet bu sürümü/içinde Visual Studio sürümü kullanmaya devam emin değilseniz olduğundan, biz bu kullanıcılar için özel olarak ayrı bir Visual Studio uzantı yayımlama ve CodePlex (Visual Studio uzantı Galerisi yerine) yayımlama . Bu, etkiler, ancak bu uzantı korumak için devam edin planlıyoruz yok Lütfen bize CodePlex üzerinde bir sorun dosyalama tarafından bildirin.

NuGet Paket Yöneticisi (Visual Studio 2010 Express için Windows Phone için) indirmek için şurayı ziyaret edin [NuGet 2.7 indirmeleri](https://nuget.codeplex.com/releases/view/107605) sayfası.

### <a name="bug-fixes"></a>Hata Düzeltmeleri

Bu özelliklerine ek olarak, bu sürümü NuGet, diğer birçok hata düzeltmeleri de içerir. Sürümde ele 97 toplam sorunları vardı. Tam bir listesi için iş öğeleri NuGet 2.7 içinde lütfen Görünüm sabit [NuGet sorun İzleyicisi bu sürüm için](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all).
