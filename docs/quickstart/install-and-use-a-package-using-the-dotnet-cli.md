---
title: Dotnet CLI'yi kullanarak nuget paketi yükleyin ve kullanın
description: .NET Core projesinde NuGet paketinin yüklenmesi ve kullanılması süreci yle ilgili bir iz geçidi öğreticisi.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 006fff8360ac62393e4b88c1a253514591d22f4c
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231285"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="b9d70-103">Quickstart: Dotnet CLI'yi kullanarak bir paket yükleyin ve kullanın</span><span class="sxs-lookup"><span data-stu-id="b9d70-103">Quickstart: Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="b9d70-104">NuGet paketleri, diğer geliştiricilerin projelerinizde kullanmak üzere kullanabileceğiniz yeniden kullanılabilir kodlar içerir.</span><span class="sxs-lookup"><span data-stu-id="b9d70-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="b9d70-105">NuGet [nedir?](../What-is-NuGet.md)</span><span class="sxs-lookup"><span data-stu-id="b9d70-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="b9d70-106">Paketler popüler [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) paketi `dotnet add package` için bu makalede açıklandığı gibi komutu kullanarak bir .NET Core projesine yüklenir.</span><span class="sxs-lookup"><span data-stu-id="b9d70-106">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="b9d70-107">Yüklendikten sonra, ad alanının `using <namespace>` \<\> kullanmakta olduğunuz pakete özgü olduğu koddaki pakete bakın.</span><span class="sxs-lookup"><span data-stu-id="b9d70-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="b9d70-108">Daha sonra paketin API'sini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b9d70-108">You can then use the package's API.</span></span>

> [!Tip]
> <span data-ttu-id="b9d70-109">**nuget.org ile başlayın**: nuget.org göz atma ,NET geliştiricilerin genellikle kendi uygulamalarında yeniden kullanabilecekleri bileşenleri nasıl bulduklarıdır.</span><span class="sxs-lookup"><span data-stu-id="b9d70-109">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="b9d70-110">Bu makalede gösterildiği gibi nuget.org doğrudan arayabilir veya Visual Studio'daki paketleri bulup yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b9d70-110">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9d70-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b9d70-111">Prerequisites</span></span>

- <span data-ttu-id="b9d70-112">Komut satırı aracını `dotnet` sağlayan [.NET Core SDK.](https://www.microsoft.com/net/download/)</span><span class="sxs-lookup"><span data-stu-id="b9d70-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="b9d70-113">Visual Studio 2017'den itibaren dotnet CLI,.NET Core ile ilgili iş yükleriyle otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="b9d70-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="b9d70-114">Proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="b9d70-114">Create a project</span></span>

<span data-ttu-id="b9d70-115">NuGet paketleri bir tür .NET projesine yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="b9d70-115">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="b9d70-116">Bu iziçin aşağıdaki gibi basit bir .NET Core konsol projesi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="b9d70-116">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="b9d70-117">Proje için bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b9d70-117">Create a folder for the project.</span></span>

1. <span data-ttu-id="b9d70-118">Komut istemini açın ve yeni klasöre geçin.</span><span class="sxs-lookup"><span data-stu-id="b9d70-118">Open a command prompt and switch to the new folder.</span></span>

1. <span data-ttu-id="b9d70-119">Aşağıdaki komutu kullanarak projeyi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="b9d70-119">Create the project using the following command:</span></span>

    ```dotnetcli
    dotnet new console
    ```

1. <span data-ttu-id="b9d70-120">Uygulamanın düzgün oluşturulduğunu test etmek için kullanın. `dotnet run`</span><span class="sxs-lookup"><span data-stu-id="b9d70-120">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="b9d70-121">Newtonsoft.Json NuGet paketini ekleyin</span><span class="sxs-lookup"><span data-stu-id="b9d70-121">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="b9d70-122">Paketi yüklemek için aşağıdaki `Newtonsoft.json` komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="b9d70-122">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

2. <span data-ttu-id="b9d70-123">Komut tamamlandıktan sonra, `.csproj` eklenen başvuruyu görmek için dosyayı açın:</span><span class="sxs-lookup"><span data-stu-id="b9d70-123">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="b9d70-124">Uygulamada Newtonsoft.Json API'yi kullanın</span><span class="sxs-lookup"><span data-stu-id="b9d70-124">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="b9d70-125">Dosyayı `Program.cs` açın ve dosyanın üst kısmında aşağıdaki satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b9d70-125">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="b9d70-126">`class Program` Satırdan önce aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b9d70-126">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="b9d70-127">İşlevaşağıdakilerle değiştirin: `Main`</span><span class="sxs-lookup"><span data-stu-id="b9d70-127">Replace the `Main` function with the following:</span></span>

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

1. <span data-ttu-id="b9d70-128">Komutu kullanarak uygulamayı oluşturun `dotnet run` ve çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b9d70-128">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="b9d70-129">Çıktı, koddaki nesnenin `Account` JSON gösterimi olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="b9d70-129">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```
## <a name="related-video"></a><span data-ttu-id="b9d70-130">İlgili video</span><span class="sxs-lookup"><span data-stu-id="b9d70-130">Related video</span></span>

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-the-NET-CLI-3-of-5/player]

<span data-ttu-id="b9d70-131">[Kanal 9](https://channel9.msdn.com/Series/NuGet-101) ve [YouTube'da](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_)daha fazla NuGet videosu bulun.</span><span class="sxs-lookup"><span data-stu-id="b9d70-131">Find more NuGet videos on [Channel 9](https://channel9.msdn.com/Series/NuGet-101) and [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9d70-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b9d70-132">Next steps</span></span>

<span data-ttu-id="b9d70-133">İlk NuGet paketinizi yükledikten ve kullandığınız için tebrikler!</span><span class="sxs-lookup"><span data-stu-id="b9d70-133">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b9d70-134">Dotnet CLI kullanarak paketleri yükleyin ve kullanın</span><span class="sxs-lookup"><span data-stu-id="b9d70-134">Install and use packages using the dotnet CLI</span></span>](../consume-packages/install-use-packages-dotnet-cli.md)

<span data-ttu-id="b9d70-135">NuGet'in sunduğu daha fazlasını keşfetmek için aşağıdaki bağlantıları seçin.</span><span class="sxs-lookup"><span data-stu-id="b9d70-135">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="b9d70-136">Paket tüketimine genel bakış ve iş akışı</span><span class="sxs-lookup"><span data-stu-id="b9d70-136">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="b9d70-137">Paketleri bulma ve seçme</span><span class="sxs-lookup"><span data-stu-id="b9d70-137">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="b9d70-138">Proje dosyalarında paket başvuruları</span><span class="sxs-lookup"><span data-stu-id="b9d70-138">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
