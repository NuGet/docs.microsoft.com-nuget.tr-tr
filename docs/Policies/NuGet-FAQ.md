---
title: "Sık sorulan-sorular NuGet | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/11/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 199a915d-9595-4ae2-a1fb-b15da6d7735a
description: "Ortak sorular ve yanıtlar NuGet komut satırında ve Visual Studio kullanarak ve NuGet Galerisi ile çalışmak için."
keywords: "NuGet soru- cevap, sorular ve yanıtlar, ortak sorunları, NuGet sürümleri, sürüm paketi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f029af78edfcc5e542c5df2d4d6db8eeaebc3068
ms.sourcegitcommit: d576d84fb4b6a178eb2ac11f55deb08ac771ba1c
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/16/2018
---
# <a name="nuget-frequently-asked-questions"></a><span data-ttu-id="7a5d3-104">NuGet sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="7a5d3-104">NuGet frequently-asked questions</span></span>

<span data-ttu-id="7a5d3-105">Bu konuda:</span><span class="sxs-lookup"><span data-stu-id="7a5d3-105">In this topic:</span></span>

- [<span data-ttu-id="7a5d3-106">Başlarken</span><span class="sxs-lookup"><span data-stu-id="7a5d3-106">Getting started</span></span>](#getting-started)
- [<span data-ttu-id="7a5d3-107">Visual Studio'da NuGet</span><span class="sxs-lookup"><span data-stu-id="7a5d3-107">NuGet in Visual Studio</span></span>](#nuget-in-visual-studio)
- [<span data-ttu-id="7a5d3-108">NuGet komut satırı</span><span class="sxs-lookup"><span data-stu-id="7a5d3-108">NuGet command line</span></span>](#nuget-command-line)
- [<span data-ttu-id="7a5d3-109">NuGet Paket Yöneticisi Konsolu</span><span class="sxs-lookup"><span data-stu-id="7a5d3-109">NuGet Package Manager Console</span></span>](#nuget-package-manager-console)
- [<span data-ttu-id="7a5d3-110">Oluşturma ve paketleri yayımlama</span><span class="sxs-lookup"><span data-stu-id="7a5d3-110">Creating and publishing packages</span></span>](#creating-and-publishing-packages)
- [<span data-ttu-id="7a5d3-111">Paketleri ile çalışma</span><span class="sxs-lookup"><span data-stu-id="7a5d3-111">Working with packages</span></span>](#working-with-packages)
- [<span data-ttu-id="7a5d3-112">Nuget.org paketlerini yönetme</span><span class="sxs-lookup"><span data-stu-id="7a5d3-112">Managing packages on nuget.org</span></span>](#managing-packages-on-nugetorg)
- [<span data-ttu-id="7a5d3-113">nuget.org erişilebilir değil</span><span class="sxs-lookup"><span data-stu-id="7a5d3-113">nuget.org not accessible</span></span>](#nugetorg-not-accessible)

## <a name="getting-started"></a><span data-ttu-id="7a5d3-114">Başlarken</span><span class="sxs-lookup"><span data-stu-id="7a5d3-114">Getting started</span></span>

<span data-ttu-id="7a5d3-115">**NuGet çalıştırmak için gereken nedir?**</span><span class="sxs-lookup"><span data-stu-id="7a5d3-115">**What is required to run NuGet?**</span></span>

<span data-ttu-id="7a5d3-116">Kullanıcı Arabirimi ve komut satırı araçları geçici tüm bilgileri kullanılabilir [Yükleme Kılavuzu](../guides/install-nuget.md).</span><span class="sxs-lookup"><span data-stu-id="7a5d3-116">All the information around both UI and command-line tools is available in the [Install guide](../guides/install-nuget.md).</span></span>

<span data-ttu-id="7a5d3-117">**NuGet Mono destekliyor mu?**</span><span class="sxs-lookup"><span data-stu-id="7a5d3-117">**Does NuGet support Mono?**</span></span>

<span data-ttu-id="7a5d3-118">Komut satırı aracı `nuget.exe`, oluşturur ve Mono altında 3.2 + çalıştırır ve paketleri Mono olarak oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-118">The command-line tool, `nuget.exe`, builds and runs under Mono 3.2+ and can create packages in Mono.</span></span>

<span data-ttu-id="7a5d3-119">Ancak `nuget.exe` çalışır tam olarak Windows, bilinen sorunlar vardır Linux ve OS x bakın [Mono sorunları](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) github'da.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-119">Although `nuget.exe` works fully on Windows, there are known issues on Linux and OS X. Refer to [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) on GitHub.</span></span>

<span data-ttu-id="7a5d3-120">A [grafik istemci](https://github.com/mrward/monodevelop-nuget-addin) MonoDevelop için bir eklenti olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-120">A [graphical client](https://github.com/mrward/monodevelop-nuget-addin) is available as an add-in for MonoDevelop.</span></span>

<span data-ttu-id="7a5d3-121">**Ne bir paket içerir ve kararlı ve Uygulamam için yararlı olup nasıl belirleyebilirim?**</span><span class="sxs-lookup"><span data-stu-id="7a5d3-121">**How can I determine what a package contains and whether it's stable and useful for my application?**</span></span>

<span data-ttu-id="7a5d3-122">Birincil bir paketi hakkında bilgi almak için kendi nuget.org listeleme sayfasında kaynağıdır (veya başka bir özel akış).</span><span class="sxs-lookup"><span data-stu-id="7a5d3-122">The primary source for learning about a package is its listing page on nuget.org (or another private feed).</span></span> <span data-ttu-id="7a5d3-123">Her bir paket nuget.org sayfasında paketi, sürüm geçmişi ve kullanım istatistiklerini açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-123">Each package page on nuget.org includes a description of the package, its version history, and usage statistics.</span></span> <span data-ttu-id="7a5d3-124">**Bilgisi** paketi sayfasında bölüm ayrıca projenin web genellikle bulabileceğiniz birçok örnekler ve paket nasıl kullanıldığını öğrenmenize yardımcı olacak diğer belgelerin siteye bir bağlantı içerir.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-124">The **Info** section on the package page also contains a link to the project's web site where you typically find many examples and other documentation to help you learn how the package is used.</span></span>

<span data-ttu-id="7a5d3-125">Daha fazla bilgi için bkz: [bulma ve paketleri seçme](../Consume-Packages/Finding-and-Choosing-Packages.md).</span><span class="sxs-lookup"><span data-stu-id="7a5d3-125">For more information, see [Finding and choosing packages](../Consume-Packages/Finding-and-Choosing-Packages.md).</span></span>

## <a name="nuget-in-visual-studio"></a><span data-ttu-id="7a5d3-126">Visual Studio'da NuGet</span><span class="sxs-lookup"><span data-stu-id="7a5d3-126">NuGet in Visual Studio</span></span>

<span data-ttu-id="7a5d3-127">**Nasıl NuGet farklı Visual Studio ürünlerinde destekleniyor mu?**</span><span class="sxs-lookup"><span data-stu-id="7a5d3-127">**How is NuGet supported in different Visual Studio products?**</span></span>

- <span data-ttu-id="7a5d3-128">Visual Studio Windows destekler [Paket Yöneticisi kullanıcı Arabirimi](../tools/Package-Manager-UI.md) ve [Paket Yöneticisi Konsolu](../tools/Package-Manager-Console.md).</span><span class="sxs-lookup"><span data-stu-id="7a5d3-128">Visual Studio on Windows supports the [Package Manager UI](../tools/Package-Manager-UI.md) and the [Package Manager Console](../tools/Package-Manager-Console.md).</span></span>
- <span data-ttu-id="7a5d3-129">Mac için Visual Studio açıklandığı gibi yerleşik NuGet özellikleri olan [dahil olmak üzere bir NuGet paketini projenize](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="7a5d3-129">Visual Studio for Mac has built-in NuGet capabilities as described on [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>
- <span data-ttu-id="7a5d3-130">Visual Studio Code (tüm platformlar) doğrudan herhangi NuGet tümleştirme yok.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-130">Visual Studio Code (all platforms) does not have any direct NuGet integration.</span></span> <span data-ttu-id="7a5d3-131">Kullanım [NuGet CLI](../tools/nuget-exe-CLI-Reference.md) veya [dotnet CLI](../tools/dotnet-commands.md).</span><span class="sxs-lookup"><span data-stu-id="7a5d3-131">Use the [NuGet CLI](../tools/nuget-exe-CLI-Reference.md) or the [dotnet CLI](../tools/dotnet-commands.md).</span></span>
- <span data-ttu-id="7a5d3-132">Visual Studio Team Services sağlar [NuGet paketlerini geri yüklemek için bir derleme adımı](/vsts/build-release/tasks/package/nuget).</span><span class="sxs-lookup"><span data-stu-id="7a5d3-132">Visual Studio Team Services provides [a build step to restore NuGet packages](/vsts/build-release/tasks/package/nuget).</span></span> <span data-ttu-id="7a5d3-133">Ayrıca [konak özel NuGet paketi akışları Team Services](https://www.visualstudio.com/docs/package/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="7a5d3-133">You can also [host private NuGet package feeds on Team Services](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

<span data-ttu-id="7a5d3-134">**Yüklü olan NuGet Araçlar'ün tam sürümünü nasıl kontrol edilsin mi?**</span><span class="sxs-lookup"><span data-stu-id="7a5d3-134">**How do I check the exact version of the NuGet tools that are installed?**</span></span>

<span data-ttu-id="7a5d3-135">Visual Studio'da kullanın **Yardım > Microsoft Visual Studio hakkında** komut ve yanında görüntülenen sürümünde arayın **NuGet Paket Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-135">In Visual Studio, use the **Help > About Microsoft Visual Studio** command and look at the version displayed next to **NuGet Package Manager**.</span></span>

<span data-ttu-id="7a5d3-136">Alternatif olarak, Paket Yöneticisi konsolu başlatın (**Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Konsolu**) ve girin `$host` NuGet sürümü de dahil olmak üzere hakkındaki bilgileri görmek için.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-136">Alternatively, launch the Package Manager Console (**Tools > NuGet Package Manager > Package Manager Console**) and enter `$host` to see information about NuGet including the version.</span></span>

<span data-ttu-id="7a5d3-137">**Hangi programlama dillerini NuGet tarafından destekleniyor mu?**</span><span class="sxs-lookup"><span data-stu-id="7a5d3-137">**What programming languages are supported by NuGet?**</span></span>

<span data-ttu-id="7a5d3-138">NuGet genellikle .NET diller için kullanılabilir ve .NET kitaplıkları bir projeye duruma getirmek için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-138">NuGet generally works for .NET languages and is designed to bring .NET libraries into a project.</span></span> <span data-ttu-id="7a5d3-139">Ayrıca bazı proje türleri MSBuild ve Visual Studio Otomasyon desteklediği için diğer projeler ve çeşitli derece dilleri de destekler.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-139">Because it also supports MSBuild and Visual Studio automation in some project types, it also supports other projects and languages to various degrees.</span></span>

<span data-ttu-id="7a5d3-140">C#, Visual Basic, F #, WiX ve C++ NuGet en son sürümünü destekler.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-140">The most recent version of NuGet supports C#, Visual Basic, F#, WiX, and C++.</span></span>

<span data-ttu-id="7a5d3-141">**Hangi proje şablonları NuGet tarafından destekleniyor mu?**</span><span class="sxs-lookup"><span data-stu-id="7a5d3-141">**What project templates are supported by NuGet?**</span></span>

<span data-ttu-id="7a5d3-142">NuGet proje şablonları Windows, Web, bulut, SharePoint, Wix vb. gibi çeşitli için tam destek vardır.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-142">NuGet has full support for a variety of project templates like Windows, Web, Cloud, SharePoint, Wix, and so on.</span></span>

<span data-ttu-id="7a5d3-143">**Visual Studio şablonları parçası olan paketleri nasıl güncelleştiririm?**</span><span class="sxs-lookup"><span data-stu-id="7a5d3-143">**How do I update packages that are part of Visual Studio templates?**</span></span>

<span data-ttu-id="7a5d3-144">Git **güncelleştirmeleri** sekmesinde Paket Yöneticisi Arabiriminde ve seçin **Tümünü Güncelleştir**, veya [ `Update-Package` komutu](../Tools/ps-ref-update-package.md) Paket Yöneticisi Konsolu'ndan.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-144">Go to the **Updates** tab in the Package Manager UI and select **Update All**, or use the [`Update-Package` command](../Tools/ps-ref-update-package.md) from the Package Manager Console.</span></span>

<span data-ttu-id="7a5d3-145">Şablonu güncelleştirmek için şablon depo el ile güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-145">To update the template itself, you need to manually update the template repository.</span></span> <span data-ttu-id="7a5d3-146">Bkz: [Xavier Decoster'ın blogu](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) Bu konu hakkında.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-146">See [Xavier Decoster's blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) on this subject.</span></span> <span data-ttu-id="7a5d3-147">Tüm bağımlılıklarını en son sürümünü birbirleri ile uyumlu değilse el ile güncelleştirmeleri şablona bozulmasına neden olabilir çünkü bu, kendi risk yapılır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-147">Note that this is done at your own risk, because manual updates might corrupt the template if the latest version of all dependencies are not compatible with each other.</span></span>

<span data-ttu-id="7a5d3-148">**NuGet Visual Studio dışında kullanabilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="7a5d3-148">**Can I use NuGet outside of Visual Studio?**</span></span>

<span data-ttu-id="7a5d3-149">Evet, NuGet doğrudan komut satırından çalışır.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-149">Yes, NuGet works directly from the command line.</span></span> <span data-ttu-id="7a5d3-150">Bkz: [Yükleme Kılavuzu](../guides/install-nuget.md) ve [CLI başvuru](../tools/nuget-exe-CLI-Reference.md).</span><span class="sxs-lookup"><span data-stu-id="7a5d3-150">See the [Install guide](../guides/install-nuget.md) and the [CLI reference](../tools/nuget-exe-CLI-Reference.md).</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="7a5d3-151">NuGet komut satırı</span><span class="sxs-lookup"><span data-stu-id="7a5d3-151">NuGet command line</span></span>

<span data-ttu-id="7a5d3-152">**NuGet komut satırı aracının en son sürümünü nasıl sağlarım?**</span><span class="sxs-lookup"><span data-stu-id="7a5d3-152">**How do I get the latest version of NuGet command line tool?**</span></span>

<span data-ttu-id="7a5d3-153">Bkz: [Yükleme Kılavuzu](../guides/install-nuget.md).</span><span class="sxs-lookup"><span data-stu-id="7a5d3-153">See the [Install guide](../guides/install-nuget.md).</span></span>

<span data-ttu-id="7a5d3-154">**Nuget.exe lisansını nedir?**</span><span class="sxs-lookup"><span data-stu-id="7a5d3-154">**What is the license for nuget.exe?**</span></span>

<span data-ttu-id="7a5d3-155">MIT lisans koşullarına nuget.exe yeniden dağıtmak için izin verilir.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-155">You are allowed to redistribute nuget.exe under the terms of the MIT license.</span></span> <span data-ttu-id="7a5d3-156">Güncelleştirme ve yeniden dağıtmak için seçtiğiniz nuget.exe tüm kopyalarını bakım sorumlu.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-156">You are responsible for updating and servicing any copies of nuget.exe that you choose to redistribute.</span></span>

<span data-ttu-id="7a5d3-157">**NuGet komut satırı aracı genişletmek mümkün mü?**</span><span class="sxs-lookup"><span data-stu-id="7a5d3-157">**Is it possible to extend the NuGet command line tool?**</span></span>

<span data-ttu-id="7a5d3-158">Evet, özel komut eklemek olası `nuget.exe`açıklandığı gibi [Ramiz Reynold'ın post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span><span class="sxs-lookup"><span data-stu-id="7a5d3-158">Yes, it's possible to add custom commands to `nuget.exe`, as described in [Rob Reynold's post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span></span>

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a><span data-ttu-id="7a5d3-159">NuGet Paket Yöneticisi Konsolu (Windows için Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="7a5d3-159">NuGet Package Manager Console (Visual Studio on Windows)</span></span>

<span data-ttu-id="7a5d3-160">**Paket Yöneticisi Konsolu'nda DTE nesneye erişimi nasıl sağlarım?**</span><span class="sxs-lookup"><span data-stu-id="7a5d3-160">**How do I get access to the DTE object in the Package Manager console?**</span></span>

<span data-ttu-id="7a5d3-161">Visual Studio Otomasyon nesne modeli en üst düzey nesnesinde DTE (geliştirme araçları ortamı) nesne adı verilir.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-161">The top-level object in the Visual Studio automation object model is called the DTE (Development Tools Environment) object.</span></span> <span data-ttu-id="7a5d3-162">Konsol bu adlı bir değişken üzerinden sağlar `$DTE`.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-162">The console provides this through a variable named `$DTE`.</span></span> <span data-ttu-id="7a5d3-163">Daha fazla bilgi için bkz: [Otomasyon modeline genel bakış](/visualstudio/extensibility/internals/automation-model-overview) Visual Studio genişletilebilirliğini belgelerinde.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-163">For more information, see [Automation Model Overview](/visualstudio/extensibility/internals/automation-model-overview) in the Visual Studio Extensibility documentation.</span></span>

<span data-ttu-id="7a5d3-164">**DTE2 türü $DTE değişkenine cast deneyin, ancak bir hata iletisi: "" EnvDTE80.DTE2"türü için EnvDTE.DTEClass" türündeki "EnvDTE.DTEClass" değeri dönüştürülemiyor. Ne oldu?**</span><span class="sxs-lookup"><span data-stu-id="7a5d3-164">**I try to cast the $DTE variable to the type DTE2, but I get an error: Cannot convert the "EnvDTE.DTEClass" value of type "EnvDTE.DTEClass" to type "EnvDTE80.DTE2". What's wrong?**</span></span>

<span data-ttu-id="7a5d3-165">Bu, PowerShell COM nesnesi ile nasıl etkileşim kurduğu ile bilinen bir sorundur.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-165">This is a known issue with how PowerShell interacts with a COM object.</span></span> <span data-ttu-id="7a5d3-166">Aşağıdakileri deneyin:</span><span class="sxs-lookup"><span data-stu-id="7a5d3-166">Try the following:</span></span>

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

<span data-ttu-id="7a5d3-167">`Get-Interface`yardımcı işlevi NuGet PowerShell ana bilgisayar tarafından eklenir.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-167">`Get-Interface` is a helper function added by the NuGet PowerShell host.</span></span>

## <a name="creating-and-publishing-packages"></a><span data-ttu-id="7a5d3-168">Oluşturma ve paketleri yayımlama</span><span class="sxs-lookup"><span data-stu-id="7a5d3-168">Creating and publishing packages</span></span>

<span data-ttu-id="7a5d3-169">**Bir akış my paketinde nasıl listesinde?**</span><span class="sxs-lookup"><span data-stu-id="7a5d3-169">**How do I list my package in a feed?**</span></span>

<span data-ttu-id="7a5d3-170">Bkz: [oluşturma ve yayımlama bir paketi](../quickstart/create-and-publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="7a5d3-170">See [Creating and publishing a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="7a5d3-171">**.NET Framework'ün farklı sürümlerini hedefleyen birden fazla sürümünü Kitaplığı'mdan var. Bunu destekleyen tek bir paket nasıl oluşturulacağına?**</span><span class="sxs-lookup"><span data-stu-id="7a5d3-171">**I have multiple versions of my library that target different versions of the .NET Framework. How do I build a single package that supports this?**</span></span>

<span data-ttu-id="7a5d3-172">Bkz: [birden çok .NET Framework sürümleri ve profillerini destekleyen](../create-packages/supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="7a5d3-172">See [Supporting Multiple .NET Framework Versions and Profiles](../create-packages/supporting-multiple-target-frameworks.md).</span></span>

<span data-ttu-id="7a5d3-173">**Kendi deposu veya akış nasıl ayarlarım?**</span><span class="sxs-lookup"><span data-stu-id="7a5d3-173">**How do I set up my own repository or feed?**</span></span>

<span data-ttu-id="7a5d3-174">Bkz: [paketleri genel bakış barındırma](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="7a5d3-174">See the [Hosting packages overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="7a5d3-175">**Nasıl ı toplu olarak akış my NuGet paketleri yükleyebilir?**</span><span class="sxs-lookup"><span data-stu-id="7a5d3-175">**How can I upload packages to my NuGet feed in bulk?**</span></span>

<span data-ttu-id="7a5d3-176">Bkz: [toplu NuGet paketleri yayımlama](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span><span class="sxs-lookup"><span data-stu-id="7a5d3-176">See [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span></span>

## <a name="working-with-packages"></a><span data-ttu-id="7a5d3-177">Paketleri ile çalışma</span><span class="sxs-lookup"><span data-stu-id="7a5d3-177">Working with packages</span></span>

<span data-ttu-id="7a5d3-178">**Proje düzeyi paketi ve bir çözüm düzeyi paketi arasındaki fark nedir?**</span><span class="sxs-lookup"><span data-stu-id="7a5d3-178">**What is the difference between a project-level package and a solution-level package?**</span></span>

<span data-ttu-id="7a5d3-179">Bir çözüm düzeyi paketi (NuGet 3.x+) bir çözümde yalnızca bir kez yüklenir ve ardından Çözümdeki tüm projeleri için kullanılabilir hale gelir.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-179">A solution-level package (NuGet 3.x+) is installed only once in a solution and is then available for all projects in the solution.</span></span> <span data-ttu-id="7a5d3-180">Proje düzeyi paketi kullandığı her projede yüklü.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-180">A project-level package is installed in each project that uses it.</span></span> <span data-ttu-id="7a5d3-181">Bir çözüm düzeyi paket gelen paket Yöneticisi konsolu çağrılabilen yeni komutları da yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-181">A solution-level package might also install new commands that can be called from within the Package Manager Console.</span></span>

<span data-ttu-id="7a5d3-182">**Internet bağlantısı olmadan NuGet paketlerini yüklemek mümkün mü?**</span><span class="sxs-lookup"><span data-stu-id="7a5d3-182">**Is it possible to install NuGet packages without Internet connectivity?**</span></span>

<span data-ttu-id="7a5d3-183">Evet, Scott Hanselman'ın Blog Gönderisi bkz [NuGet nuget.org aşağı (veya üzerinde bir düzlemi olduğunuz olduğunda) erişmek nasıl](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span><span class="sxs-lookup"><span data-stu-id="7a5d3-183">Yes, see Scott Hanselman's Blog post [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span></span>

<span data-ttu-id="7a5d3-184">**Varsayılan paket klasöründen farklı bir konumda paketleri nasıl yüklerim?**</span><span class="sxs-lookup"><span data-stu-id="7a5d3-184">**How do I install packages in a different location from the default packages folder?**</span></span>

<span data-ttu-id="7a5d3-185">Ayarlama [ `repositoryPath` ](../Schema/nuget-config-file.md#config-section) ayarı `Nuget.Config` kullanarak `nuget config -set repositoryPath=<path>`.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-185">Set the [`repositoryPath`](../Schema/nuget-config-file.md#config-section) setting in `Nuget.Config` using `nuget config -set repositoryPath=<path>`.</span></span>

<span data-ttu-id="7a5d3-186">**NuGet paketleri klasörüne kaynak denetimine ekleme nasıl kaçının?**</span><span class="sxs-lookup"><span data-stu-id="7a5d3-186">**How do I avoid adding the NuGet packages folder into to source control?**</span></span>

<span data-ttu-id="7a5d3-187">Ayarlama [ `disableSourceControlIntegration` ](../Schema/nuget-config-file.md#solution-section) içinde `Nuget.Config` için `true`.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-187">Set the [`disableSourceControlIntegration`](../Schema/nuget-config-file.md#solution-section) in `Nuget.Config` to `true`.</span></span> <span data-ttu-id="7a5d3-188">Çözüm, bu anahtar çalışır düzeyde ve bu nedenle gereksinim eklenecek `$(Solutiondir)\.nuget\Nuget.Config` dosya.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-188">This key works at the solution level and hence need to be added to the `$(Solutiondir)\.nuget\Nuget.Config` file.</span></span> <span data-ttu-id="7a5d3-189">Paket geri yüklemesi Visual Studio'dan etkinleştirme bu dosyayı otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-189">Enabling package restore from Visual Studio creates this file automatically.</span></span>

<span data-ttu-id="7a5d3-190">**Paket geri yükleme'yi nasıl kapatırım?**</span><span class="sxs-lookup"><span data-stu-id="7a5d3-190">**How do I turn off package restore?**</span></span>

<span data-ttu-id="7a5d3-191">Bkz: [etkinleştirme ve paket geri yüklemesi devre dışı bırakma](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="7a5d3-191">See [Enabling and disabling package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="7a5d3-192">**Neden alabilirim "bağımlılık hatası bir çözümlenemiyor" ne zaman uzaktan bağımlılıkları olan yerel bir paketi yükleniyor?**</span><span class="sxs-lookup"><span data-stu-id="7a5d3-192">**Why do I get an "Unable to resolve dependency error" when installing a local package with remote dependencies?**</span></span>

<span data-ttu-id="7a5d3-193">Seçmenize gerek **tüm** bir yerel paket projeye yüklerken kaynak.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-193">You need to select the **All** source when installing a local package into the project.</span></span> <span data-ttu-id="7a5d3-194">Bu yalnızca bir kullanmak yerine tüm akışları toplar.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-194">This aggregates all the feeds instead of using just one.</span></span> <span data-ttu-id="7a5d3-195">Bu hata görünür kullanıcıların yerel bir depo genellikle yanlışlıkla önlemek istediğiniz nedeni şirket nedeniyle uzak bir paket yükleme ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-195">The reason this error appears is that users of a local repository often want to avoid accidentally installing a remote package due to corporate polices.</span></span>

<span data-ttu-id="7a5d3-196">**Birden çok proje aynı klasörde sahibim, ayrı packages.config dosyaları her proje için nasıl kullanabilirim?**</span><span class="sxs-lookup"><span data-stu-id="7a5d3-196">**I have multiple projects in the same folder, how can I use separate packages.config files for each project?**</span></span>

<span data-ttu-id="7a5d3-197">NuGet tanımlayan gibi burada ayrı projeler Canlı ayrı klasörlerde çoğu projelerde, bu bir sorun teşkil etmez `packages.config` her proje dosyaları.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-197">In most projects where separate projects live in separate folders, this is not a problem as NuGet identifies the `packages.config` files in each project.</span></span> <span data-ttu-id="7a5d3-198">NuGet 3.3 + ve birden fazla ile projeleri ile aynı klasörde projeye adını ekleyebilirsiniz `packages.config` dosya adlarını kullanın düzeni `packages.{project-name}.config`, ve NuGet bu dosyasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-198">With NuGet 3.3+ and multiple projects in the same folder, you can insert the name of the project into the `packages.config` filenames use the pattern `packages.{project-name}.config`, and NuGet uses that file.</span></span>

<span data-ttu-id="7a5d3-199">Her proje dosyası bağımlılıkları kendi listesi içerdiğinden bu bir sorun PackageReference, kullanırken değildir.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-199">This is not an issue when using PackageReference, as each project file contains its own list of dependencies.</span></span>

<span data-ttu-id="7a5d3-200">**Nuget.org depoları my listede göremiyorum, nasıl geri sağlarım?**</span><span class="sxs-lookup"><span data-stu-id="7a5d3-200">**I don't see nuget.org in my list of repositories, how do I get it back?**</span></span>

- <span data-ttu-id="7a5d3-201">Ekleme `https://api.nuget.org/v3/index.json` kaynakları, listenize veya</span><span class="sxs-lookup"><span data-stu-id="7a5d3-201">Add `https://api.nuget.org/v3/index.json` to your list of sources, or</span></span>
- <span data-ttu-id="7a5d3-202">Silme `%appdata%\.nuget\NuGet.Config` ve yeniden oluşturun NuGet izin verin.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-202">Delete the `%appdata%\.nuget\NuGet.Config` and let NuGet re-create it.</span></span>

<span data-ttu-id="7a5d3-203">**Bir paketi belirli lisans bilgileri sağlamazsa koşulları varsayılan lisans nelerdir?**</span><span class="sxs-lookup"><span data-stu-id="7a5d3-203">**What are the default license terms if a package doesn't provide specific license information?**</span></span>

<span data-ttu-id="7a5d3-204">Her paket paketine dahil terimleri tabidir.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-204">Each package is governed by the terms that are included with the package.</span></span> <span data-ttu-id="7a5d3-205">Erişim, indirme ya da herhangi bir paket alınırken önce hüküm gözden geçirmelidir.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-205">You should review the applicable terms before accessing, downloading, or acquiring any packages.</span></span> <span data-ttu-id="7a5d3-206">Nuget.org üzerinde kullanmak **lisans bilgilerini** bağlantı paketi sayfasında.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-206">On nuget.org, use the **License Info** link on the package page.</span></span>

<span data-ttu-id="7a5d3-207">Bir paketi Lisans Koşulları'nı belirtmiyorsa kullanarak doğrudan paketi sahibine başvurun **sahipleri başvurun** nuget.org paketi sayfasında bağlantı.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-207">If a package does not specify the licensing terms, contact the package owner directly using the **Contact owners** link on the nuget.org package page.</span></span> <span data-ttu-id="7a5d3-208">Microsoft hiçbir fikri mülkiyet, üçüncü taraf paket sağlayıcılardan lisans değildir ve üçüncü taraflar tarafından sağlanan bilgileri sorumlu değildir.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-208">Microsoft does not license any intellectual property to you from third party package providers and is not responsible for information provided by third parties.</span></span>

## <a name="managing-packages-on-nugetorg"></a><span data-ttu-id="7a5d3-209">Nuget.org paketlerini yönetme</span><span class="sxs-lookup"><span data-stu-id="7a5d3-209">Managing packages on nuget.org</span></span>

<span data-ttu-id="7a5d3-210">**Paket meta verileri, karşıya yüklendikten sonra düzenleyebilir miyim? Neden nuspec düzenleme ve meta veri paketini değişiklik yapmak için yeni bir paket karşıya yükleme gerekiyor mu?**</span><span class="sxs-lookup"><span data-stu-id="7a5d3-210">**Can I edit package metadata after it's been uploaded? Why do you require editing the nuspec and uploading a new package for making changes to package metadata?**</span></span>

<span data-ttu-id="7a5d3-211">NuGet tüm paketler imzalanmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-211">NuGet requires all packages to be signed.</span></span> <span data-ttu-id="7a5d3-212">Paketin imzalanması bir tasarım prensibi imzalı paket içeriğini nuspec içeren değişmez, olmanızın gerekmesidir.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-212">A design principle of package signing is that signed package content must be immutable, which includes the nuspec.</span></span> <span data-ttu-id="7a5d3-213">Paket meta verileri düzenleme değişiklikleri varolan imza geçersiz kılmalarını nuspec için sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-213">Editing the package metadata results in changes to the nuspec, invalidating existing signatures.</span></span> <span data-ttu-id="7a5d3-214">Paket oluşturulduktan sonra paket meta verileri düzenleme gerektirmeyecek şekilde var olan iş akışları değiştirme öneririz.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-214">We recommend modifying existing workflows to not require editing the package metadata after the package has been created.</span></span>

<span data-ttu-id="7a5d3-215">Not paketiniz için listelenen bağımlılıkları paketinden otomatik olarak oluşturulur ve düzenlenemez.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-215">Note that dependencies listed for your package are generated automatically from the package itself and cannot be edited.</span></span>

<span data-ttu-id="7a5d3-216">Ayrıca, paketler karşıya [staging.nuget.org](http://staging.nuget.org) sınamak ve bir paket genel bir galeride kullanıma olmadan paketinizi doğrulamak için harika bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-216">In addition, uploading packages to [staging.nuget.org](http://staging.nuget.org) is a great way to test and validate your package without making a package available in the public gallery.</span></span>

<span data-ttu-id="7a5d3-217">**Gelecekte yayımlanacak paketler için adları ayırmak mümkün mü?**</span><span class="sxs-lookup"><span data-stu-id="7a5d3-217">**Is it possible to reserve names for packages that will be published in future?**</span></span>

<span data-ttu-id="7a5d3-218">Evet.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-218">Yes.</span></span> <span data-ttu-id="7a5d3-219">Üzerinde paketler için kimlikleri ayırabilirsiniz [nuget.org](https://www.nuget.org/) hesabınız için bir paket kimliği önek isteyen tarafından.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-219">You can reserve IDs for packages on [nuget.org](https://www.nuget.org/) by requesting a package ID prefix for your account.</span></span> <span data-ttu-id="7a5d3-220">Bir paket kimliği öneki istemek için (saat) paketi sahibi görünen adı ve istenen paket kimliği öneki ile nuget.org hesabı posta gönderin.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-220">In order to request a package ID prefix, send mail to account (at) nuget.org with the package owner display name, and the requested package ID prefix.</span></span>  

<span data-ttu-id="7a5d3-221">**Paketler için sahipliğini talep nasıl?**</span><span class="sxs-lookup"><span data-stu-id="7a5d3-221">**How do I claim ownership for packages ?**</span></span>

<span data-ttu-id="7a5d3-222">Bkz: [yönetme paket sahipleri nuget.org üzerinde](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="7a5d3-222">See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span>

<span data-ttu-id="7a5d3-223">**My yazılım lisansı ihlal eden bir paket sahibi ile nasıl ilgilenir?**</span><span class="sxs-lookup"><span data-stu-id="7a5d3-223">**How do I deal with a package owner who is violating my software license?**</span></span>

<span data-ttu-id="7a5d3-224">Paket sahipleri ve diğer yazılımların sahipleri arasında kaynaklanabilecek itirazları çözümlemek için birlikte çalışmak üzere NuGet topluluk öneririz.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-224">We encourage the NuGet community to work together to resolve any disputes that may arise between package owners and the owners of other software.</span></span> <span data-ttu-id="7a5d3-225">Biz hazırlanmış bir [itiraz çözümleme işlemi](../policies/dispute-resolution.md) nuget.org yöneticilerin intercede soran önce izlemek için.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-225">We have crafted a [dispute resolution process](../policies/dispute-resolution.md) to follow before asking nuget.org administrators to intercede.</span></span>

<span data-ttu-id="7a5d3-226">**My sınama paketlerini nuget.org için karşıya yükleme önerilir?**</span><span class="sxs-lookup"><span data-stu-id="7a5d3-226">**Is it recommended to upload my test packages to nuget.org?**</span></span>

<span data-ttu-id="7a5d3-227">Test amaçları için kullandığınız [staging.nuget.org](http://staging.nuget.org), veya alternatif ortak NuGet sunucularını [myget.org](https://myget.org) veya [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).</span><span class="sxs-lookup"><span data-stu-id="7a5d3-227">For test purposes, you can use [staging.nuget.org](http://staging.nuget.org), or alternative public NuGet servers like [myget.org](https://myget.org) or [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).</span></span>

<span data-ttu-id="7a5d3-228">Paketler için Staging.nuget.org karşıya korunmaz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-228">Note that packages uploaded to staging.nuget.org may not be preserved.</span></span> <span data-ttu-id="7a5d3-229">Bkz: [güle güle Önizleme](http://blog.nuget.org/20130419/goodbye-preview.html).</span><span class="sxs-lookup"><span data-stu-id="7a5d3-229">See [Goodbye preview](http://blog.nuget.org/20130419/goodbye-preview.html).</span></span>

<span data-ttu-id="7a5d3-230">**Paketler için nuget.org karşıya yükleyebilir en büyük boyutu nedir?**</span><span class="sxs-lookup"><span data-stu-id="7a5d3-230">**What is the maximum size of packages I can upload to nuget.org?**</span></span>

<span data-ttu-id="7a5d3-231">nuget.org sağlayan paketler en fazla 250MB, ancak paketleri birbirine bağlamak için bağımlılıkları kullanarak ve paketleri 1 MB'den mümkünse tutulması önerilir.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-231">nuget.org allows packages up to 250MB, but we recommend keeping packages under 1MB if possible and using dependencies to link packages together.</span></span> <span data-ttu-id="7a5d3-232">Altın kural, çakışmaları önlemek için yalnızca bir derleme paketleri içerir.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-232">As a rule of thumb, packages contain only one assembly to avoid collisions.</span></span>

<span data-ttu-id="7a5d3-233">NuGet paketleri, başarısız yükler olasılığı daha küçük olanları daha büyük paketleriniz varsa şekilde indirmek için HTTP kullanır.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-233">NuGet uses HTTP to download packages, so larger packages have a higher likelihood of failed installs than smaller ones.</span></span>

<span data-ttu-id="7a5d3-234">NuGet paketlerinizi Tüketiciler için toplam yükleme boyutunu küçülterek, birden çok paket arasındaki bağımlılıkları paylaşmak da mümkündür.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-234">It is possible to share dependencies between multiple packages, making the total download size for consumers of your NuGet packages smaller.</span></span>

<span data-ttu-id="7a5d3-235">Çoğunlukla statik ve hiçbir zaman değişikliği bağımlılıklardır.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-235">Dependencies are mostly static and never change.</span></span> <span data-ttu-id="7a5d3-236">Kodda bir hata düzeltme, bağımlılıkları güncelleştirilmesi gerekmeyebilir.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-236">When fixing a bug in code, the dependencies may not need to be updated.</span></span> <span data-ttu-id="7a5d3-237">Bağımlılıklar paketini, her zaman büyük paketler reshipping yukarı sonlandırın.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-237">If you bundle dependencies, you end up reshipping larger packages every time.</span></span> <span data-ttu-id="7a5d3-238">NuGet paketleri ilgili bağımlılıkları bölerek yükseltme paketinizi Tüketiciler için çok daha ayrıntılı sağlar.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-238">By splitting NuGet packages into related dependencies, upgrades are much more fine-grained for consumers of your package.</span></span>

## <a name="nugetorg-not-accessible"></a><span data-ttu-id="7a5d3-239">nuget.org erişilebilir değil</span><span class="sxs-lookup"><span data-stu-id="7a5d3-239">nuget.org not accessible</span></span>

<span data-ttu-id="7a5d3-240">**Neden paketleri indirme veya paketler için nuget.org karşıya?**</span><span class="sxs-lookup"><span data-stu-id="7a5d3-240">**Why can't I download packages from or upload packages to nuget.org?**</span></span>

<span data-ttu-id="7a5d3-241">Öncelikle, NuGet'ın en son sürümlerini kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-241">First, make sure you're using the latest versions of NuGet.</span></span> <span data-ttu-id="7a5d3-242">Bu sürüm başarısız olmaya devam ederse [desteğine başvurun](https://www.nuget.org/policies/Contact) ve sorun giderme bilgileri de dahil olmak üzere ek bağlantı sağlayın:</span><span class="sxs-lookup"><span data-stu-id="7a5d3-242">If that version continues to fail, [contact support](https://www.nuget.org/policies/Contact) and provide additional connection troubleshooting information including:</span></span>

- <span data-ttu-id="7a5d3-243">Kullanmakta olduğunuz NuGet sürümü</span><span class="sxs-lookup"><span data-stu-id="7a5d3-243">The version of NuGet you're using</span></span>
- <span data-ttu-id="7a5d3-244">Kullanmakta olduğunuz paket kaynaklarını</span><span class="sxs-lookup"><span data-stu-id="7a5d3-244">The package sources you're using</span></span>
- <span data-ttu-id="7a5d3-245">Ayrıntılı ayrıntı düzeyine sahip bir geri yükleme günlüğü</span><span class="sxs-lookup"><span data-stu-id="7a5d3-245">A restore log with detailed verbosity</span></span>
- <span data-ttu-id="7a5d3-246">MTR veya Fiddler izlemeleri (aşağıya bakın)</span><span class="sxs-lookup"><span data-stu-id="7a5d3-246">MTR or a Fiddler traces (see below)</span></span>
- <span data-ttu-id="7a5d3-247">Coğrafi konuma</span><span class="sxs-lookup"><span data-stu-id="7a5d3-247">Your geographical area</span></span>
- <span data-ttu-id="7a5d3-248">İşletim sistemi sürümü</span><span class="sxs-lookup"><span data-stu-id="7a5d3-248">Your operating system version</span></span>
- <span data-ttu-id="7a5d3-249">Makine Yapılandırma (CPU, ağ, sabit sürücü)</span><span class="sxs-lookup"><span data-stu-id="7a5d3-249">Machine configuration (CPU, Network, hard drive)</span></span>
- <span data-ttu-id="7a5d3-250">Makinenizde bir proxy veya güvenlik duvarı arkasında olup</span><span class="sxs-lookup"><span data-stu-id="7a5d3-250">Whether is your machine behind a proxy or firewall</span></span>
- <span data-ttu-id="7a5d3-251">Makinede yüklü .NET sürümlerini</span><span class="sxs-lookup"><span data-stu-id="7a5d3-251">The versions of .NET that are installed on the machine</span></span>
- <span data-ttu-id="7a5d3-252">Platformlar arası araçlarının .NET CLI ya da kullandığınız DNU gibi sürümleri</span><span class="sxs-lookup"><span data-stu-id="7a5d3-252">Versions of cross-platform tools such as .NET CLI, or DNU that you're using</span></span>

<span data-ttu-id="7a5d3-253">*MTR yakalamak için:*</span><span class="sxs-lookup"><span data-stu-id="7a5d3-253">*To capture MTR:*</span></span>

- <span data-ttu-id="7a5d3-254">Gelen WinMTR karşıdan [http://winmtr.net/download/](http://winmtr.net/)</span><span class="sxs-lookup"><span data-stu-id="7a5d3-254">Download WinMTR from [http://winmtr.net/download/](http://winmtr.net/)</span></span>
- <span data-ttu-id="7a5d3-255">Girin `api.nuget.org` tıklatın ve ana bilgisayar adı olarak **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-255">Enter `api.nuget.org` as the hostname and click **Start**.</span></span>
- <span data-ttu-id="7a5d3-256">Bekle **gönderilen** sütunu > = 100.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-256">Wait until the **Sent** column is >= 100.</span></span>

    ![MTR yakalama](media/mtr.png)

- <span data-ttu-id="7a5d3-258">Metni panoya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-258">Copy text to clipboard.</span></span>

<span data-ttu-id="7a5d3-259">*Fiddler yakalamak için:*</span><span class="sxs-lookup"><span data-stu-id="7a5d3-259">*To capture Fiddler:*</span></span>

- <span data-ttu-id="7a5d3-260">En son sürümünü yüklemek [Fiddler](http://www.telerik.com/download/fiddler).</span><span class="sxs-lookup"><span data-stu-id="7a5d3-260">Install the latest version of [Fiddler](http://www.telerik.com/download/fiddler).</span></span>
- <span data-ttu-id="7a5d3-261">Fiddler'ı başlatın ve yakalama trafiği kullanılarak devre dışı bırakma **Dosya > trafiği Yakala** menüsü.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-261">Start Fiddler and disable capturing traffic using the **File > Capture Traffic** menu.</span></span>
- <span data-ttu-id="7a5d3-262">Tüm oturumları kaldırın (tüm öğeleri listesinde, basın seçme **silmek** anahtar).</span><span class="sxs-lookup"><span data-stu-id="7a5d3-262">Remove all sessions (select all items in the list, press the **Delete** key).</span></span>
- <span data-ttu-id="7a5d3-263">HTTPS trafiğini denetleyerek yakalamak için fiddler'ı yapılandırma **şifresini HTTPS trafiği** içinde **HTTPS** sekmesinde **Araçlar > Fiddler seçenekleri...**  menüsü.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-263">Configure Fiddler to capture HTTPS traffic by checking **Decrypt HTTPS traffic** in the **HTTPS** tab of the **Tools > Fiddler Options...** menu.</span></span>
- <span data-ttu-id="7a5d3-264">Visual Studio’yu kapatın.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-264">Close Visual Studio.</span></span>
- <span data-ttu-id="7a5d3-265">Etkinleştirme **Dosya > trafiği Yakala** menüsü.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-265">Enable the **File > Capture Traffic** menu.</span></span>
- <span data-ttu-id="7a5d3-266">Visual Studio ya da nuget.exe .exe başlatmak ve çalışmıyor eylemleri gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-266">Start Visual Studio or nuget.exe .exe and perform the actions that are not working.</span></span> <span data-ttu-id="7a5d3-267">Bu eylemleri tarafından oluşturulan trafiğin Fiddler'da göstermelidir.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-267">The traffic generated by these actions should show up in Fiddler.</span></span>
- <span data-ttu-id="7a5d3-268">Eylemler çalıştırdıktan sonra kullanmak **Dosya > Kaydet > tüm oturumları** yakalanan oturumları depolamak için.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-268">Once the actions have run, use **File > Save > All Sessions** to store the captured sessions.</span></span>

<span data-ttu-id="7a5d3-269">Not: Bunu ayarlamak için gerekli olabilecek `HTTP_PROXY` ortam değişkenine `http://127.0.0.1:8888` Fiddler aracılığıyla yönlendirme NuGet trafiği için.</span><span class="sxs-lookup"><span data-stu-id="7a5d3-269">Note: it may be required to set the `HTTP_PROXY` environment variable to `http://127.0.0.1:8888` for routing NuGet traffic through Fiddler.</span></span>

<span data-ttu-id="7a5d3-270">Başarısız olursa, deneyin [bu StackOverflow postasında belirtilen ipuçları](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).</span><span class="sxs-lookup"><span data-stu-id="7a5d3-270">If that fails, try the [tips mentioned in this StackOverflow post](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).</span></span>

<span data-ttu-id="7a5d3-271">**Nuget.org için API uç noktaları nelerdir?**</span><span class="sxs-lookup"><span data-stu-id="7a5d3-271">**What are the API endpoints for nuget.org?**</span></span>

<span data-ttu-id="7a5d3-272">V3: `https://api.nuget.org/v3/index.json` V2: `https://www.nuget.org/api/v2/` (V2 API kullanım dışıdır ve NuGet ile 4 + çalışmaz unutmayın.)</span><span class="sxs-lookup"><span data-stu-id="7a5d3-272">V3: `https://api.nuget.org/v3/index.json` V2: `https://www.nuget.org/api/v2/` (Note that the V2 API is deprecated and does not work with NuGet 4+.)</span></span>
