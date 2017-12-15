---
title: "NuGet 2.2 sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 25389d8c-e7db-4920-ab5e-cff20cebee7e
description: "NuGet bilinen sorunları, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere 2.2 için sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 2.2 sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 690e76a0686a5e7bb699410edef4a6e62ccd2a32
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-22-release-notes"></a><span data-ttu-id="43efb-104">NuGet 2.2 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="43efb-104">NuGet 2.2 Release Notes</span></span>

<span data-ttu-id="43efb-105">[NuGet 2.1 sürüm notları](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 sürüm notları](../release-notes/nuget-2.2.1.md)</span><span class="sxs-lookup"><span data-stu-id="43efb-105">[NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md)</span></span>

<span data-ttu-id="43efb-106">NuGet 2.2 12 Aralık 2012'de serbest bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="43efb-106">NuGet 2.2 was released on December 12, 2012.</span></span>

## <a name="visual-studio-quick-launch"></a><span data-ttu-id="43efb-107">Visual Studio Hızlı Başlat</span><span class="sxs-lookup"><span data-stu-id="43efb-107">Visual Studio Quick Launch</span></span>
<span data-ttu-id="43efb-108">Visual Studio 2012'de eklenen yeni özellikler biri [Hızlı Başlatma iletişim](http://msdn.microsoft.com/library/hh417697.aspx).</span><span class="sxs-lookup"><span data-stu-id="43efb-108">One of the new features that was added in Visual Studio 2012 was the [quick launch dialog](http://msdn.microsoft.com/library/hh417697.aspx).</span></span> <span data-ttu-id="43efb-109">NuGet 2.2 Hızlı Başlatma girilen arama terimlerini Paket Yöneticisi iletişim kutusu başlatılmaya izin vererek bu iletişim kutusunu genişletir.</span><span class="sxs-lookup"><span data-stu-id="43efb-109">NuGet 2.2 extends this dialog, allowing it to initialize the package manager dialog with the search terms entered in the quick launch.</span></span> <span data-ttu-id="43efb-110">Örneğin, 'jquery' hızlı başlatma şimdi girerek bir seçenek 'jquery' ile eşleşen NuGet paketlerini arama sonuçlarında içerir.</span><span class="sxs-lookup"><span data-stu-id="43efb-110">For example, entering 'jquery' in quick launch now includes an option in the results to search NuGet packages matching 'jquery'.</span></span>

![NuGet Visual Studio hızlı başlatma içinde](./media/quick-launch.png)

<span data-ttu-id="43efb-112">Bu seçeneğin belirlenmesi, standart NuGet Paket Yöneticisi arama deneyimi 'jquery' terim için başlatır.</span><span class="sxs-lookup"><span data-stu-id="43efb-112">Selecting this option will launch the standard NuGet package manager search experience for the term 'jquery'.</span></span>

![Önceden doldurulmuş haldedir NuGet Paket Yöneticisi iletişim kutusu](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a><span data-ttu-id="43efb-114">Paket içeriği için tüm klasörü belirtin</span><span class="sxs-lookup"><span data-stu-id="43efb-114">Specify Entire Folder for Package Contents</span></span>
<span data-ttu-id="43efb-115">NuGet 2.2 şimdi tüm bir klasörde belirtmenize olanak verir `<file>` öğesinin `.nuspec` tüm bu klasörün içeriğini içerecek şekilde dosya.</span><span class="sxs-lookup"><span data-stu-id="43efb-115">NuGet 2.2 now allows you to specify an entire folder in the `<file>` element of the `.nuspec` file to include all of the contents of that folder.</span></span> <span data-ttu-id="43efb-116">Örneğin, aşağıdaki tüm betikler paket bir projeye yüklendiğinde contents\scripts klasörüne eklenecek paket betikleri klasöründeki neden olur.</span><span class="sxs-lookup"><span data-stu-id="43efb-116">For example, the following will cause all scripts in the package's scripts folder to be added to the contents\scripts folder when the package is installed into a project.</span></span>

```xml
<file src="scripts\" target="content\scripts"/>
```

<span data-ttu-id="43efb-117">**24/6/16 güncelleştirin: "içerik" klasöründeki boş klasörler paket yüklerken yoksayılır.**</span><span class="sxs-lookup"><span data-stu-id="43efb-117">**Update 6/24/16: Empty folders in the "content" folder are ignored when installing the package.**</span></span>

## <a name="known-issues"></a><span data-ttu-id="43efb-118">Bilinen Sorunlar</span><span class="sxs-lookup"><span data-stu-id="43efb-118">Known Issues</span></span>

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a><span data-ttu-id="43efb-119">Paket Yöneticisi konsolu kullanılırken F # projeleri için paket yükleme başarısız oluyor</span><span class="sxs-lookup"><span data-stu-id="43efb-119">Package installation fails for F# projects when using the package manager console</span></span>
<span data-ttu-id="43efb-120">Bir NuGet paketi Paket Yöneticisi konsolu kullanılarak bir F # projeye yüklemeye çalışırken, bir InvalidOperationException atılır.</span><span class="sxs-lookup"><span data-stu-id="43efb-120">When attempting to install a NuGet package into an F# project using the package manager console, an InvalidOperationException is thrown.</span></span> <span data-ttu-id="43efb-121">Bu sorunu çözmek için F # ekibi ile etkin olarak çalışıyoruz ancak bu arada, F # projelerine Konsolu yerine NuGet Paket Yöneticisi iletişim kutusu üzerinden NuGet paketlerini yüklemek için geçici bir çözüm değildir.</span><span class="sxs-lookup"><span data-stu-id="43efb-121">We are actively working with the F# team to resolve the issue, but in the meantime, the workaround is to install NuGet packages into F# projects via NuGet's package manager dialog rather than the console.</span></span> <span data-ttu-id="43efb-122">[Daha fazla bilgi CodePlex üzerinde kullanılabilir](http://nuget.codeplex.com/workitem/2873).</span><span class="sxs-lookup"><span data-stu-id="43efb-122">[More information is available on CodePlex](http://nuget.codeplex.com/workitem/2873).</span></span>


## <a name="bug-fixes"></a><span data-ttu-id="43efb-123">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="43efb-123">Bug Fixes</span></span>
<span data-ttu-id="43efb-124">NuGet 2.2 birçok hata düzeltmeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="43efb-124">NuGet 2.2 includes many bug fixes.</span></span> <span data-ttu-id="43efb-125">İş tam listesi için öğeleri NuGet 2.2 Lütfen görünüm sabit [NuGet sorun İzleyicisi bu sürüm için](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="43efb-125">For a full list of work items fixed in NuGet 2.2, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
