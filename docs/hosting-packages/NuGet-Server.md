---
title: NuGet Akışlarını Barındırmak için NuGet.Server'ı kullanma
description: NuGet.Server kullanarak IIS çalıştıran herhangi bir sunucuda bir NuGet paket akışı oluşturma ve barındırma, paketleri HTTP ve OData üzerinden kullanılabilir hale getirme.
author: karann-msft
ms.author: karann
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: 098375b2bba13675ba5d80a27e0226dc2ee39e77
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79059586"
---
# <a name="nugetserver"></a>NuGet.Server

NuGet.Server, .NET Foundation tarafından sağlanan ve IIS çalıştıran herhangi bir sunucuda paket akışı barındırabilen ASP.NET bir uygulama oluşturan bir pakettir. Basitçe, NuGet.Server sunucuda http(S) (özellikle OData) aracılığıyla kullanılabilir bir klasör yapar söyledi. Kurulumu kolaydır ve basit senaryolar için en iyisidir.

1. Visual Studio'da boş bir ASP.NET Web uygulaması oluşturun ve NuGet.Server paketini ekleyin.
1. Uygulamadaki `Packages` klasörü yapılandırın ve paket ekleyin.
1. Uygulamayı uygun bir sunucuya dağıtın.

Aşağıdaki bölümler, C# kullanarak bu işlemi ayrıntılı olarak inceleyin.

NuGet.Server hakkında başka sorularınız varsa, [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues)bir sorun oluşturun.

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a>NuGet.Server ile ASP.NET bir Web uygulaması oluşturun ve dağıtın

1. Visual Studio'da, **"ASP.NET**Web Uygulaması (.NET Framework)" araması > Yeni > Projesi dosyasını seçin, C#için eşleşen şablonu seçin.

    ![.NET Framework web proje şablonu seçin](media/Hosting_00-NuGet.Server-ProjectType.png)

1. **Çerçeveyi** ".NET Framework 4.6" olarak ayarlayın.

    ![Yeni bir proje için hedef çerçevenin ayarlanması](media/Hosting_01-NuGet.Server-Set4.6.png)

1. Uygulamaya NuGet.Server *dışında* uygun bir ad verin, Tamam'ı seçin ve bir sonraki iletişim kutusunda **Boş** şablonu seçin ve ardından **Tamam'ı**seçin.

    ![Boş web projesini seçin](media/Hosting_02-NuGet.Server-Empty.png)

1. Projeye sağ tıklayın, **NuGet Paketlerini Yönet'i**seçin.

1. Paket Yöneticisi Web Ekibi'nde **Gözat** sekmesini seçin ve .NET Framework 4.6'yı hedefliyorsanız NuGet.Server paketinin en son sürümünü arayın ve yükleyin. (Ayrıca Paket Yöneticisi Konsolu ile `Install-Package NuGet.Server`yükleyebilirsiniz.) İstenirse lisans koşullarını kabul edin.

    ![NuGet.Server paketini yükleme](media/Hosting_03-NuGet.Server-Package.png)

1. NuGet.Server'ın yüklenmesi, boş Web uygulamasını bir paket kaynağına dönüştürür. Çeşitli diğer paketleri yükler, uygulamada bir `Packages` klasör oluşturur ve ek `web.config` ayarlar içerecek şekilde değişir (ayrıntılar için bu dosyadaki yorumlara bakın).

    > [!Important]
    > NuGet.Server paketi bu dosyadaki değişikliklerini tamamladıktan sonra dikkatlice inceleyin. `web.config` NuGet.Server varolan öğelerin üzerine yazmıyor, bunun yerine yinelenen öğeler oluşturabilir. Bu yinelemeler, daha sonra projeyi çalıştırmayı denediğinizde bir "İç Sunucu Hatasına" neden olur. Örneğin, NuGet.Server'ı yüklemeden önce içerseniz, `web.config` `<compilation debug="true" targetFramework="4.5.2" />` paket üzerine yazmıyor, `<compilation debug="true" targetFramework="4.6" />`ikinci bir şey ekler. Bu durumda, eski çerçeve sürümü ile öğeyi silin.

1. Siteyi Visual Studio'da yerel olarak çalıştırın **(Hata Ayıklama > Hata Ayıklama veya** Ctrl+F5 olmadan Başlat'ı kullanarak). Ana sayfa, aşağıda gösterildiği gibi paket besleme URL'lerini sağlar. Hatalar görürseniz, daha önce `web.config` belirtildiği gibi yinelenen öğeler için dikkatlice denetleyin.

    ![NuGet.Server ile bir uygulama için varsayılan giriş sayfası](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1.  Uygulamayı ilk çalıştırdığınızda, NuGet.Server klasörü `Packages` her paket için bir klasör içerecek şekilde yeniden yapılandırır. Bu, performansı artırmak için NuGet 3.3 ile tanıtılan [yerel depolama düzeniyle](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) eşleşir. Daha fazla paket eklerken, bu yapıyı izlemeye devam edin.

1. Yerel dağıtımınızı test ettikten sonra, uygulamayı gerektiğinde başka bir dahili veya harici siteye dağıtın.

1. Bir kez `http://<domain>`dağıtıldıktan sonra, paket kaynağı için `http://<domain>/nuget`kullandığınız URL olacaktır.

## <a name="adding-packages-to-the-feed-externally"></a>Beslemeye harici paket ekleme

NuGet.Server sitesi çalışmaya başladıktan sonra, ['de](../reference/cli-reference/cli-ref-push.md) `web.config`bir API anahtar değeri ayarlamanız koşuluyla nuget push kullanarak paketler ekleyebilirsiniz.

NuGet.Server paketini yükledikten sonra `appSetting/apiKey` boş bir değer `web.config` içerir:

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

Atlandığında veya boş olduğunda, `apiKey` paketleri özet akışına itme devre dışı bırakılır.

Bu özelliği etkinleştirmek `apiKey` için, bir değer (ideal olarak güçlü bir `appSettings/requireApiKey` parola) `true`ayarlayın ve değeri ile adlandırılan bir anahtar ekleyin:

```xml
<appSettings>
    <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

Sunucunuz zaten güvenliyse veya başka bir şekilde bir API anahtarına ihtiyaç damıyorsanız `requireApiKey` (örneğin, yerel `false`bir ekip ağında özel bir sunucu kullanırken), . Sunucuya erişimi olan tüm kullanıcılar daha sonra paketleri itebilir.

NuGet.Server 3.0.0 ile başlayarak, paketleri itme için URL 'ye `http://<domain>/nuget`göre değiştirildi. 3.0.0 sürümünden önce, itme `http://<domain>/api/v2/package`URL'si .

NuGet 3.2.1 ve daha yeni `/api/v2/package` ile bu eski `/nuget` URL, `enableLegacyPushRoute: true` başlangıç config'inizdeki seçenek üzerinden varsayılan olarak (varsayılan`NuGetODataConfig.cs` olarak) ek olarak etkinleştirilir. Aynı projede birden çok özet akışı barındırıldığında bu özelliğin çalışmadığını unutmayın.

## <a name="removing-packages-from-the-feed"></a>Paketleri akıştan kaldırma

NuGet.Server ile [nuget silme](../reference/cli-reference/cli-ref-delete.md) komutu, yoruma API anahtarı eklemeniz koşuluyla bir paketi depodan kaldırır.

Bunun yerine paketin listesini çıkarmak için davranışı değiştirmek istiyorsanız (paket geri `enableDelisting` yükleme `web.config` için kullanılabilir bırakarak), anahtarı true olarak değiştirin.

## <a name="configuring-the-packages-folder"></a>Paketler klasörünü yapılandırma

1.5 ve sonrası ile, `NuGet.Server` `appSettings/packagesPath` aşağıdaki değeri kullanarak paket `web.config`klasörünü özelleştirebilirsiniz:

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

`packagesPath`mutlak veya sanal bir yol olabilir.

Atlandığında veya boş bırakıldığında, `packagesPath` paketler klasörü `~/Packages`varsayılandır.

## <a name="making-packages-available-when-you-publish-the-web-app"></a>Web uygulamasını yayımladığınızda paketleri kullanılabilir hale getirme

Uygulamayı bir sunucuda yayımladığınızda özet akışında paketleri kullanılabilir `.nupkg` hale `Packages` getirmek için, her dosyayı Visual Studio'daki klasöre ekleyin ve ardından her birinin **Yapı Eylemini** **İçerik'e** ayarlayın ve Her **zaman Kopyalamak** **için Çıktı Dizini'ne Kopyala:**

![Projedeki Paketler klasörüne paketleri kopyalama](media/Hosting_05-NuGet.Server-Package-Folder.png)

## <a name="release-notes"></a>Sürüm Notları

NuGet.Server için sürüm notları [GitHub sürüm sayfasında](https://github.com/NuGet/NuGet.Server/releases)mevcuttur.
Bu hata düzeltmeleri ve eklenen yeni özellikler hakkında ayrıntıları içerir.

## <a name="nugetserver-support"></a>NuGet.Server desteği

NuGet.Server'ı kullanarak ek yardım [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues)için bir sorun oluşturun.
