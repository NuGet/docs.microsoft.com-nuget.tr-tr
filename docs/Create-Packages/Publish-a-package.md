---
title: Bir NuGet Paketi Yayımlama | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/19/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Ayrıntılı yönergeler için NuGet paketi nuget.org veya özel akışları yayımlama ve nuget.org paket sahipliği yönetme.
keywords: NuGet Paketi Yayımlama NuGet paketi, NuGet paketinin sahipliği yayınlamak için NuGet akışlarını nuget.org, özel yayımlama
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 68db25276297353fab03258adecd9169149dbe51
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="publishing-packages"></a>Paketleri yayımlama

Bir paketi oluşturup sahip sonra `.nukpg` ele dosya, diğer geliştiriciler için genel veya özel olarak kullanılabilmesi için basit bir işlemdir:

- Ortak paketleri kullanılabilir hale getirilir tüm geliştiriciler için genel ile [nuget.org](https://www.nuget.org/packages/manage/upload) (NuGet 4.1.0+ gerektirir) Bu makalede anlatıldığı gibi.
- Özel paketler yalnızca bir ekip veya kuruluş, kullanılabilir ya da bir dosya paylaşımı, özel bir NuGet sunucu barındırarak [Visual Studio Team Services paket Yönetimi](https://www.visualstudio.com/docs/package/nuget/publish), veya bir üçüncü taraf deposu myget, ProGet, Nexus gibi Depo ve Artifactory. Daha fazla bilgi için bkz: [barındırma paketleri genel bakış](../hosting-packages/overview.md).

Bu makale nuget.org yayımlamayı kapsamaktadır; Visual Studio Team Services yayımlama için bkz: [paket Yönetimi](https://www.visualstudio.com/docs/package/nuget/publish).

## <a name="publish-to-nugetorg"></a>Nuget.org için yayımlama

Nuget.org için hangi hesabın nuget.org ile kaydetmek için istenir, bir Microsoft hesabıyla oturum gerekir. Portal eski sürümleri kullanılarak oluşturulan bir nuget.org hesabıyla oturum.

![NuGet oturum açma konumu](media/publish_NuGetSignIn.png)

Ardından, ya da nuget.org web portalı üzerinden paketini karşıya yükleyin, yapabilirsiniz nuget.org için komut satırından itme (gerektirir `nuget.exe` 4.1.0+), ya da Visual Studio Team Services aracılığıyla CI/CD işleminin parçası olarak aşağıdaki bölümlerde açıklandığı gibi yayımlayın.

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a>Web portalı: nuget.org üzerinde karşıya yükleme paketini sekmesini kullanın

1. Seçin **karşıya** üst menüsünde nuget.org ve paket konumuna göz atın.

    ![Nuget.org paketin karşıya yükle](media/publish_UploadYourPackage.PNG)

1. nuget.org paket adı olup olmadığını bildirir. Değil değiştirirseniz, projenizdeki paket tanımlayıcısı yeniden oluşturun ve karşıya yüklemeyi yeniden deneyin.

1. Paket adı olup olmadığını nuget.org açılır bir **doğrula** bölüm içinde gözden geçirebileceğiniz paket bildirimi meta verileri. Meta veri değişiklik yapmak için projenizin Düzenle (proje dosyası veya `.nuspec` dosyası) yeniden, paketi yeniden oluşturun ve yeniden yükleyin.

1. Altında **alma belgelerine** Markdown yapıştırın, bir URL ile belgelerinizi noktasına veya bir belge dosyasını karşıya yükleyin.

1. Tüm bilgileri hazır olduğunda seçme **gönderme** düğmesi

### <a name="command-line"></a>Komut satırı

Anında iletme paketlere kullanmalısınız nuget.org için [nuget.exe v4.1.0 veya yukarıdaki](https://www.nuget.org/downloads), gerekli uygulayan [NuGet protokolleri](../api/nuget-protocols.md). Ayrıca nuget.org üzerinde oluşturulan bir API anahtarı gerekir.

#### <a name="create-api-keys"></a>API anahtarları oluşturma

[!INCLUDE[publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a>DotNet nuget itme ile yayımlama

[!INCLUDE[publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a>Nuget itme ile yayımlama

1. Bir komut isteminde aşağıdaki komutu çalıştırın komutu, değiştirme `<your_API_key>` nuget.org elde edilen anahtar ile:

    ```cli
    nuget setApiKey <your_API_key>
    ```

    Bu komut, API anahtarınıza NuGet yapılandırmanızda depolar aynı bilgisayarda bu adımı yineleyin.

1. Paketinizi NuGet galerisinde aşağıdaki komutu kullanarak gönderin:

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

### <a name="package-validation-and-indexing"></a>Paket doğrulama ve dizin oluşturma

Nuget.org için gönderilen paketleri virüs denetimleri gibi birkaç doğrulamaları geçer. (Nuget.org tüm paketleri düzenli aralıklarla taranır.)

biçimindeki telefon numarasıdır. Paketin tüm doğrulama denetimlerini geçtiğinde, sıralanması ve arama sonuçlarında görüntülenmesini biraz sürebilir. Dizin oluşturma işlemi tamamlandıktan sonra paketi başarıyla yayımlandı onaylayan bir e-posta alırsınız. Paket doğrulama denetimi başarısız olursa, ilgili hatayı görüntülemek için Paket ayrıntılarını sayfa güncelleştirilir ve ayrıca hakkında bildiren bir e-posta alırsınız.

Paket doğrulama ve dizin oluşturma altında 15 dakika genellikle alır. Paket yayımlama beklenenden daha uzun sürüyorsa, ziyaret [status.nuget.org](https://status.nuget.org/) nuget.org tüm kesintileri yaşayan varsa denetlemek için. Tüm sistemler işletimsel ve paket bir saat içinde başarıyla yayımlanmadı, lütfen nuget.org oturum açın ve paket sayfasında kişi destek bağlantısı kullanarak bizimle bağlantı kurun.

Bir paketin durumunu görmek için seçin **paketlerini yönetmek** hesap adınızı nuget.org üzerinde altında. Doğrulama tamamlandıktan sonra bir onay e-posta alırsınız.

Dizine ve diğerleri, hangi sırada paket sayfanızda aşağıdaki iletiyi görürsünüz bulabileceğiniz bir yerde arama sonuçlarında görüntülenmesini paketinizi biraz sürebilir dikkat edin:

![Bir paket henüz yayımlanmadı belirten iletisi](media/publish_NotYetIndexed.png)

### <a name="visual-studio-team-services-cicd"></a>Visual Studio Team Services (CI/CD)

Paketleri nuget.org sürekli tümleştirme/dağıtım işleminin bir parçası Visual Studio Team Services kullanarak anında iletme, kullanmalısınız `nuget.exe` 4.1 veya yukarıdaki NuGet görevler. Ayrıntılar bulunabilir [yapı içinde son NuGet kullanarak](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blogu).

## <a name="managing-package-owners-on-nugetorg"></a>Nuget.org üzerinde paket sahiplerini yönetme

Ancak her NuGet paketin `.nuspec` dosyası paketin yazarlar tanımlar, nuget.org galeri meta verilerin sahipliği tanımlamak için kullanmaz. Bunun yerine, nuget.org ilk sahipliği paketi yayımlar kişiye atar. Bu paket nuget.org kullanıcı Arabirimi aracılığıyla karşıya oturum açan kullanıcının ya da, API anahtarı ile kullanıldı kullanıcılar olan `nuget SetApiKey` veya `nuget push`.

Tüm paket sahipleri paket ekleme ve kaldırma diğer sahipleri ve güncelleştirmeleri yayımlama da dahil olmak üzere, tam izinlere sahip.

Bir paket sahipliğini değiştirmek için aşağıdakileri yapın:

1. Nuget.org paketinin geçerli sahibi olan hesap ile oturum açın.
1. Hesap adınızı seçin, **paketlerini yönetmek**ve genişletin **yayımlanan paketleri**.
1. Yönetmek istediğiniz paketi seçin, sonra sağ tarafta seçin **sahiplerini yönetme**.

Buradan, birkaç seçeneğiniz vardır:

1. Altında listelenen sahip kaldırmak **geçerli sahipleri**.
1. Bir sahip altında eklemek **eklemek sahibi** kullanıcı adı, bir ileti girme ve seçerek **Ekle**. Bu eylem, yeni ikincil sahip bir onay bağlantısı ile bir e-posta gönderir. Onaylandıktan sonra o kişiyi eklemek ve sahipleri kaldırmak için tam izinleri vardır. (Onaylandı kadar **geçerli sahipleri** bu kişi için onay bekleyen bölümü gösterir.)
1. (Olarak ne zaman sahipliği değişiklikleri veya bir paket yanlış hesabı altında yayımlanan) sahipliğini aktarma için yeni sahibin ekleyin ve sahipliği onaylanıp sonra bunlar, listeden kaldırabilirsiniz.

Bir şirket veya grup sahipliği atamak için uygun ekip üyelerine iletilen bir e-posta diğer adı kullanarak bir nuget.org hesabı oluşturun. Örneğin, çeşitli Microsoft ASP.NET paketleri birlikte sahibi [microsoft](http://nuget.org/profiles/microsoft) ve [aspnet](http://nuget.org/profiles/aspnet) hesapları, hangi yalnızca gibi diğer adları.

### <a name="recovering-package-ownership"></a>Paket sahipliği kurtarma

Bazen, bir paket etkin bir sahip olmayabilir. Örneğin, özgün sahibinin paket üreten şirket bıraktıysanız, nuget.org kimlik bilgileri kaybolur veya galerisinde önceki hataların bir paket ownerless sol.

Bir paketin gerçek sahibiyseniz ve sahipliği kazanmaya ihtiyacınız varsa kullanmak [kişi formu](https://www.nuget.org/policies/Contact) açıklayan NuGet takım durumunuza nuget.org üzerinde. Biz sonra varolan sahibi paketin proje URL'sini, Twitter, e-posta veya başka yöntemler aracılığıyla bulmaya çalışan dahil olmak üzere paketin, sahipliği doğrulamak için bir işlemi izleyin. Ancak tüm yöntemler başarısız olursa, sahibi olmak için yeni bir davet gönderebiliriz.
