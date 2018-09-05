---
title: NuGet Packages.config dosyasının dosya başvurusu
description: Bazı proje türlerinde packages.config projede kullanılan NuGet paketleri listesini tutar.
author: karann-msft
ms.author: karann
ms.date: 05/21/2018
ms.topic: reference
ms.openlocfilehash: 18566671b611899b28fcc8542cf53935f5ee2dfd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551776"
---
# <a name="packagesconfig-reference"></a><span data-ttu-id="1b544-103">Packages.config başvurusu</span><span class="sxs-lookup"><span data-stu-id="1b544-103">packages.config reference</span></span>

<span data-ttu-id="1b544-104">`packages.config` Dosyası, proje tarafından başvurulan paketlerin listesini korumak için bazı proje türlerinde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1b544-104">The `packages.config` file is used in some project types to maintain the list of packages referenced by the project.</span></span> <span data-ttu-id="1b544-105">Bu proje bağımlılıklarınızı kolayca geri yüklemek NuGet sağlar, bu paketleri olmadan bir yapı sunucusu gibi farklı bir makineye taşınmasını proje.</span><span class="sxs-lookup"><span data-stu-id="1b544-105">This allows NuGet to easily restore the project's dependencies when the project to be transported to a different machine, such as a build server, without all those packages.</span></span>

<span data-ttu-id="1b544-106">Kullandıysanız, `packages.config` genellikle bir proje kök dizininde bulunur.</span><span class="sxs-lookup"><span data-stu-id="1b544-106">If used, `packages.config` is typically located in a project root.</span></span> <span data-ttu-id="1b544-107">İlk NuGet işlemi çalıştırılır, ancak ayrıca el ile herhangi bir komut çalıştırmadan önce aşağıdaki gibi oluşturulabilir otomatik olarak oluşturulur `nuget restore`.</span><span class="sxs-lookup"><span data-stu-id="1b544-107">It's automatically created when the first NuGet operation is run, but can also be created manually before running any commands such as `nuget restore`.</span></span>

<span data-ttu-id="1b544-108">Projeleri [PackageReference](../consume-packages/Package-References-in-Project-Files.md) kullanmayın `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="1b544-108">Projects that use [PackageReference](../consume-packages/Package-References-in-Project-Files.md) do not use `packages.config`.</span></span>

## <a name="schema"></a><span data-ttu-id="1b544-109">Şema</span><span class="sxs-lookup"><span data-stu-id="1b544-109">Schema</span></span>

<span data-ttu-id="1b544-110">Şema basittir: olan tek bir standart XML üst bilgi aşağıdaki `<packages>` birini veya daha fazlasını içeren düğüm `<package>` öğeleri, her başvuru.</span><span class="sxs-lookup"><span data-stu-id="1b544-110">The schema is simple: following the standard XML header is a single `<packages>` node that contains one or more `<package>` elements, one for each reference.</span></span> <span data-ttu-id="1b544-111">Her `<package>` öğesi aşağıdaki özniteliklere sahip olabilir:</span><span class="sxs-lookup"><span data-stu-id="1b544-111">Each `<package>` element can have the following attributes:</span></span>

| <span data-ttu-id="1b544-112">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="1b544-112">Attribute</span></span> | <span data-ttu-id="1b544-113">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1b544-113">Required</span></span> | <span data-ttu-id="1b544-114">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1b544-114">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1b544-115">kimlik</span><span class="sxs-lookup"><span data-stu-id="1b544-115">id</span></span> | <span data-ttu-id="1b544-116">Evet</span><span class="sxs-lookup"><span data-stu-id="1b544-116">Yes</span></span> | <span data-ttu-id="1b544-117">Newtonsoft.json veya Microsoft.AspNet.Mvc gibi paket tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="1b544-117">The identifier of the package, such as Newtonsoft.json or Microsoft.AspNet.Mvc.</span></span> | 
| <span data-ttu-id="1b544-118">sürüm</span><span class="sxs-lookup"><span data-stu-id="1b544-118">version</span></span> | <span data-ttu-id="1b544-119">Evet</span><span class="sxs-lookup"><span data-stu-id="1b544-119">Yes</span></span> | <span data-ttu-id="1b544-120">3.1.1 veya 4.2.5.11-beta gibi yüklemek için paketi tam sürümü.</span><span class="sxs-lookup"><span data-stu-id="1b544-120">The exact version of the package to install, such as 3.1.1 or 4.2.5.11-beta.</span></span> <span data-ttu-id="1b544-121">Bir sürüm dizesi en az üç sayı olması gerekir; Dördüncü, yayın öncesi son olarak, isteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="1b544-121">A version string must have at least three numbers; a fourth is optional, as is a pre-release suffix.</span></span> <span data-ttu-id="1b544-122">Aralıkları izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="1b544-122">Ranges are not allowed.</span></span> | 
| <span data-ttu-id="1b544-123">targetFramework</span><span class="sxs-lookup"><span data-stu-id="1b544-123">targetFramework</span></span> | <span data-ttu-id="1b544-124">Hayır</span><span class="sxs-lookup"><span data-stu-id="1b544-124">No</span></span> | <span data-ttu-id="1b544-125">[Hedef çerçeve adı (TFM)](target-frameworks.md) paketi yüklerken uygulanacak.</span><span class="sxs-lookup"><span data-stu-id="1b544-125">The [target framework moniker (TFM)](target-frameworks.md) to apply when installing the package.</span></span> <span data-ttu-id="1b544-126">Bir paketi yüklendiğinde bu projenin hedef başlangıçta ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="1b544-126">This is initially set to the project's target when a package is installed.</span></span> <span data-ttu-id="1b544-127">Sonuç olarak, farklı `<package>` öğeleri farklı Tfm'ler sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="1b544-127">As a result, different `<package>` elements can have different TFMs.</span></span> <span data-ttu-id="1b544-128">Örneğin, .NET 4.5.2'nin hedefleyen bir proje oluşturursanız, yüklü paketleri bu noktada net452 TFM kullanın.</span><span class="sxs-lookup"><span data-stu-id="1b544-128">For example, if you create a project targeting .NET 4.5.2, packages installed at that point will use the TFM of net452.</span></span> <span data-ttu-id="1b544-129">Varsa, daha sonra .NET 4.6 için projeyi yeniden hedefle ve daha fazla paket ekleme olanlar TFM net46 birini kullanır.</span><span class="sxs-lookup"><span data-stu-id="1b544-129">If you ;later retarget the project to .NET 4.6 and add more packages, those will use TFM of net46.</span></span> <span data-ttu-id="1b544-130">Projenin hedef arasında bir uyuşmazlık ve `targetFramework` öznitelikleri uyarılar üretir, bu durumda, etkilenen paketleri yeniden yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b544-130">A mismatch between the project's target and `targetFramework` attributes will generate warnings, in which case you can reinstall the affected packages.</span></span> | 
| <span data-ttu-id="1b544-131">allowedVersions</span><span class="sxs-lookup"><span data-stu-id="1b544-131">allowedVersions</span></span> | <span data-ttu-id="1b544-132">Hayır</span><span class="sxs-lookup"><span data-stu-id="1b544-132">No</span></span> | <span data-ttu-id="1b544-133">Bir paketi güncelleştirmesi sırasında uygulanan bu paket için izin verilen sürüm aralığı (bkz [Constraining yükseltme sürümlerinin](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span><span class="sxs-lookup"><span data-stu-id="1b544-133">A range of allowed versions for this package applied during package update (see [Constraining upgrade versions](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="1b544-134">Mevcut *değil* hangi paket yükleme sırasında yüklü etkileyebilir veya geri yükleme işlemi.</span><span class="sxs-lookup"><span data-stu-id="1b544-134">It does *not* affect what package is installed during an install or restore operation.</span></span> <span data-ttu-id="1b544-135">Bkz: [Paket sürümü oluşturma](../reference/package-versioning.md#version-ranges-and-wildcards) söz dizimi.</span><span class="sxs-lookup"><span data-stu-id="1b544-135">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for syntax.</span></span> <span data-ttu-id="1b544-136">PackageManager UI ayrıca izin verilen aralığın dışında tüm sürümler devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="1b544-136">The PackageManager UI also disables all versions outside the allowed range.</span></span> | 
| <span data-ttu-id="1b544-137">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="1b544-137">developmentDependency</span></span> | <span data-ttu-id="1b544-138">Hayır</span><span class="sxs-lookup"><span data-stu-id="1b544-138">No</span></span> | <span data-ttu-id="1b544-139">Proje kendisini kullanan, bu ayar bir NuGet paketi oluşturur `true` için bir bağımlılık, paket kaybı paketi oluşturulduğunda eklenmesini engeller.</span><span class="sxs-lookup"><span data-stu-id="1b544-139">If the consuming project itself creates a NuGet package, setting this to `true` for a dependency prevents that package from being included when the consuming package is created.</span></span> <span data-ttu-id="1b544-140">Varsayılan, `false` değeridir.</span><span class="sxs-lookup"><span data-stu-id="1b544-140">The default is `false`.</span></span> | 

## <a name="examples"></a><span data-ttu-id="1b544-141">Örnekler</span><span class="sxs-lookup"><span data-stu-id="1b544-141">Examples</span></span>

<span data-ttu-id="1b544-142">Aşağıdaki `packages.config` için iki bağımlılıkları gösterir:</span><span class="sxs-lookup"><span data-stu-id="1b544-142">The following `packages.config` refers to two dependencies:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

<span data-ttu-id="1b544-143">Aşağıdaki `packages.config` dokuz paketlere başvuruyor ancak `Microsoft.Net.Compilers` nedeniyle alıcı paket oluştururken dahil edilmez `developmentDependency` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="1b544-143">The following `packages.config` refers to nine packages, but `Microsoft.Net.Compilers` will not be included when building the consuming package because of the `developmentDependency` attribute.</span></span> <span data-ttu-id="1b544-144">Newtonsoft.Json başvuru, aynı zamanda yalnızca 8.x ve 9.x sürümlere güncelleştirmeler kısıtlar.</span><span class="sxs-lookup"><span data-stu-id="1b544-144">The reference to Newtonsoft.Json also restricts updates to 8.x and 9.x versions only.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="Microsoft.CodeDom.Providers.DotNetCompilerPlatform" version="1.0.0" targetFramework="net46" />
  <package id="Microsoft.Net.Compilers" version="1.0.0" targetFramework="net46" developmentDependency="true" />
  <package id="Microsoft.Web.Infrastructure" version="1.0.0.0" targetFramework="net46" />
  <package id="Microsoft.Web.Xdt" version="2.1.1" targetFramework="net46" />
  <package id="Newtonsoft.Json" version="8.0.3" allowedVersions="[8,10)" targetFramework="net46" />
  <package id="NuGet.Core" version="2.11.1" targetFramework="net46" />
  <package id="NuGet.Server" version="2.11.2" targetFramework="net46" />
  <package id="RouteMagic" version="1.3" targetFramework="net46" />
  <package id="WebActivatorEx" version="2.1.0" targetFramework="net46" />
</packages>
```
