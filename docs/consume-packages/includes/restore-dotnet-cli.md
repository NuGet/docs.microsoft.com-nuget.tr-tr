---
ms.openlocfilehash: ef54f102352a3d088181ad6f7c356b8c7eeac166
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "74825153"
---
<span data-ttu-id="56861-101">Proje dosyasında listelenen paketleri geri yükleyen [dotnet geri yükleme](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) komutunu kullanın (bkz. [PackageReference).](../../consume-packages/package-references-in-project-files.md)</span><span class="sxs-lookup"><span data-stu-id="56861-101">Use the [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) command, which restores packages listed in the project file (see [PackageReference](../../consume-packages/package-references-in-project-files.md)).</span></span> <span data-ttu-id="56861-102">.NET Core 2.0 ve sonraki ile geri `dotnet build` `dotnet run`yükleme ile otomatik olarak yapılır ve.</span><span class="sxs-lookup"><span data-stu-id="56861-102">With .NET Core 2.0 and later, restore is done automatically with `dotnet build` and `dotnet run`.</span></span> <span data-ttu-id="56861-103">NuGet 4.0 itibariyle, bu `nuget restore`aynı kodu çalışır.</span><span class="sxs-lookup"><span data-stu-id="56861-103">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>

<span data-ttu-id="56861-104">Diğer `dotnet` CLI komutlarında olduğu gibi, önce bir komut satırı açın ve proje dosyanızı içeren dizine geçin.</span><span class="sxs-lookup"><span data-stu-id="56861-104">As with the other `dotnet` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="56861-105">Bir paketi kullanarak `dotnet restore`geri yüklemek için:</span><span class="sxs-lookup"><span data-stu-id="56861-105">To restore a package using `dotnet restore`:</span></span>

```dotnetcli
dotnet restore 
```