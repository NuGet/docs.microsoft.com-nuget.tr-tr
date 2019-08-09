---
ms.openlocfilehash: 9764479d88cc8d87a9f455e64bd46ae8de15055d
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860597"
---
<span data-ttu-id="6b271-101">Proje dosyasında listelenen paketleri geri yükleyen [DotNet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) komutunu kullanın (bkz. [packagereference](../../consume-packages/package-references-in-project-files.md)).</span><span class="sxs-lookup"><span data-stu-id="6b271-101">Use the [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) command, which restores packages listed in the project file (see [PackageReference](../../consume-packages/package-references-in-project-files.md)).</span></span> <span data-ttu-id="6b271-102">.NET Core 2,0 ve üzeri ile geri yükleme, ve `dotnet build` `dotnet run`ile otomatik olarak yapılır.</span><span class="sxs-lookup"><span data-stu-id="6b271-102">With .NET Core 2.0 and later, restore is done automatically with `dotnet build` and `dotnet run`.</span></span> <span data-ttu-id="6b271-103">NuGet 4,0 itibariyle bu, ile `nuget restore`aynı kodu çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="6b271-103">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>

<span data-ttu-id="6b271-104">Diğer `dotnet` CLI komutlarında olduğu gibi, önce bir komut satırını açın ve proje dosyanızı içeren dizine geçiş yapın.</span><span class="sxs-lookup"><span data-stu-id="6b271-104">As with the other `dotnet` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="6b271-105">Paketini kullanarak `dotnet restore`geri yüklemek için:</span><span class="sxs-lookup"><span data-stu-id="6b271-105">To restore a package using `dotnet restore`:</span></span>

```cli
dotnet restore 
```