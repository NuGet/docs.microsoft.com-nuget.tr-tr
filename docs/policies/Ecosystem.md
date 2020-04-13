---
title: NuGet Ekosistemine Genel Bakış
description: NuGet ekosisteminde NuGet kaynakları, Microsoft dışı NuGet projeleri, yardımcı programlar ve eğitim materyalleri dahil olmak üzere kapsamlı kaynaklar.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 31243076f36f6ff274c4377c1773ea59dda8c834
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64495495"
---
# <a name="an-overview-of-the-nuget-ecosystem"></a><span data-ttu-id="eb053-103">NuGet ekosistemine genel bakış</span><span class="sxs-lookup"><span data-stu-id="eb053-103">An overview of the NuGet ecosystem</span></span>

<span data-ttu-id="eb053-104">2010 yılında piyasaya sürülmesinden bu yana, NuGet geliştirme süreçlerinin farklı yönlerini geliştirmek ve otomatikleştirmek için büyük bir fırsat sundu.</span><span class="sxs-lookup"><span data-stu-id="eb053-104">Since it's introduction in 2010, NuGet has presented a great opportunity to improve and automate different aspects of the development processes.</span></span>

<span data-ttu-id="eb053-105">NuGet izin verilen [Apache v2 lisansı](http://choosealicense.com/licenses/apache/)altında açık kaynak olduğundan, diğer projeler NuGet kaldıraç ve şirketler kendi ürünlerinde bunun için destek inşa edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eb053-105">Because NuGet is open source under a permissive [Apache v2 license](http://choosealicense.com/licenses/apache/), other projects can leverage NuGet and companies can build support for it in their products.</span></span> <span data-ttu-id="eb053-106">İster açık kaynak projeleri ister kurumsal uygulama geliştirme olsun, NuGet ve NuGet ve çevresinde yerleşik diğer uygulamalar, yazılım geliştirme sürecinizi geliştirmek için geniş bir araç ekosistemi sağlar.</span><span class="sxs-lookup"><span data-stu-id="eb053-106">Whether for open-source projects or enterprise application development, NuGet and other applications built on and around NuGet provide a broad ecosystem of tools for improving your software development process.</span></span>

<span data-ttu-id="eb053-107">Tüm bu projeler geliştirici katkıları nedeniyle yenilik yapabiliyor.</span><span class="sxs-lookup"><span data-stu-id="eb053-107">All of these projects are able to innovate because of developer contributions.</span></span> <span data-ttu-id="eb053-108">NuGet'in kendisine katkıda bulunduğugibi, hataları ve yeni özellik fikirlerini bildirerek, geri bildirim sağlayarak, dokümantasyon yazarak ve mümkün olduğunca kod katkıda bulunarak bu projelere de katkıda bulunun.</span><span class="sxs-lookup"><span data-stu-id="eb053-108">Just as you contribute to NuGet itself, also make contribution to these projects by reporting defects and new feature ideas, providing feedback, writing documentation, and contributing code where possible.</span></span>

## <a name="net-foundation-projects"></a><span data-ttu-id="eb053-109">.NET Vakfı projeleri</span><span class="sxs-lookup"><span data-stu-id="eb053-109">.NET Foundation projects</span></span>

<span data-ttu-id="eb053-110">NuGet, Microsoft geliştirme platformu için ücretsiz, açık kaynak kodlu paket yönetim sistemi sağlar.</span><span class="sxs-lookup"><span data-stu-id="eb053-110">NuGet provides a free, open source package management system for the Microsoft development platform.</span></span> <span data-ttu-id="eb053-111">Bu birkaç istemci araçları yanı sıra [resmi NuGet Galerisi](http://www.nuget.org)oluşturan hizmetler kümesi oluşur.</span><span class="sxs-lookup"><span data-stu-id="eb053-111">It consists of a few client tools as well as the set of services that comprise the [official NuGet Gallery](http://www.nuget.org).</span></span> <span data-ttu-id="eb053-112">Bunlar birleştiğinde [.NET Foundation](http://www.dotnetfoundation.org/)tarafından yönetilen NuGet projesini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="eb053-112">Combined, these form the NuGet project which is governed by the [.NET Foundation](http://www.dotnetfoundation.org/).</span></span>

<span data-ttu-id="eb053-113">NuGet Organizasyonu GitHub'da çeşitli depolar içerir.</span><span class="sxs-lookup"><span data-stu-id="eb053-113">The NuGet Organization contains various repositories on GitHub.</span></span> <span data-ttu-id="eb053-114">[https://github.com/Nuget/Home](https://github.com/Nuget/Home)tüm depolara ve çeşitli NuGet bileşenlerinin nerede bulunacağıhakkında genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="eb053-114">[https://github.com/Nuget/Home](https://github.com/Nuget/Home) gives an overview of all the repositories and where to find the various NuGet components.</span></span>

## <a name="microsoft-projects"></a><span data-ttu-id="eb053-115">Microsoft projeleri</span><span class="sxs-lookup"><span data-stu-id="eb053-115">Microsoft projects</span></span>

<span data-ttu-id="eb053-116">Microsoft, NuGet'in geliştirilmesine büyük katkıda bulunmuştur.</span><span class="sxs-lookup"><span data-stu-id="eb053-116">Microsoft has contributed extensively to the development of NuGet.</span></span> <span data-ttu-id="eb053-117">Microsoft çalışanları tarafından yapılan tüm katkılar da açık kaynak kodludur ve .NET Foundation'a bağışlanır (telif hakları dahil).</span><span class="sxs-lookup"><span data-stu-id="eb053-117">All contributions made by Microsoft employees are also open source and are donated (including copyrights) to the .NET Foundation.</span></span>

## <a name="non-microsoft-projects"></a><span data-ttu-id="eb053-118">Microsoft dışı projeler</span><span class="sxs-lookup"><span data-stu-id="eb053-118">Non-Microsoft projects</span></span>

<span data-ttu-id="eb053-119">Birçok kişi ve şirket NuGet ekosistemine önemli katkılarda bulunmuştur.</span><span class="sxs-lookup"><span data-stu-id="eb053-119">Many other individuals and companies have made significant contributions to the NuGet ecosystem.</span></span> <span data-ttu-id="eb053-120">Burada listelenen her proje, temel NuGet bileşenlerinden farklı bir lisansa sahip olabilir, bu nedenle lisans koşullarının kullanılmadan önce kabul edilebilir olduğunu onaylayın:</span><span class="sxs-lookup"><span data-stu-id="eb053-120">Each project listed here may have a different license than the core NuGet components, so confirm that the license terms are acceptable prior to use:</span></span>

- [<span data-ttu-id="eb053-121">AppVeyor CI</span><span class="sxs-lookup"><span data-stu-id="eb053-121">AppVeyor CI</span></span>](https://www.appveyor.com/)
- [<span data-ttu-id="eb053-122">Artifactory</span><span class="sxs-lookup"><span data-stu-id="eb053-122">Artifactory</span></span>](https://www.jfrog.com/artifactory/)
- [<span data-ttu-id="eb053-123">BoxStarter</span><span class="sxs-lookup"><span data-stu-id="eb053-123">BoxStarter</span></span>](http://boxstarter.org/)
- [<span data-ttu-id="eb053-124">Çikolatalı</span><span class="sxs-lookup"><span data-stu-id="eb053-124">Chocolatey</span></span>](https://chocolatey.org/)
- [<span data-ttu-id="eb053-125">CoApp</span><span class="sxs-lookup"><span data-stu-id="eb053-125">CoApp</span></span>](http://coapp.org/)
- [<span data-ttu-id="eb053-126">JetBrains ReSharper</span><span class="sxs-lookup"><span data-stu-id="eb053-126">JetBrains ReSharper</span></span>](https://resharper-plugins.jetbrains.com/)
- [<span data-ttu-id="eb053-127">JetBrains TeamCity</span><span class="sxs-lookup"><span data-stu-id="eb053-127">JetBrains TeamCity</span></span>](https://www.jetbrains.com/teamcity/)
- [<span data-ttu-id="eb053-128">Klondike</span><span class="sxs-lookup"><span data-stu-id="eb053-128">Klondike</span></span>](https://github.com/themotleyfool/Klondike)
- [<span data-ttu-id="eb053-129">MinimalNugetSunucu</span><span class="sxs-lookup"><span data-stu-id="eb053-129">MinimalNugetServer</span></span>](https://github.com/TanukiSharp/MinimalNugetServer)
- [<span data-ttu-id="eb053-130">MyGet (veya NuGet-as-a-service)</span><span class="sxs-lookup"><span data-stu-id="eb053-130">MyGet (or NuGet-as-a-service)</span></span>](http://www.myget.org/)
- [<span data-ttu-id="eb053-131">NuGet Paket Explorer</span><span class="sxs-lookup"><span data-stu-id="eb053-131">NuGet Package Explorer</span></span>](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)
- [<span data-ttu-id="eb053-132">NuGet Sunucusu</span><span class="sxs-lookup"><span data-stu-id="eb053-132">NuGet Server</span></span>](http://nugetserver.net/)
- [<span data-ttu-id="eb053-133">Ahtapot Konuşlandırma</span><span class="sxs-lookup"><span data-stu-id="eb053-133">OctopusDeploy</span></span>](https://octopus.com/)
- [<span data-ttu-id="eb053-134">Paket</span><span class="sxs-lookup"><span data-stu-id="eb053-134">Paket</span></span>](https://fsprojects.github.io/Paket/)
- [<span data-ttu-id="eb053-135">ProGet (Inedo)</span><span class="sxs-lookup"><span data-stu-id="eb053-135">ProGet (Inedo)</span></span>](http://inedo.com/proget)
- [<span data-ttu-id="eb053-136">scriptcs</span><span class="sxs-lookup"><span data-stu-id="eb053-136">scriptcs</span></span>](http://scriptcs.net/)
- [<span data-ttu-id="eb053-137">Sharpdevelop</span><span class="sxs-lookup"><span data-stu-id="eb053-137">SharpDevelop</span></span>](http://community.sharpdevelop.net/blogs/mattward/archive/2011/01/23/NuGetSupportInSharpDevelop.aspx)
- [<span data-ttu-id="eb053-138">Sonatype Nexus</span><span class="sxs-lookup"><span data-stu-id="eb053-138">Sonatype Nexus</span></span>](http://www.sonatype.com/nexus-repository-sonatype)
- [<span data-ttu-id="eb053-139">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="eb053-139">SymbolSource</span></span>](http://www.symbolsource.org/Public)
- [<span data-ttu-id="eb053-140">Xamarin ve MonoDevelop</span><span class="sxs-lookup"><span data-stu-id="eb053-140">Xamarin and MonoDevelop</span></span>](https://github.com/mrward/monodevelop-nuget-addin)

## <a name="other-nuget-based-utilities"></a><span data-ttu-id="eb053-141">Diğer NuGet tabanlı yardımcı programlar</span><span class="sxs-lookup"><span data-stu-id="eb053-141">Other NuGet-based utilities</span></span>

<span data-ttu-id="eb053-142">Bunlar NuGet üzerine inşa edilmiş araçlar ve yardımcı programlar:</span><span class="sxs-lookup"><span data-stu-id="eb053-142">These are tools and utilities built on NuGet:</span></span>

- <span data-ttu-id="eb053-143">[Glimpse Uzantıları](http://getglimpse.com/Packages) (eklentiler paketlerdir)</span><span class="sxs-lookup"><span data-stu-id="eb053-143">[Glimpse Extensions](http://getglimpse.com/Packages) (plug-ins are packages)</span></span>
- [<span data-ttu-id="eb053-144">NuGetMustHaves.com</span><span class="sxs-lookup"><span data-stu-id="eb053-144">NuGetMustHaves.com</span></span>](http://nugetmusthaves.com/)
- <span data-ttu-id="eb053-145">[Orchard](http://www.orchardproject.net/) (CMS modülleri, Orchard Galerisi'nde barındırılan v1 NuGet yemlerinden getirilir)</span><span class="sxs-lookup"><span data-stu-id="eb053-145">[Orchard](http://www.orchardproject.net/) (CMS modules are fetched from a v1 NuGet feed hosted in the Orchard Gallery)</span></span>
- [<span data-ttu-id="eb053-146">NuGet Server'ın Java uygulaması</span><span class="sxs-lookup"><span data-stu-id="eb053-146">Java implementation of NuGet Server</span></span>](http://jonnyzzz.com/blog/2012/03/07/nuget-server-in-pure-java/)
- <span data-ttu-id="eb053-147">[NuGetLatest](https://twitter.com/NuGetLatest) (Twitter bot tweeting yeni paket yayınlar)</span><span class="sxs-lookup"><span data-stu-id="eb053-147">[NuGetLatest](https://twitter.com/NuGetLatest) (Twitter bot tweeting new package publications)</span></span>
- <span data-ttu-id="eb053-148">[DefinitelyTyped](http://definitelytyped.org/) ([Otomatik](https://github.com/DefinitelyTyped/NugetAutomation/) TypeScript Tip [Tanımları NuGet için yayınlandı](http://www.nuget.org/packages?q=DefinitelyTyped))</span><span class="sxs-lookup"><span data-stu-id="eb053-148">[DefinitelyTyped](http://definitelytyped.org/) ([Automatic](https://github.com/DefinitelyTyped/NugetAutomation/) TypeScript Type [Definitions published to NuGet](http://www.nuget.org/packages?q=DefinitelyTyped))</span></span>

## <a name="training-materials-and-references"></a><span data-ttu-id="eb053-149">Eğitim materyalleri ve referanslar</span><span class="sxs-lookup"><span data-stu-id="eb053-149">Training materials and references</span></span>

<span data-ttu-id="eb053-150">Yeni bir araç veya teknoloji kullanarak genellikle bir öğrenme eğrisi ile birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="eb053-150">Using a new tool or technology usually comes with a learning curve.</span></span> <span data-ttu-id="eb053-151">Neyse ki sizin için, NuGet tüm dik öğrenme eğrisi vardır!</span><span class="sxs-lookup"><span data-stu-id="eb053-151">Luckily for you, NuGet has no steep learning curve it all!</span></span> <span data-ttu-id="eb053-152">Aslında, herkes hızlı bir şekilde [paketleri tüketen alabilirsiniz.](../quickstart/use-a-package.md)</span><span class="sxs-lookup"><span data-stu-id="eb053-152">In fact, anyone can [get started consuming packages](../quickstart/use-a-package.md) quickly.</span></span>

<span data-ttu-id="eb053-153">Bununla birlikte, paketlerin ve özellikle iyi paketlerin yazılmasının yanı sıra, nuget'i otomatik oluşturma ve dağıtım süreçlerinde benimsemek, aşağıdaki kaynaklarla biraz daha zaman geçirmeyi gerektirir:</span><span class="sxs-lookup"><span data-stu-id="eb053-153">That said, authoring packages–and especially good packages–along with  embracing NuGet in automated build and deployment processes, requires spending a little more time with the following resources:</span></span>

- [<span data-ttu-id="eb053-154">NuGet Blog</span><span class="sxs-lookup"><span data-stu-id="eb053-154">NuGet Blog</span></span>](http://blog.nuget.org/)
- [<span data-ttu-id="eb053-155">Twitter'da NuGet ekibi,@nuget</span><span class="sxs-lookup"><span data-stu-id="eb053-155">NuGet team on Twitter, @nuget</span></span>](http://twitter.com/nuget)
- <span data-ttu-id="eb053-156">Kitaplar:</span><span class="sxs-lookup"><span data-stu-id="eb053-156">Books:</span></span>
  - [<span data-ttu-id="eb053-157">Apress Pro NuGet</span><span class="sxs-lookup"><span data-stu-id="eb053-157">Apress Pro NuGet</span></span>](http://bit.ly/ProNuGet)
  - [<span data-ttu-id="eb053-158">NuGet 2 Temel</span><span class="sxs-lookup"><span data-stu-id="eb053-158">NuGet 2 Essentials</span></span>](http://www.amazon.com/NuGet-2-Essentials-Damir-Arh-ebook/dp/B00GTQD5M4)

## <a name="documentation-for-individual-packages"></a><span data-ttu-id="eb053-159">Bireysel paketler için belgeler</span><span class="sxs-lookup"><span data-stu-id="eb053-159">Documentation for individual packages</span></span>

<span data-ttu-id="eb053-160">[NuDoq,](http://nudoq.org) NuGet paketleri için basit erişim, güncellemeler ve belgeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="eb053-160">[NuDoq](http://nudoq.org) provides straightforward access and updates and documentation for NuGet packages.</span></span>

<span data-ttu-id="eb053-161">NuDoq düzenli olarak en son paket güncelleştirmeleri için nuget.org galeri sunucusunu yoklar, kitaplık belge dosyalarını boşaltır ve işler ve siteyi buna göre güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="eb053-161">NuDoq regularly polls the nuget.org gallery server for the latest package updates, unpacks and processes the library documentation files, and updates the site accordingly.</span></span>

## <a name="adding-your-project"></a><span data-ttu-id="eb053-162">Projenizi ekleme</span><span class="sxs-lookup"><span data-stu-id="eb053-162">Adding your project</span></span>

<span data-ttu-id="eb053-163">Bu sayfaya değerli bir ek olacak bir NuGet ekosistem projeniz varsa, lütfen bu sayfaya bir düzenlemesi olan bir çekme isteği gönderin.</span><span class="sxs-lookup"><span data-stu-id="eb053-163">If you have a NuGet ecosystem project that would be a valuable addition to this page, please  submit a pull request with an edit to this page.</span></span>
