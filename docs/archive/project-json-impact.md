---
title: NuGet paketi yazarları Project.JSON etkisini | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Nasıl NuGet 3.x etkiler project.json uygulama paketini desteklenmeyen özellikler, içerik ve paket biçimi gibi yazarlar ayrıntılar.
keywords: NuGet ve project.json, project.json etkisi yazma konuları, project.json özellik paketi
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 6e8af98504a2866106e84943989aeb91f2e9c1fb
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="impact-of-projectjson-when-creating-packages"></a><span data-ttu-id="54397-104">Paket oluştururken project.json etkisi</span><span class="sxs-lookup"><span data-stu-id="54397-104">Impact of project.json when creating packages</span></span>

> [!Important]
> <span data-ttu-id="54397-105">Bu içerik kullanım dışı bırakılmıştır.</span><span class="sxs-lookup"><span data-stu-id="54397-105">This content is deprecated.</span></span> <span data-ttu-id="54397-106">Projeleri ya da kullanması gereken `packages.config` veya PackageReference biçimleri.</span><span class="sxs-lookup"><span data-stu-id="54397-106">Projects should use either the `packages.config` or PackageReference formats.</span></span>

<span data-ttu-id="54397-107">`project.json` NuGet içinde 3 + kullanılan sistem aşağıdaki bölümlerde açıklandığı gibi çeşitli şekillerde paketi yazarları etkiler.</span><span class="sxs-lookup"><span data-stu-id="54397-107">The `project.json` system used in NuGet 3+ affects package authors in several ways as described in the following sections.</span></span>

## <a name="changes-affecting-existing-packages-usage"></a><span data-ttu-id="54397-108">Var olan paketler kullanım etkileyen değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="54397-108">Changes affecting existing packages usage</span></span>

<span data-ttu-id="54397-109">Geleneksel NuGet paketlerini geçişli dünyasına taşınır olmayan özellikler kümesini destekler.</span><span class="sxs-lookup"><span data-stu-id="54397-109">Traditional NuGet packages support a set of features that are not carried over to the transitive world.</span></span>

### <a name="install-and-uninstall-scripts-are-ignored"></a><span data-ttu-id="54397-110">Yükleme ve kaldırma betikleri yok sayılır</span><span class="sxs-lookup"><span data-stu-id="54397-110">Install and uninstall scripts are ignored</span></span>

<span data-ttu-id="54397-111">Açıklanan geçişli geri yükleme modeli [bağımlılık çözümlemesi](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference), "paketini yükle zaman" kavramını yok.</span><span class="sxs-lookup"><span data-stu-id="54397-111">The transitive restore model, described in [Dependency resolution](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference), does not have a concept of "package install time".</span></span> <span data-ttu-id="54397-112">Bir pakettir mevcut ya da mevcut değil, ancak bir paket yüklendiğinde oluşan tutarlı hiçbir işlem yok.</span><span class="sxs-lookup"><span data-stu-id="54397-112">A package is either present or not present, but there is no consistent process that occurs when a package is installed.</span></span>

<span data-ttu-id="54397-113">Ayrıca, komut dosyaları yalnızca Visual Studio'da desteklenen yükleyin.</span><span class="sxs-lookup"><span data-stu-id="54397-113">Also, install scripts were supported only in Visual Studio.</span></span> <span data-ttu-id="54397-114">Diğer IDE Visual Studio genişletilebilirlik gibi komut dosyalarını destekleyen girişimi için API gerekiyordu ve Destek yok ortak düzenleyicileri ve komut satırı araçları kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="54397-114">Other IDEs had to mock the Visual Studio extensibility API to attempt to support such scripts, and no support was available in common editors and command-line tools.</span></span>

### <a name="content-transforms-are-not-supported"></a><span data-ttu-id="54397-115">İçerik dönüştürmeleri desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="54397-115">Content transforms are not supported</span></span>

<span data-ttu-id="54397-116">Benzer komut dosyaları yüklemek için paketi çalıştırmak dönüşümler yükleyin ve genellikle ıdempotent değildir.</span><span class="sxs-lookup"><span data-stu-id="54397-116">Similar to install scripts, transforms run on package install and are typically not idempotent.</span></span> <span data-ttu-id="54397-117">Artık hiçbir yükleme saatini olduğundan XDT dönüştürme ve benzer özellikleri desteklenmez ve böyle bir paket geçişli bir senaryoda kullanılırsa, göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="54397-117">Since there is no install time anymore, XDT Transform and similar features are not supported, and are ignored if such a package is used in a transitive scenario.</span></span>

### <a name="content"></a><span data-ttu-id="54397-118">İçerik</span><span class="sxs-lookup"><span data-stu-id="54397-118">Content</span></span>

<span data-ttu-id="54397-119">Geleneksel NuGet paketlerini kaynak kodu gibi içerik dosyalarını ve yapılandırma dosyalarını yayımlayan.</span><span class="sxs-lookup"><span data-stu-id="54397-119">Traditional NuGet packages are shipping content files such as source code and configuration files.</span></span> <span data-ttu-id="54397-120">Var. genellikle iki senaryolarda kullanılır:</span><span class="sxs-lookup"><span data-stu-id="54397-120">There are used typically in two scenarios:</span></span>

1. <span data-ttu-id="54397-121">Kullanıcı daha sonra düzenleyebilmeniz başlangıç dosyalarını projeye bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="54397-121">Initial files dropped into the project so the user can edit them at a later time.</span></span> <span data-ttu-id="54397-122">Varsayılan yapılandırma dosyalarını ortak örnektir.</span><span class="sxs-lookup"><span data-stu-id="54397-122">The common example is default configuration files.</span></span>

1. <span data-ttu-id="54397-123">Projede yüklü derlemelerine arkadaşlarımız olarak kullanılan içerik dosyaları.</span><span class="sxs-lookup"><span data-stu-id="54397-123">Content files used as companions to the assemblies installed in the project.</span></span> <span data-ttu-id="54397-124">Örnek bir derlemesi tarafından kullanılan bir logo görüntüsü olacaktır.</span><span class="sxs-lookup"><span data-stu-id="54397-124">The example here would be a logo image used by an assembly.</span></span>

<span data-ttu-id="54397-125">Komut dosyaları ve dönüşümler benzer nedenlerle içerik şu anda devre dışıdır, ancak içerik desteğini tasarlama sürecinde olan desteği.</span><span class="sxs-lookup"><span data-stu-id="54397-125">Support for content is currently disabled for similar reasons for scripts and transforms, but we are in the process of designing support for content.</span></span>

<span data-ttu-id="54397-126">İçerik dosyaları hala paketleri aktarılabilen ve şu anda göz ardı edilir, ancak son kullanıcı hala bunları sağ nokta kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="54397-126">Content files can still be carried inside the packages, and are ignored currently, however the end user can still copy them into the right spot.</span></span>

<span data-ttu-id="54397-127">İçerik dosyalarını geri getiren teklifleri birine bakın ve ilerleme durumunu, burada izleyin: [ https://github.com/NuGet/Home/issues/627 ](https://github.com/NuGet/Home/issues/627).</span><span class="sxs-lookup"><span data-stu-id="54397-127">You can see one of the proposals for bringing back content files, and follow its progress, here: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627).</span></span>

## <a name="impact-for-package-authors"></a><span data-ttu-id="54397-128">Paketi yazarları için etkisi</span><span class="sxs-lookup"><span data-stu-id="54397-128">Impact for package authors</span></span>

<span data-ttu-id="54397-129">Yukarıdaki özellikleri kullanarak paketleri farklı mekanizmasını kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="54397-129">Packages using the above features would have to use a different mechanism.</span></span> <span data-ttu-id="54397-130">Bunun en yaygın olarak yararlı mekanizması MSBuild hedefleri/tam olarak desteklenen için devam eden özellik olacaktır.</span><span class="sxs-lookup"><span data-stu-id="54397-130">The most commonly useful mechanism for this would be the MSBuild targets/props that continues to get fully supported.</span></span> <span data-ttu-id="54397-131">Derleme sistemi diğer kuralları paketindeki alması seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="54397-131">The build system can choose to pick up other conventions in the package.</span></span> <span data-ttu-id="54397-132">MSBuild hedefleri Roslyn çözümleyiciler yanı sıra nasıl desteklendiğini budur.</span><span class="sxs-lookup"><span data-stu-id="54397-132">This is how MSBuild targets are supported as well as Roslyn analyzers.</span></span> <span data-ttu-id="54397-133">Hedefleri ve çözümleyiciler için destekleyen paketleri oluşturmak mümkün müdür `packages.config` ve `project.json` senaryoları.</span><span class="sxs-lookup"><span data-stu-id="54397-133">It is possible to build packages that supports targets and analyzers for `packages.config` and `project.json` scenarios.</span></span>

<span data-ttu-id="54397-134">Başlangıç genellikle kolaylaştırmak için proje değiştirme girişimi paketleri çok sınırlı sayıda senaryoları iş ve bunun yerine bir benioku veya kılavuz paketin nasıl kullanılacağı hakkında sağlaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="54397-134">Packages that attempt to modify the project to ease startup typically work in a very limited set of scenarios, and should instead provide a readme, or guidance on how to use the package.</span></span>

<span data-ttu-id="54397-135">Çoğu mevcut paketleri aşağıda açıklanan paket biçimi kullanmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="54397-135">Most existing packages should not need to use the package format described below.</span></span>

<span data-ttu-id="54397-136">Yerel içerik biçimi birinci sınıf bir senaryo sağlar.</span><span class="sxs-lookup"><span data-stu-id="54397-136">The format enables native content as a first class scenario.</span></span> <span data-ttu-id="54397-137">Bu yönetilen derlemeler hedef platformu temel alarak Yönetilen derlemeler yanında ikili uygulamaları dağıtmayı donanım uygulamaları yakın bağlı olduğunu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="54397-137">This means that managed assemblies depend on close to hardware implementations to ship binary implementations alongside the managed assemblies based on the target platform.</span></span> <span data-ttu-id="54397-138">Örneğin System.IO.Compression paket bu teknoloji kullanılarak.</span><span class="sxs-lookup"><span data-stu-id="54397-138">For example System.IO.Compression package is utilizing this technology.</span></span> [https://www.nuget.org/packages/System.IO.Compression](https://www.nuget.org/packages/System.IO.Compression)

<span data-ttu-id="54397-139">Yukarıdaki işlevselliği kesinlikle gerekli değilse, burada açıklanan biçimde yalnızca NuGet 3.x+ tarafından desteklenen olarak Özet olarak var olan paketi biçimiyle kalmanız öneririz.</span><span class="sxs-lookup"><span data-stu-id="54397-139">In summary if the functionality above is not absolutely necessary, we recommend sticking with the existing package format, as the format described here is supported only by NuGet 3.x+.</span></span>

<span data-ttu-id="54397-140">Her ikisi için çalışmaya paketleri oluşturmak mümkün `packages.config` ve `project.json` shimming, ancak genellikle yalnızca yukarıda belirtilen kullanım dışı özellikler olmadan geleneksel şekilde paketleri yapısı daha basit olduğu aracılığıyla senaryoları.</span><span class="sxs-lookup"><span data-stu-id="54397-140">It would be possible to build packages to work for both `packages.config` and `project.json` scenarios through shimming, however it's often simpler to just structure the packages the traditional way, without the deprecated features mentioned above.</span></span>

## <a name="3x-package-format"></a><span data-ttu-id="54397-141">3.x paket biçimi</span><span class="sxs-lookup"><span data-stu-id="54397-141">3.x package format</span></span>

<span data-ttu-id="54397-142">3.x paket biçimi NuGet ötesinde çeşitli ek özellikler sağlar 2.x:</span><span class="sxs-lookup"><span data-stu-id="54397-142">The 3.x package format allows for several additional features beyond NuGet 2.x:</span></span>

1. <span data-ttu-id="54397-143">Derleme ve bir dizi farklı platformlar/cihaz üzerinde çalışma zamanı için kullanılan uygulama derlemeler için kullanılan bir referans derlemesini tanımlama.</span><span class="sxs-lookup"><span data-stu-id="54397-143">Defining a reference assembly used for compilation and a set of implementation assemblies used for runtime on different platforms/devices.</span></span> <span data-ttu-id="54397-144">Platform özel yararlanmak verir tüketicileriniz için ortak bir yüzey alanını sağlarken API'leri.</span><span class="sxs-lookup"><span data-stu-id="54397-144">Which allows you to take advantage of platform specific APIs while providing a common surface area for your consumers.</span></span> <span data-ttu-id="54397-145">Özellikle bu şekilde, daha kolay Ara taşınabilir kitaplıklara yazmayı kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="54397-145">Specifically this makes writing intermediate portable libraries easier.</span></span>

1. <span data-ttu-id="54397-146">İşletim sistemleri veya CPU mimarisi platformlarda Örneğin Özet paketleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="54397-146">Allows packages to pivot on platforms e.g. operating systems or CPU architecture.</span></span>

1. <span data-ttu-id="54397-147">Platform belirli uygulamaları Yardımcısı paketlere ayrımı sağlar.</span><span class="sxs-lookup"><span data-stu-id="54397-147">Allows for separation of platform specific implementations to companion packages.</span></span>

1. <span data-ttu-id="54397-148">Yerel bağımlılıkları birinci sınıf vatandaşı destekler.</span><span class="sxs-lookup"><span data-stu-id="54397-148">Support Native dependencies as a first class citizen.</span></span>
