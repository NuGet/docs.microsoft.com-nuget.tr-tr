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
# <a name="transforming-source-code-and-configuration-files"></a><span data-ttu-id="a44e9-103">Kaynak kodu ve yapılandırma dosyaları dönüştürme</span><span class="sxs-lookup"><span data-stu-id="a44e9-103">Transforming source code and configuration files</span></span>

<span data-ttu-id="a44e9-104">Kullanarak projeleri için `packages.config`, NuGet kaynak koda dönüştürme yapma yeteneğini destekler ve paket konumundaki yapılandırma dosyalarını yükler ve kez kaldırın.</span><span class="sxs-lookup"><span data-stu-id="a44e9-104">For projects using `packages.config`, NuGet supports the ability to make transformations to source code and configuration files at package install and uninstall times.</span></span> <span data-ttu-id="a44e9-105">Bir paketi kullanarak bir proje yüklendiğinde yalnızca kaynak kodu dönüşümleri uygulanır [PackageReference](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="a44e9-105">Only Source code transformations are applied when a package is installed in a project using [PackageReference](../consume-packages/package-references-in-project-files.md).</span></span>

<span data-ttu-id="a44e9-106">A **kaynak kodu dönüştürme** paketin dosyalarda tek yönlü belirteç değiştirme uygulandığı `content` veya `contentFiles` klasörü (`content` kullanan müşteriler için `packages.config` ve `contentFiles` için`PackageReference`) paketi yüklendiğinde, burada belirteçleri başvurmak için Visual Studio [proje özellikleri](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span><span class="sxs-lookup"><span data-stu-id="a44e9-106">A **source code transformation** applies one-way token replacement to files in the package's `content` or `contentFiles` folder (`content` for customers using `packages.config` and `contentFiles` for `PackageReference`) when the package is installed, where tokens refer to Visual Studio [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span></span> <span data-ttu-id="a44e9-107">Bu projenin ad alanına bir dosya eklemek için ya da genellikle içine çıkacak kod özelleştirmenizi sağlar `global.asax` bir ASP.NET projesi içinde.</span><span class="sxs-lookup"><span data-stu-id="a44e9-107">This allows you to insert a file into the project's namespace, or to customize code that would typically go into `global.asax` in an ASP.NET project.</span></span>

<span data-ttu-id="a44e9-108">A **config dosya dönüştürme** zaten bir hedef projesinde gibi mevcut dosyaları değiştirebilmenizi sağlar `web.config` ve `app.config`.</span><span class="sxs-lookup"><span data-stu-id="a44e9-108">A **config file transformation** allows you to modify files that already exist in a target project, such as `web.config` and `app.config`.</span></span> <span data-ttu-id="a44e9-109">Örneğin, paketinizin bir öğeye eklemeniz gerekebilir `modules` bölümünde yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="a44e9-109">For example, your package might need to add an item to the `modules` section in the config file.</span></span> <span data-ttu-id="a44e9-110">Bu dönüştürme için yapılandırma dosyalarını eklemek bölümlerde paketinde özel dosyaları ekleyerek gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="a44e9-110">This transformation is done by including special files in the package that describe the sections to add to the configuration files.</span></span> <span data-ttu-id="a44e9-111">Bir paket kaldırıldığında, aynı değişiklikleri daha sonra bu iki yönlü bir dönüştürme yapma ters çevrilir.</span><span class="sxs-lookup"><span data-stu-id="a44e9-111">When a package is uninstalled, those same changes are then reversed, making this a two-way transformation.</span></span>

## <a name="specifying-source-code-transformations"></a><span data-ttu-id="a44e9-112">Kaynak kodu dönüşümleri belirtme</span><span class="sxs-lookup"><span data-stu-id="a44e9-112">Specifying source code transformations</span></span>

1. <span data-ttu-id="a44e9-113">Paketten projeye eklemek istediğiniz dosya paketin içinde bulunduğu olmalıdır `content` ve `contentFiles` klasörleri.</span><span class="sxs-lookup"><span data-stu-id="a44e9-113">Files that you want to insert from the package into the project must be located within the package's `content` and `contentFiles` folders.</span></span> <span data-ttu-id="a44e9-114">Adlı bir dosya istiyorsanız, örneğin, `ContosoData.cs` yüklenmesi bir `Models` klasörü hedef projenin olmalıdır içinde `content\Models` ve `contentFiles\{lang}\{tfm}\Models` paketteki klasörleri.</span><span class="sxs-lookup"><span data-stu-id="a44e9-114">For example, if you want a file called `ContosoData.cs` to be installed in a `Models` folder of the target project, it must be inside the `content\Models` and `contentFiles\{lang}\{tfm}\Models` folders in the package.</span></span>

1. <span data-ttu-id="a44e9-115">Yükleme sırasında belirteç değiştirme uygulamak için NuGet bileşenine ekleme `.pp` kaynak kod dosya adı.</span><span class="sxs-lookup"><span data-stu-id="a44e9-115">To instruct NuGet to apply token replacement at install time, append `.pp` to the source code file name.</span></span> <span data-ttu-id="a44e9-116">Yüklemeden sonra dosya olmayacaktır `.pp` uzantısı.</span><span class="sxs-lookup"><span data-stu-id="a44e9-116">After installation, the file will not have the `.pp` extension.</span></span>

    <span data-ttu-id="a44e9-117">Örneğin dönüşümlerini yapmak `ContosoData.cs`, paketteki dosya adı `ContosoData.cs.pp`.</span><span class="sxs-lookup"><span data-stu-id="a44e9-117">For example, to make transformations in `ContosoData.cs`, name the file in the package `ContosoData.cs.pp`.</span></span> <span data-ttu-id="a44e9-118">Yükleme sonrasında olarak görünür `ContosoData.cs`.</span><span class="sxs-lookup"><span data-stu-id="a44e9-118">After installation it will appear as `ContosoData.cs`.</span></span>

1. <span data-ttu-id="a44e9-119">Kaynak kodu dosyasında biçiminin büyük küçük harf duyarsız belirteçleri kullanmasını `$token$` değerleri göstermek için NuGet ile proje özelliklerini değiştirmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="a44e9-119">In the source code file, use case-insensitive tokens of the form `$token$` to indicate values that NuGet should replace with project properties:</span></span>

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

    <span data-ttu-id="a44e9-120">Yükleme işleminden sonra NuGet değiştirir `$rootnamespace$` ile `Fabrikam` hedef projeye varsayılarak kullanıcının Kök ad alanı olan `Fabrikam`.</span><span class="sxs-lookup"><span data-stu-id="a44e9-120">Upon installation, NuGet replaces `$rootnamespace$` with `Fabrikam` assuming the target project's whose root namespace is `Fabrikam`.</span></span>

<span data-ttu-id="a44e9-121">`$rootnamespace$` Belirteci en yaygın olarak kullanılan proje özelliği; diğer tüm listelenen [proje özellikleri](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span><span class="sxs-lookup"><span data-stu-id="a44e9-121">The `$rootnamespace$` token is the most commonly used project property; all others are listed in [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span></span> <span data-ttu-id="a44e9-122">Elbette, bazı özellikleri proje türüne özgü olabilir oluşturduğunu, unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a44e9-122">Be mindful, of course, that some properties might be specific to the project type.</span></span>

## <a name="specifying-config-file-transformations"></a><span data-ttu-id="a44e9-123">Yapılandırma dosyası dönüşümleri belirtme</span><span class="sxs-lookup"><span data-stu-id="a44e9-123">Specifying config file transformations</span></span>

<span data-ttu-id="a44e9-124">İzleyen bölümlerde açıklandığı gibi yapılandırma dosyası dönüşümleri iki şekilde gerçekleştirilebilir:</span><span class="sxs-lookup"><span data-stu-id="a44e9-124">As described in the sections that follow, config file transformations can be done in two ways:</span></span>

- <span data-ttu-id="a44e9-125">Dahil `app.config.transform` ve `web.config.transform` paketinizin dosyalarında `content` klasörü, burada `.transform` uzantısı NuGet paketi yüklendiğinde var olan yapılandırma dosyaları ile birleştirmek için XML bu dosyaları içermesini söyler.</span><span class="sxs-lookup"><span data-stu-id="a44e9-125">Include `app.config.transform` and `web.config.transform` files in your package's `content` folder, where the `.transform` extension tells NuGet that these files contain the XML to merge with existing config files when the package is installed.</span></span> <span data-ttu-id="a44e9-126">Bir paket kaldırıldığında, aynı XML kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="a44e9-126">When a package is uninstalled, that same XML is removed.</span></span>
- <span data-ttu-id="a44e9-127">Dahil `app.config.install.xdt` ve `web.config.install.xdt` paketinizin dosyalarında `content` klasöründe kullanarak [XDT söz dizimi](https://msdn.microsoft.com/library/dd465326.aspx) istenen değişiklikleri açıklamak için.</span><span class="sxs-lookup"><span data-stu-id="a44e9-127">Include `app.config.install.xdt` and `web.config.install.xdt` files in your package's `content` folder, using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx) to describe the desired changes.</span></span> <span data-ttu-id="a44e9-128">Bu seçenekle da dahil edebilirsiniz bir `.uninstall.xdt` paket bir projeden kaldırıldığında değişiklikleri geri almak için dosya.</span><span class="sxs-lookup"><span data-stu-id="a44e9-128">With this option you can also include a `.uninstall.xdt` file to reverse changes when the package is removed from a project.</span></span>

> [!Note]
> <span data-ttu-id="a44e9-129">Dönüştürmeleri için uygulanmaz `.config` Visual Studio'da bir bağlantı olarak başvurulan dosyaları.</span><span class="sxs-lookup"><span data-stu-id="a44e9-129">Transformations are not applied to `.config` files referenced as a link in Visual Studio.</span></span>

<span data-ttu-id="a44e9-130">XDT kullanmanın avantajı yalnızca iki statik dosyaları birleştirme yerine, bunu bir sözdizimi bir XML DOM öğesi ve öznitelik XPath için tam destek kullanarak eşleşen kullanarak yapısını işlemek için sağlamasıdır.</span><span class="sxs-lookup"><span data-stu-id="a44e9-130">The advantage of using XDT is that instead of simply merging two static files, it provides a syntax for manipulating the structure of an XML DOM using element and attribute matching using full XPath support.</span></span> <span data-ttu-id="a44e9-131">XDT ardından ekleme, güncelleştirme veya öğeleri kaldırın, yeni öğeleri belirli bir konuma yerleştirin veya (alt düğümler dahil olmak üzere) öğeleri Değiştir/Kaldır.</span><span class="sxs-lookup"><span data-stu-id="a44e9-131">XDT can then add, update, or remove elements, place new elements at a specific location, or replace/remove elements (including child nodes).</span></span> <span data-ttu-id="a44e9-132">Bu, paket yükleme sırasında yapılan tüm dönüştürmeler geri kaldırma dönüşümler oluşturmak basit kılar.</span><span class="sxs-lookup"><span data-stu-id="a44e9-132">This makes it straightforward to create uninstall transforms that back out all transformations done during package installation.</span></span>

### <a name="xml-transforms"></a><span data-ttu-id="a44e9-133">XML dönüşümleri</span><span class="sxs-lookup"><span data-stu-id="a44e9-133">XML transforms</span></span>

<span data-ttu-id="a44e9-134">`app.config.transform` Ve `web.config.transform` bir paketin içinde `content` klasörü içeren proje mevcut birleştirmek için yalnızca bu öğeleri `app.config` ve `web.config` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="a44e9-134">The `app.config.transform` and `web.config.transform` in a package's `content` folder contain only those elements to merge into the project's existing `app.config` and `web.config` files.</span></span>

<span data-ttu-id="a44e9-135">Örneğin, proje, başlangıçta aşağıdaki içeriği içerdiğini varsayın `web.config`:</span><span class="sxs-lookup"><span data-stu-id="a44e9-135">As an example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="a44e9-136">Eklemek için bir `MyNuModule` öğesine `modules` bölümünde paket yükleme sırasında oluşturun bir `web.config.transform` paketin dosyasında `content` şuna benzer bir klasörü:</span><span class="sxs-lookup"><span data-stu-id="a44e9-136">To add a `MyNuModule` element to the `modules` section during package install, create a `web.config.transform` file in the package's `content` folder that looks like this:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="a44e9-137">NuGet paket yüklendikten sonra `web.config` şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="a44e9-137">After NuGet installs the package, `web.config` will appear as follows:</span></span>

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

<span data-ttu-id="a44e9-138">NuGet değiştirmek istemediğiniz bildirimi `modules` bölümünde, yalnızca birleştirilen yeni girişine yalnızca yeni öğeler ve öznitelikler ekleyerek.</span><span class="sxs-lookup"><span data-stu-id="a44e9-138">Notice that NuGet didn't replace the `modules` section, it just merged the new entry into it by adding only new elements and attributes.</span></span> <span data-ttu-id="a44e9-139">NuGet, tüm mevcut öğeler ve öznitelikler değişmez.</span><span class="sxs-lookup"><span data-stu-id="a44e9-139">NuGet will not change any existing elements or attributes.</span></span>

<span data-ttu-id="a44e9-140">NuGet Paketi kaldırıldığında inceleyeceksiniz `.transform` yeniden dosyaları ve içerdiği öğeleri uygun kaldırmak `.config` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="a44e9-140">When the package is uninstalled, NuGet will examine the `.transform` files again and remove the elements it contains from the appropriate `.config` files.</span></span> <span data-ttu-id="a44e9-141">Bu işlem tüm satırları etkilemez Not `.config` paket yükleme sonrasında değiştirmek dosya.</span><span class="sxs-lookup"><span data-stu-id="a44e9-141">Note that this process will not affect any lines in the `.config` file that you modify after package installation.</span></span>

<span data-ttu-id="a44e9-142">Daha kapsamlı bir örnek olarak [hata günlüğü modüller ve işleyiciler için ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) paket birçok girişleri ekler `web.config`, hangi yeniden kaldırılır bir paket kaldırıldığında.</span><span class="sxs-lookup"><span data-stu-id="a44e9-142">As a more extensive example, the [Error Logging Modules and Handlers for ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) package adds many entries into `web.config`, which are again removed when a package is uninstalled.</span></span>

<span data-ttu-id="a44e9-143">İncelemek için kendi `web.config.transform` dosya, yukarıdaki bağlantıdan ELMAH paketini indirmek, paket uzantısını değiştirme `.nupkg` için `.zip`ve ardından açın `content\web.config.transform` bu ZIP dosyasında.</span><span class="sxs-lookup"><span data-stu-id="a44e9-143">To examine its `web.config.transform` file, download the ELMAH package from the link above, change the package extension from `.nupkg` to `.zip`, and then open `content\web.config.transform` in that ZIP file.</span></span>

<span data-ttu-id="a44e9-144">Yükleme ve paket kaldırma etkisini görmek için Visual Studio'da yeni bir ASP.NET projesi oluşturma (şablon altındadır **Visual C# > Web** yeni proje iletişim kutusunda), boş bir ASP.NET uygulaması seçin.</span><span class="sxs-lookup"><span data-stu-id="a44e9-144">To see the effect of installing and uninstalling the package, create a new ASP.NET project in Visual Studio (the template is under **Visual C# > Web** in the New Project dialog), and select an empty ASP.NET application.</span></span> <span data-ttu-id="a44e9-145">Açık `web.config` başlangıç durumunu görmek için.</span><span class="sxs-lookup"><span data-stu-id="a44e9-145">Open `web.config` to see its initial state.</span></span> <span data-ttu-id="a44e9-146">Daha sonra projeye sağ tıklayın, **NuGet paketlerini Yönet**ELMAH için nuget.org adresinden göz atın ve en son sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="a44e9-146">Then right-click the project, select **Manage NuGet Packages**, browse for ELMAH on nuget.org, and install the latest version.</span></span> <span data-ttu-id="a44e9-147">Yapılan tüm değişiklikler fark `web.config`.</span><span class="sxs-lookup"><span data-stu-id="a44e9-147">Notice all the changes to `web.config`.</span></span> <span data-ttu-id="a44e9-148">Artık paketi kaldırın ve gördüğünüz `web.config` önceki durumuna geri döndürme.</span><span class="sxs-lookup"><span data-stu-id="a44e9-148">Now uninstall the package and you see `web.config` revert to its prior state.</span></span>

### <a name="xdt-transforms"></a><span data-ttu-id="a44e9-149">XDT dönüşümler</span><span class="sxs-lookup"><span data-stu-id="a44e9-149">XDT transforms</span></span>

<span data-ttu-id="a44e9-150">Yapılandırma dosyalarını kullanarak değiştirebileceğiniz [XDT söz dizimi](https://msdn.microsoft.com/library/dd465326.aspx).</span><span class="sxs-lookup"><span data-stu-id="a44e9-150">You can modify config files using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx).</span></span> <span data-ttu-id="a44e9-151">NuGet belirteçleri ile değiştirin bulundurabilirsiniz [proje özellikleri](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) içinde özellik adı ekleyerek `$` sınırlayıcılar (büyük-küçük harf duyarsız).</span><span class="sxs-lookup"><span data-stu-id="a44e9-151">You can also have NuGet replace tokens with [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) by including the property name within `$` delimiters (case-insensitive).</span></span>

<span data-ttu-id="a44e9-152">Örneğin, aşağıdaki `app.config.install.xdt` dosyası ekler bir `appSettings` öğesine `app.config` içeren `FullPath`, `FileName`, ve `ActiveConfigurationSettings` projesinden değerleri:</span><span class="sxs-lookup"><span data-stu-id="a44e9-152">For example, the following `app.config.install.xdt` file will insert an `appSettings` element into `app.config` containing the `FullPath`, `FileName`, and `ActiveConfigurationSettings` values from the project:</span></span>

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

<span data-ttu-id="a44e9-153">Başka bir örnek için proje, başlangıçta aşağıdaki içeriği içerdiğini varsayın `web.config`:</span><span class="sxs-lookup"><span data-stu-id="a44e9-153">For another example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="a44e9-154">Eklemek için bir `MyNuModule` öğesine `modules` bölüm paket sırasında yükleme, paket `web.config.install.xdt` aşağıdakileri içerir:</span><span class="sxs-lookup"><span data-stu-id="a44e9-154">To add a `MyNuModule` element to the `modules` section during package install, the package's `web.config.install.xdt` would contain the following:</span></span>

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

<span data-ttu-id="a44e9-155">Paket yüklendikten sonra `web.config` şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="a44e9-155">After installing the package, `web.config` will look like this:</span></span>

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

<span data-ttu-id="a44e9-156">Yalnızca kaldırmak için `MyNuModule` öğesi paketi kaldırma sırasında `web.config.uninstall.xdt` dosyası şunları içermelidir:</span><span class="sxs-lookup"><span data-stu-id="a44e9-156">To remove only the `MyNuModule` element during package uninstall, the `web.config.uninstall.xdt` file should contain the following:</span></span>

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
