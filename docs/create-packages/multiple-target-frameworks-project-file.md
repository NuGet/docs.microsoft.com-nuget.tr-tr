---
title: Proje dosyanızdaki NuGet paketleri için Çoklu hedefleme
description: Proje dosyanızdaki tek bir NuGet paketinin içinden birden çok .NET Framework sürümünü hedeflemek için çeşitli yöntemlerin açıklaması.
author: JonDouglas
ms.author: jodou
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: a05d053340bb2fe795991dfa5a2b95d8625dfd44
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774382"
---
# <a name="support-multiple-net-framework-versions-in-your-project-file"></a>Proje dosyanızda birden çok .NET Framework sürümü destekleme

İlk kez bir proje oluşturduğunuzda, en geniş tüketen projelerle uyumluluk sağladığından .NET Standard sınıf kitaplığı oluşturmanızı öneririz. .NET Standard kullanarak, varsayılan olarak bir .NET kitaplığına [platformlar arası destek](/dotnet/standard/library-guidance/cross-platform-targeting) eklersiniz. Ancak, bazı senaryolarda belirli bir çerçeveyi hedefleyen kodu da eklemeniz gerekebilir. Bu makalede, [SDK stilindeki](../resources/check-project-format.md) projeler için nasıl yapılacağı gösterilmektedir.

SDK stilindeki projeler için, proje dosyanızda birden çok hedef çerçeve ([TFI](/dotnet/standard/frameworks)) desteğini yapılandırabilir ve ardından `dotnet pack` `msbuild /t:pack` paketi oluşturmak için veya kullanabilirsiniz.

> [!NOTE]
> nuget.exe CLı, SDK-stil projelerini paketleme, bu yüzden yalnızca veya kullanmanız gerekir `dotnet pack` `msbuild /t:pack` . Bunun yerine genellikle proje dosyasındaki dosyada bulunan [tüm özellikleri eklemeniz](../reference/msbuild-targets.md#pack-target) önerilir `.nuspec` . SDK olmayan bir projede birden çok .NET Framework sürümünü hedeflemek için bkz. [birden çok .NET Framework sürümünü destekleme](supporting-multiple-target-frameworks.md).

## <a name="create-a-project-that-supports-multiple-net-framework-versions"></a>Çoklu .NET Framework sürümlerini destekleyen bir proje oluşturma

1. Visual Studio 'da ya da kullanarak yeni bir .NET Standard sınıf kitaplığı oluşturun `dotnet new classlib` .

   En iyi uyumluluk için bir .NET Standard sınıf kitaplığı oluşturmanızı öneririz.

2. Hedef çerçeveleri desteklemek için *. csproj* dosyasını düzenleyin. Örneğin, Değiştir
   
   `<TargetFramework>netstandard2.0</TargetFramework>`
   
   Yeni değer:
   
   `<TargetFrameworks>netstandard2.0;net45</TargetFrameworks>`

   XML öğesini tekil iken plural olarak değiştirdiğinizden emin olun ("s" öğesini hem açma hem de kapatma etiketlerine ekleyin).

3. Yalnızca bir tfd içinde çalışacak bir kodunuz varsa, `#if NET45` `#if NETSTANDARD2_0` TFE bağımlı kodu ayırmak için veya kullanabilirsiniz. (Daha fazla bilgi için bkz. [MultiTarget](/dotnet/core/tutorials/libraries#how-to-multitarget).) Örneğin, aşağıdaki kodu kullanabilirsiniz:

   ```csharp
   public string Platform {
      get {
   #if NET45
         return ".NET Framework"
   #elif NETSTANDARD2_0
         return ".NET Standard"
   #else
   #error This code block does not match csproj TargetFrameworks list
   #endif
      }
   }
   ```

4. *. Csproj* öğesine istediğiniz NuGet meta verilerini MSBuild özellikleri olarak ekleyin.

   Kullanılabilir paket meta verileri ve MSBuild özellik adlarının listesi için bkz. [Pack Target](../reference/msbuild-targets.md#pack-target). Ayrıca bkz. [bağımlılık varlıklarını denetleme](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

   Yapı ile ilgili özellikleri NuGet meta verilerinden ayırmak isterseniz, farklı bir `PropertyGroup` Dosya kullanabilir veya NuGet özelliklerini başka bir dosyaya yerleştirebilir ve MSBuild 'in `Import` yönergesini dahil edebilirsiniz. `Directory.Build.Props``Directory.Build.Targets`Ayrıca, MSBuild 15,0 ' den itibaren de desteklenir.

5. Şimdi, `dotnet pack` ve elde edilen *. nupkg* hedeflerini .NET Standard 2,0 ve .NET Framework 4,5 olarak kullanın.

Yukarıdaki adımlar ve 2,2 .NET Core SDK kullanılarak oluşturulan *. csproj* dosyası aşağıda verilmiştir.

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFrameworks>netstandard2.0;net45</TargetFrameworks>
    <Description>Sample project that targets multiple TFMs</Description>
  </PropertyGroup>

</Project>
```

## <a name="see-also"></a>Ayrıca bkz.

* [Hedef çerçeveleri belirtme](/dotnet/standard/frameworks#how-to-specify-target-frameworks)
* [Platformlar arası hedefleme](/dotnet/standard/library-guidance/cross-platform-targeting)
