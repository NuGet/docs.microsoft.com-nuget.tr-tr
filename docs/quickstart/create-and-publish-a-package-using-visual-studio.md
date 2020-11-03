---
title: .NET Standard NuGet paketi oluşturma ve yayımlama-Visual Studio Windows üzerinde
description: Windows üzerinde Visual Studio kullanarak .NET Standard NuGet paketi oluşturma ve yayımlama hakkında bir adım adım öğretici.
author: karann-msft
ms.author: karann
ms.date: 08/16/2019
ms.topic: quickstart
ms.openlocfilehash: 32dcc1d233154463e2950b1ce46554b1cb89956e
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237503"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a><span data-ttu-id="846ab-103">Hızlı başlangıç: Visual Studio (.NET Standard, yalnızca Windows) kullanarak bir NuGet paketi oluşturma ve yayımlama</span><span class="sxs-lookup"><span data-stu-id="846ab-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard, Windows only)</span></span>

<span data-ttu-id="846ab-104">Windows üzerinde Visual Studio 'da bir .NET Standard sınıf kitaplığından bir NuGet paketi oluşturmak ve ardından CLı aracını kullanarak nuget.org 'de yayımlamak basit bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="846ab-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio on Windows, and then publish it to nuget.org using a CLI tool.</span></span>

> [!Note]
> <span data-ttu-id="846ab-105">Mac için Visual Studio kullanıyorsanız, bir NuGet paketi oluşturma konusunda [Bu bilgilere](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) bakın veya [DotNet CLI araçlarını](create-and-publish-a-package-using-the-dotnet-cli.md)kullanın.</span><span class="sxs-lookup"><span data-stu-id="846ab-105">If you are using Visual Studio for Mac, refer to [this information](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) on creating a NuGet package, or use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="846ab-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="846ab-106">Prerequisites</span></span>

1. <span data-ttu-id="846ab-107">.NET Core ile ilgili iş yüküyle [VisualStudio.com](https://www.visualstudio.com/) adresinden herhangi bir Visual Studio 2019 sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="846ab-107">Install any edition of Visual Studio 2019 from [visualstudio.com](https://www.visualstudio.com/) with a .NET Core related workload.</span></span>

1. <span data-ttu-id="846ab-108">Zaten yüklü değilse, CLI 'yı yükleme `dotnet` .</span><span class="sxs-lookup"><span data-stu-id="846ab-108">If it's not already installed, install the `dotnet` CLI.</span></span>

   <span data-ttu-id="846ab-109">CLI için `dotnet` , Visual Studio 2017 ' den başlayarak, `dotnet` CLI, .NET Core ile ilgili tüm iş yükleri ile otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="846ab-109">For the `dotnet` CLI, starting in Visual Studio 2017, the `dotnet` CLI is automatically installed with any .NET Core related workloads.</span></span> <span data-ttu-id="846ab-110">Aksi takdirde, CLI 'yı almak için [.NET Core SDK](https://www.microsoft.com/net/download/) ' yi yüklemelisiniz `dotnet` .</span><span class="sxs-lookup"><span data-stu-id="846ab-110">Otherwise, install the [.NET Core SDK](https://www.microsoft.com/net/download/) to get the `dotnet` CLI.</span></span> <span data-ttu-id="846ab-111">`dotnet`CLI, [SDK stili biçimini](../resources/check-project-format.md) kullanan .NET Standard projeleri için gereklidir (SDK özniteliği).</span><span class="sxs-lookup"><span data-stu-id="846ab-111">The `dotnet` CLI is required for .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md) (SDK attribute).</span></span> <span data-ttu-id="846ab-112">Visual Studio 2017 ve üzeri sürümlerde bulunan varsayılan .NET Standard sınıf kitaplığı şablonu, bu makalede kullanılan SDK özniteliğini kullanır.</span><span class="sxs-lookup"><span data-stu-id="846ab-112">The default .NET Standard class library template in Visual Studio 2017 and higher, which is used in this article, uses the SDK attribute.</span></span>
   
   > [!Important]
   > <span data-ttu-id="846ab-113">SDK olmayan bir proje ile çalışıyorsanız, bunun yerine paketi oluşturmak ve yayımlamak için [.NET Framework paketi oluşturma ve yayımlama (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) konusundaki yordamları izleyin.</span><span class="sxs-lookup"><span data-stu-id="846ab-113">If you are working with a non-SDK-style project, follow the procedures in [Create and publish a .NET Framework package (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) to create and publish the package instead.</span></span> <span data-ttu-id="846ab-114">Bu makalede, `dotnet` CLI önerilir.</span><span class="sxs-lookup"><span data-stu-id="846ab-114">For this article, the `dotnet` CLI is recommended.</span></span> <span data-ttu-id="846ab-115">CLI kullanarak herhangi bir NuGet paketini yayımlayabilseniz de `nuget.exe` , bu makaledeki adımların BAZıLARı SDK stilindeki projelere ve DotNet CLI 'ya özeldir.</span><span class="sxs-lookup"><span data-stu-id="846ab-115">Although you can publish any NuGet package using the `nuget.exe` CLI, some of the steps in this article are specific to SDK-style projects and the dotnet CLI.</span></span> <span data-ttu-id="846ab-116">nuget.exe CLı, [SDK olmayan-stil projeleri](../resources/check-project-format.md) için kullanılır (genellikle .NET Framework).</span><span class="sxs-lookup"><span data-stu-id="846ab-116">The nuget.exe CLI is used for [non-SDK-style projects](../resources/check-project-format.md) (typically .NET Framework).</span></span>

1. <span data-ttu-id="846ab-117">Henüz bir [hesabınız yoksa NuGet.org üzerinde ücretsiz bir hesaba kaydolun](../nuget-org/individual-accounts.md#add-a-new-individual-account) .</span><span class="sxs-lookup"><span data-stu-id="846ab-117">[Register for a free account on nuget.org](../nuget-org/individual-accounts.md#add-a-new-individual-account) if you don't have one already.</span></span> <span data-ttu-id="846ab-118">Yeni hesap oluşturma onay e-postası gönderir.</span><span class="sxs-lookup"><span data-stu-id="846ab-118">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="846ab-119">Bir paketi karşıya yükleyebilmek için önce hesabı onaylamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="846ab-119">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="846ab-120">Sınıf kitaplığı projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="846ab-120">Create a class library project</span></span>

<span data-ttu-id="846ab-121">Paketlemek istediğiniz kod için mevcut bir .NET Standard Sınıf Kitaplığı projesini kullanabilir veya basit bir tane oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="846ab-121">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="846ab-122">Visual Studio 'da **dosya > yeni > proje** ' yi seçin, **visual C# > .NET Standard** düğümünü genişletin, "sınıf kitaplığı (.NET Standard)" şablonunu seçin, projeyi appgünlükçü olarak adlandırın ve **Tamam** ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="846ab-122">In Visual Studio, choose **File > New > Project** , expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK** .</span></span>

   > [!Tip]
   > <span data-ttu-id="846ab-123">Aksi takdirde seçim yapmanız gerekmediğiniz sürece, en geniş kapsamlı proje yelpazğuyla uyumluluk sağladığından NuGet paketleri için tercih edilen hedef .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="846ab-123">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

1. <span data-ttu-id="846ab-124">Ortaya çıkan proje dosyasına sağ tıklayın ve projenin düzgün oluşturulduğundan emin olmak için **Oluştur** ' u seçin.</span><span class="sxs-lookup"><span data-stu-id="846ab-124">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="846ab-125">DLL, hata ayıklama klasöründe bulunur (veya bunun yerine bu yapılandırmayı oluşturursanız sürüm).</span><span class="sxs-lookup"><span data-stu-id="846ab-125">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="846ab-126">Gerçek bir NuGet paketi içinde, diğerlerinin uygulama derleyebileceği birçok yararlı özelliği uygulayacağınızı görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="846ab-126">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="846ab-127">Ancak bu izlenecek yol için, şablondan bir sınıf kitaplığı bir paket oluşturmak için yeterli olduğundan ek kod yazmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="846ab-127">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="846ab-128">Hala, paket için bir işlev kodu isterseniz, aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="846ab-128">Still, if you'd like some functional code for the package, use the following:</span></span>

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

## <a name="configure-package-properties"></a><span data-ttu-id="846ab-129">Paket özelliklerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="846ab-129">Configure package properties</span></span>

1. <span data-ttu-id="846ab-130">Çözüm Gezgini ' de projeye sağ tıklayın, **Özellikler** menü komutu ' nı ve ardından **paket** sekmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="846ab-130">Right-click the project in Solution Explorer, and choose **Properties** menu command, then select the **Package** tab.</span></span>

   <span data-ttu-id="846ab-131">**Paket** sekmesi yalnızca Visual STUDIO 'da SDK stilindeki projeler için, genellikle .NET Standard veya .NET Core sınıf kitaplığı projelerinde görünür; SDK olmayan bir stil projesini hedefliyorsanız (genellikle .NET Framework), [projeyi geçirin](../consume-packages/migrate-packages-config-to-package-reference.md) ya da adım adım yönergeler için [bir .NET Framework paketi oluşturma ve yayımlama](create-and-publish-a-package-using-visual-studio-net-framework.md) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="846ab-131">The **Package** tab appears only for SDK-style projects in Visual Studio, typically .NET Standard or .NET Core class library projects; if you are targeting a non-SDK style project (typically .NET Framework), either [migrate the project](../consume-packages/migrate-packages-config-to-package-reference.md) or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

    ![Visual Studio projesindeki NuGet paket özellikleri](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="846ab-133">Genel tüketim için oluşturulmuş paketler için Etiketler özelliğine özel dikkat edin, **Etiketler başkalarının** paketinizi bulmasına ve ne yaptığını anlamasına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="846ab-133">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="846ab-134">Paketinize benzersiz bir tanımlayıcı verin ve istediğiniz diğer özellikleri doldurun.</span><span class="sxs-lookup"><span data-stu-id="846ab-134">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="846ab-135">MSBuild özelliklerinin (SDK stili proje) bir *. nuspec* içindeki özelliklere eşlenmesi için bkz. [paket hedefleri](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="846ab-135">For a mapping of MSBuild properties (SDK-style project) to properties in a *.nuspec* , see [pack targets](../reference/msbuild-targets.md#pack-target).</span></span> <span data-ttu-id="846ab-136">Özelliklerinin açıklamaları için bkz [. nuspec dosya başvurusu](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="846ab-136">For descriptions of properties, see the [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="846ab-137">Buradaki tüm özellikler, `.nuspec` Visual Studio 'nun proje için oluşturduğu bildirime gider.</span><span class="sxs-lookup"><span data-stu-id="846ab-137">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="846ab-138">Pakete, nuget.org genelinde veya kullandığınız herhangi bir konakta benzersiz bir tanımlayıcı vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="846ab-138">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="846ab-139">Bu izlenecek yol için, "örnek" veya "test" adını, sonraki yayımlama adımı, paketi herkese açık hale getirir (ancak gerçekten onu kullanacağından çok fazla olabilir).</span><span class="sxs-lookup"><span data-stu-id="846ab-139">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="846ab-140">Zaten var olan bir ada sahip bir paketi yayımlamayı denerseniz, bir hata görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="846ab-140">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="846ab-141">Seçim Doğrudan proje dosyasında özellikleri görmek için Çözüm Gezgini içinde projeye sağ tıklayın ve **Appgünlükçü. csproj öğesini Düzenle** ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="846ab-141">(Optional) To see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj** .</span></span>

   <span data-ttu-id="846ab-142">Bu seçenek yalnızca SDK stili özniteliği kullanan projeler için Visual Studio 2017 ' den itibaren kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="846ab-142">This option is only available starting in Visual Studio 2017 for projects that use the SDK-style attribute.</span></span> <span data-ttu-id="846ab-143">Aksi takdirde, projeye sağ tıklayın ve **Projeyi Kaldır** ' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="846ab-143">Otherwise, right-click the project and choose **Unload Project** .</span></span> <span data-ttu-id="846ab-144">Ardından, kaldırılan projeye sağ tıklayın ve **Appgünlükçü. csproj öğesini Düzenle** ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="846ab-144">Then right-click the unloaded project and choose **Edit AppLogger.csproj** .</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="846ab-145">Pack komutunu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="846ab-145">Run the pack command</span></span>

1. <span data-ttu-id="846ab-146">Yapılandırmayı **serbest** olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="846ab-146">Set the configuration to **Release** .</span></span>

1. <span data-ttu-id="846ab-147">**Çözüm Gezgini** projeye sağ tıklayın ve ardından **paket** komutunu seçin:</span><span class="sxs-lookup"><span data-stu-id="846ab-147">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Visual Studio proje bağlam menüsünde NuGet paketi komutu](media/qs_create-vs-02-pack-command.png)

    <span data-ttu-id="846ab-149">**Paket** komutunu görmüyorsanız, projeniz muhtemelen bir SDK stili proje değildir ve CLI kullanmanız gerekir `nuget.exe` .</span><span class="sxs-lookup"><span data-stu-id="846ab-149">If you don't see the **Pack** command, your project is probably not an SDK-style project and you need to use the `nuget.exe` CLI.</span></span> <span data-ttu-id="846ab-150">[Projeyi geçirin](../consume-packages/migrate-packages-config-to-package-reference.md) ve `dotnet` CLI kullanın ya da adım adım yönergeler Için [.NET Framework paketi oluşturma ve yayımlama](create-and-publish-a-package-using-visual-studio-net-framework.md) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="846ab-150">Either [migrate the project](../consume-packages/migrate-packages-config-to-package-reference.md) and use `dotnet` CLI, or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

1. <span data-ttu-id="846ab-151">Visual Studio projeyi oluşturur ve `.nupkg` dosyayı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="846ab-151">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="846ab-152">Paket dosyasının yolunu içeren ayrıntılar için **Çıkış** penceresini inceleyin (aşağıdakine benzer).</span><span class="sxs-lookup"><span data-stu-id="846ab-152">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="846ab-153">Ayrıca, derlenmiş derlemenin `bin\Release\netstandard2.0` .NET Standard 2,0 hedefine uygun olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="846ab-153">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="optional-generate-package-on-build"></a><span data-ttu-id="846ab-154">Seçim Derleme üzerinde paket oluştur</span><span class="sxs-lookup"><span data-stu-id="846ab-154">(Optional) Generate package on build</span></span>

<span data-ttu-id="846ab-155">Visual Studio 'Yu, projeyi oluşturduğunuzda NuGet paketini otomatik olarak oluşturacak şekilde yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="846ab-155">You can configure Visual Studio to automatically generate the NuGet package when you build the project.</span></span>

1. <span data-ttu-id="846ab-156">Çözüm Gezgini, projeye sağ tıklayın ve **Özellikler** ' i seçin.</span><span class="sxs-lookup"><span data-stu-id="846ab-156">In Solution Explorer, right-click the project and choose **Properties** .</span></span>

2. <span data-ttu-id="846ab-157">**Paket** sekmesinde **derlemede NuGet paketi oluştur** ' u seçin.</span><span class="sxs-lookup"><span data-stu-id="846ab-157">In the **Package** tab, select **Generate NuGet package on build** .</span></span>

   ![Derleme üzerinde otomatik olarak paket oluştur](media/qs_create-vs-05-generate-on-build.png)

> [!NOTE]
> <span data-ttu-id="846ab-159">Paketi otomatik olarak oluşturduğunuzda, paketlenecek süre projenizin derleme süresini arttırır.</span><span class="sxs-lookup"><span data-stu-id="846ab-159">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="optional-pack-with-msbuild"></a><span data-ttu-id="846ab-160">MSBuild ile (isteğe bağlı) paket</span><span class="sxs-lookup"><span data-stu-id="846ab-160">(Optional) pack with MSBuild</span></span>

<span data-ttu-id="846ab-161">**Paket** menü komutunun kullanılmasına alternatif olarak, NuGet 4. x + ve MSBuild 15.1 +, `pack` Proje gerekli paket verilerini içerdiğinde bir hedefi destekler.</span><span class="sxs-lookup"><span data-stu-id="846ab-161">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="846ab-162">Bir komut istemi açın, proje klasörünüze gidin ve aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="846ab-162">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="846ab-163">(MSBuild için gereken tüm yollarla yapılandırıldıklarında, genellikle başlangıç menüsünden "Visual Studio için Geliştirici Komut İstemi" başlatmak istersiniz.)</span><span class="sxs-lookup"><span data-stu-id="846ab-163">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

<span data-ttu-id="846ab-164">Daha fazla bilgi için bkz. [MSBuild kullanarak paket oluşturma](../create-packages/creating-a-package-msbuild.md).</span><span class="sxs-lookup"><span data-stu-id="846ab-164">For more information, see [Create a package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="846ab-165">Paketi Yayımla</span><span class="sxs-lookup"><span data-stu-id="846ab-165">Publish the package</span></span>

<span data-ttu-id="846ab-166">Bir dosyaya sahip olduktan sonra `.nupkg` , `nuget.exe` NuGet.org ' `dotnet.exe` den alınan bir API anahtarı ile birlikte CLI veya CLI kullanarak NuGet.org 'de yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="846ab-166">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="846ab-167">API anahtarınızı alın</span><span class="sxs-lookup"><span data-stu-id="846ab-167">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-the-dotnet-cli-or-nugetexe-cli"></a><span data-ttu-id="846ab-168">DotNet CLı veya nuget.exe CLı ile yayımlama</span><span class="sxs-lookup"><span data-stu-id="846ab-168">Publish with the dotnet CLI or nuget.exe CLI</span></span>

<span data-ttu-id="846ab-169">CLı aracınız için **.NET Core CLI** (DotNet CLI) veya **NUGET** (nuget.exe CLI) sekmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="846ab-169">Select the tab for your CLI tool, either **.NET Core CLI** (dotnet CLI) or **NuGet** (nuget.exe CLI).</span></span>

# <a name="net-core-cli"></a>[<span data-ttu-id="846ab-170">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="846ab-170">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="846ab-171">Bu adım, kullanmanın önerilen alternatifi `nuget.exe` .</span><span class="sxs-lookup"><span data-stu-id="846ab-171">This step is the recommended alternative to using `nuget.exe`.</span></span>

<span data-ttu-id="846ab-172">Paketi yayımlayabilmeniz için önce bir komut satırı açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="846ab-172">Before you can publish the package, you must first open a command line.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

# <a name="nuget"></a>[<span data-ttu-id="846ab-173">NuGet</span><span class="sxs-lookup"><span data-stu-id="846ab-173">NuGet</span></span>](#tab/nuget)

<span data-ttu-id="846ab-174">Bu adım, kullanmanın bir alternatifidir `dotnet.exe` .</span><span class="sxs-lookup"><span data-stu-id="846ab-174">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="846ab-175">Bir komut satırı açın ve dosyayı içeren klasöre geçin `.nupkg` .</span><span class="sxs-lookup"><span data-stu-id="846ab-175">Open a command line and change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="846ab-176">Aşağıdaki komutu çalıştırarak paket adınızı (benzersiz paket KIMLIĞI) belirtip anahtar değerini API anahtarınızla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="846ab-176">Run the following command, specifying your package name (unique package ID) and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="846ab-177">nuget.exe yayımlama işleminin sonuçlarını görüntüler:</span><span class="sxs-lookup"><span data-stu-id="846ab-177">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="846ab-178">Bkz. [NuGet Push](../reference/cli-reference/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="846ab-178">See [nuget push](../reference/cli-reference/cli-ref-push.md).</span></span>

---

### <a name="publish-errors"></a><span data-ttu-id="846ab-179">Yayımlama hataları</span><span class="sxs-lookup"><span data-stu-id="846ab-179">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="846ab-180">Yayınlanan paketi yönetme</span><span class="sxs-lookup"><span data-stu-id="846ab-180">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="846ab-181">Benioku dosyası ve diğer dosyalar ekleme</span><span class="sxs-lookup"><span data-stu-id="846ab-181">Adding a readme and other files</span></span>

<span data-ttu-id="846ab-182">Pakete dahil edilecek dosyaları doğrudan belirtmek için, proje dosyasını düzenleyin ve `content` özelliğini kullanın:</span><span class="sxs-lookup"><span data-stu-id="846ab-182">To directly specify files to include in the package, edit the project file and use the `content` property:</span></span>

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

<span data-ttu-id="846ab-183">Bu, paket kökünde adlı bir dosya içerir `readme.txt` .</span><span class="sxs-lookup"><span data-stu-id="846ab-183">This will include a file named `readme.txt` in the package root.</span></span> <span data-ttu-id="846ab-184">Visual Studio, paketi doğrudan yükledikten hemen sonra bu dosyanın içeriğini düz metin olarak görüntüler.</span><span class="sxs-lookup"><span data-stu-id="846ab-184">Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="846ab-185">(Benioku dosyaları, bağımlılıklar olarak yüklenen paketler için gösterilmez).</span><span class="sxs-lookup"><span data-stu-id="846ab-185">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="846ab-186">Örneğin, HtmlAgilityPack paketinin Benioku dosyası şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="846ab-186">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Yükleme sonrasında bir NuGet paketi için Benioku dosyası görüntüleme](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="846ab-188">Yalnızca proje köküne readme.txt eklemek, sonuçta elde edilen pakete eklenmeyecektir.</span><span class="sxs-lookup"><span data-stu-id="846ab-188">Merely adding the readme.txt at the project root will not result in it being included in the resulting package.</span></span>

## <a name="related-video"></a><span data-ttu-id="846ab-189">İlgili video</span><span class="sxs-lookup"><span data-stu-id="846ab-189">Related video</span></span>

> [!Video https://channel9.msdn.com/Series/NuGet-101/Create-and-Publish-a-NuGet-Package-with-Visual-Studio-4-of-5/player]

<span data-ttu-id="846ab-190">[Channel 9](https://channel9.msdn.com/Series/NuGet-101) ve [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_)'da daha fazla NuGet videoları bulun.</span><span class="sxs-lookup"><span data-stu-id="846ab-190">Find more NuGet videos on [Channel 9](https://channel9.msdn.com/Series/NuGet-101) and [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span></span>

## <a name="related-topics"></a><span data-ttu-id="846ab-191">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="846ab-191">Related topics</span></span>

- [<span data-ttu-id="846ab-192">Paket oluşturma</span><span class="sxs-lookup"><span data-stu-id="846ab-192">Create a Package</span></span>](../create-packages/creating-a-package-dotnet-cli.md)
- [<span data-ttu-id="846ab-193">Paket yayımlama</span><span class="sxs-lookup"><span data-stu-id="846ab-193">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="846ab-194">Yayın öncesi paketler</span><span class="sxs-lookup"><span data-stu-id="846ab-194">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="846ab-195">Birden çok hedef çerçeveyi destekleme</span><span class="sxs-lookup"><span data-stu-id="846ab-195">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="846ab-196">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="846ab-196">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="846ab-197">Yerelleştirilmiş paketler oluşturma</span><span class="sxs-lookup"><span data-stu-id="846ab-197">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="846ab-198">.NET Standard kitaplığı belgeleri</span><span class="sxs-lookup"><span data-stu-id="846ab-198">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="846ab-199">.NET Framework .NET Core 'a taşıma</span><span class="sxs-lookup"><span data-stu-id="846ab-199">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
