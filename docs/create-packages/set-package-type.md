---
title: Bir NuGet paketi türü
description: Bir paketin kullanım amacını belirtmek için paket türleri açıklanmaktadır.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 8a3ba6af19125b75af17cab8c093e89485e20324
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67843535"
---
# <a name="set-a-nuget-package-type"></a>Bir NuGet paketi türü

NuGet ile 3.5 +, paketleri ile belirli bir işaretlenebilir *paket türü* kullanım amacı belirtmek için. NuGet, önceki sürümleriyle oluşturulan tüm paketleri de dahil olmak üzere, bir tür ile işaretlenmemiş paketleri varsayılan `Dependency` türü.

- `Dependency` türü paketler, kitaplıkları ve uygulamaları için derleme veya çalışma zamanı varlıklar eklemek ve (uyumlu olduklarından varsayılarak) herhangi bir proje türü yüklenebilir.

- `DotnetCliTool` tür paketlerin uzantıları [dotnet CLI](/dotnet/articles/core/tools/index) ve komut satırından çağrılır. Bu paketler, yalnızca .NET Core projelerinde yüklenebilir ve geri yükleme işlemleri üzerinde hiçbir etkisi yoktur. Bu proje başına uzantılar hakkında daha fazla ayrıntı kullanılabilir [.NET Core genişletilebilirlik](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) belgeleri.

- Özel tür paketleri paket kimliği olarak aynı biçimi kurallara uyan bir rastgele tür tanımlayıcısı kullanın. Dışında herhangi türdeki `Dependency` ve `DotnetCliTool`, ancak Visual Studio'da NuGet Paket Yöneticisi tarafından tanınmıyor.

Paket türlerinin ayarlanır `.nuspec` dosya. Geriye dönük için en iyi uyumluluk *değil* açıkça ayarlanmış `Dependency` yazın ve bunun yerine NuGet varsayılarak türü yok, bu tür üzerinde yararlanmayı belirtilir.

- `.nuspec`: Paket türü içinde göstermek bir `packageTypes\packageType` düğümünde `<metadata>` öğesi:

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetCliTool" />
        </packageTypes>
        </metadata>
    </package>
    ```
