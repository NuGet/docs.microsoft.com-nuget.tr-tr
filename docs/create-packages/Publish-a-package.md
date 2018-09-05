---
title: Bir NuGet Paketi Yayımlama
description: Nuget.org veya özel akışları için bir NuGet Paketi Yayımlama ve nuget.org üzerinde paket sahipliği yönetme konusunda ayrıntılı yönergeler.
author: karann-msft
ms.author: karann
ms.date: 05/18/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: bd36ae311da1ec824726c5d73670b1232a3f89e0
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549592"
---
# <a name="publishing-packages"></a>Paket yayımlama

Bir paket oluşturup sahip, `.nupkg` ele dosya, diğer geliştiriciler için genel veya özel olarak kullanılabilmesi için basit bir işlemdir:

- Genel paketleri kullanılabilir hale gelir tüm geliştiricilere genel ile [nuget.org](https://www.nuget.org/packages/manage/upload) (NuGet 4.1.0+ gerektirir) Bu makalede açıklandığı gibi.
- Özel paketler yalnızca bir ekip veya kuruluşlar için kullanılabilir ya da dosya paylaşımı için bir özel NuGet sunucusu barındırarak [Visual Studio Team Services paket Yönetimi](https://www.visualstudio.com/docs/package/nuget/publish), veya myget, ProGet, Nexus gibi bir üçüncü taraf depo Depo ve Artifactory. Ek ayrıntılar için bkz. [barındırma paketleri genel bakış](../hosting-packages/overview.md).

Bu makalede nuget.org yayımlama kapsar; Visual Studio Team Services yayımlama için bkz: [paket Yönetimi](https://www.visualstudio.com/docs/package/nuget/publish).

## <a name="publish-to-nugetorg"></a>Nuget.org için yayımlama

Nuget.org için birlikte, hesap nuget.org ile kaydetmek için istenir, bir Microsoft hesabıyla oturum açmanız gerekir. Ayrıca portalı eski sürümleri kullanılarak oluşturulan bir nuget.org hesabıyla kaydolabilirsiniz.

![NuGet oturum konumda](media/publish_NuGetSignIn.png)

Ardından, ya da nuget.org web Portalı aracılığıyla paketini karşıya yükleyin, komut satırından nuget.org için anında iletme (gerektirir `nuget.exe` 4.1.0+), veya Visual Studio Team Services ile CI/CD işleminin bir parçası olarak aşağıdaki bölümlerde açıklandığı şekilde yayımlayabilirsiniz.

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a>Web portalı: Paket karşıya sekmesinde nuget.org adresinden kullanın

1. Seçin **karşıya** en üstteki menüde nuget.org ve paket konumuna göz atın.

    ![Nuget.org üzerindeki bir paket karşıya yükleme](media/publish_UploadYourPackage.PNG)

1. nuget.org paket adı kullanılabilir olup olmadığını söyler. Değilse değiştirirseniz, projenizdeki paket tanımlayıcısı yeniden oluşturun ve karşıya yüklemeyi yeniden deneyin.

1. Paket adı varsa, nuget.org açılır bir **doğrulama** içinde gözden geçirebileceğiniz paket bildirimi meta verileri bölümü. Meta verileri değiştirmek için projenizi Düzenle (proje dosyası veya `.nuspec` dosyası), yeniden, paketi yeniden oluşturun ve yeniden yükleyin.

1. Altında **alma belgeleri** Markdown yapıştırın, bir URL ile belgelerinizi noktasına veya belgeleri dosyasını karşıya yükleyin.

1. Tüm bilgileri hazır olduğunda seçin **Gönder** düğmesi

### <a name="command-line"></a>Komut satırı

Anında iletme paketlerine nuget.org'da kullanmalısınız [nuget.exe verze 4.1.0 veya üzeri](https://www.nuget.org/downloads), gerekli uygulayan [NuGet protokolleri](../api/nuget-protocols.md). Nuget.org üzerinde oluşturulan bir API anahtarı da gerekir.

#### <a name="create-api-keys"></a>API anahtarları oluşturma

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a>DotNet nuget itme ile yayımlama

[!INCLUDE [publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a>Nuget itme ile yayımlama

1. Bir komut isteminde aşağıdaki komutu çalıştırın. komut, değiştirme `<your_API_key>` nuget.org adresinden aldığınız anahtarını ile:

    ```cli
    nuget setApiKey <your_API_key>
    ```

    Bu komut, API anahtarınızı NuGet yapılandırmanızda saklar, böylece aynı bilgisayarda bu adımı yinelemeniz.

1. Paketiniz, aşağıdaki komutu kullanarak NuGet Galerisine gönderin:

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

#### <a name="publish-signed-packages"></a>İmzalanmış paketleri yayımlama

İmzalanmış paketleri göndermek için önce [sertifika kaydettirir](../reference/Signed-Packages-Reference.md#register-certificate-on-nugetorg) paketleri imzalamak için kullanılır. 

> [!Warning]
> nuget.org reddeder karşılamayan paketleri [paket gereksinimleri imzalı](../reference/Signed-Packages-Reference.md#signature-requirements-on-nugetorg).

### <a name="package-validation-and-indexing"></a>Paket doğrulaması ve dizin oluşturma

Nuget.org için gönderilen paketleri virüs denetimleri gibi çeşitli doğrulamaları geçeriz. (Tüm paketleri nuget.org üzerinde düzenli aralıklarla taranır.)

biçimindeki telefon numarasıdır. Paket tüm doğrulama denetimlerini geçtiğinde, sıralanması ve arama sonuçlarında görüntülenmesi için biraz sürebilir. Dizin oluşturma tamamlandıktan sonra paketi başarıyla yayımlandı onaylayan bir e-posta alırsınız. Paket doğrulama denetimi başarısız olursa, Paket Ayrıntıları sayfasına ilgili hatayı görüntülemek için güncelleştirir ve aynı zamanda bunu bildiren bir e-posta alırsınız.

Paket doğrulaması ve dizin oluşturma genellikle 15 dakika alır. Paket yayımlama beklenenden daha uzun sürerse ziyaret [status.nuget.org](https://status.nuget.org/) nuget.org herhangi bir kesinti yaşıyor olmadığını denetlemek için. Tüm sistemler çalışır durumda ve paket başarıyla bir saat içinde yayımlanmadı Lütfen nuget.org için oturum açın ve paket sayfasında kişi destek bağlantısı kullanarak bize ulaşın.

Paketin durumunu görmek için seçin **paketleri yönetme** nuget.org hesap adınızın altında. Doğrulama tamamlandığında bir onay e-posta alırsınız.

Dizine ve başkalarının hangi sırada paket sayfanızda aşağıdaki iletiyi görürsünüz, nerede bulabileceğiniz arama sonuçlarında görünmesini paketinizi biraz sürebilir dikkat edin:

![Bir paket henüz yayımlanmadı belirten ileti.](media/publish_NotYetIndexed.png)

### <a name="visual-studio-team-services-cicd"></a>Visual Studio Team Services (CI/CD)

Paketleri nuget.org Visual Studio Team Services kullanarak sürekli tümleştirme/dağıtım işleminizin bir parçası olarak gönderirseniz kullanmalısınız `nuget.exe` 4.1 veya üzerini NuGet görevler. Ayrıntıları bulunabilir [derlemenizde en son NuGet kullanarak](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blogu).

## <a name="managing-package-owners-on-nugetorg"></a>Nuget.org paketinin sahiplerini yönetme

Ancak her NuGet paketi `.nuspec` dosyası tanımlar paketin yazarlar, nuget.org galeri meta verilerin sahipliği tanımlamak için kullanmaz. Bunun yerine, nuget.org ilk sahipliği paketi yayımlar kişiye atar. Paket nuget.org kullanıcı Arabirimi aracılığıyla karşıya oturum açmış kullanıcı veya API anahtarı ile kullanıldı kullanıcılar budur `nuget SetApiKey` veya `nuget push`.

Tüm paket sahipleri ekleme ve diğer sahipleri kaldırmak ve güncelleştirmelerini yayımlama da dahil olmak üzere paket için tam izinleri vardır.

Bir paket sahipliğini değiştirmek için aşağıdakileri yapın:

1. Nuget.org paketinin geçerli sahibi olan hesapla oturum açın.
1. Hesabınızın adını seçin, **paketleri yönetme**, genişletin **yayımlanmış paketleri**.
1. Yönetmek istediğiniz paketi seçin, sonra da sağ tarafta **sahiplerini yönetme**.

Burada birkaç seçeneğiniz vardır:

1. Altında listelenen herhangi bir sahibi kaldırma **geçerli sahipleri**.
1. Altında bir sahip ekleme **ekleme sahibi** kullanıcıların kullanıcı adı, bir ileti girme ve seçerek **Ekle**. Bu eylem, yeni ikincil sahip onayı bağlantısını içeren bir e-posta gönderir. Onaylandıktan sonra söz konusu kişinin eklemek ve sahipleri kaldırmak için tam izinlere sahiptir. (Onaylanana kadar **geçerli sahipleri** o kişinin onay bekleyen bölümü gösterir.)
1. (Zaman sahipliği değişiklikleri veya bir paket yanlış hesap altında yayımlanan) olarak sahipliğini devretmek için yeni sahibin ekleyin ve bunlar sahipliği onayladıktan sonra bunlar, listeden kaldırabilirsiniz.

Sahipliği bir şirket veya grup için atama için uygun takım üyelerine iletilen e-posta diğer adı kullanarak nuget.org hesabı oluşturun. Örneğin, çeşitli Microsoft ASP.NET paketler ortak sahibi [microsoft](http://nuget.org/profiles/microsoft) ve [aspnet](http://nuget.org/profiles/aspnet) hesapları, yalnızca tür diğer adları.

### <a name="recovering-package-ownership"></a>Paket sahipliği kurtarma

Bazen, bir paket etkin bir sahip olmayabilir. Örneğin, özgün sahibi paket hazırlayan şirket bırakmış olabilirsiniz, nuget.org kimlik bilgileri kaybolur veya önceki hatalar galerideki bir paket ownerless sol.

Bir paket gerçek sahibi ve sahipliğini yeniden elde etmek ihtiyacınız varsa, kullanmak [başvurun form](https://www.nuget.org/policies/Contact) nuget.org durumunuza NuGet ekibine açıklamak için. Biz sahipliğiniz paketin proje URL'si, e-posta, Twitter ya da başka araçlar aracılığıyla mevcut sahibi bulmaya çalışırken de dahil olmak üzere paketin doğrulamak için bir işlem daha sonra izleyin. Ancak, tüm denemeler başarısız olursa, biz sahibi olmak için yeni bir davet gönderebilirsiniz.
