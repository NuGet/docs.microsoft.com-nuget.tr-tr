---
title: Sık sorulan-sorular NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/11/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Ortak sorular ve yanıtlar NuGet komut satırında ve Visual Studio kullanarak ve NuGet Galerisi ile çalışmak için.
keywords: NuGet soru- cevap, sorular ve yanıtlar, ortak sorunları, NuGet sürümleri, sürüm paketi
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 33e4776054b1cdd874dcd7e955552ef873dbbf5b
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-frequently-asked-questions"></a><span data-ttu-id="16a25-104">NuGet sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="16a25-104">NuGet frequently-asked questions</span></span>

<span data-ttu-id="16a25-105">**NuGet çalıştırmak için gereken nedir?**</span><span class="sxs-lookup"><span data-stu-id="16a25-105">**What is required to run NuGet?**</span></span>

<span data-ttu-id="16a25-106">Kullanıcı Arabirimi ve komut satırı araçları geçici tüm bilgileri kullanılabilir [Yükleme Kılavuzu](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="16a25-106">All the information around both UI and command-line tools is available in the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="16a25-107">**NuGet Mono destekliyor mu?**</span><span class="sxs-lookup"><span data-stu-id="16a25-107">**Does NuGet support Mono?**</span></span>

<span data-ttu-id="16a25-108">Komut satırı aracı `nuget.exe`, oluşturur ve Mono altında 3.2 + çalıştırır ve paketleri Mono olarak oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="16a25-108">The command-line tool, `nuget.exe`, builds and runs under Mono 3.2+ and can create packages in Mono.</span></span>

<span data-ttu-id="16a25-109">Ancak `nuget.exe` çalışır tam olarak Windows, bilinen sorunlar vardır Linux ve OS x bakın [Mono sorunları](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) github'da.</span><span class="sxs-lookup"><span data-stu-id="16a25-109">Although `nuget.exe` works fully on Windows, there are known issues on Linux and OS X. Refer to [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) on GitHub.</span></span>

<span data-ttu-id="16a25-110">A [grafik istemci](https://github.com/mrward/monodevelop-nuget-addin) MonoDevelop için bir eklenti olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="16a25-110">A [graphical client](https://github.com/mrward/monodevelop-nuget-addin) is available as an add-in for MonoDevelop.</span></span>

<span data-ttu-id="16a25-111">**Ne bir paket içerir ve kararlı ve Uygulamam için yararlı olup nasıl belirleyebilirim?**</span><span class="sxs-lookup"><span data-stu-id="16a25-111">**How can I determine what a package contains and whether it's stable and useful for my application?**</span></span>

<span data-ttu-id="16a25-112">Birincil bir paketi hakkında bilgi almak için kendi nuget.org listeleme sayfasında kaynağıdır (veya başka bir özel akış).</span><span class="sxs-lookup"><span data-stu-id="16a25-112">The primary source for learning about a package is its listing page on nuget.org (or another private feed).</span></span> <span data-ttu-id="16a25-113">Her bir paket nuget.org sayfasında paketi, sürüm geçmişi ve kullanım istatistiklerini açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="16a25-113">Each package page on nuget.org includes a description of the package, its version history, and usage statistics.</span></span> <span data-ttu-id="16a25-114">**Bilgisi** paketi sayfasında bölüm ayrıca projenin web genellikle bulabileceğiniz birçok örnekler ve paket nasıl kullanıldığını öğrenmenize yardımcı olacak diğer belgelerin siteye bir bağlantı içerir.</span><span class="sxs-lookup"><span data-stu-id="16a25-114">The **Info** section on the package page also contains a link to the project's web site where you typically find many examples and other documentation to help you learn how the package is used.</span></span>

<span data-ttu-id="16a25-115">Daha fazla bilgi için bkz: [bulma ve paketleri seçme](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="16a25-115">For more information, see [Finding and choosing packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="nuget-in-visual-studio"></a><span data-ttu-id="16a25-116">Visual Studio'da NuGet</span><span class="sxs-lookup"><span data-stu-id="16a25-116">NuGet in Visual Studio</span></span>

<span data-ttu-id="16a25-117">**Nasıl NuGet farklı Visual Studio ürünlerinde destekleniyor mu?**</span><span class="sxs-lookup"><span data-stu-id="16a25-117">**How is NuGet supported in different Visual Studio products?**</span></span>

- <span data-ttu-id="16a25-118">Visual Studio Windows destekler [Paket Yöneticisi kullanıcı Arabirimi](../tools/package-manager-ui.md) ve [Paket Yöneticisi Konsolu](../tools/package-manager-console.md).</span><span class="sxs-lookup"><span data-stu-id="16a25-118">Visual Studio on Windows supports the [Package Manager UI](../tools/package-manager-ui.md) and the [Package Manager Console](../tools/package-manager-console.md).</span></span>
- <span data-ttu-id="16a25-119">Mac için Visual Studio açıklandığı gibi yerleşik NuGet özellikleri olan [dahil olmak üzere bir NuGet paketini projenize](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="16a25-119">Visual Studio for Mac has built-in NuGet capabilities as described on [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>
- <span data-ttu-id="16a25-120">Visual Studio Code (tüm platformlar) doğrudan herhangi NuGet tümleştirme yok.</span><span class="sxs-lookup"><span data-stu-id="16a25-120">Visual Studio Code (all platforms) does not have any direct NuGet integration.</span></span> <span data-ttu-id="16a25-121">Kullanım [NuGet CLI](../tools/nuget-exe-cli-reference.md) veya [dotnet CLI](../tools/dotnet-commands.md).</span><span class="sxs-lookup"><span data-stu-id="16a25-121">Use the [NuGet CLI](../tools/nuget-exe-cli-reference.md) or the [dotnet CLI](../tools/dotnet-commands.md).</span></span>
- <span data-ttu-id="16a25-122">Visual Studio Team Services sağlar [NuGet paketlerini geri yüklemek için bir derleme adımı](/vsts/build-release/tasks/package/nuget).</span><span class="sxs-lookup"><span data-stu-id="16a25-122">Visual Studio Team Services provides [a build step to restore NuGet packages](/vsts/build-release/tasks/package/nuget).</span></span> <span data-ttu-id="16a25-123">Ayrıca [konak özel NuGet paketi akışları Team Services](https://www.visualstudio.com/docs/package/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="16a25-123">You can also [host private NuGet package feeds on Team Services](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

<span data-ttu-id="16a25-124">**Yüklü olan NuGet Araçlar'ün tam sürümünü nasıl kontrol edilsin mi?**</span><span class="sxs-lookup"><span data-stu-id="16a25-124">**How do I check the exact version of the NuGet tools that are installed?**</span></span>

<span data-ttu-id="16a25-125">Visual Studio'da kullanın **Yardım > Microsoft Visual Studio hakkında** komut ve yanında görüntülenen sürümünde arayın **NuGet Paket Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="16a25-125">In Visual Studio, use the **Help > About Microsoft Visual Studio** command and look at the version displayed next to **NuGet Package Manager**.</span></span>

<span data-ttu-id="16a25-126">Alternatif olarak, Paket Yöneticisi konsolu başlatın (**Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Konsolu**) ve girin `$host` NuGet sürümü de dahil olmak üzere hakkındaki bilgileri görmek için.</span><span class="sxs-lookup"><span data-stu-id="16a25-126">Alternatively, launch the Package Manager Console (**Tools > NuGet Package Manager > Package Manager Console**) and enter `$host` to see information about NuGet including the version.</span></span>

<span data-ttu-id="16a25-127">**Hangi programlama dillerini NuGet tarafından destekleniyor mu?**</span><span class="sxs-lookup"><span data-stu-id="16a25-127">**What programming languages are supported by NuGet?**</span></span>

<span data-ttu-id="16a25-128">NuGet genellikle .NET diller için kullanılabilir ve .NET kitaplıkları bir projeye duruma getirmek için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="16a25-128">NuGet generally works for .NET languages and is designed to bring .NET libraries into a project.</span></span> <span data-ttu-id="16a25-129">Ayrıca bazı proje türleri MSBuild ve Visual Studio Otomasyon desteklediği için diğer projeler ve çeşitli derece dilleri de destekler.</span><span class="sxs-lookup"><span data-stu-id="16a25-129">Because it also supports MSBuild and Visual Studio automation in some project types, it also supports other projects and languages to various degrees.</span></span>

<span data-ttu-id="16a25-130">C#, Visual Basic, F #, WiX ve C++ NuGet en son sürümünü destekler.</span><span class="sxs-lookup"><span data-stu-id="16a25-130">The most recent version of NuGet supports C#, Visual Basic, F#, WiX, and C++.</span></span>

<span data-ttu-id="16a25-131">**Hangi proje şablonları NuGet tarafından destekleniyor mu?**</span><span class="sxs-lookup"><span data-stu-id="16a25-131">**What project templates are supported by NuGet?**</span></span>

<span data-ttu-id="16a25-132">NuGet proje şablonları Windows, Web, bulut, SharePoint, Wix vb. gibi çeşitli için tam destek vardır.</span><span class="sxs-lookup"><span data-stu-id="16a25-132">NuGet has full support for a variety of project templates like Windows, Web, Cloud, SharePoint, Wix, and so on.</span></span>

<span data-ttu-id="16a25-133">**Visual Studio şablonları parçası olan paketleri nasıl güncelleştiririm?**</span><span class="sxs-lookup"><span data-stu-id="16a25-133">**How do I update packages that are part of Visual Studio templates?**</span></span>

<span data-ttu-id="16a25-134">Git **güncelleştirmeleri** sekmesinde Paket Yöneticisi Arabiriminde ve seçin **Tümünü Güncelleştir**, veya [ `Update-Package` komutu](../tools/ps-ref-update-package.md) Paket Yöneticisi Konsolu'ndan.</span><span class="sxs-lookup"><span data-stu-id="16a25-134">Go to the **Updates** tab in the Package Manager UI and select **Update All**, or use the [`Update-Package` command](../tools/ps-ref-update-package.md) from the Package Manager Console.</span></span>

<span data-ttu-id="16a25-135">Şablonu güncelleştirmek için şablon depo el ile güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="16a25-135">To update the template itself, you need to manually update the template repository.</span></span> <span data-ttu-id="16a25-136">Bkz: [Xavier Decoster'ın blogu](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) Bu konu hakkında.</span><span class="sxs-lookup"><span data-stu-id="16a25-136">See [Xavier Decoster's blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) on this subject.</span></span> <span data-ttu-id="16a25-137">Tüm bağımlılıklarını en son sürümünü birbirleri ile uyumlu değilse el ile güncelleştirmeleri şablona bozulmasına neden olabilir çünkü bu, kendi risk yapılır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="16a25-137">Note that this is done at your own risk, because manual updates might corrupt the template if the latest version of all dependencies are not compatible with each other.</span></span>

<span data-ttu-id="16a25-138">**NuGet Visual Studio dışında kullanabilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="16a25-138">**Can I use NuGet outside of Visual Studio?**</span></span>

<span data-ttu-id="16a25-139">Evet, NuGet doğrudan komut satırından çalışır.</span><span class="sxs-lookup"><span data-stu-id="16a25-139">Yes, NuGet works directly from the command line.</span></span> <span data-ttu-id="16a25-140">Bkz: [Yükleme Kılavuzu](../install-nuget-client-tools.md) ve [CLI başvuru](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="16a25-140">See the [Install guide](../install-nuget-client-tools.md) and the [CLI reference](../tools/nuget-exe-cli-reference.md).</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="16a25-141">NuGet komut satırı</span><span class="sxs-lookup"><span data-stu-id="16a25-141">NuGet command line</span></span>

<span data-ttu-id="16a25-142">**NuGet komut satırı aracının en son sürümünü nasıl sağlarım?**</span><span class="sxs-lookup"><span data-stu-id="16a25-142">**How do I get the latest version of NuGet command line tool?**</span></span>

<span data-ttu-id="16a25-143">Bkz: [Yükleme Kılavuzu](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="16a25-143">See the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="16a25-144">**Nuget.exe lisansını nedir?**</span><span class="sxs-lookup"><span data-stu-id="16a25-144">**What is the license for nuget.exe?**</span></span>

<span data-ttu-id="16a25-145">MIT lisans koşullarına nuget.exe yeniden dağıtmak için izin verilir.</span><span class="sxs-lookup"><span data-stu-id="16a25-145">You are allowed to redistribute nuget.exe under the terms of the MIT license.</span></span> <span data-ttu-id="16a25-146">Güncelleştirme ve yeniden dağıtmak için seçtiğiniz nuget.exe tüm kopyalarını bakım sorumlu.</span><span class="sxs-lookup"><span data-stu-id="16a25-146">You are responsible for updating and servicing any copies of nuget.exe that you choose to redistribute.</span></span>

<span data-ttu-id="16a25-147">**NuGet komut satırı aracı genişletmek mümkün mü?**</span><span class="sxs-lookup"><span data-stu-id="16a25-147">**Is it possible to extend the NuGet command line tool?**</span></span>

<span data-ttu-id="16a25-148">Evet, özel komut eklemek olası `nuget.exe`açıklandığı gibi [Ramiz Reynold'ın post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span><span class="sxs-lookup"><span data-stu-id="16a25-148">Yes, it's possible to add custom commands to `nuget.exe`, as described in [Rob Reynold's post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span></span>

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a><span data-ttu-id="16a25-149">NuGet Paket Yöneticisi Konsolu (Windows için Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="16a25-149">NuGet Package Manager Console (Visual Studio on Windows)</span></span>

<span data-ttu-id="16a25-150">**Paket Yöneticisi Konsolu'nda DTE nesneye erişimi nasıl sağlarım?**</span><span class="sxs-lookup"><span data-stu-id="16a25-150">**How do I get access to the DTE object in the Package Manager console?**</span></span>

<span data-ttu-id="16a25-151">Visual Studio Otomasyon nesne modeli en üst düzey nesnesinde DTE (geliştirme araçları ortamı) nesne adı verilir.</span><span class="sxs-lookup"><span data-stu-id="16a25-151">The top-level object in the Visual Studio automation object model is called the DTE (Development Tools Environment) object.</span></span> <span data-ttu-id="16a25-152">Konsol bu adlı bir değişken üzerinden sağlar `$DTE`.</span><span class="sxs-lookup"><span data-stu-id="16a25-152">The console provides this through a variable named `$DTE`.</span></span> <span data-ttu-id="16a25-153">Daha fazla bilgi için bkz: [Otomasyon modeline genel bakış](/visualstudio/extensibility/internals/automation-model-overview) Visual Studio genişletilebilirliğini belgelerinde.</span><span class="sxs-lookup"><span data-stu-id="16a25-153">For more information, see [Automation Model Overview](/visualstudio/extensibility/internals/automation-model-overview) in the Visual Studio Extensibility documentation.</span></span>

<span data-ttu-id="16a25-154">**DTE2 türü $DTE değişkenine cast deneyin, ancak bir hata iletisi: "" EnvDTE80.DTE2"türü için EnvDTE.DTEClass" türündeki "EnvDTE.DTEClass" değeri dönüştürülemiyor. Ne oldu?**</span><span class="sxs-lookup"><span data-stu-id="16a25-154">**I try to cast the $DTE variable to the type DTE2, but I get an error: Cannot convert the "EnvDTE.DTEClass" value of type "EnvDTE.DTEClass" to type "EnvDTE80.DTE2". What's wrong?**</span></span>

<span data-ttu-id="16a25-155">Bu, PowerShell COM nesnesi ile nasıl etkileşim kurduğu ile bilinen bir sorundur.</span><span class="sxs-lookup"><span data-stu-id="16a25-155">This is a known issue with how PowerShell interacts with a COM object.</span></span> <span data-ttu-id="16a25-156">Aşağıdakileri deneyin:</span><span class="sxs-lookup"><span data-stu-id="16a25-156">Try the following:</span></span>

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

<span data-ttu-id="16a25-157">`Get-Interface` yardımcı işlevi NuGet PowerShell ana bilgisayar tarafından eklenir.</span><span class="sxs-lookup"><span data-stu-id="16a25-157">`Get-Interface` is a helper function added by the NuGet PowerShell host.</span></span>

## <a name="creating-and-publishing-packages"></a><span data-ttu-id="16a25-158">Oluşturma ve paketleri yayımlama</span><span class="sxs-lookup"><span data-stu-id="16a25-158">Creating and publishing packages</span></span>

<span data-ttu-id="16a25-159">**Bir akış my paketinde nasıl listesinde?**</span><span class="sxs-lookup"><span data-stu-id="16a25-159">**How do I list my package in a feed?**</span></span>

<span data-ttu-id="16a25-160">Bkz: [oluşturma ve yayımlama bir paketi](../quickstart/create-and-publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="16a25-160">See [Creating and publishing a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="16a25-161">**.NET Framework'ün farklı sürümlerini hedefleyen birden fazla sürümünü Kitaplığı'mdan var. Bunu destekleyen tek bir paket nasıl oluşturulacağına?**</span><span class="sxs-lookup"><span data-stu-id="16a25-161">**I have multiple versions of my library that target different versions of the .NET Framework. How do I build a single package that supports this?**</span></span>

<span data-ttu-id="16a25-162">Bkz: [birden çok .NET Framework sürümleri ve profillerini destekleyen](../create-packages/supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="16a25-162">See [Supporting Multiple .NET Framework Versions and Profiles](../create-packages/supporting-multiple-target-frameworks.md).</span></span>

<span data-ttu-id="16a25-163">**Kendi deposu veya akış nasıl ayarlarım?**</span><span class="sxs-lookup"><span data-stu-id="16a25-163">**How do I set up my own repository or feed?**</span></span>

<span data-ttu-id="16a25-164">Bkz: [paketleri genel bakış barındırma](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="16a25-164">See the [Hosting packages overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="16a25-165">**Nasıl ı toplu olarak akış my NuGet paketleri yükleyebilir?**</span><span class="sxs-lookup"><span data-stu-id="16a25-165">**How can I upload packages to my NuGet feed in bulk?**</span></span>

<span data-ttu-id="16a25-166">Bkz: [toplu NuGet paketleri yayımlama](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span><span class="sxs-lookup"><span data-stu-id="16a25-166">See [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span></span>

## <a name="working-with-packages"></a><span data-ttu-id="16a25-167">Paketleri ile çalışma</span><span class="sxs-lookup"><span data-stu-id="16a25-167">Working with packages</span></span>

<span data-ttu-id="16a25-168">**Proje düzeyi paketi ve bir çözüm düzeyi paketi arasındaki fark nedir?**</span><span class="sxs-lookup"><span data-stu-id="16a25-168">**What is the difference between a project-level package and a solution-level package?**</span></span>

<span data-ttu-id="16a25-169">Bir çözüm düzeyi paketi (NuGet 3.x+) bir çözümde yalnızca bir kez yüklenir ve ardından Çözümdeki tüm projeleri için kullanılabilir hale gelir.</span><span class="sxs-lookup"><span data-stu-id="16a25-169">A solution-level package (NuGet 3.x+) is installed only once in a solution and is then available for all projects in the solution.</span></span> <span data-ttu-id="16a25-170">Proje düzeyi paketi kullandığı her projede yüklü.</span><span class="sxs-lookup"><span data-stu-id="16a25-170">A project-level package is installed in each project that uses it.</span></span> <span data-ttu-id="16a25-171">Bir çözüm düzeyi paket gelen paket Yöneticisi konsolu çağrılabilen yeni komutları da yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="16a25-171">A solution-level package might also install new commands that can be called from within the Package Manager Console.</span></span>

<span data-ttu-id="16a25-172">**Internet bağlantısı olmadan NuGet paketlerini yüklemek mümkün mü?**</span><span class="sxs-lookup"><span data-stu-id="16a25-172">**Is it possible to install NuGet packages without Internet connectivity?**</span></span>

<span data-ttu-id="16a25-173">Evet, Scott Hanselman'ın Blog Gönderisi bkz [NuGet nuget.org aşağı (veya üzerinde bir düzlemi olduğunuz olduğunda) erişmek nasıl](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span><span class="sxs-lookup"><span data-stu-id="16a25-173">Yes, see Scott Hanselman's Blog post [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span></span>

<span data-ttu-id="16a25-174">**Varsayılan paket klasöründen farklı bir konumda paketleri nasıl yüklerim?**</span><span class="sxs-lookup"><span data-stu-id="16a25-174">**How do I install packages in a different location from the default packages folder?**</span></span>

<span data-ttu-id="16a25-175">Ayarlama [ `repositoryPath` ](../reference/nuget-config-file.md#config-section) ayarı `Nuget.Config` kullanarak `nuget config -set repositoryPath=<path>`.</span><span class="sxs-lookup"><span data-stu-id="16a25-175">Set the [`repositoryPath`](../reference/nuget-config-file.md#config-section) setting in `Nuget.Config` using `nuget config -set repositoryPath=<path>`.</span></span>

<span data-ttu-id="16a25-176">**NuGet paketleri klasörüne kaynak denetimine ekleme nasıl kaçının?**</span><span class="sxs-lookup"><span data-stu-id="16a25-176">**How do I avoid adding the NuGet packages folder into to source control?**</span></span>

<span data-ttu-id="16a25-177">Ayarlama [ `disableSourceControlIntegration` ](../reference/nuget-config-file.md#solution-section) içinde `Nuget.Config` için `true`.</span><span class="sxs-lookup"><span data-stu-id="16a25-177">Set the [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) in `Nuget.Config` to `true`.</span></span> <span data-ttu-id="16a25-178">Çözüm, bu anahtar çalışır düzeyde ve bu nedenle gereksinim eklenecek `$(Solutiondir)\.nuget\Nuget.Config` dosya.</span><span class="sxs-lookup"><span data-stu-id="16a25-178">This key works at the solution level and hence need to be added to the `$(Solutiondir)\.nuget\Nuget.Config` file.</span></span> <span data-ttu-id="16a25-179">Paket geri yüklemesi Visual Studio'dan etkinleştirme bu dosyayı otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="16a25-179">Enabling package restore from Visual Studio creates this file automatically.</span></span>

<span data-ttu-id="16a25-180">**Paket geri yükleme'yi nasıl kapatırım?**</span><span class="sxs-lookup"><span data-stu-id="16a25-180">**How do I turn off package restore?**</span></span>

<span data-ttu-id="16a25-181">Bkz: [etkinleştirme ve paket geri yüklemesi devre dışı bırakma](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="16a25-181">See [Enabling and disabling package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="16a25-182">**Neden alabilirim "bağımlılık hatası bir çözümlenemiyor" ne zaman uzaktan bağımlılıkları olan yerel bir paketi yükleniyor?**</span><span class="sxs-lookup"><span data-stu-id="16a25-182">**Why do I get an "Unable to resolve dependency error" when installing a local package with remote dependencies?**</span></span>

<span data-ttu-id="16a25-183">Seçmenize gerek **tüm** bir yerel paket projeye yüklerken kaynak.</span><span class="sxs-lookup"><span data-stu-id="16a25-183">You need to select the **All** source when installing a local package into the project.</span></span> <span data-ttu-id="16a25-184">Bu yalnızca bir kullanmak yerine tüm akışları toplar.</span><span class="sxs-lookup"><span data-stu-id="16a25-184">This aggregates all the feeds instead of using just one.</span></span> <span data-ttu-id="16a25-185">Bu hata görünür kullanıcıların yerel bir depo genellikle yanlışlıkla önlemek istediğiniz nedeni şirket nedeniyle uzak bir paket yükleme ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="16a25-185">The reason this error appears is that users of a local repository often want to avoid accidentally installing a remote package due to corporate polices.</span></span>

<span data-ttu-id="16a25-186">**Birden çok proje aynı klasörde sahibim, ayrı packages.config dosyaları her proje için nasıl kullanabilirim?**</span><span class="sxs-lookup"><span data-stu-id="16a25-186">**I have multiple projects in the same folder, how can I use separate packages.config files for each project?**</span></span>

<span data-ttu-id="16a25-187">NuGet tanımlayan gibi burada ayrı projeler Canlı ayrı klasörlerde çoğu projelerde, bu bir sorun teşkil etmez `packages.config` her proje dosyaları.</span><span class="sxs-lookup"><span data-stu-id="16a25-187">In most projects where separate projects live in separate folders, this is not a problem as NuGet identifies the `packages.config` files in each project.</span></span> <span data-ttu-id="16a25-188">NuGet 3.3 + ve birden fazla ile projeleri ile aynı klasörde projeye adını ekleyebilirsiniz `packages.config` dosya adlarını kullanın düzeni `packages.{project-name}.config`, ve NuGet bu dosyasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="16a25-188">With NuGet 3.3+ and multiple projects in the same folder, you can insert the name of the project into the `packages.config` filenames use the pattern `packages.{project-name}.config`, and NuGet uses that file.</span></span>

<span data-ttu-id="16a25-189">Her proje dosyası bağımlılıkları kendi listesi içerdiğinden bu bir sorun PackageReference, kullanırken değildir.</span><span class="sxs-lookup"><span data-stu-id="16a25-189">This is not an issue when using PackageReference, as each project file contains its own list of dependencies.</span></span>

<span data-ttu-id="16a25-190">**Nuget.org depoları my listede göremiyorum, nasıl geri sağlarım?**</span><span class="sxs-lookup"><span data-stu-id="16a25-190">**I don't see nuget.org in my list of repositories, how do I get it back?**</span></span>

- <span data-ttu-id="16a25-191">Ekleme `https://api.nuget.org/v3/index.json` kaynakları, listenize veya</span><span class="sxs-lookup"><span data-stu-id="16a25-191">Add `https://api.nuget.org/v3/index.json` to your list of sources, or</span></span>
- <span data-ttu-id="16a25-192">Silme `%appdata%\.nuget\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) ve yeniden oluşturun NuGet izin verin.</span><span class="sxs-lookup"><span data-stu-id="16a25-192">Delete `%appdata%\.nuget\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) and let NuGet re-create it.</span></span>

<span data-ttu-id="16a25-193">**Bir paketi belirli lisans bilgileri sağlamazsa koşulları varsayılan lisans nelerdir?**</span><span class="sxs-lookup"><span data-stu-id="16a25-193">**What are the default license terms if a package doesn't provide specific license information?**</span></span>

<span data-ttu-id="16a25-194">Her paket paketine dahil terimleri tabidir.</span><span class="sxs-lookup"><span data-stu-id="16a25-194">Each package is governed by the terms that are included with the package.</span></span> <span data-ttu-id="16a25-195">Erişim, indirme ya da herhangi bir paket alınırken önce hüküm gözden geçirmelidir.</span><span class="sxs-lookup"><span data-stu-id="16a25-195">You should review the applicable terms before accessing, downloading, or acquiring any packages.</span></span> <span data-ttu-id="16a25-196">Nuget.org üzerinde kullanmak **lisans bilgilerini** bağlantı paketi sayfasında.</span><span class="sxs-lookup"><span data-stu-id="16a25-196">On nuget.org, use the **License Info** link on the package page.</span></span>

<span data-ttu-id="16a25-197">Bir paketi Lisans Koşulları'nı belirtmiyorsa kullanarak doğrudan paketi sahibine başvurun **sahipleri başvurun** nuget.org paketi sayfasında bağlantı.</span><span class="sxs-lookup"><span data-stu-id="16a25-197">If a package does not specify the licensing terms, contact the package owner directly using the **Contact owners** link on the nuget.org package page.</span></span> <span data-ttu-id="16a25-198">Microsoft hiçbir fikri mülkiyet, üçüncü taraf paket sağlayıcılardan lisans değildir ve üçüncü taraflar tarafından sağlanan bilgileri sorumlu değildir.</span><span class="sxs-lookup"><span data-stu-id="16a25-198">Microsoft does not license any intellectual property to you from third party package providers and is not responsible for information provided by third parties.</span></span>

## <a name="managing-packages-on-nugetorg"></a><span data-ttu-id="16a25-199">Nuget.org paketlerini yönetme</span><span class="sxs-lookup"><span data-stu-id="16a25-199">Managing packages on nuget.org</span></span>

<span data-ttu-id="16a25-200">**Paket meta verileri, karşıya yüklendikten sonra düzenleyebilir miyim? Neden nuspec düzenleme ve meta veri paketini değişiklik yapmak için yeni bir paket karşıya yükleme gerekiyor mu?**</span><span class="sxs-lookup"><span data-stu-id="16a25-200">**Can I edit package metadata after it's been uploaded? Why do you require editing the nuspec and uploading a new package for making changes to package metadata?**</span></span>

<span data-ttu-id="16a25-201">NuGet tüm paketler imzalanmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="16a25-201">NuGet requires all packages to be signed.</span></span> <span data-ttu-id="16a25-202">Paketin imzalanması bir tasarım prensibi imzalı paket içeriğini nuspec içeren değişmez, olmanızın gerekmesidir.</span><span class="sxs-lookup"><span data-stu-id="16a25-202">A design principle of package signing is that signed package content must be immutable, which includes the nuspec.</span></span> <span data-ttu-id="16a25-203">Paket meta verileri düzenleme değişiklikleri varolan imza geçersiz kılmalarını nuspec için sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="16a25-203">Editing the package metadata results in changes to the nuspec, invalidating existing signatures.</span></span> <span data-ttu-id="16a25-204">Paket oluşturulduktan sonra paket meta verileri düzenleme gerektirmeyecek şekilde var olan iş akışları değiştirme öneririz.</span><span class="sxs-lookup"><span data-stu-id="16a25-204">We recommend modifying existing workflows to not require editing the package metadata after the package has been created.</span></span>

<span data-ttu-id="16a25-205">Not paketiniz için listelenen bağımlılıkları paketinden otomatik olarak oluşturulur ve düzenlenemez.</span><span class="sxs-lookup"><span data-stu-id="16a25-205">Note that dependencies listed for your package are generated automatically from the package itself and cannot be edited.</span></span>

<span data-ttu-id="16a25-206">Ayrıca, paketler karşıya [staging.nuget.org](http://staging.nuget.org) sınamak ve bir paket genel bir galeride kullanıma olmadan paketinizi doğrulamak için harika bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="16a25-206">In addition, uploading packages to [staging.nuget.org](http://staging.nuget.org) is a great way to test and validate your package without making a package available in the public gallery.</span></span>

<span data-ttu-id="16a25-207">**Gelecekte yayımlanacak paketler için adları ayırmak mümkün mü?**</span><span class="sxs-lookup"><span data-stu-id="16a25-207">**Is it possible to reserve names for packages that will be published in future?**</span></span>

<span data-ttu-id="16a25-208">Evet.</span><span class="sxs-lookup"><span data-stu-id="16a25-208">Yes.</span></span> <span data-ttu-id="16a25-209">Üzerinde paketler için kimlikleri ayırabilirsiniz [nuget.org](https://www.nuget.org/) hesabınız için bir paket kimliği önek isteyen tarafından.</span><span class="sxs-lookup"><span data-stu-id="16a25-209">You can reserve IDs for packages on [nuget.org](https://www.nuget.org/) by requesting a package ID prefix for your account.</span></span> <span data-ttu-id="16a25-210">Bir paket kimliği öneki istemek için yönergeleri izleyin [belgelerine](https://docs.microsoft.com/nuget/reference/id-prefix-reservation).</span><span class="sxs-lookup"><span data-stu-id="16a25-210">In order to request a package ID prefix, follow the instructions in the [documentation](https://docs.microsoft.com/nuget/reference/id-prefix-reservation).</span></span>

<span data-ttu-id="16a25-211">**Paketler için sahipliğini talep nasıl?**</span><span class="sxs-lookup"><span data-stu-id="16a25-211">**How do I claim ownership for packages ?**</span></span>

<span data-ttu-id="16a25-212">Bkz: [yönetme paket sahipleri nuget.org üzerinde](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="16a25-212">See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span>

<span data-ttu-id="16a25-213">**My yazılım lisansı ihlal eden bir paket sahibi ile nasıl ilgilenir?**</span><span class="sxs-lookup"><span data-stu-id="16a25-213">**How do I deal with a package owner who is violating my software license?**</span></span>

<span data-ttu-id="16a25-214">Paket sahipleri ve diğer yazılımların sahipleri arasında kaynaklanabilecek itirazları çözümlemek için birlikte çalışmak üzere NuGet topluluk öneririz.</span><span class="sxs-lookup"><span data-stu-id="16a25-214">We encourage the NuGet community to work together to resolve any disputes that may arise between package owners and the owners of other software.</span></span> <span data-ttu-id="16a25-215">Biz hazırlanmış bir [itiraz çözümleme işlemi](../policies/dispute-resolution.md) nuget.org yöneticilerin intercede soran önce izlemek için.</span><span class="sxs-lookup"><span data-stu-id="16a25-215">We have crafted a [dispute resolution process](../policies/dispute-resolution.md) to follow before asking nuget.org administrators to intercede.</span></span>

<span data-ttu-id="16a25-216">**My sınama paketlerini nuget.org için karşıya yükleme önerilir?**</span><span class="sxs-lookup"><span data-stu-id="16a25-216">**Is it recommended to upload my test packages to nuget.org?**</span></span>

<span data-ttu-id="16a25-217">Test amaçları için kullandığınız [staging.nuget.org](http://staging.nuget.org), veya alternatif ortak NuGet sunucularını [myget.org](https://myget.org) veya [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).</span><span class="sxs-lookup"><span data-stu-id="16a25-217">For test purposes, you can use [staging.nuget.org](http://staging.nuget.org), or alternative public NuGet servers like [myget.org](https://myget.org) or [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).</span></span>

<span data-ttu-id="16a25-218">Paketler için Staging.nuget.org karşıya korunmaz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="16a25-218">Note that packages uploaded to staging.nuget.org may not be preserved.</span></span> <span data-ttu-id="16a25-219">Bkz: [güle güle Önizleme](http://blog.nuget.org/20130419/goodbye-preview.html).</span><span class="sxs-lookup"><span data-stu-id="16a25-219">See [Goodbye preview](http://blog.nuget.org/20130419/goodbye-preview.html).</span></span>

<span data-ttu-id="16a25-220">**Paketler için nuget.org karşıya yükleyebilir en büyük boyutu nedir?**</span><span class="sxs-lookup"><span data-stu-id="16a25-220">**What is the maximum size of packages I can upload to nuget.org?**</span></span>

<span data-ttu-id="16a25-221">nuget.org sağlayan paketler en fazla 250MB, ancak paketleri birbirine bağlamak için bağımlılıkları kullanarak ve paketleri 1 MB'den mümkünse tutulması önerilir.</span><span class="sxs-lookup"><span data-stu-id="16a25-221">nuget.org allows packages up to 250MB, but we recommend keeping packages under 1MB if possible and using dependencies to link packages together.</span></span> <span data-ttu-id="16a25-222">Altın kural, çakışmaları önlemek için yalnızca bir derleme paketleri içerir.</span><span class="sxs-lookup"><span data-stu-id="16a25-222">As a rule of thumb, packages contain only one assembly to avoid collisions.</span></span>

<span data-ttu-id="16a25-223">NuGet paketleri, başarısız yükler olasılığı daha küçük olanları daha büyük paketleriniz varsa şekilde indirmek için HTTP kullanır.</span><span class="sxs-lookup"><span data-stu-id="16a25-223">NuGet uses HTTP to download packages, so larger packages have a higher likelihood of failed installs than smaller ones.</span></span>

<span data-ttu-id="16a25-224">NuGet paketlerinizi Tüketiciler için toplam yükleme boyutunu küçülterek, birden çok paket arasındaki bağımlılıkları paylaşmak da mümkündür.</span><span class="sxs-lookup"><span data-stu-id="16a25-224">It is possible to share dependencies between multiple packages, making the total download size for consumers of your NuGet packages smaller.</span></span>

<span data-ttu-id="16a25-225">Çoğunlukla statik ve hiçbir zaman değişikliği bağımlılıklardır.</span><span class="sxs-lookup"><span data-stu-id="16a25-225">Dependencies are mostly static and never change.</span></span> <span data-ttu-id="16a25-226">Kodda bir hata düzeltme, bağımlılıkları güncelleştirilmesi gerekmeyebilir.</span><span class="sxs-lookup"><span data-stu-id="16a25-226">When fixing a bug in code, the dependencies may not need to be updated.</span></span> <span data-ttu-id="16a25-227">Bağımlılıklar paketini, her zaman büyük paketler reshipping yukarı sonlandırın.</span><span class="sxs-lookup"><span data-stu-id="16a25-227">If you bundle dependencies, you end up reshipping larger packages every time.</span></span> <span data-ttu-id="16a25-228">NuGet paketleri ilgili bağımlılıkları bölerek yükseltme paketinizi Tüketiciler için çok daha ayrıntılı sağlar.</span><span class="sxs-lookup"><span data-stu-id="16a25-228">By splitting NuGet packages into related dependencies, upgrades are much more fine-grained for consumers of your package.</span></span>

## <a name="nugetorg-not-accessible"></a><span data-ttu-id="16a25-229">nuget.org erişilebilir değil</span><span class="sxs-lookup"><span data-stu-id="16a25-229">nuget.org not accessible</span></span>

<span data-ttu-id="16a25-230">**Neden paketleri indirme veya paketler için nuget.org karşıya?**</span><span class="sxs-lookup"><span data-stu-id="16a25-230">**Why can't I download packages from or upload packages to nuget.org?**</span></span>

<span data-ttu-id="16a25-231">Öncelikle, NuGet'ın en son sürümlerini kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="16a25-231">First, make sure you're using the latest versions of NuGet.</span></span> <span data-ttu-id="16a25-232">Bu sürüm başarısız olmaya devam ederse [desteğine başvurun](https://www.nuget.org/policies/Contact) ve sorun giderme bilgileri de dahil olmak üzere ek bağlantı sağlayın:</span><span class="sxs-lookup"><span data-stu-id="16a25-232">If that version continues to fail, [contact support](https://www.nuget.org/policies/Contact) and provide additional connection troubleshooting information including:</span></span>

- <span data-ttu-id="16a25-233">Kullanmakta olduğunuz NuGet sürümü</span><span class="sxs-lookup"><span data-stu-id="16a25-233">The version of NuGet you're using</span></span>
- <span data-ttu-id="16a25-234">Kullanmakta olduğunuz paket kaynaklarını</span><span class="sxs-lookup"><span data-stu-id="16a25-234">The package sources you're using</span></span>
- <span data-ttu-id="16a25-235">Ayrıntılı ayrıntı düzeyine sahip bir geri yükleme günlüğü</span><span class="sxs-lookup"><span data-stu-id="16a25-235">A restore log with detailed verbosity</span></span>
- <span data-ttu-id="16a25-236">MTR veya Fiddler izlemeleri (aşağıya bakın)</span><span class="sxs-lookup"><span data-stu-id="16a25-236">MTR or a Fiddler traces (see below)</span></span>
- <span data-ttu-id="16a25-237">Coğrafi konuma</span><span class="sxs-lookup"><span data-stu-id="16a25-237">Your geographical area</span></span>
- <span data-ttu-id="16a25-238">İşletim sistemi sürümü</span><span class="sxs-lookup"><span data-stu-id="16a25-238">Your operating system version</span></span>
- <span data-ttu-id="16a25-239">Makine Yapılandırma (CPU, ağ, sabit sürücü)</span><span class="sxs-lookup"><span data-stu-id="16a25-239">Machine configuration (CPU, Network, hard drive)</span></span>
- <span data-ttu-id="16a25-240">Makinenizde bir proxy veya güvenlik duvarı arkasında olup</span><span class="sxs-lookup"><span data-stu-id="16a25-240">Whether is your machine behind a proxy or firewall</span></span>
- <span data-ttu-id="16a25-241">Makinede yüklü .NET sürümlerini</span><span class="sxs-lookup"><span data-stu-id="16a25-241">The versions of .NET that are installed on the machine</span></span>
- <span data-ttu-id="16a25-242">Platformlar arası araçlarının .NET CLI ya da kullandığınız DNU gibi sürümleri</span><span class="sxs-lookup"><span data-stu-id="16a25-242">Versions of cross-platform tools such as .NET CLI, or DNU that you're using</span></span>

<span data-ttu-id="16a25-243">*MTR yakalamak için:*</span><span class="sxs-lookup"><span data-stu-id="16a25-243">*To capture MTR:*</span></span>

- <span data-ttu-id="16a25-244">Gelen WinMTR indirin [http://winmtr.net/download/](http://winmtr.net/)</span><span class="sxs-lookup"><span data-stu-id="16a25-244">Download WinMTR from [http://winmtr.net/download/](http://winmtr.net/)</span></span>
- <span data-ttu-id="16a25-245">Girin `api.nuget.org` tıklatın ve ana bilgisayar adı olarak **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="16a25-245">Enter `api.nuget.org` as the hostname and click **Start**.</span></span>
- <span data-ttu-id="16a25-246">Bekle **gönderilen** sütunu > = 100.</span><span class="sxs-lookup"><span data-stu-id="16a25-246">Wait until the **Sent** column is >= 100.</span></span>

    ![MTR yakalama](media/mtr.png)

- <span data-ttu-id="16a25-248">Metni panoya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="16a25-248">Copy text to clipboard.</span></span>

<span data-ttu-id="16a25-249">*Fiddler yakalamak için:*</span><span class="sxs-lookup"><span data-stu-id="16a25-249">*To capture Fiddler:*</span></span>

- <span data-ttu-id="16a25-250">En son sürümünü yüklemek [Fiddler](http://www.telerik.com/download/fiddler).</span><span class="sxs-lookup"><span data-stu-id="16a25-250">Install the latest version of [Fiddler](http://www.telerik.com/download/fiddler).</span></span>
- <span data-ttu-id="16a25-251">Fiddler'ı başlatın ve yakalama trafiği kullanılarak devre dışı bırakma **Dosya > trafiği Yakala** menüsü.</span><span class="sxs-lookup"><span data-stu-id="16a25-251">Start Fiddler and disable capturing traffic using the **File > Capture Traffic** menu.</span></span>
- <span data-ttu-id="16a25-252">Tüm oturumları kaldırın (tüm öğeleri listesinde, basın seçme **silmek** anahtar).</span><span class="sxs-lookup"><span data-stu-id="16a25-252">Remove all sessions (select all items in the list, press the **Delete** key).</span></span>
- <span data-ttu-id="16a25-253">HTTPS trafiğini denetleyerek yakalamak için fiddler'ı yapılandırma **şifresini HTTPS trafiği** içinde **HTTPS** sekmesinde **Araçlar > Fiddler seçenekleri...**  menüsü.</span><span class="sxs-lookup"><span data-stu-id="16a25-253">Configure Fiddler to capture HTTPS traffic by checking **Decrypt HTTPS traffic** in the **HTTPS** tab of the **Tools > Fiddler Options...** menu.</span></span>
- <span data-ttu-id="16a25-254">Visual Studio’yu kapatın.</span><span class="sxs-lookup"><span data-stu-id="16a25-254">Close Visual Studio.</span></span>
- <span data-ttu-id="16a25-255">Etkinleştirme **Dosya > trafiği Yakala** menüsü.</span><span class="sxs-lookup"><span data-stu-id="16a25-255">Enable the **File > Capture Traffic** menu.</span></span>
- <span data-ttu-id="16a25-256">Visual Studio ya da nuget.exe .exe başlatmak ve çalışmıyor eylemleri gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="16a25-256">Start Visual Studio or nuget.exe .exe and perform the actions that are not working.</span></span> <span data-ttu-id="16a25-257">Bu eylemleri tarafından oluşturulan trafiğin Fiddler'da göstermelidir.</span><span class="sxs-lookup"><span data-stu-id="16a25-257">The traffic generated by these actions should show up in Fiddler.</span></span>
- <span data-ttu-id="16a25-258">Eylemler çalıştırdıktan sonra kullanmak **Dosya > Kaydet > tüm oturumları** yakalanan oturumları depolamak için.</span><span class="sxs-lookup"><span data-stu-id="16a25-258">Once the actions have run, use **File > Save > All Sessions** to store the captured sessions.</span></span>

<span data-ttu-id="16a25-259">Not: Bunu ayarlamak için gerekli olabilecek `HTTP_PROXY` ortam değişkenine `http://127.0.0.1:8888` Fiddler aracılığıyla yönlendirme NuGet trafiği için.</span><span class="sxs-lookup"><span data-stu-id="16a25-259">Note: it may be required to set the `HTTP_PROXY` environment variable to `http://127.0.0.1:8888` for routing NuGet traffic through Fiddler.</span></span>

<span data-ttu-id="16a25-260">Başarısız olursa, deneyin [bu StackOverflow postasında belirtilen ipuçları](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).</span><span class="sxs-lookup"><span data-stu-id="16a25-260">If that fails, try the [tips mentioned in this StackOverflow post](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).</span></span>

<span data-ttu-id="16a25-261">**Nuget.org için API uç noktaları nelerdir?**</span><span class="sxs-lookup"><span data-stu-id="16a25-261">**What are the API endpoints for nuget.org?**</span></span>

<span data-ttu-id="16a25-262">V3: `https://api.nuget.org/v3/index.json` V2: `https://www.nuget.org/api/v2/` (V2 API kullanım dışıdır ve NuGet ile 4 + çalışmaz unutmayın.)</span><span class="sxs-lookup"><span data-stu-id="16a25-262">V3: `https://api.nuget.org/v3/index.json` V2: `https://www.nuget.org/api/v2/` (Note that the V2 API is deprecated and does not work with NuGet 4+.)</span></span>
