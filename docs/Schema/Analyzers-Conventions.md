---
title: ".NET derleme Platform Çözümleyicisi için NuGet biçimleri | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Paketlenmiş ve bir API veya kitaplık uygulaması NuGet paketleri ile dağıtılan .NET çözümleyiciler kuralları."
keywords: "NuGet analyzer kuralları, .NET çözümleyiciler, NuGet ve .NET derleyici platformu, NuGet ve Roslyn"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e44cfa609c14422d50769e512108844cbd2f96a4
ms.sourcegitcommit: 24997b5345a997501fff846c9bd73610245ae0a6
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/31/2018
---
# <a name="analyzer-nuget-formats"></a><span data-ttu-id="4ec29-104">Çözümleyicisi NuGet biçimleri</span><span class="sxs-lookup"><span data-stu-id="4ec29-104">Analyzer NuGet formats</span></span>

<span data-ttu-id="4ec29-105">.NET derleme Platformu (olarak da bilinen "Roslyn") [çözümleyiciler] oluşturmak geliştiriciler izin yazılmakta gibi (https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix), sözdizimi ağacı ve kod semantiği inceleyin.</span><span class="sxs-lookup"><span data-stu-id="4ec29-105">The .NET Compiler Platform (also known as "Roslyn") allow developers to create [analyzers] (https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) that examine the syntax tree and semantics of code as it's being written.</span></span> <span data-ttu-id="4ec29-106">Bu geliştiriciler oluşturmak için bir yol sağlar ve belirli bir API veya kitaplık kullanımını yardımcı olacak olanlar gibi etki alanına özgü çözümleme araçları Kılavuzu.</span><span class="sxs-lookup"><span data-stu-id="4ec29-106">This provides developers with a way to create and domain-specific analysis tools, such as those that would help guide the use of a particular API or library.</span></span> <span data-ttu-id="4ec29-107">Daha fazla bilgi bulabilirsiniz [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub wiki.</span><span class="sxs-lookup"><span data-stu-id="4ec29-107">You can find more information on the [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub wiki.</span></span> <span data-ttu-id="4ec29-108">Ayrıca makalesine bakın [kullanım API için Canlı bir kod Çözümleyicisi yazmak için Roslyn](https://msdn.microsoft.com/magazine/dn879356.aspx) MSDN dergisi içinde.</span><span class="sxs-lookup"><span data-stu-id="4ec29-108">Also see the article, [Use Roslyn to Write a Live Code Analyzer for your API](https://msdn.microsoft.com/magazine/dn879356.aspx) in MSDN Magazine.</span></span>

<span data-ttu-id="4ec29-109">Çözümleyiciler kendilerini genellikle paketlenmiş ve API veya kitaplık söz konusu uygulamak NuGet paketlerini bir parçası olarak dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="4ec29-109">Analyzers themselves are typically packaged and distributed as part of the NuGet packages that implement the API or library in question.</span></span>

<span data-ttu-id="4ec29-110">İyi bir örnek için bkz: [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) aşağıdaki içeriğe sahip paket:</span><span class="sxs-lookup"><span data-stu-id="4ec29-110">For a good example, see the [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) package, which has the following contents:</span></span>

- <span data-ttu-id="4ec29-111">analyzers\dotnet\System.Runtime.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="4ec29-111">analyzers\dotnet\System.Runtime.Analyzers.dll</span></span>
- <span data-ttu-id="4ec29-112">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="4ec29-112">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span></span>
- <span data-ttu-id="4ec29-113">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="4ec29-113">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span></span>
- <span data-ttu-id="4ec29-114">build\System.Runtime.Analyzers.Common.props</span><span class="sxs-lookup"><span data-stu-id="4ec29-114">build\System.Runtime.Analyzers.Common.props</span></span>
- <span data-ttu-id="4ec29-115">build\System.Runtime.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="4ec29-115">build\System.Runtime.Analyzers.props</span></span>
- <span data-ttu-id="4ec29-116">build\System.Runtime.CSharp.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="4ec29-116">build\System.Runtime.CSharp.Analyzers.props</span></span>
- <span data-ttu-id="4ec29-117">build\System.Runtime.VisualBasic.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="4ec29-117">build\System.Runtime.VisualBasic.Analyzers.props</span></span>
- <span data-ttu-id="4ec29-118">tools\install.ps1</span><span class="sxs-lookup"><span data-stu-id="4ec29-118">tools\install.ps1</span></span>
- <span data-ttu-id="4ec29-119">tools\uninstall.ps1</span><span class="sxs-lookup"><span data-stu-id="4ec29-119">tools\uninstall.ps1</span></span>

<span data-ttu-id="4ec29-120">Gördüğünüz gibi Çözümleyicisi DLL'leri içine yerleştirin bir `analyzers` paket klasöründe.</span><span class="sxs-lookup"><span data-stu-id="4ec29-120">As you can see, you place the analyzer DLLs into an `analyzers` folder in the package.</span></span>

<span data-ttu-id="4ec29-121">Çözümleyici uygulama lehinde eski FxCop kuralları devre dışı bırakmak için dahil edilen, özellik dosyaları yerleştirilir `build` klasör.</span><span class="sxs-lookup"><span data-stu-id="4ec29-121">Props files, which are included to disable legacy FxCop rules in favor of the analyzer implementation, are placed in the `build` folder.</span></span>

<span data-ttu-id="4ec29-122">Yükleme ve kaldırma kullanarak projeleri destek komut dosyaları `packages.config` yerleştirilir `tools`.</span><span class="sxs-lookup"><span data-stu-id="4ec29-122">Install and uninstall scripts that support projects using `packages.config` are placed in `tools`.</span></span>

<span data-ttu-id="4ec29-123">Bu paket hiçbir platforma özgü gereksinimler olduğundan ayrıca `platform` klasörü atlanmış.</span><span class="sxs-lookup"><span data-stu-id="4ec29-123">Also note that because this package has no platform-specific requirements, the `platform` folder is omitted.</span></span>


## <a name="analyzers-path-format"></a><span data-ttu-id="4ec29-124">Çözümleyiciler yol biçimi</span><span class="sxs-lookup"><span data-stu-id="4ec29-124">Analyzers path format</span></span>

<span data-ttu-id="4ec29-125">Kullanımını `analyzers` klasördür için kullanılan benzer [hedef çerçeveler](../create-packages/supporting-multiple-target-frameworks.md), derleme zamanı yerine geliştirme konak bağımlılıkları yolunda tanımlayıcıları açıklayın dışında.</span><span class="sxs-lookup"><span data-stu-id="4ec29-125">The use of the `analyzers` folder is similar to that used for [target frameworks](../create-packages/supporting-multiple-target-frameworks.md), except the specifiers in the path describe development host dependencies instead of build-time.</span></span> <span data-ttu-id="4ec29-126">Genel biçimi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="4ec29-126">The general format is as follows:</span></span>

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}}/{analyzer_name}.dll

- <span data-ttu-id="4ec29-127">**framework_name**: *isteğe bağlı* kapsanan DLL'leri çalıştırmak için gereken .NET Framework'ün yüzey alanını API.</span><span class="sxs-lookup"><span data-stu-id="4ec29-127">**framework_name**: the *optional* API surface area of the .NET Framework that the contained DLLs need to run.</span></span> <span data-ttu-id="4ec29-128">`dotnet`Roslyn çözümleyiciler çalıştırabilirsiniz yalnızca konak olduğundan şu anda yalnızca geçerli değeridir.</span><span class="sxs-lookup"><span data-stu-id="4ec29-128">`dotnet` is presently the only valid value because Roslyn is the only host that can run analyzers.</span></span> <span data-ttu-id="4ec29-129">Hiçbir hedef belirtilirse, DLL'leri uygulamak için varsayılır *tüm* hedefler.</span><span class="sxs-lookup"><span data-stu-id="4ec29-129">If no target is specified, DLLs are assumed to apply to *all* targets.</span></span>
- <span data-ttu-id="4ec29-130">**supported_language**: DLL uygulandığı, aşağıdakilerden birini dil `cs` (C#) ve `vb` (Visual Basic) ve `fs` (F #).</span><span class="sxs-lookup"><span data-stu-id="4ec29-130">**supported_language**: the language for which the DLL applies, one of `cs` (C#) and `vb` (Visual Basic), and `fs` (F#).</span></span> <span data-ttu-id="4ec29-131">Dil Çözümleyicisi yalnızca o dili kullanarak proje için yüklenmesi gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="4ec29-131">The language indicates that the analyzer should be loaded only for a project using that language.</span></span> <span data-ttu-id="4ec29-132">DLL uygulamak için varsayılır sonra hiçbir dil belirtilmiş olup olmadığını *tüm* çözümleyiciler destek diller.</span><span class="sxs-lookup"><span data-stu-id="4ec29-132">If no language is specified then DLL is assumed to apply to *all* languages that support analyzers.</span></span>
- <span data-ttu-id="4ec29-133">**analyzer_name**: Çözümleyicisi dll belirtir.</span><span class="sxs-lookup"><span data-stu-id="4ec29-133">**analyzer_name**: specifies the DLLs of the analyzer.</span></span> <span data-ttu-id="4ec29-134">DLL'leri ötesinde ek dosyalar gerekiyorsa, bunlar hedefler ya da Özellikler dosyalar ile dahil edilmelidir.</span><span class="sxs-lookup"><span data-stu-id="4ec29-134">If you need additional files beyond DLLs, they must be included through a targets or properties files.</span></span>


## <a name="install-and-uninstall-scripts"></a><span data-ttu-id="4ec29-135">Yükleme ve komut dosyaları kaldırma</span><span class="sxs-lookup"><span data-stu-id="4ec29-135">Install and uninstall scripts</span></span>

<span data-ttu-id="4ec29-136">Kullanıcının proje kullanıyorsanız `packages.config`, gerekir böylece Çözümleyicisi Çekmeleri MSBuild komut dosyası yürütme gelmez `install.ps1` ve `uninstall.ps1` içinde `tools` aşağıda açıklanan içeriğiyle klasör.</span><span class="sxs-lookup"><span data-stu-id="4ec29-136">If the user's project is using `packages.config`, the MSBuild script that picks up the analyzer does not come into play, so you should `install.ps1` and `uninstall.ps1` in the `tools` folder with the contents that are described below.</span></span>

<span data-ttu-id="4ec29-137">**install.ps1 dosyası içeriği**</span><span class="sxs-lookup"><span data-stu-id="4ec29-137">**install.ps1 file contents**</span></span>

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


<span data-ttu-id="4ec29-138">**Uninstall.ps1 dosya içerikleri**</span><span class="sxs-lookup"><span data-stu-id="4ec29-138">**uninstall.ps1 file contents**</span></span>

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
