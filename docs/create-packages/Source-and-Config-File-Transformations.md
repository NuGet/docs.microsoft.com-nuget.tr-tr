---
title: Kaynak ve yapılandırma dosyası dönüştürmeleri için NuGet paketleri
description: Kaynak kodu ve yapılandırması dönüştürmesini NuGet paketlerini yeteneğine yüklendiğinde (XML) dosyaları ayrıntılarını verir.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 04/24/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 863bf22780313a34690617dd6a1604531272808b
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="transforming-source-code-and-configuration-files"></a><span data-ttu-id="b565d-103">Kaynak kodu ve yapılandırma dosyaları dönüştürme</span><span class="sxs-lookup"><span data-stu-id="b565d-103">Transforming source code and configuration files</span></span>

<span data-ttu-id="b565d-104">Kullanarak projeleri için `packages.config`, NuGet kaynak kodu dönüşümleri yapma yeteneği destekler ve paket yapılandırma dosyaları yükleyip kez kaldırın.</span><span class="sxs-lookup"><span data-stu-id="b565d-104">For projects using `packages.config`, NuGet supports the ability to make transformations to source code and configuration files at package install and uninstall times.</span></span> <span data-ttu-id="b565d-105">Bir paketi kullanarak bir projeye yüklendiğinde yalnızca kaynak kodu dönüşümleri uygulanır [PackageReference](../consume-packages/package-references-in-project-files.md).</span><span class="sxs-lookup"><span data-stu-id="b565d-105">Only Source code transformations are applied when a package is installed in a project using [PackageReference](../consume-packages/package-references-in-project-files.md).</span></span>

<span data-ttu-id="b565d-106">A **kaynak kodu dönüştürme** paketin dosyalarında tek yönlü belirteci değiştirme uygulandığı `content` veya `contentFiles` klasörü (`content` kullanan müşteriler için `packages.config` ve `contentFiles` için`PackageReference`) paketi yüklendiğinde, burada belirteçleri başvurmak için Visual Studio [proje özellikleri](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span><span class="sxs-lookup"><span data-stu-id="b565d-106">A **source code transformation** applies one-way token replacement to files in the package's `content` or `contentFiles` folder (`content` for customers using `packages.config` and `contentFiles` for `PackageReference`) when the package is installed, where tokens refer to Visual Studio [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span></span> <span data-ttu-id="b565d-107">Bu projenin ad alanına bir dosya eklemek için ya da genellikle içine geçecek kod özelleştirmenizi sağlar `global.asax` ASP.NET projesinde.</span><span class="sxs-lookup"><span data-stu-id="b565d-107">This allows you to insert a file into the project's namespace, or to customize code that would typically go into `global.asax` in an ASP.NET project.</span></span>

<span data-ttu-id="b565d-108">A **config dosya dönüşümü** , bir hedef projesinde gibi zaten mevcut dosyaların değiştirmenizi sağlar `web.config` ve `app.config`.</span><span class="sxs-lookup"><span data-stu-id="b565d-108">A **config file transformation** allows you to modify files that already exist in a target project, such as `web.config` and `app.config`.</span></span> <span data-ttu-id="b565d-109">Örneğin, bir öğe eklemek paketinizi gereken `modules` yapılandırma dosyası bölümünde.</span><span class="sxs-lookup"><span data-stu-id="b565d-109">For example, your package might need to add an item to the `modules` section in the config file.</span></span> <span data-ttu-id="b565d-110">Bu dönüştürme için yapılandırma dosyalarını eklemek için bölümlerde paketinde özel dosyaları ekleyerek yapılır.</span><span class="sxs-lookup"><span data-stu-id="b565d-110">This transformation is done by including special files in the package that describe the sections to add to the configuration files.</span></span> <span data-ttu-id="b565d-111">Bir paketi kaldırıldığında, aynı değişiklikleri daha sonra bu iki yönlü bir dönüştürme yapma ters çevrilir.</span><span class="sxs-lookup"><span data-stu-id="b565d-111">When a package is uninstalled, those same changes are then reversed, making this a two-way transformation.</span></span>

## <a name="specifying-source-code-transformations"></a><span data-ttu-id="b565d-112">Kaynak kodu dönüşümleri belirtme</span><span class="sxs-lookup"><span data-stu-id="b565d-112">Specifying source code transformations</span></span>

1. <span data-ttu-id="b565d-113">Paketten projeye eklemek istediğiniz dosya paketin içinde bulunduğu olmalıdır `content` ve `contentFiles` klasörler.</span><span class="sxs-lookup"><span data-stu-id="b565d-113">Files that you want to insert from the package into the project must be located within the package's `content` and `contentFiles` folders.</span></span> <span data-ttu-id="b565d-114">Adlı bir dosya isterseniz, örneğin, `ContosoData.cs` yüklenmesi için bir `Models` klasörü hedef projesinin olmalıdır içinde `content\Models` ve `contentFiles\{lang}\{tfm}\Models` paket klasörlerde.</span><span class="sxs-lookup"><span data-stu-id="b565d-114">For example, if you want a file called `ContosoData.cs` to be installed in a `Models` folder of the target project, it must be inside the `content\Models` and `contentFiles\{lang}\{tfm}\Models` folders in the package.</span></span>

1. <span data-ttu-id="b565d-115">Yükleme sırasında belirteci değiştirme uygulamak için NuGet istemek üzere append `.pp` kaynak kodu dosya adı.</span><span class="sxs-lookup"><span data-stu-id="b565d-115">To instruct NuGet to apply token replacement at install time, append `.pp` to the source code file name.</span></span> <span data-ttu-id="b565d-116">Yükleme tamamlandıktan sonra dosya değil olacaktır `.pp` uzantısı.</span><span class="sxs-lookup"><span data-stu-id="b565d-116">After installation, the file will not have the `.pp` extension.</span></span>

    <span data-ttu-id="b565d-117">Örneğin, dönüşümler yapmak için `ContosoData.cs`, paketteki dosya adı `ContosoData.cs.pp`.</span><span class="sxs-lookup"><span data-stu-id="b565d-117">For example, to make transformations in `ContosoData.cs`, name the file in the package `ContosoData.cs.pp`.</span></span> <span data-ttu-id="b565d-118">Yükleme sonrasında olarak görünür `ContosoData.cs`.</span><span class="sxs-lookup"><span data-stu-id="b565d-118">After installation it will appear as `ContosoData.cs`.</span></span>

1. <span data-ttu-id="b565d-119">Kaynak kodu dosyasının formun büyük küçük harf duyarsız belirteçlerini kullanmak `$token$` değerleri belirtmek için bu NuGet proje özellikleri ile değiştirmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="b565d-119">In the source code file, use case-insensitive tokens of the form `$token$` to indicate values that NuGet should replace with project properties:</span></span>

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

    <span data-ttu-id="b565d-120">Yükleme işleminden sonra NuGet değiştirir `$rootnamespace$` ile `Fabrikam` hedef projeyi varsayılarak kullanıcının, kök ad alanı `Fabrikam`.</span><span class="sxs-lookup"><span data-stu-id="b565d-120">Upon installation, NuGet replaces `$rootnamespace$` with `Fabrikam` assuming the target project's whose root namespace is `Fabrikam`.</span></span>

<span data-ttu-id="b565d-121">`$rootnamespace$` Belirteci en yaygın kullanılan proje özelliği; diğerlerini listelenen [proje özellikleri](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span><span class="sxs-lookup"><span data-stu-id="b565d-121">The `$rootnamespace$` token is the most commonly used project property; all others are listed in [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span></span> <span data-ttu-id="b565d-122">Elbette, bazı özellikler için proje türü belirli olabileceğini oluşturduğunu, unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b565d-122">Be mindful, of course, that some properties might be specific to the project type.</span></span>

## <a name="specifying-config-file-transformations"></a><span data-ttu-id="b565d-123">Yapılandırma dosyası dönüşümleri belirtme</span><span class="sxs-lookup"><span data-stu-id="b565d-123">Specifying config file transformations</span></span>

<span data-ttu-id="b565d-124">İzleyen bölümlerde açıklandığı gibi iki yolla yapılandırma dosyası dönüşümleri yapılabilir:</span><span class="sxs-lookup"><span data-stu-id="b565d-124">As described in the sections that follow, config file transformations can be done in two ways:</span></span>

- <span data-ttu-id="b565d-125">Dahil `app.config.transform` ve `web.config.transform` , paketin dosyalarında `content` klasörü, burada `.transform` uzantısı, bu dosyaları paketi yüklendiğinde var olan yapılandırma dosyaları ile birleştirmek için bir XML içeriyor NuGet söyler.</span><span class="sxs-lookup"><span data-stu-id="b565d-125">Include `app.config.transform` and `web.config.transform` files in your package's `content` folder, where the `.transform` extension tells NuGet that these files contain the XML to merge with existing config files when the package is installed.</span></span> <span data-ttu-id="b565d-126">Bir paketi kaldırıldığında, aynı XML kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="b565d-126">When a package is uninstalled, that same XML is removed.</span></span>
- <span data-ttu-id="b565d-127">Dahil `app.config.install.xdt` ve `web.config.install.xdt` , paketin dosyalarında `content` klasörünü kullanarak [XDT sözdizimi](https://msdn.microsoft.com/library/dd465326.aspx) istediğiniz değişiklikleri açıklamak için.</span><span class="sxs-lookup"><span data-stu-id="b565d-127">Include `app.config.install.xdt` and `web.config.install.xdt` files in your package's `content` folder, using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx) to describe the desired changes.</span></span> <span data-ttu-id="b565d-128">Bu seçenek ile de ekleyebilirsiniz bir `.uninstall.xdt` paket projeden kaldırıldığında değişiklikleri geri almak için dosya.</span><span class="sxs-lookup"><span data-stu-id="b565d-128">With this option you can also include a `.uninstall.xdt` file to reverse changes when the package is removed from a project.</span></span>

> [!Note]
> <span data-ttu-id="b565d-129">Dönüştürmeleri için uygulanmaz `.config` Visual Studio'da bir bağlantı olarak başvurulan dosyaları.</span><span class="sxs-lookup"><span data-stu-id="b565d-129">Transformations are not applied to `.config` files referenced as a link in Visual Studio.</span></span>

<span data-ttu-id="b565d-130">XDT kullanmanın avantajı yalnızca iki statik dosyaları birleştirme yerine, bir sözdizimi öğe ve öznitelik kullanılarak tam XPath desteği eşleşen kullanarak bir XML DOM yapısını işlemek için sağlamasıdır.</span><span class="sxs-lookup"><span data-stu-id="b565d-130">The advantage of using XDT is that instead of simply merging two static files, it provides a syntax for manipulating the structure of an XML DOM using element and attribute matching using full XPath support.</span></span> <span data-ttu-id="b565d-131">XDT sonra ekleme, güncelleştirme veya öğeleri kaldırın, yeni öğeleri belirli bir konuma yerleştirin veya Değiştir / (alt düğümler de dahil olmak üzere) öğeleri kaldır.</span><span class="sxs-lookup"><span data-stu-id="b565d-131">XDT can then add, update, or remove elements, place new elements at a specific location, or replace/remove elements (including child nodes).</span></span> <span data-ttu-id="b565d-132">Bu, paket yükleme sırasında yapılan tüm dönüştürmeleri çıkışı geri kaldırma dönüşümleri oluşturmak basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="b565d-132">This makes it straightforward to create uninstall transforms that back out all transformations done during package installation.</span></span>

### <a name="xml-transforms"></a><span data-ttu-id="b565d-133">XML dönüşümler</span><span class="sxs-lookup"><span data-stu-id="b565d-133">XML transforms</span></span>

<span data-ttu-id="b565d-134">`app.config.transform` Ve `web.config.transform` bir paketin içinde `content` klasörünü içeren projenin varolan halinde birleştirmek için yalnızca bu öğeler `app.config` ve `web.config` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="b565d-134">The `app.config.transform` and `web.config.transform` in a package's `content` folder contain only those elements to merge into the project's existing `app.config` and `web.config` files.</span></span>

<span data-ttu-id="b565d-135">Örnek olarak, projeyi başlangıçta aşağıdaki içeriği içeren varsayalım `web.config`:</span><span class="sxs-lookup"><span data-stu-id="b565d-135">As an example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="b565d-136">Eklemek için bir `MyNuModule` öğesine `modules` bölümünde paket yükleme sırasında oluşturma bir `web.config.transform` paketin dosyasında `content` şöyle klasörü:</span><span class="sxs-lookup"><span data-stu-id="b565d-136">To add a `MyNuModule` element to the `modules` section during package install, create a `web.config.transform` file in the package's `content` folder that looks like this:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="b565d-137">NuGet paket yüklendikten sonra `web.config` şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="b565d-137">After NuGet installs the package, `web.config` will appear as follows:</span></span>

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

<span data-ttu-id="b565d-138">NuGet Değiştir kaydetmedi bildirimi `modules` bölümünde, yalnızca birleştirilen içine yeni giriş yalnızca yeni öğeleri ve özniteliklerinin ekleyerek.</span><span class="sxs-lookup"><span data-stu-id="b565d-138">Notice that NuGet didn't replace the `modules` section, it just merged the new entry into it by adding only new elements and attributes.</span></span> <span data-ttu-id="b565d-139">NuGet herhangi bir varolan öğeleri veya öznitelikleri değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="b565d-139">NuGet will not change any existing elements or attributes.</span></span>

<span data-ttu-id="b565d-140">NuGet paket kaldırıldığında inceleyeceksiniz `.transform` yeniden dosyaları ve içerdiği öğeleri uygun Kaldır `.config` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="b565d-140">When the package is uninstalled, NuGet will examine the `.transform` files again and remove the elements it contains from the appropriate `.config` files.</span></span> <span data-ttu-id="b565d-141">Bu işlem tüm satırları etkilemez Not `.config` paket yüklendikten sonra değiştirmek dosya.</span><span class="sxs-lookup"><span data-stu-id="b565d-141">Note that this process will not affect any lines in the `.config` file that you modify after package installation.</span></span>

<span data-ttu-id="b565d-142">Daha kapsamlı bir örnek olarak [hata günlük modülleri ve işleyicileri için ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) paket içine birçok girdisi ekler `web.config`, hangi yeniden kaldırılır bir paket kaldırıldığında.</span><span class="sxs-lookup"><span data-stu-id="b565d-142">As a more extensive example, the [Error Logging Modules and Handlers for ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) package adds many entries into `web.config`, which are again removed when a package is uninstalled.</span></span>

<span data-ttu-id="b565d-143">İncelemek için kendi `web.config.transform` dosya, yukarıdaki bağlantıyı ELMAH paketini indirin, paket uzantı değiştirme `.nupkg` için `.zip`ve ardından açın `content\web.config.transform` o ZIP dosyasında.</span><span class="sxs-lookup"><span data-stu-id="b565d-143">To examine its `web.config.transform` file, download the ELMAH package from the link above, change the package extension from `.nupkg` to `.zip`, and then open `content\web.config.transform` in that ZIP file.</span></span>

<span data-ttu-id="b565d-144">Yükleme ve paket kaldırma etkisini görmek için Visual Studio'da yeni bir ASP.NET projesi oluşturma (altında şablonudur **Visual C# > Web** yeni proje iletişim kutusunda) ve boş bir ASP.NET uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="b565d-144">To see the effect of installing and uninstalling the package, create a new ASP.NET project in Visual Studio (the template is under **Visual C# > Web** in the New Project dialog), and select an empty ASP.NET application.</span></span> <span data-ttu-id="b565d-145">Açık `web.config` başlangıç durumunu görmek için.</span><span class="sxs-lookup"><span data-stu-id="b565d-145">Open `web.config` to see its initial state.</span></span> <span data-ttu-id="b565d-146">Projeye sağ tıklayın, seçin **NuGet paketlerini Yönet**üzerinde nuget.org ELMAH için gözatın ve en son sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b565d-146">Then right-click the project, select **Manage NuGet Packages**, browse for ELMAH on nuget.org, and install the latest version.</span></span> <span data-ttu-id="b565d-147">Yapılan tüm değişiklikler fark `web.config`.</span><span class="sxs-lookup"><span data-stu-id="b565d-147">Notice all the changes to `web.config`.</span></span> <span data-ttu-id="b565d-148">Şimdi paketi kaldırma ve gördüğünüz `web.config` önceki durumuna geri çevirin.</span><span class="sxs-lookup"><span data-stu-id="b565d-148">Now uninstall the package and you see `web.config` revert to its prior state.</span></span>

### <a name="xdt-transforms"></a><span data-ttu-id="b565d-149">XDT dönüşümler</span><span class="sxs-lookup"><span data-stu-id="b565d-149">XDT transforms</span></span>

<span data-ttu-id="b565d-150">Yapılandırma dosyaları kullanılarak değiştirebileceğiniz [XDT sözdizimi](https://msdn.microsoft.com/library/dd465326.aspx).</span><span class="sxs-lookup"><span data-stu-id="b565d-150">You can modify config files using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx).</span></span> <span data-ttu-id="b565d-151">Ayrıca belirteçleri ile değiştir NuGet olabilir [proje özellikleri](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) içinde özellik adı ekleyerek `$` sınırlayıcı (büyük küçük harf duyarsız).</span><span class="sxs-lookup"><span data-stu-id="b565d-151">You can also have NuGet replace tokens with [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) by including the property name within `$` delimeters (case-insensitive).</span></span>

<span data-ttu-id="b565d-152">Örneğin, aşağıdaki `app.config.install.xdt` dosya ekler bir `appSettings` öğesine `app.config` içeren `FullPath`, `FileName`, ve `ActiveConfigurationSettings` projeden değerler:</span><span class="sxs-lookup"><span data-stu-id="b565d-152">For example, the following `app.config.install.xdt` file will insert an `appSettings` element into `app.config` containing the `FullPath`, `FileName`, and `ActiveConfigurationSettings` values from the project:</span></span>

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

<span data-ttu-id="b565d-153">Başka bir örnek için projeyi başlangıçta aşağıdaki içeriği içeren varsayalım `web.config`:</span><span class="sxs-lookup"><span data-stu-id="b565d-153">For another example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="b565d-154">Eklemek için bir `MyNuModule` öğesine `modules` bölüm paket sırasında yükleme, paketin `web.config.install.xdt` aşağıdakileri içerir:</span><span class="sxs-lookup"><span data-stu-id="b565d-154">To add a `MyNuModule` element to the `modules` section during package install, the package's `web.config.install.xdt` would contain the following:</span></span>

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

<span data-ttu-id="b565d-155">Paket yüklendikten sonra `web.config` şuna benzeyecektir:</span><span class="sxs-lookup"><span data-stu-id="b565d-155">After installing the package, `web.config` will look like this:</span></span>

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

<span data-ttu-id="b565d-156">Yalnızca kaldırmak için `MyNuModule` paketi kaldırma sırasında öğesi `web.config.uninstall.xdt` dosyası şunları içermelidir:</span><span class="sxs-lookup"><span data-stu-id="b565d-156">To remove only the `MyNuModule` element during package uninstall, the `web.config.uninstall.xdt` file should contain the following:</span></span>

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
