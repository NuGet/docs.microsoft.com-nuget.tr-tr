---
title: NuGet Paket Yöneticisi kullanıcı Arabirimi başvurusu
description: NuGet paketleri ile çalışmak için Visual Studio'da NuGet Paket Yöneticisi UI kullanarak yönelik yönergeler.
author: karann-msft
ms.author: karann
ms.date: 12/08/2017
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 422faf99e58e058d86db774a8f3c1c576b3dc393
ms.sourcegitcommit: 2af17c8bb452a538977794bf559cdd78d58f2790
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/29/2019
ms.locfileid: "58637629"
---
# <a name="nuget-package-manager-ui"></a>NuGet Paket Yöneticisi UI

Windows üzerinde Visual Studio'da NuGet Paket Yöneticisi UI kolayca yükleme, kaldırma ve projelerde ve çözümlerde NuGet paketlerini güncelleştirme sağlar. Mac için Visual Studio deneyim için bkz: [dahil olmak üzere bir NuGet paketini projenize](/visualstudio/mac/nuget-walkthrough). Paket Yöneticisi UI, Visual Studio Code ile dahil değildir.

Bu konuda:

- [Bulma ve bir paket (Gözat sekmesi) yükleme](#finding-and-installing-a-package)
- [Bir paket (yüklü sekmesi) kaldırma](#uninstalling-a-package)
- [Bir paket (yüklü ve güncelleştirmeleri sekmeleri) güncelleştirme](#updating-a-package) (içerir ["Örtük olarak bir SDK'sı tarafından başvurulan" veya "AutoReferenced" iletisi](#implicit_reference))
- [Çözüm için paketleri yönetme](#managing-packages-for-the-solution) (aynı anda birden fazla projeyle çalışma).
- [Paket kaynakları](#package-sources)
- [Paket Yöneticisi seçeneklerini denetleme](#package-manager-options-control)

> [!Note]
> Visual Studio 2015'te NuGet Paket Yöneticisi kayıpsa denetleyin **Araçlar > Uzantılar ve güncelleştirmeler...**  araması *NuGet Paket Yöneticisi* uzantısı. Visual Studio Uzantıları yükleyici yapamıyorsanız doğrudan uzantısını [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).
>
> Visual Studio 2017'de NuGet ve NuGet Paket Yöneticisi otomatik olarak ile yüklenir. NET ilgili iş yükleri. Tek tek seçerek yüklemek **tek tek bileşenler > kod Araçlar > NuGet Paket Yöneticisi** Visual Studio 2017 yükleyicisindeki seçeneği.

## <a name="finding-and-installing-a-package"></a>Bulma ve bir paket yükleme

1. İçinde **Çözüm Gezgini**, ya da sağ **başvuruları** veya bir proje ve select **NuGet paketlerini Yönet...** .

    ![Menü seçeneği NuGet paketlerini Yönet](media/ManagePackagesUICommand.png)

1. **Gözat** sekmesi seçili kaynaktan popülerliği tarafından paketleri görüntüler (bkz [paket kaynakları](#package-sources)). Sol üst arama kutusunu kullanarak belirli bir paket için arama yapın. Ayrıca sağlar, bilgilerini görüntülemek için listeden bir paket seçin **yükleme** sürüm seçimi açılan listesi ile birlikte düğmesi.

    ![NuGet paketleri iletişim Gözat sekmesini yönetme](media/Search.png)

1. Açılan listeden istediğiniz sürümü seçin ve seçin **yükleme**. Visual Studio projesine paketi ve bağımlılıkları yükler. Lisans koşullarını kabul etmeniz istenebilir. Yükleme tamamlandığında, eklenen paketler görünür **yüklü** sekmesi. Paketler ayrıca listelenir **başvuruları** kendisine ile projedeki başvurabilirsiniz olduğunu gösteren Çözüm Gezgini düğümünün `using` deyimleri.

    ![Çözüm Gezgini'nde başvuruların](media/References.png)

> [!Tip]
> Yayın öncesi sürümler Aramaya eklenecek ve yayın öncesi sürümler açılan sürüm kullanılabilir hale getirmek için seçin **ön sürümü dahil et** seçeneği.

## <a name="uninstalling-a-package"></a>Bir paket kaldırılıyor

1. İçinde **Çözüm Gezgini**, ya da sağ **başvuruları** veya istenen proje ' nı seçip **NuGet paketlerini Yönet...** .
1. Seçin **yüklü** sekmesi.
1. (Gerekirse listeyi filtrelemek için arama kullanarak) kaldırmak için paketini seçin ve Seç **kaldırma**.

    ![Bir paket kaldırılıyor](media/UninstallPackage.png)

1. Unutmayın **INCLUDE yayın öncesi** ve **paket kaynağı** denetimleri, paketleri kaldırılırken etkiye sahiptir.

## <a name="updating-a-package"></a>Bir paketi güncelleştiriliyor

1. İçinde **Çözüm Gezgini**, ya da sağ **başvuruları** veya istenen proje ' nı seçip **NuGet paketlerini Yönet...** . (Web sitesi projelerinde sağ **Bin** klasör.)
1. Seçin **güncelleştirmeleri** seçili paket kaynaklarından kullanılabilir güncelleştirmeleri olan paketleri görmek için sekmesinde. Seçin **ön sürümü dahil et** yayın öncesi paketleri güncelleştirme listeye dahil edilecek.
1. Güncelleştirme, sağdaki açılır listeden istediğiniz sürümü seçin ve seçin için paketi seçin **güncelleştirme**.

    ![Bir paketi güncelleştiriliyor](media/UpdatePackages.png)

1. <a name="implicit_reference"></a>Bazı paketler için **güncelleştirme** düğmesi devre dışıdır ve bunu "örtük olarak bir SDK'sı tarafından başvuruda bulunulan" bildiren bir ileti görüntülenir (veya "AutoReferenced"). Bu ileti, paket büyük bir çerçeve veya SDK'sı parçasıdır ve bağımsız olarak güncelleştirilmemelidir gösterir. (Bu paketleri dahili olarak ile işaretlenen `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) Örneğin, `Microsoft.NETCore.App` .NET Core SDK'sının bir parçasıdır ve Paket sürümü uygulama tarafından kullanılan çalışma zamanı framework sürümü ile aynı değildir. Şunları yapmanız [.NET Core yüklemenizi güncelleştirin](https://aka.ms/dotnet-download) ASP.NET Core ve .NET Core çalışma zamanı yeni sürümlerini almak için. [.NET Core meta paketler ve sürüm oluşturma hakkında daha fazla ayrıntı için bu belgeye bakın](/dotnet/core/packages). Bu, aşağıdaki yaygın olarak kullanılan paketler için geçerlidir:
    * Microsoft.AspNetCore.All
    * Microsoft.AspNetCore.App
    * Microsoft.NETCore.App
    * NETStandard.Library

    ![Örnek paket başvuruları veya AutoReferenced dolaylı olarak işaretlendi](media/PackageManagerUIAutoReferenced.png)

1. Birden çok paket en yeni sürümlerine güncelleştirmek için bunları seçin ve liste içinde seçin **güncelleştirme** düğmesi listesinin üstünde.
1. Tek bir paketten de güncelleştirebilirsiniz **yüklü** sekmesi. Bu durumda, bir sürüm Seçici Paket ayrıntılarını içerir (konusu **INCLUDE yayın öncesi** seçeneği) ve bir **güncelleştirme** düğmesi.

## <a name="managing-packages-for-the-solution"></a>Çözüm için paketleri yönetme

Bir çözüm için paketleri yönetme, aynı anda birden çok projeleriyle çalışmak için kullanışlı bir yoludur.

1. Seçin **Araçlar > NuGet Paket Yöneticisi > çözüm için NuGet paketlerini Yönet...**  menü komutunu veya çözüme sağ tıklayıp seçin **NuGet paketlerini Yönet...** :

    ![Çözüm için NuGet paketlerini Yönet](media/ManagePackagesSolutionUICommand.png)

1. Çözüm için paketler yönetirken işlemleri tarafından etkilenen projeleri seçin kullanıcı Arabirimi sağlar:

    ![Çözüm için paketler yönetirken proje Seçici](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a>Sekme birleştirin

Geliştiriciler genellikle aynı çözüm içindeki farklı projelerde aynı NuGet paketi farklı sürümlerini kullanmak için hatalı bir uygulama düşünün. Bir çözüm için paketler yönetmek seçtiğinizde, Paket Yöneticisi kullanıcı Arabirimi sağlayan bir **Birleştir** üzerinde kolayca farklı sürüm numaralarını paketlerle çözüm içindeki farklı projelerde tarafından kullanıldığı sekmesinde görebilirsiniz:

![Paket Yöneticisi UI birleştirme sekmesi](media/ConsolidateTab.png)

EntityFramework 6.1.0 ConsoleApp1 kullanıyor ancak bu örnekte, EntityFramework 6.2.0, ClassLibrary1 proje kullanıyor. Paket sürümleri birleştirmek için aşağıdakileri yapın:

- Proje listesinde güncelleştirmek için projeleri seçin.
- Bu projeleri içinde kullanılacak sürümünü seçin **sürüm** EntityFramework 6.2.0 gibi bir denetim.
- Seçin **yükleme** düğmesi.

Paket Yöneticisi, seçilen tüm projeler, sonra paket artık görünür içine seçili Paket sürümü yükler. **Birleştir** sekmesi.

## <a name="package-sources"></a>Paket kaynakları

Visual Studio paketleri alacağı kaynağını değiştirmek için bir kaynak Seçici'yi seçin:

![Paket kaynağı seçicide Paket Yöneticisi UI](media/PackageSourceDropDown.png)

Paket kaynaklarını yönetmek için:

1. Seçin **ayarları** Paket Yöneticisi UI simgesine aşağıda özetlenen veya kullanın **Araçlar > Seçenekler** komut ve kaydırma **NuGet Paket Yöneticisi**:

    ![Paket Yöneticisi UI ayarlar simgesi](media/PackageSourceSettings.png)

1. Seçin **paket kaynaklarını** düğüm:

    ![Paket kaynağı seçenekleri](media/options.png)

1. Bir kaynak eklemek için seçin **+**, adı düzenleyin, URL veya yol girin **kaynak** denetlemek ve seçin **güncelleştirme**. Kaynak Seçici açılan görünür.
1. Paket kaynağı değiştirmek için seçin, içinde düzenlemeler **adı** ve **kaynak** kutuları ve select **güncelleştirme**.
1. Paket kaynağı devre dışı bırakmak için listesinde adının sol tarafındaki kutuya temizleyin.
1. Paket kaynağı kaldırmak için onu seçin ve ardından **X** düğmesi.
1. Kullanarak yukarı ve aşağı ok düğmelerini paket kaynaklarını öncelik sırasını değiştirmez. Visual Studio isteklerine yanıt vermek için hangi kaynak gelen paketin ilk kullanarak paket kaynaklarını sırasını yoksayar. Daha fazla bilgi için [paket geri yükleme](../consume-packages/package-restore.md).

> [!Tip]
> Paket kaynağı sildikten sonra görünürse, bir bilgisayar düzeyinde veya kullanıcı düzeyi listelenebilir `NuGet.Config` dosyaları. Bkz: [yapılandırma NuGet davranışını](../consume-packages/configuring-nuget-behavior.md) bu dosyaları konumu için ardından dosyaları el ile düzenleme ya da kullanarak kaynak kaldırın [nuget komutu kaynakları](../tools/nuget-exe-CLI-reference.md).

## <a name="package-manager-options-control"></a>Paket Yöneticisi seçeneklerini denetleme

Bir paket seçildiğinde, küçük bir paket Yöneticisi UI görüntüler Genişletilebilir **seçenekleri** altına (her ikisi de daraltılmış ve genişletilmiş burada gösterilmiştir) sürüm seçici denetimi. Bazı proje için türleri, yalnızca unutmayın **Show Önizleme penceresini** seçeneği sağlanır.

![Paket Yöneticisi seçenekleri](media/PackageManagerUIOptions.png)

Aşağıdaki bölümlerde, bu seçenekler açıklanmaktadır.

### <a name="show-preview-window"></a>Önizleme penceresini göster

Paketi yüklenmeden önce kalıcı bir pencere seçildiğinde, seçilen Paket bağımlılıklarını görüntüler:

![Örnek Önizleme iletişim kutusu](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a>Yükleme ve güncelleştirme seçenekleri

(Kullanılamaz tüm proje türleri için.)

**Bağımlılık davranışı** NuGet bağımlı paketler yüklemek için hangi sürümlerinin nasıl karar yapılandırır:

- *Bağımlılıkları yoksay* herhangi bir bağımlılığın, genellikle yüklenen paket keser yükleme atlar.
- *En düşük* [Varsayılan] birincil Seçilen paketin gereksinimlerini karşılayan en az sürüm numarasına sahip bağımlılık yükler.
- *En yüksek düzeltme eki* aynı birincil ve ikincil sürüm numaralarını, ancak yüksek düzeltme numarası ile yeni sürümü yükler. Sürüm 1.2.2 belirtilirse Örneğin, ardından 1.2 ile başlayan en yüksek sürümü yüklenir
- *En yüksek ikincil* aynı büyük sürüm numarasına ancak en yüksek ikincil numara ve düzeltme numarası ile yeni sürümü yükler. Sürüm 1.2.2 belirtilirse, 1 ile başlayan en yüksek sürümü yüklenir
- *En yüksek* paket yüksek kullanılabilir sürümünü yükler.

**Dosya çakışması eylem** NuGet proje veya yerel makinedeki mevcut paketleri nasıl işleyeceğini belirtir:

- *Komut İstemi* tutmak veya var olan paketleri üzerine istemek için NuGet bildirir.
- *Tümünü Yoksay* mevcut paketleri üzerine atlamak için NuGet bildirir.
- *Tüm üzerine* mevcut paketleri üzerine yazmak için NuGet bildirir.

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a>Kaldırma seçenekleri

(Kullanılamaz tüm proje türleri için.)

**Bağımlılıkları kaldırın**: Seçili olduğunda, bunlar başka bir projede başvurulmuş değil, tüm bağımlı paketler kaldırır.

**Zorla kaldırın olsa bile bağımlılıklar üzerinde**: Seçili olduğunda, bir paket kaldırır bile projede başvuruluyor. Bu genellikle birlikte kullanılır **bağımlılıkları kaldırın** bir paket ve her şeyi kaldırmak için bağımlılıklar yüklü. Bu seçenek kullanılarak ancak projedeki bozuk başvurularda açabilir. Böyle durumlarda, gerekebilir [diğer paketleri yeniden](../consume-packages/reinstalling-and-updating-packages.md).
