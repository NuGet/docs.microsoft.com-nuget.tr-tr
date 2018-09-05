---
title: NuGet paketi sürüm başvurusu
description: Sürüm numaraları ve diğer paketleri bağımlı bir NuGet paketi ve bağımlılıkları nasıl yüklendiğini aralıkları belirtme hakkında tam ayrıntılar.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: b980c1084fe8e31573053a4dcf38bbfa6146e6de
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549779"
---
# <a name="package-versioning"></a><span data-ttu-id="bb331-103">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="bb331-103">Package versioning</span></span>

<span data-ttu-id="bb331-104">Belirli bir paket her zaman paket tanımlayıcısını ve bir tam sürüm numarası kullanılarak olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="bb331-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="bb331-105">Örneğin, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) nuget.org adresinden birkaç düzine belirli paketleri sürümden değişen kullanılabilir olan *4.1.10311* sürüme *6.1.3* (en son kararlı sürüm) ve yayın öncesi sürümleri çeşitli *6.2.0-beta1*.</span><span class="sxs-lookup"><span data-stu-id="bb331-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="bb331-106">Bir paket oluştururken, bir isteğe bağlı yayın öncesi metni soneki ile belirli bir sürüm numarası atayın.</span><span class="sxs-lookup"><span data-stu-id="bb331-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="bb331-107">Öte yandan, paket tüketildiğinde, bir tam sürüm numarası veya kabul edilebilir bir sürüm aralığı belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb331-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="bb331-108">Bu konuda:</span><span class="sxs-lookup"><span data-stu-id="bb331-108">In this topic:</span></span>

- <span data-ttu-id="bb331-109">[Sürüm Temelleri](#version-basics) yayın öncesi son ekleri dahil olmak üzere.</span><span class="sxs-lookup"><span data-stu-id="bb331-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="bb331-110">Sürüm aralıklarını ve joker karakterler</span><span class="sxs-lookup"><span data-stu-id="bb331-110">Version ranges and wildcards</span></span>](#version-ranges-and-wildcards)
- [<span data-ttu-id="bb331-111">Normalleştirilmiş sürüm numaraları</span><span class="sxs-lookup"><span data-stu-id="bb331-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="bb331-112">Sürüm temelleri</span><span class="sxs-lookup"><span data-stu-id="bb331-112">Version basics</span></span>

<span data-ttu-id="bb331-113">Belirli bir sürüm numarasını biçimindedir *ana.İkincil.yama [-soneki]*, aşağıdaki anlamlara sahip olduğu bileşenler:</span><span class="sxs-lookup"><span data-stu-id="bb331-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="bb331-114">*Ana*: bozucu değişiklikler</span><span class="sxs-lookup"><span data-stu-id="bb331-114">*Major*: Breaking changes</span></span>
- <span data-ttu-id="bb331-115">*Küçük*: yeni özellikler, ancak geriye dönük uyumluluk</span><span class="sxs-lookup"><span data-stu-id="bb331-115">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="bb331-116">*Düzeltme Eki*: yalnızca geriye dönük olarak uyumlu hata düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="bb331-116">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="bb331-117">*-Soneki* (isteğe bağlı): bir tire yayın öncesi bir sürümü belirten bir dize tarafından izlenen (aşağıdaki [Semantic Versioning veya SemVer 1.0 kuralı](http://semver.org/spec/v1.0.0.html)).</span><span class="sxs-lookup"><span data-stu-id="bb331-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](http://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="bb331-118">**Örnekler:**</span><span class="sxs-lookup"><span data-stu-id="bb331-118">**Examples:**</span></span>

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> <span data-ttu-id="bb331-119">nuget.org bir tam sürüm numarası eksik paketin karşıya yüklenmesi reddeder.</span><span class="sxs-lookup"><span data-stu-id="bb331-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="bb331-120">Sürüm belirtilmelidir `.nuspec` ya da proje dosyası paketi oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bb331-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="bb331-121">Yayın öncesi sürümleri</span><span class="sxs-lookup"><span data-stu-id="bb331-121">Pre-release versions</span></span>

<span data-ttu-id="bb331-122">Teknik terimlerle açıklamak gerekirse, paket creators herhangi bir dize sonek olarak NuGet gibi bir sürüm yayın öncesi değerlendirir ve diğer bir yorumu yayın öncesi bir sürümü belirtmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb331-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="bb331-123">Diğer bir deyişle, tam sürüm ne olursa olsun kullanıcı Arabiriminde dize NuGet görüntüler dahil, tüketiciye soneki'nın anlamı herhangi bir yorumu çıkılıyor.</span><span class="sxs-lookup"><span data-stu-id="bb331-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="bb331-124">Bu, paket geliştiriciler genellikle tanınan adlandırma kurallarına uymuyor olduğu söylenebilir:</span><span class="sxs-lookup"><span data-stu-id="bb331-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="bb331-125">`-alpha`: Yayın alfa, genellikle iş ilerleme ve deneme için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bb331-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="bb331-126">`-beta`: Beta sürümü, genellikle bir özellik için bir sonraki tam sürüm planlı, ancak bilinen hataları içerebilir.</span><span class="sxs-lookup"><span data-stu-id="bb331-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="bb331-127">`-rc`: Genellikle büyük olasılıkla son sürüm Sürüm Adayı (stable) sürece önemli hatalar ortaya çıkmaya başladı.</span><span class="sxs-lookup"><span data-stu-id="bb331-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="bb331-128">NuGet 4.3.0+ destekler [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), olarak nokta gösterimi, yayın öncesi sürüm numaralarıyla destekleyen *1.0.1-build.23*.</span><span class="sxs-lookup"><span data-stu-id="bb331-128">NuGet 4.3.0+ supports [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="bb331-129">Nokta gösterimi 4.3.0 önce NuGet sürümü ile desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="bb331-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="bb331-130">Bir form gibi kullanabileceğiniz *1.0.1-build23*.</span><span class="sxs-lookup"><span data-stu-id="bb331-130">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="bb331-131">Paket başvuruları ve birden çok paket sürümü yalnızca soneki farklılık çözülürken NuGet sürümü bir soneki olmayan ilk seçer ve ardından yayın öncesi sürümler ters alfabetik düzende öncelik geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="bb331-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="bb331-132">Örneğin, aşağıdaki sürümleri gösterilen sırada seçilir:</span><span class="sxs-lookup"><span data-stu-id="bb331-132">For example, the following versions would be chosen in the exact order shown:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a><span data-ttu-id="bb331-133">Semantic Versioning 2.0.0</span><span class="sxs-lookup"><span data-stu-id="bb331-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="bb331-134">NuGet 4.3.0+ ve Visual Studio 2017 sürüm 15.3 + ile NuGet destekler [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).</span><span class="sxs-lookup"><span data-stu-id="bb331-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="bb331-135">Belirli bir SemVer v2.0.0 semantikleri, eski istemcilere desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="bb331-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="bb331-136">NuGet Paket sürümü aşağıdaki deyimleri true ise SemVer v2.0.0 belirli olmasını göz önünde bulundurur:</span><span class="sxs-lookup"><span data-stu-id="bb331-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="bb331-137">Yayın öncesi etiketi, örneğin, noktayla ayrılmış *1.0.0-alpha.1*</span><span class="sxs-lookup"><span data-stu-id="bb331-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="bb331-138">Derleme meta veri, örneğin, sürüme sahip *1.0.0+githash*</span><span class="sxs-lookup"><span data-stu-id="bb331-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="bb331-139">Nuget.org için aşağıdaki ifadeler doğru ise bir paket bir SemVer v2.0.0 paketi olarak tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="bb331-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="bb331-140">Paketin kendi SemVer v2.0.0 uyumlu ancak değil SemVer v1.0.0 uyumlu, yukarıda tanımlanan sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="bb331-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="bb331-141">Paket bağımlılık sürüm aralıklardan herhangi biriyle uyumlu SemVer v2.0.0 ancak değil SemVer v1.0.0 uyumlu, yukarıda tanımlanan bir minimum veya maksimum sürümüne sahip; Örneğin, *[1.0.0-alpha.1,)*.</span><span class="sxs-lookup"><span data-stu-id="bb331-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="bb331-142">Nuget.org için bir SemVer v2.0.0 özgü paketini karşıya yükleyin, paketin eski istemcilere görünmez ve yalnızca aşağıdaki NuGet istemcileri için kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="bb331-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="bb331-143">NuGet 4.3.0+</span><span class="sxs-lookup"><span data-stu-id="bb331-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="bb331-144">Visual Studio 2017 sürüm 15.3 +</span><span class="sxs-lookup"><span data-stu-id="bb331-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="bb331-145">Visual Studio 2015 ile [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="bb331-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="bb331-146">DotNet</span><span class="sxs-lookup"><span data-stu-id="bb331-146">dotnet</span></span>
  - <span data-ttu-id="bb331-147">dotnetcore.exe (.NET SDK'sı 2.0.0+)</span><span class="sxs-lookup"><span data-stu-id="bb331-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="bb331-148">Üçüncü taraf istemcileri:</span><span class="sxs-lookup"><span data-stu-id="bb331-148">Third-party clients:</span></span>

- <span data-ttu-id="bb331-149">JetBrains Rider</span><span class="sxs-lookup"><span data-stu-id="bb331-149">JetBrains Rider</span></span>
- <span data-ttu-id="bb331-150">Paket sürüm 5.0 +</span><span class="sxs-lookup"><span data-stu-id="bb331-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a><span data-ttu-id="bb331-151">Sürüm aralıklarını ve joker karakterler</span><span class="sxs-lookup"><span data-stu-id="bb331-151">Version ranges and wildcards</span></span>

<span data-ttu-id="bb331-152">Paket bağımlılıklarını söz konusu olduğunda NuGet sürüm aralıklarını, aşağıdaki şekilde özetlenen belirtmek için aralığı gösterimi kullanılarak destekler:</span><span class="sxs-lookup"><span data-stu-id="bb331-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="bb331-153">Gösterim</span><span class="sxs-lookup"><span data-stu-id="bb331-153">Notation</span></span> | <span data-ttu-id="bb331-154">Uygulanan kural</span><span class="sxs-lookup"><span data-stu-id="bb331-154">Applied rule</span></span> | <span data-ttu-id="bb331-155">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bb331-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="bb331-156">1.0</span><span class="sxs-lookup"><span data-stu-id="bb331-156">1.0</span></span> | <span data-ttu-id="bb331-157">x ≥ 1.0</span><span class="sxs-lookup"><span data-stu-id="bb331-157">x ≥ 1.0</span></span> | <span data-ttu-id="bb331-158">En düşük sürüm, kapsamlı</span><span class="sxs-lookup"><span data-stu-id="bb331-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="bb331-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="bb331-159">(1.0,)</span></span> | <span data-ttu-id="bb331-160">x > 1.0</span><span class="sxs-lookup"><span data-stu-id="bb331-160">x > 1.0</span></span> | <span data-ttu-id="bb331-161">En düşük sürümü, özel</span><span class="sxs-lookup"><span data-stu-id="bb331-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="bb331-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="bb331-162">[1.0]</span></span> | <span data-ttu-id="bb331-163">x 1.0 ==</span><span class="sxs-lookup"><span data-stu-id="bb331-163">x == 1.0</span></span> | <span data-ttu-id="bb331-164">Tam sürümü eşleşmiyor</span><span class="sxs-lookup"><span data-stu-id="bb331-164">Exact version match</span></span> |
| <span data-ttu-id="bb331-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="bb331-165">(,1.0]</span></span> | <span data-ttu-id="bb331-166">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="bb331-166">x ≤ 1.0</span></span> | <span data-ttu-id="bb331-167">En yüksek sürümü, kapsamlı</span><span class="sxs-lookup"><span data-stu-id="bb331-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="bb331-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="bb331-168">(,1.0)</span></span> | <span data-ttu-id="bb331-169">< 1.0 x</span><span class="sxs-lookup"><span data-stu-id="bb331-169">x < 1.0</span></span> | <span data-ttu-id="bb331-170">Özel olarak, en yüksek sürüm</span><span class="sxs-lookup"><span data-stu-id="bb331-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="bb331-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="bb331-171">[1.0,2.0]</span></span> | <span data-ttu-id="bb331-172">1.0 ≤ x ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="bb331-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="bb331-173">Kapsamlı tam aralığı</span><span class="sxs-lookup"><span data-stu-id="bb331-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="bb331-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="bb331-174">(1.0,2.0)</span></span> | <span data-ttu-id="bb331-175">1.0 < < 2.0 x</span><span class="sxs-lookup"><span data-stu-id="bb331-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="bb331-176">Özel tam aralığı</span><span class="sxs-lookup"><span data-stu-id="bb331-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="bb331-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="bb331-177">[1.0,2.0)</span></span> | <span data-ttu-id="bb331-178">1.0 ≤ < 2.0 x</span><span class="sxs-lookup"><span data-stu-id="bb331-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="bb331-179">Karma dahil en düşük ve özel en yüksek sürüm</span><span class="sxs-lookup"><span data-stu-id="bb331-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="bb331-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="bb331-180">(1.0)</span></span>    | <span data-ttu-id="bb331-181">geçersiz</span><span class="sxs-lookup"><span data-stu-id="bb331-181">invalid</span></span> | <span data-ttu-id="bb331-182">geçersiz</span><span class="sxs-lookup"><span data-stu-id="bb331-182">invalid</span></span> |

<span data-ttu-id="bb331-183">PackageReference biçimini kullanırken bir joker karakter gösterimini kullanarak NuGet da destekler \*büyük, küçük, düzeltme eki ve sayının yayın öncesi son bölümü için.</span><span class="sxs-lookup"><span data-stu-id="bb331-183">When using the PackageReference format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="bb331-184">İle joker karakterler desteklenmez `packages.config` biçimi.</span><span class="sxs-lookup"><span data-stu-id="bb331-184">Wildcards are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="bb331-185">Yayın öncesi sürümleri, sürüm aralıklarını çözerken dahil edilmez.</span><span class="sxs-lookup"><span data-stu-id="bb331-185">Pre-release versions are not included when resolving version ranges.</span></span> <span data-ttu-id="bb331-186">Yayın öncesi sürümler *olan* joker karakter kullanırken dahil (\*).</span><span class="sxs-lookup"><span data-stu-id="bb331-186">Pre-release versions *are* included when using a wildcard (\*).</span></span> <span data-ttu-id="bb331-187">Sürüm aralığı *[1.0,2.0]*, örneğin, 2.0 beta, ancak joker karakter gösterimi içermez _2.0-\*_ yapar.</span><span class="sxs-lookup"><span data-stu-id="bb331-187">The version range *[1.0,2.0]*, for example, does not include 2.0-beta, but the wildcard notation _2.0-\*_ does.</span></span> <span data-ttu-id="bb331-188">Bkz: [sorun 912](https://github.com/NuGet/Home/issues/912) daha fazla yayın öncesi jokerler tartışma.</span><span class="sxs-lookup"><span data-stu-id="bb331-188">See [issue 912](https://github.com/NuGet/Home/issues/912) for further discussion on pre-release wildcards.</span></span>

### <a name="examples"></a><span data-ttu-id="bb331-189">Örnekler</span><span class="sxs-lookup"><span data-stu-id="bb331-189">Examples</span></span>

<span data-ttu-id="bb331-190">Proje dosyalarında her zaman bir sürüm veya sürüm aralığı için Paket bağımlılıklarını belirtin `packages.config` dosyaları ve `.nuspec` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="bb331-190">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="bb331-191">Bir sürüm veya sürüm aralığı, NuGet olmadan 2.8.x daha önce en son kullanılabilir Paket sürümü bir bağımlılık çözülürken ise seçerse NuGet 3.x ve daha sonra en düşük Paket sürümü seçer.</span><span class="sxs-lookup"><span data-stu-id="bb331-191">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="bb331-192">Bir sürüm veya sürüm aralığı bu belirsizliğin ortadan kaldırır. belirtme.</span><span class="sxs-lookup"><span data-stu-id="bb331-192">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="bb331-193">Proje dosyalarında (PackageReference) başvuruları</span><span class="sxs-lookup"><span data-stu-id="bb331-193">References in project files (PackageReference)</span></span>

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

<span data-ttu-id="bb331-194">**Başvurularının `packages.config`:**</span><span class="sxs-lookup"><span data-stu-id="bb331-194">**References in `packages.config`:**</span></span>

<span data-ttu-id="bb331-195">İçinde `packages.config`, her bağımlılık bir tam olarak listelenen `version` paketler geri yüklenirken kullanılan özniteliği.</span><span class="sxs-lookup"><span data-stu-id="bb331-195">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="bb331-196">`allowedVersions` Özniteliği yalnızca güncelleştirme işlemleri sırasında paket güncelleştirilmesi sürümleri sınırlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bb331-196">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

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

<span data-ttu-id="bb331-197">**Başvurularının `.nuspec` dosyaları**</span><span class="sxs-lookup"><span data-stu-id="bb331-197">**References in `.nuspec` files**</span></span>

<span data-ttu-id="bb331-198">`version` Özniteliğini bir `<dependency>` öğesi, bir bağımlılık için kabul edilebilir aralık sürümlerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="bb331-198">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

<!-- Accepts any 6.x.y version. -->
<dependency id="ExamplePackage" version="6.*" />

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

## <a name="normalized-version-numbers"></a><span data-ttu-id="bb331-199">Normalleştirilmiş sürüm numaraları</span><span class="sxs-lookup"><span data-stu-id="bb331-199">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="bb331-200">Bir değişiklik NuGet 3.4 ve üzeri budur.</span><span class="sxs-lookup"><span data-stu-id="bb331-200">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="bb331-201">Paketleri yükleme sırasında bir depodan edinme yeniden yükleyin veya geri yükleme işlemleri, NuGet 3.4 + sürüm numaraları gibi davranır:</span><span class="sxs-lookup"><span data-stu-id="bb331-201">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="bb331-202">Sürüm numaraları 2f3b kaldırılır:</span><span class="sxs-lookup"><span data-stu-id="bb331-202">Leading zeroes are removed from version numbers:</span></span>

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- <span data-ttu-id="bb331-203">Sürüm numarasının dördüncü bölümünde sıfır atlanacak</span><span class="sxs-lookup"><span data-stu-id="bb331-203">A zero in the fourth part of the version number will be omitted</span></span>

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

<span data-ttu-id="bb331-204">Bu normalleştirme paketleri sürüm numaraları etkilemez. Bu, yalnızca nasıl NuGet sürümlerini bağımlılıkları çözümlenirken eşleşen etkiler.</span><span class="sxs-lookup"><span data-stu-id="bb331-204">This normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="bb331-205">Ancak, NuGet paket depolarınızın bu değerleri Paket sürümü çoğaltma önlemek için aynı şekilde NuGet olarak ele almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bb331-205">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="bb331-206">Bu nedenle sürümünü içeren bir depo *1.0* paketi sürümü ayrıca barındırmamalıdır *1.0.0* ayrı ve farklı bir paket olarak.</span><span class="sxs-lookup"><span data-stu-id="bb331-206">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
