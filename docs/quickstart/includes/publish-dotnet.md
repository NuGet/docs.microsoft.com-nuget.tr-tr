---
ms.openlocfilehash: bb39e1056ea97ecf1ac70d7fd8e79e65dc04655c
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842133"
---
1. Değiştirmek için içeren klasör `.nupkg` dosya.

1. Paketinizin adını (benzersiz paket kimliği) belirtme ve API anahtarınızı anahtar değerini değiştirerek aşağıdaki komutu çalıştırın:

    ```cli
    dotnet nuget push AppLogger.1.0.0.nupkg -k qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -s https://api.nuget.org/v3/index.json
    ```

1. DotNet yayımlama işleminin sonuçlarını görüntüler:

    ```output
    info : Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
    info :   PUT https://www.nuget.org/api/v2/package/
    info :   Created https://www.nuget.org/api/v2/package/ 12620ms
    info : Your package was pushed.
    ```

Bkz: [dotnet nuget anında iletme](/dotnet/core/tools/dotnet-nuget-push).