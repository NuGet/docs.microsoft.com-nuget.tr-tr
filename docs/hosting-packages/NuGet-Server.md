---
title: NuGet akışlarını barındırmak için NuGet. Server kullanma
description: NuGet. Server kullanarak IIS çalıştıran herhangi bir sunucuda NuGet paket akışı oluşturma ve barındırma, paketleri HTTP ve OData aracılığıyla kullanılabilir hale getirme.
author: karann-msft
ms.author: karann
ms.date: 03/13/2018
ms.topic: conceptual
ms.openlocfilehash: 098375b2bba13675ba5d80a27e0226dc2ee39e77
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/10/2020
ms.locfileid: "79059586"
---
# <a name="nugetserver"></a>NuGet.Server

NuGet. Server, .NET Foundation tarafından sunulan ve IIS çalıştıran herhangi bir sunucuda paket akışını barındırasağlayan bir ASP.NET uygulaması oluşturan bir pakettir. Yalnızca NuGet. Server, sunucudaki bir klasörü HTTP (S) (özellikle OData) üzerinden kullanılabilir hale getirir. Kolayca ayarlanabilir ve basit senaryolar için idealdir.

1. Visual Studio 'da boş bir ASP.NET Web uygulaması oluşturun ve NuGet. Server paketini buna ekleyin.
1. Uygulamada `Packages` klasörünü yapılandırın ve paketleri ekleyin.
1. Uygulamayı uygun bir sunucuya dağıtın.

Aşağıdaki bölümler, kullanarak C#bu süreci ayrıntılı bir şekilde ele vermektedir.

NuGet. Server hakkında başka sorularınız varsa [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues)bir sorun oluşturun.

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a>NuGet. Server ile bir ASP.NET Web uygulaması oluşturma ve dağıtma

1. Visual Studio 'da **dosya > yeni > proje**' yi seçin, "ASP.NET Web uygulaması (.NET Framework)" araması yapın, için C#eşleşen şablonu seçin.

    ![.NET Framework Web projesi şablonunu seçin](media/Hosting_00-NuGet.Server-ProjectType.png)

1. **Framework 'ü** ".NET Framework 4,6" olarak ayarlayın.

    ![Yeni bir proje için hedef Framework 'ü ayarlama](media/Hosting_01-NuGet.Server-Set4.6.png)

1. Uygulamaya NuGet. *Server dışında uygun bir ad verin* , Tamam ' ı seçin ve sonraki Iletişim kutusunda **boş** şablonu seçin, sonra **Tamam**' ı seçin.

    ![Boş Web projesini seçin](media/Hosting_02-NuGet.Server-Empty.png)

1. Projeye sağ tıklayın, **NuGet Paketlerini Yönet**' i seçin.

1. Paket Yöneticisi Kullanıcı arabiriminde, **Gözden** geçirme sekmesini seçin, ardından .NET Framework 4,6 ' i hedefliyorsanız NuGet. Server paketinin en son sürümünü arayın ve yükleyebilirsiniz. (Aynı zamanda, `Install-Package NuGet.Server`ile paket yöneticisi konsolundan da yükleyebilirsiniz.) İstenirse lisans koşullarını kabul edin.

    ![NuGet. Server paketini yükleme](media/Hosting_03-NuGet.Server-Package.png)

1. NuGet. Server yükleme, boş Web uygulamasını bir paket kaynağına dönüştürür. Çeşitli diğer paketleri yüklerken, uygulamada bir `Packages` klasörü oluşturur ve `web.config` ek ayarları içerecek şekilde değiştirir (Ayrıntılar için bu dosyadaki açıklamalara bakın).

    > [!Important]
    > NuGet. Server paketi bu dosyadaki değişikliklerini tamamladıktan sonra `web.config` dikkatle inceleyin. NuGet. Server varolan öğelerin üzerine yazmayabilir, bunun yerine yinelenen öğeler oluşturabilir. Bu yinelemeler, daha sonra Projeyi çalıştırmaya çalıştığınızda bir "Iç sunucu hatası" oluşmasına neden olur. Örneğin, `web.config` NuGet. Server yüklenmeden önce `<compilation debug="true" targetFramework="4.5.2" />` içeriyorsa, paket onun üzerine yazmaz ancak ikinci bir `<compilation debug="true" targetFramework="4.6" />`ekler. Bu durumda, öğesini eski Framework sürümü ile silin.

1. Siteyi Visual Studio 'da yerel olarak çalıştırın (hata ayıklama **> kullanarak hata ayıklamadan başlayın** veya CTRL + F5). Giriş sayfası, aşağıda gösterildiği gibi paket akışı URL 'Lerini sağlar. Hata görürseniz, daha önce belirtildiği gibi yinelenen öğeler için `web.config` dikkatle inceleyin.

    ![NuGet. Server içeren bir uygulama için varsayılan giriş sayfası](media/Hosting_04-NuGet.Server-FeedHomePage.png)

1.  Uygulamayı ilk kez çalıştırdığınızda, NuGet. Server `Packages` klasörünü her bir paket için bir klasör içerecek şekilde yeniden yapılandırır. Bu, performansı artırmak için NuGet 3,3 ile sunulan [yerel depolama düzeniyle](https://blog.nuget.org/20151118/nuget-3.3.html#folder-based-repository-commands) eşleşir. Daha fazla paket eklerken bu yapıyı izlemeye devam edin.

1. Yerel dağıtımınızı sınadıktan sonra, gerektiğinde uygulamayı başka bir iç veya dış siteye dağıtın.

1. `http://<domain>`için dağıtıldıktan sonra, paket kaynağı için kullandığınız URL `http://<domain>/nuget`olur.

## <a name="adding-packages-to-the-feed-externally"></a>Akışa paket dışarıdan ekleniyor

NuGet. Server sitesi çalışmaya başladıktan sonra, `web.config`içinde bir API anahtar değeri ayarlamanız kaydıyla, [NuGet Push](../reference/cli-reference/cli-ref-push.md) kullanarak paket ekleyebilirsiniz.

NuGet. Server paketini yükledikten sonra `web.config` boş bir `appSetting/apiKey` değeri içerir:

```xml
<appSettings>
    <add key="apiKey" value="" />
</appSettings>
```

`apiKey` atlandığında veya boş bırakıldığında, paketlerin akışa gönderilmesi devre dışı bırakılır.

Bu özelliği etkinleştirmek için, `apiKey` bir değere ayarlayın (ideal bir parola) ve `true`değerine sahip `appSettings/requireApiKey` adlı bir anahtar ekleyin:

```xml
<appSettings>
    <!-- Sets whether an API Key is required to push/delete packages -->
    <add key="requireApiKey" value="true" />

    <!-- Set a shared password (for all users) to push/delete packages -->
    <add key="apiKey" value="" />
</appSettings>
```

Sunucunuz zaten güvenli hale getirilse veya başka türlü bir API anahtarı (örneğin, yerel bir ekip ağı üzerinde bir özel sunucu kullanırken) gerektirmiyorsa, `false``requireApiKey` ayarlayabilirsiniz. Sunucuya erişimi olan tüm kullanıcılar daha sonra paketleri gönderebilir.

NuGet. Server 3.0.0 'den başlayarak, paketlerin gönderilmesi URL 'SI `http://<domain>/nuget`olarak değişir. 3\.0.0 sürümünden önce, gönderim URL 'SI `http://<domain>/api/v2/package`.

NuGet 3.2.1 ve daha yeni bir sürümü ile, bu eski URL `/api/v2/package`, varsayılan olarak başlangıç CONFIG `enableLegacyPushRoute: true` seçeneği aracılığıyla `/nuget` ve varsayılan olarak etkinleştirilir (varsayılan olarak`NuGetODataConfig.cs`). Aynı projede birden çok akış barındırıldığı zaman bu özelliğin çalışmadığına unutmayın.

## <a name="removing-packages-from-the-feed"></a>Paketleri akıştan kaldırma

NuGet. Server ile, [NuGet Delete](../reference/cli-reference/cli-ref-delete.md) komutu, açıklama ile API anahtarını dahil etmeniz kaydıyla bir paketi depodan kaldırır.

Bunun yerine paketin listesini kaldırma (paket geri yükleme için kullanılabilir durumda bırakma) davranışını değiştirmek istiyorsanız, `web.config` `enableDelisting` anahtarını true olarak değiştirin.

## <a name="configuring-the-packages-folder"></a>Paketler klasörünü yapılandırma

`NuGet.Server` 1,5 ve üzeri sürümlerde, paket klasörünü `web.config``appSettings/packagesPath` değerini kullanarak özelleştirebilirsiniz:

```xml
<appSettings>
    <!-- Set the value here to specify your custom packages folder. -->
    <add key="packagesPath" value="C:\MyPackages" />
</appSettings>
```

`packagesPath` mutlak veya sanal yol olabilir.

`packagesPath` atlandığında veya boş bırakıldığında, paketler klasörü varsayılan `~/Packages`.

## <a name="making-packages-available-when-you-publish-the-web-app"></a>Web uygulamasını yayımladığınızda paketleri kullanılabilir hale getirme

Uygulamayı bir sunucuda yayımladığınızda paketleri akışta kullanılabilir hale getirmek için, her bir `.nupkg` dosyasını Visual Studio 'daki `Packages` klasörüne ekleyin, sonra her birinin **derleme eylemini** **içerik** olarak ayarlayın ve her **zaman kopyalamak**için **çıkış dizinine kopyalayın** :

![Paketler projedeki paketler klasörüne kopyalanıyor](media/Hosting_05-NuGet.Server-Package-Folder.png)

## <a name="release-notes"></a>Sürüm Notları

NuGet [Sürüm sayfasında](https://github.com/NuGet/NuGet.Server/releases)NuGet. Server için sürüm notları bulunur.
Bu, hata düzeltmeleri ve eklenen yeni özellikler hakkındaki ayrıntıları içerir.

## <a name="nugetserver-support"></a>NuGet. Server desteği

NuGet. Server kullanarak ek yardım için [https://github.com/nuget/NuGetGallery/issues](https://github.com/nuget/NuGetGallery/issues)bir sorun oluşturun.
