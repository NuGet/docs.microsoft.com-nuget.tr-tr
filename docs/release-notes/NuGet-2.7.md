---
title: NuGet 2,7 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 2,7 sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 70600e3c563e357663b4a2f24139d2fc25f75fdf
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780394"
---
# <a name="nuget-27-release-notes"></a>NuGet 2,7 sürüm notları

[WebMatrix Için NuGet 2.6.1 sürüm notları](../release-notes/nuget-2.6.1-for-webmatrix.md)  |  [NuGet 2.7.1 sürüm notları](../release-notes/nuget-2.7.1.md)

NuGet 2,7, 22 Ağustos 2013 tarihinde yayınlandı.

## <a name="acknowledgements"></a>Teşekkürler

NuGet 2,7 ' e yönelik önemli katkılarına yönelik olarak aşağıdaki dış katkıda bulunanlar için teşekkür ederiz:

1. [Mike Roth](http://www.codeplex.com/site/users/view/mxrss) ( [@mxrss](https://twitter.com/mxrss) )
    - Paket listelenirken ve ayrıntı ayrıntılandırılan lisans URL 'sini göster.
2. [Adam Canph](http://www.codeplex.com/site/users/view/adamralph) ( [@adamralph](https://twitter.com/adamralph) )
    - [#1956](http://nuget.codeplex.com/workitem/1956) - `packages.config` yalnızca çalışma zamanı paketlerini dahil etmek için geliştirme ve paketleme komutunda kullanın
3. [Rafael Nicoletti](http://www.codeplex.com/site/users/view/tkrafael) ( [@tkrafael](https://twitter.com/tkrafael) )
    - nuget.exe Pack komutunda yinelenen özellikler anahtarından kaçının.
4. [Ben Phegan](http://www.codeplex.com/site/users/view/benphegan) ( [@BenPhegan](https://twitter.com/benphegan) )
    - [#2610](http://nuget.codeplex.com/workitem/2610) -makine önbelleği boyutunu 200 olarak arttırın.
5. [Slava Trenogin](http://www.codeplex.com/site/users/view/derigel) ( [@derigel](https://twitter.com/derigel) )
    - [#3217](http://nuget.codeplex.com/workitem/3217) -güncelleştirmeleri yanlış sekmede gösteren NuGet iletişim kutusunu düzeltir
    - Projeyi düzeltir. TargetFramework, ProjectManager 'da null olabilir
    - var olmayan PackageID 'de [#3248](http://nuget.codeplex.com/workitem/3248) -SharedPackageRepository findpackage/Findpackagesbyıd başarısız olacak
6. [Kevin boyle](http://www.codeplex.com/site/users/view/KevinBoyleRG) ( [@kevfromireland](https://twitter.com/kevfromireland) )
    - [#3234](http://nuget.codeplex.com/workitem/3234) -Nomad projesi desteğini etkinleştir
7. [Corin Blaikie](http://www.codeplex.com/site/users/view/corinblaikie) ( [@corinblaikie](https://twitter.com/corinblaikie) )
    - dosya mevcut olmadığında, [#3252](http://nuget.codeplex.com/workitem/3252) -Push komutu 0 çıkış koduyla başarısız oluyor.
8. [MARTIN Veselý](http://www.codeplex.com/site/users/view/veselkamartin)
    - [#3226](http://nuget.codeplex.com/workitem/3226) , bir proje bir veritabanı projesine başvurduğunda Add-BindingRedirect komutuyla hatayı düzeltir.
9. [MIROSLAV Bajtos](http://www.codeplex.com/site/users/view/miroslavbajtos) ( [@bajtos](https://twitter.com/bajtos) )
    - [#2891](http://nuget.codeplex.com/workitem/2891) -' exclude ' özniteliğinde hatalı joker karakter ayrıştırma hata ayıklama hatası düzeltildi.
10. [Bağımsız](http://www.codeplex.com/site/users/view/zippy1981) ( [@zippy1981](https://twitter.com/zippy1981) )
     - [#3307](http://nuget.codeplex.com/workitem/3307) -hata giderme `NuGet.targets` , paketleri geri yüklerken nuget.exe $ (Platform) öğesini geçirmez.
11. [Brian Federbir](http://www.codeplex.com/site/users/view/benerdin)
     - [#3294](http://nuget.codeplex.com/workitem/3294) -aynı ada ancak büyük küçük harflere sahip dosya eklemeye izin veren nuget.exe paket komutunda hata düzeltildi, sonuçta "öğe zaten var" özel durumuna neden olur.
12. [Daniel Cazzulino](http://www.codeplex.com/site/users/view/dcazzulino) ( [@kzu](https://twitter.com/kzu) )
     - [#2990](http://nuget.codeplex.com/workitem/2990) -NetPortableProfile sınıfına sürüm özelliği ekleyin.
13. [David Simner](https://www.codeplex.com/site/users/view/DavidSimner)
     - [#3460](https://nuget.codeplex.com/workitem/3460) -requireapikey = true olduğunda hata NullReferenceException hatası, ancak X-NUGET-apikey üst bilgisi yok
14. [Michael Fri,](https://www.codeplex.com/site/users/view/friism) ( [@friism](https://twitter.com/friism) )
     - [#3278](https://nuget.codeplex.com/workitem/3278) -NuGet. Build hedef dosyasını, MonoDevelop üzerinde doğru çalışacak şekilde düzeltir
15. [Pranav Krishnamoorthy](https://www.codeplex.com/site/users/view/pranavkm) ( [@pranav_km](https://twitter.com/pranav_km) )
     - Paralelleştirme arttırılarak geri yükleme komutunun performansını artırma

## <a name="notable-features-in-the-release"></a>Yayındaki önemli özellikler

### <a name="package-restore-by-default-with-implicit-consent"></a>Varsayılan olarak paket geri yükleme (örtük onay ile)

NuGet 2,7, paket geri yükleme için yeni bir yaklaşım sunar ve ayrıca büyük bir aceden büyük bir zarar verir: paket geri yükleme onayı artık varsayılan olarak açık! Yeni yaklaşımın birleşimi ve örtük onay, paket geri yükleme senaryolarını büyük ölçüde basitleştirir.

#### <a name="implicit-consent"></a>Örtük onay

NuGet sürümleri 2,0, 2,1, 2,2, 2,5 ve 2,6 sayesinde, kullanıcıların derleme sırasında eksik paketleri indirmesini, NuGet 'e açıkça izin vermek için ihtiyacı vardır. Bu onay açıkça verilmemişse, paket geri yükleme özelliği etkinleştirilmiş olan çözümler, Kullanıcı izin verene kadar derlemeyebilir.

NuGet 2,7 ' den başlayarak, paket geri yükleme onayı varsayılan olarak açık olur, ancak istenirse, NuGet 'in Visual Studio 'daki ayarlarındaki onay kutusu kullanılarak, istenirse paket geri yükleme *devre dışı olarak devre dışı* . Bu örtük onay değişikliği, aşağıdaki ortamlarda NuGet 'i etkiler:

* Visual Studio 2013 Preview
* Visual Studio 2012
* Visual Studio 2010
* nuget.exe Command-Line yardımcı programı

#### <a name="automatic-package-restore-in-visual-studio"></a>Visual Studio 'da otomatik paket geri yükleme

NuGet 2,7 ' den başlayarak, çözüm için paket geri yüklemesi açıkça etkinleştirilmediği halde NuGet, Visual Studio 'da derleme sırasında eksik paketleri otomatik olarak indirirler. Bu otomatik paket geri yükleme, Visual Studio 'da bir proje veya çözüm oluşturduğunuzda, ancak MSBuild çağrılmadan önce gerçekleşir. Bu, birkaç önemli avantajı verir:

1. Çözümünüzde "NuGet paketini geri yüklemeyi etkinleştir" hareketini kullanmaya gerek yoktur
1. Projenin değiştirilmesi gerekmez ve paket geri yüklemenin etkinleştirildiğinden emin olmak için NuGet projenizde değişiklik yapamaz
1. Props/targets dosyaları için MSBuild içeri aktarmaları dahil olanlar da dahil olmak üzere tüm NuGet paketleri, MSBuild çağrılmadan *önce* , bu props/hedeflerin derleme sırasında düzgün şekilde tanınmasını sağlamak için geri yüklenecek

Visual Studio 'da otomatik paket geri yüklemeyi kullanabilmek için yalnızca bir (ın) eylemde olması gerekir:

1. Klasörünüzü iade etme `packages`

Kaynak denetiminden klasörünüzü atlamak için birkaç yol vardır `packages` . Daha fazla bilgi için bkz. [paketler ve kaynak denetimi](../consume-packages/packages-and-source-control.md) konusu.

Tüm kullanıcılar örtük olarak otomatik paket geri yükleme onayını kabul ettiğinde, Visual Studio 'da Paket Yöneticisi ayarları aracılığıyla kolayca gezinebilirsiniz.

![Paket Yöneticisi ayarları](./media/NuGet-2.7/package-manager-settings.png)

#### <a name="simplified-package-restore-from-the-command-line"></a>Command-Line 'ten Basitleştirilmiş paket geri yükleme

NuGet 2,7 nuget.exe yeni bir özellik sunar: `nuget.exe restore`

Bu yeni geri yükleme komutu, bir çözüm dosyasını veya klasörünü bağımsız değişken olarak kabul ederek tek bir komutla bir çözüme yönelik tüm paketleri kolayca geri yüklemenize olanak tanır. Ayrıca, bu bağımsız değişken geçerli klasörde yalnızca tek bir çözüm varsa kapsanır. Yani, tek bir çözüm dosyası (MySolution. sln) içeren bir klasörden aşağıdaki tüm çalışmalar anlamına gelir:

1. MySolution. sln nuget.exe geri yükleme
1. Geri yükleme nuget.exe.
1. nuget.exe geri yükleme

Restore komutu çözüm dosyasını açar ve çözüm içindeki tüm projeleri bulur. Buradan, `packages.config` projelerin her biri için dosyaları bulur ve bulunan tüm paketleri geri yükler. Ayrıca dosyada bulunan çözüm düzeyi paketleri de geri yükler `.nuget\packages.config` . Yeni restore komutu hakkında daha fazla bilgi için [komut satırı başvurusunda](../reference/cli-reference/cli-ref-restore.md)bulabilirsiniz.

#### <a name="the-new-package-restore-workflow"></a>Yeni paket geri yükleme Iş akışı

Yeni bir iş akışı kullanıma sunmakta olduğu için paket geri yükleme ile ilgili bu değişiklikler hakkında heyecanlıyız. Kaynak denetiminden paketlerinizi atlamak istiyorsanız, yalnızca klasörü yürütmeyin `packages` . Çözümü açan ve oluşturan Visual Studio kullanıcıları paketleri otomatik olarak geri yükledi. Komut satırı derlemeleri için, `nuget.exe restore` çağırmadan önce komutunu çağırmanız yeterlidir `msbuild` . Artık çözümünüzde "NuGet paketini geri yüklemeyi etkinleştir" hareketini kullanmayı unutmamanız gerekmez; artık, derlemeyi değiştirmek için projelerinizi değiştirmemiz gerekmez. Ayrıca bu durum, MSBuild içeri aktarmaları içeren paketlere yönelik daha gelişmiş bir deneyim de verir, özellikle de NuGet 'in son özelliği aracılığıyla \Build klasöründen [props/targets dosyalarını otomatik olarak içeri aktarmak](../release-notes/nuget-2.5.md#automatic-import-of-msbuild-targets-and-props-files) için.

Yaptığımız işin yanı sıra, bu yeni yaklaşımı yuvarlamak için bazı önemli iş ortaklarıyla de çalışacağız. Bunlardan herhangi biri için somut zaman çizelgeleri yoktur, ancak yeni yaklaşımda yaptığımız için her iş ortağı heyecanlıyız.

* Team Foundation Service, çağrısı `nuget.exe restore` varsayılan derleme senaryolarıyla tümleştirilecek şekilde çalışır.
* Windows Azure Web siteleri-projenizi Azure 'a itmeniz ve `nuget.exe restore` Web siteniz oluşturulmadan önce çağırılabilmesi için çalışıyoruz.
* TeamCity-TeamCity 8. x için NuGet yükleyici eklentisini güncelleştirirler
* Uygulama, deponuzu uygulamanıza dağıtmanıza ve `nuget.exe restore` çözümünüz derlemeden önce çağırılmasına olanak tanımak için çalışıyoruz.

Yukarıdaki iş ortaklarının her biri ile, kendi nuget.exe kendi kopyalarını kullanır ve çözümünüzde nuget.exe gerçekleştirmeniz gerekmez.

#### <a name="known-issues"></a>Bilinen Sorunlar

İlk 2,7 sürümüyle nuget.exe geri yükleme ile ilgili iki bilinen sorun vardı, ancak [NuGet. CommandLine paketine](http://www.nuget.org/packages/NuGet.CommandLine/)yönelik bir güncelleştirmeyle birlikte 9/6/2013 tarihinde düzeltildi.  Bu güncelleştirme, CodePlex 'teki [NuGet 2,7 indirme sayfasında](https://nuget.codeplex.com/releases/view/107605) da kullanılabilir.  Çalışan `nuget.exe update -self` , en son sürüme güncelleştirilecek.

Düzeltilen:

1. [Yeni paket geri yüklemesi, SLN dosyası kullanılırken mono üzerinde çalışmıyor](https://nuget.codeplex.com/workitem/3596)
1. [Yeni paket geri yüklemesi Wix projeleriyle çalışmıyor](https://nuget.codeplex.com/workitem/3598)

Ayrıca, [otomatik paket geri yükleme işlemi bir çözüm klasörü altındaki projeler için çalışmadığı](https://nuget.codeplex.com/workitem/3625)yeni paket geri yükleme iş akışı ile ilgili bilinen bir sorun da vardır. Bu sorun NuGet 2.7.1 'de düzeltildi.

### <a name="project-retargeting-and-upgrade-build-errorswarnings"></a>Proje yeniden hedefleme ve yükseltme derleme hataları/uyarıları

Projenizi yeniden hedefledikten veya yükselttikten sonra, bazı NuGet paketlerinin düzgün çalışmadığını fark edersiniz. Ne yazık ki bunun bir göstergesi yoktur ve bunun nasıl ele alınacağını gösteren bir rehberlik yoktur. NuGet 2,7 ile, artık projenizi, yüklü NuGet paketlerinizi etkileyecek şekilde yeniden hedeflediğiniz veya yükselttiğiniz zaman tanımak için bazı Visual Studio olaylarını kullanacağız.

Paketlerinizin herhangi birinin yeniden hedefleme veya yükseltme tarafından etkilendiğini tespit ettiğimiz takdirde, size bildirmek için anında derleme hataları üreteceğiz. Anında derleme hatasına ek olarak, `requireReinstallation="true"` `packages.config` yeniden hedeflemenin etkilediği tüm paketler için dosyanızda bir bayrak de kalıcı hale getiriyoruz ve Visual Studio 'daki sonraki her derleme bu paketlere yönelik derleme uyarıları oluşturacak.

NuGet, etkilenen paketleri yeniden yüklemek için otomatik eylem yapamasa da bu gösterge ve uyarı, paketleri yeniden yüklemeniz gerektiğinde bulmanıza yardımcı olur. Ayrıca, bu hata iletilerinin size yönlendirçalıştığı [paket yeniden yükleme kılavuzu belgeleri](../consume-packages/reinstalling-and-updating-packages.md) üzerinde çalışıyoruz.

### <a name="nuget-configuration-defaults"></a>NuGet yapılandırma Varsayılanları

Birçok şirket, NuGet 'i dahili olarak kullanıyor, ancak geliştiricilerin nuget.org yerine iç paket kaynaklarını kullanmasını sağlayan bir süre daha vardı. NuGet 2,7, için makine genelindeki varsayılan değerlerin belirtilmesini sağlayan bir yapılandırma Varsayılanları özelliği sunar:

1. Etkin paket kaynakları
1. Kaydedildi, ancak devre dışı paket kaynakları
1. Varsayılan nuget.exe gönderim kaynağı

Bunların her biri, artık konumunda bulunan bir dosya içinde yapılandırılabilir `%ProgramData%\NuGet\NuGetDefaults.Config` . Bu yapılandırma dosyasında paket kaynakları belirtilmişse, varsayılan nuget.org paket kaynağı otomatik olarak kaydedilmeyecektir ve `NuGetDefaults.Config` bunun yerine kayıt yapılır.

Bu özelliğin kullanılması gerekmediği sürece, şirketlerin grup ilkesi kullanarak dosya dağıtmaları beklenir `NuGetDefaults.Config` .

*Bu özelliğin hiçbir şekilde bir geliştirici NuGet ayarlarından bir paket kaynağı kaldırılmasına neden olacağını unutmayın. Yani, geliştirici zaten NuGet kullanıyorsa ve bu nedenle nuget.org paket kaynağı kayıtlıysa, bir dosya oluşturulduktan sonra kaldırılmaz `NuGetDefaults.Config` .*

Bu özellik hakkında daha fazla bilgi için bkz. [NuGet yapılandırma Varsayılanları](../consume-packages/configuring-nuget-behavior.md#nuget-defaults-file) .

### <a name="renaming-the-default-package-source"></a>Varsayılan paket kaynağını yeniden adlandırma

NuGet, nuget.org 'e işaret eden "NuGet resmi paket kaynağı" adlı varsayılan bir paket kaynağını her zaman kaydetti. Bu ad ayrıntılıdır ve gerçekten nerede işaret ettiğinden de belirtmiyordu. Bu iki sorunu gidermek için, bu paket kaynağını Kullanıcı arabiriminde yalnızca "nuget.org" olarak yeniden adlandırdık. Paket kaynağının URL 'SI de "www" de dahil olacak şekilde değiştirilmiştir. ekleyin. NuGet 2,7 kullanıldıktan sonra, mevcut "NuGet resmi paket kaynağınız", URL 'SI olarak "nuget.org" olarak "" olarak güncelleştirilir <https://www.nuget.org/api/v2/> .

### <a name="performance-improvements"></a>Performans Geliştirmeleri

2,7 ' de daha küçük bellek ayak, daha az disk kullanımı ve daha hızlı paket yüklemesi sağlayacak performans iyileştirmesi yaptık. Ayrıca, genel yükü azaltacak OData tabanlı akışlara daha akıllı sorgular yaptık.

### <a name="new-extensibility-apis"></a>Yeni genişletilebilirlik API 'Leri

Önceki sürümlerde eksik işlevlerin boşluğunu dolduracak genişletilebilirlik hizmetlerimize bazı yeni API 'Ler ekledik.

#### <a name="ivspackageinstallerservices"></a>Ivspackageınstallerservices

```cs
// Checks if a NuGet package with the specified Id and version is installed in the specified project.
bool IsPackageInstalledEx(Project project, string id, string versionString);

// Get the list of NuGet packages installed in the specified project.
IEnumerable<IVsPackageMetadata> GetInstalledPackages(Project project);
```

#### <a name="ivspackageinstaller"></a>Ivspackageınstaller

```cs
// Installs one or more packages that exist on disk in a folder defined in the registry.
void InstallPackagesFromRegistryRepository(string keyName, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);

// Installs one or more packages that are embedded in a Visual Studio Extension Package.
void InstallPackagesFromVSExtensionRepository(string extensionId, bool isPreUnzipped, bool skipAssemblyReferences, Project project, IDictionary<string, string> packageVersions);
```

### <a name="development-only-dependencies"></a>Development-Only bağımlılıklar

Bu özellik, [adam Canph](https://twitter.com/adamralph) tarafından katkıda bulunulmuş ve paket yazarlarının yalnızca geliştirme zamanında kullanılan ve paket bağımlılıkları gerektirmeyen bağımlılıkları bildirmesine izin veriyor. `developmentDependency="true"`İçindeki bir pakete bir öznitelik eklenerek `packages.config` , `nuget.exe pack` Bu paket artık bağımlılık olarak dahil olmayacaktır.

### <a name="removed-support-for-visual-studio-2010-express-for-windows-phone"></a>Windows Phone için Visual Studio 2010 Express desteği kaldırıldı

2,7 sürümündeki yeni paket geri yükleme modeli, ana NuGet VSPackage 'dan farklı olan yeni bir VSPackage tarafından uygulanır. Teknik bir sorun nedeniyle, aynı kod tabanını desteklenen diğer Visual Studio SKU 'Ları ile paylaştiğimiz için bu yeni VSPackage Windows Phone SKU 'su *Için Visual studio 2010 Express* 'te doğru çalışmaz. Bu nedenle, NuGet 2,7 ' den itibaren, yayımlanan uzantıdan *Windows Phone Için Visual Studio 2010 Express* desteğini bıraktık. *Web Için Visual studio 2010 Express* desteği, Visual Studio Uzantı galerisine yayımlanan birincil uzantıya hala dahildir.

Visual Studio 'nun bu sürümünde/sürümünde kaç geliştirici hala NuGet kullandığından emin olduğumuz için, bu kullanıcılara özel olarak ayrı bir Visual Studio uzantısı yayımlıyoruz ve CodePlex üzerinde yayınlarız (Visual Studio Uzantı Galerisi yerine). Bu uzantının bakımını yapmaya devam etmeyi planlıyoruz, ancak bu, bu uzantıyı etkiliyorsa, lütfen CodePlex üzerinde bir sorun kaydederek bize bilgi verin.

NuGet paket yöneticisini indirmek için (Windows Phone için Visual Studio 2010 Express için), [nuget 2,7 İndirmeleri](https://nuget.codeplex.com/releases/view/107605) sayfasını ziyaret edin.

### <a name="bug-fixes"></a>Hata Düzeltmeleri

Bu özelliklere ek olarak, NuGet 'in bu sürümü diğer birçok hata düzeltmesi de içerir. Yayında ele alınan toplam 97 sorun oluştu. NuGet 2,7 ' de düzeltilen iş öğelerinin tam listesi için lütfen [Bu sürüm Için NuGet sorun İzleyicisi](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.7&status=all)' ni görüntüleyin.
