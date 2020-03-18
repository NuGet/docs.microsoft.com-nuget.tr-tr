---
title: NuGet paket sürümü başvurusu
description: Bir NuGet paketinin bağımlı olduğu diğer paketler için sürüm numaralarını ve aralıklarını belirtmeyle ilgili tam ayrıntılar ve bağımlılıkların yüklenme şekli.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 912c0d015e2f499bc7386483bc6c35ecd765d3d4
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428837"
---
# <a name="package-versioning"></a><span data-ttu-id="d2755-103">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="d2755-103">Package versioning</span></span>

<span data-ttu-id="d2755-104">Belirli bir paket her zaman kendi paket tanımlayıcısını ve tam sürüm numarasını kullanmaya başvurulur.</span><span class="sxs-lookup"><span data-stu-id="d2755-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="d2755-105">Örneğin, nuget.org üzerindeki [Entity Framework](https://www.nuget.org/packages/EntityFramework/) , sürüm *4.1.10311* ' den sürüm *6.1.3* (en son kararlı sürüm) ve *6.2.0-Beta1*gibi çeşitli yayın öncesi sürümler arasında değişen birkaç düzine özel pakete sahiptir.</span><span class="sxs-lookup"><span data-stu-id="d2755-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="d2755-106">Bir paket oluştururken, isteğe bağlı bir yayın öncesi metin sonekine sahip belirli bir sürüm numarası atarsınız.</span><span class="sxs-lookup"><span data-stu-id="d2755-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="d2755-107">Paketleri kullanırken, diğer yandan, tam sürüm numarasını veya bir dizi kabul edilebilir sürümü belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d2755-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="d2755-108">Bu konuda:</span><span class="sxs-lookup"><span data-stu-id="d2755-108">In this topic:</span></span>

- <span data-ttu-id="d2755-109">Yayın öncesi son eklerini içeren [Sürüm temelleri](#version-basics) .</span><span class="sxs-lookup"><span data-stu-id="d2755-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="d2755-110">Sürüm aralıkları</span><span class="sxs-lookup"><span data-stu-id="d2755-110">Version ranges</span></span>](#version-ranges)
- [<span data-ttu-id="d2755-111">Normalleştirilmiş sürüm numaraları</span><span class="sxs-lookup"><span data-stu-id="d2755-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="d2755-112">Sürüm temelleri</span><span class="sxs-lookup"><span data-stu-id="d2755-112">Version basics</span></span>

<span data-ttu-id="d2755-113">Belirli bir sürüm numarası, *ana. ikincil. Patch [-suffix]* biçiminde olduğundan, bileşenler aşağıdaki anlamlara sahiptir:</span><span class="sxs-lookup"><span data-stu-id="d2755-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="d2755-114">*Birincil*: son değişiklikler</span><span class="sxs-lookup"><span data-stu-id="d2755-114">*Major*: Breaking changes</span></span>
- <span data-ttu-id="d2755-115">*İkincil*: yeni özellikler, ancak geriye dönük olarak uyumlu</span><span class="sxs-lookup"><span data-stu-id="d2755-115">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="d2755-116">*Düzeltme Eki*: yalnızca geriye dönük uyumlu hata düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="d2755-116">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="d2755-117">*-Soneki* (isteğe bağlı): ön sürüm sürümünü belirten bir dize ( [anlamsal sürüm oluşturma veya semver 1,0 kuralını](https://semver.org/spec/v1.0.0.html)izleyerek).</span><span class="sxs-lookup"><span data-stu-id="d2755-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](https://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="d2755-118">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="d2755-118">**Examples:**</span></span>

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> <span data-ttu-id="d2755-119">nuget.org, tam sürüm numarası bulunmayan tüm paket karşıya yüklemeyi reddeder.</span><span class="sxs-lookup"><span data-stu-id="d2755-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="d2755-120">Sürüm, paketi oluşturmak için kullanılan `.nuspec` veya proje dosyasında belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="d2755-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="d2755-121">Yayın öncesi sürümler</span><span class="sxs-lookup"><span data-stu-id="d2755-121">Pre-release versions</span></span>

<span data-ttu-id="d2755-122">Teknik oluşturucular, yayın öncesi sürümü göstermek için herhangi bir dizeyi sonek olarak kullanabilir, böylece NuGet bu sürümü ön sürüm olarak değerlendirir ve başka yorum yapmaz.</span><span class="sxs-lookup"><span data-stu-id="d2755-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="d2755-123">Diğer bir deyişle, NuGet herhangi bir kullanıcı arabiriminin dahil olduğu tüm sürüm dizesini, son ekin anlamı olan tüketiciye herhangi bir yorum bırakarak görüntüler.</span><span class="sxs-lookup"><span data-stu-id="d2755-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="d2755-124">Yani, paket geliştiricileri genellikle tanınan adlandırma kurallarını izler:</span><span class="sxs-lookup"><span data-stu-id="d2755-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="d2755-125">`-alpha`: genellikle süren iş ve deneme için kullanılan alfa sürümü.</span><span class="sxs-lookup"><span data-stu-id="d2755-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="d2755-126">`-beta`: beta sürümü, genellikle bir sonraki planlı yayın için bir özelliktir, ancak bilinen hatalar içerebilir.</span><span class="sxs-lookup"><span data-stu-id="d2755-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="d2755-127">`-rc`: yayın adayı, genellikle önemli hatalar oluşmadığı takdirde son derece nihai (kararlı) bir sürümdür.</span><span class="sxs-lookup"><span data-stu-id="d2755-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="d2755-128">NuGet 4.3.0 +, *1.0.1-Build. 23*' te olduğu gibi nokta gösterimi ile yayın öncesi numaralarını destekleyen [semver 2.0.0](https://semver.org/spec/v2.0.0.html)'i destekler.</span><span class="sxs-lookup"><span data-stu-id="d2755-128">NuGet 4.3.0+ supports [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="d2755-129">Nokta gösterimi 4.3.0 öncesi NuGet sürümleriyle desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="d2755-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="d2755-130">*1.0.1-build23*gibi bir biçim kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d2755-130">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="d2755-131">Paket başvuruları ve birden çok paket sürümü yalnızca sonek tarafından farklılık gösterdiği zaman, NuGet önce sonek olmadan bir sürüm seçer, ardından ön sürüm sürümüne ters alfabetik sırada öncelik uygular.</span><span class="sxs-lookup"><span data-stu-id="d2755-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="d2755-132">Örneğin, aşağıdaki sürümler gösterilen tam sırada seçilebilir:</span><span class="sxs-lookup"><span data-stu-id="d2755-132">For example, the following versions would be chosen in the exact order shown:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a><span data-ttu-id="d2755-133">Anlamsal sürüm oluşturma 2.0.0</span><span class="sxs-lookup"><span data-stu-id="d2755-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="d2755-134">NuGet 4.3.0 + ve Visual Studio 2017 sürüm 15.3 + ile NuGet, [semantik sürümü oluşturma 2.0.0](https://semver.org/spec/v2.0.0.html)'yi destekler.</span><span class="sxs-lookup"><span data-stu-id="d2755-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="d2755-135">SemVer v 2.0.0 'in belirli semantiklerinden bazıları eski istemcilerde desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="d2755-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="d2755-136">NuGet, aşağıdaki deyimlerden herhangi biri geçerliyse, bir paket sürümünü SemVer v 2.0.0 'e özgü olarak kabul eder:</span><span class="sxs-lookup"><span data-stu-id="d2755-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="d2755-137">Yayın öncesi etiketi noktayla ayrılmıştır, örneğin, *1.0.0-Alpha. 1*</span><span class="sxs-lookup"><span data-stu-id="d2755-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="d2755-138">Sürümde derleme meta verileri vardır, örneğin, *1.0.0 + githash*</span><span class="sxs-lookup"><span data-stu-id="d2755-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="d2755-139">Nuget.org için bir paket, aşağıdaki deyimlerden herhangi biri doğruysa bir SemVer v 2.0.0 paketi olarak tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="d2755-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="d2755-140">Paketin kendi sürümü, yukarıda tanımlanan semver v 2.0.0 uyumludur ancak SemVer v 1.0.0 uyumlu değildir.</span><span class="sxs-lookup"><span data-stu-id="d2755-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="d2755-141">Paketin bağımlılık sürümü aralıklarının herhangi birinin, yukarıda tanımlanan semver v 2.0.0 uyumlu ancak SemVer v 1.0.0 uyumlu olmayan en düşük veya en yüksek sürümü vardır; Örneğin, *[1.0.0-Alpha. 1,)* .</span><span class="sxs-lookup"><span data-stu-id="d2755-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="d2755-142">Nuget.org 'e özel bir SemVer v 2.0.0 paketi yüklerseniz, paket eski istemcilere görünmez ve yalnızca aşağıdaki NuGet istemcilerinin kullanımına açık olur:</span><span class="sxs-lookup"><span data-stu-id="d2755-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="d2755-143">NuGet 4.3.0 +</span><span class="sxs-lookup"><span data-stu-id="d2755-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="d2755-144">Visual Studio 2017 sürüm 15.3 +</span><span class="sxs-lookup"><span data-stu-id="d2755-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="d2755-145">[NUGET VSIX v 3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix) Ile Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="d2755-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="d2755-146">dotnet</span><span class="sxs-lookup"><span data-stu-id="d2755-146">dotnet</span></span>
  - <span data-ttu-id="d2755-147">dotnetcore. exe (.NET SDK 2.0.0 +)</span><span class="sxs-lookup"><span data-stu-id="d2755-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="d2755-148">Üçüncü taraf istemcileri:</span><span class="sxs-lookup"><span data-stu-id="d2755-148">Third-party clients:</span></span>

- <span data-ttu-id="d2755-149">JetBrains Rider</span><span class="sxs-lookup"><span data-stu-id="d2755-149">JetBrains Rider</span></span>
- <span data-ttu-id="d2755-150">Paket sürüm 5.0 +</span><span class="sxs-lookup"><span data-stu-id="d2755-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges"></a><span data-ttu-id="d2755-151">Sürüm aralıkları</span><span class="sxs-lookup"><span data-stu-id="d2755-151">Version ranges</span></span>

<span data-ttu-id="d2755-152">NuGet, paket bağımlılıklarına başvururken, sürüm aralıklarını belirtmek için Aralık gösterimini kullanmayı destekler, şöyle özetlenir:</span><span class="sxs-lookup"><span data-stu-id="d2755-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="d2755-153">İmle</span><span class="sxs-lookup"><span data-stu-id="d2755-153">Notation</span></span> | <span data-ttu-id="d2755-154">Uygulanan kural</span><span class="sxs-lookup"><span data-stu-id="d2755-154">Applied rule</span></span> | <span data-ttu-id="d2755-155">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d2755-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="d2755-156">1.0</span><span class="sxs-lookup"><span data-stu-id="d2755-156">1.0</span></span> | <span data-ttu-id="d2755-157">x ≥ 1,0</span><span class="sxs-lookup"><span data-stu-id="d2755-157">x ≥ 1.0</span></span> | <span data-ttu-id="d2755-158">En düşük sürüm, dahil</span><span class="sxs-lookup"><span data-stu-id="d2755-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="d2755-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="d2755-159">(1.0,)</span></span> | <span data-ttu-id="d2755-160">x > 1,0</span><span class="sxs-lookup"><span data-stu-id="d2755-160">x > 1.0</span></span> | <span data-ttu-id="d2755-161">En düşük sürüm, özel</span><span class="sxs-lookup"><span data-stu-id="d2755-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="d2755-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="d2755-162">[1.0]</span></span> | <span data-ttu-id="d2755-163">x = = 1,0</span><span class="sxs-lookup"><span data-stu-id="d2755-163">x == 1.0</span></span> | <span data-ttu-id="d2755-164">Tam sürüm eşleşmesi</span><span class="sxs-lookup"><span data-stu-id="d2755-164">Exact version match</span></span> |
| <span data-ttu-id="d2755-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="d2755-165">(,1.0]</span></span> | <span data-ttu-id="d2755-166">x ≤ 1,0</span><span class="sxs-lookup"><span data-stu-id="d2755-166">x ≤ 1.0</span></span> | <span data-ttu-id="d2755-167">En yüksek sürüm, dahil</span><span class="sxs-lookup"><span data-stu-id="d2755-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="d2755-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="d2755-168">(,1.0)</span></span> | <span data-ttu-id="d2755-169">x < 1,0</span><span class="sxs-lookup"><span data-stu-id="d2755-169">x < 1.0</span></span> | <span data-ttu-id="d2755-170">En yüksek sürüm, özel</span><span class="sxs-lookup"><span data-stu-id="d2755-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="d2755-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="d2755-171">[1.0,2.0]</span></span> | <span data-ttu-id="d2755-172">1,0 ≤ x ≤ 2,0</span><span class="sxs-lookup"><span data-stu-id="d2755-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="d2755-173">Tam Aralık, dahil</span><span class="sxs-lookup"><span data-stu-id="d2755-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="d2755-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="d2755-174">(1.0,2.0)</span></span> | <span data-ttu-id="d2755-175">1,0 < x < 2,0</span><span class="sxs-lookup"><span data-stu-id="d2755-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="d2755-176">Tam Aralık, özel</span><span class="sxs-lookup"><span data-stu-id="d2755-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="d2755-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="d2755-177">[1.0,2.0)</span></span> | <span data-ttu-id="d2755-178">1,0 ≤ x < 2,0</span><span class="sxs-lookup"><span data-stu-id="d2755-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="d2755-179">Karma kapsamlı en düşük ve en yüksek sürüm</span><span class="sxs-lookup"><span data-stu-id="d2755-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="d2755-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="d2755-180">(1.0)</span></span>    | <span data-ttu-id="d2755-181">geçersiz</span><span class="sxs-lookup"><span data-stu-id="d2755-181">invalid</span></span> | <span data-ttu-id="d2755-182">geçersiz</span><span class="sxs-lookup"><span data-stu-id="d2755-182">invalid</span></span> |

<span data-ttu-id="d2755-183">Bu, PackageReference biçimini kullanırken, büyük, küçük, düzeltme eki uygulama ve sayının yayın öncesi sonek bölümleri için \*kayan bir gösterim kullanımını da destekler.</span><span class="sxs-lookup"><span data-stu-id="d2755-183">When using the PackageReference format, NuGet also supports using a floating notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="d2755-184">Kayan sürümler `packages.config` biçimiyle desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="d2755-184">Floating versions are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="d2755-185">PackageReference içindeki sürüm aralıkları yayın öncesi sürümleri içerir.</span><span class="sxs-lookup"><span data-stu-id="d2755-185">Version ranges in PackageReference include pre-release versions.</span></span> <span data-ttu-id="d2755-186">Tasarım yaparak, kayan sürümler, kabul edilmediği takdirde ön sürüm sürümlerini çözmez.</span><span class="sxs-lookup"><span data-stu-id="d2755-186">By design, floating versions do not resolve prerelease versions unless opted into.</span></span> <span data-ttu-id="d2755-187">İlgili özellik isteğinin durumu için bkz. [sorun 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span><span class="sxs-lookup"><span data-stu-id="d2755-187">For the status of the related feature request, see [issue 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span></span>

### <a name="examples"></a><span data-ttu-id="d2755-188">Örnekler</span><span class="sxs-lookup"><span data-stu-id="d2755-188">Examples</span></span>

<span data-ttu-id="d2755-189">Proje dosyalarında, `packages.config` dosyalarında ve `.nuspec` dosyalarında paket bağımlılıkları için her zaman bir sürüm veya sürüm aralığı belirtin.</span><span class="sxs-lookup"><span data-stu-id="d2755-189">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="d2755-190">Sürüm veya sürüm aralığı olmadan, NuGet 2.8. x ve önceki sürümleri bir bağımlılığı çözümlerken kullanılabilir en son paket sürümünü seçer, ancak NuGet 3. x ve sonraki sürümler en düşük paket sürümünü seçer.</span><span class="sxs-lookup"><span data-stu-id="d2755-190">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="d2755-191">Bir sürüm veya sürüm aralığı belirtildiğinde bu belirsizlik önlenir.</span><span class="sxs-lookup"><span data-stu-id="d2755-191">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="d2755-192">Proje dosyalarındaki başvurular (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="d2755-192">References in project files (PackageReference)</span></span>

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

<span data-ttu-id="d2755-193">**`packages.config`başvurular:**</span><span class="sxs-lookup"><span data-stu-id="d2755-193">**References in `packages.config`:**</span></span>

<span data-ttu-id="d2755-194">`packages.config`, her bağımlılık, paketler geri yüklenirken kullanılan tam bir `version` özniteliğiyle listelenir.</span><span class="sxs-lookup"><span data-stu-id="d2755-194">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="d2755-195">`allowedVersions` özniteliği yalnızca paketin güncelleştirilemeyebilir sürümlerini kısıtlamak için güncelleştirme işlemleri sırasında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d2755-195">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

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

<span data-ttu-id="d2755-196">**`.nuspec` dosyalardaki başvurular**</span><span class="sxs-lookup"><span data-stu-id="d2755-196">**References in `.nuspec` files**</span></span>

<span data-ttu-id="d2755-197">Bir `<dependency>` öğesindeki `version` özniteliği, bağımlılık için kabul edilebilir olan Aralık sürümlerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="d2755-197">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

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

## <a name="normalized-version-numbers"></a><span data-ttu-id="d2755-198">Normalleştirilmiş sürüm numaraları</span><span class="sxs-lookup"><span data-stu-id="d2755-198">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="d2755-199">Bu, NuGet 3,4 ve üzeri için bir son değişiklik değildir.</span><span class="sxs-lookup"><span data-stu-id="d2755-199">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="d2755-200">Yükleme, yeniden yükleme veya geri yükleme işlemleri sırasında bir depodan paket edinirken, NuGet 3.4 + sürüm numaralarını aşağıdaki gibi davranır:</span><span class="sxs-lookup"><span data-stu-id="d2755-200">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="d2755-201">Önde gelen sıfırlar sürüm numaralarına kaldırılır:</span><span class="sxs-lookup"><span data-stu-id="d2755-201">Leading zeroes are removed from version numbers:</span></span>

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- <span data-ttu-id="d2755-202">Sürüm numarasının dördüncü bölümünde sıfır yok edilir</span><span class="sxs-lookup"><span data-stu-id="d2755-202">A zero in the fourth part of the version number will be omitted</span></span>

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

<span data-ttu-id="d2755-203">`pack` ve `restore` işlemleri mümkün olduğunda sürümleri normalleştirin.</span><span class="sxs-lookup"><span data-stu-id="d2755-203">`pack` and `restore` operations normalize versions whenever possible.</span></span> <span data-ttu-id="d2755-204">Zaten oluşturulan paketler için, bu normalleştirme, paketlerdeki sürüm numaralarını etkilemez; Bağımlılıklar çözümlenirken yalnızca NuGet 'in sürümleri nasıl eşleştiğini etkiler.</span><span class="sxs-lookup"><span data-stu-id="d2755-204">For packages already built, this normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="d2755-205">Ancak, NuGet paket depoları, paket sürümü çoğaltmasını engellemek için bu değerleri NuGet ile aynı şekilde ele almalıdır.</span><span class="sxs-lookup"><span data-stu-id="d2755-205">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="d2755-206">Bu nedenle, bir paketin *1,0* sürümünü içeren bir depo ayrıca ayrı ve farklı bir paket olarak sürüm *1.0.0* barındırmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="d2755-206">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
