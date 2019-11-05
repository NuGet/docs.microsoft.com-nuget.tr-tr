---
title: NuGet paketlerindeki yayın öncesi sürümler
description: Yayın öncesi paketleri oluşturma kılavuzu
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 1c19f962dc9e42154c0f4374432548e867e9538a
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610708"
---
# <a name="building-pre-release-packages"></a><span data-ttu-id="55e94-103">Yayın öncesi paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="55e94-103">Building pre-release packages</span></span>

<span data-ttu-id="55e94-104">Güncelleştirilmiş bir paketi yeni bir sürüm numarasıyla serbest bıraktığınızda, NuGet bir "en son kararlı yayın" olarak, örneğin Visual Studio içindeki paket yöneticisi Kullanıcı arabiriminde gösterildiği gibi kabul eder:</span><span class="sxs-lookup"><span data-stu-id="55e94-104">Whenever you release an updated package with a new version number, NuGet considers that one as the "latest stable release" as shown, for example in the Package Manager UI within Visual Studio:</span></span>

![En son kararlı yayını gösteren Paket Yöneticisi Kullanıcı arabirimi](media/Prerelease_01-LatestStable.png)

<span data-ttu-id="55e94-106">Kararlı bir yayın, üretimde kullanılmak üzere yeterince güvenilir olarak kabul edilen bir sürümdür.</span><span class="sxs-lookup"><span data-stu-id="55e94-106">A stable release is one that's considered reliable enough to be used in production.</span></span> <span data-ttu-id="55e94-107">En son kararlı sürüm aynı zamanda bir paket güncelleştirmesi olarak veya paket geri yükleme sırasında ( [paketleri yeniden yükleme ve güncelleştirme](../consume-packages/reinstalling-and-updating-packages.md)bölümünde açıklandığı gibi kısıtlamalara tabidir) yüklenir.</span><span class="sxs-lookup"><span data-stu-id="55e94-107">The latest stable release is also the one that will be installed as a package update or during package restore (subject to constraints as described in [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)).</span></span>

<span data-ttu-id="55e94-108">NuGet 1,6 ve üzeri, yazılım sürümü yaşam döngüsünü desteklemek için yayın öncesi paketlerin dağıtımına izin verir; burada sürüm numarası, `-alpha`, `-beta`veya `-rc`gibi bir anlamsal sürüm oluşturma soneki içerir.</span><span class="sxs-lookup"><span data-stu-id="55e94-108">To support the software release lifecycle, NuGet 1.6 and later allows for the distribution of pre-release packages, where the version number includes a semantic versioning suffix such as `-alpha`, `-beta`, or `-rc`.</span></span> <span data-ttu-id="55e94-109">Daha fazla bilgi için bkz. [paket sürümü oluşturma](../concepts/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="55e94-109">For more information, see [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span>

<span data-ttu-id="55e94-110">Aşağıdaki yollarla bu tür sürümleri belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="55e94-110">You can specify such versions using one of the following ways:</span></span>

- <span data-ttu-id="55e94-111">**Projeniz [`PackageReference`](../consume-packages/package-references-in-project-files.md)kullanıyorsa,** `.csproj` dosyanın [`PackageVersion`](/dotnet/core/tools/csproj.md#packageversion) öğesine anlamsal sürüm sonekini dahil edin:</span><span class="sxs-lookup"><span data-stu-id="55e94-111">**If your project uses [`PackageReference`](../consume-packages/package-references-in-project-files.md)**: include the semantic version suffix in the `.csproj` file's [`PackageVersion`](/dotnet/core/tools/csproj.md#packageversion) element:</span></span>

    ```xml
    <PropertyGroup>
        <PackageVersion>1.0.1-alpha</PackageVersion>
    </PropertyGroup>
    ```

- <span data-ttu-id="55e94-112">**Projenizde bir [`packages.config`](../reference/packages-config.md) dosyası varsa**: [`.nuspec`](../reference/nuspec.md) dosyasının [`version`](../reference/nuspec.md#version) öğesine anlamsal sürüm sonekini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="55e94-112">**If your project has a [`packages.config`](../reference/packages-config.md) file**: include the semantic version suffix in the [`.nuspec`](../reference/nuspec.md) file's [`version`](../reference/nuspec.md#version) element:</span></span>

    ```xml
    <version>1.0.1-alpha</version>
    ```

<span data-ttu-id="55e94-113">Kararlı bir sürümü bırakmaya hazırsanız, soneki kaldırmanız yeterlidir ve paketin herhangi bir yayın öncesi sürümüne göre öncelikli olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="55e94-113">When you're ready to release a stable version, just remove the suffix and the package takes precedence over any pre-release versions.</span></span> <span data-ttu-id="55e94-114">Yeniden, bkz. [paket sürümü oluşturma](../concepts/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="55e94-114">Again, see [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span>

## <a name="installing-and-updating-pre-release-packages"></a><span data-ttu-id="55e94-115">Yayın öncesi paketleri yükleme ve güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="55e94-115">Installing and updating pre-release packages</span></span>

<span data-ttu-id="55e94-116">Varsayılan olarak, NuGet, paketlerle çalışırken yayın öncesi sürümleri içermez, ancak bu davranışı aşağıdaki şekilde değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="55e94-116">By default, NuGet does not include pre-release versions when working with packages, but you can change this behavior as follows:</span></span>

- <span data-ttu-id="55e94-117">**Visual Studio 'Da Paket Yöneticisi Kullanıcı arabirimi**: **NuGet Paketlerini Yönet** Kullanıcı arabiriminde, **ön sürümü dahil et** kutusunu işaretleyin:</span><span class="sxs-lookup"><span data-stu-id="55e94-117">**Package Manager UI in Visual Studio**: In the **Manage NuGet Packages** UI, check the **Include prerelease** box:</span></span>

    ![Visual Studio 'da ön sürümü dahil et onay kutusu](media/Prerelease_02-CheckPrerelease.png)

    <span data-ttu-id="55e94-119">Bu kutuyu ayarlama veya Temizleme, Paket Yöneticisi Kullanıcı arabirimini ve yükleyebileceğiniz sürümlerin listesini yeniler.</span><span class="sxs-lookup"><span data-stu-id="55e94-119">Setting or clearing this box will refresh the Package Manager UI and the list of available versions you can install.</span></span>

- <span data-ttu-id="55e94-120">**Paket Yöneticisi konsolu**: `-IncludePrerelease` anahtarını `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`ve `Update-Package` komutlarıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="55e94-120">**Package Manager Console**: Use the `-IncludePrerelease` switch with the `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, and `Update-Package` commands.</span></span> <span data-ttu-id="55e94-121">[PowerShell başvurusuna](../reference/powershell-reference.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="55e94-121">Refer to the [PowerShell Reference](../reference/powershell-reference.md).</span></span>

- <span data-ttu-id="55e94-122">**NUGET CLI**: `install`, `update`, `delete`ve `mirror` komutlarıyla `-prerelease` anahtarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="55e94-122">**NuGet CLI**: Use the `-prerelease` switch with the `install`, `update`, `delete`, and `mirror` commands.</span></span> <span data-ttu-id="55e94-123">[NUGET CLI başvurusuna](../reference/nuget-exe-cli-reference.md) bakın</span><span class="sxs-lookup"><span data-stu-id="55e94-123">Refer to the [NuGet CLI reference](../reference/nuget-exe-cli-reference.md)</span></span>

## <a name="semantic-versioning"></a><span data-ttu-id="55e94-124">Anlamsal sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="55e94-124">Semantic versioning</span></span>

<span data-ttu-id="55e94-125">[Anlamsal sürüm oluşturma veya SemVer kuralı](https://semver.org/spec/v1.0.0.html) , temel alınan kodun anlamını iletmek için sürüm numaralarında dizelerin nasıl kullanılacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="55e94-125">The [Semantic Versioning or SemVer convention](https://semver.org/spec/v1.0.0.html) describes how to utilize strings in version numbers to convey the meaning of the underlying code.</span></span>

<span data-ttu-id="55e94-126">Bu durumda, her sürüm üç bölümden oluşur ve aşağıdaki anlamı `Major.Minor.Patch`:</span><span class="sxs-lookup"><span data-stu-id="55e94-126">In this convention, each version has three parts, `Major.Minor.Patch`, with the following meaning:</span></span>

- <span data-ttu-id="55e94-127">`Major`: değişiklikler kesiliyor</span><span class="sxs-lookup"><span data-stu-id="55e94-127">`Major`: Breaking changes</span></span>
- <span data-ttu-id="55e94-128">`Minor`: yeni özellikler, ancak geriye dönük olarak uyumlu</span><span class="sxs-lookup"><span data-stu-id="55e94-128">`Minor`: New features, but backwards compatible</span></span>
- <span data-ttu-id="55e94-129">`Patch`: yalnızca geriye dönük uyumlu hata düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="55e94-129">`Patch`: Backwards compatible bug fixes only</span></span>

<span data-ttu-id="55e94-130">Yayın öncesi sürümler daha sonra düzeltme numarasından sonra bir tire ve dize eklenerek gösterilir.</span><span class="sxs-lookup"><span data-stu-id="55e94-130">Pre-release versions are then denoted by appending a hyphen and a string after the patch number.</span></span> <span data-ttu-id="55e94-131">Teknik açıdan, kısa çizgiden sonra *herhangi bir* dizeyi kullanabilirsiniz ve NuGet paketi yayın öncesi olarak kabul eder.</span><span class="sxs-lookup"><span data-stu-id="55e94-131">Technically speaking, you can use *any* string after the hyphen and NuGet will treat the package as pre-release.</span></span> <span data-ttu-id="55e94-132">Daha sonra NuGet, geçerli kullanıcı arabirimindeki tam sürüm numarasını görüntüleyerek tüketicilere göre anlamı yorumlamak için tüketicileri bırakır.</span><span class="sxs-lookup"><span data-stu-id="55e94-132">NuGet then displays the full version number in the applicable UI, leaving consumers to interpret the meaning for themselves.</span></span>

<span data-ttu-id="55e94-133">Bu göz önünde bulundurularak, aşağıdaki gibi tanınan adlandırma kurallarını izlemek genellikle yararlı olur:</span><span class="sxs-lookup"><span data-stu-id="55e94-133">With this in mind, it's generally good to follow recognized naming conventions such as the following:</span></span>

- <span data-ttu-id="55e94-134">`-alpha`: genellikle süren iş ve deneme için kullanılan Alpha sürümü</span><span class="sxs-lookup"><span data-stu-id="55e94-134">`-alpha`: Alpha release, typically used for work-in-progress and experimentation</span></span>
- <span data-ttu-id="55e94-135">`-beta`: beta sürümü, genellikle bir sonraki planlı yayın için bir özelliktir, ancak bilinen hatalar içerebilir.</span><span class="sxs-lookup"><span data-stu-id="55e94-135">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="55e94-136">`-rc`: yayın adayı, genellikle önemli hatalar oluşmadığı takdirde son derece nihai (kararlı) bir sürümdür.</span><span class="sxs-lookup"><span data-stu-id="55e94-136">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="55e94-137">NuGet 4.3.0 +, `1.0.1-build.23`gibi nokta gösterimi ile yayın öncesi numaraları destekleyen [anlamsal sürüm oluşturma v 2.0.0](https://semver.org/spec/v2.0.0.html)'yi destekler.</span><span class="sxs-lookup"><span data-stu-id="55e94-137">NuGet 4.3.0+ supports [Semantic Versioning v2.0.0](https://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in `1.0.1-build.23`.</span></span> <span data-ttu-id="55e94-138">Nokta gösterimi 4.3.0 öncesi NuGet sürümleriyle desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="55e94-138">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="55e94-139">NuGet 'in önceki sürümlerinde `1.0.1-build23` gibi bir form kullanabilirsiniz, ancak bu her zaman yayın öncesi sürüm olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="55e94-139">In earlier versions of NuGet, you could use a form like `1.0.1-build23` but this was always considered a pre-release version.</span></span>

<span data-ttu-id="55e94-140">Ancak kullandığınız son ekler, NuGet 'e ters alfabetik sırada öncelik verecektir:</span><span class="sxs-lookup"><span data-stu-id="55e94-140">Whatever suffixes you use, however, NuGet will give them precedence in reverse alphabetical order:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta.12
    1.0.1-beta.5
    1.0.1-beta
    1.0.1-alpha.2
    1.0.1-alpha

<span data-ttu-id="55e94-141">Gösterildiği gibi, herhangi bir sonek olmadan sürüm, yayın öncesi sürümlerden her zaman öncelikli olur.</span><span class="sxs-lookup"><span data-stu-id="55e94-141">As shown, the version without any suffix will always take precedence over pre-release versions.</span></span>

<span data-ttu-id="55e94-142">Önde gelen 0s, semver2 için gerekli değildir, ancak eski sürüm şemasıyla bulunur.</span><span class="sxs-lookup"><span data-stu-id="55e94-142">Leading 0s are not needed with semver2, but they are with the old version schema.</span></span> <span data-ttu-id="55e94-143">Çift basamaklı sayılar (veya daha fazla) kullanan serbest bırakma etiketleriyle sayısal sonekler kullanırsanız, sayılar daha büyük olduğunda doğru sıraladıklarından emin olmak için Beta. 01 ve Beta. 05 ' de önde gelen sıfırları kullanın.</span><span class="sxs-lookup"><span data-stu-id="55e94-143">If you use numerical suffixes with pre-release tags that might use double-digit numbers (or more), use leading zeroes as in beta.01 and beta.05 to ensure that they sort correctly when the numbers get larger.</span></span> <span data-ttu-id="55e94-144">Bu öneri yalnızca eski sürüm şeması için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="55e94-144">This recommendation only applies to the old version schema.</span></span>
