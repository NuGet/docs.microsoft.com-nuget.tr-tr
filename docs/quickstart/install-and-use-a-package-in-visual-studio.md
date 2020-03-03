---
title: Visual Studio 'da bir NuGet paketi yükleyip kullanma
description: Visual Studio projesindeki bir NuGet paketini yükleme ve kullanma işleminde izlenecek yol.
author: karann-msft
ms.author: karann
ms.date: 07/24/2018
ms.topic: quickstart
ms.openlocfilehash: 96e138561390984d9def495ba5e091c43023cc92
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231337"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-windows-only"></a><span data-ttu-id="e9028-103">Hızlı başlangıç: Visual Studio 'da paket yükleyip kullanma (yalnızca Windows)</span><span class="sxs-lookup"><span data-stu-id="e9028-103">Quickstart: Install and use a package in Visual Studio (Windows only)</span></span>

<span data-ttu-id="e9028-104">NuGet paketleri, diğer geliştiricilerin projelerinizde kullanabileceğiniz bir yeniden kullanılabilir kod içerir.</span><span class="sxs-lookup"><span data-stu-id="e9028-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="e9028-105">Arka plan için bkz. [NuGet nedir?](../What-is-NuGet.md) .</span><span class="sxs-lookup"><span data-stu-id="e9028-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="e9028-106">Paketler, NuGet Paket Yöneticisi veya paket Yöneticisi konsolu kullanılarak Visual Studio projesine yüklenir.</span><span class="sxs-lookup"><span data-stu-id="e9028-106">Packages are installed into a Visual Studio project using the NuGet Package Manager or the Package Manager Console.</span></span> <span data-ttu-id="e9028-107">Bu makalede, popüler [Newtonsoft. JSON](https://www.nuget.org/packages/Newtonsoft.Json/) paketini ve bir WINDOWS PRESENTATION FOUNDATION (WPF) projesini kullanan işlem gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="e9028-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a Windows Presentation Foundation (WPF) project.</span></span> <span data-ttu-id="e9028-108">Aynı işlem, diğer tüm .NET veya .NET Core projeleri için de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="e9028-108">The same process applies to any other .NET or .NET Core project.</span></span>

<span data-ttu-id="e9028-109">Yüklendikten sonra, `using <namespace>` \<ad alanı\> kullandığınız pakete özgü olan koddaki pakete bakın.</span><span class="sxs-lookup"><span data-stu-id="e9028-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="e9028-110">Başvuru yapıldıktan sonra, paketini API 'SI aracılığıyla çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e9028-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="e9028-111">**NuGet.org Ile başlayın**: gözatma *NuGet.org* , .NET geliştiricilerinin kendi uygulamalarında yeniden kullanabilecekleri bileşenleri genellikle nasıl buldukları.</span><span class="sxs-lookup"><span data-stu-id="e9028-111">**Start with nuget.org**: Browsing *nuget.org* is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="e9028-112">Bu makalede gösterildiği gibi, *NuGet.org* doğrudan arayabilir veya Visual Studio içinde paketleri bulabilir ve yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e9028-112">You can search *nuget.org* directly or find and install packages within Visual Studio as shown in this article.</span></span> <span data-ttu-id="e9028-113">Genel bilgi için bkz. [NuGet paketlerini bulma ve değerlendirme](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="e9028-113">For general information, see [Find and evaluate NuGet packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e9028-114">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="e9028-114">Prerequisites</span></span>

- <span data-ttu-id="e9028-115">.NET masaüstü geliştirme iş yüküyle Visual Studio 2019.</span><span class="sxs-lookup"><span data-stu-id="e9028-115">Visual Studio 2019 with the .NET Desktop Development workload.</span></span>

<span data-ttu-id="e9028-116">2019 Community Edition 'ı [VisualStudio.com](https://www.visualstudio.com/) adresinden ücretsiz olarak yükleyebilir veya profesyonel ya da Enterprise sürümlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e9028-116">You can install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="e9028-117">Mac için Visual Studio kullanıyorsanız, bkz. [Mac için Visual Studio bir paketi yükleyip kullanma](install-and-use-a-package-in-visual-studio-mac.md).</span><span class="sxs-lookup"><span data-stu-id="e9028-117">If you're using Visual Studio for Mac, see [Install and use a package in Visual Studio for Mac](install-and-use-a-package-in-visual-studio-mac.md).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="e9028-118">Proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="e9028-118">Create a project</span></span>

<span data-ttu-id="e9028-119">NuGet paketleri, paketin proje ile aynı hedef Framework 'ü desteklemesi kaydıyla herhangi bir .NET projesine yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="e9028-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="e9028-120">Bu izlenecek yol için basit bir WPF uygulaması kullanın.</span><span class="sxs-lookup"><span data-stu-id="e9028-120">For this walkthrough, use a simple WPF app.</span></span> <span data-ttu-id="e9028-121">Visual Studio 'da > **Dosya** **Yeni proje**' yi kullanarak bir proje oluşturun, arama kutusuna **.net** yazın ve ardından **WPF uygulamasını (.NET Framework)** seçin.</span><span class="sxs-lookup"><span data-stu-id="e9028-121">Create a project in Visual Studio using **File** > **New Project**, typing **.NET** in the search box, and then selecting the **WPF App (.NET Framework)**.</span></span> <span data-ttu-id="e9028-122">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e9028-122">Click **Next**.</span></span> <span data-ttu-id="e9028-123">İstendiğinde **Framework** için varsayılan değerleri kabul edin.</span><span class="sxs-lookup"><span data-stu-id="e9028-123">Accept the default values for **Framework** when prompted.</span></span>

<span data-ttu-id="e9028-124">Visual Studio, Çözüm Gezgini ' de açılan projeyi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e9028-124">Visual Studio creates the project, which opens in Solution Explorer.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="e9028-125">Newtonsoft. JSON NuGet paketini ekleyin</span><span class="sxs-lookup"><span data-stu-id="e9028-125">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="e9028-126">Paketi yüklemek için, NuGet Paket Yöneticisi 'Ni ya da Paket Yöneticisi konsolunu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e9028-126">To install the package, you can use either the NuGet Package Manager or the Package Manager Console.</span></span> <span data-ttu-id="e9028-127">Bir paket yüklediğinizde NuGet, proje dosyanıza veya bir `packages.config` dosyasına bağımlılığı kaydeder (proje biçimine bağlı olarak).</span><span class="sxs-lookup"><span data-stu-id="e9028-127">When you install a package, NuGet records the dependency in either your project file or a `packages.config` file (depending on the project format).</span></span> <span data-ttu-id="e9028-128">Daha fazla bilgi için bkz. [paket tüketimine genel bakış ve iş akışı](../consume-packages/Overview-and-Workflow.md).</span><span class="sxs-lookup"><span data-stu-id="e9028-128">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="nuget-package-manager"></a><span data-ttu-id="e9028-129">NuGet Paket Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="e9028-129">NuGet Package Manager</span></span>

1. <span data-ttu-id="e9028-130">Çözüm Gezgini ' de, **Başvurular** ' a sağ tıklayın ve **NuGet Paketlerini Yönet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="e9028-130">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![Proje başvuruları için NuGet Paketlerini Yönet komutu](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="e9028-132">**Paket kaynağı**olarak "NuGet.org" öğesini seçin, **Gözden** geçirme sekmesini seçin, **Newtonsoft. JSON**' ı arayın, listeden bu paketi seçin ve sonra da **yüklemeyi**seçin:</span><span class="sxs-lookup"><span data-stu-id="e9028-132">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Newtonsoft. JSON paketi bulunuyor](media/QS_Use-03-NewtonsoftJson.png)

    <span data-ttu-id="e9028-134">NuGet Paket Yöneticisi hakkında daha fazla bilgi edinmek istiyorsanız bkz. [Visual Studio kullanarak paketleri yükleyip yönetme](../consume-packages/install-use-packages-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="e9028-134">If you want more information on the NuGet Package Manager, see [Install and manage packages using Visual Studio](../consume-packages/install-use-packages-visual-studio.md).</span></span>

1. <span data-ttu-id="e9028-135">Tüm lisans istemlerini kabul edin.</span><span class="sxs-lookup"><span data-stu-id="e9028-135">Accept any license prompts.</span></span>

1. <span data-ttu-id="e9028-136">(Yalnızca Visual Studio 2017) Paket Yönetimi biçimi seçmek isteyip istemediğiniz sorulursa **Proje dosyasında Packagereference**öğesini seçin:</span><span class="sxs-lookup"><span data-stu-id="e9028-136">(Visual Studio 2017 only) If prompted to select a package management format, select **PackageReference in project file**:</span></span>

    ![Paket yönetim biçimi seçme](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="e9028-138">Değişiklikleri gözden geçirmeniz istenirse **Tamam**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="e9028-138">If prompted to review changes, select **OK**.</span></span>

### <a name="package-manager-console"></a><span data-ttu-id="e9028-139">Paket Yöneticisi Konsolu</span><span class="sxs-lookup"><span data-stu-id="e9028-139">Package Manager Console</span></span>

1. <span data-ttu-id="e9028-140">**NuGet paket yöneticisi** > **Paket Yöneticisi konsolu** menü komutunu > **Araçlar** ' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="e9028-140">Select the **Tools** > **NuGet Package Manager** > **Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="e9028-141">Konsol açıldıktan sonra, **varsayılan proje** açılan listesinin paketi yüklemek istediğiniz projeyi gösterdiğini kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="e9028-141">Once the console opens, check that the **Default project** drop-down list shows the project into which you want to install the package.</span></span> <span data-ttu-id="e9028-142">Çözümde tek bir projeniz varsa, zaten seçilidir.</span><span class="sxs-lookup"><span data-stu-id="e9028-142">If you have a single project in the solution, it is already selected.</span></span>

    ![Newtonsoft. JSON paketi bulunuyor](media/QS_Use-08-Console1.png)

1. <span data-ttu-id="e9028-144">Komut `Install-Package Newtonsoft.Json` girin (bkz. [Install-Package](../reference/ps-reference/ps-ref-install-package.md)).</span><span class="sxs-lookup"><span data-stu-id="e9028-144">Enter the command `Install-Package Newtonsoft.Json` (see [Install-Package](../reference/ps-reference/ps-ref-install-package.md)).</span></span> <span data-ttu-id="e9028-145">Konsol penceresinde komutun çıktısı gösterilir.</span><span class="sxs-lookup"><span data-stu-id="e9028-145">The console window shows output for the command.</span></span> <span data-ttu-id="e9028-146">Hatalar genellikle paketin projenin hedef çerçevesiyle uyumlu olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="e9028-146">Errors typically indicate that the package isn't compatible with the project's target framework.</span></span>

   <span data-ttu-id="e9028-147">Paket Yöneticisi Konsolu hakkında daha fazla bilgi edinmek istiyorsanız bkz. [Paket Yöneticisi konsolu kullanılarak paketleri yükleyip yönetme](../consume-packages/install-use-packages-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e9028-147">If you want more information on the Package Manager Console, see [Install and manage packages using Package Manager Console](../consume-packages/install-use-packages-powershell.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="e9028-148">Uygulamada Newtonsoft. JSON API 'sini kullanma</span><span class="sxs-lookup"><span data-stu-id="e9028-148">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="e9028-149">Projedeki Newtonsoft. JSON paketiyle, bir nesneyi insan tarafından okunabilen bir dizeye dönüştürmek için `JsonConvert.SerializeObject` yöntemini çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e9028-149">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="e9028-150">`MainWindow.xaml` açın ve var olan `Grid` öğesini aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="e9028-150">Open `MainWindow.xaml` and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="White">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Width="100px" HorizontalAlignment="Center" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" HorizontalAlignment="Center" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="e9028-151">`MainWindow.xaml.cs` dosyasını açın (`MainWindow.xaml` düğümü altında Çözüm Gezgini bulunur) ve aşağıdaki kodu `MainWindow` sınıfına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e9028-151">Open the `MainWindow.xaml.cs` file (located in Solution Explorer under the `MainWindow.xaml` node), and insert the following code inside the `MainWindow` class:</span></span>

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

1. <span data-ttu-id="e9028-152">Newtonsoft. JSON paketini projeye ekleseniz de, kod dosyasının en üstünde bir `using` bildirimine ihtiyacınız olduğundan `JsonConvert` altında Red dalgalı çizgiler görünür:</span><span class="sxs-lookup"><span data-stu-id="e9028-152">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement at the top of the code file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="e9028-153">F5 tuşuna basarak veya hata **ayıklamayı başlatmak** > **Hata Ayıkla** ' yı seçerek uygulamayı derleyin ve çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e9028-153">Build and run the app by pressing F5 or selecting **Debug** > **Start Debugging**:</span></span>

    ![WPF uygulamasının ilk çıkışı](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="e9028-155">Bir JSON metniyle değiştirilmiş olan TextBlock içeriğini görmek için düğmeyi seçin:</span><span class="sxs-lookup"><span data-stu-id="e9028-155">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![Düğmeyi seçtikten sonra WPF uygulamasının çıkışı](media/QS_Use-07-AppEnd.png)

## <a name="related-video"></a><span data-ttu-id="e9028-157">İlgili video</span><span class="sxs-lookup"><span data-stu-id="e9028-157">Related video</span></span>

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-Visual-Studio-2-of-5/player]

<span data-ttu-id="e9028-158">[Channel 9](https://channel9.msdn.com/Series/NuGet-101) ve [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_)'da daha fazla NuGet videoları bulun.</span><span class="sxs-lookup"><span data-stu-id="e9028-158">Find more NuGet videos on [Channel 9](https://channel9.msdn.com/Series/NuGet-101) and [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9028-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e9028-159">Next steps</span></span>

<span data-ttu-id="e9028-160">İlk NuGet paketinizi yükleme ve kullanma hakkında Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="e9028-160">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e9028-161">Visual Studio kullanarak paketleri yükleyip yönetme</span><span class="sxs-lookup"><span data-stu-id="e9028-161">Install and manage packages using Visual Studio</span></span>](../consume-packages/install-use-packages-visual-studio.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="e9028-162">Paket Yöneticisi konsolu 'Nu kullanarak paket yükleyip yönetme</span><span class="sxs-lookup"><span data-stu-id="e9028-162">Install and manage packages using Package Manager Console</span></span>](../consume-packages/install-use-packages-powershell.md)

<span data-ttu-id="e9028-163">NuGet 'in sunabileceği daha fazlasını araştırmak için aşağıdaki bağlantıları seçin.</span><span class="sxs-lookup"><span data-stu-id="e9028-163">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="e9028-164">Paket tüketiminin genel bakış ve iş akışı</span><span class="sxs-lookup"><span data-stu-id="e9028-164">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="e9028-165">Paketleri bulma ve seçme</span><span class="sxs-lookup"><span data-stu-id="e9028-165">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="e9028-166">Proje dosyalarında paket başvuruları</span><span class="sxs-lookup"><span data-stu-id="e9028-166">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
