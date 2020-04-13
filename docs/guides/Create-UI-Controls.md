---
title: NuGet ile UI denetimleri nasıl paketilir?
description: Visual Studio ve Blend tasarımcıları için gerekli meta veriler ve destekleyici dosyalar da dahil olmak üzere UWP veya WPF denetimleri içeren NuGet paketleri nasıl oluşturulur?
author: karann-msft
ms.author: karann
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: da8c5a05311c790bf6b873bc0f1a077d3ef1db87
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "73610624"
---
# <a name="creating-ui-controls-as-nuget-packages"></a><span data-ttu-id="bc3db-103">NuGet paketleri olarak UI denetimleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="bc3db-103">Creating UI controls as NuGet packages</span></span>

<span data-ttu-id="bc3db-104">Visual Studio 2017'den itibaren NuGet paketlerinde sağladığınız UWP ve WPF denetimleri için ek özelliklerden yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc3db-104">Starting with Visual Studio 2017, you can take advantage of added capabilities for UWP and WPF controls that you deliver in NuGet packages.</span></span> <span data-ttu-id="bc3db-105">Bu [kılavuz, ExtensionSDKasNuGetPackage örnek](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)kullanarak UWP kontrolleri bağlamında bu yetenekleri size yol.</span><span class="sxs-lookup"><span data-stu-id="bc3db-105">This guide walks you through these capabilities in context of UWP controls using the [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span></span> <span data-ttu-id="bc3db-106">Aynı durum, aksi belirtilmedikçe WPF denetimleri için de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="bc3db-106">The same applies to WPF controls unless mentioned otherwise.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bc3db-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="bc3db-107">Prerequisites</span></span>

1. <span data-ttu-id="bc3db-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="bc3db-108">Visual Studio 2017</span></span>
1. <span data-ttu-id="bc3db-109">[UWP Paketlerinin](create-uwp-packages.md) Nasıl Oluşturulabildiğini Anlama</span><span class="sxs-lookup"><span data-stu-id="bc3db-109">Understanding of how to [Create UWP Packages](create-uwp-packages.md)</span></span>

## <a name="generate-library-layout"></a><span data-ttu-id="bc3db-110">Kitaplık Düzeni Oluşturma</span><span class="sxs-lookup"><span data-stu-id="bc3db-110">Generate Library Layout</span></span>

> [!Note]
> <span data-ttu-id="bc3db-111">Bu yalnızca UWP denetimleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="bc3db-111">This is applicable only to UWP controls.</span></span>

<span data-ttu-id="bc3db-112">Özelliğin `GenerateLibraryLayout` ayarlanması, proje oluşturma çıktısının nuspec'te tek tek dosya girişlerine gerek kalmadan paketlenmeye hazır bir düzende oluşturulmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="bc3db-112">Setting the `GenerateLibraryLayout` property ensures that the project build output is generated in a layout that is ready to be packaged without the need for individual file entries in the nuspec.</span></span>

<span data-ttu-id="bc3db-113">Proje özelliklerinden yapı sekmesine gidin ve "Kitaplık Düzeni Oluştur" onay kutusunu işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="bc3db-113">From the project properties, go to the build tab and check the "Generate Library Layout" check box.</span></span> <span data-ttu-id="bc3db-114">Bu, proje dosyasını değiştirir `GenerateLibraryLayout` ve bayrağı şu anda seçili yapı yapılandırmanız ve platformunuz için doğru olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="bc3db-114">This will modify the project file and set the `GenerateLibraryLayout` flag to true for your currently selected build configuration and platform.</span></span>

<span data-ttu-id="bc3db-115">Alternatif olarak, ilk koşulsuz özellik `<GenerateLibraryLayout>true</GenerateLibraryLayout>` grubuna eklemek için proje dosyasını edin.</span><span class="sxs-lookup"><span data-stu-id="bc3db-115">Alternately, edit the the project file to add `<GenerateLibraryLayout>true</GenerateLibraryLayout>` to the first unconditional property group.</span></span> <span data-ttu-id="bc3db-116">Bu, yapı yapılandırması ve platformune bakılmaksızın özelliği uygular.</span><span class="sxs-lookup"><span data-stu-id="bc3db-116">This would apply the property irrespective of the build configuration and platform.</span></span>

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a><span data-ttu-id="bc3db-117">XAML denetimleri için araç kutusu/varlık bölmedesteği ekleme</span><span class="sxs-lookup"><span data-stu-id="bc3db-117">Add toolbox/assets pane support for XAML controls</span></span>

<span data-ttu-id="bc3db-118">Visual Studio'daki XAML tasarımcısının araç kutusunda ve Karışım'ın Varlıklar bölmesinde bir XAML denetiminin `tools` görünmesi için, paket projenizin klasörünün kökünde bir `VisualStudioToolsManifest.xml` dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bc3db-118">To have a XAML control appear in the XAML designer’s toolbox in Visual Studio and the Assets pane of Blend, create a `VisualStudioToolsManifest.xml` file in the root of the `tools` folder of your package project.</span></span> <span data-ttu-id="bc3db-119">Araç kutusunda veya Varlıklar bölmesinde görünmesi için denetime ihtiyacınız yoksa, bu dosya gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="bc3db-119">This file is not required if you don’t need the control to appear in the toolbox or Assets pane.</span></span>

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

<span data-ttu-id="bc3db-120">Dosyanın yapısı aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="bc3db-120">The structure of the file is as follows:</span></span>

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

<span data-ttu-id="bc3db-121">burada:</span><span class="sxs-lookup"><span data-stu-id="bc3db-121">where:</span></span>

- <span data-ttu-id="bc3db-122">*your_package_file*: ("Yönetilen Paket" `ManagedPackage.winmd` bu örnek için kullanılan rasgele bir adlandırılmış ve başka bir anlamı yoktur) gibi kontrol dosyanızın adı.</span><span class="sxs-lookup"><span data-stu-id="bc3db-122">*your_package_file*: the name of your control file, such as `ManagedPackage.winmd` ("ManagedPackage" is an arbitrary named used for this example and has no other meaning).</span></span>
- <span data-ttu-id="bc3db-123">*vs_category*: Visual Studio tasarımcısının araç kutusunda kontrolün görünmesi gereken grubun etiketi.</span><span class="sxs-lookup"><span data-stu-id="bc3db-123">*vs_category*: The label for the group in which the control should appear in the Visual Studio designer’s toolbox.</span></span> <span data-ttu-id="bc3db-124">Denetimin araç kutusunda görünmesi için A `VSCategory` gereklidir.</span><span class="sxs-lookup"><span data-stu-id="bc3db-124">A `VSCategory` is necessary for the control to appear in the toolbox.</span></span>
- <span data-ttu-id="bc3db-125">*blend_category*: Karma tasarımcısının Varlıklar bölmesinde denetimin görünmesi gereken grubun etiketi.</span><span class="sxs-lookup"><span data-stu-id="bc3db-125">*blend_category*: The label for the group in which the control should appear in the Blend designer’s Assets pane.</span></span> <span data-ttu-id="bc3db-126">Denetimin Varlıklar'da görünmesi için A `BlendCategory` gereklidir.</span><span class="sxs-lookup"><span data-stu-id="bc3db-126">A `BlendCategory` is necessary for the control to appear in Assets.</span></span>
- <span data-ttu-id="bc3db-127">*type_full_name_n*: Ad alanı da `ManagedPackage.MyCustomControl`dahil olmak üzere her denetim için tam nitelikli ad.</span><span class="sxs-lookup"><span data-stu-id="bc3db-127">*type_full_name_n*: The fully-qualified name for each control, including the namespace, such as `ManagedPackage.MyCustomControl`.</span></span> <span data-ttu-id="bc3db-128">Nokta biçiminin hem yönetilen hem de yerel türler için kullanıldığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="bc3db-128">Note that the dot format is used for both managed and native types.</span></span>

<span data-ttu-id="bc3db-129">Daha gelişmiş senaryolarda, tek bir `<File>` paket `<FileList>` birden çok denetim derlemesi içerdiğinde, birden çok öğe de ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc3db-129">In more advanced scenarios, you can also include multiple `<File>` elements within `<FileList>` when a single package contains multiple control assemblies.</span></span> <span data-ttu-id="bc3db-130">Denetimlerinizi ayrı `<ToolboxItems>` kategorilerhalinde düzenlemek istiyorsanız, tek `<File>` bir düğüm içinde birden çok düğüm de olabilir.</span><span class="sxs-lookup"><span data-stu-id="bc3db-130">You can also have multiple `<ToolboxItems>` nodes within a single `<File>` if you want to organize your controls into separate categories.</span></span>

<span data-ttu-id="bc3db-131">Aşağıdaki örnekte, uygulanan `ManagedPackage.winmd` denetim Visual Studio ve Blend'te "Yönetilen Paket" adlı bir grupta görünür ve bu grupta "MyCustomControl" görünür.</span><span class="sxs-lookup"><span data-stu-id="bc3db-131">In the following example, the control implemented in `ManagedPackage.winmd` will appear in Visual Studio and Blend in a group named “Managed Package”, and “MyCustomControl” will appear in that group.</span></span> <span data-ttu-id="bc3db-132">Tüm bu isimler rasgele.</span><span class="sxs-lookup"><span data-stu-id="bc3db-132">All these names are arbitrary.</span></span>

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![Visual Studio'da göründüğü gibi bir örnek denetim](media/UWP-control-vs-toolbox.png)

![Karışım'da görünen bir örnek denetim](media/UWP-control-blend-assets.png)

> [!Note]
> <span data-ttu-id="bc3db-135">Araç kutusu/varlıklar bölmesinde görmek istediğiniz her denetimi açıkça belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="bc3db-135">You must explicitly specify every control that you would like to see in the toolbox/assets pane.</span></span> <span data-ttu-id="bc3db-136">Biçimde `Namespace.ControlName`belirttiğinizi emin olun.</span><span class="sxs-lookup"><span data-stu-id="bc3db-136">Ensure you specify them in the format `Namespace.ControlName`.</span></span>

## <a name="add-custom-icons-to-your-controls"></a><span data-ttu-id="bc3db-137">Denetimlerinize özel simgeler ekleme</span><span class="sxs-lookup"><span data-stu-id="bc3db-137">Add custom icons to your controls</span></span>

<span data-ttu-id="bc3db-138">Araç kutusu/varlıklar bölmesinde özel bir simge görüntülemek için, projenize `design.dll` veya ilgili projeye "Namespace.ControlName.extension" adıyla bir resim ekleyin ve yapı eylemini "Gömülü Kaynak" olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="bc3db-138">To display a custom icon in the toolbox/assets pane, add an image to your project or the corresponding `design.dll` project with the name “Namespace.ControlName.extension” and set the build action to “Embedded Resource”.</span></span> <span data-ttu-id="bc3db-139">Ayrıca, ilişkili `AssemblyInfo.cs` nin ProvideMetadata özniteliğini belirttiğinden `[assembly: ProvideMetadata(typeof(RegisterMetadata))]`de emin olmalısınız .</span><span class="sxs-lookup"><span data-stu-id="bc3db-139">You must also ensure that the associated `AssemblyInfo.cs` specifies the ProvideMetadata attribute - `[assembly: ProvideMetadata(typeof(RegisterMetadata))]`.</span></span> <span data-ttu-id="bc3db-140">Bu [örneğe](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20)bakın.</span><span class="sxs-lookup"><span data-stu-id="bc3db-140">See this [sample](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20).</span></span>

<span data-ttu-id="bc3db-141">Desteklenen biçimler `.png`, `.jpg` `.jpeg`, `.gif`, `.bmp`, ve .</span><span class="sxs-lookup"><span data-stu-id="bc3db-141">Supported formats are `.png`, `.jpg`, `.jpeg`, `.gif`, and `.bmp`.</span></span> <span data-ttu-id="bc3db-142">Önerilen format 16 piksele 16 pikselbMP24'dür.</span><span class="sxs-lookup"><span data-stu-id="bc3db-142">The recommended format is BMP24 in 16 pixels by 16 pixels.</span></span>

![Araç kutusu simgesi örneği](https://raw.githubusercontent.com/NuGet/docs.microsoft.com-nuget/live/docs/guides/media/ColorPicker_16x16x24.bmp)

<span data-ttu-id="bc3db-144">Pembe arka plan çalışma zamanında değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="bc3db-144">The pink background is replaced at runtime.</span></span> <span data-ttu-id="bc3db-145">Visual Studio teması değiştirildiğinde ve arka plan rengi beklendiğinde simgeler yeniden renklendirilir.</span><span class="sxs-lookup"><span data-stu-id="bc3db-145">The icons are recolored when the Visual Studio theme is changed and that background color is expected.</span></span> <span data-ttu-id="bc3db-146">Daha fazla bilgi için, [Visual Studio için Lütfen Resim ve Simgelere](https://docs.microsoft.com/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio)başvurun.</span><span class="sxs-lookup"><span data-stu-id="bc3db-146">For more information, please reference [Images and Icons for Visual Studio](https://docs.microsoft.com/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio).</span></span>

<span data-ttu-id="bc3db-147">Aşağıdaki örnekte, proje "ManagedPackage.MyCustomControl.png" adlı bir resim dosyası içerir.</span><span class="sxs-lookup"><span data-stu-id="bc3db-147">In the example below, the project contains an image file named “ManagedPackage.MyCustomControl.png”.</span></span>

![Projede özel simge ayarlama](media/UWP-control-custom-icon.png)

> [!Note]
> <span data-ttu-id="bc3db-149">Yerel denetimler için simgeyi `design.dll` projeye kaynak olarak koymanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bc3db-149">For native controls, you must put the icon as a resource in the `design.dll` project.</span></span>

## <a name="support-specific-windows-platform-versions"></a><span data-ttu-id="bc3db-150">Belirli Windows platform sürümlerini destekleyin</span><span class="sxs-lookup"><span data-stu-id="bc3db-150">Support specific Windows platform versions</span></span>

<span data-ttu-id="bc3db-151">UWP paketleri, uygulamanın yüklenebileceği işletim sistemi sürümünün üst ve alt sınırlarını tanımlayan targetplatformversion (TPV) ve TargetPlatformMinVersion (TPMinV) içerir.</span><span class="sxs-lookup"><span data-stu-id="bc3db-151">UWP packages have a TargetPlatformVersion (TPV) and TargetPlatformMinVersion (TPMinV) that define the upper and lower bounds of the OS version where the app can be installed.</span></span> <span data-ttu-id="bc3db-152">TPV ayrıca, uygulamanın oluşturuladığı SDK sürümünü de belirtir.</span><span class="sxs-lookup"><span data-stu-id="bc3db-152">TPV further specifies the version of the SDK against which the app is built.</span></span> <span data-ttu-id="bc3db-153">Bir UWP paketi yazarken bu özelliklere dikkat edin: Uygulamada tanımlanan platform sürümlerinin sınırları dışında API'ler kullanmak, yapının çalışma zamanında başarısız olmasıveya uygulamanın başarısız olması durumunda neden olur.</span><span class="sxs-lookup"><span data-stu-id="bc3db-153">Be mindful of these properties when authoring a UWP package: using APIs outside the bounds of the platform versions defined in the app will cause either the build to fail or the app to fail at runtime.</span></span>

<span data-ttu-id="bc3db-154">Örneğin, denetim paketiniz için TPMinV'i Windows 10 Anniversary Edition (10.0; 14393) oluşturun, böylece paketin yalnızca alt sınırla eşleşen UWP projeleri tarafından tüketilmesini sağlamak istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="bc3db-154">For example, let’s say you’ve set the TPMinV for your controls package to Windows 10 Anniversary Edition (10.0; Build 14393), so you want to ensure that the package is consumed only by UWP projects that match that lower bound.</span></span> <span data-ttu-id="bc3db-155">Paketinizin UWP projeleri tarafından tüketilmesine izin vermek için, denetimlerinizi aşağıdaki klasör adlarıyla paketlemeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="bc3db-155">To allow your package to be consumed by UWP projects, you must package your controls with the following folder names:</span></span>

    \lib\uap10.0.14393\*
    \ref\uap10.0.14393\*

<span data-ttu-id="bc3db-156">NuGet, tüketen projenin TPMinV'ini otomatik olarak denetler ve Windows 10 Anniversary Edition'dan daha düşükse yüklemeyi başarısız olur (10.0; Yapı 14393)</span><span class="sxs-lookup"><span data-stu-id="bc3db-156">NuGet will automatically check the TPMinV of the consuming project, and fail installation if it is lower than Windows 10 Anniversary Edition (10.0; Build 14393)</span></span>

<span data-ttu-id="bc3db-157">WPF durumunda, WPF kontrol paketinizin .NET Framework v4.6.1 veya daha yüksek hedefleyen projeler tarafından tüketilmesini istediğinizi varsayalım.</span><span class="sxs-lookup"><span data-stu-id="bc3db-157">In case of WPF, let's say you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher.</span></span> <span data-ttu-id="bc3db-158">Bunu uygulamak için denetimlerinizi aşağıdaki klasör adlarıyla paketlemeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="bc3db-158">To enforce that, you must package your controls with the following folder names:</span></span>

    \lib\net461\*
    \ref\net461\*

## <a name="add-design-time-support"></a><span data-ttu-id="bc3db-159">Tasarım zamanı desteği ekleme</span><span class="sxs-lookup"><span data-stu-id="bc3db-159">Add design-time support</span></span>

<span data-ttu-id="bc3db-160">Denetim özelliklerinin özellik denetçisinde nerede görünacağını yapılandırmak, özel süsleyiciler `design.dll` vb. `lib\uap10.0.14393\Design` eklemek için dosyanızı hedef platforma uygun şekilde klasörün içine yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="bc3db-160">To configure where the control properties show up in the property inspector, add custom adorners, etc., place your `design.dll` file inside the `lib\uap10.0.14393\Design` folder as appropriate to the target platform.</span></span> <span data-ttu-id="bc3db-161">Ayrıca, **[Şablonu Edit > Kopyala](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** özelliğinin çalıştığından emin `Generic.xaml` olmak için, `<your_assembly_name>\Themes` klasörde birleştirdiği kaynak sözlüklerini (yine, gerçek derleme adınızı kullanarak) eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="bc3db-161">Also, to ensure that the **[Edit Template > Edit a Copy](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** feature works, you must include the `Generic.xaml` and any resource dictionaries that it merges in the `<your_assembly_name>\Themes` folder (again, using your actual assembly name).</span></span> <span data-ttu-id="bc3db-162">(Bu dosyanın denetimin çalışma zamanı davranışı üzerinde hiçbir etkisi yoktur.) Klasör yapısı böylece aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="bc3db-162">(This file has no impact on the runtime behavior of a control.) The folder structure would thus appear as follows:</span></span>

    \lib
      \uap10.0.14393
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml


<span data-ttu-id="bc3db-163">WPF için, WPF denetim paketinizin .NET Framework v4.6.1 veya daha yüksek hedefleyen projeler tarafından tüketilmesini istediğiniz örnekle devam edin:</span><span class="sxs-lookup"><span data-stu-id="bc3db-163">For WPF, continuing with the example where you would like your WPF controls package to be consumed by projects targeting .NET Framework v4.6.1 or higher:</span></span>

    \lib
      \net461
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> <span data-ttu-id="bc3db-164">Varsayılan olarak, denetim özellikleri özellik denetçisindeki Çeşitli kategori altında gösterilecek.</span><span class="sxs-lookup"><span data-stu-id="bc3db-164">By default, control properties will show up under the Miscellaneous category in the property inspector.</span></span>

## <a name="use-strings-and-resources"></a><span data-ttu-id="bc3db-165">Dizeleri ve kaynakları kullanma</span><span class="sxs-lookup"><span data-stu-id="bc3db-165">Use strings and resources</span></span>

<span data-ttu-id="bc3db-166">Paketinize, denetiminiz`.resw`veya tüketen UWP projeniz tarafından kullanılabilecek dize kaynaklarını ( ) katıştırabilir, dosyanın **Yapı Eylemi** özelliğini `.resw` **PRIResource**olarak ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc3db-166">You can embed string resources (`.resw`) in your package that can be used by your control or the consuming UWP project, set the **Build Action** property of the `.resw` file to **PRIResource**.</span></span>

<span data-ttu-id="bc3db-167">Örneğin, ExtensionSDKasNuGetPackage örneğindeki [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) bakın.</span><span class="sxs-lookup"><span data-stu-id="bc3db-167">For an example, refer to [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) in the ExtensionSDKasNuGetPackage sample.</span></span>

> [!Note]
> <span data-ttu-id="bc3db-168">Bu yalnızca UWP denetimleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="bc3db-168">This is applicable only to UWP controls.</span></span>

## <a name="see-also"></a><span data-ttu-id="bc3db-169">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="bc3db-169">See also</span></span>

- [<span data-ttu-id="bc3db-170">UWP Paketleri Oluşturma</span><span class="sxs-lookup"><span data-stu-id="bc3db-170">Create UWP Packages</span></span>](create-uwp-packages.md)
- [<span data-ttu-id="bc3db-171">ExtensionSDKasNuGetPackage örneği</span><span class="sxs-lookup"><span data-stu-id="bc3db-171">ExtensionSDKasNuGetPackage sample</span></span>](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
