---
title: "Oluşturma ve yayımlama Visual Studio kullanarak bir NuGet paketi tanıtım Kılavuzu | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/02/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Oluşturma ve yayımlama Visual Studio 2017 kullanarak bir NuGet paketi bir gözden geçirme Öğreticisi."
keywords: "NuGet paketini oluşturma, NuGet paketi yayımlama, NuGet öğretici, Visual Studio NuGet paketi, msbuild paketi oluşturma"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a4d60fdc0f27f9c4080266e212ac1cfe470ba925
ms.sourcegitcommit: eabd401616a98dda2ae6293612acb3b81b584967
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/09/2018
---
# <a name="create-and-publish-a-package-using-visual-studio"></a><span data-ttu-id="3956b-104">Oluşturma ve Visual Studio kullanarak bir paket yayımlama</span><span class="sxs-lookup"><span data-stu-id="3956b-104">Create and publish a package using Visual Studio</span></span>

<span data-ttu-id="3956b-105">Visual Studio'da .NET sınıf kitaplığı NuGet paketi oluşturun ve ardından CLI aracını kullanarak nuget.org yayımlamak için basit bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="3956b-105">It's a simple process to create a NuGet package from a .NET Class Library in Visual Studio, and then publish it to nuget.org using a CLI tool.</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="3956b-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3956b-106">Pre-requisites</span></span>

1. <span data-ttu-id="3956b-107">Visual Studio 2017 ' herhangi bir sürümünü yüklemek [visualstudio.com](https://www.visualstudio.com/) herhangi biriyle. NET ilgili iş yükü.</span><span class="sxs-lookup"><span data-stu-id="3956b-107">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="3956b-108">.NET iş yükü yüklendikten sonra visual Studio 2017 otomatik olarak NuGet yetenekleri içerir.</span><span class="sxs-lookup"><span data-stu-id="3956b-108">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="3956b-109">Yükleme `nuget.exe` buradan yükleyerek CLI [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), kaydetme `.exe` dosya için uygun bir klasör ve bu klasörü PATH ortam değişkenine ekleme.</span><span class="sxs-lookup"><span data-stu-id="3956b-109">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

    <span data-ttu-id="3956b-110">Alternatif olarak, varsa [.NET Core SDK](https://www.microsoft.com/net/download/) yüklü, kullanabileceğiniz `dotnet` CLI.</span><span class="sxs-lookup"><span data-stu-id="3956b-110">Alternately, if you have the [.NET Core SDK](https://www.microsoft.com/net/download/) installed, you can use the `dotnet` CLI.</span></span>

1. <span data-ttu-id="3956b-111">[Kayıt nuget.org ücretsiz bir hesap için](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) zaten yoksa.</span><span class="sxs-lookup"><span data-stu-id="3956b-111">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="3956b-112">Yeni bir hesap oluşturmadan bir onay e-posta gönderir.</span><span class="sxs-lookup"><span data-stu-id="3956b-112">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="3956b-113">Bir paket karşıya yüklemeden önce hesap onaylamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3956b-113">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="3956b-114">Sınıf kitaplığı proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="3956b-114">Create a class library project</span></span>

<span data-ttu-id="3956b-115">Varolan bir .NET sınıf kitaplığı proje paketini veya basit bir şekilde oluşturmak için istediğiniz kodu kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3956b-115">You can use an existing .NET Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="3956b-116">Visual Studio'da, **Dosya > Yeni > Proje**, genişletin **Visual C# > .NET standart** düğümü, "Sınıf kitaplığı (.NET standart)" şablonunu seçin, AppLogger proje adı ve **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="3956b-116">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="3956b-117">Sonuçta elde edilen proje dosyasını sağ tıklatın ve seçin **yapı** projeyi düzgün bir şekilde oluşturuldu emin olmak için.</span><span class="sxs-lookup"><span data-stu-id="3956b-117">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="3956b-118">DLL Debug klasörüne (veya bunun yerine bu yapılandırma yapı sürüm) içinde bulunur.</span><span class="sxs-lookup"><span data-stu-id="3956b-118">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="3956b-119">Gerçek bir NuGet paketi içinde doğal olarak, çok sayıda kullanışlı özellikle ile diğer uygulamaları derleme uygulayın.</span><span class="sxs-lookup"><span data-stu-id="3956b-119">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="3956b-120">Bir sınıf kitaplığı şablondan bir paket oluşturmak yeterli olduğundan bu kılavuzda ancak, herhangi bir ek kod yazma olmaz.</span><span class="sxs-lookup"><span data-stu-id="3956b-120">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="3956b-121">Yine de, bazı işlevsel kod paketi için isterseniz, aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="3956b-121">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="3956b-122">Aksi takdirde seçmek için bir nedeniniz yoksa projeleri tüketen geniş kapsamlı bir uyum sağlar gibi .NET standart tercih edilen NuGet paketlerini hedefidir.</span><span class="sxs-lookup"><span data-stu-id="3956b-122">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="3956b-123">Paket özelliklerini yapılandır</span><span class="sxs-lookup"><span data-stu-id="3956b-123">Configure package properties</span></span>

1. <span data-ttu-id="3956b-124">Seçin **Proje > Özellikler** menü komutunu ve ardından **paket** sekmesi:</span><span class="sxs-lookup"><span data-stu-id="3956b-124">Select the **Project > Properties** menu command, then select the **Package** tab:</span></span>

    ![NuGet paket özelliklerinde bir Visual Studio projesi](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="3956b-126">Ortak tüketim için oluşturulan paketler için özellikle dikkat edin **etiketleri** özelliği gibi etiketler başkalarının paketinizi bulun ve neler yaptığını anlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="3956b-126">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="3956b-127">Benzersiz bir tanımlayıcı paketinizi verin ve istenen diğer özelliklerini doldurun.</span><span class="sxs-lookup"><span data-stu-id="3956b-127">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="3956b-128">Farklı özellikleri açıklaması için bkz: [.nuspec dosyası başvurusu](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="3956b-128">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="3956b-129">Tüm özellikleri burada yerleştirilmesini `.nuspec` projesi için Visual Studio oluşturur bildirimi.</span><span class="sxs-lookup"><span data-stu-id="3956b-129">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="3956b-130">Nuget.org veya ne olursa olsun, ana bilgisayar genelinde benzersiz bir tanımlayıcı kullanmakta olduğunuz paket vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3956b-130">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="3956b-131">Bu kılavuz için (Bu herkes gerçekte kullanacağı olsa da) sonraki yayımlama adım paketi herkese görünür hale "Sample" veya "Test" adı dahil olmak üzere öneririz.</span><span class="sxs-lookup"><span data-stu-id="3956b-131">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="3956b-132">Zaten bir ada sahip bir paketi yayımlamaya çalışırsanız, bir hata görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="3956b-132">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="3956b-133">İsteğe bağlı: Proje dosyası özelliklerinde doğrudan görmek için Çözüm Gezgini'nde projeye sağ tıklayın ve seçin **Düzenle AppLogger.csproj**.</span><span class="sxs-lookup"><span data-stu-id="3956b-133">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="3956b-134">Paketi komutunu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="3956b-134">Run the pack command</span></span>

1. <span data-ttu-id="3956b-135">Yapılandırma kümesi **sürüm**.</span><span class="sxs-lookup"><span data-stu-id="3956b-135">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="3956b-136">Projeye sağ tıklayın **Çözüm Gezgini** seçip **paketi** komutu:</span><span class="sxs-lookup"><span data-stu-id="3956b-136">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Visual Studio Proje bağlam menüsünde NuGet Paketi komutu](media/qs_create-vs-02-pack-command.png)

1. <span data-ttu-id="3956b-138">Visual Studio projesi oluşturur ve oluşturur `.nupkg` dosya.</span><span class="sxs-lookup"><span data-stu-id="3956b-138">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="3956b-139">İncelemek **çıkış** ayrıntıları (aşağıdakine benzer), paket dosyası yolu içeren penceresi.</span><span class="sxs-lookup"><span data-stu-id="3956b-139">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="3956b-140">Ayrıca, yerleşik bütünleştirilmiş olduğunu unutmayın `bin\Release\netstandard2.0` olarak neden önemli olduğuna .NET standart 2.0 hedef.</span><span class="sxs-lookup"><span data-stu-id="3956b-140">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a><span data-ttu-id="3956b-141">Diğer seçenek: MSBuild paketiyle</span><span class="sxs-lookup"><span data-stu-id="3956b-141">Alternate option: pack with MSBuild</span></span>

<span data-ttu-id="3956b-142">Kullanmaya alternatif olarak **paketi** menü komutu, NuGet 4.x+ ve MSBuild 15.1 + destekleyen bir `pack` hedef proje gerekli paketi veriler içeriyorsa:</span><span class="sxs-lookup"><span data-stu-id="3956b-142">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data:</span></span>

```cli
msbuild /t:pack /p:Configuration=Release
```

<span data-ttu-id="3956b-143">Paket sonra bulunabilir `bin\Release` klasör.</span><span class="sxs-lookup"><span data-stu-id="3956b-143">The package can then be found in the `bin\Release` folder.</span></span>

<span data-ttu-id="3956b-144">Ek seçeneklerle için `msbuild /t:pack`, bkz: [NuGet paketi ve geri yükleme MSBuild hedefleri olarak](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="3956b-144">For additional options with `msbuild /t:pack`, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="3956b-145">Paket yayımlama</span><span class="sxs-lookup"><span data-stu-id="3956b-145">Publish the package</span></span>

<span data-ttu-id="3956b-146">Bulduktan sonra bir `.nupkg` dosyası, yayımlama, kullanarak nuget.org `nuget.exe` CLI veya `dotnet.exe` CLI nuget.org alınan bir API anahtarı ile birlikte.</span><span class="sxs-lookup"><span data-stu-id="3956b-146">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE[publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="3956b-147">API anahtarınızı edinin</span><span class="sxs-lookup"><span data-stu-id="3956b-147">Acquire your API key</span></span>

[!INCLUDE[publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="3956b-148">Nuget itme ile yayımlama</span><span class="sxs-lookup"><span data-stu-id="3956b-148">Publish with nuget push</span></span>

<span data-ttu-id="3956b-149">Bu adım bir alternatifidir `dotnet.exe`.</span><span class="sxs-lookup"><span data-stu-id="3956b-149">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="3956b-150">Değiştirmek için içeren klasör `.nupkg` dosya...</span><span class="sxs-lookup"><span data-stu-id="3956b-150">Change to the folder containing the `.nupkg` file..</span></span>

1. <span data-ttu-id="3956b-151">Paket adı belirtme ve API anahtarınızı anahtar değerini değiştirerek aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="3956b-151">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="3956b-152">nuget.exe yayımlama işleminin sonuçlarını görüntüler:</span><span class="sxs-lookup"><span data-stu-id="3956b-152">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="3956b-153">Bkz: [nuget itme](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="3956b-153">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="3956b-154">DotNet nuget itme ile yayımlama</span><span class="sxs-lookup"><span data-stu-id="3956b-154">Publish with dotnet nuget push</span></span>

<span data-ttu-id="3956b-155">Bu adım bir alternatifidir `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="3956b-155">This step is an alternative to using `nuget.exe`.</span></span>

[!INCLUDE[publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="3956b-156">Hataları yayımlama</span><span class="sxs-lookup"><span data-stu-id="3956b-156">Publish errors</span></span>

[!INCLUDE[publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="3956b-157">Yayımlanan paket yönetme</span><span class="sxs-lookup"><span data-stu-id="3956b-157">Manage the published package</span></span>

[!INCLUDE[publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="3956b-158">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="3956b-158">Related topics</span></span>

- [<span data-ttu-id="3956b-159">Bir paket oluşturun</span><span class="sxs-lookup"><span data-stu-id="3956b-159">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="3956b-160">Paket Yayımlama</span><span class="sxs-lookup"><span data-stu-id="3956b-160">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="3956b-161">Birden çok hedef çerçeveyi desteği</span><span class="sxs-lookup"><span data-stu-id="3956b-161">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="3956b-162">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="3956b-162">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="3956b-163">Yerelleştirilmiş paketler oluşturma</span><span class="sxs-lookup"><span data-stu-id="3956b-163">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="3956b-164">.NET standart kitaplığı belgeleri</span><span class="sxs-lookup"><span data-stu-id="3956b-164">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="3956b-165">.NET Core için .NET Framework'bağlantı noktası oluşturma</span><span class="sxs-lookup"><span data-stu-id="3956b-165">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)