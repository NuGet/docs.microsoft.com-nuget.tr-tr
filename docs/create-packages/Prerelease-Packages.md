---
title: NuGet paketlerini de yayın öncesi sürümleri
description: Yayın öncesi paketleri oluşturmaya yönelik Kılavuzlar
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 696f51905198defdbfd475ba7d010ac3e27ac557
ms.sourcegitcommit: 3fc93f7a64be040699fe12125977dd25a7948470
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/29/2019
ms.locfileid: "64877937"
---
# <a name="building-pre-release-packages"></a><span data-ttu-id="0b4c3-103">Yayın öncesi paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="0b4c3-103">Building pre-release packages</span></span>

<span data-ttu-id="0b4c3-104">Güncelleştirilmiş bir paketin yeni bir sürüm numarasına sahip yayın her birinin ", örneğin Visual Studio'da Paket Yöneticisi UI gösterildiği gibi en son kararlı sürüm" olarak NuGet göz önünde bulundurur:</span><span class="sxs-lookup"><span data-stu-id="0b4c3-104">Whenever you release an updated package with a new version number, NuGet considers that one as the "latest stable release" as shown, for example in the Package Manager UI within Visual Studio:</span></span>

![Paket Yöneticisi UI en son kararlı sürüm gösteriliyor](media/Prerelease_01-LatestStable.png)

<span data-ttu-id="0b4c3-106">Kararlı bir sürüm üretimde kullanılacak güvenilir olarak değerlendirilmeyen biridir.</span><span class="sxs-lookup"><span data-stu-id="0b4c3-106">A stable release is one that's considered reliable enough to be used in production.</span></span> <span data-ttu-id="0b4c3-107">En son kararlı sürüm ayrıca paket güncelleştirmesi veya paket geri yükleme sırasında yüklenecek olan bölümdür (açıklanan kısıtlamalarına tabi [Reinstalling ve paketlerin güncelleştirilmesi](../consume-packages/reinstalling-and-updating-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="0b4c3-107">The latest stable release is also the one that will be installed as a package update or during package restore (subject to constraints as described in [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)).</span></span>

<span data-ttu-id="0b4c3-108">Yazılım sürüm yaşam döngüsünü desteklemek için NuGet 1.6 ve üzeri için yayın öncesi paketleri dağıtımını burada sürüm numarası gibi semantic versioning soneki içerir sağlıyor `-alpha`, `-beta`, veya `-rc`.</span><span class="sxs-lookup"><span data-stu-id="0b4c3-108">To support the software release lifecycle, NuGet 1.6 and later allows for the distribution of pre-release packages, where the version number includes a semantic versioning suffix such as `-alpha`, `-beta`, or `-rc`.</span></span> <span data-ttu-id="0b4c3-109">Daha fazla bilgi için [Paket sürümü oluşturma](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="0b4c3-109">For more information, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>

<span data-ttu-id="0b4c3-110">Bu tür sürümleri üç yolla belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0b4c3-110">You can specify such versions in three ways:</span></span>

- <span data-ttu-id="0b4c3-111">`.nuspec` Dosya: anlamsal Sürüm soneki dahil `version` öğesi:</span><span class="sxs-lookup"><span data-stu-id="0b4c3-111">`.nuspec` file: include the semantic version suffix in the `version` element:</span></span>

    ```xml
    <version>1.0.1-alpha</version>
    ```

- <span data-ttu-id="0b4c3-112">`.csproj` Dosya: anlamsal Sürüm soneki dahil `PackageVersion` öğesi:</span><span class="sxs-lookup"><span data-stu-id="0b4c3-112">`.csproj` file: include the semantic version suffix in the `PackageVersion` element:</span></span>

    ```xml
    <PropertyGroup>
        <PackageVersion>1.0.1-alpha</PackageVersion>
    </PropertyGroup>
    ```

- <span data-ttu-id="0b4c3-113">Derleme özniteliklerinin: sürümüyle belirtin `AssemblyInformationalVersionAttribute`:</span><span class="sxs-lookup"><span data-stu-id="0b4c3-113">Assembly attributes: specify the version using `AssemblyInformationalVersionAttribute`:</span></span>

    ```cs
    [assembly: AssemblyInformationalVersion("1.0.1-beta")]
    ```

    <span data-ttu-id="0b4c3-114">Bu değer yerine belirtilen bir NuGet alır `AssemblyVersion` semantic versioning desteklemeyen özniteliği.</span><span class="sxs-lookup"><span data-stu-id="0b4c3-114">NuGet picks up this value instead of the one specified in the `AssemblyVersion` attribute, which does not support semantic versioning.</span></span>

<span data-ttu-id="0b4c3-115">Kararlı bir sürüm hazır olduğunuzda, yalnızca soneki kaldırın ve paketin tüm yayın öncesi sürümlere göre önceliklidir.</span><span class="sxs-lookup"><span data-stu-id="0b4c3-115">When you’re ready to release a stable version, just remove the suffix and the package takes precedence over any pre-release versions.</span></span> <span data-ttu-id="0b4c3-116">Yeniden bakın [Paket sürümü oluşturma](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="0b4c3-116">Again, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>

## <a name="installing-and-updating-pre-release-packages"></a><span data-ttu-id="0b4c3-117">Yükleme ve güncelleştirme yayın öncesi paketleri</span><span class="sxs-lookup"><span data-stu-id="0b4c3-117">Installing and updating pre-release packages</span></span>

<span data-ttu-id="0b4c3-118">Varsayılan olarak, NuGet paketleri ile çalışırken, yayın öncesi sürümleri içermez, ancak bu davranışı şu şekilde değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0b4c3-118">By default, NuGet does not include pre-release versions when working with packages, but you can change this behavior as follows:</span></span>

- <span data-ttu-id="0b4c3-119">**Visual Studio'da Paket Yöneticisi UI**: İçinde **NuGet paketlerini Yönet** kullanıcı Arabirimi, onay **ön sürümü dahil et** kutusunda:</span><span class="sxs-lookup"><span data-stu-id="0b4c3-119">**Package Manager UI in Visual Studio**: In the **Manage NuGet Packages** UI, check the **Include prerelease** box:</span></span>

    ![Visual Studio'da INCLUDE Ön onay kutusu](media/Prerelease_02-CheckPrerelease.png)

    <span data-ttu-id="0b4c3-121">Ayarlama ya da bu kutuyu temizleyerek Paket Yöneticisi UI ve yükleyebileceğiniz kullanılabilir sürümlerin listesini yeniler.</span><span class="sxs-lookup"><span data-stu-id="0b4c3-121">Setting or clearing this box will refresh the Package Manager UI and the list of available versions you can install.</span></span>

- <span data-ttu-id="0b4c3-122">**Paket Yöneticisi Konsolu**: Kullanım `-IncludePrerelease` anahtarı ile `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, ve `Update-Package` komutları.</span><span class="sxs-lookup"><span data-stu-id="0b4c3-122">**Package Manager Console**: Use the `-IncludePrerelease` switch with the `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, and `Update-Package` commands.</span></span> <span data-ttu-id="0b4c3-123">Başvurmak [PowerShell başvurusu](../tools/powershell-reference.md).</span><span class="sxs-lookup"><span data-stu-id="0b4c3-123">Refer to the [PowerShell Reference](../tools/powershell-reference.md).</span></span>

- <span data-ttu-id="0b4c3-124">**NuGet CLI**: Kullanım `-prerelease` anahtarı ile `install`, `update`, `delete`, ve `mirror` komutları.</span><span class="sxs-lookup"><span data-stu-id="0b4c3-124">**NuGet CLI**: Use the `-prerelease` switch with the `install`, `update`, `delete`, and `mirror` commands.</span></span> <span data-ttu-id="0b4c3-125">Başvurmak [NuGet CLI başvurusu](../tools/nuget-exe-cli-reference.md)</span><span class="sxs-lookup"><span data-stu-id="0b4c3-125">Refer to the [NuGet CLI reference](../tools/nuget-exe-cli-reference.md)</span></span>

## <a name="semantic-versioning"></a><span data-ttu-id="0b4c3-126">Semantic versioning</span><span class="sxs-lookup"><span data-stu-id="0b4c3-126">Semantic versioning</span></span>

<span data-ttu-id="0b4c3-127">[Semantic Versioning veya SemVer kuralı](http://semver.org/spec/v1.0.0.html) arka plandaki kod anlamını iletmek için sürüm numaraları dizelerde nasıl açıklar.</span><span class="sxs-lookup"><span data-stu-id="0b4c3-127">The [Semantic Versioning or SemVer convention](http://semver.org/spec/v1.0.0.html) describes how to utilize strings in version numbers to convey the meaning of the underlying code.</span></span>

<span data-ttu-id="0b4c3-128">Bu kural, her sürüm üç bölümden `Major.Minor.Patch`, aşağıdaki anlama sahip:</span><span class="sxs-lookup"><span data-stu-id="0b4c3-128">In this convention, each version has three parts, `Major.Minor.Patch`, with the following meaning:</span></span>

- <span data-ttu-id="0b4c3-129">`Major`: Yeni değişiklikler</span><span class="sxs-lookup"><span data-stu-id="0b4c3-129">`Major`: Breaking changes</span></span>
- <span data-ttu-id="0b4c3-130">`Minor`: Geriye dönük olarak uyumlu ancak yeni özellikler</span><span class="sxs-lookup"><span data-stu-id="0b4c3-130">`Minor`: New features, but backwards compatible</span></span>
- <span data-ttu-id="0b4c3-131">`Patch`: Geriye dönük yalnızca uyumlu hata düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="0b4c3-131">`Patch`: Backwards compatible bug fixes only</span></span>

<span data-ttu-id="0b4c3-132">Yayın öncesi sürümleri düzeltme numarası sonra kısa çizgi ve bir dize ekleyerek belirtilir.</span><span class="sxs-lookup"><span data-stu-id="0b4c3-132">Pre-release versions are then denoted by appending a hyphen and a string after the patch number.</span></span> <span data-ttu-id="0b4c3-133">Kullanabileceğiniz teknik terimlerle açıklamak gerekirse, *herhangi* kısa çizgi ve NuGet paketi yayın öncesi değerlendirir sonra dize.</span><span class="sxs-lookup"><span data-stu-id="0b4c3-133">Technically speaking, you can use *any* string after the hyphen and NuGet will treat the package as pre-release.</span></span> <span data-ttu-id="0b4c3-134">NuGet, kendileri için anlam yorumlama tüketicilerin bırakarak geçerli kullanıcı arabiriminde, daha sonra tam sürüm numarası görüntüler.</span><span class="sxs-lookup"><span data-stu-id="0b4c3-134">NuGet then displays the full version number in the applicable UI, leaving consumers to interpret the meaning for themselves.</span></span>

<span data-ttu-id="0b4c3-135">Bunu aklınızda, aşağıdaki gibi tanınmış adlandırma kurallarına uymuyor genellikle iyi olur:</span><span class="sxs-lookup"><span data-stu-id="0b4c3-135">With this in mind, it's generally good to follow recognized naming conventions such as the following:</span></span>

- <span data-ttu-id="0b4c3-136">`-alpha`: Genellikle, iş ilerleme ve deneme için kullanılan alfa sürümü</span><span class="sxs-lookup"><span data-stu-id="0b4c3-136">`-alpha`: Alpha release, typically used for work-in-progress and experimentation</span></span>
- <span data-ttu-id="0b4c3-137">`-beta`: Beta sürümü, genellikle bir özellik için bir sonraki tam sürüm planlı, ancak bilinen hataları içerebilir.</span><span class="sxs-lookup"><span data-stu-id="0b4c3-137">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="0b4c3-138">`-rc`: Sürüm Adayı, genellikle büyük olasılıkla son sürüm (stable) sürece önemli hatalar ortaya çıkmaya başladı.</span><span class="sxs-lookup"><span data-stu-id="0b4c3-138">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="0b4c3-139">NuGet 4.3.0+ destekler [Semantic Versioning v2.0.0](http://semver.org/spec/v2.0.0.html), olarak nokta gösterimi, yayın öncesi sürüm numaralarıyla destekleyen `1.0.1-build.23`.</span><span class="sxs-lookup"><span data-stu-id="0b4c3-139">NuGet 4.3.0+ supports [Semantic Versioning v2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in `1.0.1-build.23`.</span></span> <span data-ttu-id="0b4c3-140">Nokta gösterimi 4.3.0 önce NuGet sürümü ile desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="0b4c3-140">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="0b4c3-141">NuGet önceki sürümlerinde, bir form gibi kullanabileceğinizi `1.0.1-build23` ancak bu her zaman yayın öncesi bir sürümü kabul.</span><span class="sxs-lookup"><span data-stu-id="0b4c3-141">In earlier versions of NuGet, you could use a form like `1.0.1-build23` but this was always considered a pre-release version.</span></span>

<span data-ttu-id="0b4c3-142">Ancak kullanmak istediğiniz sonekleri NuGet bunları öncelik ters alfabetik sırada verecektir:</span><span class="sxs-lookup"><span data-stu-id="0b4c3-142">Whatever suffixes you use, however, NuGet will give them precedence in reverse alphabetical order:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta12
    1.0.1-beta05
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha

<span data-ttu-id="0b4c3-143">Gösterildiği gibi tüm soneki olmadan sürümü her zaman yayın öncesi sürümleri üzerinde öncelikli olur.</span><span class="sxs-lookup"><span data-stu-id="0b4c3-143">As shown, the version without any suffix will always take precedence over pre-release versions.</span></span> <span data-ttu-id="0b4c3-144">Ayrıca çift haneli kullanıyor olabileceğiniz yayın öncesi etiketlerle sayısal sonekleri kullanırsanız sayıları (veya daha fazla), 2f3b beta01 ve beta05 olduğu gibi doğru sayı daha büyük ulaştıklarında sıralaması emin olmak için unutmayın.</span><span class="sxs-lookup"><span data-stu-id="0b4c3-144">Note also that if you use numerical suffixes with pre-release tags that might use double-digit numbers (or more), use leading zeroes as in beta01 and beta05 to ensure that they sort correctly when the numbers get larger.</span></span>
