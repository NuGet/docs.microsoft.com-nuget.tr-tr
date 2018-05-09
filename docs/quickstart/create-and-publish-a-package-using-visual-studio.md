---
title: Oluşturma ve bir .NET standart Visual Studio kullanarak yayımlama NuGet paketi tanıtım Kılavuzu
description: Oluşturma ve yayımlama Visual Studio 2017 kullanarak bir .NET standart NuGet paketi bir gözden geçirme Öğreticisi.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/18/2018
ms.topic: quickstart
ms.openlocfilehash: c5d58aa6312eae801607ca44a81bc092a7a7c15f
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/28/2018
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard"></a><span data-ttu-id="fdd60-103">Hızlı Başlangıç: Oluşturma ve Visual Studio (.NET standart) kullanarak bir NuGet Paketi Yayımlama</span><span class="sxs-lookup"><span data-stu-id="fdd60-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard)</span></span>

<span data-ttu-id="fdd60-104">Bir .NET standart sınıf kitaplığı Visual Studio'da NuGet paketi oluşturun ve ardından CLI aracını kullanarak nuget.org yayımlamak için basit bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="fdd60-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio, and then publish it to nuget.org using a CLI tool.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fdd60-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="fdd60-105">Prerequisites</span></span>

1. <span data-ttu-id="fdd60-106">Visual Studio 2017 ' herhangi bir sürümünü yüklemek [visualstudio.com](https://www.visualstudio.com/) herhangi biriyle. NET ilgili iş yükü.</span><span class="sxs-lookup"><span data-stu-id="fdd60-106">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="fdd60-107">.NET iş yükü yüklendikten sonra visual Studio 2017 otomatik olarak NuGet yetenekleri içerir.</span><span class="sxs-lookup"><span data-stu-id="fdd60-107">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="fdd60-108">Yükleme `nuget.exe` buradan yükleyerek CLI [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), kaydetme `.exe` dosya için uygun bir klasör ve bu klasörü PATH ortam değişkenine ekleme.</span><span class="sxs-lookup"><span data-stu-id="fdd60-108">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

    <span data-ttu-id="fdd60-109">Alternatif olarak, varsa [.NET Core SDK](https://www.microsoft.com/net/download/) yüklü, kullanabileceğiniz `dotnet` CLI.</span><span class="sxs-lookup"><span data-stu-id="fdd60-109">Alternately, if you have the [.NET Core SDK](https://www.microsoft.com/net/download/) installed, you can use the `dotnet` CLI.</span></span>

1. <span data-ttu-id="fdd60-110">[Kayıt nuget.org ücretsiz bir hesap için](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) zaten yoksa.</span><span class="sxs-lookup"><span data-stu-id="fdd60-110">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="fdd60-111">Yeni bir hesap oluşturmadan bir onay e-posta gönderir.</span><span class="sxs-lookup"><span data-stu-id="fdd60-111">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="fdd60-112">Bir paket karşıya yüklemeden önce hesap onaylamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fdd60-112">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="fdd60-113">Sınıf kitaplığı proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="fdd60-113">Create a class library project</span></span>

<span data-ttu-id="fdd60-114">Varolan bir .NET standart sınıf kitaplığı proje paketini veya basit bir şekilde oluşturmak için istediğiniz kodu kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fdd60-114">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="fdd60-115">Visual Studio'da, **Dosya > Yeni > Proje**, genişletin **Visual C# > .NET standart** düğümü, "Sınıf kitaplığı (.NET standart)" şablonunu seçin, AppLogger proje adı ve **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="fdd60-115">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="fdd60-116">Sonuçta elde edilen proje dosyasını sağ tıklatın ve seçin **yapı** projeyi düzgün bir şekilde oluşturuldu emin olmak için.</span><span class="sxs-lookup"><span data-stu-id="fdd60-116">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="fdd60-117">DLL Debug klasörüne (veya bunun yerine bu yapılandırma yapı sürüm) içinde bulunur.</span><span class="sxs-lookup"><span data-stu-id="fdd60-117">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="fdd60-118">Gerçek bir NuGet paketi içinde doğal olarak, çok sayıda kullanışlı özellikle ile diğer uygulamaları derleme uygulayın.</span><span class="sxs-lookup"><span data-stu-id="fdd60-118">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="fdd60-119">Bir sınıf kitaplığı şablondan bir paket oluşturmak yeterli olduğundan bu kılavuzda ancak, herhangi bir ek kod yazma olmaz.</span><span class="sxs-lookup"><span data-stu-id="fdd60-119">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="fdd60-120">Yine de, bazı işlevsel kod paketi için isterseniz, aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="fdd60-120">Still, if you'd like some functional code for the package, use the following:</span></span>

```cs
namespace AppLogger
{
    public class Logger
    {
        public void Log(string text)
        {
            Console.WriteLine(text);
        }
    }
}
```

> [!Tip]
> <span data-ttu-id="fdd60-121">Aksi takdirde seçmek için bir nedeniniz yoksa projeleri tüketen geniş kapsamlı bir uyum sağlar gibi .NET standart tercih edilen NuGet paketlerini hedefidir.</span><span class="sxs-lookup"><span data-stu-id="fdd60-121">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="fdd60-122">Paket özelliklerini yapılandır</span><span class="sxs-lookup"><span data-stu-id="fdd60-122">Configure package properties</span></span>

1. <span data-ttu-id="fdd60-123">Seçin **Proje > Özellikler** menü komutunu ve ardından **paket** sekmesi. ( **Paket** sekmesi yalnızca .NET standart Sınıf Kitaplığı projelerinde; .NET Framework hedefliyorsanız, görüntülenir [oluşturma ve .NET Framework Paketi Yayımlama](create-and-publish-a-package-using-visual-studio-net-framework.md) yerine.</span><span class="sxs-lookup"><span data-stu-id="fdd60-123">Select the **Project > Properties** menu command, then select the **Package** tab. (The **Package** tab appears only for .NET Standard class library projects; if you are targeting .NET Framework, see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead.</span></span> <span data-ttu-id="fdd60-124">.NET standart bir proje için görünmüyorsa, Visual Studio 2017 en son sürümüne güncelleştirmeniz gerekebilir.)</span><span class="sxs-lookup"><span data-stu-id="fdd60-124">If it doesn't appear for a .NET Standard project, you may need to update Visual Studio 2017 to the latest release.)</span></span>

    ![NuGet paket özelliklerinde bir Visual Studio projesi](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="fdd60-126">Ortak tüketim için oluşturulan paketler için özellikle dikkat edin **etiketleri** özelliği gibi etiketler başkalarının paketinizi bulun ve neler yaptığını anlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="fdd60-126">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="fdd60-127">Benzersiz bir tanımlayıcı paketinizi verin ve istenen diğer özelliklerini doldurun.</span><span class="sxs-lookup"><span data-stu-id="fdd60-127">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="fdd60-128">Farklı özellikleri açıklaması için bkz: [.nuspec dosyası başvurusu](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="fdd60-128">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="fdd60-129">Tüm özellikleri burada yerleştirilmesini `.nuspec` projesi için Visual Studio oluşturur bildirimi.</span><span class="sxs-lookup"><span data-stu-id="fdd60-129">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="fdd60-130">Nuget.org veya ne olursa olsun, ana bilgisayar genelinde benzersiz bir tanımlayıcı kullanmakta olduğunuz paket vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fdd60-130">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="fdd60-131">Bu kılavuz için (Bu herkes gerçekte kullanacağı olsa da) sonraki yayımlama adım paketi herkese görünür hale "Sample" veya "Test" adı dahil olmak üzere öneririz.</span><span class="sxs-lookup"><span data-stu-id="fdd60-131">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="fdd60-132">Zaten bir ada sahip bir paketi yayımlamaya çalışırsanız, bir hata görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="fdd60-132">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="fdd60-133">İsteğe bağlı: Proje dosyası özelliklerinde doğrudan görmek için Çözüm Gezgini'nde projeye sağ tıklayın ve seçin **Düzenle AppLogger.csproj**.</span><span class="sxs-lookup"><span data-stu-id="fdd60-133">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="fdd60-134">Paketi komutunu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="fdd60-134">Run the pack command</span></span>

1. <span data-ttu-id="fdd60-135">Yapılandırma kümesi **sürüm**.</span><span class="sxs-lookup"><span data-stu-id="fdd60-135">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="fdd60-136">Projeye sağ tıklayın **Çözüm Gezgini** seçip **paketi** komutu:</span><span class="sxs-lookup"><span data-stu-id="fdd60-136">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Visual Studio Proje bağlam menüsünde NuGet Paketi komutu](media/qs_create-vs-02-pack-command.png)

1. <span data-ttu-id="fdd60-138">Visual Studio projesi oluşturur ve oluşturur `.nupkg` dosya.</span><span class="sxs-lookup"><span data-stu-id="fdd60-138">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="fdd60-139">İncelemek **çıkış** ayrıntıları (aşağıdakine benzer), paket dosyası yolu içeren penceresi.</span><span class="sxs-lookup"><span data-stu-id="fdd60-139">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="fdd60-140">Ayrıca, yerleşik bütünleştirilmiş olduğunu unutmayın `bin\Release\netstandard2.0` olarak neden önemli olduğuna .NET standart 2.0 hedef.</span><span class="sxs-lookup"><span data-stu-id="fdd60-140">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a><span data-ttu-id="fdd60-141">Diğer seçenek: MSBuild paketiyle</span><span class="sxs-lookup"><span data-stu-id="fdd60-141">Alternate option: pack with MSBuild</span></span>

<span data-ttu-id="fdd60-142">Kullanmaya alternatif olarak **paketi** menü komutu, NuGet 4.x+ ve MSBuild 15.1 + destekleyen bir `pack` hedef proje gerekli paketi veri içerdiğinde.</span><span class="sxs-lookup"><span data-stu-id="fdd60-142">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="fdd60-143">Bir komut istemi açın, proje klasörüne gidin ve aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="fdd60-143">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="fdd60-144">(MSBuild için tüm gerekli yollarının yapılandırılacak gibi genellikle "Geliştirici komut istemi için Visual Studio" Başlat menüsünden başlatmak istediğiniz.)</span><span class="sxs-lookup"><span data-stu-id="fdd60-144">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

```cli
msbuild /t:pack /p:Configuration=Release
```

<span data-ttu-id="fdd60-145">Paket sonra bulunabilir `bin\Release` klasör.</span><span class="sxs-lookup"><span data-stu-id="fdd60-145">The package can then be found in the `bin\Release` folder.</span></span>

<span data-ttu-id="fdd60-146">Ek seçeneklerle için `msbuild /t:pack`, bkz: [NuGet paketi ve geri yükleme MSBuild hedefleri olarak](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="fdd60-146">For additional options with `msbuild /t:pack`, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="fdd60-147">Paket yayımlama</span><span class="sxs-lookup"><span data-stu-id="fdd60-147">Publish the package</span></span>

<span data-ttu-id="fdd60-148">Bulduktan sonra bir `.nupkg` dosyası, yayımlama, kullanarak nuget.org `nuget.exe` CLI veya `dotnet.exe` CLI nuget.org alınan bir API anahtarı ile birlikte.</span><span class="sxs-lookup"><span data-stu-id="fdd60-148">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="fdd60-149">API anahtarınızı edinin</span><span class="sxs-lookup"><span data-stu-id="fdd60-149">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="fdd60-150">Nuget itme ile yayımlama</span><span class="sxs-lookup"><span data-stu-id="fdd60-150">Publish with nuget push</span></span>

<span data-ttu-id="fdd60-151">Bu adım bir alternatifidir `dotnet.exe`.</span><span class="sxs-lookup"><span data-stu-id="fdd60-151">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="fdd60-152">Değiştirmek için içeren klasör `.nupkg` dosya.</span><span class="sxs-lookup"><span data-stu-id="fdd60-152">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="fdd60-153">Paket adı belirtme ve API anahtarınızı anahtar değerini değiştirerek aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="fdd60-153">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="fdd60-154">nuget.exe yayımlama işleminin sonuçlarını görüntüler:</span><span class="sxs-lookup"><span data-stu-id="fdd60-154">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="fdd60-155">Bkz: [nuget itme](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="fdd60-155">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="fdd60-156">DotNet nuget itme ile yayımlama</span><span class="sxs-lookup"><span data-stu-id="fdd60-156">Publish with dotnet nuget push</span></span>

<span data-ttu-id="fdd60-157">Bu adım bir alternatifidir `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="fdd60-157">This step is an alternative to using `nuget.exe`.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="fdd60-158">Hataları yayımlama</span><span class="sxs-lookup"><span data-stu-id="fdd60-158">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="fdd60-159">Yayımlanan paket yönetme</span><span class="sxs-lookup"><span data-stu-id="fdd60-159">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="fdd60-160">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="fdd60-160">Related topics</span></span>

- [<span data-ttu-id="fdd60-161">Bir paket oluşturun</span><span class="sxs-lookup"><span data-stu-id="fdd60-161">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="fdd60-162">Paket Yayımlama</span><span class="sxs-lookup"><span data-stu-id="fdd60-162">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="fdd60-163">Ön yayın paketleri</span><span class="sxs-lookup"><span data-stu-id="fdd60-163">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="fdd60-164">Birden çok hedef çerçeveyi desteği</span><span class="sxs-lookup"><span data-stu-id="fdd60-164">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="fdd60-165">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="fdd60-165">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="fdd60-166">Yerelleştirilmiş paketler oluşturma</span><span class="sxs-lookup"><span data-stu-id="fdd60-166">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="fdd60-167">.NET standart kitaplığı belgeleri</span><span class="sxs-lookup"><span data-stu-id="fdd60-167">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="fdd60-168">.NET Core için .NET Framework'bağlantı noktası oluşturma</span><span class="sxs-lookup"><span data-stu-id="fdd60-168">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
