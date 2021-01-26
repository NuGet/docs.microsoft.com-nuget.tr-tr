---
title: NuGet paket türü ayarla
description: Bir paketin amaçlanan kullanımını göstermek için paket türlerini açıklar.
author: JonDouglas
ms.author: jodou
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 990ac580f4031615566d78e359a24eaedaaf3e07
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774363"
---
# <a name="set-a-nuget-package-type"></a>NuGet paket türü ayarla

NuGet 3.5 + ile, paketleri amaçlanan kullanımını göstermek için belirli bir *paket türüyle* işaretlenebilir. Daha önceki NuGet sürümleriyle oluşturulan tüm paketler de dahil olmak üzere bir tür ile işaretlenmemiş paketler, varsayılan olarak `Dependency` türü.

- `Dependency` tür paketleri kitaplıklara ve uygulamalarına derleme veya çalışma zamanı varlıkları ekleyin ve herhangi bir proje türüne (uyumlu oldukları varsayılarak) yüklenebilir.

- `DotnetTool` tür paketleri [DotNet CLI](/dotnet/articles/core/tools/index) için uzantılardır ve komut satırından çağırılır. Bu tür paketler yalnızca .NET Core projelerine yüklenebilir ve geri yükleme işlemlerini etkilemez. Bu proje başına uzantılar hakkında daha fazla ayrıntı  [.NET Core genişletilebilirlik](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) belgelerinde bulunabilir.

- `Template` tür paketleri, bir uygulama, hizmet, araç veya sınıf kitaplığı gibi dosyalar ya da projeler oluşturmak için kullanılabilecek [özel şablonlar](/dotnet/core/tools/custom-templates) sağlar.

- Özel tür paketleri paket kimlikleriyle aynı biçim kurallarına uyan rastgele bir tür tanımlayıcısı kullanır. Ancak dışındaki herhangi bir `Dependency` tür `DotnetTool` , Visual Studio 'Daki NuGet Paket Yöneticisi tarafından tanınmaz.

Paket türleri `.nuspec` dosyasında ayarlanır. Açık uyumluluğun türü açıkça *ayarlanmamak* `Dependency` ve bunun yerine, hiçbir tür belirtilmediğinde bu türü kabul eden NuGet 'e dayanması için en iyi seçenektir.

- `.nuspec`: Öğe altındaki bir düğüm içinde paket türünü belirtin `packageTypes\packageType` `<metadata>` :

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetTool" />
        </packageTypes>
        </metadata>
    </package>
    ```
