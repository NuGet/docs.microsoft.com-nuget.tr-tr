---
title: NuGet için .NET Compiler Platform çözümleyici biçimleri
description: Bir API veya kitaplık uygulayan NuGet paketleri ile paketlenmiş ve dağıtılan .NET Çözümleyicileri için kurallar.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 0a8db9f6c55b7e79f9b338119e0b3ac6cb7a1e35
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69520596"
---
# <a name="analyzer-nuget-formats"></a><span data-ttu-id="52452-103">Çözümleyici NuGet biçimleri</span><span class="sxs-lookup"><span data-stu-id="52452-103">Analyzer NuGet formats</span></span>

<span data-ttu-id="52452-104">.NET Compiler Platform ("Roslyn" olarak da bilinir), geliştiricilerin yazıldığı haliyle kodun sözdizimi ağacını ve semantiğini inceleyecek [çözümleyiciler](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) oluşturmalarına olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="52452-104">The .NET Compiler Platform (also known as "Roslyn") allows developers to create [analyzers](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) that examine the syntax tree and semantics of code as it's being written.</span></span> <span data-ttu-id="52452-105">Bu, geliştiricilere belirli bir API veya kitaplığın kullanılmasına kılavuzluk eden gibi, etki alanına özgü analiz araçları oluşturmak için bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="52452-105">This provides developers with a way to create domain-specific analysis tools, such as those that would help guide the use of a particular API or library.</span></span> <span data-ttu-id="52452-106">[.Net/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub wiki hakkında daha fazla bilgi bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="52452-106">You can find more information on the [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub wiki.</span></span> <span data-ttu-id="52452-107">Ayrıca, MSDN Magazine 'teki [API 'niz Için canlı bir kod Çözümleyicisi yazmak Için Roslyn](https://msdn.microsoft.com/magazine/dn879356.aspx) ' yi kullanma makalesine bakın.</span><span class="sxs-lookup"><span data-stu-id="52452-107">Also see the article, [Use Roslyn to Write a Live Code Analyzer for your API](https://msdn.microsoft.com/magazine/dn879356.aspx) in MSDN Magazine.</span></span>

<span data-ttu-id="52452-108">Çözümleyiciler, genellikle, söz konusu API veya kitaplığı uygulayan NuGet paketlerinin bir parçası olarak paketlenir ve dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="52452-108">Analyzers themselves are typically packaged and distributed as part of the NuGet packages that implement the API or library in question.</span></span>

<span data-ttu-id="52452-109">İyi bir örnek için, aşağıdaki içeriğe sahip olan [System. Runtime. çözümleyiciler](https://www.nuget.org/packages/System.Runtime.Analyzers) paketine bakın:</span><span class="sxs-lookup"><span data-stu-id="52452-109">For a good example, see the [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) package, which has the following contents:</span></span>

- <span data-ttu-id="52452-110">analyzers\dotnet\System.Runtime.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="52452-110">analyzers\dotnet\System.Runtime.Analyzers.dll</span></span>
- <span data-ttu-id="52452-111">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="52452-111">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span></span>
- <span data-ttu-id="52452-112">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="52452-112">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span></span>
- <span data-ttu-id="52452-113">build\System.Runtime.Analyzers.Common.props</span><span class="sxs-lookup"><span data-stu-id="52452-113">build\System.Runtime.Analyzers.Common.props</span></span>
- <span data-ttu-id="52452-114">build\System.Runtime.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="52452-114">build\System.Runtime.Analyzers.props</span></span>
- <span data-ttu-id="52452-115">build\System.Runtime.CSharp.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="52452-115">build\System.Runtime.CSharp.Analyzers.props</span></span>
- <span data-ttu-id="52452-116">build\System.Runtime.VisualBasic.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="52452-116">build\System.Runtime.VisualBasic.Analyzers.props</span></span>
- <span data-ttu-id="52452-117">tools\ınstall.exe</span><span class="sxs-lookup"><span data-stu-id="52452-117">tools\install.ps1</span></span>
- <span data-ttu-id="52452-118">tools\uninstall.exe</span><span class="sxs-lookup"><span data-stu-id="52452-118">tools\uninstall.ps1</span></span>

<span data-ttu-id="52452-119">Gördüğünüz gibi, çözümleyici dll 'lerini paketteki bir `analyzers` klasöre yerleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="52452-119">As you can see, you place the analyzer DLLs into an `analyzers` folder in the package.</span></span>

<span data-ttu-id="52452-120">Çözümleyici uygulamasının yerine eski FxCop kurallarını devre dışı bırakmak için bulunan props dosyaları `build` klasörüne yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="52452-120">Props files, which are included to disable legacy FxCop rules in favor of the analyzer implementation, are placed in the `build` folder.</span></span>

<span data-ttu-id="52452-121">Kullanılarak `packages.config` projeleri destekleyen betikleri yükleme ve kaldırma komutları içine `tools`yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="52452-121">Install and uninstall scripts that support projects using `packages.config` are placed in `tools`.</span></span>

<span data-ttu-id="52452-122">Ayrıca, bu paketin platforma özgü gereksinimleri olmadığından, `platform` klasörün atlandığına de göz önünde unutmayın.</span><span class="sxs-lookup"><span data-stu-id="52452-122">Also note that because this package has no platform-specific requirements, the `platform` folder is omitted.</span></span>


## <a name="analyzers-path-format"></a><span data-ttu-id="52452-123">Çözümleyiciler yol biçimi</span><span class="sxs-lookup"><span data-stu-id="52452-123">Analyzers path format</span></span>

<span data-ttu-id="52452-124">`analyzers` Klasörün kullanımı, [hedef çerçeveler](../create-packages/supporting-multiple-target-frameworks.md)için kullanılan ile benzerdir, yoldaki tanımlayıcılar derleme zamanı yerine geliştirme ana bilgisayar bağımlılıklarını da anlatmaktadır.</span><span class="sxs-lookup"><span data-stu-id="52452-124">The use of the `analyzers` folder is similar to that used for [target frameworks](../create-packages/supporting-multiple-target-frameworks.md), except the specifiers in the path describe development host dependencies instead of build-time.</span></span> <span data-ttu-id="52452-125">Genel biçim aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="52452-125">The general format is as follows:</span></span>

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}/{analyzer_name}.dll

- <span data-ttu-id="52452-126">**framework_name**: Içerdiği dll 'lerin çalıştırılması gereken .NET Framework *isteğe bağlı* API yüzey alanı.</span><span class="sxs-lookup"><span data-stu-id="52452-126">**framework_name**: the *optional* API surface area of the .NET Framework that the contained DLLs need to run.</span></span> <span data-ttu-id="52452-127">`dotnet`Şu anda tek geçerli değerdir çünkü Roslyn, çözümleyiciler çalıştırabildiğinden tek ana bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="52452-127">`dotnet` is presently the only valid value because Roslyn is the only host that can run analyzers.</span></span> <span data-ttu-id="52452-128">Hiçbir hedef belirtilmemişse, dll 'Lerin *Tüm* hedeflere uygulanacak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="52452-128">If no target is specified, DLLs are assumed to apply to *all* targets.</span></span>
- <span data-ttu-id="52452-129">**supported_language** `cs` : DLL 'nin uygulandığı dil (( `fs` C#) ve `vb` (Visual Basic) ve (F#).</span><span class="sxs-lookup"><span data-stu-id="52452-129">**supported_language**: the language for which the DLL applies, one of `cs` (C#) and `vb` (Visual Basic), and `fs` (F#).</span></span> <span data-ttu-id="52452-130">Dil, çözümleyici 'nin yalnızca bu dil kullanılarak bir proje için yüklenmesi gerektiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="52452-130">The language indicates that the analyzer should be loaded only for a project using that language.</span></span> <span data-ttu-id="52452-131">Hiçbir dil belirtilmemişse, DLL 'nin Çözümleyicileri destekleyen *Tüm* dillere uygulanacağını kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="52452-131">If no language is specified then the DLL is assumed to apply to *all* languages that support analyzers.</span></span>
- <span data-ttu-id="52452-132">**analyzer_name**: çözümleyici 'Nin dll 'lerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="52452-132">**analyzer_name**: specifies the DLLs of the analyzer.</span></span> <span data-ttu-id="52452-133">Dll 'Lerden daha fazla dosya gerekiyorsa, bunlar bir hedefler veya özellikler dosyalarına dahil olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="52452-133">If you need additional files beyond DLLs, they must be included through a targets or properties files.</span></span>


## <a name="install-and-uninstall-scripts"></a><span data-ttu-id="52452-134">Betikleri yükleme ve kaldırma</span><span class="sxs-lookup"><span data-stu-id="52452-134">Install and uninstall scripts</span></span>

<span data-ttu-id="52452-135">Kullanıcının projesi kullanıyorsa `packages.config`, çözümleyici 'yi yükleyen MSBuild betiği Play 'e gelmez, bu nedenle `tools` klasörü aşağıda açıklanan içerikle birlikte `uninstall.ps1` yerleştirmeniz `install.ps1` gerekir.</span><span class="sxs-lookup"><span data-stu-id="52452-135">If the user's project is using `packages.config`, the MSBuild script that picks up the analyzer does not come into play, so you should place `install.ps1` and `uninstall.ps1` in the `tools` folder with the contents that are described below.</span></span>

<span data-ttu-id="52452-136">**. ps1 dosya içeriğini install**</span><span class="sxs-lookup"><span data-stu-id="52452-136">**install.ps1 file contents**</span></span>

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


<span data-ttu-id="52452-137">**. ps1 dosya içeriğini kaldır**</span><span class="sxs-lookup"><span data-stu-id="52452-137">**uninstall.ps1 file contents**</span></span>

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
