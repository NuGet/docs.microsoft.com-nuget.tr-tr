---
title: UWP projeleri ile dosyada NuGet project.js
description: Evrensel Windows Platformu (UWP) projelerinde NuGet bağımlılıklarını izlemek için project.jsdosyanın nasıl kullanıldığına ilişkin açıklama.
author: JonDouglas
ms.author: jodou
ms.date: 07/17/2017
ms.topic: conceptual
ms.openlocfilehash: 30e2272aafb5d2ea8d932e3cb0209d97c30b3209
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773801"
---
# <a name="projectjson-and-uwp"></a><span data-ttu-id="d11ae-103">project.json ve UWP</span><span class="sxs-lookup"><span data-stu-id="d11ae-103">project.json and UWP</span></span>

> [!Important]
> <span data-ttu-id="d11ae-104">Bu içerik kullanımdan kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="d11ae-104">This content is deprecated.</span></span> <span data-ttu-id="d11ae-105">Projeler ya `packages.config` ya da PackageReference biçimlerini kullanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d11ae-105">Projects should use either the `packages.config` or PackageReference formats.</span></span>

<span data-ttu-id="d11ae-106">Bu belgede, NuGet 3 + (Visual Studio 2015 ve üzeri) özelliklerini kullanan paket yapısı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d11ae-106">This document describes the package structure that employs features in NuGet 3+ (Visual Studio 2015 and later).</span></span> <span data-ttu-id="d11ae-107">' `minClientVersion` In özelliği, `.nuspec` burada açıklanan özelliklerin 3,1 olarak ayarlanarak gerekli olduğunu belirten bir durum için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d11ae-107">The `minClientVersion` property of your `.nuspec` can be used to state that you require the features described here by setting it to 3.1.</span></span>

## <a name="adding-uwp-support-to-an-existing-package"></a><span data-ttu-id="d11ae-108">Mevcut bir pakete UWP desteği ekleniyor</span><span class="sxs-lookup"><span data-stu-id="d11ae-108">Adding UWP support to an existing package</span></span>

<span data-ttu-id="d11ae-109">Mevcut bir paketiniz varsa ve UWP uygulamaları için destek eklemek istiyorsanız, burada açıklanan paketleme biçimini benimsemeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="d11ae-109">If you have an existing package and you want to add support for UWP applications, then you don’t need to adopt the  packaging format described here.</span></span> <span data-ttu-id="d11ae-110">Bu biçimi yalnızca, açıkladığı özellikleri gerektiriyorsa ve yalnızca NuGet istemcisinin sürüm 3 + ' e güncelleştirilmiş istemcilerle çalışmak istiyorsanız benimsemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d11ae-110">You only need to adopt this format if you require the features it describes and are willing to  work only with clients that have updated to version 3+ of the NuGet client.</span></span>

## <a name="i-already-target-netcore45"></a><span data-ttu-id="d11ae-111">Netcore45 zaten hedefdim</span><span class="sxs-lookup"><span data-stu-id="d11ae-111">I already target netcore45</span></span>

<span data-ttu-id="d11ae-112">`netcore45`Zaten hedefleyin ve buradaki özelliklerden faydalanmanız gerekmiyorsa, hiçbir işlem yapmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="d11ae-112">If you target `netcore45` already, and you don’t need to take advantage of the features here, no action is needed.</span></span> <span data-ttu-id="d11ae-113">`netcore45` paketler UWP uygulamaları tarafından tüketilebilir.</span><span class="sxs-lookup"><span data-stu-id="d11ae-113">`netcore45` packages can be consumed by UWP applications.</span></span>

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a><span data-ttu-id="d11ae-114">Windows 10 ' un belirli API 'lerden faydalanmak istiyorum</span><span class="sxs-lookup"><span data-stu-id="d11ae-114">I want to take advantage of Windows 10 specific APIs</span></span>

<span data-ttu-id="d11ae-115">Bu durumda, `uap10.0` hedef Framework bilinen adını (tfd veya TXD) paketinize eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d11ae-115">In this case you need to add the `uap10.0` target framework moniker (TFM or TxM) to your package.</span></span> <span data-ttu-id="d11ae-116">Paketinizdeki yeni bir klasör oluşturun ve derlenen derlemeyi bu klasöre Windows 10 ile çalışacak şekilde ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d11ae-116">Create a new folder in your package and add the assembly that has been compiled to work with Windows 10 to that folder.</span></span>

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a><span data-ttu-id="d11ae-117">Windows 10 ' a özel API 'Lere ihtiyacım var, ancak yeni .NET özellikleri mi yoksa yoksa netcore45 'e sahip değil</span><span class="sxs-lookup"><span data-stu-id="d11ae-117">I don’t need Windows 10 specific APIs, but want new .NET features or don’t have netcore45 already</span></span>

<span data-ttu-id="d11ae-118">Bu durumda, `dotnet` TXD 'yi paketinize eklersiniz.</span><span class="sxs-lookup"><span data-stu-id="d11ae-118">In this case you would add the `dotnet` TxM to your package.</span></span> <span data-ttu-id="d11ae-119">Diğer TxMs 'lerin aksine `dotnet` bir yüzey alanı veya platformu göstermez.</span><span class="sxs-lookup"><span data-stu-id="d11ae-119">Unlike other TxMs, `dotnet` doesn't imply a surface area or platform.</span></span> <span data-ttu-id="d11ae-120">Bu, paketinizin, bağımlılıklarınızın üzerinde çalıştığı tüm platformlarda çalıştığını ifade edilir.</span><span class="sxs-lookup"><span data-stu-id="d11ae-120">It is stating that your package works on any platform that your dependencies work on.</span></span> <span data-ttu-id="d11ae-121">TXD ile bir paket oluştururken, `dotnet` `.nuspec` bağlı olduğunuz BCL paketlerini ( `System.Text` vb.) tanımlamanız gerektiği gibi, sizin Için çok sayıda TXE özel bağımlılığı olması olasıdır `System.Xml` . Bu bağımlılıkların üzerinde çalıştığı konumlar, paketinizin nerede çalıştığını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="d11ae-121">When building a package with the `dotnet` TxM, you are likely to have many more TxM-specific dependencies in your `.nuspec`, as you need to define the BCL packages you depend on, such `System.Text`, `System.Xml`, etc. The locations that those dependencies work on define where your package works.</span></span>

### <a name="how-do-i-find-out-my-dependencies"></a><span data-ttu-id="d11ae-122">Bağımlılıklarımı bulma Nasıl yaparım?</span><span class="sxs-lookup"><span data-stu-id="d11ae-122">How do I find out my dependencies</span></span>

<span data-ttu-id="d11ae-123">Hangi bağımlılıkların listeye göre olduğunu anlamak için iki yol vardır:</span><span class="sxs-lookup"><span data-stu-id="d11ae-123">There are two ways to figure out which dependencies to list:</span></span>

1. <span data-ttu-id="d11ae-124">[Nuspec bağımlılık Oluşturucu](https://github.com/onovotny/ReferenceGenerator) **3. taraf** aracını kullanın.</span><span class="sxs-lookup"><span data-stu-id="d11ae-124">Use the [NuSpec Dependency Generator](https://github.com/onovotny/ReferenceGenerator) **3rd party** tool.</span></span> <span data-ttu-id="d11ae-125">Araç işlemi otomatikleştirir ve `.nuspec` derleme üzerindeki bağımlı paketlerle dosyanızı güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="d11ae-125">The tool automates the process and updates your `.nuspec` file with the dependant packages on build.</span></span> <span data-ttu-id="d11ae-126">Bu, [Nuspec. ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/)adlı bir NuGet paketi ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d11ae-126">It is available via a NuGet package, [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/).</span></span>

1. <span data-ttu-id="d11ae-127">(Sabit yol) `ILDasm` `.dll` Çalışma zamanında hangi derlemelerin gerçekten gerekli olduğunu görmek için ' i kullanın.</span><span class="sxs-lookup"><span data-stu-id="d11ae-127">(The hard way) Use `ILDasm` to look at your `.dll` to see what assemblies are actually needed at runtime.</span></span> <span data-ttu-id="d11ae-128">Ardından bunların her birinin nereden geldiği NuGet paketini saptayın.</span><span class="sxs-lookup"><span data-stu-id="d11ae-128">Then determine which NuGet package they each come from.</span></span>

<span data-ttu-id="d11ae-129">[`project.json`](project-json.md)TXD 'yi destekleyen bir paket oluşturulmasına yardımcı olan özellikler hakkındaki ayrıntılar için konusuna bakın `dotnet` .</span><span class="sxs-lookup"><span data-stu-id="d11ae-129">See the [`project.json`](project-json.md) topic for details on features that help in the creation of a package that supports the `dotnet` TxM.</span></span>

> [!Important]
> <span data-ttu-id="d11ae-130">Paketinizin PCL projeleriyle çalışmayı amaçlıyorsa, `dotnet` uyarı ve potansiyel Uyumluluk sorunlarından kaçınmak için bir klasör oluşturmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="d11ae-130">If your package is intended to work with PCL projects, we highly recommend to create a `dotnet` folder, to avoid warnings and potential compatibility issues.</span></span>

## <a name="directory-structure"></a><span data-ttu-id="d11ae-131">Dizin yapısı</span><span class="sxs-lookup"><span data-stu-id="d11ae-131">Directory structure</span></span>

<span data-ttu-id="d11ae-132">Bu biçimi kullanan NuGet paketleri, aşağıdaki iyi bilinen klasör ve davranışlara sahiptir:</span><span class="sxs-lookup"><span data-stu-id="d11ae-132">NuGet packages using this format have the following well-known folder and behaviors:</span></span>

| <span data-ttu-id="d11ae-133">Klasör</span><span class="sxs-lookup"><span data-stu-id="d11ae-133">Folder</span></span> | <span data-ttu-id="d11ae-134">Davranışlar</span><span class="sxs-lookup"><span data-stu-id="d11ae-134">Behaviors</span></span> |
| --- | --- |
| <span data-ttu-id="d11ae-135">Oluşturma</span><span class="sxs-lookup"><span data-stu-id="d11ae-135">Build</span></span> | <span data-ttu-id="d11ae-136">Bu klasördeki MSBuild hedeflerini ve props dosyalarını içerir, ancak başka bir değişiklik yoktur.</span><span class="sxs-lookup"><span data-stu-id="d11ae-136">Contains MSBuild targets and props files in this folder are integrated differently into the project, but otherwise there is no change.</span></span> |
| <span data-ttu-id="d11ae-137">Araçlar</span><span class="sxs-lookup"><span data-stu-id="d11ae-137">Tools</span></span> | <span data-ttu-id="d11ae-138">`install.ps1` ve `uninstall.ps1` çalıştırılmaz.</span><span class="sxs-lookup"><span data-stu-id="d11ae-138">`install.ps1` and `uninstall.ps1` are not run.</span></span> <span data-ttu-id="d11ae-139">`init.ps1` her zaman sahip olduğu için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="d11ae-139">`init.ps1` works as it always has.</span></span> |
| <span data-ttu-id="d11ae-140">Content</span><span class="sxs-lookup"><span data-stu-id="d11ae-140">Content</span></span> | <span data-ttu-id="d11ae-141">İçerik, kullanıcının projesine otomatik olarak kopyalanmaz.</span><span class="sxs-lookup"><span data-stu-id="d11ae-141">Content is not copied automatically into a user's project.</span></span> <span data-ttu-id="d11ae-142">Projeye dahil içerik ekleme desteği sonraki bir sürüm için planlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d11ae-142">Support for content inclusion in the project is planned for a later release.</span></span> |
| <span data-ttu-id="d11ae-143">LIB</span><span class="sxs-lookup"><span data-stu-id="d11ae-143">Lib</span></span> | <span data-ttu-id="d11ae-144">Birçok paket için, `lib` NuGet 2. x içinde yaptığı gibi, ancak içinde hangi adların kullanılabileceği ve paketler kullanılırken doğru alt klasörü seçmek için daha iyi bir mantık ile aynı şekilde çalışacak.</span><span class="sxs-lookup"><span data-stu-id="d11ae-144">For many packages the `lib` works the same way it does in NuGet 2.x, but with expanded options for what names can be used inside it and better logic for picking the correct sub-folder when consuming packages.</span></span> <span data-ttu-id="d11ae-145">Ancak, ile birlikte kullanıldığında, klasörü, `ref` `lib` klasördeki derlemeler tarafından tanımlanan yüzey alanını uygulayan derlemeler içerir `ref` .</span><span class="sxs-lookup"><span data-stu-id="d11ae-145">However, when used in conjunction with `ref`, the `lib` folder contains assemblies that implement the surface area defined by the assemblies in the `ref` folder.</span></span> |
| <span data-ttu-id="d11ae-146">Ref</span><span class="sxs-lookup"><span data-stu-id="d11ae-146">Ref</span></span> | <span data-ttu-id="d11ae-147">`ref` , bir uygulamanın derlenmesi için ortak yüzeyi (genel türler ve Yöntemler) tanımlayan .NET derlemelerini içeren isteğe bağlı bir klasördür.</span><span class="sxs-lookup"><span data-stu-id="d11ae-147">`ref` is an optional folder that contains .NET assemblies defining the public surface (public types and methods) for an application to compile against.</span></span> <span data-ttu-id="d11ae-148">Bu klasördeki derlemeler uygulamaya sahip olmayabilir, yalnızca derleyicinin yüzey alanını tanımlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d11ae-148">The assemblies in this folder may have no implementation, they are purely used to define surface area for the compiler.</span></span> <span data-ttu-id="d11ae-149">Pakette hiçbir klasör yoksa, `ref` `lib` hem başvuru derlemesi hem de uygulama bütünleştirilmiş kodu olur.</span><span class="sxs-lookup"><span data-stu-id="d11ae-149">If the package has no `ref` folder, then the `lib` is both the reference assembly and the implementation assembly.</span></span> |
| <span data-ttu-id="d11ae-150">Zamanları</span><span class="sxs-lookup"><span data-stu-id="d11ae-150">Runtimes</span></span> | <span data-ttu-id="d11ae-151">`runtimes` , CPU mimarisi ve işletim sistemine özel veya başka türlü platforma bağımlı ikili dosyalar gibi işletim sistemi özel kodu içeren isteğe bağlı bir klasördür.</span><span class="sxs-lookup"><span data-stu-id="d11ae-151">`runtimes` is an optional folder that contains OS specific code, such as CPU architecture and OS specific or otherwise platform-dependent binaries.</span></span> |

## <a name="msbuild-targets-and-props-files-in-packages"></a><span data-ttu-id="d11ae-152">Paketlerindeki MSBuild hedefleri ve props dosyaları</span><span class="sxs-lookup"><span data-stu-id="d11ae-152">MSBuild targets and props files in packages</span></span>

<span data-ttu-id="d11ae-153">NuGet paketleri `.targets` ve `.props` paketin yüklendiği herhangi bir MSBuild projesine aktarılan dosyalar içerebilir.</span><span class="sxs-lookup"><span data-stu-id="d11ae-153">NuGet packages can contain `.targets` and `.props` files which are imported into any MSBuild project that the package is installed into.</span></span> <span data-ttu-id="d11ae-154">NuGet 2. x sürümünde, bu ekleme `<Import>` deyimleri `.csproj` dosyada yapıldı, NuGet 3,0 ' de belirli bir "projeye yükleme" eylemi yok.</span><span class="sxs-lookup"><span data-stu-id="d11ae-154">In NuGet 2.x, this was done by injecting `<Import>` statements into the `.csproj` file, in NuGet 3.0 there is no specific "installation to project" action.</span></span> <span data-ttu-id="d11ae-155">Bunun yerine, paket geri yükleme işlemi iki dosya `[projectname].nuget.props` ve yazar `[projectname].NuGet.targets` .</span><span class="sxs-lookup"><span data-stu-id="d11ae-155">Instead the package restore process writes two files `[projectname].nuget.props` and `[projectname].NuGet.targets`.</span></span>

<span data-ttu-id="d11ae-156">MSBuild, bu iki dosyanın arandığını bilir ve bunları otomatik olarak proje yapı işleminin sonuna ve sonuna yakın bir şekilde içeri aktarır.</span><span class="sxs-lookup"><span data-stu-id="d11ae-156">MSBuild knows to look for these two files and automatically imports them near the beginning and near the end of the project build process.</span></span> <span data-ttu-id="d11ae-157">Bu, NuGet 2. x için çok benzer bir davranış sağlar, ancak bir büyük farklılık *vardır: Bu durumda hiçbir garanti edilen hedef/props dosyası* yoktur.</span><span class="sxs-lookup"><span data-stu-id="d11ae-157">This provides very similar behavior to NuGet 2.x, but with one major difference: *there is no guaranteed order of targets/props files in this case*.</span></span> <span data-ttu-id="d11ae-158">Bununla birlikte, MSBuild, tanımlamayı ve özniteliklerini kullanarak sıralama yollarını `BeforeTargets` sağlar `AfterTargets` `<Target>` (bkz. [target öğesi (MSBuild)](/visualstudio/msbuild/target-element-msbuild).</span><span class="sxs-lookup"><span data-stu-id="d11ae-158">However, MSBuild does provide ways to order targets through the `BeforeTargets` and `AfterTargets` attributes of the `<Target>` definition (see [Target Element (MSBuild)](/visualstudio/msbuild/target-element-msbuild).</span></span>

## <a name="lib-and-ref"></a><span data-ttu-id="d11ae-159">LIB ve ref</span><span class="sxs-lookup"><span data-stu-id="d11ae-159">Lib and Ref</span></span>

<span data-ttu-id="d11ae-160">`lib`NuGet v3 'de klasörün davranışı önemli ölçüde değişmemiştir.</span><span class="sxs-lookup"><span data-stu-id="d11ae-160">The behavior of the `lib` folder hasn't changed significantly in NuGet v3.</span></span> <span data-ttu-id="d11ae-161">Ancak, tüm derlemeler bir TXD adlı alt klasörler içinde olmalıdır ve artık doğrudan klasörün altına yerleştirilemez `lib` .</span><span class="sxs-lookup"><span data-stu-id="d11ae-161">However, all assemblies must be within sub-folders named after a TxM, and can no longer be placed directly under the `lib` folder.</span></span> <span data-ttu-id="d11ae-162">TXD, bir paketteki belirli bir varlığın çalışması beklenen platformun adıdır.</span><span class="sxs-lookup"><span data-stu-id="d11ae-162">A TxM is the name of a platform that a given asset in a package is supposed to work for.</span></span> <span data-ttu-id="d11ae-163">Mantıksal olarak bunlar hedef çerçeve adları (TFM) uzantısıdır,,, `net45` `net46` `netcore50` ve `dnxcore50` Tüm txms örnekleridir (bkz. [hedef çerçeveler](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="d11ae-163">Logically these are an extension of the Target Framework Monikers (TFM) e.g. `net45`, `net46`, `netcore50`, and `dnxcore50` are all examples of TxMs (see [Target Frameworks](../reference/target-frameworks.md).</span></span> <span data-ttu-id="d11ae-164">TXD, bir çerçeveye (TFA) ve diğer platforma özgü yüzey alanları için de başvurabilir.</span><span class="sxs-lookup"><span data-stu-id="d11ae-164">TxM can refer to a framework (TFM) as well as other platform-specific surface areas.</span></span> <span data-ttu-id="d11ae-165">Örneğin UWP TXA (), `uap10.0` .net Surface alanını ve UWP uygulamaları Için Windows Surface alanını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d11ae-165">For example the UWP TxM (`uap10.0`) represents the .NET surface area as well as the Windows surface area for UWP applications.</span></span>

<span data-ttu-id="d11ae-166">Örnek LIB yapısı:</span><span class="sxs-lookup"><span data-stu-id="d11ae-166">An example lib structure:</span></span>

```
lib
├───net40
│       MyLibrary.dll
└───wp81
        MyLibrary.dll
```

<span data-ttu-id="d11ae-167">`lib`Klasör, çalışma zamanında kullanılan derlemeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="d11ae-167">The `lib` folder contains assemblies that are used at runtime.</span></span> <span data-ttu-id="d11ae-168">Çoğu paket için, `lib` her hedef TxMs 'nin altındaki bir klasör gereklidir.</span><span class="sxs-lookup"><span data-stu-id="d11ae-168">For most packages a folder under `lib` for each of the target TxMs is all that is required.</span></span>

## <a name="ref"></a><span data-ttu-id="d11ae-169">Ref</span><span class="sxs-lookup"><span data-stu-id="d11ae-169">Ref</span></span>

<span data-ttu-id="d11ae-170">Bazen derleme sırasında farklı bir derlemenin kullanılması gereken durumlar vardır (.NET başvuru derlemeleri bunu bugün yapın).</span><span class="sxs-lookup"><span data-stu-id="d11ae-170">There are sometimes cases where a different assembly should be used during compilation (.NET Reference Assemblies do this today).</span></span> <span data-ttu-id="d11ae-171">Bu gibi durumlarda, `ref` ("başvuru derlemeleri" için kısa) adlı bir üst düzey klasör kullanın.</span><span class="sxs-lookup"><span data-stu-id="d11ae-171">For those cases, use a top-level folder called `ref` (short for "Reference Assemblies").</span></span>

<span data-ttu-id="d11ae-172">Çoğu paket yazarı klasöre gerek kalmaz `ref` .</span><span class="sxs-lookup"><span data-stu-id="d11ae-172">Most package authors don't require the `ref` folder.</span></span> <span data-ttu-id="d11ae-173">Derleme ve IntelliSense için tutarlı bir yüzey alanı sağlaması gereken, ancak farklı TxMs için farklı bir uygulamaya sahip olan paketler için yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="d11ae-173">It is useful for packages that need to provide a consistent surface area for compilation and IntelliSense but then have different implementation for different TxMs.</span></span> <span data-ttu-id="d11ae-174">Bunun en büyük kullanım durumu, `System.*` NuGet üzerinde .NET Core gönderimi kapsamında üretilen paketlerdir.</span><span class="sxs-lookup"><span data-stu-id="d11ae-174">The biggest use case of this are the `System.*` packages that are being produced as part of shipping .NET Core on NuGet.</span></span> <span data-ttu-id="d11ae-175">Bu paketlerin, tutarlı bir başvuru derlemeleri kümesiyle birleştirilmiş çeşitli uygulamaları vardır.</span><span class="sxs-lookup"><span data-stu-id="d11ae-175">These packages have various implementations that are being unified by a consistent set of ref assemblies.</span></span>

<span data-ttu-id="d11ae-176">Genel olarak, klasöre eklenen derlemeler `ref` derleyiciye geçirilen başvuru derlemelerdir.</span><span class="sxs-lookup"><span data-stu-id="d11ae-176">Mechanically, the assemblies included in the `ref` folder are the reference assemblies being passed to the compiler.</span></span> <span data-ttu-id="d11ae-177">csc.exe kullananlar için [C#/Reference seçenek](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) anahtarına geçirdiğimiz derlemelerdir.</span><span class="sxs-lookup"><span data-stu-id="d11ae-177">For those of you who have used csc.exe these are the assemblies we are passing to the [C# /reference option](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) switch.</span></span>

<span data-ttu-id="d11ae-178">Klasörün yapısı, `ref` `lib` Örneğin:</span><span class="sxs-lookup"><span data-stu-id="d11ae-178">The structure of the `ref` folder is the same as `lib`, for example:</span></span>

```
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
```

<span data-ttu-id="d11ae-179">Bu örnekte, `ref` dizinlerdeki derlemelerin hepsi aynı olur.</span><span class="sxs-lookup"><span data-stu-id="d11ae-179">In this example the assemblies in the `ref` directories would all be identical.</span></span>

## <a name="runtimes"></a><span data-ttu-id="d11ae-180">Zamanları</span><span class="sxs-lookup"><span data-stu-id="d11ae-180">Runtimes</span></span>

<span data-ttu-id="d11ae-181">Çalışma zamanları klasörü, genellikle Işletim sistemi ve CPU mimarisine göre tanımlanan belirli "çalışma zamanları" üzerinde çalışmak için gereken derlemeleri ve yerel kitaplıkları içerir.</span><span class="sxs-lookup"><span data-stu-id="d11ae-181">The runtimes folder contains assemblies and native libraries required to run on specific "runtimes", which are generally defined by Operating System and CPU architecture.</span></span> <span data-ttu-id="d11ae-182">Bu çalışma zamanları,,, vb. [çalışma zamanı tanımlayıcıları (RID 'ler)](/dotnet/core/rid-catalog) kullanılarak tanımlanır `win` `win-x86` `win7-x86` `win8-64` .</span><span class="sxs-lookup"><span data-stu-id="d11ae-182">These runtimes are identified using [Runtime Identifiers (RIDs)](/dotnet/core/rid-catalog) such as `win`, `win-x86`, `win7-x86`, `win8-64`, etc.</span></span>

## <a name="native-helpers-to-use-platform-specific-apis"></a><span data-ttu-id="d11ae-183">Platforma özgü API 'Leri kullanmak için yerel yardımcılar</span><span class="sxs-lookup"><span data-stu-id="d11ae-183">Native helpers to use platform-specific APIs</span></span>

<span data-ttu-id="d11ae-184">Aşağıdaki örnek, birkaç platform için tamamen yönetilen bir uygulamaya sahip olan bir paketi gösterir, ancak Windows 8 ' de Windows 8 ' e özgü yerel API 'lerde çağırabildiği yerel yardımcıları kullanır.</span><span class="sxs-lookup"><span data-stu-id="d11ae-184">The following example shows a package that has a purely managed implementation for several platforms, but uses native helpers on Windows 8 where it can call into Windows 8-specific native APIs.</span></span>

```
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
```

<span data-ttu-id="d11ae-185">Yukarıdaki paket verildiğinde aşağıdaki şeyler meydana gelir:</span><span class="sxs-lookup"><span data-stu-id="d11ae-185">Given the above package the following things happen:</span></span>

- <span data-ttu-id="d11ae-186">Windows 8 ' de değilse, `lib/net40/MyLibrary.dll` derleme kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d11ae-186">When not on Windows 8 the `lib/net40/MyLibrary.dll` assembly is used.</span></span>

- <span data-ttu-id="d11ae-187">Windows 8 ' de `runtimes/win8-<architecture>/lib/MyLibrary.dll` kullanılır ve `native/MyNativeHelper.dll` derleme çıktısına kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="d11ae-187">When on Windows 8 the `runtimes/win8-<architecture>/lib/MyLibrary.dll` is used and the `native/MyNativeHelper.dll` is copied to the output of your build.</span></span>

<span data-ttu-id="d11ae-188">Derlemenin Yukarıdaki örnekte, çalışma `lib/net40` zamanları klasöründeki derlemeler, Windows 8 ' e özgü API 'leri çağırmak için yerel yardımcı derlemeye p/Invoke olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="d11ae-188">In the example above the `lib/net40` assembly is purely managed code, whilst the assemblies in the runtimes folder will p/invoke into the native helper assembly to call APIs specific to Windows 8.</span></span>

<span data-ttu-id="d11ae-189">Yalnızca tek bir `lib` klasör çekilir, bu nedenle çalışma zamanına özgü bir klasör varsa, çalışma zamanında özel olmayan bir klasör seçilir `lib` .</span><span class="sxs-lookup"><span data-stu-id="d11ae-189">Only a single `lib` folder is ever be picked, so if there is a runtime specific folder it's chosen over non-runtime specific `lib`.</span></span> <span data-ttu-id="d11ae-190">Yerel klasör, varsa, derleme çıktısına kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="d11ae-190">The native folder is additive, if it exists it's copied to the output of the build.</span></span>

## <a name="managed-wrapper"></a><span data-ttu-id="d11ae-191">Yönetilen sarmalayıcı</span><span class="sxs-lookup"><span data-stu-id="d11ae-191">Managed wrapper</span></span>

<span data-ttu-id="d11ae-192">Çalışma zamanlarını kullanmanın başka bir yolu da, yerel bir derleme üzerinde yalnızca yönetilen bir sarmalayıcı olan bir paket göndermektedir.</span><span class="sxs-lookup"><span data-stu-id="d11ae-192">Another way to use runtimes is to ship a package that is purely a managed wrapper over a native assembly.</span></span> <span data-ttu-id="d11ae-193">Bu senaryoda, aşağıdaki gibi bir paket oluşturursunuz:</span><span class="sxs-lookup"><span data-stu-id="d11ae-193">In this scenario you create a package like the following:</span></span>

```
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
```

<span data-ttu-id="d11ae-194">Bu durumda, `lib` ilgili yerel derlemeye bağlı olmayan bu pakette hiçbir uygulama olmadığı için, bu klasörde en üst düzey bir klasör yoktur.</span><span class="sxs-lookup"><span data-stu-id="d11ae-194">In this case there is no top-level `lib` folder as that folder as there is no implementation of this package that doesn't rely on the corresponding native assembly.</span></span> <span data-ttu-id="d11ae-195">Yönetilen derleme, `MyLibrary.dll` her iki durumda da tam olarak aynıysa, bunu en üst düzey klasöre koyabiliriz `lib` , ancak yerel bir derlemenin olmaması, paketin, Win-x86 veya Win-x64 olmayan bir platforma yüklenmişse paketin yükleme başarısız olmasına neden olmadığı için, en üst düzey lib kullanılır ancak hiçbir yerel derleme kopyalanmaz.</span><span class="sxs-lookup"><span data-stu-id="d11ae-195">If the managed assembly, `MyLibrary.dll`, was exactly the same in both of these cases then we could put it in a top level `lib` folder, but because the lack of a native assembly doesn't cause the package to fail installing if it was installed on a platform that wasn't win-x86 or win-x64 then the top level lib would be used but no native assembly would be copied.</span></span>

## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a><span data-ttu-id="d11ae-196">NuGet 2 ve NuGet 3 için yazma paketleri</span><span class="sxs-lookup"><span data-stu-id="d11ae-196">Authoring packages for NuGet 2 and NuGet 3</span></span>

<span data-ttu-id="d11ae-197">Çalıştıran projeler tarafından, ve kullanarak paketler tarafından tüketilen bir paket oluşturmak istiyorsanız `packages.config` `project.json` aşağıdakiler geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="d11ae-197">If you want to create a package that can be consumed by projects using `packages.config` as well as packages using `project.json` then the following apply:</span></span>

- <span data-ttu-id="d11ae-198">Ref ve çalışma zamanları yalnızca NuGet 3 ' te çalışır.</span><span class="sxs-lookup"><span data-stu-id="d11ae-198">Ref and runtimes only work on NuGet 3.</span></span> <span data-ttu-id="d11ae-199">Bunlar her ikisi de NuGet 2 tarafından yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="d11ae-199">They are both ignored by NuGet 2.</span></span>

- <span data-ttu-id="d11ae-200">Kullanamazsınız `install.ps1` veya `uninstall.ps1` çalışamaz.</span><span class="sxs-lookup"><span data-stu-id="d11ae-200">You cannot rely on `install.ps1` or `uninstall.ps1` to function.</span></span> <span data-ttu-id="d11ae-201">Bu dosyalar kullanılırken yürütülür `packages.config` , ancak ile yok sayılır `project.json` .</span><span class="sxs-lookup"><span data-stu-id="d11ae-201">These files execute when using `packages.config`, but are ignored with `project.json`.</span></span> <span data-ttu-id="d11ae-202">Bu nedenle, paketinizin çalışır duruma girmeden kullanılabilir olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d11ae-202">So your package needs to be usable without them running.</span></span> <span data-ttu-id="d11ae-203">`init.ps1` NuGet 3 ' te hala çalışır.</span><span class="sxs-lookup"><span data-stu-id="d11ae-203">`init.ps1` still runs on NuGet 3.</span></span>

- <span data-ttu-id="d11ae-204">Hedefler ve props yüklemesi farklıdır, bu nedenle paketinizin her iki istemcide de beklendiği gibi çalıştığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="d11ae-204">Targets and Props installation is different, so make sure that your package works as expected on both clients.</span></span>

- <span data-ttu-id="d11ae-205">LIB alt dizinleri NuGet 3 ' te bir TXD olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d11ae-205">Subdirectories of lib must be a TxM in NuGet 3.</span></span> <span data-ttu-id="d11ae-206">Kitaplıkları klasörün köküne yerleştirebilirsiniz `lib` .</span><span class="sxs-lookup"><span data-stu-id="d11ae-206">You cannot place libraries at the root of the `lib` folder.</span></span>

- <span data-ttu-id="d11ae-207">İçerik NuGet 3 ile otomatik olarak kopyalanmaz.</span><span class="sxs-lookup"><span data-stu-id="d11ae-207">Content is not copied automatically with NuGet 3.</span></span> <span data-ttu-id="d11ae-208">Paketinizin tüketicileri dosyaları kopyalayabilir veya bir görev Çalıştırıcısı gibi bir aracı kullanarak dosyaları kopyalamayı otomatik hale getirebilir.</span><span class="sxs-lookup"><span data-stu-id="d11ae-208">Consumers of your package could copy the files themselves or use a tool like a task runner to automate copying the files.</span></span>

- <span data-ttu-id="d11ae-209">Kaynak ve yapılandırma dosyası dönüştürmeleri NuGet 3 tarafından çalıştırılmaz.</span><span class="sxs-lookup"><span data-stu-id="d11ae-209">Source and config file transforms are not run by NuGet 3.</span></span>

<span data-ttu-id="d11ae-210">NuGet 2 ve 3 ' ü destekliyorsanız, `minClientVersion` paketinizin üzerinde çalıştığından NuGet 2 istemcisinin en düşük sürümü olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d11ae-210">If you are supporting NuGet 2 and 3 then your `minClientVersion` should be the lowest version of NuGet 2 client that your package works on.</span></span> <span data-ttu-id="d11ae-211">Var olan bir pakette değişiklik olması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="d11ae-211">In the case of an existing package it shouldn't need to change.</span></span>
