---
title: Mac için Visual Studio bir NuGet paketi yükleyip kullanın
description: Bir Mac için Visual Studio projesindeki NuGet paketini yükleme ve kullanma işlemi hakkında bir adım adım öğretici.
author: jmatthiesen
ms.author: jomatthi
ms.date: 08/14/2019
ms.topic: quickstart
ms.openlocfilehash: 6f3fd4f2ffec0037a48aec845fddee258b5c1e7f
ms.sourcegitcommit: ac9a00ccaf90e539a381e92b650074910b21eb0d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/03/2019
ms.locfileid: "70238527"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-for-mac"></a><span data-ttu-id="44bd1-103">Hızlı Başlangıç: Mac için Visual Studio bir paketi yükleyip kullanma</span><span class="sxs-lookup"><span data-stu-id="44bd1-103">Quickstart: Install and use a package in Visual Studio for Mac</span></span>

<span data-ttu-id="44bd1-104">NuGet paketleri, diğer geliştiricilerin projelerinizde kullanabileceğiniz bir yeniden kullanılabilir kod içerir.</span><span class="sxs-lookup"><span data-stu-id="44bd1-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="44bd1-105">Arka plan için bkz. [NuGet nedir?](../What-is-NuGet.md) .</span><span class="sxs-lookup"><span data-stu-id="44bd1-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="44bd1-106">Paketler, NuGet Paket Yöneticisi kullanılarak bir Mac için Visual Studio projesine yüklenir.</span><span class="sxs-lookup"><span data-stu-id="44bd1-106">Packages are installed into a Visual Studio for Mac project using the NuGet Package Manager.</span></span> <span data-ttu-id="44bd1-107">Bu makalede, popüler [Newtonsoft. JSON](https://www.nuget.org/packages/Newtonsoft.Json/) paketini ve bir .NET Core konsol projesini kullanan işlem gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="44bd1-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a .NET Core console project.</span></span> <span data-ttu-id="44bd1-108">Aynı işlem diğer Xamarin veya .NET Core projeleri için de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="44bd1-108">The same process applies to any other Xamarin or .NET Core project.</span></span>

<span data-ttu-id="44bd1-109">Yüklendikten sonra, koddaki `using <namespace>` \<pakete, ad alanının\> kullandığınız pakete özgü olduğunu bakın.</span><span class="sxs-lookup"><span data-stu-id="44bd1-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="44bd1-110">Başvuru yapıldıktan sonra, paketini API 'SI aracılığıyla çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44bd1-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="44bd1-111">**NuGet.org Ile Başlat**: *NuGet.org* gözatma, .NET geliştiricilerinin kendi uygulamalarında yeniden kullanabilecekleri bileşenleri genellikle bulmasıdır.</span><span class="sxs-lookup"><span data-stu-id="44bd1-111">**Start with nuget.org**: Browsing *nuget.org* is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="44bd1-112">Bu makalede gösterildiği gibi, *NuGet.org* doğrudan arayabilir veya Visual Studio içinde paketleri bulabilir ve yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44bd1-112">You can search *nuget.org* directly or find and install packages within Visual Studio as shown in this article.</span></span> <span data-ttu-id="44bd1-113">Genel bilgi için bkz. [NuGet paketlerini bulma ve değerlendirme](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="44bd1-113">For general information, see [Find and evaluate NuGet packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44bd1-114">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="44bd1-114">Prerequisites</span></span>

- <span data-ttu-id="44bd1-115">Mac için Visual Studio 2019.</span><span class="sxs-lookup"><span data-stu-id="44bd1-115">Visual Studio 2019 for Mac.</span></span>

<span data-ttu-id="44bd1-116">2019 Community Edition 'ı [VisualStudio.com](https://www.visualstudio.com/) adresinden ücretsiz olarak yükleyebilir veya profesyonel ya da Enterprise sürümlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44bd1-116">You can install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="44bd1-117">Windows üzerinde Visual Studio kullanıyorsanız bkz. [Visual Studio 'da paket yükleyip kullanma (yalnızca Windows)](install-and-use-a-package-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="44bd1-117">If you're using Visual Studio on Windows, see [Install and use a package in Visual Studio (Windows Only)](install-and-use-a-package-in-visual-studio.md).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="44bd1-118">Proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="44bd1-118">Create a project</span></span>

<span data-ttu-id="44bd1-119">NuGet paketleri, paketin proje ile aynı hedef Framework 'ü desteklemesi kaydıyla herhangi bir .NET projesine yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="44bd1-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="44bd1-120">Bu izlenecek yol için basit bir .NET Core konsol uygulaması kullanın.</span><span class="sxs-lookup"><span data-stu-id="44bd1-120">For this walkthrough, use a simple .NET Core Console app.</span></span> <span data-ttu-id="44bd1-121">**Dosya > yeni çözüm...** ' yi kullanarak Mac için Visual Studio bir proje oluşturun, **.NET Core > uygulama > konsol uygulaması** şablonunu seçin.</span><span class="sxs-lookup"><span data-stu-id="44bd1-121">Create a project in Visual Studio for Mac using **File > New Solution...**, select the **.NET Core > App > Console Application** template.</span></span> <span data-ttu-id="44bd1-122">**İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="44bd1-122">Click **Next**.</span></span> <span data-ttu-id="44bd1-123">İstendiğinde **hedef Framework** için varsayılan değerleri kabul edin.</span><span class="sxs-lookup"><span data-stu-id="44bd1-123">Accept the default values for **Target Framework** when prompted.</span></span>

<span data-ttu-id="44bd1-124">Visual Studio, Çözüm Gezgini ' de açılan projeyi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="44bd1-124">Visual Studio creates the project, which opens in Solution Explorer.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="44bd1-125">Newtonsoft. JSON NuGet paketini ekleyin</span><span class="sxs-lookup"><span data-stu-id="44bd1-125">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="44bd1-126">Paketi yüklemek için NuGet Paket Yöneticisi 'Ni kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="44bd1-126">To install the package, you use the NuGet Package Manager.</span></span> <span data-ttu-id="44bd1-127">Bir paket yüklediğinizde, NuGet, proje dosyanıza ya da bir `packages.config` dosyaya (proje biçimine bağlı olarak) bağımlılığı kaydeder.</span><span class="sxs-lookup"><span data-stu-id="44bd1-127">When you install a package, NuGet records the dependency in  either your project file or a `packages.config` file (depending on the project format).</span></span> <span data-ttu-id="44bd1-128">Daha fazla bilgi için bkz. [paket tüketimine genel bakış ve iş akışı](../consume-packages/Overview-and-Workflow.md).</span><span class="sxs-lookup"><span data-stu-id="44bd1-128">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="nuget-package-manager"></a><span data-ttu-id="44bd1-129">NuGet Paket Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="44bd1-129">NuGet Package Manager</span></span>

1. <span data-ttu-id="44bd1-130">Çözüm Gezgini ' de **Bağımlılıklar** ' a sağ tıklayın ve **paket Ekle...** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="44bd1-130">In Solution Explorer, right-click **Dependencies** and choose **Add Packages...**.</span></span>

    ![Proje başvuruları için NuGet Paketlerini Yönet komutu](media/QS_Use_Mac-02-ManageNuGetPackages.png)

1. <span data-ttu-id="44bd1-132">İletişim kutusunun sol üst köşesindeki **paket kaynağı** olarak "NuGet.org" öğesini seçin ve **Newtonsoft. JSON**için arama yapın, listeden bu paketi seçin ve **paket Ekle...** ' yi seçin:</span><span class="sxs-lookup"><span data-stu-id="44bd1-132">Choose "nuget.org" as the **Package source** in the top left corner of the dialog, and search for **Newtonsoft.Json**, select that package in the list, and select **Add Packages...**:</span></span>

    ![Newtonsoft. JSON paketi bulunuyor](media/QS_Use_Mac-03-NewtonsoftJson.png)

    <span data-ttu-id="44bd1-134">NuGet Paket Yöneticisi hakkında daha fazla bilgi edinmek istiyorsanız, bkz. [Mac için Visual Studio kullanarak paketleri yükleyip yönetme](../consume-packages/install-use-packages-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="44bd1-134">If you want more information on the NuGet Package Manager, see [Install and manage packages using Visual Studio for Mac](../consume-packages/install-use-packages-visual-studio.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="44bd1-135">Uygulamada Newtonsoft. JSON API 'sini kullanma</span><span class="sxs-lookup"><span data-stu-id="44bd1-135">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="44bd1-136">Projedeki Newtonsoft. JSON paketiyle, bir nesneyi insan tarafından okunabilen bir dizeye dönüştürmek `JsonConvert.SerializeObject` için yöntemini çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44bd1-136">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="44bd1-137">`Program.cs` Dosyayı açın (çözüm bölmesi) ve dosya içeriğini aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="44bd1-137">Open the `Program.cs` file (located in the Solution Pad) and replace the file contents with the following code:</span></span>

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

1. <span data-ttu-id="44bd1-138">**Çalıştır > hata ayıklamayı Başlat**öğesini seçerek uygulamayı derleyin ve çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="44bd1-138">Build and run the app by selecting **Run > Start Debugging**:</span></span>

1. <span data-ttu-id="44bd1-139">Uygulama çalıştıktan sonra, serileştirilmiş JSON çıkışının konsolunda göründüğünü görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="44bd1-139">Once the app runs, you'll see the serialized JSON output appear in the console:</span></span>

  ![Konsol uygulamasının çıkışı](media/QS_Use_Mac-06-AppStart.png)

## <a name="next-steps"></a><span data-ttu-id="44bd1-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="44bd1-141">Next steps</span></span>
<span data-ttu-id="44bd1-142">İlk NuGet paketinizi yükleme ve kullanma hakkında Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="44bd1-142">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="44bd1-143">Mac için Visual Studio kullanarak paket yükleyip yönetme</span><span class="sxs-lookup"><span data-stu-id="44bd1-143">Install and manage packages using Visual Studio for Mac</span></span>](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)

<span data-ttu-id="44bd1-144">NuGet 'in sunabileceği daha fazlasını araştırmak için aşağıdaki bağlantıları seçin.</span><span class="sxs-lookup"><span data-stu-id="44bd1-144">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="44bd1-145">Paket tüketiminin genel bakış ve iş akışı</span><span class="sxs-lookup"><span data-stu-id="44bd1-145">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="44bd1-146">Proje dosyalarında paket başvuruları</span><span class="sxs-lookup"><span data-stu-id="44bd1-146">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
