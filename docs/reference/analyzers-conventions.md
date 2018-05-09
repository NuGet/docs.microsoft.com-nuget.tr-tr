---
title: NuGet için .NET derleyici Platform Çözümleyicisi biçimleri
description: Paketlenmiş ve bir API veya kitaplık uygulaması NuGet paketleri ile dağıtılan .NET çözümleyiciler kuralları.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 57ab485c8062b0515c292b68ecb5a3628b6e3e9d
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/28/2018
---
# <a name="analyzer-nuget-formats"></a>Çözümleyicisi NuGet biçimleri

.NET derleme Platformu (olarak da bilinen "Roslyn") oluşturmak geliştiriciler izin [çözümleyiciler](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) , incelemesine sözdizimi ağacı ve kod semantiği yazılmakta gibi. Bu geliştiriciler oluşturmak için bir yol sağlar ve belirli bir API veya kitaplık kullanımını yardımcı olacak olanlar gibi etki alanına özgü çözümleme araçları Kılavuzu. Daha fazla bilgi bulabilirsiniz [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub wiki. Ayrıca makalesine bakın [kullanım API için Canlı bir kod Çözümleyicisi yazmak için Roslyn](https://msdn.microsoft.com/magazine/dn879356.aspx) MSDN dergisi içinde.

Çözümleyiciler kendilerini genellikle paketlenmiş ve API veya kitaplık söz konusu uygulamak NuGet paketlerini bir parçası olarak dağıtılır.

İyi bir örnek için bkz: [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) aşağıdaki içeriğe sahip paket:

- analyzers\dotnet\System.Runtime.Analyzers.dll
- analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll
- analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll
- build\System.Runtime.Analyzers.common.props
- build\System.Runtime.Analyzers.props
- build\System.Runtime.CSharp.Analyzers.props
- build\System.Runtime.VisualBasic.Analyzers.props
- tools\install.ps1
- tools\uninstall.ps1

Gördüğünüz gibi Çözümleyicisi DLL'leri içine yerleştirin bir `analyzers` paket klasöründe.

Çözümleyici uygulama lehinde eski FxCop kuralları devre dışı bırakmak için dahil edilen, özellik dosyaları yerleştirilir `build` klasör.

Yükleme ve kaldırma kullanarak projeleri destek komut dosyaları `packages.config` yerleştirilir `tools`.

Bu paket hiçbir platforma özgü gereksinimler olduğundan ayrıca `platform` klasörü atlanmış.


## <a name="analyzers-path-format"></a>Çözümleyiciler yol biçimi

Kullanımını `analyzers` klasördür için kullanılan benzer [hedef çerçeveler](../create-packages/supporting-multiple-target-frameworks.md), derleme zamanı yerine geliştirme konak bağımlılıkları yolunda tanımlayıcıları açıklayın dışında. Genel biçimi aşağıdaki gibidir:

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}}/{analyzer_name}.dll

- **framework_name**: *isteğe bağlı* kapsanan DLL'leri çalıştırmak için gereken .NET Framework'ün yüzey alanını API. `dotnet` Roslyn çözümleyiciler çalıştırabilirsiniz yalnızca konak olduğundan şu anda yalnızca geçerli değeridir. Hiçbir hedef belirtilirse, DLL'leri uygulamak için varsayılır *tüm* hedefler.
- **supported_language**: DLL uygulandığı, aşağıdakilerden birini dil `cs` (C#) ve `vb` (Visual Basic) ve `fs` (F #). Dil Çözümleyicisi yalnızca o dili kullanarak proje için yüklenmesi gerektiğini belirtir. DLL uygulamak için varsayılır sonra hiçbir dil belirtilmiş olup olmadığını *tüm* çözümleyiciler destek diller.
- **analyzer_name**: Çözümleyicisi dll belirtir. DLL'leri ötesinde ek dosyalar gerekiyorsa, bunlar hedefler ya da Özellikler dosyalar ile dahil edilmelidir.


## <a name="install-and-uninstall-scripts"></a>Yükleme ve komut dosyaları kaldırma

Kullanıcının proje kullanıyorsanız `packages.config`, gerekir böylece Çözümleyicisi Çekmeleri MSBuild komut dosyası yürütme gelmez `install.ps1` ve `uninstall.ps1` içinde `tools` aşağıda açıklanan içeriğiyle klasör.

**install.ps1 dosyası içeriği**

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


**Uninstall.ps1 dosya içerikleri**

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
