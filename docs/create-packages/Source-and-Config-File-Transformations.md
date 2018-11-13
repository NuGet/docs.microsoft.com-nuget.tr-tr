---
title: NuGet paketleri için kaynak ve yapılandırma dosyası dönüşümleri
description: Kaynak kodu ve yapılandırması dönüştürmek NuGet paketlerini özelliği üzerinde yüklendiğinde (XML) dosyaları ayrıntılı olarak açıklanmaktadır.
author: karann-msft
ms.author: karann
ms.date: 04/24/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 830714269ac422a4784c15b000e374195f02332f
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580291"
---
# <a name="transforming-source-code-and-configuration-files"></a>Kaynak kodu ve yapılandırma dosyaları dönüştürme

Kullanarak projeleri için `packages.config`, NuGet kaynak koda dönüştürme yapma yeteneğini destekler ve paket konumundaki yapılandırma dosyalarını yükler ve kez kaldırın. Bir paketi kullanarak bir proje yüklendiğinde yalnızca kaynak kodu dönüşümleri uygulanır [PackageReference](../consume-packages/package-references-in-project-files.md).

A **kaynak kodu dönüştürme** paketin dosyalarda tek yönlü belirteç değiştirme uygulandığı `content` veya `contentFiles` klasörü (`content` kullanan müşteriler için `packages.config` ve `contentFiles` için`PackageReference`) paketi yüklendiğinde, burada belirteçleri başvurmak için Visual Studio [proje özellikleri](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7). Bu projenin ad alanına bir dosya eklemek için ya da genellikle içine çıkacak kod özelleştirmenizi sağlar `global.asax` bir ASP.NET projesi içinde.

A **config dosya dönüştürme** zaten bir hedef projesinde gibi mevcut dosyaları değiştirebilmenizi sağlar `web.config` ve `app.config`. Örneğin, paketinizin bir öğeye eklemeniz gerekebilir `modules` bölümünde yapılandırma dosyası. Bu dönüştürme için yapılandırma dosyalarını eklemek bölümlerde paketinde özel dosyaları ekleyerek gerçekleştirilir. Bir paket kaldırıldığında, aynı değişiklikleri daha sonra bu iki yönlü bir dönüştürme yapma ters çevrilir.

## <a name="specifying-source-code-transformations"></a>Kaynak kodu dönüşümleri belirtme

1. Paketten projeye eklemek istediğiniz dosya paketin içinde bulunduğu olmalıdır `content` ve `contentFiles` klasörleri. Adlı bir dosya istiyorsanız, örneğin, `ContosoData.cs` yüklenmesi bir `Models` klasörü hedef projenin olmalıdır içinde `content\Models` ve `contentFiles\{lang}\{tfm}\Models` paketteki klasörleri.

1. Yükleme sırasında belirteç değiştirme uygulamak için NuGet bileşenine ekleme `.pp` kaynak kod dosya adı. Yüklemeden sonra dosya olmayacaktır `.pp` uzantısı.

    Örneğin dönüşümlerini yapmak `ContosoData.cs`, paketteki dosya adı `ContosoData.cs.pp`. Yükleme sonrasında olarak görünür `ContosoData.cs`.

1. Kaynak kodu dosyasında biçiminin büyük küçük harf duyarsız belirteçleri kullanmasını `$token$` değerleri göstermek için NuGet ile proje özelliklerini değiştirmeniz gerekir:

    ```cs
    namespace $rootnamespace$.Models
    {
        public struct CategoryInfo
        {
            public string categoryid;
            public string description;
            public string htmlUrl;
            public string rssUrl;
            public string title;
        }
    }
    ```

    Yükleme işleminden sonra NuGet değiştirir `$rootnamespace$` ile `Fabrikam` hedef projeye varsayılarak kullanıcının Kök ad alanı olan `Fabrikam`.

`$rootnamespace$` Belirteci en yaygın olarak kullanılan proje özelliği; diğer tüm listelenen [proje özellikleri](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7). Elbette, bazı özellikleri proje türüne özgü olabilir oluşturduğunu, unutmayın.

## <a name="specifying-config-file-transformations"></a>Yapılandırma dosyası dönüşümleri belirtme

İzleyen bölümlerde açıklandığı gibi yapılandırma dosyası dönüşümleri iki şekilde gerçekleştirilebilir:

- Dahil `app.config.transform` ve `web.config.transform` paketinizin dosyalarında `content` klasörü, burada `.transform` uzantısı NuGet paketi yüklendiğinde var olan yapılandırma dosyaları ile birleştirmek için XML bu dosyaları içermesini söyler. Bir paket kaldırıldığında, aynı XML kaldırılır.
- Dahil `app.config.install.xdt` ve `web.config.install.xdt` paketinizin dosyalarında `content` klasöründe kullanarak [XDT söz dizimi](https://msdn.microsoft.com/library/dd465326.aspx) istenen değişiklikleri açıklamak için. Bu seçenekle da dahil edebilirsiniz bir `.uninstall.xdt` paket bir projeden kaldırıldığında değişiklikleri geri almak için dosya.

> [!Note]
> Dönüştürmeleri için uygulanmaz `.config` Visual Studio'da bir bağlantı olarak başvurulan dosyaları.

XDT kullanmanın avantajı yalnızca iki statik dosyaları birleştirme yerine, bunu bir sözdizimi bir XML DOM öğesi ve öznitelik XPath için tam destek kullanarak eşleşen kullanarak yapısını işlemek için sağlamasıdır. XDT ardından ekleme, güncelleştirme veya öğeleri kaldırın, yeni öğeleri belirli bir konuma yerleştirin veya (alt düğümler dahil olmak üzere) öğeleri Değiştir/Kaldır. Bu, paket yükleme sırasında yapılan tüm dönüştürmeler geri kaldırma dönüşümler oluşturmak basit kılar.

### <a name="xml-transforms"></a>XML dönüşümleri

`app.config.transform` Ve `web.config.transform` bir paketin içinde `content` klasörü içeren proje mevcut birleştirmek için yalnızca bu öğeleri `app.config` ve `web.config` dosyaları.

Örneğin, proje, başlangıçta aşağıdaki içeriği içerdiğini varsayın `web.config`:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

Eklemek için bir `MyNuModule` öğesine `modules` bölümünde paket yükleme sırasında oluşturun bir `web.config.transform` paketin dosyasında `content` şuna benzer bir klasörü:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

NuGet paket yüklendikten sonra `web.config` şu şekilde görünür:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

NuGet değiştirmek istemediğiniz bildirimi `modules` bölümünde, yalnızca birleştirilen yeni girişine yalnızca yeni öğeler ve öznitelikler ekleyerek. NuGet, tüm mevcut öğeler ve öznitelikler değişmez.

NuGet Paketi kaldırıldığında inceleyeceksiniz `.transform` yeniden dosyaları ve içerdiği öğeleri uygun kaldırmak `.config` dosyaları. Bu işlem tüm satırları etkilemez Not `.config` paket yükleme sonrasında değiştirmek dosya.

Daha kapsamlı bir örnek olarak [hata günlüğü modüller ve işleyiciler için ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) paket birçok girişleri ekler `web.config`, hangi yeniden kaldırılır bir paket kaldırıldığında.

İncelemek için kendi `web.config.transform` dosya, yukarıdaki bağlantıdan ELMAH paketini indirmek, paket uzantısını değiştirme `.nupkg` için `.zip`ve ardından açın `content\web.config.transform` bu ZIP dosyasında.

Yükleme ve paket kaldırma etkisini görmek için Visual Studio'da yeni bir ASP.NET projesi oluşturma (şablon altındadır **Visual C# > Web** yeni proje iletişim kutusunda), boş bir ASP.NET uygulaması seçin. Açık `web.config` başlangıç durumunu görmek için. Daha sonra projeye sağ tıklayın, **NuGet paketlerini Yönet**ELMAH için nuget.org adresinden göz atın ve en son sürümünü yükleyin. Yapılan tüm değişiklikler fark `web.config`. Artık paketi kaldırın ve gördüğünüz `web.config` önceki durumuna geri döndürme.

### <a name="xdt-transforms"></a>XDT dönüşümler

Yapılandırma dosyalarını kullanarak değiştirebileceğiniz [XDT söz dizimi](https://msdn.microsoft.com/library/dd465326.aspx). NuGet belirteçleri ile değiştirin bulundurabilirsiniz [proje özellikleri](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) içinde özellik adı ekleyerek `$` sınırlayıcılar (büyük-küçük harf duyarsız).

Örneğin, aşağıdaki `app.config.install.xdt` dosyası ekler bir `appSettings` öğesine `app.config` içeren `FullPath`, `FileName`, ve `ActiveConfigurationSettings` projesinden değerleri:

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <appSettings xdt:Transform="Insert">
        <add key="FullPath" value="$FullPath$" />
        <add key="FileName" value="$filename$" />
        <add key="ActiveConfigurationSettings " value="$ActiveConfigurationSettings$" />
    </appSettings>
</configuration>
```

Başka bir örnek için proje, başlangıçta aşağıdaki içeriği içerdiğini varsayın `web.config`:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

Eklemek için bir `MyNuModule` öğesine `modules` bölüm paket sırasında yükleme, paket `web.config.install.xdt` aşağıdakileri içerir:

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" xdt:Transform="Insert" />
        </modules>
    </system.webServer>
</configuration>
```

Paket yüklendikten sonra `web.config` şöyle görünür:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

Yalnızca kaldırmak için `MyNuModule` öğesi paketi kaldırma sırasında `web.config.uninstall.xdt` dosyası şunları içermelidir:

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <system.webServer>
        <modules>
            <add name="MyNuModule" xdt:Transform="Remove" xdt:Locator="Match(name)" />
        </modules>
    </system.webServer>
</configuration>
```
