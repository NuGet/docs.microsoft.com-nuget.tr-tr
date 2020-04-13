---
title: nuget için project.json Dosya Başvurusu
description: Bazı proje türlerinde project.json, projede kullanılan NuGet paketlerinin listesini tutar.
author: karann-msft
ms.author: karann
ms.date: 07/27/2017
ms.topic: reference
ms.openlocfilehash: 5ecbcd4855de8ea7b6301a5e307779216baf96fc
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "69488292"
---
# <a name="projectjson-reference"></a><span data-ttu-id="9ae38-103">project.json referans</span><span class="sxs-lookup"><span data-stu-id="9ae38-103">project.json reference</span></span>

<span data-ttu-id="9ae38-104">*NuGet 3.x+*</span><span class="sxs-lookup"><span data-stu-id="9ae38-104">*NuGet 3.x+*</span></span>

<span data-ttu-id="9ae38-105">Dosya, `project.json` paket yönetim biçimi olarak bilinen projede kullanılan paketlerin listesini tutar.</span><span class="sxs-lookup"><span data-stu-id="9ae38-105">The `project.json` file maintains a list of packages used in a project, known as a package management format.</span></span> <span data-ttu-id="9ae38-106">Bu yerini `packages.config` alır ama sırayla NuGet 4.0 + ile [PackageReference](../consume-packages/package-references-in-project-files.md) tarafından yerini alır.</span><span class="sxs-lookup"><span data-stu-id="9ae38-106">It supersedes `packages.config` but is in turn superseded by [PackageReference](../consume-packages/package-references-in-project-files.md) with NuGet 4.0+.</span></span>

<span data-ttu-id="9ae38-107">Dosya [`project.lock.json`](#projectlockjson) (aşağıda açıklanan) aynı zamanda istihdam `project.json`projelerde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9ae38-107">The [`project.lock.json`](#projectlockjson) file (described below) is also used in projects employing `project.json`.</span></span>

<span data-ttu-id="9ae38-108">`project.json`dört üst düzey nesnenin her birinin herhangi bir sayıda alt nesneye sahip olabileceği aşağıdaki temel yapıya sahiptir:</span><span class="sxs-lookup"><span data-stu-id="9ae38-108">`project.json` has the following basic structure, where each of the four top-level objects can have any number of child objects:</span></span>

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

## <a name="dependencies"></a><span data-ttu-id="9ae38-109">Bağımlılıklar</span><span class="sxs-lookup"><span data-stu-id="9ae38-109">Dependencies</span></span>

<span data-ttu-id="9ae38-110">Projenizin NuGet paket bağımlılıklarını aşağıdaki şekilde listeler:</span><span class="sxs-lookup"><span data-stu-id="9ae38-110">Lists the NuGet package dependencies of your project in the following form:</span></span>

```json
"PackageID" : "version_constraint"
```

<span data-ttu-id="9ae38-111">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="9ae38-111">For example:</span></span>

```json
"dependencies": {
    "Microsoft.NETCore": "5.0.0",
    "System.Runtime.Serialization.Primitives": "4.0.10"
}
```

<span data-ttu-id="9ae38-112">Bu `dependencies` bölüm, NuGet Paket Yöneticisi iletişim kutusunun projenize paket bağımlılıkları eklediği bölümdür.</span><span class="sxs-lookup"><span data-stu-id="9ae38-112">The `dependencies` section is where the NuGet Package Manager dialog adds package dependencies to your project.</span></span>

<span data-ttu-id="9ae38-113">Paket numarası, paket yöneticisi konsolunda kullanılan id ile aynı olan nuget.org üzerindeki `Install-Package Microsoft.NETCore`paketin kimliğine karşılık gelir: .</span><span class="sxs-lookup"><span data-stu-id="9ae38-113">The Package id corresponds to the id of the package on nuget.org , the same as the id used in the package manager console: `Install-Package Microsoft.NETCore`.</span></span>

<span data-ttu-id="9ae38-114">Paketleri geri alırken, sürüm `"5.0.0"` kısıtlaması `>= 5.0.0`ima eder.</span><span class="sxs-lookup"><span data-stu-id="9ae38-114">When restoring packages, the version constraint of `"5.0.0"` implies `>= 5.0.0`.</span></span> <span data-ttu-id="9ae38-115">Yani, 5.0.0 sunucuda kullanılamıyorsa ancak 5.0.1 ise, NuGet 5.0.1 yükler ve yükseltme hakkında sizi uyarır.</span><span class="sxs-lookup"><span data-stu-id="9ae38-115">That is, if 5.0.0 is not available on the server but 5.0.1 is, NuGet installs  5.0.1 and warns you about the upgrade.</span></span> <span data-ttu-id="9ae38-116">NuGet aksi takdirde kısıtlama eşleşen sunucuda mümkün olan en düşük sürümü seçer.</span><span class="sxs-lookup"><span data-stu-id="9ae38-116">NuGet otherwise picks the lowest possible version on the server matching the constraint.</span></span>

<span data-ttu-id="9ae38-117">Çözüm kuralları hakkında daha fazla ayrıntı için Bağımlılık çözümlemesi'ne bakın. [Dependency resolution](../concepts/dependency-resolution.md)</span><span class="sxs-lookup"><span data-stu-id="9ae38-117">See [Dependency resolution](../concepts/dependency-resolution.md) for more details on resolution rules.</span></span>

### <a name="managing-dependency-assets"></a><span data-ttu-id="9ae38-118">Bağımlılık varlıklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="9ae38-118">Managing dependency assets</span></span>

<span data-ttu-id="9ae38-119">Bağımlılıklardan hangi varlıkların üst düzey projeye aktığı, bağımlılık başvurusu ve `include` `exclude` özelliklerinde virgülle sınırlandırılmış etiketler kümesi belirtilerek denetlenir.</span><span class="sxs-lookup"><span data-stu-id="9ae38-119">Which assets from dependencies flow into the top-level project is controlled by specifying a comma-delimited set of tags in the `include` and `exclude` properties of the dependency reference.</span></span> <span data-ttu-id="9ae38-120">Etiketler aşağıdaki tabloda listelenmiştir:</span><span class="sxs-lookup"><span data-stu-id="9ae38-120">The tags are listed the table below:</span></span>

| <span data-ttu-id="9ae38-121">Etiketi ekle/hariç tut</span><span class="sxs-lookup"><span data-stu-id="9ae38-121">Include/Exclude tag</span></span> | <span data-ttu-id="9ae38-122">Hedefin etkilenen klasörleri</span><span class="sxs-lookup"><span data-stu-id="9ae38-122">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="9ae38-123">içerikDosyalar</span><span class="sxs-lookup"><span data-stu-id="9ae38-123">contentFiles</span></span> | <span data-ttu-id="9ae38-124">İçerik</span><span class="sxs-lookup"><span data-stu-id="9ae38-124">Content</span></span>  |
| <span data-ttu-id="9ae38-125">çalışma zamanı</span><span class="sxs-lookup"><span data-stu-id="9ae38-125">runtime</span></span> | <span data-ttu-id="9ae38-126">Çalışma Zamanı, Kaynaklar ve FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="9ae38-126">Runtime, Resources, and FrameworkAssemblies</span></span>  |
| <span data-ttu-id="9ae38-127">derle</span><span class="sxs-lookup"><span data-stu-id="9ae38-127">compile</span></span> | <span data-ttu-id="9ae38-128">Lib</span><span class="sxs-lookup"><span data-stu-id="9ae38-128">lib</span></span> |
| <span data-ttu-id="9ae38-129">derleme</span><span class="sxs-lookup"><span data-stu-id="9ae38-129">build</span></span> | <span data-ttu-id="9ae38-130">yapı (MSBuild sahne ve hedefleri)</span><span class="sxs-lookup"><span data-stu-id="9ae38-130">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="9ae38-131">yerel</span><span class="sxs-lookup"><span data-stu-id="9ae38-131">native</span></span> | <span data-ttu-id="9ae38-132">yerel</span><span class="sxs-lookup"><span data-stu-id="9ae38-132">native</span></span> |
| <span data-ttu-id="9ae38-133">yok</span><span class="sxs-lookup"><span data-stu-id="9ae38-133">none</span></span> | <span data-ttu-id="9ae38-134">Klasör yok</span><span class="sxs-lookup"><span data-stu-id="9ae38-134">No folders</span></span> |
| <span data-ttu-id="9ae38-135">tümü</span><span class="sxs-lookup"><span data-stu-id="9ae38-135">all</span></span> | <span data-ttu-id="9ae38-136">Tüm klasörler</span><span class="sxs-lookup"><span data-stu-id="9ae38-136">All folders</span></span> |

<span data-ttu-id="9ae38-137">'ile `exclude` belirtilenlerden önce gelen `include`etiketler.</span><span class="sxs-lookup"><span data-stu-id="9ae38-137">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="9ae38-138">Örneğin, `include="runtime, compile" exclude="compile"` aynı `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="9ae38-138">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span>

<span data-ttu-id="9ae38-139">Örneğin, bir `build` bağımlılığın `native` klasörlerini ve klasörlerini eklemek için aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="9ae38-139">For example, to include the `build` and `native` folders of a dependency, use the following:</span></span>

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

<span data-ttu-id="9ae38-140">Bir `content` bağımlılığın `build` ve klasörlerini hariç tutmak için aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="9ae38-140">To exclude the `content` and `build` folders of a dependency, use the following:</span></span>

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

## <a name="frameworks"></a><span data-ttu-id="9ae38-141">Framework’ler</span><span class="sxs-lookup"><span data-stu-id="9ae38-141">Frameworks</span></span>

<span data-ttu-id="9ae38-142">Projenin üzerinde çalıştığı çerçeveleri listeler, `net45`örneğin `netcoreapp` `netstandard`, , .</span><span class="sxs-lookup"><span data-stu-id="9ae38-142">Lists the frameworks that the project runs on, such as `net45`, `netcoreapp`, `netstandard`.</span></span>

```json
"frameworks": {
    "netcore50": {}
    }
 ```

<span data-ttu-id="9ae38-143">Bölümde yalnızca tek bir `frameworks` girişe izin verilir.</span><span class="sxs-lookup"><span data-stu-id="9ae38-143">Only a single entry is allowed in the `frameworks` section.</span></span> <span data-ttu-id="9ae38-144">(Bir istisna, birden çok hedefe izin veren, amortismana uygun DNX takım zinciriyle oluşturulan ASP.NET projeler için `project.json` dosyalardır.)</span><span class="sxs-lookup"><span data-stu-id="9ae38-144">(An exception is `project.json` files for ASP.NET projects that are build with deprecated DNX tool chain, which allows for multiple targets.)</span></span>

## <a name="runtimes"></a><span data-ttu-id="9ae38-145">Çalıştırma</span><span class="sxs-lookup"><span data-stu-id="9ae38-145">Runtimes</span></span>

<span data-ttu-id="9ae38-146">Uygulamanızın çalıştığı işletim sistemlerini ve mimarileri listeler, `win8-x64` `win8-x86`örneğin `win10-arm`, .</span><span class="sxs-lookup"><span data-stu-id="9ae38-146">Lists the operating systems and architectures that your app runs on, such as `win10-arm`, `win8-x64`, `win8-x86`.</span></span>

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

<span data-ttu-id="9ae38-147">Herhangi bir çalışma zamanında çalıştırılabilen bir PCL içeren paketin çalışma zamanı belirtmesi gerekmez.</span><span class="sxs-lookup"><span data-stu-id="9ae38-147">A package containing a PCL that can run on any runtime doesn't need to specify a runtime.</span></span> <span data-ttu-id="9ae38-148">Bu, tüm bağımlılıklar için de geçerli olmalıdır, aksi takdirde çalışma sürelerini belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ae38-148">This must also be true of any dependencies, otherwise you must specify runtimes.</span></span>


## <a name="supports"></a><span data-ttu-id="9ae38-149">Destekleyen</span><span class="sxs-lookup"><span data-stu-id="9ae38-149">Supports</span></span>

<span data-ttu-id="9ae38-150">Paket bağımlılıkları için bir denetim kümesi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="9ae38-150">Defines a set of checks for package dependencies.</span></span> <span data-ttu-id="9ae38-151">PCL veya uygulamanın nerede çalışmasını beklediğiniz tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ae38-151">You can define where you expect the PCL or app to run.</span></span> <span data-ttu-id="9ae38-152">Kodunuz başka bir yerde çalıştırılabildiği için tanımlar kısıtlayıcı değildir.</span><span class="sxs-lookup"><span data-stu-id="9ae38-152">The definitions are not restrictive, as your code may be able to run elsewhere.</span></span> <span data-ttu-id="9ae38-153">Ancak bu denetimleri belirtmek NuGet'in listelenen TxM'lerde tüm bağımlılıkların karşıdan olduğunu denetlemesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="9ae38-153">But specifying these checks makes NuGet check that all dependencies are satisfied on the listed TxMs.</span></span> <span data-ttu-id="9ae38-154">Bunun için değerlere örnek `net46.app` `uwp.10.0.app`olarak şunlar verilebilir: , , vb.</span><span class="sxs-lookup"><span data-stu-id="9ae38-154">Examples of the values for this are: `net46.app`, `uwp.10.0.app`, etc.</span></span>

<span data-ttu-id="9ae38-155">Taşınabilir Sınıf Kitaplığı hedef iletişim kutusunda bir giriş seçtiğinizde bu bölüm otomatik olarak doldurulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9ae38-155">This section should be populated automatically when you select an entry in the Portable Class Library targets dialog.</span></span>

```json
"supports": {
    "net46.app": {},
    "uwp.10.0.app": {}
}
```

## <a name="imports"></a><span data-ttu-id="9ae38-156">Ithalat</span><span class="sxs-lookup"><span data-stu-id="9ae38-156">Imports</span></span>

<span data-ttu-id="9ae38-157">İçe alma, TxM `dotnet` kullanan paketlerin dotnet TxM beyan etmeyen paketlerle çalışmasına izin verecek şekilde tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="9ae38-157">Imports are designed to allow packages that use the `dotnet` TxM to operate with packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="9ae38-158">`dotnet` Projeniz TxM kullanıyorsa, bağlı olduğunuz tüm paketlerin `dotnet` de bir TxM'si `project.json` olmalıdır, `dotnet` eğer aşağıdakileri `dotnet`eklemediğiniz sürece platformların aşağıdakilerle uyumlu olmasını sağlarsınız:</span><span class="sxs-lookup"><span data-stu-id="9ae38-158">If your project is using the `dotnet` TxM then all the packages you depend on must also have a `dotnet` TxM, unless you add the following to your `project.json` to allow non `dotnet` platforms to be compatible with `dotnet`:</span></span>

```json
"frameworks": {
    "dotnet": { "imports" : "portable-net45+win81" }
}
```

<span data-ttu-id="9ae38-159">TxM kullanıyorsanız, `dotnet` PCL proje sistemi desteklenen `imports` hedeflere göre uygun ifadeyi ekler.</span><span class="sxs-lookup"><span data-stu-id="9ae38-159">If you are using the `dotnet` TxM then the PCL project system adds the appropriate `imports` statement based on the supported targets.</span></span>

## <a name="differences-from-portable-apps-and-web-projects"></a><span data-ttu-id="9ae38-160">Taşınabilir uygulamalardan ve web projelerinden farklar</span><span class="sxs-lookup"><span data-stu-id="9ae38-160">Differences from portable apps and web projects</span></span>

<span data-ttu-id="9ae38-161">NuGet tarafından kullanılan `project.json` dosya, ASP.NET Core projelerinde bulunan bir alt kümesidir.</span><span class="sxs-lookup"><span data-stu-id="9ae38-161">The `project.json` file used by NuGet is a subset of that found in ASP.NET Core projects.</span></span> <span data-ttu-id="9ae38-162">ASP.NET Core `project.json` proje meta verileri, derleme bilgileri ve bağımlılıkları için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9ae38-162">In ASP.NET Core `project.json` is used for project metadata, compilation information, and dependencies.</span></span> <span data-ttu-id="9ae38-163">Diğer proje sistemlerinde kullanıldığında, bu üç şey ayrı `project.json` dosyalara ayrılır ve daha az bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="9ae38-163">When used in other project systems, those three things are split into separate files and `project.json` contains less information.</span></span> <span data-ttu-id="9ae38-164">Önemli farklılıklar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="9ae38-164">Notable differences include:</span></span>

- <span data-ttu-id="9ae38-165">`frameworks` Bölümde yalnızca bir çerçeve olabilir.</span><span class="sxs-lookup"><span data-stu-id="9ae38-165">There can only be one framework in the `frameworks` section.</span></span>

- <span data-ttu-id="9ae38-166">Dosya, DNX `project.json` dosyalarında gördüğünüz bağımlılıkları, derleme seçeneklerini vb. içeremez.</span><span class="sxs-lookup"><span data-stu-id="9ae38-166">The file cannot contain dependencies, compilation options, etc. that you see in DNX `project.json` files.</span></span> <span data-ttu-id="9ae38-167">Sadece tek bir çerçeve olabileceği göz önüne alındığında, çerçeveye özgü bağımlılıkları girmek mantıklı değildir.</span><span class="sxs-lookup"><span data-stu-id="9ae38-167">Given that there can only be a single framework it doesn't make sense to enter framework-specific dependencies.</span></span>

- <span data-ttu-id="9ae38-168">Derleme MSBuild tarafından bu nedenle derleme seçenekleri, önişlemci tanımlar, vb MSBuild proje dosyasının bir parçasıdır ve `project.json`.</span><span class="sxs-lookup"><span data-stu-id="9ae38-168">Compilation is handled by MSBuild so compilation options, preprocessor defines, etc. are all part of the MSBuild project file and not `project.json`.</span></span>

<span data-ttu-id="9ae38-169">NuGet 3+'ta, Visual Studio'daki Paket `project.json`Yöneticisi Kullanıcı UI içeriği manipüle ettiği için geliştiricilerin el ile düzenlemesi beklenmez.</span><span class="sxs-lookup"><span data-stu-id="9ae38-169">In NuGet 3+, developers are not expected to manually edit the `project.json`, as the Package Manager UI in Visual Studio manipulates the content.</span></span> <span data-ttu-id="9ae38-170">Bununla birlikte, dosyayı kesinlikle düzenleyebilirsiniz, ancak bir paket geri yüklemebaşlatmak veya başka bir şekilde geri yükleme çağırmak için projeyi oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ae38-170">That said, you can certainly edit the file, but you must build the project to start a package restore or invoke restore in another way.</span></span> <span data-ttu-id="9ae38-171">Bkz. [Paket geri yükleme.](../consume-packages/package-restore.md)</span><span class="sxs-lookup"><span data-stu-id="9ae38-171">See [Package restore](../consume-packages/package-restore.md).</span></span>


## <a name="projectlockjson"></a><span data-ttu-id="9ae38-172">project.lock.json</span><span class="sxs-lookup"><span data-stu-id="9ae38-172">project.lock.json</span></span>

<span data-ttu-id="9ae38-173">Dosya, `project.lock.json` nuget paketlerini kullanan `project.json`projelerde geri alma işleminde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="9ae38-173">The `project.lock.json` file is generated in the process of restoring the NuGet packages in projects that use `project.json`.</span></span> <span data-ttu-id="9ae38-174">NuGet paketlerin grafiğinde yürürken oluşturulan tüm bilgilerin anlık görüntüsünü tutar ve projenizdeki tüm paketlerin sürümünü, içeriğini ve bağımlılıklarını içerir.</span><span class="sxs-lookup"><span data-stu-id="9ae38-174">It holds a snapshot of all the information that is generated as NuGet walks the graph of packages and includes the version, contents, and dependencies of all the packages in your project.</span></span> <span data-ttu-id="9ae38-175">Yapı sistemi, projenin kendisindeki yerel paketler klasörüne bağlı kalmak yerine projeyi oluştururken ilgili olan genel bir konumdan paketleri seçmek için bunu kullanır.</span><span class="sxs-lookup"><span data-stu-id="9ae38-175">The build system uses this to choose packages from a global location that are relevant when building the project instead of depending on a local packages folder in the project itself.</span></span> <span data-ttu-id="9ae38-176">Bu, birçok ayrı `project.lock.json` `.nuspec` dosya yerine yalnızca okumak gerektiğinden daha hızlı yapı performansı sağlar.</span><span class="sxs-lookup"><span data-stu-id="9ae38-176">This results in faster build performance because it's necessary to read only `project.lock.json` instead of many separate `.nuspec` files.</span></span>

<span data-ttu-id="9ae38-177">`project.lock.json`paket geri yüklemesi otomatik olarak oluşturulur, böylece kaynak denetiminden `.gitignore` ekleyip `.tfignore` dosyalara eklenebilir (bkz. [Paketler ve kaynak denetimi.](../consume-packages/packages-and-source-control.md)</span><span class="sxs-lookup"><span data-stu-id="9ae38-177">`project.lock.json` is automatically generated on package restore, so it can be omitted from source control by adding it to `.gitignore` and `.tfignore` files (see [Packages and source control](../consume-packages/packages-and-source-control.md).</span></span> <span data-ttu-id="9ae38-178">Ancak, kaynak denetimine eklerseniz, değişiklik geçmişi zaman içinde çözülen bağımlılıkdeğişiklikleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="9ae38-178">However, if you include it in source control, the change history shows changes in dependencies resolved over time.</span></span>
