---
title: Bir NuGet Paketi Yayımlama
description: Nuget.org veya özel akışları için bir NuGet Paketi Yayımlama ve nuget.org üzerinde paket sahipliği yönetme konusunda ayrıntılı yönergeler.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/18/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: eb45ac1574efc79873d2d372f122a3d756e90ee5
ms.sourcegitcommit: 6cffa6ef59b922df2d87aa9c24034d00542983cd
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/10/2018
ms.locfileid: "37963122"
---
# <a name="publishing-packages"></a><span data-ttu-id="70a5d-103">Paket yayımlama</span><span class="sxs-lookup"><span data-stu-id="70a5d-103">Publishing packages</span></span>

<span data-ttu-id="70a5d-104">Bir paket oluşturup sahip, `.nupkg` ele dosya, diğer geliştiriciler için genel veya özel olarak kullanılabilmesi için basit bir işlemdir:</span><span class="sxs-lookup"><span data-stu-id="70a5d-104">Once you have created a package and have your `.nupkg` file in hand, it's a simple process to make it available to other developers, either publicly or privately:</span></span>

- <span data-ttu-id="70a5d-105">Genel paketleri kullanılabilir hale gelir tüm geliştiricilere genel ile [nuget.org](https://www.nuget.org/packages/manage/upload) (NuGet 4.1.0+ gerektirir) Bu makalede açıklandığı gibi.</span><span class="sxs-lookup"><span data-stu-id="70a5d-105">Public packages are made available to all developers globally through [nuget.org](https://www.nuget.org/packages/manage/upload) as described in this article (requires NuGet 4.1.0+).</span></span>
- <span data-ttu-id="70a5d-106">Özel paketler yalnızca bir ekip veya kuruluşlar için kullanılabilir ya da dosya paylaşımı için bir özel NuGet sunucusu barındırarak [Visual Studio Team Services paket Yönetimi](https://www.visualstudio.com/docs/package/nuget/publish), veya myget, ProGet, Nexus gibi bir üçüncü taraf depo Depo ve Artifactory.</span><span class="sxs-lookup"><span data-stu-id="70a5d-106">Private packages are available to only a team or organization, by hosting them either a file share, a private NuGet server, [Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish), or a third-party repository such as myget, ProGet, Nexus Repository, and Artifactory.</span></span> <span data-ttu-id="70a5d-107">Ek ayrıntılar için bkz. [barındırma paketleri genel bakış](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="70a5d-107">For additional details, see [Hosting Packages Overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="70a5d-108">Bu makalede nuget.org yayımlama kapsar; Visual Studio Team Services yayımlama için bkz: [paket Yönetimi](https://www.visualstudio.com/docs/package/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="70a5d-108">This article covers publishing to nuget.org; for publishing to Visual Studio Team Services, see [Package Management](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

## <a name="publish-to-nugetorg"></a><span data-ttu-id="70a5d-109">Nuget.org için yayımlama</span><span class="sxs-lookup"><span data-stu-id="70a5d-109">Publish to nuget.org</span></span>

<span data-ttu-id="70a5d-110">Nuget.org için birlikte, hesap nuget.org ile kaydetmek için istenir, bir Microsoft hesabıyla oturum açmanız gerekir. Ayrıca portalı eski sürümleri kullanılarak oluşturulan bir nuget.org hesabıyla kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="70a5d-110">For nuget.org, you must sign in with a Microsoft account, with which you'll be asked to register the account with nuget.org. You can also sign in with a nuget.org account created using older versions of the portal.</span></span>

![NuGet oturum konumda](media/publish_NuGetSignIn.png)

<span data-ttu-id="70a5d-112">Ardından, ya da nuget.org web Portalı aracılığıyla paketini karşıya yükleyin, komut satırından nuget.org için anında iletme (gerektirir `nuget.exe` 4.1.0+), veya Visual Studio Team Services ile CI/CD işleminin bir parçası olarak aşağıdaki bölümlerde açıklandığı şekilde yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="70a5d-112">Next, you can either upload the package through the nuget.org web portal, push to nuget.org from the command line (requires `nuget.exe` 4.1.0+) , or publish as part of a CI/CD process through Visual Studio Team Services, as described in the following sections.</span></span>

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a><span data-ttu-id="70a5d-113">Web portalı: Paket karşıya sekmesinde nuget.org adresinden kullanın</span><span class="sxs-lookup"><span data-stu-id="70a5d-113">Web portal: use the Upload Package tab on nuget.org</span></span>

1. <span data-ttu-id="70a5d-114">Seçin **karşıya** en üstteki menüde nuget.org ve paket konumuna göz atın.</span><span class="sxs-lookup"><span data-stu-id="70a5d-114">Select **Upload** on the top menu of nuget.org and browse to the package location.</span></span>

    ![Nuget.org üzerindeki bir paket karşıya yükleme](media/publish_UploadYourPackage.PNG)

1. <span data-ttu-id="70a5d-116">nuget.org paket adı kullanılabilir olup olmadığını söyler.</span><span class="sxs-lookup"><span data-stu-id="70a5d-116">nuget.org tells you if the package name is available.</span></span> <span data-ttu-id="70a5d-117">Değilse değiştirirseniz, projenizdeki paket tanımlayıcısı yeniden oluşturun ve karşıya yüklemeyi yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="70a5d-117">If it isn't, change the package identifier in your project, rebuild, and try the upload again.</span></span>

1. <span data-ttu-id="70a5d-118">Paket adı varsa, nuget.org açılır bir **doğrulama** içinde gözden geçirebileceğiniz paket bildirimi meta verileri bölümü.</span><span class="sxs-lookup"><span data-stu-id="70a5d-118">If the package name is available, nuget.org opens a **Verify** section in which you can review the metadata from the package manifest.</span></span> <span data-ttu-id="70a5d-119">Meta verileri değiştirmek için projenizi Düzenle (proje dosyası veya `.nuspec` dosyası), yeniden, paketi yeniden oluşturun ve yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="70a5d-119">To change any of the metadata, edit your project (project file or `.nuspec` file), rebuild, recreate the package, and upload again.</span></span>

1. <span data-ttu-id="70a5d-120">Altında **alma belgeleri** Markdown yapıştırın, bir URL ile belgelerinizi noktasına veya belgeleri dosyasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="70a5d-120">Under **Import Documentation** you can paste Markdown, point to your docs with a URL, or upload a documentation file.</span></span>

1. <span data-ttu-id="70a5d-121">Tüm bilgileri hazır olduğunda seçin **Gönder** düğmesi</span><span class="sxs-lookup"><span data-stu-id="70a5d-121">When all the information is ready, select the **Submit** button</span></span>

### <a name="command-line"></a><span data-ttu-id="70a5d-122">Komut satırı</span><span class="sxs-lookup"><span data-stu-id="70a5d-122">Command line</span></span>

<span data-ttu-id="70a5d-123">Anında iletme paketlerine nuget.org'da kullanmalısınız [nuget.exe verze 4.1.0 veya üzeri](https://www.nuget.org/downloads), gerekli uygulayan [NuGet protokolleri](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="70a5d-123">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span> <span data-ttu-id="70a5d-124">Nuget.org üzerinde oluşturulan bir API anahtarı da gerekir.</span><span class="sxs-lookup"><span data-stu-id="70a5d-124">You also need an API key, which is created on nuget.org.</span></span>

#### <a name="create-api-keys"></a><span data-ttu-id="70a5d-125">API anahtarları oluşturma</span><span class="sxs-lookup"><span data-stu-id="70a5d-125">Create API keys</span></span>

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="70a5d-126">DotNet nuget itme ile yayımlama</span><span class="sxs-lookup"><span data-stu-id="70a5d-126">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a><span data-ttu-id="70a5d-127">Nuget itme ile yayımlama</span><span class="sxs-lookup"><span data-stu-id="70a5d-127">Publish with nuget push</span></span>

1. <span data-ttu-id="70a5d-128">Bir komut isteminde aşağıdaki komutu çalıştırın. komut, değiştirme `<your_API_key>` nuget.org adresinden aldığınız anahtarını ile:</span><span class="sxs-lookup"><span data-stu-id="70a5d-128">At a command prompt, run the following command, replacing `<your_API_key>` with the key obtained from nuget.org:</span></span>

    ```cli
    nuget setApiKey <your_API_key>
    ```

    <span data-ttu-id="70a5d-129">Bu komut, API anahtarınızı NuGet yapılandırmanızda saklar, böylece aynı bilgisayarda bu adımı yinelemeniz.</span><span class="sxs-lookup"><span data-stu-id="70a5d-129">This command stores your API key in your NuGet configuration so that you need repeat this step again on the same computer.</span></span>

1. <span data-ttu-id="70a5d-130">Paketiniz, aşağıdaki komutu kullanarak NuGet Galerisine gönderin:</span><span class="sxs-lookup"><span data-stu-id="70a5d-130">Push your package to NuGet Gallery using the following command:</span></span>

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

#### <a name="publish-signed-packages"></a><span data-ttu-id="70a5d-131">İmzalanmış paketleri yayımlama</span><span class="sxs-lookup"><span data-stu-id="70a5d-131">Publish signed packages</span></span>

<span data-ttu-id="70a5d-132">İmzalanmış paketleri göndermek için önce [sertifika kaydettirir](../reference/Signed-Packages-Reference.md#register-certificate-on-nugetorg) paketleri imzalamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="70a5d-132">To submit signed packages, you must first [register the certificate](../reference/Signed-Packages-Reference.md#register-certificate-on-nugetorg) used for signing the packages.</span></span> 

> [!Warning]
> <span data-ttu-id="70a5d-133">nuget.org reddeder karşılamayan paketleri [paket gereksinimleri imzalı](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="70a5d-133">nuget.org rejects packages that don't satisfy the [signed package requirements](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg).</span></span>

### <a name="package-validation-and-indexing"></a><span data-ttu-id="70a5d-134">Paket doğrulaması ve dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="70a5d-134">Package validation and indexing</span></span>

<span data-ttu-id="70a5d-135">Nuget.org için gönderilen paketleri virüs denetimleri gibi çeşitli doğrulamaları geçeriz.</span><span class="sxs-lookup"><span data-stu-id="70a5d-135">Packages pushed to nuget.org undergo several validations, such as virus checks.</span></span> <span data-ttu-id="70a5d-136">(Tüm paketleri nuget.org üzerinde düzenli aralıklarla taranır.)</span><span class="sxs-lookup"><span data-stu-id="70a5d-136">(All packages on nuget.org are periodically scanned.)</span></span>

<span data-ttu-id="70a5d-137">biçimindeki telefon numarasıdır.</span><span class="sxs-lookup"><span data-stu-id="70a5d-137">.</span></span> <span data-ttu-id="70a5d-138">Paket tüm doğrulama denetimlerini geçtiğinde, sıralanması ve arama sonuçlarında görüntülenmesi için biraz sürebilir.</span><span class="sxs-lookup"><span data-stu-id="70a5d-138">When the package has passed all validation checks, it might take a while for it to be indexed and appear in search results.</span></span> <span data-ttu-id="70a5d-139">Dizin oluşturma tamamlandıktan sonra paketi başarıyla yayımlandı onaylayan bir e-posta alırsınız.</span><span class="sxs-lookup"><span data-stu-id="70a5d-139">Once indexing is complete, you receive an email confirming that the package was successfully published.</span></span> <span data-ttu-id="70a5d-140">Paket doğrulama denetimi başarısız olursa, Paket Ayrıntıları sayfasına ilgili hatayı görüntülemek için güncelleştirir ve aynı zamanda bunu bildiren bir e-posta alırsınız.</span><span class="sxs-lookup"><span data-stu-id="70a5d-140">If the package fails a validation check, the package details page will update to display the associated error and you also receive an email notifying you about it.</span></span>

<span data-ttu-id="70a5d-141">Paket doğrulaması ve dizin oluşturma genellikle 15 dakika alır.</span><span class="sxs-lookup"><span data-stu-id="70a5d-141">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="70a5d-142">Paket yayımlama beklenenden daha uzun sürerse ziyaret [status.nuget.org](https://status.nuget.org/) nuget.org herhangi bir kesinti yaşıyor olmadığını denetlemek için.</span><span class="sxs-lookup"><span data-stu-id="70a5d-142">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if nuget.org is experiencing any interruptions.</span></span> <span data-ttu-id="70a5d-143">Tüm sistemler çalışır durumda ve paket başarıyla bir saat içinde yayımlanmadı Lütfen nuget.org için oturum açın ve paket sayfasında kişi destek bağlantısı kullanarak bize ulaşın.</span><span class="sxs-lookup"><span data-stu-id="70a5d-143">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package page.</span></span>

<span data-ttu-id="70a5d-144">Paketin durumunu görmek için seçin **paketleri yönetme** nuget.org hesap adınızın altında. Doğrulama tamamlandığında bir onay e-posta alırsınız.</span><span class="sxs-lookup"><span data-stu-id="70a5d-144">To see the status of a package, select **Manage packages** under your account name on nuget.org. You receive a confirmation email when validation is complete.</span></span>

<span data-ttu-id="70a5d-145">Dizine ve başkalarının hangi sırada paket sayfanızda aşağıdaki iletiyi görürsünüz, nerede bulabileceğiniz arama sonuçlarında görünmesini paketinizi biraz sürebilir dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="70a5d-145">Note that it might take a while for your package to be indexed and appear in search results where others can find it, during which time you see the following message on your package page:</span></span>

![Bir paket henüz yayımlanmadı belirten ileti.](media/publish_NotYetIndexed.png)

### <a name="visual-studio-team-services-cicd"></a><span data-ttu-id="70a5d-147">Visual Studio Team Services (CI/CD)</span><span class="sxs-lookup"><span data-stu-id="70a5d-147">Visual Studio Team Services (CI/CD)</span></span>

<span data-ttu-id="70a5d-148">Paketleri nuget.org Visual Studio Team Services kullanarak sürekli tümleştirme/dağıtım işleminizin bir parçası olarak gönderirseniz kullanmalısınız `nuget.exe` 4.1 veya üzerini NuGet görevler.</span><span class="sxs-lookup"><span data-stu-id="70a5d-148">If you push packages to nuget.org using Visual Studio Team Services as part of your Continuous Integration/Deployment process, you must use `nuget.exe` 4.1 or above in the NuGet tasks.</span></span> <span data-ttu-id="70a5d-149">Ayrıntıları bulunabilir [derlemenizde en son NuGet kullanarak](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blogu).</span><span class="sxs-lookup"><span data-stu-id="70a5d-149">Details can be found on [Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blog).</span></span>

## <a name="managing-package-owners-on-nugetorg"></a><span data-ttu-id="70a5d-150">Nuget.org paketinin sahiplerini yönetme</span><span class="sxs-lookup"><span data-stu-id="70a5d-150">Managing package owners on nuget.org</span></span>

<span data-ttu-id="70a5d-151">Ancak her NuGet paketi `.nuspec` dosyası tanımlar paketin yazarlar, nuget.org galeri meta verilerin sahipliği tanımlamak için kullanmaz.</span><span class="sxs-lookup"><span data-stu-id="70a5d-151">Although each NuGet package's `.nuspec` file defines the package's authors, the nuget.org gallery does not use that metadata to define ownership.</span></span> <span data-ttu-id="70a5d-152">Bunun yerine, nuget.org ilk sahipliği paketi yayımlar kişiye atar.</span><span class="sxs-lookup"><span data-stu-id="70a5d-152">Instead, nuget.org assigns initial ownership to the person who publishes the package.</span></span> <span data-ttu-id="70a5d-153">Paket nuget.org kullanıcı Arabirimi aracılığıyla karşıya oturum açmış kullanıcı veya API anahtarı ile kullanıldı kullanıcılar budur `nuget SetApiKey` veya `nuget push`.</span><span class="sxs-lookup"><span data-stu-id="70a5d-153">This is either the logged-in user who uploaded the package through the nuget.org UI, or the users whose API key was used with `nuget SetApiKey` or `nuget push`.</span></span>

<span data-ttu-id="70a5d-154">Tüm paket sahipleri ekleme ve diğer sahipleri kaldırmak ve güncelleştirmelerini yayımlama da dahil olmak üzere paket için tam izinleri vardır.</span><span class="sxs-lookup"><span data-stu-id="70a5d-154">All package owners have full permissions for the package, including adding and removing other owners, and publishing updates.</span></span>

<span data-ttu-id="70a5d-155">Bir paket sahipliğini değiştirmek için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="70a5d-155">To change ownership of a package, do the following:</span></span>

1. <span data-ttu-id="70a5d-156">Nuget.org paketinin geçerli sahibi olan hesapla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="70a5d-156">Sign in to nuget.org with the account that is the current owner of the package.</span></span>
1. <span data-ttu-id="70a5d-157">Hesabınızın adını seçin, **paketleri yönetme**, genişletin **yayımlanmış paketleri**.</span><span class="sxs-lookup"><span data-stu-id="70a5d-157">Select your account name, select **Manage packages**, and expand **Published Packages**.</span></span>
1. <span data-ttu-id="70a5d-158">Yönetmek istediğiniz paketi seçin, sonra da sağ tarafta **sahiplerini yönetme**.</span><span class="sxs-lookup"><span data-stu-id="70a5d-158">Select on the package you want to manage, then on the right side select **Manage owners**.</span></span>

<span data-ttu-id="70a5d-159">Burada birkaç seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="70a5d-159">From here you have several options:</span></span>

1. <span data-ttu-id="70a5d-160">Altında listelenen herhangi bir sahibi kaldırma **geçerli sahipleri**.</span><span class="sxs-lookup"><span data-stu-id="70a5d-160">Remove any owner listed under **Current Owners**.</span></span>
1. <span data-ttu-id="70a5d-161">Altında bir sahip ekleme **ekleme sahibi** kullanıcıların kullanıcı adı, bir ileti girme ve seçerek **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="70a5d-161">Add an owner under **Add Owner** by entering their user name, a message, and selecting **Add**.</span></span> <span data-ttu-id="70a5d-162">Bu eylem, yeni ikincil sahip onayı bağlantısını içeren bir e-posta gönderir.</span><span class="sxs-lookup"><span data-stu-id="70a5d-162">This action sends an email to that new co-owner with a confirmation link.</span></span> <span data-ttu-id="70a5d-163">Onaylandıktan sonra söz konusu kişinin eklemek ve sahipleri kaldırmak için tam izinlere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="70a5d-163">Once confirmed, that person has full permissions to add and remove owners.</span></span> <span data-ttu-id="70a5d-164">(Onaylanana kadar **geçerli sahipleri** o kişinin onay bekleyen bölümü gösterir.)</span><span class="sxs-lookup"><span data-stu-id="70a5d-164">(Until confirmed, the **Current Owners** section indicates pending approval for that person.)</span></span>
1. <span data-ttu-id="70a5d-165">(Zaman sahipliği değişiklikleri veya bir paket yanlış hesap altında yayımlanan) olarak sahipliğini devretmek için yeni sahibin ekleyin ve bunlar sahipliği onayladıktan sonra bunlar, listeden kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="70a5d-165">To transfer ownership (as when ownership changes or a package was published under the wrong account), add the new owner, and once they've confirmed ownership they can remove you from the list.</span></span>

<span data-ttu-id="70a5d-166">Sahipliği bir şirket veya grup için atama için uygun takım üyelerine iletilen e-posta diğer adı kullanarak nuget.org hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="70a5d-166">To assign ownership to a company or group, create a nuget.org account using an email alias that is forwarded to the appropriate team members.</span></span> <span data-ttu-id="70a5d-167">Örneğin, çeşitli Microsoft ASP.NET paketler ortak sahibi [microsoft](http://nuget.org/profiles/microsoft) ve [aspnet](http://nuget.org/profiles/aspnet) hesapları, yalnızca tür diğer adları.</span><span class="sxs-lookup"><span data-stu-id="70a5d-167">For example, various Microsoft ASP.NET packages are co-owned by the [microsoft](http://nuget.org/profiles/microsoft) and [aspnet](http://nuget.org/profiles/aspnet) accounts, which simply such aliases.</span></span>

### <a name="recovering-package-ownership"></a><span data-ttu-id="70a5d-168">Paket sahipliği kurtarma</span><span class="sxs-lookup"><span data-stu-id="70a5d-168">Recovering package ownership</span></span>

<span data-ttu-id="70a5d-169">Bazen, bir paket etkin bir sahip olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="70a5d-169">Occasionally, a package may not have an active owner.</span></span> <span data-ttu-id="70a5d-170">Örneğin, özgün sahibi paket hazırlayan şirket bırakmış olabilirsiniz, nuget.org kimlik bilgileri kaybolur veya önceki hatalar galerideki bir paket ownerless sol.</span><span class="sxs-lookup"><span data-stu-id="70a5d-170">For example, the original owner may have left the company that produces the package, nuget.org credentials are lost, or earlier bugs in the gallery left a package ownerless.</span></span>

<span data-ttu-id="70a5d-171">Bir paket gerçek sahibi ve sahipliğini yeniden elde etmek ihtiyacınız varsa, kullanmak [başvurun form](https://www.nuget.org/policies/Contact) nuget.org durumunuza NuGet ekibine açıklamak için.</span><span class="sxs-lookup"><span data-stu-id="70a5d-171">If you are the rightful owner of a package and need to regain ownership, use the [contact form](https://www.nuget.org/policies/Contact) on nuget.org to explain your situation to the NuGet team.</span></span> <span data-ttu-id="70a5d-172">Biz sahipliğiniz paketin proje URL'si, e-posta, Twitter ya da başka araçlar aracılığıyla mevcut sahibi bulmaya çalışırken de dahil olmak üzere paketin doğrulamak için bir işlem daha sonra izleyin.</span><span class="sxs-lookup"><span data-stu-id="70a5d-172">We then follow a process to verify your ownership of the package, including trying to locate the existing owner through the package's Project URL, Twitter, email, or other means.</span></span> <span data-ttu-id="70a5d-173">Ancak, tüm denemeler başarısız olursa, biz sahibi olmak için yeni bir davet gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="70a5d-173">But if all else fails, we can send you a new invite to become an owner.</span></span>
