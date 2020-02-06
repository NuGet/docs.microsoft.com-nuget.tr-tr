---
title: NuGet paket türü ayarla
description: Bir paketin amaçlanan kullanımını göstermek için paket türlerini açıklar.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 22e8ac2e9e2086a1280c5b0c3be8a032b7998b36
ms.sourcegitcommit: 415c70d7014545c1f65271a2debf8c3c1c5eb688
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/06/2020
ms.locfileid: "77036922"
---
# <a name="set-a-nuget-package-type"></a>NuGet paket türü ayarla

NuGet 3.5 + ile, paketleri amaçlanan kullanımını göstermek için belirli bir *paket türüyle* işaretlenebilir. Daha önceki NuGet sürümleriyle oluşturulan tüm paketler de dahil olmak üzere bir türle işaretlenmemiş paketler, varsayılan olarak `Dependency` türüdür.

- `Dependency` tür paketleri kitaplıklara ve uygulamalara derleme veya çalışma zamanı varlıkları ekler ve herhangi bir proje türüne (uyumlu oldukları varsayılarak) yüklenebilir.

- `DotnetTool` tür paketleri [DotNet CLI](/dotnet/articles/core/tools/index) için uzantılardır ve komut satırından çağırılır. Bu tür paketler yalnızca .NET Core projelerine yüklenebilir ve geri yükleme işlemlerini etkilemez. Bu proje başına uzantılar hakkında daha fazla ayrıntı [.NET Core genişletilebilirlik](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) belgelerinde bulunabilir.

- `Template` tür paketleri, bir uygulama, hizmet, araç veya sınıf kitaplığı gibi dosyalar ya da projeler oluşturmak için kullanılabilecek [özel şablonlar](/dotnet/core/tools/custom-templates) sağlar.

- Özel tür paketleri paket kimlikleriyle aynı biçim kurallarına uyan rastgele bir tür tanımlayıcısı kullanır. Ancak `Dependency` ve `DotnetTool`dışındaki herhangi bir tür, Visual Studio 'daki NuGet Paket Yöneticisi tarafından tanınmaz.

Paket türleri `.nuspec` dosyasında ayarlanır. `Dependency` türü açıkça *ayarlanmamak* ve bunun yerine, hiçbir tür belirtilmediğinde bu türü kabul eden NuGet 'i kullanmak için geriye dönük uyumluluk için idealdir.

- `.nuspec`: `<metadata>` öğesi altındaki bir `packageTypes\packageType` düğümü içindeki paket türünü gösterir:

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetTool" />
        </packageTypes>
        </metadata>
    </package>
    ```
