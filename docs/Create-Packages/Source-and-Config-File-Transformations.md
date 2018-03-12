---
title: "Kaynak ve yapılandırma dosyası dönüştürmeleri için NuGet paketleri | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 04/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Kaynak kodu ve yapılandırması dönüştürmesini NuGet paketlerini yeteneğine yüklendiğinde (XML) dosyaları ayrıntılarını verir."
keywords: "NuGet paket yükleme, yapılandırma dosyalarını, kaynak kodun değiştirilmesiyle değiştirme NuGet paketi dönüşümleri"
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: 47d02d160a7e40f323edcbd87e2c8642905b8ddf
ms.sourcegitcommit: df21fe770900644d476d51622a999597a6f20ef8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/12/2018
---
# <a name="transforming-source-code-and-configuration-files"></a>Kaynak kodu ve yapılandırma dosyaları dönüştürme

Kullanarak projeleri için `packages.config`, NuGet kaynak kodu dönüşümleri yapma yeteneği destekler ve paket yapılandırma dosyaları yükleyip kez kaldırın. Bir paketi kullanarak bir projeye yüklendiğinde yalnızca kaynak kodu dönüşümleri uygulanır [PackageReference](../consume-packages/package-references-in-project-files.md).

A **kaynak kodu dönüştürme** paketin dosyalarında tek yönlü belirteci değiştirme uygulandığı `content` veya `contentFiles` klasörü (`content` kullanan müşteriler için `packages.config` ve `contentFiles` için`PackageReference`) paketi yüklendiğinde, burada belirteçleri başvurmak için Visual Studio [proje özellikleri](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7). Bu projenin ad alanına bir dosya eklemek için ya da genellikle içine geçecek kod özelleştirmenizi sağlar `global.asax` ASP.NET projesinde.

A **config dosya dönüşümü** , bir hedef projesinde gibi zaten mevcut dosyaların değiştirmenizi sağlar `web.config` ve `app.config`. Örneğin, bir öğe eklemek paketinizi gereken `modules` yapılandırma dosyası bölümünde. Bu dönüştürme için yapılandırma dosyalarını eklemek için bölümlerde paketinde özel dosyaları ekleyerek yapılır. Bir paketi kaldırıldığında, aynı değişiklikleri daha sonra bu iki yönlü bir dönüştürme yapma ters çevrilir.

## <a name="specifying-source-code-transformations"></a>Kaynak kodu dönüşümleri belirtme

1. Paketten projeye eklemek istediğiniz dosya paketin içinde bulunduğu olmalıdır `content` ve `contentFiles` klasörler. Adlı bir dosya isterseniz, örneğin, `ContosoData.cs` yüklenmesi için bir `Models` klasörü hedef projesinin olmalıdır içinde `content\Models` ve `contentFiles\{lang}\{tfm}\Models` paket klasörlerde.

1. Yükleme sırasında belirteci değiştirme uygulamak için NuGet istemek üzere append `.pp` kaynak kodu dosya adı. Yükleme tamamlandıktan sonra dosya değil olacaktır `.pp` uzantısı.

    Örneğin, dönüşümler yapmak için `ContosoData.cs`, paketteki dosya adı `ContosoData.cs.pp`. Yükleme sonrasında olarak görünür `ContosoData.cs`.

1. Kaynak kodu dosyasının formun büyük küçük harf duyarsız belirteçlerini kullanmak `$token$` değerleri belirtmek için bu NuGet proje özellikleri ile değiştirmeniz gerekir:

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

    Yükleme işleminden sonra NuGet değiştirir `$rootnamespace$` ile `Fabrikam` hedef projeyi varsayılarak kullanıcının, kök ad alanı `Fabrikam`.

`$rootnamespace$` Belirteci en yaygın kullanılan proje özelliği; diğerlerini listelenen [proje özellikleri](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7). Elbette, bazı özellikler için proje türü belirli olabileceğini oluşturduğunu, unutmayın.

## <a name="specifying-config-file-transformations"></a>Yapılandırma dosyası dönüşümleri belirtme

İzleyen bölümlerde açıklandığı gibi iki yolla yapılandırma dosyası dönüşümleri yapılabilir:

- Dahil `app.config.transform` ve `web.config.transform` , paketin dosyalarında `content` klasörü, burada `.transform` uzantısı, bu dosyaları paketi yüklendiğinde var olan yapılandırma dosyaları ile birleştirmek için bir XML içeriyor NuGet söyler. Bir paketi kaldırıldığında, aynı XML kaldırılır.
- Dahil `app.config.install.xdt` ve `web.config.install.xdt` , paketin dosyalarında `content` klasörünü kullanarak [XDT sözdizimi](https://msdn.microsoft.com/library/dd465326.aspx) istediğiniz değişiklikleri açıklamak için. Bu seçenek ile de ekleyebilirsiniz bir `.uninstall.xdt` paket projeden kaldırıldığında değişiklikleri geri almak için dosya.

> [!Note]
> Dönüştürmeleri için uygulanmaz `.config` Visual Studio'da bir bağlantı olarak başvurulan dosyaları.

XDT kullanmanın avantajı yalnızca iki statik dosyaları birleştirme yerine, bir sözdizimi öğe ve öznitelik kullanılarak tam XPath desteği eşleşen kullanarak bir XML DOM yapısını işlemek için sağlamasıdır. XDT sonra ekleme, güncelleştirme veya öğeleri kaldırın, yeni öğeleri belirli bir konuma yerleştirin veya Değiştir / (alt düğümler de dahil olmak üzere) öğeleri kaldır. Bu, paket yükleme sırasında yapılan tüm dönüştürmeleri çıkışı geri kaldırma dönüşümleri oluşturmak basitleştirir.

### <a name="xml-transforms"></a>XML dönüşümler

`app.config.transform` Ve `web.config.transform` bir paketin içinde `content` klasörünü içeren projenin varolan halinde birleştirmek için yalnızca bu öğeler `app.config` ve `web.config` dosyaları.

Örnek olarak, projeyi başlangıçta aşağıdaki içeriği içeren varsayalım `web.config`:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

Eklemek için bir `MyNuModule` öğesine `modules` bölümünde paket yükleme sırasında oluşturma bir `web.config.transform` paketin dosyasında `content` şöyle klasörü:

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

NuGet Değiştir kaydetmedi bildirimi `modules` bölümünde, yalnızca birleştirilen içine yeni giriş yalnızca yeni öğeleri ve özniteliklerinin ekleyerek. NuGet herhangi bir varolan öğeleri veya öznitelikleri değiştirmez.

NuGet paket kaldırıldığında inceleyeceksiniz `.transform` yeniden dosyaları ve içerdiği öğeleri uygun Kaldır `.config` dosyaları. Bu işlem tüm satırları etkilemez Not `.config` paket yüklendikten sonra değiştirmek dosya.

Daha kapsamlı bir örnek olarak [hata günlük modülleri ve işleyicileri için ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) paket içine birçok girdisi ekler `web.config`, hangi yeniden kaldırılır bir paket kaldırıldığında.

İncelemek için kendi `web.config.transform` dosya, yukarıdaki bağlantıyı ELMAH paketini indirin, paket uzantı değiştirme `.nupkg` için `.zip`ve ardından açın `content\web.config.transform` o ZIP dosyasında.

Yükleme ve paket kaldırma etkisini görmek için Visual Studio'da yeni bir ASP.NET projesi oluşturma (altında şablonudur **Visual C# > Web** yeni proje iletişim kutusunda) ve boş bir ASP.NET uygulamasını seçin. Açık `web.config` başlangıç durumunu görmek için. Projeye sağ tıklayın, seçin **NuGet paketlerini Yönet**üzerinde nuget.org ELMAH için gözatın ve en son sürümünü yükleyin. Yapılan tüm değişiklikler fark `web.config`. Şimdi paketi kaldırma ve gördüğünüz `web.config` önceki durumuna geri çevirin.

### <a name="xdt-transforms"></a>XDT dönüşümler

Yapılandırma dosyaları kullanılarak değiştirebileceğiniz [XDT sözdizimi](https://msdn.microsoft.com/library/dd465326.aspx). Ayrıca belirteçleri ile değiştir NuGet olabilir [proje özellikleri](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) içinde özellik adı ekleyerek `$` sınırlayıcı (büyük küçük harf duyarsız).

Örneğin, aşağıdaki `app.config.install.xdt` dosya ekler bir `appSettings` öğesine `app.config` içeren `FullPath`, `FileName`, ve `ActiveConfigurationSettings` projeden değerler:

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

Başka bir örnek için projeyi başlangıçta aşağıdaki içeriği içeren varsayalım `web.config`:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

Eklemek için bir `MyNuModule` öğesine `modules` bölüm paket sırasında yükleme, paketin `web.config.install.xdt` aşağıdakileri içerir:

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

Paket yüklendikten sonra `web.config` şuna benzeyecektir:

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

Yalnızca kaldırmak için `MyNuModule` paketi kaldırma sırasında öğesi `web.config.uninstall.xdt` dosyası şunları içermelidir:

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
