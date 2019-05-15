---
title: Yeni Sembol paket biçimi '.snupkg' kullanarak NuGet sembol paketleri yayımlama | Microsoft Docs
author:
- cristinamanu
- kraigb
ms.author:
- cristinamanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: NuGet sembol paketleri (snupkg) oluşturma
keywords: NuGet sembol paketleri, hata ayıklama, hata ayıklama, paket sembolleri sembol paketi kuralları NuGet destekleyen NuGet paketi
ms.reviewer:
- anangaur
- karann
ms.openlocfilehash: 18d54e28d77f2bdcfea70ff9ae9def05278cb26c
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610562"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="61dd7-104">Sembol paketleri (.snupkg) oluşturma</span><span class="sxs-lookup"><span data-stu-id="61dd7-104">Creating symbol packages (.snupkg)</span></span>

<span data-ttu-id="61dd7-105">Sembol paketleri NuGet paketlerinizi hata ayıklama deneyimini geliştirmeye olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="61dd7-105">Symbol packages allow you to improve the debugging experience of your NuGet packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="61dd7-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="61dd7-106">Prerequisites</span></span>

<span data-ttu-id="61dd7-107">[nuget.exe v4.9.0 veya yukarıdaki](https://www.nuget.org/downloads) veya [dotnet.exe v2.2.0 veya yukarıdaki](https://www.microsoft.com/net/download/dotnet-core/2.2), hangi uygulamak gerekli [NuGet protokolleri](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="61dd7-107">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet.exe v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="61dd7-108">Bir sembol paketi oluşturma</span><span class="sxs-lookup"><span data-stu-id="61dd7-108">Creating a symbol package</span></span>

<span data-ttu-id="61dd7-109">Dotnet.exe, NuGet.exe veya MSBuild'ı kullanarak bir snupkg sembol paketi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="61dd7-109">You can create a snupkg symbol package using dotnet.exe, NuGet.exe, or MSBuild.</span></span> <span data-ttu-id="61dd7-110">NuGet.exe kullanıyorsanız .nupkg dosyasının yanı sıra bir .snupkg dosyası oluşturmak için aşağıdaki komutları kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="61dd7-110">If you're using NuGet.exe, you can use the following commands to create a .snupkg file in addition to the .nupkg file:</span></span>

```
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

<span data-ttu-id="61dd7-111">Dotnet.exe veya MSBuild'ı kullanıyorsanız .nupkg dosyasının yanı sıra bir .snupkg dosyası oluşturmak için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="61dd7-111">If you're using dotnet.exe or MSBuild, use the following steps to create a .snupkg file in addition to the .nupkg file:</span></span>

1. <span data-ttu-id="61dd7-112">Aşağıdaki özellikler için .csproj dosyasını ekleyin:</span><span class="sxs-lookup"><span data-stu-id="61dd7-112">Add the following properties to your .csproj file:</span></span>

    ```xml
    <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
    </PropertyGroup>
    ```

1. <span data-ttu-id="61dd7-113">Projenizle paketi `dotnet pack MyPackage.csproj` veya `msbuild -t:pack MyPackage.csproj`.</span><span class="sxs-lookup"><span data-stu-id="61dd7-113">Pack your project with `dotnet pack MyPackage.csproj` or `msbuild -t:pack MyPackage.csproj`.</span></span>

<span data-ttu-id="61dd7-114">[ `SymbolPackageFormat` ](/dotnet/core/tools/csproj.md#symbolpackageformat) Özelliği iki değerden birine sahip olabilir: `symbols.nupkg` (varsayılan) veya `snupkg`.</span><span class="sxs-lookup"><span data-stu-id="61dd7-114">The [`SymbolPackageFormat`](/dotnet/core/tools/csproj.md#symbolpackageformat) property can have one of two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="61dd7-115">Varsa [ `SymbolPackageFormat` ](/dotnet/core/tools/csproj.md#symbolpackageformat) özelliği belirtilmezse, eski sembol paketi oluşturulacak.</span><span class="sxs-lookup"><span data-stu-id="61dd7-115">If the [`SymbolPackageFormat`](/dotnet/core/tools/csproj.md#symbolpackageformat) property is not specified, a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="61dd7-116">Eski biçim `.symbols.nupkg` ancak yalnızca uyumluluk açısından hala desteklenmektedir (bkz [eski sembol paketleri](Symbol-Packages.md)).</span><span class="sxs-lookup"><span data-stu-id="61dd7-116">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="61dd7-117">Sembol sunucusuna NuGet.org yalnızca yeni sembol paket biçimi - kabul `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="61dd7-117">NuGet.org's symbol server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="61dd7-118">Bir sembol Paketi Yayımlama</span><span class="sxs-lookup"><span data-stu-id="61dd7-118">Publishing a symbol package</span></span>

1. <span data-ttu-id="61dd7-119">Kolaylık olması için NuGet ile ilk API anahtarınızı kaydedin (bkz [paket yayımlama](../create-packages/publish-a-package.md)).</span><span class="sxs-lookup"><span data-stu-id="61dd7-119">For convenience, first save your API key with NuGet (see [publish a package](../create-packages/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="61dd7-120">Nuget.org için birincil paketinizi yayımladıktan sonra aşağıdaki gibi sembol paketi gönderin.</span><span class="sxs-lookup"><span data-stu-id="61dd7-120">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="61dd7-121">Ayrıca hem birincil hem de anında iletme ve sembol kullanarak aynı anda paketleri aşağıdaki komutu.</span><span class="sxs-lookup"><span data-stu-id="61dd7-121">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="61dd7-122">.Nupkg hem .snupkg dosyaları geçerli klasörde mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="61dd7-122">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="61dd7-123">NuGet nuget.org için her iki paketi yayımlar. `MyPackage.nupkg` ilk yayımlama, ardından `MyPackage.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="61dd7-123">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

> [!Note]
> <span data-ttu-id="61dd7-124">NuGet.org kaynağı olarak yapılandırdığınız sembol paketi yayımlanmış değil, denetleyin `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="61dd7-124">If the symbol package isn't published, check that you've configured the NuGet.org source as `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="61dd7-125">Sembol Paketi Yayımlama tarafından desteklenen yalnızca [NuGet V3 API](../api/overview.md#versioning).</span><span class="sxs-lookup"><span data-stu-id="61dd7-125">Symbol package publishing is only supported by [the NuGet V3 API](../api/overview.md#versioning).</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="61dd7-126">NuGet.org sembol sunucusu</span><span class="sxs-lookup"><span data-stu-id="61dd7-126">NuGet.org symbol server</span></span>

<span data-ttu-id="61dd7-127">NuGet.org kendi sembolleri sunucu deposu destekler ve yalnızca yeni sembol paket biçimi - kabul `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="61dd7-127">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="61dd7-128">Paketi tüketicileri, sembol sunucusuna nuget.org ekleyerek yayımlanan simgeleri kullanabilirsiniz `https://symbols.nuget.org/download/symbols` kendi sembol kaynaklarına Visual Studio'da sağlayan Visual Studio hata ayıklayıcısı paket kod içine Adımlama.</span><span class="sxs-lookup"><span data-stu-id="61dd7-128">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="61dd7-129">Bkz: [Visual Studio hata ayıklayıcısında simge (.pdb) ve kaynak dosyaları belirtme](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017) işlem hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="61dd7-129">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="61dd7-130">Nuget.org sembol paketi kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="61dd7-130">Nuget.org symbol package constraints</span></span>

<span data-ttu-id="61dd7-131">Sembol paketleri nuget.org üzerinde desteklenen aşağıdaki kısıtlamaları vardır.</span><span class="sxs-lookup"><span data-stu-id="61dd7-131">The symbol packages supported on nuget.org have the following contraints</span></span>

- <span data-ttu-id="61dd7-132">Yalnızca aşağıdaki dosya uzantılarını sembol pakete eklenecek izin verilir.</span><span class="sxs-lookup"><span data-stu-id="61dd7-132">Only the following file extensions are allowed to be added to a symbol package.</span></span> ```.pdb,.nuspec,.xml,.psmdcp,.rels,.p7s```
- <span data-ttu-id="61dd7-133">Yalnızca yönetilen [taşınabilir pdb](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) nuget sembol sunucusunda şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="61dd7-133">Only managed [Portable pdbs](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are currently supported on nuget symbol server.</span></span>
- <span data-ttu-id="61dd7-134">Ekli PDB'ler ve ilişkili nupkg DLL'lerini Visual Studio sürüm 15.9 ya da üzeri derleyici ile oluşturulması gereken (bkz [pdb şifreleme karması](https://github.com/dotnet/roslyn/issues/24429))</span><span class="sxs-lookup"><span data-stu-id="61dd7-134">The pdbs and associated nupkg dlls need to be built with the compiler in Visual Studio version 15.9 or above (see [pdb crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="61dd7-135">Sembol Paketi Yayımlama üzerinde herhangi bir dosya türünün içinde .snupkg eklediyseniz nuget.org başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="61dd7-135">The symbol package publish on nuget.org will fail if any other file types are included in the .snupkg.</span></span>

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="61dd7-136">Sembol paketi doğrulama ve dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="61dd7-136">Symbol package validation and indexing</span></span>

<span data-ttu-id="61dd7-137">Sembol paketleri yayımlanan [NuGet.org](https://www.nuget.org/) virüs denetimleri gibi çeşitli doğrulamaları geçeriz.</span><span class="sxs-lookup"><span data-stu-id="61dd7-137">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, such as virus checks.</span></span>

<span data-ttu-id="61dd7-138">Paket tüm doğrulama denetimlerini geçtiğinde, dizin ve NuGet.org sembol sunucularından tüketim için kullanılabilir semboller için biraz sürebilir.</span><span class="sxs-lookup"><span data-stu-id="61dd7-138">When the package has passed all validation checks, it might take a while for the symbols to index and be available for consumption from the NuGet.org symbol servers.</span></span> <span data-ttu-id="61dd7-139">Paket doğrulama denetimi başarısız olursa .nupkg için Paket Ayrıntıları sayfasına ilgili hatayı görüntülemek için güncelleştirir ve ayrıca bunu bildiren bir e-posta alırsınız.</span><span class="sxs-lookup"><span data-stu-id="61dd7-139">If the package fails a validation check, the package details page for the .nupkg will update to display the associated error and you will also receive an email notifying you about it.</span></span>

<span data-ttu-id="61dd7-140">Paket doğrulaması ve dizin oluşturma genellikle 15 dakika alır.</span><span class="sxs-lookup"><span data-stu-id="61dd7-140">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="61dd7-141">Paket yayımlama beklenenden daha uzun sürerse ziyaret [status.nuget.org](https://status.nuget.org/) nuget.org herhangi bir kesinti yaşıyor olmadığını denetlemek için.</span><span class="sxs-lookup"><span data-stu-id="61dd7-141">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if nuget.org is experiencing any interruptions.</span></span> <span data-ttu-id="61dd7-142">Tüm sistemler çalışır durumda ve paket başarıyla bir saat içinde yayımlanmadı Lütfen nuget.org için oturum açın ve Paket Ayrıntıları sayfasına başvurun destek bağlantısı kullanarak bize ulaşın.</span><span class="sxs-lookup"><span data-stu-id="61dd7-142">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="61dd7-143">Sembol paket yapısı</span><span class="sxs-lookup"><span data-stu-id="61dd7-143">Symbol package structure</span></span>

<span data-ttu-id="61dd7-144">.Nupkg dosyanın tam olarak aynı bugün olduğu halde .snupkg dosya aşağıdaki özelliklere sahip gibi olacaktır:</span><span class="sxs-lookup"><span data-stu-id="61dd7-144">The .nupkg file would be exactly the same as it is today, but the .snupkg file would have the following characteristics:</span></span>

1) <span data-ttu-id="61dd7-145">.snupkg karşılık gelen .nupkg aynı kimliği ve sürüm gerekir.</span><span class="sxs-lookup"><span data-stu-id="61dd7-145">The .snupkg will have the same id and version as the corresponding .nupkg.</span></span>
2) <span data-ttu-id="61dd7-146">.snupkg tam klasör yapısını yerine dll/exe, aynı klasör hiyerarşisindeki karşılık gelen kendi pdb eklenecek ayrım ile DLL veya EXE dosyaları için nupkg olur.</span><span class="sxs-lookup"><span data-stu-id="61dd7-146">The .snupkg will have the exact folder structure as the nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="61dd7-147">PDB dışında uzantıları ile dosya ve klasörleri snupkg dışında bırakılır.</span><span class="sxs-lookup"><span data-stu-id="61dd7-147">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="61dd7-148">.snupkg .nuspec dosyasında da yeni bir PackageType aşağıdaki gibi belirtin.</span><span class="sxs-lookup"><span data-stu-id="61dd7-148">The .nuspec file in the .snupkg will also specify a new PackageType as below.</span></span> <span data-ttu-id="61dd7-149">Bu, belirtilen yalnızca bir PackageType gerekir.</span><span class="sxs-lookup"><span data-stu-id="61dd7-149">This should the only one PackageType specified.</span></span> 
``` 
<packageTypes>
  <packageType name="SymbolsPackage"/>
</packageTypes>
```
4) <span data-ttu-id="61dd7-150">Bir yazar kendi nupkg ve snupkg oluşturmak için özel bir nuspec kullanmaya karar verirse, snupkg 2'de ayrıntılı dosya ve klasör hiyerarşisi aynı olmalıdır).</span><span class="sxs-lookup"><span data-stu-id="61dd7-150">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="61dd7-151">```authors``` ve ```owners``` alan snupkg'ın nuspec ' çıkarılır.</span><span class="sxs-lookup"><span data-stu-id="61dd7-151">```authors``` and ```owners``` field will be excluded from the snupkg's nuspec.</span></span>

## <a name="see-also"></a><span data-ttu-id="61dd7-152">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="61dd7-152">See Also</span></span>

[<span data-ttu-id="61dd7-153">NuGet-Package - hata ayıklama - ve - sembolleri - iyileştirmeler</span><span class="sxs-lookup"><span data-stu-id="61dd7-153">NuGet-Package-Debugging-&-Symbols-Improvements</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)
