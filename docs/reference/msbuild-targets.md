---
title: NuGet paketi ve geri yükleme MSBuild hedefleri olarak
description: NuGet paketi ve geri yükleme, NuGet 4.0 + ile doğrudan MSBuild hedefleri olarak çalışabilir.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 8e662194fffc031d0cfc0aa129a5a15b555a4231
ms.sourcegitcommit: e65180e622f6233b51bb0b41d0e919688083eb26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68420014"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="5398b-103">NuGet paketi ve geri yükleme MSBuild hedefleri olarak</span><span class="sxs-lookup"><span data-stu-id="5398b-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="5398b-104">*NuGet 4.0 +*</span><span class="sxs-lookup"><span data-stu-id="5398b-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="5398b-105">[Packagereference](../consume-packages/package-references-in-project-files.md) biçimi sayesinde, NuGet 4.0 + tüm bildirim meta verilerini ayrı `.nuspec` bir dosya kullanmak yerine doğrudan proje dosyası içinde depolayabilirler.</span><span class="sxs-lookup"><span data-stu-id="5398b-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="5398b-106">MSBuild 15.1 + ile NuGet, aşağıda açıklandığı gibi, `pack` ve `restore` hedefleri ile birinci sınıf MSBuild vatandaşlık da vardır.</span><span class="sxs-lookup"><span data-stu-id="5398b-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="5398b-107">Bu hedefler, diğer herhangi bir MSBuild görevi veya hedefi ile yaptığınız gibi NuGet ile çalışmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="5398b-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="5398b-108">(NuGet 3. x ve öncesi için, bunun yerine NuGet CLı aracılığıyla [paketle](../reference/cli-reference/cli-ref-pack.md) ve [geri yükleme](../reference/cli-reference/cli-ref-restore.md) komutlarını kullanırsınız.)</span><span class="sxs-lookup"><span data-stu-id="5398b-108">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="5398b-109">Hedef derleme sırası</span><span class="sxs-lookup"><span data-stu-id="5398b-109">Target build order</span></span>

<span data-ttu-id="5398b-110">`pack` Ve`restore` MSBuild hedefleri olduğundan, iş akışınızı geliştirmek için bunlara erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5398b-110">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="5398b-111">Örneğin, paketledikten sonra paketinizi bir ağ paylaşımında kopyalamak istediğinizi varsayalım.</span><span class="sxs-lookup"><span data-stu-id="5398b-111">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="5398b-112">Bunu, proje dosyanıza aşağıdakileri ekleyerek yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5398b-112">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="5398b-113">Benzer şekilde, MSBuild görevinde bir MSBuild görevi yazabilir, kendi hedefini yazabilir ve NuGet özelliklerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5398b-113">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="5398b-114">paket hedefi</span><span class="sxs-lookup"><span data-stu-id="5398b-114">pack target</span></span>

<span data-ttu-id="5398b-115">Packagereference biçimini kullanan .NET Standard projeler için, `msbuild -t:pack` bir NuGet paketi oluştururken kullanılacak proje dosyasından girişler çizer.</span><span class="sxs-lookup"><span data-stu-id="5398b-115">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="5398b-116">Aşağıdaki tabloda, ilk `<PropertyGroup>` düğüm içindeki bir proje dosyasına eklenebilen MSBuild özellikleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="5398b-116">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="5398b-117">Projeyi sağ tıklayıp bağlam menüsünde **{Project_Name} Düzenle** ' yi seçerek Visual Studio 2017 ve sonraki sürümlerde bu düzenlemeleri kolayca yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5398b-117">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="5398b-118">Kolaylık olması için tablo, bir [ `.nuspec` dosyadaki](../reference/nuspec.md)denk özelliğe göre düzenlenir.</span><span class="sxs-lookup"><span data-stu-id="5398b-118">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="5398b-119">`Owners` Ve özelliklerininMSBuild`.nuspec`iledesteklenmediğiniunutmayın. `Summary`</span><span class="sxs-lookup"><span data-stu-id="5398b-119">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="5398b-120">Öznitelik/NuSpec değeri</span><span class="sxs-lookup"><span data-stu-id="5398b-120">Attribute/NuSpec Value</span></span> | <span data-ttu-id="5398b-121">MSBuild özelliği</span><span class="sxs-lookup"><span data-stu-id="5398b-121">MSBuild Property</span></span> | <span data-ttu-id="5398b-122">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="5398b-122">Default</span></span> | <span data-ttu-id="5398b-123">Notlar</span><span class="sxs-lookup"><span data-stu-id="5398b-123">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="5398b-124">Id</span><span class="sxs-lookup"><span data-stu-id="5398b-124">Id</span></span> | <span data-ttu-id="5398b-125">PackageId</span><span class="sxs-lookup"><span data-stu-id="5398b-125">PackageId</span></span> | <span data-ttu-id="5398b-126">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="5398b-126">AssemblyName</span></span> | <span data-ttu-id="5398b-127">MSBuild 'ten $ (AssemblyName)</span><span class="sxs-lookup"><span data-stu-id="5398b-127">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="5398b-128">Sürüm</span><span class="sxs-lookup"><span data-stu-id="5398b-128">Version</span></span> | <span data-ttu-id="5398b-129">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="5398b-129">PackageVersion</span></span> | <span data-ttu-id="5398b-130">Sürüm</span><span class="sxs-lookup"><span data-stu-id="5398b-130">Version</span></span> | <span data-ttu-id="5398b-131">Bu semver uyumludur, örneğin "1.0.0", "1.0.0-Beta" veya "1.0.0-Beta-00345"</span><span class="sxs-lookup"><span data-stu-id="5398b-131">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="5398b-132">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="5398b-132">VersionPrefix</span></span> | <span data-ttu-id="5398b-133">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="5398b-133">PackageVersionPrefix</span></span> | <span data-ttu-id="5398b-134">empty</span><span class="sxs-lookup"><span data-stu-id="5398b-134">empty</span></span> | <span data-ttu-id="5398b-135">PackageVersion ayarı PackageVersionPrefix üzerine yazıyor</span><span class="sxs-lookup"><span data-stu-id="5398b-135">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="5398b-136">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="5398b-136">VersionSuffix</span></span> | <span data-ttu-id="5398b-137">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="5398b-137">PackageVersionSuffix</span></span> | <span data-ttu-id="5398b-138">empty</span><span class="sxs-lookup"><span data-stu-id="5398b-138">empty</span></span> | <span data-ttu-id="5398b-139">MSBuild 'ten $ (VersionSuffix).</span><span class="sxs-lookup"><span data-stu-id="5398b-139">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="5398b-140">PackageVersion ayarı PackageVersionSuffix üzerine yazıyor</span><span class="sxs-lookup"><span data-stu-id="5398b-140">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="5398b-141">Yazarlar</span><span class="sxs-lookup"><span data-stu-id="5398b-141">Authors</span></span> | <span data-ttu-id="5398b-142">Yazarlar</span><span class="sxs-lookup"><span data-stu-id="5398b-142">Authors</span></span> | <span data-ttu-id="5398b-143">Geçerli kullanıcının Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="5398b-143">Username of the current user</span></span> | |
| <span data-ttu-id="5398b-144">lere</span><span class="sxs-lookup"><span data-stu-id="5398b-144">Owners</span></span> | <span data-ttu-id="5398b-145">Yok</span><span class="sxs-lookup"><span data-stu-id="5398b-145">N/A</span></span> | <span data-ttu-id="5398b-146">NuSpec içinde yok</span><span class="sxs-lookup"><span data-stu-id="5398b-146">Not present in NuSpec</span></span> | |
| <span data-ttu-id="5398b-147">Başlık</span><span class="sxs-lookup"><span data-stu-id="5398b-147">Title</span></span> | <span data-ttu-id="5398b-148">Başlık</span><span class="sxs-lookup"><span data-stu-id="5398b-148">Title</span></span> | <span data-ttu-id="5398b-149">PackageID</span><span class="sxs-lookup"><span data-stu-id="5398b-149">The PackageId</span></span>| |
| <span data-ttu-id="5398b-150">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5398b-150">Description</span></span> | <span data-ttu-id="5398b-151">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5398b-151">Description</span></span> | <span data-ttu-id="5398b-152">"Paket açıklaması"</span><span class="sxs-lookup"><span data-stu-id="5398b-152">"Package Description"</span></span> | |
| <span data-ttu-id="5398b-153">Yaptırımlar</span><span class="sxs-lookup"><span data-stu-id="5398b-153">Copyright</span></span> | <span data-ttu-id="5398b-154">Yaptırımlar</span><span class="sxs-lookup"><span data-stu-id="5398b-154">Copyright</span></span> | <span data-ttu-id="5398b-155">empty</span><span class="sxs-lookup"><span data-stu-id="5398b-155">empty</span></span> | |
| <span data-ttu-id="5398b-156">Requirelicensekabulünü</span><span class="sxs-lookup"><span data-stu-id="5398b-156">RequireLicenseAcceptance</span></span> | <span data-ttu-id="5398b-157">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="5398b-157">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="5398b-158">false</span><span class="sxs-lookup"><span data-stu-id="5398b-158">false</span></span> | |
| <span data-ttu-id="5398b-159">Lisan</span><span class="sxs-lookup"><span data-stu-id="5398b-159">license</span></span> | <span data-ttu-id="5398b-160">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="5398b-160">PackageLicenseExpression</span></span> | <span data-ttu-id="5398b-161">empty</span><span class="sxs-lookup"><span data-stu-id="5398b-161">empty</span></span> | <span data-ttu-id="5398b-162">Karşılık gelen`<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="5398b-162">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="5398b-163">Lisan</span><span class="sxs-lookup"><span data-stu-id="5398b-163">license</span></span> | <span data-ttu-id="5398b-164">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="5398b-164">PackageLicenseFile</span></span> | <span data-ttu-id="5398b-165">empty</span><span class="sxs-lookup"><span data-stu-id="5398b-165">empty</span></span> | <span data-ttu-id="5398b-166">Öğesine `<license type="file">`karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="5398b-166">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="5398b-167">Başvurulan lisans dosyasını açık bir şekilde paketetmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="5398b-167">You may need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="5398b-168">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="5398b-168">LicenseUrl</span></span> | <span data-ttu-id="5398b-169">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="5398b-169">PackageLicenseUrl</span></span> | <span data-ttu-id="5398b-170">empty</span><span class="sxs-lookup"><span data-stu-id="5398b-170">empty</span></span> | <span data-ttu-id="5398b-171">`licenseUrl`kullanım dışı bırakılıyor, PackageLicenseExpression veya PackageLicenseFile özelliğini kullanın</span><span class="sxs-lookup"><span data-stu-id="5398b-171">`licenseUrl` is being deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="5398b-172">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="5398b-172">ProjectUrl</span></span> | <span data-ttu-id="5398b-173">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="5398b-173">PackageProjectUrl</span></span> | <span data-ttu-id="5398b-174">empty</span><span class="sxs-lookup"><span data-stu-id="5398b-174">empty</span></span> | |
| <span data-ttu-id="5398b-175">IconUrl</span><span class="sxs-lookup"><span data-stu-id="5398b-175">IconUrl</span></span> | <span data-ttu-id="5398b-176">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="5398b-176">PackageIconUrl</span></span> | <span data-ttu-id="5398b-177">empty</span><span class="sxs-lookup"><span data-stu-id="5398b-177">empty</span></span> | |
| <span data-ttu-id="5398b-178">Etiketler</span><span class="sxs-lookup"><span data-stu-id="5398b-178">Tags</span></span> | <span data-ttu-id="5398b-179">PackageTags</span><span class="sxs-lookup"><span data-stu-id="5398b-179">PackageTags</span></span> | <span data-ttu-id="5398b-180">empty</span><span class="sxs-lookup"><span data-stu-id="5398b-180">empty</span></span> | <span data-ttu-id="5398b-181">Etiketler noktalı virgülle ayrılır.</span><span class="sxs-lookup"><span data-stu-id="5398b-181">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="5398b-182">relet 'ler</span><span class="sxs-lookup"><span data-stu-id="5398b-182">ReleaseNotes</span></span> | <span data-ttu-id="5398b-183">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="5398b-183">PackageReleaseNotes</span></span> | <span data-ttu-id="5398b-184">empty</span><span class="sxs-lookup"><span data-stu-id="5398b-184">empty</span></span> | |
| <span data-ttu-id="5398b-185">Depo/URL</span><span class="sxs-lookup"><span data-stu-id="5398b-185">Repository/Url</span></span> | <span data-ttu-id="5398b-186">Depourl 'Si</span><span class="sxs-lookup"><span data-stu-id="5398b-186">RepositoryUrl</span></span> | <span data-ttu-id="5398b-187">empty</span><span class="sxs-lookup"><span data-stu-id="5398b-187">empty</span></span> | <span data-ttu-id="5398b-188">Kaynak kodu kopyalamak veya almak için kullanılan depo URL 'SI.</span><span class="sxs-lookup"><span data-stu-id="5398b-188">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="5398b-189">Örneğinde *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="5398b-189">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="5398b-190">Depo/tür</span><span class="sxs-lookup"><span data-stu-id="5398b-190">Repository/Type</span></span> | <span data-ttu-id="5398b-191">Repositorytype parametrelerinin sağlanması</span><span class="sxs-lookup"><span data-stu-id="5398b-191">RepositoryType</span></span> | <span data-ttu-id="5398b-192">empty</span><span class="sxs-lookup"><span data-stu-id="5398b-192">empty</span></span> | <span data-ttu-id="5398b-193">Depo türü.</span><span class="sxs-lookup"><span data-stu-id="5398b-193">Repository type.</span></span> <span data-ttu-id="5398b-194">Örnekler: *Git*, *TFS*.</span><span class="sxs-lookup"><span data-stu-id="5398b-194">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="5398b-195">Depo/dal</span><span class="sxs-lookup"><span data-stu-id="5398b-195">Repository/Branch</span></span> | <span data-ttu-id="5398b-196">Depodalı</span><span class="sxs-lookup"><span data-stu-id="5398b-196">RepositoryBranch</span></span> | <span data-ttu-id="5398b-197">empty</span><span class="sxs-lookup"><span data-stu-id="5398b-197">empty</span></span> | <span data-ttu-id="5398b-198">İsteğe bağlı depo dalı bilgileri.</span><span class="sxs-lookup"><span data-stu-id="5398b-198">Optional repository branch information.</span></span> <span data-ttu-id="5398b-199">Bu özelliğin dahil olması için aynı zamanda bir *Depo-URL* belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="5398b-199">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="5398b-200">Örnek: *Master* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="5398b-200">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="5398b-201">Depo/kayıt</span><span class="sxs-lookup"><span data-stu-id="5398b-201">Repository/Commit</span></span> | <span data-ttu-id="5398b-202">Kayıt yapma</span><span class="sxs-lookup"><span data-stu-id="5398b-202">RepositoryCommit</span></span> | <span data-ttu-id="5398b-203">empty</span><span class="sxs-lookup"><span data-stu-id="5398b-203">empty</span></span> | <span data-ttu-id="5398b-204">Paketin hangi kaynağa göre oluşturulduğunu göstermek için isteğe bağlı depo kaydı veya değişiklik kümesi.</span><span class="sxs-lookup"><span data-stu-id="5398b-204">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="5398b-205">Bu özelliğin dahil olması için aynı zamanda bir *Depo-URL* belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="5398b-205">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="5398b-206">Örnek: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="5398b-206">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="5398b-207">PackageType</span><span class="sxs-lookup"><span data-stu-id="5398b-207">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="5398b-208">Özet</span><span class="sxs-lookup"><span data-stu-id="5398b-208">Summary</span></span> | <span data-ttu-id="5398b-209">Desteklenmez</span><span class="sxs-lookup"><span data-stu-id="5398b-209">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="5398b-210">Paket hedef girişleri</span><span class="sxs-lookup"><span data-stu-id="5398b-210">pack target inputs</span></span>

- <span data-ttu-id="5398b-211">Ispackable</span><span class="sxs-lookup"><span data-stu-id="5398b-211">IsPackable</span></span>
- <span data-ttu-id="5398b-212">Suppressbağımlıcıeswhenpaketleme</span><span class="sxs-lookup"><span data-stu-id="5398b-212">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="5398b-213">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="5398b-213">PackageVersion</span></span>
- <span data-ttu-id="5398b-214">PackageId</span><span class="sxs-lookup"><span data-stu-id="5398b-214">PackageId</span></span>
- <span data-ttu-id="5398b-215">Yazarlar</span><span class="sxs-lookup"><span data-stu-id="5398b-215">Authors</span></span>
- <span data-ttu-id="5398b-216">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5398b-216">Description</span></span>
- <span data-ttu-id="5398b-217">Yaptırımlar</span><span class="sxs-lookup"><span data-stu-id="5398b-217">Copyright</span></span>
- <span data-ttu-id="5398b-218">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="5398b-218">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="5398b-219">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="5398b-219">DevelopmentDependency</span></span>
- <span data-ttu-id="5398b-220">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="5398b-220">PackageLicenseExpression</span></span>
- <span data-ttu-id="5398b-221">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="5398b-221">PackageLicenseFile</span></span>
- <span data-ttu-id="5398b-222">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="5398b-222">PackageLicenseUrl</span></span>
- <span data-ttu-id="5398b-223">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="5398b-223">PackageProjectUrl</span></span>
- <span data-ttu-id="5398b-224">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="5398b-224">PackageIconUrl</span></span>
- <span data-ttu-id="5398b-225">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="5398b-225">PackageReleaseNotes</span></span>
- <span data-ttu-id="5398b-226">PackageTags</span><span class="sxs-lookup"><span data-stu-id="5398b-226">PackageTags</span></span>
- <span data-ttu-id="5398b-227">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="5398b-227">PackageOutputPath</span></span>
- <span data-ttu-id="5398b-228">Includesymbols</span><span class="sxs-lookup"><span data-stu-id="5398b-228">IncludeSymbols</span></span>
- <span data-ttu-id="5398b-229">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="5398b-229">IncludeSource</span></span>
- <span data-ttu-id="5398b-230">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="5398b-230">PackageTypes</span></span>
- <span data-ttu-id="5398b-231">IsTool</span><span class="sxs-lookup"><span data-stu-id="5398b-231">IsTool</span></span>
- <span data-ttu-id="5398b-232">Depourl 'Si</span><span class="sxs-lookup"><span data-stu-id="5398b-232">RepositoryUrl</span></span>
- <span data-ttu-id="5398b-233">Repositorytype parametrelerinin sağlanması</span><span class="sxs-lookup"><span data-stu-id="5398b-233">RepositoryType</span></span>
- <span data-ttu-id="5398b-234">Depodalı</span><span class="sxs-lookup"><span data-stu-id="5398b-234">RepositoryBranch</span></span>
- <span data-ttu-id="5398b-235">Kayıt yapma</span><span class="sxs-lookup"><span data-stu-id="5398b-235">RepositoryCommit</span></span>
- <span data-ttu-id="5398b-236">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="5398b-236">NoPackageAnalysis</span></span>
- <span data-ttu-id="5398b-237">minClientVersion</span><span class="sxs-lookup"><span data-stu-id="5398b-237">MinClientVersion</span></span>
- <span data-ttu-id="5398b-238">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="5398b-238">IncludeBuildOutput</span></span>
- <span data-ttu-id="5398b-239">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="5398b-239">IncludeContentInPack</span></span>
- <span data-ttu-id="5398b-240">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="5398b-240">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="5398b-241">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="5398b-241">ContentTargetFolders</span></span>
- <span data-ttu-id="5398b-242">Nusguus dosyası</span><span class="sxs-lookup"><span data-stu-id="5398b-242">NuspecFile</span></span>
- <span data-ttu-id="5398b-243">Nusgubasepath</span><span class="sxs-lookup"><span data-stu-id="5398b-243">NuspecBasePath</span></span>
- <span data-ttu-id="5398b-244">Nus, Properties</span><span class="sxs-lookup"><span data-stu-id="5398b-244">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="5398b-245">paket senaryoları</span><span class="sxs-lookup"><span data-stu-id="5398b-245">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="5398b-246">Bağımlılıkları gösterme</span><span class="sxs-lookup"><span data-stu-id="5398b-246">Suppress dependencies</span></span>

<span data-ttu-id="5398b-247">Oluşturulan NuGet paketinden paket bağımlılıklarını bastırmak için, olarak `SuppressDependenciesWhenPacking` `true` ayarlayın ve oluşturulan nupkg dosyasından tüm bağımlılıkların atlanmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="5398b-247">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="5398b-248">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="5398b-248">PackageIconUrl</span></span>

<span data-ttu-id="5398b-249">[NuGet sorunu 352](https://github.com/NuGet/Home/issues/352)değişikliğinin bir parçası olarak, `PackageIconUrl` sonunda olarak `PackageIconUri` değiştirilir ve sonuç paketinin köküne dahil edilecek bir simge dosyasının göreli yolu olabilir.</span><span class="sxs-lookup"><span data-stu-id="5398b-249">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="5398b-250">Çıkış derlemeleri</span><span class="sxs-lookup"><span data-stu-id="5398b-250">Output assemblies</span></span>

<span data-ttu-id="5398b-251">`nuget pack`çıktı dosyalarını,,, `.exe`, `.dll`ve `.xml` `.winmd` uzantılarınakopyalar`.json`. `.pri`</span><span class="sxs-lookup"><span data-stu-id="5398b-251">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="5398b-252">Kopyalanan çıkış dosyaları, `BuiltOutputProjectGroup` hedef tarafından MSBuild 'in sağladığı şuna bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="5398b-252">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="5398b-253">Çıktı derlemelerinin nerede olduğunu denetlemek için, proje dosyanızda veya komut satırında kullanabileceğiniz iki MSBuild özelliği vardır:</span><span class="sxs-lookup"><span data-stu-id="5398b-253">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="5398b-254">`IncludeBuildOutput`: Derleme çıkış derlemelerinin pakete dahil edilip edilmeyeceğini belirleyen bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="5398b-254">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="5398b-255">`BuildOutputTargetFolder`: Çıkış derlemelerinin yerleştirilmesi gereken klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="5398b-255">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="5398b-256">Çıkış derlemeleri (ve diğer çıkış dosyaları) ilgili çerçeve klasörlerine kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="5398b-256">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="5398b-257">Paket başvuruları</span><span class="sxs-lookup"><span data-stu-id="5398b-257">Package references</span></span>

<span data-ttu-id="5398b-258">Bkz. [Proje dosyalarındaki paket başvuruları](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="5398b-258">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="5398b-259">Projeden projeye başvurular</span><span class="sxs-lookup"><span data-stu-id="5398b-259">Project to project references</span></span>

<span data-ttu-id="5398b-260">Proje başvuruları, varsayılan olarak NuGet paket başvuruları olarak değerlendirilir, örneğin:</span><span class="sxs-lookup"><span data-stu-id="5398b-260">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="5398b-261">Ayrıca, proje başvurunuz için aşağıdaki meta verileri de ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5398b-261">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="5398b-262">Bir paketteki içerik ekleme</span><span class="sxs-lookup"><span data-stu-id="5398b-262">Including content in a package</span></span>

<span data-ttu-id="5398b-263">İçerik eklemek için var olan `<Content>` öğeye ek meta veriler ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5398b-263">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="5398b-264">Varsayılan olarak, aşağıdaki gibi girdilerle geçersiz kılmadığınız müddetçe "Içerik" türünde her şey pakete dahil edilir:</span><span class="sxs-lookup"><span data-stu-id="5398b-264">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="5398b-265">Varsayılan olarak, her şey bir paket içindeki `content` ve `contentFiles\any\<target_framework>` klasörünün köküne eklenir ve bir paket yolu belirtmediğiniz takdirde göreli klasör yapısını korur:</span><span class="sxs-lookup"><span data-stu-id="5398b-265">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="5398b-266">Tüm içeriğinizi yalnızca belirli bir kök klasöre ( `content` ve `contentFiles` her ikisi yerine) kopyalamak istiyorsanız, varsayılan olarak "Content; ContentFiles" olan, ancak başka bir klasör `ContentTargetFolders`adına ayarlanabilir MSBuild özelliğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5398b-266">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="5398b-267">Yalnızca dosyaları ' ın `ContentTargetFolders` altında veya `contentFiles\<language>\<target_framework>` temel alarak `buildAction`"ContentFiles" `contentFiles\any\<target_framework>` seçeneğinin belirtildiğine unutmayın.</span><span class="sxs-lookup"><span data-stu-id="5398b-267">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="5398b-268">`PackagePath`noktalı virgülle ayrılmış bir hedef yolları kümesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="5398b-268">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="5398b-269">Boş bir paket yolu belirtilmesi, dosyayı paketin köküne ekler.</span><span class="sxs-lookup"><span data-stu-id="5398b-269">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="5398b-270">Örneğin, aşağıdaki, ve paket `libuv.txt` köküne `content\myfiles`ekler `content\samples`:</span><span class="sxs-lookup"><span data-stu-id="5398b-270">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="5398b-271">Ayrıca, varsayılan olarak `$(IncludeContentInPack)` `true`olan MSBuild özelliği de vardır.</span><span class="sxs-lookup"><span data-stu-id="5398b-271">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="5398b-272">Bu, herhangi bir projede `false` olarak ayarlandıysa, bu projeden içerik NuGet paketine dahil edilmez.</span><span class="sxs-lookup"><span data-stu-id="5398b-272">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="5398b-273">Yukarıdaki öğelerin herhangi birine ayarlayabileceğiniz diğer paketine özgü meta veriler içerir ```<PackageCopyToOutput>``` ve ```<PackageFlatten>``` çıkış nuspec içindeki ```contentFiles``` giriş ```CopyToOutput``` üzerinde ```Flatten``` ve değerlerini belirler.</span><span class="sxs-lookup"><span data-stu-id="5398b-273">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="5398b-274">İçerik öğelerinden ayrı olarak `<Pack>` , ve `<PackagePath>` meta veriler de derleme, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, designdata, designdatawithdesigntimecreateabletypes derleme eylemine sahip dosyalarda ayarlanabilir , CodeAnalysisDictionary, AndroidAsset, AndroidResource, paketleme Leresource veya None.</span><span class="sxs-lookup"><span data-stu-id="5398b-274">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="5398b-275">Glob desenleri kullanılırken dosya adını paket yolunuza eklemek için paket yolu, klasör ayırıcı karakteriyle bitmelidir; Aksi takdirde, paket yolu dosya adı dahil tam yol olarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="5398b-275">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="5398b-276">Includesymbols</span><span class="sxs-lookup"><span data-stu-id="5398b-276">IncludeSymbols</span></span>

<span data-ttu-id="5398b-277">`MSBuild -t:pack -p:IncludeSymbols=true`Kullanırken, karşılık gelen`.dll` `.winmd` `.pri` dosyalardiğer`.json`çıkış dosyalarıylabirlikte`.exe`kopyalanır (,,, ,,).`.xml` `.pdb`</span><span class="sxs-lookup"><span data-stu-id="5398b-277">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="5398b-278">Ayarın `IncludeSymbols=true` düzenli bir paket *ve* bir semboller paketi oluşturduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="5398b-278">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="5398b-279">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="5398b-279">IncludeSource</span></span>

<span data-ttu-id="5398b-280">Bu, ile `IncludeSymbols` `.pdb` aynıdır, ancak kaynak dosyalarını da dosyalarla birlikte kopyalar.</span><span class="sxs-lookup"><span data-stu-id="5398b-280">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="5398b-281">Tüm dosya türleri `Compile` , elde edilen paketteki göreli `src\<ProjectName>\` yol klasörü yapısını korumak için üzerine kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="5398b-281">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="5398b-282">Aynı zamanda, olarak `ProjectReference` `TreatAsPackageReference` `false`ayarlanmış herhangi bir kaynak dosyası için de aynı olur.</span><span class="sxs-lookup"><span data-stu-id="5398b-282">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="5398b-283">Derleme türü bir dosya proje klasörünün dışında ise, ' ye `src\<ProjectName>\`eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="5398b-283">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="5398b-284">Lisans ifadesi veya lisans dosyası paketleme</span><span class="sxs-lookup"><span data-stu-id="5398b-284">Packing a license expression or a license file</span></span>

<span data-ttu-id="5398b-285">Bir lisans ifadesi kullanılırken PackageLicenseExpression özelliğinin kullanılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5398b-285">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="5398b-286">[Lisans ifadesi örneği](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="5398b-286">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="5398b-287">[NuGet.org tarafından kabul edilen lisans ifadeleri ve lisanslar hakkında daha fazla bilgi edinin](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="5398b-287">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="5398b-288">Bir lisans dosyası paketleme sırasında, paketin köküne göre paket yolunu belirtmek için PackageLicenseFile özelliğini kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5398b-288">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="5398b-289">Ayrıca, dosyanın pakete eklendiğinden emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5398b-289">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="5398b-290">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="5398b-290">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```
<span data-ttu-id="5398b-291">[Lisans dosyası örneği](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="5398b-291">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="5398b-292">IsTool</span><span class="sxs-lookup"><span data-stu-id="5398b-292">IsTool</span></span>

<span data-ttu-id="5398b-293">Kullanırken `MSBuild -t:pack -p:IsTool=true`, [Çıkış derlemeleri](#output-assemblies) senaryosunda belirtilen tüm çıkış dosyaları, `tools` `lib` klasörü yerine klasörüne kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="5398b-293">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="5398b-294">Bunun, `DotNetCliTool` `PackageType` içindeki dosyasınıayarlayarakbelirtilenöğesindenfarklıolduğunuunutmayın.`.csproj`</span><span class="sxs-lookup"><span data-stu-id="5398b-294">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="5398b-295">. Nuspec kullanarak paketleme</span><span class="sxs-lookup"><span data-stu-id="5398b-295">Packing using a .nuspec</span></span>

<span data-ttu-id="5398b-296">Bunun yerine genellikle `.nuspec` proje dosyasındaki dosyada bulunan [tüm özellikleri eklemeniz](../reference/msbuild-targets.md#pack-target) önerilse de, projenizi paketlebilmeniz için bir `.nuspec` dosya kullanmayı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5398b-296">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="5398b-297">Tarafından kullanılan `PackageReference`SDK olmayan bir proje için, paket görevinin yürütülebilmesi için içeri aktarmanız `NuGet.Build.Tasks.Pack.targets` gerekir.</span><span class="sxs-lookup"><span data-stu-id="5398b-297">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="5398b-298">Bir nuspec dosyası paketetmeden önce projeyi geri yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5398b-298">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="5398b-299">(SDK stili bir proje varsayılan olarak paket hedeflerini içerir.)</span><span class="sxs-lookup"><span data-stu-id="5398b-299">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="5398b-300">Proje dosyasının hedef çerçevesi ilgisizdir ve bir nuspec paketleme sırasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="5398b-300">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="5398b-301">Aşağıdaki üç MSBuild özelliği, ile `.nuspec`paketleme ile ilgilidir:</span><span class="sxs-lookup"><span data-stu-id="5398b-301">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="5398b-302">`NuspecFile`: paketleme için kullanılan `.nuspec` dosyanın göreli veya mutlak yolu.</span><span class="sxs-lookup"><span data-stu-id="5398b-302">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="5398b-303">`NuspecProperties`: Key = değer çiftleri için noktalı virgülle ayrılmış bir liste.</span><span class="sxs-lookup"><span data-stu-id="5398b-303">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="5398b-304">MSBuild komut satırı ayrıştırması çalışma yöntemi nedeniyle, birden çok özellik şu şekilde belirtilmelidir: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="5398b-304">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="5398b-305">`NuspecBasePath`: `.nuspec` Dosya için temel yol.</span><span class="sxs-lookup"><span data-stu-id="5398b-305">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="5398b-306">Projenizi paketmek için kullanıyorsanız `dotnet.exe` , aşağıdaki gibi bir komut kullanın:</span><span class="sxs-lookup"><span data-stu-id="5398b-306">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="5398b-307">Projenizi paketmek için MSBuild kullanıyorsanız, aşağıdaki gibi bir komut kullanın:</span><span class="sxs-lookup"><span data-stu-id="5398b-307">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="5398b-308">Lütfen DotNet. exe veya MSBuild kullanarak bir nuspec paketleme, projenin varsayılan olarak oluşturulmasına da neden olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="5398b-308">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="5398b-309">Bu, proje dosyasında ayarı ```--no-build``` ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` ile birlikte proje dosyanızdaki ayarın ```<NoBuild>true</NoBuild> ``` eşdeğeri olan DotNet. exe ' ye geçirilerek kaçınılabilir.</span><span class="sxs-lookup"><span data-stu-id="5398b-309">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="5398b-310">Bir nuspec dosyası paketiçin bir *. csproj* dosyası örneği:</span><span class="sxs-lookup"><span data-stu-id="5398b-310">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="5398b-311">Özelleştirilmiş paket oluşturmak için gelişmiş uzantı noktaları</span><span class="sxs-lookup"><span data-stu-id="5398b-311">Advanced extension points to create customized package</span></span>

<span data-ttu-id="5398b-312">`pack` Hedef, iç, hedef çerçeveye özgü derlemede çalışan iki uzantı noktası sağlar.</span><span class="sxs-lookup"><span data-stu-id="5398b-312">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="5398b-313">Uzantı noktaları, hedef çerçeveye özgü içerik ve derlemelerin bir pakete dahil edilmesi için destek:</span><span class="sxs-lookup"><span data-stu-id="5398b-313">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="5398b-314">`TargetsForTfmSpecificBuildOutput`hedef `lib` Klasörü veya kullanılarak `BuildOutputTargetFolder`belirtilen bir klasörü içindeki dosyalar için kullanın.</span><span class="sxs-lookup"><span data-stu-id="5398b-314">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="5398b-315">`TargetsForTfmSpecificContentInPackage`hedef Dışındaki dosyalar için kullanın `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="5398b-315">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="5398b-316">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="5398b-316">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="5398b-317">Özel bir hedef yazın ve `$(TargetsForTfmSpecificBuildOutput)` özelliğin değeri olarak belirtin.</span><span class="sxs-lookup"><span data-stu-id="5398b-317">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="5398b-318">`BuildOutputTargetFolder` (Varsayılan olarak LIB) öğesine gitmesi gereken tüm dosyalar için, hedef bu dosyaları ItemGroup `BuildOutputInPackage` 'a yazmalıdır ve aşağıdaki iki meta veri değerini ayarlamış olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="5398b-318">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="5398b-319">`FinalOutputPath`: Dosyanın mutlak yolu; sağlanmazsa, kimlik kaynak yolunu değerlendirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5398b-319">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="5398b-320">`TargetPath`:  Seçim Dosyanın içinde `lib\<TargetFramework>` , ilgili kültür klasörlerinin altında yer alan uydu derlemeleri gibi bir alt klasöre gitmesi gerektiğinde ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="5398b-320">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="5398b-321">Varsayılan olarak dosyanın adıdır.</span><span class="sxs-lookup"><span data-stu-id="5398b-321">Defaults to the name of the file.</span></span>

<span data-ttu-id="5398b-322">Örnek:</span><span class="sxs-lookup"><span data-stu-id="5398b-322">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="5398b-323">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="5398b-323">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="5398b-324">Özel bir hedef yazın ve `$(TargetsForTfmSpecificContentInPackage)` özelliğin değeri olarak belirtin.</span><span class="sxs-lookup"><span data-stu-id="5398b-324">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="5398b-325">Pakete dahil edilecek tüm dosyalar için, hedef bu dosyaları ItemGroup `TfmSpecificPackageFile` 'a yazmalıdır ve aşağıdaki isteğe bağlı meta verileri ayarlar:</span><span class="sxs-lookup"><span data-stu-id="5398b-325">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="5398b-326">`PackagePath`: Dosyanın pakette çıkış olması gereken yol.</span><span class="sxs-lookup"><span data-stu-id="5398b-326">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="5398b-327">Aynı paket yoluna birden fazla dosya eklenirse NuGet bir uyarı verir.</span><span class="sxs-lookup"><span data-stu-id="5398b-327">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="5398b-328">`BuildAction`: Dosyaya atanacak derleme eylemi, yalnızca paket yolu `contentFiles` klasörsaise gereklidir.</span><span class="sxs-lookup"><span data-stu-id="5398b-328">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="5398b-329">Varsayılan "none" olarak belirlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="5398b-329">Defaults to "None".</span></span>

<span data-ttu-id="5398b-330">Örnek:</span><span class="sxs-lookup"><span data-stu-id="5398b-330">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="5398b-331">hedefi geri yükle</span><span class="sxs-lookup"><span data-stu-id="5398b-331">restore target</span></span>

<span data-ttu-id="5398b-332">`MSBuild -t:restore`(.NETCoreprojeleriylebirliktekullanılması),projedosyasındabaşvurulanpaketleriaşağıdakişekildegeriyükler:`nuget restore` `dotnet restore`</span><span class="sxs-lookup"><span data-stu-id="5398b-332">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="5398b-333">Proje başvurularına tüm projeyi oku</span><span class="sxs-lookup"><span data-stu-id="5398b-333">Read all project to project references</span></span>
1. <span data-ttu-id="5398b-334">Ara klasörünü ve hedef çerçeveleri bulmak için proje özelliklerini okuyun</span><span class="sxs-lookup"><span data-stu-id="5398b-334">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="5398b-335">MSBuild verilerini NuGet. Build. Tasks. dll dosyasına geçir</span><span class="sxs-lookup"><span data-stu-id="5398b-335">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="5398b-336">Geri yüklemeyi Çalıştır</span><span class="sxs-lookup"><span data-stu-id="5398b-336">Run restore</span></span>
1. <span data-ttu-id="5398b-337">Paketleri İndir</span><span class="sxs-lookup"><span data-stu-id="5398b-337">Download packages</span></span>
1. <span data-ttu-id="5398b-338">Varlıklar dosyası, hedefler ve props yazma</span><span class="sxs-lookup"><span data-stu-id="5398b-338">Write assets file, targets, and props</span></span>

<span data-ttu-id="5398b-339">Hedef yalnızca packagereference biçimini kullanan projeler için kullanılabilir.  `restore`</span><span class="sxs-lookup"><span data-stu-id="5398b-339">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="5398b-340">Bu, `packages.config` biçimi kullanan projeler **için çalışmaz;** bunun yerine [NuGet geri yüklemeyi](../reference/cli-reference/cli-ref-restore.md) kullanın.</span><span class="sxs-lookup"><span data-stu-id="5398b-340">It does **not** work for projects using the `packages.config` format; use [nuget restore](../reference/cli-reference/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="5398b-341">Özellikleri geri yükle</span><span class="sxs-lookup"><span data-stu-id="5398b-341">Restore properties</span></span>

<span data-ttu-id="5398b-342">Ek geri yükleme ayarları proje dosyasındaki MSBuild özelliklerinden gelebilir.</span><span class="sxs-lookup"><span data-stu-id="5398b-342">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="5398b-343">Değerler, `-p:` anahtar kullanılarak komut satırından da ayarlanabilir (aşağıdaki örneklere bakın).</span><span class="sxs-lookup"><span data-stu-id="5398b-343">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="5398b-344">Özellik</span><span class="sxs-lookup"><span data-stu-id="5398b-344">Property</span></span> | <span data-ttu-id="5398b-345">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5398b-345">Description</span></span> |
|--------|--------|
| <span data-ttu-id="5398b-346">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="5398b-346">RestoreSources</span></span> | <span data-ttu-id="5398b-347">Paket kaynaklarının noktalı virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="5398b-347">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="5398b-348">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="5398b-348">RestorePackagesPath</span></span> | <span data-ttu-id="5398b-349">Kullanıcı paketleri klasör yolu.</span><span class="sxs-lookup"><span data-stu-id="5398b-349">User packages folder path.</span></span> |
| <span data-ttu-id="5398b-350">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="5398b-350">RestoreDisableParallel</span></span> | <span data-ttu-id="5398b-351">İndirmeleri tek seferde bir ile sınırlayın.</span><span class="sxs-lookup"><span data-stu-id="5398b-351">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="5398b-352">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="5398b-352">RestoreConfigFile</span></span> | <span data-ttu-id="5398b-353">`Nuget.Config` Uygulanacak dosyanın yolu.</span><span class="sxs-lookup"><span data-stu-id="5398b-353">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="5398b-354">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="5398b-354">RestoreNoCache</span></span> | <span data-ttu-id="5398b-355">Doğru ise, önbelleğe alınmış paketlerin kullanılmasını önler.</span><span class="sxs-lookup"><span data-stu-id="5398b-355">If true, avoids using cached packages.</span></span> <span data-ttu-id="5398b-356">Bkz. [genel paketleri ve önbellek klasörlerini yönetme](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="5398b-356">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="5398b-357">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="5398b-357">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="5398b-358">Doğru ise, başarısız veya eksik paket kaynaklarını yoksayar.</span><span class="sxs-lookup"><span data-stu-id="5398b-358">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="5398b-359">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="5398b-359">RestoreFallbackFolders</span></span> | <span data-ttu-id="5398b-360">Geri dönüş klasörleri, Kullanıcı paketleri klasörüyle aynı şekilde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5398b-360">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="5398b-361">Restoreaddıtionalprojectsources</span><span class="sxs-lookup"><span data-stu-id="5398b-361">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="5398b-362">Geri yükleme sırasında kullanılacak ek kaynaklar.</span><span class="sxs-lookup"><span data-stu-id="5398b-362">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="5398b-363">Restoreaddıtionalprojectfallbackfolders</span><span class="sxs-lookup"><span data-stu-id="5398b-363">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="5398b-364">Geri yükleme sırasında kullanılacak ek geri dönüş klasörleri.</span><span class="sxs-lookup"><span data-stu-id="5398b-364">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="5398b-365">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="5398b-365">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="5398b-366">İçinde belirtilen geri dönüş klasörlerini dışlar`RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="5398b-366">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="5398b-367">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="5398b-367">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="5398b-368">`NuGet.Build.Tasks.dll`Yolu.</span><span class="sxs-lookup"><span data-stu-id="5398b-368">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="5398b-369">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="5398b-369">RestoreGraphProjectInput</span></span> | <span data-ttu-id="5398b-370">Geri yüklenecek projelerin, mutlak yollar içermesi gereken, noktalı virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="5398b-370">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="5398b-371">Restoreuseskipnontenttargets</span><span class="sxs-lookup"><span data-stu-id="5398b-371">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="5398b-372">Projeler MSBuild aracılığıyla toplandığında, `SkipNonexistentTargets` iyileştirme kullanılarak toplanıp toplanmayacağını belirler.</span><span class="sxs-lookup"><span data-stu-id="5398b-372">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="5398b-373">Ayarlanmazsa, varsayılan olarak `true`olur.</span><span class="sxs-lookup"><span data-stu-id="5398b-373">When not set, defaults to `true`.</span></span> <span data-ttu-id="5398b-374">Projenin hedefleri içeri aktarılmadığı zaman, sonuç hızlı bir davranıştır.</span><span class="sxs-lookup"><span data-stu-id="5398b-374">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="5398b-375">Msbuildprojeclarsionspath</span><span class="sxs-lookup"><span data-stu-id="5398b-375">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="5398b-376">Çıkış klasörü, varsayılan olarak `BaseIntermediateOutputPath` `obj` ve klasörü.</span><span class="sxs-lookup"><span data-stu-id="5398b-376">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="5398b-377">Örnekler</span><span class="sxs-lookup"><span data-stu-id="5398b-377">Examples</span></span>

<span data-ttu-id="5398b-378">Komut satırı:</span><span class="sxs-lookup"><span data-stu-id="5398b-378">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="5398b-379">Proje dosyası:</span><span class="sxs-lookup"><span data-stu-id="5398b-379">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="5398b-380">Çıkışları geri yükleme</span><span class="sxs-lookup"><span data-stu-id="5398b-380">Restore outputs</span></span>

<span data-ttu-id="5398b-381">Restore derleme `obj` klasöründe aşağıdaki dosyaları oluşturur:</span><span class="sxs-lookup"><span data-stu-id="5398b-381">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="5398b-382">Dosya</span><span class="sxs-lookup"><span data-stu-id="5398b-382">File</span></span> | <span data-ttu-id="5398b-383">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5398b-383">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="5398b-384">Tüm paket başvurularının bağımlılık grafiğini içerir.</span><span class="sxs-lookup"><span data-stu-id="5398b-384">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="5398b-385">Paketlerde bulunan MSBuild props 'a başvurular</span><span class="sxs-lookup"><span data-stu-id="5398b-385">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="5398b-386">Paketlerde bulunan MSBuild hedeflerine başvurular</span><span class="sxs-lookup"><span data-stu-id="5398b-386">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="5398b-387">Tek bir MSBuild komutuyla geri yükleme ve oluşturma</span><span class="sxs-lookup"><span data-stu-id="5398b-387">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="5398b-388">NuGet, MSBuild hedeflerini ve props 'ı getiren paketleri geri yükleyebilir, geri yükleme ve derleme değerlendirmeleri farklı genel özelliklerle çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="5398b-388">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="5398b-389">Bu, aşağıdakilerin öngörülemeyen ve genellikle yanlış bir davranışa sahip olacağı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="5398b-389">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="5398b-390">Bunun yerine önerilen yaklaşım şunlardır:</span><span class="sxs-lookup"><span data-stu-id="5398b-390">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="5398b-391">Aynı Logic şuna benzer `build`diğer hedefler için de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="5398b-391">The same logic applies to other targets similar to `build`.</span></span>

### <a name="packagetargetfallback"></a><span data-ttu-id="5398b-392">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="5398b-392">PackageTargetFallback</span></span>

<span data-ttu-id="5398b-393">Öğesi `PackageTargetFallback` , paketler geri yüklenirken kullanılacak bir dizi uyumlu hedef belirtmenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="5398b-393">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="5398b-394">DotNet [TXD](../reference/target-frameworks.md) kullanan paketlere, DotNet TXD bildirmeyin uyumlu paketlerle çalışmak üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="5398b-394">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="5398b-395">Diğer bir deyişle, projeniz DotNet TXI kullanıyorsa, bu durumda, `<PackageTargetFallback>` DotNet olmayan platformların DotNet ile uyumlu olmasını sağlamak için projeye eklemediğiniz sürece bağımlı olduğu tüm paketler DotNet TXD olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5398b-395">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="5398b-396">Örneğin, proje `netstandard1.6` TXI kullanıyorsa ve bağımlı bir paket yalnızca `lib/net45/a.dll` ve `lib/portable-net45+win81/a.dll`içeriyorsa, proje derlenmeyecektir.</span><span class="sxs-lookup"><span data-stu-id="5398b-396">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="5398b-397">İçine getirmek istediğiniz değer ikinci dll ise, `PackageTargetFallback` `portable-net45+win81` dll 'nin uyumlu olduğunu söylemek için aşağıdaki gibi bir ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5398b-397">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="5398b-398">Projenizdeki tüm hedeflere yönelik bir geri dönüş bildirmek için, `Condition` özniteliği devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="5398b-398">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="5398b-399">Ayrıca, burada gösterildiği `PackageTargetFallback` `$(PackageTargetFallback)` gibi, var olan varsa de genişletebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5398b-399">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="5398b-400">Bir geri yükleme grafiğinden bir kitaplığı değiştirme</span><span class="sxs-lookup"><span data-stu-id="5398b-400">Replacing one library from a restore graph</span></span>

<span data-ttu-id="5398b-401">Geri yükleme yanlış derlemeyi alıyorsa, bu paketlerin varsayılan seçeneğini hariç tutabilir ve kendi seçimiyle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="5398b-401">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="5398b-402">Birincisi, en üst düzeyle `PackageReference`, tüm varlıkları hariç tut:</span><span class="sxs-lookup"><span data-stu-id="5398b-402">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="5398b-403">Ardından, DLL 'nin uygun yerel kopyasına kendi başvurunuz ekleyin:</span><span class="sxs-lookup"><span data-stu-id="5398b-403">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
