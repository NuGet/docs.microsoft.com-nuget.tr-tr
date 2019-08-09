---
title: NuGet sık sorulan sorular
description: NuGet 'i komut satırında ve Visual Studio 'da kullanmak için ortak sorular ve yanıtlar
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 27a925c8748cb2085e8c9fe71ef23281cf9fd553
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860545"
---
# <a name="nuget-frequently-asked-questions"></a>NuGet sık sorulan sorular

**NuGet 'i çalıştırmak için ne gerekir?**

Hem Kullanıcı arabirimi hem de komut satırı araçlarının etrafındaki tüm bilgiler, [Install kılavuzunda](../install-nuget-client-tools.md)bulunabilir.

**NuGet mono destekliyor mu?**

Komut satırı aracı `nuget.exe`, mono 3.2 + altında oluşturulup çalışır ve mono içinde paketler oluşturabilir.

, `nuget.exe` Windows üzerinde tam olarak çalışsa da, Linux ve OS X üzerinde bilinen sorunlar vardır. GitHub 'daki [mono sorunları](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) bölümüne bakın.

Bir [grafik istemci](https://github.com/mrward/monodevelop-nuget-addin) , MonoDevelop için bir eklenti olarak kullanılabilir.

**Bir paketin neleri içerdiğini ve uygulamamın kararlı olduğunu ve yararlı olup olmadığını nasıl belirleyebilirim?**

Bir paket hakkında öğrenme birincil kaynağı, nuget.org (veya başka bir özel akıştaki) listeleme sayfasıdır. Nuget.org üzerindeki her paket sayfasında paketin açıklaması, sürüm geçmişi ve kullanım istatistikleri bulunur. Paket sayfasındaki **bilgi** bölümü Ayrıca, paketin nasıl kullanıldığını öğrenmenize yardımcı olmak için genellikle birçok örnek ve diğer belgeleri bulabileceğiniz projenin Web sitesine bir bağlantı içerir.

Daha fazla bilgi için bkz. [paketleri bulma ve seçme](../consume-packages/finding-and-choosing-packages.md).

## <a name="nuget-in-visual-studio"></a>Visual Studio 'da NuGet

**NuGet farklı Visual Studio ürünlerinde nasıl desteklenir?**

- Windows üzerinde Visual Studio, [Paket Yöneticisi Kullanıcı arabirimini](../consume-packages/install-use-packages-visual-studio.md) ve [Paket Yöneticisi konsolunu](../consume-packages/install-use-packages-powershell.md)destekler.
- Mac için Visual Studio, [projenizde bir NuGet paketi ekleme](/visualstudio/mac/nuget-walkthrough)konusunda açıklandığı gibi yerleşik NuGet özelliklerine sahiptir.
- Visual Studio Code (tüm platformlar) doğrudan bir NuGet tümleştirmesi yoktur. [NUGET CLI](../reference/nuget-exe-cli-reference.md) veya [DotNet CLI](../reference/dotnet-commands.md)kullanın.
- Azure DevOps, [NuGet paketlerini geri yüklemek için bir derleme adımı](/vsts/build-release/tasks/package/nuget)sağlar. Ayrıca, [özel NuGet paket akışlarını Azure DevOps üzerinde](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish)de barındırabilirsiniz.

**Nasıl yaparım?, yüklü olan NuGet araçlarının tam sürümü kontrol edilsin mi?**

Visual Studio 'da **Microsoft Visual Studio hakkında yardım >** komutunu kullanın ve **NuGet Paket Yöneticisi**' nin yanında görüntülenecek sürüme bakın.

Alternatif olarak, Paket Yöneticisi konsolunu (**Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi konsolu**) başlatın ve sürümü `$host` içeren NuGet hakkındaki bilgileri görmek için girin.

**NuGet hangi programlama dillerini destekler?**

NuGet genellikle .NET dilleri için geçerlidir ve .NET kitaplıklarını bir projeye getirmek için tasarlanmıştır. Ayrıca, bazı proje türlerinde MSBuild ve Visual Studio Otomasyonu ' nu desteklediğinden, diğer projeleri ve dilleri de çeşitli derecelerde destekler.

NuGet 'in en son sürümü, Visual Basic C# F#,, Wix ve C++' i destekler.

**NuGet tarafından desteklenen proje şablonları nelerdir?**

NuGet, Windows, Web, Cloud, SharePoint, Wix gibi çeşitli proje şablonları için tam desteğe sahiptir.

**Visual Studio şablonlarının parçası olan Nasıl yaparım? güncelleştirme paketleri mi?**

Paket Yöneticisi Kullanıcı arabirimindeki **güncelleştirmeler** sekmesine gidin ve **Tümünü Güncelleştir**' i seçin [ `Update-Package` ](../reference/ps-reference/ps-ref-update-package.md) ya da paket yöneticisi konsolundan komutunu kullanın.

Şablonun kendisini güncelleştirmek için şablon deposunu el ile güncelleştirmeniz gerekir. Bu konudaki [Xavier Ayrışıcı 'nın bloguna](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) bakın. Tüm bağımlılıkların en son sürümü birbirleriyle uyumlu değilse, el ile yapılan güncelleştirmeler şablonu bozabileceğinden bunun sizin sorumluluğunuzdadır.

**NuGet 'i Visual Studio dışında kullanabilir miyim?**

Evet, NuGet doğrudan komut satırından çalışmaktadır. Bkz. [Install Guide](../install-nuget-client-tools.md) ve [CLI başvurusu](../reference/nuget-exe-cli-reference.md).

## <a name="nuget-command-line"></a>NuGet komut satırı

**NuGet komut satırı aracının en son sürümünü almak Nasıl yaparım??**

Bkz. [Install Guide](../install-nuget-client-tools.md).

**NuGet. exe için lisans nedir?**

NuGet. exe ' yi MıT lisansı koşullarına göre yeniden dağıtmanıza izin verilir. Yeniden dağıtmak üzere seçtiğiniz NuGet. exe ' nin tüm kopyalarını güncelleştirmeden ve bakımını yapmaktan siz sorumlusunuz.

**NuGet komut satırı aracını genişletmek mümkün mü?**

Evet, [ramiz Reynold 'ın Post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx)bölümünde açıklandığı `nuget.exe`gibi öğesine özel komutlar eklemek mümkündür.

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a>NuGet Paket Yöneticisi Konsolu (Windows üzerinde Visual Studio)

**Nasıl yaparım? Paket Yöneticisi konsolundaki DTE nesnesine erişim izni veriyor musunuz?**

Visual Studio Automation nesne modelindeki en üst düzey nesneye DTE (geliştirme araçları ortamı) nesnesi denir. Konsol bunu adlı `$DTE`bir değişken aracılığıyla sağlar. Daha fazla bilgi için bkz. Visual Studio genişletilebilirlik belgelerindeki [Otomasyon modeline genel bakış](/visualstudio/extensibility/internals/automation-model-overview) .

**$DTE değişkenini DTE2 türüne dönüştürmeye çalışırsam, ancak bir hata alıyorum: "EnvDTE. DTEClass" türündeki "EnvDTE. DTEClass" değeri "EnvDTE80. DTE2" türüne dönüştürülemez. Ne oldu?**

Bu, PowerShell 'in bir COM nesnesiyle etkileşime girdiği bilinen bir sorundur. Aşağıdakileri deneyin:

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

`Get-Interface`, NuGet PowerShell ana bilgisayarı tarafından eklenen bir yardımcı işlevdir.

## <a name="creating-and-publishing-packages"></a>Paket oluşturma ve yayımlama

**Nasıl yaparım? bir akışta paketmi Listele?**

Bkz. [paket oluşturma ve yayımlama](../quickstart/create-and-publish-a-package.md).

**.NET Framework farklı sürümlerini hedefleyen kitaplığımın birden çok sürümü var. Bunu destekleyen tek bir paket mi Nasıl yaparım??**

Bkz. [birden çok .NET Framework sürümünü ve profilini destekleme](../create-packages/supporting-multiple-target-frameworks.md).

**Kendi deponuzu mi yoksa akışımı mı ayarlamak Nasıl yaparım??**

[Barındırma paketlerine genel bakış](../hosting-packages/overview.md)bölümüne bakın.

**Paketleri toplu olarak NuGet akışımla nasıl karşıya yükleyebilirim?**

Bkz. [toplu yayımlama NuGet paketleri](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).

## <a name="working-with-packages"></a>Paketlerle çalışma

**Proje düzeyi paket ve çözüm düzeyi paket arasındaki fark nedir?**

Çözüm düzeyindeki bir paket (NuGet 3. x +) bir çözüme yalnızca bir kez yüklenir ve ardından Çözümdeki tüm projeler için kullanılabilir. Proje düzeyindeki bir paket, onu kullanan her bir projeye yüklenir. Çözüm düzeyindeki bir paket, Paket Yöneticisi konsolu içinden çağrılabilecek yeni komutlar de yükleyebilir.

**Internet bağlantısı olmadan NuGet paketleri yüklenebilirsin mi?**

Evet, bkz. Scott Hanselman 'ın blog gönderisi [NuGet.org kapalıysa (veya bir düzlemde olduğunuzda) NuGet 'e erişme](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (Hanselman.com).

**Paketler, varsayılan paketler klasöründen farklı bir konuma yüklensin mi Nasıl yaparım??**

' [`repositoryPath`](../reference/nuget-config-file.md#config-section) `nuget config -set repositoryPath=<path>`Da ayarını kullanarak ayarlayın. `Nuget.Config`

**Nasıl yaparım? NuGet paketleri klasörünü kaynak denetimine eklemektan kaçının mi?**

' İ ' `Nuget.Config` olarak ayarlayın. `true` [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) Bu anahtar çözüm düzeyinde çalışarak, `$(Solutiondir)\.nuget\Nuget.Config` bu nedenle dosyaya eklenmesi gerekir. Visual Studio 'dan paket geri yüklemeyi etkinleştirmek bu dosyayı otomatik olarak oluşturur.

**Paket geri yükleme Nasıl yaparım? kapatılsın mı?**

Bkz. [paket geri yüklemeyi etkinleştirme ve devre dışı bırakma](../consume-packages/package-restore.md#enable-and-disable-package-restore-in-visual-studio).

**Uzak bağımlılıklara sahip yerel bir paket yüklerken neden "bağımlılık hatası çözümlenemiyor" ifadesini alıyorum?**

Projeye yerel bir paket yüklerken **Tüm** kaynağı seçmeniz gerekir. Bu, yalnızca bir tane kullanmak yerine tüm akışların toplamlarını toplar. Bu hatanın nedeni, yerel bir deponun kullanıcıları genellikle şirket ilkeleri nedeniyle yanlışlıkla uzak bir paket yüklemeyi önlemek istemesidir.

**Aynı klasörde birden fazla projem var, her proje için ayrı Packages. config dosyalarını nasıl kullanabilirim?**

Ayrı projelerin ayrı klasörlerde bulunduğu çoğu projede, NuGet her bir projedeki dosyaları tanımladığı için `packages.config` bu bir sorun değildir. NuGet 3.3 + ve aynı klasörde birden çok proje ile, projenin `packages.config` adını dosya adlarıyla `packages.{project-name}.config`ekleyebilirsiniz ve NuGet bu dosyayı kullanır.

Her proje dosyası kendi bağımlılıklar listesini içerdiğinden, PackageReference kullanılırken bu bir sorun değildir.

**Depolar listemdeki nuget.org görmüyorum, nasıl geri alabilirim?**

- Kaynak `https://api.nuget.org/v3/index.json` listenize ekleyin veya
- ( `%appdata%\.nuget\NuGet.Config` Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) öğesini silin ve NuGet 'in yeniden oluşturmasını sağlayın.
