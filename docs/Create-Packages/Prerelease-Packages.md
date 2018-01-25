---
title: "NuGet paketlerini sürümlerde sürüm öncesi | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/14/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Yayın öncesi paketleri oluşturmak için yönergeler"
keywords: "sürüm oluşturma, NuGet paketini sürüm oluşturma, NuGet yayın öncesi sürümler, NuGet ön sürüm paketlerini, Önizleme paketi sürümleri, RC paketi sürümleri, Beta paketi sürümleri, NuGet anlamsal sürüm oluşturma"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f07b4a0428685b036640a7153190fd8454885608
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2018
---
# <a name="building-pre-release-packages"></a><span data-ttu-id="5b3ef-104">Yayın öncesi paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="5b3ef-104">Building pre-release packages</span></span>

<span data-ttu-id="5b3ef-105">Güncelleştirilmiş bir paketin yeni bir sürüm numarası olan yayın olduğunda, bir ", örneğin Paket Yöneticisi kullanıcı arabiriminde Visual Studio içinde gösterildiği gibi en son kararlı sürümü" olarak NuGet göz önünde bulundurur:</span><span class="sxs-lookup"><span data-stu-id="5b3ef-105">Whenever you release an updated package with a new version number, NuGet considers that one as the "latest stable release" as shown, for example in the Package Manager UI within Visual Studio:</span></span>

![Paket Yöneticisi en son kararlı sürümü gösteren UI](media/Prerelease_01-LatestStable.png)

<span data-ttu-id="5b3ef-107">Durağan sürümü üretimde kullanılacak güvenilir olarak görülmeyen biridir.</span><span class="sxs-lookup"><span data-stu-id="5b3ef-107">A stable release is one that's considered reliable enough to be used in production.</span></span> <span data-ttu-id="5b3ef-108">En son kararlı sürümü de bir paket güncelleştirmesi veya paket geri yükleme sırasında yüklenecek sunucudur (açıklandığı gibi kısıtlamaları tabi [Reinstalling ve paketleri güncelleştiriliyor](../consume-packages/reinstalling-and-updating-packages.md)).</span><span class="sxs-lookup"><span data-stu-id="5b3ef-108">The latest stable release is also the one that will be installed as a package update or during package restore (subject to constraints as described in [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)).</span></span>

<span data-ttu-id="5b3ef-109">Yazılım sürüm yaşam döngüsü desteklemek için NuGet 1.6 ve üzeri yayın öncesi paket, dağıtım için burada sürüm numarası gibi bir anlamsal sürüm oluşturma soneki içerir verir `-alpha`, `-beta`, veya `-rc`.</span><span class="sxs-lookup"><span data-stu-id="5b3ef-109">To support the software release lifecycle, NuGet 1.6 and later allows for the distribution of pre-release packages, where the version number includes a semantic versioning suffix such as `-alpha`, `-beta`, or `-rc`.</span></span> <span data-ttu-id="5b3ef-110">Daha fazla bilgi için bkz: [paket sürüm](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="5b3ef-110">For more information, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>

<span data-ttu-id="5b3ef-111">Bu tür sürümlerini iki yolla belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5b3ef-111">You can specify such versions in two ways:</span></span>

- <span data-ttu-id="5b3ef-112">`.nuspec`Dosya: semantik Sürüm soneki dahil `version` öğe:</span><span class="sxs-lookup"><span data-stu-id="5b3ef-112">`.nuspec` file: include the semantic version suffix in the `version` element:</span></span>

    ```xml
    <version>1.0.1-alpha</version>
    ```

- <span data-ttu-id="5b3ef-113">Derleme özniteliklerinin: Visual Studio projesi paketinden oluştururken (`.csproj` veya `.vbproj`), kullanın `AssemblyInformationalVersionAttribute` sürüm belirtmek için:</span><span class="sxs-lookup"><span data-stu-id="5b3ef-113">Assembly attributes: when building a package from a Visual Studio project (`.csproj` or `.vbproj`), use the `AssemblyInformationalVersionAttribute` to specify the version:</span></span>

    ```cs
    [assembly: AssemblyInformationalVersion("1.0.1-beta")]
    ```

    <span data-ttu-id="5b3ef-114">Bu değer yerine belirtilen bir NuGet alır `AssemblyVersion` anlamsal sürüm oluşturma desteklemiyor özniteliği.</span><span class="sxs-lookup"><span data-stu-id="5b3ef-114">NuGet picks up this value instead of the one specified in the `AssemblyVersion` attribute, which does not support semantic versioning.</span></span>

<span data-ttu-id="5b3ef-115">Kararlı bir sürümünü hazır olduğunuzda, yalnızca soneki kaldırın ve paketin tüm yayın öncesi sürümlerini göre önceliklidir.</span><span class="sxs-lookup"><span data-stu-id="5b3ef-115">When you’re ready to release a stable version, just remove the suffix and the package takes precedence over any pre-release versions.</span></span> <span data-ttu-id="5b3ef-116">Yeniden bkz [paket sürüm](../reference/package-versioning.md#pre-release-versions).</span><span class="sxs-lookup"><span data-stu-id="5b3ef-116">Again, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>

## <a name="installing-and-updating-pre-release-packages"></a><span data-ttu-id="5b3ef-117">Yükleme ve ön sürüm paketlerini güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="5b3ef-117">Installing and updating pre-release packages</span></span>

<span data-ttu-id="5b3ef-118">Varsayılan olarak, NuGet paketleri ile çalışırken, yayın öncesi sürümleri içermiyor, ancak bu davranışı aşağıdaki gibi değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5b3ef-118">By default, NuGet does not include pre-release versions when working with packages, but you can change this behavior as follows:</span></span>

- <span data-ttu-id="5b3ef-119">**Visual Studio'da Paket Yöneticisi kullanıcı Arabirimi**: içinde **NuGet paketlerini Yönet** UI, onay **dahil et** kutusunda:</span><span class="sxs-lookup"><span data-stu-id="5b3ef-119">**Package Manager UI in Visual Studio**: In the **Manage NuGet Packages** UI, check the **Include prerelease** box:</span></span>

    ![Visual Studio INCLUDE Ön onay kutusu](media/Prerelease_02-CheckPrerelease.png)

    <span data-ttu-id="5b3ef-121">Ayarlama ya da bu kutusunu temizleyerek Paket Yöneticisi kullanıcı Arabirimi ve yükleyebileceğiniz kullanılabilir sürümlerin listesini yeniler.</span><span class="sxs-lookup"><span data-stu-id="5b3ef-121">Setting or clearing this box will refresh the Package Manager UI and the list of available versions you can install.</span></span>

- <span data-ttu-id="5b3ef-122">**Paket Yöneticisi Konsolu**: kullanım `-IncludePrerelease` anahtarı ile `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, ve `Update-Package` komutları.</span><span class="sxs-lookup"><span data-stu-id="5b3ef-122">**Package Manager Console**: Use the `-IncludePrerelease` switch with the `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, and `Update-Package` commands.</span></span> <span data-ttu-id="5b3ef-123">Başvurmak [PowerShell başvurusu](../tools/powershell-reference.md).</span><span class="sxs-lookup"><span data-stu-id="5b3ef-123">Refer to the [PowerShell Reference](../tools/powershell-reference.md).</span></span>

- <span data-ttu-id="5b3ef-124">**NuGet CLI**: kullanım `-prerelease` anahtarı ile `install`, `update`, `delete`, ve `mirror` komutları.</span><span class="sxs-lookup"><span data-stu-id="5b3ef-124">**NuGet CLI**: Use the `-prerelease` switch with the `install`, `update`, `delete`, and `mirror` commands.</span></span> <span data-ttu-id="5b3ef-125">Başvurmak [NuGet CLI başvurusu](../tools/nuget-exe-cli-reference.md)</span><span class="sxs-lookup"><span data-stu-id="5b3ef-125">Refer to the [NuGet CLI reference](../tools/nuget-exe-cli-reference.md)</span></span>

## <a name="semantic-versioning"></a><span data-ttu-id="5b3ef-126">Anlamsal sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="5b3ef-126">Semantic versioning</span></span>

<span data-ttu-id="5b3ef-127">[Anlamsal sürüm oluşturma veya SemVer kuralı](http://semver.org/spec/v1.0.0.html) iletmek için sürüm numaraları dizelerde kullanmaya açıklar arka plandaki kod anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="5b3ef-127">The [Semantic Versioning or SemVer convention](http://semver.org/spec/v1.0.0.html) describes how to utilize strings in version numbers to convey they meaning of the underlying code.</span></span>

<span data-ttu-id="5b3ef-128">Bu kural, her üç bölümden sürümde `Major.Minor.Patch`, aşağıdaki anlamı ile:</span><span class="sxs-lookup"><span data-stu-id="5b3ef-128">In this convention, each version has three parts, `Major.Minor.Patch`, with the following meaning:</span></span>

- <span data-ttu-id="5b3ef-129">`Major`: Yeni değişiklikler</span><span class="sxs-lookup"><span data-stu-id="5b3ef-129">`Major`: Breaking changes</span></span>
- <span data-ttu-id="5b3ef-130">`Minor`: Geriye dönük olarak uyumlu ancak yeni özellikler</span><span class="sxs-lookup"><span data-stu-id="5b3ef-130">`Minor`: New features, but backwards compatible</span></span>
- <span data-ttu-id="5b3ef-131">`Patch`: Geriye dönük uyumlu hata yalnızca düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="5b3ef-131">`Patch`: Backwards compatible bug fixes only</span></span>

<span data-ttu-id="5b3ef-132">Yayın öncesi sürümleri kısa çizgi ve bir dize sonra düzeltme numarası ekleyerek belirtilir.</span><span class="sxs-lookup"><span data-stu-id="5b3ef-132">Pre-release versions are then denoted by appending a hyphen and a string after the patch number.</span></span> <span data-ttu-id="5b3ef-133">Teknik olarak konuşarak kullanabilirsiniz * herhangi * tire ve NuGet paketi yayın öncesi kabul eder sonra dize.</span><span class="sxs-lookup"><span data-stu-id="5b3ef-133">Technically speaking, you can use *any *string after the hyphen and NuGet will treat the package as pre-release.</span></span> <span data-ttu-id="5b3ef-134">NuGet sonra kendileri için anlamı yorumlamaya tüketicileri bırakarak geçerli UI tam sürüm numarasını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="5b3ef-134">NuGet then displays the full version number in the applicable UI, leaving consumers to interpret the meaning for themselves.</span></span>

<span data-ttu-id="5b3ef-135">Bu durum dikkate alınarak, aşağıdaki gibi tanınan adlandırma kurallarına uygun genellikle iyi olur:</span><span class="sxs-lookup"><span data-stu-id="5b3ef-135">With this in mind, it's generally good to follow recognized naming conventions such as the following:</span></span>

- <span data-ttu-id="5b3ef-136">`-alpha`: Genelde iş ilerleme ve deneme için kullanılan alfa sürüm</span><span class="sxs-lookup"><span data-stu-id="5b3ef-136">`-alpha`: Alpha release, typically used for work-in-progress and experimentation</span></span>
- <span data-ttu-id="5b3ef-137">`-beta`: Beta sürümü, genellikle bir özellik için sonraki tam planlanmış serbest bırakma, ancak bilinen hataları içerebilir.</span><span class="sxs-lookup"><span data-stu-id="5b3ef-137">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="5b3ef-138">`-rc`: Sürüm Adayı, genellikle büyük olasılıkla son bir yayın (stable) önemli hatalar ortaya çıkan sürece.</span><span class="sxs-lookup"><span data-stu-id="5b3ef-138">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="5b3ef-139">NuGet desteklemiyor [SemVer uyumlu (v2.0.0)](http://semver.org/spec/v2.0.0.html) yayın öncesi olarak noktalı gösterim ile numaraları `1.0.1-build.23`.</span><span class="sxs-lookup"><span data-stu-id="5b3ef-139">NuGet does not support [SemVer-compatible (v2.0.0)](http://semver.org/spec/v2.0.0.html) prerelease numbers with dot notation, as in `1.0.1-build.23`.</span></span> <span data-ttu-id="5b3ef-140">Bir form gibi kullanabilirsiniz `1.0.1-build23` ancak bu her zaman bir yayım öncesi sürümü olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="5b3ef-140">You can use a form like `1.0.1-build23` but this is always considered a pre-release version.</span></span>

<span data-ttu-id="5b3ef-141">Ancak, kullanan ne olursa olsun sonekleri NuGet bunları öncelik ters alfabetik sırada verecektir:</span><span class="sxs-lookup"><span data-stu-id="5b3ef-141">Whatever suffixes you use, however, NuGet will give them precedence in reverse alphabetical order:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta12
    1.0.1-beta05
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha

<span data-ttu-id="5b3ef-142">Gösterildiği gibi herhangi bir sonek olmadan sürüm yayın öncesi sürümleri üzerinde her zaman öncelikli olur.</span><span class="sxs-lookup"><span data-stu-id="5b3ef-142">As shown, the version without any suffix will always take precedence over pre-release versions.</span></span> <span data-ttu-id="5b3ef-143">Ayrıca ift kullanabilecek yayın öncesi etiketleriyle sayısal sonekleri kullanırsanız, sayılar (veya daha fazla), 2f3b beta01 ve beta05 olduğu gibi bunlar doğru sayıları büyük ulaştıklarında sıralaması emin olmak için unutmayın.</span><span class="sxs-lookup"><span data-stu-id="5b3ef-143">Note also that if you use numerical suffixes with pre-release tags that might use double-digit numbers (or more), use leading zeroes as in beta01 and beta05 to ensure that they sort correctly when the numbers get larger.</span></span>
