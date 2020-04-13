---
ms.openlocfilehash: 2fc62e7161a07d739760ed638653fbdec0dfc330
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "68860566"
---
*Paketler* klasöründen eksik olan paketleri indiren ve yükleyen [geri yükleme](../../reference/cli-reference/cli-ref-restore.md) komutunu kullanın.

PackageReference'a geçirilen projeler için, paketleri geri yüklemek için [msbuild -t:geri yükleme'yi](../package-restore.md#restore-using-msbuild) kullanın.

`restore`yalnızca diske paket ekler, ancak projenin bağımlılıklarını değiştirmez. Proje bağımlılıklarını geri `packages.config`yüklemek için `restore` değiştirin ve ardından komutu kullanın.

Diğer `nuget.exe` CLI komutlarında olduğu gibi, önce bir komut satırı açın ve proje dosyanızı içeren dizine geçin.

Bir paketi kullanarak `restore`geri yüklemek için:

```cli
nuget restore MySolution.sln
```