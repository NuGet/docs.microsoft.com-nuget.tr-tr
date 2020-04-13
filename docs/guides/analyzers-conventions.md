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
# <a name="analyzer-nuget-formats"></a>Analyzer NuGet biçimleri

.NET Derleyici Platformu ("Roslyn" olarak da bilinir), geliştiricilerin kod sözdizimi ağacını ve kod anlamtlarını incelenirken inceleyen [çözümleyiciler](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) oluşturmasına olanak tanır. Bu, geliştiricilere, belirli bir API veya kitaplığın kullanımına rehberlik edecek alanlar gibi etki alanına özgü çözümleme araçları oluşturmanın bir yolunu sağlar. [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub wiki hakkında daha fazla bilgi bulabilirsiniz. Ayrıca makaleye bakın, MSDN Dergisi'nde [API için canlı kod analizörü yazmak için Roslyn kullanın.](https://msdn.microsoft.com/magazine/dn879356.aspx)

Çözümleyicilerin kendileri genellikle söz konusu API veya kitaplığı uygulayan NuGet paketlerinin bir parçası olarak paketlenir ve dağıtılır.

İyi bir örnek için, aşağıdaki içerikleri içeren [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) paketine bakın:

- çözümleyiciler\dotnet\System.Runtime.Analyzers.dll
- çözümleyiciler\dotnet\cs\System.Runtime.CSharp.Analyzers.dll
- çözümleyiciler\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll
- build\System.Runtime.Analyzers.Common.props
- build\System.Runtime.Analyzers.props
- build\System.Runtime.CSharp.Analyzers.props
- build\System.Runtime.VisualBasic.Analyzers.props
- araçlar\install.ps1
- araçlar\uninstall.ps1

Gördüğünüz gibi, çözümleyici DL'leri paketteki `analyzers` bir klasöre yersiniz.

Çözümleyici uygulaması lehine eski FxCop kurallarını devre dışı bırakan sahne dosyaları klasöre `build` yerleştirilir.

Projeleri destekleyen `packages.config` komut dosyalarını yükleyin ve `tools`kaldırın.

Ayrıca, bu paketin platforma özgü gereksinimleri `platform` olmadığından klasörün atlandığına da dikkat edin.


## <a name="analyzers-path-format"></a>Çözümleyiciler yol biçimi

Klasörün `analyzers` kullanımı [hedef çerçeveler](../create-packages/supporting-multiple-target-frameworks.md)için kullanılana benzer , ancak yoldaki belirteçler yapı zamanı yerine geliştirme ana bilgisayar bağımlılıklarını açıklar. Genel biçimi aşağıdaki gibidir:

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}/{analyzer_name}.dll

- **framework_name** ve **sürüm**: .NET Framework'ün, içerdiği DL'lerin çalışması gereken *isteğe bağlı* API yüzey alanı. `dotnet`roslyn çözümleyicileri çalıştırabilen tek ana bilgisayar olduğundan, şu anda tek geçerli değerdir. Hedef belirtilmemişse, DL'lerin *tüm* hedeflere uygulanacağı varsayılır.
- **supported_language**: DLL'nin geçerli olduğu dil, `cs` (C#) ve (Visual Basic) ve `vb` `fs` (F#). Dil, çözümleyicinin yalnızca bu dili kullanan bir proje için yüklenmesi gerektiğini gösterir. Dil belirtilmemişse, DLL'nin çözümleyicileri destekleyen *tüm* dillere uygulanacağı varsayılır.
- **analyzer_name**: çözümleyicinin DL'lerini belirtir. DL'lerin ötesinde ek dosyalara ihtiyacınız varsa, bunlar bir hedef veya özellik dosyaları aracılığıyla eklenmelidir.


## <a name="install-and-uninstall-scripts"></a>Komut dosyalarını yükleme ve kaldırma

Kullanıcının projesi `packages.config`kullanıyorsa, çözümleyiciyi alan MSBuild komut dosyası devreye girmez, `install.ps1` bu `uninstall.ps1` nedenle `tools` aşağıda açıklanan içerikleri klasöre yerleştirmeniz gerekir.

**install.ps1 dosya içeriği**

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


**uninstall.ps1 dosya içeriği**

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
