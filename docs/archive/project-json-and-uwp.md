---
title: NuGet project.json dosyasını içeren UWP projeleri
description: Project.json dosyasını NuGet bağımlılıklarını Evrensel Windows Platformu (UWP) projelerindeki izlemek için nasıl kullanıldığını açıklaması.
author: karann-msft
ms.author: karann
ms.date: 07/17/2017
ms.topic: conceptual
ms.openlocfilehash: ac3c137dd0ba50571737093eef11c8ab0ef932b2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548670"
---
# <a name="projectjson-and-uwp"></a><span data-ttu-id="02053-103">Project.JSON ve UWP</span><span class="sxs-lookup"><span data-stu-id="02053-103">project.json and UWP</span></span>

> [!Important]
> <span data-ttu-id="02053-104">Bu içerik kullanım dışı bırakılmıştır.</span><span class="sxs-lookup"><span data-stu-id="02053-104">This content is deprecated.</span></span> <span data-ttu-id="02053-105">Projeleri ya da kullanması gereken `packages.config` veya PackageReference biçimleri.</span><span class="sxs-lookup"><span data-stu-id="02053-105">Projects should use either the `packages.config` or PackageReference formats.</span></span>

<span data-ttu-id="02053-106">Bu belge, özellikleri NuGet 3 + (Visual Studio 2015 veya üzeri) kullanır paket yapısını açıklar.</span><span class="sxs-lookup"><span data-stu-id="02053-106">This document describes the package structure that employs features in NuGet 3+ (Visual Studio 2015 and later).</span></span> <span data-ttu-id="02053-107">`minClientVersion` Özelliği, `.nuspec` 3.1 için ayarlayarak burada açıklanan özellikler ihtiyacınız olan durum için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="02053-107">The `minClientVersion` property of your `.nuspec` can be used to state that you require the features described here by setting it to 3.1.</span></span>

## <a name="adding-uwp-support-to-an-existing-package"></a><span data-ttu-id="02053-108">Var olan bir pakete eklenirken podpora UWP</span><span class="sxs-lookup"><span data-stu-id="02053-108">Adding UWP support to an existing package</span></span>

<span data-ttu-id="02053-109">Var olan bir paket varsa ve UWP uygulamaları için desteği eklemek istiyorsanız, burada açıklanan paketleme biçimini benimseyin gerekmez.</span><span class="sxs-lookup"><span data-stu-id="02053-109">If you have an existing package and you want to add support for UWP applications, then you don’t need to adopt the  packaging format described here.</span></span> <span data-ttu-id="02053-110">Tanımlar ve yalnızca NuGet istemci sürümüne 3 + güncelleştirilmiş istemciler çalışmak istediğiniz özellikler gerektiriyorsa, bu biçim benimsemek yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="02053-110">You only need to adopt this format if you require the features it describes and are willing to  work only with clients that have updated to version 3+ of the NuGet client.</span></span>

## <a name="i-already-target-netcore45"></a><span data-ttu-id="02053-111">Ben zaten netcore45 hedef</span><span class="sxs-lookup"><span data-stu-id="02053-111">I already target netcore45</span></span>

<span data-ttu-id="02053-112">Hedefliyorsanız `netcore45` zaten ve özelliklerden burada yapmanız gerekmez, Eylem gerekmiyor.</span><span class="sxs-lookup"><span data-stu-id="02053-112">If you target `netcore45` already, and you don’t need to take advantage of the features here, no action is needed.</span></span> <span data-ttu-id="02053-113">`netcore45` paketleri UWP uygulamaları tarafından kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="02053-113">`netcore45` packages can be consumed by UWP applications.</span></span>

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a><span data-ttu-id="02053-114">Windows 10 özel API'ların yararlanmak istiyorum</span><span class="sxs-lookup"><span data-stu-id="02053-114">I want to take advantage of Windows 10 specific APIs</span></span>

<span data-ttu-id="02053-115">Bu durumda, eklemeniz gereken `uap10.0` hedef çerçeve adı (TFM veya TxM) paketi.</span><span class="sxs-lookup"><span data-stu-id="02053-115">In this case you need to add the `uap10.0` target framework moniker (TFM or TxM) to your package.</span></span> <span data-ttu-id="02053-116">Paketiniz yeni bir klasör oluşturun ve bu klasöre Windows 10 ile çalışmak için derlenmiş bütünleştirilmiş kod ekleyin.</span><span class="sxs-lookup"><span data-stu-id="02053-116">Create a new folder in your package and add the assembly that has been compiled to work with Windows 10 to that folder.</span></span>

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a><span data-ttu-id="02053-117">Windows 10 özel API'ler, ihtiyacınız yoktur, ancak yeni .NET özellikleri istediğiniz veya netcore45 yoksa</span><span class="sxs-lookup"><span data-stu-id="02053-117">I don’t need Windows 10 specific APIs, but want new .NET features or don’t have netcore45 already</span></span>

<span data-ttu-id="02053-118">Bu durumda, eklediğiniz `dotnet` TxM paketi.</span><span class="sxs-lookup"><span data-stu-id="02053-118">In this case you would add the `dotnet` TxM to your package.</span></span> <span data-ttu-id="02053-119">Diğer TxMs aksine `dotnet` yüzey veya platform açık değil.</span><span class="sxs-lookup"><span data-stu-id="02053-119">Unlike other TxMs, `dotnet` doesn't imply a surface area or platform.</span></span> <span data-ttu-id="02053-120">Bu, paket bağımlılıklarınızı üzerinde çalışan herhangi bir platformda çalışan belirten olur.</span><span class="sxs-lookup"><span data-stu-id="02053-120">It is stating that your package works on any platform that your dependencies work on.</span></span> <span data-ttu-id="02053-121">Sahip bir paket oluştururken `dotnet` TxM, büyük olasılıkla pek çok daha fazla TxM özel bağımlılıklar vardır uygulamanızın `.nuspec`, gibi bağımlı BCL paketleri tanımlamak gerek duyduğunuz `System.Text`, `System.Xml`vb. Burada paketinizi çalışır, bu bağımlılıkların çalıştığı konumları tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="02053-121">When building a package with the `dotnet` TxM, you are likely to have many more TxM-specific dependencies in your `.nuspec`, as you need to define the BCL packages you depend on, such `System.Text`, `System.Xml`, etc. The locations that those dependencies work on define where your package works.</span></span>

### <a name="how-do-i-find-out-my-dependencies"></a><span data-ttu-id="02053-122">Bağımlılıkların nasıl bulabilirim</span><span class="sxs-lookup"><span data-stu-id="02053-122">How do I find out my dependencies</span></span>

<span data-ttu-id="02053-123">Listelemek için hangi bağımlılıkların anlamak için iki yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="02053-123">There are two ways to figure out which dependencies to list:</span></span>

1. <span data-ttu-id="02053-124">Kullanım [NuSpec bağımlılık Oluşturucu](https://github.com/onovotny/ReferenceGenerator) **3. taraf** aracı.</span><span class="sxs-lookup"><span data-stu-id="02053-124">Use the [NuSpec Dependency Generator](https://github.com/onovotny/ReferenceGenerator) **3rd party** tool.</span></span> <span data-ttu-id="02053-125">Aracı işlemini ve güncelleştirmeleri otomatikleştirir, `.nuspec` derlemede bağımlı paketlerin dosya.</span><span class="sxs-lookup"><span data-stu-id="02053-125">The tool automates the process and updates your `.nuspec` file with the dependant packages on build.</span></span> <span data-ttu-id="02053-126">Bir NuGet paketi kullanılabilir [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).</span><span class="sxs-lookup"><span data-stu-id="02053-126">It is available via a NuGet package, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).</span></span>

1. <span data-ttu-id="02053-127">(Zor olan yolu) Kullanım `ILDasm` bakmak için `.dll` hangi derlemeleri çalışma zamanında gerçekten gerekli olup olmadığını görmek için.</span><span class="sxs-lookup"><span data-stu-id="02053-127">(The hard way) Use `ILDasm` to look at your `.dll` to see what assemblies are actually needed at runtime.</span></span> <span data-ttu-id="02053-128">Ardından gelir her hangi bir NuGet paketi belirler.</span><span class="sxs-lookup"><span data-stu-id="02053-128">Then determine which NuGet package they each come from.</span></span>

<span data-ttu-id="02053-129">Bkz: [ `project.json` ](project-json.md) destekleyen bir paketin oluşturmaya yardımcı olan özellikler hakkında ayrıntılı bilgi için konu `dotnet` TxM.</span><span class="sxs-lookup"><span data-stu-id="02053-129">See the [`project.json`](project-json.md) topic for details on features that help in the creation of a package that supports the `dotnet` TxM.</span></span>

> [!Important]
> <span data-ttu-id="02053-130">Paketiniz PCL projeleri ile kullanılmak üzere tasarlanmış, yüksek oranda oluşturmak için önerilir bir `dotnet` uyarıları ve olası uyumluluk sorunları önlemek için klasör.</span><span class="sxs-lookup"><span data-stu-id="02053-130">If your package is intended to work with PCL projects, we highly recommend to create a `dotnet` folder, to avoid warnings and potential compatibility issues.</span></span>

## <a name="directory-structure"></a><span data-ttu-id="02053-131">Dizin yapısı</span><span class="sxs-lookup"><span data-stu-id="02053-131">Directory structure</span></span>

<span data-ttu-id="02053-132">NuGet paketlerini şu biçimi kullanarak aşağıdaki bilinen bir klasörü ve davranışları vardır:</span><span class="sxs-lookup"><span data-stu-id="02053-132">NuGet packages using this format have the following well-known folder and behaviors:</span></span>

| <span data-ttu-id="02053-133">Klasör</span><span class="sxs-lookup"><span data-stu-id="02053-133">Folder</span></span> | <span data-ttu-id="02053-134">Davranışlar</span><span class="sxs-lookup"><span data-stu-id="02053-134">Behaviors</span></span> |
| --- | --- |
| <span data-ttu-id="02053-135">Derleme</span><span class="sxs-lookup"><span data-stu-id="02053-135">Build</span></span> | <span data-ttu-id="02053-136">İçeren MSBuild hedeflerini ve özellik dosyalarını bu klasöre projeye farklı şekilde tümleştirilir, ancak Aksi halde bir değişiklik yoktur.</span><span class="sxs-lookup"><span data-stu-id="02053-136">Contains MSBuild targets and props files in this folder are integrated differently into the project, but otherwise there is no change.</span></span> |
| <span data-ttu-id="02053-137">Araçlar</span><span class="sxs-lookup"><span data-stu-id="02053-137">Tools</span></span> | <span data-ttu-id="02053-138">`install.ps1` ve `uninstall.ps1` çalıştırılamaz.</span><span class="sxs-lookup"><span data-stu-id="02053-138">`install.ps1` and `uninstall.ps1` are not run.</span></span> <span data-ttu-id="02053-139">`init.ps1` her zaman olduğu gibi çalışır.</span><span class="sxs-lookup"><span data-stu-id="02053-139">`init.ps1` works as it always has.</span></span> |
| <span data-ttu-id="02053-140">İçerik</span><span class="sxs-lookup"><span data-stu-id="02053-140">Content</span></span> | <span data-ttu-id="02053-141">İçeriği bir kullanıcının projesine otomatik olarak kopyalanır değil.</span><span class="sxs-lookup"><span data-stu-id="02053-141">Content is not copied automatically into a user's project.</span></span> <span data-ttu-id="02053-142">Sonraki bir sürümü için içerik ekleme projedeki desteği planlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="02053-142">Support for content inclusion in the project is planned for a later release.</span></span> |
| <span data-ttu-id="02053-143">lib</span><span class="sxs-lookup"><span data-stu-id="02053-143">Lib</span></span> | <span data-ttu-id="02053-144">Birçok paketler için `lib` Nuget'te yaptığı aynı şekilde çalışan 2.x, ancak hangi adları için genişletilmiş seçenekler ile kullanılabilir ve daha iyi mantıksal paketleri tüketildiğinde doğru alt klasörü seçmek için.</span><span class="sxs-lookup"><span data-stu-id="02053-144">For many packages the `lib` works the same way it does in NuGet 2.x, but with expanded options for what names can be used inside it and better logic for picking the correct sub-folder when consuming packages.</span></span> <span data-ttu-id="02053-145">Ancak, birlikte kullanıldığında `ref`, `lib` klasörünü içeren derlemeler tarafından tanımlanan yüzey uygulayan derlemeler `ref` klasör.</span><span class="sxs-lookup"><span data-stu-id="02053-145">However, when used in conjunction with `ref`, the `lib` folder contains assemblies that implement the surface area defined by the assemblies in the `ref` folder.</span></span> |
| <span data-ttu-id="02053-146">başvuru</span><span class="sxs-lookup"><span data-stu-id="02053-146">Ref</span></span> | <span data-ttu-id="02053-147">`ref` genel tanımlama .NET derlemelerini içeren isteğe bağlı bir klasördür karşı derleme olanağı, bir uygulama için surface (Genel türleri ve yöntemleri).</span><span class="sxs-lookup"><span data-stu-id="02053-147">`ref` is an optional folder that contains .NET assemblies defining the public surface (public types and methods) for an application to compile against.</span></span> <span data-ttu-id="02053-148">Bu klasör derlemelerde uygulaması bulunmuyor, bunlar tamamen derleyici yüzey alanını tanımlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="02053-148">The assemblies in this folder may have no implementation, they are purely used to define surface area for the compiler.</span></span> <span data-ttu-id="02053-149">Paket Hayır varsa `ref` klasörü, ardından `lib` başvuru bütünleştirilmiş kodu hem uygulama derleme.</span><span class="sxs-lookup"><span data-stu-id="02053-149">If the package has no `ref` folder, then the `lib` is both the reference assembly and the implementation assembly.</span></span> |
| <span data-ttu-id="02053-150">Çalışma zamanları</span><span class="sxs-lookup"><span data-stu-id="02053-150">Runtimes</span></span> | <span data-ttu-id="02053-151">`runtimes` CPU mimarisi ve işletim sistemi belirli veya başka türlü platforma bağımlı ikili dosyalar gibi belirli işletim sistemi kodu içeren bir isteğe bağlı bir klasördür.</span><span class="sxs-lookup"><span data-stu-id="02053-151">`runtimes` is an optional folder that contains OS specific code, such as CPU architecture and OS specific or otherwise platform-dependent binaries.</span></span> |

## <a name="msbuild-targets-and-props-files-in-packages"></a><span data-ttu-id="02053-152">MSBuild hedeflerini ve özellik dosyalarını paketler</span><span class="sxs-lookup"><span data-stu-id="02053-152">MSBuild targets and props files in packages</span></span>

<span data-ttu-id="02053-153">NuGet paketlerini içerebilir `.targets` ve `.props` içine paketinin yüklü olduğu herhangi bir MSBuild Projesi içeri aktarılan dosyaları.</span><span class="sxs-lookup"><span data-stu-id="02053-153">NuGet packages can contain `.targets` and `.props` files which are imported into any MSBuild project that the package is installed into.</span></span> <span data-ttu-id="02053-154">Nuget'te 2.x, bu silme işleminin ekleyerek `<Import>` açıklamaalarını `.csproj` dosya, NuGet 3.0 özel "Kurulum" projesi için bir eylem yok.</span><span class="sxs-lookup"><span data-stu-id="02053-154">In NuGet 2.x, this was done by injecting `<Import>` statements into the `.csproj` file, in NuGet 3.0 there is no specific "installation to project" action.</span></span> <span data-ttu-id="02053-155">Bunun yerine paket geri yükleme işlemi iki dosyalarını Yazar `[projectname].nuget.props` ve `[projectname].NuGet.targets`.</span><span class="sxs-lookup"><span data-stu-id="02053-155">Instead the package restore process writes two files `[projectname].nuget.props` and `[projectname].NuGet.targets`.</span></span>

<span data-ttu-id="02053-156">MSBuild, bu iki dosyaları aramak için bilir ve başlangıcı yakınında ve proje derleme işleminin sonunda otomatik olarak alır.</span><span class="sxs-lookup"><span data-stu-id="02053-156">MSBuild knows to look for these two files and automatically imports them near the beginning and near the end of the project build process.</span></span> <span data-ttu-id="02053-157">Bu çok benzer bir davranış için NuGet sağlar 2.x, ancak temel farklardan biri: *yoktur yürütülme sırası belirli hedefleri/özellik dosyaları bu durumda*.</span><span class="sxs-lookup"><span data-stu-id="02053-157">This provides very similar behavior to NuGet 2.x, but with one major difference: *there is no guaranteed order of targets/props files in this case*.</span></span> <span data-ttu-id="02053-158">MSBuild yolu sipariş hedeflere sağlar ancak `BeforeTargets` ve `AfterTargets` özniteliklerini `<Target>` tanımı (bkz [hedef öğe (MSBuild)](/visualstudio/msbuild/target-element-msbuild).</span><span class="sxs-lookup"><span data-stu-id="02053-158">However, MSBuild does provide ways to order targets through the `BeforeTargets` and `AfterTargets` attributes of the `<Target>` definition (see [Target Element (MSBuild)](/visualstudio/msbuild/target-element-msbuild).</span></span>

## <a name="lib-and-ref"></a><span data-ttu-id="02053-159">LIB ve başvuru</span><span class="sxs-lookup"><span data-stu-id="02053-159">Lib and Ref</span></span>

<span data-ttu-id="02053-160">Davranışını `lib` klasörü henüz değiştirilen önemli ölçüde NuGet v3 sürümünde.</span><span class="sxs-lookup"><span data-stu-id="02053-160">The behavior of the `lib` folder hasn't changed significantly in NuGet v3.</span></span> <span data-ttu-id="02053-161">Ancak, tüm derlemelerin bir TxM sonra alt klasörleri içinde olmalıdır ve artık doğrudan altında yerleştirilebilir `lib` klasör.</span><span class="sxs-lookup"><span data-stu-id="02053-161">However, all assemblies must be within sub-folders named after a TxM, and can no longer be placed directly under the `lib` folder.</span></span> <span data-ttu-id="02053-162">Bir TxM bir paket içinde belirli bir varlık için iş geç bir platform adıdır.</span><span class="sxs-lookup"><span data-stu-id="02053-162">A TxM is the name of a platform that a given asset in a package is supposed to work for.</span></span> <span data-ttu-id="02053-163">Mantıksal bir uzantı hedef çerçeve bilinen adlar (TFM) Örneğin bunlar `net45`, `net46`, `netcore50`, ve `dnxcore50` TxMs tüm örnekleri (bkz [hedef çerçeve](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="02053-163">Logically these are an extension of the Target Framework Monikers (TFM) e.g. `net45`, `net46`, `netcore50`, and `dnxcore50` are all examples of TxMs (see [Target Frameworks](../reference/target-frameworks.md).</span></span> <span data-ttu-id="02053-164">TxM bir çerçeve (TFM) yanı sıra diğer platforma özgü yüzey alanlarına başvurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02053-164">TxM can refer to a framework (TFM) as well as other platform-specific surface areas.</span></span> <span data-ttu-id="02053-165">Örneğin UWP TxM (`uap10.0`) UWP uygulamaları için Windows yüzey alanını yanı sıra .NET yüzey alanını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="02053-165">For example the UWP TxM (`uap10.0`) represents the .NET surface area as well as the Windows surface area for UWP applications.</span></span>

<span data-ttu-id="02053-166">Bir örnek LIB yapısı:</span><span class="sxs-lookup"><span data-stu-id="02053-166">An example lib structure:</span></span>

    lib
    ├───net40
    │       MyLibrary.dll
    └───wp81
            MyLibrary.dll

<span data-ttu-id="02053-167">`lib` Klasörü, çalışma zamanında kullanılan derlemeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="02053-167">The `lib` folder contains assemblies that are used at runtime.</span></span> <span data-ttu-id="02053-168">En altında bir klasör paketleri `lib` her hedef TxMs gerekli olan tüm için.</span><span class="sxs-lookup"><span data-stu-id="02053-168">For most packages a folder under `lib` for each of the target TxMs is all that is required.</span></span>

## <a name="ref"></a><span data-ttu-id="02053-169">başvuru</span><span class="sxs-lookup"><span data-stu-id="02053-169">Ref</span></span>

<span data-ttu-id="02053-170">Bazı durumlarda farklı bir derleme (.NET başvuru derlemeleri yapın bu Bugün) derleme sırasında burada kullanılması gereken durumlar da vardır.</span><span class="sxs-lookup"><span data-stu-id="02053-170">There are sometimes cases where a different assembly should be used during compilation (.NET Reference Assemblies do this today).</span></span> <span data-ttu-id="02053-171">Bu gibi durumlarda adlı en üst düzey bir klasör kullanan `ref` (kısaltması "başvuru bütünleştirilmiş kodlarını").</span><span class="sxs-lookup"><span data-stu-id="02053-171">For those cases, use a top-level folder called `ref` (short for "Reference Assemblies").</span></span>

<span data-ttu-id="02053-172">Çoğu paket yazarlarının gerektirmeyen `ref` klasör.</span><span class="sxs-lookup"><span data-stu-id="02053-172">Most package authors don't require the `ref` folder.</span></span> <span data-ttu-id="02053-173">Derleme ve IntelliSense için tutarlı bir yüzey alanını sağlar ancak ardından farklı TxMs için farklı bir uygulama için gereksinim paketlerin için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="02053-173">It is useful for packages that need to provide a consistent surface area for compilation and IntelliSense but then have different implementation for different TxMs.</span></span> <span data-ttu-id="02053-174">Bu olan büyük kullanım örneği `System.*` sevkiyat .NET Core NuGet üzerindeki bir parçası olarak oluşturulan paketler.</span><span class="sxs-lookup"><span data-stu-id="02053-174">The biggest use case of this are the `System.*` packages that are being produced as part of shipping .NET Core on NuGet.</span></span> <span data-ttu-id="02053-175">Bu paketler, ref derlemelerin tutarlı bir kümesini birleşik çeşitli uygulamalara sahip.</span><span class="sxs-lookup"><span data-stu-id="02053-175">These packages have various implementations that are being unified by a consistent set of ref assemblies.</span></span>

<span data-ttu-id="02053-176">Derlemeleri mekanik olarak, dahil `ref` klasörü olduğu için derleyici geçirilen başvuru bütünleştirilmiş kodları.</span><span class="sxs-lookup"><span data-stu-id="02053-176">Mechanically, the assemblies included in the `ref` folder are the reference assemblies being passed to the compiler.</span></span> <span data-ttu-id="02053-177">Biz için kaçı derlemeleri olanlar csc.exe kullanmış için bunlar [C# / Reference seçeneği](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) geçin.</span><span class="sxs-lookup"><span data-stu-id="02053-177">For those of you who have used csc.exe these are the assemblies we are passing to the [C# /reference option](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) switch.</span></span>

<span data-ttu-id="02053-178">Yapısını `ref` klasördür aynı `lib`, örneğin:</span><span class="sxs-lookup"><span data-stu-id="02053-178">The structure of the `ref` folder is the same as `lib`, for example:</span></span>

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

<span data-ttu-id="02053-179">Bu örnekte derlemelerde `ref` dizinleri tüm aynı olması.</span><span class="sxs-lookup"><span data-stu-id="02053-179">In this example the assemblies in the `ref` directories would all be identical.</span></span>

## <a name="runtimes"></a><span data-ttu-id="02053-180">Çalışma zamanları</span><span class="sxs-lookup"><span data-stu-id="02053-180">Runtimes</span></span>

<span data-ttu-id="02053-181">Çalışma zamanları klasörü, derlemeleri ve "genellikle işletim sistemi ve CPU mimarisine göre tanımlanan özel çalışma zamanları", üzerinde çalıştırmak için gerekli yerel kitaplıkları içerir.</span><span class="sxs-lookup"><span data-stu-id="02053-181">The runtimes folder contains assemblies and native libraries required to run on specific "runtimes", which are generally defined by Operating System and CPU architecture.</span></span> <span data-ttu-id="02053-182">Bu çalışma zamanları kullanılarak tanımlanır [çalışma zamanı tanımlayıcılarının (RID'ler)](/dotnet/core/rid-catalog) gibi `win`, `win-x86`, `win7-x86`, `win8-64`vb.</span><span class="sxs-lookup"><span data-stu-id="02053-182">These runtimes are identified using [Runtime Identifiers (RIDs)](/dotnet/core/rid-catalog) such as `win`, `win-x86`, `win7-x86`, `win8-64`, etc.</span></span>

## <a name="native-helpers-to-use-platform-specific-apis"></a><span data-ttu-id="02053-183">Platforma özel API'leri kullanmak için yerel Yardımcıları</span><span class="sxs-lookup"><span data-stu-id="02053-183">Native helpers to use platform-specific APIs</span></span>

<span data-ttu-id="02053-184">Aşağıdaki örnek, çeşitli platformlar için tamamen yönetilen bir uygulamasını var, ancak Windows 8'i Windows 8 özgü yerel API'lere burada çağırabilirsiniz yerel Yardımcıları kullanan bir paket gösterir.</span><span class="sxs-lookup"><span data-stu-id="02053-184">The following example shows a package that has a purely managed implementation for several platforms, but uses native helpers on Windows 8 where it can call into Windows 8-specific native APIs.</span></span>

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

<span data-ttu-id="02053-185">Yukarıdaki paket aşağıdakiler gerçekleşir:</span><span class="sxs-lookup"><span data-stu-id="02053-185">Given the above package the following things happen:</span></span>

- <span data-ttu-id="02053-186">Windows 8'de ne zaman `lib/net40/MyLibrary.dll` derleme kullanılır.</span><span class="sxs-lookup"><span data-stu-id="02053-186">When not on Windows 8 the `lib/net40/MyLibrary.dll` assembly is used.</span></span>

- <span data-ttu-id="02053-187">Windows 8 ne zaman `runtimes/win8-<architecture>/lib/MyLibrary.dll` kullanılır ve `native/MyNativeHelper.dll` yapı çıkışını kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="02053-187">When on Windows 8 the `runtimes/win8-<architecture>/lib/MyLibrary.dll` is used and the `native/MyNativeHelper.dll` is copied to the output of your build.</span></span>

<span data-ttu-id="02053-188">Yukarıdaki örnekte `lib/net40` derlemedir, tamamen yönetilen kod, Windows 8 özel API'leri çağırmak için yerel Yardımcısı derlemesini p/Invoke derlemeler çalışma zamanları klasöründe olacaktır artırabileceksiniz.</span><span class="sxs-lookup"><span data-stu-id="02053-188">In the example above the `lib/net40` assembly is purely managed code, whilst the assemblies in the runtimes folder will p/invoke into the native helper assembly to call APIs specific to Windows 8.</span></span>

<span data-ttu-id="02053-189">Yalnızca tek bir `lib` klasör olduğu hiç olmadığı kadar olması Çekildi, çalışma zamanı belirli bir klasöre ise çalışma zamanı olmayan özel seçilir şekilde `lib`.</span><span class="sxs-lookup"><span data-stu-id="02053-189">Only a single `lib` folder is ever be picked, so if there is a runtime specific folder it's chosen over non-runtime specific `lib`.</span></span> <span data-ttu-id="02053-190">Yerel klasör, varsa eklenebilir, yapı çıkışını kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="02053-190">The native folder is additive, if it exists it's copied to the output of the build.</span></span>

## <a name="managed-wrapper"></a><span data-ttu-id="02053-191">Yönetilen sarmalayıcı</span><span class="sxs-lookup"><span data-stu-id="02053-191">Managed wrapper</span></span>

<span data-ttu-id="02053-192">Çalışma zamanı kullanmak için başka bir yerel bir derleme üzerinde tamamen yönetilen bir sarmalayıcı olan bir paket göndermeye yoludur.</span><span class="sxs-lookup"><span data-stu-id="02053-192">Another way to use runtimes is to ship a package that is purely a managed wrapper over a native assembly.</span></span> <span data-ttu-id="02053-193">Bu senaryoda aşağıdaki gibi bir paket oluşturun:</span><span class="sxs-lookup"><span data-stu-id="02053-193">In this scenario you create a package like the following:</span></span>

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

<span data-ttu-id="02053-194">Bu durumda olduğu en üst düzey `lib` klasördür orada olarak bu klasör olarak hiçbir uygulama bu paketinin karşılık gelen yerel derleme üzerinde içermez.</span><span class="sxs-lookup"><span data-stu-id="02053-194">In this case there is no top-level `lib` folder as that folder as there is no implementation of this package that doesn't rely on the corresponding native assembly.</span></span> <span data-ttu-id="02053-195">Yönetilen bütünleştirilmiş kod `MyLibrary.dll`, biz bunu bir üst düzey yerleştirebilirsiniz sonra tam olarak her iki durumda aynı olan `lib` klasörü, ancak yerel bir derleme eksikliği paket bir platformda yüklediyseniz yükleme başarısız olmasına neden olmaz, Win-x86 veya win x64 üst düzey LIB kullanılır ancak hiçbir yerel derleme kopyalanacak değildi.</span><span class="sxs-lookup"><span data-stu-id="02053-195">If the managed assembly, `MyLibrary.dll`, was exactly the same in both of these cases then we could put it in a top level `lib` folder, but because the lack of a native assembly doesn't cause the package to fail installing if it was installed on a platform that wasn't win-x86 or win-x64 then the top level lib would be used but no native assembly would be copied.</span></span>

## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a><span data-ttu-id="02053-196">NuGet 2 ve 3 NuGet paketleri yazma</span><span class="sxs-lookup"><span data-stu-id="02053-196">Authoring packages for NuGet 2 and NuGet 3</span></span>

<span data-ttu-id="02053-197">Kullanarak projeleri tarafından kullanılabilen bir paket oluşturmak istiyorsanız `packages.config` de olarak paketleri kullanarak `project.json` sonra aşağıdaki Uygula:</span><span class="sxs-lookup"><span data-stu-id="02053-197">If you want to create a package that can be consumed by projects using `packages.config` as well as packages using `project.json` then the following apply:</span></span>

- <span data-ttu-id="02053-198">Yalnızca ref ve çalışma zamanları NuGet 3'te çalışır.</span><span class="sxs-lookup"><span data-stu-id="02053-198">Ref and runtimes only work on NuGet 3.</span></span> <span data-ttu-id="02053-199">Bunlar her ikisi de NuGet 2 tarafından yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="02053-199">They are both ignored by NuGet 2.</span></span>

- <span data-ttu-id="02053-200">Üzerinde güvenemezsiniz `install.ps1` veya `uninstall.ps1` işlevi.</span><span class="sxs-lookup"><span data-stu-id="02053-200">You cannot rely on `install.ps1` or `uninstall.ps1` to function.</span></span> <span data-ttu-id="02053-201">Bu dosyaları kullanırken yürütmek `packages.config`, ile göz ardı edilir ancak `project.json`.</span><span class="sxs-lookup"><span data-stu-id="02053-201">These files execute when using `packages.config`, but are ignored with `project.json`.</span></span> <span data-ttu-id="02053-202">Paketiniz onlar olmadan kullanılabilir olması gerekir çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="02053-202">So your package needs to be usable without them running.</span></span> <span data-ttu-id="02053-203">`init.ps1` yine de NuGet 3'te çalışır.</span><span class="sxs-lookup"><span data-stu-id="02053-203">`init.ps1` still runs on NuGet 3.</span></span>

- <span data-ttu-id="02053-204">Hedeflerini ve özellik yükleme farklıdır, bu nedenle paketinizi hem de istemcilerde beklendiği gibi çalıştığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="02053-204">Targets and Props installation is different, so make sure that your package works as expected on both clients.</span></span>

- <span data-ttu-id="02053-205">LIB alt dizinleri NuGet 3'te bir TxM olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="02053-205">Subdirectories of lib must be a TxM in NuGet 3.</span></span> <span data-ttu-id="02053-206">Kitaplıkları kökünde yerleştirilemiyor `lib` klasör.</span><span class="sxs-lookup"><span data-stu-id="02053-206">You cannot place libraries at the root of the `lib` folder.</span></span>

- <span data-ttu-id="02053-207">İçeriği NuGet 3 ile otomatik olarak kopyalanır değil.</span><span class="sxs-lookup"><span data-stu-id="02053-207">Content is not copied automatically with NuGet 3.</span></span> <span data-ttu-id="02053-208">Tüketiciler paketinizin, dosyaları kopyalayın veya dosyaları kopyalama otomatikleştirmek için görev Çalıştırıcı gibi bir araç kullanın.</span><span class="sxs-lookup"><span data-stu-id="02053-208">Consumers of your package could copy the files themselves or use a tool like a task runner to automate copying the files.</span></span>

- <span data-ttu-id="02053-209">Kaynak ve yapılandırma dosyası dönüşümleri NuGet 3 ile çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="02053-209">Source and config file transforms are not run by NuGet 3.</span></span>

<span data-ttu-id="02053-210">NuGet 2 ve 3 destekleniyorsa sonra `minClientVersion` paketinizi çalışır NuGet 2 istemci en düşük sürümü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="02053-210">If you are supporting NuGet 2 and 3 then your `minClientVersion` should be the lowest version of NuGet 2 client that your package works on.</span></span> <span data-ttu-id="02053-211">Söz konusu olduğunda var olan bir paketi bunu değiştirmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="02053-211">In the case of an existing package it shouldn't need to change.</span></span>
