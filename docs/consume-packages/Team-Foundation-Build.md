---
title: Team Foundation Yapısı ile NuGet paket Geri Yükleme Kılavuzu
description: NuGet paket geri yükleme ile Team Foundation Yapısı (TFS ve Visual Studio Team Services) ile nasıl bir kılavuz.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 0e69491525fce03e504d9d455bee2718510c83c2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549891"
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a><span data-ttu-id="0c630-103">Paket geri yükleme Team Foundation Yapısı ile ayarlama</span><span class="sxs-lookup"><span data-stu-id="0c630-103">Setting up package restore with Team Foundation Build</span></span>

<span data-ttu-id="0c630-104">Bu makalede, paketleri bir parçası olarak geri yükleme konusunda ayrıntılı bir kılavuz sağlar. [Team Services derleme](/vsts/build-release/index) her ikisi için hem Git hem de Team Services sürüm denetimi.</span><span class="sxs-lookup"><span data-stu-id="0c630-104">This article provides a detailed walkthrough on how to restore packages as part of the [Team Services Build](/vsts/build-release/index) both, for both Git and Team Services Version Control.</span></span>

<span data-ttu-id="0c630-105">Bu izlenecek yol Visual Studio Team Services kullanarak senaryosu için belirli olsa da, kavramları da diğer sürüm denetimi için geçerlidir ve sistemler oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="0c630-105">Although this walkthrough is specific for the scenario of using Visual Studio Team Services, the concepts also apply to other version control and build systems.</span></span>

<span data-ttu-id="0c630-106">Uygulama hedefi:</span><span class="sxs-lookup"><span data-stu-id="0c630-106">Applies To:</span></span>

- <span data-ttu-id="0c630-107">TFS herhangi bir sürümünü çalıştıran özel bir MSBuild projeleri</span><span class="sxs-lookup"><span data-stu-id="0c630-107">Custom MSBuild projects running on any version of TFS</span></span>
- <span data-ttu-id="0c630-108">Team Foundation Server 2012 veya önceki bir sürümü</span><span class="sxs-lookup"><span data-stu-id="0c630-108">Team Foundation Server 2012 or earlier</span></span>
- <span data-ttu-id="0c630-109">TFS 2013 veya sonraki bir sürüme özel Team Foundation Yapı işlem şablonlarını geçişi</span><span class="sxs-lookup"><span data-stu-id="0c630-109">Custom Team Foundation Build Process Templates migrated to TFS 2013 or later</span></span>
- <span data-ttu-id="0c630-110">Derleme işlem şablonları ile Nuget geri yükleme işlevi kaldırıldı</span><span class="sxs-lookup"><span data-stu-id="0c630-110">Build Process Templates With Nuget Restore functionality removed</span></span>

<span data-ttu-id="0c630-111">Kendi derleme işlem şablonları ile Visual Studio Team Services veya Team Foundation Server 2013 kullanıyorsanız, yapı işleminin bir parçası olarak otomatik paket geri yükleme gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="0c630-111">If you're using Visual Studio Team Services or Team Foundation Server 2013 with its build process templates, automatic package restore happens as part of the build process.</span></span>

## <a name="the-general-approach"></a><span data-ttu-id="0c630-112">Genel yaklaşım</span><span class="sxs-lookup"><span data-stu-id="0c630-112">The general approach</span></span>

<span data-ttu-id="0c630-113">NuGet kullanarak bir avantajı, sürüm denetimi Sisteminiz ikili dosyaları iade önlemek için kullanabileceğiniz olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="0c630-113">An advantage of using NuGet is that you can use it to avoid checking in binaries to your version control system.</span></span>

<span data-ttu-id="0c630-114">Bu kullanıyorsanız özellikle ilgi çekici bir [dağıtılmış sürüm denetimi](http://en.wikipedia.org/wiki/Distributed_revision_control) geliştiriciler, yerel olarak çalışmaya başlamadan önce tam geçmişini de dahil olmak üzere tüm depoyu kopyalamak gerektiği için git gibi sistem.</span><span class="sxs-lookup"><span data-stu-id="0c630-114">This is especially interesting if you are using a [distributed version control](http://en.wikipedia.org/wiki/Distributed_revision_control) system like git because developers need to clone the entire repository, including the full history, before they can start working locally.</span></span> <span data-ttu-id="0c630-115">İkili dosyalar genellikle delta sıkıştırma depolandığından ikili dosyaları denetleniyor önemli depoyu Şişirme neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="0c630-115">Checking in binaries can cause significant repository bloat as binary files are typically stored without delta compression.</span></span>

<span data-ttu-id="0c630-116">NuGet desteklenmediği [paketler geri yükleniyor](../consume-packages/package-restore.md) uzun bir süre için derlemenin bir parçası olarak artık zaman.</span><span class="sxs-lookup"><span data-stu-id="0c630-116">NuGet has supported [restoring packages](../consume-packages/package-restore.md) as part of the build for a long time now.</span></span> <span data-ttu-id="0c630-117">Önceki uygulaması için proje derlenirken NuGet paketleri geri çünkü derleme işlemini genişletme istediğiniz paketlerini tavuk ve Yumurta sorunu yaşıyor.</span><span class="sxs-lookup"><span data-stu-id="0c630-117">The previous implementation had a chicken-and-egg problem for packages that want to extend the build process because NuGet restored packages while building the project.</span></span> <span data-ttu-id="0c630-118">Ancak, MSBuild, derleme yapı sırasında genişletme izin vermez; bir buna bu MSBuild içinde bir sorun, ancak bu devralınan bir sorun olduğunu buna.</span><span class="sxs-lookup"><span data-stu-id="0c630-118">However, MSBuild doesn't allow extending the build during the build; one could argue that this an issue in MSBuild but I would argue that this is an inherent problem.</span></span> <span data-ttu-id="0c630-119">Genişletmek için gereken hangi yönüyle bağlı olarak, paket geri zaman kaydetmek için çok geç olabilir.</span><span class="sxs-lookup"><span data-stu-id="0c630-119">Depending on which aspect you need to extend it might be too late to register by the time your package is restored.</span></span>

<span data-ttu-id="0c630-120">Bu sorunun hastalıktan yapı sürecinin ilk adımı olarak paketleri geri yüklendiğinden emin yapıyor:</span><span class="sxs-lookup"><span data-stu-id="0c630-120">The cure to this problem is making sure that packages are restored as the first step in the build process:</span></span>

```cli
nuget restore path\to\solution.sln
```

<span data-ttu-id="0c630-121">Yapı işleminizin, kod oluşturulmadan önce paketleri geri yükler, iade edilmesine gerekmeyen `.targets` dosyaları</span><span class="sxs-lookup"><span data-stu-id="0c630-121">When your build process restores packages before building the code, you don't need to check-in `.targets` files</span></span>

> [!Note]
> <span data-ttu-id="0c630-122">Visual Studio'da yükleme izin vermek için paketler yeniden yazılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0c630-122">Packages must be authored to allow loading in Visual Studio.</span></span> <span data-ttu-id="0c630-123">Aksi takdirde, yine de iade isteyebileceğiniz `.targets` diğer geliştiriciler çözüm paketleri önce geri yüklemeye gerek kalmadan açabilirler dosyalar.</span><span class="sxs-lookup"><span data-stu-id="0c630-123">Otherwise, you may still want to check in `.targets` files so that other developers can simply open the solution without having to restore packages first.</span></span>

<span data-ttu-id="0c630-124">Aşağıdaki tanıtım proje derleme şekilde ayarlama işlemi gösterilmektedir, `packages` klasörleri ve `.targets` dosyaları iade olması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="0c630-124">The following demo project shows how to set up the build in such a way that the `packages` folders and `.targets` files don't need to be checked-in.</span></span> <span data-ttu-id="0c630-125">Ayrıca bu örnek project için Team Foundation Service üzerinde otomatik bir yapı ayarlama işlemini de gösterir.</span><span class="sxs-lookup"><span data-stu-id="0c630-125">It also shows how to set up an automated build on the Team Foundation Service for this sample project.</span></span>

## <a name="repository-structure"></a><span data-ttu-id="0c630-126">Depo yapısı</span><span class="sxs-lookup"><span data-stu-id="0c630-126">Repository structure</span></span>

<span data-ttu-id="0c630-127">Tanıtım Projemizin sorgu Bing komut satırı bağımsız değişkeni kullanan bir basit bir komut satırı aracıdır.</span><span class="sxs-lookup"><span data-stu-id="0c630-127">Our demo project is a simple command line tool that uses the command line argument to query Bing.</span></span> <span data-ttu-id="0c630-128">.NET Framework 4 hedefleyen ve birçok kullanan [BCL paketleri](http://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async), ve [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)).</span><span class="sxs-lookup"><span data-stu-id="0c630-128">It targets the .NET Framework 4 and uses many of the [BCL packages](http://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async), and [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)).</span></span>

<span data-ttu-id="0c630-129">Depo yapısı şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="0c630-129">The structure of the repository looks as follows:</span></span>

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

<span data-ttu-id="0c630-130">Şu iade, henüz gördüğünüz `packages` klasörünün veya `.targets` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="0c630-130">You can see that we haven't checked-in the `packages` folder nor any `.targets` files.</span></span>

<span data-ttu-id="0c630-131">Biz ancak iade olan `nuget.exe` yapı sırasında gerektiğinde.</span><span class="sxs-lookup"><span data-stu-id="0c630-131">We have, however, checked-in the `nuget.exe` as it's needed during the build.</span></span> <span data-ttu-id="0c630-132">Aşağıdaki yaygın olarak kullanılan kuralları biz iade, paylaşılan altında `tools` klasör.</span><span class="sxs-lookup"><span data-stu-id="0c630-132">Following widely used conventions we've checked it in under a shared `tools` folder.</span></span>

<span data-ttu-id="0c630-133">Kaynak kodu altındadır `src` klasör.</span><span class="sxs-lookup"><span data-stu-id="0c630-133">The source code is under the `src` folder.</span></span> <span data-ttu-id="0c630-134">Tanıtımımızı yalnızca tek bir çözüm kullansa da, bu klasör, birden fazla çözüm içeriyor kolayca hayal edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0c630-134">Although our demo only uses a single solution, you can easily imagine that this folder contains more than one solution.</span></span>

### <a name="ignore-files"></a><span data-ttu-id="0c630-135">Dosyaları yoksayma</span><span class="sxs-lookup"><span data-stu-id="0c630-135">Ignore files</span></span>

> [!Note]
> <span data-ttu-id="0c630-136">Şu anda bir [NuGet istemci bilinen hata](https://nuget.codeplex.com/workitem/4072) hala eklemek istemci neden `packages` sürüm denetimi klasörü.</span><span class="sxs-lookup"><span data-stu-id="0c630-136">There is currently a [known bug in the NuGet client](https://nuget.codeplex.com/workitem/4072) that causes the client to still add the `packages` folder to version control.</span></span> <span data-ttu-id="0c630-137">Kaynak denetimi tümleştirmesi devre dışı bırakmak için bir çözüm olabilir.</span><span class="sxs-lookup"><span data-stu-id="0c630-137">A workaround is to disable the source control integration.</span></span> <span data-ttu-id="0c630-138">Bunu yapmak için bir `Nuget.Config ` dosyası `.nuget` çözümünüze paralel klasör.</span><span class="sxs-lookup"><span data-stu-id="0c630-138">In order to do that, you need a `Nuget.Config ` file in the  `.nuget` folder that is parallel to your solution.</span></span> <span data-ttu-id="0c630-139">Bu klasörü henüz yoksa, oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0c630-139">If this folder doesn't exist yet, you need to create it.</span></span> <span data-ttu-id="0c630-140">İçinde [ `Nuget.Config` ](../consume-packages/configuring-nuget-behavior.md), aşağıdaki içeriği ekleyin:</span><span class="sxs-lookup"><span data-stu-id="0c630-140">In [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md), add the following content:</span></span>

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```

<span data-ttu-id="0c630-141">Sürüm denetimi için biz iade için hedefi yok iletişim kurmak için **paketleri** klasörleri ekledik hem git dosyaları yoksay (`.gitignore`) TF sürüm denetimi yanında (`.tfignore`).</span><span class="sxs-lookup"><span data-stu-id="0c630-141">To communicate to version control that we don’t intent to check-in the **packages** folders, we've also added ignore files for both git (`.gitignore`) as well as TF version control (`.tfignore`).</span></span> <span data-ttu-id="0c630-142">Bu dosyalar, dosyaların iade edilmesine istemediğiniz desenleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="0c630-142">These files describe patterns of files you don't want to check-in.</span></span>

<span data-ttu-id="0c630-143">`.gitignore` Dosya şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="0c630-143">The `.gitignore` file looks as follows:</span></span>

    syntax: glob
    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

<span data-ttu-id="0c630-144">`.gitignore` Dosyasıdır [oldukça güçlü](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span><span class="sxs-lookup"><span data-stu-id="0c630-144">The `.gitignore` file is [quite powerful](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span></span> <span data-ttu-id="0c630-145">Örneğin, genellikle içeriği iade değil istediğiniz `packages` klasör ancak iade kılavuzun önceki ile gitmek istiyorsanız `.targets` dosyaları sahip olabilir, aşağıdaki kuralı yerine:</span><span class="sxs-lookup"><span data-stu-id="0c630-145">For example, if you want to generally not check-in the contents of the `packages` folder but want to go with previous guidance of checking in the `.targets` files you could have the following rule instead:</span></span>

    packages
    !packages/**/*.targets

<span data-ttu-id="0c630-146">Bu, tüm dışladığı `packages` klasörleri ancak olacak yeniden dahil tüm kapsanan `.targets` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="0c630-146">This will exclude all `packages` folders but will re-include all contained `.targets` files.</span></span> <span data-ttu-id="0c630-147">Şekilde, bir şablon bulabilirsiniz `.gitignore` ihtiyaçlarını Visual Studio geliştiricileri için özel olarak uyarlanmıştır dosyaları [burada](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span><span class="sxs-lookup"><span data-stu-id="0c630-147">By the way, you can find a template for `.gitignore` files that is specifically tailored for the needs of Visual Studio developers [here](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>

<span data-ttu-id="0c630-148">TF sürüm denetimi destekleyen çok benzer bir mekanizma aracılığıyla [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) dosya.</span><span class="sxs-lookup"><span data-stu-id="0c630-148">TF version control supports a very similar mechanism via the [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) file.</span></span> <span data-ttu-id="0c630-149">Söz dizimi neredeyse aynıdır:</span><span class="sxs-lookup"><span data-stu-id="0c630-149">The syntax is virtually the same:</span></span>

    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

## <a name="buildproj"></a><span data-ttu-id="0c630-150">Build.proj</span><span class="sxs-lookup"><span data-stu-id="0c630-150">build.proj</span></span>

<span data-ttu-id="0c630-151">Tanıtımımızı için derleme işlemi oldukça basittir saklarız.</span><span class="sxs-lookup"><span data-stu-id="0c630-151">For our demo, we keep the build process fairly simple.</span></span> <span data-ttu-id="0c630-152">Paketleri çözüm oluşturmadan önce geri yüklendiğinden emin olmasını sağlarken tüm çözümler oluşturan bir MSBuild Projesi oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="0c630-152">We'll create an MSBuild project that builds all solutions while making sure that packages are restored before building the solutions.</span></span>

<span data-ttu-id="0c630-153">Bu projeyi üç geleneksel hedefleri olur `Clean`, `Build` ve `Rebuild` yeni bir hedef yanı sıra `RestorePackages`.</span><span class="sxs-lookup"><span data-stu-id="0c630-153">This project will have the three conventional targets `Clean`, `Build` and `Rebuild` as well as a new target `RestorePackages`.</span></span>

- <span data-ttu-id="0c630-154">`Build` Ve `Rebuild` hem de bağımlı hedefleri `RestorePackages`.</span><span class="sxs-lookup"><span data-stu-id="0c630-154">The `Build` and `Rebuild` targets both depend on `RestorePackages`.</span></span> <span data-ttu-id="0c630-155">Bu, her ikisi de çalıştırabilirsiniz xenapp'i `Build` ve `Rebuild` ve paketleri geri yükleniyor.</span><span class="sxs-lookup"><span data-stu-id="0c630-155">This makes sure that you can both run `Build` and `Rebuild` and rely on packages being restored.</span></span>
- <span data-ttu-id="0c630-156">`Clean`, `Build` ve `Rebuild` tüm çözüm dosyalarını karşılık gelen MSBuild hedef çağırır.</span><span class="sxs-lookup"><span data-stu-id="0c630-156">`Clean`, `Build` and `Rebuild` invoke the corresponding MSBuild target on all solution files.</span></span>
- <span data-ttu-id="0c630-157">`RestorePackages` Hedefini çağırır `nuget.exe` her çözüm dosyası.</span><span class="sxs-lookup"><span data-stu-id="0c630-157">The `RestorePackages` target invokes `nuget.exe` for each solution file.</span></span> <span data-ttu-id="0c630-158">Bu kullanılarak başarılır [MSBuild toplu işleme işlevleri](/visualstudio/msbuild/msbuild-batching).</span><span class="sxs-lookup"><span data-stu-id="0c630-158">This is accomplished by using [MSBuild's batching functionality](/visualstudio/msbuild/msbuild-batching).</span></span>

<span data-ttu-id="0c630-159">Sonuç şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="0c630-159">The result looks as follows:</span></span>

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

## <a name="configuring-team-build"></a><span data-ttu-id="0c630-160">Takım derlemesi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0c630-160">Configuring Team Build</span></span>

<span data-ttu-id="0c630-161">Takım derlemesi, çeşitli şablonlar sunar.</span><span class="sxs-lookup"><span data-stu-id="0c630-161">Team Build offers various process templates.</span></span> <span data-ttu-id="0c630-162">Bu Tanıtım için Team Foundation Service kullanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="0c630-162">For this demonstration, we're using the Team Foundation Service.</span></span> <span data-ttu-id="0c630-163">Şirket içi TFS yüklemeleri yine de çok benzer olacaktır.</span><span class="sxs-lookup"><span data-stu-id="0c630-163">On-premises installations of TFS will be very similar though.</span></span>

<span data-ttu-id="0c630-164">Aşağıdaki adımlarda kullandığınız hangi sürüm denetimi sistemine bağlı olarak farklılık gösterir farklı ekip şablonları, Git ve TF sürüm denetimi vardır.</span><span class="sxs-lookup"><span data-stu-id="0c630-164">Git and TF Version Control have different Team Build templates, so the following steps will vary depending on which version control system you are using.</span></span> <span data-ttu-id="0c630-165">Her iki durumda da, tüm yapmanız gereken seçmeye build.proj derlemek istediğiniz proje.</span><span class="sxs-lookup"><span data-stu-id="0c630-165">In both cases, all you need is selecting the build.proj as the project you want to build.</span></span>

<span data-ttu-id="0c630-166">İlk olarak, işlem şablonu git için göz atalım.</span><span class="sxs-lookup"><span data-stu-id="0c630-166">First, let's look at the process template for git.</span></span> <span data-ttu-id="0c630-167">Git tabanlı şablonda yapı özelliği aracılığıyla seçili `Solution to build`:</span><span class="sxs-lookup"><span data-stu-id="0c630-167">In the git based template the build is selected via the property `Solution to build`:</span></span>

![Derleme işlemi için git](media/PackageRestoreTeamBuildGit.png)

<span data-ttu-id="0c630-169">Lütfen bu özellik bir konumda bir deponuz olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="0c630-169">Please note that this property is a location in your repository.</span></span> <span data-ttu-id="0c630-170">Bu yana bizim `build.proj` olduğu kök dizininde yalnızca kullandığımız `build.proj`.</span><span class="sxs-lookup"><span data-stu-id="0c630-170">Since our `build.proj` is in the root, we simply used `build.proj`.</span></span> <span data-ttu-id="0c630-171">Derleme dosyası adlı bir klasör yerleştirmek, `tools`, değer `tools\build.proj`.</span><span class="sxs-lookup"><span data-stu-id="0c630-171">If you place the build file under a folder called `tools`, the value would be `tools\build.proj`.</span></span>

<span data-ttu-id="0c630-172">TF sürüm denetimi şablonunda özelliği aracılığıyla proje seçilen `Projects`:</span><span class="sxs-lookup"><span data-stu-id="0c630-172">In the TF version control template the project is selected via the property `Projects`:</span></span>

![TFVC için derleme işlemi](media/PackageRestoreTeamBuildTFVC.png)

<span data-ttu-id="0c630-174">Git tabanlı şablon aksine TF sürüm denetimi seçiciler (sağ taraftaki üç noktalı düğme) destekler.</span><span class="sxs-lookup"><span data-stu-id="0c630-174">In contrast to the git based template the TF version control supports pickers (the button on the right hand side with the three dots).</span></span> <span data-ttu-id="0c630-175">Bu nedenle herhangi bir yazım hatalarını önlemek için bunları projeyi seçmek için kullandığınız öneririz.</span><span class="sxs-lookup"><span data-stu-id="0c630-175">So in order to avoid any typing errors we suggest you use them to select the project.</span></span>
