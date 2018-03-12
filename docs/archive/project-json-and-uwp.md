---
title: "NuGet project.json dosyası UWP projeleri | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 07/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Evrensel Windows Platformu (UWP) projelerinde NuGet bağımlılıkları izlemek için project.json dosyasına nasıl kullanıldığı açıklaması."
keywords: "NuGet bağımlılıkları, NuGet ve UWP, UWP ve project.json, NuGet project.json dosyası"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3ef3703b2be92f84d37866bce9934ebcfed3a9f7
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/08/2018
---
# <a name="projectjson-and-uwp"></a><span data-ttu-id="520b7-104">Project.JSON ve UWP</span><span class="sxs-lookup"><span data-stu-id="520b7-104">project.json and UWP</span></span>

> [!Important]
> <span data-ttu-id="520b7-105">Bu içerik kullanım dışı bırakılmıştır.</span><span class="sxs-lookup"><span data-stu-id="520b7-105">This content is deprecated.</span></span> <span data-ttu-id="520b7-106">Projeleri ya da kullanması gereken `packages.config` veya PackageReference biçimleri.</span><span class="sxs-lookup"><span data-stu-id="520b7-106">Projects should use either the `packages.config` or PackageReference formats.</span></span>

<span data-ttu-id="520b7-107">Bu belge NuGet 3 + özelliklerinde (2015 ve sonraki Visual Studio) kullanan paket yapısını açıklar.</span><span class="sxs-lookup"><span data-stu-id="520b7-107">This document describes the package structure that employs features in NuGet 3+ (Visual Studio 2015 and later).</span></span> <span data-ttu-id="520b7-108">`minClientVersion` Özelliği, `.nuspec` için 3.1 ayarlayarak burada açıklanan özellikleri gerektirir durum için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="520b7-108">The `minClientVersion` property of your `.nuspec` can be used to state that you require the features described here by setting it to 3.1.</span></span>

## <a name="adding-uwp-support-to-an-existing-package"></a><span data-ttu-id="520b7-109">Varolan paketini UWP desteği ekleme</span><span class="sxs-lookup"><span data-stu-id="520b7-109">Adding UWP support to an existing package</span></span>

<span data-ttu-id="520b7-110">Var olan bir paket varsa ve UWP uygulamalar için destek eklemek istediğiniz, burada açıklanan paketleme biçimine uyar gerekmez.</span><span class="sxs-lookup"><span data-stu-id="520b7-110">If you have an existing package and you want to add support for UWP applications, then you don’t need to adopt the  packaging format described here.</span></span> <span data-ttu-id="520b7-111">Yalnızca özelliklerini açıklar ve NuGet istemci sürümüne 3 + güncelleyen istemcileri ile çalışma konusunda istekli gerekiyorsa bu biçim benimsemeyi gerekir.</span><span class="sxs-lookup"><span data-stu-id="520b7-111">You only need to adopt this format if you require the features it describes and are willing to  work only with clients that have updated to version 3+ of the NuGet client.</span></span>

## <a name="i-already-target-netcore45"></a><span data-ttu-id="520b7-112">I zaten netcore45 hedef</span><span class="sxs-lookup"><span data-stu-id="520b7-112">I already target netcore45</span></span>

<span data-ttu-id="520b7-113">Hedefliyorsanız `netcore45` zaten ve özelliklerinden burada yapmanıza gerek yoktur, Eylem gerekmiyor.</span><span class="sxs-lookup"><span data-stu-id="520b7-113">If you target `netcore45` already, and you don’t need to take advantage of the features here, no action is needed.</span></span> <span data-ttu-id="520b7-114">`netcore45` paketleri UWP uygulamaları tarafından kullanılabilecek.</span><span class="sxs-lookup"><span data-stu-id="520b7-114">`netcore45` packages can be consumed by UWP applications.</span></span>

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a><span data-ttu-id="520b7-115">Windows 10 özel API'leri yararlanmak istiyorum</span><span class="sxs-lookup"><span data-stu-id="520b7-115">I want to take advantage of Windows 10 specific APIs</span></span>

<span data-ttu-id="520b7-116">Bu durumda, eklemeniz gerekir `uap10.0` framework bilinen ad (TFM veya TxM) paketiniz için hedef.</span><span class="sxs-lookup"><span data-stu-id="520b7-116">In this case you need to add the `uap10.0` target framework moniker (TFM or TxM) to your package.</span></span> <span data-ttu-id="520b7-117">Paketinize yeni bir klasör oluşturun ve bu klasöre Windows 10 ile çalışmak için derlenmiş derleme ekleyin.</span><span class="sxs-lookup"><span data-stu-id="520b7-117">Create a new folder in your package and add the assembly that has been compiled to work with Windows 10 to that folder.</span></span>

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a><span data-ttu-id="520b7-118">Windows 10 özel API'leri, gerek yoktur, ancak yeni .NET özellikleri istediğiniz veya netcore45 zaten yok</span><span class="sxs-lookup"><span data-stu-id="520b7-118">I don’t need Windows 10 specific APIs, but want new .NET features or don’t have netcore45 already</span></span>

<span data-ttu-id="520b7-119">Bu durumda, eklediğiniz `dotnet` TxM paketiniz için.</span><span class="sxs-lookup"><span data-stu-id="520b7-119">In this case you would add the `dotnet` TxM to your package.</span></span> <span data-ttu-id="520b7-120">Diğer TxMs aksine `dotnet` yüzey alanını ya da platform anlamına değil.</span><span class="sxs-lookup"><span data-stu-id="520b7-120">Unlike other TxMs, `dotnet` doesn't imply a surface area or platform.</span></span> <span data-ttu-id="520b7-121">Bu, paketinizi bağımlılıklarınızı çalıştığı herhangi bir platformda çalışan belirten olur.</span><span class="sxs-lookup"><span data-stu-id="520b7-121">It is stating that your package works on any platform that your dependencies work on.</span></span> <span data-ttu-id="520b7-122">Olan bir paket oluştururken `dotnet` TxM, pek çok daha fazla TxM özgü bağımlılıkları vardır büyük olasılıkla, `.nuspec`gibi bağımlı BCL paketleri tanımlamanız gibi `System.Text`, `System.Xml`vb. Bu bağımlılıklar çalıştığı konumlarını paketinizi çalıştığı tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="520b7-122">When building a package with the `dotnet` TxM, you are likely to have many more TxM-specific dependencies in your `.nuspec`, as you need to define the BCL packages you depend on, such `System.Text`, `System.Xml`, etc. The locations that those dependencies work on define where your package works.</span></span>

### <a name="how-do-i-find-out-my-dependencies"></a><span data-ttu-id="520b7-123">My bağımlılıkları nasıl bulabilirim</span><span class="sxs-lookup"><span data-stu-id="520b7-123">How do I find out my dependencies</span></span>

<span data-ttu-id="520b7-124">Listelemek için hangi bağımlılıkları bulmak için iki yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="520b7-124">There are two ways to figure out which dependencies to list:</span></span>

1. <span data-ttu-id="520b7-125">Kullanım [NuSpec bağımlılık Oluşturucu](https://github.com/onovotny/ReferenceGenerator) **3. taraf** aracı.</span><span class="sxs-lookup"><span data-stu-id="520b7-125">Use the [NuSpec Dependency Generator](https://github.com/onovotny/ReferenceGenerator) **3rd party** tool.</span></span> <span data-ttu-id="520b7-126">Aracı işlemi ve güncelleştirmeleri otomatikleştirir, `.nuspec` yapı bağımlı paketleriyle dosyada.</span><span class="sxs-lookup"><span data-stu-id="520b7-126">The tool automates the process and updates your `.nuspec` file with the dependant packages on build.</span></span> <span data-ttu-id="520b7-127">Bir NuGet paketi kullanılabilir [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).</span><span class="sxs-lookup"><span data-stu-id="520b7-127">It is available via a NuGet package, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).</span></span>

1. <span data-ttu-id="520b7-128">(Sabit yolu) Kullanım `ILDasm` bakmak için `.dll` hangi derlemelerin çalışma zamanında gerçekten gerekli olan görmek için.</span><span class="sxs-lookup"><span data-stu-id="520b7-128">(The hard way) Use `ILDasm` to look at your `.dll` to see what assemblies are actually needed at runtime.</span></span> <span data-ttu-id="520b7-129">Sonra her geliyor hangi NuGet paketi belirleyin.</span><span class="sxs-lookup"><span data-stu-id="520b7-129">Then determine which NuGet package they each come from.</span></span>

<span data-ttu-id="520b7-130">Bkz: [ `project.json` ](project-json.md) destekleyen bir paket oluşturulmasında yardımcı olan özellikler hakkında ayrıntılı bilgi için konu `dotnet` TxM.</span><span class="sxs-lookup"><span data-stu-id="520b7-130">See the [`project.json`](project-json.md) topic for details on features that help in the creation of a package that supports the `dotnet` TxM.</span></span>

> [!Important]
> <span data-ttu-id="520b7-131">Paketinizi PCL projelerle çalışmak için amaçlanıyorsa oluşturmak için öneririz bir `dotnet` uyarılar ve olası uyumluluk sorunları önlemek için klasör.</span><span class="sxs-lookup"><span data-stu-id="520b7-131">If your package is intended to work with PCL projects, we highly recommend to create a `dotnet` folder, to avoid warnings and potential compatibility issues.</span></span>

## <a name="directory-structure"></a><span data-ttu-id="520b7-132">Dizin yapısı</span><span class="sxs-lookup"><span data-stu-id="520b7-132">Directory structure</span></span>

<span data-ttu-id="520b7-133">NuGet paketlerini bu biçimi kullanarak aşağıdaki bilinen klasör ve davranışları vardır:</span><span class="sxs-lookup"><span data-stu-id="520b7-133">NuGet packages using this format have the following well-known folder and behaviors:</span></span>

| <span data-ttu-id="520b7-134">Klasör</span><span class="sxs-lookup"><span data-stu-id="520b7-134">Folder</span></span> | <span data-ttu-id="520b7-135">Davranışlar</span><span class="sxs-lookup"><span data-stu-id="520b7-135">Behaviors</span></span> |
| --- | --- |
| <span data-ttu-id="520b7-136">Derleme</span><span class="sxs-lookup"><span data-stu-id="520b7-136">Build</span></span> | <span data-ttu-id="520b7-137">MSBuild içeren hedefleri ve özellik dosyalarını bu klasöre farklı projeye tümleşik ancak Aksi halde değişiklik yoktur.</span><span class="sxs-lookup"><span data-stu-id="520b7-137">Contains MSBuild targets and props files in this folder are integrated differently into the project, but otherwise there is no change.</span></span> |
| <span data-ttu-id="520b7-138">Araçlar</span><span class="sxs-lookup"><span data-stu-id="520b7-138">Tools</span></span> | <span data-ttu-id="520b7-139">`install.ps1` ve `uninstall.ps1` çalıştırılamaz.</span><span class="sxs-lookup"><span data-stu-id="520b7-139">`install.ps1` and `uninstall.ps1` are not run.</span></span> <span data-ttu-id="520b7-140">`init.ps1` her zaman olduğu gibi çalışır.</span><span class="sxs-lookup"><span data-stu-id="520b7-140">`init.ps1` works as it always has.</span></span> |
| <span data-ttu-id="520b7-141">İçerik</span><span class="sxs-lookup"><span data-stu-id="520b7-141">Content</span></span> | <span data-ttu-id="520b7-142">İçeriği otomatik olarak bir kullanıcının projeye kopyalanmaz.</span><span class="sxs-lookup"><span data-stu-id="520b7-142">Content is not copied automatically into a user's project.</span></span> <span data-ttu-id="520b7-143">Projedeki içerik ekleme desteği için sonraki bir sürümü planlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="520b7-143">Support for content inclusion in the project is planned for a later release.</span></span> |
| <span data-ttu-id="520b7-144">Lib</span><span class="sxs-lookup"><span data-stu-id="520b7-144">Lib</span></span> | <span data-ttu-id="520b7-145">Çoğu paketlere ilişkin `lib` NuGet içinde mevcut aynı şekilde çalışır 2.x, ancak hangi adları için genişletilmiş seçenekleriyle kullanılabilir ve daha iyi mantığı içinde doğru alt klasörü paketler kullanırken çekme.</span><span class="sxs-lookup"><span data-stu-id="520b7-145">For many packages the `lib` works the same way it does in NuGet 2.x, but with expanded options for what names can be used inside it and better logic for picking the correct sub-folder when consuming packages.</span></span> <span data-ttu-id="520b7-146">Ancak, ile birlikte kullanıldığında `ref`, `lib` klasörde derlemelerde tarafından tanımlanan yüzey alanını uygulamak derlemeler `ref` klasör.</span><span class="sxs-lookup"><span data-stu-id="520b7-146">However, when used in conjunction with `ref`, the `lib` folder contains assemblies that implement the surface area defined by the assemblies in the `ref` folder.</span></span> |
| <span data-ttu-id="520b7-147">Ref</span><span class="sxs-lookup"><span data-stu-id="520b7-147">Ref</span></span> | <span data-ttu-id="520b7-148">`ref` Ortak tanımlama .NET derlemelerini içeren bir isteğe bağlı klasördür karşı derlemek bir uygulama için yüzey (Genel türleri ve yöntemleri).</span><span class="sxs-lookup"><span data-stu-id="520b7-148">`ref` is an optional folder that contains .NET assemblies defining the public surface (public types and methods) for an application to compile against.</span></span> <span data-ttu-id="520b7-149">Bu klasör derlemelerde uygulaması olabilir, bunlar tamamen derleyici yüzey alanını tanımlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="520b7-149">The assemblies in this folder may have no implementation, they are purely used to define surface area for the compiler.</span></span> <span data-ttu-id="520b7-150">Paket Hayır varsa `ref` klasörü, sonra `lib` referans derlemesini ve uygulaması derleme.</span><span class="sxs-lookup"><span data-stu-id="520b7-150">If the package has no `ref` folder, then the `lib` is both the reference assembly and the implementation assembly.</span></span> |
| <span data-ttu-id="520b7-151">Çalışma zamanları</span><span class="sxs-lookup"><span data-stu-id="520b7-151">Runtimes</span></span> | <span data-ttu-id="520b7-152">`runtimes` CPU mimarisi ve işletim sistemi belirli veya başka türlü platforma bağımlı ikili dosyaları gibi belirli işletim sistemi kodu içeren bir isteğe bağlı klasördür.</span><span class="sxs-lookup"><span data-stu-id="520b7-152">`runtimes` is an optional folder that contains OS specific code, such as CPU architecture and OS specific or otherwise platform-dependent binaries.</span></span> |

## <a name="msbuild-targets-and-props-files-in-packages"></a><span data-ttu-id="520b7-153">MSBuild hedefleri ve özellik dosyalarını paketler</span><span class="sxs-lookup"><span data-stu-id="520b7-153">MSBuild targets and props files in packages</span></span>

<span data-ttu-id="520b7-154">NuGet paketlerini içerebilir `.targets` ve `.props` paket içine yüklenir herhangi MSBuild proje içeri aktarılan dosyalar.</span><span class="sxs-lookup"><span data-stu-id="520b7-154">NuGet packages can contain `.targets` and `.props` files which are imported into any MSBuild project that the package is installed into.</span></span> <span data-ttu-id="520b7-155">NuGet içinde 2.x, bu yapıldı ekleyerek `<Import>` deyimleri `.csproj` dosya, NuGet 3. 0'belirli "projesine yükleme" eylemi yok.</span><span class="sxs-lookup"><span data-stu-id="520b7-155">In NuGet 2.x, this was done by injecting `<Import>` statements into the `.csproj` file, in NuGet 3.0 there is no specific "installation to project" action.</span></span> <span data-ttu-id="520b7-156">Bunun yerine paket geri yükleme işlemi iki dosya Yazar `[projectname].nuget.props` ve `[projectname].NuGet.targets`.</span><span class="sxs-lookup"><span data-stu-id="520b7-156">Instead the package restore process writes two files `[projectname].nuget.props` and `[projectname].NuGet.targets`.</span></span>

<span data-ttu-id="520b7-157">MSBuild için bu iki dosyayı aramak için bilir ve başına yakın ve proje oluşturma işlemi sona otomatik olarak alır.</span><span class="sxs-lookup"><span data-stu-id="520b7-157">MSBuild knows to look for these two files and automatically imports them near the beginning and near the end of the project build process.</span></span> <span data-ttu-id="520b7-158">Bu Nuget'e çok benzer bir davranış sağlar 2.x, ancak temel farklardan biri ile: *var. hedefler/özellik dosyaları yok garantili sırası bu durumda*.</span><span class="sxs-lookup"><span data-stu-id="520b7-158">This provides very similar behavior to NuGet 2.x, but with one major difference: *there is no guaranteed order of targets/props files in this case*.</span></span> <span data-ttu-id="520b7-159">MSBuild yolu sipariş hedefleri ancak sunar `BeforeTargets` ve `AfterTargets` özniteliklerini `<Target>` tanımı (bkz [hedef öğesi (MSBuild)](/visualstudio/msbuild/target-element-msbuild).</span><span class="sxs-lookup"><span data-stu-id="520b7-159">However, MSBuild does provide ways to order targets through the `BeforeTargets` and `AfterTargets` attributes of the `<Target>` definition (see [Target Element (MSBuild)](/visualstudio/msbuild/target-element-msbuild).</span></span>

## <a name="lib-and-ref"></a><span data-ttu-id="520b7-160">LIB ve Ref</span><span class="sxs-lookup"><span data-stu-id="520b7-160">Lib and Ref</span></span>

<span data-ttu-id="520b7-161">Davranışını `lib` klasörü kurmadı değiştirilen önemli ölçüde NuGet v3.</span><span class="sxs-lookup"><span data-stu-id="520b7-161">The behavior of the `lib` folder hasn't changed significantly in NuGet v3.</span></span> <span data-ttu-id="520b7-162">Ancak, tüm derlemelerde bir TxM sonra adlı alt klasörler içinde olmalıdır ve artık doğrudan altında yerleştirilebilir `lib` klasör.</span><span class="sxs-lookup"><span data-stu-id="520b7-162">However, all assemblies must be within sub-folders named after a TxM, and can no longer be placed directly under the `lib` folder.</span></span> <span data-ttu-id="520b7-163">Bir TxM bir paketteki belirli bir varlık için iş gerektiği bir platform adıdır.</span><span class="sxs-lookup"><span data-stu-id="520b7-163">A TxM is the name of a platform that a given asset in a package is supposed to work for.</span></span> <span data-ttu-id="520b7-164">Mantıksal bir uzantı hedef Framework adlar (TFM) Örneğin bunlar `net45`, `net46`, `netcore50`, ve `dnxcore50` TxMs tüm örnekleri (bkz [hedef çerçeveyi](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="520b7-164">Logically these are an extension of the Target Framework Monikers (TFM) e.g. `net45`, `net46`, `netcore50`, and `dnxcore50` are all examples of TxMs (see [Target Frameworks](../reference/target-frameworks.md).</span></span> <span data-ttu-id="520b7-165">TxM bir çerçeve (TFM) yanı sıra diğer platforma özgü yüzey alanlara başvurabilir.</span><span class="sxs-lookup"><span data-stu-id="520b7-165">TxM can refer to a framework (TFM) as well as other platform-specific surface areas.</span></span> <span data-ttu-id="520b7-166">Örneğin UWP TxM (`uap10.0`) UWP uygulamaları Windows yüzey alanını yanı sıra .NET yüzey alanını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="520b7-166">For example the UWP TxM (`uap10.0`) represents the .NET surface area as well as the Windows surface area for UWP applications.</span></span>

<span data-ttu-id="520b7-167">Bir örnek lib yapısı:</span><span class="sxs-lookup"><span data-stu-id="520b7-167">An example lib structure:</span></span>

    lib
    ├───net40
    │       MyLibrary.dll
    └───wp81
            MyLibrary.dll

<span data-ttu-id="520b7-168">`lib` Klasörü çalışma zamanında kullanılan derlemelerini içerir.</span><span class="sxs-lookup"><span data-stu-id="520b7-168">The `lib` folder contains assemblies that are used at runtime.</span></span> <span data-ttu-id="520b7-169">Çoğu için paketler altında bir klasör `lib` her hedef TxMs gerekli olan tüm için.</span><span class="sxs-lookup"><span data-stu-id="520b7-169">For most packages a folder under `lib` for each of the target TxMs is all that is required.</span></span>

## <a name="ref"></a><span data-ttu-id="520b7-170">Ref</span><span class="sxs-lookup"><span data-stu-id="520b7-170">Ref</span></span>

<span data-ttu-id="520b7-171">Bazı durumlarda farklı bir derleme (.NET başvuru derlemeleri do bu Bugün) derleme sırasında nerede kullanılması gereken durumlar vardır.</span><span class="sxs-lookup"><span data-stu-id="520b7-171">There are sometimes cases where a different assembly should be used during compilation (.NET Reference Assemblies do this today).</span></span> <span data-ttu-id="520b7-172">Bu gibi durumlarda adlı bir üst düzey klasör kullanmak `ref` (kısaltması "başvuru derlemeleri").</span><span class="sxs-lookup"><span data-stu-id="520b7-172">For those cases, use a top-level folder called `ref` (short for "Reference Assemblies").</span></span>

<span data-ttu-id="520b7-173">Çoğu paketi yazarları gerektirmeyen `ref` klasör.</span><span class="sxs-lookup"><span data-stu-id="520b7-173">Most package authors don't require the `ref` folder.</span></span> <span data-ttu-id="520b7-174">Derleme ve IntelliSense için tutarlı bir yüzey alanını sağlar ancak farklı TxMs için farklı uygulama olması gereken paketleri için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="520b7-174">It is useful for packages that need to provide a consistent surface area for compilation and IntelliSense but then have different implementation for different TxMs.</span></span> <span data-ttu-id="520b7-175">Bu öğeler büyük kullanım örneği `System.*` sevkiyat .NET Core NuGet üzerinde bir parçası olarak oluşturulan paketler.</span><span class="sxs-lookup"><span data-stu-id="520b7-175">The biggest use case of this are the `System.*` packages that are being produced as part of shipping .NET Core on NuGet.</span></span> <span data-ttu-id="520b7-176">Bu paketleri ref derlemelerin tutarlı bir kümesini birleşik çeşitli uygulamaları sahiptir.</span><span class="sxs-lookup"><span data-stu-id="520b7-176">These packages have various implementations that are being unified by a consistent set of ref assemblies.</span></span>

<span data-ttu-id="520b7-177">Derlemeleri mekanik olarak, dahil `ref` klasöründe derleyiciye geçirilen başvuru derlemeleri alır.</span><span class="sxs-lookup"><span data-stu-id="520b7-177">Mechanically, the assemblies included in the `ref` folder are the reference assemblies being passed to the compiler.</span></span> <span data-ttu-id="520b7-178">Biz geçirme için derlemeler için olanlar csc.exe kullanmış olduğunuz bunlar [C# / Reference seçeneği](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) geçin.</span><span class="sxs-lookup"><span data-stu-id="520b7-178">For those of you who have used csc.exe these are the assemblies we are passing to the [C# /reference option](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) switch.</span></span>

<span data-ttu-id="520b7-179">Yapısını `ref` klasördür aynı `lib`, örneğin:</span><span class="sxs-lookup"><span data-stu-id="520b7-179">The structure of the `ref` folder is the same as `lib`, for example:</span></span>

    └───MyImageProcessingLib
         ├───lib
         │   ├───net40
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   ├───net451
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   └───win81
         │           MyImageProcessingLibrary.dll
         │
         └───ref
             ├───net40
             │       MyImageProcessingLibrary.dll
             │
             └───portable-net451-win81
                     MyImageProcessingLibrary.dll

<span data-ttu-id="520b7-180">Bu örnekte derlemelerde `ref` dizinler tüm olacaktır aynı.</span><span class="sxs-lookup"><span data-stu-id="520b7-180">In this example the assemblies in the `ref` directories would all be identical.</span></span>

## <a name="runtimes"></a><span data-ttu-id="520b7-181">Çalışma zamanları</span><span class="sxs-lookup"><span data-stu-id="520b7-181">Runtimes</span></span>

<span data-ttu-id="520b7-182">Çalışma zamanları klasör derlemeler ve "işletim sistemi ve CPU mimarisine göre genellikle tanımlanmış olan belirli çalışma zamanları", üzerinde çalıştırmak için gerekli yerel kitaplıkları içerir.</span><span class="sxs-lookup"><span data-stu-id="520b7-182">The runtimes folder contains assemblies and native libraries required to run on specific "runtimes", which are generally defined by Operating System and CPU architecture.</span></span> <span data-ttu-id="520b7-183">Bu çalışma zamanları kullanılarak tanımlanır [çalışma zamanı tanımlayıcıları (RID)](/dotnet/core/rid-catalog) gibi `win`, `win-x86`, `win7-x86`, `win8-64`vb.</span><span class="sxs-lookup"><span data-stu-id="520b7-183">These runtimes are identified using [Runtime Identifiers (RIDs)](/dotnet/core/rid-catalog) such as `win`, `win-x86`, `win7-x86`, `win8-64`, etc.</span></span>

## <a name="native-helpers-to-use-platform-specific-apis"></a><span data-ttu-id="520b7-184">Platforma özgü API'ları kullanmak için yerel Yardımcıları</span><span class="sxs-lookup"><span data-stu-id="520b7-184">Native helpers to use platform-specific APIs</span></span>

<span data-ttu-id="520b7-185">Aşağıdaki örnek, çeşitli platformlar için tamamen yönetilen bir uygulama olsa da, Windows 8'i Windows 8 özgü yerel API burada çağırabilirsiniz yerel Yardımcıları kullanan bir paket gösterir.</span><span class="sxs-lookup"><span data-stu-id="520b7-185">The following example shows a package that has a purely managed implementation for several platforms, but uses native helpers on Windows 8 where it can call into Windows 8-specific native APIs.</span></span>

    └───MyLibrary
         ├───lib
         │   └───net40
         │           MyLibrary.dll
         │
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net40
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyNativeLibrary.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net40
                 │           MyLibrary.dll
                 │
                 └───native
                         MyNativeLibrary.dll

<span data-ttu-id="520b7-186">Yukarıdaki paket aşağıdakiler gerçekleşir:</span><span class="sxs-lookup"><span data-stu-id="520b7-186">Given the above package the following things happen:</span></span>

- <span data-ttu-id="520b7-187">Windows 8'deki ne zaman `lib/net40/MyLibrary.dll` derleme kullanılır.</span><span class="sxs-lookup"><span data-stu-id="520b7-187">When not on Windows 8 the `lib/net40/MyLibrary.dll` assembly is used.</span></span>

- <span data-ttu-id="520b7-188">Windows 8 ne zaman `runtimes/win8-<architecture>/lib/MyLibrary.dll` kullanılır ve `native/MyNativeHelper.dll` yapınızın çıkışına kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="520b7-188">When on Windows 8 the `runtimes/win8-<architecture>/lib/MyLibrary.dll` is used and the `native/MyNativeHelper.dll` is copied to the output of your build.</span></span>

<span data-ttu-id="520b7-189">Yukarıdaki örnekte `lib/net40` derlemedir tamamen yönetilen kod, Windows 8 özel API'leri çağırmak için yerel Yardımcısı derlemesini p/Invoke çalışma zamanları klasörü derlemelerde olacak adımında.</span><span class="sxs-lookup"><span data-stu-id="520b7-189">In the example above the `lib/net40` assembly is purely managed code, whilst the assemblies in the runtimes folder will p/invoke into the native helper assembly to call APIs specific to Windows 8.</span></span>

<span data-ttu-id="520b7-190">Yalnızca tek bir `lib` klasör olan herhangi bir zamanda olması Çekildi, çalışma zamanı belirli bir klasörde ise çalışma zamanı olmayan özel seçilir şekilde `lib`.</span><span class="sxs-lookup"><span data-stu-id="520b7-190">Only a single `lib` folder is ever be picked, so if there is a runtime specific folder it's chosen over non-runtime specific `lib`.</span></span> <span data-ttu-id="520b7-191">Yerel klasör, varsa ADDITIVE yapı çıkışına kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="520b7-191">The native folder is additive, if it exists it's copied to the output of the build.</span></span>

## <a name="managed-wrapper"></a><span data-ttu-id="520b7-192">Yönetilen sarmalayıcı</span><span class="sxs-lookup"><span data-stu-id="520b7-192">Managed wrapper</span></span>

<span data-ttu-id="520b7-193">Çalışma zamanları kullanmak için başka bir yerel derleme tamamen yönetilen sarmalayıcı bir paket dağıtmayı yoludur.</span><span class="sxs-lookup"><span data-stu-id="520b7-193">Another way to use runtimes is to ship a package that is purely a managed wrapper over a native assembly.</span></span> <span data-ttu-id="520b7-194">Bu senaryoda aşağıdaki gibi bir paket oluşturun:</span><span class="sxs-lookup"><span data-stu-id="520b7-194">In this scenario you create a package like the following:</span></span>

    └───MyLibrary
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net451
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyImplementation.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net451
                 │           MyLibrary.dll
                 │
                 └───native
                         MyImplementation.dll

<span data-ttu-id="520b7-195">Bu durumda olduğundan en üst düzey `lib` klasördür orada olarak bu klasör olarak hiçbir uygulama karşılık gelen yerel derleme üzerinde kullanmaz bu paketi.</span><span class="sxs-lookup"><span data-stu-id="520b7-195">In this case there is no top-level `lib` folder as that folder as there is no implementation of this package that doesn't rely on the corresponding native assembly.</span></span> <span data-ttu-id="520b7-196">Yönetilen derleme `MyLibrary.dll`, biz bu bir üst düzey koyabilirsiniz sonra tam olarak her iki durumda aynı olan `lib` klasörü, ancak yerel derleme eksikliği paket bir platformda yüklenmişse, yükleme başarısız olmasına neden değil, Win-x86 veya win x64 en üst düzey lib kullanılır, ancak yerel derleme kopyalanır sonra değildi.</span><span class="sxs-lookup"><span data-stu-id="520b7-196">If the managed assembly, `MyLibrary.dll`, was exactly the same in both of these cases then we could put it in a top level `lib` folder, but because the lack of a native assembly doesn't cause the package to fail installing if it was installed on a platform that wasn't win-x86 or win-x64 then the top level lib would be used but no native assembly would be copied.</span></span>

## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a><span data-ttu-id="520b7-197">NuGet 2 ve 3 NuGet paketleri yazma</span><span class="sxs-lookup"><span data-stu-id="520b7-197">Authoring packages for NuGet 2 and NuGet 3</span></span>

<span data-ttu-id="520b7-198">Kullanarak projeleri tarafından kullanılabilecek bir paket oluşturmak isteyip istemediğinizi `packages.config` de olarak paketleri kullanarak `project.json` sonra aşağıdaki Uygula:</span><span class="sxs-lookup"><span data-stu-id="520b7-198">If you want to create a package that can be consumed by projects using `packages.config` as well as packages using `project.json` then the following apply:</span></span>

- <span data-ttu-id="520b7-199">Ref ve çalışma zamanları yalnızca NuGet 3'te çalışır.</span><span class="sxs-lookup"><span data-stu-id="520b7-199">Ref and runtimes only work on NuGet 3.</span></span> <span data-ttu-id="520b7-200">NuGet 2 ile hem de yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="520b7-200">They are both ignored by NuGet 2.</span></span>

- <span data-ttu-id="520b7-201">Bağlı olamaz `install.ps1` veya `uninstall.ps1` işlevi.</span><span class="sxs-lookup"><span data-stu-id="520b7-201">You cannot rely on `install.ps1` or `uninstall.ps1` to function.</span></span> <span data-ttu-id="520b7-202">Bu dosyaları kullanırken yürütme `packages.config`, ile göz ardı edilir, ancak `project.json`.</span><span class="sxs-lookup"><span data-stu-id="520b7-202">These files execute when using `packages.config`, but are ignored with `project.json`.</span></span> <span data-ttu-id="520b7-203">Paketinizi onlar olmadan kullanılabilir olması gereken şekilde çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="520b7-203">So your package needs to be usable without them running.</span></span> <span data-ttu-id="520b7-204">`init.ps1` hala NuGet 3'te çalışır.</span><span class="sxs-lookup"><span data-stu-id="520b7-204">`init.ps1` still runs on NuGet 3.</span></span>

- <span data-ttu-id="520b7-205">Hedefleri ve özellik yükleme farklıdır, bu nedenle paketinizi hem de istemcilerde beklendiği gibi çalıştığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="520b7-205">Targets and Props installation is different, so make sure that your package works as expected on both clients.</span></span>

- <span data-ttu-id="520b7-206">LIB alt dizinleri TxM NuGet 3 olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="520b7-206">Subdirectories of lib must be a TxM in NuGet 3.</span></span> <span data-ttu-id="520b7-207">Kitaplıkları kökünde yerleştirilemiyor `lib` klasör.</span><span class="sxs-lookup"><span data-stu-id="520b7-207">You cannot place libraries at the root of the `lib` folder.</span></span>

- <span data-ttu-id="520b7-208">İçerik NuGet 3 ile otomatik olarak kopyalanmaz.</span><span class="sxs-lookup"><span data-stu-id="520b7-208">Content is not copied automatically with NuGet 3.</span></span> <span data-ttu-id="520b7-209">Tüketiciler, paketi, dosyaları kendileri kopyalama veya dosyaları kopyalanıyor otomatikleştirmek için görev Çalıştırıcı gibi bir araç kullanın.</span><span class="sxs-lookup"><span data-stu-id="520b7-209">Consumers of your package could copy the files themselves or use a tool like a task runner to automate copying the files.</span></span>

- <span data-ttu-id="520b7-210">Kaynak ve yapılandırma dosyası dönüşümler NuGet 3 ile çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="520b7-210">Source and config file transforms are not run by NuGet 3.</span></span>

<span data-ttu-id="520b7-211">NuGet 2 ve 3 destekleniyorsa sonra `minClientVersion` paketinizi çalışır NuGet 2 istemci en düşük sürümü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="520b7-211">If you are supporting NuGet 2 and 3 then your `minClientVersion` should be the lowest version of NuGet 2 client that your package works on.</span></span> <span data-ttu-id="520b7-212">Var olan bir paket olması durumunda onu değiştirmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="520b7-212">In the case of an existing package it shouldn't need to change.</span></span>
