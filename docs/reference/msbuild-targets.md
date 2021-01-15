---
title: NuGet paketi ve geri yükleme MSBuild hedefleri olarak
description: NuGet paketi ve geri yükleme, NuGet 4.0 + ile doğrudan MSBuild hedefleri olarak çalışabilir.
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 7de3f0f1133a89848e9268d489751293fb3cbf25
ms.sourcegitcommit: 323a107c345c7cb4e344a6e6d8de42c63c5188b7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/15/2021
ms.locfileid: "98235704"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="fc1e8-103">NuGet paketi ve geri yükleme MSBuild hedefleri olarak</span><span class="sxs-lookup"><span data-stu-id="fc1e8-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="fc1e8-104">*NuGet 4.0 +*</span><span class="sxs-lookup"><span data-stu-id="fc1e8-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="fc1e8-105">[Packagereference](../consume-packages/package-references-in-project-files.md) biçimi sayesinde, NuGet 4.0 + tüm bildirim meta verilerini ayrı bir dosya kullanmak yerine doğrudan proje dosyası içinde depolayabilirler `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="fc1e8-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="fc1e8-106">MSBuild 15.1 + ile NuGet, `pack` aşağıda açıklandığı gibi, ve hedefleri ile birinci sınıf MSBuild vatandaşlık da vardır `restore` .</span><span class="sxs-lookup"><span data-stu-id="fc1e8-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="fc1e8-107">Bu hedefler, diğer herhangi bir MSBuild görevi veya hedefi ile yaptığınız gibi NuGet ile çalışmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="fc1e8-108">MSBuild kullanarak bir NuGet paketi oluşturma yönergeleri için bkz. [MSBuild kullanarak NuGet paketi oluşturma](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="fc1e8-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="fc1e8-109">(NuGet 3. x ve öncesi için, bunun yerine NuGet CLı aracılığıyla [paketle](../reference/cli-reference/cli-ref-pack.md) ve [geri yükleme](../reference/cli-reference/cli-ref-restore.md) komutlarını kullanırsınız.)</span><span class="sxs-lookup"><span data-stu-id="fc1e8-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="fc1e8-110">Hedef derleme sırası</span><span class="sxs-lookup"><span data-stu-id="fc1e8-110">Target build order</span></span>

<span data-ttu-id="fc1e8-111">`pack`Ve `restore` MSBuild hedefleri olduğundan, iş akışınızı geliştirmek için bunlara erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="fc1e8-112">Örneğin, paketledikten sonra paketinizi bir ağ paylaşımında kopyalamak istediğinizi varsayalım.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="fc1e8-113">Bunu, proje dosyanıza aşağıdakileri ekleyerek yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fc1e8-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="fc1e8-114">Benzer şekilde, MSBuild görevinde bir MSBuild görevi yazabilir, kendi hedefini yazabilir ve NuGet özelliklerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="fc1e8-115">`$(OutputPath)` görelidir ve bu komutu proje kökünden çalıştırdığınız için bekliyor.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="fc1e8-116">paket hedefi</span><span class="sxs-lookup"><span data-stu-id="fc1e8-116">pack target</span></span>

<span data-ttu-id="fc1e8-117">PackageReference biçimini kullanan .NET Standard projeler için, `msbuild -t:pack` bir NuGet paketi oluştururken kullanılacak proje dosyasından girişler çizer.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-117">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="fc1e8-118">Aşağıdaki tabloda, ilk düğüm içindeki bir proje dosyasına eklenebilen MSBuild özellikleri açıklanmaktadır `<PropertyGroup>` .</span><span class="sxs-lookup"><span data-stu-id="fc1e8-118">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="fc1e8-119">Bu düzenlemeleri Visual Studio 2017 ve sonraki sürümlerde kolayca yaparak, projeye sağ tıklayıp bağlam menüsünde **{Project_Name} Düzenle** ' yi seçerek yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="fc1e8-120">Kolaylık olması için tablo, bir [ `.nuspec` dosyadaki](../reference/nuspec.md)denk özelliğe göre düzenlenir.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-120">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="fc1e8-121">`Owners`Ve `Summary` özelliklerinin `.nuspec` MSBuild ile desteklenmediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-121">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="fc1e8-122">Öznitelik/NuSpec değeri</span><span class="sxs-lookup"><span data-stu-id="fc1e8-122">Attribute/NuSpec Value</span></span> | <span data-ttu-id="fc1e8-123">MSBuild özelliği</span><span class="sxs-lookup"><span data-stu-id="fc1e8-123">MSBuild Property</span></span> | <span data-ttu-id="fc1e8-124">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="fc1e8-124">Default</span></span> | <span data-ttu-id="fc1e8-125">Notlar</span><span class="sxs-lookup"><span data-stu-id="fc1e8-125">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="fc1e8-126">Id</span><span class="sxs-lookup"><span data-stu-id="fc1e8-126">Id</span></span> | <span data-ttu-id="fc1e8-127">PackageID</span><span class="sxs-lookup"><span data-stu-id="fc1e8-127">PackageId</span></span> | <span data-ttu-id="fc1e8-128">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="fc1e8-128">AssemblyName</span></span> | <span data-ttu-id="fc1e8-129">MSBuild 'ten $ (AssemblyName)</span><span class="sxs-lookup"><span data-stu-id="fc1e8-129">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="fc1e8-130">Sürüm</span><span class="sxs-lookup"><span data-stu-id="fc1e8-130">Version</span></span> | <span data-ttu-id="fc1e8-131">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="fc1e8-131">PackageVersion</span></span> | <span data-ttu-id="fc1e8-132">Sürüm</span><span class="sxs-lookup"><span data-stu-id="fc1e8-132">Version</span></span> | <span data-ttu-id="fc1e8-133">Bu semver uyumludur, örneğin "1.0.0", "1.0.0-Beta" veya "1.0.0-Beta-00345"</span><span class="sxs-lookup"><span data-stu-id="fc1e8-133">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="fc1e8-134">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="fc1e8-134">VersionPrefix</span></span> | <span data-ttu-id="fc1e8-135">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="fc1e8-135">PackageVersionPrefix</span></span> | <span data-ttu-id="fc1e8-136">empty</span><span class="sxs-lookup"><span data-stu-id="fc1e8-136">empty</span></span> | <span data-ttu-id="fc1e8-137">PackageVersion ayarı PackageVersionPrefix üzerine yazıyor</span><span class="sxs-lookup"><span data-stu-id="fc1e8-137">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="fc1e8-138">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="fc1e8-138">VersionSuffix</span></span> | <span data-ttu-id="fc1e8-139">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="fc1e8-139">PackageVersionSuffix</span></span> | <span data-ttu-id="fc1e8-140">empty</span><span class="sxs-lookup"><span data-stu-id="fc1e8-140">empty</span></span> | <span data-ttu-id="fc1e8-141">MSBuild 'ten $ (VersionSuffix).</span><span class="sxs-lookup"><span data-stu-id="fc1e8-141">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="fc1e8-142">PackageVersion ayarı PackageVersionSuffix üzerine yazıyor</span><span class="sxs-lookup"><span data-stu-id="fc1e8-142">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="fc1e8-143">Yazarlar</span><span class="sxs-lookup"><span data-stu-id="fc1e8-143">Authors</span></span> | <span data-ttu-id="fc1e8-144">Yazarlar</span><span class="sxs-lookup"><span data-stu-id="fc1e8-144">Authors</span></span> | <span data-ttu-id="fc1e8-145">Geçerli kullanıcının Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="fc1e8-145">Username of the current user</span></span> | |
| <span data-ttu-id="fc1e8-146">Sahipler</span><span class="sxs-lookup"><span data-stu-id="fc1e8-146">Owners</span></span> | <span data-ttu-id="fc1e8-147">Yok</span><span class="sxs-lookup"><span data-stu-id="fc1e8-147">N/A</span></span> | <span data-ttu-id="fc1e8-148">NuSpec içinde yok</span><span class="sxs-lookup"><span data-stu-id="fc1e8-148">Not present in NuSpec</span></span> | |
| <span data-ttu-id="fc1e8-149">Başlık</span><span class="sxs-lookup"><span data-stu-id="fc1e8-149">Title</span></span> | <span data-ttu-id="fc1e8-150">Başlık</span><span class="sxs-lookup"><span data-stu-id="fc1e8-150">Title</span></span> | <span data-ttu-id="fc1e8-151">PackageID</span><span class="sxs-lookup"><span data-stu-id="fc1e8-151">The PackageId</span></span>| |
| <span data-ttu-id="fc1e8-152">Description</span><span class="sxs-lookup"><span data-stu-id="fc1e8-152">Description</span></span> | <span data-ttu-id="fc1e8-153">Description</span><span class="sxs-lookup"><span data-stu-id="fc1e8-153">Description</span></span> | <span data-ttu-id="fc1e8-154">"Paket açıklaması"</span><span class="sxs-lookup"><span data-stu-id="fc1e8-154">"Package Description"</span></span> | |
| <span data-ttu-id="fc1e8-155">Telif Hakkı</span><span class="sxs-lookup"><span data-stu-id="fc1e8-155">Copyright</span></span> | <span data-ttu-id="fc1e8-156">Telif Hakkı</span><span class="sxs-lookup"><span data-stu-id="fc1e8-156">Copyright</span></span> | <span data-ttu-id="fc1e8-157">empty</span><span class="sxs-lookup"><span data-stu-id="fc1e8-157">empty</span></span> | |
| <span data-ttu-id="fc1e8-158">Requirelicensekabulünü</span><span class="sxs-lookup"><span data-stu-id="fc1e8-158">RequireLicenseAcceptance</span></span> | <span data-ttu-id="fc1e8-159">Packagerequirelicensekabulünü</span><span class="sxs-lookup"><span data-stu-id="fc1e8-159">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="fc1e8-160">yanlış</span><span class="sxs-lookup"><span data-stu-id="fc1e8-160">false</span></span> | |
| <span data-ttu-id="fc1e8-161">lisans</span><span class="sxs-lookup"><span data-stu-id="fc1e8-161">license</span></span> | <span data-ttu-id="fc1e8-162">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="fc1e8-162">PackageLicenseExpression</span></span> | <span data-ttu-id="fc1e8-163">empty</span><span class="sxs-lookup"><span data-stu-id="fc1e8-163">empty</span></span> | <span data-ttu-id="fc1e8-164">Karşılık gelen `<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="fc1e8-164">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="fc1e8-165">lisans</span><span class="sxs-lookup"><span data-stu-id="fc1e8-165">license</span></span> | <span data-ttu-id="fc1e8-166">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="fc1e8-166">PackageLicenseFile</span></span> | <span data-ttu-id="fc1e8-167">empty</span><span class="sxs-lookup"><span data-stu-id="fc1e8-167">empty</span></span> | <span data-ttu-id="fc1e8-168">Öğesine karşılık gelir `<license type="file">` .</span><span class="sxs-lookup"><span data-stu-id="fc1e8-168">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="fc1e8-169">Başvurulan lisans dosyasını açık bir şekilde paketetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-169">You need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="fc1e8-170">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="fc1e8-170">LicenseUrl</span></span> | <span data-ttu-id="fc1e8-171">PackageLicenseUrl 'Si</span><span class="sxs-lookup"><span data-stu-id="fc1e8-171">PackageLicenseUrl</span></span> | <span data-ttu-id="fc1e8-172">empty</span><span class="sxs-lookup"><span data-stu-id="fc1e8-172">empty</span></span> | <span data-ttu-id="fc1e8-173">`PackageLicenseUrl` kullanım dışı, PackageLicenseExpression veya PackageLicenseFile özelliğini kullanın</span><span class="sxs-lookup"><span data-stu-id="fc1e8-173">`PackageLicenseUrl` is deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="fc1e8-174">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="fc1e8-174">ProjectUrl</span></span> | <span data-ttu-id="fc1e8-175">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="fc1e8-175">PackageProjectUrl</span></span> | <span data-ttu-id="fc1e8-176">empty</span><span class="sxs-lookup"><span data-stu-id="fc1e8-176">empty</span></span> | |
| <span data-ttu-id="fc1e8-177">Simge</span><span class="sxs-lookup"><span data-stu-id="fc1e8-177">Icon</span></span> | <span data-ttu-id="fc1e8-178">Packageıcon</span><span class="sxs-lookup"><span data-stu-id="fc1e8-178">PackageIcon</span></span> | <span data-ttu-id="fc1e8-179">empty</span><span class="sxs-lookup"><span data-stu-id="fc1e8-179">empty</span></span> | <span data-ttu-id="fc1e8-180">Başvurulan simge görüntü dosyasını açıkça paketetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-180">You need to explicitly pack the referenced icon image file.</span></span>|
| <span data-ttu-id="fc1e8-181">Iurl</span><span class="sxs-lookup"><span data-stu-id="fc1e8-181">IconUrl</span></span> | <span data-ttu-id="fc1e8-182">PackageIconUrl 'Si</span><span class="sxs-lookup"><span data-stu-id="fc1e8-182">PackageIconUrl</span></span> | <span data-ttu-id="fc1e8-183">empty</span><span class="sxs-lookup"><span data-stu-id="fc1e8-183">empty</span></span> | <span data-ttu-id="fc1e8-184">En iyi alt düzey deneyim için `PackageIconUrl` öğesine ek olarak belirtilmelidir `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="fc1e8-184">For the best downlevel experience, `PackageIconUrl` should be specified in addition to `PackageIcon`.</span></span> <span data-ttu-id="fc1e8-185">Daha uzun vadeli `PackageIconUrl` kullanım dışı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-185">Longer term, `PackageIconUrl` will be deprecated.</span></span> |
| <span data-ttu-id="fc1e8-186">Etiketler</span><span class="sxs-lookup"><span data-stu-id="fc1e8-186">Tags</span></span> | <span data-ttu-id="fc1e8-187">PackageTags</span><span class="sxs-lookup"><span data-stu-id="fc1e8-187">PackageTags</span></span> | <span data-ttu-id="fc1e8-188">empty</span><span class="sxs-lookup"><span data-stu-id="fc1e8-188">empty</span></span> | <span data-ttu-id="fc1e8-189">Etiketler noktalı virgülle ayrılır.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-189">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="fc1e8-190">Relet 'ler</span><span class="sxs-lookup"><span data-stu-id="fc1e8-190">ReleaseNotes</span></span> | <span data-ttu-id="fc1e8-191">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="fc1e8-191">PackageReleaseNotes</span></span> | <span data-ttu-id="fc1e8-192">empty</span><span class="sxs-lookup"><span data-stu-id="fc1e8-192">empty</span></span> | |
| <span data-ttu-id="fc1e8-193">Depo/URL</span><span class="sxs-lookup"><span data-stu-id="fc1e8-193">Repository/Url</span></span> | <span data-ttu-id="fc1e8-194">Depourl 'Si</span><span class="sxs-lookup"><span data-stu-id="fc1e8-194">RepositoryUrl</span></span> | <span data-ttu-id="fc1e8-195">empty</span><span class="sxs-lookup"><span data-stu-id="fc1e8-195">empty</span></span> | <span data-ttu-id="fc1e8-196">Kaynak kodu kopyalamak veya almak için kullanılan depo URL 'SI.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-196">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="fc1e8-197">Örneğinde *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="fc1e8-197">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="fc1e8-198">Depo/tür</span><span class="sxs-lookup"><span data-stu-id="fc1e8-198">Repository/Type</span></span> | <span data-ttu-id="fc1e8-199">Repositorytype parametrelerinin sağlanması</span><span class="sxs-lookup"><span data-stu-id="fc1e8-199">RepositoryType</span></span> | <span data-ttu-id="fc1e8-200">empty</span><span class="sxs-lookup"><span data-stu-id="fc1e8-200">empty</span></span> | <span data-ttu-id="fc1e8-201">Depo türü.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-201">Repository type.</span></span> <span data-ttu-id="fc1e8-202">Örnekler: *Git*, *TFS*.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-202">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="fc1e8-203">Depo/dal</span><span class="sxs-lookup"><span data-stu-id="fc1e8-203">Repository/Branch</span></span> | <span data-ttu-id="fc1e8-204">Depodalı</span><span class="sxs-lookup"><span data-stu-id="fc1e8-204">RepositoryBranch</span></span> | <span data-ttu-id="fc1e8-205">empty</span><span class="sxs-lookup"><span data-stu-id="fc1e8-205">empty</span></span> | <span data-ttu-id="fc1e8-206">İsteğe bağlı depo dalı bilgileri.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-206">Optional repository branch information.</span></span> <span data-ttu-id="fc1e8-207">Bu özelliğin dahil olması için aynı zamanda bir *Depo-URL* belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-207">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="fc1e8-208">Örnek: *Master* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="fc1e8-208">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="fc1e8-209">Depo/kayıt</span><span class="sxs-lookup"><span data-stu-id="fc1e8-209">Repository/Commit</span></span> | <span data-ttu-id="fc1e8-210">Kayıt yapma</span><span class="sxs-lookup"><span data-stu-id="fc1e8-210">RepositoryCommit</span></span> | <span data-ttu-id="fc1e8-211">empty</span><span class="sxs-lookup"><span data-stu-id="fc1e8-211">empty</span></span> | <span data-ttu-id="fc1e8-212">Paketin hangi kaynağa göre oluşturulduğunu göstermek için isteğe bağlı depo kaydı veya değişiklik kümesi.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-212">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="fc1e8-213">Bu özelliğin dahil olması için aynı zamanda bir *Depo-URL* belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-213">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="fc1e8-214">Örnek: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="fc1e8-214">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="fc1e8-215">PackageType</span><span class="sxs-lookup"><span data-stu-id="fc1e8-215">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="fc1e8-216">Özet</span><span class="sxs-lookup"><span data-stu-id="fc1e8-216">Summary</span></span> | <span data-ttu-id="fc1e8-217">Desteklenmez</span><span class="sxs-lookup"><span data-stu-id="fc1e8-217">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="fc1e8-218">Paket hedef girişleri</span><span class="sxs-lookup"><span data-stu-id="fc1e8-218">pack target inputs</span></span>

- <span data-ttu-id="fc1e8-219">Ispackable</span><span class="sxs-lookup"><span data-stu-id="fc1e8-219">IsPackable</span></span>
- <span data-ttu-id="fc1e8-220">Suppressbağımlıcıeswhenpaketleme</span><span class="sxs-lookup"><span data-stu-id="fc1e8-220">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="fc1e8-221">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="fc1e8-221">PackageVersion</span></span>
- <span data-ttu-id="fc1e8-222">PackageID</span><span class="sxs-lookup"><span data-stu-id="fc1e8-222">PackageId</span></span>
- <span data-ttu-id="fc1e8-223">Yazarlar</span><span class="sxs-lookup"><span data-stu-id="fc1e8-223">Authors</span></span>
- <span data-ttu-id="fc1e8-224">Description</span><span class="sxs-lookup"><span data-stu-id="fc1e8-224">Description</span></span>
- <span data-ttu-id="fc1e8-225">Telif Hakkı</span><span class="sxs-lookup"><span data-stu-id="fc1e8-225">Copyright</span></span>
- <span data-ttu-id="fc1e8-226">Packagerequirelicensekabulünü</span><span class="sxs-lookup"><span data-stu-id="fc1e8-226">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="fc1e8-227">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="fc1e8-227">DevelopmentDependency</span></span>
- <span data-ttu-id="fc1e8-228">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="fc1e8-228">PackageLicenseExpression</span></span>
- <span data-ttu-id="fc1e8-229">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="fc1e8-229">PackageLicenseFile</span></span>
- <span data-ttu-id="fc1e8-230">PackageLicenseUrl 'Si</span><span class="sxs-lookup"><span data-stu-id="fc1e8-230">PackageLicenseUrl</span></span>
- <span data-ttu-id="fc1e8-231">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="fc1e8-231">PackageProjectUrl</span></span>
- <span data-ttu-id="fc1e8-232">PackageIconUrl 'Si</span><span class="sxs-lookup"><span data-stu-id="fc1e8-232">PackageIconUrl</span></span>
- <span data-ttu-id="fc1e8-233">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="fc1e8-233">PackageReleaseNotes</span></span>
- <span data-ttu-id="fc1e8-234">PackageTags</span><span class="sxs-lookup"><span data-stu-id="fc1e8-234">PackageTags</span></span>
- <span data-ttu-id="fc1e8-235">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="fc1e8-235">PackageOutputPath</span></span>
- <span data-ttu-id="fc1e8-236">Includesymbols</span><span class="sxs-lookup"><span data-stu-id="fc1e8-236">IncludeSymbols</span></span>
- <span data-ttu-id="fc1e8-237">Includesource</span><span class="sxs-lookup"><span data-stu-id="fc1e8-237">IncludeSource</span></span>
- <span data-ttu-id="fc1e8-238">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="fc1e8-238">PackageTypes</span></span>
- <span data-ttu-id="fc1e8-239">IsTool</span><span class="sxs-lookup"><span data-stu-id="fc1e8-239">IsTool</span></span>
- <span data-ttu-id="fc1e8-240">Depourl 'Si</span><span class="sxs-lookup"><span data-stu-id="fc1e8-240">RepositoryUrl</span></span>
- <span data-ttu-id="fc1e8-241">Repositorytype parametrelerinin sağlanması</span><span class="sxs-lookup"><span data-stu-id="fc1e8-241">RepositoryType</span></span>
- <span data-ttu-id="fc1e8-242">Depodalı</span><span class="sxs-lookup"><span data-stu-id="fc1e8-242">RepositoryBranch</span></span>
- <span data-ttu-id="fc1e8-243">Kayıt yapma</span><span class="sxs-lookup"><span data-stu-id="fc1e8-243">RepositoryCommit</span></span>
- <span data-ttu-id="fc1e8-244">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="fc1e8-244">NoPackageAnalysis</span></span>
- <span data-ttu-id="fc1e8-245">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="fc1e8-245">MinClientVersion</span></span>
- <span data-ttu-id="fc1e8-246">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="fc1e8-246">IncludeBuildOutput</span></span>
- <span data-ttu-id="fc1e8-247">Includecontentınpack</span><span class="sxs-lookup"><span data-stu-id="fc1e8-247">IncludeContentInPack</span></span>
- <span data-ttu-id="fc1e8-248">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="fc1e8-248">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="fc1e8-249">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="fc1e8-249">ContentTargetFolders</span></span>
- <span data-ttu-id="fc1e8-250">Nusguus dosyası</span><span class="sxs-lookup"><span data-stu-id="fc1e8-250">NuspecFile</span></span>
- <span data-ttu-id="fc1e8-251">Nusgubasepath</span><span class="sxs-lookup"><span data-stu-id="fc1e8-251">NuspecBasePath</span></span>
- <span data-ttu-id="fc1e8-252">Nus, Properties</span><span class="sxs-lookup"><span data-stu-id="fc1e8-252">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="fc1e8-253">paket senaryoları</span><span class="sxs-lookup"><span data-stu-id="fc1e8-253">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="fc1e8-254">Bağımlılıkları gösterme</span><span class="sxs-lookup"><span data-stu-id="fc1e8-254">Suppress dependencies</span></span>

<span data-ttu-id="fc1e8-255">Oluşturulan NuGet paketinden paket bağımlılıklarını bastırmak için, olarak ayarlayın `SuppressDependenciesWhenPacking` ve `true` oluşturulan nupkg dosyasından tüm bağımlılıkların atlanmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-255">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="fc1e8-256">PackageIconUrl 'Si</span><span class="sxs-lookup"><span data-stu-id="fc1e8-256">PackageIconUrl</span></span>

<span data-ttu-id="fc1e8-257">`PackageIconUrl` yeni özellik yararına kullanım dışı olacaktır [`PackageIcon`](#packageicon) .</span><span class="sxs-lookup"><span data-stu-id="fc1e8-257">`PackageIconUrl` will be deprecated in favor of the new [`PackageIcon`](#packageicon) property.</span></span>

<span data-ttu-id="fc1e8-258">NuGet 5,3 & Visual Studio 2019 sürüm 16,3 ' den itibaren, `pack` paket meta verileri yalnızca belirtiyorsa [NU5048](./errors-and-warnings/nu5048.md) uyarı verecek `PackageIconUrl` .</span><span class="sxs-lookup"><span data-stu-id="fc1e8-258">Starting with NuGet 5.3 & Visual Studio 2019 version 16.3, `pack` will raise [NU5048](./errors-and-warnings/nu5048.md) warning if the package metadata only specifies `PackageIconUrl`.</span></span>

### <a name="packageicon"></a><span data-ttu-id="fc1e8-259">Packageıcon</span><span class="sxs-lookup"><span data-stu-id="fc1e8-259">PackageIcon</span></span>

> [!Tip]
> <span data-ttu-id="fc1e8-260">`PackageIcon` `PackageIconUrl` Henüz desteklemeyen istemcilerle ve kaynaklarla geriye dönük uyumluluğu sürdürmek için ve ikisini de belirtmeniz gerekir `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="fc1e8-260">You should specify both `PackageIcon` and `PackageIconUrl` to maintain backward compatibility with clients and sources that do not yet support `PackageIcon`.</span></span> <span data-ttu-id="fc1e8-261">Visual Studio, `PackageIcon` gelecek sürümlerde klasör tabanlı bir kaynaktan gelen paketleri destekleyecektir.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-261">Visual Studio will support `PackageIcon` for packages coming from a folder-based source in a future release.</span></span>

#### <a name="packing-an-icon-image-file"></a><span data-ttu-id="fc1e8-262">Simge görüntüsü dosyası paketleme</span><span class="sxs-lookup"><span data-stu-id="fc1e8-262">Packing an icon image file</span></span>

<span data-ttu-id="fc1e8-263">Bir simge resim dosyası paketleme sırasında, paketin `PackageIcon` köküne göre paket yolunu belirtmek için özelliğini kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-263">When packing an icon image file, you need to use `PackageIcon` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="fc1e8-264">Ayrıca, dosyanın pakete eklendiğinden emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-264">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="fc1e8-265">Görüntü dosyası boyutu 1 MB ile sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-265">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="fc1e8-266">Desteklenen dosya biçimleri JPEG ve PNG içerir.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-266">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="fc1e8-267">128x128 görüntü çözümlemesi yapmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-267">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="fc1e8-268">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="fc1e8-268">For example:</span></span>

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

<span data-ttu-id="fc1e8-269">[Paket simgesi örneği](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span><span class="sxs-lookup"><span data-stu-id="fc1e8-269">[Package Icon sample](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span></span>

<span data-ttu-id="fc1e8-270">Nuspec eşdeğeri için, [simgenin nuspec başvurusuna](nuspec.md#icon)göz atın.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-270">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="fc1e8-271">Çıkış derlemeleri</span><span class="sxs-lookup"><span data-stu-id="fc1e8-271">Output assemblies</span></span>

<span data-ttu-id="fc1e8-272">`nuget pack` çıktı dosyalarını,,,, ve uzantılarına kopyalar `.exe` `.dll` `.xml` `.winmd` `.json` `.pri` .</span><span class="sxs-lookup"><span data-stu-id="fc1e8-272">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="fc1e8-273">Kopyalanan çıkış dosyaları, hedef tarafından MSBuild 'in sağladığı şuna bağlıdır `BuiltOutputProjectGroup` .</span><span class="sxs-lookup"><span data-stu-id="fc1e8-273">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="fc1e8-274">Çıktı derlemelerinin nerede olduğunu denetlemek için, proje dosyanızda veya komut satırında kullanabileceğiniz iki MSBuild özelliği vardır:</span><span class="sxs-lookup"><span data-stu-id="fc1e8-274">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="fc1e8-275">`IncludeBuildOutput`: Derleme çıkış derlemelerinin pakete dahil edilip edilmeyeceğini belirleyen bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-275">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="fc1e8-276">`BuildOutputTargetFolder`: Çıkış derlemelerinin yerleştirilmesi gereken klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-276">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="fc1e8-277">Çıkış derlemeleri (ve diğer çıkış dosyaları) ilgili çerçeve klasörlerine kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-277">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="fc1e8-278">Paket başvuruları</span><span class="sxs-lookup"><span data-stu-id="fc1e8-278">Package references</span></span>

<span data-ttu-id="fc1e8-279">Bkz. [Proje dosyalarındaki paket başvuruları](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="fc1e8-279">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="fc1e8-280">Projeden projeye başvurular</span><span class="sxs-lookup"><span data-stu-id="fc1e8-280">Project to project references</span></span>

<span data-ttu-id="fc1e8-281">Proje başvuruları, varsayılan olarak NuGet paket başvuruları olarak değerlendirilir, örneğin:</span><span class="sxs-lookup"><span data-stu-id="fc1e8-281">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="fc1e8-282">Ayrıca, proje başvurunuz için aşağıdaki meta verileri de ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fc1e8-282">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="fc1e8-283">Bir paketteki içerik ekleme</span><span class="sxs-lookup"><span data-stu-id="fc1e8-283">Including content in a package</span></span>

<span data-ttu-id="fc1e8-284">İçerik eklemek için var olan öğeye ek meta veriler ekleyin `<Content>` .</span><span class="sxs-lookup"><span data-stu-id="fc1e8-284">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="fc1e8-285">Varsayılan olarak, aşağıdaki gibi girdilerle geçersiz kılmadığınız müddetçe "Içerik" türünde her şey pakete dahil edilir:</span><span class="sxs-lookup"><span data-stu-id="fc1e8-285">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="fc1e8-286">Varsayılan olarak, her şey `content` `contentFiles\any\<target_framework>` bir paket içindeki ve klasörünün köküne eklenir ve bir paket yolu belirtmediğiniz takdirde göreli klasör yapısını korur:</span><span class="sxs-lookup"><span data-stu-id="fc1e8-286">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="fc1e8-287">Tüm içeriğinizi yalnızca belirli bir kök klasöre ( `content` ve her ikisi yerine) kopyalamak istiyorsanız, `contentFiles` Varsayılan olarak `ContentTargetFolders` "Content; ContentFiles" olan, ancak başka bir klasör adına ayarlanabilir MSBuild özelliğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-287">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="fc1e8-288">Yalnızca `ContentTargetFolders` dosyaları ' ın altında `contentFiles\any\<target_framework>` veya `contentFiles\<language>\<target_framework>` temel alarak "ContentFiles" seçeneğinin belirtildiğine unutmayın `buildAction` .</span><span class="sxs-lookup"><span data-stu-id="fc1e8-288">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="fc1e8-289">`PackagePath` noktalı virgülle ayrılmış bir hedef yolları kümesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-289">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="fc1e8-290">Boş bir paket yolu belirtilmesi, dosyayı paketin köküne ekler.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-290">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="fc1e8-291">Örneğin, aşağıdaki, `libuv.txt` `content\myfiles` `content\samples` ve paket köküne ekler:</span><span class="sxs-lookup"><span data-stu-id="fc1e8-291">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="fc1e8-292">Ayrıca `$(IncludeContentInPack)` , varsayılan olarak olan MSBuild özelliği de vardır `true` .</span><span class="sxs-lookup"><span data-stu-id="fc1e8-292">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="fc1e8-293">Bu, `false` herhangi bir projede olarak ayarlandıysa, bu projeden içerik NuGet paketine dahil edilmez.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-293">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="fc1e8-294">Yukarıdaki öğelerin herhangi birine ayarlayabileceğiniz diğer paketine özgü meta veriler içerir ```<PackageCopyToOutput>``` ve ```<PackageFlatten>``` ```CopyToOutput``` ```Flatten``` ```contentFiles``` Çıkış nuspec içindeki giriş üzerinde ve değerlerini belirler.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-294">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="fc1e8-295">Içerik öğelerinden ayrı olarak, `<Pack>` ve `<PackagePath>` meta veriler de derleme, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, Designdata, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, Paketleresource veya None derleme eylemine sahip dosyalar üzerinde de ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-295">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="fc1e8-296">Glob desenleri kullanılırken dosya adını paket yolunuza eklemek için paket yolu, klasör ayırıcı karakteriyle bitmelidir; Aksi takdirde, paket yolu dosya adı dahil tam yol olarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-296">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="fc1e8-297">Includesymbols</span><span class="sxs-lookup"><span data-stu-id="fc1e8-297">IncludeSymbols</span></span>

<span data-ttu-id="fc1e8-298">Kullanırken `MSBuild -t:pack -p:IncludeSymbols=true` , karşılık gelen `.pdb` dosyalar diğer çıkış dosyalarıyla birlikte kopyalanır ( `.dll` ,,, `.exe` `.winmd` `.xml` , `.json` , `.pri` ).</span><span class="sxs-lookup"><span data-stu-id="fc1e8-298">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="fc1e8-299">Ayarın `IncludeSymbols=true` düzenli bir paket *ve* bir semboller paketi oluşturduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-299">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="fc1e8-300">Includesource</span><span class="sxs-lookup"><span data-stu-id="fc1e8-300">IncludeSource</span></span>

<span data-ttu-id="fc1e8-301">Bu, `IncludeSymbols` ile aynıdır, ancak kaynak dosyalarını da dosyalarla birlikte kopyalar `.pdb` .</span><span class="sxs-lookup"><span data-stu-id="fc1e8-301">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="fc1e8-302">Tüm dosya türleri, `Compile` `src\<ProjectName>\` elde edilen paketteki göreli yol klasörü yapısını korumak için üzerine kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-302">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="fc1e8-303">Aynı zamanda, olarak ayarlanmış herhangi bir kaynak dosyası için de aynı olur `ProjectReference` `TreatAsPackageReference` `false` .</span><span class="sxs-lookup"><span data-stu-id="fc1e8-303">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="fc1e8-304">Derleme türü bir dosya proje klasörünün dışında ise, ' ye eklenmiştir `src\<ProjectName>\` .</span><span class="sxs-lookup"><span data-stu-id="fc1e8-304">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="fc1e8-305">Lisans ifadesi veya lisans dosyası paketleme</span><span class="sxs-lookup"><span data-stu-id="fc1e8-305">Packing a license expression or a license file</span></span>

<span data-ttu-id="fc1e8-306">Bir lisans ifadesi kullanılırken PackageLicenseExpression özelliğinin kullanılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-306">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="fc1e8-307">[Lisans ifadesi örneği](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="fc1e8-307">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="fc1e8-308">[NuGet.org tarafından kabul edilen lisans ifadeleri ve lisanslar hakkında daha fazla bilgi edinin](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="fc1e8-308">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="fc1e8-309">Bir lisans dosyası paketleme sırasında, paketin köküne göre paket yolunu belirtmek için PackageLicenseFile özelliğini kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-309">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="fc1e8-310">Ayrıca, dosyanın pakete eklendiğinden emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-310">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="fc1e8-311">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="fc1e8-311">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="fc1e8-312">[Lisans dosyası örneği](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="fc1e8-312">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="packing-a-file-without-an-extension"></a><span data-ttu-id="fc1e8-313">Uzantı olmadan dosya paketleme</span><span class="sxs-lookup"><span data-stu-id="fc1e8-313">Packing a file without an extension</span></span>

<span data-ttu-id="fc1e8-314">Bir lisans dosyası paketleme gibi bazı senaryolarda, uzantısı olmayan bir dosya eklemek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-314">In some scenarios, like when packing a license file, you might want to include a file without an extension.</span></span>
<span data-ttu-id="fc1e8-315">Geçmiş nedenlerle NuGet & MSBuild, bir uzantısı olmayan yolları dizin olarak değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-315">For historical reasons, NuGet & MSBuild treat paths without an extension as directories.</span></span>

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

<span data-ttu-id="fc1e8-316">[Dosya uzantı örneği olmadan](https://github.com/NuGet/Samples/blob/master/PackageLicenseFileExtensionlessExample/).</span><span class="sxs-lookup"><span data-stu-id="fc1e8-316">[File without an extension sample](https://github.com/NuGet/Samples/blob/master/PackageLicenseFileExtensionlessExample/).</span></span>
### <a name="istool"></a><span data-ttu-id="fc1e8-317">IsTool</span><span class="sxs-lookup"><span data-stu-id="fc1e8-317">IsTool</span></span>

<span data-ttu-id="fc1e8-318">Kullanırken `MSBuild -t:pack -p:IsTool=true` , [Çıkış derlemeleri](#output-assemblies) senaryosunda belirtilen tüm çıkış dosyaları, `tools` klasörü yerine klasörüne kopyalanır `lib` .</span><span class="sxs-lookup"><span data-stu-id="fc1e8-318">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="fc1e8-319">Bunun, `DotNetCliTool` içindeki dosyasını ayarlayarak belirtilen öğesinden farklı olduğunu unutmayın `PackageType` `.csproj` .</span><span class="sxs-lookup"><span data-stu-id="fc1e8-319">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="fc1e8-320">. Nuspec kullanarak paketleme</span><span class="sxs-lookup"><span data-stu-id="fc1e8-320">Packing using a .nuspec</span></span>

<span data-ttu-id="fc1e8-321">Bunun yerine genellikle proje dosyasındaki dosyada bulunan [tüm özellikleri eklemeniz](../reference/msbuild-targets.md#pack-target) önerilse de `.nuspec` , `.nuspec` projenizi paketlebilmeniz için bir dosya kullanmayı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-321">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="fc1e8-322">Tarafından kullanılan SDK olmayan bir proje için `PackageReference` , paket görevinin yürütülebilmesi için içeri aktarmanız gerekir `NuGet.Build.Tasks.Pack.targets` .</span><span class="sxs-lookup"><span data-stu-id="fc1e8-322">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="fc1e8-323">Bir nuspec dosyası paketetmeden önce projeyi geri yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-323">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="fc1e8-324">(SDK stili bir proje varsayılan olarak paket hedeflerini içerir.)</span><span class="sxs-lookup"><span data-stu-id="fc1e8-324">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="fc1e8-325">Proje dosyasının hedef çerçevesi ilgisizdir ve bir nuspec paketleme sırasında kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-325">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="fc1e8-326">Aşağıdaki üç MSBuild özelliği, ile paketleme ile ilgilidir `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="fc1e8-326">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="fc1e8-327">`NuspecFile`: `.nuspec` paketleme için kullanılan dosyanın göreli veya mutlak yolu.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-327">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="fc1e8-328">`NuspecProperties`: Key = değer çiftleri için noktalı virgülle ayrılmış bir liste.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-328">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="fc1e8-329">MSBuild komut satırı ayrıştırması çalışma yöntemi nedeniyle, birden çok özellik şu şekilde belirtilmelidir: `-p:NuspecProperties="key1=value1;key2=value2"` .</span><span class="sxs-lookup"><span data-stu-id="fc1e8-329">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties="key1=value1;key2=value2"`.</span></span>  
1. <span data-ttu-id="fc1e8-330">`NuspecBasePath`: Dosyanın temel yolu `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="fc1e8-330">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="fc1e8-331">`dotnet.exe`Projenizi paketmek için kullanıyorsanız, aşağıdaki gibi bir komut kullanın:</span><span class="sxs-lookup"><span data-stu-id="fc1e8-331">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="fc1e8-332">Projenizi paketmek için MSBuild kullanıyorsanız, aşağıdaki gibi bir komut kullanın:</span><span class="sxs-lookup"><span data-stu-id="fc1e8-332">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="fc1e8-333">dotnet.exe veya MSBuild kullanarak bir nuspec paketleme, projenin varsayılan olarak oluşturulmasına da neden olduğuna lütfen emin olun.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-333">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="fc1e8-334">Bu, proje dosyanızdaki ```--no-build``` ```<NoBuild>true</NoBuild> ``` ayar ile birlikte proje dosyanızdaki ayarın eşdeğeri olan dotnet.exe özelliği ' a geçirerek kaçınılabilir ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` .</span><span class="sxs-lookup"><span data-stu-id="fc1e8-334">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="fc1e8-335">Bir nuspec dosyası paketiçin bir *. csproj* dosyası örneği:</span><span class="sxs-lookup"><span data-stu-id="fc1e8-335">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="fc1e8-336">Özelleştirilmiş paket oluşturmak için gelişmiş uzantı noktaları</span><span class="sxs-lookup"><span data-stu-id="fc1e8-336">Advanced extension points to create customized package</span></span>

<span data-ttu-id="fc1e8-337">`pack`Hedef, iç, hedef çerçeveye özgü derlemede çalışan iki uzantı noktası sağlar.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-337">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="fc1e8-338">Uzantı noktaları, hedef çerçeveye özgü içerik ve derlemelerin bir pakete dahil edilmesi için destek:</span><span class="sxs-lookup"><span data-stu-id="fc1e8-338">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="fc1e8-339">`TargetsForTfmSpecificBuildOutput` target: klasör içindeki dosyaları `lib` veya kullanılarak belirtilen klasörü kullanın `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="fc1e8-339">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="fc1e8-340">`TargetsForTfmSpecificContentInPackage` target: dışındaki dosyalar için kullanın `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="fc1e8-340">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="fc1e8-341">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="fc1e8-341">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="fc1e8-342">Özel bir hedef yazın ve özelliğin değeri olarak belirtin `$(TargetsForTfmSpecificBuildOutput)` .</span><span class="sxs-lookup"><span data-stu-id="fc1e8-342">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="fc1e8-343">(Varsayılan olarak LIB) öğesine gitmesi gereken tüm dosyalar için `BuildOutputTargetFolder` , hedef bu dosyaları ItemGroup 'a yazmalıdır `BuildOutputInPackage` ve aşağıdaki iki meta veri değerini ayarlamış olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="fc1e8-343">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="fc1e8-344">`FinalOutputPath`: Dosyanın mutlak yolu; sağlanmazsa, kimlik kaynak yolunu değerlendirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-344">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="fc1e8-345">`TargetPath`: (İsteğe bağlı) dosyanın içindeki bir alt klasöre gitmesi gerektiğinde ayarlanır `lib\<TargetFramework>` . Bu, ilgili kültür klasörlerinin altına giten uydu derlemeleri gibi.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-345">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="fc1e8-346">Varsayılan olarak dosyanın adıdır.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-346">Defaults to the name of the file.</span></span>

<span data-ttu-id="fc1e8-347">Örnek:</span><span class="sxs-lookup"><span data-stu-id="fc1e8-347">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="fc1e8-348">Targetsfortfmspecificcontenınpackage</span><span class="sxs-lookup"><span data-stu-id="fc1e8-348">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="fc1e8-349">Özel bir hedef yazın ve özelliğin değeri olarak belirtin `$(TargetsForTfmSpecificContentInPackage)` .</span><span class="sxs-lookup"><span data-stu-id="fc1e8-349">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="fc1e8-350">Pakete dahil edilecek tüm dosyalar için, hedef bu dosyaları ItemGroup 'a yazmalıdır `TfmSpecificPackageFile` ve aşağıdaki isteğe bağlı meta verileri ayarlar:</span><span class="sxs-lookup"><span data-stu-id="fc1e8-350">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="fc1e8-351">`PackagePath`: Dosyanın pakette çıkış olması gereken yol.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-351">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="fc1e8-352">Aynı paket yoluna birden fazla dosya eklenirse NuGet bir uyarı verir.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-352">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="fc1e8-353">`BuildAction`: Dosyaya atanacak derleme eylemi, yalnızca paket yolu `contentFiles` klasörsise gereklidir.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-353">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="fc1e8-354">Varsayılan "none" olarak belirlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-354">Defaults to "None".</span></span>

<span data-ttu-id="fc1e8-355">Örnek:</span><span class="sxs-lookup"><span data-stu-id="fc1e8-355">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="fc1e8-356">hedefi geri yükle</span><span class="sxs-lookup"><span data-stu-id="fc1e8-356">restore target</span></span>

<span data-ttu-id="fc1e8-357">`MSBuild -t:restore` ( `nuget restore` `dotnet restore` .NET Core projeleriyle birlikte kullanılması), proje dosyasında başvurulan paketleri aşağıdaki şekilde geri yükler:</span><span class="sxs-lookup"><span data-stu-id="fc1e8-357">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="fc1e8-358">Proje başvurularına tüm projeyi oku</span><span class="sxs-lookup"><span data-stu-id="fc1e8-358">Read all project to project references</span></span>
1. <span data-ttu-id="fc1e8-359">Ara klasörünü ve hedef çerçeveleri bulmak için proje özelliklerini okuyun</span><span class="sxs-lookup"><span data-stu-id="fc1e8-359">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="fc1e8-360">MSBuild verilerini NuGet.Build.Tasks.dll geçirin</span><span class="sxs-lookup"><span data-stu-id="fc1e8-360">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="fc1e8-361">Geri yüklemeyi Çalıştır</span><span class="sxs-lookup"><span data-stu-id="fc1e8-361">Run restore</span></span>
1. <span data-ttu-id="fc1e8-362">Paketleri İndir</span><span class="sxs-lookup"><span data-stu-id="fc1e8-362">Download packages</span></span>
1. <span data-ttu-id="fc1e8-363">Varlıklar dosyası, hedefler ve props yazma</span><span class="sxs-lookup"><span data-stu-id="fc1e8-363">Write assets file, targets, and props</span></span>

<span data-ttu-id="fc1e8-364">`restore`Hedef, PackageReference biçimini kullanan projeler için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-364">The `restore` target works for projects using the PackageReference format.</span></span>
<span data-ttu-id="fc1e8-365">`MSBuild 16.5+` Ayrıca, biçim için [kabul desteği](#restoring-packagereference-and-packagesconfig-with-msbuild) de vardır `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="fc1e8-365">`MSBuild 16.5+` also has [opt-in support](#restoring-packagereference-and-packagesconfig-with-msbuild) for the `packages.config` format.</span></span>

> [!NOTE]
> <span data-ttu-id="fc1e8-366">`restore`Hedef, hedefle birlikte [çalıştırılmamalıdır](#restoring-and-building-with-one-msbuild-command) `build` .</span><span class="sxs-lookup"><span data-stu-id="fc1e8-366">The `restore` target [should not be run](#restoring-and-building-with-one-msbuild-command) in combination with the `build` target.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="fc1e8-367">Özellikleri geri yükle</span><span class="sxs-lookup"><span data-stu-id="fc1e8-367">Restore properties</span></span>

<span data-ttu-id="fc1e8-368">Ek geri yükleme ayarları proje dosyasındaki MSBuild özelliklerinden gelebilir.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-368">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="fc1e8-369">Değerler, anahtar kullanılarak komut satırından da ayarlanabilir `-p:` (aşağıdaki örneklere bakın).</span><span class="sxs-lookup"><span data-stu-id="fc1e8-369">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="fc1e8-370">Özellik</span><span class="sxs-lookup"><span data-stu-id="fc1e8-370">Property</span></span> | <span data-ttu-id="fc1e8-371">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fc1e8-371">Description</span></span> |
|--------|--------|
| <span data-ttu-id="fc1e8-372">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="fc1e8-372">RestoreSources</span></span> | <span data-ttu-id="fc1e8-373">Paket kaynaklarının noktalı virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-373">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="fc1e8-374">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="fc1e8-374">RestorePackagesPath</span></span> | <span data-ttu-id="fc1e8-375">Kullanıcı paketleri klasör yolu.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-375">User packages folder path.</span></span> |
| <span data-ttu-id="fc1e8-376">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="fc1e8-376">RestoreDisableParallel</span></span> | <span data-ttu-id="fc1e8-377">İndirmeleri tek seferde bir ile sınırlayın.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-377">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="fc1e8-378">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="fc1e8-378">RestoreConfigFile</span></span> | <span data-ttu-id="fc1e8-379">`Nuget.Config`Uygulanacak dosyanın yolu.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-379">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="fc1e8-380">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="fc1e8-380">RestoreNoCache</span></span> | <span data-ttu-id="fc1e8-381">Doğru ise, önbelleğe alınmış paketlerin kullanılmasını önler.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-381">If true, avoids using cached packages.</span></span> <span data-ttu-id="fc1e8-382">Bkz. [genel paketleri ve önbellek klasörlerini yönetme](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="fc1e8-382">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="fc1e8-383">Restoreıgnorefailedsources</span><span class="sxs-lookup"><span data-stu-id="fc1e8-383">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="fc1e8-384">Doğru ise, başarısız veya eksik paket kaynaklarını yoksayar.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-384">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="fc1e8-385">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="fc1e8-385">RestoreFallbackFolders</span></span> | <span data-ttu-id="fc1e8-386">Geri dönüş klasörleri, Kullanıcı paketleri klasörüyle aynı şekilde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-386">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="fc1e8-387">Restoreaddıtionalprojectsources</span><span class="sxs-lookup"><span data-stu-id="fc1e8-387">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="fc1e8-388">Geri yükleme sırasında kullanılacak ek kaynaklar.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-388">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="fc1e8-389">Restoreaddıtionalprojectfallbackfolders</span><span class="sxs-lookup"><span data-stu-id="fc1e8-389">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="fc1e8-390">Geri yükleme sırasında kullanılacak ek geri dönüş klasörleri.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-390">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="fc1e8-391">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="fc1e8-391">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="fc1e8-392">İçinde belirtilen geri dönüş klasörlerini dışlar `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="fc1e8-392">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="fc1e8-393">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="fc1e8-393">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="fc1e8-394">Yolu `NuGet.Build.Tasks.dll` .</span><span class="sxs-lookup"><span data-stu-id="fc1e8-394">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="fc1e8-395">Restoregraphprojectınput</span><span class="sxs-lookup"><span data-stu-id="fc1e8-395">RestoreGraphProjectInput</span></span> | <span data-ttu-id="fc1e8-396">Geri yüklenecek projelerin, mutlak yollar içermesi gereken, noktalı virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-396">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="fc1e8-397">Restoreuseskipnontenttargets</span><span class="sxs-lookup"><span data-stu-id="fc1e8-397">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="fc1e8-398">Projeler MSBuild aracılığıyla toplandığında, iyileştirme kullanılarak toplanıp toplanmayacağını belirler `SkipNonexistentTargets` .</span><span class="sxs-lookup"><span data-stu-id="fc1e8-398">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="fc1e8-399">Ayarlanmazsa, varsayılan olarak olur `true` .</span><span class="sxs-lookup"><span data-stu-id="fc1e8-399">When not set, defaults to `true`.</span></span> <span data-ttu-id="fc1e8-400">Projenin hedefleri içeri aktarılmadığı zaman, sonuç hızlı bir davranıştır.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-400">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="fc1e8-401">Msbuildprojeclarsionspath</span><span class="sxs-lookup"><span data-stu-id="fc1e8-401">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="fc1e8-402">Çıkış klasörü, varsayılan olarak `BaseIntermediateOutputPath` ve `obj` klasörü.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-402">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| <span data-ttu-id="fc1e8-403">Restorezorlamalı</span><span class="sxs-lookup"><span data-stu-id="fc1e8-403">RestoreForce</span></span> | <span data-ttu-id="fc1e8-404">PackageReference tabanlı projelerde, son geri yükleme başarılı olsa bile tüm bağımlılıkların çözülmesini zorlar.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-404">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="fc1e8-405">Bu bayrağın belirtilmesi, dosyanın silinmesine benzer `project.assets.json` .</span><span class="sxs-lookup"><span data-stu-id="fc1e8-405">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="fc1e8-406">Bu, http-cache ' i atlar.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-406">This does not bypass the http-cache.</span></span> |
| <span data-ttu-id="fc1e8-407">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="fc1e8-407">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="fc1e8-408">Bir kilit dosyasının kullanımıyla ilgili olarak.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-408">Opts into the usage of a lock file.</span></span> |
| <span data-ttu-id="fc1e8-409">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="fc1e8-409">RestoreLockedMode</span></span> | <span data-ttu-id="fc1e8-410">Geri yüklemeyi kilitli modda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-410">Run restore in locked mode.</span></span> <span data-ttu-id="fc1e8-411">Bu, geri yüklemenin bağımlılıkları yeniden değerlendirmeyeceği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-411">This means that restore will not reevaluate the dependencies.</span></span> |
| <span data-ttu-id="fc1e8-412">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="fc1e8-412">NuGetLockFilePath</span></span> | <span data-ttu-id="fc1e8-413">Kilit dosyası için özel bir konum.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-413">A custom location for the lock file.</span></span> <span data-ttu-id="fc1e8-414">Varsayılan konum projenin yanında bulunur ve adlandırılır `packages.lock.json` .</span><span class="sxs-lookup"><span data-stu-id="fc1e8-414">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| <span data-ttu-id="fc1e8-415">Restoreforcedeğerlendir</span><span class="sxs-lookup"><span data-stu-id="fc1e8-415">RestoreForceEvaluate</span></span> | <span data-ttu-id="fc1e8-416">Bağımlılıkları yeniden hesaplamak ve herhangi bir uyarı olmadan kilit dosyasını güncelleştirmek için geri yüklemeyi zorlar.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-416">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> |
| <span data-ttu-id="fc1e8-417">RestorePackagesConfig</span><span class="sxs-lookup"><span data-stu-id="fc1e8-417">RestorePackagesConfig</span></span> | <span data-ttu-id="fc1e8-418">packages.config olan projeleri geri yükleyen bir kabul etme anahtarı. Yalnızca ile desteklenir `MSBuild -t:restore` .</span><span class="sxs-lookup"><span data-stu-id="fc1e8-418">An opt-in switch, that restores projects with packages.config. Support with `MSBuild -t:restore` only.</span></span> |
| <span data-ttu-id="fc1e8-419">Restoreusestaticgraphedeğerleme</span><span class="sxs-lookup"><span data-stu-id="fc1e8-419">RestoreUseStaticGraphEvaluation</span></span> | <span data-ttu-id="fc1e8-420">Standart değerlendirme yerine statik grafik MSBuild değerlendirmesi kullanmak için bir tercih edilen anahtar.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-420">An opt-in switch to use static graph MSBuild evaluation instead of the standard evaluation.</span></span> <span data-ttu-id="fc1e8-421">Statik grafik değerlendirmesi, büyük depolar ve çözümler için önemli ölçüde daha hızlı olan deneysel bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-421">Static graph evaluation is an experimental feature that's significantly faster for large repos and solutions.</span></span> |

#### <a name="examples"></a><span data-ttu-id="fc1e8-422">Örnekler</span><span class="sxs-lookup"><span data-stu-id="fc1e8-422">Examples</span></span>

<span data-ttu-id="fc1e8-423">Komut satırı:</span><span class="sxs-lookup"><span data-stu-id="fc1e8-423">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="fc1e8-424">Proje dosyası:</span><span class="sxs-lookup"><span data-stu-id="fc1e8-424">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="fc1e8-425">Çıkışları geri yükleme</span><span class="sxs-lookup"><span data-stu-id="fc1e8-425">Restore outputs</span></span>

<span data-ttu-id="fc1e8-426">Restore derleme klasöründe aşağıdaki dosyaları oluşturur `obj` :</span><span class="sxs-lookup"><span data-stu-id="fc1e8-426">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="fc1e8-427">Dosya</span><span class="sxs-lookup"><span data-stu-id="fc1e8-427">File</span></span> | <span data-ttu-id="fc1e8-428">Description</span><span class="sxs-lookup"><span data-stu-id="fc1e8-428">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="fc1e8-429">Tüm paket başvurularının bağımlılık grafiğini içerir.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-429">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="fc1e8-430">Paketlerde bulunan MSBuild props 'a başvurular</span><span class="sxs-lookup"><span data-stu-id="fc1e8-430">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="fc1e8-431">Paketlerde bulunan MSBuild hedeflerine başvurular</span><span class="sxs-lookup"><span data-stu-id="fc1e8-431">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="fc1e8-432">Tek bir MSBuild komutuyla geri yükleme ve oluşturma</span><span class="sxs-lookup"><span data-stu-id="fc1e8-432">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="fc1e8-433">NuGet, MSBuild hedeflerini ve props 'ı getiren paketleri geri yükleyebilir, geri yükleme ve derleme değerlendirmeleri farklı genel özelliklerle çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-433">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="fc1e8-434">Bu, aşağıdakilerin öngörülemeyen ve genellikle yanlış bir davranışa sahip olacağı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-434">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="fc1e8-435">Bunun yerine önerilen yaklaşım şunlardır:</span><span class="sxs-lookup"><span data-stu-id="fc1e8-435">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="fc1e8-436">Aynı Logic şuna benzer diğer hedefler için de geçerlidir `build` .</span><span class="sxs-lookup"><span data-stu-id="fc1e8-436">The same logic applies to other targets similar to `build`.</span></span>

### <a name="restoring-packagereference-and-packagesconfig-with-msbuild"></a><span data-ttu-id="fc1e8-437">MSBuild ile PackageReference ve packages.config geri yükleme</span><span class="sxs-lookup"><span data-stu-id="fc1e8-437">Restoring PackageReference and packages.config with MSBuild</span></span>

<span data-ttu-id="fc1e8-438">MSBuild 16.5 + ile packages.config de desteklenir `msbuild -t:restore` .</span><span class="sxs-lookup"><span data-stu-id="fc1e8-438">With MSBuild 16.5+, packages.config are also supported for `msbuild -t:restore`.</span></span>

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> <span data-ttu-id="fc1e8-439">`packages.config` restore yalnızca ile kullanılabilir `MSBuild 16.5+` ve `dotnet.exe`</span><span class="sxs-lookup"><span data-stu-id="fc1e8-439">`packages.config` restore is only available with `MSBuild 16.5+`, and not with `dotnet.exe`</span></span>

### <a name="restoring-with-msbuild-static-graph-evaluation"></a><span data-ttu-id="fc1e8-440">MSBuild statik Graph değerlendirmesi ile geri yükleme</span><span class="sxs-lookup"><span data-stu-id="fc1e8-440">Restoring with MSBuild static graph evaluation</span></span>

> [!NOTE]
> <span data-ttu-id="fc1e8-441">MSBuild 16.6 + ile, NuGet, büyük depolar için geri yükleme süresini önemli ölçüde artıran komut satırından statik grafik değerlendirmesi kullanmak için deneysel bir özellik eklemiştir.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-441">With MSBuild 16.6+, NuGet has added an experimental feature to use static graph evaluation from the command line that significantly improves the restore time for large repositories.</span></span>

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

<span data-ttu-id="fc1e8-442">Alternatif olarak, bir dizin. Build. props içindeki özelliği ayarlayarak bunu etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-442">Alternatively you can enable it by setting the property in a Directory.Build.Props.</span></span>

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> <span data-ttu-id="fc1e8-443">Visual Studio 2019. x ve NuGet 5. x itibariyle, bu özellik deneysel ve kabul edilmelidir.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-443">As of Visual Studio 2019.x and NuGet 5.x, this feature is considered experimental and opt-in.</span></span> <span data-ttu-id="fc1e8-444">Bu özelliğin varsayılan olarak etkinleştirileceği hakkında daha fazla bilgi için [NuGet/Home # 9803](https://github.com/NuGet/Home/issues/9803) izleyin.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-444">Follow [NuGet/Home#9803](https://github.com/NuGet/Home/issues/9803) for details on when this feature will be enabled by default.</span></span>

<span data-ttu-id="fc1e8-445">Statik grafik geri yükleme, geri yükleme 'nin MSBuild bölümünü, Proje okuma ve değerlendirme, ancak geri yükleme algoritmasını etkilemez!</span><span class="sxs-lookup"><span data-stu-id="fc1e8-445">Static graph restore changes the msbuild part of restore, the project reading and evaluation, but not the restore algorithm!</span></span> <span data-ttu-id="fc1e8-446">Geri yükleme algoritması tüm NuGet araçları (NuGet.exe, MSBuild.exe, dotnet.exe ve Visual Studio) genelinde aynıdır.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-446">The restore algorithm is the same across all NuGet tools (NuGet.exe, MSBuild.exe, dotnet.exe and Visual Studio).</span></span>

<span data-ttu-id="fc1e8-447">Birçok senaryoda, statik grafik geri yükleme geçerli geri yüklemeden farklı davranabilir ve belirtilen bazı Packagereferklu veya ProjectReferences eksik olabilir.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-447">In very few scenarios, static graph restore may behave differently from current restore and certain declared PackageReferences or ProjectReferences might be missing.</span></span>

<span data-ttu-id="fc1e8-448">Bir kez göz önünde bulundurmanız için, statik grafik geri yüklemeye geçiş yaparken şunu çalıştırmayı göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="fc1e8-448">To ease your mind, as a one time check, when migrating to static graph restore, consider running:</span></span>

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

<span data-ttu-id="fc1e8-449">NuGet hiçbir *değişiklik bildirmemelidir* .</span><span class="sxs-lookup"><span data-stu-id="fc1e8-449">NuGet should *not* report any changes.</span></span> <span data-ttu-id="fc1e8-450">Bir tutarsızlık görürseniz lütfen [NuGet/evde](https://github.com/nuget/home/issues/new)bir sorun bildirin.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-450">If you do see a discrepancy, please file an issue at [NuGet/Home](https://github.com/nuget/home/issues/new).</span></span>

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="fc1e8-451">Bir geri yükleme grafiğinden bir kitaplığı değiştirme</span><span class="sxs-lookup"><span data-stu-id="fc1e8-451">Replacing one library from a restore graph</span></span>

<span data-ttu-id="fc1e8-452">Geri yükleme yanlış derlemeyi alıyorsa, bu paketlerin varsayılan seçeneğini hariç tutabilir ve kendi seçimiyle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="fc1e8-452">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="fc1e8-453">Birincisi, en üst düzeyle `PackageReference` , tüm varlıkları hariç tut:</span><span class="sxs-lookup"><span data-stu-id="fc1e8-453">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="fc1e8-454">Ardından, DLL 'nin uygun yerel kopyasına kendi başvurunuz ekleyin:</span><span class="sxs-lookup"><span data-stu-id="fc1e8-454">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
