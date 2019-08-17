---
title: NuGet sembol paketleri oluşturma
description: Visual Studio 'da diğer NuGet paketlerinde hata ayıklamayı desteklemek için yalnızca semboller içeren NuGet paketleri oluşturma.
author: karann-msft
ms.author: karann
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: f7503dd413a976997580aa03da26df0c462ff0e1
ms.sourcegitcommit: 80cf99f40759911324468be1ec815c96aebf376d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/17/2019
ms.locfileid: "69564557"
---
# <a name="creating-symbol-packages-legacy"></a><span data-ttu-id="a2f33-103">Sembol paketleri oluşturma (eski)</span><span class="sxs-lookup"><span data-stu-id="a2f33-103">Creating symbol packages (legacy)</span></span>

> [!Important]
> <span data-ttu-id="a2f33-104">Sembol paketleri için önerilen yeni biçim. snupkg 'dir.</span><span class="sxs-lookup"><span data-stu-id="a2f33-104">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="a2f33-105">Bkz. [sembol paketleri oluşturma (. snupkg)](Symbol-Packages-snupkg.md).</span><span class="sxs-lookup"><span data-stu-id="a2f33-105">See [Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md).</span></span> </br>
> <span data-ttu-id="a2f33-106">. Symbols. nupkg hala desteklenir ancak yalnızca uyumluluk nedenleriyle desteklenir.</span><span class="sxs-lookup"><span data-stu-id="a2f33-106">.symbols.nupkg is still supported but only for compatibility reasons.</span></span>

<span data-ttu-id="a2f33-107">NuGet, nuget.org veya diğer kaynaklar için paket oluşturmaya ek olarak ilişkili sembol paketleri oluşturmayı ve bunları SymbolSource deposuna yayımlamayı da destekler.</span><span class="sxs-lookup"><span data-stu-id="a2f33-107">In addition to building packages for nuget.org or other sources, NuGet also supports creating associated symbol packages and publishing them to the SymbolSource repository.</span></span>

<span data-ttu-id="a2f33-108">Paket tüketicileri, Visual `https://nuget.smbsrc.net` Studio 'da, Visual Studio hata ayıklayıcısında paket koduna adımla izin veren sembol kaynaklarına eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="a2f33-108">Package consumers can then add `https://nuget.smbsrc.net` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="a2f33-109">Bu işlemle ilgili ayrıntılar için bkz. [Visual Studio hata ayıklayıcısında simge (. pdb) ve kaynak dosyaları belirtme](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) .</span><span class="sxs-lookup"><span data-stu-id="a2f33-109">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="a2f33-110">Sembol paketi oluşturma</span><span class="sxs-lookup"><span data-stu-id="a2f33-110">Creating a symbol package</span></span>

<span data-ttu-id="a2f33-111">Bir sembol paketi oluşturmak için aşağıdaki kuralları izleyin:</span><span class="sxs-lookup"><span data-stu-id="a2f33-111">To create a symbol package, follow these conventions:</span></span>

- <span data-ttu-id="a2f33-112">Birincil paketi (kodunuzla birlikte) `{identifier}.nupkg` adlandırın ve dosyalar hariç `.pdb` tüm dosyalarınızı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a2f33-112">Name the primary package (with your code) `{identifier}.nupkg` and include all your files except `.pdb` files.</span></span>
- <span data-ttu-id="a2f33-113">Sembol paketini `{identifier}.symbols.nupkg` adlandırın ve derleme dll 'sini, `.pdb` dosyalarınızı, xmlDoc dosyalarını, kaynak dosyalarınızı (izleyen bölümlere bakın) ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a2f33-113">Name the symbol package `{identifier}.symbols.nupkg` and include your assembly DLL, `.pdb` files, XMLDOC files, source files (see the sections that follow).</span></span>

<span data-ttu-id="a2f33-114">`-Symbols` Bir`.nuspec` dosya ya da proje dosyasından, seçeneğiyle her iki paket de oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a2f33-114">You can create both packages with the `-Symbols` option, either from a `.nuspec` file or a project file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

<span data-ttu-id="a2f33-115">Mac OS X mono 4.4.2 gerektirdiğini ve Linux sistemlerinde çalışmadığına not edin. `pack`</span><span class="sxs-lookup"><span data-stu-id="a2f33-115">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="a2f33-116">Mac 'te Ayrıca, `.nuspec` dosyadaki Windows yol adlarını UNIX stili yollara dönüştürmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a2f33-116">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="a2f33-117">Sembol paketi yapısı</span><span class="sxs-lookup"><span data-stu-id="a2f33-117">Symbol package structure</span></span>

<span data-ttu-id="a2f33-118">Bir sembol paketi birden çok hedef çerçeveyi bir kitaplık paketiyle aynı şekilde hedefleyebilir, bu nedenle `lib` klasörün yapısı yalnızca dll ile birlikte dosyalar dahil olmak üzere `.pdb` birincil paket ile tam olarak aynı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a2f33-118">A symbol package can target multiple target frameworks in the same way that a library package does, so the structure of the `lib` folder should be exactly the same as the primary package, only including `.pdb` files alongside the DLL.</span></span>

<span data-ttu-id="a2f33-119">Örneğin, .NET 4,0 ve Silverlight 4 ' ü hedefleyen bir sembol paketinin bu düzeni olacaktır:</span><span class="sxs-lookup"><span data-stu-id="a2f33-119">For example, a symbol package that targets .NET 4.0 and Silverlight 4 would have this layout:</span></span>

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

<span data-ttu-id="a2f33-120">Kaynak dosyalar daha sonra adlı `src`ayrı bir özel klasöre yerleştirilir ve bu, kaynak deponuzun göreli yapısına uymalıdır.</span><span class="sxs-lookup"><span data-stu-id="a2f33-120">Source files are then placed in a separate special folder named `src`, which must follow the relative structure of your source repository.</span></span> <span data-ttu-id="a2f33-121">Bunun nedeni, pdb 'leri 'ın eşleşen DLL 'yi derlemek için kullanılan kaynak dosyalara mutlak yollar içermesi ve yayımlama işlemi sırasında bulunması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a2f33-121">This is because PDBs contain absolute paths to source files used to compile the matching DLL, and they need to be found during the publishing process.</span></span> <span data-ttu-id="a2f33-122">Temel yol (ortak yol öneki) eklenebilir. Örneğin, bu dosyalardan oluşturulmuş bir kitaplığı düşünün:</span><span class="sxs-lookup"><span data-stu-id="a2f33-122">A base path (common path prefix) can be stripped out. For example, consider a library built from these files:</span></span>

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

<span data-ttu-id="a2f33-123">`lib` Klasörden ayrı olarak, bir sembol paketinin bu düzeni içermesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="a2f33-123">Apart from the `lib` folder, a symbol package would need to contain this layout:</span></span>

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

## <a name="referring-to-files-in-the-nuspec"></a><span data-ttu-id="a2f33-124">Nuspec içindeki dosyalara başvurma</span><span class="sxs-lookup"><span data-stu-id="a2f33-124">Referring to files in the nuspec</span></span>

<span data-ttu-id="a2f33-125">Bir sembol paketi, önceki bölümde açıklandığı gibi bir klasör yapısından veya bildirimin `files` bölümünde içeriğini belirterek, kurallara göre derlenebilir.</span><span class="sxs-lookup"><span data-stu-id="a2f33-125">A symbol package can be built by conventions, from a folder structure as described in the previous section, or by specifying its contents in the `files` section of the manifest.</span></span> <span data-ttu-id="a2f33-126">Örneğin, önceki bölümde gösterilen paketi oluşturmak için, `.nuspec` dosyasında aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="a2f33-126">For example, to build the package shown in the previous section, use the following in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="a2f33-127">Sembol paketi yayımlama</span><span class="sxs-lookup"><span data-stu-id="a2f33-127">Publishing a symbol package</span></span>

> [!Important]
> <span data-ttu-id="a2f33-128">Paketleri nuget.org 'e göndermek için gereken [NuGet protokollerini](../api/nuget-protocols.md)uygulayan [NuGet. exe v 4.9.1 veya üstünü](https://www.nuget.org/downloads)kullanmalısınız.</span><span class="sxs-lookup"><span data-stu-id="a2f33-128">To push packages to nuget.org you must use [nuget.exe v4.9.1 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="a2f33-129">Daha kolay olması için, önce API anahtarınızı NuGet ile kaydedin (bkz. nuget.org ve symbolsource.org için uygulanacak [bir paket yayımlama](../nuget-org/publish-a-package.md)), bu, paket sahibi olduğunuzu doğrulamak üzere NuGet.org ile kontrol edecektir.</span><span class="sxs-lookup"><span data-stu-id="a2f33-129">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md), which will apply to both nuget.org and symbolsource.org, because symbolsource.org will check with nuget.org to verify that you are the package owner.</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. <span data-ttu-id="a2f33-130">Birincil paketinizi NuGet.org 'e yayımladıktan sonra, sembol paketini aşağıdaki gibi gönderin. Bu, dosya adında adı nedeniyle `.symbols` otomatik olarak symbolsource.org ' i kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="a2f33-130">After publishing your primary package to nuget.org, push the symbol package as follows, which will automatically use symbolsource.org as the target because of the `.symbols` in the filename:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. <span data-ttu-id="a2f33-131">Farklı bir sembol deposuna yayımlamak veya adlandırma kuralını izleyen bir sembol paketini göndermek için `-Source` seçeneğini kullanın:</span><span class="sxs-lookup"><span data-stu-id="a2f33-131">To publish to a different symbol repository, or to push a symbol package that doesn't follow the naming convention, use the `-Source` option:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. <span data-ttu-id="a2f33-132">Ayrıca, aşağıdakileri kullanarak hem birincil hem de sembol paketlerini aynı anda her iki depoya da gönderebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a2f33-132">You can also push both primary and symbol packages to both repositories at the same time using the following:</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > <span data-ttu-id="a2f33-133">NuGet. exe 4.5.0 veya üzeri ile, semboller paketleri otomatik olarak symbolsource.org 'e gönderilmez. Önceki adımlarda açıklandığı gibi semboller paketlerini ayrı olarak göndermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a2f33-133">With nuget.exe 4.5.0 or above, the symbols packages are not automatically pushed to symbolsource.org. You would need to push the symbols packages separately as explained in the earlier steps.</span></span>
   
<span data-ttu-id="a2f33-134">Bu durumda, NuGet birincil paketi NuGet.org `MyPackage.symbols.nupkg`' ye yayımladıktan sonra https://nuget.smbsrc.net/ , varsa NuGet (symbolsource.org için gönderim URL 'si) olarak yayımlanır.</span><span class="sxs-lookup"><span data-stu-id="a2f33-134">In this case, NuGet will publish `MyPackage.symbols.nupkg`, if present, to https://nuget.smbsrc.net/ (the push URL for symbolsource.org), after it publishes the primary package to nuget.org.</span></span>

## <a name="see-also"></a><span data-ttu-id="a2f33-135">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="a2f33-135">See Also</span></span>

<span data-ttu-id="a2f33-136">[Yeni SymbolSource altyapısına geçme](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span><span class="sxs-lookup"><span data-stu-id="a2f33-136">[Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span></span>
