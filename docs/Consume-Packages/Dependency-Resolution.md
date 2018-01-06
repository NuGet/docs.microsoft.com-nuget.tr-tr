---
title: "NuGet paketi bağımlılık çözümleme | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 8/14/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 1d530a72-3486-4a0d-b6fb-017524616f91
description: "Üzerinden bir NuGet paketin bağımlılıklarını çözümlendi ve her iki NuGet yüklü işlemiyle ilgili ayrıntılar 2.x ve NuGet 3.x+."
keywords: "NuGet Paket bağımlılıklarını, NuGet sürüm oluşturma, bağımlılık sürümleri, sürüm grafiği, sürüm çözünürlüğü, geçişli geri yükleme"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 251ae6944cc0010f596c9b3daf95c318595a5c4d
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/05/2018
---
# <a name="how-nuget-resolves-package-dependencies"></a><span data-ttu-id="dced5-104">NuGet Paket bağımlılıklarını nasıl çözümler</span><span class="sxs-lookup"><span data-stu-id="dced5-104">How NuGet resolves package dependencies</span></span>

<span data-ttu-id="dced5-105">Bir parçası olarak yüklenen içeren bir paket yüklü veya yeniden, dilediğiniz zaman bir [geri](../consume-packages/package-restore.md) işlemi, NuGet de ilk paket bağımlı olduğu herhangi bir ek paket yükler.</span><span class="sxs-lookup"><span data-stu-id="dced5-105">Any time a package is installed or reinstalled, which includes being installed as part of a [restore](../consume-packages/package-restore.md) process, NuGet also installs any additional packages on which that first package depends.</span></span>

<span data-ttu-id="dced5-106">Bu hemen bağımlılıkları da kendi başlarına, için rasgele bir derinliği devam edebilirsiniz bağımlılıkları olabilir.</span><span class="sxs-lookup"><span data-stu-id="dced5-106">Those immediate dependencies might then also have dependencies on their own, which can continue to an arbitrary depth.</span></span> <span data-ttu-id="dced5-107">Bu ne adlı üreten bir *bağımlılık grafiğinin* paketleri arasındaki ilişkileri açıklar tüm düzeyleri şunlardır.</span><span class="sxs-lookup"><span data-stu-id="dced5-107">This produces what's called a *dependency graph* that describes the relationships between packages are all levels.</span></span>

<span data-ttu-id="dced5-108">Birden çok paket aynı bağımlılık varsa, daha sonra aynı paket kimliği grafikte birden çok kez olası farklı sürüm kısıtlamalarıyla görünebilir.</span><span class="sxs-lookup"><span data-stu-id="dced5-108">When multiple packages have the same dependency, then the same package ID can appear in the graph multiple times, potentially with different version constraints.</span></span> <span data-ttu-id="dced5-109">NuGet hangi sürümü seçmeniz gerekir böylece ancak, belirli bir paket yalnızca bir sürümü bir projede kullanılabilir kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="dced5-109">However, only one version of a given package can be used in a project, so NuGet must choose which version is be used.</span></span> <span data-ttu-id="dced5-110">Tam işlem kullanılan paket başvuru biçimi bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="dced5-110">The exact process depends on the package reference format being used.</span></span>

<span data-ttu-id="dced5-111">Bu konuda:</span><span class="sxs-lookup"><span data-stu-id="dced5-111">In this topic:</span></span>
- [<span data-ttu-id="dced5-112">PackageReference ve project.json bir bağımlılık çözümleme</span><span class="sxs-lookup"><span data-stu-id="dced5-112">Dependency resolution with PackageReference and project.json</span></span>](#dependency-resolution-with-packagereference-and-projectjson)
- [<span data-ttu-id="dced5-113">Packages.config bir bağımlılık çözümleme</span><span class="sxs-lookup"><span data-stu-id="dced5-113">Dependency resolution with packages.config</span></span>](#dependency-resolution-with-packagesconfig)
- <span data-ttu-id="dced5-114">[Başvuruları hariç](#excluding-references), bir proje ve bir başkası tarafından üretilen bir derlemeyi belirtilen bir bağımlılık arasında bir çakışma olduğunda gerekli olduğu.</span><span class="sxs-lookup"><span data-stu-id="dced5-114">[Excluding references](#excluding-references), which is necessary when there's a conflict between a dependency specified in one project and an assembly that's produced by another.</span></span>
- [<span data-ttu-id="dced5-115">Paket sırasında bağımlılık güncelleştirmeleri yükle</span><span class="sxs-lookup"><span data-stu-id="dced5-115">Dependency updates during package install</span></span>](#dependency-updates-during-package-install)
- [<span data-ttu-id="dced5-116">Uyumsuz paket hatalarını çözme</span><span class="sxs-lookup"><span data-stu-id="dced5-116">Resolving incompatible package errors</span></span>](#resolving-incompatible-package-errors)

## <a name="dependency-resolution-with-packagereference-and-projectjson"></a><span data-ttu-id="dced5-117">PackageReference ve project.json bir bağımlılık çözümleme</span><span class="sxs-lookup"><span data-stu-id="dced5-117">Dependency resolution with PackageReference and project.json</span></span>

<span data-ttu-id="dced5-118">Paketleri PackageReference kullanarak projelere yüklerken veya `project.json` biçimleri, NuGet uygun dosyasında bir düz paket grafik başvuruları ekler ve önceden çakışmalar çözümlendi.</span><span class="sxs-lookup"><span data-stu-id="dced5-118">When installing packages into projects using the PackageReference or `project.json` formats, NuGet adds references to a flat package graph in the appropriate file and resolves conflicts ahead of time.</span></span> <span data-ttu-id="dced5-119">Bu işlem olarak adlandırılır *geçişli geri yükleme*.</span><span class="sxs-lookup"><span data-stu-id="dced5-119">This process is referred to as *transitive restore*.</span></span> <span data-ttu-id="dced5-120">Yeniden yüklemeyi veya paketleri geri sonra daha hızlı sonuçta grafikte listelenen paketler indirme işlemi ve daha tahmin edilebilir oluşturur.</span><span class="sxs-lookup"><span data-stu-id="dced5-120">Reinstalling or restoring packages is then a process of downloading the packages listed in the graph, resulting in faster and more predictable builds.</span></span> <span data-ttu-id="dced5-121">Ayrıca 2.8 gibi joker karakter (kayan) sürümlerinden yararlanabilirsiniz. \*, pahalı önlemenin ve hata potansiyeli çağrıları `nuget update` yapı sunucuları ve istemci makineleri.</span><span class="sxs-lookup"><span data-stu-id="dced5-121">You can also take advantage of wildcard (floating) versions, such as 2.8.\*, avoiding expensive and error prone calls to `nuget update` on the client machines and build servers.</span></span>

<span data-ttu-id="dced5-122">NuGet geri yükleme işlemi önce bir yapı çalıştığında, bağımlılıkları ilk bellekte çözümler, ardından, elde edilen grafik adlı bir dosyaya yazar `project.assets.json` içinde `obj` klasörü PackageReference kullanarak bir proje veya adlı bir dosyaya `project.lock.json` yanında `project.json`.</span><span class="sxs-lookup"><span data-stu-id="dced5-122">When the NuGet restore process runs prior to a build, it resolves dependencies first in memory, then writes the resulting graph to a file called `project.assets.json` in the `obj` folder of a project using PackageReference, or in a file named `project.lock.json` alongside `project.json`.</span></span> <span data-ttu-id="dced5-123">MSBuild sonra bu dosyayı okur ve burada olası başvurular bulunabilir ve ardından bunları bellek proje ağacında ekler klasörler kümesi çevirir.</span><span class="sxs-lookup"><span data-stu-id="dced5-123">MSBuild then reads this file and translates it into a set of folders where potential references can be found, and then adds them to the project tree in memory.</span></span>

<span data-ttu-id="dced5-124">Kilit dosyası geçicidir ve kaynak denetimi eklenmemesi.</span><span class="sxs-lookup"><span data-stu-id="dced5-124">The lock file is temporary and should not be added to source control.</span></span> <span data-ttu-id="dced5-125">Hem de varsayılan olarak listelenen `.gitignore` ve `.tfignore`.</span><span class="sxs-lookup"><span data-stu-id="dced5-125">It's listed by default in both `.gitignore` and `.tfignore`.</span></span> <span data-ttu-id="dced5-126">Bkz: [paketler ve kaynak denetimi](Packages-and-Source-Control.md).</span><span class="sxs-lookup"><span data-stu-id="dced5-126">See [Packages and source control](Packages-and-Source-Control.md).</span></span>

### <a name="dependency-resolution-rules"></a><span data-ttu-id="dced5-127">Bağımlılık çözümleme kurallarını</span><span class="sxs-lookup"><span data-stu-id="dced5-127">Dependency resolution rules</span></span>

<span data-ttu-id="dced5-128">Geçişli geri yükleme bağımlılıkları çözümlemek için dört ana kuralları uygular: en düşük geçerli sürüm, kayan sürümleri, en yakın WINS ve Kuzen bağımlılıkları.</span><span class="sxs-lookup"><span data-stu-id="dced5-128">Transitive restore applies four main rules to resolve dependencies: lowest applicable version, floating versions, nearest-wins, and cousin dependencies.</span></span>

<a name="lowest-applicable-version"></a>

#### <a name="lowest-applicable-version"></a><span data-ttu-id="dced5-129">En düşük geçerli sürüm</span><span class="sxs-lookup"><span data-stu-id="dced5-129">Lowest applicable version</span></span>

<span data-ttu-id="dced5-130">En düşük geçerli sürüm kuralı bağımlılıklarını tarafından tanımlandığı şekilde bir paketin olası en düşük sürümü yükler.</span><span class="sxs-lookup"><span data-stu-id="dced5-130">The lowest applicable version rule restores the lowest possible version of a package as defined by its dependencies.</span></span> <span data-ttu-id="dced5-131">Ayrıca uygulama veya sınıf kitaplığı bağımlılıkları olarak bildirilir sürece uygulandığı [kayan](#floating-versions).</span><span class="sxs-lookup"><span data-stu-id="dced5-131">It also applies to dependencies on the application or the class library unless declared as [floating](#floating-versions).</span></span>

<span data-ttu-id="dced5-132">NuGet 1.0 sürümü seçer şekilde aşağıdaki şekilde, örneğin, 1.0 beta 1.0 düşük olarak kabul edilir:</span><span class="sxs-lookup"><span data-stu-id="dced5-132">In the following figure, for example, 1.0-beta is considered lower than 1.0 so NuGet chooses the 1.0 version:</span></span>

![Geçerli en düşük sürüm seçme](media/projectJson-dependency-1.png)

<span data-ttu-id="dced5-134">Sonraki şekilde, sürüm 2.1 Besleme üzerindeki kullanılabilir değil ancak sürüm kısıtlaması olduğundan > bunu bulabilir, bu durumda 2.2 sonraki en düşük sürüm 2.1 NuGet Çekmeleri =:</span><span class="sxs-lookup"><span data-stu-id="dced5-134">In the next figure, version 2.1 is not available on the feed but because the version constraint is >= 2.1 NuGet picks the next lowest version it can find, in this case 2.2:</span></span>

![Özet akışı kullanılabilir sonraki en düşük sürüm seçme](media/projectJson-dependency-2.png)

<span data-ttu-id="dced5-136">Uygulamanın Besleme üzerindeki kullanılabilir değil, 1.2 gibi bir tam sürüm numarası belirttiğinde NuGet bir hata ile yüklemek veya paket geri yükleme girişimi sırasında başarısız oluyor:</span><span class="sxs-lookup"><span data-stu-id="dced5-136">When an application specifies an exact version number, such as 1.2, that is not available on the feed, NuGet fails with an error when attempting to install or restore the package:</span></span>

![Bir tam paket sürümü mevcut olmadığında NuGet, bir hata oluşturur.](media/projectJson-dependency-3.png)

<a name="floating-versions"></a>

#### <a name="floating-wildcard-versions"></a><span data-ttu-id="dced5-138">(Joker karakterler) kayan sürümleri</span><span class="sxs-lookup"><span data-stu-id="dced5-138">Floating (wildcard) versions</span></span>

<span data-ttu-id="dced5-139">Bir kayan veya joker karakter bağımlılık sürümü ile belirtilen \* joker karakter olarak 6.0 ile.\*.</span><span class="sxs-lookup"><span data-stu-id="dced5-139">A floating or wildcard dependency version is specified with the \* wildcard, as with 6.0.\*.</span></span> <span data-ttu-id="dced5-140">"En son 6.0.x sürümü kullan"; Bu sürüm belirtimi diyor 4.\* anlamına gelir "kullan en son 4.x sürümünü."</span><span class="sxs-lookup"><span data-stu-id="dced5-140">This version specification says "use the latest 6.0.x version"; 4.\* means "use the latest 4.x version."</span></span> <span data-ttu-id="dced5-141">Bir joker karakter kullanılması, bir kullanıcı uygulama için bir değişiklik gerektirmeden gelişen devam etmek için bağımlılık paketi (veya paketi) sağlar.</span><span class="sxs-lookup"><span data-stu-id="dced5-141">Using a wildcard allows a dependency package to continue evolving without requiring a change to the consuming application (or package).</span></span>

<span data-ttu-id="dced5-142">Joker karakter kullanırken, NuGet yüksek paketinin sürümünü, örneğin 6.0 sürüm desenle eşleşen bir çözümler. \* en yüksek sürüm 6.0 ile başlayan bir paketin alır:</span><span class="sxs-lookup"><span data-stu-id="dced5-142">When using a wildcard, NuGet resolves the highest version of a package that matches the version pattern, for example 6.0.\* gets the highest version of a package that starts with 6.0:</span></span>

![Sürüm 6.0.1 kayan bir sürüm olduğunda 6.0 seçme. * İstenen](media/projectJson-dependency-4.png)

> [!Note]
> <span data-ttu-id="dced5-144">Joker karakterler ve yayın öncesi sürümlerini davranışı hakkında bilgi için bkz: [paket sürüm](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="dced5-144">For information on the behavior of wildcards and pre-release versions, see [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>


<a name="nearest-wins"></a>

#### <a name="nearest-wins"></a><span data-ttu-id="dced5-145">Yakın WINS</span><span class="sxs-lookup"><span data-stu-id="dced5-145">Nearest wins</span></span>

<span data-ttu-id="dced5-146">Bir uygulama için paket grafik aynı paketin farklı sürümlerini içerdiğinde, NuGet grafiği uygulamada yakın ve diğer tüm yoksayar paketi seçer.</span><span class="sxs-lookup"><span data-stu-id="dced5-146">When the package graph for an application contains different versions of the same package, NuGet chooses the package that's closest to the application in the graph and ignores all others.</span></span> <span data-ttu-id="dced5-147">Bu davranış herhangi belirli paket sürümünü bağımlılık grafiğinin geçersiz kılmak bir uygulama sağlar.</span><span class="sxs-lookup"><span data-stu-id="dced5-147">This behavior allows an application to override any particular package version in the dependency graph.</span></span>

<span data-ttu-id="dced5-148">Aşağıdaki örnekte, uygulamanın doğrudan sürüm kısıtlaması, paket B bağımlı > 2.0 =.</span><span class="sxs-lookup"><span data-stu-id="dced5-148">In the example below, the application depends directly on Package B with a version constraint of >=2.0.</span></span> <span data-ttu-id="dced5-149">Uygulamanın Paket B, aynı ile sırayla de bağlıdır A paketi de bağımlı bir > 1.0 kısıtlaması =.</span><span class="sxs-lookup"><span data-stu-id="dced5-149">The application also depends on Package A which in turn also depends on Package B, but with a >=1.0 constraint.</span></span> <span data-ttu-id="dced5-150">Grafik uygulamada nearer to Paket B 2.0 bağımlı olduğu için bu sürüm kullanılır:</span><span class="sxs-lookup"><span data-stu-id="dced5-150">Because the dependency on Package B 2.0 is nearer to the application in the graph, that version is used:</span></span>

![Yakın WINS kuralı kullanarak uygulama](media/projectJson-dependency-5.png)

>[!Warning]
> <span data-ttu-id="dced5-152">Yakın WINS kural böylece büyük olasılıkla başka bir bağımlılık grafikte yeni Paket sürümü, eski sürüme düşürülmesini neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="dced5-152">The Nearest Wins rule can result in a downgrade of the package version, thus potentially breaking other dependencies in the graph.</span></span> <span data-ttu-id="dced5-153">Bu nedenle bu kural bir uyarı ile kullanıcıyı uyarmak için uygulanır.</span><span class="sxs-lookup"><span data-stu-id="dced5-153">Hence this rule is applied with a warning to alert the user.</span></span>

<span data-ttu-id="dced5-154">Verilen bir bağımlılık göz ardı sonra NuGet de o şubedeki grafik kalan tüm bağımlılıkları yoksayar çünkü bu kural ayrıca verimliliği büyük bağımlılık grafiğinin (örneğin BCL paketleri olanlar) ile sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="dced5-154">This rule also results in greater efficiency with a large dependency graph (such as those with the BCL packages) because once a given dependency is ignored, NuGet also ignores all remaining dependencies on that branch of the graph.</span></span> <span data-ttu-id="dced5-155">Paket C 2.0 kullanıldığından, aşağıdaki çizimde NuGet paketi C: daha eski bir sürümü başvuran tüm dalları grafikte örneğin yoksayar.</span><span class="sxs-lookup"><span data-stu-id="dced5-155">In the diagram below, for example, because Package C 2.0 is used, NuGet ignores any branches in the graph that refer to an older version of Package C:</span></span>

![NuGet paket grafikte yoksayar, tüm bu dalı yoksayar](media/projectJson-dependency-6.png)

<a name="cousin-dependencies"></a>

#### <a name="cousin-dependencies"></a><span data-ttu-id="dced5-157">Kuzen bağımlılıkları</span><span class="sxs-lookup"><span data-stu-id="dced5-157">Cousin dependencies</span></span>

<span data-ttu-id="dced5-158">Farklı paketi sürümleri için grafikte aynı uzaklıkta uygulamadan adlandırılır NuGet tüm sürüm gereksinimlerini karşılayan en düşük sürüm kullanır (olduğu gibi [en düşük geçerli sürüm](#lowest-applicable-version) ve [ sürümleri kayan](#floating-versions) kuralları).</span><span class="sxs-lookup"><span data-stu-id="dced5-158">When different package versions are referred to at the same distance in the graph from the application, NuGet uses the lowest version that satisfies all version requirements (as with the [lowest applicable version](#lowest-applicable-version) and [floating versions](#floating-versions) rules).</span></span> <span data-ttu-id="dced5-159">Aşağıdaki resimde, örneğin, paket B 2.0 sürümünü diğer karşılayan > 1.0 kısıtlaması = ve bu nedenle kullanılır:</span><span class="sxs-lookup"><span data-stu-id="dced5-159">In the image below, for example, version 2.0 of Package B satisfies the other >=1.0 constraint, and is thus used:</span></span>

![Tüm kısıtlamaları karşılayan düşük sürümünü kullanarak Kuzen bağımlılıkları çözümleniyor](media/projectJson-dependency-7.png)

<span data-ttu-id="dced5-161">Bazı durumlarda, tüm sürüm gereksinimlerini karşılamak olası değil.</span><span class="sxs-lookup"><span data-stu-id="dced5-161">In some cases, it's not possible to meet all version requirements.</span></span> <span data-ttu-id="dced5-162">Aşağıda gösterildiği gibi paketi A tam olarak paket B 1.0 gerektirir ve paket C gerektiriyorsa Paket B > NuGet bağımlılıklar çözümlenemiyor ve bir hata verir 2.0 =.</span><span class="sxs-lookup"><span data-stu-id="dced5-162">As shown below, if Package A requires exactly Package B 1.0 and Package C requires Package B >=2.0, then NuGet cannot resolve the dependencies and gives an error.</span></span>

![Bir tam sürüm gereksinimini nedeniyle çözülemeyen bağımlılıkları](media/projectJson-dependency-8.png)

<span data-ttu-id="dced5-164">Bu durumlarda, üst düzey bir tüketici (uygulama veya Paketle) doğrudan bağımlılık Paket B eklemeniz gerekir böylece [yakın WINS](#nearest-wins) kuralı uygular.</span><span class="sxs-lookup"><span data-stu-id="dced5-164">In these situations, the top-level consumer (the application or package) should add its own direct dependency on Package B so that the [Nearest Wins](#nearest-wins) rule applies.</span></span>

## <a name="dependency-resolution-with-packagesconfig"></a><span data-ttu-id="dced5-165">Packages.config bir bağımlılık çözümleme</span><span class="sxs-lookup"><span data-stu-id="dced5-165">Dependency resolution with packages.config</span></span>

<span data-ttu-id="dced5-166">İle `packages.config`, bir projenin bağımlılıkları yazılır `packages.config` düz bir liste olarak.</span><span class="sxs-lookup"><span data-stu-id="dced5-166">With `packages.config`, a project's dependencies are written to `packages.config` as a flat list.</span></span> <span data-ttu-id="dced5-167">Bu paket bağımlılıkları da aynı listesinde yazılır.</span><span class="sxs-lookup"><span data-stu-id="dced5-167">Any dependencies of those packages are also written in the same list.</span></span> <span data-ttu-id="dced5-168">NuGet paketleri yüklendiğinde, ayrıca değişiklik `.csproj` dosyası `app.config`, `web.config`ve tek tek diğer dosyaları.</span><span class="sxs-lookup"><span data-stu-id="dced5-168">When packages are installed, NuGet might also modify the `.csproj` file, `app.config`, `web.config`, and other individual files.</span></span>

<span data-ttu-id="dced5-169">İle `packages.config`, NuGet tek tek her paketin yüklenmesi sırasında bağımlılık çakışmaları dener.</span><span class="sxs-lookup"><span data-stu-id="dced5-169">With `packages.config`, NuGet attempts to resolve dependency conflicts during the installation of each individual package.</span></span> <span data-ttu-id="dced5-170">A paketi yükleniyor ve paket B ve paket B bağlıdır, diğer bir deyişle, zaten listede `packages.config` bir bağımlılık, başka bir NuGet paketi istenen B sürümlerini karşılaştırır ve tüm sürüm karşılayan bir sürümünü bulmaya çalışır kısıtlamaları.</span><span class="sxs-lookup"><span data-stu-id="dced5-170">That is, if Package A is being installed and depends on Package B, and Package B is already listed in `packages.config` as a dependency of something else, NuGet compares the versions of Package B being requested and attempts to find a version that satisfies all version constraints.</span></span> <span data-ttu-id="dced5-171">Özellikle, NuGet alt seçer *major.minor* bağımlılıkları karşılayan sürümü.</span><span class="sxs-lookup"><span data-stu-id="dced5-171">Specifically, NuGet selects the lower *major.minor* version that satisfies dependencies.</span></span>

<span data-ttu-id="dced5-172">Varsayılan olarak, NuGet 2.7 ve önceki en yüksek çözümler *düzeltme eki* sürüm (kullanarak *major.minor.patch.build* kuralı).</span><span class="sxs-lookup"><span data-stu-id="dced5-172">By default, NuGet 2.7 and earlier resolves the highest *patch* version (using the *major.minor.patch.build* convention).</span></span> <span data-ttu-id="dced5-173">[NuGet 2.8 ve daha yüksek](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies) için en düşük düzeltme eki sürümü varsayılan olarak aramak için bu davranış değişir.</span><span class="sxs-lookup"><span data-stu-id="dced5-173">[NuGet 2.8 and higher](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies) changes this behavior to look for the lowest patch version by default.</span></span> <span data-ttu-id="dced5-174">Bu ayarı kullanılarak denetleyebilirsiniz `DependencyVersion` özniteliğini `Nuget.Config` ve `-DependencyVersion` komut satırında geçin.</span><span class="sxs-lookup"><span data-stu-id="dced5-174">You can control this setting through the `DependencyVersion` attribute in `Nuget.Config` and the `-DependencyVersion` switch on the command line.</span></span>  

<span data-ttu-id="dced5-175">`packages.config` Bağımlılıkları çözümleniyor büyük bağımlılık grafikleri için karmaşık alır için işlem.</span><span class="sxs-lookup"><span data-stu-id="dced5-175">The `packages.config` process for resolving dependencies gets complicated for larger dependency graphs.</span></span> <span data-ttu-id="dced5-176">Her yeni paket yükleme tüm grafik çapraz geçişi gerektirir ve sürüm çakışmaları için Fırsat başlatır.</span><span class="sxs-lookup"><span data-stu-id="dced5-176">Each new package installation requires a traversal of the whole graph and raises the chance for version conflicts.</span></span> <span data-ttu-id="dced5-177">Bir çakışma oluştuğunda, özellikle proje dosyasına olası değişiklikleri ile belirlenmemiş bir durum proje bırakarak yükleme durdurulur.</span><span class="sxs-lookup"><span data-stu-id="dced5-177">When a conflict occurs, installation is stopped, leaving the project in an indeterminate state, especially with potential modifications to the project file itself.</span></span> <span data-ttu-id="dced5-178">Bu sorunu diğer paketi başvurusu biçimleri kullanırken değildir.</span><span class="sxs-lookup"><span data-stu-id="dced5-178">This is not an issue when using other package reference formats.</span></span>


## <a name="managing-dependency-assets"></a><span data-ttu-id="dced5-179">Bağımlılık varlıklarını yönetme</span><span class="sxs-lookup"><span data-stu-id="dced5-179">Managing dependency assets</span></span>

<span data-ttu-id="dced5-180">Kullanırken `project.json` veya PackageReference biçimleri, üst düzey proje bağımlılıkları akışına hangi varlıklarından kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dced5-180">When using the `project.json` or PackageReference formats, you can control which assets from dependencies flow into the top-level project.</span></span> <span data-ttu-id="dced5-181">Ayrıntılar için bkz [project.json](../Schema/project-json.md) ve [paketini proje dosyalarını başvurularında](Package-References-in-Project-Files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="dced5-181">For details, see [project.json](../Schema/project-json.md) and [Package references in project files](Package-References-in-Project-Files.md#controlling-dependency-assets).</span></span>

<span data-ttu-id="dced5-182">Üst düzey proje kendisini bir paketi olduğunda, bu akış denetime kullanarak de `include` ve `exclude` listelenen bağımlılıkları özniteliklerle `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="dced5-182">When the top-level project is itself a package, you also have control over this flow by using the `include` and `exclude` attributes with dependencies listed in the `.nuspec` file.</span></span> <span data-ttu-id="dced5-183">Bkz: [.nuspec başvuru - bağımlılıkları](../Schema/nuspec.md#dependencies).</span><span class="sxs-lookup"><span data-stu-id="dced5-183">See [.nuspec Reference - Dependencies](../Schema/nuspec.md#dependencies).</span></span>

## <a name="excluding-references"></a><span data-ttu-id="dced5-184">Başvuruları hariç</span><span class="sxs-lookup"><span data-stu-id="dced5-184">Excluding references</span></span>

<span data-ttu-id="dced5-185">İçinde aynı ada sahip birden çok kez bir projede tasarım zamanı ve derleme zamanı hatalarını oluşturan başvurulan derlemeler senaryo vardır.</span><span class="sxs-lookup"><span data-stu-id="dced5-185">There are scenarios in which assemblies with the same name might be referenced more than once in a project, producing design-time and build-time errors.</span></span> <span data-ttu-id="dced5-186">Özel bir sürümünü içeren bir proje göz önünde bulundurun `C.dll`ve ayrıca içeren paket C başvurur `C.dll`.</span><span class="sxs-lookup"><span data-stu-id="dced5-186">Consider a project that contains a custom version of `C.dll`, and references Package C that also contains `C.dll`.</span></span> <span data-ttu-id="dced5-187">Aynı anda proje de aynı zamanda paket C bağlıdır Paket B bağlıdır ve `C.dll`.</span><span class="sxs-lookup"><span data-stu-id="dced5-187">At the same time, the project also depends on Package B which also depends on Package C and `C.dll`.</span></span> <span data-ttu-id="dced5-188">Sonuç olarak, NuGet hangi belirleyemiyor `C.dll` kullanmak için ancak Paket B de ona bağımlı olduğundan paket C projenin bağımlılığını yalnızca kaldıramazsınız.</span><span class="sxs-lookup"><span data-stu-id="dced5-188">As a result, NuGet can't determine which `C.dll` to use, but you can't just remove the project's dependency on Package C because Package B also depends on it.</span></span>

<span data-ttu-id="dced5-189">Bu sorunu çözmek için doğrudan başvurmalıdır `C.dll` sizin (veya doğru olanı başvuran başka bir paket kullanmak) ve ardından bir bağımlılık paketi C tüm varlıklarını dışlar ekleyin.</span><span class="sxs-lookup"><span data-stu-id="dced5-189">To resolve this, you must directly reference the `C.dll` you want (or use another package that references the right one), and then add a dependency on Package C that excludes all its assets.</span></span> <span data-ttu-id="dced5-190">Bu paketi başvurusu biçime bağlı olarak şu şekilde gerçekleştirilir:</span><span class="sxs-lookup"><span data-stu-id="dced5-190">This is done as follows depending on the package reference format in use:</span></span>

- <span data-ttu-id="dced5-191">[PackageReference](../consume-packages/package-references-in-project-files.md): eklemek `Exclude="All"` bağımlılık olarak:</span><span class="sxs-lookup"><span data-stu-id="dced5-191">[PackageReference](../consume-packages/package-references-in-project-files.md): add `Exclude="All"` in the dependency:</span></span>

    ```xml
    <PackageReference Include="PackageC" Version="1.0.0" Exclude="All" />
    ```

- <span data-ttu-id="dced5-192">`packages.config`: PackageC başvurusunu kaldırın `.csproj` yalnızca sürümüne başvuruyor dosyasını `C.dll` istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="dced5-192">`packages.config`: remove the reference to PackageC from the `.csproj` file so that it references only the version of `C.dll` that you want.</span></span>
    
- <span data-ttu-id="dced5-193">`project.json`: eklemek `"exclude" : "all"` PackageC bağımlılığı içinde:</span><span class="sxs-lookup"><span data-stu-id="dced5-193">`project.json`: add `"exclude" : "all"` in the dependency for PackageC:</span></span>

    ```json
    {
        "dependencies": {
            "PackageC": {
            "version": "1.0.0",
            "exclude": "all"
            }
        }
    }
    ```

## <a name="dependency-updates-during-package-install"></a><span data-ttu-id="dced5-194">Paket sırasında bağımlılık güncelleştirmeleri yükle</span><span class="sxs-lookup"><span data-stu-id="dced5-194">Dependency updates during package install</span></span> 

<span data-ttu-id="dced5-195">NuGet ile 2.4.x ve, bağımlılık projede zaten bir paketi yüklendiğinde, mevcut sürümü de bu kısıtlamalar uymazsa bile daha önce bağımlılık sürümü kısıtlamaları karşılayan en son sürümüne güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="dced5-195">With NuGet 2.4.x and earlier, when a package is installed whose dependency already exists in the project, the dependency is updated to the latest version that satisfies the version constraints, even if the existing version also satisfies those constraints.</span></span> 

<span data-ttu-id="dced5-196">Örneğin, paket B paketine bağlıdır ve 1.0 için sürüm numarasını belirtir A göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="dced5-196">For example, consider package A that depends on package B and specifies 1.0 for the version number.</span></span> <span data-ttu-id="dced5-197">Her iki sürümü 1.0, 1.1 ve 1.2 paketinin B. kaynak deposu içerir A B sürüm 1.0 zaten içeren projede yüklü ise B sürüm 1.2 güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="dced5-197">The source repository contains both versions 1.0, 1.1, and 1.2 of package B. If A is installed in a project that already contains B version 1.0, then B is updated to version 1.2.</span></span> 

<span data-ttu-id="dced5-198">Bağımlılık sürümünü zaten sağlanıyorsa bağımlılık NuGet 2.5 ve daha sonra diğer paket yüklemeleri sırasında güncelleştirilmez.</span><span class="sxs-lookup"><span data-stu-id="dced5-198">With NuGet 2.5 and later, if a dependency version is already satisfied, the dependency isn't updated during other package installations.</span></span> 

<span data-ttu-id="dced5-199">Aynı yukarıdaki örnekte, paket B 1.0 projesinde NuGet 2.5 ve daha sonraki bir projesine bırakır paketi yüklerken, olarak zaten sürüm kısıtlamasına.</span><span class="sxs-lookup"><span data-stu-id="dced5-199">In the same example above, installing package A into a project with NuGet 2.5 and later leaves package B 1.0 in the project, as it already satisfies the version constraint.</span></span> <span data-ttu-id="dced5-200">A paketi istekleri sürüm 1.1 veya üstü b olsaydı, ancak, ardından B 1.2 yüklenmesi.</span><span class="sxs-lookup"><span data-stu-id="dced5-200">However, if package A had requests version 1.1 or higher of B, then B 1.2 would be installed.</span></span> 

## <a name="resolving-incompatible-package-errors"></a><span data-ttu-id="dced5-201">Uyumsuz paket hatalarını çözme</span><span class="sxs-lookup"><span data-stu-id="dced5-201">Resolving incompatible package errors</span></span>

<span data-ttu-id="dced5-202">Geri yükleme işlemi sırasında bir paket, "bir veya daha fazla paket uyumlu olmadığında..." veya bir paketi "uyumlu değil" hata görebilirsiniz projenin hedef çerçevesi ile.</span><span class="sxs-lookup"><span data-stu-id="dced5-202">During a package restore operation, you may see the error "One or more packages are not compatible..." or that a package "is not compatible" with the project's target framework.</span></span>

<span data-ttu-id="dced5-203">Bu hata, bir veya daha fazla projenizde başvurulan paketleri projenin hedef çerçevesini destekleyen göstermiyor oluşur; diğer bir deyişle, paketi uygun DLL'de içermiyor kendi `lib` proje ile uyumlu olan bir hedef çerçeve için klasör.</span><span class="sxs-lookup"><span data-stu-id="dced5-203">This error occurs when one or more of the packages referenced in your project do not indicate that they support the project's target framework; that is, the package does not contain a suitable DLL in its `lib` folder for a target framework that is compatible with the project.</span></span> <span data-ttu-id="dced5-204">(Bkz [hedef çerçeveler](../Schema/Target-Frameworks.md) bir listesi için.)</span><span class="sxs-lookup"><span data-stu-id="dced5-204">(See [Target frameworks](../Schema/Target-Frameworks.md) for a list.)</span></span> 

<span data-ttu-id="dced5-205">Örneğin, bir proje hedefleri, `netstandard1.6` DLL'leri içinde yalnızca içeren bir paket yüklemeyi denerseniz `lib\net20` ve `\lib\net45` klasörleri olduktan sonra paketi ve muhtemelen, bağımlılıklar için aşağıdaki gibi iletileri göreceksiniz:</span><span class="sxs-lookup"><span data-stu-id="dced5-205">For example, if a project targets `netstandard1.6` and you attempt to install a package that contains DLLs in only the `lib\net20` and `\lib\net45` folders, then you'll see messages like the following for the package and possibly its dependents:</span></span>

```output
Restoring packages for myproject.csproj...
Package ContosoUtilities 2.1.2.3 is not compatible with netstandard1.6 (.NETStandard,Version=v1.6). Package ContosoUtilities 2.1.2.3 supports:
  - net20 (.NETFramework,Version=v2.0)
  - net45 (.NETFramework,Version=v4.5)
Package ContosoCore 0.86.0 is not compatible with netstandard1.6 (.NETStandard,Version=v1.6). Package ContosoCore 0.86.0 supports:
  - 11 (11,Version=v0.0)
  - net20 (.NETFramework,Version=v2.0)
  - sl3 (Silverlight,Version=v3.0)
  - sl4 (Silverlight,Version=v4.0)
One or more packages are incompatible with .NETStandard,Version=v1.6.
Package restore failed. Rolling back package changes for 'MyProject'.
```

<span data-ttu-id="dced5-206">Uyumsuzlukları çözmek için şunlardan birini yapın:</span><span class="sxs-lookup"><span data-stu-id="dced5-206">To resolve incompatibilities, do one of the following:</span></span>

- <span data-ttu-id="dced5-207">Kullanmak istediğiniz paketleri tarafından desteklenen bir çerçeve projenize yeniden hedefleyin.</span><span class="sxs-lookup"><span data-stu-id="dced5-207">Retarget your project to a framework that is supported by the packages you want to use.</span></span>
- <span data-ttu-id="dced5-208">Paket yazarına başvurun ve onlarla seçilen framework desteği eklemek için çalışma.</span><span class="sxs-lookup"><span data-stu-id="dced5-208">Contact the author of the packages and work with them to add support for your chosen framework.</span></span> <span data-ttu-id="dced5-209">Üzerinde sayfa listeleme her paket [nuget.org](https://www.nuget.org/) sahip bir **kişi sahipleri** bu amaç için bağlantı.</span><span class="sxs-lookup"><span data-stu-id="dced5-209">Each package listing page on [nuget.org](https://www.nuget.org/) has a **Contact Owners** link for this purpose.</span></span>
- <span data-ttu-id="dced5-210">**Önerilmez**: geçici bir çözüm olarak için paket yazarına ile çalışırken projeleri hedefleyen `netcore`, `netstandard`, ve `netcoreapp` uyumlu, böylece bu hedefleme paketleri izin verme olarak diğer çerçeveler belirtmek kullanılacak diğer çerçeveler.</span><span class="sxs-lookup"><span data-stu-id="dced5-210">**Not recommended**: as a temporary solution while you work with the package author, projects targeting `netcore`, `netstandard`, and `netcoreapp` can denote other frameworks as being compatible, thereby allowing packages targeting those other frameworks to be used.</span></span> <span data-ttu-id="dced5-211">Bkz: [project.json alır](../Schema/project-json.md#imports) ve [MSBuild geri yükleme hedefi PackageTargetFallback](../Schema/msbuild-targets.md#packagetargetfallback).</span><span class="sxs-lookup"><span data-stu-id="dced5-211">See [project.json imports](../Schema/project-json.md#imports) and [MSBuild restore target PackageTargetFallback](../Schema/msbuild-targets.md#packagetargetfallback).</span></span> <span data-ttu-id="dced5-212">Bu beklenmeyen davranışları neden şekilde yeniden üzerinde bir güncelleştirme için paket yazarına ile çalışarak paket uyumsuzlukları gidermek en iyisidir.</span><span class="sxs-lookup"><span data-stu-id="dced5-212">This can cause unexpected behaviors, so again, it's best to resolve package incompatibilities by working with the package author on an update.</span></span>
