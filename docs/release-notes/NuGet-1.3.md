---
title: NuGet 1,3 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 1,3 sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 45d5caa46d532670e370b81f675663b3c5aaaa95
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825256"
---
# <a name="nuget-13-release-notes"></a><span data-ttu-id="44368-103">NuGet 1,3 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="44368-103">NuGet 1.3 Release Notes</span></span>

<span data-ttu-id="44368-104">[Nuget 1,2 sürüm notları](../release-notes/nuget-1.2.md) | [NuGet 1,4 sürüm notları](../release-notes/nuget-1.4.md)</span><span class="sxs-lookup"><span data-stu-id="44368-104">[NuGet 1.2 Release Notes](../release-notes/nuget-1.2.md) | [NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md)</span></span>

<span data-ttu-id="44368-105">NuGet 1,3, 25 Nisan 2011 ' de yayımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="44368-105">NuGet 1.3 was released on April 25, 2011.</span></span>

## <a name="new-features"></a><span data-ttu-id="44368-106">Yeni Özellikler</span><span class="sxs-lookup"><span data-stu-id="44368-106">New Features</span></span>

### <a name="streamlined-package-creation-with-symbol-server-integration"></a><span data-ttu-id="44368-107">Sembol sunucusu tümleştirmesiyle kolaylaştırılmış paket oluşturma</span><span class="sxs-lookup"><span data-stu-id="44368-107">Streamlined Package Creation with symbol server integration</span></span>

<span data-ttu-id="44368-108">NuGet ekibi, kaynaklarınızı ve PDB 'yi paketinizle birlikte yayımlamanın gerçekten basit bir yolunu sunmak için [SymbolSource.org](http://www.symbolsource.org/) adresindeki katlarla işbirliği yapar.</span><span class="sxs-lookup"><span data-stu-id="44368-108">The NuGet team partnered with the folks at [SymbolSource.org](http://www.symbolsource.org/) to offer a really simple way of publishing your sources and PDB’s along with your package.</span></span> <span data-ttu-id="44368-109">Bu, paketinizin tüketicilerinin hata ayıklayıcıdaki paketinizin kaynağına ilerlemenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="44368-109">This allows consumers of your package to step into the source for your package in the debugger.</span></span> <span data-ttu-id="44368-110">Daha fazla ayrıntı için, [bir sembol paketini oluşturma ve yayımlama](../create-packages/symbol-packages.md) hakkında bilgi edinmek için, kaynak ile NuGet paketlerini yayımlamanın kolay yolunu okuyun.</span><span class="sxs-lookup"><span data-stu-id="44368-110">For more details, read [Creating and Publishing a Symbol Package](../create-packages/symbol-packages.md) The easy way to publish NuGet packages with sources.</span></span> <span data-ttu-id="44368-111">Ayrıca, Mix11 adresindeki NuGet 'in bir parçası olarak bu özelliğin canlı bir gösterimini izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44368-111">You can also watch a live demonstration of this feature as part of the NuGet in Depth talk at Mix11.</span></span> <span data-ttu-id="44368-112">Bu özellik, videonun 20 dakikalık işaretiyle başlayarak tam olarak gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="44368-112">This feature is fully demonstrated starting at the 20 minute mark of the video.</span></span>

### <a name="open-packagepage-command"></a><span data-ttu-id="44368-113">`Open-PackagePage` komutu</span><span class="sxs-lookup"><span data-stu-id="44368-113">`Open-PackagePage` Command</span></span>

<span data-ttu-id="44368-114">Bu komut, paket yöneticisi konsolundan bir paketin proje sayfasına almayı kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="44368-114">This command makes it easy to get to the project page for a package from within the Package Manager Console.</span></span> <span data-ttu-id="44368-115">Ayrıca, paket için lisans URL 'sini ve kötüye kullanımı raporla sayfasını açma seçenekleri de sağlar.</span><span class="sxs-lookup"><span data-stu-id="44368-115">It also provides options to open the license URL and the report abuse page for the package.</span></span>
<span data-ttu-id="44368-116">Komutun sözdizimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="44368-116">The syntax for the command is:</span></span>

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

<span data-ttu-id="44368-117">`-PassThru` seçeneği, belirtilen URL 'nin değerini döndürmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="44368-117">The `-PassThru` option is used to return the value of the specified URL.</span></span>

<span data-ttu-id="44368-118">Örnekler:</span><span class="sxs-lookup"><span data-stu-id="44368-118">Examples:</span></span>

    PM> Open-PackagePage Ninject

<span data-ttu-id="44368-119">Nekleme paketinde belirtilen proje URL 'SI için bir tarayıcı açar.</span><span class="sxs-lookup"><span data-stu-id="44368-119">Opens a browser to the project URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -License

<span data-ttu-id="44368-120">Nekleme paketinde belirtilen lisans URL 'SI için bir tarayıcı açar.</span><span class="sxs-lookup"><span data-stu-id="44368-120">Opens a browser to the license URL specified in the Ninject package.</span></span>

    PM> Open-PackagePage Ninject -ReportAbuse

<span data-ttu-id="44368-121">Belirtilen paket için kötüye kullanımı raporlamak üzere kullanılan geçerli paket kaynağında URL 'ye bir tarayıcı açar.</span><span class="sxs-lookup"><span data-stu-id="44368-121">Opens a browser to the URL at the current package source used to report abuse for the specified package.</span></span>

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

<span data-ttu-id="44368-122">URL 'yi bir tarayıcıda açmadan $url, lisans URL 'sini değişkenine atar.</span><span class="sxs-lookup"><span data-stu-id="44368-122">Assigns the license URL to the variable, $url, without opening the URL in a browser.</span></span>

### <a name="performance-improvements"></a><span data-ttu-id="44368-123">Performans Geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="44368-123">Performance Improvements</span></span>

<span data-ttu-id="44368-124">NuGet 1,3, çok sayıda performans geliştirmesi sunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="44368-124">NuGet 1.3 introduces a lot of performance improvements.</span></span> <span data-ttu-id="44368-125">NuGet 1,3, Yerel Kullanıcı başına önbellek ekleyerek aynı paketin aynı sürümünü birden çok kez indirmeyi önler.</span><span class="sxs-lookup"><span data-stu-id="44368-125">NuGet 1.3 avoids downloading the same version of a package multiple times by including a local per-user cache.</span></span> <span data-ttu-id="44368-126">Önbellek, Paket Yöneticisi ayarları iletişim kutusu aracılığıyla erişilebilir ve temizlenir:</span><span class="sxs-lookup"><span data-stu-id="44368-126">The cache can be accessed and cleared via the Package Manager Settings dialog:</span></span>

![Paket önbelleği ayarlarıyla NuGet seçenekleri Iletişim kutusu](./media/nuget-options.png)

<span data-ttu-id="44368-128">Diğer performans geliştirmeleri, HTTP sıkıştırması desteği ekleme ve Visual Studio içinde paket yükleme hızını geliştirme içerir.</span><span class="sxs-lookup"><span data-stu-id="44368-128">Other performance improvements include adding support for HTTP compression and improving the package installation speed within Visual Studio.</span></span>

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a><span data-ttu-id="44368-129">Visual Studio ve NuGet. exe aynı paket kaynakları listesini kullanır</span><span class="sxs-lookup"><span data-stu-id="44368-129">Visual Studio and nuget.exe uses the same list of package sources</span></span>

<span data-ttu-id="44368-130">NuGet 1,3 ' den önce, NuGet. exe ve NuGet Visual Studio eklentisi tarafından kullanılan paket kaynaklarının listesi aynı yerde depolanmaz.</span><span class="sxs-lookup"><span data-stu-id="44368-130">Prior to NuGet 1.3, the list of package sources used by nuget.exe and the NuGet Visual Studio Add-In were not stored in the same place.</span></span> <span data-ttu-id="44368-131">NuGet 1,3 artık her iki yerde de aynı listeyi kullanır.</span><span class="sxs-lookup"><span data-stu-id="44368-131">NuGet 1.3 now uses the same list in both places.</span></span> <span data-ttu-id="44368-132">Liste `NuGet.Config` depolanır ve AppData klasöründe depolanır.</span><span class="sxs-lookup"><span data-stu-id="44368-132">The list is stored in `NuGet.Config` and stored in the AppData folder.</span></span>

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a><span data-ttu-id="44368-133">NuGet. exe, varsayılan olarak '. ' ile başlayan dosyaları ve klasörleri yoksayar</span><span class="sxs-lookup"><span data-stu-id="44368-133">nuget.exe Ignores Files and Folders that start with '.' by default</span></span>

<span data-ttu-id="44368-134">NuGet. exe, bu tür alt sürüm ve Mercurial gibi kaynak denetimi sistemleriyle düzgün şekilde çalışabilmek için, paketler oluştururken '. ' karakteriyle başlayan klasörleri ve dosyaları yoksayar.</span><span class="sxs-lookup"><span data-stu-id="44368-134">In order to make NuGet work well with source control systems such Subversion and Mercurial, nuget.exe ignores folders and files that start with the '.' character when creating packages.</span></span> <span data-ttu-id="44368-135">Bu, iki yeni bayrak kullanılarak geçersiz kılınabilir:</span><span class="sxs-lookup"><span data-stu-id="44368-135">This can be overridden using two new flags:</span></span>

* <span data-ttu-id="44368-136">__-Nodefaultexcludes__ , bu ayarı geçersiz kılmak ve tüm dosyaları dahil etmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="44368-136">__-NoDefaultExcludes__ is used to override this setting and include all files.</span></span>
* <span data-ttu-id="44368-137">__-Exclude__ , bir model kullanılarak dışlanacak diğer dosya/klasörleri eklemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="44368-137">__-Exclude__ is used to add other files/folders to exclude using a pattern.</span></span> <span data-ttu-id="44368-138">Örneğin, '. bak ' dosya uzantısına sahip tüm dosyaları dışlamak için</span><span class="sxs-lookup"><span data-stu-id="44368-138">For example, to exclude all files with the '.bak' file extension</span></span>

```cli
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

<span data-ttu-id="44368-139">_Not: varsayılan olarak, model özyinelemeli değildir._</span><span class="sxs-lookup"><span data-stu-id="44368-139">_Note: the pattern is not recursive by default._</span></span>

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a><span data-ttu-id="44368-140">WiX projeleri ve .NET mikro Framework desteği</span><span class="sxs-lookup"><span data-stu-id="44368-140">Support for WiX Projects and the .NET Micro Framework</span></span>

<span data-ttu-id="44368-141">NuGet, topluluk katkılarına yönelik olarak WiX proje türlerinin yanı sıra .NET mikro Framework için de destek içerir.</span><span class="sxs-lookup"><span data-stu-id="44368-141">Thanks to community contributions, NuGet includes support for WiX project types as well as the .NET Micro Framework.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="44368-142">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="44368-142">Bug Fixes</span></span>

<span data-ttu-id="44368-143">Hata düzeltmelerinin tam listesi için lütfen [Bu sürüm Için NuGet sorun İzleyicisi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)' ni görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="44368-143">For a full list of bug fixes, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="44368-144">Hata düzeltmeleri dikkat edilecek değer</span><span class="sxs-lookup"><span data-stu-id="44368-144">Bug fixes worth noting</span></span>

* <span data-ttu-id="44368-145">Kaynak dosyaları olan paketler her iki Web sitesinde ve Web uygulaması projelerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="44368-145">Packages with source files work in both Websites and in Web Application Projects.</span></span>
<span data-ttu-id="44368-146">Web siteleri için, kaynak dosyalar `App_Code` klasörüne kopyalanır</span><span class="sxs-lookup"><span data-stu-id="44368-146">For Websites, source files are copied into the `App_Code` folder</span></span>
