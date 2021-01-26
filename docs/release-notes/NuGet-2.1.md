---
title: NuGet 2,1 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 2,1 sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c44ad32c8c4018ccb517b41bffda674eef1f11f3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777027"
---
# <a name="nuget-21-release-notes"></a><span data-ttu-id="67f86-103">NuGet 2,1 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="67f86-103">NuGet 2.1 Release Notes</span></span>

<span data-ttu-id="67f86-104">[NuGet 2,0 sürüm notları](../release-notes/nuget-2.0.md)  |  [NuGet 2,2 sürüm notları](../release-notes/nuget-2.2.md)</span><span class="sxs-lookup"><span data-stu-id="67f86-104">[NuGet 2.0 Release Notes](../release-notes/nuget-2.0.md) | [NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md)</span></span>

<span data-ttu-id="67f86-105">NuGet 2,1, 4 Ekim 2012 ' de yayımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="67f86-105">NuGet 2.1 was released on October 4, 2012.</span></span>

## <a name="hierarchical-nugetconfig"></a><span data-ttu-id="67f86-106">Hiyerarşik Nuget.Config</span><span class="sxs-lookup"><span data-stu-id="67f86-106">Hierarchical Nuget.Config</span></span>

<span data-ttu-id="67f86-107">NuGet 2,1, `NuGet.Config` dosyaları bulmak ve sonra bulunan tüm dosyalar kümesinden yapılandırmayı oluşturmak için, NuGet ayarlarını Denetim konusunda daha fazla esneklik sağlar.</span><span class="sxs-lookup"><span data-stu-id="67f86-107">NuGet 2.1 gives you greater flexibility in controlling NuGet settings by way of recursively walking up the folder structure looking for `NuGet.Config` files and then building the configuration from the set of all found files.</span></span>  <span data-ttu-id="67f86-108">Örnek olarak, bir ekibin diğer iç bağımlılıkların CI derlemeleri için iç paket deposuna sahip olduğu senaryoyu göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="67f86-108">As an example, consider the scenario where a team has an internal package repository for CI builds of other internal dependencies.</span></span> <span data-ttu-id="67f86-109">Tek bir projenin klasör yapısı aşağıdaki gibi görünebilir:</span><span class="sxs-lookup"><span data-stu-id="67f86-109">The folder structure for an individual project might look like the following:</span></span>

```
C:\
C:\myteam\
C:\myteam\solution1
C:\myteam\solution1\project1
```

<span data-ttu-id="67f86-110">Ayrıca, çözüm için paket geri yüklemesi etkinleştirilmişse, aşağıdaki klasör de mevcuttur:</span><span class="sxs-lookup"><span data-stu-id="67f86-110">Additionally, if package restore is enabled for the solution, the following folder will also exist:</span></span>

```
C:\myteam\solution1\.nuget
```

<span data-ttu-id="67f86-111">Takımın çalıştığı tüm projeler için ekibin iç paket deposunu kullanabilmesi için, bu dosyayı makinedeki her proje için kullanılabilir hale getirmekle, yeni bir Nuget.Config dosyası oluşturabilir ve c:\Team klasörüne yerleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="67f86-111">In order to have the team’s internal package repository available for all projects that the team works on, while not making it available for every project on the machine, we can create a new Nuget.Config file and place it in the c:\myteam folder.</span></span> <span data-ttu-id="67f86-112">Her proje için bir paket klasörünü specificbir yol yoktur.</span><span class="sxs-lookup"><span data-stu-id="67f86-112">There is no way to specificy a packages folder per project.</span></span>

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

<span data-ttu-id="67f86-113">Şimdi, aşağıda gösterildiği gibi c:\myteam altındaki herhangi bir klasörden ' nuget.exe Sources ' komutunu çalıştırarak kaynağın eklendiğini görebiliriz:</span><span class="sxs-lookup"><span data-stu-id="67f86-113">We can now see that the source was added by running the ‘nuget.exe sources’ command from any folder beneath c:\myteam as shown below:</span></span>

![Üst NuGet yapılandırmadan paket kaynakları](./media/releasenotes-21-cfg-hierarchy.png)

<span data-ttu-id="67f86-115">`NuGet.Config` dosyalar aşağıdaki sırayla aranır:</span><span class="sxs-lookup"><span data-stu-id="67f86-115">`NuGet.Config` files are searched for in the following order:</span></span>

1. `.nuget\Nuget.Config`
2. <span data-ttu-id="67f86-116">Proje klasöründen köke özyinelemeli ilerleme</span><span class="sxs-lookup"><span data-stu-id="67f86-116">Recursive walk from project folder to root</span></span>
3. <span data-ttu-id="67f86-117">Global `Nuget.Config` ( `%appdata%\NuGet\Nuget.Config` )</span><span class="sxs-lookup"><span data-stu-id="67f86-117">Global `Nuget.Config` (`%appdata%\NuGet\Nuget.Config`)</span></span>

<span data-ttu-id="67f86-118">Konfigürasyonlar *ters sırada* uygulanmasından, Yani yukarıdaki sıralamaya bağlı olarak, genel Nuget.Config önce uygulanır ve ardından kök 'ten proje klasörüne ve ardından tarafından oluşturulan Nuget.Config dosyalar gelmelidir `.nuget\Nuget.Config` .</span><span class="sxs-lookup"><span data-stu-id="67f86-118">The configurations are than applied in the *reverse order*, meaning that based on the above ordering, the global Nuget.Config would be applied first, followed by the discovered Nuget.Config files from root to project folder, followed by `.nuget\Nuget.Config`.</span></span>  <span data-ttu-id="67f86-119">Bu, `<clear/>` bir öğe kümesini yapılandırmadan kaldırmak için öğesini kullanıyorsanız özellikle önemlidir.</span><span class="sxs-lookup"><span data-stu-id="67f86-119">This is particularly important if you’re using the `<clear/>` element to remove a set of items from config.</span></span>

## <a name="specify-packages-folder-location"></a><span data-ttu-id="67f86-120">' Paketlerin ' klasör konumunu belirtin</span><span class="sxs-lookup"><span data-stu-id="67f86-120">Specify ‘packages’ Folder Location</span></span>

<span data-ttu-id="67f86-121">Geçmişte, NuGet çözüm kök klasörü altında bulunan bilinen bir ' Packages ' klasöründen bir çözümün paketlerini yönetilemiştir.</span><span class="sxs-lookup"><span data-stu-id="67f86-121">In the past, NuGet has managed a solution’s packages from a known ‘packages’ folder found beneath the solution root folder.</span></span>  <span data-ttu-id="67f86-122">NuGet paketleri yüklü olan çok sayıda farklı çözümü olan geliştirme ekiplerinde, bu paket, dosya sistemindeki birçok farklı yere aynı paketin yüklenmesini sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="67f86-122">For development teams that have many different solutions which have NuGet packages installed, this can result in the same package being installed in many different places on the file system.</span></span>

<span data-ttu-id="67f86-123">NuGet 2,1, dosyadaki öğesi aracılığıyla Packages klasörünün konumu üzerinde daha ayrıntılı denetim sağlar `repositoryPath` `NuGet.Config` .</span><span class="sxs-lookup"><span data-stu-id="67f86-123">NuGet 2.1 provides more granular control over the location of the packages folder via the `repositoryPath` element in the `NuGet.Config` file.</span></span>  <span data-ttu-id="67f86-124">Önceki hiyerarşik Nuget.Config desteğinin örneğini oluşturmak, C:\team\ ' ın altındaki tüm projelerin aynı paketler klasörünü paylaşmasını istediğinizi varsayalım.</span><span class="sxs-lookup"><span data-stu-id="67f86-124">Building on the previous example of hierarchical Nuget.Config support, assume that we wish to have all projects under C:\myteam\ share the same packages folder.</span></span>  <span data-ttu-id="67f86-125">Bunu gerçekleştirmek için aşağıdaki girdiyi öğesine eklemeniz yeterlidir `c:\myteam\Nuget.Config` .</span><span class="sxs-lookup"><span data-stu-id="67f86-125">To accomplish this, simply add the following entry to `c:\myteam\Nuget.Config`.</span></span>

```xml
<configuration>
    <config>
    <add key="repositoryPath" value="C:\myteam\teampackages" />
    </config>
    ...
</configuration>
```

<span data-ttu-id="67f86-126">Bu örnekte, paylaşılan dosya, `Nuget.Config` derinliğinden bağımsız olarak C:\myteam altında oluşturulan her proje için paylaşılan paketler klasörünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="67f86-126">In this example, the shared `Nuget.Config` file specifies a shared packages folder for every project that is created beneath C:\myteam, regardless of depth.</span></span> <span data-ttu-id="67f86-127">Çözüm kökünün altında var olan bir paket klasörünüz varsa, NuGet paketleri yeni konuma yerleştirebilmeniz için bunu silmeniz gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="67f86-127">Note that if you have an existing packages folder underneath your solution root, you need to delete it before NuGet will place packages in the new location.</span></span>

## <a name="support-for-portable-libraries"></a><span data-ttu-id="67f86-128">Taşınabilir kitaplıklar için destek</span><span class="sxs-lookup"><span data-stu-id="67f86-128">Support for Portable Libraries</span></span>

<span data-ttu-id="67f86-129">[Taşınabilir kitaplıklar](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) , .NET 4 ' te ilk kez sunulan ve The.NET Framework sürümlerinden Silverlight 'e Windows Phone ve hatta Xbox 360 ' ye (Şu anda NuGet, Xbox taşınabilir kitaplık hedefini desteklemez) farklı Microsoft platformları üzerinde değişiklik yapılmaksızın çalışabilen derlemeler oluşturmanıza olanak tanıyan bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="67f86-129">[Portable libraries](/dotnet/standard/cross-platform/cross-platform-development-with-the-portable-class-library) is a feature first introduced with .NET 4 that enables you to build assemblies that can work without modification on different Microsoft platforms, from versions of the.NET Framework to Silverlight to Windows Phone and even Xbox 360 (though at this time, NuGet does not support the Xbox portable library target).</span></span>  <span data-ttu-id="67f86-130">NuGet 2,1, Framework sürümleri ve profilleri için [paket kurallarını](../create-packages/supporting-multiple-target-frameworks.md) genişleterek artık bileşik çerçeve ve profil hedef klasörlerine sahip paketler oluşturmanızı sağlayarak taşınabilir kitaplıkları desteklemektedir `lib` .</span><span class="sxs-lookup"><span data-stu-id="67f86-130">By extending the [package conventions](../create-packages/supporting-multiple-target-frameworks.md) for framework versions and profiles, NuGet 2.1 now supports portable libraries by enabling you to create packages that have compound framework and profile target `lib` folders.</span></span>

<span data-ttu-id="67f86-131">Örnek olarak, aşağıdaki taşınabilir sınıf kitaplığının kullanılabilir hedef platformlarını göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="67f86-131">As an example, consider the following portable class library’s available target platforms.</span></span>

![Taşınabilir kitaplık oluşturma iletişim kutusu](./media/releasenotes-21-plib.png)

<span data-ttu-id="67f86-133">Kitaplık oluşturulduktan ve komut `nuget.exe pack MyPortableProject.csproj` çalıştırıldıktan sonra, yeni taşınabilir kitaplık paketi klasör yapısı oluşturulan NuGet paketinin içeriği incelenerek görülebilir.</span><span class="sxs-lookup"><span data-stu-id="67f86-133">After the library is built and the command `nuget.exe pack MyPortableProject.csproj` is run, the new portable library package folder structure can be seen by examining the contents of the generated NuGet package.</span></span>

![Taşınabilir Kitaplık paket düzeni](./media/releasenotes-21-plib-layout.png)

<span data-ttu-id="67f86-135">Görebileceğiniz gibi, taşınabilir kitaplık klasörü adı kuralı, çerçeve tanımlayıcılarının mevcut [çerçeve adı ve sürüm kurallarını](../reference/target-frameworks.md)izlediği ' Portable-{Framework 1} + {Framework n} ' düzenine uyar.</span><span class="sxs-lookup"><span data-stu-id="67f86-135">As you can see, the portable library folder name convention follows the pattern ‘portable-{framework 1}+{framework n}’ where the framework identifiers follow the existing [framework name and version conventions](../reference/target-frameworks.md).</span></span> <span data-ttu-id="67f86-136">Windows Phone için kullanılan çerçeve tanımlayıcıda ad ve sürüm kuralları için bir özel durum bulundu.</span><span class="sxs-lookup"><span data-stu-id="67f86-136">One exception to the name and version conventions is found in the framework identifier used for Windows Phone.</span></span>  <span data-ttu-id="67f86-137">Bu bilinen ad, ' wp ' çerçeve adını (WP7, wp71 veya WP8) kullanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="67f86-137">This moniker should use the framework name ‘wp’ (wp7, wp71 or wp8).</span></span> <span data-ttu-id="67f86-138">Örneğin, ' Silverlight-WP7 ' kullanılması bir hatayla sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="67f86-138">Using ‘silverlight-wp7’, for example, will result in an error.</span></span>

<span data-ttu-id="67f86-139">Bu klasör yapısından oluşturulan paketi yüklerken, NuGet artık çerçeve ve profil kurallarını, klasör adında belirtildiği gibi birden çok hedefe uygulayabilir.</span><span class="sxs-lookup"><span data-stu-id="67f86-139">When installing the package that is created from this folder structure, NuGet can now apply its framework and profile rules to multiple targets, as specified in the folder name.</span></span>  <span data-ttu-id="67f86-140">NuGet 'in eşleşen kurallarının arkasında "daha belirgin" hedeflerin "daha az spesifik" olarak öncelikli olduğu prensip.</span><span class="sxs-lookup"><span data-stu-id="67f86-140">Behind NuGet’s matching rules is the principle that “more specific” targets will take precedence over “less specific” ones.</span></span>  <span data-ttu-id="67f86-141">Bu, belirli bir platformu hedefleyen bilinen adların, her ikisi de proje ile uyumluysa taşınabilir dosyalar üzerinde her zaman tercih edildiği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="67f86-141">This means that monikers targeting a specific platform will always be preferred over portable ones if they are both compatible with a project.</span></span>  <span data-ttu-id="67f86-142">Ayrıca, birden çok taşınabilir hedef bir proje ile uyumluysa NuGet, desteklenen platform kümesinin pakete başvuran projeye "en yakın" olduğu bir tane tercih eder.</span><span class="sxs-lookup"><span data-stu-id="67f86-142">Additionally, if multiple portable targets are compatible with a project, NuGet will prefer the one where the set of platforms supported is “closest” to the project referencing the package.</span></span>

## <a name="targeting-windows-8-and-windows-phone-8-projects"></a><span data-ttu-id="67f86-143">Windows 8 ve Windows Phone 8 projelerini hedefleme</span><span class="sxs-lookup"><span data-stu-id="67f86-143">Targeting Windows 8 and Windows Phone 8 Projects</span></span>

<span data-ttu-id="67f86-144">NuGet 2,1, taşınabilir kitaplık projelerini hedeflemek için destek eklemenin yanı sıra hem Windows 8 Mağazası hem de Windows Phone 8 projeleri için yeni çerçeve adları ve Windows Mağazası için yeni genel adlar ve ilgili platformların gelecek sürümlerinde daha kolay Yönetilecek projeler için de Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="67f86-144">In addition to adding support for targeting portable library projects, NuGet 2.1 provides new framework monikers for both Windows 8 Store and Windows Phone 8 projects, as well as some new general monikers for Windows Store and Windows Phone projects that will be easier to manage across future versions of the respective platforms.</span></span>

<span data-ttu-id="67f86-145">Windows 8 Mağaza uygulamaları için tanımlayıcılar şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="67f86-145">For Windows 8 Store applications, the identifiers look as follows:</span></span>

| <span data-ttu-id="67f86-146">NuGet 2,0 ve öncesi</span><span class="sxs-lookup"><span data-stu-id="67f86-146">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="67f86-147">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="67f86-147">NuGet 2.1</span></span> |
| ---------------- | ----------- |
| <span data-ttu-id="67f86-148">winRT45, . NETCore45</span><span class="sxs-lookup"><span data-stu-id="67f86-148">winRT45, .NETCore45</span></span> | <span data-ttu-id="67f86-149">Windows, Windows8, Win, Win8</span><span class="sxs-lookup"><span data-stu-id="67f86-149">Windows, Windows8, win, win8</span></span> |

<br/>
<span data-ttu-id="67f86-150">Windows Phone projeleri için, tanımlayıcılar şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="67f86-150">For Windows Phone projects, the identifiers look as follows:</span></span>

| <span data-ttu-id="67f86-151">Telefon OS</span><span class="sxs-lookup"><span data-stu-id="67f86-151">Phone OS</span></span> | <span data-ttu-id="67f86-152">NuGet 2,0 ve öncesi</span><span class="sxs-lookup"><span data-stu-id="67f86-152">NuGet 2.0 and earlier</span></span> | <span data-ttu-id="67f86-153">NuGet 2.1</span><span class="sxs-lookup"><span data-stu-id="67f86-153">NuGet 2.1</span></span> |
| --- | --- | --- |
| <span data-ttu-id="67f86-154">Windows Phone 7</span><span class="sxs-lookup"><span data-stu-id="67f86-154">Windows Phone 7</span></span> | <span data-ttu-id="67f86-155">silverlight3-WP</span><span class="sxs-lookup"><span data-stu-id="67f86-155">silverlight3-wp</span></span> | <span data-ttu-id="67f86-156">WP, wp7, WindowsPhone, WindowsPhone7</span><span class="sxs-lookup"><span data-stu-id="67f86-156">wp, wp7, WindowsPhone, WindowsPhone7</span></span> |
| <span data-ttu-id="67f86-157">Windows Phone 7,5 (Mango)</span><span class="sxs-lookup"><span data-stu-id="67f86-157">Windows Phone 7.5 (Mango)</span></span> | <span data-ttu-id="67f86-158">silverlight4-wp71</span><span class="sxs-lookup"><span data-stu-id="67f86-158">silverlight4-wp71</span></span> | <span data-ttu-id="67f86-159">wp71, WindowsPhone71</span><span class="sxs-lookup"><span data-stu-id="67f86-159">wp71, WindowsPhone71</span></span> |
| <span data-ttu-id="67f86-160">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="67f86-160">Windows Phone 8</span></span> | <span data-ttu-id="67f86-161">(desteklenmiyor)</span><span class="sxs-lookup"><span data-stu-id="67f86-161">(not supported)</span></span> | <span data-ttu-id="67f86-162">WP8, WindowsPhone8</span><span class="sxs-lookup"><span data-stu-id="67f86-162">wp8, WindowsPhone8</span></span> |

<br/>
<span data-ttu-id="67f86-163">Yukarıdaki değişikliklerin tümünde, eski Framework adları NuGet 2,1 tarafından tam olarak desteklenmeye devam edecektir.</span><span class="sxs-lookup"><span data-stu-id="67f86-163">In all of the above changes, the old framework names will continue to be fully supported by NuGet 2.1.</span></span>  <span data-ttu-id="67f86-164">İleri doğru, yeni adların ilgili platformların gelecekteki sürümlerinde daha kararlı olacağı için kullanılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="67f86-164">Moving forward, the new names should be used as they will be more stable across future versions of the respective platforms.</span></span> <span data-ttu-id="67f86-165">Yeni adlar 2,1 ' den önceki NuGet sürümlerinde *desteklenmeyecektir, bu nedenle* anahtarın ne zaman olacağını planlayın.</span><span class="sxs-lookup"><span data-stu-id="67f86-165">The new names will *not* be supported in versions of NuGet prior to 2.1, however, so plan accordingly for when to make the switch.</span></span>

## <a name="improved-search-in-package-manager-dialog"></a><span data-ttu-id="67f86-166">Paket Yöneticisi Iletişim kutusunda geliştirilmiş arama</span><span class="sxs-lookup"><span data-stu-id="67f86-166">Improved Search in Package Manager Dialog</span></span>

<span data-ttu-id="67f86-167">Son birkaç yinelemeden sonra, paket aramalarının hızını ve uygunluğunu büyük ölçüde artıran NuGet galerisine değişiklikler yapılmıştır.</span><span class="sxs-lookup"><span data-stu-id="67f86-167">Over the past several iterations, changes have been introduced to the NuGet gallery that greatly improved the speed and relevance of package searches.</span></span>  <span data-ttu-id="67f86-168">Ancak, bu iyileştirmeler nuget.org Web sitesiyle sınırlandırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="67f86-168">However, these improvements were limited to the nuget.org Web site.</span></span>  <span data-ttu-id="67f86-169">NuGet 2,1, NuGet Paket Yöneticisi iletişim kutusunda geliştirilmiş arama deneyimini kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="67f86-169">NuGet 2.1 makes the improved search experience available through the NuGet package manager dialog.</span></span>  <span data-ttu-id="67f86-170">Örnek olarak, Windows Azure önbelleğe alma önizleme paketini bulmak istediğinizi düşünün.</span><span class="sxs-lookup"><span data-stu-id="67f86-170">As an example, imagine that you wanted to find the Windows Azure Caching Preview package.</span></span>  <span data-ttu-id="67f86-171">Bu paket için makul bir arama sorgusu "Azure önbelleği" olabilir.</span><span class="sxs-lookup"><span data-stu-id="67f86-171">A reasonable search query for this package may be “Azure Cache”.</span></span>  <span data-ttu-id="67f86-172">Paket Yöneticisi iletişim kutusunun önceki sürümlerinde, istenen paket sonuçların ilk sayfasında da listelenmemelidir.</span><span class="sxs-lookup"><span data-stu-id="67f86-172">In previous versions of the package manager dialog, the desired package would not even be listed on the first page of results.</span></span>  <span data-ttu-id="67f86-173">Ancak, NuGet 2,1 ' de, istenen paket artık arama sonuçlarının en üstünde görünür.</span><span class="sxs-lookup"><span data-stu-id="67f86-173">However, in NuGet 2.1, the desired package now shows up at the top of the search results.</span></span>

![Paket Yöneticisi iletişim kutusu arama](./media/releasenotes-21-vsdlg-search.png)

## <a name="force-package-update"></a><span data-ttu-id="67f86-175">Paket güncelleştirmesine zorla</span><span class="sxs-lookup"><span data-stu-id="67f86-175">Force Package Update</span></span>

<span data-ttu-id="67f86-176">NuGet 2,1 ' den önce, büyük bir sürüm numarası olmadığında NuGet bir paketin güncelleştirilmesini atlar.</span><span class="sxs-lookup"><span data-stu-id="67f86-176">Prior to NuGet 2.1, NuGet would skip updating a package when there was a not a high version number.</span></span>  <span data-ttu-id="67f86-177">Bu, özellikle ekibin her bir derleme ile paket sürüm numarasını artırmak istememediği belirli senaryolar için ortaya çıkan, özellikle de derleme veya CI senaryolarında tanıtılmıştır.</span><span class="sxs-lookup"><span data-stu-id="67f86-177">This introduced friction for certain scenarios – particularly in the case of build or CI scenarios where the team did not want to increment the package version number with each build.</span></span>  <span data-ttu-id="67f86-178">İstenen davranış, bir güncelleştirmeyi bağımsız olarak zorlamaktır.</span><span class="sxs-lookup"><span data-stu-id="67f86-178">The desired behavior was to force an update regardless.</span></span>  <span data-ttu-id="67f86-179">NuGet 2,1 bunu ' REINSTALL ' bayrağıyla gidermektedir.</span><span class="sxs-lookup"><span data-stu-id="67f86-179">NuGet 2.1 addresses this with the ‘reinstall’ flag.</span></span>  <span data-ttu-id="67f86-180">Örneğin, NuGet 'in önceki sürümleri, daha yeni bir paket sürümüne sahip olmayan bir paketi güncelleştirmeye çalışırken aşağıdakiler ile sonuçlanır:</span><span class="sxs-lookup"><span data-stu-id="67f86-180">For example, previous versions of NuGet would result in the following when attempting to update a package that did not have a more recent package version:</span></span>

```
PM> Update-Package Moq
No updates available for 'Moq' in project 'MySolution.MyConsole'.
```

<span data-ttu-id="67f86-181">Yeniden yükleme bayrağıyla, daha yeni bir sürüm olup olmamasına bakılmaksızın paket güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="67f86-181">With the reinstall flag, the package will be updated regardless of whether there is a newer version.</span></span>

```
PM> Update-Package Moq -Reinstall
Successfully removed 'Moq 4.0.10827' from MySolution.MyConsole.
Successfully uninstalled 'Moq 4.0.10827'.
Successfully installed 'Moq 4.0.10827'.
Successfully added 'Moq 4.0.10827' to MySolution.MyConsole.
```

<span data-ttu-id="67f86-182">Yeniden yükleme bayrağının yararlı olduğu başka bir senaryo Framework 'ün yeniden hedeflemesine yarar.</span><span class="sxs-lookup"><span data-stu-id="67f86-182">Another scenario where the reinstall flag proves beneficial is that of framework re-targeting.</span></span> <span data-ttu-id="67f86-183">Projenin hedef çerçevesini değiştirirken (örneğin, .NET 4 ' ten .NET 4,5 ' e kadar), Update-Package yeniden yükleme, projede yüklü olan tüm NuGet paketleri için doğru derlemelere başvuruları güncelleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="67f86-183">When changing the target framework of a project (for example, from .NET 4 to .NET 4.5), Update-Package -Reinstall can update references to the correct assemblies for all NuGet packages installed in the project.</span></span>

## <a name="edit-package-sources-within-visual-studio"></a><span data-ttu-id="67f86-184">Visual Studio 'Da paket kaynaklarını düzenleme</span><span class="sxs-lookup"><span data-stu-id="67f86-184">Edit Package Sources Within Visual Studio</span></span>

<span data-ttu-id="67f86-185">NuGet 'in önceki sürümlerinde, Visual Studio Seçenekler iletişim kutusunun içinden bir paket kaynağını güncelleştirme, paket kaynağını silme ve yeniden ekleme için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="67f86-185">In previous versions of NuGet, updating a package source from within the Visual Studio options dialog required deleting and re-adding the package source.</span></span>  <span data-ttu-id="67f86-186">NuGet 2,1, güncelleştirmeyi yapılandırma Kullanıcı arabiriminin ilk sınıf işlevi olarak destekleyerek bu iş akışını geliştirir.</span><span class="sxs-lookup"><span data-stu-id="67f86-186">NuGet 2.1 improves this workflow by supporting update as a first class function of the configuration user interface.</span></span>

![Paket Yöneticisi yapılandırma iletişim kutusu](./media/releasenotes-21-edit-pkg-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="67f86-188">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="67f86-188">Bug Fixes</span></span>

<span data-ttu-id="67f86-189">NuGet 2,1 birçok hata düzeltmesi içerir.</span><span class="sxs-lookup"><span data-stu-id="67f86-189">NuGet 2.1 includes many bug fixes.</span></span> <span data-ttu-id="67f86-190">NuGet 2,0 ' de düzeltilen iş öğelerinin tam listesi için lütfen [Bu sürüm Için NuGet sorun İzleyicisi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)' ni görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="67f86-190">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Fixed&type=All&priority=All&release=NuGet%202.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
