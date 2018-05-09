---
title: Tanıtım kılavuzu kullanarak NuGet paketleri yoluyla CLI dotnet
description: İzlenecek yol öğretici yüklenmesi ve .NET Core projede bir NuGet paketi kullanarak işleme.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 41a249394a8a0504cc8841d3bdb67ad29ec2dc26
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/28/2018
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="2bab9-103">Hızlı Başlangıç: Yükleme ve dotnet CLI kullanarak bir paket kullanma</span><span class="sxs-lookup"><span data-stu-id="2bab9-103">Quickstart: Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="2bab9-104">NuGet paketleri diğer geliştiriciler projelerinizi kullanmak için kullanılabilir hale yeniden kullanılabilir kod içerir.</span><span class="sxs-lookup"><span data-stu-id="2bab9-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="2bab9-105">Bkz: [NuGet nedir?](../What-is-NuGet.md) arka planı için.</span><span class="sxs-lookup"><span data-stu-id="2bab9-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="2bab9-106">Paketler, .NET Core kullanarak projesi içine yüklenir `dotnet add package` komutu popüler için bu makalede açıklanan [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) paket.</span><span class="sxs-lookup"><span data-stu-id="2bab9-106">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="2bab9-107">Koduyla paketinde yüklendikten sonra başvurmak `using <namespace>` nerede \<ad alanı\> kullanmakta olduğunuz paket özeldir.</span><span class="sxs-lookup"><span data-stu-id="2bab9-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="2bab9-108">Ardından, paketin API de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2bab9-108">You can then use the package's API.</span></span>

> [!Tip]
> <span data-ttu-id="2bab9-109">**Başlat nuget.org ile**: Tarama nuget.org olan nasıl .NET geliştiricilerinin bileşenleri genellikle bulmak, kendi uygulamalarında yeniden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2bab9-109">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="2bab9-110">Nuget.org doğrudan arama veya bulabilir ve bu makalede gösterilen şekilde Visual Studio içindeki paketleri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2bab9-110">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2bab9-111">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="2bab9-111">Prerequisites</span></span>

- <span data-ttu-id="2bab9-112">[.NET Core SDK](https://www.microsoft.com/net/download/), sağlayan `dotnet` komut satırı aracı.</span><span class="sxs-lookup"><span data-stu-id="2bab9-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="2bab9-113">Proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="2bab9-113">Create a project</span></span>

<span data-ttu-id="2bab9-114">NuGet paketlerini tür .NET projeye yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="2bab9-114">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="2bab9-115">Bu kılavuzda gibi basit bir .NET Core konsol projesi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="2bab9-115">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="2bab9-116">Proje için bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2bab9-116">Create a folder for the project.</span></span>

1. <span data-ttu-id="2bab9-117">Aşağıdaki komutu kullanarak projesi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="2bab9-117">Create the project using the following command:</span></span>

    ```cli
    dotnet new console
    ```

1. <span data-ttu-id="2bab9-118">Kullanım `dotnet run` uygulamayı düzgün bir şekilde oluşturulduğunu test etmek için.</span><span class="sxs-lookup"><span data-stu-id="2bab9-118">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="2bab9-119">Newtonsoft.Json NuGet paketi ekleme</span><span class="sxs-lookup"><span data-stu-id="2bab9-119">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="2bab9-120">Yüklemek için aşağıdaki komutu kullanın `Newtonsoft.json` paketi:</span><span class="sxs-lookup"><span data-stu-id="2bab9-120">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```cli
    dotnet add package Newtonsoft.Json
    ```

2. <span data-ttu-id="2bab9-121">Komut tamamlandıktan sonra açmak `.csproj` dosya eklenen başvurusuna bakın:</span><span class="sxs-lookup"><span data-stu-id="2bab9-121">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="10.0.3" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="2bab9-122">' % S ' Newtonsoft.Json API uygulamasında kullanma</span><span class="sxs-lookup"><span data-stu-id="2bab9-122">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="2bab9-123">Açık `Program.cs` dosya ve dosyanın üst kısmında aşağıdaki satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="2bab9-123">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="2bab9-124">Önce aşağıdaki kodu ekleyin `class Program` satır:</span><span class="sxs-lookup"><span data-stu-id="2bab9-124">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="2bab9-125">Değiştir `Main` aşağıdaki işleviyle:</span><span class="sxs-lookup"><span data-stu-id="2bab9-125">Replace the `Main` function with the following:</span></span>

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

1. <span data-ttu-id="2bab9-126">Derleme ve uygulamayı kullanarak çalıştırma `dotnet run` komutu.</span><span class="sxs-lookup"><span data-stu-id="2bab9-126">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="2bab9-127">Çıkış JSON gösterimi olmalıdır `Account` kodu nesnesinde:</span><span class="sxs-lookup"><span data-stu-id="2bab9-127">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="related-articles"></a><span data-ttu-id="2bab9-128">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="2bab9-128">Related articles</span></span>

- [<span data-ttu-id="2bab9-129">Genel bakış ve iş akışı paket tüketimi</span><span class="sxs-lookup"><span data-stu-id="2bab9-129">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="2bab9-130">Paketleri bulma ve seçme</span><span class="sxs-lookup"><span data-stu-id="2bab9-130">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="2bab9-131">Bir paketi yüklemek için yollar</span><span class="sxs-lookup"><span data-stu-id="2bab9-131">Ways to install a package</span></span>](../consume-packages/ways-to-install-a-package.md)
- [<span data-ttu-id="2bab9-132">NuGet Davranışını Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2bab9-132">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
