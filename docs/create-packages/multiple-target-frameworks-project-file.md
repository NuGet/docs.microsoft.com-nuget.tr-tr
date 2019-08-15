---
title: Proje dosyanızdaki NuGet paketleri için Çoklu hedefleme
description: Tek bir NuGet paketinin içinden birden çok .NET Framework sürümünü hedeflemek için çeşitli yöntemlerin açıklaması.
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: 8c1d8a479747f6f7bce388c1555589543c8824a0
ms.sourcegitcommit: fc1b716afda999148eb06d62beedb350643eb346
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69020067"
---
# <a name="support-multiple-net-framework-versions-in-your-project-file"></a>Proje dosyanızda birden çok .NET Framework sürümü destekleme

İlk kez bir proje oluşturduğunuzda, en geniş tüketen projelerle uyumluluk sağladığından .NET Standard sınıf kitaplığı oluşturmanızı öneririz. .NET Standard kullanarak, varsayılan olarak bir .NET kitaplığına [platformlar arası destek](/dotnet/standard/library-guidance/cross-platform-targeting) eklersiniz. Ancak, bazı senaryolarda belirli bir çerçeveyi hedefleyen kodu da eklemeniz gerekebilir. Bu makalede, [SDK stilindeki](../resources/check-project-format.md) projeler için nasıl yapılacağı gösterilmektedir.

SDK stilindeki projeler için, proje dosyanızda birden çok hedef çerçeve ([TFI](/dotnet/standard/frameworks)) desteğini yapılandırabilir ve ardından paketi oluşturmak için veya `dotnet pack` `msbuild /t:pack` kullanabilirsiniz.

> [!NOTE]
> NuGet. exe CLI, paketleme SDK stili projelerini desteklemez, bu nedenle yalnızca veya `dotnet pack` `msbuild /t:pack`kullanmanız gerekir. Bunun yerine genellikle `.nuspec` proje dosyasındaki dosyada bulunan [tüm özellikleri eklemeniz](../reference/msbuild-targets.md#pack-target) önerilir. SDK olmayan bir projede birden çok .NET Framework sürümünü hedeflemek için bkz. [birden çok .NET Framework sürümünü destekleme](supporting-multiple-target-frameworks.md).

## <a name="create-a-project-that-supports-multiple-net-framework-versions"></a>Çoklu .NET Framework sürümlerini destekleyen bir proje oluşturma

1. Visual Studio 'da ya da kullanarak `dotnet new classlib`yeni bir .NET Standard sınıf kitaplığı oluşturun.

   En iyi uyumluluk için bir .NET Standard sınıf kitaplığı oluşturmanızı öneririz.

2. Hedef çerçeveleri desteklemek için *. csproj* dosyasını düzenleyin. Örneğin, Değiştir
   
   `<TargetFramework>netstandard2.0</TargetFramework>`
   
   Yeni değer:
   
   `<TargetFrameworks>netstandard2.0;net45</TargetFrameworks>`

   XML öğesini tekil iken plural olarak değiştirdiğinizden emin olun ("s" öğesini hem açma hem de kapatma etiketlerine ekleyin).

3. Yalnızca bir tfd içinde çalışacak bir kodunuz varsa, TFE bağımlı kodu ayırmak için `#if NET45` veya `#if NETSTANDARD20` kullanabilirsiniz. (Daha fazla bilgi için bkz. [MultiTarget](/dotnet/core/tutorials/libraries#how-to-multitarget).) Örneğin, aşağıdaki kodu kullanabilirsiniz:

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

   Yapı ile ilgili özellikleri NuGet meta verilerinden ayırmak isterseniz, farklı `PropertyGroup`bir dosya kullanabilir veya NuGet özelliklerini başka bir dosyaya yerleştirebilir ve MSBuild 'in `Import` yönergesini dahil edebilirsiniz. `Directory.Build.Props`Ayrıca `Directory.Build.Targets` , MSBuild 15,0 ' den itibaren de desteklenir.

5. Şimdi, ve `dotnet pack` elde edilen *. nupkg* hedeflerini .NET Standard 2,0 ve .NET Framework 4,5 olarak kullanın.

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
