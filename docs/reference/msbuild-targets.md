---
title: NuGet paketi ve geri yükleme MSBuild hedefleri olarak
description: NuGet paketi ve geri yükleme, NuGet 4.0 + ile doğrudan MSBuild hedefleri olarak çalışabilir.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 6a49e410617c14e22f0d4a67d8bfe280f64f5505
ms.sourcegitcommit: 8a424829b1f70cf7590e95db61997af6ae2d7a41
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72510800"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="ef172-103">NuGet paketi ve geri yükleme MSBuild hedefleri olarak</span><span class="sxs-lookup"><span data-stu-id="ef172-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="ef172-104">*NuGet 4.0 +*</span><span class="sxs-lookup"><span data-stu-id="ef172-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="ef172-105">[Packagereference](../consume-packages/package-references-in-project-files.md) biçimi sayesinde, NuGet 4.0 + tüm bildirim meta verilerini ayrı bir `.nuspec` dosyası kullanmak yerine doğrudan proje dosyası içinde depolayabilirler.</span><span class="sxs-lookup"><span data-stu-id="ef172-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="ef172-106">MSBuild 15.1 + ile NuGet, aşağıda açıklandığı gibi `pack` ve `restore` hedeflerine sahip birinci sınıf MSBuild vatandaşlık.</span><span class="sxs-lookup"><span data-stu-id="ef172-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="ef172-107">Bu hedefler, diğer herhangi bir MSBuild görevi veya hedefi ile yaptığınız gibi NuGet ile çalışmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="ef172-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="ef172-108">MSBuild kullanarak bir NuGet paketi oluşturma yönergeleri için bkz. [MSBuild kullanarak NuGet paketi oluşturma](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="ef172-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="ef172-109">(NuGet 3. x ve öncesi için, bunun yerine NuGet CLı aracılığıyla [paketle](../reference/cli-reference/cli-ref-pack.md) ve [geri yükleme](../reference/cli-reference/cli-ref-restore.md) komutlarını kullanırsınız.)</span><span class="sxs-lookup"><span data-stu-id="ef172-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="ef172-110">Hedef derleme sırası</span><span class="sxs-lookup"><span data-stu-id="ef172-110">Target build order</span></span>

<span data-ttu-id="ef172-111">@No__t-0 ve `restore` MSBuild hedefleri olduğundan, iş akışınızı geliştirmek için bunlara erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef172-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="ef172-112">Örneğin, paketledikten sonra paketinizi bir ağ paylaşımında kopyalamak istediğinizi varsayalım.</span><span class="sxs-lookup"><span data-stu-id="ef172-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="ef172-113">Bunu, proje dosyanıza aşağıdakileri ekleyerek yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ef172-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="ef172-114">Benzer şekilde, MSBuild görevinde bir MSBuild görevi yazabilir, kendi hedefini yazabilir ve NuGet özelliklerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef172-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="ef172-115">`$(OutputPath)` görelidir ve bu komutu proje kökünden çalıştırdığınız için bekliyor.</span><span class="sxs-lookup"><span data-stu-id="ef172-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="ef172-116">paket hedefi</span><span class="sxs-lookup"><span data-stu-id="ef172-116">pack target</span></span>

<span data-ttu-id="ef172-117">.NET Standard projeler için, `msbuild -t:pack` ' ı kullanarak, bir NuGet paketi oluştururken kullanılacak proje dosyasından girişler çizer.</span><span class="sxs-lookup"><span data-stu-id="ef172-117">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="ef172-118">Aşağıdaki tabloda, ilk `<PropertyGroup>` düğümü içindeki bir proje dosyasına eklenebilen MSBuild özellikleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ef172-118">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="ef172-119">Projeyi sağ tıklayıp bağlam menüsünde **{Project_Name} Düzenle** ' yi seçerek Visual Studio 2017 ve sonraki sürümlerde bu düzenlemeleri kolayca yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef172-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="ef172-120">Kolaylık sağlaması için tablo, [`.nuspec` dosyasındaki](../reference/nuspec.md)denk özelliğe göre düzenlenir.</span><span class="sxs-lookup"><span data-stu-id="ef172-120">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="ef172-121">@No__t-2 ' den `Owners` ve `Summary` özelliklerinin MSBuild ile desteklenmediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ef172-121">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="ef172-122">Öznitelik/NuSpec değeri</span><span class="sxs-lookup"><span data-stu-id="ef172-122">Attribute/NuSpec Value</span></span> | <span data-ttu-id="ef172-123">MSBuild özelliği</span><span class="sxs-lookup"><span data-stu-id="ef172-123">MSBuild Property</span></span> | <span data-ttu-id="ef172-124">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="ef172-124">Default</span></span> | <span data-ttu-id="ef172-125">Notlar</span><span class="sxs-lookup"><span data-stu-id="ef172-125">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="ef172-126">Numarasını</span><span class="sxs-lookup"><span data-stu-id="ef172-126">Id</span></span> | <span data-ttu-id="ef172-127">PackageID</span><span class="sxs-lookup"><span data-stu-id="ef172-127">PackageId</span></span> | <span data-ttu-id="ef172-128">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="ef172-128">AssemblyName</span></span> | <span data-ttu-id="ef172-129">MSBuild 'ten $ (AssemblyName)</span><span class="sxs-lookup"><span data-stu-id="ef172-129">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="ef172-130">Version</span><span class="sxs-lookup"><span data-stu-id="ef172-130">Version</span></span> | <span data-ttu-id="ef172-131">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="ef172-131">PackageVersion</span></span> | <span data-ttu-id="ef172-132">Version</span><span class="sxs-lookup"><span data-stu-id="ef172-132">Version</span></span> | <span data-ttu-id="ef172-133">Bu semver uyumludur, örneğin "1.0.0", "1.0.0-Beta" veya "1.0.0-Beta-00345"</span><span class="sxs-lookup"><span data-stu-id="ef172-133">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="ef172-134">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="ef172-134">VersionPrefix</span></span> | <span data-ttu-id="ef172-135">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="ef172-135">PackageVersionPrefix</span></span> | <span data-ttu-id="ef172-136">empty</span><span class="sxs-lookup"><span data-stu-id="ef172-136">empty</span></span> | <span data-ttu-id="ef172-137">PackageVersion ayarı PackageVersionPrefix üzerine yazıyor</span><span class="sxs-lookup"><span data-stu-id="ef172-137">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="ef172-138">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="ef172-138">VersionSuffix</span></span> | <span data-ttu-id="ef172-139">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="ef172-139">PackageVersionSuffix</span></span> | <span data-ttu-id="ef172-140">empty</span><span class="sxs-lookup"><span data-stu-id="ef172-140">empty</span></span> | <span data-ttu-id="ef172-141">MSBuild 'ten $ (VersionSuffix).</span><span class="sxs-lookup"><span data-stu-id="ef172-141">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="ef172-142">PackageVersion ayarı PackageVersionSuffix üzerine yazıyor</span><span class="sxs-lookup"><span data-stu-id="ef172-142">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="ef172-143">Yazarlar</span><span class="sxs-lookup"><span data-stu-id="ef172-143">Authors</span></span> | <span data-ttu-id="ef172-144">Yazarlar</span><span class="sxs-lookup"><span data-stu-id="ef172-144">Authors</span></span> | <span data-ttu-id="ef172-145">Geçerli kullanıcının Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="ef172-145">Username of the current user</span></span> | |
| <span data-ttu-id="ef172-146">lere</span><span class="sxs-lookup"><span data-stu-id="ef172-146">Owners</span></span> | <span data-ttu-id="ef172-147">Yok</span><span class="sxs-lookup"><span data-stu-id="ef172-147">N/A</span></span> | <span data-ttu-id="ef172-148">NuSpec içinde yok</span><span class="sxs-lookup"><span data-stu-id="ef172-148">Not present in NuSpec</span></span> | |
| <span data-ttu-id="ef172-149">Başlık</span><span class="sxs-lookup"><span data-stu-id="ef172-149">Title</span></span> | <span data-ttu-id="ef172-150">Başlık</span><span class="sxs-lookup"><span data-stu-id="ef172-150">Title</span></span> | <span data-ttu-id="ef172-151">PackageID</span><span class="sxs-lookup"><span data-stu-id="ef172-151">The PackageId</span></span>| |
| <span data-ttu-id="ef172-152">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ef172-152">Description</span></span> | <span data-ttu-id="ef172-153">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ef172-153">Description</span></span> | <span data-ttu-id="ef172-154">"Paket açıklaması"</span><span class="sxs-lookup"><span data-stu-id="ef172-154">"Package Description"</span></span> | |
| <span data-ttu-id="ef172-155">yaptırımlar</span><span class="sxs-lookup"><span data-stu-id="ef172-155">Copyright</span></span> | <span data-ttu-id="ef172-156">yaptırımlar</span><span class="sxs-lookup"><span data-stu-id="ef172-156">Copyright</span></span> | <span data-ttu-id="ef172-157">empty</span><span class="sxs-lookup"><span data-stu-id="ef172-157">empty</span></span> | |
| <span data-ttu-id="ef172-158">Requirelicensekabulünü</span><span class="sxs-lookup"><span data-stu-id="ef172-158">RequireLicenseAcceptance</span></span> | <span data-ttu-id="ef172-159">Packagerequirelicensekabulünü</span><span class="sxs-lookup"><span data-stu-id="ef172-159">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="ef172-160">false</span><span class="sxs-lookup"><span data-stu-id="ef172-160">false</span></span> | |
| <span data-ttu-id="ef172-161">lisan</span><span class="sxs-lookup"><span data-stu-id="ef172-161">license</span></span> | <span data-ttu-id="ef172-162">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="ef172-162">PackageLicenseExpression</span></span> | <span data-ttu-id="ef172-163">empty</span><span class="sxs-lookup"><span data-stu-id="ef172-163">empty</span></span> | <span data-ttu-id="ef172-164">@No__t karşılık gelir-0</span><span class="sxs-lookup"><span data-stu-id="ef172-164">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="ef172-165">lisan</span><span class="sxs-lookup"><span data-stu-id="ef172-165">license</span></span> | <span data-ttu-id="ef172-166">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="ef172-166">PackageLicenseFile</span></span> | <span data-ttu-id="ef172-167">empty</span><span class="sxs-lookup"><span data-stu-id="ef172-167">empty</span></span> | <span data-ttu-id="ef172-168">@No__t-0 ' a karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="ef172-168">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="ef172-169">Başvurulan lisans dosyasını açık bir şekilde paketetmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="ef172-169">You may need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="ef172-170">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="ef172-170">LicenseUrl</span></span> | <span data-ttu-id="ef172-171">PackageLicenseUrl 'Si</span><span class="sxs-lookup"><span data-stu-id="ef172-171">PackageLicenseUrl</span></span> | <span data-ttu-id="ef172-172">empty</span><span class="sxs-lookup"><span data-stu-id="ef172-172">empty</span></span> | <span data-ttu-id="ef172-173">`PackageLicenseUrl` kullanım dışıdır, PackageLicenseExpression veya PackageLicenseFile özelliğini kullanın</span><span class="sxs-lookup"><span data-stu-id="ef172-173">`PackageLicenseUrl` is deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="ef172-174">projectUrl</span><span class="sxs-lookup"><span data-stu-id="ef172-174">ProjectUrl</span></span> | <span data-ttu-id="ef172-175">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="ef172-175">PackageProjectUrl</span></span> | <span data-ttu-id="ef172-176">empty</span><span class="sxs-lookup"><span data-stu-id="ef172-176">empty</span></span> | |
| <span data-ttu-id="ef172-177">Simge</span><span class="sxs-lookup"><span data-stu-id="ef172-177">Icon</span></span> | <span data-ttu-id="ef172-178">Packageıcon</span><span class="sxs-lookup"><span data-stu-id="ef172-178">PackageIcon</span></span> | <span data-ttu-id="ef172-179">empty</span><span class="sxs-lookup"><span data-stu-id="ef172-179">empty</span></span> | <span data-ttu-id="ef172-180">Başvurulan simge görüntü dosyasını açıkça paketetmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="ef172-180">You may need to explicitly pack the referenced icon image file.</span></span>|
| <span data-ttu-id="ef172-181">Iurl</span><span class="sxs-lookup"><span data-stu-id="ef172-181">IconUrl</span></span> | <span data-ttu-id="ef172-182">PackageIconUrl 'Si</span><span class="sxs-lookup"><span data-stu-id="ef172-182">PackageIconUrl</span></span> | <span data-ttu-id="ef172-183">empty</span><span class="sxs-lookup"><span data-stu-id="ef172-183">empty</span></span> | <span data-ttu-id="ef172-184">`PackageIconUrl` kullanım dışıdır, Packageıcon özelliğini kullanın</span><span class="sxs-lookup"><span data-stu-id="ef172-184">`PackageIconUrl` is deprecated, use the PackageIcon property</span></span> |
| <span data-ttu-id="ef172-185">Etiketler</span><span class="sxs-lookup"><span data-stu-id="ef172-185">Tags</span></span> | <span data-ttu-id="ef172-186">PackageTags</span><span class="sxs-lookup"><span data-stu-id="ef172-186">PackageTags</span></span> | <span data-ttu-id="ef172-187">empty</span><span class="sxs-lookup"><span data-stu-id="ef172-187">empty</span></span> | <span data-ttu-id="ef172-188">Etiketler noktalı virgülle ayrılır.</span><span class="sxs-lookup"><span data-stu-id="ef172-188">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="ef172-189">relet 'ler</span><span class="sxs-lookup"><span data-stu-id="ef172-189">ReleaseNotes</span></span> | <span data-ttu-id="ef172-190">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="ef172-190">PackageReleaseNotes</span></span> | <span data-ttu-id="ef172-191">empty</span><span class="sxs-lookup"><span data-stu-id="ef172-191">empty</span></span> | |
| <span data-ttu-id="ef172-192">Depo/URL</span><span class="sxs-lookup"><span data-stu-id="ef172-192">Repository/Url</span></span> | <span data-ttu-id="ef172-193">Depourl 'Si</span><span class="sxs-lookup"><span data-stu-id="ef172-193">RepositoryUrl</span></span> | <span data-ttu-id="ef172-194">empty</span><span class="sxs-lookup"><span data-stu-id="ef172-194">empty</span></span> | <span data-ttu-id="ef172-195">Kaynak kodu kopyalamak veya almak için kullanılan depo URL 'SI.</span><span class="sxs-lookup"><span data-stu-id="ef172-195">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="ef172-196">Örnek: *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="ef172-196">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="ef172-197">Depo/tür</span><span class="sxs-lookup"><span data-stu-id="ef172-197">Repository/Type</span></span> | <span data-ttu-id="ef172-198">Repositorytype parametrelerinin sağlanması</span><span class="sxs-lookup"><span data-stu-id="ef172-198">RepositoryType</span></span> | <span data-ttu-id="ef172-199">empty</span><span class="sxs-lookup"><span data-stu-id="ef172-199">empty</span></span> | <span data-ttu-id="ef172-200">Depo türü.</span><span class="sxs-lookup"><span data-stu-id="ef172-200">Repository type.</span></span> <span data-ttu-id="ef172-201">Örnekler: *Git*, *TFS*.</span><span class="sxs-lookup"><span data-stu-id="ef172-201">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="ef172-202">Depo/dal</span><span class="sxs-lookup"><span data-stu-id="ef172-202">Repository/Branch</span></span> | <span data-ttu-id="ef172-203">Depodalı</span><span class="sxs-lookup"><span data-stu-id="ef172-203">RepositoryBranch</span></span> | <span data-ttu-id="ef172-204">empty</span><span class="sxs-lookup"><span data-stu-id="ef172-204">empty</span></span> | <span data-ttu-id="ef172-205">İsteğe bağlı depo dalı bilgileri.</span><span class="sxs-lookup"><span data-stu-id="ef172-205">Optional repository branch information.</span></span> <span data-ttu-id="ef172-206">Bu özelliğin dahil olması için aynı zamanda bir *Depo-URL* belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="ef172-206">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="ef172-207">Örnek: *Master* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="ef172-207">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="ef172-208">Depo/kayıt</span><span class="sxs-lookup"><span data-stu-id="ef172-208">Repository/Commit</span></span> | <span data-ttu-id="ef172-209">Kayıt yapma</span><span class="sxs-lookup"><span data-stu-id="ef172-209">RepositoryCommit</span></span> | <span data-ttu-id="ef172-210">empty</span><span class="sxs-lookup"><span data-stu-id="ef172-210">empty</span></span> | <span data-ttu-id="ef172-211">Paketin hangi kaynağa göre oluşturulduğunu göstermek için isteğe bağlı depo kaydı veya değişiklik kümesi.</span><span class="sxs-lookup"><span data-stu-id="ef172-211">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="ef172-212">Bu özelliğin dahil olması için aynı zamanda bir *Depo-URL* belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="ef172-212">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="ef172-213">Örnek: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="ef172-213">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="ef172-214">PackageType</span><span class="sxs-lookup"><span data-stu-id="ef172-214">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="ef172-215">Özet</span><span class="sxs-lookup"><span data-stu-id="ef172-215">Summary</span></span> | <span data-ttu-id="ef172-216">Desteklenmez</span><span class="sxs-lookup"><span data-stu-id="ef172-216">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="ef172-217">Paket hedef girişleri</span><span class="sxs-lookup"><span data-stu-id="ef172-217">pack target inputs</span></span>

- <span data-ttu-id="ef172-218">Ispackable</span><span class="sxs-lookup"><span data-stu-id="ef172-218">IsPackable</span></span>
- <span data-ttu-id="ef172-219">Suppressbağımlıcıeswhenpaketleme</span><span class="sxs-lookup"><span data-stu-id="ef172-219">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="ef172-220">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="ef172-220">PackageVersion</span></span>
- <span data-ttu-id="ef172-221">PackageID</span><span class="sxs-lookup"><span data-stu-id="ef172-221">PackageId</span></span>
- <span data-ttu-id="ef172-222">Yazarlar</span><span class="sxs-lookup"><span data-stu-id="ef172-222">Authors</span></span>
- <span data-ttu-id="ef172-223">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ef172-223">Description</span></span>
- <span data-ttu-id="ef172-224">yaptırımlar</span><span class="sxs-lookup"><span data-stu-id="ef172-224">Copyright</span></span>
- <span data-ttu-id="ef172-225">Packagerequirelicensekabulünü</span><span class="sxs-lookup"><span data-stu-id="ef172-225">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="ef172-226">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="ef172-226">DevelopmentDependency</span></span>
- <span data-ttu-id="ef172-227">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="ef172-227">PackageLicenseExpression</span></span>
- <span data-ttu-id="ef172-228">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="ef172-228">PackageLicenseFile</span></span>
- <span data-ttu-id="ef172-229">PackageLicenseUrl 'Si</span><span class="sxs-lookup"><span data-stu-id="ef172-229">PackageLicenseUrl</span></span>
- <span data-ttu-id="ef172-230">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="ef172-230">PackageProjectUrl</span></span>
- <span data-ttu-id="ef172-231">PackageIconUrl 'Si</span><span class="sxs-lookup"><span data-stu-id="ef172-231">PackageIconUrl</span></span>
- <span data-ttu-id="ef172-232">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="ef172-232">PackageReleaseNotes</span></span>
- <span data-ttu-id="ef172-233">PackageTags</span><span class="sxs-lookup"><span data-stu-id="ef172-233">PackageTags</span></span>
- <span data-ttu-id="ef172-234">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="ef172-234">PackageOutputPath</span></span>
- <span data-ttu-id="ef172-235">Includesymbols</span><span class="sxs-lookup"><span data-stu-id="ef172-235">IncludeSymbols</span></span>
- <span data-ttu-id="ef172-236">Includesource</span><span class="sxs-lookup"><span data-stu-id="ef172-236">IncludeSource</span></span>
- <span data-ttu-id="ef172-237">packageTypes</span><span class="sxs-lookup"><span data-stu-id="ef172-237">PackageTypes</span></span>
- <span data-ttu-id="ef172-238">IsTool</span><span class="sxs-lookup"><span data-stu-id="ef172-238">IsTool</span></span>
- <span data-ttu-id="ef172-239">Depourl 'Si</span><span class="sxs-lookup"><span data-stu-id="ef172-239">RepositoryUrl</span></span>
- <span data-ttu-id="ef172-240">Repositorytype parametrelerinin sağlanması</span><span class="sxs-lookup"><span data-stu-id="ef172-240">RepositoryType</span></span>
- <span data-ttu-id="ef172-241">Depodalı</span><span class="sxs-lookup"><span data-stu-id="ef172-241">RepositoryBranch</span></span>
- <span data-ttu-id="ef172-242">Kayıt yapma</span><span class="sxs-lookup"><span data-stu-id="ef172-242">RepositoryCommit</span></span>
- <span data-ttu-id="ef172-243">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="ef172-243">NoPackageAnalysis</span></span>
- <span data-ttu-id="ef172-244">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="ef172-244">MinClientVersion</span></span>
- <span data-ttu-id="ef172-245">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="ef172-245">IncludeBuildOutput</span></span>
- <span data-ttu-id="ef172-246">Includecontentınpack</span><span class="sxs-lookup"><span data-stu-id="ef172-246">IncludeContentInPack</span></span>
- <span data-ttu-id="ef172-247">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="ef172-247">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="ef172-248">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="ef172-248">ContentTargetFolders</span></span>
- <span data-ttu-id="ef172-249">Nusguus dosyası</span><span class="sxs-lookup"><span data-stu-id="ef172-249">NuspecFile</span></span>
- <span data-ttu-id="ef172-250">Nusgubasepath</span><span class="sxs-lookup"><span data-stu-id="ef172-250">NuspecBasePath</span></span>
- <span data-ttu-id="ef172-251">Nus, Properties</span><span class="sxs-lookup"><span data-stu-id="ef172-251">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="ef172-252">paket senaryoları</span><span class="sxs-lookup"><span data-stu-id="ef172-252">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="ef172-253">Bağımlılıkları gösterme</span><span class="sxs-lookup"><span data-stu-id="ef172-253">Suppress dependencies</span></span>

<span data-ttu-id="ef172-254">Oluşturulan NuGet paketinden paket bağımlılıklarını bastırmak için `SuppressDependenciesWhenPacking` ' ı `true` olarak ayarlayın. Bu, oluşturulan nupkg dosyasından tüm bağımlılıkların atlanmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="ef172-254">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="ef172-255">PackageIconUrl 'Si</span><span class="sxs-lookup"><span data-stu-id="ef172-255">PackageIconUrl</span></span>

> [!Important]
> <span data-ttu-id="ef172-256">PackageIconUrl, NuGet 5.3 + & Visual Studio 2019 Version 16.3 + ile kullanım dışıdır.</span><span class="sxs-lookup"><span data-stu-id="ef172-256">PackageIconUrl is deprecated with NuGet 5.3+ & Visual Studio 2019 version 16.3+.</span></span> <span data-ttu-id="ef172-257">Bunun yerine [Packageıcon](#packing-an-icon-image-file) kullanın.</span><span class="sxs-lookup"><span data-stu-id="ef172-257">Use [PackageIcon](#packing-an-icon-image-file) instead.</span></span>

### <a name="packing-an-icon-image-file"></a><span data-ttu-id="ef172-258">Simge görüntüsü dosyası paketleme</span><span class="sxs-lookup"><span data-stu-id="ef172-258">Packing an icon image file</span></span>

<span data-ttu-id="ef172-259">Bir simge resim dosyası paketleme sırasında, paketin köküne göre paket yolunu belirtmek için Packageıcon özelliğini kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ef172-259">When packing an icon image file, you need to use PackageIcon property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="ef172-260">Ayrıca, dosyanın pakete eklendiğinden emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ef172-260">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="ef172-261">Görüntü dosyası boyutu 1 MB ile sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="ef172-261">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="ef172-262">Desteklenen dosya biçimleri JPEG ve PNG içerir.</span><span class="sxs-lookup"><span data-stu-id="ef172-262">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="ef172-263">64x64 görüntü çözünürlüğü önerilir.</span><span class="sxs-lookup"><span data-stu-id="ef172-263">We recommend an image resolution of 64x64.</span></span>

<span data-ttu-id="ef172-264">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="ef172-264">For example:</span></span>

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

<span data-ttu-id="ef172-265">[Paket simgesi örneği](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span><span class="sxs-lookup"><span data-stu-id="ef172-265">[Package Icon sample](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span></span>

<span data-ttu-id="ef172-266">Nuspec eşdeğeri için, [simgenin nuspec başvurusuna](nuspec.md#icon)göz atın.</span><span class="sxs-lookup"><span data-stu-id="ef172-266">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="ef172-267">Çıkış derlemeleri</span><span class="sxs-lookup"><span data-stu-id="ef172-267">Output assemblies</span></span>

<span data-ttu-id="ef172-268">`nuget pack`, `.exe`, `.dll`, `.xml`, `.winmd`, `.json` ve `.pri` uzantılarına sahip çıktı dosyalarını kopyalar.</span><span class="sxs-lookup"><span data-stu-id="ef172-268">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="ef172-269">Kopyalanan çıkış dosyaları, `BuiltOutputProjectGroup` hedeften MSBuild 'in sağladığı öğesine bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="ef172-269">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="ef172-270">Çıktı derlemelerinin nerede olduğunu denetlemek için, proje dosyanızda veya komut satırında kullanabileceğiniz iki MSBuild özelliği vardır:</span><span class="sxs-lookup"><span data-stu-id="ef172-270">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="ef172-271">`IncludeBuildOutput`: derleme çıkış derlemelerinin pakete dahil edilip edilmeyeceğini belirleyen bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="ef172-271">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="ef172-272">`BuildOutputTargetFolder`: çıkış derlemelerinin yerleştirilmesi gereken klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="ef172-272">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="ef172-273">Çıkış derlemeleri (ve diğer çıkış dosyaları) ilgili çerçeve klasörlerine kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="ef172-273">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="ef172-274">Paket başvuruları</span><span class="sxs-lookup"><span data-stu-id="ef172-274">Package references</span></span>

<span data-ttu-id="ef172-275">Bkz. [Proje dosyalarındaki paket başvuruları](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="ef172-275">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="ef172-276">Projeden projeye başvurular</span><span class="sxs-lookup"><span data-stu-id="ef172-276">Project to project references</span></span>

<span data-ttu-id="ef172-277">Proje başvuruları, varsayılan olarak NuGet paket başvuruları olarak değerlendirilir, örneğin:</span><span class="sxs-lookup"><span data-stu-id="ef172-277">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="ef172-278">Ayrıca, proje başvurunuz için aşağıdaki meta verileri de ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ef172-278">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="ef172-279">Bir paketteki içerik ekleme</span><span class="sxs-lookup"><span data-stu-id="ef172-279">Including content in a package</span></span>

<span data-ttu-id="ef172-280">İçerik eklemek için var olan `<Content>` öğesine ek meta veriler ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ef172-280">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="ef172-281">Varsayılan olarak, aşağıdaki gibi girdilerle geçersiz kılmadığınız müddetçe "Içerik" türünde her şey pakete dahil edilir:</span><span class="sxs-lookup"><span data-stu-id="ef172-281">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="ef172-282">Varsayılan olarak, her şey bir paket içinde `content` ve `contentFiles\any\<target_framework>` klasörünün köküne eklenir ve bir paket yolu belirtmediğiniz takdirde göreli klasör yapısını korur:</span><span class="sxs-lookup"><span data-stu-id="ef172-282">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="ef172-283">Tüm içeriğinizi yalnızca belirli bir kök klasöre (`content` ve `contentFiles` yerine) kopyalamak istiyorsanız, "Content; contentFiles" varsayılan olan ancak başka bir klasör adı olarak ayarlanabilir olan `ContentTargetFolders` MSBuild özelliğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef172-283">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="ef172-284">Yalnızca `ContentTargetFolders` ' daki "contentFiles" belirtildiğinde dosyaları `contentFiles\any\<target_framework>` veya `contentFiles\<language>\<target_framework>` ' ye `buildAction` ' ü temel alarak koyar.</span><span class="sxs-lookup"><span data-stu-id="ef172-284">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="ef172-285">`PackagePath`, noktalı virgülle ayrılmış bir hedef yolları kümesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="ef172-285">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="ef172-286">Boş bir paket yolu belirtilmesi, dosyayı paketin köküne ekler.</span><span class="sxs-lookup"><span data-stu-id="ef172-286">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="ef172-287">Örneğin, aşağıdaki `libuv.txt` `content\myfiles`, `content\samples` ve paket köküne ekler:</span><span class="sxs-lookup"><span data-stu-id="ef172-287">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="ef172-288">Ayrıca, `true` ' i varsayılan olan-0 @no__t bir MSBuild özelliği de vardır.</span><span class="sxs-lookup"><span data-stu-id="ef172-288">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="ef172-289">Bu, herhangi bir projede `false` olarak ayarlandıysa, söz konusu projeden içerik NuGet paketine dahil edilmez.</span><span class="sxs-lookup"><span data-stu-id="ef172-289">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="ef172-290">Yukarıdaki öğelerin hiçbirinde ayarlayabileceğiniz diğer paketine özgü meta veriler ```<PackageCopyToOutput>``` ve ```<PackageFlatten>``` ' i içerir. Bu, çıktı nuspec içindeki ```contentFiles``` girişinde ```CopyToOutput``` ve ```Flatten``` değerlerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="ef172-290">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="ef172-291">Içerik öğelerinden ayrı olarak, `<Pack>` ve `<PackagePath>` meta verileri de derleme, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes oluşturma eylemi olan dosyalarda ayarlanabilir. CodeAnalysisDictionary, AndroidAsset, AndroidResource, paketleme Leresource veya None.</span><span class="sxs-lookup"><span data-stu-id="ef172-291">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="ef172-292">Glob desenleri kullanılırken dosya adını paket yolunuza eklemek için paket yolu, klasör ayırıcı karakteriyle bitmelidir; Aksi takdirde, paket yolu dosya adı dahil tam yol olarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="ef172-292">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="ef172-293">Includesymbols</span><span class="sxs-lookup"><span data-stu-id="ef172-293">IncludeSymbols</span></span>

<span data-ttu-id="ef172-294">@No__t-0 kullanılırken, karşılık gelen `.pdb` dosyaları diğer çıkış dosyalarıyla birlikte kopyalanır (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span><span class="sxs-lookup"><span data-stu-id="ef172-294">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="ef172-295">@No__t-0 ayarının normal bir paket *ve* bir semboller paketi oluşturduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ef172-295">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="ef172-296">Includesource</span><span class="sxs-lookup"><span data-stu-id="ef172-296">IncludeSource</span></span>

<span data-ttu-id="ef172-297">Bu `IncludeSymbols` ile aynıdır, ancak kaynak dosyalarını ve `.pdb` dosyalarla birlikte kopyalar.</span><span class="sxs-lookup"><span data-stu-id="ef172-297">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="ef172-298">@No__t-0 türündeki tüm dosyalar, elde edilen paketteki göreli yol klasörü yapısını koruyarak `src\<ProjectName>\` ' e kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="ef172-298">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="ef172-299">Aynı zamanda, `TreatAsPackageReference` ' in `false` ' ye ayarlandığı `ProjectReference` ' ın kaynak dosyaları için de aynı olur.</span><span class="sxs-lookup"><span data-stu-id="ef172-299">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="ef172-300">Derleme türünde bir dosya proje klasörünün dışındaysa, `src\<ProjectName>\` ' a eklenir.</span><span class="sxs-lookup"><span data-stu-id="ef172-300">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="ef172-301">Lisans ifadesi veya lisans dosyası paketleme</span><span class="sxs-lookup"><span data-stu-id="ef172-301">Packing a license expression or a license file</span></span>

<span data-ttu-id="ef172-302">Bir lisans ifadesi kullanılırken PackageLicenseExpression özelliğinin kullanılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ef172-302">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="ef172-303">[Lisans ifadesi örneği](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="ef172-303">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="ef172-304">[NuGet.org tarafından kabul edilen lisans ifadeleri ve lisanslar hakkında daha fazla bilgi edinin](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="ef172-304">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="ef172-305">Bir lisans dosyası paketleme sırasında, paketin köküne göre paket yolunu belirtmek için PackageLicenseFile özelliğini kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ef172-305">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="ef172-306">Ayrıca, dosyanın pakete eklendiğinden emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ef172-306">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="ef172-307">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="ef172-307">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="ef172-308">[Lisans dosyası örneği](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="ef172-308">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="ef172-309">IsTool</span><span class="sxs-lookup"><span data-stu-id="ef172-309">IsTool</span></span>

<span data-ttu-id="ef172-310">@No__t-0 kullanılırken, [Çıkış derlemeleri](#output-assemblies) senaryosunda belirtilen tüm çıkış dosyaları `lib` klasörü yerine `tools` klasörüne kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="ef172-310">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="ef172-311">Bu, `.csproj` dosyasında `PackageType` ayarlanarak belirtilen `DotNetCliTool` ' dan farklı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ef172-311">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="ef172-312">. Nuspec kullanarak paketleme</span><span class="sxs-lookup"><span data-stu-id="ef172-312">Packing using a .nuspec</span></span>

<span data-ttu-id="ef172-313">Bunun yerine, genellikle proje dosyasındaki `.nuspec` dosyasında bulunan [tüm özellikleri eklemeniz](../reference/msbuild-targets.md#pack-target) önerilir, ancak projenizi paketetmek için bir `.nuspec` dosyası kullanmayı tercih edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef172-313">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="ef172-314">@No__t-0 kullanan SDK olmayan bir proje için, paket görevinin yürütülebilmesi için `NuGet.Build.Tasks.Pack.targets` ' i içeri aktarmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ef172-314">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="ef172-315">Bir nuspec dosyası paketetmeden önce projeyi geri yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ef172-315">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="ef172-316">(SDK stili bir proje varsayılan olarak paket hedeflerini içerir.)</span><span class="sxs-lookup"><span data-stu-id="ef172-316">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="ef172-317">Proje dosyasının hedef çerçevesi ilgisizdir ve bir nuspec paketleme sırasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="ef172-317">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="ef172-318">Aşağıdaki üç MSBuild özelliği @no__t ile paketleme ile ilgilidir: 0:</span><span class="sxs-lookup"><span data-stu-id="ef172-318">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="ef172-319">`NuspecFile`: paketleme için kullanılan `.nuspec` dosyasının göreli veya mutlak yolu.</span><span class="sxs-lookup"><span data-stu-id="ef172-319">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="ef172-320">`NuspecProperties`: anahtar = değer çiftleri için noktalı virgülle ayrılmış bir liste.</span><span class="sxs-lookup"><span data-stu-id="ef172-320">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="ef172-321">MSBuild komut satırı ayrıştırması çalışma yöntemi nedeniyle, birden çok özellik şu şekilde belirtilmelidir: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span><span class="sxs-lookup"><span data-stu-id="ef172-321">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="ef172-322">`NuspecBasePath`: `.nuspec` dosyasının temel yolu.</span><span class="sxs-lookup"><span data-stu-id="ef172-322">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="ef172-323">Projenizi paketmek için `dotnet.exe` kullanıyorsanız, aşağıdaki gibi bir komut kullanın:</span><span class="sxs-lookup"><span data-stu-id="ef172-323">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="ef172-324">Projenizi paketmek için MSBuild kullanıyorsanız, aşağıdaki gibi bir komut kullanın:</span><span class="sxs-lookup"><span data-stu-id="ef172-324">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="ef172-325">Lütfen DotNet. exe veya MSBuild kullanarak bir nuspec paketleme, projenin varsayılan olarak oluşturulmasına da neden olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ef172-325">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="ef172-326">Bu, proje dosyasında ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` ayarıyla birlikte ```--no-build``` özelliği DotNet. exe @no__t ' ye geçirilerek kaçınılmaz.</span><span class="sxs-lookup"><span data-stu-id="ef172-326">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="ef172-327">Bir nuspec dosyası paketiçin bir *. csproj* dosyası örneği:</span><span class="sxs-lookup"><span data-stu-id="ef172-327">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="ef172-328">Özelleştirilmiş paket oluşturmak için gelişmiş uzantı noktaları</span><span class="sxs-lookup"><span data-stu-id="ef172-328">Advanced extension points to create customized package</span></span>

<span data-ttu-id="ef172-329">@No__t-0 hedefi, iç, hedef çerçeveye özgü derlemede çalışan iki uzantı noktası sağlar.</span><span class="sxs-lookup"><span data-stu-id="ef172-329">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="ef172-330">Uzantı noktaları, hedef çerçeveye özgü içerik ve derlemelerin bir pakete dahil edilmesi için destek:</span><span class="sxs-lookup"><span data-stu-id="ef172-330">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="ef172-331">`TargetsForTfmSpecificBuildOutput` hedefi: `lib` klasörünün içindeki dosyalar veya `BuildOutputTargetFolder` kullanılarak belirtilen bir klasör için kullanın.</span><span class="sxs-lookup"><span data-stu-id="ef172-331">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="ef172-332">`TargetsForTfmSpecificContentInPackage` hedefi: `BuildOutputTargetFolder` dışındaki dosyalar için kullanın.</span><span class="sxs-lookup"><span data-stu-id="ef172-332">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="ef172-333">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="ef172-333">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="ef172-334">Özel bir hedef yazın ve `$(TargetsForTfmSpecificBuildOutput)` özelliğinin değeri olarak belirtin.</span><span class="sxs-lookup"><span data-stu-id="ef172-334">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="ef172-335">@No__t-0 ' a (varsayılan olarak lib) gitmesi gereken tüm dosyalar için, hedef bu dosyaları ItemGroup `BuildOutputInPackage` ' e yazmalıdır ve aşağıdaki iki meta veri değerini ayarlamış olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="ef172-335">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="ef172-336">`FinalOutputPath`: dosyanın mutlak yolu; sağlanmazsa, kimlik kaynak yolunu değerlendirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ef172-336">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="ef172-337">`TargetPath`: (Isteğe bağlı) dosyanın, ilgili kültür klasörlerinin altında yer alan uydu derlemeleri gibi `lib\<TargetFramework>` içindeki bir alt klasöre gitmesi gerektiğinde ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="ef172-337">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="ef172-338">Varsayılan olarak dosyanın adıdır.</span><span class="sxs-lookup"><span data-stu-id="ef172-338">Defaults to the name of the file.</span></span>

<span data-ttu-id="ef172-339">Örnek:</span><span class="sxs-lookup"><span data-stu-id="ef172-339">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="ef172-340">Targetsfortfmspecificcontenınpackage</span><span class="sxs-lookup"><span data-stu-id="ef172-340">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="ef172-341">Özel bir hedef yazın ve `$(TargetsForTfmSpecificContentInPackage)` özelliğinin değeri olarak belirtin.</span><span class="sxs-lookup"><span data-stu-id="ef172-341">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="ef172-342">Pakete dahil edilecek herhangi bir dosya için, hedef bu dosyaları ItemGroup `TfmSpecificPackageFile` ' a yazıp, aşağıdaki isteğe bağlı meta verileri ayarlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ef172-342">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="ef172-343">`PackagePath`: dosyanın pakette çıkış olması gereken yol.</span><span class="sxs-lookup"><span data-stu-id="ef172-343">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="ef172-344">Aynı paket yoluna birden fazla dosya eklenirse NuGet bir uyarı verir.</span><span class="sxs-lookup"><span data-stu-id="ef172-344">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="ef172-345">`BuildAction`: dosyaya atanacak derleme eylemi, yalnızca paket yolu `contentFiles` klasörsde olduğunda gereklidir.</span><span class="sxs-lookup"><span data-stu-id="ef172-345">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="ef172-346">Varsayılan "none" olarak belirlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="ef172-346">Defaults to "None".</span></span>

<span data-ttu-id="ef172-347">Örnek:</span><span class="sxs-lookup"><span data-stu-id="ef172-347">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="ef172-348">hedefi geri yükle</span><span class="sxs-lookup"><span data-stu-id="ef172-348">restore target</span></span>

<span data-ttu-id="ef172-349">`MSBuild -t:restore` (`nuget restore` ve @no__t-.NET Core projeleriyle birlikte kullanılan), proje dosyasında başvurulan paketleri aşağıdaki şekilde geri yükler:</span><span class="sxs-lookup"><span data-stu-id="ef172-349">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="ef172-350">Proje başvurularına tüm projeyi oku</span><span class="sxs-lookup"><span data-stu-id="ef172-350">Read all project to project references</span></span>
1. <span data-ttu-id="ef172-351">Ara klasörünü ve hedef çerçeveleri bulmak için proje özelliklerini okuyun</span><span class="sxs-lookup"><span data-stu-id="ef172-351">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="ef172-352">MSBuild verilerini NuGet. Build. Tasks. dll dosyasına geçir</span><span class="sxs-lookup"><span data-stu-id="ef172-352">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="ef172-353">Geri yüklemeyi Çalıştır</span><span class="sxs-lookup"><span data-stu-id="ef172-353">Run restore</span></span>
1. <span data-ttu-id="ef172-354">Paketleri İndir</span><span class="sxs-lookup"><span data-stu-id="ef172-354">Download packages</span></span>
1. <span data-ttu-id="ef172-355">Varlıklar dosyası, hedefler ve props yazma</span><span class="sxs-lookup"><span data-stu-id="ef172-355">Write assets file, targets, and props</span></span>

<span data-ttu-id="ef172-356">@No__t-0 hedefi **yalnızca** packagereference biçimi kullanan projeler için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ef172-356">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="ef172-357">@No__t-1 biçimini kullanan projeler **için çalışmaz;** Bunun yerine [NuGet geri yükleme](../reference/cli-reference/cli-ref-restore.md) kullanın.</span><span class="sxs-lookup"><span data-stu-id="ef172-357">It does **not** work for projects using the `packages.config` format; use [nuget restore](../reference/cli-reference/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="ef172-358">Özellikleri geri yükle</span><span class="sxs-lookup"><span data-stu-id="ef172-358">Restore properties</span></span>

<span data-ttu-id="ef172-359">Ek geri yükleme ayarları proje dosyasındaki MSBuild özelliklerinden gelebilir.</span><span class="sxs-lookup"><span data-stu-id="ef172-359">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="ef172-360">Değerler, `-p:` anahtarı kullanılarak komut satırından da ayarlanabilir (aşağıdaki örneklere bakın).</span><span class="sxs-lookup"><span data-stu-id="ef172-360">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="ef172-361">Özellik</span><span class="sxs-lookup"><span data-stu-id="ef172-361">Property</span></span> | <span data-ttu-id="ef172-362">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ef172-362">Description</span></span> |
|--------|--------|
| <span data-ttu-id="ef172-363">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="ef172-363">RestoreSources</span></span> | <span data-ttu-id="ef172-364">Paket kaynaklarının noktalı virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="ef172-364">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="ef172-365">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="ef172-365">RestorePackagesPath</span></span> | <span data-ttu-id="ef172-366">Kullanıcı paketleri klasör yolu.</span><span class="sxs-lookup"><span data-stu-id="ef172-366">User packages folder path.</span></span> |
| <span data-ttu-id="ef172-367">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="ef172-367">RestoreDisableParallel</span></span> | <span data-ttu-id="ef172-368">İndirmeleri tek seferde bir ile sınırlayın.</span><span class="sxs-lookup"><span data-stu-id="ef172-368">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="ef172-369">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="ef172-369">RestoreConfigFile</span></span> | <span data-ttu-id="ef172-370">Uygulanacak `Nuget.Config` dosyasının yolu.</span><span class="sxs-lookup"><span data-stu-id="ef172-370">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="ef172-371">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="ef172-371">RestoreNoCache</span></span> | <span data-ttu-id="ef172-372">Doğru ise, önbelleğe alınmış paketlerin kullanılmasını önler.</span><span class="sxs-lookup"><span data-stu-id="ef172-372">If true, avoids using cached packages.</span></span> <span data-ttu-id="ef172-373">Bkz. [genel paketleri ve önbellek klasörlerini yönetme](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="ef172-373">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="ef172-374">Restoreıgnorefailedsources</span><span class="sxs-lookup"><span data-stu-id="ef172-374">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="ef172-375">Doğru ise, başarısız veya eksik paket kaynaklarını yoksayar.</span><span class="sxs-lookup"><span data-stu-id="ef172-375">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="ef172-376">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="ef172-376">RestoreFallbackFolders</span></span> | <span data-ttu-id="ef172-377">Geri dönüş klasörleri, Kullanıcı paketleri klasörüyle aynı şekilde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ef172-377">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="ef172-378">Restoreaddıtionalprojectsources</span><span class="sxs-lookup"><span data-stu-id="ef172-378">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="ef172-379">Geri yükleme sırasında kullanılacak ek kaynaklar.</span><span class="sxs-lookup"><span data-stu-id="ef172-379">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="ef172-380">Restoreaddıtionalprojectfallbackfolders</span><span class="sxs-lookup"><span data-stu-id="ef172-380">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="ef172-381">Geri yükleme sırasında kullanılacak ek geri dönüş klasörleri.</span><span class="sxs-lookup"><span data-stu-id="ef172-381">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="ef172-382">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="ef172-382">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="ef172-383">@No__t belirtilen geri dönüş klasörlerini dışlar-0</span><span class="sxs-lookup"><span data-stu-id="ef172-383">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="ef172-384">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="ef172-384">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="ef172-385">@No__t-0 için yol.</span><span class="sxs-lookup"><span data-stu-id="ef172-385">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="ef172-386">Restoregraphprojectınput</span><span class="sxs-lookup"><span data-stu-id="ef172-386">RestoreGraphProjectInput</span></span> | <span data-ttu-id="ef172-387">Geri yüklenecek projelerin, mutlak yollar içermesi gereken, noktalı virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="ef172-387">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="ef172-388">Restoreuseskipnontenttargets</span><span class="sxs-lookup"><span data-stu-id="ef172-388">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="ef172-389">Projeler MSBuild aracılığıyla toplandığında, bunların `SkipNonexistentTargets` iyileştirmesi kullanılarak toplanıp toplanmayacağını belirler.</span><span class="sxs-lookup"><span data-stu-id="ef172-389">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="ef172-390">Ayarlanmazsa, varsayılan olarak `true` olur.</span><span class="sxs-lookup"><span data-stu-id="ef172-390">When not set, defaults to `true`.</span></span> <span data-ttu-id="ef172-391">Projenin hedefleri içeri aktarılmadığı zaman, sonuç hızlı bir davranıştır.</span><span class="sxs-lookup"><span data-stu-id="ef172-391">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="ef172-392">Msbuildprojeclarsionspath</span><span class="sxs-lookup"><span data-stu-id="ef172-392">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="ef172-393">Çıkış klasörü, `BaseIntermediateOutputPath` ve `obj` klasörü ayarlanıyor.</span><span class="sxs-lookup"><span data-stu-id="ef172-393">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| <span data-ttu-id="ef172-394">Restorezorlamalı</span><span class="sxs-lookup"><span data-stu-id="ef172-394">RestoreForce</span></span> | <span data-ttu-id="ef172-395">PackageReference tabanlı projelerde, son geri yükleme başarılı olsa bile tüm bağımlılıkların çözülmesini zorlar.</span><span class="sxs-lookup"><span data-stu-id="ef172-395">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="ef172-396">Bu bayrağın belirtilmesi `project.assets.json` dosyasını silmeye benzerdir.</span><span class="sxs-lookup"><span data-stu-id="ef172-396">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="ef172-397">Bu, http-cache ' i atlar.</span><span class="sxs-lookup"><span data-stu-id="ef172-397">This does not bypass the http-cache.</span></span> |
| <span data-ttu-id="ef172-398">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="ef172-398">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="ef172-399">Bir kilit dosyasının kullanımıyla ilgili olarak.</span><span class="sxs-lookup"><span data-stu-id="ef172-399">Opts into the usage of a lock file.</span></span> |
| <span data-ttu-id="ef172-400">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="ef172-400">RestoreLockedMode</span></span> | <span data-ttu-id="ef172-401">Geri yüklemeyi kilitli modda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ef172-401">Run restore in locked mode.</span></span> <span data-ttu-id="ef172-402">Bu, geri yüklemenin bağımlılıkları yeniden değerlendirmeyeceği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="ef172-402">This means that restore will not reevaluate the dependencies.</span></span> |
| <span data-ttu-id="ef172-403">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="ef172-403">NuGetLockFilePath</span></span> | <span data-ttu-id="ef172-404">Kilit dosyası için özel bir konum.</span><span class="sxs-lookup"><span data-stu-id="ef172-404">A custom location for the lock file.</span></span> <span data-ttu-id="ef172-405">Varsayılan konum projenin yanında bulunur ve `packages.lock.json` olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="ef172-405">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| <span data-ttu-id="ef172-406">Restoreforcedeğerlendir</span><span class="sxs-lookup"><span data-stu-id="ef172-406">RestoreForceEvaluate</span></span> | <span data-ttu-id="ef172-407">Bağımlılıkları yeniden hesaplamak ve herhangi bir uyarı olmadan kilit dosyasını güncelleştirmek için geri yüklemeyi zorlar.</span><span class="sxs-lookup"><span data-stu-id="ef172-407">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> | 

#### <a name="examples"></a><span data-ttu-id="ef172-408">Örnekler</span><span class="sxs-lookup"><span data-stu-id="ef172-408">Examples</span></span>

<span data-ttu-id="ef172-409">Komut satırı:</span><span class="sxs-lookup"><span data-stu-id="ef172-409">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="ef172-410">Proje dosyası:</span><span class="sxs-lookup"><span data-stu-id="ef172-410">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="ef172-411">Çıkışları geri yükleme</span><span class="sxs-lookup"><span data-stu-id="ef172-411">Restore outputs</span></span>

<span data-ttu-id="ef172-412">Restore, derleme `obj` klasöründe aşağıdaki dosyaları oluşturur:</span><span class="sxs-lookup"><span data-stu-id="ef172-412">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="ef172-413">Dosya</span><span class="sxs-lookup"><span data-stu-id="ef172-413">File</span></span> | <span data-ttu-id="ef172-414">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ef172-414">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="ef172-415">Tüm paket başvurularının bağımlılık grafiğini içerir.</span><span class="sxs-lookup"><span data-stu-id="ef172-415">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="ef172-416">Paketlerde bulunan MSBuild props 'a başvurular</span><span class="sxs-lookup"><span data-stu-id="ef172-416">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="ef172-417">Paketlerde bulunan MSBuild hedeflerine başvurular</span><span class="sxs-lookup"><span data-stu-id="ef172-417">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="ef172-418">Tek bir MSBuild komutuyla geri yükleme ve oluşturma</span><span class="sxs-lookup"><span data-stu-id="ef172-418">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="ef172-419">NuGet, MSBuild hedeflerini ve props 'ı getiren paketleri geri yükleyebilir, geri yükleme ve derleme değerlendirmeleri farklı genel özelliklerle çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="ef172-419">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="ef172-420">Bu, aşağıdakilerin öngörülemeyen ve genellikle yanlış bir davranışa sahip olacağı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="ef172-420">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="ef172-421">Bunun yerine önerilen yaklaşım şunlardır:</span><span class="sxs-lookup"><span data-stu-id="ef172-421">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="ef172-422">Aynı mantık `build` ' a benzer diğer hedefler için de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="ef172-422">The same logic applies to other targets similar to `build`.</span></span>

### <a name="packagetargetfallback"></a><span data-ttu-id="ef172-423">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="ef172-423">PackageTargetFallback</span></span>

<span data-ttu-id="ef172-424">@No__t-0 öğesi, paketler geri yüklenirken kullanılacak bir dizi uyumlu hedef belirtmenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="ef172-424">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="ef172-425">DotNet [TXD](../reference/target-frameworks.md) kullanan paketlere, DotNet TXD bildirmeyin uyumlu paketlerle çalışmak üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ef172-425">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="ef172-426">Diğer bir deyişle, projeniz DotNet TXD 'yi kullanıyorsa, DotNet olmayan platformların DotNet ile uyumlu olmasını sağlamak üzere projenize `<PackageTargetFallback>` ' ı eklemediğiniz sürece, bağımlı olduğu tüm paketlerin DotNet TXD olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ef172-426">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="ef172-427">Örneğin, proje `netstandard1.6` TXI kullanıyorsa ve bağımlı bir paket yalnızca `lib/net45/a.dll` ve `lib/portable-net45+win81/a.dll` içeriyorsa, projenin derlenmesi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="ef172-427">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="ef172-428">İçine getirmek istediğiniz değer ikinci DLL ise, `portable-net45+win81` DLL 'inin uyumlu olduğunu söylemek için `PackageTargetFallback` ' ı aşağıdaki şekilde ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ef172-428">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="ef172-429">Projenizdeki tüm hedeflere geri dönüş bildirmek için `Condition` özniteliğini bırakın.</span><span class="sxs-lookup"><span data-stu-id="ef172-429">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="ef172-430">Ayrıca, burada gösterildiği gibi, `$(PackageTargetFallback)` ekleyerek var olan @no__t de genişletebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ef172-430">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="ef172-431">Bir geri yükleme grafiğinden bir kitaplığı değiştirme</span><span class="sxs-lookup"><span data-stu-id="ef172-431">Replacing one library from a restore graph</span></span>

<span data-ttu-id="ef172-432">Geri yükleme yanlış derlemeyi alıyorsa, bu paketlerin varsayılan seçeneğini hariç tutabilir ve kendi seçimiyle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ef172-432">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="ef172-433">İlk olarak @no__t en üst düzey olan-0, tüm varlıkları hariç tut:</span><span class="sxs-lookup"><span data-stu-id="ef172-433">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="ef172-434">Ardından, DLL 'nin uygun yerel kopyasına kendi başvurunuz ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ef172-434">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
