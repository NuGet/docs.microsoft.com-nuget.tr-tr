---
title: NuGet paketi ve MSBuild hedefleri olarak geri yükleme
description: NuGet paketi ve geri yükleme, MSBuild hedefleri NuGet 4.0 + ile doğrudan olarak çalışabilir.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 07296ce5a9ba85d68eca5f4915d6efea00dc8980
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548878"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="95cb0-103">NuGet paketi ve MSBuild hedefleri olarak geri yükleme</span><span class="sxs-lookup"><span data-stu-id="95cb0-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="95cb0-104">*NuGet 4.0 +*</span><span class="sxs-lookup"><span data-stu-id="95cb0-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="95cb0-105">PackageReference biçimiyle tüm bildirim meta verileri doğrudan içinde bir proje dosyası yerine ayrı bir NuGet 4.0 + depolayabilirsiniz `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="95cb0-105">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="95cb0-106">MSBuild ile 15.1 +, NuGet ile birinci sınıf bir MSBuild Vatandaşlık Ayrıca, `pack` ve `restore` aşağıda açıklandığı gibi hedefler.</span><span class="sxs-lookup"><span data-stu-id="95cb0-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="95cb0-107">Bu hedefler, başka MSBuild görevi veya hedef ile olduğu gibi NuGet ile çalışmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="95cb0-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="95cb0-108">(İçin NuGet 3.x ve daha önce kullandığınız [paketi](../tools/cli-ref-pack.md) ve [geri](../tools/cli-ref-restore.md) yerine aracılığıyla NuGet CLI komutları.)</span><span class="sxs-lookup"><span data-stu-id="95cb0-108">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="95cb0-109">Hedef derleme sırası</span><span class="sxs-lookup"><span data-stu-id="95cb0-109">Target build order</span></span>

<span data-ttu-id="95cb0-110">Çünkü `pack` ve `restore` MSBuild hedefleri olan iş akışınızı geliştirmek için erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95cb0-110">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="95cb0-111">Örneğin, paketinizin bir ağ paylaşımına paketleme sonra kopyalamak istediğiniz varsayalım.</span><span class="sxs-lookup"><span data-stu-id="95cb0-111">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="95cb0-112">Proje dosyanızda aşağıdaki ekleyerek bunu yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="95cb0-112">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="95cb0-113">Benzer şekilde, bir MSBuild görevi yazabilir, kendi hedefleyin ve MSBuild görevindeki NuGet özelliklerini kullanma.</span><span class="sxs-lookup"><span data-stu-id="95cb0-113">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="95cb0-114">paketi hedef</span><span class="sxs-lookup"><span data-stu-id="95cb0-114">pack target</span></span>

<span data-ttu-id="95cb0-115">PackageReference biçimini kullanarak, kullanarak .NET Standard projeleri için `msbuild /t:pack` bir NuGet paketi oluşturmak için Proje dosyasındaki girişleri çizer.</span><span class="sxs-lookup"><span data-stu-id="95cb0-115">For .NET Standard projects using the PackageReference format, using `msbuild /t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="95cb0-116">Aşağıdaki tabloda, bir proje dosyası birinci içinde eklenebilir MSBuild özellikleri tanımlar `<PropertyGroup>` düğümü.</span><span class="sxs-lookup"><span data-stu-id="95cb0-116">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="95cb0-117">Bu düzenlemeler kolayca Visual Studio 2017'de ve daha sonra projeyi sağ tıklayıp tarafından yapabileceğiniz **{project_name} Düzenle** bağlam menüsünde.</span><span class="sxs-lookup"><span data-stu-id="95cb0-117">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="95cb0-118">Kolaylık olması için tablo eşdeğer özelliği tarafından düzenlenir bir [ `.nuspec` dosya](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="95cb0-118">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="95cb0-119">Unutmayın `Owners` ve `Summary` özelliklerinden `.nuspec` MSBuild ile desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="95cb0-119">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="95cb0-120">Öznitelik/NuSpec değeri</span><span class="sxs-lookup"><span data-stu-id="95cb0-120">Attribute/NuSpec Value</span></span> | <span data-ttu-id="95cb0-121">MSBuild özelliği</span><span class="sxs-lookup"><span data-stu-id="95cb0-121">MSBuild Property</span></span> | <span data-ttu-id="95cb0-122">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="95cb0-122">Default</span></span> | <span data-ttu-id="95cb0-123">Notlar</span><span class="sxs-lookup"><span data-stu-id="95cb0-123">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="95cb0-124">Kimliği</span><span class="sxs-lookup"><span data-stu-id="95cb0-124">Id</span></span> | <span data-ttu-id="95cb0-125">PackageId</span><span class="sxs-lookup"><span data-stu-id="95cb0-125">PackageId</span></span> | <span data-ttu-id="95cb0-126">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="95cb0-126">AssemblyName</span></span> | <span data-ttu-id="95cb0-127">MSBuild gelen $(AssemblyName)</span><span class="sxs-lookup"><span data-stu-id="95cb0-127">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="95cb0-128">Sürüm</span><span class="sxs-lookup"><span data-stu-id="95cb0-128">Version</span></span> | <span data-ttu-id="95cb0-129">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="95cb0-129">PackageVersion</span></span> | <span data-ttu-id="95cb0-130">Sürüm</span><span class="sxs-lookup"><span data-stu-id="95cb0-130">Version</span></span> | <span data-ttu-id="95cb0-131">Bu örnek "1.0.0", "1.0.0-beta" veya "1.0.0-beta-00345" uyumlu semver</span><span class="sxs-lookup"><span data-stu-id="95cb0-131">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="95cb0-132">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="95cb0-132">VersionPrefix</span></span> | <span data-ttu-id="95cb0-133">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="95cb0-133">PackageVersionPrefix</span></span> | <span data-ttu-id="95cb0-134">empty</span><span class="sxs-lookup"><span data-stu-id="95cb0-134">empty</span></span> | <span data-ttu-id="95cb0-135">PackageVersionPrefix PackageVersion ayarını geçersiz kılar</span><span class="sxs-lookup"><span data-stu-id="95cb0-135">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="95cb0-136">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="95cb0-136">VersionSuffix</span></span> | <span data-ttu-id="95cb0-137">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="95cb0-137">PackageVersionSuffix</span></span> | <span data-ttu-id="95cb0-138">empty</span><span class="sxs-lookup"><span data-stu-id="95cb0-138">empty</span></span> | <span data-ttu-id="95cb0-139">MSBuild gelen $(VersionSuffix).</span><span class="sxs-lookup"><span data-stu-id="95cb0-139">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="95cb0-140">PackageVersionSuffix PackageVersion ayarını geçersiz kılar</span><span class="sxs-lookup"><span data-stu-id="95cb0-140">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="95cb0-141">Yazarlar</span><span class="sxs-lookup"><span data-stu-id="95cb0-141">Authors</span></span> | <span data-ttu-id="95cb0-142">Yazarlar</span><span class="sxs-lookup"><span data-stu-id="95cb0-142">Authors</span></span> | <span data-ttu-id="95cb0-143">Geçerli kullanıcının kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="95cb0-143">Username of the current user</span></span> | |
| <span data-ttu-id="95cb0-144">Sahipleri</span><span class="sxs-lookup"><span data-stu-id="95cb0-144">Owners</span></span> | <span data-ttu-id="95cb0-145">Yok</span><span class="sxs-lookup"><span data-stu-id="95cb0-145">N/A</span></span> | <span data-ttu-id="95cb0-146">Sınıflandırmalarına yok</span><span class="sxs-lookup"><span data-stu-id="95cb0-146">Not present in NuSpec</span></span> | |
| <span data-ttu-id="95cb0-147">Başlık</span><span class="sxs-lookup"><span data-stu-id="95cb0-147">Title</span></span> | <span data-ttu-id="95cb0-148">Başlık</span><span class="sxs-lookup"><span data-stu-id="95cb0-148">Title</span></span> | <span data-ttu-id="95cb0-149">PackageId</span><span class="sxs-lookup"><span data-stu-id="95cb0-149">The PackageId</span></span>| |
| <span data-ttu-id="95cb0-150">Açıklama</span><span class="sxs-lookup"><span data-stu-id="95cb0-150">Description</span></span> | <span data-ttu-id="95cb0-151">Açıklama</span><span class="sxs-lookup"><span data-stu-id="95cb0-151">Description</span></span> | <span data-ttu-id="95cb0-152">"Paketi"</span><span class="sxs-lookup"><span data-stu-id="95cb0-152">"Package Description"</span></span> | |
| <span data-ttu-id="95cb0-153">Telif Hakkı</span><span class="sxs-lookup"><span data-stu-id="95cb0-153">Copyright</span></span> | <span data-ttu-id="95cb0-154">Telif Hakkı</span><span class="sxs-lookup"><span data-stu-id="95cb0-154">Copyright</span></span> | <span data-ttu-id="95cb0-155">empty</span><span class="sxs-lookup"><span data-stu-id="95cb0-155">empty</span></span> | |
| <span data-ttu-id="95cb0-156">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="95cb0-156">RequireLicenseAcceptance</span></span> | <span data-ttu-id="95cb0-157">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="95cb0-157">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="95cb0-158">false</span><span class="sxs-lookup"><span data-stu-id="95cb0-158">false</span></span> | |
| <span data-ttu-id="95cb0-159">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="95cb0-159">LicenseUrl</span></span> | <span data-ttu-id="95cb0-160">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="95cb0-160">PackageLicenseUrl</span></span> | <span data-ttu-id="95cb0-161">empty</span><span class="sxs-lookup"><span data-stu-id="95cb0-161">empty</span></span> | |
| <span data-ttu-id="95cb0-162">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="95cb0-162">ProjectUrl</span></span> | <span data-ttu-id="95cb0-163">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="95cb0-163">PackageProjectUrl</span></span> | <span data-ttu-id="95cb0-164">empty</span><span class="sxs-lookup"><span data-stu-id="95cb0-164">empty</span></span> | |
| <span data-ttu-id="95cb0-165">IconUrl</span><span class="sxs-lookup"><span data-stu-id="95cb0-165">IconUrl</span></span> | <span data-ttu-id="95cb0-166">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="95cb0-166">PackageIconUrl</span></span> | <span data-ttu-id="95cb0-167">empty</span><span class="sxs-lookup"><span data-stu-id="95cb0-167">empty</span></span> | |
| <span data-ttu-id="95cb0-168">Etiketler</span><span class="sxs-lookup"><span data-stu-id="95cb0-168">Tags</span></span> | <span data-ttu-id="95cb0-169">PackageTags</span><span class="sxs-lookup"><span data-stu-id="95cb0-169">PackageTags</span></span> | <span data-ttu-id="95cb0-170">empty</span><span class="sxs-lookup"><span data-stu-id="95cb0-170">empty</span></span> | <span data-ttu-id="95cb0-171">Etiketleri noktalı virgülle ayrılmış olan.</span><span class="sxs-lookup"><span data-stu-id="95cb0-171">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="95cb0-172">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="95cb0-172">ReleaseNotes</span></span> | <span data-ttu-id="95cb0-173">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="95cb0-173">PackageReleaseNotes</span></span> | <span data-ttu-id="95cb0-174">empty</span><span class="sxs-lookup"><span data-stu-id="95cb0-174">empty</span></span> | |
| <span data-ttu-id="95cb0-175">Depo/URL'si</span><span class="sxs-lookup"><span data-stu-id="95cb0-175">Repository/Url</span></span> | <span data-ttu-id="95cb0-176">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="95cb0-176">RepositoryUrl</span></span> | <span data-ttu-id="95cb0-177">empty</span><span class="sxs-lookup"><span data-stu-id="95cb0-177">empty</span></span> | <span data-ttu-id="95cb0-178">Kopyalayın veya kaynak kodu almak için kullanılan depo URL'si.</span><span class="sxs-lookup"><span data-stu-id="95cb0-178">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="95cb0-179">Örnek: *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="95cb0-179">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="95cb0-180">Depo/türü</span><span class="sxs-lookup"><span data-stu-id="95cb0-180">Repository/Type</span></span> | <span data-ttu-id="95cb0-181">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="95cb0-181">RepositoryType</span></span> | <span data-ttu-id="95cb0-182">empty</span><span class="sxs-lookup"><span data-stu-id="95cb0-182">empty</span></span> | <span data-ttu-id="95cb0-183">Depo türü.</span><span class="sxs-lookup"><span data-stu-id="95cb0-183">Repository type.</span></span> <span data-ttu-id="95cb0-184">Örnekler: *git*, *tfs*.</span><span class="sxs-lookup"><span data-stu-id="95cb0-184">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="95cb0-185">Depo/dal</span><span class="sxs-lookup"><span data-stu-id="95cb0-185">Repository/Branch</span></span> | <span data-ttu-id="95cb0-186">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="95cb0-186">RepositoryBranch</span></span> | <span data-ttu-id="95cb0-187">empty</span><span class="sxs-lookup"><span data-stu-id="95cb0-187">empty</span></span> | <span data-ttu-id="95cb0-188">İsteğe bağlı bir depo dalı bilgileri.</span><span class="sxs-lookup"><span data-stu-id="95cb0-188">Optional repository branch information.</span></span> <span data-ttu-id="95cb0-189">*RepositoryUrl* dahil edilmek üzere bu özellik için de belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="95cb0-189">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="95cb0-190">Örnek: *ana* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="95cb0-190">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="95cb0-191">Depo/yürütme</span><span class="sxs-lookup"><span data-stu-id="95cb0-191">Repository/Commit</span></span> | <span data-ttu-id="95cb0-192">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="95cb0-192">RepositoryCommit</span></span> | <span data-ttu-id="95cb0-193">empty</span><span class="sxs-lookup"><span data-stu-id="95cb0-193">empty</span></span> | <span data-ttu-id="95cb0-194">İsteğe bağlı depo işleme veya değişiklik kümesi, paket kaynak belirtmek için karşı hazırlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="95cb0-194">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="95cb0-195">*RepositoryUrl* dahil edilmek üzere bu özellik için de belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="95cb0-195">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="95cb0-196">Örnek: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="95cb0-196">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="95cb0-197">PackageType</span><span class="sxs-lookup"><span data-stu-id="95cb0-197">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="95cb0-198">Özet</span><span class="sxs-lookup"><span data-stu-id="95cb0-198">Summary</span></span> | <span data-ttu-id="95cb0-199">Desteklenmez</span><span class="sxs-lookup"><span data-stu-id="95cb0-199">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="95cb0-200">paketi hedef girişleri</span><span class="sxs-lookup"><span data-stu-id="95cb0-200">pack target inputs</span></span>

- <span data-ttu-id="95cb0-201">IsPackable</span><span class="sxs-lookup"><span data-stu-id="95cb0-201">IsPackable</span></span>
- <span data-ttu-id="95cb0-202">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="95cb0-202">PackageVersion</span></span>
- <span data-ttu-id="95cb0-203">PackageId</span><span class="sxs-lookup"><span data-stu-id="95cb0-203">PackageId</span></span>
- <span data-ttu-id="95cb0-204">Yazarlar</span><span class="sxs-lookup"><span data-stu-id="95cb0-204">Authors</span></span>
- <span data-ttu-id="95cb0-205">Açıklama</span><span class="sxs-lookup"><span data-stu-id="95cb0-205">Description</span></span>
- <span data-ttu-id="95cb0-206">Telif Hakkı</span><span class="sxs-lookup"><span data-stu-id="95cb0-206">Copyright</span></span>
- <span data-ttu-id="95cb0-207">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="95cb0-207">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="95cb0-208">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="95cb0-208">DevelopmentDependency</span></span>
- <span data-ttu-id="95cb0-209">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="95cb0-209">PackageLicenseUrl</span></span>
- <span data-ttu-id="95cb0-210">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="95cb0-210">PackageProjectUrl</span></span>
- <span data-ttu-id="95cb0-211">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="95cb0-211">PackageIconUrl</span></span>
- <span data-ttu-id="95cb0-212">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="95cb0-212">PackageReleaseNotes</span></span>
- <span data-ttu-id="95cb0-213">PackageTags</span><span class="sxs-lookup"><span data-stu-id="95cb0-213">PackageTags</span></span>
- <span data-ttu-id="95cb0-214">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="95cb0-214">PackageOutputPath</span></span>
- <span data-ttu-id="95cb0-215">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="95cb0-215">IncludeSymbols</span></span>
- <span data-ttu-id="95cb0-216">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="95cb0-216">IncludeSource</span></span>
- <span data-ttu-id="95cb0-217">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="95cb0-217">PackageTypes</span></span>
- <span data-ttu-id="95cb0-218">IsTool</span><span class="sxs-lookup"><span data-stu-id="95cb0-218">IsTool</span></span>
- <span data-ttu-id="95cb0-219">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="95cb0-219">RepositoryUrl</span></span>
- <span data-ttu-id="95cb0-220">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="95cb0-220">RepositoryType</span></span>
- <span data-ttu-id="95cb0-221">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="95cb0-221">RepositoryBranch</span></span>
- <span data-ttu-id="95cb0-222">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="95cb0-222">RepositoryCommit</span></span>
- <span data-ttu-id="95cb0-223">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="95cb0-223">NoPackageAnalysis</span></span>
- <span data-ttu-id="95cb0-224">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="95cb0-224">MinClientVersion</span></span>
- <span data-ttu-id="95cb0-225">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="95cb0-225">IncludeBuildOutput</span></span>
- <span data-ttu-id="95cb0-226">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="95cb0-226">IncludeContentInPack</span></span>
- <span data-ttu-id="95cb0-227">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="95cb0-227">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="95cb0-228">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="95cb0-228">ContentTargetFolders</span></span>
- <span data-ttu-id="95cb0-229">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="95cb0-229">NuspecFile</span></span>
- <span data-ttu-id="95cb0-230">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="95cb0-230">NuspecBasePath</span></span>
- <span data-ttu-id="95cb0-231">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="95cb0-231">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="95cb0-232">Paketi senaryoları</span><span class="sxs-lookup"><span data-stu-id="95cb0-232">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="95cb0-233">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="95cb0-233">PackageIconUrl</span></span>

<span data-ttu-id="95cb0-234">Değişikliğin parçası olarak [NuGet sorunu 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` sonunda değiştirilecek `PackageIconUri` ve sonuçta elde edilen paketin kökünde dahil bir simge dosyası için göreli yol olabilir.</span><span class="sxs-lookup"><span data-stu-id="95cb0-234">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="95cb0-235">Çıkış bütünleştirilmiş kodları</span><span class="sxs-lookup"><span data-stu-id="95cb0-235">Output assemblies</span></span>

<span data-ttu-id="95cb0-236">`nuget pack` kopya çıkış uzantılara sahip dosyalar `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, ve `.pri`.</span><span class="sxs-lookup"><span data-stu-id="95cb0-236">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="95cb0-237">Kopyalanan çıkış dosyalarının ne MSBuild sağlıyor üzerinde bağımlı `BuiltOutputProjectGroup` hedef.</span><span class="sxs-lookup"><span data-stu-id="95cb0-237">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="95cb0-238">Çıkış derlemeleri nereye proje dosyası veya komut satırı denetimi için kullanabileceğiniz iki MSBuild özellikleri vardır:</span><span class="sxs-lookup"><span data-stu-id="95cb0-238">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="95cb0-239">`IncludeBuildOutput`: Yapı çıkış derlemeleri pakete dahil edilip edilmeyeceğini belirler bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="95cb0-239">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="95cb0-240">`BuildOutputTargetFolder`: Çıkış bütünleştirilmiş kodları yerleştirilmelidir klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="95cb0-240">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="95cb0-241">Çıkış bütünleştirilmiş kodları (ve diğer çıktı dosyalarının) ilgili framework klasörlerine kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="95cb0-241">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="95cb0-242">Paket başvuruları</span><span class="sxs-lookup"><span data-stu-id="95cb0-242">Package references</span></span>

<span data-ttu-id="95cb0-243">Bkz: [paket başvuruları proje dosyalarındaki](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="95cb0-243">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="95cb0-244">Proje Proje başvurular</span><span class="sxs-lookup"><span data-stu-id="95cb0-244">Project to project references</span></span>

<span data-ttu-id="95cb0-245">Proje başvuruları projeye değerlendirilir varsayılan nuget paket başvuruları, örneğin:</span><span class="sxs-lookup"><span data-stu-id="95cb0-245">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="95cb0-246">Ayrıca aşağıdaki meta verileri, proje başvurusu eklenebilir mi:</span><span class="sxs-lookup"><span data-stu-id="95cb0-246">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="95cb0-247">Bir içerik paketine</span><span class="sxs-lookup"><span data-stu-id="95cb0-247">Including content in a package</span></span>

<span data-ttu-id="95cb0-248">İçerik dahil etmek varolan fazladan meta verileri ekleme `<Content>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="95cb0-248">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="95cb0-249">Varsayılan olarak her şeyi girişlerle yazmadığınız sürece "İçerik" paketinde türü ister aşağıdakiler:</span><span class="sxs-lookup"><span data-stu-id="95cb0-249">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="95cb0-250">Varsayılan olarak, her şeyi köküne eklenen `content` ve `contentFiles\any\<target_framework>` klasördeki bir paket ve korur göreli klasör yapısı, bir paket yolu belirtmediğiniz sürece:</span><span class="sxs-lookup"><span data-stu-id="95cb0-250">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="95cb0-251">Klasörleri yalnızca belirli için tüm içeriğinizi kopyalamak istiyorsanız kök (yerine `content` ve `contentFiles` her ikisi de), MSBuild özelliğini kullanabilirsiniz `ContentTargetFolders`, varsayılan olarak "içerik; contentFiles" ancak herhangi bir klasör adı için ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="95cb0-251">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="95cb0-252">Not, yalnızca "contentFiles" belirterek `ContentTargetFolders` altındaki dosyaları yerleştirir `contentFiles\any\<target_framework>` veya `contentFiles\<language>\<target_framework>` göre `buildAction`.</span><span class="sxs-lookup"><span data-stu-id="95cb0-252">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="95cb0-253">`PackagePath` hedef yolları noktalı virgül ile ayrılmış bir dizi olabilir.</span><span class="sxs-lookup"><span data-stu-id="95cb0-253">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="95cb0-254">Bir boş paket yolu belirterek dosya paket köküne eklersiniz.</span><span class="sxs-lookup"><span data-stu-id="95cb0-254">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="95cb0-255">Örneğin, aşağıdaki ekler `libuv.txt` için `content\myfiles`, `content\samples`ve paket kök:</span><span class="sxs-lookup"><span data-stu-id="95cb0-255">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="95cb0-256">Bir MSBuild özelliği de mevcuttur `$(IncludeContentInPack)`, bunun varsayılan `true`.</span><span class="sxs-lookup"><span data-stu-id="95cb0-256">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="95cb0-257">Bu ayarlanırsa `false` hiçbir projede, ardından bu projeye ait içeriği dahil değildir nuget paketinin.</span><span class="sxs-lookup"><span data-stu-id="95cb0-257">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="95cb0-258">Yukarıdaki öğelerden birini ayarlayabilirsiniz diğer paketi belirli meta veriler içeren ```<PackageCopyToOutput>``` ve ```<PackageFlatten>``` hangi kümeleri ```CopyToOutput``` ve ```Flatten``` üzerinde değerleri ```contentFiles``` çıkış nuspec girişi.</span><span class="sxs-lookup"><span data-stu-id="95cb0-258">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="95cb0-259">İçerik öğeleri dışında `<Pack>` ve `<PackagePath>` meta verileri de ayarlanabilir derleme, EmbeddedResource, ApplicationDefinition, sayfa, kaynak, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes derleme eylemiyle dosyaları , CodeAnalysisDictionary AndroidAsset, AndroidResource, BundleResource veya yok.</span><span class="sxs-lookup"><span data-stu-id="95cb0-259">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="95cb0-260">Glob desenlerinin kullanırken paket yolunuza dosya eklemek paketi için paket yolu, dosya adı dahil olmak üzere tam yolu kabul edilir klasör ayırıcı karakteri ile aksi takdirde, paket yolu bitmelidir.</span><span class="sxs-lookup"><span data-stu-id="95cb0-260">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="95cb0-261">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="95cb0-261">IncludeSymbols</span></span>

<span data-ttu-id="95cb0-262">Kullanırken `MSBuild /t:pack /p:IncludeSymbols=true`, karşılık gelen `.pdb` dosyaların yanı sıra diğer çıktı dosyalarının kopyalandığından (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="95cb0-262">When using `MSBuild /t:pack /p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="95cb0-263">Bu ayarı Not `IncludeSymbols=true` normal bir paket oluşturan *ve* bir sembol paketi.</span><span class="sxs-lookup"><span data-stu-id="95cb0-263">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="95cb0-264">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="95cb0-264">IncludeSource</span></span>

<span data-ttu-id="95cb0-265">Aynı budur `IncludeSymbols`dışında kaynak dosyaları ile birlikte kopyalar `.pdb` dosyalar.</span><span class="sxs-lookup"><span data-stu-id="95cb0-265">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="95cb0-266">Tüm dosya türü `Compile` üzerinden kopyalanır `src\<ProjectName>\` sonuç paketine göreli yol klasör yapısında korur.</span><span class="sxs-lookup"><span data-stu-id="95cb0-266">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="95cb0-267">Aynı kaynak dosyaları herhangi da yapılır `ProjectReference` olduğu `TreatAsPackageReference` kümesine `false`.</span><span class="sxs-lookup"><span data-stu-id="95cb0-267">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="95cb0-268">Dosya türü ile derleme yaparsanız, proje klasörünün dışında olduğu için yeni eklenen sonra `src\<ProjectName>\`.</span><span class="sxs-lookup"><span data-stu-id="95cb0-268">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="istool"></a><span data-ttu-id="95cb0-269">IsTool</span><span class="sxs-lookup"><span data-stu-id="95cb0-269">IsTool</span></span>

<span data-ttu-id="95cb0-270">Kullanırken `MSBuild /t:pack /p:IsTool=true`, tüm çıktı dosyaları, belirtilen [çıkış derlemeleri](#output-assemblies) senaryosu, kopyalanır `tools` klasörü yerine `lib` klasör.</span><span class="sxs-lookup"><span data-stu-id="95cb0-270">When using `MSBuild /t:pack /p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="95cb0-271">Bu farklı olduğunu unutmayın bir `DotNetCliTool` , belirtilen ayarlayarak `PackageType` içinde `.csproj` dosya.</span><span class="sxs-lookup"><span data-stu-id="95cb0-271">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="95cb0-272">Bir .nuspec kullanarak paketleme</span><span class="sxs-lookup"><span data-stu-id="95cb0-272">Packing using a .nuspec</span></span>

<span data-ttu-id="95cb0-273">Kullanabileceğiniz bir `.nuspec` projenize SDK proje dosyasını içeri aktarmak için sahip olması koşuluyla paketlemek için dosya `NuGet.Build.Tasks.Pack.targets` böylece paketi görevi yürütülebilir.</span><span class="sxs-lookup"><span data-stu-id="95cb0-273">You can use a `.nuspec` file to pack your project provided that you have a SDK project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="95cb0-274">Yine de soubor nuspec paketi önce projeyi geri yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="95cb0-274">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="95cb0-275">Hedef Çerçeve proje dosyasının ilgisizdir ve paket bir nuspec iletişim kurulurken kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="95cb0-275">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="95cb0-276">Aşağıdaki üç MSBuild özellikleri kullanarak paket için uygun olan bir `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="95cb0-276">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="95cb0-277">`NuspecFile`: göreli veya mutlak yolunu `.nuspec` paketleme için kullanılan dosya.</span><span class="sxs-lookup"><span data-stu-id="95cb0-277">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="95cb0-278">`NuspecProperties`: noktalı virgülle ayrılmış listesini anahtar = değer çiftleri.</span><span class="sxs-lookup"><span data-stu-id="95cb0-278">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="95cb0-279">MSBuild komut satırı Ayrıştırmada works yöntemi nedeniyle birden çok özellikleri şu şekilde belirtilmelidir: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="95cb0-279">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="95cb0-280">`NuspecBasePath`: Temel yolunu `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="95cb0-280">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="95cb0-281">Kullanıyorsanız `dotnet.exe` projenizi paketlemek için aşağıdakine benzer bir komut kullanın:</span><span class="sxs-lookup"><span data-stu-id="95cb0-281">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="95cb0-282">MSBuild proje paketi için kullanılıyorsa, aşağıdakine benzer bir komut kullanın:</span><span class="sxs-lookup"><span data-stu-id="95cb0-282">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="95cb0-283">Paket bir nuspec dotnet.exe veya msbuild'ı kullanarak da varsayılan olarak proje oluşturmak için müşteri adayları olduğunu lütfen unutmayın.</span><span class="sxs-lookup"><span data-stu-id="95cb0-283">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="95cb0-284">Bu geçirerek önlenebilir ```--no-build``` ayarı denk olan dotnet.exe özelliğini ```<NoBuild>true</NoBuild> ``` ayarı ile birlikte proje dosyanızda ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` proje dosyasındaki</span><span class="sxs-lookup"><span data-stu-id="95cb0-284">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file</span></span>

<span data-ttu-id="95cb0-285">Soubor nuspec paketlenecek csproj dosyasının bir örnektir:</span><span class="sxs-lookup"><span data-stu-id="95cb0-285">An example of a csproj file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="95cb0-286">Gelişmiş özelleştirilmiş paketi oluşturmak için uzantı noktaları</span><span class="sxs-lookup"><span data-stu-id="95cb0-286">Advanced extension points to create customized package</span></span>

<span data-ttu-id="95cb0-287">`pack` Hedef iç, hedef framework belirli derlemede çalıştırılan iki uzantı noktaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="95cb0-287">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="95cb0-288">Belirli içerik hedef framework ve derlemeleri pakete dahil olmak üzere genişletme noktaları destekler:</span><span class="sxs-lookup"><span data-stu-id="95cb0-288">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="95cb0-289">`TargetsForTfmSpecificBuildOutput` Hedef: içindeki dosyaları kullanıma `lib` klasör veya kullanılarak belirtilen bir klasör `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="95cb0-289">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="95cb0-290">`TargetsForTfmSpecificContentInPackage` Hedef: dışındaki dosyalara kullanılmak `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="95cb0-290">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="95cb0-291">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="95cb0-291">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="95cb0-292">Özel bir hedefleyin ve değeri olarak belirtin `$(TargetsForTfmSpecificBuildOutput)` özelliği.</span><span class="sxs-lookup"><span data-stu-id="95cb0-292">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="95cb0-293">Gitmesi gereken tüm dosyalara `BuildOutputTargetFolder` (LIB) varsayılan olarak hedef dosyaları ItemGroup yazmanız gerekir `BuildOutputInPackage` aşağıdaki iki meta veri değerleri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="95cb0-293">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="95cb0-294">`FinalOutputPath`: Dosyanın mutlak yolu; sağlanmazsa, kimlik kaynak yolu değerlendirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="95cb0-294">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="95cb0-295">`TargetPath`: (İsteğe bağlı) dosyası içinde bir alt kısımlarda gerektiğinde ayarlamak `lib\<TargetFramework>` derlemeleri ilgili kültür klasörlerine altında ötesine uydu gibi.</span><span class="sxs-lookup"><span data-stu-id="95cb0-295">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="95cb0-296">Varsayılan ayar dosyasının adı.</span><span class="sxs-lookup"><span data-stu-id="95cb0-296">Defaults to the name of the file.</span></span>

<span data-ttu-id="95cb0-297">Örnek:</span><span class="sxs-lookup"><span data-stu-id="95cb0-297">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="95cb0-298">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="95cb0-298">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="95cb0-299">Özel bir hedefleyin ve değeri olarak belirtin `$(TargetsForTfmSpecificContentInPackage)` özelliği.</span><span class="sxs-lookup"><span data-stu-id="95cb0-299">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="95cb0-300">Tüm dosyalar paket içerisine dâhil etmek, hedef dosyaları ItemGroup yazmanız gerekir `TfmSpecificPackageFile` ve aşağıdaki isteğe bağlı meta verileri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="95cb0-300">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="95cb0-301">`PackagePath`: Yol dosya paketinde çıkış burada olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="95cb0-301">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="95cb0-302">Birden fazla dosya aynı paket yolu eklediyseniz NuGet bir uyarı verir.</span><span class="sxs-lookup"><span data-stu-id="95cb0-302">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="95cb0-303">`BuildAction`: Paket yolu ise dosyaya atamak için derleme eylemi yalnızca gerekli `contentFiles` klasör.</span><span class="sxs-lookup"><span data-stu-id="95cb0-303">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="95cb0-304">Varsayılan olarak "None".</span><span class="sxs-lookup"><span data-stu-id="95cb0-304">Defaults to "None".</span></span>

<span data-ttu-id="95cb0-305">Örnek:</span><span class="sxs-lookup"><span data-stu-id="95cb0-305">An example:</span></span>
```xml
<PropertyGroup>
  <TargetsForTfmSpecificContentInPackage>$(TargetsForTfmSpecificContentInPackage);CustomContentTarget</TargetsForTfmSpecificContentInPackage>
</PropertyGroup>

<Target Name="CustomContentTarget">
  <ItemGroup>
    <TfmSpecificPackageFile Include="abc.txt">
      <PackagePath>mycontent/$(TargetFramework)</PackagePath>
    </TfmSpecificPackageFile>
    <TfmSpecificPackageFile Include="Extensions/ext.txt" Condition="'$(TargetFramework)' == 'net46'">
      <PackagePath>net46content</PackagePath>
    </TfmSpecificPackageFile>  
  </ItemGroup>
</Target>  
```

## <a name="restore-target"></a><span data-ttu-id="95cb0-306">geri yükleme hedefi</span><span class="sxs-lookup"><span data-stu-id="95cb0-306">restore target</span></span>

<span data-ttu-id="95cb0-307">`MSBuild /t:restore` (hangi `nuget restore` ve `dotnet restore` .NET Core projeleriyle kullanın), aşağıdaki gibi proje dosyasında başvurulan paketleri geri yükler:</span><span class="sxs-lookup"><span data-stu-id="95cb0-307">`MSBuild /t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="95cb0-308">Tüm projeden projeye başvurular okuyun</span><span class="sxs-lookup"><span data-stu-id="95cb0-308">Read all project to project references</span></span>
1. <span data-ttu-id="95cb0-309">Ara klasörü ve hedef çerçeveleri bulmak için proje özellikleri okuma</span><span class="sxs-lookup"><span data-stu-id="95cb0-309">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="95cb0-310">NuGet.Build.Tasks.dll msbuild veri geçişi</span><span class="sxs-lookup"><span data-stu-id="95cb0-310">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="95cb0-311">Geri yükleme</span><span class="sxs-lookup"><span data-stu-id="95cb0-311">Run restore</span></span>
1. <span data-ttu-id="95cb0-312">Paketleri indirin</span><span class="sxs-lookup"><span data-stu-id="95cb0-312">Download packages</span></span>
1. <span data-ttu-id="95cb0-313">Varlıklar dosyasını, hedef ve Özellikler Yaz</span><span class="sxs-lookup"><span data-stu-id="95cb0-313">Write assets file, targets, and props</span></span>

<span data-ttu-id="95cb0-314">`restore` Hedef works **yalnızca** PackageReference biçimini kullanan projeler için.</span><span class="sxs-lookup"><span data-stu-id="95cb0-314">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="95cb0-315">Mevcut **değil** kullanarak projeleri için iş `packages.config` biçimini; kullanma [nuget geri yükleme](../tools/cli-ref-restore.md) yerine.</span><span class="sxs-lookup"><span data-stu-id="95cb0-315">It does **not** work for projects using the `packages.config` format; use [nuget restore](../tools/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="95cb0-316">Özellikler geri yükleme</span><span class="sxs-lookup"><span data-stu-id="95cb0-316">Restore properties</span></span>

<span data-ttu-id="95cb0-317">Ek geri yükleme ayarlarını MSBuild proje dosyası özelliklerinde gelir.</span><span class="sxs-lookup"><span data-stu-id="95cb0-317">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="95cb0-318">Değerleri de ayarlanabilir kullanılarak komut satırından `/p:` geçiş (aşağıdaki örneklere bakın).</span><span class="sxs-lookup"><span data-stu-id="95cb0-318">Values can also be set from the command line using the `/p:` switch (see Examples below).</span></span>

| <span data-ttu-id="95cb0-319">Özellik</span><span class="sxs-lookup"><span data-stu-id="95cb0-319">Property</span></span> | <span data-ttu-id="95cb0-320">Açıklama</span><span class="sxs-lookup"><span data-stu-id="95cb0-320">Description</span></span> |
|--------|--------|
| <span data-ttu-id="95cb0-321">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="95cb0-321">RestoreSources</span></span> | <span data-ttu-id="95cb0-322">Noktalı virgül ile ayrılmış paket kaynaklarının listesi.</span><span class="sxs-lookup"><span data-stu-id="95cb0-322">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="95cb0-323">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="95cb0-323">RestorePackagesPath</span></span> | <span data-ttu-id="95cb0-324">Kullanıcı paketleri klasör yolu.</span><span class="sxs-lookup"><span data-stu-id="95cb0-324">User packages folder path.</span></span> |
| <span data-ttu-id="95cb0-325">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="95cb0-325">RestoreDisableParallel</span></span> | <span data-ttu-id="95cb0-326">Bir kerede sınırı indirir.</span><span class="sxs-lookup"><span data-stu-id="95cb0-326">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="95cb0-327">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="95cb0-327">RestoreConfigFile</span></span> | <span data-ttu-id="95cb0-328">Yol için bir `Nuget.Config` uygulamak için dosya.</span><span class="sxs-lookup"><span data-stu-id="95cb0-328">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="95cb0-329">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="95cb0-329">RestoreNoCache</span></span> | <span data-ttu-id="95cb0-330">TRUE ise, önbelleğe eklenen paketler kullanılmasını önlemiş olursunuz.</span><span class="sxs-lookup"><span data-stu-id="95cb0-330">If true, avoids using cached packages.</span></span> <span data-ttu-id="95cb0-331">Bkz: [genel paketleri ve önbellek klasörlerini yönetme](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="95cb0-331">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="95cb0-332">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="95cb0-332">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="95cb0-333">TRUE ise, başarısız veya eksik paket kaynaklarını yok sayar.</span><span class="sxs-lookup"><span data-stu-id="95cb0-333">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="95cb0-334">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="95cb0-334">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="95cb0-335">Yolu `NuGet.Build.Tasks.dll`.</span><span class="sxs-lookup"><span data-stu-id="95cb0-335">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="95cb0-336">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="95cb0-336">RestoreGraphProjectInput</span></span> | <span data-ttu-id="95cb0-337">Noktalı virgül ile ayrılmış mutlak yollar içermelidir geri yüklemek için projeler listesi.</span><span class="sxs-lookup"><span data-stu-id="95cb0-337">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="95cb0-338">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="95cb0-338">RestoreOutputPath</span></span> | <span data-ttu-id="95cb0-339">Varsayarak, çıkış dosyasının `obj` klasör.</span><span class="sxs-lookup"><span data-stu-id="95cb0-339">Output folder, defaulting to the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="95cb0-340">Örnekler</span><span class="sxs-lookup"><span data-stu-id="95cb0-340">Examples</span></span>

<span data-ttu-id="95cb0-341">Komut satırı:</span><span class="sxs-lookup"><span data-stu-id="95cb0-341">Command line:</span></span>

```cli
msbuild /t:restore /p:RestoreConfigFile=<path>
```

<span data-ttu-id="95cb0-342">Proje dosyası:</span><span class="sxs-lookup"><span data-stu-id="95cb0-342">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="95cb0-343">Çıktıları geri yükleme</span><span class="sxs-lookup"><span data-stu-id="95cb0-343">Restore outputs</span></span>

<span data-ttu-id="95cb0-344">Geri yükleme, yapı aşağıdaki dosyaları oluşturur `obj` klasörü:</span><span class="sxs-lookup"><span data-stu-id="95cb0-344">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="95cb0-345">Dosya</span><span class="sxs-lookup"><span data-stu-id="95cb0-345">File</span></span> | <span data-ttu-id="95cb0-346">Açıklama</span><span class="sxs-lookup"><span data-stu-id="95cb0-346">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="95cb0-347">Tüm paket başvuruları bağımlılık grafiği içerir.</span><span class="sxs-lookup"><span data-stu-id="95cb0-347">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="95cb0-348">MSBuild özellikler paketlerde yer alan başvuruları</span><span class="sxs-lookup"><span data-stu-id="95cb0-348">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="95cb0-349">MSBuild hedefleri paketlerde yer alan başvuruları</span><span class="sxs-lookup"><span data-stu-id="95cb0-349">References to MSBuild targets contained in packages</span></span> |

### <a name="packagetargetfallback"></a><span data-ttu-id="95cb0-350">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="95cb0-350">PackageTargetFallback</span></span>

<span data-ttu-id="95cb0-351">`PackageTargetFallback` Öğesi, bir dizi paketler geri yüklenirken kullanılacak uyumlu hedefleri belirtmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="95cb0-351">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="95cb0-352">Bir dotnet kullanan paketleri izin vermek için tasarlanmış [TxM](../reference/target-frameworks.md) bir dotnet TxM bildirmeyin uyumlu paketlerle çalışmak için.</span><span class="sxs-lookup"><span data-stu-id="95cb0-352">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="95cb0-353">Projenizin kullandığı dotnet TxM eklediğiniz sürece diğer bir deyişle, ardından bu bağlıdır üzerinde gerekir ayrıca tüm paketleri bir dotnet TxM, varsa `<PackageTargetFallback>` dotnet ile uyumlu olacak şekilde dotnet olmayan platformlar için projenize.</span><span class="sxs-lookup"><span data-stu-id="95cb0-353">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="95cb0-354">Örneğin, proje kullanıyorsanız `netstandard1.6` TxM ve bağımlı paketi içeren yalnızca `lib/net45/a.dll` ve `lib/portable-net45+win81/a.dll`, Proje yapı başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="95cb0-354">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="95cb0-355">Almak istediğiniz ikinci alan DLL'dir sonra ekleyebileceğiniz bir `PackageTargetFallback` şu şekilde söylemek `portable-net45+win81` DLL uyumludur:</span><span class="sxs-lookup"><span data-stu-id="95cb0-355">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="95cb0-356">Bir geri dönüş için projenizdeki tüm hedefleri bildirmek üzere bırakın `Condition` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="95cb0-356">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="95cb0-357">Ayrıca var olan tüm genişletebilirsiniz `PackageTargetFallback` ekleyerek `$(PackageTargetFallback)` burada gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="95cb0-357">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="95cb0-358">Bir geri yükleme grafik bir kitaplıktan değiştirme</span><span class="sxs-lookup"><span data-stu-id="95cb0-358">Replacing one library from a restore graph</span></span>

<span data-ttu-id="95cb0-359">Bir geri yükleme, yanlış derleme getiriyor, tutma paketleri istediğiniz varsayılan ve kendi yönteminizi değiştirmek mümkündür.</span><span class="sxs-lookup"><span data-stu-id="95cb0-359">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="95cb0-360">Üst düzey ile ilk `PackageReference`, tüm varlıkları dışla:</span><span class="sxs-lookup"><span data-stu-id="95cb0-360">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="95cb0-361">Ardından, DLL uygun yerel kopyasını kendi başvuru ekleyin:</span><span class="sxs-lookup"><span data-stu-id="95cb0-361">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
