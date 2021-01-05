---
title: NuGet paketi ve geri yükleme MSBuild hedefleri olarak
description: NuGet paketi ve geri yükleme, NuGet 4.0 + ile doğrudan MSBuild hedefleri olarak çalışabilir.
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 66df4e0e4739300608fd5f9e44eea5bcd00079c8
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699893"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="7d379-103">NuGet paketi ve geri yükleme MSBuild hedefleri olarak</span><span class="sxs-lookup"><span data-stu-id="7d379-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="7d379-104">*NuGet 4.0 +*</span><span class="sxs-lookup"><span data-stu-id="7d379-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="7d379-105">[Packagereference](../consume-packages/package-references-in-project-files.md) biçimi sayesinde, NuGet 4.0 + tüm bildirim meta verilerini ayrı bir dosya kullanmak yerine doğrudan proje dosyası içinde depolayabilirler `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="7d379-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="7d379-106">MSBuild 15.1 + ile NuGet, `pack` aşağıda açıklandığı gibi, ve hedefleri ile birinci sınıf MSBuild vatandaşlık da vardır `restore` .</span><span class="sxs-lookup"><span data-stu-id="7d379-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="7d379-107">Bu hedefler, diğer herhangi bir MSBuild görevi veya hedefi ile yaptığınız gibi NuGet ile çalışmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="7d379-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="7d379-108">MSBuild kullanarak bir NuGet paketi oluşturma yönergeleri için bkz. [MSBuild kullanarak NuGet paketi oluşturma](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="7d379-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="7d379-109">(NuGet 3. x ve öncesi için, bunun yerine NuGet CLı aracılığıyla [paketle](../reference/cli-reference/cli-ref-pack.md) ve [geri yükleme](../reference/cli-reference/cli-ref-restore.md) komutlarını kullanırsınız.)</span><span class="sxs-lookup"><span data-stu-id="7d379-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="7d379-110">Hedef derleme sırası</span><span class="sxs-lookup"><span data-stu-id="7d379-110">Target build order</span></span>

<span data-ttu-id="7d379-111">`pack`Ve `restore` MSBuild hedefleri olduğundan, iş akışınızı geliştirmek için bunlara erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d379-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="7d379-112">Örneğin, paketledikten sonra paketinizi bir ağ paylaşımında kopyalamak istediğinizi varsayalım.</span><span class="sxs-lookup"><span data-stu-id="7d379-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="7d379-113">Bunu, proje dosyanıza aşağıdakileri ekleyerek yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7d379-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="7d379-114">Benzer şekilde, MSBuild görevinde bir MSBuild görevi yazabilir, kendi hedefini yazabilir ve NuGet özelliklerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d379-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="7d379-115">`$(OutputPath)` görelidir ve bu komutu proje kökünden çalıştırdığınız için bekliyor.</span><span class="sxs-lookup"><span data-stu-id="7d379-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="7d379-116">paket hedefi</span><span class="sxs-lookup"><span data-stu-id="7d379-116">pack target</span></span>

<span data-ttu-id="7d379-117">PackageReference biçimini kullanan .NET Standard projeler için, `msbuild -t:pack` bir NuGet paketi oluştururken kullanılacak proje dosyasından girişler çizer.</span><span class="sxs-lookup"><span data-stu-id="7d379-117">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="7d379-118">Aşağıdaki tabloda, ilk düğüm içindeki bir proje dosyasına eklenebilen MSBuild özellikleri açıklanmaktadır `<PropertyGroup>` .</span><span class="sxs-lookup"><span data-stu-id="7d379-118">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="7d379-119">Bu düzenlemeleri Visual Studio 2017 ve sonraki sürümlerde kolayca yaparak, projeye sağ tıklayıp bağlam menüsünde **{Project_Name} Düzenle** ' yi seçerek yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d379-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="7d379-120">Kolaylık olması için tablo, bir [ `.nuspec` dosyadaki](../reference/nuspec.md)denk özelliğe göre düzenlenir.</span><span class="sxs-lookup"><span data-stu-id="7d379-120">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="7d379-121">`Owners`Ve `Summary` özelliklerinin `.nuspec` MSBuild ile desteklenmediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="7d379-121">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="7d379-122">Öznitelik/NuSpec değeri</span><span class="sxs-lookup"><span data-stu-id="7d379-122">Attribute/NuSpec Value</span></span> | <span data-ttu-id="7d379-123">MSBuild özelliği</span><span class="sxs-lookup"><span data-stu-id="7d379-123">MSBuild Property</span></span> | <span data-ttu-id="7d379-124">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="7d379-124">Default</span></span> | <span data-ttu-id="7d379-125">Notlar</span><span class="sxs-lookup"><span data-stu-id="7d379-125">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="7d379-126">Id</span><span class="sxs-lookup"><span data-stu-id="7d379-126">Id</span></span> | <span data-ttu-id="7d379-127">PackageID</span><span class="sxs-lookup"><span data-stu-id="7d379-127">PackageId</span></span> | <span data-ttu-id="7d379-128">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="7d379-128">AssemblyName</span></span> | <span data-ttu-id="7d379-129">MSBuild 'ten $ (AssemblyName)</span><span class="sxs-lookup"><span data-stu-id="7d379-129">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="7d379-130">Sürüm</span><span class="sxs-lookup"><span data-stu-id="7d379-130">Version</span></span> | <span data-ttu-id="7d379-131">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="7d379-131">PackageVersion</span></span> | <span data-ttu-id="7d379-132">Sürüm</span><span class="sxs-lookup"><span data-stu-id="7d379-132">Version</span></span> | <span data-ttu-id="7d379-133">Bu semver uyumludur, örneğin "1.0.0", "1.0.0-Beta" veya "1.0.0-Beta-00345"</span><span class="sxs-lookup"><span data-stu-id="7d379-133">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="7d379-134">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="7d379-134">VersionPrefix</span></span> | <span data-ttu-id="7d379-135">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="7d379-135">PackageVersionPrefix</span></span> | <span data-ttu-id="7d379-136">empty</span><span class="sxs-lookup"><span data-stu-id="7d379-136">empty</span></span> | <span data-ttu-id="7d379-137">PackageVersion ayarı PackageVersionPrefix üzerine yazıyor</span><span class="sxs-lookup"><span data-stu-id="7d379-137">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="7d379-138">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="7d379-138">VersionSuffix</span></span> | <span data-ttu-id="7d379-139">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="7d379-139">PackageVersionSuffix</span></span> | <span data-ttu-id="7d379-140">empty</span><span class="sxs-lookup"><span data-stu-id="7d379-140">empty</span></span> | <span data-ttu-id="7d379-141">MSBuild 'ten $ (VersionSuffix).</span><span class="sxs-lookup"><span data-stu-id="7d379-141">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="7d379-142">PackageVersion ayarı PackageVersionSuffix üzerine yazıyor</span><span class="sxs-lookup"><span data-stu-id="7d379-142">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="7d379-143">Yazarlar</span><span class="sxs-lookup"><span data-stu-id="7d379-143">Authors</span></span> | <span data-ttu-id="7d379-144">Yazarlar</span><span class="sxs-lookup"><span data-stu-id="7d379-144">Authors</span></span> | <span data-ttu-id="7d379-145">Geçerli kullanıcının Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="7d379-145">Username of the current user</span></span> | |
| <span data-ttu-id="7d379-146">Sahipler</span><span class="sxs-lookup"><span data-stu-id="7d379-146">Owners</span></span> | <span data-ttu-id="7d379-147">Yok</span><span class="sxs-lookup"><span data-stu-id="7d379-147">N/A</span></span> | <span data-ttu-id="7d379-148">NuSpec içinde yok</span><span class="sxs-lookup"><span data-stu-id="7d379-148">Not present in NuSpec</span></span> | |
| <span data-ttu-id="7d379-149">Title</span><span class="sxs-lookup"><span data-stu-id="7d379-149">Title</span></span> | <span data-ttu-id="7d379-150">Title</span><span class="sxs-lookup"><span data-stu-id="7d379-150">Title</span></span> | <span data-ttu-id="7d379-151">PackageID</span><span class="sxs-lookup"><span data-stu-id="7d379-151">The PackageId</span></span>| |
| <span data-ttu-id="7d379-152">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7d379-152">Description</span></span> | <span data-ttu-id="7d379-153">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7d379-153">Description</span></span> | <span data-ttu-id="7d379-154">"Paket açıklaması"</span><span class="sxs-lookup"><span data-stu-id="7d379-154">"Package Description"</span></span> | |
| <span data-ttu-id="7d379-155">Telif Hakkı</span><span class="sxs-lookup"><span data-stu-id="7d379-155">Copyright</span></span> | <span data-ttu-id="7d379-156">Telif Hakkı</span><span class="sxs-lookup"><span data-stu-id="7d379-156">Copyright</span></span> | <span data-ttu-id="7d379-157">empty</span><span class="sxs-lookup"><span data-stu-id="7d379-157">empty</span></span> | |
| <span data-ttu-id="7d379-158">Requirelicensekabulünü</span><span class="sxs-lookup"><span data-stu-id="7d379-158">RequireLicenseAcceptance</span></span> | <span data-ttu-id="7d379-159">Packagerequirelicensekabulünü</span><span class="sxs-lookup"><span data-stu-id="7d379-159">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="7d379-160">yanlış</span><span class="sxs-lookup"><span data-stu-id="7d379-160">false</span></span> | |
| <span data-ttu-id="7d379-161">lisans</span><span class="sxs-lookup"><span data-stu-id="7d379-161">license</span></span> | <span data-ttu-id="7d379-162">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="7d379-162">PackageLicenseExpression</span></span> | <span data-ttu-id="7d379-163">empty</span><span class="sxs-lookup"><span data-stu-id="7d379-163">empty</span></span> | <span data-ttu-id="7d379-164">Karşılık gelen `<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="7d379-164">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="7d379-165">lisans</span><span class="sxs-lookup"><span data-stu-id="7d379-165">license</span></span> | <span data-ttu-id="7d379-166">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="7d379-166">PackageLicenseFile</span></span> | <span data-ttu-id="7d379-167">empty</span><span class="sxs-lookup"><span data-stu-id="7d379-167">empty</span></span> | <span data-ttu-id="7d379-168">Öğesine karşılık gelir `<license type="file">` .</span><span class="sxs-lookup"><span data-stu-id="7d379-168">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="7d379-169">Başvurulan lisans dosyasını açık bir şekilde paketetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d379-169">You need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="7d379-170">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="7d379-170">LicenseUrl</span></span> | <span data-ttu-id="7d379-171">PackageLicenseUrl 'Si</span><span class="sxs-lookup"><span data-stu-id="7d379-171">PackageLicenseUrl</span></span> | <span data-ttu-id="7d379-172">empty</span><span class="sxs-lookup"><span data-stu-id="7d379-172">empty</span></span> | <span data-ttu-id="7d379-173">`PackageLicenseUrl` kullanım dışı, PackageLicenseExpression veya PackageLicenseFile özelliğini kullanın</span><span class="sxs-lookup"><span data-stu-id="7d379-173">`PackageLicenseUrl` is deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="7d379-174">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="7d379-174">ProjectUrl</span></span> | <span data-ttu-id="7d379-175">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="7d379-175">PackageProjectUrl</span></span> | <span data-ttu-id="7d379-176">empty</span><span class="sxs-lookup"><span data-stu-id="7d379-176">empty</span></span> | |
| <span data-ttu-id="7d379-177">Simge</span><span class="sxs-lookup"><span data-stu-id="7d379-177">Icon</span></span> | <span data-ttu-id="7d379-178">Packageıcon</span><span class="sxs-lookup"><span data-stu-id="7d379-178">PackageIcon</span></span> | <span data-ttu-id="7d379-179">empty</span><span class="sxs-lookup"><span data-stu-id="7d379-179">empty</span></span> | <span data-ttu-id="7d379-180">Başvurulan simge görüntü dosyasını açıkça paketetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d379-180">You need to explicitly pack the referenced icon image file.</span></span>|
| <span data-ttu-id="7d379-181">Iurl</span><span class="sxs-lookup"><span data-stu-id="7d379-181">IconUrl</span></span> | <span data-ttu-id="7d379-182">PackageIconUrl 'Si</span><span class="sxs-lookup"><span data-stu-id="7d379-182">PackageIconUrl</span></span> | <span data-ttu-id="7d379-183">empty</span><span class="sxs-lookup"><span data-stu-id="7d379-183">empty</span></span> | <span data-ttu-id="7d379-184">En iyi alt düzey deneyim için `PackageIconUrl` öğesine ek olarak belirtilmelidir `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="7d379-184">For the best downlevel experience, `PackageIconUrl` should be specified in addition to `PackageIcon`.</span></span> <span data-ttu-id="7d379-185">Daha uzun vadeli `PackageIconUrl` kullanım dışı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7d379-185">Longer term, `PackageIconUrl` will be deprecated.</span></span> |
| <span data-ttu-id="7d379-186">Etiketler</span><span class="sxs-lookup"><span data-stu-id="7d379-186">Tags</span></span> | <span data-ttu-id="7d379-187">PackageTags</span><span class="sxs-lookup"><span data-stu-id="7d379-187">PackageTags</span></span> | <span data-ttu-id="7d379-188">empty</span><span class="sxs-lookup"><span data-stu-id="7d379-188">empty</span></span> | <span data-ttu-id="7d379-189">Etiketler noktalı virgülle ayrılır.</span><span class="sxs-lookup"><span data-stu-id="7d379-189">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="7d379-190">Relet 'ler</span><span class="sxs-lookup"><span data-stu-id="7d379-190">ReleaseNotes</span></span> | <span data-ttu-id="7d379-191">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="7d379-191">PackageReleaseNotes</span></span> | <span data-ttu-id="7d379-192">empty</span><span class="sxs-lookup"><span data-stu-id="7d379-192">empty</span></span> | |
| <span data-ttu-id="7d379-193">Depo/URL</span><span class="sxs-lookup"><span data-stu-id="7d379-193">Repository/Url</span></span> | <span data-ttu-id="7d379-194">Depourl 'Si</span><span class="sxs-lookup"><span data-stu-id="7d379-194">RepositoryUrl</span></span> | <span data-ttu-id="7d379-195">empty</span><span class="sxs-lookup"><span data-stu-id="7d379-195">empty</span></span> | <span data-ttu-id="7d379-196">Kaynak kodu kopyalamak veya almak için kullanılan depo URL 'SI.</span><span class="sxs-lookup"><span data-stu-id="7d379-196">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="7d379-197">Örneğinde *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="7d379-197">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="7d379-198">Depo/tür</span><span class="sxs-lookup"><span data-stu-id="7d379-198">Repository/Type</span></span> | <span data-ttu-id="7d379-199">Repositorytype parametrelerinin sağlanması</span><span class="sxs-lookup"><span data-stu-id="7d379-199">RepositoryType</span></span> | <span data-ttu-id="7d379-200">empty</span><span class="sxs-lookup"><span data-stu-id="7d379-200">empty</span></span> | <span data-ttu-id="7d379-201">Depo türü.</span><span class="sxs-lookup"><span data-stu-id="7d379-201">Repository type.</span></span> <span data-ttu-id="7d379-202">Örnekler: *Git*, *TFS*.</span><span class="sxs-lookup"><span data-stu-id="7d379-202">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="7d379-203">Depo/dal</span><span class="sxs-lookup"><span data-stu-id="7d379-203">Repository/Branch</span></span> | <span data-ttu-id="7d379-204">Depodalı</span><span class="sxs-lookup"><span data-stu-id="7d379-204">RepositoryBranch</span></span> | <span data-ttu-id="7d379-205">empty</span><span class="sxs-lookup"><span data-stu-id="7d379-205">empty</span></span> | <span data-ttu-id="7d379-206">İsteğe bağlı depo dalı bilgileri.</span><span class="sxs-lookup"><span data-stu-id="7d379-206">Optional repository branch information.</span></span> <span data-ttu-id="7d379-207">Bu özelliğin dahil olması için aynı zamanda bir *Depo-URL* belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="7d379-207">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="7d379-208">Örnek: *Master* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="7d379-208">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="7d379-209">Depo/kayıt</span><span class="sxs-lookup"><span data-stu-id="7d379-209">Repository/Commit</span></span> | <span data-ttu-id="7d379-210">Kayıt yapma</span><span class="sxs-lookup"><span data-stu-id="7d379-210">RepositoryCommit</span></span> | <span data-ttu-id="7d379-211">empty</span><span class="sxs-lookup"><span data-stu-id="7d379-211">empty</span></span> | <span data-ttu-id="7d379-212">Paketin hangi kaynağa göre oluşturulduğunu göstermek için isteğe bağlı depo kaydı veya değişiklik kümesi.</span><span class="sxs-lookup"><span data-stu-id="7d379-212">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="7d379-213">Bu özelliğin dahil olması için aynı zamanda bir *Depo-URL* belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="7d379-213">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="7d379-214">Örnek: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="7d379-214">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="7d379-215">PackageType</span><span class="sxs-lookup"><span data-stu-id="7d379-215">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="7d379-216">Özet</span><span class="sxs-lookup"><span data-stu-id="7d379-216">Summary</span></span> | <span data-ttu-id="7d379-217">Desteklenmez</span><span class="sxs-lookup"><span data-stu-id="7d379-217">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="7d379-218">Paket hedef girişleri</span><span class="sxs-lookup"><span data-stu-id="7d379-218">pack target inputs</span></span>

- <span data-ttu-id="7d379-219">Ispackable</span><span class="sxs-lookup"><span data-stu-id="7d379-219">IsPackable</span></span>
- <span data-ttu-id="7d379-220">Suppressbağımlıcıeswhenpaketleme</span><span class="sxs-lookup"><span data-stu-id="7d379-220">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="7d379-221">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="7d379-221">PackageVersion</span></span>
- <span data-ttu-id="7d379-222">PackageID</span><span class="sxs-lookup"><span data-stu-id="7d379-222">PackageId</span></span>
- <span data-ttu-id="7d379-223">Yazarlar</span><span class="sxs-lookup"><span data-stu-id="7d379-223">Authors</span></span>
- <span data-ttu-id="7d379-224">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7d379-224">Description</span></span>
- <span data-ttu-id="7d379-225">Telif Hakkı</span><span class="sxs-lookup"><span data-stu-id="7d379-225">Copyright</span></span>
- <span data-ttu-id="7d379-226">Packagerequirelicensekabulünü</span><span class="sxs-lookup"><span data-stu-id="7d379-226">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="7d379-227">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="7d379-227">DevelopmentDependency</span></span>
- <span data-ttu-id="7d379-228">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="7d379-228">PackageLicenseExpression</span></span>
- <span data-ttu-id="7d379-229">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="7d379-229">PackageLicenseFile</span></span>
- <span data-ttu-id="7d379-230">PackageLicenseUrl 'Si</span><span class="sxs-lookup"><span data-stu-id="7d379-230">PackageLicenseUrl</span></span>
- <span data-ttu-id="7d379-231">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="7d379-231">PackageProjectUrl</span></span>
- <span data-ttu-id="7d379-232">PackageIconUrl 'Si</span><span class="sxs-lookup"><span data-stu-id="7d379-232">PackageIconUrl</span></span>
- <span data-ttu-id="7d379-233">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="7d379-233">PackageReleaseNotes</span></span>
- <span data-ttu-id="7d379-234">PackageTags</span><span class="sxs-lookup"><span data-stu-id="7d379-234">PackageTags</span></span>
- <span data-ttu-id="7d379-235">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="7d379-235">PackageOutputPath</span></span>
- <span data-ttu-id="7d379-236">Includesymbols</span><span class="sxs-lookup"><span data-stu-id="7d379-236">IncludeSymbols</span></span>
- <span data-ttu-id="7d379-237">Includesource</span><span class="sxs-lookup"><span data-stu-id="7d379-237">IncludeSource</span></span>
- <span data-ttu-id="7d379-238">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="7d379-238">PackageTypes</span></span>
- <span data-ttu-id="7d379-239">IsTool</span><span class="sxs-lookup"><span data-stu-id="7d379-239">IsTool</span></span>
- <span data-ttu-id="7d379-240">Depourl 'Si</span><span class="sxs-lookup"><span data-stu-id="7d379-240">RepositoryUrl</span></span>
- <span data-ttu-id="7d379-241">Repositorytype parametrelerinin sağlanması</span><span class="sxs-lookup"><span data-stu-id="7d379-241">RepositoryType</span></span>
- <span data-ttu-id="7d379-242">Depodalı</span><span class="sxs-lookup"><span data-stu-id="7d379-242">RepositoryBranch</span></span>
- <span data-ttu-id="7d379-243">Kayıt yapma</span><span class="sxs-lookup"><span data-stu-id="7d379-243">RepositoryCommit</span></span>
- <span data-ttu-id="7d379-244">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="7d379-244">NoPackageAnalysis</span></span>
- <span data-ttu-id="7d379-245">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="7d379-245">MinClientVersion</span></span>
- <span data-ttu-id="7d379-246">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="7d379-246">IncludeBuildOutput</span></span>
- <span data-ttu-id="7d379-247">Includecontentınpack</span><span class="sxs-lookup"><span data-stu-id="7d379-247">IncludeContentInPack</span></span>
- <span data-ttu-id="7d379-248">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="7d379-248">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="7d379-249">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="7d379-249">ContentTargetFolders</span></span>
- <span data-ttu-id="7d379-250">Nusguus dosyası</span><span class="sxs-lookup"><span data-stu-id="7d379-250">NuspecFile</span></span>
- <span data-ttu-id="7d379-251">Nusgubasepath</span><span class="sxs-lookup"><span data-stu-id="7d379-251">NuspecBasePath</span></span>
- <span data-ttu-id="7d379-252">Nus, Properties</span><span class="sxs-lookup"><span data-stu-id="7d379-252">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="7d379-253">paket senaryoları</span><span class="sxs-lookup"><span data-stu-id="7d379-253">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="7d379-254">Bağımlılıkları gösterme</span><span class="sxs-lookup"><span data-stu-id="7d379-254">Suppress dependencies</span></span>

<span data-ttu-id="7d379-255">Oluşturulan NuGet paketinden paket bağımlılıklarını bastırmak için, olarak ayarlayın `SuppressDependenciesWhenPacking` ve `true` oluşturulan nupkg dosyasından tüm bağımlılıkların atlanmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="7d379-255">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="7d379-256">PackageIconUrl 'Si</span><span class="sxs-lookup"><span data-stu-id="7d379-256">PackageIconUrl</span></span>

<span data-ttu-id="7d379-257">`PackageIconUrl` yeni özellik yararına kullanım dışı olacaktır [`PackageIcon`](#packageicon) .</span><span class="sxs-lookup"><span data-stu-id="7d379-257">`PackageIconUrl` will be deprecated in favor of the new [`PackageIcon`](#packageicon) property.</span></span>

<span data-ttu-id="7d379-258">NuGet 5,3 & Visual Studio 2019 sürüm 16,3 ' den itibaren, `pack` paket meta verileri yalnızca belirtiyorsa [NU5048](./errors-and-warnings/nu5048.md) uyarı verecek `PackageIconUrl` .</span><span class="sxs-lookup"><span data-stu-id="7d379-258">Starting with NuGet 5.3 & Visual Studio 2019 version 16.3, `pack` will raise [NU5048](./errors-and-warnings/nu5048.md) warning if the package metadata only specifies `PackageIconUrl`.</span></span>

### <a name="packageicon"></a><span data-ttu-id="7d379-259">Packageıcon</span><span class="sxs-lookup"><span data-stu-id="7d379-259">PackageIcon</span></span>

> [!Tip]
> <span data-ttu-id="7d379-260">`PackageIcon` `PackageIconUrl` Henüz desteklemeyen istemcilerle ve kaynaklarla geriye dönük uyumluluğu sürdürmek için ve ikisini de belirtmeniz gerekir `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="7d379-260">You should specify both `PackageIcon` and `PackageIconUrl` to maintain backward compatibility with clients and sources that do not yet support `PackageIcon`.</span></span> <span data-ttu-id="7d379-261">Visual Studio, `PackageIcon` gelecek sürümlerde klasör tabanlı bir kaynaktan gelen paketleri destekleyecektir.</span><span class="sxs-lookup"><span data-stu-id="7d379-261">Visual Studio will support `PackageIcon` for packages coming from a folder-based source in a future release.</span></span>

#### <a name="packing-an-icon-image-file"></a><span data-ttu-id="7d379-262">Simge görüntüsü dosyası paketleme</span><span class="sxs-lookup"><span data-stu-id="7d379-262">Packing an icon image file</span></span>

<span data-ttu-id="7d379-263">Bir simge resim dosyası paketleme sırasında, paketin `PackageIcon` köküne göre paket yolunu belirtmek için özelliğini kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d379-263">When packing an icon image file, you need to use `PackageIcon` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="7d379-264">Ayrıca, dosyanın pakete eklendiğinden emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d379-264">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="7d379-265">Görüntü dosyası boyutu 1 MB ile sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="7d379-265">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="7d379-266">Desteklenen dosya biçimleri JPEG ve PNG içerir.</span><span class="sxs-lookup"><span data-stu-id="7d379-266">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="7d379-267">128x128 görüntü çözümlemesi yapmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="7d379-267">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="7d379-268">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="7d379-268">For example:</span></span>

```xml
<PropertyGroup>
    ...
    <PackageIcon>icon.png</PackageIcon>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="images\icon.png" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

<span data-ttu-id="7d379-269">[Paket simgesi örneği](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span><span class="sxs-lookup"><span data-stu-id="7d379-269">[Package Icon sample](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span></span>

<span data-ttu-id="7d379-270">Nuspec eşdeğeri için, [simgenin nuspec başvurusuna](nuspec.md#icon)göz atın.</span><span class="sxs-lookup"><span data-stu-id="7d379-270">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="7d379-271">Çıkış derlemeleri</span><span class="sxs-lookup"><span data-stu-id="7d379-271">Output assemblies</span></span>

<span data-ttu-id="7d379-272">`nuget pack` çıktı dosyalarını,,,, ve uzantılarına kopyalar `.exe` `.dll` `.xml` `.winmd` `.json` `.pri` .</span><span class="sxs-lookup"><span data-stu-id="7d379-272">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="7d379-273">Kopyalanan çıkış dosyaları, hedef tarafından MSBuild 'in sağladığı şuna bağlıdır `BuiltOutputProjectGroup` .</span><span class="sxs-lookup"><span data-stu-id="7d379-273">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="7d379-274">Çıktı derlemelerinin nerede olduğunu denetlemek için, proje dosyanızda veya komut satırında kullanabileceğiniz iki MSBuild özelliği vardır:</span><span class="sxs-lookup"><span data-stu-id="7d379-274">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="7d379-275">`IncludeBuildOutput`: Derleme çıkış derlemelerinin pakete dahil edilip edilmeyeceğini belirleyen bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="7d379-275">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="7d379-276">`BuildOutputTargetFolder`: Çıkış derlemelerinin yerleştirilmesi gereken klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="7d379-276">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="7d379-277">Çıkış derlemeleri (ve diğer çıkış dosyaları) ilgili çerçeve klasörlerine kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="7d379-277">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="7d379-278">Paket başvuruları</span><span class="sxs-lookup"><span data-stu-id="7d379-278">Package references</span></span>

<span data-ttu-id="7d379-279">Bkz. [Proje dosyalarındaki paket başvuruları](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="7d379-279">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="7d379-280">Projeden projeye başvurular</span><span class="sxs-lookup"><span data-stu-id="7d379-280">Project to project references</span></span>

<span data-ttu-id="7d379-281">Proje başvuruları, varsayılan olarak NuGet paket başvuruları olarak değerlendirilir, örneğin:</span><span class="sxs-lookup"><span data-stu-id="7d379-281">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="7d379-282">Ayrıca, proje başvurunuz için aşağıdaki meta verileri de ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7d379-282">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="7d379-283">Bir paketteki içerik ekleme</span><span class="sxs-lookup"><span data-stu-id="7d379-283">Including content in a package</span></span>

<span data-ttu-id="7d379-284">İçerik eklemek için var olan öğeye ek meta veriler ekleyin `<Content>` .</span><span class="sxs-lookup"><span data-stu-id="7d379-284">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="7d379-285">Varsayılan olarak, aşağıdaki gibi girdilerle geçersiz kılmadığınız müddetçe "Içerik" türünde her şey pakete dahil edilir:</span><span class="sxs-lookup"><span data-stu-id="7d379-285">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="7d379-286">Varsayılan olarak, her şey `content` `contentFiles\any\<target_framework>` bir paket içindeki ve klasörünün köküne eklenir ve bir paket yolu belirtmediğiniz takdirde göreli klasör yapısını korur:</span><span class="sxs-lookup"><span data-stu-id="7d379-286">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="7d379-287">Tüm içeriğinizi yalnızca belirli bir kök klasöre ( `content` ve her ikisi yerine) kopyalamak istiyorsanız, `contentFiles` Varsayılan olarak `ContentTargetFolders` "Content; ContentFiles" olan, ancak başka bir klasör adına ayarlanabilir MSBuild özelliğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d379-287">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="7d379-288">Yalnızca `ContentTargetFolders` dosyaları ' ın altında `contentFiles\any\<target_framework>` veya `contentFiles\<language>\<target_framework>` temel alarak "ContentFiles" seçeneğinin belirtildiğine unutmayın `buildAction` .</span><span class="sxs-lookup"><span data-stu-id="7d379-288">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="7d379-289">`PackagePath` noktalı virgülle ayrılmış bir hedef yolları kümesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="7d379-289">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="7d379-290">Boş bir paket yolu belirtilmesi, dosyayı paketin köküne ekler.</span><span class="sxs-lookup"><span data-stu-id="7d379-290">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="7d379-291">Örneğin, aşağıdaki, `libuv.txt` `content\myfiles` `content\samples` ve paket köküne ekler:</span><span class="sxs-lookup"><span data-stu-id="7d379-291">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="7d379-292">Ayrıca `$(IncludeContentInPack)` , varsayılan olarak olan MSBuild özelliği de vardır `true` .</span><span class="sxs-lookup"><span data-stu-id="7d379-292">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="7d379-293">Bu, `false` herhangi bir projede olarak ayarlandıysa, bu projeden içerik NuGet paketine dahil edilmez.</span><span class="sxs-lookup"><span data-stu-id="7d379-293">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="7d379-294">Yukarıdaki öğelerin herhangi birine ayarlayabileceğiniz diğer paketine özgü meta veriler içerir ```<PackageCopyToOutput>``` ve ```<PackageFlatten>``` ```CopyToOutput``` ```Flatten``` ```contentFiles``` Çıkış nuspec içindeki giriş üzerinde ve değerlerini belirler.</span><span class="sxs-lookup"><span data-stu-id="7d379-294">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="7d379-295">Içerik öğelerinden ayrı olarak, `<Pack>` ve `<PackagePath>` meta veriler de derleme, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, Designdata, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, Paketleresource veya None derleme eylemine sahip dosyalar üzerinde de ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="7d379-295">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="7d379-296">Glob desenleri kullanılırken dosya adını paket yolunuza eklemek için paket yolu, klasör ayırıcı karakteriyle bitmelidir; Aksi takdirde, paket yolu dosya adı dahil tam yol olarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="7d379-296">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="7d379-297">Includesymbols</span><span class="sxs-lookup"><span data-stu-id="7d379-297">IncludeSymbols</span></span>

<span data-ttu-id="7d379-298">Kullanırken `MSBuild -t:pack -p:IncludeSymbols=true` , karşılık gelen `.pdb` dosyalar diğer çıkış dosyalarıyla birlikte kopyalanır ( `.dll` ,,, `.exe` `.winmd` `.xml` , `.json` , `.pri` ).</span><span class="sxs-lookup"><span data-stu-id="7d379-298">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="7d379-299">Ayarın `IncludeSymbols=true` düzenli bir paket *ve* bir semboller paketi oluşturduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="7d379-299">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="7d379-300">Includesource</span><span class="sxs-lookup"><span data-stu-id="7d379-300">IncludeSource</span></span>

<span data-ttu-id="7d379-301">Bu, `IncludeSymbols` ile aynıdır, ancak kaynak dosyalarını da dosyalarla birlikte kopyalar `.pdb` .</span><span class="sxs-lookup"><span data-stu-id="7d379-301">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="7d379-302">Tüm dosya türleri, `Compile` `src\<ProjectName>\` elde edilen paketteki göreli yol klasörü yapısını korumak için üzerine kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="7d379-302">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="7d379-303">Aynı zamanda, olarak ayarlanmış herhangi bir kaynak dosyası için de aynı olur `ProjectReference` `TreatAsPackageReference` `false` .</span><span class="sxs-lookup"><span data-stu-id="7d379-303">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="7d379-304">Derleme türü bir dosya proje klasörünün dışında ise, ' ye eklenmiştir `src\<ProjectName>\` .</span><span class="sxs-lookup"><span data-stu-id="7d379-304">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="7d379-305">Lisans ifadesi veya lisans dosyası paketleme</span><span class="sxs-lookup"><span data-stu-id="7d379-305">Packing a license expression or a license file</span></span>

<span data-ttu-id="7d379-306">Bir lisans ifadesi kullanılırken PackageLicenseExpression özelliğinin kullanılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d379-306">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="7d379-307">[Lisans ifadesi örneği](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="7d379-307">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="7d379-308">[NuGet.org tarafından kabul edilen lisans ifadeleri ve lisanslar hakkında daha fazla bilgi edinin](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="7d379-308">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="7d379-309">Bir lisans dosyası paketleme sırasında, paketin köküne göre paket yolunu belirtmek için PackageLicenseFile özelliğini kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d379-309">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="7d379-310">Ayrıca, dosyanın pakete eklendiğinden emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d379-310">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="7d379-311">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="7d379-311">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="7d379-312">[Lisans dosyası örneği](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="7d379-312">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="packing-a-file-without-an-extension"></a><span data-ttu-id="7d379-313">Uzantı olmadan dosya paketleme</span><span class="sxs-lookup"><span data-stu-id="7d379-313">Packing a file without an extension</span></span>

<span data-ttu-id="7d379-314">Bir lisans dosyası paketleme gibi bazı senaryolarda, uzantısı olmayan bir dosya eklemek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d379-314">In some scenarios, like when packing a license file, you might want to include a file without an extension.</span></span>
<span data-ttu-id="7d379-315">Geçmiş nedenlerle NuGet & MSBuild, bir uzantısı olmayan yolları dizin olarak değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="7d379-315">For historical reasons, NuGet & MSBuild treat paths without an extension as directories.</span></span>

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

<span data-ttu-id="7d379-316">[Dosya uzantı örneği olmadan](https://github.com/NuGet/Samples/blob/master/PackageLicenseFileExtensionlessExample/).</span><span class="sxs-lookup"><span data-stu-id="7d379-316">[File without an extension sample](https://github.com/NuGet/Samples/blob/master/PackageLicenseFileExtensionlessExample/).</span></span>
### <a name="istool"></a><span data-ttu-id="7d379-317">IsTool</span><span class="sxs-lookup"><span data-stu-id="7d379-317">IsTool</span></span>

<span data-ttu-id="7d379-318">Kullanırken `MSBuild -t:pack -p:IsTool=true` , [Çıkış derlemeleri](#output-assemblies) senaryosunda belirtilen tüm çıkış dosyaları, `tools` klasörü yerine klasörüne kopyalanır `lib` .</span><span class="sxs-lookup"><span data-stu-id="7d379-318">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="7d379-319">Bunun, `DotNetCliTool` içindeki dosyasını ayarlayarak belirtilen öğesinden farklı olduğunu unutmayın `PackageType` `.csproj` .</span><span class="sxs-lookup"><span data-stu-id="7d379-319">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="7d379-320">. Nuspec kullanarak paketleme</span><span class="sxs-lookup"><span data-stu-id="7d379-320">Packing using a .nuspec</span></span>

<span data-ttu-id="7d379-321">Bunun yerine genellikle proje dosyasındaki dosyada bulunan [tüm özellikleri eklemeniz](../reference/msbuild-targets.md#pack-target) önerilse de `.nuspec` , `.nuspec` projenizi paketlebilmeniz için bir dosya kullanmayı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d379-321">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="7d379-322">Tarafından kullanılan SDK olmayan bir proje için `PackageReference` , paket görevinin yürütülebilmesi için içeri aktarmanız gerekir `NuGet.Build.Tasks.Pack.targets` .</span><span class="sxs-lookup"><span data-stu-id="7d379-322">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="7d379-323">Bir nuspec dosyası paketetmeden önce projeyi geri yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d379-323">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="7d379-324">(SDK stili bir proje varsayılan olarak paket hedeflerini içerir.)</span><span class="sxs-lookup"><span data-stu-id="7d379-324">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="7d379-325">Proje dosyasının hedef çerçevesi ilgisizdir ve bir nuspec paketleme sırasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="7d379-325">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="7d379-326">Aşağıdaki üç MSBuild özelliği, ile paketleme ile ilgilidir `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="7d379-326">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="7d379-327">`NuspecFile`: `.nuspec` paketleme için kullanılan dosyanın göreli veya mutlak yolu.</span><span class="sxs-lookup"><span data-stu-id="7d379-327">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="7d379-328">`NuspecProperties`: Key = değer çiftleri için noktalı virgülle ayrılmış bir liste.</span><span class="sxs-lookup"><span data-stu-id="7d379-328">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="7d379-329">MSBuild komut satırı ayrıştırması çalışma yöntemi nedeniyle, birden çok özellik şu şekilde belirtilmelidir: `-p:NuspecProperties="key1=value1;key2=value2"` .</span><span class="sxs-lookup"><span data-stu-id="7d379-329">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties="key1=value1;key2=value2"`.</span></span>  
1. <span data-ttu-id="7d379-330">`NuspecBasePath`: Dosyanın temel yolu `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="7d379-330">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="7d379-331">`dotnet.exe`Projenizi paketmek için kullanıyorsanız, aşağıdaki gibi bir komut kullanın:</span><span class="sxs-lookup"><span data-stu-id="7d379-331">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="7d379-332">Projenizi paketmek için MSBuild kullanıyorsanız, aşağıdaki gibi bir komut kullanın:</span><span class="sxs-lookup"><span data-stu-id="7d379-332">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="7d379-333">dotnet.exe veya MSBuild kullanarak bir nuspec paketleme, projenin varsayılan olarak oluşturulmasına da neden olduğuna lütfen emin olun.</span><span class="sxs-lookup"><span data-stu-id="7d379-333">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="7d379-334">Bu, proje dosyanızdaki ```--no-build``` ```<NoBuild>true</NoBuild> ``` ayar ile birlikte proje dosyanızdaki ayarın eşdeğeri olan dotnet.exe özelliği ' a geçirerek kaçınılabilir ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` .</span><span class="sxs-lookup"><span data-stu-id="7d379-334">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="7d379-335">Bir nuspec dosyası paketiçin bir *. csproj* dosyası örneği:</span><span class="sxs-lookup"><span data-stu-id="7d379-335">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="7d379-336">Özelleştirilmiş paket oluşturmak için gelişmiş uzantı noktaları</span><span class="sxs-lookup"><span data-stu-id="7d379-336">Advanced extension points to create customized package</span></span>

<span data-ttu-id="7d379-337">`pack`Hedef, iç, hedef çerçeveye özgü derlemede çalışan iki uzantı noktası sağlar.</span><span class="sxs-lookup"><span data-stu-id="7d379-337">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="7d379-338">Uzantı noktaları, hedef çerçeveye özgü içerik ve derlemelerin bir pakete dahil edilmesi için destek:</span><span class="sxs-lookup"><span data-stu-id="7d379-338">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="7d379-339">`TargetsForTfmSpecificBuildOutput` target: klasör içindeki dosyaları `lib` veya kullanılarak belirtilen klasörü kullanın `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="7d379-339">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="7d379-340">`TargetsForTfmSpecificContentInPackage` target: dışındaki dosyalar için kullanın `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="7d379-340">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="7d379-341">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="7d379-341">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="7d379-342">Özel bir hedef yazın ve özelliğin değeri olarak belirtin `$(TargetsForTfmSpecificBuildOutput)` .</span><span class="sxs-lookup"><span data-stu-id="7d379-342">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="7d379-343">(Varsayılan olarak LIB) öğesine gitmesi gereken tüm dosyalar için `BuildOutputTargetFolder` , hedef bu dosyaları ItemGroup 'a yazmalıdır `BuildOutputInPackage` ve aşağıdaki iki meta veri değerini ayarlamış olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="7d379-343">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="7d379-344">`FinalOutputPath`: Dosyanın mutlak yolu; sağlanmazsa, kimlik kaynak yolunu değerlendirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7d379-344">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="7d379-345">`TargetPath`: (İsteğe bağlı) dosyanın içindeki bir alt klasöre gitmesi gerektiğinde ayarlanır `lib\<TargetFramework>` . Bu, ilgili kültür klasörlerinin altına giten uydu derlemeleri gibi.</span><span class="sxs-lookup"><span data-stu-id="7d379-345">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="7d379-346">Varsayılan olarak dosyanın adıdır.</span><span class="sxs-lookup"><span data-stu-id="7d379-346">Defaults to the name of the file.</span></span>

<span data-ttu-id="7d379-347">Örnek:</span><span class="sxs-lookup"><span data-stu-id="7d379-347">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="7d379-348">Targetsfortfmspecificcontenınpackage</span><span class="sxs-lookup"><span data-stu-id="7d379-348">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="7d379-349">Özel bir hedef yazın ve özelliğin değeri olarak belirtin `$(TargetsForTfmSpecificContentInPackage)` .</span><span class="sxs-lookup"><span data-stu-id="7d379-349">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="7d379-350">Pakete dahil edilecek tüm dosyalar için, hedef bu dosyaları ItemGroup 'a yazmalıdır `TfmSpecificPackageFile` ve aşağıdaki isteğe bağlı meta verileri ayarlar:</span><span class="sxs-lookup"><span data-stu-id="7d379-350">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="7d379-351">`PackagePath`: Dosyanın pakette çıkış olması gereken yol.</span><span class="sxs-lookup"><span data-stu-id="7d379-351">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="7d379-352">Aynı paket yoluna birden fazla dosya eklenirse NuGet bir uyarı verir.</span><span class="sxs-lookup"><span data-stu-id="7d379-352">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="7d379-353">`BuildAction`: Dosyaya atanacak derleme eylemi, yalnızca paket yolu `contentFiles` klasörsise gereklidir.</span><span class="sxs-lookup"><span data-stu-id="7d379-353">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="7d379-354">Varsayılan "none" olarak belirlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="7d379-354">Defaults to "None".</span></span>

<span data-ttu-id="7d379-355">Örnek:</span><span class="sxs-lookup"><span data-stu-id="7d379-355">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="7d379-356">hedefi geri yükle</span><span class="sxs-lookup"><span data-stu-id="7d379-356">restore target</span></span>

<span data-ttu-id="7d379-357">`MSBuild -t:restore` ( `nuget restore` `dotnet restore` .NET Core projeleriyle birlikte kullanılması), proje dosyasında başvurulan paketleri aşağıdaki şekilde geri yükler:</span><span class="sxs-lookup"><span data-stu-id="7d379-357">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="7d379-358">Proje başvurularına tüm projeyi oku</span><span class="sxs-lookup"><span data-stu-id="7d379-358">Read all project to project references</span></span>
1. <span data-ttu-id="7d379-359">Ara klasörünü ve hedef çerçeveleri bulmak için proje özelliklerini okuyun</span><span class="sxs-lookup"><span data-stu-id="7d379-359">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="7d379-360">MSBuild verilerini NuGet.Build.Tasks.dll geçirin</span><span class="sxs-lookup"><span data-stu-id="7d379-360">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="7d379-361">Geri yüklemeyi Çalıştır</span><span class="sxs-lookup"><span data-stu-id="7d379-361">Run restore</span></span>
1. <span data-ttu-id="7d379-362">Paketleri İndir</span><span class="sxs-lookup"><span data-stu-id="7d379-362">Download packages</span></span>
1. <span data-ttu-id="7d379-363">Varlıklar dosyası, hedefler ve props yazma</span><span class="sxs-lookup"><span data-stu-id="7d379-363">Write assets file, targets, and props</span></span>

<span data-ttu-id="7d379-364">`restore`Hedef, PackageReference biçimini kullanan projeler için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="7d379-364">The `restore` target works for projects using the PackageReference format.</span></span>
<span data-ttu-id="7d379-365">`MSBuild 16.5+` Ayrıca, biçim için [kabul desteği](#restoring-packagereference-and-packagesconfig-with-msbuild) de vardır `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="7d379-365">`MSBuild 16.5+` also has [opt-in support](#restoring-packagereference-and-packagesconfig-with-msbuild) for the `packages.config` format.</span></span>

> [!NOTE]
> <span data-ttu-id="7d379-366">`restore`Hedef, hedefle birlikte [çalıştırılmamalıdır](#restoring-and-building-with-one-msbuild-command) `build` .</span><span class="sxs-lookup"><span data-stu-id="7d379-366">The `restore` target [should not be run](#restoring-and-building-with-one-msbuild-command) in combination with the `build` target.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="7d379-367">Özellikleri geri yükle</span><span class="sxs-lookup"><span data-stu-id="7d379-367">Restore properties</span></span>

<span data-ttu-id="7d379-368">Ek geri yükleme ayarları proje dosyasındaki MSBuild özelliklerinden gelebilir.</span><span class="sxs-lookup"><span data-stu-id="7d379-368">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="7d379-369">Değerler, anahtar kullanılarak komut satırından da ayarlanabilir `-p:` (aşağıdaki örneklere bakın).</span><span class="sxs-lookup"><span data-stu-id="7d379-369">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="7d379-370">Özellik</span><span class="sxs-lookup"><span data-stu-id="7d379-370">Property</span></span> | <span data-ttu-id="7d379-371">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7d379-371">Description</span></span> |
|--------|--------|
| <span data-ttu-id="7d379-372">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="7d379-372">RestoreSources</span></span> | <span data-ttu-id="7d379-373">Paket kaynaklarının noktalı virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="7d379-373">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="7d379-374">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="7d379-374">RestorePackagesPath</span></span> | <span data-ttu-id="7d379-375">Kullanıcı paketleri klasör yolu.</span><span class="sxs-lookup"><span data-stu-id="7d379-375">User packages folder path.</span></span> |
| <span data-ttu-id="7d379-376">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="7d379-376">RestoreDisableParallel</span></span> | <span data-ttu-id="7d379-377">İndirmeleri tek seferde bir ile sınırlayın.</span><span class="sxs-lookup"><span data-stu-id="7d379-377">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="7d379-378">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="7d379-378">RestoreConfigFile</span></span> | <span data-ttu-id="7d379-379">`Nuget.Config`Uygulanacak dosyanın yolu.</span><span class="sxs-lookup"><span data-stu-id="7d379-379">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="7d379-380">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="7d379-380">RestoreNoCache</span></span> | <span data-ttu-id="7d379-381">Doğru ise, önbelleğe alınmış paketlerin kullanılmasını önler.</span><span class="sxs-lookup"><span data-stu-id="7d379-381">If true, avoids using cached packages.</span></span> <span data-ttu-id="7d379-382">Bkz. [genel paketleri ve önbellek klasörlerini yönetme](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="7d379-382">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="7d379-383">Restoreıgnorefailedsources</span><span class="sxs-lookup"><span data-stu-id="7d379-383">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="7d379-384">Doğru ise, başarısız veya eksik paket kaynaklarını yoksayar.</span><span class="sxs-lookup"><span data-stu-id="7d379-384">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="7d379-385">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="7d379-385">RestoreFallbackFolders</span></span> | <span data-ttu-id="7d379-386">Geri dönüş klasörleri, Kullanıcı paketleri klasörüyle aynı şekilde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7d379-386">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="7d379-387">Restoreaddıtionalprojectsources</span><span class="sxs-lookup"><span data-stu-id="7d379-387">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="7d379-388">Geri yükleme sırasında kullanılacak ek kaynaklar.</span><span class="sxs-lookup"><span data-stu-id="7d379-388">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="7d379-389">Restoreaddıtionalprojectfallbackfolders</span><span class="sxs-lookup"><span data-stu-id="7d379-389">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="7d379-390">Geri yükleme sırasında kullanılacak ek geri dönüş klasörleri.</span><span class="sxs-lookup"><span data-stu-id="7d379-390">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="7d379-391">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="7d379-391">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="7d379-392">İçinde belirtilen geri dönüş klasörlerini dışlar `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="7d379-392">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="7d379-393">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="7d379-393">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="7d379-394">Yolu `NuGet.Build.Tasks.dll` .</span><span class="sxs-lookup"><span data-stu-id="7d379-394">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="7d379-395">Restoregraphprojectınput</span><span class="sxs-lookup"><span data-stu-id="7d379-395">RestoreGraphProjectInput</span></span> | <span data-ttu-id="7d379-396">Geri yüklenecek projelerin, mutlak yollar içermesi gereken, noktalı virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="7d379-396">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="7d379-397">Restoreuseskipnontenttargets</span><span class="sxs-lookup"><span data-stu-id="7d379-397">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="7d379-398">Projeler MSBuild aracılığıyla toplandığında, iyileştirme kullanılarak toplanıp toplanmayacağını belirler `SkipNonexistentTargets` .</span><span class="sxs-lookup"><span data-stu-id="7d379-398">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="7d379-399">Ayarlanmazsa, varsayılan olarak olur `true` .</span><span class="sxs-lookup"><span data-stu-id="7d379-399">When not set, defaults to `true`.</span></span> <span data-ttu-id="7d379-400">Projenin hedefleri içeri aktarılmadığı zaman, sonuç hızlı bir davranıştır.</span><span class="sxs-lookup"><span data-stu-id="7d379-400">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="7d379-401">Msbuildprojeclarsionspath</span><span class="sxs-lookup"><span data-stu-id="7d379-401">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="7d379-402">Çıkış klasörü, varsayılan olarak `BaseIntermediateOutputPath` ve `obj` klasörü.</span><span class="sxs-lookup"><span data-stu-id="7d379-402">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| <span data-ttu-id="7d379-403">Restorezorlamalı</span><span class="sxs-lookup"><span data-stu-id="7d379-403">RestoreForce</span></span> | <span data-ttu-id="7d379-404">PackageReference tabanlı projelerde, son geri yükleme başarılı olsa bile tüm bağımlılıkların çözülmesini zorlar.</span><span class="sxs-lookup"><span data-stu-id="7d379-404">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="7d379-405">Bu bayrağın belirtilmesi, dosyanın silinmesine benzer `project.assets.json` .</span><span class="sxs-lookup"><span data-stu-id="7d379-405">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="7d379-406">Bu, http-cache ' i atlar.</span><span class="sxs-lookup"><span data-stu-id="7d379-406">This does not bypass the http-cache.</span></span> |
| <span data-ttu-id="7d379-407">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="7d379-407">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="7d379-408">Bir kilit dosyasının kullanımıyla ilgili olarak.</span><span class="sxs-lookup"><span data-stu-id="7d379-408">Opts into the usage of a lock file.</span></span> |
| <span data-ttu-id="7d379-409">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="7d379-409">RestoreLockedMode</span></span> | <span data-ttu-id="7d379-410">Geri yüklemeyi kilitli modda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7d379-410">Run restore in locked mode.</span></span> <span data-ttu-id="7d379-411">Bu, geri yüklemenin bağımlılıkları yeniden değerlendirmeyeceği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="7d379-411">This means that restore will not reevaluate the dependencies.</span></span> |
| <span data-ttu-id="7d379-412">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="7d379-412">NuGetLockFilePath</span></span> | <span data-ttu-id="7d379-413">Kilit dosyası için özel bir konum.</span><span class="sxs-lookup"><span data-stu-id="7d379-413">A custom location for the lock file.</span></span> <span data-ttu-id="7d379-414">Varsayılan konum projenin yanında bulunur ve adlandırılır `packages.lock.json` .</span><span class="sxs-lookup"><span data-stu-id="7d379-414">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| <span data-ttu-id="7d379-415">Restoreforcedeğerlendir</span><span class="sxs-lookup"><span data-stu-id="7d379-415">RestoreForceEvaluate</span></span> | <span data-ttu-id="7d379-416">Bağımlılıkları yeniden hesaplamak ve herhangi bir uyarı olmadan kilit dosyasını güncelleştirmek için geri yüklemeyi zorlar.</span><span class="sxs-lookup"><span data-stu-id="7d379-416">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> |
| <span data-ttu-id="7d379-417">RestorePackagesConfig</span><span class="sxs-lookup"><span data-stu-id="7d379-417">RestorePackagesConfig</span></span> | <span data-ttu-id="7d379-418">packages.config olan projeleri geri yükleyen bir kabul etme anahtarı. Yalnızca ile desteklenir `MSBuild -t:restore` .</span><span class="sxs-lookup"><span data-stu-id="7d379-418">An opt in switch, that restores projects with packages.config. Support with `MSBuild -t:restore` only.</span></span> |

#### <a name="examples"></a><span data-ttu-id="7d379-419">Örnekler</span><span class="sxs-lookup"><span data-stu-id="7d379-419">Examples</span></span>

<span data-ttu-id="7d379-420">Komut satırı:</span><span class="sxs-lookup"><span data-stu-id="7d379-420">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="7d379-421">Proje dosyası:</span><span class="sxs-lookup"><span data-stu-id="7d379-421">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="7d379-422">Çıkışları geri yükleme</span><span class="sxs-lookup"><span data-stu-id="7d379-422">Restore outputs</span></span>

<span data-ttu-id="7d379-423">Restore derleme klasöründe aşağıdaki dosyaları oluşturur `obj` :</span><span class="sxs-lookup"><span data-stu-id="7d379-423">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="7d379-424">Dosya</span><span class="sxs-lookup"><span data-stu-id="7d379-424">File</span></span> | <span data-ttu-id="7d379-425">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7d379-425">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="7d379-426">Tüm paket başvurularının bağımlılık grafiğini içerir.</span><span class="sxs-lookup"><span data-stu-id="7d379-426">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="7d379-427">Paketlerde bulunan MSBuild props 'a başvurular</span><span class="sxs-lookup"><span data-stu-id="7d379-427">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="7d379-428">Paketlerde bulunan MSBuild hedeflerine başvurular</span><span class="sxs-lookup"><span data-stu-id="7d379-428">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="7d379-429">Tek bir MSBuild komutuyla geri yükleme ve oluşturma</span><span class="sxs-lookup"><span data-stu-id="7d379-429">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="7d379-430">NuGet, MSBuild hedeflerini ve props 'ı getiren paketleri geri yükleyebilir, geri yükleme ve derleme değerlendirmeleri farklı genel özelliklerle çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="7d379-430">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="7d379-431">Bu, aşağıdakilerin öngörülemeyen ve genellikle yanlış bir davranışa sahip olacağı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="7d379-431">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="7d379-432">Bunun yerine önerilen yaklaşım şunlardır:</span><span class="sxs-lookup"><span data-stu-id="7d379-432">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="7d379-433">Aynı Logic şuna benzer diğer hedefler için de geçerlidir `build` .</span><span class="sxs-lookup"><span data-stu-id="7d379-433">The same logic applies to other targets similar to `build`.</span></span>

### <a name="restoring-packagereference-and-packagesconfig-with-msbuild"></a><span data-ttu-id="7d379-434">MSBuild ile PackageReference ve packages.config geri yükleme</span><span class="sxs-lookup"><span data-stu-id="7d379-434">Restoring PackageReference and packages.config with MSBuild</span></span>

<span data-ttu-id="7d379-435">MSBuild 16.5 + ile packages.config de desteklenir `msbuild -t:restore` .</span><span class="sxs-lookup"><span data-stu-id="7d379-435">With MSBuild 16.5+, packages.config are also supported for `msbuild -t:restore`.</span></span>

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> <span data-ttu-id="7d379-436">`packages.config` restore yalnızca ile kullanılabilir `MSBuild 16.5+` ve `dotnet.exe`</span><span class="sxs-lookup"><span data-stu-id="7d379-436">`packages.config` restore is only available with `MSBuild 16.5+`, and not with `dotnet.exe`</span></span>

### <a name="packagetargetfallback"></a><span data-ttu-id="7d379-437">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="7d379-437">PackageTargetFallback</span></span>

<span data-ttu-id="7d379-438">`PackageTargetFallback`Öğesi, paketler geri yüklenirken kullanılacak bir dizi uyumlu hedef belirtmenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="7d379-438">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="7d379-439">DotNet [TXD](../reference/target-frameworks.md) kullanan paketlere, DotNet TXD bildirmeyin uyumlu paketlerle çalışmak üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="7d379-439">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="7d379-440">Diğer bir deyişle, projeniz DotNet TXI kullanıyorsa, bu durumda, `<PackageTargetFallback>` DotNet olmayan platformların DotNet ile uyumlu olmasını sağlamak için projeye eklemediğiniz sürece bağımlı olduğu tüm paketler DotNet TXD olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7d379-440">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="7d379-441">Örneğin, proje `netstandard1.6` TXI kullanıyorsa ve bağımlı bir paket yalnızca `lib/net45/a.dll` ve içeriyorsa `lib/portable-net45+win81/a.dll` , proje derlenmeyecektir.</span><span class="sxs-lookup"><span data-stu-id="7d379-441">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="7d379-442">İçine getirmek istediğiniz değer ikinci DLL ise, `PackageTargetFallback` DLL 'nin uyumlu olduğunu söylemek için aşağıdaki gibi bir ekleyebilirsiniz `portable-net45+win81` :</span><span class="sxs-lookup"><span data-stu-id="7d379-442">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="7d379-443">Projenizdeki tüm hedeflere yönelik bir geri dönüş bildirmek için, özniteliği devre dışı bırakın `Condition` .</span><span class="sxs-lookup"><span data-stu-id="7d379-443">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="7d379-444">Ayrıca, `PackageTargetFallback` burada gösterildiği gibi, var olan varsa de genişletebilirsiniz `$(PackageTargetFallback)` :</span><span class="sxs-lookup"><span data-stu-id="7d379-444">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="7d379-445">Bir geri yükleme grafiğinden bir kitaplığı değiştirme</span><span class="sxs-lookup"><span data-stu-id="7d379-445">Replacing one library from a restore graph</span></span>

<span data-ttu-id="7d379-446">Geri yükleme yanlış derlemeyi alıyorsa, bu paketlerin varsayılan seçeneğini hariç tutabilir ve kendi seçimiyle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="7d379-446">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="7d379-447">Birincisi, en üst düzeyle `PackageReference` , tüm varlıkları hariç tut:</span><span class="sxs-lookup"><span data-stu-id="7d379-447">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="7d379-448">Ardından, DLL 'nin uygun yerel kopyasına kendi başvurunuz ekleyin:</span><span class="sxs-lookup"><span data-stu-id="7d379-448">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
