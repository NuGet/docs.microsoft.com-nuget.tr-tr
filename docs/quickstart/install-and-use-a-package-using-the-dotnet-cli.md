---
title: DotNet CLı kullanarak bir NuGet paketi yükleyip kullanma
description: Bir .NET Core projesinde NuGet paketini yükleme ve kullanma işlemi hakkında bir adım adım öğretici.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 9b6eb012b4bc8135b1648fa9f5e84d7d1c9d6b16
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825354"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a>Hızlı başlangıç: DotNet CLı kullanarak bir paket yükleyip kullanma

NuGet paketleri, diğer geliştiricilerin projelerinizde kullanabileceğiniz bir yeniden kullanılabilir kod içerir. Arka plan için bkz. [NuGet nedir?](../What-is-NuGet.md) . Paketler, popüler [Newtonsoft. JSON](https://www.nuget.org/packages/Newtonsoft.Json/) paketi için bu makalede açıklandığı gibi `dotnet add package` komutu kullanılarak bir .NET Core projesine yüklenir.

Yüklendikten sonra, `using <namespace>` \<ad alanı\> kullandığınız pakete özgü olan koddaki pakete bakın. Daha sonra paketin API 'sini kullanabilirsiniz.

> [!Tip]
> **NuGet.org Ile başlayın**: gözatma NUGET.org, .NET geliştiricilerinin kendi uygulamalarında yeniden kullanabilecekleri bileşenleri genellikle nasıl buldukları. Bu makalede gösterildiği gibi, nuget.org doğrudan arayabilir veya Visual Studio içinde paketleri bulabilir ve yükleyebilirsiniz.

## <a name="prerequisites"></a>Prerequisites

- `dotnet` komut satırı aracını sağlayan [.NET Core SDK](https://www.microsoft.com/net/download/). Visual Studio 2017 ' den başlayarak DotNet CLı, .NET Core ile ilgili iş yükleriyle otomatik olarak yüklenir.

## <a name="create-a-project"></a>Proje oluştur

NuGet paketleri, bir çeşit .NET projesine yüklenebilir. Bu izlenecek yol için aşağıdaki gibi basit bir .NET Core konsol projesi oluşturun:

1. Proje için bir klasör oluşturun.

1. Bir komut istemi açın ve yeni klasöre geçiş yapın.

1. Aşağıdaki komutu kullanarak projeyi oluşturun:

    ```dotnetcli
    dotnet new console
    ```

1. Uygulamanın düzgün bir şekilde oluşturulduğunu sınamak için `dotnet run` kullanın.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Newtonsoft. JSON NuGet paketini ekleyin

1. `Newtonsoft.json` paketini yüklemek için aşağıdaki komutu kullanın:

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

2. Komut tamamlandıktan sonra, eklenen başvuruyu görmek için `.csproj` dosyasını açın:

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Uygulamada Newtonsoft. JSON API 'sini kullanma

1. `Program.cs` dosyasını açın ve dosyanın en üstüne aşağıdaki satırı ekleyin:

    ```cs
    using Newtonsoft.Json;
    ```

1. `class Program` satırından önce aşağıdaki kodu ekleyin:

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. `Main` işlevini aşağıdaki kodla değiştirin:

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

1. `dotnet run` komutunu kullanarak uygulamayı derleyin ve çalıştırın. Çıktı, koddaki `Account` nesnesinin JSON temsili olmalıdır:

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
