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
# <a name="set-a-nuget-package-type"></a><span data-ttu-id="5ceba-103">NuGet paket türü ayarla</span><span class="sxs-lookup"><span data-stu-id="5ceba-103">Set a NuGet package type</span></span>

<span data-ttu-id="5ceba-104">NuGet 3.5 + ile, paketleri amaçlanan kullanımını göstermek için belirli bir *paket türüyle* işaretlenebilir.</span><span class="sxs-lookup"><span data-stu-id="5ceba-104">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="5ceba-105">Daha önceki NuGet sürümleriyle oluşturulan tüm paketler de dahil olmak üzere bir tür ile işaretlenmemiş paketler, varsayılan olarak `Dependency` türü.</span><span class="sxs-lookup"><span data-stu-id="5ceba-105">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="5ceba-106">`Dependency` tür paketleri kitaplıklara ve uygulamalarına derleme veya çalışma zamanı varlıkları ekleyin ve herhangi bir proje türüne (uyumlu oldukları varsayılarak) yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="5ceba-106">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="5ceba-107">`DotnetTool` tür paketleri [DotNet CLI](/dotnet/articles/core/tools/index) için uzantılardır ve komut satırından çağırılır.</span><span class="sxs-lookup"><span data-stu-id="5ceba-107">`DotnetTool` type packages are extensions to the [dotnet CLI](/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="5ceba-108">Bu tür paketler yalnızca .NET Core projelerine yüklenebilir ve geri yükleme işlemlerini etkilemez.</span><span class="sxs-lookup"><span data-stu-id="5ceba-108">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="5ceba-109">Bu proje başına uzantılar hakkında daha fazla ayrıntı  [.NET Core genişletilebilirlik](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) belgelerinde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="5ceba-109">More details about these per-project extensions are available in the  [.NET Core extensibility](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

- <span data-ttu-id="5ceba-110">`Template` tür paketleri, bir uygulama, hizmet, araç veya sınıf kitaplığı gibi dosyalar ya da projeler oluşturmak için kullanılabilecek [özel şablonlar](/dotnet/core/tools/custom-templates) sağlar.</span><span class="sxs-lookup"><span data-stu-id="5ceba-110">`Template` type packages provide [custom templates](/dotnet/core/tools/custom-templates) that can be used to create files or projects like an app, service, tool, or class library.</span></span>

- <span data-ttu-id="5ceba-111">Özel tür paketleri paket kimlikleriyle aynı biçim kurallarına uyan rastgele bir tür tanımlayıcısı kullanır.</span><span class="sxs-lookup"><span data-stu-id="5ceba-111">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="5ceba-112">Ancak dışındaki herhangi bir `Dependency` tür `DotnetTool` , Visual Studio 'Daki NuGet Paket Yöneticisi tarafından tanınmaz.</span><span class="sxs-lookup"><span data-stu-id="5ceba-112">Any type other than `Dependency` and `DotnetTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="5ceba-113">Paket türleri `.nuspec` dosyasında ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="5ceba-113">Package types are set in the `.nuspec` file.</span></span> <span data-ttu-id="5ceba-114">Açık uyumluluğun türü açıkça *ayarlanmamak* `Dependency` ve bunun yerine, hiçbir tür belirtilmediğinde bu türü kabul eden NuGet 'e dayanması için en iyi seçenektir.</span><span class="sxs-lookup"><span data-stu-id="5ceba-114">It's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="5ceba-115">`.nuspec`: Öğe altındaki bir düğüm içinde paket türünü belirtin `packageTypes\packageType` `<metadata>` :</span><span class="sxs-lookup"><span data-stu-id="5ceba-115">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

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
