---
ms.openlocfilehash: ef54f102352a3d088181ad6f7c356b8c7eeac166
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "74825153"
---
Proje dosyasında listelenen paketleri geri yükleyen [dotnet geri yükleme](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) komutunu kullanın (bkz. [PackageReference).](../../consume-packages/package-references-in-project-files.md) .NET Core 2.0 ve sonraki ile geri `dotnet build` `dotnet run`yükleme ile otomatik olarak yapılır ve. NuGet 4.0 itibariyle, bu `nuget restore`aynı kodu çalışır.

Diğer `dotnet` CLI komutlarında olduğu gibi, önce bir komut satırı açın ve proje dosyanızı içeren dizine geçin.

Bir paketi kullanarak `dotnet restore`geri yüklemek için:

```dotnetcli
dotnet restore 
```