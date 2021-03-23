---
title: Projeler tarafından başvurulan derlemeleri seçin
description: Paketteki tüm derlemeler çalışma zamanında kullanılabilir olduğunda, paketteki derlemelerin bir alt kümesini oluşturun.
author: zivkan
ms.author: zivkan
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: b2202946d0060e09828250d240f931044d1bf485
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859037"
---
# <a name="select-assemblies-referenced-by-projects"></a><span data-ttu-id="d11f1-103">Projeler tarafından başvurulan derlemeleri seçin</span><span class="sxs-lookup"><span data-stu-id="d11f1-103">Select Assemblies Referenced By Projects</span></span>

<span data-ttu-id="d11f1-104">Açık derleme başvuruları, tüm derlemeler çalışma zamanında kullanılabilir olduğunda, IntelliSense ve derleme için derlemelerin bir alt kümesinin kullanılmasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="d11f1-104">Explicit assembly references allows a subset of assemblies to be used for IntelliSense and compiling, while all assemblies are available at run-time.</span></span> <span data-ttu-id="d11f1-105">`PackageReference` ve `packages.config` farklı şekilde çalışır ve bir sonuç paketi yazarlarının her iki proje türüyle uyumlu olacak şekilde paketi oluşturması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d11f1-105">`PackageReference` and `packages.config` work differently, and as a result package authors need to take care to create the package to be compatible with both project types.</span></span>

> [!Note]
> <span data-ttu-id="d11f1-106">Açık derleme başvuruları .NET Derlemeleriyle ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="d11f1-106">Explicit assembly references are related to .NET assemblies.</span></span> <span data-ttu-id="d11f1-107">Yönetilen bir derleme tarafından P/çağrılan yerel derlemeleri dağıtmak için bir yöntem değildir.</span><span class="sxs-lookup"><span data-stu-id="d11f1-107">It is not a method to distribute native assemblies that are P/Invoked by a managed assembly.</span></span>

## <a name="packagereference-support"></a><span data-ttu-id="d11f1-108">`PackageReference` support</span><span class="sxs-lookup"><span data-stu-id="d11f1-108">`PackageReference` support</span></span>

<span data-ttu-id="d11f1-109">Bir proje ile paket kullandığında `PackageReference` ve paket bir `ref\<tfm>\` Dizin Içerdiğinde, NuGet bu çeviricileri derleme zamanı varlıkları olarak sınıflandırır, ancak `lib\<tfm>\` derlemeler çalışma zamanı varlıkları olarak sınıflandırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="d11f1-109">When a project uses a package with `PackageReference` and the package contains a `ref\<tfm>\` directory, NuGet will classify those assembles as compile-time assets, while the `lib\<tfm>\` assemblies are classified as runtime assets.</span></span> <span data-ttu-id="d11f1-110">İçindeki derlemeler `ref\<tfm>\` çalışma zamanında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="d11f1-110">Assemblies in `ref\<tfm>\` are not used at runtime.</span></span> <span data-ttu-id="d11f1-111">Bu, ' deki herhangi bir derlemenin ya `ref\<tfm>\` da ilgili bir dizinde eşleşen bir derlemeye sahip olması gerektiği anlamına gelir `lib\<tfm>\` `runtime\` , aksi takdirde çalışma zamanı hataları meydana gelir.</span><span class="sxs-lookup"><span data-stu-id="d11f1-111">This means it is necessary for any assembly in `ref\<tfm>\` to have a matching assembly in either `lib\<tfm>\` or a relevant `runtime\` directory, otherwise runtime errors will likely occur.</span></span> <span data-ttu-id="d11f1-112">İçindeki derlemeler `ref\<tfm>\` çalışma zamanında kullanılmadığından, paket boyutunu azaltmak için [yalnızca meta veri derlemeleri](https://github.com/dotnet/roslyn/blob/main/docs/features/refout.md) olabilir.</span><span class="sxs-lookup"><span data-stu-id="d11f1-112">Since assemblies in `ref\<tfm>\` are not used at runtime, they may be [metadata-only assemblies](https://github.com/dotnet/roslyn/blob/main/docs/features/refout.md) to reduce package size.</span></span>

> [!Important]
> <span data-ttu-id="d11f1-113">Bir paket nuspec `<references>` öğesini (tarafından kullanılır `packages.config` , aşağıdaki gibi) içeriyorsa ve içinde derleme içermiyorsa `ref\<tfm>\` , NuGet nuspec öğesinde listelenen derlemeleri `<references>` hem derleme hem de çalışma zamanı varlıkları olarak duyuracaktır.</span><span class="sxs-lookup"><span data-stu-id="d11f1-113">If a package contains the nuspec `<references>` element (used by `packages.config`, see below) and does not contain assemblies in `ref\<tfm>\`, NuGet will advertise the assemblies listed in the nuspec `<references>` element as both the compile and runtime assets.</span></span> <span data-ttu-id="d11f1-114">Bu, başvurulan derlemelerin dizindeki diğer bir derlemeyi yüklemesi gerektiğinde çalışma zamanı özel durumları olacağı anlamına gelir `lib\<tfm>\` .</span><span class="sxs-lookup"><span data-stu-id="d11f1-114">This means there will be runtime exceptions when the referenced assemblies need to load any other assembly in the `lib\<tfm>\` directory.</span></span>

> [!Note]
> <span data-ttu-id="d11f1-115">Paket bir `runtime\` Dizin içeriyorsa, NuGet dizindeki varlıkları kullanamaz `lib\` .</span><span class="sxs-lookup"><span data-stu-id="d11f1-115">If the package contains a `runtime\` directory, NuGet may not use the assets in the `lib\` directory.</span></span>

## <a name="packagesconfig-support"></a><span data-ttu-id="d11f1-116">`packages.config` support</span><span class="sxs-lookup"><span data-stu-id="d11f1-116">`packages.config` support</span></span>

<span data-ttu-id="d11f1-117">`packages.config`NuGet paketlerini yönetmek için kullanan projeler normalde dizindeki tüm derlemelere başvurular ekler `lib\<tfm>\` .</span><span class="sxs-lookup"><span data-stu-id="d11f1-117">Projects using `packages.config` to manage NuGet packages normally add references to all assemblies in the `lib\<tfm>\` directory.</span></span> <span data-ttu-id="d11f1-118">`ref\`Dizin, destek için eklenmiştir `PackageReference` ve bu nedenle kullanılırken dikkate alınmamasıdır `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="d11f1-118">The `ref\` directory was added to support `PackageReference` and therefore isn't considered when using `packages.config`.</span></span> <span data-ttu-id="d11f1-119">Kullanılarak projeler için hangi derlemelerin başvurulduğunu açıkça ayarlamak için `packages.config` , paketin [ `<references>` nuspec dosyasındaki öğesini](../reference/nuspec.md#explicit-assembly-references)kullanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d11f1-119">To explicitly set which assemblies are referenced for projects using `packages.config`, the package must use the [`<references>` element in the nuspec file](../reference/nuspec.md#explicit-assembly-references).</span></span> <span data-ttu-id="d11f1-120">Örnek:</span><span class="sxs-lookup"><span data-stu-id="d11f1-120">For example:</span></span>

```xml
<references>
    <group targetFramework="net45">
        <reference file="MyLibrary.dll" />
    </group>
</references>
```

> [!Note]
> <span data-ttu-id="d11f1-121">`packages.config` Proje, derlemeleri çıkış dizinine kopyalamak için [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/main/documentation/wiki/ResolveAssemblyReference.md) adlı bir işlem kullanın `bin\<configuration>\` .</span><span class="sxs-lookup"><span data-stu-id="d11f1-121">`packages.config` project use a process called [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/main/documentation/wiki/ResolveAssemblyReference.md) to copy assemblies to the `bin\<configuration>\` output directory.</span></span> <span data-ttu-id="d11f1-122">Projenizin derlemesi kopyalanır, ardından derleme sistemi başvurulan derlemeler için derleme bildirimine bakar, ardından bu derlemeleri kopyalar ve tüm derlemeler için yinelemeli olarak yinelenir.</span><span class="sxs-lookup"><span data-stu-id="d11f1-122">Your project's assembly is copied, then the build system looks at the assembly manifest for referenced assemblies, then copies those assemblies and recursively repeats for all assemblies.</span></span> <span data-ttu-id="d11f1-123">Bu, dizininizdeki derlemelerin herhangi birinin `lib\<tfm>\` bağımlılık olarak başka herhangi bir derlemede listelenmediği anlamına gelir (derleme çalışma zamanında `Assembly.Load` , MEF veya başka bir bağımlılık ekleme çerçevesi kullanılarak yükleniyorsa), bu durumda, `bin\<configuration>\` içinde olmasına rağmen projenizin çıkış dizinine kopyalanmayabilir `bin\<tfm>\` .</span><span class="sxs-lookup"><span data-stu-id="d11f1-123">This means that if any of the assemblies in your `lib\<tfm>\` directory are not listed in any other assembly's manifest as a dependency (if the assembly is loaded at runtime using `Assembly.Load`, MEF or another dependency injection framework), then it may not be copied to your project's `bin\<configuration>\` output directory despite being in `bin\<tfm>\`.</span></span>

## <a name="example"></a><span data-ttu-id="d11f1-124">Örnek</span><span class="sxs-lookup"><span data-stu-id="d11f1-124">Example</span></span>

<span data-ttu-id="d11f1-125">Pakem, `MyLib.dll` `MyHelpers.dll` ve `MyUtilities.dll` .NET Framework 4.7.2 hedefleyen üç derleme içerir.</span><span class="sxs-lookup"><span data-stu-id="d11f1-125">My package will contain three assemblies, `MyLib.dll`, `MyHelpers.dll` and `MyUtilities.dll`, which are targeting the .NET Framework 4.7.2.</span></span> <span data-ttu-id="d11f1-126">`MyUtilities.dll` yalnızca diğer iki derleme tarafından kullanılmak üzere tasarlanan sınıfları içerir, bu nedenle bu sınıfları IntelliSense 'te veya paketmi kullanan projelere derleme zamanında kullanılabilir hale getirmek istemiyorum.</span><span class="sxs-lookup"><span data-stu-id="d11f1-126">`MyUtilities.dll` contains classes intended to be used only by the other two assemblies, so I don't want to make those classes available in IntelliSense or at compile time to projects using my package.</span></span> <span data-ttu-id="d11f1-127">My `nuspec` dosyası AŞAĞıDAKI XML öğelerini içermelidir:</span><span class="sxs-lookup"><span data-stu-id="d11f1-127">My `nuspec` file needs to contain the following XML elements:</span></span>

```xml
<references>
    <group targetFramework="net472">
        <reference file="MyLib.dll" />
        <reference file="MyHelpers.dll" />
    </group>
</references>
```

<span data-ttu-id="d11f1-128">ve Paketteki dosyalar şu şekilde olacaktır:</span><span class="sxs-lookup"><span data-stu-id="d11f1-128">and the files in the package will be:</span></span>

```text
lib\net472\MyLib.dll
lib\net472\MyHelpers.dll
lib\net472\MyUtilities.dll
ref\net472\MyLib.dll
ref\net472\MyHelpers.dll
```
