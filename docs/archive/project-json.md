---
title: NuGet için Project.JSON dosyası başvurusu
description: Bazı proje türlerinde project.json projede kullanılan NuGet paketleri listesini tutar.
author: karann-msft
ms.author: karann
ms.date: 07/27/2017
ms.topic: reference
ms.openlocfilehash: e4d8b5b9ab4605516827ead8939f278d110c7a48
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547790"
---
# <a name="projectjson-reference"></a><span data-ttu-id="50bbb-103">Project.JSON başvurusu</span><span class="sxs-lookup"><span data-stu-id="50bbb-103">project.json reference</span></span>

<span data-ttu-id="50bbb-104">*NuGet 3.x+*</span><span class="sxs-lookup"><span data-stu-id="50bbb-104">*NuGet 3.x+*</span></span>

<span data-ttu-id="50bbb-105">`project.json` Dosyası bir paket Yönetimi biçimi olarak bilinen, bir projede kullanılan paketler listesini tutar.</span><span class="sxs-lookup"><span data-stu-id="50bbb-105">The `project.json` file maintains a list of packages used in a project, known as a package management format.</span></span> <span data-ttu-id="50bbb-106">Sürümlereni `packages.config` sırayla yerine geçen ancak [PackageReference](../consume-packages/package-references-in-project-files.md) NuGet 4.0 + ile.</span><span class="sxs-lookup"><span data-stu-id="50bbb-106">It supersedes `packages.config` but is in turn superseded by [PackageReference](../consume-packages/package-references-in-project-files.md) with NuGet 4.0+.</span></span>

<span data-ttu-id="50bbb-107">[ `project.lock.json` ](#projectlockjson) (Aşağıda açıklanmıştır) dosyası da kullanan projelerinde kullanılan `project.json`.</span><span class="sxs-lookup"><span data-stu-id="50bbb-107">The [`project.lock.json`](#projectlockjson) file (described below) is also used in projects employing `project.json`.</span></span>

<span data-ttu-id="50bbb-108">`project.json` aşağıdaki temel yapısını dört üst düzey nesnelerin her biri herhangi bir sayıda alt nesneler burada sahip sahiptir:</span><span class="sxs-lookup"><span data-stu-id="50bbb-108">`project.json` has the following basic structure, where each of the four top-level objects can have any number of child objects:</span></span>

```json
{
    "dependencies": {
        "PackageID" : "{version_constraint}"
    },
    "frameworks" : {
        "TxM" : {}
    },
    "runtimes" : {
        "RID": {}
    },
    "supports" : {
        "CompatibilityProfile" : {}
    }
}
```

## <a name="dependencies"></a><span data-ttu-id="50bbb-109">Bağımlılıkları</span><span class="sxs-lookup"><span data-stu-id="50bbb-109">Dependencies</span></span>

<span data-ttu-id="50bbb-110">NuGet Paket bağımlılıklarını projenizin aşağıdaki biçimde listeler:</span><span class="sxs-lookup"><span data-stu-id="50bbb-110">Lists the NuGet package dependencies of your project in the following form:</span></span>

```json
"PackageID" : "version_constraint"
```

<span data-ttu-id="50bbb-111">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="50bbb-111">For example:</span></span>

```json
"dependencies": {
    "Microsoft.NETCore": "5.0.0",
    "System.Runtime.Serialization.Primitives": "4.0.10"
}
```

<span data-ttu-id="50bbb-112">`dependencies` Bölümdür burada NuGet Paket Yöneticisi iletişim paket bağımlılıkları projenize ekler.</span><span class="sxs-lookup"><span data-stu-id="50bbb-112">The `dependencies` section is where the NuGet Package Manager dialog adds package dependencies to your project.</span></span>

<span data-ttu-id="50bbb-113">Nuget.org, Paket Yöneticisi Konsolu'nda kullanılan kimliği ile aynı paket kimliği için paket kimliği karşılık gelir: `Install-Package Microsoft.NETCore`.</span><span class="sxs-lookup"><span data-stu-id="50bbb-113">The Package id corresponds to the id of the package on nuget.org , the same as the id used in the package manager console: `Install-Package Microsoft.NETCore`.</span></span>

<span data-ttu-id="50bbb-114">Ne zaman geri yükleme paketleri sürüm kısıtlamasını `"5.0.0"` gelir `>= 5.0.0`.</span><span class="sxs-lookup"><span data-stu-id="50bbb-114">When restoring packages, the version constraint of `"5.0.0"` implies `>= 5.0.0`.</span></span> <span data-ttu-id="50bbb-115">Diğer bir deyişle, sunucuda 5.0.0 kullanılamıyor, ancak 5.0.1 olduğundan, NuGet 5.0.1 yükler ve yükseltme hakkında sizi uyarır.</span><span class="sxs-lookup"><span data-stu-id="50bbb-115">That is, if 5.0.0 is not available on the server but 5.0.1 is, NuGet installs  5.0.1 and warns you about the upgrade.</span></span> <span data-ttu-id="50bbb-116">NuGet, aksi takdirde olası en düşük sürüm kısıtlaması eşleşen sunucuda seçer.</span><span class="sxs-lookup"><span data-stu-id="50bbb-116">NuGet otherwise picks the lowest possible version on the server matching the constraint.</span></span>

<span data-ttu-id="50bbb-117">Bkz: [bağımlılık çözümlemesi](../consume-packages/dependency-resolution.md) çözümleme kuralları hakkında daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="50bbb-117">See [Dependency resolution](../consume-packages/dependency-resolution.md) for more details on resolution rules.</span></span>

### <a name="managing-dependency-assets"></a><span data-ttu-id="50bbb-118">Bağımlılık varlıklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="50bbb-118">Managing dependency assets</span></span>

<span data-ttu-id="50bbb-119">Hangi bağımlılıklar varlıklarından en üst düzey projeye akış etiketleri virgülle ayrılmış bir dizi belirterek denetlenir `include` ve `exclude` bağımlılık başvurusu özellikleri.</span><span class="sxs-lookup"><span data-stu-id="50bbb-119">Which assets from dependencies flow into the top-level project is controlled by specifying a comma-delimited set of tags in the `include` and `exclude` properties of the dependency reference.</span></span> <span data-ttu-id="50bbb-120">Etiketleri listelenen aşağıdaki tabloda:</span><span class="sxs-lookup"><span data-stu-id="50bbb-120">The tags are listed the table below:</span></span>

| <span data-ttu-id="50bbb-121">Etiket Ekle/Dışla</span><span class="sxs-lookup"><span data-stu-id="50bbb-121">Include/Exclude tag</span></span> | <span data-ttu-id="50bbb-122">Etkilenen hedef klasör</span><span class="sxs-lookup"><span data-stu-id="50bbb-122">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="50bbb-123">contentFiles</span><span class="sxs-lookup"><span data-stu-id="50bbb-123">contentFiles</span></span> | <span data-ttu-id="50bbb-124">İçerik</span><span class="sxs-lookup"><span data-stu-id="50bbb-124">Content</span></span>  |
| <span data-ttu-id="50bbb-125">çalışma zamanı</span><span class="sxs-lookup"><span data-stu-id="50bbb-125">runtime</span></span> | <span data-ttu-id="50bbb-126">Çalışma zamanı, kaynaklar ve FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="50bbb-126">Runtime, Resources, and FrameworkAssemblies</span></span>  |
| <span data-ttu-id="50bbb-127">Derleme</span><span class="sxs-lookup"><span data-stu-id="50bbb-127">compile</span></span> | <span data-ttu-id="50bbb-128">lib</span><span class="sxs-lookup"><span data-stu-id="50bbb-128">lib</span></span> |
| <span data-ttu-id="50bbb-129">derleme</span><span class="sxs-lookup"><span data-stu-id="50bbb-129">build</span></span> | <span data-ttu-id="50bbb-130">derleme (MSBuild özellikler ve hedefler)</span><span class="sxs-lookup"><span data-stu-id="50bbb-130">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="50bbb-131">yerel</span><span class="sxs-lookup"><span data-stu-id="50bbb-131">native</span></span> | <span data-ttu-id="50bbb-132">yerel</span><span class="sxs-lookup"><span data-stu-id="50bbb-132">native</span></span> |
| <span data-ttu-id="50bbb-133">yok</span><span class="sxs-lookup"><span data-stu-id="50bbb-133">none</span></span> | <span data-ttu-id="50bbb-134">Klasör yok</span><span class="sxs-lookup"><span data-stu-id="50bbb-134">No folders</span></span> |
| <span data-ttu-id="50bbb-135">tüm</span><span class="sxs-lookup"><span data-stu-id="50bbb-135">all</span></span> | <span data-ttu-id="50bbb-136">Tüm klasörler</span><span class="sxs-lookup"><span data-stu-id="50bbb-136">All folders</span></span> |

<span data-ttu-id="50bbb-137">İle belirtilen etiketlere `exclude` ile belirtilenler üzerinde önceliklidir `include`.</span><span class="sxs-lookup"><span data-stu-id="50bbb-137">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="50bbb-138">Örneğin, `include="runtime, compile" exclude="compile"` aynı `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="50bbb-138">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span>

<span data-ttu-id="50bbb-139">Örneğin, dahil etmek için `build` ve `native` klasörleri, bağımlılık aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="50bbb-139">For example, to include the `build` and `native` folders of a dependency, use the following:</span></span>

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "include": "build, native"
    }
  }
}
```

<span data-ttu-id="50bbb-140">Dışlanacak `content` ve `build` klasörleri, bağımlılık aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="50bbb-140">To exclude the `content` and `build` folders of a dependency, use the following:</span></span>

```json
{
  "dependencies": {
    "packageA": {
      "version": "1.0.0",
      "exclude": "contentFiles, build"
    }
  }
}
```

## <a name="frameworks"></a><span data-ttu-id="50bbb-141">Çerçeveler</span><span class="sxs-lookup"><span data-stu-id="50bbb-141">Frameworks</span></span>

<span data-ttu-id="50bbb-142">Listeler gibi proje üzerinde çalıştığı çerçeveleri `net45`, `netcoreapp`, `netstandard`.</span><span class="sxs-lookup"><span data-stu-id="50bbb-142">Lists the frameworks that the project runs on, such as `net45`, `netcoreapp`, `netstandard`.</span></span>

```json
"frameworks": {
    "netcore50": {}
    }
 ```

<span data-ttu-id="50bbb-143">Yalnızca tek bir giriş izin `frameworks` bölümü.</span><span class="sxs-lookup"><span data-stu-id="50bbb-143">Only a single entry is allowed in the `frameworks` section.</span></span> <span data-ttu-id="50bbb-144">(Bir özel durum `project.json` dosyaları derleme kullanım dışı DNX ile olan ASP.NET projeleri için araç için birden çok hedef sağlayan zinciri.)</span><span class="sxs-lookup"><span data-stu-id="50bbb-144">(An exception is `project.json` files for ASP.NET projects that are build with deprecated DNX tool chain, which allows for multiple targets.)</span></span>

## <a name="runtimes"></a><span data-ttu-id="50bbb-145">Çalışma zamanları</span><span class="sxs-lookup"><span data-stu-id="50bbb-145">Runtimes</span></span>

<span data-ttu-id="50bbb-146">Gibi uygulamanızın üzerinde çalıştığı işletim sistemleri ve mimariler listeler `win10-arm`, `win8-x64`, `win8-x86`.</span><span class="sxs-lookup"><span data-stu-id="50bbb-146">Lists the operating systems and architectures that your app runs on, such as `win10-arm`, `win8-x64`, `win8-x86`.</span></span>

```json
"runtimes": {
    "win10-arm": { },
    "win10-arm-aot": { },
    "win10-x86": { },
    "win10-x86-aot": { },
    "win10-x64": { },
    "win10-x64-aot": { }
}
```

<span data-ttu-id="50bbb-147">Herhangi bir çalışma zamanı üzerinde çalışabilen bir PCL içeren bir paket, bir çalışma zamanı belirtmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="50bbb-147">A package containing a PCL that can run on any runtime doesn't need to specify a runtime.</span></span> <span data-ttu-id="50bbb-148">Bu ayrıca herhangi bir bağımlılığın true olmalıdır, aksi takdirde, çalışma zamanları belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="50bbb-148">This must also be true of any dependencies, otherwise you must specify runtimes.</span></span>


## <a name="supports"></a><span data-ttu-id="50bbb-149">Destekler</span><span class="sxs-lookup"><span data-stu-id="50bbb-149">Supports</span></span>

<span data-ttu-id="50bbb-150">Paket bağımlılıkları için denetimleri kümesini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="50bbb-150">Defines a set of checks for package dependencies.</span></span> <span data-ttu-id="50bbb-151">Burada, PCL veya uygulamanın çalışmasını beklediğiniz tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50bbb-151">You can define where you expect the PCL or app to run.</span></span> <span data-ttu-id="50bbb-152">Tanımları kısıtlayıcı olmayan kod başka bir yerde çalıştırmak mümkün olabilir.</span><span class="sxs-lookup"><span data-stu-id="50bbb-152">The definitions are not restrictive, as your code may be able to run elsewhere.</span></span> <span data-ttu-id="50bbb-153">Ancak bu denetimleri belirten tüm bağımlılıklar üzerinde listelenen TxMs karşılanır denetleyin NuGet yapar.</span><span class="sxs-lookup"><span data-stu-id="50bbb-153">But specifying these checks makes NuGet check that all dependencies are satisfied on the listed TxMs.</span></span> <span data-ttu-id="50bbb-154">Örnek değerler için bu şunlardır: `net46.app`, `uwp.10.0.app`vb.</span><span class="sxs-lookup"><span data-stu-id="50bbb-154">Examples of the values for this are: `net46.app`, `uwp.10.0.app`, etc.</span></span>

<span data-ttu-id="50bbb-155">Bu bölümde, taşınabilir sınıf kitaplığı hedefleri iletişim kutusunda bir girişi seçtiğinizde otomatik olarak doldurulur.</span><span class="sxs-lookup"><span data-stu-id="50bbb-155">This section should be populated automatically when you select an entry in the Portable Class Library targets dialog.</span></span>

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a><span data-ttu-id="50bbb-156">İçeri aktarmalar</span><span class="sxs-lookup"><span data-stu-id="50bbb-156">Imports</span></span>

<span data-ttu-id="50bbb-157">İçeri aktarmalar kullanan paketleri izin verecek şekilde tasarlanmıştır `dotnet` TxM bir dotnet TxM bildirmeyin paketlerle çalışılacak.</span><span class="sxs-lookup"><span data-stu-id="50bbb-157">Imports are designed to allow packages that use the `dotnet` TxM to operate with packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="50bbb-158">Projenizi kullanıyorsa `dotnet` TxM sonra bağlı olduğu tüm paketleri ayrıca olmalıdır bir `dotnet` TxM, aşağıdaki eklemediğiniz sürece, `project.json` olmayan izin vermek için `dotnet` platformları ile uyumlu olacak şekilde `dotnet`:</span><span class="sxs-lookup"><span data-stu-id="50bbb-158">If your project is using the `dotnet` TxM then all the packages you depend on must also have a `dotnet` TxM, unless you add the following to your `project.json` to allow non `dotnet` platforms to be compatible with `dotnet`:</span></span>

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

<span data-ttu-id="50bbb-159">Kullanıyorsanız `dotnet` TxM ardından PCL proje sistemi ekler uygun `imports` tabanlı desteklenen hedeflerde bildirimi.</span><span class="sxs-lookup"><span data-stu-id="50bbb-159">If you are using the `dotnet` TxM then the PCL project system adds the appropriate `imports` statement based on the supported targets.</span></span>

## <a name="differences-from-portable-apps-and-web-projects"></a><span data-ttu-id="50bbb-160">Taşınabilir uygulamaları ve web projeleri arasındaki farklar</span><span class="sxs-lookup"><span data-stu-id="50bbb-160">Differences from portable apps and web projects</span></span>

<span data-ttu-id="50bbb-161">`project.json` NuGet tarafından kullanılan dosya, ASP.NET Core projelerinde bulunan özelliklerinin bir alt kümesidir.</span><span class="sxs-lookup"><span data-stu-id="50bbb-161">The `project.json` file used by NuGet is a subset of that found in ASP.NET Core projects.</span></span> <span data-ttu-id="50bbb-162">ASP.NET core'da `project.json` proje meta verileri, derleme bilgilerini ve bağımlılıklar için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="50bbb-162">In ASP.NET Core `project.json` is used for project metadata, compilation information, and dependencies.</span></span> <span data-ttu-id="50bbb-163">Diğer proje sistemleri kullanıldığında, bu üç şey ayrı dosyalar halinde bölme ve `project.json` daha az bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="50bbb-163">When used in other project systems, those three things are split into separate files and `project.json` contains less information.</span></span> <span data-ttu-id="50bbb-164">Önemli farklar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="50bbb-164">Notable differences include:</span></span>

- <span data-ttu-id="50bbb-165">Ayrıca bir framework yalnızca olabilir `frameworks` bölümü.</span><span class="sxs-lookup"><span data-stu-id="50bbb-165">There can only be one framework in the `frameworks` section.</span></span>

- <span data-ttu-id="50bbb-166">Dosya içeremez bağımlılıkları, derleme seçenekleri vb. DNX içinde gördüğünüz `project.json` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="50bbb-166">The file cannot contain dependencies, compilation options, etc. that you see in DNX `project.json` files.</span></span> <span data-ttu-id="50bbb-167">Yalnızca olabilir koşuluyla, tek bir çerçeve bu çerçeveye özgü bağımlılıkları girmek için anlam ifade etmez.</span><span class="sxs-lookup"><span data-stu-id="50bbb-167">Given that there can only be a single framework it doesn't make sense to enter framework-specific dependencies.</span></span>

- <span data-ttu-id="50bbb-168">Derleme tarafından işlenir derleme seçenekleri, önişlemci tanımlar için MSBuild, vb. tüm MSBuild proje dosyası parçası olan ve olmayan `project.json`.</span><span class="sxs-lookup"><span data-stu-id="50bbb-168">Compilation is handled by MSBuild so compilation options, preprocessor defines, etc. are all part of the MSBuild project file and not `project.json`.</span></span>

<span data-ttu-id="50bbb-169">Nuget'te 3 +, geliştiricilerin el ile düzenlemek için beklenmiyor `project.json`gibi Visual Studio'da Paket Yöneticisi UI içeriği yönetir.</span><span class="sxs-lookup"><span data-stu-id="50bbb-169">In NuGet 3+, developers are not expected to manually edit the `project.json`, as the Package Manager UI in Visual Studio manipulates the content.</span></span> <span data-ttu-id="50bbb-170">Bu, dosyanın kesinlikle düzenleyebilirsiniz; ama bir paket geri yüklemeyi başlatmak veya başka bir şekilde geri çağırma için projeyi oluşturmalısınız da belirtti.</span><span class="sxs-lookup"><span data-stu-id="50bbb-170">That said, you can certainly edit the file, but you must build the project to start a package restore or invoke restore in another way.</span></span> <span data-ttu-id="50bbb-171">Bkz: [paket geri yükleme](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="50bbb-171">See [Package restore](../consume-packages/package-restore.md).</span></span>


## <a name="projectlockjson"></a><span data-ttu-id="50bbb-172">project.lock.json</span><span class="sxs-lookup"><span data-stu-id="50bbb-172">project.lock.json</span></span>

<span data-ttu-id="50bbb-173">`project.lock.json` Kullanılan projelerde NuGet paketlerini geri yükleme işleminde dosya oluşturulduğunda `project.json`.</span><span class="sxs-lookup"><span data-stu-id="50bbb-173">The `project.lock.json` file is generated in the process of restoring the NuGet packages in projects that use `project.json`.</span></span> <span data-ttu-id="50bbb-174">Bu bir anlık görüntüsünü NuGet paketleri grafiği size yol gösterir ve projenizde sürüm, içeriği ve Paket bağımlılıklarını içerir oluşturulan tüm bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="50bbb-174">It holds a snapshot of all the information that is generated as NuGet walks the graph of packages and includes the version, contents, and dependencies of all the packages in your project.</span></span> <span data-ttu-id="50bbb-175">Derleme sistemi, bu paket yerine projeyi yerel paketleri klasöründe bağlı olarak projeyi derlerken ilgili genel bir konum seçmek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="50bbb-175">The build system uses this to choose packages from a global location that are relevant when building the project instead of depending on a local packages folder in the project itself.</span></span> <span data-ttu-id="50bbb-176">Salt okunur olarak gerekli olduğundan bu daha hızlı derleme performansla sonuçlanır `project.lock.json` birçok yerine ayrı `.nuspec` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="50bbb-176">This results in faster build performance because it's necessary to read only `project.lock.json` instead of many separate `.nuspec` files.</span></span>

<span data-ttu-id="50bbb-177">`project.lock.json` kaynak denetiminden bu atlanabilir ekleyerek için paket geri yükleme, otomatik olarak oluşturulan `.gitignore` ve `.tfignore` dosyaları (bkz [paketleri ve kaynak denetimi](../consume-packages/packages-and-source-control.md).</span><span class="sxs-lookup"><span data-stu-id="50bbb-177">`project.lock.json` is automatically generated on package restore, so it can be omitted from source control by adding it to `.gitignore` and `.tfignore` files (see [Packages and source control](../consume-packages/packages-and-source-control.md).</span></span> <span data-ttu-id="50bbb-178">Kaynak denetimine dahil, ancak zaman içinde çözümlenen bağımlılıklar değişiklikleri değişiklik geçmişini gösterir.</span><span class="sxs-lookup"><span data-stu-id="50bbb-178">However, if you include it in source control, the change history shows changes in dependencies resolved over time.</span></span>
