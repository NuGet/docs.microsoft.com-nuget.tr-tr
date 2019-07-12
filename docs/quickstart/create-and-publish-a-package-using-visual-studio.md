---
title: Windows üzerinde Visual Studio kullanarak bir .NET Standard paketi oluşturma ve yayımlama
description: Oluşturma ve Windows üzerinde Visual Studio kullanarak bir standart .NET NuGet Paketi Yayımlama Kılavuzu öğretici.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: quickstart
ms.openlocfilehash: d9eccfa373a5a283542fd158e76ba74b1872f3d6
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842135"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a><span data-ttu-id="fa4b7-103">Hızlı Başlangıç: Visual Studio (.NET Standard, yalnızca Windows) kullanarak bir NuGet paketi oluşturma ve yayımlama</span><span class="sxs-lookup"><span data-stu-id="fa4b7-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard, Windows only)</span></span>

<span data-ttu-id="fa4b7-104">Bir .NET standart sınıf kitaplığı Windows üzerinde Visual Studio'da NuGet paketi oluşturun ve ardından bir CLI aracını kullanarak nuget.org için yayımlama için basit bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio on Windows, and then publish it to nuget.org using a CLI tool.</span></span>

> [!Note]
> <span data-ttu-id="fa4b7-105">Mac için Visual Studio kullanıyorsanız, başvurmak [bu bilgileri](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) üzerinde bir NuGet paketi oluşturuluyor veya kullanın [dotnet CLI Araçları](create-and-publish-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="fa4b7-105">If you are using Visual Studio for Mac, refer to [this information](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) on creating a NuGet package, or use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fa4b7-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="fa4b7-106">Prerequisites</span></span>

1. <span data-ttu-id="fa4b7-107">Visual Studio 2017 veya sonraki herhangi bir sürümünü yükleyin [visualstudio.com](https://www.visualstudio.com/) herhangi. AĞ ile ilgili bir iş yükü.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-107">Install any edition of Visual Studio 2017 or higher from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="fa4b7-108">Visual Studio 2017 ve üzeri otomatik olarak dahil NuGet özellikleri .NET iş yükü yüklendiğinde.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-108">Visual Studio 2017 and higher automatically include NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="fa4b7-109">Yükleme `dotnet` CLI.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-109">Install the `dotnet` CLI.</span></span>

   <span data-ttu-id="fa4b7-110">İçin `dotnet` CLI, Visual Studio 2017'den itibaren `dotnet` CLI herhangi bir .NET Core ile otomatik olarak yüklenen ilişkili iş yükleri.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-110">For the `dotnet` CLI, starting in Visual Studio 2017, the `dotnet` CLI is automatically installed with any .NET Core related workloads.</span></span> <span data-ttu-id="fa4b7-111">Aksi takdirde yükleme [.NET Core SDK'sı](https://www.microsoft.com/net/download/) almak için `dotnet` CLI.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-111">Otherwise, install the [.NET Core SDK](https://www.microsoft.com/net/download/) to get the `dotnet` CLI.</span></span> <span data-ttu-id="fa4b7-112">`dotnet` CLI kullanan .NET Standard projeleri için gerekli [SDK stilinde biçimi](../resources/check-project-format.md) (SDK'sı özniteliği).</span><span class="sxs-lookup"><span data-stu-id="fa4b7-112">The `dotnet` CLI is required for .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md) (SDK attribute).</span></span> <span data-ttu-id="fa4b7-113">Bu makalede kullanılan varsayılan sınıf kitaplığı şablonu Visual Studio 2017 ve üzeri SDK'sı özniteliğini kullanır.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-113">The default class library template in Visual Studio 2017 and higher, which is used in this article, uses the SDK attribute.</span></span>
   
   > [!Important]
   > <span data-ttu-id="fa4b7-114">Bu makalede `dotnet` CLI önerilir.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-114">For this article, the `dotnet` CLI is recommended.</span></span> <span data-ttu-id="fa4b7-115">Kullanarak herhangi bir NuGet paketi yayınlasa bile `nuget.exe` CLI, bu makaledeki adımlarda bazıları CLI dotnet SDK stili projeleri ile belirli.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-115">Although you can publish any NuGet package using the `nuget.exe` CLI, some of the steps in this article are specific to SDK-style projects and the dotnet CLI.</span></span> <span data-ttu-id="fa4b7-116">Nuget.exe CLI için kullanılan [SDK stili projeleri](../resources/check-project-format.md) (genellikle, .NET Framework).</span><span class="sxs-lookup"><span data-stu-id="fa4b7-116">The nuget.exe CLI is used for [non-SDK-style projects](../resources/check-project-format.md) (typically .NET Framework).</span></span> <span data-ttu-id="fa4b7-117">SDK stili projesiyle çalışıyorsanız konusundaki yordamları izleyin [oluşturun ve bir .NET Framework paketi (Visual Studio) yayımlama](create-and-publish-a-package-using-visual-studio-net-framework.md) paketi oluşturma ve yayımlama için.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-117">If you are working with a non-SDK-style project, follow the procedures in [Create and publish a .NET Framework package (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) to create and publish the package.</span></span>

1. <span data-ttu-id="fa4b7-118">[Nuget.org üzerindeki bir ücretsiz hesaba kaydolun](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account) zaten yoksa.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-118">[Register for a free account on nuget.org](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account) if you don't have one already.</span></span> <span data-ttu-id="fa4b7-119">Yeni bir hesap oluşturmadan bir onay e-posta gönderir.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-119">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="fa4b7-120">Bir paketi karşıya yükleyebilmeniz, hesap onaylamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-120">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="fa4b7-121">Bir sınıf kitaplığı projesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="fa4b7-121">Create a class library project</span></span>

<span data-ttu-id="fa4b7-122">Mevcut .NET standart sınıf kitaplığı projesinde paketini veya basit bir şekilde oluşturmak istediğiniz kodu kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fa4b7-122">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="fa4b7-123">Visual Studio'da **Dosya > Yeni > Proje**, genişletme **Visual C# > .NET Standard** düğümü, "Sınıf kitaplığı (.NET Standard)" şablonu seçin, AppLogger Projeyi adlandırın ve **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-123">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="fa4b7-124">Sonuçta elde edilen proje dosyasını sağ tıklatın ve seçin **derleme** proje düzgün oluşturulduğu emin olmak için.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-124">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="fa4b7-125">DLL hata ayıklama klasörü (veya bunun yerine, yapılandırma derleme yaparsanız sürüm) içinde bulunur.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-125">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="fa4b7-126">Gerçek bir NuGet paketi içinde Elbette ile diğer uygulamaları oluşturabileceğiniz birçok yararlı özellik uygulayın.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-126">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="fa4b7-127">Şablon sınıf kitaplığından bir paketi oluşturmak yeterli olduğundan bu kılavuz için ancak herhangi bir ek kod yazmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-127">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="fa4b7-128">Yine de bazı işlevsel kod paketi için isterseniz aşağıdakini kullanın:</span><span class="sxs-lookup"><span data-stu-id="fa4b7-128">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="fa4b7-129">Aksi takdirde seçmek için bir nedeniniz yoksa projeleri kullanan geniş kapsamlı uyumluluk sağlar .NET Standard NuGet paketlerini tercih edilen hedef aynıdır.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-129">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="fa4b7-130">Paket özelliklerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fa4b7-130">Configure package properties</span></span>

1. <span data-ttu-id="fa4b7-131">Çözüm Gezgini'nde projeye sağ tıklayıp seçin **özellikleri** menü komutunu ve ardından **paket** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-131">Right-click the project in Solution Explorer, and choose **Properties** menu command, then select the **Package** tab.</span></span>

   <span data-ttu-id="fa4b7-132">**Paket** sekmesi görünür yalnızca Visual Studio SDK stili projeleri için genellikle .NET Standard veya .NET Core sınıf kitaplığı projeleri; SDK olmayan stil projeyi (genellikle .NET Framework), ya da hedefliyorsanız [ Projeyi geçirmek](../reference/migrate-packages-config-to-package-reference.md) ve `dotnet` CLI, veya [oluştur ve .NET Framework paket yayımlama](create-and-publish-a-package-using-visual-studio-net-framework.md) veya bkz [oluştur ve .NET Framework paket yayımlama](create-and-publish-a-package-using-visual-studio-net-framework.md) bunun yerine için adım adım yönergeler.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-132">The **Package** tab appears only for SDK-style projects in Visual Studio, typically .NET Standard or .NET Core class library projects; if you are targeting a non-SDK style project (typically .NET Framework), either [migrate the project](../reference/migrate-packages-config-to-package-reference.md) and use `dotnet` CLI, or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

    ![Visual Studio projesinde NuGet paket özellikleri](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="fa4b7-134">Ortak tüketim için oluşturulan paketler için özel dikkat **etiketleri** özelliği olarak etiketler diğerlerinin paketinize bulun ve ne yaptığını anlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-134">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="fa4b7-135">Benzersiz bir tanımlayıcı paketinizi vermek ve diğer istenen özellikleri doldurun.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-135">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="fa4b7-136">Farklı özellikleri açıklaması için bkz: [.nuspec dosyası başvurusu](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="fa4b7-136">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="fa4b7-137">Burada tüm özellikler kısımlarda `.nuspec` Visual Studio projesi için oluşturduğu bildirimi.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-137">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="fa4b7-138">Nuget.org veya, konak arasında benzersiz bir tanımlayıcı kullanmakta olduğunuz paket vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-138">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="fa4b7-139">Bu kılavuz için (Bu herkes gerçekten kullanacağı olsa da) yayımlama sonraki adım paketi herkese görünür hale "Örnek" veya "Test" adı dahil olmak üzere öneririz.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-139">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="fa4b7-140">Zaten bir ada sahip bir paketi yayımlamaya çalışırsanız, bir hata görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-140">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="fa4b7-141">İsteğe bağlı: doğrudan proje dosyasındaki özellikleri görmek için Çözüm Gezgini'nde projeye sağ tıklayıp **Düzenle AppLogger.csproj**.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-141">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

   <span data-ttu-id="fa4b7-142">Bu seçenek, yalnızca SDK stilinde öznitelik kullanan projeler için Visual Studio 2017'de başlayarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-142">This option is only available starting in Visual Studio 2017 for projects that use the SDK-style attribute.</span></span> <span data-ttu-id="fa4b7-143">Aksi takdirde, projeye sağ tıklayıp seçin **projeyi**.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-143">Otherwise, right-click the project and choose **Unload Project**.</span></span> <span data-ttu-id="fa4b7-144">Ardından bellekten projeye sağ tıklayıp seçin **Düzenle AppLogger.csproj**.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-144">Then right-click the unloaded project and choose **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="fa4b7-145">Paketi komutunu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="fa4b7-145">Run the pack command</span></span>

1. <span data-ttu-id="fa4b7-146">Yapılandırmayı ayarlamak **yayın**.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-146">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="fa4b7-147">Projeye sağ tıklayın **Çözüm Gezgini** seçip **paketi** komutu:</span><span class="sxs-lookup"><span data-stu-id="fa4b7-147">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Visual Studio Proje bağlam menüsündeki NuGet Paketi komutu](media/qs_create-vs-02-pack-command.png)

    <span data-ttu-id="fa4b7-149">Görmüyorsanız **paketi** komutunu kullanmanız gerekir ve projenize SDK stilinde projesinde olan büyük olasılıkla `nuget.exe` CLI.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-149">If you don't see the **Pack** command, your project is probably not an SDK-style project and you need to use the `nuget.exe` CLI.</span></span> <span data-ttu-id="fa4b7-150">Ya da [projeyi geçirmek](../reference/migrate-packages-config-to-package-reference.md) ve `dotnet` CLI, veya [oluşturma ve bir .NET Framework Paketi Yayımlama](create-and-publish-a-package-using-visual-studio-net-framework.md) bunun yerine adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-150">Either [migrate the project](../reference/migrate-packages-config-to-package-reference.md) and use `dotnet` CLI, or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

1. <span data-ttu-id="fa4b7-151">Visual Studio projeyi derler ve oluşturur `.nupkg` dosya.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-151">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="fa4b7-152">İnceleme **çıkış** paketi dosyasının yolunu içeren pencere Ayrıntılar (aşağıdakine benzer).</span><span class="sxs-lookup"><span data-stu-id="fa4b7-152">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="fa4b7-153">Ayrıca derlemesi olduğunu unutmayın. `bin\Release\netstandard2.0` olarak neden önemli olduğuna .NET Standard 2.0 hedef.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-153">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a><span data-ttu-id="fa4b7-154">Diğer seçenek: MSBuild paketi</span><span class="sxs-lookup"><span data-stu-id="fa4b7-154">Alternate option: pack with MSBuild</span></span>

<span data-ttu-id="fa4b7-155">Kullanmaya alternatif olarak **paketi** menü komutu, NuGet 4.x+ ve MSBuild 15.1 + destekleyen bir `pack` hedef proje gerekli paket verilerini içerdiğinde.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-155">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="fa4b7-156">Bir komut istemi açın, proje klasörüne gidin ve aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-156">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="fa4b7-157">(MSBuild için gerekli tüm yolları ile yapılandırılacak gibi genellikle "Geliştirici komut istemi için Visual Studio" Başlat Menüsü'nden başlatmak istediğiniz.)</span><span class="sxs-lookup"><span data-stu-id="fa4b7-157">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

```cli
msbuild -t:pack -p:Configuration=Release
```

<span data-ttu-id="fa4b7-158">Paket ardından bulunabilir `bin\Release` klasör.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-158">The package can then be found in the `bin\Release` folder.</span></span>

<span data-ttu-id="fa4b7-159">Ek seçeneklerle için `msbuild -t:pack`, bkz: [NuGet paketi ve geri yükleme, MSBuild hedefleri](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="fa4b7-159">For additional options with `msbuild -t:pack`, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="fa4b7-160">Paket yayımlama</span><span class="sxs-lookup"><span data-stu-id="fa4b7-160">Publish the package</span></span>

<span data-ttu-id="fa4b7-161">Sonra bir `.nupkg` dosyası yayımladığınızda, kullanarak nuget.org için `nuget.exe` CLI veya `dotnet.exe` nuget.org adresinden alınan bir API anahtarı ile birlikte CLI.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-161">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="fa4b7-162">API anahtarınızı alma</span><span class="sxs-lookup"><span data-stu-id="fa4b7-162">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push-dotnet-cli"></a><span data-ttu-id="fa4b7-163">DotNet nuget itme (dotnet CLI) ile yayımlama</span><span class="sxs-lookup"><span data-stu-id="fa4b7-163">Publish with dotnet nuget push (dotnet CLI)</span></span>

<span data-ttu-id="fa4b7-164">Bu adım önerilen alternatifidir `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-164">This step is the recommended alternative to using `nuget.exe`.</span></span>

<span data-ttu-id="fa4b7-165">Paket yayımlayabilmeniz için önce bir komut satırı önce açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-165">Before you can publish the package, you must first open a command line.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-with-nuget-push-nugetexe-cli"></a><span data-ttu-id="fa4b7-166">Nuget anında iletme (nuget.exe CLI) ile yayımlama</span><span class="sxs-lookup"><span data-stu-id="fa4b7-166">Publish with nuget push (nuget.exe CLI)</span></span>

<span data-ttu-id="fa4b7-167">Bu adım bir alternatifidir `dotnet.exe`.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-167">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="fa4b7-168">Bir komut satırı açın ve değiştirmek için içeren klasör `.nupkg` dosya.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-168">Open a command line and change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="fa4b7-169">Paketinizin adını (benzersiz paket kimliği) belirtme ve API anahtarınızı anahtar değerini değiştirerek aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="fa4b7-169">Run the following command, specifying your package name (unique package ID) and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="fa4b7-170">nuget.exe yayımlama işleminin sonuçlarını görüntüler:</span><span class="sxs-lookup"><span data-stu-id="fa4b7-170">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="fa4b7-171">Bkz: [nuget anında iletme](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="fa4b7-171">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="fa4b7-172">Hataları yayımlama</span><span class="sxs-lookup"><span data-stu-id="fa4b7-172">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="fa4b7-173">Yayımlanan paket yönetme</span><span class="sxs-lookup"><span data-stu-id="fa4b7-173">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="fa4b7-174">Benioku ve diğer dosyaları ekleme</span><span class="sxs-lookup"><span data-stu-id="fa4b7-174">Adding a readme and other files</span></span>

<span data-ttu-id="fa4b7-175">Pakete dahil edilecek dosyalar doğrudan belirtmek için proje dosyasını düzenleyin ve kullanın `content` özelliği:</span><span class="sxs-lookup"><span data-stu-id="fa4b7-175">To directly specify files to include in the package, edit the project file and use the `content` property:</span></span>

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

<span data-ttu-id="fa4b7-176">Bu adlı bir dosya dahil eder `readme.txt` paket kökünde.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-176">This will include a file named `readme.txt` in the package root.</span></span> <span data-ttu-id="fa4b7-177">Visual Studio, hemen paket doğrudan yüklendikten sonra düz metin olarak bu dosyanın içeriğini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-177">Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="fa4b7-178">(Benioku dosyaları bağımlılıkların yüklü paketler için görüntülenmez).</span><span class="sxs-lookup"><span data-stu-id="fa4b7-178">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="fa4b7-179">Örneğin, işte HtmlAgilityPack paketinin Benioku dosyasını nasıl görünür:</span><span class="sxs-lookup"><span data-stu-id="fa4b7-179">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Yükleme sonrasında bir NuGet paketi için bir benioku dosyası görüntüsü](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="fa4b7-181">Yalnızca proje kök dizininde readme.txt ekleme sonuç paketine dahil açmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="fa4b7-181">Merely adding the readme.txt at the project root will not result in it being included in the resulting package.</span></span>

## <a name="related-topics"></a><span data-ttu-id="fa4b7-182">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="fa4b7-182">Related topics</span></span>

- [<span data-ttu-id="fa4b7-183">Paket oluşturma</span><span class="sxs-lookup"><span data-stu-id="fa4b7-183">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="fa4b7-184">Paket Yayımlama</span><span class="sxs-lookup"><span data-stu-id="fa4b7-184">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="fa4b7-185">Yayın öncesi paketleri</span><span class="sxs-lookup"><span data-stu-id="fa4b7-185">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="fa4b7-186">Birden çok hedef çerçeveyi destekleme</span><span class="sxs-lookup"><span data-stu-id="fa4b7-186">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="fa4b7-187">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="fa4b7-187">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="fa4b7-188">Yerelleştirilmiş paketler oluşturma</span><span class="sxs-lookup"><span data-stu-id="fa4b7-188">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="fa4b7-189">.NET standard kitaplığı belgeleri</span><span class="sxs-lookup"><span data-stu-id="fa4b7-189">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="fa4b7-190">.NET Core ile .NET Framework'ten taşıma</span><span class="sxs-lookup"><span data-stu-id="fa4b7-190">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
