---
title: NuGet 2.2 sürüm notları
description: NuGet bilinen sorunları, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr 2.2 için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a968ced3c58b7187a8bd9a8b14baa92f61f0140f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545998"
---
# <a name="nuget-22-release-notes"></a><span data-ttu-id="53ccb-103">NuGet 2.2 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="53ccb-103">NuGet 2.2 Release Notes</span></span>

<span data-ttu-id="53ccb-104">[2.1 NuGet sürüm notları](../release-notes/nuget-2.1.md) | [2.2.1 NuGet sürüm notları](../release-notes/nuget-2.2.1.md)</span><span class="sxs-lookup"><span data-stu-id="53ccb-104">[NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md)</span></span>

<span data-ttu-id="53ccb-105">NuGet 2.2 12 Aralık 2012 tarihinde yayınlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="53ccb-105">NuGet 2.2 was released on December 12, 2012.</span></span>

## <a name="visual-studio-quick-launch"></a><span data-ttu-id="53ccb-106">Visual Studio hızlı başlatma</span><span class="sxs-lookup"><span data-stu-id="53ccb-106">Visual Studio Quick Launch</span></span>
<span data-ttu-id="53ccb-107">Visual Studio 2012'de eklenen yeni özellikler biriydi [Hızlı Başlatma iletişim](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span><span class="sxs-lookup"><span data-stu-id="53ccb-107">One of the new features that was added in Visual Studio 2012 was the [quick launch dialog](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span></span> <span data-ttu-id="53ccb-108">2.2 NuGet Paket Yöneticisi iletişim kutusu içinde hızlı başlatma girdiğiniz arama terimi ile başlatmak izin bu iletişim kutusunu genişletir.</span><span class="sxs-lookup"><span data-stu-id="53ccb-108">NuGet 2.2 extends this dialog, allowing it to initialize the package manager dialog with the search terms entered in the quick launch.</span></span> <span data-ttu-id="53ccb-109">Örneğin, 'jquery' içinde hızlı başlatma şimdi girerek bir seçeneği 'jquery' eşleşen NuGet paketleri aramak için sonuçları içerir.</span><span class="sxs-lookup"><span data-stu-id="53ccb-109">For example, entering 'jquery' in quick launch now includes an option in the results to search NuGet packages matching 'jquery'.</span></span>

![NuGet, Visual Studio hızlı başlatma](./media/quick-launch.png)

<span data-ttu-id="53ccb-111">Bu seçeneğin belirlenmesi, standart NuGet Paket Yöneticisi arama deneyimi bir dönem 'jquery' başlatılır.</span><span class="sxs-lookup"><span data-stu-id="53ccb-111">Selecting this option will launch the standard NuGet package manager search experience for the term 'jquery'.</span></span>

![Önceden doldurulmuş NuGet Paket Yöneticisi iletişim kutusu](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a><span data-ttu-id="53ccb-113">Paket içeriği için tüm klasörü belirtin</span><span class="sxs-lookup"><span data-stu-id="53ccb-113">Specify Entire Folder for Package Contents</span></span>
<span data-ttu-id="53ccb-114">NuGet 2.2 artık klasörün tamamını belirtmenize olanak verir `<file>` öğesinin `.nuspec` tüm bu klasörün içeriğine dahil edilecek dosyası.</span><span class="sxs-lookup"><span data-stu-id="53ccb-114">NuGet 2.2 now allows you to specify an entire folder in the `<file>` element of the `.nuspec` file to include all of the contents of that folder.</span></span> <span data-ttu-id="53ccb-115">Örneğin, aşağıdaki tüm betikler paketin betikleri klasöründe projeye paketi yüklendiğinde contents\scripts klasörüne eklenecek neden olur.</span><span class="sxs-lookup"><span data-stu-id="53ccb-115">For example, the following will cause all scripts in the package's scripts folder to be added to the contents\scripts folder when the package is installed into a project.</span></span>

```xml
<file src="scripts\" target="content\scripts"/>
```

<span data-ttu-id="53ccb-116">**6/24/16 güncelleştirin: "içerik" klasöründeki boş klasörler paketi yüklerken yoksayılır.**</span><span class="sxs-lookup"><span data-stu-id="53ccb-116">**Update 6/24/16: Empty folders in the "content" folder are ignored when installing the package.**</span></span>

## <a name="known-issues"></a><span data-ttu-id="53ccb-117">Bilinen Sorunlar</span><span class="sxs-lookup"><span data-stu-id="53ccb-117">Known Issues</span></span>

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a><span data-ttu-id="53ccb-118">Paket Yöneticisi konsolu kullanılırken F # projeleri için paket yüklemesi başarısız oluyor</span><span class="sxs-lookup"><span data-stu-id="53ccb-118">Package installation fails for F# projects when using the package manager console</span></span>
<span data-ttu-id="53ccb-119">Paket Yöneticisi konsolu kullanarak bir F # projesi bir NuGet paketi yüklemeye çalışırken, bir InvalidOperationException oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="53ccb-119">When attempting to install a NuGet package into an F# project using the package manager console, an InvalidOperationException is thrown.</span></span> <span data-ttu-id="53ccb-120">Bu sorunu çözmek için F # ekip ile etkin olarak çalışıyoruz ancak bu arada, çözüm Konsolu yerine, NuGet Paket Yöneticisi iletişim kutusu aracılığıyla F # projeleri NuGet paketlerini yükleme olabilir.</span><span class="sxs-lookup"><span data-stu-id="53ccb-120">We are actively working with the F# team to resolve the issue, but in the meantime, the workaround is to install NuGet packages into F# projects via NuGet's package manager dialog rather than the console.</span></span> <span data-ttu-id="53ccb-121">[Daha fazla bilgi Codeplex'te kullanılabilir](http://nuget.codeplex.com/workitem/2873).</span><span class="sxs-lookup"><span data-stu-id="53ccb-121">[More information is available on CodePlex](http://nuget.codeplex.com/workitem/2873).</span></span>


## <a name="bug-fixes"></a><span data-ttu-id="53ccb-122">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="53ccb-122">Bug Fixes</span></span>
<span data-ttu-id="53ccb-123">NuGet 2.2 birçok hata düzeltmeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="53ccb-123">NuGet 2.2 includes many bug fixes.</span></span> <span data-ttu-id="53ccb-124">Tam bir listesi için iş öğeleri NuGet 2.2 içinde lütfen görünümü sabit [bu sürüm için NuGet sorun İzleyicisi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="53ccb-124">For a full list of work items fixed in NuGet 2.2, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
