---
title: NuGethedef olarak Paketle ve geri yükle MSBuild
description: NuGet Paketleme ve geri yükleme, MSBuild 4.0 + ile doğrudan hedef olarak çalışabilir NuGet .
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
no-loc:
- NuGet
- MSBuild
- .nuspec
- nuspec
ms.openlocfilehash: 47411641db47884f79f2bc9a4aa00035fc79993b
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387380"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="aebff-103">NuGethedef olarak Paketle ve geri yükle MSBuild</span><span class="sxs-lookup"><span data-stu-id="aebff-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="aebff-104">*NuGet 4.0 +*</span><span class="sxs-lookup"><span data-stu-id="aebff-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="aebff-105">[Packagereference](../consume-packages/package-references-in-project-files.md) biçimiyle NuGet 4.0 +, tüm bildirim meta verilerini ayrı bir dosya kullanmak yerine doğrudan proje dosyası içinde depolayabilirler `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="aebff-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="aebff-106">MSBuild15.1 + ile, NuGet MSBuild `pack` aşağıda açıklandığı gibi, ve hedefleriyle birlikte birinci sınıf bir vatandaşlık `restore` .</span><span class="sxs-lookup"><span data-stu-id="aebff-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="aebff-107">Bu hedefler, ile NuGet diğer herhangi bir MSBuild görev veya hedefle yaptığınız gibi çalışmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="aebff-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="aebff-108">Kullanarak paket oluşturma yönergeleri için NuGet MSBuild bkz. [ NuGet kullanarak MSBuild paket oluşturma ](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="aebff-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="aebff-109">(İçin NuGet 3. x ve önceki sürümlerde, bunun yerine CLI aracılığıyla [paketle](../reference/cli-reference/cli-ref-pack.md) ve [geri yükleme](../reference/cli-reference/cli-ref-restore.md) komutlarını kullanırsınız NuGet .)</span><span class="sxs-lookup"><span data-stu-id="aebff-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="aebff-110">Hedef derleme sırası</span><span class="sxs-lookup"><span data-stu-id="aebff-110">Target build order</span></span>

<span data-ttu-id="aebff-111">`pack`Ve `restore` hedefleri olduğundan MSBuild , iş akışınızı iyileştirmek için bunlara erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aebff-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="aebff-112">Örneğin, paketledikten sonra paketinizi bir ağ paylaşımında kopyalamak istediğinizi varsayalım.</span><span class="sxs-lookup"><span data-stu-id="aebff-112">For example, let's say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="aebff-113">Bunu, proje dosyanıza aşağıdakileri ekleyerek yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="aebff-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="aebff-114">Benzer şekilde, bir görev yazabilir MSBuild , kendi hedefini yazabilir ve NuGet görevde özellikleri kullanabilirsiniz MSBuild .</span><span class="sxs-lookup"><span data-stu-id="aebff-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="aebff-115">`$(OutputPath)` görelidir ve bu komutu proje kökünden çalıştırdığınız için bekliyor.</span><span class="sxs-lookup"><span data-stu-id="aebff-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="aebff-116">paket hedefi</span><span class="sxs-lookup"><span data-stu-id="aebff-116">pack target</span></span>

<span data-ttu-id="aebff-117">Biçimini kullanan .NET projeleri için `PackageReference` , `msbuild -t:pack` bir paket oluştururken kullanmak üzere proje dosyasından girişler çizer NuGet .</span><span class="sxs-lookup"><span data-stu-id="aebff-117">For .NET projects that use the `PackageReference` format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="aebff-118">Aşağıdaki tabloda, MSBuild ilk düğüm içindeki bir proje dosyasına eklenebilen özellikler açıklanmaktadır `<PropertyGroup>` .</span><span class="sxs-lookup"><span data-stu-id="aebff-118">The following table describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="aebff-119">Bu düzenlemeleri Visual Studio 2017 ve sonraki sürümlerde kolayca yaparak, projeye sağ tıklayıp bağlam menüsünde **{Project_Name} Düzenle** ' yi seçerek yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aebff-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="aebff-120">Kolaylık sağlaması için tablo, bir [ `.nuspec` dosyadaki](../reference/nuspec.md)denk özelliğe göre düzenlenir.</span><span class="sxs-lookup"><span data-stu-id="aebff-120">For convenience, the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

> [!NOTE]
> <span data-ttu-id="aebff-121">`Owners` ve `Summary` özellikleri `.nuspec` ile desteklenmez MSBuild .</span><span class="sxs-lookup"><span data-stu-id="aebff-121">`Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="aebff-122">Öznitelik/ nuspec değer</span><span class="sxs-lookup"><span data-stu-id="aebff-122">Attribute/nuspec Value</span></span> | <span data-ttu-id="aebff-123">MSBuild Özelliði</span><span class="sxs-lookup"><span data-stu-id="aebff-123">MSBuild Property</span></span> | <span data-ttu-id="aebff-124">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="aebff-124">Default</span></span> | <span data-ttu-id="aebff-125">Notlar</span><span class="sxs-lookup"><span data-stu-id="aebff-125">Notes</span></span> |
|--------|--------|--------|--------|
| `Id` | `PackageId` | `$(AssemblyName)` | <span data-ttu-id="aebff-126">`$(AssemblyName)` Kaynak MSBuild</span><span class="sxs-lookup"><span data-stu-id="aebff-126">`$(AssemblyName)` from MSBuild</span></span> |
| `Version` | `PackageVersion` | <span data-ttu-id="aebff-127">Sürüm</span><span class="sxs-lookup"><span data-stu-id="aebff-127">Version</span></span> | <span data-ttu-id="aebff-128">Bu, örneğin, veya gibi bir semver uyumludur. `1.0.0` `1.0.0-beta``1.0.0-beta-00345`</span><span class="sxs-lookup"><span data-stu-id="aebff-128">This is semver compatible, for example `1.0.0`, `1.0.0-beta`, or `1.0.0-beta-00345`</span></span> |
| `VersionPrefix` | `PackageVersionPrefix` | <span data-ttu-id="aebff-129">empty</span><span class="sxs-lookup"><span data-stu-id="aebff-129">empty</span></span> | <span data-ttu-id="aebff-130">`PackageVersion`Üzerine yazma ayarları`PackageVersionPrefix`</span><span class="sxs-lookup"><span data-stu-id="aebff-130">Setting `PackageVersion` overwrites `PackageVersionPrefix`</span></span> |
| `VersionSuffix` | `PackageVersionSuffix` | <span data-ttu-id="aebff-131">empty</span><span class="sxs-lookup"><span data-stu-id="aebff-131">empty</span></span> | <span data-ttu-id="aebff-132">`$(VersionSuffix)` öğesinden MSBuild .</span><span class="sxs-lookup"><span data-stu-id="aebff-132">`$(VersionSuffix)` from MSBuild.</span></span> <span data-ttu-id="aebff-133">`PackageVersion`Üzerine yazma ayarları`PackageVersionSuffix`</span><span class="sxs-lookup"><span data-stu-id="aebff-133">Setting `PackageVersion` overwrites `PackageVersionSuffix`</span></span> |
| `Authors` | `Authors` | <span data-ttu-id="aebff-134">Geçerli kullanıcının Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="aebff-134">Username of the current user</span></span> | <span data-ttu-id="aebff-135">Nuget.org üzerindeki profil adlarıyla eşleşen paket yazarları için noktalı virgülle ayrılmış bir liste. Bunlar, NuGet NuGet.org üzerindeki galeride görüntülenir ve aynı yazarlara göre çapraz başvuru için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="aebff-135">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| `Owners` | <span data-ttu-id="aebff-136">Yok</span><span class="sxs-lookup"><span data-stu-id="aebff-136">N/A</span></span> | <span data-ttu-id="aebff-137">İçinde yok nuspec</span><span class="sxs-lookup"><span data-stu-id="aebff-137">Not present in nuspec</span></span> | |
| `Title` | `Title` | <span data-ttu-id="aebff-138">`PackageId`</span><span class="sxs-lookup"><span data-stu-id="aebff-138">The `PackageId`</span></span> | <span data-ttu-id="aebff-139">Genellikle, Kullanıcı arabiriminde kullanılan ve Visual Studio 'da paket yöneticisi olarak görüntülenen, paketin kolay bir başlığı.</span><span class="sxs-lookup"><span data-stu-id="aebff-139">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> |
| `Description` | `Description` | <span data-ttu-id="aebff-140">"Paket açıklaması"</span><span class="sxs-lookup"><span data-stu-id="aebff-140">"Package Description"</span></span> | <span data-ttu-id="aebff-141">Derleme için uzun bir açıklama.</span><span class="sxs-lookup"><span data-stu-id="aebff-141">A long description for the assembly.</span></span> <span data-ttu-id="aebff-142">`PackageDescription`Belirtilmezse, bu özellik paketin açıklaması olarak da kullanılır.</span><span class="sxs-lookup"><span data-stu-id="aebff-142">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| `Copyright` | `Copyright` | <span data-ttu-id="aebff-143">empty</span><span class="sxs-lookup"><span data-stu-id="aebff-143">empty</span></span> | <span data-ttu-id="aebff-144">Paket için telif hakkı ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="aebff-144">Copyright details for the package.</span></span> |
| `RequireLicenseAcceptance` | `PackageRequireLicenseAcceptance` | `false` | <span data-ttu-id="aebff-145">İstemcinin paketi yüklemeden önce paket lisansını kabul etmesini isteyip istemeyeceğini belirten bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="aebff-145">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> |
| `license` | `PackageLicenseExpression` | <span data-ttu-id="aebff-146">empty</span><span class="sxs-lookup"><span data-stu-id="aebff-146">empty</span></span> | <span data-ttu-id="aebff-147">Öğesine karşılık gelir `<license type="expression">` .</span><span class="sxs-lookup"><span data-stu-id="aebff-147">Corresponds to `<license type="expression">`.</span></span> <span data-ttu-id="aebff-148">Bkz. [Lisans ifadesi veya lisans dosyası paketleme](#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="aebff-148">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `license` | `PackageLicenseFile` | <span data-ttu-id="aebff-149">empty</span><span class="sxs-lookup"><span data-stu-id="aebff-149">empty</span></span> | <span data-ttu-id="aebff-150">Özel bir lisans veya bir SPDX tanımlayıcısı atanmamış bir lisans kullanıyorsanız paket içindeki bir lisans dosyasının yolu.</span><span class="sxs-lookup"><span data-stu-id="aebff-150">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> <span data-ttu-id="aebff-151">Başvurulan lisans dosyasını açık bir şekilde paketetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="aebff-151">You need to explicitly pack the referenced license file.</span></span> <span data-ttu-id="aebff-152">Öğesine karşılık gelir `<license type="file">` .</span><span class="sxs-lookup"><span data-stu-id="aebff-152">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="aebff-153">Bkz. [Lisans ifadesi veya lisans dosyası paketleme](#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="aebff-153">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `LicenseUrl` | `PackageLicenseUrl` | <span data-ttu-id="aebff-154">empty</span><span class="sxs-lookup"><span data-stu-id="aebff-154">empty</span></span> | <span data-ttu-id="aebff-155">`PackageLicenseUrl` kullanım dışıdır.</span><span class="sxs-lookup"><span data-stu-id="aebff-155">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="aebff-156">`PackageLicenseExpression` `PackageLicenseFile` Bunun yerine veya kullanın.</span><span class="sxs-lookup"><span data-stu-id="aebff-156">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| `ProjectUrl` | `PackageProjectUrl` | <span data-ttu-id="aebff-157">empty</span><span class="sxs-lookup"><span data-stu-id="aebff-157">empty</span></span> | |
| `Icon` | `PackageIcon` | <span data-ttu-id="aebff-158">empty</span><span class="sxs-lookup"><span data-stu-id="aebff-158">empty</span></span> | <span data-ttu-id="aebff-159">Paket simgesi olarak kullanılacak paketteki bir görüntünün yolu.</span><span class="sxs-lookup"><span data-stu-id="aebff-159">A path to an image in the package to use as a package icon.</span></span> <span data-ttu-id="aebff-160">Başvurulan simge görüntü dosyasını açıkça paketetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="aebff-160">You need to explicitly pack the referenced icon image file.</span></span> <span data-ttu-id="aebff-161">Daha fazla bilgi için bkz. [paketleme bir simge görüntü dosyası](#packing-an-icon-image-file) ve [ `icon` meta verileri](./nuspec.md#icon).</span><span class="sxs-lookup"><span data-stu-id="aebff-161">For more information, see [Packing an icon image file](#packing-an-icon-image-file) and [`icon` metadata](./nuspec.md#icon).</span></span> |
| `IconUrl` | `PackageIconUrl` | <span data-ttu-id="aebff-162">empty</span><span class="sxs-lookup"><span data-stu-id="aebff-162">empty</span></span> | <span data-ttu-id="aebff-163">`PackageIconUrl` kullanım dışı bırakılmıştır `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="aebff-163">`PackageIconUrl` is deprecated in favor of `PackageIcon`.</span></span> <span data-ttu-id="aebff-164">Ancak, en iyi alt düzey deneyim için öğesine ek olarak belirtmeniz gerekir `PackageIconUrl` `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="aebff-164">However, for the best downlevel experience, you should specify `PackageIconUrl` in addition to `PackageIcon`.</span></span> |
| `Readme` | `PackageReadmeFile` | <span data-ttu-id="aebff-165">empty</span><span class="sxs-lookup"><span data-stu-id="aebff-165">empty</span></span> | <span data-ttu-id="aebff-166">Başvurulan Benioku dosyasını açıkça paketetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="aebff-166">You need to explicitly pack the referenced readme file.</span></span>|
| `Tags` | `PackageTags` | <span data-ttu-id="aebff-167">empty</span><span class="sxs-lookup"><span data-stu-id="aebff-167">empty</span></span> | <span data-ttu-id="aebff-168">Paketi atayan etiketlerin noktalı virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="aebff-168">A semicolon-delimited list of tags that designates the package.</span></span> |
| `ReleaseNotes` | `PackageReleaseNotes` | <span data-ttu-id="aebff-169">empty</span><span class="sxs-lookup"><span data-stu-id="aebff-169">empty</span></span> | <span data-ttu-id="aebff-170">Paket için sürüm notları.</span><span class="sxs-lookup"><span data-stu-id="aebff-170">Release notes for the package.</span></span> |
| `Repository/Url` | `RepositoryUrl` | <span data-ttu-id="aebff-171">empty</span><span class="sxs-lookup"><span data-stu-id="aebff-171">empty</span></span> | <span data-ttu-id="aebff-172">Kaynak kodu kopyalamak veya almak için kullanılan depo URL 'SI.</span><span class="sxs-lookup"><span data-stu-id="aebff-172">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="aebff-173">Örnek: *https://github.com/ NuGet / NuGet . Client. git*.</span><span class="sxs-lookup"><span data-stu-id="aebff-173">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| `Repository/Type` | `RepositoryType` | <span data-ttu-id="aebff-174">empty</span><span class="sxs-lookup"><span data-stu-id="aebff-174">empty</span></span> | <span data-ttu-id="aebff-175">Depo türü.</span><span class="sxs-lookup"><span data-stu-id="aebff-175">Repository type.</span></span> <span data-ttu-id="aebff-176">Örnekler: `git` (varsayılan), `tfs` .</span><span class="sxs-lookup"><span data-stu-id="aebff-176">Examples: `git` (default), `tfs`.</span></span> |
| `Repository/Branch` | `RepositoryBranch` | <span data-ttu-id="aebff-177">empty</span><span class="sxs-lookup"><span data-stu-id="aebff-177">empty</span></span> | <span data-ttu-id="aebff-178">İsteğe bağlı depo dalı bilgileri.</span><span class="sxs-lookup"><span data-stu-id="aebff-178">Optional repository branch information.</span></span> <span data-ttu-id="aebff-179">`RepositoryUrl` Bu özelliğin dahil edilmesini sağlamak için de belirtilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="aebff-179">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="aebff-180">Örnek: *Master* ( NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="aebff-180">Example: *master* (NuGet 4.7.0+).</span></span> |
| `Repository/Commit` | `RepositoryCommit` | <span data-ttu-id="aebff-181">empty</span><span class="sxs-lookup"><span data-stu-id="aebff-181">empty</span></span> | <span data-ttu-id="aebff-182">Paketin hangi kaynağa göre oluşturulduğunu göstermek için isteğe bağlı depo kaydı veya değişiklik kümesi.</span><span class="sxs-lookup"><span data-stu-id="aebff-182">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="aebff-183">`RepositoryUrl` Bu özelliğin dahil edilmesini sağlamak için de belirtilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="aebff-183">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="aebff-184">Örnek: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="aebff-184">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| `PackageType` | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| `Summary` | <span data-ttu-id="aebff-185">Desteklenmez</span><span class="sxs-lookup"><span data-stu-id="aebff-185">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="aebff-186">Paket hedef girişleri</span><span class="sxs-lookup"><span data-stu-id="aebff-186">pack target inputs</span></span>

| <span data-ttu-id="aebff-187">Özellik</span><span class="sxs-lookup"><span data-stu-id="aebff-187">Property</span></span> | <span data-ttu-id="aebff-188">Açıklama</span><span class="sxs-lookup"><span data-stu-id="aebff-188">Description</span></span> |
| - | - |
| `IsPackable` | <span data-ttu-id="aebff-189">Projenin paketlenemeyeceğini belirten bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="aebff-189">A Boolean value that specifies whether the project can be packed.</span></span> <span data-ttu-id="aebff-190">`true` varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="aebff-190">The default value is `true`.</span></span> |
| `SuppressDependenciesWhenPacking` | <span data-ttu-id="aebff-191">`true`Oluşturulan paketten paket bağımlılıklarını göstermemek için olarak ayarlayın NuGet .</span><span class="sxs-lookup"><span data-stu-id="aebff-191">Set to `true` to suppress package dependencies from the generated NuGet package.</span></span> |
| `PackageVersion` | <span data-ttu-id="aebff-192">Elde edilen paketin sahip olacağı sürümü belirtir.</span><span class="sxs-lookup"><span data-stu-id="aebff-192">Specifies the version that the resulting package will have.</span></span> <span data-ttu-id="aebff-193">Tüm sürüm dizesi biçimlerini kabul eder NuGet .</span><span class="sxs-lookup"><span data-stu-id="aebff-193">Accepts all forms of NuGet version string.</span></span> <span data-ttu-id="aebff-194">Varsayılan değeri,, `$(Version)` Yani, projedeki özelliğinin değeridir `Version` .</span><span class="sxs-lookup"><span data-stu-id="aebff-194">Default is the value of `$(Version)`, that is, of the property `Version` in the project.</span></span> |
| `PackageId` | <span data-ttu-id="aebff-195">Sonuç paketinin adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="aebff-195">Specifies the name for the resulting package.</span></span> <span data-ttu-id="aebff-196">Belirtilmemişse, `pack` işlem varsayılan `AssemblyName` olarak paketin adı ile veya dizin adını kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="aebff-196">If not specified, the `pack` operation will default to using the `AssemblyName` or directory name as the name of the package.</span></span> |
| `PackageDescription` | <span data-ttu-id="aebff-197">UI görüntüleme paketinin uzun açıklaması.</span><span class="sxs-lookup"><span data-stu-id="aebff-197">A long description of the package for UI display.</span></span> |
| `Authors` | <span data-ttu-id="aebff-198">Nuget.org üzerindeki profil adlarıyla eşleşen paket yazarları için noktalı virgülle ayrılmış bir liste. Bunlar, NuGet NuGet.org üzerindeki galeride görüntülenir ve aynı yazarlara göre çapraz başvuru için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="aebff-198">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| `Description` | <span data-ttu-id="aebff-199">Derleme için uzun bir açıklama.</span><span class="sxs-lookup"><span data-stu-id="aebff-199">A long description for the assembly.</span></span> <span data-ttu-id="aebff-200">`PackageDescription`Belirtilmezse, bu özellik paketin açıklaması olarak da kullanılır.</span><span class="sxs-lookup"><span data-stu-id="aebff-200">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| `Copyright` | <span data-ttu-id="aebff-201">Paket için telif hakkı ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="aebff-201">Copyright details for the package.</span></span> |
| `PackageRequireLicenseAcceptance` | <span data-ttu-id="aebff-202">İstemcinin paketi yüklemeden önce paket lisansını kabul etmesini isteyip istemeyeceğini belirten bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="aebff-202">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> <span data-ttu-id="aebff-203">Varsayılan değer: `false`.</span><span class="sxs-lookup"><span data-stu-id="aebff-203">The default is `false`.</span></span> |
| `DevelopmentDependency` | <span data-ttu-id="aebff-204">Paketin bir yalnızca geliştirme bağımlılığı olarak işaretlenip işaretlenmediğini belirten ve paketin diğer paketlere bağımlılık olarak eklenmesini önleyen bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="aebff-204">A Boolean value that specifies whether the package is marked as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="aebff-205">`PackageReference`( NuGet 4.8 +) ile bu bayrak, derleme zamanı varlıklarının derlemeden dışlandığı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="aebff-205">With `PackageReference` (NuGet 4.8+), this flag also means that compile-time assets are excluded from compilation.</span></span> <span data-ttu-id="aebff-206">Daha fazla bilgi için bkz. [PackageReference Için Developmentdependency desteği](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span><span class="sxs-lookup"><span data-stu-id="aebff-206">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span> |
| `PackageLicenseExpression` | <span data-ttu-id="aebff-207">Örneğin, bir [Spdx lisans tanımlayıcısı](https://spdx.org/licenses/) veya ifadesi `Apache-2.0` .</span><span class="sxs-lookup"><span data-stu-id="aebff-207">An [SPDX license identifier](https://spdx.org/licenses/) or expression, for example, `Apache-2.0`.</span></span> <span data-ttu-id="aebff-208">Daha fazla bilgi için bkz. [Lisans ifadesi veya lisans dosyası paketleme](#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="aebff-208">For more information, see [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `PackageLicenseFile` | <span data-ttu-id="aebff-209">Özel bir lisans veya bir SPDX tanımlayıcısı atanmamış bir lisans kullanıyorsanız paket içindeki bir lisans dosyasının yolu.</span><span class="sxs-lookup"><span data-stu-id="aebff-209">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> |
| `PackageLicenseUrl` | <span data-ttu-id="aebff-210">`PackageLicenseUrl` kullanım dışıdır.</span><span class="sxs-lookup"><span data-stu-id="aebff-210">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="aebff-211">`PackageLicenseExpression` `PackageLicenseFile` Bunun yerine veya kullanın.</span><span class="sxs-lookup"><span data-stu-id="aebff-211">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| `PackageProjectUrl` | |
| `PackageIcon` | <span data-ttu-id="aebff-212">Paketin köküne göre paket simge yolunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="aebff-212">Specifies the package icon path, relative to the root of the package.</span></span> <span data-ttu-id="aebff-213">Daha fazla bilgi için bkz. [paketleme a Icon Image File](#packing-an-icon-image-file).</span><span class="sxs-lookup"><span data-stu-id="aebff-213">For more information, see [Packing an icon image file](#packing-an-icon-image-file).</span></span> |
| `PackageReleaseNotes` | <span data-ttu-id="aebff-214">Paket için sürüm notları.</span><span class="sxs-lookup"><span data-stu-id="aebff-214">Release notes for the package.</span></span> |
| `PackageReadmeFile` | <span data-ttu-id="aebff-215">Paket için README.</span><span class="sxs-lookup"><span data-stu-id="aebff-215">Readme for the package.</span></span> |
| `PackageTags` | <span data-ttu-id="aebff-216">Paketi atayan etiketlerin noktalı virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="aebff-216">A semicolon-delimited list of tags that designates the package.</span></span> |
| `PackageOutputPath` | <span data-ttu-id="aebff-217">Paketlenmiş paketin bırakılacak çıkış yolunu belirler.</span><span class="sxs-lookup"><span data-stu-id="aebff-217">Determines the output path in which the packed package will be dropped.</span></span> <span data-ttu-id="aebff-218">`$(OutputPath)` varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="aebff-218">Default is `$(OutputPath)`.</span></span> |
| `IncludeSymbols` | <span data-ttu-id="aebff-219">Bu Boole değeri, paketin proje paketedildiğinde ek bir sembol paketi oluşturup oluşturmayacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="aebff-219">This Boolean value indicates whether the package should create an additional symbols package when the project is packed.</span></span> <span data-ttu-id="aebff-220">Semboller paketinin biçimi, özelliği tarafından denetlenir `SymbolPackageFormat` .</span><span class="sxs-lookup"><span data-stu-id="aebff-220">The symbols package's format is controlled by the `SymbolPackageFormat` property.</span></span> <span data-ttu-id="aebff-221">Daha fazla bilgi için bkz. [ıncludesymbols](#includesymbols).</span><span class="sxs-lookup"><span data-stu-id="aebff-221">For more information, see [IncludeSymbols](#includesymbols).</span></span> |
| `IncludeSource` | <span data-ttu-id="aebff-222">Bu Boole değeri, paket işleminin bir kaynak paketi oluşturup oluşturmayacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="aebff-222">This Boolean value indicates whether the pack process should create a source package.</span></span> <span data-ttu-id="aebff-223">Kaynak paket, kitaplığın kaynak kodunu ve PDB dosyalarını içerir.</span><span class="sxs-lookup"><span data-stu-id="aebff-223">The source package contains the library's source code as well as PDB files.</span></span> <span data-ttu-id="aebff-224">Kaynak dosyalar, `src/ProjectName` elde edilen paket dosyasındaki dizinin altına yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="aebff-224">Source files are put under the `src/ProjectName` directory in the resulting package file.</span></span> <span data-ttu-id="aebff-225">Daha fazla bilgi için bkz. [ıncludesource](#includesource).</span><span class="sxs-lookup"><span data-stu-id="aebff-225">For more information, see [IncludeSource](#includesource).</span></span> |
| `PackageType` | |
| `IsTool` | <span data-ttu-id="aebff-226">Tüm çıkış dosyalarının *lib* klasörü yerine *Araçlar* klasörüne kopyalanıp kopyalanmayacağını belirtir.</span><span class="sxs-lookup"><span data-stu-id="aebff-226">Specifies whether all output files are copied to the *tools* folder instead of the *lib* folder.</span></span> <span data-ttu-id="aebff-227">Daha fazla bilgi için bkz. [ISTool](#istool).</span><span class="sxs-lookup"><span data-stu-id="aebff-227">For more information, see [IsTool](#istool).</span></span> |
| `RepositoryUrl` | <span data-ttu-id="aebff-228">Kaynak kodu kopyalamak veya almak için kullanılan depo URL 'SI.</span><span class="sxs-lookup"><span data-stu-id="aebff-228">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="aebff-229">Örnek: *https://github.com/ NuGet / NuGet . Client. git*.</span><span class="sxs-lookup"><span data-stu-id="aebff-229">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| `RepositoryType` | <span data-ttu-id="aebff-230">Depo türü.</span><span class="sxs-lookup"><span data-stu-id="aebff-230">Repository type.</span></span> <span data-ttu-id="aebff-231">Örnekler: `git` (varsayılan), `tfs` .</span><span class="sxs-lookup"><span data-stu-id="aebff-231">Examples: `git` (default), `tfs`.</span></span> |
| `RepositoryBranch` | <span data-ttu-id="aebff-232">İsteğe bağlı depo dalı bilgileri.</span><span class="sxs-lookup"><span data-stu-id="aebff-232">Optional repository branch information.</span></span> <span data-ttu-id="aebff-233">`RepositoryUrl` Bu özelliğin dahil edilmesini sağlamak için de belirtilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="aebff-233">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="aebff-234">Örnek: *Master* ( NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="aebff-234">Example: *master* (NuGet 4.7.0+).</span></span> |
| `RepositoryCommit` | <span data-ttu-id="aebff-235">Paketin hangi kaynağa göre oluşturulduğunu göstermek için isteğe bağlı depo kaydı veya değişiklik kümesi.</span><span class="sxs-lookup"><span data-stu-id="aebff-235">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="aebff-236">`RepositoryUrl` Bu özelliğin dahil edilmesini sağlamak için de belirtilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="aebff-236">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="aebff-237">Örnek: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="aebff-237">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| `SymbolPackageFormat` | <span data-ttu-id="aebff-238">Semboller paketinin biçimini belirtir.</span><span class="sxs-lookup"><span data-stu-id="aebff-238">Specifies the format of the symbols package.</span></span> <span data-ttu-id="aebff-239">"Symbols. nupkg" ise, pdb 'leri, dll 'Ler ve diğer çıktı dosyalarını içeren *. Symbols. nupkg* Uzantısı ile eski bir sembol paketi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="aebff-239">If "symbols.nupkg", a legacy symbols package is created with a *.symbols.nupkg* extension containing PDBs, DLLs, and other output files.</span></span> <span data-ttu-id="aebff-240">"Snupkg" ise, taşınabilir pdb 'leri içeren bir snupkg sembol paketi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="aebff-240">If "snupkg", a snupkg symbol package is created containing the portable PDBs.</span></span> <span data-ttu-id="aebff-241">Varsayılan değer "symbols. nupkg" dır.</span><span class="sxs-lookup"><span data-stu-id="aebff-241">The default is "symbols.nupkg".</span></span> |
| `NoPackageAnalysis` | <span data-ttu-id="aebff-242">`pack`Paketi derlemeden sonra paket analizini çalıştırmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="aebff-242">Specifies that `pack` should not run package analysis after building the package.</span></span> |
| `MinClientVersion` | <span data-ttu-id="aebff-243">NuGetnuget.exe ve Visual Studio Paket Yöneticisi tarafından zorlanan bu paketi yükleyesağlayan istemcinin en düşük sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="aebff-243">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> |
| `IncludeBuildOutput` | <span data-ttu-id="aebff-244">Bu Boole değeri, derleme çıkış derlemelerinin *. nupkg* dosyasına paketedilip edilmeyeceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="aebff-244">This Boolean value specifies whether the build output assemblies should be packed into the *.nupkg* file or not.</span></span> |
| `IncludeContentInPack` | <span data-ttu-id="aebff-245">Bu Boole değeri, türü olan herhangi bir öğenin `Content` elde edilen pakete otomatik olarak dahil edilip edilmeyeceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="aebff-245">This Boolean value specifies whether any items that have a type of `Content` are included in the resulting package automatically.</span></span> <span data-ttu-id="aebff-246">Varsayılan değer: `true`.</span><span class="sxs-lookup"><span data-stu-id="aebff-246">The default is `true`.</span></span> |
| `BuildOutputTargetFolder` | <span data-ttu-id="aebff-247">Çıkış derlemelerinin yerleştirileceği klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="aebff-247">Specifies the folder where to place the output assemblies.</span></span> <span data-ttu-id="aebff-248">Çıkış derlemeleri (ve diğer çıkış dosyaları) ilgili çerçeve klasörlerine kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="aebff-248">The output assemblies (and other output files) are copied into their respective framework folders.</span></span> <span data-ttu-id="aebff-249">Daha fazla bilgi için bkz. [Çıkış derlemeleri](#output-assemblies).</span><span class="sxs-lookup"><span data-stu-id="aebff-249">For more information, see [Output assemblies](#output-assemblies).</span></span> |
| `ContentTargetFolders` | <span data-ttu-id="aebff-250">Kendileri için belirtilmemişse, tüm içerik dosyalarının gitmesi gereken varsayılan konumu belirtir `PackagePath` .</span><span class="sxs-lookup"><span data-stu-id="aebff-250">Specifies the default location of where all the content files should go if `PackagePath` is not specified for them.</span></span> <span data-ttu-id="aebff-251">Varsayılan değer "Content; contentFiles" dır.</span><span class="sxs-lookup"><span data-stu-id="aebff-251">The default value is "content;contentFiles".</span></span> <span data-ttu-id="aebff-252">Daha fazla bilgi için bkz. [bir paketteki Içerik ekleme](#including-content-in-a-package).</span><span class="sxs-lookup"><span data-stu-id="aebff-252">For more information, see [Including content in a package](#including-content-in-a-package).</span></span> |
| `NuspecFile` | <span data-ttu-id="aebff-253">*.nuspec* Paketleme için kullanılan dosyanın göreli veya mutlak yolu.</span><span class="sxs-lookup"><span data-stu-id="aebff-253">Relative or absolute path to the *.nuspec* file being used for packing.</span></span> <span data-ttu-id="aebff-254">Belirtilmişse, **yalnızca** paketleme bilgileri için kullanılır ve projelerdeki tüm bilgiler kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="aebff-254">If specified, it's used **exclusively** for packaging information, and any information in the projects is not used.</span></span> <span data-ttu-id="aebff-255">Daha fazla bilgi için bkz. [Using a .nuspec paketleme ](#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="aebff-255">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |
| `NuspecBasePath` | <span data-ttu-id="aebff-256">Dosya için temel yol *.nuspec* .</span><span class="sxs-lookup"><span data-stu-id="aebff-256">Base path for the *.nuspec* file.</span></span> <span data-ttu-id="aebff-257">Daha fazla bilgi için bkz. [Using a .nuspec paketleme ](#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="aebff-257">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |
| `NuspecProperties` | <span data-ttu-id="aebff-258">Anahtar = değer çiftlerinin noktalı virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="aebff-258">Semicolon separated list of key=value pairs.</span></span> <span data-ttu-id="aebff-259">Daha fazla bilgi için bkz. [Using a .nuspec paketleme ](#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="aebff-259">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |

## <a name="pack-scenarios"></a><span data-ttu-id="aebff-260">paket senaryoları</span><span class="sxs-lookup"><span data-stu-id="aebff-260">pack scenarios</span></span>

### <a name="suppressing-dependencies"></a><span data-ttu-id="aebff-261">Gizleme bağımlılıkları</span><span class="sxs-lookup"><span data-stu-id="aebff-261">Suppressing dependencies</span></span>

<span data-ttu-id="aebff-262">Oluşturulan paketten paket bağımlılıklarını bastırmak için NuGet , olarak ayarlayın `SuppressDependenciesWhenPacking` ve `true` oluşturulan nupkg dosyasından tüm bağımlılıkların atlanmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="aebff-262">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### `PackageIconUrl`

<span data-ttu-id="aebff-263">`PackageIconUrl` özelliği kullanım dışı bırakılmıştır [`PackageIcon`](#packageicon) .</span><span class="sxs-lookup"><span data-stu-id="aebff-263">`PackageIconUrl` is deprecated in favor of the [`PackageIcon`](#packageicon) property.</span></span> <span data-ttu-id="aebff-264">NuGet5,3 ve Visual Studio 2019 sürüm 16,3 ' den başlayarak, `pack` paket meta verileri yalnızca belirtiyorsa [NU5048](./errors-and-warnings/nu5048.md) uyarı oluşturur `PackageIconUrl` .</span><span class="sxs-lookup"><span data-stu-id="aebff-264">Starting with NuGet 5.3 and Visual Studio 2019 version 16.3, `pack` raises the [NU5048](./errors-and-warnings/nu5048.md) warning if the package metadata only specifies `PackageIconUrl`.</span></span>

### `PackageIcon`

> [!Tip]
> <span data-ttu-id="aebff-265">Henüz desteklemeyen istemcilerle ve kaynaklarla geriye dönük uyumluluk sağlamak için hem hem `PackageIcon` de belirtin `PackageIcon` `PackageIconUrl` .</span><span class="sxs-lookup"><span data-stu-id="aebff-265">To maintain backward compatibility with clients and sources that don't yet support `PackageIcon`, specify both `PackageIcon` and `PackageIconUrl`.</span></span> <span data-ttu-id="aebff-266">Visual Studio, `PackageIcon` Klasör tabanlı bir kaynaktan gelen paketler için destekler.</span><span class="sxs-lookup"><span data-stu-id="aebff-266">Visual Studio supports `PackageIcon` for packages coming from a folder-based source.</span></span>

#### <a name="packing-an-icon-image-file"></a><span data-ttu-id="aebff-267">Simge görüntüsü dosyası paketleme</span><span class="sxs-lookup"><span data-stu-id="aebff-267">Packing an icon image file</span></span>

<span data-ttu-id="aebff-268">Bir simge görüntü dosyası paketleme sırasında, `PackageIcon` paketin köküne göre simge dosya yolunu belirtmek için özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="aebff-268">When packing an icon image file, use `PackageIcon` property to specify the icon file path, relative to the root of the package.</span></span> <span data-ttu-id="aebff-269">Ayrıca, dosyanın pakete eklendiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="aebff-269">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="aebff-270">Görüntü dosyası boyutu 1 MB ile sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="aebff-270">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="aebff-271">Desteklenen dosya biçimleri JPEG ve PNG içerir.</span><span class="sxs-lookup"><span data-stu-id="aebff-271">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="aebff-272">128x128 görüntü çözümlemesi yapmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="aebff-272">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="aebff-273">Örnek:</span><span class="sxs-lookup"><span data-stu-id="aebff-273">For example:</span></span>

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

<span data-ttu-id="aebff-274">[Paket simgesi örneği](https://github.com/NuGet/Samples/tree/main/PackageIconExample).</span><span class="sxs-lookup"><span data-stu-id="aebff-274">[Package Icon sample](https://github.com/NuGet/Samples/tree/main/PackageIconExample).</span></span>

<span data-ttu-id="aebff-275">nuspecEşdeğer bir deyişle, [ nuspec simgeye yönelik başvuruya](nuspec.md#icon)göz atın.</span><span class="sxs-lookup"><span data-stu-id="aebff-275">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="packagereadmefile"></a><span data-ttu-id="aebff-276">PackageReadmeFile</span><span class="sxs-lookup"><span data-stu-id="aebff-276">PackageReadmeFile</span></span>

<span data-ttu-id="aebff-277">Bir Benioku dosyası paketleme sırasında, paketin `PackageReadmeFile` köküne göre paket yolunu belirtmek için özelliğini kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="aebff-277">When packing a readme file, you need to use the `PackageReadmeFile` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="aebff-278">Buna ek olarak, dosyanın pakete eklendiğinden emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="aebff-278">In addition to this, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="aebff-279">Desteklenen dosya biçimleri yalnızca Marklt (*. MD*) içerir.</span><span class="sxs-lookup"><span data-stu-id="aebff-279">Supported file formats include only Markdown (*.md*).</span></span>

<span data-ttu-id="aebff-280">Örnek:</span><span class="sxs-lookup"><span data-stu-id="aebff-280">For example:</span></span>

```xml
<PropertyGroup>
    ...
    <PackageReadmeFile>readme.md</PackageReadmeFile>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="docs\readme.md" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

<span data-ttu-id="aebff-281">nuspecEşdeğer olarak, [ nuspec Benioku için başvuruya](nuspec.md#readme)göz atın.</span><span class="sxs-lookup"><span data-stu-id="aebff-281">For the nuspec equivalent, take a look at [nuspec reference for readme](nuspec.md#readme).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="aebff-282">Çıkış derlemeleri</span><span class="sxs-lookup"><span data-stu-id="aebff-282">Output assemblies</span></span>

<span data-ttu-id="aebff-283">`nuget pack` çıktı dosyalarını,,,, ve uzantılarına kopyalar `.exe` `.dll` `.xml` `.winmd` `.json` `.pri` .</span><span class="sxs-lookup"><span data-stu-id="aebff-283">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="aebff-284">Kopyalanan çıkış dosyaları MSBuild hedeften neler sundığına bağlıdır `BuiltOutputProjectGroup` .</span><span class="sxs-lookup"><span data-stu-id="aebff-284">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="aebff-285">MSBuildÇıktı derlemelerinin nerede olduğunu denetlemek için, proje dosyanızda veya komut satırında kullanabileceğiniz iki özellik vardır:</span><span class="sxs-lookup"><span data-stu-id="aebff-285">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="aebff-286">`IncludeBuildOutput`: Derleme çıkış derlemelerinin pakete dahil edilip edilmeyeceğini belirleyen bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="aebff-286">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="aebff-287">`BuildOutputTargetFolder`: Çıkış derlemelerinin yerleştirilmesi gereken klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="aebff-287">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="aebff-288">Çıkış derlemeleri (ve diğer çıkış dosyaları) ilgili çerçeve klasörlerine kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="aebff-288">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="aebff-289">Paket başvuruları</span><span class="sxs-lookup"><span data-stu-id="aebff-289">Package references</span></span>

<span data-ttu-id="aebff-290">Bkz. [Proje dosyalarındaki paket başvuruları](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="aebff-290">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="aebff-291">Projeden projeye başvurular</span><span class="sxs-lookup"><span data-stu-id="aebff-291">Project to project references</span></span>

<span data-ttu-id="aebff-292">Proje başvurularına proje başvuruları, paket başvuruları olarak varsayılan olarak kabul edilir NuGet .</span><span class="sxs-lookup"><span data-stu-id="aebff-292">Project to project references are considered by default as NuGet package references.</span></span> <span data-ttu-id="aebff-293">Örnek:</span><span class="sxs-lookup"><span data-stu-id="aebff-293">For example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="aebff-294">Ayrıca, proje başvurunuz için aşağıdaki meta verileri de ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="aebff-294">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="aebff-295">Bir paketteki içerik ekleme</span><span class="sxs-lookup"><span data-stu-id="aebff-295">Including content in a package</span></span>

<span data-ttu-id="aebff-296">İçerik eklemek için var olan öğeye ek meta veriler ekleyin `<Content>` .</span><span class="sxs-lookup"><span data-stu-id="aebff-296">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="aebff-297">Varsayılan olarak, aşağıdaki gibi girdilerle geçersiz kılmadığınız müddetçe "Içerik" türünde her şey pakete dahil edilir:</span><span class="sxs-lookup"><span data-stu-id="aebff-297">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="aebff-298">Varsayılan olarak, her şey `content` `contentFiles\any\<target_framework>` bir paket içindeki ve klasörünün köküne eklenir ve bir paket yolu belirtmediğiniz takdirde göreli klasör yapısını korur:</span><span class="sxs-lookup"><span data-stu-id="aebff-298">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="aebff-299">Tüm içeriğinizi yalnızca belirli bir kök klasöre ( `content` ve her ikisi yerine) kopyalamak istiyorsanız, `contentFiles` Varsayılan olarak MSBuild `ContentTargetFolders` "Content; ContentFiles" olarak ayarlanmış ancak başka bir klasör adına ayarlanabilir özelliğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aebff-299">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="aebff-300">Yalnızca `ContentTargetFolders` dosyaları ' ın altında `contentFiles\any\<target_framework>` veya `contentFiles\<language>\<target_framework>` temel alarak "ContentFiles" seçeneğinin belirtildiğine unutmayın `buildAction` .</span><span class="sxs-lookup"><span data-stu-id="aebff-300">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="aebff-301">`PackagePath` noktalı virgülle ayrılmış bir hedef yolları kümesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="aebff-301">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="aebff-302">Boş bir paket yolu belirtilmesi, dosyayı paketin köküne ekler.</span><span class="sxs-lookup"><span data-stu-id="aebff-302">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="aebff-303">Örneğin, aşağıdaki, `libuv.txt` `content\myfiles` `content\samples` ve paket köküne ekler:</span><span class="sxs-lookup"><span data-stu-id="aebff-303">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="aebff-304">Ayrıca MSBuild `$(IncludeContentInPack)` , varsayılan olarak olan bir özellik vardır `true` .</span><span class="sxs-lookup"><span data-stu-id="aebff-304">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="aebff-305">Bu, `false` herhangi bir projede olarak ayarlandıysa, bu projeden içerik NuGet paketine dahil edilmez.</span><span class="sxs-lookup"><span data-stu-id="aebff-305">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="aebff-306">Yukarıdaki öğelerin herhangi birine ayarlayabileceğiniz diğer paketine özgü meta veriler de dahil olmak üzere ```<PackageCopyToOutput>``` ```<PackageFlatten>``` ```CopyToOutput``` ```Flatten``` ```contentFiles``` , çıktı içindeki giriş ve değer değerlerini içerir nuspec .</span><span class="sxs-lookup"><span data-stu-id="aebff-306">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="aebff-307">Içerik öğelerinden ayrı olarak, `<Pack>` ve `<PackagePath>` meta veriler de derleme, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, Designdata, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, Paketleresource veya None derleme eylemine sahip dosyalar üzerinde de ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="aebff-307">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="aebff-308">Glob desenleri kullanılırken dosya adını paket yolunuza eklemek için paket yolu, klasör ayırıcı karakteriyle bitmelidir; Aksi takdirde, paket yolu dosya adı dahil tam yol olarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="aebff-308">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="aebff-309">Includesymbols</span><span class="sxs-lookup"><span data-stu-id="aebff-309">IncludeSymbols</span></span>

<span data-ttu-id="aebff-310">Kullanırken `MSBuild -t:pack -p:IncludeSymbols=true` , karşılık gelen `.pdb` dosyalar diğer çıkış dosyalarıyla birlikte kopyalanır ( `.dll` ,,, `.exe` `.winmd` `.xml` , `.json` , `.pri` ).</span><span class="sxs-lookup"><span data-stu-id="aebff-310">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="aebff-311">Ayarın `IncludeSymbols=true` düzenli bir paket *ve* bir semboller paketi oluşturduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="aebff-311">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="aebff-312">Includesource</span><span class="sxs-lookup"><span data-stu-id="aebff-312">IncludeSource</span></span>

<span data-ttu-id="aebff-313">Bu, `IncludeSymbols` ile aynıdır, ancak kaynak dosyalarını da dosyalarla birlikte kopyalar `.pdb` .</span><span class="sxs-lookup"><span data-stu-id="aebff-313">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="aebff-314">Tüm dosya türleri, `Compile` `src\<ProjectName>\` elde edilen paketteki göreli yol klasörü yapısını korumak için üzerine kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="aebff-314">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="aebff-315">Aynı zamanda, olarak ayarlanmış herhangi bir kaynak dosyası için de aynı olur `ProjectReference` `TreatAsPackageReference` `false` .</span><span class="sxs-lookup"><span data-stu-id="aebff-315">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="aebff-316">Derleme türü bir dosya proje klasörünün dışında ise, ' ye eklenmiştir `src\<ProjectName>\` .</span><span class="sxs-lookup"><span data-stu-id="aebff-316">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="aebff-317">Lisans ifadesi veya lisans dosyası paketleme</span><span class="sxs-lookup"><span data-stu-id="aebff-317">Packing a license expression or a license file</span></span>

<span data-ttu-id="aebff-318">Bir lisans ifadesi kullanırken, `PackageLicenseExpression` özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="aebff-318">When using a license expression, use the `PackageLicenseExpression` property.</span></span> <span data-ttu-id="aebff-319">Bir örnek için bkz. [Lisans ifadesi örneği](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="aebff-319">For a sample, see [License expression sample](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="aebff-320">Lisans ifadeleri ve. org tarafından kabul edilen lisanslar hakkında daha fazla bilgi edinmek için NuGet bkz. [Lisans meta verileri](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="aebff-320">To learn more about license expressions and licenses that are accepted by NuGet.org, see [license metadata](nuspec.md#license).</span></span>

<span data-ttu-id="aebff-321">Bir lisans dosyası paketleme sırasında, paketin `PackageLicenseFile` köküne göre paket yolunu belirtmek için özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="aebff-321">When packing a license file, use `PackageLicenseFile` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="aebff-322">Ayrıca, dosyanın pakete eklendiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="aebff-322">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="aebff-323">Örnek:</span><span class="sxs-lookup"><span data-stu-id="aebff-323">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="aebff-324">Bir örnek için bkz. [Lisans dosyası örneği](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="aebff-324">For a sample, see [License file sample](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample).</span></span>

> [!NOTE]
> <span data-ttu-id="aebff-325">Tek seferde,, ve yalnızca biri `PackageLicenseExpression` `PackageLicenseFile` `PackageLicenseUrl` belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="aebff-325">Only one of `PackageLicenseExpression`, `PackageLicenseFile`, and `PackageLicenseUrl` can be specified at a time.</span></span>

### <a name="packing-a-file-without-an-extension"></a><span data-ttu-id="aebff-326">Uzantı olmadan dosya paketleme</span><span class="sxs-lookup"><span data-stu-id="aebff-326">Packing a file without an extension</span></span>

<span data-ttu-id="aebff-327">Bir lisans dosyası paketleme gibi bazı senaryolarda, uzantısı olmayan bir dosya eklemek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aebff-327">In some scenarios, like when packing a license file, you might want to include a file without an extension.</span></span>
<span data-ttu-id="aebff-328">Geçmiş nedenlerle, NuGet  &  MSBuild bir uzantısı olmayan yolları dizin olarak değerlendirin.</span><span class="sxs-lookup"><span data-stu-id="aebff-328">For historical reasons, NuGet & MSBuild treat paths without an extension as directories.</span></span>

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

<span data-ttu-id="aebff-329">[Dosya uzantı örneği olmadan](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/).</span><span class="sxs-lookup"><span data-stu-id="aebff-329">[File without an extension sample](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/).</span></span>

### <a name="istool"></a><span data-ttu-id="aebff-330">IsTool</span><span class="sxs-lookup"><span data-stu-id="aebff-330">IsTool</span></span>

<span data-ttu-id="aebff-331">Kullanırken `MSBuild -t:pack -p:IsTool=true` , [Çıkış derlemeleri](#output-assemblies) senaryosunda belirtilen tüm çıkış dosyaları, `tools` klasörü yerine klasörüne kopyalanır `lib` .</span><span class="sxs-lookup"><span data-stu-id="aebff-331">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="aebff-332">Bunun, `DotNetCliTool` içindeki dosyasını ayarlayarak belirtilen öğesinden farklı olduğunu unutmayın `PackageType` `.csproj` .</span><span class="sxs-lookup"><span data-stu-id="aebff-332">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec-file"></a><span data-ttu-id="aebff-333">Dosya kullanarak paketleme `.nuspec`</span><span class="sxs-lookup"><span data-stu-id="aebff-333">Packing using a `.nuspec` file</span></span>

<span data-ttu-id="aebff-334">Bunun yerine genellikle proje dosyasındaki dosyada bulunan [tüm özellikleri eklemeniz](../reference/msbuild-targets.md#pack-target) önerilse de `.nuspec` , `.nuspec` projenizi paketlebilmeniz için bir dosya kullanmayı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aebff-334">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="aebff-335">Tarafından kullanılan SDK olmayan bir proje için `PackageReference` , paket görevinin yürütülebilmesi için içeri aktarmanız gerekir `NuGet.Build.Tasks.Pack.targets` .</span><span class="sxs-lookup"><span data-stu-id="aebff-335">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="aebff-336">Bir dosyayı paketetmeden önce projeyi geri yüklemeniz gerekir nuspec .</span><span class="sxs-lookup"><span data-stu-id="aebff-336">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="aebff-337">(SDK stili bir proje varsayılan olarak paket hedeflerini içerir.)</span><span class="sxs-lookup"><span data-stu-id="aebff-337">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="aebff-338">Proje dosyasının hedef çerçevesi ilgisizdir ve bir paketleme sırasında kullanılmaz nuspec .</span><span class="sxs-lookup"><span data-stu-id="aebff-338">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="aebff-339">Aşağıdaki üç MSBuild özellik, ile paketleme için geçerlidir `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="aebff-339">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="aebff-340">`NuspecFile`: `.nuspec` paketleme için kullanılan dosyanın göreli veya mutlak yolu.</span><span class="sxs-lookup"><span data-stu-id="aebff-340">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="aebff-341">`NuspecProperties`: Key = değer çiftleri için noktalı virgülle ayrılmış bir liste.</span><span class="sxs-lookup"><span data-stu-id="aebff-341">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="aebff-342">MSBuildKomut satırı ayrıştırması çalışma yöntemi nedeniyle, birden çok özellik şu şekilde belirtilmelidir: `-p:NuspecProperties="key1=value1;key2=value2"` .</span><span class="sxs-lookup"><span data-stu-id="aebff-342">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties="key1=value1;key2=value2"`.</span></span>  
1. <span data-ttu-id="aebff-343">`NuspecBasePath`: Dosyanın temel yolu `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="aebff-343">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="aebff-344">`dotnet.exe`Projenizi paketmek için kullanıyorsanız, aşağıdaki gibi bir komut kullanın:</span><span class="sxs-lookup"><span data-stu-id="aebff-344">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="aebff-345">MSBuildProjenizi paketmek için kullanıyorsanız, aşağıdaki gibi bir komut kullanın:</span><span class="sxs-lookup"><span data-stu-id="aebff-345">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="aebff-346">nuspecdotnet.exe veya MSBuild kullanan paketleme, projenin varsayılan olarak oluşturulmasına da neden olduğuna emin olun.</span><span class="sxs-lookup"><span data-stu-id="aebff-346">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="aebff-347">Bu, proje dosyanızdaki ```--no-build``` ```<NoBuild>true</NoBuild> ``` ayar ile birlikte proje dosyanızdaki ayarın eşdeğeri olan dotnet.exe özelliği ' a geçirerek kaçınılabilir ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` .</span><span class="sxs-lookup"><span data-stu-id="aebff-347">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="aebff-348">Bir dosyayı paketetmek için *. csproj* dosyası örneği nuspec :</span><span class="sxs-lookup"><span data-stu-id="aebff-348">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="aebff-349">Özelleştirilmiş paket oluşturmak için gelişmiş uzantı noktaları</span><span class="sxs-lookup"><span data-stu-id="aebff-349">Advanced extension points to create customized package</span></span>

<span data-ttu-id="aebff-350">`pack`Hedef, iç, hedef çerçeveye özgü derlemede çalışan iki uzantı noktası sağlar.</span><span class="sxs-lookup"><span data-stu-id="aebff-350">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="aebff-351">Uzantı noktaları, hedef çerçeveye özgü içerik ve derlemelerin bir pakete dahil edilmesi için destek:</span><span class="sxs-lookup"><span data-stu-id="aebff-351">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="aebff-352">`TargetsForTfmSpecificBuildOutput` target: klasör içindeki dosyaları `lib` veya kullanılarak belirtilen klasörü kullanın `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="aebff-352">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="aebff-353">`TargetsForTfmSpecificContentInPackage` target: dışındaki dosyalar için kullanın `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="aebff-353">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### `TargetsForTfmSpecificBuildOutput`

<span data-ttu-id="aebff-354">Özel bir hedef yazın ve özelliğin değeri olarak belirtin `$(TargetsForTfmSpecificBuildOutput)` .</span><span class="sxs-lookup"><span data-stu-id="aebff-354">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="aebff-355">(Varsayılan olarak LIB) öğesine gitmesi gereken tüm dosyalar için `BuildOutputTargetFolder` , hedef bu dosyaları ItemGroup 'a yazmalıdır `BuildOutputInPackage` ve aşağıdaki iki meta veri değerini ayarlamış olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="aebff-355">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="aebff-356">`FinalOutputPath`: Dosyanın mutlak yolu; sağlanmazsa, kimlik kaynak yolunu değerlendirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="aebff-356">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="aebff-357">`TargetPath`: (İsteğe bağlı) dosyanın içindeki bir alt klasöre gitmesi gerektiğinde ayarlanır `lib\<TargetFramework>` . Bu, ilgili kültür klasörlerinin altına giten uydu derlemeleri gibi.</span><span class="sxs-lookup"><span data-stu-id="aebff-357">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="aebff-358">Varsayılan olarak dosyanın adıdır.</span><span class="sxs-lookup"><span data-stu-id="aebff-358">Defaults to the name of the file.</span></span>

<span data-ttu-id="aebff-359">Örnek:</span><span class="sxs-lookup"><span data-stu-id="aebff-359">Example:</span></span>

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

#### `TargetsForTfmSpecificContentInPackage`

<span data-ttu-id="aebff-360">Özel bir hedef yazın ve özelliğin değeri olarak belirtin `$(TargetsForTfmSpecificContentInPackage)` .</span><span class="sxs-lookup"><span data-stu-id="aebff-360">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="aebff-361">Pakete dahil edilecek tüm dosyalar için, hedef bu dosyaları ItemGroup 'a yazmalıdır `TfmSpecificPackageFile` ve aşağıdaki isteğe bağlı meta verileri ayarlar:</span><span class="sxs-lookup"><span data-stu-id="aebff-361">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="aebff-362">`PackagePath`: Dosyanın pakette çıkış olması gereken yol.</span><span class="sxs-lookup"><span data-stu-id="aebff-362">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="aebff-363">NuGet aynı paket yoluna birden fazla dosya eklenirse bir uyarı verir.</span><span class="sxs-lookup"><span data-stu-id="aebff-363">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="aebff-364">`BuildAction`: Dosyaya atanacak derleme eylemi, yalnızca paket yolu `contentFiles` klasörsise gereklidir.</span><span class="sxs-lookup"><span data-stu-id="aebff-364">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="aebff-365">Varsayılan "none" olarak belirlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="aebff-365">Defaults to "None".</span></span>

<span data-ttu-id="aebff-366">Örnek:</span><span class="sxs-lookup"><span data-stu-id="aebff-366">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="aebff-367">hedefi geri yükle</span><span class="sxs-lookup"><span data-stu-id="aebff-367">restore target</span></span>

<span data-ttu-id="aebff-368">`MSBuild -t:restore` ( `nuget restore` `dotnet restore` .NET Core projeleriyle birlikte kullanılması), proje dosyasında başvurulan paketleri aşağıdaki şekilde geri yükler:</span><span class="sxs-lookup"><span data-stu-id="aebff-368">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="aebff-369">Proje başvurularına tüm projeyi oku</span><span class="sxs-lookup"><span data-stu-id="aebff-369">Read all project to project references</span></span>
1. <span data-ttu-id="aebff-370">Ara klasörünü ve hedef çerçeveleri bulmak için proje özelliklerini okuyun</span><span class="sxs-lookup"><span data-stu-id="aebff-370">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="aebff-371">MSBuild.Build.Tasks.dll verileri geçirme NuGet</span><span class="sxs-lookup"><span data-stu-id="aebff-371">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="aebff-372">Geri yüklemeyi Çalıştır</span><span class="sxs-lookup"><span data-stu-id="aebff-372">Run restore</span></span>
1. <span data-ttu-id="aebff-373">Paketleri İndir</span><span class="sxs-lookup"><span data-stu-id="aebff-373">Download packages</span></span>
1. <span data-ttu-id="aebff-374">Varlıklar dosyası, hedefler ve props yazma</span><span class="sxs-lookup"><span data-stu-id="aebff-374">Write assets file, targets, and props</span></span>

<span data-ttu-id="aebff-375">`restore`Hedef, PackageReference biçimini kullanan projeler için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="aebff-375">The `restore` target works for projects using the PackageReference format.</span></span>
<span data-ttu-id="aebff-376">`MSBuild 16.5+` Ayrıca, biçim için [kabul desteği](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) de vardır `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="aebff-376">`MSBuild 16.5+` also has [opt-in support](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) for the `packages.config` format.</span></span>

> [!NOTE]
> <span data-ttu-id="aebff-377">`restore`Hedef, hedefle birlikte [çalıştırılmamalıdır](#restoring-and-building-with-one-msbuild-command) `build` .</span><span class="sxs-lookup"><span data-stu-id="aebff-377">The `restore` target [should not be run](#restoring-and-building-with-one-msbuild-command) in combination with the `build` target.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="aebff-378">Özellikleri geri yükle</span><span class="sxs-lookup"><span data-stu-id="aebff-378">Restore properties</span></span>

<span data-ttu-id="aebff-379">Ek geri yükleme ayarları MSBuild Proje dosyasındaki özelliklerden gelebilir.</span><span class="sxs-lookup"><span data-stu-id="aebff-379">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="aebff-380">Değerler, anahtar kullanılarak komut satırından da ayarlanabilir `-p:` (aşağıdaki örneklere bakın).</span><span class="sxs-lookup"><span data-stu-id="aebff-380">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="aebff-381">Özellik</span><span class="sxs-lookup"><span data-stu-id="aebff-381">Property</span></span> | <span data-ttu-id="aebff-382">Açıklama</span><span class="sxs-lookup"><span data-stu-id="aebff-382">Description</span></span> |
|--------|--------|
| `RestoreSources` | <span data-ttu-id="aebff-383">Paket kaynaklarının noktalı virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="aebff-383">Semicolon-delimited list of package sources.</span></span> |
| `RestorePackagesPath` | <span data-ttu-id="aebff-384">Kullanıcı paketleri klasör yolu.</span><span class="sxs-lookup"><span data-stu-id="aebff-384">User packages folder path.</span></span> |
| `RestoreDisableParallel` | <span data-ttu-id="aebff-385">İndirmeleri tek seferde bir ile sınırlayın.</span><span class="sxs-lookup"><span data-stu-id="aebff-385">Limit downloads to one at a time.</span></span> |
| `RestoreConfigFile` | <span data-ttu-id="aebff-386">`Nuget.Config`Uygulanacak dosyanın yolu.</span><span class="sxs-lookup"><span data-stu-id="aebff-386">Path to a `Nuget.Config` file to apply.</span></span> |
| `RestoreNoCache` | <span data-ttu-id="aebff-387">Doğru ise, önbelleğe alınmış paketlerin kullanılmasını önler.</span><span class="sxs-lookup"><span data-stu-id="aebff-387">If true, avoids using cached packages.</span></span> <span data-ttu-id="aebff-388">Bkz. [genel paketleri ve önbellek klasörlerini yönetme](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="aebff-388">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| `RestoreIgnoreFailedSources` | <span data-ttu-id="aebff-389">Doğru ise, başarısız veya eksik paket kaynaklarını yoksayar.</span><span class="sxs-lookup"><span data-stu-id="aebff-389">If true, ignores failing or missing package sources.</span></span> |
| `RestoreFallbackFolders` | <span data-ttu-id="aebff-390">Geri dönüş klasörleri, Kullanıcı paketleri klasörüyle aynı şekilde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="aebff-390">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| `RestoreAdditionalProjectSources` | <span data-ttu-id="aebff-391">Geri yükleme sırasında kullanılacak ek kaynaklar.</span><span class="sxs-lookup"><span data-stu-id="aebff-391">Additional sources to use during restore.</span></span> |
| `RestoreAdditionalProjectFallbackFolders` | <span data-ttu-id="aebff-392">Geri yükleme sırasında kullanılacak ek geri dönüş klasörleri.</span><span class="sxs-lookup"><span data-stu-id="aebff-392">Additional fallback folders to use during restore.</span></span> |
| `RestoreAdditionalProjectFallbackFoldersExcludes` | <span data-ttu-id="aebff-393">İçinde belirtilen geri dönüş klasörlerini dışlar `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="aebff-393">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| `RestoreTaskAssemblyFile` | <span data-ttu-id="aebff-394">Yolu `NuGet.Build.Tasks.dll` .</span><span class="sxs-lookup"><span data-stu-id="aebff-394">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| `RestoreGraphProjectInput` | <span data-ttu-id="aebff-395">Geri yüklenecek projelerin, mutlak yollar içermesi gereken, noktalı virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="aebff-395">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| `RestoreUseSkipNonexistentTargets`  | <span data-ttu-id="aebff-396">Projeler aracılığıyla toplandığında, MSBuild iyileştirme kullanılarak toplanıp toplanmayacağını belirler `SkipNonexistentTargets` .</span><span class="sxs-lookup"><span data-stu-id="aebff-396">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="aebff-397">Ayarlanmazsa, varsayılan olarak olur `true` .</span><span class="sxs-lookup"><span data-stu-id="aebff-397">When not set, defaults to `true`.</span></span> <span data-ttu-id="aebff-398">Projenin hedefleri içeri aktarılmadığı zaman, sonuç hızlı bir davranıştır.</span><span class="sxs-lookup"><span data-stu-id="aebff-398">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| `MSBuildProjectExtensionsPath` | <span data-ttu-id="aebff-399">Çıkış klasörü, varsayılan olarak `BaseIntermediateOutputPath` ve `obj` klasörü.</span><span class="sxs-lookup"><span data-stu-id="aebff-399">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| `RestoreForce` | <span data-ttu-id="aebff-400">PackageReference tabanlı projelerde, son geri yükleme başarılı olsa bile tüm bağımlılıkların çözülmesini zorlar.</span><span class="sxs-lookup"><span data-stu-id="aebff-400">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="aebff-401">Bu bayrağın belirtilmesi, dosyanın silinmesine benzer `project.assets.json` .</span><span class="sxs-lookup"><span data-stu-id="aebff-401">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="aebff-402">Bu, http-cache ' i atlar.</span><span class="sxs-lookup"><span data-stu-id="aebff-402">This does not bypass the http-cache.</span></span> |
| `RestorePackagesWithLockFile` | <span data-ttu-id="aebff-403">Bir kilit dosyasının kullanımıyla ilgili olarak.</span><span class="sxs-lookup"><span data-stu-id="aebff-403">Opts into the usage of a lock file.</span></span> |
| `RestoreLockedMode` | <span data-ttu-id="aebff-404">Geri yüklemeyi kilitli modda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="aebff-404">Run restore in locked mode.</span></span> <span data-ttu-id="aebff-405">Bu, geri yüklemenin bağımlılıkları yeniden değerlendirmeyeceği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="aebff-405">This means that restore will not reevaluate the dependencies.</span></span> |
| `NuGetLockFilePath` | <span data-ttu-id="aebff-406">Kilit dosyası için özel bir konum.</span><span class="sxs-lookup"><span data-stu-id="aebff-406">A custom location for the lock file.</span></span> <span data-ttu-id="aebff-407">Varsayılan konum projenin yanında bulunur ve adlandırılır `packages.lock.json` .</span><span class="sxs-lookup"><span data-stu-id="aebff-407">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| `RestoreForceEvaluate` | <span data-ttu-id="aebff-408">Bağımlılıkları yeniden hesaplamak ve herhangi bir uyarı olmadan kilit dosyasını güncelleştirmek için geri yüklemeyi zorlar.</span><span class="sxs-lookup"><span data-stu-id="aebff-408">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> |
| `RestorePackagesConfig` | <span data-ttu-id="aebff-409">packages.config olan projeleri geri yükleyen bir kabul etme anahtarı. Yalnızca ile desteklenir `MSBuild -t:restore` .</span><span class="sxs-lookup"><span data-stu-id="aebff-409">An opt-in switch, that restores projects with packages.config. Support with `MSBuild -t:restore` only.</span></span> |
| `RestoreUseStaticGraphEvaluation` | <span data-ttu-id="aebff-410">Standart değerlendirme yerine statik grafik değerlendirmesini kullanmak için bir tercih MSBuild edilen anahtar.</span><span class="sxs-lookup"><span data-stu-id="aebff-410">An opt-in switch to use static graph MSBuild evaluation instead of the standard evaluation.</span></span> <span data-ttu-id="aebff-411">Statik grafik değerlendirmesi, büyük depolar ve çözümler için önemli ölçüde daha hızlı olan deneysel bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="aebff-411">Static graph evaluation is an experimental feature that's significantly faster for large repos and solutions.</span></span> |

#### <a name="examples"></a><span data-ttu-id="aebff-412">Örnekler</span><span class="sxs-lookup"><span data-stu-id="aebff-412">Examples</span></span>

<span data-ttu-id="aebff-413">Komut satırı:</span><span class="sxs-lookup"><span data-stu-id="aebff-413">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="aebff-414">Proje dosyası:</span><span class="sxs-lookup"><span data-stu-id="aebff-414">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="aebff-415">Çıkışları geri yükleme</span><span class="sxs-lookup"><span data-stu-id="aebff-415">Restore outputs</span></span>

<span data-ttu-id="aebff-416">Restore derleme klasöründe aşağıdaki dosyaları oluşturur `obj` :</span><span class="sxs-lookup"><span data-stu-id="aebff-416">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="aebff-417">Dosya</span><span class="sxs-lookup"><span data-stu-id="aebff-417">File</span></span> | <span data-ttu-id="aebff-418">Açıklama</span><span class="sxs-lookup"><span data-stu-id="aebff-418">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="aebff-419">Tüm paket başvurularının bağımlılık grafiğini içerir.</span><span class="sxs-lookup"><span data-stu-id="aebff-419">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="aebff-420">MSBuildPaketlerde bulunan props 'a başvurular</span><span class="sxs-lookup"><span data-stu-id="aebff-420">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="aebff-421">MSBuildPaketlerde bulunan hedeflere başvurular</span><span class="sxs-lookup"><span data-stu-id="aebff-421">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="aebff-422">Tek bir komutla geri yükleme ve oluşturma MSBuild</span><span class="sxs-lookup"><span data-stu-id="aebff-422">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="aebff-423">NuGetHedefleri ve props 'ı getiren paketleri geri yükleyen olgu nedeniyle MSBuild , geri yükleme ve derleme değerlendirmeleri farklı genel özelliklerle çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="aebff-423">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="aebff-424">Bu, aşağıdakilerin öngörülemeyen ve genellikle yanlış bir davranışa sahip olacağı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="aebff-424">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="aebff-425">Bunun yerine önerilen yaklaşım şunlardır:</span><span class="sxs-lookup"><span data-stu-id="aebff-425">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="aebff-426">Aynı Logic şuna benzer diğer hedefler için de geçerlidir `build` .</span><span class="sxs-lookup"><span data-stu-id="aebff-426">The same logic applies to other targets similar to `build`.</span></span>

### <a name="restoring-packagereference-and-packagesconfig-projects-with-msbuild"></a><span data-ttu-id="aebff-427">İle PackageReference ve packages.config projelerini geri yükleme MSBuild</span><span class="sxs-lookup"><span data-stu-id="aebff-427">Restoring PackageReference and packages.config projects with MSBuild</span></span>

<span data-ttu-id="aebff-428">MSBuild16.5 + ile packages.config de desteklenir `msbuild -t:restore` .</span><span class="sxs-lookup"><span data-stu-id="aebff-428">With MSBuild 16.5+, packages.config are also supported for `msbuild -t:restore`.</span></span>

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> <span data-ttu-id="aebff-429">`packages.config` restore yalnızca ile kullanılabilir `MSBuild 16.5+` ve `dotnet.exe`</span><span class="sxs-lookup"><span data-stu-id="aebff-429">`packages.config` restore is only available with `MSBuild 16.5+`, and not with `dotnet.exe`</span></span>

### <a name="restoring-with-msbuild-static-graph-evaluation"></a><span data-ttu-id="aebff-430">MSBuildStatik grafik değerlendirmesi ile geri yükleme</span><span class="sxs-lookup"><span data-stu-id="aebff-430">Restoring with MSBuild static graph evaluation</span></span>

> [!NOTE]
> <span data-ttu-id="aebff-431">MSBuild16.6 + ile, NuGet büyük depolar için geri yükleme süresini önemli ölçüde artıran komut satırından statik grafik değerlendirmesi kullanmak için deneysel bir özellik eklemiştir.</span><span class="sxs-lookup"><span data-stu-id="aebff-431">With MSBuild 16.6+, NuGet has added an experimental feature to use static graph evaluation from the command line that significantly improves the restore time for large repositories.</span></span>

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

<span data-ttu-id="aebff-432">Alternatif olarak, bir dizin. Build. props içindeki özelliği ayarlayarak bunu etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aebff-432">Alternatively you can enable it by setting the property in a Directory.Build.Props.</span></span>

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> <span data-ttu-id="aebff-433">Visual Studio 2019. x ve NuGet 5. x itibariyle, bu özellik deneysel ve kabul edilmelidir.</span><span class="sxs-lookup"><span data-stu-id="aebff-433">As of Visual Studio 2019.x and NuGet 5.x, this feature is considered experimental and opt-in.</span></span> <span data-ttu-id="aebff-434">Bu özelliğin varsayılan olarak etkinleştirileceği hakkında daha fazla bilgi için [ NuGet /Home # 9803](https://github.com/NuGet/Home/issues/9803) izleyin.</span><span class="sxs-lookup"><span data-stu-id="aebff-434">Follow [NuGet/Home#9803](https://github.com/NuGet/Home/issues/9803) for details on when this feature will be enabled by default.</span></span>

<span data-ttu-id="aebff-435">Statik grafik geri yükleme, geri yükleme 'nin MSBuild bölümünü, Proje okuma ve değerlendirme, ancak geri yükleme algoritmasını etkilemez!</span><span class="sxs-lookup"><span data-stu-id="aebff-435">Static graph restore changes the msbuild part of restore, the project reading and evaluation, but not the restore algorithm!</span></span> <span data-ttu-id="aebff-436">Geri yükleme algoritması tüm NuGet araçlarda ( NuGet . exe, MSBuild . exe, dotnet.exe ve Visual Studio) aynıdır.</span><span class="sxs-lookup"><span data-stu-id="aebff-436">The restore algorithm is the same across all NuGet tools (NuGet.exe, MSBuild.exe, dotnet.exe and Visual Studio).</span></span>

<span data-ttu-id="aebff-437">Birçok senaryoda, statik grafik geri yükleme geçerli geri yüklemeden farklı davranabilir ve belirtilen bazı Packagereferklu veya ProjectReferences eksik olabilir.</span><span class="sxs-lookup"><span data-stu-id="aebff-437">In very few scenarios, static graph restore may behave differently from current restore and certain declared PackageReferences or ProjectReferences might be missing.</span></span>

<span data-ttu-id="aebff-438">Bir kez göz önünde bulundurmanız için, statik grafik geri yüklemeye geçiş yaparken şunu çalıştırmayı göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="aebff-438">To ease your mind, as a one time check, when migrating to static graph restore, consider running:</span></span>

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

<span data-ttu-id="aebff-439">NuGet hiçbir *değişiklik raporlanmamalıdır* .</span><span class="sxs-lookup"><span data-stu-id="aebff-439">NuGet should *not* report any changes.</span></span> <span data-ttu-id="aebff-440">Bir tutarsızlık görürseniz, lütfen [ NuGet /Home](https://github.com/nuget/home/issues/new)'ta bir sorun bildirin.</span><span class="sxs-lookup"><span data-stu-id="aebff-440">If you do see a discrepancy, please file an issue at [NuGet/Home](https://github.com/nuget/home/issues/new).</span></span>

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="aebff-441">Bir geri yükleme grafiğinden bir kitaplığı değiştirme</span><span class="sxs-lookup"><span data-stu-id="aebff-441">Replacing one library from a restore graph</span></span>

<span data-ttu-id="aebff-442">Geri yükleme yanlış derlemeyi alıyorsa, bu paketlerin varsayılan seçeneğini hariç tutabilir ve kendi seçimiyle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="aebff-442">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="aebff-443">Birincisi, en üst düzeyle `PackageReference` , tüm varlıkları hariç tut:</span><span class="sxs-lookup"><span data-stu-id="aebff-443">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="aebff-444">Ardından, DLL 'nin uygun yerel kopyasına kendi başvurunuz ekleyin:</span><span class="sxs-lookup"><span data-stu-id="aebff-444">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```