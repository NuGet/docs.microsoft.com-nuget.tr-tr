---
title: "NuGet barındırmak için NuGet.Server kullanarak akışları | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/13/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet.Server kullanarak, paketleri HTTP ve OData yoluyla kullanılabilir hale getirme IIS çalıştıran herhangi bir sunucuda nasıl oluşturulacağı ve bir NuGet paketi konak akış."
keywords: "Akış, NuGet NuGet galerisinde, akış, Uzak paket NuGet.Server"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d85c1ca88ca44c8f8bfa5cb9c453279f65f26f50
ms.sourcegitcommit: 9adf5349eab91bd1d044e11f34836d53cfb115b3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/16/2018
---
# <a name="nugetserver"></a><span data-ttu-id="20f08-104">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="20f08-104">NuGet.Server</span></span>

<span data-ttu-id="20f08-105">NuGet.Server, IIS çalıştıran herhangi bir sunucu üzerinde akış paket barındırabilen bir ASP.NET uygulaması oluşturur .NET Foundation tarafından sağlanan bir pakettir.</span><span class="sxs-lookup"><span data-stu-id="20f08-105">NuGet.Server is a package provided by the .NET Foundation that creates an ASP.NET application that can host a package feed on any server that runs IIS.</span></span> <span data-ttu-id="20f08-106">Kısaca, NuGet.Server sunucusundaki bir klasöre aracılığıyla HTTP (S) (özellikle OData) kullanılabilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="20f08-106">Simply said, NuGet.Server makes a folder on the server available through HTTP(S) (specifically OData).</span></span> <span data-ttu-id="20f08-107">Ayarlamak kolaydır ve basit senaryoları için en iyisidir.</span><span class="sxs-lookup"><span data-stu-id="20f08-107">It's easy to set up and is best for simple scenarios.</span></span>

1. <span data-ttu-id="20f08-108">Visual Studio'da boş bir ASP.NET Web uygulaması oluşturun ve NuGet.Server paketi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="20f08-108">Create an empty ASP.NET Web application in Visual Studio and add the NuGet.Server package to it.</span></span>
1. <span data-ttu-id="20f08-109">Yapılandırma `Packages` uygulama klasöründe ve paketleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="20f08-109">Configure the `Packages` folder in the application and add packages.</span></span>
1. <span data-ttu-id="20f08-110">Uygun bir sunucu uygulamayı dağıtın.</span><span class="sxs-lookup"><span data-stu-id="20f08-110">Deploy the application to a suitable server.</span></span>

<span data-ttu-id="20f08-111">Aşağıdaki bölümlerde bu işlem C# kullanarak ayrıntılı yol.</span><span class="sxs-lookup"><span data-stu-id="20f08-111">The following sections walk through this process in detail, using C#.</span></span>

<span data-ttu-id="20f08-112">Daha fazla NuGet.Server hakkında sorularınız varsa, bir sorun oluşturmak [ https://github.com/nuget/NuGetGallery/issues ](https://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="20f08-112">If you have further questions about NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a><span data-ttu-id="20f08-113">Bir ASP.NET Web uygulama NuGet.Server ile oluşturun ve dağıtın</span><span class="sxs-lookup"><span data-stu-id="20f08-113">Create and deploy an ASP.NET Web application with NuGet.Server</span></span>

1. <span data-ttu-id="20f08-114">Visual Studio'da seçin **Dosya > Yeni > Proje**, arama "ASP.NET için", seçin **ASP.NET Web uygulaması (.NET Framework)** C# ve kümesi için şablon **Framework** ".NET Framework 4.6":</span><span class="sxs-lookup"><span data-stu-id="20f08-114">In Visual Studio, select **File > New > Project**, search for "ASP.NET", select the **ASP.NET Web Application (.NET Framework)** template for C#, and set **Framework** to ".NET Framework 4.6":</span></span>

    ![Yeni bir proje hedef çerçevesi ayarlama](media/Hosting_01-NuGet.Server-Set4.6.png)

1. <span data-ttu-id="20f08-116">Uygulama uygun bir ad verin *diğer* NuGet.Server Tamam ve sonraki iletişim kutusunda seçin **boş** şablonu, ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="20f08-116">Give the application a suitable name *other* than NuGet.Server, select OK, and in the next dialog select the **Empty** template, then select **OK**.</span></span>

1. <span data-ttu-id="20f08-117">Projeye sağ tıklayın, **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="20f08-117">Right-click the project, select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="20f08-118">Paket Yöneticisi Arabiriminde seçin **Gözat** sekmesinde, sonra arayın ve .NET Framework 4.6 hedefleme NuGet.Server paketinin en son sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="20f08-118">In the Package Manager UI, select the **Browse** tab, then search and install the latest version of the NuGet.Server package if you're targeting .NET Framework 4.6.</span></span> <span data-ttu-id="20f08-119">(İle Paket Yöneticisi Konsolu'ndan de yükleyebilirsiniz `Install-Package NuGet.Server`.) Lisans koşullarını kabul etmeniz istenirse.</span><span class="sxs-lookup"><span data-stu-id="20f08-119">(You can also install it from the Package Manager Console with `Install-Package NuGet.Server`.) Accept the license terms if prompted.</span></span>

    ![NuGet.Server paketi yükleniyor](media/Hosting_02-NuGet.Server-Package.png)

1. <span data-ttu-id="20f08-121">NuGet.Server yükleme boş bir Web uygulaması bir paket kaynağına dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="20f08-121">Installing NuGet.Server converts the empty Web application into a package source.</span></span> <span data-ttu-id="20f08-122">Çeşitli diğer paketler yükler, oluşturur bir `Packages` uygulama klasöründe ve değiştirir `web.config` (bkz. Ayrıntılar için bu dosyayı açıklamalarda) ek ayarlar dahil etmek için.</span><span class="sxs-lookup"><span data-stu-id="20f08-122">It installs a variety of other packages, creates a `Packages` folder in the application, and modifies `web.config` to include additional settings (see the comments in that file for details).</span></span>

    > [!Important]
    > <span data-ttu-id="20f08-123">Dikkatlice inceleyin `web.config` NuGet.Server paket bu dosyaya kendi değişiklikler tamamlandıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="20f08-123">Carefully inspect `web.config` after the NuGet.Server package has completed its modifications to that file.</span></span> <span data-ttu-id="20f08-124">NuGet.Server bellek kaynakları olan öğeleri üzerine değildir ancak bunun yerine yinelenen öğeler oluşturur.</span><span class="sxs-lookup"><span data-stu-id="20f08-124">NuGet.Server may not overwrite existing elements but instead create duplicate elements.</span></span> <span data-ttu-id="20f08-125">Daha sonra projeyi çalıştırmayı denediğinizde bu yinelenen bir "Dahili Sunucu hatası" neden olur.</span><span class="sxs-lookup"><span data-stu-id="20f08-125">Those duplicates will cause an "Internal Server Error" when you later try to run the project.</span></span> <span data-ttu-id="20f08-126">Örneğin, varsa, `web.config` içeren `<compilation debug="true" targetFramework="4.5.2" />` NuGet.Server'ı yüklemeden önce paketin üzerine değildir ancak ikinci ekler `<compilation debug="true" targetFramework="4.6" />`.</span><span class="sxs-lookup"><span data-stu-id="20f08-126">For example, if your `web.config` contains `<compilation debug="true" targetFramework="4.5.2" />` before installing NuGet.Server, the package doesn't overwrite it but inserts a second `<compilation debug="true" targetFramework="4.6" />`.</span></span> <span data-ttu-id="20f08-127">Bu durumda, eski framework sürüm öğesini silin.</span><span class="sxs-lookup"><span data-stu-id="20f08-127">In that case, delete the element with the older framework version.</span></span>

1. <span data-ttu-id="20f08-128">Bir sunucuya uygulama yayımladığınızda, paketleri akıştaki kullanılabilir kılmak için her eklemeniz `.nupkg` dosyaları `Packages` klasörü Visual Studio'da sonra ayarlanmış her birinin **yapı eylemi** için **İçerik**ve **çıktı dizinine Kopyala** için **her zaman Kopyala**:</span><span class="sxs-lookup"><span data-stu-id="20f08-128">To make packages available in the feed when you publish the application to a server, add each `.nupkg` files to the `Packages` folder in Visual Studio, then set each one's **Build Action** to **Content** and **Copy to Output Directory** to **Copy always**:</span></span>

    ![Paketleri projesinde paketleri klasöre kopyalama](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. <span data-ttu-id="20f08-130">Siteyi Visual Studio'da yerel olarak çalıştırın (kullanarak **hata ayıklama > hata ayıklama olmadan Başlat** veya Ctrl + F5).</span><span class="sxs-lookup"><span data-stu-id="20f08-130">Run the site locally in Visual Studio (using **Debug > Start Without Debugging** or Ctrl+F5).</span></span> <span data-ttu-id="20f08-131">Giriş sayfası, aşağıda gösterildiği gibi URL'leri paket akışı sağlar.</span><span class="sxs-lookup"><span data-stu-id="20f08-131">The home page provides the package feed URLs as shown below.</span></span> <span data-ttu-id="20f08-132">Hatalar görürseniz, dikkatlice inceleyin, `web.config` için yinelenen öğeler önceki adım 5 ile belirtilmiştir.</span><span class="sxs-lookup"><span data-stu-id="20f08-132">If you see errors, carefully inspect your `web.config` for duplicate elements are noted earlier with step 5.</span></span>

    ![NuGet.Server olan bir uygulama için varsayılan giriş sayfası](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. <span data-ttu-id="20f08-134">Tıklayın **burada** paketlerin OData akışı görmek için yukarıda özetlenen alanında.</span><span class="sxs-lookup"><span data-stu-id="20f08-134">Click on **here** in the area outlined above to see the OData feed of packages.</span></span>

1. <span data-ttu-id="20f08-135">İlk kez uygulamayı çalıştırın, NuGet.Server yeniden yapılandırır `Packages` her paket için bir klasör içeren klasör.</span><span class="sxs-lookup"><span data-stu-id="20f08-135">The first time you run the application, NuGet.Server restructures the `Packages` folder to contain a folder for each package.</span></span> <span data-ttu-id="20f08-136">Bu eşleşen [yerel depolama düzeni](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) performansını artırmak için NuGet 3.3 ile sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="20f08-136">This matches the [local storage layout](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduced with NuGet 3.3 to improve performance.</span></span> <span data-ttu-id="20f08-137">Daha fazla paket eklerken, bu yapıyı izlemeye devam edin.</span><span class="sxs-lookup"><span data-stu-id="20f08-137">When adding more packages, continue to follow this structure.</span></span>

1. <span data-ttu-id="20f08-138">Yerel dağıtımınızı test ettikten sonra diğer iç veya dış site uygulamaya gerektiği gibi dağıtın.</span><span class="sxs-lookup"><span data-stu-id="20f08-138">Once you've tested your local deployment, deploy the application to any other internal or external site as needed.</span></span>

1. <span data-ttu-id="20f08-139">Dağıtıldıktan sonra `http://<domain>`, paket kaynağı için kullandığınız URL'yi olacaktır `http://<domain>/nuget`.</span><span class="sxs-lookup"><span data-stu-id="20f08-139">Once deployed to `http://<domain>`, the URL that you use for the package source will be `http://<domain>/nuget`.</span></span>

## <a name="configuring-the-packages-folder"></a><span data-ttu-id="20f08-140">Paketler klasörü yapılandırma</span><span class="sxs-lookup"><span data-stu-id="20f08-140">Configuring the Packages folder</span></span>

<span data-ttu-id="20f08-141">İle `NuGet.Server` 1,5 ve daha sonra daha açık belirtmek gerekirse paket klasörünü kullanarak yapılandırabileceğiniz `appSetting/packagesPath` değeri `web.config`:</span><span class="sxs-lookup"><span data-stu-id="20f08-141">With `NuGet.Server` 1.5 and later, you can more specifically configure the package folder using the `appSetting/packagesPath` value in `web.config`:</span></span>

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

<span data-ttu-id="20f08-142">`packagesPath` mutlak ya da sanal bir yol olabilir.</span><span class="sxs-lookup"><span data-stu-id="20f08-142">`packagesPath` can be an absolute or virtual path.</span></span>

<span data-ttu-id="20f08-143">Zaman `packagesPath` atlanmış veya boş, sol varsayılan paketleri klasörüdür `~/Packages`.</span><span class="sxs-lookup"><span data-stu-id="20f08-143">When `packagesPath` is omitted or left blank, the packages folder is the default `~/Packages`.</span></span>

## <a name="adding-packages-to-the-feed-externally"></a><span data-ttu-id="20f08-144">Akışa dışarıdan paketleri ekleme</span><span class="sxs-lookup"><span data-stu-id="20f08-144">Adding packages to the feed externally</span></span>

<span data-ttu-id="20f08-145">NuGet.Server site çalışmaya başladıktan sonra kullanarak paketleri ekleyebilirsiniz [nuget itme](../tools/cli-ref-push.md) API anahtar değeri ayarlanmış koşuluyla, `web.config`.</span><span class="sxs-lookup"><span data-stu-id="20f08-145">Once a NuGet.Server site is running, you can add packages using [nuget push](../tools/cli-ref-push.md) provided that you set an API key value in `web.config`.</span></span>

<span data-ttu-id="20f08-146">NuGet.Server paketini yükledikten sonra `web.config` boş bir içeren `appSetting/apiKey` değeri:</span><span class="sxs-lookup"><span data-stu-id="20f08-146">After installing the NuGet.Server package, `web.config` contains an empty `appSetting/apiKey` value:</span></span>

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="20f08-147">Zaman `apiKey` atlanmış veya boş, paketleri akışa Ftp'den devre dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="20f08-147">When `apiKey` is omitted or blank, pushing packages to the feed is disabled.</span></span>

<span data-ttu-id="20f08-148">Bu özelliği etkinleştirmek için ayarlanmış `apiKey` bir değere (İdeal olarak güçlü bir parola) adlı bir anahtar ekleyin `appSettings/requireApiKey` değeriyle `true`:</span><span class="sxs-lookup"><span data-stu-id="20f08-148">To enable this capability, set the `apiKey` to a value (ideally a strong password) and add a key called `appSettings/requireApiKey` with the value of `true`:</span></span>

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="20f08-149">Sunucunuz zaten korunuyor veya aksi halde bir API anahtarı (örneğin, özel bir sunucu yerel takım ağında kullanırken) gerektirmez, ayarlayabileceğiniz `requireApiKey` için `false`.</span><span class="sxs-lookup"><span data-stu-id="20f08-149">If your server is already secured or you do not otherwise require an API key (for example, when using a private server on a local team network), you can set `requireApiKey` to `false`.</span></span> <span data-ttu-id="20f08-150">Sunucu erişimi olan tüm kullanıcılar, ardından paketleri gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="20f08-150">All users with access to the server can then push packages.</span></span>

## <a name="removing-packages-from-the-feed"></a><span data-ttu-id="20f08-151">Akıştan paketlerini kaldırma</span><span class="sxs-lookup"><span data-stu-id="20f08-151">Removing packages from the feed</span></span>

<span data-ttu-id="20f08-152">NuGet.Server ile [nuget silmek](../tools/cli-ref-delete.md) komutu açıklamayı içeren API anahtarı eklemek koşuluyla, bir paket depodan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="20f08-152">With NuGet.Server, the [nuget delete](../tools/cli-ref-delete.md) command removes a package from the repository provided that you include the API key with the comment.</span></span>

<span data-ttu-id="20f08-153">Bunun yerine paket delist davranışı değiştirmek isterseniz (paket geri yükleme için kullanılabilir bırakarak), değiştirme `enableDelisting` anahtarını `web.config` true.</span><span class="sxs-lookup"><span data-stu-id="20f08-153">If you want to change the behavior to delist the package instead (leaving it available for package restore), change the `enableDelisting` key in `web.config` to true.</span></span>

## <a name="nugetserver-support"></a><span data-ttu-id="20f08-154">NuGet.Server desteği</span><span class="sxs-lookup"><span data-stu-id="20f08-154">NuGet.Server support</span></span>

<span data-ttu-id="20f08-155">Ek Yardım için NuGet.Server, kullanarak oluşturduğunuz bir sorun üzerinde [ https://github.com/nuget/NuGetGallery/issues ](https://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="20f08-155">For additional help using NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>