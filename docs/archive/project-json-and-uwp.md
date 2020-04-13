---
title: UWP projeleri ile NuGet project.json dosyası
description: Universal Windows Platform (UWP) projelerindeki NuGet bağımlılıklarını izlemek için project.json dosyasının nasıl kullanıldığının açıklaması.
author: karann-msft
ms.author: karann
ms.date: 07/17/2017
ms.topic: conceptual
ms.openlocfilehash: ac3c137dd0ba50571737093eef11c8ab0ef932b2
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64494365"
---
# <a name="projectjson-and-uwp"></a><span data-ttu-id="35c82-103">project.json ve UWP</span><span class="sxs-lookup"><span data-stu-id="35c82-103">project.json and UWP</span></span>

> [!Important]
> <span data-ttu-id="35c82-104">Bu içerik amortismana hazırdır.</span><span class="sxs-lookup"><span data-stu-id="35c82-104">This content is deprecated.</span></span> <span data-ttu-id="35c82-105">Projeler `packages.config` de PackageReference biçimlerini kullanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="35c82-105">Projects should use either the `packages.config` or PackageReference formats.</span></span>

<span data-ttu-id="35c82-106">Bu belge, NuGet 3+ (Visual Studio 2015 ve sonrası) özellikleri kullanan paket yapısını açıklar.</span><span class="sxs-lookup"><span data-stu-id="35c82-106">This document describes the package structure that employs features in NuGet 3+ (Visual Studio 2015 and later).</span></span> <span data-ttu-id="35c82-107">Özelliğiniz, `minClientVersion` `.nuspec` burada açıklanan özelliklere 3.1 olarak ayarlayarak ihtiyaç duyduğunuzu belirtmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="35c82-107">The `minClientVersion` property of your `.nuspec` can be used to state that you require the features described here by setting it to 3.1.</span></span>

## <a name="adding-uwp-support-to-an-existing-package"></a><span data-ttu-id="35c82-108">Varolan bir pakete UWP desteği ekleme</span><span class="sxs-lookup"><span data-stu-id="35c82-108">Adding UWP support to an existing package</span></span>

<span data-ttu-id="35c82-109">Varolan bir paketiniz varsa ve UWP uygulamaları için destek eklemek istiyorsanız, burada açıklanan ambalaj biçimini benimsemeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="35c82-109">If you have an existing package and you want to add support for UWP applications, then you don’t need to adopt the  packaging format described here.</span></span> <span data-ttu-id="35c82-110">Yalnızca açıkladığı özelliklere ihtiyaç duyuyorsanız ve yalnızca NuGet istemcisinin sürüm 3+ sürümüne güncelleştirilmiş istemcilerle çalışmak istiyorsanız bu biçimi benimsemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="35c82-110">You only need to adopt this format if you require the features it describes and are willing to  work only with clients that have updated to version 3+ of the NuGet client.</span></span>

## <a name="i-already-target-netcore45"></a><span data-ttu-id="35c82-111">Zaten netcore45 hedef</span><span class="sxs-lookup"><span data-stu-id="35c82-111">I already target netcore45</span></span>

<span data-ttu-id="35c82-112">Zaten hedef `netcore45` alırsanız ve buradaki özelliklerden yararlanmanız gerekmiyorsa, herhangi bir işlem yapmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="35c82-112">If you target `netcore45` already, and you don’t need to take advantage of the features here, no action is needed.</span></span> <span data-ttu-id="35c82-113">`netcore45`paketleri UWP uygulamaları tarafından tüketilebilir.</span><span class="sxs-lookup"><span data-stu-id="35c82-113">`netcore45` packages can be consumed by UWP applications.</span></span>

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a><span data-ttu-id="35c82-114">Windows 10'a özgü API'lerden yararlanmak istiyorum</span><span class="sxs-lookup"><span data-stu-id="35c82-114">I want to take advantage of Windows 10 specific APIs</span></span>

<span data-ttu-id="35c82-115">Bu durumda, hedef çerçeve `uap10.0` takma aparatı (TFM veya TxM) paketinize eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="35c82-115">In this case you need to add the `uap10.0` target framework moniker (TFM or TxM) to your package.</span></span> <span data-ttu-id="35c82-116">Paketinizde yeni bir klasör oluşturun ve Windows 10 ile çalışmak üzere derlenen derlemeyi bu klasöre ekleyin.</span><span class="sxs-lookup"><span data-stu-id="35c82-116">Create a new folder in your package and add the assembly that has been compiled to work with Windows 10 to that folder.</span></span>

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a><span data-ttu-id="35c82-117">Windows 10 özel API'ler gerekmez, ama yeni .NET özellikleri istiyorum ya da netcore45 zaten yok</span><span class="sxs-lookup"><span data-stu-id="35c82-117">I don’t need Windows 10 specific APIs, but want new .NET features or don’t have netcore45 already</span></span>

<span data-ttu-id="35c82-118">Bu durumda, TxM'yi `dotnet` paketinize eklersiniz.</span><span class="sxs-lookup"><span data-stu-id="35c82-118">In this case you would add the `dotnet` TxM to your package.</span></span> <span data-ttu-id="35c82-119">Diğer TxM'lerden farklı olarak, `dotnet` bir yüzey alanı veya platform anlamına gelmez.</span><span class="sxs-lookup"><span data-stu-id="35c82-119">Unlike other TxMs, `dotnet` doesn't imply a surface area or platform.</span></span> <span data-ttu-id="35c82-120">Paketinizin bağımlılıklarınızın üzerinde çalıştığı herhangi bir platformda çalıştığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="35c82-120">It is stating that your package works on any platform that your dependencies work on.</span></span> <span data-ttu-id="35c82-121">`dotnet` TxM ile bir paket inşa ederken, size bağlı BCL paketleri tanımlamak `.nuspec`için gereken gibi, çok daha fazla TxM özgü bağımlılıkları olması muhtemeldir, vb. `System.Text` `System.Xml` Bu bağımlılıkların üzerinde çalıştığı konumlar paketinizin nerede çalıştığını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="35c82-121">When building a package with the `dotnet` TxM, you are likely to have many more TxM-specific dependencies in your `.nuspec`, as you need to define the BCL packages you depend on, such `System.Text`, `System.Xml`, etc. The locations that those dependencies work on define where your package works.</span></span>

### <a name="how-do-i-find-out-my-dependencies"></a><span data-ttu-id="35c82-122">Bağımlılıklarımı nasıl öğrenebilirim?</span><span class="sxs-lookup"><span data-stu-id="35c82-122">How do I find out my dependencies</span></span>

<span data-ttu-id="35c82-123">Hangi bağımlılıkların listelenemeye ne kadar yol olduğunu anlamanın iki yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="35c82-123">There are two ways to figure out which dependencies to list:</span></span>

1. <span data-ttu-id="35c82-124">[NuSpec Bağımlılık Jeneratörü](https://github.com/onovotny/ReferenceGenerator) **3.**</span><span class="sxs-lookup"><span data-stu-id="35c82-124">Use the [NuSpec Dependency Generator](https://github.com/onovotny/ReferenceGenerator) **3rd party** tool.</span></span> <span data-ttu-id="35c82-125">Araç işlemi otomatikleştirir ve `.nuspec` dosyanızı yapıdaki bağımlı paketlerle güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="35c82-125">The tool automates the process and updates your `.nuspec` file with the dependant packages on build.</span></span> <span data-ttu-id="35c82-126">Bir NuGet paketi, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/)üzerinden kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="35c82-126">It is available via a NuGet package, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).</span></span>

1. <span data-ttu-id="35c82-127">(Zor yol) Çalışma `ILDasm` zamanında hangi `.dll` derlemelerin gerçekten gerekli olduğunu görmek için bakmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="35c82-127">(The hard way) Use `ILDasm` to look at your `.dll` to see what assemblies are actually needed at runtime.</span></span> <span data-ttu-id="35c82-128">Ardından, her birinin hangi NuGet paketinden geldiğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="35c82-128">Then determine which NuGet package they each come from.</span></span>

<span data-ttu-id="35c82-129">TxM'yi destekleyen bir paketin oluşturulmasına yardımcı olan özellikler le ilgili ayrıntılar için [`project.json`](project-json.md) konuya bakın. `dotnet`</span><span class="sxs-lookup"><span data-stu-id="35c82-129">See the [`project.json`](project-json.md) topic for details on features that help in the creation of a package that supports the `dotnet` TxM.</span></span>

> [!Important]
> <span data-ttu-id="35c82-130">Paketiniz PCL projeleri ile çalışmak üzere tasarlanmıştırsa, `dotnet` uyarılardan ve olası uyumluluk sorunlarını önlemek için bir klasör oluşturmanızı şiddetle öneririz.</span><span class="sxs-lookup"><span data-stu-id="35c82-130">If your package is intended to work with PCL projects, we highly recommend to create a `dotnet` folder, to avoid warnings and potential compatibility issues.</span></span>

## <a name="directory-structure"></a><span data-ttu-id="35c82-131">Dizin yapısı</span><span class="sxs-lookup"><span data-stu-id="35c82-131">Directory structure</span></span>

<span data-ttu-id="35c82-132">Bu biçimi kullanan NuGet paketleri aşağıdaki iyi bilinen klasöre ve davranışlara sahiptir:</span><span class="sxs-lookup"><span data-stu-id="35c82-132">NuGet packages using this format have the following well-known folder and behaviors:</span></span>

| <span data-ttu-id="35c82-133">Klasör</span><span class="sxs-lookup"><span data-stu-id="35c82-133">Folder</span></span> | <span data-ttu-id="35c82-134">Davranışlar</span><span class="sxs-lookup"><span data-stu-id="35c82-134">Behaviors</span></span> |
| --- | --- |
| <span data-ttu-id="35c82-135">Yapı</span><span class="sxs-lookup"><span data-stu-id="35c82-135">Build</span></span> | <span data-ttu-id="35c82-136">Bu klasördeki MSBuild hedefleri ve sahne dosyaları projeye farklı olarak entegre edilmiştir, ancak aksi takdirde değişiklik yoktur.</span><span class="sxs-lookup"><span data-stu-id="35c82-136">Contains MSBuild targets and props files in this folder are integrated differently into the project, but otherwise there is no change.</span></span> |
| <span data-ttu-id="35c82-137">Araçlar</span><span class="sxs-lookup"><span data-stu-id="35c82-137">Tools</span></span> | <span data-ttu-id="35c82-138">`install.ps1`ve `uninstall.ps1` çalıştırılmayız.</span><span class="sxs-lookup"><span data-stu-id="35c82-138">`install.ps1` and `uninstall.ps1` are not run.</span></span> <span data-ttu-id="35c82-139">`init.ps1`her zaman olduğu gibi çalışır.</span><span class="sxs-lookup"><span data-stu-id="35c82-139">`init.ps1` works as it always has.</span></span> |
| <span data-ttu-id="35c82-140">İçerik</span><span class="sxs-lookup"><span data-stu-id="35c82-140">Content</span></span> | <span data-ttu-id="35c82-141">İçerik otomatik olarak kullanıcının projesine kopyalanmaz.</span><span class="sxs-lookup"><span data-stu-id="35c82-141">Content is not copied automatically into a user's project.</span></span> <span data-ttu-id="35c82-142">Projeye içerik ekleme desteğinin daha sonra yayınlanması planlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="35c82-142">Support for content inclusion in the project is planned for a later release.</span></span> |
| <span data-ttu-id="35c82-143">Lib</span><span class="sxs-lookup"><span data-stu-id="35c82-143">Lib</span></span> | <span data-ttu-id="35c82-144">Birçok paket `lib` için NuGet 2.x'te olduğu gibi çalışır, ancak içinde hangi adların kullanılabileceğinin genişletilmiş seçenekleri ve paketleri tüketirken doğru alt klasörü seçmek için daha iyi bir mantık la çalışır.</span><span class="sxs-lookup"><span data-stu-id="35c82-144">For many packages the `lib` works the same way it does in NuGet 2.x, but with expanded options for what names can be used inside it and better logic for picking the correct sub-folder when consuming packages.</span></span> <span data-ttu-id="35c82-145">Ancak, klasör ile `ref`birlikte `lib` kullanıldığında, `ref` klasör klasördeki derlemeler tarafından tanımlanan yüzey alanını uygulayan derlemeler içerir.</span><span class="sxs-lookup"><span data-stu-id="35c82-145">However, when used in conjunction with `ref`, the `lib` folder contains assemblies that implement the surface area defined by the assemblies in the `ref` folder.</span></span> |
| <span data-ttu-id="35c82-146">Referans</span><span class="sxs-lookup"><span data-stu-id="35c82-146">Ref</span></span> | <span data-ttu-id="35c82-147">`ref`karşı derlemek için bir uygulama için ortak yüzeyi (genel türleri ve yöntemleri) tanımlayan .NET derlemeleri içeren isteğe bağlı bir klasördür.</span><span class="sxs-lookup"><span data-stu-id="35c82-147">`ref` is an optional folder that contains .NET assemblies defining the public surface (public types and methods) for an application to compile against.</span></span> <span data-ttu-id="35c82-148">Bu klasördeki derlemeler hiçbir uygulama olabilir, onlar tamamen derleyici için yüzey alanı tanımlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="35c82-148">The assemblies in this folder may have no implementation, they are purely used to define surface area for the compiler.</span></span> <span data-ttu-id="35c82-149">Paketin klasörü `ref` yoksa, hem `lib` başvuru derlemesi hem de uygulama derlemesi olur.</span><span class="sxs-lookup"><span data-stu-id="35c82-149">If the package has no `ref` folder, then the `lib` is both the reference assembly and the implementation assembly.</span></span> |
| <span data-ttu-id="35c82-150">Çalıştırma</span><span class="sxs-lookup"><span data-stu-id="35c82-150">Runtimes</span></span> | <span data-ttu-id="35c82-151">`runtimes`CPU mimarisi ve işletim sistemi belirli veya başka bir platforma bağımlı ikililer gibi işletim sistemi özgü kodu içeren isteğe bağlı bir klasördür.</span><span class="sxs-lookup"><span data-stu-id="35c82-151">`runtimes` is an optional folder that contains OS specific code, such as CPU architecture and OS specific or otherwise platform-dependent binaries.</span></span> |

## <a name="msbuild-targets-and-props-files-in-packages"></a><span data-ttu-id="35c82-152">MSBuild dosyaları paketler halinde hedefler ve sahne</span><span class="sxs-lookup"><span data-stu-id="35c82-152">MSBuild targets and props files in packages</span></span>

<span data-ttu-id="35c82-153">NuGet paketleri, `.targets` `.props` paketin yüklü olduğu herhangi bir MSBuild projesine içe aktarılan dosyaları ve dosyaları içerebilir.</span><span class="sxs-lookup"><span data-stu-id="35c82-153">NuGet packages can contain `.targets` and `.props` files which are imported into any MSBuild project that the package is installed into.</span></span> <span data-ttu-id="35c82-154">NuGet 2.x'te bu durum `<Import>` dosyaya `.csproj` ekstreler enjekte edilerek yapıldı, NuGet 3.0'da belirli bir "projeye yükleme" eylemi yoktur.</span><span class="sxs-lookup"><span data-stu-id="35c82-154">In NuGet 2.x, this was done by injecting `<Import>` statements into the `.csproj` file, in NuGet 3.0 there is no specific "installation to project" action.</span></span> <span data-ttu-id="35c82-155">Bunun yerine paket geri `[projectname].nuget.props` yükleme `[projectname].NuGet.targets`işlemi iki dosya yazar ve .</span><span class="sxs-lookup"><span data-stu-id="35c82-155">Instead the package restore process writes two files `[projectname].nuget.props` and `[projectname].NuGet.targets`.</span></span>

<span data-ttu-id="35c82-156">MSBuild bu iki dosyayı aramayı ve bunları proje oluşturma sürecinin başlangıcına ve sonuna yakın otomatik olarak içe aktarmayı bilir.</span><span class="sxs-lookup"><span data-stu-id="35c82-156">MSBuild knows to look for these two files and automatically imports them near the beginning and near the end of the project build process.</span></span> <span data-ttu-id="35c82-157">Bu NuGet 2.x çok benzer bir davranış sağlar, ancak büyük bir fark ile: *Bu durumda hedef / sahne dosyaları nın garantili bir sırası yoktur.*</span><span class="sxs-lookup"><span data-stu-id="35c82-157">This provides very similar behavior to NuGet 2.x, but with one major difference: *there is no guaranteed order of targets/props files in this case*.</span></span> <span data-ttu-id="35c82-158">Ancak, `BeforeTargets` MSBuild `AfterTargets` `<Target>` tanımı ve öznitelikleri ile hedefleri sipariş etmek için yollar sağlar [(Bkz. Hedef Öğesi (MSBuild)](/visualstudio/msbuild/target-element-msbuild).</span><span class="sxs-lookup"><span data-stu-id="35c82-158">However, MSBuild does provide ways to order targets through the `BeforeTargets` and `AfterTargets` attributes of the `<Target>` definition (see [Target Element (MSBuild)](/visualstudio/msbuild/target-element-msbuild).</span></span>

## <a name="lib-and-ref"></a><span data-ttu-id="35c82-159">Lib ve Ref</span><span class="sxs-lookup"><span data-stu-id="35c82-159">Lib and Ref</span></span>

<span data-ttu-id="35c82-160">NuGet v3'te klasörün `lib` davranışı önemli ölçüde değişmedi.</span><span class="sxs-lookup"><span data-stu-id="35c82-160">The behavior of the `lib` folder hasn't changed significantly in NuGet v3.</span></span> <span data-ttu-id="35c82-161">Ancak, tüm derlemeler TxM'den sonra adlandırılan alt klasörlerde olmalıdır ve artık `lib` doğrudan klasörün altına yerleştirilememelidir.</span><span class="sxs-lookup"><span data-stu-id="35c82-161">However, all assemblies must be within sub-folders named after a TxM, and can no longer be placed directly under the `lib` folder.</span></span> <span data-ttu-id="35c82-162">TxM, paketteki belirli bir varlığın çalışması gereken bir platformun adıdır.</span><span class="sxs-lookup"><span data-stu-id="35c82-162">A TxM is the name of a platform that a given asset in a package is supposed to work for.</span></span> <span data-ttu-id="35c82-163">Mantıksal olarak bunlar Hedef Çerçeve Monikers 'in (TFM) `net45` `net46`bir `netcore50`uzantısıdır, örneğin, , , ve `dnxcore50` Tüm TxM örnekleridir (Bkz. [Hedef Çerçeveler.](../reference/target-frameworks.md)</span><span class="sxs-lookup"><span data-stu-id="35c82-163">Logically these are an extension of the Target Framework Monikers (TFM) e.g. `net45`, `net46`, `netcore50`, and `dnxcore50` are all examples of TxMs (see [Target Frameworks](../reference/target-frameworks.md).</span></span> <span data-ttu-id="35c82-164">TxM bir çerçeve (TFM) yanı sıra diğer platforma özgü yüzey alanları başvurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="35c82-164">TxM can refer to a framework (TFM) as well as other platform-specific surface areas.</span></span> <span data-ttu-id="35c82-165">Örneğin UWP TxM`uap10.0`( ) UWP uygulamaları için Windows yüzey alanının yanı sıra .NET yüzey alanını da temsil eder.</span><span class="sxs-lookup"><span data-stu-id="35c82-165">For example the UWP TxM (`uap10.0`) represents the .NET surface area as well as the Windows surface area for UWP applications.</span></span>

<span data-ttu-id="35c82-166">Bir örnek lib yapısı:</span><span class="sxs-lookup"><span data-stu-id="35c82-166">An example lib structure:</span></span>

    lib
    ├───net40
    │       MyLibrary.dll
    └───wp81
            MyLibrary.dll

<span data-ttu-id="35c82-167">Klasör, `lib` çalışma zamanında kullanılan derlemeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="35c82-167">The `lib` folder contains assemblies that are used at runtime.</span></span> <span data-ttu-id="35c82-168">Çoğu paket için `lib` hedef TxM'lerin her biri için altında bir klasör gereklidir.</span><span class="sxs-lookup"><span data-stu-id="35c82-168">For most packages a folder under `lib` for each of the target TxMs is all that is required.</span></span>

## <a name="ref"></a><span data-ttu-id="35c82-169">Referans</span><span class="sxs-lookup"><span data-stu-id="35c82-169">Ref</span></span>

<span data-ttu-id="35c82-170">Derleme sırasında farklı bir derlemenin kullanılması gereken durumlar bazen vardır (.NET Başvuru Derlemeleri bunu bugün yapar).</span><span class="sxs-lookup"><span data-stu-id="35c82-170">There are sometimes cases where a different assembly should be used during compilation (.NET Reference Assemblies do this today).</span></span> <span data-ttu-id="35c82-171">Bu gibi durumlarda, ("Başvuru `ref` Derlemeleri"nin kısaltması) adlı üst düzey bir klasör kullanın.</span><span class="sxs-lookup"><span data-stu-id="35c82-171">For those cases, use a top-level folder called `ref` (short for "Reference Assemblies").</span></span>

<span data-ttu-id="35c82-172">Çoğu paket yazarı klasörü `ref` gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="35c82-172">Most package authors don't require the `ref` folder.</span></span> <span data-ttu-id="35c82-173">Derleme ve IntelliSense için tutarlı bir yüzey alanı sağlaması gereken ancak daha sonra farklı TxM'ler için farklı bir uygulamaya sahip paketler için yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="35c82-173">It is useful for packages that need to provide a consistent surface area for compilation and IntelliSense but then have different implementation for different TxMs.</span></span> <span data-ttu-id="35c82-174">Bunun en büyük kullanım `System.*` örneği NuGet'de .NET Core taşımacılığının bir parçası olarak üretilen paketlerdir.</span><span class="sxs-lookup"><span data-stu-id="35c82-174">The biggest use case of this are the `System.*` packages that are being produced as part of shipping .NET Core on NuGet.</span></span> <span data-ttu-id="35c82-175">Bu paketler, tutarlı bir ref derlemeleri kümesi tarafından birleştirilmiş olan çeşitli uygulamalara sahiptir.</span><span class="sxs-lookup"><span data-stu-id="35c82-175">These packages have various implementations that are being unified by a consistent set of ref assemblies.</span></span>

<span data-ttu-id="35c82-176">Mekanik olarak, `ref` klasörde yer alan derlemeler derleyiciye geçirilen başvuru derlemeleridir.</span><span class="sxs-lookup"><span data-stu-id="35c82-176">Mechanically, the assemblies included in the `ref` folder are the reference assemblies being passed to the compiler.</span></span> <span data-ttu-id="35c82-177">CSC.exe kullananlar için bunlar [C# /reference option](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) switch'e aktardığımız montajlardır.</span><span class="sxs-lookup"><span data-stu-id="35c82-177">For those of you who have used csc.exe these are the assemblies we are passing to the [C# /reference option](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) switch.</span></span>

<span data-ttu-id="35c82-178">Klasörün `ref` yapısı, örneğin aşağıdakiyle `lib`aynıdır:</span><span class="sxs-lookup"><span data-stu-id="35c82-178">The structure of the `ref` folder is the same as `lib`, for example:</span></span>

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

<span data-ttu-id="35c82-179">Bu örnekte dizinlerde `ref` derlemeler tüm özdeş olacaktır.</span><span class="sxs-lookup"><span data-stu-id="35c82-179">In this example the assemblies in the `ref` directories would all be identical.</span></span>

## <a name="runtimes"></a><span data-ttu-id="35c82-180">Çalıştırma</span><span class="sxs-lookup"><span data-stu-id="35c82-180">Runtimes</span></span>

<span data-ttu-id="35c82-181">Runtimes klasörü, genellikle İşletim Sistemi ve CPU mimarisi tarafından tanımlanan belirli "çalışma zamanlarında" çalışması için gereken derlemeleri ve yerel kitaplıkları içerir.</span><span class="sxs-lookup"><span data-stu-id="35c82-181">The runtimes folder contains assemblies and native libraries required to run on specific "runtimes", which are generally defined by Operating System and CPU architecture.</span></span> <span data-ttu-id="35c82-182">Bu çalışma süreleri [Runtime Tanımlayıcıları (RIDs)](/dotnet/core/rid-catalog) gibi `win`, `win-x86`, `win7-x86` `win8-64`, , vb kullanılarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="35c82-182">These runtimes are identified using [Runtime Identifiers (RIDs)](/dotnet/core/rid-catalog) such as `win`, `win-x86`, `win7-x86`, `win8-64`, etc.</span></span>

## <a name="native-helpers-to-use-platform-specific-apis"></a><span data-ttu-id="35c82-183">Platforma özgü API'leri kullanmak için yerel yardımcılar</span><span class="sxs-lookup"><span data-stu-id="35c82-183">Native helpers to use platform-specific APIs</span></span>

<span data-ttu-id="35c82-184">Aşağıdaki örnek, çeşitli platformlar için tamamen yönetilen bir uygulamaya sahip, ancak Windows 8'e özgü yerel API'leri arayabildiği Windows 8'de yerel yardımcıları kullanan bir paketi gösterir.</span><span class="sxs-lookup"><span data-stu-id="35c82-184">The following example shows a package that has a purely managed implementation for several platforms, but uses native helpers on Windows 8 where it can call into Windows 8-specific native APIs.</span></span>

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

<span data-ttu-id="35c82-185">Yukarıdaki paket göz önüne alındığında aşağıdaki şeyler olur:</span><span class="sxs-lookup"><span data-stu-id="35c82-185">Given the above package the following things happen:</span></span>

- <span data-ttu-id="35c82-186">Windows 8'de `lib/net40/MyLibrary.dll` olmadığında derleme kullanılır.</span><span class="sxs-lookup"><span data-stu-id="35c82-186">When not on Windows 8 the `lib/net40/MyLibrary.dll` assembly is used.</span></span>

- <span data-ttu-id="35c82-187">Windows 8'de `runtimes/win8-<architecture>/lib/MyLibrary.dll` kullanıldığında ve `native/MyNativeHelper.dll` yapınızın çıktısına kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="35c82-187">When on Windows 8 the `runtimes/win8-<architecture>/lib/MyLibrary.dll` is used and the `native/MyNativeHelper.dll` is copied to the output of your build.</span></span>

<span data-ttu-id="35c82-188">Yukarıdaki örnekte `lib/net40` derleme tamamen yönetilen kod iken, runtimes klasöründeki derlemeler Windows 8'e özgü API'leri çağırmak için yerel yardımcı derlemeye başvurur.</span><span class="sxs-lookup"><span data-stu-id="35c82-188">In the example above the `lib/net40` assembly is purely managed code, whilst the assemblies in the runtimes folder will p/invoke into the native helper assembly to call APIs specific to Windows 8.</span></span>

<span data-ttu-id="35c82-189">Yalnızca tek `lib` bir klasör seçilir, bu nedenle çalışma zamanı belirli bir klasör varsa, `lib`çalışma zamanı olmayan belirli bir klasör seçilir.</span><span class="sxs-lookup"><span data-stu-id="35c82-189">Only a single `lib` folder is ever be picked, so if there is a runtime specific folder it's chosen over non-runtime specific `lib`.</span></span> <span data-ttu-id="35c82-190">Yerel klasör katkı maddesidir, varsa yapının çıktısına kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="35c82-190">The native folder is additive, if it exists it's copied to the output of the build.</span></span>

## <a name="managed-wrapper"></a><span data-ttu-id="35c82-191">Yönetilen sarıcı</span><span class="sxs-lookup"><span data-stu-id="35c82-191">Managed wrapper</span></span>

<span data-ttu-id="35c82-192">Çalışma sürelerini kullanmanın başka bir yolu da, tamamen yerel bir derleme üzerinde yönetilen bir ambalaj olan bir paketi sevk etmektir.</span><span class="sxs-lookup"><span data-stu-id="35c82-192">Another way to use runtimes is to ship a package that is purely a managed wrapper over a native assembly.</span></span> <span data-ttu-id="35c82-193">Bu senaryoda aşağıdaki gibi bir paket oluşturursunuz:</span><span class="sxs-lookup"><span data-stu-id="35c82-193">In this scenario you create a package like the following:</span></span>

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

<span data-ttu-id="35c82-194">Bu durumda, ilgili yerel `lib` derlemeye dayanmayan bu paketin uygulanması olmadığı için, bu klasör olarak üst düzey klasör yoktur.</span><span class="sxs-lookup"><span data-stu-id="35c82-194">In this case there is no top-level `lib` folder as that folder as there is no implementation of this package that doesn't rely on the corresponding native assembly.</span></span> <span data-ttu-id="35c82-195">Yönetilen derleme, `MyLibrary.dll`, her iki durumda da tam olarak aynı olsaydı o `lib` zaman bir üst düzey klasöre koyabilirsiniz, ancak bir yerel derleme eksikliği bir paket win-x86 veya win-x64 sonra üst düzey lib kullanılan ama hiçbir yerel derleme kopyalanmış olsaydı yükleme başarısız olmasına neden olmaz çünkü.</span><span class="sxs-lookup"><span data-stu-id="35c82-195">If the managed assembly, `MyLibrary.dll`, was exactly the same in both of these cases then we could put it in a top level `lib` folder, but because the lack of a native assembly doesn't cause the package to fail installing if it was installed on a platform that wasn't win-x86 or win-x64 then the top level lib would be used but no native assembly would be copied.</span></span>

## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a><span data-ttu-id="35c82-196">NuGet 2 ve NuGet 3 için yazma paketleri</span><span class="sxs-lookup"><span data-stu-id="35c82-196">Authoring packages for NuGet 2 and NuGet 3</span></span>

<span data-ttu-id="35c82-197">Aşağıdakileri kullanarak `packages.config` paketlerin yanı sıra projeler tarafından da tüketilebilen bir paket oluşturmak istiyorsanız aşağıdakileri uygulayın: `project.json`</span><span class="sxs-lookup"><span data-stu-id="35c82-197">If you want to create a package that can be consumed by projects using `packages.config` as well as packages using `project.json` then the following apply:</span></span>

- <span data-ttu-id="35c82-198">Ref ve çalışma süreleri yalnızca NuGet 3'te çalışır.</span><span class="sxs-lookup"><span data-stu-id="35c82-198">Ref and runtimes only work on NuGet 3.</span></span> <span data-ttu-id="35c82-199">Her ikisi de NuGet 2 tarafından göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="35c82-199">They are both ignored by NuGet 2.</span></span>

- <span data-ttu-id="35c82-200">Buna `install.ps1` güvenemezsiniz `uninstall.ps1` ya da çalışamazsınız.</span><span class="sxs-lookup"><span data-stu-id="35c82-200">You cannot rely on `install.ps1` or `uninstall.ps1` to function.</span></span> <span data-ttu-id="35c82-201">Bu dosyalar kullanırken `packages.config`yürütülür, ancak . `project.json`</span><span class="sxs-lookup"><span data-stu-id="35c82-201">These files execute when using `packages.config`, but are ignored with `project.json`.</span></span> <span data-ttu-id="35c82-202">Bu nedenle paketinizin onlar çalışmadan kullanılabilir olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="35c82-202">So your package needs to be usable without them running.</span></span> <span data-ttu-id="35c82-203">`init.ps1`hala NuGet 3'te çalışır.</span><span class="sxs-lookup"><span data-stu-id="35c82-203">`init.ps1` still runs on NuGet 3.</span></span>

- <span data-ttu-id="35c82-204">Hedefler ve Sahne Yüklemesi farklıdır, bu nedenle paketinizin her iki istemcide de beklendiği gibi çalıştığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="35c82-204">Targets and Props installation is different, so make sure that your package works as expected on both clients.</span></span>

- <span data-ttu-id="35c82-205">Lib alt dizinleri NuGet 3'te bir TxM olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="35c82-205">Subdirectories of lib must be a TxM in NuGet 3.</span></span> <span data-ttu-id="35c82-206">Kitaplıkları `lib` klasörün köküne yerleştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="35c82-206">You cannot place libraries at the root of the `lib` folder.</span></span>

- <span data-ttu-id="35c82-207">İçerik NuGet 3 ile otomatik olarak kopyalanmaz.</span><span class="sxs-lookup"><span data-stu-id="35c82-207">Content is not copied automatically with NuGet 3.</span></span> <span data-ttu-id="35c82-208">Paketinizin tüketicileri dosyaları kendileri kopyalayabilir veya dosyaları kopyalamayı otomatikleştirmek için görev koşucusu gibi bir araç kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="35c82-208">Consumers of your package could copy the files themselves or use a tool like a task runner to automate copying the files.</span></span>

- <span data-ttu-id="35c82-209">Kaynak ve config dosya dönüşümleri NuGet 3 tarafından çalıştırılmez.</span><span class="sxs-lookup"><span data-stu-id="35c82-209">Source and config file transforms are not run by NuGet 3.</span></span>

<span data-ttu-id="35c82-210">NuGet 2 ve 3'ü destekliyorsanız, paketinizin üzerinde çalıştığı NuGet 2 istemcisinin en düşük sürümü `minClientVersion` olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="35c82-210">If you are supporting NuGet 2 and 3 then your `minClientVersion` should be the lowest version of NuGet 2 client that your package works on.</span></span> <span data-ttu-id="35c82-211">Varolan bir paket söz konusu olduğunda, bu paketin değişmesi gerekmez.</span><span class="sxs-lookup"><span data-stu-id="35c82-211">In the case of an existing package it shouldn't need to change.</span></span>
