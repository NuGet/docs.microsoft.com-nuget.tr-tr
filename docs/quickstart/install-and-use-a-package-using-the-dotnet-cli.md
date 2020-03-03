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
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a>Hızlı başlangıç: DotNet CLı kullanarak bir paket yükleyip kullanma

NuGet paketleri, diğer geliştiricilerin projelerinizde kullanabileceğiniz bir yeniden kullanılabilir kod içerir. Arka plan için bkz. [NuGet nedir?](../What-is-NuGet.md) . Paketler, popüler [Newtonsoft. JSON](https://www.nuget.org/packages/Newtonsoft.Json/) paketi için bu makalede açıklandığı gibi `dotnet add package` komutu kullanılarak bir .NET Core projesine yüklenir.

Yüklendikten sonra, `using <namespace>` \<ad alanı\> kullandığınız pakete özgü olan koddaki pakete bakın. Daha sonra paketin API 'sini kullanabilirsiniz.

> [!Tip]
> **NuGet.org Ile başlayın**: gözatma NUGET.org, .NET geliştiricilerinin kendi uygulamalarında yeniden kullanabilecekleri bileşenleri genellikle nasıl buldukları. Bu makalede gösterildiği gibi, nuget.org doğrudan arayabilir veya Visual Studio içinde paketleri bulabilir ve yükleyebilirsiniz.

## <a name="prerequisites"></a>Önkoşullar

- `dotnet` komut satırı aracını sağlayan [.NET Core SDK](https://www.microsoft.com/net/download/). Visual Studio 2017 ' den başlayarak DotNet CLı, .NET Core ile ilgili iş yükleriyle otomatik olarak yüklenir.

## <a name="create-a-project"></a>Proje oluşturma

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
