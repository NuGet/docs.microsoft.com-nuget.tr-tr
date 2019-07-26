---
title: Visual Studio 'da bir NuGet paketi yükleyip kullanma
description: Visual Studio projesindeki bir NuGet paketini yükleme ve kullanma işleminde izlenecek yol.
author: karann-msft
ms.author: karann
ms.date: 07/24/2018
ms.topic: quickstart
ms.openlocfilehash: a2be42aeb322cfd0ab43c9cec6ad1b063cbc3089
ms.sourcegitcommit: f291ff91561a6b58c2aec41c624d798e00ce41fa
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68462518"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-windows-only"></a><span data-ttu-id="f9140-103">Hızlı Başlangıç: Visual Studio 'da paket yükleyip kullanma (yalnızca Windows)</span><span class="sxs-lookup"><span data-stu-id="f9140-103">Quickstart: Install and use a package in Visual Studio (Windows only)</span></span>

<span data-ttu-id="f9140-104">NuGet paketleri, diğer geliştiricilerin projelerinizde kullanabileceğiniz bir yeniden kullanılabilir kod içerir.</span><span class="sxs-lookup"><span data-stu-id="f9140-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="f9140-105">Arka plan için bkz. [NuGet nedir?](../What-is-NuGet.md) .</span><span class="sxs-lookup"><span data-stu-id="f9140-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="f9140-106">Paketler, NuGet Paket Yöneticisi veya paket Yöneticisi konsolu kullanılarak Visual Studio projesine yüklenir.</span><span class="sxs-lookup"><span data-stu-id="f9140-106">Packages are installed into a Visual Studio project using the NuGet Package Manager or the Package Manager Console.</span></span> <span data-ttu-id="f9140-107">Bu makalede, popüler [Newtonsoft. JSON](https://www.nuget.org/packages/Newtonsoft.Json/) paketini ve bir WINDOWS PRESENTATION FOUNDATION (WPF) projesini kullanan işlem gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="f9140-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a Windows Presentation Foundation (WPF) project.</span></span> <span data-ttu-id="f9140-108">Aynı işlem, diğer tüm .NET veya .NET Core projeleri için de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="f9140-108">The same process applies to any other .NET or .NET Core project.</span></span>

<span data-ttu-id="f9140-109">Yüklendikten sonra, koddaki `using <namespace>` \<pakete, ad alanının\> kullandığınız pakete özgü olduğunu bakın.</span><span class="sxs-lookup"><span data-stu-id="f9140-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="f9140-110">Başvuru yapıldıktan sonra, paketini API 'SI aracılığıyla çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9140-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="f9140-111">**NuGet.org Ile Başlat**: *NuGet.org* gözatma, .NET geliştiricilerinin kendi uygulamalarında yeniden kullanabilecekleri bileşenleri genellikle bulmasıdır.</span><span class="sxs-lookup"><span data-stu-id="f9140-111">**Start with nuget.org**: Browsing *nuget.org* is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="f9140-112">Bu makalede gösterildiği gibi, *NuGet.org* doğrudan arayabilir veya Visual Studio içinde paketleri bulabilir ve yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9140-112">You can search *nuget.org* directly or find and install packages within Visual Studio as shown in this article.</span></span> <span data-ttu-id="f9140-113">Genel bilgi için bkz. [NuGet paketlerini bulma ve değerlendirme](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="f9140-113">For general information, see [Find and evaluate NuGet packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f9140-114">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="f9140-114">Prerequisites</span></span>

- <span data-ttu-id="f9140-115">.NET masaüstü geliştirme iş yüküyle Visual Studio 2019.</span><span class="sxs-lookup"><span data-stu-id="f9140-115">Visual Studio 2019 with the .NET Desktop Development workload.</span></span>

<span data-ttu-id="f9140-116">2019 Community Edition 'ı [VisualStudio.com](https://www.visualstudio.com/) adresinden ücretsiz olarak yükleyebilir veya profesyonel ya da Enterprise sürümlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9140-116">You can install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="f9140-117">Mac için Visual Studio kullanıyorsanız, bkz. [projenize bir NuGet paketi ekleme](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="f9140-117">If you're using Visual Studio for Mac, see [Include a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="f9140-118">Proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="f9140-118">Create a project</span></span>

<span data-ttu-id="f9140-119">NuGet paketleri, paketin proje ile aynı hedef Framework 'ü desteklemesi kaydıyla herhangi bir .NET projesine yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="f9140-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="f9140-120">Bu izlenecek yol için basit bir WPF uygulaması kullanın.</span><span class="sxs-lookup"><span data-stu-id="f9140-120">For this walkthrough, use a simple WPF app.</span></span> <span data-ttu-id="f9140-121">Visual Studio 'da **dosya > yeni proje...** öğesini kullanarak bir proje oluşturun, arama kutusuna **.net** yazın ve ardından **WPF uygulamasını (.NET Framework)** seçin.</span><span class="sxs-lookup"><span data-stu-id="f9140-121">Create a project in Visual Studio using **File > New Project...**, typing **.NET** in the search box, and then selecting the **WPF App (.NET Framework)**.</span></span> <span data-ttu-id="f9140-122">          **İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f9140-122">Click **Next**.</span></span> <span data-ttu-id="f9140-123">İstendiğinde **Framework** için varsayılan değerleri kabul edin.</span><span class="sxs-lookup"><span data-stu-id="f9140-123">Accept the default values for **Framework** when prompted.</span></span>

<span data-ttu-id="f9140-124">Visual Studio, Çözüm Gezgini ' de açılan projeyi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f9140-124">Visual Studio creates the project, which opens in Solution Explorer.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="f9140-125">Newtonsoft. JSON NuGet paketini ekleyin</span><span class="sxs-lookup"><span data-stu-id="f9140-125">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="f9140-126">Paketi yüklemek için, NuGet Paket Yöneticisi 'Ni ya da Paket Yöneticisi konsolunu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9140-126">To install the package, you can use either the NuGet Package Manager or the Package Manager Console.</span></span> <span data-ttu-id="f9140-127">Bir paket yüklediğinizde, NuGet, proje dosyanıza ya da bir `packages.config` dosyaya (proje biçimine bağlı olarak) bağımlılığı kaydeder.</span><span class="sxs-lookup"><span data-stu-id="f9140-127">When you install a package, NuGet records the dependency in either your project file or a `packages.config` file (depending on the project format).</span></span> <span data-ttu-id="f9140-128">Daha fazla bilgi için bkz. [paket tüketimine genel bakış ve iş akışı](../consume-packages/Overview-and-Workflow.md).</span><span class="sxs-lookup"><span data-stu-id="f9140-128">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="nuget-package-manager"></a><span data-ttu-id="f9140-129">NuGet Paket Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="f9140-129">NuGet Package Manager</span></span>

1. <span data-ttu-id="f9140-130">Çözüm Gezgini ' de, **Başvurular** ' a sağ tıklayın ve **NuGet Paketlerini Yönet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="f9140-130">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![Proje başvuruları için NuGet Paketlerini Yönet komutu](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="f9140-132">**Paket kaynağı**olarak "NuGet.org" öğesini seçin, **Gözden** geçirme sekmesini seçin, **Newtonsoft. JSON**' ı arayın, listeden bu paketi seçin ve sonra da **yüklemeyi**seçin:</span><span class="sxs-lookup"><span data-stu-id="f9140-132">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Newtonsoft. JSON paketi bulunuyor](media/QS_Use-03-NewtonsoftJson.png)

    <span data-ttu-id="f9140-134">NuGet Paket Yöneticisi hakkında daha fazla bilgi edinmek istiyorsanız bkz. [Visual Studio kullanarak paketleri yükleyip yönetme](../consume-packages/install-use-packages-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="f9140-134">If you want more information on the NuGet Package Manager, see [Install and manage packages using Visual Studio](../consume-packages/install-use-packages-visual-studio.md).</span></span>

1. <span data-ttu-id="f9140-135">Tüm lisans istemlerini kabul edin.</span><span class="sxs-lookup"><span data-stu-id="f9140-135">Accept any license prompts.</span></span>

1. <span data-ttu-id="f9140-136">(Yalnızca Visual Studio 2017) Paket Yönetimi biçimi seçmek isteyip istemediğiniz sorulursa **Proje dosyasında Packagereference**öğesini seçin:</span><span class="sxs-lookup"><span data-stu-id="f9140-136">(Visual Studio 2017 only) If prompted to select a package management format, select **PackageReference in project file**:</span></span>

    ![Paket yönetim biçimi seçme](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="f9140-138">Değişiklikleri gözden geçirmeniz istenirse **Tamam**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="f9140-138">If prompted to review changes, select **OK**.</span></span>

### <a name="package-manager-console"></a><span data-ttu-id="f9140-139">Paket Yöneticisi Konsolu</span><span class="sxs-lookup"><span data-stu-id="f9140-139">Package Manager Console</span></span>

1. <span data-ttu-id="f9140-140">**NuGet paket yöneticisi > Paket Yöneticisi konsolu menü komutunu > araçlar** ' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="f9140-140">Select the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="f9140-141">Konsol açıldıktan sonra, **varsayılan proje** açılan listesinin paketi yüklemek istediğiniz projeyi gösterdiğini kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="f9140-141">Once the console opens, check that the **Default project** drop-down list shows the project into which you want to install the package.</span></span> <span data-ttu-id="f9140-142">Çözümde tek bir projeniz varsa, zaten seçilidir.</span><span class="sxs-lookup"><span data-stu-id="f9140-142">If you have a single project in the solution, it is already selected.</span></span>

    ![Newtonsoft. JSON paketi bulunuyor](media/QS_Use-08-Console1.png)

1. <span data-ttu-id="f9140-144">Komutu `Install-Package Newtonsoft.Json` girin (bkz. [Install-Package](../reference/ps-reference/ps-ref-install-package.md)).</span><span class="sxs-lookup"><span data-stu-id="f9140-144">Enter the command `Install-Package Newtonsoft.Json` (see [Install-Package](../reference/ps-reference/ps-ref-install-package.md)).</span></span> <span data-ttu-id="f9140-145">Konsol penceresinde komutun çıktısı gösterilir.</span><span class="sxs-lookup"><span data-stu-id="f9140-145">The console window shows output for the command.</span></span> <span data-ttu-id="f9140-146">Hatalar genellikle paketin projenin hedef çerçevesiyle uyumlu olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="f9140-146">Errors typically indicate that the package isn't compatible with the project's target framework.</span></span>

   <span data-ttu-id="f9140-147">Paket Yöneticisi Konsolu hakkında daha fazla bilgi edinmek istiyorsanız bkz. [Paket Yöneticisi konsolu kullanılarak paketleri yükleyip yönetme](../consume-packages/install-use-packages-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="f9140-147">If you want more information on the Package Manager Console, see [Install and manage packages using Package Manager Console](../consume-packages/install-use-packages-powershell.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="f9140-148">Uygulamada Newtonsoft. JSON API 'sini kullanma</span><span class="sxs-lookup"><span data-stu-id="f9140-148">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="f9140-149">Projedeki Newtonsoft. JSON paketiyle, bir nesneyi insan tarafından okunabilen bir dizeye dönüştürmek `JsonConvert.SerializeObject` için yöntemini çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9140-149">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="f9140-150">Öğesini `MainWindow.xaml` açın ve var olan `Grid` öğeyi şu şekilde değiştirin:</span><span class="sxs-lookup"><span data-stu-id="f9140-150">Open `MainWindow.xaml` and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="White">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Width="100px" HorizontalAlignment="Center" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" HorizontalAlignment="Center" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="f9140-151">Dosyasını açın ( `MainWindow.xaml` düğüm altında Çözüm Gezgini bulunur) ve aşağıdaki kodu `MainWindow` sınıfına ekleyin: `MainWindow.xaml.cs`</span><span class="sxs-lookup"><span data-stu-id="f9140-151">Open the `MainWindow.xaml.cs` file (located in Solution Explorer under the `MainWindow.xaml` node), and insert the following code inside the `MainWindow` class:</span></span>

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

1. <span data-ttu-id="f9140-152">Newtonsoft. JSON paketini projeye ekleseniz de, kod dosyasının en üstünde bir `JsonConvert` `using` deyime ihtiyacınız olduğu için kırmızı dalgalı çizgiler altında görünür:</span><span class="sxs-lookup"><span data-stu-id="f9140-152">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement at the top of the code file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="f9140-153">F5 tuşuna basarak veya **hata ayıklamayı başlatmak > hata ayıkla**' yı seçerek uygulamayı derleyin ve çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f9140-153">Build and run the app by pressing F5 or selecting **Debug > Start Debugging**:</span></span>

    ![WPF uygulamasının ilk çıkışı](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="f9140-155">Bir JSON metniyle değiştirilmiş olan TextBlock içeriğini görmek için düğmeyi seçin:</span><span class="sxs-lookup"><span data-stu-id="f9140-155">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![Düğmeyi seçtikten sonra WPF uygulamasının çıkışı](media/QS_Use-07-AppEnd.png)

## <a name="next-steps"></a><span data-ttu-id="f9140-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f9140-157">Next steps</span></span>

<span data-ttu-id="f9140-158">İlk NuGet paketinizi yükleme ve kullanma hakkında Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="f9140-158">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f9140-159">Visual Studio kullanarak paketleri yükleyip yönetme</span><span class="sxs-lookup"><span data-stu-id="f9140-159">Install and manage packages using Visual Studio</span></span>](../consume-packages/install-use-packages-visual-studio.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="f9140-160">Paket Yöneticisi konsolu 'Nu kullanarak paket yükleyip yönetme</span><span class="sxs-lookup"><span data-stu-id="f9140-160">Install and manage packages using Package Manager Console</span></span>](../consume-packages/install-use-packages-powershell.md)

<span data-ttu-id="f9140-161">NuGet 'in sunabileceği daha fazlasını araştırmak için aşağıdaki bağlantıları seçin.</span><span class="sxs-lookup"><span data-stu-id="f9140-161">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="f9140-162">Paket tüketiminin genel bakış ve iş akışı</span><span class="sxs-lookup"><span data-stu-id="f9140-162">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="f9140-163">Paketleri bulma ve seçme</span><span class="sxs-lookup"><span data-stu-id="f9140-163">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="f9140-164">Proje dosyalarında paket başvuruları</span><span class="sxs-lookup"><span data-stu-id="f9140-164">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
