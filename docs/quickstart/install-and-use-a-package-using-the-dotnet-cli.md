---
title: Kullanarak NuGet paketleri aracılığıyla dotnet CLI için tanıtım Kılavuzu
description: Bir NuGet paketi kullanarak bir .NET Core projesinde ve yükleme işlemini bir gözden geçirme öğretici.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 4b593cc215ad68629e5a93d1f17c90e53c0b4f4f
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324636"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="131e2-103">Hızlı Başlangıç: Dotnet CLI kullanarak bir paket yükleyip</span><span class="sxs-lookup"><span data-stu-id="131e2-103">Quickstart: Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="131e2-104">NuGet paketleri diğer geliştiriciler projelerinizde kullanmak için kullanılabilir hale yeniden kullanılabilir bir kod içerir.</span><span class="sxs-lookup"><span data-stu-id="131e2-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="131e2-105">Bkz: [NuGet nedir?](../What-is-NuGet.md) arka planı.</span><span class="sxs-lookup"><span data-stu-id="131e2-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="131e2-106">Paketleri kullanarak bir .NET Core projesi yüklü `dotnet add package` komutu popüler için bu makalede anlatıldığı gibi [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) paket.</span><span class="sxs-lookup"><span data-stu-id="131e2-106">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="131e2-107">Kod ile paket yüklendikten sonra başvurmak `using <namespace>` burada \<ad alanı\> kullanmakta olduğunuz paket özgüdür.</span><span class="sxs-lookup"><span data-stu-id="131e2-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="131e2-108">Ardından, paket API'si de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="131e2-108">You can then use the package's API.</span></span>

> [!Tip]
> <span data-ttu-id="131e2-109">**Nuget.org ile Başlat**: Gözatma nuget.org'nin olduğundan nasıl .NET geliştiricilerinin bileşenler genellikle bulun, kendi uygulamalarında yeniden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="131e2-109">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="131e2-110">Nuget.org doğrudan arama veya bulabilir ve bu makalede gösterilen şekilde Visual Studio içindeki paketleri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="131e2-110">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="131e2-111">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="131e2-111">Prerequisites</span></span>

- <span data-ttu-id="131e2-112">[.NET Core SDK'sı](https://www.microsoft.com/net/download/), sağlayan `dotnet` komut satırı aracı.</span><span class="sxs-lookup"><span data-stu-id="131e2-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="131e2-113">Proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="131e2-113">Create a project</span></span>

<span data-ttu-id="131e2-114">NuGet paketlerini, tür bir .NET projesine yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="131e2-114">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="131e2-115">Bu kılavuz için şu şekilde basit bir .NET Core konsol projesi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="131e2-115">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="131e2-116">Proje için bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="131e2-116">Create a folder for the project.</span></span>

1. <span data-ttu-id="131e2-117">Aşağıdaki komutu kullanarak proje oluştur:</span><span class="sxs-lookup"><span data-stu-id="131e2-117">Create the project using the following command:</span></span>

    ```cli
    dotnet new console
    ```

1. <span data-ttu-id="131e2-118">Kullanım `dotnet run` uygulamayı düzgün bir şekilde oluşturulduğunu test etmek için.</span><span class="sxs-lookup"><span data-stu-id="131e2-118">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="131e2-119">Newtonsoft.Json NuGet paketi ekleme</span><span class="sxs-lookup"><span data-stu-id="131e2-119">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="131e2-120">Yüklemek için aşağıdaki komutu kullanın `Newtonsoft.json` paket:</span><span class="sxs-lookup"><span data-stu-id="131e2-120">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```cli
    dotnet add package Newtonsoft.Json
    ```

2. <span data-ttu-id="131e2-121">Komut tamamlandıktan sonra açın `.csproj` dosya eklendi başvuru görmek için:</span><span class="sxs-lookup"><span data-stu-id="131e2-121">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="131e2-122">' % S ' Newtonsoft.Json API uygulamasında kullanma</span><span class="sxs-lookup"><span data-stu-id="131e2-122">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="131e2-123">Açık `Program.cs` dosya ve dosyasının en üstüne aşağıdaki satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="131e2-123">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="131e2-124">Önce aşağıdaki kodu ekleyin `class Program` satırı:</span><span class="sxs-lookup"><span data-stu-id="131e2-124">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="131e2-125">Değiştirin `Main` işlevi aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="131e2-125">Replace the `Main` function with the following:</span></span>

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

1. <span data-ttu-id="131e2-126">Kullanarak uygulaması derleyebilir ve `dotnet run` komutu.</span><span class="sxs-lookup"><span data-stu-id="131e2-126">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="131e2-127">Çıkış JSON gösterimi olmalıdır `Account` kod nesnesinde:</span><span class="sxs-lookup"><span data-stu-id="131e2-127">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="related-articles"></a><span data-ttu-id="131e2-128">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="131e2-128">Related articles</span></span>

- [<span data-ttu-id="131e2-129">Genel bakış ve paket tüketim iş akışı</span><span class="sxs-lookup"><span data-stu-id="131e2-129">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="131e2-130">Paketleri bulma ve seçme</span><span class="sxs-lookup"><span data-stu-id="131e2-130">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="131e2-131">Paket yükleme yolu</span><span class="sxs-lookup"><span data-stu-id="131e2-131">Ways to install a package</span></span>](../consume-packages/ways-to-install-a-package.md)
- [<span data-ttu-id="131e2-132">NuGet Davranışını Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="131e2-132">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
