---
title: Projelere Göre Başvurulan Meclisleri Seçin
description: Tüm derlemeler çalışma zamanında kullanılabilirken, paketteki derlemelerin bir alt kümesini derleyicinin kullanımına sun.
author: zivkan
ms.author: zivkan
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: b32075c3f2c06c15c07d36602bdabdaee8b9405a
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427661"
---
# <a name="select-assemblies-referenced-by-projects"></a><span data-ttu-id="6c20c-103">Projelere Göre Başvurulan Meclisleri Seçin</span><span class="sxs-lookup"><span data-stu-id="6c20c-103">Select Assemblies Referenced By Projects</span></span>

<span data-ttu-id="6c20c-104">Açık montaj başvuruları, intelliSense ve derleme için bir derleme alt kümesinin kullanılmasına olanak sağlarken, tüm derlemeler çalışma zamanında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="6c20c-104">Explicit assembly references allows a subset of assemblies to be used for IntelliSense and compiling, while all assemblies are available at run-time.</span></span> <span data-ttu-id="6c20c-105">`PackageReference`ve `packages.config` farklı çalışma ve sonuç olarak paket yazarları her iki proje türleri ile uyumlu olacak şekilde paketi oluşturmak için dikkat etmek gerekir.</span><span class="sxs-lookup"><span data-stu-id="6c20c-105">`PackageReference` and `packages.config` work differently, and as a result package authors need to take care to create the package to be compatible with both project types.</span></span>

> [!Note]
> <span data-ttu-id="6c20c-106">Açık montaj başvuruları .NET derlemeleri ile ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="6c20c-106">Explicit assembly references are related to .NET assemblies.</span></span> <span data-ttu-id="6c20c-107">Yönetilen bir derleme tarafından P/Invoked olan yerel derlemeleri dağıtmak için bir yöntem değildir.</span><span class="sxs-lookup"><span data-stu-id="6c20c-107">It is not a method to distribute native assemblies that are P/Invoked by a managed assembly.</span></span>

## <a name="packagereference-support"></a><span data-ttu-id="6c20c-108">`PackageReference`Destek</span><span class="sxs-lookup"><span data-stu-id="6c20c-108">`PackageReference` support</span></span>

<span data-ttu-id="6c20c-109">Bir proje ile `PackageReference` bir paket kullandığında `ref\<tfm>\` ve paket bir dizin içeriyorsa, NuGet bu derlemeleri derleme zamanı varlıkları olarak sınıflandırılırken, `lib\<tfm>\` derlemeler çalışma zamanı varlıkları olarak sınıflandırılır.</span><span class="sxs-lookup"><span data-stu-id="6c20c-109">When a project uses a package with `PackageReference` and the package contains a `ref\<tfm>\` directory, NuGet will classify those assembles as compile-time assets, while the `lib\<tfm>\` assemblies are classified as runtime assets.</span></span> <span data-ttu-id="6c20c-110">Montajlar `ref\<tfm>\` çalışma zamanında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="6c20c-110">Assemblies in `ref\<tfm>\` are not used at runtime.</span></span> <span data-ttu-id="6c20c-111">Bu, herhangi bir derlemenin `ref\<tfm>\` eşleşen bir derlemenin `lib\<tfm>\` veya `runtime\` ilgili bir dizinde olması gerektiği anlamına gelir, aksi takdirde çalışma zamanı hataları büyük olasılıkla oluşacaktır.</span><span class="sxs-lookup"><span data-stu-id="6c20c-111">This means it is necessary for any assembly in `ref\<tfm>\` to have a matching assembly in either `lib\<tfm>\` or a relevant `runtime\` directory, otherwise runtime errors will likely occur.</span></span> <span data-ttu-id="6c20c-112">Çalışma `ref\<tfm>\` zamanında derlemeler kullanılmadığından, paket boyutunu azaltmak için [yalnızca meta veri derlemeleri](https://github.com/dotnet/roslyn/blob/master/docs/features/refout.md) olabilir.</span><span class="sxs-lookup"><span data-stu-id="6c20c-112">Since assemblies in `ref\<tfm>\` are not used at runtime, they may be [metadata-only assemblies](https://github.com/dotnet/roslyn/blob/master/docs/features/refout.md) to reduce package size.</span></span>

> [!Important]
> <span data-ttu-id="6c20c-113">Bir `<references>` paket nuspec öğesi içeriyorsa (aşağıda görmek `packages.config`te, aşağıya `ref\<tfm>\`bakın) ve derlemeler içermiyorsa, NuGet nuspec `<references>` öğesinde listelenen derlemelerin hem derleme hem de çalışma zamanı varlıkları olarak tanıtılacaktır.</span><span class="sxs-lookup"><span data-stu-id="6c20c-113">If a package contains the nuspec `<references>` element (used by `packages.config`, see below) and does not contain assemblies in `ref\<tfm>\`, NuGet will advertise the assemblies listed in the nuspec `<references>` element as both the compile and runtime assets.</span></span> <span data-ttu-id="6c20c-114">Bu, başvurulan derlemelerin `lib\<tfm>\` dizindeki diğer derlemeleri yüklemesi gerektiğinde çalışma zamanı özel durumları olacağı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="6c20c-114">This means there will be runtime exceptions when the referenced assemblies need to load any other assembly in the `lib\<tfm>\` directory.</span></span>

> [!Note]
> <span data-ttu-id="6c20c-115">Paketbir `runtime\` dizin içeriyorsa, NuGet `lib\` dizindeki varlıkları kullanamaz.</span><span class="sxs-lookup"><span data-stu-id="6c20c-115">If the package contains a `runtime\` directory, NuGet may not use the assets in the `lib\` directory.</span></span>

## <a name="packagesconfig-support"></a><span data-ttu-id="6c20c-116">`packages.config`Destek</span><span class="sxs-lookup"><span data-stu-id="6c20c-116">`packages.config` support</span></span>

<span data-ttu-id="6c20c-117">NuGet `packages.config` paketlerini yönetmek için kullanan projeler normalde `lib\<tfm>\` dizindeki tüm derlemelere başvurular ekler.</span><span class="sxs-lookup"><span data-stu-id="6c20c-117">Projects using `packages.config` to manage NuGet packages normally add references to all assemblies in the `lib\<tfm>\` directory.</span></span> <span data-ttu-id="6c20c-118">Dizin `ref\` destek `PackageReference` eklendi ve bu nedenle kullanırken `packages.config`dikkate alınmadı.</span><span class="sxs-lookup"><span data-stu-id="6c20c-118">The `ref\` directory was added to support `PackageReference` and therefore isn't considered when using `packages.config`.</span></span> <span data-ttu-id="6c20c-119">Hangi derlemelerin kullanılan `packages.config`projeler için başvurulmasını açıkça ayarlamak için, paketin [ `<references>` nuspec dosyasındaki öğeyi](../reference/nuspec.md#explicit-assembly-references)kullanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6c20c-119">To explicitly set which assemblies are referenced for projects using `packages.config`, the package must use the [`<references>` element in the nuspec file](../reference/nuspec.md#explicit-assembly-references).</span></span> <span data-ttu-id="6c20c-120">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="6c20c-120">For example:</span></span>

```xml
<references>
    <group targetFramework="net45">
        <reference file="MyLibrary.dll" />
    </group>
</references>
```

> [!Note]
> <span data-ttu-id="6c20c-121">`packages.config``bin\<configuration>\` proje, derlemeleri çıktı dizinine kopyalamak için [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/master/documentation/wiki/ResolveAssemblyReference.md) adlı bir işlem kullanın.</span><span class="sxs-lookup"><span data-stu-id="6c20c-121">`packages.config` project use a process called [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/master/documentation/wiki/ResolveAssemblyReference.md) to copy assemblies to the `bin\<configuration>\` output directory.</span></span> <span data-ttu-id="6c20c-122">Projenizin derlemesi kopyalanır, sonra yapı sistemi başvurulan derlemeler için derleme bildirimine bakar, ardından bu derlemeleri kopyalar ve tüm derlemeler için özyinelemeli olarak yineler.</span><span class="sxs-lookup"><span data-stu-id="6c20c-122">Your project's assembly is copied, then the build system looks at the assembly manifest for referenced assemblies, then copies those assemblies and recursively repeats for all assemblies.</span></span> <span data-ttu-id="6c20c-123">`lib\<tfm>\` Bu, dizininizdeki derlemelerden herhangi birinin başka bir derlemenin bildiriminde bağımlılık olarak listelenmemesi durumunda (derleme `Assembly.Load`çalışma zamanında , MEF veya başka bir bağımlılık enjeksiyon çerçevesi kullanılarak `bin\<configuration>\` yükleniyorsa), `bin\<tfm>\`içinde olmasına rağmen projenizin çıktı dizinine kopyalanamayabileceği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="6c20c-123">This means that if any of the assemblies in your `lib\<tfm>\` directory are not listed in any other assembly's manifest as a dependency (if the assembly is loaded at runtime using `Assembly.Load`, MEF or another dependency injection framework), then it may not be copied to your project's `bin\<configuration>\` output directory despite being in `bin\<tfm>\`.</span></span>

## <a name="example"></a><span data-ttu-id="6c20c-124">Örnek</span><span class="sxs-lookup"><span data-stu-id="6c20c-124">Example</span></span>

<span data-ttu-id="6c20c-125">Paketim,.NET `MyLib.dll` `MyHelpers.dll` `MyUtilities.dll`Framework 4.7.2'yi hedefleyen üç derleme içerir.</span><span class="sxs-lookup"><span data-stu-id="6c20c-125">My package will contain three assemblies, `MyLib.dll`, `MyHelpers.dll` and `MyUtilities.dll`, which are targeting the .NET Framework 4.7.2.</span></span> <span data-ttu-id="6c20c-126">`MyUtilities.dll`yalnızca diğer iki derleme tarafından kullanılmak üzere tasarlanmış sınıfları içerir, bu nedenle bu sınıfları IntelliSense'de kullanılabilir hale getirmek veya paketimi kullanarak projelere zaman derlemek istemiyorum.</span><span class="sxs-lookup"><span data-stu-id="6c20c-126">`MyUtilities.dll` contains classes intended to be used only by the other two assemblies, so I don't want to make those classes available in IntelliSense or at compile time to projects using my package.</span></span> <span data-ttu-id="6c20c-127">Dosyamın `nuspec` aşağıdaki XML öğelerini içermesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="6c20c-127">My `nuspec` file needs to contain the following XML elements:</span></span>

```xml
<references>
    <group targetFramework="net472">
        <reference file="MyLib.dll" />
        <reference file="MyHelpers.dll" />
    </group>
</references>
```

<span data-ttu-id="6c20c-128">ve paketteki dosyalar:</span><span class="sxs-lookup"><span data-stu-id="6c20c-128">and the files in the package will be:</span></span>

```text
lib\net472\MyLib.dll
lib\net472\MyHelpers.dll
lib\net472\MyUtilities.dll
ref\net472\MyLib.dll
ref\net472\MyHelpers.dll
```
