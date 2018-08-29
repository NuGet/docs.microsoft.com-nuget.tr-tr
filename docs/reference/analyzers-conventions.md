---
title: NuGet için .NET derleyici platformu Çözümleyicisi biçimler
description: Paketlenmiş ve API veya kitaplık uygulayan NuGet paketleri ile dağıtılmış .NET Çözümleyicileri için kuralları.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 9e833447820c0fb13cf558a45921554e82e2b2df
ms.sourcegitcommit: ddc2b07a788d4a92b9df193c9bbd43db945b14d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/28/2018
ms.locfileid: "43119168"
---
# <a name="analyzer-nuget-formats"></a>Çözümleyici NuGet biçimleri

.NET derleyici Platformu (diğer adıyla "Roslyn"), geliştiricilerin izin [Çözümleyicileri](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) , incelemesine söz dizimi ağacı ve kod semantikleri, yazıldığı gibi. Bu geliştiricilerin oluşturmak için bir yol sağlar ve etki alanına özgü analiz araçları, yardımcı olacak olanlar gibi belirli bir API veya kitaplığı kullanın yol gösterir. Daha fazla bilgi bulabilirsiniz [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub wiki. Ayrıca bkz [kullanım API'niz için bir Canlı kod analizi yazmak için Roslyn](https://msdn.microsoft.com/magazine/dn879356.aspx) MSDN magazine'de.

Çözümleyiciler kendilerini genellikle paketlenir ve API ya da söz konusu kitaplığı NuGet paketlerini bir parçası olarak dağıtılmış.

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

Gördüğünüz gibi Çözümleyicisi DLL'lere yerleştirileceği bir `analyzers` paketi klasörüne.

Çözümleyici uygulaması yerine eski FxCop kuralı devre dışı bırakmak için dahil olan özellik dosyaları yerleştirildiğinde `build` klasör.

Yükleme ve kaldırma kullanarak projeleri destek komut dosyaları `packages.config` yerleştirilir `tools`.

Bu paket hiçbir platforma özgü gereksinimleri olduğundan da unutmayın `platform` klasör atlanmış.


## <a name="analyzers-path-format"></a>Çözümleyiciler yol biçimi

Kullanımını `analyzers` klasördür için kullanılan benzer [hedef çerçeveyi](../create-packages/supporting-multiple-target-frameworks.md)dışında geliştirme konak bağımlılıkları yerine derleme zamanı yolunda tanımlayıcıları açıklar. Genel biçimi aşağıdaki gibidir:

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}/{analyzer_name}.dll

- **framework_name**: *isteğe bağlı* kapsanan DLL'leri çalıştırmak için gereken .NET Framework'ün API yüzey alanı. `dotnet` Roslyn Çözümleyicileri çalışabilen tek bir ana bilgisayar şu anda yalnızca geçerli bir değer olduğundan. Hiçbir hedef belirtilmemişse, DLL'leri uygulamak için varsayılır *tüm* hedefler.
- **supported_language**: DLL uygulandığı, bir dil `cs` (C#) ve `vb` (Visual Basic) ve `fs` (F #). Dil Çözümleyicisi bu dili kullanarak yalnızca bir proje için yüklenmesi gerektiğini gösterir. DLL uygulamak için işleyecektir dil belirtilmezse *tüm* Çözümleyicileri destekleyen diller.
- **analyzer_name**: çözümleyicisinin DLL'leri belirtir. DLL'leri ötesinde ek dosyaları gerekiyorsa, hedefler ya da Özellikler dosyalarıyla birlikte olmalıdır.


## <a name="install-and-uninstall-scripts"></a>Yükleme ve komut dosyaları kaldırma

Kullanıcının proje kullanıyorsanız `packages.config`, gerekir böylece çözümleyiciyi alır MSBuild komut dosyası yürütme gelmez `install.ps1` ve `uninstall.ps1` içinde `tools` klasörün içeriğiyle aşağıda açıklanmıştır.

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


**Uninstall.ps1 dosya içeriği**

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
