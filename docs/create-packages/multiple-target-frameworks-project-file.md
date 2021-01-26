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
# <a name="support-multiple-net-framework-versions-in-your-project-file"></a><span data-ttu-id="eb676-103">Proje dosyanızda birden çok .NET Framework sürümü destekleme</span><span class="sxs-lookup"><span data-stu-id="eb676-103">Support multiple .NET Framework versions in your project file</span></span>

<span data-ttu-id="eb676-104">İlk kez bir proje oluşturduğunuzda, en geniş tüketen projelerle uyumluluk sağladığından .NET Standard sınıf kitaplığı oluşturmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="eb676-104">When you first create a project, we recommend you create a .NET Standard class library, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="eb676-105">.NET Standard kullanarak, varsayılan olarak bir .NET kitaplığına [platformlar arası destek](/dotnet/standard/library-guidance/cross-platform-targeting) eklersiniz.</span><span class="sxs-lookup"><span data-stu-id="eb676-105">By using .NET Standard, you add [cross-platform support](/dotnet/standard/library-guidance/cross-platform-targeting) to a .NET library by default.</span></span> <span data-ttu-id="eb676-106">Ancak, bazı senaryolarda belirli bir çerçeveyi hedefleyen kodu da eklemeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="eb676-106">However, in some scenarios, you may also need to include code that targets a particular framework.</span></span> <span data-ttu-id="eb676-107">Bu makalede, [SDK stilindeki](../resources/check-project-format.md) projeler için nasıl yapılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="eb676-107">This article shows you how to do that for [SDK-style](../resources/check-project-format.md) projects.</span></span>

<span data-ttu-id="eb676-108">SDK stilindeki projeler için, proje dosyanızda birden çok hedef çerçeve ([TFI](/dotnet/standard/frameworks)) desteğini yapılandırabilir ve ardından `dotnet pack` `msbuild /t:pack` paketi oluşturmak için veya kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eb676-108">For SDK-style projects, you can configure support for multiple targets frameworks ([TFM](/dotnet/standard/frameworks)) in your project file, then use `dotnet pack` or `msbuild /t:pack` to create the package.</span></span>

> [!NOTE]
> <span data-ttu-id="eb676-109">nuget.exe CLı, SDK-stil projelerini paketleme, bu yüzden yalnızca veya kullanmanız gerekir `dotnet pack` `msbuild /t:pack` .</span><span class="sxs-lookup"><span data-stu-id="eb676-109">nuget.exe CLI does not support packing SDK-style projects, so you should only use `dotnet pack` or `msbuild /t:pack`.</span></span> <span data-ttu-id="eb676-110">Bunun yerine genellikle proje dosyasındaki dosyada bulunan [tüm özellikleri eklemeniz](../reference/msbuild-targets.md#pack-target) önerilir `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="eb676-110">We recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="eb676-111">SDK olmayan bir projede birden çok .NET Framework sürümünü hedeflemek için bkz. [birden çok .NET Framework sürümünü destekleme](supporting-multiple-target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="eb676-111">To target multiple .NET Framework versions in a non-SDK-style project, see [Supporting multiple .NET Framework versions](supporting-multiple-target-frameworks.md).</span></span>

## <a name="create-a-project-that-supports-multiple-net-framework-versions"></a><span data-ttu-id="eb676-112">Çoklu .NET Framework sürümlerini destekleyen bir proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="eb676-112">Create a project that supports multiple .NET Framework versions</span></span>

1. <span data-ttu-id="eb676-113">Visual Studio 'da ya da kullanarak yeni bir .NET Standard sınıf kitaplığı oluşturun `dotnet new classlib` .</span><span class="sxs-lookup"><span data-stu-id="eb676-113">Create a new .NET Standard class library either in Visual Studio or use `dotnet new classlib`.</span></span>

   <span data-ttu-id="eb676-114">En iyi uyumluluk için bir .NET Standard sınıf kitaplığı oluşturmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="eb676-114">We recommend that you create a .NET Standard class library for best compatibility.</span></span>

2. <span data-ttu-id="eb676-115">Hedef çerçeveleri desteklemek için *. csproj* dosyasını düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="eb676-115">Edit the *.csproj* file to support the target frameworks.</span></span> <span data-ttu-id="eb676-116">Örneğin, Değiştir</span><span class="sxs-lookup"><span data-stu-id="eb676-116">For example, change</span></span>
   
   `<TargetFramework>netstandard2.0</TargetFramework>`
   
   <span data-ttu-id="eb676-117">Yeni değer:</span><span class="sxs-lookup"><span data-stu-id="eb676-117">to:</span></span>
   
   `<TargetFrameworks>netstandard2.0;net45</TargetFrameworks>`

   <span data-ttu-id="eb676-118">XML öğesini tekil iken plural olarak değiştirdiğinizden emin olun ("s" öğesini hem açma hem de kapatma etiketlerine ekleyin).</span><span class="sxs-lookup"><span data-stu-id="eb676-118">Make sure that you change the XML element changed from singular to plural (add the "s" to both the open and close tags).</span></span>

3. <span data-ttu-id="eb676-119">Yalnızca bir tfd içinde çalışacak bir kodunuz varsa, `#if NET45` `#if NETSTANDARD2_0` TFE bağımlı kodu ayırmak için veya kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eb676-119">If you have any code that only works in one TFM, you can use `#if NET45` or `#if NETSTANDARD2_0` to separate TFM-dependent code.</span></span> <span data-ttu-id="eb676-120">(Daha fazla bilgi için bkz. [MultiTarget](/dotnet/core/tutorials/libraries#how-to-multitarget).) Örneğin, aşağıdaki kodu kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="eb676-120">(For more information, see [How to multitarget](/dotnet/core/tutorials/libraries#how-to-multitarget).) For example, you can use the following code:</span></span>

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

4. <span data-ttu-id="eb676-121">*. Csproj* öğesine istediğiniz NuGet meta verilerini MSBuild özellikleri olarak ekleyin.</span><span class="sxs-lookup"><span data-stu-id="eb676-121">Add any NuGet metadata you want to the *.csproj* as MSBuild properties.</span></span>

   <span data-ttu-id="eb676-122">Kullanılabilir paket meta verileri ve MSBuild özellik adlarının listesi için bkz. [Pack Target](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="eb676-122">For the list of available package metadata and the MSBuild property names, see [pack target](../reference/msbuild-targets.md#pack-target).</span></span> <span data-ttu-id="eb676-123">Ayrıca bkz. [bağımlılık varlıklarını denetleme](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="eb676-123">Also see [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

   <span data-ttu-id="eb676-124">Yapı ile ilgili özellikleri NuGet meta verilerinden ayırmak isterseniz, farklı bir `PropertyGroup` Dosya kullanabilir veya NuGet özelliklerini başka bir dosyaya yerleştirebilir ve MSBuild 'in `Import` yönergesini dahil edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eb676-124">If you want to separate build-related properties from NuGet metadata, you can use a different `PropertyGroup`, or put the NuGet properties in another file and use MSBuild's `Import` directive to include it.</span></span> <span data-ttu-id="eb676-125">`Directory.Build.Props``Directory.Build.Targets`Ayrıca, MSBuild 15,0 ' den itibaren de desteklenir.</span><span class="sxs-lookup"><span data-stu-id="eb676-125">`Directory.Build.Props` and `Directory.Build.Targets` are also supported starting with MSBuild 15.0.</span></span>

5. <span data-ttu-id="eb676-126">Şimdi, `dotnet pack` ve elde edilen *. nupkg* hedeflerini .NET Standard 2,0 ve .NET Framework 4,5 olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="eb676-126">Now, use `dotnet pack` and the resulting *.nupkg* targets both .NET Standard 2.0 and .NET Framework 4.5.</span></span>

<span data-ttu-id="eb676-127">Yukarıdaki adımlar ve 2,2 .NET Core SDK kullanılarak oluşturulan *. csproj* dosyası aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="eb676-127">Here is the *.csproj* file that is generated using the preceding steps and .NET Core SDK 2.2.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFrameworks>netstandard2.0;net45</TargetFrameworks>
    <Description>Sample project that targets multiple TFMs</Description>
  </PropertyGroup>

</Project>
```

## <a name="see-also"></a><span data-ttu-id="eb676-128">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="eb676-128">See also</span></span>

* [<span data-ttu-id="eb676-129">Hedef çerçeveleri belirtme</span><span class="sxs-lookup"><span data-stu-id="eb676-129">How to specify target frameworks</span></span>](/dotnet/standard/frameworks#how-to-specify-target-frameworks)
* [<span data-ttu-id="eb676-130">Platformlar arası hedefleme</span><span class="sxs-lookup"><span data-stu-id="eb676-130">Cross-platform targeting</span></span>](/dotnet/standard/library-guidance/cross-platform-targeting)
