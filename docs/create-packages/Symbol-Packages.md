---
title: Eski sembol paketleri oluşturuluyor (. Symbols. nupkg)
description: Visual Studio 'da diğer NuGet paketlerinde hata ayıklamayı desteklemek için yalnızca semboller içeren NuGet paketleri oluşturma.
author: karann-msft
ms.author: karann
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 374e9ccfc01cd06508e76529765db3f849342222
ms.sourcegitcommit: 1799d4ac23c8aacee7498fdc72c40dd1646d267b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77476275"
---
# <a name="creating-legacy-symbol-packages-symbolsnupkg"></a><span data-ttu-id="f6e2b-103">Eski sembol paketleri oluşturuluyor (. Symbols. nupkg)</span><span class="sxs-lookup"><span data-stu-id="f6e2b-103">Creating legacy symbol packages (.symbols.nupkg)</span></span>

> [!Important]
> <span data-ttu-id="f6e2b-104">Sembol paketleri için önerilen yeni biçim. snupkg 'dir.</span><span class="sxs-lookup"><span data-stu-id="f6e2b-104">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="f6e2b-105">Bkz. [sembol paketleri oluşturma (. snupkg)](Symbol-Packages-snupkg.md).</span><span class="sxs-lookup"><span data-stu-id="f6e2b-105">See [Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md).</span></span> </br>
> <span data-ttu-id="f6e2b-106">. Symbols. nupkg hala desteklenir ancak yalnızca uyumluluk nedenleriyle desteklenir.</span><span class="sxs-lookup"><span data-stu-id="f6e2b-106">.symbols.nupkg is still supported but only for compatibility reasons.</span></span>

<span data-ttu-id="f6e2b-107">NuGet, nuget.org veya diğer kaynaklar için paket oluşturmaya ek olarak, sembol sunucularına yayımlanmakta olabilecek ilişkili sembol paketleri oluşturmayı da destekler.</span><span class="sxs-lookup"><span data-stu-id="f6e2b-107">In addition to building packages for nuget.org or other sources, NuGet also supports creating associated symbol packages that can be published to symbol servers.</span></span> <span data-ttu-id="f6e2b-108">Eski sembol paketi biçimi. Symbols. nupkg, SymbolSource deposuna itilmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="f6e2b-108">The legacy symbol package format, .symbols.nupkg, can be pushed to the SymbolSource repository.</span></span>

<span data-ttu-id="f6e2b-109">Böylece, paket tüketicileri Visual Studio 'daki sembol kaynaklarına `https://nuget.smbsrc.net` ekleyebilir ve bu, Visual Studio hata ayıklayıcısında paket koduna adımlamayı sağlar.</span><span class="sxs-lookup"><span data-stu-id="f6e2b-109">Package consumers can then add `https://nuget.smbsrc.net` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="f6e2b-110">Bu işlemle ilgili ayrıntılar için bkz. [Visual Studio hata ayıklayıcısında simge (. pdb) ve kaynak dosyaları belirtme](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) .</span><span class="sxs-lookup"><span data-stu-id="f6e2b-110">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

## <a name="creating-a-legacy-symbol-package"></a><span data-ttu-id="f6e2b-111">Eski sembol paketi oluşturma</span><span class="sxs-lookup"><span data-stu-id="f6e2b-111">Creating a legacy symbol package</span></span>

<span data-ttu-id="f6e2b-112">Eski bir sembol paketi oluşturmak için aşağıdaki kuralları izleyin:</span><span class="sxs-lookup"><span data-stu-id="f6e2b-112">To create a legacy symbol package, follow these conventions:</span></span>

- <span data-ttu-id="f6e2b-113">Birincil paketi (kodunuzla birlikte) adlandırın `{identifier}.nupkg` ve `.pdb` dosyaları hariç tüm dosyalarınızı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f6e2b-113">Name the primary package (with your code) `{identifier}.nupkg` and include all your files except `.pdb` files.</span></span>
- <span data-ttu-id="f6e2b-114">Eski sembol paketini adlandırın `{identifier}.symbols.nupkg` ve derleme DLL 'sini, `.pdb` dosyalarını, XMLDOC dosyalarını, kaynak dosyalarını (izleyen bölümlere bakın) ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f6e2b-114">Name the legacy symbol package `{identifier}.symbols.nupkg` and include your assembly DLL, `.pdb` files, XMLDOC files, source files (see the sections that follow).</span></span>

<span data-ttu-id="f6e2b-115">`-Symbols` seçeneğiyle her iki paketi de oluşturabilirsiniz: bir `.nuspec` dosyası ya da bir proje dosyası:</span><span class="sxs-lookup"><span data-stu-id="f6e2b-115">You can create both packages with the `-Symbols` option, either from a `.nuspec` file or a project file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

<span data-ttu-id="f6e2b-116">`pack` Mac OS X için mono 4.4.2 gerektirdiğini ve Linux sistemlerinde çalışmayacağını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f6e2b-116">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="f6e2b-117">Mac 'te Ayrıca, `.nuspec` dosyasındaki Windows yol adları adlarını UNIX stili yollara dönüştürmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f6e2b-117">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="legacy-symbol-package-structure"></a><span data-ttu-id="f6e2b-118">Eski sembol paketi yapısı</span><span class="sxs-lookup"><span data-stu-id="f6e2b-118">Legacy symbol package structure</span></span>

<span data-ttu-id="f6e2b-119">Eski bir sembol paketi, bir kitaplık paketiyle aynı şekilde birden çok hedef çerçeveyi hedefleyebilir, bu nedenle `lib` klasörünün yapısı yalnızca DLL ile birlikte `.pdb` dosyaları dahil olmak üzere birincil paket ile tam olarak aynı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f6e2b-119">A legacy symbol package can target multiple target frameworks in the same way that a library package does, so the structure of the `lib` folder should be exactly the same as the primary package, only including `.pdb` files alongside the DLL.</span></span>

<span data-ttu-id="f6e2b-120">Örneğin, .NET 4,0 ve Silverlight 4 ' ü hedefleyen eski bir sembol paketi bu düzene sahip olacaktır:</span><span class="sxs-lookup"><span data-stu-id="f6e2b-120">For example, a legacy symbol package that targets .NET 4.0 and Silverlight 4 would have this layout:</span></span>

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

<span data-ttu-id="f6e2b-121">Kaynak dosyalar daha sonra, kaynak deponuzun göreli yapısını izlemesi gereken `src`adlı ayrı bir özel klasöre yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="f6e2b-121">Source files are then placed in a separate special folder named `src`, which must follow the relative structure of your source repository.</span></span> <span data-ttu-id="f6e2b-122">Bunun nedeni, pdb 'leri 'ın eşleşen DLL 'yi derlemek için kullanılan kaynak dosyalara mutlak yollar içermesi ve yayımlama işlemi sırasında bulunması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f6e2b-122">This is because PDBs contain absolute paths to source files used to compile the matching DLL, and they need to be found during the publishing process.</span></span> <span data-ttu-id="f6e2b-123">Temel yol (ortak yol öneki) eklenebilir. Örneğin, bu dosyalardan oluşturulmuş bir kitaplığı düşünün:</span><span class="sxs-lookup"><span data-stu-id="f6e2b-123">A base path (common path prefix) can be stripped out. For example, consider a library built from these files:</span></span>

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

<span data-ttu-id="f6e2b-124">`lib` klasörden ayrı olarak, eski bir sembol paketinin bu düzeni içermesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="f6e2b-124">Apart from the `lib` folder, a legacy symbol package would need to contain this layout:</span></span>

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

## <a name="referring-to-files-in-the-nuspec"></a><span data-ttu-id="f6e2b-125">Nuspec içindeki dosyalara başvurma</span><span class="sxs-lookup"><span data-stu-id="f6e2b-125">Referring to files in the nuspec</span></span>

<span data-ttu-id="f6e2b-126">Eski bir sembol paketi, önceki bölümde açıklandığı gibi bir klasör yapısından veya bildirimin `files` bölümünde içeriğini belirterek, kurallar tarafından oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="f6e2b-126">A legacy symbol package can be built by conventions, from a folder structure as described in the previous section, or by specifying its contents in the `files` section of the manifest.</span></span> <span data-ttu-id="f6e2b-127">Örneğin, önceki bölümde gösterilen paketi oluşturmak için `.nuspec` dosyasında aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="f6e2b-127">For example, to build the package shown in the previous section, use the following in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-legacy-symbol-package"></a><span data-ttu-id="f6e2b-128">Eski bir sembol paketi yayımlanıyor</span><span class="sxs-lookup"><span data-stu-id="f6e2b-128">Publishing a legacy symbol package</span></span>

> [!Important]
> <span data-ttu-id="f6e2b-129">Paketleri nuget.org 'e göndermek için gereken [NuGet protokollerini](../api/nuget-protocols.md)uygulayan [NuGet. exe v 4.9.1 veya üstünü](https://www.nuget.org/downloads)kullanmalısınız.</span><span class="sxs-lookup"><span data-stu-id="f6e2b-129">To push packages to nuget.org you must use [nuget.exe v4.9.1 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="f6e2b-130">Daha kolay olması için, önce API anahtarınızı NuGet ile kaydedin (bkz. nuget.org ve symbolsource.org için uygulanacak [bir paket yayımlama](../nuget-org/publish-a-package.md)), bu, paket sahibi olduğunuzu doğrulamak üzere NuGet.org ile kontrol edecektir.</span><span class="sxs-lookup"><span data-stu-id="f6e2b-130">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md), which will apply to both nuget.org and symbolsource.org, because symbolsource.org will check with nuget.org to verify that you are the package owner.</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. <span data-ttu-id="f6e2b-131">Birincil paketinizi nuget.org 'e yayımladıktan sonra, eski sembol paketini aşağıdaki gibi gönderin. Bu, dosya adında `.symbols` nedeniyle otomatik olarak symbolsource.org hedef olarak kullanılır:</span><span class="sxs-lookup"><span data-stu-id="f6e2b-131">After publishing your primary package to nuget.org, push the legacy symbol package as follows, which will automatically use symbolsource.org as the target because of the `.symbols` in the filename:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. <span data-ttu-id="f6e2b-132">Farklı bir sembol deposuna yayımlamak veya adlandırma kuralını izleyen eski bir sembol paketini göndermek için `-Source` seçeneğini kullanın:</span><span class="sxs-lookup"><span data-stu-id="f6e2b-132">To publish to a different symbol repository, or to push a legacy symbol package that doesn't follow the naming convention, use the `-Source` option:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. <span data-ttu-id="f6e2b-133">Ayrıca, aşağıdakileri kullanarak hem birincil hem de sembol paketlerini aynı anda her iki depoya da gönderebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f6e2b-133">You can also push both primary and symbol packages to both repositories at the same time using the following:</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > <span data-ttu-id="f6e2b-134">NuGet. exe 4.5.0 veya üzeri ile, semboller paketleri otomatik olarak symbolsource.org 'e gönderilmez. Önceki adımlarda açıklandığı gibi semboller paketlerini ayrı olarak göndermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f6e2b-134">With nuget.exe 4.5.0 or above, the symbols packages are not automatically pushed to symbolsource.org. You would need to push the symbols packages separately as explained in the earlier steps.</span></span>
   
<span data-ttu-id="f6e2b-135">Bu durumda, NuGet birincil paketi nuget.org ' ye yayımladıktan sonra, varsa NuGet, varsa https://nuget.smbsrc.net/ (symbolsource.org için gönderim URL 'SI) `MyPackage.symbols.nupkg`yayımlar.</span><span class="sxs-lookup"><span data-stu-id="f6e2b-135">In this case, NuGet will publish `MyPackage.symbols.nupkg`, if present, to https://nuget.smbsrc.net/ (the push URL for symbolsource.org), after it publishes the primary package to nuget.org.</span></span>

## <a name="see-also"></a><span data-ttu-id="f6e2b-136">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="f6e2b-136">See also</span></span>

* <span data-ttu-id="f6e2b-137">[Sembol paketleri (. snupkg) oluşturuluyor](Symbol-Packages-snupkg.md) -sembol paketleri için önerilen yeni biçim</span><span class="sxs-lookup"><span data-stu-id="f6e2b-137">[Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md) - The new recommended format for symbol packages</span></span>
* <span data-ttu-id="f6e2b-138">[Yeni SymbolSource Engine 'e geçme](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span><span class="sxs-lookup"><span data-stu-id="f6e2b-138">[Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span></span>
