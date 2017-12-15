---
title: "Bir NuGet Paketi Yayımlama | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/5/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 2342aabd-983e-4db1-9230-57c84fa36969
description: "Ayrıntılı yönergeler için NuGet paketi nuget.org veya özel akışları yayımlama ve nuget.org paket sahipliği yönetme."
keywords: "NuGet Paketi Yayımlama NuGet paketi, NuGet paketinin sahipliği yayınlamak için NuGet akışlarını nuget.org, özel yayımlama"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: fab25931165afb65aa3fd09c5bc37492ce814a49
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="publishing-packages"></a><span data-ttu-id="85741-104">Paketleri yayımlama</span><span class="sxs-lookup"><span data-stu-id="85741-104">Publishing packages</span></span>

<span data-ttu-id="85741-105">Bulduktan sonra [bir paket oluşturuldu](../create-packages/creating-a-package.md) ile `nuget pack`, diğer geliştiriciler için genel veya özel olarak kullanılabilmesi için basit bir işlemdir:</span><span class="sxs-lookup"><span data-stu-id="85741-105">Once you have [created a package](../create-packages/creating-a-package.md) with `nuget pack`, it's a simple process to make it available to other developers, either publicly or privately:</span></span>

- <span data-ttu-id="85741-106">Ortak paketleri kullanılabilir hale getirilir tüm geliştiriciler için genel ile [nuget.org](https://www.nuget.org/packages/manage/upload) Bu konu başlığı altında açıklandığı gibi.</span><span class="sxs-lookup"><span data-stu-id="85741-106">Public packages are made available to all developers globally through [nuget.org](https://www.nuget.org/packages/manage/upload) as described in this topic.</span></span>
- <span data-ttu-id="85741-107">Özel paketler yalnızca bir ekip veya kuruluş, kullanılabilir ya da bir dosya paylaşımı, özel bir NuGet sunucu barındırarak [Visual Studio Team Services paket Yönetimi](https://www.visualstudio.com/docs/package/nuget/publish), veya bir üçüncü taraf deposu myget, ProGet, Nexus gibi Depo ve Artifactory.</span><span class="sxs-lookup"><span data-stu-id="85741-107">Private packages are available to only a team or organization, by hosting them either a file share, a private NuGet server, [Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish), or a third-party repository such as myget, ProGet, Nexus Repository, and Artifactory.</span></span> <span data-ttu-id="85741-108">Daha fazla bilgi için bkz: [barındırma paketleri genel bakış](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="85741-108">For additional details, see [Hosting Packages Overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="85741-109">Bu konu, nuget.org yayımlamayı kapsar; Visual Studio Team Services yayımlama için bkz: [paket Yönetimi](https://www.visualstudio.com/docs/package/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="85741-109">This topic covers publishing to nuget.org; for publishing to Visual Studio Team Services, see [Package Management](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

## <a name="publish-to-nugetorg"></a><span data-ttu-id="85741-110">Nuget.org için yayımlama</span><span class="sxs-lookup"><span data-stu-id="85741-110">Publish to nuget.org</span></span>

<span data-ttu-id="85741-111">Nuget.org için öncelikle [ücretsiz bir hesap için kayıt](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) veya zaten kayıtlı oturum açma:</span><span class="sxs-lookup"><span data-stu-id="85741-111">For nuget.org, you must first [register for a free account](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) or sign in if already registered:</span></span>

![NuGet kayıt ve oturum açın. konumda](media/publish_NuGetSignIn.png)

<span data-ttu-id="85741-113">Ardından, paketi nuget.org web Portalı aracılığıyla karşıya yükleme, komut satırından nuget.org için anında veya Visual Studio Team Services aracılığıyla CI/CD işleminin parçası olarak aşağıdaki bölümlerde açıklandığı gibi yayımlama.</span><span class="sxs-lookup"><span data-stu-id="85741-113">Next, you can either upload the package through the nuget.org web portal, push to nuget.org from the command line, or publish as part of a CI/CD process through Visual Studio Team Services, as described in the following sections.</span></span>

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a><span data-ttu-id="85741-114">Web portalı: nuget.org üzerinde karşıya yükleme paketini sekmesini kullanın:</span><span class="sxs-lookup"><span data-stu-id="85741-114">Web portal: use the Upload Package tab on nuget.org:</span></span>

![Bir paketi ile NuGet Paket Yöneticisi'ni yükleme](media/publish_UploadYourPackage.PNG)

### <a name="command-line"></a><span data-ttu-id="85741-116">Komut satırı:</span><span class="sxs-lookup"><span data-stu-id="85741-116">Command line:</span></span>
> [!Important]
> <span data-ttu-id="85741-117">Anında iletme paketlere kullanmalısınız nuget.org için [nuget.exe v4.1.0 veya yukarıdaki](https://www.nuget.org/downloads), gerekli uygulayan [NuGet protokolleri](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="85741-117">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="85741-118">Hesap ayarlarınızı gitmek için kullanıcı adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="85741-118">Click on your user name to navigate to your account settings.</span></span>
2. <span data-ttu-id="85741-119">Altında **API anahtarı**, tıklatın **Panoya Kopyala** erişim almak için anahtar CLI sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="85741-119">Under **API Key**, click **copy to clipboard** to retrieve the access key you'll need in the CLI:</span></span>

    ![Hesap ayarlarından bir API anahtarını kopyalama](media/publish_APIKey.png)

3. <span data-ttu-id="85741-121">Bir komut isteminde aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="85741-121">At a command prompt, run the following command:</span></span>

    ```
    nuget setApiKey Your-API-Key
    ```

    <span data-ttu-id="85741-122">Bu adım aynı makinede yapmak böylece bu makinede API anahtarınıza depolar.</span><span class="sxs-lookup"><span data-stu-id="85741-122">This stores your API key on the machine so that you need not do this step again on the same machine.</span></span>

4. <span data-ttu-id="85741-123">Paketinizi NuGet galerisinde komutu kullanarak gönderin:</span><span class="sxs-lookup"><span data-stu-id="85741-123">Push your package to NuGet Gallery using the command:</span></span>

    ```
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

5. <span data-ttu-id="85741-124">Ortak yapılan önce tüm paketler için nuget.org karşıya virüs taraması ve herhangi bir virüs bulunursa reddetti.</span><span class="sxs-lookup"><span data-stu-id="85741-124">Before being made public, all packages uploaded to nuget.org are scanned for viruses and rejected if any viruses are found.</span></span> <span data-ttu-id="85741-125">Nuget.org üzerinde listelenen tüm paketler de düzenli aralıklarla taranır.</span><span class="sxs-lookup"><span data-stu-id="85741-125">All packages listed on nuget.org are also scanned periodically.</span></span>

6. <span data-ttu-id="85741-126">Nuget.org üzerinde hesabınızı, tıklatın **my paketlerini yönetme** yeni bir görmek için yayımlanan; bir onay e-posta iletisi alacaksınız.</span><span class="sxs-lookup"><span data-stu-id="85741-126">In your account on nuget.org, click **Manage my packages** to see the one that you just published; you'll also receive a confirmation email.</span></span> <span data-ttu-id="85741-127">Dizine ve diğerleri, hangi sırada paket sayfanızda şu iletiyi görürsünüz bulabileceğiniz bir yerde arama sonuçlarında görüntülenmesini paketinizi biraz sürebilir dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="85741-127">Note that it might take a while for your package to be indexed and appear in search results where others can find it, during which time you'll see the following message on your package page:</span></span>

    ![Bir paket henüz dizine belirten iletisi](media/publish_NotYetIndexed.png)

### <a name="package-validation-and-indexing"></a><span data-ttu-id="85741-129">Paket doğrulama ve dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="85741-129">Package Validation and Indexing</span></span>

<span data-ttu-id="85741-130">NuGet.org için gönderilen paketleri birkaç doğrulamaları geçer.</span><span class="sxs-lookup"><span data-stu-id="85741-130">Packages pushed to NuGet.org undergo several validations.</span></span> <span data-ttu-id="85741-131">Paketin tüm doğrulama denetimlerini geçtiğinde, sıralanması ve arama sonuçlarında görüntülenmesini biraz sürebilir.</span><span class="sxs-lookup"><span data-stu-id="85741-131">When the package has passed all validation checks, it might take a while for it to be indexed and appear in search results.</span></span> <span data-ttu-id="85741-132">Dizin oluşturma işlemi tamamlandıktan sonra paketi başarıyla yayımlandı onaylayan bir e-posta alırsınız.</span><span class="sxs-lookup"><span data-stu-id="85741-132">Once indexing is complete, you'll receive an email confirming that the package was successfully published.</span></span> <span data-ttu-id="85741-133">Paket doğrulama denetimi başarısız olursa, ilgili hatayı görüntülemek için Paket ayrıntılarını sayfa güncelleştirilir ve hakkında bildiren bir e-posta iletisi alacaksınız.</span><span class="sxs-lookup"><span data-stu-id="85741-133">If the package fails a validation check, the package details page will update to display the associated error and you'll also receive an email notifying you about it.</span></span>

<span data-ttu-id="85741-134">Paket doğrulama ve dizin oluşturma altında 15 dakika genellikle alır.</span><span class="sxs-lookup"><span data-stu-id="85741-134">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="85741-135">Paket yayımlama beklenenden daha uzun sürüyorsa, ziyaret [status.nuget.org](https://status.nuget.org/) NuGet.org tüm kesintileri yaşayan varsa denetlemek için.</span><span class="sxs-lookup"><span data-stu-id="85741-135">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if NuGet.org is experiencing any interruptions.</span></span> <span data-ttu-id="85741-136">Tüm sistemler işletimsel ve paket bir saat içinde başarıyla yayımlanmadı, lütfen NuGet.org oturum açın ve paket sayfasında kişi destek bağlantısı kullanarak bizimle bağlantı kurun.</span><span class="sxs-lookup"><span data-stu-id="85741-136">If all systems are operational and the package hasn't been successfully published within an hour, please login to NuGet.org and contact us using the Contact Support link on the package page.</span></span>

### <a name="visual-studio-team-services-cicd"></a><span data-ttu-id="85741-137">Visual Studio Team Services (CI/CD)</span><span class="sxs-lookup"><span data-stu-id="85741-137">Visual Studio Team Services (CI/CD)</span></span>

<span data-ttu-id="85741-138">Visual Studio Team Services sürekli tümleştirme/dağıtım işleminin bir parçası kullanarak nuget.org paketleri iletin nuget.exe 4.1 kullanmanız gerekir ya da yukarıdaki NuGet görevler.</span><span class="sxs-lookup"><span data-stu-id="85741-138">If you push packages to nuget.org using Visual Studio Team Services as part of your Continuous Integration/Deployment process, you must use nuget.exe 4.1 or above in the NuGet tasks.</span></span> <span data-ttu-id="85741-139">Ayrıntılar bulunabilir [yapı içinde son NuGet kullanarak](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blogu).</span><span class="sxs-lookup"><span data-stu-id="85741-139">Details can be found on [Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blog).</span></span>

## <a name="managing-package-owners-on-nugetorg"></a><span data-ttu-id="85741-140">Nuget.org üzerinde paket sahiplerini yönetme</span><span class="sxs-lookup"><span data-stu-id="85741-140">Managing package owners on nuget.org</span></span>

<span data-ttu-id="85741-141">Ancak her NuGet paketin `.nuspec` dosyası paketin yazarlar tanımlar, nuget.org galeri meta verilerin sahipliği tanımlamak için kullanmaz.</span><span class="sxs-lookup"><span data-stu-id="85741-141">Although each NuGet package's `.nuspec` file defines the package's authors, the nuget.org gallery does not use that metadata to define ownership.</span></span> <span data-ttu-id="85741-142">Bunun yerine, nuget.org ilk sahipliği paketi yayımlar kişiye atar.</span><span class="sxs-lookup"><span data-stu-id="85741-142">Instead, nuget.org assigns initial ownership to the person who publishes the package.</span></span> <span data-ttu-id="85741-143">Bu paket nuget.org kullanıcı Arabirimi aracılığıyla karşıya oturum açan kullanıcının ya da, API anahtarı ile kullanıldı kullanıcılar olan `nuget SetApiKey` veya `nuget push`.</span><span class="sxs-lookup"><span data-stu-id="85741-143">This is either the logged-in user who uploaded the package through the nuget.org UI, or the users whose API key was used with `nuget SetApiKey` or `nuget push`.</span></span>

<span data-ttu-id="85741-144">Tüm paket sahipleri paket ekleme ve kaldırma diğer sahipleri ve güncelleştirmeleri yayımlama da dahil olmak üzere, tam izinlere sahip.</span><span class="sxs-lookup"><span data-stu-id="85741-144">All package owners have full permissions for the package, including adding and removing other owners, and publishing updates.</span></span>

<span data-ttu-id="85741-145">Bir paket sahipliğini değiştirmek için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="85741-145">To change ownership of a package, do the following:</span></span>

1. <span data-ttu-id="85741-146">Nuget.org paketinin geçerli sahibi olan hesap ile oturum açın.</span><span class="sxs-lookup"><span data-stu-id="85741-146">Sign in to nuget.org with the account that is the current owner of the package.</span></span>
1. <span data-ttu-id="85741-147">Tıklayarak kullanıcı adınıza, ardından **my paketlerini yönetme**, yönetmek istediğiniz paketi sonra.</span><span class="sxs-lookup"><span data-stu-id="85741-147">Click on your username, then on **Manage my packages**, then on the package you want to manage.</span></span>
1. <span data-ttu-id="85741-148">Tıklatın **sahiplerini yönetme** sol tarafındaki bağlantı.</span><span class="sxs-lookup"><span data-stu-id="85741-148">Click the **Manage owners** link on the left side.</span></span>

<span data-ttu-id="85741-149">Buradan, birkaç seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="85741-149">From here you have several options:</span></span>

1. <span data-ttu-id="85741-150">Bir sahip eklemek, kendi NuGet hesabı adı girin ve **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="85741-150">To add an owner, enter their NuGet account name and click **Add**.</span></span> <span data-ttu-id="85741-151">Bu onay bağlantısı ile yeni ortak sahibi için bir e-posta gönderir.</span><span class="sxs-lookup"><span data-stu-id="85741-151">This sends an email to that new co-owner with a confirmation link.</span></span> <span data-ttu-id="85741-152">Onaylandıktan sonra o kişiyi eklemek ve sahipleri kaldırmak için tam izinleri vardır.</span><span class="sxs-lookup"><span data-stu-id="85741-152">Once confirmed, that person has full permissions to add and remove owners.</span></span> <span data-ttu-id="85741-153">(Onaylandı kadar **sahiplerini yönetme** sayfası, bu kişi için "onay bekliyor" gösterir).</span><span class="sxs-lookup"><span data-stu-id="85741-153">(Until confirmed, the **Manage owners** page indicates "pending approval" for that person).</span></span>
1. <span data-ttu-id="85741-154">Bir sahip kaldırmak için kullanıcıların adı seçin **sahiplerini yönetme** tıklatıp **kaldırmak**.</span><span class="sxs-lookup"><span data-stu-id="85741-154">To remove an owner, select their name on the **Manage owners** and click **Remove**.</span></span>
1. <span data-ttu-id="85741-155">(Olarak ne zaman sahipliği değişiklikleri veya bir paket yanlış hesabı altında yayımlandı), sahipliği yalnızca aktarmak için yeni sahibin ekleyin ve sahipliği onaylanıp sonra bunlar, listeden kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85741-155">To transfer ownership (as when ownership changes or a package was published under the wrong account), simply add the new owner, and once they've confirmed ownership they can remove you from the list.</span></span>

<span data-ttu-id="85741-156">Bir şirket veya grup sahipliği atamak için uygun ekip üyelerine iletilen bir e-posta diğer adı kullanarak bir nuget.org hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="85741-156">To assign ownership to a company or group, create a nuget.org account using an email alias that is forwarded to the appropriate team members.</span></span> <span data-ttu-id="85741-157">Örneğin, çeşitli Microsoft ASP.NET paketleri birlikte sahibi [microsoft](http://nuget.org/profiles/microsoft) ve [aspnet](http://nuget.org/profiles/aspnet) hesapları, hangi yalnızca gibi diğer adları.</span><span class="sxs-lookup"><span data-stu-id="85741-157">For example, various Microsoft ASP.NET packages are co-owned by the [microsoft](http://nuget.org/profiles/microsoft) and [aspnet](http://nuget.org/profiles/aspnet) accounts, which simply such aliases.</span></span>

### <a name="recovering-package-ownership"></a><span data-ttu-id="85741-158">Paket sahipliği kurtarma</span><span class="sxs-lookup"><span data-stu-id="85741-158">Recovering package ownership</span></span>

<span data-ttu-id="85741-159">Bazen, bir paket etkin bir sahip olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="85741-159">Occasionally, a package may not have an active owner.</span></span> <span data-ttu-id="85741-160">Örneğin, özgün sahibinin paket üreten şirket bıraktıysanız, nuget.org kimlik bilgileri kaybolur veya galerisinde önceki hataların bir paket ownerless sol.</span><span class="sxs-lookup"><span data-stu-id="85741-160">For example, the original owner may have left the company that produces the package, nuget.org credentials are lost, or earlier bugs in the gallery left a package ownerless.</span></span>

<span data-ttu-id="85741-161">Bir paketin gerçek sahibiyseniz ve sahipliği kazanmaya ihtiyacınız varsa kullanmak [kişi formu](https://www.nuget.org/policies/Contact) açıklayan NuGet takım durumunuza nuget.org üzerinde.</span><span class="sxs-lookup"><span data-stu-id="85741-161">If you are the rightful owner of a package and need to regain ownership, use the [contact form](https://www.nuget.org/policies/Contact) on nuget.org to explain your situation to the NuGet team.</span></span> <span data-ttu-id="85741-162">Biz sonra varolan sahibi paketin proje URL'sini, Twitter, e-posta veya başka yöntemler aracılığıyla bulmaya çalışan dahil olmak üzere paketin, sahipliği doğrulamak için bir işlemi izleyin.</span><span class="sxs-lookup"><span data-stu-id="85741-162">We then follow a process to verify your ownership of the package, including trying to locate the existing owner through the package's Project URL, Twitter, email, or other means.</span></span> <span data-ttu-id="85741-163">Ancak tüm yöntemler başarısız olursa, sahibi olmak için yeni bir davet gönderebiliriz.</span><span class="sxs-lookup"><span data-stu-id="85741-163">But if all else fails, we can send you a new invite to become an owner.</span></span>
