---
title: DotNet CLı kullanarak bir NuGet paketi yükleyip kullanma
description: Bir .NET Core projesinde NuGet paketini yükleme ve kullanma işlemi hakkında bir adım adım öğretici.
author: JonDouglas
ms.author: jodou
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: adbf8f457d8520e3087e539b91ef932877aec3a0
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775453"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="af568-103">Hızlı başlangıç: DotNet CLı kullanarak bir paket yükleyip kullanma</span><span class="sxs-lookup"><span data-stu-id="af568-103">Quickstart: Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="af568-104">NuGet paketleri, diğer geliştiricilerin projelerinizde kullanabileceğiniz bir yeniden kullanılabilir kod içerir.</span><span class="sxs-lookup"><span data-stu-id="af568-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="af568-105">Arka plan için bkz. [NuGet nedir?](../What-is-NuGet.md) .</span><span class="sxs-lookup"><span data-stu-id="af568-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="af568-106">Paketler, `dotnet add package` Bu makalede popüler [Newtonsoft.Js](https://www.nuget.org/packages/Newtonsoft.Json/) paketi için açıklandığı gibi komut kullanılarak bir .NET Core projesine yüklenir.</span><span class="sxs-lookup"><span data-stu-id="af568-106">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="af568-107">Yüklendikten sonra, `using <namespace>` kullandığınız pakete özgü olan koddaki pakete bakın \<namespace\> .</span><span class="sxs-lookup"><span data-stu-id="af568-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="af568-108">Daha sonra paketin API 'sini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="af568-108">You can then use the package's API.</span></span>

> [!Tip]
> <span data-ttu-id="af568-109">**NuGet.org Ile başlayın**: gözatma NUGET.org, .NET geliştiricilerinin kendi uygulamalarında yeniden kullanabilecekleri bileşenleri genellikle nasıl buldukları.</span><span class="sxs-lookup"><span data-stu-id="af568-109">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="af568-110">Bu makalede gösterildiği gibi, nuget.org doğrudan arayabilir veya Visual Studio içinde paketleri bulabilir ve yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="af568-110">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="af568-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="af568-111">Prerequisites</span></span>

- <span data-ttu-id="af568-112">[](https://www.microsoft.com/net/download/) `dotnet` Komut satırı aracını sağlayan .NET Core SDK.</span><span class="sxs-lookup"><span data-stu-id="af568-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="af568-113">Visual Studio 2017 ' den başlayarak DotNet CLı, .NET Core ile ilgili iş yükleriyle otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="af568-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="af568-114">Proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="af568-114">Create a project</span></span>

<span data-ttu-id="af568-115">NuGet paketleri, bir çeşit .NET projesine yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="af568-115">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="af568-116">Bu izlenecek yol için aşağıdaki gibi basit bir .NET Core konsol projesi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="af568-116">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="af568-117">Proje için bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="af568-117">Create a folder for the project.</span></span>

1. <span data-ttu-id="af568-118">Bir komut istemi açın ve yeni klasöre geçiş yapın.</span><span class="sxs-lookup"><span data-stu-id="af568-118">Open a command prompt and switch to the new folder.</span></span>

1. <span data-ttu-id="af568-119">Aşağıdaki komutu kullanarak projeyi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="af568-119">Create the project using the following command:</span></span>

    ```dotnetcli
    dotnet new console
    ```

1. <span data-ttu-id="af568-120">`dotnet run`Uygulamanın düzgün şekilde oluşturulduğunu test etmek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="af568-120">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="af568-121">NuGet paketine Newtonsoft.Jsekleyin</span><span class="sxs-lookup"><span data-stu-id="af568-121">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="af568-122">Paketini yüklemek için aşağıdaki komutu kullanın `Newtonsoft.json` :</span><span class="sxs-lookup"><span data-stu-id="af568-122">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

2. <span data-ttu-id="af568-123">Komut tamamlandıktan sonra, `.csproj` eklenen başvuruyu görmek için dosyayı açın:</span><span class="sxs-lookup"><span data-stu-id="af568-123">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="af568-124">Uygulamadaki API Newtonsoft.Jskullanın</span><span class="sxs-lookup"><span data-stu-id="af568-124">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="af568-125">Dosyasını açın `Program.cs` ve dosyanın en üstüne aşağıdaki satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="af568-125">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="af568-126">Aşağıdaki kodu satırdan önce ekleyin `class Program` :</span><span class="sxs-lookup"><span data-stu-id="af568-126">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="af568-127">`Main`İşlevi aşağıdaki ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="af568-127">Replace the `Main` function with the following:</span></span>

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

1. <span data-ttu-id="af568-128">Komutunu kullanarak uygulamayı derleyin ve çalıştırın `dotnet run` .</span><span class="sxs-lookup"><span data-stu-id="af568-128">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="af568-129">Çıktı, koddaki nesnenin JSON temsili olmalıdır `Account` :</span><span class="sxs-lookup"><span data-stu-id="af568-129">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```
## <a name="related-video"></a><span data-ttu-id="af568-130">İlgili video</span><span class="sxs-lookup"><span data-stu-id="af568-130">Related video</span></span>

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-the-NET-CLI-3-of-5/player]

<span data-ttu-id="af568-131">[Channel 9](https://channel9.msdn.com/Series/NuGet-101) ve [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_)'da daha fazla NuGet videoları bulun.</span><span class="sxs-lookup"><span data-stu-id="af568-131">Find more NuGet videos on [Channel 9](https://channel9.msdn.com/Series/NuGet-101) and [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span></span>

## <a name="next-steps"></a><span data-ttu-id="af568-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="af568-132">Next steps</span></span>

<span data-ttu-id="af568-133">İlk NuGet paketinizi yükleme ve kullanma hakkında Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="af568-133">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="af568-134">DotNet CLı kullanarak paketleri yükleyip kullanma</span><span class="sxs-lookup"><span data-stu-id="af568-134">Install and use packages using the dotnet CLI</span></span>](../consume-packages/install-use-packages-dotnet-cli.md)

<span data-ttu-id="af568-135">NuGet 'in sunabileceği daha fazlasını araştırmak için aşağıdaki bağlantıları seçin.</span><span class="sxs-lookup"><span data-stu-id="af568-135">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="af568-136">Paket tüketiminin genel bakış ve iş akışı</span><span class="sxs-lookup"><span data-stu-id="af568-136">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="af568-137">Paketleri bulma ve seçme</span><span class="sxs-lookup"><span data-stu-id="af568-137">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="af568-138">Proje dosyalarında paket başvuruları</span><span class="sxs-lookup"><span data-stu-id="af568-138">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
