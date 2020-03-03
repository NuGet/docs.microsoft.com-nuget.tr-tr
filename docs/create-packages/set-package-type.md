---
title: NuGet paket türü ayarla
description: Bir paketin amaçlanan kullanımını göstermek için paket türlerini açıklar.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 1d869f616ce0291cf1c0a17b7ff20fc61e6a3bd5
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230830"
---
# <a name="set-a-nuget-package-type"></a><span data-ttu-id="fa772-103">NuGet paket türü ayarla</span><span class="sxs-lookup"><span data-stu-id="fa772-103">Set a NuGet package type</span></span>

<span data-ttu-id="fa772-104">NuGet 3.5 + ile, paketleri amaçlanan kullanımını göstermek için belirli bir *paket türüyle* işaretlenebilir.</span><span class="sxs-lookup"><span data-stu-id="fa772-104">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="fa772-105">Daha önceki NuGet sürümleriyle oluşturulan tüm paketler de dahil olmak üzere bir türle işaretlenmemiş paketler, varsayılan olarak `Dependency` türüdür.</span><span class="sxs-lookup"><span data-stu-id="fa772-105">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="fa772-106">`Dependency` tür paketleri kitaplıklara ve uygulamalara derleme veya çalışma zamanı varlıkları ekler ve herhangi bir proje türüne (uyumlu oldukları varsayılarak) yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="fa772-106">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="fa772-107">`DotnetTool` tür paketleri [DotNet CLI](/dotnet/articles/core/tools/index) için uzantılardır ve komut satırından çağırılır.</span><span class="sxs-lookup"><span data-stu-id="fa772-107">`DotnetTool` type packages are extensions to the [dotnet CLI](/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="fa772-108">Bu tür paketler yalnızca .NET Core projelerine yüklenebilir ve geri yükleme işlemlerini etkilemez.</span><span class="sxs-lookup"><span data-stu-id="fa772-108">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="fa772-109">Bu proje başına uzantılar hakkında daha fazla ayrıntı [.NET Core genişletilebilirlik](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) belgelerinde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="fa772-109">More details about these per-project extensions are available in the  [.NET Core extensibility](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

- <span data-ttu-id="fa772-110">`Template` tür paketleri, bir uygulama, hizmet, araç veya sınıf kitaplığı gibi dosyalar ya da projeler oluşturmak için kullanılabilecek [özel şablonlar](/dotnet/core/tools/custom-templates) sağlar.</span><span class="sxs-lookup"><span data-stu-id="fa772-110">`Template` type packages provide [custom templates](/dotnet/core/tools/custom-templates) that can be used to create files or projects like an app, service, tool, or class library.</span></span>

- <span data-ttu-id="fa772-111">Özel tür paketleri paket kimlikleriyle aynı biçim kurallarına uyan rastgele bir tür tanımlayıcısı kullanır.</span><span class="sxs-lookup"><span data-stu-id="fa772-111">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="fa772-112">Ancak `Dependency` ve `DotnetTool`dışındaki herhangi bir tür, Visual Studio 'daki NuGet Paket Yöneticisi tarafından tanınmaz.</span><span class="sxs-lookup"><span data-stu-id="fa772-112">Any type other than `Dependency` and `DotnetTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="fa772-113">Paket türleri `.nuspec` dosyasında ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="fa772-113">Package types are set in the `.nuspec` file.</span></span> <span data-ttu-id="fa772-114">`Dependency` türü açıkça *ayarlanmamak* ve bunun yerine, hiçbir tür belirtilmediğinde bu türü kabul eden NuGet 'i kullanmak için geriye dönük uyumluluk için idealdir.</span><span class="sxs-lookup"><span data-stu-id="fa772-114">It's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="fa772-115">`.nuspec`: `<metadata>` öğesi altındaki bir `packageTypes\packageType` düğümü içindeki paket türünü gösterir:</span><span class="sxs-lookup"><span data-stu-id="fa772-115">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

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
