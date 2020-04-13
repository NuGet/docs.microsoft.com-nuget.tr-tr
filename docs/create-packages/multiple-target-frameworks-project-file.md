---
title: Proje dosyanızda NuGet Paketleri için çoklu hedefleme
description: Tek bir NuGet paketinin içinden birden fazla .NET Framework sürümlerini hedefleyen çeşitli yöntemlerin açıklaması.
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: 1d23759433efb405fa5f0035049befced2c43d6b
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "72380681"
---
# <a name="support-multiple-net-framework-versions-in-your-project-file"></a>Proje dosyanızda birden çok .NET Framework sürümü destekleme

Bir projeyi ilk oluşturduğunuzda, en geniş tüketici proje yelpazesiyle uyumluluk sağladığından bir .NET Standart sınıf kitaplığı oluşturmanızı öneririz. .NET Standard'ı kullanarak, varsayılan olarak bir .NET kitaplığına [çapraz platform desteği](/dotnet/standard/library-guidance/cross-platform-targeting) eklersiniz. Ancak, bazı senaryolarda, belirli bir çerçeveyi hedefleyen kod eklemeniz de gerekebilir. Bu makalede, [SDK tarzı](../resources/check-project-format.md) projeler için bunu nasıl yapacağınızı gösterir.

SDK tarzı projelerde, proje dosyanızda birden çok hedef çerçevesi[(TFM)](/dotnet/standard/frameworks)için `dotnet pack` `msbuild /t:pack` destek yapılandırabilir, ardından paketi kullanabilir veya oluşturabilirsiniz.

> [!NOTE]
> nuget.exe CLI SDK tarzı projeleri paketleme desteklemez, `dotnet pack` bu `msbuild /t:pack`yüzden sadece kullanmalısınız veya . Bunun `.nuspec` yerine, genellikle dosyada bulunan tüm özellikleri proje dosyasına [eklemenizi](../reference/msbuild-targets.md#pack-target) öneririz. SDK tarzı olmayan bir projede birden çok .NET Framework sürümlerini [hedeflemek](supporting-multiple-target-frameworks.md)için bkz.

## <a name="create-a-project-that-supports-multiple-net-framework-versions"></a>Birden çok .NET Framework sürümlerini destekleyen bir proje oluşturma

1. Visual Studio'da yeni bir .NET Standart `dotnet new classlib`sınıf kitaplığı oluşturun veya kullanın.

   En iyi uyumluluk için bir .NET Standart sınıf kitaplığı oluşturmanızı öneririz.

2. Hedef çerçeveleri desteklemek için *.csproj* dosyasını edin. Örneğin, değişiklik
   
   `<TargetFramework>netstandard2.0</TargetFramework>`
   
   yerine şunu yazın:
   
   `<TargetFrameworks>netstandard2.0;net45</TargetFrameworks>`

   XML öğesini tekilden çoğul'a değiştirdiğinizden emin olun (hem açık hem de kapat etiketlere "s" ekleyin).

3. Yalnızca bir TFM'de çalışan bir kodunuz `#if NET45` varsa, TFM'ye bağlı kodu kullanabilir veya `#if NETSTANDARD2_0` ayırabilirsiniz. (Daha fazla bilgi için [bkz.](/dotnet/core/tutorials/libraries#how-to-multitarget) Örneğin, aşağıdaki kodu kullanabilirsiniz:

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

4. MSBuild özellikleri olarak *.csproj istediğiniz* herhangi bir NuGet meta veri ekleyin.

   Kullanılabilir paket meta verileri ve MSBuild özellik adları listesi için [paket hedefine](../reference/msbuild-targets.md#pack-target)bakın. Ayrıca [bkz.](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)

   Yapıyla ilgili özellikleri NuGet meta verilerinden ayırmak istiyorsanız, `PropertyGroup`farklı bir ,nuget özelliklerini başka bir dosyaya `Import` koyabilir ve MSBuild'in yönergesini bunu eklemek için kullanabilirsiniz. `Directory.Build.Props`ve `Directory.Build.Targets` ayrıca MSBuild 15.0 ile başlayan desteklenir.

5. Şimdi, `dotnet pack` kullanım ve elde edilen *.nupkg* hedefleri hem .NET Standart 2.0 ve .NET Framework 4.5.

Aşağıda, önceki adımlar ve .NET Core SDK 2.2 kullanılarak oluşturulan *.csproj* dosyası verilmiştir.

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFrameworks>netstandard2.0;net45</TargetFrameworks>
    <Description>Sample project that targets multiple TFMs</Description>
  </PropertyGroup>

</Project>
```

## <a name="see-also"></a>Ayrıca bkz.

* [Hedef çerçeveler nasıl belirtilir?](/dotnet/standard/frameworks#how-to-specify-target-frameworks)
* [Platformlar arası hedefleme](/dotnet/standard/library-guidance/cross-platform-targeting)
