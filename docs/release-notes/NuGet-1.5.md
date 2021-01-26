---
title: NuGet 1,5 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 1,5 sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c9946f3d8cf545ec14f842c40105743c231b4b72
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777091"
---
# <a name="nuget-15-release-notes"></a><span data-ttu-id="abe7e-103">NuGet 1,5 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="abe7e-103">NuGet 1.5 Release Notes</span></span>

<span data-ttu-id="abe7e-104">[NuGet 1,4 sürüm notları](../release-notes/nuget-1.4.md)  |  [NuGet 1,6 sürüm notları](../release-notes/nuget-1.6.md)</span><span class="sxs-lookup"><span data-stu-id="abe7e-104">[NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md) | [NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md)</span></span>

<span data-ttu-id="abe7e-105">NuGet 1,5, 30 Ağustos 2011 tarihinde yayınlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="abe7e-105">NuGet 1.5 was released on August 30, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="abe7e-106">Özellikler</span><span class="sxs-lookup"><span data-stu-id="abe7e-106">Features</span></span>

### <a name="project-templates-with-preinstalled-nuget-packages"></a><span data-ttu-id="abe7e-107">Önceden yüklenmiş NuGet paketlerine sahip proje şablonları</span><span class="sxs-lookup"><span data-stu-id="abe7e-107">Project Templates with Preinstalled NuGet Packages</span></span>
<span data-ttu-id="abe7e-108">Yeni bir ASP.NET MVC 3 proje şablonu oluştururken, projeye dahil edilen jQuery betik kitaplıkları, NuGet paketleri yüklenerek buraya yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="abe7e-108">When creating a new ASP.NET MVC 3 project template, the jQuery script libraries included in the project are actually placed there by installing NuGet packages.</span></span>

<span data-ttu-id="abe7e-109">ASP.NET MVC 3 proje şablonu, proje şablonu çağrıldığında yüklenen bir NuGet paketleri kümesi içerir.</span><span class="sxs-lookup"><span data-stu-id="abe7e-109">The ASP.NET MVC 3 project template includes a set of NuGet packages that get installed when the project template is invoked.</span></span> <span data-ttu-id="abe7e-110">Bir proje şablonu ile NuGet paketleri dahil etme özelliği artık _herhangi_ bir proje şablonunun avantajlarından yararlanabilme özelliği olan bir NuGet özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="abe7e-110">This ability to include NuGet packages with a project template is now a feature of NuGet that _any_ project template can now take advantage of.</span></span>

<span data-ttu-id="abe7e-111">Bu özellik hakkında daha fazla bilgi için bu [blog gönderisini özelliğin geliştiricisi ile](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx)okuyun.</span><span class="sxs-lookup"><span data-stu-id="abe7e-111">For more details about this feature, read this [blog post by the developer of the feature](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span></span>

### <a name="explicit-assembly-references"></a><span data-ttu-id="abe7e-112">Açık bütünleştirilmiş kod başvuruları</span><span class="sxs-lookup"><span data-stu-id="abe7e-112">Explicit Assembly References</span></span>

<span data-ttu-id="abe7e-113">`<references />`Paket içindeki hangi derlemelerin başvurulduğunu açıkça belirtmek için kullanılan yeni bir öğe eklendi.</span><span class="sxs-lookup"><span data-stu-id="abe7e-113">Added a new `<references />` element used to explicitly specify which assemblies within the the package should be referenced.</span></span>

<span data-ttu-id="abe7e-114">Örneğin, aşağıdakileri eklerseniz:</span><span class="sxs-lookup"><span data-stu-id="abe7e-114">For example, if you add the following:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="abe7e-115">Daha sonra, `xunit.dll` `xunit.extensions.dll` klasörde başka derlemeler olsa da, klasörün yalnızca ve ilgili [Framework/profile alt](../reference/nuspec.md#explicit-assembly-references) klasöründen başvuracaktır `lib` .</span><span class="sxs-lookup"><span data-stu-id="abe7e-115">Then only the `xunit.dll` and `xunit.extensions.dll` will be referenced from the appropriate [framework/profile subfolder](../reference/nuspec.md#explicit-assembly-references) of the `lib` folder even if there are other assemblies in the folder.</span></span>

<span data-ttu-id="abe7e-116">Bu öğe atlanırsa, her bir derleme, klasördeki her derlemeye başvurmak için geçerlidir `lib` .</span><span class="sxs-lookup"><span data-stu-id="abe7e-116">If this element is omitted, then the usual behavior applies, which is to reference every assembly in the `lib` folder.</span></span>

<span data-ttu-id="abe7e-117">__Bu özellik ne için kullanılır?__</span><span class="sxs-lookup"><span data-stu-id="abe7e-117">__What is this feature used for?__</span></span>

<span data-ttu-id="abe7e-118">Bu özellik yalnızca tasarım zamanı derlemelerini destekler.</span><span class="sxs-lookup"><span data-stu-id="abe7e-118">This feature supports design-time only assemblies.</span></span> <span data-ttu-id="abe7e-119">Örneğin, kod sözleşmeleri kullanılırken, Visual Studio 'Nun bunları bulabilmesi için anlaşma derlemelerinin, iyileştirdikleri çalışma zamanı derlemelerinin yanında olması gerekir, ancak sözleşme derlemelerinin proje tarafından gerçekten başvurulması ve klasöre kopyalanmaması gerekir `bin` .</span><span class="sxs-lookup"><span data-stu-id="abe7e-119">For example, when using Code Contracts, the contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies should not actually be referenced by the project and should not be copied into the `bin` folder.</span></span>

<span data-ttu-id="abe7e-120">Benzer şekilde, özelliği, araç derlemelerinin çalışma zamanı derlemelerinin yanında konumlandırılabilir, ancak proje başvurularından hariç tutulması gereken XUnit gibi birim testi çerçeveleri için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="abe7e-120">Likewise, the feature can be used to for unit test frameworks such as XUnit which need its tools assemblies to be located next to the runtime assemblies, but excluded from project references.</span></span>

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a><span data-ttu-id="abe7e-121">. Nuspec içindeki dosyaları dışarıda bırakma özelliği eklendi</span><span class="sxs-lookup"><span data-stu-id="abe7e-121">Added ability to exclude files in the .nuspec</span></span>
<span data-ttu-id="abe7e-122">`<file>`Bir dosya içindeki öğe, bir `.nuspec` joker karakter kullanarak belirli bir dosyayı veya bir dosya kümesini dahil etmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="abe7e-122">The `<file>` element within a `.nuspec` file can be used to include a specific file or a set of files using a wildcard.</span></span> <span data-ttu-id="abe7e-123">Joker karakter kullanırken, eklenen dosyaların belirli bir alt kümesini dışlayamazsınız.</span><span class="sxs-lookup"><span data-stu-id="abe7e-123">When using a wildcard, there's no way to exclude a specific subset of the included files.</span></span> <span data-ttu-id="abe7e-124">Örneğin, belirli bir klasörde yer alan tüm metin dosyalarını istediğiniz gibi düşünün.</span><span class="sxs-lookup"><span data-stu-id="abe7e-124">For example, suppose you want all text files within a folder except a specific one.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

<span data-ttu-id="abe7e-125">Birden çok dosya belirtmek için noktalı virgül kullanın.</span><span class="sxs-lookup"><span data-stu-id="abe7e-125">Use semicolons to specify multiple files.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

<span data-ttu-id="abe7e-126">Ya da tüm yedekleme dosyaları gibi bir dosya kümesini dışlamak için bir joker karakter kullanın</span><span class="sxs-lookup"><span data-stu-id="abe7e-126">Or use a wild card to exclude a set of files such as all backup files</span></span>

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a><span data-ttu-id="abe7e-127">İletişim kutusu kullanarak paketleri kaldırma bağımlılıklarını kaldırma istemleri</span><span class="sxs-lookup"><span data-stu-id="abe7e-127">Removing packages using the dialog prompts to remove dependencies</span></span>
<span data-ttu-id="abe7e-128">Bağımlılıklar içeren bir paket kaldırılırken, NuGet istemleri, paket ile birlikte paketin bağımlılıklarının kaldırılmasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="abe7e-128">When uninstalling a package with dependencies, NuGet prompts, allowing the removal of a package's dependencies along with the package.</span></span>

![Bağımlı paketler kaldırılıyor](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a><span data-ttu-id="abe7e-130">`Get-Package` komut geliştirmesi</span><span class="sxs-lookup"><span data-stu-id="abe7e-130">`Get-Package` command improvement</span></span>
<span data-ttu-id="abe7e-131">`Get-Package`Komut artık bir parametreyi destekliyor `-ProjectName` .</span><span class="sxs-lookup"><span data-stu-id="abe7e-131">The `Get-Package` command now supports a `-ProjectName` parameter.</span></span> <span data-ttu-id="abe7e-132">Bu nedenle komut</span><span class="sxs-lookup"><span data-stu-id="abe7e-132">So the command</span></span>

```
Get-Package –ProjectName A
```

<span data-ttu-id="abe7e-133">, A projesinde yüklü olan tüm paketleri listeler.</span><span class="sxs-lookup"><span data-stu-id="abe7e-133">will list all packages installed in project A.</span></span>

### <a name="support-for-proxies-that-require-authentication"></a><span data-ttu-id="abe7e-134">Kimlik doğrulaması gerektiren proxy 'Ler için destek</span><span class="sxs-lookup"><span data-stu-id="abe7e-134">Support for Proxies that require authentication</span></span>
<span data-ttu-id="abe7e-135">Kimlik doğrulaması gerektiren bir proxy 'nin arkasında NuGet kullanılırken, NuGet artık proxy kimlik bilgilerini ister.</span><span class="sxs-lookup"><span data-stu-id="abe7e-135">When using NuGet behind a proxy that requires authentication, NuGet will now prompt for proxy credentials.</span></span> <span data-ttu-id="abe7e-136">Kimlik bilgilerinin girilmesi, NuGet 'in uzak depoya bağlanmasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="abe7e-136">Entering credentials allows NuGet to connect to the remote repository.</span></span>

### <a name="support-for-repositories-that-require-authentication"></a><span data-ttu-id="abe7e-137">Kimlik doğrulaması gerektiren depolar için destek</span><span class="sxs-lookup"><span data-stu-id="abe7e-137">Support for Repositories that require authentication</span></span>
<span data-ttu-id="abe7e-138">NuGet artık temel veya NTLM kimlik doğrulaması gerektiren [özel depolara](../hosting-packages/local-feeds.md) bağlanmayı desteklemektedir.</span><span class="sxs-lookup"><span data-stu-id="abe7e-138">NuGet now supports connecting to [private repositories](../hosting-packages/local-feeds.md) that require basic or NTLM authentication.</span></span>

<span data-ttu-id="abe7e-139">Özet kimlik doğrulaması desteği gelecek bir sürüme eklenecektir.</span><span class="sxs-lookup"><span data-stu-id="abe7e-139">Support for Digest authentication will be added in a future release.</span></span>

### <a name="performance-improvements-to-the-nugetorg-repository"></a><span data-ttu-id="abe7e-140">Nuget.org deposunda performans iyileştirmeleri</span><span class="sxs-lookup"><span data-stu-id="abe7e-140">Performance improvements to the nuget.org repository</span></span>
<span data-ttu-id="abe7e-141">Paket listesini ve aramayı daha hızlı hale getirmek için nuget.org galerisinde çeşitli performans geliştirmeleri yaptık.</span><span class="sxs-lookup"><span data-stu-id="abe7e-141">We've made several performance improvements to the nuget.org gallery to make package listing and searching faster.</span></span>

### <a name="solution-dialog-project-filtering"></a><span data-ttu-id="abe7e-142">Çözüm iletişim kutusu proje filtreleme</span><span class="sxs-lookup"><span data-stu-id="abe7e-142">Solution dialog project filtering</span></span>
<span data-ttu-id="abe7e-143">Çözüm düzeyi iletişim kutusunda, hangi projelerin yükleneceğini sorduktan sonra yalnızca seçili paketle uyumlu olan projeleri gösteririz.</span><span class="sxs-lookup"><span data-stu-id="abe7e-143">In the Solution-level dialog, when prompting for what projects to install, we only show projects that are compatible with the selected package.</span></span>

### <a name="package-release-notes"></a><span data-ttu-id="abe7e-144">Paket sürüm notları</span><span class="sxs-lookup"><span data-stu-id="abe7e-144">Package Release Notes</span></span>
<span data-ttu-id="abe7e-145">NuGet paketleri artık sürüm notları desteğini içerir.</span><span class="sxs-lookup"><span data-stu-id="abe7e-145">NuGet packages now include support for release notes.</span></span> <span data-ttu-id="abe7e-146">Sürüm notları yalnızca bir paket için _güncelleştirmeler_ görüntülenirken görünür, bu nedenle bunları ilk sürüme eklemek mantıklı değildir.</span><span class="sxs-lookup"><span data-stu-id="abe7e-146">The release notes only show up when viewing _Updates_ for a package, so it doesn't make sense to add them to your first release.</span></span>

![Güncelleştirmeler sekmesi içinde sürüm notları](./media/manage-nuget-packages-release-notes.png)

<span data-ttu-id="abe7e-148">Bir pakete sürüm notları eklemek için `<releaseNotes />` NuSpec dosyanızdaki yeni meta veri öğesini kullanın.</span><span class="sxs-lookup"><span data-stu-id="abe7e-148">To add release notes to a package, use the new `<releaseNotes />` metadata element in your NuSpec file.</span></span>

### <a name="nuspec-ltfiles-gt-improvement"></a><span data-ttu-id="abe7e-149">. nuspec &ltdosyaları/ &gt; geliştirmesi</span><span class="sxs-lookup"><span data-stu-id="abe7e-149">.nuspec &ltfiles /&gt; improvement</span></span>
<span data-ttu-id="abe7e-150">`.nuspec`Dosya artık boş öğeye izin veriyor `<files />` . bu, nuget.exe pakete hiçbir dosya dahil olmadığını söyler.</span><span class="sxs-lookup"><span data-stu-id="abe7e-150">The `.nuspec` file now allows empty `<files />` element, which tells nuget.exe not to include any file in the package.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="abe7e-151">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="abe7e-151">Bug Fixes</span></span>
<span data-ttu-id="abe7e-152">NuGet 1,5, Toplam 107 iş öğesine sahipti.</span><span class="sxs-lookup"><span data-stu-id="abe7e-152">NuGet 1.5 had a total of 107 work items fixed.</span></span> <span data-ttu-id="abe7e-153">103 tanesi hata olarak işaretlendi.</span><span class="sxs-lookup"><span data-stu-id="abe7e-153">103 of those were marked as bugs.</span></span>

<span data-ttu-id="abe7e-154">NuGet 1,5 ' de düzeltilen iş öğelerinin tam listesi için lütfen [Bu sürüm Için NuGet sorun İzleyicisi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0)' ni görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="abe7e-154">For a full list of work items fixed in NuGet 1.5, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="abe7e-155">Hata düzeltmeleri dikkat edilecek değer:</span><span class="sxs-lookup"><span data-stu-id="abe7e-155">Bug fixes worth noting:</span></span>

* <span data-ttu-id="abe7e-156">[Sorun 1273](http://nuget.codeplex.com/workitem/1273): `packages.config` paketler alfabetik olarak sıralandığında ve fazladan boşluk kaldırılarak daha fazla sürüm denetimi yapılıyor.</span><span class="sxs-lookup"><span data-stu-id="abe7e-156">[Issue 1273](http://nuget.codeplex.com/workitem/1273): Made `packages.config` more version control friendly by sorting packages alphabetically and removing extra whitespace.</span></span>
* <span data-ttu-id="abe7e-157">[Sorun 844](http://nuget.codeplex.com/workitem/844): sürüm numaraları artık `Install-Package 1.0` , sürümüne sahip bir pakette çalışacak şekilde normalleştirilmektedir `1.0.0` .</span><span class="sxs-lookup"><span data-stu-id="abe7e-157">[Issue 844](http://nuget.codeplex.com/workitem/844): Version numbers are now normalized so that `Install-Package 1.0` works on a package with the version `1.0.0`.</span></span>
* <span data-ttu-id="abe7e-158">[Sorun 1060](http://nuget.codeplex.com/workitem/1060): nuget.exe kullanarak bir paket oluştururken, `-Version` bayrak öğeyi geçersiz kılar `<version />` .</span><span class="sxs-lookup"><span data-stu-id="abe7e-158">[Issue 1060](http://nuget.codeplex.com/workitem/1060): When creating a package using nuget.exe, the `-Version` flag overrides the `<version />` element.</span></span>
