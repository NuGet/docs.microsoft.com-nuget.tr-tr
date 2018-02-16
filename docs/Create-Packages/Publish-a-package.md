---
title: "Bir NuGet Paketi Yayımlama | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/05/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Ayrıntılı yönergeler için NuGet paketi nuget.org veya özel akışları yayımlama ve nuget.org paket sahipliği yönetme."
keywords: "NuGet Paketi Yayımlama NuGet paketi, NuGet paketinin sahipliği yayınlamak için NuGet akışlarını nuget.org, özel yayımlama"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: 610b20831b17ca5c1bae07546fde6eff3e2e43cc
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/14/2018
---
# <a name="publishing-packages"></a>Paketleri yayımlama

Bir paketi oluşturup sahip sonra `.nukpg` ele dosya, diğer geliştiriciler için genel veya özel olarak kullanılabilmesi için basit bir işlemdir:

- Ortak paketleri kullanılabilir hale getirilir tüm geliştiriciler için genel ile [nuget.org](https://www.nuget.org/packages/manage/upload) Bu konu başlığı altında açıklandığı gibi.
- Özel paketler yalnızca bir ekip veya kuruluş, kullanılabilir ya da bir dosya paylaşımı, özel bir NuGet sunucu barındırarak [Visual Studio Team Services paket Yönetimi](https://www.visualstudio.com/docs/package/nuget/publish), veya bir üçüncü taraf deposu myget, ProGet, Nexus gibi Depo ve Artifactory. Daha fazla bilgi için bkz: [barındırma paketleri genel bakış](../hosting-packages/overview.md).

Bu konu, nuget.org yayımlamayı kapsar; Visual Studio Team Services yayımlama için bkz: [paket Yönetimi](https://www.visualstudio.com/docs/package/nuget/publish).

## <a name="publish-to-nugetorg"></a>Nuget.org için yayımlama

Nuget.org için öncelikle [ücretsiz bir hesap için kayıt](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) veya zaten kayıtlı oturum açma:

![NuGet kayıt ve oturum açın. konumda](media/publish_NuGetSignIn.png)

Ardından, ya da nuget.org web portalı üzerinden paketini karşıya yükleyin, yapabilirsiniz nuget.org için komut satırından itme (gerektirir `nuget.exe` 4.1.0+), ya da Visual Studio Team Services aracılığıyla CI/CD işleminin parçası olarak aşağıdaki bölümlerde açıklandığı gibi yayımlayın.

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a>Web portalı: nuget.org üzerinde karşıya yükleme paketini sekmesini kullanın

![Bir paketi ile NuGet Paket Yöneticisi'ni yükleme](media/publish_UploadYourPackage.PNG)

### <a name="command-line"></a>Komut satırı

> [!Important]
> Anında iletme paketlere kullanmalısınız nuget.org için [nuget.exe v4.1.0 veya yukarıdaki](https://www.nuget.org/downloads), gerekli uygulayan [NuGet protokolleri](../api/nuget-protocols.md).

1. Hesap ayarlarınızı gitmek için kullanıcı adına tıklayın.
1. Altında **API anahtarı**, tıklatın **Panoya Kopyala** erişim almak için anahtar CLI gerekir:

    ![Hesap ayarlarından bir API anahtarını kopyalama](media/publish_APIKey.png)

1. Bir komut isteminde aşağıdaki komutu çalıştırın:

    ```cli
    nuget setApiKey Your-API-Key
    ```

    Bu adım aynı makinede yapmak böylece bu makinede API anahtarınıza depolar.

1. Paketinizi NuGet galerisinde komutu kullanarak gönderin:

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

1. Ortak yapılan önce tüm paketler için nuget.org karşıya virüs taraması ve herhangi bir virüs bulunursa reddetti. Nuget.org üzerinde listelenen tüm paketler de düzenli aralıklarla taranır.

1. Nuget.org üzerinde hesabınızı, tıklatın **my paketlerini yönetme** yeni bir görmek için yayımlanan; ayrıca bir onay e-postası. Dizine ve diğerleri, hangi sırada paket sayfanızda aşağıdaki iletiyi görürsünüz bulabileceğiniz bir yerde arama sonuçlarında görüntülenmesini paketinizi biraz sürebilir dikkat edin:

    ![Bir paket henüz dizine belirten iletisi](media/publish_NotYetIndexed.png)

### <a name="package-validation-and-indexing"></a>Paket doğrulama ve dizin oluşturma

NuGet.org için gönderilen paketleri birkaç doğrulamaları geçer. Paketin tüm doğrulama denetimlerini geçtiğinde, sıralanması ve arama sonuçlarında görüntülenmesini biraz sürebilir. Dizin oluşturma işlemi tamamlandıktan sonra paketi başarıyla yayımlandı onaylayan bir e-posta alırsınız. Paket doğrulama denetimi başarısız olursa, ilgili hatayı görüntülemek için Paket ayrıntılarını sayfa güncelleştirilir ve ayrıca hakkında bildiren bir e-posta alırsınız.

Paket doğrulama ve dizin oluşturma altında 15 dakika genellikle alır. Paket yayımlama beklenenden daha uzun sürüyorsa, ziyaret [status.nuget.org](https://status.nuget.org/) NuGet.org tüm kesintileri yaşayan varsa denetlemek için. Tüm sistemler işletimsel ve paket bir saat içinde başarıyla yayımlanmadı, lütfen NuGet.org oturum açın ve paket sayfasında kişi destek bağlantısı kullanarak bizimle bağlantı kurun.

### <a name="visual-studio-team-services-cicd"></a>Visual Studio Team Services (CI/CD)

Paketleri nuget.org sürekli tümleştirme/dağıtım işleminin bir parçası Visual Studio Team Services kullanarak anında iletme, kullanmalısınız `nuget.exe` 4.1 veya yukarıdaki NuGet görevler. Ayrıntılar bulunabilir [yapı içinde son NuGet kullanarak](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blogu).

## <a name="managing-package-owners-on-nugetorg"></a>Nuget.org üzerinde paket sahiplerini yönetme

Ancak her NuGet paketin `.nuspec` dosyası paketin yazarlar tanımlar, nuget.org galeri meta verilerin sahipliği tanımlamak için kullanmaz. Bunun yerine, nuget.org ilk sahipliği paketi yayımlar kişiye atar. Bu paket nuget.org kullanıcı Arabirimi aracılığıyla karşıya oturum açan kullanıcının ya da, API anahtarı ile kullanıldı kullanıcılar olan `nuget SetApiKey` veya `nuget push`.

Tüm paket sahipleri paket ekleme ve kaldırma diğer sahipleri ve güncelleştirmeleri yayımlama da dahil olmak üzere, tam izinlere sahip.

Bir paket sahipliğini değiştirmek için aşağıdakileri yapın:

1. Nuget.org paketinin geçerli sahibi olan hesap ile oturum açın.
1. Tıklayarak kullanıcı adınıza, ardından **my paketlerini yönetme**, yönetmek istediğiniz paketi sonra.
1. Tıklatın **sahiplerini yönetme** sol tarafındaki bağlantı.

Buradan, birkaç seçeneğiniz vardır:

1. Bir sahip eklemek, kendi NuGet hesabı adı girin ve **Ekle**. Bu onay bağlantısı ile yeni ortak sahibi için bir e-posta gönderir. Onaylandıktan sonra o kişiyi eklemek ve sahipleri kaldırmak için tam izinleri vardır. (Onaylandı kadar **sahiplerini yönetme** sayfası, bu kişi için "onay bekliyor" gösterir).
1. Bir sahip kaldırmak için kullanıcıların adı seçin **sahiplerini yönetme** tıklatıp **kaldırmak**.
1. (Olarak ne zaman sahipliği değişiklikleri veya bir paket yanlış hesabı altında yayımlandı), sahipliği yalnızca aktarmak için yeni sahibin ekleyin ve sahipliği onaylanıp sonra bunlar, listeden kaldırabilirsiniz.

Bir şirket veya grup sahipliği atamak için uygun ekip üyelerine iletilen bir e-posta diğer adı kullanarak bir nuget.org hesabı oluşturun. Örneğin, çeşitli Microsoft ASP.NET paketleri birlikte sahibi [microsoft](http://nuget.org/profiles/microsoft) ve [aspnet](http://nuget.org/profiles/aspnet) hesapları, hangi yalnızca gibi diğer adları.

### <a name="recovering-package-ownership"></a>Paket sahipliği kurtarma

Bazen, bir paket etkin bir sahip olmayabilir. Örneğin, özgün sahibinin paket üreten şirket bıraktıysanız, nuget.org kimlik bilgileri kaybolur veya galerisinde önceki hataların bir paket ownerless sol.

Bir paketin gerçek sahibiyseniz ve sahipliği kazanmaya ihtiyacınız varsa kullanmak [kişi formu](https://www.nuget.org/policies/Contact) açıklayan NuGet takım durumunuza nuget.org üzerinde. Biz sonra varolan sahibi paketin proje URL'sini, Twitter, e-posta veya başka yöntemler aracılığıyla bulmaya çalışan dahil olmak üzere paketin, sahipliği doğrulamak için bir işlemi izleyin. Ancak tüm yöntemler başarısız olursa, sahibi olmak için yeni bir davet gönderebiliriz.
