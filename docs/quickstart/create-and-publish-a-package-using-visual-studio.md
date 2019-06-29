---
title: Windows üzerinde Visual Studio kullanarak bir .NET Standard paketi oluşturma ve yayımlama
description: Oluşturma ve Windows üzerinde Visual Studio 2017 kullanılarak bir standart .NET NuGet Paketi Yayımlama Kılavuzu öğretici.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: c75785d361f25564c8a59d7a2d85924c570a7b9a
ms.sourcegitcommit: b9a134a6e10d7d8502613f389f7d5f9b9e206ec8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67467809"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a><span data-ttu-id="ea9dd-103">Hızlı Başlangıç: Visual Studio (.NET Standard, yalnızca Windows) kullanarak bir NuGet paketi oluşturma ve yayımlama</span><span class="sxs-lookup"><span data-stu-id="ea9dd-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard, Windows only)</span></span>

<span data-ttu-id="ea9dd-104">Bir .NET standart sınıf kitaplığı Windows üzerinde Visual Studio'da NuGet paketi oluşturun ve ardından bir CLI aracını kullanarak nuget.org için yayımlama için basit bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="ea9dd-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio on Windows, and then publish it to nuget.org using a CLI tool.</span></span>

> [!Note]
> <span data-ttu-id="ea9dd-105">Bu hızlı başlangıçta, Visual Studio 2017'ye yalnızca Windows için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="ea9dd-105">This Quickstart applies to Visual Studio 2017 for Windows only.</span></span> <span data-ttu-id="ea9dd-106">Mac için Visual Studio, burada açıklanan özellikleri içermez.</span><span class="sxs-lookup"><span data-stu-id="ea9dd-106">Visual Studio for Mac does not include the capabilities described here.</span></span> <span data-ttu-id="ea9dd-107">Kullanım [dotnet CLI Araçları](create-and-publish-a-package-using-the-dotnet-cli.md) yerine.</span><span class="sxs-lookup"><span data-stu-id="ea9dd-107">Use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md) instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ea9dd-108">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="ea9dd-108">Prerequisites</span></span>

1. <span data-ttu-id="ea9dd-109">Visual Studio 2017'den herhangi bir sürümünü yükleme [visualstudio.com](https://www.visualstudio.com/) herhangi. AĞ ile ilgili bir iş yükü.</span><span class="sxs-lookup"><span data-stu-id="ea9dd-109">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="ea9dd-110">.NET iş yükü yüklendiğinde visual Studio 2017, NuGet özellikleri otomatik olarak içerir.</span><span class="sxs-lookup"><span data-stu-id="ea9dd-110">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="ea9dd-111">CLI araçlarından birini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ea9dd-111">Install one of the CLI tools.</span></span>

   * <span data-ttu-id="ea9dd-112">İçin `dotnet` CLI yükleme [.NET Core SDK'sı](https://www.microsoft.com/net/download/).</span><span class="sxs-lookup"><span data-stu-id="ea9dd-112">For the `dotnet` CLI, install the [.NET Core SDK](https://www.microsoft.com/net/download/).</span></span> <span data-ttu-id="ea9dd-113">Dotnet CLI SDK stilinde biçimini (SDK'sı özniteliği) kullanan .NET Standard projeleri için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="ea9dd-113">The dotnet CLI is required for .NET Standard projects that use the SDK-style format (SDK attribute).</span></span>

   * <span data-ttu-id="ea9dd-114">İçin `nuget.exe` CLI, indirdiği [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), kaydetme `.exe` uygun bir klasöre dosya ve klasörün PATH ortam değişkeninize ekleme.</span><span class="sxs-lookup"><span data-stu-id="ea9dd-114">For the `nuget.exe` CLI, download it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving the `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span> <span data-ttu-id="ea9dd-115">Nuget.exe CLI SDK stilinde olmayan biçimde .NET standart kitaplıkları için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ea9dd-115">The nuget.exe CLI is used for .NET Standard libraries in the non-SDK-style format.</span></span>

1. <span data-ttu-id="ea9dd-116">[Nuget.org üzerindeki bir ücretsiz hesaba kaydolun](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account) zaten yoksa.</span><span class="sxs-lookup"><span data-stu-id="ea9dd-116">[Register for a free account on nuget.org](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account) if you don't have one already.</span></span> <span data-ttu-id="ea9dd-117">Yeni bir hesap oluşturmadan bir onay e-posta gönderir.</span><span class="sxs-lookup"><span data-stu-id="ea9dd-117">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="ea9dd-118">Bir paketi karşıya yükleyebilmeniz, hesap onaylamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea9dd-118">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="ea9dd-119">Bir sınıf kitaplığı projesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="ea9dd-119">Create a class library project</span></span>

<span data-ttu-id="ea9dd-120">Mevcut .NET standart sınıf kitaplığı projesinde paketini veya basit bir şekilde oluşturmak istediğiniz kodu kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ea9dd-120">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="ea9dd-121">Visual Studio'da **Dosya > Yeni > Proje**, genişletme **Visual C# > .NET Standard** düğümü, "Sınıf kitaplığı (.NET Standard)" şablonu seçin, AppLogger Projeyi adlandırın ve **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="ea9dd-121">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="ea9dd-122">Sonuçta elde edilen proje dosyasını sağ tıklatın ve seçin **derleme** proje düzgün oluşturulduğu emin olmak için.</span><span class="sxs-lookup"><span data-stu-id="ea9dd-122">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="ea9dd-123">DLL hata ayıklama klasörü (veya bunun yerine, yapılandırma derleme yaparsanız sürüm) içinde bulunur.</span><span class="sxs-lookup"><span data-stu-id="ea9dd-123">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="ea9dd-124">Gerçek bir NuGet paketi içinde Elbette ile diğer uygulamaları oluşturabileceğiniz birçok yararlı özellik uygulayın.</span><span class="sxs-lookup"><span data-stu-id="ea9dd-124">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="ea9dd-125">Şablon sınıf kitaplığından bir paketi oluşturmak yeterli olduğundan bu kılavuz için ancak herhangi bir ek kod yazmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="ea9dd-125">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="ea9dd-126">Yine de bazı işlevsel kod paketi için isterseniz aşağıdakini kullanın:</span><span class="sxs-lookup"><span data-stu-id="ea9dd-126">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="ea9dd-127">Aksi takdirde seçmek için bir nedeniniz yoksa projeleri kullanan geniş kapsamlı uyumluluk sağlar .NET Standard NuGet paketlerini tercih edilen hedef aynıdır.</span><span class="sxs-lookup"><span data-stu-id="ea9dd-127">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="ea9dd-128">Paket özelliklerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ea9dd-128">Configure package properties</span></span>

1. <span data-ttu-id="ea9dd-129">Seçin **Proje > Özellikleri** menü komutunu ve ardından **paket** sekmesi. ( **Paket** .NET Framework hedefliyorsanız, yalnızca .NET Standard sınıf kitaplığı projeleri için; sekmesi görünür bkz [oluşturma ve bir .NET Framework Paketi Yayımlama](create-and-publish-a-package-using-visual-studio-net-framework.md) bunun yerine.</span><span class="sxs-lookup"><span data-stu-id="ea9dd-129">Select the **Project > Properties** menu command, then select the **Package** tab. (The **Package** tab appears only for .NET Standard class library projects; if you are targeting .NET Framework, see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead.</span></span> <span data-ttu-id="ea9dd-130">.NET Standard projesi görünmüyorsa, Visual Studio 2017 en son sürüme güncelleştirmeniz gerekebilir.)</span><span class="sxs-lookup"><span data-stu-id="ea9dd-130">If it doesn't appear for a .NET Standard project, you may need to update Visual Studio 2017 to the latest release.)</span></span>

    ![Visual Studio projesinde NuGet paket özellikleri](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="ea9dd-132">Ortak tüketim için oluşturulan paketler için özel dikkat **etiketleri** özelliği olarak etiketler diğerlerinin paketinize bulun ve ne yaptığını anlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="ea9dd-132">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="ea9dd-133">Benzersiz bir tanımlayıcı paketinizi vermek ve diğer istenen özellikleri doldurun.</span><span class="sxs-lookup"><span data-stu-id="ea9dd-133">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="ea9dd-134">Farklı özellikleri açıklaması için bkz: [.nuspec dosyası başvurusu](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="ea9dd-134">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="ea9dd-135">Burada tüm özellikler kısımlarda `.nuspec` Visual Studio projesi için oluşturduğu bildirimi.</span><span class="sxs-lookup"><span data-stu-id="ea9dd-135">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="ea9dd-136">Nuget.org veya, konak arasında benzersiz bir tanımlayıcı kullanmakta olduğunuz paket vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea9dd-136">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="ea9dd-137">Bu kılavuz için (Bu herkes gerçekten kullanacağı olsa da) yayımlama sonraki adım paketi herkese görünür hale "Örnek" veya "Test" adı dahil olmak üzere öneririz.</span><span class="sxs-lookup"><span data-stu-id="ea9dd-137">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="ea9dd-138">Zaten bir ada sahip bir paketi yayımlamaya çalışırsanız, bir hata görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="ea9dd-138">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="ea9dd-139">İsteğe bağlı: doğrudan proje dosyasındaki özellikleri görmek için Çözüm Gezgini'nde projeye sağ tıklayıp **Düzenle AppLogger.csproj**.</span><span class="sxs-lookup"><span data-stu-id="ea9dd-139">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="ea9dd-140">Paketi komutunu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="ea9dd-140">Run the pack command</span></span>

1. <span data-ttu-id="ea9dd-141">Yapılandırmayı ayarlamak **yayın**.</span><span class="sxs-lookup"><span data-stu-id="ea9dd-141">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="ea9dd-142">Projeye sağ tıklayın **Çözüm Gezgini** seçip **paketi** komutu:</span><span class="sxs-lookup"><span data-stu-id="ea9dd-142">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Visual Studio Proje bağlam menüsündeki NuGet Paketi komutu](media/qs_create-vs-02-pack-command.png)

1. <span data-ttu-id="ea9dd-144">Visual Studio projeyi derler ve oluşturur `.nupkg` dosya.</span><span class="sxs-lookup"><span data-stu-id="ea9dd-144">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="ea9dd-145">İnceleme **çıkış** paketi dosyasının yolunu içeren pencere Ayrıntılar (aşağıdakine benzer).</span><span class="sxs-lookup"><span data-stu-id="ea9dd-145">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="ea9dd-146">Ayrıca derlemesi olduğunu unutmayın. `bin\Release\netstandard2.0` olarak neden önemli olduğuna .NET Standard 2.0 hedef.</span><span class="sxs-lookup"><span data-stu-id="ea9dd-146">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a><span data-ttu-id="ea9dd-147">Diğer seçenek: MSBuild paketi</span><span class="sxs-lookup"><span data-stu-id="ea9dd-147">Alternate option: pack with MSBuild</span></span>

<span data-ttu-id="ea9dd-148">Kullanmaya alternatif olarak **paketi** menü komutu, NuGet 4.x+ ve MSBuild 15.1 + destekleyen bir `pack` hedef proje gerekli paket verilerini içerdiğinde.</span><span class="sxs-lookup"><span data-stu-id="ea9dd-148">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="ea9dd-149">Bir komut istemi açın, proje klasörüne gidin ve aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ea9dd-149">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="ea9dd-150">(MSBuild için gerekli tüm yolları ile yapılandırılacak gibi genellikle "Geliştirici komut istemi için Visual Studio" Başlat Menüsü'nden başlatmak istediğiniz.)</span><span class="sxs-lookup"><span data-stu-id="ea9dd-150">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

```cli
msbuild -t:pack -p:Configuration=Release
```

<span data-ttu-id="ea9dd-151">Paket ardından bulunabilir `bin\Release` klasör.</span><span class="sxs-lookup"><span data-stu-id="ea9dd-151">The package can then be found in the `bin\Release` folder.</span></span>

<span data-ttu-id="ea9dd-152">Ek seçeneklerle için `msbuild -t:pack`, bkz: [NuGet paketi ve geri yükleme, MSBuild hedefleri](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="ea9dd-152">For additional options with `msbuild -t:pack`, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="ea9dd-153">Paket yayımlama</span><span class="sxs-lookup"><span data-stu-id="ea9dd-153">Publish the package</span></span>

<span data-ttu-id="ea9dd-154">Sonra bir `.nupkg` dosyası yayımladığınızda, kullanarak nuget.org için `nuget.exe` CLI veya `dotnet.exe` nuget.org adresinden alınan bir API anahtarı ile birlikte CLI.</span><span class="sxs-lookup"><span data-stu-id="ea9dd-154">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="ea9dd-155">API anahtarınızı alma</span><span class="sxs-lookup"><span data-stu-id="ea9dd-155">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push-dotnet-cli"></a><span data-ttu-id="ea9dd-156">DotNet nuget itme (dotnet CLI) ile yayımlama</span><span class="sxs-lookup"><span data-stu-id="ea9dd-156">Publish with dotnet nuget push (dotnet CLI)</span></span>

<span data-ttu-id="ea9dd-157">Bu adım bir alternatifidir `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="ea9dd-157">This step is an alternative to using `nuget.exe`.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-with-nuget-push-nugetexe-cli"></a><span data-ttu-id="ea9dd-158">Nuget anında iletme (nuget.exe CLI) ile yayımlama</span><span class="sxs-lookup"><span data-stu-id="ea9dd-158">Publish with nuget push (nuget.exe CLI)</span></span>

<span data-ttu-id="ea9dd-159">Bu adım bir alternatifidir `dotnet.exe`.</span><span class="sxs-lookup"><span data-stu-id="ea9dd-159">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="ea9dd-160">Değiştirmek için içeren klasör `.nupkg` dosya.</span><span class="sxs-lookup"><span data-stu-id="ea9dd-160">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="ea9dd-161">Paketinizin adını belirterek ve API anahtarınızı anahtar değerini değiştirerek aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ea9dd-161">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="ea9dd-162">nuget.exe yayımlama işleminin sonuçlarını görüntüler:</span><span class="sxs-lookup"><span data-stu-id="ea9dd-162">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="ea9dd-163">Bkz: [nuget anında iletme](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="ea9dd-163">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="ea9dd-164">Hataları yayımlama</span><span class="sxs-lookup"><span data-stu-id="ea9dd-164">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="ea9dd-165">Yayımlanan paket yönetme</span><span class="sxs-lookup"><span data-stu-id="ea9dd-165">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="ea9dd-166">Benioku ve diğer dosyaları ekleme</span><span class="sxs-lookup"><span data-stu-id="ea9dd-166">Adding a readme and other files</span></span>

<span data-ttu-id="ea9dd-167">Pakete dahil edilecek dosyalar doğrudan belirtmek için proje dosyasını düzenleyin ve kullanın `content` özelliği:</span><span class="sxs-lookup"><span data-stu-id="ea9dd-167">To directly specify files to include in the package, edit the project file and use the `content` property:</span></span>

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

<span data-ttu-id="ea9dd-168">Bu adlı bir dosya dahil eder `readme.txt` paket kökünde.</span><span class="sxs-lookup"><span data-stu-id="ea9dd-168">This will include a file named `readme.txt` in the package root.</span></span> <span data-ttu-id="ea9dd-169">Visual Studio, hemen paket doğrudan yüklendikten sonra düz metin olarak bu dosyanın içeriğini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="ea9dd-169">Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="ea9dd-170">(Benioku dosyaları bağımlılıkların yüklü paketler için görüntülenmez).</span><span class="sxs-lookup"><span data-stu-id="ea9dd-170">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="ea9dd-171">Örneğin, işte HtmlAgilityPack paketinin Benioku dosyasını nasıl görünür:</span><span class="sxs-lookup"><span data-stu-id="ea9dd-171">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Yükleme sonrasında bir NuGet paketi için bir benioku dosyası görüntüsü](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="ea9dd-173">Yalnızca proje kök dizininde readme.txt ekleme sonuç paketine dahil açmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="ea9dd-173">Merely adding the readme.txt at the project root will not result in it being included in the resulting package.</span></span>

## <a name="related-topics"></a><span data-ttu-id="ea9dd-174">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="ea9dd-174">Related topics</span></span>

- [<span data-ttu-id="ea9dd-175">Paket oluşturma</span><span class="sxs-lookup"><span data-stu-id="ea9dd-175">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="ea9dd-176">Paket Yayımlama</span><span class="sxs-lookup"><span data-stu-id="ea9dd-176">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="ea9dd-177">Yayın öncesi paketleri</span><span class="sxs-lookup"><span data-stu-id="ea9dd-177">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="ea9dd-178">Birden çok hedef çerçeve desteği</span><span class="sxs-lookup"><span data-stu-id="ea9dd-178">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="ea9dd-179">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="ea9dd-179">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="ea9dd-180">Yerelleştirilmiş paketler oluşturma</span><span class="sxs-lookup"><span data-stu-id="ea9dd-180">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="ea9dd-181">.NET standard kitaplığı belgeleri</span><span class="sxs-lookup"><span data-stu-id="ea9dd-181">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="ea9dd-182">.NET Core ile .NET Framework'ten taşıma</span><span class="sxs-lookup"><span data-stu-id="ea9dd-182">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
