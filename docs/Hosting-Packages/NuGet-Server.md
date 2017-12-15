---
title: "NuGet barındırmak için NuGet.Server kullanarak akışları | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 8/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 45138f80-9717-42c2-8b34-9a1bc1fb3eab
description: "NuGet.Server kullanarak, paketleri HTTP ve OData yoluyla kullanılabilir hale getirme IIS çalıştıran herhangi bir sunucuda nasıl oluşturulacağı ve bir NuGet paketi konak akış."
keywords: "Akış, NuGet NuGet galerisinde, akış, Uzak paket NuGet.Server"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f37b9b711a2bc8c39314214113045a6485f297a8
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="nugetserver"></a>NuGet.Server

NuGet.Server, IIS çalıştıran herhangi bir sunucu üzerinde akış paket barındırabilen bir ASP.NET uygulaması oluşturur .NET Foundation tarafından sağlanan bir pakettir. Kısaca, NuGet.Server sunucusundaki bir klasöre aracılığıyla HTTP (S) (özellikle OData) kullanılabilir hale getirir. Ayarlamak kolaydır ve basit senaryoları için en iyisidir.

1. Visual Studio'da boş bir ASP.NET Web uygulaması oluşturun ve NuGet.Server paketi ekleyin.
1. Yapılandırma `Packages` uygulama klasöründe ve paketleri ekleyin.
1. Uygun bir sunucu uygulamayı dağıtın.

Aşağıdaki bölümlerde bu işlem C# kullanarak ayrıntılı yol.

## <a name="create-and-deploy-an-aspnet-web-application-with-nugetserver"></a>Bir ASP.NET Web uygulama NuGet.Server ile oluşturun ve dağıtın

1. Visual Studio'da seçin **Dosya > Yeni > Proje**, .NET Framework 4.6 (aşağıya bakın), "ASP.NET" için arama için hedef Framework'ü ayarlayabilir ve seçin **ASP.NET Web uygulaması (.NET Framework)** Şablon için C#.

    ![.NET Framework hedef 4.6 için ayarlama](media/Hosting_01-NuGet.Server-Set4.6.png)

1. Uygulama uygun bir ad verin *diğer* NuGet.Server Tamam ve sonraki iletişim kutusunda seçin **boş** şablonu ve select Tamam.

1. Projeye sağ tıklayın, **NuGet paketlerini Yönet**, Paket Yöneticisi Arabiriminde arayın ve .NET Framework 4.6 hedefleme NuGet.Server paketinin en son sürümünü yükleyin. (İle Paket Yöneticisi Konsolu'ndan de yükleyebilirsiniz `Install-Package NuGet.Server`.)

    ![NuGet.Server paketi yükleniyor](media/Hosting_02-NuGet.Server-Package.png)

    > [!Important]
    > Web uygulamanız .NET Framework 4.5.2 hedefliyorsa, NuGet sunucusu yüklemeniz gerekir **2.10.3** yerine.

1. NuGet.Server yükleme boş bir Web uygulaması bir paket kaynağına dönüştürür. Oluşturduğu bir `Packages` uygulama klasöründe ve üzerine yazar `web.config` (bkz. Ayrıntılar için bu dosyayı açıklamalarda) ek ayarlar dahil etmek için.

1. Bir sunucuya uygulama yayımladığınızda, paketleri akıştaki kullanılabilir kılmak için eklemeniz kendi `.nupkg` dosyaları `Packages` klasörü Visual Studio'da sonra ayarlanmış kendi **yapı eylemi** için **İçerik**ve **çıktı dizinine Kopyala** için **her zaman Kopyala**:

    ![Paketleri projesinde paketleri klasöre kopyalama](media/Hosting_03-NuGet.Server-Package-Folder.png)

1. Site (hata ayıklama olmadan, yani Ctrl + F5) Visual Studio'da yerel olarak çalıştırın. Giriş sayfası URL'leri paket akışı sağlar:

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

`packagesPath`mutlak ya da sanal bir yol olabilir.

Zaman `packagesPath` atlanmış veya boş, sol varsayılan paketleri klasörüdür `~/Packages`.

## <a name="adding-packages-to-the-feed-externally"></a>Akışa dışarıdan paketleri ekleme

NuGet.Server site çalışmaya başladıktan sonra ekleme veya API anahtar değeri ayarlanmış koşuluyla, nuget.exe kullanarak paketleri silme `web.config`.

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

Sunucunuz zaten korunuyor veya aksi halde bir API anahtarı (örneğin, özel bir sunucu yerel takım ağında kullanırken) gerektirmez, ayarlayabileceğiniz `requireApiKey` için `false`. Sunucu erişimi olan tüm kullanıcılar sonra push veya paketleri silmek.