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
# <a name="analyzer-nuget-formats"></a>Çözümleyici NuGet biçimleri

.NET Compiler Platform ("Roslyn" olarak da bilinir), geliştiricilerin yazıldığı haliyle kodun sözdizimi ağacını ve semantiğini inceleyecek [çözümleyiciler](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) oluşturmalarına olanak tanır. Bu, geliştiricilere belirli bir API veya kitaplığın kullanılmasına kılavuzluk eden gibi, etki alanına özgü analiz araçları oluşturmak için bir yol sağlar. [.Net/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub wiki hakkında daha fazla bilgi bulabilirsiniz. Ayrıca, MSDN Magazine 'teki [API 'niz Için canlı bir kod Çözümleyicisi yazmak Için Roslyn](https://msdn.microsoft.com/magazine/dn879356.aspx) ' yi kullanma makalesine bakın.

Çözümleyiciler, genellikle, söz konusu API veya kitaplığı uygulayan NuGet paketlerinin bir parçası olarak paketlenir ve dağıtılır.

İyi bir örnek için, aşağıdaki içeriğe sahip olan [System. Runtime. çözümleyiciler](https://www.nuget.org/packages/System.Runtime.Analyzers) paketine bakın:

- analyzers\dotnet\System.Runtime.Analyzers.dll
- analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll
- analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll
- build\System.Runtime.Analyzers.Common.props
- build\System.Runtime.Analyzers.props
- build\System.Runtime.CSharp.Analyzers.props
- build\System.Runtime.VisualBasic.Analyzers.props
- tools\ınstall.exe
- tools\uninstall.exe

Gördüğünüz gibi, çözümleyici dll 'lerini paketteki bir `analyzers` klasöre yerleştirebilirsiniz.

Çözümleyici uygulamasının yerine eski FxCop kurallarını devre dışı bırakmak için bulunan props dosyaları `build` klasörüne yerleştirilir.

Kullanılarak `packages.config` projeleri destekleyen betikleri yükleme ve kaldırma komutları içine `tools`yerleştirilir.

Ayrıca, bu paketin platforma özgü gereksinimleri olmadığından, `platform` klasörün atlandığına de göz önünde unutmayın.


## <a name="analyzers-path-format"></a>Çözümleyiciler yol biçimi

`analyzers` Klasörün kullanımı, [hedef çerçeveler](../create-packages/supporting-multiple-target-frameworks.md)için kullanılan ile benzerdir, yoldaki tanımlayıcılar derleme zamanı yerine geliştirme ana bilgisayar bağımlılıklarını da anlatmaktadır. Genel biçim aşağıdaki gibidir:

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}/{analyzer_name}.dll

- **framework_name**: Içerdiği dll 'lerin çalıştırılması gereken .NET Framework *isteğe bağlı* API yüzey alanı. `dotnet`Şu anda tek geçerli değerdir çünkü Roslyn, çözümleyiciler çalıştırabildiğinden tek ana bilgisayar. Hiçbir hedef belirtilmemişse, dll 'Lerin *Tüm* hedeflere uygulanacak kabul edilir.
- **supported_language** `cs` : DLL 'nin uygulandığı dil (( `fs` C#) ve `vb` (Visual Basic) ve (F#). Dil, çözümleyici 'nin yalnızca bu dil kullanılarak bir proje için yüklenmesi gerektiğini gösterir. Hiçbir dil belirtilmemişse, DLL 'nin Çözümleyicileri destekleyen *Tüm* dillere uygulanacağını kabul edilir.
- **analyzer_name**: çözümleyici 'Nin dll 'lerini belirtir. Dll 'Lerden daha fazla dosya gerekiyorsa, bunlar bir hedefler veya özellikler dosyalarına dahil olmalıdır.


## <a name="install-and-uninstall-scripts"></a>Betikleri yükleme ve kaldırma

Kullanıcının projesi kullanıyorsa `packages.config`, çözümleyici 'yi yükleyen MSBuild betiği Play 'e gelmez, bu nedenle `tools` klasörü aşağıda açıklanan içerikle birlikte `uninstall.ps1` yerleştirmeniz `install.ps1` gerekir.

**. ps1 dosya içeriğini install**

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


**. ps1 dosya içeriğini kaldır**

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
