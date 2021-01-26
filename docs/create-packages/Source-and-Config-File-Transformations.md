---
title: NuGet paketleri için kaynak ve yapılandırma dosyası dönüşümleri
description: NuGet paketlerinin yüklenirken kaynak kodu ve yapılandırma (XML) dosyalarını dönüştürme yeteneği hakkında ayrıntılı bilgi.
author: JonDouglas
ms.author: jodou
ms.date: 04/24/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 5bd0e409f527fb668008204fb16ad002f4784c46
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774585"
---
# <a name="transforming-source-code-and-configuration-files"></a>Kaynak kodu ve yapılandırma dosyalarını dönüştürme

**Kaynak kodu dönüştürmesi** , paket `content` `contentFiles` `content` `packages.config` `contentFiles` `PackageReference` yüklendiğinde, belirtecin Visual Studio [Proje özelliklerine](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7)başvurduğu paketin veya klasördeki dosyalara tek yönlü belirteç değişimini uygular (ve için kullanan müşteriler için). Bu, projenin ad alanına bir dosya eklemenize veya tipik `global.asax` olarak bir ASP.net projesinde gidilecek kodu özelleştirmenize olanak sağlar.

Bir **yapılandırma dosyası dönüştürmesi** , ve gibi bir hedef projede zaten mevcut olan dosyaları değiştirmenize izin verir `web.config` `app.config` . Örneğin, paketinizin yapılandırma dosyasındaki bölümüne bir öğe eklemesi gerekebilir `modules` . Bu dönüşüm, yapılandırma dosyalarına eklenecek bölümleri tanımlayan paketteki özel dosyalar eklenerek yapılır. Bir paket kaldırıldığında, bu değişiklikler iki yönlü bir dönüşüm yaparak ters çevrilir.

## <a name="specifying-source-code-transformations"></a>Kaynak kodu dönüşümlerini belirtme

1. Paketten projeye eklemek istediğiniz dosyalar, paket `content` ve klasörler içinde bulunmalıdır `contentFiles` . Örneğin, adlı bir dosyanın `ContosoData.cs` `Models` hedef projenin bir klasörüne yüklenmesini istiyorsanız, `content\Models` paketin içinde ve klasörlerinde olması gerekir `contentFiles\{lang}\{tfm}\Models` .

1. NuGet 'in yüklemesi sırasında belirteç değişimini uygulamasına bildirmek için `.pp` kaynak kodu dosya adına ekleyin. Yüklemeden sonra, dosya uzantıya sahip olmaz `.pp` .

    Örneğin, içinde dönüşümler yapmak için `ContosoData.cs` dosyayı pakette adlandırın `ContosoData.cs.pp` . Yükleme sonrasında, olarak görünür `ContosoData.cs` .

1. Kaynak kodu dosyasında, `$token$` NuGet 'in proje özellikleriyle değiştirmek zorunda olduğu değerleri belirtmek için formun büyük/küçük harfe duyarsız belirteçlerini kullanın:

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

    Yükleme sonrasında NuGet, `$rootnamespace$` `Fabrikam` hedef projenin kök ad alanı olduğu varsayımıyla değiştirilir `Fabrikam` .

`$rootnamespace$`Belirteç en yaygın olarak kullanılan proje özelliğidir; diğerleri [proje özelliklerinde](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7)listelenir. Kuşkusuz, bazı özelliklerin proje türüne özgü olabileceğini unutmayın.

## <a name="specifying-config-file-transformations"></a>Yapılandırma dosyası dönüşümlerini belirtme

Aşağıdaki bölümlerde açıklandığı gibi, yapılandırma dosyası dönüştürmeleri iki şekilde yapılabilir:

- Paketin `app.config.transform` , `web.config.transform` `content` `.transform` paketin yüklendiği sırada var olan yapılandırma dosyalarıyla birleştirmek için bu dosyaların NuGet 'e söylemiş olduğunu ve paketinizin klasörüne dosya ekleyin. Bir paket kaldırıldığında aynı XML kaldırılır.
- `app.config.install.xdt` `web.config.install.xdt` `content` İstenen değişiklikleri anlatmak için [xdt söz dizimini](/previous-versions/aspnet/dd465326(v=vs.110)) kullanarak paketinizin klasörüne ve dosyalarını ekleyin. Bu seçenekle `.uninstall.xdt` , paket bir projeden kaldırıldığında ters değişiklikler için bir dosya de ekleyebilirsiniz.

> [!Note]
> Dönüşümler, `.config` Visual Studio 'da bağlantı olarak başvurulan dosyalara uygulanmaz.

XDT kullanmanın avantajı, yalnızca iki statik dosyayı birleştirmek yerine, bir XML DOM yapısını, tam XPath desteği kullanılarak öğe ve öznitelik eşleştirme kullanarak işlemek için bir sözdizimi sağlar. XDT daha sonra öğeleri ekleyebilir, güncelleştirebilir veya kaldırabilir, belirli bir konuma yeni öğeleri yerleştirebilir veya öğeleri (alt düğümler dahil) değiştirebilir/kaldırabilir. Bu, paket yüklemesi sırasında yapılan tüm dönüştürmeleri geri yükleyen kaldırma dönüştürmeleri oluşturmayı basit hale getirir.

### <a name="xml-transforms"></a>XML dönüşümleri

`app.config.transform` `web.config.transform` Bir paketin klasöründe ve, `content` yalnızca projenin var olan ve dosyalarında birleştirilecek öğeleri içerir `app.config` `web.config` .

Örnek olarak, projenin başlangıçta aşağıdaki içeriği içerdiğini varsayın `web.config` :

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

`MyNuModule` `modules` Paket yüklemesi sırasında bölüme bir öğe eklemek için, paketin klasöründe şuna benzeyen bir `web.config.transform` dosya oluşturun `content` :

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

NuGet 'in bölümün yerini değiştirmediğine dikkat edin `modules` , yalnızca yeni öğeler ve öznitelikler ekleyerek yalnızca yeni girişi birleştirir. NuGet, varolan herhangi bir öğeyi veya özniteliği değiştirmez.

Paket kaldırıldığında, NuGet `.transform` dosyaları yeniden inceler ve içerdiği öğeleri uygun `.config` dosyalardan kaldırır. Bu işlemin, `.config` dosyadaki paket yüklemesinden sonra değişiklik yaptığınız herhangi bir satırı etkilemeyeceğini unutmayın.

Daha kapsamlı bir örnek olarak, [ASP.net (ELMAH) paketi Için hata günlüğü modülleri ve işleyiciler](https://www.nuget.org/packages/elmah/) , `web.config` ' a bir paket kaldırıldığında yeniden kaldırılan birçok giriş ekler.

Dosyasını incelemek için `web.config.transform` Yukarıdaki bağlantıdan ELMAH paketini indirin, paket uzantısını `.nupkg` olarak olarak değiştirin `.zip` ve ardından `content\web.config.transform` Bu ZIP dosyasında açın.

Paketi yükleme ve kaldırma etkisini görmek için, Visual Studio 'da yeni bir ASP.NET projesi oluşturun (şablon, yeni proje iletişim kutusunda **visual C# > Web** altında bulunur) ve boş bir ASP.NET uygulaması seçin. `web.config`İlk durumunu görmek için açın. Ardından projeye sağ tıklayın, **NuGet Paketlerini Yönet**' i seçin, NuGet.org üzerinde ELMAH için gezinme yapın ve en son sürümü yükler. Tüm değişiklikleri unutmayın `web.config` . Şimdi paketi kaldırın ve `web.config` önceki durumuna geri dönün.

### <a name="xdt-transforms"></a>XDT dönüşümleri

> [!Note]
> ' [Dan `packages.config` `PackageReference` ' a geçiş için docs 'ın paket uyumluluk sorunları bölümünde ](../consume-packages/migrate-packages-config-to-package-reference.md#package-compatibility-issues)belirtildiği gibi, aşağıda açıklandığı gibi xdt dönüştürmeleri yalnızca tarafından desteklenir `packages.config` . Aşağıdaki dosyaları paketinize eklerseniz, paketinizi kullanan tüketiciler, `PackageReference` Dönüştürmelere uygulanmaz (XDT dönüştürmelerinin birlikte çalışmasını sağlamak için [Bu örneğe](https://github.com/NuGet/Samples/tree/master/XDTransformExample) başvurun `PackageReference` ).

[Xdt sözdizimini](/previous-versions/aspnet/dd465326(v=vs.110))kullanarak yapılandırma dosyalarını değiştirebilirsiniz. Ayrıca, sınırlayıcıları (büyük/küçük harfe duyarsız) içinde özellik adını ekleyerek NuGet 'in belirteçleri [Proje özellikleriyle](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) değiştirmesini sağlayabilirsiniz `$` .

Örneğin, aşağıdaki `app.config.install.xdt` Dosya `appSettings` `app.config` `FullPath` `FileName` projedeki, ve değerlerini içeren içine bir öğesi ekleyecektir `ActiveConfigurationSettings` :

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

Başka bir örnek için, projenin başlangıçta aşağıdaki içeriği içerdiğini varsayalım `web.config` :

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

`MyNuModule` `modules` Paket yüklemesi sırasında bölüme bir öğe eklemek için, paket `web.config.install.xdt` şunları içerir:

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

Paketi yükledikten sonra şöyle `web.config` görünür:

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

Yalnızca `MyNuModule` paketi kaldırma sırasında öğeyi kaldırmak için, `web.config.uninstall.xdt` Dosya şunları içermelidir:

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