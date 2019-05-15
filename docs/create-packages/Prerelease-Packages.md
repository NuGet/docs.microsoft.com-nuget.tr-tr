---
title: NuGet paketlerini de yayın öncesi sürümleri
description: Yayın öncesi paketleri oluşturmaya yönelik Kılavuzlar
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 845f0ea84bcb92fedf9e5f4fb2b1deee1462a004
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610490"
---
# <a name="building-pre-release-packages"></a><span data-ttu-id="087a2-103">Yayın öncesi paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="087a2-103">Building pre-release packages</span></span>

<span data-ttu-id="087a2-104">Güncelleştirilmiş bir paketin yeni bir sürüm numarasına sahip yayın her birinin ", örneğin Visual Studio'da Paket Yöneticisi UI gösterildiği gibi en son kararlı sürüm" olarak NuGet göz önünde bulundurur:</span><span class="sxs-lookup"><span data-stu-id="087a2-104">Whenever you release an updated package with a new version number, NuGet considers that one as the "latest stable release" as shown, for example in the Package Manager UI within Visual Studio:</span></span>

![Paket Yöneticisi UI en son kararlı sürüm gösteriliyor](media/Prerelease_01-LatestStable.png)

<span data-ttu-id="087a2-106">Kararlı bir sürüm üretimde kullanılacak güvenilir olarak değerlendirilmeyen biridir.</span><span class="sxs-lookup"><span data-stu-id="087a2-106">A stable release is one that's considered reliable enough to be used in production.</span></span> <span data-ttu-id="087a2-107">En son kararlı sürüm ayrıca paket güncelleştirmesi veya paket geri yükleme sırasında yüklenecek olan bölümdür (açıklanan kısıtlamalarına tabi [Reinstalling ve paketlerin güncelleştirilmesi](../consume-packages/reinstalling-and-updating-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="087a2-107">The latest stable release is also the one that will be installed as a package update or during package restore (subject to constraints as described in [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)).</span></span>

<span data-ttu-id="087a2-108">Yazılım sürüm yaşam döngüsünü desteklemek için NuGet 1.6 ve üzeri için yayın öncesi paketleri dağıtımını burada sürüm numarası gibi semantic versioning soneki içerir sağlıyor `-alpha`, `-beta`, veya `-rc`.</span><span class="sxs-lookup"><span data-stu-id="087a2-108">To support the software release lifecycle, NuGet 1.6 and later allows for the distribution of pre-release packages, where the version number includes a semantic versioning suffix such as `-alpha`, `-beta`, or `-rc`.</span></span> <span data-ttu-id="087a2-109">Daha fazla bilgi için [Paket sürümü oluşturma](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="087a2-109">For more information, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>

<span data-ttu-id="087a2-110">Aşağıdaki yöntemlerden birini kullanarak bu tür sürümleri belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="087a2-110">You can specify such versions using one of the following ways:</span></span>

- <span data-ttu-id="087a2-111">**Projeniz kullanıyorsa [ `PackageReference` ](../consume-packages/package-references-in-project-files.md)** : anlamsal Sürüm soneki dahil `.csproj` dosyanın [ `PackageVersion` ](/dotnet/core/tools/csproj.md#packageversion) öğesi:</span><span class="sxs-lookup"><span data-stu-id="087a2-111">**If your project uses [`PackageReference`](../consume-packages/package-references-in-project-files.md)**: include the semantic version suffix in the `.csproj` file's [`PackageVersion`](/dotnet/core/tools/csproj.md#packageversion) element:</span></span>

    ```xml
    <PropertyGroup>
        <PackageVersion>1.0.1-alpha</PackageVersion>
    </PropertyGroup>
    ```

- <span data-ttu-id="087a2-112">**Projenizin varsa bir [ `packages.config` ](../reference/packages-config.md) dosya**: anlamsal Sürüm soneki dahil [ `.nuspec` ](../reference/nuspec.md) dosyanın [ `version` ](../reference/nuspec.md#version) öğe:</span><span class="sxs-lookup"><span data-stu-id="087a2-112">**If your project has a [`packages.config`](../reference/packages-config.md) file**: include the semantic version suffix in the [`.nuspec`](../reference/nuspec.md) file's [`version`](../reference/nuspec.md#version) element:</span></span>

    ```xml
    <version>1.0.1-alpha</version>
    ```

<span data-ttu-id="087a2-113">Kararlı bir sürüm hazır olduğunuzda, yalnızca soneki kaldırın ve paketin tüm yayın öncesi sürümlere göre önceliklidir.</span><span class="sxs-lookup"><span data-stu-id="087a2-113">When you're ready to release a stable version, just remove the suffix and the package takes precedence over any pre-release versions.</span></span> <span data-ttu-id="087a2-114">Yeniden bakın [Paket sürümü oluşturma](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="087a2-114">Again, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>

## <a name="installing-and-updating-pre-release-packages"></a><span data-ttu-id="087a2-115">Yükleme ve güncelleştirme yayın öncesi paketleri</span><span class="sxs-lookup"><span data-stu-id="087a2-115">Installing and updating pre-release packages</span></span>

<span data-ttu-id="087a2-116">Varsayılan olarak, NuGet paketleri ile çalışırken, yayın öncesi sürümleri içermez, ancak bu davranışı şu şekilde değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="087a2-116">By default, NuGet does not include pre-release versions when working with packages, but you can change this behavior as follows:</span></span>

- <span data-ttu-id="087a2-117">**Visual Studio'da Paket Yöneticisi UI**: İçinde **NuGet paketlerini Yönet** kullanıcı Arabirimi, onay **ön sürümü dahil et** kutusunda:</span><span class="sxs-lookup"><span data-stu-id="087a2-117">**Package Manager UI in Visual Studio**: In the **Manage NuGet Packages** UI, check the **Include prerelease** box:</span></span>

    ![Visual Studio'da INCLUDE Ön onay kutusu](media/Prerelease_02-CheckPrerelease.png)

    <span data-ttu-id="087a2-119">Ayarlama ya da bu kutuyu temizleyerek Paket Yöneticisi UI ve yükleyebileceğiniz kullanılabilir sürümlerin listesini yeniler.</span><span class="sxs-lookup"><span data-stu-id="087a2-119">Setting or clearing this box will refresh the Package Manager UI and the list of available versions you can install.</span></span>

- <span data-ttu-id="087a2-120">**Paket Yöneticisi Konsolu**: Kullanım `-IncludePrerelease` anahtarı ile `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, ve `Update-Package` komutları.</span><span class="sxs-lookup"><span data-stu-id="087a2-120">**Package Manager Console**: Use the `-IncludePrerelease` switch with the `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, and `Update-Package` commands.</span></span> <span data-ttu-id="087a2-121">Başvurmak [PowerShell başvurusu](../tools/powershell-reference.md).</span><span class="sxs-lookup"><span data-stu-id="087a2-121">Refer to the [PowerShell Reference](../tools/powershell-reference.md).</span></span>

- <span data-ttu-id="087a2-122">**NuGet CLI**: Kullanım `-prerelease` anahtarı ile `install`, `update`, `delete`, ve `mirror` komutları.</span><span class="sxs-lookup"><span data-stu-id="087a2-122">**NuGet CLI**: Use the `-prerelease` switch with the `install`, `update`, `delete`, and `mirror` commands.</span></span> <span data-ttu-id="087a2-123">Başvurmak [NuGet CLI başvurusu](../tools/nuget-exe-cli-reference.md)</span><span class="sxs-lookup"><span data-stu-id="087a2-123">Refer to the [NuGet CLI reference](../tools/nuget-exe-cli-reference.md)</span></span>

## <a name="semantic-versioning"></a><span data-ttu-id="087a2-124">Semantic versioning</span><span class="sxs-lookup"><span data-stu-id="087a2-124">Semantic versioning</span></span>

<span data-ttu-id="087a2-125">[Semantic Versioning veya SemVer kuralı](http://semver.org/spec/v1.0.0.html) arka plandaki kod anlamını iletmek için sürüm numaraları dizelerde nasıl açıklar.</span><span class="sxs-lookup"><span data-stu-id="087a2-125">The [Semantic Versioning or SemVer convention](http://semver.org/spec/v1.0.0.html) describes how to utilize strings in version numbers to convey the meaning of the underlying code.</span></span>

<span data-ttu-id="087a2-126">Bu kural, her sürüm üç bölümden `Major.Minor.Patch`, aşağıdaki anlama sahip:</span><span class="sxs-lookup"><span data-stu-id="087a2-126">In this convention, each version has three parts, `Major.Minor.Patch`, with the following meaning:</span></span>

- <span data-ttu-id="087a2-127">`Major`: Yeni değişiklikler</span><span class="sxs-lookup"><span data-stu-id="087a2-127">`Major`: Breaking changes</span></span>
- <span data-ttu-id="087a2-128">`Minor`: Geriye dönük olarak uyumlu ancak yeni özellikler</span><span class="sxs-lookup"><span data-stu-id="087a2-128">`Minor`: New features, but backwards compatible</span></span>
- <span data-ttu-id="087a2-129">`Patch`: Geriye dönük yalnızca uyumlu hata düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="087a2-129">`Patch`: Backwards compatible bug fixes only</span></span>

<span data-ttu-id="087a2-130">Yayın öncesi sürümleri düzeltme numarası sonra kısa çizgi ve bir dize ekleyerek belirtilir.</span><span class="sxs-lookup"><span data-stu-id="087a2-130">Pre-release versions are then denoted by appending a hyphen and a string after the patch number.</span></span> <span data-ttu-id="087a2-131">Kullanabileceğiniz teknik terimlerle açıklamak gerekirse, *herhangi* kısa çizgi ve NuGet paketi yayın öncesi değerlendirir sonra dize.</span><span class="sxs-lookup"><span data-stu-id="087a2-131">Technically speaking, you can use *any* string after the hyphen and NuGet will treat the package as pre-release.</span></span> <span data-ttu-id="087a2-132">NuGet, kendileri için anlam yorumlama tüketicilerin bırakarak geçerli kullanıcı arabiriminde, daha sonra tam sürüm numarası görüntüler.</span><span class="sxs-lookup"><span data-stu-id="087a2-132">NuGet then displays the full version number in the applicable UI, leaving consumers to interpret the meaning for themselves.</span></span>

<span data-ttu-id="087a2-133">Bunu aklınızda, aşağıdaki gibi tanınmış adlandırma kurallarına uymuyor genellikle iyi olur:</span><span class="sxs-lookup"><span data-stu-id="087a2-133">With this in mind, it's generally good to follow recognized naming conventions such as the following:</span></span>

- <span data-ttu-id="087a2-134">`-alpha`: Genellikle, iş ilerleme ve deneme için kullanılan alfa sürümü</span><span class="sxs-lookup"><span data-stu-id="087a2-134">`-alpha`: Alpha release, typically used for work-in-progress and experimentation</span></span>
- <span data-ttu-id="087a2-135">`-beta`: Beta sürümü, genellikle bir özellik için bir sonraki tam sürüm planlı, ancak bilinen hataları içerebilir.</span><span class="sxs-lookup"><span data-stu-id="087a2-135">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="087a2-136">`-rc`: Sürüm Adayı, genellikle büyük olasılıkla son sürüm (stable) sürece önemli hatalar ortaya çıkmaya başladı.</span><span class="sxs-lookup"><span data-stu-id="087a2-136">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="087a2-137">NuGet 4.3.0+ destekler [Semantic Versioning v2.0.0](http://semver.org/spec/v2.0.0.html), olarak nokta gösterimi, yayın öncesi sürüm numaralarıyla destekleyen `1.0.1-build.23`.</span><span class="sxs-lookup"><span data-stu-id="087a2-137">NuGet 4.3.0+ supports [Semantic Versioning v2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in `1.0.1-build.23`.</span></span> <span data-ttu-id="087a2-138">Nokta gösterimi 4.3.0 önce NuGet sürümü ile desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="087a2-138">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="087a2-139">NuGet önceki sürümlerinde, bir form gibi kullanabileceğinizi `1.0.1-build23` ancak bu her zaman yayın öncesi bir sürümü kabul.</span><span class="sxs-lookup"><span data-stu-id="087a2-139">In earlier versions of NuGet, you could use a form like `1.0.1-build23` but this was always considered a pre-release version.</span></span>

<span data-ttu-id="087a2-140">Ancak kullanmak istediğiniz sonekleri NuGet bunları öncelik ters alfabetik sırada verecektir:</span><span class="sxs-lookup"><span data-stu-id="087a2-140">Whatever suffixes you use, however, NuGet will give them precedence in reverse alphabetical order:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta12
    1.0.1-beta05
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha

<span data-ttu-id="087a2-141">Gösterildiği gibi tüm soneki olmadan sürümü her zaman yayın öncesi sürümleri üzerinde öncelikli olur.</span><span class="sxs-lookup"><span data-stu-id="087a2-141">As shown, the version without any suffix will always take precedence over pre-release versions.</span></span> <span data-ttu-id="087a2-142">Ayrıca çift haneli kullanıyor olabileceğiniz yayın öncesi etiketlerle sayısal sonekleri kullanırsanız sayıları (veya daha fazla), 2f3b beta01 ve beta05 olduğu gibi doğru sayı daha büyük ulaştıklarında sıralaması emin olmak için unutmayın.</span><span class="sxs-lookup"><span data-stu-id="087a2-142">Note also that if you use numerical suffixes with pre-release tags that might use double-digit numbers (or more), use leading zeroes as in beta01 and beta05 to ensure that they sort correctly when the numbers get larger.</span></span>
