---
title: NuGet için .NET derleyici platformu Çözümleyicisi biçimler
description: Paketlenmiş ve API veya kitaplık uygulayan NuGet paketleri ile dağıtılmış .NET Çözümleyicileri için kuralları.
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 0a8db9f6c55b7e79f9b338119e0b3ac6cb7a1e35
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324805"
---
# <a name="analyzer-nuget-formats"></a><span data-ttu-id="1540d-103">Çözümleyici NuGet biçimleri</span><span class="sxs-lookup"><span data-stu-id="1540d-103">Analyzer NuGet formats</span></span>

<span data-ttu-id="1540d-104">.NET derleyici Platformu (diğer adıyla "Roslyn") geliştiricilerin oluşturmasını sağlar. [Çözümleyicileri](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) , incelemesine söz dizimi ağacı ve kod semantikleri, yazıldığı gibi.</span><span class="sxs-lookup"><span data-stu-id="1540d-104">The .NET Compiler Platform (also known as "Roslyn") allows developers to create [analyzers](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) that examine the syntax tree and semantics of code as it's being written.</span></span> <span data-ttu-id="1540d-105">Yardımcı olan bir özel API veya kitaplık kılavuzu gibi bu geliştiricilerin etki alanına özgü çözümleme araçları oluşturmak için bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="1540d-105">This provides developers with a way to create domain-specific analysis tools, such as those that would help guide the use of a particular API or library.</span></span> <span data-ttu-id="1540d-106">Daha fazla bilgi bulabilirsiniz [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub wiki.</span><span class="sxs-lookup"><span data-stu-id="1540d-106">You can find more information on the [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub wiki.</span></span> <span data-ttu-id="1540d-107">Ayrıca bkz [kullanım API'niz için bir Canlı kod analizi yazmak için Roslyn](https://msdn.microsoft.com/magazine/dn879356.aspx) MSDN magazine'de.</span><span class="sxs-lookup"><span data-stu-id="1540d-107">Also see the article, [Use Roslyn to Write a Live Code Analyzer for your API](https://msdn.microsoft.com/magazine/dn879356.aspx) in MSDN Magazine.</span></span>

<span data-ttu-id="1540d-108">Çözümleyiciler kendilerini genellikle paketlenir ve API ya da söz konusu kitaplığı NuGet paketlerini bir parçası olarak dağıtılmış.</span><span class="sxs-lookup"><span data-stu-id="1540d-108">Analyzers themselves are typically packaged and distributed as part of the NuGet packages that implement the API or library in question.</span></span>

<span data-ttu-id="1540d-109">İyi bir örnek için bkz: [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) aşağıdaki içeriğe sahip paket:</span><span class="sxs-lookup"><span data-stu-id="1540d-109">For a good example, see the [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) package, which has the following contents:</span></span>

- <span data-ttu-id="1540d-110">analyzers\dotnet\System.Runtime.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="1540d-110">analyzers\dotnet\System.Runtime.Analyzers.dll</span></span>
- <span data-ttu-id="1540d-111">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="1540d-111">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span></span>
- <span data-ttu-id="1540d-112">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="1540d-112">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span></span>
- <span data-ttu-id="1540d-113">build\System.Runtime.Analyzers.Common.props</span><span class="sxs-lookup"><span data-stu-id="1540d-113">build\System.Runtime.Analyzers.Common.props</span></span>
- <span data-ttu-id="1540d-114">build\System.Runtime.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="1540d-114">build\System.Runtime.Analyzers.props</span></span>
- <span data-ttu-id="1540d-115">build\System.Runtime.CSharp.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="1540d-115">build\System.Runtime.CSharp.Analyzers.props</span></span>
- <span data-ttu-id="1540d-116">build\System.Runtime.VisualBasic.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="1540d-116">build\System.Runtime.VisualBasic.Analyzers.props</span></span>
- <span data-ttu-id="1540d-117">tools\install.ps1</span><span class="sxs-lookup"><span data-stu-id="1540d-117">tools\install.ps1</span></span>
- <span data-ttu-id="1540d-118">tools\uninstall.ps1</span><span class="sxs-lookup"><span data-stu-id="1540d-118">tools\uninstall.ps1</span></span>

<span data-ttu-id="1540d-119">Gördüğünüz gibi Çözümleyicisi DLL'lere yerleştirileceği bir `analyzers` paketi klasörüne.</span><span class="sxs-lookup"><span data-stu-id="1540d-119">As you can see, you place the analyzer DLLs into an `analyzers` folder in the package.</span></span>

<span data-ttu-id="1540d-120">Çözümleyici uygulaması yerine eski FxCop kuralı devre dışı bırakmak için dahil olan özellik dosyaları yerleştirildiğinde `build` klasör.</span><span class="sxs-lookup"><span data-stu-id="1540d-120">Props files, which are included to disable legacy FxCop rules in favor of the analyzer implementation, are placed in the `build` folder.</span></span>

<span data-ttu-id="1540d-121">Yükleme ve kaldırma kullanarak projeleri destek komut dosyaları `packages.config` yerleştirilir `tools`.</span><span class="sxs-lookup"><span data-stu-id="1540d-121">Install and uninstall scripts that support projects using `packages.config` are placed in `tools`.</span></span>

<span data-ttu-id="1540d-122">Bu paket hiçbir platforma özgü gereksinimleri olduğundan da unutmayın `platform` klasör atlanmış.</span><span class="sxs-lookup"><span data-stu-id="1540d-122">Also note that because this package has no platform-specific requirements, the `platform` folder is omitted.</span></span>


## <a name="analyzers-path-format"></a><span data-ttu-id="1540d-123">Çözümleyiciler yol biçimi</span><span class="sxs-lookup"><span data-stu-id="1540d-123">Analyzers path format</span></span>

<span data-ttu-id="1540d-124">Kullanımını `analyzers` klasördür için kullanılan benzer [hedef çerçeveyi](../create-packages/supporting-multiple-target-frameworks.md)dışında geliştirme konak bağımlılıkları yerine derleme zamanı yolunda tanımlayıcıları açıklar.</span><span class="sxs-lookup"><span data-stu-id="1540d-124">The use of the `analyzers` folder is similar to that used for [target frameworks](../create-packages/supporting-multiple-target-frameworks.md), except the specifiers in the path describe development host dependencies instead of build-time.</span></span> <span data-ttu-id="1540d-125">Genel biçimi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="1540d-125">The general format is as follows:</span></span>

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}/{analyzer_name}.dll

- <span data-ttu-id="1540d-126">**framework_name**: *isteğe bağlı* kapsanan DLL'leri çalıştırmak için gereken .NET Framework'ün API yüzey alanı.</span><span class="sxs-lookup"><span data-stu-id="1540d-126">**framework_name**: the *optional* API surface area of the .NET Framework that the contained DLLs need to run.</span></span> <span data-ttu-id="1540d-127">`dotnet` Roslyn Çözümleyicileri çalışabilen tek bir ana bilgisayar şu anda yalnızca geçerli bir değer olduğundan.</span><span class="sxs-lookup"><span data-stu-id="1540d-127">`dotnet` is presently the only valid value because Roslyn is the only host that can run analyzers.</span></span> <span data-ttu-id="1540d-128">Hiçbir hedef belirtilmemişse, DLL'leri uygulamak için varsayılır *tüm* hedefler.</span><span class="sxs-lookup"><span data-stu-id="1540d-128">If no target is specified, DLLs are assumed to apply to *all* targets.</span></span>
- <span data-ttu-id="1540d-129">**supported_language**: DLL uygulandığı, bir dil `cs` (C#) ve `vb` (Visual Basic) ve `fs` (F#).</span><span class="sxs-lookup"><span data-stu-id="1540d-129">**supported_language**: the language for which the DLL applies, one of `cs` (C#) and `vb` (Visual Basic), and `fs` (F#).</span></span> <span data-ttu-id="1540d-130">Dil Çözümleyicisi bu dili kullanarak yalnızca bir proje için yüklenmesi gerektiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="1540d-130">The language indicates that the analyzer should be loaded only for a project using that language.</span></span> <span data-ttu-id="1540d-131">DLL uygulamak için işleyecektir dil belirtilmezse *tüm* Çözümleyicileri destekleyen diller.</span><span class="sxs-lookup"><span data-stu-id="1540d-131">If no language is specified then the DLL is assumed to apply to *all* languages that support analyzers.</span></span>
- <span data-ttu-id="1540d-132">**analyzer_name**: çözümleyicisinin DLL'leri belirtir.</span><span class="sxs-lookup"><span data-stu-id="1540d-132">**analyzer_name**: specifies the DLLs of the analyzer.</span></span> <span data-ttu-id="1540d-133">DLL'leri ötesinde ek dosyaları gerekiyorsa, hedefler ya da Özellikler dosyalarıyla birlikte olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1540d-133">If you need additional files beyond DLLs, they must be included through a targets or properties files.</span></span>


## <a name="install-and-uninstall-scripts"></a><span data-ttu-id="1540d-134">Yükleme ve komut dosyaları kaldırma</span><span class="sxs-lookup"><span data-stu-id="1540d-134">Install and uninstall scripts</span></span>

<span data-ttu-id="1540d-135">Kullanıcının proje kullanıyorsanız `packages.config`, yerleştirmeniz gerekir böylece çözümleyiciyi alır MSBuild komut dosyası yürütme gelmez `install.ps1` ve `uninstall.ps1` içinde `tools` klasörün içeriğiyle aşağıda açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="1540d-135">If the user's project is using `packages.config`, the MSBuild script that picks up the analyzer does not come into play, so you should place `install.ps1` and `uninstall.ps1` in the `tools` folder with the contents that are described below.</span></span>

<span data-ttu-id="1540d-136">**install.ps1 dosyası içeriği**</span><span class="sxs-lookup"><span data-stu-id="1540d-136">**install.ps1 file contents**</span></span>

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


<span data-ttu-id="1540d-137">**Uninstall.ps1 dosya içeriği**</span><span class="sxs-lookup"><span data-stu-id="1540d-137">**uninstall.ps1 file contents**</span></span>

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
