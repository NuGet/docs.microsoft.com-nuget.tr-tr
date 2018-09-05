---
title: NuGet 1,5 sürüm notları
description: NuGet bilinen sorunları, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr 1.5 için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c2b549f65e675e5fde9ae1dfea3f44f7d691a86b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548731"
---
# <a name="nuget-15-release-notes"></a><span data-ttu-id="e9a93-103">NuGet 1,5 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="e9a93-103">NuGet 1.5 Release Notes</span></span>

<span data-ttu-id="e9a93-104">[1.4 NuGet sürüm notları](../release-notes/nuget-1.4.md) | [1.6 NuGet sürüm notları](../release-notes/nuget-1.6.md)</span><span class="sxs-lookup"><span data-stu-id="e9a93-104">[NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md) | [NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md)</span></span>

<span data-ttu-id="e9a93-105">NuGet 1.5 30 Ağustos 2011'de yayınlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="e9a93-105">NuGet 1.5 was released on August 30, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="e9a93-106">Özellikler</span><span class="sxs-lookup"><span data-stu-id="e9a93-106">Features</span></span>

### <a name="project-templates-with-preinstalled-nuget-packages"></a><span data-ttu-id="e9a93-107">Önceden yüklenmiş NuGet paketleri ile proje şablonları</span><span class="sxs-lookup"><span data-stu-id="e9a93-107">Project Templates with Preinstalled NuGet Packages</span></span>
<span data-ttu-id="e9a93-108">Yeni bir ASP.NET MVC 3 proje şablonu oluştururken, projeye dahil jQuery betik kitaplıkları gerçekten var NuGet paketlerini yükleyerek yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="e9a93-108">When creating a new ASP.NET MVC 3 project template, the jQuery script libraries included in the project are actually placed there by installing NuGet packages.</span></span>

<span data-ttu-id="e9a93-109">ASP.NET MVC 3 proje şablonu proje şablonu çağrıldığında yükleneceğini NuGet paketleri kümesi içerir.</span><span class="sxs-lookup"><span data-stu-id="e9a93-109">The ASP.NET MVC 3 project template includes a set of NuGet packages that get installed when the project template is invoked.</span></span> <span data-ttu-id="e9a93-110">Bir proje şablonu ile NuGet paketlerini içerecek şekilde bu özelliği artık NuGet özelliğidir, _herhangi_ proje şablonu artık yararlanabilir.</span><span class="sxs-lookup"><span data-stu-id="e9a93-110">This ability to include NuGet packages with a project template is now a feature of NuGet that _any_ project template can now take advantage of.</span></span>

<span data-ttu-id="e9a93-111">Bu özellik hakkında daha fazla ayrıntı için bu okuma [özelliğinin geliştirici tarafından blog gönderisi](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span><span class="sxs-lookup"><span data-stu-id="e9a93-111">For more details about this feature, read this [blog post by the developer of the feature](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span></span>

### <a name="explicit-assembly-references"></a><span data-ttu-id="e9a93-112">Açık derleme başvuruları</span><span class="sxs-lookup"><span data-stu-id="e9a93-112">Explicit Assembly References</span></span>

<span data-ttu-id="e9a93-113">Yeni eklenen `<references />` içinde hangi derlemelerin açıkça belirtmek için kullanılan öğe paket başvurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e9a93-113">Added a new `<references />` element used to explicitly specify which assemblies within the the package should be referenced.</span></span>

<span data-ttu-id="e9a93-114">Örneğin şunu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e9a93-114">For example, if you add the following:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="e9a93-115">Ardından yalnızca `xunit.dll` ve `xunit.extensions.dll` uygun başvurulacağını [framework/PROFILE alt](../reference/nuspec.md#explicit-assembly-references) , `lib` klasör klasöründe diğer derlemeler olsa bile.</span><span class="sxs-lookup"><span data-stu-id="e9a93-115">Then only the `xunit.dll` and `xunit.extensions.dll` will be referenced from the appropriate [framework/profile subfolder](../reference/nuspec.md#explicit-assembly-references) of the `lib` folder even if there are other assemblies in the folder.</span></span>

<span data-ttu-id="e9a93-116">Bu öğe atlanır sonra her derleme başvurusu olan genel davranış uygulanır `lib` klasör.</span><span class="sxs-lookup"><span data-stu-id="e9a93-116">If this element is omitted, then the usual behavior applies, which is to reference every assembly in the `lib` folder.</span></span>

<span data-ttu-id="e9a93-117">__Bu özellik ne için kullanılır?__</span><span class="sxs-lookup"><span data-stu-id="e9a93-117">__What is this feature used for?__</span></span>

<span data-ttu-id="e9a93-118">Bu özellik yalnızca tasarım zamanı derlemelerini destekler.</span><span class="sxs-lookup"><span data-stu-id="e9a93-118">This feature supports design-time only assemblies.</span></span> <span data-ttu-id="e9a93-119">Örneğin, kod sözleşmeleri kullanırken, sözleşme derlemeleri böylece Visual Studio bunları bulabilirsiniz ancak sözleşme derlemeler proje tarafından gerçekten başvurulmaması gereken ve içine kopyalanmaması gereken büyütmek çalışma zamanı derlemeleri yanında olmasına gerek `bin` klasör.</span><span class="sxs-lookup"><span data-stu-id="e9a93-119">For example, when using Code Contracts, the contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies should not actually be referenced by the project and should not be copied into the `bin` folder.</span></span>

<span data-ttu-id="e9a93-120">Benzer şekilde, özellik için gereken çalışma zamanı derlemeleri yanında bulunan, ancak proje başvurularından'hariç tutulan araçları derlemelerini XUnit gibi birim test çerçeveler için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e9a93-120">Likewise, the feature can be used to for unit test frameworks such as XUnit which need its tools assemblies to be located next to the runtime assemblies, but excluded from project references.</span></span>

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a><span data-ttu-id="e9a93-121">.nuspec dosyaları dışarıda bırak özelliği eklendi</span><span class="sxs-lookup"><span data-stu-id="e9a93-121">Added ability to exclude files in the .nuspec</span></span>
<span data-ttu-id="e9a93-122">`<file>` Öğesi içinde bir `.nuspec` dosyası, belirli bir dosyayı veya bir joker karakter kullanarak dosyaları eklemek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e9a93-122">The `<file>` element within a `.nuspec` file can be used to include a specific file or a set of files using a wildcard.</span></span> <span data-ttu-id="e9a93-123">Joker karakter kullanırken, belirli bir alt kümesini eklenen dosyalar hariç tutmak için hiçbir yolu yoktur.</span><span class="sxs-lookup"><span data-stu-id="e9a93-123">When using a wildcard, there's no way to exclude a specific subset of the included files.</span></span> <span data-ttu-id="e9a93-124">Örneğin, belirli bir dışında bir klasördeki tüm metin dosyalarını istediğinizi varsayalım.</span><span class="sxs-lookup"><span data-stu-id="e9a93-124">For example, suppose you want all text files within a folder except a specific one.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

<span data-ttu-id="e9a93-125">Birden çok dosyayı belirtmek için noktalı virgül kullanın.</span><span class="sxs-lookup"><span data-stu-id="e9a93-125">Use semicolons to specify multiple files.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

<span data-ttu-id="e9a93-126">Veya tüm yedekleme dosyaları gibi dosyaları hariç tutmak için bir joker kullanın</span><span class="sxs-lookup"><span data-stu-id="e9a93-126">Or use a wild card to exclude a set of files such as all backup files</span></span>

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a><span data-ttu-id="e9a93-127">İletişim kutusunu kullanarak paketlerini kaldırma bağımlılıkları kaldırmak isteyip istemediğinizi sorar</span><span class="sxs-lookup"><span data-stu-id="e9a93-127">Removing packages using the dialog prompts to remove dependencies</span></span>
<span data-ttu-id="e9a93-128">Bir paket bağımlılığı olan bir paketin bağımlılıkları paketin birlikte kaldırılmasını sağlayan NuGet ister kaldırırken.</span><span class="sxs-lookup"><span data-stu-id="e9a93-128">When uninstalling a package with dependencies, NuGet prompts, allowing the removal of a package's dependencies along with the package.</span></span>

![Bağımlı paket kaldırılıyor](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a><span data-ttu-id="e9a93-130">`Get-Package` komut geliştirme</span><span class="sxs-lookup"><span data-stu-id="e9a93-130">`Get-Package` command improvement</span></span>
<span data-ttu-id="e9a93-131">`Get-Package` Komutu artık bir `-ProjectName` parametresi.</span><span class="sxs-lookup"><span data-stu-id="e9a93-131">The `Get-Package` command now supports a `-ProjectName` parameter.</span></span> <span data-ttu-id="e9a93-132">Bu nedenle komutu</span><span class="sxs-lookup"><span data-stu-id="e9a93-132">So the command</span></span>

    Get-Package –ProjectName A

<span data-ttu-id="e9a93-133">A. projesinde yüklü tüm paketleri listeler</span><span class="sxs-lookup"><span data-stu-id="e9a93-133">will list all packages installed in project A.</span></span>

### <a name="support-for-proxies-that-require-authentication"></a><span data-ttu-id="e9a93-134">Kimlik doğrulaması gerektiren bir proxy için destek</span><span class="sxs-lookup"><span data-stu-id="e9a93-134">Support for Proxies that require authentication</span></span>
<span data-ttu-id="e9a93-135">NuGet kimlik doğrulaması gerektiren bir proxy kullanırken, NuGet artık proxy kimlik bilgileri istenir.</span><span class="sxs-lookup"><span data-stu-id="e9a93-135">When using NuGet behind a proxy that requires authentication, NuGet will now prompt for proxy credentials.</span></span> <span data-ttu-id="e9a93-136">Kimlik bilgilerini girme uzak depoya bağlanmak NuGet sağlar.</span><span class="sxs-lookup"><span data-stu-id="e9a93-136">Entering credentials allows NuGet to connect to the remote repository.</span></span>

### <a name="support-for-repositories-that-require-authentication"></a><span data-ttu-id="e9a93-137">Kimlik doğrulaması gerektiren depoları için destek</span><span class="sxs-lookup"><span data-stu-id="e9a93-137">Support for Repositories that require authentication</span></span>
<span data-ttu-id="e9a93-138">NuGet artık destekliyor bağlanma [özel depo](../hosting-packages/local-feeds.md) temel veya NTLM kimlik doğrulaması gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e9a93-138">NuGet now supports connecting to [private repositories](../hosting-packages/local-feeds.md) that require basic or NTLM authentication.</span></span>

<span data-ttu-id="e9a93-139">Özet kimlik doğrulaması için destek, gelecek sürümlerin birinde eklenecektir.</span><span class="sxs-lookup"><span data-stu-id="e9a93-139">Support for Digest authentication will be added in a future release.</span></span>

### <a name="performance-improvements-to-the-nugetorg-repository"></a><span data-ttu-id="e9a93-140">Nuget.org depoya performans geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="e9a93-140">Performance improvements to the nuget.org repository</span></span>
<span data-ttu-id="e9a93-141">Nuget.org Galerisine paket listeleme ve daha hızlı arama yapmak için birkaç performans geliştirmeleri yaptık.</span><span class="sxs-lookup"><span data-stu-id="e9a93-141">We've made several performance improvements to the nuget.org gallery to make package listing and searching faster.</span></span>

### <a name="solution-dialog-project-filtering"></a><span data-ttu-id="e9a93-142">Çözüm, proje iletişim filtreleme</span><span class="sxs-lookup"><span data-stu-id="e9a93-142">Solution dialog project filtering</span></span>
<span data-ttu-id="e9a93-143">Çözüm düzeyinde iletişim kutusunda, hangi projelerin yüklemek isterken, yalnızca seçilen paket ile uyumlu olan projeler göstereceğiz.</span><span class="sxs-lookup"><span data-stu-id="e9a93-143">In the Solution-level dialog, when prompting for what projects to install, we only show projects that are compatible with the selected package.</span></span>

### <a name="package-release-notes"></a><span data-ttu-id="e9a93-144">Paket sürüm notları</span><span class="sxs-lookup"><span data-stu-id="e9a93-144">Package Release Notes</span></span>
<span data-ttu-id="e9a93-145">NuGet paketlerini artık sürüm notları için destek içerir.</span><span class="sxs-lookup"><span data-stu-id="e9a93-145">NuGet packages now include support for release notes.</span></span> <span data-ttu-id="e9a93-146">Yayın yalnızca show yukarı görüntülerken notları _güncelleştirmeleri_ bir paket için bu nedenle, değil mantıklı ilk sürümünüzü eklemek.</span><span class="sxs-lookup"><span data-stu-id="e9a93-146">The release notes only show up when viewing _Updates_ for a package, so it doesn't make sense to add them to your first release.</span></span>

![Güncelleştirmeler sekmesini içinde sürüm notları](./media/manage-nuget-packages-release-notes.png)

<span data-ttu-id="e9a93-148">Bir paket için sürüm notları eklemek için yeni kullanın `<releaseNotes />` soubor NuSpec meta veri öğesi.</span><span class="sxs-lookup"><span data-stu-id="e9a93-148">To add release notes to a package, use the new `<releaseNotes />` metadata element in your NuSpec file.</span></span>

### <a name="nuspec-ltfiles-gt-improvement"></a><span data-ttu-id="e9a93-149">.nuspec & ltfiles /&gt; geliştirme</span><span class="sxs-lookup"><span data-stu-id="e9a93-149">.nuspec &ltfiles /&gt; improvement</span></span>
<span data-ttu-id="e9a93-150">`.nuspec` Dosya artık sağlayan boş `<files />` herhangi bir dosya paketinde içermeyecek şekilde nuget.exe belirten öğe.</span><span class="sxs-lookup"><span data-stu-id="e9a93-150">The `.nuspec` file now allows empty `<files />` element, which tells nuget.exe not to include any file in the package.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="e9a93-151">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="e9a93-151">Bug Fixes</span></span>
<span data-ttu-id="e9a93-152">NuGet 1.5, iş öğelerini sabit 107 toplam vardı.</span><span class="sxs-lookup"><span data-stu-id="e9a93-152">NuGet 1.5 had a total of 107 work items fixed.</span></span> <span data-ttu-id="e9a93-153">Bu 103 hataları olarak işaretlenmiş.</span><span class="sxs-lookup"><span data-stu-id="e9a93-153">103 of those were marked as bugs.</span></span>

<span data-ttu-id="e9a93-154">Tam bir listesi için iş öğeleri NuGet 1.5 Lütfen görünümü sabit [bu sürüm için NuGet sorun İzleyicisi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="e9a93-154">For a full list of work items fixed in NuGet 1.5, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="e9a93-155">Önemli hata düzeltmeleri:</span><span class="sxs-lookup"><span data-stu-id="e9a93-155">Bug fixes worth noting:</span></span>

* <span data-ttu-id="e9a93-156">[Sorunu 1273](http://nuget.codeplex.com/workitem/1273): yapılan `packages.config` paketleri alfabetik sıralama ve fazladan boşlukları kaldırmanın kolay daha fazla sürüm denetimi.</span><span class="sxs-lookup"><span data-stu-id="e9a93-156">[Issue 1273](http://nuget.codeplex.com/workitem/1273): Made `packages.config` more version control friendly by sorting packages alphabetically and removing extra whitespace.</span></span>
* <span data-ttu-id="e9a93-157">[Sorun 844](http://nuget.codeplex.com/workitem/844): sürüm numaraları artık normalleştirilmiş böylece `Install-Package 1.0` bir paket sürümü ile çalışır `1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="e9a93-157">[Issue 844](http://nuget.codeplex.com/workitem/844): Version numbers are now normalized so that `Install-Package 1.0` works on a package with the version `1.0.0`.</span></span>
* <span data-ttu-id="e9a93-158">[Sorun 1060](http://nuget.codeplex.com/workitem/1060): nuget.exe kullanarak bir paket oluştururken `-Version` bayrağı geçersiz kılmaları `<version />` öğesi.</span><span class="sxs-lookup"><span data-stu-id="e9a93-158">[Issue 1060](http://nuget.codeplex.com/workitem/1060): When creating a package using nuget.exe, the `-Version` flag overrides the `<version />` element.</span></span>
