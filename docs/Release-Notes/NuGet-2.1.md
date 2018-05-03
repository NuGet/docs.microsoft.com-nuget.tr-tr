---
title: NuGet 2.1 sürüm notları
description: NuGet bilinen sorunları, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere 2.1 için sürüm notları.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3b7a000098a7362f4b1c2c4072c6cd1468baf9b5
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/28/2018
---
# <a name="nuget-21-release-notes"></a><span data-ttu-id="9fbec-103">NuGet 2.1 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="9fbec-103">NuGet 2.1 Release Notes</span></span>

<span data-ttu-id="9fbec-104">[NuGet 2.0 sürüm notları](../release-notes/nuget-2.0.md) | [NuGet 2.2 sürüm notları](../release-notes/nuget-2.2.md)</span><span class="sxs-lookup"><span data-stu-id="9fbec-104">[NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md) | [NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md)</span></span>

<span data-ttu-id="9fbec-105">NuGet 2.1 4 Ekim 2012'de serbest bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="9fbec-105">NuGet 2.1 was released on October 4, 2012.</span></span>

## <a name="hierarchical-nugetconfig"></a><span data-ttu-id="9fbec-106">Hiyerarşik Nuget.Config</span><span class="sxs-lookup"><span data-stu-id="9fbec-106">Hierarchical Nuget.Config</span></span>

<span data-ttu-id="9fbec-107">NuGet 2.1 aramakta klasör yapısını taramasını yinelemeli yapmamanız NuGet ayarlarını denetleme daha fazla esneklik sağlar `NuGet.Config` dosyaları ve tüm bulunan dosyaları kümesini yapılandırmasından oluşturma.</span><span class="sxs-lookup"><span data-stu-id="9fbec-107">NuGet 2.1 gives you greater flexibility in controlling NuGet settings by way of recursively walking up the folder structure looking for `NuGet.Config` files and then building the configuration from the set of all found files.</span></span>  <span data-ttu-id="9fbec-108">Örnek olarak, bir takım iç Paket Deposu diğer iç bağımlılıklar CI yapılar için sahip olduğu senaryo düşünün.</span><span class="sxs-lookup"><span data-stu-id="9fbec-108">As an example, consider the scenario where a team has an internal package repository for CI builds of other internal dependencies.</span></span> <span data-ttu-id="9fbec-109">Her bir proje için klasör yapısı aşağıdakine benzeyebilir:</span><span class="sxs-lookup"><span data-stu-id="9fbec-109">The folder structure for an individual project might look like the following:</span></span>

    C:\
    C:\myteam\
    C:\myteam\solution1
    C:\myteam\solution1\project1

<span data-ttu-id="9fbec-110">Ayrıca, çözüm için paket geri yüklemesi etkinleştirilirse, aşağıdaki klasörü de bulunur:</span><span class="sxs-lookup"><span data-stu-id="9fbec-110">Additionally, if package restore is enabled for the solution, the following folder will also exist:</span></span>

    C:\myteam\solution1\.nuget

<span data-ttu-id="9fbec-111">Ekibin iç Paket Deposu takım çalışır, her proje için makinede kullanıma değil sırasında tüm projeleri için kullanılabilir olması için Biz yeni bir Nuget.Config dosyası oluşturabilir ve bu c:\myteam klasöre yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="9fbec-111">In order to have the team’s internal package repository available for all projects that the team works on, while not making it available for every project on the machine, we can create a new Nuget.Config file and place it in the c:\myteam folder.</span></span> <span data-ttu-id="9fbec-112">Hiçbir şekilde çok specificy proje her bir paket klasörü.</span><span class="sxs-lookup"><span data-stu-id="9fbec-112">There is no way to specificy a packages folder per project.</span></span>

```xml
<configuration>
    <packageSources>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </packageSources>
    <disabledPackageSources />
    <activePackageSource>
    <add key="Official project team source" value="http://teamserver/api/v2/" />
    </activePackageSource>
</configuration>
```

<span data-ttu-id="9fbec-113">Şimdi aşağıda gösterildiği gibi c:\myteam altındaki herhangi bir klasörden 'nuget.exe kaynakları' komutunu çalıştırarak kaynak eklendi görebiliriz:</span><span class="sxs-lookup"><span data-stu-id="9fbec-113">We can now see that the source was added by running the ‘nuget.exe sources’ command from any folder beneath c:\myteam as shown below:</span></span>

![Paket kaynaklardan üst nuget yapılandırma](./media/releasenotes-21-cfg-hierarchy.png)

<span data-ttu-id="9fbec-115">`NuGet.Config` dosyaları aşağıdaki sırayla aranır:</span><span class="sxs-lookup"><span data-stu-id="9fbec-115">`NuGet.Config` files are searched for in the following order:</span></span>

1. `.nuget\Nuget.Config`
2. <span data-ttu-id="9fbec-116">Özyinelemeli kök proje klasöründen yol</span><span class="sxs-lookup"><span data-stu-id="9fbec-116">Recursive walk from project folder to root</span></span>
3. <span data-ttu-id="9fbec-117">Genel `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)</span><span class="sxs-lookup"><span data-stu-id="9fbec-117">Global `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)</span></span>

<span data-ttu-id="9fbec-118">İçinde uygulanan daha bağlantılardır *ters sırada*, yukarıdaki sırasını temel anlamına gelir, genel Nuget.Config ilk uygulanan, keşfedilen Nuget.Config dosyalar kökünden proje klasörüne gelir, ve ardından tarafından `.nuget\Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="9fbec-118">The configurations are than applied in the *reverse order*, meaning that based on the above ordering, the global Nuget.Config would be applied first, followed by the discovered Nuget.Config files from root to project folder, followed by `.nuget\Nuget.Config`.</span></span>  <span data-ttu-id="9fbec-119">Bu kullanıyorsanız, özellikle önemlidir `<clear/>` öğeleri kümesi yapılandırma dosyasından kaldırılacak öğe.</span><span class="sxs-lookup"><span data-stu-id="9fbec-119">This is particularly important if you’re using the `<clear/>` element to remove a set of items from config.</span></span>

## <a name="specify-packages-folder-location"></a><span data-ttu-id="9fbec-120">'Packages' klasörü konumu belirtin</span><span class="sxs-lookup"><span data-stu-id="9fbec-120">Specify ‘packages’ Folder Location</span></span>

<span data-ttu-id="9fbec-121">Geçmişte, NuGet, çözüm kök klasörünün altında bulunan bir bilinen 'packages' klasöründen bir çözümün paketleri yönetilen.</span><span class="sxs-lookup"><span data-stu-id="9fbec-121">In the past, NuGet has managed a solution’s packages from a known ‘packages’ folder found beneath the solution root folder.</span></span>  <span data-ttu-id="9fbec-122">NuGet paketleri yüklü olan birçok farklı çözümler sahip geliştirme ekipleri için bu dosya sisteminde pek çok farklı yerde yüklenen aynı paketin neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="9fbec-122">For development teams that have many different solutions which have NuGet packages installed, this can result in the same package being installed in many different places on the file system.</span></span>

<span data-ttu-id="9fbec-123">NuGet 2.1 paketleri klasörünün konumunu üzerinde daha ayrıntılı denetim sağlar `repositoryPath` öğesinde `NuGet.Config` dosya.</span><span class="sxs-lookup"><span data-stu-id="9fbec-123">NuGet 2.1 provides more granular control over the location of the packages folder via the `repositoryPath` element in the `NuGet.Config` file.</span></span>  <span data-ttu-id="9fbec-124">Hiyerarşik Nuget.Config destek önceki örneği oluşturma, C:\myteam\ paylaşımı aynı paketler klasörü altındaki tüm projeleri istediğimiz varsayalım.</span><span class="sxs-lookup"><span data-stu-id="9fbec-124">Building on the previous example of hierarchical Nuget.Config support, assume that we wish to have all projects under C:\myteam\ share the same packages folder.</span></span>  <span data-ttu-id="9fbec-125">Bunu başarmak için yalnızca aşağıdaki girdiyi `c:\myteam\Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="9fbec-125">To accomplish this, simply add the following entry to `c:\myteam\Nuget.Config`.</span></span>

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

<span data-ttu-id="9fbec-126">Bu örnekte, paylaşılan `Nuget.Config` dosya C:\myteam derinliği bağımsız olarak oluşturulan her proje için paylaşılan paketler klasörünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="9fbec-126">In this example, the shared `Nuget.Config` file specifies a shared packages folder for every project that is created beneath C:\myteam, regardless of depth.</span></span> <span data-ttu-id="9fbec-127">Var olan bir paket klasörü altında çözüm kök varsa, NuGet paketleri yeni konuma yerleştirir önce silmeniz gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="9fbec-127">Note that if you have an existing packages folder underneath your solution root, you need to delete it before NuGet will place packages in the new location.</span></span>

## <a name="support-for-portable-libraries"></a><span data-ttu-id="9fbec-128">Taşınabilir kitaplıklara desteği</span><span class="sxs-lookup"><span data-stu-id="9fbec-128">Support for Portable Libraries</span></span>

<span data-ttu-id="9fbec-129">[Taşınabilir kitaplıklara](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) önce farklı platformlarda Microsoft.NET Framework Windows Phone ve hatta Xbox Silverlight'a sürümlerinden yapmadan çalışabilirsiniz derlemeleri oluşturmanıza olanak sağlayan bir .NET 4 ile sunulan bir özelliktir 360 (şu anda NuGet Xbox taşınabilir kitaplığı hedef desteklemiyor rağmen).</span><span class="sxs-lookup"><span data-stu-id="9fbec-129">[Portable libraries](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) is a feature first introduced with .NET 4 that enables you to build assemblies that can work without modification on different Microsoft platforms, from versions of the.NET Framework to Silverlight to Windows Phone and even Xbox 360 (though at this time, NuGet does not support the Xbox portable library target).</span></span>  <span data-ttu-id="9fbec-130">Genişletme tarafından [paketini kuralları](../create-packages/supporting-multiple-target-frameworks.md) framework sürümleri ve profilleri için NuGet 2.1 artık taşınabilir kitaplıklara bileşik framework ve profil hedef sahip paketleri oluşturmanıza olanak sağlayarak destekler `lib` klasörler.</span><span class="sxs-lookup"><span data-stu-id="9fbec-130">By extending the [package conventions](../create-packages/supporting-multiple-target-frameworks.md) for framework versions and profiles, NuGet 2.1 now supports portable libraries by enabling you to create packages that have compound framework and profile target `lib` folders.</span></span>

<span data-ttu-id="9fbec-131">Örnek olarak, aşağıdaki taşınabilir sınıf kitaplığının kullanılabilir hedef platformlar göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="9fbec-131">As an example, consider the following portable class library’s available target platforms.</span></span>

![Taşınabilir Kitaplığı oluşturma iletişim kutusu](./media/releasenotes-21-plib.png)

<span data-ttu-id="9fbec-133">Kitaplığı oluşturulduktan sonra ve komutu `nuget.exe pack MyPortableProject.csproj` çalıştırıldığında, yeni taşınabilir kitaplık paketi klasör yapısı oluşturulan NuGet paketinin içeriğini inceleyerek görülme.</span><span class="sxs-lookup"><span data-stu-id="9fbec-133">After the library is built and the command `nuget.exe pack MyPortableProject.csproj` is run, the new portable library package folder structure can be seen by examining the contents of the generated NuGet package.</span></span>

![Taşınabilir kitaplık paketi düzeni](./media/releasenotes-21-plib-layout.png)

<span data-ttu-id="9fbec-135">Gördüğünüz gibi taşınabilir kitaplığı klasörü adı kuralını düzeni 'taşınabilir-{framework 1} + {framework n}' Varolan framework tanımlayıcıları burada izleyin izleyen [framework adı ve sürümü kuralları](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="9fbec-135">As you can see, the portable library folder name convention follows the pattern ‘portable-{framework 1}+{framework n}’ where the framework identifiers follow the existing [framework name and version conventions](../reference/target-frameworks.md).</span></span> <span data-ttu-id="9fbec-136">Bir özel durum adı ve sürümü kuralları için Windows Phone için kullanılan framework tanımlayıcısı dizininde bulunur.</span><span class="sxs-lookup"><span data-stu-id="9fbec-136">One exception to the name and version conventions is found in the framework identifier used for Windows Phone.</span></span>  <span data-ttu-id="9fbec-137">Bu ad, çerçeve adı 'wp' (wp7, wp71 veya wp8) kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9fbec-137">This moniker should use the framework name ‘wp’ (wp7, wp71 or wp8).</span></span> <span data-ttu-id="9fbec-138">'Silverlight-wp7' kullanarak, örneğin, bir hatayla sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="9fbec-138">Using ‘silverlight-wp7’, for example, will result in an error.</span></span>

<span data-ttu-id="9fbec-139">Bu klasör yapısından oluşturduğunuz paketi yüklerken, NuGet çerçevesi ve profil kurallarını klasör adı belirtildiği gibi birden çok hedefe şimdi uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9fbec-139">When installing the package that is created from this folder structure, NuGet can now apply its framework and profile rules to multiple targets, as specified in the folder name.</span></span>  <span data-ttu-id="9fbec-140">NuGet eşleştirme kurallarına "daha fazla belirli" hedefler "küçük" yayına öncelik kazanır ilkesidir.</span><span class="sxs-lookup"><span data-stu-id="9fbec-140">Behind NuGet’s matching rules is the principle that “more specific” targets will take precedence over “less specific” ones.</span></span>  <span data-ttu-id="9fbec-141">Bu her ikisi de bir proje ile uyumlu olmaları durumunda belirli bir platform desteği adlar her zaman taşınabilir olanları tercih edilen olacağı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="9fbec-141">This means that monikers targeting a specific platform will always be preferred over portable ones if they are both compatible with a project.</span></span>  <span data-ttu-id="9fbec-142">Ayrıca, birden çok taşınabilir hedefi bir projeyle uyumlu olup olmadıklarını NuGet desteklenen platformlar kümesi "paketi başvuran projeye yakın" olduğu bir tercih eder.</span><span class="sxs-lookup"><span data-stu-id="9fbec-142">Additionally, if multiple portable targets are compatible with a project, NuGet will prefer the one where the set of platforms supported is “closest” to the project referencing the package.</span></span>

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a><span data-ttu-id="9fbec-143">Hedefleme Windows 8 ve Windows Phone 8 projeleri</span><span class="sxs-lookup"><span data-stu-id="9fbec-143">Targeting Windows 8 and Windows Phone 8 Projects</span></span>

<span data-ttu-id="9fbec-144">Taşınabilir kitaplık projeleri hedefleyen desteği ekleme ek olarak, NuGet 2.1 yeni framework adlar için Windows mağazası ve olacaktır Windows Phone projeleri için bazı yeni genel adlar yanı sıra Windows 8 Mağazası ve Windows Phone 8 projeleri sağlar ilgili platformları gelecekteki sürümleri arasında yönetmek daha kolay.</span><span class="sxs-lookup"><span data-stu-id="9fbec-144">In addition to adding support for targeting portable library projects, NuGet 2.1 provides new framework monikers for both Windows 8 Store and Windows Phone 8 projects, as well as some new general monikers for Windows Store and Windows Phone projects that will be easier to manage across future versions of the respective platforms.</span></span>

<span data-ttu-id="9fbec-145">Windows 8 Mağazası uygulamaları için tanımlayıcıları aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="9fbec-145">For Windows 8 Store applications, the identifiers look as follows:</span></span>

| <span data-ttu-id="9fbec-146">NuGet 2.0 ve daha önceki</span><span class="sxs-lookup"><span data-stu-id="9fbec-146">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="9fbec-147">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="9fbec-147">NuGet 2.1</span></span> |
| ---------------- | ----------- |
| <span data-ttu-id="9fbec-148">winRT45. NETCore45</span><span class="sxs-lookup"><span data-stu-id="9fbec-148">winRT45, .NETCore45</span></span> | <span data-ttu-id="9fbec-149">Windows, Windows8, win olduğu win8</span><span class="sxs-lookup"><span data-stu-id="9fbec-149">Windows, Windows8, win, win8</span></span> |

<br/>
<span data-ttu-id="9fbec-150">Windows Phone projeleri için tanımlayıcıları aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="9fbec-150">For Windows Phone projects, the identifiers look as follows:</span></span>

| <span data-ttu-id="9fbec-151">Phone OS</span><span class="sxs-lookup"><span data-stu-id="9fbec-151">Phone OS</span></span> | <span data-ttu-id="9fbec-152">NuGet 2.0 ve daha önceki</span><span class="sxs-lookup"><span data-stu-id="9fbec-152">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="9fbec-153">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="9fbec-153">NuGet 2.1</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9fbec-154">Windows Phone 7</span><span class="sxs-lookup"><span data-stu-id="9fbec-154">Windows Phone 7</span></span> | <span data-ttu-id="9fbec-155">silverlight3 wp</span><span class="sxs-lookup"><span data-stu-id="9fbec-155">silverlight3-wp</span></span> | <span data-ttu-id="9fbec-156">WB, wp7, WindowsPhone, WindowsPhone7</span><span class="sxs-lookup"><span data-stu-id="9fbec-156">wp, wp7, WindowsPhone, WindowsPhone7</span></span> |
| <span data-ttu-id="9fbec-157">Windows Phone 7.5 (Mango)</span><span class="sxs-lookup"><span data-stu-id="9fbec-157">Windows Phone 7.5 (Mango)</span></span> | <span data-ttu-id="9fbec-158">silverlight4 wp71</span><span class="sxs-lookup"><span data-stu-id="9fbec-158">silverlight4-wp71</span></span> | <span data-ttu-id="9fbec-159">wp71, WindowsPhone71</span><span class="sxs-lookup"><span data-stu-id="9fbec-159">wp71, WindowsPhone71</span></span> |
| <span data-ttu-id="9fbec-160">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="9fbec-160">Windows Phone 8</span></span> | <span data-ttu-id="9fbec-161">(desteklenmez)</span><span class="sxs-lookup"><span data-stu-id="9fbec-161">(not supported)</span></span> | <span data-ttu-id="9fbec-162">wp8, WindowsPhone8</span><span class="sxs-lookup"><span data-stu-id="9fbec-162">wp8, WindowsPhone8</span></span> |

<br/>
<span data-ttu-id="9fbec-163">Tüm yukarıdaki değişiklikleri eski framework adları tam olarak NuGet 2.1 tarafından desteklenen devam eder.</span><span class="sxs-lookup"><span data-stu-id="9fbec-163">In all of the above changes, the old framework names will continue to be fully supported by NuGet 2.1.</span></span>  <span data-ttu-id="9fbec-164">Bunlar ilgili platformları gelecekteki sürümleri arasında daha tutarlı olarak ilerleyen, yeni adlarını kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9fbec-164">Moving forward, the new names should be used as they will be more stable across future versions of the respective platforms.</span></span> <span data-ttu-id="9fbec-165">Yeni adlarını olur *değil* olması 2.1 önce NuGet sürümlerinde desteklenir, ancak, bu nedenle uygun şekilde planlamak geçiş yapmak ne zaman.</span><span class="sxs-lookup"><span data-stu-id="9fbec-165">The new names will *not* be supported in versions of NuGet prior to 2.1, however, so plan accordingly for when to make the switch.</span></span>

## <a name="improved-search-in-package-manager-dialog"></a><span data-ttu-id="9fbec-166">Paket Yöneticisi iletişim kutusundaki Gelişmiş arama</span><span class="sxs-lookup"><span data-stu-id="9fbec-166">Improved Search in Package Manager Dialog</span></span>

<span data-ttu-id="9fbec-167">Son birkaç yinelemeler üzerinden değişiklikleri hızı ve paket aramaları alaka büyük ölçüde geliştirilmiş NuGet galerisinde tanıtılmıştır.</span><span class="sxs-lookup"><span data-stu-id="9fbec-167">Over the past several iterations, changes have been introduced to the NuGet gallery that greatly improved the speed and relevance of package searches.</span></span>  <span data-ttu-id="9fbec-168">Ancak, bu geliştirmeler nuget.org Web sitesine sınırlı.</span><span class="sxs-lookup"><span data-stu-id="9fbec-168">However, these improvements were limited to the nuget.org Web site.</span></span>  <span data-ttu-id="9fbec-169">NuGet 2.1 deneyimi geliştirilmiş arama NuGet Paket Yöneticisi iletişim kutusu üzerinden kullanılabilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="9fbec-169">NuGet 2.1 makes the improved search experience available through the NuGet package manager dialog.</span></span>  <span data-ttu-id="9fbec-170">Örnek olarak, Windows Azure önbelleğe alma Önizleme paketini bulmak istediğinizi düşünelim.</span><span class="sxs-lookup"><span data-stu-id="9fbec-170">As an example, imagine that you wanted to find the Windows Azure Caching Preview package.</span></span>  <span data-ttu-id="9fbec-171">Bu paket için makul arama sorgusu, "Azure önbelleği" olabilir.</span><span class="sxs-lookup"><span data-stu-id="9fbec-171">A reasonable search query for this package may be “Azure Cache”.</span></span>  <span data-ttu-id="9fbec-172">Paket Yöneticisi iletişim önceki sürümlerinde, istenen paket bile sonuçları'nın ilk sayfasında listelenir değil.</span><span class="sxs-lookup"><span data-stu-id="9fbec-172">In previous versions of the package manager dialog, the desired package would not even be listed on the first page of results.</span></span>  <span data-ttu-id="9fbec-173">Ancak, NuGet 2.1 istenen paket şimdi arama sonuçları en üstünde görünür.</span><span class="sxs-lookup"><span data-stu-id="9fbec-173">However, in NuGet 2.1, the desired package now shows up at the top of the search results.</span></span>

![Paket Yöneticisi iletişim arama](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a><span data-ttu-id="9fbec-175">Paket güncelleştirme zorla</span><span class="sxs-lookup"><span data-stu-id="9fbec-175">Force Package Update</span></span>

<span data-ttu-id="9fbec-176">Bir not değiştirildiği bir paketin güncelleştirilmesi, NuGet 2.1 önce NuGet Atla yüksek sürüm numarası.</span><span class="sxs-lookup"><span data-stu-id="9fbec-176">Prior to NuGet 2.1, NuGet would skip updating a package when there was a not a high version number.</span></span>  <span data-ttu-id="9fbec-177">Bu uyuşmazlık – özellikle söz konusu olduğunda derleme veya CI senaryolar burada takım Paket sürümü ile her yapı numarası artırılacağını istemediğiniz belirli senaryolar için kullanıma sunuldu.</span><span class="sxs-lookup"><span data-stu-id="9fbec-177">This introduced friction for certain scenarios – particularly in the case of build or CI scenarios where the team did not want to increment the package version number with each build.</span></span>  <span data-ttu-id="9fbec-178">Bir güncelleştirme bakılmaksızın zorlamak için istenen davranışı oluştu.</span><span class="sxs-lookup"><span data-stu-id="9fbec-178">The desired behavior was to force an update regardless.</span></span>  <span data-ttu-id="9fbec-179">NuGet 2.1 Bu 'yeniden' bayrağıyla giderir.</span><span class="sxs-lookup"><span data-stu-id="9fbec-179">NuGet 2.1 addresses this with the ‘reinstall’ flag.</span></span>  <span data-ttu-id="9fbec-180">Örneğin, NuGet önceki sürümleri aşağıdaki daha yeni bir paket sürüme sahip bir paketi güncelleştirmeye çalışırken neden olur:</span><span class="sxs-lookup"><span data-stu-id="9fbec-180">For example, previous versions of NuGet would result in the following when attempting to update a package that did not have a more recent package version:</span></span>

    PM> Update-Package Moq
    No updates available for 'Moq' in project 'MySolution.MyConsole'.

<span data-ttu-id="9fbec-181">Paket olup olmamasına bakılmaksızın yeniden bayrağıyla güncelleştirileceği daha yeni bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="9fbec-181">With the reinstall flag, the package will be updated regardless of whether there is a newer version.</span></span>

    PM> Update-Package Moq -Reinstall
    Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
    Successfully uninstalled 'Moq 4.0.10827'.
    Successfully installed 'Moq 4.0.10827'.
    Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.

<span data-ttu-id="9fbec-182">Burada REINSTALL bayrağı faydalı kanıtlar başka bir senaryo framework yeniden hedefleme olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="9fbec-182">Another scenario where the reinstall flag proves beneficial is that of framework re-targeting.</span></span> <span data-ttu-id="9fbec-183">Bir projeden (örneğin, .NET 4.5 için .NET 4), hedef Framework'ü değiştirirken güncelleştirme paketini-yeniden projede yüklü olan tüm NuGet paketleri için doğru derlemelerine başvurular güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9fbec-183">When changing the target framework of a project (for example, from .NET 4 to .NET 4.5), Update-Package -Reinstall can update references to the correct assemblies for all NuGet packages installed in the project.</span></span>

## <a name="edit-package-sources-within-visual-studio"></a><span data-ttu-id="9fbec-184">Visual Studio içinde paket kaynaklarını Düzenle</span><span class="sxs-lookup"><span data-stu-id="9fbec-184">Edit Package Sources Within Visual Studio</span></span>

<span data-ttu-id="9fbec-185">NuGet önceki sürümlerinde, silme ve paket kaynağı yeniden eklenmesi gereken Visual Studio Seçenekleri iletişim kutusu içinde bir paket kaynağından güncelleştiriliyor.</span><span class="sxs-lookup"><span data-stu-id="9fbec-185">In previous versions of NuGet, updating a package source from within the Visual Studio options dialog required deleting and re-adding the package source.</span></span>  <span data-ttu-id="9fbec-186">NuGet 2.1, bu iş akışı Yapılandırması kullanıcı arabirimi birinci sınıf bir işlevi olarak güncelleştirme destekleyerek artırır.</span><span class="sxs-lookup"><span data-stu-id="9fbec-186">NuGet 2.1 improves this workflow by supporting update as a first class function of the configuration user interface.</span></span>

![Paket Yöneticisi yapılandırma iletişim kutusu](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="9fbec-188">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="9fbec-188">Bug Fixes</span></span>

<span data-ttu-id="9fbec-189">NuGet 2.1 birçok hata düzeltmeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="9fbec-189">NuGet 2.1 includes many bug fixes.</span></span> <span data-ttu-id="9fbec-190">Tam bir listesi için iş öğeleri NuGet 2. 0'da, lütfen Görünüm sabit [NuGet sorun İzleyicisi bu sürüm için](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="9fbec-190">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
