---
title: DotNet CLı kullanarak bir NuGet paketi yükleyip kullanma
description: Bir .NET Core projesinde NuGet paketini yükleme ve kullanma işlemi hakkında bir adım adım öğretici.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 47593cc65ad707b8880d854dc43824b9234fd44a
ms.sourcegitcommit: ba8ad1bd13a4bba3df94374e34e20c425a05af2f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2019
ms.locfileid: "68833305"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="66d84-103">Hızlı Başlangıç: DotNet CLı kullanarak bir paket yükleyip kullanma</span><span class="sxs-lookup"><span data-stu-id="66d84-103">Quickstart: Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="66d84-104">NuGet paketleri, diğer geliştiricilerin projelerinizde kullanabileceğiniz bir yeniden kullanılabilir kod içerir.</span><span class="sxs-lookup"><span data-stu-id="66d84-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="66d84-105">Arka plan için bkz. [NuGet nedir?](../What-is-NuGet.md) .</span><span class="sxs-lookup"><span data-stu-id="66d84-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="66d84-106">Paketler, popüler [Newtonsoft. JSON](https://www.nuget.org/packages/Newtonsoft.Json/) paketi için `dotnet add package` Bu makalede açıklandığı gibi komut kullanılarak bir .NET Core projesine yüklenir.</span><span class="sxs-lookup"><span data-stu-id="66d84-106">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="66d84-107">Yüklendikten sonra, koddaki `using <namespace>` \<pakete, ad alanının\> kullandığınız pakete özgü olduğunu bakın.</span><span class="sxs-lookup"><span data-stu-id="66d84-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="66d84-108">Daha sonra paketin API 'sini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66d84-108">You can then use the package's API.</span></span>

> [!Tip]
> <span data-ttu-id="66d84-109">**NuGet.org Ile Başlat**: Nuget.org gözatma, .NET geliştiricilerinin kendi uygulamalarında yeniden kullanabilecekleri bileşenleri genellikle bulmasıdır.</span><span class="sxs-lookup"><span data-stu-id="66d84-109">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="66d84-110">Bu makalede gösterildiği gibi, nuget.org doğrudan arayabilir veya Visual Studio içinde paketleri bulabilir ve yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66d84-110">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66d84-111">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="66d84-111">Prerequisites</span></span>

- <span data-ttu-id="66d84-112">`dotnet` Komut satırı aracını sağlayan [.NET Core SDK](https://www.microsoft.com/net/download/).</span><span class="sxs-lookup"><span data-stu-id="66d84-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="66d84-113">Visual Studio 2017 ' den başlayarak DotNet CLı, .NET Core ile ilgili iş yükleriyle otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="66d84-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="66d84-114">Proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="66d84-114">Create a project</span></span>

<span data-ttu-id="66d84-115">NuGet paketleri, bir çeşit .NET projesine yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="66d84-115">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="66d84-116">Bu izlenecek yol için aşağıdaki gibi basit bir .NET Core konsol projesi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="66d84-116">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="66d84-117">Proje için bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="66d84-117">Create a folder for the project.</span></span>

1. <span data-ttu-id="66d84-118">Bir komut istemi açın ve yeni klasöre geçiş yapın.</span><span class="sxs-lookup"><span data-stu-id="66d84-118">Open a command prompt and switch to the new folder.</span></span>

1. <span data-ttu-id="66d84-119">Aşağıdaki komutu kullanarak projeyi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="66d84-119">Create the project using the following command:</span></span>

    ```cli
    dotnet new console
    ```

1. <span data-ttu-id="66d84-120">Uygulamanın `dotnet run` düzgün şekilde oluşturulduğunu test etmek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="66d84-120">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="66d84-121">Newtonsoft. JSON NuGet paketini ekleyin</span><span class="sxs-lookup"><span data-stu-id="66d84-121">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="66d84-122">`Newtonsoft.json` Paketini yüklemek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="66d84-122">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```cli
    dotnet add package Newtonsoft.Json
    ```

2. <span data-ttu-id="66d84-123">Komut tamamlandıktan sonra, eklenen başvuruyu görmek `.csproj` için dosyayı açın:</span><span class="sxs-lookup"><span data-stu-id="66d84-123">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="66d84-124">Uygulamada Newtonsoft. JSON API 'sini kullanma</span><span class="sxs-lookup"><span data-stu-id="66d84-124">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="66d84-125">`Program.cs` Dosyasını açın ve dosyanın en üstüne aşağıdaki satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="66d84-125">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="66d84-126">Aşağıdaki kodu `class Program` satırdan önce ekleyin:</span><span class="sxs-lookup"><span data-stu-id="66d84-126">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="66d84-127">`Main` İşlevi aşağıdaki ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="66d84-127">Replace the `Main` function with the following:</span></span>

    ```cs
    static void Main(string[] args)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@nuget.org",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };

        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        Console.WriteLine(json);
    }
    ```

1. <span data-ttu-id="66d84-128">`dotnet run` Komutunu kullanarak uygulamayı derleyin ve çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="66d84-128">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="66d84-129">Çıktı, koddaki `Account` nesnenin JSON temsili olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="66d84-129">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="next-steps"></a><span data-ttu-id="66d84-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="66d84-130">Next steps</span></span>

<span data-ttu-id="66d84-131">İlk NuGet paketinizi yükleme ve kullanma hakkında Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="66d84-131">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="66d84-132">DotNet CLı kullanarak paketleri yükleyip kullanma</span><span class="sxs-lookup"><span data-stu-id="66d84-132">Install and use packages using the dotnet CLI</span></span>](../consume-packages/install-use-packages-dotnet-cli.md)

<span data-ttu-id="66d84-133">NuGet 'in sunabileceği daha fazlasını araştırmak için aşağıdaki bağlantıları seçin.</span><span class="sxs-lookup"><span data-stu-id="66d84-133">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="66d84-134">Paket tüketiminin genel bakış ve iş akışı</span><span class="sxs-lookup"><span data-stu-id="66d84-134">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="66d84-135">Paketleri bulma ve seçme</span><span class="sxs-lookup"><span data-stu-id="66d84-135">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="66d84-136">Proje dosyalarında paket başvuruları</span><span class="sxs-lookup"><span data-stu-id="66d84-136">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
