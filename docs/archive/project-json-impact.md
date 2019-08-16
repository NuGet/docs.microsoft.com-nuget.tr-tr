---
title: NuGet paket yazarları üzerinde Project. JSON etkisi
description: NuGet 3. x içindeki Project. JSON uygulamasının uygulamanın desteklenmeyen özellikler, içerik ve paket biçimi gibi paket yazarlarıyla nasıl etkilendiğine ilişkin ayrıntılar.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 34b08f06f04efdcf7bf73efc2cbdb5a5494ae2d9
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488192"
---
# <a name="impact-of-projectjson-when-creating-packages"></a><span data-ttu-id="d1f95-103">Paket oluştururken Project. json ' un etkileri</span><span class="sxs-lookup"><span data-stu-id="d1f95-103">Impact of project.json when creating packages</span></span>

> [!Important]
> <span data-ttu-id="d1f95-104">Bu içerik kullanımdan kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="d1f95-104">This content is deprecated.</span></span> <span data-ttu-id="d1f95-105">Projeler ya `packages.config` ya da packagereference biçimlerini kullanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d1f95-105">Projects should use either the `packages.config` or PackageReference formats.</span></span>

<span data-ttu-id="d1f95-106">NuGet `project.json` 3 + ' de kullanılan sistem, paket yazarlarını aşağıdaki bölümlerde açıklandığı gibi çeşitli yollarla etkiler.</span><span class="sxs-lookup"><span data-stu-id="d1f95-106">The `project.json` system used in NuGet 3+ affects package authors in several ways as described in the following sections.</span></span>

## <a name="changes-affecting-existing-packages-usage"></a><span data-ttu-id="d1f95-107">Mevcut paketlerin kullanımını etkileyen değişiklikler</span><span class="sxs-lookup"><span data-stu-id="d1f95-107">Changes affecting existing packages usage</span></span>

<span data-ttu-id="d1f95-108">Geleneksel NuGet paketleri geçişli dünyaya taşınmayan bir özellik kümesini destekler.</span><span class="sxs-lookup"><span data-stu-id="d1f95-108">Traditional NuGet packages support a set of features that are not carried over to the transitive world.</span></span>

### <a name="install-and-uninstall-scripts-are-ignored"></a><span data-ttu-id="d1f95-109">Yükleme ve kaldırma betikleri yoksayıldı</span><span class="sxs-lookup"><span data-stu-id="d1f95-109">Install and uninstall scripts are ignored</span></span>

<span data-ttu-id="d1f95-110">[Bağımlılık çözümlemesi](../concepts/dependency-resolution.md#dependency-resolution-with-packagereference)bölümünde açıklanan geçişli geri yükleme modelinin "paket yükleme süresi" kavramı yoktur.</span><span class="sxs-lookup"><span data-stu-id="d1f95-110">The transitive restore model, described in [Dependency resolution](../concepts/dependency-resolution.md#dependency-resolution-with-packagereference), does not have a concept of "package install time".</span></span> <span data-ttu-id="d1f95-111">Bir paket mevcut değil veya yok, ancak paket yüklendiğinde oluşan tutarlı bir işlem yok.</span><span class="sxs-lookup"><span data-stu-id="d1f95-111">A package is either present or not present, but there is no consistent process that occurs when a package is installed.</span></span>

<span data-ttu-id="d1f95-112">Ayrıca, yüklenen betikler yalnızca Visual Studio 'da desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="d1f95-112">Also, install scripts were supported only in Visual Studio.</span></span> <span data-ttu-id="d1f95-113">Diğer Ides 'ler, bu tür betikleri desteklemeyi denemek için Visual Studio genişletilebilirlik API 'sini sahte ve ortak düzenleyiciler ve komut satırı araçlarında hiçbir destek yoktu.</span><span class="sxs-lookup"><span data-stu-id="d1f95-113">Other IDEs had to mock the Visual Studio extensibility API to attempt to support such scripts, and no support was available in common editors and command-line tools.</span></span>

### <a name="content-transforms-are-not-supported"></a><span data-ttu-id="d1f95-114">İçerik dönüştürmeleri desteklenmez</span><span class="sxs-lookup"><span data-stu-id="d1f95-114">Content transforms are not supported</span></span>

<span data-ttu-id="d1f95-115">Betikleri yüklemeye benzer şekilde, dönüşümler paket yüklemesi üzerinde çalışır ve genellikle ıdempotent değildir.</span><span class="sxs-lookup"><span data-stu-id="d1f95-115">Similar to install scripts, transforms run on package install and are typically not idempotent.</span></span> <span data-ttu-id="d1f95-116">Artık bir yük süresi olmadığından, XDT dönüşümü ve benzer özellikler desteklenmez ve bu tür bir paket geçişli bir senaryoda kullanılıyorsa yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="d1f95-116">Since there is no install time anymore, XDT Transform and similar features are not supported, and are ignored if such a package is used in a transitive scenario.</span></span>

### <a name="content"></a><span data-ttu-id="d1f95-117">İçerik</span><span class="sxs-lookup"><span data-stu-id="d1f95-117">Content</span></span>

<span data-ttu-id="d1f95-118">Geleneksel NuGet paketleri, kaynak kodu ve yapılandırma dosyaları gibi içerik dosyalarını aktarıyor.</span><span class="sxs-lookup"><span data-stu-id="d1f95-118">Traditional NuGet packages are shipping content files such as source code and configuration files.</span></span> <span data-ttu-id="d1f95-119">Genellikle iki senaryoda kullanılır:</span><span class="sxs-lookup"><span data-stu-id="d1f95-119">There are used typically in two scenarios:</span></span>

1. <span data-ttu-id="d1f95-120">Kullanıcının bunları daha sonra düzenleyebilmesi için ilk dosyalar projeye bırakılmış.</span><span class="sxs-lookup"><span data-stu-id="d1f95-120">Initial files dropped into the project so the user can edit them at a later time.</span></span> <span data-ttu-id="d1f95-121">Ortak örnek, varsayılan yapılandırma dosyalarıdır.</span><span class="sxs-lookup"><span data-stu-id="d1f95-121">The common example is default configuration files.</span></span>

1. <span data-ttu-id="d1f95-122">Projede yüklü olan derlemeler için companmı olarak kullanılan içerik dosyaları.</span><span class="sxs-lookup"><span data-stu-id="d1f95-122">Content files used as companions to the assemblies installed in the project.</span></span> <span data-ttu-id="d1f95-123">Buradaki örnek, bir derleme tarafından kullanılan bir logo görüntüsü olacaktır.</span><span class="sxs-lookup"><span data-stu-id="d1f95-123">The example here would be a logo image used by an assembly.</span></span>

<span data-ttu-id="d1f95-124">İçerik desteği şu anda betiklerin ve dönüştürmelerdeki benzer nedenlerle devre dışıdır, ancak içerik için destek tasarlama sürecimiz vardır.</span><span class="sxs-lookup"><span data-stu-id="d1f95-124">Support for content is currently disabled for similar reasons for scripts and transforms, but we are in the process of designing support for content.</span></span>

<span data-ttu-id="d1f95-125">İçerik dosyaları yine de paketler içinde taşınırlar ve şu anda yok sayılır, ancak son kullanıcı bunları yine de doğru noktaya kopyalayabilir.</span><span class="sxs-lookup"><span data-stu-id="d1f95-125">Content files can still be carried inside the packages, and are ignored currently, however the end user can still copy them into the right spot.</span></span>

<span data-ttu-id="d1f95-126">İçerik dosyalarını geri getirme tekliflerinden birini görebilir ve ilerleme durumunu takip edebilirsiniz: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627).</span><span class="sxs-lookup"><span data-stu-id="d1f95-126">You can see one of the proposals for bringing back content files, and follow its progress, here: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627).</span></span>

## <a name="impact-for-package-authors"></a><span data-ttu-id="d1f95-127">Paket yazarları için etki</span><span class="sxs-lookup"><span data-stu-id="d1f95-127">Impact for package authors</span></span>

<span data-ttu-id="d1f95-128">Yukarıdaki özellikleri kullanan paketlerin farklı bir mekanizma kullanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d1f95-128">Packages using the above features would have to use a different mechanism.</span></span> <span data-ttu-id="d1f95-129">Bunun için en yaygın faydalı mekanizma, tam olarak desteklenmeye devam eden MSBuild hedefleri/props olacaktır.</span><span class="sxs-lookup"><span data-stu-id="d1f95-129">The most commonly useful mechanism for this would be the MSBuild targets/props that continues to get fully supported.</span></span> <span data-ttu-id="d1f95-130">Yapı sistemi, pakette diğer kuralları da çekmeyi seçebilir.</span><span class="sxs-lookup"><span data-stu-id="d1f95-130">The build system can choose to pick up other conventions in the package.</span></span> <span data-ttu-id="d1f95-131">Bu, MSBuild hedeflerinin yanı sıra Roslyn Çözümleyicileri de desteklenir.</span><span class="sxs-lookup"><span data-stu-id="d1f95-131">This is how MSBuild targets are supported as well as Roslyn analyzers.</span></span> <span data-ttu-id="d1f95-132">`packages.config` Ve`project.json` senaryolarına yönelik hedefleri ve Çözümleyicileri destekleyen paketler oluşturmak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="d1f95-132">It is possible to build packages that supports targets and analyzers for `packages.config` and `project.json` scenarios.</span></span>

<span data-ttu-id="d1f95-133">Projeyi kolay bir şekilde değiştirmeye çalışan paketler, genellikle çok sınırlı bir dizi senaryoda çalışır ve bunun yerine paketin nasıl kullanılacağına ilişkin bir Benioku veya bir kılavuz sağlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="d1f95-133">Packages that attempt to modify the project to ease startup typically work in a very limited set of scenarios, and should instead provide a readme, or guidance on how to use the package.</span></span>

<span data-ttu-id="d1f95-134">Birçok mevcut paketin aşağıda açıklanan paket biçimini kullanması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="d1f95-134">Most existing packages should not need to use the package format described below.</span></span>

<span data-ttu-id="d1f95-135">Biçim, yerel içeriği ilk sınıf senaryosu olarak sunar.</span><span class="sxs-lookup"><span data-stu-id="d1f95-135">The format enables native content as a first class scenario.</span></span> <span data-ttu-id="d1f95-136">Bu, yönetilen derlemelerin, hedef platforma bağlı olarak yönetilen derlemelerle birlikte ikili uygulamalar göndermek için donanım uygulamalarına yakın dayanmasıdır.</span><span class="sxs-lookup"><span data-stu-id="d1f95-136">This means that managed assemblies depend on close to hardware implementations to ship binary implementations alongside the managed assemblies based on the target platform.</span></span> <span data-ttu-id="d1f95-137">Örneğin, System. ıO. Compression paketi bu teknolojinin kullanılmasıyla sorumludur.</span><span class="sxs-lookup"><span data-stu-id="d1f95-137">For example System.IO.Compression package is utilizing this technology.</span></span> [https://www.nuget.org/packages/System.IO.Compression](https://www.nuget.org/packages/System.IO.Compression)

<span data-ttu-id="d1f95-138">Özet ' te, yukarıdaki işlev kesinlikle gerekli değilse, burada açıklanan biçim yalnızca NuGet 3. x + tarafından desteklenene kadar, mevcut paket biçimiyle bir çıkartma önerilir.</span><span class="sxs-lookup"><span data-stu-id="d1f95-138">In summary if the functionality above is not absolutely necessary, we recommend sticking with the existing package format, as the format described here is supported only by NuGet 3.x+.</span></span>

<span data-ttu-id="d1f95-139">Paketler, için dolgu oluşturuluyor aracılığıyla her iki `packages.config` `project.json` senaryo için de çalışacak şekilde oluşturulabilir; ancak, yukarıda bahsedilen kullanım dışı özellikler olmadan paketleri geleneksel olarak yapılandırmak genellikle daha kolay bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="d1f95-139">It would be possible to build packages to work for both `packages.config` and `project.json` scenarios through shimming, however it's often simpler to just structure the packages the traditional way, without the deprecated features mentioned above.</span></span>

## <a name="3x-package-format"></a><span data-ttu-id="d1f95-140">3. x paket biçimi</span><span class="sxs-lookup"><span data-stu-id="d1f95-140">3.x package format</span></span>

<span data-ttu-id="d1f95-141">3\. x paket biçimi, NuGet 2. x ' in ötesinde birkaç ek özellik sağlar:</span><span class="sxs-lookup"><span data-stu-id="d1f95-141">The 3.x package format allows for several additional features beyond NuGet 2.x:</span></span>

1. <span data-ttu-id="d1f95-142">Derleme için kullanılan bir başvuru bütünleştirilmiş kodu ve farklı platformlarda/cihazlarda çalışma zamanı için kullanılan bir uygulama derlemeleri kümesi tanımlama.</span><span class="sxs-lookup"><span data-stu-id="d1f95-142">Defining a reference assembly used for compilation and a set of implementation assemblies used for runtime on different platforms/devices.</span></span> <span data-ttu-id="d1f95-143">Tüketicileriniz için ortak bir yüzey alanı sağlarken platforma özgü API 'lerden yararlanmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="d1f95-143">Which allows you to take advantage of platform specific APIs while providing a common surface area for your consumers.</span></span> <span data-ttu-id="d1f95-144">Bu, özellikle de ara taşınabilir kitaplıkların yazılmasını kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="d1f95-144">Specifically this makes writing intermediate portable libraries easier.</span></span>

1. <span data-ttu-id="d1f95-145">Paketlerin platformlar (işletim sistemleri veya CPU mimarisi) üzerinde özetlemesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="d1f95-145">Allows packages to pivot on platforms e.g. operating systems or CPU architecture.</span></span>

1. <span data-ttu-id="d1f95-146">Platforma özgü uygulamaların eşlik eden paketlere ayrılmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="d1f95-146">Allows for separation of platform specific implementations to companion packages.</span></span>

1. <span data-ttu-id="d1f95-147">Birinci sınıf vatandaşlık olarak yerel bağımlılıkları destekler.</span><span class="sxs-lookup"><span data-stu-id="d1f95-147">Support Native dependencies as a first class citizen.</span></span>
