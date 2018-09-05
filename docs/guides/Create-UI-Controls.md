---
title: NuGet ile paket kullanıcı Arabirimi denetimleri hakkında
description: UWP ya da WPF içeren NuGet paketleri oluşturmak nasıl destek dosyaları Visual Studio'da ve Blend'de tasarımcılarına ve gerekli meta veriler dahil olmak üzere denetler.
author: karann-msft
ms.author: karann
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: ce5ad07209a06010150b14092aa1b15ee6f84146
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548744"
---
# <a name="creating-ui-controls-as-nuget-packages"></a><span data-ttu-id="03c74-103">NuGet paketleri olarak kullanıcı Arabirimi denetimleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="03c74-103">Creating UI controls as NuGet packages</span></span>

<span data-ttu-id="03c74-104">Visual Studio 2017 ile NuGet paketlerinde teslim UWP ve WPF denetimleri için eklenen özelliklerin yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="03c74-104">With Visual Studio 2017, you can take advantage of added capabilities for UWP and WPF controls that you deliver in NuGet packages.</span></span> <span data-ttu-id="03c74-105">Bu kılavuzu kullanarak UWP denetimleri bağlamında bu özellikler size [ExtensionSDKasNuGetPackage örnek](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span><span class="sxs-lookup"><span data-stu-id="03c74-105">This guide walks you through these capabilities in context of UWP controls using the [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span></span> <span data-ttu-id="03c74-106">Aksi belirtilmediği sürece aynı WPF denetimleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="03c74-106">The same applies to WPF controls unless mentioned otherwise.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="03c74-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="03c74-107">Prerequisites</span></span>

1. <span data-ttu-id="03c74-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="03c74-108">Visual Studio 2017</span></span>
1. <span data-ttu-id="03c74-109">Olma [UWP paketleri oluşturma](create-uwp-packages.md)</span><span class="sxs-lookup"><span data-stu-id="03c74-109">Understanding of how to [Create UWP Packages](create-uwp-packages.md)</span></span>

## <a name="generate-library-layout"></a><span data-ttu-id="03c74-110">Kitaplık düzeni oluştur</span><span class="sxs-lookup"><span data-stu-id="03c74-110">Generate Library Layout</span></span>

> [!Note]
> <span data-ttu-id="03c74-111">Bu, yalnızca UWP denetimleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="03c74-111">This is applicable only to UWP controls.</span></span>

<span data-ttu-id="03c74-112">Ayarı `GenerateLibraryLayout` özelliği sağlar projesi yapı çıkış nuspec tek tek dosya girişleri gerek kalmadan paketlenmesi hazır bir düzende oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="03c74-112">Setting the `GenerateLibraryLayout` property ensures that the project build output is generated in a layout that is ready to be packaged without the need for individual file entries in the nuspec.</span></span>

<span data-ttu-id="03c74-113">Proje Özellikleri derleme sekmesine gidin ve "Kitaplık düzeni oluştur" onay kutusunu işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="03c74-113">From the project properties, go to the build tab and check the "Generate Library Layout" check box.</span></span> <span data-ttu-id="03c74-114">Bu proje dosyasını değiştirmek ve ayarlama `GenerateLibraryLayout` bayrağı şu anda seçilen derleme yapılandırması ve platformu için true.</span><span class="sxs-lookup"><span data-stu-id="03c74-114">This will modify the project file and set the `GenerateLibraryLayout` flag to true for your currently selected build configuration and platform.</span></span>

<span data-ttu-id="03c74-115">Alternatif olarak, Düzen eklemek için proje dosyasını `<GenerateLibraryLayout>true</GenerateLibraryLayout>` ilk koşulsuz özellik grubuna.</span><span class="sxs-lookup"><span data-stu-id="03c74-115">Alternately, edit the the project file to add `<GenerateLibraryLayout>true</GenerateLibraryLayout>` to the first unconditional property group.</span></span> <span data-ttu-id="03c74-116">Bu özellik derleme yapılandırması ve platform fark etmeksizin geçerli.</span><span class="sxs-lookup"><span data-stu-id="03c74-116">This would apply the property irrespective of the build configuration and platform.</span></span>

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a><span data-ttu-id="03c74-117">XAML denetimleri için araç kutusu/varlıklar bölmesinde desteği ekleme</span><span class="sxs-lookup"><span data-stu-id="03c74-117">Add toolbox/assets pane support for XAML controls</span></span>

<span data-ttu-id="03c74-118">Visual Studio ve varlıklar bölmesinde Blend, XAML Tasarımcısı araç çubuğunda görünen bir XAML denetimi sağlamak için oluşturun bir `VisualStudioToolsManifest.xml` köküne dosya `tools` paket projenizin klasör.</span><span class="sxs-lookup"><span data-stu-id="03c74-118">To have a XAML control appear in the XAML designer’s toolbox in Visual Studio and the Assets pane of Blend, create a `VisualStudioToolsManifest.xml` file in the root of the `tools` folder of your package project.</span></span> <span data-ttu-id="03c74-119">Araç kutusu veya varlıklar bölmesinde görüntülenmesinin denetimini gerekmiyorsa, bu dosya gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="03c74-119">This file is not required if you don’t need the control to appear in the toolbox or Assets pane.</span></span>

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

<span data-ttu-id="03c74-120">Dosya yapısı aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="03c74-120">The structure of the file is as follows:</span></span>

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

<span data-ttu-id="03c74-121">burada:</span><span class="sxs-lookup"><span data-stu-id="03c74-121">where:</span></span>

- <span data-ttu-id="03c74-122">*your_package_file*: gibi bir denetimin adını dosya `ManagedPackage.winmd` ("ManagedPackage" olan bir rastgele adlı bu örnek için kullanılan ve diğer bir anlamı yoktur).</span><span class="sxs-lookup"><span data-stu-id="03c74-122">*your_package_file*: the name of your control file, such as `ManagedPackage.winmd` ("ManagedPackage" is an arbitrary named used for this example and has no other meaning).</span></span>
- <span data-ttu-id="03c74-123">*vs_category*: denetimin Visual Studio Tasarımcısı araç kutusunda görünmelidir grubun etiketi.</span><span class="sxs-lookup"><span data-stu-id="03c74-123">*vs_category*: The label for the group in which the control should appear in the Visual Studio designer’s toolbox.</span></span> <span data-ttu-id="03c74-124">A `VSCategory` denetimi araç kutusunda görünmesi için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="03c74-124">A `VSCategory` is necessary for the control to appear in the toolbox.</span></span>
- <span data-ttu-id="03c74-125">*blend_category*: denetimin Blend tasarımcının varlıklar bölmesinde görünmelidir grubun etiketi.</span><span class="sxs-lookup"><span data-stu-id="03c74-125">*blend_category*: The label for the group in which the control should appear in the Blend designer’s Assets pane.</span></span> <span data-ttu-id="03c74-126">A `BlendCategory` varlıkları görüntülenmesini denetim için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="03c74-126">A `BlendCategory` is necessary for the control to appear in Assets.</span></span>
- <span data-ttu-id="03c74-127">*type_full_name_n*: tam adı ad alanı, aşağıdaki gibi her denetim için `ManagedPackage.MyCustomControl`.</span><span class="sxs-lookup"><span data-stu-id="03c74-127">*type_full_name_n*: The fully-qualified name for each control, including the namespace, such as `ManagedPackage.MyCustomControl`.</span></span> <span data-ttu-id="03c74-128">Nokta biçimi hem yönetilen hem de yerel türleri için kullanıldığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="03c74-128">Note that the dot format is used for both managed and native types.</span></span>

<span data-ttu-id="03c74-129">Daha gelişmiş senaryolarda, birden çok de içerebilir `<File>` öğeleri içinde `<FileList>` tek bir paket birden çok denetim derleme içerdiğinde.</span><span class="sxs-lookup"><span data-stu-id="03c74-129">In more advanced scenarios, you can also include multiple `<File>` elements within `<FileList>` when a single package contains multiple control assemblies.</span></span> <span data-ttu-id="03c74-130">Birden çok bulundurabilirsiniz `<ToolboxItems>` tek bir düğüm `<File>` denetimlerinizi ayrı kategoriler halinde düzenlemek istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="03c74-130">You can also have multiple `<ToolboxItems>` nodes within a single `<File>` if you want to organize your controls into separate categories.</span></span>

<span data-ttu-id="03c74-131">Aşağıdaki örnekte, denetime uygulanan `ManagedPackage.winmd` Visual Studio'da görünür ve "Yönetilen paket" adlı bir grupta Blend ve "MyCustomControl", o grupta görünür.</span><span class="sxs-lookup"><span data-stu-id="03c74-131">In the following example, the control implemented in `ManagedPackage.winmd` will appear in Visual Studio and Blend in a group named “Managed Package”, and “MyCustomControl” will appear in that group.</span></span> <span data-ttu-id="03c74-132">Bu adların hepsinin rastgele.</span><span class="sxs-lookup"><span data-stu-id="03c74-132">All these names are arbitrary.</span></span>

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

![Blend'de bir örnek denetimi olarak görünür](media/UWP-control-blend-assets.png)

> [!Note]
> <span data-ttu-id="03c74-135">Araç kutusu/varlıklar bölmesinde görmek istediğiniz her denetim açıkça belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="03c74-135">You must explicitly specify every control that you would like to see in the toolbox/assets pane.</span></span> <span data-ttu-id="03c74-136">Belirttiğiniz bunları biçiminde olun `Namespace.ControlName`.</span><span class="sxs-lookup"><span data-stu-id="03c74-136">Ensure you specify them in the format `Namespace.ControlName`.</span></span>

## <a name="add-custom-icons-to-your-controls"></a><span data-ttu-id="03c74-137">Özel simgeleri denetimlerinizi ekleyin</span><span class="sxs-lookup"><span data-stu-id="03c74-137">Add custom icons to your controls</span></span>

<span data-ttu-id="03c74-138">Araç kutusu/varlıklar Bölmesi'nde özel bir simge görüntülemek için bir görüntü projenizi veya ilgili ekleme `design.dll` proje adıyla "Namespace.ControlName.extension" ve "Gömülü kaynak" derleme eylemi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="03c74-138">To display a custom icon in the toolbox/assets pane, add an image to your project or the corresponding `design.dll` project with the name “Namespace.ControlName.extension” and set the build action to “Embedded Resource”.</span></span> <span data-ttu-id="03c74-139">Desteklenen biçimler `.png`, `.jpg`, `.jpeg`, `.gif`, ve `.bmp`.</span><span class="sxs-lookup"><span data-stu-id="03c74-139">Supported formats are `.png`, `.jpg`, `.jpeg`, `.gif`, and `.bmp`.</span></span> <span data-ttu-id="03c74-140">Önerilen görüntü boyutu 64 x 64 piksel ' dir.</span><span class="sxs-lookup"><span data-stu-id="03c74-140">The recommended image size is 64 pixels by 64 pixels.</span></span>

<span data-ttu-id="03c74-141">Aşağıdaki örnekte, "ManagedPackage.MyCustomControl.png" adlı bir görüntü dosyasının proje içerir.</span><span class="sxs-lookup"><span data-stu-id="03c74-141">In the example below, the project contains an image file named “ManagedPackage.MyCustomControl.png”.</span></span>

![Bir projeye özel bir simge ayarlama](media/UWP-control-custom-icon.png)

> [!Note]
> <span data-ttu-id="03c74-143">Yerel denetimler için bir kaynak olarak simgesi yerleştirmelidir `design.dll` proje.</span><span class="sxs-lookup"><span data-stu-id="03c74-143">For native controls, you must put the icon as a resource in the `design.dll` project.</span></span>

## <a name="support-specific-windows-platform-versions"></a><span data-ttu-id="03c74-144">Belirli Windows platform sürümleri desteği</span><span class="sxs-lookup"><span data-stu-id="03c74-144">Support specific Windows platform versions</span></span>

<span data-ttu-id="03c74-145">UWP paketleri, uygulamanın yüklendiği bir işletim sistemi sürümünün alt ve üst sınırlarını tanımlayın TargetPlatformVersion (TPV) ve targetplatformminversion'ından (TPMinV) sahip.</span><span class="sxs-lookup"><span data-stu-id="03c74-145">UWP packages have a TargetPlatformVersion (TPV) and TargetPlatformMinVersion (TPMinV) that define the upper and lower bounds of the OS version where the app can be installed.</span></span> <span data-ttu-id="03c74-146">Daha fazla TPV karşı yerleşik uygulama SDK'sı sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="03c74-146">TPV further specifies the version of the SDK against which the app is built.</span></span> <span data-ttu-id="03c74-147">Bir UWP paket yazarken bu özellikleri dikkatli olmanızı: uygulamada tanımlanan platform sürümleri sınırları dışında API'lerini kullanarak neden olacak başarısız için yapı ya da uygulama çalışma zamanında başarısız.</span><span class="sxs-lookup"><span data-stu-id="03c74-147">Be mindful of these properties when authoring a UWP package: using APIs outside the bounds of the platform versions defined in the app will cause either the build to fail or the app to fail at runtime.</span></span>

<span data-ttu-id="03c74-148">Örneğin, Windows 10 Anniversary Edition (10.0; denetimleri paketinize için TPMinV ayarladığınızdan varsayalım Derleme 14393), paket yalnızca UWP tarafından tüketilmesi sağlamak istediğiniz şekilde karşılayan bağlı alt projeleri.</span><span class="sxs-lookup"><span data-stu-id="03c74-148">For example, let’s say you’ve set the TPMinV for your controls package to Windows 10 Anniversary Edition (10.0; Build 14393), so you want to ensure that the package is consumed only by UWP projects that match that lower bound.</span></span> <span data-ttu-id="03c74-149">UWP projeleri tarafından kullanılacak paketinizi izin vermek için aşağıdaki klasör adları, denetimleriyle paketi gerekir:</span><span class="sxs-lookup"><span data-stu-id="03c74-149">To allow your package to be consumed by UWP projects, you must package your controls with the following folder names:</span></span>

    \lib\uap10.0.14393\*
    \ref\uap10.0.14393\*

<span data-ttu-id="03c74-150">NuGet otomatik olarak kullanan projenin TPMinV denetleyin ve Windows 10 Anniversary Edition (10.0; düşükse, yükleme başarısız Derleme 14393)</span><span class="sxs-lookup"><span data-stu-id="03c74-150">NuGet will automatically check the TPMinV of the consuming project, and fail installation if it is lower than Windows 10 Anniversary Edition (10.0; Build 14393)</span></span>

<span data-ttu-id="03c74-151">WPF olması durumunda, WPF denetimleri paketinizi v4.6.1 .NET Framework'ü hedefleyen projeleri tarafından tüketilen veya daha yüksek olmasını istediğiniz varsayalım.</span><span class="sxs-lookup"><span data-stu-id="03c74-151">In case of WPF, let's say you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher.</span></span> <span data-ttu-id="03c74-152">Zorlamak için aşağıdaki klasör adları, denetimleriyle paketi gerekir:</span><span class="sxs-lookup"><span data-stu-id="03c74-152">To enforce that, you must package your controls with the following folder names:</span></span>

    \lib\net461\*
    \ref\net461\*

## <a name="add-design-time-support"></a><span data-ttu-id="03c74-153">Tasarım zamanı desteği eklendi</span><span class="sxs-lookup"><span data-stu-id="03c74-153">Add design-time support</span></span>

<span data-ttu-id="03c74-154">Burada özelliği denetçi'deki denetim özelliklerini göster yapılandırmak için özel donatıcıları, vs. yerleştirin ekleyin, `design.dll` içinde dosya `lib\uap10.0.14393\Design` klasörü olarak hedef platform için uygun.</span><span class="sxs-lookup"><span data-stu-id="03c74-154">To configure where the control properties show up in the property inspector, add custom adorners, etc., place your `design.dll` file inside the `lib\uap10.0.14393\Design` folder as appropriate to the target platform.</span></span> <span data-ttu-id="03c74-155">Ayrıca, emin olmak için **[Şablonu Düzenle > Kopya Düzenle](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** özellik works içermelidir `Generic.xaml` ve içinde birleştirir herhangi bir kaynak sözlükleri `<your_assembly_name>\Themes` klasörü (yeniden kullanma Gerçek derleme adı).</span><span class="sxs-lookup"><span data-stu-id="03c74-155">Also, to ensure that the **[Edit Template > Edit a Copy](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** feature works, you must include the `Generic.xaml` and any resource dictionaries that it merges in the `<your_assembly_name>\Themes` folder (again, using your actual assembly name).</span></span> <span data-ttu-id="03c74-156">(Bu dosya, bir denetimin çalışma zamanı davranışı üzerinde herhangi bir etkisi yoktur.) Bu nedenle, klasör yapısı aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="03c74-156">(This file has no impact on the runtime behavior of a control.) The folder structure would thus appear as follows:</span></span>

    \lib
      \uap10.0.14393
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml


<span data-ttu-id="03c74-157">Paket, .NET Framework v4.6.1 hedefleyen projeleri tarafından tüketilen veya daha yüksek olmasını denetimleri, WPF istediğiniz örneğiyle devam WPF için:</span><span class="sxs-lookup"><span data-stu-id="03c74-157">For WPF, continuing with the example where you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher:</span></span>

    \lib
      \net461
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> <span data-ttu-id="03c74-158">Varsayılan olarak, denetim özelliklerini Özellik denetçisi çeşitli kategorisi altında görünür.</span><span class="sxs-lookup"><span data-stu-id="03c74-158">By default, control properties will show up under the Miscellaneous category in the property inspector.</span></span>

## <a name="use-strings-and-resources"></a><span data-ttu-id="03c74-159">Kullanım dizeleri ve kaynakları</span><span class="sxs-lookup"><span data-stu-id="03c74-159">Use strings and resources</span></span>

<span data-ttu-id="03c74-160">Dize kaynakları ekleyebilir (`.resw`) denetiminiz veya alıcı UWP projesi tarafından kullanılan, pakette ayarlanan **derleme eylemi** özelliği `.resw` dosyasını **PRIResource**.</span><span class="sxs-lookup"><span data-stu-id="03c74-160">You can embed string resources (`.resw`) in your package that can be used by your control or the consuming UWP project, set the **Build Action** property of the `.resw` file to **PRIResource**.</span></span>

<span data-ttu-id="03c74-161">Örneğin, başvurmak [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) ExtensionSDKasNuGetPackage örnekteki.</span><span class="sxs-lookup"><span data-stu-id="03c74-161">For an example, refer to [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) in the ExtensionSDKasNuGetPackage sample.</span></span>

> [!Note]
> <span data-ttu-id="03c74-162">Bu, yalnızca UWP denetimleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="03c74-162">This is applicable only to UWP controls.</span></span>

## <a name="see-also"></a><span data-ttu-id="03c74-163">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="03c74-163">See also</span></span>

- [<span data-ttu-id="03c74-164">UWP Paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="03c74-164">Create UWP Packages</span></span>](create-uwp-packages.md)
- [<span data-ttu-id="03c74-165">ExtensionSDKasNuGetPackage örnek</span><span class="sxs-lookup"><span data-stu-id="03c74-165">ExtensionSDKasNuGetPackage sample</span></span>](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
