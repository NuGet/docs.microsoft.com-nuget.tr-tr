---
title: Bir .NET Standart NuGet paketi oluşturun ve yayımlayın - Windows'ta Visual Studio
description: Windows'da Visual Studio'u kullanarak bir .NET Standart NuGet paketi oluşturma ve yayımlama konusunda bir iz geçidi öğretici.
author: karann-msft
ms.author: karann
ms.date: 08/16/2019
ms.topic: quickstart
ms.openlocfilehash: 32dcc1d233154463e2950b1ce46554b1cb89956e
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79429033"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a><span data-ttu-id="78fbf-103">Quickstart: Visual Studio 'yı kullanarak bir NuGet paketi oluşturun ve yayımlayın (.NET Standardı, yalnızca Windows)</span><span class="sxs-lookup"><span data-stu-id="78fbf-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard, Windows only)</span></span>

<span data-ttu-id="78fbf-104">Windows'daki Visual Studio'daki .NET Standart Sınıf Kitaplığı'ndan bir NuGet paketi oluşturmak ve ardından cli aracını kullanarak nuget.org yayınlamak basit bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="78fbf-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio on Windows, and then publish it to nuget.org using a CLI tool.</span></span>

> [!Note]
> <span data-ttu-id="78fbf-105">Mac için Visual Studio kullanıyorsanız, nuget paketi oluşturma yla ilgili [bu bilgilere](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) bakın veya [dotnet CLI araçlarını](create-and-publish-a-package-using-the-dotnet-cli.md)kullanın.</span><span class="sxs-lookup"><span data-stu-id="78fbf-105">If you are using Visual Studio for Mac, refer to [this information](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) on creating a NuGet package, or use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="78fbf-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="78fbf-106">Prerequisites</span></span>

1. <span data-ttu-id="78fbf-107">.NET Core ile ilgili iş yüküne [sahip visualstudio.com](https://www.visualstudio.com/) Visual Studio 2019'un herhangi bir sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="78fbf-107">Install any edition of Visual Studio 2019 from [visualstudio.com](https://www.visualstudio.com/) with a .NET Core related workload.</span></span>

1. <span data-ttu-id="78fbf-108">Zaten yüklü değilse, CLI'yi `dotnet` yükleyin.</span><span class="sxs-lookup"><span data-stu-id="78fbf-108">If it's not already installed, install the `dotnet` CLI.</span></span>

   <span data-ttu-id="78fbf-109">`dotnet` Visual Studio 2017'den `dotnet` başlayarak CLI için ,NET Core ile ilgili iş yükleriyle otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="78fbf-109">For the `dotnet` CLI, starting in Visual Studio 2017, the `dotnet` CLI is automatically installed with any .NET Core related workloads.</span></span> <span data-ttu-id="78fbf-110">Aksi takdirde, CLI almak için `dotnet` [.NET Core SDK'yı](https://www.microsoft.com/net/download/) yükleyin.</span><span class="sxs-lookup"><span data-stu-id="78fbf-110">Otherwise, install the [.NET Core SDK](https://www.microsoft.com/net/download/) to get the `dotnet` CLI.</span></span> <span data-ttu-id="78fbf-111">[CLI, SDK stili biçimini (SDK](../resources/check-project-format.md) özniteliği) kullanan .NET Standard projeleri için gereklidir. `dotnet`</span><span class="sxs-lookup"><span data-stu-id="78fbf-111">The `dotnet` CLI is required for .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md) (SDK attribute).</span></span> <span data-ttu-id="78fbf-112">Visual Studio 2017 ve üzeri'nde bu makalede kullanılan varsayılan .NET Standart sınıf kitaplığı şablonu SDK özniteliğini kullanır.</span><span class="sxs-lookup"><span data-stu-id="78fbf-112">The default .NET Standard class library template in Visual Studio 2017 and higher, which is used in this article, uses the SDK attribute.</span></span>
   
   > [!Important]
   > <span data-ttu-id="78fbf-113">SDK tarzı olmayan bir projeyle çalışıyorsanız, paketi oluşturmak ve yayınlamak için [bir .NET Framework paketi (Visual Studio) oluştur'daki](create-and-publish-a-package-using-visual-studio-net-framework.md) yordamları izleyin ve yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="78fbf-113">If you are working with a non-SDK-style project, follow the procedures in [Create and publish a .NET Framework package (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) to create and publish the package instead.</span></span> <span data-ttu-id="78fbf-114">Bu makale için `dotnet` CLI önerilir.</span><span class="sxs-lookup"><span data-stu-id="78fbf-114">For this article, the `dotnet` CLI is recommended.</span></span> <span data-ttu-id="78fbf-115">`nuget.exe` CLI'yi kullanarak herhangi bir NuGet paketini yayımlayabilirsiniz, ancak bu makaledeki bazı adımlar SDK tarzı projelere ve dotnet CLI'ye özgüdür.</span><span class="sxs-lookup"><span data-stu-id="78fbf-115">Although you can publish any NuGet package using the `nuget.exe` CLI, some of the steps in this article are specific to SDK-style projects and the dotnet CLI.</span></span> <span data-ttu-id="78fbf-116">nuget.exe CLI, [SDK tarzı olmayan projeler](../resources/check-project-format.md) için kullanılır (genellikle .NET Framework).</span><span class="sxs-lookup"><span data-stu-id="78fbf-116">The nuget.exe CLI is used for [non-SDK-style projects](../resources/check-project-format.md) (typically .NET Framework).</span></span>

1. <span data-ttu-id="78fbf-117">Zaten bir hesabınız yoksa [nuget.org ücretsiz bir hesaba kaydolun.](../nuget-org/individual-accounts.md#add-a-new-individual-account)</span><span class="sxs-lookup"><span data-stu-id="78fbf-117">[Register for a free account on nuget.org](../nuget-org/individual-accounts.md#add-a-new-individual-account) if you don't have one already.</span></span> <span data-ttu-id="78fbf-118">Yeni bir hesap oluşturmak bir onay e-postası gönderir.</span><span class="sxs-lookup"><span data-stu-id="78fbf-118">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="78fbf-119">Bir paket yükleyemeden önce hesabı onaylamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="78fbf-119">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="78fbf-120">Sınıf kitaplığı projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="78fbf-120">Create a class library project</span></span>

<span data-ttu-id="78fbf-121">Paketlemek istediğiniz kod için varolan bir .NET Standart Sınıf Kitaplığı projesini kullanabilir veya aşağıdaki gibi basit bir kitap oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="78fbf-121">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="78fbf-122">Visual **Studio'da, Yeni > Projesi > Dosya'yı**seçin, **Visual C# > .NET Standard** düğümünü genişletin, "Sınıf Kitaplığı (.NET Standart)" şablonuna tıklayın, proje AppLogger'ı adlandırın ve **Tamam'ı**tıklatın.</span><span class="sxs-lookup"><span data-stu-id="78fbf-122">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

   > [!Tip]
   > <span data-ttu-id="78fbf-123">Aksini seçmek için bir nedeniniz yoksa, .NET Standard, en geniş tüketici proje yelpazesiyle uyumluluk sağladığından NuGet paketleri için tercih edilen hedeftir.</span><span class="sxs-lookup"><span data-stu-id="78fbf-123">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

1. <span data-ttu-id="78fbf-124">Projenin düzgün oluşturulduğundan emin olmak için ortaya çıkan proje dosyasına sağ tıklayın ve **Yapı'yı** seçin.</span><span class="sxs-lookup"><span data-stu-id="78fbf-124">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="78fbf-125">DLL Hata Ayıklama klasöründe bulunur (veya bu yapılandırmayı oluşturursanız serbest bırakın).</span><span class="sxs-lookup"><span data-stu-id="78fbf-125">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="78fbf-126">Gerçek bir NuGet paketi içinde, tabii ki, başkalarının uygulamaları oluşturabilirsiniz birçok yararlı özellikleri uygulamak.</span><span class="sxs-lookup"><span data-stu-id="78fbf-126">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="78fbf-127">Ancak bu geçiş için, şablondan bir sınıf kitaplığı bir paket oluşturmak için yeterli olduğundan, ek kod yazmazsınız.</span><span class="sxs-lookup"><span data-stu-id="78fbf-127">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="78fbf-128">Yine de, paket için bazı işlevsel kod istiyorsanız, aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="78fbf-128">Still, if you'd like some functional code for the package, use the following:</span></span>

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

## <a name="configure-package-properties"></a><span data-ttu-id="78fbf-129">Paket özelliklerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="78fbf-129">Configure package properties</span></span>

1. <span data-ttu-id="78fbf-130">Solution Explorer'da projeyi sağ tıklatın ve **Özellikler** menüsü komutunu seçin ve ardından **Paket** sekmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="78fbf-130">Right-click the project in Solution Explorer, and choose **Properties** menu command, then select the **Package** tab.</span></span>

   <span data-ttu-id="78fbf-131">**Paket** sekmesi yalnızca Visual Studio'daki SDK tarzı projeler için görünür, genellikle .NET Standardı veya .NET Core sınıf kitaplık projeleri; SDK tarzı olmayan bir projeyi (genellikle .NET Framework) hedefliyorsanız, [projeyi geçirin](../consume-packages/migrate-packages-config-to-package-reference.md) veya adım adım yönergeler yerine [bir .NET Framework paketi oluştur ve yayımlama](create-and-publish-a-package-using-visual-studio-net-framework.md) yı görün.</span><span class="sxs-lookup"><span data-stu-id="78fbf-131">The **Package** tab appears only for SDK-style projects in Visual Studio, typically .NET Standard or .NET Core class library projects; if you are targeting a non-SDK style project (typically .NET Framework), either [migrate the project](../consume-packages/migrate-packages-config-to-package-reference.md) or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

    ![Görsel Stüdyo projesinde NuGet paket özellikleri](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="78fbf-133">Genel tüketim için oluşturulmuş paketler için, etiketler başkalarının paketinizi bulmasına ve ne işe yaradığına yardımcı olduğundan, **Etiketler** özelliğine özel olarak dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="78fbf-133">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="78fbf-134">Paketinize benzersiz bir tanımlayıcı verin ve istediğiniz diğer özellikleri doldurun.</span><span class="sxs-lookup"><span data-stu-id="78fbf-134">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="78fbf-135">MSBuild özelliklerinin (SDK stili proje) bir *.nuspec'teki*özelliklere eşlenemeiçin [paket hedeflerine](../reference/msbuild-targets.md#pack-target)bakın.</span><span class="sxs-lookup"><span data-stu-id="78fbf-135">For a mapping of MSBuild properties (SDK-style project) to properties in a *.nuspec*, see [pack targets](../reference/msbuild-targets.md#pack-target).</span></span> <span data-ttu-id="78fbf-136">Özelliklerin açıklamaları için [.nuspec dosya başvurusuna](../reference/nuspec.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="78fbf-136">For descriptions of properties, see the [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="78fbf-137">Buradaki tüm özellikler Visual `.nuspec` Studio'nun proje için oluşturduğu manifestoya gidiyor.</span><span class="sxs-lookup"><span data-stu-id="78fbf-137">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="78fbf-138">Pakete, nuget.org veya kullandığınız ana bilgisayarda benzersiz bir tanımlayıcı vermelisiniz.</span><span class="sxs-lookup"><span data-stu-id="78fbf-138">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="78fbf-139">Bu izlenecek yol için, daha sonraki yayımlama adımı paketi herkese açık hale getirebildiğinden (kimsenin gerçekten kullanması pek olası olmasa da) adına "Örnek" veya "Test" eklenmesini öneririz.</span><span class="sxs-lookup"><span data-stu-id="78fbf-139">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="78fbf-140">Zaten var olan bir ada sahip bir paketi yayımlamaya çalışırsanız, bir hata görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="78fbf-140">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="78fbf-141">(İsteğe bağlı) Özellikleri doğrudan proje dosyasında görmek için Solution Explorer'da projeyi sağ tıklatın ve **AppLogger.csproj'u edit'i**seçin.</span><span class="sxs-lookup"><span data-stu-id="78fbf-141">(Optional) To see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

   <span data-ttu-id="78fbf-142">Bu seçenek yalnızca Visual Studio 2017'den itibaren SDK stili özniteliği kullanan projeler için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="78fbf-142">This option is only available starting in Visual Studio 2017 for projects that use the SDK-style attribute.</span></span> <span data-ttu-id="78fbf-143">Aksi takdirde, projeyi sağ tıklatın ve **Project'i Boşalt'ı**seçin.</span><span class="sxs-lookup"><span data-stu-id="78fbf-143">Otherwise, right-click the project and choose **Unload Project**.</span></span> <span data-ttu-id="78fbf-144">Sonra sağ boşproje tıklayın ve **AppLogger.csproj edit**seçin.</span><span class="sxs-lookup"><span data-stu-id="78fbf-144">Then right-click the unloaded project and choose **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="78fbf-145">Sürü komutunu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="78fbf-145">Run the pack command</span></span>

1. <span data-ttu-id="78fbf-146">Yapılandırmayı **Release**olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="78fbf-146">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="78fbf-147">**Solution Explorer'da** projeyi sağ tıklatın ve **Paket** komutunu seçin:</span><span class="sxs-lookup"><span data-stu-id="78fbf-147">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Visual Studio proje bağlam menüsünde NuGet paketi komutu](media/qs_create-vs-02-pack-command.png)

    <span data-ttu-id="78fbf-149">**Paket** komutunu görmüyorsanız, projeniz büyük olasılıkla SDK tarzı bir proje değildir `nuget.exe` ve CLI'yi kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="78fbf-149">If you don't see the **Pack** command, your project is probably not an SDK-style project and you need to use the `nuget.exe` CLI.</span></span> <span data-ttu-id="78fbf-150">[Projeyi geçirin](../consume-packages/migrate-packages-config-to-package-reference.md) ve `dotnet` CLI'yi kullanın veya adım adım yönergeler yerine [bir .NET Framework paketi oluştur ve yayımla'ya](create-and-publish-a-package-using-visual-studio-net-framework.md) bakın.</span><span class="sxs-lookup"><span data-stu-id="78fbf-150">Either [migrate the project](../consume-packages/migrate-packages-config-to-package-reference.md) and use `dotnet` CLI, or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

1. <span data-ttu-id="78fbf-151">Visual Studio projeyi oluşturur ve `.nupkg` dosyayı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="78fbf-151">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="78fbf-152">Paket dosyasına giden yolu içeren ayrıntılar (aşağıdakilere benzer) **Çıktı** penceresini inceleyin.</span><span class="sxs-lookup"><span data-stu-id="78fbf-152">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="78fbf-153">Yapılı derlemenin .NET `bin\Release\netstandard2.0` Standart 2.0 hedefine yakışır şekilde olduğunu da unutmayın.</span><span class="sxs-lookup"><span data-stu-id="78fbf-153">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="optional-generate-package-on-build"></a><span data-ttu-id="78fbf-154">(İsteğe bağlı) Yapı da paket oluşturma</span><span class="sxs-lookup"><span data-stu-id="78fbf-154">(Optional) Generate package on build</span></span>

<span data-ttu-id="78fbf-155">Projeyi oluştururken Visual Studio'yu NuGet paketini otomatik olarak oluşturacak şekilde yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78fbf-155">You can configure Visual Studio to automatically generate the NuGet package when you build the project.</span></span>

1. <span data-ttu-id="78fbf-156">Çözüm Gezgini'nde projeyi sağ tıklatın ve **Özellikler'i**seçin.</span><span class="sxs-lookup"><span data-stu-id="78fbf-156">In Solution Explorer, right-click the project and choose **Properties**.</span></span>

2. <span data-ttu-id="78fbf-157">**Paket** sekmesinde, **yapıda NuGet paketi**oluştur'u'nu seçin.</span><span class="sxs-lookup"><span data-stu-id="78fbf-157">In the **Package** tab, select **Generate NuGet package on build**.</span></span>

   ![Otomatik olarak yapı üzerinde paket oluşturmak](media/qs_create-vs-05-generate-on-build.png)

> [!NOTE]
> <span data-ttu-id="78fbf-159">Paketi otomatik olarak oluşturduğunuzda, paketi hazırlama süresi projenizin oluşturma süresini artırır.</span><span class="sxs-lookup"><span data-stu-id="78fbf-159">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="optional-pack-with-msbuild"></a><span data-ttu-id="78fbf-160">MSBuild ile (İsteğe bağlı) paket</span><span class="sxs-lookup"><span data-stu-id="78fbf-160">(Optional) pack with MSBuild</span></span>

<span data-ttu-id="78fbf-161">**Paket** menüsü komutunu kullanmaya alternatif olarak, NuGet 4.x+ ve MSBuild `pack` 15.1+ proje gerekli paket verilerini içerdiğinde bir hedefi destekler.</span><span class="sxs-lookup"><span data-stu-id="78fbf-161">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="78fbf-162">Komut istemini açın, proje klasörünüze gidin ve aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="78fbf-162">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="78fbf-163">(MsBuild için gerekli tüm yollarla yapılandırılacak gibi, genellikle Başlat menüsünden "Visual Studio için Geliştirici Komut Komut Ustem"i başlatmak istersiniz.)</span><span class="sxs-lookup"><span data-stu-id="78fbf-163">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

<span data-ttu-id="78fbf-164">Daha fazla bilgi için [bkz.](../create-packages/creating-a-package-msbuild.md)</span><span class="sxs-lookup"><span data-stu-id="78fbf-164">For more information, see [Create a package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="78fbf-165">Paketi yayımlama</span><span class="sxs-lookup"><span data-stu-id="78fbf-165">Publish the package</span></span>

<span data-ttu-id="78fbf-166">Bir `.nupkg` dosyaya sahip olduktan sonra, nuget.org'dan edinilen bir API anahtarıyla birlikte `nuget.exe` CLI veya `dotnet.exe` CLI'yi kullanarak dosyayı nuget.org yayımlarsınız.</span><span class="sxs-lookup"><span data-stu-id="78fbf-166">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="78fbf-167">API anahtarınızı edinin</span><span class="sxs-lookup"><span data-stu-id="78fbf-167">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-the-dotnet-cli-or-nugetexe-cli"></a><span data-ttu-id="78fbf-168">dotnet CLI veya nuget.exe CLI ile yayımlayın</span><span class="sxs-lookup"><span data-stu-id="78fbf-168">Publish with the dotnet CLI or nuget.exe CLI</span></span>

<span data-ttu-id="78fbf-169">CLI aracınızın sekmesini seçin, **yani .NET Core CLI** (dotnet CLI) veya **NuGet** (nuget.exe CLI).</span><span class="sxs-lookup"><span data-stu-id="78fbf-169">Select the tab for your CLI tool, either **.NET Core CLI** (dotnet CLI) or **NuGet** (nuget.exe CLI).</span></span>

# <a name="net-core-cli"></a>[<span data-ttu-id="78fbf-170">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="78fbf-170">.NET Core CLI</span></span>](#tab/netcore-cli)

<span data-ttu-id="78fbf-171">Bu adım kullanarak `nuget.exe`önerilen bir alternatiftir.</span><span class="sxs-lookup"><span data-stu-id="78fbf-171">This step is the recommended alternative to using `nuget.exe`.</span></span>

<span data-ttu-id="78fbf-172">Paketi yayımlamadan önce bir komut satırı açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="78fbf-172">Before you can publish the package, you must first open a command line.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

# <a name="nuget"></a>[<span data-ttu-id="78fbf-173">NuGet</span><span class="sxs-lookup"><span data-stu-id="78fbf-173">NuGet</span></span>](#tab/nuget)

<span data-ttu-id="78fbf-174">Bu adım kullanarak `dotnet.exe`bir alternatiftir.</span><span class="sxs-lookup"><span data-stu-id="78fbf-174">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="78fbf-175">Bir komut satırı açın ve dosyayı içeren klasöre değiştirin. `.nupkg`</span><span class="sxs-lookup"><span data-stu-id="78fbf-175">Open a command line and change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="78fbf-176">Paket adınızı (benzersiz paket kimliğinizi) belirterek ve anahtar değerini API anahtarınızla değiştirerek aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="78fbf-176">Run the following command, specifying your package name (unique package ID) and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="78fbf-177">nuget.exe yayımlama sürecinin sonuçlarını görüntüler:</span><span class="sxs-lookup"><span data-stu-id="78fbf-177">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="78fbf-178">Nuget [itme](../reference/cli-reference/cli-ref-push.md)bakın .</span><span class="sxs-lookup"><span data-stu-id="78fbf-178">See [nuget push](../reference/cli-reference/cli-ref-push.md).</span></span>

---

### <a name="publish-errors"></a><span data-ttu-id="78fbf-179">Hataları yayımlama</span><span class="sxs-lookup"><span data-stu-id="78fbf-179">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="78fbf-180">Yayımlanmış paketi yönetme</span><span class="sxs-lookup"><span data-stu-id="78fbf-180">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="78fbf-181">Okuma meme ve diğer dosyalar ekleme</span><span class="sxs-lookup"><span data-stu-id="78fbf-181">Adding a readme and other files</span></span>

<span data-ttu-id="78fbf-182">Pakete dahil olacak dosyaları doğrudan belirtmek için proje dosyasını edin ve `content` özelliği kullanın:</span><span class="sxs-lookup"><span data-stu-id="78fbf-182">To directly specify files to include in the package, edit the project file and use the `content` property:</span></span>

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

<span data-ttu-id="78fbf-183">Bu, paket kökünde adlı `readme.txt` bir dosya içerir.</span><span class="sxs-lookup"><span data-stu-id="78fbf-183">This will include a file named `readme.txt` in the package root.</span></span> <span data-ttu-id="78fbf-184">Visual Studio, paketi doğrudan yükledikten hemen sonra dosyanın içeriğini düz metin olarak görüntüler.</span><span class="sxs-lookup"><span data-stu-id="78fbf-184">Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="78fbf-185">(Bağımlılık olarak yüklenen paketler için Okuma dosyaları görüntülenmez).</span><span class="sxs-lookup"><span data-stu-id="78fbf-185">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="78fbf-186">Örneğin, HtmlAgilityPack paketinin okuma sı şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="78fbf-186">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Yükleme üzerine NuGet paketi için okuma dosyasının görüntülenmesi](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="78fbf-188">Proje köküne readme.txt eklenmesi, yalnızca ortaya çıkan pakete eklenmesine neden olmaz.</span><span class="sxs-lookup"><span data-stu-id="78fbf-188">Merely adding the readme.txt at the project root will not result in it being included in the resulting package.</span></span>

## <a name="related-video"></a><span data-ttu-id="78fbf-189">İlgili video</span><span class="sxs-lookup"><span data-stu-id="78fbf-189">Related video</span></span>

> [!Video https://channel9.msdn.com/Series/NuGet-101/Create-and-Publish-a-NuGet-Package-with-Visual-Studio-4-of-5/player]

<span data-ttu-id="78fbf-190">[Kanal 9](https://channel9.msdn.com/Series/NuGet-101) ve [YouTube'da](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_)daha fazla NuGet videosu bulun.</span><span class="sxs-lookup"><span data-stu-id="78fbf-190">Find more NuGet videos on [Channel 9](https://channel9.msdn.com/Series/NuGet-101) and [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span></span>

## <a name="related-topics"></a><span data-ttu-id="78fbf-191">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="78fbf-191">Related topics</span></span>

- [<span data-ttu-id="78fbf-192">Paket Oluşturma</span><span class="sxs-lookup"><span data-stu-id="78fbf-192">Create a Package</span></span>](../create-packages/creating-a-package-dotnet-cli.md)
- [<span data-ttu-id="78fbf-193">Paket Yayınlama</span><span class="sxs-lookup"><span data-stu-id="78fbf-193">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="78fbf-194">Ön Sürüm Paketleri</span><span class="sxs-lookup"><span data-stu-id="78fbf-194">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="78fbf-195">Birden çok hedef çerçeveyi destekleme</span><span class="sxs-lookup"><span data-stu-id="78fbf-195">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="78fbf-196">Paket sürüm</span><span class="sxs-lookup"><span data-stu-id="78fbf-196">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="78fbf-197">Yerelleştirilmiş paketler oluşturma</span><span class="sxs-lookup"><span data-stu-id="78fbf-197">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="78fbf-198">.NET Standart Kütüphane belgeleri</span><span class="sxs-lookup"><span data-stu-id="78fbf-198">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="78fbf-199">.NET Framework'den .NET Core'a taşıma</span><span class="sxs-lookup"><span data-stu-id="78fbf-199">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
