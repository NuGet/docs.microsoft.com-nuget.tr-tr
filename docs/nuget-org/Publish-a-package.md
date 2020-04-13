---
title: NuGet Paketi Nasıl Yayınlanır?
description: NuGet paketinin nuget.org veya özel akışlara nasıl yayımlanacağına ve nuget.org paket sahipliğinin nasıl yönetileceklerine ilişkin ayrıntılı yönergeler.
author: karann-msft
ms.author: karann
ms.date: 05/18/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 02c6c8f3018bfd063c2d16a10381f88b54cac840
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79429026"
---
# <a name="publishing-packages"></a><span data-ttu-id="148fd-103">Yayımlama paketleri</span><span class="sxs-lookup"><span data-stu-id="148fd-103">Publishing packages</span></span>

<span data-ttu-id="148fd-104">Bir paket oluşturduktan ve `.nupkg` dosyanızı elinizin altında bulunduktan sonra, paketi genel veya özel olarak diğer geliştiricilerin kullanımına açmak basit bir işlemdir:</span><span class="sxs-lookup"><span data-stu-id="148fd-104">Once you have created a package and have your `.nupkg` file in hand, it's a simple process to make it available to other developers, either publicly or privately:</span></span>

- <span data-ttu-id="148fd-105">Genel paketler, bu makalede açıklandığı gibi [nuget.org](https://www.nuget.org/packages/manage/upload) aracılığıyla tüm geliştiricilerin kullanımına sunulmuştur (NuGet 4.1.0+' gerektirir).</span><span class="sxs-lookup"><span data-stu-id="148fd-105">Public packages are made available to all developers globally through [nuget.org](https://www.nuget.org/packages/manage/upload) as described in this article (requires NuGet 4.1.0+).</span></span>
- <span data-ttu-id="148fd-106">Özel paketler, yalnızca bir dosya paylaşımı, özel nuget sunucusu, [Azure Yapıları](https://www.visualstudio.com/docs/package/nuget/publish)veya myget, ProGet, Nexus Deposu ve Artifactory gibi üçüncü taraf depolarını barındırarak yalnızca bir ekip veya kuruluş tarafından kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="148fd-106">Private packages are available to only a team or organization, by hosting them either a file share, a private NuGet server, [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish), or a third-party repository such as myget, ProGet, Nexus Repository, and Artifactory.</span></span> <span data-ttu-id="148fd-107">Daha fazla ayrıntı için [Hosting Paketlerine Genel Bakış'a](../hosting-packages/overview.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="148fd-107">For additional details, see [Hosting Packages Overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="148fd-108">Bu makale, nuget.org yayımlama yı kapsar; Azure Yapıları'nda yayımlamak için [Bkz. Paket Yönetimi.](https://www.visualstudio.com/docs/package/nuget/publish)</span><span class="sxs-lookup"><span data-stu-id="148fd-108">This article covers publishing to nuget.org; for publishing to Azure Artifacts, see [Package Management](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

## <a name="publish-to-nugetorg"></a><span data-ttu-id="148fd-109">nuget.org yayınlayın</span><span class="sxs-lookup"><span data-stu-id="148fd-109">Publish to nuget.org</span></span>

<span data-ttu-id="148fd-110">nuget.org için, hesabı nuget.org kaydettirmeniz istenecek bir Microsoft hesabıyla oturum açmanız gerekir. Portalın eski sürümleri kullanılarak oluşturulan nuget.org bir hesapla da oturum açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="148fd-110">For nuget.org, you must sign in with a Microsoft account, with which you'll be asked to register the account with nuget.org. You can also sign in with a nuget.org account created using older versions of the portal.</span></span>

![NuGet konumunda oturum aç](media/publish_NuGetSignIn.png)

<span data-ttu-id="148fd-112">Ardından, paketi nuget.org web portalı üzerinden yükleyebilir, komut satırından nuget.org'a itebilir `nuget.exe` (4.1.0+) veya aşağıdaki bölümlerde açıklandığı gibi Azure DevOps Hizmetleri aracılığıyla CI/CD işleminin bir parçası olarak yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="148fd-112">Next, you can either upload the package through the nuget.org web portal, push to nuget.org from the command line (requires `nuget.exe` 4.1.0+) , or publish as part of a CI/CD process through Azure DevOps Services, as described in the following sections.</span></span>

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a><span data-ttu-id="148fd-113">Web portalı: nuget.org'daki Yükleme Paketi sekmesini kullanın</span><span class="sxs-lookup"><span data-stu-id="148fd-113">Web portal: use the Upload Package tab on nuget.org</span></span>

1. <span data-ttu-id="148fd-114">nuget.org üst menüsünden **Yükle'yi** seçin ve paket konumuna göz atın.</span><span class="sxs-lookup"><span data-stu-id="148fd-114">Select **Upload** on the top menu of nuget.org and browse to the package location.</span></span>

    ![nuget.org'da paket yükleyin](media/publish_UploadYourPackage.PNG)

1. <span data-ttu-id="148fd-116">nuget.org paket adının kullanılabilir olup olmadığını söyler.</span><span class="sxs-lookup"><span data-stu-id="148fd-116">nuget.org tells you if the package name is available.</span></span> <span data-ttu-id="148fd-117">Değilse, projenizdeki paket tanımlayıcısını değiştirin, yeniden yeniden oluşturun ve yüklemeyi yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="148fd-117">If it isn't, change the package identifier in your project, rebuild, and try the upload again.</span></span>

1. <span data-ttu-id="148fd-118">Paket adı varsa, nuget.org paket bildiriminden meta verileri gözden geçirebileceğiniz bir **Doğrula** bölümünü açar.</span><span class="sxs-lookup"><span data-stu-id="148fd-118">If the package name is available, nuget.org opens a **Verify** section in which you can review the metadata from the package manifest.</span></span> <span data-ttu-id="148fd-119">Meta verilerden herhangi birini değiştirmek için projenizi `.nuspec` (proje dosyası veya dosya) edin, yeniden oluşturun, paketi yeniden oluşturun ve yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="148fd-119">To change any of the metadata, edit your project (project file or `.nuspec` file), rebuild, recreate the package, and upload again.</span></span>

1. <span data-ttu-id="148fd-120">**Belgeyi Aktar'ın** altında Markdown'u yapıştırabilir, dokümanlarınızı BIR URL ile işaret edebilir veya bir belge dosyası yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="148fd-120">Under **Import Documentation** you can paste Markdown, point to your docs with a URL, or upload a documentation file.</span></span>

1. <span data-ttu-id="148fd-121">Tüm bilgiler hazır olduğunda Gönder **düğmesini** seçin</span><span class="sxs-lookup"><span data-stu-id="148fd-121">When all the information is ready, select the **Submit** button</span></span>

### <a name="command-line"></a><span data-ttu-id="148fd-122">Komut satırı</span><span class="sxs-lookup"><span data-stu-id="148fd-122">Command line</span></span>

<span data-ttu-id="148fd-123">Paketleri nuget.org itmek için gerekli [NuGet protokollerini](../api/nuget-protocols.md)uygulayan [nuget.exe v4.1.0 veya üzeri](https://www.nuget.org/downloads)nikullanmalısınız.</span><span class="sxs-lookup"><span data-stu-id="148fd-123">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span> <span data-ttu-id="148fd-124">Ayrıca, nuget.org'da oluşturulan bir API anahtarına da ihtiyacınız var.</span><span class="sxs-lookup"><span data-stu-id="148fd-124">You also need an API key, which is created on nuget.org.</span></span>

#### <a name="create-api-keys"></a><span data-ttu-id="148fd-125">API tuşlarını oluşturma</span><span class="sxs-lookup"><span data-stu-id="148fd-125">Create API keys</span></span>

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="148fd-126">dotnet nuget push ile yayımla</span><span class="sxs-lookup"><span data-stu-id="148fd-126">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a><span data-ttu-id="148fd-127">Nuget push ile yayımla</span><span class="sxs-lookup"><span data-stu-id="148fd-127">Publish with nuget push</span></span>

1. <span data-ttu-id="148fd-128">Komut isteminde, nuget.org elde edilen `<your_API_key>` anahtarı değiştirerek aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="148fd-128">At a command prompt, run the following command, replacing `<your_API_key>` with the key obtained from nuget.org:</span></span>

    ```cli
    nuget setApiKey <your_API_key>
    ```

    <span data-ttu-id="148fd-129">Bu komut, API anahtarınızı NuGet yapılandırmanızda saklar, böylece bu adımı aynı bilgisayarda tekrarlamanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="148fd-129">This command stores your API key in your NuGet configuration so that you don't need to repeat this step again on the same computer.</span></span>

    > [!NOTE]
    > <span data-ttu-id="148fd-130">API anahtarı, özel beslemeyle kimlik doğrulaması için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="148fd-130">API key is not used for authenticating with the private feed.</span></span> <span data-ttu-id="148fd-131">Kaynakla kimlik doğrulaması için kimlik bilgilerini yönetmek için [ `nuget sources` komuta](../reference/cli-reference/cli-ref-sources.md) bakın.</span><span class="sxs-lookup"><span data-stu-id="148fd-131">Refer to [`nuget sources` command](../reference/cli-reference/cli-ref-sources.md) to manage credentials for authenticating with the source.</span></span>
    > <span data-ttu-id="148fd-132">API anahtarları tek tek NuGet sunucularından elde edilebilir.</span><span class="sxs-lookup"><span data-stu-id="148fd-132">API keys can be obtained from the individual NuGet servers.</span></span> <span data-ttu-id="148fd-133">nuget.org için APIKeys oluşturmak ve manange için [publish-api-key](../quickstart/includes/publish-api-key.md) bakın</span><span class="sxs-lookup"><span data-stu-id="148fd-133">To create and manange APIKeys for nuget.org refer to [publish-api-key](../quickstart/includes/publish-api-key.md)</span></span>

1. <span data-ttu-id="148fd-134">Aşağıdaki komutu kullanarak paketinizi NuGet Galerisi'ne itin:</span><span class="sxs-lookup"><span data-stu-id="148fd-134">Push your package to NuGet Gallery using the following command:</span></span>

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

#### <a name="publish-signed-packages"></a><span data-ttu-id="148fd-135">İmzalı paketleri yayımlama</span><span class="sxs-lookup"><span data-stu-id="148fd-135">Publish signed packages</span></span>

<span data-ttu-id="148fd-136">İmzalı paketleri göndermek için, önce paketleri imzalamak için kullanılan [sertifikayı kaydetmeniz](../create-packages/Sign-a-Package.md#register-the-certificate-on-nugetorg) gerekir.</span><span class="sxs-lookup"><span data-stu-id="148fd-136">To submit signed packages, you must first [register the certificate](../create-packages/Sign-a-Package.md#register-the-certificate-on-nugetorg) used for signing the packages.</span></span> 

> [!Warning]
> <span data-ttu-id="148fd-137">nuget.org, [imzalanan paket gereksinimlerini](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg)karşılamayan paketleri reddeder.</span><span class="sxs-lookup"><span data-stu-id="148fd-137">nuget.org rejects packages that don't satisfy the [signed package requirements](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg).</span></span>

### <a name="package-validation-and-indexing"></a><span data-ttu-id="148fd-138">Paket doğrulama ve dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="148fd-138">Package validation and indexing</span></span>

<span data-ttu-id="148fd-139">nuget.org itilen paketler virüs denetimleri gibi çeşitli doğrulamalara tabi dir.</span><span class="sxs-lookup"><span data-stu-id="148fd-139">Packages pushed to nuget.org undergo several validations, such as virus checks.</span></span> <span data-ttu-id="148fd-140">(nuget.org üzerindeki tüm paketler periyodik olarak taranır.)</span><span class="sxs-lookup"><span data-stu-id="148fd-140">(All packages on nuget.org are periodically scanned.)</span></span>

<span data-ttu-id="148fd-141">Paket tüm doğrulama denetimlerini geçtiğinde, dizine ekleştirilmesi ve arama sonuçlarında görünmesi biraz zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="148fd-141">When the package has passed all validation checks, it might take a while for it to be indexed and appear in search results.</span></span> <span data-ttu-id="148fd-142">Dizin oluşturma tamamlandıktan sonra, paketin başarıyla yayımlandığını onaylayan bir e-posta alırsınız.</span><span class="sxs-lookup"><span data-stu-id="148fd-142">Once indexing is complete, you receive an email confirming that the package was successfully published.</span></span> <span data-ttu-id="148fd-143">Paket doğrulama denetiminde başarısız olursa, paket ayrıntıları sayfası ilişkili hatayı görüntülemek için güncellenir ve ayrıca bu konuda size bildiren bir e-posta alırsınız.</span><span class="sxs-lookup"><span data-stu-id="148fd-143">If the package fails a validation check, the package details page will update to display the associated error and you also receive an email notifying you about it.</span></span>

<span data-ttu-id="148fd-144">Paket doğrulama ve dizin oluşturma genellikle 15 dakikanın altında sürer.</span><span class="sxs-lookup"><span data-stu-id="148fd-144">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="148fd-145">Paket yayımlama beklenenden uzun sürüyorsa, nuget.org herhangi bir kesinti yaşanıp yaşanmayacağını kontrol etmek için [status.nuget.org](https://status.nuget.org/) ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="148fd-145">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if nuget.org is experiencing any interruptions.</span></span> <span data-ttu-id="148fd-146">Tüm sistemler çalışır durumdaysa ve paket bir saat içinde başarıyla yayınlanmamışsa, lütfen nuget.org giriş yapın ve paket sayfasındaki Destek Bağlantısını kullanarak bizimle iletişime geçin.</span><span class="sxs-lookup"><span data-stu-id="148fd-146">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package page.</span></span>

<span data-ttu-id="148fd-147">Paketin durumunu görmek için, nuget.org'da hesap adınız altında **paketleri yönet'i** seçin. Doğrulama tamamlandığında bir onay e-postası alırsınız.</span><span class="sxs-lookup"><span data-stu-id="148fd-147">To see the status of a package, select **Manage packages** under your account name on nuget.org. You receive a confirmation email when validation is complete.</span></span>

<span data-ttu-id="148fd-148">Paketinizin dizine eksinin eklenmesinin biraz zaman alacağını ve başkalarının bulabileceği arama sonuçlarında görünmesinin biraz zaman alacağını ve bu süre zarfında paket sayfanızda aşağıdaki iletiyi görebileceğinizi unutmayın:</span><span class="sxs-lookup"><span data-stu-id="148fd-148">Note that it might take a while for your package to be indexed and appear in search results where others can find it, during which time you see the following message on your package page:</span></span>

![Paketin henüz yayımlanmadığını belirten ileti](media/publish_NotYetIndexed.png)

### <a name="azure-devops-services-cicd"></a><span data-ttu-id="148fd-150">Azure Devops Hizmetleri (CI/CD)</span><span class="sxs-lookup"><span data-stu-id="148fd-150">Azure DevOps Services (CI/CD)</span></span>

<span data-ttu-id="148fd-151">Sürekli Tümleştirme/Dağıtım işleminizin bir parçası olarak Azure DevOps Hizmetlerini kullanarak `nuget.exe` paketleri nuget.org iterseniz, NuGet görevlerinde 4.1 ve üzerini kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="148fd-151">If you push packages to nuget.org using Azure DevOps Services as part of your Continuous Integration/Deployment process, you must use `nuget.exe` 4.1 or above in the NuGet tasks.</span></span> <span data-ttu-id="148fd-152">Ayrıntılar, [yapınızdaki en son NuGet'i](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blogu) kullanma hakkında bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="148fd-152">Details can be found on [Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blog).</span></span>

## <a name="managing-package-owners-on-nugetorg"></a><span data-ttu-id="148fd-153">paket sahiplerini nuget.org</span><span class="sxs-lookup"><span data-stu-id="148fd-153">Managing package owners on nuget.org</span></span>

<span data-ttu-id="148fd-154">Her NuGet paketinin `.nuspec` dosyası paketin yazarlarını tanımlasa da, nuget.org galerisi sahipliği tanımlamak için bu meta verileri kullanmaz.</span><span class="sxs-lookup"><span data-stu-id="148fd-154">Although each NuGet package's `.nuspec` file defines the package's authors, the nuget.org gallery does not use that metadata to define ownership.</span></span> <span data-ttu-id="148fd-155">Bunun yerine, nuget.org paketi yayımlayan kişiye ilk sahipliği atar.</span><span class="sxs-lookup"><span data-stu-id="148fd-155">Instead, nuget.org assigns initial ownership to the person who publishes the package.</span></span> <span data-ttu-id="148fd-156">Bu, paketi kullanıcı nuget.org Kullanıcı Arama Birimi üzerinden yükleyen oturum açmış kullanıcı veya API `nuget SetApiKey` `nuget push`anahtarı nın kullanıldığı kullanıcılar veya.</span><span class="sxs-lookup"><span data-stu-id="148fd-156">This is either the logged-in user who uploaded the package through the nuget.org UI, or the users whose API key was used with `nuget SetApiKey` or `nuget push`.</span></span>

<span data-ttu-id="148fd-157">Tüm paket sahipleri, diğer sahiplerin eklenmesi ve kaldırılması ve güncelleştirmelerin yayımlanması da dahil olmak üzere paket için tam izinlere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="148fd-157">All package owners have full permissions for the package, including adding and removing other owners, and publishing updates.</span></span>

<span data-ttu-id="148fd-158">Bir paketin sahipliğini değiştirmek için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="148fd-158">To change ownership of a package, do the following:</span></span>

1. <span data-ttu-id="148fd-159">Paketin geçerli sahibi olan hesapla nuget.org oturum açın.</span><span class="sxs-lookup"><span data-stu-id="148fd-159">Sign in to nuget.org with the account that is the current owner of the package.</span></span>
1. <span data-ttu-id="148fd-160">Hesap adınızı seçin, **Paketleri Yönet'i**seçin ve **Yayınlanan Paketleri genişletin.**</span><span class="sxs-lookup"><span data-stu-id="148fd-160">Select your account name, select **Manage packages**, and expand **Published Packages**.</span></span>
1. <span data-ttu-id="148fd-161">Yönetmek istediğiniz pakette seçin, ardından sağ tarafta **sahipleri yönet'i**seçin.</span><span class="sxs-lookup"><span data-stu-id="148fd-161">Select on the package you want to manage, then on the right side select **Manage owners**.</span></span>

<span data-ttu-id="148fd-162">Buradan birkaç seçeneğiniz var:</span><span class="sxs-lookup"><span data-stu-id="148fd-162">From here you have several options:</span></span>

1. <span data-ttu-id="148fd-163">**Geçerli Sahipler**altında listelenen tüm sahibi kaldırın.</span><span class="sxs-lookup"><span data-stu-id="148fd-163">Remove any owner listed under **Current Owners**.</span></span>
1. <span data-ttu-id="148fd-164">Kullanıcı adını, bir iletiyi girerek ve **Ekle'yi**seçerek **Sahibi Ekle'nin** altına bir sahip ekle.</span><span class="sxs-lookup"><span data-stu-id="148fd-164">Add an owner under **Add Owner** by entering their user name, a message, and selecting **Add**.</span></span> <span data-ttu-id="148fd-165">Bu eylem, onay bağlantısı olan yeni ortak sahibine bir e-posta gönderir.</span><span class="sxs-lookup"><span data-stu-id="148fd-165">This action sends an email to that new co-owner with a confirmation link.</span></span> <span data-ttu-id="148fd-166">Onaylandıktan sonra, bu kişinin sahiplerini eklemek ve kaldırmak için tam izinleri vardır.</span><span class="sxs-lookup"><span data-stu-id="148fd-166">Once confirmed, that person has full permissions to add and remove owners.</span></span> <span data-ttu-id="148fd-167">(Onaylanana kadar, **Geçerli Sahipler** bölümü o kişinin onayını beklemede olduğunu gösterir.)</span><span class="sxs-lookup"><span data-stu-id="148fd-167">(Until confirmed, the **Current Owners** section indicates pending approval for that person.)</span></span>
1. <span data-ttu-id="148fd-168">Sahipliği aktarmak için (sahiplik değiştiğinde veya bir paket yanlış hesap altında yayınlandığında olduğu gibi), yeni sahibi ekleyin ve sahipliği onayladıktan sonra sizi listeden kaldırabilirler.</span><span class="sxs-lookup"><span data-stu-id="148fd-168">To transfer ownership (as when ownership changes or a package was published under the wrong account), add the new owner, and once they've confirmed ownership they can remove you from the list.</span></span>

<span data-ttu-id="148fd-169">Bir şirkete veya gruba sahiplik atamak için, ilgili ekip üyelerine iletilen bir e-posta takma adını kullanarak bir nuget.org hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="148fd-169">To assign ownership to a company or group, create a nuget.org account using an email alias that is forwarded to the appropriate team members.</span></span> <span data-ttu-id="148fd-170">Örneğin, çeşitli Microsoft ASP.NET paketleri, yalnızca bu tür diğer adları içeren [microsoft](https://nuget.org/profiles/microsoft) ve [aspnet](https://nuget.org/profiles/aspnet) hesaplarına aittir.</span><span class="sxs-lookup"><span data-stu-id="148fd-170">For example, various Microsoft ASP.NET packages are co-owned by the [microsoft](https://nuget.org/profiles/microsoft) and [aspnet](https://nuget.org/profiles/aspnet) accounts, which simply such aliases.</span></span>

### <a name="recovering-package-ownership"></a><span data-ttu-id="148fd-171">Paket sahipliğini kurtarma</span><span class="sxs-lookup"><span data-stu-id="148fd-171">Recovering package ownership</span></span>

<span data-ttu-id="148fd-172">Bazen, bir paketin etkin bir sahibi olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="148fd-172">Occasionally, a package may not have an active owner.</span></span> <span data-ttu-id="148fd-173">Örneğin, özgün sahibi paketi üreten şirketten ayrılmış olabilir, kimlik bilgilerinin kaybolmasına nuget.org veya galerideki önceki hatalar paket sahibiz bırakılmış olabilir.</span><span class="sxs-lookup"><span data-stu-id="148fd-173">For example, the original owner may have left the company that produces the package, nuget.org credentials are lost, or earlier bugs in the gallery left a package ownerless.</span></span>

<span data-ttu-id="148fd-174">Bir paketin gerçek sahibiyseniz ve sahipliğini yeniden kazanmanız gerekiyorsa, durumunuzu NuGet ekibine açıklamak için nuget.org'daki [iletişim formunu](https://www.nuget.org/policies/Contact) kullanın.</span><span class="sxs-lookup"><span data-stu-id="148fd-174">If you are the rightful owner of a package and need to regain ownership, use the [contact form](https://www.nuget.org/policies/Contact) on nuget.org to explain your situation to the NuGet team.</span></span> <span data-ttu-id="148fd-175">Daha sonra, paketin Proje URL'si, Twitter, e-posta veya diğer yollarla mevcut sahibini bulmaya çalışmak da dahil olmak üzere paketin sahipliğini doğrulamak için bir işlem uygularız.</span><span class="sxs-lookup"><span data-stu-id="148fd-175">We then follow a process to verify your ownership of the package, including trying to locate the existing owner through the package's Project URL, Twitter, email, or other means.</span></span> <span data-ttu-id="148fd-176">Ama her şey başarısız olursa, sana yeni bir davet gönderebiliriz.</span><span class="sxs-lookup"><span data-stu-id="148fd-176">But if all else fails, we can send you a new invite to become an owner.</span></span>
