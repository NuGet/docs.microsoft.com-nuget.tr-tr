---
title: Visual Studio içinden NuGet paketlerini kullanmaya yönelik tanıtım Kılavuzu
description: Visual Studio projesindeki bir NuGet paketini yükleme ve kullanma işleminde izlenecek yol.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: deedc251b605b5b58659d3b70e1ca01b19c72865
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317563"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio"></a><span data-ttu-id="53e70-103">Hızlı Başlangıç: Visual Studio 'da paket yükleyip kullanma</span><span class="sxs-lookup"><span data-stu-id="53e70-103">Quickstart: Install and use a package in Visual Studio</span></span>

<span data-ttu-id="53e70-104">NuGet paketleri, diğer geliştiricilerin projelerinizde kullanabileceğiniz bir yeniden kullanılabilir kod içerir.</span><span class="sxs-lookup"><span data-stu-id="53e70-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="53e70-105">Arka plan için bkz. [NuGet nedir?](../What-is-NuGet.md) .</span><span class="sxs-lookup"><span data-stu-id="53e70-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="53e70-106">Paketler bir Visual Studio projesine Paket Yöneticisi Kullanıcı arabirimi veya paket Yöneticisi konsolu kullanılarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="53e70-106">Packages are installed into a Visual Studio project using the Package Manager UI or the Package Manager Console.</span></span> <span data-ttu-id="53e70-107">Bu makalede, popüler [Newtonsoft. JSON](https://www.nuget.org/packages/Newtonsoft.Json/) paketini ve bir evrensel WINDOWS platformu (UWP) projesini kullanan işlem gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="53e70-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a Universal Windows Platform (UWP) project.</span></span> <span data-ttu-id="53e70-108">Aynı işlem, diğer tüm .NET veya .NET Core projeleri için de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="53e70-108">The same process applies to any other .NET or .NET Core project.</span></span>

<span data-ttu-id="53e70-109">Yüklendikten sonra, koddaki `using <namespace>` \<pakete, ad alanının\> kullandığınız pakete özgü olduğunu bakın.</span><span class="sxs-lookup"><span data-stu-id="53e70-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="53e70-110">Başvuru yapıldıktan sonra, paketini API 'SI aracılığıyla çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="53e70-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="53e70-111">**NuGet.org Ile Başlat**: Nuget.org gözatma, .NET geliştiricilerinin kendi uygulamalarında yeniden kullanabilecekleri bileşenleri genellikle bulmasıdır.</span><span class="sxs-lookup"><span data-stu-id="53e70-111">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="53e70-112">Bu makalede gösterildiği gibi, nuget.org doğrudan arayabilir veya Visual Studio içinde paketleri bulabilir ve yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="53e70-112">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="53e70-113">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="53e70-113">Prerequisites</span></span>

- <span data-ttu-id="53e70-114">Evrensel Windows Platformu geliştirme iş yüküyle Visual Studio 2017 veya</span><span class="sxs-lookup"><span data-stu-id="53e70-114">Visual Studio 2017 with the Universal Windows Platform development workload, or</span></span>
- <span data-ttu-id="53e70-115">Evrensel Windows uygulamaları için araçlar içeren Visual Studio 2015 güncelleştirme 3.</span><span class="sxs-lookup"><span data-stu-id="53e70-115">Visual Studio 2015 Update 3 with Tools for Universal Windows Apps.</span></span>

<span data-ttu-id="53e70-116">2017 Community Edition 'ı [VisualStudio.com](https://www.visualstudio.com/) adresinden ücretsiz olarak yükleyebilir veya profesyonel ya da Enterprise sürümlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="53e70-116">You can install the 2017 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="53e70-117">Mac için Visual Studio kullanıyorsanız, bkz. [projenize bir NuGet paketi ekleme](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="53e70-117">If you're using Visual Studio for Mac, see [Include a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="53e70-118">Proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="53e70-118">Create a project</span></span>

<span data-ttu-id="53e70-119">NuGet paketleri, paketin proje ile aynı hedef Framework 'ü desteklemesi kaydıyla herhangi bir .NET projesine yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="53e70-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="53e70-120">Bu izlenecek yol için basit bir Evrensel Windows (UWP) uygulaması kullanın.</span><span class="sxs-lookup"><span data-stu-id="53e70-120">For this walkthrough, use a simple Universal Windows (UWP) app.</span></span> <span data-ttu-id="53e70-121">Visual Studio 'da **dosya > yeni proje...** öğesini kullanarak ve **Windows Evrensel > boş uygulamasını (Evrensel Windows)** seçerek bir proje oluşturun.</span><span class="sxs-lookup"><span data-stu-id="53e70-121">Create a project in Visual Studio using **File > New Project...** and selecting the **Windows Universal > Blank App (Universal Windows)**.</span></span> <span data-ttu-id="53e70-122">İstendiğinde, hedef sürüm için varsayılan değerleri ve en düşük sürümü kabul edin.</span><span class="sxs-lookup"><span data-stu-id="53e70-122">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="53e70-123">Newtonsoft. JSON NuGet paketini ekleyin</span><span class="sxs-lookup"><span data-stu-id="53e70-123">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="53e70-124">Paketi yüklemek için Paket Yöneticisi Kullanıcı arabirimini ya da Paket Yöneticisi konsolunu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="53e70-124">To install the package, you can use either the Package Manager UI or the Package Manager Console.</span></span> <span data-ttu-id="53e70-125">Bir paket yüklediğinizde NuGet, proje dosyanıza ya da bir `packages.config` dosyaya bağımlılığı kaydeder.</span><span class="sxs-lookup"><span data-stu-id="53e70-125">When you install a package, NuGet records the dependency in either your project file or a `packages.config` file.</span></span> <span data-ttu-id="53e70-126">Daha fazla bilgi için bkz. [paket tüketimine genel bakış ve iş akışı](../consume-packages/Overview-and-Workflow.md).</span><span class="sxs-lookup"><span data-stu-id="53e70-126">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="package-manager-ui"></a><span data-ttu-id="53e70-127">Paket Yöneticisi UI</span><span class="sxs-lookup"><span data-stu-id="53e70-127">Package Manager UI</span></span>

1. <span data-ttu-id="53e70-128">Çözüm Gezgini ' de, **Başvurular** ' a sağ tıklayın ve **NuGet Paketlerini Yönet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="53e70-128">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![Proje başvuruları için NuGet Paketlerini Yönet komutu](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="53e70-130">**Paket kaynağı**olarak "NuGet.org" öğesini seçin, **Gözden** geçirme sekmesini seçin, **Newtonsoft. JSON**' ı arayın, listeden bu paketi seçin ve sonra da **yüklemeyi**seçin:</span><span class="sxs-lookup"><span data-stu-id="53e70-130">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Newtonsoft. JSON paketi bulunuyor](media/QS_Use-03-NewtonsoftJson.png)

1. <span data-ttu-id="53e70-132">Tüm lisans istemlerini kabul edin.</span><span class="sxs-lookup"><span data-stu-id="53e70-132">Accept any license prompts.</span></span>

1. <span data-ttu-id="53e70-133">(Visual Studio 2017) Paket Yönetimi biçimi seçmek isteyip istemediğiniz sorulursa **Proje dosyasında Packagereference**öğesini seçin:</span><span class="sxs-lookup"><span data-stu-id="53e70-133">(Visual Studio 2017) If prompted to select a package management format, select **PackageReference in project file**:</span></span>

    ![Paket yönetim biçimi seçme](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="53e70-135">Değişiklikleri gözden geçirmeniz istenirse **Tamam**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="53e70-135">If prompted to review changes, select **OK**.</span></span>

### <a name="package-manager-console"></a><span data-ttu-id="53e70-136">Paket Yöneticisi Konsolu</span><span class="sxs-lookup"><span data-stu-id="53e70-136">Package Manager Console</span></span>

1. <span data-ttu-id="53e70-137">**NuGet paket yöneticisi > Paket Yöneticisi konsolu menü komutunu > araçlar** ' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="53e70-137">Select the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="53e70-138">Konsol açıldıktan sonra, **varsayılan proje** açılan listesinin paketi yüklemek istediğiniz projeyi gösterdiğini kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="53e70-138">Once the console opens, check that the **Default project** drop-down list shows the project into which you want to install the package.</span></span> <span data-ttu-id="53e70-139">Çözümde tek bir projeniz varsa, zaten seçilidir.</span><span class="sxs-lookup"><span data-stu-id="53e70-139">If you have a single project in the solution, it is already selected.</span></span>

    ![Newtonsoft. JSON paketi bulunuyor](media/QS_Use-08-Console1.png)

1. <span data-ttu-id="53e70-141">Komutu `Install-Package Newtonsoft.Json` girin (bkz. [Install-Package](../reference/ps-reference/ps-ref-install-package.md)).</span><span class="sxs-lookup"><span data-stu-id="53e70-141">Enter the command `Install-Package Newtonsoft.Json` (see [Install-Package](../reference/ps-reference/ps-ref-install-package.md)).</span></span> <span data-ttu-id="53e70-142">Konsol penceresinde komutun çıktısı gösterilir.</span><span class="sxs-lookup"><span data-stu-id="53e70-142">The console window shows output for the command.</span></span> <span data-ttu-id="53e70-143">Hatalar genellikle paketin projenin hedef çerçevesiyle uyumlu olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="53e70-143">Errors typically indicate that the package isn't compatible with the project's target framework.</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="53e70-144">Uygulamada Newtonsoft. JSON API 'sini kullanma</span><span class="sxs-lookup"><span data-stu-id="53e70-144">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="53e70-145">Projedeki Newtonsoft. JSON paketiyle, bir nesneyi insan tarafından okunabilen bir dizeye dönüştürmek `JsonConvert.SerializeObject` için yöntemini çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="53e70-145">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="53e70-146">Öğesini `MainPage.xaml` açın ve var olan `Grid` öğeyi şu şekilde değiştirin:</span><span class="sxs-lookup"><span data-stu-id="53e70-146">Open `MainPage.xaml` and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="53e70-147">Dosyasını açın ( `MainPage.xaml` düğüm altında Çözüm Gezgini bulunur) ve aşağıdaki kodu `MainPage` oluşturucunun içine ekleyin: `MainPage.xaml.cs`</span><span class="sxs-lookup"><span data-stu-id="53e70-147">Open the `MainPage.xaml.cs` file (located in Solution Explorer under the `MainPage.xaml` node), and insert the following code inside the `MainPage` constructor:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }

    private void Button_Click(object sender, RoutedEventArgs e)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@microsoft.com",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };
        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        TextBlock.Text = json;
    }
    ```

1. <span data-ttu-id="53e70-148">Newtonsoft. JSON paketini projeye ekleseniz de, kod dosyasının en üstünde bir `JsonConvert` `using` deyime ihtiyacınız olduğu için kırmızı dalgalı çizgiler altında görünür:</span><span class="sxs-lookup"><span data-stu-id="53e70-148">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement at the top of the code file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="53e70-149">F5 tuşuna basarak veya **hata ayıklamayı başlatmak > hata ayıkla**' yı seçerek uygulamayı derleyin ve çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="53e70-149">Build and run the app by pressing F5 or selecting **Debug > Start Debugging**:</span></span>

    ![UWP uygulamasının ilk çıkışı](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="53e70-151">Bir JSON metniyle değiştirilmiş olan TextBlock içeriğini görmek için düğmeyi seçin:</span><span class="sxs-lookup"><span data-stu-id="53e70-151">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![Düğmeyi seçtikten sonra UWP uygulamasının çıkışı](media/QS_Use-07-AppEnd.png)

## <a name="related-articles"></a><span data-ttu-id="53e70-153">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="53e70-153">Related articles</span></span>

- [<span data-ttu-id="53e70-154">Paket tüketiminin genel bakış ve iş akışı</span><span class="sxs-lookup"><span data-stu-id="53e70-154">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="53e70-155">Paketleri bulma ve seçme</span><span class="sxs-lookup"><span data-stu-id="53e70-155">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="53e70-156">Ortak NuGet yapılandırmaları</span><span class="sxs-lookup"><span data-stu-id="53e70-156">Common NuGet configurations</span></span>](../consume-packages/configuring-nuget-behavior.md)
