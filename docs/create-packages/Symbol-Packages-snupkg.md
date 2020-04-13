---
title: NuGet sembol paketleri yeni sembol paketi formatı '.snupkg' kullanarak nasıl yayımlanır? Microsoft Dokümanlar
author: cristinamanu
ms.author: cristinamanu
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: NuGet sembol paketleri (snupkg) nasıl oluşturulur?
keywords: NuGet sembol paketleri, NuGet paketi hata ayıklama, NuGet hata ayıklama destekleyen, paket sembolleri, sembol paketi kuralları
ms.reviewer:
- anangaur
- karann
ms.openlocfilehash: c42032f1869f4be0af44ffa8fbd5ad522f73c459
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "80380424"
---
# <a name="creating-symbol-packages-snupkg"></a><span data-ttu-id="180a6-104">Sembol paketleri oluşturma (.snupkg)</span><span class="sxs-lookup"><span data-stu-id="180a6-104">Creating symbol packages (.snupkg)</span></span>

<span data-ttu-id="180a6-105">İyi bir hata ayıklama deneyimi, derlenen ve kaynak kod arasındaki ilişki, yerel değişkenlerin adları, yığın izleri ve daha fazlası gibi kritik bilgileri sağladığından hata ayıklama sembollerinin varlığına dayanır.</span><span class="sxs-lookup"><span data-stu-id="180a6-105">A good debugging experience relies on the presence of debug symbols as they provide critical information like the association between the compiled and the source code, names of local variables, stack traces, and more.</span></span> <span data-ttu-id="180a6-106">Bu sembolleri dağıtmak ve NuGet paketlerinizin hata ayıklama deneyimini geliştirmek için sembol paketlerini (.snupkg) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="180a6-106">You can use symbol packages (.snupkg) to distribute these symbols and improve the debugging experience of your NuGet packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="180a6-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="180a6-107">Prerequisites</span></span>

<span data-ttu-id="180a6-108">[nuget.exe v4.9.0 veya üzeri](https://www.nuget.org/downloads) veya [dotnet CLI v2.2.0 veya üzeri,](https://www.microsoft.com/net/download/dotnet-core/2.2)gerekli [NuGet protokollerini](../api/nuget-protocols.md)uygulamak .</span><span class="sxs-lookup"><span data-stu-id="180a6-108">[nuget.exe v4.9.0 or above](https://www.nuget.org/downloads) or [dotnet CLI v2.2.0 or above](https://www.microsoft.com/net/download/dotnet-core/2.2), which implement the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

## <a name="creating-a-symbol-package"></a><span data-ttu-id="180a6-109">Sembol paketi oluşturma</span><span class="sxs-lookup"><span data-stu-id="180a6-109">Creating a symbol package</span></span>

<span data-ttu-id="180a6-110">Dotnet CLI veya MSBuild kullanıyorsanız, .nupkg dosyasına ek olarak bir .snupkg dosyası oluşturmak için özellikleri `IncludeSymbols` ve `SymbolPackageFormat` özelliklerini ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="180a6-110">If you're using dotnet CLI or MSBuild, you need to set the `IncludeSymbols` and `SymbolPackageFormat` properties to create a .snupkg file in addition to the .nupkg file.</span></span>

* <span data-ttu-id="180a6-111">.csproj dosyanıza aşağıdaki özellikleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="180a6-111">Either add the following properties to your .csproj file:</span></span>

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
   </PropertyGroup>
   ```

* <span data-ttu-id="180a6-112">Veya komut satırında bu özellikleri belirtin:</span><span class="sxs-lookup"><span data-stu-id="180a6-112">Or specify these properties on the command-line:</span></span>

     ```dotnetcli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  <span data-ttu-id="180a6-113">or</span><span class="sxs-lookup"><span data-stu-id="180a6-113">or</span></span>

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

<span data-ttu-id="180a6-114">NuGet.exe kullanıyorsanız, .nupkg dosyasına ek olarak bir .snupkg dosyası oluşturmak için aşağıdaki komutları kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="180a6-114">If you're using NuGet.exe, you can use the following commands to create a .snupkg file in addition to the .nupkg file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

<span data-ttu-id="180a6-115">Özellik [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) iki değerden birine `symbols.nupkg` sahip olabilir: `snupkg`(varsayılan) veya .</span><span class="sxs-lookup"><span data-stu-id="180a6-115">The [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) property can have one of two values: `symbols.nupkg` (the default) or `snupkg`.</span></span> <span data-ttu-id="180a6-116">Bu özellik belirtilmemişse, eski bir simge paketi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="180a6-116">If this property is not specified, a legacy symbol package will be created.</span></span>

> [!Note]
> <span data-ttu-id="180a6-117">Eski biçim `.symbols.nupkg` hala ancak uyumluluk nedenleriyle desteklenir (bkz. [Eski Simge Paketleri).](Symbol-Packages.md)</span><span class="sxs-lookup"><span data-stu-id="180a6-117">The legacy format `.symbols.nupkg` is still supported but only for compatibility reasons (see [Legacy Symbol Packages](Symbol-Packages.md)).</span></span> <span data-ttu-id="180a6-118">NuGet.org sembol sunucusu sadece yeni sembol paketi `.snupkg`biçimini kabul eder - .</span><span class="sxs-lookup"><span data-stu-id="180a6-118">NuGet.org's symbol server only accepts the new symbol package format - `.snupkg`.</span></span>

## <a name="publishing-a-symbol-package"></a><span data-ttu-id="180a6-119">Sembol paketi yayımlama</span><span class="sxs-lookup"><span data-stu-id="180a6-119">Publishing a symbol package</span></span>

1. <span data-ttu-id="180a6-120">Kolaylık sağlamak için önce API anahtarınızı NuGet ile kaydedin (bkz. [bir paket yayımla).](../nuget-org/publish-a-package.md)</span><span class="sxs-lookup"><span data-stu-id="180a6-120">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md)).</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. <span data-ttu-id="180a6-121">Birincil paketinizi nuget.org yayımladıktan sonra, sembol paketini aşağıdaki gibi itin.</span><span class="sxs-lookup"><span data-stu-id="180a6-121">After publishing your primary package to nuget.org, push the symbol package as follows.</span></span>

    ```cli
    nuget push MyPackage.snupkg
    ```

1. <span data-ttu-id="180a6-122">Ayrıca, aşağıdaki komutu kullanarak hem birincil hem de sembol paketlerini aynı anda itebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="180a6-122">You can also push both primary and symbol packages at the same time using the below command.</span></span> <span data-ttu-id="180a6-123">Hem .nupkg hem de .snupkg dosyalarının geçerli klasörde bulunması gerekir.</span><span class="sxs-lookup"><span data-stu-id="180a6-123">Both .nupkg and .snupkg files need to be present in the current folder.</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

<span data-ttu-id="180a6-124">NuGet her iki paketi de nuget.org yayınlayacaktır. `MyPackage.nupkg` önce yayınlanacak, ardından `MyPackage.snupkg`.</span><span class="sxs-lookup"><span data-stu-id="180a6-124">NuGet will publish both packages to nuget.org. `MyPackage.nupkg` will be published first, followed by `MyPackage.snupkg`.</span></span>

> [!Note]
> <span data-ttu-id="180a6-125">Sembol paketi yayımlanmıyorsa, NuGet.org kaynağı 'olarak `https://api.nuget.org/v3/index.json`yapılandırdığınızdan denetlemeyin.</span><span class="sxs-lookup"><span data-stu-id="180a6-125">If the symbol package isn't published, check that you've configured the NuGet.org source as `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="180a6-126">Sembol paket yayımlama yalnızca [NuGet V3 API](../api/overview.md#versioning)tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="180a6-126">Symbol package publishing is only supported by [the NuGet V3 API](../api/overview.md#versioning).</span></span>

## <a name="nugetorg-symbol-server"></a><span data-ttu-id="180a6-127">NuGet.org sembol sunucusu</span><span class="sxs-lookup"><span data-stu-id="180a6-127">NuGet.org symbol server</span></span>

<span data-ttu-id="180a6-128">NuGet.org kendi sembolleri sunucu deposu destekler ve sadece yeni sembol `.snupkg`paketi biçimini kabul eder - .</span><span class="sxs-lookup"><span data-stu-id="180a6-128">NuGet.org supports its own symbols server repository and only accepts the new symbol package format - `.snupkg`.</span></span> <span data-ttu-id="180a6-129">Paket tüketicileri, Visual Studio'daki sembol `https://symbols.nuget.org/download/symbols` kaynaklarına ekleyerek sembol sunucuyu nuget.org için yayınlanan sembolleri kullanabilirler, bu da Visual Studio hata ayıklayıcısında paket koduna adım atmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="180a6-129">Package consumers can use the symbols published to nuget.org symbol server by adding `https://symbols.nuget.org/download/symbols` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="180a6-130">Bkz. Bu işlemle ilgili ayrıntılar için [Visual Studio hata ayıklamasında ki simge (.pdb) ve kaynak dosyaları belirtin.](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger)</span><span class="sxs-lookup"><span data-stu-id="180a6-130">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

### <a name="nugetorg-symbol-package-constraints"></a><span data-ttu-id="180a6-131">NuGet.org sembolü paket kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="180a6-131">NuGet.org symbol package constraints</span></span>

<span data-ttu-id="180a6-132">NuGet.org sembol paketleri için aşağıdaki kısıtlamalara sahiptir:</span><span class="sxs-lookup"><span data-stu-id="180a6-132">NuGet.org has the following constraints for symbol packages:</span></span>

- <span data-ttu-id="180a6-133">Yalnızca aşağıdaki dosya uzantılarına sembol paketlerinde `.nuspec` `.xml`izin `.psmdcp` `.rels`verilir: `.pdb`, , , ,`.p7s`</span><span class="sxs-lookup"><span data-stu-id="180a6-133">Only the following file extensions are allowed in symbol packages: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`</span></span>
- <span data-ttu-id="180a6-134">NuGet.org'un sembol sunucusunda yalnızca yönetilen [Taşınabilir PDF'ler](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) desteklenir.</span><span class="sxs-lookup"><span data-stu-id="180a6-134">Only managed [Portable PDBs](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) are supported on NuGet.org's symbol server.</span></span>
- <span data-ttu-id="180a6-135">PDB'ler ve bunların ilişkili .nupkg DL'leri Visual Studio sürüm 15.9 veya üzeri derleyici ile oluşturulmalıdır (bkz. [PDB kripto karma)](https://github.com/dotnet/roslyn/issues/24429)</span><span class="sxs-lookup"><span data-stu-id="180a6-135">The PDBs and their associated .nupkg DLLs need to be built with the compiler in Visual Studio version 15.9 or above (see [PDB crypto hash](https://github.com/dotnet/roslyn/issues/24429))</span></span>

<span data-ttu-id="180a6-136">bu kısıtlamalar karşılanmazsa, NuGet.org için yayınlanan sembol paketleri doğrulamada başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="180a6-136">Symbol packages published to NuGet.org will fail validation if these constraints aren't met.</span></span> 

### <a name="symbol-package-validation-and-indexing"></a><span data-ttu-id="180a6-137">Sembol paketi doğrulama ve dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="180a6-137">Symbol package validation and indexing</span></span>

<span data-ttu-id="180a6-138">[NuGet.org](https://www.nuget.org/) için yayınlanan sembol paketleri, kötü amaçlı yazılım taraması da dahil olmak üzere çeşitli doğrulamalara tabi dir.</span><span class="sxs-lookup"><span data-stu-id="180a6-138">Symbol packages published to [NuGet.org](https://www.nuget.org/) undergo several validations, including malware scanning.</span></span> <span data-ttu-id="180a6-139">Bir paket doğrulama denetiminde başarısız olursa, paket ayrıntıları sayfası bir hata iletisi görüntüler.</span><span class="sxs-lookup"><span data-stu-id="180a6-139">If a package fails a validation check, its package details page will display an error message.</span></span> <span data-ttu-id="180a6-140">Buna ek olarak, paketin sahipleri tanımlanan sorunları nasıl düzelteceklerine ilişkin talimatları içeren bir e-posta alır.</span><span class="sxs-lookup"><span data-stu-id="180a6-140">In addition, the package's owners will receive an email with instructions on how to fix the identified issues.</span></span>

<span data-ttu-id="180a6-141">Sembol paketi tüm doğrulamaları geçtiğinde, semboller NuGet.org'un sembol sunucuları tarafından dizine eklenir ve tüketime sunulacaktır.</span><span class="sxs-lookup"><span data-stu-id="180a6-141">When the symbol package has passed all validations, the symbols will be indexed by NuGet.org's symbol servers and will be available for consumption.</span></span>

<span data-ttu-id="180a6-142">Paket doğrulama ve dizin oluşturma genellikle 15 dakikanın altında sürer.</span><span class="sxs-lookup"><span data-stu-id="180a6-142">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="180a6-143">Paket yayımlama beklenenden uzun sürüyorsa, NuGet.org herhangi bir kesinti yaşanıp yaşanmayacağını kontrol etmek için [status.nuget.org](https://status.nuget.org/) ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="180a6-143">If the package publishing takes longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if NuGet.org is experiencing any interruptions.</span></span> <span data-ttu-id="180a6-144">Tüm sistemler çalışır durumdaysa ve paket bir saat içinde başarıyla yayınlanmamışsa, lütfen nuget.org giriş yapın ve paket detayları sayfasındaki İletişim Destek bağlantısını kullanarak bizimle iletişime geçin.</span><span class="sxs-lookup"><span data-stu-id="180a6-144">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package details page.</span></span>

## <a name="symbol-package-structure"></a><span data-ttu-id="180a6-145">Sembol paket yapısı</span><span class="sxs-lookup"><span data-stu-id="180a6-145">Symbol package structure</span></span>

<span data-ttu-id="180a6-146">Sembol paketi (.snupkg) aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="180a6-146">The symbol package (.snupkg) has the following characteristics:</span></span>

1) <span data-ttu-id="180a6-147">.snupkg, karşılık gelen NuGet paketi (.nupkg) ile aynı id ve sürüme sahiptir.</span><span class="sxs-lookup"><span data-stu-id="180a6-147">The .snupkg has the same id and version as its corresponding NuGet package (.nupkg).</span></span>
2) <span data-ttu-id="180a6-148">.snupkg, DLs/EXE yerine, ilgili PDB'lerinin aynı klasör hiyerarşisine dahil olacağı ayrımına sahip herhangi bir DLL veya EXE dosyası için karşılık gelen .nupkg ile aynı klasör yapısına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="180a6-148">The .snupkg has the same folder structure as its corresponding .nupkg for any DLL or EXE files with the distinction that instead of DLLs/EXEs, their corresponding PDBs will be included in the same folder hierarchy.</span></span> <span data-ttu-id="180a6-149">PDB dışındaki uzantılı dosya ve klasörler snupkg dışında bırakılır.</span><span class="sxs-lookup"><span data-stu-id="180a6-149">Files and folders with extensions other than PDB will be left out of the snupkg.</span></span>
3) <span data-ttu-id="180a6-150">Sembol paketinin .nuspec dosyasında `SymbolsPackage` paket türü vardır:</span><span class="sxs-lookup"><span data-stu-id="180a6-150">The symbol package's .nuspec file has the `SymbolsPackage` package type:</span></span>

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) <span data-ttu-id="180a6-151">Bir yazar nupkg ve snupkg oluşturmak için özel bir nuspec kullanmaya karar verirse, snupkg aynı klasör hiyerarşisi ve dosyaları 2 ayrıntılı olmalıdır).</span><span class="sxs-lookup"><span data-stu-id="180a6-151">If an author decides to use a custom nuspec to build their nupkg and snupkg, the snupkg should have the same folder hierarchy and files detailed in 2).</span></span>
5) <span data-ttu-id="180a6-152">Aşağıdaki alanlar snupkg'ın nuspec dışında tutulur: ```authors``` ```owners```, ```requireLicenseAcceptance``` ```license type```, ```licenseUrl```, ```icon```, ve .</span><span class="sxs-lookup"><span data-stu-id="180a6-152">The following fields will be excluded from the snupkg's nuspec: ```authors```, ```owners```, ```requireLicenseAcceptance```, ```license type```, ```licenseUrl```, and  ```icon```.</span></span>
6) <span data-ttu-id="180a6-153">Öğeyi kullanmayın. ```<license>```</span><span class="sxs-lookup"><span data-stu-id="180a6-153">Do not use the ```<license>``` element.</span></span> <span data-ttu-id="180a6-154">Bir .snupkg ilgili .nupkg ile aynı lisans altında dır.</span><span class="sxs-lookup"><span data-stu-id="180a6-154">A .snupkg is covered under the same license as the corresponding .nupkg.</span></span>

## <a name="see-also"></a><span data-ttu-id="180a6-155">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="180a6-155">See also</span></span>

<span data-ttu-id="180a6-156">.NET derlemelerinin kaynak kodunun hata ayıklanmasını etkinleştirmek için Kaynak Bağlantısını kullanmayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="180a6-156">Consider using Source Link to enable source code debugging of .NET assemblies.</span></span> <span data-ttu-id="180a6-157">Daha fazla bilgi için lütfen [Kaynak Bağlantı kılavuzuna](/dotnet/standard/library-guidance/sourcelink)bakın.</span><span class="sxs-lookup"><span data-stu-id="180a6-157">For more information, please refer to the [Source Link guidance](/dotnet/standard/library-guidance/sourcelink).</span></span>

<span data-ttu-id="180a6-158">Sembol paketleri hakkında daha fazla bilgi için lütfen [NuGet Paketi Hata Ayıklama & Semboller Geliştirmeleri](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) tasarım özelliklerine bakın.</span><span class="sxs-lookup"><span data-stu-id="180a6-158">For more information on symbol packages, please refer to the [NuGet Package Debugging & Symbols Improvements](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) design spec.</span></span>
