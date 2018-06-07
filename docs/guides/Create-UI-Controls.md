---
title: NuGet paketi UI denetimleriyle nasıl
description: UWP ya da WPF içeren NuGet paketleri oluşturmak nasıl destek dosyaları için Visual Studio ve harmanlama tasarımcıları ve gerekli meta veriler dahil olmak üzere denetler.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: ab7499c415f63319fd314f33607f74d400b5f957
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818664"
---
# <a name="creating-ui-controls-as-nuget-packages"></a><span data-ttu-id="c2a50-103">NuGet paketleri UI denetimleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="c2a50-103">Creating UI controls as NuGet packages</span></span>

<span data-ttu-id="c2a50-104">Visual Studio 2017 ile NuGet paketlerini teslim UWP ve WPF denetimleri eklenen özelliklerinin avantajından yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c2a50-104">With Visual Studio 2017, you can take advantage of added capabilities for UWP and WPF controls that you deliver in NuGet packages.</span></span> <span data-ttu-id="c2a50-105">Bu kılavuzda, bu özellikleri kullanarak UWP denetimleri bağlamında anlatılmaktadır [ExtensionSDKasNuGetPackage örnek](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span><span class="sxs-lookup"><span data-stu-id="c2a50-105">This guide walks you through these capabilities in context of UWP controls using the [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span></span> <span data-ttu-id="c2a50-106">Aksi belirtilmediği sürece aynı WPF denetimleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="c2a50-106">The same applies to WPF controls unless mentioned otherwise.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c2a50-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="c2a50-107">Prerequisites</span></span>

1. <span data-ttu-id="c2a50-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="c2a50-108">Visual Studio 2017</span></span>
1. <span data-ttu-id="c2a50-109">Nasıl yapılır anlayış [UWP paketleri oluşturma](create-uwp-packages.md)</span><span class="sxs-lookup"><span data-stu-id="c2a50-109">Understanding of how to [Create UWP Packages](create-uwp-packages.md)</span></span>

## <a name="generate-library-layout"></a><span data-ttu-id="c2a50-110">Kitaplık düzenine oluştur</span><span class="sxs-lookup"><span data-stu-id="c2a50-110">Generate Library Layout</span></span>

> [!Note]
> <span data-ttu-id="c2a50-111">Bu, yalnızca UWP denetimleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="c2a50-111">This is applicable only to UWP controls.</span></span>

<span data-ttu-id="c2a50-112">Ayar `GenerateLibraryLayout` özelliği sağlar proje derleme çıktısı nuspec tek tek dosya girişlerinde gerek kalmadan paketlenmesi hazır bir düzende oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c2a50-112">Setting the `GenerateLibraryLayout` property ensures that the project build output is generated in a layout that is ready to be packaged without the need for individual file entries in the nuspec.</span></span>

<span data-ttu-id="c2a50-113">Proje Özellikleri yapı sekmesine gidin ve "Kitaplığı düzeni oluştur" onay kutusunu işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="c2a50-113">From the project properties, go to the build tab and check the "Generate Library Layout" check box.</span></span> <span data-ttu-id="c2a50-114">Bu proje dosyasını değiştirmek ve ayarlama `GenerateLibraryLayout` bayrağı şu anda seçili yapı yapılandırması ve platformu için true.</span><span class="sxs-lookup"><span data-stu-id="c2a50-114">This will modify the project file and set the `GenerateLibraryLayout` flag to true for your currently selected build configuration and platform.</span></span>

<span data-ttu-id="c2a50-115">Alternatif olarak, düzenleme eklemek için proje dosyası `<GenerateLibraryLayout>true</GenerateLibraryLayout>` ilk koşulsuz özelliği gruba.</span><span class="sxs-lookup"><span data-stu-id="c2a50-115">Alternately, edit the the project file to add `<GenerateLibraryLayout>true</GenerateLibraryLayout>` to the first unconditional property group.</span></span> <span data-ttu-id="c2a50-116">Bu özellik yapı yapılandırması ve platformu yedeklemiş geçerli.</span><span class="sxs-lookup"><span data-stu-id="c2a50-116">This would apply the property irrespective of the build configuration and platform.</span></span>

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a><span data-ttu-id="c2a50-117">XAML denetimler için araç kutusu/varlıklar bölmesinde desteği ekleme</span><span class="sxs-lookup"><span data-stu-id="c2a50-117">Add toolbox/assets pane support for XAML controls</span></span>

<span data-ttu-id="c2a50-118">XAML Tasarımcısı araç Visual Studio ve harmanlama varlıklar bölmesinde görünür bir XAML denetime sahip olmasını oluşturma bir `VisualStudioToolsManifest.xml` kökündeki dosyasında `tools` paket projenizin klasör.</span><span class="sxs-lookup"><span data-stu-id="c2a50-118">To have a XAML control appear in the XAML designer’s toolbox in Visual Studio and the Assets pane of Blend, create a `VisualStudioToolsManifest.xml` file in the root of the `tools` folder of your package project.</span></span> <span data-ttu-id="c2a50-119">Araç kutusu veya varlıklar bölmesinde görünmesi denetimi gerekmiyorsa, bu dosyayı gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="c2a50-119">This file is not required if you don’t need the control to appear in the toolbox or Assets pane.</span></span>

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

<span data-ttu-id="c2a50-120">Dosya yapısı aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="c2a50-120">The structure of the file is as follows:</span></span>

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

<span data-ttu-id="c2a50-121">burada:</span><span class="sxs-lookup"><span data-stu-id="c2a50-121">where:</span></span>

- <span data-ttu-id="c2a50-122">*your_package_file*: denetiminizin dosya adı, gibi `ManagedPackage.winmd` ("ManagedPackage" olan bir rastgele adlı bu örnek için kullanılan ve diğer bir anlamı yoktur).</span><span class="sxs-lookup"><span data-stu-id="c2a50-122">*your_package_file*: the name of your control file, such as `ManagedPackage.winmd` ("ManagedPackage" is an arbitrary named used for this example and has no other meaning).</span></span>
- <span data-ttu-id="c2a50-123">*vs_category*: denetim Visual Studio tasarımcının araç kutusunda görünmelidir grubun etiketi.</span><span class="sxs-lookup"><span data-stu-id="c2a50-123">*vs_category*: The label for the group in which the control should appear in the Visual Studio designer’s toolbox.</span></span> <span data-ttu-id="c2a50-124">A `VSCategory` araç kutusunda görünmesi denetimi için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="c2a50-124">A `VSCategory` is necessary for the control to appear in the toolbox.</span></span>
- <span data-ttu-id="c2a50-125">*blend_category*: denetim karışım tasarımcının varlıklar bölmesinde görünmelidir grubun etiketi.</span><span class="sxs-lookup"><span data-stu-id="c2a50-125">*blend_category*: The label for the group in which the control should appear in the Blend designer’s Assets pane.</span></span> <span data-ttu-id="c2a50-126">A `BlendCategory` varlıkları görünmesi denetimi için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="c2a50-126">A `BlendCategory` is necessary for the control to appear in Assets.</span></span>
- <span data-ttu-id="c2a50-127">*type_full_name_n*: ad alanı gibi dahil her denetim için tam ad `ManagedPackage.MyCustomControl`.</span><span class="sxs-lookup"><span data-stu-id="c2a50-127">*type_full_name_n*: The fully-qualified name for each control, including the namespace, such as `ManagedPackage.MyCustomControl`.</span></span> <span data-ttu-id="c2a50-128">Nokta biçimi hem yönetilen hem de yerel türleri için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c2a50-128">Note that the dot format is used for both managed and native types.</span></span>

<span data-ttu-id="c2a50-129">Daha gelişmiş senaryolarda, birden çok da içerebilir `<File>` içinde öğelerin `<FileList>` zaman tek bir paket birden çok denetim derlemelerini içerir.</span><span class="sxs-lookup"><span data-stu-id="c2a50-129">In more advanced scenarios, you can also include multiple `<File>` elements within `<FileList>` when a single package contains multiple control assemblies.</span></span> <span data-ttu-id="c2a50-130">Ayrıca birden çok olabilir `<ToolboxItems>` tek bir düğüm `<File>` denetimlerinizi ayrı kategoriler halinde düzenlemek istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="c2a50-130">You can also have multiple `<ToolboxItems>` nodes within a single `<File>` if you want to organize your controls into separate categories.</span></span>

<span data-ttu-id="c2a50-131">Aşağıdaki örnekte, Denetim uygulanan `ManagedPackage.winmd` Visual Studio'da görünür ve "Yönetilen paketi" adlı bir grup Blend ve "MyCustomControl", o grupta görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="c2a50-131">In the following example, the control implemented in `ManagedPackage.winmd` will appear in Visual Studio and Blend in a group named “Managed Package”, and “MyCustomControl” will appear in that group.</span></span> <span data-ttu-id="c2a50-132">Tüm bu rasgele adlardır.</span><span class="sxs-lookup"><span data-stu-id="c2a50-132">All these names are arbitrary.</span></span>

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
> <span data-ttu-id="c2a50-135">Araç kutusu/varlıklar Bölmesi'nde görmek istediğiniz her denetim açıkça belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c2a50-135">You must explicitly specify every control that you would like to see in the toolbox/assets pane.</span></span> <span data-ttu-id="c2a50-136">Belirttiğiniz bunları biçiminde olun `Namespace.ControlName`.</span><span class="sxs-lookup"><span data-stu-id="c2a50-136">Ensure you specify them in the format `Namespace.ControlName`.</span></span>

## <a name="add-custom-icons-to-your-controls"></a><span data-ttu-id="c2a50-137">Özel simge, denetimleri ekleme</span><span class="sxs-lookup"><span data-stu-id="c2a50-137">Add custom icons to your controls</span></span>

<span data-ttu-id="c2a50-138">Araç kutusu/varlıklar Bölmesi'nde özel bir simge görüntülemek için görüntüyü projenizi veya karşılık gelen ekleme `design.dll` proje adında "Namespace.ControlName.extension" ve "Katıştırılmış kaynağa" yapı eylemi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="c2a50-138">To display a custom icon in the toolbox/assets pane, add an image to your project or the corresponding `design.dll` project with the name “Namespace.ControlName.extension” and set the build action to “Embedded Resource”.</span></span> <span data-ttu-id="c2a50-139">Desteklenen biçimler: `.png`, `.jpg`, `.jpeg`, `.gif`, ve `.bmp`.</span><span class="sxs-lookup"><span data-stu-id="c2a50-139">Supported formats are `.png`, `.jpg`, `.jpeg`, `.gif`, and `.bmp`.</span></span> <span data-ttu-id="c2a50-140">Önerilen görüntü boyutu 64 x 64 piksel ' dir.</span><span class="sxs-lookup"><span data-stu-id="c2a50-140">The recommended image size is 64 pixels by 64 pixels.</span></span>

<span data-ttu-id="c2a50-141">Aşağıdaki örnekte, proje "ManagedPackage.MyCustomControl.png" adlı bir görüntü dosyası içeriyor.</span><span class="sxs-lookup"><span data-stu-id="c2a50-141">In the example below, the project contains an image file named “ManagedPackage.MyCustomControl.png”.</span></span>

![Bir proje ile özel bir simge ayarlama](media/UWP-control-custom-icon.png)

> [!Note]
> <span data-ttu-id="c2a50-143">Yerel denetimler için bir kaynak olarak simge konulmalıdır `design.dll` projesi.</span><span class="sxs-lookup"><span data-stu-id="c2a50-143">For native controls, you must put the icon as a resource in the `design.dll` project.</span></span>

## <a name="support-specific-windows-platform-versions"></a><span data-ttu-id="c2a50-144">Belirli Windows platform sürümleri desteği</span><span class="sxs-lookup"><span data-stu-id="c2a50-144">Support specific Windows platform versions</span></span>

<span data-ttu-id="c2a50-145">UWP paketleri, uygulamanın yüklendiği bir işletim sistemi sürümü üst ve alt sınırları tanımlamak TargetPlatformVersion (TPV) ve TargetPlatformMinVersion (TPMinV) sahiptir.</span><span class="sxs-lookup"><span data-stu-id="c2a50-145">UWP packages have a TargetPlatformVersion (TPV) and TargetPlatformMinVersion (TPMinV) that define the upper and lower bounds of the OS version where the app can be installed.</span></span> <span data-ttu-id="c2a50-146">Daha fazla TPV karşı uygulama derlendiği SDK sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="c2a50-146">TPV further specifies the version of the SDK against which the app is built.</span></span> <span data-ttu-id="c2a50-147">Bir UWP paketi yazarken bu özellikleri oluşturduğunu unutmayın: uygulamada tanımlı platform sürümlerinin sınırları dışındaki API'lerini kullanarak neden olacak yapılandırmanın başarısız olmasına veya uygulamanın çalışma zamanında başarısız.</span><span class="sxs-lookup"><span data-stu-id="c2a50-147">Be mindful of these properties when authoring a UWP package: using APIs outside the bounds of the platform versions defined in the app will cause either the build to fail or the app to fail at runtime.</span></span>

<span data-ttu-id="c2a50-148">Örneğin, Windows 10 Anniversary Edition (10.0; denetimleri paketinize TPMinV ayarladınız düşünelim Yapı 14393), böylece paket yalnızca UWP tarafından tüketilen emin olmak istiyorsanız, bağlı alt eşleşen projeleri.</span><span class="sxs-lookup"><span data-stu-id="c2a50-148">For example, let’s say you’ve set the TPMinV for your controls package to Windows 10 Anniversary Edition (10.0; Build 14393), so you want to ensure that the package is consumed only by UWP projects that match that lower bound.</span></span> <span data-ttu-id="c2a50-149">UWP projeleri tarafından tüketilmesi paketinizi izin vermek için aşağıdaki klasör adları, denetimleriyle paketi gerekir:</span><span class="sxs-lookup"><span data-stu-id="c2a50-149">To allow your package to be consumed by UWP projects, you must package your controls with the following folder names:</span></span>

    \lib\uap10.0.14393\*
    \ref\uap10.0.14393\*

<span data-ttu-id="c2a50-150">NuGet otomatik olarak alabilir proje TPMinV denetleyin ve Windows 10 Anniversary Edition (10.0; düşükse yükleme başarısız Yapı 14393)</span><span class="sxs-lookup"><span data-stu-id="c2a50-150">NuGet will automatically check the TPMinV of the consuming project, and fail installation if it is lower than Windows 10 Anniversary Edition (10.0; Build 14393)</span></span>

<span data-ttu-id="c2a50-151">WPF durumunda, .NET Framework v4.6.1 hedefleyen projeler tarafından tüketilen veya daha yüksek olması, WPF denetimleri paket istediğiniz varsayalım.</span><span class="sxs-lookup"><span data-stu-id="c2a50-151">In case of WPF, let's say you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher.</span></span> <span data-ttu-id="c2a50-152">Zorlamak için aşağıdaki klasör adları denetimleriyle paketi gerekir:</span><span class="sxs-lookup"><span data-stu-id="c2a50-152">To enforce that, you must package your controls with the following folder names:</span></span>

    \lib\net461\*
    \ref\net461\*

## <a name="add-design-time-support"></a><span data-ttu-id="c2a50-153">Tasarım zamanı desteği ekleme</span><span class="sxs-lookup"><span data-stu-id="c2a50-153">Add design-time support</span></span>

<span data-ttu-id="c2a50-154">Burada Özellik denetçisi'nde denetim özelliklerini göster yapılandırmak için özel donatıcıların, vb. yerleştirin ekleyin, `design.dll` içinde dosya `lib\uap10.0.14393\Design` klasörü hedef platformu için uygun olarak.</span><span class="sxs-lookup"><span data-stu-id="c2a50-154">To configure where the control properties show up in the property inspector, add custom adorners, etc., place your `design.dll` file inside the `lib\uap10.0.14393\Design` folder as appropriate to the target platform.</span></span> <span data-ttu-id="c2a50-155">Ayrıca, emin olmak için **[Şablonu Düzenle > bir kopyasını düzenlemek](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** özelliği works içermelidir `Generic.xaml` ve içinde birleştirir tüm kaynak sözlükleri `<your_assembly_name>\Themes` klasörü (yeniden kullanma Gerçek derleme adınız).</span><span class="sxs-lookup"><span data-stu-id="c2a50-155">Also, to ensure that the **[Edit Template > Edit a Copy](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** feature works, you must include the `Generic.xaml` and any resource dictionaries that it merges in the `<your_assembly_name>\Themes` folder (again, using your actual assembly name).</span></span> <span data-ttu-id="c2a50-156">(Bu dosyayı bir denetimin çalışma zamanı davranışını etkisi yoktur.) Bu nedenle, klasör yapısı şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="c2a50-156">(This file has no impact on the runtime behavior of a control.) The folder structure would thus appear as follows:</span></span>

    \lib
      \uap10.0.14393
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml


<span data-ttu-id="c2a50-157">WPF için WPF oluşturulacağı yeri örnekle devam edersek, .NET Framework v4.6.1 hedefleyen projeler tarafından tüketilen veya daha yüksek olması paketi denetler:</span><span class="sxs-lookup"><span data-stu-id="c2a50-157">For WPF, continuing with the example where you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher:</span></span>

    \lib
      \net461
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> <span data-ttu-id="c2a50-158">Varsayılan olarak, denetim özelliklerini Özellik denetçisi çeşitli kategorisinde altında gösterilir.</span><span class="sxs-lookup"><span data-stu-id="c2a50-158">By default, control properties will show up under the Miscellaneous category in the property inspector.</span></span>

## <a name="use-strings-and-resources"></a><span data-ttu-id="c2a50-159">Kullanım dizeler ve kaynakları</span><span class="sxs-lookup"><span data-stu-id="c2a50-159">Use strings and resources</span></span>

<span data-ttu-id="c2a50-160">Dize kaynakları katıştırma (`.resw`) denetiminizi veya kaybı UWP projesi tarafından kullanılan, pakette ayarlanan **yapı eylemi** özelliği `.resw` dosya **PRIResource**.</span><span class="sxs-lookup"><span data-stu-id="c2a50-160">You can embed string resources (`.resw`) in your package that can be used by your control or the consuming UWP project, set the **Build Action** property of the `.resw` file to **PRIResource**.</span></span>

<span data-ttu-id="c2a50-161">Bir örnek için bkz [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) ExtensionSDKasNuGetPackage örnekteki.</span><span class="sxs-lookup"><span data-stu-id="c2a50-161">For an example, refer to [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) in the ExtensionSDKasNuGetPackage sample.</span></span>

> [!Note]
> <span data-ttu-id="c2a50-162">Bu, yalnızca UWP denetimleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="c2a50-162">This is applicable only to UWP controls.</span></span>

## <a name="see-also"></a><span data-ttu-id="c2a50-163">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="c2a50-163">See also</span></span>

- [<span data-ttu-id="c2a50-164">UWP Paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="c2a50-164">Create UWP Packages</span></span>](create-uwp-packages.md)
- [<span data-ttu-id="c2a50-165">ExtensionSDKasNuGetPackage örnek</span><span class="sxs-lookup"><span data-stu-id="c2a50-165">ExtensionSDKasNuGetPackage sample</span></span>](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
