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
# <a name="support-multiple-net-framework-versions-in-your-project-file"></a><span data-ttu-id="ce829-103">Proje dosyanızda birden çok .NET Framework sürümü destekleme</span><span class="sxs-lookup"><span data-stu-id="ce829-103">Support multiple .NET Framework versions in your project file</span></span>

<span data-ttu-id="ce829-104">Bir projeyi ilk oluşturduğunuzda, en geniş tüketici proje yelpazesiyle uyumluluk sağladığından bir .NET Standart sınıf kitaplığı oluşturmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="ce829-104">When you first create a project, we recommend you create a .NET Standard class library, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="ce829-105">.NET Standard'ı kullanarak, varsayılan olarak bir .NET kitaplığına [çapraz platform desteği](/dotnet/standard/library-guidance/cross-platform-targeting) eklersiniz.</span><span class="sxs-lookup"><span data-stu-id="ce829-105">By using .NET Standard, you add [cross-platform support](/dotnet/standard/library-guidance/cross-platform-targeting) to a .NET library by default.</span></span> <span data-ttu-id="ce829-106">Ancak, bazı senaryolarda, belirli bir çerçeveyi hedefleyen kod eklemeniz de gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="ce829-106">However, in some scenarios, you may also need to include code that targets a particular framework.</span></span> <span data-ttu-id="ce829-107">Bu makalede, [SDK tarzı](../resources/check-project-format.md) projeler için bunu nasıl yapacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="ce829-107">This article shows you how to do that for [SDK-style](../resources/check-project-format.md) projects.</span></span>

<span data-ttu-id="ce829-108">SDK tarzı projelerde, proje dosyanızda birden çok hedef çerçevesi[(TFM)](/dotnet/standard/frameworks)için `dotnet pack` `msbuild /t:pack` destek yapılandırabilir, ardından paketi kullanabilir veya oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ce829-108">For SDK-style projects, you can configure support for multiple targets frameworks ([TFM](/dotnet/standard/frameworks)) in your project file, then use `dotnet pack` or `msbuild /t:pack` to create the package.</span></span>

> [!NOTE]
> <span data-ttu-id="ce829-109">nuget.exe CLI SDK tarzı projeleri paketleme desteklemez, `dotnet pack` bu `msbuild /t:pack`yüzden sadece kullanmalısınız veya .</span><span class="sxs-lookup"><span data-stu-id="ce829-109">nuget.exe CLI does not support packing SDK-style projects, so you should only use `dotnet pack` or `msbuild /t:pack`.</span></span> <span data-ttu-id="ce829-110">Bunun `.nuspec` yerine, genellikle dosyada bulunan tüm özellikleri proje dosyasına [eklemenizi](../reference/msbuild-targets.md#pack-target) öneririz.</span><span class="sxs-lookup"><span data-stu-id="ce829-110">We recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="ce829-111">SDK tarzı olmayan bir projede birden çok .NET Framework sürümlerini [hedeflemek](supporting-multiple-target-frameworks.md)için bkz.</span><span class="sxs-lookup"><span data-stu-id="ce829-111">To target multiple .NET Framework versions in a non-SDK-style project, see [Supporting multiple .NET Framework versions](supporting-multiple-target-frameworks.md).</span></span>

## <a name="create-a-project-that-supports-multiple-net-framework-versions"></a><span data-ttu-id="ce829-112">Birden çok .NET Framework sürümlerini destekleyen bir proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="ce829-112">Create a project that supports multiple .NET Framework versions</span></span>

1. <span data-ttu-id="ce829-113">Visual Studio'da yeni bir .NET Standart `dotnet new classlib`sınıf kitaplığı oluşturun veya kullanın.</span><span class="sxs-lookup"><span data-stu-id="ce829-113">Create a new .NET Standard class library either in Visual Studio or use `dotnet new classlib`.</span></span>

   <span data-ttu-id="ce829-114">En iyi uyumluluk için bir .NET Standart sınıf kitaplığı oluşturmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="ce829-114">We recommend that you create a .NET Standard class library for best compatibility.</span></span>

2. <span data-ttu-id="ce829-115">Hedef çerçeveleri desteklemek için *.csproj* dosyasını edin.</span><span class="sxs-lookup"><span data-stu-id="ce829-115">Edit the *.csproj* file to support the target frameworks.</span></span> <span data-ttu-id="ce829-116">Örneğin, değişiklik</span><span class="sxs-lookup"><span data-stu-id="ce829-116">For example, change</span></span>
   
   `<TargetFramework>netstandard2.0</TargetFramework>`
   
   <span data-ttu-id="ce829-117">yerine şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="ce829-117">to:</span></span>
   
   `<TargetFrameworks>netstandard2.0;net45</TargetFrameworks>`

   <span data-ttu-id="ce829-118">XML öğesini tekilden çoğul'a değiştirdiğinizden emin olun (hem açık hem de kapat etiketlere "s" ekleyin).</span><span class="sxs-lookup"><span data-stu-id="ce829-118">Make sure that you change the XML element changed from singular to plural (add the "s" to both the open and close tags).</span></span>

3. <span data-ttu-id="ce829-119">Yalnızca bir TFM'de çalışan bir kodunuz `#if NET45` varsa, TFM'ye bağlı kodu kullanabilir veya `#if NETSTANDARD2_0` ayırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ce829-119">If you have any code that only works in one TFM, you can use `#if NET45` or `#if NETSTANDARD2_0` to separate TFM-dependent code.</span></span> <span data-ttu-id="ce829-120">(Daha fazla bilgi için [bkz.](/dotnet/core/tutorials/libraries#how-to-multitarget) Örneğin, aşağıdaki kodu kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ce829-120">(For more information, see [How to multitarget](/dotnet/core/tutorials/libraries#how-to-multitarget).) For example, you can use the following code:</span></span>

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

4. <span data-ttu-id="ce829-121">MSBuild özellikleri olarak *.csproj istediğiniz* herhangi bir NuGet meta veri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ce829-121">Add any NuGet metadata you want to the *.csproj* as MSBuild properties.</span></span>

   <span data-ttu-id="ce829-122">Kullanılabilir paket meta verileri ve MSBuild özellik adları listesi için [paket hedefine](../reference/msbuild-targets.md#pack-target)bakın.</span><span class="sxs-lookup"><span data-stu-id="ce829-122">For the list of available package metadata and the MSBuild property names, see [pack target](../reference/msbuild-targets.md#pack-target).</span></span> <span data-ttu-id="ce829-123">Ayrıca [bkz.](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)</span><span class="sxs-lookup"><span data-stu-id="ce829-123">Also see [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

   <span data-ttu-id="ce829-124">Yapıyla ilgili özellikleri NuGet meta verilerinden ayırmak istiyorsanız, `PropertyGroup`farklı bir ,nuget özelliklerini başka bir dosyaya `Import` koyabilir ve MSBuild'in yönergesini bunu eklemek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ce829-124">If you want to separate build-related properties from NuGet metadata, you can use a different `PropertyGroup`, or put the NuGet properties in another file and use MSBuild's `Import` directive to include it.</span></span> <span data-ttu-id="ce829-125">`Directory.Build.Props`ve `Directory.Build.Targets` ayrıca MSBuild 15.0 ile başlayan desteklenir.</span><span class="sxs-lookup"><span data-stu-id="ce829-125">`Directory.Build.Props` and `Directory.Build.Targets` are also supported starting with MSBuild 15.0.</span></span>

5. <span data-ttu-id="ce829-126">Şimdi, `dotnet pack` kullanım ve elde edilen *.nupkg* hedefleri hem .NET Standart 2.0 ve .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="ce829-126">Now, use `dotnet pack` and the resulting *.nupkg* targets both .NET Standard 2.0 and .NET Framework 4.5.</span></span>

<span data-ttu-id="ce829-127">Aşağıda, önceki adımlar ve .NET Core SDK 2.2 kullanılarak oluşturulan *.csproj* dosyası verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ce829-127">Here is the *.csproj* file that is generated using the preceding steps and .NET Core SDK 2.2.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFrameworks>netstandard2.0;net45</TargetFrameworks>
    <Description>Sample project that targets multiple TFMs</Description>
  </PropertyGroup>

</Project>
```

## <a name="see-also"></a><span data-ttu-id="ce829-128">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="ce829-128">See also</span></span>

* [<span data-ttu-id="ce829-129">Hedef çerçeveler nasıl belirtilir?</span><span class="sxs-lookup"><span data-stu-id="ce829-129">How to specify target frameworks</span></span>](/dotnet/standard/frameworks#how-to-specify-target-frameworks)
* [<span data-ttu-id="ce829-130">Platformlar arası hedefleme</span><span class="sxs-lookup"><span data-stu-id="ce829-130">Cross-platform targeting</span></span>](/dotnet/standard/library-guidance/cross-platform-targeting)
