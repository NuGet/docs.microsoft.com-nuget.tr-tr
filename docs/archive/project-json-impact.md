---
title: NuGet paket yazarları üzerinde project.json etkisi
description: NuGet 3.x'te project.json uygulamasının desteklenmeyen özellikler, içerik ve paket biçimi gibi paket yazarlarını nasıl etkilediğine ilişkin ayrıntılar.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 34b08f06f04efdcf7bf73efc2cbdb5a5494ae2d9
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "69488192"
---
# <a name="impact-of-projectjson-when-creating-packages"></a><span data-ttu-id="5337d-103">Paket oluştururken project.json'un etkisi</span><span class="sxs-lookup"><span data-stu-id="5337d-103">Impact of project.json when creating packages</span></span>

> [!Important]
> <span data-ttu-id="5337d-104">Bu içerik amortismana hazırdır.</span><span class="sxs-lookup"><span data-stu-id="5337d-104">This content is deprecated.</span></span> <span data-ttu-id="5337d-105">Projeler `packages.config` de PackageReference biçimlerini kullanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5337d-105">Projects should use either the `packages.config` or PackageReference formats.</span></span>

<span data-ttu-id="5337d-106">NuGet 3+'da kullanılan `project.json` sistem, aşağıdaki bölümlerde açıklandığı gibi paket yazarlarını çeşitli şekillerde etkiler.</span><span class="sxs-lookup"><span data-stu-id="5337d-106">The `project.json` system used in NuGet 3+ affects package authors in several ways as described in the following sections.</span></span>

## <a name="changes-affecting-existing-packages-usage"></a><span data-ttu-id="5337d-107">Varolan paket kullanımını etkileyen değişiklikler</span><span class="sxs-lookup"><span data-stu-id="5337d-107">Changes affecting existing packages usage</span></span>

<span data-ttu-id="5337d-108">Geleneksel NuGet paketleri, geçişli dünyaya taşınamayan bir dizi özelliği destekler.</span><span class="sxs-lookup"><span data-stu-id="5337d-108">Traditional NuGet packages support a set of features that are not carried over to the transitive world.</span></span>

### <a name="install-and-uninstall-scripts-are-ignored"></a><span data-ttu-id="5337d-109">Komut dosyalarını yükleme ve kaldırma</span><span class="sxs-lookup"><span data-stu-id="5337d-109">Install and uninstall scripts are ignored</span></span>

<span data-ttu-id="5337d-110">[Bağımlılık çözümünde](../concepts/dependency-resolution.md#dependency-resolution-with-packagereference)açıklanan geçişli geri yükleme modelinde "paket yükleme süresi" kavramı yoktur.</span><span class="sxs-lookup"><span data-stu-id="5337d-110">The transitive restore model, described in [Dependency resolution](../concepts/dependency-resolution.md#dependency-resolution-with-packagereference), does not have a concept of "package install time".</span></span> <span data-ttu-id="5337d-111">Paket var veya yok, ancak paket yüklendiğinde oluşan tutarlı bir işlem yoktur.</span><span class="sxs-lookup"><span data-stu-id="5337d-111">A package is either present or not present, but there is no consistent process that occurs when a package is installed.</span></span>

<span data-ttu-id="5337d-112">Ayrıca, yükleme komut dosyaları yalnızca Visual Studio'da desteklendi.</span><span class="sxs-lookup"><span data-stu-id="5337d-112">Also, install scripts were supported only in Visual Studio.</span></span> <span data-ttu-id="5337d-113">Diğer IDA'lar bu tür komut dosyalarını desteklemek için Visual Studio genişletilebilirlik API'si ile alay etmek zorunda kaldı ve ortak editörler ve komut satırı araçlarında destek yoktu.</span><span class="sxs-lookup"><span data-stu-id="5337d-113">Other IDEs had to mock the Visual Studio extensibility API to attempt to support such scripts, and no support was available in common editors and command-line tools.</span></span>

### <a name="content-transforms-are-not-supported"></a><span data-ttu-id="5337d-114">İçerik dönüşümleri desteklenmiyor</span><span class="sxs-lookup"><span data-stu-id="5337d-114">Content transforms are not supported</span></span>

<span data-ttu-id="5337d-115">Komut dosyalarını yüklemeye benzer şekilde, dönüşümler paket yüklemede çalışır ve genellikle idempotent değildir.</span><span class="sxs-lookup"><span data-stu-id="5337d-115">Similar to install scripts, transforms run on package install and are typically not idempotent.</span></span> <span data-ttu-id="5337d-116">Artık yükleme zamanı olmadığından, XDT Dönüşümü ve benzeri özellikler desteklenmez ve böyle bir paket geçişli bir senaryoda kullanılırsa yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="5337d-116">Since there is no install time anymore, XDT Transform and similar features are not supported, and are ignored if such a package is used in a transitive scenario.</span></span>

### <a name="content"></a><span data-ttu-id="5337d-117">İçerik</span><span class="sxs-lookup"><span data-stu-id="5337d-117">Content</span></span>

<span data-ttu-id="5337d-118">Geleneksel NuGet paketleri, kaynak kodu ve yapılandırma dosyaları gibi içerik dosyalarını göndermiştir.</span><span class="sxs-lookup"><span data-stu-id="5337d-118">Traditional NuGet packages are shipping content files such as source code and configuration files.</span></span> <span data-ttu-id="5337d-119">Genellikle iki senaryoda kullanılır:</span><span class="sxs-lookup"><span data-stu-id="5337d-119">There are used typically in two scenarios:</span></span>

1. <span data-ttu-id="5337d-120">Kullanıcının bunları daha sonra düzenlemesi için projeye bırakılan ilk dosyalar.</span><span class="sxs-lookup"><span data-stu-id="5337d-120">Initial files dropped into the project so the user can edit them at a later time.</span></span> <span data-ttu-id="5337d-121">Yaygın örnek varsayılan yapılandırma dosyalarıdır.</span><span class="sxs-lookup"><span data-stu-id="5337d-121">The common example is default configuration files.</span></span>

1. <span data-ttu-id="5337d-122">Projede yüklü olan derlemelere yardımcı olarak kullanılan içerik dosyaları.</span><span class="sxs-lookup"><span data-stu-id="5337d-122">Content files used as companions to the assemblies installed in the project.</span></span> <span data-ttu-id="5337d-123">Buradaki örnek, bir derleme tarafından kullanılan bir logo görüntüsü olacaktır.</span><span class="sxs-lookup"><span data-stu-id="5337d-123">The example here would be a logo image used by an assembly.</span></span>

<span data-ttu-id="5337d-124">İçerik desteği şu anda komut dosyaları ve dönüşümler için benzer nedenlerle devre dışı bırakılmıştır, ancak içerik için destek tasarlama aşamasındayız.</span><span class="sxs-lookup"><span data-stu-id="5337d-124">Support for content is currently disabled for similar reasons for scripts and transforms, but we are in the process of designing support for content.</span></span>

<span data-ttu-id="5337d-125">İçerik dosyaları hala paketler içinde taşınabilir ve şu anda yoksayılır, ancak son kullanıcı bunları yine de doğru noktaya kopyalayabilir.</span><span class="sxs-lookup"><span data-stu-id="5337d-125">Content files can still be carried inside the packages, and are ignored currently, however the end user can still copy them into the right spot.</span></span>

<span data-ttu-id="5337d-126">İçerik dosyalarını geri getirmek için önerilerden birini görebilir ve [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)ilerlemeyi buradan takip edebilirsiniz: .</span><span class="sxs-lookup"><span data-stu-id="5337d-126">You can see one of the proposals for bringing back content files, and follow its progress, here: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627).</span></span>

## <a name="impact-for-package-authors"></a><span data-ttu-id="5337d-127">Paket yazarlar için etki</span><span class="sxs-lookup"><span data-stu-id="5337d-127">Impact for package authors</span></span>

<span data-ttu-id="5337d-128">Yukarıdaki özellikleri kullanan paketlerfarklı bir mekanizma kullanmak zorunda kalacak.</span><span class="sxs-lookup"><span data-stu-id="5337d-128">Packages using the above features would have to use a different mechanism.</span></span> <span data-ttu-id="5337d-129">Bunun için en yaygın olarak yararlı mekanizma tam olarak desteklenmeye devam msbuild hedefleri / sahne olacaktır.</span><span class="sxs-lookup"><span data-stu-id="5337d-129">The most commonly useful mechanism for this would be the MSBuild targets/props that continues to get fully supported.</span></span> <span data-ttu-id="5337d-130">Yapı sistemi paketteki diğer kuralları almayı seçebilir.</span><span class="sxs-lookup"><span data-stu-id="5337d-130">The build system can choose to pick up other conventions in the package.</span></span> <span data-ttu-id="5337d-131">Bu şekilde MSBuild hedefleri yanı sıra Roslyn analizörleri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="5337d-131">This is how MSBuild targets are supported as well as Roslyn analyzers.</span></span> <span data-ttu-id="5337d-132">Hedefleri ve çözümleyicileri `packages.config` destekleyen `project.json` paketler oluşturmak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="5337d-132">It is possible to build packages that supports targets and analyzers for `packages.config` and `project.json` scenarios.</span></span>

<span data-ttu-id="5337d-133">Başlatmayı kolaylaştırmak için projeyi değiştirmeye çalışan paketler genellikle çok sınırlı bir senaryo kümesinde çalışır ve bunun yerine bir okuma veya paketin nasıl kullanılacağı nasıI rehberlik sağlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="5337d-133">Packages that attempt to modify the project to ease startup typically work in a very limited set of scenarios, and should instead provide a readme, or guidance on how to use the package.</span></span>

<span data-ttu-id="5337d-134">Varolan paketlerin çoğunun aşağıda açıklanan paket biçimini kullanması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="5337d-134">Most existing packages should not need to use the package format described below.</span></span>

<span data-ttu-id="5337d-135">Biçim, birinci sınıf bir senaryo olarak yerel içeriği etkinleştirirken.</span><span class="sxs-lookup"><span data-stu-id="5337d-135">The format enables native content as a first class scenario.</span></span> <span data-ttu-id="5337d-136">Bu, yönetilen derlemelerin, hedef platforma dayalı yönetilen derlemelerin yanında ikili uygulamaları sevk etmek için donanım uygulamalarına yakın bağlı olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="5337d-136">This means that managed assemblies depend on close to hardware implementations to ship binary implementations alongside the managed assemblies based on the target platform.</span></span> <span data-ttu-id="5337d-137">Örneğin System.IO.Compression paketi bu teknolojiyi kullanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="5337d-137">For example System.IO.Compression package is utilizing this technology.</span></span> [https://www.nuget.org/packages/System.IO.Compression](https://www.nuget.org/packages/System.IO.Compression)

<span data-ttu-id="5337d-138">Özetle, yukarıdaki işlevsellik kesinlikle gerekli değilse, burada açıklanan biçim yalnızca NuGet 3.x+ tarafından desteklendirildiği için mevcut paket biçimine uymanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="5337d-138">In summary if the functionality above is not absolutely necessary, we recommend sticking with the existing package format, as the format described here is supported only by NuGet 3.x+.</span></span>

<span data-ttu-id="5337d-139">Şimleme yoluyla hem de `packages.config` `project.json` senaryolar için çalışacak paketler oluşturmak mümkün olabilir, ancak yukarıda belirtilen amortismana uygun özellikler olmadan paketleri geleneksel şekilde yapılandırmak genellikle daha kolaydır.</span><span class="sxs-lookup"><span data-stu-id="5337d-139">It would be possible to build packages to work for both `packages.config` and `project.json` scenarios through shimming, however it's often simpler to just structure the packages the traditional way, without the deprecated features mentioned above.</span></span>

## <a name="3x-package-format"></a><span data-ttu-id="5337d-140">3.x paket formatı</span><span class="sxs-lookup"><span data-stu-id="5337d-140">3.x package format</span></span>

<span data-ttu-id="5337d-141">3.x paket biçimi NuGet 2.x ötesinde birkaç ek özellik sağlar:</span><span class="sxs-lookup"><span data-stu-id="5337d-141">The 3.x package format allows for several additional features beyond NuGet 2.x:</span></span>

1. <span data-ttu-id="5337d-142">Derleme için kullanılan bir başvuru derlemesi ve farklı platformlarda/cihazlarda çalışma zamanı için kullanılan bir dizi uygulama derlemesi tanımlama.</span><span class="sxs-lookup"><span data-stu-id="5337d-142">Defining a reference assembly used for compilation and a set of implementation assemblies used for runtime on different platforms/devices.</span></span> <span data-ttu-id="5337d-143">Bu da tüketicileriçin ortak bir yüzey alanı sağlarken platforma özgü API'lerden yararlanmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="5337d-143">Which allows you to take advantage of platform specific APIs while providing a common surface area for your consumers.</span></span> <span data-ttu-id="5337d-144">Özellikle bu, ara taşınabilir kitaplıkların yazılmasını kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="5337d-144">Specifically this makes writing intermediate portable libraries easier.</span></span>

1. <span data-ttu-id="5337d-145">Paketlerin işletim sistemleri veya CPU mimarisi gibi platformlarda dönmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="5337d-145">Allows packages to pivot on platforms e.g. operating systems or CPU architecture.</span></span>

1. <span data-ttu-id="5337d-146">Platforma özgü uygulamaların eş ekibe ayrılmasına olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="5337d-146">Allows for separation of platform specific implementations to companion packages.</span></span>

1. <span data-ttu-id="5337d-147">Birinci sınıf vatandaş olarak yerel bağımlılıkları destekleyin.</span><span class="sxs-lookup"><span data-stu-id="5337d-147">Support Native dependencies as a first class citizen.</span></span>
