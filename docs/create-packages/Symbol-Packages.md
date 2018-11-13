---
title: NuGet sembol paketleri oluşturma
description: NuGet paketi Visual Studio'da hata ayıklamayı desteklemek için yalnızca sembolleri içeren NuGet paketleri oluşturma
author: karann-msft
ms.author: karann
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 3321cba9082eb35b53ba693e246db18e5d8e187b
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580265"
---
# <a name="creating-symbol-packages-legacy"></a><span data-ttu-id="df58d-103">Sembol paketleri (eski) oluşturma</span><span class="sxs-lookup"><span data-stu-id="df58d-103">Creating symbol packages (legacy)</span></span>

> [!Important]
> <span data-ttu-id="df58d-104">Sembol paketleri yeni Önerilen biçimi .snupkg değil.</span><span class="sxs-lookup"><span data-stu-id="df58d-104">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="df58d-105">Bkz: [sembol paketleri (.snupkg) oluşturma](Symbol-Packages-snupkg.md).</span><span class="sxs-lookup"><span data-stu-id="df58d-105">See [Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md).</span></span> </br>
> <span data-ttu-id="df58d-106">. symbols.nupkg ancak yalnızca uyumluluk açısından hala destekleniyor.</span><span class="sxs-lookup"><span data-stu-id="df58d-106">.symbols.nupkg is still supported but only for compatibility reasons.</span></span>

<span data-ttu-id="df58d-107">Nuget.org veya diğer kaynaklar, NuGet paketlerini de oluşturmaya ek olarak, sembol paketleri ve SymbolSource depoya yayımlama oluşturmayı destekler ilişkili.</span><span class="sxs-lookup"><span data-stu-id="df58d-107">In addition to building packages for nuget.org or other sources, NuGet also supports creating associated symbol packages and publishing them to the SymbolSource repository.</span></span>

<span data-ttu-id="df58d-108">Paketi tüketicileri daha sonra ekleyebilirsiniz `https://nuget.smbsrc.net` kendi sembol kaynaklarına Visual Studio'da sağlayan Visual Studio hata ayıklayıcısı paket kod içine Adımlama.</span><span class="sxs-lookup"><span data-stu-id="df58d-108">Package consumers can then add `https://nuget.smbsrc.net` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="df58d-109">Bkz: [Visual Studio hata ayıklayıcısında simge (.pdb) ve kaynak dosyaları belirtme](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) işlem hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="df58d-109">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="df58d-110">Bir sembol paketi oluşturma</span><span class="sxs-lookup"><span data-stu-id="df58d-110">Creating a symbol package</span></span>

<span data-ttu-id="df58d-111">Bir sembol paketi oluşturmak için bu kuralları izleyin:</span><span class="sxs-lookup"><span data-stu-id="df58d-111">To create a symbol package, follow these conventions:</span></span>

- <span data-ttu-id="df58d-112">(Sizin kodunuz ile) birincil paket adı `{identifier}.nupkg` ve hariç tüm dosyalarınızı eklemek `.pdb` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="df58d-112">Name the primary package (with your code) `{identifier}.nupkg` and include all your files except `.pdb` files.</span></span>
- <span data-ttu-id="df58d-113">Sembol paketi adı `{identifier}.symbols.nupkg` ve bütünleştirilmiş kodunuzda DLL `.pdb` dosyaları, XMLDOC dosyaları, kaynak dosyaları (bölümlerde bakın).</span><span class="sxs-lookup"><span data-stu-id="df58d-113">Name the symbol package `{identifier}.symbols.nupkg` and include your assembly DLL, `.pdb` files, XMLDOC files, source files (see the sections that follow).</span></span>

<span data-ttu-id="df58d-114">Her iki paketlerle oluşturabilirsiniz `-Symbols` seçeneği,'nden ya da bir `.nuspec` dosyası veya proje dosyası:</span><span class="sxs-lookup"><span data-stu-id="df58d-114">You can create both packages with the `-Symbols` option, either from a `.nuspec` file or a project file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

<span data-ttu-id="df58d-115">Unutmayın `pack` Mac OS X üzerinde Mono 4.4.2 gerektirir ve Linux sistemlerinde çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="df58d-115">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="df58d-116">Mac bilgisayarlarda, Windows yol adları olarak da dönüştürmelisiniz `.nuspec` UNIX stili yollara dosya.</span><span class="sxs-lookup"><span data-stu-id="df58d-116">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="df58d-117">Sembol paket yapısı</span><span class="sxs-lookup"><span data-stu-id="df58d-117">Symbol package structure</span></span>

<span data-ttu-id="df58d-118">Bir sembol paketi birden çok hedef çerçeve kitaplığı paketi yapan aynı şekilde hedefleyebilirsiniz. böylece yapısını `lib` klasör tam olarak aynı olmalıdır, birincil paketi olarak dahil olmak üzere yalnızca `.pdb` yanında DLL dosyaları.</span><span class="sxs-lookup"><span data-stu-id="df58d-118">A symbol package can target multiple target frameworks in the same way that a library package does, so the structure of the `lib` folder should be exactly the same as the primary package, only including `.pdb` files alongside the DLL.</span></span>

<span data-ttu-id="df58d-119">Örneğin, .NET 4.0 ve Silverlight 4'ü hedefleyen bir sembol paketi bu düzen gerekir:</span><span class="sxs-lookup"><span data-stu-id="df58d-119">For example, a symbol package that targets .NET 4.0 and Silverlight 4 would have this layout:</span></span>

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

<span data-ttu-id="df58d-120">Kaynak dosyaları ardından adlı ayrı bir özel klasöre yerleştirilen `src`, kaynak deponuza göreli yapısını izlemelidir.</span><span class="sxs-lookup"><span data-stu-id="df58d-120">Source files are then placed in a separate special folder named `src`, which must follow the relative structure of your source repository.</span></span> <span data-ttu-id="df58d-121">Pdb eşleşen DLL derlemek için kullanılan kaynak dosyalarının mutlak yolları içerir ve yayımlama işlemi sırasında bulunması gerekir çünkü budur.</span><span class="sxs-lookup"><span data-stu-id="df58d-121">This is because PDBs contain absolute paths to source files used to compile the matching DLL, and they need to be found during the publishing process.</span></span> <span data-ttu-id="df58d-122">Temel bir yol (genel yol ön eki) kullanıma kesilmiş. Örneğin, bu dosyalardaki yerleşik bir kitaplık göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="df58d-122">A base path (common path prefix) can be stripped out. For example, consider a library built from these files:</span></span>

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

<span data-ttu-id="df58d-123">Gelen apart `lib` klasöründe bir sembol paketi gerekir bu düzen içerir:</span><span class="sxs-lookup"><span data-stu-id="df58d-123">Apart from the `lib` folder, a symbol package would need to contain this layout:</span></span>

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

## <a name="referring-to-files-in-the-nuspec"></a><span data-ttu-id="df58d-124">Nuspec dosyalara başvurma</span><span class="sxs-lookup"><span data-stu-id="df58d-124">Referring to files in the nuspec</span></span>

<span data-ttu-id="df58d-125">Önceki bölümde açıklandığı gibi bir klasör yapısı kurallarından veya içeriğini belirterek bir sembol paketi oluşturulabilir `files` bildiriminin.</span><span class="sxs-lookup"><span data-stu-id="df58d-125">A symbol package can be built by conventions, from a folder structure as described in the previous section, or by specifying its contents in the `files` section of the manifest.</span></span> <span data-ttu-id="df58d-126">Örneğin, önceki bölümde gösterilenle paketi oluşturmak için aşağıdakileri kullanın. `.nuspec` dosyası:</span><span class="sxs-lookup"><span data-stu-id="df58d-126">For example, to build the package shown in the previous section, use the following in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="df58d-127">Bir sembol Paketi Yayımlama</span><span class="sxs-lookup"><span data-stu-id="df58d-127">Publishing a symbol package</span></span>

> [!Important]
> <span data-ttu-id="df58d-128">Anında iletme paketlerine nuget.org'da kullanmalısınız [nuget.exe verze 4.1.0 veya üzeri](https://www.nuget.org/downloads), gerekli uygulayan [NuGet protokolleri](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="df58d-128">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="df58d-129">Kolaylık olması için NuGet ile ilk API anahtarınızı kaydedin (bkz [paket yayımlama](../create-packages/publish-a-package.md)nuget.org hem symbolsource.org geçerli, symbolsource.org doğrulamak için nuget.org ile denetleyecek çünkü paket sahip olursunuz.</span><span class="sxs-lookup"><span data-stu-id="df58d-129">For convenience, first save your API key with NuGet (see [publish a package](../create-packages/publish-a-package.md), which will apply to both nuget.org and symbolsource.org, because symbolsource.org will check with nuget.org to verify that you are the package owner.</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. <span data-ttu-id="df58d-130">Nuget.org için birincil paketinizi yayımladıktan sonra sembol paketi aşağıdaki gibi otomatik olarak symbolsource.org nedeniyle hedefi olarak kullanacak anında iletme `.symbols` dosya:</span><span class="sxs-lookup"><span data-stu-id="df58d-130">After publishing your primary package to nuget.org, push the symbol package as follows, which will automatically use symbolsource.org as the target because of the `.symbols` in the filename:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. <span data-ttu-id="df58d-131">Farklı bir sembol deposuna yayımlamak için veya yönelik adlandırma kuralını uygulamalıdır olmayan bir sembol paketi göndermeye `-Source` seçeneği:</span><span class="sxs-lookup"><span data-stu-id="df58d-131">To publish to a different symbol repository, or to push a symbol package that doesn't follow the naming convention, use the `-Source` option:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. <span data-ttu-id="df58d-132">Ayrıca, hem birincil hem de anında iletme ve paketleri hem de aşağıdaki kullanarak aynı anda simge:</span><span class="sxs-lookup"><span data-stu-id="df58d-132">You can also push both primary and symbol packages to both repositories at the same time using the following:</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > <span data-ttu-id="df58d-133">Nuget.exe 4.5.0 veya yukarıdaki simgeleri paketleri otomatik olarak için symbolsource.org itilir değil. Sembol paketleri sonraki adımda açıklandığı gibi ayrı ayrı anında iletme gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="df58d-133">With nuget.exe 4.5.0 or above, the symbols packages are not automatically pushed to symbolsource.org. You would need to push the symbols packages separately as explained in the next step.</span></span>
   
<span data-ttu-id="df58d-134">Bu durumda, NuGet yayımlayacak `MyPackage.symbols.nupkg`için mevcut, https://nuget.smbsrc.net/ (anında iletme URL'si için symbolsource.org) sonra nuget.org için birincil paketi yayımlar.</span><span class="sxs-lookup"><span data-stu-id="df58d-134">In this case, NuGet will publish `MyPackage.symbols.nupkg`, if present, to https://nuget.smbsrc.net/ (the push URL for symbolsource.org), after it publishes the primary package to nuget.org.</span></span>

## <a name="see-also"></a><span data-ttu-id="df58d-135">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="df58d-135">See Also</span></span>

<span data-ttu-id="df58d-136">[Yeni SymbolSource Altyapısı'na taşıma](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span><span class="sxs-lookup"><span data-stu-id="df58d-136">[Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span></span>
