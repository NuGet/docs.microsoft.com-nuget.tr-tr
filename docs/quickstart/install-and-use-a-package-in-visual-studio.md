---
title: Visual Studio'da NuGet paketleri kullanmaya tanıtım Kılavuzu
description: Yükleme ve bir NuGet paketi kullanarak bir Visual Studio projesinde işlemini bir gözden geçirme öğretici.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 8cfb7bd31c37847d83ffe31f11ba61eadc717eb8
ms.sourcegitcommit: b8c63744252a5a37a2843f6bc1d5917496ee40dd
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812898"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio"></a><span data-ttu-id="2b713-103">Hızlı Başlangıç: Yükleme ve Visual Studio'da paket kullanma</span><span class="sxs-lookup"><span data-stu-id="2b713-103">Quickstart: Install and use a package in Visual Studio</span></span>

<span data-ttu-id="2b713-104">NuGet paketleri diğer geliştiriciler projelerinizde kullanmak için kullanılabilir hale yeniden kullanılabilir bir kod içerir.</span><span class="sxs-lookup"><span data-stu-id="2b713-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="2b713-105">Bkz: [NuGet nedir?](../What-is-NuGet.md) arka planı.</span><span class="sxs-lookup"><span data-stu-id="2b713-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="2b713-106">Paket Yöneticisi UI veya Paket Yöneticisi konsolunu kullanarak bir Visual Studio projesine paketleri yüklenir.</span><span class="sxs-lookup"><span data-stu-id="2b713-106">Packages are installed into a Visual Studio project using the Package Manager UI or the Package Manager Console.</span></span> <span data-ttu-id="2b713-107">Bu makalede, popüler kullanma işlemi gösterilmektedir. [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) paket ve evrensel Windows Platformu (UWP) projesi.</span><span class="sxs-lookup"><span data-stu-id="2b713-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a Universal Windows Platform (UWP) project.</span></span> <span data-ttu-id="2b713-108">Aynı işlem, diğer tüm .NET veya .NET Core projeleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="2b713-108">The same process applies to any other .NET or .NET Core project.</span></span>

<span data-ttu-id="2b713-109">Kod ile paket yüklendikten sonra başvurmak `using <namespace>` burada \<ad alanı\> kullanmakta olduğunuz paket özgüdür.</span><span class="sxs-lookup"><span data-stu-id="2b713-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="2b713-110">Başvuru yaptıktan sonra paketi API'si aracılığıyla çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2b713-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="2b713-111">**Nuget.org ile Başlat**: Gözatma nuget.org'nin olduğundan nasıl .NET geliştiricilerinin bileşenler genellikle bulun, kendi uygulamalarında yeniden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2b713-111">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="2b713-112">Nuget.org doğrudan arama veya bulabilir ve bu makalede gösterilen şekilde Visual Studio içindeki paketleri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2b713-112">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b713-113">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="2b713-113">Prerequisites</span></span>

- <span data-ttu-id="2b713-114">Evrensel Windows platformu geliştirme iş yüküyle Visual Studio 2017 veya</span><span class="sxs-lookup"><span data-stu-id="2b713-114">Visual Studio 2017 with the Universal Windows Platform development workload, or</span></span>
- <span data-ttu-id="2b713-115">Visual Studio 2015 güncelleştirme 3 ile Evrensel Windows uygulamaları için Araçlar.</span><span class="sxs-lookup"><span data-stu-id="2b713-115">Visual Studio 2015 Update 3 with Tools for Universal Windows Apps.</span></span>

<span data-ttu-id="2b713-116">2017 Community edition ücretsiz nden yüklenebilecek [visualstudio.com](https://www.visualstudio.com/) veya Professional veya Enterprise Edition'ı kullanın.</span><span class="sxs-lookup"><span data-stu-id="2b713-116">You can install the 2017 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="2b713-117">Mac için Visual Studio kullanıyorsanız, bkz. [NuGet paketini projenize dahil](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="2b713-117">If you're using Visual Studio for Mac, see [Include a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="2b713-118">Proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="2b713-118">Create a project</span></span>

<span data-ttu-id="2b713-119">Paket projesi olarak aynı hedef Framework'ü destekliyorsa, NuGet paketlerini herhangi bir .NET projesine yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="2b713-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="2b713-120">Bu kılavuz için basit bir evrensel Windows (UWP) uygulamasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="2b713-120">For this walkthrough, use a simple Universal Windows (UWP) app.</span></span> <span data-ttu-id="2b713-121">Visual Studio kullanarak bir proje oluşturun **Dosya > Yeni proje...**  seçerek **Windows Evrensel > boş uygulama (Evrensel Windows)** .</span><span class="sxs-lookup"><span data-stu-id="2b713-121">Create a project in Visual Studio using **File > New Project...** and selecting the **Windows Universal > Blank App (Universal Windows)**.</span></span> <span data-ttu-id="2b713-122">Hedef sürümü ve en düşük istendiğinde sürümü için varsayılan değerleri kabul.</span><span class="sxs-lookup"><span data-stu-id="2b713-122">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="2b713-123">Newtonsoft.Json NuGet paketi ekleme</span><span class="sxs-lookup"><span data-stu-id="2b713-123">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="2b713-124">Paketi yüklemek için Paket Yöneticisi kullanıcı Arabirimi veya Paket Yöneticisi konsolu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2b713-124">To install the package, you can use either the Package Manager UI or the Package Manager Console.</span></span> <span data-ttu-id="2b713-125">Bir paketi yüklediğinizde, NuGet bağımlılık ya da proje dosyanız kaydeder veya `packages.config` dosya.</span><span class="sxs-lookup"><span data-stu-id="2b713-125">When you install a package, NuGet records the dependency in either your project file or a `packages.config` file.</span></span> <span data-ttu-id="2b713-126">Daha fazla bilgi için [paket tüketim genel bakış ve iş akışı](../consume-packages/Overview-and-Workflow.md).</span><span class="sxs-lookup"><span data-stu-id="2b713-126">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="package-manager-ui"></a><span data-ttu-id="2b713-127">Paket Yöneticisi UI</span><span class="sxs-lookup"><span data-stu-id="2b713-127">Package Manager UI</span></span>

1. <span data-ttu-id="2b713-128">Çözüm Gezgini'nde sağ **başvuruları** ve **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="2b713-128">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![NuGet paketlerini komutu için proje başvurularını yönetme](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="2b713-130">"Nuget.org" olarak seçin **paket kaynağı**seçin **Gözat** sekmesinde, arama **Newtonsoft.Json**, bu paket listesinde seçip  **Yükleme**:</span><span class="sxs-lookup"><span data-stu-id="2b713-130">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Newtonsoft.Json paketini bulma](media/QS_Use-03-NewtonsoftJson.png)

1. <span data-ttu-id="2b713-132">Herhangi bir lisans istemi kabul edin.</span><span class="sxs-lookup"><span data-stu-id="2b713-132">Accept any license prompts.</span></span>

1. <span data-ttu-id="2b713-133">(Visual Studio 2017) Paket Yönetimi biçimi seçin istenirse seçin **packagereference v souboru projektu**:</span><span class="sxs-lookup"><span data-stu-id="2b713-133">(Visual Studio 2017) If prompted to select a package management format, select **PackageReference in project file**:</span></span>

    ![Paket Yönetimi biçimini seçme](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="2b713-135">Değişiklikleri gözden geçirmek için istenirse seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="2b713-135">If prompted to review changes, select **OK**.</span></span>

### <a name="package-manager-console"></a><span data-ttu-id="2b713-136">Paket Yöneticisi Konsolu</span><span class="sxs-lookup"><span data-stu-id="2b713-136">Package Manager Console</span></span>

1. <span data-ttu-id="2b713-137">Seçin **Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Konsolu** menü komutu.</span><span class="sxs-lookup"><span data-stu-id="2b713-137">Select the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="2b713-138">Konsol açıldıktan sonra bu maddeyi **varsayılan proje** aşağı açılan listesinde istediğiniz paketi yüklemek projeyi gösterir.</span><span class="sxs-lookup"><span data-stu-id="2b713-138">Once the console opens, check that the **Default project** drop-down list shows the project into which you want to install the package.</span></span> <span data-ttu-id="2b713-139">Tek bir proje çözümde varsa, bu zaten seçilir.</span><span class="sxs-lookup"><span data-stu-id="2b713-139">If you have a single project in the solution, it is already selected.</span></span>

    ![Newtonsoft.Json paketini bulma](media/QS_Use-08-Console1.png)

1. <span data-ttu-id="2b713-141">Komutu girdikten `Install-Package Newtonsoft.Json` (bkz [Install-Package](../tools/ps-ref-install-package.md)).</span><span class="sxs-lookup"><span data-stu-id="2b713-141">Enter the command `Install-Package Newtonsoft.Json` (see [Install-Package](../tools/ps-ref-install-package.md)).</span></span> <span data-ttu-id="2b713-142">Konsol penceresinde komutunun çıktısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="2b713-142">The console window shows output for the command.</span></span> <span data-ttu-id="2b713-143">Hatalar genellikle paket projenin hedef çerçevesi ile uyumlu olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="2b713-143">Errors typically indicate that the package isn't compatible with the project's target framework.</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="2b713-144">' % S ' Newtonsoft.Json API uygulamasında kullanma</span><span class="sxs-lookup"><span data-stu-id="2b713-144">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="2b713-145">Projesinde Newtonsoft.Json paketiyle çağırabilirsiniz kendi `JsonConvert.SerializeObject` bir nesneyi bir kullanıcı tarafından okunabilen bir dizeye dönüştürmek için yöntemi.</span><span class="sxs-lookup"><span data-stu-id="2b713-145">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="2b713-146">Açık `MainPage.xaml` ve varolan `Grid` aşağıdaki öğe:</span><span class="sxs-lookup"><span data-stu-id="2b713-146">Open `MainPage.xaml` and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="2b713-147">Açık `MainPage.xaml.cs` dosyası (altında Çözüm Gezgini'nde bulunan `MainPage.xaml` düğümü) ve içine aşağıdaki kodu ekleyin `MainPage` Oluşturucusu:</span><span class="sxs-lookup"><span data-stu-id="2b713-147">Open the `MainPage.xaml.cs` file (located in Solution Explorer under the `MainPage.xaml` node), and insert the following code inside the `MainPage` constructor:</span></span>

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

1. <span data-ttu-id="2b713-148">Newtonsoft.Json paketini projeye eklenen olsa da, kırmızı dalgalı çizgiler altında görünür `JsonConvert` ihtiyacınız olduğundan bir `using` kod dosyasının üst deyimi:</span><span class="sxs-lookup"><span data-stu-id="2b713-148">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement at the top of the code file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="2b713-149">F5 tuşuna basarak veya seçerek uygulaması derleyebilir ve **hata ayıklama > hata ayıklamayı Başlat**:</span><span class="sxs-lookup"><span data-stu-id="2b713-149">Build and run the app by pressing F5 or selecting **Debug > Start Debugging**:</span></span>

    ![UWP uygulamasının ilk çıkış](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="2b713-151">İle bazı JSON metnin yerine geçen TextBlock içeriğini görmek için düğmesini seçin:</span><span class="sxs-lookup"><span data-stu-id="2b713-151">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![Çıkış düğmesi seçildikten sonra UWP uygulaması](media/QS_Use-07-AppEnd.png)

## <a name="related-articles"></a><span data-ttu-id="2b713-153">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="2b713-153">Related articles</span></span>

- [<span data-ttu-id="2b713-154">Genel bakış ve paket tüketim iş akışı</span><span class="sxs-lookup"><span data-stu-id="2b713-154">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="2b713-155">Paketleri bulma ve seçme</span><span class="sxs-lookup"><span data-stu-id="2b713-155">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="2b713-156">Paket yükleme yolu</span><span class="sxs-lookup"><span data-stu-id="2b713-156">Ways to install a package</span></span>](../consume-packages/ways-to-install-a-package.md)
- [<span data-ttu-id="2b713-157">NuGet Davranışını Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2b713-157">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
