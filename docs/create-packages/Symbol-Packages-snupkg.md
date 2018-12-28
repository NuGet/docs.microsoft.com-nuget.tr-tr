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
ms.openlocfilehash: 1fbb243a7b3518307a393b5f371feae1edb7623a
ms.sourcegitcommit: 5c5f0f0e1f79098e27d9566dd98371f6ee16f8b5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645665"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="f088b-104">Sembol paketleri (.snupkg) oluşturma</span><span class="sxs-lookup"><span data-stu-id="f088b-104">Creating symbol packages (.snupkg)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f088b-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="f088b-105">Prerequisites</span></span>

<span data-ttu-id="f088b-106">[nuget.exe v4.9.0 veya yukarıdaki](https://www.nuget.org/downloads) veya [dotnet.exe v2.2.0 veya yukarıdaki](https://www.microsoft.com/net/download/dotnet-core/2.2), hangi uygulamak gerekli [NuGet protokolleri](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="f088b-106">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet.exe v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="f088b-107">Bir sembol paketi oluşturma</span><span class="sxs-lookup"><span data-stu-id="f088b-107">Creating a symbol package</span></span>

<span data-ttu-id="f088b-108">Bir .nuspec dosyası veya .csproj dosyasını bir snupkg sembol paketi oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="f088b-108">A snupkg symbol package can be created from a .nuspec file or from a .csproj file.</span></span> <span data-ttu-id="f088b-109">NuGet.exe ve dotnet.exe her ikisi de desteklenir.</span><span class="sxs-lookup"><span data-stu-id="f088b-109">NuGet.exe and dotnet.exe are both supported.</span></span> <span data-ttu-id="f088b-110">Zaman seçenekleri ```-Symbols -SymbolPackageFormat snupkg``` .snupkg dosya .nupkg dosyasına ek olarak oluşturulacak nuget.exe paketi komutu kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f088b-110">When the options ```-Symbols -SymbolPackageFormat snupkg``` are used on the nuget.exe pack command a .snupkg file will be created in addition to the .nupkg file.</span></span>

<span data-ttu-id="f088b-111">Örnek komutlar .snupkg dosyaları oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="f088b-111">Example commands to create .snupkg files</span></span>
```
dotnet pack MyPackage.csproj --include-symbols -p:SymbolPackageFormat=snupkg

nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg

msbuild -t:pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
```

<span data-ttu-id="f088b-112">`.snupkgs` Varsayılan olarak oluşturulan değil.</span><span class="sxs-lookup"><span data-stu-id="f088b-112">`.snupkgs` are not produced by default.</span></span> <span data-ttu-id="f088b-113">Geçmesi gereken `SymbolPackageFormat` özelliği ile birlikte `-Symbols` nuget.exe durumunda `--include-symbols` dotnet.exe, durumunda veya `-p:IncludeSymbols` msbuild durumunda.</span><span class="sxs-lookup"><span data-stu-id="f088b-113">You must pass the `SymbolPackageFormat` property along with `-Symbols` in case of nuget.exe, `--include-symbols` in case of dotnet.exe, or `-p:IncludeSymbols` in case of msbuild.</span></span>

<span data-ttu-id="f088b-114">SymbolPackageFormat özelliği iki değerden birine sahip olabilir: `symbols.nupkg` (varsayılan) veya `snupkg`.</span><span class="sxs-lookup"><span data-stu-id="f088b-114">SymbolPackageFormat property can have one of the two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="f088b-115">SymbolPackageFormat belirtilmezse, varsayılan `symbols.nupkg` ve eski sembol paketi oluşturulacak.</span><span class="sxs-lookup"><span data-stu-id="f088b-115">If the SymbolPackageFormat is not specified, it defaults to `symbols.nupkg` and a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="f088b-116">Eski biçim `.symbols.nupkg` ancak yalnızca uyumluluk açısından hala desteklenmektedir (bkz [eski sembol paketleri](Symbol-Packages.md)).</span><span class="sxs-lookup"><span data-stu-id="f088b-116">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="f088b-117">Sembol sunucusuna NuGet.org yalnızca yeni sembol paket biçimi - kabul `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="f088b-117">NuGet.org symbols server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="f088b-118">Bir sembol Paketi Yayımlama</span><span class="sxs-lookup"><span data-stu-id="f088b-118">Publishing a symbol package</span></span>

1. <span data-ttu-id="f088b-119">Kolaylık olması için NuGet ile ilk API anahtarınızı kaydedin (bkz [paket yayımlama](../create-packages/publish-a-package.md)).</span><span class="sxs-lookup"><span data-stu-id="f088b-119">For convenience, first save your API key with NuGet (see [publish a package](../create-packages/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="f088b-120">Nuget.org için birincil paketinizi yayımladıktan sonra aşağıdaki gibi sembol paketi gönderin.</span><span class="sxs-lookup"><span data-stu-id="f088b-120">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="f088b-121">Ayrıca hem birincil hem de anında iletme ve sembol kullanarak aynı anda paketleri aşağıdaki komutu.</span><span class="sxs-lookup"><span data-stu-id="f088b-121">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="f088b-122">.Nupkg hem .snupkg dosyaları geçerli klasörde mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f088b-122">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="f088b-123">NuGet nuget.org için her iki paketi yayımlar. `MyPackage.nupkg` ilk yayımlama, ardından `MyPackage.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="f088b-123">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="f088b-124">NuGet.org sembol sunucusu</span><span class="sxs-lookup"><span data-stu-id="f088b-124">NuGet.org symbol server</span></span>

<span data-ttu-id="f088b-125">NuGet.org kendi sembolleri sunucu deposu destekler ve yalnızca yeni sembol paket biçimi - kabul `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="f088b-125">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="f088b-126">Paketi tüketicileri, sembol sunucusuna nuget.org ekleyerek yayımlanan simgeleri kullanabilirsiniz `https://symbols.nuget.org/download/symbols` kendi sembol kaynaklarına Visual Studio'da sağlayan Visual Studio hata ayıklayıcısı paket kod içine Adımlama.</span><span class="sxs-lookup"><span data-stu-id="f088b-126">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="f088b-127">Bkz: [Visual Studio hata ayıklayıcısında simge (.pdb) ve kaynak dosyaları belirtme](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017) işlem hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="f088b-127">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="f088b-128">Nuget.org sembol paketi kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="f088b-128">Nuget.org symbol package constraints</span></span>

<span data-ttu-id="f088b-129">Sembol paketleri nuget.org üzerinde desteklenen aşağıdaki kısıtlamaları vardır.</span><span class="sxs-lookup"><span data-stu-id="f088b-129">The symbol packages supported on nuget.org have the following contraints</span></span>

- <span data-ttu-id="f088b-130">Yalnızca aşağıdaki dosya uzantılarını sembol pakete eklenecek izin verilir.</span><span class="sxs-lookup"><span data-stu-id="f088b-130">Only the following file extensions are allowed to be added to a symbol package.</span></span> ```.pdb,.nuspec,.xml,.psmdcp,.rels,.p7s```
- <span data-ttu-id="f088b-131">Yalnızca yönetilen [taşınabilir pdb](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) nuget sembol sunucusunda şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="f088b-131">Only managed [Portable pdbs](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are currently supported on nuget symbol server.</span></span>
- <span data-ttu-id="f088b-132">Ekli PDB'ler ve ilişkili nupkg DLL'lerini Visual Studio sürüm 15.9 ya da üzeri derleyici ile oluşturulması gereken (bkz [pdb şifreleme karması](https://github.com/dotnet/roslyn/issues/24429))</span><span class="sxs-lookup"><span data-stu-id="f088b-132">The pdbs and associated nupkg dlls need to be built with the compiler in Visual Studio version 15.9 or above (see [pdb crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="f088b-133">Sembol Paketi Yayımlama üzerinde herhangi bir dosya türünün içinde .snupkg eklediyseniz nuget.org başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="f088b-133">The symbol package publish on nuget.org will fail if any other file types are included in the .snupkg.</span></span>

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="f088b-134">Sembol paketi doğrulama ve dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="f088b-134">Symbol package validation and indexing</span></span>

<span data-ttu-id="f088b-135">Sembol paketleri yayımlanan [NuGet.org](https://www.nuget.org/) virüs denetimleri gibi çeşitli doğrulamaları geçeriz.</span><span class="sxs-lookup"><span data-stu-id="f088b-135">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, such as virus checks.</span></span>

<span data-ttu-id="f088b-136">Paket tüm doğrulama denetimlerini geçtiğinde, dizin ve NuGet.org sembol sunucularından tüketim için kullanılabilir semboller için biraz sürebilir.</span><span class="sxs-lookup"><span data-stu-id="f088b-136">When the package has passed all validation checks, it might take a while for the symbols to index and be available for consumption from the NuGet.org symbol servers.</span></span> <span data-ttu-id="f088b-137">Paket doğrulama denetimi başarısız olursa .nupkg için Paket Ayrıntıları sayfasına ilgili hatayı görüntülemek için güncelleştirir ve ayrıca bunu bildiren bir e-posta alırsınız.</span><span class="sxs-lookup"><span data-stu-id="f088b-137">If the package fails a validation check, the package details page for the .nupkg will update to display the associated error and you will also receive an email notifying you about it.</span></span>

<span data-ttu-id="f088b-138">Paket doğrulaması ve dizin oluşturma genellikle 15 dakika alır.</span><span class="sxs-lookup"><span data-stu-id="f088b-138">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="f088b-139">Paket yayımlama beklenenden daha uzun sürerse ziyaret [status.nuget.org](https://status.nuget.org/) nuget.org herhangi bir kesinti yaşıyor olmadığını denetlemek için.</span><span class="sxs-lookup"><span data-stu-id="f088b-139">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if nuget.org is experiencing any interruptions.</span></span> <span data-ttu-id="f088b-140">Tüm sistemler çalışır durumda ve paket başarıyla bir saat içinde yayımlanmadı Lütfen nuget.org için oturum açın ve Paket Ayrıntıları sayfasına başvurun destek bağlantısı kullanarak bize ulaşın.</span><span class="sxs-lookup"><span data-stu-id="f088b-140">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="f088b-141">Sembol paket yapısı</span><span class="sxs-lookup"><span data-stu-id="f088b-141">Symbol package structure</span></span>

<span data-ttu-id="f088b-142">.Nupkg dosyanın tam olarak aynı bugün olduğu halde .snupkg dosya aşağıdaki özelliklere sahip gibi olacaktır:</span><span class="sxs-lookup"><span data-stu-id="f088b-142">The .nupkg file would be exactly the same as it is today, but the .snupkg file would have the following characteristics:</span></span>

1) <span data-ttu-id="f088b-143">.snupkg karşılık gelen .nupkg aynı kimliği ve sürüm gerekir.</span><span class="sxs-lookup"><span data-stu-id="f088b-143">The .snupkg will have the same id and version as the corresponding .nupkg.</span></span>
2) <span data-ttu-id="f088b-144">.snupkg tam klasör yapısını yerine dll/exe, aynı klasör hiyerarşisindeki karşılık gelen kendi pdb eklenecek ayrım ile DLL veya EXE dosyaları için nupkg olur.</span><span class="sxs-lookup"><span data-stu-id="f088b-144">The .snupkg will have the exact folder structure as the nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="f088b-145">PDB dışında uzantıları ile dosya ve klasörleri snupkg dışında bırakılır.</span><span class="sxs-lookup"><span data-stu-id="f088b-145">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="f088b-146">.snupkg .nuspec dosyasında da yeni bir PackageType aşağıdaki gibi belirtin.</span><span class="sxs-lookup"><span data-stu-id="f088b-146">The .nuspec file in the .snupkg will also specify a new PackageType as below.</span></span> <span data-ttu-id="f088b-147">Bu, belirtilen yalnızca bir PackageType gerekir.</span><span class="sxs-lookup"><span data-stu-id="f088b-147">This should the only one PackageType specified.</span></span> 
``` 
<packageTypes>
  <packageType name="SymbolsPackage"/>
</packageTypes>
```
4) <span data-ttu-id="f088b-148">Bir yazar kendi nupkg ve snupkg oluşturmak için özel bir nuspec kullanmaya karar verirse, snupkg 2'de ayrıntılı dosya ve klasör hiyerarşisi aynı olmalıdır).</span><span class="sxs-lookup"><span data-stu-id="f088b-148">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="f088b-149">```authors``` ve ```owners``` alan snupkg'ın nuspec ' çıkarılır.</span><span class="sxs-lookup"><span data-stu-id="f088b-149">```authors``` and ```owners``` field will be excluded from the snupkg's nuspec.</span></span>

## <a name="see-also"></a><span data-ttu-id="f088b-150">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="f088b-150">See Also</span></span>

[<span data-ttu-id="f088b-151">NuGet-Package - hata ayıklama - ve - sembolleri - iyileştirmeler</span><span class="sxs-lookup"><span data-stu-id="f088b-151">NuGet-Package-Debugging-&-Symbols-Improvements</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)
