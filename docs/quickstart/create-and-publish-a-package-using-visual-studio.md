---
title: Windows üzerinde Visual Studio 'Yu kullanarak .NET Standard NuGet paketi oluşturma ve yayımlama
description: Windows üzerinde Visual Studio kullanarak .NET Standard NuGet paketi oluşturma ve yayımlama hakkında bir adım adım öğretici.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: quickstart
ms.openlocfilehash: 0fc3b15c6d5ffa93eb6e26660f71cea2286ba77d
ms.sourcegitcommit: aed04cc04b0902403612de6736a900d41c265afd
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2019
ms.locfileid: "68821429"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a><span data-ttu-id="9708e-103">Hızlı Başlangıç: Visual Studio (.NET Standard, yalnızca Windows) kullanarak bir NuGet paketi oluşturma ve yayımlama</span><span class="sxs-lookup"><span data-stu-id="9708e-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard, Windows only)</span></span>

<span data-ttu-id="9708e-104">Windows üzerinde Visual Studio 'da bir .NET Standard sınıf kitaplığından bir NuGet paketi oluşturmak ve ardından CLı aracını kullanarak nuget.org 'de yayımlamak basit bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="9708e-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio on Windows, and then publish it to nuget.org using a CLI tool.</span></span>

> [!Note]
> <span data-ttu-id="9708e-105">Mac için Visual Studio kullanıyorsanız, bir NuGet paketi oluşturma konusunda [Bu bilgilere](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) bakın veya [DotNet CLI araçlarını](create-and-publish-a-package-using-the-dotnet-cli.md)kullanın.</span><span class="sxs-lookup"><span data-stu-id="9708e-105">If you are using Visual Studio for Mac, refer to [this information](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) on creating a NuGet package, or use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9708e-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="9708e-106">Prerequisites</span></span>

1. <span data-ttu-id="9708e-107">.NET Core ile ilgili iş yüküyle [VisualStudio.com](https://www.visualstudio.com/) 'tan herhangi bir Visual Studio 2017 veya üzeri sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="9708e-107">Install any edition of Visual Studio 2017 or higher from [visualstudio.com](https://www.visualstudio.com/) with a .NET Core related workload.</span></span>

1. <span data-ttu-id="9708e-108">Zaten yüklü değilse, `dotnet` CLI 'yı yükleme.</span><span class="sxs-lookup"><span data-stu-id="9708e-108">If it's not already installed, install the `dotnet` CLI.</span></span>

   <span data-ttu-id="9708e-109">CLI için, Visual Studio 2017 ' den başlayarak `dotnet` , CLI, .NET Core ile ilgili tüm iş yükleri ile otomatik olarak yüklenir. `dotnet`</span><span class="sxs-lookup"><span data-stu-id="9708e-109">For the `dotnet` CLI, starting in Visual Studio 2017, the `dotnet` CLI is automatically installed with any .NET Core related workloads.</span></span> <span data-ttu-id="9708e-110">Aksi takdirde, `dotnet` CLI 'yı almak için [.NET Core SDK](https://www.microsoft.com/net/download/) ' yi yüklemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="9708e-110">Otherwise, install the [.NET Core SDK](https://www.microsoft.com/net/download/) to get the `dotnet` CLI.</span></span> <span data-ttu-id="9708e-111">CLI `dotnet` , [SDK stili biçimini](../resources/check-project-format.md) kullanan .NET Standard projeleri için gereklidir (SDK özniteliği).</span><span class="sxs-lookup"><span data-stu-id="9708e-111">The `dotnet` CLI is required for .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md) (SDK attribute).</span></span> <span data-ttu-id="9708e-112">Visual Studio 2017 ve üzeri sürümlerde, bu makalede kullanılan varsayılan sınıf kitaplığı şablonu SDK özniteliğini kullanır.</span><span class="sxs-lookup"><span data-stu-id="9708e-112">The default class library template in Visual Studio 2017 and higher, which is used in this article, uses the SDK attribute.</span></span>
   
   > [!Important]
   > <span data-ttu-id="9708e-113">Bu makalede, `dotnet` CLI önerilir.</span><span class="sxs-lookup"><span data-stu-id="9708e-113">For this article, the `dotnet` CLI is recommended.</span></span> <span data-ttu-id="9708e-114">`nuget.exe` CLI kullanarak herhangi bir NuGet paketini yayımlayabilseniz de, bu makaledeki adımların bazıları SDK stilindeki projelere ve DotNet CLI 'ya özeldir.</span><span class="sxs-lookup"><span data-stu-id="9708e-114">Although you can publish any NuGet package using the `nuget.exe` CLI, some of the steps in this article are specific to SDK-style projects and the dotnet CLI.</span></span> <span data-ttu-id="9708e-115">NuGet. exe CLı, [SDK olmayan-stil projeleri](../resources/check-project-format.md) için kullanılır (genellikle .NET Framework).</span><span class="sxs-lookup"><span data-stu-id="9708e-115">The nuget.exe CLI is used for [non-SDK-style projects](../resources/check-project-format.md) (typically .NET Framework).</span></span> <span data-ttu-id="9708e-116">SDK olmayan bir proje ile çalışıyorsanız, paketi oluşturmak ve yayımlamak için [.NET Framework paketi oluşturma ve yayımlama (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) konusundaki yordamları izleyin.</span><span class="sxs-lookup"><span data-stu-id="9708e-116">If you are working with a non-SDK-style project, follow the procedures in [Create and publish a .NET Framework package (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) to create and publish the package.</span></span>

1. <span data-ttu-id="9708e-117">Henüz bir [hesabınız yoksa NuGet.org üzerinde ücretsiz bir hesaba kaydolun](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account) .</span><span class="sxs-lookup"><span data-stu-id="9708e-117">[Register for a free account on nuget.org](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account) if you don't have one already.</span></span> <span data-ttu-id="9708e-118">Yeni hesap oluşturma onay e-postası gönderir.</span><span class="sxs-lookup"><span data-stu-id="9708e-118">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="9708e-119">Bir paketi karşıya yükleyebilmek için önce hesabı onaylamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9708e-119">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="9708e-120">Sınıf kitaplığı projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="9708e-120">Create a class library project</span></span>

<span data-ttu-id="9708e-121">Paketlemek istediğiniz kod için mevcut bir .NET Standard Sınıf Kitaplığı projesini kullanabilir veya basit bir tane oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9708e-121">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="9708e-122">Visual Studio 'da **dosya > yeni > proje**' yi seçin, **Visual C# > .NET Standard** düğümünü genişletin, "sınıf kitaplığı (.NET Standard)" şablonunu seçin, projeyi appgünlükçü olarak adlandırın ve **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9708e-122">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="9708e-123">Ortaya çıkan proje dosyasına sağ tıklayın ve projenin düzgün oluşturulduğundan emin olmak için **Oluştur** ' u seçin.</span><span class="sxs-lookup"><span data-stu-id="9708e-123">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="9708e-124">DLL, hata ayıklama klasöründe bulunur (veya bunun yerine bu yapılandırmayı oluşturursanız sürüm).</span><span class="sxs-lookup"><span data-stu-id="9708e-124">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="9708e-125">Gerçek bir NuGet paketi içinde, diğerlerinin uygulama derleyebileceği birçok yararlı özelliği uygulayacağınızı görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="9708e-125">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="9708e-126">Ancak bu izlenecek yol için, şablondan bir sınıf kitaplığı bir paket oluşturmak için yeterli olduğundan ek kod yazmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="9708e-126">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="9708e-127">Hala, paket için bir işlev kodu isterseniz, aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="9708e-127">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="9708e-128">Aksi takdirde seçim yapmanız gerekmediğiniz sürece, en geniş kapsamlı proje yelpazğuyla uyumluluk sağladığından NuGet paketleri için tercih edilen hedef .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="9708e-128">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="9708e-129">Paket özelliklerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9708e-129">Configure package properties</span></span>

1. <span data-ttu-id="9708e-130">Çözüm Gezgini ' de projeye sağ tıklayın, **Özellikler** menü komutu ' nı ve ardından **paket** sekmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="9708e-130">Right-click the project in Solution Explorer, and choose **Properties** menu command, then select the **Package** tab.</span></span>

   <span data-ttu-id="9708e-131">**Paket** sekmesi yalnızca Visual STUDIO 'da SDK stilindeki projeler için, genellikle .NET Standard veya .NET Core sınıf kitaplığı projelerinde görünür; SDK olmayan bir stil projesini hedefliyorsanız (genellikle .NET Framework), [projeyi geçirin](../reference/migrate-packages-config-to-package-reference.md) ve CLI kullanın `dotnet` veya [bir .NET Framework paketi oluşturma ve](create-and-publish-a-package-using-visual-studio-net-framework.md) yayımlama konusuna bakın veya [.NET Framework paketi oluşturma ve yayımlama](create-and-publish-a-package-using-visual-studio-net-framework.md) konusuna bakın. Bunun yerine adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="9708e-131">The **Package** tab appears only for SDK-style projects in Visual Studio, typically .NET Standard or .NET Core class library projects; if you are targeting a non-SDK style project (typically .NET Framework), either [migrate the project](../reference/migrate-packages-config-to-package-reference.md) and use `dotnet` CLI, or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

    ![Visual Studio projesindeki NuGet paket özellikleri](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="9708e-133">Genel tüketim için oluşturulmuş paketler için Etiketler özelliğine özel dikkat edin, Etiketler başkalarının paketinizi bulmasına ve ne yaptığını anlamasına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="9708e-133">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="9708e-134">Paketinize benzersiz bir tanımlayıcı verin ve istediğiniz diğer özellikleri doldurun.</span><span class="sxs-lookup"><span data-stu-id="9708e-134">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="9708e-135">Farklı özelliklerin bir açıklaması için bkz. [. nuspec dosya başvurusu](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="9708e-135">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="9708e-136">Buradaki tüm özellikler, Visual Studio 'nun proje `.nuspec` için oluşturduğu bildirime gider.</span><span class="sxs-lookup"><span data-stu-id="9708e-136">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="9708e-137">Pakete, nuget.org genelinde veya kullandığınız herhangi bir konakta benzersiz bir tanımlayıcı vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9708e-137">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="9708e-138">Bu izlenecek yol için, "örnek" veya "test" adını, sonraki yayımlama adımı, paketi herkese açık hale getirir (ancak gerçekten onu kullanacağından çok fazla olabilir).</span><span class="sxs-lookup"><span data-stu-id="9708e-138">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="9708e-139">Zaten var olan bir ada sahip bir paketi yayımlamayı denerseniz, bir hata görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="9708e-139">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="9708e-140">İsteğe bağlı: doğrudan proje dosyasında özellikleri görmek için Çözüm Gezgini içinde projeye sağ tıklayın ve **Appgünlükçü. csproj öğesini Düzenle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="9708e-140">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

   <span data-ttu-id="9708e-141">Bu seçenek yalnızca SDK stili özniteliği kullanan projeler için Visual Studio 2017 ' den itibaren kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="9708e-141">This option is only available starting in Visual Studio 2017 for projects that use the SDK-style attribute.</span></span> <span data-ttu-id="9708e-142">Aksi takdirde, projeye sağ tıklayın ve **Projeyi Kaldır**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="9708e-142">Otherwise, right-click the project and choose **Unload Project**.</span></span> <span data-ttu-id="9708e-143">Ardından, kaldırılan projeye sağ tıklayın ve **Appgünlükçü. csproj öğesini Düzenle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="9708e-143">Then right-click the unloaded project and choose **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="9708e-144">Pack komutunu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="9708e-144">Run the pack command</span></span>

1. <span data-ttu-id="9708e-145">Yapılandırmayı **serbest**olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9708e-145">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="9708e-146">**Çözüm Gezgini** projeye sağ tıklayın ve ardından **paket** komutunu seçin:</span><span class="sxs-lookup"><span data-stu-id="9708e-146">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Visual Studio proje bağlam menüsünde NuGet paketi komutu](media/qs_create-vs-02-pack-command.png)

    <span data-ttu-id="9708e-148">**Paket** komutunu görmüyorsanız, projeniz muhtemelen bir SDK stili proje değildir ve `nuget.exe` CLI kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9708e-148">If you don't see the **Pack** command, your project is probably not an SDK-style project and you need to use the `nuget.exe` CLI.</span></span> <span data-ttu-id="9708e-149">[Projeyi geçirin](../reference/migrate-packages-config-to-package-reference.md) ve CLI kullanın `dotnet` ya da adım adım yönergeler için [.NET Framework paketi oluşturma ve yayımlama](create-and-publish-a-package-using-visual-studio-net-framework.md) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="9708e-149">Either [migrate the project](../reference/migrate-packages-config-to-package-reference.md) and use `dotnet` CLI, or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

1. <span data-ttu-id="9708e-150">Visual Studio projeyi oluşturur ve `.nupkg` dosyayı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9708e-150">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="9708e-151">Paket dosyasının yolunu içeren ayrıntılar için **Çıkış** penceresini inceleyin (aşağıdakine benzer).</span><span class="sxs-lookup"><span data-stu-id="9708e-151">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="9708e-152">Ayrıca, derlenmiş derlemenin `bin\Release\netstandard2.0` .NET Standard 2,0 hedefine uygun olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="9708e-152">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="optional-generate-package-on-build"></a><span data-ttu-id="9708e-153">Seçim Derleme üzerinde paket oluştur</span><span class="sxs-lookup"><span data-stu-id="9708e-153">(Optional) Generate package on build</span></span>

<span data-ttu-id="9708e-154">Visual Studio 'Yu, projeyi oluşturduğunuzda NuGet paketini otomatik olarak oluşturacak şekilde yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9708e-154">You can configure Visual Studio to automatically generate the NuGet package when you build the project.</span></span>

1. <span data-ttu-id="9708e-155">Çözüm Gezgini'nde projeye sağ tıklayıp seçin **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="9708e-155">In Solution Explorer, right-click the project and choose **Properties**.</span></span>

2. <span data-ttu-id="9708e-156">**Paket** sekmesinde **derlemede NuGet paketi oluştur**' u seçin.</span><span class="sxs-lookup"><span data-stu-id="9708e-156">In the **Package** tab, select **Generate NuGet package on build**.</span></span>

   ![Derleme üzerinde otomatik olarak paket oluştur](media/qs_create-vs-05-generate-on-build.png)

> [!NOTE]
> <span data-ttu-id="9708e-158">Paketi otomatik olarak oluşturduğunuzda, paketlenecek süre projenizin derleme süresini arttırır.</span><span class="sxs-lookup"><span data-stu-id="9708e-158">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="optional-pack-with-msbuild"></a><span data-ttu-id="9708e-159">MSBuild ile (isteğe bağlı) paket</span><span class="sxs-lookup"><span data-stu-id="9708e-159">(Optional) pack with MSBuild</span></span>

<span data-ttu-id="9708e-160">**Paket** menü komutunun kullanılmasına alternatif olarak, NuGet 4. x + ve MSBuild 15.1 +, proje gerekli paket verilerini `pack` içerdiğinde bir hedefi destekler.</span><span class="sxs-lookup"><span data-stu-id="9708e-160">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="9708e-161">Bir komut istemi açın, proje klasörünüze gidin ve aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="9708e-161">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="9708e-162">(MSBuild için gereken tüm yollarla yapılandırıldıklarında, genellikle başlangıç menüsünden "Visual Studio için Geliştirici Komut İstemi" başlatmak istersiniz.)</span><span class="sxs-lookup"><span data-stu-id="9708e-162">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

<span data-ttu-id="9708e-163">Daha fazla bilgi için bkz. [MSBuild kullanarak paket oluşturma](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="9708e-163">For more information, see [Create a package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="9708e-164">Paketi Yayımla</span><span class="sxs-lookup"><span data-stu-id="9708e-164">Publish the package</span></span>

<span data-ttu-id="9708e-165">Bir `.nupkg` dosyaya sahip olduktan sonra, NuGet.org ' den alınan bir API anahtarı ile `nuget.exe` birlikte CLI veya `dotnet.exe` CLI kullanarak NuGet.org 'de yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="9708e-165">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="9708e-166">API anahtarınızı alın</span><span class="sxs-lookup"><span data-stu-id="9708e-166">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push-dotnet-cli"></a><span data-ttu-id="9708e-167">DotNet NuGet push (DotNet CLı) ile yayımlama</span><span class="sxs-lookup"><span data-stu-id="9708e-167">Publish with dotnet nuget push (dotnet CLI)</span></span>

<span data-ttu-id="9708e-168">Bu adım, kullanmanın `nuget.exe`önerilen alternatifi.</span><span class="sxs-lookup"><span data-stu-id="9708e-168">This step is the recommended alternative to using `nuget.exe`.</span></span>

<span data-ttu-id="9708e-169">Paketi yayımlayabilmeniz için önce bir komut satırı açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9708e-169">Before you can publish the package, you must first open a command line.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-with-nuget-push-nugetexe-cli"></a><span data-ttu-id="9708e-170">NuGet Push ile yayımlama (NuGet. exe CLı)</span><span class="sxs-lookup"><span data-stu-id="9708e-170">Publish with nuget push (nuget.exe CLI)</span></span>

<span data-ttu-id="9708e-171">Bu adım, kullanmanın `dotnet.exe`bir alternatifidir.</span><span class="sxs-lookup"><span data-stu-id="9708e-171">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="9708e-172">Bir komut satırı açın ve `.nupkg` dosyayı içeren klasöre geçin.</span><span class="sxs-lookup"><span data-stu-id="9708e-172">Open a command line and change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="9708e-173">Aşağıdaki komutu çalıştırarak paket adınızı (benzersiz paket KIMLIĞI) belirtip anahtar değerini API anahtarınızla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="9708e-173">Run the following command, specifying your package name (unique package ID) and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="9708e-174">NuGet. exe yayımlama işleminin sonuçlarını görüntüler:</span><span class="sxs-lookup"><span data-stu-id="9708e-174">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="9708e-175">Bkz. [NuGet Push](../reference/cli-reference/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="9708e-175">See [nuget push](../reference/cli-reference/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="9708e-176">Yayımlama hataları</span><span class="sxs-lookup"><span data-stu-id="9708e-176">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="9708e-177">Yayınlanan paketi yönetme</span><span class="sxs-lookup"><span data-stu-id="9708e-177">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="9708e-178">Benioku dosyası ve diğer dosyalar ekleme</span><span class="sxs-lookup"><span data-stu-id="9708e-178">Adding a readme and other files</span></span>

<span data-ttu-id="9708e-179">Pakete dahil edilecek dosyaları doğrudan belirtmek için, proje dosyasını düzenleyin ve `content` özelliğini kullanın:</span><span class="sxs-lookup"><span data-stu-id="9708e-179">To directly specify files to include in the package, edit the project file and use the `content` property:</span></span>

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

<span data-ttu-id="9708e-180">Bu, paket kökünde adlı `readme.txt` bir dosya içerir.</span><span class="sxs-lookup"><span data-stu-id="9708e-180">This will include a file named `readme.txt` in the package root.</span></span> <span data-ttu-id="9708e-181">Visual Studio, paketi doğrudan yükledikten hemen sonra bu dosyanın içeriğini düz metin olarak görüntüler.</span><span class="sxs-lookup"><span data-stu-id="9708e-181">Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="9708e-182">(Benioku dosyaları, bağımlılıklar olarak yüklenen paketler için gösterilmez).</span><span class="sxs-lookup"><span data-stu-id="9708e-182">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="9708e-183">Örneğin, HtmlAgilityPack paketinin Benioku dosyası şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="9708e-183">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Yükleme sonrasında bir NuGet paketi için Benioku dosyası görüntüleme](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="9708e-185">Yalnızca proje kökündeki Readme. txt ' i eklemek, sonuçta elde edilen pakete eklenmeyecektir.</span><span class="sxs-lookup"><span data-stu-id="9708e-185">Merely adding the readme.txt at the project root will not result in it being included in the resulting package.</span></span>

## <a name="related-topics"></a><span data-ttu-id="9708e-186">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="9708e-186">Related topics</span></span>

- [<span data-ttu-id="9708e-187">Paket oluşturma</span><span class="sxs-lookup"><span data-stu-id="9708e-187">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="9708e-188">Paket Yayımlama</span><span class="sxs-lookup"><span data-stu-id="9708e-188">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="9708e-189">Yayın öncesi paketler</span><span class="sxs-lookup"><span data-stu-id="9708e-189">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="9708e-190">Birden çok hedef çerçeveyi destekleme</span><span class="sxs-lookup"><span data-stu-id="9708e-190">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="9708e-191">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="9708e-191">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="9708e-192">Yerelleştirilmiş paketler oluşturma</span><span class="sxs-lookup"><span data-stu-id="9708e-192">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="9708e-193">.NET Standard kitaplığı belgeleri</span><span class="sxs-lookup"><span data-stu-id="9708e-193">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="9708e-194">.NET Framework .NET Core 'a taşıma</span><span class="sxs-lookup"><span data-stu-id="9708e-194">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
