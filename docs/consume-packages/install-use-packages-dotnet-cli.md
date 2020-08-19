---
title: DotNet CLı kullanarak NuGet paketlerini yükleyip yönetme
description: NuGet paketleriyle çalışmak için DotNet CLı kullanma yönergeleri.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 38455e61bd91f115df9f27df090ba47a029f6877
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622947"
---
# <a name="install-and-manage-packages-using-the-dotnet-cli"></a>DotNet CLı kullanarak paketleri yükleyip yönetme

CLı Aracı, projelerde ve çözümlerde NuGet paketlerini kolayca yüklemenize, kaldırmanıza ve güncelleştirmenize olanak tanır. Windows, Mac OS X ve Linux üzerinde çalışır.

DotNet CLı, .NET Core ve .NET Standard projesi (SDK stili proje türleri) ve diğer SDK stilindeki projeler (örneğin, .NET Framework hedefleyen SDK stili bir proje) için kullanım içindir. Daha fazla bilgi için bkz. [SDK özniteliği](/dotnet/core/tools/csproj#additions).

Bu makalede, en yaygın DotNet CLı komutlarının birçoğuna ilişkin temel kullanım gösterilmektedir. Bu komutların çoğu için, komutta bir proje dosyası belirtilmediği takdirde (proje dosyası isteğe bağlı bir anahtardır) CLı aracı geçerli dizinde proje dosyası arar. Komutların ve kullanabileceğiniz bağımsız değişkenlerin tam listesi için bkz. [.NET Core komut satırı arabirimi (CLI) araçları](../reference/dotnet-commands.md).

## <a name="prerequisites"></a>Ön koşullar

- [.NET Core SDK](https://www.microsoft.com/net/download/) `dotnet` Komut satırı aracını sağlayan .NET Core SDK. Visual Studio 2017 ' den başlayarak DotNet CLı, .NET Core ile ilgili iş yükleriyle otomatik olarak yüklenir.

## <a name="install-a-package"></a>Paketi yükleme

[DotNet Add paketi](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) proje dosyasına bir paket başvurusu ekler ve ardından `dotnet restore` paketi yüklemek için çalıştırılır.

1. Bir komut satırı açın ve proje dosyanızı içeren dizine geçiş yapın.

2. Bir NuGet paketini yüklemek için aşağıdaki komutu kullanın:

    ```dotnetcli
    dotnet add package <PACKAGE_NAME>
    ```

    Örneğin, paketini yüklemek için `Newtonsoft.Json` aşağıdaki komutu kullanın

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

3. Komut tamamlandıktan sonra, paketin yüklendiğinden emin olmak için proje dosyasına bakın.

   `.csproj`Eklenen başvuruyu görmek için dosyayı açabilirsiniz:

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="install-a-specific-version-of-a-package"></a>Bir paketin belirli bir sürümünü yükler

Sürüm belirtilmemişse, NuGet paketin en son sürümünü yüklenir. Ayrıca, bir NuGet paketinin belirli bir sürümünü yüklemek için [DotNet Add Package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) komutunu da kullanabilirsiniz:

```dotnetcli
dotnet add package <PACKAGE_NAME> --version <VERSION>
```

Örneğin, paketin sürüm 12.0.1 ' i eklemek için `Newtonsoft.Json` Şu komutu kullanın:

```dotnetcli
dotnet add package Newtonsoft.Json --version 12.0.1
```

## <a name="list-package-references"></a>Paket başvurularını Listele

[DotNet List Package](/dotnet/core/tools/dotnet-list-package?tabs=netcore2x) komutunu kullanarak projenizin paket başvurularını listeleyebilirsiniz.

```dotnetcli
dotnet list package
```

## <a name="remove-a-package"></a>Bir paketi kaldırma

Proje dosyasından bir paket başvurusunu kaldırmak için [DotNet Remove Package](/dotnet/core/tools/dotnet-remove-package?tabs=netcore2x) komutunu kullanın.

```dotnetcli
dotnet remove package <PACKAGE_NAME>
```

Örneğin, paketini kaldırmak için `Newtonsoft.Json` aşağıdaki komutu kullanın

```dotnetcli
dotnet remove package Newtonsoft.Json
```

## <a name="update-a-package"></a>Bir paketi güncelleştirme

`dotnet add package`Paket sürümünü (anahtar) belirtmediğiniz takdirde NuGet, komutunu kullandığınızda paketin en son sürümünü yükleme `-v` .

## <a name="restore-packages"></a>Paketleri geri yükleme

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]
