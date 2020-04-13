---
title: NuGet paketlerinde ön sürüm sürümleri
description: Sürüm öncesi paketler oluşturma kılavuzu
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 1c19f962dc9e42154c0f4374432548e867e9538a
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "73610708"
---
# <a name="building-pre-release-packages"></a><span data-ttu-id="9be2e-103">Ön sürüm paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="9be2e-103">Building pre-release packages</span></span>

<span data-ttu-id="9be2e-104">Yeni bir sürüm numarası na sahip güncelleştirilmiş bir paket yayımladiğinizde, NuGet bunu örneğin Visual Studio'daki Paket Yöneticisi UI'sinde gösterildiği gibi "en son kararlı sürüm" olarak kabul eder:</span><span class="sxs-lookup"><span data-stu-id="9be2e-104">Whenever you release an updated package with a new version number, NuGet considers that one as the "latest stable release" as shown, for example in the Package Manager UI within Visual Studio:</span></span>

![Paket Yöneticisi UI en son kararlı sürümü gösteren](media/Prerelease_01-LatestStable.png)

<span data-ttu-id="9be2e-106">Kararlı bir sürüm, üretimde kullanılacak kadar güvenilir kabul edilen bir sürümdür.</span><span class="sxs-lookup"><span data-stu-id="9be2e-106">A stable release is one that's considered reliable enough to be used in production.</span></span> <span data-ttu-id="9be2e-107">En son kararlı sürüm aynı zamanda paket güncelleştirme olarak veya paket geri yükleme sırasında yüklenecek olansürümdür [(paketleri yeniden yükleme ve güncelleştirmede](../consume-packages/reinstalling-and-updating-packages.md)açıklandığı gibi kısıtlamalara tabidir).</span><span class="sxs-lookup"><span data-stu-id="9be2e-107">The latest stable release is also the one that will be installed as a package update or during package restore (subject to constraints as described in [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)).</span></span>

<span data-ttu-id="9be2e-108">Yazılım sürüm yaşam döngüsünü desteklemek için, NuGet 1.6 ve daha sonra sürüm numarası gibi `-alpha`semantik bir sürüm soneki `-beta`içeren `-rc`ön sürüm paketlerinin dağıtımına izin verir , , veya .</span><span class="sxs-lookup"><span data-stu-id="9be2e-108">To support the software release lifecycle, NuGet 1.6 and later allows for the distribution of pre-release packages, where the version number includes a semantic versioning suffix such as `-alpha`, `-beta`, or `-rc`.</span></span> <span data-ttu-id="9be2e-109">Daha fazla bilgi için [Paket sürümüne](../concepts/package-versioning.md#pre-release-versions)bakın.</span><span class="sxs-lookup"><span data-stu-id="9be2e-109">For more information, see [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span>

<span data-ttu-id="9be2e-110">Bu tür sürümleri aşağıdaki yollardan birini kullanarak belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9be2e-110">You can specify such versions using one of the following ways:</span></span>

- <span data-ttu-id="9be2e-111">\*\*Projenizde [`PackageReference`](../consume-packages/package-references-in-project-files.md) \*\*: `.csproj` dosyanın [`PackageVersion`](/dotnet/core/tools/csproj.md#packageversion) öğesine anlamsal sürüm soneki ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9be2e-111">**If your project uses [`PackageReference`](../consume-packages/package-references-in-project-files.md)**: include the semantic version suffix in the `.csproj` file's [`PackageVersion`](/dotnet/core/tools/csproj.md#packageversion) element:</span></span>

    ```xml
    <PropertyGroup>
        <PackageVersion>1.0.1-alpha</PackageVersion>
    </PropertyGroup>
    ```

- <span data-ttu-id="9be2e-112">**Projenizde bir [`packages.config`](../reference/packages-config.md) dosya varsa:** [`.nuspec`](../reference/nuspec.md) dosyanın [`version`](../reference/nuspec.md#version) öğesine anlamsal sürüm soneki ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9be2e-112">**If your project has a [`packages.config`](../reference/packages-config.md) file**: include the semantic version suffix in the [`.nuspec`](../reference/nuspec.md) file's [`version`](../reference/nuspec.md#version) element:</span></span>

    ```xml
    <version>1.0.1-alpha</version>
    ```

<span data-ttu-id="9be2e-113">Kararlı bir sürüm yayınlamaya hazır olduğunuzda, soneği kaldırmanız ve paketin ön sürümsürümlerinden önce gelen bir şey olması.</span><span class="sxs-lookup"><span data-stu-id="9be2e-113">When you're ready to release a stable version, just remove the suffix and the package takes precedence over any pre-release versions.</span></span> <span data-ttu-id="9be2e-114">Yine, [Bkz. Paket sürüm.](../concepts/package-versioning.md#pre-release-versions)</span><span class="sxs-lookup"><span data-stu-id="9be2e-114">Again, see [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span>

## <a name="installing-and-updating-pre-release-packages"></a><span data-ttu-id="9be2e-115">Sürüm öncesi paketlerin yüklenmesi ve güncellenmesi</span><span class="sxs-lookup"><span data-stu-id="9be2e-115">Installing and updating pre-release packages</span></span>

<span data-ttu-id="9be2e-116">Varsayılan olarak, NuGet paketleri ile çalışırken ön sürüm sürümleri içermez, ancak aşağıdaki gibi bu davranışı değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9be2e-116">By default, NuGet does not include pre-release versions when working with packages, but you can change this behavior as follows:</span></span>

- <span data-ttu-id="9be2e-117">**Visual Studio'da Paket Yöneticisi UI**: **NuGet Paketlerini** Yönet'te, **Ön Sürüm Ekle** kutusunu işaretleyin:</span><span class="sxs-lookup"><span data-stu-id="9be2e-117">**Package Manager UI in Visual Studio**: In the **Manage NuGet Packages** UI, check the **Include prerelease** box:</span></span>

    ![Visual Studio'ya yayın öncesi onay kutusu ekle](media/Prerelease_02-CheckPrerelease.png)

    <span data-ttu-id="9be2e-119">Bu kutuyu ayarlamak veya temizlemek, Paket Yöneticisi Arabirimi'ni ve yükleyebileceğiniz kullanılabilir sürümlerin listesini yeniler.</span><span class="sxs-lookup"><span data-stu-id="9be2e-119">Setting or clearing this box will refresh the Package Manager UI and the list of available versions you can install.</span></span>

- <span data-ttu-id="9be2e-120">**Paket Yöneticisi Konsolu** `-IncludePrerelease` : `Find-Package`Anahtarı `Get-Package` `Install-Package`, `Sync-Package`, `Update-Package` , ve komutlarla kullanın.</span><span class="sxs-lookup"><span data-stu-id="9be2e-120">**Package Manager Console**: Use the `-IncludePrerelease` switch with the `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, and `Update-Package` commands.</span></span> <span data-ttu-id="9be2e-121">[PowerShell Referans](../reference/powershell-reference.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="9be2e-121">Refer to the [PowerShell Reference](../reference/powershell-reference.md).</span></span>

- <span data-ttu-id="9be2e-122">**NuGet CLI**: `-prerelease` Anahtarı `install`, `update` `delete`, `mirror` , ve komutlarla kullanın.</span><span class="sxs-lookup"><span data-stu-id="9be2e-122">**NuGet CLI**: Use the `-prerelease` switch with the `install`, `update`, `delete`, and `mirror` commands.</span></span> <span data-ttu-id="9be2e-123">[NuGet CLI referansına](../reference/nuget-exe-cli-reference.md) bakın</span><span class="sxs-lookup"><span data-stu-id="9be2e-123">Refer to the [NuGet CLI reference](../reference/nuget-exe-cli-reference.md)</span></span>

## <a name="semantic-versioning"></a><span data-ttu-id="9be2e-124">Anlamsal sürüm</span><span class="sxs-lookup"><span data-stu-id="9be2e-124">Semantic versioning</span></span>

<span data-ttu-id="9be2e-125">[Anlamsal Sürüm veya SemVer kuralı,](https://semver.org/spec/v1.0.0.html) temel kodun anlamını iletmek için sürüm numaralarındaki dizeleri nasıl kullanılacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="9be2e-125">The [Semantic Versioning or SemVer convention](https://semver.org/spec/v1.0.0.html) describes how to utilize strings in version numbers to convey the meaning of the underlying code.</span></span>

<span data-ttu-id="9be2e-126">Bu sözleşmede, her sürümün `Major.Minor.Patch`üç bölümü vardır, aşağıdaki anlamı ile:</span><span class="sxs-lookup"><span data-stu-id="9be2e-126">In this convention, each version has three parts, `Major.Minor.Patch`, with the following meaning:</span></span>

- <span data-ttu-id="9be2e-127">`Major`: Son dakika değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="9be2e-127">`Major`: Breaking changes</span></span>
- <span data-ttu-id="9be2e-128">`Minor`: Yeni özellikler, ancak geriye uyumlu</span><span class="sxs-lookup"><span data-stu-id="9be2e-128">`Minor`: New features, but backwards compatible</span></span>
- <span data-ttu-id="9be2e-129">`Patch`: Geriye uyumlu hata düzeltmeleri yalnızca</span><span class="sxs-lookup"><span data-stu-id="9be2e-129">`Patch`: Backwards compatible bug fixes only</span></span>

<span data-ttu-id="9be2e-130">Ön sürüm sürümleri daha sonra yama numarasından sonra bir tire ve dize ekleyerek gösterilir.</span><span class="sxs-lookup"><span data-stu-id="9be2e-130">Pre-release versions are then denoted by appending a hyphen and a string after the patch number.</span></span> <span data-ttu-id="9be2e-131">Teknik olarak konuşursak, tire ve NuGet ön sürüm olarak paketi ele alacak sonra *herhangi bir* dize kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9be2e-131">Technically speaking, you can use *any* string after the hyphen and NuGet will treat the package as pre-release.</span></span> <span data-ttu-id="9be2e-132">NuGet daha sonra geçerli UI'de tam sürüm numarasını görüntüler ve tüketicilerin anlamını kendileri için yorumlamalarına neden olur.</span><span class="sxs-lookup"><span data-stu-id="9be2e-132">NuGet then displays the full version number in the applicable UI, leaving consumers to interpret the meaning for themselves.</span></span>

<span data-ttu-id="9be2e-133">Bunu göz önünde bulundurarak, genellikle aşağıdaki gibi tanınan adlandırma kuralları takip etmek iyidir:</span><span class="sxs-lookup"><span data-stu-id="9be2e-133">With this in mind, it's generally good to follow recognized naming conventions such as the following:</span></span>

- <span data-ttu-id="9be2e-134">`-alpha`: Alfa salınımı, genellikle devam aşamasındaki işler ve deneyler için kullanılır</span><span class="sxs-lookup"><span data-stu-id="9be2e-134">`-alpha`: Alpha release, typically used for work-in-progress and experimentation</span></span>
- <span data-ttu-id="9be2e-135">`-beta`: Beta sürümü, genellikle bir sonraki planlanan sürüm için tamamlanmış özellik, ancak bilinen hataları içerebilir.</span><span class="sxs-lookup"><span data-stu-id="9be2e-135">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="9be2e-136">`-rc`: Sürüm adayı, önemli hatalar ortaya çıkmadıkça genellikle nihai (kararlı) bir sürüm.</span><span class="sxs-lookup"><span data-stu-id="9be2e-136">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="9be2e-137">NuGet 4.3.0+ gibi nokta gösterimi ile ön sürüm numaraları destekleyen [Semantik Sürüm v2.0.0](https://semver.org/spec/v2.0.0.html)destekler `1.0.1-build.23`.</span><span class="sxs-lookup"><span data-stu-id="9be2e-137">NuGet 4.3.0+ supports [Semantic Versioning v2.0.0](https://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in `1.0.1-build.23`.</span></span> <span data-ttu-id="9be2e-138">Nokta gösterimi 4.3.0'dan önce NuGet sürümleriyle desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="9be2e-138">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="9be2e-139">NuGet önceki sürümlerinde, gibi `1.0.1-build23` bir form kullanabilirsiniz ama bu her zaman bir ön sürüm olarak kabul edildi.</span><span class="sxs-lookup"><span data-stu-id="9be2e-139">In earlier versions of NuGet, you could use a form like `1.0.1-build23` but this was always considered a pre-release version.</span></span>

<span data-ttu-id="9be2e-140">Ancak kullandığınız sonekler ne olursa olsun, NuGet onlara ters alfabetik sırayla öncelik verecektir:</span><span class="sxs-lookup"><span data-stu-id="9be2e-140">Whatever suffixes you use, however, NuGet will give them precedence in reverse alphabetical order:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta.12
    1.0.1-beta.5
    1.0.1-beta
    1.0.1-alpha.2
    1.0.1-alpha

<span data-ttu-id="9be2e-141">Gösterildiği gibi, herhangi bir sonek olmayan sürüm her zaman ön sürüm sürümlerine göre öncelikli olacaktır.</span><span class="sxs-lookup"><span data-stu-id="9be2e-141">As shown, the version without any suffix will always take precedence over pre-release versions.</span></span>

<span data-ttu-id="9be2e-142">Lider 0s semver2 ile gerekli değildir, ancak eski sürüm şema ile vardır.</span><span class="sxs-lookup"><span data-stu-id="9be2e-142">Leading 0s are not needed with semver2, but they are with the old version schema.</span></span> <span data-ttu-id="9be2e-143">Çift basamaklı sayılar (veya daha fazla) kullanabilen ön sürüm etiketlerine sahip sayısal sonekler kullanıyorsanız, sayılar büyüdükçe doğru şekilde sıralandığından emin olmak için beta.01 ve beta.05'teki gibi önde gelen sıfırları kullanın.</span><span class="sxs-lookup"><span data-stu-id="9be2e-143">If you use numerical suffixes with pre-release tags that might use double-digit numbers (or more), use leading zeroes as in beta.01 and beta.05 to ensure that they sort correctly when the numbers get larger.</span></span> <span data-ttu-id="9be2e-144">Bu öneri yalnızca eski sürüm şeması için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="9be2e-144">This recommendation only applies to the old version schema.</span></span>
