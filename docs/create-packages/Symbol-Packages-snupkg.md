---
title: Yeni sembol paketi biçimi '. snupkg ' kullanarak NuGet sembol paketleri yayımlama | Microsoft Docs
author: cristinamanu
ms.author: cristinamanu
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: NuGet sembol paketleri oluşturma (snupkg).
keywords: NuGet sembol paketleri, NuGet paket hata ayıklaması, NuGet hata ayıklamayı destekleme, paket sembolleri, sembol paketi kuralları
ms.reviewer:
- anangaur
- karann
ms.openlocfilehash: 109df18bcfd3e6a3fbd3ef3da1707ffada585140
ms.sourcegitcommit: f4bfdbf62302c95f1f39e81ccf998f8bbc6d56b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70749036"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="612ec-104">Sembol paketleri (. snupkg) oluşturuluyor</span><span class="sxs-lookup"><span data-stu-id="612ec-104">Creating symbol packages (.snupkg)</span></span>

<span data-ttu-id="612ec-105">Sembol paketleri, NuGet paketlerinizin hata ayıklama deneyimini iyileştirmenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="612ec-105">Symbol packages allow you to improve the debugging experience of your NuGet packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="612ec-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="612ec-106">Prerequisites</span></span>

<span data-ttu-id="612ec-107">gerekli [NuGet protokollerini](../api/nuget-protocols.md)uygulayan [NuGet. exe v 4.9.0 veya üzeri](https://www.nuget.org/downloads) ya da [DotNet. exe v 2.2.0 veya üzeri](https://www.microsoft.com/net/download/dotnet-core/2.2).</span><span class="sxs-lookup"><span data-stu-id="612ec-107">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet.exe v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="612ec-108">Sembol paketi oluşturma</span><span class="sxs-lookup"><span data-stu-id="612ec-108">Creating a symbol package</span></span>

<span data-ttu-id="612ec-109">DotNet. exe veya MSBuild kullanıyorsanız,. nupkg dosyasına ek olarak. `IncludeSymbols` snupkg dosyası oluşturmak için ve `SymbolPackageFormat` özelliklerini ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="612ec-109">If you're using dotnet.exe or MSBuild, you need to set the `IncludeSymbols` and `SymbolPackageFormat` properties to create a .snupkg file in addition to the .nupkg file.</span></span>

* <span data-ttu-id="612ec-110">Aşağıdaki özellikleri. csproj dosyanıza ekleyin:</span><span class="sxs-lookup"><span data-stu-id="612ec-110">Either add the following properties to your .csproj file:</span></span>

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols> 
      <SymbolPackageFormat>snupkg</SymbolPackageFormat> 
   </PropertyGroup>
   ```

* <span data-ttu-id="612ec-111">Veya komut satırında aşağıdaki özellikleri belirtin:</span><span class="sxs-lookup"><span data-stu-id="612ec-111">Or specify these properties on the command-line:</span></span>

     ```cli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  <span data-ttu-id="612ec-112">veya</span><span class="sxs-lookup"><span data-stu-id="612ec-112">or</span></span>

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

<span data-ttu-id="612ec-113">NuGet. exe kullanıyorsanız,. nupkg dosyasına ek olarak bir. snupkg dosyası oluşturmak için aşağıdaki komutları kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="612ec-113">If you're using NuGet.exe, you can use the following commands to create a .snupkg file in addition to the .nupkg file:</span></span>

```
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

<span data-ttu-id="612ec-114">Özellik iki değerden birine sahip olabilir: `symbols.nupkg` (varsayılan) veya `snupkg`. [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat)</span><span class="sxs-lookup"><span data-stu-id="612ec-114">The [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) property can have one of two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="612ec-115">Bu özellik belirtilmezse, eski bir sembol paketi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="612ec-115">If this property is not specified, a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="612ec-116">Eski biçim `.symbols.nupkg` hala desteklenir, ancak yalnızca uyumluluk nedenleriyle desteklenir (bkz. [eski sembol paketleri](Symbol-Packages.md)).</span><span class="sxs-lookup"><span data-stu-id="612ec-116">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="612ec-117">NuGet. org 'ın sembol sunucusu yalnızca yeni sembol paketi biçimini kabul eder- `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="612ec-117">NuGet.org's symbol server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="612ec-118">Sembol paketi yayımlama</span><span class="sxs-lookup"><span data-stu-id="612ec-118">Publishing a symbol package</span></span>

1. <span data-ttu-id="612ec-119">Kolaylık olması için önce API anahtarınızı NuGet ile kaydedin (bkz. [bir paket yayımlama](../nuget-org/publish-a-package.md)).</span><span class="sxs-lookup"><span data-stu-id="612ec-119">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="612ec-120">Birincil paketinizi nuget.org 'e yayımladıktan sonra, sembol paketini aşağıdaki gibi gönderin.</span><span class="sxs-lookup"><span data-stu-id="612ec-120">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="612ec-121">Ayrıca, aşağıdaki komutu kullanarak hem birincil hem de sembol paketlerini aynı anda gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="612ec-121">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="612ec-122">. Nupkg ve. snupkg dosyalarının her ikisi de geçerli klasörde bulunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="612ec-122">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="612ec-123">NuGet, her iki paketi de nuget.org 'e yayımlar. önce yayımlanacak ve `MyPackage.snupkg`ardından. `MyPackage.nupkg`</span><span class="sxs-lookup"><span data-stu-id="612ec-123">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

> [!Note]
> <span data-ttu-id="612ec-124">Sembol paketi yayınlanmamışsa, NuGet.org kaynağını olarak `https://api.nuget.org/v3/index.json`yapılandırdığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="612ec-124">If the symbol package isn't published, check that you've configured the NuGet.org source as `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="612ec-125">Sembol paketi yayımlaması yalnızca [NuGet v3 API 'si](../api/overview.md#versioning)tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="612ec-125">Symbol package publishing is only supported by [the NuGet V3 API](../api/overview.md#versioning).</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="612ec-126">NuGet.org symbol sunucusu</span><span class="sxs-lookup"><span data-stu-id="612ec-126">NuGet.org symbol server</span></span>

<span data-ttu-id="612ec-127">NuGet.org kendi sembol sunucu deposunu destekler ve yalnızca yeni sembol paketi biçimini kabul eder- `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="612ec-127">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="612ec-128">Paket tüketicileri Visual Studio 'daki sembol kaynaklarına ekleyerek `https://symbols.nuget.org/download/symbols` NuGet.org sembol sunucusunda yayınlanan sembolleri kullanarak Visual Studio hata ayıklayıcısında paket koduna adımlamayı sağlar.</span><span class="sxs-lookup"><span data-stu-id="612ec-128">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="612ec-129">Bu işlemle ilgili ayrıntılar için bkz. [Visual Studio hata ayıklayıcısında simge (. pdb) ve kaynak dosyaları belirtme](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017) .</span><span class="sxs-lookup"><span data-stu-id="612ec-129">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="612ec-130">Nuget.org sembol paketi kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="612ec-130">Nuget.org symbol package constraints</span></span>

<span data-ttu-id="612ec-131">Nuget.org üzerinde desteklenen sembol paketleri aşağıdaki gibi olabilir</span><span class="sxs-lookup"><span data-stu-id="612ec-131">The symbol packages supported on nuget.org have the following contraints</span></span>

- <span data-ttu-id="612ec-132">Bir sembol paketine yalnızca aşağıdaki dosya uzantılarının eklenmesine izin verilir.</span><span class="sxs-lookup"><span data-stu-id="612ec-132">Only the following file extensions are allowed to be added to a symbol package.</span></span> ```.pdb,.nuspec,.xml,.psmdcp,.rels,.p7s```
- <span data-ttu-id="612ec-133">Şu anda yalnızca Managed [Taşınabilir pdb 'leri](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) , NuGet sembol sunucusunda destekleniyor.</span><span class="sxs-lookup"><span data-stu-id="612ec-133">Only managed [Portable pdbs](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are currently supported on nuget symbol server.</span></span>
- <span data-ttu-id="612ec-134">Pdb 'leri ve ilişkili nupkg dll 'lerinin Visual Studio sürüm 15,9 veya üzeri bir derleyici ile oluşturulması gerekir (bkz. [pdb şifre karması](https://github.com/dotnet/roslyn/issues/24429))</span><span class="sxs-lookup"><span data-stu-id="612ec-134">The pdbs and associated nupkg dlls need to be built with the compiler in Visual Studio version 15.9 or above (see [pdb crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="612ec-135">. Snupkg 'ye başka herhangi bir dosya türü dahil olursa, nuget.org üzerinde Yayımla sembol paketi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="612ec-135">The symbol package publish on nuget.org will fail if any other file types are included in the .snupkg.</span></span>

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="612ec-136">Sembol paketi doğrulama ve dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="612ec-136">Symbol package validation and indexing</span></span>

<span data-ttu-id="612ec-137">[NuGet.org](https://www.nuget.org/) ' de yayınlanan sembol paketleri, virüs denetimleri gibi çeşitli Doğrulamalardan biridir.</span><span class="sxs-lookup"><span data-stu-id="612ec-137">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, such as virus checks.</span></span>

<span data-ttu-id="612ec-138">Paket tüm doğrulama denetimlerini geçtiğinde, simgeler dizin oluşturma ve NuGet.org sembol sunucularından tüketim için kullanılabilir hale gelmesi biraz zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="612ec-138">When the package has passed all validation checks, it might take a while for the symbols to index and be available for consumption from the NuGet.org symbol servers.</span></span> <span data-ttu-id="612ec-139">Paket bir doğrulama denetiminden geçemezse,. nupkg için paket ayrıntıları sayfası, ilişkili hatayı görüntüleyecek şekilde güncellenecek ve size bunu bildiren bir e-posta alacaksınız.</span><span class="sxs-lookup"><span data-stu-id="612ec-139">If the package fails a validation check, the package details page for the .nupkg will update to display the associated error and you will also receive an email notifying you about it.</span></span>

<span data-ttu-id="612ec-140">Paket doğrulama ve dizin oluşturma genellikle 15 dakika boyunca sürer.</span><span class="sxs-lookup"><span data-stu-id="612ec-140">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="612ec-141">Paket yayımlaması beklenenden uzun sürüyorsa, nuget.org 'in herhangi bir kesinti yaşamadığını denetlemek için [Status.NuGet.org](https://status.nuget.org/) adresini ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="612ec-141">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if nuget.org is experiencing any interruptions.</span></span> <span data-ttu-id="612ec-142">Tüm sistemler çalışır durumda ve paket bir saat içinde başarıyla yayımlanmamışsa, lütfen nuget.org ' e oturum açın ve paket ayrıntıları sayfasında desteğe başvurun bağlantısını kullanarak bizimle iletişime geçin.</span><span class="sxs-lookup"><span data-stu-id="612ec-142">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="612ec-143">Sembol paketi yapısı</span><span class="sxs-lookup"><span data-stu-id="612ec-143">Symbol package structure</span></span>

<span data-ttu-id="612ec-144">. Nupkg dosyası bugün olduğu gibi tamamen aynıdır, ancak. snupkg dosyası aşağıdaki özelliklere sahip olacaktır:</span><span class="sxs-lookup"><span data-stu-id="612ec-144">The .nupkg file would be exactly the same as it is today, but the .snupkg file would have the following characteristics:</span></span>

1) <span data-ttu-id="612ec-145">. Snupkg, karşılık gelen. nupkg ile aynı kimliğe ve sürüme sahip olacaktır.</span><span class="sxs-lookup"><span data-stu-id="612ec-145">The .snupkg will have the same id and version as the corresponding .nupkg.</span></span>
2) <span data-ttu-id="612ec-146">. Snupkg, DLL 'Ler veya EXE dosyaları için, dll/EXEs yerine, karşılık gelen pdb 'leri aynı klasör hiyerarşisine dahil edilecek şekilde tam klasör yapısına sahip olur.</span><span class="sxs-lookup"><span data-stu-id="612ec-146">The .snupkg will have the exact folder structure as the nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="612ec-147">PDB 'den farklı uzantılara sahip dosyalar ve klasörler, snupkg 'dan bırakılır.</span><span class="sxs-lookup"><span data-stu-id="612ec-147">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="612ec-148">. Snupkg içindeki. nuspec dosyası, aşağıda gösterildiği gibi yeni bir PackageType de belirtir.</span><span class="sxs-lookup"><span data-stu-id="612ec-148">The .nuspec file in the .snupkg will also specify a new PackageType as below.</span></span> <span data-ttu-id="612ec-149">Bu, tek bir PackageType belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="612ec-149">This should the only one PackageType specified.</span></span>

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) <span data-ttu-id="612ec-150">Bir yazar, nupkg ve snupkg 'leri oluşturmak için özel bir nuspec kullanılmasına karar verirse, snupkg, aynı klasör hiyerarşisine ve 2 ' de ayrıntılı dosyalar içermelidir.</span><span class="sxs-lookup"><span data-stu-id="612ec-150">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="612ec-151">```authors```ve ```owners``` alan, snupkg 'dan nuspec 'ten çıkarılacak.</span><span class="sxs-lookup"><span data-stu-id="612ec-151">```authors``` and ```owners``` field will be excluded from the snupkg's nuspec.</span></span>
6) <span data-ttu-id="612ec-152">```<license>``` Öğesini kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="612ec-152">Do not use the ```<license>``` element.</span></span> <span data-ttu-id="612ec-153">A. snupkg, karşılık gelen. nupkg ile aynı lisans kapsamında ele alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="612ec-153">A .snupkg is covered under the same license as the corresponding .nupkg.</span></span>

## <a name="see-also"></a><span data-ttu-id="612ec-154">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="612ec-154">See Also</span></span>

[<span data-ttu-id="612ec-155">NuGet paketi hata ayıklama & semboller geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="612ec-155">NuGet Package Debugging & Symbols Improvements</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)
