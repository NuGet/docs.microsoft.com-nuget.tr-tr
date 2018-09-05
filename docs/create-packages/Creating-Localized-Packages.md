---
title: Yerelleştirilmiş bir NuGet paketi oluşturma
description: Tek bir pakette tüm derlemelerin dahil olmak üzere veya ayrı derlemeler yayımlama NuGet paketleri oluşturmanın iki yolu hakkında ayrıntılı bilgi yerelleştirilmiş.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: b1c2511c1fbafc7f52029c23521fa55671b0b5c5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546901"
---
# <a name="creating-localized-nuget-packages"></a><span data-ttu-id="4af28-103">Yerelleştirilmiş NuGet paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="4af28-103">Creating localized NuGet packages</span></span>

<span data-ttu-id="4af28-104">Bir kitaplık yerelleştirilmiş sürümlerini oluşturmak için iki yol vardır:</span><span class="sxs-lookup"><span data-stu-id="4af28-104">There are two ways to create localized versions of a library:</span></span>

1. <span data-ttu-id="4af28-105">Tüm yerelleştirilmiş kaynaklar derlemelere tek bir pakette içerir.</span><span class="sxs-lookup"><span data-stu-id="4af28-105">Include all localized resources assemblies in a single package.</span></span>
1. <span data-ttu-id="4af28-106">Kuralları katı bir dizi ayrı yerelleştirilmiş uydu paketleri oluşturma.</span><span class="sxs-lookup"><span data-stu-id="4af28-106">Create separate localized satellite packages by following a strict set of conventions.</span></span>

<span data-ttu-id="4af28-107">Aşağıdaki bölümlerde açıklandığı gibi avantajları ve dezavantajları, iki yöntem de sahiptir.</span><span class="sxs-lookup"><span data-stu-id="4af28-107">Both methods have their advantages and disadvantages, as described in the following sections.</span></span>

## <a name="localized-resource-assemblies-in-a-single-package"></a><span data-ttu-id="4af28-108">Tek bir paket içinde yerelleştirilmiş kaynak derlemeleri</span><span class="sxs-lookup"><span data-stu-id="4af28-108">Localized resource assemblies in a single package</span></span>

<span data-ttu-id="4af28-109">Tek bir paket içinde yerelleştirilmiş kaynak derlemeleri de dahil olmak üzere genellikle en basit yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="4af28-109">Including localized resource assemblies in a single package is typically the simplest approach.</span></span> <span data-ttu-id="4af28-110">Bunu yapmak için klasörler oluşturma `lib` için desteklenen dil paketi varsayılan dışındaki (tr varsayılır-us).</span><span class="sxs-lookup"><span data-stu-id="4af28-110">To do this, create folders within `lib` for supported language other than the package default (assumed to be en-us).</span></span> <span data-ttu-id="4af28-111">Bu klasörlerde kaynak derlemeleri ve yerelleştirilmiş IntelliSense XML dosyaları yerleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4af28-111">In these folders you can place resource assemblies and localized IntelliSense XML files.</span></span>

<span data-ttu-id="4af28-112">Örneğin, aşağıdaki klasör yapısını destekler, Almanca (de), İtalyanca (,), Japonca (ja), Rusça (ru), Çince (Basitleştirilmiş) (zh-Hans) ve Çince (Geleneksel) (zh-Hant):</span><span class="sxs-lookup"><span data-stu-id="4af28-112">For example, the following folder structure supports, German (de), Italian (it), Japanese (ja), Russian (ru), Chinese (Simplified) (zh-Hans), and Chinese (Traditional) (zh-Hant):</span></span>

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

<span data-ttu-id="4af28-113">Dilleri tüm altında listelendiğini gördüğünüz `net40` hedef çerçeve klasörü.</span><span class="sxs-lookup"><span data-stu-id="4af28-113">You can see that the languages are all listed underneath the `net40` target framework folder.</span></span> <span data-ttu-id="4af28-114">Size [birden çok çerçeveyi destekleme](../create-packages/supporting-multiple-target-frameworks.md), altında bir klasöre sahip `lib` her değişken için.</span><span class="sxs-lookup"><span data-stu-id="4af28-114">If you're [supporting multiple frameworks](../create-packages/supporting-multiple-target-frameworks.md), then you have a folder under `lib` for each variant.</span></span>

<span data-ttu-id="4af28-115">Bu klasörleri yerinde sonra tüm dosyaları başvuru, `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="4af28-115">With these folders in place, you then reference all the files in your `.nuspec`:</span></span>

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

<span data-ttu-id="4af28-116">Bu yaklaşım kullanan bir örnek paket [Microsoft.Data.OData 5.4.0](http://nuget.org/packages/Microsoft.Data.OData/5.4.0).</span><span class="sxs-lookup"><span data-stu-id="4af28-116">One example package that uses this approach is [Microsoft.Data.OData 5.4.0](http://nuget.org/packages/Microsoft.Data.OData/5.4.0).</span></span>

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a><span data-ttu-id="4af28-117">Avantajlar ve dezavantajlar (yerelleştirilmiş kaynak bütünleştirilmiş kodları)</span><span class="sxs-lookup"><span data-stu-id="4af28-117">Advantages and disadvantages (localized resource assemblies)</span></span>

<span data-ttu-id="4af28-118">Tüm diller, tek bir pakette paketleme bazı dezavantajları vardır:</span><span class="sxs-lookup"><span data-stu-id="4af28-118">Bundling all languages in a single package has a few disadvantages:</span></span>

1. <span data-ttu-id="4af28-119">**Meta veri paylaşılan**: yalnızca tek bir NuGet paketi içerebileceğinden `.nuspec` dosyası, yalnızca tek bir dil için meta verileri sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4af28-119">**Shared metadata**: Because a NuGet package can only contain a single `.nuspec` file, you can provide metadata for only a single language.</span></span> <span data-ttu-id="4af28-120">Diğer bir deyişle, NuGet desteği yerelleştirilmiş meta verileri sunmaz.</span><span class="sxs-lookup"><span data-stu-id="4af28-120">That is, NuGet does not present support localized metadata.</span></span>
1. <span data-ttu-id="4af28-121">**Paket boyutu**: desteklediğiniz dilleri sayısına bağlı olarak, kitaplık, yükleme ve paket geri yükleme yavaşlatır önemli ölçüde büyük olabilir.</span><span class="sxs-lookup"><span data-stu-id="4af28-121">**Package size**: Depending on the number of languages you support, the library can become considerably large, which slows installing and restoring the package.</span></span>
1. <span data-ttu-id="4af28-122">**Eşzamanlı yayınlar**: tek bir pakete yerelleştirilmiş dosyaları paketleme gerektirir, bu paket grubundaki tüm varlıkları eşzamanlı olarak ayrı ayrı her bir yerelleştirme yayınlayabilir olmak yerine yayın.</span><span class="sxs-lookup"><span data-stu-id="4af28-122">**Simultaneous releases**: Bundling localized files into a single package requires that you release all assets in that package simultaneously, rather than being able to release each localization separately.</span></span> <span data-ttu-id="4af28-123">Ayrıca, herhangi bir yerelleştirme için herhangi bir güncelleştirme tüm paketin yeni bir sürümü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="4af28-123">Furthermore, any update to any one localization requires a new version of the entire package.</span></span>

<span data-ttu-id="4af28-124">Bununla birlikte, bazı avantajları da vardır:</span><span class="sxs-lookup"><span data-stu-id="4af28-124">However, it also has a few benefits:</span></span>

1. <span data-ttu-id="4af28-125">**Basitlik**: desteklenen tüm dillerde ayrı ayrı her bir dil yüklemek zorunda yerine tek bir yükleme paketi tüketicileri alın.</span><span class="sxs-lookup"><span data-stu-id="4af28-125">**Simplicity**: Consumers of the package get all supported languages in a single install, rather than having to install each language separately.</span></span> <span data-ttu-id="4af28-126">Tek bir pakette de nuget.org adresinden bulmak daha kolay olur.</span><span class="sxs-lookup"><span data-stu-id="4af28-126">A single package is also easier to find on nuget.org.</span></span>
1. <span data-ttu-id="4af28-127">**Sürümleri eşleşmiş**: tüm kaynak derlemeler birincil derlemeyle aynı pakette olduğundan, bunların tümü aynı sürüm numarasını paylaşır ve deneyebileceğinizi ayrılmış riskini çalıştırmayın.</span><span class="sxs-lookup"><span data-stu-id="4af28-127">**Coupled versions**: Because all of the resource assemblies are in the same package as the primary assembly, they all share the same version number and don't run a risk of getting erroneously decoupled.</span></span>

## <a name="localized-satellite-packages"></a><span data-ttu-id="4af28-128">Yerelleştirilmiş uydu paketleri</span><span class="sxs-lookup"><span data-stu-id="4af28-128">Localized satellite packages</span></span>

<span data-ttu-id="4af28-129">Benzer şekilde nasıl .NET Framework uydu derlemelerini destekler, bu yöntem yerelleştirilmiş kaynaklar ve IntelliSense XML dosyalarını uydu paketler ayırır.</span><span class="sxs-lookup"><span data-stu-id="4af28-129">Similar to how .NET Framework supports satellite assemblies, this method separates localized resources and IntelliSense XML files into satellite packages.</span></span>

<span data-ttu-id="4af28-130">Bunun için birincil paketinizi adlandırma kuralını kullanır `{identifier}.{version}.nupkg` ve derleme için varsayılan dil (örneğin, en-US) içerir.</span><span class="sxs-lookup"><span data-stu-id="4af28-130">Do to this, your primary package uses the naming convention `{identifier}.{version}.nupkg` and contains the assembly for the default language (such as en-US).</span></span> <span data-ttu-id="4af28-131">Örneğin, `ContosoUtilities.1.0.0.nupkg` aşağıdaki yapısını içerir:</span><span class="sxs-lookup"><span data-stu-id="4af28-131">For example, `ContosoUtilities.1.0.0.nupkg` would contain the following structure:</span></span>

    lib
    └───net40
            ContosoUtilities.dll
            ContosoUtilities.xml

<span data-ttu-id="4af28-132">Ardından bir uydu derleme adlandırma kuralını kullanır `{identifier}.{language}.{version}.nupkg`, gibi `ContosoUtilities.de.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="4af28-132">A satellite assembly then uses the naming convention `{identifier}.{language}.{version}.nupkg`, such as `ContosoUtilities.de.1.0.0.nupkg`.</span></span> <span data-ttu-id="4af28-133">Tanımlayıcı **gerekir** birincil paketi tam olarak eşleşmesi.</span><span class="sxs-lookup"><span data-stu-id="4af28-133">The identifier **must** exactly match that of the primary package.</span></span>

<span data-ttu-id="4af28-134">Bu ayrı bir paket olduğundan, kendi yoktur `.nuspec` yerelleştirilmiş meta veriler içeren dosya.</span><span class="sxs-lookup"><span data-stu-id="4af28-134">Because this is a separate package, it has its own `.nuspec` file that contains localized metadata.</span></span> <span data-ttu-id="4af28-135">Dikkatli olmanızı bu dilde `.nuspec` **gerekir** dosya adında kullanılanla eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="4af28-135">Be mindful that the language in the `.nuspec` **must** match the one used in the filename.</span></span>

<span data-ttu-id="4af28-136">Uydu derlemesi **gerekir** ayrıca birincil paketi tam bir sürümünü [] sürümü gösterimini kullanarak bir bağımlılık olarak bildirin (bkz [Paket sürümü oluşturma](../reference/package-versioning.md)).</span><span class="sxs-lookup"><span data-stu-id="4af28-136">The satellite assembly **must** also declare an exact version of the primary package as a dependency, using the [] version notation (see [Package versioning](../reference/package-versioning.md)).</span></span> <span data-ttu-id="4af28-137">Örneğin, `ContosoUtilities.de.1.0.0.nupkg` bağımlılık bildirmeniz gerekir `ContosoUtilities.1.0.0.nupkg` kullanarak `[1.0.0]` gösterimi.</span><span class="sxs-lookup"><span data-stu-id="4af28-137">For example, `ContosoUtilities.de.1.0.0.nupkg` must declare a dependency on `ContosoUtilities.1.0.0.nupkg` using the `[1.0.0]` notation.</span></span> <span data-ttu-id="4af28-138">Elbette, uydu paket birincil paketi farklı bir sürüm numarasından olabilir.</span><span class="sxs-lookup"><span data-stu-id="4af28-138">The satellite package can, of course, have a different version number than the primary package.</span></span>

<span data-ttu-id="4af28-139">Uydu paket yapısı sonra kaynak derleme ve IntelliSense XML dosyası ile eşleşen bir alt içermelidir `{language}` paket dosya:</span><span class="sxs-lookup"><span data-stu-id="4af28-139">The satellite package's structure must then include the resource assembly and XML IntelliSense file in a subfolder that matches `{language}` in the package filename:</span></span>

    lib
    └───net40
        └───de
                ContosoUtilities.resources.dll
                ContosoUtilities.xml

<span data-ttu-id="4af28-140">**Not**: sürece gibi belirli subcultures `ja-JP` gerekliyse, her zaman daha yüksek düzey bir dil tanımlayıcısı, gibi kullanın `ja`.</span><span class="sxs-lookup"><span data-stu-id="4af28-140">**Note**: unless specific subcultures such as `ja-JP` are necessary, always use the higher level language identifier, like `ja`.</span></span>

<span data-ttu-id="4af28-141">Bir uydu derlemesine NuGet tanıyacağınız **yalnızca** eşleşen klasöründeki dosyalarla `{language}` dosya adında.</span><span class="sxs-lookup"><span data-stu-id="4af28-141">In a satellite assembly, NuGet will recognize **only** those files in the folder that matches the `{language}` in the filename.</span></span> <span data-ttu-id="4af28-142">Diğerleri yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="4af28-142">All others are ignored.</span></span>

<span data-ttu-id="4af28-143">Tüm bu kuralları karşılandığında, NuGet paketi bir uydu paketi olarak tanınması ve birincil pakete ait yerelleştirilmiş dosyaları yüklemek `lib` klasör gibi bunlar ilk olarak toplanmış.</span><span class="sxs-lookup"><span data-stu-id="4af28-143">When all of these conventions are met, NuGet will recognize the package as a satellite package and install the localized files into the primary package's `lib` folder, as if they had been originally bundled.</span></span> <span data-ttu-id="4af28-144">Uydu paketi dosyalarını aynı bu klasörden kaldırın.</span><span class="sxs-lookup"><span data-stu-id="4af28-144">Uninstalling the satellite package will remove its files from that same folder.</span></span>

<span data-ttu-id="4af28-145">Desteklenen her dil için aynı şekilde ek uydu derlemeleri oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="4af28-145">You would create additional satellite assemblies in the same way for each supported language.</span></span> <span data-ttu-id="4af28-146">Örneğin, ASP.NET MVC paketleri kümesini inceleyin:</span><span class="sxs-lookup"><span data-stu-id="4af28-146">For an example, examine the set of ASP.NET MVC packages:</span></span>

- <span data-ttu-id="4af28-147">[Microsoft.AspNet.Mvc](http://nuget.org/packages/Microsoft.AspNet.Mvc) (İngilizce birincil)</span><span class="sxs-lookup"><span data-stu-id="4af28-147">[Microsoft.AspNet.Mvc](http://nuget.org/packages/Microsoft.AspNet.Mvc) (English primary)</span></span>
- <span data-ttu-id="4af28-148">[Microsoft.AspNet.Mvc.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.de) (Almanya)</span><span class="sxs-lookup"><span data-stu-id="4af28-148">[Microsoft.AspNet.Mvc.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.de) (German)</span></span>
- <span data-ttu-id="4af28-149">[Microsoft.AspNet.Mvc.ja](http://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (Japonca)</span><span class="sxs-lookup"><span data-stu-id="4af28-149">[Microsoft.AspNet.Mvc.ja](http://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (Japanese)</span></span>
- <span data-ttu-id="4af28-150">[Microsoft.AspNet.Mvc.zh Hans](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (Çince (Basitleştirilmiş))</span><span class="sxs-lookup"><span data-stu-id="4af28-150">[Microsoft.AspNet.Mvc.zh-Hans](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (Chinese (Simplified))</span></span>
- <span data-ttu-id="4af28-151">[Microsoft.AspNet.Mvc.zh Hant](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (Çince (Geleneksel))</span><span class="sxs-lookup"><span data-stu-id="4af28-151">[Microsoft.AspNet.Mvc.zh-Hant](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (Chinese (Traditional))</span></span>

### <a name="summary-of-required-conventions"></a><span data-ttu-id="4af28-152">Gerekli kuralları özeti</span><span class="sxs-lookup"><span data-stu-id="4af28-152">Summary of required conventions</span></span>

- <span data-ttu-id="4af28-153">Birincil paketi olarak adlandırılmalıdır `{identifier}.{version}.nupkg`</span><span class="sxs-lookup"><span data-stu-id="4af28-153">Primary package must be named `{identifier}.{version}.nupkg`</span></span>
- <span data-ttu-id="4af28-154">Uydu paket olarak adlandırılmalıdır `{identifier}.{language}.{version}.nupkg`</span><span class="sxs-lookup"><span data-stu-id="4af28-154">A satellite package must be named `{identifier}.{language}.{version}.nupkg`</span></span>
- <span data-ttu-id="4af28-155">Uydu paketin `.nuspec` dosya adını eşleştirmek için dili belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4af28-155">A satellite package's `.nuspec` must specify its language to match the filename.</span></span>
- <span data-ttu-id="4af28-156">[] Gösterim kullanılarak birincil tam bir sürümünü bir uydu paketi bir bağımlılık bildirmeniz gerekir, `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="4af28-156">A satellite package must declare a dependency on an exact version of the primary using the [] notation in its `.nuspec` file.</span></span> <span data-ttu-id="4af28-157">Aralıkları desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="4af28-157">Ranges are not supported.</span></span>
- <span data-ttu-id="4af28-158">Uydu paket dosyaları yerleştirmelisiniz `lib\[{framework}\]{language}` tam olarak eşleşen bir klasör `{language}` dosya adında.</span><span class="sxs-lookup"><span data-stu-id="4af28-158">A satellite package must place files in the `lib\[{framework}\]{language}` folder that exactly matches `{language}` in the filename.</span></span>

### <a name="advantages-and-disadvantages-satellite-packages"></a><span data-ttu-id="4af28-159">Avantajlar ve dezavantajlar (uydu paketler)</span><span class="sxs-lookup"><span data-stu-id="4af28-159">Advantages and disadvantages (satellite packages)</span></span>

<span data-ttu-id="4af28-160">Uydu paketlerini kullanma, bazı avantajları vardır:</span><span class="sxs-lookup"><span data-stu-id="4af28-160">Using satellite packages has a few benefits:</span></span>

1. <span data-ttu-id="4af28-161">**Paket boyutu**: birincil paketin bütün kapladığı alanı en aza indirilir ve tüketiciler yalnızca, kullanmak istediğiniz her bir dilin maliyetleri doğurur.</span><span class="sxs-lookup"><span data-stu-id="4af28-161">**Package size**: The overall footprint of the primary package is minimized, and consumers only incur the costs of each language they want to use.</span></span>
1. <span data-ttu-id="4af28-162">**Ayrı bir meta veri**: her bir uydu paketi kendi bölümüne sahiptir `.nuspec` dosya ve bu nedenle kendi yerelleştirilmiş meta verileri için.</span><span class="sxs-lookup"><span data-stu-id="4af28-162">**Separate metadata**: Each satellite package has its own `.nuspec` file and thus its own localized metadata because.</span></span> <span data-ttu-id="4af28-163">Bu paketleri nuget.org yerelleştirilmiş koşullarıyla arayarak daha kolay bulmak bazı tüketiciler izin verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4af28-163">This can allow some consumers to find packages more easily by searching nuget.org with localized terms.</span></span>
1. <span data-ttu-id="4af28-164">**Ayrılmış yayınlar**: uydu derlemeleri serbest bırakılabilir zamanla yerine tümünü tek seferde yerelleştirme çalışmalarınızı yayılan etmenize imkan sağlar.</span><span class="sxs-lookup"><span data-stu-id="4af28-164">**Decoupled releases**: Satellite assemblies can be released over time, rather than all at once, allowing you to spread out your localization efforts.</span></span>

<span data-ttu-id="4af28-165">Ancak, uydu paketleri kendi dezavantajları vardır:</span><span class="sxs-lookup"><span data-stu-id="4af28-165">However, satellite packages have their own set of disadvantages:</span></span>

1. <span data-ttu-id="4af28-166">**Dağınıklığı**: tek bir paket yerine derli toplu arama sonuçlarını nuget.org ve Visual Studio projede başvuruları uzun listesi yol açabilecek birçok paketleri vardır.</span><span class="sxs-lookup"><span data-stu-id="4af28-166">**Clutter**: Instead of a single package, you have many packages that can lead to cluttered search results on nuget.org and a long list of references in a Visual Studio project.</span></span>
1. <span data-ttu-id="4af28-167">**Katı kuralları**.</span><span class="sxs-lookup"><span data-stu-id="4af28-167">**Strict conventions**.</span></span> <span data-ttu-id="4af28-168">Uydu paketleri tam olarak kurallarına uymalıdır veya yerelleştirilmiş sürümleri düzgün çekilmesi olmaz.</span><span class="sxs-lookup"><span data-stu-id="4af28-168">Satellite packages must follow the conventions exactly or the localized versions won't be picked up properly.</span></span>
1. <span data-ttu-id="4af28-169">**Sürüm oluşturma**: her bir uydu paketi birincil paketi bir tam sürüme bağımlılığı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4af28-169">**Versioning**: Each satellite package must have an exact version dependency on the primary package.</span></span> <span data-ttu-id="4af28-170">Kaynakları değişmedi olsa bile bu birincil paketi güncelleştirme de tüm uydu paketlerin güncelleştirilmesi gerektiğini anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="4af28-170">This means that updating the primary package may require updating all satellite packages as well, even if the resources didn't change.</span></span>
