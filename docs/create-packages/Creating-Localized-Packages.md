---
title: Yerelleştirilmiş NuGet Paketi Nasıl Oluşturulur?
description: Tüm derlemeleri tek bir pakete ekleyerek veya ayrı derlemeler yayımlayarak yerelleştirilmiş NuGet paketleri oluşturmanın iki yolu hakkındaki ayrıntılar.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 83414a824676844f9e44eab874e5eac788d50583
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "73610947"
---
# <a name="creating-localized-nuget-packages"></a><span data-ttu-id="7425a-103">Yerelleştirilmiş NuGet paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="7425a-103">Creating localized NuGet packages</span></span>

<span data-ttu-id="7425a-104">Kitaplığın yerelleştirilmiş sürümlerini oluşturmanın iki yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="7425a-104">There are two ways to create localized versions of a library:</span></span>

1. <span data-ttu-id="7425a-105">Tüm yerelleştirilmiş kaynak derlemelerini tek bir pakete ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7425a-105">Include all localized resources assemblies in a single package.</span></span>
1. <span data-ttu-id="7425a-106">Katı bir dizi kuralı izleyerek ayrı yerelleştirilmiş uydu paketleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7425a-106">Create separate localized satellite packages by following a strict set of conventions.</span></span>

<span data-ttu-id="7425a-107">Her iki yöntemin de avantajları ve dezavantajları vardır, aşağıdaki bölümlerde açıklandığı gibi.</span><span class="sxs-lookup"><span data-stu-id="7425a-107">Both methods have their advantages and disadvantages, as described in the following sections.</span></span>

## <a name="localized-resource-assemblies-in-a-single-package"></a><span data-ttu-id="7425a-108">Tek bir pakette yerelleştirilmiş kaynak derlemeleri</span><span class="sxs-lookup"><span data-stu-id="7425a-108">Localized resource assemblies in a single package</span></span>

<span data-ttu-id="7425a-109">Yerelleştirilmiş kaynak derlemelerini tek bir pakete dahil etmek genellikle en basit yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="7425a-109">Including localized resource assemblies in a single package is typically the simplest approach.</span></span> <span data-ttu-id="7425a-110">Bunu yapmak için, paket `lib` varsayılanı dışında desteklenen dil için klasörler oluşturun (en-us olarak kabul edilir).</span><span class="sxs-lookup"><span data-stu-id="7425a-110">To do this, create folders within `lib` for supported language other than the package default (assumed to be en-us).</span></span> <span data-ttu-id="7425a-111">Bu klasörlerde kaynak derlemeleri ve yerelleştirilmiş IntelliSense XML dosyaları yerleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7425a-111">In these folders you can place resource assemblies and localized IntelliSense XML files.</span></span>

<span data-ttu-id="7425a-112">Örneğin, aşağıdaki klasör yapısı destekler, Almanca (de), İtalyanca (it), Japonca (ja), Rusça (ru), Çince (Basitleştirilmiş) (zh-Hans) ve Çince (Geleneksel) (zh-Hant):</span><span class="sxs-lookup"><span data-stu-id="7425a-112">For example, the following folder structure supports, German (de), Italian (it), Japanese (ja), Russian (ru), Chinese (Simplified) (zh-Hans), and Chinese (Traditional) (zh-Hant):</span></span>

    lib
    └───net40
        │   Contoso.Utilities.dll
        │   Contoso.Utilities.xml
        │
        ├───de
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───it
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ja
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ru
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───zh-Hans
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        └───zh-Hant
                Contoso.Utilities.resources.dll
                Contoso.Utilities.xml

<span data-ttu-id="7425a-113">Dillerin tamamının hedef çerçeve klasörü `net40` altında listelenmiş olduğunu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7425a-113">You can see that the languages are all listed underneath the `net40` target framework folder.</span></span> <span data-ttu-id="7425a-114">Birden çok [çerçeveyi destekliyorsanız,](../create-packages/supporting-multiple-target-frameworks.md)her varyant için `lib` altında bir klasör vardır.</span><span class="sxs-lookup"><span data-stu-id="7425a-114">If you're [supporting multiple frameworks](../create-packages/supporting-multiple-target-frameworks.md), then you have a folder under `lib` for each variant.</span></span>

<span data-ttu-id="7425a-115">Bu klasörler yerinde, daha sonra tüm dosyaları `.nuspec`başvuru:</span><span class="sxs-lookup"><span data-stu-id="7425a-115">With these folders in place, you then reference all the files in your `.nuspec`:</span></span>

```xml
<?xml version="1.0"?>
<package>
    <metadata>...
    </metadata>
    <files>
    <file src="lib\**" target="lib" />
    </files>
</package>
```

<span data-ttu-id="7425a-116">Bu yaklaşımı kullanan bir örnek paket [Microsoft.Data.OData 5.4.0'dır.](https://nuget.org/packages/Microsoft.Data.OData/5.4.0)</span><span class="sxs-lookup"><span data-stu-id="7425a-116">One example package that uses this approach is [Microsoft.Data.OData 5.4.0](https://nuget.org/packages/Microsoft.Data.OData/5.4.0).</span></span>

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a><span data-ttu-id="7425a-117">Avantajları ve dezavantajları (yerelleştirilmiş kaynak derlemeleri)</span><span class="sxs-lookup"><span data-stu-id="7425a-117">Advantages and disadvantages (localized resource assemblies)</span></span>

<span data-ttu-id="7425a-118">Tüm dilleri tek bir pakette birleştirmenin birkaç dezavantajı vardır:</span><span class="sxs-lookup"><span data-stu-id="7425a-118">Bundling all languages in a single package has a few disadvantages:</span></span>

1. <span data-ttu-id="7425a-119">**Paylaşılan meta veriler**: NuGet paketi yalnızca `.nuspec` tek bir dosya içerebildiği için, yalnızca tek bir dil için meta veri sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7425a-119">**Shared metadata**: Because a NuGet package can only contain a single `.nuspec` file, you can provide metadata for only a single language.</span></span> <span data-ttu-id="7425a-120">Diğer bir de, NuGet yerelleştirilmiş meta verileri desteklemez.</span><span class="sxs-lookup"><span data-stu-id="7425a-120">That is, NuGet does not present support localized metadata.</span></span>
1. <span data-ttu-id="7425a-121">**Paket boyutu**: Desteklediğiniz dil sayısına bağlı olarak, kitaplık önemli ölçüde büyüyebilir ve bu da paketin yüklenmesini ve geri yüklenmesini yavaşlatır.</span><span class="sxs-lookup"><span data-stu-id="7425a-121">**Package size**: Depending on the number of languages you support, the library can become considerably large, which slows installing and restoring the package.</span></span>
1. <span data-ttu-id="7425a-122">**Eşzamanlı sürümler**: Yerelleştirilmiş dosyaları tek bir pakete dönüştürmek, her yerelleştirmeyi ayrı ayrı serbest bırakmak yerine, o paketteki tüm varlıkları aynı anda serbest bırakmanızı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="7425a-122">**Simultaneous releases**: Bundling localized files into a single package requires that you release all assets in that package simultaneously, rather than being able to release each localization separately.</span></span> <span data-ttu-id="7425a-123">Ayrıca, herhangi bir yerelleştirme için herhangi bir güncelleştirme tüm paketin yeni bir sürümünü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="7425a-123">Furthermore, any update to any one localization requires a new version of the entire package.</span></span>

<span data-ttu-id="7425a-124">Ancak, aynı zamanda birkaç faydası vardır:</span><span class="sxs-lookup"><span data-stu-id="7425a-124">However, it also has a few benefits:</span></span>

1. <span data-ttu-id="7425a-125">**Basitlik**: Paketin tüketicileri, her dili ayrı ayrı yüklemek yerine desteklenen tüm dilleri tek bir yüklemede alır.</span><span class="sxs-lookup"><span data-stu-id="7425a-125">**Simplicity**: Consumers of the package get all supported languages in a single install, rather than having to install each language separately.</span></span> <span data-ttu-id="7425a-126">Tek bir paketi de nuget.org bulmak daha kolaydır.</span><span class="sxs-lookup"><span data-stu-id="7425a-126">A single package is also easier to find on nuget.org.</span></span>
1. <span data-ttu-id="7425a-127">**Birleştirilmiş sürümler**: Kaynak derlemelerinin tümü birincil derlemeyle aynı pakette olduğundan, hepsi aynı sürüm numarasını paylaşır ve hatalı bir şekilde ayrılma riskiyle karşı çıkmaz.</span><span class="sxs-lookup"><span data-stu-id="7425a-127">**Coupled versions**: Because all of the resource assemblies are in the same package as the primary assembly, they all share the same version number and don't run a risk of getting erroneously decoupled.</span></span>

## <a name="localized-satellite-packages"></a><span data-ttu-id="7425a-128">Yerelleştirilmiş uydu paketleri</span><span class="sxs-lookup"><span data-stu-id="7425a-128">Localized satellite packages</span></span>

<span data-ttu-id="7425a-129">.NET Framework'ün uydu derlemelerini desteklemesine benzer şekilde, bu yöntem yerelleştirilmiş kaynakları ve IntelliSense XML dosyalarını uydu paketlerine ayırır.</span><span class="sxs-lookup"><span data-stu-id="7425a-129">Similar to how .NET Framework supports satellite assemblies, this method separates localized resources and IntelliSense XML files into satellite packages.</span></span>

<span data-ttu-id="7425a-130">Bunu yapın, birincil paketiniz adlandırma `{identifier}.{version}.nupkg` kuralını kullanır ve varsayılan dil (en-US gibi) için derlemeyi içerir.</span><span class="sxs-lookup"><span data-stu-id="7425a-130">Do to this, your primary package uses the naming convention `{identifier}.{version}.nupkg` and contains the assembly for the default language (such as en-US).</span></span> <span data-ttu-id="7425a-131">Örneğin, `ContosoUtilities.1.0.0.nupkg` aşağıdaki yapıyı içerir:</span><span class="sxs-lookup"><span data-stu-id="7425a-131">For example, `ContosoUtilities.1.0.0.nupkg` would contain the following structure:</span></span>

    lib
    └───net40
            ContosoUtilities.dll
            ContosoUtilities.xml

<span data-ttu-id="7425a-132">Uydu derlemesi daha `{identifier}.{language}.{version}.nupkg`sonra adlandırma `ContosoUtilities.de.1.0.0.nupkg`kuralını kullanır, örneğin.</span><span class="sxs-lookup"><span data-stu-id="7425a-132">A satellite assembly then uses the naming convention `{identifier}.{language}.{version}.nupkg`, such as `ContosoUtilities.de.1.0.0.nupkg`.</span></span> <span data-ttu-id="7425a-133">Tanımlayıcı, birincil paketinkiyle tam olarak **eşleşmelidir.**</span><span class="sxs-lookup"><span data-stu-id="7425a-133">The identifier **must** exactly match that of the primary package.</span></span>

<span data-ttu-id="7425a-134">Bu ayrı bir paket olduğundan, `.nuspec` yerelleştirilmiş meta verileri içeren kendi dosyası vardır.</span><span class="sxs-lookup"><span data-stu-id="7425a-134">Because this is a separate package, it has its own `.nuspec` file that contains localized metadata.</span></span> <span data-ttu-id="7425a-135">Dosya adındaki `.nuspec` dilin dosya adındakullanılan dille **eşleşmesi gerektiğine** dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="7425a-135">Be mindful that the language in the `.nuspec` **must** match the one used in the filename.</span></span>

<span data-ttu-id="7425a-136">Uydu derlemesi ayrıca[] sürüm gösterimini kullanarak birincil paketin tam sürümünü bağımlılık olarak **bildirmelidir** (bkz. [Paket sürümü).](../concepts/package-versioning.md)</span><span class="sxs-lookup"><span data-stu-id="7425a-136">The satellite assembly **must** also declare an exact version of the primary package as a dependency, using the [] version notation (see [Package versioning](../concepts/package-versioning.md)).</span></span> <span data-ttu-id="7425a-137">Örneğin, `ContosoUtilities.de.1.0.0.nupkg` `ContosoUtilities.1.0.0.nupkg` `[1.0.0]` notasyonu kullanarak bir bağımlılık bildirmelidir.</span><span class="sxs-lookup"><span data-stu-id="7425a-137">For example, `ContosoUtilities.de.1.0.0.nupkg` must declare a dependency on `ContosoUtilities.1.0.0.nupkg` using the `[1.0.0]` notation.</span></span> <span data-ttu-id="7425a-138">Uydu paketi, tabii ki, birincil paket daha farklı bir sürüm numarası olabilir.</span><span class="sxs-lookup"><span data-stu-id="7425a-138">The satellite package can, of course, have a different version number than the primary package.</span></span>

<span data-ttu-id="7425a-139">Uydu paketinin yapısı daha sonra kaynak derlemesini ve XML IntelliSense `{language}` dosyasını paket dosya adıyla eşleşen bir alt klasöre içermelidir:</span><span class="sxs-lookup"><span data-stu-id="7425a-139">The satellite package's structure must then include the resource assembly and XML IntelliSense file in a subfolder that matches `{language}` in the package filename:</span></span>

    lib
    └───net40
        └───de
                ContosoUtilities.resources.dll
                ContosoUtilities.xml

<span data-ttu-id="7425a-140">**Not**: Gibi `ja-JP` belirli alt kültürler gerekli olmadıkça, her zaman gibi `ja`daha yüksek düzey dil tanımlayıcısı kullanın.</span><span class="sxs-lookup"><span data-stu-id="7425a-140">**Note**: unless specific subcultures such as `ja-JP` are necessary, always use the higher level language identifier, like `ja`.</span></span>

<span data-ttu-id="7425a-141">Uydu derlemesinde, NuGet **yalnızca** dosya `{language}` adıyla eşleşen klasördeki dosyaları tanır.</span><span class="sxs-lookup"><span data-stu-id="7425a-141">In a satellite assembly, NuGet will recognize **only** those files in the folder that matches the `{language}` in the filename.</span></span> <span data-ttu-id="7425a-142">Diğerleri göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="7425a-142">All others are ignored.</span></span>

<span data-ttu-id="7425a-143">Tüm bu kurallar karşılandığında, NuGet paketi uydu paketi olarak tanıyacak ve yerelleştirilmiş dosyaları `lib` ilk olarak paketlenmiş gibi birincil paketin klasörüne yükler.</span><span class="sxs-lookup"><span data-stu-id="7425a-143">When all of these conventions are met, NuGet will recognize the package as a satellite package and install the localized files into the primary package's `lib` folder, as if they had been originally bundled.</span></span> <span data-ttu-id="7425a-144">Uydu paketini kaldırmak, dosyalarını aynı klasörden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="7425a-144">Uninstalling the satellite package will remove its files from that same folder.</span></span>

<span data-ttu-id="7425a-145">Desteklenen her dil için aynı şekilde ek uydu derlemeleri oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="7425a-145">You would create additional satellite assemblies in the same way for each supported language.</span></span> <span data-ttu-id="7425a-146">Örneğin, ASP.NET MVC paketleri kümesini inceleyin:</span><span class="sxs-lookup"><span data-stu-id="7425a-146">For an example, examine the set of ASP.NET MVC packages:</span></span>

- <span data-ttu-id="7425a-147">[Microsoft.AspNet.Mvc](https://nuget.org/packages/Microsoft.AspNet.Mvc) (İngilizce birincil)</span><span class="sxs-lookup"><span data-stu-id="7425a-147">[Microsoft.AspNet.Mvc](https://nuget.org/packages/Microsoft.AspNet.Mvc) (English primary)</span></span>
- <span data-ttu-id="7425a-148">[Microsoft.AspNet.Mvc.de](https://nuget.org/packages/Microsoft.AspNet.Mvc.de) (Almanca)</span><span class="sxs-lookup"><span data-stu-id="7425a-148">[Microsoft.AspNet.Mvc.de](https://nuget.org/packages/Microsoft.AspNet.Mvc.de) (German)</span></span>
- <span data-ttu-id="7425a-149">[Microsoft.AspNet.Mvc.ja](https://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (Japonca)</span><span class="sxs-lookup"><span data-stu-id="7425a-149">[Microsoft.AspNet.Mvc.ja](https://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (Japanese)</span></span>
- <span data-ttu-id="7425a-150">[Microsoft.AspNet.Mvc.zh-Hans](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (Çince (Basitleştirilmiş))</span><span class="sxs-lookup"><span data-stu-id="7425a-150">[Microsoft.AspNet.Mvc.zh-Hans](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (Chinese (Simplified))</span></span>
- <span data-ttu-id="7425a-151">[Microsoft.AspNet.Mvc.zh-Hant](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (Çince (Geleneksel))</span><span class="sxs-lookup"><span data-stu-id="7425a-151">[Microsoft.AspNet.Mvc.zh-Hant](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (Chinese (Traditional))</span></span>

### <a name="summary-of-required-conventions"></a><span data-ttu-id="7425a-152">Gerekli sözleşmelerin özeti</span><span class="sxs-lookup"><span data-stu-id="7425a-152">Summary of required conventions</span></span>

- <span data-ttu-id="7425a-153">Birincil paket adlandırılmalıdır`{identifier}.{version}.nupkg`</span><span class="sxs-lookup"><span data-stu-id="7425a-153">Primary package must be named `{identifier}.{version}.nupkg`</span></span>
- <span data-ttu-id="7425a-154">Bir uydu paketi adlandırılmalıdır`{identifier}.{language}.{version}.nupkg`</span><span class="sxs-lookup"><span data-stu-id="7425a-154">A satellite package must be named `{identifier}.{language}.{version}.nupkg`</span></span>
- <span data-ttu-id="7425a-155">Uydu paketinin `.nuspec` dosya adıyla eşleşecek dilini belirtmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="7425a-155">A satellite package's `.nuspec` must specify its language to match the filename.</span></span>
- <span data-ttu-id="7425a-156">Uydu paketi, `.nuspec` dosyasındaki [] gösterimini kullanarak birincil ürünün tam sürümüne bağımlılık beyan etmelidir.</span><span class="sxs-lookup"><span data-stu-id="7425a-156">A satellite package must declare a dependency on an exact version of the primary using the [] notation in its `.nuspec` file.</span></span> <span data-ttu-id="7425a-157">Aralıklar desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="7425a-157">Ranges are not supported.</span></span>
- <span data-ttu-id="7425a-158">Uydu paketi, dosya adına `lib\[{framework}\]{language}` tam olarak `{language}` uyan dosyaları klasöre yerleştirmelidir.</span><span class="sxs-lookup"><span data-stu-id="7425a-158">A satellite package must place files in the `lib\[{framework}\]{language}` folder that exactly matches `{language}` in the filename.</span></span>

### <a name="advantages-and-disadvantages-satellite-packages"></a><span data-ttu-id="7425a-159">Avantajları ve dezavantajları (uydu paketleri)</span><span class="sxs-lookup"><span data-stu-id="7425a-159">Advantages and disadvantages (satellite packages)</span></span>

<span data-ttu-id="7425a-160">Uydu paketlerinin kullanılmasının birkaç faydası vardır:</span><span class="sxs-lookup"><span data-stu-id="7425a-160">Using satellite packages has a few benefits:</span></span>

1. <span data-ttu-id="7425a-161">**Paket boyutu**: Birincil paketin genel ayak izi en aza indirgendi ve tüketiciler yalnızca kullanmak istedikleri her dilin maliyetine maruz kaldılar.</span><span class="sxs-lookup"><span data-stu-id="7425a-161">**Package size**: The overall footprint of the primary package is minimized, and consumers only incur the costs of each language they want to use.</span></span>
1. <span data-ttu-id="7425a-162">**Ayrı meta veriler**: Her `.nuspec` uydu paketinin kendi dosyası ve dolayısıyla kendi yerelleştirilmiş meta verileri vardır çünkü.</span><span class="sxs-lookup"><span data-stu-id="7425a-162">**Separate metadata**: Each satellite package has its own `.nuspec` file and thus its own localized metadata because.</span></span> <span data-ttu-id="7425a-163">Bu, bazı tüketicilerin yerelleştirilmiş terimlerle nuget.org arayarak paketleri daha kolay bulmalarını sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="7425a-163">This can allow some consumers to find packages more easily by searching nuget.org with localized terms.</span></span>
1. <span data-ttu-id="7425a-164">**Ayrılmış sürümler**: Uydu derlemeleri zaman içinde, hepsi bir kerede değil, serbest bırakılabilir ve yerelleştirme çabalarınızı yaymanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="7425a-164">**Decoupled releases**: Satellite assemblies can be released over time, rather than all at once, allowing you to spread out your localization efforts.</span></span>

<span data-ttu-id="7425a-165">Ancak, uydu paketlerinin kendi dezavantajları vardır:</span><span class="sxs-lookup"><span data-stu-id="7425a-165">However, satellite packages have their own set of disadvantages:</span></span>

1. <span data-ttu-id="7425a-166">**Yığılmayı**: Tek bir paket yerine, nuget.org'da karmaşık arama sonuçlarına ve Visual Studio projesinde uzun bir referans listesine yol açabilecek birçok paketiniz var.</span><span class="sxs-lookup"><span data-stu-id="7425a-166">**Clutter**: Instead of a single package, you have many packages that can lead to cluttered search results on nuget.org and a long list of references in a Visual Studio project.</span></span>
1. <span data-ttu-id="7425a-167">**Katı kurallar.**</span><span class="sxs-lookup"><span data-stu-id="7425a-167">**Strict conventions**.</span></span> <span data-ttu-id="7425a-168">Uydu paketleri nin kurallara tam olarak uyması gerekir veya yerelleştirilmiş sürümler düzgün olarak alınmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="7425a-168">Satellite packages must follow the conventions exactly or the localized versions won't be picked up properly.</span></span>
1. <span data-ttu-id="7425a-169">**Sürüm :** Her uydu paketinin birincil pakete tam bir sürüm bağımlılığı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7425a-169">**Versioning**: Each satellite package must have an exact version dependency on the primary package.</span></span> <span data-ttu-id="7425a-170">Bu, kaynaklar değişmemiş olsa bile birincil paketin güncelleştirilmesi nin tüm uydu paketlerinin güncelleştirilmesini gerektirebileceği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="7425a-170">This means that updating the primary package may require updating all satellite packages as well, even if the resources didn't change.</span></span>
