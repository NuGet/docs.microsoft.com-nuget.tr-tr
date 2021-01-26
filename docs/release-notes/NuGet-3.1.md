---
title: NuGet 3,1 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 3,1 sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e1dc31e2543610b1da395f77fd2424bd85d985ef
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776533"
---
# <a name="nuget-31-release-notes"></a><span data-ttu-id="f8d52-103">NuGet 3,1 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="f8d52-103">NuGet 3.1 Release Notes</span></span>

<span data-ttu-id="f8d52-104">[NuGet 3,0 sürüm notları](../release-notes/nuget-3.0.0.md)  |  [NuGet 3.1.1 sürüm notları](../release-notes/nuget-3.1.1.md)</span><span class="sxs-lookup"><span data-stu-id="f8d52-104">[NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 Release Notes](../release-notes/nuget-3.1.1.md)</span></span>

<span data-ttu-id="f8d52-105">NuGet 3,1, Visual Studio 2015 için Evrensel Windows Platformu SDK 'Sı için paketlenmiş bir uzantı olarak 27 Temmuz 2015 tarihinde yayımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="f8d52-105">NuGet 3.1 was released on July 27, 2015 as a bundled extension to the Universal Windows Platform SDK for Visual Studio 2015.</span></span> <span data-ttu-id="f8d52-106">Windows geliştirme deneyiminin daha önce başlatılmış olan NuGet platformlar arası çalışmanın avantajlarından yararlanması için, bu sürümü Windows platformu SDK ile birlikte sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="f8d52-106">We delivered this release with the Windows Platform SDK so that the Windows development experience could take advantage of the NuGet cross-platform work that had been previously started.</span></span> <span data-ttu-id="f8d52-107">Bu NuGet uzantısı sürümü yalnızca Visual Studio 2015 için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f8d52-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="f8d52-108">Her zaman hata düzeltmeleri ve yeni özelliklerle güncelleştirmeler yayımladığımızda, Visual Studio Galerisi güncelleştirmesine erişimi olan geliştiricilerin, mevcut en son sürüme erişmesini öneririz.</span><span class="sxs-lookup"><span data-stu-id="f8d52-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are always publishing updates with bug fixes and new features.</span></span>

## <a name="nuget-visual-studio-extension"></a><span data-ttu-id="f8d52-109">NuGet Visual Studio uzantısı</span><span class="sxs-lookup"><span data-stu-id="f8d52-109">NuGet Visual Studio Extension</span></span>

<span data-ttu-id="f8d52-110">Bu sürümdeki sorunlar ve özellikler, GitHub 'da ["3,1 RTM UWP geçişli destek" kilometre taşına](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  göre etiketlendi ve 3,1 sürümündeki 67 sorunlarını kapattık.</span><span class="sxs-lookup"><span data-stu-id="f8d52-110">Issues and features in this release are tagged on GitHub with the ["3.1 RTM UWP transitive support" milestone](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  In total, we closed 67 issues in the 3.1 release.</span></span>

### <a name="new-features"></a><span data-ttu-id="f8d52-111">Yeni Özellikler</span><span class="sxs-lookup"><span data-stu-id="f8d52-111">New Features</span></span>

* <span data-ttu-id="f8d52-112">`project.json` Windows UWP ve ASP.NET 5 desteği desteği</span><span class="sxs-lookup"><span data-stu-id="f8d52-112">`project.json` support for Windows UWP and ASP.NET 5 support</span></span>
* <span data-ttu-id="f8d52-113">Geçişli paket yüklemesi</span><span class="sxs-lookup"><span data-stu-id="f8d52-113">Transitive package installation</span></span>

<span data-ttu-id="f8d52-114">Bu özelliklerin açıklaması ve tanımı belgelerde başka bir yerde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="f8d52-114">Description and definition of these features can be found elsewhere in the documentation.</span></span>

### <a name="deprecated"></a><span data-ttu-id="f8d52-115">Kullanım Dışı</span><span class="sxs-lookup"><span data-stu-id="f8d52-115">Deprecated</span></span>

<span data-ttu-id="f8d52-116">Aşağıdaki özellikler artık Visual Studio 2015 için kullanılamaz:</span><span class="sxs-lookup"><span data-stu-id="f8d52-116">The following features are no longer available for Visual Studio 2015:</span></span>

* <span data-ttu-id="f8d52-117">Çözüm düzeyi paketler artık yüklenemez</span><span class="sxs-lookup"><span data-stu-id="f8d52-117">Solution level packages can no longer be installed</span></span>

<span data-ttu-id="f8d52-118">Aşağıdaki özellikler artık Visual Studio 2015 ve belirtimi kullanan projeler için kullanılamaz `project.json`</span><span class="sxs-lookup"><span data-stu-id="f8d52-118">The following features are no longer available for Visual Studio 2015 and projects that use the `project.json` specification</span></span>

* <span data-ttu-id="f8d52-119">`install.ps1` ve `uninstall.ps1` -Bu betikler paket yükleme, geri yükleme, güncelleştirme ve kaldırma işlemi sırasında yok sayılır</span><span class="sxs-lookup"><span data-stu-id="f8d52-119">`install.ps1` and `uninstall.ps1` - These scripts will be ignored during package install, restore, update, and uninstall</span></span>
* <span data-ttu-id="f8d52-120">Yapılandırma dönüştürmeleri yoksayılacak</span><span class="sxs-lookup"><span data-stu-id="f8d52-120">Configuration transforms will be ignored</span></span>
* <span data-ttu-id="f8d52-121">İçerik taşınır, ancak bir projeye kopyalanmaz.</span><span class="sxs-lookup"><span data-stu-id="f8d52-121">Content will be carried, but not copied into a project.</span></span>
    * <span data-ttu-id="f8d52-122">Takım, bu özelliği yeniden uygulamak için çalışıyor, tartışma ve ilerleme durumunu takip eden: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span><span class="sxs-lookup"><span data-stu-id="f8d52-122">The team is working to re-implement this feature, follow the discussion and progress at: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)</span></span>


### <a name="known-issues"></a><span data-ttu-id="f8d52-123">Bilinen Sorunlar</span><span class="sxs-lookup"><span data-stu-id="f8d52-123">Known Issues</span></span>

<span data-ttu-id="f8d52-124">Bu sürümle birlikte sunulan bazı bilinen sorunlar oluştu.</span><span class="sxs-lookup"><span data-stu-id="f8d52-124">There were a number of known issues delivered with this release.</span></span>

* <span data-ttu-id="f8d52-125">Windows 10 SDK ile 3,1 sürümünün yüklenmesi, daha önce yüklenmiş olan herhangi bir NuGet uzantısı sürümünün indirgenmesini sağlayacak</span><span class="sxs-lookup"><span data-stu-id="f8d52-125">Installation of the 3.1 release with the Windows 10 SDK will downgrade any version of NuGet extension that was previously installed</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="f8d52-126">NuGet komut satırı</span><span class="sxs-lookup"><span data-stu-id="f8d52-126">NuGet Command-line</span></span>

<span data-ttu-id="f8d52-127">NuGet komut satırı yürütülebilir dosyası güncelleştirildi ve yeni bir dağıtılabilir konuma taşındı nuget.exe geçmiş sürümlerinin kullanılabilir hale getirilmeye devam edebilmesi için.</span><span class="sxs-lookup"><span data-stu-id="f8d52-127">The NuGet command-line executable was updated and moved to a new distributable location so that historical versions of nuget.exe can continue to be made available.</span></span>  <span data-ttu-id="f8d52-128">Windows için nuget.exe 'nin 3,1 Beta sürümünü şu adreste indirebilirsiniz: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span><span class="sxs-lookup"><span data-stu-id="f8d52-128">You can download the 3.1 beta version of nuget.exe for Windows at: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)</span></span>

<span data-ttu-id="f8d52-129">Yeni dağıtılabilir konum dist.nuget.org konağında bulunur ve bu şablonu izleyen bir klasör yapısıdır:</span><span class="sxs-lookup"><span data-stu-id="f8d52-129">The new distributable location resides on the dist.nuget.org host, with a folder structure that follows this template:</span></span>

```
{platform supported}/{version}/nuget.exe
```

### <a name="new-features"></a><span data-ttu-id="f8d52-130">Yeni Özellikler</span><span class="sxs-lookup"><span data-stu-id="f8d52-130">New Features</span></span>

* <span data-ttu-id="f8d52-131">nuget.exe, paketleri bir dosya kullanan projelere geri yükleyebilir ve yükleyebilir `project.json` .</span><span class="sxs-lookup"><span data-stu-id="f8d52-131">nuget.exe can restore and install packages into projects that use a `project.json` file.</span></span>
* <span data-ttu-id="f8d52-132">nuget.exe, şu adreste bulunan NuGet v3 protokolüne bağlanabilir ve bunları kullanabilir: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span><span class="sxs-lookup"><span data-stu-id="f8d52-132">nuget.exe can connect to and consume the NuGet v3 protocol at: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)</span></span>

## <a name="known-issues"></a><span data-ttu-id="f8d52-133">Bilinen Sorunlar</span><span class="sxs-lookup"><span data-stu-id="f8d52-133">Known Issues</span></span> ##

1.    <span data-ttu-id="f8d52-134">Paket bir dosyaya karşı yürütülemiyor `project.json` - [928](https://github.com/NuGet/Home/issues/928)</span><span class="sxs-lookup"><span data-stu-id="f8d52-134">Cannot execute pack against a `project.json` file - [928](https://github.com/NuGet/Home/issues/928)</span></span>
2.    <span data-ttu-id="f8d52-135">Mono- [1059](https://github.com/NuGet/Home/issues/1059) ' de desteklenmez</span><span class="sxs-lookup"><span data-stu-id="f8d52-135">Is not supported on Mono - [1059](https://github.com/NuGet/Home/issues/1059)</span></span>
3.    <span data-ttu-id="f8d52-136">Yerelleştirilmiş değil- [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span><span class="sxs-lookup"><span data-stu-id="f8d52-136">Is not localized - [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)</span></span>
4.    <span data-ttu-id="f8d52-137">, Tıpkı var olan http://nuget.org/nuget.exe  -  [1073](https://github.com/NuGet/Home/issues/1073) gibi imzalanmadı</span><span class="sxs-lookup"><span data-stu-id="f8d52-137">Is not signed, just like the existing http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)</span></span>
