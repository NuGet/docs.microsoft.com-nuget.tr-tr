---
title: NuGet için .NET Derleyici Platform Analizörü Biçimleri
description: API veya kitaplık uygulayan NuGet paketleriyle paketlenip dağıtılan .NET çözümleyicileri için sözleşmeler.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 4d337299f725b38981b0121069d5e6295b05e34e
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "72924634"
---
# <a name="analyzer-nuget-formats"></a><span data-ttu-id="efe1f-103">Analyzer NuGet biçimleri</span><span class="sxs-lookup"><span data-stu-id="efe1f-103">Analyzer NuGet formats</span></span>

<span data-ttu-id="efe1f-104">.NET Derleyici Platformu ("Roslyn" olarak da bilinir), geliştiricilerin kod sözdizimi ağacını ve kod anlamtlarını incelenirken inceleyen [çözümleyiciler](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) oluşturmasına olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="efe1f-104">The .NET Compiler Platform (also known as "Roslyn") allows developers to create [analyzers](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) that examine the syntax tree and semantics of code as it's being written.</span></span> <span data-ttu-id="efe1f-105">Bu, geliştiricilere, belirli bir API veya kitaplığın kullanımına rehberlik edecek alanlar gibi etki alanına özgü çözümleme araçları oluşturmanın bir yolunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="efe1f-105">This provides developers with a way to create domain-specific analysis tools, such as those that would help guide the use of a particular API or library.</span></span> <span data-ttu-id="efe1f-106">[.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub wiki hakkında daha fazla bilgi bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="efe1f-106">You can find more information on the [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub wiki.</span></span> <span data-ttu-id="efe1f-107">Ayrıca makaleye bakın, MSDN Dergisi'nde [API için canlı kod analizörü yazmak için Roslyn kullanın.](https://msdn.microsoft.com/magazine/dn879356.aspx)</span><span class="sxs-lookup"><span data-stu-id="efe1f-107">Also see the article, [Use Roslyn to Write a Live Code Analyzer for your API](https://msdn.microsoft.com/magazine/dn879356.aspx) in MSDN Magazine.</span></span>

<span data-ttu-id="efe1f-108">Çözümleyicilerin kendileri genellikle söz konusu API veya kitaplığı uygulayan NuGet paketlerinin bir parçası olarak paketlenir ve dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="efe1f-108">Analyzers themselves are typically packaged and distributed as part of the NuGet packages that implement the API or library in question.</span></span>

<span data-ttu-id="efe1f-109">İyi bir örnek için, aşağıdaki içerikleri içeren [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) paketine bakın:</span><span class="sxs-lookup"><span data-stu-id="efe1f-109">For a good example, see the [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) package, which has the following contents:</span></span>

- <span data-ttu-id="efe1f-110">çözümleyiciler\dotnet\System.Runtime.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="efe1f-110">analyzers\dotnet\System.Runtime.Analyzers.dll</span></span>
- <span data-ttu-id="efe1f-111">çözümleyiciler\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="efe1f-111">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span></span>
- <span data-ttu-id="efe1f-112">çözümleyiciler\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="efe1f-112">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span></span>
- <span data-ttu-id="efe1f-113">build\System.Runtime.Analyzers.Common.props</span><span class="sxs-lookup"><span data-stu-id="efe1f-113">build\System.Runtime.Analyzers.Common.props</span></span>
- <span data-ttu-id="efe1f-114">build\System.Runtime.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="efe1f-114">build\System.Runtime.Analyzers.props</span></span>
- <span data-ttu-id="efe1f-115">build\System.Runtime.CSharp.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="efe1f-115">build\System.Runtime.CSharp.Analyzers.props</span></span>
- <span data-ttu-id="efe1f-116">build\System.Runtime.VisualBasic.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="efe1f-116">build\System.Runtime.VisualBasic.Analyzers.props</span></span>
- <span data-ttu-id="efe1f-117">araçlar\install.ps1</span><span class="sxs-lookup"><span data-stu-id="efe1f-117">tools\install.ps1</span></span>
- <span data-ttu-id="efe1f-118">araçlar\uninstall.ps1</span><span class="sxs-lookup"><span data-stu-id="efe1f-118">tools\uninstall.ps1</span></span>

<span data-ttu-id="efe1f-119">Gördüğünüz gibi, çözümleyici DL'leri paketteki `analyzers` bir klasöre yersiniz.</span><span class="sxs-lookup"><span data-stu-id="efe1f-119">As you can see, you place the analyzer DLLs into an `analyzers` folder in the package.</span></span>

<span data-ttu-id="efe1f-120">Çözümleyici uygulaması lehine eski FxCop kurallarını devre dışı bırakan sahne dosyaları klasöre `build` yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="efe1f-120">Props files, which are included to disable legacy FxCop rules in favor of the analyzer implementation, are placed in the `build` folder.</span></span>

<span data-ttu-id="efe1f-121">Projeleri destekleyen `packages.config` komut dosyalarını yükleyin ve `tools`kaldırın.</span><span class="sxs-lookup"><span data-stu-id="efe1f-121">Install and uninstall scripts that support projects using `packages.config` are placed in `tools`.</span></span>

<span data-ttu-id="efe1f-122">Ayrıca, bu paketin platforma özgü gereksinimleri `platform` olmadığından klasörün atlandığına da dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="efe1f-122">Also note that because this package has no platform-specific requirements, the `platform` folder is omitted.</span></span>


## <a name="analyzers-path-format"></a><span data-ttu-id="efe1f-123">Çözümleyiciler yol biçimi</span><span class="sxs-lookup"><span data-stu-id="efe1f-123">Analyzers path format</span></span>

<span data-ttu-id="efe1f-124">Klasörün `analyzers` kullanımı [hedef çerçeveler](../create-packages/supporting-multiple-target-frameworks.md)için kullanılana benzer , ancak yoldaki belirteçler yapı zamanı yerine geliştirme ana bilgisayar bağımlılıklarını açıklar.</span><span class="sxs-lookup"><span data-stu-id="efe1f-124">The use of the `analyzers` folder is similar to that used for [target frameworks](../create-packages/supporting-multiple-target-frameworks.md), except the specifiers in the path describe development host dependencies instead of build-time.</span></span> <span data-ttu-id="efe1f-125">Genel biçimi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="efe1f-125">The general format is as follows:</span></span>

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}/{analyzer_name}.dll

- <span data-ttu-id="efe1f-126">**framework_name** ve **sürüm**: .NET Framework'ün, içerdiği DL'lerin çalışması gereken *isteğe bağlı* API yüzey alanı.</span><span class="sxs-lookup"><span data-stu-id="efe1f-126">**framework_name** and **version**: the *optional* API surface area of the .NET Framework that the contained DLLs need to run.</span></span> <span data-ttu-id="efe1f-127">`dotnet`roslyn çözümleyicileri çalıştırabilen tek ana bilgisayar olduğundan, şu anda tek geçerli değerdir.</span><span class="sxs-lookup"><span data-stu-id="efe1f-127">`dotnet` is presently the only valid value because Roslyn is the only host that can run analyzers.</span></span> <span data-ttu-id="efe1f-128">Hedef belirtilmemişse, DL'lerin *tüm* hedeflere uygulanacağı varsayılır.</span><span class="sxs-lookup"><span data-stu-id="efe1f-128">If no target is specified, DLLs are assumed to apply to *all* targets.</span></span>
- <span data-ttu-id="efe1f-129">**supported_language**: DLL'nin geçerli olduğu dil, `cs` (C#) ve (Visual Basic) ve `vb` `fs` (F#).</span><span class="sxs-lookup"><span data-stu-id="efe1f-129">**supported_language**: the language for which the DLL applies, one of `cs` (C#) and `vb` (Visual Basic), and `fs` (F#).</span></span> <span data-ttu-id="efe1f-130">Dil, çözümleyicinin yalnızca bu dili kullanan bir proje için yüklenmesi gerektiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="efe1f-130">The language indicates that the analyzer should be loaded only for a project using that language.</span></span> <span data-ttu-id="efe1f-131">Dil belirtilmemişse, DLL'nin çözümleyicileri destekleyen *tüm* dillere uygulanacağı varsayılır.</span><span class="sxs-lookup"><span data-stu-id="efe1f-131">If no language is specified then the DLL is assumed to apply to *all* languages that support analyzers.</span></span>
- <span data-ttu-id="efe1f-132">**analyzer_name**: çözümleyicinin DL'lerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="efe1f-132">**analyzer_name**: specifies the DLLs of the analyzer.</span></span> <span data-ttu-id="efe1f-133">DL'lerin ötesinde ek dosyalara ihtiyacınız varsa, bunlar bir hedef veya özellik dosyaları aracılığıyla eklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="efe1f-133">If you need additional files beyond DLLs, they must be included through a targets or properties files.</span></span>


## <a name="install-and-uninstall-scripts"></a><span data-ttu-id="efe1f-134">Komut dosyalarını yükleme ve kaldırma</span><span class="sxs-lookup"><span data-stu-id="efe1f-134">Install and uninstall scripts</span></span>

<span data-ttu-id="efe1f-135">Kullanıcının projesi `packages.config`kullanıyorsa, çözümleyiciyi alan MSBuild komut dosyası devreye girmez, `install.ps1` bu `uninstall.ps1` nedenle `tools` aşağıda açıklanan içerikleri klasöre yerleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="efe1f-135">If the user's project is using `packages.config`, the MSBuild script that picks up the analyzer does not come into play, so you should place `install.ps1` and `uninstall.ps1` in the `tools` folder with the contents that are described below.</span></span>

<span data-ttu-id="efe1f-136">**install.ps1 dosya içeriği**</span><span class="sxs-lookup"><span data-stu-id="efe1f-136">**install.ps1 file contents**</span></span>

```ps
param($installPath, $toolsPath, $package, $project)

$analyzersPaths = Join-Path (Join-Path (Split-Path -Path $toolsPath -Parent) "analyzers" ) * -Resolve

foreach($analyzersPath in $analyzersPaths)
{
    # Install the language agnostic analyzers.
    if (Test-Path $analyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $analyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Add($analyzerFilePath.FullName)
            }
        }
    }
}

$project.Type # gives the language name like (C# or VB.NET)
$languageFolder = ""
if($project.Type -eq "C#")
{
    $languageFolder = "cs"
}
if($project.Type -eq "VB.NET")
{
    $languageFolder = "vb"
}
if($languageFolder -eq "")
{
    return
}

foreach($analyzersPath in $analyzersPaths)
{
    # Install language specific analyzers.
    $languageAnalyzersPath = join-path $analyzersPath $languageFolder
    if (Test-Path $languageAnalyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $languageAnalyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Add($analyzerFilePath.FullName)
            }
        }
    }
}
```


<span data-ttu-id="efe1f-137">**uninstall.ps1 dosya içeriği**</span><span class="sxs-lookup"><span data-stu-id="efe1f-137">**uninstall.ps1 file contents**</span></span>

```ps
param($installPath, $toolsPath, $package, $project)

$analyzersPaths = Join-Path (Join-Path (Split-Path -Path $toolsPath -Parent) "analyzers" ) * -Resolve

foreach($analyzersPath in $analyzersPaths)
{
    # Uninstall the language agnostic analyzers.
    if (Test-Path $analyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $analyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Remove($analyzerFilePath.FullName)
            }
        }
    }
}

$project.Type # gives the language name like (C# or VB.NET)
$languageFolder = ""
if($project.Type -eq "C#")
{
    $languageFolder = "cs"
}
if($project.Type -eq "VB.NET")
{
    $languageFolder = "vb"
}
if($languageFolder -eq "")
{
    return
}

foreach($analyzersPath in $analyzersPaths)
{
    # Uninstall language specific analyzers.
    $languageAnalyzersPath = join-path $analyzersPath $languageFolder
    if (Test-Path $languageAnalyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $languageAnalyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                try
                {
                    $project.Object.AnalyzerReferences.Remove($analyzerFilePath.FullName)
                }
                catch
                {

                }
            }
        }
    }
}
```
