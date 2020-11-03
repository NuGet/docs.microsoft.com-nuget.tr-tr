---
title: NuGet ile UI denetimlerini paketleme
description: Visual Studio ve Blend tasarımcıları için gerekli meta veriler ve destekleyici dosyalar dahil olmak üzere UWP veya WPF denetimleri içeren NuGet paketleri oluşturma.
author: karann-msft
ms.author: karann
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: 17062d83349fe1b8cd28e57dd888686a226ac9cb
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238029"
---
# <a name="creating-ui-controls-as-nuget-packages"></a><span data-ttu-id="f3a66-103">NuGet paketleri olarak UI denetimleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="f3a66-103">Creating UI controls as NuGet packages</span></span>

<span data-ttu-id="f3a66-104">Visual Studio 2017 ' den itibaren, NuGet paketlerinde teslim ettiğiniz UWP ve WPF denetimleri için eklenen özelliklerden yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f3a66-104">Starting with Visual Studio 2017, you can take advantage of added capabilities for UWP and WPF controls that you deliver in NuGet packages.</span></span> <span data-ttu-id="f3a66-105">Bu kılavuzda, [Extensionsdkasnugetpackage örneği](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)kullanılarak UWP denetimleri bağlamında bu özelliklerde adım adım gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="f3a66-105">This guide walks you through these capabilities in context of UWP controls using the [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span></span> <span data-ttu-id="f3a66-106">Aksi belirtilmedikçe WPF denetimleri için de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="f3a66-106">The same applies to WPF controls unless mentioned otherwise.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f3a66-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="f3a66-107">Prerequisites</span></span>

1. <span data-ttu-id="f3a66-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="f3a66-108">Visual Studio 2017</span></span>
1. <span data-ttu-id="f3a66-109">[UWP paketleri oluşturmayı](create-uwp-packages.md) anlama</span><span class="sxs-lookup"><span data-stu-id="f3a66-109">Understanding of how to [Create UWP Packages](create-uwp-packages.md)</span></span>

## <a name="generate-library-layout"></a><span data-ttu-id="f3a66-110">Kitaplık düzeni oluştur</span><span class="sxs-lookup"><span data-stu-id="f3a66-110">Generate Library Layout</span></span>

> [!Note]
> <span data-ttu-id="f3a66-111">Bu yalnızca UWP denetimleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="f3a66-111">This is applicable only to UWP controls.</span></span>

<span data-ttu-id="f3a66-112">Özelliği ayarlamak, `GenerateLibraryLayout` proje yapı çıkışının nuspec içindeki bireysel dosya girişlerine gerek olmadan paketlenebilecek şekilde hazırlanmaya izin veren bir düzende oluşturulmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="f3a66-112">Setting the `GenerateLibraryLayout` property ensures that the project build output is generated in a layout that is ready to be packaged without the need for individual file entries in the nuspec.</span></span>

<span data-ttu-id="f3a66-113">Proje Özellikleri ' nden, derleme sekmesine gidin ve "kitaplık düzeni oluştur" onay kutusunu işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="f3a66-113">From the project properties, go to the build tab and check the "Generate Library Layout" check box.</span></span> <span data-ttu-id="f3a66-114">Bu işlem, proje dosyasını değiştirecek ve `GenerateLibraryLayout` geçerli olarak seçili derleme yapılandırması ve platformunuz için bayrağı true olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="f3a66-114">This will modify the project file and set the `GenerateLibraryLayout` flag to true for your currently selected build configuration and platform.</span></span>

<span data-ttu-id="f3a66-115">Alternatif olarak, `<GenerateLibraryLayout>true</GenerateLibraryLayout>` ilk koşulsuz özellik grubuna eklemek için proje dosyasını düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="f3a66-115">Alternately, edit the the project file to add `<GenerateLibraryLayout>true</GenerateLibraryLayout>` to the first unconditional property group.</span></span> <span data-ttu-id="f3a66-116">Bu, yapı yapılandırması ve platformundan bağımsız olarak özelliği uygular.</span><span class="sxs-lookup"><span data-stu-id="f3a66-116">This would apply the property irrespective of the build configuration and platform.</span></span>

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a><span data-ttu-id="f3a66-117">XAML denetimleri için araç kutusu/varlık bölmesi desteği ekle</span><span class="sxs-lookup"><span data-stu-id="f3a66-117">Add toolbox/assets pane support for XAML controls</span></span>

<span data-ttu-id="f3a66-118">Xaml tasarımcısının Visual Studio 'daki araç kutusunda ve Blend 'nin varlıklar bölmesinde görünmesi için, `VisualStudioToolsManifest.xml` paket projenizin klasörünün kökünde bir dosya oluşturun `tools` .</span><span class="sxs-lookup"><span data-stu-id="f3a66-118">To have a XAML control appear in the XAML designer’s toolbox in Visual Studio and the Assets pane of Blend, create a `VisualStudioToolsManifest.xml` file in the root of the `tools` folder of your package project.</span></span> <span data-ttu-id="f3a66-119">Denetimin araç kutusu veya varlıklar bölmesinde görünmesi gerekmiyorsa bu dosya gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="f3a66-119">This file is not required if you don’t need the control to appear in the toolbox or Assets pane.</span></span>

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

<span data-ttu-id="f3a66-120">Dosyanın yapısı aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="f3a66-120">The structure of the file is as follows:</span></span>

```xml
<FileList>
  <File Reference = "your_package_file">
    <ToolboxItems UIFramework="WPF" VSCategory="vs_category" BlendCategory="blend_category">
      <Item Type="type_full_name_1" />

      <!-- Any number of additional Items -->
      <Item Type="type_full_name_2" />
      <Item Type="type_full_name_3" />
    </ToolboxItems>
  </File>
</FileList>
```

<span data-ttu-id="f3a66-121">burada:</span><span class="sxs-lookup"><span data-stu-id="f3a66-121">where:</span></span>

- <span data-ttu-id="f3a66-122">*your_package_file* : `ManagedPackage.winmd` ("managedpackage" gibi) denetim dosyanızın adı bu örnek için kullanılan rastgele bir adlandırılmış addır ve başka bir anlamı yoktur).</span><span class="sxs-lookup"><span data-stu-id="f3a66-122">*your_package_file* : the name of your control file, such as `ManagedPackage.winmd` ("ManagedPackage" is an arbitrary named used for this example and has no other meaning).</span></span>
- <span data-ttu-id="f3a66-123">*vs_category* : denetimin Visual Studio Tasarımcısı araç kutusunda görünmesi gereken grubun etiketi.</span><span class="sxs-lookup"><span data-stu-id="f3a66-123">*vs_category* : The label for the group in which the control should appear in the Visual Studio designer’s toolbox.</span></span> <span data-ttu-id="f3a66-124">`VSCategory`Denetim, denetimin araç kutusunda görünmesi için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="f3a66-124">A `VSCategory` is necessary for the control to appear in the toolbox.</span></span>
<span data-ttu-id="f3a66-125">*ui_framework* : çerçeve adı (örneğin, ' WPF '), `UIFramework` denetimin araç kutusunda görünmesi için Visual Studio 16,7 Preview 3 veya üzeri sürümlerde ToolBoxItems düğümlerinde bu özniteliğin gerekli olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f3a66-125">*ui_framework* : The name of the Framework, such as 'WPF', note that `UIFramework` attribute is required on ToolboxItems nodes on Visual Studio 16.7 Preview 3 or above for the control to appear in toolbox.</span></span>
- <span data-ttu-id="f3a66-126">*blend_category* : denetimin Blend Tasarımcısı varlık bölmesinde görünmesi gereken grubun etiketi.</span><span class="sxs-lookup"><span data-stu-id="f3a66-126">*blend_category* : The label for the group in which the control should appear in the Blend designer’s Assets pane.</span></span> <span data-ttu-id="f3a66-127">, `BlendCategory` Denetimin varlıklarda görünmesi için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="f3a66-127">A `BlendCategory` is necessary for the control to appear in Assets.</span></span>
- <span data-ttu-id="f3a66-128">*type_full_name_n* : ad alanı da dahil olmak üzere her denetim için tam olarak nitelenmiş addır `ManagedPackage.MyCustomControl` .</span><span class="sxs-lookup"><span data-stu-id="f3a66-128">*type_full_name_n* : The fully-qualified name for each control, including the namespace, such as `ManagedPackage.MyCustomControl`.</span></span> <span data-ttu-id="f3a66-129">Hem yönetilen hem de yerel türler için nokta biçiminin kullanıldığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f3a66-129">Note that the dot format is used for both managed and native types.</span></span>

<span data-ttu-id="f3a66-130">Daha Gelişmiş senaryolarda, `<File>` `<FileList>` tek bir paket birden çok denetim derlemesi içerdiğinde içinde birden çok öğe de ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f3a66-130">In more advanced scenarios, you can also include multiple `<File>` elements within `<FileList>` when a single package contains multiple control assemblies.</span></span> <span data-ttu-id="f3a66-131">Ayrıca, `<ToolboxItems>` `<File>` denetimlerinizi ayrı kategoriler halinde düzenlemek istiyorsanız tek bir içinde birden fazla düğüme sahip olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f3a66-131">You can also have multiple `<ToolboxItems>` nodes within a single `<File>` if you want to organize your controls into separate categories.</span></span>

<span data-ttu-id="f3a66-132">Aşağıdaki örnekte, içinde uygulanan denetim `ManagedPackage.winmd` Visual Studio 'da görünür ve "yönetilen paket" adlı bir grupta Blend ve bu grupta "MyCustomControl" görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="f3a66-132">In the following example, the control implemented in `ManagedPackage.winmd` will appear in Visual Studio and Blend in a group named “Managed Package”, and “MyCustomControl” will appear in that group.</span></span> <span data-ttu-id="f3a66-133">Tüm bu adlar rastgele.</span><span class="sxs-lookup"><span data-stu-id="f3a66-133">All these names are arbitrary.</span></span>

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems UIFramework="WPF" VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![Visual Studio 'da göründüğü haliyle örnek bir denetim](media/UWP-control-vs-toolbox.png)

![Blend 'de göründüğü şekliyle örnek bir denetim](media/UWP-control-blend-assets.png)

> [!Note]
> <span data-ttu-id="f3a66-136">Araç kutusu/varlıklar bölmesinde görmek istediğiniz her denetimi açıkça belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f3a66-136">You must explicitly specify every control that you would like to see in the toolbox/assets pane.</span></span> <span data-ttu-id="f3a66-137">Bunları biçimde belirttiğinizden emin olun `Namespace.ControlName` .</span><span class="sxs-lookup"><span data-stu-id="f3a66-137">Ensure you specify them in the format `Namespace.ControlName`.</span></span>

## <a name="add-custom-icons-to-your-controls"></a><span data-ttu-id="f3a66-138">Denetimleriniz için özel simgeler ekleme</span><span class="sxs-lookup"><span data-stu-id="f3a66-138">Add custom icons to your controls</span></span>

<span data-ttu-id="f3a66-139">Araç kutusu/varlıklar bölmesinde özel bir simge göstermek için projenize veya `design.dll` "namespace. ControlName. Extension" adlı ilgili projeye bir resim ekleyin ve derleme eylemini "katıştırılmış kaynak" olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f3a66-139">To display a custom icon in the toolbox/assets pane, add an image to your project or the corresponding `design.dll` project with the name “Namespace.ControlName.extension” and set the build action to “Embedded Resource”.</span></span> <span data-ttu-id="f3a66-140">Ayrıca, ilişkili öğesinin `AssemblyInfo.cs` ProvideMetadata özniteliğini belirttiğinden emin olmanız gerekir `[assembly: ProvideMetadata(typeof(RegisterMetadata))]` .</span><span class="sxs-lookup"><span data-stu-id="f3a66-140">You must also ensure that the associated `AssemblyInfo.cs` specifies the ProvideMetadata attribute - `[assembly: ProvideMetadata(typeof(RegisterMetadata))]`.</span></span> <span data-ttu-id="f3a66-141">Bu [örneğe](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20)bakın.</span><span class="sxs-lookup"><span data-stu-id="f3a66-141">See this [sample](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20).</span></span>

<span data-ttu-id="f3a66-142">Desteklenen biçimler şunlardır,,, `.png` `.jpg` `.jpeg` `.gif` ve `.bmp` .</span><span class="sxs-lookup"><span data-stu-id="f3a66-142">Supported formats are `.png`, `.jpg`, `.jpeg`, `.gif`, and `.bmp`.</span></span> <span data-ttu-id="f3a66-143">Önerilen biçim 16 piksel ile 16 piksel BMP24.</span><span class="sxs-lookup"><span data-stu-id="f3a66-143">The recommended format is BMP24 in 16 pixels by 16 pixels.</span></span>

![Araç kutusu simgesi örneği](https://raw.githubusercontent.com/NuGet/docs.microsoft.com-nuget/live/docs/guides/media/ColorPicker_16x16x24.bmp)

<span data-ttu-id="f3a66-145">Pembe arka plan, çalışma zamanında değiştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="f3a66-145">The pink background is replaced at runtime.</span></span> <span data-ttu-id="f3a66-146">Visual Studio teması değiştirildiğinde ve arka plan rengi beklendiğinde simgeler yeniden renklendirilmez.</span><span class="sxs-lookup"><span data-stu-id="f3a66-146">The icons are recolored when the Visual Studio theme is changed and that background color is expected.</span></span> <span data-ttu-id="f3a66-147">Daha fazla bilgi için lütfen [Visual Studio görüntüleri ve simgelerine](/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio)başvurun.</span><span class="sxs-lookup"><span data-stu-id="f3a66-147">For more information, please reference [Images and Icons for Visual Studio](/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio).</span></span>

<span data-ttu-id="f3a66-148">Aşağıdaki örnekte, proje "ManagedPackage.MyCustomControl.png" adlı bir görüntü dosyası içerir.</span><span class="sxs-lookup"><span data-stu-id="f3a66-148">In the example below, the project contains an image file named “ManagedPackage.MyCustomControl.png”.</span></span>

![Bir projede özel bir simge ayarlama](media/UWP-control-custom-icon.png)

> [!Note]
> <span data-ttu-id="f3a66-150">Yerel denetimler için, simgeyi projeye bir kaynak olarak koymanız gerekir `design.dll` .</span><span class="sxs-lookup"><span data-stu-id="f3a66-150">For native controls, you must put the icon as a resource in the `design.dll` project.</span></span>

## <a name="support-specific-windows-platform-versions"></a><span data-ttu-id="f3a66-151">Belirli Windows platformu sürümlerini destekleme</span><span class="sxs-lookup"><span data-stu-id="f3a66-151">Support specific Windows platform versions</span></span>

<span data-ttu-id="f3a66-152">UWP paketlerinde, uygulamanın yüklenebildiği işletim sistemi sürümünün üst ve alt sınırlarını tanımlayan bir TargetPlatformVersion (TPV) ve TargetPlatformMinVersion (TPMinV) vardır.</span><span class="sxs-lookup"><span data-stu-id="f3a66-152">UWP packages have a TargetPlatformVersion (TPV) and TargetPlatformMinVersion (TPMinV) that define the upper and lower bounds of the OS version where the app can be installed.</span></span> <span data-ttu-id="f3a66-153">TPV daha fazla uygulamanın oluşturulduğu SDK sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="f3a66-153">TPV further specifies the version of the SDK against which the app is built.</span></span> <span data-ttu-id="f3a66-154">UWP paketi yazarken bu özelliklerden en az birine sahip olun: uygulamada tanımlanan platform sürümlerinin sınırları dışında API 'Lerin kullanılması, derleme başarısız olur ya da uygulamanın çalışma zamanında başarısız olmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="f3a66-154">Be mindful of these properties when authoring a UWP package: using APIs outside the bounds of the platform versions defined in the app will cause either the build to fail or the app to fail at runtime.</span></span>

<span data-ttu-id="f3a66-155">Örneğin, denetimler paketiniz için TPMinV 'i Windows 10 yıldönümü sürümüne (10,0;) ayarlayadığınızı varsayalım. Derleme 14393), bu nedenle paketin yalnızca alt sınır ile eşleşen UWP projeleri tarafından tüketildiğinden emin olmak istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="f3a66-155">For example, let’s say you’ve set the TPMinV for your controls package to Windows 10 Anniversary Edition (10.0; Build 14393), so you want to ensure that the package is consumed only by UWP projects that match that lower bound.</span></span> <span data-ttu-id="f3a66-156">Paketinizin UWP projeleri tarafından tüketilebilmesi için, denetimlerinizi aşağıdaki klasör adlarıyla paketetmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="f3a66-156">To allow your package to be consumed by UWP projects, you must package your controls with the following folder names:</span></span>

    \lib\uap10.0.14393\*
    \ref\uap10.0.14393\*

<span data-ttu-id="f3a66-157">NuGet, tüketen projenin TPMinV otomatik olarak kontrol eder ve Windows 10 yıldönümü Edition 'dan düşükse yükleme başarısız olur (10,0; Derleme 14393)</span><span class="sxs-lookup"><span data-stu-id="f3a66-157">NuGet will automatically check the TPMinV of the consuming project, and fail installation if it is lower than Windows 10 Anniversary Edition (10.0; Build 14393)</span></span>

<span data-ttu-id="f3a66-158">WPF söz konusu olduğunda, WPF denetimleri paketinizin .NET Framework v 4.6.1 veya üstünü hedefleyen projeler tarafından tüketildiğini varsayalım.</span><span class="sxs-lookup"><span data-stu-id="f3a66-158">In case of WPF, let's say you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher.</span></span> <span data-ttu-id="f3a66-159">Bunu zorlamak için, denetimlerinizi aşağıdaki klasör adlarıyla paketetmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="f3a66-159">To enforce that, you must package your controls with the following folder names:</span></span>

    \lib\net461\*
    \ref\net461\*

## <a name="add-design-time-support"></a><span data-ttu-id="f3a66-160">Tasarım zamanı desteği ekle</span><span class="sxs-lookup"><span data-stu-id="f3a66-160">Add design-time support</span></span>

<span data-ttu-id="f3a66-161">Denetim özelliklerinin, Özellik denetçisinde nerede olduğunu yapılandırmak için özel Donatıcılar ekleyin, vb., `design.dll` `lib\uap10.0.14393\Design` hedef platforma uygun şekilde dosyanızı klasöre yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="f3a66-161">To configure where the control properties show up in the property inspector, add custom adorners, etc., place your `design.dll` file inside the `lib\uap10.0.14393\Design` folder as appropriate to the target platform.</span></span> <span data-ttu-id="f3a66-162">Ayrıca, **[şablonu düzenle > kopyalama özelliğini Düzenle](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** ' nin çalıştığından emin olmak için, `Generic.xaml` `<your_assembly_name>\Themes` klasöre (gerçek derleme adınızı kullanarak) Birleşmiş olan ve tüm kaynak sözlüklerini dahil etmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f3a66-162">Also, to ensure that the **[Edit Template > Edit a Copy](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** feature works, you must include the `Generic.xaml` and any resource dictionaries that it merges in the `<your_assembly_name>\Themes` folder (again, using your actual assembly name).</span></span> <span data-ttu-id="f3a66-163">(Bu dosya, bir denetimin çalışma zamanı davranışını etkilemez.) Bu nedenle, klasör yapısı şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="f3a66-163">(This file has no impact on the runtime behavior of a control.) The folder structure would thus appear as follows:</span></span>

    \lib
      \uap10.0.14393
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml


<span data-ttu-id="f3a66-164">WPF için, WPF denetimleri paketinizin .NET Framework v 4.6.1 veya üstünü hedefleyen projeler tarafından tüketildiğini istediğiniz örneğe devam edin:</span><span class="sxs-lookup"><span data-stu-id="f3a66-164">For WPF, continuing with the example where you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher:</span></span>

    \lib
      \net461
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> <span data-ttu-id="f3a66-165">Varsayılan olarak, denetim özellikleri, Özellik denetçisindeki çeşitli Kategoriler altında görünür.</span><span class="sxs-lookup"><span data-stu-id="f3a66-165">By default, control properties will show up under the Miscellaneous category in the property inspector.</span></span>

## <a name="use-strings-and-resources"></a><span data-ttu-id="f3a66-166">Dizeleri ve kaynakları kullanma</span><span class="sxs-lookup"><span data-stu-id="f3a66-166">Use strings and resources</span></span>

<span data-ttu-id="f3a66-167">`.resw`Paketinize veya tüketen UWP projesi tarafından kullanılabilecek dize kaynaklarını (),, dosyanın **derleme eylemi** özelliğini `.resw` **priresource** olarak ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f3a66-167">You can embed string resources (`.resw`) in your package that can be used by your control or the consuming UWP project, set the **Build Action** property of the `.resw` file to **PRIResource** .</span></span>

<span data-ttu-id="f3a66-168">Bir örnek için, ExtensionSDKasNuGetPackage örneğindeki [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) adresine bakın.</span><span class="sxs-lookup"><span data-stu-id="f3a66-168">For an example, refer to [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) in the ExtensionSDKasNuGetPackage sample.</span></span>

> [!Note]
> <span data-ttu-id="f3a66-169">Bu yalnızca UWP denetimleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="f3a66-169">This is applicable only to UWP controls.</span></span>

## <a name="see-also"></a><span data-ttu-id="f3a66-170">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="f3a66-170">See also</span></span>

- [<span data-ttu-id="f3a66-171">UWP paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="f3a66-171">Create UWP Packages</span></span>](create-uwp-packages.md)
- [<span data-ttu-id="f3a66-172">ExtensionSDKasNuGetPackage örneği</span><span class="sxs-lookup"><span data-stu-id="f3a66-172">ExtensionSDKasNuGetPackage sample</span></span>](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)