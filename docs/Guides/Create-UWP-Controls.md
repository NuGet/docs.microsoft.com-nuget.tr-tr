---
title: "UWP için nasıl NuGet ile denetimleri | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/21/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "UWP içeren NuGet paketleri oluşturmak nasıl gerekli meta veriler ve Visual Studio ve harmanlama tasarımcıları için destek dosyaları dahil olmak üzere denetler."
keywords: "NuGet UWP denetimleri, Visual Studio XAML Tasarımcısı, harmanlama Tasarımcısı, özel denetimler"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3af17121f73b878decd5f0c933696fc1b0c786d7
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/02/2018
---
# <a name="creating-uwp-controls-as-nuget-packages"></a><span data-ttu-id="d4682-104">NuGet paketleri olarak UWP denetimler oluşturma</span><span class="sxs-lookup"><span data-stu-id="d4682-104">Creating UWP controls as NuGet packages</span></span>

<span data-ttu-id="d4682-105">Visual Studio 2017 ile NuGet paketlerini teslim UWP denetimleri eklenen özelliklerinin avantajından yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4682-105">With Visual Studio 2017, you can take advantage of added capabilities for UWP controls that you deliver in NuGet packages.</span></span> <span data-ttu-id="d4682-106">Bu kılavuzda kullanarak şu olanakları anlatılmaktadır [ExtensionSDKasNuGetPackage örnek](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span><span class="sxs-lookup"><span data-stu-id="d4682-106">This guide walks you through these capabilities using the [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span></span> 

## <a name="pre-requisites"></a><span data-ttu-id="d4682-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d4682-107">Pre-requisites</span></span>

1. <span data-ttu-id="d4682-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="d4682-108">Visual Studio 2017</span></span>
1. <span data-ttu-id="d4682-109">Nasıl yapılır anlayış [UWP paketleri oluşturma](create-uwp-packages.md)</span><span class="sxs-lookup"><span data-stu-id="d4682-109">Understanding of how to [Create UWP Packages](create-uwp-packages.md)</span></span>

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a><span data-ttu-id="d4682-110">XAML denetimler için araç kutusu/varlıklar bölmesinde desteği ekleme</span><span class="sxs-lookup"><span data-stu-id="d4682-110">Add toolbox/assets pane support for XAML controls</span></span>

<span data-ttu-id="d4682-111">XAML Tasarımcısı araç Visual Studio ve harmanlama varlıklar bölmesinde görünür bir XAML denetime sahip olmasını oluşturma bir `VisualStudioToolsManifest.xml` kökündeki dosyasında `tools` paket projenizin klasör.</span><span class="sxs-lookup"><span data-stu-id="d4682-111">To have a XAML control appear in the XAML designer’s toolbox in Visual Studio and the Assets pane of Blend, create a `VisualStudioToolsManifest.xml` file in the root of the `tools` folder of your package project.</span></span> <span data-ttu-id="d4682-112">Araç kutusu veya varlıklar bölmesinde görünmesi denetimi gerekmiyorsa, bu dosyayı gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="d4682-112">This file is not required if you don’t need the control to appear in the toolbox or Assets pane.</span></span>

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

<span data-ttu-id="d4682-113">Dosya yapısı aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="d4682-113">The structure of the file is as follows:</span></span>

```xml
<FileList>
  <File Reference = "your_package_file">
    <ToolboxItems VSCategory="vs_category" BlendCategory="blend_category">
      <Item Type="type_full_name_1" />

      <!-- Any number of additional Items -->
      <Item Type="type_full_name_2" />
      <Item Type="type_full_name_3" />
    </ToolboxItems>
  </File>
</FileList>
```

<span data-ttu-id="d4682-114">burada:</span><span class="sxs-lookup"><span data-stu-id="d4682-114">where:</span></span>

- <span data-ttu-id="d4682-115">*your_package_file*: denetiminizin dosya adı, gibi `ManagedPackage.winmd` ("ManagedPackage" olan bir rastgele adlı bu örnek için kullanılan ve diğer bir anlamı yoktur).</span><span class="sxs-lookup"><span data-stu-id="d4682-115">*your_package_file*: the name of your control file, such as `ManagedPackage.winmd` ("ManagedPackage" is an arbitrary named used for this example and has no other meaning).</span></span>
- <span data-ttu-id="d4682-116">*vs_category*: denetim Visual Studio tasarımcının araç kutusunda görünmelidir grubun etiketi.</span><span class="sxs-lookup"><span data-stu-id="d4682-116">*vs_category*: The label for the group in which the control should appear in the Visual Studio designer’s toolbox.</span></span> <span data-ttu-id="d4682-117">A `VSCategory` araç kutusunda görünmesi denetimi için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="d4682-117">A `VSCategory` is necessary for the control to appear in the toolbox.</span></span>
- <span data-ttu-id="d4682-118">*blend_category*: denetim karışım tasarımcının varlıklar bölmesinde görünmelidir grubun etiketi.</span><span class="sxs-lookup"><span data-stu-id="d4682-118">*blend_category*: The label for the group in which the control should appear in the Blend designer’s Assets pane.</span></span> <span data-ttu-id="d4682-119">A `BlendCategory` varlıkları görünmesi denetimi için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="d4682-119">A `BlendCategory` is necessary for the control to appear in Assets.</span></span>
- <span data-ttu-id="d4682-120">*type_full_name_n*: ad alanı gibi dahil her denetim için tam ad `ManagedPackage.MyCustomControl`.</span><span class="sxs-lookup"><span data-stu-id="d4682-120">*type_full_name_n*: The fully-qualified name for each control, including the namespace, such as `ManagedPackage.MyCustomControl`.</span></span> <span data-ttu-id="d4682-121">Nokta biçimi hem yönetilen hem de yerel türleri için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d4682-121">Note that the dot format is used for both managed and native types.</span></span>

<span data-ttu-id="d4682-122">Daha gelişmiş senaryolarda, birden çok da içerebilir `<File>` içinde öğelerin `<FileList>` zaman tek bir paket birden çok denetim derlemelerini içerir.</span><span class="sxs-lookup"><span data-stu-id="d4682-122">In more advanced scenarios, you can also include multiple `<File>` elements within `<FileList>` when a single package contains multiple control assemblies.</span></span> <span data-ttu-id="d4682-123">Ayrıca birden çok olabilir `<ToolboxItems>` tek bir düğüm `<File>` denetimlerinizi ayrı kategoriler halinde düzenlemek istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="d4682-123">You can also have multiple `<ToolboxItems>` nodes within a single `<File>` if you want to organize your controls into separate categories.</span></span>

<span data-ttu-id="d4682-124">Aşağıdaki örnekte, Denetim uygulanan `ManagedPackage.winmd` Visual Studio'da görünür ve "Yönetilen paketi" adlı bir grup Blend ve "MyCustomControl", o grupta görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d4682-124">In the following example, the control implemented in `ManagedPackage.winmd` will appear in Visual Studio and Blend in a group named “Managed Package”, and “MyCustomControl” will appear in that group.</span></span> <span data-ttu-id="d4682-125">Tüm bu rasgele adlardır.</span><span class="sxs-lookup"><span data-stu-id="d4682-125">All these names are arbitrary.</span></span>

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![Visual Studio'da bir örnek denetimi olarak görünür](media/UWP-control-vs-toolbox.png)

![Bir örnek denetimi olarak grubunda görünür](media/UWP-control-blend-assets.png)

> [!Note]
> <span data-ttu-id="d4682-128">Araç kutusu/varlıklar Bölmesi'nde görmek istediğiniz her denetim açıkça belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d4682-128">You must explicitly specify every control that you would like to see in the toolbox/assets pane.</span></span> <span data-ttu-id="d4682-129">Belirttiğiniz bunları biçiminde olun `Namespace.ControlName`.</span><span class="sxs-lookup"><span data-stu-id="d4682-129">Ensure you specify them in the format `Namespace.ControlName`.</span></span>

## <a name="add-custom-icons-to-your-controls"></a><span data-ttu-id="d4682-130">Özel simge, denetimleri ekleme</span><span class="sxs-lookup"><span data-stu-id="d4682-130">Add custom icons to your controls</span></span>

<span data-ttu-id="d4682-131">Araç kutusu/varlıklar Bölmesi'nde özel bir simge görüntülemek için görüntüyü projenizi veya karşılık gelen ekleme `design.dll` proje adında "Namespace.ControlName.extension" ve "Katıştırılmış kaynağa" yapı eylemi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="d4682-131">To display a custom icon in the toolbox/assets pane, add an image to your project or the corresponding `design.dll` project with the name “Namespace.ControlName.extension” and set the build action to “Embedded Resource”.</span></span> <span data-ttu-id="d4682-132">Desteklenen biçimler: `.png`, `.jpg`, `.jpeg`, `.gif`, ve `.bmp`.</span><span class="sxs-lookup"><span data-stu-id="d4682-132">Supported formats are `.png`, `.jpg`, `.jpeg`, `.gif`, and `.bmp`.</span></span> <span data-ttu-id="d4682-133">Önerilen görüntü boyutu 64 x 64 piksel ' dir.</span><span class="sxs-lookup"><span data-stu-id="d4682-133">The recommended image size is 64 pixels by 64 pixels.</span></span>

<span data-ttu-id="d4682-134">Aşağıdaki örnekte, proje "ManagedPackage.MyCustomControl.png" adlı bir görüntü dosyası içeriyor.</span><span class="sxs-lookup"><span data-stu-id="d4682-134">In the example below, the project contains an image file named “ManagedPackage.MyCustomControl.png”.</span></span>

![Bir proje ile özel bir simge ayarlama](media/UWP-control-custom-icon.png)

> [!Note]
> <span data-ttu-id="d4682-136">Yerel denetimler için bir kaynak olarak simge konulmalıdır `design.dll` projesi.</span><span class="sxs-lookup"><span data-stu-id="d4682-136">For native controls, you must put the icon as a resource in the `design.dll` project.</span></span>

## <a name="support-specific-windows-platform-versions"></a><span data-ttu-id="d4682-137">Belirli Windows platform sürümleri desteği</span><span class="sxs-lookup"><span data-stu-id="d4682-137">Support specific Windows platform versions</span></span>

<span data-ttu-id="d4682-138">UWP paketleri, uygulamanın yüklendiği bir işletim sistemi sürümü üst ve alt sınırları tanımlamak TargetPlatformVersion (TPV) ve TargetPlatformMinVersion (TPMinV) sahiptir.</span><span class="sxs-lookup"><span data-stu-id="d4682-138">UWP packages have a TargetPlatformVersion (TPV) and TargetPlatformMinVersion (TPMinV) that define the upper and lower bounds of the OS version where the app can be installed.</span></span> <span data-ttu-id="d4682-139">Daha fazla TPV karşı uygulama derlendiği SDK sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="d4682-139">TPV further specifies the version of the SDK against which the app is built.</span></span> <span data-ttu-id="d4682-140">Bir UWP paketi yazarken bu özellikleri oluşturduğunu unutmayın: uygulamada tanımlı platform sürümlerinin sınırları dışındaki API'lerini kullanarak neden olacak yapılandırmanın başarısız olmasına veya uygulamanın çalışma zamanında başarısız.</span><span class="sxs-lookup"><span data-stu-id="d4682-140">Be mindful of these properties when authoring a UWP package: using APIs outside the bounds of the platform versions defined in the app will cause either the build to fail or the app to fail at runtime.</span></span>

<span data-ttu-id="d4682-141">Örneğin, Windows 10 Anniversary Edition (10.0; TPMinV, denetimleri paketi için ayarladığınız düşünelim Yapı 14393), böylece paket yalnızca UWP tarafından tüketilen emin olmak istiyorsanız, bağlı alt eşleşen projeleri.</span><span class="sxs-lookup"><span data-stu-id="d4682-141">For example, let’s say you’ve set the TPMinV for you controls package to Windows 10 Anniversary Edition (10.0; Build 14393), so you want to ensure that the package is consumed only by UWP projects that match that lower bound.</span></span> <span data-ttu-id="d4682-142">UWP projeleri tarafından tüketilmesi paketinizi izin vermek için aşağıdaki klasör adları, denetimleriyle paketi gerekir:</span><span class="sxs-lookup"><span data-stu-id="d4682-142">To allow your package to be consumed by UWP projects, you must package your controls with the following folder names:</span></span>

    \lib\uap10.0\*
    \ref\uap10.0\*

<span data-ttu-id="d4682-143">Uygun TPMinV onay zorlamak için oluşturma bir [MSBuild hedefleri dosya](/visualstudio/msbuild/msbuild-targets) ve ("your_assembly_name" belirli derlemenizi adıyla değiştirerek) yapı klasörü altındaki paket:</span><span class="sxs-lookup"><span data-stu-id="d4682-143">To enforce the appropriate TPMinV check, create an [MSBuild targets file](/visualstudio/msbuild/msbuild-targets) and package it under the build folder (replacing "your_assembly_name" with the name of your specific assembly):</span></span>

    \build
      \uap10.0
        your_assembly_name.targets
    \lib
    \tools

<span data-ttu-id="d4682-144">Hedef dosyanın aşağıdaki gibi görünmelidir örneği şöyledir:</span><span class="sxs-lookup"><span data-stu-id="d4682-144">Here is an example of what the targets file should look like:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

  <Target Name="TPMinVCheck" BeforeTargets="Build;ReBuild" Condition="'$(TargetPlatformMinVersion)' != ''">
    <PropertyGroup>
      <RequiredTPMinV>10.0.14393</RequiredTPMinV>
      <ActualTPMinV>$(TargetPlatformMinVersion)</ActualTPMinV>
    </PropertyGroup>
    <Error Condition=" '$([System.Version]::Parse($(ActualTPMinV)).CompareTo($([System.Version]::Parse($(RequiredTPMinV)))))' == '-1' "        Text = "The INSERT_PACKAGE_ID_HERE nuget package cannot be used in the $(MSBuildProjectName) project since the project's TargetPlatformMinVersion - $(ActualTPMinV) does not match the Minimum Version - $(RequiredTPMinV) supported by the package" />
  </Target>
</Project>
```

## <a name="add-design-time-support"></a><span data-ttu-id="d4682-145">Tasarım zamanı desteği ekleme</span><span class="sxs-lookup"><span data-stu-id="d4682-145">Add design-time support</span></span>

<span data-ttu-id="d4682-146">Burada Özellik denetçisi'nde denetim özelliklerini göster yapılandırmak için özel donatıcıların, vb. yerleştirin ekleyin, `design.dll` içinde dosya `lib\<platform>\Design` klasörü hedef platformu için uygun olarak.</span><span class="sxs-lookup"><span data-stu-id="d4682-146">To configure where the control properties show up in the property inspector, add custom adorners, etc., place your `design.dll` file inside the `lib\<platform>\Design` folder as appropriate to the target platform.</span></span> <span data-ttu-id="d4682-147">Ayrıca, emin olmak için  **[Şablonu Düzenle > bir kopyasını düzenlemek](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)**  özelliği works içermelidir `Generic.xaml` ve içinde birleştirir tüm kaynak sözlükleri `<AssemblyName>\Themes` klasör.</span><span class="sxs-lookup"><span data-stu-id="d4682-147">Also, to ensure that the **[Edit Template > Edit a Copy](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** feature works, you must include the `Generic.xaml` and any resource dictionaries that it merges in the `<AssemblyName>\Themes` folder.</span></span> <span data-ttu-id="d4682-148">(Bu dosyayı bir denetimin çalışma zamanı davranışını etkisi yoktur.)</span><span class="sxs-lookup"><span data-stu-id="d4682-148">(This file has no impact on the runtime behavior of a control.)</span></span>

    \build
    \lib
      \uap10.0.14393.0
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml
    \tools

> [!Note]
> <span data-ttu-id="d4682-149">Varsayılan olarak, denetim özelliklerini Özellik denetçisi çeşitli kategorisinde altında gösterilir.</span><span class="sxs-lookup"><span data-stu-id="d4682-149">By default, control properties will show up under the Miscellaneous category in the property inspector.</span></span>

## <a name="use-strings-and-resources"></a><span data-ttu-id="d4682-150">Kullanım dizeler ve kaynakları</span><span class="sxs-lookup"><span data-stu-id="d4682-150">Use strings and resources</span></span>

<span data-ttu-id="d4682-151">Dize kaynakları katıştırma (`.resw`) denetiminizi veya kaybı UWP projesi tarafından kullanılan, pakette ayarlanan **yapı eylemi** özelliği `.resw` dosya **PRIResource**.</span><span class="sxs-lookup"><span data-stu-id="d4682-151">You can embed string resources (`.resw`) in your package that can be used by your control or the consuming UWP project, set the **Build Action** property of the `.resw` file to **PRIResource**.</span></span>

<span data-ttu-id="d4682-152">Bir örnek için bkz [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) ExtensionSDKasNuGetPackage örnekteki.</span><span class="sxs-lookup"><span data-stu-id="d4682-152">For an example, refer to [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) in the ExtensionSDKasNuGetPackage sample.</span></span>

## <a name="package-content-such-as-images"></a><span data-ttu-id="d4682-153">Paket içeriğini görüntüleri gibi</span><span class="sxs-lookup"><span data-stu-id="d4682-153">Package content such as images</span></span>

<span data-ttu-id="d4682-154">Denetim veya kaybı UWP projesi tarafından kullanılan görüntüleri gibi paket içeriğini.</span><span class="sxs-lookup"><span data-stu-id="d4682-154">To package content such as images that can be used by your control or the consuming UWP project.</span></span> <span data-ttu-id="d4682-155">Bu dosyaları ekleme `lib\uap10.0.14393.0` ("your_assembly_name" belirli denetiminizi yeniden de eşleşmelidir) şekilde klasörü:</span><span class="sxs-lookup"><span data-stu-id="d4682-155">add those files `lib\uap10.0.14393.0` folder as follows ("your_assembly_name" should again match your particular control):</span></span>

    \build
    \lib
      \uap10.0.14393.0
        \Design
          \your_assembly_name
    \contosoSampleImage.jpg
    \tools

<span data-ttu-id="d4682-156">Ayrıca Yaz bir[MSBuild hedefleri dosya](/visualstudio/msbuild/msbuild-targets) varlık Süren projenin çıkış klasörüne kopyalanır emin olmak için:</span><span class="sxs-lookup"><span data-stu-id="d4682-156">You may also author an[MSBuild targets file](/visualstudio/msbuild/msbuild-targets) to ensure the asset is copied to the consuming project’s output folder:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Content Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0.14393.0\contosoSampleImage.jpg">
            <CopyToOutputDirectory>Always</CopyToOutputDirectory>
        </Content>
    </ItemGroup>
</Project>
```

## <a name="see-also"></a><span data-ttu-id="d4682-157">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="d4682-157">See also</span></span>

- [<span data-ttu-id="d4682-158">UWP Paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="d4682-158">Create UWP Packages</span></span>](create-uwp-packages.md)
- [<span data-ttu-id="d4682-159">ExtensionSDKasNuGetPackage sample</span><span class="sxs-lookup"><span data-stu-id="d4682-159">ExtensionSDKasNuGetPackage sample</span></span>](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)