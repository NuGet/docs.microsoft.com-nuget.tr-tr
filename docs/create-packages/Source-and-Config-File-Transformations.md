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
# <a name="transforming-source-code-and-configuration-files"></a><span data-ttu-id="441a9-103">Kaynak kodu ve yapılandırma dosyalarını dönüştürme</span><span class="sxs-lookup"><span data-stu-id="441a9-103">Transforming source code and configuration files</span></span>

<span data-ttu-id="441a9-104">**Kaynak kodu dönüştürme,** paketin `content` veya `contentFiles` klasöründeki dosyalara tek`content` yönlü belirteç `packages.config` `contentFiles` değiştirme `PackageReference`(paket yüklendiğinde ve için) için, jetonların Visual Studio [proje özelliklerine](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7)atıfta bulunduğu dosyalara tek yönlü belirteç değiştirme uygular.</span><span class="sxs-lookup"><span data-stu-id="441a9-104">A **source code transformation** applies one-way token replacement to files in the package's `content` or `contentFiles` folder (`content` for customers using `packages.config` and `contentFiles` for `PackageReference`) when the package is installed, where tokens refer to Visual Studio [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span></span> <span data-ttu-id="441a9-105">Bu, projenin ad alanına bir dosya eklemenize veya genellikle ASP.NET bir `global.asax` projede girecek kodu özelleştirmenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="441a9-105">This allows you to insert a file into the project's namespace, or to customize code that would typically go into `global.asax` in an ASP.NET project.</span></span>

<span data-ttu-id="441a9-106">**Config dosyası dönüştürme,** hedef projede zaten var olan dosyaları `web.config` `app.config`değiştirmenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="441a9-106">A **config file transformation** allows you to modify files that already exist in a target project, such as `web.config` and `app.config`.</span></span> <span data-ttu-id="441a9-107">Örneğin, paketinizin config dosyasındaki `modules` bölüme bir öğe eklemesi gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="441a9-107">For example, your package might need to add an item to the `modules` section in the config file.</span></span> <span data-ttu-id="441a9-108">Bu dönüştürme, yapılandırma dosyalarına eklenecek bölümleri açıklayan pakete özel dosyalar eklenerek yapılır.</span><span class="sxs-lookup"><span data-stu-id="441a9-108">This transformation is done by including special files in the package that describe the sections to add to the configuration files.</span></span> <span data-ttu-id="441a9-109">Bir paket kaldırıldığında, aynı değişiklikler daha sonra tersine çevrilerek bu iki yönlü bir dönüştürme haline getirir.</span><span class="sxs-lookup"><span data-stu-id="441a9-109">When a package is uninstalled, those same changes are then reversed, making this a two-way transformation.</span></span>

## <a name="specifying-source-code-transformations"></a><span data-ttu-id="441a9-110">Kaynak kodu dönüşümlerini belirtme</span><span class="sxs-lookup"><span data-stu-id="441a9-110">Specifying source code transformations</span></span>

1. <span data-ttu-id="441a9-111">Paketten projeye eklemek istediğiniz dosyalar paketin `content` ve `contentFiles` klasörlerin içinde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="441a9-111">Files that you want to insert from the package into the project must be located within the package's `content` and `contentFiles` folders.</span></span> <span data-ttu-id="441a9-112">Örneğin, çağrılan `ContosoData.cs` bir dosyanın hedef projenin bir `Models` klasörüne yüklenmesini istiyorsanız, dosyanın `content\Models` paketteki ve `contentFiles\{lang}\{tfm}\Models` klasörlerin içinde olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="441a9-112">For example, if you want a file called `ContosoData.cs` to be installed in a `Models` folder of the target project, it must be inside the `content\Models` and `contentFiles\{lang}\{tfm}\Models` folders in the package.</span></span>

1. <span data-ttu-id="441a9-113">NuGet'e yükleme zamanında belirteç değiştirme `.pp` uygulaması talimatı vermek için kaynak kodu dosya adını ekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="441a9-113">To instruct NuGet to apply token replacement at install time, append `.pp` to the source code file name.</span></span> <span data-ttu-id="441a9-114">Yüklemeden sonra, dosya uzantısı `.pp` olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="441a9-114">After installation, the file will not have the `.pp` extension.</span></span>

    <span data-ttu-id="441a9-115">Örneğin, dönüşümler yapmak `ContosoData.cs`için , paketteki `ContosoData.cs.pp`dosyayı adlandırın.</span><span class="sxs-lookup"><span data-stu-id="441a9-115">For example, to make transformations in `ContosoData.cs`, name the file in the package `ContosoData.cs.pp`.</span></span> <span data-ttu-id="441a9-116">Kurulumdan sonra . `ContosoData.cs`</span><span class="sxs-lookup"><span data-stu-id="441a9-116">After installation it will appear as `ContosoData.cs`.</span></span>

1. <span data-ttu-id="441a9-117">Kaynak kod dosyasında, NuGet'in proje özellikleriyle `$token$` değiştirmesi gereken değerleri belirtmek için formun büyük/küçük harf duyarlı belirteçlerini kullanın:</span><span class="sxs-lookup"><span data-stu-id="441a9-117">In the source code file, use case-insensitive tokens of the form `$token$` to indicate values that NuGet should replace with project properties:</span></span>

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

    <span data-ttu-id="441a9-118">Yükleme üzerine, NuGet `$rootnamespace$` `Fabrikam` hedef projenin kök ad alanı olduğunu `Fabrikam`varsayarak değiştirir.</span><span class="sxs-lookup"><span data-stu-id="441a9-118">Upon installation, NuGet replaces `$rootnamespace$` with `Fabrikam` assuming the target project's whose root namespace is `Fabrikam`.</span></span>

<span data-ttu-id="441a9-119">Belirteç `$rootnamespace$` en yaygın olarak kullanılan proje özelliğidir; diğerleri [proje özelliklerinde](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7)listelenir.</span><span class="sxs-lookup"><span data-stu-id="441a9-119">The `$rootnamespace$` token is the most commonly used project property; all others are listed in [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7).</span></span> <span data-ttu-id="441a9-120">Elbette, bazı özelliklerin proje türüne özgü olabileceğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="441a9-120">Be mindful, of course, that some properties might be specific to the project type.</span></span>

## <a name="specifying-config-file-transformations"></a><span data-ttu-id="441a9-121">Config dosya dönüşümlerini belirtme</span><span class="sxs-lookup"><span data-stu-id="441a9-121">Specifying config file transformations</span></span>

<span data-ttu-id="441a9-122">Takip eden bölümlerde açıklandığı gibi, config dosya dönüşümleri iki şekilde yapılabilir:</span><span class="sxs-lookup"><span data-stu-id="441a9-122">As described in the sections that follow, config file transformations can be done in two ways:</span></span>

- <span data-ttu-id="441a9-123">Uzantı, Paket yüklü `content` olduğunda varolan config dosyalarıyla birleştirmek için Bu dosyaların XML içerdiğini NuGet'e söylediği paketin klasörüne `web.config.transform` ve dosyalarını ekleyin. `app.config.transform` `.transform`</span><span class="sxs-lookup"><span data-stu-id="441a9-123">Include `app.config.transform` and `web.config.transform` files in your package's `content` folder, where the `.transform` extension tells NuGet that these files contain the XML to merge with existing config files when the package is installed.</span></span> <span data-ttu-id="441a9-124">Bir paket kaldırıldığında, aynı XML kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="441a9-124">When a package is uninstalled, that same XML is removed.</span></span>
- <span data-ttu-id="441a9-125">İstediğindeğişiklikleri `web.config.install.xdt` açıklamak için [XDT sözdizimini](https://msdn.microsoft.com/library/dd465326.aspx) kullanarak paketinizin `content` klasörüne dosya ekleyin `app.config.install.xdt` ve dosya ekleyin.</span><span class="sxs-lookup"><span data-stu-id="441a9-125">Include `app.config.install.xdt` and `web.config.install.xdt` files in your package's `content` folder, using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx) to describe the desired changes.</span></span> <span data-ttu-id="441a9-126">Bu seçenekle, paket `.uninstall.xdt` projeden kaldırıldığında değişiklikleri tersine çevirecek bir dosya da ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="441a9-126">With this option you can also include a `.uninstall.xdt` file to reverse changes when the package is removed from a project.</span></span>

> [!Note]
> <span data-ttu-id="441a9-127">Dönüşümler Visual Studio'da `.config` bağlantı olarak başvurulan dosyalara uygulanmaz.</span><span class="sxs-lookup"><span data-stu-id="441a9-127">Transformations are not applied to `.config` files referenced as a link in Visual Studio.</span></span>

<span data-ttu-id="441a9-128">XDT kullanmanın avantajı, yalnızca iki statik dosyayı birleştirmek yerine, tam XPath desteğini kullanarak öğe ve öznitelik eşleştirme kullanarak Bir XML DOM yapısını işlemek için bir sözdizimi sağlamasıdır.</span><span class="sxs-lookup"><span data-stu-id="441a9-128">The advantage of using XDT is that instead of simply merging two static files, it provides a syntax for manipulating the structure of an XML DOM using element and attribute matching using full XPath support.</span></span> <span data-ttu-id="441a9-129">XDT daha sonra öğeleri ekleyebilir, güncelleyebilir veya kaldırabilir, belirli bir konuma yeni öğeler yerleyebilir veya öğeleri değiştirebilir/kaldırabilir (alt düğümler dahil).</span><span class="sxs-lookup"><span data-stu-id="441a9-129">XDT can then add, update, or remove elements, place new elements at a specific location, or replace/remove elements (including child nodes).</span></span> <span data-ttu-id="441a9-130">Bu, paket yükleme sırasında yapılan tüm dönüşümleri geri kaldıran kaldırma dönüşümleri oluşturmayı kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="441a9-130">This makes it straightforward to create uninstall transforms that back out all transformations done during package installation.</span></span>

### <a name="xml-transforms"></a><span data-ttu-id="441a9-131">XML dönüştürür</span><span class="sxs-lookup"><span data-stu-id="441a9-131">XML transforms</span></span>

<span data-ttu-id="441a9-132">Ve `app.config.transform` `web.config.transform` bir paketin `content` klasöründe yalnızca projenin varolan `app.config` ve `web.config` dosyaları birleştirmek için bu öğeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="441a9-132">The `app.config.transform` and `web.config.transform` in a package's `content` folder contain only those elements to merge into the project's existing `app.config` and `web.config` files.</span></span>

<span data-ttu-id="441a9-133">Örnek olarak, projenin başlangıçta aşağıdaki içeriği `web.config`içerdiğini varsayalım:</span><span class="sxs-lookup"><span data-stu-id="441a9-133">As an example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="441a9-134">Paket yükleme `MyNuModule` sırasında `modules` bölüme bir öğe `web.config.transform` eklemek için, paketin `content` klasöründe aşağıdaki gibi görünen bir dosya oluşturun:</span><span class="sxs-lookup"><span data-stu-id="441a9-134">To add a `MyNuModule` element to the `modules` section during package install, create a `web.config.transform` file in the package's `content` folder that looks like this:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="441a9-135">NuGet paketi `web.config` yükledikten sonra aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="441a9-135">After NuGet installs the package, `web.config` will appear as follows:</span></span>

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

<span data-ttu-id="441a9-136">`modules` NuGet'in bölümün yerini almadığını, yalnızca yeni öğeler ve öznitelikler ekleyerek yeni girişi birleştirdiğini fark edin.</span><span class="sxs-lookup"><span data-stu-id="441a9-136">Notice that NuGet didn't replace the `modules` section, it just merged the new entry into it by adding only new elements and attributes.</span></span> <span data-ttu-id="441a9-137">NuGet varolan öğeleri veya öznitelikleri değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="441a9-137">NuGet will not change any existing elements or attributes.</span></span>

<span data-ttu-id="441a9-138">Paket kaldırıldığında, NuGet `.transform` dosyaları yeniden inceler ve içerdiği öğeleri uygun `.config` dosyalardan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="441a9-138">When the package is uninstalled, NuGet will examine the `.transform` files again and remove the elements it contains from the appropriate `.config` files.</span></span> <span data-ttu-id="441a9-139">Bu `.config` işlemin, paket yüklemeden sonra değiştirdiğiniz dosyadaki satırları etkilemeyeceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="441a9-139">Note that this process will not affect any lines in the `.config` file that you modify after package installation.</span></span>

<span data-ttu-id="441a9-140">Daha kapsamlı bir örnek olarak, [ASP.NET için Hata Günlüğü Modülleri ve İşleyiciler (ELMAH)](https://www.nuget.org/packages/elmah/) paketi, bir paket kaldırıldığında yeniden kaldırılan `web.config`birçok giriş ekler.</span><span class="sxs-lookup"><span data-stu-id="441a9-140">As a more extensive example, the [Error Logging Modules and Handlers for ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) package adds many entries into `web.config`, which are again removed when a package is uninstalled.</span></span>

<span data-ttu-id="441a9-141">Dosyasını `web.config.transform` incelemek için, elmah paketini yukarıdaki bağlantıdan indirin, paket uzantısını ''dan `.nupkg` ' ''a `.zip`çevirin ve sonra o ZIP dosyasında açın. `content\web.config.transform`</span><span class="sxs-lookup"><span data-stu-id="441a9-141">To examine its `web.config.transform` file, download the ELMAH package from the link above, change the package extension from `.nupkg` to `.zip`, and then open `content\web.config.transform` in that ZIP file.</span></span>

<span data-ttu-id="441a9-142">Paketi yükleme ve kaldırma nın etkisini görmek için Visual Studio'da yeni bir ASP.NET projesi oluşturun (şablon Yeni Proje iletişim kutusunda **Visual C# > Web** altındadır) ve boş bir ASP.NET uygulaması seçin.</span><span class="sxs-lookup"><span data-stu-id="441a9-142">To see the effect of installing and uninstalling the package, create a new ASP.NET project in Visual Studio (the template is under **Visual C# > Web** in the New Project dialog), and select an empty ASP.NET application.</span></span> <span data-ttu-id="441a9-143">İlk `web.config` durumunu görmek için açın.</span><span class="sxs-lookup"><span data-stu-id="441a9-143">Open `web.config` to see its initial state.</span></span> <span data-ttu-id="441a9-144">Ardından projeyi sağ tıklatın, **NuGet Paketlerini Yönet'i**seçin, nuget.org'da ELMAH'a göz atın ve en son sürümü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="441a9-144">Then right-click the project, select **Manage NuGet Packages**, browse for ELMAH on nuget.org, and install the latest version.</span></span> <span data-ttu-id="441a9-145">Tüm değişikliklere `web.config`dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="441a9-145">Notice all the changes to `web.config`.</span></span> <span data-ttu-id="441a9-146">Şimdi paketi kaldırın ve `web.config` önceki durumuna geri dönmek bakın.</span><span class="sxs-lookup"><span data-stu-id="441a9-146">Now uninstall the package and you see `web.config` revert to its prior state.</span></span>

### <a name="xdt-transforms"></a><span data-ttu-id="441a9-147">XDT dönüştürür</span><span class="sxs-lookup"><span data-stu-id="441a9-147">XDT transforms</span></span>

> [!Note]
> <span data-ttu-id="441a9-148">Aşağıda açıklandığı gibi , XDT [dönüşümleri geçiş `packages.config` `PackageReference`için dokümanların paket uyumluluk sorunları bölümünde ](../consume-packages/migrate-packages-config-to-package-reference.md#package-compatibility-issues)belirtildiği gibi `packages.config`sadece desteklenir .</span><span class="sxs-lookup"><span data-stu-id="441a9-148">As mentioned in the [package compatibility issues section of the docs for migrating from `packages.config` to `PackageReference`](../consume-packages/migrate-packages-config-to-package-reference.md#package-compatibility-issues), XDT transformations as described below are only supported by `packages.config`.</span></span> <span data-ttu-id="441a9-149">Aşağıdaki dosyaları paketinize eklerseniz, paketinizi `PackageReference` kullanan tüketiciler dönüşümleri uygulamaz (XDT dönüşümlerinin işe yaraması için bu [örneğe](https://github.com/NuGet/Samples/tree/master/XDTransformExample) `PackageReference`bakın).</span><span class="sxs-lookup"><span data-stu-id="441a9-149">If you add the below files to your package, consumers using your package with `PackageReference` will not have the transformations applied (refer to [this sample](https://github.com/NuGet/Samples/tree/master/XDTransformExample) to make XDT transforms work with`PackageReference`).</span></span>

<span data-ttu-id="441a9-150">[XDT sözdizimini](https://msdn.microsoft.com/library/dd465326.aspx)kullanarak config dosyalarını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="441a9-150">You can modify config files using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx).</span></span> <span data-ttu-id="441a9-151">Ayrıca, nuget belirteçleri [proje özellikleri](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) ile delimiters `$` (büyük/küçük harf duyarsız) içinde özellik adını ekleyerek değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="441a9-151">You can also have NuGet replace tokens with [project properties](/dotnet/api/vslangproj.projectproperties?view=visualstudiosdk-2017&viewFallbackFrom=netframework-4.7) by including the property name within `$` delimiters (case-insensitive).</span></span>

<span data-ttu-id="441a9-152">`app.config.install.xdt` Örneğin, aşağıdaki dosya projeden `appSettings` `app.config` `FullPath`, ve `FileName` `ActiveConfigurationSettings` değerleri içeren bir öğe ekler:</span><span class="sxs-lookup"><span data-stu-id="441a9-152">For example, the following `app.config.install.xdt` file will insert an `appSettings` element into `app.config` containing the `FullPath`, `FileName`, and `ActiveConfigurationSettings` values from the project:</span></span>

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

<span data-ttu-id="441a9-153">Başka bir örnek olarak, projenin başlangıçta `web.config`aşağıdaki içeriği içerdiğini varsayalım:</span><span class="sxs-lookup"><span data-stu-id="441a9-153">For another example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="441a9-154">Paket yükleme `MyNuModule` sırasında `modules` bölüme bir öğe eklemek `web.config.install.xdt` için, paketin aşağıdakileri içerir:</span><span class="sxs-lookup"><span data-stu-id="441a9-154">To add a `MyNuModule` element to the `modules` section during package install, the package's `web.config.install.xdt` would contain the following:</span></span>

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

<span data-ttu-id="441a9-155">Paketi yükledikten `web.config` sonra, bu gibi görünecektir:</span><span class="sxs-lookup"><span data-stu-id="441a9-155">After installing the package, `web.config` will look like this:</span></span>

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

<span data-ttu-id="441a9-156">Paket kaldırma `MyNuModule` sırasında yalnızca öğeyi `web.config.uninstall.xdt` kaldırmak için dosya aşağıdakileri içermelidir:</span><span class="sxs-lookup"><span data-stu-id="441a9-156">To remove only the `MyNuModule` element during package uninstall, the `web.config.uninstall.xdt` file should contain the following:</span></span>

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
