---
title: Visual Studio'da NuGet paketlerini yükleyin ve yönetin
description: NuGet paketleri ile çalışmak için Visual Studio'da NuGet Paket Yöneticisi UI'yi kullanma talimatları.
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
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428697"
---
# <a name="install-and-manage-packages-in-visual-studio-using-the-nuget-package-manager"></a>NuGet Paket Yöneticisi'ni kullanarak Visual Studio'da paketleri yükleyin ve yönetin

Windows'daki Visual Studio'daki NuGet Paket Yöneticisi Kullanıcı UI, projelerde ve çözümlerde NuGet paketlerini kolayca yüklemenize, kaldırmanıza ve güncellemenize olanak tanır. Mac için Visual Studio'daki deneyim için, [projenize bir NuGet paketi dahil etme](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)hakkında bakınız. Paket Yöneticisi UI Visual Studio Code ile birlikte değildir.

> [!NOTE]
> Visual Studio 2015'te NuGet Paket Yöneticisi'ni kaçırıyorsanız, **Araçlar > Uzantıları ve Güncellemeler...'ı** kontrol edin ve *NuGet Paket Yöneticisi* uzantısını arayın. Visual Studio'daki uzantıları yükleyicisi kullanamıyorsanız, uzantıyı [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)doğrudan 'den indirin.
>
> Visual Studio 2017'den itibaren NuGet ve NuGet Paket Yöneticisi otomatik olarak herhangi bir . NET ile ilgili iş yükleri. Visual Studio yükleyicisinde **NuGet paket yöneticisi** seçeneği > Tek tek bileşenleri > Kod araçlarını seçerek tek tek yükleyin.

## <a name="find-and-install-a-package"></a>Bir paket bulma ve yükleme

1. **Çözüm Gezgini'nde,** **Referanslar** veya proje için sağ tıklayın ve **NuGet Paketlerini Yönet'i seçin...**

    ![NuGet Paketleri menüsü seçeneğini yönetin](media/ManagePackagesUICommand.png)

1. **Gözat** sekmesi paketleri şu anda seçili kaynaktan popülerlik olarak görüntüler [(paket kaynaklarına](#package-sources)bakın). Sol üstteki arama kutusunu kullanarak belirli bir paketi arayın. Bilgilerini görüntülemek için listeden bir paket seçin ve **Install** bu da sürüm seçimi açılır bırakma düğmesini etkinleştirir.

    ![NuGet Paketleri İletişim Sekmesini Yönet](media/Search.png)

1. Açılan açılır dan istenilen sürümü seçin ve **Yükle'yi**seçin. Visual Studio paketi ve bağımlılıklarını projeye yükler. Lisans koşullarını kabul etmeniz istenebilir. Yükleme tamamlandığında, eklenen paketler **Yüklenen** sekmesinde görünür. Paketler, Çözüm Gezgini'nin **Başvuru düğümünde** de listelenir ve bu `using` da projede deyimlerle bunlara başvurabileceğinizi gösterir.

    ![Çözüm Gezgini'ndeki Referanslar](media/References.png)

> [!Tip]
> Aramada ön sürüm sürümlerini eklemek ve sürüm açılır sürümünde ön sürüm sürümlerini kullanılabilir hale getirmek **için, ön sürüm ekle** seçeneğini belirleyin.

> [!Note]
> NuGet,bir projenin paketleri kullanabileceği iki biçimi [`PackageReference`](package-references-in-project-files.md) [`packages.config`](../reference/packages-config.md)vardır: ve . [Varsayılan değer Visual Studio'nun seçenekler penceresinde ayarlanabilir.](Package-Restore.md#choose-default-package-management-format)

## <a name="uninstall-a-package"></a>Paketi kaldırma

1. **Çözüm Gezgini'nde,** **Referanslar'a** veya istenilen projeye sağ tıklayın ve **NuGet Paketlerini Yönet'i seçin... seçeneğini belirleyin.**
1. **Yüklü öğeler** sekmesini seçin.
1. Kaldırmak için paketi seçin (gerekirse listeye filtre lemek için aramayı kullanarak) ve **Kaldır'ı**seçin.

    ![Paketi kaldırma](media/UninstallPackage.png)

1. **Paketleri** yüklerken Ön Sürüm Ekle ve **Paket kaynak** denetimleri üzerinde hiçbir etkisi olmadığını unutmayın.

## <a name="update-a-package"></a>Paketi güncelleştir

1. **Çözüm Gezgini'nde,** **Referanslar'a** veya istenilen projeye sağ tıklayın ve **NuGet Paketlerini Yönet'i seçin... seçeneğini belirleyin.** (Web sitesi projelerinde, **Bin** klasörüne sağ tıklayın.)
1. Seçili paket kaynaklarından kullanılabilir güncelleştirmeleri olan paketleri görmek için **Güncelleştirmeler** sekmesini seçin. Güncelleştirme listesine yayın öncesi paketleri eklemek için yayın öncesi paketleri **ekle'yi** seçin.
1. Güncellemek için paketi seçin, sağdaki açılır yerden istenen sürümü seçin ve **Güncelleştir'i**seçin.

    ![Paketi güncelleştirme](media/UpdatePackages.png)

1. <a name="implicit_reference"></a>Bazı paketler için **Güncelleştirme** düğmesi devre dışı bırakılır ve "Örtülü olarak bir SDK tarafından başvurulan" (veya "AutoReferenced") olduğunu belirten bir ileti görüntülenir. Bu ileti, paketin daha büyük bir çerçevenin veya SDK'nın bir parçası olduğunu ve bağımsız olarak güncelleştirilmemesi gerektiğini gösterir. (Bu tür paketler dahili olarak `<IsImplicitlyDefined>True</IsImplicitlyDefined>`işaretlenir.) Örneğin, `Microsoft.NETCore.App` .NET Core SDK'nın bir parçasıdır ve paket sürümü, uygulama tarafından kullanılan çalışma zamanı çerçevesinin sürümüyle aynı değildir. ASP.NET Core ve .NET Core çalışma zamanının yeni sürümlerini almak için [.NET Core yüklemenizi güncelleştirmeniz](https://aka.ms/dotnet-download) gerekir. [.NET Core metapackages ve sürüm hakkında daha fazla bilgi için bu belgeye bakın.](/dotnet/core/packages) Bu, sık kullanılan aşağıdaki paketler için geçerlidir:
    * Microsoft.AspNetCore.All
    * Microsoft.AspNetCore.App
    * Microsoft.NETCore.App
    * NETStandard.Library

    ![Dolaylı referanslar veya AutoReferenced olarak işaretlenmiş örnek paket](media/PackageManagerUIAutoReferenced.png)

1. Birden çok paketi en yeni sürümlerinde güncelleştirmek için, bunları listede seçin ve listenin üstündeki **Güncelleştir** düğmesini seçin.
1. Yüklü sekmesinden tek bir paketi de **güncelleştirebilirsiniz.** Bu durumda, paketin ayrıntıları bir sürüm seçici **(Ön sürüm ekle** seçeneğine tabidir) ve Güncelleştirme düğmesini içerir. **Update**

## <a name="manage-packages-for-the-solution"></a>Çözüm için paketleri yönetme

Bir çözüm için paketleri yönetmek, aynı anda birden fazla projeyle çalışmak için kullanışlı bir araçtır.

1. **NuGet Paket Yöneticisi > Paketleri Çözüm için Yönet' > Araçlar'ı seçin...** menü komutu veya çözüme sağ tıklayın ve **NuGet Paketlerini Yönet'i seçin...**

    ![Çözüm için NuGet paketlerini yönetin](media/ManagePackagesSolutionUICommand.png)

1. Çözüm için paketleri yönetirken, UI operasyonlardan etkilenen projeleri seçmenize olanak tanır:

    ![Çözüm için paketleri yönetirken proje seçici](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a>Sekmeyi birleştir

Geliştiriciler genellikle aynı çözümde farklı projeler arasında aynı NuGet paketinin farklı sürümlerini kullanmanın kötü bir uygulama olduğunu düşünür. Bir çözüm için paketleri yönetmeyi seçtiğinizde, Paket Yöneticisi Kullanıcı Arabirimi, farklı sürüm numaralarına sahip paketlerin çözümde farklı projeler tarafından nerede kullanıldığını kolayca görebileceğiniz bir **Birleştirme** sekmesi sağlar:

![Paket Yöneticisi UI Birleştirme sekmesi](media/ConsolidateTab.png)

Bu örnekte, ClassLibrary1 projesi EntityFramework 6.2.0 kullanırken, ConsoleApp1 EntityFramework 6.1.0'ı kullanıyor. Paket sürümlerini birleştirmek için aşağıdakileri yapın:

- Proje listesinde güncelleştirilecek projeleri seçin.
- EntityFramework 6.2.0 gibi **Sürüm** denetimindeki tüm bu projelerde kullanılacak sürümü seçin.
- **Yükle** düğmesini seçin.

Paket Yöneticisi, seçili paket sürümünü seçili tüm projelere yükler ve ardından paket **Birleştirme** sekmesinde görünmez.

## <a name="package-sources"></a>Paket kaynakları

Visual Studio'nun paketleri aldığı kaynağı değiştirmek için kaynak seçiciden birini seçin:

![Paket yöneticisi UI'deki paket kaynak seçici](media/PackageSourceDropDown.png)

Paket kaynaklarını yönetmek için:

1. Aşağıda özetlenen Paket Yöneticisi UI'deki **Ayarlar** simgesini seçin veya **Araçlar > Seçenekleri** komutunu kullanın ve **NuGet Paket Yöneticisi'ne**gidin:

    ![Paket yöneticisi UI ayarları simgesi](media/PackageSourceSettings.png)

1. Paket **Kaynakları** düğümünü seçin:

    ![Paket Kaynakları seçenekleri](media/options.png)

1. Kaynak eklemek için, **+** adı seçin, adı seçin, **Kaynak** denetimine URL'yi veya yolu girin ve **Güncelleştir'i**seçin. Kaynak şimdi seçici açılır açılır görünür.
1. Paket kaynağını değiştirmek için, onu seçin, **Ad** ve **Kaynak** kutularında değişiklikler yapın ve **Güncelleştir'i**seçin.
1. Paket kaynağını devre dışı kalmak için listedeki adın solundaki kutuyu temizleyin.
1. Bir paket kaynağını kaldırmak için, onu seçin ve ardından **X** düğmesini seçin.
1. Yukarı ve aşağı ok düğmelerini kullanmak paket kaynaklarının öncelik sırasını değiştirmez. Visual Studio, isteklere yanıt vermek için ilk hangi kaynaktan gelen paketi kullanarak paket kaynaklarının sırasını yok sayar. Daha fazla bilgi için [Paket geri yükleme'ye](../consume-packages/package-restore.md)bakın.

> [!Tip]
> Bir paket kaynağı siledikten sonra yeniden görünürse, bilgisayar düzeyinde veya kullanıcı `NuGet.Config` düzeyindeki dosyalarda listelenebilir. Bu dosyaların konumu için [Ortak NuGet yapılandırmalarına](../consume-packages/configuring-nuget-behavior.md) bakın, ardından dosyaları el ile düzenleyerek veya [nuget kaynakları komutunu](../reference/nuget-exe-CLI-reference.md)kullanarak kaynağı kaldırın.

## <a name="package-manager-options-control"></a>Paket yöneticisi Seçenekleri kontrolü

Bir paket seçildiğinde, Paket Yöneticisi UI sürüm seçicinin altında küçük, genişletilebilir **seçenekler** denetimini görüntüler (burada hem daraltılmış hem de genişletilmiş olarak gösterilir). Bazı proje türleri için yalnızca **Önizleme penceresini göster** seçeneğinin sağlandığını unutmayın.

![Paket yöneticisi seçenekleri](media/PackageManagerUIOptions.png)

Aşağıdaki bölümlerde bu seçenekleri açıklayınız.

### <a name="show-preview-window"></a>Önizleme penceresini göster

Seçildiğinde, bir modal pencere, seçilen paketin paket yüklenmeden önceki bağımlılıklarını görüntüler:

![Örnek Önizleme İletişim](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a>Yükleme ve Güncelleştirme Seçenekleri

(Tüm proje türleri için kullanılamaz.)

**Bağımlılık davranışı,** NuGet'in bağımlı paketlerin hangi sürümlerini yükleyeceklerine nasıl karar vereceğine göre yapılandırır:

- *Bağımlılıkları yoksay,* genellikle yüklenen paketi bozan bağımlılıkları yüklemeyi atlar.
- *En Düşük* [Varsayılan] bağımlılığı, birincil seçilen paketin gereksinimlerini karşılayan en az sürüm numarasıyla yükler.
- *En Yüksek Yama,* sürümü aynı büyük ve küçük sürüm numaralarına, ancak en yüksek yama numarasına sahip olarak yükler. Örneğin, sürüm 1.2.2 belirtilirse, 1.2 ile başlayan en yüksek sürüm yüklenir
- *En Yüksek Minor* aynı ana sürüm numarasına, ancak en yüksek küçük sayı ve yama numarasına sahip sürümü yükler. Sürüm 1.2.2 belirtilirse, 1 ile başlayan en yüksek sürüm yüklenir
- *En yüksek* paket, paketin mevcut en yüksek sürümünü yükler.

**Dosya çakışması eylemi,** NuGet'in projede veya yerel makinede zaten var olan paketleri nasıl işlemesi gerektiğini belirtir:

- *İstem,* NuGet'e varolan paketleri tutup tutmamayı veya üzerine yazıp yazmamayı sormasını ister.
- Tüm tüm yetkileri *yoksayın* NuGet varolan paketlerin üzerine yazmayı atlamak için.
- *Tüm Bunların Üzerine Yazın* NuGet'in varolan paketlerin üzerine yazmasını emreder.

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a>Seçenekleri Kaldır

(Tüm proje türleri için kullanılamaz.)

**Bağımlılıkları kaldırın**: seçildiğinde, projenin başka bir yerinde başvurulmuyorsa bağımlı paketleri kaldırır.

**Bağımlılıklar olsa bile kaldırmayı zorlayın:** seçildiğinde, projede hala başvurulmakta olsa bile paketi kaldırın. Bu genellikle bir paketi kaldırmak için **kaldır bağımlılıkları** ve yüklü ne olursa olsun bağımlılıkları ile birlikte kullanılır. Ancak, bu seçeneğin kullanılması projede bozuk başvurulara neden olabilir. Bu gibi durumlarda, [bu diğer paketleri yeniden yüklemeniz](../consume-packages/reinstalling-and-updating-packages.md)gerekebilir.
