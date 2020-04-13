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
# <a name="set-a-nuget-package-type"></a><span data-ttu-id="3eae0-103">NuGet paket türünü ayarlama</span><span class="sxs-lookup"><span data-stu-id="3eae0-103">Set a NuGet package type</span></span>

<span data-ttu-id="3eae0-104">NuGet 3.5+ ile paketler, kullanım amacını belirtmek için belirli bir *paket türüyle* işaretlenebilir.</span><span class="sxs-lookup"><span data-stu-id="3eae0-104">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="3eae0-105">NuGet'in önceki sürümleriyle oluşturulan tüm paketler de dahil olmak `Dependency` üzere bir türle işaretlenmemiş paketler varsayılan türe benzer.</span><span class="sxs-lookup"><span data-stu-id="3eae0-105">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="3eae0-106">`Dependency`tür paketleri kitaplıklara ve uygulamalara yapı veya çalışma zamanı varlıkları ekler ve herhangi bir proje türüne (uyumlu oldukları varsayarak) yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="3eae0-106">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="3eae0-107">`DotnetTool`tip paketleri [dotnet CLI](/dotnet/articles/core/tools/index) uzantıları ve komut satırından çağrılır.</span><span class="sxs-lookup"><span data-stu-id="3eae0-107">`DotnetTool` type packages are extensions to the [dotnet CLI](/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="3eae0-108">Bu tür paketler yalnızca .NET Core projelerine yüklenebilir ve geri yükleme işlemleri üzerinde hiçbir etkisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="3eae0-108">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="3eae0-109">Proje başına bu uzantılar hakkında daha fazla ayrıntı [.NET Core genişletilebilirlik](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) belgelerinde mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="3eae0-109">More details about these per-project extensions are available in the  [.NET Core extensibility](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

- <span data-ttu-id="3eae0-110">`Template`tür paketleri, uygulama, hizmet, araç veya sınıf kitaplığı gibi dosya veya proje oluşturmak için kullanılabilecek [özel şablonlar](/dotnet/core/tools/custom-templates) sağlar.</span><span class="sxs-lookup"><span data-stu-id="3eae0-110">`Template` type packages provide [custom templates](/dotnet/core/tools/custom-templates) that can be used to create files or projects like an app, service, tool, or class library.</span></span>

- <span data-ttu-id="3eae0-111">Özel tür paketleri, paket kimliklerle aynı biçim kurallarına uyan rasgele bir tür tanımlayıcı kullanır.</span><span class="sxs-lookup"><span data-stu-id="3eae0-111">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="3eae0-112">`Dependency` Ancak Visual Studio'daki NuGet Paket Yöneticisi tarafından tanınmaz. `DotnetTool`</span><span class="sxs-lookup"><span data-stu-id="3eae0-112">Any type other than `Dependency` and `DotnetTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="3eae0-113">Paket türleri `.nuspec` dosyada ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="3eae0-113">Package types are set in the `.nuspec` file.</span></span> <span data-ttu-id="3eae0-114">Türü açıkça *ayarlamamak* ve bunun yerine hiçbir `Dependency` tür belirtilmediğinde bu türü varsayarak NuGet'e güvenmek geriye dönük uyumluluk için en iyisidir.</span><span class="sxs-lookup"><span data-stu-id="3eae0-114">It's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="3eae0-115">`.nuspec`: Öğenin altındaki `packageTypes\packageType` bir düğüm `<metadata>` içindeki paket türünü belirtin:</span><span class="sxs-lookup"><span data-stu-id="3eae0-115">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

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
