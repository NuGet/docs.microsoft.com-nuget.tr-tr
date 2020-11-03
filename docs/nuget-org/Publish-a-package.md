---
title: NuGet paketi yayımlama
description: Bir NuGet paketini nuget.org veya özel akışlara yayımlama ve nuget.org üzerinde paket sahipliğini yönetme hakkında ayrıntılı yönergeler.
author: karann-msft
ms.author: karann
ms.date: 05/18/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: fe5625247dca51c10d82fffe82022c40a4716069
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237938"
---
# <a name="publishing-packages"></a>Paketler yayımlanıyor

Bir paket oluşturduktan ve dosyanızı el ile oluşturduktan sonra `.nupkg` , bu, diğer geliştiricilerin herkese açık veya özel olarak kullanılabilmesini sağlamak için basit bir işlemdir:

- Ortak paketler, bu makalede açıklandığı gibi [NuGet.org](https://www.nuget.org/packages/manage/upload) aracılığıyla genel olarak tüm geliştiriciler tarafından kullanılabilir hale getirilir (NuGet 4.1.0 + gerektirir).
- Özel paketler, bir dosya paylaşımında, özel bir NuGet sunucusunda, [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish)veya Myget, Proal, Nexus deposu ve Artifactory gibi üçüncü taraf depolardan yararlanarak yalnızca bir ekip veya kuruluş tarafından kullanılabilir. Ek ayrıntılar için bkz. [barındırma paketlerine genel bakış](../hosting-packages/overview.md).

Bu makalede, nuget.org ' a yayımlama ele alınmaktadır. Azure Artifacts yayımlamak için bkz. [Paket Yönetimi](https://www.visualstudio.com/docs/package/nuget/publish).

## <a name="publish-to-nugetorg"></a>Nuget.org 'e Yayımla

Nuget.org için Microsoft hesabı ile oturum açmanız gerekir, bu, hesabı nuget.org ile kaydetmeniz istenecektir.

![NuGet oturum açma konumu](media/publish_NuGetSignIn.png)

Daha sonra, nuget.org Web portalı aracılığıyla paketi karşıya yükleyebilir, komut satırından nuget.org 'e gönderebilir ( `nuget.exe` 4.1.0 + gerektirir) veya aşağıdaki bölümlerde açıklandığı gibi Azure DevOps Services aracılığıyla BIR CI/CD işleminin parçası olarak yayımlayabilirsiniz.

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a>Web Portalı: nuget.org 'de paket yükle sekmesini kullanın

1. Nuget.org üst menüsünde **karşıya yükle** ' yi seçin ve paket konumuna gidin.

    ![Nuget.org 'de paket yükleme](media/publish_UploadYourPackage.PNG)

1. nuget.org, paket adının kullanılabilir olup olmadığını söyler. Değilse, projenizdeki paket tanımlayıcısını değiştirin, yeniden derleyin ve karşıya yüklemeyi yeniden deneyin.

1. Paket adı kullanılabiliyorsa nuget.org, paket bildiriminden meta verileri gözden geçirebilmeniz için bir **doğrulama** bölümü açar. Meta verileri değiştirmek için projenizi (proje dosyası veya dosyası) düzenleyin, yeniden `.nuspec` derleyin, paketi yeniden oluşturun ve tekrar yükleyin.

1. **Belgeleri Içeri aktar** ' ın altında markaşağı yapıştırabilir, bir URL ile belgelerinize işaret edebilir veya bir belge dosyası yükleyebilirsiniz.

1. Tüm bilgiler hazırlanıyor, **Gönder** düğmesini seçin

### <a name="command-line"></a>Komut satırı

Paketleri nuget.org 'e göndermek için, önce nuget.org üzerinde oluşturulan bir API anahtarına ihtiyacınız vardır. Gerekli NuGet protokollerini uygulayan dotnet.exe (.NET Core) veya nuget.exe v 4.1.0 ya da üstünü kullanmanız gerekir.
Daha fazla bilgi için bkz. [.NET Core](/dotnet/core/install/), [nuget.exe](https://www.nuget.org/downloads)ve [NuGet protokolleri](../api/nuget-protocols.md).

#### <a name="create-api-keys"></a>API anahtarları oluşturma

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a>DotNet NuGet Push ile yayımlama

[!INCLUDE [publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a>NuGet Push ile yayımlama

1. Komut isteminde, `<your_API_key>` NuGet.org adresinden elde edilen anahtarla değiştirerek aşağıdaki komutu çalıştırın:

    ```cli
    nuget setApiKey <your_API_key>
    ```

    Bu komut, API anahtarınızı NuGet yapılandırmanızda depolar, böylece bu adımı aynı bilgisayarda tekrar yinelemeniz gerekmez.

    > [!NOTE]
    > API anahtarı özel akışta kimlik doğrulaması için kullanılmaz. Kaynak ile kimlik doğrulaması için kimlik bilgilerini yönetmek üzere [ `nuget sources` komutuna](../reference/cli-reference/cli-ref-sources.md) bakın.
    > Tek bir NuGet sunucusundan API anahtarları elde edilebilir. Nuget.org için APIKeys oluşturmak ve sağlamak için [API anahtarları oluşturma](#create-api-keys)bölümüne bakın.

1. Aşağıdaki komutu kullanarak paketinizi NuGet galerisine gönderin:

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

#### <a name="publish-signed-packages"></a>İmzalı paketleri yayımlama

İmzalı paketleri göndermek için, önce paketleri imzalamak üzere kullanılan [sertifikayı kaydetmeniz](../create-packages/Sign-a-Package.md#register-the-certificate-on-nugetorg) gerekir. 

> [!Warning]
> nuget.org, [İmzalı paket gereksinimlerini](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg)karşılamayan paketleri reddeder.

### <a name="package-validation-and-indexing"></a>Paket doğrulama ve dizin oluşturma

Paketler, virüs denetimleri gibi çeşitli doğrulamaları nuget.org 'e gönderdi. (Nuget.org üzerindeki tüm paketler düzenli aralıklarla taranır.)

Paket tüm doğrulama denetimlerini geçtiğinde, dizin oluşturulması ve arama sonuçlarında görünmesi biraz zaman alabilir. Dizin oluşturma işlemi tamamlandıktan sonra, paketin başarıyla yayımlandığını onaylayan bir e-posta alırsınız. Paket bir doğrulama denetiminden başarısız olursa, paket ayrıntıları sayfası ilgili hatayı görüntüleyecek şekilde güncellenecek ve size bir e-posta gönderilir.

Paket doğrulama ve dizin oluşturma genellikle 15 dakika boyunca sürer. Paket yayımlaması beklenenden uzun sürüyorsa, nuget.org 'in herhangi bir kesinti yaşamadığını denetlemek için [Status.NuGet.org](https://status.nuget.org/) adresini ziyaret edin. Tüm sistemler çalışır durumda ve paket bir saat içinde başarıyla yayımlanmamışsa, lütfen nuget.org ' e oturum açın ve paket sayfasındaki desteğe başvurun bağlantısını kullanarak bizimle iletişime geçin.

Bir paketin durumunu görmek için nuget.org adresindeki hesap adınızın altındaki **paketleri Yönet** ' i seçin. Doğrulama tamamlandığında bir onay e-postası alırsınız.

Paketinizin dizine alınması ve başkalarının bulabileceği arama sonuçlarında görünmesi biraz zaman alabilir ve bu durumda paket sayfanızda aşağıdaki iletiyi görürsünüz:

![Bir paketin henüz yayımlanmadığını belirten ileti](media/publish_NotYetIndexed.png)

### <a name="azure-devops-services-cicd"></a>Azure DevOps Services (CI/CD)

Sürekli tümleştirme/dağıtım işleminizin bir parçası olarak Azure DevOps Services kullanarak paketler nuget.org 'e gönderim yaparsanız, `nuget.exe` NuGet görevlerinde 4,1 veya üzeri bir sürümü kullanmanız gerekir. Ayrıntılar [, derlemede en son NuGet](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blogu) kullanılarak bulunabilir.

## <a name="managing-package-owners-on-nugetorg"></a>Nuget.org üzerinde paket sahiplerini yönetme

Her NuGet paketinin `.nuspec` dosyası paketin yazarlarını tanımlasa da, NuGet.org Galerisi bu meta verileri sahipliğini tanımlamak için kullanmaz. Bunun yerine nuget.org, paketi yayımlayan kişiye ilk sahiplik atar. Bu, paketi nuget.org kullanıcı arabiriminden yükleyen oturum açmış bir kullanıcı veya API anahtarı veya ile kullanılan kullanıcıları ya da `nuget SetApiKey` `nuget push` .

Tüm paket sahipleri, diğer sahipleri ekleme ve kaldırma ve güncelleştirme yayımlama dahil olmak üzere paket için tam izinlere sahiptir.

Bir paketin sahipliğini değiştirmek için aşağıdakileri yapın:

1. Nuget.org 'de paketin geçerli sahibi olan hesapla oturum açın.
1. Hesap adınızı seçin, **paketleri Yönet** ' i seçin ve **yayımlanan paketler** ' i genişletin.
1. Yönetmek istediğiniz paketi seçin, ardından sağ tarafta **sahipleri Yönet** ' i seçin.

Buradan çeşitli seçenekleriniz vardır:

1. **Geçerli sahipler** altında listelenen tüm sahipleri kaldırın.
1. Kullanıcı adını, bir iletiyi girerek ve **Ekle** ' yi seçerek **sahip Ekle** altına bir sahip ekleyin. Bu eylem, bu yeni ortak Sahibe onay bağlantısı ile bir e-posta gönderir. Onaylandıktan sonra, bu kişinin sahipleri eklemek ve kaldırmak için tam izinleri vardır. (Onaylanana kadar, **geçerli sahipler** bölümü söz konusu kişi için bekleyen onay olduğunu gösterir.)
1. Sahipliği aktarmak için (sahiplik değişiklikleri veya bir paket yanlış hesap altında yayımlandığında olduğu gibi), yeni sahibi ekleyin ve sahipliği onayladıktan sonra listeden kaldırabilir.

Bir şirkete veya gruba sahiplik atamak için, uygun takım üyelerine iletilen bir e-posta diğer adı kullanarak bir nuget.org hesabı oluşturun. Örneğin, çeşitli Microsoft ASP.NET paketleri [Microsoft](https://nuget.org/profiles/microsoft) ve [ASPNET](https://nuget.org/profiles/aspnet) hesaplarına aittir, bu da yalnızca diğer adlar vardır.

### <a name="recovering-package-ownership"></a>Paket sahipliği kurtarılıyor

Bazen bir paket etkin bir sahibe sahip olmayabilir. Örneğin, özgün sahip, paketi üreten şirketi bıraktı, nuget.org kimlik bilgileri kayboluyor veya galerideki daha önceki hatalar bir paket sahipi bıraktı.

Bir paketin sağtasyon sahibiyseniz ve sahipliği yeniden kazanmak istiyorsanız, nuget.org adresindeki [iletişim formunu](https://www.nuget.org/policies/Contact) kullanarak, durumunuzu NuGet ekibine açıklayın. Daha sonra paketin sahipliğini doğrulamak için, paketin proje URL 'SI, Twitter, e-posta veya başka yollarla mevcut sahibini bulmaya çalışmak de dahil olmak üzere bir işlemi izliyoruz. Ancak diğerleri başarısız olursa, size sahip olmaya yönelik yeni bir davet gönderebiliriz.
