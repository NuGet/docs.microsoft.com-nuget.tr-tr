---
title: "NuGet ekosistemine genel bakış | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Kapsamlı kaynaklar NuGet kaynakları, Microsoft olmayan NuGet projeleri, yardımcı programlar ve eğitim malzemelerinizin de dahil olmak üzere NuGet ekosistemindeki."
keywords: "NuGet ekosistemi, Microsoft olmayan NuGet projeleri, NuGet açık kaynak, NuGet yardımcı programlar, NuGet eğitim malzemelerini"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7c1e457c034f239fbea4e75f24851ea38182a294
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/02/2018
---
# <a name="an-overview-of-the-nuget-ecosystem"></a><span data-ttu-id="e997f-104">NuGet ekosistemine genel bakış</span><span class="sxs-lookup"><span data-stu-id="e997f-104">An overview of the NuGet ecosystem</span></span>

<span data-ttu-id="e997f-105">Giriş 2010 olduğuna göre NuGet artırmak ve farklı yönlerini geliştirme süreçleri otomatik hale getirmek için harika bir fırsat sunulan.</span><span class="sxs-lookup"><span data-stu-id="e997f-105">Since it's introduction in 2010, NuGet has presented a great opportunity to improve and automate different aspects of the development processes.</span></span>

<span data-ttu-id="e997f-106">NuGet açık kaynaklı bir izin veren altında olduğundan [Apache v2 lisans](http://choosealicense.com/licenses/apache/), diğer projeler NuGet yararlanabilir ve şirketler ürünlerinin onun için desteği oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="e997f-106">Because NuGet is open source under a permissive [Apache v2 license](http://choosealicense.com/licenses/apache/), other projects can leverage NuGet and companies can build support for it in their products.</span></span> <span data-ttu-id="e997f-107">Açık kaynaklı proje mı Kurumsal uygulama geliştirme, NuGet ve diğer uygulamalar üzerinde ve NuGet geçici yerleşik araçları geniş ekosistemiyle yazılım geliştirme sürecini iyileştirmek için sağlama.</span><span class="sxs-lookup"><span data-stu-id="e997f-107">Whether for open-source projects or enterprise application development, NuGet and other applications built on and around NuGet provide a broad ecosystem of tools for improving your software development process.</span></span>

<span data-ttu-id="e997f-108">Tüm bu projeleri Geliştirici Katkıları nedeniyle yenilik imkanınız olur.</span><span class="sxs-lookup"><span data-stu-id="e997f-108">All of these projects are able to innovate because of developer contributions.</span></span> <span data-ttu-id="e997f-109">Ayrıca NuGet için katkıda yalnızca gibi bu projeler katkısı raporlama kusurları ve geribildirim sağlama, belgeleri yazma ve mümkün olduğunda kod katkıda bulunan yeni özellik fikirleri tarafından olun.</span><span class="sxs-lookup"><span data-stu-id="e997f-109">Just as you contribute to NuGet itself, also make contribution to these projects by reporting defects and new feature ideas, providing feedback, writing documentation, and contributing code where possible.</span></span>

## <a name="net-foundation-projects"></a><span data-ttu-id="e997f-110">.NET foundation projeleri</span><span class="sxs-lookup"><span data-stu-id="e997f-110">.NET Foundation projects</span></span>

<span data-ttu-id="e997f-111">NuGet Microsoft geliştirme platformu için ücretsiz, açık kaynaklı paket yönetim sistemi sağlar.</span><span class="sxs-lookup"><span data-stu-id="e997f-111">NuGet provides a free, open source package management system for the Microsoft development platform.</span></span> <span data-ttu-id="e997f-112">Oluşturan bir hizmetler kümesi olan yanı sıra birkaç istemci araçları oluşur [resmi NuGet galerisinde](http://www.nuget.org).</span><span class="sxs-lookup"><span data-stu-id="e997f-112">It consists of a few client tools as well as the set of services that comprise the [official NuGet Gallery](http://www.nuget.org).</span></span> <span data-ttu-id="e997f-113">Birleştirilmiş, bunlar tarafından yönetilen NuGet proje form [.NET Foundation](http://www.dotnetfoundation.org/).</span><span class="sxs-lookup"><span data-stu-id="e997f-113">Combined, these form the NuGet project which is governed by the [.NET Foundation](http://www.dotnetfoundation.org/).</span></span>

<span data-ttu-id="e997f-114">NuGet kuruluşu, GitHub üzerinde çeşitli depoları içerir.</span><span class="sxs-lookup"><span data-stu-id="e997f-114">The NuGet Organization contains various repositories on GitHub.</span></span> <span data-ttu-id="e997f-115">[https://github.com/Nuget/Home](https://github.com/Nuget/Home) tüm depoları genel bir bakış ve çeşitli NuGet bileşenleri nerede sağlar.</span><span class="sxs-lookup"><span data-stu-id="e997f-115">[https://github.com/Nuget/Home](https://github.com/Nuget/Home) gives an overview of all the repositories and where to find the various NuGet components.</span></span>

## <a name="microsoft-projects"></a><span data-ttu-id="e997f-116">Microsoft projeleri</span><span class="sxs-lookup"><span data-stu-id="e997f-116">Microsoft projects</span></span>

<span data-ttu-id="e997f-117">Microsoft, NuGet geliştirme için yaygın katıldığını.</span><span class="sxs-lookup"><span data-stu-id="e997f-117">Microsoft has contributed extensively to the development of NuGet.</span></span> <span data-ttu-id="e997f-118">Microsoft çalışanlar tarafından bir katkılar de açık kaynaklıdır olan ve (telif hakları dahil olmak üzere) .NET Foundation'a bağışlanır.</span><span class="sxs-lookup"><span data-stu-id="e997f-118">All contributions made by Microsoft employees are also open source and are donated (including copyrights) to the .NET Foundation.</span></span>

## <a name="non-microsoft-projects"></a><span data-ttu-id="e997f-119">Microsoft olmayan projeleri</span><span class="sxs-lookup"><span data-stu-id="e997f-119">Non-Microsoft projects</span></span>

<span data-ttu-id="e997f-120">Diğer birçok kişiler ve şirketler NuGet ekosistemi önemli ölçüde katkıda yaptınız.</span><span class="sxs-lookup"><span data-stu-id="e997f-120">Many other individuals and companies have made significant contributions to the NuGet ecosystem.</span></span> <span data-ttu-id="e997f-121">Burada listelenen her proje, çekirdek NuGet Bileşenler'den farklı bir lisansa sahip olabilir, böylece Lisans Koşulları'nı kullanmadan önce kabul edilebilir olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="e997f-121">Each project listed here may have a different license than the core NuGet components, so confirm that the license terms are acceptable prior to use:</span></span>

- [<span data-ttu-id="e997f-122">AppVeyor CI</span><span class="sxs-lookup"><span data-stu-id="e997f-122">AppVeyor CI</span></span>](https://www.appveyor.com/)
- [<span data-ttu-id="e997f-123">Artifactory</span><span class="sxs-lookup"><span data-stu-id="e997f-123">Artifactory</span></span>](https://www.jfrog.com/artifactory/)
- [<span data-ttu-id="e997f-124">BoxStarter</span><span class="sxs-lookup"><span data-stu-id="e997f-124">BoxStarter</span></span>](http://boxstarter.org/)
- [<span data-ttu-id="e997f-125">Chocolatey</span><span class="sxs-lookup"><span data-stu-id="e997f-125">Chocolatey</span></span>](https://chocolatey.org/)
- [<span data-ttu-id="e997f-126">CoApp</span><span class="sxs-lookup"><span data-stu-id="e997f-126">CoApp</span></span>](http://coapp.org/)
- [<span data-ttu-id="e997f-127">JetBrains ReSharper</span><span class="sxs-lookup"><span data-stu-id="e997f-127">JetBrains ReSharper</span></span>](https://resharper-plugins.jetbrains.com/)
- [<span data-ttu-id="e997f-128">JetBrains TeamCity</span><span class="sxs-lookup"><span data-stu-id="e997f-128">JetBrains TeamCity</span></span>](https://www.jetbrains.com/teamcity/)
- [<span data-ttu-id="e997f-129">Klondike</span><span class="sxs-lookup"><span data-stu-id="e997f-129">Klondike</span></span>](https://github.com/themotleyfool/Klondike)
- [<span data-ttu-id="e997f-130">MinimalNugetServer</span><span class="sxs-lookup"><span data-stu-id="e997f-130">MinimalNugetServer</span></span>](https://github.com/TanukiSharp/MinimalNugetServer)
- [<span data-ttu-id="e997f-131">MyGet (veya hizmet olarak NuGet)</span><span class="sxs-lookup"><span data-stu-id="e997f-131">MyGet (or NuGet-as-a-service)</span></span>](http://www.myget.org/)
- [<span data-ttu-id="e997f-132">NuGet paketi Gezgini</span><span class="sxs-lookup"><span data-stu-id="e997f-132">NuGet Package Explorer</span></span>](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)
- [<span data-ttu-id="e997f-133">NuGet Server</span><span class="sxs-lookup"><span data-stu-id="e997f-133">NuGet Server</span></span>](http://nugetserver.net/)
- [<span data-ttu-id="e997f-134">OctopusDeploy</span><span class="sxs-lookup"><span data-stu-id="e997f-134">OctopusDeploy</span></span>](https://octopus.com/)
- [<span data-ttu-id="e997f-135">Paket</span><span class="sxs-lookup"><span data-stu-id="e997f-135">Paket</span></span>](https://fsprojects.github.io/Paket/)
- [<span data-ttu-id="e997f-136">ProGet (Inedo)</span><span class="sxs-lookup"><span data-stu-id="e997f-136">ProGet (Inedo)</span></span>](http://inedo.com/proget)
- [<span data-ttu-id="e997f-137">scriptcs</span><span class="sxs-lookup"><span data-stu-id="e997f-137">scriptcs</span></span>](http://scriptcs.net/)
- [<span data-ttu-id="e997f-138">SharpDevelop</span><span class="sxs-lookup"><span data-stu-id="e997f-138">SharpDevelop</span></span>](http://community.sharpdevelop.net/blogs/mattward/archive/2011/01/23/NuGetSupportInSharpDevelop.aspx)
- [<span data-ttu-id="e997f-139">Sonatype Nexus</span><span class="sxs-lookup"><span data-stu-id="e997f-139">Sonatype Nexus</span></span>](http://www.sonatype.com/nexus-repository-sonatype)
- [<span data-ttu-id="e997f-140">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="e997f-140">SymbolSource</span></span>](http://www.symbolsource.org/Public)
- [<span data-ttu-id="e997f-141">Xamarin ve MonoDevelop</span><span class="sxs-lookup"><span data-stu-id="e997f-141">Xamarin and MonoDevelop</span></span>](https://github.com/mrward/monodevelop-nuget-addin)

## <a name="other-nuget-based-utilities"></a><span data-ttu-id="e997f-142">Diğer NuGet tabanlı yardımcı programları</span><span class="sxs-lookup"><span data-stu-id="e997f-142">Other NuGet-based utilities</span></span>

<span data-ttu-id="e997f-143">Bu araçlar ve yardımcı programlar NuGet üzerinde oluşturulmuş şunlardır:</span><span class="sxs-lookup"><span data-stu-id="e997f-143">These are tools and utilities built on NuGet:</span></span>

- <span data-ttu-id="e997f-144">[Glimpse'in uzantıları](http://getglimpse.com/Packages) (eklentileri olan paketleri)</span><span class="sxs-lookup"><span data-stu-id="e997f-144">[Glimpse Extensions](http://getglimpse.com/Packages) (plug-ins are packages)</span></span>
- [<span data-ttu-id="e997f-145">NuGetMustHaves.com</span><span class="sxs-lookup"><span data-stu-id="e997f-145">NuGetMustHaves.com</span></span>](http://nugetmusthaves.com/)
- <span data-ttu-id="e997f-146">[Orchard](http://www.orchardproject.net/) (CMS modülleri getirilen Orchard Galerisi'nde barındırılan NuGet akışı bir v1'den)</span><span class="sxs-lookup"><span data-stu-id="e997f-146">[Orchard](http://www.orchardproject.net/) (CMS modules are fetched from a v1 NuGet feed hosted in the Orchard Gallery)</span></span>
- [<span data-ttu-id="e997f-147">NuGet sunucu Java uygulaması</span><span class="sxs-lookup"><span data-stu-id="e997f-147">Java implementation of NuGet Server</span></span>](http://jonnyzzz.com/blog/2012/03/07/nuget-server-in-pure-java/)
- <span data-ttu-id="e997f-148">[NuGetLatest](https://twitter.com/NuGetLatest) (yeni TWİTLEME bot yayınlar paketi Twitter)</span><span class="sxs-lookup"><span data-stu-id="e997f-148">[NuGetLatest](https://twitter.com/NuGetLatest) (Twitter bot tweeting new package publications)</span></span>
- <span data-ttu-id="e997f-149">[DefinitelyTyped](http://definitelytyped.org/) ([otomatik](https://github.com/DefinitelyTyped/NugetAutomation/) TypeScript türü [tanımları için NuGet yayımlanan](http://www.nuget.org/packages?q=DefinitelyTyped))</span><span class="sxs-lookup"><span data-stu-id="e997f-149">[DefinitelyTyped](http://definitelytyped.org/) ([Automatic](https://github.com/DefinitelyTyped/NugetAutomation/) TypeScript Type [Definitions published to NuGet](http://www.nuget.org/packages?q=DefinitelyTyped))</span></span>

## <a name="training-materials-and-references"></a><span data-ttu-id="e997f-150">Eğitim malzemelerini ve başvurular</span><span class="sxs-lookup"><span data-stu-id="e997f-150">Training materials and references</span></span>

<span data-ttu-id="e997f-151">Genellikle bir yeni aracın veya teknoloji kullanarak bir öğrenme eğrisi ile birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="e997f-151">Using a new tool or technology usually comes with a learning curve.</span></span> <span data-ttu-id="e997f-152">Luckily sizin için NuGet tüm eğri hiçbir hızı yüksek öğrenme var!</span><span class="sxs-lookup"><span data-stu-id="e997f-152">Luckily for you, NuGet has no steep learning curve it all!</span></span> <span data-ttu-id="e997f-153">Aslında, herkes için [paketleri kullanma başlamak](../quickstart/use-a-package.md) hızlı bir şekilde.</span><span class="sxs-lookup"><span data-stu-id="e997f-153">In fact, anyone can [get started consuming packages](../quickstart/use-a-package.md) quickly.</span></span>

<span data-ttu-id="e997f-154">Başka bir deyişle, paketleri yazma – ve özellikle iyi paketleri – otomatik derleme ve dağıtım işlemleri NuGet benimsemenin ile birlikte, aşağıdaki kaynaklarla biraz daha uzun harcama gerektirir:</span><span class="sxs-lookup"><span data-stu-id="e997f-154">That said, authoring packages–and especially good packages–along with  embracing NuGet in automated build and deployment processes, requires spending a little more time with the following resources:</span></span>

- [<span data-ttu-id="e997f-155">NuGet Blog</span><span class="sxs-lookup"><span data-stu-id="e997f-155">NuGet Blog</span></span>](http://blog.nuget.org/)
- [<span data-ttu-id="e997f-156">NuGet takım Twitter'da@nuget</span><span class="sxs-lookup"><span data-stu-id="e997f-156">NuGet team on Twitter, @nuget</span></span>](http://twitter.com/nuget)
- <span data-ttu-id="e997f-157">Kitaplar:</span><span class="sxs-lookup"><span data-stu-id="e997f-157">Books:</span></span>
  - [<span data-ttu-id="e997f-158">Apress Pro NuGet</span><span class="sxs-lookup"><span data-stu-id="e997f-158">Apress Pro NuGet</span></span>](http://bit.ly/ProNuGet)
  - [<span data-ttu-id="e997f-159">NuGet 2 temelleri</span><span class="sxs-lookup"><span data-stu-id="e997f-159">NuGet 2 Essentials</span></span>](http://www.amazon.com/NuGet-2-Essentials-Damir-Arh-ebook/dp/B00GTQD5M4)

## <a name="documentation-for-individual-packages"></a><span data-ttu-id="e997f-160">Tek paketler için belgeler</span><span class="sxs-lookup"><span data-stu-id="e997f-160">Documentation for individual packages</span></span>

<span data-ttu-id="e997f-161">[NuDoq](http://nudoq.org) kolay erişim, güncelleştirmeleri ve NuGet paketleri için belgeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="e997f-161">[NuDoq](http://nudoq.org) provides straightforward access and updates and documentation for NuGet packages.</span></span>

<span data-ttu-id="e997f-162">NuDoq düzenli olarak nuget.org galeri sunucuyu en son paket güncelleştirmelerini tarar, ayıklar ve kitaplığı belgeleri dosyaları işler ve site uygun şekilde güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="e997f-162">NuDoq regularly polls the nuget.org gallery server for the latest package updates, unpacks and processes the library documentation files, and updates the site accordingly.</span></span>

## <a name="adding-your-project"></a><span data-ttu-id="e997f-163">Projenize ekleme</span><span class="sxs-lookup"><span data-stu-id="e997f-163">Adding your project</span></span>

<span data-ttu-id="e997f-164">Bu sayfaya değerli bir toplama olacak NuGet ekosistemi proje varsa, lütfen bu sayfaya bir düzen içeren bir çekme isteği gönderin.</span><span class="sxs-lookup"><span data-stu-id="e997f-164">If you have a NuGet ecosystem project that would be a valuable addition to this page, please  submit a pull request with an edit to this page.</span></span>
