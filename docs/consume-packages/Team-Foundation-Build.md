---
title: Team Foundation derlemesi ile NuGet paketi geri yükleme kılavuzu
description: NuGet paketinin Team Foundation Build (TFS ve Visual Studio Team Services) ile birlikte nasıl geri yükleneceğini gösteren bir yol.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: a86a58f8afb4b0f1affeddd47d6c5606fb465757
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610996"
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a><span data-ttu-id="9373a-103">Team Foundation derlemesi ile paket geri yüklemeyi ayarlama</span><span class="sxs-lookup"><span data-stu-id="9373a-103">Setting up package restore with Team Foundation Build</span></span>

<span data-ttu-id="9373a-104">Bu makalede, hem git hem de Team Services sürüm denetimi için [Team Services derlemesinin](/vsts/build-release/index) bir parçası olarak paketlerin nasıl geri yükleneceği hakkında ayrıntılı bir yol sunulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9373a-104">This article provides a detailed walkthrough on how to restore packages as part of the [Team Services Build](/vsts/build-release/index) both, for both Git and Team Services Version Control.</span></span>

<span data-ttu-id="9373a-105">Bu izlenecek yol Visual Studio Team Services kullanma senaryosuna özgü olsa da, kavramlar diğer sürüm denetimi ve yapı sistemleri için de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="9373a-105">Although this walkthrough is specific for the scenario of using Visual Studio Team Services, the concepts also apply to other version control and build systems.</span></span>

<span data-ttu-id="9373a-106">Uygulama hedefi:</span><span class="sxs-lookup"><span data-stu-id="9373a-106">Applies To:</span></span>

- <span data-ttu-id="9373a-107">TFS 'nin herhangi bir sürümünde çalışan özel MSBuild projeleri</span><span class="sxs-lookup"><span data-stu-id="9373a-107">Custom MSBuild projects running on any version of TFS</span></span>
- <span data-ttu-id="9373a-108">Team Foundation Server 2012 veya öncesi</span><span class="sxs-lookup"><span data-stu-id="9373a-108">Team Foundation Server 2012 or earlier</span></span>
- <span data-ttu-id="9373a-109">TFS 2013 veya sonraki bir sürüme geçirilen özel Team Foundation derleme Işlemi şablonları</span><span class="sxs-lookup"><span data-stu-id="9373a-109">Custom Team Foundation Build Process Templates migrated to TFS 2013 or later</span></span>
- <span data-ttu-id="9373a-110">NuGet geri yükleme işlevselliği kaldırılmış şekilde Işlem şablonları oluşturun</span><span class="sxs-lookup"><span data-stu-id="9373a-110">Build Process Templates With Nuget Restore functionality removed</span></span>

<span data-ttu-id="9373a-111">Yapı işlemi şablonlarıyla Visual Studio Team Services veya Team Foundation Server 2013 kullanıyorsanız, derleme işleminin bir parçası olarak otomatik paket geri yüklemesi gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="9373a-111">If you're using Visual Studio Team Services or Team Foundation Server 2013 with its build process templates, automatic package restore happens as part of the build process.</span></span>

## <a name="the-general-approach"></a><span data-ttu-id="9373a-112">Genel yaklaşım</span><span class="sxs-lookup"><span data-stu-id="9373a-112">The general approach</span></span>

<span data-ttu-id="9373a-113">NuGet kullanmanın bir avantajı, bunu, sürüm denetim sisteminize ikili dosyaları iade etmekten kaçınmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9373a-113">An advantage of using NuGet is that you can use it to avoid checking in binaries to your version control system.</span></span>

<span data-ttu-id="9373a-114">Bu özellikle, git gibi [Dağıtılmış bir sürüm denetimi](https://en.wikipedia.org/wiki/Distributed_revision_control) sistemi kullanıyorsanız, geliştiricilerin yerel olarak çalışmaya başlayabilmeleri için tam geçmiş dahil olmak üzere tüm depoyu kopyalaması gerektiğinden çok ilginç olur.</span><span class="sxs-lookup"><span data-stu-id="9373a-114">This is especially interesting if you are using a [distributed version control](https://en.wikipedia.org/wiki/Distributed_revision_control) system like git because developers need to clone the entire repository, including the full history, before they can start working locally.</span></span> <span data-ttu-id="9373a-115">İkili dosyalar genellikle değişim sıkıştırması olmadan depolandığından, ikili dosyaların iade edilirken önemli depo blobunun oluşmasına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="9373a-115">Checking in binaries can cause significant repository bloat as binary files are typically stored without delta compression.</span></span>

<span data-ttu-id="9373a-116">NuGet, yapılandırmanın bir parçası olarak uzun süredir [geri yüklemeyi](../consume-packages/package-restore.md) destekliyordu.</span><span class="sxs-lookup"><span data-stu-id="9373a-116">NuGet has supported [restoring packages](../consume-packages/package-restore.md) as part of the build for a long time now.</span></span> <span data-ttu-id="9373a-117">Önceki uygulamada, derleme işlemini genişletmek isteyen paketlere yönelik bir tavuk-yumurg sorunu vardı, çünkü projeyi oluştururken NuGet geri yüklendi paketleri.</span><span class="sxs-lookup"><span data-stu-id="9373a-117">The previous implementation had a chicken-and-egg problem for packages that want to extend the build process because NuGet restored packages while building the project.</span></span> <span data-ttu-id="9373a-118">Ancak, MSBuild derleme sırasında derlemeyi genişletmeye izin vermez; Bunlardan biri MSBuild 'deki bir sorun olduğunu, ancak bunun devralınmış bir sorun olduğunu anlıyorum.</span><span class="sxs-lookup"><span data-stu-id="9373a-118">However, MSBuild doesn't allow extending the build during the build; one could argue that this an issue in MSBuild but I would argue that this is an inherent problem.</span></span> <span data-ttu-id="9373a-119">Genişletmeniz gereken en boy düzeyine bağlı olarak, paketinizin geri yüklendiği zamana göre kaydolmak için çok geç olabilir.</span><span class="sxs-lookup"><span data-stu-id="9373a-119">Depending on which aspect you need to extend it might be too late to register by the time your package is restored.</span></span>

<span data-ttu-id="9373a-120">Bu sorunu çözmek, paketlerin derleme işlemindeki ilk adım olarak geri yüklendiğinden emin olmanızı sağlar:</span><span class="sxs-lookup"><span data-stu-id="9373a-120">The cure to this problem is making sure that packages are restored as the first step in the build process:</span></span>

```cli
nuget restore path\to\solution.sln
```

<span data-ttu-id="9373a-121">Yapı işleminiz kodu oluşturmadan önce paketleri geri yüklediğinde, `.targets` dosyaları iade etmeniz gerekmez</span><span class="sxs-lookup"><span data-stu-id="9373a-121">When your build process restores packages before building the code, you don't need to check-in `.targets` files</span></span>

> [!Note]
> <span data-ttu-id="9373a-122">Visual Studio 'da yüklemeye izin vermek için paketlerin yazılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9373a-122">Packages must be authored to allow loading in Visual Studio.</span></span> <span data-ttu-id="9373a-123">Aksi takdirde, diğer geliştiricilerin önce paketleri geri yüklemek zorunda kalmadan çözümü açabilmeleri için `.targets` dosyaları iade etmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9373a-123">Otherwise, you may still want to check in `.targets` files so that other developers can simply open the solution without having to restore packages first.</span></span>

<span data-ttu-id="9373a-124">Aşağıdaki demo projesi, `packages` klasörlerinin ve `.targets` dosyalarının iade alınması gerekmeyen şekilde derlemeyi nasıl ayarlayagösterdiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="9373a-124">The following demo project shows how to set up the build in such a way that the `packages` folders and `.targets` files don't need to be checked-in.</span></span> <span data-ttu-id="9373a-125">Ayrıca, bu örnek proje için Team Foundation Service otomatik bir derlemeyi ayarlamayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="9373a-125">It also shows how to set up an automated build on the Team Foundation Service for this sample project.</span></span>

## <a name="repository-structure"></a><span data-ttu-id="9373a-126">Depo yapısı</span><span class="sxs-lookup"><span data-stu-id="9373a-126">Repository structure</span></span>

<span data-ttu-id="9373a-127">Tanıtım projemiz, Bing sorgulamak için komut satırı bağımsız değişkenini kullanan basit bir komut satırı aracıdır.</span><span class="sxs-lookup"><span data-stu-id="9373a-127">Our demo project is a simple command line tool that uses the command line argument to query Bing.</span></span> <span data-ttu-id="9373a-128">.NET Framework 4 ' ü hedefler ve birçok [BCL paketini](https://www.nuget.org/profiles/dotnetframework/) ([Microsoft.net. http](https://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft. BCL](https://www.nuget.org/packages/Microsoft.Bcl), [Microsoft. BCL. Async](https://www.nuget.org/packages/Microsoft.Bcl.Async)ve [Microsoft. BCL. Build](https://www.nuget.org/packages/Microsoft.Bcl.Build)) kullanır.</span><span class="sxs-lookup"><span data-stu-id="9373a-128">It targets the .NET Framework 4 and uses many of the [BCL packages](https://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](https://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](https://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](https://www.nuget.org/packages/Microsoft.Bcl.Async), and [Microsoft.Bcl.Build](https://www.nuget.org/packages/Microsoft.Bcl.Build)).</span></span>

<span data-ttu-id="9373a-129">Deponun yapısı şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="9373a-129">The structure of the repository looks as follows:</span></span>

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

<span data-ttu-id="9373a-130">`packages` klasörünü veya `.targets` dosyalarını iade etmediğimiz hakkında bilgi alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9373a-130">You can see that we haven't checked-in the `packages` folder nor any `.targets` files.</span></span>

<span data-ttu-id="9373a-131">Ancak, derleme sırasında gerekli olduğu gibi `nuget.exe` iade ettik.</span><span class="sxs-lookup"><span data-stu-id="9373a-131">We have, however, checked-in the `nuget.exe` as it's needed during the build.</span></span> <span data-ttu-id="9373a-132">Yaygın olarak kullanılan kuralları paylaşılan bir `tools` klasörü altında denetliyoruz.</span><span class="sxs-lookup"><span data-stu-id="9373a-132">Following widely used conventions we've checked it in under a shared `tools` folder.</span></span>

<span data-ttu-id="9373a-133">Kaynak kodu `src` klasörünün altındadır.</span><span class="sxs-lookup"><span data-stu-id="9373a-133">The source code is under the `src` folder.</span></span> <span data-ttu-id="9373a-134">Tanıtımız yalnızca tek bir çözüm kullandığından, bu klasörün birden fazla çözüm içerdiğini kolayca hayal edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9373a-134">Although our demo only uses a single solution, you can easily imagine that this folder contains more than one solution.</span></span>

### <a name="ignore-files"></a><span data-ttu-id="9373a-135">Dosyaları yoksayma</span><span class="sxs-lookup"><span data-stu-id="9373a-135">Ignore files</span></span>

> [!Note]
> <span data-ttu-id="9373a-136">[NuGet istemcisinde](https://nuget.codeplex.com/workitem/4072) , istemcinin hala `packages` klasörünü sürüm denetimine eklemesine neden olan bilinen bir hata var.</span><span class="sxs-lookup"><span data-stu-id="9373a-136">There is currently a [known bug in the NuGet client](https://nuget.codeplex.com/workitem/4072) that causes the client to still add the `packages` folder to version control.</span></span> <span data-ttu-id="9373a-137">Kaynak denetimi tümleştirmesini devre dışı bırakmak geçici bir çözümdür.</span><span class="sxs-lookup"><span data-stu-id="9373a-137">A workaround is to disable the source control integration.</span></span> <span data-ttu-id="9373a-138">Bunu yapmak için çözümünüze paralel `.nuget` klasöründe bir `Nuget.Config ` dosyası gerekir.</span><span class="sxs-lookup"><span data-stu-id="9373a-138">In order to do that, you need a `Nuget.Config ` file in the  `.nuget` folder that is parallel to your solution.</span></span> <span data-ttu-id="9373a-139">Bu klasör henüz yoksa, oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9373a-139">If this folder doesn't exist yet, you need to create it.</span></span> <span data-ttu-id="9373a-140">[`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md), aşağıdaki içeriği ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9373a-140">In [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md), add the following content:</span></span>

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```

<span data-ttu-id="9373a-141">**Paket** klasörlerinde iade etme amacını verdiğimiz Sürüm denetimiyle iletişim kurmak için hem git (`.gitignore`) hem de TF sürüm denetimi (`.tfignore`) için de Ignore dosyalarını ekledik.</span><span class="sxs-lookup"><span data-stu-id="9373a-141">To communicate to version control that we don’t intent to check-in the **packages** folders, we've also added ignore files for both git (`.gitignore`) as well as TF version control (`.tfignore`).</span></span> <span data-ttu-id="9373a-142">Bu dosyalar iade etmek istemediğiniz dosyaların desenlerini anlatmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9373a-142">These files describe patterns of files you don't want to check-in.</span></span>

<span data-ttu-id="9373a-143">`.gitignore` dosya aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="9373a-143">The `.gitignore` file looks as follows:</span></span>

    syntax: glob
    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

<span data-ttu-id="9373a-144">`.gitignore` dosya [oldukça güçlüdür](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span><span class="sxs-lookup"><span data-stu-id="9373a-144">The `.gitignore` file is [quite powerful](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span></span> <span data-ttu-id="9373a-145">Örneğin, `packages` klasörünün içeriğini iade etmek, ancak `.targets` dosyaları iade etme hakkında önceki kılavuza gitmek istiyorsanız bunun yerine aşağıdaki kurala sahip olabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9373a-145">For example, if you want to generally not check-in the contents of the `packages` folder but want to go with previous guidance of checking in the `.targets` files you could have the following rule instead:</span></span>

    packages
    !packages/**/*.targets

<span data-ttu-id="9373a-146">Bu, tüm `packages` klasörlerini dışlayacak, ancak içerilen tüm `.targets` dosyalarını yeniden ekleyecek.</span><span class="sxs-lookup"><span data-stu-id="9373a-146">This will exclude all `packages` folders but will re-include all contained `.targets` files.</span></span> <span data-ttu-id="9373a-147">Bu şekilde, [burada](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore)Visual Studio geliştiricilerinin ihtiyaçlarını karşılamak için özel olarak uyarlanmış `.gitignore` dosyaları için bir şablon bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9373a-147">By the way, you can find a template for `.gitignore` files that is specifically tailored for the needs of Visual Studio developers [here](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>

<span data-ttu-id="9373a-148">TF Version Control, [. tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) dosyası aracılığıyla çok benzer bir mekanizmayı destekler.</span><span class="sxs-lookup"><span data-stu-id="9373a-148">TF version control supports a very similar mechanism via the [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) file.</span></span> <span data-ttu-id="9373a-149">Sözdizimi neredeyse aynıdır:</span><span class="sxs-lookup"><span data-stu-id="9373a-149">The syntax is virtually the same:</span></span>

    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

## <a name="buildproj"></a><span data-ttu-id="9373a-150">Build. proj</span><span class="sxs-lookup"><span data-stu-id="9373a-150">build.proj</span></span>

<span data-ttu-id="9373a-151">Tanıtımızın için yapı sürecini oldukça basit tutuyoruz.</span><span class="sxs-lookup"><span data-stu-id="9373a-151">For our demo, we keep the build process fairly simple.</span></span> <span data-ttu-id="9373a-152">Çözümleri oluşturmadan önce paketlerin geri yüklendiğinden emin olmak için tüm çözümleri oluşturan bir MSBuild projesi oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="9373a-152">We'll create an MSBuild project that builds all solutions while making sure that packages are restored before building the solutions.</span></span>

<span data-ttu-id="9373a-153">Bu proje üç geleneksel hedefe `Clean`, `Build` ve `Rebuild` yanı sıra yeni bir hedef `RestorePackages`sahip olacaktır.</span><span class="sxs-lookup"><span data-stu-id="9373a-153">This project will have the three conventional targets `Clean`, `Build` and `Rebuild` as well as a new target `RestorePackages`.</span></span>

- <span data-ttu-id="9373a-154">`Build` ve `Rebuild` hedeflerin ikisi de `RestorePackages`bağımlıdır.</span><span class="sxs-lookup"><span data-stu-id="9373a-154">The `Build` and `Rebuild` targets both depend on `RestorePackages`.</span></span> <span data-ttu-id="9373a-155">Bu, hem `Build` hem de `Rebuild` çalıştırabildiğinden ve geri yüklenen paketlere güvendiğinizden emin olmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="9373a-155">This makes sure that you can both run `Build` and `Rebuild` and rely on packages being restored.</span></span>
- <span data-ttu-id="9373a-156">`Clean`, `Build` ve `Rebuild` tüm çözüm dosyalarında karşılık gelen MSBuild hedefini çağırır.</span><span class="sxs-lookup"><span data-stu-id="9373a-156">`Clean`, `Build` and `Rebuild` invoke the corresponding MSBuild target on all solution files.</span></span>
- <span data-ttu-id="9373a-157">`RestorePackages` hedefi her çözüm dosyası için `nuget.exe` çağırır.</span><span class="sxs-lookup"><span data-stu-id="9373a-157">The `RestorePackages` target invokes `nuget.exe` for each solution file.</span></span> <span data-ttu-id="9373a-158">Bu, [MSBuild 'in toplu işlem işlevselliği](/visualstudio/msbuild/msbuild-batching)kullanılarak gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="9373a-158">This is accomplished by using [MSBuild's batching functionality](/visualstudio/msbuild/msbuild-batching).</span></span>

<span data-ttu-id="9373a-159">Sonuç şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="9373a-159">The result looks as follows:</span></span>

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

## <a name="configuring-team-build"></a><span data-ttu-id="9373a-160">Takım derlemesini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9373a-160">Configuring Team Build</span></span>

<span data-ttu-id="9373a-161">Ekip derlemesi çeşitli işlem şablonları sunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9373a-161">Team Build offers various process templates.</span></span> <span data-ttu-id="9373a-162">Bu gösterim için Team Foundation Service kullanırız.</span><span class="sxs-lookup"><span data-stu-id="9373a-162">For this demonstration, we're using the Team Foundation Service.</span></span> <span data-ttu-id="9373a-163">TFS 'nin şirket içi yüklemeleri çok benzer olacaktır.</span><span class="sxs-lookup"><span data-stu-id="9373a-163">On-premises installations of TFS will be very similar though.</span></span>

<span data-ttu-id="9373a-164">Git ve TF sürüm denetimi farklı takım derleme şablonlarına sahiptir, bu nedenle, kullanmakta olduğunuz sürüm denetim sistemine bağlı olarak aşağıdaki adımlar değişiklik gösterecektir.</span><span class="sxs-lookup"><span data-stu-id="9373a-164">Git and TF Version Control have different Team Build templates, so the following steps will vary depending on which version control system you are using.</span></span> <span data-ttu-id="9373a-165">Her iki durumda da tüm ihtiyacınız olan Build. proj ' i derlemek istediğiniz proje olarak seçmektir.</span><span class="sxs-lookup"><span data-stu-id="9373a-165">In both cases, all you need is selecting the build.proj as the project you want to build.</span></span>

<span data-ttu-id="9373a-166">İlk olarak, git için işlem şablonuna göz atalım.</span><span class="sxs-lookup"><span data-stu-id="9373a-166">First, let's look at the process template for git.</span></span> <span data-ttu-id="9373a-167">Git tabanlı şablonda, derleme `Solution to build`özellik ile seçilir:</span><span class="sxs-lookup"><span data-stu-id="9373a-167">In the git based template the build is selected via the property `Solution to build`:</span></span>

![Git için derleme Işlemi](media/PackageRestoreTeamBuildGit.png)

<span data-ttu-id="9373a-169">Bu özelliğin deponuzdaki bir konum olduğunu lütfen unutmayın.</span><span class="sxs-lookup"><span data-stu-id="9373a-169">Please note that this property is a location in your repository.</span></span> <span data-ttu-id="9373a-170">`build.proj` kökte olduğundan, `build.proj`yalnızca kullandık.</span><span class="sxs-lookup"><span data-stu-id="9373a-170">Since our `build.proj` is in the root, we simply used `build.proj`.</span></span> <span data-ttu-id="9373a-171">Yapı dosyasını `tools`adlı bir klasöre yerleştirirseniz, değer `tools\build.proj`olur.</span><span class="sxs-lookup"><span data-stu-id="9373a-171">If you place the build file under a folder called `tools`, the value would be `tools\build.proj`.</span></span>

<span data-ttu-id="9373a-172">TF sürüm denetimi şablonunda proje, özellik `Projects`seçilir:</span><span class="sxs-lookup"><span data-stu-id="9373a-172">In the TF version control template the project is selected via the property `Projects`:</span></span>

![TFVC için derleme Işlemi](media/PackageRestoreTeamBuildTFVC.png)

<span data-ttu-id="9373a-174">Git tabanlı şablonun aksine, TF sürüm denetimi, etiketleri destekler (üç nokta ile sağ taraftaki düğme).</span><span class="sxs-lookup"><span data-stu-id="9373a-174">In contrast to the git based template the TF version control supports pickers (the button on the right hand side with the three dots).</span></span> <span data-ttu-id="9373a-175">Bu nedenle, herhangi bir yazma hatasını önlemek için, projeyi seçmek üzere bunları kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="9373a-175">So in order to avoid any typing errors we suggest you use them to select the project.</span></span>
