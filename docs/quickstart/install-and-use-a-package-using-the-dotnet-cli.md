---
title: DotNet CLı kullanarak bir NuGet paketi yükleyip kullanma
description: Bir .NET Core projesinde NuGet paketini yükleme ve kullanma işlemi hakkında bir adım adım öğretici.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: ee456fd49675db37fee78dc14502a897d84a2b99
ms.sourcegitcommit: 0f5363353f9dc1c3d68e7718f51b7ff92bb35e21
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68342464"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a>Hızlı Başlangıç: DotNet CLı kullanarak bir paket yükleyip kullanma

NuGet paketleri, diğer geliştiricilerin projelerinizde kullanabileceğiniz bir yeniden kullanılabilir kod içerir. Arka plan için bkz. [NuGet nedir?](../What-is-NuGet.md) . Paketler, popüler [Newtonsoft. JSON](https://www.nuget.org/packages/Newtonsoft.Json/) paketi için `dotnet add package` Bu makalede açıklandığı gibi komut kullanılarak bir .NET Core projesine yüklenir.

Yüklendikten sonra, koddaki `using <namespace>` \<pakete, ad alanının\> kullandığınız pakete özgü olduğunu bakın. Daha sonra paketin API 'sini kullanabilirsiniz.

> [!Tip]
> **NuGet.org Ile Başlat**: Nuget.org gözatma, .NET geliştiricilerinin kendi uygulamalarında yeniden kullanabilecekleri bileşenleri genellikle bulmasıdır. Bu makalede gösterildiği gibi, nuget.org doğrudan arayabilir veya Visual Studio içinde paketleri bulabilir ve yükleyebilirsiniz.

## <a name="prerequisites"></a>Önkoşullar

- `dotnet` Komut satırı aracını sağlayan [.NET Core SDK](https://www.microsoft.com/net/download/). Visual Studio 2017 ' den başlayarak DotNet CLı, .NET Core ile ilgili iş yükleriyle otomatik olarak yüklenir.

## <a name="create-a-project"></a>Proje oluşturma

NuGet paketleri, bir çeşit .NET projesine yüklenebilir. Bu izlenecek yol için aşağıdaki gibi basit bir .NET Core konsol projesi oluşturun:

1. Proje için bir klasör oluşturun.

1. Aşağıdaki komutu kullanarak projeyi oluşturun:

    ```cli
    dotnet new console
    ```

1. Uygulamanın `dotnet run` düzgün şekilde oluşturulduğunu test etmek için kullanın.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Newtonsoft. JSON NuGet paketini ekleyin

1. `Newtonsoft.json` Paketini yüklemek için aşağıdaki komutu kullanın:

    ```cli
    dotnet add package Newtonsoft.Json
    ```

2. Komut tamamlandıktan sonra, eklenen başvuruyu görmek `.csproj` için dosyayı açın:

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Uygulamada Newtonsoft. JSON API 'sini kullanma

1. `Program.cs` Dosyasını açın ve dosyanın en üstüne aşağıdaki satırı ekleyin:

    ```cs
    using Newtonsoft.Json;
    ```

1. Aşağıdaki kodu `class Program` satırdan önce ekleyin:

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. `Main` İşlevi aşağıdaki ile değiştirin:

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

1. `dotnet run` Komutunu kullanarak uygulamayı derleyin ve çalıştırın. Çıktı, koddaki `Account` nesnenin JSON temsili olmalıdır:

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="next-steps"></a>Sonraki adımlar

İlk NuGet paketinizi yükleme ve kullanma hakkında Tebrikler!

> [!div class="nextstepaction"]
> [DotNet CLı kullanarak paketleri yükleyip kullanma](../consume-packages/install-use-packages-dotnet-cli.md)

NuGet 'in sunabileceği daha fazlasını araştırmak için aşağıdaki bağlantıları seçin.

- [Paket tüketiminin genel bakış ve iş akışı](../consume-packages/overview-and-workflow.md)
- [Paketleri bulma ve seçme](../consume-packages/finding-and-choosing-packages.md)
- [Proje dosyalarında paket başvuruları](../consume-packages/package-references-in-project-files.md)
