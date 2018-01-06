---
title: "Kaynak ve yapılandırma dosyası dönüştürmeleri için NuGet paketleri | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 4/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 20991d69-9e2e-4881-bbf2-96ae634e1872
description: "Kaynak kodu ve yapılandırması dönüştürmesini NuGet paketlerini yeteneğine yüklendiğinde (XML) dosyaları ayrıntılarını verir."
keywords: "NuGet paket yükleme, yapılandırma dosyalarını, kaynak kodun değiştirilmesiyle değiştirme NuGet paketi dönüşümleri"
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: 89a55716ccbc9043cfce4c7f38ec8ab9a0e2f768
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/05/2018
---
# <a name="transforming-source-code-and-configuration-files"></a><span data-ttu-id="bbb85-104">Kaynak kodu ve yapılandırma dosyaları dönüştürme</span><span class="sxs-lookup"><span data-stu-id="bbb85-104">Transforming source code and configuration files</span></span>

<span data-ttu-id="bbb85-105">Kullanarak projeleri için `packages.config` veya `project.json`, NuGet kaynak kodu dönüşümleri yapma yeteneği destekler ve paket yapılandırma dosyaları yükleyip kez kaldırın.</span><span class="sxs-lookup"><span data-stu-id="bbb85-105">For projects using `packages.config` or `project.json`, NuGet supports the ability to make transformations to source code and configuration files at package install and uninstall times.</span></span>

> [!Note]
> <span data-ttu-id="bbb85-106">Bir paketi kullanarak bir projeye yüklendiğinde, kaynak ve yapılandırma dosyası dönüşümleri uygulanan değil [paket referanslarını proje dosyalarına](../Consume-Packages/Package-References-in-Project-Files.md).</span><span class="sxs-lookup"><span data-stu-id="bbb85-106">Source and configuration file transformations are not applied when a package is installed in a project using [Package References in project files](../Consume-Packages/Package-References-in-Project-Files.md).</span></span> 

<span data-ttu-id="bbb85-107">A **kaynak kodu dönüştürme** paketin dosyalarında tek yönlü belirteci değiştirme uygulandığı `content` paketi yüklendiğinde burada belirteçleri Visual Studio'ya başvurmak klasörü [proje özellikleri](/dotnet/api/vslangproj.projectproperties?redirectedfrom=MSDN&view=visualstudiosdk-2017#properties_) .</span><span class="sxs-lookup"><span data-stu-id="bbb85-107">A **source code transformation** applies one-way token replacement to files in the package's `content` folder when the package is installed, where tokens refer to Visual Studio [project properties](/dotnet/api/vslangproj.projectproperties?redirectedfrom=MSDN&view=visualstudiosdk-2017#properties_).</span></span> <span data-ttu-id="bbb85-108">Bu projenin ad alanına bir dosya eklemek için ya da genellikle içine geçecek kod özelleştirmenizi sağlar `global.asax` ASP.NET projesinde.</span><span class="sxs-lookup"><span data-stu-id="bbb85-108">This allows you to insert a file into the project's namespace, or to customize code that would typically go into `global.asax` in an ASP.NET project.</span></span>

<span data-ttu-id="bbb85-109">A **config dosya dönüşümü** , bir hedef projesinde gibi zaten mevcut dosyaların değiştirmenizi sağlar `web.config` ve `app.config`.</span><span class="sxs-lookup"><span data-stu-id="bbb85-109">A **config file transformation** allows you to modify files that already exist in a target project, such as `web.config` and `app.config`.</span></span> <span data-ttu-id="bbb85-110">Örneğin, bir öğe eklemek paketinizi gereken `modules` yapılandırma dosyası bölümünde.</span><span class="sxs-lookup"><span data-stu-id="bbb85-110">For example, your package might need to add an item to the `modules` section in the config file.</span></span> <span data-ttu-id="bbb85-111">Bu dönüştürme için yapılandırma dosyalarını eklemek için bölümlerde paketinde özel dosyaları ekleyerek yapılır.</span><span class="sxs-lookup"><span data-stu-id="bbb85-111">This transformation is done by including special files in the package that describe the sections to add to the configuration files.</span></span> <span data-ttu-id="bbb85-112">Bir paketi kaldırıldığında, aynı değişiklikleri daha sonra bu iki yönlü bir dönüştürme yapma ters çevrilir.</span><span class="sxs-lookup"><span data-stu-id="bbb85-112">When a package is uninstalled, those same changes are then reversed, making this a two-way transformation.</span></span>

## <a name="specifying-source-code-transformations"></a><span data-ttu-id="bbb85-113">Kaynak kodu dönüşümleri belirtme</span><span class="sxs-lookup"><span data-stu-id="bbb85-113">Specifying source code transformations</span></span>

1. <span data-ttu-id="bbb85-114">Paketten projeye eklemek istediğiniz dosya paketin içinde bulunduğu olmalıdır `content` klasör.</span><span class="sxs-lookup"><span data-stu-id="bbb85-114">Files that you want to insert from the package into the project must be located within the package's `content` folder.</span></span> <span data-ttu-id="bbb85-115">Adlı bir dosya isterseniz, örneğin, `ContosoData.cs` yüklenmesi için bir `Models` klasörü hedef projesinin olmalıdır içinde `content\Models` paket klasöründe.</span><span class="sxs-lookup"><span data-stu-id="bbb85-115">For example, if you want a file called `ContosoData.cs` to be installed in a `Models` folder of the target project, it must be inside the `content\Models` folder in the package.</span></span>

1. <span data-ttu-id="bbb85-116">Yükleme sırasında belirteci değiştirme uygulamak için NuGet istemek üzere append `.pp` kaynak kodu dosya adı.</span><span class="sxs-lookup"><span data-stu-id="bbb85-116">To instruct NuGet to apply token replacement at install time, append `.pp` to the source code file name.</span></span> <span data-ttu-id="bbb85-117">Yükleme tamamlandıktan sonra dosya değil olacaktır `.pp` uzantısı.</span><span class="sxs-lookup"><span data-stu-id="bbb85-117">After installation, the file will not have the `.pp` extension.</span></span>

    <span data-ttu-id="bbb85-118">Örneğin, dönüşümler yapmak için `ContosoData.cs`, paketteki dosya adı `ContosoData.cs.pp`.</span><span class="sxs-lookup"><span data-stu-id="bbb85-118">For example, to make transformations in `ContosoData.cs`, name the file in the package `ContosoData.cs.pp`.</span></span> <span data-ttu-id="bbb85-119">Yükleme sonrasında olarak görünür `ContosoData.cs`.</span><span class="sxs-lookup"><span data-stu-id="bbb85-119">After installation it will appear as `ContosoData.cs`.</span></span>

1. <span data-ttu-id="bbb85-120">Kaynak kodu dosyasının formun büyük küçük harf duyarsız belirteçlerini kullanmak `$token$` değerleri belirtmek için bu NuGet proje özellikleri ile değiştirmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="bbb85-120">In the source code file, use case-insensitive tokens of the form `$token$` to indicate values that NuGet should replace with project properties:</span></span>

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

    <span data-ttu-id="bbb85-121">Yükleme işleminden sonra NuGet değiştirir `$rootnamespace$` ile `Fabrikam` hedef projeyi varsayılarak kullanıcının, kök ad alanı `Fabrikam`.</span><span class="sxs-lookup"><span data-stu-id="bbb85-121">Upon installation, NuGet replaces `$rootnamespace$` with `Fabrikam` assuming the target project's whose root namespace is `Fabrikam`.</span></span>

<span data-ttu-id="bbb85-122">`$rootnamespace$` Belirteci en yaygın kullanılan proje özelliği; diğerlerini listelenen [proje özelliklerini](/dotnet/api/vslangproj.projectproperties?redirectedfrom=MSDN&view=visualstudiosdk-2017#properties_) MSDN'de belgelerin.</span><span class="sxs-lookup"><span data-stu-id="bbb85-122">The `$rootnamespace$` token is the most commonly used project property; all others are listed in the [Project Properties](/dotnet/api/vslangproj.projectproperties?redirectedfrom=MSDN&view=visualstudiosdk-2017#properties_) documentation on MSDN.</span></span> <span data-ttu-id="bbb85-123">Elbette, bazı özellikler için proje türü belirli olabileceğini oluşturduğunu, unutmayın.</span><span class="sxs-lookup"><span data-stu-id="bbb85-123">Be mindful, of course, that some properties might be specific to the project type.</span></span>

## <a name="specifying-config-file-transformations"></a><span data-ttu-id="bbb85-124">Yapılandırma dosyası dönüşümleri belirtme</span><span class="sxs-lookup"><span data-stu-id="bbb85-124">Specifying config file transformations</span></span>

<span data-ttu-id="bbb85-125">İzleyen bölümlerde açıklandığı gibi iki yolla yapılandırma dosyası dönüşümleri yapılabilir:</span><span class="sxs-lookup"><span data-stu-id="bbb85-125">As described in the sections that follow, config file transformations can be done in two ways:</span></span>

- <span data-ttu-id="bbb85-126">Dahil `app.config.transform` ve `web.config.transform` , paketin dosyalarında `content` klasörü, burada `.transform` uzantısı, bu dosyaları paketi yüklendiğinde var olan yapılandırma dosyaları ile birleştirmek için bir XML içeriyor NuGet söyler.</span><span class="sxs-lookup"><span data-stu-id="bbb85-126">Include `app.config.transform` and `web.config.transform` files in your package's `content` folder, where the `.transform` extension tells NuGet that these files contain the XML to merge with existing config files when the package is installed.</span></span> <span data-ttu-id="bbb85-127">Bir paketi kaldırıldığında, aynı XML kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="bbb85-127">When a package is uninstalled, that same XML is removed.</span></span>
- <span data-ttu-id="bbb85-128">(NuGet 2.6 ve sonrası) Dahil `app.config.install.xdt` ve `web.config.install.xdt` , paketin dosyalarında `content` klasörünü kullanarak [XDT sözdizimi](https://msdn.microsoft.com/library/dd465326.aspx) istediğiniz değişiklikleri açıklamak için.</span><span class="sxs-lookup"><span data-stu-id="bbb85-128">(NuGet 2.6 and later) Include `app.config.install.xdt` and `web.config.install.xdt` files in your package's `content` folder, using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx) to describe the desired changes.</span></span> <span data-ttu-id="bbb85-129">Bu seçenek ile de ekleyebilirsiniz bir `.uninstall.xdt` paket projeden kaldırıldığında değişiklikleri geri almak için dosya.</span><span class="sxs-lookup"><span data-stu-id="bbb85-129">With this option you can also include a `.uninstall.xdt` file to reverse changes when the package is removed from a project.</span></span>

> [!Note]
> <span data-ttu-id="bbb85-130">Dönüştürmeleri için uygulanmaz `.config` Visual Studio'da bir bağlantı olarak başvurulan dosyaları.</span><span class="sxs-lookup"><span data-stu-id="bbb85-130">Transformations are not applied to `.config` files referenced as a link in Visual Studio.</span></span>

<span data-ttu-id="bbb85-131">XDT kullanmanın avantajı yalnızca iki statik dosyaları birleştirme yerine, bir sözdizimi öğe ve öznitelik kullanılarak tam XPath desteği eşleşen kullanarak bir XML DOM yapısını işlemek için sağlamasıdır.</span><span class="sxs-lookup"><span data-stu-id="bbb85-131">The advantage of using XDT is that instead of simply merging two static files, it provides a syntax for manipulating the structure of an XML DOM using element and attribute matching using full XPath support.</span></span> <span data-ttu-id="bbb85-132">XDT sonra ekleme, güncelleştirme veya öğeleri kaldırın, yeni öğeleri belirli bir konuma yerleştirin veya Değiştir / (alt düğümler de dahil olmak üzere) öğeleri kaldır.</span><span class="sxs-lookup"><span data-stu-id="bbb85-132">XDT can then add, update, or remove elements, place new elements at a specific location, or replace/remove elements (including child nodes).</span></span> <span data-ttu-id="bbb85-133">Bu, paket yükleme sırasında yapılan tüm dönüştürmeleri çıkışı geri kaldırma dönüşümleri oluşturmak basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="bbb85-133">This makes it straightforward to create uninstall transforms that back out all transformations done during package installation.</span></span>

### <a name="xml-transforms"></a><span data-ttu-id="bbb85-134">XML dönüşümler</span><span class="sxs-lookup"><span data-stu-id="bbb85-134">XML transforms</span></span>

<span data-ttu-id="bbb85-135">`app.config.transform` Ve `web.config.transform` bir paketin içinde `content` klasörünü içeren projenin varolan halinde birleştirmek için yalnızca bu öğeler `app.config` ve `web.config` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="bbb85-135">The `app.config.transform` and `web.config.transform` in a package's `content` folder contain only those elements to merge into the project's existing `app.config` and `web.config` files.</span></span>

<span data-ttu-id="bbb85-136">Örnek olarak, projeyi başlangıçta aşağıdaki içeriği içeren varsayalım `web.config`:</span><span class="sxs-lookup"><span data-stu-id="bbb85-136">As an example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    <system.webServer>
</configuration>
```

<span data-ttu-id="bbb85-137">Eklemek için bir `MyNuModule` öğesine `modules` bölümünde paket yükleme sırasında oluşturma bir `web.config.transform` paketin dosyasında `content` şöyle klasörü:</span><span class="sxs-lookup"><span data-stu-id="bbb85-137">To add a `MyNuModule` element to the `modules` section during package install, create a `web.config.transform` file in the package's `content` folder that looks like this:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    <system.webServer>
</configuration>
```

<span data-ttu-id="bbb85-138">NuGet paket yüklendikten sonra `web.config` şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="bbb85-138">After NuGet installs the package, `web.config` will appear as follows:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    <system.webServer>
</configuration>
```

<span data-ttu-id="bbb85-139">NuGet Değiştir kaydetmedi bildirimi `modules` bölümünde, yalnızca birleştirilen içine yeni giriş yalnızca yeni öğeleri ve özniteliklerinin ekleyerek.</span><span class="sxs-lookup"><span data-stu-id="bbb85-139">Notice that NuGet didn't replace the `modules` section, it just merged the new entry into it by adding only new elements and attributes.</span></span> <span data-ttu-id="bbb85-140">NuGet herhangi bir varolan öğeleri veya öznitelikleri değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="bbb85-140">NuGet will not change any existing elements or attributes.</span></span>

<span data-ttu-id="bbb85-141">NuGet paket kaldırıldığında inceleyeceksiniz `.transform` yeniden dosyaları ve içerdiği öğeleri uygun Kaldır `.config` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="bbb85-141">When the package is uninstalled, NuGet will examine the `.transform` files again and remove the elements it contains from the appropriate `.config` files.</span></span> <span data-ttu-id="bbb85-142">Bu işlem tüm satırları etkilemez Not `.config` paket yüklendikten sonra değiştirmek dosya.</span><span class="sxs-lookup"><span data-stu-id="bbb85-142">Note that this process will not affect any lines in the `.config` file that you modify after package installation.</span></span>

<span data-ttu-id="bbb85-143">Daha kapsamlı bir örnek olarak [hata günlük modülleri ve işleyicileri için ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) paket içine birçok girdisi ekler `web.config`, hangi yeniden kaldırılır bir paket kaldırıldığında.</span><span class="sxs-lookup"><span data-stu-id="bbb85-143">As a more extensive example, the [Error Logging Modules and Handlers for ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) package adds many entries into `web.config`, which are again removed when a package is uninstalled.</span></span>

<span data-ttu-id="bbb85-144">İncelemek için kendi `web.config.transform` dosya, yukarıdaki bağlantıyı ELMAH paketini indirin, paket uzantı değiştirme `.nupkg` için `.zip`ve ardından açın `content\web.config.transform` o ZIP dosyasında.</span><span class="sxs-lookup"><span data-stu-id="bbb85-144">To examine its `web.config.transform` file, download the ELMAH package from the link above, change the package extension from `.nupkg` to `.zip`, and then open `content\web.config.transform` in that ZIP file.</span></span>

<span data-ttu-id="bbb85-145">Yükleme ve paket kaldırma etkisini görmek için Visual Studio'da yeni bir ASP.NET projesi oluşturma (altında şablonudur **Visual C# > Web** yeni proje iletişim kutusunda) ve boş bir ASP.NET uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="bbb85-145">To see the effect of installing and uninstalling the package, create a new ASP.NET project in Visual Studio (the template is under **Visual C# > Web** in the New Project dialog), and select an empty ASP.NET application.</span></span> <span data-ttu-id="bbb85-146">Açık `web.config` başlangıç durumunu görmek için.</span><span class="sxs-lookup"><span data-stu-id="bbb85-146">Open `web.config` to see its initial state.</span></span> <span data-ttu-id="bbb85-147">Projeye sağ tıklayın, seçin **NuGet paketlerini Yönet**üzerinde nuget.org ELMAH için gözatın ve en son sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="bbb85-147">Then right-click the project, select **Manage NuGet Packages**, browse for ELMAH on nuget.org, and install the latest version.</span></span> <span data-ttu-id="bbb85-148">Yapılan tüm değişiklikler fark `web.config`.</span><span class="sxs-lookup"><span data-stu-id="bbb85-148">Notice all the changes to `web.config`.</span></span> <span data-ttu-id="bbb85-149">Şimdi paketi kaldırma ve göreceğiniz `web.config` önceki durumuna geri çevirin.</span><span class="sxs-lookup"><span data-stu-id="bbb85-149">Now uninstall the package and you'll see `web.config` revert to its prior state.</span></span>

### <a name="xdt-transforms"></a><span data-ttu-id="bbb85-150">XDT dönüşümler</span><span class="sxs-lookup"><span data-stu-id="bbb85-150">XDT transforms</span></span>

<span data-ttu-id="bbb85-151">NuGet 2.6 ve daha sonra yapılandırma dosyalarını kullanarak değiştirebilirsiniz [XDT sözdizimi](https://msdn.microsoft.com/library/dd465326.aspx).</span><span class="sxs-lookup"><span data-stu-id="bbb85-151">With NuGet 2.6 and later, you can modify config files using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx).</span></span> <span data-ttu-id="bbb85-152">Ayrıca belirteçleri ile değiştir NuGet olabilir [proje özellikleri](/dotnet/api/vslangproj.projectproperties?redirectedfrom=MSDN&view=visualstudiosdk-2017#properties_) içinde özellik adı ekleyerek `$` sınırlayıcı (büyük küçük harf duyarsız).</span><span class="sxs-lookup"><span data-stu-id="bbb85-152">You can also have NuGet replace tokens with [Project Properties](/dotnet/api/vslangproj.projectproperties?redirectedfrom=MSDN&view=visualstudiosdk-2017#properties_) by including the property name within `$` delimeters (case-insensitive).</span></span>

<span data-ttu-id="bbb85-153">Örneğin, aşağıdaki `app.config.install.xdt` dosya ekler bir `appSettings` öğesine `app.config` içeren `FullPath`, `FileName`, ve `ActiveConfigurationSettings` projeden değerler:</span><span class="sxs-lookup"><span data-stu-id="bbb85-153">For example, the following `app.config.install.xdt` file will insert an `appSettings` element into `app.config` containing the `FullPath`, `FileName`, and `ActiveConfigurationSettings` values from the project:</span></span>

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

<span data-ttu-id="bbb85-154">Başka bir örnek için projeyi başlangıçta aşağıdaki içeriği içeren varsayalım `web.config`:</span><span class="sxs-lookup"><span data-stu-id="bbb85-154">For another example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    <system.webServer>
</configuration>
```

<span data-ttu-id="bbb85-155">Eklemek için bir `MyNuModule` öğesine `modules` bölüm paket sırasında yükleme, paketin `web.config.install.xdt` aşağıdakileri içerir:</span><span class="sxs-lookup"><span data-stu-id="bbb85-155">To add a `MyNuModule` element to the `modules` section during package install, the package's `web.config.install.xdt` would contain the following:</span></span>

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

<span data-ttu-id="bbb85-156">Paket yüklendikten sonra `web.config` şuna benzeyecektir:</span><span class="sxs-lookup"><span data-stu-id="bbb85-156">After installing the package, `web.config` will look like this:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    <system.webServer>
</configuration>
```

<span data-ttu-id="bbb85-157">Yalnızca kaldırmak için `MyNuModule` paketi kaldırma sırasında öğesi `web.config.uninstall.xdt` dosyası şunları içermelidir:</span><span class="sxs-lookup"><span data-stu-id="bbb85-157">To remove only the `MyNuModule` element during package uninstall, the `web.config.uninstall.xdt` file should contain the following:</span></span>

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
