---
title: Visual Studio'da NuGet paketi yükleyin ve kullanın
description: Visual Studio projesinde nuget paketini yükleme ve kullanma süreci hakkında bir iz geçidi öğreticisi.
author: karann-msft
ms.author: karann
ms.date: 07/24/2018
ms.topic: quickstart
ms.openlocfilehash: 10bc34653d294cf70b5c91ce79a79cf6532fba1b
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "80147493"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-windows-only"></a><span data-ttu-id="176fe-103">Quickstart: Visual Studio'da bir paket yükleyin ve kullanın (yalnızca Windows)</span><span class="sxs-lookup"><span data-stu-id="176fe-103">Quickstart: Install and use a package in Visual Studio (Windows only)</span></span>

<span data-ttu-id="176fe-104">NuGet paketleri, diğer geliştiricilerin projelerinizde kullanmak üzere kullanabileceğiniz yeniden kullanılabilir kodlar içerir.</span><span class="sxs-lookup"><span data-stu-id="176fe-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="176fe-105">NuGet [nedir?](../What-is-NuGet.md)</span><span class="sxs-lookup"><span data-stu-id="176fe-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="176fe-106">Paketler NuGet Paket Yöneticisi, [Paket Yöneticisi Konsolu](../consume-packages/install-use-packages-powershell)veya [dotnet CLI](install-and-use-a-package-using-the-dotnet-cli.md)kullanılarak Visual Studio projesine yüklenir.</span><span class="sxs-lookup"><span data-stu-id="176fe-106">Packages are installed into a Visual Studio project using the NuGet Package Manager, the [Package Manager Console](../consume-packages/install-use-packages-powershell), or the [dotnet CLI](install-and-use-a-package-using-the-dotnet-cli.md).</span></span> <span data-ttu-id="176fe-107">Bu makale, popüler [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) paketi ve Bir Windows Sunum Vakfı (WPF) projesini kullanarak süreci göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="176fe-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a Windows Presentation Foundation (WPF) project.</span></span> <span data-ttu-id="176fe-108">Aynı işlem diğer .NET veya .NET Core projesi için de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="176fe-108">The same process applies to any other .NET or .NET Core project.</span></span>

<span data-ttu-id="176fe-109">Yüklendikten sonra, ad alanının `using <namespace>` \<\> kullanmakta olduğunuz pakete özgü olduğu koddaki pakete bakın.</span><span class="sxs-lookup"><span data-stu-id="176fe-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="176fe-110">Başvuru yapıldıktan sonra, paketi API'si aracılığıyla arayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="176fe-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="176fe-111">**nuget.org ile başlayın**: nuget.org göz *atma* ,NET geliştiricilerin genellikle kendi uygulamalarında yeniden kullanabilecekleri bileşenleri nasıl bulduklarıdır.</span><span class="sxs-lookup"><span data-stu-id="176fe-111">**Start with nuget.org**: Browsing *nuget.org* is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="176fe-112">Bu makalede gösterildiği gibi *doğrudan nuget.org* arayabilir veya Visual Studio'daki paketleri bulabilir ve yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="176fe-112">You can search *nuget.org* directly or find and install packages within Visual Studio as shown in this article.</span></span> <span data-ttu-id="176fe-113">Genel bilgi için [NuGet paketlerini bul ve değerlendirin.](../consume-packages/finding-and-choosing-packages.md)</span><span class="sxs-lookup"><span data-stu-id="176fe-113">For general information, see [Find and evaluate NuGet packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="176fe-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="176fe-114">Prerequisites</span></span>

- <span data-ttu-id="176fe-115">.NET Masaüstü Geliştirme iş yükü ile Visual Studio 2019.</span><span class="sxs-lookup"><span data-stu-id="176fe-115">Visual Studio 2019 with the .NET Desktop Development workload.</span></span>

<span data-ttu-id="176fe-116">2019 Topluluk sürümünü [visualstudio.com](https://www.visualstudio.com/) ücretsiz olarak yükleyebilir veya Professional veya Enterprise sürümlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="176fe-116">You can install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="176fe-117">Mac için Visual Studio kullanıyorsanız, Visual Studio for Mac için [bir paket yükleyin ve kullanın.](install-and-use-a-package-in-visual-studio-mac.md)</span><span class="sxs-lookup"><span data-stu-id="176fe-117">If you're using Visual Studio for Mac, see [Install and use a package in Visual Studio for Mac](install-and-use-a-package-in-visual-studio-mac.md).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="176fe-118">Proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="176fe-118">Create a project</span></span>

<span data-ttu-id="176fe-119">NuGet paketleri, paketin projeyle aynı hedef çerçeveyi desteklemesi koşuluyla herhangi bir .NET projesine yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="176fe-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="176fe-120">Bu geçiş için basit bir WPF uygulaması kullanın.</span><span class="sxs-lookup"><span data-stu-id="176fe-120">For this walkthrough, use a simple WPF app.</span></span> <span data-ttu-id="176fe-121">**Visual** > Studio'da Dosya**Yeni Projesi'ni**kullanarak bir proje oluşturun, arama kutusuna **.NET** yazarak ve ardından **WPF Uygulamasını (.NET Framework)** seçerek.</span><span class="sxs-lookup"><span data-stu-id="176fe-121">Create a project in Visual Studio using **File** > **New Project**, typing **.NET** in the search box, and then selecting the **WPF App (.NET Framework)**.</span></span> <span data-ttu-id="176fe-122">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="176fe-122">Click **Next**.</span></span> <span data-ttu-id="176fe-123">İstendiğinde **Framework** için varsayılan değerleri kabul edin.</span><span class="sxs-lookup"><span data-stu-id="176fe-123">Accept the default values for **Framework** when prompted.</span></span>

<span data-ttu-id="176fe-124">Visual Studio, Solution Explorer'da açılan projeyi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="176fe-124">Visual Studio creates the project, which opens in Solution Explorer.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="176fe-125">Newtonsoft.Json NuGet paketini ekleyin</span><span class="sxs-lookup"><span data-stu-id="176fe-125">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="176fe-126">Paketi yüklemek için NuGet Paket Yöneticisi'ni veya Paket Yöneticisi Konsolu'nu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="176fe-126">To install the package, you can use either the NuGet Package Manager or the Package Manager Console.</span></span> <span data-ttu-id="176fe-127">Bir paket yüklediğinizde, NuGet bağımlılıkları proje dosyanıza `packages.config` veya dosyanızda kaydeder (proje biçimine bağlı olarak).</span><span class="sxs-lookup"><span data-stu-id="176fe-127">When you install a package, NuGet records the dependency in either your project file or a `packages.config` file (depending on the project format).</span></span> <span data-ttu-id="176fe-128">Daha fazla bilgi için [bkz: Paket tüketimine genel bakış ve iş akışı.](../consume-packages/Overview-and-Workflow.md)</span><span class="sxs-lookup"><span data-stu-id="176fe-128">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="nuget-package-manager"></a><span data-ttu-id="176fe-129">NuGet Paket Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="176fe-129">NuGet Package Manager</span></span>

1. <span data-ttu-id="176fe-130">Çözüm Gezgini'nde, **Başvurular'a** sağ tıklayın ve **NuGet Paketlerini Yönet'i**seçin.</span><span class="sxs-lookup"><span data-stu-id="176fe-130">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![Proje Başvuruları için NuGet Paketleri komutunu yönetme](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="176fe-132">**Paket kaynağı**olarak "nuget.org" seçeneğini belirleyin, **Gözat** sekmesini seçin, **Newtonsoft.Json'u**arayın, listedeki paketi seçin ve **Yükle'yi**seçin:</span><span class="sxs-lookup"><span data-stu-id="176fe-132">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Newtonsoft.Json paketinin bulunması](media/QS_Use-03-NewtonsoftJson.png)

    <span data-ttu-id="176fe-134">NuGet Paket Yöneticisi hakkında daha fazla bilgi istiyorsanız Visual [Studio'yu kullanarak paketleri yükle ve yönet'](../consume-packages/install-use-packages-visual-studio.md)e bakın.</span><span class="sxs-lookup"><span data-stu-id="176fe-134">If you want more information on the NuGet Package Manager, see [Install and manage packages using Visual Studio](../consume-packages/install-use-packages-visual-studio.md).</span></span>

1. <span data-ttu-id="176fe-135">Herhangi bir lisans istemlerini kabul edin.</span><span class="sxs-lookup"><span data-stu-id="176fe-135">Accept any license prompts.</span></span>

1. <span data-ttu-id="176fe-136">(Sadece Visual Studio 2017) Paket yönetim biçimi seçmek istenirse, **proje dosyasında PackageReference'ı**seçin:</span><span class="sxs-lookup"><span data-stu-id="176fe-136">(Visual Studio 2017 only) If prompted to select a package management format, select **PackageReference in project file**:</span></span>

    ![Paket yönetim biçimi seçme](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="176fe-138">Değişiklikleri gözden geçirmek istenirse, **Tamam'ı**seçin.</span><span class="sxs-lookup"><span data-stu-id="176fe-138">If prompted to review changes, select **OK**.</span></span>

### <a name="package-manager-console"></a><span data-ttu-id="176fe-139">Paket Yöneticisi Konsolu</span><span class="sxs-lookup"><span data-stu-id="176fe-139">Package Manager Console</span></span>

1. <span data-ttu-id="176fe-140">**Araçlar** > **NuGet Paket Yöneticisi** > **Paket Yöneticisi Konsol** menü komutunu seçin.</span><span class="sxs-lookup"><span data-stu-id="176fe-140">Select the **Tools** > **NuGet Package Manager** > **Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="176fe-141">Konsol açıldıktan sonra, **Varsayılan proje** açılır listesinin paketi yüklemek istediğiniz projeyi gösterip gösterdiğini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="176fe-141">Once the console opens, check that the **Default project** drop-down list shows the project into which you want to install the package.</span></span> <span data-ttu-id="176fe-142">Çözümde tek bir proje varsa, zaten seçilir.</span><span class="sxs-lookup"><span data-stu-id="176fe-142">If you have a single project in the solution, it is already selected.</span></span>

    ![Newtonsoft.Json paketinin bulunması](media/QS_Use-08-Console1.png)

1. <span data-ttu-id="176fe-144">Komutu `Install-Package Newtonsoft.Json` girin (bkz. [Yükle-Paket](../reference/ps-reference/ps-ref-install-package.md)).</span><span class="sxs-lookup"><span data-stu-id="176fe-144">Enter the command `Install-Package Newtonsoft.Json` (see [Install-Package](../reference/ps-reference/ps-ref-install-package.md)).</span></span> <span data-ttu-id="176fe-145">Konsol penceresi komut için çıktı gösterir.</span><span class="sxs-lookup"><span data-stu-id="176fe-145">The console window shows output for the command.</span></span> <span data-ttu-id="176fe-146">Hatalar genellikle paketin projenin hedef çerçevesiyle uyumlu olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="176fe-146">Errors typically indicate that the package isn't compatible with the project's target framework.</span></span>

   <span data-ttu-id="176fe-147">Paket Yöneticisi Konsolu hakkında daha fazla bilgi istiyorsanız, [Paket Yöneticisi Konsolu'nu kullanarak paketleri yükle ve yönet'](../consume-packages/install-use-packages-powershell.md)e bakın.</span><span class="sxs-lookup"><span data-stu-id="176fe-147">If you want more information on the Package Manager Console, see [Install and manage packages using Package Manager Console](../consume-packages/install-use-packages-powershell.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="176fe-148">Uygulamada Newtonsoft.Json API'yi kullanın</span><span class="sxs-lookup"><span data-stu-id="176fe-148">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="176fe-149">Projedeki Newtonsoft.Json paketi yle, bir `JsonConvert.SerializeObject` nesneyi insan tarafından okunabilir bir dize dönüştürme yöntemini arayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="176fe-149">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="176fe-150">Varolan `MainWindow.xaml` `Grid` öğeyi aşağıdakilerle açın ve değiştirin:</span><span class="sxs-lookup"><span data-stu-id="176fe-150">Open `MainWindow.xaml` and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="White">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Width="100px" HorizontalAlignment="Center" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" HorizontalAlignment="Center" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="176fe-151">Dosyayı `MainWindow.xaml.cs` açın (düğüm altında `MainWindow.xaml` Çözüm Gezgini'nde bulunan) ve `MainWindow` sınıfın içine aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="176fe-151">Open the `MainWindow.xaml.cs` file (located in Solution Explorer under the `MainWindow.xaml` node), and insert the following code inside the `MainWindow` class:</span></span>

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

1. <span data-ttu-id="176fe-152">Newtonsoft.Json paketini projeye eklemiş olsanız bile, kod dosyasının üst `using` kısmında bir ifadeye ihtiyacınız olduğundan kırmızı dalgalı lar altında `JsonConvert` görünür:</span><span class="sxs-lookup"><span data-stu-id="176fe-152">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement at the top of the code file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="176fe-153">F5 tuşuna basarak veya **Hata Ayıklama** > **Başlatma Hata Ayıklama'yı**seçerek uygulamayı oluşturun ve çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="176fe-153">Build and run the app by pressing F5 or selecting **Debug** > **Start Debugging**:</span></span>

    ![WPF uygulamasının ilk çıktısı](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="176fe-155">TextBlock'un içeriğinin bazı JSON metinleri ile değiştirilmesini görmek için düğmeyi seçin:</span><span class="sxs-lookup"><span data-stu-id="176fe-155">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![Düğmeyi seçtikten sonra WPF uygulamasının çıktısı](media/QS_Use-07-AppEnd.png)

## <a name="related-video"></a><span data-ttu-id="176fe-157">İlgili video</span><span class="sxs-lookup"><span data-stu-id="176fe-157">Related video</span></span>

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-Visual-Studio-2-of-5/player]

<span data-ttu-id="176fe-158">[Kanal 9](https://channel9.msdn.com/Series/NuGet-101) ve [YouTube'da](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_)daha fazla NuGet videosu bulun.</span><span class="sxs-lookup"><span data-stu-id="176fe-158">Find more NuGet videos on [Channel 9](https://channel9.msdn.com/Series/NuGet-101) and [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span></span>

## <a name="next-steps"></a><span data-ttu-id="176fe-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="176fe-159">Next steps</span></span>

<span data-ttu-id="176fe-160">İlk NuGet paketinizi yükledikten ve kullandığınız için tebrikler!</span><span class="sxs-lookup"><span data-stu-id="176fe-160">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="176fe-161">Visual Studio'u kullanarak paketleri yükleyin ve yönetin</span><span class="sxs-lookup"><span data-stu-id="176fe-161">Install and manage packages using Visual Studio</span></span>](../consume-packages/install-use-packages-visual-studio.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="176fe-162">Paket Yöneticisi Konsolu'nu kullanarak paketleri yükleme ve yönetme</span><span class="sxs-lookup"><span data-stu-id="176fe-162">Install and manage packages using Package Manager Console</span></span>](../consume-packages/install-use-packages-powershell.md)

<span data-ttu-id="176fe-163">NuGet'in sunduğu daha fazlasını keşfetmek için aşağıdaki bağlantıları seçin.</span><span class="sxs-lookup"><span data-stu-id="176fe-163">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="176fe-164">Paket tüketimine genel bakış ve iş akışı</span><span class="sxs-lookup"><span data-stu-id="176fe-164">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="176fe-165">Paketleri bulma ve seçme</span><span class="sxs-lookup"><span data-stu-id="176fe-165">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="176fe-166">Proje dosyalarında paket başvuruları</span><span class="sxs-lookup"><span data-stu-id="176fe-166">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
