---
title: NuGet akışlarını barındırmak için NuGet. Server kullanma
description: NuGet. Server kullanarak IIS çalıştıran herhangi bir sunucuda NuGet paket akışı oluşturma ve barındırma, paketleri HTTP ve OData aracılığıyla kullanılabilir hale getirme.
author: karann-msft
ms.author: karann
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: 82b353450ff1da23a17e5b1c6a825ad32782bf75
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610601"
---
# <a name="nugetserver"></a><span data-ttu-id="39b3a-103">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="39b3a-103">NuGet.Server</span></span>

<span data-ttu-id="39b3a-104">NuGet. Server, .NET Foundation tarafından sunulan ve IIS çalıştıran herhangi bir sunucuda paket akışını barındırasağlayan bir ASP.NET uygulaması oluşturan bir pakettir.</span><span class="sxs-lookup"><span data-stu-id="39b3a-104">NuGet.Server is a package provided by the .NET Foundation that creates an ASP.NET application that can host a package feed on any server that runs IIS.</span></span> <span data-ttu-id="39b3a-105">Yalnızca NuGet. Server, sunucudaki bir klasörü HTTP (S) (özellikle OData) üzerinden kullanılabilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="39b3a-105">Simply said, NuGet.Server makes a folder on the server available through HTTP(S) (specifically OData).</span></span> <span data-ttu-id="39b3a-106">Kolayca ayarlanabilir ve basit senaryolar için idealdir.</span><span class="sxs-lookup"><span data-stu-id="39b3a-106">It's easy to set up and is best for simple scenarios.</span></span>

1. <span data-ttu-id="39b3a-107">Visual Studio 'da boş bir ASP.NET Web uygulaması oluşturun ve NuGet. Server paketini buna ekleyin.</span><span class="sxs-lookup"><span data-stu-id="39b3a-107">Create an empty ASP.NET Web application in Visual Studio and add the NuGet.Server package to it.</span></span>
1. <span data-ttu-id="39b3a-108">Uygulamada `Packages` klasörünü yapılandırın ve paketleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="39b3a-108">Configure the `Packages` folder in the application and add packages.</span></span>
1. <span data-ttu-id="39b3a-109">Uygulamayı uygun bir sunucuya dağıtın.</span><span class="sxs-lookup"><span data-stu-id="39b3a-109">Deploy the application to a suitable server.</span></span>

<span data-ttu-id="39b3a-110">Aşağıdaki bölümler, kullanarak C#bu süreci ayrıntılı bir şekilde ele vermektedir.</span><span class="sxs-lookup"><span data-stu-id="39b3a-110">The following sections walk through this process in detail, using C#.</span></span>

<span data-ttu-id="39b3a-111">NuGet. Server hakkında başka sorularınız varsa [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues)bir sorun oluşturun.</span><span class="sxs-lookup"><span data-stu-id="39b3a-111">If you have further questions about NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a><span data-ttu-id="39b3a-112">NuGet. Server ile bir ASP.NET Web uygulaması oluşturma ve dağıtma</span><span class="sxs-lookup"><span data-stu-id="39b3a-112">Create and deploy an ASP.NET Web application with NuGet.Server</span></span>

1. <span data-ttu-id="39b3a-113">Visual Studio 'da **dosya > yeni > proje**' yi seçin, "ASP.net" araması yapın, C#için **ASP.NET Web uygulaması (.NET Framework)** şablonunu seçin ve **Framework 'ü** ".NET Framework 4,6" olarak ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="39b3a-113">In Visual Studio, select **File > New > Project**, search for "ASP.NET", select the **ASP.NET Web Application (.NET Framework)** template for C#, and set **Framework** to ".NET Framework 4.6":</span></span>

    ![Yeni bir proje için hedef Framework 'ü ayarlama](media/Hosting_01-NuGet.Server-Set4.6.png)

1. <span data-ttu-id="39b3a-115">Uygulamaya NuGet. *Server dışında uygun bir ad verin* , Tamam ' ı seçin ve sonraki Iletişim kutusunda **boş** şablonu seçin, sonra **Tamam**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="39b3a-115">Give the application a suitable name *other* than NuGet.Server, select OK, and in the next dialog select the **Empty** template, then select **OK**.</span></span>

1. <span data-ttu-id="39b3a-116">Projeye sağ tıklayın, **NuGet Paketlerini Yönet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="39b3a-116">Right-click the project, select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="39b3a-117">Paket Yöneticisi Kullanıcı arabiriminde, **Gözden** geçirme sekmesini seçin, ardından .NET Framework 4,6 ' i hedefliyorsanız NuGet. Server paketinin en son sürümünü arayın ve yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="39b3a-117">In the Package Manager UI, select the **Browse** tab, then search and install the latest version of the NuGet.Server package if you're targeting .NET Framework 4.6.</span></span> <span data-ttu-id="39b3a-118">(Aynı zamanda, `Install-Package NuGet.Server`ile paket yöneticisi konsolundan da yükleyebilirsiniz.) İstenirse lisans koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="39b3a-118">(You can also install it from the Package Manager Console with `Install-Package NuGet.Server`.) Accept the license terms if prompted.</span></span>

    ![NuGet. Server paketini yükleme](media/Hosting_02-NuGet.Server-Package.png)

1. <span data-ttu-id="39b3a-120">NuGet. Server yükleme, boş Web uygulamasını bir paket kaynağına dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="39b3a-120">Installing NuGet.Server converts the empty Web application into a package source.</span></span> <span data-ttu-id="39b3a-121">Çeşitli diğer paketleri yüklerken, uygulamada bir `Packages` klasörü oluşturur ve `web.config` ek ayarları içerecek şekilde değiştirir (Ayrıntılar için bu dosyadaki açıklamalara bakın).</span><span class="sxs-lookup"><span data-stu-id="39b3a-121">It installs a variety of other packages, creates a `Packages` folder in the application, and modifies `web.config` to include additional settings (see the comments in that file for details).</span></span>

    > [!Important]
    > <span data-ttu-id="39b3a-122">NuGet. Server paketi bu dosyadaki değişikliklerini tamamladıktan sonra `web.config` dikkatle inceleyin.</span><span class="sxs-lookup"><span data-stu-id="39b3a-122">Carefully inspect `web.config` after the NuGet.Server package has completed its modifications to that file.</span></span> <span data-ttu-id="39b3a-123">NuGet. Server varolan öğelerin üzerine yazmayabilir, bunun yerine yinelenen öğeler oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="39b3a-123">NuGet.Server may not overwrite existing elements but instead create duplicate elements.</span></span> <span data-ttu-id="39b3a-124">Bu yinelemeler, daha sonra Projeyi çalıştırmaya çalıştığınızda bir "Iç sunucu hatası" oluşmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="39b3a-124">Those duplicates will cause an "Internal Server Error" when you later try to run the project.</span></span> <span data-ttu-id="39b3a-125">Örneğin, `web.config` NuGet. Server yüklenmeden önce `<compilation debug="true" targetFramework="4.5.2" />` içeriyorsa, paket onun üzerine yazmaz ancak ikinci bir `<compilation debug="true" targetFramework="4.6" />`ekler.</span><span class="sxs-lookup"><span data-stu-id="39b3a-125">For example, if your `web.config` contains `<compilation debug="true" targetFramework="4.5.2" />` before installing NuGet.Server, the package doesn't overwrite it but inserts a second `<compilation debug="true" targetFramework="4.6" />`.</span></span> <span data-ttu-id="39b3a-126">Bu durumda, öğesini eski Framework sürümü ile silin.</span><span class="sxs-lookup"><span data-stu-id="39b3a-126">In that case, delete the element with the older framework version.</span></span>

1. <span data-ttu-id="39b3a-127">Uygulamayı bir sunucuda yayımladığınızda paketleri akışta kullanılabilir hale getirmek için, her bir `.nupkg` dosyasını Visual Studio 'daki `Packages` klasörüne ekleyin, sonra her birinin **derleme eylemini** **içerik** olarak ayarlayın ve kopyalanacak **çıkış dizinine kopyalayın**  **her zaman**:</span><span class="sxs-lookup"><span data-stu-id="39b3a-127">To make packages available in the feed when you publish the application to a server, add each `.nupkg` files to the `Packages` folder in Visual Studio, then set each one's **Build Action** to **Content** and **Copy to Output Directory** to **Copy always**:</span></span>

    ![Paketler projedeki paketler klasörüne kopyalanıyor](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. <span data-ttu-id="39b3a-129">Siteyi Visual Studio 'da yerel olarak çalıştırın (hata ayıklama **> kullanarak hata ayıklamadan başlayın** veya CTRL + F5).</span><span class="sxs-lookup"><span data-stu-id="39b3a-129">Run the site locally in Visual Studio (using **Debug > Start Without Debugging** or Ctrl+F5).</span></span> <span data-ttu-id="39b3a-130">Giriş sayfası, aşağıda gösterildiği gibi paket akışı URL 'Lerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="39b3a-130">The home page provides the package feed URLs as shown below.</span></span> <span data-ttu-id="39b3a-131">Hata görürseniz, daha önce 5. adımda yinelenen öğeler için `web.config` dikkatle inceleyin.</span><span class="sxs-lookup"><span data-stu-id="39b3a-131">If you see errors, carefully inspect your `web.config` for duplicate elements are noted earlier with step 5.</span></span>

    ![NuGet. Server içeren bir uygulama için varsayılan giriş sayfası](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. <span data-ttu-id="39b3a-133">Paketlerin OData akışını görmek için yukarıda özetlenen alanda **buraya** tıklayın.</span><span class="sxs-lookup"><span data-stu-id="39b3a-133">Click on **here** in the area outlined above to see the OData feed of packages.</span></span>

1. <span data-ttu-id="39b3a-134">Uygulamayı ilk kez çalıştırdığınızda, NuGet. Server `Packages` klasörünü her bir paket için bir klasör içerecek şekilde yeniden yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="39b3a-134">The first time you run the application, NuGet.Server restructures the `Packages` folder to contain a folder for each package.</span></span> <span data-ttu-id="39b3a-135">Bu, performansı artırmak için NuGet 3,3 ile sunulan [yerel depolama düzeniyle](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) eşleşir.</span><span class="sxs-lookup"><span data-stu-id="39b3a-135">This matches the [local storage layout](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduced with NuGet 3.3 to improve performance.</span></span> <span data-ttu-id="39b3a-136">Daha fazla paket eklerken bu yapıyı izlemeye devam edin.</span><span class="sxs-lookup"><span data-stu-id="39b3a-136">When adding more packages, continue to follow this structure.</span></span>

1. <span data-ttu-id="39b3a-137">Yerel dağıtımınızı sınadıktan sonra, gerektiğinde uygulamayı başka bir iç veya dış siteye dağıtın.</span><span class="sxs-lookup"><span data-stu-id="39b3a-137">Once you've tested your local deployment, deploy the application to any other internal or external site as needed.</span></span>

1. <span data-ttu-id="39b3a-138">`http://<domain>`için dağıtıldıktan sonra, paket kaynağı için kullandığınız URL `http://<domain>/nuget`olur.</span><span class="sxs-lookup"><span data-stu-id="39b3a-138">Once deployed to `http://<domain>`, the URL that you use for the package source will be `http://<domain>/nuget`.</span></span>

## <a name="configuring-the-packages-folder"></a><span data-ttu-id="39b3a-139">Paketler klasörünü yapılandırma</span><span class="sxs-lookup"><span data-stu-id="39b3a-139">Configuring the Packages folder</span></span>

<span data-ttu-id="39b3a-140">`NuGet.Server` 1,5 ve üzeri sürümlerde, paket klasörünü, `web.config``appSetting/packagesPath` değerini kullanarak daha özel bir şekilde yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="39b3a-140">With `NuGet.Server` 1.5 and later, you can more specifically configure the package folder using the `appSetting/packagesPath` value in `web.config`:</span></span>

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

<span data-ttu-id="39b3a-141">`packagesPath` mutlak veya sanal yol olabilir.</span><span class="sxs-lookup"><span data-stu-id="39b3a-141">`packagesPath` can be an absolute or virtual path.</span></span>

<span data-ttu-id="39b3a-142">`packagesPath` atlandığında veya boş bırakıldığında, paketler klasörü varsayılan `~/Packages`.</span><span class="sxs-lookup"><span data-stu-id="39b3a-142">When `packagesPath` is omitted or left blank, the packages folder is the default `~/Packages`.</span></span>

## <a name="adding-packages-to-the-feed-externally"></a><span data-ttu-id="39b3a-143">Akışa paket dışarıdan ekleniyor</span><span class="sxs-lookup"><span data-stu-id="39b3a-143">Adding packages to the feed externally</span></span>

<span data-ttu-id="39b3a-144">NuGet. Server sitesi çalışmaya başladıktan sonra, `web.config`içinde bir API anahtar değeri ayarlamanız kaydıyla, [NuGet Push](../reference/cli-reference/cli-ref-push.md) kullanarak paket ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="39b3a-144">Once a NuGet.Server site is running, you can add packages using [nuget push](../reference/cli-reference/cli-ref-push.md) provided that you set an API key value in `web.config`.</span></span>

<span data-ttu-id="39b3a-145">NuGet. Server paketini yükledikten sonra `web.config` boş bir `appSetting/apiKey` değeri içerir:</span><span class="sxs-lookup"><span data-stu-id="39b3a-145">After installing the NuGet.Server package, `web.config` contains an empty `appSetting/apiKey` value:</span></span>

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="39b3a-146">`apiKey` atlandığında veya boş bırakıldığında, paketlerin akışa gönderilmesi devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="39b3a-146">When `apiKey` is omitted or blank, pushing packages to the feed is disabled.</span></span>

<span data-ttu-id="39b3a-147">Bu özelliği etkinleştirmek için, `apiKey` bir değere ayarlayın (ideal bir parola) ve `true`değerine sahip `appSettings/requireApiKey` adlı bir anahtar ekleyin:</span><span class="sxs-lookup"><span data-stu-id="39b3a-147">To enable this capability, set the `apiKey` to a value (ideally a strong password) and add a key called `appSettings/requireApiKey` with the value of `true`:</span></span>

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="39b3a-148">Sunucunuz zaten güvenli hale getirilse veya başka türlü bir API anahtarı (örneğin, yerel bir ekip ağı üzerinde bir özel sunucu kullanırken) gerektirmiyorsa, `false``requireApiKey` ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="39b3a-148">If your server is already secured or you do not otherwise require an API key (for example, when using a private server on a local team network), you can set `requireApiKey` to `false`.</span></span> <span data-ttu-id="39b3a-149">Sunucuya erişimi olan tüm kullanıcılar daha sonra paketleri gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="39b3a-149">All users with access to the server can then push packages.</span></span>

## <a name="removing-packages-from-the-feed"></a><span data-ttu-id="39b3a-150">Paketleri akıştan kaldırma</span><span class="sxs-lookup"><span data-stu-id="39b3a-150">Removing packages from the feed</span></span>

<span data-ttu-id="39b3a-151">NuGet. Server ile, [NuGet Delete](../reference/cli-reference/cli-ref-delete.md) komutu, açıklama ile API anahtarını dahil etmeniz kaydıyla bir paketi depodan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="39b3a-151">With NuGet.Server, the [nuget delete](../reference/cli-reference/cli-ref-delete.md) command removes a package from the repository provided that you include the API key with the comment.</span></span>

<span data-ttu-id="39b3a-152">Bunun yerine paketin listesini kaldırma (paket geri yükleme için kullanılabilir durumda bırakma) davranışını değiştirmek istiyorsanız, `web.config` `enableDelisting` anahtarını true olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="39b3a-152">If you want to change the behavior to delist the package instead (leaving it available for package restore), change the `enableDelisting` key in `web.config` to true.</span></span>

## <a name="nugetserver-support"></a><span data-ttu-id="39b3a-153">NuGet. Server desteği</span><span class="sxs-lookup"><span data-stu-id="39b3a-153">NuGet.Server support</span></span>

<span data-ttu-id="39b3a-154">NuGet. Server kullanarak ek yardım için [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues)bir sorun oluşturun.</span><span class="sxs-lookup"><span data-stu-id="39b3a-154">For additional help using NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>