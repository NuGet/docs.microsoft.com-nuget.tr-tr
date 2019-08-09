---
ms.openlocfilehash: 2fc62e7161a07d739760ed638653fbdec0dfc330
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860566"
---
<span data-ttu-id="d992f-101">*Paketler* klasöründe eksik olan paketleri indiren ve yükleyen [restore](../../reference/cli-reference/cli-ref-restore.md) komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="d992f-101">Use the [restore](../../reference/cli-reference/cli-ref-restore.md) command, which downloads and installs any packages missing from the *packages* folder.</span></span>

<span data-ttu-id="d992f-102">PackageReference 'a geçirilen projeler için, bunun yerine paketleri geri yüklemek için [MSBuild-t:restore](../package-restore.md#restore-using-msbuild) kullanın.</span><span class="sxs-lookup"><span data-stu-id="d992f-102">For projects migrated to PackageReference, use [msbuild -t:restore](../package-restore.md#restore-using-msbuild) to restore packages instead.</span></span>

<span data-ttu-id="d992f-103">`restore`yalnızca paketleri diske ekler ancak projenin bağımlılıklarını değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="d992f-103">`restore` only adds packages to disk but does not change a project's dependencies.</span></span> <span data-ttu-id="d992f-104">Proje bağımlılıklarını geri yüklemek için, `packages.config`öğesini değiştirin, sonra `restore` komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="d992f-104">To restore project dependencies, modify `packages.config`, then use the `restore` command.</span></span>

<span data-ttu-id="d992f-105">Diğer `nuget.exe` CLI komutlarında olduğu gibi, önce bir komut satırını açın ve proje dosyanızı içeren dizine geçiş yapın.</span><span class="sxs-lookup"><span data-stu-id="d992f-105">As with the other `nuget.exe` CLI commands, first open a command line and switch to the directory that contains your project file.</span></span>

<span data-ttu-id="d992f-106">Paketini kullanarak `restore`geri yüklemek için:</span><span class="sxs-lookup"><span data-stu-id="d992f-106">To restore a package using `restore`:</span></span>

```cli
nuget restore MySolution.sln
```