---
title: NuGet paketi ve geri yükleme MSBuild hedefleri olarak | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/23/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: NuGet paketi ve geri yükleme, doğrudan NuGet 4.0 + ile MSBuild hedefleri olarak çalışabilir.
keywords: NuGet ve MSBuild, NuGet paketi hedef, NuGet geri yükleme hedefi
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: a9c2c2229d717dff8472dce0ba568e4a21900b19
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="f72d7-104">NuGet paketi ve MSBuild hedefleri olarak geri yükleme</span><span class="sxs-lookup"><span data-stu-id="f72d7-104">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="f72d7-105">*NuGet 4.0+*</span><span class="sxs-lookup"><span data-stu-id="f72d7-105">*NuGet 4.0+*</span></span>

<span data-ttu-id="f72d7-106">PackageReference biçimiyle NuGet 4.0 + doğrudan ayrı bir kullanmak yerine bir proje dosyası içinde tüm bildirim meta veri depolayabilirsiniz `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="f72d7-106">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="f72d7-107">MSBuild ile 15.1 +, NuGet birinci sınıf MSBuild vatandaşı ile aynı zamanda olan `pack` ve `restore` aşağıda açıklandığı gibi hedefler.</span><span class="sxs-lookup"><span data-stu-id="f72d7-107">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="f72d7-108">Bu hedeflerde, diğer MSBuild görev veya hedef ile olduğu gibi NuGet ile çalışmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="f72d7-108">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="f72d7-109">(NuGet için 3.x ve daha önce kullandığınız [paketi](../tools/cli-ref-pack.md) ve [geri](../tools/cli-ref-restore.md) NuGet CLI aracılığıyla yerine komutları.)</span><span class="sxs-lookup"><span data-stu-id="f72d7-109">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="f72d7-110">Hedef derleme sırası</span><span class="sxs-lookup"><span data-stu-id="f72d7-110">Target build order</span></span>

<span data-ttu-id="f72d7-111">Olduğundan `pack` ve `restore` MSBuild hedefleri şunlardır akışınızı artırmak için bunları erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f72d7-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="f72d7-112">Örneğin, paket sonra bir ağ paylaşımına paketinizi kopyalamak istediğiniz varsayalım.</span><span class="sxs-lookup"><span data-stu-id="f72d7-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="f72d7-113">Bunu, proje dosyasında aşağıdaki ekleyerek yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f72d7-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
    <Copy
        SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
        DestinationFolder="\\myshare\packageshare\"
        />
</Target>
```

<span data-ttu-id="f72d7-114">Benzer şekilde, bir MSBuild görev yazabileceğiniz, kendi hedef yazma ve MSBuild görevi NuGet özelliklerinde kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="f72d7-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="f72d7-115">paketi hedef</span><span class="sxs-lookup"><span data-stu-id="f72d7-115">pack target</span></span>

<span data-ttu-id="f72d7-116">PackageReference biçimini kullanarak, kullanarak .NET standart projeleri için `msbuild /t:pack` bir NuGet paketi oluşturmak için proje dosyasından girişleri çizer.</span><span class="sxs-lookup"><span data-stu-id="f72d7-116">For .NET Standard projects using the PackageReference format, using `msbuild /t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="f72d7-117">Proje dosyası içinde ilk eklenebilir MSBuild özellikler aşağıdaki tabloda açıklanmıştır `<PropertyGroup>` düğümü.</span><span class="sxs-lookup"><span data-stu-id="f72d7-117">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="f72d7-118">Bu düzenlemeler kolayca Visual Studio 2017 ve daha sonra projeye sağ tıklayıp seçerek yapabileceğiniz **{project_name} Düzenle** bağlam menüsünde.</span><span class="sxs-lookup"><span data-stu-id="f72d7-118">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="f72d7-119">Kolaylık olması için tablo eşdeğer özelliği tarafından düzenlenir bir [ `.nuspec` dosya](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="f72d7-119">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="f72d7-120">Unutmayın `Owners` ve `Summary` özelliklerinden `.nuspec` MSBuild ile desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="f72d7-120">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="f72d7-121">Öznitelik/NuSpec değeri</span><span class="sxs-lookup"><span data-stu-id="f72d7-121">Attribute/NuSpec Value</span></span> | <span data-ttu-id="f72d7-122">MSBuild özelliği</span><span class="sxs-lookup"><span data-stu-id="f72d7-122">MSBuild Property</span></span> | <span data-ttu-id="f72d7-123">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="f72d7-123">Default</span></span> | <span data-ttu-id="f72d7-124">Notlar</span><span class="sxs-lookup"><span data-stu-id="f72d7-124">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="f72d7-125">Kimliği</span><span class="sxs-lookup"><span data-stu-id="f72d7-125">Id</span></span> | <span data-ttu-id="f72d7-126">PackageId</span><span class="sxs-lookup"><span data-stu-id="f72d7-126">PackageId</span></span> | <span data-ttu-id="f72d7-127">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="f72d7-127">AssemblyName</span></span> | <span data-ttu-id="f72d7-128">MSBuild gelen $(AssemblyName)</span><span class="sxs-lookup"><span data-stu-id="f72d7-128">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="f72d7-129">Sürüm</span><span class="sxs-lookup"><span data-stu-id="f72d7-129">Version</span></span> | <span data-ttu-id="f72d7-130">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="f72d7-130">PackageVersion</span></span> | <span data-ttu-id="f72d7-131">Sürüm</span><span class="sxs-lookup"><span data-stu-id="f72d7-131">Version</span></span> | <span data-ttu-id="f72d7-132">Bu semver örnek "1.0.0", "1.0.0-beta" veya "1.0.0-beta-00345" için uyumlu değil</span><span class="sxs-lookup"><span data-stu-id="f72d7-132">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="f72d7-133">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="f72d7-133">VersionPrefix</span></span> | <span data-ttu-id="f72d7-134">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="f72d7-134">PackageVersionPrefix</span></span> | <span data-ttu-id="f72d7-135">empty</span><span class="sxs-lookup"><span data-stu-id="f72d7-135">empty</span></span> | <span data-ttu-id="f72d7-136">PackageVersionPrefix PackageVersion ayarını geçersiz kılar</span><span class="sxs-lookup"><span data-stu-id="f72d7-136">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="f72d7-137">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="f72d7-137">VersionSuffix</span></span> | <span data-ttu-id="f72d7-138">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="f72d7-138">PackageVersionSuffix</span></span> | <span data-ttu-id="f72d7-139">empty</span><span class="sxs-lookup"><span data-stu-id="f72d7-139">empty</span></span> | <span data-ttu-id="f72d7-140">MSBuild gelen $(VersionSuffix).</span><span class="sxs-lookup"><span data-stu-id="f72d7-140">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="f72d7-141">PackageVersionSuffix PackageVersion ayarını geçersiz kılar</span><span class="sxs-lookup"><span data-stu-id="f72d7-141">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="f72d7-142">Yazarlar</span><span class="sxs-lookup"><span data-stu-id="f72d7-142">Authors</span></span> | <span data-ttu-id="f72d7-143">Yazarlar</span><span class="sxs-lookup"><span data-stu-id="f72d7-143">Authors</span></span> | <span data-ttu-id="f72d7-144">Geçerli kullanıcının kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="f72d7-144">Username of the current user</span></span> | |
| <span data-ttu-id="f72d7-145">Sahipleri</span><span class="sxs-lookup"><span data-stu-id="f72d7-145">Owners</span></span> | <span data-ttu-id="f72d7-146">Yok</span><span class="sxs-lookup"><span data-stu-id="f72d7-146">N/A</span></span> | <span data-ttu-id="f72d7-147">NuSpec içinde mevcut olmayan</span><span class="sxs-lookup"><span data-stu-id="f72d7-147">Not present in NuSpec</span></span> | |
| <span data-ttu-id="f72d7-148">Başlık</span><span class="sxs-lookup"><span data-stu-id="f72d7-148">Title</span></span> | <span data-ttu-id="f72d7-149">Başlık</span><span class="sxs-lookup"><span data-stu-id="f72d7-149">Title</span></span> | <span data-ttu-id="f72d7-150">Paket kimliği</span><span class="sxs-lookup"><span data-stu-id="f72d7-150">The PackageId</span></span>| |
| <span data-ttu-id="f72d7-151">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f72d7-151">Description</span></span> | <span data-ttu-id="f72d7-152">PackageDescription</span><span class="sxs-lookup"><span data-stu-id="f72d7-152">PackageDescription</span></span> | <span data-ttu-id="f72d7-153">"Paketi"</span><span class="sxs-lookup"><span data-stu-id="f72d7-153">"Package Description"</span></span> | |
| <span data-ttu-id="f72d7-154">Telif Hakkı</span><span class="sxs-lookup"><span data-stu-id="f72d7-154">Copyright</span></span> | <span data-ttu-id="f72d7-155">Telif Hakkı</span><span class="sxs-lookup"><span data-stu-id="f72d7-155">Copyright</span></span> | <span data-ttu-id="f72d7-156">empty</span><span class="sxs-lookup"><span data-stu-id="f72d7-156">empty</span></span> | |
| <span data-ttu-id="f72d7-157">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="f72d7-157">RequireLicenseAcceptance</span></span> | <span data-ttu-id="f72d7-158">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="f72d7-158">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="f72d7-159">false</span><span class="sxs-lookup"><span data-stu-id="f72d7-159">false</span></span> | |
| <span data-ttu-id="f72d7-160">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="f72d7-160">LicenseUrl</span></span> | <span data-ttu-id="f72d7-161">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="f72d7-161">PackageLicenseUrl</span></span> | <span data-ttu-id="f72d7-162">empty</span><span class="sxs-lookup"><span data-stu-id="f72d7-162">empty</span></span> | |
| <span data-ttu-id="f72d7-163">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="f72d7-163">ProjectUrl</span></span> | <span data-ttu-id="f72d7-164">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="f72d7-164">PackageProjectUrl</span></span> | <span data-ttu-id="f72d7-165">empty</span><span class="sxs-lookup"><span data-stu-id="f72d7-165">empty</span></span> | |
| <span data-ttu-id="f72d7-166">IconUrl</span><span class="sxs-lookup"><span data-stu-id="f72d7-166">IconUrl</span></span> | <span data-ttu-id="f72d7-167">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="f72d7-167">PackageIconUrl</span></span> | <span data-ttu-id="f72d7-168">empty</span><span class="sxs-lookup"><span data-stu-id="f72d7-168">empty</span></span> | |
| <span data-ttu-id="f72d7-169">Etiketler</span><span class="sxs-lookup"><span data-stu-id="f72d7-169">Tags</span></span> | <span data-ttu-id="f72d7-170">PackageTags</span><span class="sxs-lookup"><span data-stu-id="f72d7-170">PackageTags</span></span> | <span data-ttu-id="f72d7-171">empty</span><span class="sxs-lookup"><span data-stu-id="f72d7-171">empty</span></span> | <span data-ttu-id="f72d7-172">Etiketleri noktalı virgülle ayrılmış olan.</span><span class="sxs-lookup"><span data-stu-id="f72d7-172">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="f72d7-173">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="f72d7-173">ReleaseNotes</span></span> | <span data-ttu-id="f72d7-174">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="f72d7-174">PackageReleaseNotes</span></span> | <span data-ttu-id="f72d7-175">empty</span><span class="sxs-lookup"><span data-stu-id="f72d7-175">empty</span></span> | |
| <span data-ttu-id="f72d7-176">Depo/URL'si</span><span class="sxs-lookup"><span data-stu-id="f72d7-176">Repository/Url</span></span> | <span data-ttu-id="f72d7-177">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="f72d7-177">RepositoryUrl</span></span> | <span data-ttu-id="f72d7-178">empty</span><span class="sxs-lookup"><span data-stu-id="f72d7-178">empty</span></span> | <span data-ttu-id="f72d7-179">Depo URL'si kopyalama veya kaynak kodu almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f72d7-179">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="f72d7-180">Örnek: *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="f72d7-180">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="f72d7-181">Depo/türü</span><span class="sxs-lookup"><span data-stu-id="f72d7-181">Repository/Type</span></span> | <span data-ttu-id="f72d7-182">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="f72d7-182">RepositoryType</span></span> | <span data-ttu-id="f72d7-183">empty</span><span class="sxs-lookup"><span data-stu-id="f72d7-183">empty</span></span> | <span data-ttu-id="f72d7-184">Depo türü.</span><span class="sxs-lookup"><span data-stu-id="f72d7-184">Repository type.</span></span> <span data-ttu-id="f72d7-185">Örnekler: *git*, *tfs*.</span><span class="sxs-lookup"><span data-stu-id="f72d7-185">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="f72d7-186">Depo/şube</span><span class="sxs-lookup"><span data-stu-id="f72d7-186">Repository/Branch</span></span> | <span data-ttu-id="f72d7-187">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="f72d7-187">RepositoryBranch</span></span> | <span data-ttu-id="f72d7-188">empty</span><span class="sxs-lookup"><span data-stu-id="f72d7-188">empty</span></span> | <span data-ttu-id="f72d7-189">İsteğe bağlı depo şube bilgileri.</span><span class="sxs-lookup"><span data-stu-id="f72d7-189">Optional repository branch information.</span></span> <span data-ttu-id="f72d7-190">*RepositoryUrl* dahil edilmek üzere bu özellik için de belirtilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="f72d7-190">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="f72d7-191">Örnek: *ana* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="f72d7-191">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="f72d7-192">Depo/tamamlama</span><span class="sxs-lookup"><span data-stu-id="f72d7-192">Repository/Commit</span></span> | <span data-ttu-id="f72d7-193">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="f72d7-193">RepositoryCommit</span></span> | <span data-ttu-id="f72d7-194">empty</span><span class="sxs-lookup"><span data-stu-id="f72d7-194">empty</span></span> | <span data-ttu-id="f72d7-195">İsteğe bağlı depo yürütme veya, paket kaynak belirtmek için değişiklik karşı oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="f72d7-195">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="f72d7-196">*RepositoryUrl* dahil edilmek üzere bu özellik için de belirtilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="f72d7-196">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="f72d7-197">Örnek: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="f72d7-197">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="f72d7-198">PackageType</span><span class="sxs-lookup"><span data-stu-id="f72d7-198">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="f72d7-199">Özet</span><span class="sxs-lookup"><span data-stu-id="f72d7-199">Summary</span></span> | <span data-ttu-id="f72d7-200">Desteklenmez</span><span class="sxs-lookup"><span data-stu-id="f72d7-200">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="f72d7-201">paketi hedef girişleri</span><span class="sxs-lookup"><span data-stu-id="f72d7-201">pack target inputs</span></span>

- <span data-ttu-id="f72d7-202">IsPackable</span><span class="sxs-lookup"><span data-stu-id="f72d7-202">IsPackable</span></span>
- <span data-ttu-id="f72d7-203">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="f72d7-203">PackageVersion</span></span>
- <span data-ttu-id="f72d7-204">PackageId</span><span class="sxs-lookup"><span data-stu-id="f72d7-204">PackageId</span></span>
- <span data-ttu-id="f72d7-205">Yazarlar</span><span class="sxs-lookup"><span data-stu-id="f72d7-205">Authors</span></span>
- <span data-ttu-id="f72d7-206">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f72d7-206">Description</span></span>
- <span data-ttu-id="f72d7-207">Telif Hakkı</span><span class="sxs-lookup"><span data-stu-id="f72d7-207">Copyright</span></span>
- <span data-ttu-id="f72d7-208">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="f72d7-208">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="f72d7-209">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="f72d7-209">DevelopmentDependency</span></span>
- <span data-ttu-id="f72d7-210">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="f72d7-210">PackageLicenseUrl</span></span>
- <span data-ttu-id="f72d7-211">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="f72d7-211">PackageProjectUrl</span></span>
- <span data-ttu-id="f72d7-212">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="f72d7-212">PackageIconUrl</span></span>
- <span data-ttu-id="f72d7-213">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="f72d7-213">PackageReleaseNotes</span></span>
- <span data-ttu-id="f72d7-214">PackageTags</span><span class="sxs-lookup"><span data-stu-id="f72d7-214">PackageTags</span></span>
- <span data-ttu-id="f72d7-215">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="f72d7-215">PackageOutputPath</span></span>
- <span data-ttu-id="f72d7-216">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="f72d7-216">IncludeSymbols</span></span>
- <span data-ttu-id="f72d7-217">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="f72d7-217">IncludeSource</span></span>
- <span data-ttu-id="f72d7-218">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="f72d7-218">PackageTypes</span></span>
- <span data-ttu-id="f72d7-219">IsTool</span><span class="sxs-lookup"><span data-stu-id="f72d7-219">IsTool</span></span>
- <span data-ttu-id="f72d7-220">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="f72d7-220">RepositoryUrl</span></span>
- <span data-ttu-id="f72d7-221">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="f72d7-221">RepositoryType</span></span>
- <span data-ttu-id="f72d7-222">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="f72d7-222">RepositoryBranch</span></span>
- <span data-ttu-id="f72d7-223">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="f72d7-223">RepositoryCommit</span></span>
- <span data-ttu-id="f72d7-224">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="f72d7-224">NoPackageAnalysis</span></span>
- <span data-ttu-id="f72d7-225">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="f72d7-225">MinClientVersion</span></span>
- <span data-ttu-id="f72d7-226">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="f72d7-226">IncludeBuildOutput</span></span>
- <span data-ttu-id="f72d7-227">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="f72d7-227">IncludeContentInPack</span></span>
- <span data-ttu-id="f72d7-228">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="f72d7-228">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="f72d7-229">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="f72d7-229">ContentTargetFolders</span></span>
- <span data-ttu-id="f72d7-230">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="f72d7-230">NuspecFile</span></span>
- <span data-ttu-id="f72d7-231">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="f72d7-231">NuspecBasePath</span></span>
- <span data-ttu-id="f72d7-232">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="f72d7-232">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="f72d7-233">Paketi senaryoları</span><span class="sxs-lookup"><span data-stu-id="f72d7-233">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="f72d7-234">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="f72d7-234">PackageIconUrl</span></span>

<span data-ttu-id="f72d7-235">Değişikliğin parçası olarak [NuGet sorunu 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` sonunda değiştirilecek `PackageIconUri` ve sonuçta elde edilen paketin kökünde bulunan bir simge dosyası için göreli bir yol olabilir.</span><span class="sxs-lookup"><span data-stu-id="f72d7-235">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="f72d7-236">Çıktı derlemeler</span><span class="sxs-lookup"><span data-stu-id="f72d7-236">Output assemblies</span></span>

<span data-ttu-id="f72d7-237">`nuget pack` kopya çıktı uzantılara sahip dosyaları `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, ve `.pri`.</span><span class="sxs-lookup"><span data-stu-id="f72d7-237">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="f72d7-238">MSBuild gelen sağladıkları üzerinde kopyalanır ve çıkış dosyalarının bağımlı `BuiltOutputProjectGroup` hedef.</span><span class="sxs-lookup"><span data-stu-id="f72d7-238">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="f72d7-239">Çıkış derlemelerinin nereye proje dosyası veya komut satırı denetlemek için kullanabileceğiniz iki MSBuild özellikleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="f72d7-239">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="f72d7-240">`IncludeBuildOutput`: Derleme çıktı derlemelerinin pakete dahil edilip edilmeyeceğini belirler bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="f72d7-240">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="f72d7-241">`BuildOutputTargetFolder`: Çıktı derlemelerinin yerleştirilmelidir klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="f72d7-241">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="f72d7-242">Çıktı derlemelerinin (ve diğer çıktı dosyaları) ilgili framework klasörlerine kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="f72d7-242">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="f72d7-243">Paket referanslarını</span><span class="sxs-lookup"><span data-stu-id="f72d7-243">Package references</span></span>

<span data-ttu-id="f72d7-244">Bkz: [paketini proje dosyalarını başvurularında](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="f72d7-244">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="f72d7-245">Proje başvuruları projeye</span><span class="sxs-lookup"><span data-stu-id="f72d7-245">Project to project references</span></span>

<span data-ttu-id="f72d7-246">Proje başvuruları projeye değerlendirilir varsayılan olarak nuget paket referanslarını, örneğin:</span><span class="sxs-lookup"><span data-stu-id="f72d7-246">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="f72d7-247">Ayrıca, aşağıdaki meta verileri, proje başvurusu ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f72d7-247">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="f72d7-248">Bir paketteki içerik dahil olmak üzere</span><span class="sxs-lookup"><span data-stu-id="f72d7-248">Including content in a package</span></span>

<span data-ttu-id="f72d7-249">İçerik eklemek için fazladan meta verileri, mevcut eklemek `<Content>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="f72d7-249">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="f72d7-250">Varsayılan olarak girişlerle geçersiz kılma sürece "İçerik" paketinde türünde her şeyi ister aşağıdakiler:</span><span class="sxs-lookup"><span data-stu-id="f72d7-250">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
    <Content Include="..\win7-x64\libuv.txt">
        <Pack>false</Pack>
    </Content>
 ```

<span data-ttu-id="f72d7-251">Varsayılan olarak, her şeyi köküne eklenen `content` ve `contentFiles\any\<target_framework>` bir paket ve korur klasördeki göreli klasör yapısı, bir paket yolu belirtmediğiniz sürece:</span><span class="sxs-lookup"><span data-stu-id="f72d7-251">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="f72d7-252">Yalnızca belirli bir tüm içeriğinizi kopyalamak isterseniz klasörlerde kök (yerine `content` ve `contentFiles` her ikisi de), MSBuild özelliği kullanabilirsiniz `ContentTargetFolders`, varsayılan olarak "içerik; Content dosyaları" ancak başka bir klasör adı için ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="f72d7-252">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="f72d7-253">Not "Content dosyaları" belirterek, yalnızca `ContentTargetFolders` altında dosyaları koyan `contentFiles\any\<target_framework>` veya `contentFiles\<language>\<target_framework>` göre `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="f72d7-253">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="f72d7-254">`PackagePath` hedef yolları noktalı virgülle ayrılmış bir kümesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="f72d7-254">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="f72d7-255">Bir boş paket yolu belirterek dosya paket köküne ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f72d7-255">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="f72d7-256">Örneğin, aşağıdaki ekler `libuv.txt` için `content\myfiles`, `content\samples`ve paket kök:</span><span class="sxs-lookup"><span data-stu-id="f72d7-256">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="f72d7-257">Ayrıca bir MSBuild özelliği olan `$(IncludeContentInPack)`, varsayılan olarak `true`.</span><span class="sxs-lookup"><span data-stu-id="f72d7-257">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="f72d7-258">Bu ayarlanırsa `false` hiçbir projede sonra proje içerikten eklenmemiştir nuget paketi.</span><span class="sxs-lookup"><span data-stu-id="f72d7-258">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="f72d7-259">Yukarıdaki öğelerin hiçbirinde ayarlayabilirsiniz diğer paketi belirli meta verileri içeren ```<PackageCopyToOutput>``` ve ```<PackageFlatten>``` hangi kümeleri ```CopyToOutput``` ve ```Flatten``` üzerinde değerleri ```contentFiles``` çıkış nuspec girişi.</span><span class="sxs-lookup"><span data-stu-id="f72d7-259">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="f72d7-260">İçerik öğeleri dışında `<Pack>` ve `<PackagePath>` meta verileri de ayarlanabilir derleme, EmbeddedResource, ApplicationDefinition, sayfa, kaynak, KarşılamaEkranı, DesignData, DesignDataWithDesignTimeCreateableTypes yapı eylemiyle dosyalarda , CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource veya yok.</span><span class="sxs-lookup"><span data-stu-id="f72d7-260">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="f72d7-261">Dosya adı, paket yolu genelleme desenleri kullanırken eklenecek paketi için paket yolu paket yoluyla dosya adını içeren tam yol kabul edilir klasör ayırıcı karakter, aksi takdirde ile bitmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="f72d7-261">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="f72d7-262">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="f72d7-262">IncludeSymbols</span></span>

<span data-ttu-id="f72d7-263">Kullanırken `MSBuild /t:pack /p:IncludeSymbols=true`, karşılık gelen `.pdb` dosyaları, diğer çıkış dosyalarının yanı sıra kopyalanır (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="f72d7-263">When using `MSBuild /t:pack /p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="f72d7-264">Bu ayarı Not `IncludeSymbols=true` normal bir paket oluşturur *ve* simge paketi.</span><span class="sxs-lookup"><span data-stu-id="f72d7-264">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="f72d7-265">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="f72d7-265">IncludeSource</span></span>

<span data-ttu-id="f72d7-266">Bu aynı sonucu verir `IncludeSymbols`ile birlikte kaynak dosyalarını kopyalar dışında `.pdb` da dosyaları.</span><span class="sxs-lookup"><span data-stu-id="f72d7-266">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="f72d7-267">Tüm dosya türlerini `Compile` üzerinden kopyalanır `src\<ProjectName>\` elde edilen paketindeki göreli yol klasör yapısı korunarak.</span><span class="sxs-lookup"><span data-stu-id="f72d7-267">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="f72d7-268">Aynı kaynak dosyaları herhangi da yapılır `ProjectReference` olan `TreatAsPackageReference` kümesine `false`.</span><span class="sxs-lookup"><span data-stu-id="f72d7-268">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="f72d7-269">Dosya türü derlemek için yeni eklenen sonra proje klasörünün dışında varsa, `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="f72d7-269">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="istool"></a><span data-ttu-id="f72d7-270">IsTool</span><span class="sxs-lookup"><span data-stu-id="f72d7-270">IsTool</span></span>

<span data-ttu-id="f72d7-271">Kullanırken `MSBuild /t:pack /p:IsTool=true`, tüm dosyaları belirtilen çıktı [çıkış derlemelerinin](#output-assemblies) senaryosu, kopyalanır `tools` klasörü yerine `lib` klasör.</span><span class="sxs-lookup"><span data-stu-id="f72d7-271">When using `MSBuild /t:pack /p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="f72d7-272">Bu farklı olduğuna dikkat edin bir `DotNetCliTool` , belirtilen ayarlayarak `PackageType` içinde `.csproj` dosya.</span><span class="sxs-lookup"><span data-stu-id="f72d7-272">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="f72d7-273">Bir .nuspec kullanarak paketleme</span><span class="sxs-lookup"><span data-stu-id="f72d7-273">Packing using a .nuspec</span></span>

<span data-ttu-id="f72d7-274">Kullanabileceğiniz bir `.nuspec` almak için SDK proje dosyası olması koşuluyla, projenizin paketi dosyaya `NuGet.Build.Tasks.Pack.targets` böylece paketi görevi çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="f72d7-274">You can use a `.nuspec` file to pack your project provided that you have a SDK project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="f72d7-275">Hala bir nuspec dosyası paketlemeden önce projeyi geri yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f72d7-275">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="f72d7-276">Proje dosyası hedef Framework'ü ilgisiz ve bir nuspec sevk kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="f72d7-276">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="f72d7-277">Aşağıdaki üç MSBuild özellikleri kullanarak paket için uygun olan bir `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="f72d7-277">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="f72d7-278">`NuspecFile`: göreli veya mutlak bir yol `.nuspec` paketleme için kullanılan dosya.</span><span class="sxs-lookup"><span data-stu-id="f72d7-278">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="f72d7-279">`NuspecProperties`: noktalı virgülle ayrılmış listesini anahtar = değer çiftleri.</span><span class="sxs-lookup"><span data-stu-id="f72d7-279">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="f72d7-280">MSBuild komut satırı ayrıştırma works yöntemi nedeniyle birden çok özellikleri şu şekilde belirtilmelidir: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="f72d7-280">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="f72d7-281">`NuspecBasePath`: Temel yolu `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="f72d7-281">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="f72d7-282">Kullanıyorsanız `dotnet.exe` projenizi paketi için bir komut aşağıdaki gibi kullanın:</span><span class="sxs-lookup"><span data-stu-id="f72d7-282">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="f72d7-283">MSBuild projenizi Paketi kullanıyorsanız, aşağıdaki gibi bir komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="f72d7-283">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="f72d7-284">Lütfen bir nuspec paket dotnet.exe veya msbuild kullanarak da varsayılan olarak projeyi oluşturmayı için müşteri adayları olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f72d7-284">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="f72d7-285">Bu geçirerek önlenebilir ```--no-build``` ayarı eşdeğerdir dotnet.exe özelliğine ```<NoBuild>true</NoBuild> ``` ayarı ile birlikte, proje dosyanızdaki ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` proje dosyasında</span><span class="sxs-lookup"><span data-stu-id="f72d7-285">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file</span></span>

<span data-ttu-id="f72d7-286">Nuspec dosyası paketlemek için csproj dosyası örneği verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="f72d7-286">An example of a csproj file to pack a nuspec file is:</span></span>

```
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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="f72d7-287">Özelleştirilmiş paketi oluşturmak için uzantı noktaları Gelişmiş</span><span class="sxs-lookup"><span data-stu-id="f72d7-287">Advanced extension points to create customized package</span></span>

<span data-ttu-id="f72d7-288">`pack` Hedef iç, hedef framework belirli derlemede çalıştırılan iki uzantı noktaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="f72d7-288">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="f72d7-289">Hedef framework belirli içerik ve derlemeler pakete dahil olmak üzere uzantı noktalarını destekler:</span><span class="sxs-lookup"><span data-stu-id="f72d7-289">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="f72d7-290">`TargetsForTfmSpecificBuildOutput` Hedef: kullanım içindeki dosyaları için `lib` klasör veya kullanarak belirtilen bir klasör `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="f72d7-290">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="f72d7-291">`TargetsForTfmSpecificContentInPackage` Hedef: dışındaki dosyalara kullanılmak `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="f72d7-291">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="f72d7-292">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="f72d7-292">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="f72d7-293">Özel bir hedef yazma ve değeri olarak belirtin `$(TargetsForTfmSpecificBuildOutput)` özelliği.</span><span class="sxs-lookup"><span data-stu-id="f72d7-293">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="f72d7-294">Gitmesi gereken herhangi bir dosya için `BuildOutputTargetFolder` (lib varsayılan olarak), hedef dosyalar ItemGroup yazmalısınız `BuildOutputInPackage` ve aşağıdaki iki meta veri değerleri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="f72d7-294">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="f72d7-295">`FinalOutputPath`: Mutlak dosyasının yolunu; sağlanmazsa, kimliği kaynak yolu değerlendirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f72d7-295">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="f72d7-296">`TargetPath`: (İsteğe bağlı) dosya içinde bir alt yerleştirilmesini gerektiğinde ayarlamak `lib\<TargetFramework>` ilgili kültür klasörlerine altında ötesine derlemeleri uydu gibi.</span><span class="sxs-lookup"><span data-stu-id="f72d7-296">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="f72d7-297">Varsayılan olarak dosyasının adı.</span><span class="sxs-lookup"><span data-stu-id="f72d7-297">Defaults to the name of the file.</span></span>

<span data-ttu-id="f72d7-298">Örnek:</span><span class="sxs-lookup"><span data-stu-id="f72d7-298">Example:</span></span>

```
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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="f72d7-299">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="f72d7-299">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="f72d7-300">Özel bir hedef yazma ve değeri olarak belirtin `$(TargetsForTfmSpecificContentInPackage)` özelliği.</span><span class="sxs-lookup"><span data-stu-id="f72d7-300">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="f72d7-301">Pakete dahil etmek için tüm dosyaları, hedef ItemGroup bu dosyaları yazmalısınız `TfmSpecificPackageFile` ve aşağıdaki isteğe bağlı meta veriler ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="f72d7-301">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="f72d7-302">`PackagePath`: Yolu dosya paketinde çıkış burada olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f72d7-302">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="f72d7-303">Birden fazla dosya aynı paket yolu eklediyseniz NuGet bir uyarı verir.</span><span class="sxs-lookup"><span data-stu-id="f72d7-303">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="f72d7-304">`BuildAction`: Paket yolu ise dosyasına atamak için derleme eylem yalnızca gerekli `contentFiles` klasör.</span><span class="sxs-lookup"><span data-stu-id="f72d7-304">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="f72d7-305">Varsayılan olarak "None".</span><span class="sxs-lookup"><span data-stu-id="f72d7-305">Defaults to "None".</span></span>

<span data-ttu-id="f72d7-306">Örnek:</span><span class="sxs-lookup"><span data-stu-id="f72d7-306">An example:</span></span>
```
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

## <a name="restore-target"></a><span data-ttu-id="f72d7-307">geri yükleme hedefi</span><span class="sxs-lookup"><span data-stu-id="f72d7-307">restore target</span></span>

<span data-ttu-id="f72d7-308">`MSBuild /t:restore` (hangi `nuget restore` ve `dotnet restore` .NET Core projeleriyle kullanmak), proje dosyasında aşağıdaki gibi başvurduğu paketleri yükler:</span><span class="sxs-lookup"><span data-stu-id="f72d7-308">`MSBuild /t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="f72d7-309">Tüm proje için proje başvuruları okuma</span><span class="sxs-lookup"><span data-stu-id="f72d7-309">Read all project to project references</span></span>
1. <span data-ttu-id="f72d7-310">Ara klasörü ve hedef çerçeveleri bulmak için proje özelliklerini okuma</span><span class="sxs-lookup"><span data-stu-id="f72d7-310">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="f72d7-311">Msbuild veri NuGet.Build.Tasks.dll geçirmek</span><span class="sxs-lookup"><span data-stu-id="f72d7-311">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="f72d7-312">Geri yükleme çalıştırma</span><span class="sxs-lookup"><span data-stu-id="f72d7-312">Run restore</span></span>
1. <span data-ttu-id="f72d7-313">Paketleri indirin</span><span class="sxs-lookup"><span data-stu-id="f72d7-313">Download packages</span></span>
1. <span data-ttu-id="f72d7-314">Varlıklar dosya, hedefleri ve özellik yazma</span><span class="sxs-lookup"><span data-stu-id="f72d7-314">Write assets file, targets, and props</span></span>

<span data-ttu-id="f72d7-315">`restore` Hedef works **yalnızca** PackageReference biçimini kullanarak projeleri için.</span><span class="sxs-lookup"><span data-stu-id="f72d7-315">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="f72d7-316">Mevcut **değil** kullanarak projeleri için iş `packages.config` biçimini; kullanın [nuget restore](../tools/cli-ref-restore.md) yerine.</span><span class="sxs-lookup"><span data-stu-id="f72d7-316">It does **not** work for projects using the `packages.config` format; use [nuget restore](../tools/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="f72d7-317">Özellikler geri yükleme</span><span class="sxs-lookup"><span data-stu-id="f72d7-317">Restore properties</span></span>

<span data-ttu-id="f72d7-318">Ek geri yükleme ayarlarını MSBuild proje dosyası özelliklerinde alınması.</span><span class="sxs-lookup"><span data-stu-id="f72d7-318">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="f72d7-319">Değerleri de ayarlanabilir kullanarak komut satırından `/p:` geçiş (aşağıdaki örneklere bakın).</span><span class="sxs-lookup"><span data-stu-id="f72d7-319">Values can also be set from the command line using the `/p:` switch (see Examples below).</span></span>

| <span data-ttu-id="f72d7-320">Özellik</span><span class="sxs-lookup"><span data-stu-id="f72d7-320">Property</span></span> | <span data-ttu-id="f72d7-321">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f72d7-321">Description</span></span> |
|--------|--------|
| <span data-ttu-id="f72d7-322">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="f72d7-322">RestoreSources</span></span> | <span data-ttu-id="f72d7-323">Paket kaynaklarını noktalı virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="f72d7-323">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="f72d7-324">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="f72d7-324">RestorePackagesPath</span></span> | <span data-ttu-id="f72d7-325">Kullanıcı paketleri klasör yolu.</span><span class="sxs-lookup"><span data-stu-id="f72d7-325">User packages folder path.</span></span> |
| <span data-ttu-id="f72d7-326">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="f72d7-326">RestoreDisableParallel</span></span> | <span data-ttu-id="f72d7-327">Bir seferde bir sınır indirir.</span><span class="sxs-lookup"><span data-stu-id="f72d7-327">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="f72d7-328">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="f72d7-328">RestoreConfigFile</span></span> | <span data-ttu-id="f72d7-329">Yol için bir `Nuget.Config` uygulamak için dosya.</span><span class="sxs-lookup"><span data-stu-id="f72d7-329">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="f72d7-330">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="f72d7-330">RestoreNoCache</span></span> | <span data-ttu-id="f72d7-331">TRUE ise, önbelleğe alınan paketler kullanarak önler.</span><span class="sxs-lookup"><span data-stu-id="f72d7-331">If true, avoids using cached packages.</span></span> <span data-ttu-id="f72d7-332">Bkz: [genel paketleri ve önbellek klasör yönetimi](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="f72d7-332">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="f72d7-333">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="f72d7-333">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="f72d7-334">TRUE ise, başarısız olan veya eksik paket kaynaklarını yok sayar.</span><span class="sxs-lookup"><span data-stu-id="f72d7-334">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="f72d7-335">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="f72d7-335">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="f72d7-336">Yolu `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="f72d7-336">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="f72d7-337">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="f72d7-337">RestoreGraphProjectInput</span></span> | <span data-ttu-id="f72d7-338">Mutlak yollar içermesi gereken geri yüklemek için projeleri noktalı virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="f72d7-338">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="f72d7-339">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="f72d7-339">RestoreOutputPath</span></span> | <span data-ttu-id="f72d7-340">Çıkış klasörüne varsayarak, `obj` klasörü.</span><span class="sxs-lookup"><span data-stu-id="f72d7-340">Output folder, defaulting to the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="f72d7-341">Örnekler</span><span class="sxs-lookup"><span data-stu-id="f72d7-341">Examples</span></span>

<span data-ttu-id="f72d7-342">Komut satırı:</span><span class="sxs-lookup"><span data-stu-id="f72d7-342">Command line:</span></span>

```cli
msbuild /t:restore /p:RestoreConfigFile=<path>
```

<span data-ttu-id="f72d7-343">Proje dosyası:</span><span class="sxs-lookup"><span data-stu-id="f72d7-343">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
<PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="f72d7-344">Çıkış geri yükleme</span><span class="sxs-lookup"><span data-stu-id="f72d7-344">Restore outputs</span></span>

<span data-ttu-id="f72d7-345">Geri yükleme yapı aşağıdaki dosyaları oluşturur `obj` klasörü:</span><span class="sxs-lookup"><span data-stu-id="f72d7-345">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="f72d7-346">Dosya</span><span class="sxs-lookup"><span data-stu-id="f72d7-346">File</span></span> | <span data-ttu-id="f72d7-347">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f72d7-347">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="f72d7-348">Tüm paket referanslarını bağımlılık grafiğinin içerir.</span><span class="sxs-lookup"><span data-stu-id="f72d7-348">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="f72d7-349">MSBuild özellik paketlerinde bulunan başvurular</span><span class="sxs-lookup"><span data-stu-id="f72d7-349">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="f72d7-350">MSBuild hedefleri paketlerinde bulunan başvurular</span><span class="sxs-lookup"><span data-stu-id="f72d7-350">References to MSBuild targets contained in packages</span></span> |

### <a name="packagetargetfallback"></a><span data-ttu-id="f72d7-351">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="f72d7-351">PackageTargetFallback</span></span>

<span data-ttu-id="f72d7-352">`PackageTargetFallback` Öğesi paketleri geri yüklenirken kullanılacak uyumlu hedefleri kümesi belirtmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="f72d7-352">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="f72d7-353">Bir dotnet kullanmak paketleri izin vermek için tasarlanmış [TxM](../reference/target-frameworks.md) dotnet TxM bildirmeyin uyumlu paketlerle çalışmak için.</span><span class="sxs-lookup"><span data-stu-id="f72d7-353">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="f72d7-354">Projeniz TxM dotnet kullanıyorsa, eklediğiniz sürece diğer bir deyişle, daha sonra bağlı olduğu gereken üzerinde de tüm paketler dotnet TxM, olması `<PackageTargetFallback>` dotnet ile uyumlu olacak şekilde dotnet olmayan platformları izin vermek üzere projenize.</span><span class="sxs-lookup"><span data-stu-id="f72d7-354">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="f72d7-355">Proje kullanıyorsa, örneğin, `netstandard1.6` TxM ve bağımlı paketi içeren yalnızca `lib/net45/a.dll` ve `lib/portable-net45+win81/a.dll`, projeyi oluşturmak başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="f72d7-355">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="f72d7-356">Getirileceğini istediğiniz ikinci DLL'dir sonra ekleyebileceğiniz bir `PackageTargetFallback` gibi söylemek için `portable-net45+win81` DLL uyumludur:</span><span class="sxs-lookup"><span data-stu-id="f72d7-356">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="f72d7-357">Projenizdeki tüm hedefler için bir geri dönüş bildirmek için devre dışı bırakın `Condition` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f72d7-357">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="f72d7-358">Var olan genişletebilirsiniz `PackageTargetFallback` ekleyerek `$(PackageTargetFallback)` aşağıda gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="f72d7-358">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="f72d7-359">Bir geri yükleme grafik bir kitaplıktan değiştirme</span><span class="sxs-lookup"><span data-stu-id="f72d7-359">Replacing one library from a restore graph</span></span>

<span data-ttu-id="f72d7-360">Bir geri yükleme yanlış derleme getiren, paketleri seçim varsayılan ve kendi seçimi ile değiştir dışlamak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="f72d7-360">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="f72d7-361">Üst düzey ile ilk `PackageReference`, tüm varlıklar çıkar:</span><span class="sxs-lookup"><span data-stu-id="f72d7-361">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
    <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="f72d7-362">Ardından, DLL uygun yerel kopyasını kendi başvuru ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f72d7-362">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
