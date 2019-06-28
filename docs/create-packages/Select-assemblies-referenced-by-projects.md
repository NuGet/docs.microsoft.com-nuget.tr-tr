---
title: Proje tarafından başvurulan bütünleştirilmiş kodları seçin
description: Tüm derlemeleri çalışma zamanında kullanılabilir ancak paketteki kümesini derleyici kullanılabilir hale getirmek.
author: zivkan
ms.author: zivkan
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: b32075c3f2c06c15c07d36602bdabdaee8b9405a
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427661"
---
# <a name="select-assemblies-referenced-by-projects"></a><span data-ttu-id="62be6-103">Proje tarafından başvurulan bütünleştirilmiş kodları seçin</span><span class="sxs-lookup"><span data-stu-id="62be6-103">Select Assemblies Referenced By Projects</span></span>

<span data-ttu-id="62be6-104">Açık derleme başvurularını tüm derlemeleri çalışma zamanında kullanılabilir ancak derleme ve IntelliSense için kullanılacak bir kümesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="62be6-104">Explicit assembly references allows a subset of assemblies to be used for IntelliSense and compiling, while all assemblies are available at run-time.</span></span> <span data-ttu-id="62be6-105">`PackageReference` ve `packages.config` farklı çalışır ve bunun sonucunda paket yazarlarının ilgileniriz iki proje türü ile uyumlu olacak şekilde paketi oluşturmak için gerekir.</span><span class="sxs-lookup"><span data-stu-id="62be6-105">`PackageReference` and `packages.config` work differently, and as a result package authors need to take care to create the package to be compatible with both project types.</span></span>

> [!Note]
> <span data-ttu-id="62be6-106">Açık derleme başvurularını .NET derlemeleri için ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="62be6-106">Explicit assembly references are related to .NET assemblies.</span></span> <span data-ttu-id="62be6-107">P/çağrılan yönetilen bir derlemeye olan yerel derlemeleri dağıtmak için bir yöntem değil.</span><span class="sxs-lookup"><span data-stu-id="62be6-107">It is not a method to distribute native assemblies that are P/Invoked by a managed assembly.</span></span>

## <a name="packagereference-support"></a><span data-ttu-id="62be6-108">`PackageReference` Destek</span><span class="sxs-lookup"><span data-stu-id="62be6-108">`PackageReference` support</span></span>

<span data-ttu-id="62be6-109">Bir proje olan bir pakete kullandığında `PackageReference` ve paketi içeren bir `ref\<tfm>\` NuGet dizin sınıflandırmak bu derleme zamanı varlıklar çeviren sırada `lib\<tfm>\` derlemeler çalışma zamanı varlıklar sınıflandırılan.</span><span class="sxs-lookup"><span data-stu-id="62be6-109">When a project uses a package with `PackageReference` and the package contains a `ref\<tfm>\` directory, NuGet will classify those assembles as compile-time assets, while the `lib\<tfm>\` assemblies are classified as runtime assets.</span></span> <span data-ttu-id="62be6-110">Derlemelerde `ref\<tfm>\` çalışma zamanında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="62be6-110">Assemblies in `ref\<tfm>\` are not used at runtime.</span></span> <span data-ttu-id="62be6-111">Bu, herhangi bir derleme için gerekli olduğu anlamına gelir `ref\<tfm>\` eşleşen derleme ya da için `lib\<tfm>\` veya ilgili `runtime\` dizin, aksi takdirde çalışma zamanı hataları büyük olasılıkla oluşur.</span><span class="sxs-lookup"><span data-stu-id="62be6-111">This means it is necessary for any assembly in `ref\<tfm>\` to have a matching assembly in either `lib\<tfm>\` or a relevant `runtime\` directory, otherwise runtime errors will likely occur.</span></span> <span data-ttu-id="62be6-112">Derlemelerde beri `ref\<tfm>\` kullanılmayan çalışma zamanında, bunlar olabilir [yalnızca meta veri bütünleştirilmiş kodları](https://github.com/dotnet/roslyn/blob/master/docs/features/refout.md) paket boyutunu küçültmek için.</span><span class="sxs-lookup"><span data-stu-id="62be6-112">Since assemblies in `ref\<tfm>\` are not used at runtime, they may be [metadata-only assemblies](https://github.com/dotnet/roslyn/blob/master/docs/features/refout.md) to reduce package size.</span></span>

> [!Important]
> <span data-ttu-id="62be6-113">Bir paket bir nuspec içeriyorsa `<references>` öğesi (tarafından kullanılan `packages.config`, aşağıya bakın) ve derlemeleri içermiyor `ref\<tfm>\`, NuGet sınıflandırmalarına listelenen derlemeleri tanıtır `<references>` öğesi derleme ve çalışma zamanı varlıklar olarak.</span><span class="sxs-lookup"><span data-stu-id="62be6-113">If a package contains the nuspec `<references>` element (used by `packages.config`, see below) and does not contain assemblies in `ref\<tfm>\`, NuGet will advertise the assemblies listed in the nuspec `<references>` element as both the compile and runtime assets.</span></span> <span data-ttu-id="62be6-114">Başvurulan derlemeleri diğer herhangi bir derlemede yük gerektiğinde, çalışma zamanı özel durumları olacağı anlamına gelir `lib\<tfm>\` dizin.</span><span class="sxs-lookup"><span data-stu-id="62be6-114">This means there will be runtime exceptions when the referenced assemblies need to load any other assembly in the `lib\<tfm>\` directory.</span></span>

> [!Note]
> <span data-ttu-id="62be6-115">Paket içeriyorsa bir `runtime\` dizin, NuGet varlıkları kullanamazsınız `lib\` dizin.</span><span class="sxs-lookup"><span data-stu-id="62be6-115">If the package contains a `runtime\` directory, NuGet may not use the assets in the `lib\` directory.</span></span>

## <a name="packagesconfig-support"></a><span data-ttu-id="62be6-116">`packages.config` Destek</span><span class="sxs-lookup"><span data-stu-id="62be6-116">`packages.config` support</span></span>

<span data-ttu-id="62be6-117">Kullanarak projeleri `packages.config` NuGet yönetmek için paketleri normalde tüm derlemelerin başvurularını eklemek `lib\<tfm>\` dizin.</span><span class="sxs-lookup"><span data-stu-id="62be6-117">Projects using `packages.config` to manage NuGet packages normally add references to all assemblies in the `lib\<tfm>\` directory.</span></span> <span data-ttu-id="62be6-118">`ref\` Dizin desteklemek için eklenen `PackageReference` ve bu nedenle kullanırken dikkate değil `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="62be6-118">The `ref\` directory was added to support `PackageReference` and therefore isn't considered when using `packages.config`.</span></span> <span data-ttu-id="62be6-119">Hangi derlemelerin kullanarak projeleri için başvurulan açıkça ayarlamak için `packages.config`, paket kullanmalısınız [ `<references>` soubor nuspec öğesinde](../reference/nuspec.md#explicit-assembly-references).</span><span class="sxs-lookup"><span data-stu-id="62be6-119">To explicitly set which assemblies are referenced for projects using `packages.config`, the package must use the [`<references>` element in the nuspec file](../reference/nuspec.md#explicit-assembly-references).</span></span> <span data-ttu-id="62be6-120">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="62be6-120">For example:</span></span>

```xml
<references>
    <group targetFramework="net45">
        <reference file="MyLibrary.dll" />
    </group>
</references>
```

> [!Note]
> <span data-ttu-id="62be6-121">`packages.config` adlı bir işlem proje kullanım [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/master/documentation/wiki/ResolveAssemblyReference.md) derlemeleri kopyalamak için `bin\<configuration>\` çıkış dizini.</span><span class="sxs-lookup"><span data-stu-id="62be6-121">`packages.config` project use a process called [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/master/documentation/wiki/ResolveAssemblyReference.md) to copy assemblies to the `bin\<configuration>\` output directory.</span></span> <span data-ttu-id="62be6-122">Proje derleme kopyalanır, ardından derleme sistemi, başvurulan derlemeler için derleme bildirimini inceler ve ardından bu derlemeleri kopyalar ve yinelemeli olarak tüm derlemeler için yinelenir.</span><span class="sxs-lookup"><span data-stu-id="62be6-122">Your project's assembly is copied, then the build system looks at the assembly manifest for referenced assemblies, then copies those assemblies and recursively repeats for all assemblies.</span></span> <span data-ttu-id="62be6-123">Bu durumlarda derlemelerin hiçbirini anlamına gelir, `lib\<tfm>\` herhangi diğer derleme bildiriminde bağımlılık olarak dizin listelenmez (derleme çalışma zamanı kullanarak yüklü ise `Assembly.Load`, MEF veya başka bir bağımlılık ekleme framework), sonra çalışmıyor olabilir projenizin kopyalanan `bin\<configuration>\` işlemlerle rağmen çıkış dizinine `bin\<tfm>\`.</span><span class="sxs-lookup"><span data-stu-id="62be6-123">This means that if any of the assemblies in your `lib\<tfm>\` directory are not listed in any other assembly's manifest as a dependency (if the assembly is loaded at runtime using `Assembly.Load`, MEF or another dependency injection framework), then it may not be copied to your project's `bin\<configuration>\` output directory despite being in `bin\<tfm>\`.</span></span>

## <a name="example"></a><span data-ttu-id="62be6-124">Örnek</span><span class="sxs-lookup"><span data-stu-id="62be6-124">Example</span></span>

<span data-ttu-id="62be6-125">Paketimle üç derlemeleri içerir `MyLib.dll`, `MyHelpers.dll` ve `MyUtilities.dll`, .NET Framework 4.7.2 hedefleme.</span><span class="sxs-lookup"><span data-stu-id="62be6-125">My package will contain three assemblies, `MyLib.dll`, `MyHelpers.dll` and `MyUtilities.dll`, which are targeting the .NET Framework 4.7.2.</span></span> <span data-ttu-id="62be6-126">`MyUtilities.dll` Bu sınıfların IntelliSense içinde ya da derleme zamanında paketimle kullanarak projeleri için kullanılabilmesini istemediğiniz için yalnızca diğer iki derlemeler tarafından kullanılmak üzere sınıfları içerir.</span><span class="sxs-lookup"><span data-stu-id="62be6-126">`MyUtilities.dll` contains classes intended to be used only by the other two assemblies, so I don't want to make those classes available in IntelliSense or at compile time to projects using my package.</span></span> <span data-ttu-id="62be6-127">My `nuspec` dosya aşağıdaki XML öğeleri içeren gerekir:</span><span class="sxs-lookup"><span data-stu-id="62be6-127">My `nuspec` file needs to contain the following XML elements:</span></span>

```xml
<references>
    <group targetFramework="net472">
        <reference file="MyLib.dll" />
        <reference file="MyHelpers.dll" />
    </group>
</references>
```

<span data-ttu-id="62be6-128">ve paketteki dosyaların olacaktır:</span><span class="sxs-lookup"><span data-stu-id="62be6-128">and the files in the package will be:</span></span>

```text
lib\net472\MyLib.dll
lib\net472\MyHelpers.dll
lib\net472\MyUtilities.dll
ref\net472\MyLib.dll
ref\net472\MyHelpers.dll
```
