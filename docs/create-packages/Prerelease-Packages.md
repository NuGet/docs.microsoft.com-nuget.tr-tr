---
title: NuGet paketlerindeki yayın öncesi sürümler
description: Yayın öncesi paketleri oluşturma kılavuzu
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 5dda56ccd4c959bcbcbd12b7a4771ddff1fe7530
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623012"
---
# <a name="building-pre-release-packages"></a><span data-ttu-id="a8180-103">Yayın öncesi paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="a8180-103">Building pre-release packages</span></span>

<span data-ttu-id="a8180-104">Güncelleştirilmiş bir paketi yeni bir sürüm numarasıyla serbest bıraktığınızda, NuGet bir "en son kararlı yayın" olarak, örneğin Visual Studio içindeki paket yöneticisi Kullanıcı arabiriminde gösterildiği gibi kabul eder:</span><span class="sxs-lookup"><span data-stu-id="a8180-104">Whenever you release an updated package with a new version number, NuGet considers that one as the "latest stable release" as shown, for example in the Package Manager UI within Visual Studio:</span></span>

![En son kararlı yayını gösteren Paket Yöneticisi Kullanıcı arabirimi](media/Prerelease_01-LatestStable.png)

<span data-ttu-id="a8180-106">Kararlı bir yayın, üretimde kullanılmak üzere yeterince güvenilir olarak kabul edilen bir sürümdür.</span><span class="sxs-lookup"><span data-stu-id="a8180-106">A stable release is one that's considered reliable enough to be used in production.</span></span> <span data-ttu-id="a8180-107">En son kararlı sürüm aynı zamanda bir paket güncelleştirmesi olarak veya paket geri yükleme sırasında ( [paketleri yeniden yükleme ve güncelleştirme](../consume-packages/reinstalling-and-updating-packages.md)bölümünde açıklandığı gibi kısıtlamalara tabidir) yüklenir.</span><span class="sxs-lookup"><span data-stu-id="a8180-107">The latest stable release is also the one that will be installed as a package update or during package restore (subject to constraints as described in [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)).</span></span>

<span data-ttu-id="a8180-108">NuGet 1,6 ve üzeri, yazılım sürümü yaşam döngüsünü desteklemek için yayın öncesi paketlerin dağıtımına izin verir; burada sürüm numarası,, veya gibi bir anlamsal sürüm oluşturma soneki içerir `-alpha` `-beta` `-rc` .</span><span class="sxs-lookup"><span data-stu-id="a8180-108">To support the software release lifecycle, NuGet 1.6 and later allows for the distribution of pre-release packages, where the version number includes a semantic versioning suffix such as `-alpha`, `-beta`, or `-rc`.</span></span> <span data-ttu-id="a8180-109">Daha fazla bilgi için bkz. [paket sürümü oluşturma](../concepts/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="a8180-109">For more information, see [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span>

<span data-ttu-id="a8180-110">Aşağıdaki yollarla bu tür sürümleri belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a8180-110">You can specify such versions using one of the following ways:</span></span>

- <span data-ttu-id="a8180-111">\*\*Projeniz kullanıyorsa [`PackageReference`](../consume-packages/package-references-in-project-files.md) \*\*: `.csproj` dosyanın öğesine anlam sürümü sonekini dahil et: [`PackageVersion`](/dotnet/core/tools/csproj#packageversion)</span><span class="sxs-lookup"><span data-stu-id="a8180-111">**If your project uses [`PackageReference`](../consume-packages/package-references-in-project-files.md)**: include the semantic version suffix in the `.csproj` file's [`PackageVersion`](/dotnet/core/tools/csproj#packageversion) element:</span></span>

    ```xml
    <PropertyGroup>
        <PackageVersion>1.0.1-alpha</PackageVersion>
    </PropertyGroup>
    ```

- <span data-ttu-id="a8180-112">**Projenizde bir [`packages.config`](../reference/packages-config.md) dosya varsa**: dosyanın öğesine anlam sürümü sonekini ekleyin [`.nuspec`](../reference/nuspec.md) [`version`](../reference/nuspec.md#version) :</span><span class="sxs-lookup"><span data-stu-id="a8180-112">**If your project has a [`packages.config`](../reference/packages-config.md) file**: include the semantic version suffix in the [`.nuspec`](../reference/nuspec.md) file's [`version`](../reference/nuspec.md#version) element:</span></span>

    ```xml
    <version>1.0.1-alpha</version>
    ```

<span data-ttu-id="a8180-113">Kararlı bir sürümü bırakmaya hazırsanız, soneki kaldırmanız yeterlidir ve paketin herhangi bir yayın öncesi sürümüne göre öncelikli olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a8180-113">When you're ready to release a stable version, just remove the suffix and the package takes precedence over any pre-release versions.</span></span> <span data-ttu-id="a8180-114">Yeniden, bkz. [paket sürümü oluşturma](../concepts/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="a8180-114">Again, see [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span>

## <a name="installing-and-updating-pre-release-packages"></a><span data-ttu-id="a8180-115">Yayın öncesi paketleri yükleme ve güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="a8180-115">Installing and updating pre-release packages</span></span>

<span data-ttu-id="a8180-116">Varsayılan olarak, NuGet, paketlerle çalışırken yayın öncesi sürümleri içermez, ancak bu davranışı aşağıdaki şekilde değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a8180-116">By default, NuGet does not include pre-release versions when working with packages, but you can change this behavior as follows:</span></span>

- <span data-ttu-id="a8180-117">**Visual Studio 'Da Paket Yöneticisi Kullanıcı arabirimi**: **NuGet Paketlerini Yönet** Kullanıcı arabiriminde, **ön sürümü dahil et** kutusunu işaretleyin:</span><span class="sxs-lookup"><span data-stu-id="a8180-117">**Package Manager UI in Visual Studio**: In the **Manage NuGet Packages** UI, check the **Include prerelease** box:</span></span>

    ![Visual Studio 'da ön sürümü dahil et onay kutusu](media/Prerelease_02-CheckPrerelease.png)

    <span data-ttu-id="a8180-119">Bu kutuyu ayarlama veya Temizleme, Paket Yöneticisi Kullanıcı arabirimini ve yükleyebileceğiniz sürümlerin listesini yeniler.</span><span class="sxs-lookup"><span data-stu-id="a8180-119">Setting or clearing this box will refresh the Package Manager UI and the list of available versions you can install.</span></span>

- <span data-ttu-id="a8180-120">**Paket Yöneticisi konsolu**:,,, `-IncludePrerelease` `Find-Package` `Get-Package` `Install-Package` `Sync-Package` ve `Update-Package` komutlarıyla anahtarı kullanın.</span><span class="sxs-lookup"><span data-stu-id="a8180-120">**Package Manager Console**: Use the `-IncludePrerelease` switch with the `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, and `Update-Package` commands.</span></span> <span data-ttu-id="a8180-121">[PowerShell başvurusuna](../reference/powershell-reference.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="a8180-121">Refer to the [PowerShell Reference](../reference/powershell-reference.md).</span></span>

- <span data-ttu-id="a8180-122">**NuGet CLI**:,, `-prerelease` `install` `update` `delete` ve komutlarıyla anahtarı kullanın `mirror` .</span><span class="sxs-lookup"><span data-stu-id="a8180-122">**NuGet CLI**: Use the `-prerelease` switch with the `install`, `update`, `delete`, and `mirror` commands.</span></span> <span data-ttu-id="a8180-123">[NUGET CLI başvurusuna](../reference/nuget-exe-cli-reference.md) bakın</span><span class="sxs-lookup"><span data-stu-id="a8180-123">Refer to the [NuGet CLI reference](../reference/nuget-exe-cli-reference.md)</span></span>

## <a name="semantic-versioning"></a><span data-ttu-id="a8180-124">Anlamsal sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="a8180-124">Semantic versioning</span></span>

<span data-ttu-id="a8180-125">[Anlamsal sürüm oluşturma veya SemVer kuralı](https://semver.org/spec/v1.0.0.html) , temel alınan kodun anlamını iletmek için sürüm numaralarında dizelerin nasıl kullanılacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="a8180-125">The [Semantic Versioning or SemVer convention](https://semver.org/spec/v1.0.0.html) describes how to utilize strings in version numbers to convey the meaning of the underlying code.</span></span>

<span data-ttu-id="a8180-126">Bu kurala göre, her sürüm üç bölümden oluşur ve `Major.Minor.Patch` aşağıdaki anlamı vardır:</span><span class="sxs-lookup"><span data-stu-id="a8180-126">In this convention, each version has three parts, `Major.Minor.Patch`, with the following meaning:</span></span>

- <span data-ttu-id="a8180-127">`Major`: Değişiklikler kesiliyor</span><span class="sxs-lookup"><span data-stu-id="a8180-127">`Major`: Breaking changes</span></span>
- <span data-ttu-id="a8180-128">`Minor`: Yeni özellikler, ancak geriye dönük olarak uyumlu</span><span class="sxs-lookup"><span data-stu-id="a8180-128">`Minor`: New features, but backwards compatible</span></span>
- <span data-ttu-id="a8180-129">`Patch`: Yalnızca geriye dönük uyumlu hata düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="a8180-129">`Patch`: Backwards compatible bug fixes only</span></span>

<span data-ttu-id="a8180-130">Yayın öncesi sürümler daha sonra düzeltme numarasından sonra bir tire ve dize eklenerek gösterilir.</span><span class="sxs-lookup"><span data-stu-id="a8180-130">Pre-release versions are then denoted by appending a hyphen and a string after the patch number.</span></span> <span data-ttu-id="a8180-131">Teknik açıdan, kısa çizgiden sonra *herhangi bir* dizeyi kullanabilirsiniz ve NuGet paketi yayın öncesi olarak kabul eder.</span><span class="sxs-lookup"><span data-stu-id="a8180-131">Technically speaking, you can use *any* string after the hyphen and NuGet will treat the package as pre-release.</span></span> <span data-ttu-id="a8180-132">Daha sonra NuGet, geçerli kullanıcı arabirimindeki tam sürüm numarasını görüntüleyerek tüketicilere göre anlamı yorumlamak için tüketicileri bırakır.</span><span class="sxs-lookup"><span data-stu-id="a8180-132">NuGet then displays the full version number in the applicable UI, leaving consumers to interpret the meaning for themselves.</span></span>

<span data-ttu-id="a8180-133">Bu göz önünde bulundurularak, aşağıdaki gibi tanınan adlandırma kurallarını izlemek genellikle yararlı olur:</span><span class="sxs-lookup"><span data-stu-id="a8180-133">With this in mind, it's generally good to follow recognized naming conventions such as the following:</span></span>

- <span data-ttu-id="a8180-134">`-alpha`: Genellikle süren iş ve deneme için kullanılan alfa sürümü</span><span class="sxs-lookup"><span data-stu-id="a8180-134">`-alpha`: Alpha release, typically used for work-in-progress and experimentation</span></span>
- <span data-ttu-id="a8180-135">`-beta`: Beta sürümü, genellikle bir sonraki planlı yayın için bir özelliktir, ancak bilinen hatalar içerebilir.</span><span class="sxs-lookup"><span data-stu-id="a8180-135">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="a8180-136">`-rc`: Yayın adayı, genellikle önemli hatalar oluşmadığı takdirde son derece nihai (kararlı) bir sürümdür.</span><span class="sxs-lookup"><span data-stu-id="a8180-136">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="a8180-137">NuGet 4.3.0 +, ' de olduğu gibi nokta gösterimi ile yayın öncesi numaralarını destekleyen [anlamsal sürüm oluşturma v 2.0.0](https://semver.org/spec/v2.0.0.html)'yi destekler `1.0.1-build.23` .</span><span class="sxs-lookup"><span data-stu-id="a8180-137">NuGet 4.3.0+ supports [Semantic Versioning v2.0.0](https://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in `1.0.1-build.23`.</span></span> <span data-ttu-id="a8180-138">Nokta gösterimi 4.3.0 öncesi NuGet sürümleriyle desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="a8180-138">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="a8180-139">NuGet 'in önceki sürümlerinde, gibi bir form kullanabilirsiniz, `1.0.1-build23` ancak bu her zaman yayın öncesi sürüm olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="a8180-139">In earlier versions of NuGet, you could use a form like `1.0.1-build23` but this was always considered a pre-release version.</span></span>

<span data-ttu-id="a8180-140">Ancak kullandığınız son ekler, NuGet 'e ters alfabetik sırada öncelik verecektir:</span><span class="sxs-lookup"><span data-stu-id="a8180-140">Whatever suffixes you use, however, NuGet will give them precedence in reverse alphabetical order:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta.12
    1.0.1-beta.5
    1.0.1-beta
    1.0.1-alpha.2
    1.0.1-alpha

<span data-ttu-id="a8180-141">Gösterildiği gibi, herhangi bir sonek olmadan sürüm, yayın öncesi sürümlerden her zaman öncelikli olur.</span><span class="sxs-lookup"><span data-stu-id="a8180-141">As shown, the version without any suffix will always take precedence over pre-release versions.</span></span>

<span data-ttu-id="a8180-142">Önde gelen 0s, semver2 için gerekli değildir, ancak eski sürüm şemasıyla bulunur.</span><span class="sxs-lookup"><span data-stu-id="a8180-142">Leading 0s are not needed with semver2, but they are with the old version schema.</span></span> <span data-ttu-id="a8180-143">Çift basamaklı sayılar (veya daha fazla) kullanan serbest bırakma etiketleriyle sayısal sonekler kullanırsanız, sayılar daha büyük olduğunda doğru sıraladıklarından emin olmak için Beta. 01 ve Beta. 05 ' de önde gelen sıfırları kullanın.</span><span class="sxs-lookup"><span data-stu-id="a8180-143">If you use numerical suffixes with pre-release tags that might use double-digit numbers (or more), use leading zeroes as in beta.01 and beta.05 to ensure that they sort correctly when the numbers get larger.</span></span> <span data-ttu-id="a8180-144">Bu öneri yalnızca eski sürüm şeması için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="a8180-144">This recommendation only applies to the old version schema.</span></span>
