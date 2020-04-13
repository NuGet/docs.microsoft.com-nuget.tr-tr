---
title: Team Foundation Build ile NuGet Paketi Geri Yükleme'nin Walkthrough'u
description: Team Foundation Build (Hem TFS hem de Visual Studio Team Services) ile NuGet paketinin nasıl geri yüklenirolduğunun bir walkthrough'u.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: a86a58f8afb4b0f1affeddd47d6c5606fb465757
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "73610996"
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a><span data-ttu-id="e3b4d-103">Team Foundation Build ile paket geri yüklemesi ayarlama</span><span class="sxs-lookup"><span data-stu-id="e3b4d-103">Setting up package restore with Team Foundation Build</span></span>

<span data-ttu-id="e3b4d-104">Bu makalede, hem Git hem de Takım Hizmetleri Sürüm Denetimi [için, Her](/vsts/build-release/index) ikisi de Ekip Hizmetleri Yapısı'nın bir parçası olarak paketlerin nasıl geri yükleneneceklerine ilişkin ayrıntılı bir gözden geçirme sağlar.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-104">This article provides a detailed walkthrough on how to restore packages as part of the [Team Services Build](/vsts/build-release/index) both, for both Git and Team Services Version Control.</span></span>

<span data-ttu-id="e3b4d-105">Bu izbis Visual Studio Team Services'ı kullanma senaryosu için özel olsa da, kavramlar diğer sürüm denetimi ve yapı sistemleri için de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-105">Although this walkthrough is specific for the scenario of using Visual Studio Team Services, the concepts also apply to other version control and build systems.</span></span>

<span data-ttu-id="e3b4d-106">Şunun için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="e3b4d-106">Applies To:</span></span>

- <span data-ttu-id="e3b4d-107">TFS'nin herhangi bir sürümünde çalışan özel MSBuild projeleri</span><span class="sxs-lookup"><span data-stu-id="e3b4d-107">Custom MSBuild projects running on any version of TFS</span></span>
- <span data-ttu-id="e3b4d-108">Team Foundation Server 2012 veya önceki</span><span class="sxs-lookup"><span data-stu-id="e3b4d-108">Team Foundation Server 2012 or earlier</span></span>
- <span data-ttu-id="e3b4d-109">TFS 2013 veya sonraki bir süre sonra geçirilen Özel Takım Temel Oluşturma İşlemşablonları</span><span class="sxs-lookup"><span data-stu-id="e3b4d-109">Custom Team Foundation Build Process Templates migrated to TFS 2013 or later</span></span>
- <span data-ttu-id="e3b4d-110">Nuget Geri Yükleme işlevi kaldırılmış olan İşlem Şablonları Oluşturma</span><span class="sxs-lookup"><span data-stu-id="e3b4d-110">Build Process Templates With Nuget Restore functionality removed</span></span>

<span data-ttu-id="e3b4d-111">Visual Studio Team Services veya Team Foundation Server 2013'ü yapı işlem şablonlarıyla kullanıyorsanız, otomatik paket geri yüklemesi yapı sürecinin bir parçası olarak gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-111">If you're using Visual Studio Team Services or Team Foundation Server 2013 with its build process templates, automatic package restore happens as part of the build process.</span></span>

## <a name="the-general-approach"></a><span data-ttu-id="e3b4d-112">Genel yaklaşım</span><span class="sxs-lookup"><span data-stu-id="e3b4d-112">The general approach</span></span>

<span data-ttu-id="e3b4d-113">NuGet kullanmanın bir avantajı, sürüm kontrol sisteminize ikili olarak giriş yapmaktan kaçınmak için bunu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-113">An advantage of using NuGet is that you can use it to avoid checking in binaries to your version control system.</span></span>

<span data-ttu-id="e3b4d-114">Geliştiriciler yerel olarak çalışmaya başlamadan önce, tam geçmişi de dahil olmak üzere tüm depo klonlamak gerekir, çünkü git gibi [dağıtılmış](https://en.wikipedia.org/wiki/Distributed_revision_control) bir sürüm kontrol sistemi kullanıyorsanız bu özellikle ilginç.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-114">This is especially interesting if you are using a [distributed version control](https://en.wikipedia.org/wiki/Distributed_revision_control) system like git because developers need to clone the entire repository, including the full history, before they can start working locally.</span></span> <span data-ttu-id="e3b4d-115">İkili dosyaların genellikle delta sıkıştırma olmadan depolanır gibi ikili olarak kontrol önemli depo şişkinlik neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-115">Checking in binaries can cause significant repository bloat as binary files are typically stored without delta compression.</span></span>

<span data-ttu-id="e3b4d-116">NuGet, uzun zamandır yapının bir parçası olarak [paketleri geri almayı](../consume-packages/package-restore.md) desteklemiştir.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-116">NuGet has supported [restoring packages](../consume-packages/package-restore.md) as part of the build for a long time now.</span></span> <span data-ttu-id="e3b4d-117">NuGet projeyi oluştururken paketleri geri yüklediği için, önceki uygulamada yapı işlemini uzatmak isteyen paketler için tavuk ve yumurta sorunu vardı.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-117">The previous implementation had a chicken-and-egg problem for packages that want to extend the build process because NuGet restored packages while building the project.</span></span> <span data-ttu-id="e3b4d-118">Ancak, MSBuild yapı sırasında yapı genişletilmesine izin vermez; bir MSBuild bu bir sorun olduğunu iddia edebilir ama bu doğal bir sorun olduğunu iddia ediyorum.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-118">However, MSBuild doesn't allow extending the build during the build; one could argue that this an issue in MSBuild but I would argue that this is an inherent problem.</span></span> <span data-ttu-id="e3b4d-119">Hangi yönü genişletmeniz gerektiğine bağlı olarak, paketiniz geri yüklenene kadar kaydolmak için çok geç olabilir.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-119">Depending on which aspect you need to extend it might be too late to register by the time your package is restored.</span></span>

<span data-ttu-id="e3b4d-120">Bu sorunun çözümü, paketlerin yapı işleminin ilk adımı olarak geri yüklenmesidir:</span><span class="sxs-lookup"><span data-stu-id="e3b4d-120">The cure to this problem is making sure that packages are restored as the first step in the build process:</span></span>

```cli
nuget restore path\to\solution.sln
```

<span data-ttu-id="e3b4d-121">Yapı işleminiz kodu oluşturmadan önce paketleri geri yüklediğinde, `.targets` iade dosyalarına gerek yoktur</span><span class="sxs-lookup"><span data-stu-id="e3b4d-121">When your build process restores packages before building the code, you don't need to check-in `.targets` files</span></span>

> [!Note]
> <span data-ttu-id="e3b4d-122">Paketler Visual Studio'da yüklemeye izin verecek şekilde yazılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-122">Packages must be authored to allow loading in Visual Studio.</span></span> <span data-ttu-id="e3b4d-123">Aksi takdirde, diğer geliştiricilerin `.targets` önce paketleri geri yüklemek zorunda kalmadan çözümü açabilmeleri için dosyaları iade etmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-123">Otherwise, you may still want to check in `.targets` files so that other developers can simply open the solution without having to restore packages first.</span></span>

<span data-ttu-id="e3b4d-124">Aşağıdaki demo projesi, `packages` klasörlerin ve `.targets` dosyaların iade edilmesine gerek olmayacak şekilde yapının nasıl ayarlanış edilebildiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-124">The following demo project shows how to set up the build in such a way that the `packages` folders and `.targets` files don't need to be checked-in.</span></span> <span data-ttu-id="e3b4d-125">Ayrıca, bu örnek proje için Team Foundation Service üzerinde otomatik bir yapının nasıl kurulabildiğini de gösterir.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-125">It also shows how to set up an automated build on the Team Foundation Service for this sample project.</span></span>

## <a name="repository-structure"></a><span data-ttu-id="e3b4d-126">Depo yapısı</span><span class="sxs-lookup"><span data-stu-id="e3b4d-126">Repository structure</span></span>

<span data-ttu-id="e3b4d-127">Demo projemiz, Bing'i sorgulamak için komut satırı bağımsız değişkenini kullanan basit bir komut satırı aracıdır.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-127">Our demo project is a simple command line tool that uses the command line argument to query Bing.</span></span> <span data-ttu-id="e3b4d-128">Bu .NET Framework 4 hedefleri ve [BCL paketleri](https://www.nuget.org/profiles/dotnetframework/) [(Microsoft.Net.Http](https://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](https://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](https://www.nuget.org/packages/Microsoft.Bcl.Async)ve [Microsoft.Bcl.Build)](https://www.nuget.org/packages/Microsoft.Bcl.Build)birçok kullanır.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-128">It targets the .NET Framework 4 and uses many of the [BCL packages](https://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](https://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](https://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](https://www.nuget.org/packages/Microsoft.Bcl.Async), and [Microsoft.Bcl.Build](https://www.nuget.org/packages/Microsoft.Bcl.Build)).</span></span>

<span data-ttu-id="e3b4d-129">Deponun yapısı aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="e3b4d-129">The structure of the repository looks as follows:</span></span>

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

<span data-ttu-id="e3b4d-130">Klasöre veya herhangi bir `packages` `.targets` dosyaya giriş yapmadığımızı görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-130">You can see that we haven't checked-in the `packages` folder nor any `.targets` files.</span></span>

<span data-ttu-id="e3b4d-131">Ancak, inşa sırasında ihtiyaç duyulan `nuget.exe` şekilde check-in yaptık.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-131">We have, however, checked-in the `nuget.exe` as it's needed during the build.</span></span> <span data-ttu-id="e3b4d-132">Yaygın olarak kullanılan kuralları takiben, paylaşılan `tools` bir klasöraltında kontrol ettik.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-132">Following widely used conventions we've checked it in under a shared `tools` folder.</span></span>

<span data-ttu-id="e3b4d-133">Kaynak kodu klasörün `src` altındadır.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-133">The source code is under the `src` folder.</span></span> <span data-ttu-id="e3b4d-134">Demomuz yalnızca tek bir çözüm kullansa da, bu klasörün birden fazla çözüm içerdiğini kolayca hayal edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-134">Although our demo only uses a single solution, you can easily imagine that this folder contains more than one solution.</span></span>

### <a name="ignore-files"></a><span data-ttu-id="e3b4d-135">Dosyaları yoksayma</span><span class="sxs-lookup"><span data-stu-id="e3b4d-135">Ignore files</span></span>

> [!Note]
> <span data-ttu-id="e3b4d-136">Şu anda [NuGet istemcisinde istemcinin](https://nuget.codeplex.com/workitem/4072) klasörü `packages` sürüm denetimine eklemesine neden olan bilinen bir hata vardır.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-136">There is currently a [known bug in the NuGet client](https://nuget.codeplex.com/workitem/4072) that causes the client to still add the `packages` folder to version control.</span></span> <span data-ttu-id="e3b4d-137">Geçici çözüm, kaynak denetim tümleştirmesini devre dışı betmektir.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-137">A workaround is to disable the source control integration.</span></span> <span data-ttu-id="e3b4d-138">Bunu yapmak için, `Nuget.Config ` `.nuget` klasörde çözümünüze paralel bir dosya gerekir.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-138">In order to do that, you need a `Nuget.Config ` file in the  `.nuget` folder that is parallel to your solution.</span></span> <span data-ttu-id="e3b4d-139">Bu klasör henüz yoksa, klasörü oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-139">If this folder doesn't exist yet, you need to create it.</span></span> <span data-ttu-id="e3b4d-140">In [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md), aşağıdaki içeriği ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e3b4d-140">In [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md), add the following content:</span></span>

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```

<span data-ttu-id="e3b4d-141">**Paket** klasörlerini iade etme niyetimiz olmadığını sürüm denetimine iletmek için, hem git (`.gitignore`) hem de TF sürüm`.tfignore`denetimi ( ) için yoksay dosyaları ekledik.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-141">To communicate to version control that we don’t intent to check-in the **packages** folders, we've also added ignore files for both git (`.gitignore`) as well as TF version control (`.tfignore`).</span></span> <span data-ttu-id="e3b4d-142">Bu dosyalar, iade etmek istemediğiniz dosyaların modellerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-142">These files describe patterns of files you don't want to check-in.</span></span>

<span data-ttu-id="e3b4d-143">Dosya `.gitignore` aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="e3b4d-143">The `.gitignore` file looks as follows:</span></span>

    syntax: glob
    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

<span data-ttu-id="e3b4d-144">Dosya `.gitignore` [oldukça güçlü.](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html)</span><span class="sxs-lookup"><span data-stu-id="e3b4d-144">The `.gitignore` file is [quite powerful](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span></span> <span data-ttu-id="e3b4d-145">Örneğin, genellikle `packages` klasörün içeriğini iade etmek istemiyorsanız ancak `.targets` dosyaları iade etme kılavuzunu önceki kılavuzla gitmek istiyorsanız, bunun yerine aşağıdaki kurala sahip olabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e3b4d-145">For example, if you want to generally not check-in the contents of the `packages` folder but want to go with previous guidance of checking in the `.targets` files you could have the following rule instead:</span></span>

    packages
    !packages/**/*.targets

<span data-ttu-id="e3b4d-146">Bu, tüm `packages` klasörleri hariç tutar, `.targets` ancak içerdiği tüm dosyaları yeniden içerir.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-146">This will exclude all `packages` folders but will re-include all contained `.targets` files.</span></span> <span data-ttu-id="e3b4d-147">Bu arada, [burada](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore)Visual Studio `.gitignore` geliştiricilerin ihtiyaçlarına özel olarak uyarlanmış dosyalar için bir şablon bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-147">By the way, you can find a template for `.gitignore` files that is specifically tailored for the needs of Visual Studio developers [here](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>

<span data-ttu-id="e3b4d-148">TF sürüm denetimi [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) dosyası üzerinden çok benzer bir mekanizmayı destekler.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-148">TF version control supports a very similar mechanism via the [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) file.</span></span> <span data-ttu-id="e3b4d-149">Sözdizimi hemen hemen aynıdır:</span><span class="sxs-lookup"><span data-stu-id="e3b4d-149">The syntax is virtually the same:</span></span>

    *.user
    *.suo
    bin
    obj
    packages
    *.nupkg
    project.lock.json
    project.assets.json

## <a name="buildproj"></a><span data-ttu-id="e3b4d-150">build.proj</span><span class="sxs-lookup"><span data-stu-id="e3b4d-150">build.proj</span></span>

<span data-ttu-id="e3b4d-151">Demomuz için, yapı işlemini oldukça basit tutuyoruz.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-151">For our demo, we keep the build process fairly simple.</span></span> <span data-ttu-id="e3b4d-152">Çözümleri oluşturmadan önce paketlerin geri yüklenirken tüm çözümleri oluşturan bir MSBuild projesi oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-152">We'll create an MSBuild project that builds all solutions while making sure that packages are restored before building the solutions.</span></span>

<span data-ttu-id="e3b4d-153">Bu proje üç konvansiyonel `Clean`hedefleri `Build` `Rebuild` olacak, hem de `RestorePackages`yeni bir hedef .</span><span class="sxs-lookup"><span data-stu-id="e3b4d-153">This project will have the three conventional targets `Clean`, `Build` and `Rebuild` as well as a new target `RestorePackages`.</span></span>

- <span data-ttu-id="e3b4d-154">Hem hedefler hem de bağlıdır. `RestorePackages` `Build` `Rebuild`</span><span class="sxs-lookup"><span data-stu-id="e3b4d-154">The `Build` and `Rebuild` targets both depend on `RestorePackages`.</span></span> <span data-ttu-id="e3b4d-155">Bu, hem çalıştırabileceğinizi `Build` `Rebuild` hem de geri yüklenen paketlere güvenmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-155">This makes sure that you can both run `Build` and `Rebuild` and rely on packages being restored.</span></span>
- <span data-ttu-id="e3b4d-156">`Clean`ve `Build` `Rebuild` tüm çözüm dosyalarında karşılık gelen MSBuild hedefini çağırın.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-156">`Clean`, `Build` and `Rebuild` invoke the corresponding MSBuild target on all solution files.</span></span>
- <span data-ttu-id="e3b4d-157">Hedef `RestorePackages` her `nuget.exe` çözüm dosyası için çağırır.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-157">The `RestorePackages` target invokes `nuget.exe` for each solution file.</span></span> <span data-ttu-id="e3b4d-158">Bu, [MSBuild'in toplu işişlevini](/visualstudio/msbuild/msbuild-batching)kullanarak gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-158">This is accomplished by using [MSBuild's batching functionality](/visualstudio/msbuild/msbuild-batching).</span></span>

<span data-ttu-id="e3b4d-159">Sonuç aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="e3b4d-159">The result looks as follows:</span></span>

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

## <a name="configuring-team-build"></a><span data-ttu-id="e3b4d-160">Takım Oluşturmayı Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e3b4d-160">Configuring Team Build</span></span>

<span data-ttu-id="e3b4d-161">Team Build çeşitli işlem şablonları sunar.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-161">Team Build offers various process templates.</span></span> <span data-ttu-id="e3b4d-162">Bu gösteri için, Takım Hazırlık Servisi'ni kullanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-162">For this demonstration, we're using the Team Foundation Service.</span></span> <span data-ttu-id="e3b4d-163">TFS'nin şirket içi kurulumları çok benzer olacaktır.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-163">On-premises installations of TFS will be very similar though.</span></span>

<span data-ttu-id="e3b4d-164">Git ve TF Sürüm Denetimi farklı Takım Oluşturma şablonlarına sahiptir, bu nedenle aşağıdaki adımlar kullandığınız sürüm kontrol sistemine bağlı olarak değişir.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-164">Git and TF Version Control have different Team Build templates, so the following steps will vary depending on which version control system you are using.</span></span> <span data-ttu-id="e3b4d-165">Her iki durumda da, tek ihtiyacınız oluşturmak istediğiniz proje olarak build.proj seçmektir.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-165">In both cases, all you need is selecting the build.proj as the project you want to build.</span></span>

<span data-ttu-id="e3b4d-166">İlk olarak, git için işlem şablonuna bakalım.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-166">First, let's look at the process template for git.</span></span> <span data-ttu-id="e3b4d-167">Git tabanlı şablonda yapı özelliği `Solution to build`üzerinden seçilir:</span><span class="sxs-lookup"><span data-stu-id="e3b4d-167">In the git based template the build is selected via the property `Solution to build`:</span></span>

![Git için Yapı Süreci](media/PackageRestoreTeamBuildGit.png)

<span data-ttu-id="e3b4d-169">Bu tesisin deponuzdaki bir yer olduğunu lütfen unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-169">Please note that this property is a location in your repository.</span></span> <span data-ttu-id="e3b4d-170">Bizim `build.proj` kök olduğu için, biz `build.proj`sadece kullanılır .</span><span class="sxs-lookup"><span data-stu-id="e3b4d-170">Since our `build.proj` is in the root, we simply used `build.proj`.</span></span> <span data-ttu-id="e3b4d-171">Yapı dosyasını adlı `tools`bir klasörün altına yerlesanız, değer . `tools\build.proj`</span><span class="sxs-lookup"><span data-stu-id="e3b4d-171">If you place the build file under a folder called `tools`, the value would be `tools\build.proj`.</span></span>

<span data-ttu-id="e3b4d-172">TF sürüm kontrol şablonunda proje özellik `Projects`üzerinden seçilir:</span><span class="sxs-lookup"><span data-stu-id="e3b4d-172">In the TF version control template the project is selected via the property `Projects`:</span></span>

![TFVC için Yapı Süreci](media/PackageRestoreTeamBuildTFVC.png)

<span data-ttu-id="e3b4d-174">Git tabanlı şablonun aksine TF sürüm denetimi toplayıcıları destekler (sağ taraftaki düğme üç noktayla birlikte).</span><span class="sxs-lookup"><span data-stu-id="e3b4d-174">In contrast to the git based template the TF version control supports pickers (the button on the right hand side with the three dots).</span></span> <span data-ttu-id="e3b4d-175">Bu nedenle yazım hatalarından kaçınmak için projeyi seçmek için bunları kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="e3b4d-175">So in order to avoid any typing errors we suggest you use them to select the project.</span></span>
