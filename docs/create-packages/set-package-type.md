---
title: NuGet paket türünü ayarlama
description: Paketin kullanım amacını belirtmek için paket türlerini açıklar.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 1d869f616ce0291cf1c0a17b7ff20fc61e6a3bd5
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "78230830"
---
# <a name="set-a-nuget-package-type"></a>NuGet paket türünü ayarlama

NuGet 3.5+ ile paketler, kullanım amacını belirtmek için belirli bir *paket türüyle* işaretlenebilir. NuGet'in önceki sürümleriyle oluşturulan tüm paketler de dahil olmak `Dependency` üzere bir türle işaretlenmemiş paketler varsayılan türe benzer.

- `Dependency`tür paketleri kitaplıklara ve uygulamalara yapı veya çalışma zamanı varlıkları ekler ve herhangi bir proje türüne (uyumlu oldukları varsayarak) yüklenebilir.

- `DotnetTool`tip paketleri [dotnet CLI](/dotnet/articles/core/tools/index) uzantıları ve komut satırından çağrılır. Bu tür paketler yalnızca .NET Core projelerine yüklenebilir ve geri yükleme işlemleri üzerinde hiçbir etkisi yoktur. Proje başına bu uzantılar hakkında daha fazla ayrıntı [.NET Core genişletilebilirlik](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) belgelerinde mevcuttur.

- `Template`tür paketleri, uygulama, hizmet, araç veya sınıf kitaplığı gibi dosya veya proje oluşturmak için kullanılabilecek [özel şablonlar](/dotnet/core/tools/custom-templates) sağlar.

- Özel tür paketleri, paket kimliklerle aynı biçim kurallarına uyan rasgele bir tür tanımlayıcı kullanır. `Dependency` Ancak Visual Studio'daki NuGet Paket Yöneticisi tarafından tanınmaz. `DotnetTool`

Paket türleri `.nuspec` dosyada ayarlanır. Türü açıkça *ayarlamamak* ve bunun yerine hiçbir `Dependency` tür belirtilmediğinde bu türü varsayarak NuGet'e güvenmek geriye dönük uyumluluk için en iyisidir.

- `.nuspec`: Öğenin altındaki `packageTypes\packageType` bir düğüm `<metadata>` içindeki paket türünü belirtin:

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
