---
title: NuGet 3.1 sürüm notları
description: NuGet bilinen sorunları, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr 3.1 sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 779567d94a5a9a1b3eacddaa4c882201a446cb4b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545353"
---
# <a name="nuget-31-release-notes"></a><span data-ttu-id="c1daa-103">NuGet 3.1 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="c1daa-103">NuGet 3.1 Release Notes</span></span>

<span data-ttu-id="c1daa-104">[NuGet 3.0 sürüm notları](../release-notes/nuget-3.0.0.md) | [3.1.1 NuGet sürüm notları](../release-notes/nuget-3.1.1.md)</span><span class="sxs-lookup"><span data-stu-id="c1daa-104">[NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 Release Notes](../release-notes/nuget-3.1.1.md)</span></span>

<span data-ttu-id="c1daa-105">NuGet 3.1 27 Temmuz 2015 tarihinde Visual Studio 2015 için evrensel Windows Platform SDK'sı ile birlikte gelen bir uzantısı olarak yayımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="c1daa-105">NuGet 3.1 was released on July 27, 2015 as a bundled extension to the Universal Windows Platform SDK for Visual Studio 2015.</span></span> <span data-ttu-id="c1daa-106">Daha önce başlatılmış NuGet platformlar arası iş yararlanmak Windows geliştirme deneyimi böylece Biz bu sürüm Windows Platform SDK'sı ile teslim.</span><span class="sxs-lookup"><span data-stu-id="c1daa-106">We delivered this release with the Windows Platform SDK so that the Windows development experience could take advantage of the NuGet cross-platform work that had been previously started.</span></span> <span data-ttu-id="c1daa-107">Bu NuGet uzantısı sürüm, yalnızca Visual Studio 2015 için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c1daa-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="c1daa-108">Biz her zaman güncelleştirmeleri hata düzeltmeleri ve yeni özelliklerle yayımlamayı gibi kullanılabilir en son sürümü için Visual Studio Galerisi Update'e erişecek bu geliştiriciler öneririz.</span><span class="sxs-lookup"><span data-stu-id="c1daa-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are always publishing updates with bug fixes and new features.</span></span>

## <a name="nuget-visual-studio-extension"></a><span data-ttu-id="c1daa-109">NuGet Visual Studio uzantısı</span><span class="sxs-lookup"><span data-stu-id="c1daa-109">NuGet Visual Studio Extension</span></span>

<span data-ttu-id="c1daa-110">Sorunları ve özellikler bu sürümde ile github'da etiketli ["3.1 RTM UWP geçişli desteği" aşama](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+) toplam biz 3.1 sürümündeki 67 sorunları kapatıldı.</span><span class="sxs-lookup"><span data-stu-id="c1daa-110">Issues and features in this release are tagged on GitHub with the ["3.1 RTM UWP transitive support" milestone](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  In total, we closed 67 issues in the 3.1 release.</span></span>

### <a name="new-features"></a><span data-ttu-id="c1daa-111">Yeni Özellikler</span><span class="sxs-lookup"><span data-stu-id="c1daa-111">New Features</span></span>

* <span data-ttu-id="c1daa-112">`project.json` Windows UWP ve ASP.NET 5 desteği için destek</span><span class="sxs-lookup"><span data-stu-id="c1daa-112">`project.json` support for Windows UWP and ASP.NET 5 support</span></span>
* <span data-ttu-id="c1daa-113">Geçişli paket yükleme</span><span class="sxs-lookup"><span data-stu-id="c1daa-113">Transitive package installation</span></span>

<span data-ttu-id="c1daa-114">Açıklama ve bu özelliklerin tanımı başka bir yerde belgelerinde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="c1daa-114">Description and definition of these features can be found elsewhere in the documentation.</span></span>

### <a name="deprecated"></a><span data-ttu-id="c1daa-115">kullanım dışı</span><span class="sxs-lookup"><span data-stu-id="c1daa-115">Deprecated</span></span>

<span data-ttu-id="c1daa-116">Aşağıdaki özellikler artık Visual Studio 2015 için kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="c1daa-116">The following features are no longer available for Visual Studio 2015:</span></span>

* <span data-ttu-id="c1daa-117">Çözüm düzeyinde paketleri artık yüklenebilir</span><span class="sxs-lookup"><span data-stu-id="c1daa-117">Solution level packages can no longer be installed</span></span>

<span data-ttu-id="c1daa-118">Aşağıdaki özellikler artık Visual Studio 2015 ve kullanan projeler için kullanılabilir `project.json` belirtimi</span><span class="sxs-lookup"><span data-stu-id="c1daa-118">The following features are no longer available for Visual Studio 2015 and projects that use the `project.json` specification</span></span>

* <span data-ttu-id="c1daa-119">`install.ps1` ve `uninstall.ps1` -bu komut dosyaları paket yükleme sırasında yok sayılacak, geri yükleme, güncelleştirme ve kaldırma</span><span class="sxs-lookup"><span data-stu-id="c1daa-119">`install.ps1` and `uninstall.ps1` - These scripts will be ignored during package install, restore, update, and uninstall</span></span>
* <span data-ttu-id="c1daa-120">Yapılandırma dönüşümleri yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="c1daa-120">Configuration transforms will be ignored</span></span>
* <span data-ttu-id="c1daa-121">İçerik yürütülüyor ancak projeye kopyalanmaz.</span><span class="sxs-lookup"><span data-stu-id="c1daa-121">Content will be carried, but not copied into a project.</span></span>
    * <span data-ttu-id="c1daa-122">Ekibi bu özelliği yeniden uygulamanız ve tartışmayı izlemek, ilerleme çalışıyor: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span><span class="sxs-lookup"><span data-stu-id="c1daa-122">The team is working to re-implement this feature, follow the discussion and progress at: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span></span>


### <a name="known-issues"></a><span data-ttu-id="c1daa-123">Bilinen Sorunlar</span><span class="sxs-lookup"><span data-stu-id="c1daa-123">Known Issues</span></span>

<span data-ttu-id="c1daa-124">Bu sürümle birlikte sunulan bilinen sorunlar vardı.</span><span class="sxs-lookup"><span data-stu-id="c1daa-124">There were a number of known issues delivered with this release.</span></span>

* <span data-ttu-id="c1daa-125">Yükleme 3.1 sürümüne ait Windows 10 SDK'sı NuGet uzantısı, daha önce yüklü olduğu herhangi bir sürümünü indirilecektir.</span><span class="sxs-lookup"><span data-stu-id="c1daa-125">Installation of the 3.1 release with the Windows 10 SDK will downgrade any version of NuGet extension that was previously installed</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="c1daa-126">NuGet komut satırı</span><span class="sxs-lookup"><span data-stu-id="c1daa-126">NuGet Command-line</span></span>

<span data-ttu-id="c1daa-127">NuGet komut satırı yürütülebilir dosyasını güncelleştirildi ve kullanılabilir olmasını nuget.exe adet geçmiş sürümü devam edebilmesi için yeni dağıtılabilir bir konuma taşındı.</span><span class="sxs-lookup"><span data-stu-id="c1daa-127">The NuGet command-line executable was updated and moved to a new distributable location so that historical versions of nuget.exe can continue to be made available.</span></span>  <span data-ttu-id="c1daa-128">Nuget.exe 3.1 beta sürümü Windows için yükleyebilirsiniz: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="c1daa-128">You can download the 3.1 beta version of nuget.exe for Windows at: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span></span>

<span data-ttu-id="c1daa-129">Bu şablon aşağıdaki klasör yapısı ile dist.nuget.org ana bilgisayarda dağıtılabilir konuma bulunur:</span><span class="sxs-lookup"><span data-stu-id="c1daa-129">The new distributable location resides on the dist.nuget.org host, with a folder structure that follows this template:</span></span>

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a><span data-ttu-id="c1daa-130">Yeni Özellikler</span><span class="sxs-lookup"><span data-stu-id="c1daa-130">New Features</span></span>

* <span data-ttu-id="c1daa-131">nuget.exe geri yükleyebilir ve kullanan projeler paketlerini yüklemek bir `project.json` dosya.</span><span class="sxs-lookup"><span data-stu-id="c1daa-131">nuget.exe can restore and install packages into projects that use a `project.json` file.</span></span>
* <span data-ttu-id="c1daa-132">nuget.exe bağlanabilir ve kullanma, NuGet v3 protokolü: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span><span class="sxs-lookup"><span data-stu-id="c1daa-132">nuget.exe can connect to and consume the NuGet v3 protocol at: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span></span>

## <a name="known-issues"></a><span data-ttu-id="c1daa-133">Bilinen Sorunlar</span><span class="sxs-lookup"><span data-stu-id="c1daa-133">Known Issues</span></span> ##

1.    <span data-ttu-id="c1daa-134">Paketi karşı yürütülemiyor bir `project.json` dosya - [928](https://github.com/NuGet/Home/issues/928)</span><span class="sxs-lookup"><span data-stu-id="c1daa-134">Cannot execute pack against a `project.json` file - [928](https://github.com/NuGet/Home/issues/928)</span></span>
2.    <span data-ttu-id="c1daa-135">Mono üzerinde - desteklenmeyen [1059](https://github.com/NuGet/Home/issues/1059)</span><span class="sxs-lookup"><span data-stu-id="c1daa-135">Is not supported on Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span></span>
3.    <span data-ttu-id="c1daa-136">Yerelleştirilmez - [1058](https://github.com/NuGet/Home/issues/1058), [1057](https://github.com/NuGet/Home/issues/1057)</span><span class="sxs-lookup"><span data-stu-id="c1daa-136">Is not localized - [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span></span>
4.    <span data-ttu-id="c1daa-137">, Yalnızca mevcut gibi imzalanmamış http://nuget.org/nuget.exe  -  [1073](https://github.com/NuGet/Home/issues/1073)</span><span class="sxs-lookup"><span data-stu-id="c1daa-137">Is not signed, just like the existing http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span></span>
