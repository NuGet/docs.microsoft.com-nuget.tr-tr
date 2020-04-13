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
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a>Quickstart: Dotnet CLI'yi kullanarak bir paket yükleyin ve kullanın

NuGet paketleri, diğer geliştiricilerin projelerinizde kullanmak üzere kullanabileceğiniz yeniden kullanılabilir kodlar içerir. NuGet [nedir?](../What-is-NuGet.md) Paketler popüler [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) paketi `dotnet add package` için bu makalede açıklandığı gibi komutu kullanarak bir .NET Core projesine yüklenir.

Yüklendikten sonra, ad alanının `using <namespace>` \<\> kullanmakta olduğunuz pakete özgü olduğu koddaki pakete bakın. Daha sonra paketin API'sini kullanabilirsiniz.

> [!Tip]
> **nuget.org ile başlayın**: nuget.org göz atma ,NET geliştiricilerin genellikle kendi uygulamalarında yeniden kullanabilecekleri bileşenleri nasıl bulduklarıdır. Bu makalede gösterildiği gibi nuget.org doğrudan arayabilir veya Visual Studio'daki paketleri bulup yükleyebilirsiniz.

## <a name="prerequisites"></a>Ön koşullar

- Komut satırı aracını `dotnet` sağlayan [.NET Core SDK.](https://www.microsoft.com/net/download/) Visual Studio 2017'den itibaren dotnet CLI,.NET Core ile ilgili iş yükleriyle otomatik olarak yüklenir.

## <a name="create-a-project"></a>Proje oluşturma

NuGet paketleri bir tür .NET projesine yüklenebilir. Bu iziçin aşağıdaki gibi basit bir .NET Core konsol projesi oluşturun:

1. Proje için bir klasör oluşturun.

1. Komut istemini açın ve yeni klasöre geçin.

1. Aşağıdaki komutu kullanarak projeyi oluşturun:

    ```dotnetcli
    dotnet new console
    ```

1. Uygulamanın düzgün oluşturulduğunu test etmek için kullanın. `dotnet run`

## <a name="add-the-newtonsoftjson-nuget-package"></a>Newtonsoft.Json NuGet paketini ekleyin

1. Paketi yüklemek için aşağıdaki `Newtonsoft.json` komutu kullanın:

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

2. Komut tamamlandıktan sonra, `.csproj` eklenen başvuruyu görmek için dosyayı açın:

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Uygulamada Newtonsoft.Json API'yi kullanın

1. Dosyayı `Program.cs` açın ve dosyanın üst kısmında aşağıdaki satırı ekleyin:

    ```cs
    using Newtonsoft.Json;
    ```

1. `class Program` Satırdan önce aşağıdaki kodu ekleyin:

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. İşlevaşağıdakilerle değiştirin: `Main`

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

1. Komutu kullanarak uygulamayı oluşturun `dotnet run` ve çalıştırın. Çıktı, koddaki nesnenin `Account` JSON gösterimi olmalıdır:

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```
## <a name="related-video"></a>İlgili video

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-the-NET-CLI-3-of-5/player]

[Kanal 9](https://channel9.msdn.com/Series/NuGet-101) ve [YouTube'da](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_)daha fazla NuGet videosu bulun.

## <a name="next-steps"></a>Sonraki adımlar

İlk NuGet paketinizi yükledikten ve kullandığınız için tebrikler!

> [!div class="nextstepaction"]
> [Dotnet CLI kullanarak paketleri yükleyin ve kullanın](../consume-packages/install-use-packages-dotnet-cli.md)

NuGet'in sunduğu daha fazlasını keşfetmek için aşağıdaki bağlantıları seçin.

- [Paket tüketimine genel bakış ve iş akışı](../consume-packages/overview-and-workflow.md)
- [Paketleri bulma ve seçme](../consume-packages/finding-and-choosing-packages.md)
- [Proje dosyalarında paket başvuruları](../consume-packages/package-references-in-project-files.md)
