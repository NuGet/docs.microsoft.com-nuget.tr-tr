---
title: NuGet paketleri için kaynak ve config dosya dönüşümleri
description: NuGet paketlerinin yüklendiğinde kaynak kodu ve yapılandırma (XML) dosyalarını dönüştürme yeteneğiyle ilgili ayrıntılar.
author: karann-msft
ms.author: karann
ms.date: 04/24/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 2fefd9cff4d151111023521c31d58878743775bf
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231181"
---
# <a name="transforming-source-code-and-configuration-files"></a>Kaynak kodu ve yapılandırma dosyalarını dönüştürme

**Kaynak kodu dönüştürme,** paketin `content` veya `contentFiles` klasöründeki dosyalara tek`content` yönlü belirteç `packages.config` `contentFiles` değiştirme `PackageReference`(paket yüklendiğinde ve için) için, jetonların Visual Studio [proje özelliklerine](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7)atıfta bulunduğu dosyalara tek yönlü belirteç değiştirme uygular. Bu, projenin ad alanına bir dosya eklemenize veya genellikle ASP.NET bir `global.asax` projede girecek kodu özelleştirmenize olanak tanır.

**Config dosyası dönüştürme,** hedef projede zaten var olan dosyaları `web.config` `app.config`değiştirmenize olanak tanır. Örneğin, paketinizin config dosyasındaki `modules` bölüme bir öğe eklemesi gerekebilir. Bu dönüştürme, yapılandırma dosyalarına eklenecek bölümleri açıklayan pakete özel dosyalar eklenerek yapılır. Bir paket kaldırıldığında, aynı değişiklikler daha sonra tersine çevrilerek bu iki yönlü bir dönüştürme haline getirir.

## <a name="specifying-source-code-transformations"></a>Kaynak kodu dönüşümlerini belirtme

1. Paketten projeye eklemek istediğiniz dosyalar paketin `content` ve `contentFiles` klasörlerin içinde olmalıdır. Örneğin, çağrılan `ContosoData.cs` bir dosyanın hedef projenin bir `Models` klasörüne yüklenmesini istiyorsanız, dosyanın `content\Models` paketteki ve `contentFiles\{lang}\{tfm}\Models` klasörlerin içinde olması gerekir.

1. NuGet'e yükleme zamanında belirteç değiştirme `.pp` uygulaması talimatı vermek için kaynak kodu dosya adını ekleyebilir. Yüklemeden sonra, dosya uzantısı `.pp` olmayacaktır.

    Örneğin, dönüşümler yapmak `ContosoData.cs`için , paketteki `ContosoData.cs.pp`dosyayı adlandırın. Kurulumdan sonra . `ContosoData.cs`

1. Kaynak kod dosyasında, NuGet'in proje özellikleriyle `$token$` değiştirmesi gereken değerleri belirtmek için formun büyük/küçük harf duyarlı belirteçlerini kullanın:

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

    Yükleme üzerine, NuGet `$rootnamespace$` `Fabrikam` hedef projenin kök ad alanı olduğunu `Fabrikam`varsayarak değiştirir.

Belirteç `$rootnamespace$` en yaygın olarak kullanılan proje özelliğidir; diğerleri [proje özelliklerinde](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7)listelenir. Elbette, bazı özelliklerin proje türüne özgü olabileceğine dikkat edin.

## <a name="specifying-config-file-transformations"></a>Config dosya dönüşümlerini belirtme

Takip eden bölümlerde açıklandığı gibi, config dosya dönüşümleri iki şekilde yapılabilir:

- Uzantı, Paket yüklü `content` olduğunda varolan config dosyalarıyla birleştirmek için Bu dosyaların XML içerdiğini NuGet'e söylediği paketin klasörüne `web.config.transform` ve dosyalarını ekleyin. `app.config.transform` `.transform` Bir paket kaldırıldığında, aynı XML kaldırılır.
- İstediğindeğişiklikleri `web.config.install.xdt` açıklamak için [XDT sözdizimini](https://msdn.microsoft.com/library/dd465326.aspx) kullanarak paketinizin `content` klasörüne dosya ekleyin `app.config.install.xdt` ve dosya ekleyin. Bu seçenekle, paket `.uninstall.xdt` projeden kaldırıldığında değişiklikleri tersine çevirecek bir dosya da ekleyebilirsiniz.

> [!Note]
> Dönüşümler Visual Studio'da `.config` bağlantı olarak başvurulan dosyalara uygulanmaz.

XDT kullanmanın avantajı, yalnızca iki statik dosyayı birleştirmek yerine, tam XPath desteğini kullanarak öğe ve öznitelik eşleştirme kullanarak Bir XML DOM yapısını işlemek için bir sözdizimi sağlamasıdır. XDT daha sonra öğeleri ekleyebilir, güncelleyebilir veya kaldırabilir, belirli bir konuma yeni öğeler yerleyebilir veya öğeleri değiştirebilir/kaldırabilir (alt düğümler dahil). Bu, paket yükleme sırasında yapılan tüm dönüşümleri geri kaldıran kaldırma dönüşümleri oluşturmayı kolaylaştırır.

### <a name="xml-transforms"></a>XML dönüştürür

Ve `app.config.transform` `web.config.transform` bir paketin `content` klasöründe yalnızca projenin varolan `app.config` ve `web.config` dosyaları birleştirmek için bu öğeleri içerir.

Örnek olarak, projenin başlangıçta aşağıdaki içeriği `web.config`içerdiğini varsayalım:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

Paket yükleme `MyNuModule` sırasında `modules` bölüme bir öğe `web.config.transform` eklemek için, paketin `content` klasöründe aşağıdaki gibi görünen bir dosya oluşturun:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

NuGet paketi `web.config` yükledikten sonra aşağıdaki gibi görünür:

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

`modules` NuGet'in bölümün yerini almadığını, yalnızca yeni öğeler ve öznitelikler ekleyerek yeni girişi birleştirdiğini fark edin. NuGet varolan öğeleri veya öznitelikleri değiştirmez.

Paket kaldırıldığında, NuGet `.transform` dosyaları yeniden inceler ve içerdiği öğeleri uygun `.config` dosyalardan kaldırır. Bu `.config` işlemin, paket yüklemeden sonra değiştirdiğiniz dosyadaki satırları etkilemeyeceğini unutmayın.

Daha kapsamlı bir örnek olarak, [ASP.NET için Hata Günlüğü Modülleri ve İşleyiciler (ELMAH)](https://www.nuget.org/packages/elmah/) paketi, bir paket kaldırıldığında yeniden kaldırılan `web.config`birçok giriş ekler.

Dosyasını `web.config.transform` incelemek için, elmah paketini yukarıdaki bağlantıdan indirin, paket uzantısını ''dan `.nupkg` ' ''a `.zip`çevirin ve sonra o ZIP dosyasında açın. `content\web.config.transform`

Paketi yükleme ve kaldırma nın etkisini görmek için Visual Studio'da yeni bir ASP.NET projesi oluşturun (şablon Yeni Proje iletişim kutusunda **Visual C# > Web** altındadır) ve boş bir ASP.NET uygulaması seçin. İlk `web.config` durumunu görmek için açın. Ardından projeyi sağ tıklatın, **NuGet Paketlerini Yönet'i**seçin, nuget.org'da ELMAH'a göz atın ve en son sürümü yükleyin. Tüm değişikliklere `web.config`dikkat edin. Şimdi paketi kaldırın ve `web.config` önceki durumuna geri dönmek bakın.

### <a name="xdt-transforms"></a>XDT dönüştürür

> [!Note]
> Aşağıda açıklandığı gibi , XDT [dönüşümleri geçiş `packages.config` `PackageReference`için dokümanların paket uyumluluk sorunları bölümünde ](../consume-packages/migrate-packages-config-to-package-reference.md#package-compatibility-issues)belirtildiği gibi `packages.config`sadece desteklenir . Aşağıdaki dosyaları paketinize eklerseniz, paketinizi `PackageReference` kullanan tüketiciler dönüşümleri uygulamaz (XDT dönüşümlerinin işe yaraması için bu [örneğe](https://github.com/NuGet/Samples/tree/master/XDTransformExample) `PackageReference`bakın).

[XDT sözdizimini](https://msdn.microsoft.com/library/dd465326.aspx)kullanarak config dosyalarını değiştirebilirsiniz. Ayrıca, nuget belirteçleri [proje özellikleri](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) ile delimiters `$` (büyük/küçük harf duyarsız) içinde özellik adını ekleyerek değiştirebilirsiniz.

`app.config.install.xdt` Örneğin, aşağıdaki dosya projeden `appSettings` `app.config` `FullPath`, ve `FileName` `ActiveConfigurationSettings` değerleri içeren bir öğe ekler:

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

Başka bir örnek olarak, projenin başlangıçta `web.config`aşağıdaki içeriği içerdiğini varsayalım:

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

Paket yükleme `MyNuModule` sırasında `modules` bölüme bir öğe eklemek `web.config.install.xdt` için, paketin aşağıdakileri içerir:

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

Paketi yükledikten `web.config` sonra, bu gibi görünecektir:

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

Paket kaldırma `MyNuModule` sırasında yalnızca öğeyi `web.config.uninstall.xdt` kaldırmak için dosya aşağıdakileri içermelidir:

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
