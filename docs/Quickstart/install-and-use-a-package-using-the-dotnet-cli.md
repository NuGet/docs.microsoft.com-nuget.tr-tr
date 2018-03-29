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
# <a name="install-and-use-a-package-using-the-dotnet-cli"></a>Yükleme ve dotnet CLI kullanarak bir paket kullanma

NuGet paketleri diğer geliştiriciler projelerinizi kullanmak için kullanılabilir hale yeniden kullanılabilir kod içerir. Bkz: [NuGet nedir?](../What-is-NuGet.md) arka planı için. Paketler, .NET Core kullanarak projesi içine yüklenir `dotnet add package` komutu popüler için bu makalede açıklanan [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) paket.

Koduyla paketinde yüklendikten sonra başvurmak `using <namespace>` nerede \<ad alanı\> kullanmakta olduğunuz paket özeldir. Ardından, paketin API de kullanabilirsiniz.

> [!Tip]
> **Başlat nuget.org ile**: Tarama nuget.org olan nasıl .NET geliştiricilerinin bileşenleri genellikle bulmak, kendi uygulamalarında yeniden kullanabilirsiniz. Nuget.org doğrudan arama veya bulabilir ve bu makalede gösterilen şekilde Visual Studio içindeki paketleri yükleyin.

## <a name="prerequisites"></a>Önkoşullar

- [.NET Core SDK](https://www.microsoft.com/net/download/), sağlayan `dotnet` komut satırı aracı.

## <a name="create-a-project"></a>Proje oluşturma

NuGet paketlerini tür .NET projeye yüklenebilir. Bu kılavuzda gibi basit bir .NET Core konsol projesi oluşturun:

1. Proje için bir klasör oluşturun.

1. Aşağıdaki komutu kullanarak projesi oluşturun:

    ```cli
    dotnet new console
    ```

1. Kullanım `dotnet run` uygulamayı düzgün bir şekilde oluşturulduğunu test etmek için.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Newtonsoft.Json NuGet paketi ekleme

1. Yüklemek için aşağıdaki komutu kullanın `Newtonsoft.json` paketi:

    ```cli
    dotnet add package Newtonsoft.Json
    ```

1. Komut tamamlandıktan sonra açmak `.csproj` dosya eklenen başvurusuna bakın:

    ```xml
  <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="10.0.3" />
  </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>' % S ' Newtonsoft.Json API uygulamasında kullanma

1. Açık `Program.cs` dosya ve dosyanın üst kısmında aşağıdaki satırı ekleyin:

    ```cs
    using Newtonsoft.Json;
    ```

1. Önce aşağıdaki kodu ekleyin `class Program` satır:

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. Değiştir `Main` aşağıdaki işleviyle:

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

1. Derleme ve uygulamayı kullanarak çalıştırma `dotnet run` komutu. Çıkış JSON gösterimi olmalıdır `Account` kodu nesnesinde:

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="related-articles"></a>İlgili makaleler

- [Genel bakış ve iş akışı paket tüketimi](../consume-packages/overview-and-workflow.md)
- [Paketleri bulma ve seçme](../consume-packages/finding-and-choosing-packages.md)
- [Bir paketi yüklemek için yollar](../consume-packages/ways-to-install-a-package.md)
- [NuGet Davranışını Yapılandırma](../consume-packages/configuring-nuget-behavior.md)
