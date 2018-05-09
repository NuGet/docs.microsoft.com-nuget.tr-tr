---
title: NuGet sık sorulan sorular
description: Ortak sorular ve yanıtlar NuGet komut satırında ve Visual Studio kullanarak ve NuGet Galerisi ile çalışmak için.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/11/2018
ms.topic: conceptual
ms.openlocfilehash: bcdb4e8971ee4e742e6cf37f8b662e50a77604f0
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-frequently-asked-questions"></a>NuGet sık sorulan sorular

**NuGet çalıştırmak için gereken nedir?**

Kullanıcı Arabirimi ve komut satırı araçları geçici tüm bilgileri kullanılabilir [Yükleme Kılavuzu](../install-nuget-client-tools.md).

**NuGet Mono destekliyor mu?**

Komut satırı aracı `nuget.exe`, oluşturur ve Mono altında 3.2 + çalıştırır ve paketleri Mono olarak oluşturabilirsiniz.

Ancak `nuget.exe` çalışır tam olarak Windows, bilinen sorunlar vardır Linux ve OS x bakın [Mono sorunları](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) github'da.

A [grafik istemci](https://github.com/mrward/monodevelop-nuget-addin) MonoDevelop için bir eklenti olarak kullanılabilir.

**Ne bir paket içerir ve kararlı ve Uygulamam için yararlı olup nasıl belirleyebilirim?**

Birincil bir paketi hakkında bilgi almak için kendi nuget.org listeleme sayfasında kaynağıdır (veya başka bir özel akış). Her bir paket nuget.org sayfasında paketi, sürüm geçmişi ve kullanım istatistiklerini açıklamasını içerir. **Bilgisi** paketi sayfasında bölüm ayrıca projenin web genellikle bulabileceğiniz birçok örnekler ve paket nasıl kullanıldığını öğrenmenize yardımcı olacak diğer belgelerin siteye bir bağlantı içerir.

Daha fazla bilgi için bkz: [bulma ve paketleri seçme](../consume-packages/finding-and-choosing-packages.md).

## <a name="nuget-in-visual-studio"></a>Visual Studio'da NuGet

**Nasıl NuGet farklı Visual Studio ürünlerinde destekleniyor mu?**

- Visual Studio Windows destekler [Paket Yöneticisi kullanıcı Arabirimi](../tools/package-manager-ui.md) ve [Paket Yöneticisi Konsolu](../tools/package-manager-console.md).
- Mac için Visual Studio açıklandığı gibi yerleşik NuGet özellikleri olan [dahil olmak üzere bir NuGet paketini projenize](/visualstudio/mac/nuget-walkthrough).
- Visual Studio Code (tüm platformlar) doğrudan herhangi NuGet tümleştirme yok. Kullanım [NuGet CLI](../tools/nuget-exe-cli-reference.md) veya [dotnet CLI](../tools/dotnet-commands.md).
- Visual Studio Team Services sağlar [NuGet paketlerini geri yüklemek için bir derleme adımı](/vsts/build-release/tasks/package/nuget). Ayrıca [konak özel NuGet paketi akışları Team Services](https://www.visualstudio.com/docs/package/nuget/publish).

**Yüklü olan NuGet Araçlar'ün tam sürümünü nasıl kontrol edilsin mi?**

Visual Studio'da kullanın **Yardım > Microsoft Visual Studio hakkında** komut ve yanında görüntülenen sürümünde arayın **NuGet Paket Yöneticisi**.

Alternatif olarak, Paket Yöneticisi konsolu başlatın (**Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Konsolu**) ve girin `$host` NuGet sürümü de dahil olmak üzere hakkındaki bilgileri görmek için.

**Hangi programlama dillerini NuGet tarafından destekleniyor mu?**

NuGet genellikle .NET diller için kullanılabilir ve .NET kitaplıkları bir projeye duruma getirmek için tasarlanmıştır. Ayrıca bazı proje türleri MSBuild ve Visual Studio Otomasyon desteklediği için diğer projeler ve çeşitli derece dilleri de destekler.

C#, Visual Basic, F #, WiX ve C++ NuGet en son sürümünü destekler.

**Hangi proje şablonları NuGet tarafından destekleniyor mu?**

NuGet proje şablonları Windows, Web, bulut, SharePoint, Wix vb. gibi çeşitli için tam destek vardır.

**Visual Studio şablonları parçası olan paketleri nasıl güncelleştiririm?**

Git **güncelleştirmeleri** sekmesinde Paket Yöneticisi Arabiriminde ve seçin **Tümünü Güncelleştir**, veya [ `Update-Package` komutu](../tools/ps-ref-update-package.md) Paket Yöneticisi Konsolu'ndan.

Şablonu güncelleştirmek için şablon depo el ile güncelleştirmeniz gerekir. Bkz: [Xavier Decoster'ın blogu](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) Bu konu hakkında. Tüm bağımlılıklarını en son sürümünü birbirleri ile uyumlu değilse el ile güncelleştirmeleri şablona bozulmasına neden olabilir çünkü bu, kendi risk yapılır unutmayın.

**NuGet Visual Studio dışında kullanabilir miyim?**

Evet, NuGet doğrudan komut satırından çalışır. Bkz: [Yükleme Kılavuzu](../install-nuget-client-tools.md) ve [CLI başvuru](../tools/nuget-exe-cli-reference.md).

## <a name="nuget-command-line"></a>NuGet komut satırı

**NuGet komut satırı aracının en son sürümünü nasıl sağlarım?**

Bkz: [Yükleme Kılavuzu](../install-nuget-client-tools.md).

**Nuget.exe lisansını nedir?**

MIT lisans koşullarına nuget.exe yeniden dağıtmak için izin verilir. Güncelleştirme ve yeniden dağıtmak için seçtiğiniz nuget.exe tüm kopyalarını bakım sorumlu.

**NuGet komut satırı aracı genişletmek mümkün mü?**

Evet, özel komut eklemek olası `nuget.exe`açıklandığı gibi [Ramiz Reynold'ın post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a>NuGet Paket Yöneticisi Konsolu (Windows için Visual Studio)

**Paket Yöneticisi Konsolu'nda DTE nesneye erişimi nasıl sağlarım?**

Visual Studio Otomasyon nesne modeli en üst düzey nesnesinde DTE (geliştirme araçları ortamı) nesne adı verilir. Konsol bu adlı bir değişken üzerinden sağlar `$DTE`. Daha fazla bilgi için bkz: [Otomasyon modeline genel bakış](/visualstudio/extensibility/internals/automation-model-overview) Visual Studio genişletilebilirliğini belgelerinde.

**DTE2 türü $DTE değişkenine cast deneyin, ancak bir hata iletisi: "" EnvDTE80.DTE2"türü için EnvDTE.DTEClass" türündeki "EnvDTE.DTEClass" değeri dönüştürülemiyor. Ne oldu?**

Bu, PowerShell COM nesnesi ile nasıl etkileşim kurduğu ile bilinen bir sorundur. Aşağıdakileri deneyin:

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

`Get-Interface` yardımcı işlevi NuGet PowerShell ana bilgisayar tarafından eklenir.

## <a name="creating-and-publishing-packages"></a>Oluşturma ve paketleri yayımlama

**Bir akış my paketinde nasıl listesinde?**

Bkz: [oluşturma ve yayımlama bir paketi](../quickstart/create-and-publish-a-package.md).

**.NET Framework'ün farklı sürümlerini hedefleyen birden fazla sürümünü Kitaplığı'mdan var. Bunu destekleyen tek bir paket nasıl oluşturulacağına?**

Bkz: [birden çok .NET Framework sürümleri ve profillerini destekleyen](../create-packages/supporting-multiple-target-frameworks.md).

**Kendi deposu veya akış nasıl ayarlarım?**

Bkz: [paketleri genel bakış barındırma](../hosting-packages/overview.md).

**Nasıl ı toplu olarak akış my NuGet paketleri yükleyebilir?**

Bkz: [toplu NuGet paketleri yayımlama](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).

## <a name="working-with-packages"></a>Paketleri ile çalışma

**Proje düzeyi paketi ve bir çözüm düzeyi paketi arasındaki fark nedir?**

Bir çözüm düzeyi paketi (NuGet 3.x+) bir çözümde yalnızca bir kez yüklenir ve ardından Çözümdeki tüm projeleri için kullanılabilir hale gelir. Proje düzeyi paketi kullandığı her projede yüklü. Bir çözüm düzeyi paket gelen paket Yöneticisi konsolu çağrılabilen yeni komutları da yükleyebilirsiniz.

**Internet bağlantısı olmadan NuGet paketlerini yüklemek mümkün mü?**

Evet, Scott Hanselman'ın Blog Gönderisi bkz [NuGet nuget.org aşağı (veya üzerinde bir düzlemi olduğunuz olduğunda) erişmek nasıl](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).

**Varsayılan paket klasöründen farklı bir konumda paketleri nasıl yüklerim?**

Ayarlama [ `repositoryPath` ](../reference/nuget-config-file.md#config-section) ayarı `Nuget.Config` kullanarak `nuget config -set repositoryPath=<path>`.

**NuGet paketleri klasörüne kaynak denetimine ekleme nasıl kaçının?**

Ayarlama [ `disableSourceControlIntegration` ](../reference/nuget-config-file.md#solution-section) içinde `Nuget.Config` için `true`. Çözüm, bu anahtar çalışır düzeyde ve bu nedenle gereksinim eklenecek `$(Solutiondir)\.nuget\Nuget.Config` dosya. Paket geri yüklemesi Visual Studio'dan etkinleştirme bu dosyayı otomatik olarak oluşturur.

**Paket geri yükleme'yi nasıl kapatırım?**

Bkz: [etkinleştirme ve paket geri yüklemesi devre dışı bırakma](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).

**Neden alabilirim "bağımlılık hatası bir çözümlenemiyor" ne zaman uzaktan bağımlılıkları olan yerel bir paketi yükleniyor?**

Seçmenize gerek **tüm** bir yerel paket projeye yüklerken kaynak. Bu yalnızca bir kullanmak yerine tüm akışları toplar. Bu hata görünür kullanıcıların yerel bir depo genellikle yanlışlıkla önlemek istediğiniz nedeni şirket nedeniyle uzak bir paket yükleme ilkeleri.

**Birden çok proje aynı klasörde sahibim, ayrı packages.config dosyaları her proje için nasıl kullanabilirim?**

NuGet tanımlayan gibi burada ayrı projeler Canlı ayrı klasörlerde çoğu projelerde, bu bir sorun teşkil etmez `packages.config` her proje dosyaları. NuGet 3.3 + ve birden fazla ile projeleri ile aynı klasörde projeye adını ekleyebilirsiniz `packages.config` dosya adlarını kullanın düzeni `packages.{project-name}.config`, ve NuGet bu dosyasını kullanır.

Her proje dosyası bağımlılıkları kendi listesi içerdiğinden bu bir sorun PackageReference, kullanırken değildir.

**Nuget.org depoları my listede göremiyorum, nasıl geri sağlarım?**

- Ekleme `https://api.nuget.org/v3/index.json` kaynakları, listenize veya
- Silme `%appdata%\.nuget\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) ve yeniden oluşturun NuGet izin verin.

**Bir paketi belirli lisans bilgileri sağlamazsa koşulları varsayılan lisans nelerdir?**

Her paket paketine dahil terimleri tabidir. Erişim, indirme ya da herhangi bir paket alınırken önce hüküm gözden geçirmelidir. Nuget.org üzerinde kullanmak **lisans bilgilerini** bağlantı paketi sayfasında.

Bir paketi Lisans Koşulları'nı belirtmiyorsa kullanarak doğrudan paketi sahibine başvurun **sahipleri başvurun** nuget.org paketi sayfasında bağlantı. Microsoft hiçbir fikri mülkiyet, üçüncü taraf paket sağlayıcılardan lisans değildir ve üçüncü taraflar tarafından sağlanan bilgileri sorumlu değildir.

## <a name="managing-packages-on-nugetorg"></a>Nuget.org paketlerini yönetme

**Paket meta verileri, karşıya yüklendikten sonra düzenleyebilir miyim? Neden nuspec düzenleme ve meta veri paketini değişiklik yapmak için yeni bir paket karşıya yükleme gerekiyor mu?**

NuGet tüm paketler imzalanmasını gerektirir. Paketin imzalanması bir tasarım prensibi imzalı paket içeriğini nuspec içeren değişmez, olmanızın gerekmesidir. Paket meta verileri düzenleme değişiklikleri varolan imza geçersiz kılmalarını nuspec için sonuçlanır. Paket oluşturulduktan sonra paket meta verileri düzenleme gerektirmeyecek şekilde var olan iş akışları değiştirme öneririz.

Not paketiniz için listelenen bağımlılıkları paketinden otomatik olarak oluşturulur ve düzenlenemez.

Ayrıca, paketler karşıya [staging.nuget.org](http://staging.nuget.org) sınamak ve bir paket genel bir galeride kullanıma olmadan paketinizi doğrulamak için harika bir yoludur.

**Gelecekte yayımlanacak paketler için adları ayırmak mümkün mü?**

Evet. Üzerinde paketler için kimlikleri ayırabilirsiniz [nuget.org](https://www.nuget.org/) hesabınız için bir paket kimliği önek isteyen tarafından. Bir paket kimliği öneki istemek için yönergeleri izleyin [belgelerine](https://docs.microsoft.com/nuget/reference/id-prefix-reservation).

**Paketler için sahipliğini talep nasıl?**

Bkz: [yönetme paket sahipleri nuget.org üzerinde](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).

**My yazılım lisansı ihlal eden bir paket sahibi ile nasıl ilgilenir?**

Paket sahipleri ve diğer yazılımların sahipleri arasında kaynaklanabilecek itirazları çözümlemek için birlikte çalışmak üzere NuGet topluluk öneririz. Biz hazırlanmış bir [itiraz çözümleme işlemi](../policies/dispute-resolution.md) nuget.org yöneticilerin intercede soran önce izlemek için.

**My sınama paketlerini nuget.org için karşıya yükleme önerilir?**

Test amaçları için kullandığınız [staging.nuget.org](http://staging.nuget.org), veya alternatif ortak NuGet sunucularını [myget.org](https://myget.org) veya [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).

Paketler için Staging.nuget.org karşıya korunmaz unutmayın. Bkz: [güle güle Önizleme](http://blog.nuget.org/20130419/goodbye-preview.html).

**Paketler için nuget.org karşıya yükleyebilir en büyük boyutu nedir?**

nuget.org sağlayan paketler en fazla 250MB, ancak paketleri birbirine bağlamak için bağımlılıkları kullanarak ve paketleri 1 MB'den mümkünse tutulması önerilir. Altın kural, çakışmaları önlemek için yalnızca bir derleme paketleri içerir.

NuGet paketleri, başarısız yükler olasılığı daha küçük olanları daha büyük paketleriniz varsa şekilde indirmek için HTTP kullanır.

NuGet paketlerinizi Tüketiciler için toplam yükleme boyutunu küçülterek, birden çok paket arasındaki bağımlılıkları paylaşmak da mümkündür.

Çoğunlukla statik ve hiçbir zaman değişikliği bağımlılıklardır. Kodda bir hata düzeltme, bağımlılıkları güncelleştirilmesi gerekmeyebilir. Bağımlılıklar paketini, her zaman büyük paketler reshipping yukarı sonlandırın. NuGet paketleri ilgili bağımlılıkları bölerek yükseltme paketinizi Tüketiciler için çok daha ayrıntılı sağlar.

## <a name="nugetorg-not-accessible"></a>nuget.org erişilebilir değil

**Neden paketleri indirme veya paketler için nuget.org karşıya?**

Öncelikle, NuGet'ın en son sürümlerini kullandığınızdan emin olun. Bu sürüm başarısız olmaya devam ederse [desteğine başvurun](https://www.nuget.org/policies/Contact) ve sorun giderme bilgileri de dahil olmak üzere ek bağlantı sağlayın:

- Kullanmakta olduğunuz NuGet sürümü
- Kullanmakta olduğunuz paket kaynaklarını
- Ayrıntılı ayrıntı düzeyine sahip bir geri yükleme günlüğü
- MTR veya Fiddler izlemeleri (aşağıya bakın)
- Coğrafi konuma
- İşletim sistemi sürümü
- Makine Yapılandırma (CPU, ağ, sabit sürücü)
- Makinenizde bir proxy veya güvenlik duvarı arkasında olup
- Makinede yüklü .NET sürümlerini
- Platformlar arası araçlarının .NET CLI ya da kullandığınız DNU gibi sürümleri

*MTR yakalamak için:*

- Gelen WinMTR indirin [http://winmtr.net/download/](http://winmtr.net/)
- Girin `api.nuget.org` tıklatın ve ana bilgisayar adı olarak **Başlat**.
- Bekle **gönderilen** sütunu > = 100.

    ![MTR yakalama](media/mtr.png)

- Metni panoya kopyalayın.

*Fiddler yakalamak için:*

- En son sürümünü yüklemek [Fiddler](http://www.telerik.com/download/fiddler).
- Fiddler'ı başlatın ve yakalama trafiği kullanılarak devre dışı bırakma **Dosya > trafiği Yakala** menüsü.
- Tüm oturumları kaldırın (tüm öğeleri listesinde, basın seçme **silmek** anahtar).
- HTTPS trafiğini denetleyerek yakalamak için fiddler'ı yapılandırma **şifresini HTTPS trafiği** içinde **HTTPS** sekmesinde **Araçlar > Fiddler seçenekleri...**  menüsü.
- Visual Studio’yu kapatın.
- Etkinleştirme **Dosya > trafiği Yakala** menüsü.
- Visual Studio ya da nuget.exe .exe başlatmak ve çalışmıyor eylemleri gerçekleştirebilirsiniz. Bu eylemleri tarafından oluşturulan trafiğin Fiddler'da göstermelidir.
- Eylemler çalıştırdıktan sonra kullanmak **Dosya > Kaydet > tüm oturumları** yakalanan oturumları depolamak için.

Not: Bunu ayarlamak için gerekli olabilecek `HTTP_PROXY` ortam değişkenine `http://127.0.0.1:8888` Fiddler aracılığıyla yönlendirme NuGet trafiği için.

Başarısız olursa, deneyin [bu StackOverflow postasında belirtilen ipuçları](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).

**Nuget.org için API uç noktaları nelerdir?**

V3: `https://api.nuget.org/v3/index.json` V2: `https://www.nuget.org/api/v2/` (V2 API kullanım dışıdır ve NuGet ile 4 + çalışmaz unutmayın.)
