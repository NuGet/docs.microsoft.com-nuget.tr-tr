---
title: Mac için Visual Studio'da nuget paketi yükleyin ve kullanın
description: Mac projesi için Visual Studio'da bir NuGet paketini yükleme ve kullanma süreci hakkında bir iz geçidi öğreticisi.
author: jmatthiesen
ms.author: jomatthi
ms.date: 08/14/2019
ms.topic: quickstart
ms.openlocfilehash: 6f3fd4f2ffec0037a48aec845fddee258b5c1e7f
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "70238527"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-for-mac"></a><span data-ttu-id="faec1-103">Quickstart: Mac için Visual Studio'da bir paket yükleyin ve kullanın</span><span class="sxs-lookup"><span data-stu-id="faec1-103">Quickstart: Install and use a package in Visual Studio for Mac</span></span>

<span data-ttu-id="faec1-104">NuGet paketleri, diğer geliştiricilerin projelerinizde kullanmak üzere kullanabileceğiniz yeniden kullanılabilir kodlar içerir.</span><span class="sxs-lookup"><span data-stu-id="faec1-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="faec1-105">NuGet [nedir?](../What-is-NuGet.md)</span><span class="sxs-lookup"><span data-stu-id="faec1-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="faec1-106">Paketler NuGet Paket Yöneticisi kullanılarak Mac projesi için bir Visual Studio'ya yüklenir.</span><span class="sxs-lookup"><span data-stu-id="faec1-106">Packages are installed into a Visual Studio for Mac project using the NuGet Package Manager.</span></span> <span data-ttu-id="faec1-107">Bu makale, popüler [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) paketi ve .NET Core konsol projesini kullanarak süreci göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="faec1-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a .NET Core console project.</span></span> <span data-ttu-id="faec1-108">Aynı işlem diğer Xamarin veya .NET Core projesi için de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="faec1-108">The same process applies to any other Xamarin or .NET Core project.</span></span>

<span data-ttu-id="faec1-109">Yüklendikten sonra, ad alanının `using <namespace>` \<\> kullanmakta olduğunuz pakete özgü olduğu koddaki pakete bakın.</span><span class="sxs-lookup"><span data-stu-id="faec1-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="faec1-110">Başvuru yapıldıktan sonra, paketi API'si aracılığıyla arayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="faec1-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="faec1-111">**nuget.org ile başlayın**: nuget.org göz *atma* ,NET geliştiricilerin genellikle kendi uygulamalarında yeniden kullanabilecekleri bileşenleri nasıl bulduklarıdır.</span><span class="sxs-lookup"><span data-stu-id="faec1-111">**Start with nuget.org**: Browsing *nuget.org* is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="faec1-112">Bu makalede gösterildiği gibi *doğrudan nuget.org* arayabilir veya Visual Studio'daki paketleri bulabilir ve yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="faec1-112">You can search *nuget.org* directly or find and install packages within Visual Studio as shown in this article.</span></span> <span data-ttu-id="faec1-113">Genel bilgi için [NuGet paketlerini bul ve değerlendirin.](../consume-packages/finding-and-choosing-packages.md)</span><span class="sxs-lookup"><span data-stu-id="faec1-113">For general information, see [Find and evaluate NuGet packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="faec1-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="faec1-114">Prerequisites</span></span>

- <span data-ttu-id="faec1-115">Mac için Visual Studio 2019.</span><span class="sxs-lookup"><span data-stu-id="faec1-115">Visual Studio 2019 for Mac.</span></span>

<span data-ttu-id="faec1-116">2019 Topluluk sürümünü [visualstudio.com](https://www.visualstudio.com/) ücretsiz olarak yükleyebilir veya Professional veya Enterprise sürümlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="faec1-116">You can install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="faec1-117">Windows'da Visual Studio kullanıyorsanız, [Visual Studio'da (Yalnızca Windows) bir paketi yükle'ye](install-and-use-a-package-in-visual-studio.md)bakın ve kullanın.</span><span class="sxs-lookup"><span data-stu-id="faec1-117">If you're using Visual Studio on Windows, see [Install and use a package in Visual Studio (Windows Only)](install-and-use-a-package-in-visual-studio.md).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="faec1-118">Proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="faec1-118">Create a project</span></span>

<span data-ttu-id="faec1-119">NuGet paketleri, paketin projeyle aynı hedef çerçeveyi desteklemesi koşuluyla herhangi bir .NET projesine yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="faec1-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="faec1-120">Bu iz için basit bir .NET Core Console uygulamasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="faec1-120">For this walkthrough, use a simple .NET Core Console app.</span></span> <span data-ttu-id="faec1-121">Dosya > Yeni Çözüm'> kullanarak Mac için Visual Studio'da bir proje **oluşturun...** **.NET Core > App > Console Application** şablonu'nu seçin.</span><span class="sxs-lookup"><span data-stu-id="faec1-121">Create a project in Visual Studio for Mac using **File > New Solution...**, select the **.NET Core > App > Console Application** template.</span></span> <span data-ttu-id="faec1-122">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="faec1-122">Click **Next**.</span></span> <span data-ttu-id="faec1-123">İstendiğinde **Hedef Çerçeve** için varsayılan değerleri kabul edin.</span><span class="sxs-lookup"><span data-stu-id="faec1-123">Accept the default values for **Target Framework** when prompted.</span></span>

<span data-ttu-id="faec1-124">Visual Studio, Solution Explorer'da açılan projeyi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="faec1-124">Visual Studio creates the project, which opens in Solution Explorer.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="faec1-125">Newtonsoft.Json NuGet paketini ekleyin</span><span class="sxs-lookup"><span data-stu-id="faec1-125">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="faec1-126">Paketi yüklemek için NuGet Paket Yöneticisi'ni kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="faec1-126">To install the package, you use the NuGet Package Manager.</span></span> <span data-ttu-id="faec1-127">Bir paket yüklediğinizde, NuGet bağımlılıkları proje dosyanıza `packages.config` veya dosyanızda kaydeder (proje biçimine bağlı olarak).</span><span class="sxs-lookup"><span data-stu-id="faec1-127">When you install a package, NuGet records the dependency in  either your project file or a `packages.config` file (depending on the project format).</span></span> <span data-ttu-id="faec1-128">Daha fazla bilgi için [bkz: Paket tüketimine genel bakış ve iş akışı.](../consume-packages/Overview-and-Workflow.md)</span><span class="sxs-lookup"><span data-stu-id="faec1-128">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="nuget-package-manager"></a><span data-ttu-id="faec1-129">NuGet Paket Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="faec1-129">NuGet Package Manager</span></span>

1. <span data-ttu-id="faec1-130">Çözüm Gezgini'nde, **Bağımlılıklar'ı** sağ tıklatın ve **Paket Ekle'yi seçin...** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="faec1-130">In Solution Explorer, right-click **Dependencies** and choose **Add Packages...**.</span></span>

    ![Proje Başvuruları için NuGet Paketleri komutunu yönetme](media/QS_Use_Mac-02-ManageNuGetPackages.png)

1. <span data-ttu-id="faec1-132">İletişim kutusunun sol üst **köşesindeki Paket kaynağı** olarak "nuget.org" seçeneğini belirleyin ve **Newtonsoft.Json'ı**arayın, listedeki paketi seçin ve **Paket Ekle'yi seçin...**</span><span class="sxs-lookup"><span data-stu-id="faec1-132">Choose "nuget.org" as the **Package source** in the top left corner of the dialog, and search for **Newtonsoft.Json**, select that package in the list, and select **Add Packages...**:</span></span>

    ![Newtonsoft.Json paketinin bulunması](media/QS_Use_Mac-03-NewtonsoftJson.png)

    <span data-ttu-id="faec1-134">NuGet Paket Yöneticisi hakkında daha fazla bilgi istiyorsanız, [Mac için Visual Studio'yu kullanarak paketleri yükle ve yönet'](../consume-packages/install-use-packages-visual-studio.md)e bakın.</span><span class="sxs-lookup"><span data-stu-id="faec1-134">If you want more information on the NuGet Package Manager, see [Install and manage packages using Visual Studio for Mac](../consume-packages/install-use-packages-visual-studio.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="faec1-135">Uygulamada Newtonsoft.Json API'yi kullanın</span><span class="sxs-lookup"><span data-stu-id="faec1-135">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="faec1-136">Projedeki Newtonsoft.Json paketi yle, bir `JsonConvert.SerializeObject` nesneyi insan tarafından okunabilir bir dize dönüştürme yöntemini arayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="faec1-136">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="faec1-137">Dosyayı `Program.cs` açın (Çözüm Defteri'nde bulunan) ve dosya içeriğini aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="faec1-137">Open the `Program.cs` file (located in the Solution Pad) and replace the file contents with the following code:</span></span>

    ```cs
    using System;
    using Newtonsoft.Json;

    namespace NuGetDemo
    {
        public class Account
        {
            public string Name { get; set; }
            public string Email { get; set; }
            public DateTime DOB { get; set; }
        }
    
        class Program
        {
            static void Main(string[] args)
            {
                Account account = new Account()
                {
                    Name = "Joe Doe",
                    Email = "joe@test.com",
                    DOB = new DateTime(1976, 3, 24)
                };
                string json = JsonConvert.SerializeObject(account);
                Console.WriteLine(json);
            }
        }
    }
    ```

1. <span data-ttu-id="faec1-138">Hata Ayıklama yı **başlat'> çalıştır'ı**seçerek uygulamayı oluşturun ve çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="faec1-138">Build and run the app by selecting **Run > Start Debugging**:</span></span>

1. <span data-ttu-id="faec1-139">Uygulama çalıştırıldıktan sonra, seri leştirilmiş JSON çıkışının konsolda göründüğünü görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="faec1-139">Once the app runs, you'll see the serialized JSON output appear in the console:</span></span>

  ![Konsol uygulamasının çıktısı](media/QS_Use_Mac-06-AppStart.png)

## <a name="next-steps"></a><span data-ttu-id="faec1-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="faec1-141">Next steps</span></span>
<span data-ttu-id="faec1-142">İlk NuGet paketinizi yükledikten ve kullandığınız için tebrikler!</span><span class="sxs-lookup"><span data-stu-id="faec1-142">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="faec1-143">Mac için Visual Studio'u kullanarak paketleri yükleyin ve yönetin</span><span class="sxs-lookup"><span data-stu-id="faec1-143">Install and manage packages using Visual Studio for Mac</span></span>](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)

<span data-ttu-id="faec1-144">NuGet'in sunduğu daha fazlasını keşfetmek için aşağıdaki bağlantıları seçin.</span><span class="sxs-lookup"><span data-stu-id="faec1-144">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="faec1-145">Paket tüketimine genel bakış ve iş akışı</span><span class="sxs-lookup"><span data-stu-id="faec1-145">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="faec1-146">Proje dosyalarında paket başvuruları</span><span class="sxs-lookup"><span data-stu-id="faec1-146">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
