---
title: NuGet hataları ve Uyarıları başvurusu
description: Uyarıları ve hataları Nuget'ten çeşitli NuGet işlemleri sırasında verilen başvurusunu tamamlayın.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: anangaur
f1_keywords:
- NU1000
- NU1001
- NU1002
- NU1003
- NU1100
- NU1101
- NU1102
- NU1103
- NU1104
- NU1105
- NU1106
- NU1107
- NU1108
- NU1201
- NU1202
- NU1203
- NU1401
- NU1500
- NU1501
- NU1502
- NU1503
- NU1601
- NU1602
- NU1603
- NU1604
- NU1605
- NU1608
- NU1701
- NU1801
- NU3000
- NU3001
- NU3002
- NU3004
- NU3008
- NU3018
- NU3028
ms.openlocfilehash: 748c2746a61886617e2eefe3e6c4a2e2a5b9d4d3
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/22/2018
---
# <a name="errors-and-warnings"></a><span data-ttu-id="11c1f-103">Hatalar ve uyarılar</span><span class="sxs-lookup"><span data-stu-id="11c1f-103">Errors and warnings</span></span>

<span data-ttu-id="11c1f-104">NuGet 4.3.0+, hataları ve Uyarıları Bu konu başlığı altında açıklandığı gibi numaralı ve ilgili sorunları gidermek amacıyla ayrıntılı bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="11c1f-104">In NuGet 4.3.0+, errors and warnings are numbered as described in this topic and provide detailed information to help you address the issues involved.</span></span>

<span data-ttu-id="11c1f-105">Hatalar ve uyarılar burada listelenen yalnızca [PackageReference tabanlı](../consume-packages/package-references-in-project-files.md) projeleri ve NuGet 4.3.0+.</span><span class="sxs-lookup"><span data-stu-id="11c1f-105">The errors and warnings listed here are available only with [PackageReference-based](../consume-packages/package-references-in-project-files.md) projects and NuGet 4.3.0+.</span></span> <span data-ttu-id="11c1f-106">NuGet uyarıları bastırma veya hataları yükseltmesine MSBuild özellikleri de geliştirir.</span><span class="sxs-lookup"><span data-stu-id="11c1f-106">NuGet also honors MSBuild properties to suppress warnings or elevate them to errors.</span></span> <span data-ttu-id="11c1f-107">Daha fazla bilgi için bkz: [nasıl yapılır: Derleyici uyarılarını bastırma](/visualstudio/ide/how-to-suppress-compiler-warnings) Visual Studio belgelerinde.</span><span class="sxs-lookup"><span data-stu-id="11c1f-107">For more information, see [How to: Suppress Compiler Warnings](/visualstudio/ide/how-to-suppress-compiler-warnings) in the Visual Studio documentation.</span></span>

<span data-ttu-id="11c1f-108">**Hataları**</span><span class="sxs-lookup"><span data-stu-id="11c1f-108">**Errors**</span></span>

| <span data-ttu-id="11c1f-109">Grup</span><span class="sxs-lookup"><span data-stu-id="11c1f-109">Group</span></span> | <span data-ttu-id="11c1f-110">Hata numaraları</span><span class="sxs-lookup"><span data-stu-id="11c1f-110">Error Numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="11c1f-111">Geçersiz giriş hataları</span><span class="sxs-lookup"><span data-stu-id="11c1f-111">Invalid input errors</span></span>](#invalid-input-errors) | <span data-ttu-id="11c1f-112">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="11c1f-112">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span></span> |
| [<span data-ttu-id="11c1f-113">Eksik paket ve proje hataları</span><span class="sxs-lookup"><span data-stu-id="11c1f-113">Missing package and project errors</span></span>](#missing-package-and-project-errors) | <span data-ttu-id="11c1f-114">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (daha önce NU1607) [NU1108](#nu1108) (daha önce NU1606)</span><span class="sxs-lookup"><span data-stu-id="11c1f-114">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1108) (previously NU1606)</span></span> |
| [<span data-ttu-id="11c1f-115">Uyumluluk hataları</span><span class="sxs-lookup"><span data-stu-id="11c1f-115">Compatibility errors</span></span>](#compatibility-errors) | <span data-ttu-id="11c1f-116">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="11c1f-116">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span></span> |

<span data-ttu-id="11c1f-117">**Uyarıları**</span><span class="sxs-lookup"><span data-stu-id="11c1f-117">**Warnings**</span></span>

| <span data-ttu-id="11c1f-118">Grup</span><span class="sxs-lookup"><span data-stu-id="11c1f-118">Group</span></span> | <span data-ttu-id="11c1f-119">Uyarı numaraları</span><span class="sxs-lookup"><span data-stu-id="11c1f-119">Warning numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="11c1f-120">Geçersiz giriş uyarıları</span><span class="sxs-lookup"><span data-stu-id="11c1f-120">Invalid input warnings</span></span>](#invalid-input-warnings) | <span data-ttu-id="11c1f-121">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="11c1f-121">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span></span> |
| [<span data-ttu-id="11c1f-122">Beklenmeyen Paket sürümü uyarıları</span><span class="sxs-lookup"><span data-stu-id="11c1f-122">Unexpected package version warnings</span></span>](#unexpected-package-version-warnings) | <span data-ttu-id="11c1f-123">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="11c1f-123">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span></span> |
| [<span data-ttu-id="11c1f-124">Çözümleyici çakışma uyarıları</span><span class="sxs-lookup"><span data-stu-id="11c1f-124">Resolver conflict warnings</span></span>](#resolver-conflict-warnings) | [<span data-ttu-id="11c1f-125">NU1608</span><span class="sxs-lookup"><span data-stu-id="11c1f-125">NU1608</span></span>](#nu1608) |
| [<span data-ttu-id="11c1f-126">Paket geri dönüş uyarıları</span><span class="sxs-lookup"><span data-stu-id="11c1f-126">Package fallback warnings</span></span>](#package-fallback-warnings) | [<span data-ttu-id="11c1f-127">NU1701</span><span class="sxs-lookup"><span data-stu-id="11c1f-127">NU1701</span></span>](#nu1701) |
| [<span data-ttu-id="11c1f-128">Akış uyarıları</span><span class="sxs-lookup"><span data-stu-id="11c1f-128">Feed warnings</span></span>](#feed-warnings) | [<span data-ttu-id="11c1f-129">NU1801</span><span class="sxs-lookup"><span data-stu-id="11c1f-129">NU1801</span></span>](#nu1801) |
| [<span data-ttu-id="11c1f-130">NuGet iç hatalar ve uyarılar</span><span class="sxs-lookup"><span data-stu-id="11c1f-130">NuGet internal errors and warnings</span></span>](#nuget-internal-errors-and-warnings) | <span data-ttu-id="11c1f-131">[NU1000](#nu1000), [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="11c1f-131">[NU1000](#nu1000), [NU1500](#nu1500)</span></span> |
| [<span data-ttu-id="11c1f-132">İmzalı Paketleri (oluşturma ve doğrulama)</span><span class="sxs-lookup"><span data-stu-id="11c1f-132">Signed packages (creation and verification)</span></span>](#signed-packages-creation-and-verification)| <span data-ttu-id="11c1f-133">[NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="11c1f-133">[NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028)</span></span> |

## <a name="invalid-input-errors"></a><span data-ttu-id="11c1f-134">Geçersiz giriş hataları</span><span class="sxs-lookup"><span data-stu-id="11c1f-134">Invalid input errors</span></span>

<span data-ttu-id="11c1f-135">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="11c1f-135">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span></span>

### <a name="nu1001"></a><span data-ttu-id="11c1f-136">NU1001</span><span class="sxs-lookup"><span data-stu-id="11c1f-136">NU1001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="11c1f-137">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="11c1f-137">**Issue**</span></span> | <span data-ttu-id="11c1f-138">Bir veya daha fazla çerçeveler proje içermiyor.</span><span class="sxs-lookup"><span data-stu-id="11c1f-138">The project doesn't contain one or more frameworks.</span></span> |
| <span data-ttu-id="11c1f-139">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="11c1f-139">**Example message**</span></span> | <span data-ttu-id="11c1f-140">*Proje projA c:\tmp\projA.csproj içinde herhangi bir hedef çerçeve belirtmiyor*</span><span class="sxs-lookup"><span data-stu-id="11c1f-140">*The project projA does not specify any target frameworks in c:\tmp\projA.csproj*</span></span> |
| <span data-ttu-id="11c1f-141">**Çözüm**</span><span class="sxs-lookup"><span data-stu-id="11c1f-141">**Solution**</span></span> | <span data-ttu-id="11c1f-142">Ekleme bir `TargetFramework` veya `TargetFrameworks` belirtilen proje dosyasına özelliği.</span><span class="sxs-lookup"><span data-stu-id="11c1f-142">Add a `TargetFramework` or `TargetFrameworks` property to the specified project file.</span></span> |

### <a name="nu1002"></a><span data-ttu-id="11c1f-143">NU1002</span><span class="sxs-lookup"><span data-stu-id="11c1f-143">NU1002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="11c1f-144">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="11c1f-144">**Issue**</span></span> | <span data-ttu-id="11c1f-145">Girişleri Temizle anahtar sözcüğü ile birlikte birleşimi geçersiz.</span><span class="sxs-lookup"><span data-stu-id="11c1f-145">Invalid combination of inputs along with a CLEAR keyword.</span></span> |
| <span data-ttu-id="11c1f-146">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="11c1f-146">**Example message**</span></span> | <span data-ttu-id="11c1f-147">*'CLEAR' diğer değerler ile birlikte kullanılamaz*</span><span class="sxs-lookup"><span data-stu-id="11c1f-147">*'CLEAR' cannot be used in conjunction with other values*</span></span> |
| <span data-ttu-id="11c1f-148">**Çözüm**</span><span class="sxs-lookup"><span data-stu-id="11c1f-148">**Solution**</span></span> | <span data-ttu-id="11c1f-149">CLEAR başına kullanın ve diğer tüm girişleri atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="11c1f-149">Use CLEAR by itself and omit all other inputs.</span></span> |

### <a name="nu1003"></a><span data-ttu-id="11c1f-150">NU1003</span><span class="sxs-lookup"><span data-stu-id="11c1f-150">NU1003</span></span>

| | |
| --- | --- |
| <span data-ttu-id="11c1f-151">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="11c1f-151">**Issue**</span></span> | <span data-ttu-id="11c1f-152">`PackageTargetFallback` ve `AssetTargetFallback` varlıklar seçmek için farklı bir davranış sağlar ve birlikte kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="11c1f-152">`PackageTargetFallback` and `AssetTargetFallback` provide different behavior for selecting assets and cannot be used together.</span></span> |
| <span data-ttu-id="11c1f-153">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="11c1f-153">**Example message**</span></span> | <span data-ttu-id="11c1f-154">*PackageTargetFallback ve AssetTargetFallback birlikte kullanılamaz. Proje ortamından PackageTargetFallback(deprecated) başvuruları kaldırın.*</span><span class="sxs-lookup"><span data-stu-id="11c1f-154">*PackageTargetFallback and AssetTargetFallback cannot be used together. Remove PackageTargetFallback(deprecated) references from the project environment.*</span></span> |
| <span data-ttu-id="11c1f-155">**Çözüm**</span><span class="sxs-lookup"><span data-stu-id="11c1f-155">**Solution**</span></span> | <span data-ttu-id="11c1f-156">Kullanım dışı kaldırmak `PackageTargetFallback` proje öğesi.</span><span class="sxs-lookup"><span data-stu-id="11c1f-156">Remove the deprecated `PackageTargetFallback` element from the project.</span></span> |

## <a name="missing-package-and-project-errors"></a><span data-ttu-id="11c1f-157">Eksik paket ve proje hataları</span><span class="sxs-lookup"><span data-stu-id="11c1f-157">Missing package and project errors</span></span>

<span data-ttu-id="11c1f-158">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104)  |  [NU1105](#nu1105) | [NU1106](#nu1106)</span><span class="sxs-lookup"><span data-stu-id="11c1f-158">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span></span>

### <a name="nu1100"></a><span data-ttu-id="11c1f-159">NU1100</span><span class="sxs-lookup"><span data-stu-id="11c1f-159">NU1100</span></span>

| | |
| --- | --- |
| <span data-ttu-id="11c1f-160">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="11c1f-160">**Issue**</span></span> | <span data-ttu-id="11c1f-161">Bir bağımlılık grubunun çözülmesi değil.</span><span class="sxs-lookup"><span data-stu-id="11c1f-161">A dependency group not be resolved.</span></span> <span data-ttu-id="11c1f-162">Bu, paket veya projeleri olmayan türleri için genel bir sorundur.</span><span class="sxs-lookup"><span data-stu-id="11c1f-162">This is a generic issue for types that are not packages or projects.</span></span> |
| <span data-ttu-id="11c1f-163">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="11c1f-163">**Example message**</span></span> | <span data-ttu-id="11c1f-164">*System.Missing için net45 çözümlenemiyor*</span><span class="sxs-lookup"><span data-stu-id="11c1f-164">*Unable to resolve System.Missing for net45*</span></span> |
| <span data-ttu-id="11c1f-165">**Çözüm**</span><span class="sxs-lookup"><span data-stu-id="11c1f-165">**Solution**</span></span> | <span data-ttu-id="11c1f-166">Proje dosyasını açın ve bağımlılıklarını listesini inceleyin.</span><span class="sxs-lookup"><span data-stu-id="11c1f-166">Open the project file and examine the list of its dependencies.</span></span> <span data-ttu-id="11c1f-167">Her bir bağımlılığın kullanmakta olduğunuz paket kaynaklarını üzerinde var olduğunu ve paket projenin hedef çerçevesi desteklediğini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="11c1f-167">Check that each dependency exists on the package sources you're using, and that the package supports the project's target framework.</span></span> |

### <a name="nu1101"></a><span data-ttu-id="11c1f-168">NU1101</span><span class="sxs-lookup"><span data-stu-id="11c1f-168">NU1101</span></span>

| | |
| --- | --- |
| <span data-ttu-id="11c1f-169">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="11c1f-169">**Issue**</span></span> | <span data-ttu-id="11c1f-170">Paketin tüm kaynakları bulunamıyor.</span><span class="sxs-lookup"><span data-stu-id="11c1f-170">The package cannot be found on any sources.</span></span> |
| <span data-ttu-id="11c1f-171">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="11c1f-171">**Example message**</span></span> | <span data-ttu-id="11c1f-172">*Paket System.Missing bulunamıyor. Bu kimlikle kaynakları hiç paket yok: dotnet çekirdekli, dotnet roslyn, nuget.org*</span><span class="sxs-lookup"><span data-stu-id="11c1f-172">*Unable to find package System.Missing. No packages exist with this id in source(s): dotnet-core, dotnet-roslyn, nuget.org*</span></span> |
| <span data-ttu-id="11c1f-173">**Çözüm**</span><span class="sxs-lookup"><span data-stu-id="11c1f-173">**Solution**</span></span> | <span data-ttu-id="11c1f-174">Doğru paket tanımlayıcısı ve sürüm numarasını kullandığınızdan emin olmak için Visual Studio Proje bağımlılıkları inceleyin.</span><span class="sxs-lookup"><span data-stu-id="11c1f-174">Examine the project's dependencies in Visual Studio to be sure you're using the correct package identifier and version number.</span></span> <span data-ttu-id="11c1f-175">Ayrıca denetleyin [NuGet Yapılandırması](../consume-packages/Configuring-NuGet-Behavior.md) paket kaynaklarını tanımlar, kullanılmasını bekler.</span><span class="sxs-lookup"><span data-stu-id="11c1f-175">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="11c1f-176">Sahip paketleri kullanıyorsanız [anlamsal sürüm oluşturma 2.0.0](../reference/package-versioning.md#semantic-versioning-200), lütfen akışı, V3 kullandığınızdan emin olun `https://api.nuget.org/v3/index.json`, [NuGet Yapılandırması](../consume-packages/Configuring-NuGet-Behavior.md).</span><span class="sxs-lookup"><span data-stu-id="11c1f-176">If you use packages that have [Semantic Versioning 2.0.0](../reference/package-versioning.md#semantic-versioning-200), please make sure that you are using the V3 feed, `https://api.nuget.org/v3/index.json`, in the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md).</span></span> |

### <a name="nu1102"></a><span data-ttu-id="11c1f-177">NU1102</span><span class="sxs-lookup"><span data-stu-id="11c1f-177">NU1102</span></span>

| | |
| --- | --- |
| <span data-ttu-id="11c1f-178">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="11c1f-178">**Issue**</span></span> | <span data-ttu-id="11c1f-179">Paket tanımlayıcısı bulundu, ancak belirtilen bağımlılık aralıkta bir sürüm kaynakları hiçbirinde bulunamıyor.</span><span class="sxs-lookup"><span data-stu-id="11c1f-179">The package identifier is found but a version within the specified dependency range cannot be found on any of the sources.</span></span> <span data-ttu-id="11c1f-180">Aralığın bir paket ve kullanıcı tarafından belirtilen.</span><span class="sxs-lookup"><span data-stu-id="11c1f-180">The range might be specified by a package and not the user.</span></span> |
| <span data-ttu-id="11c1f-181">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="11c1f-181">**Example message**</span></span> | <span data-ttu-id="11c1f-182">*Paketi NuGet.Versioning sürümüyle bulunamadı (> 9.0.1 =)<br/> -nuget.org içinde bulunan 30 sürümler [sürüm en yakın: 4.0.0]<br/> -dotnet buildtools içinde bulunan 10 sürümler [sürüm en yakın: 4.0.0-rc-2129]<br/> -9 bulundu NuGetVolatile sürümler [sürüm en yakın: 3.0.0-beta-00032]<br/> -0 sürümler dotnet-çekirdek bulunan<br/> -0 sürümler dotnet-roslyn bulundu*</span><span class="sxs-lookup"><span data-stu-id="11c1f-182">*Unable to find package NuGet.Versioning with version (>= 9.0.1)<br/>  - Found 30 version(s) in nuget.org [ Nearest version: 4.0.0 ]<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="11c1f-183">**Çözüm**</span><span class="sxs-lookup"><span data-stu-id="11c1f-183">**Solution**</span></span> | <span data-ttu-id="11c1f-184">Paket sürümü düzeltmek için proje dosyasını düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="11c1f-184">Edit the project file to correct the package version.</span></span> <span data-ttu-id="11c1f-185">Ayrıca denetleyin [NuGet Yapılandırması](../consume-packages/Configuring-NuGet-Behavior.md) paket kaynaklarını tanımlar, kullanılmasını bekler.</span><span class="sxs-lookup"><span data-stu-id="11c1f-185">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="11c1f-186">Bu paket proje tarafından doğrudan başvurulduğunda requeted version değiştirmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="11c1f-186">You may need to change the requeted version if this package is referenced by the project directly.</span></span> |

### <a name="nu1103"></a><span data-ttu-id="11c1f-187">NU1103</span><span class="sxs-lookup"><span data-stu-id="11c1f-187">NU1103</span></span>

| | |
| --- | --- |
| <span data-ttu-id="11c1f-188">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="11c1f-188">**Issue**</span></span> | <span data-ttu-id="11c1f-189">Proje kararlı bir sürüm bağımlılığı aralığı için belirtilen ancak hiçbir kararlı sürümleri bu aralıkta bulundu.</span><span class="sxs-lookup"><span data-stu-id="11c1f-189">The project specified a stable version for the dependency range, but no stable versions were found in that range.</span></span> <span data-ttu-id="11c1f-190">Yayın öncesi sürümleri bulundu, ancak izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="11c1f-190">Pre-release versions were found but are not allowed.</span></span> |
| <span data-ttu-id="11c1f-191">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="11c1f-191">**Example message**</span></span> | <span data-ttu-id="11c1f-192">*Sürümüyle kararlı paketi NuGet.Versioning bulunamadı (> 3.0.0 =)<br/> -dotnet buildtools içinde bulunan 10 sürümler [sürüm en yakın: 4.0.0-rc-2129]<br/> -NuGetVolatile içinde bulunan 9 sürümler [sürüm en yakın: 3.0.0-beta-00032] <br/> -0 sürümler dotnet-çekirdek bulunan<br/> -0 sürümler dotnet-roslyn bulundu*</span><span class="sxs-lookup"><span data-stu-id="11c1f-192">*Unable to find a stable package NuGet.Versioning with version (>= 3.0.0)<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="11c1f-193">**Çözüm**</span><span class="sxs-lookup"><span data-stu-id="11c1f-193">**Solution**</span></span> |  <span data-ttu-id="11c1f-194">Yayın öncesi sürümleri dahil etmek için proje dosyasında sürüm aralığı düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="11c1f-194">Edit the version range in the project file to include pre-release versions.</span></span> <span data-ttu-id="11c1f-195">Bkz: [paket sürüm](../reference/Package-Versioning.md).</span><span class="sxs-lookup"><span data-stu-id="11c1f-195">See [Package versioning](../reference/Package-Versioning.md).</span></span> |

### <a name="nu1104"></a><span data-ttu-id="11c1f-196">NU1104</span><span class="sxs-lookup"><span data-stu-id="11c1f-196">NU1104</span></span>

| | |
| --- | --- |
| <span data-ttu-id="11c1f-197">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="11c1f-197">**Issue**</span></span> | <span data-ttu-id="11c1f-198">Bir ProjectReference mevcut olmayan bir dosyaya işaret eder.</span><span class="sxs-lookup"><span data-stu-id="11c1f-198">A ProjectReference points to a file that doesn't exist.</span></span> |
| <span data-ttu-id="11c1f-199">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="11c1f-199">**Example message**</span></span> | <span data-ttu-id="11c1f-200">*Proje Başvurusu 'c:\a.csproj' yok. Proje başvurusu geçerli olduğunu ve proje dosyasının varolduğunu kontrol edin.*</span><span class="sxs-lookup"><span data-stu-id="11c1f-200">*Project reference does not exist 'c:\a.csproj'. Check that the project reference is valid and that the project file exists.*</span></span> |
| <span data-ttu-id="11c1f-201">**Çözüm**</span><span class="sxs-lookup"><span data-stu-id="11c1f-201">**Solution**</span></span> | <span data-ttu-id="11c1f-202">Proje dosyası ya da başvuruda bulunulan proje yolunu düzeltin veya başvuruyu kaldırmak üzere Düzenle artık ihtiyaç duyduğunuzda değerlerinin.</span><span class="sxs-lookup"><span data-stu-id="11c1f-202">Edit the project file to either correct the path to the referenced project or to remove the reference altogether if it's no longer needed.</span></span> |

### <a name="nu1105"></a><span data-ttu-id="11c1f-203">NU1105</span><span class="sxs-lookup"><span data-stu-id="11c1f-203">NU1105</span></span>

| | |
| --- | --- |
| <span data-ttu-id="11c1f-204">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="11c1f-204">**Issue**</span></span> | <span data-ttu-id="11c1f-205">Proje dosyası var, ancak bunun için hiçbir geri yükleme bilgisi verilmedi.</span><span class="sxs-lookup"><span data-stu-id="11c1f-205">The project file exists but no restore information was provided for it.</span></span> |
| <span data-ttu-id="11c1f-206">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="11c1f-206">**Example message**</span></span> | <span data-ttu-id="11c1f-207">*'C:\a.csproj' için proje bilgileri okunamıyor. Proje dosyası geçersiz veya eksik hedefleri geri yüklemek için gerekli olabilir.*</span><span class="sxs-lookup"><span data-stu-id="11c1f-207">*Unable to read project information for 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="11c1f-208">**Çözüm**</span><span class="sxs-lookup"><span data-stu-id="11c1f-208">**Solution**</span></span> | <span data-ttu-id="11c1f-209">Visual Studio'da hata projenin, bu durumda yeniden içinde proje, kaldırılmış olduğunu anlamına gelebilir.</span><span class="sxs-lookup"><span data-stu-id="11c1f-209">In Visual Studio, the error could mean that the project is unloaded, in which case reload the project.</span></span> <span data-ttu-id="11c1f-210">Komut satırından bu dosya bozuk veya bu özel "içeri aktarmalar sonra" içermiyor anlamına gelebilir proje okumak geri yükleme için gereken hedef.</span><span class="sxs-lookup"><span data-stu-id="11c1f-210">From the command line this could mean that the file is corrupt or that it doesn't contain the custom "after imports" target needed for restore to read the project.</span></span> <span data-ttu-id="11c1f-211">Proje dosyası geçerli olduğundan ve "sonra içeri aktarmalar" hedef içerdiğini denetleyin.</span><span class="sxs-lookup"><span data-stu-id="11c1f-211">Check that the project file is valid and contains an "after imports" target.</span></span> |

### <a name="nu1106"></a><span data-ttu-id="11c1f-212">NU1106</span><span class="sxs-lookup"><span data-stu-id="11c1f-212">NU1106</span></span>

| | |
| --- | --- |
| <span data-ttu-id="11c1f-213">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="11c1f-213">**Issue**</span></span> | <span data-ttu-id="11c1f-214">Bağımlılık kısıtlamalarını çözümlenemiyor.</span><span class="sxs-lookup"><span data-stu-id="11c1f-214">Dependency constraints cannot be resolved.</span></span> |
| <span data-ttu-id="11c1f-215">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="11c1f-215">**Example message**</span></span> | <span data-ttu-id="11c1f-216">*{İd}'için çakışma istekleri giderilemiyor: {çakışma yolu} Framework: {hedef grafik}*</span><span class="sxs-lookup"><span data-stu-id="11c1f-216">*Unable to satisfy conflicting requests for {id}: {conflict path} Framework: {target graph}*</span></span> |
| <span data-ttu-id="11c1f-217">**Çözüm**</span><span class="sxs-lookup"><span data-stu-id="11c1f-217">**Solution**</span></span> | <span data-ttu-id="11c1f-218">Bir tam sürümü yerine bağımlılık daha uçlu aralıklarını belirtmek için proje dosyasını düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="11c1f-218">Edit the project file to specify more open-ended ranges for the dependency rather than an exact version.</span></span> |
|

<a name="nu1107"></a>

### <a name="nu1107-previously-nu1607"></a><span data-ttu-id="11c1f-219">NU1107 (daha önce NU1607)</span><span class="sxs-lookup"><span data-stu-id="11c1f-219">NU1107 (Previously NU1607)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="11c1f-220">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="11c1f-220">**Issue**</span></span> | <span data-ttu-id="11c1f-221">Bağımlılık kısıtlamalarını paketler arasında çözümlenemiyor.</span><span class="sxs-lookup"><span data-stu-id="11c1f-221">Unable to resolve dependency constraints between packages.</span></span> |
| <span data-ttu-id="11c1f-222">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="11c1f-222">**Example message**</span></span> | <span data-ttu-id="11c1f-223">*Sürüm çakışması için NuGet.Versioning algılandı. Paket, bu sorunu çözmek için doğrudan projeden başvuru.<br/>  NuGet.Packaging 3.5.0 -> (= 3.5.0) NuGet.Versioning<br/> NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span><span class="sxs-lookup"><span data-stu-id="11c1f-223">*Version conflict detected for NuGet.Versioning. Reference the package directly from the project to resolve this issue.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span></span> |
| <span data-ttu-id="11c1f-224">**Çözüm**</span><span class="sxs-lookup"><span data-stu-id="11c1f-224">**Solution**</span></span> | <span data-ttu-id="11c1f-225">Tam sürümleri bağımlılık kısıtlamalar paketlerle sürüm gerekirse artırmak diğer paketleri izin vermez.</span><span class="sxs-lookup"><span data-stu-id="11c1f-225">Packages with dependency constraints on exact versions do not allow other packages to increase the version if needed.</span></span> <span data-ttu-id="11c1f-226">Gerekli tam sürümü ile doğrudan (proje dosyasında) projesine bir başvuru ekleyin.</span><span class="sxs-lookup"><span data-stu-id="11c1f-226">Add a reference to the project directly (in the project file) with the exact version required.</span></span> |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a><span data-ttu-id="11c1f-227">NU1108 (daha önce NU1606)</span><span class="sxs-lookup"><span data-stu-id="11c1f-227">NU1108 (Previously NU1606)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="11c1f-228">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="11c1f-228">**Issue**</span></span> | <span data-ttu-id="11c1f-229">Döngüsel bağımlılık algılandı.</span><span class="sxs-lookup"><span data-stu-id="11c1f-229">A circular dependency was detected.</span></span> |
| <span data-ttu-id="11c1f-230">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="11c1f-230">**Example message**</span></span> | <span data-ttu-id="11c1f-231">*Döngü algılandı: A B -> A ->*</span><span class="sxs-lookup"><span data-stu-id="11c1f-231">*Cycle detected: A -> B -> A*</span></span> |
| <span data-ttu-id="11c1f-232">**Çözüm**</span><span class="sxs-lookup"><span data-stu-id="11c1f-232">**Solution**</span></span> | <span data-ttu-id="11c1f-233">Paket yanlış yazılmış; hatayı düzeltmek için paket sahibine başvurun.</span><span class="sxs-lookup"><span data-stu-id="11c1f-233">The package is authored incorrectly; contact the package owner to correct the bug.</span></span> |

## <a name="compatibility-errors"></a><span data-ttu-id="11c1f-234">Uyumluluk hataları</span><span class="sxs-lookup"><span data-stu-id="11c1f-234">Compatibility errors</span></span>

<span data-ttu-id="11c1f-235">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="11c1f-235">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span></span>

### <a name="nu1201"></a><span data-ttu-id="11c1f-236">NU1201</span><span class="sxs-lookup"><span data-stu-id="11c1f-236">NU1201</span></span>

| | |
| --- | --- |
| <span data-ttu-id="11c1f-237">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="11c1f-237">**Issue**</span></span> | <span data-ttu-id="11c1f-238">Bir bağımlılık proje Geçerli projeyle uyumlu bir çerçeve içermiyor.</span><span class="sxs-lookup"><span data-stu-id="11c1f-238">A dependency project doesn't contain a framework compatible with the current project.</span></span> <span data-ttu-id="11c1f-239">Genellikle, projenin hedef çerçevesi Süren proje daha yüksek bir sürüme ' dir.</span><span class="sxs-lookup"><span data-stu-id="11c1f-239">Typically, the project's target framework is a higher version than the consuming project.</span></span> |
| <span data-ttu-id="11c1f-240">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="11c1f-240">**Example message**</span></span> | <span data-ttu-id="11c1f-241">*Proje nokta netstandard1.3 ile uyumlu değil (. NETStandard, sürüm = v1.3). Proje nokta destekler:<br/> -netstandard1.6 (. NETStandard, sürüm = v1.6)<br/> -netcoreapp1.0 (. NETCoreApp, sürüm v1.0 =)*</span><span class="sxs-lookup"><span data-stu-id="11c1f-241">*Project ServerWeb is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Project ServerWeb supports:<br/>  - netstandard1.6 (.NETStandard,Version=v1.6)<br/>  - netcoreapp1.0 (.NETCoreApp,Version=v1.0)*</span></span> |
| <span data-ttu-id="11c1f-242">**Çözüm**</span><span class="sxs-lookup"><span data-stu-id="11c1f-242">**Solution**</span></span> | <span data-ttu-id="11c1f-243">Projenin hedef çerçevesi Süren proje eşit veya daha düşük bir sürümden değiştirin.</span><span class="sxs-lookup"><span data-stu-id="11c1f-243">Change the project's target framework to an equal or lower version than the consuming project.</span></span> |

### <a name="nu1202"></a><span data-ttu-id="11c1f-244">NU1202</span><span class="sxs-lookup"><span data-stu-id="11c1f-244">NU1202</span></span>

| | |
| --- | --- |
| <span data-ttu-id="11c1f-245">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="11c1f-245">**Issue**</span></span> | <span data-ttu-id="11c1f-246">Bir bağımlılık paketi projeyle uyumlu tüm varlıkları içermiyor.</span><span class="sxs-lookup"><span data-stu-id="11c1f-246">A dependency package doesn't contain any assets compatible with the project.</span></span> |
| <span data-ttu-id="11c1f-247">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="11c1f-247">**Example message**</span></span> | <span data-ttu-id="11c1f-248">*Paket System.ComponentModel.EventBasedAsync 4.0.11 netstandard1.3 ile uyumlu değil (. NETStandard, sürüm = v1.3). Paket System.ComponentModel.EventBasedAsync 4.0.11 destekler:<br/> -monoandroid10 (MonoAndroid, sürüm = v1.0)<br/> -monotouch10 (MonoTouch, sürüm = v1.0)<br/> -net45 (. NETFramework, sürümü v4.5 =)<br/> -netcore50 (. NETCore, sürüm = v5.0)<br/> -netstandard1.0 (. NETStandard, sürüm = v1.0)<br/> -taşınabilir net45 olduğu win8 + wp8 + wpa81 (. NETPortable, sürüm v0.0, profil = Profile259 =)<br/> -olduğu win8 (Windows, sürüm = v8.0)<br/> -wp8 (WindowsPhone, sürüm v8.0 =)<br/> -wpa81 (WindowsPhoneApp, sürüm v8.1 =)<br/> -xamarinios10 () Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span><span class="sxs-lookup"><span data-stu-id="11c1f-248">*Package System.ComponentModel.EventBasedAsync 4.0.11 is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span></span>|
| <span data-ttu-id="11c1f-249">**Çözüm**</span><span class="sxs-lookup"><span data-stu-id="11c1f-249">**Solution**</span></span> | <span data-ttu-id="11c1f-250">Projenin hedef çerçevesi paket destekleyen bir değiştirin.</span><span class="sxs-lookup"><span data-stu-id="11c1f-250">Change the project's target framework to one that the package supports.</span></span> |

### <a name="nu1203"></a><span data-ttu-id="11c1f-251">NU1203</span><span class="sxs-lookup"><span data-stu-id="11c1f-251">NU1203</span></span>

| | |
| --- | --- |
| <span data-ttu-id="11c1f-252">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="11c1f-252">**Issue**</span></span> | <span data-ttu-id="11c1f-253">Paket projenin desteklemiyor `RuntimeIdentifier`.</span><span class="sxs-lookup"><span data-stu-id="11c1f-253">The package doesn't support the project's `RuntimeIdentifier`.</span></span> |
| <span data-ttu-id="11c1f-254">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="11c1f-254">**Example message**</span></span> | <span data-ttu-id="11c1f-255">*System.Example 1.0.0 a.dll için derleme zamanı referans derlemesini üzerinde net461 sağlar, ancak uyumlu çalışma zamanı derlemesi bulunmuyor.*</span><span class="sxs-lookup"><span data-stu-id="11c1f-255">*System.Example 1.0.0 provides a compile-time reference assembly for a.dll on net461, but there is no compatible run-time assembly.*</span></span> |
| <span data-ttu-id="11c1f-256">**Çözüm**</span><span class="sxs-lookup"><span data-stu-id="11c1f-256">**Solution**</span></span> | <span data-ttu-id="11c1f-257">Değişiklik `RuntimeIdentifier` gerektiğinde projesinde kullanılan değerler.</span><span class="sxs-lookup"><span data-stu-id="11c1f-257">Change the `RuntimeIdentifier` values used in the project as needed.</span></span> |

### <a name="nu1401"></a><span data-ttu-id="11c1f-258">NU1401</span><span class="sxs-lookup"><span data-stu-id="11c1f-258">NU1401</span></span>

| | |
| --- | --- |
| <span data-ttu-id="11c1f-259">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="11c1f-259">**Issue**</span></span> | <span data-ttu-id="11c1f-260">Paket özelliklerini veya şu anda yüklü olan NuGet sürümü tarafından desteklenmeyen çerçeveler gerektirir.</span><span class="sxs-lookup"><span data-stu-id="11c1f-260">The package requires features or frameworks not currently supported by the installed version of NuGet.</span></span> |
| <span data-ttu-id="11c1f-261">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="11c1f-261">**Example message**</span></span> | <span data-ttu-id="11c1f-262">*'NuGet.Versioning' paketi NuGet İstemcisi Sürüm '5.0.0' gerektirir veya üstü, ancak geçerli NuGet sürümü '4.3.0'.*</span><span class="sxs-lookup"><span data-stu-id="11c1f-262">*The 'NuGet.Versioning' package requires NuGet client version '5.0.0' or above, but the current NuGet version is '4.3.0'.*</span></span> |
| <span data-ttu-id="11c1f-263">**Çözüm**</span><span class="sxs-lookup"><span data-stu-id="11c1f-263">**Solution**</span></span> | <span data-ttu-id="11c1f-264">NuGet daha yeni bir sürümü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="11c1f-264">Install a newer version of NuGet.</span></span> <span data-ttu-id="11c1f-265">Bkz: [yükleme NuGet istemci araçları](../install-nuget-client-tools.md).</span><span class="sxs-lookup"><span data-stu-id="11c1f-265">See [Installing NuGet client tools](../install-nuget-client-tools.md).</span></span> |

## <a name="invalid-input-warnings"></a><span data-ttu-id="11c1f-266">Geçersiz giriş uyarıları</span><span class="sxs-lookup"><span data-stu-id="11c1f-266">Invalid input warnings</span></span>

<span data-ttu-id="11c1f-267">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="11c1f-267">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span></span>

### <a name="nu1501"></a><span data-ttu-id="11c1f-268">NU1501</span><span class="sxs-lookup"><span data-stu-id="11c1f-268">NU1501</span></span>

| | |
| --- | --- |
| <span data-ttu-id="11c1f-269">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="11c1f-269">**Issue**</span></span> | <span data-ttu-id="11c1f-270">Proje geri yükleme çalışması çalışıyor üzerinde bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="11c1f-270">The project restore is attempting to operate on was not found.</span></span> |
| <span data-ttu-id="11c1f-271">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="11c1f-271">**Example message**</span></span> | <span data-ttu-id="11c1f-272">*'C:\projects\a' klasörü geri yüklenecek bir proje içermiyor.*</span><span class="sxs-lookup"><span data-stu-id="11c1f-272">*The folder 'c:\projects\a' does not contain a project to restore.*</span></span> |
| <span data-ttu-id="11c1f-273">**Çözüm**</span><span class="sxs-lookup"><span data-stu-id="11c1f-273">**Solution**</span></span> | <span data-ttu-id="11c1f-274">Nuget restore bir proje içeren bir klasörde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="11c1f-274">Run nuget restore in a folder that contains a project.</span></span> |

### <a name="nu1502"></a><span data-ttu-id="11c1f-275">NU1502</span><span class="sxs-lookup"><span data-stu-id="11c1f-275">NU1502</span></span>

| | |
| --- | --- |
| <span data-ttu-id="11c1f-276">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="11c1f-276">**Issue**</span></span> | <span data-ttu-id="11c1f-277">`RuntimeSupports` Geçersiz bir profil içerir.</span><span class="sxs-lookup"><span data-stu-id="11c1f-277">`RuntimeSupports` contains an invalid profile.</span></span> <span data-ttu-id="11c1f-278">Genellikle, destekler profili bulunamadı bir `runtime.json` geçerli bağımlılık paketleri dosyasından.</span><span class="sxs-lookup"><span data-stu-id="11c1f-278">Typically, the supports profile was not found in a `runtime.json` file from the current dependency packages.</span></span>|
| <span data-ttu-id="11c1f-279">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="11c1f-279">**Example message**</span></span> | <span data-ttu-id="11c1f-280">*Bilinmeyen uyumluluk profili: aaa*</span><span class="sxs-lookup"><span data-stu-id="11c1f-280">*Unknown Compatibility Profile: aaa*</span></span> |
| <span data-ttu-id="11c1f-281">**Çözüm**</span><span class="sxs-lookup"><span data-stu-id="11c1f-281">**Solution**</span></span> | <span data-ttu-id="11c1f-282">Denetleme `RuntimeSupports` projenizdeki değeri.</span><span class="sxs-lookup"><span data-stu-id="11c1f-282">Check the `RuntimeSupports` value in your project.</span></span> |

### <a name="nu1503"></a><span data-ttu-id="11c1f-283">NU1503</span><span class="sxs-lookup"><span data-stu-id="11c1f-283">NU1503</span></span>

| | |
| --- | --- |
| <span data-ttu-id="11c1f-284">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="11c1f-284">**Issue**</span></span> | <span data-ttu-id="11c1f-285">Bir bağımlılık proje Nuget'in geri yükleme hedeflerini içe aktarmaz.</span><span class="sxs-lookup"><span data-stu-id="11c1f-285">A dependency project doesn't import NuGet's restore targets.</span></span> <span data-ttu-id="11c1f-286">Bu NU1105 için benzer ancak burada proje atlanır ve tüm geri yükleme başarısız olmasına neden yerine yoksayıldı.</span><span class="sxs-lookup"><span data-stu-id="11c1f-286">This is similar to NU1105 but here the project is skipped and ignored instead of causing all of restore to fail.</span></span> <span data-ttu-id="11c1f-287">Karmaşık çözümlerinde çoğunlukla diğer geri yükleme desteklemeyebilir proje türleri vardır.</span><span class="sxs-lookup"><span data-stu-id="11c1f-287">In complex solutions there are often other types of projects that may not support restore.</span></span> |
| <span data-ttu-id="11c1f-288">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="11c1f-288">**Example message**</span></span> | <span data-ttu-id="11c1f-289">*Proje 'c:\a.csproj' için geri atlanıyor. Proje dosyası geçersiz veya eksik hedefleri geri yüklemek için gerekli olabilir.*</span><span class="sxs-lookup"><span data-stu-id="11c1f-289">*Skipping restore for project 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="11c1f-290">**Çözüm**</span><span class="sxs-lookup"><span data-stu-id="11c1f-290">**Solution**</span></span> | <span data-ttu-id="11c1f-291">Bu ortak özellik/geri yükleme otomatik olarak içeri hedefleri almayın projelerde meydana gelebilir.</span><span class="sxs-lookup"><span data-stu-id="11c1f-291">This can happen for projects that do not import common props/targets which automatically import restore.</span></span> <span data-ttu-id="11c1f-292">Proje geri gerekmez, bu yoksayılabilir.</span><span class="sxs-lookup"><span data-stu-id="11c1f-292">If the project doesn't need to be restored this can be ignored.</span></span> <span data-ttu-id="11c1f-293">Aksi takdirde, geri yükleme hedeflerini eklemek için etkilenen proje düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="11c1f-293">Otherwise, edit the affected project to add targets for restore.</span></span> |

## <a name="unexpected-package-version-warnings"></a><span data-ttu-id="11c1f-294">Beklenmeyen Paket sürümü uyarıları</span><span class="sxs-lookup"><span data-stu-id="11c1f-294">Unexpected package version warnings</span></span>

<span data-ttu-id="11c1f-295">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="11c1f-295">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span></span>

### <a name="nu1601"></a><span data-ttu-id="11c1f-296">NU1601</span><span class="sxs-lookup"><span data-stu-id="11c1f-296">NU1601</span></span>

| | |
| --- | --- |
| <span data-ttu-id="11c1f-297">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="11c1f-297">**Issue**</span></span> | <span data-ttu-id="11c1f-298">Bir doğrudan proje bağımlılığı belirtilen proje daha yüksek bir sürüme indirgenmesine.</span><span class="sxs-lookup"><span data-stu-id="11c1f-298">A direct project dependency was bumped to a higher version than the project specified.</span></span> |
| <span data-ttu-id="11c1f-299">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="11c1f-299">**Example message**</span></span> | <span data-ttu-id="11c1f-300">*Bağımlılık belirtildi NuGet.Versioning (> = 3.5.0) ancak 4.0.0 NuGet.Versioning ile sonuçlandı.*</span><span class="sxs-lookup"><span data-stu-id="11c1f-300">*Dependency specified was NuGet.Versioning (>= 3.5.0) but ended up with NuGet.Versioning 4.0.0.*</span></span> |
| <span data-ttu-id="11c1f-301">**Çözüm**</span><span class="sxs-lookup"><span data-stu-id="11c1f-301">**Solution**</span></span> | <span data-ttu-id="11c1f-302">Proje bağımlılığı uygun bir sürüme güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="11c1f-302">Update the dependency in the project to an appropriate version.</span></span> |

### <a name="nu1602"></a><span data-ttu-id="11c1f-303">NU1602</span><span class="sxs-lookup"><span data-stu-id="11c1f-303">NU1602</span></span>

| | |
| --- | --- |
| <span data-ttu-id="11c1f-304">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="11c1f-304">**Issue**</span></span> | <span data-ttu-id="11c1f-305">Bir paket bağımlılığı alt sınır eksik.</span><span class="sxs-lookup"><span data-stu-id="11c1f-305">A package dependency is missing a lower bound.</span></span> <span data-ttu-id="11c1f-306">Bunu bulmak geri yükleme izin vermeyen *en iyi eşleşmeyi*.</span><span class="sxs-lookup"><span data-stu-id="11c1f-306">This doesn't allow restore to find the *best match*.</span></span> <span data-ttu-id="11c1f-307">Her geri yükleme, aşağı doğru hareket kullanılabilir daha düşük bir sürüm bulunmaya çalışılırken float.</span><span class="sxs-lookup"><span data-stu-id="11c1f-307">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="11c1f-308">Bu geri yükleme zaten paketleri kullanıcı paket klasöründe kullanmak yerine her zaman tüm kaynakları denetlemek için çevrimiçi duruma geçtiğinde anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="11c1f-308">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="11c1f-309">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="11c1f-309">**Example message**</span></span> | <span data-ttu-id="11c1f-310">*NuGet.Packaging 4.0.0 (bunlar dahil) bir alt sınır için bağımlılık NuGet.Versioning (> 3.5.0) sağlamaz. Yaklaşık en iyi eşleşme 3.6.0, çözüldü.*</span><span class="sxs-lookup"><span data-stu-id="11c1f-310">*NuGet.Packaging 4.0.0 does not provide an inclusive lower bound for dependency NuGet.Versioning (> 3.5.0). An approximate best match of 3.6.0 was resolved.*</span></span> |
| <span data-ttu-id="11c1f-311">**Çözüm**</span><span class="sxs-lookup"><span data-stu-id="11c1f-311">**Solution**</span></span> | <span data-ttu-id="11c1f-312">Bu genellikle hata yazma bir pakettir.</span><span class="sxs-lookup"><span data-stu-id="11c1f-312">This is usually a package authoring error.</span></span> <span data-ttu-id="11c1f-313">Bu sorunu çözmek için paket yazarına danışın.</span><span class="sxs-lookup"><span data-stu-id="11c1f-313">Contact the package author to resolve the issue.</span></span> |

### <a name="nu1603"></a><span data-ttu-id="11c1f-314">NU1603</span><span class="sxs-lookup"><span data-stu-id="11c1f-314">NU1603</span></span>

| | |
| --- | --- |
| <span data-ttu-id="11c1f-315">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="11c1f-315">**Issue**</span></span> | <span data-ttu-id="11c1f-316">Bir paket bağımlılığı bulunamadı bir sürüm belirtildi.</span><span class="sxs-lookup"><span data-stu-id="11c1f-316">A package dependency specified a version that could not be found.</span></span> <span data-ttu-id="11c1f-317">Genellikle, paket kaynaklarını beklenen alt sınır sürüm içermiyor.</span><span class="sxs-lookup"><span data-stu-id="11c1f-317">Typically, the package sources do not contain the expected lower bound version.</span></span> <span data-ttu-id="11c1f-318">Bunun yerine, daha yüksek bir sürüm ne paket karşı yönetilmiyor öğesinden farklı kullanıldı.</span><span class="sxs-lookup"><span data-stu-id="11c1f-318">A higher version was used instead, which differs from what the package was authored against.</span></span><br/><br/><span data-ttu-id="11c1f-319">Bu geri yükleme bulamadı anlamına gelir *en iyi eşleşmeyi*.</span><span class="sxs-lookup"><span data-stu-id="11c1f-319">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="11c1f-320">Her geri yükleme, aşağı doğru hareket kullanılabilir daha düşük bir sürüm bulunmaya çalışılırken float.</span><span class="sxs-lookup"><span data-stu-id="11c1f-320">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="11c1f-321">Bu geri yükleme zaten paketleri kullanıcı paket klasöründe kullanmak yerine her zaman tüm kaynakları denetlemek için çevrimiçi duruma geçtiğinde anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="11c1f-321">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="11c1f-322">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="11c1f-322">**Example message**</span></span> | <span data-ttu-id="11c1f-323">NuGet.Packaging 4.0.0 NuGet.Versioning üzerinde bağlıdır (> = 4.0.0) ancak 4.0.0 bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="11c1f-323">NuGet.Packaging 4.0.0 depends on NuGet.Versioning (>= 4.0.0) but 4.0.0 was not found.</span></span> <span data-ttu-id="11c1f-324">Yaklaşık en iyi eşleşme 5.0.0, çözüldü.</span><span class="sxs-lookup"><span data-stu-id="11c1f-324">An approximate best match of 5.0.0 was resolved.</span></span> |
| <span data-ttu-id="11c1f-325">**Çözüm**</span><span class="sxs-lookup"><span data-stu-id="11c1f-325">**Solution**</span></span> | <span data-ttu-id="11c1f-326">Beklenen paket bırakılmamışsa değilse bu hata yazma bir paket olabilir.</span><span class="sxs-lookup"><span data-stu-id="11c1f-326">If the package expected has not been released then this may be a package authoring error.</span></span> <span data-ttu-id="11c1f-327">Bu sorunu çözmek için paket yazarına danışın.</span><span class="sxs-lookup"><span data-stu-id="11c1f-327">Contact the package author to resolve the issue.</span></span> <span data-ttu-id="11c1f-328">Paket yayımlanan, kullanmakta olduğunuz paket kaynaklarını üzerinde kullanılabilir olduğunu denetleyin.</span><span class="sxs-lookup"><span data-stu-id="11c1f-328">If the package has been released, then check that it's available on the package sources you're using.</span></span> <span data-ttu-id="11c1f-329">Özel kaynak kullanıyorsanız, akış paketi güncelleştirmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="11c1f-329">If using a private source, you may need to update the package on that feed.</span></span> |

### <a name="nu1604"></a><span data-ttu-id="11c1f-330">NU1604</span><span class="sxs-lookup"><span data-stu-id="11c1f-330">NU1604</span></span>

| | |
| --- | --- |
| <span data-ttu-id="11c1f-331">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="11c1f-331">**Issue**</span></span> | <span data-ttu-id="11c1f-332">Proje bağımlılığı alt sınır tanımlamıyor.</span><span class="sxs-lookup"><span data-stu-id="11c1f-332">A project dependency doesn't define a lower bound.</span></span><br/><br/><span data-ttu-id="11c1f-333">Bu geri yükleme bulamadı anlamına gelir *en iyi eşleşmeyi*.</span><span class="sxs-lookup"><span data-stu-id="11c1f-333">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="11c1f-334">Her geri yükleme, aşağı doğru hareket kullanılabilir daha düşük bir sürüm bulunmaya çalışılırken float.</span><span class="sxs-lookup"><span data-stu-id="11c1f-334">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="11c1f-335">Bu geri yükleme zaten paketleri kullanıcı paket klasöründe kullanmak yerine her zaman tüm kaynakları denetlemek için çevrimiçi duruma geçtiğinde anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="11c1f-335">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="11c1f-336">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="11c1f-336">**Example message**</span></span> | <span data-ttu-id="11c1f-337">*Bağımlılık NuGet.Versioning proje (< 9.0.0 =) doe (bunlar dahil) bir alt sınır içeremez. Alt sınır tutarlı geri yükleme sonuçlar sağlamak için bağımlılık sürümünü içerir.*</span><span class="sxs-lookup"><span data-stu-id="11c1f-337">*Project dependency NuGet.Versioning (<= 9.0.0) doe not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span> |
| <span data-ttu-id="11c1f-338">**Çözüm**</span><span class="sxs-lookup"><span data-stu-id="11c1f-338">**Solution**</span></span> | <span data-ttu-id="11c1f-339">Projenin güncelleştirme `PackageReference` `Version` alt sınır eklenecek özniteliği.</span><span class="sxs-lookup"><span data-stu-id="11c1f-339">Update the project's `PackageReference` `Version` attribute to include a lower bound.</span></span> |

### <a name="nu1605"></a><span data-ttu-id="11c1f-340">NU1605</span><span class="sxs-lookup"><span data-stu-id="11c1f-340">NU1605</span></span>

| | |
| --- | --- |
| <span data-ttu-id="11c1f-341">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="11c1f-341">**Issue**</span></span> | <span data-ttu-id="11c1f-342">Bir bağımlılık paketi bir paket geri yükleme sonuçta çözülmüş daha yüksek bir sürüm bir sürüm kısıtlaması belirtildi.</span><span class="sxs-lookup"><span data-stu-id="11c1f-342">A dependency package specified a version constraint on a higher version of a package than restore ultimately resolved.</span></span> <span data-ttu-id="11c1f-343">Diğer bir deyişle, paketleri çözülürken "en yakın WINS" kural nedeniyle, grafik yakın bir pakette uzaktaki bir paket silmiş.</span><span class="sxs-lookup"><span data-stu-id="11c1f-343">That is, because of the "nearest wins" rule when resolving packages, a nearer package in the graph may have overridden a distant package.</span></span> |
| <span data-ttu-id="11c1f-344">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="11c1f-344">**Example message**</span></span> | <span data-ttu-id="11c1f-345">*Paket indirgeme algılandı: 4.0.0 gelen NuGet.Versioning 3.5.0 için. Paketi farklı bir sürüm seçmek için doğrudan projeden başvuru.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 NuGet.Versioning 4.0.0 ->*</span><span class="sxs-lookup"><span data-stu-id="11c1f-345">*Detected package downgrade: NuGet.Versioning from 4.0.0 to 3.5.0. Reference the package directly from the project to select a different version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span></span> |
| <span data-ttu-id="11c1f-346">**Çözüm**</span><span class="sxs-lookup"><span data-stu-id="11c1f-346">**Solution**</span></span> | <span data-ttu-id="11c1f-347">Proje için kullanmak istediğiniz paketinin daha yüksek sürümünü doğrudan bir başvuru ekleyin.</span><span class="sxs-lookup"><span data-stu-id="11c1f-347">Add a direct reference to the project for the higher version of the package that you want to use.</span></span> |

## <a name="resolver-conflict-warnings"></a><span data-ttu-id="11c1f-348">Çözümleyici çakışma uyarıları</span><span class="sxs-lookup"><span data-stu-id="11c1f-348">Resolver conflict warnings</span></span>

### <a name="nu1608"></a><span data-ttu-id="11c1f-349">NU1608</span><span class="sxs-lookup"><span data-stu-id="11c1f-349">NU1608</span></span>

| | |
| --- | --- |
| <span data-ttu-id="11c1f-350">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="11c1f-350">**Issue**</span></span> | <span data-ttu-id="11c1f-351">Çözümlenen bir paketi bir bağımlılık kısıtlaması izin verdiğinden daha yüksektir.</span><span class="sxs-lookup"><span data-stu-id="11c1f-351">A resolved package is higher than a dependency constraint allows.</span></span> <span data-ttu-id="11c1f-352">Başka bir deyişle, doğrudan bir proje tarafından başvurulan paket diğer paketlerinden bağımlılık kısıtlamalarını geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="11c1f-352">This means that a package referenced directly by a project overrides dependency constraints from other packages.</span></span>|
| <span data-ttu-id="11c1f-353">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="11c1f-353">**Example message**</span></span> | <span data-ttu-id="11c1f-354">*Bağımlılık kısıtlaması dışında algılanan Paket sürümü: x 1.0.0 (= 1.0.0) y gerektiriyor, ancak sürüm y 2.0.0 çözülmüş.*</span><span class="sxs-lookup"><span data-stu-id="11c1f-354">*Detected package version outside of dependency constraint: x 1.0.0 requires y (= 1.0.0) but version y 2.0.0 was resolved.*</span></span> |
| <span data-ttu-id="11c1f-355">**Çözüm**</span><span class="sxs-lookup"><span data-stu-id="11c1f-355">**Solution**</span></span> | <span data-ttu-id="11c1f-356">Bazı durumlarda bu bilinen bir durumdur ve uyarıyı gizlenebilir.</span><span class="sxs-lookup"><span data-stu-id="11c1f-356">In some cases this is intentional and the warning can be suppressed.</span></span> <span data-ttu-id="11c1f-357">Aksi durumda, kendi sürüm kısıtlamaları genişletmek için paketi projenin referansı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="11c1f-357">Otherwise, change the project's reference to the package to widen its version constraints.</span></span> |

## <a name="package-fallback-warnings"></a><span data-ttu-id="11c1f-358">Paket geri dönüş uyarıları</span><span class="sxs-lookup"><span data-stu-id="11c1f-358">Package fallback warnings</span></span>

### <a name="nu1701"></a><span data-ttu-id="11c1f-359">NU1701</span><span class="sxs-lookup"><span data-stu-id="11c1f-359">NU1701</span></span>

| | |
| --- | --- |
| <span data-ttu-id="11c1f-360">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="11c1f-360">**Issue**</span></span> | <span data-ttu-id="11c1f-361">`PackageTargetFallback` / `AssetTargetFallback` varlıklar bir paket seçmek için kullanıldı.</span><span class="sxs-lookup"><span data-stu-id="11c1f-361">`PackageTargetFallback` / `AssetTargetFallback` was used to select assets from a package.</span></span> <span data-ttu-id="11c1f-362">Uyarı varlıklar % 100 uyumlu olmayabilir bilmenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="11c1f-362">The warning let users know that the assets may not be 100% compatible.</span></span> |
| <span data-ttu-id="11c1f-363">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="11c1f-363">**Example message**</span></span> | <span data-ttu-id="11c1f-364">*Paket 'NuGet.Versioning', 'taşınabilir net45 + olduğu win8' yerine projenin hedef çerçevesi 'netstandard1.5' kullanılarak geri yüklendi. Bu paket projenizi ile tamamen uyumlu olmayabilir.*</span><span class="sxs-lookup"><span data-stu-id="11c1f-364">*Package 'NuGet.Versioning' was restored using 'portable-net45+win8' instead the project target framework 'netstandard1.5'. This package may not be fully compatible with your project.*</span></span> |
| <span data-ttu-id="11c1f-365">**Çözüm**</span><span class="sxs-lookup"><span data-stu-id="11c1f-365">**Solution**</span></span> | <span data-ttu-id="11c1f-366">Projenin hedef çerçevesi paket destekleyen bir değiştirin.</span><span class="sxs-lookup"><span data-stu-id="11c1f-366">Change the project's target framework to one that the package supports.</span></span> |

## <a name="feed-warnings"></a><span data-ttu-id="11c1f-367">Akış uyarıları</span><span class="sxs-lookup"><span data-stu-id="11c1f-367">Feed warnings</span></span>

### <a name="nu1801"></a><span data-ttu-id="11c1f-368">NU1801</span><span class="sxs-lookup"><span data-stu-id="11c1f-368">NU1801</span></span>

| | |
| --- | --- |
| <span data-ttu-id="11c1f-369">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="11c1f-369">**Issue**</span></span> | <span data-ttu-id="11c1f-370">Akış okunurken bir hata oluştu, `IgnoreFailedSources` ayarlanır için önemli olmayan uyarı dönüştürme true.</span><span class="sxs-lookup"><span data-stu-id="11c1f-370">An error occurred when reading the feed when `IgnoreFailedSources` is set to true, converting it to a non-fatal warning.</span></span> <span data-ttu-id="11c1f-371">Bu herhangi bir iletisi içerebilir ve genel.</span><span class="sxs-lookup"><span data-stu-id="11c1f-371">This could contain any message and is generic.</span></span> |
| <span data-ttu-id="11c1f-372">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="11c1f-372">**Example message**</span></span> | <span data-ttu-id="11c1f-373">yok</span><span class="sxs-lookup"><span data-stu-id="11c1f-373">n/a</span></span> |
| <span data-ttu-id="11c1f-374">**Çözüm**</span><span class="sxs-lookup"><span data-stu-id="11c1f-374">**Solution**</span></span> | <span data-ttu-id="11c1f-375">Geçerli kaynakları belirtmek için yapılandırmasını düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="11c1f-375">Edit your configuration to specify valid sources.</span></span> |

## <a name="nuget-internal-errors-and-warnings"></a><span data-ttu-id="11c1f-376">NuGet iç hatalar ve uyarılar</span><span class="sxs-lookup"><span data-stu-id="11c1f-376">NuGet internal errors and warnings</span></span>

<span data-ttu-id="11c1f-377">[NU1000](#nu1000) | [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="11c1f-377">[NU1000](#nu1000) | [NU1500](#nu1500)</span></span>

### <a name="nu1000"></a><span data-ttu-id="11c1f-378">NU1000</span><span class="sxs-lookup"><span data-stu-id="11c1f-378">NU1000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="11c1f-379">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="11c1f-379">**Issue**</span></span> | <span data-ttu-id="11c1f-380">NuGet from olmayan belirli bir iç hata.</span><span class="sxs-lookup"><span data-stu-id="11c1f-380">A non specific internal error from NuGet.</span></span> |
| <span data-ttu-id="11c1f-381">**Çözüm**</span><span class="sxs-lookup"><span data-stu-id="11c1f-381">**Solution**</span></span> | <span data-ttu-id="11c1f-382">Daha fazla bilgi için günlükleri denetleyin</span><span class="sxs-lookup"><span data-stu-id="11c1f-382">Check the logs for more information</span></span> |

### <a name="nu1500"></a><span data-ttu-id="11c1f-383">NU1500</span><span class="sxs-lookup"><span data-stu-id="11c1f-383">NU1500</span></span>

| | |
| --- | --- |
| <span data-ttu-id="11c1f-384">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="11c1f-384">**Issue**</span></span> | <span data-ttu-id="11c1f-385">Belirsiz bir iç uyarıyı NuGet engeller.</span><span class="sxs-lookup"><span data-stu-id="11c1f-385">A non specific internal warning from NuGet.</span></span> |
| <span data-ttu-id="11c1f-386">**Çözüm**</span><span class="sxs-lookup"><span data-stu-id="11c1f-386">**Solution**</span></span> | <span data-ttu-id="11c1f-387">Daha fazla bilgi için günlükleri denetleyin</span><span class="sxs-lookup"><span data-stu-id="11c1f-387">Check the logs for more information</span></span> |

## <a name="signed-packages-creation-and-verification"></a><span data-ttu-id="11c1f-388">İmzalı Paketleri (oluşturma ve doğrulama)</span><span class="sxs-lookup"><span data-stu-id="11c1f-388">Signed packages (creation and verification)</span></span>

<span data-ttu-id="11c1f-389">*NuGet 4.6.0+*</span><span class="sxs-lookup"><span data-stu-id="11c1f-389">*NuGet 4.6.0+*</span></span>

<span data-ttu-id="11c1f-390">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008)  |  [NU3018](#nu3018) | [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="11c1f-390">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span></span>

### <a name="nu3000"></a><span data-ttu-id="11c1f-391">NU3000</span><span class="sxs-lookup"><span data-stu-id="11c1f-391">NU3000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="11c1f-392">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="11c1f-392">**Issue**</span></span> | <span data-ttu-id="11c1f-393">Belirli olmayan bir hata paket imzalama ile ilgili ve paket doğrulama imzalanmış.</span><span class="sxs-lookup"><span data-stu-id="11c1f-393">A non-specific error related to package signing and signed package verification.</span></span> |
| <span data-ttu-id="11c1f-394">**Çözüm**</span><span class="sxs-lookup"><span data-stu-id="11c1f-394">**Solution**</span></span> | <span data-ttu-id="11c1f-395">Daha fazla bilgi için günlükleri denetleyin.</span><span class="sxs-lookup"><span data-stu-id="11c1f-395">Check the logs for more information.</span></span> |

### <a name="nu3001"></a><span data-ttu-id="11c1f-396">NU3001</span><span class="sxs-lookup"><span data-stu-id="11c1f-396">NU3001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="11c1f-397">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="11c1f-397">**Issue**</span></span> | <span data-ttu-id="11c1f-398">Geçersiz bağımsız değişkenler ya da [oturum komutu](../tools/cli-ref-sign.md) veya [komut doğrulama](../tools/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="11c1f-398">Invalid arguments to either the [sign command](../tools/cli-ref-sign.md) or the [verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="11c1f-399">**Çözüm**</span><span class="sxs-lookup"><span data-stu-id="11c1f-399">**Solution**</span></span> | <span data-ttu-id="11c1f-400">Denetleyin ve sağlanan bağımsız değişkenler düzeltin.</span><span class="sxs-lookup"><span data-stu-id="11c1f-400">Check and correct the arguments provided.</span></span> |

### <a name="nu3002"></a><span data-ttu-id="11c1f-401">NU3002</span><span class="sxs-lookup"><span data-stu-id="11c1f-401">NU3002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="11c1f-402">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="11c1f-402">**Issue**</span></span> | <span data-ttu-id="11c1f-403">`-Timestamper` Seçeneği ile belirtilmemiş [nuget oturum komutu](../tools/cli-ref-sign.md).</span><span class="sxs-lookup"><span data-stu-id="11c1f-403">The `-Timestamper` option was not specified with the [nuget sign command](../tools/cli-ref-sign.md).</span></span> |
| <span data-ttu-id="11c1f-404">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="11c1f-404">**Example message**</span></span> | <span data-ttu-id="11c1f-405">*'-Timestamper' seçeneği sağlanan değil. İmzalı paket zaman damgalı olmaz.*</span><span class="sxs-lookup"><span data-stu-id="11c1f-405">*The '-Timestamper' option was not provided. The signed package will not be timestamped.*</span></span> |
| <span data-ttu-id="11c1f-406">**Çözüm**</span><span class="sxs-lookup"><span data-stu-id="11c1f-406">**Solution**</span></span> | <span data-ttu-id="11c1f-407">Belirtin `-Timestamper` seçeneğini `nuget sign`.</span><span class="sxs-lookup"><span data-stu-id="11c1f-407">Specify the `-Timestamper` option with `nuget sign`.</span></span> |

### <a name="nu3004"></a><span data-ttu-id="11c1f-408">NU3004</span><span class="sxs-lookup"><span data-stu-id="11c1f-408">NU3004</span></span>

| | |
| --- | --- |
| <span data-ttu-id="11c1f-409">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="11c1f-409">**Issue**</span></span> | <span data-ttu-id="11c1f-410">İmzasız bir paket için sağlanan [nuget doğrulayın komutu](../tools/cli-ref-verify.md).</span><span class="sxs-lookup"><span data-stu-id="11c1f-410">An unsigned package was provided to the [nuget verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="11c1f-411">**Çözüm**</span><span class="sxs-lookup"><span data-stu-id="11c1f-411">**Solution**</span></span> | <span data-ttu-id="11c1f-412">Çalıştırma `nuget verify` imzalı paketine sahip.</span><span class="sxs-lookup"><span data-stu-id="11c1f-412">Run `nuget verify` with a signed package.</span></span> <span data-ttu-id="11c1f-413">Bkz: [bir paket oturum](../create-packages/Sign-a-Package.md).</span><span class="sxs-lookup"><span data-stu-id="11c1f-413">See [Sign a package](../create-packages/Sign-a-Package.md).</span></span> |

### <a name="nu3008"></a><span data-ttu-id="11c1f-414">NU3008</span><span class="sxs-lookup"><span data-stu-id="11c1f-414">NU3008</span></span>

| | |
| --- | --- |
| <span data-ttu-id="11c1f-415">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="11c1f-415">**Issue**</span></span> | <span data-ttu-id="11c1f-416">Paket bütünlük denetimi başarısız oldu, imzalı itibaren imzalı paketi ile uğradığını anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="11c1f-416">The package integrity check failed, meaning that a signed package was tampered with since being signed.</span></span> |
| <span data-ttu-id="11c1f-417">**Çözüm**</span><span class="sxs-lookup"><span data-stu-id="11c1f-417">**Solution**</span></span> | <span data-ttu-id="11c1f-418">Virüsten koruma yazılımı ile bilgisayarınızı tarayın.</span><span class="sxs-lookup"><span data-stu-id="11c1f-418">Scan your computer with anti-virus software.</span></span> <span data-ttu-id="11c1f-419">Ardından paket bilgisayardan kaldırın, yükleyin ve işlemi yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="11c1f-419">Then remove the package from the computer, reinstall it, and try the operation again.</span></span> <span data-ttu-id="11c1f-420">Sorun devam ederse, paket kaynağının sahibi ve paket sahibine başvurun.</span><span class="sxs-lookup"><span data-stu-id="11c1f-420">If the problem persists, contact the owner of the package source and the package owner.</span></span> |

### <a name="nu3018"></a><span data-ttu-id="11c1f-421">NU3018</span><span class="sxs-lookup"><span data-stu-id="11c1f-421">NU3018</span></span>

| | |
| --- | --- |
| <span data-ttu-id="11c1f-422">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="11c1f-422">**Issue**</span></span> | <span data-ttu-id="11c1f-423">Sertifika zinciri oluşturma için birincil imza başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="11c1f-423">Certificate chain building failed for the primary signature.</span></span> <span data-ttu-id="11c1f-424">Birincil imzalama sertifikası iptal edildi, güvenilmeyen, veya sertifika için iptal bilgilerini kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="11c1f-424">The primary signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="11c1f-425">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="11c1f-425">**Example message**</span></span> | <span data-ttu-id="11c1f-426">*Uyarı: NU3018: iptal işlevi sertifika için İptal denetleyemedi.*</span><span class="sxs-lookup"><span data-stu-id="11c1f-426">*WARNING: NU3018: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="11c1f-427">**Çözüm**</span><span class="sxs-lookup"><span data-stu-id="11c1f-427">**Solution**</span></span> | <span data-ttu-id="11c1f-428">Güvenilir ve geçerli bir sertifika kullanın.</span><span class="sxs-lookup"><span data-stu-id="11c1f-428">Use a trusted and valid certificate.</span></span> <span data-ttu-id="11c1f-429">İnternet bağlantısını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="11c1f-429">Check internet connectivity.</span></span> |

### <a name="nu3028"></a><span data-ttu-id="11c1f-430">NU3028</span><span class="sxs-lookup"><span data-stu-id="11c1f-430">NU3028</span></span>

| | |
| --- | --- |
| <span data-ttu-id="11c1f-431">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="11c1f-431">**Issue**</span></span> | <span data-ttu-id="11c1f-432">Sertifika zinciri oluşturma zaman damgası imza için başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="11c1f-432">Certificate chain building failed for the timestamp signature.</span></span> <span data-ttu-id="11c1f-433">Zaman damgası imzalama sertifikası iptal edildi, güvenilmeyen, veya sertifika için iptal bilgilerini kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="11c1f-433">The timestamp signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="11c1f-434">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="11c1f-434">**Example message**</span></span> | <span data-ttu-id="11c1f-435">*Uyarı: NU3028: iptal işlevi sertifika için İptal denetleyemedi.*</span><span class="sxs-lookup"><span data-stu-id="11c1f-435">*WARNING: NU3028: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="11c1f-436">**Çözüm**</span><span class="sxs-lookup"><span data-stu-id="11c1f-436">**Solution**</span></span> | <span data-ttu-id="11c1f-437">Güvenilir ve geçerli bir sertifika kullanın.</span><span class="sxs-lookup"><span data-stu-id="11c1f-437">Use a trusted and valid certificate.</span></span> <span data-ttu-id="11c1f-438">İnternet bağlantısını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="11c1f-438">Check internet connectivity.</span></span> |
