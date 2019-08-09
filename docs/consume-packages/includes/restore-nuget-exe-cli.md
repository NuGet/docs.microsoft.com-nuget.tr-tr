---
ms.openlocfilehash: 2fc62e7161a07d739760ed638653fbdec0dfc330
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860566"
---
*Paketler* klasöründe eksik olan paketleri indiren ve yükleyen [restore](../../reference/cli-reference/cli-ref-restore.md) komutunu kullanın.

PackageReference 'a geçirilen projeler için, bunun yerine paketleri geri yüklemek için [MSBuild-t:restore](../package-restore.md#restore-using-msbuild) kullanın.

`restore`yalnızca paketleri diske ekler ancak projenin bağımlılıklarını değiştirmez. Proje bağımlılıklarını geri yüklemek için, `packages.config`öğesini değiştirin, sonra `restore` komutunu kullanın.

Diğer `nuget.exe` CLI komutlarında olduğu gibi, önce bir komut satırını açın ve proje dosyanızı içeren dizine geçiş yapın.

Paketini kullanarak `restore`geri yüklemek için:

```cli
nuget restore MySolution.sln
```