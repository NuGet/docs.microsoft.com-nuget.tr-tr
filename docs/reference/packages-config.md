---
title: NuGet packages.config dosya başvurusu
description: Bazı proje türlerinde, packages.config projede kullanılan NuGet paketlerinin listesini tutar.
author: JonDouglas
ms.author: jodou
ms.date: 05/21/2018
ms.topic: reference
ms.openlocfilehash: 3e5db779f735cd42aa331f9f8a93496d32c8df54
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777622"
---
# <a name="packagesconfig-reference"></a><span data-ttu-id="ee4d2-103">packages.config başvurusu</span><span class="sxs-lookup"><span data-stu-id="ee4d2-103">packages.config reference</span></span>

<span data-ttu-id="ee4d2-104">`packages.config`Dosya, proje tarafından başvurulan paketlerin listesini sürdürmek için bazı proje türlerinde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ee4d2-104">The `packages.config` file is used in some project types to maintain the list of packages referenced by the project.</span></span> <span data-ttu-id="ee4d2-105">Bu, NuGet 'in projenin bağımlılıklarını kolayca geri yüklemesine olanak tanır, çünkü proje bir yapı sunucusu gibi farklı bir makineye taşınır.</span><span class="sxs-lookup"><span data-stu-id="ee4d2-105">This allows NuGet to easily restore the project's dependencies when the project to be transported to a different machine, such as a build server, without all those packages.</span></span>

<span data-ttu-id="ee4d2-106">Kullanılıyorsa, `packages.config` genellikle proje kökünde bulunur.</span><span class="sxs-lookup"><span data-stu-id="ee4d2-106">If used, `packages.config` is typically located in a project root.</span></span> <span data-ttu-id="ee4d2-107">İlk NuGet işlemi çalıştırıldığında otomatik olarak oluşturulur, ancak gibi herhangi bir komut çalıştırılmadan önce el ile de oluşturulabilirler `nuget restore` .</span><span class="sxs-lookup"><span data-stu-id="ee4d2-107">It's automatically created when the first NuGet operation is run, but can also be created manually before running any commands such as `nuget restore`.</span></span>

<span data-ttu-id="ee4d2-108">[Packagereference](../consume-packages/Package-References-in-Project-Files.md) kullanan projeler kullanmaz `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="ee4d2-108">Projects that use [PackageReference](../consume-packages/Package-References-in-Project-Files.md) do not use `packages.config`.</span></span>

## <a name="schema"></a><span data-ttu-id="ee4d2-109">Şema</span><span class="sxs-lookup"><span data-stu-id="ee4d2-109">Schema</span></span>

<span data-ttu-id="ee4d2-110">Şema basittir: standart XML üst bilgisinin ardından `<packages>` her başvuru için bir veya daha fazla öğe içeren tek bir düğümdür `<package>` .</span><span class="sxs-lookup"><span data-stu-id="ee4d2-110">The schema is simple: following the standard XML header is a single `<packages>` node that contains one or more `<package>` elements, one for each reference.</span></span> <span data-ttu-id="ee4d2-111">Her `<package>` öğe aşağıdaki özniteliklere sahip olabilir:</span><span class="sxs-lookup"><span data-stu-id="ee4d2-111">Each `<package>` element can have the following attributes:</span></span>

| <span data-ttu-id="ee4d2-112">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="ee4d2-112">Attribute</span></span> | <span data-ttu-id="ee4d2-113">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ee4d2-113">Required</span></span> | <span data-ttu-id="ee4d2-114">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee4d2-114">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ee4d2-115">kimlik</span><span class="sxs-lookup"><span data-stu-id="ee4d2-115">id</span></span> | <span data-ttu-id="ee4d2-116">Yes</span><span class="sxs-lookup"><span data-stu-id="ee4d2-116">Yes</span></span> | <span data-ttu-id="ee4d2-117">Paketin tanımlayıcısı, örneğin Newtonsoft.json veya Microsoft. AspNet. Mvc.</span><span class="sxs-lookup"><span data-stu-id="ee4d2-117">The identifier of the package, such as Newtonsoft.json or Microsoft.AspNet.Mvc.</span></span> | 
| <span data-ttu-id="ee4d2-118">sürüm</span><span class="sxs-lookup"><span data-stu-id="ee4d2-118">version</span></span> | <span data-ttu-id="ee4d2-119">Yes</span><span class="sxs-lookup"><span data-stu-id="ee4d2-119">Yes</span></span> | <span data-ttu-id="ee4d2-120">Yüklenecek paketin tam sürümü (örneğin, 3.1.1 veya 4.2.5.11-Beta).</span><span class="sxs-lookup"><span data-stu-id="ee4d2-120">The exact version of the package to install, such as 3.1.1 or 4.2.5.11-beta.</span></span> <span data-ttu-id="ee4d2-121">Sürüm dizesinin en az üç numarası olmalıdır; Dördüncü, ön sürüm ön eki olduğu gibi isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="ee4d2-121">A version string must have at least three numbers; a fourth is optional, as is a pre-release suffix.</span></span> <span data-ttu-id="ee4d2-122">Aralıklara izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="ee4d2-122">Ranges are not allowed.</span></span> | 
| <span data-ttu-id="ee4d2-123">targetFramework</span><span class="sxs-lookup"><span data-stu-id="ee4d2-123">targetFramework</span></span> | <span data-ttu-id="ee4d2-124">Hayır</span><span class="sxs-lookup"><span data-stu-id="ee4d2-124">No</span></span> | <span data-ttu-id="ee4d2-125">Paket yüklenirken uygulanacak [hedef çerçeve bilinen adı (tfd)](target-frameworks.md) .</span><span class="sxs-lookup"><span data-stu-id="ee4d2-125">The [target framework moniker (TFM)](target-frameworks.md) to apply when installing the package.</span></span> <span data-ttu-id="ee4d2-126">Bu, başlangıçta bir paket yüklendiğinde projenin hedefine ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="ee4d2-126">This is initially set to the project's target when a package is installed.</span></span> <span data-ttu-id="ee4d2-127">Sonuç olarak, farklı `<package>` öğelerin farklı TFMs 'leri olabilir.</span><span class="sxs-lookup"><span data-stu-id="ee4d2-127">As a result, different `<package>` elements can have different TFMs.</span></span> <span data-ttu-id="ee4d2-128">Örneğin, .NET 4.5.2 'i hedefleyen bir proje oluşturursanız, bu noktada yüklenen paketler, net452 ' nin TFı 'sini kullanır.</span><span class="sxs-lookup"><span data-stu-id="ee4d2-128">For example, if you create a project targeting .NET 4.5.2, packages installed at that point will use the TFM of net452.</span></span> <span data-ttu-id="ee4d2-129">Projeyi daha sonra .NET 4,6 ' e yeniden hedeflemeniz ve daha fazla paket eklerseniz, bunlar net46 tfd kullanır.</span><span class="sxs-lookup"><span data-stu-id="ee4d2-129">If you ;later retarget the project to .NET 4.6 and add more packages, those will use TFM of net46.</span></span> <span data-ttu-id="ee4d2-130">Projenin hedefi ve öznitelikleri arasında bir uyumsuzluk `targetFramework` uyarı oluşturur ve bu durumda etkilenen paketleri yeniden yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee4d2-130">A mismatch between the project's target and `targetFramework` attributes will generate warnings, in which case you can reinstall the affected packages.</span></span> | 
| <span data-ttu-id="ee4d2-131">allowedVersions</span><span class="sxs-lookup"><span data-stu-id="ee4d2-131">allowedVersions</span></span> | <span data-ttu-id="ee4d2-132">Hayır</span><span class="sxs-lookup"><span data-stu-id="ee4d2-132">No</span></span> | <span data-ttu-id="ee4d2-133">Bu paket için, paket güncelleştirmesi sırasında uygulanan bir izin verilen sürüm aralığı (bkz. [yükseltme sürümlerini kısıtlama](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span><span class="sxs-lookup"><span data-stu-id="ee4d2-133">A range of allowed versions for this package applied during package update (see [Constraining upgrade versions](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="ee4d2-134">Yükleme veya geri yükleme işlemi sırasında hangi paketin *yükleneceğini etkilemez.*</span><span class="sxs-lookup"><span data-stu-id="ee4d2-134">It does *not* affect what package is installed during an install or restore operation.</span></span> <span data-ttu-id="ee4d2-135">Sözdizimi için [paket sürümü oluşturma](../concepts/package-versioning.md#version-ranges) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="ee4d2-135">See [Package versioning](../concepts/package-versioning.md#version-ranges) for syntax.</span></span> <span data-ttu-id="ee4d2-136">PackageManager UI, izin verilen Aralık dışındaki tüm sürümleri de devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="ee4d2-136">The PackageManager UI also disables all versions outside the allowed range.</span></span> | 
| <span data-ttu-id="ee4d2-137">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="ee4d2-137">developmentDependency</span></span> | <span data-ttu-id="ee4d2-138">Hayır</span><span class="sxs-lookup"><span data-stu-id="ee4d2-138">No</span></span> | <span data-ttu-id="ee4d2-139">Kullanan projenin kendisi bir NuGet paketi oluşturursa, bunu bir bağımlılık için olarak ayarlamak, bu `true` paketin, tüketen paket oluşturulduğunda eklenmesini engeller.</span><span class="sxs-lookup"><span data-stu-id="ee4d2-139">If the consuming project itself creates a NuGet package, setting this to `true` for a dependency prevents that package from being included when the consuming package is created.</span></span> <span data-ttu-id="ee4d2-140">Varsayılan değer: `false`.</span><span class="sxs-lookup"><span data-stu-id="ee4d2-140">The default is `false`.</span></span> | 

## <a name="examples"></a><span data-ttu-id="ee4d2-141">Örnekler</span><span class="sxs-lookup"><span data-stu-id="ee4d2-141">Examples</span></span>

<span data-ttu-id="ee4d2-142">Aşağıdaki `packages.config` iki bağımlılığı ifade eder:</span><span class="sxs-lookup"><span data-stu-id="ee4d2-142">The following `packages.config` refers to two dependencies:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

<span data-ttu-id="ee4d2-143">Aşağıdakiler `packages.config` dokuz pakete başvurur, ancak `Microsoft.Net.Compilers` öznitelik nedeniyle tüketen paket oluşturulurken dahil edilmez `developmentDependency` .</span><span class="sxs-lookup"><span data-stu-id="ee4d2-143">The following `packages.config` refers to nine packages, but `Microsoft.Net.Compilers` will not be included when building the consuming package because of the `developmentDependency` attribute.</span></span> <span data-ttu-id="ee4d2-144">Ayrıca Newtonsoft.Jsbaşvurusu, güncelleştirmeleri yalnızca 8. x ve 9. x sürümleri ile sınırlar.</span><span class="sxs-lookup"><span data-stu-id="ee4d2-144">The reference to Newtonsoft.Json also restricts updates to 8.x and 9.x versions only.</span></span>

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
