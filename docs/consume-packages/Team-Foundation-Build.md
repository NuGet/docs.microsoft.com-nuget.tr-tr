---
title: Team Foundation derlemesi ile NuGet paketi geri yükleme kılavuzu
description: NuGet paketinin Team Foundation Build (TFS ve Visual Studio Team Services) ile birlikte nasıl geri yükleneceğini gösteren bir yol.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 8b993106d439dc137fbe040b51fda373539de81a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774989"
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a><span data-ttu-id="d0901-103">Team Foundation derlemesi ile paket geri yüklemeyi ayarlama</span><span class="sxs-lookup"><span data-stu-id="d0901-103">Setting up package restore with Team Foundation Build</span></span>

<span data-ttu-id="d0901-104">Bu makalede, hem git hem de Team Services sürüm denetimi için [Team Services derlemesinin](/vsts/build-release/index) bir parçası olarak paketlerin nasıl geri yükleneceği hakkında ayrıntılı bir yol sunulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d0901-104">This article provides a detailed walkthrough on how to restore packages as part of the [Team Services Build](/vsts/build-release/index) both, for both Git and Team Services Version Control.</span></span>

<span data-ttu-id="d0901-105">Bu izlenecek yol Visual Studio Team Services kullanma senaryosuna özgü olsa da, kavramlar diğer sürüm denetimi ve yapı sistemleri için de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="d0901-105">Although this walkthrough is specific for the scenario of using Visual Studio Team Services, the concepts also apply to other version control and build systems.</span></span>

<span data-ttu-id="d0901-106">Şunun için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="d0901-106">Applies To:</span></span>

- <span data-ttu-id="d0901-107">TFS 'nin herhangi bir sürümünde çalışan özel MSBuild projeleri</span><span class="sxs-lookup"><span data-stu-id="d0901-107">Custom MSBuild projects running on any version of TFS</span></span>
- <span data-ttu-id="d0901-108">Team Foundation Server 2012 veya öncesi</span><span class="sxs-lookup"><span data-stu-id="d0901-108">Team Foundation Server 2012 or earlier</span></span>
- <span data-ttu-id="d0901-109">TFS 2013 veya sonraki bir sürüme geçirilen özel Team Foundation derleme Işlemi şablonları</span><span class="sxs-lookup"><span data-stu-id="d0901-109">Custom Team Foundation Build Process Templates migrated to TFS 2013 or later</span></span>
- <span data-ttu-id="d0901-110">NuGet geri yükleme işlevselliği kaldırılmış şekilde Işlem şablonları oluşturun</span><span class="sxs-lookup"><span data-stu-id="d0901-110">Build Process Templates With Nuget Restore functionality removed</span></span>

<span data-ttu-id="d0901-111">Yapı işlemi şablonlarıyla Visual Studio Team Services veya Team Foundation Server 2013 kullanıyorsanız, derleme işleminin bir parçası olarak otomatik paket geri yüklemesi gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="d0901-111">If you're using Visual Studio Team Services or Team Foundation Server 2013 with its build process templates, automatic package restore happens as part of the build process.</span></span>

## <a name="the-general-approach"></a><span data-ttu-id="d0901-112">Genel yaklaşım</span><span class="sxs-lookup"><span data-stu-id="d0901-112">The general approach</span></span>

<span data-ttu-id="d0901-113">NuGet kullanmanın bir avantajı, bunu, sürüm denetim sisteminize ikili dosyaları iade etmekten kaçınmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0901-113">An advantage of using NuGet is that you can use it to avoid checking in binaries to your version control system.</span></span>

<span data-ttu-id="d0901-114">Bu özellikle, git gibi [Dağıtılmış bir sürüm denetimi](https://en.wikipedia.org/wiki/Distributed_revision_control) sistemi kullanıyorsanız, geliştiricilerin yerel olarak çalışmaya başlayabilmeleri için tam geçmiş dahil olmak üzere tüm depoyu kopyalaması gerektiğinden çok ilginç olur.</span><span class="sxs-lookup"><span data-stu-id="d0901-114">This is especially interesting if you are using a [distributed version control](https://en.wikipedia.org/wiki/Distributed_revision_control) system like git because developers need to clone the entire repository, including the full history, before they can start working locally.</span></span> <span data-ttu-id="d0901-115">İkili dosyalar genellikle değişim sıkıştırması olmadan depolandığından, ikili dosyaların iade edilirken önemli depo blobunun oluşmasına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="d0901-115">Checking in binaries can cause significant repository bloat as binary files are typically stored without delta compression.</span></span>

<span data-ttu-id="d0901-116">NuGet, yapılandırmanın bir parçası olarak uzun süredir [geri yüklemeyi](../consume-packages/package-restore.md) destekliyordu.</span><span class="sxs-lookup"><span data-stu-id="d0901-116">NuGet has supported [restoring packages](../consume-packages/package-restore.md) as part of the build for a long time now.</span></span> <span data-ttu-id="d0901-117">Önceki uygulamada, derleme işlemini genişletmek isteyen paketlere yönelik bir tavuk-yumurg sorunu vardı, çünkü projeyi oluştururken NuGet geri yüklendi paketleri.</span><span class="sxs-lookup"><span data-stu-id="d0901-117">The previous implementation had a chicken-and-egg problem for packages that want to extend the build process because NuGet restored packages while building the project.</span></span> <span data-ttu-id="d0901-118">Ancak, MSBuild derleme sırasında derlemeyi genişletmeye izin vermez; Bunlardan biri MSBuild 'deki bir sorun olduğunu, ancak bunun devralınmış bir sorun olduğunu anlıyorum.</span><span class="sxs-lookup"><span data-stu-id="d0901-118">However, MSBuild doesn't allow extending the build during the build; one could argue that this an issue in MSBuild but I would argue that this is an inherent problem.</span></span> <span data-ttu-id="d0901-119">Genişletmeniz gereken en boy düzeyine bağlı olarak, paketinizin geri yüklendiği zamana göre kaydolmak için çok geç olabilir.</span><span class="sxs-lookup"><span data-stu-id="d0901-119">Depending on which aspect you need to extend it might be too late to register by the time your package is restored.</span></span>

<span data-ttu-id="d0901-120">Bu sorunu çözmek, paketlerin derleme işlemindeki ilk adım olarak geri yüklendiğinden emin olmanızı sağlar:</span><span class="sxs-lookup"><span data-stu-id="d0901-120">The cure to this problem is making sure that packages are restored as the first step in the build process:</span></span>

```cli
nuget restore path\to\solution.sln
```

<span data-ttu-id="d0901-121">Yapı işleminiz kodu oluşturmadan önce paketleri geri yüklediğinde, dosyaları iade etmeniz gerekmez `.targets`</span><span class="sxs-lookup"><span data-stu-id="d0901-121">When your build process restores packages before building the code, you don't need to check-in `.targets` files</span></span>

> [!Note]
> <span data-ttu-id="d0901-122">Visual Studio 'da yüklemeye izin vermek için paketlerin yazılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0901-122">Packages must be authored to allow loading in Visual Studio.</span></span> <span data-ttu-id="d0901-123">Aksi takdirde, `.targets` diğer geliştiricilerin önce paketleri geri yüklemek zorunda kalmadan çözümü açabilmeleri için dosyaları iade etmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0901-123">Otherwise, you may still want to check in `.targets` files so that other developers can simply open the solution without having to restore packages first.</span></span>

<span data-ttu-id="d0901-124">Aşağıdaki demo projesi, bir derlemeyi `packages` klasörlerin ve dosyaların iade etme gereksinimi olacak şekilde ayarlamayı gösterir `.targets` .</span><span class="sxs-lookup"><span data-stu-id="d0901-124">The following demo project shows how to set up the build in such a way that the `packages` folders and `.targets` files don't need to be checked-in.</span></span> <span data-ttu-id="d0901-125">Ayrıca, bu örnek proje için Team Foundation Service otomatik bir derlemeyi ayarlamayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="d0901-125">It also shows how to set up an automated build on the Team Foundation Service for this sample project.</span></span>

## <a name="repository-structure"></a><span data-ttu-id="d0901-126">Depo yapısı</span><span class="sxs-lookup"><span data-stu-id="d0901-126">Repository structure</span></span>

<span data-ttu-id="d0901-127">Tanıtım projemiz, Bing sorgulamak için komut satırı bağımsız değişkenini kullanan basit bir komut satırı aracıdır.</span><span class="sxs-lookup"><span data-stu-id="d0901-127">Our demo project is a simple command line tool that uses the command line argument to query Bing.</span></span> <span data-ttu-id="d0901-128">.NET Framework 4 ' ü hedefler ve birçok [BCL paketini](https://www.nuget.org/profiles/dotnetframework/) ([Microsoft.net. http](https://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft. BCL](https://www.nuget.org/packages/Microsoft.Bcl), [Microsoft. BCL. Async](https://www.nuget.org/packages/Microsoft.Bcl.Async)ve [Microsoft. BCL. Build](https://www.nuget.org/packages/Microsoft.Bcl.Build)) kullanır.</span><span class="sxs-lookup"><span data-stu-id="d0901-128">It targets the .NET Framework 4 and uses many of the [BCL packages](https://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](https://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](https://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](https://www.nuget.org/packages/Microsoft.Bcl.Async), and [Microsoft.Bcl.Build](https://www.nuget.org/packages/Microsoft.Bcl.Build)).</span></span>

<span data-ttu-id="d0901-129">Deponun yapısı şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="d0901-129">The structure of the repository looks as follows:</span></span>

```
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
```

<span data-ttu-id="d0901-130">`packages`Klasörü veya herhangi bir dosyayı iade etmediğimiz hakkında bilgi alabilirsiniz `.targets` .</span><span class="sxs-lookup"><span data-stu-id="d0901-130">You can see that we haven't checked-in the `packages` folder nor any `.targets` files.</span></span>

<span data-ttu-id="d0901-131">Ancak, `nuget.exe` derleme sırasında gerekli olduğu gibi iade ettik.</span><span class="sxs-lookup"><span data-stu-id="d0901-131">We have, however, checked-in the `nuget.exe` as it's needed during the build.</span></span> <span data-ttu-id="d0901-132">Yaygın olarak kullanılan kuralları paylaşılan bir klasör altında denetliyoruz `tools` .</span><span class="sxs-lookup"><span data-stu-id="d0901-132">Following widely used conventions we've checked it in under a shared `tools` folder.</span></span>

<span data-ttu-id="d0901-133">Kaynak kodu `src` klasörün altındadır.</span><span class="sxs-lookup"><span data-stu-id="d0901-133">The source code is under the `src` folder.</span></span> <span data-ttu-id="d0901-134">Tanıtımız yalnızca tek bir çözüm kullandığından, bu klasörün birden fazla çözüm içerdiğini kolayca hayal edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0901-134">Although our demo only uses a single solution, you can easily imagine that this folder contains more than one solution.</span></span>

### <a name="ignore-files"></a><span data-ttu-id="d0901-135">Dosyaları yoksayma</span><span class="sxs-lookup"><span data-stu-id="d0901-135">Ignore files</span></span>

> [!Note]
> <span data-ttu-id="d0901-136">[NuGet istemcisinde](https://nuget.codeplex.com/workitem/4072) , istemcinin hala sürüm denetimine klasör eklemesine neden olan bilinen bir hata var `packages` .</span><span class="sxs-lookup"><span data-stu-id="d0901-136">There is currently a [known bug in the NuGet client](https://nuget.codeplex.com/workitem/4072) that causes the client to still add the `packages` folder to version control.</span></span> <span data-ttu-id="d0901-137">Kaynak denetimi tümleştirmesini devre dışı bırakmak geçici bir çözümdür.</span><span class="sxs-lookup"><span data-stu-id="d0901-137">A workaround is to disable the source control integration.</span></span> <span data-ttu-id="d0901-138">Bunu yapmak için `Nuget.Config `  `.nuget` çözümünüze paralel olan klasörde bir dosyaya ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="d0901-138">In order to do that, you need a `Nuget.Config ` file in the  `.nuget` folder that is parallel to your solution.</span></span> <span data-ttu-id="d0901-139">Bu klasör henüz yoksa, oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0901-139">If this folder doesn't exist yet, you need to create it.</span></span> <span data-ttu-id="d0901-140">İçinde [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md) , aşağıdaki içeriği ekleyin:</span><span class="sxs-lookup"><span data-stu-id="d0901-140">In [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md), add the following content:</span></span>

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```

<span data-ttu-id="d0901-141">**Paket** klasörlerinde iade etme amacını verdiğimiz Sürüm denetimiyle iletişim kurmak için, hem git () hem de `.gitignore` tf sürüm denetimi () için de Ignore dosyaları ekledik `.tfignore` .</span><span class="sxs-lookup"><span data-stu-id="d0901-141">To communicate to version control that we don’t intent to check-in the **packages** folders, we've also added ignore files for both git (`.gitignore`) as well as TF version control (`.tfignore`).</span></span> <span data-ttu-id="d0901-142">Bu dosyalar iade etmek istemediğiniz dosyaların desenlerini anlatmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d0901-142">These files describe patterns of files you don't want to check-in.</span></span>

<span data-ttu-id="d0901-143">`.gitignore`Dosya aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="d0901-143">The `.gitignore` file looks as follows:</span></span>

```
syntax: glob
*.user
*.suo
bin
obj
packages
*.nupkg
project.lock.json
project.assets.json
```

<span data-ttu-id="d0901-144">`.gitignore`Dosya [oldukça güçlüdür](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span><span class="sxs-lookup"><span data-stu-id="d0901-144">The `.gitignore` file is [quite powerful](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span></span> <span data-ttu-id="d0901-145">Örneğin, genellikle klasörün içeriğini iade etmek, `packages` ancak dosyaları iade etme hakkında daha önceki kılavuza gitmek istiyorsanız `.targets` bunun yerine aşağıdaki kurala sahip olabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d0901-145">For example, if you want to generally not check-in the contents of the `packages` folder but want to go with previous guidance of checking in the `.targets` files you could have the following rule instead:</span></span>

```
packages
!packages/**/*.targets
```

<span data-ttu-id="d0901-146">Bu, tüm klasörleri hariç tutar, `packages` ancak içerilen tüm dosyaları yeniden içerecektir `.targets` .</span><span class="sxs-lookup"><span data-stu-id="d0901-146">This will exclude all `packages` folders but will re-include all contained `.targets` files.</span></span> <span data-ttu-id="d0901-147">Bu şekilde, `.gitignore` [burada](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore)Visual Studio geliştiricilerinin ihtiyaçlarını karşılamak için özel olarak uyarlanmış dosyalar için bir şablon bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0901-147">By the way, you can find a template for `.gitignore` files that is specifically tailored for the needs of Visual Studio developers [here](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>

<span data-ttu-id="d0901-148">TF Version Control, [. tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) dosyası aracılığıyla çok benzer bir mekanizmayı destekler.</span><span class="sxs-lookup"><span data-stu-id="d0901-148">TF version control supports a very similar mechanism via the [.tfignore](/vsts/tfvc/add-files-server#customize-which-files-are-ignored-by-version-control) file.</span></span> <span data-ttu-id="d0901-149">Sözdizimi neredeyse aynıdır:</span><span class="sxs-lookup"><span data-stu-id="d0901-149">The syntax is virtually the same:</span></span>

```
*.user
*.suo
bin
obj
packages
*.nupkg
project.lock.json
project.assets.json
```

## <a name="buildproj"></a><span data-ttu-id="d0901-150">Build. proj</span><span class="sxs-lookup"><span data-stu-id="d0901-150">build.proj</span></span>

<span data-ttu-id="d0901-151">Tanıtımızın için yapı sürecini oldukça basit tutuyoruz.</span><span class="sxs-lookup"><span data-stu-id="d0901-151">For our demo, we keep the build process fairly simple.</span></span> <span data-ttu-id="d0901-152">Çözümleri oluşturmadan önce paketlerin geri yüklendiğinden emin olmak için tüm çözümleri oluşturan bir MSBuild projesi oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="d0901-152">We'll create an MSBuild project that builds all solutions while making sure that packages are restored before building the solutions.</span></span>

<span data-ttu-id="d0901-153">Bu proje, üç geleneksel hedefe `Clean` `Build` ve `Rebuild` Ayrıca yeni bir hedefe sahip olacaktır `RestorePackages` .</span><span class="sxs-lookup"><span data-stu-id="d0901-153">This project will have the three conventional targets `Clean`, `Build` and `Rebuild` as well as a new target `RestorePackages`.</span></span>

- <span data-ttu-id="d0901-154">`Build`Ve `Rebuild` hedefleri her ikisi de bağımlıdır `RestorePackages` .</span><span class="sxs-lookup"><span data-stu-id="d0901-154">The `Build` and `Rebuild` targets both depend on `RestorePackages`.</span></span> <span data-ttu-id="d0901-155">Bu, hem çalıştırıp hem de `Build` `Rebuild` Geri yüklenmekte olan paketleri temel almanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="d0901-155">This makes sure that you can both run `Build` and `Rebuild` and rely on packages being restored.</span></span>
- <span data-ttu-id="d0901-156">`Clean``Build`ve `Rebuild` tüm çözüm dosyalarında karşılık gelen MSBuild hedefini çağırır.</span><span class="sxs-lookup"><span data-stu-id="d0901-156">`Clean`, `Build` and `Rebuild` invoke the corresponding MSBuild target on all solution files.</span></span>
- <span data-ttu-id="d0901-157">`RestorePackages`Hedef `nuget.exe` her çözüm dosyası için çağırır.</span><span class="sxs-lookup"><span data-stu-id="d0901-157">The `RestorePackages` target invokes `nuget.exe` for each solution file.</span></span> <span data-ttu-id="d0901-158">Bu, [MSBuild 'in toplu işlem işlevselliği](/visualstudio/msbuild/msbuild-batching)kullanılarak gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="d0901-158">This is accomplished by using [MSBuild's batching functionality](/visualstudio/msbuild/msbuild-batching).</span></span>

<span data-ttu-id="d0901-159">Sonuç şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="d0901-159">The result looks as follows:</span></span>

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

## <a name="configuring-team-build"></a><span data-ttu-id="d0901-160">Takım derlemesini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d0901-160">Configuring Team Build</span></span>

<span data-ttu-id="d0901-161">Ekip derlemesi çeşitli işlem şablonları sunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d0901-161">Team Build offers various process templates.</span></span> <span data-ttu-id="d0901-162">Bu gösterim için Team Foundation Service kullanırız.</span><span class="sxs-lookup"><span data-stu-id="d0901-162">For this demonstration, we're using the Team Foundation Service.</span></span> <span data-ttu-id="d0901-163">TFS 'nin şirket içi yüklemeleri çok benzer olacaktır.</span><span class="sxs-lookup"><span data-stu-id="d0901-163">On-premises installations of TFS will be very similar though.</span></span>

<span data-ttu-id="d0901-164">Git ve TF sürüm denetimi farklı takım derleme şablonlarına sahiptir, bu nedenle, kullanmakta olduğunuz sürüm denetim sistemine bağlı olarak aşağıdaki adımlar değişiklik gösterecektir.</span><span class="sxs-lookup"><span data-stu-id="d0901-164">Git and TF Version Control have different Team Build templates, so the following steps will vary depending on which version control system you are using.</span></span> <span data-ttu-id="d0901-165">Her iki durumda da tüm ihtiyacınız olan Build. proj ' i derlemek istediğiniz proje olarak seçmektir.</span><span class="sxs-lookup"><span data-stu-id="d0901-165">In both cases, all you need is selecting the build.proj as the project you want to build.</span></span>

<span data-ttu-id="d0901-166">İlk olarak, git için işlem şablonuna göz atalım.</span><span class="sxs-lookup"><span data-stu-id="d0901-166">First, let's look at the process template for git.</span></span> <span data-ttu-id="d0901-167">Git tabanlı şablonda, yapı özelliği aracılığıyla seçilir `Solution to build` :</span><span class="sxs-lookup"><span data-stu-id="d0901-167">In the git based template the build is selected via the property `Solution to build`:</span></span>

![Git için derleme Işlemi](media/PackageRestoreTeamBuildGit.png)

<span data-ttu-id="d0901-169">Bu özelliğin deponuzdaki bir konum olduğunu lütfen unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d0901-169">Please note that this property is a location in your repository.</span></span> <span data-ttu-id="d0901-170">Bizim `build.proj` kökte olduğundan, yalnızca kullandık `build.proj` .</span><span class="sxs-lookup"><span data-stu-id="d0901-170">Since our `build.proj` is in the root, we simply used `build.proj`.</span></span> <span data-ttu-id="d0901-171">Yapı dosyasını adlı bir klasöre yerleştirirseniz `tools` değer şöyle olur `tools\build.proj` .</span><span class="sxs-lookup"><span data-stu-id="d0901-171">If you place the build file under a folder called `tools`, the value would be `tools\build.proj`.</span></span>

<span data-ttu-id="d0901-172">TF sürüm denetimi şablonunda, proje özelliği aracılığıyla seçilir `Projects` :</span><span class="sxs-lookup"><span data-stu-id="d0901-172">In the TF version control template the project is selected via the property `Projects`:</span></span>

![TFVC için derleme Işlemi](media/PackageRestoreTeamBuildTFVC.png)

<span data-ttu-id="d0901-174">Git tabanlı şablonun aksine, TF sürüm denetimi, etiketleri destekler (üç nokta ile sağ taraftaki düğme).</span><span class="sxs-lookup"><span data-stu-id="d0901-174">In contrast to the git based template the TF version control supports pickers (the button on the right hand side with the three dots).</span></span> <span data-ttu-id="d0901-175">Bu nedenle, herhangi bir yazma hatasını önlemek için, projeyi seçmek üzere bunları kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="d0901-175">So in order to avoid any typing errors we suggest you use them to select the project.</span></span>
