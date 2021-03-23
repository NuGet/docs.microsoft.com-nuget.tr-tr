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
ms.openlocfilehash: 9d40d43d972537ee1cb11d54194ed6450ccd0b6e
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/23/2021
ms.locfileid: "104858972"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="36b5c-103">NuGethedef olarak Paketle ve geri yükle MSBuild</span><span class="sxs-lookup"><span data-stu-id="36b5c-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="36b5c-104">*NuGet 4.0 +*</span><span class="sxs-lookup"><span data-stu-id="36b5c-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="36b5c-105">[Packagereference](../consume-packages/package-references-in-project-files.md) biçimiyle NuGet 4.0 +, tüm bildirim meta verilerini ayrı bir dosya kullanmak yerine doğrudan proje dosyası içinde depolayabilirler `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="36b5c-106">MSBuild15.1 + ile, NuGet MSBuild `pack` aşağıda açıklandığı gibi, ve hedefleriyle birlikte birinci sınıf bir vatandaşlık `restore` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="36b5c-107">Bu hedefler, ile NuGet diğer herhangi bir MSBuild görev veya hedefle yaptığınız gibi çalışmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="36b5c-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="36b5c-108">Kullanarak paket oluşturma yönergeleri için NuGet MSBuild bkz. [ NuGet kullanarak MSBuild paket oluşturma ](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="36b5c-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="36b5c-109">(İçin NuGet 3. x ve önceki sürümlerde, bunun yerine CLI aracılığıyla [paketle](../reference/cli-reference/cli-ref-pack.md) ve [geri yükleme](../reference/cli-reference/cli-ref-restore.md) komutlarını kullanırsınız NuGet .)</span><span class="sxs-lookup"><span data-stu-id="36b5c-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="36b5c-110">Hedef derleme sırası</span><span class="sxs-lookup"><span data-stu-id="36b5c-110">Target build order</span></span>

<span data-ttu-id="36b5c-111">`pack`Ve `restore` hedefleri olduğundan MSBuild , iş akışınızı iyileştirmek için bunlara erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="36b5c-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="36b5c-112">Örneğin, paketledikten sonra paketinizi bir ağ paylaşımında kopyalamak istediğinizi varsayalım.</span><span class="sxs-lookup"><span data-stu-id="36b5c-112">For example, let's say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="36b5c-113">Bunu, proje dosyanıza aşağıdakileri ekleyerek yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="36b5c-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="36b5c-114">Benzer şekilde, bir görev yazabilir MSBuild , kendi hedefini yazabilir ve NuGet görevde özellikleri kullanabilirsiniz MSBuild .</span><span class="sxs-lookup"><span data-stu-id="36b5c-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="36b5c-115">`$(OutputPath)` görelidir ve bu komutu proje kökünden çalıştırdığınız için bekliyor.</span><span class="sxs-lookup"><span data-stu-id="36b5c-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="36b5c-116">paket hedefi</span><span class="sxs-lookup"><span data-stu-id="36b5c-116">pack target</span></span>

<span data-ttu-id="36b5c-117">Biçimini kullanan .NET projeleri için `PackageReference` , `msbuild -t:pack` bir paket oluştururken kullanmak üzere proje dosyasından girişler çizer NuGet .</span><span class="sxs-lookup"><span data-stu-id="36b5c-117">For .NET projects that use the `PackageReference` format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="36b5c-118">Aşağıdaki tabloda, MSBuild ilk düğüm içindeki bir proje dosyasına eklenebilen özellikler açıklanmaktadır `<PropertyGroup>` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-118">The following table describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="36b5c-119">Bu düzenlemeleri Visual Studio 2017 ve sonraki sürümlerde kolayca yaparak, projeye sağ tıklayıp bağlam menüsünde **{Project_Name} Düzenle** ' yi seçerek yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="36b5c-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="36b5c-120">Kolaylık sağlaması için tablo, bir [ `.nuspec` dosyadaki](../reference/nuspec.md)denk özelliğe göre düzenlenir.</span><span class="sxs-lookup"><span data-stu-id="36b5c-120">For convenience, the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

> [!NOTE]
> <span data-ttu-id="36b5c-121">`Owners` ve `Summary` özellikleri `.nuspec` ile desteklenmez MSBuild .</span><span class="sxs-lookup"><span data-stu-id="36b5c-121">`Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="36b5c-122">Öznitelik/ nuspec değer</span><span class="sxs-lookup"><span data-stu-id="36b5c-122">Attribute/nuspec Value</span></span> | <span data-ttu-id="36b5c-123">MSBuild Özelliði</span><span class="sxs-lookup"><span data-stu-id="36b5c-123">MSBuild Property</span></span> | <span data-ttu-id="36b5c-124">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="36b5c-124">Default</span></span> | <span data-ttu-id="36b5c-125">Notlar</span><span class="sxs-lookup"><span data-stu-id="36b5c-125">Notes</span></span> |
|--------|--------|--------|--------|
| `Id` | `PackageId` | `$(AssemblyName)` | <span data-ttu-id="36b5c-126">`$(AssemblyName)` Kaynak MSBuild</span><span class="sxs-lookup"><span data-stu-id="36b5c-126">`$(AssemblyName)` from MSBuild</span></span> |
| `Version` | `PackageVersion` | <span data-ttu-id="36b5c-127">Sürüm</span><span class="sxs-lookup"><span data-stu-id="36b5c-127">Version</span></span> | <span data-ttu-id="36b5c-128">Bu, örneğin, veya gibi bir semver uyumludur. `1.0.0` `1.0.0-beta``1.0.0-beta-00345`</span><span class="sxs-lookup"><span data-stu-id="36b5c-128">This is semver compatible, for example `1.0.0`, `1.0.0-beta`, or `1.0.0-beta-00345`</span></span> |
| `VersionPrefix` | `PackageVersionPrefix` | <span data-ttu-id="36b5c-129">empty</span><span class="sxs-lookup"><span data-stu-id="36b5c-129">empty</span></span> | <span data-ttu-id="36b5c-130">`PackageVersion`Üzerine yazma ayarları`PackageVersionPrefix`</span><span class="sxs-lookup"><span data-stu-id="36b5c-130">Setting `PackageVersion` overwrites `PackageVersionPrefix`</span></span> |
| `VersionSuffix` | `PackageVersionSuffix` | <span data-ttu-id="36b5c-131">empty</span><span class="sxs-lookup"><span data-stu-id="36b5c-131">empty</span></span> | <span data-ttu-id="36b5c-132">`$(VersionSuffix)` öğesinden MSBuild .</span><span class="sxs-lookup"><span data-stu-id="36b5c-132">`$(VersionSuffix)` from MSBuild.</span></span> <span data-ttu-id="36b5c-133">`PackageVersion`Üzerine yazma ayarları`PackageVersionSuffix`</span><span class="sxs-lookup"><span data-stu-id="36b5c-133">Setting `PackageVersion` overwrites `PackageVersionSuffix`</span></span> |
| `Authors` | `Authors` | <span data-ttu-id="36b5c-134">Geçerli kullanıcının Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="36b5c-134">Username of the current user</span></span> | <span data-ttu-id="36b5c-135">Nuget.org üzerindeki profil adlarıyla eşleşen paket yazarları için noktalı virgülle ayrılmış bir liste. Bunlar, NuGet NuGet.org üzerindeki galeride görüntülenir ve aynı yazarlara göre çapraz başvuru için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="36b5c-135">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| `Owners` | <span data-ttu-id="36b5c-136">Yok</span><span class="sxs-lookup"><span data-stu-id="36b5c-136">N/A</span></span> | <span data-ttu-id="36b5c-137">İçinde yok nuspec</span><span class="sxs-lookup"><span data-stu-id="36b5c-137">Not present in nuspec</span></span> | |
| `Title` | `Title` | <span data-ttu-id="36b5c-138">`PackageId`</span><span class="sxs-lookup"><span data-stu-id="36b5c-138">The `PackageId`</span></span> | <span data-ttu-id="36b5c-139">Genellikle, Kullanıcı arabiriminde kullanılan ve Visual Studio 'da paket yöneticisi olarak görüntülenen, paketin kolay bir başlığı.</span><span class="sxs-lookup"><span data-stu-id="36b5c-139">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> |
| `Description` | `Description` | <span data-ttu-id="36b5c-140">"Paket açıklaması"</span><span class="sxs-lookup"><span data-stu-id="36b5c-140">"Package Description"</span></span> | <span data-ttu-id="36b5c-141">Derleme için uzun bir açıklama.</span><span class="sxs-lookup"><span data-stu-id="36b5c-141">A long description for the assembly.</span></span> <span data-ttu-id="36b5c-142">`PackageDescription`Belirtilmezse, bu özellik paketin açıklaması olarak da kullanılır.</span><span class="sxs-lookup"><span data-stu-id="36b5c-142">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| `Copyright` | `Copyright` | <span data-ttu-id="36b5c-143">empty</span><span class="sxs-lookup"><span data-stu-id="36b5c-143">empty</span></span> | <span data-ttu-id="36b5c-144">Paket için telif hakkı ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="36b5c-144">Copyright details for the package.</span></span> |
| `RequireLicenseAcceptance` | `PackageRequireLicenseAcceptance` | `false` | <span data-ttu-id="36b5c-145">İstemcinin paketi yüklemeden önce paket lisansını kabul etmesini isteyip istemeyeceğini belirten bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="36b5c-145">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> |
| `license` | `PackageLicenseExpression` | <span data-ttu-id="36b5c-146">empty</span><span class="sxs-lookup"><span data-stu-id="36b5c-146">empty</span></span> | <span data-ttu-id="36b5c-147">Öğesine karşılık gelir `<license type="expression">` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-147">Corresponds to `<license type="expression">`.</span></span> <span data-ttu-id="36b5c-148">Bkz. [Lisans ifadesi veya lisans dosyası paketleme](#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="36b5c-148">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `license` | `PackageLicenseFile` | <span data-ttu-id="36b5c-149">empty</span><span class="sxs-lookup"><span data-stu-id="36b5c-149">empty</span></span> | <span data-ttu-id="36b5c-150">Özel bir lisans veya bir SPDX tanımlayıcısı atanmamış bir lisans kullanıyorsanız paket içindeki bir lisans dosyasının yolu.</span><span class="sxs-lookup"><span data-stu-id="36b5c-150">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> <span data-ttu-id="36b5c-151">Başvurulan lisans dosyasını açık bir şekilde paketetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="36b5c-151">You need to explicitly pack the referenced license file.</span></span> <span data-ttu-id="36b5c-152">Öğesine karşılık gelir `<license type="file">` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-152">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="36b5c-153">Bkz. [Lisans ifadesi veya lisans dosyası paketleme](#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="36b5c-153">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `LicenseUrl` | `PackageLicenseUrl` | <span data-ttu-id="36b5c-154">empty</span><span class="sxs-lookup"><span data-stu-id="36b5c-154">empty</span></span> | <span data-ttu-id="36b5c-155">`PackageLicenseUrl` kullanım dışıdır.</span><span class="sxs-lookup"><span data-stu-id="36b5c-155">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="36b5c-156">`PackageLicenseExpression` `PackageLicenseFile` Bunun yerine veya kullanın.</span><span class="sxs-lookup"><span data-stu-id="36b5c-156">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| `ProjectUrl` | `PackageProjectUrl` | <span data-ttu-id="36b5c-157">empty</span><span class="sxs-lookup"><span data-stu-id="36b5c-157">empty</span></span> | |
| `Icon` | `PackageIcon` | <span data-ttu-id="36b5c-158">empty</span><span class="sxs-lookup"><span data-stu-id="36b5c-158">empty</span></span> | <span data-ttu-id="36b5c-159">Paket simgesi olarak kullanılacak paketteki bir görüntünün yolu.</span><span class="sxs-lookup"><span data-stu-id="36b5c-159">A path to an image in the package to use as a package icon.</span></span> <span data-ttu-id="36b5c-160">Başvurulan simge görüntü dosyasını açıkça paketetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="36b5c-160">You need to explicitly pack the referenced icon image file.</span></span> <span data-ttu-id="36b5c-161">Daha fazla bilgi için bkz. [paketleme bir simge görüntü dosyası](#packing-an-icon-image-file) ve [ `icon` meta verileri](/nuget/reference/nuspec#icon).</span><span class="sxs-lookup"><span data-stu-id="36b5c-161">For more information, see [Packing an icon image file](#packing-an-icon-image-file) and [`icon` metadata](/nuget/reference/nuspec#icon).</span></span> |
| `IconUrl` | `PackageIconUrl` | <span data-ttu-id="36b5c-162">empty</span><span class="sxs-lookup"><span data-stu-id="36b5c-162">empty</span></span> | <span data-ttu-id="36b5c-163">`PackageIconUrl` kullanım dışı bırakılmıştır `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-163">`PackageIconUrl` is deprecated in favor of `PackageIcon`.</span></span> <span data-ttu-id="36b5c-164">Ancak, en iyi alt düzey deneyim için öğesine ek olarak belirtmeniz gerekir `PackageIconUrl` `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-164">However, for the best downlevel experience, you should specify `PackageIconUrl` in addition to `PackageIcon`.</span></span> |
| `Tags` | `PackageTags` | <span data-ttu-id="36b5c-165">empty</span><span class="sxs-lookup"><span data-stu-id="36b5c-165">empty</span></span> | <span data-ttu-id="36b5c-166">Paketi atayan etiketlerin noktalı virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="36b5c-166">A semicolon-delimited list of tags that designates the package.</span></span> |
| `ReleaseNotes` | `PackageReleaseNotes` | <span data-ttu-id="36b5c-167">empty</span><span class="sxs-lookup"><span data-stu-id="36b5c-167">empty</span></span> | <span data-ttu-id="36b5c-168">Paket için sürüm notları.</span><span class="sxs-lookup"><span data-stu-id="36b5c-168">Release notes for the package.</span></span> |
| `Repository/Url` | `RepositoryUrl` | <span data-ttu-id="36b5c-169">empty</span><span class="sxs-lookup"><span data-stu-id="36b5c-169">empty</span></span> | <span data-ttu-id="36b5c-170">Kaynak kodu kopyalamak veya almak için kullanılan depo URL 'SI.</span><span class="sxs-lookup"><span data-stu-id="36b5c-170">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="36b5c-171">Örnek: *https://github.com/ NuGet / NuGet . Client. git*.</span><span class="sxs-lookup"><span data-stu-id="36b5c-171">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| `Repository/Type` | `RepositoryType` | <span data-ttu-id="36b5c-172">empty</span><span class="sxs-lookup"><span data-stu-id="36b5c-172">empty</span></span> | <span data-ttu-id="36b5c-173">Depo türü.</span><span class="sxs-lookup"><span data-stu-id="36b5c-173">Repository type.</span></span> <span data-ttu-id="36b5c-174">Örnekler: `git` (varsayılan), `tfs` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-174">Examples: `git` (default), `tfs`.</span></span> |
| `Repository/Branch` | `RepositoryBranch` | <span data-ttu-id="36b5c-175">empty</span><span class="sxs-lookup"><span data-stu-id="36b5c-175">empty</span></span> | <span data-ttu-id="36b5c-176">İsteğe bağlı depo dalı bilgileri.</span><span class="sxs-lookup"><span data-stu-id="36b5c-176">Optional repository branch information.</span></span> <span data-ttu-id="36b5c-177">`RepositoryUrl` Bu özelliğin dahil edilmesini sağlamak için de belirtilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="36b5c-177">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="36b5c-178">Örnek: *Master* ( NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="36b5c-178">Example: *master* (NuGet 4.7.0+).</span></span> |
| `Repository/Commit` | `RepositoryCommit` | <span data-ttu-id="36b5c-179">empty</span><span class="sxs-lookup"><span data-stu-id="36b5c-179">empty</span></span> | <span data-ttu-id="36b5c-180">Paketin hangi kaynağa göre oluşturulduğunu göstermek için isteğe bağlı depo kaydı veya değişiklik kümesi.</span><span class="sxs-lookup"><span data-stu-id="36b5c-180">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="36b5c-181">`RepositoryUrl` Bu özelliğin dahil edilmesini sağlamak için de belirtilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="36b5c-181">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="36b5c-182">Örnek: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="36b5c-182">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| `PackageType` | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| `Summary` | <span data-ttu-id="36b5c-183">Desteklenmez</span><span class="sxs-lookup"><span data-stu-id="36b5c-183">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="36b5c-184">Paket hedef girişleri</span><span class="sxs-lookup"><span data-stu-id="36b5c-184">pack target inputs</span></span>

| <span data-ttu-id="36b5c-185">Özellik</span><span class="sxs-lookup"><span data-stu-id="36b5c-185">Property</span></span> | <span data-ttu-id="36b5c-186">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36b5c-186">Description</span></span> |
| - | - |
| `IsPackable` | <span data-ttu-id="36b5c-187">Projenin paketlenemeyeceğini belirten bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="36b5c-187">A Boolean value that specifies whether the project can be packed.</span></span> <span data-ttu-id="36b5c-188">`true` varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="36b5c-188">The default value is `true`.</span></span> |
| `SuppressDependenciesWhenPacking` | <span data-ttu-id="36b5c-189">`true`Oluşturulan paketten paket bağımlılıklarını göstermemek için olarak ayarlayın NuGet .</span><span class="sxs-lookup"><span data-stu-id="36b5c-189">Set to `true` to suppress package dependencies from the generated NuGet package.</span></span> |
| `PackageVersion` | <span data-ttu-id="36b5c-190">Elde edilen paketin sahip olacağı sürümü belirtir.</span><span class="sxs-lookup"><span data-stu-id="36b5c-190">Specifies the version that the resulting package will have.</span></span> <span data-ttu-id="36b5c-191">Tüm sürüm dizesi biçimlerini kabul eder NuGet .</span><span class="sxs-lookup"><span data-stu-id="36b5c-191">Accepts all forms of NuGet version string.</span></span> <span data-ttu-id="36b5c-192">Varsayılan değeri,, `$(Version)` Yani, projedeki özelliğinin değeridir `Version` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-192">Default is the value of `$(Version)`, that is, of the property `Version` in the project.</span></span> |
| `PackageId` | <span data-ttu-id="36b5c-193">Sonuç paketinin adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="36b5c-193">Specifies the name for the resulting package.</span></span> <span data-ttu-id="36b5c-194">Belirtilmemişse, `pack` işlem varsayılan `AssemblyName` olarak paketin adı ile veya dizin adını kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="36b5c-194">If not specified, the `pack` operation will default to using the `AssemblyName` or directory name as the name of the package.</span></span> |
| `PackageDescription` | <span data-ttu-id="36b5c-195">UI görüntüleme paketinin uzun açıklaması.</span><span class="sxs-lookup"><span data-stu-id="36b5c-195">A long description of the package for UI display.</span></span> |
| `Authors` | <span data-ttu-id="36b5c-196">Nuget.org üzerindeki profil adlarıyla eşleşen paket yazarları için noktalı virgülle ayrılmış bir liste. Bunlar, NuGet NuGet.org üzerindeki galeride görüntülenir ve aynı yazarlara göre çapraz başvuru için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="36b5c-196">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| `Description` | <span data-ttu-id="36b5c-197">Derleme için uzun bir açıklama.</span><span class="sxs-lookup"><span data-stu-id="36b5c-197">A long description for the assembly.</span></span> <span data-ttu-id="36b5c-198">`PackageDescription`Belirtilmezse, bu özellik paketin açıklaması olarak da kullanılır.</span><span class="sxs-lookup"><span data-stu-id="36b5c-198">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| `Copyright` | <span data-ttu-id="36b5c-199">Paket için telif hakkı ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="36b5c-199">Copyright details for the package.</span></span> |
| `PackageRequireLicenseAcceptance` | <span data-ttu-id="36b5c-200">İstemcinin paketi yüklemeden önce paket lisansını kabul etmesini isteyip istemeyeceğini belirten bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="36b5c-200">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> <span data-ttu-id="36b5c-201">Varsayılan değer: `false`.</span><span class="sxs-lookup"><span data-stu-id="36b5c-201">The default is `false`.</span></span> |
| `DevelopmentDependency` | <span data-ttu-id="36b5c-202">Paketin bir yalnızca geliştirme bağımlılığı olarak işaretlenip işaretlenmediğini belirten ve paketin diğer paketlere bağımlılık olarak eklenmesini önleyen bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="36b5c-202">A Boolean value that specifies whether the package is marked as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="36b5c-203">`PackageReference`( NuGet 4.8 +) ile bu bayrak, derleme zamanı varlıklarının derlemeden dışlandığı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="36b5c-203">With `PackageReference` (NuGet 4.8+), this flag also means that compile-time assets are excluded from compilation.</span></span> <span data-ttu-id="36b5c-204">Daha fazla bilgi için bkz. [PackageReference Için Developmentdependency desteği](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span><span class="sxs-lookup"><span data-stu-id="36b5c-204">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span> |
| `PackageLicenseExpression` | <span data-ttu-id="36b5c-205">Örneğin, bir [Spdx lisans tanımlayıcısı](https://spdx.org/licenses/) veya ifadesi `Apache-2.0` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-205">An [SPDX license identifier](https://spdx.org/licenses/) or expression, for example, `Apache-2.0`.</span></span> <span data-ttu-id="36b5c-206">Daha fazla bilgi için bkz. [Lisans ifadesi veya lisans dosyası paketleme](#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="36b5c-206">For more information, see [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `PackageLicenseFile` | <span data-ttu-id="36b5c-207">Özel bir lisans veya bir SPDX tanımlayıcısı atanmamış bir lisans kullanıyorsanız paket içindeki bir lisans dosyasının yolu.</span><span class="sxs-lookup"><span data-stu-id="36b5c-207">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> |
| `PackageLicenseUrl` | <span data-ttu-id="36b5c-208">`PackageLicenseUrl` kullanım dışıdır.</span><span class="sxs-lookup"><span data-stu-id="36b5c-208">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="36b5c-209">`PackageLicenseExpression` `PackageLicenseFile` Bunun yerine veya kullanın.</span><span class="sxs-lookup"><span data-stu-id="36b5c-209">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| `PackageProjectUrl` | |
| `PackageIcon` | <span data-ttu-id="36b5c-210">Paketin köküne göre paket simge yolunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="36b5c-210">Specifies the package icon path, relative to the root of the package.</span></span> <span data-ttu-id="36b5c-211">Daha fazla bilgi için bkz. [paketleme a Icon Image File](#packing-an-icon-image-file).</span><span class="sxs-lookup"><span data-stu-id="36b5c-211">For more information, see [Packing an icon image file](#packing-an-icon-image-file).</span></span> |
| `PackageReleaseNotes` | <span data-ttu-id="36b5c-212">Paket için sürüm notları.</span><span class="sxs-lookup"><span data-stu-id="36b5c-212">Release notes for the package.</span></span> |
| `PackageTags` | <span data-ttu-id="36b5c-213">Paketi atayan etiketlerin noktalı virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="36b5c-213">A semicolon-delimited list of tags that designates the package.</span></span> |
| `PackageOutputPath` | <span data-ttu-id="36b5c-214">Paketlenmiş paketin bırakılacak çıkış yolunu belirler.</span><span class="sxs-lookup"><span data-stu-id="36b5c-214">Determines the output path in which the packed package will be dropped.</span></span> <span data-ttu-id="36b5c-215">`$(OutputPath)` varsayılan değerdir.</span><span class="sxs-lookup"><span data-stu-id="36b5c-215">Default is `$(OutputPath)`.</span></span> |
| `IncludeSymbols` | <span data-ttu-id="36b5c-216">Bu Boole değeri, paketin proje paketedildiğinde ek bir sembol paketi oluşturup oluşturmayacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="36b5c-216">This Boolean value indicates whether the package should create an additional symbols package when the project is packed.</span></span> <span data-ttu-id="36b5c-217">Semboller paketinin biçimi, özelliği tarafından denetlenir `SymbolPackageFormat` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-217">The symbols package's format is controlled by the `SymbolPackageFormat` property.</span></span> <span data-ttu-id="36b5c-218">Daha fazla bilgi için bkz. [ıncludesymbols](#includesymbols).</span><span class="sxs-lookup"><span data-stu-id="36b5c-218">For more information, see [IncludeSymbols](#includesymbols).</span></span> |
| `IncludeSource` | <span data-ttu-id="36b5c-219">Bu Boole değeri, paket işleminin bir kaynak paketi oluşturup oluşturmayacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="36b5c-219">This Boolean value indicates whether the pack process should create a source package.</span></span> <span data-ttu-id="36b5c-220">Kaynak paket, kitaplığın kaynak kodunu ve PDB dosyalarını içerir.</span><span class="sxs-lookup"><span data-stu-id="36b5c-220">The source package contains the library's source code as well as PDB files.</span></span> <span data-ttu-id="36b5c-221">Kaynak dosyalar, `src/ProjectName` elde edilen paket dosyasındaki dizinin altına yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="36b5c-221">Source files are put under the `src/ProjectName` directory in the resulting package file.</span></span> <span data-ttu-id="36b5c-222">Daha fazla bilgi için bkz. [ıncludesource](#includesource).</span><span class="sxs-lookup"><span data-stu-id="36b5c-222">For more information, see [IncludeSource](#includesource).</span></span> |
| `PackageType` | |
| `IsTool` | <span data-ttu-id="36b5c-223">Tüm çıkış dosyalarının *lib* klasörü yerine *Araçlar* klasörüne kopyalanıp kopyalanmayacağını belirtir.</span><span class="sxs-lookup"><span data-stu-id="36b5c-223">Specifies whether all output files are copied to the *tools* folder instead of the *lib* folder.</span></span> <span data-ttu-id="36b5c-224">Daha fazla bilgi için bkz. [ISTool](#istool).</span><span class="sxs-lookup"><span data-stu-id="36b5c-224">For more information, see [IsTool](#istool).</span></span> |
| `RepositoryUrl` | <span data-ttu-id="36b5c-225">Kaynak kodu kopyalamak veya almak için kullanılan depo URL 'SI.</span><span class="sxs-lookup"><span data-stu-id="36b5c-225">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="36b5c-226">Örnek: *https://github.com/ NuGet / NuGet . Client. git*.</span><span class="sxs-lookup"><span data-stu-id="36b5c-226">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| `RepositoryType` | <span data-ttu-id="36b5c-227">Depo türü.</span><span class="sxs-lookup"><span data-stu-id="36b5c-227">Repository type.</span></span> <span data-ttu-id="36b5c-228">Örnekler: `git` (varsayılan), `tfs` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-228">Examples: `git` (default), `tfs`.</span></span> |
| `RepositoryBranch` | <span data-ttu-id="36b5c-229">İsteğe bağlı depo dalı bilgileri.</span><span class="sxs-lookup"><span data-stu-id="36b5c-229">Optional repository branch information.</span></span> <span data-ttu-id="36b5c-230">`RepositoryUrl` Bu özelliğin dahil edilmesini sağlamak için de belirtilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="36b5c-230">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="36b5c-231">Örnek: *Master* ( NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="36b5c-231">Example: *master* (NuGet 4.7.0+).</span></span> |
| `RepositoryCommit` | <span data-ttu-id="36b5c-232">Paketin hangi kaynağa göre oluşturulduğunu göstermek için isteğe bağlı depo kaydı veya değişiklik kümesi.</span><span class="sxs-lookup"><span data-stu-id="36b5c-232">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="36b5c-233">`RepositoryUrl` Bu özelliğin dahil edilmesini sağlamak için de belirtilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="36b5c-233">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="36b5c-234">Örnek: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="36b5c-234">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| `SymbolPackageFormat` | <span data-ttu-id="36b5c-235">Semboller paketinin biçimini belirtir.</span><span class="sxs-lookup"><span data-stu-id="36b5c-235">Specifies the format of the symbols package.</span></span> <span data-ttu-id="36b5c-236">"Symbols. nupkg" ise, pdb 'leri, dll 'Ler ve diğer çıktı dosyalarını içeren *. Symbols. nupkg* Uzantısı ile eski bir sembol paketi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="36b5c-236">If "symbols.nupkg", a legacy symbols package is created with a *.symbols.nupkg* extension containing PDBs, DLLs, and other output files.</span></span> <span data-ttu-id="36b5c-237">"Snupkg" ise, taşınabilir pdb 'leri içeren bir snupkg sembol paketi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="36b5c-237">If "snupkg", a snupkg symbol package is created containing the portable PDBs.</span></span> <span data-ttu-id="36b5c-238">Varsayılan değer "symbols. nupkg" dır.</span><span class="sxs-lookup"><span data-stu-id="36b5c-238">The default is "symbols.nupkg".</span></span> |
| `NoPackageAnalysis` | <span data-ttu-id="36b5c-239">`pack`Paketi derlemeden sonra paket analizini çalıştırmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="36b5c-239">Specifies that `pack` should not run package analysis after building the package.</span></span> |
| `MinClientVersion` | <span data-ttu-id="36b5c-240">NuGetnuget.exe ve Visual Studio Paket Yöneticisi tarafından zorlanan bu paketi yükleyesağlayan istemcinin en düşük sürümünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="36b5c-240">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> |
| `IncludeBuildOutput` | <span data-ttu-id="36b5c-241">Bu Boole değeri, derleme çıkış derlemelerinin *. nupkg* dosyasına paketedilip edilmeyeceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="36b5c-241">This Boolean value specifies whether the build output assemblies should be packed into the *.nupkg* file or not.</span></span> |
| `IncludeContentInPack` | <span data-ttu-id="36b5c-242">Bu Boole değeri, türü olan herhangi bir öğenin `Content` elde edilen pakete otomatik olarak dahil edilip edilmeyeceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="36b5c-242">This Boolean value specifies whether any items that have a type of `Content` are included in the resulting package automatically.</span></span> <span data-ttu-id="36b5c-243">Varsayılan değer: `true`.</span><span class="sxs-lookup"><span data-stu-id="36b5c-243">The default is `true`.</span></span> |
| `BuildOutputTargetFolder` | <span data-ttu-id="36b5c-244">Çıkış derlemelerinin yerleştirileceği klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="36b5c-244">Specifies the folder where to place the output assemblies.</span></span> <span data-ttu-id="36b5c-245">Çıkış derlemeleri (ve diğer çıkış dosyaları) ilgili çerçeve klasörlerine kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="36b5c-245">The output assemblies (and other output files) are copied into their respective framework folders.</span></span> <span data-ttu-id="36b5c-246">Daha fazla bilgi için bkz. [Çıkış derlemeleri](#output-assemblies).</span><span class="sxs-lookup"><span data-stu-id="36b5c-246">For more information, see [Output assemblies](#output-assemblies).</span></span> |
| `ContentTargetFolders` | <span data-ttu-id="36b5c-247">Kendileri için belirtilmemişse, tüm içerik dosyalarının gitmesi gereken varsayılan konumu belirtir `PackagePath` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-247">Specifies the default location of where all the content files should go if `PackagePath` is not specified for them.</span></span> <span data-ttu-id="36b5c-248">Varsayılan değer "Content; contentFiles" dır.</span><span class="sxs-lookup"><span data-stu-id="36b5c-248">The default value is "content;contentFiles".</span></span> <span data-ttu-id="36b5c-249">Daha fazla bilgi için bkz. [bir paketteki Içerik ekleme](#including-content-in-a-package).</span><span class="sxs-lookup"><span data-stu-id="36b5c-249">For more information, see [Including content in a package](#including-content-in-a-package).</span></span> |
| `NuspecFile` | <span data-ttu-id="36b5c-250">*.nuspec* Paketleme için kullanılan dosyanın göreli veya mutlak yolu.</span><span class="sxs-lookup"><span data-stu-id="36b5c-250">Relative or absolute path to the *.nuspec* file being used for packing.</span></span> <span data-ttu-id="36b5c-251">Belirtilmişse, **yalnızca** paketleme bilgileri için kullanılır ve projelerdeki tüm bilgiler kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="36b5c-251">If specified, it's used **exclusively** for packaging information, and any information in the projects is not used.</span></span> <span data-ttu-id="36b5c-252">Daha fazla bilgi için bkz. [Using a .nuspec paketleme ](#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="36b5c-252">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |
| `NuspecBasePath` | <span data-ttu-id="36b5c-253">Dosya için temel yol *.nuspec* .</span><span class="sxs-lookup"><span data-stu-id="36b5c-253">Base path for the *.nuspec* file.</span></span> <span data-ttu-id="36b5c-254">Daha fazla bilgi için bkz. [Using a .nuspec paketleme ](#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="36b5c-254">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |
| `NuspecProperties` | <span data-ttu-id="36b5c-255">Anahtar = değer çiftlerinin noktalı virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="36b5c-255">Semicolon separated list of key=value pairs.</span></span> <span data-ttu-id="36b5c-256">Daha fazla bilgi için bkz. [Using a .nuspec paketleme ](#packing-using-a-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="36b5c-256">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |

## <a name="pack-scenarios"></a><span data-ttu-id="36b5c-257">paket senaryoları</span><span class="sxs-lookup"><span data-stu-id="36b5c-257">pack scenarios</span></span>

### <a name="suppressing-dependencies"></a><span data-ttu-id="36b5c-258">Gizleme bağımlılıkları</span><span class="sxs-lookup"><span data-stu-id="36b5c-258">Suppressing dependencies</span></span>

<span data-ttu-id="36b5c-259">Oluşturulan paketten paket bağımlılıklarını bastırmak için NuGet , olarak ayarlayın `SuppressDependenciesWhenPacking` ve `true` oluşturulan nupkg dosyasından tüm bağımlılıkların atlanmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="36b5c-259">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### `PackageIconUrl`

<span data-ttu-id="36b5c-260">`PackageIconUrl` özelliği kullanım dışı bırakılmıştır [`PackageIcon`](#packageicon) .</span><span class="sxs-lookup"><span data-stu-id="36b5c-260">`PackageIconUrl` is deprecated in favor of the [`PackageIcon`](#packageicon) property.</span></span> <span data-ttu-id="36b5c-261">NuGet5,3 ve Visual Studio 2019 sürüm 16,3 ' den başlayarak, `pack` paket meta verileri yalnızca belirtiyorsa [NU5048](./errors-and-warnings/nu5048.md) uyarı oluşturur `PackageIconUrl` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-261">Starting with NuGet 5.3 and Visual Studio 2019 version 16.3, `pack` raises the [NU5048](./errors-and-warnings/nu5048.md) warning if the package metadata only specifies `PackageIconUrl`.</span></span>

### `PackageIcon`

> [!Tip]
> <span data-ttu-id="36b5c-262">Henüz desteklemeyen istemcilerle ve kaynaklarla geriye dönük uyumluluk sağlamak için hem hem `PackageIcon` de belirtin `PackageIcon` `PackageIconUrl` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-262">To maintain backward compatibility with clients and sources that don't yet support `PackageIcon`, specify both `PackageIcon` and `PackageIconUrl`.</span></span> <span data-ttu-id="36b5c-263">Visual Studio, `PackageIcon` Klasör tabanlı bir kaynaktan gelen paketler için destekler.</span><span class="sxs-lookup"><span data-stu-id="36b5c-263">Visual Studio supports `PackageIcon` for packages coming from a folder-based source.</span></span>

#### <a name="packing-an-icon-image-file"></a><span data-ttu-id="36b5c-264">Simge görüntüsü dosyası paketleme</span><span class="sxs-lookup"><span data-stu-id="36b5c-264">Packing an icon image file</span></span>

<span data-ttu-id="36b5c-265">Bir simge görüntü dosyası paketleme sırasında, `PackageIcon` paketin köküne göre simge dosya yolunu belirtmek için özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="36b5c-265">When packing an icon image file, use `PackageIcon` property to specify the icon file path, relative to the root of the package.</span></span> <span data-ttu-id="36b5c-266">Ayrıca, dosyanın pakete eklendiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="36b5c-266">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="36b5c-267">Görüntü dosyası boyutu 1 MB ile sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="36b5c-267">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="36b5c-268">Desteklenen dosya biçimleri JPEG ve PNG içerir.</span><span class="sxs-lookup"><span data-stu-id="36b5c-268">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="36b5c-269">128x128 görüntü çözümlemesi yapmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="36b5c-269">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="36b5c-270">Örnek:</span><span class="sxs-lookup"><span data-stu-id="36b5c-270">For example:</span></span>

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

<span data-ttu-id="36b5c-271">[Paket simgesi örneği](https://github.com/NuGet/Samples/tree/main/PackageIconExample).</span><span class="sxs-lookup"><span data-stu-id="36b5c-271">[Package Icon sample](https://github.com/NuGet/Samples/tree/main/PackageIconExample).</span></span>

<span data-ttu-id="36b5c-272">nuspecEşdeğer bir deyişle, [ nuspec simgeye yönelik başvuruya](nuspec.md#icon)göz atın.</span><span class="sxs-lookup"><span data-stu-id="36b5c-272">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="36b5c-273">Çıkış derlemeleri</span><span class="sxs-lookup"><span data-stu-id="36b5c-273">Output assemblies</span></span>

<span data-ttu-id="36b5c-274">`nuget pack` çıktı dosyalarını,,,, ve uzantılarına kopyalar `.exe` `.dll` `.xml` `.winmd` `.json` `.pri` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-274">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="36b5c-275">Kopyalanan çıkış dosyaları MSBuild hedeften neler sundığına bağlıdır `BuiltOutputProjectGroup` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-275">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="36b5c-276">MSBuildÇıktı derlemelerinin nerede olduğunu denetlemek için, proje dosyanızda veya komut satırında kullanabileceğiniz iki özellik vardır:</span><span class="sxs-lookup"><span data-stu-id="36b5c-276">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="36b5c-277">`IncludeBuildOutput`: Derleme çıkış derlemelerinin pakete dahil edilip edilmeyeceğini belirleyen bir Boole değeri.</span><span class="sxs-lookup"><span data-stu-id="36b5c-277">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="36b5c-278">`BuildOutputTargetFolder`: Çıkış derlemelerinin yerleştirilmesi gereken klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="36b5c-278">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="36b5c-279">Çıkış derlemeleri (ve diğer çıkış dosyaları) ilgili çerçeve klasörlerine kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="36b5c-279">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="36b5c-280">Paket başvuruları</span><span class="sxs-lookup"><span data-stu-id="36b5c-280">Package references</span></span>

<span data-ttu-id="36b5c-281">Bkz. [Proje dosyalarındaki paket başvuruları](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="36b5c-281">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="36b5c-282">Projeden projeye başvurular</span><span class="sxs-lookup"><span data-stu-id="36b5c-282">Project to project references</span></span>

<span data-ttu-id="36b5c-283">Proje başvurularına proje başvuruları, paket başvuruları olarak varsayılan olarak kabul edilir NuGet .</span><span class="sxs-lookup"><span data-stu-id="36b5c-283">Project to project references are considered by default as NuGet package references.</span></span> <span data-ttu-id="36b5c-284">Örnek:</span><span class="sxs-lookup"><span data-stu-id="36b5c-284">For example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="36b5c-285">Ayrıca, proje başvurunuz için aşağıdaki meta verileri de ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="36b5c-285">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="36b5c-286">Bir paketteki içerik ekleme</span><span class="sxs-lookup"><span data-stu-id="36b5c-286">Including content in a package</span></span>

<span data-ttu-id="36b5c-287">İçerik eklemek için var olan öğeye ek meta veriler ekleyin `<Content>` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-287">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="36b5c-288">Varsayılan olarak, aşağıdaki gibi girdilerle geçersiz kılmadığınız müddetçe "Içerik" türünde her şey pakete dahil edilir:</span><span class="sxs-lookup"><span data-stu-id="36b5c-288">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="36b5c-289">Varsayılan olarak, her şey `content` `contentFiles\any\<target_framework>` bir paket içindeki ve klasörünün köküne eklenir ve bir paket yolu belirtmediğiniz takdirde göreli klasör yapısını korur:</span><span class="sxs-lookup"><span data-stu-id="36b5c-289">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="36b5c-290">Tüm içeriğinizi yalnızca belirli bir kök klasöre ( `content` ve her ikisi yerine) kopyalamak istiyorsanız, `contentFiles` Varsayılan olarak MSBuild `ContentTargetFolders` "Content; ContentFiles" olarak ayarlanmış ancak başka bir klasör adına ayarlanabilir özelliğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="36b5c-290">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="36b5c-291">Yalnızca `ContentTargetFolders` dosyaları ' ın altında `contentFiles\any\<target_framework>` veya `contentFiles\<language>\<target_framework>` temel alarak "ContentFiles" seçeneğinin belirtildiğine unutmayın `buildAction` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-291">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="36b5c-292">`PackagePath` noktalı virgülle ayrılmış bir hedef yolları kümesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="36b5c-292">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="36b5c-293">Boş bir paket yolu belirtilmesi, dosyayı paketin köküne ekler.</span><span class="sxs-lookup"><span data-stu-id="36b5c-293">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="36b5c-294">Örneğin, aşağıdaki, `libuv.txt` `content\myfiles` `content\samples` ve paket köküne ekler:</span><span class="sxs-lookup"><span data-stu-id="36b5c-294">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="36b5c-295">Ayrıca MSBuild `$(IncludeContentInPack)` , varsayılan olarak olan bir özellik vardır `true` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-295">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="36b5c-296">Bu, `false` herhangi bir projede olarak ayarlandıysa, bu projeden içerik NuGet paketine dahil edilmez.</span><span class="sxs-lookup"><span data-stu-id="36b5c-296">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="36b5c-297">Yukarıdaki öğelerin herhangi birine ayarlayabileceğiniz diğer paketine özgü meta veriler de dahil olmak üzere ```<PackageCopyToOutput>``` ```<PackageFlatten>``` ```CopyToOutput``` ```Flatten``` ```contentFiles``` , çıktı içindeki giriş ve değer değerlerini içerir nuspec .</span><span class="sxs-lookup"><span data-stu-id="36b5c-297">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="36b5c-298">Içerik öğelerinden ayrı olarak, `<Pack>` ve `<PackagePath>` meta veriler de derleme, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, Designdata, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, Paketleresource veya None derleme eylemine sahip dosyalar üzerinde de ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="36b5c-298">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="36b5c-299">Glob desenleri kullanılırken dosya adını paket yolunuza eklemek için paket yolu, klasör ayırıcı karakteriyle bitmelidir; Aksi takdirde, paket yolu dosya adı dahil tam yol olarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="36b5c-299">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="36b5c-300">Includesymbols</span><span class="sxs-lookup"><span data-stu-id="36b5c-300">IncludeSymbols</span></span>

<span data-ttu-id="36b5c-301">Kullanırken `MSBuild -t:pack -p:IncludeSymbols=true` , karşılık gelen `.pdb` dosyalar diğer çıkış dosyalarıyla birlikte kopyalanır ( `.dll` ,,, `.exe` `.winmd` `.xml` , `.json` , `.pri` ).</span><span class="sxs-lookup"><span data-stu-id="36b5c-301">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="36b5c-302">Ayarın `IncludeSymbols=true` düzenli bir paket *ve* bir semboller paketi oluşturduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="36b5c-302">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="36b5c-303">Includesource</span><span class="sxs-lookup"><span data-stu-id="36b5c-303">IncludeSource</span></span>

<span data-ttu-id="36b5c-304">Bu, `IncludeSymbols` ile aynıdır, ancak kaynak dosyalarını da dosyalarla birlikte kopyalar `.pdb` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-304">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="36b5c-305">Tüm dosya türleri, `Compile` `src\<ProjectName>\` elde edilen paketteki göreli yol klasörü yapısını korumak için üzerine kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="36b5c-305">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="36b5c-306">Aynı zamanda, olarak ayarlanmış herhangi bir kaynak dosyası için de aynı olur `ProjectReference` `TreatAsPackageReference` `false` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-306">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="36b5c-307">Derleme türü bir dosya proje klasörünün dışında ise, ' ye eklenmiştir `src\<ProjectName>\` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-307">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="36b5c-308">Lisans ifadesi veya lisans dosyası paketleme</span><span class="sxs-lookup"><span data-stu-id="36b5c-308">Packing a license expression or a license file</span></span>

<span data-ttu-id="36b5c-309">Bir lisans ifadesi kullanırken, `PackageLicenseExpression` özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="36b5c-309">When using a license expression, use the `PackageLicenseExpression` property.</span></span> <span data-ttu-id="36b5c-310">Bir örnek için bkz. [Lisans ifadesi örneği](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample).</span><span class="sxs-lookup"><span data-stu-id="36b5c-310">For a sample, see [License expression sample](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="36b5c-311">Lisans ifadeleri ve. org tarafından kabul edilen lisanslar hakkında daha fazla bilgi edinmek için NuGet bkz. [Lisans meta verileri](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="36b5c-311">To learn more about license expressions and licenses that are accepted by NuGet.org, see [license metadata](nuspec.md#license).</span></span>

<span data-ttu-id="36b5c-312">Bir lisans dosyası paketleme sırasında, paketin `PackageLicenseFile` köküne göre paket yolunu belirtmek için özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="36b5c-312">When packing a license file, use `PackageLicenseFile` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="36b5c-313">Ayrıca, dosyanın pakete eklendiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="36b5c-313">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="36b5c-314">Örnek:</span><span class="sxs-lookup"><span data-stu-id="36b5c-314">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="36b5c-315">Bir örnek için bkz. [Lisans dosyası örneği](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="36b5c-315">For a sample, see [License file sample](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample).</span></span>

> [!NOTE]
> <span data-ttu-id="36b5c-316">Tek seferde,, ve yalnızca biri `PackageLicenseExpression` `PackageLicenseFile` `PackageLicenseUrl` belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="36b5c-316">Only one of `PackageLicenseExpression`, `PackageLicenseFile`, and `PackageLicenseUrl` can be specified at a time.</span></span>

### <a name="packing-a-file-without-an-extension"></a><span data-ttu-id="36b5c-317">Uzantı olmadan dosya paketleme</span><span class="sxs-lookup"><span data-stu-id="36b5c-317">Packing a file without an extension</span></span>

<span data-ttu-id="36b5c-318">Bir lisans dosyası paketleme gibi bazı senaryolarda, uzantısı olmayan bir dosya eklemek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="36b5c-318">In some scenarios, like when packing a license file, you might want to include a file without an extension.</span></span>
<span data-ttu-id="36b5c-319">Geçmiş nedenlerle, NuGet  &  MSBuild bir uzantısı olmayan yolları dizin olarak değerlendirin.</span><span class="sxs-lookup"><span data-stu-id="36b5c-319">For historical reasons, NuGet & MSBuild treat paths without an extension as directories.</span></span>

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

<span data-ttu-id="36b5c-320">[Dosya uzantı örneği olmadan](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/).</span><span class="sxs-lookup"><span data-stu-id="36b5c-320">[File without an extension sample](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/).</span></span>

### <a name="istool"></a><span data-ttu-id="36b5c-321">IsTool</span><span class="sxs-lookup"><span data-stu-id="36b5c-321">IsTool</span></span>

<span data-ttu-id="36b5c-322">Kullanırken `MSBuild -t:pack -p:IsTool=true` , [Çıkış derlemeleri](#output-assemblies) senaryosunda belirtilen tüm çıkış dosyaları, `tools` klasörü yerine klasörüne kopyalanır `lib` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-322">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="36b5c-323">Bunun, `DotNetCliTool` içindeki dosyasını ayarlayarak belirtilen öğesinden farklı olduğunu unutmayın `PackageType` `.csproj` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-323">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec-file"></a><span data-ttu-id="36b5c-324">Dosya kullanarak paketleme `.nuspec`</span><span class="sxs-lookup"><span data-stu-id="36b5c-324">Packing using a `.nuspec` file</span></span>

<span data-ttu-id="36b5c-325">Bunun yerine genellikle proje dosyasındaki dosyada bulunan [tüm özellikleri eklemeniz](../reference/msbuild-targets.md#pack-target) önerilse de `.nuspec` , `.nuspec` projenizi paketlebilmeniz için bir dosya kullanmayı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="36b5c-325">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="36b5c-326">Tarafından kullanılan SDK olmayan bir proje için `PackageReference` , paket görevinin yürütülebilmesi için içeri aktarmanız gerekir `NuGet.Build.Tasks.Pack.targets` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-326">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="36b5c-327">Bir dosyayı paketetmeden önce projeyi geri yüklemeniz gerekir nuspec .</span><span class="sxs-lookup"><span data-stu-id="36b5c-327">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="36b5c-328">(SDK stili bir proje varsayılan olarak paket hedeflerini içerir.)</span><span class="sxs-lookup"><span data-stu-id="36b5c-328">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="36b5c-329">Proje dosyasının hedef çerçevesi ilgisizdir ve bir paketleme sırasında kullanılmaz nuspec .</span><span class="sxs-lookup"><span data-stu-id="36b5c-329">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="36b5c-330">Aşağıdaki üç MSBuild özellik, ile paketleme için geçerlidir `.nuspec` :</span><span class="sxs-lookup"><span data-stu-id="36b5c-330">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="36b5c-331">`NuspecFile`: `.nuspec` paketleme için kullanılan dosyanın göreli veya mutlak yolu.</span><span class="sxs-lookup"><span data-stu-id="36b5c-331">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="36b5c-332">`NuspecProperties`: Key = değer çiftleri için noktalı virgülle ayrılmış bir liste.</span><span class="sxs-lookup"><span data-stu-id="36b5c-332">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="36b5c-333">MSBuildKomut satırı ayrıştırması çalışma yöntemi nedeniyle, birden çok özellik şu şekilde belirtilmelidir: `-p:NuspecProperties="key1=value1;key2=value2"` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-333">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties="key1=value1;key2=value2"`.</span></span>  
1. <span data-ttu-id="36b5c-334">`NuspecBasePath`: Dosyanın temel yolu `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-334">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="36b5c-335">`dotnet.exe`Projenizi paketmek için kullanıyorsanız, aşağıdaki gibi bir komut kullanın:</span><span class="sxs-lookup"><span data-stu-id="36b5c-335">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="36b5c-336">MSBuildProjenizi paketmek için kullanıyorsanız, aşağıdaki gibi bir komut kullanın:</span><span class="sxs-lookup"><span data-stu-id="36b5c-336">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="36b5c-337">nuspecdotnet.exe veya MSBuild kullanan paketleme, projenin varsayılan olarak oluşturulmasına da neden olduğuna emin olun.</span><span class="sxs-lookup"><span data-stu-id="36b5c-337">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="36b5c-338">Bu, proje dosyanızdaki ```--no-build``` ```<NoBuild>true</NoBuild> ``` ayar ile birlikte proje dosyanızdaki ayarın eşdeğeri olan dotnet.exe özelliği ' a geçirerek kaçınılabilir ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-338">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="36b5c-339">Bir dosyayı paketetmek için *. csproj* dosyası örneği nuspec :</span><span class="sxs-lookup"><span data-stu-id="36b5c-339">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="36b5c-340">Özelleştirilmiş paket oluşturmak için gelişmiş uzantı noktaları</span><span class="sxs-lookup"><span data-stu-id="36b5c-340">Advanced extension points to create customized package</span></span>

<span data-ttu-id="36b5c-341">`pack`Hedef, iç, hedef çerçeveye özgü derlemede çalışan iki uzantı noktası sağlar.</span><span class="sxs-lookup"><span data-stu-id="36b5c-341">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="36b5c-342">Uzantı noktaları, hedef çerçeveye özgü içerik ve derlemelerin bir pakete dahil edilmesi için destek:</span><span class="sxs-lookup"><span data-stu-id="36b5c-342">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="36b5c-343">`TargetsForTfmSpecificBuildOutput` target: klasör içindeki dosyaları `lib` veya kullanılarak belirtilen klasörü kullanın `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-343">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="36b5c-344">`TargetsForTfmSpecificContentInPackage` target: dışındaki dosyalar için kullanın `BuildOutputTargetFolder` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-344">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### `TargetsForTfmSpecificBuildOutput`

<span data-ttu-id="36b5c-345">Özel bir hedef yazın ve özelliğin değeri olarak belirtin `$(TargetsForTfmSpecificBuildOutput)` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-345">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="36b5c-346">(Varsayılan olarak LIB) öğesine gitmesi gereken tüm dosyalar için `BuildOutputTargetFolder` , hedef bu dosyaları ItemGroup 'a yazmalıdır `BuildOutputInPackage` ve aşağıdaki iki meta veri değerini ayarlamış olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="36b5c-346">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="36b5c-347">`FinalOutputPath`: Dosyanın mutlak yolu; sağlanmazsa, kimlik kaynak yolunu değerlendirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="36b5c-347">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="36b5c-348">`TargetPath`: (İsteğe bağlı) dosyanın içindeki bir alt klasöre gitmesi gerektiğinde ayarlanır `lib\<TargetFramework>` . Bu, ilgili kültür klasörlerinin altına giten uydu derlemeleri gibi.</span><span class="sxs-lookup"><span data-stu-id="36b5c-348">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="36b5c-349">Varsayılan olarak dosyanın adıdır.</span><span class="sxs-lookup"><span data-stu-id="36b5c-349">Defaults to the name of the file.</span></span>

<span data-ttu-id="36b5c-350">Örnek:</span><span class="sxs-lookup"><span data-stu-id="36b5c-350">Example:</span></span>

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

<span data-ttu-id="36b5c-351">Özel bir hedef yazın ve özelliğin değeri olarak belirtin `$(TargetsForTfmSpecificContentInPackage)` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-351">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="36b5c-352">Pakete dahil edilecek tüm dosyalar için, hedef bu dosyaları ItemGroup 'a yazmalıdır `TfmSpecificPackageFile` ve aşağıdaki isteğe bağlı meta verileri ayarlar:</span><span class="sxs-lookup"><span data-stu-id="36b5c-352">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="36b5c-353">`PackagePath`: Dosyanın pakette çıkış olması gereken yol.</span><span class="sxs-lookup"><span data-stu-id="36b5c-353">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="36b5c-354">NuGet aynı paket yoluna birden fazla dosya eklenirse bir uyarı verir.</span><span class="sxs-lookup"><span data-stu-id="36b5c-354">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="36b5c-355">`BuildAction`: Dosyaya atanacak derleme eylemi, yalnızca paket yolu `contentFiles` klasörsise gereklidir.</span><span class="sxs-lookup"><span data-stu-id="36b5c-355">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="36b5c-356">Varsayılan "none" olarak belirlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="36b5c-356">Defaults to "None".</span></span>

<span data-ttu-id="36b5c-357">Örnek:</span><span class="sxs-lookup"><span data-stu-id="36b5c-357">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="36b5c-358">hedefi geri yükle</span><span class="sxs-lookup"><span data-stu-id="36b5c-358">restore target</span></span>

<span data-ttu-id="36b5c-359">`MSBuild -t:restore` ( `nuget restore` `dotnet restore` .NET Core projeleriyle birlikte kullanılması), proje dosyasında başvurulan paketleri aşağıdaki şekilde geri yükler:</span><span class="sxs-lookup"><span data-stu-id="36b5c-359">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="36b5c-360">Proje başvurularına tüm projeyi oku</span><span class="sxs-lookup"><span data-stu-id="36b5c-360">Read all project to project references</span></span>
1. <span data-ttu-id="36b5c-361">Ara klasörünü ve hedef çerçeveleri bulmak için proje özelliklerini okuyun</span><span class="sxs-lookup"><span data-stu-id="36b5c-361">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="36b5c-362">MSBuild.Build.Tasks.dll verileri geçirme NuGet</span><span class="sxs-lookup"><span data-stu-id="36b5c-362">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="36b5c-363">Geri yüklemeyi Çalıştır</span><span class="sxs-lookup"><span data-stu-id="36b5c-363">Run restore</span></span>
1. <span data-ttu-id="36b5c-364">Paketleri İndir</span><span class="sxs-lookup"><span data-stu-id="36b5c-364">Download packages</span></span>
1. <span data-ttu-id="36b5c-365">Varlıklar dosyası, hedefler ve props yazma</span><span class="sxs-lookup"><span data-stu-id="36b5c-365">Write assets file, targets, and props</span></span>

<span data-ttu-id="36b5c-366">`restore`Hedef, PackageReference biçimini kullanan projeler için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="36b5c-366">The `restore` target works for projects using the PackageReference format.</span></span>
<span data-ttu-id="36b5c-367">`MSBuild 16.5+` Ayrıca, biçim için [kabul desteği](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) de vardır `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-367">`MSBuild 16.5+` also has [opt-in support](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) for the `packages.config` format.</span></span>

> [!NOTE]
> <span data-ttu-id="36b5c-368">`restore`Hedef, hedefle birlikte [çalıştırılmamalıdır](#restoring-and-building-with-one-msbuild-command) `build` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-368">The `restore` target [should not be run](#restoring-and-building-with-one-msbuild-command) in combination with the `build` target.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="36b5c-369">Özellikleri geri yükle</span><span class="sxs-lookup"><span data-stu-id="36b5c-369">Restore properties</span></span>

<span data-ttu-id="36b5c-370">Ek geri yükleme ayarları MSBuild Proje dosyasındaki özelliklerden gelebilir.</span><span class="sxs-lookup"><span data-stu-id="36b5c-370">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="36b5c-371">Değerler, anahtar kullanılarak komut satırından da ayarlanabilir `-p:` (aşağıdaki örneklere bakın).</span><span class="sxs-lookup"><span data-stu-id="36b5c-371">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="36b5c-372">Özellik</span><span class="sxs-lookup"><span data-stu-id="36b5c-372">Property</span></span> | <span data-ttu-id="36b5c-373">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36b5c-373">Description</span></span> |
|--------|--------|
| `RestoreSources` | <span data-ttu-id="36b5c-374">Paket kaynaklarının noktalı virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="36b5c-374">Semicolon-delimited list of package sources.</span></span> |
| `RestorePackagesPath` | <span data-ttu-id="36b5c-375">Kullanıcı paketleri klasör yolu.</span><span class="sxs-lookup"><span data-stu-id="36b5c-375">User packages folder path.</span></span> |
| `RestoreDisableParallel` | <span data-ttu-id="36b5c-376">İndirmeleri tek seferde bir ile sınırlayın.</span><span class="sxs-lookup"><span data-stu-id="36b5c-376">Limit downloads to one at a time.</span></span> |
| `RestoreConfigFile` | <span data-ttu-id="36b5c-377">`Nuget.Config`Uygulanacak dosyanın yolu.</span><span class="sxs-lookup"><span data-stu-id="36b5c-377">Path to a `Nuget.Config` file to apply.</span></span> |
| `RestoreNoCache` | <span data-ttu-id="36b5c-378">Doğru ise, önbelleğe alınmış paketlerin kullanılmasını önler.</span><span class="sxs-lookup"><span data-stu-id="36b5c-378">If true, avoids using cached packages.</span></span> <span data-ttu-id="36b5c-379">Bkz. [genel paketleri ve önbellek klasörlerini yönetme](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="36b5c-379">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| `RestoreIgnoreFailedSources` | <span data-ttu-id="36b5c-380">Doğru ise, başarısız veya eksik paket kaynaklarını yoksayar.</span><span class="sxs-lookup"><span data-stu-id="36b5c-380">If true, ignores failing or missing package sources.</span></span> |
| `RestoreFallbackFolders` | <span data-ttu-id="36b5c-381">Geri dönüş klasörleri, Kullanıcı paketleri klasörüyle aynı şekilde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="36b5c-381">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| `RestoreAdditionalProjectSources` | <span data-ttu-id="36b5c-382">Geri yükleme sırasında kullanılacak ek kaynaklar.</span><span class="sxs-lookup"><span data-stu-id="36b5c-382">Additional sources to use during restore.</span></span> |
| `RestoreAdditionalProjectFallbackFolders` | <span data-ttu-id="36b5c-383">Geri yükleme sırasında kullanılacak ek geri dönüş klasörleri.</span><span class="sxs-lookup"><span data-stu-id="36b5c-383">Additional fallback folders to use during restore.</span></span> |
| `RestoreAdditionalProjectFallbackFoldersExcludes` | <span data-ttu-id="36b5c-384">İçinde belirtilen geri dönüş klasörlerini dışlar `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="36b5c-384">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| `RestoreTaskAssemblyFile` | <span data-ttu-id="36b5c-385">Yolu `NuGet.Build.Tasks.dll` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-385">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| `RestoreGraphProjectInput` | <span data-ttu-id="36b5c-386">Geri yüklenecek projelerin, mutlak yollar içermesi gereken, noktalı virgülle ayrılmış listesi.</span><span class="sxs-lookup"><span data-stu-id="36b5c-386">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| `RestoreUseSkipNonexistentTargets`  | <span data-ttu-id="36b5c-387">Projeler aracılığıyla toplandığında, MSBuild iyileştirme kullanılarak toplanıp toplanmayacağını belirler `SkipNonexistentTargets` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-387">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="36b5c-388">Ayarlanmazsa, varsayılan olarak olur `true` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-388">When not set, defaults to `true`.</span></span> <span data-ttu-id="36b5c-389">Projenin hedefleri içeri aktarılmadığı zaman, sonuç hızlı bir davranıştır.</span><span class="sxs-lookup"><span data-stu-id="36b5c-389">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| `MSBuildProjectExtensionsPath` | <span data-ttu-id="36b5c-390">Çıkış klasörü, varsayılan olarak `BaseIntermediateOutputPath` ve `obj` klasörü.</span><span class="sxs-lookup"><span data-stu-id="36b5c-390">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| `RestoreForce` | <span data-ttu-id="36b5c-391">PackageReference tabanlı projelerde, son geri yükleme başarılı olsa bile tüm bağımlılıkların çözülmesini zorlar.</span><span class="sxs-lookup"><span data-stu-id="36b5c-391">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="36b5c-392">Bu bayrağın belirtilmesi, dosyanın silinmesine benzer `project.assets.json` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-392">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="36b5c-393">Bu, http-cache ' i atlar.</span><span class="sxs-lookup"><span data-stu-id="36b5c-393">This does not bypass the http-cache.</span></span> |
| `RestorePackagesWithLockFile` | <span data-ttu-id="36b5c-394">Bir kilit dosyasının kullanımıyla ilgili olarak.</span><span class="sxs-lookup"><span data-stu-id="36b5c-394">Opts into the usage of a lock file.</span></span> |
| `RestoreLockedMode` | <span data-ttu-id="36b5c-395">Geri yüklemeyi kilitli modda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="36b5c-395">Run restore in locked mode.</span></span> <span data-ttu-id="36b5c-396">Bu, geri yüklemenin bağımlılıkları yeniden değerlendirmeyeceği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="36b5c-396">This means that restore will not reevaluate the dependencies.</span></span> |
| `NuGetLockFilePath` | <span data-ttu-id="36b5c-397">Kilit dosyası için özel bir konum.</span><span class="sxs-lookup"><span data-stu-id="36b5c-397">A custom location for the lock file.</span></span> <span data-ttu-id="36b5c-398">Varsayılan konum projenin yanında bulunur ve adlandırılır `packages.lock.json` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-398">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| `RestoreForceEvaluate` | <span data-ttu-id="36b5c-399">Bağımlılıkları yeniden hesaplamak ve herhangi bir uyarı olmadan kilit dosyasını güncelleştirmek için geri yüklemeyi zorlar.</span><span class="sxs-lookup"><span data-stu-id="36b5c-399">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> |
| `RestorePackagesConfig` | <span data-ttu-id="36b5c-400">packages.config olan projeleri geri yükleyen bir kabul etme anahtarı. Yalnızca ile desteklenir `MSBuild -t:restore` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-400">An opt-in switch, that restores projects with packages.config. Support with `MSBuild -t:restore` only.</span></span> |
| `RestoreUseStaticGraphEvaluation` | <span data-ttu-id="36b5c-401">Standart değerlendirme yerine statik grafik değerlendirmesini kullanmak için bir tercih MSBuild edilen anahtar.</span><span class="sxs-lookup"><span data-stu-id="36b5c-401">An opt-in switch to use static graph MSBuild evaluation instead of the standard evaluation.</span></span> <span data-ttu-id="36b5c-402">Statik grafik değerlendirmesi, büyük depolar ve çözümler için önemli ölçüde daha hızlı olan deneysel bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="36b5c-402">Static graph evaluation is an experimental feature that's significantly faster for large repos and solutions.</span></span> |

#### <a name="examples"></a><span data-ttu-id="36b5c-403">Örnekler</span><span class="sxs-lookup"><span data-stu-id="36b5c-403">Examples</span></span>

<span data-ttu-id="36b5c-404">Komut satırı:</span><span class="sxs-lookup"><span data-stu-id="36b5c-404">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="36b5c-405">Proje dosyası:</span><span class="sxs-lookup"><span data-stu-id="36b5c-405">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="36b5c-406">Çıkışları geri yükleme</span><span class="sxs-lookup"><span data-stu-id="36b5c-406">Restore outputs</span></span>

<span data-ttu-id="36b5c-407">Restore derleme klasöründe aşağıdaki dosyaları oluşturur `obj` :</span><span class="sxs-lookup"><span data-stu-id="36b5c-407">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="36b5c-408">Dosya</span><span class="sxs-lookup"><span data-stu-id="36b5c-408">File</span></span> | <span data-ttu-id="36b5c-409">Açıklama</span><span class="sxs-lookup"><span data-stu-id="36b5c-409">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="36b5c-410">Tüm paket başvurularının bağımlılık grafiğini içerir.</span><span class="sxs-lookup"><span data-stu-id="36b5c-410">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="36b5c-411">MSBuildPaketlerde bulunan props 'a başvurular</span><span class="sxs-lookup"><span data-stu-id="36b5c-411">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="36b5c-412">MSBuildPaketlerde bulunan hedeflere başvurular</span><span class="sxs-lookup"><span data-stu-id="36b5c-412">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="36b5c-413">Tek bir komutla geri yükleme ve oluşturma MSBuild</span><span class="sxs-lookup"><span data-stu-id="36b5c-413">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="36b5c-414">NuGetHedefleri ve props 'ı getiren paketleri geri yükleyen olgu nedeniyle MSBuild , geri yükleme ve derleme değerlendirmeleri farklı genel özelliklerle çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="36b5c-414">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="36b5c-415">Bu, aşağıdakilerin öngörülemeyen ve genellikle yanlış bir davranışa sahip olacağı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="36b5c-415">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="36b5c-416">Bunun yerine önerilen yaklaşım şunlardır:</span><span class="sxs-lookup"><span data-stu-id="36b5c-416">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="36b5c-417">Aynı Logic şuna benzer diğer hedefler için de geçerlidir `build` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-417">The same logic applies to other targets similar to `build`.</span></span>

### <a name="restoring-packagereference-and-packagesconfig-projects-with-msbuild"></a><span data-ttu-id="36b5c-418">İle PackageReference ve packages.config projelerini geri yükleme MSBuild</span><span class="sxs-lookup"><span data-stu-id="36b5c-418">Restoring PackageReference and packages.config projects with MSBuild</span></span>

<span data-ttu-id="36b5c-419">MSBuild16.5 + ile packages.config de desteklenir `msbuild -t:restore` .</span><span class="sxs-lookup"><span data-stu-id="36b5c-419">With MSBuild 16.5+, packages.config are also supported for `msbuild -t:restore`.</span></span>

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> <span data-ttu-id="36b5c-420">`packages.config` restore yalnızca ile kullanılabilir `MSBuild 16.5+` ve `dotnet.exe`</span><span class="sxs-lookup"><span data-stu-id="36b5c-420">`packages.config` restore is only available with `MSBuild 16.5+`, and not with `dotnet.exe`</span></span>

### <a name="restoring-with-msbuild-static-graph-evaluation"></a><span data-ttu-id="36b5c-421">MSBuildStatik grafik değerlendirmesi ile geri yükleme</span><span class="sxs-lookup"><span data-stu-id="36b5c-421">Restoring with MSBuild static graph evaluation</span></span>

> [!NOTE]
> <span data-ttu-id="36b5c-422">MSBuild16.6 + ile, NuGet büyük depolar için geri yükleme süresini önemli ölçüde artıran komut satırından statik grafik değerlendirmesi kullanmak için deneysel bir özellik eklemiştir.</span><span class="sxs-lookup"><span data-stu-id="36b5c-422">With MSBuild 16.6+, NuGet has added an experimental feature to use static graph evaluation from the command line that significantly improves the restore time for large repositories.</span></span>

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

<span data-ttu-id="36b5c-423">Alternatif olarak, bir dizin. Build. props içindeki özelliği ayarlayarak bunu etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="36b5c-423">Alternatively you can enable it by setting the property in a Directory.Build.Props.</span></span>

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> <span data-ttu-id="36b5c-424">Visual Studio 2019. x ve NuGet 5. x itibariyle, bu özellik deneysel ve kabul edilmelidir.</span><span class="sxs-lookup"><span data-stu-id="36b5c-424">As of Visual Studio 2019.x and NuGet 5.x, this feature is considered experimental and opt-in.</span></span> <span data-ttu-id="36b5c-425">Bu özelliğin varsayılan olarak etkinleştirileceği hakkında daha fazla bilgi için [ NuGet /Home # 9803](https://github.com/NuGet/Home/issues/9803) izleyin.</span><span class="sxs-lookup"><span data-stu-id="36b5c-425">Follow [NuGet/Home#9803](https://github.com/NuGet/Home/issues/9803) for details on when this feature will be enabled by default.</span></span>

<span data-ttu-id="36b5c-426">Statik grafik geri yükleme, geri yükleme 'nin MSBuild bölümünü, Proje okuma ve değerlendirme, ancak geri yükleme algoritmasını etkilemez!</span><span class="sxs-lookup"><span data-stu-id="36b5c-426">Static graph restore changes the msbuild part of restore, the project reading and evaluation, but not the restore algorithm!</span></span> <span data-ttu-id="36b5c-427">Geri yükleme algoritması tüm NuGet araçlarda ( NuGet . exe, MSBuild . exe, dotnet.exe ve Visual Studio) aynıdır.</span><span class="sxs-lookup"><span data-stu-id="36b5c-427">The restore algorithm is the same across all NuGet tools (NuGet.exe, MSBuild.exe, dotnet.exe and Visual Studio).</span></span>

<span data-ttu-id="36b5c-428">Birçok senaryoda, statik grafik geri yükleme geçerli geri yüklemeden farklı davranabilir ve belirtilen bazı Packagereferklu veya ProjectReferences eksik olabilir.</span><span class="sxs-lookup"><span data-stu-id="36b5c-428">In very few scenarios, static graph restore may behave differently from current restore and certain declared PackageReferences or ProjectReferences might be missing.</span></span>

<span data-ttu-id="36b5c-429">Bir kez göz önünde bulundurmanız için, statik grafik geri yüklemeye geçiş yaparken şunu çalıştırmayı göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="36b5c-429">To ease your mind, as a one time check, when migrating to static graph restore, consider running:</span></span>

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

<span data-ttu-id="36b5c-430">NuGet hiçbir *değişiklik raporlanmamalıdır* .</span><span class="sxs-lookup"><span data-stu-id="36b5c-430">NuGet should *not* report any changes.</span></span> <span data-ttu-id="36b5c-431">Bir tutarsızlık görürseniz, lütfen [ NuGet /Home](https://github.com/nuget/home/issues/new)'ta bir sorun bildirin.</span><span class="sxs-lookup"><span data-stu-id="36b5c-431">If you do see a discrepancy, please file an issue at [NuGet/Home](https://github.com/nuget/home/issues/new).</span></span>

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="36b5c-432">Bir geri yükleme grafiğinden bir kitaplığı değiştirme</span><span class="sxs-lookup"><span data-stu-id="36b5c-432">Replacing one library from a restore graph</span></span>

<span data-ttu-id="36b5c-433">Geri yükleme yanlış derlemeyi alıyorsa, bu paketlerin varsayılan seçeneğini hariç tutabilir ve kendi seçimiyle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="36b5c-433">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="36b5c-434">Birincisi, en üst düzeyle `PackageReference` , tüm varlıkları hariç tut:</span><span class="sxs-lookup"><span data-stu-id="36b5c-434">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="36b5c-435">Ardından, DLL 'nin uygun yerel kopyasına kendi başvurunuz ekleyin:</span><span class="sxs-lookup"><span data-stu-id="36b5c-435">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
