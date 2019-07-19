---
title: NuGet akışlarını barındırmak için NuGet. Server kullanma
description: NuGet. Server kullanarak IIS çalıştıran herhangi bir sunucuda NuGet paket akışı oluşturma ve barındırma, paketleri HTTP ve OData aracılığıyla kullanılabilir hale getirme.
author: karann-msft
ms.author: karann
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: 734f0a609f243c7bdb218a53ed664de68c707dd7
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317655"
---
# <a name="nugetserver"></a><span data-ttu-id="db989-103">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="db989-103">NuGet.Server</span></span>

<span data-ttu-id="db989-104">NuGet. Server, .NET Foundation tarafından sunulan ve IIS çalıştıran herhangi bir sunucuda paket akışını barındırasağlayan bir ASP.NET uygulaması oluşturan bir pakettir.</span><span class="sxs-lookup"><span data-stu-id="db989-104">NuGet.Server is a package provided by the .NET Foundation that creates an ASP.NET application that can host a package feed on any server that runs IIS.</span></span> <span data-ttu-id="db989-105">Yalnızca NuGet. Server, sunucudaki bir klasörü HTTP (S) (özellikle OData) üzerinden kullanılabilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="db989-105">Simply said, NuGet.Server makes a folder on the server available through HTTP(S) (specifically OData).</span></span> <span data-ttu-id="db989-106">Kolayca ayarlanabilir ve basit senaryolar için idealdir.</span><span class="sxs-lookup"><span data-stu-id="db989-106">It's easy to set up and is best for simple scenarios.</span></span>

1. <span data-ttu-id="db989-107">Visual Studio 'da boş bir ASP.NET Web uygulaması oluşturun ve NuGet. Server paketini buna ekleyin.</span><span class="sxs-lookup"><span data-stu-id="db989-107">Create an empty ASP.NET Web application in Visual Studio and add the NuGet.Server package to it.</span></span>
1. <span data-ttu-id="db989-108">`Packages` Uygulamadaki klasörü yapılandırın ve paketleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="db989-108">Configure the `Packages` folder in the application and add packages.</span></span>
1. <span data-ttu-id="db989-109">Uygulamayı uygun bir sunucuya dağıtın.</span><span class="sxs-lookup"><span data-stu-id="db989-109">Deploy the application to a suitable server.</span></span>

<span data-ttu-id="db989-110">Aşağıdaki bölümler, kullanarak C#bu süreci ayrıntılı bir şekilde ele vermektedir.</span><span class="sxs-lookup"><span data-stu-id="db989-110">The following sections walk through this process in detail, using C#.</span></span>

<span data-ttu-id="db989-111">NuGet. Server hakkında başka sorularınız varsa, üzerinde [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues)bir sorun oluşturun.</span><span class="sxs-lookup"><span data-stu-id="db989-111">If you have further questions about NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a><span data-ttu-id="db989-112">NuGet. Server ile bir ASP.NET Web uygulaması oluşturma ve dağıtma</span><span class="sxs-lookup"><span data-stu-id="db989-112">Create and deploy an ASP.NET Web application with NuGet.Server</span></span>

1. <span data-ttu-id="db989-113">Visual Studio 'da **dosya > yeni > proje**' yi seçin, "ASP.net" araması yapın, C#için **ASP.NET Web uygulaması (.NET Framework)** şablonunu seçin ve **Framework 'ü** ".NET Framework 4,6" olarak ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="db989-113">In Visual Studio, select **File > New > Project**, search for "ASP.NET", select the **ASP.NET Web Application (.NET Framework)** template for C#, and set **Framework** to ".NET Framework 4.6":</span></span>

    ![Yeni bir proje için hedef Framework 'ü ayarlama](media/Hosting_01-NuGet.Server-Set4.6.png)

1. <span data-ttu-id="db989-115">Uygulamaya NuGet. Server dışında uygun *bir ad verin* , Tamam ' ı seçin ve sonraki Iletişim kutusunda **boş** şablonu seçin, sonra **Tamam**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="db989-115">Give the application a suitable name *other* than NuGet.Server, select OK, and in the next dialog select the **Empty** template, then select **OK**.</span></span>

1. <span data-ttu-id="db989-116">Projeye sağ tıklayın, **NuGet Paketlerini Yönet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="db989-116">Right-click the project, select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="db989-117">Paket Yöneticisi Kullanıcı arabiriminde, **Gözden** geçirme sekmesini seçin, ardından .NET Framework 4,6 ' i hedefliyorsanız NuGet. Server paketinin en son sürümünü arayın ve yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="db989-117">In the Package Manager UI, select the **Browse** tab, then search and install the latest version of the NuGet.Server package if you're targeting .NET Framework 4.6.</span></span> <span data-ttu-id="db989-118">(Ayrıca paket yöneticisi konsolundan ile `Install-Package NuGet.Server`yükleyebilirsiniz.) İstenirse lisans koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="db989-118">(You can also install it from the Package Manager Console with `Install-Package NuGet.Server`.) Accept the license terms if prompted.</span></span>

    ![NuGet. Server paketini yükleme](media/Hosting_02-NuGet.Server-Package.png)

1. <span data-ttu-id="db989-120">NuGet. Server yükleme, boş Web uygulamasını bir paket kaynağına dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="db989-120">Installing NuGet.Server converts the empty Web application into a package source.</span></span> <span data-ttu-id="db989-121">Diğer birçok paketi kurar, uygulamada bir `Packages` klasör oluşturur ve ek ayarları dahil etmek için değiştirir `web.config` (Ayrıntılar için bu dosyadaki açıklamalara bakın).</span><span class="sxs-lookup"><span data-stu-id="db989-121">It installs a variety of other packages, creates a `Packages` folder in the application, and modifies `web.config` to include additional settings (see the comments in that file for details).</span></span>

    > [!Important]
    > <span data-ttu-id="db989-122">NuGet. `web.config` Server paketi bu dosyadaki değişikliklerini tamamladıktan sonra dikkatle inceleyin.</span><span class="sxs-lookup"><span data-stu-id="db989-122">Carefully inspect `web.config` after the NuGet.Server package has completed its modifications to that file.</span></span> <span data-ttu-id="db989-123">NuGet. Server varolan öğelerin üzerine yazmayabilir, bunun yerine yinelenen öğeler oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="db989-123">NuGet.Server may not overwrite existing elements but instead create duplicate elements.</span></span> <span data-ttu-id="db989-124">Bu yinelemeler, daha sonra Projeyi çalıştırmaya çalıştığınızda bir "Iç sunucu hatası" oluşmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="db989-124">Those duplicates will cause an "Internal Server Error" when you later try to run the project.</span></span> <span data-ttu-id="db989-125">Örneğin, `web.config` NuGet. Server 'ı `<compilation debug="true" targetFramework="4.5.2" />` yüklemeden önce içeriyorsa, paket onun üzerine yazmaz ancak ikinci `<compilation debug="true" targetFramework="4.6" />`bir ekler.</span><span class="sxs-lookup"><span data-stu-id="db989-125">For example, if your `web.config` contains `<compilation debug="true" targetFramework="4.5.2" />` before installing NuGet.Server, the package doesn't overwrite it but inserts a second `<compilation debug="true" targetFramework="4.6" />`.</span></span> <span data-ttu-id="db989-126">Bu durumda, öğesini eski Framework sürümü ile silin.</span><span class="sxs-lookup"><span data-stu-id="db989-126">In that case, delete the element with the older framework version.</span></span>

1. <span data-ttu-id="db989-127">Uygulamayı bir sunucuda yayımladığınızda paketleri akışta kullanılabilir hale getirmek için, her `.nupkg` bir dosyayı `Packages` Visual Studio 'daki klasöre ekleyin, sonra her birinin **derleme eylemini** **içerik** olarak ayarlayın ve **çıkış dizinine kopyalayın** **Her zaman Kopyala**:</span><span class="sxs-lookup"><span data-stu-id="db989-127">To make packages available in the feed when you publish the application to a server, add each `.nupkg` files to the `Packages` folder in Visual Studio, then set each one's **Build Action** to **Content** and **Copy to Output Directory** to **Copy always**:</span></span>

    ![Paketler projedeki paketler klasörüne kopyalanıyor](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. <span data-ttu-id="db989-129">Siteyi Visual Studio 'da yerel olarak çalıştırın (hata ayıklama **> kullanarak hata ayıklamadan başlayın** veya CTRL + F5).</span><span class="sxs-lookup"><span data-stu-id="db989-129">Run the site locally in Visual Studio (using **Debug > Start Without Debugging** or Ctrl+F5).</span></span> <span data-ttu-id="db989-130">Giriş sayfası, aşağıda gösterildiği gibi paket akışı URL 'Lerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="db989-130">The home page provides the package feed URLs as shown below.</span></span> <span data-ttu-id="db989-131">Hata görürseniz, daha önce 5. adımda `web.config` yinelenen öğeleri için bilgilerinizi dikkatle inceleyin.</span><span class="sxs-lookup"><span data-stu-id="db989-131">If you see errors, carefully inspect your `web.config` for duplicate elements are noted earlier with step 5.</span></span>

    ![NuGet. Server içeren bir uygulama için varsayılan giriş sayfası](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. <span data-ttu-id="db989-133">Paketlerin OData akışını görmek için yukarıda özetlenen alanda **buraya** tıklayın.</span><span class="sxs-lookup"><span data-stu-id="db989-133">Click on **here** in the area outlined above to see the OData feed of packages.</span></span>

1. <span data-ttu-id="db989-134">Uygulamayı ilk kez çalıştırdığınızda NuGet. Server, `Packages` klasörü her bir paket için bir klasör içerecek şekilde yeniden yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="db989-134">The first time you run the application, NuGet.Server restructures the `Packages` folder to contain a folder for each package.</span></span> <span data-ttu-id="db989-135">Bu, performansı artırmak için NuGet 3,3 ile sunulan [yerel depolama düzeniyle](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) eşleşir.</span><span class="sxs-lookup"><span data-stu-id="db989-135">This matches the [local storage layout](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduced with NuGet 3.3 to improve performance.</span></span> <span data-ttu-id="db989-136">Daha fazla paket eklerken bu yapıyı izlemeye devam edin.</span><span class="sxs-lookup"><span data-stu-id="db989-136">When adding more packages, continue to follow this structure.</span></span>

1. <span data-ttu-id="db989-137">Yerel dağıtımınızı sınadıktan sonra, gerektiğinde uygulamayı başka bir iç veya dış siteye dağıtın.</span><span class="sxs-lookup"><span data-stu-id="db989-137">Once you've tested your local deployment, deploy the application to any other internal or external site as needed.</span></span>

1. <span data-ttu-id="db989-138">`http://<domain>`' A dağıtıldıktan sonra, paket kaynağı için kullandığınız URL `http://<domain>/nuget`olur.</span><span class="sxs-lookup"><span data-stu-id="db989-138">Once deployed to `http://<domain>`, the URL that you use for the package source will be `http://<domain>/nuget`.</span></span>

## <a name="configuring-the-packages-folder"></a><span data-ttu-id="db989-139">Paketler klasörünü yapılandırma</span><span class="sxs-lookup"><span data-stu-id="db989-139">Configuring the Packages folder</span></span>

<span data-ttu-id="db989-140">1,5 ve sonraki sürümlerde, paket klasörünü, içindeki `appSetting/packagesPath` değeri kullanarak daha özel bir şekilde `web.config`yapılandırabilirsiniz: `NuGet.Server`</span><span class="sxs-lookup"><span data-stu-id="db989-140">With `NuGet.Server` 1.5 and later, you can more specifically configure the package folder using the `appSetting/packagesPath` value in `web.config`:</span></span>

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

<span data-ttu-id="db989-141">`packagesPath`mutlak veya sanal yol olabilir.</span><span class="sxs-lookup"><span data-stu-id="db989-141">`packagesPath` can be an absolute or virtual path.</span></span>

<span data-ttu-id="db989-142">Atlanırsa veya boş bırakılırsa, paketler klasörü varsayılandır `~/Packages`. `packagesPath`</span><span class="sxs-lookup"><span data-stu-id="db989-142">When `packagesPath` is omitted or left blank, the packages folder is the default `~/Packages`.</span></span>

## <a name="adding-packages-to-the-feed-externally"></a><span data-ttu-id="db989-143">Akışa paket dışarıdan ekleniyor</span><span class="sxs-lookup"><span data-stu-id="db989-143">Adding packages to the feed externally</span></span>

<span data-ttu-id="db989-144">NuGet. Server sitesi çalışmaya başladıktan sonra, içinde `web.config`bir API anahtarı değeri ayarlamanız kaydıyla, [NuGet Push](../reference/cli-reference/cli-ref-push.md) kullanarak paket ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="db989-144">Once a NuGet.Server site is running, you can add packages using [nuget push](../reference/cli-reference/cli-ref-push.md) provided that you set an API key value in `web.config`.</span></span>

<span data-ttu-id="db989-145">NuGet. Server paketini `web.config` yükledikten sonra boş `appSetting/apiKey` bir değer içerir:</span><span class="sxs-lookup"><span data-stu-id="db989-145">After installing the NuGet.Server package, `web.config` contains an empty `appSetting/apiKey` value:</span></span>

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="db989-146">Atlanırsa `apiKey` veya boş bırakıldığında, paketlerin akışa gönderilmesi devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="db989-146">When `apiKey` is omitted or blank, pushing packages to the feed is disabled.</span></span>

<span data-ttu-id="db989-147">Bu özelliği etkinleştirmek için, `apiKey` değerini bir değere ayarlayın (ideal bir parola) ve şu değere `true`sahip adlı `appSettings/requireApiKey` bir anahtar ekleyin:</span><span class="sxs-lookup"><span data-stu-id="db989-147">To enable this capability, set the `apiKey` to a value (ideally a strong password) and add a key called `appSettings/requireApiKey` with the value of `true`:</span></span>

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="db989-148">Sunucunuz zaten güvenli hale getirilse veya başka türlü bir API anahtarı (örneğin, yerel bir ekip ağı üzerinde bir özel sunucu kullanırken) gerektirmiyorsa, olarak `requireApiKey` `false`ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="db989-148">If your server is already secured or you do not otherwise require an API key (for example, when using a private server on a local team network), you can set `requireApiKey` to `false`.</span></span> <span data-ttu-id="db989-149">Sunucuya erişimi olan tüm kullanıcılar daha sonra paketleri gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="db989-149">All users with access to the server can then push packages.</span></span>

## <a name="removing-packages-from-the-feed"></a><span data-ttu-id="db989-150">Paketleri akıştan kaldırma</span><span class="sxs-lookup"><span data-stu-id="db989-150">Removing packages from the feed</span></span>

<span data-ttu-id="db989-151">NuGet. Server ile, [NuGet Delete](../reference/cli-reference/cli-ref-delete.md) komutu, açıklama ile API anahtarını dahil etmeniz kaydıyla bir paketi depodan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="db989-151">With NuGet.Server, the [nuget delete](../reference/cli-reference/cli-ref-delete.md) command removes a package from the repository provided that you include the API key with the comment.</span></span>

<span data-ttu-id="db989-152">Bunun yerine paketin listesini kaldırma (paket geri yükleme için kullanılabilir durumda bırakma) davranışını değiştirmek istiyorsanız, içindeki `enableDelisting` `web.config` anahtarı true olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="db989-152">If you want to change the behavior to delist the package instead (leaving it available for package restore), change the `enableDelisting` key in `web.config` to true.</span></span>

## <a name="nugetserver-support"></a><span data-ttu-id="db989-153">NuGet. Server desteği</span><span class="sxs-lookup"><span data-stu-id="db989-153">NuGet.Server support</span></span>

<span data-ttu-id="db989-154">NuGet. Server kullanarak ek yardım için, üzerinde [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues)bir sorun oluşturun.</span><span class="sxs-lookup"><span data-stu-id="db989-154">For additional help using NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>