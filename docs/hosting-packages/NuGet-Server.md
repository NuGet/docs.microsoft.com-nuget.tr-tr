---
title: NuGet barındırmak için NuGet.Server kullanarak akışları
description: NuGet.Server kullanarak, HTTP ve OData aracılığıyla paketleri kullanımına IIS çalıştıran herhangi bir sunucuda nasıl oluşturulacağı ve bir NuGet paketi ana akış.
author: karann-msft
ms.author: karann
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: e99d42744ec860976ae098be94e747ec4bc9a7c6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551962"
---
# <a name="nugetserver"></a>NuGet.Server

NuGet.Server, IIS çalıştıran herhangi bir sunucu üzerinde akış bir paket barındırabilecek bir ASP.NET uygulaması oluşturan bir .NET Foundation tarafından sağlanan bir pakettir. Kısaca, NuGet.Server sunucu üzerindeki bir klasöre üzerinden HTTP (S) (özellikle, OData) kullanılabilir hale getirir. Bunu ayarlamak kolaydır ve basit senaryolar için idealdir.

1. Visual Studio'da boş bir ASP.NET Web uygulaması oluşturma ve NuGet.Server paketi ekleyin.
1. Yapılandırma `Packages` uygulama klasöründe ve paketleri ekleyin.
1. Uygun bir sunucu uygulaması dağıtın.

Aşağıdaki bölümlerde ayrıntılı olarak C# kullanarak bu işlemi yol.

Başka NuGet.Server hakkında sorularınız varsa, bir sorun oluşturmak [ https://github.com/nuget/NuGetGallery/issues ](https://github.com/nuget/NuGetGallery/issues).

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a>NuGet.Server ile bir ASP.NET Web uygulaması oluşturma ve dağıtma

1. Visual Studio'da **Dosya > Yeni > Proje**, "ASP.NET için" arayın, seçin **ASP.NET Web uygulaması (.NET Framework)** C# ve küme için şablon **Framework** ".NET Framework 4.6":

    ![Yeni bir proje için hedef Framework'ü ayarlama](media/Hosting_01-NuGet.Server-Set4.6.png)

1. Uygulama uygun bir ad verin *diğer* NuGet.Server Tamam ve sonraki iletişim kutusunda seçin **boş** şablonu seçip **Tamam**.

1. Projeye sağ tıklayın, **NuGet paketlerini Yönet**.

1. Paket Yöneticisi UI'nızda seçin **Gözat** sekmesini, sonra arayın ve .NET Framework 4.6 hedefliyorsanız NuGet.Server paketin en son sürümünü yükleyin. (Paket Yöneticisi konsolu ile de yükleyebilirsiniz `Install-Package NuGet.Server`.) İstenirse, lisans koşullarını kabul.

    ![NuGet.Server paketi yükleniyor](media/Hosting_02-NuGet.Server-Package.png)

1. NuGet.Server yükleme boş bir Web uygulaması, paket kaynağına dönüştürür. Diğer paketleri çeşitli yükler, oluşturur bir `Packages` uygulama klasöründe ve değiştirir `web.config` (bkz. Ayrıntılar için bu dosyayı açıklamalarda) ek ayarlar eklenecek.

    > [!Important]
    > Dikkatli bir şekilde incelemek `web.config` NuGet.Server paketi bu dosya, değişiklik tamamlandıktan sonra. NuGet.Server var olan öğelerin üzerine değil ancak bunun yerine yinelenen öğeler oluşturmak. Daha sonra projeyi çalıştırmak çalıştığınızda bu yinelemeler bir "İç sunucu hatası" neden olur. Örneğin, varsa, `web.config` içeren `<compilation debug="true" targetFramework="4.5.2" />` NuGet.Server'ı yüklemeden önce paket üzerine değil ancak bir saniye ekler `<compilation debug="true" targetFramework="4.6" />`. Bu durumda, daha eski framework sürümü öğeyi silin.

1. Bir sunucu için uygulamayı yayımladığınızda paketleri akışta kullanabilmek için her ekleyin `.nupkg` dosyaları `Packages` klasör Visual Studio'da ayarlayın her birinin **derleme eylemi** için **İçerik**ve **çıkış dizinine Kopyala** için **her zaman Kopyala**:

    ![Projedeki paketler klasörüne kopyalama paketleri](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. Site Visual Studio'da yerel olarak çalıştırma (kullanarak **hata ayıklama > hata ayıklama olmadan Başlat** ya da Ctrl + F5). Giriş sayfasında, aşağıda gösterildiği gibi paket URL'leri akışı sağlar. Hatalar görürseniz, dikkatlice inceleyin, `web.config` için yinelenen öğeler daha önce 5. adım ile belirtilmiştir.

    ![NuGet.Server ile bir uygulama için varsayılan giriş sayfası](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. Tıklayarak **burada** paketlerin OData akışı görmek için yukarıda özetlenen alanında.

1. İlk kez uygulamayı çalıştırdığınızda, NuGet.Server yeniden yapılandırır `Packages` her paket için bir klasör içeren klasör. Bu eşleşen [yerel depolama düzeni](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) performansını artırmak için NuGet 3.3 ile sunulan. Daha fazla paket eklerken, bu yapı izlemeye devam edin.

1. Yerel dağıtımınızı test ettikten sonra gerektiğinde diğer iç veya dış konuma uygulamayı dağıtın.

1. Dağıtıldıktan sonra `http://<domain>`, kullandığınız için paket kaynağı URL'si olacaktır `http://<domain>/nuget`.

## <a name="configuring-the-packages-folder"></a>Paketleri klasörünü yapılandırma

İle `NuGet.Server` 1.5 ve sonrası, daha açık belirtmek gerekirse klasör paketini kullanarak yapılandırabileceğiniz `appSetting/packagesPath` değerini `web.config`:

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

`packagesPath` mutlak ya da sanal bir yol olabilir.

Zaman `packagesPath` atlanırsa veya boş bırakılmış packages klasörünü varsayılandır `~/Packages`.

## <a name="adding-packages-to-the-feed-externally"></a>Harici olarak akışa paketleri ekleme

NuGet.Server site çalışır duruma geçtikten sonra kullanarak paketleri ekleyebilirsiniz [nuget anında iletme](../tools/cli-ref-push.md) API anahtar değeri ayarlamak koşuluyla `web.config`.

NuGet.Server paketini yükledikten sonra `web.config` boş içeren `appSetting/apiKey` değeri:

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

Zaman `apiKey` atlanırsa veya boş, akışa paketleri gönderme devre dışıdır.

Bu özelliği etkinleştirmek için `apiKey` bir değere (İdeal olarak güçlü bir parola) adlı bir anahtar ekleyin `appSettings/requireApiKey` değeriyle `true`:

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

Sunucunuz zaten güvenli veya aksi halde bir API anahtarı (örneğin, bir yerel takım ağında özel bir sunucu kullanarak) gerektirmez, ayarlayabileceğiniz `requireApiKey` için `false`. Sunucusuna erişimi olan tüm kullanıcılar, ardından paketleri gönderebilirsiniz.

## <a name="removing-packages-from-the-feed"></a>Akıştan paket kaldırılıyor

NuGet.Server ile [nuget Sil](../tools/cli-ref-delete.md) komut açıklamayı API anahtarını dahil koşuluyla bu bir paket depodan kaldırır.

Bunun yerine paket delist davranışını değiştirmek istiyorsanız (paket geri yükleme için kullanılabilir bırakarak), değiştirme `enableDelisting` anahtarını `web.config` true.

## <a name="nugetserver-support"></a>NuGet.Server desteği

Ek Yardım için NuGet.Server, kullanarak oluşturduğunuz bir sorun üzerinde [ https://github.com/nuget/NuGetGallery/issues ](https://github.com/nuget/NuGetGallery/issues).