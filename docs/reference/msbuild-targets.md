---
title: NuGet paketi ve geri yükleme MSBuild hedefleri olarak
description: NuGet paketi ve geri yükleme, NuGet 4.0 + ile doğrudan MSBuild hedefleri olarak çalışabilir.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 8403ae38b5d2e907c6f06b162a18cdcd5425565b
ms.sourcegitcommit: 5aa49478dc466c67db5c3edda7c6ce8dcd8ae033
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2019
ms.locfileid: "68817528"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="525bf-103">NuGet paketi ve geri yükleme MSBuild hedefleri olarak</span><span class="sxs-lookup"><span data-stu-id="525bf-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="525bf-104">*NuGet 4.0 +*</span><span class="sxs-lookup"><span data-stu-id="525bf-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="525bf-105">[Packagereference](../consume-packages/package-references-in-project-files.md) biçimi sayesinde, NuGet 4.0 + tüm bildirim meta verilerini ayrı `.nuspec` bir dosya kullanmak yerine doğrudan proje dosyası içinde depolayabilirler.</span><span class="sxs-lookup"><span data-stu-id="525bf-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="525bf-106">MSBuild 15.1 + ile NuGet, aşağıda açıklandığı gibi, `pack` ve `restore` hedefleri ile birinci sınıf MSBuild vatandaşlık da vardır.</span><span class="sxs-lookup"><span data-stu-id="525bf-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="525bf-107">Bu hedefler, diğer herhangi bir MSBuild görevi veya hedefi ile yaptığınız gibi NuGet ile çalışmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="525bf-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="525bf-108">MSBuild kullanarak bir NuGet paketi oluşturma yönergeleri için bkz. [MSBuild kullanarak NuGet paketi oluşturma](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="525bf-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="525bf-109">(NuGet 3. x ve öncesi için, bunun yerine NuGet CLı aracılığıyla [paketle](../reference/cli-reference/cli-ref-pack.md) ve [geri yükleme](../reference/cli-reference/cli-ref-restore.md) komutlarını kullanırsınız.)</span><span class="sxs-lookup"><span data-stu-id="525bf-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="525bf-110">Hedef derleme sırası</span><span class="sxs-lookup"><span data-stu-id="525bf-110">Target build order</span></span>

<span data-ttu-id="525bf-111">`pack` Ve`restore` MSBuild hedefleri olduğundan, iş akışınızı geliştirmek için bunlara erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="525bf-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="525bf-112">Örneğin, paketledikten sonra paketinizi bir ağ paylaşımında kopyalamak istediğinizi varsayalım.</span><span class="sxs-lookup"><span data-stu-id="525bf-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="525bf-113">Bunu, proje dosyanıza aşağıdakileri ekleyerek yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="525bf-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="525bf-114">Benzer şekilde, MSBuild görevinde bir MSBuild görevi yazabilir, kendi hedefini yazabilir ve NuGet özelliklerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="525bf-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="525bf-115">paket hedefi</span><span class="sxs-lookup"><span data-stu-id="525bf-115">pack target</span></span>

<span data-ttu-id="525bf-116">Packagereference biçimini kullanan .NET Standard projeler için, `msbuild -t:pack` bir NuGet paketi oluştururken kullanılacak proje dosyasından girişler çizer.</span><span class="sxs-lookup"><span data-stu-id="525bf-116">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="525bf-117">Aşağıdaki tabloda, ilk `<PropertyGroup>` düğüm içindeki bir proje dosyasına eklenebilen MSBuild özellikleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="525bf-117">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="525bf-118">Projeyi sağ tıklayıp bağlam menüsünde **{Project_Name} Düzenle** ' yi seçerek Visual Studio 2017 ve sonraki sürümlerde bu düzenlemeleri kolayca yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="525bf-118">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="525bf-119">Kolaylık olması için tablo, bir [ `.nuspec` dosyadaki](../reference/nuspec.md)denk özelliğe göre düzenlenir.</span><span class="sxs-lookup"><span data-stu-id="525bf-119">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="525bf-120">`Owners` Ve özelliklerininMSBuild`.nuspec`iledesteklenmediğiniunutmayın. `Summary`</span><span class="sxs-lookup"><span data-stu-id="525bf-120">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="525bf-121">Öznitelik/NuSpec değeri</span><span class="sxs-lookup"><span data-stu-id="525bf-121">Attribute/NuSpec Value</span></span> | <span data-ttu-id="525bf-122">MSBuild özelliği</span><span class="sxs-lookup"><span data-stu-id="525bf-122">MSBuild Property</span></span> | <span data-ttu-id="525bf-123">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="525bf-123">Default</span></span> | <span data-ttu-id="525bf-124">Notlar</span><span class="sxs-lookup"><span data-stu-id="525bf-124">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="525bf-125">Id</span><span class="sxs-lookup"><span data-stu-id="525bf-125">Id</span></span> | <span data-ttu-id="525bf-126">PackageId</span><span class="sxs-lookup"><span data-stu-id="525bf-126">PackageId</span></span> | <span data-ttu-id="525bf-127">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="525bf-127">AssemblyName</span></span> | <span data-ttu-id="525bf-128">MSBuild 'ten $ (AssemblyName)</span><span class="sxs-lookup"><span data-stu-id="525bf-128">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="525bf-129">Sürüm</span><span class="sxs-lookup"><span data-stu-id="525bf-129">Version</span></span> | <span data-ttu-id="525bf-130">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="525bf-130">PackageVersion</span></span> | <span data-ttu-id="525bf-131">Sürüm</span><span class="sxs-lookup"><span data-stu-id="525bf-131">Version</span></span> | <span data-ttu-id="525bf-132">Bu semver uyumludur, örneğin "1.0.0", "1.0.0-Beta" veya "1.0.0-Beta-00345"</span><span class="sxs-lookup"><span data-stu-id="525bf-132">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="525bf-133">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="525bf-133">VersionPrefix</span></span> | <span data-ttu-id="525bf-134">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="525bf-134">PackageVersionPrefix</span></span> | <span data-ttu-id="525bf-135">empty</span><span class="sxs-lookup"><span data-stu-id="525bf-135">empty</span></span> | <span data-ttu-id="525bf-136">PackageVersion ayarı PackageVersionPrefix üzerine yazıyor</span><span class="sxs-lookup"><span data-stu-id="525bf-136">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="525bf-137">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="525bf-137">VersionSuffix</span></span> | <span data-ttu-id="525bf-138">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="525bf-138">PackageVersionSuffix</span></span> | <span data-ttu-id="525bf-139">empty</span><span class="sxs-lookup"><span data-stu-id="525bf-139">empty</span></span> | <span data-ttu-id="525bf-140">MSBuild 'ten $ (VersionSuffix).</span><span class="sxs-lookup"><span data-stu-id="525bf-140">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="525bf-141">PackageVersion ayarı PackageVersionSuffix üzerine yazıyor</span><span class="sxs-lookup"><span data-stu-id="525bf-141">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="525bf-142">Yazarlar</span><span class="sxs-lookup"><span data-stu-id="525bf-142">Authors</span></span> | <span data-ttu-id="525bf-143">Yazarlar</span><span class="sxs-lookup"><span data-stu-id="525bf-143">Authors</span></span> | <span data-ttu-id="525bf-144">Geçerli kullanıcının Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="525bf-144">Username of the current user</span></span> | |
| <span data-ttu-id="525bf-145">Lere</span><span class="sxs-lookup"><span data-stu-id="525bf-145">Owners</span></span> | <span data-ttu-id="525bf-146">Yok</span><span class="sxs-lookup"><span data-stu-id="525bf-146">N/A</span></span> | <span data-ttu-id="525bf-147">NuSpec içinde yok</span><span class="sxs-lookup"><span data-stu-id="525bf-147">Not present in NuSpec</span></span> | |
| <span data-ttu-id="525bf-148">Başlık</span><span class="sxs-lookup"><span data-stu-id="525bf-148">Title</span></span> | <span data-ttu-id="525bf-149">Başlık</span><span class="sxs-lookup"><span data-stu-id="525bf-149">Title</span></span> | <span data-ttu-id="525bf-150">PackageID</span><span class="sxs-lookup"><span data-stu-id="525bf-150">The PackageId</span></span>| |
| <span data-ttu-id="525bf-151">Açıklama</span><span class="sxs-lookup"><span data-stu-id="525bf-151">Description</span></span> | <span data-ttu-id="525bf-152">Açıklama</span><span class="sxs-lookup"><span data-stu-id="525bf-152">Description</span></span> | <span data-ttu-id="525bf-153">"Paket açıklaması"</span><span class="sxs-lookup"><span data-stu-id="525bf-153">"Package Description"</span></span> | |
| <span data-ttu-id="525bf-154">Yaptırımlar</span><span class="sxs-lookup"><span data-stu-id="525bf-154">Copyright</span></span> | <span data-ttu-id="525bf-155">Yaptırımlar</span><span class="sxs-lookup"><span data-stu-id="525bf-155">Copyright</span></span> | <span data-ttu-id="525bf-156">empty</span><span class="sxs-lookup"><span data-stu-id="525bf-156">empty</span></span> | |
| <span data-ttu-id="525bf-157">Requirelicensekabulünü</span><span class="sxs-lookup"><span data-stu-id="525bf-157">RequireLicenseAcceptance</span></span> | <span data-ttu-id="525bf-158">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="525bf-158">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="525bf-159">false</span><span class="sxs-lookup"><span data-stu-id="525bf-159">false</span></span> | |
| <span data-ttu-id="525bf-160">lisan</span><span class="sxs-lookup"><span data-stu-id="525bf-160">license</span></span> | <span data-ttu-id="525bf-161">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="525bf-161">PackageLicenseExpression</span></span> | <span data-ttu-id="525bf-162">empty</span><span class="sxs-lookup"><span data-stu-id="525bf-162">empty</span></span> | <span data-ttu-id="525bf-163">Karşılık gelen`<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="525bf-163">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="525bf-164">lisan</span><span class="sxs-lookup"><span data-stu-id="525bf-164">license</span></span> | <span data-ttu-id="525bf-165">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="525bf-165">PackageLicenseFile</span></span> | <span data-ttu-id="525bf-166">empty</span><span class="sxs-lookup"><span data-stu-id="525bf-166">empty</span></span> | <span data-ttu-id="525bf-167">Öğesine `<license type="file">`karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="525bf-167">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="525bf-168">Başvurulan lisans dosyasını açık bir şekilde paketetmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="525bf-168">You may need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="525bf-169">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="525bf-169">LicenseUrl</span></span> | <span data-ttu-id="525bf-170">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="525bf-170">PackageLicenseUrl</span></span> | <span data-ttu-id="525bf-171">empty</span><span class="sxs-lookup"><span data-stu-id="525bf-171">empty</span></span> | <span data-ttu-id="525bf-172">`licenseUrl`kullanım dışı bırakılıyor, PackageLicenseExpression veya PackageLicenseFile özelliğini kullanın</span><span class="sxs-lookup"><span data-stu-id="525bf-172">`licenseUrl` is being deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="525bf-173">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="525bf-173">ProjectUrl</span></span> | <span data-ttu-id="525bf-174">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="525bf-174">PackageProjectUrl</span></span> | <span data-ttu-id="525bf-175">empty</span><span class="sxs-lookup"><span data-stu-id="525bf-175">empty</span></span> | |
| <span data-ttu-id="525bf-176">IconUrl</span><span class="sxs-lookup"><span data-stu-id="525bf-176">IconUrl</span></span> | <span data-ttu-id="525bf-177">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="525bf-177">PackageIconUrl</span></span> | <span data-ttu-id="525bf-178">empty</span><span class="sxs-lookup"><span data-stu-id="525bf-178">empty</span></span> | |
| <span data-ttu-id="525bf-179">Etiketler</span><span class="sxs-lookup"><span data-stu-id="525bf-179">Tags</span></span> | <span data-ttu-id="525bf-180">PackageTags</span><span class="sxs-lookup"><span data-stu-id="525bf-180">PackageTags</span></span> | <span data-ttu-id="525bf-181">empty</span><span class="sxs-lookup"><span data-stu-id="525bf-181">empty</span></span> | <span data-ttu-id="525bf-182">Etiketler noktalı virgülle ayrılır.</span><span class="sxs-lookup"><span data-stu-id="525bf-182">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="525bf-183">Relet 'ler</span><span class="sxs-lookup"><span data-stu-id="525bf-183">ReleaseNotes</span></span> | <span data-ttu-id="525bf-184">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="525bf-184">PackageReleaseNotes</span></span> | <span data-ttu-id="525bf-185">empty</span><span class="sxs-lookup"><span data-stu-id="525bf-185">empty</span></span> | |
| <span data-ttu-id="525bf-186">Depo/URL</span><span class="sxs-lookup"><span data-stu-id="525bf-186">Repository/Url</span></span> | <span data-ttu-id="525bf-187">Depourl 'Si</span><span class="sxs-lookup"><span data-stu-id="525bf-187">RepositoryUrl</span></span> | <span data-ttu-id="525bf-188">empty</span><span class="sxs-lookup"><span data-stu-id="525bf-188">empty</span></span> | <span data-ttu-id="525bf-189">Kaynak kodu kopyalamak veya almak için kullanılan depo URL 'SI.</span><span class="sxs-lookup"><span data-stu-id="525bf-189">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="525bf-190">Örneğinde *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="525bf-190">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="525bf-191">Depo/tür</span><span class="sxs-lookup"><span data-stu-id="525bf-191">Repository/Type</span></span> | <span data-ttu-id="525bf-192">Repositorytype parametrelerinin sağlanması</span><span class="sxs-lookup"><span data-stu-id="525bf-192">RepositoryType</span></span> | <span data-ttu-id="525bf-193">empty</span><span class="sxs-lookup"><span data-stu-id="525bf-193">empty</span></span> | <span data-ttu-id="525bf-194">Depo türü.</span><span class="sxs-lookup"><span data-stu-id="525bf-194">Repository type.</span></span> <span data-ttu-id="525bf-195">Örnekler: *Git*, *TFS*.</span><span class="sxs-lookup"><span data-stu-id="525bf-195">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="525bf-196">Depo/dal</span><span class="sxs-lookup"><span data-stu-id="525bf-196">Repository/Branch</span></span> | <span data-ttu-id="525bf-197">Depodalı</span><span class="sxs-lookup"><span data-stu-id="525bf-197">RepositoryBranch</span></span> | <span data-ttu-id="525bf-198">empty</span><span class="sxs-lookup"><span data-stu-id="525bf-198">empty</span></span> | <span data-ttu-id="525bf-199">İsteğe bağlı depo dalı bilgileri.</span><span class="sxs-lookup"><span data-stu-id="525bf-199">Optional repository branch information.</span></span> <span data-ttu-id="525bf-200">Bu özelliğin dahil olması için aynı zamanda bir *Depo-URL* belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="525bf-200">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="525bf-201">Örnek: *Master* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="525bf-201">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="525bf-202">Depo/kayıt</span><span class="sxs-lookup"><span data-stu-id="525bf-202">Repository/Commit</span></span> | <span data-ttu-id="525bf-203">Kayıt yapma</span><span class="sxs-lookup"><span data-stu-id="525bf-203">RepositoryCommit</span></span> | <span data-ttu-id="525bf-204">empty</span><span class="sxs-lookup"><span data-stu-id="525bf-204">empty</span></span> | <span data-ttu-id="525bf-205">Paketin hangi kaynağa göre oluşturulduğunu göstermek için isteğe bağlı depo kaydı veya değişiklik kümesi.</span><span class="sxs-lookup"><span data-stu-id="525bf-205">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="525bf-206">Bu özelliğin dahil olması için aynı zamanda bir *Depo-URL* belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="525bf-206">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="525bf-207">Örnek: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="525bf-207">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="525bf-208">PackageType</span><span class="sxs-lookup"><span data-stu-id="525bf-208">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="525bf-209">Özet</span><span class="sxs-lookup"><span data-stu-id="525bf-209">Summary</span></span> | <span data-ttu-id="525bf-210">Desteklenmez</span><span class="sxs-lookup"><span data-stu-id="525bf-210">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="525bf-211">Paket hedef girişleri</span><span class="sxs-lookup"><span data-stu-id="525bf-211">pack target inputs</span></span>

- <span data-ttu-id="525bf-212">Ispackable</span><span class="sxs-lookup"><span data-stu-id="525bf-212">IsPackable</span></span>
- <span data-ttu-id="525bf-213">Suppressbağımlıcıeswhenpaketleme</span><span class="sxs-lookup"><span data-stu-id="525bf-213">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="525bf-214">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="525bf-214">PackageVersion</span></span>
- <span data-ttu-id="525bf-215">PackageId</span><span class="sxs-lookup"><span data-stu-id="525bf-215">PackageId</span></span>
- <span data-ttu-id="525bf-216">Yazarlar</span><span class="sxs-lookup"><span data-stu-id="525bf-216">Authors</span></span>
- <span data-ttu-id="525bf-217">Açıklama</span><span class="sxs-lookup"><span data-stu-id="525bf-217">Description</span></span>
- <span data-ttu-id="525bf-218">Yaptırımlar</span><span class="sxs-lookup"><span data-stu-id="525bf-218">Copyright</span></span>
- <span data-ttu-id="525bf-219">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="525bf-219">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="525bf-220">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="525bf-220">DevelopmentDependency</span></span>
- <span data-ttu-id="525bf-221">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="525bf-221">PackageLicenseExpression</span></span>
- <span data-ttu-id="525bf-222">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="525bf-222">PackageLicenseFile</span></span>
- <span data-ttu-id="525bf-223">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="525bf-223">PackageLicenseUrl</span></span>
- <span data-ttu-id="525bf-224">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="525bf-224">PackageProjectUrl</span></span>
- <span data-ttu-id="525bf-225">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="525bf-225">PackageIconUrl</span></span>
- <span data-ttu-id="525bf-226">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="525bf-226">PackageReleaseNotes</span></span>
- <span data-ttu-id="525bf-227">PackageTags</span><span class="sxs-lookup"><span data-stu-id="525bf-227">PackageTags</span></span>
- <span data-ttu-id="525bf-228">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="525bf-228">PackageOutputPath</span></span>
- <span data-ttu-id="525bf-229">Includesymbols</span><span class="sxs-lookup"><span data-stu-id="525bf-229">IncludeSymbols</span></span>
- <span data-ttu-id="525bf-230">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="525bf-230">IncludeSource</span></span>
- <span data-ttu-id="525bf-231">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="525bf-231">PackageTypes</span></span>
- <span data-ttu-id="525bf-232">IsTool</span><span class="sxs-lookup"><span data-stu-id="525bf-232">IsTool</span></span>
- <span data-ttu-id="525bf-233">Depourl 'Si</span><span class="sxs-lookup"><span data-stu-id="525bf-233">RepositoryUrl</span></span>
- <span data-ttu-id="525bf-234">Repositorytype parametrelerinin sağlanması</span><span class="sxs-lookup"><span data-stu-id="525bf-234">RepositoryType</span></span>
- <span data-ttu-id="525bf-235">Depodalı</span><span class="sxs-lookup"><span data-stu-id="525bf-235">RepositoryBranch</span></span>
- <span data-ttu-id="525bf-236">Kayıt yapma</span><span class="sxs-lookup"><span data-stu-id="525bf-236">RepositoryCommit</span></span>
- <span data-ttu-id="525bf-237">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="525bf-237">NoPackageAnalysis</span></span>
- <span data-ttu-id="525bf-238">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="525bf-238">MinClientVersion</span></span>
- <span data-ttu-id="525bf-239">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="525bf-239">IncludeBuildOutput</span></span>
- <span data-ttu-id="525bf-240">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="525bf-240">IncludeContentInPack</span></span>
- <span data-ttu-id="525bf-241">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="525bf-241">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="525bf-242">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="525bf-242">ContentTargetFolders</span></span>
- <span data-ttu-id="525bf-243">Nusguus dosyası</span><span class="sxs-lookup"><span data-stu-id="525bf-243">NuspecFile</span></span>
- <span data-ttu-id="525bf-244">Nusgubasepath</span><span class="sxs-lookup"><span data-stu-id="525bf-244">NuspecBasePath</span></span>
- <span data-ttu-id="525bf-245">Nus, Properties</span><span class="sxs-lookup"><span data-stu-id="525bf-245">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="525bf-246">paket senaryoları</span><span class="sxs-lookup"><span data-stu-id="525bf-246">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="525bf-247">Bağımlılıkları gösterme</span><span class="sxs-lookup"><span data-stu-id="525bf-247">Suppress dependencies</span></span>

<span data-ttu-id="525bf-248">Oluşturulan NuGet paketinden paket bağımlılıklarını bastırmak için, olarak `SuppressDependenciesWhenPacking` `true` ayarlayın ve oluşturulan nupkg dosyasından tüm bağımlılıkların atlanmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="525bf-248">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="525bf-249">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="525bf-249">PackageIconUrl</span></span>

<span data-ttu-id="525bf-250">[NuGet sorunu 352](https://github.com/NuGet/Home/issues/352)değişikliğinin bir parçası olarak, `PackageIconUrl` sonunda olarak `PackageIconUri` değiştirilir ve sonuç paketinin köküne dahil edilecek bir simge dosyasının göreli yolu olabilir.</span><span class="sxs-lookup"><span data-stu-id="525bf-250">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="525bf-251">Çıkış derlemeleri</span><span class="sxs-lookup"><span data-stu-id="525bf-251">Output assemblies</span></span>

<span data-ttu-id="525bf-252">`nuget pack`çıktı dosyalarını,,, `.exe`, `.dll`ve `.xml` `.winmd` uzantılarınakopyalar`.json`. `.pri`</span><span class="sxs-lookup"><span data-stu-id="525bf-252">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="525bf-253">Kopyalanan çıkış dosyaları, `BuiltOutputProjectGroup` hedef tarafından MSBuild 'in sağladığı şuna bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="525bf-253">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="525bf-254">Çıktı derlemelerinin nerede olduğunu denetlemek için, proje dosyanızda veya komut satırında kullanabileceğiniz iki MSBuild özelliği vardır:</span><span class="sxs-lookup"><span data-stu-id="525bf-254">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="525bf-255">`IncludeBuildOutput`: Derleme çıkış derlemelerinin pakete dahil edilip edilmeyeceğini belirleyen bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="525bf-255">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="525bf-256">`BuildOutputTargetFolder`: Çıkış derlemelerinin yerleştirilmesi gereken klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="525bf-256">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="525bf-257">Çıkış derlemeleri (ve diğer çıkış dosyaları) ilgili çerçeve klasörlerine kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="525bf-257">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="525bf-258">Paket başvuruları</span><span class="sxs-lookup"><span data-stu-id="525bf-258">Package references</span></span>

<span data-ttu-id="525bf-259">Bkz. [Proje dosyalarındaki paket başvuruları](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="525bf-259">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="525bf-260">Projeden projeye başvurular</span><span class="sxs-lookup"><span data-stu-id="525bf-260">Project to project references</span></span>

<span data-ttu-id="525bf-261">Proje başvuruları, varsayılan olarak NuGet paket başvuruları olarak değerlendirilir, örneğin:</span><span class="sxs-lookup"><span data-stu-id="525bf-261">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="525bf-262">Ayrıca, proje başvurunuz için aşağıdaki meta verileri de ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="525bf-262">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="525bf-263">Bir paketteki içerik ekleme</span><span class="sxs-lookup"><span data-stu-id="525bf-263">Including content in a package</span></span>

<span data-ttu-id="525bf-264">İçerik eklemek için var olan `<Content>` öğeye ek meta veriler ekleyin.</span><span class="sxs-lookup"><span data-stu-id="525bf-264">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="525bf-265">Varsayılan olarak, aşağıdaki gibi girdilerle geçersiz kılmadığınız müddetçe "Içerik" türünde her şey pakete dahil edilir:</span><span class="sxs-lookup"><span data-stu-id="525bf-265">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="525bf-266">Varsayılan olarak, her şey bir paket içindeki `content` ve `contentFiles\any\<target_framework>` klasörünün köküne eklenir ve bir paket yolu belirtmediğiniz takdirde göreli klasör yapısını korur:</span><span class="sxs-lookup"><span data-stu-id="525bf-266">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="525bf-267">Tüm içeriğinizi yalnızca belirli bir kök klasöre ( `content` ve `contentFiles` her ikisi yerine) kopyalamak istiyorsanız, varsayılan olarak "Content; ContentFiles" olan, ancak başka bir klasör `ContentTargetFolders`adına ayarlanabilir MSBuild özelliğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="525bf-267">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="525bf-268">Yalnızca dosyaları ' ın `ContentTargetFolders` altında veya `contentFiles\<language>\<target_framework>` temel alarak `buildAction`"ContentFiles" `contentFiles\any\<target_framework>` seçeneğinin belirtildiğine unutmayın.</span><span class="sxs-lookup"><span data-stu-id="525bf-268">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="525bf-269">`PackagePath`noktalı virgülle ayrılmış bir hedef yolları kümesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="525bf-269">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="525bf-270">Boş bir paket yolu belirtilmesi, dosyayı paketin köküne ekler.</span><span class="sxs-lookup"><span data-stu-id="525bf-270">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="525bf-271">Örneğin, aşağıdaki, ve paket `libuv.txt` köküne `content\myfiles`ekler `content\samples`:</span><span class="sxs-lookup"><span data-stu-id="525bf-271">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="525bf-272">Ayrıca, varsayılan olarak `$(IncludeContentInPack)` `true`olan MSBuild özelliği de vardır.</span><span class="sxs-lookup"><span data-stu-id="525bf-272">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="525bf-273">Bu, herhangi bir projede `false` olarak ayarlandıysa, bu projeden içerik NuGet paketine dahil edilmez.</span><span class="sxs-lookup"><span data-stu-id="525bf-273">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="525bf-274">Yukarıdaki öğelerin herhangi birine ayarlayabileceğiniz diğer paketine özgü meta veriler içerir ```<PackageCopyToOutput>``` ve ```<PackageFlatten>``` çıkış nuspec içindeki ```contentFiles``` giriş ```CopyToOutput``` üzerinde ```Flatten``` ve değerlerini belirler.</span><span class="sxs-lookup"><span data-stu-id="525bf-274">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="525bf-275">İçerik öğelerinden ayrı olarak `<Pack>` , ve `<PackagePath>` meta veriler de derleme, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, designdata, designdatawithdesigntimecreateabletypes derleme eylemine sahip dosyalarda ayarlanabilir , CodeAnalysisDictionary, AndroidAsset, AndroidResource, paketleme Leresource veya None.</span><span class="sxs-lookup"><span data-stu-id="525bf-275">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="525bf-276">Glob desenleri kullanılırken dosya adını paket yolunuza eklemek için paket yolu, klasör ayırıcı karakteriyle bitmelidir; Aksi takdirde, paket yolu dosya adı dahil tam yol olarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="525bf-276">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="525bf-277">Includesymbols</span><span class="sxs-lookup"><span data-stu-id="525bf-277">IncludeSymbols</span></span>

<span data-ttu-id="525bf-278">`MSBuild -t:pack -p:IncludeSymbols=true`Kullanırken, karşılık gelen`.dll` `.winmd` `.pri` dosyalardiğer`.json`çıkış dosyalarıylabirlikte`.exe`kopyalanır (,,, ,,).`.xml` `.pdb`</span><span class="sxs-lookup"><span data-stu-id="525bf-278">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="525bf-279">Ayarın `IncludeSymbols=true` düzenli bir paket *ve* bir semboller paketi oluşturduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="525bf-279">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="525bf-280">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="525bf-280">IncludeSource</span></span>

<span data-ttu-id="525bf-281">Bu, ile `IncludeSymbols` `.pdb` aynıdır, ancak kaynak dosyalarını da dosyalarla birlikte kopyalar.</span><span class="sxs-lookup"><span data-stu-id="525bf-281">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="525bf-282">Tüm dosya türleri `Compile` , elde edilen paketteki göreli `src\<ProjectName>\` yol klasörü yapısını korumak için üzerine kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="525bf-282">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="525bf-283">Aynı zamanda, olarak `ProjectReference` `TreatAsPackageReference` `false`ayarlanmış herhangi bir kaynak dosyası için de aynı olur.</span><span class="sxs-lookup"><span data-stu-id="525bf-283">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="525bf-284">Derleme türü bir dosya proje klasörünün dışında ise, ' ye `src\<ProjectName>\`eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="525bf-284">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="525bf-285">Lisans ifadesi veya lisans dosyası paketleme</span><span class="sxs-lookup"><span data-stu-id="525bf-285">Packing a license expression or a license file</span></span>

<span data-ttu-id="525bf-286">Bir lisans ifadesi kullanılırken PackageLicenseExpression özelliğinin kullanılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="525bf-286">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="525bf-287">[Lisans ifadesi örneği](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="525bf-287">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="525bf-288">[NuGet.org tarafından kabul edilen lisans ifadeleri ve lisanslar hakkında daha fazla bilgi edinin](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="525bf-288">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="525bf-289">Bir lisans dosyası paketleme sırasında, paketin köküne göre paket yolunu belirtmek için PackageLicenseFile özelliğini kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="525bf-289">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="525bf-290">Ayrıca, dosyanın pakete eklendiğinden emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="525bf-290">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="525bf-291">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="525bf-291">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```
<span data-ttu-id="525bf-292">[Lisans dosyası örneği](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="525bf-292">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="525bf-293">IsTool</span><span class="sxs-lookup"><span data-stu-id="525bf-293">IsTool</span></span>

<span data-ttu-id="525bf-294">Kullanırken `MSBuild -t:pack -p:IsTool=true`, [Çıkış derlemeleri](#output-assemblies) senaryosunda belirtilen tüm çıkış dosyaları, `tools` `lib` klasörü yerine klasörüne kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="525bf-294">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="525bf-295">Bunun, `DotNetCliTool` `PackageType` içindeki dosyasınıayarlayarakbelirtilenöğesindenfarklıolduğunuunutmayın.`.csproj`</span><span class="sxs-lookup"><span data-stu-id="525bf-295">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="525bf-296">. Nuspec kullanarak paketleme</span><span class="sxs-lookup"><span data-stu-id="525bf-296">Packing using a .nuspec</span></span>

<span data-ttu-id="525bf-297">Bunun yerine genellikle `.nuspec` proje dosyasındaki dosyada bulunan [tüm özellikleri eklemeniz](../reference/msbuild-targets.md#pack-target) önerilse de, projenizi paketlebilmeniz için bir `.nuspec` dosya kullanmayı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="525bf-297">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="525bf-298">Tarafından kullanılan `PackageReference`SDK olmayan bir proje için, paket görevinin yürütülebilmesi için içeri aktarmanız `NuGet.Build.Tasks.Pack.targets` gerekir.</span><span class="sxs-lookup"><span data-stu-id="525bf-298">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="525bf-299">Bir nuspec dosyası paketetmeden önce projeyi geri yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="525bf-299">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="525bf-300">(SDK stili bir proje varsayılan olarak paket hedeflerini içerir.)</span><span class="sxs-lookup"><span data-stu-id="525bf-300">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="525bf-301">Proje dosyasının hedef çerçevesi ilgisizdir ve bir nuspec paketleme sırasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="525bf-301">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="525bf-302">Aşağıdaki üç MSBuild özelliği, ile `.nuspec`paketleme ile ilgilidir:</span><span class="sxs-lookup"><span data-stu-id="525bf-302">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="525bf-303">`NuspecFile`: paketleme için kullanılan `.nuspec` dosyanın göreli veya mutlak yolu.</span><span class="sxs-lookup"><span data-stu-id="525bf-303">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="525bf-304">`NuspecProperties`: Key = değer çiftleri için noktalı virgülle ayrılmış bir liste.</span><span class="sxs-lookup"><span data-stu-id="525bf-304">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="525bf-305">MSBuild komut satırı ayrıştırması çalışma yöntemi nedeniyle, birden çok özellik şu şekilde belirtilmelidir: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="525bf-305">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="525bf-306">`NuspecBasePath`: `.nuspec` Dosya için temel yol.</span><span class="sxs-lookup"><span data-stu-id="525bf-306">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="525bf-307">Projenizi paketmek için kullanıyorsanız `dotnet.exe` , aşağıdaki gibi bir komut kullanın:</span><span class="sxs-lookup"><span data-stu-id="525bf-307">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="525bf-308">Projenizi paketmek için MSBuild kullanıyorsanız, aşağıdaki gibi bir komut kullanın:</span><span class="sxs-lookup"><span data-stu-id="525bf-308">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="525bf-309">Lütfen DotNet. exe veya MSBuild kullanarak bir nuspec paketleme, projenin varsayılan olarak oluşturulmasına da neden olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="525bf-309">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="525bf-310">Bu, proje dosyasında ayarı ```--no-build``` ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` ile birlikte proje dosyanızdaki ayarın ```<NoBuild>true</NoBuild> ``` eşdeğeri olan DotNet. exe ' ye geçirilerek kaçınılabilir.</span><span class="sxs-lookup"><span data-stu-id="525bf-310">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="525bf-311">Bir nuspec dosyası paketiçin bir *. csproj* dosyası örneği:</span><span class="sxs-lookup"><span data-stu-id="525bf-311">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="525bf-312">Özelleştirilmiş paket oluşturmak için gelişmiş uzantı noktaları</span><span class="sxs-lookup"><span data-stu-id="525bf-312">Advanced extension points to create customized package</span></span>

<span data-ttu-id="525bf-313">`pack` Hedef, iç, hedef çerçeveye özgü derlemede çalışan iki uzantı noktası sağlar.</span><span class="sxs-lookup"><span data-stu-id="525bf-313">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="525bf-314">Uzantı noktaları, hedef çerçeveye özgü içerik ve derlemelerin bir pakete dahil edilmesi için destek:</span><span class="sxs-lookup"><span data-stu-id="525bf-314">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="525bf-315">`TargetsForTfmSpecificBuildOutput`hedef `lib` Klasörü veya kullanılarak `BuildOutputTargetFolder`belirtilen bir klasörü içindeki dosyalar için kullanın.</span><span class="sxs-lookup"><span data-stu-id="525bf-315">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="525bf-316">`TargetsForTfmSpecificContentInPackage`hedef Dışındaki dosyalar için kullanın `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="525bf-316">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="525bf-317">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="525bf-317">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="525bf-318">Özel bir hedef yazın ve `$(TargetsForTfmSpecificBuildOutput)` özelliğin değeri olarak belirtin.</span><span class="sxs-lookup"><span data-stu-id="525bf-318">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="525bf-319">`BuildOutputTargetFolder` (Varsayılan olarak LIB) öğesine gitmesi gereken tüm dosyalar için, hedef bu dosyaları ItemGroup `BuildOutputInPackage` 'a yazmalıdır ve aşağıdaki iki meta veri değerini ayarlamış olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="525bf-319">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="525bf-320">`FinalOutputPath`: Dosyanın mutlak yolu; sağlanmazsa, kimlik kaynak yolunu değerlendirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="525bf-320">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="525bf-321">`TargetPath`:  Seçim Dosyanın içinde `lib\<TargetFramework>` , ilgili kültür klasörlerinin altında yer alan uydu derlemeleri gibi bir alt klasöre gitmesi gerektiğinde ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="525bf-321">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="525bf-322">Varsayılan olarak dosyanın adıdır.</span><span class="sxs-lookup"><span data-stu-id="525bf-322">Defaults to the name of the file.</span></span>

<span data-ttu-id="525bf-323">Örnek:</span><span class="sxs-lookup"><span data-stu-id="525bf-323">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="525bf-324">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="525bf-324">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="525bf-325">Özel bir hedef yazın ve `$(TargetsForTfmSpecificContentInPackage)` özelliğin değeri olarak belirtin.</span><span class="sxs-lookup"><span data-stu-id="525bf-325">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="525bf-326">Pakete dahil edilecek tüm dosyalar için, hedef bu dosyaları ItemGroup `TfmSpecificPackageFile` 'a yazmalıdır ve aşağıdaki isteğe bağlı meta verileri ayarlar:</span><span class="sxs-lookup"><span data-stu-id="525bf-326">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="525bf-327">`PackagePath`: Dosyanın pakette çıkış olması gereken yol.</span><span class="sxs-lookup"><span data-stu-id="525bf-327">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="525bf-328">Aynı paket yoluna birden fazla dosya eklenirse NuGet bir uyarı verir.</span><span class="sxs-lookup"><span data-stu-id="525bf-328">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="525bf-329">`BuildAction`: Dosyaya atanacak derleme eylemi, yalnızca paket yolu `contentFiles` klasörsaise gereklidir.</span><span class="sxs-lookup"><span data-stu-id="525bf-329">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="525bf-330">Varsayılan "none" olarak belirlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="525bf-330">Defaults to "None".</span></span>

<span data-ttu-id="525bf-331">Örnek:</span><span class="sxs-lookup"><span data-stu-id="525bf-331">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="525bf-332">hedefi geri yükle</span><span class="sxs-lookup"><span data-stu-id="525bf-332">restore target</span></span>

<span data-ttu-id="525bf-333">`MSBuild -t:restore`(.NETCoreprojeleriylebirliktekullanılması),projedosyasındabaşvurulanpaketleriaşağıdakişekildegeriyükler:`nuget restore` `dotnet restore`</span><span class="sxs-lookup"><span data-stu-id="525bf-333">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="525bf-334">Proje başvurularına tüm projeyi oku</span><span class="sxs-lookup"><span data-stu-id="525bf-334">Read all project to project references</span></span>
1. <span data-ttu-id="525bf-335">Ara klasörünü ve hedef çerçeveleri bulmak için proje özelliklerini okuyun</span><span class="sxs-lookup"><span data-stu-id="525bf-335">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="525bf-336">MSBuild verilerini NuGet. Build. Tasks. dll dosyasına geçir</span><span class="sxs-lookup"><span data-stu-id="525bf-336">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="525bf-337">Geri yüklemeyi Çalıştır</span><span class="sxs-lookup"><span data-stu-id="525bf-337">Run restore</span></span>
1. <span data-ttu-id="525bf-338">Paketleri İndir</span><span class="sxs-lookup"><span data-stu-id="525bf-338">Download packages</span></span>
1. <span data-ttu-id="525bf-339">Varlıklar dosyası, hedefler ve props yazma</span><span class="sxs-lookup"><span data-stu-id="525bf-339">Write assets file, targets, and props</span></span>

<span data-ttu-id="525bf-340">Hedef yalnızca packagereference biçimini kullanan projeler için kullanılabilir. `restore`</span><span class="sxs-lookup"><span data-stu-id="525bf-340">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="525bf-341">Bu, `packages.config` biçimi kullanan projeler için çalışmaz; bunun yerine [NuGet geri yüklemeyi](../reference/cli-reference/cli-ref-restore.md) kullanın.</span><span class="sxs-lookup"><span data-stu-id="525bf-341">It does **not** work for projects using the `packages.config` format; use [nuget restore](../reference/cli-reference/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="525bf-342">Özellikleri geri yükle</span><span class="sxs-lookup"><span data-stu-id="525bf-342">Restore properties</span></span>

<span data-ttu-id="525bf-343">Ek geri yükleme ayarları proje dosyasındaki MSBuild özelliklerinden gelebilir.</span><span class="sxs-lookup"><span data-stu-id="525bf-343">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="525bf-344">Değerler, `-p:` anahtar kullanılarak komut satırından da ayarlanabilir (aşağıdaki örneklere bakın).</span><span class="sxs-lookup"><span data-stu-id="525bf-344">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="525bf-345">Özellik</span><span class="sxs-lookup"><span data-stu-id="525bf-345">Property</span></span> | <span data-ttu-id="525bf-346">Açıklama</span><span class="sxs-lookup"><span data-stu-id="525bf-346">Description</span></span> |
|--------|--------|
| <span data-ttu-id="525bf-347">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="525bf-347">RestoreSources</span></span> | <span data-ttu-id="525bf-348">Paket kaynaklarının noktalı virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="525bf-348">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="525bf-349">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="525bf-349">RestorePackagesPath</span></span> | <span data-ttu-id="525bf-350">Kullanıcı paketleri klasör yolu.</span><span class="sxs-lookup"><span data-stu-id="525bf-350">User packages folder path.</span></span> |
| <span data-ttu-id="525bf-351">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="525bf-351">RestoreDisableParallel</span></span> | <span data-ttu-id="525bf-352">İndirmeleri tek seferde bir ile sınırlayın.</span><span class="sxs-lookup"><span data-stu-id="525bf-352">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="525bf-353">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="525bf-353">RestoreConfigFile</span></span> | <span data-ttu-id="525bf-354">`Nuget.Config` Uygulanacak dosyanın yolu.</span><span class="sxs-lookup"><span data-stu-id="525bf-354">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="525bf-355">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="525bf-355">RestoreNoCache</span></span> | <span data-ttu-id="525bf-356">Doğru ise, önbelleğe alınmış paketlerin kullanılmasını önler.</span><span class="sxs-lookup"><span data-stu-id="525bf-356">If true, avoids using cached packages.</span></span> <span data-ttu-id="525bf-357">Bkz. [genel paketleri ve önbellek klasörlerini yönetme](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="525bf-357">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="525bf-358">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="525bf-358">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="525bf-359">Doğru ise, başarısız veya eksik paket kaynaklarını yoksayar.</span><span class="sxs-lookup"><span data-stu-id="525bf-359">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="525bf-360">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="525bf-360">RestoreFallbackFolders</span></span> | <span data-ttu-id="525bf-361">Geri dönüş klasörleri, Kullanıcı paketleri klasörüyle aynı şekilde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="525bf-361">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="525bf-362">Restoreaddıtionalprojectsources</span><span class="sxs-lookup"><span data-stu-id="525bf-362">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="525bf-363">Geri yükleme sırasında kullanılacak ek kaynaklar.</span><span class="sxs-lookup"><span data-stu-id="525bf-363">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="525bf-364">Restoreaddıtionalprojectfallbackfolders</span><span class="sxs-lookup"><span data-stu-id="525bf-364">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="525bf-365">Geri yükleme sırasında kullanılacak ek geri dönüş klasörleri.</span><span class="sxs-lookup"><span data-stu-id="525bf-365">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="525bf-366">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="525bf-366">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="525bf-367">İçinde belirtilen geri dönüş klasörlerini dışlar`RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="525bf-367">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="525bf-368">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="525bf-368">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="525bf-369">`NuGet.Build.Tasks.dll`Yolu.</span><span class="sxs-lookup"><span data-stu-id="525bf-369">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="525bf-370">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="525bf-370">RestoreGraphProjectInput</span></span> | <span data-ttu-id="525bf-371">Geri yüklenecek projelerin, mutlak yollar içermesi gereken, noktalı virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="525bf-371">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="525bf-372">Restoreuseskipnontenttargets</span><span class="sxs-lookup"><span data-stu-id="525bf-372">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="525bf-373">Projeler MSBuild aracılığıyla toplandığında, `SkipNonexistentTargets` iyileştirme kullanılarak toplanıp toplanmayacağını belirler.</span><span class="sxs-lookup"><span data-stu-id="525bf-373">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="525bf-374">Ayarlanmazsa, varsayılan olarak `true`olur.</span><span class="sxs-lookup"><span data-stu-id="525bf-374">When not set, defaults to `true`.</span></span> <span data-ttu-id="525bf-375">Projenin hedefleri içeri aktarılmadığı zaman, sonuç hızlı bir davranıştır.</span><span class="sxs-lookup"><span data-stu-id="525bf-375">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="525bf-376">Msbuildprojeclarsionspath</span><span class="sxs-lookup"><span data-stu-id="525bf-376">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="525bf-377">Çıkış klasörü, varsayılan olarak `BaseIntermediateOutputPath` `obj` ve klasörü.</span><span class="sxs-lookup"><span data-stu-id="525bf-377">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="525bf-378">Örnekler</span><span class="sxs-lookup"><span data-stu-id="525bf-378">Examples</span></span>

<span data-ttu-id="525bf-379">Komut satırı:</span><span class="sxs-lookup"><span data-stu-id="525bf-379">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="525bf-380">Proje dosyası:</span><span class="sxs-lookup"><span data-stu-id="525bf-380">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="525bf-381">Çıkışları geri yükleme</span><span class="sxs-lookup"><span data-stu-id="525bf-381">Restore outputs</span></span>

<span data-ttu-id="525bf-382">Restore derleme `obj` klasöründe aşağıdaki dosyaları oluşturur:</span><span class="sxs-lookup"><span data-stu-id="525bf-382">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="525bf-383">Dosya</span><span class="sxs-lookup"><span data-stu-id="525bf-383">File</span></span> | <span data-ttu-id="525bf-384">Açıklama</span><span class="sxs-lookup"><span data-stu-id="525bf-384">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="525bf-385">Tüm paket başvurularının bağımlılık grafiğini içerir.</span><span class="sxs-lookup"><span data-stu-id="525bf-385">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="525bf-386">Paketlerde bulunan MSBuild props 'a başvurular</span><span class="sxs-lookup"><span data-stu-id="525bf-386">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="525bf-387">Paketlerde bulunan MSBuild hedeflerine başvurular</span><span class="sxs-lookup"><span data-stu-id="525bf-387">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="525bf-388">Tek bir MSBuild komutuyla geri yükleme ve oluşturma</span><span class="sxs-lookup"><span data-stu-id="525bf-388">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="525bf-389">NuGet, MSBuild hedeflerini ve props 'ı getiren paketleri geri yükleyebilir, geri yükleme ve derleme değerlendirmeleri farklı genel özelliklerle çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="525bf-389">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="525bf-390">Bu, aşağıdakilerin öngörülemeyen ve genellikle yanlış bir davranışa sahip olacağı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="525bf-390">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="525bf-391">Bunun yerine önerilen yaklaşım şunlardır:</span><span class="sxs-lookup"><span data-stu-id="525bf-391">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="525bf-392">Aynı Logic şuna benzer `build`diğer hedefler için de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="525bf-392">The same logic applies to other targets similar to `build`.</span></span>

### <a name="packagetargetfallback"></a><span data-ttu-id="525bf-393">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="525bf-393">PackageTargetFallback</span></span>

<span data-ttu-id="525bf-394">Öğesi `PackageTargetFallback` , paketler geri yüklenirken kullanılacak bir dizi uyumlu hedef belirtmenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="525bf-394">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="525bf-395">DotNet [TXD](../reference/target-frameworks.md) kullanan paketlere, DotNet TXD bildirmeyin uyumlu paketlerle çalışmak üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="525bf-395">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="525bf-396">Diğer bir deyişle, projeniz DotNet TXI kullanıyorsa, bu durumda, `<PackageTargetFallback>` DotNet olmayan platformların DotNet ile uyumlu olmasını sağlamak için projeye eklemediğiniz sürece bağımlı olduğu tüm paketler DotNet TXD olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="525bf-396">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="525bf-397">Örneğin, proje `netstandard1.6` TXI kullanıyorsa ve bağımlı bir paket yalnızca `lib/net45/a.dll` ve `lib/portable-net45+win81/a.dll`içeriyorsa, proje derlenmeyecektir.</span><span class="sxs-lookup"><span data-stu-id="525bf-397">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="525bf-398">İçine getirmek istediğiniz değer ikinci dll ise, `PackageTargetFallback` `portable-net45+win81` dll 'nin uyumlu olduğunu söylemek için aşağıdaki gibi bir ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="525bf-398">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="525bf-399">Projenizdeki tüm hedeflere yönelik bir geri dönüş bildirmek için, `Condition` özniteliği devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="525bf-399">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="525bf-400">Ayrıca, burada gösterildiği `PackageTargetFallback` `$(PackageTargetFallback)` gibi, var olan varsa de genişletebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="525bf-400">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="525bf-401">Bir geri yükleme grafiğinden bir kitaplığı değiştirme</span><span class="sxs-lookup"><span data-stu-id="525bf-401">Replacing one library from a restore graph</span></span>

<span data-ttu-id="525bf-402">Geri yükleme yanlış derlemeyi alıyorsa, bu paketlerin varsayılan seçeneğini hariç tutabilir ve kendi seçimiyle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="525bf-402">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="525bf-403">Birincisi, en üst düzeyle `PackageReference`, tüm varlıkları hariç tut:</span><span class="sxs-lookup"><span data-stu-id="525bf-403">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="525bf-404">Ardından, DLL 'nin uygun yerel kopyasına kendi başvurunuz ekleyin:</span><span class="sxs-lookup"><span data-stu-id="525bf-404">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
