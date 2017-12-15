---
title: "NuGet 1.3 sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 5d1c2191-783f-4faa-b72e-356a59323d39
description: "NuGet bilinen sorunları, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere 1.3 için sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 1.3 sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7bc39efd5b9c550c3fdeddf9ad980c0bd9d4dcb3
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-13-release-notes"></a><span data-ttu-id="cd333-104">NuGet 1.3 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="cd333-104">NuGet 1.3 Release Notes</span></span>

<span data-ttu-id="cd333-105">[NuGet 1.2 sürüm notları](../release-notes/nuget-1.2.md) | [NuGet 1.4 sürüm notları](../release-notes/nuget-1.4.md)</span><span class="sxs-lookup"><span data-stu-id="cd333-105">[NuGet 1.2 Release Notes](../release-notes/nuget-1.2.md) | [NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md)</span></span>

<span data-ttu-id="cd333-106">NuGet 1.3 25 Nisan 2011'de serbest bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="cd333-106">NuGet 1.3 was released on April 25, 2011.</span></span>

## <a name="new-features"></a><span data-ttu-id="cd333-107">Yeni Özellikler</span><span class="sxs-lookup"><span data-stu-id="cd333-107">New Features</span></span>

### <a name="streamlined-package-creation-with-symbol-server-integration"></a><span data-ttu-id="cd333-108">Sembol sunucu Tümleştirmesi ile kolaylaştırılmış paketi oluşturma</span><span class="sxs-lookup"><span data-stu-id="cd333-108">Streamlined Package Creation with symbol server integration</span></span>

<span data-ttu-id="cd333-109">NuGet takım işbirliği çok kişi ile [SymbolSource.org](http://www.symbolsource.org/) kaynakları ve PDB'ın yayımlama yanı sıra, paketi gerçekten basit bir yol sunmak için.</span><span class="sxs-lookup"><span data-stu-id="cd333-109">The NuGet team partnered with the folks at [SymbolSource.org](http://www.symbolsource.org/) to offer a really simple way of publishing your sources and PDB’s along with your package.</span></span> <span data-ttu-id="cd333-110">Bu hata ayıklayıcı paketinize kaynağı adımla tüketicilerin paketinin sağlar.</span><span class="sxs-lookup"><span data-stu-id="cd333-110">This allows consumers of your package to step into the source for your package in the debugger.</span></span> <span data-ttu-id="cd333-111">Daha fazla ayrıntı için okuma [oluşturma ve yayımlama sembol paketi](../create-packages/symbol-packages.md) kaynaklarıyla NuGet paketlerini yayımlamak için en kolay yolu.</span><span class="sxs-lookup"><span data-stu-id="cd333-111">For more details, read [Creating and Publishing a Symbol Package](../create-packages/symbol-packages.md) The easy way to publish NuGet packages with sources.</span></span> <span data-ttu-id="cd333-112">Mix11 konuşun dinamik gösterimini bu özellik derinlemesine NuGet bir parçası olarak da izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cd333-112">You can also watch a live demonstration of this feature as part of the NuGet in Depth talk at Mix11.</span></span> <span data-ttu-id="cd333-113">Bu özellik, video 20 dakika işaretinde başlatma tam olarak gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="cd333-113">This feature is fully demonstrated starting at the 20 minute mark of the video.</span></span>

### <a name="open-packagepage-command"></a><span data-ttu-id="cd333-114">`Open-PackagePage`Komutu</span><span class="sxs-lookup"><span data-stu-id="cd333-114">`Open-PackagePage` Command</span></span>

<span data-ttu-id="cd333-115">Bu komut Paket Yöneticisi Konsolu içinden paketinden proje sayfasına almak kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="cd333-115">This command makes it easy to get to the project page for a package from within the Package Manager Console.</span></span> <span data-ttu-id="cd333-116">Ayrıca, lisans URL'sini ve paketi için rapor kötüye sayfası açmak için seçenekler sağlar.</span><span class="sxs-lookup"><span data-stu-id="cd333-116">It also provides options to open the license URL and the report abuse page for the package.</span></span>
<span data-ttu-id="cd333-117">Komut sözdizimi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="cd333-117">The syntax for the command is:</span></span>

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

<span data-ttu-id="cd333-118">`-PassThru` Seçeneği, belirtilen URL değeri döndürmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cd333-118">The `-PassThru` option is used to return the value of the specified URL.</span></span>

<span data-ttu-id="cd333-119">Örnekler:</span><span class="sxs-lookup"><span data-stu-id="cd333-119">Examples:</span></span>

    PM> Open-PackagePage Ninject

<span data-ttu-id="cd333-120">Ninject paketinde belirtilen proje URL'sini bir tarayıcı açar.</span><span class="sxs-lookup"><span data-stu-id="cd333-120">Opens a browser to the project URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -License

<span data-ttu-id="cd333-121">Ninject paketinde belirtilen lisans URL'sini bir tarayıcı açar.</span><span class="sxs-lookup"><span data-stu-id="cd333-121">Opens a browser to the license URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -ReportAbuse

<span data-ttu-id="cd333-122">Rapor Uygunsuz kullanım için belirtilen paket için kullanılan geçerli paket kaynağında URL'sini bir tarayıcı penceresinde açar.</span><span class="sxs-lookup"><span data-stu-id="cd333-122">Opens a browser to the URL at the current package source used to report abuse for the specified package.</span></span>

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

<span data-ttu-id="cd333-123">Lisans URL'sini $url değişkenine URL'yi bir tarayıcıda açmadan atar.</span><span class="sxs-lookup"><span data-stu-id="cd333-123">Assigns the license URL to the variable, $url, without opening the URL in a browser.</span></span>

### <a name="performance-improvements"></a><span data-ttu-id="cd333-124">Performans Geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="cd333-124">Performance Improvements</span></span>

<span data-ttu-id="cd333-125">NuGet 1.3 çok fazla performans geliştirmeleri tanıtır.</span><span class="sxs-lookup"><span data-stu-id="cd333-125">NuGet 1.3 introduces a lot of performance improvements.</span></span> <span data-ttu-id="cd333-126">NuGet 1.3 bir yerel kullanıcı başına önbellek dahil olmak üzere birden çok kez aynı bir paketin sürümü indirme önler.</span><span class="sxs-lookup"><span data-stu-id="cd333-126">NuGet 1.3 avoids downloading the same version of a package multiple times by including a local per-user cache.</span></span> <span data-ttu-id="cd333-127">Önbellek erişilen ve paket Yönetimi Ayarları iletişim kutusu temizlenmiş:</span><span class="sxs-lookup"><span data-stu-id="cd333-127">The cache can be accessed and cleared via the Package Manager Settings dialog:</span></span>

![Paket önbelleği ayarları ile NuGet Seçenekleri iletişim kutusu](./media/nuget-options.png)

<span data-ttu-id="cd333-129">HTTP sıkıştırma desteği ekleme ve Visual Studio içindeki paketi yükleme hızı artırma diğer performans iyileştirmeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="cd333-129">Other performance improvements include adding support for HTTP compression and improving the package installation speed within Visual Studio.</span></span>

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a><span data-ttu-id="cd333-130">Visual Studio ve nuget.exe kullanan paket kaynaklarını aynı listesi</span><span class="sxs-lookup"><span data-stu-id="cd333-130">Visual Studio and nuget.exe uses the same list of package sources</span></span>

<span data-ttu-id="cd333-131">NuGet 1.3 önce nuget.exe ve NuGet Visual Studio eklentisi tarafından kullanılan paket kaynaklarını listesi depolanmadığını aynı yerde.</span><span class="sxs-lookup"><span data-stu-id="cd333-131">Prior to NuGet 1.3, the list of package sources used by nuget.exe and the NuGet Visual Studio Add-In were not stored in the same place.</span></span> <span data-ttu-id="cd333-132">NuGet 1.3 artık her iki yerde de aynı listesini kullanır.</span><span class="sxs-lookup"><span data-stu-id="cd333-132">NuGet 1.3 now uses the same list in both places.</span></span> <span data-ttu-id="cd333-133">Listenin depolanan `NuGet.Config` ve AppData klasöründe depolanır.</span><span class="sxs-lookup"><span data-stu-id="cd333-133">The list is stored in `NuGet.Config` and stored in the AppData folder.</span></span>

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a><span data-ttu-id="cd333-134">nuget.exe yoksayar dosyaları ve başlayın klasörleri '.' varsayılan olarak</span><span class="sxs-lookup"><span data-stu-id="cd333-134">nuget.exe Ignores Files and Folders that start with '.' by default</span></span>

<span data-ttu-id="cd333-135">Bu tür alt sürüme ve Mercurial de kaynak denetimi sistemleriyle iş NuGet yapmak için nuget.exe ile başlayan dosya ve klasörleri yoksayar '.' karakteri paket oluştururken.</span><span class="sxs-lookup"><span data-stu-id="cd333-135">In order to make NuGet work well with source control systems such Subversion and Mercurial, nuget.exe ignores folders and files that start with the '.' character when creating packages.</span></span> <span data-ttu-id="cd333-136">Bu iki yeni bayrakları kullanılarak geçersiz kılınabilir:</span><span class="sxs-lookup"><span data-stu-id="cd333-136">This can be overridden using two new flags:</span></span>

* <span data-ttu-id="cd333-137">__-NoDefaultExcludes__ bu ayarını geçersiz kılmak ve tüm dosyaları dahil etmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cd333-137">__-NoDefaultExcludes__ is used to override this setting and include all files.</span></span>
* <span data-ttu-id="cd333-138">__-Hariç__ diğer dosyalar/desen kullanarak hariç tutulacak klasörleri eklemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cd333-138">__-Exclude__ is used to add other files/folders to exclude using a pattern.</span></span> <span data-ttu-id="cd333-139">Örneğin, '.bak' dosya uzantısına sahip tüm dosyaları dışlayın</span><span class="sxs-lookup"><span data-stu-id="cd333-139">For example, to exclude all files with the '.bak' file extension</span></span>

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

<span data-ttu-id="cd333-140">_Not: düzeni varsayılan özyinelemeli değil._</span><span class="sxs-lookup"><span data-stu-id="cd333-140">_Note: the pattern is not recursive by default._</span></span>

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a><span data-ttu-id="cd333-141">WiX projeleri ve mikro .NET Framework desteği</span><span class="sxs-lookup"><span data-stu-id="cd333-141">Support for WiX Projects and the .NET Micro Framework</span></span>

<span data-ttu-id="cd333-142">Topluluk Katkıları sayesinde NuGet .NET mikro Framework yanı sıra WiX proje türleri için destek içerir.</span><span class="sxs-lookup"><span data-stu-id="cd333-142">Thanks to community contributions, NuGet includes support for WiX project types as well as the .NET Micro Framework.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="cd333-143">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="cd333-143">Bug Fixes</span></span>

<span data-ttu-id="cd333-144">Hata düzeltmeleri tam bir listesi için lütfen görüntülemek [NuGet sorun İzleyicisi bu sürüm için](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="cd333-144">For a full list of bug fixes, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="cd333-145">Eşitlenmeyeceği hata düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="cd333-145">Bug fixes worth noting</span></span>

* <span data-ttu-id="cd333-146">Her iki Web siteleri ve Web Uygulama projeleri paket kaynak dosyaları ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="cd333-146">Packages with source files work in both Websites and in Web Application Projects.</span></span>
<span data-ttu-id="cd333-147">Web siteleri için kaynak dosyaları içine kopyalanır `App_Code` klasörü</span><span class="sxs-lookup"><span data-stu-id="cd333-147">For Websites, source files are copied into the `App_Code` folder</span></span>
