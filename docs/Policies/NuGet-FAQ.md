---
title: "Sık sorulan-sorular NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 199a915d-9595-4ae2-a1fb-b15da6d7735a
description: "Ortak sorular ve yanıtlar NuGet komut satırında ve Visual Studio kullanarak ve NuGet Galerisi ile çalışmak için."
keywords: "NuGet soru- cevap, sorular ve yanıtlar, ortak sorunları, NuGet sürümleri, sürüm paketi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 44636a3ab8a3f7aaf96e52aa67d568d7ef381549
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-frequently-asked-questions"></a><span data-ttu-id="d1c24-104">NuGet sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="d1c24-104">NuGet frequently-asked questions</span></span>

<span data-ttu-id="d1c24-105">Bu konuda:</span><span class="sxs-lookup"><span data-stu-id="d1c24-105">In this topic:</span></span>

- [<span data-ttu-id="d1c24-106">Başlarken</span><span class="sxs-lookup"><span data-stu-id="d1c24-106">Getting started</span></span>](#getting-started)
- [<span data-ttu-id="d1c24-107">Visual Studio'da NuGet</span><span class="sxs-lookup"><span data-stu-id="d1c24-107">NuGet in Visual Studio</span></span>](#nuget-in-visual-studio)
- [<span data-ttu-id="d1c24-108">NuGet komut satırı</span><span class="sxs-lookup"><span data-stu-id="d1c24-108">NuGet command line</span></span>](#nuget-command-line)
- [<span data-ttu-id="d1c24-109">NuGet Paket Yöneticisi Konsolu</span><span class="sxs-lookup"><span data-stu-id="d1c24-109">NuGet Package Manager Console</span></span>](#nuget-package-manager-console)
- [<span data-ttu-id="d1c24-110">Oluşturma ve paketleri yayımlama</span><span class="sxs-lookup"><span data-stu-id="d1c24-110">Creating and publishing packages</span></span>](#creating-and-publishing-packages)
- [<span data-ttu-id="d1c24-111">Paketleri ile çalışma</span><span class="sxs-lookup"><span data-stu-id="d1c24-111">Working with packages</span></span>](#working-with-packages)
- [<span data-ttu-id="d1c24-112">Nuget.org paketlerini yönetme</span><span class="sxs-lookup"><span data-stu-id="d1c24-112">Managing packages on nuget.org</span></span>](#managing-packages-on-nugetorg)
- [<span data-ttu-id="d1c24-113">nuget.org erişilebilir değil</span><span class="sxs-lookup"><span data-stu-id="d1c24-113">nuget.org not accessible</span></span>](#nugetorg-not-accessible)

## <a name="getting-started"></a><span data-ttu-id="d1c24-114">Başlarken</span><span class="sxs-lookup"><span data-stu-id="d1c24-114">Getting started</span></span>

<span data-ttu-id="d1c24-115">**NuGet çalıştırmak için gereken nedir?**</span><span class="sxs-lookup"><span data-stu-id="d1c24-115">**What is required to run NuGet?**</span></span>

<span data-ttu-id="d1c24-116">Kullanıcı Arabirimi ve komut satırı araçları geçici tüm bilgileri kullanılabilir [Yükleme Kılavuzu](../guides/install-nuget.md).</span><span class="sxs-lookup"><span data-stu-id="d1c24-116">All the information around both UI and command-line tools is available in the [Install guide](../guides/install-nuget.md).</span></span>

<span data-ttu-id="d1c24-117">**NuGet Mono destekliyor mu?**</span><span class="sxs-lookup"><span data-stu-id="d1c24-117">**Does NuGet support Mono?**</span></span>

<span data-ttu-id="d1c24-118">Komut satırı aracı `nuget.exe`, oluşturur ve Mono altında 3.2 + çalıştırır ve paketleri Mono olarak oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d1c24-118">The command-line tool, `nuget.exe`, builds and runs under Mono 3.2+ and can create packages in Mono.</span></span>

<span data-ttu-id="d1c24-119">Ancak `nuget.exe` çalışır tam olarak Windows, bilinen sorunlar vardır Linux ve OS x bakın [Mono sorunları](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) github'da.</span><span class="sxs-lookup"><span data-stu-id="d1c24-119">Although `nuget.exe` works fully on Windows, there are known issues on Linux and OS X. Refer to [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) on GitHub.</span></span>

<span data-ttu-id="d1c24-120">A [grafik istemci](https://github.com/mrward/monodevelop-nuget-addin) MonoDevelop için bir eklenti olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d1c24-120">A [graphical client](https://github.com/mrward/monodevelop-nuget-addin) is available as an add-in for MonoDevelop.</span></span>

<span data-ttu-id="d1c24-121">**Ne bir paket içerir ve kararlı ve Uygulamam için yararlı olup nasıl belirleyebilirim?**</span><span class="sxs-lookup"><span data-stu-id="d1c24-121">**How can I determine what a package contains and whether it's stable and useful for my application?**</span></span>

<span data-ttu-id="d1c24-122">Birincil bir paketi hakkında bilgi almak için kendi nuget.org listeleme sayfasında kaynağıdır (veya başka bir özel akış).</span><span class="sxs-lookup"><span data-stu-id="d1c24-122">The primary source for learning about a package is its listing page on nuget.org (or another private feed).</span></span> <span data-ttu-id="d1c24-123">Her bir paket nuget.org sayfasında paketi, sürüm geçmişi ve kullanım istatistiklerini açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="d1c24-123">Each package page on nuget.org includes a description of the package, its version history, and usage statistics.</span></span> <span data-ttu-id="d1c24-124">**Bilgisi** paketi sayfasında bölüm ayrıca projenin web genellikle bulabileceğiniz birçok örnekler ve paket nasıl kullanıldığını öğrenmenize yardımcı olacak diğer belgelerin siteye bir bağlantı içerir.</span><span class="sxs-lookup"><span data-stu-id="d1c24-124">The **Info** section on the package page also contains a link to the project's web site where you typically find many examples and other documentation to help you learn how the package is used.</span></span>

<span data-ttu-id="d1c24-125">Daha fazla bilgi için bkz: [bulma ve paketleri seçme](../Consume-Packages/Finding-and-Choosing-Packages.md).</span><span class="sxs-lookup"><span data-stu-id="d1c24-125">For more information, see [Finding and choosing packages](../Consume-Packages/Finding-and-Choosing-Packages.md).</span></span>

## <a name="nuget-in-visual-studio"></a><span data-ttu-id="d1c24-126">Visual Studio'da NuGet</span><span class="sxs-lookup"><span data-stu-id="d1c24-126">NuGet in Visual Studio</span></span>

<span data-ttu-id="d1c24-127">**Nasıl NuGet farklı Visual Studio ürünlerinde destekleniyor mu?**</span><span class="sxs-lookup"><span data-stu-id="d1c24-127">**How is NuGet supported in different Visual Studio products?**</span></span>

- <span data-ttu-id="d1c24-128">Visual Studio Windows destekler [Paket Yöneticisi kullanıcı Arabirimi](../tools/Package-Manager-UI.md) ve [Paket Yöneticisi Konsolu](../tools/Package-Manager-Console.md).</span><span class="sxs-lookup"><span data-stu-id="d1c24-128">Visual Studio on Windows supports the [Package Manager UI](../tools/Package-Manager-UI.md) and the [Package Manager Console](../tools/Package-Manager-Console.md).</span></span>
- <span data-ttu-id="d1c24-129">Mac için Visual Studio açıklandığı gibi yerleşik NuGet özellikleri olan [dahil olmak üzere bir NuGet paketini projenize](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="d1c24-129">Visual Studio for Mac has built-in NuGet capabilities as described on [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>
- <span data-ttu-id="d1c24-130">Visual Studio Code (tüm platformlar) doğrudan herhangi NuGet tümleştirme yok.</span><span class="sxs-lookup"><span data-stu-id="d1c24-130">Visual Studio Code (all platforms) does not have any direct NuGet integration.</span></span> <span data-ttu-id="d1c24-131">Kullanım [NuGet CLI](../tools/nuget-exe-CLI-Reference.md) veya [dotnet CLI](../tools/dotnet-commands.md).</span><span class="sxs-lookup"><span data-stu-id="d1c24-131">Use the [NuGet CLI](../tools/nuget-exe-CLI-Reference.md) or the [dotnet CLI](../tools/dotnet-commands.md).</span></span>
- <span data-ttu-id="d1c24-132">Visual Studio Team Services sağlar [NuGet paketlerini geri yüklemek için bir derleme adımı](/vsts/build-release/tasks/package/nuget).</span><span class="sxs-lookup"><span data-stu-id="d1c24-132">Visual Studio Team Services provides [a build step to restore NuGet packages](/vsts/build-release/tasks/package/nuget).</span></span> <span data-ttu-id="d1c24-133">Ayrıca [konak özel NuGet paketi akışları Team Services](https://www.visualstudio.com/docs/package/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="d1c24-133">You can also [host private NuGet package feeds on Team Services](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

<span data-ttu-id="d1c24-134">**Yüklü olan NuGet Araçlar'ün tam sürümünü nasıl kontrol edilsin mi?**</span><span class="sxs-lookup"><span data-stu-id="d1c24-134">**How do I check the exact version of the NuGet tools that are installed?**</span></span>

<span data-ttu-id="d1c24-135">Visual Studio'da kullanın **Yardım > Microsoft Visual Studio hakkında** komut ve yanında görüntülenen sürümünde arayın **NuGet Paket Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="d1c24-135">In Visual Studio, use the **Help > About Microsoft Visual Studio** command and look at the version displayed next to **NuGet Package Manager**.</span></span>

<span data-ttu-id="d1c24-136">Alternatif olarak, Paket Yöneticisi konsolu başlatın (**Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Konsolu**) ve girin `$host` NuGet sürümü de dahil olmak üzere hakkındaki bilgileri görmek için.</span><span class="sxs-lookup"><span data-stu-id="d1c24-136">Alternatively, launch the Package Manager Console (**Tools > NuGet Package Manager > Package Manager Console**) and enter `$host` to see information about NuGet including the version.</span></span>

<span data-ttu-id="d1c24-137">**Hangi programlama dillerini NuGet tarafından destekleniyor mu?**</span><span class="sxs-lookup"><span data-stu-id="d1c24-137">**What programming languages are supported by NuGet?**</span></span>

<span data-ttu-id="d1c24-138">NuGet genellikle .NET diller için kullanılabilir ve .NET kitaplıkları bir projeye duruma getirmek için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="d1c24-138">NuGet generally works for .NET languages and is designed to bring .NET libraries into a project.</span></span> <span data-ttu-id="d1c24-139">Ayrıca bazı proje türleri MSBuild ve Visual Studio Otomasyon desteklediği için diğer projeler ve çeşitli derece dilleri de destekler.</span><span class="sxs-lookup"><span data-stu-id="d1c24-139">Because it also supports MSBuild and Visual Studio automation in some project types, it also supports other projects and languages to various degrees.</span></span>

<span data-ttu-id="d1c24-140">C#, Visual Basic, F #, WiX ve C++ NuGet en son sürümünü destekler.</span><span class="sxs-lookup"><span data-stu-id="d1c24-140">The most recent version of NuGet supports C#, Visual Basic, F#, WiX, and C++.</span></span>

<span data-ttu-id="d1c24-141">**Hangi proje şablonları NuGet tarafından destekleniyor mu?**</span><span class="sxs-lookup"><span data-stu-id="d1c24-141">**What project templates are supported by NuGet?**</span></span>

<span data-ttu-id="d1c24-142">NuGet proje şablonları Windows, Web, bulut, SharePoint, Wix vb. gibi çeşitli için tam destek vardır.</span><span class="sxs-lookup"><span data-stu-id="d1c24-142">NuGet has full support for a variety of project templates like Windows, Web, Cloud, SharePoint, Wix, and so on.</span></span>

<span data-ttu-id="d1c24-143">**Visual Studio şablonları parçası olan paketleri nasıl güncelleştiririm?**</span><span class="sxs-lookup"><span data-stu-id="d1c24-143">**How do I update packages that are part of Visual Studio templates?**</span></span>

<span data-ttu-id="d1c24-144">Git **güncelleştirmeleri** sekmesinde Paket Yöneticisi Arabiriminde ve seçin **Tümünü Güncelleştir**, veya [ `Update-Package` komutu](../Tools/ps-ref-update-package.md) Paket Yöneticisi Konsolu'ndan.</span><span class="sxs-lookup"><span data-stu-id="d1c24-144">Go to the **Updates** tab in the Package Manager UI and select **Update All**, or use the [`Update-Package` command](../Tools/ps-ref-update-package.md) from the Package Manager Console.</span></span>

<span data-ttu-id="d1c24-145">Şablonu güncelleştirmek için şablon depo el ile güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d1c24-145">To update the template itself, you need to manually update the template repository.</span></span> <span data-ttu-id="d1c24-146">Bkz: [Xavier Decoster'ın blogu](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) Bu konu hakkında.</span><span class="sxs-lookup"><span data-stu-id="d1c24-146">See [Xavier Decoster's blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) on this subject.</span></span> <span data-ttu-id="d1c24-147">Tüm bağımlılıklarını en son sürümünü birbirleri ile uyumlu değilse el ile güncelleştirmeleri şablona bozulmasına neden olabilir çünkü bu, kendi risk yapılır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d1c24-147">Note that this is done at your own risk, because manual updates might corrupt the template if the latest version of all dependencies are not compatible with each other.</span></span>

<span data-ttu-id="d1c24-148">**NuGet Visual Studio dışında kullanabilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="d1c24-148">**Can I use NuGet outside of Visual Studio?**</span></span>

<span data-ttu-id="d1c24-149">Evet, NuGet doğrudan komut satırından çalışır.</span><span class="sxs-lookup"><span data-stu-id="d1c24-149">Yes, NuGet works directly from the command line.</span></span> <span data-ttu-id="d1c24-150">Bkz: [Yükleme Kılavuzu](../guides/install-nuget.md) ve [CLI başvuru](../tools/nuget-exe-CLI-Reference.md).</span><span class="sxs-lookup"><span data-stu-id="d1c24-150">See the [Install guide](../guides/install-nuget.md) and the [CLI reference](../tools/nuget-exe-CLI-Reference.md).</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="d1c24-151">NuGet komut satırı</span><span class="sxs-lookup"><span data-stu-id="d1c24-151">NuGet command line</span></span>

<span data-ttu-id="d1c24-152">**NuGet komut satırı aracının en son sürümünü nasıl sağlarım?**</span><span class="sxs-lookup"><span data-stu-id="d1c24-152">**How do I get the latest version of NuGet command line tool?**</span></span>

<span data-ttu-id="d1c24-153">Bkz: [Yükleme Kılavuzu](../guides/install-nuget.md).</span><span class="sxs-lookup"><span data-stu-id="d1c24-153">See the [Install guide](../guides/install-nuget.md).</span></span>

<span data-ttu-id="d1c24-154">**NuGet komut satırı aracı genişletmek mümkün mü?**</span><span class="sxs-lookup"><span data-stu-id="d1c24-154">**Is it possible to extend the NuGet command line tool?**</span></span>

<span data-ttu-id="d1c24-155">Evet, özel komut eklemek olası `nuget.exe`açıklandığı gibi [Ramiz Reynold'ın post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span><span class="sxs-lookup"><span data-stu-id="d1c24-155">Yes, it's possible to add custom commands to `nuget.exe`, as described in [Rob Reynold's post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span></span>

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a><span data-ttu-id="d1c24-156">NuGet Paket Yöneticisi Konsolu (Windows için Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="d1c24-156">NuGet Package Manager Console (Visual Studio on Windows)</span></span>

<span data-ttu-id="d1c24-157">**Paket Yöneticisi Konsolu'nda DTE nesneye erişimi nasıl sağlarım?**</span><span class="sxs-lookup"><span data-stu-id="d1c24-157">**How do I get access to the DTE object in the Package Manager console?**</span></span>

<span data-ttu-id="d1c24-158">Visual Studio Otomasyon nesne modeli en üst düzey nesnesinde DTE (geliştirme araçları ortamı) nesne adı verilir.</span><span class="sxs-lookup"><span data-stu-id="d1c24-158">The top-level object in the Visual Studio automation object model is called the DTE (Development Tools Environment) object.</span></span> <span data-ttu-id="d1c24-159">Konsol bu adlı bir değişken üzerinden sağlar `$DTE`.</span><span class="sxs-lookup"><span data-stu-id="d1c24-159">The console provides this through a variable named `$DTE`.</span></span> <span data-ttu-id="d1c24-160">Daha fazla bilgi için bkz: [Otomasyon modeline genel bakış](/visualstudio/extensibility/internals/automation-model-overview) Visual Studio genişletilebilirliğini belgelerinde.</span><span class="sxs-lookup"><span data-stu-id="d1c24-160">For more information, see [Automation Model Overview](/visualstudio/extensibility/internals/automation-model-overview) in the Visual Studio Extensibility documentation.</span></span>

<span data-ttu-id="d1c24-161">**DTE2 türü $DTE değişkenine cast deneyin, ancak bir hata iletisi: "" EnvDTE80.DTE2"türü için EnvDTE.DTEClass" türündeki "EnvDTE.DTEClass" değeri dönüştürülemiyor. Ne oldu?**</span><span class="sxs-lookup"><span data-stu-id="d1c24-161">**I try to cast the $DTE variable to the type DTE2, but I get an error: Cannot convert the "EnvDTE.DTEClass" value of type "EnvDTE.DTEClass" to type "EnvDTE80.DTE2". What's wrong?**</span></span>

<span data-ttu-id="d1c24-162">Bu, PowerShell COM nesnesi ile nasıl etkileşim kurduğu ile bilinen bir sorundur.</span><span class="sxs-lookup"><span data-stu-id="d1c24-162">This is a known issue with how PowerShell interacts with a COM object.</span></span> <span data-ttu-id="d1c24-163">Aşağıdakileri deneyin:</span><span class="sxs-lookup"><span data-stu-id="d1c24-163">Try the following:</span></span>

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

<span data-ttu-id="d1c24-164">`Get-Interface`yardımcı işlevi NuGet PowerShell ana bilgisayar tarafından eklenir.</span><span class="sxs-lookup"><span data-stu-id="d1c24-164">`Get-Interface` is a helper function added by the NuGet PowerShell host.</span></span>

## <a name="creating-and-publishing-packages"></a><span data-ttu-id="d1c24-165">Oluşturma ve paketleri yayımlama</span><span class="sxs-lookup"><span data-stu-id="d1c24-165">Creating and publishing packages</span></span>

<span data-ttu-id="d1c24-166">**Bir akış my paketinde nasıl listesinde?**</span><span class="sxs-lookup"><span data-stu-id="d1c24-166">**How do I list my package in a feed?**</span></span>

<span data-ttu-id="d1c24-167">Bkz: [oluşturma ve yayımlama bir paketi](../quickstart/create-and-publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="d1c24-167">See [Creating and publishing a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="d1c24-168">**.NET Framework'ün farklı sürümlerini hedefleyen birden fazla sürümünü Kitaplığı'mdan var. Bunu destekleyen tek bir paket nasıl oluşturulacağına?**</span><span class="sxs-lookup"><span data-stu-id="d1c24-168">**I have multiple versions of my library that target different versions of the .NET Framework. How do I build a single package that supports this?**</span></span>

<span data-ttu-id="d1c24-169">Bkz: [birden çok .NET Framework sürümleri ve profillerini destekleyen](../create-packages/supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="d1c24-169">See [Supporting Multiple .NET Framework Versions and Profiles](../create-packages/supporting-multiple-target-frameworks.md).</span></span>

<span data-ttu-id="d1c24-170">**Kendi deposu veya akış nasıl ayarlarım?**</span><span class="sxs-lookup"><span data-stu-id="d1c24-170">**How do I set up my own repository or feed?**</span></span>

<span data-ttu-id="d1c24-171">Bkz: [paketleri genel bakış barındırma](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="d1c24-171">See the [Hosting packages overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="d1c24-172">**Nasıl ı toplu olarak akış my NuGet paketleri yükleyebilir?**</span><span class="sxs-lookup"><span data-stu-id="d1c24-172">**How can I upload packages to my NuGet feed in bulk?**</span></span>

<span data-ttu-id="d1c24-173">Bkz: [toplu NuGet paketleri yayımlama](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span><span class="sxs-lookup"><span data-stu-id="d1c24-173">See [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span></span>

## <a name="working-with-packages"></a><span data-ttu-id="d1c24-174">Paketleri ile çalışma</span><span class="sxs-lookup"><span data-stu-id="d1c24-174">Working with packages</span></span>

<span data-ttu-id="d1c24-175">**Proje düzeyi paketi ve bir çözüm düzeyi paketi arasındaki fark nedir?**</span><span class="sxs-lookup"><span data-stu-id="d1c24-175">**What is the difference between a project-level package and a solution-level package?**</span></span>

<span data-ttu-id="d1c24-176">Bir çözüm düzeyi paketi (NuGet 3.x+) bir çözümde yalnızca bir kez yüklenir ve ardından Çözümdeki tüm projeleri için kullanılabilir hale gelir.</span><span class="sxs-lookup"><span data-stu-id="d1c24-176">A solution-level package (NuGet 3.x+) is installed only once in a solution and is then available for all projects in the solution.</span></span> <span data-ttu-id="d1c24-177">Proje düzeyi paketi kullandığı her projede yüklü.</span><span class="sxs-lookup"><span data-stu-id="d1c24-177">A project-level package is installed in each project that uses it.</span></span> <span data-ttu-id="d1c24-178">Bir çözüm düzeyi paket gelen paket Yöneticisi konsolu çağrılabilen yeni komutları da yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d1c24-178">A solution-level package might also install new commands that can be called from within the Package Manager Console.</span></span>

<span data-ttu-id="d1c24-179">**Internet bağlantısı olmadan NuGet paketlerini yüklemek mümkün mü?**</span><span class="sxs-lookup"><span data-stu-id="d1c24-179">**Is it possible to install NuGet packages without Internet connectivity?**</span></span>

<span data-ttu-id="d1c24-180">Evet, Scott Hanselman'ın Blog Gönderisi bkz [NuGet nuget.org aşağı (veya üzerinde bir düzlemi olduğunuz olduğunda) erişmek nasıl](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span><span class="sxs-lookup"><span data-stu-id="d1c24-180">Yes, see Scott Hanselman's Blog post [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span></span>

<span data-ttu-id="d1c24-181">**Varsayılan paket klasöründen farklı bir konumda paketleri nasıl yüklerim?**</span><span class="sxs-lookup"><span data-stu-id="d1c24-181">**How do I install packages in a different location from the default packages folder?**</span></span>

<span data-ttu-id="d1c24-182">Ayarlama [ `repositoryPath` ](../Schema/nuget-config-file.md#config-section) ayarı `Nuget.Config` kullanarak `nuget config -set repositoryPath=<path>`.</span><span class="sxs-lookup"><span data-stu-id="d1c24-182">Set the [`repositoryPath`](../Schema/nuget-config-file.md#config-section) setting in `Nuget.Config` using `nuget config -set repositoryPath=<path>`.</span></span>

<span data-ttu-id="d1c24-183">**NuGet paketleri klasörüne kaynak denetimine ekleme nasıl kaçının?**</span><span class="sxs-lookup"><span data-stu-id="d1c24-183">**How do I avoid adding the NuGet packages folder into to source control?**</span></span>

<span data-ttu-id="d1c24-184">Ayarlama [ `disableSourceControlIntegration` ](../Schema/nuget-config-file.md#solution-section) içinde `Nuget.Config` için `true`.</span><span class="sxs-lookup"><span data-stu-id="d1c24-184">Set the [`disableSourceControlIntegration`](../Schema/nuget-config-file.md#solution-section) in `Nuget.Config` to `true`.</span></span> <span data-ttu-id="d1c24-185">Çözüm, bu anahtar çalışır düzeyde ve bu nedenle gereksinim eklenecek `$(Solutiondir)\.nuget\Nuget.Config` dosya.</span><span class="sxs-lookup"><span data-stu-id="d1c24-185">This key works at the solution level and hence need to be added to the `$(Solutiondir)\.nuget\Nuget.Config` file.</span></span> <span data-ttu-id="d1c24-186">Paket geri yüklemesi Visual Studio'dan etkinleştirme bu dosyayı otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d1c24-186">Enabling package restore from Visual Studio creates this file automatically.</span></span>

<span data-ttu-id="d1c24-187">**Paket geri yükleme'yi nasıl kapatırım?**</span><span class="sxs-lookup"><span data-stu-id="d1c24-187">**How do I turn off package restore?**</span></span>

<span data-ttu-id="d1c24-188">Bkz: [etkinleştirme ve paket geri yüklemesi devre dışı bırakma](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="d1c24-188">See [Enabling and disabling package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="d1c24-189">**Neden alabilirim "bağımlılık hatası bir çözümlenemiyor" ne zaman uzaktan bağımlılıkları olan yerel bir paketi yükleniyor?**</span><span class="sxs-lookup"><span data-stu-id="d1c24-189">**Why do I get an "Unable to resolve dependency error" when installing a local package with remote dependencies?**</span></span>

<span data-ttu-id="d1c24-190">Seçmenize gerek **tüm** bir yerel paket projeye yüklerken kaynak.</span><span class="sxs-lookup"><span data-stu-id="d1c24-190">You need to select the **All** source when installing a local package into the project.</span></span> <span data-ttu-id="d1c24-191">Bu yalnızca bir kullanmak yerine tüm akışları toplar.</span><span class="sxs-lookup"><span data-stu-id="d1c24-191">This aggregates all the feeds instead of using just one.</span></span> <span data-ttu-id="d1c24-192">Bu hata görünür kullanıcıların yerel bir depo genellikle yanlışlıkla önlemek istediğiniz nedeni şirket nedeniyle uzak bir paket yükleme ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="d1c24-192">The reason this error appears is that users of a local repository often want to avoid accidentally installing a remote package due to corporate polices.</span></span>

<span data-ttu-id="d1c24-193">**Birden çok proje aynı klasörde sahibim, ayrı packages.config dosyaları her proje için nasıl kullanabilirim?**</span><span class="sxs-lookup"><span data-stu-id="d1c24-193">**I have multiple projects in the same folder, how can I use separate packages.config files for each project?**</span></span>

<span data-ttu-id="d1c24-194">NuGet tanımlayan gibi burada ayrı projeler Canlı ayrı klasörlerde çoğu projelerde, bu bir sorun teşkil etmez `packages.config` her proje dosyaları.</span><span class="sxs-lookup"><span data-stu-id="d1c24-194">In most projects where separate projects live in separate folders, this is not a problem as NuGet identifies the `packages.config` files in each project.</span></span> <span data-ttu-id="d1c24-195">NuGet 3.3 + ve birden fazla ile projeleri ile aynı klasörde projeye adını ekleyebilirsiniz `packages.config` dosya adlarını kullanın düzeni `packages.{project-name}.config`, ve NuGet bu dosyasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="d1c24-195">With NuGet 3.3+ and multiple projects in the same folder, you can insert the name of the project into the `packages.config` filenames use the pattern `packages.{project-name}.config`, and NuGet uses that file.</span></span>

<span data-ttu-id="d1c24-196">Her proje dosyası bağımlılıkları kendi listesi içerdiğinden bu bir sorun PackageReference, kullanırken değildir.</span><span class="sxs-lookup"><span data-stu-id="d1c24-196">This is not an issue when using PackageReference, as each project file contains its own list of dependencies.</span></span>

<span data-ttu-id="d1c24-197">**Nuget.org depoları my listede göremiyorum, nasıl geri sağlarım?**</span><span class="sxs-lookup"><span data-stu-id="d1c24-197">**I don't see nuget.org in my list of repositories, how do I get it back?**</span></span>

- <span data-ttu-id="d1c24-198">Ekleme `https://api.nuget.org/v3/index.json` kaynakları, listenize veya</span><span class="sxs-lookup"><span data-stu-id="d1c24-198">Add `https://api.nuget.org/v3/index.json` to your list of sources, or</span></span>
- <span data-ttu-id="d1c24-199">Silme `%appdata%\.nuget\NuGet.Config` ve yeniden oluşturun NuGet izin verin.</span><span class="sxs-lookup"><span data-stu-id="d1c24-199">Delete the `%appdata%\.nuget\NuGet.Config` and let NuGet re-create it.</span></span>

<span data-ttu-id="d1c24-200">**Bir paketi belirli lisans bilgileri sağlamazsa koşulları varsayılan lisans nelerdir?**</span><span class="sxs-lookup"><span data-stu-id="d1c24-200">**What are the default license terms if a package doesn't provide specific license information?**</span></span>

<span data-ttu-id="d1c24-201">Her paket paketine dahil terimleri tabidir.</span><span class="sxs-lookup"><span data-stu-id="d1c24-201">Each package is governed by the terms that are included with the package.</span></span> <span data-ttu-id="d1c24-202">Erişim, indirme ya da herhangi bir paket alınırken önce hüküm gözden geçirmelidir.</span><span class="sxs-lookup"><span data-stu-id="d1c24-202">You should review the applicable terms before accessing, downloading, or acquiring any packages.</span></span> <span data-ttu-id="d1c24-203">Nuget.org üzerinde kullanmak **lisans bilgilerini** bağlantı paketi sayfasında.</span><span class="sxs-lookup"><span data-stu-id="d1c24-203">On nuget.org, use the **License Info** link on the package page.</span></span>

<span data-ttu-id="d1c24-204">Bir paketi Lisans Koşulları'nı belirtmiyorsa kullanarak doğrudan paketi sahibine başvurun **sahipleri başvurun** nuget.org paketi sayfasında bağlantı.</span><span class="sxs-lookup"><span data-stu-id="d1c24-204">If a package does not specify the licensing terms, contact the package owner directly using the **Contact owners** link on the nuget.org package page.</span></span> <span data-ttu-id="d1c24-205">Microsoft hiçbir fikri mülkiyet, üçüncü taraf paket sağlayıcılardan lisans değildir ve üçüncü taraflar tarafından sağlanan bilgileri sorumlu değildir.</span><span class="sxs-lookup"><span data-stu-id="d1c24-205">Microsoft does not license any intellectual property to you from third party package providers and is not responsible for information provided by third parties.</span></span>


## <a name="managing-packages-on-nugetorg"></a><span data-ttu-id="d1c24-206">Nuget.org paketlerini yönetme</span><span class="sxs-lookup"><span data-stu-id="d1c24-206">Managing packages on nuget.org</span></span>

<span data-ttu-id="d1c24-207">**Paket meta verileri, karşıya yüklendikten sonra düzenleyebilir miyim? Nuspec düzenleme ve meta veri paketini değişiklik yapmak için yeni bir paket karşıya yükleme neden önerilir?**</span><span class="sxs-lookup"><span data-stu-id="d1c24-207">**Can I edit package metadata after it's been uploaded? Why do you recommend editing the nuspec and uploading a new package for making changes to package metadata?**</span></span>

<span data-ttu-id="d1c24-208">NuGet paket imzalama uygulama.</span><span class="sxs-lookup"><span data-stu-id="d1c24-208">NuGet will be implementing package signing.</span></span> <span data-ttu-id="d1c24-209">Paketin imzalanması bir tasarım prensibi imzalı paket içeriğini nuspec içeren değişmez, olmanızın gerekmesidir.</span><span class="sxs-lookup"><span data-stu-id="d1c24-209">A design principle of package signing is that signed package content must be immutable, which includes the nuspec.</span></span> <span data-ttu-id="d1c24-210">Paket meta verileri düzenleme değişiklikleri varolan imza geçersiz kılmalarını nuspec için sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="d1c24-210">Editing the package metadata results in changes to the nuspec, invalidating existing signatures.</span></span> <span data-ttu-id="d1c24-211">Paket oluşturulduktan sonra paket meta verileri düzenleme gerektirmeyecek şekilde var olan iş akışları değiştirme öneririz.</span><span class="sxs-lookup"><span data-stu-id="d1c24-211">We recommend modifying existing workflows to not require editing the package metadata after the package has been created.</span></span>

<span data-ttu-id="d1c24-212">Not paketiniz için listelenen bağımlılıkları paketinden otomatik olarak oluşturulur ve düzenlenemez.</span><span class="sxs-lookup"><span data-stu-id="d1c24-212">Note that dependencies listed for your package are generated automatically from the package itself and cannot be edited.</span></span>

<span data-ttu-id="d1c24-213">Ayrıca, paketler karşıya [staging.nuget.org](http://staging.nuget.org) sınamak ve bir paket genel bir galeride kullanıma olmadan paketinizi doğrulamak için harika bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="d1c24-213">In addition, uploading packages to [staging.nuget.org](http://staging.nuget.org) is a great way to test and validate your package without making a package available in the public gallery.</span></span>

<span data-ttu-id="d1c24-214">**Gelecekte yayımlanacak paketler için adları ayırmak mümkün mü?**</span><span class="sxs-lookup"><span data-stu-id="d1c24-214">**Is it possible to reserve names for packages that will be published in future?**</span></span>

<span data-ttu-id="d1c24-215">Evet.</span><span class="sxs-lookup"><span data-stu-id="d1c24-215">Yes.</span></span> <span data-ttu-id="d1c24-216">Üzerinde paketler için kimlikleri ayırabilirsiniz [nuget.org](https://www.nuget.org/) hesabınız için bir paket kimliği önek isteyen tarafından.</span><span class="sxs-lookup"><span data-stu-id="d1c24-216">You can reserve IDs for packages on [nuget.org](https://www.nuget.org/) by requesting a package ID prefix for your account.</span></span> <span data-ttu-id="d1c24-217">Bir paket kimliği öneki istemek için (saat) paketi sahibi görünen adı ve istenen paket kimliği öneki ile nuget.org hesabı posta gönderin.</span><span class="sxs-lookup"><span data-stu-id="d1c24-217">In order to request a package ID prefix, send mail to account (at) nuget.org with the package owner display name, and the requested package ID prefix.</span></span>  

<span data-ttu-id="d1c24-218">**Paketler için sahipliğini talep nasıl?**</span><span class="sxs-lookup"><span data-stu-id="d1c24-218">**How do I claim ownership for packages ?**</span></span>

<span data-ttu-id="d1c24-219">Bkz: [yönetme paket sahipleri nuget.org üzerinde](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="d1c24-219">See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span>

<span data-ttu-id="d1c24-220">**My yazılım lisansı ihlal eden bir paket sahibi ile nasıl ilgilenir?**</span><span class="sxs-lookup"><span data-stu-id="d1c24-220">**How do I deal with a package owner who is violating my software license?**</span></span>

<span data-ttu-id="d1c24-221">Paket sahipleri ve diğer yazılımların sahipleri arasında kaynaklanabilecek itirazları çözümlemek için birlikte çalışmak üzere NuGet topluluk öneririz.</span><span class="sxs-lookup"><span data-stu-id="d1c24-221">We encourage the NuGet community to work together to resolve any disputes that may arise between package owners and the owners of other software.</span></span> <span data-ttu-id="d1c24-222">Biz hazırlanmış bir [itiraz çözümleme işlemi](../policies/dispute-resolution.md) nuget.org yöneticilerin intercede soran önce izlemek için.</span><span class="sxs-lookup"><span data-stu-id="d1c24-222">We have crafted a [dispute resolution process](../policies/dispute-resolution.md) to follow before asking nuget.org administrators to intercede.</span></span>

<span data-ttu-id="d1c24-223">**My sınama paketlerini nuget.org için karşıya yükleme önerilir?**</span><span class="sxs-lookup"><span data-stu-id="d1c24-223">**Is it recommended to upload my test packages to nuget.org?**</span></span>

<span data-ttu-id="d1c24-224">Test amaçları için kullandığınız [staging.nuget.org](http://staging.nuget.org), veya alternatif ortak NuGet sunucularını [myget.org](https://myget.org) veya [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).</span><span class="sxs-lookup"><span data-stu-id="d1c24-224">For test purposes, you can use [staging.nuget.org](http://staging.nuget.org), or alternative public NuGet servers like [myget.org](https://myget.org) or [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).</span></span>

<span data-ttu-id="d1c24-225">Paketler için Staging.nuget.org karşıya korunmaz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d1c24-225">Note that packages uploaded to staging.nuget.org may not be preserved.</span></span> <span data-ttu-id="d1c24-226">Bkz: [güle güle Önizleme](http://blog.nuget.org/20130419/goodbye-preview.html).</span><span class="sxs-lookup"><span data-stu-id="d1c24-226">See [Goodbye preview](http://blog.nuget.org/20130419/goodbye-preview.html).</span></span>

<span data-ttu-id="d1c24-227">**Paketler için nuget.org karşıya yükleyebilir en büyük boyutu nedir?**</span><span class="sxs-lookup"><span data-stu-id="d1c24-227">**What is the maximum size of packages I can upload to nuget.org?**</span></span>

<span data-ttu-id="d1c24-228">nuget.org sağlayan paketler en fazla 250MB, ancak paketleri birbirine bağlamak için bağımlılıkları kullanarak ve paketleri 1 MB'den mümkünse tutulması önerilir.</span><span class="sxs-lookup"><span data-stu-id="d1c24-228">nuget.org allows packages up to 250MB, but we recommend keeping packages under 1MB if possible and using dependencies to link packages together.</span></span> <span data-ttu-id="d1c24-229">Altın kural, çakışmaları önlemek için yalnızca bir derleme paketleri içerir.</span><span class="sxs-lookup"><span data-stu-id="d1c24-229">As a rule of thumb, packages contain only one assembly to avoid collisions.</span></span>

<span data-ttu-id="d1c24-230">NuGet paketleri, başarısız yükler olasılığı daha küçük olanları daha büyük paketleriniz varsa şekilde indirmek için HTTP kullanır.</span><span class="sxs-lookup"><span data-stu-id="d1c24-230">NuGet uses HTTP to download packages, so larger packages have a higher likelihood of failed installs than smaller ones.</span></span>

<span data-ttu-id="d1c24-231">NuGet paketlerinizi Tüketiciler için toplam yükleme boyutunu küçülterek, birden çok paket arasındaki bağımlılıkları paylaşmak da mümkündür.</span><span class="sxs-lookup"><span data-stu-id="d1c24-231">It is possible to share dependencies between multiple packages, making the total download size for consumers of your NuGet packages smaller.</span></span>

<span data-ttu-id="d1c24-232">Çoğunlukla statik ve hiçbir zaman değişikliği bağımlılıklardır.</span><span class="sxs-lookup"><span data-stu-id="d1c24-232">Dependencies are mostly static and never change.</span></span> <span data-ttu-id="d1c24-233">Kodda bir hata düzeltme, bağımlılıkları güncelleştirilmesi gerekmeyebilir.</span><span class="sxs-lookup"><span data-stu-id="d1c24-233">When fixing a bug in code, the dependencies may not need to be updated.</span></span> <span data-ttu-id="d1c24-234">Bağımlılıklar paketini, her zaman büyük paketler reshipping yukarı sonlandırın.</span><span class="sxs-lookup"><span data-stu-id="d1c24-234">If you bundle dependencies, you end up reshipping larger packages every time.</span></span> <span data-ttu-id="d1c24-235">NuGet paketleri ilgili bağımlılıkları bölerek yükseltme paketinizi Tüketiciler için çok daha ayrıntılı sağlar.</span><span class="sxs-lookup"><span data-stu-id="d1c24-235">By splitting NuGet packages into related dependencies, upgrades are much more fine-grained for consumers of your package.</span></span>

## <a name="nugetorg-not-accessible"></a><span data-ttu-id="d1c24-236">nuget.org erişilebilir değil</span><span class="sxs-lookup"><span data-stu-id="d1c24-236">nuget.org not accessible</span></span>

<span data-ttu-id="d1c24-237">**Neden paketleri indirme veya paketler için nuget.org karşıya?**</span><span class="sxs-lookup"><span data-stu-id="d1c24-237">**Why can't I download packages from or upload packages to nuget.org?**</span></span>

<span data-ttu-id="d1c24-238">Öncelikle, NuGet'ın en son sürümlerini kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d1c24-238">First, make sure you're using the latest versions of NuGet.</span></span> <span data-ttu-id="d1c24-239">Bu sürüm başarısız olmaya devam ederse [desteğine başvurun](https://www.nuget.org/policies/Contact) ve sorun giderme bilgileri de dahil olmak üzere ek bağlantı sağlayın:</span><span class="sxs-lookup"><span data-stu-id="d1c24-239">If that version continues to fail, [contact support](https://www.nuget.org/policies/Contact) and provide additional connection troubleshooting information including:</span></span>

- <span data-ttu-id="d1c24-240">Kullanmakta olduğunuz NuGet sürümü</span><span class="sxs-lookup"><span data-stu-id="d1c24-240">The version of NuGet you're using</span></span>
- <span data-ttu-id="d1c24-241">Kullanmakta olduğunuz paket kaynaklarını</span><span class="sxs-lookup"><span data-stu-id="d1c24-241">The package sources you're using</span></span>
- <span data-ttu-id="d1c24-242">Ayrıntılı ayrıntı düzeyine sahip bir geri yükleme günlüğü</span><span class="sxs-lookup"><span data-stu-id="d1c24-242">A restore log with detailed verbosity</span></span>
- <span data-ttu-id="d1c24-243">MTR veya Fiddler izlemeleri (aşağıya bakın)</span><span class="sxs-lookup"><span data-stu-id="d1c24-243">MTR or a Fiddler traces (see below)</span></span>
- <span data-ttu-id="d1c24-244">Coğrafi konuma</span><span class="sxs-lookup"><span data-stu-id="d1c24-244">Your geographical area</span></span>
- <span data-ttu-id="d1c24-245">İşletim sistemi sürümü</span><span class="sxs-lookup"><span data-stu-id="d1c24-245">Your operating system version</span></span>
- <span data-ttu-id="d1c24-246">Makine Yapılandırma (CPU, ağ, sabit sürücü)</span><span class="sxs-lookup"><span data-stu-id="d1c24-246">Machine configuration (CPU, Network, hard drive)</span></span>
- <span data-ttu-id="d1c24-247">Makinenizde bir proxy veya güvenlik duvarı arkasında olup</span><span class="sxs-lookup"><span data-stu-id="d1c24-247">Whether is your machine behind a proxy or firewall</span></span>
- <span data-ttu-id="d1c24-248">Makinede yüklü .NET sürümlerini</span><span class="sxs-lookup"><span data-stu-id="d1c24-248">The versions of .NET that are installed on the machine</span></span>
- <span data-ttu-id="d1c24-249">Platformlar arası araçlarının .NET CLI ya da kullandığınız DNU gibi sürümleri</span><span class="sxs-lookup"><span data-stu-id="d1c24-249">Versions of cross-platform tools such as .NET CLI, or DNU that you're using</span></span>

<span data-ttu-id="d1c24-250">*MTR yakalamak için:*</span><span class="sxs-lookup"><span data-stu-id="d1c24-250">*To capture MTR:*</span></span>

- <span data-ttu-id="d1c24-251">Gelen WinMTR karşıdan [http://winmtr.net/download/](http://winmtr.net/)</span><span class="sxs-lookup"><span data-stu-id="d1c24-251">Download WinMTR from [http://winmtr.net/download/](http://winmtr.net/)</span></span>
- <span data-ttu-id="d1c24-252">Girin `api.nuget.org` tıklatın ve ana bilgisayar adı olarak **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="d1c24-252">Enter `api.nuget.org` as the hostname and click **Start**.</span></span>
- <span data-ttu-id="d1c24-253">Bekle **gönderilen** sütunu > = 100.</span><span class="sxs-lookup"><span data-stu-id="d1c24-253">Wait until the **Sent** column is >= 100.</span></span>

    ![MTR yakalama](media/mtr.png)

- <span data-ttu-id="d1c24-255">Metni panoya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="d1c24-255">Copy text to clipboard.</span></span>

<span data-ttu-id="d1c24-256">*Fiddler yakalamak için:*</span><span class="sxs-lookup"><span data-stu-id="d1c24-256">*To capture Fiddler:*</span></span>

- <span data-ttu-id="d1c24-257">En son sürümünü yüklemek [Fiddler](http://www.telerik.com/download/fiddler).</span><span class="sxs-lookup"><span data-stu-id="d1c24-257">Install the latest version of [Fiddler](http://www.telerik.com/download/fiddler).</span></span>
- <span data-ttu-id="d1c24-258">Fiddler'ı başlatın ve yakalama trafiği kullanılarak devre dışı bırakma **Dosya > trafiği Yakala** menüsü.</span><span class="sxs-lookup"><span data-stu-id="d1c24-258">Start Fiddler and disable capturing traffic using the **File > Capture Traffic** menu.</span></span>
- <span data-ttu-id="d1c24-259">Tüm oturumları kaldırın (tüm öğeleri listesinde, basın seçme **silmek** anahtar).</span><span class="sxs-lookup"><span data-stu-id="d1c24-259">Remove all sessions (select all items in the list, press the **Delete** key).</span></span>
- <span data-ttu-id="d1c24-260">HTTPS trafiğini denetleyerek yakalamak için fiddler'ı yapılandırma **şifresini HTTPS trafiği** içinde **HTTPS** sekmesinde **Araçlar > Fiddler seçenekleri...**  menüsü.</span><span class="sxs-lookup"><span data-stu-id="d1c24-260">Configure Fiddler to capture HTTPS traffic by checking **Decrypt HTTPS traffic** in the **HTTPS** tab of the **Tools > Fiddler Options...** menu.</span></span>
- <span data-ttu-id="d1c24-261">Visual Studio’yu kapatın.</span><span class="sxs-lookup"><span data-stu-id="d1c24-261">Close Visual Studio.</span></span>
- <span data-ttu-id="d1c24-262">Etkinleştirme **Dosya > trafiği Yakala** menüsü.</span><span class="sxs-lookup"><span data-stu-id="d1c24-262">Enable the **File > Capture Traffic** menu.</span></span>
- <span data-ttu-id="d1c24-263">Visual Studio ya da nuget.exe .exe başlatmak ve çalışmıyor eylemleri gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d1c24-263">Start Visual Studio or nuget.exe .exe and perform the actions that are not working.</span></span> <span data-ttu-id="d1c24-264">Bu eylemleri tarafından oluşturulan trafiğin Fiddler'da göstermelidir.</span><span class="sxs-lookup"><span data-stu-id="d1c24-264">The traffic generated by these actions should show up in Fiddler.</span></span>
- <span data-ttu-id="d1c24-265">Eylemler çalıştırdıktan sonra kullanmak **Dosya > Kaydet > tüm oturumları** yakalanan oturumları depolamak için.</span><span class="sxs-lookup"><span data-stu-id="d1c24-265">Once the actions have run, use **File > Save > All Sessions** to store the captured sessions.</span></span>

<span data-ttu-id="d1c24-266">Not: Bunu ayarlamak için gerekli olabilecek `HTTP_PROXY` ortam değişkenine `http://127.0.0.1:8888` Fiddler aracılığıyla yönlendirme NuGet trafiği için.</span><span class="sxs-lookup"><span data-stu-id="d1c24-266">Note: it may be required to set the `HTTP_PROXY` environment variable to `http://127.0.0.1:8888` for routing NuGet traffic through Fiddler.</span></span>

<span data-ttu-id="d1c24-267">Başarısız olursa, deneyin [bu StackOverflow postasında belirtilen ipuçları](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).</span><span class="sxs-lookup"><span data-stu-id="d1c24-267">If that fails, try the [tips mentioned in this StackOverflow post](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).</span></span>

<span data-ttu-id="d1c24-268">**Nuget.org için API uç noktaları nelerdir?**</span><span class="sxs-lookup"><span data-stu-id="d1c24-268">**What are the API endpoints for nuget.org?**</span></span>

<span data-ttu-id="d1c24-269">V3: `https://api.nuget.org/v3/index.json` V2: `https://www.nuget.org/api/v2/` (V2 API kullanım dışıdır ve NuGet ile 4 + çalışmaz unutmayın.)</span><span class="sxs-lookup"><span data-stu-id="d1c24-269">V3: `https://api.nuget.org/v3/index.json` V2: `https://www.nuget.org/api/v2/` (Note that the V2 API is deprecated and does not work with NuGet 4+.)</span></span>
