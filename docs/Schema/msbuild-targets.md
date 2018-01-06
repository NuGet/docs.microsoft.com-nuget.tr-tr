---
title: "NuGet paketi ve geri yükleme MSBuild hedefleri olarak | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 4/3/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 86f7e724-2509-4d7d-aa8d-4a3fb913ded6
description: "NuGet paketi ve geri yükleme, doğrudan NuGet 4.0 + ile MSBuild hedefleri olarak çalışabilir."
keywords: "NuGet ve MSBuild, NuGet paketi hedef, NuGet geri yükleme hedefi"
ms.reviewer: karann-msft
ms.openlocfilehash: d4778a21a96de6d76d7a20ff9a305960dd6c2bf1
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="273e9-104">NuGet paketi ve MSBuild hedefleri olarak geri yükleme</span><span class="sxs-lookup"><span data-stu-id="273e9-104">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="273e9-105">*NuGet 4.0 +*</span><span class="sxs-lookup"><span data-stu-id="273e9-105">*NuGet 4.0+*</span></span>

<span data-ttu-id="273e9-106">NuGet 4.0 +, bilgileri ile doğrudan çalışabilir bir `.csproj` ayrı bir gerektirmeden dosya `.nuspec` veya `project.json` dosyası.</span><span class="sxs-lookup"><span data-stu-id="273e9-106">NuGet 4.0+ can work directly with the information in a `.csproj` file without requiring a separate `.nuspec` or `project.json` file.</span></span> <span data-ttu-id="273e9-107">Bu yapılandırma dosyaları daha önce depolanan tüm meta veriler yerine depolanabilir `.csproj` doğrudan, burada açıklandığı gibi dosya.</span><span class="sxs-lookup"><span data-stu-id="273e9-107">All the metadata that was previously stored in those configuration files can be instead stored in the `.csproj` file directly, as described here.</span></span>

<span data-ttu-id="273e9-108">MSBuild ile 15.1 +, NuGet birinci sınıf MSBuild vatandaşı ile aynı zamanda olan `pack` ve `restore` aşağıda açıklandığı gibi hedefler.</span><span class="sxs-lookup"><span data-stu-id="273e9-108">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="273e9-109">Bu hedeflerde, diğer MSBuild görev veya hedef ile olduğu gibi NuGet ile çalışmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="273e9-109">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="273e9-110">(NuGet için 3.x ve daha önce kullandığınız [paketi](../tools/cli-ref-pack.md) ve [geri](../tools/cli-ref-restore.md) NuGet CLI aracılığıyla yerine komutları.)</span><span class="sxs-lookup"><span data-stu-id="273e9-110">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

<span data-ttu-id="273e9-111">Bu konuda:</span><span class="sxs-lookup"><span data-stu-id="273e9-111">In this topic:</span></span>

- [<span data-ttu-id="273e9-112">Hedef derleme sırası</span><span class="sxs-lookup"><span data-stu-id="273e9-112">Target build order</span></span>](#target-build-order)
- [<span data-ttu-id="273e9-113">paketi hedef</span><span class="sxs-lookup"><span data-stu-id="273e9-113">pack target</span></span>](#pack-target)
- [<span data-ttu-id="273e9-114">Paketi senaryoları</span><span class="sxs-lookup"><span data-stu-id="273e9-114">pack scenarios</span></span>](#pack-scenarios)
- [<span data-ttu-id="273e9-115">geri yükleme hedefi</span><span class="sxs-lookup"><span data-stu-id="273e9-115">restore target</span></span>](#restore-target)
- [<span data-ttu-id="273e9-116">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="273e9-116">PackageTargetFallback</span></span>](#packagetargetfallback)

## <a name="target-build-order"></a><span data-ttu-id="273e9-117">Hedef derleme sırası</span><span class="sxs-lookup"><span data-stu-id="273e9-117">Target build order</span></span>

<span data-ttu-id="273e9-118">Olduğundan `pack` ve `restore` MSBuild hedefleri şunlardır akışınızı artırmak için bunları erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="273e9-118">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="273e9-119">Örneğin, paket sonra bir ağ paylaşımına paketinizi kopyalamak istediğiniz varsayalım.</span><span class="sxs-lookup"><span data-stu-id="273e9-119">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="273e9-120">Bunu, proje dosyasında aşağıdaki ekleyerek yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="273e9-120">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
    <Copy
        SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
        DestinationFolder="\\myshare\packageshare\"
        />
</Target>
```

<span data-ttu-id="273e9-121">Benzer şekilde, bir MSBuild görev yazabileceğiniz, kendi hedef yazma ve MSBuild görevi NuGet özelliklerinde kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="273e9-121">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="273e9-122">paketi hedef</span><span class="sxs-lookup"><span data-stu-id="273e9-122">pack target</span></span>

<span data-ttu-id="273e9-123">Diğer bir deyişle, paketi hedef kullanırken `msbuild /t:pack`, MSBuild çizer girdilerinden gelen `.csproj` dosya yerine `project.json` veya `.nuspec` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="273e9-123">When using the pack target, that is, `msbuild /t:pack`, MSBuild draws its inputs from the `.csproj` file rather than `project.json` or `.nuspec` files.</span></span> <span data-ttu-id="273e9-124">Aşağıdaki tabloda eklenebilir MSBuild özellikleri açıklanmaktadır bir `.csproj` ilk dosyasında `<PropertyGroup>` düğümü.</span><span class="sxs-lookup"><span data-stu-id="273e9-124">The table below describes the MSBuild properties that can be added to a `.csproj` file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="273e9-125">Bu düzenlemeler kolayca Visual Studio 2017 ve daha sonra projeye sağ tıklayıp seçerek yapabileceğiniz **{project_name} Düzenle** bağlam menüsünde.</span><span class="sxs-lookup"><span data-stu-id="273e9-125">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="273e9-126">Kolaylık olması için tablo eşdeğer özelliği tarafından düzenlenir bir [ `.nuspec` dosya](../schema/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="273e9-126">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../schema/nuspec.md).</span></span>

<span data-ttu-id="273e9-127">Unutmayın `Owners` ve `Summary` özelliklerinden `.nuspec` MSBuild ile desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="273e9-127">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>


| <span data-ttu-id="273e9-128">Öznitelik/NuSpec değeri</span><span class="sxs-lookup"><span data-stu-id="273e9-128">Attribute/NuSpec Value</span></span> | <span data-ttu-id="273e9-129">MSBuild özelliği</span><span class="sxs-lookup"><span data-stu-id="273e9-129">MSBuild Property</span></span> | <span data-ttu-id="273e9-130">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="273e9-130">Default</span></span> | <span data-ttu-id="273e9-131">Notlar</span><span class="sxs-lookup"><span data-stu-id="273e9-131">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="273e9-132">Kimliği</span><span class="sxs-lookup"><span data-stu-id="273e9-132">Id</span></span> | <span data-ttu-id="273e9-133">Paket kimliği</span><span class="sxs-lookup"><span data-stu-id="273e9-133">PackageId</span></span> | <span data-ttu-id="273e9-134">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="273e9-134">AssemblyName</span></span> | <span data-ttu-id="273e9-135">MSBuild gelen $(AssemblyName)</span><span class="sxs-lookup"><span data-stu-id="273e9-135">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="273e9-136">Sürüm</span><span class="sxs-lookup"><span data-stu-id="273e9-136">Version</span></span> | <span data-ttu-id="273e9-137">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="273e9-137">PackageVersion</span></span> | <span data-ttu-id="273e9-138">Sürüm</span><span class="sxs-lookup"><span data-stu-id="273e9-138">Version</span></span> | <span data-ttu-id="273e9-139">Bu semver örnek "1.0.0", "1.0.0-beta" veya "1.0.0-beta-00345" için uyumlu değil</span><span class="sxs-lookup"><span data-stu-id="273e9-139">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="273e9-140">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="273e9-140">VersionPrefix</span></span> | <span data-ttu-id="273e9-141">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="273e9-141">PackageVersionPrefix</span></span> | <span data-ttu-id="273e9-142">empty</span><span class="sxs-lookup"><span data-stu-id="273e9-142">empty</span></span> | <span data-ttu-id="273e9-143">PackageVersion ayarı PackageVersionPrefix üzerine yazar</span><span class="sxs-lookup"><span data-stu-id="273e9-143">Setting PackageVersion will overwrite PackageVersionPrefix</span></span> |
| <span data-ttu-id="273e9-144">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="273e9-144">VersionSuffix</span></span> | <span data-ttu-id="273e9-145">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="273e9-145">PackageVersionSuffix</span></span> | <span data-ttu-id="273e9-146">empty</span><span class="sxs-lookup"><span data-stu-id="273e9-146">empty</span></span> | <span data-ttu-id="273e9-147">MSBuild gelen $(VersionSuffix).</span><span class="sxs-lookup"><span data-stu-id="273e9-147">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="273e9-148">PackageVersion ayarı PackageVersionSuffix üzerine yazar</span><span class="sxs-lookup"><span data-stu-id="273e9-148">Setting PackageVersion will overwrite PackageVersionSuffix</span></span> | 
| <span data-ttu-id="273e9-149">Yazarlar</span><span class="sxs-lookup"><span data-stu-id="273e9-149">Authors</span></span> | <span data-ttu-id="273e9-150">Yazarlar</span><span class="sxs-lookup"><span data-stu-id="273e9-150">Authors</span></span> | <span data-ttu-id="273e9-151">Geçerli kullanıcının kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="273e9-151">Username of the current user</span></span> | |
| <span data-ttu-id="273e9-152">Sahipleri</span><span class="sxs-lookup"><span data-stu-id="273e9-152">Owners</span></span> | <span data-ttu-id="273e9-153">Yok</span><span class="sxs-lookup"><span data-stu-id="273e9-153">N/A</span></span> | <span data-ttu-id="273e9-154">NuSpec içinde mevcut olmayan</span><span class="sxs-lookup"><span data-stu-id="273e9-154">Not present in NuSpec</span></span> | |
| <span data-ttu-id="273e9-155">Başlık</span><span class="sxs-lookup"><span data-stu-id="273e9-155">Title</span></span> | <span data-ttu-id="273e9-156">Başlık</span><span class="sxs-lookup"><span data-stu-id="273e9-156">Title</span></span> | <span data-ttu-id="273e9-157">Paket kimliği</span><span class="sxs-lookup"><span data-stu-id="273e9-157">The PackageId</span></span>| |
| <span data-ttu-id="273e9-158">Açıklama</span><span class="sxs-lookup"><span data-stu-id="273e9-158">Description</span></span> | <span data-ttu-id="273e9-159">Açıklama</span><span class="sxs-lookup"><span data-stu-id="273e9-159">Description</span></span> | <span data-ttu-id="273e9-160">"Paketi"</span><span class="sxs-lookup"><span data-stu-id="273e9-160">"Package Description"</span></span> | |
| <span data-ttu-id="273e9-161">Telif Hakkı</span><span class="sxs-lookup"><span data-stu-id="273e9-161">Copyright</span></span> | <span data-ttu-id="273e9-162">Telif Hakkı</span><span class="sxs-lookup"><span data-stu-id="273e9-162">Copyright</span></span> | <span data-ttu-id="273e9-163">empty</span><span class="sxs-lookup"><span data-stu-id="273e9-163">empty</span></span> | |
| <span data-ttu-id="273e9-164">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="273e9-164">RequireLicenseAcceptance</span></span> | <span data-ttu-id="273e9-165">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="273e9-165">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="273e9-166">false</span><span class="sxs-lookup"><span data-stu-id="273e9-166">false</span></span> | |
| <span data-ttu-id="273e9-167">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="273e9-167">LicenseUrl</span></span> | <span data-ttu-id="273e9-168">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="273e9-168">PackageLicenseUrl</span></span> | <span data-ttu-id="273e9-169">empty</span><span class="sxs-lookup"><span data-stu-id="273e9-169">empty</span></span> | |
| <span data-ttu-id="273e9-170">projectUrl</span><span class="sxs-lookup"><span data-stu-id="273e9-170">ProjectUrl</span></span> | <span data-ttu-id="273e9-171">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="273e9-171">PackageProjectUrl</span></span> | <span data-ttu-id="273e9-172">empty</span><span class="sxs-lookup"><span data-stu-id="273e9-172">empty</span></span> | |
| <span data-ttu-id="273e9-173">iconUrl</span><span class="sxs-lookup"><span data-stu-id="273e9-173">IconUrl</span></span> | <span data-ttu-id="273e9-174">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="273e9-174">PackageIconUrl</span></span> | <span data-ttu-id="273e9-175">empty</span><span class="sxs-lookup"><span data-stu-id="273e9-175">empty</span></span> | |
| <span data-ttu-id="273e9-176">Etiketler</span><span class="sxs-lookup"><span data-stu-id="273e9-176">Tags</span></span> | <span data-ttu-id="273e9-177">PackageTags</span><span class="sxs-lookup"><span data-stu-id="273e9-177">PackageTags</span></span> | <span data-ttu-id="273e9-178">empty</span><span class="sxs-lookup"><span data-stu-id="273e9-178">empty</span></span> | <span data-ttu-id="273e9-179">Etiketleri noktalı virgülle ayrılmış olan.</span><span class="sxs-lookup"><span data-stu-id="273e9-179">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="273e9-180">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="273e9-180">ReleaseNotes</span></span> | <span data-ttu-id="273e9-181">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="273e9-181">PackageReleaseNotes</span></span> | <span data-ttu-id="273e9-182">empty</span><span class="sxs-lookup"><span data-stu-id="273e9-182">empty</span></span> | |
| <span data-ttu-id="273e9-183">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="273e9-183">RepositoryUrl</span></span> | <span data-ttu-id="273e9-184">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="273e9-184">RepositoryUrl</span></span> | <span data-ttu-id="273e9-185">empty</span><span class="sxs-lookup"><span data-stu-id="273e9-185">empty</span></span> | |
| <span data-ttu-id="273e9-186">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="273e9-186">RepositoryType</span></span> | <span data-ttu-id="273e9-187">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="273e9-187">RepositoryType</span></span> | <span data-ttu-id="273e9-188">empty</span><span class="sxs-lookup"><span data-stu-id="273e9-188">empty</span></span> | |
| <span data-ttu-id="273e9-189">PackageType</span><span class="sxs-lookup"><span data-stu-id="273e9-189">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="273e9-190">Özet</span><span class="sxs-lookup"><span data-stu-id="273e9-190">Summary</span></span> | <span data-ttu-id="273e9-191">Desteklenmez</span><span class="sxs-lookup"><span data-stu-id="273e9-191">Not supported</span></span> | | |


### <a name="pack-target-inputs"></a><span data-ttu-id="273e9-192">paketi hedef girişleri</span><span class="sxs-lookup"><span data-stu-id="273e9-192">pack target inputs</span></span>

- <span data-ttu-id="273e9-193">IsPackable</span><span class="sxs-lookup"><span data-stu-id="273e9-193">IsPackable</span></span>
- <span data-ttu-id="273e9-194">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="273e9-194">PackageVersion</span></span>
- <span data-ttu-id="273e9-195">Paket kimliği</span><span class="sxs-lookup"><span data-stu-id="273e9-195">PackageId</span></span>
- <span data-ttu-id="273e9-196">Yazarlar</span><span class="sxs-lookup"><span data-stu-id="273e9-196">Authors</span></span>
- <span data-ttu-id="273e9-197">Açıklama</span><span class="sxs-lookup"><span data-stu-id="273e9-197">Description</span></span>
- <span data-ttu-id="273e9-198">Telif Hakkı</span><span class="sxs-lookup"><span data-stu-id="273e9-198">Copyright</span></span>
- <span data-ttu-id="273e9-199">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="273e9-199">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="273e9-200">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="273e9-200">DevelopmentDependency</span></span>
- <span data-ttu-id="273e9-201">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="273e9-201">PackageLicenseUrl</span></span>
- <span data-ttu-id="273e9-202">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="273e9-202">PackageProjectUrl</span></span>
- <span data-ttu-id="273e9-203">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="273e9-203">PackageIconUrl</span></span>
- <span data-ttu-id="273e9-204">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="273e9-204">PackageReleaseNotes</span></span>
- <span data-ttu-id="273e9-205">PackageTags</span><span class="sxs-lookup"><span data-stu-id="273e9-205">PackageTags</span></span>
- <span data-ttu-id="273e9-206">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="273e9-206">PackageOutputPath</span></span>
- <span data-ttu-id="273e9-207">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="273e9-207">IncludeSymbols</span></span>
- <span data-ttu-id="273e9-208">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="273e9-208">IncludeSource</span></span>
- <span data-ttu-id="273e9-209">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="273e9-209">PackageTypes</span></span>
- <span data-ttu-id="273e9-210">IsTool</span><span class="sxs-lookup"><span data-stu-id="273e9-210">IsTool</span></span>
- <span data-ttu-id="273e9-211">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="273e9-211">RepositoryUrl</span></span>
- <span data-ttu-id="273e9-212">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="273e9-212">RepositoryType</span></span>
- <span data-ttu-id="273e9-213">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="273e9-213">NoPackageAnalysis</span></span>
- <span data-ttu-id="273e9-214">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="273e9-214">MinClientVersion</span></span>
- <span data-ttu-id="273e9-215">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="273e9-215">IncludeBuildOutput</span></span>
- <span data-ttu-id="273e9-216">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="273e9-216">IncludeContentInPack</span></span>
- <span data-ttu-id="273e9-217">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="273e9-217">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="273e9-218">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="273e9-218">ContentTargetFolders</span></span>
- <span data-ttu-id="273e9-219">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="273e9-219">NuspecFile</span></span>
- <span data-ttu-id="273e9-220">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="273e9-220">NuspecBasePath</span></span>
- <span data-ttu-id="273e9-221">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="273e9-221">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="273e9-222">Paketi senaryoları</span><span class="sxs-lookup"><span data-stu-id="273e9-222">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="273e9-223">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="273e9-223">PackageIconUrl</span></span>

<span data-ttu-id="273e9-224">Değişikliğin parçası olarak [NuGet sorunu 2582](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` sonunda değiştirilecek `PackageIconUri` ve sonuçta elde edilen paketin kökünde bulunan bir simge dosyası için göreli bir yol olabilir.</span><span class="sxs-lookup"><span data-stu-id="273e9-224">As part of the change for [NuGet Issue 2582](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="273e9-225">Çıktı derlemeler</span><span class="sxs-lookup"><span data-stu-id="273e9-225">Output assemblies</span></span>

<span data-ttu-id="273e9-226">`nuget pack`kopya çıktı uzantılara sahip dosyaları `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, ve `.pri`.</span><span class="sxs-lookup"><span data-stu-id="273e9-226">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="273e9-227">MSBuild gelen sağladıkları üzerinde kopyalanır ve çıkış dosyalarının bağımlı `BuiltOutputProjectGroup` hedef.</span><span class="sxs-lookup"><span data-stu-id="273e9-227">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="273e9-228">Çıkış derlemelerinin nereye proje dosyası veya komut satırı denetlemek için kullanabileceğiniz iki MSBuild özellikleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="273e9-228">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="273e9-229">`IncludeBuildOutput`: Derleme çıktı derlemelerinin pakete dahil edilip edilmeyeceğini belirler bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="273e9-229">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="273e9-230">`BuildOutputTargetFolder`: Çıktı derlemelerinin yerleştirilmelidir klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="273e9-230">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="273e9-231">Çıktı derlemelerinin (ve diğer çıktı dosyaları) ilgili framework klasörlerine kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="273e9-231">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="273e9-232">Paket referanslarını</span><span class="sxs-lookup"><span data-stu-id="273e9-232">Package references</span></span>

<span data-ttu-id="273e9-233">Bkz: [paketini proje dosyalarını başvurularında](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="273e9-233">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="273e9-234">Proje başvuruları projeye</span><span class="sxs-lookup"><span data-stu-id="273e9-234">Project to project references</span></span>

<span data-ttu-id="273e9-235">Proje başvuruları projeye değerlendirilir varsayılan olarak nuget paket referanslarını, örneğin:</span><span class="sxs-lookup"><span data-stu-id="273e9-235">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="273e9-236">Ayrıca, aşağıdaki meta verileri, proje başvurusu ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="273e9-236">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="273e9-237">Bir paketteki içerik dahil olmak üzere</span><span class="sxs-lookup"><span data-stu-id="273e9-237">Including content in a package</span></span>

<span data-ttu-id="273e9-238">İçerik eklemek için fazladan meta verileri, mevcut eklemek `<Content>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="273e9-238">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="273e9-239">Varsayılan olarak girişlerle geçersiz kılma sürece "İçerik" paketinde türünde her şeyi ister aşağıdakiler:</span><span class="sxs-lookup"><span data-stu-id="273e9-239">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
    <Content Include="..\win7-x64\libuv.txt">
        <Pack>false</Pack>
    </Content>
 ```

<span data-ttu-id="273e9-240">Varsayılan olarak, her şeyi köküne eklenen `content` ve `contentFiles\any\<target_framework>` bir paket ve korur klasördeki göreli klasör yapısı, bir paket yolu belirtmediğiniz sürece:</span><span class="sxs-lookup"><span data-stu-id="273e9-240">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">        
    <Pack>true</Pack>
    <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="273e9-241">Yalnızca belirli bir tüm içeriğinizi kopyalamak isterseniz klasörlerde kök (yerine `content` ve `contentFiles` her ikisi de), MSBuild özelliği kullanabilirsiniz `ContentTargetFolders`, varsayılan olarak "içerik; Content dosyaları" ancak başka bir klasör adı için ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="273e9-241">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="273e9-242">Not "Content dosyaları" belirterek, yalnızca `ContentTargetFolders` altında dosyaları koyan `contentFiles\any\<target_framework>` veya `contentFiles\<language>\<target_framework>` göre `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="273e9-242">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="273e9-243">`PackagePath`hedef yolları noktalı virgülle ayrılmış bir kümesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="273e9-243">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="273e9-244">Bir boş paket yolu belirterek dosya paket köküne ekleyin.</span><span class="sxs-lookup"><span data-stu-id="273e9-244">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="273e9-245">Örneğin, aşağıdaki ekler `libuv.txt` için `content\myfiles`, `content\samples`ve paket kök:</span><span class="sxs-lookup"><span data-stu-id="273e9-245">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="273e9-246">Ayrıca bir MSBuild özelliği olan `$(IncludeContentInPack)`, varsayılan olarak `true`.</span><span class="sxs-lookup"><span data-stu-id="273e9-246">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="273e9-247">Bu ayarlanırsa `false` hiçbir projede sonra proje içerikten eklenmemiştir nuget paketi.</span><span class="sxs-lookup"><span data-stu-id="273e9-247">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="273e9-248">Yukarıdaki öğelerin hiçbirinde ayarlayabilirsiniz diğer paketi belirli meta verileri içeren ```<PackageCopyToOutput>``` ve ```<PackageFlatten>``` hangi kümeleri ```CopyToOutput``` ve ```Flatten``` üzerinde değerleri ```contentFiles``` çıkış nuspec girişi.</span><span class="sxs-lookup"><span data-stu-id="273e9-248">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>


> [!Note]
> <span data-ttu-id="273e9-249">İçerik öğeleri dışında `<Pack>` ve `<PackagePath>` meta verileri de ayarlanabilir derleme, EmbeddedResource, ApplicationDefinition, sayfa, kaynak, KarşılamaEkranı, DesignData, DesignDataWithDesignTimeCreatableTypes, yapı eylemiyle dosyalarda CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource veya yok.</span><span class="sxs-lookup"><span data-stu-id="273e9-249">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreatableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="273e9-250">Dosya adı, paket yolu genelleme desenleri kullanırken eklenecek paketi için paket yolu paket yoluyla dosya adını içeren tam yol kabul edilir klasör ayırıcı karakter, aksi takdirde ile bitmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="273e9-250">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="273e9-251">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="273e9-251">IncludeSymbols</span></span>

<span data-ttu-id="273e9-252">Kullanırken `MSBuild /t:pack /p:IncludeSymbols=true`, karşılık gelen `.pdb` dosyaları, diğer çıkış dosyalarının yanı sıra kopyalanır (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="273e9-252">When using `MSBuild /t:pack /p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="273e9-253">Bu ayarı Not `IncludeSymbols=true` normal bir paket oluşturur *ve* simge paketi.</span><span class="sxs-lookup"><span data-stu-id="273e9-253">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="273e9-254">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="273e9-254">IncludeSource</span></span>

<span data-ttu-id="273e9-255">Bu aynı sonucu verir `IncludeSymbols`ile birlikte kaynak dosyalarını kopyalar dışında `.pdb` da dosyaları.</span><span class="sxs-lookup"><span data-stu-id="273e9-255">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="273e9-256">Tüm dosya türlerini `Compile` üzerinden kopyalanır `src\<ProjectName>\` elde edilen paketindeki göreli yol klasör yapısı korunarak.</span><span class="sxs-lookup"><span data-stu-id="273e9-256">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="273e9-257">Aynı kaynak dosyaları herhangi da yapılır `ProjectReference` olan `TreatAsPackageReference` kümesine `false`.</span><span class="sxs-lookup"><span data-stu-id="273e9-257">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="273e9-258">Dosya türü derlemek için yeni eklenen sonra proje klasörünün dışında varsa, `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="273e9-258">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="istool"></a><span data-ttu-id="273e9-259">IsTool</span><span class="sxs-lookup"><span data-stu-id="273e9-259">IsTool</span></span>

<span data-ttu-id="273e9-260">Kullanırken `MSBuild /t:pack /p:IsTool=true`, tüm dosyaları belirtilen çıktı [çıkış derlemelerinin](#output-assemblies) senaryosu, kopyalanır `tools` klasörü yerine `lib` klasör.</span><span class="sxs-lookup"><span data-stu-id="273e9-260">When using `MSBuild /t:pack /p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="273e9-261">Bu farklı olduğuna dikkat edin bir `DotNetCliTool` , belirtilen ayarlayarak `PackageType` içinde `.csproj` dosya.</span><span class="sxs-lookup"><span data-stu-id="273e9-261">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="273e9-262">Bir .nuspec kullanarak paketleme</span><span class="sxs-lookup"><span data-stu-id="273e9-262">Packing using a .nuspec</span></span>

<span data-ttu-id="273e9-263">Kullanabileceğiniz bir `.nuspec` içeri aktarmak için bir proje dosyasına sahip olması koşuluyla, projenizin paketi dosyaya `NuGet.Build.Tasks.Pack.targets` böylece paketi görevi çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="273e9-263">You can use a `.nuspec` file to pack your project provided that you have a project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="273e9-264">Aşağıdaki üç MSBuild özellikleri kullanarak paket için uygun olan bir `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="273e9-264">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="273e9-265">`NuspecFile`: göreli veya mutlak bir yol `.nuspec` paketleme için kullanılan dosya.</span><span class="sxs-lookup"><span data-stu-id="273e9-265">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="273e9-266">`NuspecProperties`: noktalı virgülle ayrılmış listesini anahtar = değer çiftleri.</span><span class="sxs-lookup"><span data-stu-id="273e9-266">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="273e9-267">MSBuild komut satırı ayrıştırma works yöntemi nedeniyle birden çok özellikleri şu şekilde belirtilmelidir: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="273e9-267">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="273e9-268">`NuspecBasePath`: Temel yolu `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="273e9-268">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="273e9-269">Kullanıyorsanız `dotnet.exe` projenizi paketi için bir komut aşağıdaki gibi kullanın:</span><span class="sxs-lookup"><span data-stu-id="273e9-269">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="273e9-270">MSBuild projenizi Paketi kullanıyorsanız, aşağıdaki gibi bir komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="273e9-270">If using MSBuild to pack your project, use a command like the following:</span></span>

```
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

## <a name="restore-target"></a><span data-ttu-id="273e9-271">geri yükleme hedefi</span><span class="sxs-lookup"><span data-stu-id="273e9-271">restore target</span></span>

<span data-ttu-id="273e9-272">`MSBuild /t:restore`(hangi `nuget restore` ve `dotnet restore` .NET Core projeleriyle kullanmak), proje dosyasında aşağıdaki gibi başvurduğu paketleri yükler:</span><span class="sxs-lookup"><span data-stu-id="273e9-272">`MSBuild /t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="273e9-273">Tüm proje için proje başvuruları okuma</span><span class="sxs-lookup"><span data-stu-id="273e9-273">Read all project to project references</span></span>
1. <span data-ttu-id="273e9-274">Ara klasörü ve hedef çerçeveleri bulmak için proje özelliklerini okuma</span><span class="sxs-lookup"><span data-stu-id="273e9-274">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="273e9-275">Msbuild veri NuGet.Build.Tasks.dll geçirmek</span><span class="sxs-lookup"><span data-stu-id="273e9-275">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="273e9-276">Geri yükleme çalıştırma</span><span class="sxs-lookup"><span data-stu-id="273e9-276">Run restore</span></span>
1. <span data-ttu-id="273e9-277">Paketleri indirin</span><span class="sxs-lookup"><span data-stu-id="273e9-277">Download packages</span></span>
1. <span data-ttu-id="273e9-278">Varlıklar dosya, hedefleri ve özellik yazma</span><span class="sxs-lookup"><span data-stu-id="273e9-278">Write assets file, targets, and props</span></span>


### <a name="restore-properties"></a><span data-ttu-id="273e9-279">Özellikler geri yükleme</span><span class="sxs-lookup"><span data-stu-id="273e9-279">Restore properties</span></span>

<span data-ttu-id="273e9-280">Ek geri yükleme ayarlarını MSBuild proje dosyası özelliklerinde alınması.</span><span class="sxs-lookup"><span data-stu-id="273e9-280">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="273e9-281">Değerleri de ayarlanabilir kullanarak komut satırından `/p:` geçiş (aşağıdaki örneklere bakın).</span><span class="sxs-lookup"><span data-stu-id="273e9-281">Values can also be set from the command line using the `/p:` switch (see Examples below).</span></span>

| <span data-ttu-id="273e9-282">Özellik</span><span class="sxs-lookup"><span data-stu-id="273e9-282">Property</span></span> | <span data-ttu-id="273e9-283">Açıklama</span><span class="sxs-lookup"><span data-stu-id="273e9-283">Description</span></span> |
|--------|--------|
| <span data-ttu-id="273e9-284">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="273e9-284">RestoreSources</span></span> | <span data-ttu-id="273e9-285">Paket kaynaklarını noktalı virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="273e9-285">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="273e9-286">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="273e9-286">RestorePackagesPath</span></span> | <span data-ttu-id="273e9-287">Kullanıcı paketleri klasör yolu.</span><span class="sxs-lookup"><span data-stu-id="273e9-287">User packages folder path.</span></span> |
| <span data-ttu-id="273e9-288">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="273e9-288">RestoreDisableParallel</span></span> | <span data-ttu-id="273e9-289">Bir seferde bir sınır indirir.</span><span class="sxs-lookup"><span data-stu-id="273e9-289">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="273e9-290">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="273e9-290">RestoreConfigFile</span></span> | <span data-ttu-id="273e9-291">Yol için bir `Nuget.Config` uygulamak için dosya.</span><span class="sxs-lookup"><span data-stu-id="273e9-291">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="273e9-292">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="273e9-292">RestoreNoCache</span></span> | <span data-ttu-id="273e9-293">TRUE ise, web önbelleği kullanılarak önler.</span><span class="sxs-lookup"><span data-stu-id="273e9-293">If true, avoids using the web cache.</span></span> |
| <span data-ttu-id="273e9-294">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="273e9-294">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="273e9-295">TRUE ise, başarısız olan veya eksik paket kaynaklarını yok sayar.</span><span class="sxs-lookup"><span data-stu-id="273e9-295">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="273e9-296">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="273e9-296">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="273e9-297">Yolu `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="273e9-297">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="273e9-298">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="273e9-298">RestoreGraphProjectInput</span></span> | <span data-ttu-id="273e9-299">Mutlak yollar içermesi gereken geri yüklemek için projeleri noktalı virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="273e9-299">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="273e9-300">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="273e9-300">RestoreOutputPath</span></span> | <span data-ttu-id="273e9-301">Çıkış klasörüne varsayarak, `obj` klasörü.</span><span class="sxs-lookup"><span data-stu-id="273e9-301">Output folder, defaulting to the `obj` folder.</span></span> |

<span data-ttu-id="273e9-302">**Örnekler**</span><span class="sxs-lookup"><span data-stu-id="273e9-302">**Examples**</span></span>

<span data-ttu-id="273e9-303">Komut satırı:</span><span class="sxs-lookup"><span data-stu-id="273e9-303">Command line:</span></span>

```
msbuild /t:restore /p:RestoreConfigFile=<path>
```

<span data-ttu-id="273e9-304">Proje dosyası:</span><span class="sxs-lookup"><span data-stu-id="273e9-304">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
<PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="273e9-305">Çıkış geri yükleme</span><span class="sxs-lookup"><span data-stu-id="273e9-305">Restore outputs</span></span>

<span data-ttu-id="273e9-306">Geri yükleme yapı aşağıdaki dosyaları oluşturur `obj` klasörü:</span><span class="sxs-lookup"><span data-stu-id="273e9-306">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="273e9-307">Dosya</span><span class="sxs-lookup"><span data-stu-id="273e9-307">File</span></span> | <span data-ttu-id="273e9-308">Açıklama</span><span class="sxs-lookup"><span data-stu-id="273e9-308">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="273e9-309">Daha önce`project.lock.json`</span><span class="sxs-lookup"><span data-stu-id="273e9-309">Previously `project.lock.json`</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="273e9-310">MSBuild özellik paketlerinde bulunan başvurular</span><span class="sxs-lookup"><span data-stu-id="273e9-310">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="273e9-311">MSBuild hedefleri paketlerinde bulunan başvurular</span><span class="sxs-lookup"><span data-stu-id="273e9-311">References to MSBuild targets contained in packages</span></span> |


### <a name="packagetargetfallback"></a><span data-ttu-id="273e9-312">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="273e9-312">PackageTargetFallback</span></span> 

<span data-ttu-id="273e9-313">`PackageTargetFallback` Öğesi paketleri geri yüklenirken kullanılacak uyumlu hedefleri kümesi belirtmenize olanak verir (denk [ `imports` içinde `project.json` ](../schema/project-json.md#imports)).</span><span class="sxs-lookup"><span data-stu-id="273e9-313">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages (the equivalent of [`imports` in `project.json`](../schema/project-json.md#imports)).</span></span> <span data-ttu-id="273e9-314">Bir dotnet kullanmak paketleri izin vermek için tasarlanmış [TxM](../schema/target-frameworks.md) dotnet TxM bildirmeyin uyumlu paketlerle çalışmak için.</span><span class="sxs-lookup"><span data-stu-id="273e9-314">It's designed to allow packages that use a dotnet [TxM](../schema/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="273e9-315">Projeniz TxM dotnet kullanıyorsa, eklediğiniz sürece diğer bir deyişle, daha sonra bağlı olduğu gereken üzerinde de tüm paketler dotnet TxM, olması `<PackageTargetFallback>` dotnet ile uyumlu olacak şekilde dotnet olmayan platformları izin vermek üzere projenize.</span><span class="sxs-lookup"><span data-stu-id="273e9-315">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span> 

<span data-ttu-id="273e9-316">Proje kullanıyorsa, örneğin, `netstandard1.6` TxM ve bağımlı paketi içeren yalnızca `lib/net45/a.dll` ve `lib/portable-net45+win81/a.dll`, projeyi oluşturmak başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="273e9-316">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="273e9-317">Getirileceğini istediğiniz ikinci DLL'dir sonra ekleyebileceğiniz bir `PackageTargetFallback` gibi söylemek için `portable-net45+win81` DLL uyumludur:</span><span class="sxs-lookup"><span data-stu-id="273e9-317">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="273e9-318">Projenizdeki tüm hedefler için bir geri dönüş bildirmek için devre dışı bırakın `Condition` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="273e9-318">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="273e9-319">Var olan genişletebilirsiniz `PackageTargetFallback` ekleyerek `$(PackageTargetFallback)` aşağıda gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="273e9-319">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```


### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="273e9-320">Bir geri yükleme grafik bir kitaplıktan değiştirme</span><span class="sxs-lookup"><span data-stu-id="273e9-320">Replacing one library from a restore graph</span></span>

<span data-ttu-id="273e9-321">Bir geri yükleme yanlış derleme getiren, paketleri seçim varsayılan ve kendi seçimi ile değiştir dışlamak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="273e9-321">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="273e9-322">Üst düzey ile ilk `PackageReference`, tüm varlıklar çıkar:</span><span class="sxs-lookup"><span data-stu-id="273e9-322">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
    <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="273e9-323">Ardından, DLL uygun yerel kopyasını kendi başvuru ekleyin:</span><span class="sxs-lookup"><span data-stu-id="273e9-323">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
