---
title: NuGet 2.1 sürüm notları
description: NuGet bilinen sorunları, hata düzeltmeleri, eklenen özellikler ve dcr dahil olmak üzere 2.1 için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fd6dadc7968991c77c1b06a6a261415355b2fd73
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548603"
---
# <a name="nuget-21-release-notes"></a><span data-ttu-id="b6d70-103">NuGet 2.1 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="b6d70-103">NuGet 2.1 Release Notes</span></span>

<span data-ttu-id="b6d70-104">[NuGet 2.0 sürüm notları](../release-notes/nuget-2.0.md) | [NuGet 2.2 sürüm notları](../release-notes/nuget-2.2.md)</span><span class="sxs-lookup"><span data-stu-id="b6d70-104">[NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md) | [NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md)</span></span>

<span data-ttu-id="b6d70-105">NuGet 2.1 4 Ekim 2012 tarihinde yayınlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b6d70-105">NuGet 2.1 was released on October 4, 2012.</span></span>

## <a name="hierarchical-nugetconfig"></a><span data-ttu-id="b6d70-106">Hiyerarşik Nuget.Config</span><span class="sxs-lookup"><span data-stu-id="b6d70-106">Hierarchical Nuget.Config</span></span>

<span data-ttu-id="b6d70-107">NuGet 2.1 özyinelemeli olarak aramak klasör yapısını walking yoluyla NuGet ayarları denetleme daha fazla esneklik sağlar `NuGet.Config` dosyaları ve ardından yapılandırma kümesinden tüm bulunan dosyalar oluşturma.</span><span class="sxs-lookup"><span data-stu-id="b6d70-107">NuGet 2.1 gives you greater flexibility in controlling NuGet settings by way of recursively walking up the folder structure looking for `NuGet.Config` files and then building the configuration from the set of all found files.</span></span>  <span data-ttu-id="b6d70-108">Örneğin, takım CI derlemeleri diğer iç bağımlılıklar için bir iç Paket Deposu olduğu senaryoyu düşünün.</span><span class="sxs-lookup"><span data-stu-id="b6d70-108">As an example, consider the scenario where a team has an internal package repository for CI builds of other internal dependencies.</span></span> <span data-ttu-id="b6d70-109">Her bir proje için klasör yapısı aşağıdaki gibi görünebilir:</span><span class="sxs-lookup"><span data-stu-id="b6d70-109">The folder structure for an individual project might look like the following:</span></span>

    C:\
    C:\myteam\
    C:\myteam\solution1
    C:\myteam\solution1\project1

<span data-ttu-id="b6d70-110">Ayrıca, çözüm için paket geri yükleme etkinleştirilirse, aşağıdaki klasörü de vardır:</span><span class="sxs-lookup"><span data-stu-id="b6d70-110">Additionally, if package restore is enabled for the solution, the following folder will also exist:</span></span>

    C:\myteam\solution1\.nuget

<span data-ttu-id="b6d70-111">Takımın iç paket deposu, her proje için kullanılabilir makinede yaparken değil, takımın çalıştığı tüm projeleri için kullanılabilir olması için size yeni bir Nuget.Config dosyası oluşturabilir ve c:\myteam klasörüne yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="b6d70-111">In order to have the team’s internal package repository available for all projects that the team works on, while not making it available for every project on the machine, we can create a new Nuget.Config file and place it in the c:\myteam folder.</span></span> <span data-ttu-id="b6d70-112">Bir yolu yoktur çok specificy her proje bir paket klasörü.</span><span class="sxs-lookup"><span data-stu-id="b6d70-112">There is no way to specificy a packages folder per project.</span></span>

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

<span data-ttu-id="b6d70-113">Artık kaynak aşağıda gösterildiği gibi c:\myteam altındaki herhangi bir klasörde 'nuget.exe kaynakları' komutunu çalıştırarak eklendiğini görebiliriz:</span><span class="sxs-lookup"><span data-stu-id="b6d70-113">We can now see that the source was added by running the ‘nuget.exe sources’ command from any folder beneath c:\myteam as shown below:</span></span>

![Paket kaynaklarından üst nuget yapılandırma](./media/releasenotes-21-cfg-hierarchy.png)

<span data-ttu-id="b6d70-115">`NuGet.Config` dosyaları aşağıdaki sırayla aranır:</span><span class="sxs-lookup"><span data-stu-id="b6d70-115">`NuGet.Config` files are searched for in the following order:</span></span>

1. `.nuget\Nuget.Config`
2. <span data-ttu-id="b6d70-116">Yinelemeli proje klasöründen kök yol</span><span class="sxs-lookup"><span data-stu-id="b6d70-116">Recursive walk from project folder to root</span></span>
3. <span data-ttu-id="b6d70-117">Genel `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)</span><span class="sxs-lookup"><span data-stu-id="b6d70-117">Global `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)</span></span>

<span data-ttu-id="b6d70-118">Uygulanan daha yapılandırmalarıdır *ters sırada*, yukarıdaki sıralamaya bağlı anlamına gelir, genel Nuget.Config ilk uygulanan, bulunan Nuget.Config dosyalar kökünden proje klasörüne gelir, ardından tarafından `.nuget\Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="b6d70-118">The configurations are than applied in the *reverse order*, meaning that based on the above ordering, the global Nuget.Config would be applied first, followed by the discovered Nuget.Config files from root to project folder, followed by `.nuget\Nuget.Config`.</span></span>  <span data-ttu-id="b6d70-119">Bu kullanıyorsanız özellikle önemlidir `<clear/>` öğenin bir dizi öğesini yapılandırma dosyasından kaldırın.</span><span class="sxs-lookup"><span data-stu-id="b6d70-119">This is particularly important if you’re using the `<clear/>` element to remove a set of items from config.</span></span>

## <a name="specify-packages-folder-location"></a><span data-ttu-id="b6d70-120">'Paketleri' klasör konumunu belirtin</span><span class="sxs-lookup"><span data-stu-id="b6d70-120">Specify ‘packages’ Folder Location</span></span>

<span data-ttu-id="b6d70-121">Geçmişte, NuGet bilinen 'paketleri' klasöründen çözüm kök klasörü altında bulunan bir çözümün paketleri yönettiği.</span><span class="sxs-lookup"><span data-stu-id="b6d70-121">In the past, NuGet has managed a solution’s packages from a known ‘packages’ folder found beneath the solution root folder.</span></span>  <span data-ttu-id="b6d70-122">NuGet paketlerini, yüklü olan birçok farklı çözümü olan geliştirme ekipleri için bu dosya sisteminde pek çok farklı yerde yüklenen paketteki sonuçlanabilir.</span><span class="sxs-lookup"><span data-stu-id="b6d70-122">For development teams that have many different solutions which have NuGet packages installed, this can result in the same package being installed in many different places on the file system.</span></span>

<span data-ttu-id="b6d70-123">NuGet 2.1 paketleri klasörünün konumu üzerinde daha ayrıntılı denetim sağlar `repositoryPath` öğesinde `NuGet.Config` dosya.</span><span class="sxs-lookup"><span data-stu-id="b6d70-123">NuGet 2.1 provides more granular control over the location of the packages folder via the `repositoryPath` element in the `NuGet.Config` file.</span></span>  <span data-ttu-id="b6d70-124">Hiyerarşik Nuget.Config destek önceki örneği üzerinde oluşturma, tüm projeleri aynı paketleri klasörü C:\myteam\ paylaşmak istediğimiz varsayılır.</span><span class="sxs-lookup"><span data-stu-id="b6d70-124">Building on the previous example of hierarchical Nuget.Config support, assume that we wish to have all projects under C:\myteam\ share the same packages folder.</span></span>  <span data-ttu-id="b6d70-125">Bunu yapmak için aşağıdaki girişe eklemeniz yeterlidir `c:\myteam\Nuget.Config`.</span><span class="sxs-lookup"><span data-stu-id="b6d70-125">To accomplish this, simply add the following entry to `c:\myteam\Nuget.Config`.</span></span>

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

<span data-ttu-id="b6d70-126">Bu örnekte, paylaşılan `Nuget.Config` dosya C:\myteam derinliği bağımsız olarak oluşturulan her proje için bir paylaşılan paketleri klasörünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="b6d70-126">In this example, the shared `Nuget.Config` file specifies a shared packages folder for every project that is created beneath C:\myteam, regardless of depth.</span></span> <span data-ttu-id="b6d70-127">Var olan bir paket klasörü altında çözüm kökünüzde varsa, NuGet paketlerini yeni konuma yerleştirir önce VM'yi silmektir gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b6d70-127">Note that if you have an existing packages folder underneath your solution root, you need to delete it before NuGet will place packages in the new location.</span></span>

## <a name="support-for-portable-libraries"></a><span data-ttu-id="b6d70-128">Taşınabilir kitaplıklar için destek</span><span class="sxs-lookup"><span data-stu-id="b6d70-128">Support for Portable Libraries</span></span>

<span data-ttu-id="b6d70-129">[Taşınabilir kitaplıklar](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) ilk .NET 4,.NET Framework Windows Phone ve Xbox bile Silverlight'a sürümlerinden farklı Microsoft platformda değişiklik olmadan çalışan derlemeler oluşturmanıza olanak sağlayan ile sunulan bir özelliktir 360 (şu anda NuGet Xbox taşınabilir kitaplık hedefi desteklemiyor rağmen).</span><span class="sxs-lookup"><span data-stu-id="b6d70-129">[Portable libraries](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) is a feature first introduced with .NET 4 that enables you to build assemblies that can work without modification on different Microsoft platforms, from versions of the.NET Framework to Silverlight to Windows Phone and even Xbox 360 (though at this time, NuGet does not support the Xbox portable library target).</span></span>  <span data-ttu-id="b6d70-130">Genişleterek [paketini kuralları](../create-packages/supporting-multiple-target-frameworks.md) framework sürümleri ve profilleri, NuGet 2.1 artık taşınabilir kitaplıklar bileşik çerçevesi ve hedef profil olan paketleri oluşturmanızı sağlayarak destekler `lib` klasörleri.</span><span class="sxs-lookup"><span data-stu-id="b6d70-130">By extending the [package conventions](../create-packages/supporting-multiple-target-frameworks.md) for framework versions and profiles, NuGet 2.1 now supports portable libraries by enabling you to create packages that have compound framework and profile target `lib` folders.</span></span>

<span data-ttu-id="b6d70-131">Örneğin, aşağıdaki taşınabilir sınıf kitaplığının kullanılabilir hedef platformlar göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="b6d70-131">As an example, consider the following portable class library’s available target platforms.</span></span>

![Taşınabilir kitaplık oluşturma iletişim kutusu](./media/releasenotes-21-plib.png)

<span data-ttu-id="b6d70-133">Kitaplığı oluşturulduktan sonra ve komut `nuget.exe pack MyPortableProject.csproj` çalıştırılır, yeni taşınabilir kitaplık paketi klasör yapısı oluşturulan NuGet paketinin içeriği incelenerek herkes tarafından görülebilir.</span><span class="sxs-lookup"><span data-stu-id="b6d70-133">After the library is built and the command `nuget.exe pack MyPortableProject.csproj` is run, the new portable library package folder structure can be seen by examining the contents of the generated NuGet package.</span></span>

![Taşınabilir kitaplık paketi düzeni](./media/releasenotes-21-plib-layout.png)

<span data-ttu-id="b6d70-135">Gördüğünüz gibi taşınabilir kitaplık klasörü adı kuralını 'taşınabilir-{framework 1} + {framework n}' deseni burada mevcut framework tanımlayıcıları izleyin izleyen [framework adı ve sürümü kuralları](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="b6d70-135">As you can see, the portable library folder name convention follows the pattern ‘portable-{framework 1}+{framework n}’ where the framework identifiers follow the existing [framework name and version conventions](../reference/target-frameworks.md).</span></span> <span data-ttu-id="b6d70-136">Bir özel durum adı ve sürümü kuralları için Windows Phone için kullanılan çerçeve tanımlayıcısı dizininde bulunur.</span><span class="sxs-lookup"><span data-stu-id="b6d70-136">One exception to the name and version conventions is found in the framework identifier used for Windows Phone.</span></span>  <span data-ttu-id="b6d70-137">Bu ad, çerçeve adı 'wp' (wp7, wp71 veya wp8) kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b6d70-137">This moniker should use the framework name ‘wp’ (wp7, wp71 or wp8).</span></span> <span data-ttu-id="b6d70-138">'Silverlight-wp7' kullanarak, örneğin, bir hatayla sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="b6d70-138">Using ‘silverlight-wp7’, for example, will result in an error.</span></span>

<span data-ttu-id="b6d70-139">Bu klasör yapısından oluşturulan paketi yüklerken, NuGet klasör adı belirtildiği gibi birden çok hedefe artık kendi çerçevesi ve profili kuralları uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6d70-139">When installing the package that is created from this folder structure, NuGet can now apply its framework and profile rules to multiple targets, as specified in the folder name.</span></span>  <span data-ttu-id="b6d70-140">NuGet'ın eşleştirme kuralları "ayrıntılı" hedef "daha az özel" olanları öncelik kazanır ilkesidir.</span><span class="sxs-lookup"><span data-stu-id="b6d70-140">Behind NuGet’s matching rules is the principle that “more specific” targets will take precedence over “less specific” ones.</span></span>  <span data-ttu-id="b6d70-141">Bu hem de bir proje ile uyumlu olmaları durumunda belirli bir platformu hedefleyen adlar her zaman taşınabilir olanları tercih edilen anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="b6d70-141">This means that monikers targeting a specific platform will always be preferred over portable ones if they are both compatible with a project.</span></span>  <span data-ttu-id="b6d70-142">Ayrıca, birden çok taşınabilir hedefi bir proje ile uyumlu ise NuGet desteklenen platformlar kümesi "Bu paketi projeye en yakın" olduğu bir tercih eder.</span><span class="sxs-lookup"><span data-stu-id="b6d70-142">Additionally, if multiple portable targets are compatible with a project, NuGet will prefer the one where the set of platforms supported is “closest” to the project referencing the package.</span></span>

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a><span data-ttu-id="b6d70-143">Hedefleme Windows 8 ve Windows Phone 8 projeleri</span><span class="sxs-lookup"><span data-stu-id="b6d70-143">Targeting Windows 8 and Windows Phone 8 Projects</span></span>

<span data-ttu-id="b6d70-144">Taşınabilir kitaplık projelerine hedeflemek için destek eklemenin yanı sıra, NuGet 2.1 yeni framework bilinen adlar için hem Windows 8 Store hem de Windows Phone 8 projeleri yanı sıra, Windows Store ve olacak Windows Phone projeleri için bazı yeni genel adlar sağlar gelecekteki sürümleri ilgili platformlar arasında yönetmek daha kolay.</span><span class="sxs-lookup"><span data-stu-id="b6d70-144">In addition to adding support for targeting portable library projects, NuGet 2.1 provides new framework monikers for both Windows 8 Store and Windows Phone 8 projects, as well as some new general monikers for Windows Store and Windows Phone projects that will be easier to manage across future versions of the respective platforms.</span></span>

<span data-ttu-id="b6d70-145">Windows 8 Store uygulamaları için tanımlayıcıları aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="b6d70-145">For Windows 8 Store applications, the identifiers look as follows:</span></span>

| <span data-ttu-id="b6d70-146">NuGet 2.0 ve daha önceki</span><span class="sxs-lookup"><span data-stu-id="b6d70-146">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="b6d70-147">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="b6d70-147">NuGet 2.1</span></span> |
| ---------------- | ----------- |
| <span data-ttu-id="b6d70-148">winRT45. NETCore45</span><span class="sxs-lookup"><span data-stu-id="b6d70-148">winRT45, .NETCore45</span></span> | <span data-ttu-id="b6d70-149">Windows, Windows8, win, win8</span><span class="sxs-lookup"><span data-stu-id="b6d70-149">Windows, Windows8, win, win8</span></span> |

<br/>
<span data-ttu-id="b6d70-150">Windows Phone projeleri için tanımlayıcıları aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="b6d70-150">For Windows Phone projects, the identifiers look as follows:</span></span>

| <span data-ttu-id="b6d70-151">Phone işletim sistemi</span><span class="sxs-lookup"><span data-stu-id="b6d70-151">Phone OS</span></span> | <span data-ttu-id="b6d70-152">NuGet 2.0 ve daha önceki</span><span class="sxs-lookup"><span data-stu-id="b6d70-152">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="b6d70-153">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="b6d70-153">NuGet 2.1</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b6d70-154">Windows Phone 7</span><span class="sxs-lookup"><span data-stu-id="b6d70-154">Windows Phone 7</span></span> | <span data-ttu-id="b6d70-155">silverlight3 wp</span><span class="sxs-lookup"><span data-stu-id="b6d70-155">silverlight3-wp</span></span> | <span data-ttu-id="b6d70-156">WP, wp7, WindowsPhone, WindowsPhone7</span><span class="sxs-lookup"><span data-stu-id="b6d70-156">wp, wp7, WindowsPhone, WindowsPhone7</span></span> |
| <span data-ttu-id="b6d70-157">Windows Phone 7.5 (Mango)</span><span class="sxs-lookup"><span data-stu-id="b6d70-157">Windows Phone 7.5 (Mango)</span></span> | <span data-ttu-id="b6d70-158">silverlight4 wp71</span><span class="sxs-lookup"><span data-stu-id="b6d70-158">silverlight4-wp71</span></span> | <span data-ttu-id="b6d70-159">wp71, WindowsPhone71</span><span class="sxs-lookup"><span data-stu-id="b6d70-159">wp71, WindowsPhone71</span></span> |
| <span data-ttu-id="b6d70-160">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="b6d70-160">Windows Phone 8</span></span> | <span data-ttu-id="b6d70-161">(desteklenmiyor)</span><span class="sxs-lookup"><span data-stu-id="b6d70-161">(not supported)</span></span> | <span data-ttu-id="b6d70-162">wp8, WindowsPhone8</span><span class="sxs-lookup"><span data-stu-id="b6d70-162">wp8, WindowsPhone8</span></span> |

<br/>
<span data-ttu-id="b6d70-163">Tüm yukarıdaki değişiklikleri eski framework adları NuGet 2.1 tarafından tam olarak desteklenmeye devam edecektir.</span><span class="sxs-lookup"><span data-stu-id="b6d70-163">In all of the above changes, the old framework names will continue to be fully supported by NuGet 2.1.</span></span>  <span data-ttu-id="b6d70-164">Bunlar gelecek sürümleri ilgili platformlar arasında daha kararlı olacaktır gibi ilerletme, yeni adları kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b6d70-164">Moving forward, the new names should be used as they will be more stable across future versions of the respective platforms.</span></span> <span data-ttu-id="b6d70-165">Yeni adlar olur *değil* olması 2.1 önce NuGet sürümlerinde desteklenir, ancak, bu nedenle buna göre planlayın geçiş yapmak ne zaman.</span><span class="sxs-lookup"><span data-stu-id="b6d70-165">The new names will *not* be supported in versions of NuGet prior to 2.1, however, so plan accordingly for when to make the switch.</span></span>

## <a name="improved-search-in-package-manager-dialog"></a><span data-ttu-id="b6d70-166">Paket Yöneticisi iletişim kutusunda geliştirilmiş arama</span><span class="sxs-lookup"><span data-stu-id="b6d70-166">Improved Search in Package Manager Dialog</span></span>

<span data-ttu-id="b6d70-167">Son birkaç yineleme büyük ölçüde geliştirilmiş hız ve paket aramalarınızı ilgi NuGet galerisinde değişiklikleri tanıtılmıştır.</span><span class="sxs-lookup"><span data-stu-id="b6d70-167">Over the past several iterations, changes have been introduced to the NuGet gallery that greatly improved the speed and relevance of package searches.</span></span>  <span data-ttu-id="b6d70-168">Ancak, bu geliştirmeler nuget.org Web sitesine sınırlıydı.</span><span class="sxs-lookup"><span data-stu-id="b6d70-168">However, these improvements were limited to the nuget.org Web site.</span></span>  <span data-ttu-id="b6d70-169">NuGet 2.1 geliştirilmiş arama deneyimi NuGet Paket Yöneticisi iletişim kutusu kullanılabilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="b6d70-169">NuGet 2.1 makes the improved search experience available through the NuGet package manager dialog.</span></span>  <span data-ttu-id="b6d70-170">Örneğin, Windows Azure önbelleğe almayı Önizleme paketi bulmak istediğinizi düşünelim.</span><span class="sxs-lookup"><span data-stu-id="b6d70-170">As an example, imagine that you wanted to find the Windows Azure Caching Preview package.</span></span>  <span data-ttu-id="b6d70-171">Bu paket için makul bir arama sorgusu, "Azure Cache" olabilir.</span><span class="sxs-lookup"><span data-stu-id="b6d70-171">A reasonable search query for this package may be “Azure Cache”.</span></span>  <span data-ttu-id="b6d70-172">Paket Yöneticisi iletişim kutusu önceki sürümlerinde, istenen paket bile sonuçları'nın ilk sayfasında listelenir değil.</span><span class="sxs-lookup"><span data-stu-id="b6d70-172">In previous versions of the package manager dialog, the desired package would not even be listed on the first page of results.</span></span>  <span data-ttu-id="b6d70-173">Ancak, NuGet 2.1 içinde istenen paket artık arama sonuçları en üstünde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="b6d70-173">However, in NuGet 2.1, the desired package now shows up at the top of the search results.</span></span>

![Paket Yöneticisi iletişim arama](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a><span data-ttu-id="b6d70-175">Paket güncelleştirme zorla</span><span class="sxs-lookup"><span data-stu-id="b6d70-175">Force Package Update</span></span>

<span data-ttu-id="b6d70-176">NuGet 2.1 önce NuGet olmadığından değiştirildiği bir paketin güncelleştirilmesi atlarsınız yüksek sürüm numarası.</span><span class="sxs-lookup"><span data-stu-id="b6d70-176">Prior to NuGet 2.1, NuGet would skip updating a package when there was a not a high version number.</span></span>  <span data-ttu-id="b6d70-177">Bu, özellikle nerede takım Paket sürümü ile her yapı numarası artırmak için istemediğiniz derleme veya CI senaryoları durumunda belirli senaryoları uyuşmazlıkları kullanıma sunuldu.</span><span class="sxs-lookup"><span data-stu-id="b6d70-177">This introduced friction for certain scenarios – particularly in the case of build or CI scenarios where the team did not want to increment the package version number with each build.</span></span>  <span data-ttu-id="b6d70-178">Bir güncelleştirme bakılmaksızın zorlamak için istenen davranışı oluştu.</span><span class="sxs-lookup"><span data-stu-id="b6d70-178">The desired behavior was to force an update regardless.</span></span>  <span data-ttu-id="b6d70-179">NuGet 2.1 'yeniden' bayrağına sahip'yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="b6d70-179">NuGet 2.1 addresses this with the ‘reinstall’ flag.</span></span>  <span data-ttu-id="b6d70-180">Örneğin, önceki NuGet sürümleri aşağıdaki daha yeni bir paket sürümü sahip bir paketi güncelleştirmeye çalışırken neden olur:</span><span class="sxs-lookup"><span data-stu-id="b6d70-180">For example, previous versions of NuGet would result in the following when attempting to update a package that did not have a more recent package version:</span></span>

    PM> Update-Package Moq
    No updates available for 'Moq' in project 'MySolution.MyConsole'.

<span data-ttu-id="b6d70-181">Yeniden bayrağıyla paket olup olmamasına bakılmaksızın güncelleştirilecek daha yeni bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="b6d70-181">With the reinstall flag, the package will be updated regardless of whether there is a newer version.</span></span>

    PM> Update-Package Moq -Reinstall
    Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
    Successfully uninstalled 'Moq 4.0.10827'.
    Successfully installed 'Moq 4.0.10827'.
    Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.

<span data-ttu-id="b6d70-182">Burada yeniden bayrağı yararlı kanıtlar başka bir senaryo framework yeniden hedefleme olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="b6d70-182">Another scenario where the reinstall flag proves beneficial is that of framework re-targeting.</span></span> <span data-ttu-id="b6d70-183">Bir projeden (örneğin, .NET 4.5 için .NET 4), hedef Framework'ü değiştirilirken Update-Package-yeniden projede yüklü tüm NuGet paketlerinin doğru derlemelerine başvurular güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6d70-183">When changing the target framework of a project (for example, from .NET 4 to .NET 4.5), Update-Package -Reinstall can update references to the correct assemblies for all NuGet packages installed in the project.</span></span>

## <a name="edit-package-sources-within-visual-studio"></a><span data-ttu-id="b6d70-184">Paket kaynaklarını Visual Studio'dan Düzenle</span><span class="sxs-lookup"><span data-stu-id="b6d70-184">Edit Package Sources Within Visual Studio</span></span>

<span data-ttu-id="b6d70-185">NuGet önceki sürümlerinde, silme ve paket kaynağı yeniden ekleyerek gerekli Visual Studio Seçenekleri iletişim kutusu içinde bir paket kaynağından güncelleştiriliyor.</span><span class="sxs-lookup"><span data-stu-id="b6d70-185">In previous versions of NuGet, updating a package source from within the Visual Studio options dialog required deleting and re-adding the package source.</span></span>  <span data-ttu-id="b6d70-186">NuGet 2.1, bu iş akışı Yapılandırması kullanıcı arabirimi birinci sınıf bir işlev olarak güncelleştirme destekleyerek artırır.</span><span class="sxs-lookup"><span data-stu-id="b6d70-186">NuGet 2.1 improves this workflow by supporting update as a first class function of the configuration user interface.</span></span>

![Paket Yöneticisi'ni yapılandırma iletişim kutusu](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="b6d70-188">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="b6d70-188">Bug Fixes</span></span>

<span data-ttu-id="b6d70-189">NuGet 2.1 birçok hata düzeltmeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="b6d70-189">NuGet 2.1 includes many bug fixes.</span></span> <span data-ttu-id="b6d70-190">Tam bir listesi için iş öğeleri NuGet 2. 0'da, lütfen görünümü sabit [bu sürüm için NuGet sorun İzleyicisi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="b6d70-190">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
