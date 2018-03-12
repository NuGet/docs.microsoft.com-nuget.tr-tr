---
title: "NuGet paketi ve geri yükleme MSBuild hedefleri olarak | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 04/03/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet paketi ve geri yükleme, doğrudan NuGet 4.0 + ile MSBuild hedefleri olarak çalışabilir."
keywords: "NuGet ve MSBuild, NuGet paketi hedef, NuGet geri yükleme hedefi"
ms.reviewer:
- karann-msft
ms.openlocfilehash: 798b3550718294072d86b6e4827ec5017178d2cc
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/08/2018
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="45c4a-104">NuGet paketi ve MSBuild hedefleri olarak geri yükleme</span><span class="sxs-lookup"><span data-stu-id="45c4a-104">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="45c4a-105">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="45c4a-105">*NuGet 4.0+*</span></span>

<span data-ttu-id="45c4a-106">PackageReference biçimiyle NuGet 4.0 + doğrudan ayrı bir kullanmak yerine bir proje dosyası içinde tüm bildirim meta veri depolayabilirsiniz `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="45c4a-106">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="45c4a-107">MSBuild ile 15.1 +, NuGet birinci sınıf MSBuild vatandaşı ile aynı zamanda olan `pack` ve `restore` aşağıda açıklandığı gibi hedefler.</span><span class="sxs-lookup"><span data-stu-id="45c4a-107">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="45c4a-108">Bu hedeflerde, diğer MSBuild görev veya hedef ile olduğu gibi NuGet ile çalışmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="45c4a-108">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="45c4a-109">(NuGet için 3.x ve daha önce kullandığınız [paketi](../tools/cli-ref-pack.md) ve [geri](../tools/cli-ref-restore.md) NuGet CLI aracılığıyla yerine komutları.)</span><span class="sxs-lookup"><span data-stu-id="45c4a-109">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="45c4a-110">Hedef derleme sırası</span><span class="sxs-lookup"><span data-stu-id="45c4a-110">Target build order</span></span>

<span data-ttu-id="45c4a-111">Olduğundan `pack` ve `restore` MSBuild hedefleri şunlardır akışınızı artırmak için bunları erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45c4a-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="45c4a-112">Örneğin, paket sonra bir ağ paylaşımına paketinizi kopyalamak istediğiniz varsayalım.</span><span class="sxs-lookup"><span data-stu-id="45c4a-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="45c4a-113">Bunu, proje dosyasında aşağıdaki ekleyerek yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="45c4a-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
    <Copy
        SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
        DestinationFolder="\\myshare\packageshare\"
        />
</Target>
```

<span data-ttu-id="45c4a-114">Benzer şekilde, bir MSBuild görev yazabileceğiniz, kendi hedef yazma ve MSBuild görevi NuGet özelliklerinde kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="45c4a-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="45c4a-115">paketi hedef</span><span class="sxs-lookup"><span data-stu-id="45c4a-115">pack target</span></span>

<span data-ttu-id="45c4a-116">Diğer bir deyişle, paketi hedef kullanırken `msbuild /t:pack`, MSBuild proje dosyasından girdilerinden çizer.</span><span class="sxs-lookup"><span data-stu-id="45c4a-116">When using the pack target, that is, `msbuild /t:pack`, MSBuild draws its inputs from the project file.</span></span> <span data-ttu-id="45c4a-117">Proje dosyası içinde ilk eklenebilir MSBuild özellikler aşağıdaki tabloda açıklanmıştır `<PropertyGroup>` düğümü.</span><span class="sxs-lookup"><span data-stu-id="45c4a-117">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="45c4a-118">Bu düzenlemeler kolayca Visual Studio 2017 ve daha sonra projeye sağ tıklayıp seçerek yapabileceğiniz **{project_name} Düzenle** bağlam menüsünde.</span><span class="sxs-lookup"><span data-stu-id="45c4a-118">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="45c4a-119">Kolaylık olması için tablo eşdeğer özelliği tarafından düzenlenir bir [ `.nuspec` dosya](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="45c4a-119">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="45c4a-120">Unutmayın `Owners` ve `Summary` özelliklerinden `.nuspec` MSBuild ile desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="45c4a-120">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="45c4a-121">Öznitelik/NuSpec değeri</span><span class="sxs-lookup"><span data-stu-id="45c4a-121">Attribute/NuSpec Value</span></span> | <span data-ttu-id="45c4a-122">MSBuild özelliği</span><span class="sxs-lookup"><span data-stu-id="45c4a-122">MSBuild Property</span></span> | <span data-ttu-id="45c4a-123">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="45c4a-123">Default</span></span> | <span data-ttu-id="45c4a-124">Notlar</span><span class="sxs-lookup"><span data-stu-id="45c4a-124">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="45c4a-125">Kimliği</span><span class="sxs-lookup"><span data-stu-id="45c4a-125">Id</span></span> | <span data-ttu-id="45c4a-126">PackageId</span><span class="sxs-lookup"><span data-stu-id="45c4a-126">PackageId</span></span> | <span data-ttu-id="45c4a-127">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="45c4a-127">AssemblyName</span></span> | <span data-ttu-id="45c4a-128">MSBuild gelen $(AssemblyName)</span><span class="sxs-lookup"><span data-stu-id="45c4a-128">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="45c4a-129">Sürüm</span><span class="sxs-lookup"><span data-stu-id="45c4a-129">Version</span></span> | <span data-ttu-id="45c4a-130">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="45c4a-130">PackageVersion</span></span> | <span data-ttu-id="45c4a-131">Sürüm</span><span class="sxs-lookup"><span data-stu-id="45c4a-131">Version</span></span> | <span data-ttu-id="45c4a-132">Bu semver örnek "1.0.0", "1.0.0-beta" veya "1.0.0-beta-00345" için uyumlu değil</span><span class="sxs-lookup"><span data-stu-id="45c4a-132">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="45c4a-133">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="45c4a-133">VersionPrefix</span></span> | <span data-ttu-id="45c4a-134">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="45c4a-134">PackageVersionPrefix</span></span> | <span data-ttu-id="45c4a-135">empty</span><span class="sxs-lookup"><span data-stu-id="45c4a-135">empty</span></span> | <span data-ttu-id="45c4a-136">PackageVersionPrefix PackageVersion ayarını geçersiz kılar</span><span class="sxs-lookup"><span data-stu-id="45c4a-136">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="45c4a-137">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="45c4a-137">VersionSuffix</span></span> | <span data-ttu-id="45c4a-138">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="45c4a-138">PackageVersionSuffix</span></span> | <span data-ttu-id="45c4a-139">empty</span><span class="sxs-lookup"><span data-stu-id="45c4a-139">empty</span></span> | <span data-ttu-id="45c4a-140">MSBuild gelen $(VersionSuffix).</span><span class="sxs-lookup"><span data-stu-id="45c4a-140">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="45c4a-141">PackageVersionSuffix PackageVersion ayarını geçersiz kılar</span><span class="sxs-lookup"><span data-stu-id="45c4a-141">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="45c4a-142">Yazarlar</span><span class="sxs-lookup"><span data-stu-id="45c4a-142">Authors</span></span> | <span data-ttu-id="45c4a-143">Yazarlar</span><span class="sxs-lookup"><span data-stu-id="45c4a-143">Authors</span></span> | <span data-ttu-id="45c4a-144">Geçerli kullanıcının kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="45c4a-144">Username of the current user</span></span> | |
| <span data-ttu-id="45c4a-145">Sahipleri</span><span class="sxs-lookup"><span data-stu-id="45c4a-145">Owners</span></span> | <span data-ttu-id="45c4a-146">Yok</span><span class="sxs-lookup"><span data-stu-id="45c4a-146">N/A</span></span> | <span data-ttu-id="45c4a-147">NuSpec içinde mevcut olmayan</span><span class="sxs-lookup"><span data-stu-id="45c4a-147">Not present in NuSpec</span></span> | |
| <span data-ttu-id="45c4a-148">Başlık</span><span class="sxs-lookup"><span data-stu-id="45c4a-148">Title</span></span> | <span data-ttu-id="45c4a-149">Başlık</span><span class="sxs-lookup"><span data-stu-id="45c4a-149">Title</span></span> | <span data-ttu-id="45c4a-150">Paket kimliği</span><span class="sxs-lookup"><span data-stu-id="45c4a-150">The PackageId</span></span>| |
| <span data-ttu-id="45c4a-151">Açıklama</span><span class="sxs-lookup"><span data-stu-id="45c4a-151">Description</span></span> | <span data-ttu-id="45c4a-152">PackageDescription</span><span class="sxs-lookup"><span data-stu-id="45c4a-152">PackageDescription</span></span> | <span data-ttu-id="45c4a-153">"Paketi"</span><span class="sxs-lookup"><span data-stu-id="45c4a-153">"Package Description"</span></span> | |
| <span data-ttu-id="45c4a-154">Telif Hakkı</span><span class="sxs-lookup"><span data-stu-id="45c4a-154">Copyright</span></span> | <span data-ttu-id="45c4a-155">Telif Hakkı</span><span class="sxs-lookup"><span data-stu-id="45c4a-155">Copyright</span></span> | <span data-ttu-id="45c4a-156">empty</span><span class="sxs-lookup"><span data-stu-id="45c4a-156">empty</span></span> | |
| <span data-ttu-id="45c4a-157">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="45c4a-157">RequireLicenseAcceptance</span></span> | <span data-ttu-id="45c4a-158">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="45c4a-158">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="45c4a-159">false</span><span class="sxs-lookup"><span data-stu-id="45c4a-159">false</span></span> | |
| <span data-ttu-id="45c4a-160">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="45c4a-160">LicenseUrl</span></span> | <span data-ttu-id="45c4a-161">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="45c4a-161">PackageLicenseUrl</span></span> | <span data-ttu-id="45c4a-162">empty</span><span class="sxs-lookup"><span data-stu-id="45c4a-162">empty</span></span> | |
| <span data-ttu-id="45c4a-163">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="45c4a-163">ProjectUrl</span></span> | <span data-ttu-id="45c4a-164">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="45c4a-164">PackageProjectUrl</span></span> | <span data-ttu-id="45c4a-165">empty</span><span class="sxs-lookup"><span data-stu-id="45c4a-165">empty</span></span> | |
| <span data-ttu-id="45c4a-166">IconUrl</span><span class="sxs-lookup"><span data-stu-id="45c4a-166">IconUrl</span></span> | <span data-ttu-id="45c4a-167">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="45c4a-167">PackageIconUrl</span></span> | <span data-ttu-id="45c4a-168">empty</span><span class="sxs-lookup"><span data-stu-id="45c4a-168">empty</span></span> | |
| <span data-ttu-id="45c4a-169">Etiketler</span><span class="sxs-lookup"><span data-stu-id="45c4a-169">Tags</span></span> | <span data-ttu-id="45c4a-170">PackageTags</span><span class="sxs-lookup"><span data-stu-id="45c4a-170">PackageTags</span></span> | <span data-ttu-id="45c4a-171">empty</span><span class="sxs-lookup"><span data-stu-id="45c4a-171">empty</span></span> | <span data-ttu-id="45c4a-172">Etiketleri noktalı virgülle ayrılmış olan.</span><span class="sxs-lookup"><span data-stu-id="45c4a-172">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="45c4a-173">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="45c4a-173">ReleaseNotes</span></span> | <span data-ttu-id="45c4a-174">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="45c4a-174">PackageReleaseNotes</span></span> | <span data-ttu-id="45c4a-175">empty</span><span class="sxs-lookup"><span data-stu-id="45c4a-175">empty</span></span> | |
| <span data-ttu-id="45c4a-176">Depo/URL'si</span><span class="sxs-lookup"><span data-stu-id="45c4a-176">Repository/Url</span></span> | <span data-ttu-id="45c4a-177">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="45c4a-177">RepositoryUrl</span></span> | <span data-ttu-id="45c4a-178">empty</span><span class="sxs-lookup"><span data-stu-id="45c4a-178">empty</span></span> | <span data-ttu-id="45c4a-179">Depo URL'si kopyalama veya kaynak kodu almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="45c4a-179">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="45c4a-180">Örnek: *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="45c4a-180">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="45c4a-181">Depo/türü</span><span class="sxs-lookup"><span data-stu-id="45c4a-181">Repository/Type</span></span> | <span data-ttu-id="45c4a-182">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="45c4a-182">RepositoryType</span></span> | <span data-ttu-id="45c4a-183">empty</span><span class="sxs-lookup"><span data-stu-id="45c4a-183">empty</span></span> | <span data-ttu-id="45c4a-184">Depo türü.</span><span class="sxs-lookup"><span data-stu-id="45c4a-184">Repository type.</span></span> <span data-ttu-id="45c4a-185">Örnekler: *git*, *tfs*.</span><span class="sxs-lookup"><span data-stu-id="45c4a-185">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="45c4a-186">Depo/şube</span><span class="sxs-lookup"><span data-stu-id="45c4a-186">Repository/Branch</span></span> | <span data-ttu-id="45c4a-187">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="45c4a-187">RepositoryBranch</span></span> | <span data-ttu-id="45c4a-188">empty</span><span class="sxs-lookup"><span data-stu-id="45c4a-188">empty</span></span> | <span data-ttu-id="45c4a-189">İsteğe bağlı depo şube bilgileri.</span><span class="sxs-lookup"><span data-stu-id="45c4a-189">Optional repository branch information.</span></span> <span data-ttu-id="45c4a-190">*RepositoryUrl* dahil edilmek üzere bu özellik için de belirtilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="45c4a-190">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="45c4a-191">Örnek: *ana* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="45c4a-191">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="45c4a-192">Depo/tamamlama</span><span class="sxs-lookup"><span data-stu-id="45c4a-192">Repository/Commit</span></span> | <span data-ttu-id="45c4a-193">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="45c4a-193">RepositoryCommit</span></span> | <span data-ttu-id="45c4a-194">empty</span><span class="sxs-lookup"><span data-stu-id="45c4a-194">empty</span></span> | <span data-ttu-id="45c4a-195">İsteğe bağlı depo yürütme veya, paket kaynak belirtmek için değişiklik karşı oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="45c4a-195">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="45c4a-196">*RepositoryUrl* dahil edilmek üzere bu özellik için de belirtilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="45c4a-196">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="45c4a-197">Örnek: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="45c4a-197">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="45c4a-198">PackageType</span><span class="sxs-lookup"><span data-stu-id="45c4a-198">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="45c4a-199">Özet</span><span class="sxs-lookup"><span data-stu-id="45c4a-199">Summary</span></span> | <span data-ttu-id="45c4a-200">Desteklenmez</span><span class="sxs-lookup"><span data-stu-id="45c4a-200">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="45c4a-201">paketi hedef girişleri</span><span class="sxs-lookup"><span data-stu-id="45c4a-201">pack target inputs</span></span>

- <span data-ttu-id="45c4a-202">IsPackable</span><span class="sxs-lookup"><span data-stu-id="45c4a-202">IsPackable</span></span>
- <span data-ttu-id="45c4a-203">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="45c4a-203">PackageVersion</span></span>
- <span data-ttu-id="45c4a-204">PackageId</span><span class="sxs-lookup"><span data-stu-id="45c4a-204">PackageId</span></span>
- <span data-ttu-id="45c4a-205">Yazarlar</span><span class="sxs-lookup"><span data-stu-id="45c4a-205">Authors</span></span>
- <span data-ttu-id="45c4a-206">Açıklama</span><span class="sxs-lookup"><span data-stu-id="45c4a-206">Description</span></span>
- <span data-ttu-id="45c4a-207">Telif Hakkı</span><span class="sxs-lookup"><span data-stu-id="45c4a-207">Copyright</span></span>
- <span data-ttu-id="45c4a-208">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="45c4a-208">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="45c4a-209">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="45c4a-209">DevelopmentDependency</span></span>
- <span data-ttu-id="45c4a-210">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="45c4a-210">PackageLicenseUrl</span></span>
- <span data-ttu-id="45c4a-211">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="45c4a-211">PackageProjectUrl</span></span>
- <span data-ttu-id="45c4a-212">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="45c4a-212">PackageIconUrl</span></span>
- <span data-ttu-id="45c4a-213">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="45c4a-213">PackageReleaseNotes</span></span>
- <span data-ttu-id="45c4a-214">PackageTags</span><span class="sxs-lookup"><span data-stu-id="45c4a-214">PackageTags</span></span>
- <span data-ttu-id="45c4a-215">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="45c4a-215">PackageOutputPath</span></span>
- <span data-ttu-id="45c4a-216">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="45c4a-216">IncludeSymbols</span></span>
- <span data-ttu-id="45c4a-217">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="45c4a-217">IncludeSource</span></span>
- <span data-ttu-id="45c4a-218">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="45c4a-218">PackageTypes</span></span>
- <span data-ttu-id="45c4a-219">IsTool</span><span class="sxs-lookup"><span data-stu-id="45c4a-219">IsTool</span></span>
- <span data-ttu-id="45c4a-220">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="45c4a-220">RepositoryUrl</span></span>
- <span data-ttu-id="45c4a-221">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="45c4a-221">RepositoryType</span></span>
- <span data-ttu-id="45c4a-222">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="45c4a-222">RepositoryBranch</span></span>
- <span data-ttu-id="45c4a-223">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="45c4a-223">RepositoryCommit</span></span>
- <span data-ttu-id="45c4a-224">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="45c4a-224">NoPackageAnalysis</span></span>
- <span data-ttu-id="45c4a-225">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="45c4a-225">MinClientVersion</span></span>
- <span data-ttu-id="45c4a-226">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="45c4a-226">IncludeBuildOutput</span></span>
- <span data-ttu-id="45c4a-227">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="45c4a-227">IncludeContentInPack</span></span>
- <span data-ttu-id="45c4a-228">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="45c4a-228">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="45c4a-229">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="45c4a-229">ContentTargetFolders</span></span>
- <span data-ttu-id="45c4a-230">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="45c4a-230">NuspecFile</span></span>
- <span data-ttu-id="45c4a-231">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="45c4a-231">NuspecBasePath</span></span>
- <span data-ttu-id="45c4a-232">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="45c4a-232">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="45c4a-233">Paketi senaryoları</span><span class="sxs-lookup"><span data-stu-id="45c4a-233">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="45c4a-234">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="45c4a-234">PackageIconUrl</span></span>

<span data-ttu-id="45c4a-235">Değişikliğin parçası olarak [NuGet sorunu 2582](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` sonunda değiştirilecek `PackageIconUri` ve sonuçta elde edilen paketin kökünde bulunan bir simge dosyası için göreli bir yol olabilir.</span><span class="sxs-lookup"><span data-stu-id="45c4a-235">As part of the change for [NuGet Issue 2582](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="45c4a-236">Çıktı derlemeler</span><span class="sxs-lookup"><span data-stu-id="45c4a-236">Output assemblies</span></span>

<span data-ttu-id="45c4a-237">`nuget pack` kopya çıktı uzantılara sahip dosyaları `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, ve `.pri`.</span><span class="sxs-lookup"><span data-stu-id="45c4a-237">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="45c4a-238">MSBuild gelen sağladıkları üzerinde kopyalanır ve çıkış dosyalarının bağımlı `BuiltOutputProjectGroup` hedef.</span><span class="sxs-lookup"><span data-stu-id="45c4a-238">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="45c4a-239">Çıkış derlemelerinin nereye proje dosyası veya komut satırı denetlemek için kullanabileceğiniz iki MSBuild özellikleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="45c4a-239">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="45c4a-240">`IncludeBuildOutput`: Derleme çıktı derlemelerinin pakete dahil edilip edilmeyeceğini belirler bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="45c4a-240">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="45c4a-241">`BuildOutputTargetFolder`: Çıktı derlemelerinin yerleştirilmelidir klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="45c4a-241">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="45c4a-242">Çıktı derlemelerinin (ve diğer çıktı dosyaları) ilgili framework klasörlerine kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="45c4a-242">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="45c4a-243">Paket referanslarını</span><span class="sxs-lookup"><span data-stu-id="45c4a-243">Package references</span></span>

<span data-ttu-id="45c4a-244">Bkz: [paketini proje dosyalarını başvurularında](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="45c4a-244">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="45c4a-245">Proje başvuruları projeye</span><span class="sxs-lookup"><span data-stu-id="45c4a-245">Project to project references</span></span>

<span data-ttu-id="45c4a-246">Proje başvuruları projeye değerlendirilir varsayılan olarak nuget paket referanslarını, örneğin:</span><span class="sxs-lookup"><span data-stu-id="45c4a-246">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="45c4a-247">Ayrıca, aşağıdaki meta verileri, proje başvurusu ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="45c4a-247">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="45c4a-248">Bir paketteki içerik dahil olmak üzere</span><span class="sxs-lookup"><span data-stu-id="45c4a-248">Including content in a package</span></span>

<span data-ttu-id="45c4a-249">İçerik eklemek için fazladan meta verileri, mevcut eklemek `<Content>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="45c4a-249">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="45c4a-250">Varsayılan olarak girişlerle geçersiz kılma sürece "İçerik" paketinde türünde her şeyi ister aşağıdakiler:</span><span class="sxs-lookup"><span data-stu-id="45c4a-250">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
    <Content Include="..\win7-x64\libuv.txt">
        <Pack>false</Pack>
    </Content>
 ```

<span data-ttu-id="45c4a-251">Varsayılan olarak, her şeyi köküne eklenen `content` ve `contentFiles\any\<target_framework>` bir paket ve korur klasördeki göreli klasör yapısı, bir paket yolu belirtmediğiniz sürece:</span><span class="sxs-lookup"><span data-stu-id="45c4a-251">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="45c4a-252">Yalnızca belirli bir tüm içeriğinizi kopyalamak isterseniz klasörlerde kök (yerine `content` ve `contentFiles` her ikisi de), MSBuild özelliği kullanabilirsiniz `ContentTargetFolders`, varsayılan olarak "içerik; Content dosyaları" ancak başka bir klasör adı için ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="45c4a-252">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="45c4a-253">Not "Content dosyaları" belirterek, yalnızca `ContentTargetFolders` altında dosyaları koyan `contentFiles\any\<target_framework>` veya `contentFiles\<language>\<target_framework>` göre `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="45c4a-253">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="45c4a-254">`PackagePath` hedef yolları noktalı virgülle ayrılmış bir kümesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="45c4a-254">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="45c4a-255">Bir boş paket yolu belirterek dosya paket köküne ekleyin.</span><span class="sxs-lookup"><span data-stu-id="45c4a-255">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="45c4a-256">Örneğin, aşağıdaki ekler `libuv.txt` için `content\myfiles`, `content\samples`ve paket kök:</span><span class="sxs-lookup"><span data-stu-id="45c4a-256">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="45c4a-257">Ayrıca bir MSBuild özelliği olan `$(IncludeContentInPack)`, varsayılan olarak `true`.</span><span class="sxs-lookup"><span data-stu-id="45c4a-257">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="45c4a-258">Bu ayarlanırsa `false` hiçbir projede sonra proje içerikten eklenmemiştir nuget paketi.</span><span class="sxs-lookup"><span data-stu-id="45c4a-258">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="45c4a-259">Yukarıdaki öğelerin hiçbirinde ayarlayabilirsiniz diğer paketi belirli meta verileri içeren ```<PackageCopyToOutput>``` ve ```<PackageFlatten>``` hangi kümeleri ```CopyToOutput``` ve ```Flatten``` üzerinde değerleri ```contentFiles``` çıkış nuspec girişi.</span><span class="sxs-lookup"><span data-stu-id="45c4a-259">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="45c4a-260">İçerik öğeleri dışında `<Pack>` ve `<PackagePath>` meta verileri de ayarlanabilir derleme, EmbeddedResource, ApplicationDefinition, sayfa, kaynak, KarşılamaEkranı, DesignData, DesignDataWithDesignTimeCreateableTypes yapı eylemiyle dosyalarda , CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource veya yok.</span><span class="sxs-lookup"><span data-stu-id="45c4a-260">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="45c4a-261">Dosya adı, paket yolu genelleme desenleri kullanırken eklenecek paketi için paket yolu paket yoluyla dosya adını içeren tam yol kabul edilir klasör ayırıcı karakter, aksi takdirde ile bitmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="45c4a-261">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="45c4a-262">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="45c4a-262">IncludeSymbols</span></span>

<span data-ttu-id="45c4a-263">Kullanırken `MSBuild /t:pack /p:IncludeSymbols=true`, karşılık gelen `.pdb` dosyaları, diğer çıkış dosyalarının yanı sıra kopyalanır (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="45c4a-263">When using `MSBuild /t:pack /p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="45c4a-264">Bu ayarı Not `IncludeSymbols=true` normal bir paket oluşturur *ve* simge paketi.</span><span class="sxs-lookup"><span data-stu-id="45c4a-264">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="45c4a-265">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="45c4a-265">IncludeSource</span></span>

<span data-ttu-id="45c4a-266">Bu aynı sonucu verir `IncludeSymbols`ile birlikte kaynak dosyalarını kopyalar dışında `.pdb` da dosyaları.</span><span class="sxs-lookup"><span data-stu-id="45c4a-266">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="45c4a-267">Tüm dosya türlerini `Compile` üzerinden kopyalanır `src\<ProjectName>\` elde edilen paketindeki göreli yol klasör yapısı korunarak.</span><span class="sxs-lookup"><span data-stu-id="45c4a-267">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="45c4a-268">Aynı kaynak dosyaları herhangi da yapılır `ProjectReference` olan `TreatAsPackageReference` kümesine `false`.</span><span class="sxs-lookup"><span data-stu-id="45c4a-268">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="45c4a-269">Dosya türü derlemek için yeni eklenen sonra proje klasörünün dışında varsa, `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="45c4a-269">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="istool"></a><span data-ttu-id="45c4a-270">IsTool</span><span class="sxs-lookup"><span data-stu-id="45c4a-270">IsTool</span></span>

<span data-ttu-id="45c4a-271">Kullanırken `MSBuild /t:pack /p:IsTool=true`, tüm dosyaları belirtilen çıktı [çıkış derlemelerinin](#output-assemblies) senaryosu, kopyalanır `tools` klasörü yerine `lib` klasör.</span><span class="sxs-lookup"><span data-stu-id="45c4a-271">When using `MSBuild /t:pack /p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="45c4a-272">Bu farklı olduğuna dikkat edin bir `DotNetCliTool` , belirtilen ayarlayarak `PackageType` içinde `.csproj` dosya.</span><span class="sxs-lookup"><span data-stu-id="45c4a-272">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="45c4a-273">Bir .nuspec kullanarak paketleme</span><span class="sxs-lookup"><span data-stu-id="45c4a-273">Packing using a .nuspec</span></span>

<span data-ttu-id="45c4a-274">Kullanabileceğiniz bir `.nuspec` içeri aktarmak için bir proje dosyasına sahip olması koşuluyla, projenizin paketi dosyaya `NuGet.Build.Tasks.Pack.targets` böylece paketi görevi çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="45c4a-274">You can use a `.nuspec` file to pack your project provided that you have a project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="45c4a-275">Aşağıdaki üç MSBuild özellikleri kullanarak paket için uygun olan bir `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="45c4a-275">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="45c4a-276">`NuspecFile`: göreli veya mutlak bir yol `.nuspec` paketleme için kullanılan dosya.</span><span class="sxs-lookup"><span data-stu-id="45c4a-276">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="45c4a-277">`NuspecProperties`: noktalı virgülle ayrılmış listesini anahtar = değer çiftleri.</span><span class="sxs-lookup"><span data-stu-id="45c4a-277">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="45c4a-278">MSBuild komut satırı ayrıştırma works yöntemi nedeniyle birden çok özellikleri şu şekilde belirtilmelidir: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="45c4a-278">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="45c4a-279">`NuspecBasePath`: Temel yolu `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="45c4a-279">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="45c4a-280">Kullanıyorsanız `dotnet.exe` projenizi paketi için bir komut aşağıdaki gibi kullanın:</span><span class="sxs-lookup"><span data-stu-id="45c4a-280">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="45c4a-281">MSBuild projenizi Paketi kullanıyorsanız, aşağıdaki gibi bir komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="45c4a-281">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

## <a name="restore-target"></a><span data-ttu-id="45c4a-282">geri yükleme hedefi</span><span class="sxs-lookup"><span data-stu-id="45c4a-282">restore target</span></span>

<span data-ttu-id="45c4a-283">`MSBuild /t:restore` (hangi `nuget restore` ve `dotnet restore` .NET Core projeleriyle kullanmak), proje dosyasında aşağıdaki gibi başvurduğu paketleri yükler:</span><span class="sxs-lookup"><span data-stu-id="45c4a-283">`MSBuild /t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="45c4a-284">Tüm proje için proje başvuruları okuma</span><span class="sxs-lookup"><span data-stu-id="45c4a-284">Read all project to project references</span></span>
1. <span data-ttu-id="45c4a-285">Ara klasörü ve hedef çerçeveleri bulmak için proje özelliklerini okuma</span><span class="sxs-lookup"><span data-stu-id="45c4a-285">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="45c4a-286">Msbuild veri NuGet.Build.Tasks.dll geçirmek</span><span class="sxs-lookup"><span data-stu-id="45c4a-286">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="45c4a-287">Geri yükleme çalıştırma</span><span class="sxs-lookup"><span data-stu-id="45c4a-287">Run restore</span></span>
1. <span data-ttu-id="45c4a-288">Paketleri indirin</span><span class="sxs-lookup"><span data-stu-id="45c4a-288">Download packages</span></span>
1. <span data-ttu-id="45c4a-289">Varlıklar dosya, hedefleri ve özellik yazma</span><span class="sxs-lookup"><span data-stu-id="45c4a-289">Write assets file, targets, and props</span></span>

> [!Note]
> <span data-ttu-id="45c4a-290">`restore` MSBuild hedef yalnızca kullanarak projeleri için çalışır `PackageReference` öğeleri ve paketleri kullanarak başvurulan geri yüklemez bir `packages.config` dosyası.</span><span class="sxs-lookup"><span data-stu-id="45c4a-290">The `restore` MSBuild target only works for projects using `PackageReference` items and does not restore packages referenced using a `packages.config` file.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="45c4a-291">Özellikler geri yükleme</span><span class="sxs-lookup"><span data-stu-id="45c4a-291">Restore properties</span></span>

<span data-ttu-id="45c4a-292">Ek geri yükleme ayarlarını MSBuild proje dosyası özelliklerinde alınması.</span><span class="sxs-lookup"><span data-stu-id="45c4a-292">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="45c4a-293">Değerleri de ayarlanabilir kullanarak komut satırından `/p:` geçiş (aşağıdaki örneklere bakın).</span><span class="sxs-lookup"><span data-stu-id="45c4a-293">Values can also be set from the command line using the `/p:` switch (see Examples below).</span></span>

| <span data-ttu-id="45c4a-294">Özellik</span><span class="sxs-lookup"><span data-stu-id="45c4a-294">Property</span></span> | <span data-ttu-id="45c4a-295">Açıklama</span><span class="sxs-lookup"><span data-stu-id="45c4a-295">Description</span></span> |
|--------|--------|
| <span data-ttu-id="45c4a-296">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="45c4a-296">RestoreSources</span></span> | <span data-ttu-id="45c4a-297">Paket kaynaklarını noktalı virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="45c4a-297">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="45c4a-298">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="45c4a-298">RestorePackagesPath</span></span> | <span data-ttu-id="45c4a-299">Kullanıcı paketleri klasör yolu.</span><span class="sxs-lookup"><span data-stu-id="45c4a-299">User packages folder path.</span></span> |
| <span data-ttu-id="45c4a-300">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="45c4a-300">RestoreDisableParallel</span></span> | <span data-ttu-id="45c4a-301">Bir seferde bir sınır indirir.</span><span class="sxs-lookup"><span data-stu-id="45c4a-301">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="45c4a-302">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="45c4a-302">RestoreConfigFile</span></span> | <span data-ttu-id="45c4a-303">Yol için bir `Nuget.Config` uygulamak için dosya.</span><span class="sxs-lookup"><span data-stu-id="45c4a-303">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="45c4a-304">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="45c4a-304">RestoreNoCache</span></span> | <span data-ttu-id="45c4a-305">TRUE ise, web önbelleği kullanılarak önler.</span><span class="sxs-lookup"><span data-stu-id="45c4a-305">If true, avoids using the web cache.</span></span> |
| <span data-ttu-id="45c4a-306">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="45c4a-306">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="45c4a-307">TRUE ise, başarısız olan veya eksik paket kaynaklarını yok sayar.</span><span class="sxs-lookup"><span data-stu-id="45c4a-307">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="45c4a-308">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="45c4a-308">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="45c4a-309">Yolu `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="45c4a-309">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="45c4a-310">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="45c4a-310">RestoreGraphProjectInput</span></span> | <span data-ttu-id="45c4a-311">Mutlak yollar içermesi gereken geri yüklemek için projeleri noktalı virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="45c4a-311">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="45c4a-312">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="45c4a-312">RestoreOutputPath</span></span> | <span data-ttu-id="45c4a-313">Çıkış klasörüne varsayarak, `obj` klasörü.</span><span class="sxs-lookup"><span data-stu-id="45c4a-313">Output folder, defaulting to the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="45c4a-314">Örnekler</span><span class="sxs-lookup"><span data-stu-id="45c4a-314">Examples</span></span>

<span data-ttu-id="45c4a-315">Komut satırı:</span><span class="sxs-lookup"><span data-stu-id="45c4a-315">Command line:</span></span>

```cli
msbuild /t:restore /p:RestoreConfigFile=<path>
```

<span data-ttu-id="45c4a-316">Proje dosyası:</span><span class="sxs-lookup"><span data-stu-id="45c4a-316">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
<PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="45c4a-317">Çıkış geri yükleme</span><span class="sxs-lookup"><span data-stu-id="45c4a-317">Restore outputs</span></span>

<span data-ttu-id="45c4a-318">Geri yükleme yapı aşağıdaki dosyaları oluşturur `obj` klasörü:</span><span class="sxs-lookup"><span data-stu-id="45c4a-318">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="45c4a-319">Dosya</span><span class="sxs-lookup"><span data-stu-id="45c4a-319">File</span></span> | <span data-ttu-id="45c4a-320">Açıklama</span><span class="sxs-lookup"><span data-stu-id="45c4a-320">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="45c4a-321">Daha önce `project.lock.json`</span><span class="sxs-lookup"><span data-stu-id="45c4a-321">Previously `project.lock.json`</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="45c4a-322">MSBuild özellik paketlerinde bulunan başvurular</span><span class="sxs-lookup"><span data-stu-id="45c4a-322">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="45c4a-323">MSBuild hedefleri paketlerinde bulunan başvurular</span><span class="sxs-lookup"><span data-stu-id="45c4a-323">References to MSBuild targets contained in packages</span></span> |

### <a name="packagetargetfallback"></a><span data-ttu-id="45c4a-324">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="45c4a-324">PackageTargetFallback</span></span>

<span data-ttu-id="45c4a-325">`PackageTargetFallback` Öğesi paketleri geri yüklenirken kullanılacak uyumlu hedefleri kümesi belirtmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="45c4a-325">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="45c4a-326">Bir dotnet kullanmak paketleri izin vermek için tasarlanmış [TxM](../reference/target-frameworks.md) dotnet TxM bildirmeyin uyumlu paketlerle çalışmak için.</span><span class="sxs-lookup"><span data-stu-id="45c4a-326">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="45c4a-327">Projeniz TxM dotnet kullanıyorsa, eklediğiniz sürece diğer bir deyişle, daha sonra bağlı olduğu gereken üzerinde de tüm paketler dotnet TxM, olması `<PackageTargetFallback>` dotnet ile uyumlu olacak şekilde dotnet olmayan platformları izin vermek üzere projenize.</span><span class="sxs-lookup"><span data-stu-id="45c4a-327">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="45c4a-328">Proje kullanıyorsa, örneğin, `netstandard1.6` TxM ve bağımlı paketi içeren yalnızca `lib/net45/a.dll` ve `lib/portable-net45+win81/a.dll`, projeyi oluşturmak başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="45c4a-328">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="45c4a-329">Getirileceğini istediğiniz ikinci DLL'dir sonra ekleyebileceğiniz bir `PackageTargetFallback` gibi söylemek için `portable-net45+win81` DLL uyumludur:</span><span class="sxs-lookup"><span data-stu-id="45c4a-329">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="45c4a-330">Projenizdeki tüm hedefler için bir geri dönüş bildirmek için devre dışı bırakın `Condition` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="45c4a-330">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="45c4a-331">Var olan genişletebilirsiniz `PackageTargetFallback` ekleyerek `$(PackageTargetFallback)` aşağıda gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="45c4a-331">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="45c4a-332">Bir geri yükleme grafik bir kitaplıktan değiştirme</span><span class="sxs-lookup"><span data-stu-id="45c4a-332">Replacing one library from a restore graph</span></span>

<span data-ttu-id="45c4a-333">Bir geri yükleme yanlış derleme getiren, paketleri seçim varsayılan ve kendi seçimi ile değiştir dışlamak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="45c4a-333">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="45c4a-334">Üst düzey ile ilk `PackageReference`, tüm varlıklar çıkar:</span><span class="sxs-lookup"><span data-stu-id="45c4a-334">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
    <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="45c4a-335">Ardından, DLL uygun yerel kopyasını kendi başvuru ekleyin:</span><span class="sxs-lookup"><span data-stu-id="45c4a-335">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
