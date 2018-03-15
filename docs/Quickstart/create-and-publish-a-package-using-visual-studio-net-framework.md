---
title: "Oluşturma ve yayımlama Visual Studio kullanarak bir .NET Framework NuGet paketi tanıtım Kılavuzu | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/13/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Oluşturma ve yayımlama Visual Studio 2017 kullanarak bir .NET Framework NuGet paketi bir gözden geçirme Öğreticisi."
keywords: "NuGet paketini oluşturma, NuGet paketi yayımlama, NuGet öğretici, Visual Studio NuGet paketi, msbuild paketi oluşturma"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 613cb6e8cf5762f354d69aa271c1e2f0d4851c97
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/15/2018
---
# <a name="create-and-publish-a-package-using-visual-studio-net-framework"></a><span data-ttu-id="9e674-104">Oluşturma ve Visual Studio (.NET Framework) kullanarak bir paket yayımlama</span><span class="sxs-lookup"><span data-stu-id="9e674-104">Create and publish a package using Visual Studio (.NET Framework)</span></span>

<span data-ttu-id="9e674-105">Bir NuGet paketi bir .NET Framework Sınıf Kitaplığı'ndan Visual Studio'da DLL oluşturma ve ardından oluşturmak ve paket yayımlamak için nuget.exe komut satırı aracını kullanarak oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="9e674-105">Creating a NuGet package from a .NET Framework Class Library involves creating the DLL in Visual Studio, then using the nuget.exe command line tool to create and publish the package.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9e674-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="9e674-106">Prerequisites</span></span>

1. <span data-ttu-id="9e674-107">Visual Studio 2017 ' herhangi bir sürümünü yüklemek [visualstudio.com](https://www.visualstudio.com/) herhangi biriyle. NET ilgili iş yükü.</span><span class="sxs-lookup"><span data-stu-id="9e674-107">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="9e674-108">.NET iş yükü yüklendikten sonra visual Studio 2017 otomatik olarak NuGet yetenekleri içerir.</span><span class="sxs-lookup"><span data-stu-id="9e674-108">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="9e674-109">Yükleme `nuget.exe` buradan yükleyerek CLI [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), kaydetme `.exe` dosya için uygun bir klasör ve bu klasörü PATH ortam değişkenine ekleme.</span><span class="sxs-lookup"><span data-stu-id="9e674-109">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

1. <span data-ttu-id="9e674-110">[Kayıt nuget.org ücretsiz bir hesap için](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) zaten yoksa.</span><span class="sxs-lookup"><span data-stu-id="9e674-110">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="9e674-111">Yeni bir hesap oluşturmadan bir onay e-posta gönderir.</span><span class="sxs-lookup"><span data-stu-id="9e674-111">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="9e674-112">Bir paket karşıya yüklemeden önce hesap onaylamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9e674-112">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="9e674-113">Sınıf kitaplığı proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="9e674-113">Create a class library project</span></span>

<span data-ttu-id="9e674-114">Varolan bir .NET Framework sınıf kitaplığı proje paketini veya basit bir şekilde oluşturmak için istediğiniz kodu kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9e674-114">You can use an existing .NET Framework Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="9e674-115">Visual Studio'da, **Dosya > Yeni > Proje**seçin **Visual C#** düğümü, "Sınıf kitaplığı (.NET Framework)" şablonunu seçin, AppLogger proje adı ve tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="9e674-115">In Visual Studio, choose **File > New > Project**, select the **Visual C#** node, select the "Class Library (.NET Framework)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="9e674-116">Sonuçta elde edilen proje dosyasını sağ tıklatın ve seçin **yapı** projeyi düzgün bir şekilde oluşturuldu emin olmak için.</span><span class="sxs-lookup"><span data-stu-id="9e674-116">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="9e674-117">DLL Debug klasörüne (veya bunun yerine bu yapılandırma yapı sürüm) içinde bulunur.</span><span class="sxs-lookup"><span data-stu-id="9e674-117">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="9e674-118">Gerçek bir NuGet paketi içinde doğal olarak, çok sayıda kullanışlı özellikle ile diğer uygulamaları derleme uygulayın.</span><span class="sxs-lookup"><span data-stu-id="9e674-118">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="9e674-119">Ancak, istediğiniz bir hedef çerçeveyi de ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9e674-119">You can also set the target frameworks however you like.</span></span> <span data-ttu-id="9e674-120">Örneğin, bkz. kılavuzları için [UWP](../guides/create-uwp-packages.md) ve [Xamarin](../guides/create-packages-for-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="9e674-120">For example, see the guides for [UWP](../guides/create-uwp-packages.md) and [Xamarin](../guides/create-packages-for-xamarin.md).</span></span>

<span data-ttu-id="9e674-121">Bir sınıf kitaplığı şablondan bir paket oluşturmak yeterli olduğundan bu kılavuzda ancak, herhangi bir ek kod yazma olmaz.</span><span class="sxs-lookup"><span data-stu-id="9e674-121">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="9e674-122">Yine de, bazı işlevsel kod paketi için isterseniz, aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="9e674-122">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="9e674-123">Aksi takdirde seçmek için bir nedeniniz yoksa projeleri tüketen geniş kapsamlı bir uyum sağlar gibi .NET standart tercih edilen NuGet paketlerini hedefidir.</span><span class="sxs-lookup"><span data-stu-id="9e674-123">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="9e674-124">Bkz: [oluşturma ve Visual Studio (.NET standart) kullanarak bir paketi yayımlamaya](create-and-publish-a-package-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="9e674-124">See [Create and publish a package using Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).</span></span>

## <a name="configure-project-properties-for-the-package"></a><span data-ttu-id="9e674-125">Paket proje özelliklerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="9e674-125">Configure project properties for the package</span></span>

<span data-ttu-id="9e674-126">Bir NuGet paketi içeren bir bildirime (bir `.nuspec` dosyası), paket tanımlayıcısı, sürüm numarası, açıklama ve daha fazlası gibi ilgili meta veriler içeriyor.</span><span class="sxs-lookup"><span data-stu-id="9e674-126">A NuGet package contains a manifest (a `.nuspec` file), that contains relevant metadata such as the package identifier, version number, description, and more.</span></span> <span data-ttu-id="9e674-127">Bunlardan bazıları proje özellikleri doğrudan, hem proje hem de bildirim ayrı ayrı güncelleştirme gereğini ortadan kaldırır çizilebilir.</span><span class="sxs-lookup"><span data-stu-id="9e674-127">Some of these can be drawn from the project properties directly, which avoids having to separately update them in both the project and the manifest.</span></span> <span data-ttu-id="9e674-128">Bu bölümde ilgili özelliklerini ayarlamak nereye açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9e674-128">This section describes where to set the applicable properties.</span></span>

1. <span data-ttu-id="9e674-129">Seçin **Proje > Özellikler** menü komutunu ve ardından **uygulama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="9e674-129">Select the **Project > Properties** menu command, then select the **Application** tab.</span></span>

1. <span data-ttu-id="9e674-130">İçinde **derleme adı** alan, benzersiz bir tanımlayıcı paketinizi verin.</span><span class="sxs-lookup"><span data-stu-id="9e674-130">In the **Assembly name** field, give your package a unique identifier.</span></span>

    > [!Important]
    > <span data-ttu-id="9e674-131">Nuget.org veya ne olursa olsun, ana bilgisayar genelinde benzersiz bir tanımlayıcı kullanmakta olduğunuz paket vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9e674-131">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="9e674-132">Bu kılavuz için (Bu herkes gerçekte kullanacağı olsa da) sonraki yayımlama adım paketi herkese görünür hale "Sample" veya "Test" adı dahil olmak üzere öneririz.</span><span class="sxs-lookup"><span data-stu-id="9e674-132">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="9e674-133">Zaten bir ada sahip bir paketi yayımlamaya çalışırsanız, bir hata görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="9e674-133">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="9e674-134">Seçin **derleme bilgilerini...**  içinde girebilirsiniz taşımak diğer özellikleri bildirimine bir iletişim kutusu getirir düğmesi (bkz [.nuspec dosyası başvurusu - değiştirme belirteçleri](../reference/nuspec.md#replacement-tokens)).</span><span class="sxs-lookup"><span data-stu-id="9e674-134">Select the **Assembly Information...** button, which brings up a dialog box in which you can enter other properties that carry into the manifest (see [.nuspec file reference - replacement tokens](../reference/nuspec.md#replacement-tokens)).</span></span> <span data-ttu-id="9e674-135">En yaygın kullanılan alanları **başlık**, **açıklama**, **şirket**, **telif hakkı**, ve **derleme sürümü**.</span><span class="sxs-lookup"><span data-stu-id="9e674-135">The most commonly used fields are **Title**, **Description**, **Company**, **Copyright**, and **Assembly version**.</span></span> <span data-ttu-id="9e674-136">Bu özellikleri sonuçta paketinizi nuget.org gibi bir ana bilgisayarda görünür şekilde tam olarak açıklayıcı emin olun.</span><span class="sxs-lookup"><span data-stu-id="9e674-136">These properties ultimately appear with your package on a host like nuget.org, so make sure they're fully descriptive.</span></span>

    ![Visual Studio'da .NET Framework projesi derleme bilgileri](media/qs_create-vs-01b-project-properties.png)

1. <span data-ttu-id="9e674-138">İsteğe bağlı: görmek ve doğrudan özellikleri düzenlemek için açın `Properties/AssemblyInfo.cs` proje dosyasında.</span><span class="sxs-lookup"><span data-stu-id="9e674-138">Optional: to see and edit the properties directly, open the `Properties/AssemblyInfo.cs` file in the project.</span></span>

1. <span data-ttu-id="9e674-139">Özellikleri ayarladığınızda, proje yapılandırması kümesine **sürüm** ve güncelleştirilmiş DLL'sini üretmek için projeyi derleyin.</span><span class="sxs-lookup"><span data-stu-id="9e674-139">When the properties are set, set the project configuration to **Release** and rebuild the project to generate the updated DLL.</span></span>

## <a name="generate-the-initial-manifest"></a><span data-ttu-id="9e674-140">İlk bildirim oluşturmak</span><span class="sxs-lookup"><span data-stu-id="9e674-140">Generate the initial manifest</span></span>

<span data-ttu-id="9e674-141">Şimdi el ve proje özelliklerini kümesindeki bir DLL ile kullanmanız `nuget spec` bir ilk oluşturmak için komutu `.nuspec` proje dosyasından.</span><span class="sxs-lookup"><span data-stu-id="9e674-141">With a DLL in hand and project properties set, you now use the `nuget spec` command to generate an initial `.nuspec` file from the project.</span></span> <span data-ttu-id="9e674-142">Bu adım, proje dosyasından bilgileri çizmek için ilgili değiştirme belirteçleri içerir.</span><span class="sxs-lookup"><span data-stu-id="9e674-142">This step includes the relevant replacement tokens to draw information from the project file.</span></span>

<span data-ttu-id="9e674-143">Çalıştırmadan `nuget spec` ilk bildirimi oluşturmak için yalnızca bir kez.</span><span class="sxs-lookup"><span data-stu-id="9e674-143">You run `nuget spec` only once to generate the initial manifest.</span></span> <span data-ttu-id="9e674-144">Paket güncelleştirilirken projenizde değerlerini değiştirmek veya bildirim doğrudan düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="9e674-144">When updating the package, you either change values in your project or edit the manifest directly.</span></span>

1. <span data-ttu-id="9e674-145">Bir komut istemi açın ve projeyi içeren klasöre gidin `AppLogger.csproj` dosya.</span><span class="sxs-lookup"><span data-stu-id="9e674-145">Open a command prompt and navigate to the project folder containing `AppLogger.csproj` file.</span></span>

1. <span data-ttu-id="9e674-146">Aşağıdaki komutu çalıştırın: `nuget spec AppLogger.csproj`.</span><span class="sxs-lookup"><span data-stu-id="9e674-146">Run the following command: `nuget spec AppLogger.csproj`.</span></span> <span data-ttu-id="9e674-147">Bir proje belirterek, NuGet bu durumda proje adıyla eşleşen bir bildirim oluşturur `AppLogger.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="9e674-147">By specifying a project, NuGet creates a manifest that matches the name of the project, in this case `AppLogger.nuspec`.</span></span> <span data-ttu-id="9e674-148">Ayrıca dahil değiştirme belirteçleri bildiriminde.</span><span class="sxs-lookup"><span data-stu-id="9e674-148">It also include replacement tokens in the manifest.</span></span>

1. <span data-ttu-id="9e674-149">Açık `AppLogger.nuspec` içeriğini incelemek için bir metin Düzenleyicisi'nde, aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="9e674-149">Open `AppLogger.nuspec` in a text editor to examine its contents, which should appear as follows:</span></span>

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

## <a name="edit-the-manifest"></a><span data-ttu-id="9e674-150">Bildirim Düzenle</span><span class="sxs-lookup"><span data-stu-id="9e674-150">Edit the manifest</span></span>

1. <span data-ttu-id="9e674-151">NuGet üreten bir hata varsayılan değerleri içeren bir paket oluşturmayı denerseniz, `.nuspec` devam etmeden önce aşağıdaki alanları düzenlemek için dosya.</span><span class="sxs-lookup"><span data-stu-id="9e674-151">NuGet produces an error if you try to create a package with default values in your `.nuspec` file, so you must edit the following fields before proceeding.</span></span> <span data-ttu-id="9e674-152">Bkz: [.nuspec dosyası başvurusu - tek öğeleri](../reference/nuspec.md#single-elements) bunların nasıl kullanıldığı bir açıklaması için.</span><span class="sxs-lookup"><span data-stu-id="9e674-152">See [.nuspec file reference - single elements](../reference/nuspec.md#single-elements) for a description of how these are used.</span></span>

    - <span data-ttu-id="9e674-153">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="9e674-153">licenseUrl</span></span>
    - <span data-ttu-id="9e674-154">projectUrl</span><span class="sxs-lookup"><span data-stu-id="9e674-154">projectUrl</span></span>
    - <span data-ttu-id="9e674-155">iconUrl</span><span class="sxs-lookup"><span data-stu-id="9e674-155">iconUrl</span></span>
    - <span data-ttu-id="9e674-156">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="9e674-156">releaseNotes</span></span>
    - <span data-ttu-id="9e674-157">etiketler</span><span class="sxs-lookup"><span data-stu-id="9e674-157">tags</span></span>

1. <span data-ttu-id="9e674-158">Ortak tüketim için oluşturulan paketler için özellikle dikkat edin **etiketleri** özelliği gibi etiketler başkalarının nuget.org gibi kaynaklarında paketinizi bulun ve neler yaptığını anlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="9e674-158">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package on sources like nuget.org and understand what it does.</span></span>

1. <span data-ttu-id="9e674-159">Ayrıca diğer öğeleri bildirime şu anda açıklandığı gibi ekleyebileceğiniz [.nuspec dosyası başvurusu](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="9e674-159">You can also add any other elements to the manifest at this time, as described on [.nuspec file reference](../reference/nuspec.md).</span></span>

1. <span data-ttu-id="9e674-160">Devam etmeden önce dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="9e674-160">Save the file before proceeding.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="9e674-161">Paketi komutunu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="9e674-161">Run the pack command</span></span>

1. <span data-ttu-id="9e674-162">İçeren klasör, bir komut isteminden, `.nuspec` komutunu çalıştırın, dosyayı `nuget pack`.</span><span class="sxs-lookup"><span data-stu-id="9e674-162">From a command prompt in the folder containing your `.nuspec` file, run the command `nuget pack`.</span></span>

1. <span data-ttu-id="9e674-163">NuGet oluşturan bir `.nupkg` dosya biçiminde *tanımlayıcısı version.nupkg*, hangi geçerli klasörde bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="9e674-163">NuGet generates a `.nupkg` file in the form of *identifier-version.nupkg*, which you'll find in the current folder.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="9e674-164">Paket yayımlama</span><span class="sxs-lookup"><span data-stu-id="9e674-164">Publish the package</span></span>

<span data-ttu-id="9e674-165">Bulduktan sonra bir `.nupkg` dosyası, yayımlama, nuget.org kullanmaya `nuget.exe` bir API anahtarı ile nuget.org alınan. Nuget.org için kullanmanız gerekir `nuget.exe` 4.1.0'da ya da daha yüksek.</span><span class="sxs-lookup"><span data-stu-id="9e674-165">Once you have a `.nupkg` file, you publish it to nuget.org using `nuget.exe` with an API key acquired from nuget.org. For nuget.org you must use `nuget.exe` 4.1.0 or higher.</span></span>

[!INCLUDE[publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="9e674-166">API anahtarınızı edinin</span><span class="sxs-lookup"><span data-stu-id="9e674-166">Acquire your API key</span></span>

[!INCLUDE[publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="9e674-167">Nuget itme ile yayımlama</span><span class="sxs-lookup"><span data-stu-id="9e674-167">Publish with nuget push</span></span>

1. <span data-ttu-id="9e674-168">Değiştirmek için içeren klasör `.nupkg` dosya.</span><span class="sxs-lookup"><span data-stu-id="9e674-168">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="9e674-169">Paket adı belirtme ve API anahtarınızı anahtar değerini değiştirerek aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="9e674-169">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="9e674-170">nuget.exe yayımlama işleminin sonuçlarını görüntüler:</span><span class="sxs-lookup"><span data-stu-id="9e674-170">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="9e674-171">Bkz: [nuget itme](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="9e674-171">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="9e674-172">Hataları yayımlama</span><span class="sxs-lookup"><span data-stu-id="9e674-172">Publish errors</span></span>

[!INCLUDE[publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="9e674-173">Yayımlanan paket yönetme</span><span class="sxs-lookup"><span data-stu-id="9e674-173">Manage the published package</span></span>

[!INCLUDE[publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="9e674-174">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="9e674-174">Related topics</span></span>

- [<span data-ttu-id="9e674-175">Bir paket oluşturun</span><span class="sxs-lookup"><span data-stu-id="9e674-175">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="9e674-176">Paket Yayımlama</span><span class="sxs-lookup"><span data-stu-id="9e674-176">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="9e674-177">Birden çok hedef çerçeveyi desteği</span><span class="sxs-lookup"><span data-stu-id="9e674-177">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="9e674-178">Paket sürümü oluşturma</span><span class="sxs-lookup"><span data-stu-id="9e674-178">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="9e674-179">Yerelleştirilmiş paketler oluşturma</span><span class="sxs-lookup"><span data-stu-id="9e674-179">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
