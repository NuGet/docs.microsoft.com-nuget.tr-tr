---
title: NuGet Sık Sorulan Sorular
description: NuGet'i komut satırında ve Visual Studio'da kullanmak için sık sorulan sorular ve yanıtlar
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 8cc990e0c9eed07c59c8dffb04d104be47051736
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "69999949"
---
# <a name="nuget-frequently-asked-questions"></a><span data-ttu-id="3f2f0-103">NuSık sık sorulan soruları alın</span><span class="sxs-lookup"><span data-stu-id="3f2f0-103">NuGet frequently-asked questions</span></span>

<span data-ttu-id="3f2f0-104">NuGet.org hesap soruları gibi NuGet.org ilgili sık sorulan sorular için, [sık sorulan NuGet.org sorulara](../nuget-org/nuget-org-faq.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-104">For frequently-asked questions pertaining to NuGet.org, such as NuGet.org account questions, see [NuGet.org frequently-asked questions](../nuget-org/nuget-org-faq.md).</span></span>

<span data-ttu-id="3f2f0-105">**NuGet'i çalıştırmak için neler gereklidir?**</span><span class="sxs-lookup"><span data-stu-id="3f2f0-105">**What is required to run NuGet?**</span></span>

<span data-ttu-id="3f2f0-106">Hem Kullanıcı UI hem de komut satırı araçları yla ilgili tüm bilgiler [Yükleme kılavuzunda](../install-nuget-client-tools.md)mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-106">All the information around both UI and command-line tools is available in the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="3f2f0-107">**NuGet Mono'yı destekliyor mu?**</span><span class="sxs-lookup"><span data-stu-id="3f2f0-107">**Does NuGet support Mono?**</span></span>

<span data-ttu-id="3f2f0-108">Komut satırı aracı, `nuget.exe`Mono 3.2+ altında oluşturur ve çalışır ve Mono'da paketler oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-108">The command-line tool, `nuget.exe`, builds and runs under Mono 3.2+ and can create packages in Mono.</span></span>

<span data-ttu-id="3f2f0-109">Windows'da tam olarak çalışsa da, `nuget.exe` Linux ve [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) OS X ile ilgili bilinen sorunlar vardır.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-109">Although `nuget.exe` works fully on Windows, there are known issues on Linux and OS X. Refer to [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) on GitHub.</span></span>

<span data-ttu-id="3f2f0-110">MonoDevelop için eklenti olarak [bir grafik istemcisi](https://github.com/mrward/monodevelop-nuget-addin) kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-110">A [graphical client](https://github.com/mrward/monodevelop-nuget-addin) is available as an add-in for MonoDevelop.</span></span>

<span data-ttu-id="3f2f0-111">**Bir paketin ne içerdiğini ve uygulamam için kararlı ve kullanışlı olup olmadığını nasıl belirleyebilirim?**</span><span class="sxs-lookup"><span data-stu-id="3f2f0-111">**How can I determine what a package contains and whether it's stable and useful for my application?**</span></span>

<span data-ttu-id="3f2f0-112">Bir paket hakkında bilgi edinmek için birincil kaynak nuget.org (veya başka bir özel besleme) üzerindeki giriş sayfasıdır.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-112">The primary source for learning about a package is its listing page on nuget.org (or another private feed).</span></span> <span data-ttu-id="3f2f0-113">nuget.org'daki her paket sayfası paketin açıklamasını, sürüm geçmişini ve kullanım istatistiklerini içerir.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-113">Each package page on nuget.org includes a description of the package, its version history, and usage statistics.</span></span> <span data-ttu-id="3f2f0-114">Paket sayfasındaki **Bilgi** bölümü, genellikle paketin nasıl kullanıldığını öğrenmenize yardımcı olacak birçok örnek ve diğer belgeleri bulduğunuz projenin web sitesine bir bağlantı da içerir.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-114">The **Info** section on the package page also contains a link to the project's web site where you typically find many examples and other documentation to help you learn how the package is used.</span></span>

<span data-ttu-id="3f2f0-115">Daha fazla bilgi için [paketleri bulma ve seçme](../consume-packages/finding-and-choosing-packages.md)ye bakın.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-115">For more information, see [Finding and choosing packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="nuget-in-visual-studio"></a><span data-ttu-id="3f2f0-116">NuGet Görsel Stüdyoda</span><span class="sxs-lookup"><span data-stu-id="3f2f0-116">NuGet in Visual Studio</span></span>

<span data-ttu-id="3f2f0-117">**NuGet farklı Visual Studio ürünlerinde nasıl desteklenir?**</span><span class="sxs-lookup"><span data-stu-id="3f2f0-117">**How is NuGet supported in different Visual Studio products?**</span></span>

- <span data-ttu-id="3f2f0-118">Windows'daki Visual [Studio, Paket Yöneticisi UI'yi](../consume-packages/install-use-packages-visual-studio.md) ve [Paket Yöneticisi Konsolu'nu](../consume-packages/install-use-packages-powershell.md)destekler.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-118">Visual Studio on Windows supports the [Package Manager UI](../consume-packages/install-use-packages-visual-studio.md) and the [Package Manager Console](../consume-packages/install-use-packages-powershell.md).</span></span>
- <span data-ttu-id="3f2f0-119">Mac için Visual Studio, [projenize bir NuGet paketi dahil](/visualstudio/mac/nuget-walkthrough)etme de dahil olmak üzere açıklandığı gibi yerleşik NuGet özelliklerine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-119">Visual Studio for Mac has built-in NuGet capabilities as described on [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>
- <span data-ttu-id="3f2f0-120">Visual Studio Code (tüm platformlar) herhangi bir doğrudan NuGet entegrasyonu yok.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-120">Visual Studio Code (all platforms) does not have any direct NuGet integration.</span></span> <span data-ttu-id="3f2f0-121">[NuGet CLI](../reference/nuget-exe-cli-reference.md) veya [dotnet CLI'yi](../reference/dotnet-commands.md)kullanın.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-121">Use the [NuGet CLI](../reference/nuget-exe-cli-reference.md) or the [dotnet CLI](../reference/dotnet-commands.md).</span></span>
- <span data-ttu-id="3f2f0-122">Azure [DevOps, NuGet paketlerini geri yüklemek için bir yapı adımı](/vsts/build-release/tasks/package/nuget)sağlar.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-122">Azure DevOps provides [a build step to restore NuGet packages](/vsts/build-release/tasks/package/nuget).</span></span> <span data-ttu-id="3f2f0-123">Azure [DevOps'te özel NuGet paket akışlarını](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish)da barındırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-123">You can also [host private NuGet package feeds on Azure DevOps](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish).</span></span>

<span data-ttu-id="3f2f0-124">**Yüklenen NuGet araçlarının tam sürümünü nasıl kontrol edebilirim?**</span><span class="sxs-lookup"><span data-stu-id="3f2f0-124">**How do I check the exact version of the NuGet tools that are installed?**</span></span>

<span data-ttu-id="3f2f0-125">Visual Studio'da Microsoft **Visual Studio** hakkında yardım > kullanın ve **NuGet Package Manager'ın**yanında görüntülenen sürüme bakın.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-125">In Visual Studio, use the **Help > About Microsoft Visual Studio** command and look at the version displayed next to **NuGet Package Manager**.</span></span>

<span data-ttu-id="3f2f0-126">Alternatif olarak, Paket Yöneticisi Konsolu 'nu **(Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Konsolu)** başlatın ve sürüm de dahil olmak üzere NuGet hakkındaki bilgileri görmek için girin. `$host`</span><span class="sxs-lookup"><span data-stu-id="3f2f0-126">Alternatively, launch the Package Manager Console (**Tools > NuGet Package Manager > Package Manager Console**) and enter `$host` to see information about NuGet including the version.</span></span>

<span data-ttu-id="3f2f0-127">**NuGet tarafından hangi programlama dilleri desteklenir?**</span><span class="sxs-lookup"><span data-stu-id="3f2f0-127">**What programming languages are supported by NuGet?**</span></span>

<span data-ttu-id="3f2f0-128">NuGet genellikle .NET dilleri için çalışır ve .NET kitaplıklarını bir projeye katmak üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-128">NuGet generally works for .NET languages and is designed to bring .NET libraries into a project.</span></span> <span data-ttu-id="3f2f0-129">Bazı proje türlerinde MSBuild ve Visual Studio otomasyonunu da desteklediği nden, diğer projeleri ve dilleri çeşitli derecelerde de destekler.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-129">Because it also supports MSBuild and Visual Studio automation in some project types, it also supports other projects and languages to various degrees.</span></span>

<span data-ttu-id="3f2f0-130">NuGet'in en son sürümü C#, Visual Basic, F#, WiX ve C++'ı destekler.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-130">The most recent version of NuGet supports C#, Visual Basic, F#, WiX, and C++.</span></span>

<span data-ttu-id="3f2f0-131">**NuGet tarafından hangi proje şablonları desteklenir?**</span><span class="sxs-lookup"><span data-stu-id="3f2f0-131">**What project templates are supported by NuGet?**</span></span>

<span data-ttu-id="3f2f0-132">NuGet, Windows, Web, Bulut, SharePoint, Wix gibi çeşitli proje şablonları için tam destek vardır.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-132">NuGet has full support for a variety of project templates like Windows, Web, Cloud, SharePoint, Wix, and so on.</span></span>

<span data-ttu-id="3f2f0-133">**Visual Studio şablonlarının bir parçası olan paketleri nasıl güncellerim?**</span><span class="sxs-lookup"><span data-stu-id="3f2f0-133">**How do I update packages that are part of Visual Studio templates?**</span></span>

<span data-ttu-id="3f2f0-134">Paket Yöneticisi Kullanıcı UI'deki **Güncelleştirmeler** sekmesine gidin ve **Tümünü Güncelleştir'i**seçin veya Paket Yöneticisi Konsolu'ndan [ `Update-Package` komutu](../reference/ps-reference/ps-ref-update-package.md) kullanın.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-134">Go to the **Updates** tab in the Package Manager UI and select **Update All**, or use the [`Update-Package` command](../reference/ps-reference/ps-ref-update-package.md) from the Package Manager Console.</span></span>

<span data-ttu-id="3f2f0-135">Şablonun kendisini güncelleştirmek için şablon deposunu el ile güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-135">To update the template itself, you need to manually update the template repository.</span></span> <span data-ttu-id="3f2f0-136">Bu konuda [Xavier Decoster günlüğü](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) bakın.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-136">See [Xavier Decoster's blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) on this subject.</span></span> <span data-ttu-id="3f2f0-137">Tüm bağımlılıkların en son sürümü birbiriyle uyumlu değilse, el ile güncelleştirmeler şablonu bozabileceğinden, bunun kendi riskiniz olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-137">Note that this is done at your own risk, because manual updates might corrupt the template if the latest version of all dependencies are not compatible with each other.</span></span>

<span data-ttu-id="3f2f0-138">**Visual Studio dışında NuGet kullanabilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="3f2f0-138">**Can I use NuGet outside of Visual Studio?**</span></span>

<span data-ttu-id="3f2f0-139">Evet, NuGet doğrudan komut satırından çalışır.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-139">Yes, NuGet works directly from the command line.</span></span> <span data-ttu-id="3f2f0-140">Yükleme [kılavuzuna](../install-nuget-client-tools.md) ve [CLI başvurusuna](../reference/nuget-exe-cli-reference.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-140">See the [Install guide](../install-nuget-client-tools.md) and the [CLI reference](../reference/nuget-exe-cli-reference.md).</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="3f2f0-141">NuGet komut satırı</span><span class="sxs-lookup"><span data-stu-id="3f2f0-141">NuGet command line</span></span>

<span data-ttu-id="3f2f0-142">**NuGet komut satırı aracının en son sürümünü nasıl edinebilirim?**</span><span class="sxs-lookup"><span data-stu-id="3f2f0-142">**How do I get the latest version of NuGet command line tool?**</span></span>

<span data-ttu-id="3f2f0-143">Yükle [kılavuzuna](../install-nuget-client-tools.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-143">See the [Install guide](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="3f2f0-144">Aracın geçerli yüklü sürümünü denetlemek için `nuget help`.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-144">To check the current installed version of the tool, use `nuget help`.</span></span>

<span data-ttu-id="3f2f0-145">**Nuget.exe'nin lisansı nedir?**</span><span class="sxs-lookup"><span data-stu-id="3f2f0-145">**What is the license for nuget.exe?**</span></span>

<span data-ttu-id="3f2f0-146">Nuget.exe'yi MIT lisansı nın şartları altında yeniden dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-146">You are allowed to redistribute nuget.exe under the terms of the MIT license.</span></span> <span data-ttu-id="3f2f0-147">Yeniden dağıtmayı seçtiğiniz nuget.exe kopyalarını güncellemek ve hizmet vermek sizin sorumluluğunuzdadır.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-147">You are responsible for updating and servicing any copies of nuget.exe that you choose to redistribute.</span></span>

<span data-ttu-id="3f2f0-148">**NuGet komut satırı aracını genişletmek mümkün mü?**</span><span class="sxs-lookup"><span data-stu-id="3f2f0-148">**Is it possible to extend the NuGet command line tool?**</span></span>

<span data-ttu-id="3f2f0-149">Evet, [Rob Reynold sonrası](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx)açıklandığı `nuget.exe`gibi , özel komutları eklemek mümkündür.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-149">Yes, it's possible to add custom commands to `nuget.exe`, as described in [Rob Reynold's post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span></span>

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a><span data-ttu-id="3f2f0-150">NuGet Paket Yöneticisi Konsolu (Windows'da Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="3f2f0-150">NuGet Package Manager Console (Visual Studio on Windows)</span></span>

<span data-ttu-id="3f2f0-151">**Paket Yöneticisi konsolundaki DTE nesnesine nasıl erişebilirim?**</span><span class="sxs-lookup"><span data-stu-id="3f2f0-151">**How do I get access to the DTE object in the Package Manager console?**</span></span>

<span data-ttu-id="3f2f0-152">Visual Studio otomasyon nesnesi modelindeki üst düzey nesneye DTE (Geliştirme Araçları Ortamı) nesnesi adı verilir.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-152">The top-level object in the Visual Studio automation object model is called the DTE (Development Tools Environment) object.</span></span> <span data-ttu-id="3f2f0-153">Konsol bunu . `$DTE`</span><span class="sxs-lookup"><span data-stu-id="3f2f0-153">The console provides this through a variable named `$DTE`.</span></span> <span data-ttu-id="3f2f0-154">Daha fazla bilgi için Visual Studio Genişletilebilirlik belgelerinde [Otomasyon Modeline Genel Bakış'a](/visualstudio/extensibility/internals/automation-model-overview) bakın.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-154">For more information, see [Automation Model Overview](/visualstudio/extensibility/internals/automation-model-overview) in the Visual Studio Extensibility documentation.</span></span>

<span data-ttu-id="3f2f0-155">**$DTE değişkenini DTE2 türüne dökmeye çalışıyorum, ancak bir hata alıyorum: "EnvDTE.DTEClass" türündeki "EnvDTE.DTEClass" değerini "EnvDTE80.DTE2" yazına dönüştüremiyorum. Ne oldu?**</span><span class="sxs-lookup"><span data-stu-id="3f2f0-155">**I try to cast the $DTE variable to the type DTE2, but I get an error: Cannot convert the "EnvDTE.DTEClass" value of type "EnvDTE.DTEClass" to type "EnvDTE80.DTE2". What's wrong?**</span></span>

<span data-ttu-id="3f2f0-156">Bu, PowerShell'in com nesnesiyle nasıl etkileşimde olduğuyla ilgili bilinen bir sorundur.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-156">This is a known issue with how PowerShell interacts with a COM object.</span></span> <span data-ttu-id="3f2f0-157">Aşağıdaki işlemi deneyin:</span><span class="sxs-lookup"><span data-stu-id="3f2f0-157">Try the following:</span></span>

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

<span data-ttu-id="3f2f0-158">`Get-Interface`NuGet PowerShell ana bilgisayar tarafından eklenen bir yardımcı işlevdir.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-158">`Get-Interface` is a helper function added by the NuGet PowerShell host.</span></span>

## <a name="creating-and-publishing-packages"></a><span data-ttu-id="3f2f0-159">Paket oluşturma ve yayımlama</span><span class="sxs-lookup"><span data-stu-id="3f2f0-159">Creating and publishing packages</span></span>

<span data-ttu-id="3f2f0-160">**Paketimi özet akışında nasıl listeleyebilirim?**</span><span class="sxs-lookup"><span data-stu-id="3f2f0-160">**How do I list my package in a feed?**</span></span>

<span data-ttu-id="3f2f0-161">Bkz. [Paket oluşturma ve yayımlama.](../quickstart/create-and-publish-a-package.md)</span><span class="sxs-lookup"><span data-stu-id="3f2f0-161">See [Creating and publishing a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="3f2f0-162">**Kütüphanemin .NET Framework'ün farklı sürümlerini hedefleyen birden çok sürümü var. Bunu destekleyen tek bir paketi nasıl oluştururum?**</span><span class="sxs-lookup"><span data-stu-id="3f2f0-162">**I have multiple versions of my library that target different versions of the .NET Framework. How do I build a single package that supports this?**</span></span>

<span data-ttu-id="3f2f0-163">Bkz. [Birden Çok .NET Framework Sürümlerini ve Profillerini Destekleme](../create-packages/supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="3f2f0-163">See [Supporting Multiple .NET Framework Versions and Profiles](../create-packages/supporting-multiple-target-frameworks.md).</span></span>

<span data-ttu-id="3f2f0-164">**Kendi depomu veya beslememi nasıl ayarlıyorum?**</span><span class="sxs-lookup"><span data-stu-id="3f2f0-164">**How do I set up my own repository or feed?**</span></span>

<span data-ttu-id="3f2f0-165">Hosting [paketlerine genel bakışa](../hosting-packages/overview.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-165">See the [Hosting packages overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="3f2f0-166">**Paketleri NuGet akışıma toplu olarak nasıl yükleyebilirim?**</span><span class="sxs-lookup"><span data-stu-id="3f2f0-166">**How can I upload packages to my NuGet feed in bulk?**</span></span>

<span data-ttu-id="3f2f0-167">Bkz. [Toplu yayımlama NuGet paketleri](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span><span class="sxs-lookup"><span data-stu-id="3f2f0-167">See [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span></span>

## <a name="working-with-packages"></a><span data-ttu-id="3f2f0-168">Paketlerle çalışma</span><span class="sxs-lookup"><span data-stu-id="3f2f0-168">Working with packages</span></span>

<span data-ttu-id="3f2f0-169">**Proje düzeyinde paket ile çözüm düzeyinde paket arasındaki fark nedir?**</span><span class="sxs-lookup"><span data-stu-id="3f2f0-169">**What is the difference between a project-level package and a solution-level package?**</span></span>

<span data-ttu-id="3f2f0-170">Çözüm düzeyinde bir paket (NuGet 3.x+) bir çözüme yalnızca bir kez yüklenir ve daha sonra çözümdeki tüm projeler için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-170">A solution-level package (NuGet 3.x+) is installed only once in a solution and is then available for all projects in the solution.</span></span> <span data-ttu-id="3f2f0-171">Onu kullanan her projeye proje düzeyinde bir paket yüklenir.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-171">A project-level package is installed in each project that uses it.</span></span> <span data-ttu-id="3f2f0-172">Çözüm düzeyindebir paket, Paket Yöneticisi Konsolu'nun içinden çağrılabilen yeni komutlar da yükleyebilir.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-172">A solution-level package might also install new commands that can be called from within the Package Manager Console.</span></span>

<span data-ttu-id="3f2f0-173">**NuGet paketlerini Internet bağlantısı olmadan yüklemek mümkün mü?**</span><span class="sxs-lookup"><span data-stu-id="3f2f0-173">**Is it possible to install NuGet packages without Internet connectivity?**</span></span>

<span data-ttu-id="3f2f0-174">Evet, Scott Hanselman'ın blog gönderisine bakın [nuget.org düştüğünde (veya uçaktaolduğunuzda) NuGet'e nasıl erişilir](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span><span class="sxs-lookup"><span data-stu-id="3f2f0-174">Yes, see Scott Hanselman's Blog post [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span></span>

<span data-ttu-id="3f2f0-175">**Paketleri varsayılan paketler klasöründen farklı bir konuma nasıl yüklerim?**</span><span class="sxs-lookup"><span data-stu-id="3f2f0-175">**How do I install packages in a different location from the default packages folder?**</span></span>

<span data-ttu-id="3f2f0-176">[`repositoryPath`](../reference/nuget-config-file.md#config-section) Kullanarak ayarı `Nuget.Config` `nuget config -set repositoryPath=<path>`ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-176">Set the [`repositoryPath`](../reference/nuget-config-file.md#config-section) setting in `Nuget.Config` using `nuget config -set repositoryPath=<path>`.</span></span>

<span data-ttu-id="3f2f0-177">**NuGet paketleri klasörünü kaynak denetimine eklemekten nasıl kaçınırım?**</span><span class="sxs-lookup"><span data-stu-id="3f2f0-177">**How do I avoid adding the NuGet packages folder into to source control?**</span></span>

<span data-ttu-id="3f2f0-178">[`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) Ayarlayın. `Nuget.Config` `true`</span><span class="sxs-lookup"><span data-stu-id="3f2f0-178">Set the [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) in `Nuget.Config` to `true`.</span></span> <span data-ttu-id="3f2f0-179">Bu anahtar çözüm düzeyinde çalışır ve bu nedenle `$(Solutiondir)\.nuget\Nuget.Config` dosyaya eklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-179">This key works at the solution level and hence need to be added to the `$(Solutiondir)\.nuget\Nuget.Config` file.</span></span> <span data-ttu-id="3f2f0-180">Visual Studio'dan paket geri yüklemesini etkinleştirmek bu dosyayı otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-180">Enabling package restore from Visual Studio creates this file automatically.</span></span>

<span data-ttu-id="3f2f0-181">**Paket geri yüklemeyi nasıl kapatırım?**</span><span class="sxs-lookup"><span data-stu-id="3f2f0-181">**How do I turn off package restore?**</span></span>

<span data-ttu-id="3f2f0-182">Bkz. [Etkinleştirme ve devre dışı bırakma paketi geri yükleme.](../consume-packages/package-restore.md#enable-and-disable-package-restore-in-visual-studio)</span><span class="sxs-lookup"><span data-stu-id="3f2f0-182">See [Enabling and disabling package restore](../consume-packages/package-restore.md#enable-and-disable-package-restore-in-visual-studio).</span></span>

<span data-ttu-id="3f2f0-183">**Uzak bağımlılıkları olan yerel bir paket yüklerken neden "Bağımlılık hatasını çözemedim" alıyorum?**</span><span class="sxs-lookup"><span data-stu-id="3f2f0-183">**Why do I get an "Unable to resolve dependency error" when installing a local package with remote dependencies?**</span></span>

<span data-ttu-id="3f2f0-184">Projeye yerel bir paket yüklerken **Tüm** kaynağı seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-184">You need to select the **All** source when installing a local package into the project.</span></span> <span data-ttu-id="3f2f0-185">Bu, tek bir tane kullanmak yerine tüm akışları toplar.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-185">This aggregates all the feeds instead of using just one.</span></span> <span data-ttu-id="3f2f0-186">Bu hatanın ortaya çıkmasının nedeni, yerel bir deponun kullanıcılarının genellikle şirket polisleri nedeniyle yanlışlıkla uzak bir paket yüklemekten kaçınmak istemeleridir.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-186">The reason this error appears is that users of a local repository often want to avoid accidentally installing a remote package due to corporate polices.</span></span>

<span data-ttu-id="3f2f0-187">**Aynı klasörde birden fazla projem var, her proje için ayrı paketler.config dosyalarını nasıl kullanabilirim?**</span><span class="sxs-lookup"><span data-stu-id="3f2f0-187">**I have multiple projects in the same folder, how can I use separate packages.config files for each project?**</span></span>

<span data-ttu-id="3f2f0-188">Ayrı projelerin ayrı klasörlerde yaşadığı çoğu projede, NuGet her `packages.config` projedeki dosyaları tanımladığı için bu bir sorun değildir.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-188">In most projects where separate projects live in separate folders, this is not a problem as NuGet identifies the `packages.config` files in each project.</span></span> <span data-ttu-id="3f2f0-189">NuGet 3.3+ ve aynı klasördeki birden fazla proje yle, proje `packages.config` adını dosya adlarına ekleyebilirsiniz deseni `packages.{project-name}.config`kullanın ve NuGet bu dosyayı kullanır.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-189">With NuGet 3.3+ and multiple projects in the same folder, you can insert the name of the project into the `packages.config` filenames use the pattern `packages.{project-name}.config`, and NuGet uses that file.</span></span>

<span data-ttu-id="3f2f0-190">Her proje dosyası kendi bağımlılık listesini içerdiğinden, PackageReference'ı kullanırken bu bir sorun değildir.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-190">This is not an issue when using PackageReference, as each project file contains its own list of dependencies.</span></span>

<span data-ttu-id="3f2f0-191">**Depo listemde nuget.org göremiyorum, nasıl geri alabilirim?**</span><span class="sxs-lookup"><span data-stu-id="3f2f0-191">**I don't see nuget.org in my list of repositories, how do I get it back?**</span></span>

- <span data-ttu-id="3f2f0-192">Kaynak `https://api.nuget.org/v3/index.json` listenize ekleyin veya</span><span class="sxs-lookup"><span data-stu-id="3f2f0-192">Add `https://api.nuget.org/v3/index.json` to your list of sources, or</span></span>
- <span data-ttu-id="3f2f0-193">Delete `%appdata%\.nuget\NuGet.Config` (Windows) `~/.nuget/NuGet/NuGet.Config` veya (Mac/Linux) ve NuGet'in yeniden oluşturmasına izin verin.</span><span class="sxs-lookup"><span data-stu-id="3f2f0-193">Delete `%appdata%\.nuget\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) and let NuGet re-create it.</span></span>
