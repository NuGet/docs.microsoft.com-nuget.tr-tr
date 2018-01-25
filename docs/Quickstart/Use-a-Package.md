---
title: "NuGet paketlerini kullanarak tanıtım Kılavuzu | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/04/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Yükleme ve bir NuGet paketi projede kullanma sürecini bir gözden geçirme öğretici."
keywords: "NuGet paketlerini kullanarak NuGet paketleri, NuGet paket referanslarını yükleme NuGet, NuGet paketi tüketim yükleyin"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 897419d1e49f12d54fbb996a2462e06e32933e65
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2018
---
# <a name="install-and-use-a-package"></a><span data-ttu-id="b6083-104">Yükleme ve bir paket kullanma</span><span class="sxs-lookup"><span data-stu-id="b6083-104">Install and use a package</span></span>

<span data-ttu-id="b6083-105">NuGet paketleri diğer geliştiriciler projelerinizi kullanmak için kullanılabilir hale yeniden kullanılabilir kod birimleridir.</span><span class="sxs-lookup"><span data-stu-id="b6083-105">NuGet packages are units of reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="b6083-106">Bkz: [NuGet nedir?](../What-is-NuGet.md) arka planı için.</span><span class="sxs-lookup"><span data-stu-id="b6083-106">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span>

[!INCLUDE [install-methods](../includes/install-methods.md)]

<span data-ttu-id="b6083-107">Koduyla paketinde yüklendikten sonra başvurmak `using <namespace>` nerede \<ad alanı\> kullanmakta olduğunuz paket özeldir.</span><span class="sxs-lookup"><span data-stu-id="b6083-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="b6083-108">Başvuru yapıldığında, kendi API aracılığıyla paket çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6083-108">Once the reference is made, you can call the package through its API.</span></span>

<span data-ttu-id="b6083-109">Bu konunun geri kalanında popüler yüklemek için Paket Yöneticisi kullanıcı arabirimini kullanarak sürecinde yardımcı olur [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) bir evrensel Windows Platformu (UWP) proje paketinde.</span><span class="sxs-lookup"><span data-stu-id="b6083-109">The remainder of this topic walks through the process of using the Package Manager UI to install the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package in a Universal Windows Platform (UWP) project.</span></span> <span data-ttu-id="b6083-110">Ardından, paketi kullanarak bir örnek gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b6083-110">It then shows an example of using the package.</span></span> <span data-ttu-id="b6083-111">Benzer bir iş akışı için diğer NuGet paketlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="b6083-111">You use a similar workflow for other NuGet packages.</span></span>

- [<span data-ttu-id="b6083-112">Önkoşulları yüklemek</span><span class="sxs-lookup"><span data-stu-id="b6083-112">Install pre-requisites</span></span>](#install-pre-requisites)
- [<span data-ttu-id="b6083-113">Proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="b6083-113">Create a project</span></span>](#create-a-project)
- [<span data-ttu-id="b6083-114">Newtonsoft.Json NuGet paketi ekleme</span><span class="sxs-lookup"><span data-stu-id="b6083-114">Add the Newtonsoft.Json NuGet package</span></span>](#add-the-newtonsoftjson-nuget-package)
- [<span data-ttu-id="b6083-115">' % S ' Newtonsoft.Json API uygulamasında kullanma</span><span class="sxs-lookup"><span data-stu-id="b6083-115">Use the Newtonsoft.Json API in the app</span></span>](#use-the-newtonsoftjson-api-in-the-app)

> [!Tip]
> <span data-ttu-id="b6083-116">**Başlat nuget.org ile**: nuget.org paket yükleme olan kendi uygulamalarında kullanabilecekleri bileşenleri bulmak için .NET geliştiricilerinin kullanan ortak bir iş akışı.</span><span class="sxs-lookup"><span data-stu-id="b6083-116">**Start with nuget.org**: Installing packages from nuget.org is a common workflow that .NET developers use to find components they can use in their own applications.</span></span> <span data-ttu-id="b6083-117">Her zaman nuget.org doğrudan arama ya da bulmak ve bu konu başlığı altında gösterildiği gibi Visual Studio içindeki paketleri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b6083-117">You can always search nuget.org directly or find and install packages within Visual Studio as shown in this topic.</span></span>

## <a name="install-pre-requisites"></a><span data-ttu-id="b6083-118">Önkoşulları yüklemek</span><span class="sxs-lookup"><span data-stu-id="b6083-118">Install pre-requisites</span></span>

<span data-ttu-id="b6083-119">Bu öğretici araçları ile Visual Studio 2015 güncelleştirme 3, Evrensel Windows uygulamaları ya da Visual Studio 2017 için evrensel Windows platformu geliştirme yüküyle gerektirir.</span><span class="sxs-lookup"><span data-stu-id="b6083-119">This tutorial requires Visual Studio 2015 Update 3 with Tools for Universal Windows Apps, or Visual Studio 2017 with the Universal Windows Platform development workload.</span></span> <span data-ttu-id="b6083-120">Visual Studio zaten yüklüyse, UWP araçları tekrar eklemeyi yükleyici çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6083-120">If you already have Visual Studio installed, you can run the installer again to add the UWP tools.</span></span>

<span data-ttu-id="b6083-121">Community edition ücretsiz nden yüklenebilecek [visualstudio.com](https://www.visualstudio.com/) ya da Professional veya Enterprise sürümü kullanın.</span><span class="sxs-lookup"><span data-stu-id="b6083-121">You can install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span> 

## <a name="create-a-project"></a><span data-ttu-id="b6083-122">Proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="b6083-122">Create a project</span></span>

<span data-ttu-id="b6083-123">Bir NuGet paketi yüklemek için bazı tür gerekir. Visual Studio'da NET tabanlı projesi.</span><span class="sxs-lookup"><span data-stu-id="b6083-123">To install a NuGet package, you need some kind of .NET-based project in Visual Studio.</span></span> <span data-ttu-id="b6083-124">Bu kılavuz için kullanabileceğiniz basit bir Windows Presentation Foundation (WPF) veya evrensel Windows (UWP) uygulamasını kullanın:</span><span class="sxs-lookup"><span data-stu-id="b6083-124">For this walkthrough, you can use use a simple Windows Presentation Foundation (WPF) or Universal Windows (UWP) app:</span></span>

- <span data-ttu-id="b6083-125">WPF (Windows 7 +) seçin **Dosya > Yeni > Proje**, genişletin **Visual C#**seçin **Windows Klasik Masaüstü > WPF uygulaması (.NET Framework)**, seçip**Tamam**.</span><span class="sxs-lookup"><span data-stu-id="b6083-125">For WPF (Windows 7+), choose **File > New > Project**, expand **Visual C#**, select **Windows Classic Desktop > WPF App (.NET Framework)**, and select **OK**.</span></span>
- <span data-ttu-id="b6083-126">UWP (Windows 10) kullanma **Windows Evrensel > boş uygulama (Evrensel Windows)** yerine.</span><span class="sxs-lookup"><span data-stu-id="b6083-126">For UWP (Windows 10), use the **Windows Universal > Blank App (Universal Windows)** instead.</span></span> <span data-ttu-id="b6083-127">Hedef sürüm ve Minimum istendiğinde sürüm için varsayılan değerleri kabul.</span><span class="sxs-lookup"><span data-stu-id="b6083-127">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="b6083-128">Newtonsoft.Json NuGet paketi ekleme</span><span class="sxs-lookup"><span data-stu-id="b6083-128">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="b6083-129">Çözüm Gezgini'nde sağ **başvuruları** ve **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="b6083-129">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![NuGet paketlerini komutu için proje başvuruları yönetme](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="b6083-131">"Nuget.org" olarak seçin **paket kaynağı**seçin **Gözat** sekmesinde, arama **Newtonsoft.Json**, listesinde o paketi seçin ve seçin  **Yükleme**:</span><span class="sxs-lookup"><span data-stu-id="b6083-131">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Newtonsoft.Json paket bulma](media/QS_Use-03-NewtonsoftJson.png)

1. <span data-ttu-id="b6083-133">Paket Yönetimi biçimi seçin isteyip istemediğiniz sorulduğunda (önerilen) PackageReference arasında seçin ve `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="b6083-133">If prompted to select a package management format, choose between PackageReference (recommended) and `packages.config`:</span></span>

    ![Bir paket başvuru biçimi seçme](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="b6083-135">Değişiklikleri gözden geçirmek için istenirse seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="b6083-135">If prompted to review changes, select **OK**.</span></span>

1. <span data-ttu-id="b6083-136">Çözüm Gezgini'ndeki çözüme sağ tıklayın ve **yapı çözümü**.</span><span class="sxs-lookup"><span data-stu-id="b6083-136">Right-click the solution in Solution Explorer and select **Build Solution**.</span></span> <span data-ttu-id="b6083-137">Bu altında listelenen herhangi bir NuGet paketinin geri yükler **başvurular**.</span><span class="sxs-lookup"><span data-stu-id="b6083-137">This restores any NuGet packages listed under **References**.</span></span> <span data-ttu-id="b6083-138">Daha fazla ayrıntı için bkz: [paketi geri yüklemesi](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="b6083-138">For more details, see [Package Restore](../consume-packages/package-restore.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="b6083-139">' % S ' Newtonsoft.Json API uygulamasında kullanma</span><span class="sxs-lookup"><span data-stu-id="b6083-139">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="b6083-140">Projedeki Newtonsoft.Json paketiyle çağırabilirsiniz kendi `JsonConvert.SerializeObject` bir nesne okunabilir bir dizeye dönüştürmek için yöntem.</span><span class="sxs-lookup"><span data-stu-id="b6083-140">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="b6083-141">Açık `MainWindow.xaml` (WPF) veya `MainPage.xaml` (UWP) ve varolan `Grid` aşağıdaki öğeyle:</span><span class="sxs-lookup"><span data-stu-id="b6083-141">Open `MainWindow.xaml` (WPF) or `MainPage.xaml` (UWP) and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="b6083-142">Genişletme `MainWindow.xaml` (WPF) veya `MainPage.xaml` Çözüm Gezgini'nde Aç (UWP) düğüm `.cs` dosya ve aşağıdaki kodu ekleyin `MainWindow` veya `MainPage` Oluşturucusu sonra sınıfı:</span><span class="sxs-lookup"><span data-stu-id="b6083-142">Expand the `MainWindow.xaml` (WPF) or `MainPage.xaml` (UWP) node in Solution Explorer, open the `.cs` file, and insert the following code inside the `MainWindow` or `MainPage` class, after the constructor:</span></span>

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

1. <span data-ttu-id="b6083-143">Newtonsoft.Json paketini projeye eklenen olsa da, kırmızı dalgalı çizgiler altında görünür `JsonConvert` , gerektiğinden bir `using` deyimi.</span><span class="sxs-lookup"><span data-stu-id="b6083-143">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement.</span></span> <span data-ttu-id="b6083-144">Altı çizili getirin `JsonConvert` ampul ve seçeneğini görürsünüz **olası düzeltmeleri göster**:</span><span class="sxs-lookup"><span data-stu-id="b6083-144">Hover over the underlined `JsonConvert` and you'll see the Lightbulb and the option to **Show potential fixes**:</span></span>

    ![Ampul Göster olası ile komut giderir](media/QS_Use-04-ShowPotentialFixes.png)


1. <span data-ttu-id="b6083-146">Tıklayın **olası düzeltmeleri göster** (veya ampul) ve ilk önerilen düzeltmeyi seçin `using Newtonsoft.Json;`.</span><span class="sxs-lookup"><span data-stu-id="b6083-146">Click on **Show potential fixes** (or the Lightbulb) and select the first suggested fix, `using Newtonsoft.Json;`.</span></span> <span data-ttu-id="b6083-147">Bu gerekli satır dosyanın üst kısmına ekler.</span><span class="sxs-lookup"><span data-stu-id="b6083-147">This adds the necessary line to the top of the file.</span></span>

    ![Kullanarak bir eklemek için seçeneği vermiş ampul deyimi](media/QS_Use-05-AddUsing.png)

1. <span data-ttu-id="b6083-149">Derleme ve F5 tuşuna basarak veya seçerek uygulamayı çalıştırma **hata ayıklama > hata ayıklamayı Başlat** (UWP burada; gösterilen WPF benzer):</span><span class="sxs-lookup"><span data-stu-id="b6083-149">Build and run the app by pressing F5 or selecting **Debug > Start Debugging** (UWP shown here; WPF is similar):</span></span>

    ![UWP uygulaması ilk çıktısı](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="b6083-151">İle bazı JSON metnin yerine TextBlock içeriğini görmek için düğmeyi seçin:</span><span class="sxs-lookup"><span data-stu-id="b6083-151">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![Düğme seçtikten sonra UWP uygulamasında çıktısı](media/QS_Use-07-AppEnd.png)

## <a name="related-topics"></a><span data-ttu-id="b6083-153">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="b6083-153">Related topics</span></span>

- [<span data-ttu-id="b6083-154">Genel bakış ve iş akışı paket tüketimi</span><span class="sxs-lookup"><span data-stu-id="b6083-154">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="b6083-155">Bulma ve paketleri seçme</span><span class="sxs-lookup"><span data-stu-id="b6083-155">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="b6083-156">NuGet Davranışını Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="b6083-156">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
