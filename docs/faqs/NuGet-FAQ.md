---
title: NuGet sık sorulan sorular
description: Sık sorulan sorular ve yanıtlar komut satırında ve Visual Studio'da NuGet kullanma
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 20a55c6ba89478e70d8e6837aaebc1b7b7754a93
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842431"
---
# <a name="nuget-frequently-asked-questions"></a><span data-ttu-id="12ee0-103">NuGet sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="12ee0-103">NuGet frequently-asked questions</span></span>

<span data-ttu-id="12ee0-104">**NuGet çalıştırmak için gereken nedir?**</span><span class="sxs-lookup"><span data-stu-id="12ee0-104">**What is required to run NuGet?**</span></span>

<span data-ttu-id="12ee0-105">Hem kullanıcı Arabirimi ve komut satırı araçları tüm bilgileri kullanılabilir [Yükleme Kılavuzu](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="12ee0-105">All the information around both UI and command-line tools is available in the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="12ee0-106">**NuGet, Mono destekliyor mu?**</span><span class="sxs-lookup"><span data-stu-id="12ee0-106">**Does NuGet support Mono?**</span></span>

<span data-ttu-id="12ee0-107">Komut satırı aracı `nuget.exe`, yapılar ve Mono altında 3.2 + çalıştırır ve paketleri Mono'da oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="12ee0-107">The command-line tool, `nuget.exe`, builds and runs under Mono 3.2+ and can create packages in Mono.</span></span>

<span data-ttu-id="12ee0-108">Ancak `nuget.exe` çalışır tamamen Windows üzerinde bilinen sorunlar vardır Linux ve OS x başvurun [Mono sorunları](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) GitHub üzerinde.</span><span class="sxs-lookup"><span data-stu-id="12ee0-108">Although `nuget.exe` works fully on Windows, there are known issues on Linux and OS X. Refer to [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) on GitHub.</span></span>

<span data-ttu-id="12ee0-109">A [grafik istemci](https://github.com/mrward/monodevelop-nuget-addin) MonoDevelop için bir eklenti olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="12ee0-109">A [graphical client](https://github.com/mrward/monodevelop-nuget-addin) is available as an add-in for MonoDevelop.</span></span>

<span data-ttu-id="12ee0-110">**Bir paketi ne içerir ve kararlı ve Uygulamam için yararlı olup nasıl belirleyebilirim?**</span><span class="sxs-lookup"><span data-stu-id="12ee0-110">**How can I determine what a package contains and whether it's stable and useful for my application?**</span></span>

<span data-ttu-id="12ee0-111">Bir paketi hakkında bilgi almak için birincil kaynağı kendi nuget.org listeleme sayfasıdır (veya başka özel akış).</span><span class="sxs-lookup"><span data-stu-id="12ee0-111">The primary source for learning about a package is its listing page on nuget.org (or another private feed).</span></span> <span data-ttu-id="12ee0-112">Her bir paket nuget.org sayfasında, paket, sürüm geçmişi ve kullanım istatistiklerini açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="12ee0-112">Each package page on nuget.org includes a description of the package, its version history, and usage statistics.</span></span> <span data-ttu-id="12ee0-113">**Bilgisi** bölüm paketi sayfasında, ayrıca projenin web sitesine, genelde nerede birçok örnekler ve diğer belgeler paket nasıl kullanıldığını öğrenmenize yardımcı olması için bir bağlantı içerir.</span><span class="sxs-lookup"><span data-stu-id="12ee0-113">The **Info** section on the package page also contains a link to the project's web site where you typically find many examples and other documentation to help you learn how the package is used.</span></span>

<span data-ttu-id="12ee0-114">Daha fazla bilgi için [bulma ve seçme paketleri](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="12ee0-114">For more information, see [Finding and choosing packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="nuget-in-visual-studio"></a><span data-ttu-id="12ee0-115">Visual Studio'da NuGet</span><span class="sxs-lookup"><span data-stu-id="12ee0-115">NuGet in Visual Studio</span></span>

<span data-ttu-id="12ee0-116">**NuGet farklı Visual Studio ürünleri nasıl destekleniyor mu?**</span><span class="sxs-lookup"><span data-stu-id="12ee0-116">**How is NuGet supported in different Visual Studio products?**</span></span>

- <span data-ttu-id="12ee0-117">Windows üzerinde Visual Studio destekleyen [Paket Yöneticisi UI](../tools/package-manager-ui.md) ve [Paket Yöneticisi Konsolu](../tools/package-manager-console.md).</span><span class="sxs-lookup"><span data-stu-id="12ee0-117">Visual Studio on Windows supports the [Package Manager UI](../tools/package-manager-ui.md) and the [Package Manager Console](../tools/package-manager-console.md).</span></span>
- <span data-ttu-id="12ee0-118">Mac için Visual Studio sahip yerleşik NuGet özellikleri üzerinde açıklandığı [dahil olmak üzere bir NuGet paketini projenize](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="12ee0-118">Visual Studio for Mac has built-in NuGet capabilities as described on [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>
- <span data-ttu-id="12ee0-119">Visual Studio Code (tüm platformlar) doğrudan bir NuGet tümleştirmesi yok.</span><span class="sxs-lookup"><span data-stu-id="12ee0-119">Visual Studio Code (all platforms) does not have any direct NuGet integration.</span></span> <span data-ttu-id="12ee0-120">Kullanım [NuGet CLI](../tools/nuget-exe-cli-reference.md) veya [dotnet CLI](../tools/dotnet-commands.md).</span><span class="sxs-lookup"><span data-stu-id="12ee0-120">Use the [NuGet CLI](../tools/nuget-exe-cli-reference.md) or the [dotnet CLI](../tools/dotnet-commands.md).</span></span>
- <span data-ttu-id="12ee0-121">Azure DevOps sağlar [NuGet paketlerini geri yüklemek için bir derleme adımı](/vsts/build-release/tasks/package/nuget).</span><span class="sxs-lookup"><span data-stu-id="12ee0-121">Azure DevOps provides [a build step to restore NuGet packages](/vsts/build-release/tasks/package/nuget).</span></span> <span data-ttu-id="12ee0-122">Ayrıca [konak özel NuGet paketi üzerinde Azure DevOps akışları](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="12ee0-122">You can also [host private NuGet package feeds on Azure DevOps](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish).</span></span>

<span data-ttu-id="12ee0-123">**Yüklü olan NuGet Araçları'nın tam sürümünü nasıl kontrol edebilirim?**</span><span class="sxs-lookup"><span data-stu-id="12ee0-123">**How do I check the exact version of the NuGet tools that are installed?**</span></span>

<span data-ttu-id="12ee0-124">Visual Studio'da kullanmak **Yardım > Microsoft Visual Studio hakkında** komut ve görüntülendiğini sürümde Ara **NuGet Paket Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="12ee0-124">In Visual Studio, use the **Help > About Microsoft Visual Studio** command and look at the version displayed next to **NuGet Package Manager**.</span></span>

<span data-ttu-id="12ee0-125">Alternatif olarak, Paket Yöneticisi konsolu başlatın (**Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Konsolu**) girin `$host` NuGet sürümü dahil olmak üzere hakkındaki bilgileri görmek için.</span><span class="sxs-lookup"><span data-stu-id="12ee0-125">Alternatively, launch the Package Manager Console (**Tools > NuGet Package Manager > Package Manager Console**) and enter `$host` to see information about NuGet including the version.</span></span>

<span data-ttu-id="12ee0-126">**Hangi programlama dillerini NuGet tarafından destekleniyor mu?**</span><span class="sxs-lookup"><span data-stu-id="12ee0-126">**What programming languages are supported by NuGet?**</span></span>

<span data-ttu-id="12ee0-127">NuGet, genellikle .NET dilleri için çalışır ve bir projeye .NET kitaplıkları getirmek için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="12ee0-127">NuGet generally works for .NET languages and is designed to bring .NET libraries into a project.</span></span> <span data-ttu-id="12ee0-128">Ayrıca bazı proje türlerinde MSBuild ve Visual Studio Otomasyonu desteklediği için diğer projeleri ve çeşitli dereceye dilleri de destekler.</span><span class="sxs-lookup"><span data-stu-id="12ee0-128">Because it also supports MSBuild and Visual Studio automation in some project types, it also supports other projects and languages to various degrees.</span></span>

<span data-ttu-id="12ee0-129">En son NuGet sürümünü destekleyen C#, Visual Basic F#, WiX ve C++.</span><span class="sxs-lookup"><span data-stu-id="12ee0-129">The most recent version of NuGet supports C#, Visual Basic, F#, WiX, and C++.</span></span>

<span data-ttu-id="12ee0-130">**Hangi proje şablonları, NuGet tarafından destekleniyor mu?**</span><span class="sxs-lookup"><span data-stu-id="12ee0-130">**What project templates are supported by NuGet?**</span></span>

<span data-ttu-id="12ee0-131">NuGet, çeşitli Windows, Web, bulut, SharePoint, Wix ve benzeri gibi proje şablonları için tam destek sunar.</span><span class="sxs-lookup"><span data-stu-id="12ee0-131">NuGet has full support for a variety of project templates like Windows, Web, Cloud, SharePoint, Wix, and so on.</span></span>

<span data-ttu-id="12ee0-132">**Visual Studio şablonları parçası olan paketleri nasıl güncelleştirebilirim?**</span><span class="sxs-lookup"><span data-stu-id="12ee0-132">**How do I update packages that are part of Visual Studio templates?**</span></span>

<span data-ttu-id="12ee0-133">Git **güncelleştirmeleri** sekmesinde Paket Yöneticisi UI ve seçin **Tümünü Güncelleştir**, veya [ `Update-Package` komut](../tools/ps-ref-update-package.md) Paket Yöneticisi konsolu.</span><span class="sxs-lookup"><span data-stu-id="12ee0-133">Go to the **Updates** tab in the Package Manager UI and select **Update All**, or use the [`Update-Package` command](../tools/ps-ref-update-package.md) from the Package Manager Console.</span></span>

<span data-ttu-id="12ee0-134">Şablonu güncelleştirmek için şablon deposu el ile güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="12ee0-134">To update the template itself, you need to manually update the template repository.</span></span> <span data-ttu-id="12ee0-135">Bkz: [Xavier Decoster'ın blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) bu konuda.</span><span class="sxs-lookup"><span data-stu-id="12ee0-135">See [Xavier Decoster's blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) on this subject.</span></span> <span data-ttu-id="12ee0-136">Tüm bağımlılıkları en son sürümünü birbiriyle uyumlu değilse, el ile güncelleştirmeler şablonu bozulmasına neden olabilir çünkü kendi sorumluluğunuzdadır yapıldığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="12ee0-136">Note that this is done at your own risk, because manual updates might corrupt the template if the latest version of all dependencies are not compatible with each other.</span></span>

<span data-ttu-id="12ee0-137">**Visual Studio dışında NuGet kullanabilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="12ee0-137">**Can I use NuGet outside of Visual Studio?**</span></span>

<span data-ttu-id="12ee0-138">Evet, NuGet doğrudan komut satırından çalışır.</span><span class="sxs-lookup"><span data-stu-id="12ee0-138">Yes, NuGet works directly from the command line.</span></span> <span data-ttu-id="12ee0-139">Bkz: [Yükleme Kılavuzu](../install-nuget-client-tools.md) ve [CLI başvurusu](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="12ee0-139">See the [Install guide](../install-nuget-client-tools.md) and the [CLI reference](../tools/nuget-exe-cli-reference.md).</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="12ee0-140">NuGet komut satırı</span><span class="sxs-lookup"><span data-stu-id="12ee0-140">NuGet command line</span></span>

<span data-ttu-id="12ee0-141">**NuGet komut satırı aracının en son sürümünü nasıl alabilirim?**</span><span class="sxs-lookup"><span data-stu-id="12ee0-141">**How do I get the latest version of NuGet command line tool?**</span></span>

<span data-ttu-id="12ee0-142">Bkz: [Yükleme Kılavuzu](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="12ee0-142">See the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="12ee0-143">**Nuget.exe lisansı nedir?**</span><span class="sxs-lookup"><span data-stu-id="12ee0-143">**What is the license for nuget.exe?**</span></span>

<span data-ttu-id="12ee0-144">Nuget.exe MIT lisansı koşulları altında yeniden dağıtmanız izin verilir.</span><span class="sxs-lookup"><span data-stu-id="12ee0-144">You are allowed to redistribute nuget.exe under the terms of the MIT license.</span></span> <span data-ttu-id="12ee0-145">Güncelleştirme ve yeniden dağıtmak için seçtiğiniz nuget.exe tüm kopyalarını bakım için sorumlu olursunuz.</span><span class="sxs-lookup"><span data-stu-id="12ee0-145">You are responsible for updating and servicing any copies of nuget.exe that you choose to redistribute.</span></span>

<span data-ttu-id="12ee0-146">**NuGet komut satırı aracını genişletmek mümkündür?**</span><span class="sxs-lookup"><span data-stu-id="12ee0-146">**Is it possible to extend the NuGet command line tool?**</span></span>

<span data-ttu-id="12ee0-147">Evet, özel komutları eklemek mümkündür `nuget.exe`anlatılan şekilde [Rob Reynold'ın post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span><span class="sxs-lookup"><span data-stu-id="12ee0-147">Yes, it's possible to add custom commands to `nuget.exe`, as described in [Rob Reynold's post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span></span>

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a><span data-ttu-id="12ee0-148">NuGet Paket Yöneticisi Konsolu (Windows için Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="12ee0-148">NuGet Package Manager Console (Visual Studio on Windows)</span></span>

<span data-ttu-id="12ee0-149">**Paket Yöneticisi Konsolu'nda DTE nesnesine erişimi nasıl edinebilirim?**</span><span class="sxs-lookup"><span data-stu-id="12ee0-149">**How do I get access to the DTE object in the Package Manager console?**</span></span>

<span data-ttu-id="12ee0-150">Visual Studio Otomasyon nesne modelindeki üst düzey nesnesi (geliştirme araçları ortamı) DTE nesnesi olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="12ee0-150">The top-level object in the Visual Studio automation object model is called the DTE (Development Tools Environment) object.</span></span> <span data-ttu-id="12ee0-151">Konsol bu adlı bir değişken üzerinden sağlar `$DTE`.</span><span class="sxs-lookup"><span data-stu-id="12ee0-151">The console provides this through a variable named `$DTE`.</span></span> <span data-ttu-id="12ee0-152">Daha fazla bilgi için [Otomasyon modeline genel bakış](/visualstudio/extensibility/internals/automation-model-overview) Visual Studio genişletilebilirlik belgelerinde.</span><span class="sxs-lookup"><span data-stu-id="12ee0-152">For more information, see [Automation Model Overview](/visualstudio/extensibility/internals/automation-model-overview) in the Visual Studio Extensibility documentation.</span></span>

<span data-ttu-id="12ee0-153">**$DTE değişkeni DTE2 türüne dönüştürme deneyin ancak bir hata alıyorum: "" EnvDTE80.DTE2"türüne EnvDTE.DTEClass" türünün "EnvDTE.DTEClass" değeri dönüştürülemiyor. Ne oldu?**</span><span class="sxs-lookup"><span data-stu-id="12ee0-153">**I try to cast the $DTE variable to the type DTE2, but I get an error: Cannot convert the "EnvDTE.DTEClass" value of type "EnvDTE.DTEClass" to type "EnvDTE80.DTE2". What's wrong?**</span></span>

<span data-ttu-id="12ee0-154">Bu PowerShell bir COM nesnesi ile nasıl etkileştiğini ile bilinen bir sorundur.</span><span class="sxs-lookup"><span data-stu-id="12ee0-154">This is a known issue with how PowerShell interacts with a COM object.</span></span> <span data-ttu-id="12ee0-155">Şunları deneyin:</span><span class="sxs-lookup"><span data-stu-id="12ee0-155">Try the following:</span></span>

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

<span data-ttu-id="12ee0-156">`Get-Interface` yardımcı işlevi, NuGet PowerShell ana bilgisayar tarafından eklenir.</span><span class="sxs-lookup"><span data-stu-id="12ee0-156">`Get-Interface` is a helper function added by the NuGet PowerShell host.</span></span>

## <a name="creating-and-publishing-packages"></a><span data-ttu-id="12ee0-157">Oluşturma ve paketleri yayımlama</span><span class="sxs-lookup"><span data-stu-id="12ee0-157">Creating and publishing packages</span></span>

<span data-ttu-id="12ee0-158">**Bir akışta paketimle nasıl listelensin mi?**</span><span class="sxs-lookup"><span data-stu-id="12ee0-158">**How do I list my package in a feed?**</span></span>

<span data-ttu-id="12ee0-159">Bkz: [oluşturma ve bir paket yayımlama](../quickstart/create-and-publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="12ee0-159">See [Creating and publishing a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="12ee0-160">**My kitaplığının .NET Framework'ün farklı sürümlerini hedefleyen birden çok sürümü var. Bunu destekleyen tek bir paket nasıl oluşturabilirim?**</span><span class="sxs-lookup"><span data-stu-id="12ee0-160">**I have multiple versions of my library that target different versions of the .NET Framework. How do I build a single package that supports this?**</span></span>

<span data-ttu-id="12ee0-161">Bkz: [birden çok .NET Framework sürümleri ve profillerini destekleyen](../create-packages/supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="12ee0-161">See [Supporting Multiple .NET Framework Versions and Profiles](../create-packages/supporting-multiple-target-frameworks.md).</span></span>

<span data-ttu-id="12ee0-162">**Kendi depo veya akış yukarı nasıl ayarlayabilirim?**</span><span class="sxs-lookup"><span data-stu-id="12ee0-162">**How do I set up my own repository or feed?**</span></span>

<span data-ttu-id="12ee0-163">Bkz: [paketleri genel bakış barındırma](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="12ee0-163">See the [Hosting packages overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="12ee0-164">**Nasıl miyim toplu olarak akış my NuGet paketlerini yükleyebilir?**</span><span class="sxs-lookup"><span data-stu-id="12ee0-164">**How can I upload packages to my NuGet feed in bulk?**</span></span>

<span data-ttu-id="12ee0-165">Bkz: [toplu NuGet paketleri yayımlama](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span><span class="sxs-lookup"><span data-stu-id="12ee0-165">See [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span></span>

## <a name="working-with-packages"></a><span data-ttu-id="12ee0-166">Paketleri ile çalışma</span><span class="sxs-lookup"><span data-stu-id="12ee0-166">Working with packages</span></span>

<span data-ttu-id="12ee0-167">**Proje düzeyi paketi ve çözüm düzeyinde paket arasındaki fark nedir?**</span><span class="sxs-lookup"><span data-stu-id="12ee0-167">**What is the difference between a project-level package and a solution-level package?**</span></span>

<span data-ttu-id="12ee0-168">Bir çözüm düzeyinde paketi (NuGet 3.x+) bir çözümde yalnızca bir kez yüklenir ve ardından iş Çözümdeki tüm projeleri için kullanılabilir hale gelir.</span><span class="sxs-lookup"><span data-stu-id="12ee0-168">A solution-level package (NuGet 3.x+) is installed only once in a solution and is then available for all projects in the solution.</span></span> <span data-ttu-id="12ee0-169">Proje düzeyi paket kullandığı her projede yüklenir.</span><span class="sxs-lookup"><span data-stu-id="12ee0-169">A project-level package is installed in each project that uses it.</span></span> <span data-ttu-id="12ee0-170">Bir çözüm düzeyinde paketi, gelen paket Yöneticisi konsolu çağrılabilen yeni komutlar da yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="12ee0-170">A solution-level package might also install new commands that can be called from within the Package Manager Console.</span></span>

<span data-ttu-id="12ee0-171">**NuGet paketleri Internet bağlantısı olmadan yüklemek mümkündür?**</span><span class="sxs-lookup"><span data-stu-id="12ee0-171">**Is it possible to install NuGet packages without Internet connectivity?**</span></span>

<span data-ttu-id="12ee0-172">Evet, Scott Hanselman'ın Blog yayınına bakın [NuGet nuget.org aşağı (veya gezmeyi İşiniz olduğunda) erişmek nasıl](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span><span class="sxs-lookup"><span data-stu-id="12ee0-172">Yes, see Scott Hanselman's Blog post [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span></span>

<span data-ttu-id="12ee0-173">**Varsayılan paket klasöründen farklı bir konumda paketleri nasıl yüklerim?**</span><span class="sxs-lookup"><span data-stu-id="12ee0-173">**How do I install packages in a different location from the default packages folder?**</span></span>

<span data-ttu-id="12ee0-174">Ayarlama [ `repositoryPath` ](../reference/nuget-config-file.md#config-section) ayarı `Nuget.Config` kullanarak `nuget config -set repositoryPath=<path>`.</span><span class="sxs-lookup"><span data-stu-id="12ee0-174">Set the [`repositoryPath`](../reference/nuget-config-file.md#config-section) setting in `Nuget.Config` using `nuget config -set repositoryPath=<path>`.</span></span>

<span data-ttu-id="12ee0-175">**NuGet paketleri klasörüne kaynak denetimine eklemeye nasıl kaçınabilirim?**</span><span class="sxs-lookup"><span data-stu-id="12ee0-175">**How do I avoid adding the NuGet packages folder into to source control?**</span></span>

<span data-ttu-id="12ee0-176">Ayarlama [ `disableSourceControlIntegration` ](../reference/nuget-config-file.md#solution-section) içinde `Nuget.Config` için `true`.</span><span class="sxs-lookup"><span data-stu-id="12ee0-176">Set the [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) in `Nuget.Config` to `true`.</span></span> <span data-ttu-id="12ee0-177">Çözüm, bu anahtar çalışır düzeyi ve bu nedenle gerek eklenecek `$(Solutiondir)\.nuget\Nuget.Config` dosya.</span><span class="sxs-lookup"><span data-stu-id="12ee0-177">This key works at the solution level and hence need to be added to the `$(Solutiondir)\.nuget\Nuget.Config` file.</span></span> <span data-ttu-id="12ee0-178">Visual Studio'da paket geri yükleme etkinleştirme bu dosya otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="12ee0-178">Enabling package restore from Visual Studio creates this file automatically.</span></span>

<span data-ttu-id="12ee0-179">**Paket geri yükleme'yi nasıl kapatırım?**</span><span class="sxs-lookup"><span data-stu-id="12ee0-179">**How do I turn off package restore?**</span></span>

<span data-ttu-id="12ee0-180">Bkz: [etkinleştirme ve devre dışı paket geri yükleme](../consume-packages/package-restore.md#enable-and-disable-package-restore-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="12ee0-180">See [Enabling and disabling package restore](../consume-packages/package-restore.md#enable-and-disable-package-restore-visual-studio).</span></span>

<span data-ttu-id="12ee0-181">**Neden alabilirim "bağımlılık hatayı gidermek için yapılandırılamıyor" ne zaman yerel paket ile uzak Bağımlılıkların yüklenmesi?**</span><span class="sxs-lookup"><span data-stu-id="12ee0-181">**Why do I get an "Unable to resolve dependency error" when installing a local package with remote dependencies?**</span></span>

<span data-ttu-id="12ee0-182">Seçmenize gerek **tüm** projeye yerel bir paket yükleme sırasında kaynak.</span><span class="sxs-lookup"><span data-stu-id="12ee0-182">You need to select the **All** source when installing a local package into the project.</span></span> <span data-ttu-id="12ee0-183">Bu, yalnızca bir tane yerine tüm akışları toplar.</span><span class="sxs-lookup"><span data-stu-id="12ee0-183">This aggregates all the feeds instead of using just one.</span></span> <span data-ttu-id="12ee0-184">Bu hatanın görünür bir yerel depo kullanıcıları genellikle yanlışlıkla önlemek istediğiniz nedeni Kurumsal nedeniyle uzak bir paketi yükleme ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="12ee0-184">The reason this error appears is that users of a local repository often want to avoid accidentally installing a remote package due to corporate polices.</span></span>

<span data-ttu-id="12ee0-185">**Aynı klasörde birden çok proje sahibim, ayrı packages.config dosyaları her proje için nasıl kullanabilirim?**</span><span class="sxs-lookup"><span data-stu-id="12ee0-185">**I have multiple projects in the same folder, how can I use separate packages.config files for each project?**</span></span>

<span data-ttu-id="12ee0-186">NuGet tanımlar burada ayrı projeler Canlı ayrı klasörlerde çoğu projelerinde, bu bir sorun değildir `packages.config` her proje dosyaları.</span><span class="sxs-lookup"><span data-stu-id="12ee0-186">In most projects where separate projects live in separate folders, this is not a problem as NuGet identifies the `packages.config` files in each project.</span></span> <span data-ttu-id="12ee0-187">NuGet 3.3 + ve birden çok ile aynı klasörde yer alan projeler, projeye adı ekleyebilirsiniz `packages.config` dosya adlarını desenini kullanın `packages.{project-name}.config`, ve bu dosyayı NuGet kullanır.</span><span class="sxs-lookup"><span data-stu-id="12ee0-187">With NuGet 3.3+ and multiple projects in the same folder, you can insert the name of the project into the `packages.config` filenames use the pattern `packages.{project-name}.config`, and NuGet uses that file.</span></span>

<span data-ttu-id="12ee0-188">Her proje dosyası kendi listesi bağımlılıklar içerdiğinden bu soruna PackageReference, kullanırken değil.</span><span class="sxs-lookup"><span data-stu-id="12ee0-188">This is not an issue when using PackageReference, as each project file contains its own list of dependencies.</span></span>

<span data-ttu-id="12ee0-189">**Depolarımın listesini nuget.org göremiyorum, nasıl geri alabilirim?**</span><span class="sxs-lookup"><span data-stu-id="12ee0-189">**I don't see nuget.org in my list of repositories, how do I get it back?**</span></span>

- <span data-ttu-id="12ee0-190">Ekleme `https://api.nuget.org/v3/index.json` listenize kaynakları, veya</span><span class="sxs-lookup"><span data-stu-id="12ee0-190">Add `https://api.nuget.org/v3/index.json` to your list of sources, or</span></span>
- <span data-ttu-id="12ee0-191">Silme `%appdata%\.nuget\NuGet.Config` (Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) ve NuGet yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="12ee0-191">Delete `%appdata%\.nuget\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) and let NuGet re-create it.</span></span>
