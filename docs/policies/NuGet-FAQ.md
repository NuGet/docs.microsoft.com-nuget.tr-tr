---
title: NuGet sık sorulan sorular
description: Sık sorulan sorular ve komut satırında ve Visual Studio'da NuGet kullanma ve NuGet Galerisi ile çalışmaya yönelik yanıtlar.
author: karann-msft
ms.author: karann
ms.date: 01/11/2018
ms.topic: conceptual
ms.openlocfilehash: c136a3dffac38a68b80f730de1e4c3a3a9c8bd5d
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580369"
---
# <a name="nuget-frequently-asked-questions"></a><span data-ttu-id="4508c-103">NuGet sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="4508c-103">NuGet frequently-asked questions</span></span>

<span data-ttu-id="4508c-104">**NuGet çalıştırmak için gereken nedir?**</span><span class="sxs-lookup"><span data-stu-id="4508c-104">**What is required to run NuGet?**</span></span>

<span data-ttu-id="4508c-105">Hem kullanıcı Arabirimi ve komut satırı araçları tüm bilgileri kullanılabilir [Yükleme Kılavuzu](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="4508c-105">All the information around both UI and command-line tools is available in the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="4508c-106">**NuGet, Mono destekliyor mu?**</span><span class="sxs-lookup"><span data-stu-id="4508c-106">**Does NuGet support Mono?**</span></span>

<span data-ttu-id="4508c-107">Komut satırı aracı `nuget.exe`, yapılar ve Mono altında 3.2 + çalıştırır ve paketleri Mono'da oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4508c-107">The command-line tool, `nuget.exe`, builds and runs under Mono 3.2+ and can create packages in Mono.</span></span>

<span data-ttu-id="4508c-108">Ancak `nuget.exe` çalışır tamamen Windows üzerinde bilinen sorunlar vardır Linux ve OS x başvurun [Mono sorunları](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) GitHub üzerinde.</span><span class="sxs-lookup"><span data-stu-id="4508c-108">Although `nuget.exe` works fully on Windows, there are known issues on Linux and OS X. Refer to [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) on GitHub.</span></span>

<span data-ttu-id="4508c-109">A [grafik istemci](https://github.com/mrward/monodevelop-nuget-addin) MonoDevelop için bir eklenti olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="4508c-109">A [graphical client](https://github.com/mrward/monodevelop-nuget-addin) is available as an add-in for MonoDevelop.</span></span>

<span data-ttu-id="4508c-110">**Bir paketi ne içerir ve kararlı ve Uygulamam için yararlı olup nasıl belirleyebilirim?**</span><span class="sxs-lookup"><span data-stu-id="4508c-110">**How can I determine what a package contains and whether it's stable and useful for my application?**</span></span>

<span data-ttu-id="4508c-111">Bir paketi hakkında bilgi almak için birincil kaynağı kendi nuget.org listeleme sayfasıdır (veya başka özel akış).</span><span class="sxs-lookup"><span data-stu-id="4508c-111">The primary source for learning about a package is its listing page on nuget.org (or another private feed).</span></span> <span data-ttu-id="4508c-112">Her bir paket nuget.org sayfasında, paket, sürüm geçmişi ve kullanım istatistiklerini açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="4508c-112">Each package page on nuget.org includes a description of the package, its version history, and usage statistics.</span></span> <span data-ttu-id="4508c-113">**Bilgisi** bölüm paketi sayfasında, ayrıca projenin web sitesine, genelde nerede birçok örnekler ve diğer belgeler paket nasıl kullanıldığını öğrenmenize yardımcı olması için bir bağlantı içerir.</span><span class="sxs-lookup"><span data-stu-id="4508c-113">The **Info** section on the package page also contains a link to the project's web site where you typically find many examples and other documentation to help you learn how the package is used.</span></span>

<span data-ttu-id="4508c-114">Daha fazla bilgi için [bulma ve seçme paketleri](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="4508c-114">For more information, see [Finding and choosing packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="nuget-in-visual-studio"></a><span data-ttu-id="4508c-115">Visual Studio'da NuGet</span><span class="sxs-lookup"><span data-stu-id="4508c-115">NuGet in Visual Studio</span></span>

<span data-ttu-id="4508c-116">**NuGet farklı Visual Studio ürünleri nasıl destekleniyor mu?**</span><span class="sxs-lookup"><span data-stu-id="4508c-116">**How is NuGet supported in different Visual Studio products?**</span></span>

- <span data-ttu-id="4508c-117">Windows üzerinde Visual Studio destekleyen [Paket Yöneticisi UI](../tools/package-manager-ui.md) ve [Paket Yöneticisi Konsolu](../tools/package-manager-console.md).</span><span class="sxs-lookup"><span data-stu-id="4508c-117">Visual Studio on Windows supports the [Package Manager UI](../tools/package-manager-ui.md) and the [Package Manager Console](../tools/package-manager-console.md).</span></span>
- <span data-ttu-id="4508c-118">Mac için Visual Studio sahip yerleşik NuGet özellikleri üzerinde açıklandığı [dahil olmak üzere bir NuGet paketini projenize](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="4508c-118">Visual Studio for Mac has built-in NuGet capabilities as described on [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>
- <span data-ttu-id="4508c-119">Visual Studio Code (tüm platformlar) doğrudan bir NuGet tümleştirmesi yok.</span><span class="sxs-lookup"><span data-stu-id="4508c-119">Visual Studio Code (all platforms) does not have any direct NuGet integration.</span></span> <span data-ttu-id="4508c-120">Kullanım [NuGet CLI](../tools/nuget-exe-cli-reference.md) veya [dotnet CLI](../tools/dotnet-commands.md).</span><span class="sxs-lookup"><span data-stu-id="4508c-120">Use the [NuGet CLI](../tools/nuget-exe-cli-reference.md) or the [dotnet CLI](../tools/dotnet-commands.md).</span></span>
- <span data-ttu-id="4508c-121">Visual Studio Team Services sağlar [NuGet paketlerini geri yüklemek için bir derleme adımı](/vsts/build-release/tasks/package/nuget).</span><span class="sxs-lookup"><span data-stu-id="4508c-121">Visual Studio Team Services provides [a build step to restore NuGet packages](/vsts/build-release/tasks/package/nuget).</span></span> <span data-ttu-id="4508c-122">Ayrıca [konak özel NuGet paket akışları Team Services üzerinde](https://www.visualstudio.com/docs/package/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="4508c-122">You can also [host private NuGet package feeds on Team Services](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

<span data-ttu-id="4508c-123">**Yüklü olan NuGet Araçları'nın tam sürümünü nasıl kontrol edebilirim?**</span><span class="sxs-lookup"><span data-stu-id="4508c-123">**How do I check the exact version of the NuGet tools that are installed?**</span></span>

<span data-ttu-id="4508c-124">Visual Studio'da kullanmak **Yardım > Microsoft Visual Studio hakkında** komut ve görüntülendiğini sürümde Ara **NuGet Paket Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="4508c-124">In Visual Studio, use the **Help > About Microsoft Visual Studio** command and look at the version displayed next to **NuGet Package Manager**.</span></span>

<span data-ttu-id="4508c-125">Alternatif olarak, Paket Yöneticisi konsolu başlatın (**Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Konsolu**) girin `$host` NuGet sürümü dahil olmak üzere hakkındaki bilgileri görmek için.</span><span class="sxs-lookup"><span data-stu-id="4508c-125">Alternatively, launch the Package Manager Console (**Tools > NuGet Package Manager > Package Manager Console**) and enter `$host` to see information about NuGet including the version.</span></span>

<span data-ttu-id="4508c-126">**Hangi programlama dillerini NuGet tarafından destekleniyor mu?**</span><span class="sxs-lookup"><span data-stu-id="4508c-126">**What programming languages are supported by NuGet?**</span></span>

<span data-ttu-id="4508c-127">NuGet, genellikle .NET dilleri için çalışır ve bir projeye .NET kitaplıkları getirmek için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="4508c-127">NuGet generally works for .NET languages and is designed to bring .NET libraries into a project.</span></span> <span data-ttu-id="4508c-128">Ayrıca bazı proje türlerinde MSBuild ve Visual Studio Otomasyonu desteklediği için diğer projeleri ve çeşitli dereceye dilleri de destekler.</span><span class="sxs-lookup"><span data-stu-id="4508c-128">Because it also supports MSBuild and Visual Studio automation in some project types, it also supports other projects and languages to various degrees.</span></span>

<span data-ttu-id="4508c-129">En son NuGet sürümünü destekleyen C#, Visual Basic F#, WiX ve C++.</span><span class="sxs-lookup"><span data-stu-id="4508c-129">The most recent version of NuGet supports C#, Visual Basic, F#, WiX, and C++.</span></span>

<span data-ttu-id="4508c-130">**Hangi proje şablonları, NuGet tarafından destekleniyor mu?**</span><span class="sxs-lookup"><span data-stu-id="4508c-130">**What project templates are supported by NuGet?**</span></span>

<span data-ttu-id="4508c-131">NuGet, çeşitli Windows, Web, bulut, SharePoint, Wix ve benzeri gibi proje şablonları için tam destek sunar.</span><span class="sxs-lookup"><span data-stu-id="4508c-131">NuGet has full support for a variety of project templates like Windows, Web, Cloud, SharePoint, Wix, and so on.</span></span>

<span data-ttu-id="4508c-132">**Visual Studio şablonları parçası olan paketleri nasıl güncelleştirebilirim?**</span><span class="sxs-lookup"><span data-stu-id="4508c-132">**How do I update packages that are part of Visual Studio templates?**</span></span>

<span data-ttu-id="4508c-133">Git **güncelleştirmeleri** sekmesinde Paket Yöneticisi UI ve seçin **Tümünü Güncelleştir**, veya [ `Update-Package` komut](../tools/ps-ref-update-package.md) Paket Yöneticisi konsolu.</span><span class="sxs-lookup"><span data-stu-id="4508c-133">Go to the **Updates** tab in the Package Manager UI and select **Update All**, or use the [`Update-Package` command](../tools/ps-ref-update-package.md) from the Package Manager Console.</span></span>

<span data-ttu-id="4508c-134">Şablonu güncelleştirmek için şablon deposu el ile güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4508c-134">To update the template itself, you need to manually update the template repository.</span></span> <span data-ttu-id="4508c-135">Bkz: [Xavier Decoster'ın blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) bu konuda.</span><span class="sxs-lookup"><span data-stu-id="4508c-135">See [Xavier Decoster's blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) on this subject.</span></span> <span data-ttu-id="4508c-136">Tüm bağımlılıkları en son sürümünü birbiriyle uyumlu değilse, el ile güncelleştirmeler şablonu bozulmasına neden olabilir çünkü kendi sorumluluğunuzdadır yapıldığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="4508c-136">Note that this is done at your own risk, because manual updates might corrupt the template if the latest version of all dependencies are not compatible with each other.</span></span>

<span data-ttu-id="4508c-137">**Visual Studio dışında NuGet kullanabilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="4508c-137">**Can I use NuGet outside of Visual Studio?**</span></span>

<span data-ttu-id="4508c-138">Evet, NuGet doğrudan komut satırından çalışır.</span><span class="sxs-lookup"><span data-stu-id="4508c-138">Yes, NuGet works directly from the command line.</span></span> <span data-ttu-id="4508c-139">Bkz: [Yükleme Kılavuzu](../install-nuget-client-tools.md) ve [CLI başvurusu](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="4508c-139">See the [Install guide](../install-nuget-client-tools.md) and the [CLI reference](../tools/nuget-exe-cli-reference.md).</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="4508c-140">NuGet komut satırı</span><span class="sxs-lookup"><span data-stu-id="4508c-140">NuGet command line</span></span>

<span data-ttu-id="4508c-141">**NuGet komut satırı aracının en son sürümünü nasıl alabilirim?**</span><span class="sxs-lookup"><span data-stu-id="4508c-141">**How do I get the latest version of NuGet command line tool?**</span></span>

<span data-ttu-id="4508c-142">Bkz: [Yükleme Kılavuzu](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="4508c-142">See the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="4508c-143">**Nuget.exe lisansı nedir?**</span><span class="sxs-lookup"><span data-stu-id="4508c-143">**What is the license for nuget.exe?**</span></span>

<span data-ttu-id="4508c-144">Nuget.exe MIT lisansı koşulları altında yeniden dağıtmanız izin verilir.</span><span class="sxs-lookup"><span data-stu-id="4508c-144">You are allowed to redistribute nuget.exe under the terms of the MIT license.</span></span> <span data-ttu-id="4508c-145">Güncelleştirme ve yeniden dağıtmak için seçtiğiniz nuget.exe tüm kopyalarını bakım için sorumlu olursunuz.</span><span class="sxs-lookup"><span data-stu-id="4508c-145">You are responsible for updating and servicing any copies of nuget.exe that you choose to redistribute.</span></span>

<span data-ttu-id="4508c-146">**NuGet komut satırı aracını genişletmek mümkündür?**</span><span class="sxs-lookup"><span data-stu-id="4508c-146">**Is it possible to extend the NuGet command line tool?**</span></span>

<span data-ttu-id="4508c-147">Evet, özel komutları eklemek mümkündür `nuget.exe`anlatılan şekilde [Rob Reynold'ın post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span><span class="sxs-lookup"><span data-stu-id="4508c-147">Yes, it's possible to add custom commands to `nuget.exe`, as described in [Rob Reynold's post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span></span>

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a><span data-ttu-id="4508c-148">NuGet Paket Yöneticisi Konsolu (Windows için Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="4508c-148">NuGet Package Manager Console (Visual Studio on Windows)</span></span>

<span data-ttu-id="4508c-149">**Paket Yöneticisi Konsolu'nda DTE nesnesine erişimi nasıl edinebilirim?**</span><span class="sxs-lookup"><span data-stu-id="4508c-149">**How do I get access to the DTE object in the Package Manager console?**</span></span>

<span data-ttu-id="4508c-150">Visual Studio Otomasyon nesne modelindeki üst düzey nesnesi (geliştirme araçları ortamı) DTE nesnesi olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="4508c-150">The top-level object in the Visual Studio automation object model is called the DTE (Development Tools Environment) object.</span></span> <span data-ttu-id="4508c-151">Konsol bu adlı bir değişken üzerinden sağlar `$DTE`.</span><span class="sxs-lookup"><span data-stu-id="4508c-151">The console provides this through a variable named `$DTE`.</span></span> <span data-ttu-id="4508c-152">Daha fazla bilgi için [Otomasyon modeline genel bakış](/visualstudio/extensibility/internals/automation-model-overview) Visual Studio genişletilebilirlik belgelerinde.</span><span class="sxs-lookup"><span data-stu-id="4508c-152">For more information, see [Automation Model Overview](/visualstudio/extensibility/internals/automation-model-overview) in the Visual Studio Extensibility documentation.</span></span>

<span data-ttu-id="4508c-153">**$DTE değişkeni DTE2 türüne dönüştürme deneyin ancak bir hata alıyorum: "" EnvDTE80.DTE2"türüne EnvDTE.DTEClass" türünün "EnvDTE.DTEClass" değeri dönüştürülemiyor. Ne oldu?**</span><span class="sxs-lookup"><span data-stu-id="4508c-153">**I try to cast the $DTE variable to the type DTE2, but I get an error: Cannot convert the "EnvDTE.DTEClass" value of type "EnvDTE.DTEClass" to type "EnvDTE80.DTE2". What's wrong?**</span></span>

<span data-ttu-id="4508c-154">Bu PowerShell bir COM nesnesi ile nasıl etkileştiğini ile bilinen bir sorundur.</span><span class="sxs-lookup"><span data-stu-id="4508c-154">This is a known issue with how PowerShell interacts with a COM object.</span></span> <span data-ttu-id="4508c-155">Şunları deneyin:</span><span class="sxs-lookup"><span data-stu-id="4508c-155">Try the following:</span></span>

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

<span data-ttu-id="4508c-156">`Get-Interface` yardımcı işlevi, NuGet PowerShell ana bilgisayar tarafından eklenir.</span><span class="sxs-lookup"><span data-stu-id="4508c-156">`Get-Interface` is a helper function added by the NuGet PowerShell host.</span></span>

## <a name="creating-and-publishing-packages"></a><span data-ttu-id="4508c-157">Oluşturma ve paketleri yayımlama</span><span class="sxs-lookup"><span data-stu-id="4508c-157">Creating and publishing packages</span></span>

<span data-ttu-id="4508c-158">**Bir akışta paketimle nasıl listelensin mi?**</span><span class="sxs-lookup"><span data-stu-id="4508c-158">**How do I list my package in a feed?**</span></span>

<span data-ttu-id="4508c-159">Bkz: [oluşturma ve bir paket yayımlama](../quickstart/create-and-publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="4508c-159">See [Creating and publishing a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="4508c-160">**My kitaplığının .NET Framework'ün farklı sürümlerini hedefleyen birden çok sürümü var. Bunu destekleyen tek bir paket nasıl oluşturabilirim?**</span><span class="sxs-lookup"><span data-stu-id="4508c-160">**I have multiple versions of my library that target different versions of the .NET Framework. How do I build a single package that supports this?**</span></span>

<span data-ttu-id="4508c-161">Bkz: [birden çok .NET Framework sürümleri ve profillerini destekleyen](../create-packages/supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="4508c-161">See [Supporting Multiple .NET Framework Versions and Profiles](../create-packages/supporting-multiple-target-frameworks.md).</span></span>

<span data-ttu-id="4508c-162">**Kendi depo veya akış yukarı nasıl ayarlayabilirim?**</span><span class="sxs-lookup"><span data-stu-id="4508c-162">**How do I set up my own repository or feed?**</span></span>

<span data-ttu-id="4508c-163">Bkz: [paketleri genel bakış barındırma](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="4508c-163">See the [Hosting packages overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="4508c-164">**Nasıl miyim toplu olarak akış my NuGet paketlerini yükleyebilir?**</span><span class="sxs-lookup"><span data-stu-id="4508c-164">**How can I upload packages to my NuGet feed in bulk?**</span></span>

<span data-ttu-id="4508c-165">Bkz: [toplu NuGet paketleri yayımlama](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span><span class="sxs-lookup"><span data-stu-id="4508c-165">See [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span></span>

## <a name="working-with-packages"></a><span data-ttu-id="4508c-166">Paketleri ile çalışma</span><span class="sxs-lookup"><span data-stu-id="4508c-166">Working with packages</span></span>

<span data-ttu-id="4508c-167">**Proje düzeyi paketi ve çözüm düzeyinde paket arasındaki fark nedir?**</span><span class="sxs-lookup"><span data-stu-id="4508c-167">**What is the difference between a project-level package and a solution-level package?**</span></span>

<span data-ttu-id="4508c-168">Bir çözüm düzeyinde paketi (NuGet 3.x+) bir çözümde yalnızca bir kez yüklenir ve ardından iş Çözümdeki tüm projeleri için kullanılabilir hale gelir.</span><span class="sxs-lookup"><span data-stu-id="4508c-168">A solution-level package (NuGet 3.x+) is installed only once in a solution and is then available for all projects in the solution.</span></span> <span data-ttu-id="4508c-169">Proje düzeyi paket kullandığı her projede yüklenir.</span><span class="sxs-lookup"><span data-stu-id="4508c-169">A project-level package is installed in each project that uses it.</span></span> <span data-ttu-id="4508c-170">Bir çözüm düzeyinde paketi, gelen paket Yöneticisi konsolu çağrılabilen yeni komutlar da yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4508c-170">A solution-level package might also install new commands that can be called from within the Package Manager Console.</span></span>

<span data-ttu-id="4508c-171">**NuGet paketleri Internet bağlantısı olmadan yüklemek mümkündür?**</span><span class="sxs-lookup"><span data-stu-id="4508c-171">**Is it possible to install NuGet packages without Internet connectivity?**</span></span>

<span data-ttu-id="4508c-172">Evet, Scott Hanselman'ın Blog yayınına bakın [NuGet nuget.org aşağı (veya gezmeyi İşiniz olduğunda) erişmek nasıl](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span><span class="sxs-lookup"><span data-stu-id="4508c-172">Yes, see Scott Hanselman's Blog post [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span></span>

<span data-ttu-id="4508c-173">**Varsayılan paket klasöründen farklı bir konumda paketleri nasıl yüklerim?**</span><span class="sxs-lookup"><span data-stu-id="4508c-173">**How do I install packages in a different location from the default packages folder?**</span></span>

<span data-ttu-id="4508c-174">Ayarlama [ `repositoryPath` ](../reference/nuget-config-file.md#config-section) ayarı `Nuget.Config` kullanarak `nuget config -set repositoryPath=<path>`.</span><span class="sxs-lookup"><span data-stu-id="4508c-174">Set the [`repositoryPath`](../reference/nuget-config-file.md#config-section) setting in `Nuget.Config` using `nuget config -set repositoryPath=<path>`.</span></span>

<span data-ttu-id="4508c-175">**NuGet paketleri klasörüne kaynak denetimine eklemeye nasıl kaçınabilirim?**</span><span class="sxs-lookup"><span data-stu-id="4508c-175">**How do I avoid adding the NuGet packages folder into to source control?**</span></span>

<span data-ttu-id="4508c-176">Ayarlama [ `disableSourceControlIntegration` ](../reference/nuget-config-file.md#solution-section) içinde `Nuget.Config` için `true`.</span><span class="sxs-lookup"><span data-stu-id="4508c-176">Set the [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) in `Nuget.Config` to `true`.</span></span> <span data-ttu-id="4508c-177">Çözüm, bu anahtar çalışır düzeyi ve bu nedenle gerek eklenecek `$(Solutiondir)\.nuget\Nuget.Config` dosya.</span><span class="sxs-lookup"><span data-stu-id="4508c-177">This key works at the solution level and hence need to be added to the `$(Solutiondir)\.nuget\Nuget.Config` file.</span></span> <span data-ttu-id="4508c-178">Visual Studio'da paket geri yükleme etkinleştirme bu dosya otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4508c-178">Enabling package restore from Visual Studio creates this file automatically.</span></span>

<span data-ttu-id="4508c-179">**Paket geri yükleme'yi nasıl kapatırım?**</span><span class="sxs-lookup"><span data-stu-id="4508c-179">**How do I turn off package restore?**</span></span>

<span data-ttu-id="4508c-180">Bkz: [etkinleştirme ve devre dışı paket geri yükleme](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span><span class="sxs-lookup"><span data-stu-id="4508c-180">See [Enabling and disabling package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="4508c-181">**Neden alabilirim "bağımlılık hatayı gidermek için yapılandırılamıyor" ne zaman yerel paket ile uzak Bağımlılıkların yüklenmesi?**</span><span class="sxs-lookup"><span data-stu-id="4508c-181">**Why do I get an "Unable to resolve dependency error" when installing a local package with remote dependencies?**</span></span>

<span data-ttu-id="4508c-182">Seçmenize gerek **tüm** projeye yerel bir paket yükleme sırasında kaynak.</span><span class="sxs-lookup"><span data-stu-id="4508c-182">You need to select the **All** source when installing a local package into the project.</span></span> <span data-ttu-id="4508c-183">Bu, yalnızca bir tane yerine tüm akışları toplar.</span><span class="sxs-lookup"><span data-stu-id="4508c-183">This aggregates all the feeds instead of using just one.</span></span> <span data-ttu-id="4508c-184">Bu hatanın görünür bir yerel depo kullanıcıları genellikle yanlışlıkla önlemek istediğiniz nedeni Kurumsal nedeniyle uzak bir paketi yükleme ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="4508c-184">The reason this error appears is that users of a local repository often want to avoid accidentally installing a remote package due to corporate polices.</span></span>

<span data-ttu-id="4508c-185">**Aynı klasörde birden çok proje sahibim, ayrı packages.config dosyaları her proje için nasıl kullanabilirim?**</span><span class="sxs-lookup"><span data-stu-id="4508c-185">**I have multiple projects in the same folder, how can I use separate packages.config files for each project?**</span></span>

<span data-ttu-id="4508c-186">NuGet tanımlar burada ayrı projeler Canlı ayrı klasörlerde çoğu projelerinde, bu bir sorun değildir `packages.config` her proje dosyaları.</span><span class="sxs-lookup"><span data-stu-id="4508c-186">In most projects where separate projects live in separate folders, this is not a problem as NuGet identifies the `packages.config` files in each project.</span></span> <span data-ttu-id="4508c-187">NuGet 3.3 + ve birden çok ile aynı klasörde yer alan projeler, projeye adı ekleyebilirsiniz `packages.config` dosya adlarını desenini kullanın `packages.{project-name}.config`, ve bu dosyayı NuGet kullanır.</span><span class="sxs-lookup"><span data-stu-id="4508c-187">With NuGet 3.3+ and multiple projects in the same folder, you can insert the name of the project into the `packages.config` filenames use the pattern `packages.{project-name}.config`, and NuGet uses that file.</span></span>

<span data-ttu-id="4508c-188">Her proje dosyası kendi listesi bağımlılıklar içerdiğinden bu soruna PackageReference, kullanırken değil.</span><span class="sxs-lookup"><span data-stu-id="4508c-188">This is not an issue when using PackageReference, as each project file contains its own list of dependencies.</span></span>

<span data-ttu-id="4508c-189">**Depolarımın listesini nuget.org göremiyorum, nasıl geri alabilirim?**</span><span class="sxs-lookup"><span data-stu-id="4508c-189">**I don't see nuget.org in my list of repositories, how do I get it back?**</span></span>

- <span data-ttu-id="4508c-190">Ekleme `https://api.nuget.org/v3/index.json` listenize kaynakları, veya</span><span class="sxs-lookup"><span data-stu-id="4508c-190">Add `https://api.nuget.org/v3/index.json` to your list of sources, or</span></span>
- <span data-ttu-id="4508c-191">Silme `%appdata%\.nuget\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) ve NuGet yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4508c-191">Delete `%appdata%\.nuget\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) and let NuGet re-create it.</span></span>

<span data-ttu-id="4508c-192">**Bir paketi belirli bir lisans bilgileri sağlamıyorsa koşulları varsayılan lisans nelerdir?**</span><span class="sxs-lookup"><span data-stu-id="4508c-192">**What are the default license terms if a package doesn't provide specific license information?**</span></span>

<span data-ttu-id="4508c-193">Her bir paketi paket ile birlikte gelen koşulları tabidir.</span><span class="sxs-lookup"><span data-stu-id="4508c-193">Each package is governed by the terms that are included with the package.</span></span> <span data-ttu-id="4508c-194">Erişim, indirme veya herhangi bir paket alınırken önce hüküm gözden geçirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4508c-194">You should review the applicable terms before accessing, downloading, or acquiring any packages.</span></span> <span data-ttu-id="4508c-195">Nuget.org kullanın **lisans bilgilerini** bağlantı paketi sayfasında.</span><span class="sxs-lookup"><span data-stu-id="4508c-195">On nuget.org, use the **License Info** link on the package page.</span></span>

<span data-ttu-id="4508c-196">Bir paketi lisans koşulları belirtmezse kullanarak doğrudan paket sahibiyle iletişime geçin **sahipleriyle temas** nuget.org paketi sayfasında bağlantı.</span><span class="sxs-lookup"><span data-stu-id="4508c-196">If a package does not specify the licensing terms, contact the package owner directly using the **Contact owners** link on the nuget.org package page.</span></span> <span data-ttu-id="4508c-197">Microsoft hiçbir fikri mülkiyet, üçüncü taraf paketi sağlayıcılarından lisans değil ve üçüncü taraflarca sağlanan bilgileri sorumlu değildir.</span><span class="sxs-lookup"><span data-stu-id="4508c-197">Microsoft does not license any intellectual property to you from third party package providers and is not responsible for information provided by third parties.</span></span>

## <a name="managing-packages-on-nugetorg"></a><span data-ttu-id="4508c-198">Paketleri nuget.org üzerinde yönetme</span><span class="sxs-lookup"><span data-stu-id="4508c-198">Managing packages on nuget.org</span></span>

<span data-ttu-id="4508c-199">**Paket meta verileri, karşıya yüklendikten sonra düzenleyebilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="4508c-199">**Can I edit package metadata after it's been uploaded?**</span></span>

<span data-ttu-id="4508c-200">NuGet imzalanması için tüm paketleri önerir.</span><span class="sxs-lookup"><span data-stu-id="4508c-200">NuGet recommends all packages to be signed.</span></span> <span data-ttu-id="4508c-201">Paket imzalama tasarımı prensibi imzalı paket içeriğini nuspec içeren değişmezse, olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="4508c-201">A design principle of package signing is that signed package content must be immutable, which includes the nuspec.</span></span> <span data-ttu-id="4508c-202">Paket meta verileri düzenleme, mevcut imza geçersiz kılmalarını nuspec için değişiklikle sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="4508c-202">Editing the package metadata results in changes to the nuspec, invalidating existing signatures.</span></span> <span data-ttu-id="4508c-203">Paket oluşturulduktan sonra paket meta verileri düzenleme gerektirmeyecek şekilde mevcut iş akışları değiştirme öneririz.</span><span class="sxs-lookup"><span data-stu-id="4508c-203">We recommend modifying existing workflows to not require editing the package metadata after the package has been created.</span></span>

<span data-ttu-id="4508c-204">Paketiniz için listelenen bağımlılıkları paketinden otomatik olarak oluşturulur ve düzenlenemez unutmayın.</span><span class="sxs-lookup"><span data-stu-id="4508c-204">Note that dependencies listed for your package are generated automatically from the package itself and cannot be edited.</span></span>

<span data-ttu-id="4508c-205">Ayrıca, paketler için karşıya yükleme [int.nugettest.org](https://int.nugettest.org) test edin ve bir paket kullanılabilir genel galeride yapmadan paketinizi doğrulamak için harika bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="4508c-205">In addition, uploading packages to [int.nugettest.org](https://int.nugettest.org) is a great way to test and validate your package without making a package available in the public gallery.</span></span>

<span data-ttu-id="4508c-206">**Bu ad gelecekte yayımlanacak paketleri için ayrılacak mümkün mü?**</span><span class="sxs-lookup"><span data-stu-id="4508c-206">**Is it possible to reserve names for packages that will be published in future?**</span></span>

<span data-ttu-id="4508c-207">Evet.</span><span class="sxs-lookup"><span data-stu-id="4508c-207">Yes.</span></span> <span data-ttu-id="4508c-208">Şirket için paket kimlikleri ayırabilirsiniz [nuget.org](https://www.nuget.org/) hesabınız için bir paket kimliği öneki isteyerek.</span><span class="sxs-lookup"><span data-stu-id="4508c-208">You can reserve IDs for packages on [nuget.org](https://www.nuget.org/) by requesting a package ID prefix for your account.</span></span> <span data-ttu-id="4508c-209">Bir paket kimliği öneki isteğinde bulunmak için yönergeleri izleyin. [belgeleri](https://docs.microsoft.com/nuget/reference/id-prefix-reservation).</span><span class="sxs-lookup"><span data-stu-id="4508c-209">In order to request a package ID prefix, follow the instructions in the [documentation](https://docs.microsoft.com/nuget/reference/id-prefix-reservation).</span></span>

<span data-ttu-id="4508c-210">**Paketler için mülkiyeti üzerine hak iddia nasıl?**</span><span class="sxs-lookup"><span data-stu-id="4508c-210">**How do I claim ownership for packages ?**</span></span>

<span data-ttu-id="4508c-211">Bkz: [yönetme paket sahipleri nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="4508c-211">See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span>

<span data-ttu-id="4508c-212">**Yazılım lisansımın ihlal bir paket sahibi ile nasıl dağıtılsın mı?**</span><span class="sxs-lookup"><span data-stu-id="4508c-212">**How do I deal with a package owner who is violating my software license?**</span></span>

<span data-ttu-id="4508c-213">Paket sahipleri ve diğer yazılımların sahipleri arasında kaynaklanabilecek herhangi Anlaşmazlıkların çözüm yeri birlikte çalışmak için NuGet topluluk öneririz.</span><span class="sxs-lookup"><span data-stu-id="4508c-213">We encourage the NuGet community to work together to resolve any disputes that may arise between package owners and the owners of other software.</span></span> <span data-ttu-id="4508c-214">Biz hazırlanmış bir [itiraz çözümleme işlemi](../policies/dispute-resolution.md) nuget.org yöneticilerin intercede isteyen önce izlemek için.</span><span class="sxs-lookup"><span data-stu-id="4508c-214">We have crafted a [dispute resolution process](../policies/dispute-resolution.md) to follow before asking nuget.org administrators to intercede.</span></span>

<span data-ttu-id="4508c-215">**Benim test paketleri nuget.org için karşıya yüklemek için tavsiye edilir?**</span><span class="sxs-lookup"><span data-stu-id="4508c-215">**Is it recommended to upload my test packages to nuget.org?**</span></span>

<span data-ttu-id="4508c-216">Test amaçları için kullanabileceğiniz [int.nugettest.org](https://int.nugettest.org), veya diğer genel NuGet sunucularını [myget.org](https://myget.org) veya [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).</span><span class="sxs-lookup"><span data-stu-id="4508c-216">For test purposes, you can use [int.nugettest.org](https://int.nugettest.org), or alternative public NuGet servers like [myget.org](https://myget.org) or [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).</span></span>

<span data-ttu-id="4508c-217">Paketler için int.nugettest.org karşıya korunmaz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="4508c-217">Note that packages uploaded to int.nugettest.org may not be preserved.</span></span>

<span data-ttu-id="4508c-218">**Paketleri nuget.org için karşıya yükleyebilirsiniz boyutu üst sınırı nedir?**</span><span class="sxs-lookup"><span data-stu-id="4508c-218">**What is the maximum size of packages I can upload to nuget.org?**</span></span>

<span data-ttu-id="4508c-219">nuget.org sağlayan paketler en fazla 250MB, ancak paketleri 1 MB'den mümkünse tutulması ve paketleri birbirine bağlamak için bağımlılıklar kullanarak önerilir.</span><span class="sxs-lookup"><span data-stu-id="4508c-219">nuget.org allows packages up to 250MB, but we recommend keeping packages under 1MB if possible and using dependencies to link packages together.</span></span> <span data-ttu-id="4508c-220">Bir kural karşısında, paketler çarpışmalardan kaçınmak için yalnızca bir derleme içerir.</span><span class="sxs-lookup"><span data-stu-id="4508c-220">As a rule of thumb, packages contain only one assembly to avoid collisions.</span></span>

<span data-ttu-id="4508c-221">NuGet paketleri başarısız yüklemeler olasılığı daha küçük parçalara değerinden daha büyük paketleriniz varsa bu nedenle indirmek için HTTP kullanır.</span><span class="sxs-lookup"><span data-stu-id="4508c-221">NuGet uses HTTP to download packages, so larger packages have a higher likelihood of failed installs than smaller ones.</span></span>

<span data-ttu-id="4508c-222">Toplam yükleme boyutu için NuGet paketlerinizi tüketicilerinin küçülterek birden çok paketleri arasındaki bağımlılıkları paylaşmak da mümkündür.</span><span class="sxs-lookup"><span data-stu-id="4508c-222">It is possible to share dependencies between multiple packages, making the total download size for consumers of your NuGet packages smaller.</span></span>

<span data-ttu-id="4508c-223">Çoğunlukla statik ve hiçbir zaman değişiklik bağımlılıklardır.</span><span class="sxs-lookup"><span data-stu-id="4508c-223">Dependencies are mostly static and never change.</span></span> <span data-ttu-id="4508c-224">Kodda bir hatayı düzeltirken, bağımlılıkları güncelleştirilmesi gerekmez.</span><span class="sxs-lookup"><span data-stu-id="4508c-224">When fixing a bug in code, the dependencies may not need to be updated.</span></span> <span data-ttu-id="4508c-225">Bağımlılıkları paketlerseniz, her zaman büyük paketler reshipping yukarı bitmelidir.</span><span class="sxs-lookup"><span data-stu-id="4508c-225">If you bundle dependencies, you end up reshipping larger packages every time.</span></span> <span data-ttu-id="4508c-226">NuGet paketlerini ilgili bağımlılıklarınızı bölerek yükseltme paketinin Tüketiciler için çok daha ayrıntılı sağlar.</span><span class="sxs-lookup"><span data-stu-id="4508c-226">By splitting NuGet packages into related dependencies, upgrades are much more fine-grained for consumers of your package.</span></span>

## <a name="nugetorg-not-accessible"></a><span data-ttu-id="4508c-227">nuget.org erişilebilir değil</span><span class="sxs-lookup"><span data-stu-id="4508c-227">nuget.org not accessible</span></span>

<span data-ttu-id="4508c-228">**Neden paketleri indirin veya paketleri nuget.org için Yükle?**</span><span class="sxs-lookup"><span data-stu-id="4508c-228">**Why can't I download packages from or upload packages to nuget.org?**</span></span>

<span data-ttu-id="4508c-229">İlk olarak, en son NuGet sürümlerini kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="4508c-229">First, make sure you're using the latest versions of NuGet.</span></span> <span data-ttu-id="4508c-230">Bu sürüm başarısız devam ederseniz [Destek ekibiyle iletişime geçin](https://www.nuget.org/policies/Contact) ve sorun giderme bilgileri de dahil olmak üzere ek bağlantı sağlayın:</span><span class="sxs-lookup"><span data-stu-id="4508c-230">If that version continues to fail, [contact support](https://www.nuget.org/policies/Contact) and provide additional connection troubleshooting information including:</span></span>

- <span data-ttu-id="4508c-231">Kullanmakta olduğunuz NuGet sürümü</span><span class="sxs-lookup"><span data-stu-id="4508c-231">The version of NuGet you're using</span></span>
- <span data-ttu-id="4508c-232">Kullanmakta olduğunuz paket kaynakları</span><span class="sxs-lookup"><span data-stu-id="4508c-232">The package sources you're using</span></span>
- <span data-ttu-id="4508c-233">Ayrıntılı ayrıntı düzeyi içeren bir geri yükleme günlüğü</span><span class="sxs-lookup"><span data-stu-id="4508c-233">A restore log with detailed verbosity</span></span>
- <span data-ttu-id="4508c-234">MTR veya Fiddler izlemeleri (aşağıya bakın)</span><span class="sxs-lookup"><span data-stu-id="4508c-234">MTR or a Fiddler traces (see below)</span></span>
- <span data-ttu-id="4508c-235">Coğrafi konuma</span><span class="sxs-lookup"><span data-stu-id="4508c-235">Your geographical area</span></span>
- <span data-ttu-id="4508c-236">İşletim sistemi sürümünüz</span><span class="sxs-lookup"><span data-stu-id="4508c-236">Your operating system version</span></span>
- <span data-ttu-id="4508c-237">Makine Yapılandırması (CPU, ağ, sabit sürücü)</span><span class="sxs-lookup"><span data-stu-id="4508c-237">Machine configuration (CPU, Network, hard drive)</span></span>
- <span data-ttu-id="4508c-238">Makinenizde bir proxy veya güvenlik duvarı olup</span><span class="sxs-lookup"><span data-stu-id="4508c-238">Whether your machine is behind a proxy or firewall</span></span>
- <span data-ttu-id="4508c-239">Makinede yüklü .NET sürümlerini</span><span class="sxs-lookup"><span data-stu-id="4508c-239">The versions of .NET that are installed on the machine</span></span>
- <span data-ttu-id="4508c-240">.NET CLI veya kullanmakta olduğunuz DNU gibi platformlar arası araçları sürümleri</span><span class="sxs-lookup"><span data-stu-id="4508c-240">Versions of cross-platform tools such as .NET CLI, or DNU that you're using</span></span>

<span data-ttu-id="4508c-241">*MTR yakalamak için:*</span><span class="sxs-lookup"><span data-stu-id="4508c-241">*To capture MTR:*</span></span>

- <span data-ttu-id="4508c-242">Gelen WinMTR indirin [http://winmtr.net/download/](http://winmtr.net/)</span><span class="sxs-lookup"><span data-stu-id="4508c-242">Download WinMTR from [http://winmtr.net/download/](http://winmtr.net/)</span></span>
- <span data-ttu-id="4508c-243">Girin `api.nuget.org` tıklayın ve ana bilgisayar adı olarak **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="4508c-243">Enter `api.nuget.org` as the hostname and click **Start**.</span></span>
- <span data-ttu-id="4508c-244">Bekle **gönderilen** sütun > = 100.</span><span class="sxs-lookup"><span data-stu-id="4508c-244">Wait until the **Sent** column is >= 100.</span></span>

    ![MTR yakalama](media/mtr.png)

- <span data-ttu-id="4508c-246">Metin Panoya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="4508c-246">Copy text to clipboard.</span></span>

<span data-ttu-id="4508c-247">*Fiddler yakalamak için:*</span><span class="sxs-lookup"><span data-stu-id="4508c-247">*To capture Fiddler:*</span></span>

- <span data-ttu-id="4508c-248">En son sürümünü yükleyin [Fiddler](http://www.telerik.com/download/fiddler).</span><span class="sxs-lookup"><span data-stu-id="4508c-248">Install the latest version of [Fiddler](http://www.telerik.com/download/fiddler).</span></span>
- <span data-ttu-id="4508c-249">Fiddler'ı başlatın ve trafik yakalama kullanarak devre dışı **Dosya > trafik yakalama** menüsü.</span><span class="sxs-lookup"><span data-stu-id="4508c-249">Start Fiddler and disable capturing traffic using the **File > Capture Traffic** menu.</span></span>
- <span data-ttu-id="4508c-250">Tüm oturumlar kaldırın (tüm öğeleri listesinde, tuşuna seçin **Sil** anahtar).</span><span class="sxs-lookup"><span data-stu-id="4508c-250">Remove all sessions (select all items in the list, press the **Delete** key).</span></span>
- <span data-ttu-id="4508c-251">HTTPS trafiğini denetleyerek yakalamak için fiddler'ı yapılandırma **şifresini HTTPS trafiğini** içinde **HTTPS** sekmesinde **Araçlar > Fiddler seçenekleri...**  menüsü.</span><span class="sxs-lookup"><span data-stu-id="4508c-251">Configure Fiddler to capture HTTPS traffic by checking **Decrypt HTTPS traffic** in the **HTTPS** tab of the **Tools > Fiddler Options...** menu.</span></span>
- <span data-ttu-id="4508c-252">Visual Studio’yu kapatın.</span><span class="sxs-lookup"><span data-stu-id="4508c-252">Close Visual Studio.</span></span>
- <span data-ttu-id="4508c-253">Etkinleştirme **Dosya > trafik yakalama** menüsü.</span><span class="sxs-lookup"><span data-stu-id="4508c-253">Enable the **File > Capture Traffic** menu.</span></span>
- <span data-ttu-id="4508c-254">Visual Studio ya da nuget.exe .exe başlatın ve çalışmıyor eylemleri gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4508c-254">Start Visual Studio or nuget.exe .exe and perform the actions that are not working.</span></span> <span data-ttu-id="4508c-255">Bu eylemler tarafından oluşturulan trafiğin Fiddler'da göstermelidir.</span><span class="sxs-lookup"><span data-stu-id="4508c-255">The traffic generated by these actions should show up in Fiddler.</span></span>
- <span data-ttu-id="4508c-256">Bir eylem gerçekleştirdikten sonra kullanmak **Dosya > Kaydet > tüm oturumları** yakalanan oturumları depolamak için.</span><span class="sxs-lookup"><span data-stu-id="4508c-256">Once the actions have run, use **File > Save > All Sessions** to store the captured sessions.</span></span>

<span data-ttu-id="4508c-257">Not: Bunu ayarlamak için gerekli olabilecek `HTTP_PROXY` ortam değişkenine `http://127.0.0.1:8888` için fiddler'ı aracılığıyla NuGet trafiği yönlendirme.</span><span class="sxs-lookup"><span data-stu-id="4508c-257">Note: it may be required to set the `HTTP_PROXY` environment variable to `http://127.0.0.1:8888` for routing NuGet traffic through Fiddler.</span></span>

<span data-ttu-id="4508c-258">Bu başarısız olursa deneyin [ipuçları bu StackOverflow gönderide bahsedilen](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).</span><span class="sxs-lookup"><span data-stu-id="4508c-258">If that fails, try the [tips mentioned in this StackOverflow post](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).</span></span>

<span data-ttu-id="4508c-259">**Nuget.org API uç noktaları nelerdir?**</span><span class="sxs-lookup"><span data-stu-id="4508c-259">**What are the API endpoints for nuget.org?**</span></span>

<span data-ttu-id="4508c-260">V3: `https://api.nuget.org/v3/index.json` V2: `https://www.nuget.org/api/v2/` (V2 API kullanım dışıdır ve NuGet ile 4 + çalışmaz unutmayın.)</span><span class="sxs-lookup"><span data-stu-id="4508c-260">V3: `https://api.nuget.org/v3/index.json` V2: `https://www.nuget.org/api/v2/` (Note that the V2 API is deprecated and does not work with NuGet 4+.)</span></span>
