---
title: Kullanarak NuGet paketleri aracılığıyla dotnet CLI için tanıtım Kılavuzu
description: Bir NuGet paketi kullanarak bir .NET Core projesinde ve yükleme işlemini bir gözden geçirme öğretici.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 0d637c441cf9f36e8e3e04e47b524b2defecae52
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67841665"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a>Hızlı Başlangıç: Dotnet CLI kullanarak bir paket yükleyip

NuGet paketleri diğer geliştiriciler projelerinizde kullanmak için kullanılabilir hale yeniden kullanılabilir bir kod içerir. Bkz: [NuGet nedir?](../What-is-NuGet.md) arka planı. Paketleri kullanarak bir .NET Core projesi yüklü `dotnet add package` komutu popüler için bu makalede anlatıldığı gibi [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) paket.

Kod ile paket yüklendikten sonra başvurmak `using <namespace>` burada \<ad alanı\> kullanmakta olduğunuz paket özgüdür. Ardından, paket API'si de kullanabilirsiniz.

> [!Tip]
> **Nuget.org ile Başlat**: Gözatma nuget.org'nin olduğundan nasıl .NET geliştiricilerinin bileşenler genellikle bulun, kendi uygulamalarında yeniden kullanabilirsiniz. Nuget.org doğrudan arama veya bulabilir ve bu makalede gösterilen şekilde Visual Studio içindeki paketleri yükleyin.

## <a name="prerequisites"></a>Önkoşullar

- [.NET Core SDK'sı](https://www.microsoft.com/net/download/), sağlayan `dotnet` komut satırı aracı. Dotnet CLI herhangi bir .NET Core ile otomatik olarak yüklenir, Visual Studio 2017'de başlayarak, iş yüklerini ilgili.

## <a name="create-a-project"></a>Proje oluşturma

NuGet paketlerini, tür bir .NET projesine yüklenebilir. Bu kılavuz için şu şekilde basit bir .NET Core konsol projesi oluşturun:

1. Proje için bir klasör oluşturun.

1. Aşağıdaki komutu kullanarak proje oluştur:

    ```cli
    dotnet new console
    ```

1. Kullanım `dotnet run` uygulamayı düzgün bir şekilde oluşturulduğunu test etmek için.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Newtonsoft.Json NuGet paketi ekleme

1. Yüklemek için aşağıdaki komutu kullanın `Newtonsoft.json` paket:

    ```cli
    dotnet add package Newtonsoft.Json
    ```

2. Komut tamamlandıktan sonra açın `.csproj` dosya eklendi başvuru görmek için:

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>' % S ' Newtonsoft.Json API uygulamasında kullanma

1. Açık `Program.cs` dosya ve dosyasının en üstüne aşağıdaki satırı ekleyin:

    ```cs
    using Newtonsoft.Json;
    ```

1. Önce aşağıdaki kodu ekleyin `class Program` satırı:

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. Değiştirin `Main` işlevi aşağıdaki:

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

1. Kullanarak uygulaması derleyebilir ve `dotnet run` komutu. Çıkış JSON gösterimi olmalıdır `Account` kod nesnesinde:

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="related-articles"></a>İlgili makaleler

- [Dotnet CLI kullanarak paketleri yükleyip](../consume-packages/install-use-packages-dotnet-cli.md)
- [Genel bakış ve paket tüketim iş akışı](../consume-packages/overview-and-workflow.md)
- [Paketleri bulma ve seçme](../consume-packages/finding-and-choosing-packages.md)
- [Ortak NuGet yapılandırmaları](../consume-packages/configuring-nuget-behavior.md)
