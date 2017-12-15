---
title: "NuGet sembol paketlerini oluşturma | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 9/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 4667a70d-5a17-4f1e-b2f2-b8d0c6af3882
description: "Diğer NuGet paketleri Visual Studio'da hata ayıklamayı desteklemek için yalnızca sembolleri içeren NuGet paketleri oluşturma"
keywords: "NuGet sembol paketlerini, hata ayıklama, hata ayıklama, paket sembolleri, sembol paketi kuralları NuGet destekleyen NuGet paketi"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: b1a29fe6e9a3dec6847dbed07761e28fb8eb9b19
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="creating-symbol-packages"></a><span data-ttu-id="f9289-104">Sembol paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="f9289-104">Creating symbol packages</span></span>

<span data-ttu-id="f9289-105">Nuget.org veya diğer kaynakları NuGet paketleri de destekler yanı sıra ilişkili sembol paketlerini oluşturmak ve bunları yayımlama [SymbolSource depo](http://www.symbolsource.org/Public).</span><span class="sxs-lookup"><span data-stu-id="f9289-105">In addition to building packages for nuget.org or other sources, NuGet also supports creating associated symbol packages and publishing them to the [SymbolSource repository](http://www.symbolsource.org/Public).</span></span>

<span data-ttu-id="f9289-106">Paket tüketicileri ardından ekleyebilirsiniz `http://srv.symbolsource.org/pdb/Public` Visual Studio'da simgesi kaynakları için böylece Visual Studio hata ayıklayıcısında paket koda atlama.</span><span class="sxs-lookup"><span data-stu-id="f9289-106">Package consumers can then add `http://srv.symbolsource.org/pdb/Public` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="f9289-107">Bkz: [Visual Studio hata ayıklayıcısında simge (.pdb) ve kaynak dosyaları belirtme](https://docs.microsoft.com/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) işlem hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="f9289-107">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](https://docs.microsoft.com/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>


## <a name="creating-a-symbol-package"></a><span data-ttu-id="f9289-108">Sembol paket oluşturma</span><span class="sxs-lookup"><span data-stu-id="f9289-108">Creating a symbol package</span></span>

<span data-ttu-id="f9289-109">Sembol paketi oluşturmak için bu kuralları izleyin:</span><span class="sxs-lookup"><span data-stu-id="f9289-109">To create a symbol package, follow these conventions:</span></span>

- <span data-ttu-id="f9289-110">Birincil paketiyle (kodunuzu) ad `{identifier}.nupkg` ve tüm dosyalar hariç dahil `.pdb` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="f9289-110">Name the primary package (with your code) `{identifier}.nupkg` and include all your files except `.pdb` files.</span></span>
- <span data-ttu-id="f9289-111">Sembol paket adı `{identifier}.symbols.nupkg` ve derlemenizi DLL dahil `.pdb` dosyaları, XMLDOC dosyaları, kaynak dosyaları (bölümlerde bakın).</span><span class="sxs-lookup"><span data-stu-id="f9289-111">Name the symbol package `{identifier}.symbols.nupkg` and include your assembly DLL, `.pdb` files, XMLDOC files, source files (see the sections that follow).</span></span>

<span data-ttu-id="f9289-112">Her iki paketlerle oluşturabilirsiniz `-Symbols` herhangi birinden seçeneği bir `.nuspec` veya proje dosyası:</span><span class="sxs-lookup"><span data-stu-id="f9289-112">You can create both packages with the `-Symbols` option, either from a `.nuspec` file or a project file:</span></span>

```
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

<span data-ttu-id="f9289-113">Unutmayın `pack` Mono 4.4.2 Mac OS x gerektirir ve Linux sistemlerinde çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="f9289-113">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="f9289-114">Bir Mac üzerinde Windows yol adları olarak da dönüştürmelidir `.nuspec` UNIX stili yollara dosya.</span><span class="sxs-lookup"><span data-stu-id="f9289-114">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="f9289-115">Sembol paket yapısı</span><span class="sxs-lookup"><span data-stu-id="f9289-115">Symbol package structure</span></span>

<span data-ttu-id="f9289-116">Sembol paketi birden çok hedef çerçeveyi kitaplık paketi yapan aynı şekilde hedefleyebilirsiniz böylece yapısını `lib` klasörü tam olarak aynı olmalıdır birincil paketi olarak dahil olmak üzere yalnızca `.pdb` yanında DLL dosyaları.</span><span class="sxs-lookup"><span data-stu-id="f9289-116">A symbol package can target multiple target frameworks in the same way that a library package does, so the structure of the `lib` folder should be exactly the same as the primary package, only including `.pdb` files alongside the DLL.</span></span>

<span data-ttu-id="f9289-117">Örneğin, .NET 4.0 ve Silverlight 4 hedefleyen bir sembol paketi bu düzeni sahip olur:</span><span class="sxs-lookup"><span data-stu-id="f9289-117">For example, a symbol package that targets .NET 4.0 and Silverlight 4 would have this layout:</span></span>

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

<span data-ttu-id="f9289-118">Kaynak dosyalarını sonra adlı ayrı bir özel klasöre yerleştirdiğiniz `src`, kaynak deponuz göreli yapısını izlemelidir.</span><span class="sxs-lookup"><span data-stu-id="f9289-118">Source files are then placed in a separate special folder named `src`, which must follow the relative structure of your source repository.</span></span> <span data-ttu-id="f9289-119">Pdb mutlak yolları eşleşen DLL derlemek için kullanılan kaynak dosyaları içerir ve yayımlama işlemi sırasında bulunması gerekir çünkü budur.</span><span class="sxs-lookup"><span data-stu-id="f9289-119">This is because PDBs contain absolute paths to source files used to compile the matching DLL, and they need to be found during the publishing process.</span></span> <span data-ttu-id="f9289-120">Taban yol (ortak yolu önek) çıkarılır. Örneğin, bu dosyaları dışında oluşturulmuş bir kitaplık göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="f9289-120">A base path (common path prefix) can be stripped out. For example, consider a library built from these files:</span></span>

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

<span data-ttu-id="f9289-121">Apart gelen `lib` klasörü, bir sembol paketi gerekir bu düzeni içerir:</span><span class="sxs-lookup"><span data-stu-id="f9289-121">Apart from the `lib` folder, a symbol package would need to contain this layout:</span></span>

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

## <a name="referring-to-files-in-the-nuspec"></a><span data-ttu-id="f9289-122">Nuspec dosyalarında başvurma</span><span class="sxs-lookup"><span data-stu-id="f9289-122">Referring to files in the nuspec</span></span>

<span data-ttu-id="f9289-123">Sembol paketi kurallarından önceki bölümde açıklandığı gibi klasör yapısı veya içeriğini belirterek yerleşik `files` bildirim bölümü.</span><span class="sxs-lookup"><span data-stu-id="f9289-123">A symbol package can be built by conventions, from a folder structure as described in the previous section, or by specifying its contents in the `files` section of the manifest.</span></span> <span data-ttu-id="f9289-124">Örneğin, önceki bölümde gösterilen paketi oluşturmak için aşağıdakileri kullanın `.nuspec` dosyası:</span><span class="sxs-lookup"><span data-stu-id="f9289-124">For example, to build the package shown in the previous section, use the following in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="f9289-125">Sembol Paketi Yayımlama</span><span class="sxs-lookup"><span data-stu-id="f9289-125">Publishing a symbol package</span></span>

> [!Important]
> <span data-ttu-id="f9289-126">Anında iletme paketlere kullanmalısınız nuget.org için [nuget.exe v4.1.0 veya yukarıdaki](https://www.nuget.org/downloads), gerekli uygulayan [NuGet protokolleri](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="f9289-126">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="f9289-127">Kolaylık olması için NuGet ile ilk API anahtarınıza kaydedin (bkz [bir paketi yayımlamaya](../create-packages/publish-a-package.md)nuget.org ve symbolsource.org için geçerli, symbolsource.org doğrulamak için nuget.org ile denetleyecek olduğundan paket sahibi değil.</span><span class="sxs-lookup"><span data-stu-id="f9289-127">For convenience, first save your API key with NuGet (see [publish a package](../create-packages/publish-a-package.md), which will apply to both nuget.org and symbolsource.org, because symbolsource.org will check with nuget.org to verify that you are the package owner.</span></span>

    ```
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="f9289-128">Birincil paketiniz için nuget.org yayımlandıktan sonra simge paketini aşağıdaki gibi otomatik olarak symbolsource.org nedeniyle hedefi olarak kullanacak anında `.symbols` dosya:</span><span class="sxs-lookup"><span data-stu-id="f9289-128">After publishing your primary package to nuget.org, push the symbol package as follows, which will automatically use symbolsource.org as the target because of the `.symbols` in the filename:</span></span>

    ```
    nuget push MyPackage.symbols.nupkg
    ```
> [!Note]
> <span data-ttu-id="f9289-129">Nuget.exe 4.5.0 veya üzeri, simgeler paketleri otomatik olarak symbolsource.org için gönderilen değil. Sonraki adımda açıklandığı gibi ayrı ayrı simgeleri paketleri göndermek gerekir.</span><span class="sxs-lookup"><span data-stu-id="f9289-129">With nuget.exe 4.5.0 or above, the symbols packages are not automatically pushed to symbolsource.org. You would need to push the symbols packages separately as explained in the next step.</span></span>

1. <span data-ttu-id="f9289-130">Farklı simge depoya yayımlamak ya da adlandırma kuralı IU bir sembol paketi göndermek için kullanmak `-Source` seçeneği:</span><span class="sxs-lookup"><span data-stu-id="f9289-130">To publish to a different symbol repository, or to push a symbol package that doesn't follow the naming convention, use the `-Source` option:</span></span>

    ```
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

1. <span data-ttu-id="f9289-131">Ayrıca, hem birincil hem de anında ve aşağıdakileri kullanarak aynı anda hem depoları paketlere simge:</span><span class="sxs-lookup"><span data-stu-id="f9289-131">You can also push both primary and symbol packages to both repositories at the same time using the following:</span></span>

    ```
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="f9289-132">Bu durumda, NuGet yayımlayacak `MyPackage.symbols.nupkg`, varsa, https://nuget.smbsrc.net/ (anında iletme URL'si için symbolsource.org) için birincil paketi için nuget.org yayımlar sonra.</span><span class="sxs-lookup"><span data-stu-id="f9289-132">In this case, NuGet will publish `MyPackage.symbols.nupkg`, if present, to https://nuget.smbsrc.net/ (the push URL for symbolsource.org), after it publishes the primary package to nuget.org.</span></span>

## <a name="see-also"></a><span data-ttu-id="f9289-133">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="f9289-133">See Also</span></span>

 - <span data-ttu-id="f9289-134"><a href="https://www.symbolsource.org/Public/Wiki/Using" target="_blank">SymbolSource kullanarak</a> (symbolsource.org)</span><span class="sxs-lookup"><span data-stu-id="f9289-134"><a href="https://www.symbolsource.org/Public/Wiki/Using" target="_blank">Using SymbolSource</a> (symbolsource.org)</span></span>
