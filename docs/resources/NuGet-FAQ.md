---
title: NuGet Frequently-Asked soruları
description: NuGet 'i komut satırında ve Visual Studio 'da kullanmak için ortak sorular ve yanıtlar
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: aae6f0474cc6e8e8aa5c269b79be6fd949d9184c
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238003"
---
# <a name="nuget-frequently-asked-questions"></a>NuGet sık sorulan sorular

NuGet.org hesabı soruları gibi NuGet.org ile ilgili sık sorulan sorular için bkz. [NuGet.org sık sorulan sorular](../nuget-org/nuget-org-faq.md).

**NuGet 'i çalıştırmak için ne gerekir?**

Hem Kullanıcı arabirimi hem de komut satırı araçlarının etrafındaki tüm bilgiler, [Install kılavuzunda](../install-nuget-client-tools.md)bulunabilir.

**NuGet mono destekliyor mu?**

Komut satırı aracı, `nuget.exe` mono 3.2 + altında oluşturulup çalışır ve mono içinde paketler oluşturabilir.

`nuget.exe`, Windows üzerinde tam olarak çalışsa da, Linux ve OS X üzerinde bilinen sorunlar vardır. GitHub 'Daki [mono sorunları](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) bölümüne bakın.

Bir [grafik istemci](https://github.com/mrward/monodevelop-nuget-addin) , MonoDevelop için bir eklenti olarak kullanılabilir.

**Bir paketin neleri içerdiğini ve uygulamamın kararlı olduğunu ve yararlı olup olmadığını nasıl belirleyebilirim?**

Bir paket hakkında öğrenme birincil kaynağı, nuget.org (veya başka bir özel akıştaki) listeleme sayfasıdır. Nuget.org üzerindeki her paket sayfasında paketin açıklaması, sürüm geçmişi ve kullanım istatistikleri bulunur. Paket sayfasındaki **bilgi** bölümü Ayrıca, paketin nasıl kullanıldığını öğrenmenize yardımcı olmak için genellikle birçok örnek ve diğer belgeleri bulabileceğiniz projenin Web sitesine bir bağlantı içerir.

Daha fazla bilgi için bkz. [paketleri bulma ve seçme](../consume-packages/finding-and-choosing-packages.md).

## <a name="nuget-in-visual-studio"></a>Visual Studio 'da NuGet

**NuGet farklı Visual Studio ürünlerinde nasıl desteklenir?**

- Windows üzerinde Visual Studio, [Paket Yöneticisi Kullanıcı arabirimini](../consume-packages/install-use-packages-visual-studio.md) ve [Paket Yöneticisi konsolunu](../consume-packages/install-use-packages-powershell.md)destekler.
- Mac için Visual Studio, [projenizde bir NuGet paketi ekleme](/visualstudio/mac/nuget-walkthrough)konusunda açıklandığı gibi yerleşik NuGet özelliklerine sahiptir.
- Visual Studio Code (tüm platformlar) doğrudan bir NuGet tümleştirmesi yoktur. [NUGET CLI](../reference/nuget-exe-cli-reference.md) veya [DotNet CLI](../reference/dotnet-commands.md)kullanın.
- Azure DevOps, [NuGet paketlerini geri yüklemek için bir derleme adımı](/vsts/build-release/tasks/package/nuget)sağlar. Ayrıca, [özel NuGet paket akışlarını Azure DevOps üzerinde de barındırabilirsiniz](/azure/devops/artifacts/nuget/publish).

**Nasıl yaparım?, yüklü olan NuGet araçlarının tam sürümü kontrol edilsin mi?**

Visual Studio 'da **Microsoft Visual Studio hakkında yardım >** komutunu kullanın ve **NuGet Paket Yöneticisi** ' nin yanında görüntülenecek sürüme bakın.

Alternatif olarak, Paket Yöneticisi konsolunu ( **araçlar > NuGet paket yöneticisi > Paket Yöneticisi konsolu** ) başlatın ve `$host` sürümü içeren NuGet hakkındaki bilgileri görmek için girin.

**NuGet hangi programlama dillerini destekler?**

NuGet genellikle .NET dilleri için geçerlidir ve .NET kitaplıklarını bir projeye getirmek için tasarlanmıştır. Ayrıca, bazı proje türlerinde MSBuild ve Visual Studio Otomasyonu ' nu desteklediğinden, diğer projeleri ve dilleri de çeşitli derecelerde destekler.

NuGet 'in en son sürümü C#, Visual Basic, F #, WiX ve C++ sürümlerini destekler.

**NuGet tarafından desteklenen proje şablonları nelerdir?**

NuGet, Windows, Web, Cloud, SharePoint, Wix gibi çeşitli proje şablonları için tam desteğe sahiptir.

**Visual Studio şablonlarının parçası olan Nasıl yaparım? güncelleştirme paketleri mi?**

Paket Yöneticisi Kullanıcı arabirimindeki **güncelleştirmeler** sekmesine gidin ve **Tümünü Güncelleştir** ' i seçin ya da paket yöneticisi konsolundan [ `Update-Package` komutunu](../reference/ps-reference/ps-ref-update-package.md) kullanın.

Şablonun kendisini güncelleştirmek için şablon deposunu el ile güncelleştirmeniz gerekir. Bu konudaki [Xavier Ayrışıcı 'nın bloguna](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) bakın. Tüm bağımlılıkların en son sürümü birbirleriyle uyumlu değilse, el ile yapılan güncelleştirmeler şablonu bozabileceğinden bunun sizin sorumluluğunuzdadır.

**NuGet 'i Visual Studio dışında kullanabilir miyim?**

Evet, NuGet doğrudan komut satırından çalışmaktadır. Bkz. [Install Guide](../install-nuget-client-tools.md) ve [CLI başvurusu](../reference/nuget-exe-cli-reference.md).

## <a name="nuget-command-line"></a>NuGet komut satırı

**NuGet komut satırı aracının en son sürümünü almak Nasıl yaparım??**

Bkz. [Install Guide](../install-nuget-client-tools.md). Aracın geçerli yüklü sürümünü denetlemek için kullanın `nuget help` .

**nuget.exe için lisans nedir?**

nuget.exe, MıT lisansı koşullarına göre yeniden dağıtmanıza izin verilir. Yeniden dağıtmak için seçtiğiniz nuget.exe kopyalarının güncelleştirilmesi ve bakımı konusunda siz sorumlusunuz.

**NuGet komut satırı aracını genişletmek mümkün mü?**

Evet, `nuget.exe` [ramiz Reynold 'ın Post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx)bölümünde açıklandığı gibi öğesine özel komutlar eklemek mümkündür.

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a>NuGet Paket Yöneticisi Konsolu (Windows üzerinde Visual Studio)

**Nasıl yaparım? Paket Yöneticisi konsolundaki DTE nesnesine erişim izni veriyor musunuz?**

Visual Studio Automation nesne modelindeki en üst düzey nesneye DTE (geliştirme araçları ortamı) nesnesi denir. Konsol bunu adlı bir değişken aracılığıyla sağlar `$DTE` . Daha fazla bilgi için bkz. Visual Studio genişletilebilirlik belgelerindeki [Otomasyon modeline genel bakış](/visualstudio/extensibility/internals/automation-model-overview) .

**$DTE değişkenini DTE2 türüne dönüştürmeye çalışırsam, ancak hata alıyorum: "EnvDTE. DTEClass" türündeki "EnvDTE. DTEClass" değeri "EnvDTE80. DTE2" türüne dönüştürülemez. Ne oldu?**

Bu, PowerShell 'in bir COM nesnesiyle etkileşime girdiği bilinen bir sorundur. Aşağıdaki işlemi deneyin:

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

`Get-Interface` , NuGet PowerShell ana bilgisayarı tarafından eklenen bir yardımcı işlevdir.

## <a name="creating-and-publishing-packages"></a>Paket oluşturma ve yayımlama

**Nasıl yaparım? bir akışta paketmi Listele?**

Bkz. [paket oluşturma ve yayımlama](../quickstart/create-and-publish-a-package-using-visual-studio.md).

**.NET Framework farklı sürümlerini hedefleyen kitaplığımın birden çok sürümü var. Bunu destekleyen tek bir paket mi Nasıl yaparım??**

Bkz. [birden çok .NET Framework sürümünü ve profilini destekleme](../create-packages/supporting-multiple-target-frameworks.md).

**Kendi deponuzu mi yoksa akışımı mı ayarlamak Nasıl yaparım??**

[Barındırma paketlerine genel bakış](../hosting-packages/overview.md)bölümüne bakın.

**Paketleri toplu olarak NuGet akışımla nasıl karşıya yükleyebilirim?**

Bkz. [toplu yayımlama NuGet paketleri](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).

## <a name="working-with-packages"></a>Paketlerle çalışma

**Internet bağlantısı olmadan NuGet paketleri yüklenebilirsin mi?**

Evet, bkz. Scott Hanselman 'ın blog gönderisi [NuGet.org kapalıysa (veya bir düzlemde olduğunuzda) NuGet 'e erişme](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (Hanselman.com).

**Paketler, varsayılan paketler klasöründen farklı bir konuma yüklensin mi Nasıl yaparım??**

' Da [`repositoryPath`](../reference/nuget-config-file.md#config-section) ayarını `Nuget.Config` kullanarak ayarlayın `nuget config -set repositoryPath=<path>` .

**Nasıl yaparım? NuGet paketleri klasörünü kaynak denetimine eklemektan kaçının mi?**

' İ [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) ' olarak ayarlayın `Nuget.Config` `true` . Bu anahtar çözüm düzeyinde çalışarak, bu nedenle dosyaya eklenmesi gerekir `$(Solutiondir)\.nuget\Nuget.Config` . Visual Studio 'dan paket geri yüklemeyi etkinleştirmek bu dosyayı otomatik olarak oluşturur.

**Paket geri yükleme Nasıl yaparım? kapatılsın mı?**

Bkz. [paket geri yüklemeyi etkinleştirme ve devre dışı bırakma](../consume-packages/package-restore.md#enable-and-disable-package-restore-in-visual-studio).

**Uzak bağımlılıklara sahip yerel bir paket yüklerken neden "bağımlılık hatası çözümlenemiyor" ifadesini alıyorum?**

Projeye yerel bir paket yüklerken **Tüm** kaynağı seçmeniz gerekir. Bu, yalnızca bir tane kullanmak yerine tüm akışların toplamlarını toplar. Bu hatanın nedeni, yerel bir deponun kullanıcıları genellikle şirket ilkeleri nedeniyle yanlışlıkla uzak bir paket yüklemeyi önlemek istemesidir.

**Aynı klasörde birden fazla projem var, her proje için ayrı packages.config dosyalarını nasıl kullanabilirim?**

Ayrı projelerin ayrı klasörlerde bulunduğu çoğu projede, NuGet her bir projedeki dosyaları tanımladığı için bu bir sorun değildir `packages.config` . NuGet 3.3 + ve aynı klasörde birden çok proje ile, projenin adını `packages.config` dosya adlarıyla ekleyebilirsiniz `packages.{project-name}.config` ve NuGet bu dosyayı kullanır.

Her proje dosyası kendi bağımlılıklar listesini içerdiğinden, PackageReference kullanılırken bu bir sorun değildir.

**Depolar listemdeki nuget.org görmüyorum, nasıl geri alabilirim?**

- `https://api.nuget.org/v3/index.json`Kaynak listenize ekleyin veya
- `%appdata%\.nuget\NuGet.Config`(Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) öğesini silin ve NuGet 'in yeniden oluşturmasını sağlayın.