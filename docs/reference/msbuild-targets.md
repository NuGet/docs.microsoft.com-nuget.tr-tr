---
title: NuGet paketi ve MSBuild hedefleri olarak geri yükleme
description: NuGet paketi ve geri yükleme, doğrudan NuGet 4.0 + ile MSBuild hedefleri olarak çalışabilir.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 73885256c5d5ea67140051bf63ff470991978928
ms.sourcegitcommit: 055248d790051774c892b220eca12015babbd668
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/14/2018
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="b088d-103">NuGet paketi ve MSBuild hedefleri olarak geri yükleme</span><span class="sxs-lookup"><span data-stu-id="b088d-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="b088d-104">*NuGet 4.0 +*</span><span class="sxs-lookup"><span data-stu-id="b088d-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="b088d-105">PackageReference biçimiyle NuGet 4.0 + doğrudan ayrı bir kullanmak yerine bir proje dosyası içinde tüm bildirim meta veri depolayabilirsiniz `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="b088d-105">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="b088d-106">MSBuild ile 15.1 +, NuGet birinci sınıf MSBuild vatandaşı ile aynı zamanda olan `pack` ve `restore` aşağıda açıklandığı gibi hedefler.</span><span class="sxs-lookup"><span data-stu-id="b088d-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="b088d-107">Bu hedeflerde, diğer MSBuild görev veya hedef ile olduğu gibi NuGet ile çalışmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="b088d-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="b088d-108">(NuGet için 3.x ve daha önce kullandığınız [paketi](../tools/cli-ref-pack.md) ve [geri](../tools/cli-ref-restore.md) NuGet CLI aracılığıyla yerine komutları.)</span><span class="sxs-lookup"><span data-stu-id="b088d-108">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="b088d-109">Hedef derleme sırası</span><span class="sxs-lookup"><span data-stu-id="b088d-109">Target build order</span></span>

<span data-ttu-id="b088d-110">Olduğundan `pack` ve `restore` MSBuild hedefleri şunlardır akışınızı artırmak için bunları erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b088d-110">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="b088d-111">Örneğin, paket sonra bir ağ paylaşımına paketinizi kopyalamak istediğiniz varsayalım.</span><span class="sxs-lookup"><span data-stu-id="b088d-111">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="b088d-112">Bunu, proje dosyasında aşağıdaki ekleyerek yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b088d-112">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="b088d-113">Benzer şekilde, bir MSBuild görev yazabileceğiniz, kendi hedef yazma ve MSBuild görevi NuGet özelliklerinde kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="b088d-113">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="b088d-114">paketi hedef</span><span class="sxs-lookup"><span data-stu-id="b088d-114">pack target</span></span>

<span data-ttu-id="b088d-115">PackageReference biçimini kullanarak, kullanarak .NET standart projeleri için `msbuild /t:pack` bir NuGet paketi oluşturmak için proje dosyasından girişleri çizer.</span><span class="sxs-lookup"><span data-stu-id="b088d-115">For .NET Standard projects using the PackageReference format, using `msbuild /t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="b088d-116">Proje dosyası içinde ilk eklenebilir MSBuild özellikler aşağıdaki tabloda açıklanmıştır `<PropertyGroup>` düğümü.</span><span class="sxs-lookup"><span data-stu-id="b088d-116">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="b088d-117">Bu düzenlemeler kolayca Visual Studio 2017 ve daha sonra projeye sağ tıklayıp seçerek yapabileceğiniz **{project_name} Düzenle** bağlam menüsünde.</span><span class="sxs-lookup"><span data-stu-id="b088d-117">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="b088d-118">Kolaylık olması için tablo eşdeğer özelliği tarafından düzenlenir bir [ `.nuspec` dosya](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="b088d-118">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="b088d-119">Unutmayın `Owners` ve `Summary` özelliklerinden `.nuspec` MSBuild ile desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="b088d-119">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="b088d-120">Öznitelik/NuSpec değeri</span><span class="sxs-lookup"><span data-stu-id="b088d-120">Attribute/NuSpec Value</span></span> | <span data-ttu-id="b088d-121">MSBuild özelliği</span><span class="sxs-lookup"><span data-stu-id="b088d-121">MSBuild Property</span></span> | <span data-ttu-id="b088d-122">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="b088d-122">Default</span></span> | <span data-ttu-id="b088d-123">Notlar</span><span class="sxs-lookup"><span data-stu-id="b088d-123">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="b088d-124">Kimliği</span><span class="sxs-lookup"><span data-stu-id="b088d-124">Id</span></span> | <span data-ttu-id="b088d-125">Paket kimliği</span><span class="sxs-lookup"><span data-stu-id="b088d-125">PackageId</span></span> | <span data-ttu-id="b088d-126">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="b088d-126">AssemblyName</span></span> | <span data-ttu-id="b088d-127">MSBuild gelen $(AssemblyName)</span><span class="sxs-lookup"><span data-stu-id="b088d-127">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="b088d-128">Sürüm</span><span class="sxs-lookup"><span data-stu-id="b088d-128">Version</span></span> | <span data-ttu-id="b088d-129">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="b088d-129">PackageVersion</span></span> | <span data-ttu-id="b088d-130">Sürüm</span><span class="sxs-lookup"><span data-stu-id="b088d-130">Version</span></span> | <span data-ttu-id="b088d-131">Bu semver örnek "1.0.0", "1.0.0-beta" veya "1.0.0-beta-00345" için uyumlu değil</span><span class="sxs-lookup"><span data-stu-id="b088d-131">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="b088d-132">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="b088d-132">VersionPrefix</span></span> | <span data-ttu-id="b088d-133">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="b088d-133">PackageVersionPrefix</span></span> | <span data-ttu-id="b088d-134">empty</span><span class="sxs-lookup"><span data-stu-id="b088d-134">empty</span></span> | <span data-ttu-id="b088d-135">PackageVersionPrefix PackageVersion ayarını geçersiz kılar</span><span class="sxs-lookup"><span data-stu-id="b088d-135">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="b088d-136">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="b088d-136">VersionSuffix</span></span> | <span data-ttu-id="b088d-137">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="b088d-137">PackageVersionSuffix</span></span> | <span data-ttu-id="b088d-138">empty</span><span class="sxs-lookup"><span data-stu-id="b088d-138">empty</span></span> | <span data-ttu-id="b088d-139">MSBuild gelen $(VersionSuffix).</span><span class="sxs-lookup"><span data-stu-id="b088d-139">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="b088d-140">PackageVersionSuffix PackageVersion ayarını geçersiz kılar</span><span class="sxs-lookup"><span data-stu-id="b088d-140">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="b088d-141">Yazarlar</span><span class="sxs-lookup"><span data-stu-id="b088d-141">Authors</span></span> | <span data-ttu-id="b088d-142">Yazarlar</span><span class="sxs-lookup"><span data-stu-id="b088d-142">Authors</span></span> | <span data-ttu-id="b088d-143">Geçerli kullanıcının kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="b088d-143">Username of the current user</span></span> | |
| <span data-ttu-id="b088d-144">Sahipleri</span><span class="sxs-lookup"><span data-stu-id="b088d-144">Owners</span></span> | <span data-ttu-id="b088d-145">Yok</span><span class="sxs-lookup"><span data-stu-id="b088d-145">N/A</span></span> | <span data-ttu-id="b088d-146">NuSpec içinde mevcut olmayan</span><span class="sxs-lookup"><span data-stu-id="b088d-146">Not present in NuSpec</span></span> | |
| <span data-ttu-id="b088d-147">Başlık</span><span class="sxs-lookup"><span data-stu-id="b088d-147">Title</span></span> | <span data-ttu-id="b088d-148">Başlık</span><span class="sxs-lookup"><span data-stu-id="b088d-148">Title</span></span> | <span data-ttu-id="b088d-149">Paket kimliği</span><span class="sxs-lookup"><span data-stu-id="b088d-149">The PackageId</span></span>| |
| <span data-ttu-id="b088d-150">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b088d-150">Description</span></span> | <span data-ttu-id="b088d-151">PackageDescription</span><span class="sxs-lookup"><span data-stu-id="b088d-151">PackageDescription</span></span> | <span data-ttu-id="b088d-152">"Paketi"</span><span class="sxs-lookup"><span data-stu-id="b088d-152">"Package Description"</span></span> | |
| <span data-ttu-id="b088d-153">Telif Hakkı</span><span class="sxs-lookup"><span data-stu-id="b088d-153">Copyright</span></span> | <span data-ttu-id="b088d-154">Telif Hakkı</span><span class="sxs-lookup"><span data-stu-id="b088d-154">Copyright</span></span> | <span data-ttu-id="b088d-155">empty</span><span class="sxs-lookup"><span data-stu-id="b088d-155">empty</span></span> | |
| <span data-ttu-id="b088d-156">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="b088d-156">RequireLicenseAcceptance</span></span> | <span data-ttu-id="b088d-157">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="b088d-157">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="b088d-158">false</span><span class="sxs-lookup"><span data-stu-id="b088d-158">false</span></span> | |
| <span data-ttu-id="b088d-159">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="b088d-159">LicenseUrl</span></span> | <span data-ttu-id="b088d-160">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="b088d-160">PackageLicenseUrl</span></span> | <span data-ttu-id="b088d-161">empty</span><span class="sxs-lookup"><span data-stu-id="b088d-161">empty</span></span> | |
| <span data-ttu-id="b088d-162">projectUrl</span><span class="sxs-lookup"><span data-stu-id="b088d-162">ProjectUrl</span></span> | <span data-ttu-id="b088d-163">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="b088d-163">PackageProjectUrl</span></span> | <span data-ttu-id="b088d-164">empty</span><span class="sxs-lookup"><span data-stu-id="b088d-164">empty</span></span> | |
| <span data-ttu-id="b088d-165">iconUrl</span><span class="sxs-lookup"><span data-stu-id="b088d-165">IconUrl</span></span> | <span data-ttu-id="b088d-166">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="b088d-166">PackageIconUrl</span></span> | <span data-ttu-id="b088d-167">empty</span><span class="sxs-lookup"><span data-stu-id="b088d-167">empty</span></span> | |
| <span data-ttu-id="b088d-168">Etiketler</span><span class="sxs-lookup"><span data-stu-id="b088d-168">Tags</span></span> | <span data-ttu-id="b088d-169">PackageTags</span><span class="sxs-lookup"><span data-stu-id="b088d-169">PackageTags</span></span> | <span data-ttu-id="b088d-170">empty</span><span class="sxs-lookup"><span data-stu-id="b088d-170">empty</span></span> | <span data-ttu-id="b088d-171">Etiketleri noktalı virgülle ayrılmış olan.</span><span class="sxs-lookup"><span data-stu-id="b088d-171">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="b088d-172">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="b088d-172">ReleaseNotes</span></span> | <span data-ttu-id="b088d-173">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="b088d-173">PackageReleaseNotes</span></span> | <span data-ttu-id="b088d-174">empty</span><span class="sxs-lookup"><span data-stu-id="b088d-174">empty</span></span> | |
| <span data-ttu-id="b088d-175">Depo/URL'si</span><span class="sxs-lookup"><span data-stu-id="b088d-175">Repository/Url</span></span> | <span data-ttu-id="b088d-176">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="b088d-176">RepositoryUrl</span></span> | <span data-ttu-id="b088d-177">empty</span><span class="sxs-lookup"><span data-stu-id="b088d-177">empty</span></span> | <span data-ttu-id="b088d-178">Depo URL'si kopyalama veya kaynak kodu almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b088d-178">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="b088d-179">Örnek: *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="b088d-179">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="b088d-180">Depo/türü</span><span class="sxs-lookup"><span data-stu-id="b088d-180">Repository/Type</span></span> | <span data-ttu-id="b088d-181">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="b088d-181">RepositoryType</span></span> | <span data-ttu-id="b088d-182">empty</span><span class="sxs-lookup"><span data-stu-id="b088d-182">empty</span></span> | <span data-ttu-id="b088d-183">Depo türü.</span><span class="sxs-lookup"><span data-stu-id="b088d-183">Repository type.</span></span> <span data-ttu-id="b088d-184">Örnekler: *git*, *tfs*.</span><span class="sxs-lookup"><span data-stu-id="b088d-184">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="b088d-185">Depo/şube</span><span class="sxs-lookup"><span data-stu-id="b088d-185">Repository/Branch</span></span> | <span data-ttu-id="b088d-186">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="b088d-186">RepositoryBranch</span></span> | <span data-ttu-id="b088d-187">empty</span><span class="sxs-lookup"><span data-stu-id="b088d-187">empty</span></span> | <span data-ttu-id="b088d-188">İsteğe bağlı depo şube bilgileri.</span><span class="sxs-lookup"><span data-stu-id="b088d-188">Optional repository branch information.</span></span> <span data-ttu-id="b088d-189">*RepositoryUrl* dahil edilmek üzere bu özellik için de belirtilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="b088d-189">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="b088d-190">Örnek: *ana* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="b088d-190">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="b088d-191">Depo/tamamlama</span><span class="sxs-lookup"><span data-stu-id="b088d-191">Repository/Commit</span></span> | <span data-ttu-id="b088d-192">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="b088d-192">RepositoryCommit</span></span> | <span data-ttu-id="b088d-193">empty</span><span class="sxs-lookup"><span data-stu-id="b088d-193">empty</span></span> | <span data-ttu-id="b088d-194">İsteğe bağlı depo yürütme veya, paket kaynak belirtmek için değişiklik karşı oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="b088d-194">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="b088d-195">*RepositoryUrl* dahil edilmek üzere bu özellik için de belirtilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="b088d-195">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="b088d-196">Örnek: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="b088d-196">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="b088d-197">PackageType</span><span class="sxs-lookup"><span data-stu-id="b088d-197">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="b088d-198">Özet</span><span class="sxs-lookup"><span data-stu-id="b088d-198">Summary</span></span> | <span data-ttu-id="b088d-199">Desteklenmez</span><span class="sxs-lookup"><span data-stu-id="b088d-199">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="b088d-200">paketi hedef girişleri</span><span class="sxs-lookup"><span data-stu-id="b088d-200">pack target inputs</span></span>

- <span data-ttu-id="b088d-201">IsPackable</span><span class="sxs-lookup"><span data-stu-id="b088d-201">IsPackable</span></span>
- <span data-ttu-id="b088d-202">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="b088d-202">PackageVersion</span></span>
- <span data-ttu-id="b088d-203">Paket kimliği</span><span class="sxs-lookup"><span data-stu-id="b088d-203">PackageId</span></span>
- <span data-ttu-id="b088d-204">Yazarlar</span><span class="sxs-lookup"><span data-stu-id="b088d-204">Authors</span></span>
- <span data-ttu-id="b088d-205">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b088d-205">Description</span></span>
- <span data-ttu-id="b088d-206">Telif Hakkı</span><span class="sxs-lookup"><span data-stu-id="b088d-206">Copyright</span></span>
- <span data-ttu-id="b088d-207">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="b088d-207">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="b088d-208">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="b088d-208">DevelopmentDependency</span></span>
- <span data-ttu-id="b088d-209">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="b088d-209">PackageLicenseUrl</span></span>
- <span data-ttu-id="b088d-210">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="b088d-210">PackageProjectUrl</span></span>
- <span data-ttu-id="b088d-211">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="b088d-211">PackageIconUrl</span></span>
- <span data-ttu-id="b088d-212">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="b088d-212">PackageReleaseNotes</span></span>
- <span data-ttu-id="b088d-213">PackageTags</span><span class="sxs-lookup"><span data-stu-id="b088d-213">PackageTags</span></span>
- <span data-ttu-id="b088d-214">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="b088d-214">PackageOutputPath</span></span>
- <span data-ttu-id="b088d-215">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="b088d-215">IncludeSymbols</span></span>
- <span data-ttu-id="b088d-216">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="b088d-216">IncludeSource</span></span>
- <span data-ttu-id="b088d-217">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="b088d-217">PackageTypes</span></span>
- <span data-ttu-id="b088d-218">IsTool</span><span class="sxs-lookup"><span data-stu-id="b088d-218">IsTool</span></span>
- <span data-ttu-id="b088d-219">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="b088d-219">RepositoryUrl</span></span>
- <span data-ttu-id="b088d-220">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="b088d-220">RepositoryType</span></span>
- <span data-ttu-id="b088d-221">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="b088d-221">RepositoryBranch</span></span>
- <span data-ttu-id="b088d-222">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="b088d-222">RepositoryCommit</span></span>
- <span data-ttu-id="b088d-223">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="b088d-223">NoPackageAnalysis</span></span>
- <span data-ttu-id="b088d-224">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="b088d-224">MinClientVersion</span></span>
- <span data-ttu-id="b088d-225">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="b088d-225">IncludeBuildOutput</span></span>
- <span data-ttu-id="b088d-226">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="b088d-226">IncludeContentInPack</span></span>
- <span data-ttu-id="b088d-227">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="b088d-227">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="b088d-228">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="b088d-228">ContentTargetFolders</span></span>
- <span data-ttu-id="b088d-229">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="b088d-229">NuspecFile</span></span>
- <span data-ttu-id="b088d-230">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="b088d-230">NuspecBasePath</span></span>
- <span data-ttu-id="b088d-231">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="b088d-231">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="b088d-232">Paketi senaryoları</span><span class="sxs-lookup"><span data-stu-id="b088d-232">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="b088d-233">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="b088d-233">PackageIconUrl</span></span>

<span data-ttu-id="b088d-234">Değişikliğin parçası olarak [NuGet sorunu 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` sonunda değiştirilecek `PackageIconUri` ve sonuçta elde edilen paketin kökünde bulunan bir simge dosyası için göreli bir yol olabilir.</span><span class="sxs-lookup"><span data-stu-id="b088d-234">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="b088d-235">Çıktı derlemeler</span><span class="sxs-lookup"><span data-stu-id="b088d-235">Output assemblies</span></span>

<span data-ttu-id="b088d-236">`nuget pack` kopya çıktı uzantılara sahip dosyaları `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, ve `.pri`.</span><span class="sxs-lookup"><span data-stu-id="b088d-236">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="b088d-237">MSBuild gelen sağladıkları üzerinde kopyalanır ve çıkış dosyalarının bağımlı `BuiltOutputProjectGroup` hedef.</span><span class="sxs-lookup"><span data-stu-id="b088d-237">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="b088d-238">Çıkış derlemelerinin nereye proje dosyası veya komut satırı denetlemek için kullanabileceğiniz iki MSBuild özellikleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b088d-238">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="b088d-239">`IncludeBuildOutput`: Derleme çıktı derlemelerinin pakete dahil edilip edilmeyeceğini belirler bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="b088d-239">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="b088d-240">`BuildOutputTargetFolder`: Çıktı derlemelerinin yerleştirilmelidir klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="b088d-240">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="b088d-241">Çıktı derlemelerinin (ve diğer çıktı dosyaları) ilgili framework klasörlerine kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="b088d-241">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="b088d-242">Paket referanslarını</span><span class="sxs-lookup"><span data-stu-id="b088d-242">Package references</span></span>

<span data-ttu-id="b088d-243">Bkz: [paketini proje dosyalarını başvurularında](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="b088d-243">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="b088d-244">Proje başvuruları projeye</span><span class="sxs-lookup"><span data-stu-id="b088d-244">Project to project references</span></span>

<span data-ttu-id="b088d-245">Proje başvuruları projeye değerlendirilir varsayılan olarak nuget paket referanslarını, örneğin:</span><span class="sxs-lookup"><span data-stu-id="b088d-245">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="b088d-246">Ayrıca, aşağıdaki meta verileri, proje başvurusu ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b088d-246">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="b088d-247">Bir paketteki içerik dahil olmak üzere</span><span class="sxs-lookup"><span data-stu-id="b088d-247">Including content in a package</span></span>

<span data-ttu-id="b088d-248">İçerik eklemek için fazladan meta verileri, mevcut eklemek `<Content>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="b088d-248">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="b088d-249">Varsayılan olarak girişlerle geçersiz kılma sürece "İçerik" paketinde türünde her şeyi ister aşağıdakiler:</span><span class="sxs-lookup"><span data-stu-id="b088d-249">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="b088d-250">Varsayılan olarak, her şeyi köküne eklenen `content` ve `contentFiles\any\<target_framework>` bir paket ve korur klasördeki göreli klasör yapısı, bir paket yolu belirtmediğiniz sürece:</span><span class="sxs-lookup"><span data-stu-id="b088d-250">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="b088d-251">Yalnızca belirli bir tüm içeriğinizi kopyalamak isterseniz klasörlerde kök (yerine `content` ve `contentFiles` her ikisi de), MSBuild özelliği kullanabilirsiniz `ContentTargetFolders`, varsayılan olarak "içerik; Content dosyaları" ancak başka bir klasör adı için ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="b088d-251">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="b088d-252">Not "Content dosyaları" belirterek, yalnızca `ContentTargetFolders` altında dosyaları koyan `contentFiles\any\<target_framework>` veya `contentFiles\<language>\<target_framework>` göre `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="b088d-252">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="b088d-253">`PackagePath` hedef yolları noktalı virgülle ayrılmış bir kümesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="b088d-253">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="b088d-254">Bir boş paket yolu belirterek dosya paket köküne ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b088d-254">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="b088d-255">Örneğin, aşağıdaki ekler `libuv.txt` için `content\myfiles`, `content\samples`ve paket kök:</span><span class="sxs-lookup"><span data-stu-id="b088d-255">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="b088d-256">Ayrıca bir MSBuild özelliği olan `$(IncludeContentInPack)`, varsayılan olarak `true`.</span><span class="sxs-lookup"><span data-stu-id="b088d-256">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="b088d-257">Bu ayarlanırsa `false` hiçbir projede sonra proje içerikten eklenmemiştir nuget paketi.</span><span class="sxs-lookup"><span data-stu-id="b088d-257">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="b088d-258">Yukarıdaki öğelerin hiçbirinde ayarlayabilirsiniz diğer paketi belirli meta verileri içeren ```<PackageCopyToOutput>``` ve ```<PackageFlatten>``` hangi kümeleri ```CopyToOutput``` ve ```Flatten``` üzerinde değerleri ```contentFiles``` çıkış nuspec girişi.</span><span class="sxs-lookup"><span data-stu-id="b088d-258">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="b088d-259">İçerik öğeleri dışında `<Pack>` ve `<PackagePath>` meta verileri de ayarlanabilir derleme, EmbeddedResource, ApplicationDefinition, sayfa, kaynak, KarşılamaEkranı, DesignData, DesignDataWithDesignTimeCreateableTypes yapı eylemiyle dosyalarda , CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource veya yok.</span><span class="sxs-lookup"><span data-stu-id="b088d-259">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="b088d-260">Dosya adı, paket yolu genelleme desenleri kullanırken eklenecek paketi için paket yolu paket yoluyla dosya adını içeren tam yol kabul edilir klasör ayırıcı karakter, aksi takdirde ile bitmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="b088d-260">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="b088d-261">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="b088d-261">IncludeSymbols</span></span>

<span data-ttu-id="b088d-262">Kullanırken `MSBuild /t:pack /p:IncludeSymbols=true`, karşılık gelen `.pdb` dosyaları, diğer çıkış dosyalarının yanı sıra kopyalanır (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="b088d-262">When using `MSBuild /t:pack /p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="b088d-263">Bu ayarı Not `IncludeSymbols=true` normal bir paket oluşturur *ve* simge paketi.</span><span class="sxs-lookup"><span data-stu-id="b088d-263">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="b088d-264">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="b088d-264">IncludeSource</span></span>

<span data-ttu-id="b088d-265">Bu aynı sonucu verir `IncludeSymbols`ile birlikte kaynak dosyalarını kopyalar dışında `.pdb` da dosyaları.</span><span class="sxs-lookup"><span data-stu-id="b088d-265">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="b088d-266">Tüm dosya türlerini `Compile` üzerinden kopyalanır `src\<ProjectName>\` elde edilen paketindeki göreli yol klasör yapısı korunarak.</span><span class="sxs-lookup"><span data-stu-id="b088d-266">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="b088d-267">Aynı kaynak dosyaları herhangi da yapılır `ProjectReference` olan `TreatAsPackageReference` kümesine `false`.</span><span class="sxs-lookup"><span data-stu-id="b088d-267">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="b088d-268">Dosya türü derlemek için yeni eklenen sonra proje klasörünün dışında varsa, `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="b088d-268">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="istool"></a><span data-ttu-id="b088d-269">IsTool</span><span class="sxs-lookup"><span data-stu-id="b088d-269">IsTool</span></span>

<span data-ttu-id="b088d-270">Kullanırken `MSBuild /t:pack /p:IsTool=true`, tüm dosyaları belirtilen çıktı [çıkış derlemelerinin](#output-assemblies) senaryosu, kopyalanır `tools` klasörü yerine `lib` klasör.</span><span class="sxs-lookup"><span data-stu-id="b088d-270">When using `MSBuild /t:pack /p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="b088d-271">Bu farklı olduğuna dikkat edin bir `DotNetCliTool` , belirtilen ayarlayarak `PackageType` içinde `.csproj` dosya.</span><span class="sxs-lookup"><span data-stu-id="b088d-271">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="b088d-272">Bir .nuspec kullanarak paketleme</span><span class="sxs-lookup"><span data-stu-id="b088d-272">Packing using a .nuspec</span></span>

<span data-ttu-id="b088d-273">Kullanabileceğiniz bir `.nuspec` almak için SDK proje dosyası olması koşuluyla, projenizin paketi dosyaya `NuGet.Build.Tasks.Pack.targets` böylece paketi görevi çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="b088d-273">You can use a `.nuspec` file to pack your project provided that you have a SDK project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="b088d-274">Hala bir nuspec dosyası paketlemeden önce projeyi geri yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b088d-274">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="b088d-275">Proje dosyası hedef Framework'ü ilgisiz ve bir nuspec sevk kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="b088d-275">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="b088d-276">Aşağıdaki üç MSBuild özellikleri kullanarak paket için uygun olan bir `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="b088d-276">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="b088d-277">`NuspecFile`: göreli veya mutlak bir yol `.nuspec` paketleme için kullanılan dosya.</span><span class="sxs-lookup"><span data-stu-id="b088d-277">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="b088d-278">`NuspecProperties`: noktalı virgülle ayrılmış listesini anahtar = değer çiftleri.</span><span class="sxs-lookup"><span data-stu-id="b088d-278">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="b088d-279">MSBuild komut satırı ayrıştırma works yöntemi nedeniyle birden çok özellikleri şu şekilde belirtilmelidir: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="b088d-279">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="b088d-280">`NuspecBasePath`: Temel yolu `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="b088d-280">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="b088d-281">Kullanıyorsanız `dotnet.exe` projenizi paketi için bir komut aşağıdaki gibi kullanın:</span><span class="sxs-lookup"><span data-stu-id="b088d-281">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="b088d-282">MSBuild projenizi Paketi kullanıyorsanız, aşağıdaki gibi bir komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="b088d-282">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="b088d-283">Lütfen bir nuspec paket dotnet.exe veya msbuild kullanarak da varsayılan olarak projeyi oluşturmayı için müşteri adayları olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b088d-283">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="b088d-284">Bu geçirerek önlenebilir ```--no-build``` ayarı eşdeğerdir dotnet.exe özelliğine ```<NoBuild>true</NoBuild> ``` ayarı ile birlikte, proje dosyanızdaki ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` proje dosyasında</span><span class="sxs-lookup"><span data-stu-id="b088d-284">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file</span></span>

<span data-ttu-id="b088d-285">Nuspec dosyası paketlemek için csproj dosyası örneği verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="b088d-285">An example of a csproj file to pack a nuspec file is:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <NoBuild>true</NoBuild>
    <IncludeBuildOutput>false</IncludeBuildOutput>
    <NuspecFile>PATH_TO_NUSPEC_FILE</NuspecFile>
    <NuspecProperties>add nuspec properties here</NuspecProperties>
    <NuspecBasePath>optional to provide</NuspecBasePath>
  </PropertyGroup>
</Project>
```

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="b088d-286">Özelleştirilmiş paketi oluşturmak için uzantı noktaları Gelişmiş</span><span class="sxs-lookup"><span data-stu-id="b088d-286">Advanced extension points to create customized package</span></span>

<span data-ttu-id="b088d-287">`pack` Hedef iç, hedef framework belirli derlemede çalıştırılan iki uzantı noktaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="b088d-287">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="b088d-288">Hedef framework belirli içerik ve derlemeler pakete dahil olmak üzere uzantı noktalarını destekler:</span><span class="sxs-lookup"><span data-stu-id="b088d-288">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="b088d-289">`TargetsForTfmSpecificBuildOutput` Hedef: kullanım içindeki dosyaları için `lib` klasör veya kullanarak belirtilen bir klasör `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="b088d-289">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="b088d-290">`TargetsForTfmSpecificContentInPackage` Hedef: dışındaki dosyalara kullanılmak `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="b088d-290">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="b088d-291">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="b088d-291">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="b088d-292">Özel bir hedef yazma ve değeri olarak belirtin `$(TargetsForTfmSpecificBuildOutput)` özelliği.</span><span class="sxs-lookup"><span data-stu-id="b088d-292">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="b088d-293">Gitmesi gereken herhangi bir dosya için `BuildOutputTargetFolder` (lib varsayılan olarak), hedef dosyalar ItemGroup yazmalısınız `BuildOutputInPackage` ve aşağıdaki iki meta veri değerleri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="b088d-293">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="b088d-294">`FinalOutputPath`: Mutlak dosyasının yolunu; sağlanmazsa, kimliği kaynak yolu değerlendirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b088d-294">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="b088d-295">`TargetPath`: (İsteğe bağlı) dosya içinde bir alt yerleştirilmesini gerektiğinde ayarlamak `lib\<TargetFramework>` ilgili kültür klasörlerine altında ötesine derlemeleri uydu gibi.</span><span class="sxs-lookup"><span data-stu-id="b088d-295">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="b088d-296">Varsayılan olarak dosyasının adı.</span><span class="sxs-lookup"><span data-stu-id="b088d-296">Defaults to the name of the file.</span></span>

<span data-ttu-id="b088d-297">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b088d-297">Example:</span></span>

```xml
<PropertyGroup>
  <TargetsForTfmSpecificBuildOutput>$(TargetsForTfmSpecificBuildOutput);GetMyPackageFiles</TargetsForTfmSpecificBuildOutput>
</PropertyGroup>

<Target Name="GetMyPackageFiles">
  <ItemGroup>
    <BuildOutputInPackage Include="$(OutputPath)cs\$(AssemblyName).resources.dll">
        <TargetPath>cs</TargetPath>
    </BuildOutputInPackage>
  </ItemGroup>
</Target>
```

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="b088d-298">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="b088d-298">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="b088d-299">Özel bir hedef yazma ve değeri olarak belirtin `$(TargetsForTfmSpecificContentInPackage)` özelliği.</span><span class="sxs-lookup"><span data-stu-id="b088d-299">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="b088d-300">Pakete dahil etmek için tüm dosyaları, hedef ItemGroup bu dosyaları yazmalısınız `TfmSpecificPackageFile` ve aşağıdaki isteğe bağlı meta veriler ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="b088d-300">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="b088d-301">`PackagePath`: Yolu dosya paketinde çıkış burada olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b088d-301">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="b088d-302">Birden fazla dosya aynı paket yolu eklediyseniz NuGet bir uyarı verir.</span><span class="sxs-lookup"><span data-stu-id="b088d-302">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="b088d-303">`BuildAction`: Paket yolu ise dosyasına atamak için derleme eylem yalnızca gerekli `contentFiles` klasör.</span><span class="sxs-lookup"><span data-stu-id="b088d-303">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="b088d-304">Varsayılan olarak "None".</span><span class="sxs-lookup"><span data-stu-id="b088d-304">Defaults to "None".</span></span>

<span data-ttu-id="b088d-305">Örnek:</span><span class="sxs-lookup"><span data-stu-id="b088d-305">An example:</span></span>
```xml
<PropertyGroup>
  <TargetsForTfmSpecificContentInPackage>$(TargetsForTfmSpecificContentInPackage);CustomContentTarget</TargetsForTfmSpecificContentInPackage>
</PropertyGroup>

<Target Name=""CustomContentTarget"">
  <ItemGroup>
    <TfmSpecificPackageFile Include=""abc.txt"">
      <PackagePath>mycontent/$(TargetFramework)</PackagePath>
    </TfmSpecificPackageFile>
    <TfmSpecificPackageFile Include=""Extensions/ext.txt"" Condition=""'$(TargetFramework)' == 'net46'"">
      <PackagePath>net46content</PackagePath>
    </TfmSpecificPackageFile>  
  </ItemGroup>
</Target>  
```

## <a name="restore-target"></a><span data-ttu-id="b088d-306">geri yükleme hedefi</span><span class="sxs-lookup"><span data-stu-id="b088d-306">restore target</span></span>

<span data-ttu-id="b088d-307">`MSBuild /t:restore` (hangi `nuget restore` ve `dotnet restore` .NET Core projeleriyle kullanmak), proje dosyasında aşağıdaki gibi başvurduğu paketleri yükler:</span><span class="sxs-lookup"><span data-stu-id="b088d-307">`MSBuild /t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="b088d-308">Tüm proje için proje başvuruları okuma</span><span class="sxs-lookup"><span data-stu-id="b088d-308">Read all project to project references</span></span>
1. <span data-ttu-id="b088d-309">Ara klasörü ve hedef çerçeveleri bulmak için proje özelliklerini okuma</span><span class="sxs-lookup"><span data-stu-id="b088d-309">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="b088d-310">Msbuild veri NuGet.Build.Tasks.dll geçirmek</span><span class="sxs-lookup"><span data-stu-id="b088d-310">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="b088d-311">Geri yükleme çalıştırma</span><span class="sxs-lookup"><span data-stu-id="b088d-311">Run restore</span></span>
1. <span data-ttu-id="b088d-312">Paketleri indirin</span><span class="sxs-lookup"><span data-stu-id="b088d-312">Download packages</span></span>
1. <span data-ttu-id="b088d-313">Varlıklar dosya, hedefleri ve özellik yazma</span><span class="sxs-lookup"><span data-stu-id="b088d-313">Write assets file, targets, and props</span></span>

<span data-ttu-id="b088d-314">`restore` Hedef works **yalnızca** PackageReference biçimini kullanarak projeleri için.</span><span class="sxs-lookup"><span data-stu-id="b088d-314">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="b088d-315">Mevcut **değil** kullanarak projeleri için iş `packages.config` biçimini; kullanın [nuget restore](../tools/cli-ref-restore.md) yerine.</span><span class="sxs-lookup"><span data-stu-id="b088d-315">It does **not** work for projects using the `packages.config` format; use [nuget restore](../tools/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="b088d-316">Özellikler geri yükleme</span><span class="sxs-lookup"><span data-stu-id="b088d-316">Restore properties</span></span>

<span data-ttu-id="b088d-317">Ek geri yükleme ayarlarını MSBuild proje dosyası özelliklerinde alınması.</span><span class="sxs-lookup"><span data-stu-id="b088d-317">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="b088d-318">Değerleri de ayarlanabilir kullanarak komut satırından `/p:` geçiş (aşağıdaki örneklere bakın).</span><span class="sxs-lookup"><span data-stu-id="b088d-318">Values can also be set from the command line using the `/p:` switch (see Examples below).</span></span>

| <span data-ttu-id="b088d-319">Özellik</span><span class="sxs-lookup"><span data-stu-id="b088d-319">Property</span></span> | <span data-ttu-id="b088d-320">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b088d-320">Description</span></span> |
|--------|--------|
| <span data-ttu-id="b088d-321">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="b088d-321">RestoreSources</span></span> | <span data-ttu-id="b088d-322">Paket kaynaklarını noktalı virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="b088d-322">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="b088d-323">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="b088d-323">RestorePackagesPath</span></span> | <span data-ttu-id="b088d-324">Kullanıcı paketleri klasör yolu.</span><span class="sxs-lookup"><span data-stu-id="b088d-324">User packages folder path.</span></span> |
| <span data-ttu-id="b088d-325">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="b088d-325">RestoreDisableParallel</span></span> | <span data-ttu-id="b088d-326">Bir seferde bir sınır indirir.</span><span class="sxs-lookup"><span data-stu-id="b088d-326">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="b088d-327">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="b088d-327">RestoreConfigFile</span></span> | <span data-ttu-id="b088d-328">Yol için bir `Nuget.Config` uygulamak için dosya.</span><span class="sxs-lookup"><span data-stu-id="b088d-328">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="b088d-329">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="b088d-329">RestoreNoCache</span></span> | <span data-ttu-id="b088d-330">TRUE ise, önbelleğe alınan paketler kullanarak önler.</span><span class="sxs-lookup"><span data-stu-id="b088d-330">If true, avoids using cached packages.</span></span> <span data-ttu-id="b088d-331">Bkz: [genel paketleri ve önbellek klasör yönetimi](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="b088d-331">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="b088d-332">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="b088d-332">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="b088d-333">TRUE ise, başarısız olan veya eksik paket kaynaklarını yok sayar.</span><span class="sxs-lookup"><span data-stu-id="b088d-333">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="b088d-334">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="b088d-334">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="b088d-335">Yolu `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="b088d-335">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="b088d-336">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="b088d-336">RestoreGraphProjectInput</span></span> | <span data-ttu-id="b088d-337">Mutlak yollar içermesi gereken geri yüklemek için projeleri noktalı virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="b088d-337">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="b088d-338">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="b088d-338">RestoreOutputPath</span></span> | <span data-ttu-id="b088d-339">Çıkış klasörüne varsayarak, `obj` klasörü.</span><span class="sxs-lookup"><span data-stu-id="b088d-339">Output folder, defaulting to the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="b088d-340">Örnekler</span><span class="sxs-lookup"><span data-stu-id="b088d-340">Examples</span></span>

<span data-ttu-id="b088d-341">Komut satırı:</span><span class="sxs-lookup"><span data-stu-id="b088d-341">Command line:</span></span>

```cli
msbuild /t:restore /p:RestoreConfigFile=<path>
```

<span data-ttu-id="b088d-342">Proje dosyası:</span><span class="sxs-lookup"><span data-stu-id="b088d-342">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="b088d-343">Çıkış geri yükleme</span><span class="sxs-lookup"><span data-stu-id="b088d-343">Restore outputs</span></span>

<span data-ttu-id="b088d-344">Geri yükleme yapı aşağıdaki dosyaları oluşturur `obj` klasörü:</span><span class="sxs-lookup"><span data-stu-id="b088d-344">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="b088d-345">Dosya</span><span class="sxs-lookup"><span data-stu-id="b088d-345">File</span></span> | <span data-ttu-id="b088d-346">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b088d-346">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="b088d-347">Tüm paket referanslarını bağımlılık grafiğinin içerir.</span><span class="sxs-lookup"><span data-stu-id="b088d-347">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="b088d-348">MSBuild özellik paketlerinde bulunan başvurular</span><span class="sxs-lookup"><span data-stu-id="b088d-348">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="b088d-349">MSBuild hedefleri paketlerinde bulunan başvurular</span><span class="sxs-lookup"><span data-stu-id="b088d-349">References to MSBuild targets contained in packages</span></span> |

### <a name="packagetargetfallback"></a><span data-ttu-id="b088d-350">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="b088d-350">PackageTargetFallback</span></span>

<span data-ttu-id="b088d-351">`PackageTargetFallback` Öğesi paketleri geri yüklenirken kullanılacak uyumlu hedefleri kümesi belirtmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="b088d-351">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="b088d-352">Bir dotnet kullanmak paketleri izin vermek için tasarlanmış [TxM](../reference/target-frameworks.md) dotnet TxM bildirmeyin uyumlu paketlerle çalışmak için.</span><span class="sxs-lookup"><span data-stu-id="b088d-352">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="b088d-353">Projeniz TxM dotnet kullanıyorsa, eklediğiniz sürece diğer bir deyişle, daha sonra bağlı olduğu gereken üzerinde de tüm paketler dotnet TxM, olması `<PackageTargetFallback>` dotnet ile uyumlu olacak şekilde dotnet olmayan platformları izin vermek üzere projenize.</span><span class="sxs-lookup"><span data-stu-id="b088d-353">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="b088d-354">Proje kullanıyorsa, örneğin, `netstandard1.6` TxM ve bağımlı paketi içeren yalnızca `lib/net45/a.dll` ve `lib/portable-net45+win81/a.dll`, projeyi oluşturmak başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="b088d-354">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="b088d-355">Getirileceğini istediğiniz ikinci DLL'dir sonra ekleyebileceğiniz bir `PackageTargetFallback` gibi söylemek için `portable-net45+win81` DLL uyumludur:</span><span class="sxs-lookup"><span data-stu-id="b088d-355">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="b088d-356">Projenizdeki tüm hedefler için bir geri dönüş bildirmek için devre dışı bırakın `Condition` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="b088d-356">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="b088d-357">Var olan genişletebilirsiniz `PackageTargetFallback` ekleyerek `$(PackageTargetFallback)` aşağıda gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="b088d-357">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="b088d-358">Bir geri yükleme grafik bir kitaplıktan değiştirme</span><span class="sxs-lookup"><span data-stu-id="b088d-358">Replacing one library from a restore graph</span></span>

<span data-ttu-id="b088d-359">Bir geri yükleme yanlış derleme getiren, paketleri seçim varsayılan ve kendi seçimi ile değiştir dışlamak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="b088d-359">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="b088d-360">Üst düzey ile ilk `PackageReference`, tüm varlıklar çıkar:</span><span class="sxs-lookup"><span data-stu-id="b088d-360">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="b088d-361">Ardından, DLL uygun yerel kopyasını kendi başvuru ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b088d-361">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
