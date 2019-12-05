---
ms.openlocfilehash: ef54f102352a3d088181ad6f7c356b8c7eeac166
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825153"
---
Proje dosyasında listelenen paketleri geri yükleyen [DotNet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) komutunu kullanın (bkz. [packagereference](../../consume-packages/package-references-in-project-files.md)). .NET Core 2,0 ve üzeri ile geri yükleme, `dotnet build` ve `dotnet run`ile otomatik olarak yapılır. NuGet 4,0 itibariyle bu, `nuget restore`ile aynı kodu çalıştırır.

Diğer `dotnet` CLı komutlarında olduğu gibi, önce bir komut satırını açın ve proje dosyanızı içeren dizine geçiş yapın.

`dotnet restore`kullanarak bir paketi geri yüklemek için:

```dotnetcli
dotnet restore 
```