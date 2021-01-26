---
title: NuGet için dosya başvurusunda project.js
description: Bazı proje türlerinde project.js, projede kullanılan NuGet paketlerinin listesini tutar.
author: JonDouglas
ms.author: jodou
ms.date: 07/27/2017
ms.topic: reference
ms.openlocfilehash: 6665f4f3e688cb4a3989216c8c8f1a8655b61ed8
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775199"
---
# <a name="projectjson-reference"></a><span data-ttu-id="a2292-103">Başvuruya project.js</span><span class="sxs-lookup"><span data-stu-id="a2292-103">project.json reference</span></span>

<span data-ttu-id="a2292-104">*NuGet 3. x +*</span><span class="sxs-lookup"><span data-stu-id="a2292-104">*NuGet 3.x+*</span></span>

<span data-ttu-id="a2292-105">`project.json`Dosya, bir projede kullanılan paketlerin bir listesini tutar ve paket yönetim biçimi olarak bilinir.</span><span class="sxs-lookup"><span data-stu-id="a2292-105">The `project.json` file maintains a list of packages used in a project, known as a package management format.</span></span> <span data-ttu-id="a2292-106">Onun yerini alır `packages.config` ancak bu, NuGet 4.0 + Ile [packagereference](../consume-packages/package-references-in-project-files.md) 'ın yerini almıştır.</span><span class="sxs-lookup"><span data-stu-id="a2292-106">It supersedes `packages.config` but is in turn superseded by [PackageReference](../consume-packages/package-references-in-project-files.md) with NuGet 4.0+.</span></span>

<span data-ttu-id="a2292-107">[`project.lock.json`](#projectlockjson)Dosya (aşağıda açıklanmıştır), kullanan projelerde de kullanılır `project.json` .</span><span class="sxs-lookup"><span data-stu-id="a2292-107">The [`project.lock.json`](#projectlockjson) file (described below) is also used in projects employing `project.json`.</span></span>

<span data-ttu-id="a2292-108">`project.json` Aşağıdaki temel yapıya sahiptir ve burada dört üst düzey nesne herhangi bir sayıda alt nesneye sahip olabilir:</span><span class="sxs-lookup"><span data-stu-id="a2292-108">`project.json` has the following basic structure, where each of the four top-level objects can have any number of child objects:</span></span>

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

## <a name="dependencies"></a><span data-ttu-id="a2292-109">Bağımlılıklar</span><span class="sxs-lookup"><span data-stu-id="a2292-109">Dependencies</span></span>

<span data-ttu-id="a2292-110">Projenizin NuGet paketi bağımlılıklarını aşağıdaki biçimde listeler:</span><span class="sxs-lookup"><span data-stu-id="a2292-110">Lists the NuGet package dependencies of your project in the following form:</span></span>

```json
"PackageID" : "version_constraint"
```

<span data-ttu-id="a2292-111">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="a2292-111">For example:</span></span>

```json
"dependencies": {
    "Microsoft.NETCore": "5.0.0",
    "System.Runtime.Serialization.Primitives": "4.0.10"
}
```

<span data-ttu-id="a2292-112">Bu `dependencies` bölüm, NuGet Paket Yöneticisi iletişim kutusunun projenize paket bağımlılıkları eklediği yerdir.</span><span class="sxs-lookup"><span data-stu-id="a2292-112">The `dependencies` section is where the NuGet Package Manager dialog adds package dependencies to your project.</span></span>

<span data-ttu-id="a2292-113">Paket kimliği, Paket Yöneticisi konsolunda kullanılan kimlikle aynı nuget.org üzerindeki paketin kimliğine karşılık gelir: `Install-Package Microsoft.NETCore` .</span><span class="sxs-lookup"><span data-stu-id="a2292-113">The Package id corresponds to the id of the package on nuget.org , the same as the id used in the package manager console: `Install-Package Microsoft.NETCore`.</span></span>

<span data-ttu-id="a2292-114">Paketleri geri yüklerken, öğesinin sürüm kısıtlaması `"5.0.0"` anlamına gelir `>= 5.0.0` .</span><span class="sxs-lookup"><span data-stu-id="a2292-114">When restoring packages, the version constraint of `"5.0.0"` implies `>= 5.0.0`.</span></span> <span data-ttu-id="a2292-115">Diğer bir deyişle, 5.0.0 sunucuda kullanılabilir değilse ancak 5.0.1 ise NuGet, 5.0.1 ' yi yükleyip yükseltme hakkında sizi uyarır.</span><span class="sxs-lookup"><span data-stu-id="a2292-115">That is, if 5.0.0 is not available on the server but 5.0.1 is, NuGet installs  5.0.1 and warns you about the upgrade.</span></span> <span data-ttu-id="a2292-116">NuGet, kısıtlama ile eşleşen sunucuda mümkün olan en düşük sürümü de seçer.</span><span class="sxs-lookup"><span data-stu-id="a2292-116">NuGet otherwise picks the lowest possible version on the server matching the constraint.</span></span>

<span data-ttu-id="a2292-117">Çözüm kuralları hakkında daha fazla bilgi için bkz. [bağımlılık çözünürlüğü](../concepts/dependency-resolution.md) .</span><span class="sxs-lookup"><span data-stu-id="a2292-117">See [Dependency resolution](../concepts/dependency-resolution.md) for more details on resolution rules.</span></span>

### <a name="managing-dependency-assets"></a><span data-ttu-id="a2292-118">Bağımlılık varlıklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="a2292-118">Managing dependency assets</span></span>

<span data-ttu-id="a2292-119">Bağımlılıklardan en üst düzey projeye akan varlıkların, `include` bağımlılık başvurusunun ve özelliklerinde virgülle ayrılmış bir etiket kümesi belirtilerek denetlenir `exclude` .</span><span class="sxs-lookup"><span data-stu-id="a2292-119">Which assets from dependencies flow into the top-level project is controlled by specifying a comma-delimited set of tags in the `include` and `exclude` properties of the dependency reference.</span></span> <span data-ttu-id="a2292-120">Etiketler aşağıdaki tabloda listelenmiştir:</span><span class="sxs-lookup"><span data-stu-id="a2292-120">The tags are listed the table below:</span></span>

| <span data-ttu-id="a2292-121">Dahil etme/hariç tutma etiketi</span><span class="sxs-lookup"><span data-stu-id="a2292-121">Include/Exclude tag</span></span> | <span data-ttu-id="a2292-122">Hedefin etkilenen klasörleri</span><span class="sxs-lookup"><span data-stu-id="a2292-122">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="a2292-123">contentFiles</span><span class="sxs-lookup"><span data-stu-id="a2292-123">contentFiles</span></span> | <span data-ttu-id="a2292-124">Content</span><span class="sxs-lookup"><span data-stu-id="a2292-124">Content</span></span>  |
| <span data-ttu-id="a2292-125">çalışma zamanı</span><span class="sxs-lookup"><span data-stu-id="a2292-125">runtime</span></span> | <span data-ttu-id="a2292-126">Çalışma zamanı, kaynaklar ve FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="a2292-126">Runtime, Resources, and FrameworkAssemblies</span></span>  |
| <span data-ttu-id="a2292-127">derle</span><span class="sxs-lookup"><span data-stu-id="a2292-127">compile</span></span> | <span data-ttu-id="a2292-128">LIB</span><span class="sxs-lookup"><span data-stu-id="a2292-128">lib</span></span> |
| <span data-ttu-id="a2292-129">derleme</span><span class="sxs-lookup"><span data-stu-id="a2292-129">build</span></span> | <span data-ttu-id="a2292-130">Build (MSBuild props ve targets)</span><span class="sxs-lookup"><span data-stu-id="a2292-130">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="a2292-131">yerel</span><span class="sxs-lookup"><span data-stu-id="a2292-131">native</span></span> | <span data-ttu-id="a2292-132">yerel</span><span class="sxs-lookup"><span data-stu-id="a2292-132">native</span></span> |
| <span data-ttu-id="a2292-133">yok</span><span class="sxs-lookup"><span data-stu-id="a2292-133">none</span></span> | <span data-ttu-id="a2292-134">Klasör yok</span><span class="sxs-lookup"><span data-stu-id="a2292-134">No folders</span></span> |
| <span data-ttu-id="a2292-135">tümü</span><span class="sxs-lookup"><span data-stu-id="a2292-135">all</span></span> | <span data-ttu-id="a2292-136">Tüm klasörler</span><span class="sxs-lookup"><span data-stu-id="a2292-136">All folders</span></span> |

<span data-ttu-id="a2292-137">İle belirtilen Etiketler `exclude` , ile belirtilen değerlere göre önceliğe sahip olacak şekilde belirlenir `include` .</span><span class="sxs-lookup"><span data-stu-id="a2292-137">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="a2292-138">Örneğin, `include="runtime, compile" exclude="compile"` ile aynıdır `include="runtime"` .</span><span class="sxs-lookup"><span data-stu-id="a2292-138">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span>

<span data-ttu-id="a2292-139">Örneğin, `build` `native` bir bağımlılığın ve klasörlerinin dahil olması için aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="a2292-139">For example, to include the `build` and `native` folders of a dependency, use the following:</span></span>

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

<span data-ttu-id="a2292-140">`content`Bir bağımlılığın ve klasörlerinin hariç tutulması için `build` aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="a2292-140">To exclude the `content` and `build` folders of a dependency, use the following:</span></span>

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

## <a name="frameworks"></a><span data-ttu-id="a2292-141">Framework’ler</span><span class="sxs-lookup"><span data-stu-id="a2292-141">Frameworks</span></span>

<span data-ttu-id="a2292-142">Projenin üzerinde çalıştığı çerçeveleri listeler, örneğin,, `net45` `netcoreapp` `netstandard` .</span><span class="sxs-lookup"><span data-stu-id="a2292-142">Lists the frameworks that the project runs on, such as `net45`, `netcoreapp`, `netstandard`.</span></span>

```json
"frameworks": {
    "netcore50": {}
    }
 ```

<span data-ttu-id="a2292-143">Bölümünde yalnızca tek bir girdiye izin verilir `frameworks` .</span><span class="sxs-lookup"><span data-stu-id="a2292-143">Only a single entry is allowed in the `frameworks` section.</span></span> <span data-ttu-id="a2292-144">(Bir özel durum, `project.json` birden çok hedefe izin veren kullanım dışı DNX araç zinciri ile oluşturulan ASP.net projelerine yönelik dosyalardır.)</span><span class="sxs-lookup"><span data-stu-id="a2292-144">(An exception is `project.json` files for ASP.NET projects that are build with deprecated DNX tool chain, which allows for multiple targets.)</span></span>

## <a name="runtimes"></a><span data-ttu-id="a2292-145">Zamanları</span><span class="sxs-lookup"><span data-stu-id="a2292-145">Runtimes</span></span>

<span data-ttu-id="a2292-146">Uygulamanızın üzerinde çalıştığı işletim sistemlerini ve mimarilerini listeler, örneğin,, `win10-arm` `win8-x64` `win8-x86` .</span><span class="sxs-lookup"><span data-stu-id="a2292-146">Lists the operating systems and architectures that your app runs on, such as `win10-arm`, `win8-x64`, `win8-x86`.</span></span>

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

<span data-ttu-id="a2292-147">Herhangi bir çalışma zamanı üzerinde çalışabilecek bir PCL içeren paketin çalışma zamanı belirtmesi gerekmez.</span><span class="sxs-lookup"><span data-stu-id="a2292-147">A package containing a PCL that can run on any runtime doesn't need to specify a runtime.</span></span> <span data-ttu-id="a2292-148">Bu, herhangi bir bağımlılıkda doğru olmalıdır, aksi takdirde çalışma zamanlarını belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a2292-148">This must also be true of any dependencies, otherwise you must specify runtimes.</span></span>


## <a name="supports"></a><span data-ttu-id="a2292-149">Destekleyen</span><span class="sxs-lookup"><span data-stu-id="a2292-149">Supports</span></span>

<span data-ttu-id="a2292-150">Paket bağımlılıkları için bir denetim kümesi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="a2292-150">Defines a set of checks for package dependencies.</span></span> <span data-ttu-id="a2292-151">PCL veya uygulamayı hangi noktada çalıştıracağınızı belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2292-151">You can define where you expect the PCL or app to run.</span></span> <span data-ttu-id="a2292-152">Kodunuzun başka bir yerde çalıştırılabilmesi için tanımlar kısıtlayıcı değildir.</span><span class="sxs-lookup"><span data-stu-id="a2292-152">The definitions are not restrictive, as your code may be able to run elsewhere.</span></span> <span data-ttu-id="a2292-153">Ancak bu denetimlerin belirlenmesi, tüm bağımlılıkların listelenen TxMs üzerinde karşılanıp karşılanmadığını, NuGet denetimi yapar.</span><span class="sxs-lookup"><span data-stu-id="a2292-153">But specifying these checks makes NuGet check that all dependencies are satisfied on the listed TxMs.</span></span> <span data-ttu-id="a2292-154">Bunun değerlerine örnek olarak şunlar verilebilir: `net46.app` , `uwp.10.0.app` , vb.</span><span class="sxs-lookup"><span data-stu-id="a2292-154">Examples of the values for this are: `net46.app`, `uwp.10.0.app`, etc.</span></span>

<span data-ttu-id="a2292-155">Bu bölüm, taşınabilir sınıf kitaplığı hedefleri iletişim kutusunda bir giriş seçtiğinizde otomatik olarak doldurulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a2292-155">This section should be populated automatically when you select an entry in the Portable Class Library targets dialog.</span></span>

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a><span data-ttu-id="a2292-156">İşlemlerinin</span><span class="sxs-lookup"><span data-stu-id="a2292-156">Imports</span></span>

<span data-ttu-id="a2292-157">İçeri aktarmalar, `dotnet` bir DotNet TXD bildirmeyin paketlerle çalışmak üzere TXD kullanan paketlere izin vermek için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="a2292-157">Imports are designed to allow packages that use the `dotnet` TxM to operate with packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="a2292-158">Projeniz `dotnet` TXI kullanıyorsa, `dotnet` `project.json` `dotnet` platformların ile uyumlu olmasını sağlamak için aşağıdaki öğesine eklemediğiniz sürece bağlı olduğunuz tüm paketler bir TXD içermelidir `dotnet` .</span><span class="sxs-lookup"><span data-stu-id="a2292-158">If your project is using the `dotnet` TxM then all the packages you depend on must also have a `dotnet` TxM, unless you add the following to your `project.json` to allow non `dotnet` platforms to be compatible with `dotnet`:</span></span>

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

<span data-ttu-id="a2292-159">`dotnet`TXD 'yi kullanıyorsanız, PCL proje sistemi `imports` desteklenen hedeflere göre uygun ifadeyi ekler.</span><span class="sxs-lookup"><span data-stu-id="a2292-159">If you are using the `dotnet` TxM then the PCL project system adds the appropriate `imports` statement based on the supported targets.</span></span>

## <a name="differences-from-portable-apps-and-web-projects"></a><span data-ttu-id="a2292-160">Taşınabilir uygulamalardan ve Web projelerinden farklılıklar</span><span class="sxs-lookup"><span data-stu-id="a2292-160">Differences from portable apps and web projects</span></span>

<span data-ttu-id="a2292-161">`project.json`NuGet tarafından kullanılan dosya ASP.NET Core projelerinde bulunan bir alt kümesidir.</span><span class="sxs-lookup"><span data-stu-id="a2292-161">The `project.json` file used by NuGet is a subset of that found in ASP.NET Core projects.</span></span> <span data-ttu-id="a2292-162">ASP.NET Core, `project.json` proje meta verileri, derleme bilgileri ve Bağımlılıklar için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a2292-162">In ASP.NET Core `project.json` is used for project metadata, compilation information, and dependencies.</span></span> <span data-ttu-id="a2292-163">Diğer proje sistemlerinde kullanıldığında, bu üç şey ayrı dosyalara bölünür ve `project.json` daha az bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="a2292-163">When used in other project systems, those three things are split into separate files and `project.json` contains less information.</span></span> <span data-ttu-id="a2292-164">Önemli farklar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a2292-164">Notable differences include:</span></span>

- <span data-ttu-id="a2292-165">Bölümde yalnızca bir çerçeve olabilir `frameworks` .</span><span class="sxs-lookup"><span data-stu-id="a2292-165">There can only be one framework in the `frameworks` section.</span></span>

- <span data-ttu-id="a2292-166">Bu dosya DNX dosyalarında gördüğünüz bağımlılıklar, derleme seçenekleri vb. içeremez. `project.json`</span><span class="sxs-lookup"><span data-stu-id="a2292-166">The file cannot contain dependencies, compilation options, etc. that you see in DNX `project.json` files.</span></span> <span data-ttu-id="a2292-167">Yalnızca tek bir çerçeve olabilir. Bu, çerçeveye özgü bağımlılıklar girmek mantıklı değildir.</span><span class="sxs-lookup"><span data-stu-id="a2292-167">Given that there can only be a single framework it doesn't make sense to enter framework-specific dependencies.</span></span>

- <span data-ttu-id="a2292-168">Derleme MSBuild, derleme seçenekleri, Önişlemci tanımlar, vb., MSBuild proje dosyasının tüm parçasıdır `project.json` .</span><span class="sxs-lookup"><span data-stu-id="a2292-168">Compilation is handled by MSBuild so compilation options, preprocessor defines, etc. are all part of the MSBuild project file and not `project.json`.</span></span>

<span data-ttu-id="a2292-169">NuGet 3 + ' de, `project.json` Visual Studio 'Da Paket Yöneticisi Kullanıcı arabirimi içeriği yaparken geliştiricilerin el ile düzenlemesi beklenmez.</span><span class="sxs-lookup"><span data-stu-id="a2292-169">In NuGet 3+, developers are not expected to manually edit the `project.json`, as the Package Manager UI in Visual Studio manipulates the content.</span></span> <span data-ttu-id="a2292-170">Yani, dosyayı kesinlikle düzenleyebilirsiniz, ancak bir paket geri yüklemeyi başlatmak veya geri yüklemeyi başka bir şekilde çağırmak için projeyi derlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a2292-170">That said, you can certainly edit the file, but you must build the project to start a package restore or invoke restore in another way.</span></span> <span data-ttu-id="a2292-171">Bkz. [paket geri yükleme](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="a2292-171">See [Package restore](../consume-packages/package-restore.md).</span></span>


## <a name="projectlockjson"></a><span data-ttu-id="a2292-172">Üzerinde project.lock.js</span><span class="sxs-lookup"><span data-stu-id="a2292-172">project.lock.json</span></span>

<span data-ttu-id="a2292-173">`project.lock.json`Dosya, kullanan projelerde NuGet paketlerini geri yükleme işleminde oluşturulur `project.json` .</span><span class="sxs-lookup"><span data-stu-id="a2292-173">The `project.lock.json` file is generated in the process of restoring the NuGet packages in projects that use `project.json`.</span></span> <span data-ttu-id="a2292-174">NuGet olarak oluşturulan tüm bilgilerin bir anlık görüntüsünü tutar ve kuruluşunuzdaki tüm paketlerin sürümünü, içeriğini ve bağımlılıklarını içerir.</span><span class="sxs-lookup"><span data-stu-id="a2292-174">It holds a snapshot of all the information that is generated as NuGet walks the graph of packages and includes the version, contents, and dependencies of all the packages in your project.</span></span> <span data-ttu-id="a2292-175">Yapı sistemi, projenin kendisindeki yerel paketler klasörüne bağlı olmak yerine, projeyi oluştururken uygun olan küresel bir konumdan paket seçmek için bunu kullanır.</span><span class="sxs-lookup"><span data-stu-id="a2292-175">The build system uses this to choose packages from a global location that are relevant when building the project instead of depending on a local packages folder in the project itself.</span></span> <span data-ttu-id="a2292-176">Bu `project.lock.json` , çok sayıda ayrı dosya yerine yalnızca okunması gerektiğinden daha hızlı derleme performansına neden olur `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="a2292-176">This results in faster build performance because it's necessary to read only `project.lock.json` instead of many separate `.nuspec` files.</span></span>

<span data-ttu-id="a2292-177">`project.lock.json` paket geri yükleme sırasında otomatik olarak oluşturulur. bu nedenle, ve dosyalarına ekleyerek kaynak denetiminden atlanabilir `.gitignore` `.tfignore` (bkz. [paketler ve kaynak denetimi](../consume-packages/packages-and-source-control.md).</span><span class="sxs-lookup"><span data-stu-id="a2292-177">`project.lock.json` is automatically generated on package restore, so it can be omitted from source control by adding it to `.gitignore` and `.tfignore` files (see [Packages and source control](../consume-packages/packages-and-source-control.md).</span></span> <span data-ttu-id="a2292-178">Ancak, kaynak denetimine eklerseniz, değişiklik geçmişi zaman içinde çözümlenen bağımlılıklarda yapılan değişiklikleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="a2292-178">However, if you include it in source control, the change history shows changes in dependencies resolved over time.</span></span>
