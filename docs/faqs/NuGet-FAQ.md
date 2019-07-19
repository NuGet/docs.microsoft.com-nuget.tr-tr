---
title: NuGet sık sorulan sorular
description: NuGet 'i komut satırında ve Visual Studio 'da kullanmak için ortak sorular ve yanıtlar
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 9094d6b4a2dbd6ea1899b4470624948ce7c21f43
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317628"
---
# <a name="nuget-frequently-asked-questions"></a><span data-ttu-id="25fc6-103">NuGet sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="25fc6-103">NuGet frequently-asked questions</span></span>

<span data-ttu-id="25fc6-104">**NuGet 'i çalıştırmak için ne gerekir?**</span><span class="sxs-lookup"><span data-stu-id="25fc6-104">**What is required to run NuGet?**</span></span>

<span data-ttu-id="25fc6-105">Hem Kullanıcı arabirimi hem de komut satırı araçlarının etrafındaki tüm bilgiler, [Install kılavuzunda](../install-nuget-client-tools.md)bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="25fc6-105">All the information around both UI and command-line tools is available in the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="25fc6-106">**NuGet mono destekliyor mu?**</span><span class="sxs-lookup"><span data-stu-id="25fc6-106">**Does NuGet support Mono?**</span></span>

<span data-ttu-id="25fc6-107">Komut satırı aracı `nuget.exe`, mono 3.2 + altında oluşturulup çalışır ve mono içinde paketler oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="25fc6-107">The command-line tool, `nuget.exe`, builds and runs under Mono 3.2+ and can create packages in Mono.</span></span>

<span data-ttu-id="25fc6-108">, `nuget.exe` Windows üzerinde tam olarak çalışsa da, Linux ve OS X üzerinde bilinen sorunlar vardır. GitHub 'daki [mono sorunları](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="25fc6-108">Although `nuget.exe` works fully on Windows, there are known issues on Linux and OS X. Refer to [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) on GitHub.</span></span>

<span data-ttu-id="25fc6-109">Bir [grafik istemci](https://github.com/mrward/monodevelop-nuget-addin) , MonoDevelop için bir eklenti olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="25fc6-109">A [graphical client](https://github.com/mrward/monodevelop-nuget-addin) is available as an add-in for MonoDevelop.</span></span>

<span data-ttu-id="25fc6-110">**Bir paketin neleri içerdiğini ve uygulamamın kararlı olduğunu ve yararlı olup olmadığını nasıl belirleyebilirim?**</span><span class="sxs-lookup"><span data-stu-id="25fc6-110">**How can I determine what a package contains and whether it's stable and useful for my application?**</span></span>

<span data-ttu-id="25fc6-111">Bir paket hakkında öğrenme birincil kaynağı, nuget.org (veya başka bir özel akıştaki) listeleme sayfasıdır.</span><span class="sxs-lookup"><span data-stu-id="25fc6-111">The primary source for learning about a package is its listing page on nuget.org (or another private feed).</span></span> <span data-ttu-id="25fc6-112">Nuget.org üzerindeki her paket sayfasında paketin açıklaması, sürüm geçmişi ve kullanım istatistikleri bulunur.</span><span class="sxs-lookup"><span data-stu-id="25fc6-112">Each package page on nuget.org includes a description of the package, its version history, and usage statistics.</span></span> <span data-ttu-id="25fc6-113">Paket sayfasındaki **bilgi** bölümü Ayrıca, paketin nasıl kullanıldığını öğrenmenize yardımcı olmak için genellikle birçok örnek ve diğer belgeleri bulabileceğiniz projenin Web sitesine bir bağlantı içerir.</span><span class="sxs-lookup"><span data-stu-id="25fc6-113">The **Info** section on the package page also contains a link to the project's web site where you typically find many examples and other documentation to help you learn how the package is used.</span></span>

<span data-ttu-id="25fc6-114">Daha fazla bilgi için bkz. [paketleri bulma ve seçme](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="25fc6-114">For more information, see [Finding and choosing packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="nuget-in-visual-studio"></a><span data-ttu-id="25fc6-115">Visual Studio 'da NuGet</span><span class="sxs-lookup"><span data-stu-id="25fc6-115">NuGet in Visual Studio</span></span>

<span data-ttu-id="25fc6-116">**NuGet farklı Visual Studio ürünlerinde nasıl desteklenir?**</span><span class="sxs-lookup"><span data-stu-id="25fc6-116">**How is NuGet supported in different Visual Studio products?**</span></span>

- <span data-ttu-id="25fc6-117">Windows üzerinde Visual Studio, [Paket Yöneticisi Kullanıcı arabirimini](../consume-packages/install-use-packages-visual-studio.md) ve [Paket Yöneticisi konsolunu](../consume-packages/install-use-packages-powershell.md)destekler.</span><span class="sxs-lookup"><span data-stu-id="25fc6-117">Visual Studio on Windows supports the [Package Manager UI](../consume-packages/install-use-packages-visual-studio.md) and the [Package Manager Console](../consume-packages/install-use-packages-powershell.md).</span></span>
- <span data-ttu-id="25fc6-118">Mac için Visual Studio, [projenizde bir NuGet paketi ekleme](/visualstudio/mac/nuget-walkthrough)konusunda açıklandığı gibi yerleşik NuGet özelliklerine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="25fc6-118">Visual Studio for Mac has built-in NuGet capabilities as described on [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>
- <span data-ttu-id="25fc6-119">Visual Studio Code (tüm platformlar) doğrudan bir NuGet tümleştirmesi yoktur.</span><span class="sxs-lookup"><span data-stu-id="25fc6-119">Visual Studio Code (all platforms) does not have any direct NuGet integration.</span></span> <span data-ttu-id="25fc6-120">[NUGET CLI](../reference/nuget-exe-cli-reference.md) veya [DotNet CLI](../reference/dotnet-commands.md)kullanın.</span><span class="sxs-lookup"><span data-stu-id="25fc6-120">Use the [NuGet CLI](../reference/nuget-exe-cli-reference.md) or the [dotnet CLI](../reference/dotnet-commands.md).</span></span>
- <span data-ttu-id="25fc6-121">Azure DevOps, [NuGet paketlerini geri yüklemek için bir derleme adımı](/vsts/build-release/tasks/package/nuget)sağlar.</span><span class="sxs-lookup"><span data-stu-id="25fc6-121">Azure DevOps provides [a build step to restore NuGet packages](/vsts/build-release/tasks/package/nuget).</span></span> <span data-ttu-id="25fc6-122">Ayrıca, [özel NuGet paket akışlarını Azure DevOps üzerinde](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish)de barındırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="25fc6-122">You can also [host private NuGet package feeds on Azure DevOps](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish).</span></span>

<span data-ttu-id="25fc6-123">**Nasıl yaparım?, yüklü olan NuGet araçlarının tam sürümü kontrol edilsin mi?**</span><span class="sxs-lookup"><span data-stu-id="25fc6-123">**How do I check the exact version of the NuGet tools that are installed?**</span></span>

<span data-ttu-id="25fc6-124">Visual Studio 'da **Microsoft Visual Studio hakkında yardım >** komutunu kullanın ve **NuGet Paket Yöneticisi**' nin yanında görüntülenecek sürüme bakın.</span><span class="sxs-lookup"><span data-stu-id="25fc6-124">In Visual Studio, use the **Help > About Microsoft Visual Studio** command and look at the version displayed next to **NuGet Package Manager**.</span></span>

<span data-ttu-id="25fc6-125">Alternatif olarak, Paket Yöneticisi konsolunu (**Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi konsolu**) başlatın ve sürümü `$host` içeren NuGet hakkındaki bilgileri görmek için girin.</span><span class="sxs-lookup"><span data-stu-id="25fc6-125">Alternatively, launch the Package Manager Console (**Tools > NuGet Package Manager > Package Manager Console**) and enter `$host` to see information about NuGet including the version.</span></span>

<span data-ttu-id="25fc6-126">**NuGet hangi programlama dillerini destekler?**</span><span class="sxs-lookup"><span data-stu-id="25fc6-126">**What programming languages are supported by NuGet?**</span></span>

<span data-ttu-id="25fc6-127">NuGet genellikle .NET dilleri için geçerlidir ve .NET kitaplıklarını bir projeye getirmek için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="25fc6-127">NuGet generally works for .NET languages and is designed to bring .NET libraries into a project.</span></span> <span data-ttu-id="25fc6-128">Ayrıca, bazı proje türlerinde MSBuild ve Visual Studio Otomasyonu ' nu desteklediğinden, diğer projeleri ve dilleri de çeşitli derecelerde destekler.</span><span class="sxs-lookup"><span data-stu-id="25fc6-128">Because it also supports MSBuild and Visual Studio automation in some project types, it also supports other projects and languages to various degrees.</span></span>

<span data-ttu-id="25fc6-129">NuGet 'in en son sürümü, Visual Basic C# F#,, Wix ve C++' i destekler.</span><span class="sxs-lookup"><span data-stu-id="25fc6-129">The most recent version of NuGet supports C#, Visual Basic, F#, WiX, and C++.</span></span>

<span data-ttu-id="25fc6-130">**NuGet tarafından desteklenen proje şablonları nelerdir?**</span><span class="sxs-lookup"><span data-stu-id="25fc6-130">**What project templates are supported by NuGet?**</span></span>

<span data-ttu-id="25fc6-131">NuGet, Windows, Web, Cloud, SharePoint, Wix gibi çeşitli proje şablonları için tam desteğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="25fc6-131">NuGet has full support for a variety of project templates like Windows, Web, Cloud, SharePoint, Wix, and so on.</span></span>

<span data-ttu-id="25fc6-132">**Visual Studio şablonlarının parçası olan Nasıl yaparım? güncelleştirme paketleri mi?**</span><span class="sxs-lookup"><span data-stu-id="25fc6-132">**How do I update packages that are part of Visual Studio templates?**</span></span>

<span data-ttu-id="25fc6-133">Paket Yöneticisi Kullanıcı arabirimindeki **güncelleştirmeler** sekmesine gidin ve **Tümünü Güncelleştir**' i seçin [ `Update-Package` ](../reference/ps-reference/ps-ref-update-package.md) ya da paket yöneticisi konsolundan komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="25fc6-133">Go to the **Updates** tab in the Package Manager UI and select **Update All**, or use the [`Update-Package` command](../reference/ps-reference/ps-ref-update-package.md) from the Package Manager Console.</span></span>

<span data-ttu-id="25fc6-134">Şablonun kendisini güncelleştirmek için şablon deposunu el ile güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="25fc6-134">To update the template itself, you need to manually update the template repository.</span></span> <span data-ttu-id="25fc6-135">Bu konudaki [Xavier Ayrışıcı 'nın bloguna](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) bakın.</span><span class="sxs-lookup"><span data-stu-id="25fc6-135">See [Xavier Decoster's blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) on this subject.</span></span> <span data-ttu-id="25fc6-136">Tüm bağımlılıkların en son sürümü birbirleriyle uyumlu değilse, el ile yapılan güncelleştirmeler şablonu bozabileceğinden bunun sizin sorumluluğunuzdadır.</span><span class="sxs-lookup"><span data-stu-id="25fc6-136">Note that this is done at your own risk, because manual updates might corrupt the template if the latest version of all dependencies are not compatible with each other.</span></span>

<span data-ttu-id="25fc6-137">**NuGet 'i Visual Studio dışında kullanabilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="25fc6-137">**Can I use NuGet outside of Visual Studio?**</span></span>

<span data-ttu-id="25fc6-138">Evet, NuGet doğrudan komut satırından çalışmaktadır.</span><span class="sxs-lookup"><span data-stu-id="25fc6-138">Yes, NuGet works directly from the command line.</span></span> <span data-ttu-id="25fc6-139">Bkz. [Install Guide](../install-nuget-client-tools.md) ve [CLI başvurusu](../reference/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="25fc6-139">See the [Install guide](../install-nuget-client-tools.md) and the [CLI reference](../reference/nuget-exe-cli-reference.md).</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="25fc6-140">NuGet komut satırı</span><span class="sxs-lookup"><span data-stu-id="25fc6-140">NuGet command line</span></span>

<span data-ttu-id="25fc6-141">**NuGet komut satırı aracının en son sürümünü almak Nasıl yaparım??**</span><span class="sxs-lookup"><span data-stu-id="25fc6-141">**How do I get the latest version of NuGet command line tool?**</span></span>

<span data-ttu-id="25fc6-142">Bkz. [Install Guide](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="25fc6-142">See the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="25fc6-143">**NuGet. exe için lisans nedir?**</span><span class="sxs-lookup"><span data-stu-id="25fc6-143">**What is the license for nuget.exe?**</span></span>

<span data-ttu-id="25fc6-144">NuGet. exe ' yi MıT lisansı koşullarına göre yeniden dağıtmanıza izin verilir.</span><span class="sxs-lookup"><span data-stu-id="25fc6-144">You are allowed to redistribute nuget.exe under the terms of the MIT license.</span></span> <span data-ttu-id="25fc6-145">Yeniden dağıtmak üzere seçtiğiniz NuGet. exe ' nin tüm kopyalarını güncelleştirmeden ve bakımını yapmaktan siz sorumlusunuz.</span><span class="sxs-lookup"><span data-stu-id="25fc6-145">You are responsible for updating and servicing any copies of nuget.exe that you choose to redistribute.</span></span>

<span data-ttu-id="25fc6-146">**NuGet komut satırı aracını genişletmek mümkün mü?**</span><span class="sxs-lookup"><span data-stu-id="25fc6-146">**Is it possible to extend the NuGet command line tool?**</span></span>

<span data-ttu-id="25fc6-147">Evet, [ramiz Reynold 'ın Post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx)bölümünde açıklandığı `nuget.exe`gibi öğesine özel komutlar eklemek mümkündür.</span><span class="sxs-lookup"><span data-stu-id="25fc6-147">Yes, it's possible to add custom commands to `nuget.exe`, as described in [Rob Reynold's post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span></span>

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a><span data-ttu-id="25fc6-148">NuGet Paket Yöneticisi Konsolu (Windows üzerinde Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="25fc6-148">NuGet Package Manager Console (Visual Studio on Windows)</span></span>

<span data-ttu-id="25fc6-149">**Nasıl yaparım? Paket Yöneticisi konsolundaki DTE nesnesine erişim izni veriyor musunuz?**</span><span class="sxs-lookup"><span data-stu-id="25fc6-149">**How do I get access to the DTE object in the Package Manager console?**</span></span>

<span data-ttu-id="25fc6-150">Visual Studio Automation nesne modelindeki en üst düzey nesneye DTE (geliştirme araçları ortamı) nesnesi denir.</span><span class="sxs-lookup"><span data-stu-id="25fc6-150">The top-level object in the Visual Studio automation object model is called the DTE (Development Tools Environment) object.</span></span> <span data-ttu-id="25fc6-151">Konsol bunu adlı `$DTE`bir değişken aracılığıyla sağlar.</span><span class="sxs-lookup"><span data-stu-id="25fc6-151">The console provides this through a variable named `$DTE`.</span></span> <span data-ttu-id="25fc6-152">Daha fazla bilgi için bkz. Visual Studio genişletilebilirlik belgelerindeki [Otomasyon modeline genel bakış](/visualstudio/extensibility/internals/automation-model-overview) .</span><span class="sxs-lookup"><span data-stu-id="25fc6-152">For more information, see [Automation Model Overview](/visualstudio/extensibility/internals/automation-model-overview) in the Visual Studio Extensibility documentation.</span></span>

<span data-ttu-id="25fc6-153">**$DTE değişkenini DTE2 türüne dönüştürmeye çalışırsam, ancak bir hata alıyorum: "EnvDTE. DTEClass" türündeki "EnvDTE. DTEClass" değeri "EnvDTE80. DTE2" türüne dönüştürülemez. Ne oldu?**</span><span class="sxs-lookup"><span data-stu-id="25fc6-153">**I try to cast the $DTE variable to the type DTE2, but I get an error: Cannot convert the "EnvDTE.DTEClass" value of type "EnvDTE.DTEClass" to type "EnvDTE80.DTE2". What's wrong?**</span></span>

<span data-ttu-id="25fc6-154">Bu, PowerShell 'in bir COM nesnesiyle etkileşime girdiği bilinen bir sorundur.</span><span class="sxs-lookup"><span data-stu-id="25fc6-154">This is a known issue with how PowerShell interacts with a COM object.</span></span> <span data-ttu-id="25fc6-155">Aşağıdakileri deneyin:</span><span class="sxs-lookup"><span data-stu-id="25fc6-155">Try the following:</span></span>

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

<span data-ttu-id="25fc6-156">`Get-Interface`, NuGet PowerShell ana bilgisayarı tarafından eklenen bir yardımcı işlevdir.</span><span class="sxs-lookup"><span data-stu-id="25fc6-156">`Get-Interface` is a helper function added by the NuGet PowerShell host.</span></span>

## <a name="creating-and-publishing-packages"></a><span data-ttu-id="25fc6-157">Paket oluşturma ve yayımlama</span><span class="sxs-lookup"><span data-stu-id="25fc6-157">Creating and publishing packages</span></span>

<span data-ttu-id="25fc6-158">**Nasıl yaparım? bir akışta paketmi Listele?**</span><span class="sxs-lookup"><span data-stu-id="25fc6-158">**How do I list my package in a feed?**</span></span>

<span data-ttu-id="25fc6-159">Bkz. [paket oluşturma ve yayımlama](../quickstart/create-and-publish-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="25fc6-159">See [Creating and publishing a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="25fc6-160">**.NET Framework farklı sürümlerini hedefleyen kitaplığımın birden çok sürümü var. Bunu destekleyen tek bir paket mi Nasıl yaparım??**</span><span class="sxs-lookup"><span data-stu-id="25fc6-160">**I have multiple versions of my library that target different versions of the .NET Framework. How do I build a single package that supports this?**</span></span>

<span data-ttu-id="25fc6-161">Bkz. [birden çok .NET Framework sürümünü ve profilini destekleme](../create-packages/supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="25fc6-161">See [Supporting Multiple .NET Framework Versions and Profiles](../create-packages/supporting-multiple-target-frameworks.md).</span></span>

<span data-ttu-id="25fc6-162">**Kendi deponuzu mi yoksa akışımı mı ayarlamak Nasıl yaparım??**</span><span class="sxs-lookup"><span data-stu-id="25fc6-162">**How do I set up my own repository or feed?**</span></span>

<span data-ttu-id="25fc6-163">[Barındırma paketlerine genel bakış](../hosting-packages/overview.md)bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="25fc6-163">See the [Hosting packages overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="25fc6-164">**Paketleri toplu olarak NuGet akışımla nasıl karşıya yükleyebilirim?**</span><span class="sxs-lookup"><span data-stu-id="25fc6-164">**How can I upload packages to my NuGet feed in bulk?**</span></span>

<span data-ttu-id="25fc6-165">Bkz. [toplu yayımlama NuGet paketleri](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span><span class="sxs-lookup"><span data-stu-id="25fc6-165">See [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span></span>

## <a name="working-with-packages"></a><span data-ttu-id="25fc6-166">Paketlerle çalışma</span><span class="sxs-lookup"><span data-stu-id="25fc6-166">Working with packages</span></span>

<span data-ttu-id="25fc6-167">**Proje düzeyi paket ve çözüm düzeyi paket arasındaki fark nedir?**</span><span class="sxs-lookup"><span data-stu-id="25fc6-167">**What is the difference between a project-level package and a solution-level package?**</span></span>

<span data-ttu-id="25fc6-168">Çözüm düzeyindeki bir paket (NuGet 3. x +) bir çözüme yalnızca bir kez yüklenir ve ardından Çözümdeki tüm projeler için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="25fc6-168">A solution-level package (NuGet 3.x+) is installed only once in a solution and is then available for all projects in the solution.</span></span> <span data-ttu-id="25fc6-169">Proje düzeyindeki bir paket, onu kullanan her bir projeye yüklenir.</span><span class="sxs-lookup"><span data-stu-id="25fc6-169">A project-level package is installed in each project that uses it.</span></span> <span data-ttu-id="25fc6-170">Çözüm düzeyindeki bir paket, Paket Yöneticisi konsolu içinden çağrılabilecek yeni komutlar de yükleyebilir.</span><span class="sxs-lookup"><span data-stu-id="25fc6-170">A solution-level package might also install new commands that can be called from within the Package Manager Console.</span></span>

<span data-ttu-id="25fc6-171">**Internet bağlantısı olmadan NuGet paketleri yüklenebilirsin mi?**</span><span class="sxs-lookup"><span data-stu-id="25fc6-171">**Is it possible to install NuGet packages without Internet connectivity?**</span></span>

<span data-ttu-id="25fc6-172">Evet, bkz. Scott Hanselman 'ın blog gönderisi [NuGet.org kapalıysa (veya bir düzlemde olduğunuzda) NuGet 'e erişme](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (Hanselman.com).</span><span class="sxs-lookup"><span data-stu-id="25fc6-172">Yes, see Scott Hanselman's Blog post [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span></span>

<span data-ttu-id="25fc6-173">**Paketler, varsayılan paketler klasöründen farklı bir konuma yüklensin mi Nasıl yaparım??**</span><span class="sxs-lookup"><span data-stu-id="25fc6-173">**How do I install packages in a different location from the default packages folder?**</span></span>

<span data-ttu-id="25fc6-174">' [`repositoryPath`](../reference/nuget-config-file.md#config-section) `nuget config -set repositoryPath=<path>`Da ayarını kullanarak ayarlayın. `Nuget.Config`</span><span class="sxs-lookup"><span data-stu-id="25fc6-174">Set the [`repositoryPath`](../reference/nuget-config-file.md#config-section) setting in `Nuget.Config` using `nuget config -set repositoryPath=<path>`.</span></span>

<span data-ttu-id="25fc6-175">**Nasıl yaparım? NuGet paketleri klasörünü kaynak denetimine eklemektan kaçının mi?**</span><span class="sxs-lookup"><span data-stu-id="25fc6-175">**How do I avoid adding the NuGet packages folder into to source control?**</span></span>

<span data-ttu-id="25fc6-176">' İ ' `Nuget.Config` olarak ayarlayın. `true` [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section)</span><span class="sxs-lookup"><span data-stu-id="25fc6-176">Set the [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) in `Nuget.Config` to `true`.</span></span> <span data-ttu-id="25fc6-177">Bu anahtar çözüm düzeyinde çalışarak, `$(Solutiondir)\.nuget\Nuget.Config` bu nedenle dosyaya eklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="25fc6-177">This key works at the solution level and hence need to be added to the `$(Solutiondir)\.nuget\Nuget.Config` file.</span></span> <span data-ttu-id="25fc6-178">Visual Studio 'dan paket geri yüklemeyi etkinleştirmek bu dosyayı otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="25fc6-178">Enabling package restore from Visual Studio creates this file automatically.</span></span>

<span data-ttu-id="25fc6-179">**Paket geri yükleme Nasıl yaparım? kapatılsın mı?**</span><span class="sxs-lookup"><span data-stu-id="25fc6-179">**How do I turn off package restore?**</span></span>

<span data-ttu-id="25fc6-180">Bkz. [paket geri yüklemeyi etkinleştirme ve devre dışı bırakma](../consume-packages/package-restore.md#enable-and-disable-package-restore-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="25fc6-180">See [Enabling and disabling package restore](../consume-packages/package-restore.md#enable-and-disable-package-restore-visual-studio).</span></span>

<span data-ttu-id="25fc6-181">**Uzak bağımlılıklara sahip yerel bir paket yüklerken neden "bağımlılık hatası çözümlenemiyor" ifadesini alıyorum?**</span><span class="sxs-lookup"><span data-stu-id="25fc6-181">**Why do I get an "Unable to resolve dependency error" when installing a local package with remote dependencies?**</span></span>

<span data-ttu-id="25fc6-182">Projeye yerel bir paket yüklerken **Tüm** kaynağı seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="25fc6-182">You need to select the **All** source when installing a local package into the project.</span></span> <span data-ttu-id="25fc6-183">Bu, yalnızca bir tane kullanmak yerine tüm akışların toplamlarını toplar.</span><span class="sxs-lookup"><span data-stu-id="25fc6-183">This aggregates all the feeds instead of using just one.</span></span> <span data-ttu-id="25fc6-184">Bu hatanın nedeni, yerel bir deponun kullanıcıları genellikle şirket ilkeleri nedeniyle yanlışlıkla uzak bir paket yüklemeyi önlemek istemesidir.</span><span class="sxs-lookup"><span data-stu-id="25fc6-184">The reason this error appears is that users of a local repository often want to avoid accidentally installing a remote package due to corporate polices.</span></span>

<span data-ttu-id="25fc6-185">**Aynı klasörde birden fazla projem var, her proje için ayrı Packages. config dosyalarını nasıl kullanabilirim?**</span><span class="sxs-lookup"><span data-stu-id="25fc6-185">**I have multiple projects in the same folder, how can I use separate packages.config files for each project?**</span></span>

<span data-ttu-id="25fc6-186">Ayrı projelerin ayrı klasörlerde bulunduğu çoğu projede, NuGet her bir projedeki dosyaları tanımladığı için `packages.config` bu bir sorun değildir.</span><span class="sxs-lookup"><span data-stu-id="25fc6-186">In most projects where separate projects live in separate folders, this is not a problem as NuGet identifies the `packages.config` files in each project.</span></span> <span data-ttu-id="25fc6-187">NuGet 3.3 + ve aynı klasörde birden çok proje ile, projenin `packages.config` adını dosya adlarıyla `packages.{project-name}.config`ekleyebilirsiniz ve NuGet bu dosyayı kullanır.</span><span class="sxs-lookup"><span data-stu-id="25fc6-187">With NuGet 3.3+ and multiple projects in the same folder, you can insert the name of the project into the `packages.config` filenames use the pattern `packages.{project-name}.config`, and NuGet uses that file.</span></span>

<span data-ttu-id="25fc6-188">Her proje dosyası kendi bağımlılıklar listesini içerdiğinden, PackageReference kullanılırken bu bir sorun değildir.</span><span class="sxs-lookup"><span data-stu-id="25fc6-188">This is not an issue when using PackageReference, as each project file contains its own list of dependencies.</span></span>

<span data-ttu-id="25fc6-189">**Depolar listemdeki nuget.org görmüyorum, nasıl geri alabilirim?**</span><span class="sxs-lookup"><span data-stu-id="25fc6-189">**I don't see nuget.org in my list of repositories, how do I get it back?**</span></span>

- <span data-ttu-id="25fc6-190">Kaynak `https://api.nuget.org/v3/index.json` listenize ekleyin veya</span><span class="sxs-lookup"><span data-stu-id="25fc6-190">Add `https://api.nuget.org/v3/index.json` to your list of sources, or</span></span>
- <span data-ttu-id="25fc6-191">( `%appdata%\.nuget\NuGet.Config` Windows) veya `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) öğesini silin ve NuGet 'in yeniden oluşturmasını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="25fc6-191">Delete `%appdata%\.nuget\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) and let NuGet re-create it.</span></span>
