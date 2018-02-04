---
title: "Tanıtım kılavuzu oluşturma ve yayımlama NuGet paketi | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/03/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Oluşturma ve yayımlama nuget.exe komut satırı arabirimi ve Visual Studio kullanarak bir NuGet paketi bir gözden geçirme Öğreticisi."
keywords: "NuGet paket oluşturma, yayımlama, NuGet paketi NuGet Öğreticisi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 53d29283c9e786fc27e9a608d7d251d8d0b5b0b2
ms.sourcegitcommit: 24997b5345a997501fff846c9bd73610245ae0a6
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/31/2018
---
# <a name="create-and-publish-a-package"></a><span data-ttu-id="a2315-104">Oluşturma ve bir paket yayımlama</span><span class="sxs-lookup"><span data-stu-id="a2315-104">Create and publish a package</span></span>

<span data-ttu-id="a2315-105">Bir .NET sınıf kitaplığı'ndan bir NuGet paketi oluşturmak ve nuget.org için yayımlamak için basit bir işlemdir. Bu makalede NuGet komut satırı arabirimi (CLI) ve Visual Studio kullanarak işleminde size kılavuzluk eder.</span><span class="sxs-lookup"><span data-stu-id="a2315-105">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org. This article walks you through the process using the NuGet command-line interface (CLI) and Visual Studio.</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="a2315-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a2315-106">Pre-requisites</span></span>

1. <span data-ttu-id="a2315-107">Visual Studio 2017 ' herhangi bir sürümünü yüklemek [visualstudio.com](https://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="a2315-107">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/).</span></span>

1. <span data-ttu-id="a2315-108">NuGet CLI Aracı'nı yüklemeden `nuget.exe`, en son sürümünü yükleyerek `nuget.exe` gelen [nuget.org/downloads](https://nuget.org/downloads)ve kaydetme `.exe` yolda bir konuma.</span><span class="sxs-lookup"><span data-stu-id="a2315-108">Install the NuGet CLI tool, `nuget.exe`, by downloading the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), and saving the `.exe` to a location in your PATH.</span></span> <span data-ttu-id="a2315-109">Unutmayın indirme *olan* aracı, bir yükleyici.</span><span class="sxs-lookup"><span data-stu-id="a2315-109">Note that the download *is* the tool itself, not an installer.</span></span>

1. <span data-ttu-id="a2315-110">Paket istediğiniz kod için uygun bir .NET sınıf kitaplığı projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a2315-110">Create a suitable .NET Class Library project for the code you want to package.</span></span> <span data-ttu-id="a2315-111">Bir proje zaten sahip değilseniz, basit bir şekilde oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a2315-111">If you don't already have a project, you can create a simple one as follows:</span></span>
    1. <span data-ttu-id="a2315-112">Visual Studio'da, **Dosya > Yeni > Proje**, genişletin **Visual C# > Windows** düğümü, "Sınıf kitaplığı" şablonunu seçin, AppLogger proje adı ve tıklayın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="a2315-112">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > Windows** node, select the "Class Library" template, name the project AppLogger, and click **OK**.</span></span>
    1. <span data-ttu-id="a2315-113">Sonuçta elde edilen proje dosyasını sağ tıklatın ve seçin **yapı** projeyi düzgün bir şekilde oluşturuldu emin olmak için.</span><span class="sxs-lookup"><span data-stu-id="a2315-113">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="a2315-114">DLL Debug klasörüne (veya bunun yerine bu yapılandırma yapı sürüm) içinde bulunur.</span><span class="sxs-lookup"><span data-stu-id="a2315-114">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

    <span data-ttu-id="a2315-115">Gerçek bir NuGet paketi içinde doğal olarak, bağlı diğer uygulamaları geliştirmek çok sayıda kullanışlı özellikle uygulaması.</span><span class="sxs-lookup"><span data-stu-id="a2315-115">Within a real NuGet package, of course, you'll implement many useful features upon which others can build applications.</span></span> <span data-ttu-id="a2315-116">Bir sınıf kitaplığı şablondan bir paket oluşturmak yeterli olduğundan bu kılavuzda ancak, herhangi bir ek kod yazma olmaz.</span><span class="sxs-lookup"><span data-stu-id="a2315-116">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span>

## <a name="create-the-nuspec-package-manifest-file"></a><span data-ttu-id="a2315-117">.Nuspec paket bildirim dosyası oluştur</span><span class="sxs-lookup"><span data-stu-id="a2315-117">Create the .nuspec package manifest file</span></span>

<span data-ttu-id="a2315-118">Bir bildirim her NuGet paketi gerekir&mdash;bir `.nuspec` dosya&mdash;içeriğini ve onun bağımlılıklarını açıklamak için.</span><span class="sxs-lookup"><span data-stu-id="a2315-118">Every NuGet package needs a manifest&mdash;a `.nuspec` file&mdash;to describe its contents and its dependencies.</span></span> <span data-ttu-id="a2315-119">`nuget spec` Komutu, sizin için hangi sonra özelleştirin bu dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a2315-119">The `nuget spec` command creates this file for you, which you then customize.</span></span> <span data-ttu-id="a2315-120">Bu örnekte, oluşturduğunuz `.nuspec` proje dosyasından; ayrıca arasında başka yollarla bildirimi açıklandığı gibi oluşturabilirsiniz [bir paket oluşturun](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="a2315-120">In this example you create the `.nuspec` from a project file; you can also create the manifest through other means as described on [Create a Package](../create-packages/creating-a-package.md).</span></span>

1. <span data-ttu-id="a2315-121">Bir komut istemi açın ve proje dosyasını içeren klasöre gidin (`.csproj`).</span><span class="sxs-lookup"><span data-stu-id="a2315-121">Open a command prompt and navigate to the folder containing your project file (`.csproj`).</span></span>

1. <span data-ttu-id="a2315-122">NuGet CLI çalıştırmak `spec` projenizi sonra gibi adlı bildirim oluşturmak üzere komut `AppLogger.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="a2315-122">Run the NuGet CLI `spec` command to generate the manifest, which is named after your project, such as `AppLogger.nuspec`:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="a2315-123">Dosyayı bir metin düzenleyicisinde açın.</span><span class="sxs-lookup"><span data-stu-id="a2315-123">Open the file in a text editor.</span></span> <span data-ttu-id="a2315-124">Bildirim yere aşağıdaki kod şöyle görünür belirteçleri biçiminde `<token>` (gibi `$id$`) olması değiştirilir paket oluşturma işlemi sırasında projenin Properties/AssemblyInfo.cs dosyasından gelen değerlerle.</span><span class="sxs-lookup"><span data-stu-id="a2315-124">The manifest looks something like the code below, where tokens in the form `<token>` (such as `$id$`) are be replaced during the packaging process with values from the project's Properties/AssemblyInfo.cs file.</span></span> <span data-ttu-id="a2315-125">Belirteçleri hakkında daha fazla bilgi için bkz: [.nuspec dosyası oluşturma](../create-packages/creating-a-package.md#creating-the-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="a2315-125">For more details on tokens, see [Creating a .nuspec file](../create-packages/creating-a-package.md#creating-the-nuspec-file).</span></span>

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>$id$</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>$author$</authors>
        <owners>$author$</owners>
        <licenseUrl>http://LICENSE_URL_HERE_OR_DELETE_THIS_LINE</licenseUrl>
        <projectUrl>http://PROJECT_URL_HERE_OR_DELETE_THIS_LINE</projectUrl>
        <iconUrl>http://ICON_URL_HERE_OR_DELETE_THIS_LINE</iconUrl>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>$description$</description>
        <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>Tag1 Tag2</tags>
        </metadata>
    </package>
    ```

1. <span data-ttu-id="a2315-126">Nuget.org arasında benzersiz olan bir paket kimliği seçin. Açıklanan adlandırma kuralları kullanmanızı öneririz [paket oluşturma](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="a2315-126">Select a package ID that is unique across nuget.org. We recommend using the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="a2315-127">Yazar ve açıklama etiketleri güncelleştirdiğinizden emin olun veya sonraki adımda bir hata alıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="a2315-127">Be sure to update the author and description tags or you get an error in the next step.</span></span> <span data-ttu-id="a2315-128">İşte güncelleştirilmiş `.nuspec` dosyası bir örnek olarak:</span><span class="sxs-lookup"><span data-stu-id="a2315-128">Here's an updated `.nuspec` file as an example:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>MyCompanyName.MyProductName.MyPackageName</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>kraigb</authors>
        <owners>kraigb</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>application app logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Note]
> <span data-ttu-id="a2315-129">Ortak tüketim için oluşturulan paketler için özel dikkat `<tags>` öğesi, bu etiketler başkalarının paketinizi bulun ve neler yaptığını anlamanıza yardımcı olmak gibi.</span><span class="sxs-lookup"><span data-stu-id="a2315-129">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="a2315-130">Paketi komutunu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="a2315-130">Run the pack command</span></span>

<span data-ttu-id="a2315-131">Bir NuGet paketi oluşturmak için (bir `.nupkg` dosyası) bir projeden çalıştırmak `pack` komutu:</span><span class="sxs-lookup"><span data-stu-id="a2315-131">To build a NuGet package (a `.nupkg` file) from a project, run the `pack` command:</span></span>

```cli
nuget pack AppLogger.csproj
```

<span data-ttu-id="a2315-132">Bu komut oluşturur `AppLogger.1.0.0.0.nupkg` paket adı ve sürüm numarası kullanarak `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="a2315-132">This command creates `AppLogger.1.0.0.0.nupkg` using the package name and version number from the `.nuspec` file.</span></span> <span data-ttu-id="a2315-133">Çeşitli alanları güncelleştirmediyseniz uyarıları komutu verdiğinde `.nuspec` varsayılan değerlerine dosyasından.</span><span class="sxs-lookup"><span data-stu-id="a2315-133">The command issues warnings if you haven't updated various fields in the `.nuspec` file from their default values.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="a2315-134">Paket yayımlama</span><span class="sxs-lookup"><span data-stu-id="a2315-134">Publish the package</span></span>

<span data-ttu-id="a2315-135">Bulduktan sonra bir `.nupkg` dosyası, yayımlama, nuget.org kullanmaya `push` komutu.</span><span class="sxs-lookup"><span data-stu-id="a2315-135">Once you have a `.nupkg` file, you publish it to nuget.org using the `push` command.</span></span> <span data-ttu-id="a2315-136">(Alternatif olarak, kullanabileceğiniz [nuget.org yayımlama iş akışı](../create-packages/publish-a-package.md#publish-to-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="a2315-136">(Alternately, you can use the [nuget.org publishing workflow](../create-packages/publish-a-package.md#publish-to-nugetorg).</span></span>

> [!Warning]
> <span data-ttu-id="a2315-137">Nuget.org için yayımlama paketleri diğer geliştiricilerine herkese görünür.</span><span class="sxs-lookup"><span data-stu-id="a2315-137">The packages you publish to nuget.org are publicly visible to other developers.</span></span> <span data-ttu-id="a2315-138">Paketleri özel olarak barındırmak için bkz: [paketleri barındırma](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="a2315-138">To host packages privately, see [Hosting packages](../hosting-packages/overview.md).</span></span>

1. <span data-ttu-id="a2315-139">Ücretsiz bir hesap oluşturmak [nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), veya zaten varsa oturum açın.</span><span class="sxs-lookup"><span data-stu-id="a2315-139">Create a free account on [nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), or log in if you already have one.</span></span> <span data-ttu-id="a2315-140">Yeni bir hesap oluşturmadan bir onay e-posta gönderir.</span><span class="sxs-lookup"><span data-stu-id="a2315-140">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="a2315-141">Bir paket karşıya yüklemeden önce hesap onaylamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a2315-141">You must confirm the account before you can upload a package.</span></span>

1. <span data-ttu-id="a2315-142">Oturum açtıktan sonra kullanıcı adınızın (sağ üstte) seçin ve ardından **API anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="a2315-142">Once logged in, select your user name (on the upper right), then select **API Keys**.</span></span>

1. <span data-ttu-id="a2315-143">Seçin **oluşturma**, anahtarınız için bir ad, seçin **kapsamları seçin > anında** altında **API anahtarı**, girin \* için **Glob düzeni**, ardından seçin **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="a2315-143">Select **Create**, provide a name for your key, select **Select Scopes > Push** under **API Key**, enter \* for **Glob pattern**, then select **Create**.</span></span>

1. <span data-ttu-id="a2315-144">Anahtar oluşturulduktan sonra Seç **kopyalama** erişim almak için anahtar CLI sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="a2315-144">Once the key is created, select **Copy** to retrieve the access key you'll need in the CLI:</span></span>

    ![API anahtarını Panoya kopyalama](media/QS_Create-02-APIKey.png)

    > [!Warning]
    > <span data-ttu-id="a2315-146">Anahtarınızı güvenli bir konuma kaydedin ve gizli tutun.</span><span class="sxs-lookup"><span data-stu-id="a2315-146">Save your key in a secure location and keep it secret.</span></span> <span data-ttu-id="a2315-147">Anahtarınızı yanlışlıkla açığa, herhangi bir zamanda yeniden oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2315-147">If your key is accidentally revealed, you can regenerate it at any time.</span></span> <span data-ttu-id="a2315-148">Artık paketleri CLI itmek istiyorsanız, API anahtarını da kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a2315-148">You can also remove the API key if you no longer want to push packages via the CLI.</span></span>

1. <span data-ttu-id="a2315-149">Aşağıdaki komutu çalıştırın istemine, paket adı belirtme ve anahtar değeri ile değiştirerek 4. adımda kopyalanan:</span><span class="sxs-lookup"><span data-stu-id="a2315-149">At a command prompt, run the following command, specifying your package name and replacing the key with the value copied in step 4:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.0.nupkg 47be3377-c434-4c29-8576-af7f6993a54b -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="a2315-150">nuget.exe yayımlama işleminin sonuçlarını görüntüler:</span><span class="sxs-lookup"><span data-stu-id="a2315-150">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed. 
    ```

1. <span data-ttu-id="a2315-151">Profilinizdeki nuget.org üzerinde seçin **paketlerini Yönet** bir görmek için yalnızca yayımlanmış.</span><span class="sxs-lookup"><span data-stu-id="a2315-151">From your profile on nuget.org, Select **Manage Packages** to see the one you just published.</span></span> <span data-ttu-id="a2315-152">Aynı zamanda bir onay e-posta alırsınız.</span><span class="sxs-lookup"><span data-stu-id="a2315-152">You also receive a confirmation email.</span></span> <span data-ttu-id="a2315-153">Biraz sıralanması ve diğerleri bulabileceğiniz arama sonuçlarında görüntülenmesi paketinize sürebileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a2315-153">Note that it might take a while for your package to be indexed and appear in search results where others can find it.</span></span> <span data-ttu-id="a2315-154">Bu işlem sırasında paket sayfanızı aşağıdaki iletiyi gösterir:</span><span class="sxs-lookup"><span data-stu-id="a2315-154">During that time your package page shows the message below:</span></span>

    ![Bu paket henüz dizin değil.](media/QS_Create-03-NotIndexed.png)

> [!Note]
> <span data-ttu-id="a2315-157">**Virüs tarama**: tüm paketler için nuget.org karşıya virüs taraması ve herhangi bir virüs bulunursa reddetti.</span><span class="sxs-lookup"><span data-stu-id="a2315-157">**Virus scanning**: All packages uploaded to nuget.org are scanned for viruses and rejected if any viruses are found.</span></span> <span data-ttu-id="a2315-158">Nuget.org üzerinde listelenen tüm paketler de düzenli aralıklarla taranır.</span><span class="sxs-lookup"><span data-stu-id="a2315-158">All packages listed on nuget.org are also scanned periodically.</span></span>

<span data-ttu-id="a2315-159">Ve bu kadar!</span><span class="sxs-lookup"><span data-stu-id="a2315-159">And that's it!</span></span> <span data-ttu-id="a2315-160">Yalnızca ilk NuGet paketinizi yayımladıktan [nuget.org](https://www.nuget.org/), diğer geliştiricilerin kendi projelerinde kullanabileceğiniz.</span><span class="sxs-lookup"><span data-stu-id="a2315-160">You've just published your first NuGet package to [nuget.org](https://www.nuget.org/), that other developers can use in their own projects.</span></span>

## <a name="related-topics"></a><span data-ttu-id="a2315-161">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="a2315-161">Related topics</span></span>

- [<span data-ttu-id="a2315-162">Bir paket oluşturun</span><span class="sxs-lookup"><span data-stu-id="a2315-162">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="a2315-163">Paket Yayımlama</span><span class="sxs-lookup"><span data-stu-id="a2315-163">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="a2315-164">Birden çok hedef çerçeveyi desteği</span><span class="sxs-lookup"><span data-stu-id="a2315-164">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="a2315-165">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="a2315-165">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="a2315-166">Yerelleştirilmiş paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="a2315-166">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
