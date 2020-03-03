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
# <a name="transforming-source-code-and-configuration-files"></a><span data-ttu-id="f8ca6-103">Kaynak kodu ve yapılandırma dosyalarını dönüştürme</span><span class="sxs-lookup"><span data-stu-id="f8ca6-103">Transforming source code and configuration files</span></span>

<span data-ttu-id="f8ca6-104">**Kaynak kodu dönüştürmesi** , paketin yüklendiği zaman, belirtecin Visual Studio [Proje özelliklerine](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7)başvurduğu, paketin `content` veya `contentFiles` `contentFiles` `packages.config``content` klasöründeki dosyalara tek yönlü belirteç değişikliği uygular.`PackageReference`</span><span class="sxs-lookup"><span data-stu-id="f8ca6-104">A **source code transformation** applies one-way token replacement to files in the package's `content` or `contentFiles` folder (`content` for customers using `packages.config` and `contentFiles` for `PackageReference`) when the package is installed, where tokens refer to Visual Studio [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span></span> <span data-ttu-id="f8ca6-105">Bu, projenin ad alanına bir dosya eklemenize veya tipik olarak bir ASP.NET projesinde `global.asax` gidecek kodu özelleştirmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="f8ca6-105">This allows you to insert a file into the project's namespace, or to customize code that would typically go into `global.asax` in an ASP.NET project.</span></span>

<span data-ttu-id="f8ca6-106">Bir **yapılandırma dosyası dönüştürmesi** , `web.config` ve `app.config`gibi bir hedef projede zaten mevcut olan dosyaları değiştirmenize izin verir.</span><span class="sxs-lookup"><span data-stu-id="f8ca6-106">A **config file transformation** allows you to modify files that already exist in a target project, such as `web.config` and `app.config`.</span></span> <span data-ttu-id="f8ca6-107">Örneğin, paketinizin yapılandırma dosyasındaki `modules` bölümüne bir öğe eklemesi gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="f8ca6-107">For example, your package might need to add an item to the `modules` section in the config file.</span></span> <span data-ttu-id="f8ca6-108">Bu dönüşüm, yapılandırma dosyalarına eklenecek bölümleri tanımlayan paketteki özel dosyalar eklenerek yapılır.</span><span class="sxs-lookup"><span data-stu-id="f8ca6-108">This transformation is done by including special files in the package that describe the sections to add to the configuration files.</span></span> <span data-ttu-id="f8ca6-109">Bir paket kaldırıldığında, bu değişiklikler iki yönlü bir dönüşüm yaparak ters çevrilir.</span><span class="sxs-lookup"><span data-stu-id="f8ca6-109">When a package is uninstalled, those same changes are then reversed, making this a two-way transformation.</span></span>

## <a name="specifying-source-code-transformations"></a><span data-ttu-id="f8ca6-110">Kaynak kodu dönüşümlerini belirtme</span><span class="sxs-lookup"><span data-stu-id="f8ca6-110">Specifying source code transformations</span></span>

1. <span data-ttu-id="f8ca6-111">Paketten projeye eklemek istediğiniz dosyalar paketin `content` ve `contentFiles` klasörlerinde yer almalıdır.</span><span class="sxs-lookup"><span data-stu-id="f8ca6-111">Files that you want to insert from the package into the project must be located within the package's `content` and `contentFiles` folders.</span></span> <span data-ttu-id="f8ca6-112">Örneğin, `ContosoData.cs` adlı bir dosyanın hedef projenin bir `Models` klasörüne yüklenmesini istiyorsanız, paketin içindeki `content\Models` ve `contentFiles\{lang}\{tfm}\Models` klasörlerin içinde olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8ca6-112">For example, if you want a file called `ContosoData.cs` to be installed in a `Models` folder of the target project, it must be inside the `content\Models` and `contentFiles\{lang}\{tfm}\Models` folders in the package.</span></span>

1. <span data-ttu-id="f8ca6-113">NuGet 'in, yüklemenin zamanında belirteç değişimini uygulamasını istemek için `.pp` kaynak kodu dosya adına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f8ca6-113">To instruct NuGet to apply token replacement at install time, append `.pp` to the source code file name.</span></span> <span data-ttu-id="f8ca6-114">Yüklemeden sonra dosya `.pp` uzantısına sahip olmaz.</span><span class="sxs-lookup"><span data-stu-id="f8ca6-114">After installation, the file will not have the `.pp` extension.</span></span>

    <span data-ttu-id="f8ca6-115">Örneğin, `ContosoData.cs`dönüşümler yapmak için dosyayı paket `ContosoData.cs.pp`olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="f8ca6-115">For example, to make transformations in `ContosoData.cs`, name the file in the package `ContosoData.cs.pp`.</span></span> <span data-ttu-id="f8ca6-116">Yüklemeden sonra, `ContosoData.cs`olarak görünür.</span><span class="sxs-lookup"><span data-stu-id="f8ca6-116">After installation it will appear as `ContosoData.cs`.</span></span>

1. <span data-ttu-id="f8ca6-117">Kaynak kodu dosyasında, NuGet 'in proje özellikleriyle yerine geçecek değerleri belirtmek için `$token$` form büyük/küçük harfe duyarsız belirteçlerini kullanın:</span><span class="sxs-lookup"><span data-stu-id="f8ca6-117">In the source code file, use case-insensitive tokens of the form `$token$` to indicate values that NuGet should replace with project properties:</span></span>

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

    <span data-ttu-id="f8ca6-118">Yükleme sonrasında, NuGet, hedef projenin kök ad alanı `Fabrikam`olan `$rootnamespace$` `Fabrikam` ile değiştirir.</span><span class="sxs-lookup"><span data-stu-id="f8ca6-118">Upon installation, NuGet replaces `$rootnamespace$` with `Fabrikam` assuming the target project's whose root namespace is `Fabrikam`.</span></span>

<span data-ttu-id="f8ca6-119">`$rootnamespace$` belirteci en yaygın olarak kullanılan proje özelliğidir; Tüm diğerleri [proje özelliklerinde](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7)listelenir.</span><span class="sxs-lookup"><span data-stu-id="f8ca6-119">The `$rootnamespace$` token is the most commonly used project property; all others are listed in [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span></span> <span data-ttu-id="f8ca6-120">Kuşkusuz, bazı özelliklerin proje türüne özgü olabileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f8ca6-120">Be mindful, of course, that some properties might be specific to the project type.</span></span>

## <a name="specifying-config-file-transformations"></a><span data-ttu-id="f8ca6-121">Yapılandırma dosyası dönüşümlerini belirtme</span><span class="sxs-lookup"><span data-stu-id="f8ca6-121">Specifying config file transformations</span></span>

<span data-ttu-id="f8ca6-122">Aşağıdaki bölümlerde açıklandığı gibi, yapılandırma dosyası dönüştürmeleri iki şekilde yapılabilir:</span><span class="sxs-lookup"><span data-stu-id="f8ca6-122">As described in the sections that follow, config file transformations can be done in two ways:</span></span>

- <span data-ttu-id="f8ca6-123">`app.config.transform` ve `web.config.transform` dosyalarını, paketinizin `content` klasöre ekleyin. burada `.transform` uzantısı, bu dosyaların, paket yüklendiğinde var olan yapılandırma dosyalarıyla birleştirmek için XML içerdiğini NuGet 'e söyler.</span><span class="sxs-lookup"><span data-stu-id="f8ca6-123">Include `app.config.transform` and `web.config.transform` files in your package's `content` folder, where the `.transform` extension tells NuGet that these files contain the XML to merge with existing config files when the package is installed.</span></span> <span data-ttu-id="f8ca6-124">Bir paket kaldırıldığında aynı XML kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="f8ca6-124">When a package is uninstalled, that same XML is removed.</span></span>
- <span data-ttu-id="f8ca6-125">İstenen değişiklikleri anlatmak için [xdt söz dizimini](https://msdn.microsoft.com/library/dd465326.aspx) kullanarak paketinizin `content` klasöre `app.config.install.xdt` ve `web.config.install.xdt` dosyaları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f8ca6-125">Include `app.config.install.xdt` and `web.config.install.xdt` files in your package's `content` folder, using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx) to describe the desired changes.</span></span> <span data-ttu-id="f8ca6-126">Bu seçenekle, paket bir projeden kaldırıldığında ters değişiklikler için bir `.uninstall.xdt` dosyası da ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8ca6-126">With this option you can also include a `.uninstall.xdt` file to reverse changes when the package is removed from a project.</span></span>

> [!Note]
> <span data-ttu-id="f8ca6-127">Dönüşümler, Visual Studio 'da bağlantı olarak başvurulan `.config` dosyalarına uygulanmaz.</span><span class="sxs-lookup"><span data-stu-id="f8ca6-127">Transformations are not applied to `.config` files referenced as a link in Visual Studio.</span></span>

<span data-ttu-id="f8ca6-128">XDT kullanmanın avantajı, yalnızca iki statik dosyayı birleştirmek yerine, bir XML DOM yapısını, tam XPath desteği kullanılarak öğe ve öznitelik eşleştirme kullanarak işlemek için bir sözdizimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="f8ca6-128">The advantage of using XDT is that instead of simply merging two static files, it provides a syntax for manipulating the structure of an XML DOM using element and attribute matching using full XPath support.</span></span> <span data-ttu-id="f8ca6-129">XDT daha sonra öğeleri ekleyebilir, güncelleştirebilir veya kaldırabilir, belirli bir konuma yeni öğeleri yerleştirebilir veya öğeleri (alt düğümler dahil) değiştirebilir/kaldırabilir.</span><span class="sxs-lookup"><span data-stu-id="f8ca6-129">XDT can then add, update, or remove elements, place new elements at a specific location, or replace/remove elements (including child nodes).</span></span> <span data-ttu-id="f8ca6-130">Bu, paket yüklemesi sırasında yapılan tüm dönüştürmeleri geri yükleyen kaldırma dönüştürmeleri oluşturmayı basit hale getirir.</span><span class="sxs-lookup"><span data-stu-id="f8ca6-130">This makes it straightforward to create uninstall transforms that back out all transformations done during package installation.</span></span>

### <a name="xml-transforms"></a><span data-ttu-id="f8ca6-131">XML dönüşümleri</span><span class="sxs-lookup"><span data-stu-id="f8ca6-131">XML transforms</span></span>

<span data-ttu-id="f8ca6-132">Bir paketin `content` klasöründeki `app.config.transform` ve `web.config.transform` yalnızca projenin mevcut `app.config` ve `web.config` dosyalarını birleştirmek için bu öğeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="f8ca6-132">The `app.config.transform` and `web.config.transform` in a package's `content` folder contain only those elements to merge into the project's existing `app.config` and `web.config` files.</span></span>

<span data-ttu-id="f8ca6-133">Örnek olarak, projenin başlangıçta `web.config`aşağıdaki içeriği içerdiğini varsayın:</span><span class="sxs-lookup"><span data-stu-id="f8ca6-133">As an example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="f8ca6-134">Paket yüklemesi sırasında `modules` bölümüne `MyNuModule` öğesi eklemek için, paketin `content` klasöründe şuna benzer bir `web.config.transform` dosyası oluşturun:</span><span class="sxs-lookup"><span data-stu-id="f8ca6-134">To add a `MyNuModule` element to the `modules` section during package install, create a `web.config.transform` file in the package's `content` folder that looks like this:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="f8ca6-135">NuGet paketi yükledikten sonra `web.config` aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="f8ca6-135">After NuGet installs the package, `web.config` will appear as follows:</span></span>

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

<span data-ttu-id="f8ca6-136">NuGet `modules` bölümünün değiştirmediğine dikkat edin. yalnızca yeni öğeler ve öznitelikler ekleyerek yalnızca yeni girişi birleştirir.</span><span class="sxs-lookup"><span data-stu-id="f8ca6-136">Notice that NuGet didn't replace the `modules` section, it just merged the new entry into it by adding only new elements and attributes.</span></span> <span data-ttu-id="f8ca6-137">NuGet, varolan herhangi bir öğeyi veya özniteliği değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="f8ca6-137">NuGet will not change any existing elements or attributes.</span></span>

<span data-ttu-id="f8ca6-138">Paket kaldırıldığında, NuGet `.transform` dosyalarını yeniden inceler ve içerdiği öğeleri uygun `.config` dosyalarından kaldırır.</span><span class="sxs-lookup"><span data-stu-id="f8ca6-138">When the package is uninstalled, NuGet will examine the `.transform` files again and remove the elements it contains from the appropriate `.config` files.</span></span> <span data-ttu-id="f8ca6-139">Bu işlemin, paket yüklemesinden sonra değiştirdiğiniz `.config` dosyasındaki herhangi bir satırı etkilemeyeceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f8ca6-139">Note that this process will not affect any lines in the `.config` file that you modify after package installation.</span></span>

<span data-ttu-id="f8ca6-140">Daha kapsamlı bir örnek olarak, [ASP.net (ELMAH) Için hata günlüğü modülleri ve işleyiciler](https://www.nuget.org/packages/elmah/) , bir paket kaldırıldığında yeniden kaldırılan `web.config`çok sayıda girdi ekler.</span><span class="sxs-lookup"><span data-stu-id="f8ca6-140">As a more extensive example, the [Error Logging Modules and Handlers for ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) package adds many entries into `web.config`, which are again removed when a package is uninstalled.</span></span>

<span data-ttu-id="f8ca6-141">`web.config.transform` dosyasını incelemek için Yukarıdaki bağlantıdan ELMAH paketini indirin, `.nupkg` paket uzantısını `.zip`olarak değiştirin ve ardından söz konusu ZIP dosyasında `content\web.config.transform` açın.</span><span class="sxs-lookup"><span data-stu-id="f8ca6-141">To examine its `web.config.transform` file, download the ELMAH package from the link above, change the package extension from `.nupkg` to `.zip`, and then open `content\web.config.transform` in that ZIP file.</span></span>

<span data-ttu-id="f8ca6-142">Paketi yükleme ve kaldırma etkisini görmek için, Visual Studio 'da yeni bir ASP.NET projesi oluşturun (şablon, yeni proje iletişim kutusunda  **C# Visual > Web** altında bulunur) ve boş bir ASP.NET uygulaması seçin.</span><span class="sxs-lookup"><span data-stu-id="f8ca6-142">To see the effect of installing and uninstalling the package, create a new ASP.NET project in Visual Studio (the template is under **Visual C# > Web** in the New Project dialog), and select an empty ASP.NET application.</span></span> <span data-ttu-id="f8ca6-143">İlk durumunu görmek için `web.config` açın.</span><span class="sxs-lookup"><span data-stu-id="f8ca6-143">Open `web.config` to see its initial state.</span></span> <span data-ttu-id="f8ca6-144">Ardından projeye sağ tıklayın, **NuGet Paketlerini Yönet**' i seçin, NuGet.org üzerinde ELMAH için gezinme yapın ve en son sürümü yükler.</span><span class="sxs-lookup"><span data-stu-id="f8ca6-144">Then right-click the project, select **Manage NuGet Packages**, browse for ELMAH on nuget.org, and install the latest version.</span></span> <span data-ttu-id="f8ca6-145">`web.config`yapılan tüm değişiklikleri fark edin.</span><span class="sxs-lookup"><span data-stu-id="f8ca6-145">Notice all the changes to `web.config`.</span></span> <span data-ttu-id="f8ca6-146">Şimdi paketi kaldırın ve önceki durumuna geri dönmek `web.config` görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="f8ca6-146">Now uninstall the package and you see `web.config` revert to its prior state.</span></span>

### <a name="xdt-transforms"></a><span data-ttu-id="f8ca6-147">XDT dönüşümleri</span><span class="sxs-lookup"><span data-stu-id="f8ca6-147">XDT transforms</span></span>

> [!Note]
> <span data-ttu-id="f8ca6-148">[`packages.config` 'den `PackageReference`geçirmek için docs 'ın paket uyumluluk sorunları bölümünde ](../consume-packages/migrate-packages-config-to-package-reference.md#package-compatibility-issues)belirtildiği gibi, aşağıda açıklanan xdt dönüştürmeleri yalnızca `packages.config`tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="f8ca6-148">As mentioned in the [package compatibility issues section of the docs for migrating from `packages.config` to `PackageReference`](../consume-packages/migrate-packages-config-to-package-reference.md#package-compatibility-issues), XDT transformations as described below are only supported by `packages.config`.</span></span> <span data-ttu-id="f8ca6-149">Aşağıdaki dosyaları paketinize eklerseniz, paketinizin `PackageReference` ile kullandığı tüketiciler Dönüştürmelere uygulanmaz (XDT dönüştürmelerinin`PackageReference`ile çalışması için [Bu örneğe](https://github.com/NuGet/Samples/tree/master/XDTransformExample) başvurun).</span><span class="sxs-lookup"><span data-stu-id="f8ca6-149">If you add the below files to your package, consumers using your package with `PackageReference` will not have the transformations applied (refer to [this sample](https://github.com/NuGet/Samples/tree/master/XDTransformExample) to make XDT transforms work with`PackageReference`).</span></span>

<span data-ttu-id="f8ca6-150">[Xdt sözdizimini](https://msdn.microsoft.com/library/dd465326.aspx)kullanarak yapılandırma dosyalarını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8ca6-150">You can modify config files using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx).</span></span> <span data-ttu-id="f8ca6-151">Ayrıca, `$` sınırlayıcıları (büyük/küçük harfe duyarsız) içinde özellik adı ekleyerek NuGet 'in belirteçleri [Proje özellikleriyle](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) değiştirmesini sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8ca6-151">You can also have NuGet replace tokens with [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) by including the property name within `$` delimiters (case-insensitive).</span></span>

<span data-ttu-id="f8ca6-152">Örneğin, aşağıdaki `app.config.install.xdt` dosyası, projeden `FullPath`, `FileName`ve `ActiveConfigurationSettings` değerlerini içeren `app.config` bir `appSettings` öğesi ekleyecektir:</span><span class="sxs-lookup"><span data-stu-id="f8ca6-152">For example, the following `app.config.install.xdt` file will insert an `appSettings` element into `app.config` containing the `FullPath`, `FileName`, and `ActiveConfigurationSettings` values from the project:</span></span>

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

<span data-ttu-id="f8ca6-153">Başka bir örnek için, projenin başlangıçta `web.config`aşağıdaki içeriği içerdiğini varsayalım:</span><span class="sxs-lookup"><span data-stu-id="f8ca6-153">For another example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="f8ca6-154">Paket yüklemesi sırasında `modules` bölümüne `MyNuModule` öğesi eklemek için, paketin `web.config.install.xdt` şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="f8ca6-154">To add a `MyNuModule` element to the `modules` section during package install, the package's `web.config.install.xdt` would contain the following:</span></span>

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

<span data-ttu-id="f8ca6-155">Paketi yükledikten sonra `web.config` şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="f8ca6-155">After installing the package, `web.config` will look like this:</span></span>

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

<span data-ttu-id="f8ca6-156">Paketi kaldırma sırasında yalnızca `MyNuModule` öğesini kaldırmak için `web.config.uninstall.xdt` dosya şunları içermelidir:</span><span class="sxs-lookup"><span data-stu-id="f8ca6-156">To remove only the `MyNuModule` element during package uninstall, the `web.config.uninstall.xdt` file should contain the following:</span></span>

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
