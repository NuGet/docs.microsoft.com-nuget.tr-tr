---
title: "NuGet geri yükleme hataları ve Uyarıları başvurusu | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/13/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: b76b8a00-7155-4163-b533-894086d2ef78
description: "Tam başvuru için uyarıları ve hataları NuGet paket geri yüklemesi sırasında verilen"
keywords: "NuGet hatalar, NuGet uyarılar tanılama"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: 53fccbb86f2920d870b5383070d043e25045a626
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/05/2018
---
# <a name="errors-and-warnings"></a><span data-ttu-id="6a039-104">Hatalar ve uyarılar</span><span class="sxs-lookup"><span data-stu-id="6a039-104">Errors and warnings</span></span>

<span data-ttu-id="6a039-105">NuGet 4.3.0, hataları ve Uyarıları Bu konu başlığı altında açıklandığı gibi numaralı ve ilgili sorunları gidermek amacıyla ayrıntılı bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="6a039-105">In NuGet 4.3.0, errors and warnings are numbered as described in this topic and provide detailed information to help you address the issues involved.</span></span> 

<span data-ttu-id="6a039-106">Hatalar ve uyarılar burada listelenen yalnızca [PackageReference tabanlı](../Consume-Packages/Package-References-in-Project-Files.md) projeleri ve NuGet 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="6a039-106">The errors and warnings listed here are available only with [PackageReference-based](../Consume-Packages/Package-References-in-Project-Files.md) projects and NuGet 4.3.0.</span></span> <span data-ttu-id="6a039-107">NuGet uyarıları bastırma veya hataları yükseltmesine MSBuild özellikleri de geliştirir.</span><span class="sxs-lookup"><span data-stu-id="6a039-107">NuGet also honors MSBuild properties to suppress warnings or elevate them to errors.</span></span> <span data-ttu-id="6a039-108">Daha fazla bilgi için bkz: [nasıl yapılır: Derleyici uyarılarını bastırma](/visualstudio/ide/how-to-suppress-compiler-warnings) Visual Studio belgelerinde.</span><span class="sxs-lookup"><span data-stu-id="6a039-108">For more information, see [How to: Suppress Compiler Warnings](/visualstudio/ide/how-to-suppress-compiler-warnings) in the Visual Studio documentation.</span></span>

<span data-ttu-id="6a039-109">**Hataları**</span><span class="sxs-lookup"><span data-stu-id="6a039-109">**Errors**</span></span>

| <span data-ttu-id="6a039-110">Grup</span><span class="sxs-lookup"><span data-stu-id="6a039-110">Group</span></span> | <span data-ttu-id="6a039-111">Hata numaraları</span><span class="sxs-lookup"><span data-stu-id="6a039-111">Error Numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="6a039-112">Geçersiz giriş hataları</span><span class="sxs-lookup"><span data-stu-id="6a039-112">Invalid input errors</span></span>](#invalid-input-errors) | <span data-ttu-id="6a039-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="6a039-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span></span> |
| [<span data-ttu-id="6a039-114">Eksik paket ve proje hataları</span><span class="sxs-lookup"><span data-stu-id="6a039-114">Missing package and project errors</span></span>](#missing-package-and-project-errors) | <span data-ttu-id="6a039-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [ NU1106](#nu1106), [NU1107](#nu1107) (daha önce NU1607) [NU1108](#nu1107) (daha önce NU1606)</span><span class="sxs-lookup"><span data-stu-id="6a039-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1107) (previously NU1606)</span></span> |
| [<span data-ttu-id="6a039-116">Uyumluluk hataları</span><span class="sxs-lookup"><span data-stu-id="6a039-116">Compatibility errors</span></span>](#compatibility-errors) | <span data-ttu-id="6a039-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="6a039-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span></span> |

<span data-ttu-id="6a039-118">**Uyarıları**</span><span class="sxs-lookup"><span data-stu-id="6a039-118">**Warnings**</span></span>

| <span data-ttu-id="6a039-119">Grup</span><span class="sxs-lookup"><span data-stu-id="6a039-119">Group</span></span> | <span data-ttu-id="6a039-120">Uyarı numaraları</span><span class="sxs-lookup"><span data-stu-id="6a039-120">Warning numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="6a039-121">Geçersiz giriş uyarıları</span><span class="sxs-lookup"><span data-stu-id="6a039-121">Invalid input warnings</span></span>](#invalid-input-warnings) | <span data-ttu-id="6a039-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="6a039-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span></span> |
| [<span data-ttu-id="6a039-123">Beklenmeyen Paket sürümü uyarıları</span><span class="sxs-lookup"><span data-stu-id="6a039-123">Unexpected package version warnings</span></span>](#unexpected-package-version-warnings) | <span data-ttu-id="6a039-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="6a039-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span></span> |
| [<span data-ttu-id="6a039-125">Çözümleyici çakışma uyarıları</span><span class="sxs-lookup"><span data-stu-id="6a039-125">Resolver conflict warnings</span></span>](#resolver-conflict-warnings) | [<span data-ttu-id="6a039-126">NU1608</span><span class="sxs-lookup"><span data-stu-id="6a039-126">NU1608</span></span>](#nu1608) |
| [<span data-ttu-id="6a039-127">Paket geri dönüş uyarıları</span><span class="sxs-lookup"><span data-stu-id="6a039-127">Package fallback warnings</span></span>](#package-fallback-warnings) | [<span data-ttu-id="6a039-128">NU1701</span><span class="sxs-lookup"><span data-stu-id="6a039-128">NU1701</span></span>](#nu1701) |
| [<span data-ttu-id="6a039-129">Akış uyarıları</span><span class="sxs-lookup"><span data-stu-id="6a039-129">Feed warnings</span></span>](#feed-warnings) | [<span data-ttu-id="6a039-130">NU1801</span><span class="sxs-lookup"><span data-stu-id="6a039-130">NU1801</span></span>](#nu1801) |
| [<span data-ttu-id="6a039-131">NuGet iç hatalar ve uyarılar</span><span class="sxs-lookup"><span data-stu-id="6a039-131">NuGet internal errors and warnings</span></span>](#nuget-internal-errors-and-warnings) | <span data-ttu-id="6a039-132">[NU1000](#nu1000), [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="6a039-132">[NU1000](#nu1000), [NU1500](#nu1500)</span></span> |

## <a name="invalid-input-errors"></a><span data-ttu-id="6a039-133">Geçersiz giriş hataları</span><span class="sxs-lookup"><span data-stu-id="6a039-133">Invalid input errors</span></span>

<span data-ttu-id="6a039-134">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="6a039-134">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span></span>

### <a name="nu1001"></a><span data-ttu-id="6a039-135">NU1001</span><span class="sxs-lookup"><span data-stu-id="6a039-135">NU1001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6a039-136">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="6a039-136">**Issue**</span></span> | <span data-ttu-id="6a039-137">Bir veya daha fazla çerçeveler proje içermiyor.</span><span class="sxs-lookup"><span data-stu-id="6a039-137">The project doesn't contain one or more frameworks.</span></span> |
| <span data-ttu-id="6a039-138">**Olası nedenler**</span><span class="sxs-lookup"><span data-stu-id="6a039-138">**Common causes**</span></span> | <span data-ttu-id="6a039-139">Proje içermiyor. bir `TargetFramework` veya `TargetFrameworks` özelliği.</span><span class="sxs-lookup"><span data-stu-id="6a039-139">The project doesn't contain a `TargetFramework` or `TargetFrameworks` property.</span></span> |
| <span data-ttu-id="6a039-140">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="6a039-140">**Example message**</span></span> | <span data-ttu-id="6a039-141">*Proje projA c:\tmp\projA.csproj içinde herhangi bir hedef çerçeve belirtmiyor*</span><span class="sxs-lookup"><span data-stu-id="6a039-141">*The project projA does not specify any target frameworks in c:\tmp\projA.csproj*</span></span> |

### <a name="nu1002"></a><span data-ttu-id="6a039-142">NU1002</span><span class="sxs-lookup"><span data-stu-id="6a039-142">NU1002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6a039-143">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="6a039-143">**Issue**</span></span> | <span data-ttu-id="6a039-144">Girişleri Temizle anahtar sözcüğü ile birlikte birleşimi geçersiz.</span><span class="sxs-lookup"><span data-stu-id="6a039-144">Invalid combination of inputs along with a CLEAR keyword.</span></span> |
| <span data-ttu-id="6a039-145">**Olası nedenler**</span><span class="sxs-lookup"><span data-stu-id="6a039-145">**Common causes**</span></span> | <span data-ttu-id="6a039-146">CLEAR diğer girişle birleştirilemez.</span><span class="sxs-lookup"><span data-stu-id="6a039-146">CLEAR may not be combined with other inputs.</span></span> |
| <span data-ttu-id="6a039-147">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="6a039-147">**Example message**</span></span> | <span data-ttu-id="6a039-148">*'CLEAR' diğer değerler ile birlikte kullanılamaz*</span><span class="sxs-lookup"><span data-stu-id="6a039-148">*'CLEAR' cannot be used in conjunction with other values*</span></span> |

### <a name="nu1003"></a><span data-ttu-id="6a039-149">NU1003</span><span class="sxs-lookup"><span data-stu-id="6a039-149">NU1003</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6a039-150">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="6a039-150">**Issue**</span></span> | <span data-ttu-id="6a039-151">`PackageTargetFallback`ve `AssetTargetFallback` varlıklar seçmek için farklı bir davranış sağlar ve birlikte kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="6a039-151">`PackageTargetFallback` and `AssetTargetFallback` provide different behavior for selecting assets and cannot be used together.</span></span> |
| <span data-ttu-id="6a039-152">**Olası nedenler**</span><span class="sxs-lookup"><span data-stu-id="6a039-152">**Common causes**</span></span> | <span data-ttu-id="6a039-153">Her ikisi de `PackageTargetFallback` ve `AssetTargetFallback` projede mevcut.</span><span class="sxs-lookup"><span data-stu-id="6a039-153">Both `PackageTargetFallback` and `AssetTargetFallback` exist in the project.</span></span> |
| <span data-ttu-id="6a039-154">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="6a039-154">**Example message**</span></span> | <span data-ttu-id="6a039-155">*PackageTargetFallback ve AssetTargetFallback birlikte kullanılamaz. Proje ortamından PackageTargetFallback(deprecated) başvuruları kaldırın.*</span><span class="sxs-lookup"><span data-stu-id="6a039-155">*PackageTargetFallback and AssetTargetFallback cannot be used together. Remove PackageTargetFallback(deprecated) references from the project environment.*</span></span> |

## <a name="missing-package-and-project-errors"></a><span data-ttu-id="6a039-156">Eksik paket ve proje hataları</span><span class="sxs-lookup"><span data-stu-id="6a039-156">Missing package and project errors</span></span>

<span data-ttu-id="6a039-157">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104 ](#nu1104)  |  [NU1105](#nu1105) | [NU1106](#nu1106)</span><span class="sxs-lookup"><span data-stu-id="6a039-157">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span></span>

### <a name="nu1100"></a><span data-ttu-id="6a039-158">NU1100</span><span class="sxs-lookup"><span data-stu-id="6a039-158">NU1100</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6a039-159">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="6a039-159">**Issue**</span></span> | <span data-ttu-id="6a039-160">Bir bağımlılık grubunun çözülmesi değil.</span><span class="sxs-lookup"><span data-stu-id="6a039-160">A dependency group not be resolved.</span></span> <span data-ttu-id="6a039-161">Bu, paket veya projeleri olmayan türleri için genel bir sorundur.</span><span class="sxs-lookup"><span data-stu-id="6a039-161">This is a generic issue for types that are not packages or projects.</span></span> |
| <span data-ttu-id="6a039-162">**Olası nedenler**</span><span class="sxs-lookup"><span data-stu-id="6a039-162">**Common causes**</span></span> | <span data-ttu-id="6a039-163">Proje mevcut olmayan bir öğe üzerinde bir bağımlılık içeriyor.</span><span class="sxs-lookup"><span data-stu-id="6a039-163">The project contains a dependency on an item that doesn't exist.</span></span> |
| <span data-ttu-id="6a039-164">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="6a039-164">**Example message**</span></span> | <span data-ttu-id="6a039-165">*System.Missing için net45 çözümlenemiyor*</span><span class="sxs-lookup"><span data-stu-id="6a039-165">*Unable to resolve System.Missing for net45*</span></span> |

### <a name="nu1101"></a><span data-ttu-id="6a039-166">NU1101</span><span class="sxs-lookup"><span data-stu-id="6a039-166">NU1101</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6a039-167">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="6a039-167">**Issue**</span></span> | <span data-ttu-id="6a039-168">Paketin tüm kaynakları bulunamıyor.</span><span class="sxs-lookup"><span data-stu-id="6a039-168">The package cannot be found on any sources.</span></span> |
| <span data-ttu-id="6a039-169">**Olası nedenler**</span><span class="sxs-lookup"><span data-stu-id="6a039-169">**Common causes**</span></span> | <span data-ttu-id="6a039-170">Doğru paket kaynağı eksik veya paket tanımlayıcısı geçersiz.</span><span class="sxs-lookup"><span data-stu-id="6a039-170">The correct package source is missing or the package identifier is incorrect.</span></span> |
| <span data-ttu-id="6a039-171">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="6a039-171">**Example message**</span></span> | <span data-ttu-id="6a039-172">*Paket System.Missing bulunamıyor. Bu kimlikle kaynakları hiç paket yok: dotnet çekirdekli, dotnet roslyn, nuget.org*</span><span class="sxs-lookup"><span data-stu-id="6a039-172">*Unable to find package System.Missing. No packages exist with this id in source(s): dotnet-core, dotnet-roslyn, nuget.org*</span></span> |

### <a name="nu1102"></a><span data-ttu-id="6a039-173">NU1102</span><span class="sxs-lookup"><span data-stu-id="6a039-173">NU1102</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6a039-174">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="6a039-174">**Issue**</span></span> | <span data-ttu-id="6a039-175">Paket tanımlayıcısı bulundu, ancak belirtilen bağımlılık aralıkta bir sürüm kaynakları hiçbirinde bulunamıyor.</span><span class="sxs-lookup"><span data-stu-id="6a039-175">The package identifier is found but a version within the specified dependency range cannot be found on any of the sources.</span></span> |
| <span data-ttu-id="6a039-176">**Olası nedenler**</span><span class="sxs-lookup"><span data-stu-id="6a039-176">**Common causes**</span></span> | <span data-ttu-id="6a039-177">Doğru paket kaynağı eksik veya bağımlılık aralığı yanlış.</span><span class="sxs-lookup"><span data-stu-id="6a039-177">The correct package source is missing or the dependency range is incorrect.</span></span> <span data-ttu-id="6a039-178">Aralığın bir paket ve kullanıcı tarafından belirtilen.</span><span class="sxs-lookup"><span data-stu-id="6a039-178">The range might be specified by a package and not the user.</span></span> <span data-ttu-id="6a039-179">Kullanıcı Bu paket proje tarafından doğrudan başvurulduğunda bir sürüme geçiş yapmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="6a039-179">The user may need to switch to an available version if this package is referenced by the project directly.</span></span> |
| <span data-ttu-id="6a039-180">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="6a039-180">**Example message**</span></span> | <span data-ttu-id="6a039-181">*Paketi NuGet.Versioning sürümüyle bulunamadı (> 9.0.1 =)<br/> -nuget.org içinde bulunan 30 sürümler [sürüm en yakın: 4.0.0]<br/> -dotnet buildtools içinde bulunan 10 sürümler [sürüm en yakın: 4.0.0-rc-2129]<br/> -9 bulundu NuGetVolatile sürümler [sürüm en yakın: 3.0.0-beta-00032]<br/> -0 sürümler dotnet-çekirdek bulunan<br/> -0 sürümler dotnet-roslyn bulundu*</span><span class="sxs-lookup"><span data-stu-id="6a039-181">*Unable to find package NuGet.Versioning with version (>= 9.0.1)<br/>  - Found 30 version(s) in nuget.org [ Nearest version: 4.0.0 ]<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |

### <a name="nu1103"></a><span data-ttu-id="6a039-182">NU1103</span><span class="sxs-lookup"><span data-stu-id="6a039-182">NU1103</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6a039-183">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="6a039-183">**Issue**</span></span> | <span data-ttu-id="6a039-184">Hiçbir kararlı sürümleri bağımlılık aralığı içinde bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="6a039-184">No stable versions were found in the dependency range.</span></span> <span data-ttu-id="6a039-185">Yayın öncesi sürümleri bulundu, ancak izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="6a039-185">Pre-release versions were found but are not allowed.</span></span> |
| <span data-ttu-id="6a039-186">**Olası nedenler**</span><span class="sxs-lookup"><span data-stu-id="6a039-186">**Common causes**</span></span> | <span data-ttu-id="6a039-187">Proje bağımlılık aralığının kararlı sürüm belirtildi.</span><span class="sxs-lookup"><span data-stu-id="6a039-187">The project specified a stable version for the dependency range.</span></span> <span data-ttu-id="6a039-188">Kullanıcılar, yayın öncesi sürümleri dahil etmek için sürüm aralığı değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6a039-188">Users need to change the version range to include pre-release versions.</span></span> |
| <span data-ttu-id="6a039-189">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="6a039-189">**Example message**</span></span> | <span data-ttu-id="6a039-190">*Sürümüyle kararlı paketi NuGet.Versioning bulunamadı (> 3.0.0 =)<br/> -dotnet buildtools içinde bulunan 10 sürümler [sürüm en yakın: 4.0.0-rc-2129]<br/> -NuGetVolatile içinde bulunan 9 sürümler [sürüm en yakın: 3.0.0-beta-00032] <br/> -0 sürümler dotnet-çekirdek bulunan<br/> -0 sürümler dotnet-roslyn bulundu*</span><span class="sxs-lookup"><span data-stu-id="6a039-190">*Unable to find a stable package NuGet.Versioning with version (>= 3.0.0)<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |

### <a name="nu1104"></a><span data-ttu-id="6a039-191">NU1104</span><span class="sxs-lookup"><span data-stu-id="6a039-191">NU1104</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6a039-192">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="6a039-192">**Issue**</span></span> | <span data-ttu-id="6a039-193">Bir ProjectReference mevcut olmayan bir dosyaya işaret eder.</span><span class="sxs-lookup"><span data-stu-id="6a039-193">A ProjectReference points to a file that doesn't exist.</span></span> |
| <span data-ttu-id="6a039-194">**Olası nedenler**</span><span class="sxs-lookup"><span data-stu-id="6a039-194">**Common causes**</span></span> | <span data-ttu-id="6a039-195">Proje dosyası diskten eksik veya hatalı bir başvurudur.</span><span class="sxs-lookup"><span data-stu-id="6a039-195">The project file is missing from disk or the reference is incorrect.</span></span> |
| <span data-ttu-id="6a039-196">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="6a039-196">**Example message**</span></span> | <span data-ttu-id="6a039-197">*Proje Başvurusu 'c:\a.csproj' yok. Proje başvurusu geçerli olduğunu ve proje dosyasının varolduğunu kontrol edin.*</span><span class="sxs-lookup"><span data-stu-id="6a039-197">*Project reference does not exist 'c:\a.csproj'. Check that the project reference is valid and that the project file exists.*</span></span> |

### <a name="nu1105"></a><span data-ttu-id="6a039-198">NU1105</span><span class="sxs-lookup"><span data-stu-id="6a039-198">NU1105</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6a039-199">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="6a039-199">**Issue**</span></span> | <span data-ttu-id="6a039-200">Proje dosyası var, ancak bunun için hiçbir geri yükleme bilgisi verilmedi.</span><span class="sxs-lookup"><span data-stu-id="6a039-200">The project file exists but no restore information was provided for it.</span></span> |
| <span data-ttu-id="6a039-201">**Olası nedenler**</span><span class="sxs-lookup"><span data-stu-id="6a039-201">**Common causes**</span></span> | <span data-ttu-id="6a039-202">Visual Studio'da bu projenin yüklenmemiş olduğu anlamına gelebilir.</span><span class="sxs-lookup"><span data-stu-id="6a039-202">In Visual Studio this could mean that the project is unloaded.</span></span> <span data-ttu-id="6a039-203">Komut satırından bu dosya bozuk veya bu özel Proje okumak geri yükleme için gerekli içeri aktarmaları hedef sonra içermiyor anlamına gelebilir.</span><span class="sxs-lookup"><span data-stu-id="6a039-203">From the command line this could mean that the file is corrupt or that it doesn't contain the custom after imports target needed for restore to read the project.</span></span> |
| <span data-ttu-id="6a039-204">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="6a039-204">**Example message**</span></span> | <span data-ttu-id="6a039-205">*'C:\a.csproj' için proje bilgileri okunamıyor. Proje dosyası geçersiz veya eksik hedefleri geri yüklemek için gerekli olabilir.*</span><span class="sxs-lookup"><span data-stu-id="6a039-205">*Unable to read project information for 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |

### <a name="nu1106"></a><span data-ttu-id="6a039-206">NU1106</span><span class="sxs-lookup"><span data-stu-id="6a039-206">NU1106</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6a039-207">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="6a039-207">**Issue**</span></span> | <span data-ttu-id="6a039-208">Bağımlılık kısıtlamalarını çözümlenemiyor.</span><span class="sxs-lookup"><span data-stu-id="6a039-208">Dependency constraints cannot be resolved.</span></span> |
| <span data-ttu-id="6a039-209">**Olası nedenler**</span><span class="sxs-lookup"><span data-stu-id="6a039-209">**Common causes**</span></span> | <span data-ttu-id="6a039-210">Paketler bağımlılık paketi uçlu aralıkları yerine tam sürümlerinde içerir.</span><span class="sxs-lookup"><span data-stu-id="6a039-210">Packages contain dependency on exact versions of a package instead of open-ended ranges.</span></span> |
| <span data-ttu-id="6a039-211">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="6a039-211">**Example message**</span></span> | <span data-ttu-id="6a039-212">*{İd}'için çakışma istekleri giderilemiyor: {çakışma yolu} Framework: {hedef grafik}*</span><span class="sxs-lookup"><span data-stu-id="6a039-212">*Unable to satisfy conflicting requests for {id}: {conflict path} Framework: {target graph}*</span></span> |

<span data-ttu-id="6a039-213">< a name = "NU1107 ></a></span><span class="sxs-lookup"><span data-stu-id="6a039-213"><a name="NU1107></a></span></span>

### <a name="nu1107-previously-nu1607"></a><span data-ttu-id="6a039-214">NU1107 (daha önce NU1607)</span><span class="sxs-lookup"><span data-stu-id="6a039-214">NU1107 (Previously NU1607)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6a039-215">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="6a039-215">**Issue**</span></span> | <span data-ttu-id="6a039-216">Bağımlılık kısıtlamalarını paketler arasında çözümlenemiyor.</span><span class="sxs-lookup"><span data-stu-id="6a039-216">Unable to resolve dependency constraints between packages.</span></span> |
| <span data-ttu-id="6a039-217">**Olası nedenler**</span><span class="sxs-lookup"><span data-stu-id="6a039-217">**Common causes**</span></span> | <span data-ttu-id="6a039-218">Tam sürümleri bağımlılık kısıtlamalar paketlerle sürüm gerekirse artırmak diğer paketleri izin vermez.</span><span class="sxs-lookup"><span data-stu-id="6a039-218">Packages with dependency constraints on exact versions do not allow other packages to increase the version if needed.</span></span> |
| <span data-ttu-id="6a039-219">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="6a039-219">**Example message**</span></span> | <span data-ttu-id="6a039-220">*Sürüm çakışması için NuGet.Versioning algılandı. Paket, bu sorunu çözmek için doğrudan projeden başvuru.<br/>  NuGet.Packaging 3.5.0 -> (= 3.5.0) NuGet.Versioning<br/> NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span><span class="sxs-lookup"><span data-stu-id="6a039-220">*Version conflict detected for NuGet.Versioning. Reference the package directly from the project to resolve this issue.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span></span> |

<span data-ttu-id="6a039-221">< a name = "NU1108 ></a></span><span class="sxs-lookup"><span data-stu-id="6a039-221"><a name="NU1108></a></span></span>

### <a name="nu1108-previously-nu1606"></a><span data-ttu-id="6a039-222">NU1108 (daha önce NU1606)</span><span class="sxs-lookup"><span data-stu-id="6a039-222">NU1108 (Previously NU1606)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6a039-223">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="6a039-223">**Issue**</span></span> | <span data-ttu-id="6a039-224">Döngüsel bağımlılık algılandı.</span><span class="sxs-lookup"><span data-stu-id="6a039-224">A circular dependency was detected.</span></span> |
| <span data-ttu-id="6a039-225">**Olası nedenler**</span><span class="sxs-lookup"><span data-stu-id="6a039-225">**Common causes**</span></span> | <span data-ttu-id="6a039-226">Bir paket yanlış yazılmış.</span><span class="sxs-lookup"><span data-stu-id="6a039-226">A package is authored incorrectly.</span></span> |
| <span data-ttu-id="6a039-227">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="6a039-227">**Example message**</span></span> | <span data-ttu-id="6a039-228">*Döngü algılandı: A B -> A ->*</span><span class="sxs-lookup"><span data-stu-id="6a039-228">*Cycle detected: A -> B -> A*</span></span> |

## <a name="compatibility-errors"></a><span data-ttu-id="6a039-229">Uyumluluk hataları</span><span class="sxs-lookup"><span data-stu-id="6a039-229">Compatibility errors</span></span>

<span data-ttu-id="6a039-230">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="6a039-230">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span></span>

### <a name="nu1201"></a><span data-ttu-id="6a039-231">NU1201</span><span class="sxs-lookup"><span data-stu-id="6a039-231">NU1201</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6a039-232">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="6a039-232">**Issue**</span></span> | <span data-ttu-id="6a039-233">Bir bağımlılık proje Geçerli projeyle uyumlu bir çerçeve içermiyor.</span><span class="sxs-lookup"><span data-stu-id="6a039-233">A dependency project doesn't contain a framework compatible with the current project.</span></span> |
| <span data-ttu-id="6a039-234">**Olası nedenler**</span><span class="sxs-lookup"><span data-stu-id="6a039-234">**Common causes**</span></span> | <span data-ttu-id="6a039-235">Projenin hedef çerçevesi Süren proje daha yüksek bir sürüme ' dir.</span><span class="sxs-lookup"><span data-stu-id="6a039-235">The project's target framework is a higher version than the consuming project.</span></span> |
| <span data-ttu-id="6a039-236">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="6a039-236">**Example message**</span></span> | <span data-ttu-id="6a039-237">*Proje nokta netstandard1.3 ile uyumlu değil (. NETStandard, sürüm = v1.3). Proje nokta destekler:<br/> -netstandard1.6 (. NETStandard, sürüm = v1.6)<br/> -netcoreapp1.0 (. NETCoreApp, sürüm v1.0 =)*</span><span class="sxs-lookup"><span data-stu-id="6a039-237">*Project ServerWeb is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Project ServerWeb supports:<br/>  - netstandard1.6 (.NETStandard,Version=v1.6)<br/>  - netcoreapp1.0 (.NETCoreApp,Version=v1.0)*</span></span> |

### <a name="nu1202"></a><span data-ttu-id="6a039-238">NU1202</span><span class="sxs-lookup"><span data-stu-id="6a039-238">NU1202</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6a039-239">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="6a039-239">**Issue**</span></span> | <span data-ttu-id="6a039-240">Bir bağımlılık paketi projeyle uyumlu tüm varlıkları içermiyor.</span><span class="sxs-lookup"><span data-stu-id="6a039-240">A dependency package doesn't contain any assets compatible with the project.</span></span> |
| <span data-ttu-id="6a039-241">**Olası nedenler**</span><span class="sxs-lookup"><span data-stu-id="6a039-241">**Common causes**</span></span> | <span data-ttu-id="6a039-242">Paket projenin hedef çerçevesi desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="6a039-242">The package doesn't support the project's target framework.</span></span> |
| <span data-ttu-id="6a039-243">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="6a039-243">**Example message**</span></span> | <span data-ttu-id="6a039-244">*Paket System.ComponentModel.EventBasedAsync 4.0.11 netstandard1.3 ile uyumlu değil (. NETStandard, sürüm = v1.3). Paket System.ComponentModel.EventBasedAsync 4.0.11 destekler:<br/> -monoandroid10 (MonoAndroid, sürüm = v1.0)<br/> -monotouch10 (MonoTouch, sürüm = v1.0)<br/> -net45 (. NETFramework, sürümü v4.5 =)<br/> -netcore50 (. NETCore, sürüm = v5.0)<br/> -netstandard1.0 (. NETStandard, sürüm = v1.0)<br/> -taşınabilir net45 olduğu win8 + wp8 + wpa81 (. NETPortable, sürüm v0.0, profil = Profile259 =)<br/> -olduğu win8 (Windows, sürüm = v8.0)<br/> -wp8 (WindowsPhone, sürüm v8.0 =)<br/> -wpa81 (WindowsPhoneApp, sürüm v8.1 =)<br/> -xamarinios10 () Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span><span class="sxs-lookup"><span data-stu-id="6a039-244">*Package System.ComponentModel.EventBasedAsync 4.0.11 is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span></span>|

### <a name="nu1203"></a><span data-ttu-id="6a039-245">NU1203</span><span class="sxs-lookup"><span data-stu-id="6a039-245">NU1203</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6a039-246">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="6a039-246">**Issue**</span></span> | <span data-ttu-id="6a039-247">Paket projenin desteklemiyor `RuntimeIdentifier`.</span><span class="sxs-lookup"><span data-stu-id="6a039-247">The package doesn't support the project's `RuntimeIdentifier`.</span></span> |
| <span data-ttu-id="6a039-248">**Olası nedenler**</span><span class="sxs-lookup"><span data-stu-id="6a039-248">**Common causes**</span></span> | <span data-ttu-id="6a039-249">Paket geçerli desteklemiyor `RuntimeIdentifier`.</span><span class="sxs-lookup"><span data-stu-id="6a039-249">The package doesn't support the current `RuntimeIdentifier`.</span></span> <span data-ttu-id="6a039-250">Değişiklik `RuntimeIdentifier` gerekirse projesinde kullanılan değerler.</span><span class="sxs-lookup"><span data-stu-id="6a039-250">Change the `RuntimeIdentifier` values used in the project if needed.</span></span> |
| <span data-ttu-id="6a039-251">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="6a039-251">**Example message**</span></span> | <span data-ttu-id="6a039-252">*System.Example 1.0.0 a.dll için derleme zamanı referans derlemesini üzerinde net461 sağlar, ancak uyumlu çalışma zamanı derlemesi bulunmuyor.*</span><span class="sxs-lookup"><span data-stu-id="6a039-252">*System.Example 1.0.0 provides a compile-time reference assembly for a.dll on net461, but there is no compatible run-time assembly.*</span></span> |

### <a name="nu1401"></a><span data-ttu-id="6a039-253">NU1401</span><span class="sxs-lookup"><span data-stu-id="6a039-253">NU1401</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6a039-254">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="6a039-254">**Issue**</span></span> | <span data-ttu-id="6a039-255">Paket özelliklerini veya şu anda yüklü olan NuGet sürümü tarafından desteklenmeyen çerçeveler gerektirir.</span><span class="sxs-lookup"><span data-stu-id="6a039-255">The package requires features or frameworks not currently supported by the installed version of NuGet.</span></span> |
| <span data-ttu-id="6a039-256">**Olası nedenler**</span><span class="sxs-lookup"><span data-stu-id="6a039-256">**Common causes**</span></span> | <span data-ttu-id="6a039-257">Sorunu düzeltmek için NuGet yükseltin.</span><span class="sxs-lookup"><span data-stu-id="6a039-257">Upgrade NuGet to fix the issue.</span></span> |
| <span data-ttu-id="6a039-258">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="6a039-258">**Example message**</span></span> | <span data-ttu-id="6a039-259">*'NuGet.Versioning' paketi NuGet İstemcisi Sürüm '5.0.0' gerektirir veya üstü, ancak geçerli NuGet sürümü '4.3.0'. NuGet yükseltmek için lütfen http://docs.nuget.org/consume/installing-nuget için gidin.*</span><span class="sxs-lookup"><span data-stu-id="6a039-259">*The 'NuGet.Versioning' package requires NuGet client version '5.0.0' or above, but the current NuGet version is '4.3.0'. To upgrade NuGet, please go to http://docs.nuget.org/consume/installing-nuget.*</span></span> |

## <a name="invalid-input-warnings"></a><span data-ttu-id="6a039-260">Geçersiz giriş uyarıları</span><span class="sxs-lookup"><span data-stu-id="6a039-260">Invalid input warnings</span></span>

<span data-ttu-id="6a039-261">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="6a039-261">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span></span>

### <a name="nu1501"></a><span data-ttu-id="6a039-262">NU1501</span><span class="sxs-lookup"><span data-stu-id="6a039-262">NU1501</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6a039-263">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="6a039-263">**Issue**</span></span> | <span data-ttu-id="6a039-264">Proje geri yükleme çalışması çalışıyor üzerinde bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="6a039-264">The project restore is attempting to operate on was not found.</span></span> |
| <span data-ttu-id="6a039-265">**Olası nedenler**</span><span class="sxs-lookup"><span data-stu-id="6a039-265">**Common causes**</span></span> | <span data-ttu-id="6a039-266">Proje eksik.</span><span class="sxs-lookup"><span data-stu-id="6a039-266">The project is missing.</span></span> |
| <span data-ttu-id="6a039-267">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="6a039-267">**Example message**</span></span> | <span data-ttu-id="6a039-268">*'C:\projects\a' klasörü geri yüklenecek bir proje içermiyor.*</span><span class="sxs-lookup"><span data-stu-id="6a039-268">*The folder 'c:\projects\a' does not contain a project to restore.*</span></span> |

### <a name="nu1502"></a><span data-ttu-id="6a039-269">NU1502</span><span class="sxs-lookup"><span data-stu-id="6a039-269">NU1502</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6a039-270">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="6a039-270">**Issue**</span></span> | <span data-ttu-id="6a039-271">`RuntimeSupports`Geçersiz bir profil içerir.</span><span class="sxs-lookup"><span data-stu-id="6a039-271">`RuntimeSupports` contains an invalid profile.</span></span> |
| <span data-ttu-id="6a039-272">**Olası nedenler**</span><span class="sxs-lookup"><span data-stu-id="6a039-272">**Common causes**</span></span> | <span data-ttu-id="6a039-273">Destekler profili bulunamadı bir `runtime.json` geçerli bağımlılık paketleri dosyasından.</span><span class="sxs-lookup"><span data-stu-id="6a039-273">The supports profile was not found in a `runtime.json` file from the current dependency packages.</span></span> |
| <span data-ttu-id="6a039-274">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="6a039-274">**Example message**</span></span> | <span data-ttu-id="6a039-275">*Bilinmeyen uyumluluk profili: aaa*</span><span class="sxs-lookup"><span data-stu-id="6a039-275">*Unknown Compatibility Profile: aaa*</span></span> |

### <a name="nu1503"></a><span data-ttu-id="6a039-276">NU1503</span><span class="sxs-lookup"><span data-stu-id="6a039-276">NU1503</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6a039-277">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="6a039-277">**Issue**</span></span> | <span data-ttu-id="6a039-278">Bir bağımlılık proje Nuget'in geri yükleme hedeflerini içe aktarmaz.</span><span class="sxs-lookup"><span data-stu-id="6a039-278">A dependency project doesn't import NuGet's restore targets.</span></span> <span data-ttu-id="6a039-279">Bu NU1105 için benzer ancak burada proje atlanır ve tüm geri yükleme başarısız olmasına neden yerine yoksayıldı.</span><span class="sxs-lookup"><span data-stu-id="6a039-279">This is similar to NU1105 but here the project is skipped and ignored instead of causing all of restore to fail.</span></span> <span data-ttu-id="6a039-280">Karmaşık çözümlerinde çoğunlukla diğer geri yükleme desteklemeyebilir proje türleri vardır.</span><span class="sxs-lookup"><span data-stu-id="6a039-280">In complex solutions there are often other types of projects that may not support restore.</span></span> |
| <span data-ttu-id="6a039-281">**Olası nedenler**</span><span class="sxs-lookup"><span data-stu-id="6a039-281">**Common causes**</span></span> | <span data-ttu-id="6a039-282">Bu ortak özellik/geri yükleme otomatik olarak içeri hedefleri almayın projelerde meydana gelebilir.</span><span class="sxs-lookup"><span data-stu-id="6a039-282">This can happen for projects that do not import common props/targets which automatically import restore.</span></span> <span data-ttu-id="6a039-283">Proje geri gerekmez, bu yoksayılabilir.</span><span class="sxs-lookup"><span data-stu-id="6a039-283">If the project doesn't need to be restored this can be ignored.</span></span> |
| <span data-ttu-id="6a039-284">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="6a039-284">**Example message**</span></span> | <span data-ttu-id="6a039-285">*Proje 'c:\a.csproj' için geri atlanıyor. Proje dosyası geçersiz veya eksik hedefleri geri yüklemek için gerekli olabilir.*</span><span class="sxs-lookup"><span data-stu-id="6a039-285">*Skipping restore for project 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |

## <a name="unexpected-package-version-warnings"></a><span data-ttu-id="6a039-286">Beklenmeyen Paket sürümü uyarıları</span><span class="sxs-lookup"><span data-stu-id="6a039-286">Unexpected package version warnings</span></span>

<span data-ttu-id="6a039-287">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="6a039-287">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span></span>

### <a name="nu1601"></a><span data-ttu-id="6a039-288">NU1601</span><span class="sxs-lookup"><span data-stu-id="6a039-288">NU1601</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6a039-289">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="6a039-289">**Issue**</span></span> | <span data-ttu-id="6a039-290">Bir doğrudan proje bağımlılığı belirtilen proje daha yüksek bir sürüme indirgenmesine.</span><span class="sxs-lookup"><span data-stu-id="6a039-290">A direct project dependency was bumped to a higher version than the project specified.</span></span> |
| <span data-ttu-id="6a039-291">**Olası nedenler**</span><span class="sxs-lookup"><span data-stu-id="6a039-291">**Common causes**</span></span> | <span data-ttu-id="6a039-292">Başka bir bağımlılık paket daha yüksek bir sürüm gereklidir ve paket indirgenmesine.</span><span class="sxs-lookup"><span data-stu-id="6a039-292">Another dependency package required a higher version and bumped the package up.</span></span> |
| <span data-ttu-id="6a039-293">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="6a039-293">**Example message**</span></span> | <span data-ttu-id="6a039-294">*Bağımlılık belirtildi NuGet.Versioning (> = 3.5.0) ancak 4.0.0 NuGet.Versioning ile sonuçlandı.*</span><span class="sxs-lookup"><span data-stu-id="6a039-294">*Dependency specified was NuGet.Versioning (>= 3.5.0) but ended up with NuGet.Versioning 4.0.0.*</span></span> |

### <a name="nu1602"></a><span data-ttu-id="6a039-295">NU1602</span><span class="sxs-lookup"><span data-stu-id="6a039-295">NU1602</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6a039-296">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="6a039-296">**Issue**</span></span> | <span data-ttu-id="6a039-297">Bir paket bağımlılığı alt sınır eksik.</span><span class="sxs-lookup"><span data-stu-id="6a039-297">A package dependency is missing a lower bound.</span></span> <span data-ttu-id="6a039-298">Bunu bulmak geri yükleme izin vermeyen *en iyi eşleşmeyi*.</span><span class="sxs-lookup"><span data-stu-id="6a039-298">This doesn't allow restore to find the *best match*.</span></span> <span data-ttu-id="6a039-299">Her geri yükleme, aşağı doğru hareket kullanılabilir daha düşük bir sürüm bulunmaya çalışılırken float.</span><span class="sxs-lookup"><span data-stu-id="6a039-299">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="6a039-300">Bu geri yükleme zaten paketleri kullanıcı paket klasöründe kullanmak yerine her zaman tüm kaynakları denetlemek için çevrimiçi duruma geçtiğinde anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="6a039-300">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="6a039-301">**Olası nedenler**</span><span class="sxs-lookup"><span data-stu-id="6a039-301">**Common causes**</span></span> | <span data-ttu-id="6a039-302">Bu genellikle hata yazma bir pakettir.</span><span class="sxs-lookup"><span data-stu-id="6a039-302">This is usually a package authoring error.</span></span> |
| <span data-ttu-id="6a039-303">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="6a039-303">**Example message**</span></span> | <span data-ttu-id="6a039-304">*NuGet.Packaging 4.0.0 (bunlar dahil) bir alt sınır için bağımlılık NuGet.Versioning (> 3.5.0) sağlamaz. Yaklaşık en iyi eşleşme 3.6.0, çözüldü.*</span><span class="sxs-lookup"><span data-stu-id="6a039-304">*NuGet.Packaging 4.0.0 does not provide an inclusive lower bound for dependency NuGet.Versioning (> 3.5.0). An approximate best match of 3.6.0 was resolved.*</span></span> |

### <a name="nu1603"></a><span data-ttu-id="6a039-305">NU1603</span><span class="sxs-lookup"><span data-stu-id="6a039-305">NU1603</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6a039-306">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="6a039-306">**Issue**</span></span> | <span data-ttu-id="6a039-307">Bir paket bağımlılığı bulunamadı bir sürüm belirtildi.</span><span class="sxs-lookup"><span data-stu-id="6a039-307">A package dependency specified a version that could not be found.</span></span> <span data-ttu-id="6a039-308">Bunun yerine, daha yüksek bir sürüm ne paket karşı yönetilmiyor öğesinden farklı kullanıldı.</span><span class="sxs-lookup"><span data-stu-id="6a039-308">A higher version was used instead, which differs from what the package was authored against.</span></span><br/><br/><span data-ttu-id="6a039-309">Bu geri yükleme bulamadı anlamına gelir *en iyi eşleşmeyi*.</span><span class="sxs-lookup"><span data-stu-id="6a039-309">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="6a039-310">Her geri yükleme, aşağı doğru hareket kullanılabilir daha düşük bir sürüm bulunmaya çalışılırken float.</span><span class="sxs-lookup"><span data-stu-id="6a039-310">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="6a039-311">Bu geri yükleme zaten paketleri kullanıcı paket klasöründe kullanmak yerine her zaman tüm kaynakları denetlemek için çevrimiçi duruma geçtiğinde anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="6a039-311">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="6a039-312">**Olası nedenler**</span><span class="sxs-lookup"><span data-stu-id="6a039-312">**Common causes**</span></span> | <span data-ttu-id="6a039-313">Paket kaynaklarını beklenen alt sınır sürüm içermiyor.</span><span class="sxs-lookup"><span data-stu-id="6a039-313">The package sources do not contain the expected lower bound version.</span></span> <span data-ttu-id="6a039-314">Beklenen paket bırakılmamışsa değilse bu hata yazma bir paket olabilir.</span><span class="sxs-lookup"><span data-stu-id="6a039-314">If the package expected has not been released then this may be a package authoring error.</span></span> |
| <span data-ttu-id="6a039-315">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="6a039-315">**Example message**</span></span> | <span data-ttu-id="6a039-316">NuGet.Packaging 4.0.0 NuGet.Versioning üzerinde bağlıdır (> = 4.0.0) ancak 4.0.0 bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="6a039-316">NuGet.Packaging 4.0.0 depends on NuGet.Versioning (>= 4.0.0) but 4.0.0 was not found.</span></span> <span data-ttu-id="6a039-317">Yaklaşık en iyi eşleşme 5.0.0, çözüldü.</span><span class="sxs-lookup"><span data-stu-id="6a039-317">An approximate best match of 5.0.0 was resolved.</span></span> |

### <a name="nu1604"></a><span data-ttu-id="6a039-318">NU1604</span><span class="sxs-lookup"><span data-stu-id="6a039-318">NU1604</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6a039-319">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="6a039-319">**Issue**</span></span> | <span data-ttu-id="6a039-320">Proje bağımlılığı alt sınır tanımlamıyor.</span><span class="sxs-lookup"><span data-stu-id="6a039-320">A project dependency doesn't define a lower bound.</span></span><br/><br/><span data-ttu-id="6a039-321">Bu geri yükleme bulamadı anlamına gelir *en iyi eşleşmeyi*.</span><span class="sxs-lookup"><span data-stu-id="6a039-321">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="6a039-322">Her geri yükleme, aşağı doğru hareket kullanılabilir daha düşük bir sürüm bulunmaya çalışılırken float.</span><span class="sxs-lookup"><span data-stu-id="6a039-322">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="6a039-323">Bu geri yükleme zaten paketleri kullanıcı paket klasöründe kullanmak yerine her zaman tüm kaynakları denetlemek için çevrimiçi duruma geçtiğinde anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="6a039-323">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="6a039-324">**Olası nedenler**</span><span class="sxs-lookup"><span data-stu-id="6a039-324">**Common causes**</span></span> | <span data-ttu-id="6a039-325">Projenin *PackageReference* *sürüm* özniteliği alt sınırı içerecek şekilde güncelleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="6a039-325">The project's *PackageReference* *Version* attribute should be updated to include a lower bound.</span></span> |
| <span data-ttu-id="6a039-326">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="6a039-326">**Example message**</span></span> | <span data-ttu-id="6a039-327">*Bağımlılık NuGet.Versioning proje (< 9.0.0 =) doe (bunlar dahil) bir alt sınır içeremez. Alt sınır tutarlı geri yükleme sonuçlar sağlamak için bağımlılık sürümünü içerir.*</span><span class="sxs-lookup"><span data-stu-id="6a039-327">*Project dependency NuGet.Versioning (<= 9.0.0) doe not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span> |

### <a name="nu1605"></a><span data-ttu-id="6a039-328">NU1605</span><span class="sxs-lookup"><span data-stu-id="6a039-328">NU1605</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6a039-329">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="6a039-329">**Issue**</span></span> | <span data-ttu-id="6a039-330">Bir bağımlılık paketi bir paket geri yükleme sonuçta çözülmüş daha yüksek bir sürüm bir sürüm kısıtlaması belirtildi.</span><span class="sxs-lookup"><span data-stu-id="6a039-330">A dependency package specified a version constraint on a higher version of a package than restore ultimately resolved.</span></span> |
| <span data-ttu-id="6a039-331">**Olası nedenler**</span><span class="sxs-lookup"><span data-stu-id="6a039-331">**Common causes**</span></span> | <span data-ttu-id="6a039-332">Paketleri çözülürken yakın WINS.</span><span class="sxs-lookup"><span data-stu-id="6a039-332">Nearest wins when resolving packages.</span></span> <span data-ttu-id="6a039-333">Grafikte yakın bir paket uzaktaki bir paket silmiş.</span><span class="sxs-lookup"><span data-stu-id="6a039-333">A nearer package in the graph may have overridden a distant package.</span></span> |
| <span data-ttu-id="6a039-334">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="6a039-334">**Example message**</span></span> | <span data-ttu-id="6a039-335">*Paket indirgeme algılandı: 4.0.0 gelen NuGet.Versioning 3.5.0 için. Paketi farklı bir sürüm seçmek için doğrudan projeden başvuru.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 NuGet.Versioning 4.0.0 ->*</span><span class="sxs-lookup"><span data-stu-id="6a039-335">*Detected package downgrade: NuGet.Versioning from 4.0.0 to 3.5.0. Reference the package directly from the project to select a different version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span></span> |

## <a name="resolver-conflict-warnings"></a><span data-ttu-id="6a039-336">Çözümleyici çakışma uyarıları</span><span class="sxs-lookup"><span data-stu-id="6a039-336">Resolver conflict warnings</span></span>

[<span data-ttu-id="6a039-337">NU1608</span><span class="sxs-lookup"><span data-stu-id="6a039-337">NU1608</span></span>](#nu1608)

### <a name="nu1608"></a><span data-ttu-id="6a039-338">NU1608</span><span class="sxs-lookup"><span data-stu-id="6a039-338">NU1608</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6a039-339">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="6a039-339">**Issue**</span></span> | <span data-ttu-id="6a039-340">Bir bağımlılık kısıtlaması izin verdiğinden daha yüksek bir çözümleme paketidir.</span><span class="sxs-lookup"><span data-stu-id="6a039-340">A resolve package is higher than a dependency constraint allows.</span></span> <span data-ttu-id="6a039-341">Bazı durumlarda bu bilinen bir durumdur ve uyarıyı gizlenebilir.</span><span class="sxs-lookup"><span data-stu-id="6a039-341">In some cases this is intentional and the warning can be suppressed.</span></span> |
| <span data-ttu-id="6a039-342">**Olası nedenler**</span><span class="sxs-lookup"><span data-stu-id="6a039-342">**Common causes**</span></span> | <span data-ttu-id="6a039-343">Doğrudan bir proje tarafından başvurulan paket diğer paketlerinden bağımlılık kısıtlamalarını geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="6a039-343">A package referenced directly by a project will override dependency constraints from other packages.</span></span>   |
| <span data-ttu-id="6a039-344">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="6a039-344">**Example message**</span></span> | <span data-ttu-id="6a039-345">*Bağımlılık kısıtlaması dışında algılanan Paket sürümü: x 1.0.0 (= 1.0.0) y gerektiriyor, ancak sürüm y 2.0.0 çözülmüş.*</span><span class="sxs-lookup"><span data-stu-id="6a039-345">*Detected package version outside of dependency constraint: x 1.0.0 requires y (= 1.0.0) but version y 2.0.0 was resolved.*</span></span> |

## <a name="package-fallback-warnings"></a><span data-ttu-id="6a039-346">Paket geri dönüş uyarıları</span><span class="sxs-lookup"><span data-stu-id="6a039-346">Package fallback warnings</span></span>

[<span data-ttu-id="6a039-347">NU1701</span><span class="sxs-lookup"><span data-stu-id="6a039-347">NU1701</span></span>](#nu1701)

### <a name="nu1701"></a><span data-ttu-id="6a039-348">NU1701</span><span class="sxs-lookup"><span data-stu-id="6a039-348">NU1701</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6a039-349">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="6a039-349">**Issue**</span></span> | <span data-ttu-id="6a039-350">*PackageTargetFallback/AssetTargetFallback* varlıklar bir paket seçmek için kullanıldı.</span><span class="sxs-lookup"><span data-stu-id="6a039-350">*PackageTargetFallback/AssetTargetFallback* was used to select assets from a package.</span></span> <span data-ttu-id="6a039-351">Bu varlıklar % 100 uyumlu olmayabilir bilmeniz kullanıcı izin vermek için bir uyarıdır.</span><span class="sxs-lookup"><span data-stu-id="6a039-351">This is a warning to let the user know that the assets may not be 100% compatible.</span></span> |
| <span data-ttu-id="6a039-352">**Olası nedenler**</span><span class="sxs-lookup"><span data-stu-id="6a039-352">**Common causes**</span></span> | <span data-ttu-id="6a039-353">Paket proje framework desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="6a039-353">The package doesn't support the project framework.</span></span> |
| <span data-ttu-id="6a039-354">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="6a039-354">**Example message**</span></span> | <span data-ttu-id="6a039-355">*Paket 'NuGet.Versioning', 'taşınabilir net45 + olduğu win8' yerine projenin hedef çerçevesi 'netstandard1.5' kullanılarak geri yüklendi. Bu paket projenizi ile tamamen uyumlu olmayabilir.*</span><span class="sxs-lookup"><span data-stu-id="6a039-355">*Package 'NuGet.Versioning' was restored using 'portable-net45+win8' instead the project target framework 'netstandard1.5'. This package may not be fully compatible with your project.*</span></span> |

## <a name="feed-warnings"></a><span data-ttu-id="6a039-356">Akış uyarıları</span><span class="sxs-lookup"><span data-stu-id="6a039-356">Feed warnings</span></span>

[<span data-ttu-id="6a039-357">NU1801</span><span class="sxs-lookup"><span data-stu-id="6a039-357">NU1801</span></span>](#nu1801)

### <a name="nu1801"></a><span data-ttu-id="6a039-358">NU1801</span><span class="sxs-lookup"><span data-stu-id="6a039-358">NU1801</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6a039-359">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="6a039-359">**Issue**</span></span> | <span data-ttu-id="6a039-360">Akış okunurken bir hata oluştu, `IgnoreFailedSources` ayarlanır için önemli olmayan uyarı dönüştürme true.</span><span class="sxs-lookup"><span data-stu-id="6a039-360">An error occurred when reading the feed when `IgnoreFailedSources` is set to true, converting it to a non-fatal warning.</span></span> <span data-ttu-id="6a039-361">Bu herhangi bir iletisi içerebilir ve genel.</span><span class="sxs-lookup"><span data-stu-id="6a039-361">This could contain any message and is generic.</span></span> |
| <span data-ttu-id="6a039-362">**Olası nedenler**</span><span class="sxs-lookup"><span data-stu-id="6a039-362">**Common causes**</span></span> | <span data-ttu-id="6a039-363">Kaynağı geçersiz.</span><span class="sxs-lookup"><span data-stu-id="6a039-363">The source is invalid.</span></span> |
| <span data-ttu-id="6a039-364">**Örnek ileti**</span><span class="sxs-lookup"><span data-stu-id="6a039-364">**Example message**</span></span> | <span data-ttu-id="6a039-365">yok</span><span class="sxs-lookup"><span data-stu-id="6a039-365">n/a</span></span> |

## <a name="nuget-internal-errors-and-warnings"></a><span data-ttu-id="6a039-366">NuGet iç hatalar ve uyarılar</span><span class="sxs-lookup"><span data-stu-id="6a039-366">NuGet internal errors and warnings</span></span>

<span data-ttu-id="6a039-367">[NU1000](#nu1000) | [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="6a039-367">[NU1000](#nu1000) | [NU1500](#nu1500)</span></span>

### <a name="nu1000"></a><span data-ttu-id="6a039-368">NU1000</span><span class="sxs-lookup"><span data-stu-id="6a039-368">NU1000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6a039-369">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="6a039-369">**Issue**</span></span> | <span data-ttu-id="6a039-370">NuGet from olmayan belirli bir iç hata.</span><span class="sxs-lookup"><span data-stu-id="6a039-370">A non specific internal error from NuGet.</span></span> |
| <span data-ttu-id="6a039-371">**Olası nedenler**</span><span class="sxs-lookup"><span data-stu-id="6a039-371">**Common causes**</span></span> | <span data-ttu-id="6a039-372">Daha fazla bilgi için günlükleri denetleyin</span><span class="sxs-lookup"><span data-stu-id="6a039-372">Check the logs for more information</span></span> |

### <a name="nu1500"></a><span data-ttu-id="6a039-373">NU1500</span><span class="sxs-lookup"><span data-stu-id="6a039-373">NU1500</span></span>

| | |
| --- | --- |
| <span data-ttu-id="6a039-374">**Sorunu**</span><span class="sxs-lookup"><span data-stu-id="6a039-374">**Issue**</span></span> | <span data-ttu-id="6a039-375">Belirsiz bir iç uyarıyı NuGet engeller.</span><span class="sxs-lookup"><span data-stu-id="6a039-375">A non specific internal warning from NuGet.</span></span> |
| <span data-ttu-id="6a039-376">**Olası nedenler**</span><span class="sxs-lookup"><span data-stu-id="6a039-376">**Common causes**</span></span> | <span data-ttu-id="6a039-377">Daha fazla bilgi için günlükleri denetleyin</span><span class="sxs-lookup"><span data-stu-id="6a039-377">Check the logs for more information</span></span> |
