---
title: "Tanıtım kılavuzu oluşturma ve yayımlama NuGet paketi | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/3/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 91781ed6-da5c-49f0-b973-16dd8ad84229
description: "Oluşturma ve yayımlama nuget.exe komut satırı arabirimi ve Visual Studio kullanarak bir NuGet paketi bir gözden geçirme Öğreticisi."
keywords: "NuGet paket oluşturma, yayımlama, NuGet paketi NuGet Öğreticisi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 36a7c2b1d056dddf07a59737de1c3e94294689ac
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="create-and-publish-a-package"></a><span data-ttu-id="8f864-104">Oluşturma ve bir paket yayımlama</span><span class="sxs-lookup"><span data-stu-id="8f864-104">Create and publish a package</span></span>

<span data-ttu-id="8f864-105">Bir .NET sınıf kitaplığı'ndan bir NuGet paketi oluşturmak ve nuget.org için yayımlamak için basit bir işlemdir. Aşağıdaki adımlar NuGet komut satırı arabirimi (CLI) ve Visual Studio kullanarak işleminde size yol:</span><span class="sxs-lookup"><span data-stu-id="8f864-105">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org. The following steps walk you through the process using the NuGet command-line interface (CLI) and Visual Studio:</span></span>

- [<span data-ttu-id="8f864-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8f864-106">Pre-requisites</span></span>](#install-pre-requisites)
- [<span data-ttu-id="8f864-107">.Nuspec paket bildirim dosyası oluştur</span><span class="sxs-lookup"><span data-stu-id="8f864-107">Create the .nuspec package manifest file</span></span>](#create-the-nuspec-package-manifest-file)
- [<span data-ttu-id="8f864-108">Paketi komutunu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="8f864-108">Run the pack command</span></span>](#run-the-pack-command)
- [<span data-ttu-id="8f864-109">Paket yayımlama</span><span class="sxs-lookup"><span data-stu-id="8f864-109">Publish the package</span></span>](#publish-the-package)

## <a name="pre-requisites"></a><span data-ttu-id="8f864-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8f864-110">Pre-requisites</span></span>

1. <span data-ttu-id="8f864-111">Visual Studio 2017 ' herhangi bir sürümünü yüklemek [visualstudio.com](https://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="8f864-111">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/).</span></span>

1. <span data-ttu-id="8f864-112">NuGet CLI Aracı'nı yüklemeden `nuget.exe`, en son sürümünü yükleyerek `nuget.exe` gelen [nuget.org/downloads](https://nuget.org/downloads)ve kaydetme `.exe` yolda bir konuma.</span><span class="sxs-lookup"><span data-stu-id="8f864-112">Install the NuGet CLI tool, `nuget.exe`, by downloading the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), and saving the `.exe` to a location in your PATH.</span></span> <span data-ttu-id="8f864-113">Unutmayın indirme *olan* aracı, bir yükleyici.</span><span class="sxs-lookup"><span data-stu-id="8f864-113">Note that the download *is* the tool itself, not an installer.</span></span>

1. <span data-ttu-id="8f864-114">Paket istediğiniz kod için uygun bir .NET sınıf kitaplığı projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8f864-114">Create a suitable .NET Class Library project for the code you want to package.</span></span> <span data-ttu-id="8f864-115">Bir proje zaten sahip değilseniz, basit bir şekilde oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8f864-115">If you don't already have a project, you can create a simple one as follows:</span></span>
    1. <span data-ttu-id="8f864-116">Visual Studio'da, **Dosya > Yeni > Proje**, genişletin **Visual C# > Windows** düğümü, "Sınıf kitaplığı" şablonunu seçin, AppLogger proje adı ve tıklayın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="8f864-116">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > Windows** node, select the "Class Library" template, name the project AppLogger, and click **OK**.</span></span>
    1. <span data-ttu-id="8f864-117">Sonuçta elde edilen proje dosyasını sağ tıklatın ve seçin **yapı** projeyi düzgün bir şekilde oluşturuldu emin olmak için.</span><span class="sxs-lookup"><span data-stu-id="8f864-117">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="8f864-118">DLL Debug klasörüne (veya bunun yerine bu yapılandırma yapı sürüm) içinde bulunur.</span><span class="sxs-lookup"><span data-stu-id="8f864-118">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

    <span data-ttu-id="8f864-119">Gerçek bir NuGet paketi içinde doğal olarak, bağlı diğer uygulamaları geliştirmek çok sayıda kullanışlı özellikle uygulaması.</span><span class="sxs-lookup"><span data-stu-id="8f864-119">Within a real NuGet package, of course, you'll implement many useful features upon which others can build applications.</span></span> <span data-ttu-id="8f864-120">Bir sınıf kitaplığı şablondan bir paket oluşturmak yeterli olduğundan bu kılavuzda ancak, herhangi bir ek kod yazma olmaz.</span><span class="sxs-lookup"><span data-stu-id="8f864-120">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span>

## <a name="create-the-nuspec-package-manifest-file"></a><span data-ttu-id="8f864-121">.Nuspec paket bildirim dosyası oluştur</span><span class="sxs-lookup"><span data-stu-id="8f864-121">Create the .nuspec package manifest file</span></span>

<span data-ttu-id="8f864-122">Bir bildirim her NuGet paketi gerekir&mdash;bir `.nuspec` dosya&mdash;içeriğini ve onun bağımlılıklarını açıklamak için.</span><span class="sxs-lookup"><span data-stu-id="8f864-122">Every NuGet package needs a manifest&mdash;a `.nuspec` file&mdash;to describe its contents and its dependencies.</span></span> <span data-ttu-id="8f864-123">`nuget spec` Komutu, sizin için hangi sonra özelleştirin bu dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8f864-123">The `nuget spec` command creates this file for you, which you then customize.</span></span> <span data-ttu-id="8f864-124">Bu örnekte, oluşturduğunuz `.nuspec` proje dosyasından; ayrıca arasında başka yollarla bildirimi açıklandığı gibi oluşturabilirsiniz [bir paket oluşturun](../create-packages/creating-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="8f864-124">In this example you create the `.nuspec` from a project file; you can also create the manifest through other means as described on [Create a Package](../create-packages/creating-a-package.md).</span></span>

1. <span data-ttu-id="8f864-125">Bir komut istemi açın ve proje dosyasını içeren klasöre gidin (`.csproj`).</span><span class="sxs-lookup"><span data-stu-id="8f864-125">Open a command prompt and navigate to the folder containing your project file (`.csproj`).</span></span>

1. <span data-ttu-id="8f864-126">NuGet CLI çalıştırmak `spec` projenizi sonra gibi adlı bildirim oluşturmak üzere komut `AppLogger.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="8f864-126">Run the NuGet CLI `spec` command to generate the manifest, which is named after your project, such as `AppLogger.nuspec`:</span></span>

    ```
    nuget spec
    ```

1. <span data-ttu-id="8f864-127">Dosyayı bir metin düzenleyicisinde açın.</span><span class="sxs-lookup"><span data-stu-id="8f864-127">Open the file in a text editor.</span></span> <span data-ttu-id="8f864-128">Bildirim yere aşağıdaki kod şöyle görünür belirteçleri biçiminde  *$ `<token>` $*  olması değiştirilir paket oluşturma işlemi sırasında projenin Properties/AssemblyInfo.cs değerlerle dosya.</span><span class="sxs-lookup"><span data-stu-id="8f864-128">The manifest looks something like the code below, where tokens in the form *$`<token>`$* are be replaced during the packaging process with values from the project's Properties/AssemblyInfo.cs file.</span></span> <span data-ttu-id="8f864-129">Belirteçleri hakkında daha fazla bilgi için bkz: [.nuspec dosyası oluşturma](../create-packages/creating-a-package.md#creating-the-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="8f864-129">For more details on tokens, see [Creating a .nuspec file](../create-packages/creating-a-package.md#creating-the-nuspec-file).</span></span>

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

1. <span data-ttu-id="8f864-130">Nuget.org arasında benzersiz olan bir paket kimliği seçin. Açıklanan adlandırma kuralları kullanmanızı öneririz [paket oluşturma](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="8f864-130">Select a package ID that is unique across nuget.org. We recommend using the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="8f864-131">Yazar ve açıklama etiketleri güncelleştirdiğinizden emin olun veya sonraki adımda bir hata alıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="8f864-131">Be sure to update the author and description tags or you get an error in the next step.</span></span> <span data-ttu-id="8f864-132">İşte güncelleştirilmiş `.nuspec` dosyası bir örnek olarak:</span><span class="sxs-lookup"><span data-stu-id="8f864-132">Here's an updated `.nuspec` file as an example:</span></span>

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
> <span data-ttu-id="8f864-133">Ortak tüketim için oluşturulan paketler için özel dikkat `<tags>` öğesi, bu etiketler başkalarının paketinizi bulun ve neler yaptığını anlamanıza yardımcı olmak gibi.</span><span class="sxs-lookup"><span data-stu-id="8f864-133">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="8f864-134">Paketi komutunu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="8f864-134">Run the pack command</span></span>

<span data-ttu-id="8f864-135">Bir NuGet paketi oluşturmak için (bir `.nupkg` dosyası) bir projeden çalıştırmak `pack` komutu:</span><span class="sxs-lookup"><span data-stu-id="8f864-135">To build a NuGet package (a `.nupkg` file) from a project, run the `pack` command:</span></span>

```
nuget pack AppLogger.csproj
```

<span data-ttu-id="8f864-136">Bu komut oluşturur `AppLogger.1.0.0.0.nupkg` paket adı ve sürüm numarası kullanarak `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="8f864-136">This command creates `AppLogger.1.0.0.0.nupkg` using the package name and version number from the `.nuspec` file.</span></span> <span data-ttu-id="8f864-137">Çeşitli alanları güncelleştirmediyseniz uyarıları komutu verdiğinde `.nuspec` varsayılan değerlerine dosyasından.</span><span class="sxs-lookup"><span data-stu-id="8f864-137">The command issues warnings if you haven't updated various fields in the `.nuspec` file from their default values.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="8f864-138">Paket yayımlama</span><span class="sxs-lookup"><span data-stu-id="8f864-138">Publish the package</span></span>

<span data-ttu-id="8f864-139">Bulduktan sonra bir `.nupkg` dosyası, yayımlama, nuget.org kullanmaya `push` komutu.</span><span class="sxs-lookup"><span data-stu-id="8f864-139">Once you have a `.nupkg` file, you publish it to nuget.org using the `push` command.</span></span> <span data-ttu-id="8f864-140">(Alternatif olarak, kullanabileceğiniz [nuget.org yayımlama iş akışı](../create-packages/publish-a-package.md#publish-to-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="8f864-140">(Alternately, you can use the [nuget.org publishing workflow](../create-packages/publish-a-package.md#publish-to-nugetorg).</span></span>

> [!Warning]
> <span data-ttu-id="8f864-141">Nuget.org için yayımlama paketleri diğer geliştiricilerine herkese görünür.</span><span class="sxs-lookup"><span data-stu-id="8f864-141">The packages you publish to nuget.org are publicly visible to other developers.</span></span> <span data-ttu-id="8f864-142">Paketleri özel olarak barındırmak için bkz: [paketleri barındırma](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="8f864-142">To host packages privately, see [Hosting packages](../hosting-packages/overview.md).</span></span>


1. <span data-ttu-id="8f864-143">Ücretsiz bir hesap oluşturmak [nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), veya zaten varsa oturum açın.</span><span class="sxs-lookup"><span data-stu-id="8f864-143">Create a free account on [nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), or log in if you already have one.</span></span> <span data-ttu-id="8f864-144">Yeni bir hesap oluşturmadan bir onay e-posta gönderir.</span><span class="sxs-lookup"><span data-stu-id="8f864-144">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="8f864-145">Bir paket karşıya yüklemeden önce hesap onaylamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8f864-145">You must confirm the account before you can upload a package.</span></span>

1. <span data-ttu-id="8f864-146">Oturum açtıktan sonra kullanıcı adınızın (sağ üstte) seçin ve ardından **API anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="8f864-146">Once logged in, select your user name (on the upper right), then select **API Keys**.</span></span>

1. <span data-ttu-id="8f864-147">Seçin **oluşturma**, anahtarınız için bir ad, seçin **kapsamları seçin > anında**altında **API anahtarı**, girin * için **Glob düzeni**, ardından seçin **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="8f864-147">Select **Create**, provide a name for your key, select **Select Scopes > Push**Under **API Key**, enter * for **Glob pattern**, then select **Create**.</span></span>

1. <span data-ttu-id="8f864-148">Anahtar oluşturulduktan sonra Seç **kopyalama** erişim almak için anahtar CLI sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="8f864-148">Once the key is created, select **Copy** to retrieve the access key you'll need in the CLI:</span></span>

    ![API anahtarını Panoya kopyalama](media/QS_Create-02-APIKey.png)

    > [!Warning]
    > <span data-ttu-id="8f864-150">Anahtarınızı güvenli bir konuma kaydedin ve gizli kalmasını olmadığından.</span><span class="sxs-lookup"><span data-stu-id="8f864-150">Save your key in a secure location and keep is a secret.</span></span> <span data-ttu-id="8f864-151">Anahtarınızı yanlışlıkla açığa varsa, her zaman, dilediğiniz zaman yeniden oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8f864-151">If your key is accidentally revealed, you can always regenerate it at any time.</span></span> <span data-ttu-id="8f864-152">Artık paketleri CLI itmek istiyorsanız, API anahtarını da kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8f864-152">You can also remove the API key if you no longer want to push packages via the CLI.</span></span>

1. <span data-ttu-id="8f864-153">Aşağıdaki komutu çalıştırın istemine, paket adı belirtme ve anahtar değeri ile değiştirerek 4. adımda kopyalanan:</span><span class="sxs-lookup"><span data-stu-id="8f864-153">At a command prompt, run the following command, specifying your package name and replacing the key with the value copied in step 4:</span></span>

    ```
    nuget push AppLogger.1.0.0.0.nupkg 47be3377-c434-4c29-8576-af7f6993a54b -Source https://api.nuget.org/v3/index.json
    ```
    
1. <span data-ttu-id="8f864-154">nuget.exe yayımlama işleminin sonuçlarını görüntüler:</span><span class="sxs-lookup"><span data-stu-id="8f864-154">nuget.exe displays the results of the publishing process:</span></span>

    ```
    Pushing AppLogger.1.0.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed. 
    ```

1. <span data-ttu-id="8f864-155">Profilinizdeki nuget.org üzerinde seçin **paketlerini Yönet** bir görmek için yalnızca yayımlanmış.</span><span class="sxs-lookup"><span data-stu-id="8f864-155">From your profile on nuget.org, Select **Manage Packages** to see the one you just published.</span></span> <span data-ttu-id="8f864-156">Aynı zamanda bir onay e-posta alırsınız.</span><span class="sxs-lookup"><span data-stu-id="8f864-156">You also receive a confirmation email.</span></span> <span data-ttu-id="8f864-157">Biraz sıralanması ve diğerleri bulabileceğiniz arama sonuçlarında görüntülenmesi paketinize sürebileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8f864-157">Note that it might take a while for your package to be indexed and appear in search results where others can find it.</span></span> <span data-ttu-id="8f864-158">Bu işlem sırasında paket sayfanızı aşağıdaki iletiyi gösterir:</span><span class="sxs-lookup"><span data-stu-id="8f864-158">During that time your package page shows the message below:</span></span>

    ![Bu paket henüz dizin değil.](media/QS_Create-03-NotIndexed.png)

> [!Note]
> <span data-ttu-id="8f864-161">**Virüs tarama**: tüm paketler için nuget.org karşıya virüs taraması ve herhangi bir virüs bulunursa reddetti.</span><span class="sxs-lookup"><span data-stu-id="8f864-161">**Virus scanning**: All packages uploaded to nuget.org are scanned for viruses and rejected if any viruses are found.</span></span> <span data-ttu-id="8f864-162">Nuget.org üzerinde listelenen tüm paketler de düzenli aralıklarla taranır.</span><span class="sxs-lookup"><span data-stu-id="8f864-162">All packages listed on nuget.org are also scanned periodically.</span></span>

<span data-ttu-id="8f864-163">Ve bu kadar!</span><span class="sxs-lookup"><span data-stu-id="8f864-163">And that's it!</span></span> <span data-ttu-id="8f864-164">Yalnızca ilk NuGet paketinizi yayımladıktan [nuget.org](https://www.nuget.org/), diğer geliştiricilerin kendi projelerinde kullanabileceğiniz.</span><span class="sxs-lookup"><span data-stu-id="8f864-164">You've just published your first NuGet package to [nuget.org](https://www.nuget.org/), that other developers can use in their own projects.</span></span>

## <a name="related-topics"></a><span data-ttu-id="8f864-165">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="8f864-165">Related topics</span></span>

- [<span data-ttu-id="8f864-166">Bir paket oluşturun</span><span class="sxs-lookup"><span data-stu-id="8f864-166">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="8f864-167">Bir paket yayımlama</span><span class="sxs-lookup"><span data-stu-id="8f864-167">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="8f864-168">Birden çok hedef çerçeveyi desteği</span><span class="sxs-lookup"><span data-stu-id="8f864-168">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="8f864-169">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="8f864-169">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="8f864-170">Yerelleştirilmiş paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="8f864-170">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
