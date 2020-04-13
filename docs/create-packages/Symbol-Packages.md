---
title: Eski sembol paketleri oluşturma (.symbols.nupkg)
description: Visual Studio'daki diğer NuGet paketlerinin hata ayıklamasını desteklemek için yalnızca semboller içeren NuGet paketleri nasıl oluşturulur?
author: karann-msft
ms.author: karann
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 374e9ccfc01cd06508e76529765db3f849342222
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "77476275"
---
# <a name="creating-legacy-symbol-packages-symbolsnupkg"></a><span data-ttu-id="cc1b3-103">Eski sembol paketleri oluşturma (.symbols.nupkg)</span><span class="sxs-lookup"><span data-stu-id="cc1b3-103">Creating legacy symbol packages (.symbols.nupkg)</span></span>

> [!Important]
> <span data-ttu-id="cc1b3-104">Sembol paketleri için önerilen yeni biçim .snupkg'dır.</span><span class="sxs-lookup"><span data-stu-id="cc1b3-104">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="cc1b3-105">Bkz. [Sembol paketleri oluşturma (.snupkg)](Symbol-Packages-snupkg.md).</span><span class="sxs-lookup"><span data-stu-id="cc1b3-105">See [Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md).</span></span> </br>
> <span data-ttu-id="cc1b3-106">.symbols.nupkg hala ancak uyumluluk nedenleriyle desteklenir.</span><span class="sxs-lookup"><span data-stu-id="cc1b3-106">.symbols.nupkg is still supported but only for compatibility reasons.</span></span>

<span data-ttu-id="cc1b3-107">NuGet, nuget.org veya diğer kaynaklar için paket oluşturmanın yanı sıra, sembol sunucularında yayımlanabilen ilişkili sembol paketleri oluşturmayı da destekler.</span><span class="sxs-lookup"><span data-stu-id="cc1b3-107">In addition to building packages for nuget.org or other sources, NuGet also supports creating associated symbol packages that can be published to symbol servers.</span></span> <span data-ttu-id="cc1b3-108">Eski sembol paketi biçimi, .symbols.nupkg, SymbolSource deposuna itilebilir.</span><span class="sxs-lookup"><span data-stu-id="cc1b3-108">The legacy symbol package format, .symbols.nupkg, can be pushed to the SymbolSource repository.</span></span>

<span data-ttu-id="cc1b3-109">Paket tüketicileri `https://nuget.smbsrc.net` daha sonra Visual Studio'daki sembol kaynaklarına ekleyebilir, bu da Visual Studio hata ayıklayıcısında paket koduna adım atmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="cc1b3-109">Package consumers can then add `https://nuget.smbsrc.net` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="cc1b3-110">Bkz. Bu işlemle ilgili ayrıntılar için [Visual Studio hata ayıklamasında ki simge (.pdb) ve kaynak dosyaları belirtin.](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger)</span><span class="sxs-lookup"><span data-stu-id="cc1b3-110">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

## <a name="creating-a-legacy-symbol-package"></a><span data-ttu-id="cc1b3-111">Eski sembol paketi oluşturma</span><span class="sxs-lookup"><span data-stu-id="cc1b3-111">Creating a legacy symbol package</span></span>

<span data-ttu-id="cc1b3-112">Eski bir sembol paketi oluşturmak için aşağıdaki kuralları izleyin:</span><span class="sxs-lookup"><span data-stu-id="cc1b3-112">To create a legacy symbol package, follow these conventions:</span></span>

- <span data-ttu-id="cc1b3-113">Birincil paketi (kodunuzla) `{identifier}.nupkg` adlandırın ve `.pdb` dosyalar hariç tüm dosyalarınızı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="cc1b3-113">Name the primary package (with your code) `{identifier}.nupkg` and include all your files except `.pdb` files.</span></span>
- <span data-ttu-id="cc1b3-114">Eski simge paketini `{identifier}.symbols.nupkg` adlandırın ve `.pdb` montaj DLL, dosyaları, XMLDOC dosyaları, kaynak dosyaları (aşağıdaki bölümlere bakın) içerir.</span><span class="sxs-lookup"><span data-stu-id="cc1b3-114">Name the legacy symbol package `{identifier}.symbols.nupkg` and include your assembly DLL, `.pdb` files, XMLDOC files, source files (see the sections that follow).</span></span>

<span data-ttu-id="cc1b3-115">Her iki paketi de `-Symbols` `.nuspec` bir dosyadan veya proje dosyasından seçenekle oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="cc1b3-115">You can create both packages with the `-Symbols` option, either from a `.nuspec` file or a project file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

<span data-ttu-id="cc1b3-116">Mac `pack` OS X'te Mono 4.4.2 gerektirdiğini ve Linux sistemlerinde çalışmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="cc1b3-116">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="cc1b3-117">Mac'te, dosyadaki `.nuspec` Windows yol adlarını Unix stili yollara dönüştürmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="cc1b3-117">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="legacy-symbol-package-structure"></a><span data-ttu-id="cc1b3-118">Eski sembol paket yapısı</span><span class="sxs-lookup"><span data-stu-id="cc1b3-118">Legacy symbol package structure</span></span>

<span data-ttu-id="cc1b3-119">Eski bir simge paketi, kitaplık paketinin yaptığı gibi birden çok hedef `lib` çerçevesini hedefleyebilir, bu nedenle klasörün `.pdb` yapısı yalnızca DLL'nin yanında bulunan dosyalar da dahil olmak üzere birincil paketle tam olarak aynı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="cc1b3-119">A legacy symbol package can target multiple target frameworks in the same way that a library package does, so the structure of the `lib` folder should be exactly the same as the primary package, only including `.pdb` files alongside the DLL.</span></span>

<span data-ttu-id="cc1b3-120">Örneğin, .NET 4.0 ve Silverlight 4'ü hedefleyen bir eski sembol paketi şu düzene sahip olur:</span><span class="sxs-lookup"><span data-stu-id="cc1b3-120">For example, a legacy symbol package that targets .NET 4.0 and Silverlight 4 would have this layout:</span></span>

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

<span data-ttu-id="cc1b3-121">Kaynak dosyaları daha sonra, kaynak `src`deponuzun göreli yapısını izlemesi gereken ayrı bir özel klasöre yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="cc1b3-121">Source files are then placed in a separate special folder named `src`, which must follow the relative structure of your source repository.</span></span> <span data-ttu-id="cc1b3-122">Bunun nedeni, PDB'lerin eşleşen DLL'yi derlemek için kullanılan kaynak dosyalarıiçin mutlak yollar içermesi ve yayımlama işlemi sırasında bulunmaları gerektiğidir.</span><span class="sxs-lookup"><span data-stu-id="cc1b3-122">This is because PDBs contain absolute paths to source files used to compile the matching DLL, and they need to be found during the publishing process.</span></span> <span data-ttu-id="cc1b3-123">Bir temel yol (ortak yol öneki) çıkarılabilir. Örneğin, bu dosyalardan oluşturulmuş bir kitaplık düşünün:</span><span class="sxs-lookup"><span data-stu-id="cc1b3-123">A base path (common path prefix) can be stripped out. For example, consider a library built from these files:</span></span>

    C:\Projects
        \MyProject
            \Common
                \MyClass.cs
            \Full
                \Properties
                    \AssemblyInfo.cs
                \MyAssembly.csproj (producing \lib\net40\MyAssembly.dll)
            \Silverlight
                \Properties
                    \AssemblyInfo.cs
                \MySilverlightExtensions.cs
                \MyAssembly.csproj (producing \lib\sl4\MyAssembly.dll)

<span data-ttu-id="cc1b3-124">Klasörün `lib` dışında, eski bir simge paketinin bu düzeni içermesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="cc1b3-124">Apart from the `lib` folder, a legacy symbol package would need to contain this layout:</span></span>

    \src
        \Common
            \MyClass.cs
        \Full
            \Properties
                \AssemblyInfo.cs
        \Silverlight
            \Properties
                \AssemblyInfo.cs
            \MySilverlightExtensions.cs

## <a name="referring-to-files-in-the-nuspec"></a><span data-ttu-id="cc1b3-125">Nuspec'teki dosyalara atıfta</span><span class="sxs-lookup"><span data-stu-id="cc1b3-125">Referring to files in the nuspec</span></span>

<span data-ttu-id="cc1b3-126">Eski sembol paketi, önceki bölümde açıklandığı gibi bir klasör yapısından veya bildirimin `files` bölümünde içeriğini belirterek, sözleşmeler tarafından oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="cc1b3-126">A legacy symbol package can be built by conventions, from a folder structure as described in the previous section, or by specifying its contents in the `files` section of the manifest.</span></span> <span data-ttu-id="cc1b3-127">Örneğin, önceki bölümde gösterilen paketi oluşturmak için `.nuspec` dosyada aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="cc1b3-127">For example, to build the package shown in the previous section, use the following in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-legacy-symbol-package"></a><span data-ttu-id="cc1b3-128">Eski sembol paketini yayımlama</span><span class="sxs-lookup"><span data-stu-id="cc1b3-128">Publishing a legacy symbol package</span></span>

> [!Important]
> <span data-ttu-id="cc1b3-129">Paketleri nuget.org itmek için gerekli [NuGet protokollerini](../api/nuget-protocols.md)uygulayan [nuget.exe v4.9.1 veya üzeri](https://www.nuget.org/downloads)nikullanmalısınız.</span><span class="sxs-lookup"><span data-stu-id="cc1b3-129">To push packages to nuget.org you must use [nuget.exe v4.9.1 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="cc1b3-130">Kolaylık sağlamak için öncelikle API anahtarınızı NuGet ile kaydedin (bkz. hem nuget.org hem de symbolsource.org için geçerli olacak [bir paket yayımla,](../nuget-org/publish-a-package.md)çünkü symbolsource.org paket sahibi olduğunuzu doğrulamak için nuget.org ile kontrol edecektir.</span><span class="sxs-lookup"><span data-stu-id="cc1b3-130">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md), which will apply to both nuget.org and symbolsource.org, because symbolsource.org will check with nuget.org to verify that you are the package owner.</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. <span data-ttu-id="cc1b3-131">Birincil paketinizi nuget.org yayımladıktan sonra, dosya adındaki dosya adı nedeniyle `.symbols` symbolsource.org otomatik olarak hedef olarak kullanacak olan eski sembol paketini aşağıdaki gibi itin:</span><span class="sxs-lookup"><span data-stu-id="cc1b3-131">After publishing your primary package to nuget.org, push the legacy symbol package as follows, which will automatically use symbolsource.org as the target because of the `.symbols` in the filename:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. <span data-ttu-id="cc1b3-132">Farklı bir sembol deposunda yayımlamak veya adlandırma kuralına uymayan eski bir simge paketini `-Source` zorlamak için aşağıdaki seçeneği kullanın:</span><span class="sxs-lookup"><span data-stu-id="cc1b3-132">To publish to a different symbol repository, or to push a legacy symbol package that doesn't follow the naming convention, use the `-Source` option:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. <span data-ttu-id="cc1b3-133">Ayrıca, hem birincil hem de sembol paketlerini aşağıdakileri kullanarak aynı anda her iki depoya da itebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="cc1b3-133">You can also push both primary and symbol packages to both repositories at the same time using the following:</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > <span data-ttu-id="cc1b3-134">nuget.exe 4.5.0 veya üzeri ile sembol paketleri otomatik olarak symbolsource.org itilir. Semboller paketlerini daha önceki adımlarda açıklandığı gibi ayrı ayrı itmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="cc1b3-134">With nuget.exe 4.5.0 or above, the symbols packages are not automatically pushed to symbolsource.org. You would need to push the symbols packages separately as explained in the earlier steps.</span></span>
   
<span data-ttu-id="cc1b3-135">Bu durumda, NuGet `MyPackage.symbols.nupkg`birincil paketi nuget.org https://nuget.smbsrc.net/ yayımladıktan sonra (symbolsource.org için itme URL'si) için yayımlar.</span><span class="sxs-lookup"><span data-stu-id="cc1b3-135">In this case, NuGet will publish `MyPackage.symbols.nupkg`, if present, to https://nuget.smbsrc.net/ (the push URL for symbolsource.org), after it publishes the primary package to nuget.org.</span></span>

## <a name="see-also"></a><span data-ttu-id="cc1b3-136">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="cc1b3-136">See also</span></span>

* <span data-ttu-id="cc1b3-137">[Sembol paketleri oluşturma (.snupkg)](Symbol-Packages-snupkg.md) - Sembol paketleri için önerilen yeni biçim</span><span class="sxs-lookup"><span data-stu-id="cc1b3-137">[Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md) - The new recommended format for symbol packages</span></span>
* <span data-ttu-id="cc1b3-138">[Yeni SymbolSource motoruna taşıma](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span><span class="sxs-lookup"><span data-stu-id="cc1b3-138">[Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span></span>
