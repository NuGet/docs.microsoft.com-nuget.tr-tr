---
title: NuGet sık sorulan sorular
description: Sık sorulan sorular ve komut satırında ve Visual Studio'da NuGet kullanma ve NuGet Galerisi ile çalışmaya yönelik yanıtlar.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/11/2018
ms.topic: conceptual
ms.openlocfilehash: 3fe59ef03632053182b034052e93a5f2e6f444bd
ms.sourcegitcommit: c643dd2c44e085601551ff7079d696bcc3ad2b49
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/21/2018
ms.locfileid: "42793603"
---
# <a name="nuget-frequently-asked-questions"></a>NuGet sık sorulan sorular

**NuGet çalıştırmak için gereken nedir?**

Hem kullanıcı Arabirimi ve komut satırı araçları tüm bilgileri kullanılabilir [Yükleme Kılavuzu](../install-nuget-client-tools.md).

**NuGet, Mono destekliyor mu?**

Komut satırı aracı `nuget.exe`, yapılar ve Mono altında 3.2 + çalıştırır ve paketleri Mono'da oluşturabilirsiniz.

Ancak `nuget.exe` çalışır tamamen Windows üzerinde bilinen sorunlar vardır Linux ve OS x başvurun [Mono sorunları](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) GitHub üzerinde.

A [grafik istemci](https://github.com/mrward/monodevelop-nuget-addin) MonoDevelop için bir eklenti olarak kullanılabilir.

**Bir paketi ne içerir ve kararlı ve Uygulamam için yararlı olup nasıl belirleyebilirim?**

Bir paketi hakkında bilgi almak için birincil kaynağı kendi nuget.org listeleme sayfasıdır (veya başka özel akış). Her bir paket nuget.org sayfasında, paket, sürüm geçmişi ve kullanım istatistiklerini açıklamasını içerir. **Bilgisi** bölüm paketi sayfasında, ayrıca projenin web sitesine, genelde nerede birçok örnekler ve diğer belgeler paket nasıl kullanıldığını öğrenmenize yardımcı olması için bir bağlantı içerir.

Daha fazla bilgi için [bulma ve seçme paketleri](../consume-packages/finding-and-choosing-packages.md).

## <a name="nuget-in-visual-studio"></a>Visual Studio'da NuGet

**NuGet farklı Visual Studio ürünleri nasıl destekleniyor mu?**

- Windows üzerinde Visual Studio destekleyen [Paket Yöneticisi UI](../tools/package-manager-ui.md) ve [Paket Yöneticisi Konsolu](../tools/package-manager-console.md).
- Mac için Visual Studio sahip yerleşik NuGet özellikleri üzerinde açıklandığı [dahil olmak üzere bir NuGet paketini projenize](/visualstudio/mac/nuget-walkthrough).
- Visual Studio Code (tüm platformlar) doğrudan bir NuGet tümleştirmesi yok. Kullanım [NuGet CLI](../tools/nuget-exe-cli-reference.md) veya [dotnet CLI](../tools/dotnet-commands.md).
- Visual Studio Team Services sağlar [NuGet paketlerini geri yüklemek için bir derleme adımı](/vsts/build-release/tasks/package/nuget). Ayrıca [konak özel NuGet paket akışları Team Services üzerinde](https://www.visualstudio.com/docs/package/nuget/publish).

**Yüklü olan NuGet Araçları'nın tam sürümünü nasıl kontrol edebilirim?**

Visual Studio'da kullanmak **Yardım > Microsoft Visual Studio hakkında** komut ve görüntülendiğini sürümde Ara **NuGet Paket Yöneticisi**.

Alternatif olarak, Paket Yöneticisi konsolu başlatın (**Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Konsolu**) girin `$host` NuGet sürümü dahil olmak üzere hakkındaki bilgileri görmek için.

**Hangi programlama dillerini NuGet tarafından destekleniyor mu?**

NuGet, genellikle .NET dilleri için çalışır ve bir projeye .NET kitaplıkları getirmek için tasarlanmıştır. Ayrıca bazı proje türlerinde MSBuild ve Visual Studio Otomasyonu desteklediği için diğer projeleri ve çeşitli dereceye dilleri de destekler.

C#, Visual Basic, F #, WiX ve C++ en son NuGet sürümünü destekler.

**Hangi proje şablonları, NuGet tarafından destekleniyor mu?**

NuGet, çeşitli Windows, Web, bulut, SharePoint, Wix ve benzeri gibi proje şablonları için tam destek sunar.

**Visual Studio şablonları parçası olan paketleri nasıl güncelleştirebilirim?**

Git **güncelleştirmeleri** sekmesinde Paket Yöneticisi UI ve seçin **Tümünü Güncelleştir**, veya [ `Update-Package` komut](../tools/ps-ref-update-package.md) Paket Yöneticisi konsolu.

Şablonu güncelleştirmek için şablon deposu el ile güncelleştirmeniz gerekir. Bkz: [Xavier Decoster'ın blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) bu konuda. Tüm bağımlılıkları en son sürümünü birbiriyle uyumlu değilse, el ile güncelleştirmeler şablonu bozulmasına neden olabilir çünkü kendi sorumluluğunuzdadır yapıldığını unutmayın.

**Visual Studio dışında NuGet kullanabilir miyim?**

Evet, NuGet doğrudan komut satırından çalışır. Bkz: [Yükleme Kılavuzu](../install-nuget-client-tools.md) ve [CLI başvurusu](../tools/nuget-exe-cli-reference.md).

## <a name="nuget-command-line"></a>NuGet komut satırı

**NuGet komut satırı aracının en son sürümünü nasıl alabilirim?**

Bkz: [Yükleme Kılavuzu](../install-nuget-client-tools.md).

**Nuget.exe lisansı nedir?**

Nuget.exe MIT lisansı koşulları altında yeniden dağıtmanız izin verilir. Güncelleştirme ve yeniden dağıtmak için seçtiğiniz nuget.exe tüm kopyalarını bakım için sorumlu olursunuz.

**NuGet komut satırı aracını genişletmek mümkündür?**

Evet, özel komutları eklemek mümkündür `nuget.exe`anlatılan şekilde [Rob Reynold'ın post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a>NuGet Paket Yöneticisi Konsolu (Windows için Visual Studio)

**Paket Yöneticisi Konsolu'nda DTE nesnesine erişimi nasıl edinebilirim?**

Visual Studio Otomasyon nesne modelindeki üst düzey nesnesi (geliştirme araçları ortamı) DTE nesnesi olarak adlandırılır. Konsol bu adlı bir değişken üzerinden sağlar `$DTE`. Daha fazla bilgi için [Otomasyon modeline genel bakış](/visualstudio/extensibility/internals/automation-model-overview) Visual Studio genişletilebilirlik belgelerinde.

**$DTE değişkeni DTE2 türüne dönüştürme deneyin ancak bir hata alıyorum: "" EnvDTE80.DTE2"türüne EnvDTE.DTEClass" türünün "EnvDTE.DTEClass" değeri dönüştürülemiyor. Ne oldu?**

Bu PowerShell bir COM nesnesi ile nasıl etkileştiğini ile bilinen bir sorundur. Şunları deneyin:

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

`Get-Interface` yardımcı işlevi, NuGet PowerShell ana bilgisayar tarafından eklenir.

## <a name="creating-and-publishing-packages"></a>Oluşturma ve paketleri yayımlama

**Bir akışta paketimle nasıl listelensin mi?**

Bkz: [oluşturma ve bir paket yayımlama](../quickstart/create-and-publish-a-package.md).

**My kitaplığının .NET Framework'ün farklı sürümlerini hedefleyen birden çok sürümü var. Bunu destekleyen tek bir paket nasıl oluşturabilirim?**

Bkz: [birden çok .NET Framework sürümleri ve profillerini destekleyen](../create-packages/supporting-multiple-target-frameworks.md).

**Kendi depo veya akış yukarı nasıl ayarlayabilirim?**

Bkz: [paketleri genel bakış barındırma](../hosting-packages/overview.md).

**Nasıl miyim toplu olarak akış my NuGet paketlerini yükleyebilir?**

Bkz: [toplu NuGet paketleri yayımlama](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).

## <a name="working-with-packages"></a>Paketleri ile çalışma

**Proje düzeyi paketi ve çözüm düzeyinde paket arasındaki fark nedir?**

Bir çözüm düzeyinde paketi (NuGet 3.x+) bir çözümde yalnızca bir kez yüklenir ve ardından iş Çözümdeki tüm projeleri için kullanılabilir hale gelir. Proje düzeyi paket kullandığı her projede yüklenir. Bir çözüm düzeyinde paketi, gelen paket Yöneticisi konsolu çağrılabilen yeni komutlar da yükleyebilirsiniz.

**NuGet paketleri Internet bağlantısı olmadan yüklemek mümkündür?**

Evet, Scott Hanselman'ın Blog yayınına bakın [NuGet nuget.org aşağı (veya gezmeyi İşiniz olduğunda) erişmek nasıl](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).

**Varsayılan paket klasöründen farklı bir konumda paketleri nasıl yüklerim?**

Ayarlama [ `repositoryPath` ](../reference/nuget-config-file.md#config-section) ayarı `Nuget.Config` kullanarak `nuget config -set repositoryPath=<path>`.

**NuGet paketleri klasörüne kaynak denetimine eklemeye nasıl kaçınabilirim?**

Ayarlama [ `disableSourceControlIntegration` ](../reference/nuget-config-file.md#solution-section) içinde `Nuget.Config` için `true`. Çözüm, bu anahtar çalışır düzeyi ve bu nedenle gerek eklenecek `$(Solutiondir)\.nuget\Nuget.Config` dosya. Visual Studio'da paket geri yükleme etkinleştirme bu dosya otomatik olarak oluşturur.

**Paket geri yükleme'yi nasıl kapatırım?**

Bkz: [etkinleştirme ve devre dışı paket geri yükleme](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).

**Neden alabilirim "bağımlılık hatayı gidermek için yapılandırılamıyor" ne zaman yerel paket ile uzak Bağımlılıkların yüklenmesi?**

Seçmenize gerek **tüm** projeye yerel bir paket yükleme sırasında kaynak. Bu, yalnızca bir tane yerine tüm akışları toplar. Bu hatanın görünür bir yerel depo kullanıcıları genellikle yanlışlıkla önlemek istediğiniz nedeni Kurumsal nedeniyle uzak bir paketi yükleme ilkeleri.

**Aynı klasörde birden çok proje sahibim, ayrı packages.config dosyaları her proje için nasıl kullanabilirim?**

NuGet tanımlar burada ayrı projeler Canlı ayrı klasörlerde çoğu projelerinde, bu bir sorun değildir `packages.config` her proje dosyaları. NuGet 3.3 + ve birden çok ile aynı klasörde yer alan projeler, projeye adı ekleyebilirsiniz `packages.config` dosya adlarını desenini kullanın `packages.{project-name}.config`, ve bu dosyayı NuGet kullanır.

Her proje dosyası kendi listesi bağımlılıklar içerdiğinden bu soruna PackageReference, kullanırken değil.

**Depolarımın listesini nuget.org göremiyorum, nasıl geri alabilirim?**

- Ekleme `https://api.nuget.org/v3/index.json` listenize kaynakları, veya
- Silme `%appdata%\.nuget\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) ve NuGet yeniden oluşturun.

**Bir paketi belirli bir lisans bilgileri sağlamıyorsa koşulları varsayılan lisans nelerdir?**

Her bir paketi paket ile birlikte gelen koşulları tabidir. Erişim, indirme veya herhangi bir paket alınırken önce hüküm gözden geçirmeniz gerekir. Nuget.org kullanın **lisans bilgilerini** bağlantı paketi sayfasında.

Bir paketi lisans koşulları belirtmezse kullanarak doğrudan paket sahibiyle iletişime geçin **sahipleriyle temas** nuget.org paketi sayfasında bağlantı. Microsoft hiçbir fikri mülkiyet, üçüncü taraf paketi sağlayıcılarından lisans değil ve üçüncü taraflarca sağlanan bilgileri sorumlu değildir.

## <a name="managing-packages-on-nugetorg"></a>Paketleri nuget.org üzerinde yönetme

**Paket meta verileri, karşıya yüklendikten sonra düzenleyebilir miyim?**

NuGet imzalanması için tüm paketleri önerir. Paket imzalama tasarımı prensibi imzalı paket içeriğini nuspec içeren değişmezse, olmasıdır. Paket meta verileri düzenleme, mevcut imza geçersiz kılmalarını nuspec için değişiklikle sonuçlanır. Paket oluşturulduktan sonra paket meta verileri düzenleme gerektirmeyecek şekilde mevcut iş akışları değiştirme öneririz.

Paketiniz için listelenen bağımlılıkları paketinden otomatik olarak oluşturulur ve düzenlenemez unutmayın.

Ayrıca, paketler için karşıya yükleme [staging.nuget.org](http://staging.nuget.org) test edin ve bir paket kullanılabilir genel galeride yapmadan paketinizi doğrulamak için harika bir yoludur.

**Bu ad gelecekte yayımlanacak paketleri için ayrılacak mümkün mü?**

Evet. Şirket için paket kimlikleri ayırabilirsiniz [nuget.org](https://www.nuget.org/) hesabınız için bir paket kimliği öneki isteyerek. Bir paket kimliği öneki isteğinde bulunmak için yönergeleri izleyin. [belgeleri](https://docs.microsoft.com/nuget/reference/id-prefix-reservation).

**Paketler için mülkiyeti üzerine hak iddia nasıl?**

Bkz: [yönetme paket sahipleri nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).

**Yazılım lisansımın ihlal bir paket sahibi ile nasıl dağıtılsın mı?**

Paket sahipleri ve diğer yazılımların sahipleri arasında kaynaklanabilecek herhangi Anlaşmazlıkların çözüm yeri birlikte çalışmak için NuGet topluluk öneririz. Biz hazırlanmış bir [itiraz çözümleme işlemi](../policies/dispute-resolution.md) nuget.org yöneticilerin intercede isteyen önce izlemek için.

**Benim test paketleri nuget.org için karşıya yüklemek için tavsiye edilir?**

Test amaçları için kullanabileceğiniz [staging.nuget.org](http://staging.nuget.org), veya diğer genel NuGet sunucularını [myget.org](https://myget.org) veya [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).

Paketler için Staging.nuget.org karşıya korunmaz unutmayın. Bkz: [güle güle Önizleme](http://blog.nuget.org/20130419/goodbye-preview.html).

**Paketleri nuget.org için karşıya yükleyebilirsiniz boyutu üst sınırı nedir?**

nuget.org sağlayan paketler en fazla 250MB, ancak paketleri 1 MB'den mümkünse tutulması ve paketleri birbirine bağlamak için bağımlılıklar kullanarak önerilir. Bir kural karşısında, paketler çarpışmalardan kaçınmak için yalnızca bir derleme içerir.

NuGet paketleri başarısız yüklemeler olasılığı daha küçük parçalara değerinden daha büyük paketleriniz varsa bu nedenle indirmek için HTTP kullanır.

Toplam yükleme boyutu için NuGet paketlerinizi tüketicilerinin küçülterek birden çok paketleri arasındaki bağımlılıkları paylaşmak da mümkündür.

Çoğunlukla statik ve hiçbir zaman değişiklik bağımlılıklardır. Kodda bir hatayı düzeltirken, bağımlılıkları güncelleştirilmesi gerekmez. Bağımlılıkları paketlerseniz, her zaman büyük paketler reshipping yukarı bitmelidir. NuGet paketlerini ilgili bağımlılıklarınızı bölerek yükseltme paketinin Tüketiciler için çok daha ayrıntılı sağlar.

## <a name="nugetorg-not-accessible"></a>nuget.org erişilebilir değil

**Neden paketleri indirin veya paketleri nuget.org için Yükle?**

İlk olarak, en son NuGet sürümlerini kullandığınızdan emin olun. Bu sürüm başarısız devam ederseniz [Destek ekibiyle iletişime geçin](https://www.nuget.org/policies/Contact) ve sorun giderme bilgileri de dahil olmak üzere ek bağlantı sağlayın:

- Kullanmakta olduğunuz NuGet sürümü
- Kullanmakta olduğunuz paket kaynakları
- Ayrıntılı ayrıntı düzeyi içeren bir geri yükleme günlüğü
- MTR veya Fiddler izlemeleri (aşağıya bakın)
- Coğrafi konuma
- İşletim sistemi sürümünüz
- Makine Yapılandırması (CPU, ağ, sabit sürücü)
- Makinenizde bir proxy veya güvenlik duvarı olup
- Makinede yüklü .NET sürümlerini
- .NET CLI veya kullanmakta olduğunuz DNU gibi platformlar arası araçları sürümleri

*MTR yakalamak için:*

- Gelen WinMTR indirin [http://winmtr.net/download/](http://winmtr.net/)
- Girin `api.nuget.org` tıklayın ve ana bilgisayar adı olarak **Başlat**.
- Bekle **gönderilen** sütun > = 100.

    ![MTR yakalama](media/mtr.png)

- Metin Panoya kopyalayın.

*Fiddler yakalamak için:*

- En son sürümünü yükleyin [Fiddler](http://www.telerik.com/download/fiddler).
- Fiddler'ı başlatın ve trafik yakalama kullanarak devre dışı **Dosya > trafik yakalama** menüsü.
- Tüm oturumlar kaldırın (tüm öğeleri listesinde, tuşuna seçin **Sil** anahtar).
- HTTPS trafiğini denetleyerek yakalamak için fiddler'ı yapılandırma **şifresini HTTPS trafiğini** içinde **HTTPS** sekmesinde **Araçlar > Fiddler seçenekleri...**  menüsü.
- Visual Studio’yu kapatın.
- Etkinleştirme **Dosya > trafik yakalama** menüsü.
- Visual Studio ya da nuget.exe .exe başlatın ve çalışmıyor eylemleri gerçekleştirebilirsiniz. Bu eylemler tarafından oluşturulan trafiğin Fiddler'da göstermelidir.
- Bir eylem gerçekleştirdikten sonra kullanmak **Dosya > Kaydet > tüm oturumları** yakalanan oturumları depolamak için.

Not: Bunu ayarlamak için gerekli olabilecek `HTTP_PROXY` ortam değişkenine `http://127.0.0.1:8888` için fiddler'ı aracılığıyla NuGet trafiği yönlendirme.

Bu başarısız olursa deneyin [ipuçları bu StackOverflow gönderide bahsedilen](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).

**Nuget.org API uç noktaları nelerdir?**

V3: `https://api.nuget.org/v3/index.json` V2: `https://www.nuget.org/api/v2/` (V2 API kullanım dışıdır ve NuGet ile 4 + çalışmaz unutmayın.)
