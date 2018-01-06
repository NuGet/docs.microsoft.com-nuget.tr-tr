---
title: "NuGet paketi yazarları Project.JSON etkisini | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 983485df-9375-4827-b58b-70065320ee37
description: "Nasıl NuGet 3.x etkiler project.json uygulama paketini desteklenmeyen özellikler, içerik ve paket biçimi gibi yazarlar ayrıntılar."
keywords: "NuGet ve project.json, project.json etkisi yazma konuları, project.json özellik paketi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 69a6bbbe1c96b06dbba7ac787b836b8b62c438ec
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/05/2018
---
# <a name="impact-of-projectjson-when-creating-packages"></a><span data-ttu-id="74418-104">Paket oluştururken project.json etkisi</span><span class="sxs-lookup"><span data-stu-id="74418-104">Impact of project.json when creating packages</span></span>

<span data-ttu-id="74418-105">`project.json` NuGet içinde 3 + kullanılan sistem aşağıdaki bölümlerde açıklandığı gibi çeşitli şekillerde paketi yazarları etkiler.</span><span class="sxs-lookup"><span data-stu-id="74418-105">The `project.json` system used in NuGet 3+ affects package authors in several ways as described in the following sections.</span></span>

## <a name="changes-affecting-existing-packages-usage"></a><span data-ttu-id="74418-106">Var olan paketler kullanım etkileyen değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="74418-106">Changes affecting existing packages usage</span></span>

<span data-ttu-id="74418-107">Geleneksel NuGet paketlerini geçişli dünyasına taşınır olmayan özellikler kümesini destekler.</span><span class="sxs-lookup"><span data-stu-id="74418-107">Traditional NuGet packages support a set of features that are not carried over to the transitive world.</span></span>

### <a name="install-and-uninstall-scripts-are-ignored"></a><span data-ttu-id="74418-108">Yükleme ve kaldırma betikleri yok sayılır</span><span class="sxs-lookup"><span data-stu-id="74418-108">Install and uninstall scripts are ignored</span></span>

<span data-ttu-id="74418-109">Açıklanan geçişli geri yükleme modeli [bağımlılık çözümlemesi](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference-and-projectjson), "paketini yükle zaman" kavramını yok.</span><span class="sxs-lookup"><span data-stu-id="74418-109">The transitive restore model, described in [Dependency resolution](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference-and-projectjson), does not have a concept of "package install time".</span></span> <span data-ttu-id="74418-110">Bir pakettir mevcut ya da mevcut değil, ancak bir paket yüklendiğinde oluşan tutarlı hiçbir işlem yok.</span><span class="sxs-lookup"><span data-stu-id="74418-110">A package is either present or not present, but there is no consistent process that occurs when a package is installed.</span></span>

<span data-ttu-id="74418-111">Ayrıca, komut dosyaları yalnızca Visual Studio'da desteklenen yükleyin.</span><span class="sxs-lookup"><span data-stu-id="74418-111">Also, install scripts were supported only in Visual Studio.</span></span> <span data-ttu-id="74418-112">Diğer IDE Visual Studio genişletilebilirlik gibi komut dosyalarını destekleyen girişimi için API gerekiyordu ve Destek yok ortak düzenleyicileri ve komut satırı araçları kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="74418-112">Other IDEs had to mock the Visual Studio extensibility API to attempt to support such scripts, and no support was available in common editors and command-line tools.</span></span>

### <a name="content-transforms-are-not-supported"></a><span data-ttu-id="74418-113">İçerik dönüştürmeleri desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="74418-113">Content transforms are not supported.</span></span>

<span data-ttu-id="74418-114">Benzer komut dosyaları yüklemek için paketi çalıştırmak dönüşümler yükleyin ve genellikle ıdempotent değildir.</span><span class="sxs-lookup"><span data-stu-id="74418-114">Similar to install scripts, transforms run on package install and are typically not idempotent.</span></span> <span data-ttu-id="74418-115">Artık hiçbir yükleme saatini olduğundan XDT dönüştürme ve benzer özellikleri desteklenmez ve böyle bir paket geçişli bir senaryoda kullanılırsa, göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="74418-115">Since there is no install time anymore, XDT Transform and similar features are not supported, and are ignored if such a package is used in a transitive scenario.</span></span>


### <a name="content"></a><span data-ttu-id="74418-116">İçerik</span><span class="sxs-lookup"><span data-stu-id="74418-116">Content</span></span>

<span data-ttu-id="74418-117">Geleneksel NuGet paketlerini kaynak kodu gibi içerik dosyalarını ve yapılandırma dosyalarını yayımlayan.</span><span class="sxs-lookup"><span data-stu-id="74418-117">Traditional NuGet packages are shipping content files such as source code and configuration files.</span></span> <span data-ttu-id="74418-118">Var. genellikle iki senaryolarda kullanılır:</span><span class="sxs-lookup"><span data-stu-id="74418-118">There are used typically in two scenarios:</span></span>

1. <span data-ttu-id="74418-119">Kullanıcı daha sonra düzenleyebilmeniz başlangıç dosyalarını projeye bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="74418-119">Initial files dropped into the project so the user can edit them at a later time.</span></span> <span data-ttu-id="74418-120">Varsayılan yapılandırma dosyalarını ortak örnektir.</span><span class="sxs-lookup"><span data-stu-id="74418-120">The common example is default configuration files.</span></span>

2. <span data-ttu-id="74418-121">Projede yüklü derlemelerine arkadaşlarımız olarak kullanılan içerik dosyaları.</span><span class="sxs-lookup"><span data-stu-id="74418-121">Content files used as companions to the assemblies installed in the project.</span></span> <span data-ttu-id="74418-122">Örnek bir derlemesi tarafından kullanılan bir logo görüntüsü olacaktır.</span><span class="sxs-lookup"><span data-stu-id="74418-122">The example here would be a logo image used by an assembly.</span></span>

<span data-ttu-id="74418-123">Komut dosyaları ve dönüşümler benzer nedenlerle içerik şu anda devre dışıdır, ancak içerik desteğini tasarlama sürecinde olan desteği.</span><span class="sxs-lookup"><span data-stu-id="74418-123">Support for content is currently disabled for similar reasons for scripts and transforms, but we are in the process of designing support for content.</span></span>

<span data-ttu-id="74418-124">İçerik dosyaları hala paketleri aktarılabilen ve şu anda göz ardı edilir, ancak son kullanıcı hala bunları sağ nokta kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="74418-124">Content files can still be carried inside the packages, and are ignored currently, however the end user can still copy them into the right spot.</span></span>

<span data-ttu-id="74418-125">İçerik dosyalarını geri getiren teklifleri birine bakın ve ilerleme durumunu, burada izleyin: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627).</span><span class="sxs-lookup"><span data-stu-id="74418-125">You can see one of the proposals for bringing back content files, and follow its progress, here: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627).</span></span>

## <a name="impact-for-package-authors"></a><span data-ttu-id="74418-126">Paketi yazarları için etkisi</span><span class="sxs-lookup"><span data-stu-id="74418-126">Impact for package authors</span></span>

<span data-ttu-id="74418-127">Yukarıdaki özellikleri kullanarak paketleri farklı mekanizmasını kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="74418-127">Packages using the above features would have to use a different mechanism.</span></span> <span data-ttu-id="74418-128">Bunun en yaygın olarak yararlı mekanizması MSBuild hedefleri/tam olarak desteklenen için devam eden özellik olacaktır.</span><span class="sxs-lookup"><span data-stu-id="74418-128">The most commonly useful mechanism for this would be the MSBuild targets/props that continues to get fully supported.</span></span> <span data-ttu-id="74418-129">Derleme sistemi diğer kuralları paketindeki alması seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="74418-129">The build system can choose to pick up other conventions in the package.</span></span> <span data-ttu-id="74418-130">MSBuild hedefleri Roslyn çözümleyiciler yanı sıra nasıl desteklendiğini budur.</span><span class="sxs-lookup"><span data-stu-id="74418-130">This is how MSBuild targets are supported as well as Roslyn analyzers.</span></span> <span data-ttu-id="74418-131">Hedefleri ve çözümleyiciler için destekleyen paketleri oluşturmak mümkün müdür `packages.config` ve `project.json` senaryoları.</span><span class="sxs-lookup"><span data-stu-id="74418-131">It is possible to build packages that supports targets and analyzers for `packages.config` and `project.json` scenarios.</span></span>

<span data-ttu-id="74418-132">Başlangıç genellikle kolaylaştırmak için proje değiştirme girişimi paketleri çok sınırlı sayıda senaryoları iş ve bunun yerine bir benioku veya kılavuz paketin nasıl kullanılacağı hakkında sağlaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="74418-132">Packages that attempt to modify the project to ease startup typically work in a very limited set of scenarios, and should instead provide a readme, or guidance on how to use the package.</span></span>

<span data-ttu-id="74418-133">Çoğu mevcut paketleri aşağıda açıklanan paket biçimi kullanmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="74418-133">Most existing packages should not need to use the package format described below.</span></span>

<span data-ttu-id="74418-134">Yerel içerik biçimi birinci sınıf bir senaryo sağlar.</span><span class="sxs-lookup"><span data-stu-id="74418-134">The format enables native content as a first class scenario.</span></span> <span data-ttu-id="74418-135">Hedef platformu temel alarak Yönetilen derlemeler yanında ikili uygulamaları dağıtmayı bağlı olarak donanım uygulamaları yakın derlemeleri yönetilen anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="74418-135">This means that managed assemblies depending on close to hardware implementations to ship binary implementations alongside the managed assemblies based on the target platform.</span></span> <span data-ttu-id="74418-136">Örneğin System.IO.Compression paket bu teknoloji kullanılarak.</span><span class="sxs-lookup"><span data-stu-id="74418-136">For example System.IO.Compression package is utilizing this technology.</span></span> [<span data-ttu-id="74418-137">https://www.nuget.org/Packages/System.IO.Compression</span><span class="sxs-lookup"><span data-stu-id="74418-137">https://www.nuget.org/packages/System.IO.Compression</span></span>](https://www.nuget.org/packages/System.IO.Compression)

<span data-ttu-id="74418-138">Yukarıdaki işlevselliği kesinlikle gerekli değilse, burada açıklanan biçimde yalnızca NuGet 3.x+ tarafından desteklenen olarak Özet olarak var olan paketi biçimiyle kalmanız öneririz.</span><span class="sxs-lookup"><span data-stu-id="74418-138">In summary if the functionality above is not absolutely necessary, we recommend sticking with the existing package format, as the format described here is supported only by NuGet 3.x+.</span></span>

<span data-ttu-id="74418-139">Her ikisi için çalışmaya paketleri oluşturmak mümkün `packages.config` ve `project.json` shimming, ancak genellikle yalnızca yukarıda belirtilen kullanım dışı özellikler olmadan geleneksel şekilde paketleri yapısı daha basit olduğu aracılığıyla senaryoları.</span><span class="sxs-lookup"><span data-stu-id="74418-139">It would be possible to build packages to work for both `packages.config` and `project.json` scenarios through shimming, however it's often simpler to just structure the packages the traditional way, without the deprecated features mentioned above.</span></span>


## <a name="3x-package-format"></a><span data-ttu-id="74418-140">3.x paket biçimi</span><span class="sxs-lookup"><span data-stu-id="74418-140">3.x package format</span></span>  ##

<span data-ttu-id="74418-141">3.x paket biçimi NuGet ötesinde çeşitli ek özellikler sağlar 2.x:</span><span class="sxs-lookup"><span data-stu-id="74418-141">The 3.x package format allows for several additional features beyond NuGet 2.x:</span></span>

1. <span data-ttu-id="74418-142">Derleme ve bir dizi farklı platformlar/cihaz üzerinde çalışma zamanı için kullanılan uygulama derlemeler için kullanılan bir referans derlemesini tanımlama.</span><span class="sxs-lookup"><span data-stu-id="74418-142">Defining a reference assembly used for compilation and a set of implementation assemblies used for runtime on different platforms/devices.</span></span> <span data-ttu-id="74418-143">Platform özel yararlanmak verir tüketicileriniz için ortak bir yüzey alanını sağlarken API'leri.</span><span class="sxs-lookup"><span data-stu-id="74418-143">Which allows you to take advantage of platform specific APIs while providing a common surface area for your consumers.</span></span> <span data-ttu-id="74418-144">Özellikle bu şekilde, daha kolay Ara taşınabilir kitaplıklara yazmayı kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="74418-144">Specifically this makes writing intermediate portable libraries easier.</span></span>

2. <span data-ttu-id="74418-145">İşletim sistemleri veya CPU mimarisi platformlarda Örneğin Özet paketleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="74418-145">Allows packages to pivot on platforms e.g. operating systems or CPU architecture.</span></span>

3. <span data-ttu-id="74418-146">Platform belirli uygulamaları Yardımcısı paketlere ayrımı sağlar.</span><span class="sxs-lookup"><span data-stu-id="74418-146">Allows for separation of platform specific implementations to companion packages.</span></span>

4. <span data-ttu-id="74418-147">Yerel bağımlılıkları birinci sınıf vatandaşı destekler.</span><span class="sxs-lookup"><span data-stu-id="74418-147">Support Native dependencies as a first class citizen.</span></span>