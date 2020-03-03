---
title: NuGet paketleri için kaynak ve yapılandırma dosyası dönüşümleri
description: NuGet paketlerinin yüklenirken kaynak kodu ve yapılandırma (XML) dosyalarını dönüştürme yeteneği hakkında ayrıntılı bilgi.
author: karann-msft
ms.author: karann
ms.date: 04/24/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 2fefd9cff4d151111023521c31d58878743775bf
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231181"
---
# <a name="transforming-source-code-and-configuration-files"></a>Kaynak kodu ve yapılandırma dosyalarını dönüştürme

**Kaynak kodu dönüştürmesi** , paketin yüklendiği zaman, belirtecin Visual Studio [Proje özelliklerine](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7)başvurduğu, paketin `content` veya `contentFiles` `contentFiles` `packages.config``content` klasöründeki dosyalara tek yönlü belirteç değişikliği uygular.`PackageReference` Bu, projenin ad alanına bir dosya eklemenize veya tipik olarak bir ASP.NET projesinde `global.asax` gidecek kodu özelleştirmenize olanak sağlar.

Bir **yapılandırma dosyası dönüştürmesi** , `web.config` ve `app.config`gibi bir hedef projede zaten mevcut olan dosyaları değiştirmenize izin verir. Örneğin, paketinizin yapılandırma dosyasındaki `modules` bölümüne bir öğe eklemesi gerekebilir. Bu dönüşüm, yapılandırma dosyalarına eklenecek bölümleri tanımlayan paketteki özel dosyalar eklenerek yapılır. Bir paket kaldırıldığında, bu değişiklikler iki yönlü bir dönüşüm yaparak ters çevrilir.

## <a name="specifying-source-code-transformations"></a>Kaynak kodu dönüşümlerini belirtme

1. Paketten projeye eklemek istediğiniz dosyalar paketin `content` ve `contentFiles` klasörlerinde yer almalıdır. Örneğin, `ContosoData.cs` adlı bir dosyanın hedef projenin bir `Models` klasörüne yüklenmesini istiyorsanız, paketin içindeki `content\Models` ve `contentFiles\{lang}\{tfm}\Models` klasörlerin içinde olması gerekir.

1. NuGet 'in, yüklemenin zamanında belirteç değişimini uygulamasını istemek için `.pp` kaynak kodu dosya adına ekleyin. Yüklemeden sonra dosya `.pp` uzantısına sahip olmaz.

    Örneğin, `ContosoData.cs`dönüşümler yapmak için dosyayı paket `ContosoData.cs.pp`olarak adlandırın. Yüklemeden sonra, `ContosoData.cs`olarak görünür.

1. Kaynak kodu dosyasında, NuGet 'in proje özellikleriyle yerine geçecek değerleri belirtmek için `$token$` form büyük/küçük harfe duyarsız belirteçlerini kullanın:

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

    Yükleme sonrasında, NuGet, hedef projenin kök ad alanı `Fabrikam`olan `$rootnamespace$` `Fabrikam` ile değiştirir.

`$rootnamespace$` belirteci en yaygın olarak kullanılan proje özelliğidir; Tüm diğerleri [proje özelliklerinde](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7)listelenir. Kuşkusuz, bazı özelliklerin proje türüne özgü olabileceğini unutmayın.

## <a name="specifying-config-file-transformations"></a>Yapılandırma dosyası dönüşümlerini belirtme

Aşağıdaki bölümlerde açıklandığı gibi, yapılandırma dosyası dönüştürmeleri iki şekilde yapılabilir:

- `app.config.transform` ve `web.config.transform` dosyalarını, paketinizin `content` klasöre ekleyin. burada `.transform` uzantısı, bu dosyaların, paket yüklendiğinde var olan yapılandırma dosyalarıyla birleştirmek için XML içerdiğini NuGet 'e söyler. Bir paket kaldırıldığında aynı XML kaldırılır.
- İstenen değişiklikleri anlatmak için [xdt söz dizimini](https://msdn.microsoft.com/library/dd465326.aspx) kullanarak paketinizin `content` klasöre `app.config.install.xdt` ve `web.config.install.xdt` dosyaları ekleyin. Bu seçenekle, paket bir projeden kaldırıldığında ters değişiklikler için bir `.uninstall.xdt` dosyası da ekleyebilirsiniz.

> [!Note]
> Dönüşümler, Visual Studio 'da bağlantı olarak başvurulan `.config` dosyalarına uygulanmaz.

XDT kullanmanın avantajı, yalnızca iki statik dosyayı birleştirmek yerine, bir XML DOM yapısını, tam XPath desteği kullanılarak öğe ve öznitelik eşleştirme kullanarak işlemek için bir sözdizimi sağlar. XDT daha sonra öğeleri ekleyebilir, güncelleştirebilir veya kaldırabilir, belirli bir konuma yeni öğeleri yerleştirebilir veya öğeleri (alt düğümler dahil) değiştirebilir/kaldırabilir. Bu, paket yüklemesi sırasında yapılan tüm dönüştürmeleri geri yükleyen kaldırma dönüştürmeleri oluşturmayı basit hale getirir.

### <a name="xml-transforms"></a>XML dönüşümleri

Bir paketin `content` klasöründeki `app.config.transform` ve `web.config.transform` yalnızca projenin mevcut `app.config` ve `web.config` dosyalarını birleştirmek için bu öğeleri içerir.

Örnek olarak, projenin başlangıçta `web.config`aşağıdaki içeriği içerdiğini varsayın:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

Paket yüklemesi sırasında `modules` bölümüne `MyNuModule` öğesi eklemek için, paketin `content` klasöründe şuna benzer bir `web.config.transform` dosyası oluşturun:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

NuGet paketi yükledikten sonra `web.config` aşağıdaki gibi görünür:

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

NuGet `modules` bölümünün değiştirmediğine dikkat edin. yalnızca yeni öğeler ve öznitelikler ekleyerek yalnızca yeni girişi birleştirir. NuGet, varolan herhangi bir öğeyi veya özniteliği değiştirmez.

Paket kaldırıldığında, NuGet `.transform` dosyalarını yeniden inceler ve içerdiği öğeleri uygun `.config` dosyalarından kaldırır. Bu işlemin, paket yüklemesinden sonra değiştirdiğiniz `.config` dosyasındaki herhangi bir satırı etkilemeyeceğini unutmayın.

Daha kapsamlı bir örnek olarak, [ASP.net (ELMAH) Için hata günlüğü modülleri ve işleyiciler](https://www.nuget.org/packages/elmah/) , bir paket kaldırıldığında yeniden kaldırılan `web.config`çok sayıda girdi ekler.

`web.config.transform` dosyasını incelemek için Yukarıdaki bağlantıdan ELMAH paketini indirin, `.nupkg` paket uzantısını `.zip`olarak değiştirin ve ardından söz konusu ZIP dosyasında `content\web.config.transform` açın.

Paketi yükleme ve kaldırma etkisini görmek için, Visual Studio 'da yeni bir ASP.NET projesi oluşturun (şablon, yeni proje iletişim kutusunda  **C# Visual > Web** altında bulunur) ve boş bir ASP.NET uygulaması seçin. İlk durumunu görmek için `web.config` açın. Ardından projeye sağ tıklayın, **NuGet Paketlerini Yönet**' i seçin, NuGet.org üzerinde ELMAH için gezinme yapın ve en son sürümü yükler. `web.config`yapılan tüm değişiklikleri fark edin. Şimdi paketi kaldırın ve önceki durumuna geri dönmek `web.config` görürsünüz.

### <a name="xdt-transforms"></a>XDT dönüşümleri

> [!Note]
> [`packages.config` 'den `PackageReference`geçirmek için docs 'ın paket uyumluluk sorunları bölümünde ](../consume-packages/migrate-packages-config-to-package-reference.md#package-compatibility-issues)belirtildiği gibi, aşağıda açıklanan xdt dönüştürmeleri yalnızca `packages.config`tarafından desteklenir. Aşağıdaki dosyaları paketinize eklerseniz, paketinizin `PackageReference` ile kullandığı tüketiciler Dönüştürmelere uygulanmaz (XDT dönüştürmelerinin`PackageReference`ile çalışması için [Bu örneğe](https://github.com/NuGet/Samples/tree/master/XDTransformExample) başvurun).

[Xdt sözdizimini](https://msdn.microsoft.com/library/dd465326.aspx)kullanarak yapılandırma dosyalarını değiştirebilirsiniz. Ayrıca, `$` sınırlayıcıları (büyük/küçük harfe duyarsız) içinde özellik adı ekleyerek NuGet 'in belirteçleri [Proje özellikleriyle](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) değiştirmesini sağlayabilirsiniz.

Örneğin, aşağıdaki `app.config.install.xdt` dosyası, projeden `FullPath`, `FileName`ve `ActiveConfigurationSettings` değerlerini içeren `app.config` bir `appSettings` öğesi ekleyecektir:

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

Başka bir örnek için, projenin başlangıçta `web.config`aşağıdaki içeriği içerdiğini varsayalım:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

Paket yüklemesi sırasında `modules` bölümüne `MyNuModule` öğesi eklemek için, paketin `web.config.install.xdt` şunları içerir:

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

Paketi yükledikten sonra `web.config` şöyle görünür:

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

Paketi kaldırma sırasında yalnızca `MyNuModule` öğesini kaldırmak için `web.config.uninstall.xdt` dosya şunları içermelidir:

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
