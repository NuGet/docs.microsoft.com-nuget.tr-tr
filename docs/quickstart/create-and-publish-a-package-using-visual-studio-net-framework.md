---
title: Windows üzerinde Visual Studio kullanarak bir .NET Framework paketi oluşturma ve yayımlama
description: Oluşturma ve Windows üzerinde Visual Studio 2017'yi kullanarak bir .NET Framework NuGet Paketi Yayımlama Kılavuzu öğretici.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/13/2018
ms.topic: quickstart
ms.openlocfilehash: ffa2128b577673e980f4115f37f8685858c36250
ms.sourcegitcommit: 6cffa6ef59b922df2d87aa9c24034d00542983cd
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/10/2018
ms.locfileid: "37963165"
---
# <a name="quickstart-create-and-publish-a-package-using-visual-studio-net-framework-windows"></a><span data-ttu-id="354b8-103">Hızlı Başlangıç: Oluşturma ve Visual Studio (.NET Framework, Windows) kullanarak bir paket yayımlama</span><span class="sxs-lookup"><span data-stu-id="354b8-103">Quickstart: Create and publish a package using Visual Studio (.NET Framework, Windows)</span></span>

<span data-ttu-id="354b8-104">Windows üzerinde Visual Studio'da DLL'i oluşturmak ve ardından paketi oluşturma ve yayımlama için nuget.exe komut satırı aracını kullanarak bir .NET Framework Sınıf Kitaplığı'ndan bir NuGet paketi oluşturma içerir.</span><span class="sxs-lookup"><span data-stu-id="354b8-104">Creating a NuGet package from a .NET Framework Class Library involves creating the DLL in Visual Studio on Windows, then using the nuget.exe command line tool to create and publish the package.</span></span>

> [!Note]
> <span data-ttu-id="354b8-105">Bu hızlı başlangıçta, Visual Studio 2017'ye yalnızca Windows için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="354b8-105">This Quickstart applies to Visual Studio 2017 for Windows only.</span></span> <span data-ttu-id="354b8-106">Mac için Visual Studio, burada açıklanan özellikleri içermez.</span><span class="sxs-lookup"><span data-stu-id="354b8-106">Visual Studio for Mac does not include the capabilities described here.</span></span> <span data-ttu-id="354b8-107">Kullanım [dotnet CLI Araçları](create-and-publish-a-package-using-the-dotnet-cli.md) yerine.</span><span class="sxs-lookup"><span data-stu-id="354b8-107">Use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md) instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="354b8-108">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="354b8-108">Prerequisites</span></span>

1. <span data-ttu-id="354b8-109">Visual Studio 2017'den herhangi bir sürümünü yükleme [visualstudio.com](https://www.visualstudio.com/) herhangi. AĞ ile ilgili bir iş yükü.</span><span class="sxs-lookup"><span data-stu-id="354b8-109">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="354b8-110">.NET iş yükü yüklendiğinde visual Studio 2017, NuGet özellikleri otomatik olarak içerir.</span><span class="sxs-lookup"><span data-stu-id="354b8-110">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="354b8-111">Yükleme `nuget.exe` ondan indirerek CLI [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), kaydetme `.exe` uygun bir klasöre dosya ve klasörün PATH ortam değişkeninize ekleme.</span><span class="sxs-lookup"><span data-stu-id="354b8-111">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

1. <span data-ttu-id="354b8-112">[Nuget.org üzerindeki bir ücretsiz hesaba kaydolun](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) zaten yoksa.</span><span class="sxs-lookup"><span data-stu-id="354b8-112">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="354b8-113">Yeni bir hesap oluşturmadan bir onay e-posta gönderir.</span><span class="sxs-lookup"><span data-stu-id="354b8-113">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="354b8-114">Bir paketi karşıya yükleyebilmeniz, hesap onaylamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="354b8-114">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="354b8-115">Bir sınıf kitaplığı projesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="354b8-115">Create a class library project</span></span>

<span data-ttu-id="354b8-116">Mevcut bir .NET Framework sınıf kitaplığı projesi paketini veya basit bir şekilde oluşturmak istediğiniz kodu kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="354b8-116">You can use an existing .NET Framework Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="354b8-117">Visual Studio'da **Dosya > Yeni > Proje**seçin **Visual C#** düğümü, "Sınıf kitaplığı (.NET Framework)" şablonu seçin, AppLogger Projeyi adlandırın ve tıklayın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="354b8-117">In Visual Studio, choose **File > New > Project**, select the **Visual C#** node, select the "Class Library (.NET Framework)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="354b8-118">Sonuçta elde edilen proje dosyasını sağ tıklatın ve seçin **derleme** proje düzgün oluşturulduğu emin olmak için.</span><span class="sxs-lookup"><span data-stu-id="354b8-118">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="354b8-119">DLL hata ayıklama klasörü (veya bunun yerine, yapılandırma derleme yaparsanız sürüm) içinde bulunur.</span><span class="sxs-lookup"><span data-stu-id="354b8-119">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="354b8-120">Gerçek bir NuGet paketi içinde Elbette ile diğer uygulamaları oluşturabileceğiniz birçok yararlı özellik uygulayın.</span><span class="sxs-lookup"><span data-stu-id="354b8-120">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="354b8-121">Ancak, istediğiniz hedef çerçeveleri de ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="354b8-121">You can also set the target frameworks however you like.</span></span> <span data-ttu-id="354b8-122">Örneğin, kılavuzları için bkz. [UWP](../guides/create-uwp-packages.md) ve [Xamarin](../guides/create-packages-for-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="354b8-122">For example, see the guides for [UWP](../guides/create-uwp-packages.md) and [Xamarin](../guides/create-packages-for-xamarin.md).</span></span>

<span data-ttu-id="354b8-123">Şablon sınıf kitaplığından bir paketi oluşturmak yeterli olduğundan bu kılavuz için ancak herhangi bir ek kod yazmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="354b8-123">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="354b8-124">Yine de bazı işlevsel kod paketi için isterseniz aşağıdakini kullanın:</span><span class="sxs-lookup"><span data-stu-id="354b8-124">Still, if you'd like some functional code for the package, use the following:</span></span>

```cs
using System;

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
> <span data-ttu-id="354b8-125">Aksi takdirde seçmek için bir nedeniniz yoksa projeleri kullanan geniş kapsamlı uyumluluk sağlar .NET Standard NuGet paketlerini tercih edilen hedef aynıdır.</span><span class="sxs-lookup"><span data-stu-id="354b8-125">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="354b8-126">Bkz: [oluşturun ve Visual Studio (.NET Standard) kullanarak bir paket yayımlama](create-and-publish-a-package-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="354b8-126">See [Create and publish a package using Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).</span></span>

## <a name="configure-project-properties-for-the-package"></a><span data-ttu-id="354b8-127">Paket için proje özelliklerini yapılandır</span><span class="sxs-lookup"><span data-stu-id="354b8-127">Configure project properties for the package</span></span>

<span data-ttu-id="354b8-128">Bir NuGet paketi içeren bir bildirime (bir `.nuspec` dosyası), içeren uygulamanın paket tanımlayıcısı, sürüm numarası, açıklama ve diğer ilgili meta verileri.</span><span class="sxs-lookup"><span data-stu-id="354b8-128">A NuGet package contains a manifest (a `.nuspec` file), that contains relevant metadata such as the package identifier, version number, description, and more.</span></span> <span data-ttu-id="354b8-129">Bunların bazılarını, proje özellikleri doğrudan, hem proje hem de bildirim ayrı ayrı güncelleştirme gereğini ortadan kaldırır kurulabilir.</span><span class="sxs-lookup"><span data-stu-id="354b8-129">Some of these can be drawn from the project properties directly, which avoids having to separately update them in both the project and the manifest.</span></span> <span data-ttu-id="354b8-130">Bu bölümde, ilgili özellikleri ayarlamak nereye açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="354b8-130">This section describes where to set the applicable properties.</span></span>

1. <span data-ttu-id="354b8-131">Seçin **Proje > Özellikleri** menü komutunu ve ardından **uygulama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="354b8-131">Select the **Project > Properties** menu command, then select the **Application** tab.</span></span>

1. <span data-ttu-id="354b8-132">İçinde **derleme adı** alanında, benzersiz bir tanımlayıcı paketinizi verin.</span><span class="sxs-lookup"><span data-stu-id="354b8-132">In the **Assembly name** field, give your package a unique identifier.</span></span>

    > [!Important]
    > <span data-ttu-id="354b8-133">Nuget.org veya, konak arasında benzersiz bir tanımlayıcı kullanmakta olduğunuz paket vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="354b8-133">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="354b8-134">Bu kılavuz için (Bu herkes gerçekten kullanacağı olsa da) yayımlama sonraki adım paketi herkese görünür hale "Örnek" veya "Test" adı dahil olmak üzere öneririz.</span><span class="sxs-lookup"><span data-stu-id="354b8-134">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="354b8-135">Zaten bir ada sahip bir paketi yayımlamaya çalışırsanız, bir hata görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="354b8-135">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="354b8-136">Seçin **derleme bilgileri...**  içinde girebilirsiniz taşıyan diğer özellikleri bildirimine bir iletişim kutusu getirir düğmesini (bkz [.nuspec dosyası başvurusu - değiştirme belirteçleri](../reference/nuspec.md#replacement-tokens)).</span><span class="sxs-lookup"><span data-stu-id="354b8-136">Select the **Assembly Information...** button, which brings up a dialog box in which you can enter other properties that carry into the manifest (see [.nuspec file reference - replacement tokens](../reference/nuspec.md#replacement-tokens)).</span></span> <span data-ttu-id="354b8-137">En sık kullanılan alanlar **başlık**, **açıklama**, **şirket**, **telif hakkı**, ve **derlemesürümü**.</span><span class="sxs-lookup"><span data-stu-id="354b8-137">The most commonly used fields are **Title**, **Description**, **Company**, **Copyright**, and **Assembly version**.</span></span> <span data-ttu-id="354b8-138">Bu özellikler, nuget.org gibi bir konak üzerinde paket ile sonuçta görünür. Bu nedenle bunlar tamamen açıklayıcı olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="354b8-138">These properties ultimately appear with your package on a host like nuget.org, so make sure they're fully descriptive.</span></span>

    ![Visual Studio .NET Framework projede derleme bilgileri](media/qs_create-vs-01b-project-properties.png)

1. <span data-ttu-id="354b8-140">İsteğe bağlı: görmek ve doğrudan özelliklerini düzenlemek için açın `Properties/AssemblyInfo.cs` proje dosyasında.</span><span class="sxs-lookup"><span data-stu-id="354b8-140">Optional: to see and edit the properties directly, open the `Properties/AssemblyInfo.cs` file in the project.</span></span>

1. <span data-ttu-id="354b8-141">Özellikleri ayarladığınızda, proje yapılandırmasını ayarlayın **yayın** ve güncelleştirilmiş DLL'i oluşturmak için projeyi yeniden derleyin.</span><span class="sxs-lookup"><span data-stu-id="354b8-141">When the properties are set, set the project configuration to **Release** and rebuild the project to generate the updated DLL.</span></span>

## <a name="generate-the-initial-manifest"></a><span data-ttu-id="354b8-142">İlk bildirim oluştur</span><span class="sxs-lookup"><span data-stu-id="354b8-142">Generate the initial manifest</span></span>

<span data-ttu-id="354b8-143">Şimdi el ve proje özelliklerini kümesindeki bir DLL ile kullanmanız `nuget spec` bir ilk oluşturmak için komutu `.nuspec` proje dosyası.</span><span class="sxs-lookup"><span data-stu-id="354b8-143">With a DLL in hand and project properties set, you now use the `nuget spec` command to generate an initial `.nuspec` file from the project.</span></span> <span data-ttu-id="354b8-144">Bu adım, proje dosyasından bilgileri çizmek için ilgili değiştirme belirteçleri içerir.</span><span class="sxs-lookup"><span data-stu-id="354b8-144">This step includes the relevant replacement tokens to draw information from the project file.</span></span>

<span data-ttu-id="354b8-145">Çalıştırmadan `nuget spec` ilk bildirim oluşturmak üzere yalnızca bir kez.</span><span class="sxs-lookup"><span data-stu-id="354b8-145">You run `nuget spec` only once to generate the initial manifest.</span></span> <span data-ttu-id="354b8-146">Paketin güncelleştirilmesi, projenizde değerlerini değiştirmek veya doğrudan bildirimi düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="354b8-146">When updating the package, you either change values in your project or edit the manifest directly.</span></span>

1. <span data-ttu-id="354b8-147">Bir komut istemi açın ve projeyi içeren klasöre gidin `AppLogger.csproj` dosya.</span><span class="sxs-lookup"><span data-stu-id="354b8-147">Open a command prompt and navigate to the project folder containing `AppLogger.csproj` file.</span></span>

1. <span data-ttu-id="354b8-148">Aşağıdaki komutu çalıştırın: `nuget spec AppLogger.csproj`.</span><span class="sxs-lookup"><span data-stu-id="354b8-148">Run the following command: `nuget spec AppLogger.csproj`.</span></span> <span data-ttu-id="354b8-149">Bir proje belirterek, NuGet bu durumda proje adıyla eşleşen bir bildirim oluşturur `AppLogger.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="354b8-149">By specifying a project, NuGet creates a manifest that matches the name of the project, in this case `AppLogger.nuspec`.</span></span> <span data-ttu-id="354b8-150">Bunu de değiştirme belirteçleri bildiriminde.</span><span class="sxs-lookup"><span data-stu-id="354b8-150">It also include replacement tokens in the manifest.</span></span>

1. <span data-ttu-id="354b8-151">Açık `AppLogger.nuspec` içeriğini incelemek için bir metin düzenleyicisinde, aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="354b8-151">Open `AppLogger.nuspec` in a text editor to examine its contents, which should appear as follows:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
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
        <copyright>Copyright 2018</copyright>
        <tags>Tag1 Tag2</tags>
      </metadata>
    </package>
    ```

## <a name="edit-the-manifest"></a><span data-ttu-id="354b8-152">Bildirimi düzenleyin</span><span class="sxs-lookup"><span data-stu-id="354b8-152">Edit the manifest</span></span>

1. <span data-ttu-id="354b8-153">NuGet, varsayılan değerleri içeren bir paket oluşturmayı denerseniz bir hata üretir, `.nuspec` dosya için devam etmeden önce aşağıdaki alanları düzenlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="354b8-153">NuGet produces an error if you try to create a package with default values in your `.nuspec` file, so you must edit the following fields before proceeding.</span></span> <span data-ttu-id="354b8-154">Bkz: [.nuspec dosyası başvurusu - tek öğeleri](../reference/nuspec.md#single-elements) için bunların nasıl kullanıldığı bir açıklama.</span><span class="sxs-lookup"><span data-stu-id="354b8-154">See [.nuspec file reference - single elements](../reference/nuspec.md#single-elements) for a description of how these are used.</span></span>

    - <span data-ttu-id="354b8-155">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="354b8-155">licenseUrl</span></span>
    - <span data-ttu-id="354b8-156">projectUrl</span><span class="sxs-lookup"><span data-stu-id="354b8-156">projectUrl</span></span>
    - <span data-ttu-id="354b8-157">iconUrl</span><span class="sxs-lookup"><span data-stu-id="354b8-157">iconUrl</span></span>
    - <span data-ttu-id="354b8-158">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="354b8-158">releaseNotes</span></span>
    - <span data-ttu-id="354b8-159">etiketler</span><span class="sxs-lookup"><span data-stu-id="354b8-159">tags</span></span>

1. <span data-ttu-id="354b8-160">Ortak tüketim için oluşturulan paketler için özel dikkat **etiketleri** özelliği etiketleri diğerlerinin nuget.org gibi kaynaklar üzerinde paketinizi bulun ve ne yaptığını anlamanıza yardımcı olarak.</span><span class="sxs-lookup"><span data-stu-id="354b8-160">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package on sources like nuget.org and understand what it does.</span></span>

1. <span data-ttu-id="354b8-161">De diğer öğeleri için bildirim şu anda üzerinde açıklandığı ekleyebilirsiniz [.nuspec dosyası başvurusu](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="354b8-161">You can also add any other elements to the manifest at this time, as described on [.nuspec file reference](../reference/nuspec.md).</span></span>

1. <span data-ttu-id="354b8-162">Devam etmeden önce dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="354b8-162">Save the file before proceeding.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="354b8-163">Paketi komutunu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="354b8-163">Run the pack command</span></span>

1. <span data-ttu-id="354b8-164">İçeren klasörü içinde bir komut isteminden, `.nuspec` dosyası komutu Çalıştır `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="354b8-164">From a command prompt in the folder containing your `.nuspec` file, run the command `nuget pack`.</span></span>

1. <span data-ttu-id="354b8-165">NuGet oluşturur bir `.nupkg` dosya biçiminde *tanımlayıcı version.nupkg*, geçerli klasörde bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="354b8-165">NuGet generates a `.nupkg` file in the form of *identifier-version.nupkg*, which you'll find in the current folder.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="354b8-166">Paket yayımlama</span><span class="sxs-lookup"><span data-stu-id="354b8-166">Publish the package</span></span>

<span data-ttu-id="354b8-167">Sonra bir `.nupkg` dosyası yayımladığınızda, nuget.org kullanarak `nuget.exe` sahip bir API anahtarı nuget.org adresinden alındı. Nuget.org için kullanmanız gereken `nuget.exe` 4.1.0 veya üzeri.</span><span class="sxs-lookup"><span data-stu-id="354b8-167">Once you have a `.nupkg` file, you publish it to nuget.org using `nuget.exe` with an API key acquired from nuget.org. For nuget.org you must use `nuget.exe` 4.1.0 or higher.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="354b8-168">API anahtarınızı alma</span><span class="sxs-lookup"><span data-stu-id="354b8-168">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="354b8-169">Nuget itme ile yayımlama</span><span class="sxs-lookup"><span data-stu-id="354b8-169">Publish with nuget push</span></span>

1. <span data-ttu-id="354b8-170">Değiştirmek için içeren klasör `.nupkg` dosya.</span><span class="sxs-lookup"><span data-stu-id="354b8-170">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="354b8-171">Paketinizin adını belirterek ve API anahtarınızı anahtar değerini değiştirerek aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="354b8-171">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="354b8-172">nuget.exe yayımlama işleminin sonuçlarını görüntüler:</span><span class="sxs-lookup"><span data-stu-id="354b8-172">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="354b8-173">Bkz: [nuget anında iletme](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="354b8-173">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="354b8-174">Hataları yayımlama</span><span class="sxs-lookup"><span data-stu-id="354b8-174">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="354b8-175">Yayımlanan paket yönetme</span><span class="sxs-lookup"><span data-stu-id="354b8-175">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="354b8-176">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="354b8-176">Related topics</span></span>

- [<span data-ttu-id="354b8-177">Paket oluşturma</span><span class="sxs-lookup"><span data-stu-id="354b8-177">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="354b8-178">Paket Yayımlama</span><span class="sxs-lookup"><span data-stu-id="354b8-178">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="354b8-179">Yayın öncesi paketleri</span><span class="sxs-lookup"><span data-stu-id="354b8-179">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="354b8-180">Birden çok hedef çerçeve desteği</span><span class="sxs-lookup"><span data-stu-id="354b8-180">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="354b8-181">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="354b8-181">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="354b8-182">Yerelleştirilmiş paketler oluşturma</span><span class="sxs-lookup"><span data-stu-id="354b8-182">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
