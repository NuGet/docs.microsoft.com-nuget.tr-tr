---
title: Visual Studio içinde NuGet paketi kullanarak tanıtım Kılavuzu | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: quickstart
ms.prod: nuget
ms.technology: ''
description: İzlenecek yol öğretici yükleme ve bir NuGet paketi kullanarak bir Visual Studio projesi işleme.
keywords: NuGet paketlerini kullanarak NuGet paketleri, NuGet paket referanslarını yükleme NuGet, NuGet paketi tüketim yükleyin
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 4205893cc02cffff8926513a555393d10c046f43
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="install-and-use-a-package-in-visual-studio"></a><span data-ttu-id="66657-104">Yükleyin ve Visual Studio'da bir paket kullanın</span><span class="sxs-lookup"><span data-stu-id="66657-104">Install and use a package in Visual Studio</span></span>

<span data-ttu-id="66657-105">NuGet paketleri diğer geliştiriciler projelerinizi kullanmak için kullanılabilir hale yeniden kullanılabilir kod içerir.</span><span class="sxs-lookup"><span data-stu-id="66657-105">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="66657-106">Bkz: [NuGet nedir?](../What-is-NuGet.md) arka planı için.</span><span class="sxs-lookup"><span data-stu-id="66657-106">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="66657-107">Paketler, Paket Yöneticisi kullanıcı Arabirimi veya Paket Yöneticisi konsolu kullanarak bir Visual Studio projesi yüklenir.</span><span class="sxs-lookup"><span data-stu-id="66657-107">Packages are installed into a Visual Studio project using the Package Manager UI or the Package Manager Console.</span></span> <span data-ttu-id="66657-108">Bu makalede, popüler kullanma işlemi gösterilmektedir [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) paket ve bir evrensel Windows Platformu (UWP) projesi.</span><span class="sxs-lookup"><span data-stu-id="66657-108">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a Universal Windows Platform (UWP) project.</span></span> <span data-ttu-id="66657-109">Aynı işlemde herhangi diğer .NET veya .NET Core proje için de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="66657-109">The same process applies to any other .NET or .NET Core project.</span></span>

<span data-ttu-id="66657-110">Koduyla paketinde yüklendikten sonra başvurmak `using <namespace>` nerede \<ad alanı\> kullanmakta olduğunuz paket özeldir.</span><span class="sxs-lookup"><span data-stu-id="66657-110">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="66657-111">Başvuru yapıldığında, kendi API aracılığıyla paket çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66657-111">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="66657-112">**Başlat nuget.org ile**: Tarama nuget.org olan nasıl .NET geliştiricilerinin bileşenleri genellikle bulmak, kendi uygulamalarında yeniden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66657-112">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="66657-113">Nuget.org doğrudan arama veya bulabilir ve bu makalede gösterilen şekilde Visual Studio içindeki paketleri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="66657-113">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66657-114">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="66657-114">Prerequisites</span></span>

- <span data-ttu-id="66657-115">Evrensel Windows platformu geliştirme iş yükü ile Visual Studio 2017 veya</span><span class="sxs-lookup"><span data-stu-id="66657-115">Visual Studio 2017 with the Universal Windows Platform development workload, or</span></span>
- <span data-ttu-id="66657-116">Visual Studio 2015 güncelleştirme 3 Evrensel Windows uygulamaları için Araçlar ile.</span><span class="sxs-lookup"><span data-stu-id="66657-116">Visual Studio 2015 Update 3 with Tools for Universal Windows Apps.</span></span>

<span data-ttu-id="66657-117">2017 Community edition ücretsiz nden yüklenebilecek [visualstudio.com](https://www.visualstudio.com/) ya da Professional veya Enterprise sürümü kullanın.</span><span class="sxs-lookup"><span data-stu-id="66657-117">You can install the 2017 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="66657-118">Proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="66657-118">Create a project</span></span>

<span data-ttu-id="66657-119">Aynı hedef framework projesi olarak paket desteklediğini varsayarak NuGet paketlerini herhangi .NET projeye yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="66657-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="66657-120">Bu kılavuz için basit bir evrensel Windows (UWP) uygulamasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="66657-120">For this walkthrough, use a simple Universal Windows (UWP) app.</span></span> <span data-ttu-id="66657-121">Visual Studio kullanarak bir proje oluşturun. **Dosya > Yeni proje...**  ve seçerek **Windows Evrensel > boş uygulama (Evrensel Windows)**.</span><span class="sxs-lookup"><span data-stu-id="66657-121">Create a project in Visual Studio using **File > New Project...** and selecting the **Windows Universal > Blank App (Universal Windows)**.</span></span> <span data-ttu-id="66657-122">Hedef sürüm ve Minimum istendiğinde sürüm için varsayılan değerleri kabul.</span><span class="sxs-lookup"><span data-stu-id="66657-122">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="66657-123">Newtonsoft.Json NuGet paketi ekleme</span><span class="sxs-lookup"><span data-stu-id="66657-123">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="66657-124">Paketi yüklemek için Paket Yöneticisi kullanıcı Arabirimi veya Paket Yöneticisi konsolu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66657-124">To install the package, you can use either the Package Manager UI or the Package Manager Console.</span></span> <span data-ttu-id="66657-125">Bir paketi yüklediğinizde, NuGet bağımlılık ya da proje dosyanızı kaydeder veya `packages.config` dosyası.</span><span class="sxs-lookup"><span data-stu-id="66657-125">When you install a package, NuGet records the dependency in either your project file or a `packages.config` file.</span></span> <span data-ttu-id="66657-126">Daha fazla bilgi için bkz: [paket tüketimi genel bakış ve iş akışı](../consume-packages/Overview-and-Workflow.md).</span><span class="sxs-lookup"><span data-stu-id="66657-126">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="package-manager-ui"></a><span data-ttu-id="66657-127">Paket Yöneticisi kullanıcı Arabirimi</span><span class="sxs-lookup"><span data-stu-id="66657-127">Package Manager UI</span></span>

1. <span data-ttu-id="66657-128">Çözüm Gezgini'nde sağ **başvuruları** ve **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="66657-128">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![NuGet paketlerini komutu için proje başvuruları yönetme](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="66657-130">"Nuget.org" olarak seçin **paket kaynağı**seçin **Gözat** sekmesinde, arama **Newtonsoft.Json**, listesinde o paketi seçin ve seçin  **Yükleme**:</span><span class="sxs-lookup"><span data-stu-id="66657-130">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Newtonsoft.Json paket bulma](media/QS_Use-03-NewtonsoftJson.png)

1. <span data-ttu-id="66657-132">Lisans sizden kabul edin.</span><span class="sxs-lookup"><span data-stu-id="66657-132">Accept any license prompts.</span></span>

1. <span data-ttu-id="66657-133">(Visual Studio 2017) Paket Yönetimi biçimi seçin isteyip istemediğiniz sorulduğunda seçin **PackageReference proje dosyasında**:</span><span class="sxs-lookup"><span data-stu-id="66657-133">(Visual Studio 2017) If prompted to select a package management format, select **PackageReference in project file**:</span></span>

    ![Paket Yönetimi biçimi seçme](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="66657-135">Değişiklikleri gözden geçirmek için istenirse seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="66657-135">If prompted to review changes, select **OK**.</span></span>

### <a name="package-manager-console"></a><span data-ttu-id="66657-136">Paket Yöneticisi Konsolu</span><span class="sxs-lookup"><span data-stu-id="66657-136">Package Manager Console</span></span>

1. <span data-ttu-id="66657-137">Seçin **Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Konsolu** menü komutu.</span><span class="sxs-lookup"><span data-stu-id="66657-137">Select the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="66657-138">İçin konsolu açar sonra denetleyin **varsayılan proje** aşağı açılan liste içine paket yüklemek istediğiniz proje gösterir.</span><span class="sxs-lookup"><span data-stu-id="66657-138">Once the console opens, check that the **Default project** drop-down list shows the project into which you want to install the package.</span></span> <span data-ttu-id="66657-139">Tek bir proje çözümde varsa, zaten seçilidir.</span><span class="sxs-lookup"><span data-stu-id="66657-139">If you have a single project in the solution, it is already selected.</span></span>

    ![Newtonsoft.Json paket bulma](media/QS_Use-08-Console1.png)

1. <span data-ttu-id="66657-141">Aşağıdaki komutu girin `Install-Package Newtonsoft.json` (bkz [Install-Package](../tools/ps-ref-install-package.md)).</span><span class="sxs-lookup"><span data-stu-id="66657-141">Enter the command `Install-Package Newtonsoft.json` (see [Install-Package](../tools/ps-ref-install-package.md)).</span></span> <span data-ttu-id="66657-142">Konsol penceresinde komutunun çıktısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="66657-142">The console window shows output for the command.</span></span> <span data-ttu-id="66657-143">Hatalar genellikle paket projenin hedef çerçevesi ile uyumlu değil işaret eder.</span><span class="sxs-lookup"><span data-stu-id="66657-143">Errors typically indicate that the package isn't compatible with the project's target framework.</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="66657-144">' % S ' Newtonsoft.Json API uygulamasında kullanma</span><span class="sxs-lookup"><span data-stu-id="66657-144">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="66657-145">Projedeki Newtonsoft.Json paketiyle çağırabilirsiniz kendi `JsonConvert.SerializeObject` bir nesne okunabilir bir dizeye dönüştürmek için yöntem.</span><span class="sxs-lookup"><span data-stu-id="66657-145">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="66657-146">Açık `MainPage.xaml` ve varolan `Grid` aşağıdaki öğeyle:</span><span class="sxs-lookup"><span data-stu-id="66657-146">Open `MainPage.xaml` and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="66657-147">Açık `MainPage.xaml.cs` dosyası (Çözüm Gezgini altında bulunan `MainPage.xaml` düğüm) ve aşağıdaki kodu ekleyin `MainPage` Oluşturucusu:</span><span class="sxs-lookup"><span data-stu-id="66657-147">Open the `MainPage.xaml.cs` file (located in Solution Explorer under the `MainPage.xaml` node), and insert the following code inside the `MainPage` constructor:</span></span>

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

1. <span data-ttu-id="66657-148">Newtonsoft.Json paketini projeye eklenen olsa da, kırmızı dalgalı çizgiler altında görünür `JsonConvert` , gerektiğinden bir `using` kod dosyasının üst deyimi:</span><span class="sxs-lookup"><span data-stu-id="66657-148">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement at the top of the code file:</span></span>

    ```cs
    using Newtonsoft.json;
    ```

1. <span data-ttu-id="66657-149">Derleme ve F5 tuşuna basarak veya seçerek uygulamayı çalıştırma **hata ayıklama > hata ayıklamayı Başlat**:</span><span class="sxs-lookup"><span data-stu-id="66657-149">Build and run the app by pressing F5 or selecting **Debug > Start Debugging**:</span></span>

    ![UWP uygulaması ilk çıktısı](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="66657-151">İle bazı JSON metnin yerine TextBlock içeriğini görmek için düğmeyi seçin:</span><span class="sxs-lookup"><span data-stu-id="66657-151">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![Düğme seçtikten sonra UWP uygulamasında çıktısı](media/QS_Use-07-AppEnd.png)

## <a name="related-articles"></a><span data-ttu-id="66657-153">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="66657-153">Related articles</span></span>

- [<span data-ttu-id="66657-154">Genel bakış ve iş akışı paket tüketimi</span><span class="sxs-lookup"><span data-stu-id="66657-154">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="66657-155">Paketleri bulma ve seçme</span><span class="sxs-lookup"><span data-stu-id="66657-155">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="66657-156">Bir paketi yüklemek için yollar</span><span class="sxs-lookup"><span data-stu-id="66657-156">Ways to install a package</span></span>](../consume-packages/ways-to-install-a-package.md)
- [<span data-ttu-id="66657-157">NuGet Davranışını Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="66657-157">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
