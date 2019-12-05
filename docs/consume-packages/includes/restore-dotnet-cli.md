---
ms.openlocfilehash: ef54f102352a3d088181ad6f7c356b8c7eeac166
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825153"
---
<span data-ttu-id="f45c8-101">Proje dosyasında listelenen paketleri geri yükleyen [DotNet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) komutunu kullanın (bkz. [packagereference](../../consume-packages/package-references-in-project-files.md)).</span><span class="sxs-lookup"><span data-stu-id="f45c8-101">Use the [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) command, which restores packages listed in the project file (see [PackageReference](../../consume-packages/package-references-in-project-files.md)).</span></span> <span data-ttu-id="f45c8-102">.NET Core 2,0 ve üzeri ile geri yükleme, `dotnet build` ve `dotnet run`ile otomatik olarak yapılır.</span><span class="sxs-lookup"><span data-stu-id="f45c8-102">With .NET Core 2.0 and later, restore is done automatically with `dotnet build` and `dotnet run`.</span></span> <span data-ttu-id="f45c8-103">NuGet 4,0 itibariyle bu, `nuget restore`ile aynı kodu çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="f45c8-103">As of NuGet 4.0, this runs the same code as `nuget restore`.</span></span>

<span data-ttu-id="f45c8-104">Diğer `dotnet` CLı komutlarında olduğu gibi, önce bir komut satırını açın ve proje dosyanızı içeren dizine geçiş yapın.</span><span class="sxs-lookup"><span data-stu-id="f45c8-104">As with the other `dotnet` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="f45c8-105">`dotnet restore`kullanarak bir paketi geri yüklemek için:</span><span class="sxs-lookup"><span data-stu-id="f45c8-105">To restore a package using `dotnet restore`:</span></span>

```dotnetcli
dotnet restore 
```