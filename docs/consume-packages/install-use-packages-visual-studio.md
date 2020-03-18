---
title: Visual Studio 'da NuGet paketlerini yükleyip yönetme
description: NuGet paketleri ile çalışma için Visual Studio 'da NuGet Paket Yöneticisi Kullanıcı arabirimini kullanmaya yönelik yönergeler.
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 3adceac8c725d9ea1610aea090753c9c1d8bc818
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428697"
---
# <a name="install-and-manage-packages-in-visual-studio-using-the-nuget-package-manager"></a>NuGet Paket Yöneticisi 'Ni kullanarak Visual Studio 'da paket yükleyip yönetme

Windows üzerinde Visual Studio 'daki NuGet Paket Yöneticisi Kullanıcı arabirimi, projelerde ve çözümlerde NuGet paketlerini kolayca yüklemenize, kaldırmanıza ve güncelleştirmenize olanak tanır. Mac için Visual Studio deneyim için, bkz. [projenizde bir NuGet paketi ekleme](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json). Paket Yöneticisi Kullanıcı arabirimi Visual Studio Code dahil değildir.

> [!NOTE]
> Visual Studio 2015 ' de NuGet Paket Yöneticisi eksik ise **araçlar > Uzantılar ve güncelleştirmeler...** ' ı Işaretleyin ve *NuGet Paket Yöneticisi* uzantısını arayın. Visual Studio 'da uzantılar yükleyicisini kullandıysanız, uzantıyı doğrudan [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)' den indirin.
>
> Visual Studio 2017 ' den başlayarak NuGet ve NuGet Paket Yöneticisi ile birlikte otomatik olarak yüklenir. NET ilgili iş yükleri. Visual Studio yükleyicisindeki **tek tek bileşenler > kod araçları > NuGet Paket Yöneticisi** seçeneğini seçerek tek tek yükleme yapın.

## <a name="find-and-install-a-package"></a>Paket bulma ve yüklemeyi

1. **Çözüm Gezgini**, **başvuruya** veya bir projeye sağ tıklayın ve **NuGet Paketlerini Yönet..** . seçeneğini belirleyin.

    ![NuGet Paketlerini Yönet menü seçeneği](media/ManagePackagesUICommand.png)

1. **Gözden** geçirme sekmesi, paketleri şu anda seçili olan kaynaktan popülerlik olarak görüntüler (bkz. [paket kaynakları](#package-sources)). Sol üstteki arama kutusunu kullanarak belirli bir paketi arayın. Bilgileri göstermek için listeden bir paket seçin. Bu, Ayrıca, bir sürüm seçimi açılır ile birlikte de **Install** düğmesine de olanak sağlar.

    ![NuGet Paketlerini Yönet Iletişim kutusu tarama sekmesi](media/Search.png)

1. Açılan listeden istediğiniz **sürümü seçin ve**ardından Kaldır ' ı seçin. Visual Studio, paketi ve bağımlılıklarını projeye kurar. Lisans koşullarını kabul etmeniz istenebilir. Yükleme tamamlandığında, eklenen paketler **yüklü** sekmesinde görünür. paketler ayrıca, Çözüm Gezgini **Başvurular** düğümünde listelenir ve bu, bunlara `using` deyimleriyle projede başvurabileceğiniz anlamına gelen.

    ![Çözüm Gezgini başvurular](media/References.png)

> [!Tip]
> Aramaya yayın öncesi sürümleri eklemek ve sürüm açılır penceresinde ön sürüm sürümlerini kullanabilmek için, **ön sürümü dahil et** seçeneğini belirleyin.

> [!Note]
> NuGet, bir projenin paketleri kullanabileceği iki biçimi vardır: [`PackageReference`](package-references-in-project-files.md) ve [`packages.config`](../reference/packages-config.md). [Varsayılan, Visual Studio 'nun seçenekler penceresinde ayarlanabilir](Package-Restore.md#choose-default-package-management-format).

## <a name="uninstall-a-package"></a>Bir paketi kaldırma

1. **Çözüm Gezgini**, **başvuruya** veya istenen projeye sağ tıklayın ve **NuGet Paketlerini Yönet...** seçeneğini belirleyin.
1. **Yüklü öğeler** sekmesini seçin.
1. Kaldırılacak paketi seçin (gerekirse listeyi filtrelemek için arama ' yı kullanarak) ve **Kaldır**' ı seçin.

    ![Paket kaldırılıyor](media/UninstallPackage.png)

1. Paket kaldırılırken, **ön sürümü** ve **paket kaynak** denetimlerinin dahil edileceğini unutmayın.

## <a name="update-a-package"></a>Bir paketi güncelleştirme

1. **Çözüm Gezgini**, **başvuruya** veya istenen projeye sağ tıklayın ve **NuGet Paketlerini Yönet...** seçeneğini belirleyin. (Web sitesi projelerinde **bin** klasörüne sağ tıklayın.)
1. Seçilen paket kaynaklarından kullanılabilir güncelleştirmeleri olan paketleri görmek için **güncelleştirmeler** sekmesini seçin. Güncelleştirme listesine yayın öncesi paketleri dahil etmek için **ön sürümü dahil et** ' i seçin.
1. Güncelleştirilecek paketi seçin, sağ taraftaki açılan listeden istediğiniz sürümü seçin ve **Güncelleştir**' i seçin.

    ![Paket güncelleştiriliyor](media/UpdatePackages.png)

1. <a name="implicit_reference"></a>Bazı paketlerde **Güncelleştir** düğmesi devre dışıdır ve "bir SDK tarafından örtük olarak başvurulduğunu" (veya "Oto başvurulan") bildiren bir ileti görüntülenir. Bu ileti, paketin daha büyük bir Framework veya SDK 'nın parçası olduğunu ve bağımsız olarak güncelleştirilmemiş olduğunu gösterir. (Bu tür paketler dahili olarak `<IsImplicitlyDefined>True</IsImplicitlyDefined>`olarak işaretlenir.) Örneğin, `Microsoft.NETCore.App` .NET Core SDK bir parçasıdır ve paket sürümü, uygulama tarafından kullanılan çalışma zamanı çerçevesinin sürümü ile aynı değildir. ASP.NET Core ve .NET Core çalışma zamanının yeni sürümlerini almak için [.NET Core yüklemenizi güncelleştirmeniz](https://aka.ms/dotnet-download) gerekir. [.NET Core Metapackages ve sürüm oluşturma hakkında daha fazla bilgi için bu belgeye bakın](/dotnet/core/packages). Bu, aşağıdaki yaygın olarak kullanılan paketler için geçerlidir:
    * Microsoft.AspNetCore.All
    * Microsoft.AspNetCore.App
    * Microsoft. NETCore. app
    * NETStandard. Library

    ![Örtülü başvurular veya oto başvurulan olarak işaretlenen örnek paket](media/PackageManagerUIAutoReferenced.png)

1. Birden çok paketi en yeni sürümlerine güncelleştirmek için listeden seçin ve listenin üzerindeki **Güncelleştir** düğmesini seçin.
1. Ayrıca, **yüklü** sekmesinden tek bir paketi de güncelleştirebilirsiniz. Bu durumda, paketin ayrıntıları bir sürüm seçici ( **ön sürümü dahil et** seçeneğine tabidir) ve bir **Güncelleştir** düğmesi içerir.

## <a name="manage-packages-for-the-solution"></a>Çözüm için paketleri yönetme

Bir çözüm için paketlerin yönetilmesi, birden çok projeyle aynı anda çalışması için uygun bir yoldur.

1. **NuGet paket yöneticisi > araçlar > çözüm Için NuGet Paketlerini Yönet..** . menü komutunu seçin veya çözüme sağ tıklayıp **NuGet Paketlerini Yönet..** . öğesini seçin:

    ![Çözüm için NuGet Paketlerini Yönet](media/ManagePackagesSolutionUICommand.png)

1. Çözüm için paketleri yönetirken, Kullanıcı arabirimi işlemlerden etkilenen projeleri seçmenizi sağlar:

    ![Çözüm için paketleri yönetirken proje Seçicisi](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a>Birleştirme sekmesi

Geliştiriciler tipik olarak aynı NuGet paketinin farklı sürümlerini aynı çözümde farklı projeler arasında kullanmak için kötü bir uygulama ele alalım. Bir çözüm için paketleri yönetmeyi seçtiğinizde, Paket Yöneticisi Kullanıcı arabirimi, farklı sürüm numaralarına sahip paketlerin çözümdeki farklı projeler tarafından kullanıldığı yerleri kolayca görebileceğiniz bir **birleştirme** sekmesi sağlar:

![Paket Yöneticisi UI birleştirme sekmesi](media/ConsolidateTab.png)

Bu örnekte, ClassLibrary1 projesi EntityFramework 6.2.0 kullanıyor, ancak ConsoleApp1 EntityFramework 6.1.0 kullanıyor. Paket sürümlerini birleştirmek için aşağıdakileri yapın:

- Proje listesinde güncelleştirilecek projeleri seçin.
- **Sürüm** denetimindeki tüm projelerde kullanılacak sürümü (EntityFramework 6.2.0 gibi) seçin.
- **Install** düğmesini seçin.

Paket Yöneticisi seçili paket sürümünü seçili tüm projelere yükleyerek, bu paket artık **birleştirme** sekmesinde görünmez.

## <a name="package-sources"></a>Paket kaynakları

Visual Studio 'Nun paketleri alacağı kaynağı değiştirmek için kaynak seçiciden birini seçin:

![Paket Yöneticisi Kullanıcı arabiriminde paket kaynak Seçicisi](media/PackageSourceDropDown.png)

Paket kaynaklarını yönetmek için:

1. Aşağıda belirtilen Paket Yöneticisi Kullanıcı arabirimindeki **Ayarlar** simgesini seçin veya **Araçlar > Seçenekler** komutunu kullanın ve **NuGet Paket Yöneticisi**' ne kaydırın:

    ![Paket Yöneticisi Kullanıcı arabirimi ayarları simgesi](media/PackageSourceSettings.png)

1. **Paket kaynakları** düğümünü seçin:

    ![Paket kaynakları seçenekleri](media/options.png)

1. Kaynak eklemek için **+** seçin, adı düzenleyin, **kaynak** denetimine URL veya yol girin ve **Güncelleştir**' i seçin. Kaynak artık seçici açılan penceresinde görünür.
1. Bir paket kaynağını değiştirmek için, seçin, **ad** ve **kaynak** kutularında düzenlemeler yapın ve **Güncelleştir**' i seçin.
1. Bir paket kaynağını devre dışı bırakmak için listedeki adının solundaki kutuyu temizleyin.
1. Bir paket kaynağını kaldırmak için, seçin ve sonra **X** düğmesini seçin.
1. Yukarı ve aşağı ok düğmelerinin kullanılması, paket kaynaklarının öncelik sırasını değiştirmez. Visual Studio, isteklere yanıt vermek için ilk kaynak olan paketin kullanıldığı paket kaynaklarının sırasını yoksayar. Daha fazla bilgi için bkz. [paket geri yükleme](../consume-packages/package-restore.md).

> [!Tip]
> Bir paket kaynağı silindikten sonra yeniden görünürse, bilgisayar düzeyinde veya kullanıcı düzeyindeki `NuGet.Config` dosyalarında listelenmiş olabilir. Bu dosyaların konumu için [ortak NuGet yapılandırmalarına](../consume-packages/configuring-nuget-behavior.md) bakın, ardından dosyaları el ile düzenleyerek veya [NuGet kaynakları komutunu](../reference/nuget-exe-CLI-reference.md)kullanarak kaynağı kaldırın.

## <a name="package-manager-options-control"></a>Paket Yöneticisi seçenekler denetimi

Bir paket seçildiğinde, Paket Yöneticisi Kullanıcı arabirimi, sürüm seçicinin altında küçük, genişletilebilir bir **Seçenekler** denetimi görüntüler (burada hem daraltılmış hem de genişletilmiş olarak gösterilmiştir). Bazı proje türleri için yalnızca **Önizleme penceresini göster** seçeneğinin sağlandığını unutmayın.

![Paket Yöneticisi seçenekleri](media/PackageManagerUIOptions.png)

Aşağıdaki bölümlerde bu seçenekler açıklanmaktadır.

### <a name="show-preview-window"></a>Önizleme penceresini göster

Seçildiğinde, bir kalıcı pencere, paket yüklenmeden önce seçilen bir paketin bağımlılıklarını görüntüler:

![Örnek önizleme Iletişim kutusu](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a>Yüklemeyi ve güncelleştirme seçenekleri

(Tüm proje türleri için kullanılamaz.)

**Bağımlılık davranışı** , NuGet 'in hangi bağımlı paket sürümlerinin yükleneceğini nasıl karar verdiği hakkında bir yapılandırma sağlar:

- *Bağımlılıkları yoksay* , genellikle yüklenen paketi kesen tüm bağımlılıkları yüklemeyi atlar.
- *En düşük* [varsayılan] bağımlılığı, seçilen birincil paketin gereksinimlerini karşılayan en az sürüm numarasıyla birlikte kurar.
- *En yüksek düzeltme eki* , aynı büyük ve küçük sürüm numaralarına sahip sürümü, ancak en yüksek düzeltme eki numarasını yüklüyor. Örneğin, 1.2.2 sürümü belirtilmişse 1,2 ile başlayan en yüksek sürüm yüklenir
- *En yüksek ikincil* sürüm, aynı ana sürüm numarası, ancak en yüksek küçük sayı ve düzeltme eki numarası ile birlikte yüklenir. Sürüm 1.2.2 belirtilmişse, 1 ile başlayan en yüksek sürüm yüklenir
- *En yüksek* paketin kullanılabilir en yüksek sürümünü yükleme.

**Dosya çakışması eylemi** , NuGet 'in projede veya yerel makinede zaten var olan paketleri nasıl işleyeceğini belirtir:

- *İstem* , NuGet 'e mevcut paketlerin tutulup tutulmayacağını veya üzerine yazılıp yazılmayacağını sorar.
- *Tümünü Yoksay* , NuGet 'in varolan paketlerin üzerine yazılmasını atlayıp değiştirmesini sağlar.
- *Tüm* mevcut paketlerin üzerine yazmak Için tüm NuGet 'e yazın.

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a>Kaldırma seçenekleri

(Tüm proje türleri için kullanılamaz.)

**Bağımlılıkları kaldır**: seçildiğinde, tüm bağımlı paketleri projenin başka bir yerinde başvurulmuyorsa kaldırır.

**Üzerinde bağımlılıklar olsa bile kaldırma Işlemini zorla**: seçildiğinde, hala projede başvuruluyorsa bile bir paketi kaldırır. Bu genellikle bir paketi kaldırmak için **bağımlılıkları kaldır** ile birlikte kullanılır ve bu, yüklü bağımlılıkları ve herhangi bir bağımlılığı kaldırır. Ancak bu seçeneğin kullanılması, projedeki bozuk başvurulara yol açabilir. Bu gibi durumlarda, [diğer paketleri yeniden yüklemeniz](../consume-packages/reinstalling-and-updating-packages.md)gerekebilir.
