---
title: NuGet Frequently-Asked soruları
description: NuGet 'i komut satırında ve Visual Studio 'da kullanmak için ortak sorular ve yanıtlar
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: aae6f0474cc6e8e8aa5c269b79be6fd949d9184c
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238003"
---
# <a name="nuget-frequently-asked-questions"></a><span data-ttu-id="35f99-103">NuGet sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="35f99-103">NuGet frequently-asked questions</span></span>

<span data-ttu-id="35f99-104">NuGet.org hesabı soruları gibi NuGet.org ile ilgili sık sorulan sorular için bkz. [NuGet.org sık sorulan sorular](../nuget-org/nuget-org-faq.md).</span><span class="sxs-lookup"><span data-stu-id="35f99-104">For frequently-asked questions pertaining to NuGet.org, such as NuGet.org account questions, see [NuGet.org frequently-asked questions](../nuget-org/nuget-org-faq.md).</span></span>

<span data-ttu-id="35f99-105">**NuGet 'i çalıştırmak için ne gerekir?**</span><span class="sxs-lookup"><span data-stu-id="35f99-105">**What is required to run NuGet?**</span></span>

<span data-ttu-id="35f99-106">Hem Kullanıcı arabirimi hem de komut satırı araçlarının etrafındaki tüm bilgiler, [Install kılavuzunda](../install-nuget-client-tools.md)bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="35f99-106">All the information around both UI and command-line tools is available in the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="35f99-107">**NuGet mono destekliyor mu?**</span><span class="sxs-lookup"><span data-stu-id="35f99-107">**Does NuGet support Mono?**</span></span>

<span data-ttu-id="35f99-108">Komut satırı aracı, `nuget.exe` mono 3.2 + altında oluşturulup çalışır ve mono içinde paketler oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="35f99-108">The command-line tool, `nuget.exe`, builds and runs under Mono 3.2+ and can create packages in Mono.</span></span>

<span data-ttu-id="35f99-109">`nuget.exe`, Windows üzerinde tam olarak çalışsa da, Linux ve OS X üzerinde bilinen sorunlar vardır. GitHub 'Daki [mono sorunları](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="35f99-109">Although `nuget.exe` works fully on Windows, there are known issues on Linux and OS X. Refer to [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) on GitHub.</span></span>

<span data-ttu-id="35f99-110">Bir [grafik istemci](https://github.com/mrward/monodevelop-nuget-addin) , MonoDevelop için bir eklenti olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="35f99-110">A [graphical client](https://github.com/mrward/monodevelop-nuget-addin) is available as an add-in for MonoDevelop.</span></span>

<span data-ttu-id="35f99-111">**Bir paketin neleri içerdiğini ve uygulamamın kararlı olduğunu ve yararlı olup olmadığını nasıl belirleyebilirim?**</span><span class="sxs-lookup"><span data-stu-id="35f99-111">**How can I determine what a package contains and whether it's stable and useful for my application?**</span></span>

<span data-ttu-id="35f99-112">Bir paket hakkında öğrenme birincil kaynağı, nuget.org (veya başka bir özel akıştaki) listeleme sayfasıdır.</span><span class="sxs-lookup"><span data-stu-id="35f99-112">The primary source for learning about a package is its listing page on nuget.org (or another private feed).</span></span> <span data-ttu-id="35f99-113">Nuget.org üzerindeki her paket sayfasında paketin açıklaması, sürüm geçmişi ve kullanım istatistikleri bulunur.</span><span class="sxs-lookup"><span data-stu-id="35f99-113">Each package page on nuget.org includes a description of the package, its version history, and usage statistics.</span></span> <span data-ttu-id="35f99-114">Paket sayfasındaki **bilgi** bölümü Ayrıca, paketin nasıl kullanıldığını öğrenmenize yardımcı olmak için genellikle birçok örnek ve diğer belgeleri bulabileceğiniz projenin Web sitesine bir bağlantı içerir.</span><span class="sxs-lookup"><span data-stu-id="35f99-114">The **Info** section on the package page also contains a link to the project's web site where you typically find many examples and other documentation to help you learn how the package is used.</span></span>

<span data-ttu-id="35f99-115">Daha fazla bilgi için bkz. [paketleri bulma ve seçme](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="35f99-115">For more information, see [Finding and choosing packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="nuget-in-visual-studio"></a><span data-ttu-id="35f99-116">Visual Studio 'da NuGet</span><span class="sxs-lookup"><span data-stu-id="35f99-116">NuGet in Visual Studio</span></span>

<span data-ttu-id="35f99-117">**NuGet farklı Visual Studio ürünlerinde nasıl desteklenir?**</span><span class="sxs-lookup"><span data-stu-id="35f99-117">**How is NuGet supported in different Visual Studio products?**</span></span>

- <span data-ttu-id="35f99-118">Windows üzerinde Visual Studio, [Paket Yöneticisi Kullanıcı arabirimini](../consume-packages/install-use-packages-visual-studio.md) ve [Paket Yöneticisi konsolunu](../consume-packages/install-use-packages-powershell.md)destekler.</span><span class="sxs-lookup"><span data-stu-id="35f99-118">Visual Studio on Windows supports the [Package Manager UI](../consume-packages/install-use-packages-visual-studio.md) and the [Package Manager Console](../consume-packages/install-use-packages-powershell.md).</span></span>
- <span data-ttu-id="35f99-119">Mac için Visual Studio, [projenizde bir NuGet paketi ekleme](/visualstudio/mac/nuget-walkthrough)konusunda açıklandığı gibi yerleşik NuGet özelliklerine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="35f99-119">Visual Studio for Mac has built-in NuGet capabilities as described on [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>
- <span data-ttu-id="35f99-120">Visual Studio Code (tüm platformlar) doğrudan bir NuGet tümleştirmesi yoktur.</span><span class="sxs-lookup"><span data-stu-id="35f99-120">Visual Studio Code (all platforms) does not have any direct NuGet integration.</span></span> <span data-ttu-id="35f99-121">[NUGET CLI](../reference/nuget-exe-cli-reference.md) veya [DotNet CLI](../reference/dotnet-commands.md)kullanın.</span><span class="sxs-lookup"><span data-stu-id="35f99-121">Use the [NuGet CLI](../reference/nuget-exe-cli-reference.md) or the [dotnet CLI](../reference/dotnet-commands.md).</span></span>
- <span data-ttu-id="35f99-122">Azure DevOps, [NuGet paketlerini geri yüklemek için bir derleme adımı](/vsts/build-release/tasks/package/nuget)sağlar.</span><span class="sxs-lookup"><span data-stu-id="35f99-122">Azure DevOps provides [a build step to restore NuGet packages](/vsts/build-release/tasks/package/nuget).</span></span> <span data-ttu-id="35f99-123">Ayrıca, [özel NuGet paket akışlarını Azure DevOps üzerinde de barındırabilirsiniz](/azure/devops/artifacts/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="35f99-123">You can also [host private NuGet package feeds on Azure DevOps](/azure/devops/artifacts/nuget/publish).</span></span>

<span data-ttu-id="35f99-124">**Nasıl yaparım?, yüklü olan NuGet araçlarının tam sürümü kontrol edilsin mi?**</span><span class="sxs-lookup"><span data-stu-id="35f99-124">**How do I check the exact version of the NuGet tools that are installed?**</span></span>

<span data-ttu-id="35f99-125">Visual Studio 'da **Microsoft Visual Studio hakkında yardım >** komutunu kullanın ve **NuGet Paket Yöneticisi** ' nin yanında görüntülenecek sürüme bakın.</span><span class="sxs-lookup"><span data-stu-id="35f99-125">In Visual Studio, use the **Help > About Microsoft Visual Studio** command and look at the version displayed next to **NuGet Package Manager** .</span></span>

<span data-ttu-id="35f99-126">Alternatif olarak, Paket Yöneticisi konsolunu ( **araçlar > NuGet paket yöneticisi > Paket Yöneticisi konsolu** ) başlatın ve `$host` sürümü içeren NuGet hakkındaki bilgileri görmek için girin.</span><span class="sxs-lookup"><span data-stu-id="35f99-126">Alternatively, launch the Package Manager Console ( **Tools > NuGet Package Manager > Package Manager Console** ) and enter `$host` to see information about NuGet including the version.</span></span>

<span data-ttu-id="35f99-127">**NuGet hangi programlama dillerini destekler?**</span><span class="sxs-lookup"><span data-stu-id="35f99-127">**What programming languages are supported by NuGet?**</span></span>

<span data-ttu-id="35f99-128">NuGet genellikle .NET dilleri için geçerlidir ve .NET kitaplıklarını bir projeye getirmek için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="35f99-128">NuGet generally works for .NET languages and is designed to bring .NET libraries into a project.</span></span> <span data-ttu-id="35f99-129">Ayrıca, bazı proje türlerinde MSBuild ve Visual Studio Otomasyonu ' nu desteklediğinden, diğer projeleri ve dilleri de çeşitli derecelerde destekler.</span><span class="sxs-lookup"><span data-stu-id="35f99-129">Because it also supports MSBuild and Visual Studio automation in some project types, it also supports other projects and languages to various degrees.</span></span>

<span data-ttu-id="35f99-130">NuGet 'in en son sürümü C#, Visual Basic, F #, WiX ve C++ sürümlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="35f99-130">The most recent version of NuGet supports C#, Visual Basic, F#, WiX, and C++.</span></span>

<span data-ttu-id="35f99-131">**NuGet tarafından desteklenen proje şablonları nelerdir?**</span><span class="sxs-lookup"><span data-stu-id="35f99-131">**What project templates are supported by NuGet?**</span></span>

<span data-ttu-id="35f99-132">NuGet, Windows, Web, Cloud, SharePoint, Wix gibi çeşitli proje şablonları için tam desteğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="35f99-132">NuGet has full support for a variety of project templates like Windows, Web, Cloud, SharePoint, Wix, and so on.</span></span>

<span data-ttu-id="35f99-133">**Visual Studio şablonlarının parçası olan Nasıl yaparım? güncelleştirme paketleri mi?**</span><span class="sxs-lookup"><span data-stu-id="35f99-133">**How do I update packages that are part of Visual Studio templates?**</span></span>

<span data-ttu-id="35f99-134">Paket Yöneticisi Kullanıcı arabirimindeki **güncelleştirmeler** sekmesine gidin ve **Tümünü Güncelleştir** ' i seçin ya da paket yöneticisi konsolundan [ `Update-Package` komutunu](../reference/ps-reference/ps-ref-update-package.md) kullanın.</span><span class="sxs-lookup"><span data-stu-id="35f99-134">Go to the **Updates** tab in the Package Manager UI and select **Update All** , or use the [`Update-Package` command](../reference/ps-reference/ps-ref-update-package.md) from the Package Manager Console.</span></span>

<span data-ttu-id="35f99-135">Şablonun kendisini güncelleştirmek için şablon deposunu el ile güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="35f99-135">To update the template itself, you need to manually update the template repository.</span></span> <span data-ttu-id="35f99-136">Bu konudaki [Xavier Ayrışıcı 'nın bloguna](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) bakın.</span><span class="sxs-lookup"><span data-stu-id="35f99-136">See [Xavier Decoster's blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) on this subject.</span></span> <span data-ttu-id="35f99-137">Tüm bağımlılıkların en son sürümü birbirleriyle uyumlu değilse, el ile yapılan güncelleştirmeler şablonu bozabileceğinden bunun sizin sorumluluğunuzdadır.</span><span class="sxs-lookup"><span data-stu-id="35f99-137">Note that this is done at your own risk, because manual updates might corrupt the template if the latest version of all dependencies are not compatible with each other.</span></span>

<span data-ttu-id="35f99-138">**NuGet 'i Visual Studio dışında kullanabilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="35f99-138">**Can I use NuGet outside of Visual Studio?**</span></span>

<span data-ttu-id="35f99-139">Evet, NuGet doğrudan komut satırından çalışmaktadır.</span><span class="sxs-lookup"><span data-stu-id="35f99-139">Yes, NuGet works directly from the command line.</span></span> <span data-ttu-id="35f99-140">Bkz. [Install Guide](../install-nuget-client-tools.md) ve [CLI başvurusu](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="35f99-140">See the [Install guide](../install-nuget-client-tools.md) and the [CLI reference](../reference/nuget-exe-cli-reference.md).</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="35f99-141">NuGet komut satırı</span><span class="sxs-lookup"><span data-stu-id="35f99-141">NuGet command line</span></span>

<span data-ttu-id="35f99-142">**NuGet komut satırı aracının en son sürümünü almak Nasıl yaparım??**</span><span class="sxs-lookup"><span data-stu-id="35f99-142">**How do I get the latest version of NuGet command line tool?**</span></span>

<span data-ttu-id="35f99-143">Bkz. [Install Guide](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="35f99-143">See the [Install guide](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="35f99-144">Aracın geçerli yüklü sürümünü denetlemek için kullanın `nuget help` .</span><span class="sxs-lookup"><span data-stu-id="35f99-144">To check the current installed version of the tool, use `nuget help`.</span></span>

<span data-ttu-id="35f99-145">**nuget.exe için lisans nedir?**</span><span class="sxs-lookup"><span data-stu-id="35f99-145">**What is the license for nuget.exe?**</span></span>

<span data-ttu-id="35f99-146">nuget.exe, MıT lisansı koşullarına göre yeniden dağıtmanıza izin verilir.</span><span class="sxs-lookup"><span data-stu-id="35f99-146">You are allowed to redistribute nuget.exe under the terms of the MIT license.</span></span> <span data-ttu-id="35f99-147">Yeniden dağıtmak için seçtiğiniz nuget.exe kopyalarının güncelleştirilmesi ve bakımı konusunda siz sorumlusunuz.</span><span class="sxs-lookup"><span data-stu-id="35f99-147">You are responsible for updating and servicing any copies of nuget.exe that you choose to redistribute.</span></span>

<span data-ttu-id="35f99-148">**NuGet komut satırı aracını genişletmek mümkün mü?**</span><span class="sxs-lookup"><span data-stu-id="35f99-148">**Is it possible to extend the NuGet command line tool?**</span></span>

<span data-ttu-id="35f99-149">Evet, `nuget.exe` [ramiz Reynold 'ın Post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx)bölümünde açıklandığı gibi öğesine özel komutlar eklemek mümkündür.</span><span class="sxs-lookup"><span data-stu-id="35f99-149">Yes, it's possible to add custom commands to `nuget.exe`, as described in [Rob Reynold's post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span></span>

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a><span data-ttu-id="35f99-150">NuGet Paket Yöneticisi Konsolu (Windows üzerinde Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="35f99-150">NuGet Package Manager Console (Visual Studio on Windows)</span></span>

<span data-ttu-id="35f99-151">**Nasıl yaparım? Paket Yöneticisi konsolundaki DTE nesnesine erişim izni veriyor musunuz?**</span><span class="sxs-lookup"><span data-stu-id="35f99-151">**How do I get access to the DTE object in the Package Manager console?**</span></span>

<span data-ttu-id="35f99-152">Visual Studio Automation nesne modelindeki en üst düzey nesneye DTE (geliştirme araçları ortamı) nesnesi denir.</span><span class="sxs-lookup"><span data-stu-id="35f99-152">The top-level object in the Visual Studio automation object model is called the DTE (Development Tools Environment) object.</span></span> <span data-ttu-id="35f99-153">Konsol bunu adlı bir değişken aracılığıyla sağlar `$DTE` .</span><span class="sxs-lookup"><span data-stu-id="35f99-153">The console provides this through a variable named `$DTE`.</span></span> <span data-ttu-id="35f99-154">Daha fazla bilgi için bkz. Visual Studio genişletilebilirlik belgelerindeki [Otomasyon modeline genel bakış](/visualstudio/extensibility/internals/automation-model-overview) .</span><span class="sxs-lookup"><span data-stu-id="35f99-154">For more information, see [Automation Model Overview](/visualstudio/extensibility/internals/automation-model-overview) in the Visual Studio Extensibility documentation.</span></span>

<span data-ttu-id="35f99-155">**$DTE değişkenini DTE2 türüne dönüştürmeye çalışırsam, ancak hata alıyorum: "EnvDTE. DTEClass" türündeki "EnvDTE. DTEClass" değeri "EnvDTE80. DTE2" türüne dönüştürülemez. Ne oldu?**</span><span class="sxs-lookup"><span data-stu-id="35f99-155">**I try to cast the $DTE variable to the type DTE2, but I get an error: Cannot convert the "EnvDTE.DTEClass" value of type "EnvDTE.DTEClass" to type "EnvDTE80.DTE2". What's wrong?**</span></span>

<span data-ttu-id="35f99-156">Bu, PowerShell 'in bir COM nesnesiyle etkileşime girdiği bilinen bir sorundur.</span><span class="sxs-lookup"><span data-stu-id="35f99-156">This is a known issue with how PowerShell interacts with a COM object.</span></span> <span data-ttu-id="35f99-157">Aşağıdaki işlemi deneyin:</span><span class="sxs-lookup"><span data-stu-id="35f99-157">Try the following:</span></span>

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

<span data-ttu-id="35f99-158">`Get-Interface` , NuGet PowerShell ana bilgisayarı tarafından eklenen bir yardımcı işlevdir.</span><span class="sxs-lookup"><span data-stu-id="35f99-158">`Get-Interface` is a helper function added by the NuGet PowerShell host.</span></span>

## <a name="creating-and-publishing-packages"></a><span data-ttu-id="35f99-159">Paket oluşturma ve yayımlama</span><span class="sxs-lookup"><span data-stu-id="35f99-159">Creating and publishing packages</span></span>

<span data-ttu-id="35f99-160">**Nasıl yaparım? bir akışta paketmi Listele?**</span><span class="sxs-lookup"><span data-stu-id="35f99-160">**How do I list my package in a feed?**</span></span>

<span data-ttu-id="35f99-161">Bkz. [paket oluşturma ve yayımlama](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="35f99-161">See [Creating and publishing a package](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span></span>

<span data-ttu-id="35f99-162">**.NET Framework farklı sürümlerini hedefleyen kitaplığımın birden çok sürümü var. Bunu destekleyen tek bir paket mi Nasıl yaparım??**</span><span class="sxs-lookup"><span data-stu-id="35f99-162">**I have multiple versions of my library that target different versions of the .NET Framework. How do I build a single package that supports this?**</span></span>

<span data-ttu-id="35f99-163">Bkz. [birden çok .NET Framework sürümünü ve profilini destekleme](../create-packages/supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="35f99-163">See [Supporting Multiple .NET Framework Versions and Profiles](../create-packages/supporting-multiple-target-frameworks.md).</span></span>

<span data-ttu-id="35f99-164">**Kendi deponuzu mi yoksa akışımı mı ayarlamak Nasıl yaparım??**</span><span class="sxs-lookup"><span data-stu-id="35f99-164">**How do I set up my own repository or feed?**</span></span>

<span data-ttu-id="35f99-165">[Barındırma paketlerine genel bakış](../hosting-packages/overview.md)bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="35f99-165">See the [Hosting packages overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="35f99-166">**Paketleri toplu olarak NuGet akışımla nasıl karşıya yükleyebilirim?**</span><span class="sxs-lookup"><span data-stu-id="35f99-166">**How can I upload packages to my NuGet feed in bulk?**</span></span>

<span data-ttu-id="35f99-167">Bkz. [toplu yayımlama NuGet paketleri](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span><span class="sxs-lookup"><span data-stu-id="35f99-167">See [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span></span>

## <a name="working-with-packages"></a><span data-ttu-id="35f99-168">Paketlerle çalışma</span><span class="sxs-lookup"><span data-stu-id="35f99-168">Working with packages</span></span>

<span data-ttu-id="35f99-169">**Internet bağlantısı olmadan NuGet paketleri yüklenebilirsin mi?**</span><span class="sxs-lookup"><span data-stu-id="35f99-169">**Is it possible to install NuGet packages without Internet connectivity?**</span></span>

<span data-ttu-id="35f99-170">Evet, bkz. Scott Hanselman 'ın blog gönderisi [NuGet.org kapalıysa (veya bir düzlemde olduğunuzda) NuGet 'e erişme](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (Hanselman.com).</span><span class="sxs-lookup"><span data-stu-id="35f99-170">Yes, see Scott Hanselman's Blog post [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span></span>

<span data-ttu-id="35f99-171">**Paketler, varsayılan paketler klasöründen farklı bir konuma yüklensin mi Nasıl yaparım??**</span><span class="sxs-lookup"><span data-stu-id="35f99-171">**How do I install packages in a different location from the default packages folder?**</span></span>

<span data-ttu-id="35f99-172">' Da [`repositoryPath`](../reference/nuget-config-file.md#config-section) ayarını `Nuget.Config` kullanarak ayarlayın `nuget config -set repositoryPath=<path>` .</span><span class="sxs-lookup"><span data-stu-id="35f99-172">Set the [`repositoryPath`](../reference/nuget-config-file.md#config-section) setting in `Nuget.Config` using `nuget config -set repositoryPath=<path>`.</span></span>

<span data-ttu-id="35f99-173">**Nasıl yaparım? NuGet paketleri klasörünü kaynak denetimine eklemektan kaçının mi?**</span><span class="sxs-lookup"><span data-stu-id="35f99-173">**How do I avoid adding the NuGet packages folder into to source control?**</span></span>

<span data-ttu-id="35f99-174">' İ [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) ' olarak ayarlayın `Nuget.Config` `true` .</span><span class="sxs-lookup"><span data-stu-id="35f99-174">Set the [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) in `Nuget.Config` to `true`.</span></span> <span data-ttu-id="35f99-175">Bu anahtar çözüm düzeyinde çalışarak, bu nedenle dosyaya eklenmesi gerekir `$(Solutiondir)\.nuget\Nuget.Config` .</span><span class="sxs-lookup"><span data-stu-id="35f99-175">This key works at the solution level and hence need to be added to the `$(Solutiondir)\.nuget\Nuget.Config` file.</span></span> <span data-ttu-id="35f99-176">Visual Studio 'dan paket geri yüklemeyi etkinleştirmek bu dosyayı otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="35f99-176">Enabling package restore from Visual Studio creates this file automatically.</span></span>

<span data-ttu-id="35f99-177">**Paket geri yükleme Nasıl yaparım? kapatılsın mı?**</span><span class="sxs-lookup"><span data-stu-id="35f99-177">**How do I turn off package restore?**</span></span>

<span data-ttu-id="35f99-178">Bkz. [paket geri yüklemeyi etkinleştirme ve devre dışı bırakma](../consume-packages/package-restore.md#enable-and-disable-package-restore-in-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="35f99-178">See [Enabling and disabling package restore](../consume-packages/package-restore.md#enable-and-disable-package-restore-in-visual-studio).</span></span>

<span data-ttu-id="35f99-179">**Uzak bağımlılıklara sahip yerel bir paket yüklerken neden "bağımlılık hatası çözümlenemiyor" ifadesini alıyorum?**</span><span class="sxs-lookup"><span data-stu-id="35f99-179">**Why do I get an "Unable to resolve dependency error" when installing a local package with remote dependencies?**</span></span>

<span data-ttu-id="35f99-180">Projeye yerel bir paket yüklerken **Tüm** kaynağı seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="35f99-180">You need to select the **All** source when installing a local package into the project.</span></span> <span data-ttu-id="35f99-181">Bu, yalnızca bir tane kullanmak yerine tüm akışların toplamlarını toplar.</span><span class="sxs-lookup"><span data-stu-id="35f99-181">This aggregates all the feeds instead of using just one.</span></span> <span data-ttu-id="35f99-182">Bu hatanın nedeni, yerel bir deponun kullanıcıları genellikle şirket ilkeleri nedeniyle yanlışlıkla uzak bir paket yüklemeyi önlemek istemesidir.</span><span class="sxs-lookup"><span data-stu-id="35f99-182">The reason this error appears is that users of a local repository often want to avoid accidentally installing a remote package due to corporate polices.</span></span>

<span data-ttu-id="35f99-183">**Aynı klasörde birden fazla projem var, her proje için ayrı packages.config dosyalarını nasıl kullanabilirim?**</span><span class="sxs-lookup"><span data-stu-id="35f99-183">**I have multiple projects in the same folder, how can I use separate packages.config files for each project?**</span></span>

<span data-ttu-id="35f99-184">Ayrı projelerin ayrı klasörlerde bulunduğu çoğu projede, NuGet her bir projedeki dosyaları tanımladığı için bu bir sorun değildir `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="35f99-184">In most projects where separate projects live in separate folders, this is not a problem as NuGet identifies the `packages.config` files in each project.</span></span> <span data-ttu-id="35f99-185">NuGet 3.3 + ve aynı klasörde birden çok proje ile, projenin adını `packages.config` dosya adlarıyla ekleyebilirsiniz `packages.{project-name}.config` ve NuGet bu dosyayı kullanır.</span><span class="sxs-lookup"><span data-stu-id="35f99-185">With NuGet 3.3+ and multiple projects in the same folder, you can insert the name of the project into the `packages.config` filenames use the pattern `packages.{project-name}.config`, and NuGet uses that file.</span></span>

<span data-ttu-id="35f99-186">Her proje dosyası kendi bağımlılıklar listesini içerdiğinden, PackageReference kullanılırken bu bir sorun değildir.</span><span class="sxs-lookup"><span data-stu-id="35f99-186">This is not an issue when using PackageReference, as each project file contains its own list of dependencies.</span></span>

<span data-ttu-id="35f99-187">**Depolar listemdeki nuget.org görmüyorum, nasıl geri alabilirim?**</span><span class="sxs-lookup"><span data-stu-id="35f99-187">**I don't see nuget.org in my list of repositories, how do I get it back?**</span></span>

- <span data-ttu-id="35f99-188">`https://api.nuget.org/v3/index.json`Kaynak listenize ekleyin veya</span><span class="sxs-lookup"><span data-stu-id="35f99-188">Add `https://api.nuget.org/v3/index.json` to your list of sources, or</span></span>
- <span data-ttu-id="35f99-189">`%appdata%\.nuget\NuGet.Config`(Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) öğesini silin ve NuGet 'in yeniden oluşturmasını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="35f99-189">Delete `%appdata%\.nuget\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) and let NuGet re-create it.</span></span>