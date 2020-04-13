---
title: NuGet Paketi Sürüm Başvurusu
description: NuGet paketinin bağlı olduğu diğer paketler için sürüm numaralarını ve aralıklarını belirtme ve bağımlılıkların nasıl yüklendiği yle ilgili tam ayrıntılar.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: c79976c2f4ded2fba3796fb847d3c90807d7b86c
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "80147454"
---
# <a name="package-versioning"></a><span data-ttu-id="5d3dd-103">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="5d3dd-103">Package versioning</span></span>

<span data-ttu-id="5d3dd-104">Belirli bir paket her zaman paket tanımlayıcısı ve tam sürüm numarası kullanılarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="5d3dd-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="5d3dd-105">Örneğin, nuget.org'daki [Entity Framework](https://www.nuget.org/packages/EntityFramework/) sürüm *4.1.10311'den* sürüm *6.1.3* 'e (en son kararlı sürüm) ve *6.2.0-beta1*gibi çeşitli ön sürüm sürümlerine kadar birkaç düzine özel paket mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="5d3dd-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="5d3dd-106">Bir paket oluştururken, isteğe bağlı bir ön sürüm metin soneki yle belirli bir sürüm numarası atarsınız.</span><span class="sxs-lookup"><span data-stu-id="5d3dd-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="5d3dd-107">Diğer taraftan, paketleri tüketirken, tam sürüm numarasını veya kabul edilebilir sürümler aralığını belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5d3dd-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="5d3dd-108">Bu konuda:</span><span class="sxs-lookup"><span data-stu-id="5d3dd-108">In this topic:</span></span>

- <span data-ttu-id="5d3dd-109">Ön sürüm sonekleri de dahil olmak üzere [sürüm temelleri.](#version-basics)</span><span class="sxs-lookup"><span data-stu-id="5d3dd-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="5d3dd-110">Sürüm aralıkları</span><span class="sxs-lookup"><span data-stu-id="5d3dd-110">Version ranges</span></span>](#version-ranges)
- [<span data-ttu-id="5d3dd-111">Normalleştirilmiş sürüm numaraları</span><span class="sxs-lookup"><span data-stu-id="5d3dd-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="5d3dd-112">Sürüm temelleri</span><span class="sxs-lookup"><span data-stu-id="5d3dd-112">Version basics</span></span>

<span data-ttu-id="5d3dd-113">Belirli bir sürüm numarası *Major.Minor.Patch[-Soneki]* şeklindedir ve bileşenlerin aşağıdaki anlamları vardır:</span><span class="sxs-lookup"><span data-stu-id="5d3dd-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="5d3dd-114">*Ana :* Son dakika değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="5d3dd-114">*Major*: Breaking changes</span></span>
- <span data-ttu-id="5d3dd-115">*Minor*: Yeni özellikler, ancak geriye dönük uyumlu</span><span class="sxs-lookup"><span data-stu-id="5d3dd-115">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="5d3dd-116">*Yama*: Geriye uyumlu hata düzeltmeleri yalnızca</span><span class="sxs-lookup"><span data-stu-id="5d3dd-116">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="5d3dd-117">*-Soneki* (isteğe bağlı): bir ön sürüm sürümünü gösteren bir dize takip tire [(Anlamsal Sürüm veya SemVer 1.0 kuralını](https://semver.org/spec/v1.0.0.html)takip eder).</span><span class="sxs-lookup"><span data-stu-id="5d3dd-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](https://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="5d3dd-118">**Örnekler:**</span><span class="sxs-lookup"><span data-stu-id="5d3dd-118">**Examples:**</span></span>

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> <span data-ttu-id="5d3dd-119">nuget.org, tam sürüm numarası bulunmayan paket yüklemeyi reddeder.</span><span class="sxs-lookup"><span data-stu-id="5d3dd-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="5d3dd-120">Sürüm, paketi oluşturmak `.nuspec` için kullanılan proje dosyasında belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="5d3dd-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="5d3dd-121">Ön sürüm sürümleri</span><span class="sxs-lookup"><span data-stu-id="5d3dd-121">Pre-release versions</span></span>

<span data-ttu-id="5d3dd-122">Teknik olarak konuşursak, paket oluşturucular, nuget ön sürüm gibi herhangi bir sürümü ele alır ve başka bir yorum yapmaması nedeniyle, sürüm öncesi sürümü belirtmek için herhangi bir dizeyi sonek olarak kullanabilirler.</span><span class="sxs-lookup"><span data-stu-id="5d3dd-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="5d3dd-123">Diğer bir deyişle, NuGet, sonekin anlamının yorumunu tüketiciye bırakarak, tam sürüm dizesini ne olursa olsun, ilgili olduğunda görüntüler.</span><span class="sxs-lookup"><span data-stu-id="5d3dd-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="5d3dd-124">Yani, paket geliştiriciler genellikle tanınan adlandırma kuralları izleyin dedi:</span><span class="sxs-lookup"><span data-stu-id="5d3dd-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="5d3dd-125">`-alpha`: Alfa salınımı, genellikle devam etmekte olan işler ve deneyler için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5d3dd-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="5d3dd-126">`-beta`: Beta sürümü, genellikle bir sonraki planlanan sürüm için tamamlanmış özellik, ancak bilinen hataları içerebilir.</span><span class="sxs-lookup"><span data-stu-id="5d3dd-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="5d3dd-127">`-rc`: Sürüm adayı, önemli hatalar ortaya çıkmadıkça genellikle nihai (kararlı) bir sürüm.</span><span class="sxs-lookup"><span data-stu-id="5d3dd-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="5d3dd-128">NuGet 4.3.0+ *1.0.1-build.23'te*olduğu gibi nokta gösterimi ile ön sürüm sayılarını destekleyen [SemVer 2.0.0'ı](https://semver.org/spec/v2.0.0.html)destekler.</span><span class="sxs-lookup"><span data-stu-id="5d3dd-128">NuGet 4.3.0+ supports [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="5d3dd-129">Nokta gösterimi 4.3.0'dan önce NuGet sürümleriyle desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="5d3dd-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="5d3dd-130">*1.0.1-build23*gibi bir form kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5d3dd-130">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="5d3dd-131">Paket başvurularını ve birden çok paket sürümünü yalnızca sonek ile farklı olarak çözerken, NuGet önce sonek olmayan bir sürüm seçer, ardından ön sürüm sürümlerine ters alfabetik sırayla öncelik uygular.</span><span class="sxs-lookup"><span data-stu-id="5d3dd-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="5d3dd-132">Örneğin, aşağıdaki sürümler gösterilen tam sırada seçilir:</span><span class="sxs-lookup"><span data-stu-id="5d3dd-132">For example, the following versions would be chosen in the exact order shown:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a><span data-ttu-id="5d3dd-133">Anlamsal Versiyon 2.0.0</span><span class="sxs-lookup"><span data-stu-id="5d3dd-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="5d3dd-134">NuGet 4.3.0+ ve Visual Studio 2017 sürüm 15.3+ ile [NuGet, Anlamsal Sürüm 2.0.0'ı](https://semver.org/spec/v2.0.0.html)destekler.</span><span class="sxs-lookup"><span data-stu-id="5d3dd-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="5d3dd-135">SemVer v2.0.0 bazı semantik eski istemcilerde desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="5d3dd-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="5d3dd-136">NuGet, aşağıdaki ifadelerden biri doğruysa, bir paket sürümünüSemVer v2.0.0'a özgü olarak kabul eder:</span><span class="sxs-lookup"><span data-stu-id="5d3dd-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="5d3dd-137">Ön sürüm etiketi nokta ayrılmış, örneğin, *1.0.0-alfa.1*</span><span class="sxs-lookup"><span data-stu-id="5d3dd-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="5d3dd-138">Sürüm, örneğin, *1.0.0+githash* yapı-meta verivardır</span><span class="sxs-lookup"><span data-stu-id="5d3dd-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="5d3dd-139">Nuget.org için, aşağıdaki ifadelerden biri doğruysa, bir paket SemVer v2.0.0 paketi olarak tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="5d3dd-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="5d3dd-140">Paketin kendi sürümü SemVer v2.0.0 uyumludur, ancak yukarıda tanımlandığı gibi SemVer v1.0.0 uyumlu değildir.</span><span class="sxs-lookup"><span data-stu-id="5d3dd-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="5d3dd-141">Paketin bağımlılık sürüm aralıklarından herhangi biri, semver v2.0.0 uyumlu olan minimum veya maksimum bir sürüme sahiptir, ancak yukarıda tanımlanan SemVer v1.0.0 uyumlu değildir; örneğin, *[1.0.0-alfa.1, )*.</span><span class="sxs-lookup"><span data-stu-id="5d3dd-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="5d3dd-142">nuget.org'a semver v2.0.0'a özel bir paket yüklerseniz, paket eski istemciler tarafından görünmez ve yalnızca aşağıdaki NuGet istemcileri tarafından kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="5d3dd-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="5d3dd-143">NuGet 4.3.0+</span><span class="sxs-lookup"><span data-stu-id="5d3dd-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="5d3dd-144">Visual Studio 2017 sürümü 15.3+</span><span class="sxs-lookup"><span data-stu-id="5d3dd-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="5d3dd-145">Visual Studio 2015 [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix) ile</span><span class="sxs-lookup"><span data-stu-id="5d3dd-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="5d3dd-146">dotnet</span><span class="sxs-lookup"><span data-stu-id="5d3dd-146">dotnet</span></span>
  - <span data-ttu-id="5d3dd-147">dotnetcore.exe (.NET SDK 2.0.0+)</span><span class="sxs-lookup"><span data-stu-id="5d3dd-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="5d3dd-148">Üçüncü taraf istemciler:</span><span class="sxs-lookup"><span data-stu-id="5d3dd-148">Third-party clients:</span></span>

- <span data-ttu-id="5d3dd-149">JetBrains Rider</span><span class="sxs-lookup"><span data-stu-id="5d3dd-149">JetBrains Rider</span></span>
- <span data-ttu-id="5d3dd-150">Paket sürüm 5.0+</span><span class="sxs-lookup"><span data-stu-id="5d3dd-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges"></a><span data-ttu-id="5d3dd-151">Sürüm aralıkları</span><span class="sxs-lookup"><span data-stu-id="5d3dd-151">Version ranges</span></span>

<span data-ttu-id="5d3dd-152">Paket bağımlılıklarına atıfta bulunulduğunda, NuGet aşağıdaki gibi özetlenen sürüm aralıklarını belirtmek için aralık gösterimini desteklemektedir:</span><span class="sxs-lookup"><span data-stu-id="5d3dd-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="5d3dd-153">Gösterim</span><span class="sxs-lookup"><span data-stu-id="5d3dd-153">Notation</span></span> | <span data-ttu-id="5d3dd-154">Uygulanan kural</span><span class="sxs-lookup"><span data-stu-id="5d3dd-154">Applied rule</span></span> | <span data-ttu-id="5d3dd-155">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5d3dd-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="5d3dd-156">1.0</span><span class="sxs-lookup"><span data-stu-id="5d3dd-156">1.0</span></span> | <span data-ttu-id="5d3dd-157">x ≥ 1.0</span><span class="sxs-lookup"><span data-stu-id="5d3dd-157">x ≥ 1.0</span></span> | <span data-ttu-id="5d3dd-158">Minimum sürüm, dahil</span><span class="sxs-lookup"><span data-stu-id="5d3dd-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="5d3dd-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="5d3dd-159">(1.0,)</span></span> | <span data-ttu-id="5d3dd-160">x > 1.0</span><span class="sxs-lookup"><span data-stu-id="5d3dd-160">x > 1.0</span></span> | <span data-ttu-id="5d3dd-161">Minimum sürüm, özel</span><span class="sxs-lookup"><span data-stu-id="5d3dd-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="5d3dd-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="5d3dd-162">[1.0]</span></span> | <span data-ttu-id="5d3dd-163">x == 1.0</span><span class="sxs-lookup"><span data-stu-id="5d3dd-163">x == 1.0</span></span> | <span data-ttu-id="5d3dd-164">Tam sürüm eşleşmesi</span><span class="sxs-lookup"><span data-stu-id="5d3dd-164">Exact version match</span></span> |
| <span data-ttu-id="5d3dd-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="5d3dd-165">(,1.0]</span></span> | <span data-ttu-id="5d3dd-166">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="5d3dd-166">x ≤ 1.0</span></span> | <span data-ttu-id="5d3dd-167">Maksimum sürüm, dahil</span><span class="sxs-lookup"><span data-stu-id="5d3dd-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="5d3dd-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="5d3dd-168">(,1.0)</span></span> | <span data-ttu-id="5d3dd-169">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="5d3dd-169">x < 1.0</span></span> | <span data-ttu-id="5d3dd-170">Maksimum sürüm, özel</span><span class="sxs-lookup"><span data-stu-id="5d3dd-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="5d3dd-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="5d3dd-171">[1.0,2.0]</span></span> | <span data-ttu-id="5d3dd-172">1.0 ≤ x ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="5d3dd-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="5d3dd-173">Tam aralık, dahil</span><span class="sxs-lookup"><span data-stu-id="5d3dd-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="5d3dd-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="5d3dd-174">(1.0,2.0)</span></span> | <span data-ttu-id="5d3dd-175">1.0 < x < 2.0</span><span class="sxs-lookup"><span data-stu-id="5d3dd-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="5d3dd-176">Tam aralık, özel</span><span class="sxs-lookup"><span data-stu-id="5d3dd-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="5d3dd-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="5d3dd-177">[1.0,2.0)</span></span> | <span data-ttu-id="5d3dd-178">1.0 ≤ x < 2.0</span><span class="sxs-lookup"><span data-stu-id="5d3dd-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="5d3dd-179">Karışık dahil minimum ve münhasır maksimum sürüm</span><span class="sxs-lookup"><span data-stu-id="5d3dd-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="5d3dd-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="5d3dd-180">(1.0)</span></span>    | <span data-ttu-id="5d3dd-181">geçersiz</span><span class="sxs-lookup"><span data-stu-id="5d3dd-181">invalid</span></span> | <span data-ttu-id="5d3dd-182">geçersiz</span><span class="sxs-lookup"><span data-stu-id="5d3dd-182">invalid</span></span> |

<span data-ttu-id="5d3dd-183">PackageReference biçimini kullanırken, NuGet, numaranın Büyük, \*Küçük, Yama ve ön sürüm sonek parçaları için kayan bir gösterim ihdası da destekler.</span><span class="sxs-lookup"><span data-stu-id="5d3dd-183">When using the PackageReference format, NuGet also supports using a floating notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="5d3dd-184">Kayan sürümler `packages.config` biçimiyle desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="5d3dd-184">Floating versions are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="5d3dd-185">PackageReference'daki sürüm aralıkları, ön sürüm sürümleri içerir.</span><span class="sxs-lookup"><span data-stu-id="5d3dd-185">Version ranges in PackageReference include pre-release versions.</span></span> <span data-ttu-id="5d3dd-186">Tasarım gereği, kayan sürümler tercih edilmedikçe ön sürüm sürümlerini çözmez.</span><span class="sxs-lookup"><span data-stu-id="5d3dd-186">By design, floating versions do not resolve prerelease versions unless opted into.</span></span> <span data-ttu-id="5d3dd-187">İlgili özellik isteğinin durumu için [6434 sorununa](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297)bakın.</span><span class="sxs-lookup"><span data-stu-id="5d3dd-187">For the status of the related feature request, see [issue 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span></span>

### <a name="examples"></a><span data-ttu-id="5d3dd-188">Örnekler</span><span class="sxs-lookup"><span data-stu-id="5d3dd-188">Examples</span></span>

<span data-ttu-id="5d3dd-189">Proje dosyalarındaki, `packages.config` dosyalardaki ve `.nuspec` dosyalardaki paket bağımlılıkları için her zaman bir sürüm veya sürüm aralığı belirtin.</span><span class="sxs-lookup"><span data-stu-id="5d3dd-189">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="5d3dd-190">Bir sürüm veya sürüm aralığı olmadan, NuGet 2.8.x ve daha önce bir bağımlılık çözerken en son kullanılabilir paket sürümünü seçer, NuGet 3.x ise ve daha sonra en düşük paket sürümünü seçer.</span><span class="sxs-lookup"><span data-stu-id="5d3dd-190">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="5d3dd-191">Sürüm veya sürüm aralığının belirtilmesi bu belirsizliği önler.</span><span class="sxs-lookup"><span data-stu-id="5d3dd-191">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="5d3dd-192">Proje dosyalarındaki başvurular (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="5d3dd-192">References in project files (PackageReference)</span></span>

```xml
<!-- Accepts any version 6.1 and above. -->
<PackageReference Include="ExamplePackage" Version="6.1" />

<!-- Accepts any 6.x.y version. -->
<PackageReference Include="ExamplePackage" Version="6.*" />
<PackageReference Include="ExamplePackage" Version="[6,7)" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<PackageReference Include="ExamplePackage" Version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<PackageReference Include="ExamplePackage" Version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<PackageReference Include="ExamplePackage" Version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

<span data-ttu-id="5d3dd-193">**Referanslar `packages.config`:**</span><span class="sxs-lookup"><span data-stu-id="5d3dd-193">**References in `packages.config`:**</span></span>

<span data-ttu-id="5d3dd-194">Her `packages.config`bağımlılık, paketleri geri verirken kullanılan tam `version` bir öznitelikile listelenir.</span><span class="sxs-lookup"><span data-stu-id="5d3dd-194">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="5d3dd-195">Öznitelik, `allowedVersions` yalnızca paketin güncelleştirilebileceği sürümleri kısıtlamak için güncelleştirme işlemleri sırasında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5d3dd-195">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

```xml
<!-- Install/restore version 6.1.0, accept any version 6.1.0 and above on update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="6.1.0" />

<!-- Install/restore version 6.1.0, and do not change during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6.1.0]" />

<!-- Install/restore version 6.1.0, accept any 6.x version during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6,7)" />

<!-- Install/restore version 4.1.4, accept any version above, but not including, 4.1.3.
     Could be used to guarantee a dependency with a specific bug fix. -->
<package id="ExamplePackage" version="4.1.4" allowedVersions="(4.1.3,)" />

<!-- Install/restore version 3.1.2, accept any version up below 5.x on update, which might be
     used to prevent pulling in a later version of a dependency that changed its interface.
     However, this form is not recommended because it can be difficult to determine the lowest version. -->
<package id="ExamplePackage" version="3.1.2" allowedVersions="(,5.0)" />

<!-- Install/restore version 1.1.4, accept any 1.x or 2.x version on update, but not
     0.x or 3.x and higher. -->
<package id="ExamplePackage" version="1.1.4" allowedVersions="[1,3)" />

<!-- Install/restore version 1.3.5, accepts 1.3.2 up to 1.4.x on update, but not 1.5 and higher. -->
<package id="ExamplePackage" version="1.3.5" allowedVersions="[1.3.2,1.5)" />
```

<span data-ttu-id="5d3dd-196">**Dosyalardaki `.nuspec` başvurular**</span><span class="sxs-lookup"><span data-stu-id="5d3dd-196">**References in `.nuspec` files**</span></span>

<span data-ttu-id="5d3dd-197">Bir `version` `<dependency>` öğedeki öznitelik, bağımlılık için kabul edilebilir aralık sürümlerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="5d3dd-197">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<dependency id="ExamplePackage" version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<dependency id="ExamplePackage" version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<dependency id="ExamplePackage" version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<dependency id="ExamplePackage" version="[1.3.2,1.5)" />
```

## <a name="normalized-version-numbers"></a><span data-ttu-id="5d3dd-198">Normalleştirilmiş sürüm numaraları</span><span class="sxs-lookup"><span data-stu-id="5d3dd-198">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="5d3dd-199">Bu NuGet 3.4 ve sonrası için bir kırılma değişikliktir.</span><span class="sxs-lookup"><span data-stu-id="5d3dd-199">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="5d3dd-200">Yükleme, yeniden yükleme veya geri yükleme işlemleri sırasında bir depodan paket alırken, NuGet 3.4+ sürüm numaralarını aşağıdaki gibi davranır:</span><span class="sxs-lookup"><span data-stu-id="5d3dd-200">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="5d3dd-201">Satır aralığı sıfırları sürüm numaralarından kaldırılır:</span><span class="sxs-lookup"><span data-stu-id="5d3dd-201">Leading zeroes are removed from version numbers:</span></span>

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- <span data-ttu-id="5d3dd-202">Sürüm numarasının dördüncü bölümünde ki sıfır atlanır</span><span class="sxs-lookup"><span data-stu-id="5d3dd-202">A zero in the fourth part of the version number will be omitted</span></span>

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1
        
- <span data-ttu-id="5d3dd-203">SemVer 2.0.0 yapı meta verileri kaldırılır</span><span class="sxs-lookup"><span data-stu-id="5d3dd-203">SemVer 2.0.0 build metadata is removed</span></span>

        1.0.7+r3456 is treated as 1.0.7

<span data-ttu-id="5d3dd-204">`pack`ve `restore` işlemler mümkün olduğunda sürümleri normalleştirir.</span><span class="sxs-lookup"><span data-stu-id="5d3dd-204">`pack` and `restore` operations normalize versions whenever possible.</span></span> <span data-ttu-id="5d3dd-205">Zaten oluşturulmuş paketler için bu normalleştirme, paketlerdeki sürüm numaralarını etkilemez; yalnızca NuGet'in bağımlılıkları çözerken sürümlerle nasıl eşleştiğini etkiler.</span><span class="sxs-lookup"><span data-stu-id="5d3dd-205">For packages already built, this normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="5d3dd-206">Ancak, NuGet paket depoları, paket sürümünün çoğaltılmasını önlemek için bu değerleri NuGet ile aynı şekilde ele almalıdır.</span><span class="sxs-lookup"><span data-stu-id="5d3dd-206">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="5d3dd-207">Bu nedenle, bir paketin sürüm *1.0'ını* içeren bir depo, sürüm *1.0.0'ı* ayrı ve farklı bir paket olarak barındırmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="5d3dd-207">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
