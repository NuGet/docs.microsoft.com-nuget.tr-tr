---
title: Tanıtım kılavuzu kullanarak NuGet paketleri yoluyla için CLI dotnet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: quickstart
ms.prod: nuget
ms.technology: ''
description: İzlenecek yol öğretici yüklenmesi ve .NET Core projede bir NuGet paketi kullanarak işleme.
keywords: NuGet paketlerini kullanarak NuGet paketleri, NuGet paket referanslarını yükleme NuGet, NuGet paketi tüketim yükleyin
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 87a37a733ebbbbf9bc161247b657a69f30ed4fb3
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="6a8c7-104">Yükleme ve dotnet CLI kullanarak bir paket kullanma</span><span class="sxs-lookup"><span data-stu-id="6a8c7-104">Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="6a8c7-105">NuGet paketleri diğer geliştiriciler projelerinizi kullanmak için kullanılabilir hale yeniden kullanılabilir kod içerir.</span><span class="sxs-lookup"><span data-stu-id="6a8c7-105">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="6a8c7-106">Bkz: [NuGet nedir?](../What-is-NuGet.md) arka planı için.</span><span class="sxs-lookup"><span data-stu-id="6a8c7-106">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="6a8c7-107">Paketler, .NET Core kullanarak projesi içine yüklenir `dotnet add package` komutu popüler için bu makalede açıklanan [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) paket.</span><span class="sxs-lookup"><span data-stu-id="6a8c7-107">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="6a8c7-108">Koduyla paketinde yüklendikten sonra başvurmak `using <namespace>` nerede \<ad alanı\> kullanmakta olduğunuz paket özeldir.</span><span class="sxs-lookup"><span data-stu-id="6a8c7-108">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="6a8c7-109">Ardından, paketin API de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6a8c7-109">You can then use the package's API.</span></span>

> [!Tip]
> <span data-ttu-id="6a8c7-110">**Başlat nuget.org ile**: Tarama nuget.org olan nasıl .NET geliştiricilerinin bileşenleri genellikle bulmak, kendi uygulamalarında yeniden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6a8c7-110">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="6a8c7-111">Nuget.org doğrudan arama veya bulabilir ve bu makalede gösterilen şekilde Visual Studio içindeki paketleri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="6a8c7-111">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6a8c7-112">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="6a8c7-112">Prerequisites</span></span>

- <span data-ttu-id="6a8c7-113">[.NET Core SDK](https://www.microsoft.com/net/download/), sağlayan `dotnet` komut satırı aracı.</span><span class="sxs-lookup"><span data-stu-id="6a8c7-113">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="6a8c7-114">Proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="6a8c7-114">Create a project</span></span>

<span data-ttu-id="6a8c7-115">NuGet paketlerini tür .NET projeye yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="6a8c7-115">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="6a8c7-116">Bu kılavuzda gibi basit bir .NET Core konsol projesi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="6a8c7-116">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="6a8c7-117">Proje için bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6a8c7-117">Create a folder for the project.</span></span>

1. <span data-ttu-id="6a8c7-118">Aşağıdaki komutu kullanarak projesi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="6a8c7-118">Create the project using the following command:</span></span>

    ```cli
    dotnet new console
    ```

1. <span data-ttu-id="6a8c7-119">Kullanım `dotnet run` uygulamayı düzgün bir şekilde oluşturulduğunu test etmek için.</span><span class="sxs-lookup"><span data-stu-id="6a8c7-119">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="6a8c7-120">Newtonsoft.Json NuGet paketi ekleme</span><span class="sxs-lookup"><span data-stu-id="6a8c7-120">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="6a8c7-121">Yüklemek için aşağıdaki komutu kullanın `Newtonsoft.json` paketi:</span><span class="sxs-lookup"><span data-stu-id="6a8c7-121">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```cli
    dotnet add package Newtonsoft.Json
    ```

1. <span data-ttu-id="6a8c7-122">Komut tamamlandıktan sonra açmak `.csproj` dosya eklenen başvurusuna bakın:</span><span class="sxs-lookup"><span data-stu-id="6a8c7-122">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
  <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="10.0.3" />
  </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="6a8c7-123">' % S ' Newtonsoft.Json API uygulamasında kullanma</span><span class="sxs-lookup"><span data-stu-id="6a8c7-123">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="6a8c7-124">Açık `Program.cs` dosya ve dosyanın üst kısmında aşağıdaki satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="6a8c7-124">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="6a8c7-125">Önce aşağıdaki kodu ekleyin `class Program` satır:</span><span class="sxs-lookup"><span data-stu-id="6a8c7-125">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="6a8c7-126">Değiştir `Main` aşağıdaki işleviyle:</span><span class="sxs-lookup"><span data-stu-id="6a8c7-126">Replace the `Main` function with the following:</span></span>

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

1. <span data-ttu-id="6a8c7-127">Derleme ve uygulamayı kullanarak çalıştırma `dotnet run` komutu.</span><span class="sxs-lookup"><span data-stu-id="6a8c7-127">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="6a8c7-128">Çıkış JSON gösterimi olmalıdır `Account` kodu nesnesinde:</span><span class="sxs-lookup"><span data-stu-id="6a8c7-128">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="related-articles"></a><span data-ttu-id="6a8c7-129">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="6a8c7-129">Related articles</span></span>

- [<span data-ttu-id="6a8c7-130">Genel bakış ve iş akışı paket tüketimi</span><span class="sxs-lookup"><span data-stu-id="6a8c7-130">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="6a8c7-131">Paketleri bulma ve seçme</span><span class="sxs-lookup"><span data-stu-id="6a8c7-131">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="6a8c7-132">Bir paketi yüklemek için yollar</span><span class="sxs-lookup"><span data-stu-id="6a8c7-132">Ways to install a package</span></span>](../consume-packages/ways-to-install-a-package.md)
- [<span data-ttu-id="6a8c7-133">NuGet Davranışını Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="6a8c7-133">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
