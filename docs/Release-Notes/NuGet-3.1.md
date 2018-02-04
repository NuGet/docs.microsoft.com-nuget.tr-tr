---
title: "NuGet 3.1 sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet bilinen sorunları, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere 3.1 için sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 3.1 sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a7aa43b8701b3bbef8f6ebce9a5d636ee1bc6abe
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-31-release-notes"></a><span data-ttu-id="9ce92-104">NuGet 3.1 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="9ce92-104">NuGet 3.1 Release Notes</span></span>

<span data-ttu-id="9ce92-105">[NuGet 3.0 sürüm notları](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 sürüm notları](../release-notes/nuget-3.1.1.md)</span><span class="sxs-lookup"><span data-stu-id="9ce92-105">[NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 Release Notes](../release-notes/nuget-3.1.1.md)</span></span>

<span data-ttu-id="9ce92-106">NuGet 3.1 27 Temmuz 2015 tarihinde Visual Studio 2015 için evrensel Windows Platform SDK'sının ile birlikte gelen bir uzantısı olarak yayımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="9ce92-106">NuGet 3.1 was released on July 27, 2015 as a bundled extension to the Universal Windows Platform SDK for Visual Studio 2015.</span></span> <span data-ttu-id="9ce92-107">Windows geliştirme deneyimi daha önce başlatılmış NuGet platformlar arası iş avantajlarından ele geçirebilir böylece Biz bu sürüm Windows Platform SDK'sı teslim.</span><span class="sxs-lookup"><span data-stu-id="9ce92-107">We delivered this release with the Windows Platform SDK so that the Windows development experience could take advantage of the NuGet cross-platform work that had been previously started.</span></span> <span data-ttu-id="9ce92-108">Bu NuGet uzantısı sürüm yalnızca Visual Studio 2015 için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="9ce92-108">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="9ce92-109">Visual Studio Galerisi güncelleştirme biz her zaman hata düzeltmeleri ve yeni özelliklerle güncelleştirmeleri yayımlama olarak kullanılabilir olan, en son sürüme erişimi bu geliştiriciler öneririz.</span><span class="sxs-lookup"><span data-stu-id="9ce92-109">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are always publishing updates with bug fixes and new features.</span></span>

## <a name="nuget-visual-studio-extension"></a><span data-ttu-id="9ce92-110">NuGet Visual Studio Extension</span><span class="sxs-lookup"><span data-stu-id="9ce92-110">NuGet Visual Studio Extension</span></span>

<span data-ttu-id="9ce92-111">Sorunlar ve bu sürümdeki özellikleri etiketli ile github'da ["3.1 RTM UWP geçişli desteği" Kilometre Taşı](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+) toplam, biz 3.1 sürümdeki 67 sorunlara kapalı.</span><span class="sxs-lookup"><span data-stu-id="9ce92-111">Issues and features in this release are tagged on GitHub with the ["3.1 RTM UWP transitive support" milestone](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  In total, we closed 67 issues in the 3.1 release.</span></span>

### <a name="new-features"></a><span data-ttu-id="9ce92-112">Yeni Özellikler</span><span class="sxs-lookup"><span data-stu-id="9ce92-112">New Features</span></span>

* <span data-ttu-id="9ce92-113">`project.json`Windows UWP ve ASP.NET 5 desteği için destek</span><span class="sxs-lookup"><span data-stu-id="9ce92-113">`project.json` support for Windows UWP and ASP.NET 5 support</span></span>
* <span data-ttu-id="9ce92-114">Geçişli paket yükleme</span><span class="sxs-lookup"><span data-stu-id="9ce92-114">Transitive package installation</span></span>

<span data-ttu-id="9ce92-115">Başka bir yerde açıklama ve bu özelliklerin tanımı belgelerinde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="9ce92-115">Description and definition of these features can be found elsewhere in the documentation.</span></span>

### <a name="deprecated"></a><span data-ttu-id="9ce92-116">Kullanım dışı</span><span class="sxs-lookup"><span data-stu-id="9ce92-116">Deprecated</span></span>

<span data-ttu-id="9ce92-117">Aşağıdaki özellikler artık Visual Studio 2015 için kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="9ce92-117">The following features are no longer available for Visual Studio 2015:</span></span>

* <span data-ttu-id="9ce92-118">Çözüm düzeyi paketlerini artık yüklenebilir</span><span class="sxs-lookup"><span data-stu-id="9ce92-118">Solution level packages can no longer be installed</span></span>

<span data-ttu-id="9ce92-119">Aşağıdaki özellikleri artık Visual Studio 2015 ve kullanmak projeleri için kullanılabilir `project.json` belirtimi</span><span class="sxs-lookup"><span data-stu-id="9ce92-119">The following features are no longer available for Visual Studio 2015 and projects that use the `project.json` specification</span></span>

* <span data-ttu-id="9ce92-120">`install.ps1`ve `uninstall.ps1` -bu komut dosyalarını paket yükleme sırasında yok sayılacak, geri yükleme, güncelleştirme ve kaldırma</span><span class="sxs-lookup"><span data-stu-id="9ce92-120">`install.ps1` and `uninstall.ps1` - These scripts will be ignored during package install, restore, update, and uninstall</span></span>
* <span data-ttu-id="9ce92-121">Yapılandırma dönüşümler göz ardı edilir</span><span class="sxs-lookup"><span data-stu-id="9ce92-121">Configuration transforms will be ignored</span></span>
* <span data-ttu-id="9ce92-122">İçeriği taşınan ancak bir projeye kopyalanmaz.</span><span class="sxs-lookup"><span data-stu-id="9ce92-122">Content will be carried, but not copied into a project.</span></span>
    * <span data-ttu-id="9ce92-123">Bu özellik yeniden uygulamak, tartışmayı izlemek ve adresindeki ilerleme takım çalışma: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span><span class="sxs-lookup"><span data-stu-id="9ce92-123">The team is working to re-implement this feature, follow the discussion and progress at: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span></span>


### <a name="known-issues"></a><span data-ttu-id="9ce92-124">Bilinen Sorunlar</span><span class="sxs-lookup"><span data-stu-id="9ce92-124">Known Issues</span></span>

<span data-ttu-id="9ce92-125">Bu sürüm ile birlikte sunulan bilinen sorunlar vardı.</span><span class="sxs-lookup"><span data-stu-id="9ce92-125">There were a number of known issues delivered with this release.</span></span>

* <span data-ttu-id="9ce92-126">Windows 10 SDK'sı 3.1 sürümünün yüklemesini herhangi bir sürümünü önceden yüklenmiş olan NuGet uzantısı düşürmek</span><span class="sxs-lookup"><span data-stu-id="9ce92-126">Installation of the 3.1 release with the Windows 10 SDK will downgrade any version of NuGet extension that was previously installed</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="9ce92-127">NuGet komut satırı</span><span class="sxs-lookup"><span data-stu-id="9ce92-127">NuGet Command-line</span></span>

<span data-ttu-id="9ce92-128">NuGet komut satırı yürütülebilir dosyasını güncelleştirildi ve geçmiş sürümleri nuget.exe kullanılabilir duruma getirilmek üzere devam edebilmesi için bu yeni dağıtılabilir bir konuma taşındı.</span><span class="sxs-lookup"><span data-stu-id="9ce92-128">The NuGet command-line executable was updated and moved to a new distributable location so that historical versions of nuget.exe can continue to be made available.</span></span>  <span data-ttu-id="9ce92-129">Windows için nuget.exe 3.1 beta sürümü yükleyebilirsiniz: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="9ce92-129">You can download the 3.1 beta version of nuget.exe for Windows at: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span></span>

<span data-ttu-id="9ce92-130">Bu şablon izleyen bir klasör yapısı ile dist.nuget.org ana bilgisayarda yeni dağıtılabilir konumu bulunur:</span><span class="sxs-lookup"><span data-stu-id="9ce92-130">The new distributable location resides on the dist.nuget.org host, with a folder structure that follows this template:</span></span>

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a><span data-ttu-id="9ce92-131">Yeni Özellikler</span><span class="sxs-lookup"><span data-stu-id="9ce92-131">New Features</span></span>

* <span data-ttu-id="9ce92-132">nuget.exe geri yüklemek ve kullanmak projelere paketlerini yüklemek bir `project.json` dosyası.</span><span class="sxs-lookup"><span data-stu-id="9ce92-132">nuget.exe can restore and install packages into projects that use a `project.json` file.</span></span>
* <span data-ttu-id="9ce92-133">nuget.exe bağlanmak ve konumundaki NuGet v3 Protokolü kullanma: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span><span class="sxs-lookup"><span data-stu-id="9ce92-133">nuget.exe can connect to and consume the NuGet v3 protocol at: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span></span>

## <a name="known-issues"></a><span data-ttu-id="9ce92-134">Bilinen Sorunlar</span><span class="sxs-lookup"><span data-stu-id="9ce92-134">Known Issues</span></span> ##

1.    <span data-ttu-id="9ce92-135">Paketi karşı yürütülemiyor bir `project.json` dosyası - [928](https://github.com/NuGet/Home/issues/928)</span><span class="sxs-lookup"><span data-stu-id="9ce92-135">Cannot execute pack against a `project.json` file - [928](https://github.com/NuGet/Home/issues/928)</span></span>
2.    <span data-ttu-id="9ce92-136">Mono üzerinde - desteklenmeyen [1059](https://github.com/NuGet/Home/issues/1059)</span><span class="sxs-lookup"><span data-stu-id="9ce92-136">Is not supported on Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span></span>
3.    <span data-ttu-id="9ce92-137">Yerelleştirilmiş değil - [1058](https://github.com/NuGet/Home/issues/1058), [1057](https://github.com/NuGet/Home/issues/1057)</span><span class="sxs-lookup"><span data-stu-id="9ce92-137">Is not localized - [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span></span>
4.    <span data-ttu-id="9ce92-138">, Yalnızca mevcut http://nuget.org/nuget.exe gibi - imzalanmamış [1073](https://github.com/NuGet/Home/issues/1073)</span><span class="sxs-lookup"><span data-stu-id="9ce92-138">Is not signed, just like the existing http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span></span>
