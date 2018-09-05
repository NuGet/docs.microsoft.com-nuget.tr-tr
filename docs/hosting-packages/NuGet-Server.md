---
title: NuGet barındırmak için NuGet.Server kullanarak akışları
description: NuGet.Server kullanarak, HTTP ve OData aracılığıyla paketleri kullanımına IIS çalıştıran herhangi bir sunucuda nasıl oluşturulacağı ve bir NuGet paketi ana akış.
author: karann-msft
ms.author: karann
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: e99d42744ec860976ae098be94e747ec4bc9a7c6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551962"
---
# <a name="nugetserver"></a><span data-ttu-id="cd235-103">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="cd235-103">NuGet.Server</span></span>

<span data-ttu-id="cd235-104">NuGet.Server, IIS çalıştıran herhangi bir sunucu üzerinde akış bir paket barındırabilecek bir ASP.NET uygulaması oluşturan bir .NET Foundation tarafından sağlanan bir pakettir.</span><span class="sxs-lookup"><span data-stu-id="cd235-104">NuGet.Server is a package provided by the .NET Foundation that creates an ASP.NET application that can host a package feed on any server that runs IIS.</span></span> <span data-ttu-id="cd235-105">Kısaca, NuGet.Server sunucu üzerindeki bir klasöre üzerinden HTTP (S) (özellikle, OData) kullanılabilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="cd235-105">Simply said, NuGet.Server makes a folder on the server available through HTTP(S) (specifically OData).</span></span> <span data-ttu-id="cd235-106">Bunu ayarlamak kolaydır ve basit senaryolar için idealdir.</span><span class="sxs-lookup"><span data-stu-id="cd235-106">It's easy to set up and is best for simple scenarios.</span></span>

1. <span data-ttu-id="cd235-107">Visual Studio'da boş bir ASP.NET Web uygulaması oluşturma ve NuGet.Server paketi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="cd235-107">Create an empty ASP.NET Web application in Visual Studio and add the NuGet.Server package to it.</span></span>
1. <span data-ttu-id="cd235-108">Yapılandırma `Packages` uygulama klasöründe ve paketleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="cd235-108">Configure the `Packages` folder in the application and add packages.</span></span>
1. <span data-ttu-id="cd235-109">Uygun bir sunucu uygulaması dağıtın.</span><span class="sxs-lookup"><span data-stu-id="cd235-109">Deploy the application to a suitable server.</span></span>

<span data-ttu-id="cd235-110">Aşağıdaki bölümlerde ayrıntılı olarak C# kullanarak bu işlemi yol.</span><span class="sxs-lookup"><span data-stu-id="cd235-110">The following sections walk through this process in detail, using C#.</span></span>

<span data-ttu-id="cd235-111">Başka NuGet.Server hakkında sorularınız varsa, bir sorun oluşturmak [ https://github.com/nuget/NuGetGallery/issues ](https://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="cd235-111">If you have further questions about NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a><span data-ttu-id="cd235-112">NuGet.Server ile bir ASP.NET Web uygulaması oluşturma ve dağıtma</span><span class="sxs-lookup"><span data-stu-id="cd235-112">Create and deploy an ASP.NET Web application with NuGet.Server</span></span>

1. <span data-ttu-id="cd235-113">Visual Studio'da **Dosya > Yeni > Proje**, "ASP.NET için" arayın, seçin **ASP.NET Web uygulaması (.NET Framework)** C# ve küme için şablon **Framework** ".NET Framework 4.6":</span><span class="sxs-lookup"><span data-stu-id="cd235-113">In Visual Studio, select **File > New > Project**, search for "ASP.NET", select the **ASP.NET Web Application (.NET Framework)** template for C#, and set **Framework** to ".NET Framework 4.6":</span></span>

    ![Yeni bir proje için hedef Framework'ü ayarlama](media/Hosting_01-NuGet.Server-Set4.6.png)

1. <span data-ttu-id="cd235-115">Uygulama uygun bir ad verin *diğer* NuGet.Server Tamam ve sonraki iletişim kutusunda seçin **boş** şablonu seçip **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="cd235-115">Give the application a suitable name *other* than NuGet.Server, select OK, and in the next dialog select the **Empty** template, then select **OK**.</span></span>

1. <span data-ttu-id="cd235-116">Projeye sağ tıklayın, **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="cd235-116">Right-click the project, select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="cd235-117">Paket Yöneticisi UI'nızda seçin **Gözat** sekmesini, sonra arayın ve .NET Framework 4.6 hedefliyorsanız NuGet.Server paketin en son sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="cd235-117">In the Package Manager UI, select the **Browse** tab, then search and install the latest version of the NuGet.Server package if you're targeting .NET Framework 4.6.</span></span> <span data-ttu-id="cd235-118">(Paket Yöneticisi konsolu ile de yükleyebilirsiniz `Install-Package NuGet.Server`.) İstenirse, lisans koşullarını kabul.</span><span class="sxs-lookup"><span data-stu-id="cd235-118">(You can also install it from the Package Manager Console with `Install-Package NuGet.Server`.) Accept the license terms if prompted.</span></span>

    ![NuGet.Server paketi yükleniyor](media/Hosting_02-NuGet.Server-Package.png)

1. <span data-ttu-id="cd235-120">NuGet.Server yükleme boş bir Web uygulaması, paket kaynağına dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="cd235-120">Installing NuGet.Server converts the empty Web application into a package source.</span></span> <span data-ttu-id="cd235-121">Diğer paketleri çeşitli yükler, oluşturur bir `Packages` uygulama klasöründe ve değiştirir `web.config` (bkz. Ayrıntılar için bu dosyayı açıklamalarda) ek ayarlar eklenecek.</span><span class="sxs-lookup"><span data-stu-id="cd235-121">It installs a variety of other packages, creates a `Packages` folder in the application, and modifies `web.config` to include additional settings (see the comments in that file for details).</span></span>

    > [!Important]
    > <span data-ttu-id="cd235-122">Dikkatli bir şekilde incelemek `web.config` NuGet.Server paketi bu dosya, değişiklik tamamlandıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="cd235-122">Carefully inspect `web.config` after the NuGet.Server package has completed its modifications to that file.</span></span> <span data-ttu-id="cd235-123">NuGet.Server var olan öğelerin üzerine değil ancak bunun yerine yinelenen öğeler oluşturmak.</span><span class="sxs-lookup"><span data-stu-id="cd235-123">NuGet.Server may not overwrite existing elements but instead create duplicate elements.</span></span> <span data-ttu-id="cd235-124">Daha sonra projeyi çalıştırmak çalıştığınızda bu yinelemeler bir "İç sunucu hatası" neden olur.</span><span class="sxs-lookup"><span data-stu-id="cd235-124">Those duplicates will cause an "Internal Server Error" when you later try to run the project.</span></span> <span data-ttu-id="cd235-125">Örneğin, varsa, `web.config` içeren `<compilation debug="true" targetFramework="4.5.2" />` NuGet.Server'ı yüklemeden önce paket üzerine değil ancak bir saniye ekler `<compilation debug="true" targetFramework="4.6" />`.</span><span class="sxs-lookup"><span data-stu-id="cd235-125">For example, if your `web.config` contains `<compilation debug="true" targetFramework="4.5.2" />` before installing NuGet.Server, the package doesn't overwrite it but inserts a second `<compilation debug="true" targetFramework="4.6" />`.</span></span> <span data-ttu-id="cd235-126">Bu durumda, daha eski framework sürümü öğeyi silin.</span><span class="sxs-lookup"><span data-stu-id="cd235-126">In that case, delete the element with the older framework version.</span></span>

1. <span data-ttu-id="cd235-127">Bir sunucu için uygulamayı yayımladığınızda paketleri akışta kullanabilmek için her ekleyin `.nupkg` dosyaları `Packages` klasör Visual Studio'da ayarlayın her birinin **derleme eylemi** için **İçerik**ve **çıkış dizinine Kopyala** için **her zaman Kopyala**:</span><span class="sxs-lookup"><span data-stu-id="cd235-127">To make packages available in the feed when you publish the application to a server, add each `.nupkg` files to the `Packages` folder in Visual Studio, then set each one's **Build Action** to **Content** and **Copy to Output Directory** to **Copy always**:</span></span>

    ![Projedeki paketler klasörüne kopyalama paketleri](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. <span data-ttu-id="cd235-129">Site Visual Studio'da yerel olarak çalıştırma (kullanarak **hata ayıklama > hata ayıklama olmadan Başlat** ya da Ctrl + F5).</span><span class="sxs-lookup"><span data-stu-id="cd235-129">Run the site locally in Visual Studio (using **Debug > Start Without Debugging** or Ctrl+F5).</span></span> <span data-ttu-id="cd235-130">Giriş sayfasında, aşağıda gösterildiği gibi paket URL'leri akışı sağlar.</span><span class="sxs-lookup"><span data-stu-id="cd235-130">The home page provides the package feed URLs as shown below.</span></span> <span data-ttu-id="cd235-131">Hatalar görürseniz, dikkatlice inceleyin, `web.config` için yinelenen öğeler daha önce 5. adım ile belirtilmiştir.</span><span class="sxs-lookup"><span data-stu-id="cd235-131">If you see errors, carefully inspect your `web.config` for duplicate elements are noted earlier with step 5.</span></span>

    ![NuGet.Server ile bir uygulama için varsayılan giriş sayfası](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. <span data-ttu-id="cd235-133">Tıklayarak **burada** paketlerin OData akışı görmek için yukarıda özetlenen alanında.</span><span class="sxs-lookup"><span data-stu-id="cd235-133">Click on **here** in the area outlined above to see the OData feed of packages.</span></span>

1. <span data-ttu-id="cd235-134">İlk kez uygulamayı çalıştırdığınızda, NuGet.Server yeniden yapılandırır `Packages` her paket için bir klasör içeren klasör.</span><span class="sxs-lookup"><span data-stu-id="cd235-134">The first time you run the application, NuGet.Server restructures the `Packages` folder to contain a folder for each package.</span></span> <span data-ttu-id="cd235-135">Bu eşleşen [yerel depolama düzeni](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) performansını artırmak için NuGet 3.3 ile sunulan.</span><span class="sxs-lookup"><span data-stu-id="cd235-135">This matches the [local storage layout](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduced with NuGet 3.3 to improve performance.</span></span> <span data-ttu-id="cd235-136">Daha fazla paket eklerken, bu yapı izlemeye devam edin.</span><span class="sxs-lookup"><span data-stu-id="cd235-136">When adding more packages, continue to follow this structure.</span></span>

1. <span data-ttu-id="cd235-137">Yerel dağıtımınızı test ettikten sonra gerektiğinde diğer iç veya dış konuma uygulamayı dağıtın.</span><span class="sxs-lookup"><span data-stu-id="cd235-137">Once you've tested your local deployment, deploy the application to any other internal or external site as needed.</span></span>

1. <span data-ttu-id="cd235-138">Dağıtıldıktan sonra `http://<domain>`, kullandığınız için paket kaynağı URL'si olacaktır `http://<domain>/nuget`.</span><span class="sxs-lookup"><span data-stu-id="cd235-138">Once deployed to `http://<domain>`, the URL that you use for the package source will be `http://<domain>/nuget`.</span></span>

## <a name="configuring-the-packages-folder"></a><span data-ttu-id="cd235-139">Paketleri klasörünü yapılandırma</span><span class="sxs-lookup"><span data-stu-id="cd235-139">Configuring the Packages folder</span></span>

<span data-ttu-id="cd235-140">İle `NuGet.Server` 1.5 ve sonrası, daha açık belirtmek gerekirse klasör paketini kullanarak yapılandırabileceğiniz `appSetting/packagesPath` değerini `web.config`:</span><span class="sxs-lookup"><span data-stu-id="cd235-140">With `NuGet.Server` 1.5 and later, you can more specifically configure the package folder using the `appSetting/packagesPath` value in `web.config`:</span></span>

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

<span data-ttu-id="cd235-141">`packagesPath` mutlak ya da sanal bir yol olabilir.</span><span class="sxs-lookup"><span data-stu-id="cd235-141">`packagesPath` can be an absolute or virtual path.</span></span>

<span data-ttu-id="cd235-142">Zaman `packagesPath` atlanırsa veya boş bırakılmış packages klasörünü varsayılandır `~/Packages`.</span><span class="sxs-lookup"><span data-stu-id="cd235-142">When `packagesPath` is omitted or left blank, the packages folder is the default `~/Packages`.</span></span>

## <a name="adding-packages-to-the-feed-externally"></a><span data-ttu-id="cd235-143">Harici olarak akışa paketleri ekleme</span><span class="sxs-lookup"><span data-stu-id="cd235-143">Adding packages to the feed externally</span></span>

<span data-ttu-id="cd235-144">NuGet.Server site çalışır duruma geçtikten sonra kullanarak paketleri ekleyebilirsiniz [nuget anında iletme](../tools/cli-ref-push.md) API anahtar değeri ayarlamak koşuluyla `web.config`.</span><span class="sxs-lookup"><span data-stu-id="cd235-144">Once a NuGet.Server site is running, you can add packages using [nuget push](../tools/cli-ref-push.md) provided that you set an API key value in `web.config`.</span></span>

<span data-ttu-id="cd235-145">NuGet.Server paketini yükledikten sonra `web.config` boş içeren `appSetting/apiKey` değeri:</span><span class="sxs-lookup"><span data-stu-id="cd235-145">After installing the NuGet.Server package, `web.config` contains an empty `appSetting/apiKey` value:</span></span>

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="cd235-146">Zaman `apiKey` atlanırsa veya boş, akışa paketleri gönderme devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="cd235-146">When `apiKey` is omitted or blank, pushing packages to the feed is disabled.</span></span>

<span data-ttu-id="cd235-147">Bu özelliği etkinleştirmek için `apiKey` bir değere (İdeal olarak güçlü bir parola) adlı bir anahtar ekleyin `appSettings/requireApiKey` değeriyle `true`:</span><span class="sxs-lookup"><span data-stu-id="cd235-147">To enable this capability, set the `apiKey` to a value (ideally a strong password) and add a key called `appSettings/requireApiKey` with the value of `true`:</span></span>

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="cd235-148">Sunucunuz zaten güvenli veya aksi halde bir API anahtarı (örneğin, bir yerel takım ağında özel bir sunucu kullanarak) gerektirmez, ayarlayabileceğiniz `requireApiKey` için `false`.</span><span class="sxs-lookup"><span data-stu-id="cd235-148">If your server is already secured or you do not otherwise require an API key (for example, when using a private server on a local team network), you can set `requireApiKey` to `false`.</span></span> <span data-ttu-id="cd235-149">Sunucusuna erişimi olan tüm kullanıcılar, ardından paketleri gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cd235-149">All users with access to the server can then push packages.</span></span>

## <a name="removing-packages-from-the-feed"></a><span data-ttu-id="cd235-150">Akıştan paket kaldırılıyor</span><span class="sxs-lookup"><span data-stu-id="cd235-150">Removing packages from the feed</span></span>

<span data-ttu-id="cd235-151">NuGet.Server ile [nuget Sil](../tools/cli-ref-delete.md) komut açıklamayı API anahtarını dahil koşuluyla bu bir paket depodan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="cd235-151">With NuGet.Server, the [nuget delete](../tools/cli-ref-delete.md) command removes a package from the repository provided that you include the API key with the comment.</span></span>

<span data-ttu-id="cd235-152">Bunun yerine paket delist davranışını değiştirmek istiyorsanız (paket geri yükleme için kullanılabilir bırakarak), değiştirme `enableDelisting` anahtarını `web.config` true.</span><span class="sxs-lookup"><span data-stu-id="cd235-152">If you want to change the behavior to delist the package instead (leaving it available for package restore), change the `enableDelisting` key in `web.config` to true.</span></span>

## <a name="nugetserver-support"></a><span data-ttu-id="cd235-153">NuGet.Server desteği</span><span class="sxs-lookup"><span data-stu-id="cd235-153">NuGet.Server support</span></span>

<span data-ttu-id="cd235-154">Ek Yardım için NuGet.Server, kullanarak oluşturduğunuz bir sorun üzerinde [ https://github.com/nuget/NuGetGallery/issues ](https://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="cd235-154">For additional help using NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>