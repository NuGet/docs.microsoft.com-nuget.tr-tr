---
title: NuGet Paket Yöneticisi kullanıcı Arabirimi başvurusu
description: NuGet paketleri ile çalışmak için Visual Studio'da NuGet Paket Yöneticisi kullanıcı Arabirimi kullanma için yönergeler.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/08/2017
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 1d8cb8186b9cedb29918d48539bdf45b130030c0
ms.sourcegitcommit: 00c4c809c69c16fcf4d81012eb53ea22f0691d0b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/16/2018
---
# <a name="nuget-package-manager-ui"></a>NuGet Package Manager UI

Windows Visual Studio'da NuGet Paket Yöneticisi kullanıcı Arabirimi, kolayca yüklemek, kaldırmak ve projeler ve çözümler, NuGet paketlerini güncelleştirmeyi olanak sağlar. Visual Studio'da Mac için deneyimi için bkz: [dahil olmak üzere bir NuGet paketini projenize](/visualstudio/mac/nuget-walkthrough). Paket Yöneticisi kullanıcı Arabirimi ile Visual Studio Code dahil değildir.

Bu konuda:

- [Bulma ve bir paket (Gözat sekmesi) yükleme](#finding-and-installing-a-package)
- [Bir paket (yüklü sekmesi) kaldırılıyor](#uninstalling-a-package)
- [Bir paket (yüklü ve güncelleştirmeleri sekmeleri) güncelleştirme](#updating-a-package) (içeren ["Bir SDK'sı tarafından başvurulan dolaylı olarak" veya "AutoReferenced" iletisi](#implicit_reference))
- [Çözüm paketlerini yönetme](#managing-packages-for-the-solution) (aynı anda birden çok proje ile çalışma).
- [Paket kaynaklarını](#package-sources)
- [Paket Yöneticisi seçeneklerini denetleme](#package-manager-options-control)

> [!Note]
> Visual Studio 2015'te NuGet Paket Yöneticisi kayıpsa denetleyin **Araçlar > Uzantılar ve güncelleştirmeler...**  arayın ve *NuGet Paket Yöneticisi* uzantısı. Visual Studio Uzantıları yükleyici yapamıyorsanız doğrudan uzantısını [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).
>
> Visual Studio 2017 içinde NuGet ve NuGet Paket Yöneticisi otomatik olarak tüm yüklenir. NET ilgili iş yükleri. Tek tek seçerek yüklemek **bileşenleri tek tek > kod Araçlar > NuGet Paket Yöneticisi** Visual Studio 2017 yükleyici seçeneği.

## <a name="finding-and-installing-a-package"></a>Bulma ve bir paket yükleme

1. İçinde **Çözüm Gezgini**, sağ **başvuruları** veya bir proje ve **NuGet paketlerini Yönet...** .

    ![NuGet paketlerini menü seçeneği yönetme](media/ManagePackagesUICommand.png)

1. **Gözat** sekmesi seçili kaynağından popülerliği tarafından paketleri görüntüler (bkz [paketini kaynakları](#package-sources)). Sol üst arama kutusunu kullanarak belirli bir paket için arama yapın. Ayrıca sağlar, bilgilerini görüntülemek için listeden bir paket seçin **yükleme** bir sürüm seçimi açılan birlikte düğmesi.

    ![NuGet paket iletişim Gözat sekmesini yönetme](media/Search.png)

1. Açılan listeden istediğiniz sürümü seçin ve Seç **yükleme**. Visual Studio Paketi ve bağımlılıklarını projeye yükler. Lisans koşullarını kabul etmeniz istenebilir. Yükleme tamamlandığında, eklenen paketler görünür **yüklü** sekmesi. Paketleri de listelenir **başvuruları** projedeki başvurmak olduğunu gösteren Çözüm Gezgini düğümünün `using` deyimleri.

    ![Çözüm Gezgini'nde başvuruların](media/References.png)

> [!Tip]
> Yayın öncesi sürümler dahil ve yayın öncesi sürümler açılan sürümünde kullanılabilir hale getirmek seçin **dahil et** seçeneği.

## <a name="uninstalling-a-package"></a>Bir paketi kaldırma

1. İçinde **Çözüm Gezgini**, sağ **başvuruları** veya istenen proje ' nı seçip **NuGet paketlerini Yönet...** .
1. Seçin **yüklü** sekmesi.
1. (Gerekirse listesini filtrelemek için arama'yı kullanarak) kaldırmak için paketini seçin ve Seç **kaldırma**.

    ![Bir paketi kaldırma](media/UninstallPackage.png)

1. Unutmayın **INCLUDE yayın öncesi** ve **paket kaynağı** denetimleri etkisiz paketleri kaldırırken.

## <a name="updating-a-package"></a>Paket güncelleştirme

1. İçinde **Çözüm Gezgini**, sağ **başvuruları** veya istenen proje ' nı seçip **NuGet paketlerini Yönet...** . (Web sitesi projelerinde sağ **Bin** klasörü.)
1. Seçin **güncelleştirmeleri** sekmesi seçili paketi kaynaklardan kullanılabilir güncelleştirmeleri sahip paketleri görmek için. Seçin **dahil et** ön sürüm paketlerini güncelleştirme listeye dahil edilecek.
1. Güncelleştirme, sağda açılan istediğiniz sürümü seçin ve seçmek için paketi seçin **güncelleştirme**.

    ![Paket güncelleştirme](media/UpdatePackages.png)

1. <a name="implicit_reference"></a>Bazı paketler için **güncelleştirme** düğmesi devre dışıdır ve bunu "örtük olarak bir SDK'sı tarafından başvurulduğundan" bildiren bir ileti görüntülenir (veya "AutoReferenced"). İleti Microsoft.NETCore.App veya Microsoft.NETStandard.Library, gibi paket daha büyük bir çerçeve veya SDK parçasıdır ve bağımsız olarak güncellenmemelidir gösterir. (Gibi paketlerin dahili olarak işaretlenir `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) Güncelleştirme Paketi için paket adını içeren SDK'dan çıkarımını yapma ait olduğu, SDK güncelleştirin. Örneğin, .NET Core SDK parçası paketidir Microsoft.NETCore.App gibi bu nedenle, .NET Core SDK yükleme güncelleştirmeniz gerekir.

    ![Örnek paket başvuruları veya AutoReferenced dolaylı olarak işaretli](media/PackageManagerUIAutoReferenced.png)

1. Birden çok paket yeni sürümlerine güncelleştirmek için bunları seçin ve liste içinde seçin **güncelleştirme** düğmesi listesinin üstünde.
1. Ayrıca tek bir paketi güncelleştirebilirsiniz **yüklü** sekmesi. Bu durumda, bir sürüm Seçici Paket ayrıntılarını içerir (tabi **INCLUDE yayın öncesi** seçeneği) ve bir **güncelleştirme** düğmesi.

## <a name="managing-packages-for-the-solution"></a>Çözüm paketlerini yönetme

Çözüm paketlerini yönetme, aynı anda birden çok projelerle çalışmak için kullanışlı bir yoludur.

1. Seçin **Araçlar > NuGet Paket Yöneticisi > çözüm için NuGet paketlerini Yönet...**  menü komutunu veya çözüme sağ tıklayın ve seçin **NuGet paketlerini Yönet...** :

    ![Çözüm için NuGet paketlerini Yönet](media/ManagePackagesSolutionUICommand.png)

1. Çözüm için paketlerini yönetirken, işlemleri tarafından etkilenen projeleri seçin kullanıcı Arabirimi sağlar:

    ![Çözüm için paketlerini yönetirken proje Seçici](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a>Sekme birleştirin

Geliştiriciler genellikle aynı çözümde farklı projeler arasında aynı NuGet paketi farklı sürümlerini kullanan hatalı bir uygulama düşünün. Çözüm paketlerini yönetmek seçtiğinizde, Paket Yöneticisi kullanıcı Arabirimi sağlayan bir **Birleştir** üzerinde kolayca görebileceğiniz farklı sürüm numaralarını paketlerle çözümdeki farklı projeler tarafından kullanıldığı sekmesi:

![Paket Yöneticisi kullanıcı Arabirimi birleştirmek sekmesi](media/ConsolidateTab.png)

Bu örnekte, ConsoleApp1 EntityFramework 6.1.0 kullanıyor ancak ClassLibrary1 projesindeki EntityFramework 6.2.0, kullanıyor. Paket sürümlerinin birleştirmek için aşağıdakileri yapın:

- Proje listesinde güncelleştirmek için projeleri seçin.
- Bu tüm projelerde kullanmak için sürüm seçin **sürüm** EntityFramework 6.2.0 gibi denetim.
- Seçin **yükleme** düğmesi.

Paket Yöneticisi daha sonra paket artık görünür üzerinde tüm seçili projelerine seçili Paket sürümü yükler **Birleştir** sekmesi.

## <a name="package-sources"></a>Paket kaynaklarını

Visual Studio paketleri aldığı kaynağını değiştirmek için bir kaynak seçici seçin:

![Paket kaynak seçicide Paket Yöneticisi kullanıcı Arabirimi](media/PackageSourceDropDown.png)

Paket kaynaklarını yönetmek için:

1. Seçin **ayarları** Paket Yöneticisi kullanıcı Arabirimi simgesine aşağıda açıklanan veya kullanmak **Araçlar > Seçenekler** komut ve kaydırma **NuGet Paket Yöneticisi**:

    ![Paket Yöneticisi kullanıcı Arabirimi ayarları simgesi](media/PackageSourceSettings.png)

1. Seçin **paket kaynaklarını** düğümü:

    ![Paket kaynağı seçenekleri](media/options.png)

1. Bir kaynak eklemek için seçin **+**, ad düzenleme, URL veya yol girin **kaynak** denetlemek ve seçin **güncelleştirme**. Kaynak Seçici açılan artık görünür.
1. Paket kaynağı değiştirmek için seçmek, içinde düzenlemeler **adı** ve **kaynak** kutuları ' nı seçip **güncelleştirme**.
1. Paket kaynağı devre dışı bırakmak için listeden adı solundaki kutusunu temizleyin.
1. Paket kaynağı kaldırmak için onu seçin ve ardından **X** düğmesi.
1. Yukarı ve aşağı ok düğmelerini paket kaynaklarını öncelik sırasını değiştirmek için. Visual Studio projesi için paketleri geri yüklenirken bu kaynakları öncelik sırasına göre arar. Daha fazla bilgi için bkz: [paket geri yüklemesi](../consume-packages/package-restore.md).

> [!Tip]
> Paket kaynağı sildikten sonra görünürse, bir bilgisayar düzeyinde veya kullanıcı düzeyi listelenmeyebilir `NuGet.Config` dosyaları. Bkz: [NuGet yapılandırma davranışı](../consume-packages/configuring-nuget-behavior.md) bu dosyaları için konum ardından dosyaları el ile düzenleme veya kullanarak kaynak kaldırın [nuget kaynakları komutu](../tools/nuget-exe-CLI-reference.md).

## <a name="package-manager-options-control"></a>Paket Yöneticisi seçeneklerini denetleme

Bir paket seçildiğinde, küçük bir paket Yöneticisi kullanıcı Arabirimi görüntüler Genişletilebilir **seçenekleri** (her ikisi de daraltılmış ve genişletilmiş aşağıda gösterilen) sürüm Seçici altına denetimi. Bazı proje türleri, yalnızca unutmayın **Göster önizleme penceresi** seçeneği sağlanır.

![Paket Yöneticisi seçenekleri](media/PackageManagerUIOptions.png)

Aşağıdaki bölümlerde bu seçenekler açıklanmaktadır.

### <a name="show-preview-window"></a>Önizleme penceresi Göster

Paket yüklenmeden önce kalıcı pencere seçildiğinde, seçilen Paket bağımlılıklarını görüntüler:

![Örnek Önizleme iletişim kutusu](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a>Yükleme ve güncelleme seçenekleri

(Mevcut değil tüm türleri proje için.)

**Bağımlılık davranışı** NuGet yüklemek için bağımlı paketler hangi sürümlerinin nasıl karar yapılandırır:

- *Bağımlılıklar Yoksay* tüm bağımlılıkları genellikle yüklenen paket kıran yükleme atlar.
- *En düşük* [Varsayılan] birincil seçilen paketi gereksinimlerini karşılayan en az sürüm numarasına sahip bağımlılık yükler.
- *En yüksek düzeltme eki* aynı birincil ve ikincil sürüm numaralarını, ancak en yüksek düzeltme numarası ile yeni sürümü yükler. Sürüm 1.2.2 belirtilmişse, örneğin, ardından 1.2 ile başlayan yüksek sürümü yüklenir
- *En yüksek ikincil* aynı büyük sürüm numarasına ancak en yüksek ikincil numarası ve düzeltme numarası ile yeni sürümü yükler. Sürüm 1.2.2 belirtilirse, 1 ile başlayan en yüksek sürüm yüklenir
- *En yüksek* paketi en yüksek kullanılabilir sürümünü yükler.

**Dosya çakışma eylem** NuGet proje veya yerel makine zaten paketleri nasıl yöneteceğini belirtir:

- *Komut İstemi* tutun veya var olan paketler üzerine sormak için NuGet bildirir.
- *Tüm Yoksay* herhangi bir varolan paket üzerine atlamak için NuGet bildirir.
- *Tüm üzerine* herhangi bir varolan paket üzerine yazmak için NuGet bildirir.

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a>Kaldırma seçenekleri

(Mevcut değil tüm türleri proje için.)

**Bağımlılıkları kaldırın**: Bunlar başka bir projede başvurulmayan seçili olduğunda, tüm bağımlı paketler kaldırır.

**Zorla kaldırın olsa bile bağımlılıklar üzerinde**: projede başvuruluyor olsa bile, seçili olduğunda, bir paketi kaldırır. Bu genellikle ile birlikte kullanılır **kaldırmak bağımlılıkları** ve her bir paketi kaldırmak için yüklü bağımlılıkları. Bu seçeneği kullanarak ancak projedeki bozuk başvurularda açabilir. Böyle durumlarda, gerekebilir [bu diğer paketleri yeniden](../consume-packages/reinstalling-and-updating-packages.md).
