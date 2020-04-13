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
# <a name="publishing-packages"></a>Yayımlama paketleri

Bir paket oluşturduktan ve `.nupkg` dosyanızı elinizin altında bulunduktan sonra, paketi genel veya özel olarak diğer geliştiricilerin kullanımına açmak basit bir işlemdir:

- Genel paketler, bu makalede açıklandığı gibi [nuget.org](https://www.nuget.org/packages/manage/upload) aracılığıyla tüm geliştiricilerin kullanımına sunulmuştur (NuGet 4.1.0+' gerektirir).
- Özel paketler, yalnızca bir dosya paylaşımı, özel nuget sunucusu, [Azure Yapıları](https://www.visualstudio.com/docs/package/nuget/publish)veya myget, ProGet, Nexus Deposu ve Artifactory gibi üçüncü taraf depolarını barındırarak yalnızca bir ekip veya kuruluş tarafından kullanılabilir. Daha fazla ayrıntı için [Hosting Paketlerine Genel Bakış'a](../hosting-packages/overview.md)bakın.

Bu makale, nuget.org yayımlama yı kapsar; Azure Yapıları'nda yayımlamak için [Bkz. Paket Yönetimi.](https://www.visualstudio.com/docs/package/nuget/publish)

## <a name="publish-to-nugetorg"></a>nuget.org yayınlayın

nuget.org için, hesabı nuget.org kaydettirmeniz istenecek bir Microsoft hesabıyla oturum açmanız gerekir. Portalın eski sürümleri kullanılarak oluşturulan nuget.org bir hesapla da oturum açabilirsiniz.

![NuGet konumunda oturum aç](media/publish_NuGetSignIn.png)

Ardından, paketi nuget.org web portalı üzerinden yükleyebilir, komut satırından nuget.org'a itebilir `nuget.exe` (4.1.0+) veya aşağıdaki bölümlerde açıklandığı gibi Azure DevOps Hizmetleri aracılığıyla CI/CD işleminin bir parçası olarak yayımlayabilirsiniz.

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a>Web portalı: nuget.org'daki Yükleme Paketi sekmesini kullanın

1. nuget.org üst menüsünden **Yükle'yi** seçin ve paket konumuna göz atın.

    ![nuget.org'da paket yükleyin](media/publish_UploadYourPackage.PNG)

1. nuget.org paket adının kullanılabilir olup olmadığını söyler. Değilse, projenizdeki paket tanımlayıcısını değiştirin, yeniden yeniden oluşturun ve yüklemeyi yeniden deneyin.

1. Paket adı varsa, nuget.org paket bildiriminden meta verileri gözden geçirebileceğiniz bir **Doğrula** bölümünü açar. Meta verilerden herhangi birini değiştirmek için projenizi `.nuspec` (proje dosyası veya dosya) edin, yeniden oluşturun, paketi yeniden oluşturun ve yeniden yükleyin.

1. **Belgeyi Aktar'ın** altında Markdown'u yapıştırabilir, dokümanlarınızı BIR URL ile işaret edebilir veya bir belge dosyası yükleyebilirsiniz.

1. Tüm bilgiler hazır olduğunda Gönder **düğmesini** seçin

### <a name="command-line"></a>Komut satırı

Paketleri nuget.org itmek için gerekli [NuGet protokollerini](../api/nuget-protocols.md)uygulayan [nuget.exe v4.1.0 veya üzeri](https://www.nuget.org/downloads)nikullanmalısınız. Ayrıca, nuget.org'da oluşturulan bir API anahtarına da ihtiyacınız var.

#### <a name="create-api-keys"></a>API tuşlarını oluşturma

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a>dotnet nuget push ile yayımla

[!INCLUDE [publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a>Nuget push ile yayımla

1. Komut isteminde, nuget.org elde edilen `<your_API_key>` anahtarı değiştirerek aşağıdaki komutu çalıştırın:

    ```cli
    nuget setApiKey <your_API_key>
    ```

    Bu komut, API anahtarınızı NuGet yapılandırmanızda saklar, böylece bu adımı aynı bilgisayarda tekrarlamanız gerekmez.

    > [!NOTE]
    > API anahtarı, özel beslemeyle kimlik doğrulaması için kullanılmaz. Kaynakla kimlik doğrulaması için kimlik bilgilerini yönetmek için [ `nuget sources` komuta](../reference/cli-reference/cli-ref-sources.md) bakın.
    > API anahtarları tek tek NuGet sunucularından elde edilebilir. nuget.org için APIKeys oluşturmak ve manange için [publish-api-key](../quickstart/includes/publish-api-key.md) bakın

1. Aşağıdaki komutu kullanarak paketinizi NuGet Galerisi'ne itin:

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

#### <a name="publish-signed-packages"></a>İmzalı paketleri yayımlama

İmzalı paketleri göndermek için, önce paketleri imzalamak için kullanılan [sertifikayı kaydetmeniz](../create-packages/Sign-a-Package.md#register-the-certificate-on-nugetorg) gerekir. 

> [!Warning]
> nuget.org, [imzalanan paket gereksinimlerini](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg)karşılamayan paketleri reddeder.

### <a name="package-validation-and-indexing"></a>Paket doğrulama ve dizin oluşturma

nuget.org itilen paketler virüs denetimleri gibi çeşitli doğrulamalara tabi dir. (nuget.org üzerindeki tüm paketler periyodik olarak taranır.)

Paket tüm doğrulama denetimlerini geçtiğinde, dizine ekleştirilmesi ve arama sonuçlarında görünmesi biraz zaman alabilir. Dizin oluşturma tamamlandıktan sonra, paketin başarıyla yayımlandığını onaylayan bir e-posta alırsınız. Paket doğrulama denetiminde başarısız olursa, paket ayrıntıları sayfası ilişkili hatayı görüntülemek için güncellenir ve ayrıca bu konuda size bildiren bir e-posta alırsınız.

Paket doğrulama ve dizin oluşturma genellikle 15 dakikanın altında sürer. Paket yayımlama beklenenden uzun sürüyorsa, nuget.org herhangi bir kesinti yaşanıp yaşanmayacağını kontrol etmek için [status.nuget.org](https://status.nuget.org/) ziyaret edin. Tüm sistemler çalışır durumdaysa ve paket bir saat içinde başarıyla yayınlanmamışsa, lütfen nuget.org giriş yapın ve paket sayfasındaki Destek Bağlantısını kullanarak bizimle iletişime geçin.

Paketin durumunu görmek için, nuget.org'da hesap adınız altında **paketleri yönet'i** seçin. Doğrulama tamamlandığında bir onay e-postası alırsınız.

Paketinizin dizine eksinin eklenmesinin biraz zaman alacağını ve başkalarının bulabileceği arama sonuçlarında görünmesinin biraz zaman alacağını ve bu süre zarfında paket sayfanızda aşağıdaki iletiyi görebileceğinizi unutmayın:

![Paketin henüz yayımlanmadığını belirten ileti](media/publish_NotYetIndexed.png)

### <a name="azure-devops-services-cicd"></a>Azure Devops Hizmetleri (CI/CD)

Sürekli Tümleştirme/Dağıtım işleminizin bir parçası olarak Azure DevOps Hizmetlerini kullanarak `nuget.exe` paketleri nuget.org iterseniz, NuGet görevlerinde 4.1 ve üzerini kullanmanız gerekir. Ayrıntılar, [yapınızdaki en son NuGet'i](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blogu) kullanma hakkında bulunabilir.

## <a name="managing-package-owners-on-nugetorg"></a>paket sahiplerini nuget.org

Her NuGet paketinin `.nuspec` dosyası paketin yazarlarını tanımlasa da, nuget.org galerisi sahipliği tanımlamak için bu meta verileri kullanmaz. Bunun yerine, nuget.org paketi yayımlayan kişiye ilk sahipliği atar. Bu, paketi kullanıcı nuget.org Kullanıcı Arama Birimi üzerinden yükleyen oturum açmış kullanıcı veya API `nuget SetApiKey` `nuget push`anahtarı nın kullanıldığı kullanıcılar veya.

Tüm paket sahipleri, diğer sahiplerin eklenmesi ve kaldırılması ve güncelleştirmelerin yayımlanması da dahil olmak üzere paket için tam izinlere sahiptir.

Bir paketin sahipliğini değiştirmek için aşağıdakileri yapın:

1. Paketin geçerli sahibi olan hesapla nuget.org oturum açın.
1. Hesap adınızı seçin, **Paketleri Yönet'i**seçin ve **Yayınlanan Paketleri genişletin.**
1. Yönetmek istediğiniz pakette seçin, ardından sağ tarafta **sahipleri yönet'i**seçin.

Buradan birkaç seçeneğiniz var:

1. **Geçerli Sahipler**altında listelenen tüm sahibi kaldırın.
1. Kullanıcı adını, bir iletiyi girerek ve **Ekle'yi**seçerek **Sahibi Ekle'nin** altına bir sahip ekle. Bu eylem, onay bağlantısı olan yeni ortak sahibine bir e-posta gönderir. Onaylandıktan sonra, bu kişinin sahiplerini eklemek ve kaldırmak için tam izinleri vardır. (Onaylanana kadar, **Geçerli Sahipler** bölümü o kişinin onayını beklemede olduğunu gösterir.)
1. Sahipliği aktarmak için (sahiplik değiştiğinde veya bir paket yanlış hesap altında yayınlandığında olduğu gibi), yeni sahibi ekleyin ve sahipliği onayladıktan sonra sizi listeden kaldırabilirler.

Bir şirkete veya gruba sahiplik atamak için, ilgili ekip üyelerine iletilen bir e-posta takma adını kullanarak bir nuget.org hesabı oluşturun. Örneğin, çeşitli Microsoft ASP.NET paketleri, yalnızca bu tür diğer adları içeren [microsoft](https://nuget.org/profiles/microsoft) ve [aspnet](https://nuget.org/profiles/aspnet) hesaplarına aittir.

### <a name="recovering-package-ownership"></a>Paket sahipliğini kurtarma

Bazen, bir paketin etkin bir sahibi olmayabilir. Örneğin, özgün sahibi paketi üreten şirketten ayrılmış olabilir, kimlik bilgilerinin kaybolmasına nuget.org veya galerideki önceki hatalar paket sahibiz bırakılmış olabilir.

Bir paketin gerçek sahibiyseniz ve sahipliğini yeniden kazanmanız gerekiyorsa, durumunuzu NuGet ekibine açıklamak için nuget.org'daki [iletişim formunu](https://www.nuget.org/policies/Contact) kullanın. Daha sonra, paketin Proje URL'si, Twitter, e-posta veya diğer yollarla mevcut sahibini bulmaya çalışmak da dahil olmak üzere paketin sahipliğini doğrulamak için bir işlem uygularız. Ama her şey başarısız olursa, sana yeni bir davet gönderebiliriz.
