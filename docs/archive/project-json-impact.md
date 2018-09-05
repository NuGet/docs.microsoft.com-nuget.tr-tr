---
title: NuGet paket yazarlarının Project.JSON etkisi
description: Nasıl NuGet 3.x etkiler project.json uygulama paketini yazar, desteklenmeyen özellikler, içerik ve paket biçimi gibi ayrıntılar.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 8c85c1a89469c491c6be1f81961197450744349c
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545579"
---
# <a name="impact-of-projectjson-when-creating-packages"></a><span data-ttu-id="f6945-103">Paket oluştururken project.json etkisi</span><span class="sxs-lookup"><span data-stu-id="f6945-103">Impact of project.json when creating packages</span></span>

> [!Important]
> <span data-ttu-id="f6945-104">Bu içerik kullanım dışı bırakılmıştır.</span><span class="sxs-lookup"><span data-stu-id="f6945-104">This content is deprecated.</span></span> <span data-ttu-id="f6945-105">Projeleri ya da kullanması gereken `packages.config` veya PackageReference biçimleri.</span><span class="sxs-lookup"><span data-stu-id="f6945-105">Projects should use either the `packages.config` or PackageReference formats.</span></span>

<span data-ttu-id="f6945-106">`project.json` Nuget'te 3 + kullanılan sistem aşağıdaki bölümlerde açıklandığı gibi çeşitli şekillerde paket yazarlarının etkiler.</span><span class="sxs-lookup"><span data-stu-id="f6945-106">The `project.json` system used in NuGet 3+ affects package authors in several ways as described in the following sections.</span></span>

## <a name="changes-affecting-existing-packages-usage"></a><span data-ttu-id="f6945-107">Var olan paketler kullanım etkileyen değişiklikler</span><span class="sxs-lookup"><span data-stu-id="f6945-107">Changes affecting existing packages usage</span></span>

<span data-ttu-id="f6945-108">Geleneksel NuGet paketlerini geçişli dünya taşınmaz özellikleriyle destekler.</span><span class="sxs-lookup"><span data-stu-id="f6945-108">Traditional NuGet packages support a set of features that are not carried over to the transitive world.</span></span>

### <a name="install-and-uninstall-scripts-are-ignored"></a><span data-ttu-id="f6945-109">Yükleme ve kaldırma betiklerini yoksayıldı</span><span class="sxs-lookup"><span data-stu-id="f6945-109">Install and uninstall scripts are ignored</span></span>

<span data-ttu-id="f6945-110">Açıklanan geçişli geri yükleme modeli [bağımlılık çözümlemesi](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference), "paket yükleme saati" kavramını sahip değil.</span><span class="sxs-lookup"><span data-stu-id="f6945-110">The transitive restore model, described in [Dependency resolution](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference), does not have a concept of "package install time".</span></span> <span data-ttu-id="f6945-111">Mevcut değil ya da mevcut bir pakettir, ancak bir paket yüklendikten sonra gerçekleşen tutarlı işlem yok.</span><span class="sxs-lookup"><span data-stu-id="f6945-111">A package is either present or not present, but there is no consistent process that occurs when a package is installed.</span></span>

<span data-ttu-id="f6945-112">Ayrıca, komut dosyaları yalnızca Visual Studio ile desteklenen yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f6945-112">Also, install scripts were supported only in Visual Studio.</span></span> <span data-ttu-id="f6945-113">Diğer Ide'leri API gibi komut dosyalarını destekleyen denemek için Visual Studio genişletilebilirlik gerekiyordu ve ortak düzenleyiciler ve komut satırı araçları desteği yoktu.</span><span class="sxs-lookup"><span data-stu-id="f6945-113">Other IDEs had to mock the Visual Studio extensibility API to attempt to support such scripts, and no support was available in common editors and command-line tools.</span></span>

### <a name="content-transforms-are-not-supported"></a><span data-ttu-id="f6945-114">İçerik dönüştürmeleri desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="f6945-114">Content transforms are not supported</span></span>

<span data-ttu-id="f6945-115">Benzer betikleri yüklemek için paketi üzerinde çalıştırılan dönüşümler yükleyin ve genellikle etkili değildir.</span><span class="sxs-lookup"><span data-stu-id="f6945-115">Similar to install scripts, transforms run on package install and are typically not idempotent.</span></span> <span data-ttu-id="f6945-116">Artık hiçbir yükleme zamanı olduğundan, XDT dönüştürün ve benzer özellikleri desteklenmez ve bu tür bir paket geçişli bir senaryoda kullanılıyorsa, göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="f6945-116">Since there is no install time anymore, XDT Transform and similar features are not supported, and are ignored if such a package is used in a transitive scenario.</span></span>

### <a name="content"></a><span data-ttu-id="f6945-117">İçerik</span><span class="sxs-lookup"><span data-stu-id="f6945-117">Content</span></span>

<span data-ttu-id="f6945-118">Kaynak kodu gibi içerik dosyaları ve yapılandırma dosyaları geleneksel NuGet paketlerini yayımlayan.</span><span class="sxs-lookup"><span data-stu-id="f6945-118">Traditional NuGet packages are shipping content files such as source code and configuration files.</span></span> <span data-ttu-id="f6945-119">Var. tipik olarak iki senaryolarda kullanılır:</span><span class="sxs-lookup"><span data-stu-id="f6945-119">There are used typically in two scenarios:</span></span>

1. <span data-ttu-id="f6945-120">Kullanıcı daha sonraki bir zamanda düzenleyebilmeniz ilk dosyalar projeye bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="f6945-120">Initial files dropped into the project so the user can edit them at a later time.</span></span> <span data-ttu-id="f6945-121">Varsayılan yapılandırma dosyalarını ortak örnektir.</span><span class="sxs-lookup"><span data-stu-id="f6945-121">The common example is default configuration files.</span></span>

1. <span data-ttu-id="f6945-122">İçerik dosyalarının projede yüklü derlemelere arkadaşlarımız olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f6945-122">Content files used as companions to the assemblies installed in the project.</span></span> <span data-ttu-id="f6945-123">Örnek, bir derleme tarafından kullanılan bir logo resmi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="f6945-123">The example here would be a logo image used by an assembly.</span></span>

<span data-ttu-id="f6945-124">İçerik betikleri ve dönüştürmeler için benzer nedeniyle şu anda devre dışıdır, ancak içerik desteğini tasarlama aşamasında olan desteği.</span><span class="sxs-lookup"><span data-stu-id="f6945-124">Support for content is currently disabled for similar reasons for scripts and transforms, but we are in the process of designing support for content.</span></span>

<span data-ttu-id="f6945-125">İçerik dosyaları yine de paketleri aktarılabilen ve şu anda göz ardı edilir, ancak son kullanıcı yine de bunları doğru nokta kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f6945-125">Content files can still be carried inside the packages, and are ignored currently, however the end user can still copy them into the right spot.</span></span>

<span data-ttu-id="f6945-126">İçerik dosyalarını geri getirmek için teklifleri birine bakın ve ilerleme durumunu, burada izleyin: [ https://github.com/NuGet/Home/issues/627 ](https://github.com/NuGet/Home/issues/627).</span><span class="sxs-lookup"><span data-stu-id="f6945-126">You can see one of the proposals for bringing back content files, and follow its progress, here: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627).</span></span>

## <a name="impact-for-package-authors"></a><span data-ttu-id="f6945-127">Paket yazarlarının için etkisi</span><span class="sxs-lookup"><span data-stu-id="f6945-127">Impact for package authors</span></span>

<span data-ttu-id="f6945-128">Yukarıdaki özellikleri kullanarak paketleri farklı mekanizmasının kullanılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f6945-128">Packages using the above features would have to use a different mechanism.</span></span> <span data-ttu-id="f6945-129">Bunun en yaygın olarak yararlı mekanizması, MSBuild hedefleri/tam olarak desteklenen için devam eden özellikler olacaktır.</span><span class="sxs-lookup"><span data-stu-id="f6945-129">The most commonly useful mechanism for this would be the MSBuild targets/props that continues to get fully supported.</span></span> <span data-ttu-id="f6945-130">Derleme sistemi paketi diğer kuralları yerden devam edebiliyorduk seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f6945-130">The build system can choose to pick up other conventions in the package.</span></span> <span data-ttu-id="f6945-131">MSBuild hedefleri Roslyn Çözümleyicileri yanı sıra nasıl desteklenen budur.</span><span class="sxs-lookup"><span data-stu-id="f6945-131">This is how MSBuild targets are supported as well as Roslyn analyzers.</span></span> <span data-ttu-id="f6945-132">Hedefleri ve çözümleyiciler için destekleyen paketleri oluşturmak mümkündür `packages.config` ve `project.json` senaryoları.</span><span class="sxs-lookup"><span data-stu-id="f6945-132">It is possible to build packages that supports targets and analyzers for `packages.config` and `project.json` scenarios.</span></span>

<span data-ttu-id="f6945-133">Başlangıç genellikle kolaylaştırmak için proje değiştirmeyi deneyen paketleri senaryoları çok sınırlı kümesi içinde çalışır ve paketin nasıl kullanılacağı hakkında bir Benioku ya da yönergeler yerine sağlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="f6945-133">Packages that attempt to modify the project to ease startup typically work in a very limited set of scenarios, and should instead provide a readme, or guidance on how to use the package.</span></span>

<span data-ttu-id="f6945-134">Birçok var olan paketi aşağıda açıklanan paket biçimi kullanmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="f6945-134">Most existing packages should not need to use the package format described below.</span></span>

<span data-ttu-id="f6945-135">Biçim, birinci sınıf bir senaryo yerel içerik sağlar.</span><span class="sxs-lookup"><span data-stu-id="f6945-135">The format enables native content as a first class scenario.</span></span> <span data-ttu-id="f6945-136">Bu, yönetilen bütünleştirilmiş kodların donanım uygulamaları, hedef platforma göre Yönetilen derlemeler yanı sıra ikili uygulamaları dağıtmayı yakın bağımlı olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="f6945-136">This means that managed assemblies depend on close to hardware implementations to ship binary implementations alongside the managed assemblies based on the target platform.</span></span> <span data-ttu-id="f6945-137">Örneğin System.IO.Compression paketi bu teknoloji kullanılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f6945-137">For example System.IO.Compression package is utilizing this technology.</span></span> [https://www.nuget.org/packages/System.IO.Compression](https://www.nuget.org/packages/System.IO.Compression)

<span data-ttu-id="f6945-138">Yukarıdaki işlevselliğini kesinlikle gerekli değilse, burada açıklanan biçimde yalnızca NuGet 3.x+ tarafından desteklenmediğinden özetinde kalmanız mevcut paket biçimi öneririz.</span><span class="sxs-lookup"><span data-stu-id="f6945-138">In summary if the functionality above is not absolutely necessary, we recommend sticking with the existing package format, as the format described here is supported only by NuGet 3.x+.</span></span>

<span data-ttu-id="f6945-139">Hem çalışma için paketler oluşturmak mümkün `packages.config` ve `project.json` senaryolar aracılığıyla için dolgu oluşturuluyor, ancak bu genellikle yalnızca yukarıdaki kullanım dışı bırakılan özellikler olmadan geleneksel paketleri yapı daha kolaydır.</span><span class="sxs-lookup"><span data-stu-id="f6945-139">It would be possible to build packages to work for both `packages.config` and `project.json` scenarios through shimming, however it's often simpler to just structure the packages the traditional way, without the deprecated features mentioned above.</span></span>

## <a name="3x-package-format"></a><span data-ttu-id="f6945-140">3.x paket biçimi</span><span class="sxs-lookup"><span data-stu-id="f6945-140">3.x package format</span></span>

<span data-ttu-id="f6945-141">Birkaç ek özelliklerin ötesinde NuGet 3.x paket biçimi sağlar 2.x:</span><span class="sxs-lookup"><span data-stu-id="f6945-141">The 3.x package format allows for several additional features beyond NuGet 2.x:</span></span>

1. <span data-ttu-id="f6945-142">Derleme ve farklı platformları/cihaz üzerinde çalışma zamanı için kullanılan bir uygulama derleme kümesi için kullanılan bir başvuru bütünleştirilmiş kodu tanımlama.</span><span class="sxs-lookup"><span data-stu-id="f6945-142">Defining a reference assembly used for compilation and a set of implementation assemblies used for runtime on different platforms/devices.</span></span> <span data-ttu-id="f6945-143">Belirli platformunun avantajlarından yararlanmanıza olanak tanıyan tüketicileriniz için ortak bir yüzey alanı sağlarken API'leri.</span><span class="sxs-lookup"><span data-stu-id="f6945-143">Which allows you to take advantage of platform specific APIs while providing a common surface area for your consumers.</span></span> <span data-ttu-id="f6945-144">Özellikle bu şekilde, daha kolay Ara taşınabilir kitaplıklar yazmayı kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="f6945-144">Specifically this makes writing intermediate portable libraries easier.</span></span>

1. <span data-ttu-id="f6945-145">İşletim sistemleri veya CPU mimarisi platformlarda örn Özet paketleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="f6945-145">Allows packages to pivot on platforms e.g. operating systems or CPU architecture.</span></span>

1. <span data-ttu-id="f6945-146">Belirli platform uygulamalarını Yardımcısı paketlerine ayrımı sağlar.</span><span class="sxs-lookup"><span data-stu-id="f6945-146">Allows for separation of platform specific implementations to companion packages.</span></span>

1. <span data-ttu-id="f6945-147">Yerel bağımlılıkları öncelikli bir yere destekler.</span><span class="sxs-lookup"><span data-stu-id="f6945-147">Support Native dependencies as a first class citizen.</span></span>
