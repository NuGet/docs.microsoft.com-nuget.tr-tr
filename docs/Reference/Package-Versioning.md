---
title: "NuGet paketi sürüm başvurusu | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 6ee3c826-dd3a-4fa9-863f-1fd80bc4230f
description: "Sürüm numaraları ve diğer paketleri, bağlı bir NuGet paketi ve bağımlılıkları nasıl yükleneceğini aralıklarını belirtme hakkında tam ayrıntılar."
keywords: "sürüm oluşturma, NuGet Paket bağımlılıklarını, NuGet bağımlılık sürümleri, NuGet sürüm numaralarını, NuGet Paket sürümü, sürüm aralıkları, sürüm belirtimleri, normalleştirilmiş sürüm numaraları"
ms.reviewer:
- anandr
- karann-msft
- unniravindranathan
ms.openlocfilehash: cb5624a2fd99e8afd8a8226fd786343f485041c4
ms.sourcegitcommit: c27e565de485cbe836e6c2a66e44a50b35b487ff
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/09/2018
---
# <a name="package-versioning"></a><span data-ttu-id="0f6f8-104">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="0f6f8-104">Package versioning</span></span>

<span data-ttu-id="0f6f8-105">Belirli bir paket her zaman paket tanımlayıcısını ve tam bir sürüm numarası kullanılarak olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="0f6f8-105">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="0f6f8-106">Örneğin, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) nuget.org üzerinde çeşitli düzine belirli paketler sürümünden arasında değişen kullanılabilir olan *4.1.10311* sürümüne *6.1.3* (en son kararlı yayın) ve yayın öncesi sürümleri çeşitli *6.2.0-beta1*.</span><span class="sxs-lookup"><span data-stu-id="0f6f8-106">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="0f6f8-107">Bir paket oluştururken, bir isteğe bağlı bir yayım öncesi metin sonekiyle özel sürüm numarası atayın.</span><span class="sxs-lookup"><span data-stu-id="0f6f8-107">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="0f6f8-108">Diğer taraftan, paketleri kullanırken, bir tam sürüm numarası veya kabul edilebilir sürüm aralığı belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f6f8-108">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="0f6f8-109">Bu konuda:</span><span class="sxs-lookup"><span data-stu-id="0f6f8-109">In this topic:</span></span>

- <span data-ttu-id="0f6f8-110">[Sürüm Temelleri](#version-basics) yayın öncesi sonekleri dahil olmak üzere.</span><span class="sxs-lookup"><span data-stu-id="0f6f8-110">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="0f6f8-111">Sürüm aralıkları ve joker karakterler</span><span class="sxs-lookup"><span data-stu-id="0f6f8-111">Version ranges and wildcards</span></span>](#version-ranges-and-wildcards)
- [<span data-ttu-id="0f6f8-112">Normalleştirilmiş sürüm numaraları</span><span class="sxs-lookup"><span data-stu-id="0f6f8-112">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="0f6f8-113">Sürüm temelleri</span><span class="sxs-lookup"><span data-stu-id="0f6f8-113">Version basics</span></span>

<span data-ttu-id="0f6f8-114">Belirli bir sürüm numarasını biçimindedir *Major.Minor.Patch [-soneki]*, burada bileşenleri şu anlama gelir:</span><span class="sxs-lookup"><span data-stu-id="0f6f8-114">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="0f6f8-115">*Ana*: yeni değişiklikler</span><span class="sxs-lookup"><span data-stu-id="0f6f8-115">*Major*: Breaking changes</span></span>
- <span data-ttu-id="0f6f8-116">*İkincil*: geriye dönük olarak uyumlu ancak yeni özellikler</span><span class="sxs-lookup"><span data-stu-id="0f6f8-116">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="0f6f8-117">*Düzeltme Eki*: yalnızca geriye dönük olarak uyumlu hata düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="0f6f8-117">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="0f6f8-118">*-Soneki* (isteğe bağlı): bir tire izlenen bir yayım öncesi sürümünü belirten bir dizeyle (aşağıdaki [anlamsal sürüm oluşturma veya SemVer 1.0 kuralı](http://semver.org/spec/v1.0.0.html)).</span><span class="sxs-lookup"><span data-stu-id="0f6f8-118">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](http://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="0f6f8-119">**Örnekler:**</span><span class="sxs-lookup"><span data-stu-id="0f6f8-119">**Examples:**</span></span>
```
1.0.1
6.11.1231
4.3.1-rc
2.2.44-beta1
```

> [!Important]
> <span data-ttu-id="0f6f8-120">nuget.org tam bir sürüm numarası eksik paketini karşıya yükleme reddeder.</span><span class="sxs-lookup"><span data-stu-id="0f6f8-120">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="0f6f8-121">Sürüm belirtilmelidir `.nuspec` veya paketi oluşturmak üzere kullanılan proje dosyası.</span><span class="sxs-lookup"><span data-stu-id="0f6f8-121">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="0f6f8-122">Yayın öncesi sürümleri</span><span class="sxs-lookup"><span data-stu-id="0f6f8-122">Pre-release versions</span></span>

<span data-ttu-id="0f6f8-123">Teknik olarak konuşarak paket oluşturucuları herhangi bir dize sonek olarak NuGet herhangi bir sürüm yayın öncesi değerlendirir ve diğer bir yorumlama yapar gibi bir yayın öncesi sürüm belirtmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f6f8-123">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="0f6f8-124">Diğer bir deyişle, tam sürüm ne olursa olsun kullanıcı Arabiriminde dize NuGet görüntüler eklendiyse, tüketiciye soneki 's anlamı herhangi yorumu çıkılıyor.</span><span class="sxs-lookup"><span data-stu-id="0f6f8-124">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="0f6f8-125">Bu, paket geliştiriciler genellikle tanınan adlandırma kurallarına uygun olduğu söylenebilir:</span><span class="sxs-lookup"><span data-stu-id="0f6f8-125">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="0f6f8-126">`-alpha`: Genelde iş ilerleme ve deneme için kullanılan alfa sürüm.</span><span class="sxs-lookup"><span data-stu-id="0f6f8-126">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="0f6f8-127">`-beta`: Beta sürümü, genellikle bir özellik için sonraki tam planlanmış serbest bırakma, ancak bilinen hataları içerebilir.</span><span class="sxs-lookup"><span data-stu-id="0f6f8-127">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="0f6f8-128">`-rc`: Sürüm Adayı, genellikle büyük olasılıkla son bir yayın (stable) önemli hatalar ortaya çıkan sürece.</span><span class="sxs-lookup"><span data-stu-id="0f6f8-128">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="0f6f8-129">NuGet 4.3.0+ destekleyen [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), olarak noktalı gösterim ön sürüm numaralarıyla destekleyen *1.0.1-build.23*.</span><span class="sxs-lookup"><span data-stu-id="0f6f8-129">NuGet 4.3.0+ supports [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="0f6f8-130">Noktalı gösterim 4.3.0 önce NuGet sürümleriyle desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="0f6f8-130">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="0f6f8-131">Bir form gibi kullanabilirsiniz *1.0.1-build23*.</span><span class="sxs-lookup"><span data-stu-id="0f6f8-131">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="0f6f8-132">Paket referanslarını ve birden çok paket sürümü yalnızca soneki ile farklı çözülürken NuGet sonek olmayan bir sürümünü ilk seçer ve ardından yayın öncesi sürümler ters alfabetik sırada öncelik uygular.</span><span class="sxs-lookup"><span data-stu-id="0f6f8-132">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="0f6f8-133">Örneğin, aşağıdaki sürümleri gösterilen sırada seçilen:</span><span class="sxs-lookup"><span data-stu-id="0f6f8-133">For example, the following versions would be chosen in the exact order shown:</span></span>

```
1.0.1
1.0.1-zzz
1.0.1-rc
1.0.1-open
1.0.1-beta
1.0.1-alpha2
1.0.1-alpha
1.0.1-aaa
```

## <a name="semantic-versioning-200"></a><span data-ttu-id="0f6f8-134">Anlamsal sürüm oluşturma 2.0.0</span><span class="sxs-lookup"><span data-stu-id="0f6f8-134">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="0f6f8-135">NuGet 4.3.0+ ve Visual Studio 2017 sürüm 15.3 + ile NuGet destekleyen [anlamsal sürüm oluşturma 2.0.0](http://semver.org/spec/v2.0.0.html).</span><span class="sxs-lookup"><span data-stu-id="0f6f8-135">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="0f6f8-136">SemVer v2.0.0 belirli semantiği eski istemciler desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="0f6f8-136">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="0f6f8-137">NuGet aşağıdaki ifadelerden true ise SemVer v2.0.0 belirli olması için bir paket sürümü göz önünde bulundurur:</span><span class="sxs-lookup"><span data-stu-id="0f6f8-137">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="0f6f8-138">Noktalı virgülle ayrılmış, örneğin, yayın öncesi etiket *1.0.0-alpha.1*</span><span class="sxs-lookup"><span data-stu-id="0f6f8-138">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="0f6f8-139">Yapı-meta verileri, örneğin, sürümde *1.0.0+githash*</span><span class="sxs-lookup"><span data-stu-id="0f6f8-139">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="0f6f8-140">Aşağıdaki ifadeler doğru ise nuget.org için bir paket SemVer v2.0.0 paket olarak tanımlanır:</span><span class="sxs-lookup"><span data-stu-id="0f6f8-140">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="0f6f8-141">Paketin kendi SemVer v2.0.0 uyumlu ancak değil SemVer v1.0.0 uyumlu, yukarıda tanımlanan sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="0f6f8-141">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="0f6f8-142">Paketin bağımlılık sürümü aralıklardan herhangi biriyle uyumlu SemVer v2.0.0 ancak değil SemVer v1.0.0 uyumlu, yukarıda tanımlanan bir minimum veya maksimum sürümüne sahiptir; Örneğin, *[1.0.0-alpha.1,)*.</span><span class="sxs-lookup"><span data-stu-id="0f6f8-142">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="0f6f8-143">Nuget.org için SemVer v2.0.0 özgü paketini karşıya yükleyin, paketin eski istemcileri için görünmez ve yalnızca aşağıdaki NuGet istemcileri için kullanılabilir şöyledir:</span><span class="sxs-lookup"><span data-stu-id="0f6f8-143">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="0f6f8-144">NuGet 4.3.0+</span><span class="sxs-lookup"><span data-stu-id="0f6f8-144">NuGet 4.3.0+</span></span>
- <span data-ttu-id="0f6f8-145">Visual Studio 2017 sürüm 15.3 +</span><span class="sxs-lookup"><span data-stu-id="0f6f8-145">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="0f6f8-146">Visual Studio 2015 ile birlikte [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="0f6f8-146">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="0f6f8-147">DotNet.exe (.NET SDK'sı 2.0.0+)</span><span class="sxs-lookup"><span data-stu-id="0f6f8-147">dotnet.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="0f6f8-148">Üçüncü taraf istemciler:</span><span class="sxs-lookup"><span data-stu-id="0f6f8-148">Third-party clients:</span></span>

- <span data-ttu-id="0f6f8-149">JetBrains binici</span><span class="sxs-lookup"><span data-stu-id="0f6f8-149">JetBrains Rider</span></span>
- <span data-ttu-id="0f6f8-150">Paket sürüm 5.0 +</span><span class="sxs-lookup"><span data-stu-id="0f6f8-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a><span data-ttu-id="0f6f8-151">Sürüm aralıkları ve joker karakterler</span><span class="sxs-lookup"><span data-stu-id="0f6f8-151">Version ranges and wildcards</span></span>

<span data-ttu-id="0f6f8-152">Paket bağımlılıklarını söz konusu olduğunda NuGet sürümü aralıkları, aşağıdaki şekilde özetlenmiştir belirtmek için aralığı gösterimini kullanarak destekler:</span><span class="sxs-lookup"><span data-stu-id="0f6f8-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="0f6f8-153">Gösterimi</span><span class="sxs-lookup"><span data-stu-id="0f6f8-153">Notation</span></span> | <span data-ttu-id="0f6f8-154">Uygulanan kural</span><span class="sxs-lookup"><span data-stu-id="0f6f8-154">Applied rule</span></span> | <span data-ttu-id="0f6f8-155">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0f6f8-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="0f6f8-156">1.0</span><span class="sxs-lookup"><span data-stu-id="0f6f8-156">1.0</span></span> | <span data-ttu-id="0f6f8-157">1.0 ≤ x</span><span class="sxs-lookup"><span data-stu-id="0f6f8-157">1.0 ≤ x</span></span> | <span data-ttu-id="0f6f8-158">En düşük sürüm, (bunlar dahil)</span><span class="sxs-lookup"><span data-stu-id="0f6f8-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="0f6f8-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="0f6f8-159">(1.0,)</span></span> | <span data-ttu-id="0f6f8-160">1.0 < x</span><span class="sxs-lookup"><span data-stu-id="0f6f8-160">1.0 < x</span></span> | <span data-ttu-id="0f6f8-161">En düşük sürüm, özel</span><span class="sxs-lookup"><span data-stu-id="0f6f8-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="0f6f8-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="0f6f8-162">[1.0]</span></span> | <span data-ttu-id="0f6f8-163">x 1.0 ==</span><span class="sxs-lookup"><span data-stu-id="0f6f8-163">x == 1.0</span></span> | <span data-ttu-id="0f6f8-164">Tam sürümü eşleşmiyor</span><span class="sxs-lookup"><span data-stu-id="0f6f8-164">Exact version match</span></span> |
| <span data-ttu-id="0f6f8-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="0f6f8-165">(,1.0]</span></span> | <span data-ttu-id="0f6f8-166">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="0f6f8-166">x ≤ 1.0</span></span> | <span data-ttu-id="0f6f8-167">En yüksek sürüm, (bunlar dahil)</span><span class="sxs-lookup"><span data-stu-id="0f6f8-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="0f6f8-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="0f6f8-168">(,1.0)</span></span> | <span data-ttu-id="0f6f8-169">< 1.0 x</span><span class="sxs-lookup"><span data-stu-id="0f6f8-169">x < 1.0</span></span> | <span data-ttu-id="0f6f8-170">Özel olarak, en yüksek sürüm</span><span class="sxs-lookup"><span data-stu-id="0f6f8-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="0f6f8-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="0f6f8-171">[1.0,2.0]</span></span> | <span data-ttu-id="0f6f8-172">1.0 ≤ x ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="0f6f8-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="0f6f8-173">Tam aralık, (bunlar dahil)</span><span class="sxs-lookup"><span data-stu-id="0f6f8-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="0f6f8-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="0f6f8-174">(1.0,2.0)</span></span> | <span data-ttu-id="0f6f8-175">1.0 < < 2.0 x</span><span class="sxs-lookup"><span data-stu-id="0f6f8-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="0f6f8-176">Tam aralık, özel</span><span class="sxs-lookup"><span data-stu-id="0f6f8-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="0f6f8-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="0f6f8-177">[1.0,2.0)</span></span> | <span data-ttu-id="0f6f8-178">1.0 ≤ < 2.0 x</span><span class="sxs-lookup"><span data-stu-id="0f6f8-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="0f6f8-179">Karma (bunlar dahil) en düşük ve özel en yüksek sürüm</span><span class="sxs-lookup"><span data-stu-id="0f6f8-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="0f6f8-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="0f6f8-180">(1.0)</span></span>    | <span data-ttu-id="0f6f8-181">geçersiz</span><span class="sxs-lookup"><span data-stu-id="0f6f8-181">invalid</span></span> | <span data-ttu-id="0f6f8-182">geçersiz</span><span class="sxs-lookup"><span data-stu-id="0f6f8-182">invalid</span></span> |

<span data-ttu-id="0f6f8-183">PackageReference kullanırken veya `project.json` bir joker karakter gösterimini kullanarak destekler de başvuru biçimleri, NuGet paketini \*, birincil, ikincil, düzeltme eki ve sayının yayın öncesi soneki bölümleri için.</span><span class="sxs-lookup"><span data-stu-id="0f6f8-183">When using the PackageReference or `project.json` package reference formats, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="0f6f8-184">İle joker karakterler desteklenmez `packages.config` biçimi.</span><span class="sxs-lookup"><span data-stu-id="0f6f8-184">Wildcards are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="0f6f8-185">Yayın öncesi sürümleri, sürüm aralıkları çözülürken dahil edilmez.</span><span class="sxs-lookup"><span data-stu-id="0f6f8-185">Pre-release versions are not included when resolving version ranges.</span></span> <span data-ttu-id="0f6f8-186">Yayın öncesi sürümler *olan* bir joker karakter kullanırken dahil (\*).</span><span class="sxs-lookup"><span data-stu-id="0f6f8-186">Pre-release versions *are* included when using a wildcard (\*).</span></span> <span data-ttu-id="0f6f8-187">Sürüm aralığı *[1.0,2.0]*, örneğin, 2.0 beta ancak joker gösterimi içermez _2.0-*_ yapar.</span><span class="sxs-lookup"><span data-stu-id="0f6f8-187">The version range *[1.0,2.0]*, for example, does not include 2.0-beta, but the wildcard notation _2.0-*_ does.</span></span> <span data-ttu-id="0f6f8-188">Bkz: [sorun 912](https://github.com/NuGet/Home/issues/912) yayın öncesi joker karakterler hakkında daha fazla açıklama için.</span><span class="sxs-lookup"><span data-stu-id="0f6f8-188">See [issue 912](https://github.com/NuGet/Home/issues/912) for further discussion on pre-release wildcards.</span></span>

### <a name="examples"></a><span data-ttu-id="0f6f8-189">Örnekler</span><span class="sxs-lookup"><span data-stu-id="0f6f8-189">Examples</span></span>

<span data-ttu-id="0f6f8-190">Her zaman bir sürümü ya da sürüm aralığı Paket bağımlılıklarını için proje dosyalarında belirtin `packages.config` dosyaları ve `.nuspec` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="0f6f8-190">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="0f6f8-191">Sürüm veya sürüm aralığı, NuGet olmadan 2.8.x ve daha önce en son kullanılabilir Paket sürümü bir bağımlılık çözülürken ancak seçer NuGet 3.x ve daha sonra en düşük Paket sürümü seçer.</span><span class="sxs-lookup"><span data-stu-id="0f6f8-191">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="0f6f8-192">Bir sürümün ya da bu belirsizlik aralığı önler sürümünün belirtme.</span><span class="sxs-lookup"><span data-stu-id="0f6f8-192">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="0f6f8-193">Proje dosyaları (PackageReference) başvuruları</span><span class="sxs-lookup"><span data-stu-id="0f6f8-193">References in project files (PackageReference)</span></span>

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

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

<span data-ttu-id="0f6f8-194">**Başvurur `packages.config`:**</span><span class="sxs-lookup"><span data-stu-id="0f6f8-194">**References in `packages.config`:**</span></span>

<span data-ttu-id="0f6f8-195">İçinde `packages.config`, her bağımlılık bir tam listelenen `version` paketleri geri yüklenirken kullanılan özniteliği.</span><span class="sxs-lookup"><span data-stu-id="0f6f8-195">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="0f6f8-196">`allowedVersions` Özniteliği için paket güncelleştirilmesi sürümleri sınırlamak için yalnızca güncelleştirme işlemleri sırasında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0f6f8-196">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

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

<span data-ttu-id="0f6f8-197">**Başvurur `.nuspec` dosyaları**</span><span class="sxs-lookup"><span data-stu-id="0f6f8-197">**References in `.nuspec` files**</span></span>

<span data-ttu-id="0f6f8-198">`version` Özniteliğini bir `<dependency>` öğesi için bir bağımlılık kabul edilebilir aralık sürümlerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="0f6f8-198">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

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

## <a name="normalized-version-numbers"></a><span data-ttu-id="0f6f8-199">Normalleştirilmiş sürüm numaraları</span><span class="sxs-lookup"><span data-stu-id="0f6f8-199">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="0f6f8-200">Önemli bir değişiklik NuGet 3.4 ve daha sonra budur.</span><span class="sxs-lookup"><span data-stu-id="0f6f8-200">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="0f6f8-201">Yükleme sırasında bir depodan paketler alma yeniden yükleyin veya geri yükleme işlemleri, NuGet 3.4 + sürüm numaraları gibi davranır:</span><span class="sxs-lookup"><span data-stu-id="0f6f8-201">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="0f6f8-202">Sürüm numaraları 2f3b kaldırılır:</span><span class="sxs-lookup"><span data-stu-id="0f6f8-202">Leading zeroes are removed from version numbers:</span></span>

    ```
    1.00 is treated as 1.0
    1.01.1 is treated as 1.1.1
    1.00.0.1 is treated as 1.0.0.1
    ```

- <span data-ttu-id="0f6f8-203">Sürüm numarasını dördüncü bir parçası olarak sıfır atlanacak</span><span class="sxs-lookup"><span data-stu-id="0f6f8-203">A zero in the fourth part of the version number will be omitted</span></span>

    ```
    1.0.0.0 is treated as 1.0.0
    1.0.01.0 is treated as 1.0.1
    ```

<span data-ttu-id="0f6f8-204">Bu normalleştirme paketlerde kendilerini sürüm numaraları etkilemez; Bu, yalnızca nasıl NuGet sürümleri bağımlılıkları çözümlenirken eşleşen etkiler.</span><span class="sxs-lookup"><span data-stu-id="0f6f8-204">This normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="0f6f8-205">Ancak, NuGet paketi depoları bu değerleri Paket sürümü çoğaltılmasını önlemek için aynı şekilde NuGet ele almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0f6f8-205">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="0f6f8-206">Bu nedenle sürümünü içeren bir havuz *1.0* paketi sürümünü de barındırmamalıdır *1.0.0* ayrı ve farklı bir paket olarak.</span><span class="sxs-lookup"><span data-stu-id="0f6f8-206">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
