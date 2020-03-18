---
title: NuGet paketi yayımlama
description: Bir NuGet paketini nuget.org veya özel akışlara yayımlama ve nuget.org üzerinde paket sahipliğini yönetme hakkında ayrıntılı yönergeler.
author: karann-msft
ms.author: karann
ms.date: 05/18/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 02c6c8f3018bfd063c2d16a10381f88b54cac840
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/16/2020
ms.locfileid: "79429026"
---
# <a name="publishing-packages"></a><span data-ttu-id="6ff65-103">Paketler yayımlanıyor</span><span class="sxs-lookup"><span data-stu-id="6ff65-103">Publishing packages</span></span>

<span data-ttu-id="6ff65-104">Bir paket oluşturup `.nupkg` dosyanız elinizin altında olduğunda, bu, diğer geliştiricilerin herkese açık veya özel olarak kullanılabilmesini sağlamak için basit bir işlemdir:</span><span class="sxs-lookup"><span data-stu-id="6ff65-104">Once you have created a package and have your `.nupkg` file in hand, it's a simple process to make it available to other developers, either publicly or privately:</span></span>

- <span data-ttu-id="6ff65-105">Ortak paketler, bu makalede açıklandığı gibi [NuGet.org](https://www.nuget.org/packages/manage/upload) aracılığıyla genel olarak tüm geliştiriciler tarafından kullanılabilir hale getirilir (NuGet 4.1.0 + gerektirir).</span><span class="sxs-lookup"><span data-stu-id="6ff65-105">Public packages are made available to all developers globally through [nuget.org](https://www.nuget.org/packages/manage/upload) as described in this article (requires NuGet 4.1.0+).</span></span>
- <span data-ttu-id="6ff65-106">Özel paketler, bir dosya paylaşımında, özel bir NuGet sunucusunda, [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish)veya Myget, Proal, Nexus deposu ve Artifactory gibi üçüncü taraf depolardan yararlanarak yalnızca bir ekip veya kuruluş tarafından kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="6ff65-106">Private packages are available to only a team or organization, by hosting them either a file share, a private NuGet server, [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish), or a third-party repository such as myget, ProGet, Nexus Repository, and Artifactory.</span></span> <span data-ttu-id="6ff65-107">Ek ayrıntılar için bkz. [barındırma paketlerine genel bakış](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="6ff65-107">For additional details, see [Hosting Packages Overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="6ff65-108">Bu makalede, nuget.org ' a yayımlama ele alınmaktadır. Azure Artifacts yayımlamak için bkz. [Paket Yönetimi](https://www.visualstudio.com/docs/package/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="6ff65-108">This article covers publishing to nuget.org; for publishing to Azure Artifacts, see [Package Management](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

## <a name="publish-to-nugetorg"></a><span data-ttu-id="6ff65-109">Nuget.org 'e Yayımla</span><span class="sxs-lookup"><span data-stu-id="6ff65-109">Publish to nuget.org</span></span>

<span data-ttu-id="6ff65-110">Nuget.org için Microsoft hesabı ile oturum açmanız gerekir, bu, hesabı nuget.org ile kaydetmeniz istenecektir. Ayrıca, portalın eski sürümleri kullanılarak oluşturulan bir nuget.org hesabıyla da oturum açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ff65-110">For nuget.org, you must sign in with a Microsoft account, with which you'll be asked to register the account with nuget.org. You can also sign in with a nuget.org account created using older versions of the portal.</span></span>

![NuGet oturum açma konumu](media/publish_NuGetSignIn.png)

<span data-ttu-id="6ff65-112">Sonra, nuget.org Web portalı aracılığıyla paketi karşıya yükleyebilir, komut satırından nuget.org 'e (`nuget.exe` 4.1.0 +) gönderebilir veya aşağıdaki bölümlerde açıklandığı gibi Azure DevOps Services aracılığıyla bir CI/CD işleminin parçası olarak yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ff65-112">Next, you can either upload the package through the nuget.org web portal, push to nuget.org from the command line (requires `nuget.exe` 4.1.0+) , or publish as part of a CI/CD process through Azure DevOps Services, as described in the following sections.</span></span>

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a><span data-ttu-id="6ff65-113">Web Portalı: nuget.org 'de paket yükle sekmesini kullanın</span><span class="sxs-lookup"><span data-stu-id="6ff65-113">Web portal: use the Upload Package tab on nuget.org</span></span>

1. <span data-ttu-id="6ff65-114">Nuget.org üst menüsünde **karşıya yükle** ' yi seçin ve paket konumuna gidin.</span><span class="sxs-lookup"><span data-stu-id="6ff65-114">Select **Upload** on the top menu of nuget.org and browse to the package location.</span></span>

    ![Nuget.org 'de paket yükleme](media/publish_UploadYourPackage.PNG)

1. <span data-ttu-id="6ff65-116">nuget.org, paket adının kullanılabilir olup olmadığını söyler.</span><span class="sxs-lookup"><span data-stu-id="6ff65-116">nuget.org tells you if the package name is available.</span></span> <span data-ttu-id="6ff65-117">Değilse, projenizdeki paket tanımlayıcısını değiştirin, yeniden derleyin ve karşıya yüklemeyi yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="6ff65-117">If it isn't, change the package identifier in your project, rebuild, and try the upload again.</span></span>

1. <span data-ttu-id="6ff65-118">Paket adı kullanılabiliyorsa nuget.org, paket bildiriminden meta verileri gözden geçirebilmeniz için bir **doğrulama** bölümü açar.</span><span class="sxs-lookup"><span data-stu-id="6ff65-118">If the package name is available, nuget.org opens a **Verify** section in which you can review the metadata from the package manifest.</span></span> <span data-ttu-id="6ff65-119">Meta verileri değiştirmek için projenizi (proje dosyası veya `.nuspec` dosyası) düzenleyin, yeniden derleyin, paketi yeniden oluşturun ve yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="6ff65-119">To change any of the metadata, edit your project (project file or `.nuspec` file), rebuild, recreate the package, and upload again.</span></span>

1. <span data-ttu-id="6ff65-120">**Belgeleri Içeri aktar** ' ın altında markaşağı yapıştırabilir, bir URL ile belgelerinize işaret edebilir veya bir belge dosyası yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ff65-120">Under **Import Documentation** you can paste Markdown, point to your docs with a URL, or upload a documentation file.</span></span>

1. <span data-ttu-id="6ff65-121">Tüm bilgiler hazırlanıyor, **Gönder** düğmesini seçin</span><span class="sxs-lookup"><span data-stu-id="6ff65-121">When all the information is ready, select the **Submit** button</span></span>

### <a name="command-line"></a><span data-ttu-id="6ff65-122">Komut satırı</span><span class="sxs-lookup"><span data-stu-id="6ff65-122">Command line</span></span>

<span data-ttu-id="6ff65-123">Paketleri nuget.org 'e göndermek için gereken [NuGet protokollerini](../api/nuget-protocols.md)uygulayan [NuGet. exe v 4.1.0 veya üstünü](https://www.nuget.org/downloads)kullanmalısınız.</span><span class="sxs-lookup"><span data-stu-id="6ff65-123">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span> <span data-ttu-id="6ff65-124">Ayrıca, nuget.org üzerinde oluşturulan bir API anahtarına de ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="6ff65-124">You also need an API key, which is created on nuget.org.</span></span>

#### <a name="create-api-keys"></a><span data-ttu-id="6ff65-125">API anahtarları oluşturma</span><span class="sxs-lookup"><span data-stu-id="6ff65-125">Create API keys</span></span>

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="6ff65-126">DotNet NuGet Push ile yayımlama</span><span class="sxs-lookup"><span data-stu-id="6ff65-126">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a><span data-ttu-id="6ff65-127">NuGet Push ile yayımlama</span><span class="sxs-lookup"><span data-stu-id="6ff65-127">Publish with nuget push</span></span>

1. <span data-ttu-id="6ff65-128">Komut isteminde, aşağıdaki komutu çalıştırarak `<your_API_key>` nuget.org adresinden elde edilen anahtarla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="6ff65-128">At a command prompt, run the following command, replacing `<your_API_key>` with the key obtained from nuget.org:</span></span>

    ```cli
    nuget setApiKey <your_API_key>
    ```

    <span data-ttu-id="6ff65-129">Bu komut, API anahtarınızı NuGet yapılandırmanızda depolar, böylece bu adımı aynı bilgisayarda tekrar yinelemeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="6ff65-129">This command stores your API key in your NuGet configuration so that you don't need to repeat this step again on the same computer.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6ff65-130">API anahtarı özel akışta kimlik doğrulaması için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="6ff65-130">API key is not used for authenticating with the private feed.</span></span> <span data-ttu-id="6ff65-131">Kaynak ile kimlik doğrulaması için kimlik bilgilerini yönetmek üzere [`nuget sources` komutuna](../reference/cli-reference/cli-ref-sources.md) bakın.</span><span class="sxs-lookup"><span data-stu-id="6ff65-131">Refer to [`nuget sources` command](../reference/cli-reference/cli-ref-sources.md) to manage credentials for authenticating with the source.</span></span>
    > <span data-ttu-id="6ff65-132">Tek bir NuGet sunucusundan API anahtarları elde edilebilir.</span><span class="sxs-lookup"><span data-stu-id="6ff65-132">API keys can be obtained from the individual NuGet servers.</span></span> <span data-ttu-id="6ff65-133">Nuget.org için APIKeys oluşturmak ve sağlamak üzere [Yayımla-api-Key](../quickstart/includes/publish-api-key.md)</span><span class="sxs-lookup"><span data-stu-id="6ff65-133">To create and manange APIKeys for nuget.org refer to [publish-api-key](../quickstart/includes/publish-api-key.md)</span></span>

1. <span data-ttu-id="6ff65-134">Aşağıdaki komutu kullanarak paketinizi NuGet galerisine gönderin:</span><span class="sxs-lookup"><span data-stu-id="6ff65-134">Push your package to NuGet Gallery using the following command:</span></span>

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

#### <a name="publish-signed-packages"></a><span data-ttu-id="6ff65-135">İmzalı paketleri yayımlama</span><span class="sxs-lookup"><span data-stu-id="6ff65-135">Publish signed packages</span></span>

<span data-ttu-id="6ff65-136">İmzalı paketleri göndermek için, önce paketleri imzalamak üzere kullanılan [sertifikayı kaydetmeniz](../create-packages/Sign-a-Package.md#register-the-certificate-on-nugetorg) gerekir.</span><span class="sxs-lookup"><span data-stu-id="6ff65-136">To submit signed packages, you must first [register the certificate](../create-packages/Sign-a-Package.md#register-the-certificate-on-nugetorg) used for signing the packages.</span></span> 

> [!Warning]
> <span data-ttu-id="6ff65-137">nuget.org, [İmzalı paket gereksinimlerini](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg)karşılamayan paketleri reddeder.</span><span class="sxs-lookup"><span data-stu-id="6ff65-137">nuget.org rejects packages that don't satisfy the [signed package requirements](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg).</span></span>

### <a name="package-validation-and-indexing"></a><span data-ttu-id="6ff65-138">Paket doğrulama ve dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="6ff65-138">Package validation and indexing</span></span>

<span data-ttu-id="6ff65-139">Paketler, virüs denetimleri gibi çeşitli doğrulamaları nuget.org 'e gönderdi.</span><span class="sxs-lookup"><span data-stu-id="6ff65-139">Packages pushed to nuget.org undergo several validations, such as virus checks.</span></span> <span data-ttu-id="6ff65-140">(Nuget.org üzerindeki tüm paketler düzenli aralıklarla taranır.)</span><span class="sxs-lookup"><span data-stu-id="6ff65-140">(All packages on nuget.org are periodically scanned.)</span></span>

<span data-ttu-id="6ff65-141">Paket tüm doğrulama denetimlerini geçtiğinde, dizin oluşturulması ve arama sonuçlarında görünmesi biraz zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="6ff65-141">When the package has passed all validation checks, it might take a while for it to be indexed and appear in search results.</span></span> <span data-ttu-id="6ff65-142">Dizin oluşturma işlemi tamamlandıktan sonra, paketin başarıyla yayımlandığını onaylayan bir e-posta alırsınız.</span><span class="sxs-lookup"><span data-stu-id="6ff65-142">Once indexing is complete, you receive an email confirming that the package was successfully published.</span></span> <span data-ttu-id="6ff65-143">Paket bir doğrulama denetiminden başarısız olursa, paket ayrıntıları sayfası ilgili hatayı görüntüleyecek şekilde güncellenecek ve size bir e-posta gönderilir.</span><span class="sxs-lookup"><span data-stu-id="6ff65-143">If the package fails a validation check, the package details page will update to display the associated error and you also receive an email notifying you about it.</span></span>

<span data-ttu-id="6ff65-144">Paket doğrulama ve dizin oluşturma genellikle 15 dakika boyunca sürer.</span><span class="sxs-lookup"><span data-stu-id="6ff65-144">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="6ff65-145">Paket yayımlaması beklenenden uzun sürüyorsa, nuget.org 'in herhangi bir kesinti yaşamadığını denetlemek için [Status.NuGet.org](https://status.nuget.org/) adresini ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="6ff65-145">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if nuget.org is experiencing any interruptions.</span></span> <span data-ttu-id="6ff65-146">Tüm sistemler çalışır durumda ve paket bir saat içinde başarıyla yayımlanmamışsa, lütfen nuget.org ' e oturum açın ve paket sayfasındaki desteğe başvurun bağlantısını kullanarak bizimle iletişime geçin.</span><span class="sxs-lookup"><span data-stu-id="6ff65-146">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package page.</span></span>

<span data-ttu-id="6ff65-147">Bir paketin durumunu görmek için nuget.org adresindeki hesap adınızın altındaki **paketleri Yönet** ' i seçin. Doğrulama tamamlandığında bir onay e-postası alırsınız.</span><span class="sxs-lookup"><span data-stu-id="6ff65-147">To see the status of a package, select **Manage packages** under your account name on nuget.org. You receive a confirmation email when validation is complete.</span></span>

<span data-ttu-id="6ff65-148">Paketinizin dizine alınması ve başkalarının bulabileceği arama sonuçlarında görünmesi biraz zaman alabilir ve bu durumda paket sayfanızda aşağıdaki iletiyi görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="6ff65-148">Note that it might take a while for your package to be indexed and appear in search results where others can find it, during which time you see the following message on your package page:</span></span>

![Bir paketin henüz yayımlanmadığını belirten ileti](media/publish_NotYetIndexed.png)

### <a name="azure-devops-services-cicd"></a><span data-ttu-id="6ff65-150">Azure DevOps Services (CI/CD)</span><span class="sxs-lookup"><span data-stu-id="6ff65-150">Azure DevOps Services (CI/CD)</span></span>

<span data-ttu-id="6ff65-151">Sürekli tümleştirme/dağıtım işleminizin bir parçası olarak Azure DevOps Services kullanarak paketler nuget.org 'e gönderim yaparsanız, NuGet görevlerinde `nuget.exe` 4,1 veya üzeri bir sürümü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="6ff65-151">If you push packages to nuget.org using Azure DevOps Services as part of your Continuous Integration/Deployment process, you must use `nuget.exe` 4.1 or above in the NuGet tasks.</span></span> <span data-ttu-id="6ff65-152">Ayrıntılar [, derlemede en son NuGet](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blogu) kullanılarak bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="6ff65-152">Details can be found on [Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blog).</span></span>

## <a name="managing-package-owners-on-nugetorg"></a><span data-ttu-id="6ff65-153">Nuget.org üzerinde paket sahiplerini yönetme</span><span class="sxs-lookup"><span data-stu-id="6ff65-153">Managing package owners on nuget.org</span></span>

<span data-ttu-id="6ff65-154">Her NuGet paketinin `.nuspec` dosyası paketin yazarlarını tanımlasa da, nuget.org Galerisi bu meta verileri sahipliğini tanımlamak için kullanmaz.</span><span class="sxs-lookup"><span data-stu-id="6ff65-154">Although each NuGet package's `.nuspec` file defines the package's authors, the nuget.org gallery does not use that metadata to define ownership.</span></span> <span data-ttu-id="6ff65-155">Bunun yerine nuget.org, paketi yayımlayan kişiye ilk sahiplik atar.</span><span class="sxs-lookup"><span data-stu-id="6ff65-155">Instead, nuget.org assigns initial ownership to the person who publishes the package.</span></span> <span data-ttu-id="6ff65-156">Bu, paketi nuget.org kullanıcı arabiriminden yükleyen oturum açmış bir kullanıcı veya API anahtarı `nuget SetApiKey` veya `nuget push`ile kullanılmış olan kullanıcıdır.</span><span class="sxs-lookup"><span data-stu-id="6ff65-156">This is either the logged-in user who uploaded the package through the nuget.org UI, or the users whose API key was used with `nuget SetApiKey` or `nuget push`.</span></span>

<span data-ttu-id="6ff65-157">Tüm paket sahipleri, diğer sahipleri ekleme ve kaldırma ve güncelleştirme yayımlama dahil olmak üzere paket için tam izinlere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="6ff65-157">All package owners have full permissions for the package, including adding and removing other owners, and publishing updates.</span></span>

<span data-ttu-id="6ff65-158">Bir paketin sahipliğini değiştirmek için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="6ff65-158">To change ownership of a package, do the following:</span></span>

1. <span data-ttu-id="6ff65-159">Nuget.org 'de paketin geçerli sahibi olan hesapla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="6ff65-159">Sign in to nuget.org with the account that is the current owner of the package.</span></span>
1. <span data-ttu-id="6ff65-160">Hesap adınızı seçin, **paketleri Yönet**' i seçin ve **yayımlanan paketler**' i genişletin.</span><span class="sxs-lookup"><span data-stu-id="6ff65-160">Select your account name, select **Manage packages**, and expand **Published Packages**.</span></span>
1. <span data-ttu-id="6ff65-161">Yönetmek istediğiniz paketi seçin, ardından sağ tarafta **sahipleri Yönet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="6ff65-161">Select on the package you want to manage, then on the right side select **Manage owners**.</span></span>

<span data-ttu-id="6ff65-162">Buradan çeşitli seçenekleriniz vardır:</span><span class="sxs-lookup"><span data-stu-id="6ff65-162">From here you have several options:</span></span>

1. <span data-ttu-id="6ff65-163">**Geçerli sahipler**altında listelenen tüm sahipleri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="6ff65-163">Remove any owner listed under **Current Owners**.</span></span>
1. <span data-ttu-id="6ff65-164">Kullanıcı adını, bir iletiyi girerek ve **Ekle**' yi seçerek **sahip Ekle** altına bir sahip ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6ff65-164">Add an owner under **Add Owner** by entering their user name, a message, and selecting **Add**.</span></span> <span data-ttu-id="6ff65-165">Bu eylem, bu yeni ortak Sahibe onay bağlantısı ile bir e-posta gönderir.</span><span class="sxs-lookup"><span data-stu-id="6ff65-165">This action sends an email to that new co-owner with a confirmation link.</span></span> <span data-ttu-id="6ff65-166">Onaylandıktan sonra, bu kişinin sahipleri eklemek ve kaldırmak için tam izinleri vardır.</span><span class="sxs-lookup"><span data-stu-id="6ff65-166">Once confirmed, that person has full permissions to add and remove owners.</span></span> <span data-ttu-id="6ff65-167">(Onaylanana kadar, **geçerli sahipler** bölümü söz konusu kişi için bekleyen onay olduğunu gösterir.)</span><span class="sxs-lookup"><span data-stu-id="6ff65-167">(Until confirmed, the **Current Owners** section indicates pending approval for that person.)</span></span>
1. <span data-ttu-id="6ff65-168">Sahipliği aktarmak için (sahiplik değişiklikleri veya bir paket yanlış hesap altında yayımlandığında olduğu gibi), yeni sahibi ekleyin ve sahipliği onayladıktan sonra listeden kaldırabilir.</span><span class="sxs-lookup"><span data-stu-id="6ff65-168">To transfer ownership (as when ownership changes or a package was published under the wrong account), add the new owner, and once they've confirmed ownership they can remove you from the list.</span></span>

<span data-ttu-id="6ff65-169">Bir şirkete veya gruba sahiplik atamak için, uygun takım üyelerine iletilen bir e-posta diğer adı kullanarak bir nuget.org hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6ff65-169">To assign ownership to a company or group, create a nuget.org account using an email alias that is forwarded to the appropriate team members.</span></span> <span data-ttu-id="6ff65-170">Örneğin, çeşitli Microsoft ASP.NET paketleri [Microsoft](https://nuget.org/profiles/microsoft) ve [ASPNET](https://nuget.org/profiles/aspnet) hesaplarına aittir, bu da yalnızca diğer adlar vardır.</span><span class="sxs-lookup"><span data-stu-id="6ff65-170">For example, various Microsoft ASP.NET packages are co-owned by the [microsoft](https://nuget.org/profiles/microsoft) and [aspnet](https://nuget.org/profiles/aspnet) accounts, which simply such aliases.</span></span>

### <a name="recovering-package-ownership"></a><span data-ttu-id="6ff65-171">Paket sahipliği kurtarılıyor</span><span class="sxs-lookup"><span data-stu-id="6ff65-171">Recovering package ownership</span></span>

<span data-ttu-id="6ff65-172">Bazen bir paket etkin bir sahibe sahip olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="6ff65-172">Occasionally, a package may not have an active owner.</span></span> <span data-ttu-id="6ff65-173">Örneğin, özgün sahip, paketi üreten şirketi bıraktı, nuget.org kimlik bilgileri kayboluyor veya galerideki daha önceki hatalar bir paket sahipi bıraktı.</span><span class="sxs-lookup"><span data-stu-id="6ff65-173">For example, the original owner may have left the company that produces the package, nuget.org credentials are lost, or earlier bugs in the gallery left a package ownerless.</span></span>

<span data-ttu-id="6ff65-174">Bir paketin sağtasyon sahibiyseniz ve sahipliği yeniden kazanmak istiyorsanız, nuget.org adresindeki [iletişim formunu](https://www.nuget.org/policies/Contact) kullanarak, durumunuzu NuGet ekibine açıklayın.</span><span class="sxs-lookup"><span data-stu-id="6ff65-174">If you are the rightful owner of a package and need to regain ownership, use the [contact form](https://www.nuget.org/policies/Contact) on nuget.org to explain your situation to the NuGet team.</span></span> <span data-ttu-id="6ff65-175">Daha sonra paketin sahipliğini doğrulamak için, paketin proje URL 'SI, Twitter, e-posta veya başka yollarla mevcut sahibini bulmaya çalışmak de dahil olmak üzere bir işlemi izliyoruz.</span><span class="sxs-lookup"><span data-stu-id="6ff65-175">We then follow a process to verify your ownership of the package, including trying to locate the existing owner through the package's Project URL, Twitter, email, or other means.</span></span> <span data-ttu-id="6ff65-176">Ancak diğerleri başarısız olursa, size sahip olmaya yönelik yeni bir davet gönderebiliriz.</span><span class="sxs-lookup"><span data-stu-id="6ff65-176">But if all else fails, we can send you a new invite to become an owner.</span></span>
