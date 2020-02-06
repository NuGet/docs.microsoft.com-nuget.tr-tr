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
ms.openlocfilehash: 839c38ec165372bab9b93dec25e5c8e8e9439bfa
ms.sourcegitcommit: 415c70d7014545c1f65271a2debf8c3c1c5eb688
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/06/2020
ms.locfileid: "77036896"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="c6161-104">Sembol paketleri (. snupkg) oluşturuluyor</span><span class="sxs-lookup"><span data-stu-id="c6161-104">Creating symbol packages (.snupkg)</span></span>

<span data-ttu-id="c6161-105">İyi bir hata ayıklama deneyimi, derlenmiş ve kaynak kodu, yerel değişkenlerin adları, yığın izlemeleri ve daha fazlası arasındaki ilişki gibi kritik bilgiler sağlayan hata ayıklama sembollerinin varlığını kullanır.</span><span class="sxs-lookup"><span data-stu-id="c6161-105">A good debugging experience relies on the presence of debug symbols as they provide critical information like the association between the compiled and the source code, names of local variables, stack traces, and more.</span></span> <span data-ttu-id="c6161-106">Sembol paketlerini (. snupkg), bu sembolleri dağıtmak ve NuGet paketlerinizin hata ayıklama deneyimini geliştirmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c6161-106">You can use symbol packages (.snupkg) to distribute these symbols and improve the debugging experience of your NuGet packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6161-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="c6161-107">Prerequisites</span></span>

<span data-ttu-id="c6161-108">gerekli [NuGet protokollerini](../api/nuget-protocols.md)uygulayan [NuGet. exe v 4.9.0 veya üzeri](https://www.nuget.org/downloads) ya da [DotNet CLI v 2.2.0 veya üzeri](https://www.microsoft.com/net/download/dotnet-core/2.2).</span><span class="sxs-lookup"><span data-stu-id="c6161-108">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet CLI v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="c6161-109">Sembol paketi oluşturma</span><span class="sxs-lookup"><span data-stu-id="c6161-109">Creating a symbol package</span></span>

<span data-ttu-id="c6161-110">DotNet CLı veya MSBuild kullanıyorsanız,. nupkg dosyasına ek olarak, `IncludeSymbols` ve `SymbolPackageFormat` özelliklerini bir. snupkg dosyası oluşturacak şekilde ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c6161-110">If you're using dotnet CLI or MSBuild, you need to set the `IncludeSymbols` and `SymbolPackageFormat` properties to create a .snupkg file in addition to the .nupkg file.</span></span>

* <span data-ttu-id="c6161-111">Aşağıdaki özellikleri. csproj dosyanıza ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c6161-111">Either add the following properties to your .csproj file:</span></span>

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
   </PropertyGroup>
   ```

* <span data-ttu-id="c6161-112">Veya komut satırında aşağıdaki özellikleri belirtin:</span><span class="sxs-lookup"><span data-stu-id="c6161-112">Or specify these properties on the command-line:</span></span>

     ```dotnetcli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  <span data-ttu-id="c6161-113">or</span><span class="sxs-lookup"><span data-stu-id="c6161-113">or</span></span>

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

<span data-ttu-id="c6161-114">NuGet. exe kullanıyorsanız,. nupkg dosyasına ek olarak bir. snupkg dosyası oluşturmak için aşağıdaki komutları kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c6161-114">If you're using NuGet.exe, you can use the following commands to create a .snupkg file in addition to the .nupkg file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

<span data-ttu-id="c6161-115">[`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) özelliği iki değerden birine sahip olabilir: `symbols.nupkg` (varsayılan) veya `snupkg`.</span><span class="sxs-lookup"><span data-stu-id="c6161-115">The [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) property can have one of two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="c6161-116">Bu özellik belirtilmezse, eski bir sembol paketi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c6161-116">If this property is not specified, a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="c6161-117">Eski biçim `.symbols.nupkg` hala destekleniyor ancak yalnızca uyumluluk nedenleriyle desteklenir (bkz. [eski sembol paketleri](Symbol-Packages.md)).</span><span class="sxs-lookup"><span data-stu-id="c6161-117">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="c6161-118">NuGet. org 'ın sembol sunucusu yalnızca `.snupkg`yeni sembol paketi biçimini kabul eder.</span><span class="sxs-lookup"><span data-stu-id="c6161-118">NuGet.org's symbol server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="c6161-119">Sembol paketi yayımlama</span><span class="sxs-lookup"><span data-stu-id="c6161-119">Publishing a symbol package</span></span>

1. <span data-ttu-id="c6161-120">Kolaylık olması için önce API anahtarınızı NuGet ile kaydedin (bkz. [bir paket yayımlama](../nuget-org/publish-a-package.md)).</span><span class="sxs-lookup"><span data-stu-id="c6161-120">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="c6161-121">Birincil paketinizi nuget.org 'e yayımladıktan sonra, sembol paketini aşağıdaki gibi gönderin.</span><span class="sxs-lookup"><span data-stu-id="c6161-121">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="c6161-122">Ayrıca, aşağıdaki komutu kullanarak hem birincil hem de sembol paketlerini aynı anda gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c6161-122">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="c6161-123">. Nupkg ve. snupkg dosyalarının her ikisi de geçerli klasörde bulunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c6161-123">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="c6161-124">NuGet, her iki paketi de nuget.org 'e yayımlar. `MyPackage.nupkg` önce yayımlanacak, ardından `MyPackage.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="c6161-124">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

> [!Note]
> <span data-ttu-id="c6161-125">Sembol paketi yayınlanmamışsa, NuGet.org kaynağını `https://api.nuget.org/v3/index.json`olarak yapılandırdığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="c6161-125">If the symbol package isn't published, check that you've configured the NuGet.org source as `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="c6161-126">Sembol paketi yayımlaması yalnızca [NuGet v3 API 'si](../api/overview.md#versioning)tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="c6161-126">Symbol package publishing is only supported by [the NuGet V3 API](../api/overview.md#versioning).</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="c6161-127">NuGet.org symbol sunucusu</span><span class="sxs-lookup"><span data-stu-id="c6161-127">NuGet.org symbol server</span></span>

<span data-ttu-id="c6161-128">NuGet.org kendi sembolleri sunucu deposunu destekler ve yalnızca yeni sembol paketi biçimini kabul eder `.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="c6161-128">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="c6161-129">Paket tüketicileri, Visual Studio hata ayıklayıcısında paket koduna Adımlama sağlayan Visual Studio 'daki sembol kaynaklarına `https://symbols.nuget.org/download/symbols` ekleyerek nuget.org sembol sunucusunda yayınlanan sembolleri kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="c6161-129">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="c6161-130">Bu işlemle ilgili ayrıntılar için bkz. [Visual Studio hata ayıklayıcısında simge (. pdb) ve kaynak dosyaları belirtme](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) .</span><span class="sxs-lookup"><span data-stu-id="c6161-130">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="c6161-131">NuGet.org sembol paketi kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="c6161-131">NuGet.org symbol package constraints</span></span>

<span data-ttu-id="c6161-132">NuGet.org, sembol paketleri için aşağıdaki kısıtlamalara sahiptir:</span><span class="sxs-lookup"><span data-stu-id="c6161-132">NuGet.org has the following constraints for symbol packages:</span></span>

- <span data-ttu-id="c6161-133">Sembol paketlerinde yalnızca şu dosya uzantılarına izin veriliyor: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`</span><span class="sxs-lookup"><span data-stu-id="c6161-133">Only the following file extensions are allowed in symbol packages: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`</span></span>
- <span data-ttu-id="c6161-134">NuGet. org 'ın sembol sunucusunda yalnızca yönetilen [Taşınabilir pdb 'leri](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) desteklenir.</span><span class="sxs-lookup"><span data-stu-id="c6161-134">Only managed [Portable PDBs](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are supported on NuGet.org's symbol server.</span></span>
- <span data-ttu-id="c6161-135">Pdb 'leri ve ilişkili. nupkg dll 'Lerinin Visual Studio sürüm 15,9 veya üzeri bir derleyici ile oluşturulması gerekir (bkz. [pdb şifre karması](https://github.com/dotnet/roslyn/issues/24429))</span><span class="sxs-lookup"><span data-stu-id="c6161-135">The PDBs and their associated .nupkg DLLs need to be built with the compiler in Visual Studio version 15.9 or above (see [PDB crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="c6161-136">NuGet.org 'e yayınlanan sembol paketleri, bu kısıtlamalar karşılanmazsa doğrulama başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="c6161-136">Symbol packages published to NuGet.org will fail validation if these constraints aren't met.</span></span> 

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="c6161-137">Sembol paketi doğrulama ve dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="c6161-137">Symbol package validation and indexing</span></span>

<span data-ttu-id="c6161-138">[NuGet.org](https://www.nuget.org/) ' de yayınlanan sembol paketleri kötü amaçlı yazılım tarama dahil olmak üzere çeşitli doğrulamalar sağlar.</span><span class="sxs-lookup"><span data-stu-id="c6161-138">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, including malware scanning.</span></span> <span data-ttu-id="c6161-139">Bir paket doğrulama denetiminden başarısız olursa, paket ayrıntıları sayfasında bir hata mesajı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="c6161-139">If a package fails a validation check, its package details page will display an error message.</span></span> <span data-ttu-id="c6161-140">Ayrıca, paketin sahipleri, tanımlanan sorunları nasıl gidereceğiniz hakkında yönergeler içeren bir e-posta alır.</span><span class="sxs-lookup"><span data-stu-id="c6161-140">In addition, the package's owners will receive an email with instructions on how to fix the identified issues.</span></span>

<span data-ttu-id="c6161-141">Sembol paketi tüm doğrulamaları geçtiğinde, semboller NuGet. org 'ın sembol sunucuları tarafından dizine alınır ve tüketim için kullanılabilir olacaktır.</span><span class="sxs-lookup"><span data-stu-id="c6161-141">When the symbol package has passed all validations, the symbols will be indexed by NuGet.org's symbol servers and will be available for consumption.</span></span>

<span data-ttu-id="c6161-142">Paket doğrulama ve dizin oluşturma genellikle 15 dakika boyunca sürer.</span><span class="sxs-lookup"><span data-stu-id="c6161-142">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="c6161-143">Paket yayımlaması beklenenden uzun sürerse, NuGet.org 'in herhangi bir kesinti yaşamadığını denetlemek için [Status.NuGet.org](https://status.nuget.org/) adresini ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="c6161-143">If the package publishing takes longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if NuGet.org is experiencing any interruptions.</span></span> <span data-ttu-id="c6161-144">Tüm sistemler çalışır durumda ve paket bir saat içinde başarıyla yayımlanmamışsa, lütfen nuget.org ' e oturum açın ve paket ayrıntıları sayfasında desteğe başvurun bağlantısını kullanarak bizimle iletişime geçin.</span><span class="sxs-lookup"><span data-stu-id="c6161-144">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="c6161-145">Sembol paketi yapısı</span><span class="sxs-lookup"><span data-stu-id="c6161-145">Symbol package structure</span></span>

<span data-ttu-id="c6161-146">Sembol paketi (. snupkg) aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="c6161-146">The symbol package (.snupkg) has the following characteristics:</span></span>

1) <span data-ttu-id="c6161-147">. Snupkg, karşılık gelen NuGet paketiyle (. nupkg) aynı kimliğe ve sürüme sahiptir.</span><span class="sxs-lookup"><span data-stu-id="c6161-147">The .snupkg has the same id and version as its corresponding NuGet package (.nupkg).</span></span>
2) <span data-ttu-id="c6161-148">. Snupkg, dll 'Ler veya EXE dosyaları için karşılık gelen. nupkg ile aynı klasör yapısına sahiptir; bu, bunlara karşılık gelen pdb 'leri, aynı klasör hiyerarşisine dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="c6161-148">The .snupkg has the same folder structure as its corresponding .nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="c6161-149">PDB 'den farklı uzantılara sahip dosyalar ve klasörler, snupkg 'dan bırakılır.</span><span class="sxs-lookup"><span data-stu-id="c6161-149">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="c6161-150">Sembol paketinin. nuspec dosyasında `SymbolsPackage` paket türü vardır:</span><span class="sxs-lookup"><span data-stu-id="c6161-150">The symbol package's .nuspec file has the `SymbolsPackage` package type:</span></span>

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) <span data-ttu-id="c6161-151">Bir yazar, nupkg ve snupkg 'leri oluşturmak için özel bir nuspec kullanılmasına karar verirse, snupkg, aynı klasör hiyerarşisine ve 2 ' de ayrıntılı dosyalar içermelidir.</span><span class="sxs-lookup"><span data-stu-id="c6161-151">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="c6161-152">Aşağıdaki alanlar, snupkg 'dan nuspec: ```authors```, ```owners```, ```requireLicenseAcceptance```, ```license type```, ```licenseUrl```ve ```icon```dışarıda bırakılır.</span><span class="sxs-lookup"><span data-stu-id="c6161-152">The following fields will be excluded from the snupkg's nuspec: ```authors```, ```owners```, ```requireLicenseAcceptance```, ```license type```, ```licenseUrl```, and  ```icon```.</span></span>
6) <span data-ttu-id="c6161-153">```<license>``` öğesini kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="c6161-153">Do not use the ```<license>``` element.</span></span> <span data-ttu-id="c6161-154">A. snupkg, karşılık gelen. nupkg ile aynı lisans kapsamında ele alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="c6161-154">A .snupkg is covered under the same license as the corresponding .nupkg.</span></span>

## <a name="see-also"></a><span data-ttu-id="c6161-155">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="c6161-155">See also</span></span>

<span data-ttu-id="c6161-156">.NET derlemelerinin kaynak kodu hata ayıklamasını etkinleştirmek için kaynak bağlantısı kullanmayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="c6161-156">Consider using Source Link to enable source code debugging of .NET assemblies.</span></span> <span data-ttu-id="c6161-157">Daha fazla bilgi için lütfen [kaynak bağlantı kılavuzuna](/dotnet/standard/library-guidance/sourcelink)bakın.</span><span class="sxs-lookup"><span data-stu-id="c6161-157">For more information, please refer to the [Source Link guidance](/dotnet/standard/library-guidance/sourcelink).</span></span>

<span data-ttu-id="c6161-158">Sembol paketleri hakkında daha fazla bilgi için lütfen [NuGet paketi hata ayıklama & sembol geliştirmeleri](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) tasarım belirtimine bakın.</span><span class="sxs-lookup"><span data-stu-id="c6161-158">For more information on symbol packages, please refer to the [NuGet Package Debugging & Symbols Improvements](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) design spec.</span></span>
