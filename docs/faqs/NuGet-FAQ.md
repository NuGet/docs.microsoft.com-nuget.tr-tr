---
title: NuGet sık sorulan sorular
description: Sık sorulan sorular ve yanıtlar komut satırında ve Visual Studio'da NuGet kullanma
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 20a55c6ba89478e70d8e6837aaebc1b7b7754a93
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842431"
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
- Azure DevOps sağlar [NuGet paketlerini geri yüklemek için bir derleme adımı](/vsts/build-release/tasks/package/nuget). Ayrıca [konak özel NuGet paketi üzerinde Azure DevOps akışları](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish).

**Yüklü olan NuGet Araçları'nın tam sürümünü nasıl kontrol edebilirim?**

Visual Studio'da kullanmak **Yardım > Microsoft Visual Studio hakkında** komut ve görüntülendiğini sürümde Ara **NuGet Paket Yöneticisi**.

Alternatif olarak, Paket Yöneticisi konsolu başlatın (**Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Konsolu**) girin `$host` NuGet sürümü dahil olmak üzere hakkındaki bilgileri görmek için.

**Hangi programlama dillerini NuGet tarafından destekleniyor mu?**

NuGet, genellikle .NET dilleri için çalışır ve bir projeye .NET kitaplıkları getirmek için tasarlanmıştır. Ayrıca bazı proje türlerinde MSBuild ve Visual Studio Otomasyonu desteklediği için diğer projeleri ve çeşitli dereceye dilleri de destekler.

En son NuGet sürümünü destekleyen C#, Visual Basic F#, WiX ve C++.

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

Bkz: [etkinleştirme ve devre dışı paket geri yükleme](../consume-packages/package-restore.md#enable-and-disable-package-restore-visual-studio).

**Neden alabilirim "bağımlılık hatayı gidermek için yapılandırılamıyor" ne zaman yerel paket ile uzak Bağımlılıkların yüklenmesi?**

Seçmenize gerek **tüm** projeye yerel bir paket yükleme sırasında kaynak. Bu, yalnızca bir tane yerine tüm akışları toplar. Bu hatanın görünür bir yerel depo kullanıcıları genellikle yanlışlıkla önlemek istediğiniz nedeni Kurumsal nedeniyle uzak bir paketi yükleme ilkeleri.

**Aynı klasörde birden çok proje sahibim, ayrı packages.config dosyaları her proje için nasıl kullanabilirim?**

NuGet tanımlar burada ayrı projeler Canlı ayrı klasörlerde çoğu projelerinde, bu bir sorun değildir `packages.config` her proje dosyaları. NuGet 3.3 + ve birden çok ile aynı klasörde yer alan projeler, projeye adı ekleyebilirsiniz `packages.config` dosya adlarını desenini kullanın `packages.{project-name}.config`, ve bu dosyayı NuGet kullanır.

Her proje dosyası kendi listesi bağımlılıklar içerdiğinden bu soruna PackageReference, kullanırken değil.

**Depolarımın listesini nuget.org göremiyorum, nasıl geri alabilirim?**

- Ekleme `https://api.nuget.org/v3/index.json` listenize kaynakları, veya
- Silme `%appdata%\.nuget\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) ve NuGet yeniden oluşturun.
