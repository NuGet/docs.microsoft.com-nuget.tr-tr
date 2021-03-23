---
title: DotNet CLı kullanarak bir NuGet paketi yükleyip kullanma
description: Bir .NET Core projesinde NuGet paketini yükleme ve kullanma işlemi hakkında bir adım adım öğretici.
author: JonDouglas
ms.author: jodou
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: dbe1d3ee8e50a90803140bc2c5cb5821b485a2fd
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859440"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a>Hızlı başlangıç: DotNet CLı kullanarak bir paket yükleyip kullanma

NuGet paketleri, diğer geliştiricilerin projelerinizde kullanabileceğiniz bir yeniden kullanılabilir kod içerir. Arka plan için bkz. [NuGet nedir?](../What-is-NuGet.md) . Paketler, `dotnet add package` Bu makalede popüler [Newtonsoft.Js](https://www.nuget.org/packages/Newtonsoft.Json/) paketi için açıklandığı gibi komut kullanılarak bir .NET Core projesine yüklenir.

Yüklendikten sonra, `using <namespace>` kullandığınız pakete özgü olan koddaki pakete bakın \<namespace\> . Daha sonra paketin API 'sini kullanabilirsiniz.

> [!Tip]
> **NuGet.org Ile başlayın**: gözatma NUGET.org, .NET geliştiricilerinin kendi uygulamalarında yeniden kullanabilecekleri bileşenleri genellikle nasıl buldukları. Bu makalede gösterildiği gibi, nuget.org doğrudan arayabilir veya Visual Studio içinde paketleri bulabilir ve yükleyebilirsiniz.

## <a name="prerequisites"></a>Önkoşullar

- [](https://www.microsoft.com/net/download/) `dotnet` Komut satırı aracını sağlayan .NET Core SDK. Visual Studio 2017 ' den başlayarak DotNet CLı, .NET Core ile ilgili iş yükleriyle otomatik olarak yüklenir.

## <a name="create-a-project"></a>Proje oluşturma

NuGet paketleri, bir çeşit .NET projesine yüklenebilir. Bu izlenecek yol için aşağıdaki gibi basit bir .NET Core konsol projesi oluşturun:

1. Proje için bir klasör oluşturun.

1. Bir komut istemi açın ve yeni klasöre geçiş yapın.

1. Aşağıdaki komutu kullanarak projeyi oluşturun:

    ```dotnetcli
    dotnet new console
    ```

1. `dotnet run`Uygulamanın düzgün şekilde oluşturulduğunu test etmek için kullanın.

## <a name="add-the-newtonsoftjson-nuget-package"></a>NuGet paketine Newtonsoft.Jsekleyin

1. Paketini yüklemek için aşağıdaki komutu kullanın `Newtonsoft.json` :

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

2. Komut tamamlandıktan sonra, `.csproj` eklenen başvuruyu görmek için dosyayı açın:

    ```xml
    <ItemGroup>
      <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
    </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Uygulamadaki API Newtonsoft.Jskullanın

1. Dosyasını açın `Program.cs` ve dosyanın en üstüne aşağıdaki satırı ekleyin:

    ```cs
    using Newtonsoft.Json;
    ```

1. Aşağıdaki kodu satırdan önce ekleyin `class Program` :

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. `Main`İşlevi aşağıdaki ile değiştirin:

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

1. Komutunu kullanarak uygulamayı derleyin ve çalıştırın `dotnet run` . Çıktı, koddaki nesnenin JSON temsili olmalıdır `Account` :

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```
## <a name="related-video"></a>İlgili video

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-the-NET-CLI-3-of-5/player]

[Channel 9](https://channel9.msdn.com/Series/NuGet-101) ve [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_)'da daha fazla NuGet videoları bulun.

## <a name="next-steps"></a>Sonraki adımlar

İlk NuGet paketinizi yükleme ve kullanma hakkında Tebrikler!

> [!div class="nextstepaction"]
> [DotNet CLı kullanarak paketleri yükleyip kullanma](../consume-packages/install-use-packages-dotnet-cli.md)

NuGet 'in sunabileceği daha fazlasını araştırmak için aşağıdaki bağlantıları seçin.

- [Paket tüketiminin genel bakış ve iş akışı](../consume-packages/overview-and-workflow.md)
- [Paketleri bulma ve seçme](../consume-packages/finding-and-choosing-packages.md)
- [Proje dosyalarında paket başvuruları](../consume-packages/package-references-in-project-files.md)
