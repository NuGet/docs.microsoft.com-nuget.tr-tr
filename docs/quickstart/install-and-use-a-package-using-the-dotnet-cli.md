---
title: DotNet CLı kullanarak bir NuGet paketi yükleyip kullanma
description: Bir .NET Core projesinde NuGet paketini yükleme ve kullanma işlemi hakkında bir adım adım öğretici.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 006fff8360ac62393e4b88c1a253514591d22f4c
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231285"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="82a65-103">Hızlı başlangıç: DotNet CLı kullanarak bir paket yükleyip kullanma</span><span class="sxs-lookup"><span data-stu-id="82a65-103">Quickstart: Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="82a65-104">NuGet paketleri, diğer geliştiricilerin projelerinizde kullanabileceğiniz bir yeniden kullanılabilir kod içerir.</span><span class="sxs-lookup"><span data-stu-id="82a65-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="82a65-105">Arka plan için bkz. [NuGet nedir?](../What-is-NuGet.md) .</span><span class="sxs-lookup"><span data-stu-id="82a65-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="82a65-106">Paketler, popüler [Newtonsoft. JSON](https://www.nuget.org/packages/Newtonsoft.Json/) paketi için bu makalede açıklandığı gibi `dotnet add package` komutu kullanılarak bir .NET Core projesine yüklenir.</span><span class="sxs-lookup"><span data-stu-id="82a65-106">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="82a65-107">Yüklendikten sonra, `using <namespace>` \<ad alanı\> kullandığınız pakete özgü olan koddaki pakete bakın.</span><span class="sxs-lookup"><span data-stu-id="82a65-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="82a65-108">Daha sonra paketin API 'sini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82a65-108">You can then use the package's API.</span></span>

> [!Tip]
> <span data-ttu-id="82a65-109">**NuGet.org Ile başlayın**: gözatma NUGET.org, .NET geliştiricilerinin kendi uygulamalarında yeniden kullanabilecekleri bileşenleri genellikle nasıl buldukları.</span><span class="sxs-lookup"><span data-stu-id="82a65-109">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="82a65-110">Bu makalede gösterildiği gibi, nuget.org doğrudan arayabilir veya Visual Studio içinde paketleri bulabilir ve yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82a65-110">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82a65-111">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="82a65-111">Prerequisites</span></span>

- <span data-ttu-id="82a65-112">`dotnet` komut satırı aracını sağlayan [.NET Core SDK](https://www.microsoft.com/net/download/).</span><span class="sxs-lookup"><span data-stu-id="82a65-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="82a65-113">Visual Studio 2017 ' den başlayarak DotNet CLı, .NET Core ile ilgili iş yükleriyle otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="82a65-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="82a65-114">Proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="82a65-114">Create a project</span></span>

<span data-ttu-id="82a65-115">NuGet paketleri, bir çeşit .NET projesine yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="82a65-115">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="82a65-116">Bu izlenecek yol için aşağıdaki gibi basit bir .NET Core konsol projesi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="82a65-116">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="82a65-117">Proje için bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="82a65-117">Create a folder for the project.</span></span>

1. <span data-ttu-id="82a65-118">Bir komut istemi açın ve yeni klasöre geçiş yapın.</span><span class="sxs-lookup"><span data-stu-id="82a65-118">Open a command prompt and switch to the new folder.</span></span>

1. <span data-ttu-id="82a65-119">Aşağıdaki komutu kullanarak projeyi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="82a65-119">Create the project using the following command:</span></span>

    ```dotnetcli
    dotnet new console
    ```

1. <span data-ttu-id="82a65-120">Uygulamanın düzgün bir şekilde oluşturulduğunu sınamak için `dotnet run` kullanın.</span><span class="sxs-lookup"><span data-stu-id="82a65-120">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="82a65-121">Newtonsoft. JSON NuGet paketini ekleyin</span><span class="sxs-lookup"><span data-stu-id="82a65-121">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="82a65-122">`Newtonsoft.json` paketini yüklemek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="82a65-122">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

2. <span data-ttu-id="82a65-123">Komut tamamlandıktan sonra, eklenen başvuruyu görmek için `.csproj` dosyasını açın:</span><span class="sxs-lookup"><span data-stu-id="82a65-123">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="82a65-124">Uygulamada Newtonsoft. JSON API 'sini kullanma</span><span class="sxs-lookup"><span data-stu-id="82a65-124">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="82a65-125">`Program.cs` dosyasını açın ve dosyanın en üstüne aşağıdaki satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="82a65-125">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="82a65-126">`class Program` satırından önce aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="82a65-126">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="82a65-127">`Main` işlevini aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="82a65-127">Replace the `Main` function with the following:</span></span>

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

1. <span data-ttu-id="82a65-128">`dotnet run` komutunu kullanarak uygulamayı derleyin ve çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="82a65-128">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="82a65-129">Çıktı, koddaki `Account` nesnesinin JSON temsili olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="82a65-129">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```
## <a name="related-video"></a><span data-ttu-id="82a65-130">İlgili video</span><span class="sxs-lookup"><span data-stu-id="82a65-130">Related video</span></span>

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-the-NET-CLI-3-of-5/player]

<span data-ttu-id="82a65-131">[Channel 9](https://channel9.msdn.com/Series/NuGet-101) ve [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_)'da daha fazla NuGet videoları bulun.</span><span class="sxs-lookup"><span data-stu-id="82a65-131">Find more NuGet videos on [Channel 9](https://channel9.msdn.com/Series/NuGet-101) and [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span></span>

## <a name="next-steps"></a><span data-ttu-id="82a65-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="82a65-132">Next steps</span></span>

<span data-ttu-id="82a65-133">İlk NuGet paketinizi yükleme ve kullanma hakkında Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="82a65-133">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="82a65-134">DotNet CLı kullanarak paketleri yükleyip kullanma</span><span class="sxs-lookup"><span data-stu-id="82a65-134">Install and use packages using the dotnet CLI</span></span>](../consume-packages/install-use-packages-dotnet-cli.md)

<span data-ttu-id="82a65-135">NuGet 'in sunabileceği daha fazlasını araştırmak için aşağıdaki bağlantıları seçin.</span><span class="sxs-lookup"><span data-stu-id="82a65-135">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="82a65-136">Paket tüketiminin genel bakış ve iş akışı</span><span class="sxs-lookup"><span data-stu-id="82a65-136">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="82a65-137">Paketleri bulma ve seçme</span><span class="sxs-lookup"><span data-stu-id="82a65-137">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="82a65-138">Proje dosyalarında paket başvuruları</span><span class="sxs-lookup"><span data-stu-id="82a65-138">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
