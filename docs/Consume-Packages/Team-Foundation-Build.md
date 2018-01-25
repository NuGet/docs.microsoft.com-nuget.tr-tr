---
title: "İzlenecek yol NuGet paketinin geri yükleme ile Team Foundation derlemesi | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Nasıl NuGet paket geri yükleme işlemi ile Team Foundation Build (TFS ve Visual Studio Team Services) ile bir gözden geçirme."
keywords: "NuGet paket geri yüklemesi, NuGet ve TFS, NuGet ve VSTS, NuGet yapı sistemleri, team foundation derlemesi, özel MSBuild projelerine bulut yapı, sürekli tümleştirme"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a90b4bb9bd3a5b9200179ab16f16b276abcda981
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2018
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a><span data-ttu-id="6df3b-104">Paket geri yüklemesi Team Foundation Build ile ayarlama</span><span class="sxs-lookup"><span data-stu-id="6df3b-104">Setting up package restore with Team Foundation Build</span></span>

<span data-ttu-id="6df3b-105">Bu makale, paketleri bir parçası olarak geri yükleme konusunda ayrıntılı bilgi sağlar. [Hizmetleri ekip](/vsts/build-release/index) her ikisi de hem Git hem de Team Services sürüm denetimi.</span><span class="sxs-lookup"><span data-stu-id="6df3b-105">This article provides a detailed walkthrough on how to restore packages as part of the [Team Services Build](/vsts/build-release/index) both, for both Git and Team Services Version Control.</span></span>

<span data-ttu-id="6df3b-106">Bu kılavuzda Visual Studio Team Services kullanarak bu senaryo için belirli olsa da, kavramlar, ayrıca diğer sürüm denetimine uygulamak ve sistemler oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="6df3b-106">Although this walkthrough is specific for the scenario of using Visual Studio Team Services, the concepts also apply to other version control and build systems.</span></span>

<span data-ttu-id="6df3b-107">Uygulandığı öğe:</span><span class="sxs-lookup"><span data-stu-id="6df3b-107">Applies To:</span></span>

- <span data-ttu-id="6df3b-108">Herhangi bir TFS sürümü özel MSBuild projelerine</span><span class="sxs-lookup"><span data-stu-id="6df3b-108">Custom MSBuild projects running on any version of TFS</span></span>
- <span data-ttu-id="6df3b-109">Team Foundation Server 2012 veya önceki</span><span class="sxs-lookup"><span data-stu-id="6df3b-109">Team Foundation Server 2012 or earlier</span></span>
- <span data-ttu-id="6df3b-110">TFS 2013 veya sonraki bir sürüme özel Team Foundation Yapı işlem şablonları geçişi</span><span class="sxs-lookup"><span data-stu-id="6df3b-110">Custom Team Foundation Build Process Templates migrated to TFS 2013 or later</span></span>
- <span data-ttu-id="6df3b-111">İşlem şablonları kaldırılan Nuget geri yükleme işlevselliği ile derleme</span><span class="sxs-lookup"><span data-stu-id="6df3b-111">Build Process Templates With Nuget Restore functionality removed</span></span>

<span data-ttu-id="6df3b-112">Alt yapı işlem şablonları ile Visual Studio Team Services veya Team Foundation Server 2013 kullanıyorsanız, otomatik paket geri yüklemesi oluşturma işleminin bir parçası olarak gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="6df3b-112">If you're using Visual Studio Team Services or Team Foundation Server 2013 with its build process templates, automatic package restore happens as part of the build process.</span></span>

## <a name="the-general-approach"></a><span data-ttu-id="6df3b-113">Genel yaklaşım</span><span class="sxs-lookup"><span data-stu-id="6df3b-113">The general approach</span></span>

<span data-ttu-id="6df3b-114">NuGet kullanarak bir avantajı, onu ikili dosyalarının sürüm denetim sisteminiz için iade önlemek için kullanabileceğiniz olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="6df3b-114">An advantage of using NuGet is that you can use it to avoid checking in binaries to your version control system.</span></span>

<span data-ttu-id="6df3b-115">Bu kullanıyorsanız özellikle ilginç bir [dağıtılmış sürüm denetim](http://en.wikipedia.org/wiki/Distributed_revision_control) geliştiriciler, yerel olarak çalışmaya başlamadan önce tam geçmişi dahil olmak üzere tüm depoyu kopyalayın gerektiğinden git gibi sistem.</span><span class="sxs-lookup"><span data-stu-id="6df3b-115">This is especially interesting if you are using a [distributed version control](http://en.wikipedia.org/wiki/Distributed_revision_control) system like git because developers need to clone the entire repository, including the full history, before they can start working locally.</span></span> <span data-ttu-id="6df3b-116">İkili dosyalar genellikle delta sıkıştırma kaydedildikçe ikili dosyalarda denetimi önemli deposu oluşan şişirmeyi neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="6df3b-116">Checking in binaries can cause significant repository bloat as binary files are typically stored without delta compression.</span></span>

<span data-ttu-id="6df3b-117">NuGet desteklenen [paketleri geri](../consume-packages/package-restore.md) derleme için uzun bir parçası olarak şimdi saat.</span><span class="sxs-lookup"><span data-stu-id="6df3b-117">NuGet has supported [restoring packages](../consume-packages/package-restore.md) as part of the build for a long time now.</span></span> <span data-ttu-id="6df3b-118">Önceki uygulaması proje oluşturulurken NuGet paketleri geri çünkü derleme işlemini genişletme istediğiniz paketler için tavuk ve Yumurta sorunu yaşıyor.</span><span class="sxs-lookup"><span data-stu-id="6df3b-118">The previous implementation had a chicken-and-egg problem for packages that want to extend the build process because NuGet restored packages while building the project.</span></span> <span data-ttu-id="6df3b-119">Ancak, MSBuild yapı oluşturma sırasında genişletme izin vermez; bir karşıdır bu MSBuild bir sorunu ancak bu devralınan bir sorun olduğunu savunabilir.</span><span class="sxs-lookup"><span data-stu-id="6df3b-119">However, MSBuild doesn't allow extending the build during the build; one could argue that this an issue in MSBuild but I would argue that this is an inherent problem.</span></span> <span data-ttu-id="6df3b-120">Genişletmek için gereken hangi en boy bağlı olarak, paketi geri yüklemesi zamanına göre kaydetmek için çok geç olabilir.</span><span class="sxs-lookup"><span data-stu-id="6df3b-120">Depending on which aspect you need to extend it might be too late to register by the time your package is restored.</span></span>

<span data-ttu-id="6df3b-121">Bu sorunun kurut paketler derleme işlemindeki ilk adım olarak geri emin yapılmasıdır.</span><span class="sxs-lookup"><span data-stu-id="6df3b-121">The cure to this problem is making sure that packages are restored as the first step in the build process.</span></span> <span data-ttu-id="6df3b-122">NuGet 2.7 + bu basitleştirilmiş bir komut satırı kolaylaştırır:</span><span class="sxs-lookup"><span data-stu-id="6df3b-122">NuGet 2.7+ makes this easy via a simplified command line:</span></span>

```cli
nuget restore path\to\solution.sln
```

<span data-ttu-id="6df3b-123">Derleme sürecinde kod oluşturmadan önce paketleri yüklediğinde, iade gerekmez `.targets` dosyaları</span><span class="sxs-lookup"><span data-stu-id="6df3b-123">When your build process restores packages before building the code, you don't need to check-in `.targets` files</span></span>

> [!Note]
> <span data-ttu-id="6df3b-124">Paketleri yükleme Visual Studio'da izin vermek için yazılmış olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6df3b-124">Packages must be authored to allow loading in Visual Studio.</span></span> <span data-ttu-id="6df3b-125">Aksi takdirde, hala iade isteyebilirsiniz `.targets` diğer geliştiriciler çözüm paketlerini ilk geri yüklemek zorunda kalmadan açabilirler böylece dosyaları.</span><span class="sxs-lookup"><span data-stu-id="6df3b-125">Otherwise, you may still want to check in `.targets` files so that other developers can simply open the solution without having to restore packages first.</span></span>

<span data-ttu-id="6df3b-126">Aşağıdaki gösterim proje derleme şekilde ayarlamak gösterilmektedir, `packages` klasörleri ve `.targets` dosyaları iade edildi olması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="6df3b-126">The following demo project shows how to set up the build in such a way that the `packages` folders and `.targets` files don't need to be checked-in.</span></span> <span data-ttu-id="6df3b-127">Ayrıca, bu örnek proje için Team Foundation Service üzerinde otomatik bir yapı ayarlamak nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="6df3b-127">It also shows how to set up an automated build on the Team Foundation Service for this sample project.</span></span>

## <a name="repository-structure"></a><span data-ttu-id="6df3b-128">Depo yapısı</span><span class="sxs-lookup"><span data-stu-id="6df3b-128">Repository structure</span></span>

<span data-ttu-id="6df3b-129">Tanıtım Projemizin sorgu Bing komut satırı bağımsız değişkeni kullanan bir basit komut satırı aracıdır.</span><span class="sxs-lookup"><span data-stu-id="6df3b-129">Our demo project is a simple command line tool that uses the command line argument to query Bing.</span></span> <span data-ttu-id="6df3b-130">.NET Framework 4 hedefler ve birçok kullanan [BCL paketleri](http://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async), ve [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)).</span><span class="sxs-lookup"><span data-stu-id="6df3b-130">It targets the .NET Framework 4 and uses many of the [BCL packages](http://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async), and [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)).</span></span>

<span data-ttu-id="6df3b-131">Depo yapısı şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="6df3b-131">The structure of the repository looks as follows:</span></span>

    <Project>
        │   .gitignore
        │   .tfignore
        │   build.proj
        │
        ├───src
        │   │   BingSearcher.sln
        │   │
        │   └───BingSearcher
        │       │   App.config
        │       │   BingSearcher.csproj
        │       │   packages.config
        │       │   Program.cs
        │       │
        │       └───Properties
        │               AssemblyInfo.cs
        │
        └───tools
            └───NuGet
                    nuget.exe

<span data-ttu-id="6df3b-132">Biz iade edildi, henüz gördüğünüz `packages` ya da herhangi bir klasör `.targets` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="6df3b-132">You can see that we haven't checked-in the `packages` folder nor any `.targets` files.</span></span>

<span data-ttu-id="6df3b-133">Biz ancak iade edildi olan `nuget.exe` derleme sırasında gerektiğinde.</span><span class="sxs-lookup"><span data-stu-id="6df3b-133">We have, however, checked-in the `nuget.exe` as it's needed during the build.</span></span> <span data-ttu-id="6df3b-134">Aşağıdaki yaygın olarak kullanılan biz iade, paylaşılan altında kuralları `tools` klasör.</span><span class="sxs-lookup"><span data-stu-id="6df3b-134">Following widely used conventions we've checked it in under a shared `tools` folder.</span></span>

<span data-ttu-id="6df3b-135">Kaynak kodu altındadır `src` klasör.</span><span class="sxs-lookup"><span data-stu-id="6df3b-135">The source code is under the `src` folder.</span></span> <span data-ttu-id="6df3b-136">Kendi Tanıtımı yalnızca tek bir çözüm kullansa da, bu klasör, birden fazla çözüm içeriyor kolayca düşünebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6df3b-136">Although our demo only uses a single solution, you can easily imagine that this folder contains more than one solution.</span></span>

### <a name="ignore-files"></a><span data-ttu-id="6df3b-137">Dosyaları yoksayma</span><span class="sxs-lookup"><span data-stu-id="6df3b-137">Ignore files</span></span>

> [!Note]
> <span data-ttu-id="6df3b-138">Var. şu anda bir [NuGet istemci bilinen hata](https://nuget.codeplex.com/workitem/4072) hala eklemek istemci neden `packages` sürüm denetimi klasörüne.</span><span class="sxs-lookup"><span data-stu-id="6df3b-138">There is currently a [known bug in the NuGet client](https://nuget.codeplex.com/workitem/4072) that causes the client to still add the `packages` folder to version control.</span></span> <span data-ttu-id="6df3b-139">Kaynak denetimi tümleştirmesi devre dışı bırakmak için bir çözüm olabilir.</span><span class="sxs-lookup"><span data-stu-id="6df3b-139">A workaround is to disable the source control integration.</span></span> <span data-ttu-id="6df3b-140">Bunu yapmak için gerekir bir `Nuget.Config ` dosyasını `.nuget` çözümünüze paralel klasör.</span><span class="sxs-lookup"><span data-stu-id="6df3b-140">In order to do that, you'll need a `Nuget.Config ` file in the  `.nuget` folder that is parallel to your solution.</span></span> <span data-ttu-id="6df3b-141">Bu klasör henüz mevcut değilse, bunu oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6df3b-141">If this folder doesn't exist yet, you'll need to create it.</span></span> <span data-ttu-id="6df3b-142">İçinde [ `Nuget.Config` ](../consume-packages/configuring-nuget-behavior.md), aşağıdaki içeriği ekleyin:</span><span class="sxs-lookup"><span data-stu-id="6df3b-142">In [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md), add the following content:</span></span>

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```

<span data-ttu-id="6df3b-143">Sürüm denetimine biz giriş yapma yok iletişim kurmak için **paketleri** klasörleri ayrıca eklediğimiz yoksaymak için her iki git dosyaları (`.gitignore`) TF sürüm denetimi yanı sıra (`.tfignore`).</span><span class="sxs-lookup"><span data-stu-id="6df3b-143">To communicate to version control that we don’t intent to check-in the **packages** folders, we've also added ignore files for both git (`.gitignore`) as well as TF version control (`.tfignore`).</span></span> <span data-ttu-id="6df3b-144">Bu dosyaları iade istemediğiniz dosyaların desenleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="6df3b-144">These files describes patterns of files you don't want to check-in.</span></span>

<span data-ttu-id="6df3b-145">`.gitignore` Dosya şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="6df3b-145">The `.gitignore` file looks as follows:</span></span>

    syntax: glob
    *.user
    *.suo
    bin
    obj
    packages

<span data-ttu-id="6df3b-146">`.gitignore` Dosyası [oldukça güçlü](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span><span class="sxs-lookup"><span data-stu-id="6df3b-146">The `.gitignore` file is [quite powerful](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span></span> <span data-ttu-id="6df3b-147">Örneğin, genellikle içeriğini iade değil istiyorsanız `packages` klasör ancak denetleme önceki yönlendirme ile gitmek istiyorsanız `.targets` sahip olabilir, aşağıdaki dosyaları kural bunun yerine:</span><span class="sxs-lookup"><span data-stu-id="6df3b-147">For example, if you want to generally not check-in the contents of the `packages` folder but want to go with previous guidance of checking in the `.targets` files you could have the following rule instead:</span></span>

    packages
    !packages/**/*.targets

<span data-ttu-id="6df3b-148">Bu tüm dışlayacak `packages` klasörleri ancak olacak yeniden dahil tüm kapsanan `.targets` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="6df3b-148">This will exclude all `packages` folders but will re-include all contained `.targets` files.</span></span> <span data-ttu-id="6df3b-149">İçin bir şablon isteyenlerin bulabilirsiniz `.gitignore` Visual Studio geliştiriciler ihtiyaçlarını için özellikle tasarlanmış dosyaları [burada](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span><span class="sxs-lookup"><span data-stu-id="6df3b-149">By the way, you can find a template for `.gitignore` files that is specifically tailored for the needs of Visual Studio developers [here](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>

<span data-ttu-id="6df3b-150">TF sürüm denetimi destekleyen çok benzer bir mekanizma aracılığıyla [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) dosya.</span><span class="sxs-lookup"><span data-stu-id="6df3b-150">TF version control supports a very similar mechanism via the [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) file.</span></span> <span data-ttu-id="6df3b-151">Neredeyse aynı söz dizimi:</span><span class="sxs-lookup"><span data-stu-id="6df3b-151">The syntax is virtually the same:</span></span>

    *.user
    *.suo
    bin
    obj
    packages

## <a name="buildproj"></a><span data-ttu-id="6df3b-152">build.proj</span><span class="sxs-lookup"><span data-stu-id="6df3b-152">build.proj</span></span>

<span data-ttu-id="6df3b-153">Kendi tanıtımı için biz oluşturma işlemi oldukça basit tutun.</span><span class="sxs-lookup"><span data-stu-id="6df3b-153">For our demo, we keep the build process fairly simple.</span></span> <span data-ttu-id="6df3b-154">Çözümler oluşturulmadan önce paketleri geri yüklendiğini emin olmasını sağlarken tüm çözümler oluşturan MSBuild Projesi oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="6df3b-154">We'll create an MSBuild project that builds all solutions while making sure that packages are restored before building the solutions.</span></span>

<span data-ttu-id="6df3b-155">Bu proje üç geleneksel hedefleri olacaktır `Clean`, `Build` ve `Rebuild` yeni bir hedef yanı sıra `RestorePackages`.</span><span class="sxs-lookup"><span data-stu-id="6df3b-155">This project will have the three conventional targets `Clean`, `Build` and `Rebuild` as well as a new target `RestorePackages`.</span></span>

- <span data-ttu-id="6df3b-156">`Build` Ve `Rebuild` her ikisi de bağlıdır hedefleri `RestorePackages`.</span><span class="sxs-lookup"><span data-stu-id="6df3b-156">The `Build` and `Rebuild` targets both depend on `RestorePackages`.</span></span> <span data-ttu-id="6df3b-157">Bu, her ikisi de çalıştırabilirsiniz emin olur `Build` ve `Rebuild` ve paketleri geri yükleniyor.</span><span class="sxs-lookup"><span data-stu-id="6df3b-157">This makes sure that you can both run `Build` and `Rebuild` and rely on packages being restored.</span></span>
- <span data-ttu-id="6df3b-158">`Clean`, `Build` ve `Rebuild` tüm çözüm dosyalarını karşılık gelen MSBuild hedef çağırma.</span><span class="sxs-lookup"><span data-stu-id="6df3b-158">`Clean`, `Build` and `Rebuild` invoke the corresponding MSBuild target on all solution files.</span></span>
- <span data-ttu-id="6df3b-159">`RestorePackages` Hedef çağırır `nuget.exe` her çözüm dosyası.</span><span class="sxs-lookup"><span data-stu-id="6df3b-159">The `RestorePackages` target invokes `nuget.exe` for each solution file.</span></span> <span data-ttu-id="6df3b-160">Bu kullanarak gerçekleştirilir [toplu işleme MSBuild işlevselliği](/visualstudio/msbuild/msbuild-batching).</span><span class="sxs-lookup"><span data-stu-id="6df3b-160">This is accomplished by using [MSBuild's batching functionality](/visualstudio/msbuild/msbuild-batching).</span></span>

<span data-ttu-id="6df3b-161">Sonucu şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="6df3b-161">The result looks as follows:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project ToolsVersion="4.0"
            DefaultTargets="Build"
            xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <PropertyGroup>
    <OutDir Condition=" '$(OutDir)'=='' ">$(MSBuildThisFileDirectory)bin\</OutDir>
    <Configuration Condition=" '$(Configuration)'=='' ">Release</Configuration>
    <SourceHome Condition=" '$(SourceHome)'=='' ">$(MSBuildThisFileDirectory)src\</SourceHome>
    <ToolsHome Condition=" '$(ToolsHome)'=='' ">$(MSBuildThisFileDirectory)tools\</ToolsHome>
    </PropertyGroup>

    <ItemGroup>
    <Solution Include="$(SourceHome)*.sln">
        <AdditionalProperties>OutDir=$(OutDir);Configuration=$(Configuration)</AdditionalProperties>
    </Solution>
    </ItemGroup>

    <Target Name="RestorePackages">
    <Exec Command="&quot;$(ToolsHome)NuGet\nuget.exe&quot; restore &quot;%(Solution.Identity)&quot;" />
    </Target>

    <Target Name="Clean">
    <MSBuild Targets="Clean"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Build" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Build"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Rebuild" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Rebuild"
                Projects="@(Solution)" />
    </Target>
</Project>
```

## <a name="configuring-team-build"></a><span data-ttu-id="6df3b-162">Takım yapı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6df3b-162">Configuring Team Build</span></span>

<span data-ttu-id="6df3b-163">Ekip derlemesi çeşitli şablonlar sunar.</span><span class="sxs-lookup"><span data-stu-id="6df3b-163">Team Build offers various process templates.</span></span> <span data-ttu-id="6df3b-164">Bu Tanıtım için biz Team Foundation Service kullanıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="6df3b-164">For this demonstration, we're using the Team Foundation Service.</span></span> <span data-ttu-id="6df3b-165">TFS şirket içi yüklemeleri yine de çok benzer.</span><span class="sxs-lookup"><span data-stu-id="6df3b-165">On-premises installations of TFS will be very similar though.</span></span>

<span data-ttu-id="6df3b-166">Aşağıdaki adımlarda kullandığınız hangi sürüm denetimi sistemi bağlı olarak farklılık gösterir Git ve TF sürüm denetimi ekip farklı şablonlar vardır.</span><span class="sxs-lookup"><span data-stu-id="6df3b-166">Git and TF Version Control have different Team Build templates, so the following steps will vary depending on which version control system you are using.</span></span> <span data-ttu-id="6df3b-167">Her iki durumda da, tek ihtiyacınız seçerek build.proj oluşturmak istediğiniz projesi olarak.</span><span class="sxs-lookup"><span data-stu-id="6df3b-167">In both cases, all you need is selecting the build.proj as the project you want to build.</span></span>

<span data-ttu-id="6df3b-168">İlk olarak, git için işlem şablonu bakalım.</span><span class="sxs-lookup"><span data-stu-id="6df3b-168">First, let's look at the process template for git.</span></span> <span data-ttu-id="6df3b-169">Temel git şablonda yapı özelliği aracılığıyla seçilir `Solution to build`:</span><span class="sxs-lookup"><span data-stu-id="6df3b-169">In the git based template the build is selected via the property `Solution to build`:</span></span>

![Derleme işlemi için git](media/PackageRestoreTeamBuildGit.png)

<span data-ttu-id="6df3b-171">Bu özellik deponuzun bir konum olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="6df3b-171">Please note that this property is a location in your repository.</span></span> <span data-ttu-id="6df3b-172">Bu yana bizim `build.proj` olduğu kök dizininde yalnızca kullandık `build.proj`.</span><span class="sxs-lookup"><span data-stu-id="6df3b-172">Since our `build.proj` is in the root, we simply used `build.proj`.</span></span> <span data-ttu-id="6df3b-173">Adlı bir klasör altında derleme dosyasını yerleştirin, `tools`, değer olacaktır `tools\build.proj`.</span><span class="sxs-lookup"><span data-stu-id="6df3b-173">If you place the build file under a folder called `tools`, the value would be `tools\build.proj`.</span></span>

<span data-ttu-id="6df3b-174">TF sürüm denetimi Şablonu proje özelliği aracılığıyla seçilen `Projects`:</span><span class="sxs-lookup"><span data-stu-id="6df3b-174">In the TF version control template the project is selected via the property `Projects`:</span></span>

![TFVC'yi için derleme işlemi](media/PackageRestoreTeamBuildTFVC.png)

<span data-ttu-id="6df3b-176">Temel git şablonu TF aksine, sürüm denetimi seçiciler (sağ taraftaki üç noktalı düğmeyi) destekler.</span><span class="sxs-lookup"><span data-stu-id="6df3b-176">In contrast to the git based template the TF version control supports pickers (the button on the right hand side with the three dots).</span></span> <span data-ttu-id="6df3b-177">Bu nedenle yazım hatalarını önlemek için bunları projeyi seçmek için kullandığınız öneririz.</span><span class="sxs-lookup"><span data-stu-id="6df3b-177">So in order to avoid any typing errors we suggest you use them to select the project.</span></span>