---
title: Yerelleştirilmiş bir NuGet paketi oluşturma
description: Tüm derlemeleri tek bir pakette ekleyerek veya ayrı derlemeler yayımlayarak yerelleştirilmiş NuGet paketleri oluşturmanın iki yolu hakkında ayrıntılı bilgi.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 83414a824676844f9e44eab874e5eac788d50583
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610947"
---
# <a name="creating-localized-nuget-packages"></a><span data-ttu-id="a34ce-103">Yerelleştirilmiş NuGet paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="a34ce-103">Creating localized NuGet packages</span></span>

<span data-ttu-id="a34ce-104">Bir kitaplığın yerelleştirilmiş sürümlerini oluşturmanın iki yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="a34ce-104">There are two ways to create localized versions of a library:</span></span>

1. <span data-ttu-id="a34ce-105">Tüm yerelleştirilmiş kaynaklar derlemelerini tek bir pakete dahil edin.</span><span class="sxs-lookup"><span data-stu-id="a34ce-105">Include all localized resources assemblies in a single package.</span></span>
1. <span data-ttu-id="a34ce-106">Katı bir kural kümesini izleyerek ayrı yerelleştirilmiş uydu paketleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a34ce-106">Create separate localized satellite packages by following a strict set of conventions.</span></span>

<span data-ttu-id="a34ce-107">Her iki yöntem de aşağıdaki bölümlerde açıklandığı gibi avantajları ve dezavantajları vardır.</span><span class="sxs-lookup"><span data-stu-id="a34ce-107">Both methods have their advantages and disadvantages, as described in the following sections.</span></span>

## <a name="localized-resource-assemblies-in-a-single-package"></a><span data-ttu-id="a34ce-108">Tek bir pakette yerelleştirilmiş kaynak derlemeleri</span><span class="sxs-lookup"><span data-stu-id="a34ce-108">Localized resource assemblies in a single package</span></span>

<span data-ttu-id="a34ce-109">Yerelleştirilmiş kaynak derlemelerini tek bir pakette içermek genellikle en basit yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="a34ce-109">Including localized resource assemblies in a single package is typically the simplest approach.</span></span> <span data-ttu-id="a34ce-110">Bunu yapmak için `lib` içinde, paket varsayılanı dışında (en-US olarak kabul edilir) desteklenen dil için klasörler oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a34ce-110">To do this, create folders within `lib` for supported language other than the package default (assumed to be en-us).</span></span> <span data-ttu-id="a34ce-111">Bu klasörlerde, kaynak derlemelerini ve yerelleştirilmiş IntelliSense XML dosyalarını yerleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a34ce-111">In these folders you can place resource assemblies and localized IntelliSense XML files.</span></span>

<span data-ttu-id="a34ce-112">Örneğin, aşağıdaki klasör yapısı, Almanca (de), Italyanca (It), Japonca (ja), Rusça (ru), Çince (Basitleştirilmiş) (zh-Hans) ve Çince (Geleneksel) (zh-Hant) destekler:</span><span class="sxs-lookup"><span data-stu-id="a34ce-112">For example, the following folder structure supports, German (de), Italian (it), Japanese (ja), Russian (ru), Chinese (Simplified) (zh-Hans), and Chinese (Traditional) (zh-Hant):</span></span>

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

<span data-ttu-id="a34ce-113">Dillerin tümünün `net40` Target Framework klasörünün altında listelendiğini görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a34ce-113">You can see that the languages are all listed underneath the `net40` target framework folder.</span></span> <span data-ttu-id="a34ce-114">[Birden çok çerçeveyi destekliyorsanız](../create-packages/supporting-multiple-target-frameworks.md), her çeşit için `lib` altında bir klasörünüz vardır.</span><span class="sxs-lookup"><span data-stu-id="a34ce-114">If you're [supporting multiple frameworks](../create-packages/supporting-multiple-target-frameworks.md), then you have a folder under `lib` for each variant.</span></span>

<span data-ttu-id="a34ce-115">Bu klasörlerle birlikte, `.nuspec`tüm dosyalara başvurun:</span><span class="sxs-lookup"><span data-stu-id="a34ce-115">With these folders in place, you then reference all the files in your `.nuspec`:</span></span>

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

<span data-ttu-id="a34ce-116">Bu yaklaşımı kullanan bir örnek paket, [Microsoft. Data. OData 5.4.0](https://nuget.org/packages/Microsoft.Data.OData/5.4.0).</span><span class="sxs-lookup"><span data-stu-id="a34ce-116">One example package that uses this approach is [Microsoft.Data.OData 5.4.0](https://nuget.org/packages/Microsoft.Data.OData/5.4.0).</span></span>

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a><span data-ttu-id="a34ce-117">Avantajlar ve dezavantajlar (yerelleştirilen kaynak derlemeleri)</span><span class="sxs-lookup"><span data-stu-id="a34ce-117">Advantages and disadvantages (localized resource assemblies)</span></span>

<span data-ttu-id="a34ce-118">Tek bir paketteki tüm dillerin paket, birkaç dezavantaja sahiptir:</span><span class="sxs-lookup"><span data-stu-id="a34ce-118">Bundling all languages in a single package has a few disadvantages:</span></span>

1. <span data-ttu-id="a34ce-119">**Paylaşılan meta veriler**: bir NuGet paketi yalnızca tek bir `.nuspec` dosyası içerebildiğinden, meta verileri yalnızca tek bir dil için sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a34ce-119">**Shared metadata**: Because a NuGet package can only contain a single `.nuspec` file, you can provide metadata for only a single language.</span></span> <span data-ttu-id="a34ce-120">Diğer bir deyişle, NuGet yerelleştirilmiş meta verileri desteklemez ' i sunmaz.</span><span class="sxs-lookup"><span data-stu-id="a34ce-120">That is, NuGet does not present support localized metadata.</span></span>
1. <span data-ttu-id="a34ce-121">**Paket boyutu**: desteklemenizin dil sayısına bağlı olarak, kitaplık önemli ölçüde büyük olabilir ve bu da paketi yüklemeyi ve geri yüklemeyi yavaşlatır.</span><span class="sxs-lookup"><span data-stu-id="a34ce-121">**Package size**: Depending on the number of languages you support, the library can become considerably large, which slows installing and restoring the package.</span></span>
1. <span data-ttu-id="a34ce-122">**Eşzamanlı yayınlar**: yerelleştirilmiş dosyaları tek bir pakette paketleme, her yerelleştirmeyi ayrı olarak serbest bırakmak yerine, bu paketteki tüm varlıkları aynı anda serbest bırakmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a34ce-122">**Simultaneous releases**: Bundling localized files into a single package requires that you release all assets in that package simultaneously, rather than being able to release each localization separately.</span></span> <span data-ttu-id="a34ce-123">Ayrıca, herhangi bir Yerelleştirmede yapılan herhangi bir güncelleştirme paketin tamamının yeni bir sürümünü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="a34ce-123">Furthermore, any update to any one localization requires a new version of the entire package.</span></span>

<span data-ttu-id="a34ce-124">Bununla birlikte, Ayrıca birkaç avantaj de vardır:</span><span class="sxs-lookup"><span data-stu-id="a34ce-124">However, it also has a few benefits:</span></span>

1. <span data-ttu-id="a34ce-125">**Basitlik**: paketin tüketicileri, her dili ayrı olarak yüklemek zorunda kalmak yerine, desteklenen tüm dilleri tek bir yüklemede alır.</span><span class="sxs-lookup"><span data-stu-id="a34ce-125">**Simplicity**: Consumers of the package get all supported languages in a single install, rather than having to install each language separately.</span></span> <span data-ttu-id="a34ce-126">Tek bir paket de nuget.org üzerinde bulmayı daha kolay hale getirir.</span><span class="sxs-lookup"><span data-stu-id="a34ce-126">A single package is also easier to find on nuget.org.</span></span>
1. <span data-ttu-id="a34ce-127">**Bağlanmış sürümler**: tüm kaynak derlemeleri birincil derlemeyle aynı pakette olduğundan, hepsi aynı sürüm numarasını paylaşır ve hatalı bir şekilde ayrılmasıyla bir risk çalıştırmaz.</span><span class="sxs-lookup"><span data-stu-id="a34ce-127">**Coupled versions**: Because all of the resource assemblies are in the same package as the primary assembly, they all share the same version number and don't run a risk of getting erroneously decoupled.</span></span>

## <a name="localized-satellite-packages"></a><span data-ttu-id="a34ce-128">Yerelleştirilmiş uydu paketleri</span><span class="sxs-lookup"><span data-stu-id="a34ce-128">Localized satellite packages</span></span>

<span data-ttu-id="a34ce-129">.NET Framework uydu derlemelerini desteklediğine benzer şekilde, bu yöntem yerelleştirilmiş kaynakları ve IntelliSense XML dosyalarını uydu paketlerine ayırır.</span><span class="sxs-lookup"><span data-stu-id="a34ce-129">Similar to how .NET Framework supports satellite assemblies, this method separates localized resources and IntelliSense XML files into satellite packages.</span></span>

<span data-ttu-id="a34ce-130">Bunu yaptığınızda, birincil paketiniz `{identifier}.{version}.nupkg` adlandırma kuralını kullanır ve varsayılan dil için derlemeyi içerir (örneğin, en-US).</span><span class="sxs-lookup"><span data-stu-id="a34ce-130">Do to this, your primary package uses the naming convention `{identifier}.{version}.nupkg` and contains the assembly for the default language (such as en-US).</span></span> <span data-ttu-id="a34ce-131">Örneğin, `ContosoUtilities.1.0.0.nupkg` aşağıdaki yapıyı içerir:</span><span class="sxs-lookup"><span data-stu-id="a34ce-131">For example, `ContosoUtilities.1.0.0.nupkg` would contain the following structure:</span></span>

    lib
    └───net40
            ContosoUtilities.dll
            ContosoUtilities.xml

<span data-ttu-id="a34ce-132">Daha sonra bir uydu derlemesi, `ContosoUtilities.de.1.0.0.nupkg`gibi `{identifier}.{language}.{version}.nupkg`adlandırma kuralını kullanır.</span><span class="sxs-lookup"><span data-stu-id="a34ce-132">A satellite assembly then uses the naming convention `{identifier}.{language}.{version}.nupkg`, such as `ContosoUtilities.de.1.0.0.nupkg`.</span></span> <span data-ttu-id="a34ce-133">Tanımlayıcının, birincil paketin ile tam olarak eşleşmesi **gerekir** .</span><span class="sxs-lookup"><span data-stu-id="a34ce-133">The identifier **must** exactly match that of the primary package.</span></span>

<span data-ttu-id="a34ce-134">Bu ayrı bir paket olduğundan, yerelleştirilmiş meta verileri içeren kendi `.nuspec` dosyasına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="a34ce-134">Because this is a separate package, it has its own `.nuspec` file that contains localized metadata.</span></span> <span data-ttu-id="a34ce-135">`.nuspec` dilin dosya adında kullanılan bir ile **eşleşmesi gerektiğini unutmayın** .</span><span class="sxs-lookup"><span data-stu-id="a34ce-135">Be mindful that the language in the `.nuspec` **must** match the one used in the filename.</span></span>

<span data-ttu-id="a34ce-136">Uydu derlemesi, [] sürümü gösterimini kullanarak birincil paketin bir bağımlılık olarak tam bir sürümünü **de bildirmelidir (** bkz. [paket sürümü oluşturma](../concepts/package-versioning.md)).</span><span class="sxs-lookup"><span data-stu-id="a34ce-136">The satellite assembly **must** also declare an exact version of the primary package as a dependency, using the [] version notation (see [Package versioning](../concepts/package-versioning.md)).</span></span> <span data-ttu-id="a34ce-137">Örneğin, `ContosoUtilities.de.1.0.0.nupkg` `[1.0.0]` gösterimini kullanarak `ContosoUtilities.1.0.0.nupkg` bir bağımlılık bildirmelidir.</span><span class="sxs-lookup"><span data-stu-id="a34ce-137">For example, `ContosoUtilities.de.1.0.0.nupkg` must declare a dependency on `ContosoUtilities.1.0.0.nupkg` using the `[1.0.0]` notation.</span></span> <span data-ttu-id="a34ce-138">Uydu paketinin, birincil paketten farklı bir sürüm numarası olabilir.</span><span class="sxs-lookup"><span data-stu-id="a34ce-138">The satellite package can, of course, have a different version number than the primary package.</span></span>

<span data-ttu-id="a34ce-139">Uydu paketinin yapısı, kaynak derlemesini ve XML IntelliSense dosyasını paket dosya adında `{language}` eşleşen bir alt klasöre dahil etmelidir:</span><span class="sxs-lookup"><span data-stu-id="a34ce-139">The satellite package's structure must then include the resource assembly and XML IntelliSense file in a subfolder that matches `{language}` in the package filename:</span></span>

    lib
    └───net40
        └───de
                ContosoUtilities.resources.dll
                ContosoUtilities.xml

<span data-ttu-id="a34ce-140">**Note**: `ja-JP` gibi belirli alt kültürler gerekmedikçe, `ja`gibi her zaman daha yüksek düzey dil tanımlayıcısını kullanın.</span><span class="sxs-lookup"><span data-stu-id="a34ce-140">**Note**: unless specific subcultures such as `ja-JP` are necessary, always use the higher level language identifier, like `ja`.</span></span>

<span data-ttu-id="a34ce-141">Bir uydu derlemesinde, NuGet **yalnızca** klasördeki dosya adında `{language}` eşleşen dosyaları algılar.</span><span class="sxs-lookup"><span data-stu-id="a34ce-141">In a satellite assembly, NuGet will recognize **only** those files in the folder that matches the `{language}` in the filename.</span></span> <span data-ttu-id="a34ce-142">Diğerlerinin hepsi yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="a34ce-142">All others are ignored.</span></span>

<span data-ttu-id="a34ce-143">Bu kuralların tümü karşılandığında, NuGet paketi bir uydu paketi olarak tanır ve yerelleştirilmiş dosyaları asıl paketin `lib` klasörüne, özgün olarak paketlenmiş gibi yükler.</span><span class="sxs-lookup"><span data-stu-id="a34ce-143">When all of these conventions are met, NuGet will recognize the package as a satellite package and install the localized files into the primary package's `lib` folder, as if they had been originally bundled.</span></span> <span data-ttu-id="a34ce-144">Uydu paketini kaldırmak, dosyalarını aynı klasörden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="a34ce-144">Uninstalling the satellite package will remove its files from that same folder.</span></span>

<span data-ttu-id="a34ce-145">Desteklenen her dil için aynı şekilde ek uydu derlemeleri oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="a34ce-145">You would create additional satellite assemblies in the same way for each supported language.</span></span> <span data-ttu-id="a34ce-146">Bir örnek için, ASP.NET MVC paketlerinin kümesini inceleyin:</span><span class="sxs-lookup"><span data-stu-id="a34ce-146">For an example, examine the set of ASP.NET MVC packages:</span></span>

- <span data-ttu-id="a34ce-147">[Microsoft. Aspnet. Mvc](https://nuget.org/packages/Microsoft.AspNet.Mvc) (İngilizce birincil)</span><span class="sxs-lookup"><span data-stu-id="a34ce-147">[Microsoft.AspNet.Mvc](https://nuget.org/packages/Microsoft.AspNet.Mvc) (English primary)</span></span>
- <span data-ttu-id="a34ce-148">[Microsoft.Aspnet.Mvc.de](https://nuget.org/packages/Microsoft.AspNet.Mvc.de) (Almanca)</span><span class="sxs-lookup"><span data-stu-id="a34ce-148">[Microsoft.AspNet.Mvc.de](https://nuget.org/packages/Microsoft.AspNet.Mvc.de) (German)</span></span>
- <span data-ttu-id="a34ce-149">[Microsoft. Aspnet. Mvc. ja](https://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (Japonca)</span><span class="sxs-lookup"><span data-stu-id="a34ce-149">[Microsoft.AspNet.Mvc.ja](https://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (Japanese)</span></span>
- <span data-ttu-id="a34ce-150">[Microsoft. Aspnet. Mvc. zh-Hans](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (Çince (Basitleştirilmiş))</span><span class="sxs-lookup"><span data-stu-id="a34ce-150">[Microsoft.AspNet.Mvc.zh-Hans](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (Chinese (Simplified))</span></span>
- <span data-ttu-id="a34ce-151">[Microsoft. Aspnet. Mvc. zh-Hant](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (Çince (Geleneksel))</span><span class="sxs-lookup"><span data-stu-id="a34ce-151">[Microsoft.AspNet.Mvc.zh-Hant](https://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (Chinese (Traditional))</span></span>

### <a name="summary-of-required-conventions"></a><span data-ttu-id="a34ce-152">Gerekli kuralların Özeti</span><span class="sxs-lookup"><span data-stu-id="a34ce-152">Summary of required conventions</span></span>

- <span data-ttu-id="a34ce-153">Birincil paketin adı `{identifier}.{version}.nupkg` olmalıdır</span><span class="sxs-lookup"><span data-stu-id="a34ce-153">Primary package must be named `{identifier}.{version}.nupkg`</span></span>
- <span data-ttu-id="a34ce-154">Uydu paketinin adlandırılmış olması gerekir `{identifier}.{language}.{version}.nupkg`</span><span class="sxs-lookup"><span data-stu-id="a34ce-154">A satellite package must be named `{identifier}.{language}.{version}.nupkg`</span></span>
- <span data-ttu-id="a34ce-155">Uydu paketinin `.nuspec`, dosya adıyla eşleşecek şekilde dilini belirtmelidir.</span><span class="sxs-lookup"><span data-stu-id="a34ce-155">A satellite package's `.nuspec` must specify its language to match the filename.</span></span>
- <span data-ttu-id="a34ce-156">Uydu paketinin, `.nuspec` dosyasında [] gösterimini kullanarak, birincil öğesinin tam bir sürümüne bağımlılık bildirmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="a34ce-156">A satellite package must declare a dependency on an exact version of the primary using the [] notation in its `.nuspec` file.</span></span> <span data-ttu-id="a34ce-157">Aralıklar desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="a34ce-157">Ranges are not supported.</span></span>
- <span data-ttu-id="a34ce-158">Uydu paketinin dosya adında `{language}` tam olarak eşleşen `lib\[{framework}\]{language}` klasöre dosyaları yerleştirmelidir.</span><span class="sxs-lookup"><span data-stu-id="a34ce-158">A satellite package must place files in the `lib\[{framework}\]{language}` folder that exactly matches `{language}` in the filename.</span></span>

### <a name="advantages-and-disadvantages-satellite-packages"></a><span data-ttu-id="a34ce-159">Avantajlar ve dezavantajlar (uydu paketleri)</span><span class="sxs-lookup"><span data-stu-id="a34ce-159">Advantages and disadvantages (satellite packages)</span></span>

<span data-ttu-id="a34ce-160">Uydu paketlerinin kullanılması birkaç avantaj sunar:</span><span class="sxs-lookup"><span data-stu-id="a34ce-160">Using satellite packages has a few benefits:</span></span>

1. <span data-ttu-id="a34ce-161">**Paket boyutu**: birincil paketin genel parmak izi en aza indirilir ve tüketiciler yalnızca kullanmak istedikleri her dilin maliyetlerine neden olur.</span><span class="sxs-lookup"><span data-stu-id="a34ce-161">**Package size**: The overall footprint of the primary package is minimized, and consumers only incur the costs of each language they want to use.</span></span>
1. <span data-ttu-id="a34ce-162">**Ayrı meta veriler**: her uydu paketinin kendi `.nuspec` dosyası ve bu nedenle kendi yerelleştirilmiş meta verileri vardır.</span><span class="sxs-lookup"><span data-stu-id="a34ce-162">**Separate metadata**: Each satellite package has its own `.nuspec` file and thus its own localized metadata because.</span></span> <span data-ttu-id="a34ce-163">Bu, nuget.org ' i yerelleştirilmiş koşullara göre arayarak bazı tüketicilerin paketleri daha kolay bulmasına izin verebilir.</span><span class="sxs-lookup"><span data-stu-id="a34ce-163">This can allow some consumers to find packages more easily by searching nuget.org with localized terms.</span></span>
1. <span data-ttu-id="a34ce-164">**Ayrılmış yayınlar**: uydu derlemeleri her seferinde değil tek seferde yayımlanabilecek ve yerelleştirme çabalarınızı yaymanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="a34ce-164">**Decoupled releases**: Satellite assemblies can be released over time, rather than all at once, allowing you to spread out your localization efforts.</span></span>

<span data-ttu-id="a34ce-165">Ancak uydu paketleri kendi dezavantajlarına sahiptir:</span><span class="sxs-lookup"><span data-stu-id="a34ce-165">However, satellite packages have their own set of disadvantages:</span></span>

1. <span data-ttu-id="a34ce-166">**Dağınıklık**: tek bir paket yerine, NuGet.org üzerinde karışık arama sonuçlarına ve bir Visual Studio projesindeki bir dizi başvuruya yönelik uzun bir listeye yol açabilecek çok sayıda paketiniz olabilir.</span><span class="sxs-lookup"><span data-stu-id="a34ce-166">**Clutter**: Instead of a single package, you have many packages that can lead to cluttered search results on nuget.org and a long list of references in a Visual Studio project.</span></span>
1. <span data-ttu-id="a34ce-167">**Katı kurallar**.</span><span class="sxs-lookup"><span data-stu-id="a34ce-167">**Strict conventions**.</span></span> <span data-ttu-id="a34ce-168">Uydu paketleri, kuralları tam olarak izlemelidir veya yerelleştirilmiş sürümler doğru bir şekilde çekilmeyecektir.</span><span class="sxs-lookup"><span data-stu-id="a34ce-168">Satellite packages must follow the conventions exactly or the localized versions won't be picked up properly.</span></span>
1. <span data-ttu-id="a34ce-169">**Sürüm oluşturma**: her uydu paketinin, birincil pakette tam bir sürüm bağımlılığı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a34ce-169">**Versioning**: Each satellite package must have an exact version dependency on the primary package.</span></span> <span data-ttu-id="a34ce-170">Bu, birincil paketin güncelleştirilmesi, kaynakların değişmese de tüm uydu paketlerinin güncelleştirilmesini gerektirebileceği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="a34ce-170">This means that updating the primary package may require updating all satellite packages as well, even if the resources didn't change.</span></span>
