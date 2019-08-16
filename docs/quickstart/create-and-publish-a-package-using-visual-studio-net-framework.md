---
title: Windows üzerinde Visual Studio 'Yu kullanarak .NET Framework NuGet paketi oluşturma ve yayımlama
description: Windows üzerinde Visual Studio kullanarak .NET Framework NuGet paketi oluşturma ve yayımlama hakkında bir adım adım öğretici.
author: karann-msft
ms.author: karann
ms.date: 05/13/2018
ms.topic: quickstart
ms.openlocfilehash: 7bfe041c01114ac61e811497ecc31ebfdad45029
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488894"
---
# <a name="quickstart-create-and-publish-a-package-using-visual-studio-net-framework-windows"></a><span data-ttu-id="57011-103">Hızlı Başlangıç: Visual Studio (.NET Framework, Windows) kullanarak paket oluşturma ve yayımlama</span><span class="sxs-lookup"><span data-stu-id="57011-103">Quickstart: Create and publish a package using Visual Studio (.NET Framework, Windows)</span></span>

<span data-ttu-id="57011-104">Bir .NET Framework sınıf kitaplığından bir NuGet paketi oluşturmak, Windows üzerinde Visual Studio 'da DLL oluşturmayı, sonra da paketi oluşturmak ve yayımlamak için NuGet. exe komut satırı aracını kullanmayı içerir.</span><span class="sxs-lookup"><span data-stu-id="57011-104">Creating a NuGet package from a .NET Framework Class Library involves creating the DLL in Visual Studio on Windows, then using the nuget.exe command line tool to create and publish the package.</span></span>

> [!Note]
> <span data-ttu-id="57011-105">Bu hızlı başlangıç yalnızca Windows için Visual Studio 2017 için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="57011-105">This Quickstart applies to Visual Studio 2017 for Windows only.</span></span> <span data-ttu-id="57011-106">Mac için Visual Studio burada açıklanan özellikleri içermez.</span><span class="sxs-lookup"><span data-stu-id="57011-106">Visual Studio for Mac does not include the capabilities described here.</span></span> <span data-ttu-id="57011-107">Bunun yerine [DotNet CLI araçlarını](create-and-publish-a-package-using-the-dotnet-cli.md) kullanın.</span><span class="sxs-lookup"><span data-stu-id="57011-107">Use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md) instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57011-108">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="57011-108">Prerequisites</span></span>

1. <span data-ttu-id="57011-109">Herhangi bir Visual Studio 2017 sürümünü [VisualStudio.com](https://www.visualstudio.com/) adresinden yükleyin. NET ilgili iş yükü.</span><span class="sxs-lookup"><span data-stu-id="57011-109">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="57011-110">Visual Studio 2017, .NET iş yükü yüklendiğinde NuGet yeteneklerini otomatik olarak içerir.</span><span class="sxs-lookup"><span data-stu-id="57011-110">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="57011-111">[NuGet.org adresinden](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe)indirerek, bu `.exe` dosyayı uygun bir klasöre kaydederek ve bu klasörü PATH ortam değişkeninizden ekleyerek CLI'yıyükleme.`nuget.exe`</span><span class="sxs-lookup"><span data-stu-id="57011-111">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

1. <span data-ttu-id="57011-112">Henüz bir [hesabınız yoksa NuGet.org üzerinde ücretsiz bir hesaba kaydolun](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) .</span><span class="sxs-lookup"><span data-stu-id="57011-112">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="57011-113">Yeni hesap oluşturma onay e-postası gönderir.</span><span class="sxs-lookup"><span data-stu-id="57011-113">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="57011-114">Bir paketi karşıya yükleyebilmek için önce hesabı onaylamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="57011-114">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="57011-115">Sınıf kitaplığı projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="57011-115">Create a class library project</span></span>

<span data-ttu-id="57011-116">Paketlemek istediğiniz kod için mevcut bir .NET Framework sınıf kitaplığı projesini kullanabilir veya basit bir tane oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="57011-116">You can use an existing .NET Framework Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="57011-117">Visual Studio 'da **Dosya > Yeni > proje**' yi seçin, **görsel C#**  düğümü seçin, "sınıf kitaplığı (.NET Framework)" şablonunu seçin, projeyi appgünlükçü olarak adlandırın ve **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="57011-117">In Visual Studio, choose **File > New > Project**, select the **Visual C#** node, select the "Class Library (.NET Framework)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="57011-118">Ortaya çıkan proje dosyasına sağ tıklayın ve projenin düzgün oluşturulduğundan emin olmak için **Oluştur** ' u seçin.</span><span class="sxs-lookup"><span data-stu-id="57011-118">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="57011-119">DLL, hata ayıklama klasöründe bulunur (veya bunun yerine bu yapılandırmayı oluşturursanız sürüm).</span><span class="sxs-lookup"><span data-stu-id="57011-119">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="57011-120">Gerçek bir NuGet paketi içinde, diğerlerinin uygulama derleyebileceği birçok yararlı özelliği uygulayacağınızı görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="57011-120">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="57011-121">Hedef çerçeveleri de istediğiniz şekilde ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="57011-121">You can also set the target frameworks however you like.</span></span> <span data-ttu-id="57011-122">Örneğin, [UWP](../guides/create-uwp-packages.md) ve [Xamarin](../guides/create-packages-for-xamarin.md)kılavuzlarını inceleyin.</span><span class="sxs-lookup"><span data-stu-id="57011-122">For example, see the guides for [UWP](../guides/create-uwp-packages.md) and [Xamarin](../guides/create-packages-for-xamarin.md).</span></span>

<span data-ttu-id="57011-123">Ancak bu izlenecek yol için, şablondan bir sınıf kitaplığı bir paket oluşturmak için yeterli olduğundan ek kod yazmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="57011-123">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="57011-124">Hala, paket için bir işlev kodu isterseniz, aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="57011-124">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="57011-125">Aksi takdirde seçim yapmanız gerekmediğiniz sürece, en geniş kapsamlı proje yelpazğuyla uyumluluk sağladığından NuGet paketleri için tercih edilen hedef .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="57011-125">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="57011-126">Bkz. [Visual Studio kullanarak paket oluşturma ve yayımlama (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="57011-126">See [Create and publish a package using Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).</span></span>

## <a name="configure-project-properties-for-the-package"></a><span data-ttu-id="57011-127">Paket için proje özelliklerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="57011-127">Configure project properties for the package</span></span>

<span data-ttu-id="57011-128">Bir NuGet paketi, paket tanımlayıcısı, sürüm `.nuspec` numarası, açıklama ve daha fazlası gibi ilgili meta verileri içeren bir bildirim (dosya) içerir.</span><span class="sxs-lookup"><span data-stu-id="57011-128">A NuGet package contains a manifest (a `.nuspec` file), that contains relevant metadata such as the package identifier, version number, description, and more.</span></span> <span data-ttu-id="57011-129">Bunlardan bazıları proje özelliklerinden doğrudan çizilebilirler ve bu, hem projede hem de bildirimde ayrı ayrı güncelleştirilmesini önler.</span><span class="sxs-lookup"><span data-stu-id="57011-129">Some of these can be drawn from the project properties directly, which avoids having to separately update them in both the project and the manifest.</span></span> <span data-ttu-id="57011-130">Bu bölümde, uygulanabilir özelliklerin nerede ayarlanacağı açıklanır.</span><span class="sxs-lookup"><span data-stu-id="57011-130">This section describes where to set the applicable properties.</span></span>

1. <span data-ttu-id="57011-131">**Proje > Özellikler** menü komutunu seçin, sonra **uygulama** sekmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="57011-131">Select the **Project > Properties** menu command, then select the **Application** tab.</span></span>

1. <span data-ttu-id="57011-132">**Derleme adı** alanında, paketinize benzersiz bir tanımlayıcı verin.</span><span class="sxs-lookup"><span data-stu-id="57011-132">In the **Assembly name** field, give your package a unique identifier.</span></span>

    > [!Important]
    > <span data-ttu-id="57011-133">Pakete, nuget.org genelinde veya kullandığınız herhangi bir konakta benzersiz bir tanımlayıcı vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="57011-133">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="57011-134">Bu izlenecek yol için, "örnek" veya "test" adını, sonraki yayımlama adımı, paketi herkese açık hale getirir (ancak gerçekten onu kullanacağından çok fazla olabilir).</span><span class="sxs-lookup"><span data-stu-id="57011-134">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="57011-135">Zaten var olan bir ada sahip bir paketi yayımlamayı denerseniz, bir hata görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="57011-135">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="57011-136">Bildirimde bulunan diğer özellikleri girebileceğiniz bir iletişim kutusu getiren **derleme bilgileri...** düğmesini seçin (bkz [. nuspec dosya başvurusu-değiştirme belirteçleri](../reference/nuspec.md#replacement-tokens)).</span><span class="sxs-lookup"><span data-stu-id="57011-136">Select the **Assembly Information...** button, which brings up a dialog box in which you can enter other properties that carry into the manifest (see [.nuspec file reference - replacement tokens](../reference/nuspec.md#replacement-tokens)).</span></span> <span data-ttu-id="57011-137">En yaygın olarak kullanılan alanlar **başlık**, **Açıklama**, **Şirket**, **telif hakkı**ve **derleme sürümüdür**.</span><span class="sxs-lookup"><span data-stu-id="57011-137">The most commonly used fields are **Title**, **Description**, **Company**, **Copyright**, and **Assembly version**.</span></span> <span data-ttu-id="57011-138">Bu özellikler, nuget.org gibi bir konakta paket ile birlikte görüntülenir, bu nedenle tamamen açıklayıcı olduklarından emin olun.</span><span class="sxs-lookup"><span data-stu-id="57011-138">These properties ultimately appear with your package on a host like nuget.org, so make sure they're fully descriptive.</span></span>

    ![Visual Studio 'da bir .NET Framework projesindeki derleme bilgileri](media/qs_create-vs-01b-project-properties.png)

1. <span data-ttu-id="57011-140">İsteğe bağlı: özellikleri doğrudan görmek ve düzenlemek için `Properties/AssemblyInfo.cs` dosyayı projede açın.</span><span class="sxs-lookup"><span data-stu-id="57011-140">Optional: to see and edit the properties directly, open the `Properties/AssemblyInfo.cs` file in the project.</span></span>

1. <span data-ttu-id="57011-141">Özellikler ayarlandığında, proje yapılandırmasını **serbest bırak** olarak ayarlayın ve güncelleştirilmiş dll 'yi oluşturmak için projeyi yeniden derleyin.</span><span class="sxs-lookup"><span data-stu-id="57011-141">When the properties are set, set the project configuration to **Release** and rebuild the project to generate the updated DLL.</span></span>

## <a name="generate-the-initial-manifest"></a><span data-ttu-id="57011-142">Başlangıç bildirimini oluşturma</span><span class="sxs-lookup"><span data-stu-id="57011-142">Generate the initial manifest</span></span>

<span data-ttu-id="57011-143">Birlikte ve proje özellikleri ayarlanmış bir dll ile, bundan sonra projeden bir başlangıç `nuget spec` `.nuspec` dosyası oluşturmak için komutunu kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="57011-143">With a DLL in hand and project properties set, you now use the `nuget spec` command to generate an initial `.nuspec` file from the project.</span></span> <span data-ttu-id="57011-144">Bu adım, proje dosyasından bilgi çizmek için ilgili değiştirme belirteçlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="57011-144">This step includes the relevant replacement tokens to draw information from the project file.</span></span>

<span data-ttu-id="57011-145">İlk bildirimi `nuget spec` oluşturmak için yalnızca bir kez çalıştırırsınız.</span><span class="sxs-lookup"><span data-stu-id="57011-145">You run `nuget spec` only once to generate the initial manifest.</span></span> <span data-ttu-id="57011-146">Paketi güncelleştirirken, projenizdeki değerleri değiştirirsiniz ya da bildirimi doğrudan düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="57011-146">When updating the package, you either change values in your project or edit the manifest directly.</span></span>

1. <span data-ttu-id="57011-147">Bir komut istemi açın ve dosyayı içeren `AppLogger.csproj` proje klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="57011-147">Open a command prompt and navigate to the project folder containing `AppLogger.csproj` file.</span></span>

1. <span data-ttu-id="57011-148">Şu komutu çalıştırın: `nuget spec AppLogger.csproj`.</span><span class="sxs-lookup"><span data-stu-id="57011-148">Run the following command: `nuget spec AppLogger.csproj`.</span></span> <span data-ttu-id="57011-149">NuGet bir proje belirterek, bu durumda `AppLogger.nuspec`projenin adıyla eşleşen bir bildirim oluşturur.</span><span class="sxs-lookup"><span data-stu-id="57011-149">By specifying a project, NuGet creates a manifest that matches the name of the project, in this case `AppLogger.nuspec`.</span></span> <span data-ttu-id="57011-150">Ayrıca, bildirimde değiştirme belirteçleri de bulunur.</span><span class="sxs-lookup"><span data-stu-id="57011-150">It also include replacement tokens in the manifest.</span></span>

1. <span data-ttu-id="57011-151">İçeriğini `AppLogger.nuspec` incelemek için bir metin düzenleyicisinde açın ve aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="57011-151">Open `AppLogger.nuspec` in a text editor to examine its contents, which should appear as follows:</span></span>

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

## <a name="edit-the-manifest"></a><span data-ttu-id="57011-152">Bildirimi düzenleme</span><span class="sxs-lookup"><span data-stu-id="57011-152">Edit the manifest</span></span>

1. <span data-ttu-id="57011-153">`.nuspec` Dosyanızdaki varsayılan değerlerle bir paket oluşturmayı denerseniz NuGet bir hata oluşturur, bu nedenle devam etmeden önce aşağıdaki alanları düzenlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="57011-153">NuGet produces an error if you try to create a package with default values in your `.nuspec` file, so you must edit the following fields before proceeding.</span></span> <span data-ttu-id="57011-154">Bunların nasıl kullanıldığına ilişkin bir açıklama için bkz [. nuspec dosya başvurusu-isteğe bağlı meta veri öğeleri](../reference/nuspec.md#optional-metadata-elements) .</span><span class="sxs-lookup"><span data-stu-id="57011-154">See [.nuspec file reference - optional metadata elements](../reference/nuspec.md#optional-metadata-elements) for a description of how these are used.</span></span>

    - <span data-ttu-id="57011-155">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="57011-155">licenseUrl</span></span>
    - <span data-ttu-id="57011-156">projectUrl</span><span class="sxs-lookup"><span data-stu-id="57011-156">projectUrl</span></span>
    - <span data-ttu-id="57011-157">Iurl</span><span class="sxs-lookup"><span data-stu-id="57011-157">iconUrl</span></span>
    - <span data-ttu-id="57011-158">relet 'ler</span><span class="sxs-lookup"><span data-stu-id="57011-158">releaseNotes</span></span>
    - <span data-ttu-id="57011-159">etiketler</span><span class="sxs-lookup"><span data-stu-id="57011-159">tags</span></span>

1. <span data-ttu-id="57011-160">Genel kullanım için oluşturulmuş paketler için Etiketler özelliğine özel dikkat edin, Etiketler başkalarının paketinizi NuGet.org gibi kaynaklar üzerinde bulmasına yardımcı olur ve ne yaptığını anlayın.</span><span class="sxs-lookup"><span data-stu-id="57011-160">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package on sources like nuget.org and understand what it does.</span></span>

1. <span data-ttu-id="57011-161">Ayrıca, [. nuspec dosya başvurusu](../reference/nuspec.md)bölümünde açıklandığı gibi, şu anda bildirime başka öğeler de ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="57011-161">You can also add any other elements to the manifest at this time, as described on [.nuspec file reference](../reference/nuspec.md).</span></span>

1. <span data-ttu-id="57011-162">Devam etmeden önce dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="57011-162">Save the file before proceeding.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="57011-163">Pack komutunu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="57011-163">Run the pack command</span></span>

1. <span data-ttu-id="57011-164">`.nuspec` Dosyanızı içeren klasörde bir komut isteminden komutunu `nuget pack`çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="57011-164">From a command prompt in the folder containing your `.nuspec` file, run the command `nuget pack`.</span></span>

1. <span data-ttu-id="57011-165">NuGet, geçerli `.nupkg` klasörde bulacağınız *Identifier-Version. nupkg*biçiminde bir dosya oluşturur.</span><span class="sxs-lookup"><span data-stu-id="57011-165">NuGet generates a `.nupkg` file in the form of *identifier-version.nupkg*, which you'll find in the current folder.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="57011-166">Paketi Yayımla</span><span class="sxs-lookup"><span data-stu-id="57011-166">Publish the package</span></span>

<span data-ttu-id="57011-167">Bir `.nupkg` dosyaya sahip olduktan sonra, NuGet.org ' den alınan bir API `nuget.exe` anahtarı ile kullanarak NuGet.org 'e yayımlayabilirsiniz. NuGet.org için 4.1.0 veya üzeri `nuget.exe` bir sürümü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="57011-167">Once you have a `.nupkg` file, you publish it to nuget.org using `nuget.exe` with an API key acquired from nuget.org. For nuget.org you must use `nuget.exe` 4.1.0 or higher.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="57011-168">API anahtarınızı alın</span><span class="sxs-lookup"><span data-stu-id="57011-168">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="57011-169">NuGet Push ile yayımlama</span><span class="sxs-lookup"><span data-stu-id="57011-169">Publish with nuget push</span></span>

1. <span data-ttu-id="57011-170">Bir komut satırı açın ve `.nupkg` dosyayı içeren klasöre geçin.</span><span class="sxs-lookup"><span data-stu-id="57011-170">Open a command line and change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="57011-171">Aşağıdaki komutu çalıştırarak, paket adınızı belirtip anahtar değerini API anahtarınızla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="57011-171">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="57011-172">NuGet. exe yayımlama işleminin sonuçlarını görüntüler:</span><span class="sxs-lookup"><span data-stu-id="57011-172">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="57011-173">Bkz. [NuGet Push](../reference/cli-reference/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="57011-173">See [nuget push](../reference/cli-reference/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="57011-174">Yayımlama hataları</span><span class="sxs-lookup"><span data-stu-id="57011-174">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="57011-175">Yayınlanan paketi yönetme</span><span class="sxs-lookup"><span data-stu-id="57011-175">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="next-steps"></a><span data-ttu-id="57011-176">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="57011-176">Next steps</span></span>

<span data-ttu-id="57011-177">İlk NuGet paketinizi oluştururken Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="57011-177">Congratulations on creating your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="57011-178">Paket oluşturma</span><span class="sxs-lookup"><span data-stu-id="57011-178">Create a Package</span></span>](../create-packages/creating-a-package.md)

<span data-ttu-id="57011-179">NuGet 'in sunabileceği daha fazlasını araştırmak için aşağıdaki bağlantıları seçin.</span><span class="sxs-lookup"><span data-stu-id="57011-179">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="57011-180">Paket Yayımlama</span><span class="sxs-lookup"><span data-stu-id="57011-180">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="57011-181">Yayın öncesi paketler</span><span class="sxs-lookup"><span data-stu-id="57011-181">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="57011-182">Birden çok hedef çerçeveyi destekleme</span><span class="sxs-lookup"><span data-stu-id="57011-182">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="57011-183">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="57011-183">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="57011-184">Yerelleştirilmiş paketler oluşturma</span><span class="sxs-lookup"><span data-stu-id="57011-184">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
