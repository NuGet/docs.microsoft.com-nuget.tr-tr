---
title: Kullanarak NuGet paketleri aracılığıyla dotnet CLI için tanıtım Kılavuzu
description: Bir NuGet paketi kullanarak bir .NET Core projesinde ve yükleme işlemini bir gözden geçirme öğretici.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 0d637c441cf9f36e8e3e04e47b524b2defecae52
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67841665"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="66623-103">Hızlı Başlangıç: Dotnet CLI kullanarak bir paket yükleyip</span><span class="sxs-lookup"><span data-stu-id="66623-103">Quickstart: Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="66623-104">NuGet paketleri diğer geliştiriciler projelerinizde kullanmak için kullanılabilir hale yeniden kullanılabilir bir kod içerir.</span><span class="sxs-lookup"><span data-stu-id="66623-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="66623-105">Bkz: [NuGet nedir?](../What-is-NuGet.md) arka planı.</span><span class="sxs-lookup"><span data-stu-id="66623-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="66623-106">Paketleri kullanarak bir .NET Core projesi yüklü `dotnet add package` komutu popüler için bu makalede anlatıldığı gibi [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) paket.</span><span class="sxs-lookup"><span data-stu-id="66623-106">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="66623-107">Kod ile paket yüklendikten sonra başvurmak `using <namespace>` burada \<ad alanı\> kullanmakta olduğunuz paket özgüdür.</span><span class="sxs-lookup"><span data-stu-id="66623-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="66623-108">Ardından, paket API'si de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66623-108">You can then use the package's API.</span></span>

> [!Tip]
> <span data-ttu-id="66623-109">**Nuget.org ile Başlat**: Gözatma nuget.org'nin olduğundan nasıl .NET geliştiricilerinin bileşenler genellikle bulun, kendi uygulamalarında yeniden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66623-109">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="66623-110">Nuget.org doğrudan arama veya bulabilir ve bu makalede gösterilen şekilde Visual Studio içindeki paketleri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="66623-110">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66623-111">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="66623-111">Prerequisites</span></span>

- <span data-ttu-id="66623-112">[.NET Core SDK'sı](https://www.microsoft.com/net/download/), sağlayan `dotnet` komut satırı aracı.</span><span class="sxs-lookup"><span data-stu-id="66623-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="66623-113">Dotnet CLI herhangi bir .NET Core ile otomatik olarak yüklenir, Visual Studio 2017'de başlayarak, iş yüklerini ilgili.</span><span class="sxs-lookup"><span data-stu-id="66623-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="66623-114">Proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="66623-114">Create a project</span></span>

<span data-ttu-id="66623-115">NuGet paketlerini, tür bir .NET projesine yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="66623-115">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="66623-116">Bu kılavuz için şu şekilde basit bir .NET Core konsol projesi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="66623-116">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="66623-117">Proje için bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="66623-117">Create a folder for the project.</span></span>

1. <span data-ttu-id="66623-118">Aşağıdaki komutu kullanarak proje oluştur:</span><span class="sxs-lookup"><span data-stu-id="66623-118">Create the project using the following command:</span></span>

    ```cli
    dotnet new console
    ```

1. <span data-ttu-id="66623-119">Kullanım `dotnet run` uygulamayı düzgün bir şekilde oluşturulduğunu test etmek için.</span><span class="sxs-lookup"><span data-stu-id="66623-119">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="66623-120">Newtonsoft.Json NuGet paketi ekleme</span><span class="sxs-lookup"><span data-stu-id="66623-120">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="66623-121">Yüklemek için aşağıdaki komutu kullanın `Newtonsoft.json` paket:</span><span class="sxs-lookup"><span data-stu-id="66623-121">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```cli
    dotnet add package Newtonsoft.Json
    ```

2. <span data-ttu-id="66623-122">Komut tamamlandıktan sonra açın `.csproj` dosya eklendi başvuru görmek için:</span><span class="sxs-lookup"><span data-stu-id="66623-122">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="66623-123">' % S ' Newtonsoft.Json API uygulamasında kullanma</span><span class="sxs-lookup"><span data-stu-id="66623-123">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="66623-124">Açık `Program.cs` dosya ve dosyasının en üstüne aşağıdaki satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="66623-124">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="66623-125">Önce aşağıdaki kodu ekleyin `class Program` satırı:</span><span class="sxs-lookup"><span data-stu-id="66623-125">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="66623-126">Değiştirin `Main` işlevi aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="66623-126">Replace the `Main` function with the following:</span></span>

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

1. <span data-ttu-id="66623-127">Kullanarak uygulaması derleyebilir ve `dotnet run` komutu.</span><span class="sxs-lookup"><span data-stu-id="66623-127">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="66623-128">Çıkış JSON gösterimi olmalıdır `Account` kod nesnesinde:</span><span class="sxs-lookup"><span data-stu-id="66623-128">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="related-articles"></a><span data-ttu-id="66623-129">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="66623-129">Related articles</span></span>

- [<span data-ttu-id="66623-130">Dotnet CLI kullanarak paketleri yükleyip</span><span class="sxs-lookup"><span data-stu-id="66623-130">Install and use packages using the dotnet CLI</span></span>](../consume-packages/install-use-packages-dotnet-cli.md)
- [<span data-ttu-id="66623-131">Genel bakış ve paket tüketim iş akışı</span><span class="sxs-lookup"><span data-stu-id="66623-131">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="66623-132">Paketleri bulma ve seçme</span><span class="sxs-lookup"><span data-stu-id="66623-132">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="66623-133">Ortak NuGet yapılandırmaları</span><span class="sxs-lookup"><span data-stu-id="66623-133">Common NuGet configurations</span></span>](../consume-packages/configuring-nuget-behavior.md)
