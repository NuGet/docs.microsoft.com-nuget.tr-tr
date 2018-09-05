---
title: NuGet 2.7 Sürüm Notları
description: NuGet bilinen sorunları, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr 2.7 Sürüm Notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 97d3e5f0238fd6947a54e5eb3229b89b6746f18c
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550971"
---
# <a name="nuget-27-release-notes"></a>NuGet 2.7 Sürüm Notları

[WebMatrix sürüm notları için NuGet 2.6.1](../release-notes/nuget-2.6.1-for-webmatrix.md) | [NuGet 2.7.1 sürüm notları](../release-notes/nuget-2.7.1.md)

NuGet 2.7 22 Ağustos 2013 tarihinde yayınlanmıştır.

## <a name="acknowledgements"></a>Onayları

Aşağıdaki harici Katkıda Bulunanlar, NuGet 2.7 önemli katkılar için teşekkür ederiz istiyoruz:

1. [Mike Roth](http://www.codeplex.com/site/users/view/mxrss) ([@mxrss](https://twitter.com/mxrss))
    - Lisans URL'si, paketler ve ayrıntı listeleme ayrıntılı gösterir.
2. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#1956](http://nuget.codeplex.com/workitem/1956) -developmentDependency özniteliğe eklemek `packages.config` ve paketi komutta yalnızca çalışma zamanı paketlerini içerecek şekilde kullanın
3. [Rafael Nicoletti](http://www.codeplex.com/site/users/view/tkrafael) ([@tkrafael](https://twitter.com/tkrafael))
    - Nuget.exe paketi komut yinelenen özellikler anahtar kaçının.
4. [Ben Phegan](http://www.codeplex.com/site/users/view/benphegan) ([@BenPhegan](https://twitter.com/benphegan))
    - [#2610](http://nuget.codeplex.com/workitem/2610) -200 makine önbellek boyutunu artırın.
5. [Slava Trenogin](http://www.codeplex.com/site/users/view/derigel) ([@derigel](https://twitter.com/derigel))
    - [#3217](http://nuget.codeplex.com/workitem/3217) -yanlış sekmede güncelleştirmeleri gösteren düzeltme NuGet iletişim
    - Düzeltme Project.TargetFramework ProjectManager içinde null olabilir
    - [#3248](http://nuget.codeplex.com/workitem/3248) -SharedPackageRepository FindPackage/FindPackagesById düzeltme üzerinde mevcut olmayan PackageId başarısız olur
6. [Kevin Boyle](http://www.codeplex.com/site/users/view/KevinBoyleRG) ([@kevfromireland](https://twitter.com/kevfromireland))
    - [#3234](http://nuget.codeplex.com/workitem/3234) -Nomad proje desteğini etkinleştir
7. [Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie) ([@corinblaikie](https://twitter.com/corinblaikie))
    - [#3252](http://nuget.codeplex.com/workitem/3252) -dosya mevcut değilse düzeltme anında iletme komutu başarısız çıkış kodu 0.
8. [Martin Veselý](http://www.codeplex.com/site/users/view/veselkamartin)
    - [#3226](http://nuget.codeplex.com/workitem/3226) -hata veritabanı projesi bir projeye başvuruda bulunduğunda BindingRedirect Ekle komutu.
9. [Miroslav Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos) ([@bajtos](https://twitter.com/bajtos))
    - [#2891](http://nuget.codeplex.com/workitem/2891) -joker karakter 'exclude' özniteliğinde yanlış ayrıştırma nuget.pack hata düzeltmesi.
10. [Justin Dearing](http://www.codeplex.com/site/users/view/zippy1981) ([@zippy1981](https://twitter.com/zippy1981))
     - [#3307](http://nuget.codeplex.com/workitem/3307) -hata `NuGet.targets` $(Platform) nuget.exe için paketler geri yüklenirken geçirmez.
11. [Brian Federici](http://www.codeplex.com/site/users/view/benerdin)
     - [#3294](http://nuget.codeplex.com/workitem/3294) -düzeltme hata dosyalarla aynı ada ancak sonuçta "Öğe zaten var." özel durum neden farklı büyük/küçük harf, ekleme izin nuget.exe paket komutu.
12. [Daniel Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino) ([@kzu](https://twitter.com/kzu))
     - [#2990](http://nuget.codeplex.com/workitem/2990) -sürüm Ekle özelliğini NetPortableProfile sınıfı.
13. [David Simner](https://www.codeplex.com/site/users/view/DavidSimner)
     - [#3460](https://nuget.codeplex.com/workitem/3460) -hata NullReferenceException, düzeltme requireApiKey = true ancak üst bilgisi X-NUGET-APIKEY mevcut değil
14. [Michael Friis](https://www.codeplex.com/site/users/view/friism) ([@friism](https://twitter.com/friism))
     - [#3278](https://nuget.codeplex.com/workitem/3278) -çalışan MonoDevelop doğru çalıştığından emin düzeltmeleri NuGet.Build hedef dosya
15. [Pranav Krishnamoorthy](https://www.codeplex.com/site/users/view/pranavkm) ([@pranav_km](https://twitter.com/pranav_km))
     - Geri yükleme komutu paralelleştirme artırarak performansı

## <a name="notable-features-in-the-release"></a>Sürümündeki önemli özelliklere

### <a name="package-restore-by-default-with-implicit-consent"></a>Varsayılan (ile tanımlanabilen) paket geri yükleme

NuGet 2.7 paket geri yükleme için yeni bir yaklaşım sunmaktadır ve ayrıca önemli hurdle yelken: paket geri yükleme onayı artık varsayılan olarak açıktır! Yeni yaklaşıma ve tanımlanabilen birleşimi paket geri yükleme senaryolarında büyük ölçüde basitleştirir.

#### <a name="implicit-consent"></a>Örtülü izin

NuGet sürümü ile 2.0 ve 2.1, 2.2, 2.5 ve 2.6, açıkça sırasında eksik paketleri indirmek NuGet izin vermek için gerekli kullanıcıları oluşturun. Bu onay sahipse değil, kullanıcı onayı verilen kadar oluşturmak paket geri yükleme etkin çözümler başarısız olacağı daha sonra açıkça, verilen.

NuGet 2.7 ile başlayarak, paket geri yükleme onayı varsayılan olarak kullanıcılara açıkça izin verirken açıktır *çıkma* istenirse, Visual Studio'da NuGet ayarlarında onay kutularını kullanarak, paket geri yükleme. Bu değişiklik için tanımlanabilen şu Masaüstü ortamlarında NuGet etkiler:

* Visual Studio 2013 Preview
* Visual Studio 2012
* Visual Studio 2010
* nuget.exe komut satırı yardımcı programı

#### <a name="automatic-package-restore-in-visual-studio"></a>Visual Studio'da otomatik paket geri yükleme

Paket geri yükleme açıkça çözüm için bile etkinleştirilmemişse NuGet 2.7 ile başlayarak, NuGet otomatik olarak eksik paketleri Visual Studio'da derleme sırasında indirir. Bu otomatik geri yükleme paketi Visual Studio'da bir proje veya çözümü oluşturduğunuzda, ancak MSBuild çağrılmadan önce'olmuyor. Bu, birkaç önemli avantajlar verir:

1. Daha fazla "NuGet paketi geri yüklemeyi etkinleştir" hareketi, çözümünüzde kullanmanız gerekir
1. Projeleri değiştirilmesine gerek yoktur ve NuGet paket geri yükleme etkinleştirildiğinden emin olmak için projenize değişiklik olmaz
1. Özellikler/MSBuild, MSBuild Imports dahil de dahil olmak üzere tüm NuGet paketlerini geri yüklenecek *önce* MSBuild çağrıldığında, sağlayarak özellikler/hedeflerin doğru yapı sırasında tanınan

Visual Studio'da paket otomatik geri yükleme kullanmak için yalnızca bir (iş) başında olması gerekir:

1. Giriş yapmazsa, `packages` klasörü

Atlamak için birkaç yolu vardır, `packages` kaynak denetiminden klasör. Daha fazla bilgi için [paketleri ve kaynak denetimi](../consume-packages/packages-and-source-control.md) konu.

Tüm kullanıcıları örtük olarak çalışırken paket otomatik geri yükleme onayı seçimi yaptıysanız, kolayca Visual Studio'da Paket Yöneticisi Ayarları aracılığıyla geri çevirebilirsiniz.

![Paket Yöneticisi Ayarları](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a>Komut satırından Basitleştirilmiş paket geri yükleme

NuGet 2.7 nuget.exe için yeni bir özellik sunar: `nuget.exe restore`

Bu yeni Restore komutu tüm paketleri tek bir komutla bir çözüm için'ın bir çözüm dosyası veya klasörü bağımsız değişken olarak kabul ederek kolayca geri yüklemenize olanak sağlar. Ayrıca, geçerli klasörde yalnızca tek bir çözüm olduğunda, bağımsız değişken yapılmamaktadır. Tek bir çözüm dosyasını (MySolution.sln) içeren klasörden aşağıdaki tüm iş anlamına gelir:

1. nuget.exe geri yükleme MySolution.sln
1. nuget.exe geri yükleme.
1. nuget.exe geri yükleme

Restore komutu, çözüm dosyasını açın ve çözüm içindeki tüm projeler bulun. Buradan, bunu bulabilirsiniz `packages.config` tüm projeleri ve bulunan tüm paketlerin geri yükleme dosyaları. Ayrıca bulunan çözüm düzeyinde paketleri geri yükler `.nuget\packages.config` dosya. Yeni Restore komutu hakkında daha fazla bilgi bulunabilir [komut satırı başvurusu](../tools/cli-ref-restore.md).

#### <a name="the-new-package-restore-workflow"></a>Yeni paket geri yükleme iş akışı

Yeni bir iş akışı tanıtan bu paket geri yükleme, bu değişiklikler hakkında heyecan duyuyoruz. Kaynak denetiminden paketlerinizi atlamak istiyorsanız, yalnızca tamamlama yoksa `packages` klasör. Açın ve çözümü visual Studio kullanıcılar otomatik olarak geri paketleri görürsünüz. Komut satırı derlemeleri için yalnızca çağırma `nuget.exe restore` çağırmadan önce `msbuild`. Artık "NuGet paketi geri yüklemeyi etkinleştir" hareketi, çözümünüzde kullanmayı unutmayın gerekmez ve biz artık projelerinizi derleme değiştirmek için değiştirmeniz gerekir. Ve bu da özellikle NuGet'ın en son özellik için eklenen içe aktarmalar için MSBuild içeri aktarmaları içeren paketler için daha gelişmiş bir deneyim verir [otomatik olarak içeri özellikler/hedefleri dosyaları](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files) \build klasöründen.

Kendimize yaptığımız iş yanı sıra, ayrıca bu yeni bir yaklaşım yuvarlamak önemli bazı iş ortaklarıyla çalışıyoruz. Biz somut zaman çizelgeleri aşağıdakilerden herhangi biri için henüz yoksa, ancak her yeni yaklaşıma bizim yaptığımız gibi heyecan ortağıdır.

* Team Foundation Service - bunlar çalıştığınız çağrısı tümleştirmek için `nuget.exe restore` varsayılan senaryoları oluşturun.
* Windows Azure Web siteleri - bunlar çalıştığınız, projenizi Azure'a gönderin ve izin vermek için `nuget.exe restore` web sitenizi oluşturulmadan önce çağrılır.
* TeamCity - bunlar güncelleştirdiğiniz kendi NuGet Yükleyicisi eklentisi için TeamCity 8.x
* AppHarbor - bunlar çalıştığınız için AppHarbor deponuza gönderin ve olanak `nuget.exe restore` çözümünüzü derleme önce çağrılır.

Her iş ortaklarının yukarıdaki nuget.exe kendilerine ait kopyasında kullanmanız gerekir ve çözümünüzde nuget.exe gerçekleştirmek zorunda kalmaz.

#### <a name="known-issues"></a>Bilinen Sorunlar

Nuget.exe geri yükleme ile ilk 2.7 Sürüm ile iki bilinen sorunlar vardı, ancak 6/9/2013 yönelik bir güncelleştirme ile'te düzeltilen [NuGet.CommandLine paket](http://www.nuget.org/packages/NuGet.CommandLine/).  Bu güncelleştirme ayrıca şurada bulunur [NuGet 2.7 İndirme sayfası](https://nuget.codeplex.com/releases/view/107605) CodePlex üzerinde.  Çalışan `nuget.exe update -self` en son sürüme güncelleştirir.

Sabit şöyleydi:

1. [Yeni paket geri yükleme üzerinde Mono SLN dosyasını kullanırken çalışmıyor](https://nuget.codeplex.com/workitem/3596)
1. [Yeni paket geri yükleme Wix projeleriyle çalışmıyor](https://nuget.codeplex.com/workitem/3598)

Ayrıca bir bilinen sorun olup yeni paket geri yükleme iş akışı yapabildiği [paket otomatik geri çalışmıyor bir çözüm klasörü altındaki projelerde](https://nuget.codeplex.com/workitem/3625). Nuget'te 2.7.1 Bu sorunu düzeltildi.

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a>Proje yeniden hedefleme ve yükseltme hataları/uyarıları oluşturma

Birden çok kez yeniden hedefleme veya projenize yükselttikten sonra NuGet paketlerinden bazıları düzgün olmayan bulabilirsiniz. Ne yazık ki, bu bir gösterge yoktur ve ardından yoktur hiçbir kılavuz ele nasıl. NuGet 2.7 ile artık bazı Visual Studio olayları yeniden hedeflendi veya projenizi yüklü olan NuGet paketlerinizi etkileyen bir biçimde yükseltilmiş tanımak için kullanırız.

Paketlerinizi birini yeniden hedefleme veya yükseltme tarafından etkilendi belirlersek anında derleme hataları bildirmek için hazırladığımız. Anında derleme hatası yanı sıra, biz de kalıcı bir `requireReinstallation="true"` bayrağını, `packages.config` dosya Visual Studio'da yeniden hedefleme tarafından etkilenen ve sonraki her tüm paketleri oluşturmak için yükseltmek için bu paketleri derleme uyarıları.

NuGet etkilenen paketleri yeniden yüklemek için otomatik eylem alamaz ve bu gösterimi umuyoruz uyarı Yardım yönlendirecektir olsa da paket yeniden gerektiğinde keşfedin. Ayrıca üzerinde çalışılmaktadır [paketini yeniden Rehber belgeleri](../consume-packages/reinstalling-and-updating-packages.md) bu hata iletileri için doğrudan.

### <a name="nuget-configuration-defaults"></a>NuGet yapılandırma Varsayılanları

Birçok şirket, NuGet dahili olarak kullanarak, ancak iç paket kaynakları nuget.org yerine kullanılacak geliştiricileri erişeceğinizi gösteren sabit bir süre beklendiğinden. NuGet 2.7 için belirtilecek makine genelinden Varsayılanları sağlayan bir yapılandırma Varsayılanları özelliği sunar:

1. Etkin paket kaynakları
1. Kayıtlı ancak devre dışı paket kaynaklarını
1. Varsayılan nuget.exe anında iletme kaynağı

Her birinde bulunan bir dosya içinde artık yapılandırılabilir `%ProgramData%\NuGet\NuGetDefaults.Config`. Bu yapılandırma dosyasını, paket kaynaklarını belirtir sonra varsayılan nuget.org paket kaynağı otomatik olarak kaydedilmez ve dışındaki `NuGetDefaults.Config` yerine kaydedilir.

Bu özelliği kullanmak için gerekli olmasa da dağıtmak için şirketlerin bekliyoruz `NuGetDefaults.Config` Grup İlkesi kullanarak dosyaları.

*Bu özellik, bir geliştiricinin NuGet ayarlarından kaldırılmış bir paket kaynağı hiçbir zaman neden olacağını unutmayın. Geliştirici NuGet zaten kullandı ve bu nedenle nuget.org paket kaynağı olan anlamına kayıtlı, oluşturulmasından sonra kaldırılmaz bir `NuGetDefaults.Config` dosya.*

Bkz: [NuGet yapılandırma varsayılanları](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file) bu özellik hakkında daha fazla bilgi.

### <a name="renaming-the-default-package-source"></a>Varsayılan paket kaynağı yeniden adlandırma

NuGet, her zaman "nuget.org için işaret NuGet resmi paket kaynağı" olarak adlandırılan bir varsayılan paket kaynağı kaydettirildi. Bu ada ayrıntılı ve de burada bu gerçekten işaret ettiği belirtmediniz. İki sorunları gidermek için bu paket kaynağının yalnızca "nuget.org'da" kullanıcı arabiriminde değiştirdiniz. Paket kaynağı URL'si aynı zamanda "www." içerecek şekilde değiştirildi önek. NuGet 2.7 kullandıktan sonra mevcut "NuGet resmi paket kaynağı" otomatik olarak "nuget.org" ad olarak güncelleştirilir ve "<https://www.nuget.org/api/v2/>" URL olarak.

### <a name="performance-improvements"></a>Performans Geliştirmeleri

İçinde daha küçük bellek Ayak izi, daha az disk kullanımı ve daha hızlı paket yükleme verecek 2.7 bazı performans geliştirmesi yaptık. Ayrıca, genel yükü azaltır OData tabanlı Özet akışlarını daha akıllı sorgular hale.

### <a name="new-extensibility-apis"></a>Yeni genişletilebilirlik API'leri

Önceki sürümlerde eksik işlevleri boşluğu doldurmak için genişletilebilirlik hizmetlerimiz için bazı yeni API ekledik.

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

Bu özellik tarafından katkıda bulunulan [Adam Ralph](https://twitter.com/adamralph) ve yalnızca geliştirme sırasında kullanılan bağımlılık süresi ve Paket bağımlılıklarını gerektirmeyen bildirmek paket yazarlarının verir. Ekleyerek bir `developmentDependency="true"` öznitelik pakete `packages.config`, `nuget.exe pack` artık o paketi bir bağımlılık olarak dahil edilir.

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a>Windows Phone için Visual Studio 2010 Express desteği kaldırıldı

2.7 yeni paket geri yükleme modelinde ana NuGet VSPackage farklı olan yeni bir VSPackage tarafından uygulanır. Teknik bir sorun nedeniyle, bu yeni VSPackage içinde düzgün çalışmıyor *Visual Studio 2010 Express için Windows Phone* SKU sizinle aynı kod tabanını diğer paylaşıyoruz Visual Studio'SKU ' ları desteklenir. Bu nedenle, NuGet 2.7 ile başlayarak, biz desteği atar *Visual Studio 2010 Express için Windows Phone* yayımlanmış uzantı. Destek *Visual Studio 2010 Express Web* hala Visual Studio uzantısı galeride yayımlanmış uzantı birincil dahildir.

Biz kaç geliştiricilerin yine de bu sürümü Visual Studio'nun NuGet kullandığını emin değilseniz bu yana, biz bu kullanıcılar için özel olarak ayrı bir Visual Studio uzantısı yayımlama ve CodePlex (Visual Studio uzantı Galerisi yerine) yayımlama . Bu sizi etkiliyorsa ancak bu uzantı kullanmaya devam etmek planlamıyor Codeplex'te bir sorun kaydederek bize bildirin.

NuGet Paket Yöneticisi (Visual Studio 2010 Express için Windows Phone için) indirmek için şurayı ziyaret edin [2.7 NuGet indirir](https://nuget.codeplex.com/releases/view/107605) sayfası.

### <a name="bug-fixes"></a>Hata Düzeltmeleri

Bu özelliklerin yanı sıra bu NuGet sürümü ayrıca diğer birçok hata düzeltmeleri içerir. Sürümünde giderilen 97 toplam sorunlar oluştu. Tam bir listesi için iş öğeleri NuGet 2.7, lütfen görünümü sabit [bu sürüm için NuGet sorun İzleyicisi](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all).
