---
title: NuGet için'Project.JSON dosyası başvurusu
description: Bazı proje türleri project.json projesinde kullanılan NuGet paketleri listesini tutar.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 07/27/2017
ms.topic: reference
ms.openlocfilehash: e558bdb969d4c70f85a3c89a426f1c7b11525402
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817131"
---
# <a name="projectjson-reference"></a><span data-ttu-id="76088-103">Project.JSON başvurusu</span><span class="sxs-lookup"><span data-stu-id="76088-103">project.json reference</span></span>

<span data-ttu-id="76088-104">*NuGet 3.x+*</span><span class="sxs-lookup"><span data-stu-id="76088-104">*NuGet 3.x+*</span></span>

<span data-ttu-id="76088-105">`project.json` Dosyası paket Yönetimi biçimi bilinen bir projesinde kullanılan paketlerin listesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="76088-105">The `project.json` file maintains a list of packages used in a project, known as a package management format.</span></span> <span data-ttu-id="76088-106">Bu yerine geçiyor `packages.config` sırayla yerine geçen ancak [PackageReference](../consume-packages/package-references-in-project-files.md) NuGet 4.0 + ile.</span><span class="sxs-lookup"><span data-stu-id="76088-106">It supersedes `packages.config` but is in turn superseded by [PackageReference](../consume-packages/package-references-in-project-files.md) with NuGet 4.0+.</span></span>

<span data-ttu-id="76088-107">[ `project.lock.json` ](#projectlockjson) (Aşağıda açıklanmıştır) dosyası da kullanan projelerinde kullanılan `project.json`.</span><span class="sxs-lookup"><span data-stu-id="76088-107">The [`project.lock.json`](#projectlockjson) file (described below) is also used in projects employing `project.json`.</span></span>

<span data-ttu-id="76088-108">`project.json` aşağıdaki temel yapı dört en üst düzey nesnelerin her biri herhangi bir sayıda bağımlı nesnelere sahip olduğu sahiptir:</span><span class="sxs-lookup"><span data-stu-id="76088-108">`project.json` has the following basic structure, where each of the four top-level objects can have any number of child objects:</span></span>

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

## <a name="dependencies"></a><span data-ttu-id="76088-109">Bağımlılıklar</span><span class="sxs-lookup"><span data-stu-id="76088-109">Dependencies</span></span>

<span data-ttu-id="76088-110">Aşağıdaki biçimde projenizin NuGet paket bağımlılıkları listeler:</span><span class="sxs-lookup"><span data-stu-id="76088-110">Lists the NuGet package dependencies of your project in the following form:</span></span>

```json
"PackageID" : "version_constraint"
```

<span data-ttu-id="76088-111">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="76088-111">For example:</span></span>

```json
"dependencies": {
    "Microsoft.NETCore": "5.0.0",
    "System.Runtime.Serialization.Primitives": "4.0.10"
}
```

<span data-ttu-id="76088-112">`dependencies` Bölümdür nerede NuGet Paket Yöneticisi iletişim Paket bağımlılıklarını projenize ekler.</span><span class="sxs-lookup"><span data-stu-id="76088-112">The `dependencies` section is where the NuGet Package Manager dialog adds package dependencies to your project.</span></span>

<span data-ttu-id="76088-113">Paket Yöneticisi Konsolu'nda kullanılan kimliği ile aynı nuget.org paket kimliği için paket kimliğine karşılık gelen: `Install-Package Microsoft.NETCore`.</span><span class="sxs-lookup"><span data-stu-id="76088-113">The Package id corresponds to the id of the package on nuget.org , the same as the id used in the package manager console: `Install-Package Microsoft.NETCore`.</span></span>

<span data-ttu-id="76088-114">Ne zaman geri yükleme paketleri, sürüm kısıtlaması `"5.0.0"` gelir `>= 5.0.0`.</span><span class="sxs-lookup"><span data-stu-id="76088-114">When restoring packages, the version constraint of `"5.0.0"` implies `>= 5.0.0`.</span></span> <span data-ttu-id="76088-115">Diğer bir deyişle, 5.0.0 sunucuda kullanılamıyor 5.0.1 varsa, NuGet 5.0.1 yükler ve yükseltme hakkında sizi uyarır.</span><span class="sxs-lookup"><span data-stu-id="76088-115">That is, if 5.0.0 is not available on the server but 5.0.1 is, NuGet installs  5.0.1 and warns you about the upgrade.</span></span> <span data-ttu-id="76088-116">Aksi takdirde NuGet olası en düşük sürüm kısıtlaması eşleşen sunucuda seçer.</span><span class="sxs-lookup"><span data-stu-id="76088-116">NuGet otherwise picks the lowest possible version on the server matching the constraint.</span></span>

<span data-ttu-id="76088-117">Bkz: [bağımlılık çözümlemesi](../consume-packages/dependency-resolution.md) çözümleme kuralları hakkında daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="76088-117">See [Dependency resolution](../consume-packages/dependency-resolution.md) for more details on resolution rules.</span></span>

### <a name="managing-dependency-assets"></a><span data-ttu-id="76088-118">Bağımlılık varlıklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="76088-118">Managing dependency assets</span></span>

<span data-ttu-id="76088-119">Bağımlılıklar hangi varlıklarından en üst düzey projeye akış etiketlerinde virgülle ayrılmış bir dizi belirterek denetlenir `include` ve `exclude` bağımlılık başvurusu özelliklerini.</span><span class="sxs-lookup"><span data-stu-id="76088-119">Which assets from dependencies flow into the top-level project is controlled by specifying a comma-delimited set of tags in the `include` and `exclude` properties of the dependency reference.</span></span> <span data-ttu-id="76088-120">Etiketler listelenen aşağıdaki tabloda:</span><span class="sxs-lookup"><span data-stu-id="76088-120">The tags are listed the table below:</span></span>

| <span data-ttu-id="76088-121">Etiket dahil etme/hariç tutma</span><span class="sxs-lookup"><span data-stu-id="76088-121">Include/Exclude tag</span></span> | <span data-ttu-id="76088-122">Hedef etkilenen klasörler</span><span class="sxs-lookup"><span data-stu-id="76088-122">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="76088-123">Content dosyaları</span><span class="sxs-lookup"><span data-stu-id="76088-123">contentFiles</span></span> | <span data-ttu-id="76088-124">İçerik</span><span class="sxs-lookup"><span data-stu-id="76088-124">Content</span></span>  |
| <span data-ttu-id="76088-125">çalışma zamanı</span><span class="sxs-lookup"><span data-stu-id="76088-125">runtime</span></span> | <span data-ttu-id="76088-126">Çalışma zamanı, kaynakları ve FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="76088-126">Runtime, Resources, and FrameworkAssemblies</span></span>  |
| <span data-ttu-id="76088-127">Derleme</span><span class="sxs-lookup"><span data-stu-id="76088-127">compile</span></span> | <span data-ttu-id="76088-128">LIB</span><span class="sxs-lookup"><span data-stu-id="76088-128">lib</span></span> |
| <span data-ttu-id="76088-129">derleme</span><span class="sxs-lookup"><span data-stu-id="76088-129">build</span></span> | <span data-ttu-id="76088-130">derleme (MSBuild özellik ve hedefleri)</span><span class="sxs-lookup"><span data-stu-id="76088-130">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="76088-131">yerel</span><span class="sxs-lookup"><span data-stu-id="76088-131">native</span></span> | <span data-ttu-id="76088-132">yerel</span><span class="sxs-lookup"><span data-stu-id="76088-132">native</span></span> |
| <span data-ttu-id="76088-133">yok</span><span class="sxs-lookup"><span data-stu-id="76088-133">none</span></span> | <span data-ttu-id="76088-134">Klasör yok</span><span class="sxs-lookup"><span data-stu-id="76088-134">No folders</span></span> |
| <span data-ttu-id="76088-135">tüm</span><span class="sxs-lookup"><span data-stu-id="76088-135">all</span></span> | <span data-ttu-id="76088-136">Tüm klasörleri</span><span class="sxs-lookup"><span data-stu-id="76088-136">All folders</span></span> |

<span data-ttu-id="76088-137">İle belirtilen etiketleri `exclude` ile belirtilen önceliklidir `include`.</span><span class="sxs-lookup"><span data-stu-id="76088-137">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="76088-138">Örneğin, `include="runtime, compile" exclude="compile"` aynı `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="76088-138">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span>

<span data-ttu-id="76088-139">Örneğin, dahil etmek için `build` ve `native` bir bağımlılık klasörleri aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="76088-139">For example, to include the `build` and `native` folders of a dependency, use the following:</span></span>

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

<span data-ttu-id="76088-140">Dışlanacak `content` ve `build` bir bağımlılık klasörleri aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="76088-140">To exclude the `content` and `build` folders of a dependency, use the following:</span></span>

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

## <a name="frameworks"></a><span data-ttu-id="76088-141">çerçeveler</span><span class="sxs-lookup"><span data-stu-id="76088-141">Frameworks</span></span>

<span data-ttu-id="76088-142">Proje gibi çalışan çerçeveleri listeler `net45`, `netcoreapp`, `netstandard`.</span><span class="sxs-lookup"><span data-stu-id="76088-142">Lists the frameworks that the project runs on, such as `net45`, `netcoreapp`, `netstandard`.</span></span>

```json
"frameworks": {
    "netcore50": {}
    }
 ```

<span data-ttu-id="76088-143">Yalnızca tek bir giriş izin `frameworks` bölümü.</span><span class="sxs-lookup"><span data-stu-id="76088-143">Only a single entry is allowed in the `frameworks` section.</span></span> <span data-ttu-id="76088-144">(Bir özel durum `project.json` dosyaları yapı kullanım dışı DNX ile olan ASP.NET projeleri için araç için birden çok hedef verir zinciri.)</span><span class="sxs-lookup"><span data-stu-id="76088-144">(An exception is `project.json` files for ASP.NET projects that are build with deprecated DNX tool chain, which allows for multiple targets.)</span></span>

## <a name="runtimes"></a><span data-ttu-id="76088-145">Çalışma zamanları</span><span class="sxs-lookup"><span data-stu-id="76088-145">Runtimes</span></span>

<span data-ttu-id="76088-146">Uygulamanızı gibi çalışan işletim sistemleri ve mimariler listeler `win10-arm`, `win8-x64`, `win8-x86`.</span><span class="sxs-lookup"><span data-stu-id="76088-146">Lists the operating systems and architectures that your app runs on, such as `win10-arm`, `win8-x64`, `win8-x86`.</span></span>

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

<span data-ttu-id="76088-147">Tüm çalışma zamanı çalıştırabilirsiniz PCL içeren bir paket, bir çalışma zamanı belirtmek gerekmez.</span><span class="sxs-lookup"><span data-stu-id="76088-147">A package containing a PCL that can run on any runtime doesn't need to specify a runtime.</span></span> <span data-ttu-id="76088-148">Bu ayrıca tüm bağımlılıkları true olmalıdır, aksi halde, çalışma zamanları belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="76088-148">This must also be true of any dependencies, otherwise you must specify runtimes.</span></span>


## <a name="supports"></a><span data-ttu-id="76088-149">Destekler</span><span class="sxs-lookup"><span data-stu-id="76088-149">Supports</span></span>

<span data-ttu-id="76088-150">Paket bağımlılıklarını denetimleri kümesini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="76088-150">Defines a set of checks for package dependencies.</span></span> <span data-ttu-id="76088-151">Burada, PCL veya çalıştırmak için uygulamayı beklediğiniz tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76088-151">You can define where you expect the PCL or app to run.</span></span> <span data-ttu-id="76088-152">Kodunuz başka bir yerde çalıştırabilir gibi tanımları kısıtlayıcı değildir.</span><span class="sxs-lookup"><span data-stu-id="76088-152">The definitions are not restrictive, as your code may be able to run elsewhere.</span></span> <span data-ttu-id="76088-153">Ancak bu denetimlerin belirterek tüm üzerinde listelenen TxMs bağımlılıkların denetleyin NuGet yapar.</span><span class="sxs-lookup"><span data-stu-id="76088-153">But specifying these checks makes NuGet check that all dependencies are satisfied on the listed TxMs.</span></span> <span data-ttu-id="76088-154">Bu öğeler için değeri örnekleri: `net46.app`, `uwp.10.0.app`vb.</span><span class="sxs-lookup"><span data-stu-id="76088-154">Examples of the values for this are: `net46.app`, `uwp.10.0.app`, etc.</span></span>

<span data-ttu-id="76088-155">Taşınabilir sınıf kitaplığı hedefleri iletişim kutusunda bir giriş seçtiğinizde bu bölümde otomatik olarak doldurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="76088-155">This section should be populated automatically when you select an entry in the Portable Class Library targets dialog.</span></span>

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a><span data-ttu-id="76088-156">İçeri aktarmalar</span><span class="sxs-lookup"><span data-stu-id="76088-156">Imports</span></span>

<span data-ttu-id="76088-157">İçeri aktarmalar kullanmak paketleri izin verecek şekilde tasarlanmıştır `dotnet` dotnet TxM bildirmeyin paketlerle çalışmak üzere TxM.</span><span class="sxs-lookup"><span data-stu-id="76088-157">Imports are designed to allow packages that use the `dotnet` TxM to operate with packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="76088-158">Projenizi kullanıyorsanız `dotnet` TxM sonra bağımlı olan tüm paketleri ayrıca olmalıdır bir `dotnet` TxM, aşağıdaki eklemedikçe, `project.json` olmayan izin vermek için `dotnet` ile uyumlu olacak şekilde platformları `dotnet`:</span><span class="sxs-lookup"><span data-stu-id="76088-158">If your project is using the `dotnet` TxM then all the packages you depend on must also have a `dotnet` TxM, unless you add the following to your `project.json` to allow non `dotnet` platforms to be compatible with `dotnet`:</span></span>

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

<span data-ttu-id="76088-159">Kullanıyorsanız `dotnet` TxM sonra PCL proje sistemi ekler uygun `imports` tabanlı desteklenen hedeflerde bildirimi.</span><span class="sxs-lookup"><span data-stu-id="76088-159">If you are using the `dotnet` TxM then the PCL project system adds the appropriate `imports` statement based on the supported targets.</span></span>

## <a name="differences-from-portable-apps-and-web-projects"></a><span data-ttu-id="76088-160">Taşınabilir uygulamaları ve web projeleri arasındaki farklar</span><span class="sxs-lookup"><span data-stu-id="76088-160">Differences from portable apps and web projects</span></span>

<span data-ttu-id="76088-161">`project.json` NuGet tarafından kullanılan bir alt kümesini ASP.NET Core projelerinde bulunan dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="76088-161">The `project.json` file used by NuGet is a subset of that found in ASP.NET Core projects.</span></span> <span data-ttu-id="76088-162">ASP.NET Core içinde `project.json` proje meta veriler, derleme bilgilerini ve bağımlılıklar için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="76088-162">In ASP.NET Core `project.json` is used for project metadata, compilation information, and dependencies.</span></span> <span data-ttu-id="76088-163">Diğer proje sistemlerinde kullanıldığında, bu üç şey ayrı dosyalara ayrılır ve `project.json` daha az bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="76088-163">When used in other project systems, those three things are split into separate files and `project.json` contains less information.</span></span> <span data-ttu-id="76088-164">Önemli farklılıklar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="76088-164">Notable differences include:</span></span>

- <span data-ttu-id="76088-165">Ayrıca bir Framework'te yalnızca olabilir `frameworks` bölümü.</span><span class="sxs-lookup"><span data-stu-id="76088-165">There can only be one framework in the `frameworks` section.</span></span>

- <span data-ttu-id="76088-166">Dosya içeremez bağımlılıkları, derleme seçenekleri, DNX içinde gördüğünüz vb. `project.json` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="76088-166">The file cannot contain dependencies, compilation options, etc. that you see in DNX `project.json` files.</span></span> <span data-ttu-id="76088-167">Yalnızca tek bir çerçeve o çerçeveye özel bağımlılıkları girmek için doesn't make Sense.</span><span class="sxs-lookup"><span data-stu-id="76088-167">Given that there can only be a single framework it doesn't make sense to enter framework-specific dependencies.</span></span>

- <span data-ttu-id="76088-168">Derleme tarafından işlenir derleme seçenekleri, önişlemci tanımlar için MSBuild, vb. MSBuild proje dosyası tüm parçası olan ve olmayan `project.json`.</span><span class="sxs-lookup"><span data-stu-id="76088-168">Compilation is handled by MSBuild so compilation options, preprocessor defines, etc. are all part of the MSBuild project file and not `project.json`.</span></span>

<span data-ttu-id="76088-169">NuGet içinde 3 +, geliştiricilerin el ile düzenleme beklenmez `project.json`Visual Studio'da Paket Yöneticisi kullanıcı Arabirimi içeriği yöneten gibi.</span><span class="sxs-lookup"><span data-stu-id="76088-169">In NuGet 3+, developers are not expected to manually edit the `project.json`, as the Package Manager UI in Visual Studio manipulates the content.</span></span> <span data-ttu-id="76088-170">Bu, kesinlikle dosyasını düzenleyebilir, ancak paket geri yüklemeyi başlatmak veya başka bir şekilde geri çağırma projeyi derleme da belirtti.</span><span class="sxs-lookup"><span data-stu-id="76088-170">That said, you can certainly edit the file, but you must build the project to start a package restore or invoke restore in another way.</span></span> <span data-ttu-id="76088-171">Bkz: [paket geri yüklemesi](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="76088-171">See [Package restore](../consume-packages/package-restore.md).</span></span>


## <a name="projectlockjson"></a><span data-ttu-id="76088-172">project.lock.json</span><span class="sxs-lookup"><span data-stu-id="76088-172">project.lock.json</span></span>

<span data-ttu-id="76088-173">`project.lock.json` Dosyası kullanmak projelerinde NuGet paketleri geri yüklemeyi sürdürüyor oluşturulur `project.json`.</span><span class="sxs-lookup"><span data-stu-id="76088-173">The `project.lock.json` file is generated in the process of restoring the NuGet packages in projects that use `project.json`.</span></span> <span data-ttu-id="76088-174">Bir anlık görüntü olarak NuGet paketleri grafik anlatılmaktadır ve sürüm, içeriği ve tüm paketler bağımlılıklarını projenizde içerir oluşturan tüm bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="76088-174">It holds a snapshot of all the information that is generated as NuGet walks the graph of packages and includes the version, contents, and dependencies of all the packages in your project.</span></span> <span data-ttu-id="76088-175">Derleme sistemi bu paketleri yerine Proje proje yerel paketler klasöründe bağlı olarak oluştururken ilgili genel bir konum seçmek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="76088-175">The build system uses this to choose packages from a global location that are relevant when building the project instead of depending on a local packages folder in the project itself.</span></span> <span data-ttu-id="76088-176">Salt okunur gerekli olduğundan bu daha hızlı derleme performansla sonuçlanır `project.lock.json` birçok yerine ayrı `.nuspec` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="76088-176">This results in faster build performance because it's necessary to read only `project.lock.json` instead of many separate `.nuspec` files.</span></span>

<span data-ttu-id="76088-177">`project.lock.json` kaynak denetiminden onu atlanabilir ekleyerek için paket geri yükleme, otomatik olarak oluşturulan `.gitignore` ve `.tfignore` dosyaları (bkz [paketler ve kaynak denetimi](../consume-packages/packages-and-source-control.md).</span><span class="sxs-lookup"><span data-stu-id="76088-177">`project.lock.json` is automatically generated on package restore, so it can be omitted from source control by adding it to `.gitignore` and `.tfignore` files (see [Packages and source control](../consume-packages/packages-and-source-control.md).</span></span> <span data-ttu-id="76088-178">Ancak, kaynak denetiminde dahil, zaman içinde çözümlenen bağımlılıklar değişiklikleri değişiklik geçmişini gösterir.</span><span class="sxs-lookup"><span data-stu-id="76088-178">However, if you include it in source control, the change history shows changes in dependencies resolved over time.</span></span>
