---
title: "NuGet barındırmak için NuGet.Server kullanarak akışları | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet.Server kullanarak, paketleri HTTP ve OData yoluyla kullanılabilir hale getirme IIS çalıştıran herhangi bir sunucuda nasıl oluşturulacağı ve bir NuGet paketi konak akış."
keywords: "Akış, NuGet NuGet galerisinde, akış, Uzak paket NuGet.Server"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4cb3f04954fac1b4a39284be187776ab4a19b364
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/02/2018
---
# <a name="nugetserver"></a><span data-ttu-id="41064-104">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="41064-104">NuGet.Server</span></span>

<span data-ttu-id="41064-105">NuGet.Server, IIS çalıştıran herhangi bir sunucu üzerinde akış paket barındırabilen bir ASP.NET uygulaması oluşturur .NET Foundation tarafından sağlanan bir pakettir.</span><span class="sxs-lookup"><span data-stu-id="41064-105">NuGet.Server is a package provided by the .NET Foundation that creates an ASP.NET application that can host a package feed on any server that runs IIS.</span></span> <span data-ttu-id="41064-106">Kısaca, NuGet.Server sunucusundaki bir klasöre aracılığıyla HTTP (S) (özellikle OData) kullanılabilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="41064-106">Simply said, NuGet.Server makes a folder on the server available through HTTP(S) (specifically OData).</span></span> <span data-ttu-id="41064-107">Ayarlamak kolaydır ve basit senaryoları için en iyisidir.</span><span class="sxs-lookup"><span data-stu-id="41064-107">It's easy to set up and is best for simple scenarios.</span></span>

1. <span data-ttu-id="41064-108">Visual Studio'da boş bir ASP.NET Web uygulaması oluşturun ve NuGet.Server paketi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="41064-108">Create an empty ASP.NET Web application in Visual Studio and add the NuGet.Server package to it.</span></span>
1. <span data-ttu-id="41064-109">Yapılandırma `Packages` uygulama klasöründe ve paketleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="41064-109">Configure the `Packages` folder in the application and add packages.</span></span>
1. <span data-ttu-id="41064-110">Uygun bir sunucu uygulamayı dağıtın.</span><span class="sxs-lookup"><span data-stu-id="41064-110">Deploy the application to a suitable server.</span></span>

<span data-ttu-id="41064-111">Aşağıdaki bölümlerde bu işlem C# kullanarak ayrıntılı yol.</span><span class="sxs-lookup"><span data-stu-id="41064-111">The following sections walk through this process in detail, using C#.</span></span>

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a><span data-ttu-id="41064-112">Bir ASP.NET Web uygulama NuGet.Server ile oluşturun ve dağıtın</span><span class="sxs-lookup"><span data-stu-id="41064-112">Create and deploy an ASP.NET Web application with NuGet.Server</span></span>

1. <span data-ttu-id="41064-113">Visual Studio'da seçin **Dosya > Yeni > Proje**, .NET Framework 4.6 (aşağıya bakın), "ASP.NET" için arama için hedef Framework'ü ayarlayabilir ve seçin **ASP.NET Web uygulaması (.NET Framework)** Şablon için C#.</span><span class="sxs-lookup"><span data-stu-id="41064-113">In Visual Studio, select **File > New > Project**, set the target framework for .NET Framework 4.6 (see below), search for "ASP.NET", and select the **ASP.NET Web Application (.NET Framework)** template for C#.</span></span>

    ![.NET Framework hedef 4.6 için ayarlama](media/Hosting_01-NuGet.Server-Set4.6.png)

1. <span data-ttu-id="41064-115">Uygulama uygun bir ad verin *diğer* NuGet.Server Tamam ve sonraki iletişim kutusunda seçin **boş** şablonu ve select Tamam.</span><span class="sxs-lookup"><span data-stu-id="41064-115">Give the application a suitable name *other* than NuGet.Server, select OK, and in the next dialog select the **Empty** template and select OK.</span></span>

1. <span data-ttu-id="41064-116">Projeye sağ tıklayın, **NuGet paketlerini Yönet**, Paket Yöneticisi Arabiriminde arayın ve .NET Framework 4.6 hedefleme NuGet.Server paketinin en son sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="41064-116">Right-click the project, select **Manage NuGet Packages**, and in the Package Manager UI search and install the latest version of the NuGet.Server package if you're targeting .NET Framework 4.6.</span></span> <span data-ttu-id="41064-117">(İle Paket Yöneticisi Konsolu'ndan de yükleyebilirsiniz `Install-Package NuGet.Server`.)</span><span class="sxs-lookup"><span data-stu-id="41064-117">(You can also install it from the Package Manager Console with `Install-Package NuGet.Server`.)</span></span>

    ![NuGet.Server paketi yükleniyor](media/Hosting_02-NuGet.Server-Package.png)

    > [!Important]
    > <span data-ttu-id="41064-119">Web uygulamanız .NET Framework 4.5.2 hedefliyorsa, NuGet sunucusu yüklemeniz gerekir **2.10.3** yerine.</span><span class="sxs-lookup"><span data-stu-id="41064-119">If your web application targets .NET Framework 4.5.2, you must install NuGet Server **2.10.3** instead.</span></span>

1. <span data-ttu-id="41064-120">NuGet.Server yükleme boş bir Web uygulaması bir paket kaynağına dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="41064-120">Installing NuGet.Server converts the empty Web application into a package source.</span></span> <span data-ttu-id="41064-121">Oluşturduğu bir `Packages` uygulama klasöründe ve üzerine yazar `web.config` (bkz. Ayrıntılar için bu dosyayı açıklamalarda) ek ayarlar dahil etmek için.</span><span class="sxs-lookup"><span data-stu-id="41064-121">It creates a `Packages` folder in the application and overwrites `web.config` to include additional settings (see the comments in that file for details).</span></span>

1. <span data-ttu-id="41064-122">Bir sunucuya uygulama yayımladığınızda, paketleri akıştaki kullanılabilir kılmak için eklemeniz kendi `.nupkg` dosyaları `Packages` klasörü Visual Studio'da sonra ayarlanmış kendi **yapı eylemi** için **İçerik**ve **çıktı dizinine Kopyala** için **her zaman Kopyala**:</span><span class="sxs-lookup"><span data-stu-id="41064-122">To make packages available in the feed when you publish the application to a server, add their `.nupkg` files to the `Packages` folder in Visual Studio, then set their **Build Action** to **Content** and **Copy to Output Directory** to **Copy always**:</span></span>

    ![Paketleri projesinde paketleri klasöre kopyalama](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. <span data-ttu-id="41064-124">Site (hata ayıklama olmadan, yani Ctrl + F5) Visual Studio'da yerel olarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="41064-124">Run the site locally in Visual Studio (without debugging, that is Ctrl+F5).</span></span> <span data-ttu-id="41064-125">Giriş sayfası URL'leri paket akışı sağlar:</span><span class="sxs-lookup"><span data-stu-id="41064-125">The home page provides the package feed URLs:</span></span>

    ![NuGet.Server olan bir uygulama için varsayılan giriş sayfası](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. <span data-ttu-id="41064-127">Tıklayın **burada** paketlerin OData akışı görmek için yukarıda özetlenen alanında.</span><span class="sxs-lookup"><span data-stu-id="41064-127">Click on **here** in the area outlined above to see the OData feed of packages.</span></span>

1. <span data-ttu-id="41064-128">İlk kez uygulamayı çalıştırın, NuGet.Server yeniden yapılandırır `Packages` her paket için bir klasör içeren klasör.</span><span class="sxs-lookup"><span data-stu-id="41064-128">The first time you run the application, NuGet.Server restructures the `Packages` folder to contain a folder for each package.</span></span> <span data-ttu-id="41064-129">Bu eşleşen [yerel depolama düzeni](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) performansını artırmak için NuGet 3.3 ile sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="41064-129">This matches the [local storage layout](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduced with NuGet 3.3 to improve performance.</span></span> <span data-ttu-id="41064-130">Daha fazla paket eklerken, bu yapıyı izlemeye devam edin.</span><span class="sxs-lookup"><span data-stu-id="41064-130">When adding more packages, continue to follow this structure.</span></span>

1. <span data-ttu-id="41064-131">Yerel dağıtımınızı test ettikten sonra diğer iç veya dış site uygulamaya gerektiği gibi dağıtın.</span><span class="sxs-lookup"><span data-stu-id="41064-131">Once you've tested your local deployment, deploy the application to any other internal or external site as needed.</span></span>
1. <span data-ttu-id="41064-132">Dağıtıldıktan sonra `http://<domain>`, paket kaynağı için kullandığınız URL'yi olacaktır `http://<domain>/nuget`.</span><span class="sxs-lookup"><span data-stu-id="41064-132">Once deployed to `http://<domain>`, the URL that you use for the package source will be `http://<domain>/nuget`.</span></span>

## <a name="configuring-the-packages-folder"></a><span data-ttu-id="41064-133">Paketler klasörü yapılandırma</span><span class="sxs-lookup"><span data-stu-id="41064-133">Configuring the Packages folder</span></span>

<span data-ttu-id="41064-134">İle `NuGet.Server` 1,5 ve daha sonra daha açık belirtmek gerekirse paket klasörünü kullanarak yapılandırabileceğiniz `appSetting/packagesPath` değeri `web.config`:</span><span class="sxs-lookup"><span data-stu-id="41064-134">With `NuGet.Server` 1.5 and later, you can more specifically configure the package folder using the `appSetting/packagesPath` value in `web.config`:</span></span>

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

<span data-ttu-id="41064-135">`packagesPath`mutlak ya da sanal bir yol olabilir.</span><span class="sxs-lookup"><span data-stu-id="41064-135">`packagesPath` can be an absolute or virtual path.</span></span>

<span data-ttu-id="41064-136">Zaman `packagesPath` atlanmış veya boş, sol varsayılan paketleri klasörüdür `~/Packages`.</span><span class="sxs-lookup"><span data-stu-id="41064-136">When `packagesPath` is omitted or left blank, the packages folder is the default `~/Packages`.</span></span>

## <a name="adding-packages-to-the-feed-externally"></a><span data-ttu-id="41064-137">Akışa dışarıdan paketleri ekleme</span><span class="sxs-lookup"><span data-stu-id="41064-137">Adding packages to the feed externally</span></span>

<span data-ttu-id="41064-138">NuGet.Server site çalışmaya başladıktan sonra ekleme veya API anahtar değeri ayarlanmış koşuluyla, nuget.exe kullanarak paketleri silme `web.config`.</span><span class="sxs-lookup"><span data-stu-id="41064-138">Once a NuGet.Server site is running, you can add or delete packages using nuget.exe provided that you set an API key value in `web.config`.</span></span>

<span data-ttu-id="41064-139">NuGet.Server paketini yükledikten sonra `web.config` boş bir içeren `appSetting/apiKey` değeri:</span><span class="sxs-lookup"><span data-stu-id="41064-139">After installing the NuGet.Server package, `web.config` contains an empty `appSetting/apiKey` value:</span></span>

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="41064-140">Zaman `apiKey` atlanmış veya boş, paketleri akışa Ftp'den devre dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="41064-140">When `apiKey` is omitted or blank, pushing packages to the feed is disabled.</span></span>

<span data-ttu-id="41064-141">Bu özelliği etkinleştirmek için ayarlanmış `apiKey` bir değere (İdeal olarak güçlü bir parola) adlı bir anahtar ekleyin `appSettings/requireApiKey` değeriyle `true`:</span><span class="sxs-lookup"><span data-stu-id="41064-141">To enable this capability, set the `apiKey` to a value (ideally a strong password) and add a key called `appSettings/requireApiKey` with the value of `true`:</span></span>

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="41064-142">Sunucunuz zaten korunuyor veya aksi halde bir API anahtarı (örneğin, özel bir sunucu yerel takım ağında kullanırken) gerektirmez, ayarlayabileceğiniz `requireApiKey` için `false`.</span><span class="sxs-lookup"><span data-stu-id="41064-142">If your server is already secured or you do not otherwise require an API key (for example, when using a private server on a local team network), you can set `requireApiKey` to `false`.</span></span> <span data-ttu-id="41064-143">Sunucu erişimi olan tüm kullanıcılar sonra push veya paketleri silmek.</span><span class="sxs-lookup"><span data-stu-id="41064-143">All users with access to the server can then push or delete packages.</span></span>