---
title: NuGet için .NET Compiler Platform çözümleyici biçimleri
description: Bir API veya kitaplık uygulayan NuGet paketleri ile paketlenmiş ve dağıtılan .NET Çözümleyicileri için kurallar.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 63880b6b9bbfe6aac9cc6419d6a972062eea3495
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774131"
---
# <a name="analyzer-nuget-formats"></a>Çözümleyici NuGet biçimleri

.NET Compiler Platform ("Roslyn" olarak da bilinir), geliştiricilerin yazıldığı haliyle kodun sözdizimi ağacını ve semantiğini inceleyecek [çözümleyiciler](https://github.com/dotnet/roslyn/blob/master/docs/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix.md) oluşturmalarına olanak tanır. Bu, geliştiricilere belirli bir API veya kitaplığın kullanılmasına kılavuzluk eden gibi, etki alanına özgü analiz araçları oluşturmak için bir yol sağlar. [.Net/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub wiki hakkında daha fazla bilgi bulabilirsiniz. Ayrıca, MSDN Magazine 'teki [API 'niz Için canlı bir kod Çözümleyicisi yazmak Için Roslyn](/archive/msdn-magazine/2014/special-issue/csharp-and-visual-basic-use-roslyn-to-write-a-live-code-analyzer-for-your-api) ' yi kullanma makalesine bakın.

Çözümleyiciler, genellikle, söz konusu API veya kitaplığı uygulayan NuGet paketlerinin bir parçası olarak paketlenir ve dağıtılır.

İyi bir örnek için, aşağıdaki içeriğe sahip olan [System. Runtime. çözümleyiciler](https://www.nuget.org/packages/System.Runtime.Analyzers) paketine bakın:

- analyzers\dotnet\System.Runtime.Analyzers.dll
- analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll
- analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll
- build\System.Runtime.Analyzers.Common.props
- build\System.Runtime.Analyzers.props
- build\System.Runtime.CSharp.Analyzers.props
- build\System.Runtime.VisualBasic.Analyzers.props
- tools\install.ps1
- tools\uninstall.ps1

Gördüğünüz gibi, çözümleyici dll 'Lerini `analyzers` paketteki bir klasöre yerleştirebilirsiniz.

Çözümleyici uygulamasının yerine eski FxCop kurallarını devre dışı bırakmak için bulunan props dosyaları `build` klasörüne yerleştirilir.

Kullanılarak projeleri destekleyen betikleri yükleme ve kaldırma komutları `packages.config` içine yerleştirilir `tools` .

Ayrıca, bu paketin platforma özgü gereksinimleri olmadığından, klasörün atlandığına de göz önünde unutmayın `platform` .


## <a name="analyzers-path-format"></a>Çözümleyiciler yol biçimi

Klasörün kullanımı, `analyzers` [hedef çerçeveler](../create-packages/supporting-multiple-target-frameworks.md)için kullanılan ile benzerdir, yoldaki tanımlayıcılar derleme zamanı yerine geliştirme ana bilgisayar bağımlılıklarını da anlatmaktadır. Genel biçim aşağıdaki gibidir:

```
$/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}/{analyzer_name}.dll
```

- **framework_name** ve **Sürüm**: içerilen dll 'lerin çalıştırılması gereken .NET Framework *isteğe bağlı* API yüzey alanı. `dotnet` Şu anda tek geçerli değerdir çünkü Roslyn, çözümleyiciler çalıştırabildiğinden tek ana bilgisayar. Hiçbir hedef belirtilmemişse, dll 'Lerin *Tüm* hedeflere uygulanacak kabul edilir.
- **supported_language**: DLL 'nin uygulandığı dil `cs` (C#) ve `vb` (Visual Basic) ve `fs` (F #). Dil, çözümleyici 'nin yalnızca bu dil kullanılarak bir proje için yüklenmesi gerektiğini gösterir. Hiçbir dil belirtilmemişse, DLL 'nin Çözümleyicileri destekleyen *Tüm* dillere uygulanacağını kabul edilir.
- **analyzer_name**: çözümleyicinin dll 'lerini belirtir. Dll 'Lerden daha fazla dosya gerekiyorsa, bunlar bir hedefler veya özellikler dosyalarına dahil olmalıdır.


## <a name="install-and-uninstall-scripts"></a>Betikleri yükleme ve kaldırma

Kullanıcının projesi kullanıyorsa `packages.config` , çözümleyici 'yi yükleyen MSBuild betiği Play 'e gelmez, `install.ps1` Bu nedenle `uninstall.ps1` `tools` klasörü aşağıda açıklanan içerikle birlikte yerleştirmeniz gerekir.

**Dosya içeriğiniinstall.ps1**

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


**Dosya içeriğiniuninstall.ps1**

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
