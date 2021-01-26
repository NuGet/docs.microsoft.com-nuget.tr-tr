---
title: Eski sembol paketleri oluşturuluyor (. Symbols. nupkg)
description: Visual Studio 'da diğer NuGet paketlerinde hata ayıklamayı desteklemek için yalnızca semboller içeren NuGet paketleri oluşturma.
author: JonDouglas
ms.author: jodou
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: d9a96986bf80aa15423d7dcee6ea3fe59255252b
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774541"
---
# <a name="creating-legacy-symbol-packages-symbolsnupkg"></a><span data-ttu-id="ec1f2-103">Eski sembol paketleri oluşturuluyor (. Symbols. nupkg)</span><span class="sxs-lookup"><span data-stu-id="ec1f2-103">Creating legacy symbol packages (.symbols.nupkg)</span></span>

> [!Important]
> <span data-ttu-id="ec1f2-104">Sembol paketleri için önerilen yeni biçim. snupkg 'dir.</span><span class="sxs-lookup"><span data-stu-id="ec1f2-104">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="ec1f2-105">Bkz. [sembol paketleri oluşturma (. snupkg)](Symbol-Packages-snupkg.md).</span><span class="sxs-lookup"><span data-stu-id="ec1f2-105">See [Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md).</span></span> </br>
> <span data-ttu-id="ec1f2-106">. Symbols. nupkg hala desteklenir ancak yalnızca uyumluluk nedenleriyle desteklenir.</span><span class="sxs-lookup"><span data-stu-id="ec1f2-106">.symbols.nupkg is still supported but only for compatibility reasons.</span></span>

<span data-ttu-id="ec1f2-107">NuGet, nuget.org veya diğer kaynaklar için paket oluşturmaya ek olarak, sembol sunucularına yayımlanmakta olabilecek ilişkili sembol paketleri oluşturmayı da destekler.</span><span class="sxs-lookup"><span data-stu-id="ec1f2-107">In addition to building packages for nuget.org or other sources, NuGet also supports creating associated symbol packages that can be published to symbol servers.</span></span> <span data-ttu-id="ec1f2-108">Eski sembol paketi biçimi. Symbols. nupkg, SymbolSource deposuna itilmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="ec1f2-108">The legacy symbol package format, .symbols.nupkg, can be pushed to the SymbolSource repository.</span></span>

<span data-ttu-id="ec1f2-109">Paket tüketicileri, Visual Studio `https://nuget.smbsrc.net` 'da, Visual Studio hata ayıklayıcısında paket koduna adımla izin veren sembol kaynaklarına eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="ec1f2-109">Package consumers can then add `https://nuget.smbsrc.net` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="ec1f2-110">Bu işlemle ilgili ayrıntılar için bkz. [Visual Studio hata ayıklayıcısında simge (. pdb) ve kaynak dosyaları belirtme](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) .</span><span class="sxs-lookup"><span data-stu-id="ec1f2-110">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

## <a name="creating-a-legacy-symbol-package"></a><span data-ttu-id="ec1f2-111">Eski sembol paketi oluşturma</span><span class="sxs-lookup"><span data-stu-id="ec1f2-111">Creating a legacy symbol package</span></span>

<span data-ttu-id="ec1f2-112">Eski bir sembol paketi oluşturmak için aşağıdaki kuralları izleyin:</span><span class="sxs-lookup"><span data-stu-id="ec1f2-112">To create a legacy symbol package, follow these conventions:</span></span>

- <span data-ttu-id="ec1f2-113">Birincil paketi (kodunuzla birlikte) adlandırın `{identifier}.nupkg` ve dosyalar hariç tüm dosyalarınızı ekleyin `.pdb` .</span><span class="sxs-lookup"><span data-stu-id="ec1f2-113">Name the primary package (with your code) `{identifier}.nupkg` and include all your files except `.pdb` files.</span></span>
- <span data-ttu-id="ec1f2-114">Eski sembol paketini adlandırın `{identifier}.symbols.nupkg` ve derleme DLL 'sini, `.pdb` DOSYALARıNıZı, xmlDoc dosyalarını, kaynak dosyalarınızı (izleyen bölümlere bakın) ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ec1f2-114">Name the legacy symbol package `{identifier}.symbols.nupkg` and include your assembly DLL, `.pdb` files, XMLDOC files, source files (see the sections that follow).</span></span>

<span data-ttu-id="ec1f2-115">`-Symbols`Bir `.nuspec` dosya ya da proje dosyasından, seçeneğiyle her iki paket de oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ec1f2-115">You can create both packages with the `-Symbols` option, either from a `.nuspec` file or a project file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

<span data-ttu-id="ec1f2-116">`pack`Mac OS X mono 4.4.2 gerektirdiğini ve Linux sistemlerinde çalışmadığına not edin.</span><span class="sxs-lookup"><span data-stu-id="ec1f2-116">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="ec1f2-117">Mac 'te Ayrıca, dosyadaki Windows yol adlarını `.nuspec` UNIX stili yollara dönüştürmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ec1f2-117">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="legacy-symbol-package-structure"></a><span data-ttu-id="ec1f2-118">Eski sembol paketi yapısı</span><span class="sxs-lookup"><span data-stu-id="ec1f2-118">Legacy symbol package structure</span></span>

<span data-ttu-id="ec1f2-119">Eski bir sembol paketi, bir kitaplık paketiyle aynı şekilde birden çok hedef çerçeveyi hedefleyebilir, bu nedenle `lib` klasörün yapısı yalnızca dll ile birlikte dosyalar dahil olmak üzere birincil paket ile tam olarak aynı olmalıdır `.pdb` .</span><span class="sxs-lookup"><span data-stu-id="ec1f2-119">A legacy symbol package can target multiple target frameworks in the same way that a library package does, so the structure of the `lib` folder should be exactly the same as the primary package, only including `.pdb` files alongside the DLL.</span></span>

<span data-ttu-id="ec1f2-120">Örneğin, .NET 4,0 ve Silverlight 4 ' ü hedefleyen eski bir sembol paketi bu düzene sahip olacaktır:</span><span class="sxs-lookup"><span data-stu-id="ec1f2-120">For example, a legacy symbol package that targets .NET 4.0 and Silverlight 4 would have this layout:</span></span>

```
\lib
    \net40
        \MyAssembly.dll
        \MyAssembly.pdb
    \sl40
        \MyAssembly.dll
        \MyAssembly.pdb
```

<span data-ttu-id="ec1f2-121">Kaynak dosyalar daha sonra adlı ayrı bir özel klasöre yerleştirilir `src` ve bu, kaynak deponuzun göreli yapısına uymalıdır.</span><span class="sxs-lookup"><span data-stu-id="ec1f2-121">Source files are then placed in a separate special folder named `src`, which must follow the relative structure of your source repository.</span></span> <span data-ttu-id="ec1f2-122">Bunun nedeni, pdb 'leri 'ın eşleşen DLL 'yi derlemek için kullanılan kaynak dosyalara mutlak yollar içermesi ve yayımlama işlemi sırasında bulunması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ec1f2-122">This is because PDBs contain absolute paths to source files used to compile the matching DLL, and they need to be found during the publishing process.</span></span> <span data-ttu-id="ec1f2-123">Temel yol (ortak yol öneki) eklenebilir. Örneğin, bu dosyalardan oluşturulmuş bir kitaplığı düşünün:</span><span class="sxs-lookup"><span data-stu-id="ec1f2-123">A base path (common path prefix) can be stripped out. For example, consider a library built from these files:</span></span>

```
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
```

<span data-ttu-id="ec1f2-124">`lib`Klasörden ayrı olarak, eski bir sembol paketinin bu düzeni içermesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="ec1f2-124">Apart from the `lib` folder, a legacy symbol package would need to contain this layout:</span></span>

```
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
```

## <a name="referring-to-files-in-the-nuspec"></a><span data-ttu-id="ec1f2-125">Nuspec içindeki dosyalara başvurma</span><span class="sxs-lookup"><span data-stu-id="ec1f2-125">Referring to files in the nuspec</span></span>

<span data-ttu-id="ec1f2-126">Eski bir sembol paketi, önceki bölümde açıklandığı gibi bir klasör yapısından veya bildirimin bölümünde içeriğini belirterek, kurallara göre derlenebilir `files` .</span><span class="sxs-lookup"><span data-stu-id="ec1f2-126">A legacy symbol package can be built by conventions, from a folder structure as described in the previous section, or by specifying its contents in the `files` section of the manifest.</span></span> <span data-ttu-id="ec1f2-127">Örneğin, önceki bölümde gösterilen paketi oluşturmak için, dosyasında aşağıdakileri kullanın `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="ec1f2-127">For example, to build the package shown in the previous section, use the following in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-legacy-symbol-package"></a><span data-ttu-id="ec1f2-128">Eski bir sembol paketi yayımlanıyor</span><span class="sxs-lookup"><span data-stu-id="ec1f2-128">Publishing a legacy symbol package</span></span>

> [!Important]
> <span data-ttu-id="ec1f2-129">Paketleri nuget.org 'e göndermek için gereken [NuGet protokollerini](../api/nuget-protocols.md)uygulayan [nuget.exe v 4.9.1 veya üzeri](https://www.nuget.org/downloads)bir sürümü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ec1f2-129">To push packages to nuget.org you must use [nuget.exe v4.9.1 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="ec1f2-130">Daha kolay olması için, önce API anahtarınızı NuGet ile kaydedin (bkz. nuget.org ve symbolsource.org için uygulanacak [bir paket yayımlama](../nuget-org/publish-a-package.md)), bu, paket sahibi olduğunuzu doğrulamak üzere NuGet.org ile kontrol edecektir.</span><span class="sxs-lookup"><span data-stu-id="ec1f2-130">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md), which will apply to both nuget.org and symbolsource.org, because symbolsource.org will check with nuget.org to verify that you are the package owner.</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. <span data-ttu-id="ec1f2-131">Birincil paketinizi nuget.org ' e yayımladıktan sonra, eski sembol paketini aşağıdaki gibi gönderin. Bu, dosya adında adı nedeniyle otomatik olarak symbolsource.org ' i kullanacaktır `.symbols` .</span><span class="sxs-lookup"><span data-stu-id="ec1f2-131">After publishing your primary package to nuget.org, push the legacy symbol package as follows, which will automatically use symbolsource.org as the target because of the `.symbols` in the filename:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. <span data-ttu-id="ec1f2-132">Farklı bir sembol deposuna yayımlamak veya adlandırma kuralını takip eden eski bir sembol paketini göndermek için `-Source` seçeneğini kullanın:</span><span class="sxs-lookup"><span data-stu-id="ec1f2-132">To publish to a different symbol repository, or to push a legacy symbol package that doesn't follow the naming convention, use the `-Source` option:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. <span data-ttu-id="ec1f2-133">Ayrıca, aşağıdakileri kullanarak hem birincil hem de sembol paketlerini aynı anda her iki depoya da gönderebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ec1f2-133">You can also push both primary and symbol packages to both repositories at the same time using the following:</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > <span data-ttu-id="ec1f2-134">nuget.exe 4.5.0 veya üzeri ile, semboller paketleri otomatik olarak symbolsource.org 'e gönderilmez. Önceki adımlarda açıklandığı gibi semboller paketlerini ayrı olarak göndermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ec1f2-134">With nuget.exe 4.5.0 or above, the symbols packages are not automatically pushed to symbolsource.org. You would need to push the symbols packages separately as explained in the earlier steps.</span></span>
   
<span data-ttu-id="ec1f2-135">Bu durumda, NuGet `MyPackage.symbols.nupkg` https://nuget.smbsrc.net/ birincil paketi NuGet.org ' ye yayımladıktan sonra, varsa NuGet (symbolsource.org için gönderim URL 'si) olarak yayımlanır.</span><span class="sxs-lookup"><span data-stu-id="ec1f2-135">In this case, NuGet will publish `MyPackage.symbols.nupkg`, if present, to https://nuget.smbsrc.net/ (the push URL for symbolsource.org), after it publishes the primary package to nuget.org.</span></span>

## <a name="see-also"></a><span data-ttu-id="ec1f2-136">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="ec1f2-136">See also</span></span>

* <span data-ttu-id="ec1f2-137">[Sembol paketleri (. snupkg) oluşturuluyor](Symbol-Packages-snupkg.md) -sembol paketleri için önerilen yeni biçim</span><span class="sxs-lookup"><span data-stu-id="ec1f2-137">[Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md) - The new recommended format for symbol packages</span></span>
* <span data-ttu-id="ec1f2-138">[Yeni SymbolSource Engine 'e geçme](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span><span class="sxs-lookup"><span data-stu-id="ec1f2-138">[Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span></span>
