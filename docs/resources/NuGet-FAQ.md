---
title: NuGet Sık Sorulan Sorular
description: NuGet'i komut satırında ve Visual Studio'da kullanmak için sık sorulan sorular ve yanıtlar
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 8cc990e0c9eed07c59c8dffb04d104be47051736
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "69999949"
---
# <a name="nuget-frequently-asked-questions"></a>NuSık sık sorulan soruları alın

NuGet.org hesap soruları gibi NuGet.org ilgili sık sorulan sorular için, [sık sorulan NuGet.org sorulara](../nuget-org/nuget-org-faq.md)bakın.

**NuGet'i çalıştırmak için neler gereklidir?**

Hem Kullanıcı UI hem de komut satırı araçları yla ilgili tüm bilgiler [Yükleme kılavuzunda](../install-nuget-client-tools.md)mevcuttur.

**NuGet Mono'yı destekliyor mu?**

Komut satırı aracı, `nuget.exe`Mono 3.2+ altında oluşturur ve çalışır ve Mono'da paketler oluşturabilir.

Windows'da tam olarak çalışsa da, `nuget.exe` Linux ve [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) OS X ile ilgili bilinen sorunlar vardır.

MonoDevelop için eklenti olarak [bir grafik istemcisi](https://github.com/mrward/monodevelop-nuget-addin) kullanılabilir.

**Bir paketin ne içerdiğini ve uygulamam için kararlı ve kullanışlı olup olmadığını nasıl belirleyebilirim?**

Bir paket hakkında bilgi edinmek için birincil kaynak nuget.org (veya başka bir özel besleme) üzerindeki giriş sayfasıdır. nuget.org'daki her paket sayfası paketin açıklamasını, sürüm geçmişini ve kullanım istatistiklerini içerir. Paket sayfasındaki **Bilgi** bölümü, genellikle paketin nasıl kullanıldığını öğrenmenize yardımcı olacak birçok örnek ve diğer belgeleri bulduğunuz projenin web sitesine bir bağlantı da içerir.

Daha fazla bilgi için [paketleri bulma ve seçme](../consume-packages/finding-and-choosing-packages.md)ye bakın.

## <a name="nuget-in-visual-studio"></a>NuGet Görsel Stüdyoda

**NuGet farklı Visual Studio ürünlerinde nasıl desteklenir?**

- Windows'daki Visual [Studio, Paket Yöneticisi UI'yi](../consume-packages/install-use-packages-visual-studio.md) ve [Paket Yöneticisi Konsolu'nu](../consume-packages/install-use-packages-powershell.md)destekler.
- Mac için Visual Studio, [projenize bir NuGet paketi dahil](/visualstudio/mac/nuget-walkthrough)etme de dahil olmak üzere açıklandığı gibi yerleşik NuGet özelliklerine sahiptir.
- Visual Studio Code (tüm platformlar) herhangi bir doğrudan NuGet entegrasyonu yok. [NuGet CLI](../reference/nuget-exe-cli-reference.md) veya [dotnet CLI'yi](../reference/dotnet-commands.md)kullanın.
- Azure [DevOps, NuGet paketlerini geri yüklemek için bir yapı adımı](/vsts/build-release/tasks/package/nuget)sağlar. Azure [DevOps'te özel NuGet paket akışlarını](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish)da barındırabilirsiniz.

**Yüklenen NuGet araçlarının tam sürümünü nasıl kontrol edebilirim?**

Visual Studio'da Microsoft **Visual Studio** hakkında yardım > kullanın ve **NuGet Package Manager'ın**yanında görüntülenen sürüme bakın.

Alternatif olarak, Paket Yöneticisi Konsolu 'nu **(Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Konsolu)** başlatın ve sürüm de dahil olmak üzere NuGet hakkındaki bilgileri görmek için girin. `$host`

**NuGet tarafından hangi programlama dilleri desteklenir?**

NuGet genellikle .NET dilleri için çalışır ve .NET kitaplıklarını bir projeye katmak üzere tasarlanmıştır. Bazı proje türlerinde MSBuild ve Visual Studio otomasyonunu da desteklediği nden, diğer projeleri ve dilleri çeşitli derecelerde de destekler.

NuGet'in en son sürümü C#, Visual Basic, F#, WiX ve C++'ı destekler.

**NuGet tarafından hangi proje şablonları desteklenir?**

NuGet, Windows, Web, Bulut, SharePoint, Wix gibi çeşitli proje şablonları için tam destek vardır.

**Visual Studio şablonlarının bir parçası olan paketleri nasıl güncellerim?**

Paket Yöneticisi Kullanıcı UI'deki **Güncelleştirmeler** sekmesine gidin ve **Tümünü Güncelleştir'i**seçin veya Paket Yöneticisi Konsolu'ndan [ `Update-Package` komutu](../reference/ps-reference/ps-ref-update-package.md) kullanın.

Şablonun kendisini güncelleştirmek için şablon deposunu el ile güncelleştirmeniz gerekir. Bu konuda [Xavier Decoster günlüğü](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) bakın. Tüm bağımlılıkların en son sürümü birbiriyle uyumlu değilse, el ile güncelleştirmeler şablonu bozabileceğinden, bunun kendi riskiniz olduğunu unutmayın.

**Visual Studio dışında NuGet kullanabilir miyim?**

Evet, NuGet doğrudan komut satırından çalışır. Yükleme [kılavuzuna](../install-nuget-client-tools.md) ve [CLI başvurusuna](../reference/nuget-exe-cli-reference.md)bakın.

## <a name="nuget-command-line"></a>NuGet komut satırı

**NuGet komut satırı aracının en son sürümünü nasıl edinebilirim?**

Yükle [kılavuzuna](../install-nuget-client-tools.md)bakın. Aracın geçerli yüklü sürümünü denetlemek için `nuget help`.

**Nuget.exe'nin lisansı nedir?**

Nuget.exe'yi MIT lisansı nın şartları altında yeniden dağıtabilirsiniz. Yeniden dağıtmayı seçtiğiniz nuget.exe kopyalarını güncellemek ve hizmet vermek sizin sorumluluğunuzdadır.

**NuGet komut satırı aracını genişletmek mümkün mü?**

Evet, [Rob Reynold sonrası](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx)açıklandığı `nuget.exe`gibi , özel komutları eklemek mümkündür.

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a>NuGet Paket Yöneticisi Konsolu (Windows'da Visual Studio)

**Paket Yöneticisi konsolundaki DTE nesnesine nasıl erişebilirim?**

Visual Studio otomasyon nesnesi modelindeki üst düzey nesneye DTE (Geliştirme Araçları Ortamı) nesnesi adı verilir. Konsol bunu . `$DTE` Daha fazla bilgi için Visual Studio Genişletilebilirlik belgelerinde [Otomasyon Modeline Genel Bakış'a](/visualstudio/extensibility/internals/automation-model-overview) bakın.

**$DTE değişkenini DTE2 türüne dökmeye çalışıyorum, ancak bir hata alıyorum: "EnvDTE.DTEClass" türündeki "EnvDTE.DTEClass" değerini "EnvDTE80.DTE2" yazına dönüştüremiyorum. Ne oldu?**

Bu, PowerShell'in com nesnesiyle nasıl etkileşimde olduğuyla ilgili bilinen bir sorundur. Aşağıdaki işlemi deneyin:

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

`Get-Interface`NuGet PowerShell ana bilgisayar tarafından eklenen bir yardımcı işlevdir.

## <a name="creating-and-publishing-packages"></a>Paket oluşturma ve yayımlama

**Paketimi özet akışında nasıl listeleyebilirim?**

Bkz. [Paket oluşturma ve yayımlama.](../quickstart/create-and-publish-a-package.md)

**Kütüphanemin .NET Framework'ün farklı sürümlerini hedefleyen birden çok sürümü var. Bunu destekleyen tek bir paketi nasıl oluştururum?**

Bkz. [Birden Çok .NET Framework Sürümlerini ve Profillerini Destekleme](../create-packages/supporting-multiple-target-frameworks.md).

**Kendi depomu veya beslememi nasıl ayarlıyorum?**

Hosting [paketlerine genel bakışa](../hosting-packages/overview.md)bakın.

**Paketleri NuGet akışıma toplu olarak nasıl yükleyebilirim?**

Bkz. [Toplu yayımlama NuGet paketleri](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).

## <a name="working-with-packages"></a>Paketlerle çalışma

**Proje düzeyinde paket ile çözüm düzeyinde paket arasındaki fark nedir?**

Çözüm düzeyinde bir paket (NuGet 3.x+) bir çözüme yalnızca bir kez yüklenir ve daha sonra çözümdeki tüm projeler için kullanılabilir. Onu kullanan her projeye proje düzeyinde bir paket yüklenir. Çözüm düzeyindebir paket, Paket Yöneticisi Konsolu'nun içinden çağrılabilen yeni komutlar da yükleyebilir.

**NuGet paketlerini Internet bağlantısı olmadan yüklemek mümkün mü?**

Evet, Scott Hanselman'ın blog gönderisine bakın [nuget.org düştüğünde (veya uçaktaolduğunuzda) NuGet'e nasıl erişilir](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).

**Paketleri varsayılan paketler klasöründen farklı bir konuma nasıl yüklerim?**

[`repositoryPath`](../reference/nuget-config-file.md#config-section) Kullanarak ayarı `Nuget.Config` `nuget config -set repositoryPath=<path>`ayarlayın.

**NuGet paketleri klasörünü kaynak denetimine eklemekten nasıl kaçınırım?**

[`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) Ayarlayın. `Nuget.Config` `true` Bu anahtar çözüm düzeyinde çalışır ve bu nedenle `$(Solutiondir)\.nuget\Nuget.Config` dosyaya eklenmesi gerekir. Visual Studio'dan paket geri yüklemesini etkinleştirmek bu dosyayı otomatik olarak oluşturur.

**Paket geri yüklemeyi nasıl kapatırım?**

Bkz. [Etkinleştirme ve devre dışı bırakma paketi geri yükleme.](../consume-packages/package-restore.md#enable-and-disable-package-restore-in-visual-studio)

**Uzak bağımlılıkları olan yerel bir paket yüklerken neden "Bağımlılık hatasını çözemedim" alıyorum?**

Projeye yerel bir paket yüklerken **Tüm** kaynağı seçmeniz gerekir. Bu, tek bir tane kullanmak yerine tüm akışları toplar. Bu hatanın ortaya çıkmasının nedeni, yerel bir deponun kullanıcılarının genellikle şirket polisleri nedeniyle yanlışlıkla uzak bir paket yüklemekten kaçınmak istemeleridir.

**Aynı klasörde birden fazla projem var, her proje için ayrı paketler.config dosyalarını nasıl kullanabilirim?**

Ayrı projelerin ayrı klasörlerde yaşadığı çoğu projede, NuGet her `packages.config` projedeki dosyaları tanımladığı için bu bir sorun değildir. NuGet 3.3+ ve aynı klasördeki birden fazla proje yle, proje `packages.config` adını dosya adlarına ekleyebilirsiniz deseni `packages.{project-name}.config`kullanın ve NuGet bu dosyayı kullanır.

Her proje dosyası kendi bağımlılık listesini içerdiğinden, PackageReference'ı kullanırken bu bir sorun değildir.

**Depo listemde nuget.org göremiyorum, nasıl geri alabilirim?**

- Kaynak `https://api.nuget.org/v3/index.json` listenize ekleyin veya
- Delete `%appdata%\.nuget\NuGet.Config` (Windows) `~/.nuget/NuGet/NuGet.Config` veya (Mac/Linux) ve NuGet'in yeniden oluşturmasına izin verin.
