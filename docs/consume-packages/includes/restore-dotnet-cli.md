---
ms.openlocfilehash: 9764479d88cc8d87a9f455e64bd46ae8de15055d
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860597"
---
Proje dosyasında listelenen paketleri geri yükleyen [DotNet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) komutunu kullanın (bkz. [packagereference](../../consume-packages/package-references-in-project-files.md)). .NET Core 2,0 ve üzeri ile geri yükleme, ve `dotnet build` `dotnet run`ile otomatik olarak yapılır. NuGet 4,0 itibariyle bu, ile `nuget restore`aynı kodu çalıştırır.

Diğer `dotnet` CLI komutlarında olduğu gibi, önce bir komut satırını açın ve proje dosyanızı içeren dizine geçiş yapın.

Paketini kullanarak `dotnet restore`geri yüklemek için:

```cli
dotnet restore 
```