---
title: NuGet Akışlarını Barındırmak için NuGet.Server'ı kullanma
description: NuGet.Server kullanarak IIS çalıştıran herhangi bir sunucuda bir NuGet paket akışı oluşturma ve barındırma, paketleri HTTP ve OData üzerinden kullanılabilir hale getirme.
author: karann-msft
ms.author: karann
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: 098375b2bba13675ba5d80a27e0226dc2ee39e77
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79059586"
---
# <a name="nugetserver"></a><span data-ttu-id="61fa7-103">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="61fa7-103">NuGet.Server</span></span>

<span data-ttu-id="61fa7-104">NuGet.Server, .NET Foundation tarafından sağlanan ve IIS çalıştıran herhangi bir sunucuda paket akışı barındırabilen ASP.NET bir uygulama oluşturan bir pakettir.</span><span class="sxs-lookup"><span data-stu-id="61fa7-104">NuGet.Server is a package provided by the .NET Foundation that creates an ASP.NET application that can host a package feed on any server that runs IIS.</span></span> <span data-ttu-id="61fa7-105">Basitçe, NuGet.Server sunucuda http(S) (özellikle OData) aracılığıyla kullanılabilir bir klasör yapar söyledi.</span><span class="sxs-lookup"><span data-stu-id="61fa7-105">Simply said, NuGet.Server makes a folder on the server available through HTTP(S) (specifically OData).</span></span> <span data-ttu-id="61fa7-106">Kurulumu kolaydır ve basit senaryolar için en iyisidir.</span><span class="sxs-lookup"><span data-stu-id="61fa7-106">It's easy to set up and is best for simple scenarios.</span></span>

1. <span data-ttu-id="61fa7-107">Visual Studio'da boş bir ASP.NET Web uygulaması oluşturun ve NuGet.Server paketini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="61fa7-107">Create an empty ASP.NET Web application in Visual Studio and add the NuGet.Server package to it.</span></span>
1. <span data-ttu-id="61fa7-108">Uygulamadaki `Packages` klasörü yapılandırın ve paket ekleyin.</span><span class="sxs-lookup"><span data-stu-id="61fa7-108">Configure the `Packages` folder in the application and add packages.</span></span>
1. <span data-ttu-id="61fa7-109">Uygulamayı uygun bir sunucuya dağıtın.</span><span class="sxs-lookup"><span data-stu-id="61fa7-109">Deploy the application to a suitable server.</span></span>

<span data-ttu-id="61fa7-110">Aşağıdaki bölümler, C# kullanarak bu işlemi ayrıntılı olarak inceleyin.</span><span class="sxs-lookup"><span data-stu-id="61fa7-110">The following sections walk through this process in detail, using C#.</span></span>

<span data-ttu-id="61fa7-111">NuGet.Server hakkında başka sorularınız varsa, [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues)bir sorun oluşturun.</span><span class="sxs-lookup"><span data-stu-id="61fa7-111">If you have further questions about NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a><span data-ttu-id="61fa7-112">NuGet.Server ile ASP.NET bir Web uygulaması oluşturun ve dağıtın</span><span class="sxs-lookup"><span data-stu-id="61fa7-112">Create and deploy an ASP.NET Web application with NuGet.Server</span></span>

1. <span data-ttu-id="61fa7-113">Visual Studio'da, **"ASP.NET**Web Uygulaması (.NET Framework)" araması > Yeni > Projesi dosyasını seçin, C#için eşleşen şablonu seçin.</span><span class="sxs-lookup"><span data-stu-id="61fa7-113">In Visual Studio, select **File > New > Project**, search for "ASP.NET Web Application (.NET Framework)", select the matching template for C#.</span></span>

    ![.NET Framework web proje şablonu seçin](media/Hosting_00-NuGet.Server-ProjectType.png)

1. <span data-ttu-id="61fa7-115">**Çerçeveyi** ".NET Framework 4.6" olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="61fa7-115">Set **Framework** to ".NET Framework 4.6".</span></span>

    ![Yeni bir proje için hedef çerçevenin ayarlanması](media/Hosting_01-NuGet.Server-Set4.6.png)

1. <span data-ttu-id="61fa7-117">Uygulamaya NuGet.Server *dışında* uygun bir ad verin, Tamam'ı seçin ve bir sonraki iletişim kutusunda **Boş** şablonu seçin ve ardından **Tamam'ı**seçin.</span><span class="sxs-lookup"><span data-stu-id="61fa7-117">Give the application a suitable name *other* than NuGet.Server, select OK, and in the next dialog select the **Empty** template, then select **OK**.</span></span>

    ![Boş web projesini seçin](media/Hosting_02-NuGet.Server-Empty.png)

1. <span data-ttu-id="61fa7-119">Projeye sağ tıklayın, **NuGet Paketlerini Yönet'i**seçin.</span><span class="sxs-lookup"><span data-stu-id="61fa7-119">Right-click the project, select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="61fa7-120">Paket Yöneticisi Web Ekibi'nde **Gözat** sekmesini seçin ve .NET Framework 4.6'yı hedefliyorsanız NuGet.Server paketinin en son sürümünü arayın ve yükleyin.</span><span class="sxs-lookup"><span data-stu-id="61fa7-120">In the Package Manager UI, select the **Browse** tab, then search and install the latest version of the NuGet.Server package if you're targeting .NET Framework 4.6.</span></span> <span data-ttu-id="61fa7-121">(Ayrıca Paket Yöneticisi Konsolu ile `Install-Package NuGet.Server`yükleyebilirsiniz.) İstenirse lisans koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="61fa7-121">(You can also install it from the Package Manager Console with `Install-Package NuGet.Server`.) Accept the license terms if prompted.</span></span>

    ![NuGet.Server paketini yükleme](media/Hosting_03-NuGet.Server-Package.png)

1. <span data-ttu-id="61fa7-123">NuGet.Server'ın yüklenmesi, boş Web uygulamasını bir paket kaynağına dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="61fa7-123">Installing NuGet.Server converts the empty Web application into a package source.</span></span> <span data-ttu-id="61fa7-124">Çeşitli diğer paketleri yükler, uygulamada bir `Packages` klasör oluşturur ve ek `web.config` ayarlar içerecek şekilde değişir (ayrıntılar için bu dosyadaki yorumlara bakın).</span><span class="sxs-lookup"><span data-stu-id="61fa7-124">It installs a variety of other packages, creates a `Packages` folder in the application, and modifies `web.config` to include additional settings (see the comments in that file for details).</span></span>

    > [!Important]
    > <span data-ttu-id="61fa7-125">NuGet.Server paketi bu dosyadaki değişikliklerini tamamladıktan sonra dikkatlice inceleyin. `web.config`</span><span class="sxs-lookup"><span data-stu-id="61fa7-125">Carefully inspect `web.config` after the NuGet.Server package has completed its modifications to that file.</span></span> <span data-ttu-id="61fa7-126">NuGet.Server varolan öğelerin üzerine yazmıyor, bunun yerine yinelenen öğeler oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="61fa7-126">NuGet.Server may not overwrite existing elements but instead create duplicate elements.</span></span> <span data-ttu-id="61fa7-127">Bu yinelemeler, daha sonra projeyi çalıştırmayı denediğinizde bir "İç Sunucu Hatasına" neden olur.</span><span class="sxs-lookup"><span data-stu-id="61fa7-127">Those duplicates will cause an "Internal Server Error" when you later try to run the project.</span></span> <span data-ttu-id="61fa7-128">Örneğin, NuGet.Server'ı yüklemeden önce içerseniz, `web.config` `<compilation debug="true" targetFramework="4.5.2" />` paket üzerine yazmıyor, `<compilation debug="true" targetFramework="4.6" />`ikinci bir şey ekler.</span><span class="sxs-lookup"><span data-stu-id="61fa7-128">For example, if your `web.config` contains `<compilation debug="true" targetFramework="4.5.2" />` before installing NuGet.Server, the package doesn't overwrite it but inserts a second `<compilation debug="true" targetFramework="4.6" />`.</span></span> <span data-ttu-id="61fa7-129">Bu durumda, eski çerçeve sürümü ile öğeyi silin.</span><span class="sxs-lookup"><span data-stu-id="61fa7-129">In that case, delete the element with the older framework version.</span></span>

1. <span data-ttu-id="61fa7-130">Siteyi Visual Studio'da yerel olarak çalıştırın **(Hata Ayıklama > Hata Ayıklama veya** Ctrl+F5 olmadan Başlat'ı kullanarak).</span><span class="sxs-lookup"><span data-stu-id="61fa7-130">Run the site locally in Visual Studio (using **Debug > Start Without Debugging** or Ctrl+F5).</span></span> <span data-ttu-id="61fa7-131">Ana sayfa, aşağıda gösterildiği gibi paket besleme URL'lerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="61fa7-131">The home page provides the package feed URLs as shown below.</span></span> <span data-ttu-id="61fa7-132">Hatalar görürseniz, daha önce `web.config` belirtildiği gibi yinelenen öğeler için dikkatlice denetleyin.</span><span class="sxs-lookup"><span data-stu-id="61fa7-132">If you see errors, carefully inspect your `web.config` for duplicate elements as noted earlier.</span></span>

    ![NuGet.Server ile bir uygulama için varsayılan giriş sayfası](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1.  <span data-ttu-id="61fa7-134">Uygulamayı ilk çalıştırdığınızda, NuGet.Server klasörü `Packages` her paket için bir klasör içerecek şekilde yeniden yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="61fa7-134">The first time you run the application, NuGet.Server restructures the `Packages` folder to contain a folder for each package.</span></span> <span data-ttu-id="61fa7-135">Bu, performansı artırmak için NuGet 3.3 ile tanıtılan [yerel depolama düzeniyle](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) eşleşir.</span><span class="sxs-lookup"><span data-stu-id="61fa7-135">This matches the [local storage layout](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduced with NuGet 3.3 to improve performance.</span></span> <span data-ttu-id="61fa7-136">Daha fazla paket eklerken, bu yapıyı izlemeye devam edin.</span><span class="sxs-lookup"><span data-stu-id="61fa7-136">When adding more packages, continue to follow this structure.</span></span>

1. <span data-ttu-id="61fa7-137">Yerel dağıtımınızı test ettikten sonra, uygulamayı gerektiğinde başka bir dahili veya harici siteye dağıtın.</span><span class="sxs-lookup"><span data-stu-id="61fa7-137">Once you've tested your local deployment, deploy the application to any other internal or external site as needed.</span></span>

1. <span data-ttu-id="61fa7-138">Bir kez `http://<domain>`dağıtıldıktan sonra, paket kaynağı için `http://<domain>/nuget`kullandığınız URL olacaktır.</span><span class="sxs-lookup"><span data-stu-id="61fa7-138">Once deployed to `http://<domain>`, the URL that you use for the package source will be `http://<domain>/nuget`.</span></span>

## <a name="adding-packages-to-the-feed-externally"></a><span data-ttu-id="61fa7-139">Beslemeye harici paket ekleme</span><span class="sxs-lookup"><span data-stu-id="61fa7-139">Adding packages to the feed externally</span></span>

<span data-ttu-id="61fa7-140">NuGet.Server sitesi çalışmaya başladıktan sonra, ['de](../reference/cli-reference/cli-ref-push.md) `web.config`bir API anahtar değeri ayarlamanız koşuluyla nuget push kullanarak paketler ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="61fa7-140">Once a NuGet.Server site is running, you can add packages using [nuget push](../reference/cli-reference/cli-ref-push.md) provided that you set an API key value in `web.config`.</span></span>

<span data-ttu-id="61fa7-141">NuGet.Server paketini yükledikten sonra `appSetting/apiKey` boş bir değer `web.config` içerir:</span><span class="sxs-lookup"><span data-stu-id="61fa7-141">After installing the NuGet.Server package, `web.config` contains an empty `appSetting/apiKey` value:</span></span>

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="61fa7-142">Atlandığında veya boş olduğunda, `apiKey` paketleri özet akışına itme devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="61fa7-142">When `apiKey` is omitted or blank, pushing packages to the feed is disabled.</span></span>

<span data-ttu-id="61fa7-143">Bu özelliği etkinleştirmek `apiKey` için, bir değer (ideal olarak güçlü bir `appSettings/requireApiKey` parola) `true`ayarlayın ve değeri ile adlandırılan bir anahtar ekleyin:</span><span class="sxs-lookup"><span data-stu-id="61fa7-143">To enable this capability, set the `apiKey` to a value (ideally a strong password) and add a key called `appSettings/requireApiKey` with the value of `true`:</span></span>

```xml
<appSettings>
    <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="61fa7-144">Sunucunuz zaten güvenliyse veya başka bir şekilde bir API anahtarına ihtiyaç damıyorsanız `requireApiKey` (örneğin, yerel `false`bir ekip ağında özel bir sunucu kullanırken), .</span><span class="sxs-lookup"><span data-stu-id="61fa7-144">If your server is already secured or you do not otherwise require an API key (for example, when using a private server on a local team network), you can set `requireApiKey` to `false`.</span></span> <span data-ttu-id="61fa7-145">Sunucuya erişimi olan tüm kullanıcılar daha sonra paketleri itebilir.</span><span class="sxs-lookup"><span data-stu-id="61fa7-145">All users with access to the server can then push packages.</span></span>

<span data-ttu-id="61fa7-146">NuGet.Server 3.0.0 ile başlayarak, paketleri itme için URL 'ye `http://<domain>/nuget`göre değiştirildi.</span><span class="sxs-lookup"><span data-stu-id="61fa7-146">Starting with NuGet.Server 3.0.0, the URL for pushing packages was change to `http://<domain>/nuget`.</span></span> <span data-ttu-id="61fa7-147">3.0.0 sürümünden önce, itme `http://<domain>/api/v2/package`URL'si .</span><span class="sxs-lookup"><span data-stu-id="61fa7-147">Prior to the 3.0.0 release, the push URL was `http://<domain>/api/v2/package`.</span></span>

<span data-ttu-id="61fa7-148">NuGet 3.2.1 ve daha yeni `/api/v2/package` ile bu eski `/nuget` URL, `enableLegacyPushRoute: true` başlangıç config'inizdeki seçenek üzerinden varsayılan olarak (varsayılan`NuGetODataConfig.cs` olarak) ek olarak etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="61fa7-148">With NuGet 3.2.1 and newer, this legacy URL `/api/v2/package` is enabled in addition to `/nuget` by default via `enableLegacyPushRoute: true` option in your startup config (`NuGetODataConfig.cs` by default).</span></span> <span data-ttu-id="61fa7-149">Aynı projede birden çok özet akışı barındırıldığında bu özelliğin çalışmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="61fa7-149">Note that this feature does not work when multiple feeds are hosted in the same project.</span></span>

## <a name="removing-packages-from-the-feed"></a><span data-ttu-id="61fa7-150">Paketleri akıştan kaldırma</span><span class="sxs-lookup"><span data-stu-id="61fa7-150">Removing packages from the feed</span></span>

<span data-ttu-id="61fa7-151">NuGet.Server ile [nuget silme](../reference/cli-reference/cli-ref-delete.md) komutu, yoruma API anahtarı eklemeniz koşuluyla bir paketi depodan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="61fa7-151">With NuGet.Server, the [nuget delete](../reference/cli-reference/cli-ref-delete.md) command removes a package from the repository provided that you include the API key with the comment.</span></span>

<span data-ttu-id="61fa7-152">Bunun yerine paketin listesini çıkarmak için davranışı değiştirmek istiyorsanız (paket geri `enableDelisting` yükleme `web.config` için kullanılabilir bırakarak), anahtarı true olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="61fa7-152">If you want to change the behavior to delist the package instead (leaving it available for package restore), change the `enableDelisting` key in `web.config` to true.</span></span>

## <a name="configuring-the-packages-folder"></a><span data-ttu-id="61fa7-153">Paketler klasörünü yapılandırma</span><span class="sxs-lookup"><span data-stu-id="61fa7-153">Configuring the Packages folder</span></span>

<span data-ttu-id="61fa7-154">1.5 ve sonrası ile, `NuGet.Server` `appSettings/packagesPath` aşağıdaki değeri kullanarak paket `web.config`klasörünü özelleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="61fa7-154">With `NuGet.Server` 1.5 and later, you can customize the package folder using the `appSettings/packagesPath` value in `web.config`:</span></span>

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

<span data-ttu-id="61fa7-155">`packagesPath`mutlak veya sanal bir yol olabilir.</span><span class="sxs-lookup"><span data-stu-id="61fa7-155">`packagesPath` can be an absolute or virtual path.</span></span>

<span data-ttu-id="61fa7-156">Atlandığında veya boş bırakıldığında, `packagesPath` paketler klasörü `~/Packages`varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="61fa7-156">When `packagesPath` is omitted or left blank, the packages folder is the default `~/Packages`.</span></span>

## <a name="making-packages-available-when-you-publish-the-web-app"></a><span data-ttu-id="61fa7-157">Web uygulamasını yayımladığınızda paketleri kullanılabilir hale getirme</span><span class="sxs-lookup"><span data-stu-id="61fa7-157">Making packages available when you publish the web app</span></span>

<span data-ttu-id="61fa7-158">Uygulamayı bir sunucuda yayımladığınızda özet akışında paketleri kullanılabilir `.nupkg` hale `Packages` getirmek için, her dosyayı Visual Studio'daki klasöre ekleyin ve ardından her birinin **Yapı Eylemini** **İçerik'e** ayarlayın ve Her **zaman Kopyalamak** **için Çıktı Dizini'ne Kopyala:**</span><span class="sxs-lookup"><span data-stu-id="61fa7-158">To make packages available in the feed when you publish the application to a server, add each `.nupkg` files to the `Packages` folder in Visual Studio, then set each one's **Build Action** to **Content** and **Copy to Output Directory** to **Copy always**:</span></span>

![Projedeki Paketler klasörüne paketleri kopyalama](media/Hosting_05-NuGet.Server-Package-Folder.png)

## <a name="release-notes"></a><span data-ttu-id="61fa7-160">Sürüm Notları</span><span class="sxs-lookup"><span data-stu-id="61fa7-160">Release Notes</span></span>

<span data-ttu-id="61fa7-161">NuGet.Server için sürüm notları [GitHub sürüm sayfasında](https://github.com/NuGet/NuGet.Server/releases)mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="61fa7-161">Release notes for NuGet.Server are available on the [GitHub release page](https://github.com/NuGet/NuGet.Server/releases).</span></span>
<span data-ttu-id="61fa7-162">Bu hata düzeltmeleri ve eklenen yeni özellikler hakkında ayrıntıları içerir.</span><span class="sxs-lookup"><span data-stu-id="61fa7-162">This includes details about bug fixes and new features that are added.</span></span>

## <a name="nugetserver-support"></a><span data-ttu-id="61fa7-163">NuGet.Server desteği</span><span class="sxs-lookup"><span data-stu-id="61fa7-163">NuGet.Server support</span></span>

<span data-ttu-id="61fa7-164">NuGet.Server'ı kullanarak ek yardım [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues)için bir sorun oluşturun.</span><span class="sxs-lookup"><span data-stu-id="61fa7-164">For additional help using NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>
