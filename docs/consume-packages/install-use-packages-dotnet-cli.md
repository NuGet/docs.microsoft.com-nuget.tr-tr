---
title: Yükleme ve dotnet CLI kullanarak NuGet paketlerini Yönet
description: NuGet paketleri ile çalışmak için dotnet CLI kullanma yönergeleri.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 64f3a1978cd336064a77c9f3872357e65c37fc10
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842353"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a>Yükleme ve dotnet CLI kullanarak paketleri yönetme

CLI aracı, kolayca yükleme, kaldırma ve projelerde ve çözümlerde NuGet paketlerini güncelleştirme olanak sağlar. İşlem, Windows, Mac OS X ve Linux üzerinde çalışır.

Dotnet CLI projenizde .NET Core ve .NET Standard (SDK stilinde proje türleri) için ve tüm diğer SDK stili projeleri (örneğin, .NET Framework hedefleyen bir SDK stilinde Proje) içindir. Daha fazla bilgi için [SDK özniteliği](/dotnet/core/tools/csproj#additions).

Bu makalede en yaygın dotnet CLI komutları birkaç temel kullanımını gösterir. Bir proje dosyası (isteğe bağlı bir anahtar proje dosyasıdır) komutta belirtilmediği sürece bu komutların çoğu için CLI aracı bir proje dosyasını geçerli dizinde arar. Komut ve bağımsız değişkenler kullanabilirsiniz tam listesi için bkz: [.NET Core komut satırı arabirimi (CLI) araçlarını](../tools/dotnet-commands.md).

## <a name="prerequisites"></a>Önkoşullar

- [.NET Core SDK'sı](https://www.microsoft.com/net/download/), sağlayan `dotnet` komut satırı aracı. Dotnet CLI herhangi bir .NET Core ile otomatik olarak yüklenir, Visual Studio 2017'de başlayarak, iş yüklerini ilgili.

## <a name="install-a-package"></a>Paket yükleme

[DotNet paketini ekleyin](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) proje dosyasına bir paket başvurusu ekler ve ardından çalışan `dotnet restore` paketi yükleyin.

1. Bir komut satırı açın ve proje dosyanızı içeren dizine geçin.

2. Bir Nuget paketini yüklemek için aşağıdaki komutu kullanın:

    ```cli
    dotnet add package <PACKAGE_NAME>
    ```

    Örneğin, yükleme için `Newtonsoft.Json` paket, aşağıdaki komutu kullanın

    ```cli
    dotnet add package Newtonsoft.Json
    ```

3. Komut tamamlandıktan sonra paket emin olmak için proje dosyasını göz yüklendi.

   Açabileceğiniz `.csproj` dosya eklendi başvuru görmek için:

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a>Bir paketi belirli bir sürümünü yükleme

Sürüm belirtilmezse, NuGet paketinin en son sürümünü yükler. Ayrıca [dotnet paketini ekleyin](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) bir Nuget paketi belirli bir sürümünü yüklemek için komutu:

```cli
dotnet add package <PACKAGE_NAME> -v <VERSION>
```

Örneğin, 12.0.1 sürümünü eklemek için `Newtonsoft.Json` paketi, bu komutu kullanın:

```cli
dotnet add package Newtonsoft.Json -v 12.0.1
```

## <a name="list-package-references"></a>Liste paket başvuruları

Paket başvuruları için kullanarak projenize listeleyebilirsiniz [dotnet paket listeleme](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) komutu.

```cli
dotnet list package
```

## <a name="remove-a-package"></a>Paket kaldırma

Kullanım [dotnet paketi kaldırma](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) proje dosyasından bir paket başvurusu kaldırmak için komutu.

```cli
dotnet remove package <PACKAGE_NAME>
```

Örneğin, kaldırmak için `Newtonsoft.Json` paket, aşağıdaki komutu kullanın

```cli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a>Güncelleştirme paketi

NuGet paketinin en son sürümünü yükler kullandığınızda `dotnet add package` Paket sürümü belirtmediğiniz sürece komutu (`-v` geçiş).

## <a name="restore-packages"></a>Paketleri geri yükle

Kullanım [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) komutu, proje dosyasında listelenen paketleri geri yükler (bkz [PackageReference](../consume-packages/package-references-in-project-files.md)). .NET Core 2.0 ve daha sonra geri yükleme ile otomatik olarak gerçekleştirilir `dotnet build` ve `dotnet run`. Bu NuGet 4.0 itibariyle, aynı kodu çalıştıran `nuget restore`.

Olan diğer `dotnet` CLI komutları, ilk olarak bir komut satırı açın ve proje dosyanızı içeren dizine geçin.

Bir paketi kullanarak geri yüklemek için `dotnet restore`:

```cli
dotnet restore 
```
