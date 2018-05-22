---
title: Oluşturma ve Windows Visual Studio kullanarak .NET standart paket yayımlama
description: Oluşturma ve yayımlama Windows Visual Studio 2017 kullanarak bir .NET standart NuGet paketi bir gözden geçirme Öğreticisi.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 05/18/2018
ms.topic: quickstart
ms.openlocfilehash: f4e6473d307f2f71016f6926abbcdb1295abc7b5
ms.sourcegitcommit: f0b31af805183cf3a98eabb504e16d9b05223cfe
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/22/2018
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a><span data-ttu-id="f39f6-103">Hızlı Başlangıç: Oluşturma ve Visual Studio (.NET standart, yalnızca Windows) kullanarak bir NuGet Paketi Yayımlama</span><span class="sxs-lookup"><span data-stu-id="f39f6-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard, Windows only)</span></span>

<span data-ttu-id="f39f6-104">Bir .NET standart sınıf kitaplığı Windows Visual Studio'da NuGet paketi oluşturun ve ardından CLI aracını kullanarak nuget.org yayımlamak için basit bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="f39f6-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio on Windows, and then publish it to nuget.org using a CLI tool.</span></span>

> [!Note]
> <span data-ttu-id="f39f6-105">Bu Hızlı Başlangıç, Visual Studio 2017 yalnızca Windows için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="f39f6-105">This Quickstart applies to Visual Studio 2017 for Windows only.</span></span> <span data-ttu-id="f39f6-106">Mac için Visual Studio burada açıklanan özellikleri içermez.</span><span class="sxs-lookup"><span data-stu-id="f39f6-106">Visual Studio for Mac does not include the capabilities described here.</span></span> <span data-ttu-id="f39f6-107">Kullanım [dotnet CLI araçlarını](create-and-publish-a-package-using-the-dotnet-cli.md) yerine.</span><span class="sxs-lookup"><span data-stu-id="f39f6-107">Use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md) instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f39f6-108">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="f39f6-108">Prerequisites</span></span>

1. <span data-ttu-id="f39f6-109">Visual Studio 2017 ' herhangi bir sürümünü yüklemek [visualstudio.com](https://www.visualstudio.com/) herhangi biriyle. NET ilgili iş yükü.</span><span class="sxs-lookup"><span data-stu-id="f39f6-109">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="f39f6-110">.NET iş yükü yüklendikten sonra visual Studio 2017 otomatik olarak NuGet yetenekleri içerir.</span><span class="sxs-lookup"><span data-stu-id="f39f6-110">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="f39f6-111">Yükleme `nuget.exe` buradan yükleyerek CLI [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), kaydetme `.exe` dosya için uygun bir klasör ve bu klasörü PATH ortam değişkenine ekleme.</span><span class="sxs-lookup"><span data-stu-id="f39f6-111">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

    <span data-ttu-id="f39f6-112">Alternatif olarak, varsa [.NET Core SDK](https://www.microsoft.com/net/download/) yüklü, kullanabileceğiniz `dotnet` CLI.</span><span class="sxs-lookup"><span data-stu-id="f39f6-112">Alternately, if you have the [.NET Core SDK](https://www.microsoft.com/net/download/) installed, you can use the `dotnet` CLI.</span></span>

1. <span data-ttu-id="f39f6-113">[Kayıt nuget.org ücretsiz bir hesap için](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) zaten yoksa.</span><span class="sxs-lookup"><span data-stu-id="f39f6-113">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="f39f6-114">Yeni bir hesap oluşturmadan bir onay e-posta gönderir.</span><span class="sxs-lookup"><span data-stu-id="f39f6-114">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="f39f6-115">Bir paket karşıya yüklemeden önce hesap onaylamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f39f6-115">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="f39f6-116">Sınıf kitaplığı proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="f39f6-116">Create a class library project</span></span>

<span data-ttu-id="f39f6-117">Varolan bir .NET standart sınıf kitaplığı proje paketini veya basit bir şekilde oluşturmak için istediğiniz kodu kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f39f6-117">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="f39f6-118">Visual Studio'da, **Dosya > Yeni > Proje**, genişletin **Visual C# > .NET standart** düğümü, "Sınıf kitaplığı (.NET standart)" şablonunu seçin, AppLogger proje adı ve **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="f39f6-118">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="f39f6-119">Sonuçta elde edilen proje dosyasını sağ tıklatın ve seçin **yapı** projeyi düzgün bir şekilde oluşturuldu emin olmak için.</span><span class="sxs-lookup"><span data-stu-id="f39f6-119">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="f39f6-120">DLL Debug klasörüne (veya bunun yerine bu yapılandırma yapı sürüm) içinde bulunur.</span><span class="sxs-lookup"><span data-stu-id="f39f6-120">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="f39f6-121">Gerçek bir NuGet paketi içinde doğal olarak, çok sayıda kullanışlı özellikle ile diğer uygulamaları derleme uygulayın.</span><span class="sxs-lookup"><span data-stu-id="f39f6-121">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="f39f6-122">Bir sınıf kitaplığı şablondan bir paket oluşturmak yeterli olduğundan bu kılavuzda ancak, herhangi bir ek kod yazma olmaz.</span><span class="sxs-lookup"><span data-stu-id="f39f6-122">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="f39f6-123">Yine de, bazı işlevsel kod paketi için isterseniz, aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="f39f6-123">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="f39f6-124">Aksi takdirde seçmek için bir nedeniniz yoksa projeleri tüketen geniş kapsamlı bir uyum sağlar gibi .NET standart tercih edilen NuGet paketlerini hedefidir.</span><span class="sxs-lookup"><span data-stu-id="f39f6-124">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="f39f6-125">Paket özelliklerini yapılandır</span><span class="sxs-lookup"><span data-stu-id="f39f6-125">Configure package properties</span></span>

1. <span data-ttu-id="f39f6-126">Seçin **Proje > Özellikler** menü komutunu ve ardından **paket** sekmesi. ( **Paket** sekmesi yalnızca .NET standart Sınıf Kitaplığı projelerinde; .NET Framework hedefliyorsanız, görüntülenir [oluşturma ve .NET Framework Paketi Yayımlama](create-and-publish-a-package-using-visual-studio-net-framework.md) yerine.</span><span class="sxs-lookup"><span data-stu-id="f39f6-126">Select the **Project > Properties** menu command, then select the **Package** tab. (The **Package** tab appears only for .NET Standard class library projects; if you are targeting .NET Framework, see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead.</span></span> <span data-ttu-id="f39f6-127">.NET standart bir proje için görünmüyorsa, Visual Studio 2017 en son sürümüne güncelleştirmeniz gerekebilir.)</span><span class="sxs-lookup"><span data-stu-id="f39f6-127">If it doesn't appear for a .NET Standard project, you may need to update Visual Studio 2017 to the latest release.)</span></span>

    ![NuGet paket özelliklerinde bir Visual Studio projesi](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="f39f6-129">Ortak tüketim için oluşturulan paketler için özellikle dikkat edin **etiketleri** özelliği gibi etiketler başkalarının paketinizi bulun ve neler yaptığını anlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="f39f6-129">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="f39f6-130">Benzersiz bir tanımlayıcı paketinizi verin ve istenen diğer özelliklerini doldurun.</span><span class="sxs-lookup"><span data-stu-id="f39f6-130">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="f39f6-131">Farklı özellikleri açıklaması için bkz: [.nuspec dosyası başvurusu](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="f39f6-131">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="f39f6-132">Tüm özellikleri burada yerleştirilmesini `.nuspec` projesi için Visual Studio oluşturur bildirimi.</span><span class="sxs-lookup"><span data-stu-id="f39f6-132">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="f39f6-133">Nuget.org veya ne olursa olsun, ana bilgisayar genelinde benzersiz bir tanımlayıcı kullanmakta olduğunuz paket vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f39f6-133">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="f39f6-134">Bu kılavuz için (Bu herkes gerçekte kullanacağı olsa da) sonraki yayımlama adım paketi herkese görünür hale "Sample" veya "Test" adı dahil olmak üzere öneririz.</span><span class="sxs-lookup"><span data-stu-id="f39f6-134">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="f39f6-135">Zaten bir ada sahip bir paketi yayımlamaya çalışırsanız, bir hata görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="f39f6-135">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="f39f6-136">İsteğe bağlı: Proje dosyası özelliklerinde doğrudan görmek için Çözüm Gezgini'nde projeye sağ tıklayın ve seçin **Düzenle AppLogger.csproj**.</span><span class="sxs-lookup"><span data-stu-id="f39f6-136">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="f39f6-137">Paketi komutunu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="f39f6-137">Run the pack command</span></span>

1. <span data-ttu-id="f39f6-138">Yapılandırma kümesi **sürüm**.</span><span class="sxs-lookup"><span data-stu-id="f39f6-138">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="f39f6-139">Projeye sağ tıklayın **Çözüm Gezgini** seçip **paketi** komutu:</span><span class="sxs-lookup"><span data-stu-id="f39f6-139">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Visual Studio Proje bağlam menüsünde NuGet Paketi komutu](media/qs_create-vs-02-pack-command.png)

1. <span data-ttu-id="f39f6-141">Visual Studio projesi oluşturur ve oluşturur `.nupkg` dosya.</span><span class="sxs-lookup"><span data-stu-id="f39f6-141">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="f39f6-142">İncelemek **çıkış** ayrıntıları (aşağıdakine benzer), paket dosyası yolu içeren penceresi.</span><span class="sxs-lookup"><span data-stu-id="f39f6-142">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="f39f6-143">Ayrıca, yerleşik bütünleştirilmiş olduğunu unutmayın `bin\Release\netstandard2.0` olarak neden önemli olduğuna .NET standart 2.0 hedef.</span><span class="sxs-lookup"><span data-stu-id="f39f6-143">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a><span data-ttu-id="f39f6-144">Diğer seçenek: MSBuild paketiyle</span><span class="sxs-lookup"><span data-stu-id="f39f6-144">Alternate option: pack with MSBuild</span></span>

<span data-ttu-id="f39f6-145">Kullanmaya alternatif olarak **paketi** menü komutu, NuGet 4.x+ ve MSBuild 15.1 + destekleyen bir `pack` hedef proje gerekli paketi veri içerdiğinde.</span><span class="sxs-lookup"><span data-stu-id="f39f6-145">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="f39f6-146">Bir komut istemi açın, proje klasörüne gidin ve aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f39f6-146">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="f39f6-147">(MSBuild için tüm gerekli yollarının yapılandırılacak gibi genellikle "Geliştirici komut istemi için Visual Studio" Başlat menüsünden başlatmak istediğiniz.)</span><span class="sxs-lookup"><span data-stu-id="f39f6-147">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

```cli
msbuild /t:pack /p:Configuration=Release
```

<span data-ttu-id="f39f6-148">Paket sonra bulunabilir `bin\Release` klasör.</span><span class="sxs-lookup"><span data-stu-id="f39f6-148">The package can then be found in the `bin\Release` folder.</span></span>

<span data-ttu-id="f39f6-149">Ek seçeneklerle için `msbuild /t:pack`, bkz: [NuGet paketi ve geri yükleme MSBuild hedefleri olarak](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="f39f6-149">For additional options with `msbuild /t:pack`, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="f39f6-150">Paket yayımlama</span><span class="sxs-lookup"><span data-stu-id="f39f6-150">Publish the package</span></span>

<span data-ttu-id="f39f6-151">Bulduktan sonra bir `.nupkg` dosyası, yayımlama, kullanarak nuget.org `nuget.exe` CLI veya `dotnet.exe` CLI nuget.org alınan bir API anahtarı ile birlikte.</span><span class="sxs-lookup"><span data-stu-id="f39f6-151">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="f39f6-152">API anahtarınızı edinin</span><span class="sxs-lookup"><span data-stu-id="f39f6-152">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="f39f6-153">Nuget itme ile yayımlama</span><span class="sxs-lookup"><span data-stu-id="f39f6-153">Publish with nuget push</span></span>

<span data-ttu-id="f39f6-154">Bu adım bir alternatifidir `dotnet.exe`.</span><span class="sxs-lookup"><span data-stu-id="f39f6-154">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="f39f6-155">Değiştirmek için içeren klasör `.nupkg` dosya.</span><span class="sxs-lookup"><span data-stu-id="f39f6-155">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="f39f6-156">Paket adı belirtme ve API anahtarınızı anahtar değerini değiştirerek aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f39f6-156">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="f39f6-157">nuget.exe yayımlama işleminin sonuçlarını görüntüler:</span><span class="sxs-lookup"><span data-stu-id="f39f6-157">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="f39f6-158">Bkz: [nuget itme](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="f39f6-158">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="f39f6-159">DotNet nuget itme ile yayımlama</span><span class="sxs-lookup"><span data-stu-id="f39f6-159">Publish with dotnet nuget push</span></span>

<span data-ttu-id="f39f6-160">Bu adım bir alternatifidir `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="f39f6-160">This step is an alternative to using `nuget.exe`.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="f39f6-161">Hataları yayımlama</span><span class="sxs-lookup"><span data-stu-id="f39f6-161">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="f39f6-162">Yayımlanan paket yönetme</span><span class="sxs-lookup"><span data-stu-id="f39f6-162">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="f39f6-163">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="f39f6-163">Related topics</span></span>

- [<span data-ttu-id="f39f6-164">Bir paket oluşturun</span><span class="sxs-lookup"><span data-stu-id="f39f6-164">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="f39f6-165">Paket Yayımlama</span><span class="sxs-lookup"><span data-stu-id="f39f6-165">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="f39f6-166">Ön yayın paketleri</span><span class="sxs-lookup"><span data-stu-id="f39f6-166">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="f39f6-167">Birden çok hedef çerçeveyi desteği</span><span class="sxs-lookup"><span data-stu-id="f39f6-167">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="f39f6-168">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="f39f6-168">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="f39f6-169">Yerelleştirilmiş paketler oluşturma</span><span class="sxs-lookup"><span data-stu-id="f39f6-169">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="f39f6-170">.NET standart kitaplığı belgeleri</span><span class="sxs-lookup"><span data-stu-id="f39f6-170">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="f39f6-171">.NET Core için .NET Framework'bağlantı noktası oluşturma</span><span class="sxs-lookup"><span data-stu-id="f39f6-171">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
