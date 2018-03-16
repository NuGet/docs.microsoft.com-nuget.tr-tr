---
title: "NuGet barındırmak için NuGet.Server kullanarak akışları | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/13/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet.Server kullanarak, paketleri HTTP ve OData yoluyla kullanılabilir hale getirme IIS çalıştıran herhangi bir sunucuda nasıl oluşturulacağı ve bir NuGet paketi konak akış."
keywords: "Akış, NuGet NuGet galerisinde, akış, Uzak paket NuGet.Server"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d85c1ca88ca44c8f8bfa5cb9c453279f65f26f50
ms.sourcegitcommit: 9adf5349eab91bd1d044e11f34836d53cfb115b3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/16/2018
---
# <a name="nugetserver"></a>NuGet.Server

NuGet.Server, IIS çalıştıran herhangi bir sunucu üzerinde akış paket barındırabilen bir ASP.NET uygulaması oluşturur .NET Foundation tarafından sağlanan bir pakettir. Kısaca, NuGet.Server sunucusundaki bir klasöre aracılığıyla HTTP (S) (özellikle OData) kullanılabilir hale getirir. Ayarlamak kolaydır ve basit senaryoları için en iyisidir.

1. Visual Studio'da boş bir ASP.NET Web uygulaması oluşturun ve NuGet.Server paketi ekleyin.
1. Yapılandırma `Packages` uygulama klasöründe ve paketleri ekleyin.
1. Uygun bir sunucu uygulamayı dağıtın.

Aşağıdaki bölümlerde bu işlem C# kullanarak ayrıntılı yol.

Daha fazla NuGet.Server hakkında sorularınız varsa, bir sorun oluşturmak [ https://github.com/nuget/NuGetGallery/issues ](https://github.com/nuget/NuGetGallery/issues).

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a>Bir ASP.NET Web uygulama NuGet.Server ile oluşturun ve dağıtın

1. Visual Studio'da seçin **Dosya > Yeni > Proje**, arama "ASP.NET için", seçin **ASP.NET Web uygulaması (.NET Framework)** C# ve kümesi için şablon **Framework** ".NET Framework 4.6":

    ![Yeni bir proje hedef çerçevesi ayarlama](media/Hosting_01-NuGet.Server-Set4.6.png)

1. Uygulama uygun bir ad verin *diğer* NuGet.Server Tamam ve sonraki iletişim kutusunda seçin **boş** şablonu, ardından **Tamam**.

1. Projeye sağ tıklayın, **NuGet paketlerini Yönet**.

1. Paket Yöneticisi Arabiriminde seçin **Gözat** sekmesinde, sonra arayın ve .NET Framework 4.6 hedefleme NuGet.Server paketinin en son sürümünü yükleyin. (İle Paket Yöneticisi Konsolu'ndan de yükleyebilirsiniz `Install-Package NuGet.Server`.) Lisans koşullarını kabul etmeniz istenirse.

    ![NuGet.Server paketi yükleniyor](media/Hosting_02-NuGet.Server-Package.png)

1. NuGet.Server yükleme boş bir Web uygulaması bir paket kaynağına dönüştürür. Çeşitli diğer paketler yükler, oluşturur bir `Packages` uygulama klasöründe ve değiştirir `web.config` (bkz. Ayrıntılar için bu dosyayı açıklamalarda) ek ayarlar dahil etmek için.

    > [!Important]
    > Dikkatlice inceleyin `web.config` NuGet.Server paket bu dosyaya kendi değişiklikler tamamlandıktan sonra. NuGet.Server bellek kaynakları olan öğeleri üzerine değildir ancak bunun yerine yinelenen öğeler oluşturur. Daha sonra projeyi çalıştırmayı denediğinizde bu yinelenen bir "Dahili Sunucu hatası" neden olur. Örneğin, varsa, `web.config` içeren `<compilation debug="true" targetFramework="4.5.2" />` NuGet.Server'ı yüklemeden önce paketin üzerine değildir ancak ikinci ekler `<compilation debug="true" targetFramework="4.6" />`. Bu durumda, eski framework sürüm öğesini silin.

1. Bir sunucuya uygulama yayımladığınızda, paketleri akıştaki kullanılabilir kılmak için her eklemeniz `.nupkg` dosyaları `Packages` klasörü Visual Studio'da sonra ayarlanmış her birinin **yapı eylemi** için **İçerik**ve **çıktı dizinine Kopyala** için **her zaman Kopyala**:

    ![Paketleri projesinde paketleri klasöre kopyalama](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. Siteyi Visual Studio'da yerel olarak çalıştırın (kullanarak **hata ayıklama > hata ayıklama olmadan Başlat** veya Ctrl + F5). Giriş sayfası, aşağıda gösterildiği gibi URL'leri paket akışı sağlar. Hatalar görürseniz, dikkatlice inceleyin, `web.config` için yinelenen öğeler önceki adım 5 ile belirtilmiştir.

    ![NuGet.Server olan bir uygulama için varsayılan giriş sayfası](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1. Tıklayın **burada** paketlerin OData akışı görmek için yukarıda özetlenen alanında.

1. İlk kez uygulamayı çalıştırın, NuGet.Server yeniden yapılandırır `Packages` her paket için bir klasör içeren klasör. Bu eşleşen [yerel depolama düzeni](http://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) performansını artırmak için NuGet 3.3 ile sunulmuştur. Daha fazla paket eklerken, bu yapıyı izlemeye devam edin.

1. Yerel dağıtımınızı test ettikten sonra diğer iç veya dış site uygulamaya gerektiği gibi dağıtın.

1. Dağıtıldıktan sonra `http://<domain>`, paket kaynağı için kullandığınız URL'yi olacaktır `http://<domain>/nuget`.

## <a name="configuring-the-packages-folder"></a>Paketler klasörü yapılandırma

İle `NuGet.Server` 1,5 ve daha sonra daha açık belirtmek gerekirse paket klasörünü kullanarak yapılandırabileceğiniz `appSetting/packagesPath` değeri `web.config`:

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

`packagesPath` mutlak ya da sanal bir yol olabilir.

Zaman `packagesPath` atlanmış veya boş, sol varsayılan paketleri klasörüdür `~/Packages`.

## <a name="adding-packages-to-the-feed-externally"></a>Akışa dışarıdan paketleri ekleme

NuGet.Server site çalışmaya başladıktan sonra kullanarak paketleri ekleyebilirsiniz [nuget itme](../tools/cli-ref-push.md) API anahtar değeri ayarlanmış koşuluyla, `web.config`.

NuGet.Server paketini yükledikten sonra `web.config` boş bir içeren `appSetting/apiKey` değeri:

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

Zaman `apiKey` atlanmış veya boş, paketleri akışa Ftp'den devre dışı bırakıldı.

Bu özelliği etkinleştirmek için ayarlanmış `apiKey` bir değere (İdeal olarak güçlü bir parola) adlı bir anahtar ekleyin `appSettings/requireApiKey` değeriyle `true`:

```xml
<appSettings>
        <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

Sunucunuz zaten korunuyor veya aksi halde bir API anahtarı (örneğin, özel bir sunucu yerel takım ağında kullanırken) gerektirmez, ayarlayabileceğiniz `requireApiKey` için `false`. Sunucu erişimi olan tüm kullanıcılar, ardından paketleri gönderebilir.

## <a name="removing-packages-from-the-feed"></a>Akıştan paketlerini kaldırma

NuGet.Server ile [nuget silmek](../tools/cli-ref-delete.md) komutu açıklamayı içeren API anahtarı eklemek koşuluyla, bir paket depodan kaldırır.

Bunun yerine paket delist davranışı değiştirmek isterseniz (paket geri yükleme için kullanılabilir bırakarak), değiştirme `enableDelisting` anahtarını `web.config` true.

## <a name="nugetserver-support"></a>NuGet.Server desteği

Ek Yardım için NuGet.Server, kullanarak oluşturduğunuz bir sorun üzerinde [ https://github.com/nuget/NuGetGallery/issues ](https://github.com/nuget/NuGetGallery/issues).