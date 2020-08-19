---
title: NuGet akışlarını barındırmak için NuGet. Server kullanma
description: NuGet. Server kullanarak IIS çalıştıran herhangi bir sunucuda NuGet paket akışı oluşturma ve barındırma, paketleri HTTP ve OData aracılığıyla kullanılabilir hale getirme.
author: karann-msft
ms.author: karann
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: 7a806e6b586c63c701642c9e43865cb077d7999c
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623051"
---
# <a name="nugetserver"></a><span data-ttu-id="af852-103">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="af852-103">NuGet.Server</span></span>

<span data-ttu-id="af852-104">NuGet. Server, .NET Foundation tarafından sunulan ve IIS çalıştıran herhangi bir sunucuda paket akışını barındırasağlayan bir ASP.NET uygulaması oluşturan bir pakettir.</span><span class="sxs-lookup"><span data-stu-id="af852-104">NuGet.Server is a package provided by the .NET Foundation that creates an ASP.NET application that can host a package feed on any server that runs IIS.</span></span> <span data-ttu-id="af852-105">Yalnızca NuGet. Server, sunucudaki bir klasörü HTTP (S) (özellikle OData) üzerinden kullanılabilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="af852-105">Simply said, NuGet.Server makes a folder on the server available through HTTP(S) (specifically OData).</span></span> <span data-ttu-id="af852-106">Kolayca ayarlanabilir ve basit senaryolar için idealdir.</span><span class="sxs-lookup"><span data-stu-id="af852-106">It's easy to set up and is best for simple scenarios.</span></span>

1. <span data-ttu-id="af852-107">Visual Studio 'da boş bir ASP.NET Web uygulaması oluşturun ve NuGet. Server paketini buna ekleyin.</span><span class="sxs-lookup"><span data-stu-id="af852-107">Create an empty ASP.NET Web application in Visual Studio and add the NuGet.Server package to it.</span></span>
1. <span data-ttu-id="af852-108">`Packages`Uygulamadaki klasörü yapılandırın ve paketleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="af852-108">Configure the `Packages` folder in the application and add packages.</span></span>
1. <span data-ttu-id="af852-109">Uygulamayı uygun bir sunucuya dağıtın.</span><span class="sxs-lookup"><span data-stu-id="af852-109">Deploy the application to a suitable server.</span></span>

<span data-ttu-id="af852-110">Aşağıdaki bölümler, C# kullanarak bu süreci ayrıntılı olarak göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="af852-110">The following sections walk through this process in detail, using C#.</span></span>

<span data-ttu-id="af852-111">NuGet. Server hakkında başka sorularınız varsa, üzerinde bir sorun oluşturun [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues) .</span><span class="sxs-lookup"><span data-stu-id="af852-111">If you have further questions about NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a><span data-ttu-id="af852-112">NuGet. Server ile bir ASP.NET Web uygulaması oluşturma ve dağıtma</span><span class="sxs-lookup"><span data-stu-id="af852-112">Create and deploy an ASP.NET Web application with NuGet.Server</span></span>

1. <span data-ttu-id="af852-113">Visual Studio 'da **dosya > yeni > proje**' yi seçin, "ASP.NET Web uygulaması (.NET Framework)" araması yapın, **C#** için eşleşen şablonu seçin.</span><span class="sxs-lookup"><span data-stu-id="af852-113">In Visual Studio, select **File > New > Project**, search for "ASP.NET Web Application (.NET Framework)", select the matching template for **C#**.</span></span>

    ![.NET Framework Web projesi şablonunu seçin](media/Hosting_00-NuGet.Server-ProjectType.png)

1. <span data-ttu-id="af852-115">**Framework 'ü** ".NET Framework 4,6" olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="af852-115">Set **Framework** to ".NET Framework 4.6".</span></span>

    ![Yeni bir proje için hedef Framework 'ü ayarlama](media/Hosting_01-NuGet.Server-Set4.6.png)

1. <span data-ttu-id="af852-117">Uygulamaya NuGet. *Server dışında uygun bir ad verin* , Tamam ' ı seçin ve sonraki Iletişim kutusunda **boş** şablonu seçin, sonra **Tamam**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="af852-117">Give the application a suitable name *other* than NuGet.Server, select OK, and in the next dialog select the **Empty** template, then select **OK**.</span></span>

    ![Boş Web projesini seçin](media/Hosting_02-NuGet.Server-Empty.png)

1. <span data-ttu-id="af852-119">Projeye sağ tıklayın, **NuGet Paketlerini Yönet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="af852-119">Right-click the project, select **Manage NuGet Packages**.</span></span>

1. <span data-ttu-id="af852-120">Paket Yöneticisi Kullanıcı arabiriminde, **Gözden** geçirme sekmesini seçin, ardından .NET Framework 4,6 ' i hedefliyorsanız NuGet. Server paketinin en son sürümünü arayın ve yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="af852-120">In the Package Manager UI, select the **Browse** tab, then search and install the latest version of the NuGet.Server package if you're targeting .NET Framework 4.6.</span></span> <span data-ttu-id="af852-121">(Ayrıca paket yöneticisi konsolundan ile yükleyebilirsiniz `Install-Package NuGet.Server` .) İstenirse lisans koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="af852-121">(You can also install it from the Package Manager Console with `Install-Package NuGet.Server`.) Accept the license terms if prompted.</span></span>

    ![NuGet. Server paketini yükleme](media/Hosting_03-NuGet.Server-Package.png)

1. <span data-ttu-id="af852-123">NuGet. Server yükleme, boş Web uygulamasını bir paket kaynağına dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="af852-123">Installing NuGet.Server converts the empty Web application into a package source.</span></span> <span data-ttu-id="af852-124">Diğer birçok paketi kurar, `Packages` uygulamada bir klasör oluşturur ve `web.config` ek ayarları dahil etmek için değiştirir (Ayrıntılar için bu dosyadaki açıklamalara bakın).</span><span class="sxs-lookup"><span data-stu-id="af852-124">It installs a variety of other packages, creates a `Packages` folder in the application, and modifies `web.config` to include additional settings (see the comments in that file for details).</span></span>

    > [!Important]
    > <span data-ttu-id="af852-125">`web.config`NuGet. Server paketi bu dosyadaki değişikliklerini tamamladıktan sonra dikkatle inceleyin.</span><span class="sxs-lookup"><span data-stu-id="af852-125">Carefully inspect `web.config` after the NuGet.Server package has completed its modifications to that file.</span></span> <span data-ttu-id="af852-126">NuGet. Server varolan öğelerin üzerine yazmayabilir, bunun yerine yinelenen öğeler oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="af852-126">NuGet.Server may not overwrite existing elements but instead create duplicate elements.</span></span> <span data-ttu-id="af852-127">Bu yinelemeler, daha sonra Projeyi çalıştırmaya çalıştığınızda bir "Iç sunucu hatası" oluşmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="af852-127">Those duplicates will cause an "Internal Server Error" when you later try to run the project.</span></span> <span data-ttu-id="af852-128">Örneğin, `web.config` `<compilation debug="true" targetFramework="4.5.2" />` NuGet. Server 'ı yüklemeden önce içeriyorsa, paket onun üzerine yazmaz ancak ikinci bir ekler `<compilation debug="true" targetFramework="4.6" />` .</span><span class="sxs-lookup"><span data-stu-id="af852-128">For example, if your `web.config` contains `<compilation debug="true" targetFramework="4.5.2" />` before installing NuGet.Server, the package doesn't overwrite it but inserts a second `<compilation debug="true" targetFramework="4.6" />`.</span></span> <span data-ttu-id="af852-129">Bu durumda, öğesini eski Framework sürümü ile silin.</span><span class="sxs-lookup"><span data-stu-id="af852-129">In that case, delete the element with the older framework version.</span></span>

1. <span data-ttu-id="af852-130">Siteyi Visual Studio 'da yerel olarak çalıştırın (hata ayıklama **> kullanarak hata ayıklamadan başlayın** veya CTRL + F5).</span><span class="sxs-lookup"><span data-stu-id="af852-130">Run the site locally in Visual Studio (using **Debug > Start Without Debugging** or Ctrl+F5).</span></span> <span data-ttu-id="af852-131">Giriş sayfası, aşağıda gösterildiği gibi paket akışı URL 'Lerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="af852-131">The home page provides the package feed URLs as shown below.</span></span> <span data-ttu-id="af852-132">Hata görürseniz `web.config` daha önce belirtildiği gibi yinelenen öğeleri dikkatle inceleyin.</span><span class="sxs-lookup"><span data-stu-id="af852-132">If you see errors, carefully inspect your `web.config` for duplicate elements as noted earlier.</span></span>

    ![NuGet. Server içeren bir uygulama için varsayılan giriş sayfası](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1.  <span data-ttu-id="af852-134">Uygulamayı ilk kez çalıştırdığınızda NuGet. Server, `Packages` klasörü her bir paket için bir klasör içerecek şekilde yeniden yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="af852-134">The first time you run the application, NuGet.Server restructures the `Packages` folder to contain a folder for each package.</span></span> <span data-ttu-id="af852-135">Bu, performansı artırmak için NuGet 3,3 ile sunulan [yerel depolama düzeniyle](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) eşleşir.</span><span class="sxs-lookup"><span data-stu-id="af852-135">This matches the [local storage layout](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) introduced with NuGet 3.3 to improve performance.</span></span> <span data-ttu-id="af852-136">Daha fazla paket eklerken bu yapıyı izlemeye devam edin.</span><span class="sxs-lookup"><span data-stu-id="af852-136">When adding more packages, continue to follow this structure.</span></span>

1. <span data-ttu-id="af852-137">Yerel dağıtımınızı sınadıktan sonra, gerektiğinde uygulamayı başka bir iç veya dış siteye dağıtın.</span><span class="sxs-lookup"><span data-stu-id="af852-137">Once you've tested your local deployment, deploy the application to any other internal or external site as needed.</span></span>

1. <span data-ttu-id="af852-138">' A dağıtıldıktan sonra `http://<domain>` , paket kaynağı için KULLANDıĞıNıZ URL olur `http://<domain>/nuget` .</span><span class="sxs-lookup"><span data-stu-id="af852-138">Once deployed to `http://<domain>`, the URL that you use for the package source will be `http://<domain>/nuget`.</span></span>

## <a name="adding-packages-to-the-feed-externally"></a><span data-ttu-id="af852-139">Akışa paket dışarıdan ekleniyor</span><span class="sxs-lookup"><span data-stu-id="af852-139">Adding packages to the feed externally</span></span>

<span data-ttu-id="af852-140">NuGet. Server sitesi çalışmaya başladıktan sonra, içinde bir API anahtarı değeri ayarlamanız kaydıyla, [NuGet Push](../reference/cli-reference/cli-ref-push.md) kullanarak paket ekleyebilirsiniz `web.config` .</span><span class="sxs-lookup"><span data-stu-id="af852-140">Once a NuGet.Server site is running, you can add packages using [nuget push](../reference/cli-reference/cli-ref-push.md) provided that you set an API key value in `web.config`.</span></span>

<span data-ttu-id="af852-141">NuGet. Server paketini yükledikten sonra `web.config` boş bir `appSetting/apiKey` değer içerir:</span><span class="sxs-lookup"><span data-stu-id="af852-141">After installing the NuGet.Server package, `web.config` contains an empty `appSetting/apiKey` value:</span></span>

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="af852-142">`apiKey`Atlanırsa veya boş bırakıldığında, paketlerin akışa gönderilmesi devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="af852-142">When `apiKey` is omitted or blank, pushing packages to the feed is disabled.</span></span>

<span data-ttu-id="af852-143">Bu özelliği etkinleştirmek için, `apiKey` değerini bir değere ayarlayın (ideal bir parola) ve şu değere sahip adlı bir anahtar ekleyin `appSettings/requireApiKey` `true` :</span><span class="sxs-lookup"><span data-stu-id="af852-143">To enable this capability, set the `apiKey` to a value (ideally a strong password) and add a key called `appSettings/requireApiKey` with the value of `true`:</span></span>

```xml
<appSettings>
    <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

<span data-ttu-id="af852-144">Sunucunuz zaten güvenli hale getirilse veya başka türlü bir API anahtarı (örneğin, yerel bir ekip ağı üzerinde bir özel sunucu kullanırken) gerektirmiyorsa, `requireApiKey` olarak ayarlayabilirsiniz `false` .</span><span class="sxs-lookup"><span data-stu-id="af852-144">If your server is already secured or you do not otherwise require an API key (for example, when using a private server on a local team network), you can set `requireApiKey` to `false`.</span></span> <span data-ttu-id="af852-145">Sunucuya erişimi olan tüm kullanıcılar daha sonra paketleri gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="af852-145">All users with access to the server can then push packages.</span></span>

<span data-ttu-id="af852-146">NuGet. Server 3.0.0 'den başlayarak, paketlerin gönderilmesi URL 'SI olarak değişir `http://<domain>/nuget` .</span><span class="sxs-lookup"><span data-stu-id="af852-146">Starting with NuGet.Server 3.0.0, the URL for pushing packages was change to `http://<domain>/nuget`.</span></span> <span data-ttu-id="af852-147">3.0.0 sürümünden önce, gönderim URL 'SI idi `http://<domain>/api/v2/package` .</span><span class="sxs-lookup"><span data-stu-id="af852-147">Prior to the 3.0.0 release, the push URL was `http://<domain>/api/v2/package`.</span></span>

<span data-ttu-id="af852-148">NuGet 3.2.1 ve daha yeni bir sürümü ile, bu eski URL, `/api/v2/package` `/nuget` Varsayılan olarak `enableLegacyPushRoute: true` Başlangıç CONFIG ( `NuGetODataConfig.cs` Varsayılan olarak) seçeneği aracılığıyla etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="af852-148">With NuGet 3.2.1 and newer, this legacy URL `/api/v2/package` is enabled in addition to `/nuget` by default via `enableLegacyPushRoute: true` option in your startup config (`NuGetODataConfig.cs` by default).</span></span> <span data-ttu-id="af852-149">Aynı projede birden çok akış barındırıldığı zaman bu özelliğin çalışmadığına unutmayın.</span><span class="sxs-lookup"><span data-stu-id="af852-149">Note that this feature does not work when multiple feeds are hosted in the same project.</span></span>

## <a name="removing-packages-from-the-feed"></a><span data-ttu-id="af852-150">Paketleri akıştan kaldırma</span><span class="sxs-lookup"><span data-stu-id="af852-150">Removing packages from the feed</span></span>

<span data-ttu-id="af852-151">NuGet. Server ile, [NuGet Delete](../reference/cli-reference/cli-ref-delete.md) komutu, açıklama ile API anahtarını dahil etmeniz kaydıyla bir paketi depodan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="af852-151">With NuGet.Server, the [nuget delete](../reference/cli-reference/cli-ref-delete.md) command removes a package from the repository provided that you include the API key with the comment.</span></span>

<span data-ttu-id="af852-152">Bunun yerine paketin listesini kaldırma (paket geri yükleme için kullanılabilir durumda bırakma) davranışını değiştirmek istiyorsanız, `enableDelisting` içindeki anahtarı `web.config` true olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="af852-152">If you want to change the behavior to delist the package instead (leaving it available for package restore), change the `enableDelisting` key in `web.config` to true.</span></span>

## <a name="configuring-the-packages-folder"></a><span data-ttu-id="af852-153">Paketler klasörünü yapılandırma</span><span class="sxs-lookup"><span data-stu-id="af852-153">Configuring the Packages folder</span></span>

<span data-ttu-id="af852-154">`NuGet.Server`1,5 ve sonraki sürümlerde paket klasörünü, `appSettings/packagesPath` içindeki değeri kullanarak özelleştirebilirsiniz `web.config` :</span><span class="sxs-lookup"><span data-stu-id="af852-154">With `NuGet.Server` 1.5 and later, you can customize the package folder using the `appSettings/packagesPath` value in `web.config`:</span></span>

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

<span data-ttu-id="af852-155">`packagesPath` mutlak veya sanal yol olabilir.</span><span class="sxs-lookup"><span data-stu-id="af852-155">`packagesPath` can be an absolute or virtual path.</span></span>

<span data-ttu-id="af852-156">`packagesPath`Atlanırsa veya boş bırakılırsa, paketler klasörü varsayılandır `~/Packages` .</span><span class="sxs-lookup"><span data-stu-id="af852-156">When `packagesPath` is omitted or left blank, the packages folder is the default `~/Packages`.</span></span>

## <a name="making-packages-available-when-you-publish-the-web-app"></a><span data-ttu-id="af852-157">Web uygulamasını yayımladığınızda paketleri kullanılabilir hale getirme</span><span class="sxs-lookup"><span data-stu-id="af852-157">Making packages available when you publish the web app</span></span>

<span data-ttu-id="af852-158">Uygulamayı bir sunucuda yayımladığınızda paketleri akışta kullanılabilir hale getirmek için, her `.nupkg` `Packages` bir dosyayı Visual Studio 'daki klasöre ekleyin, sonra her bir **yapı eylemini** **Içeriğe** ayarlayın ve her **zaman kopyalamak**için **çıkış dizinine kopyalayın** :</span><span class="sxs-lookup"><span data-stu-id="af852-158">To make packages available in the feed when you publish the application to a server, add each `.nupkg` files to the `Packages` folder in Visual Studio, then set each one's **Build Action** to **Content** and **Copy to Output Directory** to **Copy always**:</span></span>

![Paketler projedeki paketler klasörüne kopyalanıyor](media/Hosting_05-NuGet.Server-Package-Folder.png)

## <a name="release-notes"></a><span data-ttu-id="af852-160">Sürüm Notları</span><span class="sxs-lookup"><span data-stu-id="af852-160">Release Notes</span></span>

<span data-ttu-id="af852-161">NuGet [Sürüm sayfasında](https://github.com/NuGet/NuGet.Server/releases)NuGet. Server için sürüm notları bulunur.</span><span class="sxs-lookup"><span data-stu-id="af852-161">Release notes for NuGet.Server are available on the [GitHub release page](https://github.com/NuGet/NuGet.Server/releases).</span></span>
<span data-ttu-id="af852-162">Bu, hata düzeltmeleri ve eklenen yeni özellikler hakkındaki ayrıntıları içerir.</span><span class="sxs-lookup"><span data-stu-id="af852-162">This includes details about bug fixes and new features that are added.</span></span>

## <a name="nugetserver-support"></a><span data-ttu-id="af852-163">NuGet. Server desteği</span><span class="sxs-lookup"><span data-stu-id="af852-163">NuGet.Server support</span></span>

<span data-ttu-id="af852-164">NuGet. Server kullanarak ek yardım için, üzerinde bir sorun oluşturun [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues) .</span><span class="sxs-lookup"><span data-stu-id="af852-164">For additional help using NuGet.Server, create an issue on [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues).</span></span>
