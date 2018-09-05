---
title: NuGet ekosistemine genel bakış
description: NuGet kaynağı, Microsoft NuGet projeler, yardımcı programlar ve eğitim malzemeleri NuGet ekosisteminde kapsamlı kaynaklar.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 31243076f36f6ff274c4377c1773ea59dda8c834
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548150"
---
# <a name="an-overview-of-the-nuget-ecosystem"></a><span data-ttu-id="0c1fc-103">NuGet ekosistemine genel bakış</span><span class="sxs-lookup"><span data-stu-id="0c1fc-103">An overview of the NuGet ecosystem</span></span>

<span data-ttu-id="0c1fc-104">NuGet, 2010'daki giriş olduğundan, geliştirmek ve farklı yönlerini geliştirme süreçleri otomatik hale getirmek için harika bir fırsat sunulan.</span><span class="sxs-lookup"><span data-stu-id="0c1fc-104">Since it's introduction in 2010, NuGet has presented a great opportunity to improve and automate different aspects of the development processes.</span></span>

<span data-ttu-id="0c1fc-105">NuGet, açık kaynak bir esnek altında olduğundan [Apache v2 lisans](http://choosealicense.com/licenses/apache/), diğer projeleri NuGet yararlanabilir ve şirketler ürünlerinin desteği de oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0c1fc-105">Because NuGet is open source under a permissive [Apache v2 license](http://choosealicense.com/licenses/apache/), other projects can leverage NuGet and companies can build support for it in their products.</span></span> <span data-ttu-id="0c1fc-106">Açık kaynaklı projelerin mı Kurumsal uygulama geliştirme, NuGet ve diğer uygulamalar üzerinde ve NuGet geçici olarak oluşturulmuş geniş bir ekosistemi araçların yazılım geliştirme sürecini iyileştirmek için sağlayın.</span><span class="sxs-lookup"><span data-stu-id="0c1fc-106">Whether for open-source projects or enterprise application development, NuGet and other applications built on and around NuGet provide a broad ecosystem of tools for improving your software development process.</span></span>

<span data-ttu-id="0c1fc-107">Bu projelerin hepsine Geliştirici Katkıları nedeniyle yenilik.</span><span class="sxs-lookup"><span data-stu-id="0c1fc-107">All of these projects are able to innovate because of developer contributions.</span></span> <span data-ttu-id="0c1fc-108">Ayrıca NuGet için yalnızca katkıda bulunuyorsanız katkı bu projeler için raporlama hataları ve geri bildirim sağlama, belgeleri yazma ve mümkün olduğunda kod katkısı yeni özellik fikirleri olun.</span><span class="sxs-lookup"><span data-stu-id="0c1fc-108">Just as you contribute to NuGet itself, also make contribution to these projects by reporting defects and new feature ideas, providing feedback, writing documentation, and contributing code where possible.</span></span>

## <a name="net-foundation-projects"></a><span data-ttu-id="0c1fc-109">.NET foundation projeleri</span><span class="sxs-lookup"><span data-stu-id="0c1fc-109">.NET Foundation projects</span></span>

<span data-ttu-id="0c1fc-110">NuGet, ücretsiz, açık kaynaklı paket yönetim sistemi için Microsoft geliştirme platformu sağlar.</span><span class="sxs-lookup"><span data-stu-id="0c1fc-110">NuGet provides a free, open source package management system for the Microsoft development platform.</span></span> <span data-ttu-id="0c1fc-111">Kümesini oluşturan Hizmetleri yanı sıra birkaç istemci araçları oluşur [resmi NuGet Galerisi](http://www.nuget.org).</span><span class="sxs-lookup"><span data-stu-id="0c1fc-111">It consists of a few client tools as well as the set of services that comprise the [official NuGet Gallery](http://www.nuget.org).</span></span> <span data-ttu-id="0c1fc-112">Birlikte kullanıldığında bu tabidir NuGet proje formu [.NET Foundation](http://www.dotnetfoundation.org/).</span><span class="sxs-lookup"><span data-stu-id="0c1fc-112">Combined, these form the NuGet project which is governed by the [.NET Foundation](http://www.dotnetfoundation.org/).</span></span>

<span data-ttu-id="0c1fc-113">NuGet kuruluş GitHub çeşitli depolarda içerir.</span><span class="sxs-lookup"><span data-stu-id="0c1fc-113">The NuGet Organization contains various repositories on GitHub.</span></span> <span data-ttu-id="0c1fc-114">[https://github.com/Nuget/Home](https://github.com/Nuget/Home) Tüm depolar genel bir bakış ve çeşitli bileşenleri NuGet nerede bulacağını sağlar.</span><span class="sxs-lookup"><span data-stu-id="0c1fc-114">[https://github.com/Nuget/Home](https://github.com/Nuget/Home) gives an overview of all the repositories and where to find the various NuGet components.</span></span>

## <a name="microsoft-projects"></a><span data-ttu-id="0c1fc-115">Microsoft projeleri</span><span class="sxs-lookup"><span data-stu-id="0c1fc-115">Microsoft projects</span></span>

<span data-ttu-id="0c1fc-116">Microsoft, NuGet geliştirilmesini kapsamlı bir şekilde katkılarıyla.</span><span class="sxs-lookup"><span data-stu-id="0c1fc-116">Microsoft has contributed extensively to the development of NuGet.</span></span> <span data-ttu-id="0c1fc-117">Microsoft çalışanları tarafından yapılan tüm katkılar de açık kaynak olan ve (telif hakkı) için .NET Foundation üzerinde Bağış.</span><span class="sxs-lookup"><span data-stu-id="0c1fc-117">All contributions made by Microsoft employees are also open source and are donated (including copyrights) to the .NET Foundation.</span></span>

## <a name="non-microsoft-projects"></a><span data-ttu-id="0c1fc-118">Microsoft olmayan projeler</span><span class="sxs-lookup"><span data-stu-id="0c1fc-118">Non-Microsoft projects</span></span>

<span data-ttu-id="0c1fc-119">Diğer kişiler ve şirketlerin birçok önemli katkılar NuGet ekosistemine yapıldı.</span><span class="sxs-lookup"><span data-stu-id="0c1fc-119">Many other individuals and companies have made significant contributions to the NuGet ecosystem.</span></span> <span data-ttu-id="0c1fc-120">Burada listelenen her bir proje çekirdek NuGet bileşenlerini değerinden farklı bir lisansa sahip, bu nedenle Lisans Koşulları'nı kullanmadan önce kabul edilebilir olduğunu onaylayın:</span><span class="sxs-lookup"><span data-stu-id="0c1fc-120">Each project listed here may have a different license than the core NuGet components, so confirm that the license terms are acceptable prior to use:</span></span>

- [<span data-ttu-id="0c1fc-121">AppVeyor CI</span><span class="sxs-lookup"><span data-stu-id="0c1fc-121">AppVeyor CI</span></span>](https://www.appveyor.com/)
- [<span data-ttu-id="0c1fc-122">Artifactory</span><span class="sxs-lookup"><span data-stu-id="0c1fc-122">Artifactory</span></span>](https://www.jfrog.com/artifactory/)
- [<span data-ttu-id="0c1fc-123">BoxStarter</span><span class="sxs-lookup"><span data-stu-id="0c1fc-123">BoxStarter</span></span>](http://boxstarter.org/)
- [<span data-ttu-id="0c1fc-124">Chocolatey</span><span class="sxs-lookup"><span data-stu-id="0c1fc-124">Chocolatey</span></span>](https://chocolatey.org/)
- [<span data-ttu-id="0c1fc-125">CoApp</span><span class="sxs-lookup"><span data-stu-id="0c1fc-125">CoApp</span></span>](http://coapp.org/)
- [<span data-ttu-id="0c1fc-126">JetBrains ReSharper</span><span class="sxs-lookup"><span data-stu-id="0c1fc-126">JetBrains ReSharper</span></span>](https://resharper-plugins.jetbrains.com/)
- [<span data-ttu-id="0c1fc-127">JetBrains TeamCity</span><span class="sxs-lookup"><span data-stu-id="0c1fc-127">JetBrains TeamCity</span></span>](https://www.jetbrains.com/teamcity/)
- [<span data-ttu-id="0c1fc-128">Klondike</span><span class="sxs-lookup"><span data-stu-id="0c1fc-128">Klondike</span></span>](https://github.com/themotleyfool/Klondike)
- [<span data-ttu-id="0c1fc-129">MinimalNugetServer</span><span class="sxs-lookup"><span data-stu-id="0c1fc-129">MinimalNugetServer</span></span>](https://github.com/TanukiSharp/MinimalNugetServer)
- [<span data-ttu-id="0c1fc-130">MyGet (veya hizmet olarak NuGet)</span><span class="sxs-lookup"><span data-stu-id="0c1fc-130">MyGet (or NuGet-as-a-service)</span></span>](http://www.myget.org/)
- [<span data-ttu-id="0c1fc-131">NuGet paket Gezgini</span><span class="sxs-lookup"><span data-stu-id="0c1fc-131">NuGet Package Explorer</span></span>](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)
- [<span data-ttu-id="0c1fc-132">NuGet sunucusu</span><span class="sxs-lookup"><span data-stu-id="0c1fc-132">NuGet Server</span></span>](http://nugetserver.net/)
- [<span data-ttu-id="0c1fc-133">OctopusDeploy</span><span class="sxs-lookup"><span data-stu-id="0c1fc-133">OctopusDeploy</span></span>](https://octopus.com/)
- [<span data-ttu-id="0c1fc-134">Paket</span><span class="sxs-lookup"><span data-stu-id="0c1fc-134">Paket</span></span>](https://fsprojects.github.io/Paket/)
- [<span data-ttu-id="0c1fc-135">ProGet (Inedo)</span><span class="sxs-lookup"><span data-stu-id="0c1fc-135">ProGet (Inedo)</span></span>](http://inedo.com/proget)
- [<span data-ttu-id="0c1fc-136">scriptcs</span><span class="sxs-lookup"><span data-stu-id="0c1fc-136">scriptcs</span></span>](http://scriptcs.net/)
- [<span data-ttu-id="0c1fc-137">SharpDevelop</span><span class="sxs-lookup"><span data-stu-id="0c1fc-137">SharpDevelop</span></span>](http://community.sharpdevelop.net/blogs/mattward/archive/2011/01/23/NuGetSupportInSharpDevelop.aspx)
- [<span data-ttu-id="0c1fc-138">Sonatype Nexus</span><span class="sxs-lookup"><span data-stu-id="0c1fc-138">Sonatype Nexus</span></span>](http://www.sonatype.com/nexus-repository-sonatype)
- [<span data-ttu-id="0c1fc-139">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="0c1fc-139">SymbolSource</span></span>](http://www.symbolsource.org/Public)
- [<span data-ttu-id="0c1fc-140">Xamarin ve MonoDevelop</span><span class="sxs-lookup"><span data-stu-id="0c1fc-140">Xamarin and MonoDevelop</span></span>](https://github.com/mrward/monodevelop-nuget-addin)

## <a name="other-nuget-based-utilities"></a><span data-ttu-id="0c1fc-141">NuGet tabanlı diğer yardımcı programları</span><span class="sxs-lookup"><span data-stu-id="0c1fc-141">Other NuGet-based utilities</span></span>

<span data-ttu-id="0c1fc-142">Araçlar ve yardımcı programlar NuGet üzerinde oluşturulmuş şunlardır:</span><span class="sxs-lookup"><span data-stu-id="0c1fc-142">These are tools and utilities built on NuGet:</span></span>

- <span data-ttu-id="0c1fc-143">[Glimpse uzantıları](http://getglimpse.com/Packages) (eklentileri olan paketleri)</span><span class="sxs-lookup"><span data-stu-id="0c1fc-143">[Glimpse Extensions](http://getglimpse.com/Packages) (plug-ins are packages)</span></span>
- [<span data-ttu-id="0c1fc-144">NuGetMustHaves.com</span><span class="sxs-lookup"><span data-stu-id="0c1fc-144">NuGetMustHaves.com</span></span>](http://nugetmusthaves.com/)
- <span data-ttu-id="0c1fc-145">[Orchard](http://www.orchardproject.net/) (CMS modülleri getirilen Orchard galeride barındırılan NuGet akışı bir v1'den)</span><span class="sxs-lookup"><span data-stu-id="0c1fc-145">[Orchard](http://www.orchardproject.net/) (CMS modules are fetched from a v1 NuGet feed hosted in the Orchard Gallery)</span></span>
- [<span data-ttu-id="0c1fc-146">Java uygulaması NuGet sunucusu</span><span class="sxs-lookup"><span data-stu-id="0c1fc-146">Java implementation of NuGet Server</span></span>](http://jonnyzzz.com/blog/2012/03/07/nuget-server-in-pure-java/)
- <span data-ttu-id="0c1fc-147">[NuGetLatest](https://twitter.com/NuGetLatest) (Twitter yeni TWİTLEME bot yayınlar paketi)</span><span class="sxs-lookup"><span data-stu-id="0c1fc-147">[NuGetLatest](https://twitter.com/NuGetLatest) (Twitter bot tweeting new package publications)</span></span>
- <span data-ttu-id="0c1fc-148">[DefinitelyTyped](http://definitelytyped.org/) ([otomatik](https://github.com/DefinitelyTyped/NugetAutomation/) TypeScript türü [tanımları için NuGet yayımlanan](http://www.nuget.org/packages?q=DefinitelyTyped))</span><span class="sxs-lookup"><span data-stu-id="0c1fc-148">[DefinitelyTyped](http://definitelytyped.org/) ([Automatic](https://github.com/DefinitelyTyped/NugetAutomation/) TypeScript Type [Definitions published to NuGet](http://www.nuget.org/packages?q=DefinitelyTyped))</span></span>

## <a name="training-materials-and-references"></a><span data-ttu-id="0c1fc-149">Eğitim malzemeleri ve başvuruları</span><span class="sxs-lookup"><span data-stu-id="0c1fc-149">Training materials and references</span></span>

<span data-ttu-id="0c1fc-150">Genellikle bir yeni aracın veya teknoloji kullanarak bir öğrenme eğrisi ile birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="0c1fc-150">Using a new tool or technology usually comes with a learning curve.</span></span> <span data-ttu-id="0c1fc-151">Neyse ki, NuGet tüm eğri hiçbir seyretmez öğrenme var!</span><span class="sxs-lookup"><span data-stu-id="0c1fc-151">Luckily for you, NuGet has no steep learning curve it all!</span></span> <span data-ttu-id="0c1fc-152">Aslında, herkes için [paketleri tüketen başlama](../quickstart/use-a-package.md) hızlı bir şekilde.</span><span class="sxs-lookup"><span data-stu-id="0c1fc-152">In fact, anyone can [get started consuming packages](../quickstart/use-a-package.md) quickly.</span></span>

<span data-ttu-id="0c1fc-153">Başka bir deyişle, paketleri yazma – ve özellikle de iyi paketler – otomatik derleme ve dağıtım işlemleri NuGet benimsemenin ile birlikte, aşağıdaki kaynaklarla biraz daha fazla zaman harcadığı gerektirir:</span><span class="sxs-lookup"><span data-stu-id="0c1fc-153">That said, authoring packages–and especially good packages–along with  embracing NuGet in automated build and deployment processes, requires spending a little more time with the following resources:</span></span>

- [<span data-ttu-id="0c1fc-154">NuGet blogu</span><span class="sxs-lookup"><span data-stu-id="0c1fc-154">NuGet Blog</span></span>](http://blog.nuget.org/)
- [<span data-ttu-id="0c1fc-155">NuGet takım Twitter'da @nuget</span><span class="sxs-lookup"><span data-stu-id="0c1fc-155">NuGet team on Twitter, @nuget</span></span>](http://twitter.com/nuget)
- <span data-ttu-id="0c1fc-156">Kitap:</span><span class="sxs-lookup"><span data-stu-id="0c1fc-156">Books:</span></span>
  - [<span data-ttu-id="0c1fc-157">Apress Pro NuGet</span><span class="sxs-lookup"><span data-stu-id="0c1fc-157">Apress Pro NuGet</span></span>](http://bit.ly/ProNuGet)
  - [<span data-ttu-id="0c1fc-158">NuGet 2 temel bileşenleri</span><span class="sxs-lookup"><span data-stu-id="0c1fc-158">NuGet 2 Essentials</span></span>](http://www.amazon.com/NuGet-2-Essentials-Damir-Arh-ebook/dp/B00GTQD5M4)

## <a name="documentation-for-individual-packages"></a><span data-ttu-id="0c1fc-159">Tek paketler için belgeleri</span><span class="sxs-lookup"><span data-stu-id="0c1fc-159">Documentation for individual packages</span></span>

<span data-ttu-id="0c1fc-160">[NuDoq](http://nudoq.org) kolay erişim ve güncelleştirmeler ve NuGet paketleri için belgeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="0c1fc-160">[NuDoq](http://nudoq.org) provides straightforward access and updates and documentation for NuGet packages.</span></span>

<span data-ttu-id="0c1fc-161">NuDoq düzenli olarak nuget.org galeri sunucuyu en son paket güncelleştirmeleri tarar, ayıklar ve kitaplık belge dosyaları işler ve site uygun şekilde güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="0c1fc-161">NuDoq regularly polls the nuget.org gallery server for the latest package updates, unpacks and processes the library documentation files, and updates the site accordingly.</span></span>

## <a name="adding-your-project"></a><span data-ttu-id="0c1fc-162">Projenize ekleme</span><span class="sxs-lookup"><span data-stu-id="0c1fc-162">Adding your project</span></span>

<span data-ttu-id="0c1fc-163">Bu sayfaya değerli bir toplama olabilecek bir NuGet ekosistemi projeniz varsa, lütfen bu sayfaya bir düzenleme ile bir çekme isteği gönderin.</span><span class="sxs-lookup"><span data-stu-id="0c1fc-163">If you have a NuGet ecosystem project that would be a valuable addition to this page, please  submit a pull request with an edit to this page.</span></span>
