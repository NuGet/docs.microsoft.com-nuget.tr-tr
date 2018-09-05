---
title: NuGet 1.3 sürüm notları
description: NuGet bilinen sorunları, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr 1.3 için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fa89af100096356c2ffb4d6c501c4a34296ad0ea
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551357"
---
# <a name="nuget-13-release-notes"></a><span data-ttu-id="d0417-103">NuGet 1.3 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="d0417-103">NuGet 1.3 Release Notes</span></span>

<span data-ttu-id="d0417-104">[NuGet 1.2 sürüm notları](../release-notes/nuget-1.2.md) | [1.4 NuGet sürüm notları](../release-notes/nuget-1.4.md)</span><span class="sxs-lookup"><span data-stu-id="d0417-104">[NuGet 1.2 Release Notes](../release-notes/nuget-1.2.md) | [NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md)</span></span>

<span data-ttu-id="d0417-105">NuGet 1.3 25 Nisan 2011'de yayınlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="d0417-105">NuGet 1.3 was released on April 25, 2011.</span></span>

## <a name="new-features"></a><span data-ttu-id="d0417-106">Yeni Özellikler</span><span class="sxs-lookup"><span data-stu-id="d0417-106">New Features</span></span>

### <a name="streamlined-package-creation-with-symbol-server-integration"></a><span data-ttu-id="d0417-107">Sembol sunucusu tümleştirme kolaylaştırılmış paket oluşturma</span><span class="sxs-lookup"><span data-stu-id="d0417-107">Streamlined Package Creation with symbol server integration</span></span>

<span data-ttu-id="d0417-108">NuGet takım iş Birliği yaparak yeni başlayanlar ile [SymbolSource.org](http://www.symbolsource.org/) kaynakları ve PDB'ın yanı sıra, paket yayımlama gerçekten çok basit bir yol sunuyor.</span><span class="sxs-lookup"><span data-stu-id="d0417-108">The NuGet team partnered with the folks at [SymbolSource.org](http://www.symbolsource.org/) to offer a really simple way of publishing your sources and PDB’s along with your package.</span></span> <span data-ttu-id="d0417-109">Bu, paket hata ayıklayıcı kaynağı adımla tüketicilerin paketinizin sağlar.</span><span class="sxs-lookup"><span data-stu-id="d0417-109">This allows consumers of your package to step into the source for your package in the debugger.</span></span> <span data-ttu-id="d0417-110">Daha fazla bilgi edinmek için [oluşturma ve bir sembol Paketi Yayımlama](../create-packages/symbol-packages.md) kaynaklarıyla NuGet paketlerini yayımlamak için kolay bir yol.</span><span class="sxs-lookup"><span data-stu-id="d0417-110">For more details, read [Creating and Publishing a Symbol Package](../create-packages/symbol-packages.md) The easy way to publish NuGet packages with sources.</span></span> <span data-ttu-id="d0417-111">Mix11 konuşma bir canlı tanıtım bu özelliğin NuGet derinlemesine bir parçası olarak da izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0417-111">You can also watch a live demonstration of this feature as part of the NuGet in Depth talk at Mix11.</span></span> <span data-ttu-id="d0417-112">Bu özellik, tam olarak 20 dakikalık video işaretinde gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d0417-112">This feature is fully demonstrated starting at the 20 minute mark of the video.</span></span>

### <a name="open-packagepage-command"></a><span data-ttu-id="d0417-113">`Open-PackagePage` Komutu</span><span class="sxs-lookup"><span data-stu-id="d0417-113">`Open-PackagePage` Command</span></span>

<span data-ttu-id="d0417-114">Bu komut Paket Yöneticisi Konsolu içinden bir paket için proje sayfasına ulaşmak kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="d0417-114">This command makes it easy to get to the project page for a package from within the Package Manager Console.</span></span> <span data-ttu-id="d0417-115">Ayrıca, lisans URL'sini ve paket için rapor kötüye sayfasını açmak için seçenekler sağlar.</span><span class="sxs-lookup"><span data-stu-id="d0417-115">It also provides options to open the license URL and the report abuse page for the package.</span></span>
<span data-ttu-id="d0417-116">Komutu için sözdizimi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="d0417-116">The syntax for the command is:</span></span>

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

<span data-ttu-id="d0417-117">`-PassThru` Seçeneği, belirtilen URL değerini döndürmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d0417-117">The `-PassThru` option is used to return the value of the specified URL.</span></span>

<span data-ttu-id="d0417-118">Örnekler:</span><span class="sxs-lookup"><span data-stu-id="d0417-118">Examples:</span></span>

    PM> Open-PackagePage Ninject

<span data-ttu-id="d0417-119">Ninject paketinde belirtilen proje URL'sini bir tarayıcı açar.</span><span class="sxs-lookup"><span data-stu-id="d0417-119">Opens a browser to the project URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -License

<span data-ttu-id="d0417-120">Ninject paketinde belirtilen lisans URL'sini bir tarayıcı açar.</span><span class="sxs-lookup"><span data-stu-id="d0417-120">Opens a browser to the license URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -ReportAbuse

<span data-ttu-id="d0417-121">Uygunsuz kullanımı için belirtilen paket için kullanılan geçerli paket kaynağı URL'SİNDE bir tarayıcı açar.</span><span class="sxs-lookup"><span data-stu-id="d0417-121">Opens a browser to the URL at the current package source used to report abuse for the specified package.</span></span>

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

<span data-ttu-id="d0417-122">Lisans URL'sini bir tarayıcıda URL'yi açmaya gerek kalmadan $url, değişkenine atar.</span><span class="sxs-lookup"><span data-stu-id="d0417-122">Assigns the license URL to the variable, $url, without opening the URL in a browser.</span></span>

### <a name="performance-improvements"></a><span data-ttu-id="d0417-123">Performans Geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="d0417-123">Performance Improvements</span></span>

<span data-ttu-id="d0417-124">NuGet 1.3 birçok performans geliştirmeleri sunar.</span><span class="sxs-lookup"><span data-stu-id="d0417-124">NuGet 1.3 introduces a lot of performance improvements.</span></span> <span data-ttu-id="d0417-125">Bir yerel kullanıcı başına önbellek dahil olmak üzere birden çok kez aynı sürümüne sahip bir paket indiriliyor NuGet 1.3 önler.</span><span class="sxs-lookup"><span data-stu-id="d0417-125">NuGet 1.3 avoids downloading the same version of a package multiple times by including a local per-user cache.</span></span> <span data-ttu-id="d0417-126">Önbellek, erişilebilir ve Paket Yöneticisi Ayarları iletişim kutusu temizlenmiş:</span><span class="sxs-lookup"><span data-stu-id="d0417-126">The cache can be accessed and cleared via the Package Manager Settings dialog:</span></span>

![Paket önbelleği ayarları ile NuGet Seçenekleri iletişim](./media/nuget-options.png)

<span data-ttu-id="d0417-128">Diğer performans geliştirmelerine, HTTP sıkıştırma desteği eklemeyi ve Visual Studio içindeki paketi yükleme hızını geliştirmek içerir.</span><span class="sxs-lookup"><span data-stu-id="d0417-128">Other performance improvements include adding support for HTTP compression and improving the package installation speed within Visual Studio.</span></span>

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a><span data-ttu-id="d0417-129">Visual Studio ve nuget.exe kullandığı aynı paket kaynaklarının listesi</span><span class="sxs-lookup"><span data-stu-id="d0417-129">Visual Studio and nuget.exe uses the same list of package sources</span></span>

<span data-ttu-id="d0417-130">NuGet 1.3 önce nuget.exe ve NuGet Visual Studio eklentisi tarafından kullanılan paket kaynaklarının listesi depolanmamış aynı yerde.</span><span class="sxs-lookup"><span data-stu-id="d0417-130">Prior to NuGet 1.3, the list of package sources used by nuget.exe and the NuGet Visual Studio Add-In were not stored in the same place.</span></span> <span data-ttu-id="d0417-131">NuGet 1.3, artık her iki yerde de aynı listesini kullanır.</span><span class="sxs-lookup"><span data-stu-id="d0417-131">NuGet 1.3 now uses the same list in both places.</span></span> <span data-ttu-id="d0417-132">Listenin depolanan `NuGet.Config` ve AppData klasöründe depolanır.</span><span class="sxs-lookup"><span data-stu-id="d0417-132">The list is stored in `NuGet.Config` and stored in the AppData folder.</span></span>

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a><span data-ttu-id="d0417-133">nuget.exe dosyaları yoksayar ve ile başlayan Klasörler '.' varsayılan olarak</span><span class="sxs-lookup"><span data-stu-id="d0417-133">nuget.exe Ignores Files and Folders that start with '.' by default</span></span>

<span data-ttu-id="d0417-134">NuGet Subversion ve Mercurial gibi kaynak denetimi sistemleriyle de çalışır hale getirmek için nuget.exe başlayan dosya ve klasörler yoksayar '.' karakteri paket oluştururken.</span><span class="sxs-lookup"><span data-stu-id="d0417-134">In order to make NuGet work well with source control systems such Subversion and Mercurial, nuget.exe ignores folders and files that start with the '.' character when creating packages.</span></span> <span data-ttu-id="d0417-135">Bu iki yeni bayrakları kullanılarak geçersiz kılınabilir:</span><span class="sxs-lookup"><span data-stu-id="d0417-135">This can be overridden using two new flags:</span></span>

* <span data-ttu-id="d0417-136">__-NoDefaultExcludes__ tüm dosyaları içerir ve bu ayarı geçersiz kılmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d0417-136">__-NoDefaultExcludes__ is used to override this setting and include all files.</span></span>
* <span data-ttu-id="d0417-137">__-Hariç__ diğer dosyaları/bir desen kullanarak hariç tutulacak klasörler eklemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d0417-137">__-Exclude__ is used to add other files/folders to exclude using a pattern.</span></span> <span data-ttu-id="d0417-138">Örneğin, '.bak' dosya uzantısına sahip tüm dosyaları dışarıda bırak</span><span class="sxs-lookup"><span data-stu-id="d0417-138">For example, to exclude all files with the '.bak' file extension</span></span>

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

<span data-ttu-id="d0417-139">_Not: desen varsayılan özyinelemeli değildir._</span><span class="sxs-lookup"><span data-stu-id="d0417-139">_Note: the pattern is not recursive by default._</span></span>

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a><span data-ttu-id="d0417-140">WiX projeleri ve mikro .NET Framework desteği</span><span class="sxs-lookup"><span data-stu-id="d0417-140">Support for WiX Projects and the .NET Micro Framework</span></span>

<span data-ttu-id="d0417-141">Topluluk Katkıları sayesinde NuGet .NET mikro Framework yanı sıra WiX proje türleri için destek içerir.</span><span class="sxs-lookup"><span data-stu-id="d0417-141">Thanks to community contributions, NuGet includes support for WiX project types as well as the .NET Micro Framework.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="d0417-142">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="d0417-142">Bug Fixes</span></span>

<span data-ttu-id="d0417-143">Hata düzeltmeleri tam bir listesi için lütfen [bu sürüm için NuGet sorun İzleyicisi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="d0417-143">For a full list of bug fixes, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="d0417-144">Önemli hata düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="d0417-144">Bug fixes worth noting</span></span>

* <span data-ttu-id="d0417-145">Her iki Web siteleri ve Web Uygulama projeleri paket kaynak dosyaları ile çalışma.</span><span class="sxs-lookup"><span data-stu-id="d0417-145">Packages with source files work in both Websites and in Web Application Projects.</span></span>
<span data-ttu-id="d0417-146">Web siteleri için kaynak dosyaları içine kopyalanır `App_Code` klasörü</span><span class="sxs-lookup"><span data-stu-id="d0417-146">For Websites, source files are copied into the `App_Code` folder</span></span>
