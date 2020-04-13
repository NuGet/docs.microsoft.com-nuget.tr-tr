---
title: Windows'da Visual Studio'u kullanarak bir .NET Framework NuGet paketi oluşturun ve yayımlayın
description: Windows'da Visual Studio'u kullanarak bir .NET Framework NuGet paketi oluşturma ve yayımlama hakkında bir iz geçidi öğretici.
author: karann-msft
ms.author: karann
ms.date: 05/13/2018
ms.topic: quickstart
ms.openlocfilehash: e00aac83a710e2f745d5e4bb9aec741ee686e595
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "72380639"
---
# <a name="quickstart-create-and-publish-a-package-using-visual-studio-net-framework-windows"></a><span data-ttu-id="66ba8-103">Quickstart: Visual Studio (.NET Framework, Windows) kullanarak bir paket oluşturun ve yayımlayın</span><span class="sxs-lookup"><span data-stu-id="66ba8-103">Quickstart: Create and publish a package using Visual Studio (.NET Framework, Windows)</span></span>

<span data-ttu-id="66ba8-104">.NET Framework Class Kitaplığı'ndan bir NuGet paketi oluşturmak, Windows'da Visual Studio'da DLL oluşturmayı ve paketi oluşturmak ve yayımlamak için nuget.exe komut satırı aracını kullanmayı içerir.</span><span class="sxs-lookup"><span data-stu-id="66ba8-104">Creating a NuGet package from a .NET Framework Class Library involves creating the DLL in Visual Studio on Windows, then using the nuget.exe command line tool to create and publish the package.</span></span>

> [!Note]
> <span data-ttu-id="66ba8-105">Bu Quickstart Visual Studio 2017 ve yalnızca Windows için daha yüksek sürümler için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="66ba8-105">This Quickstart applies to Visual Studio 2017 and higher versions for Windows only.</span></span> <span data-ttu-id="66ba8-106">Mac için Visual Studio burada açıklanan yetenekleri içermez.</span><span class="sxs-lookup"><span data-stu-id="66ba8-106">Visual Studio for Mac does not include the capabilities described here.</span></span> <span data-ttu-id="66ba8-107">Bunun yerine [dotnet CLI araçlarını](create-and-publish-a-package-using-the-dotnet-cli.md) kullanın.</span><span class="sxs-lookup"><span data-stu-id="66ba8-107">Use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md) instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66ba8-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="66ba8-108">Prerequisites</span></span>

1. <span data-ttu-id="66ba8-109">Visual Studio 2017 veya daha yüksek herhangi bir sürümünü [visualstudio.com](https://www.visualstudio.com/) herhangi bir . NET ile ilgili iş yükü.</span><span class="sxs-lookup"><span data-stu-id="66ba8-109">Install any edition of Visual Studio 2017 or higher from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="66ba8-110">Visual Studio 2017, bir .NET iş yükü yüklendiğinde NuGet özelliklerini otomatik olarak içerir.</span><span class="sxs-lookup"><span data-stu-id="66ba8-110">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="66ba8-111">CLI'yi `nuget.exe` [nuget.org'dan](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe)indirerek yükleyin, dosyayı `.exe` uygun bir klasöre kaydedin ve bu klasörü PATH ortamı değişkeninize eklediniz.</span><span class="sxs-lookup"><span data-stu-id="66ba8-111">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

1. <span data-ttu-id="66ba8-112">Zaten bir hesabınız yoksa [nuget.org ücretsiz bir hesaba kaydolun.](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)</span><span class="sxs-lookup"><span data-stu-id="66ba8-112">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="66ba8-113">Yeni bir hesap oluşturmak bir onay e-postası gönderir.</span><span class="sxs-lookup"><span data-stu-id="66ba8-113">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="66ba8-114">Bir paket yükleyemeden önce hesabı onaylamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="66ba8-114">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="66ba8-115">Sınıf kitaplığı projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="66ba8-115">Create a class library project</span></span>

<span data-ttu-id="66ba8-116">Paketlemek istediğiniz kod için varolan bir .NET Framework Class Kitaplığı projesini kullanabilir veya aşağıdaki gibi basit bir kitap oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="66ba8-116">You can use an existing .NET Framework Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="66ba8-117">Visual **Studio'da, Dosya > Yeni > Projesi'ni**seçin, **Visual C#** düğümünü seçin, "Sınıf Kitaplığı (.NET Framework)" şablonuna tıklayın, proje AppLogger'ı adlandırın ve **Tamam'ı**tıklatın.</span><span class="sxs-lookup"><span data-stu-id="66ba8-117">In Visual Studio, choose **File > New > Project**, select the **Visual C#** node, select the "Class Library (.NET Framework)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="66ba8-118">Projenin düzgün oluşturulduğundan emin olmak için ortaya çıkan proje dosyasına sağ tıklayın ve **Yapı'yı** seçin.</span><span class="sxs-lookup"><span data-stu-id="66ba8-118">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="66ba8-119">DLL Hata Ayıklama klasöründe bulunur (veya bu yapılandırmayı oluşturursanız serbest bırakın).</span><span class="sxs-lookup"><span data-stu-id="66ba8-119">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="66ba8-120">Gerçek bir NuGet paketi içinde, tabii ki, başkalarının uygulamaları oluşturabilirsiniz birçok yararlı özellikleri uygulamak.</span><span class="sxs-lookup"><span data-stu-id="66ba8-120">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="66ba8-121">Hedef çerçeveleri istediğiniz gibi de ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66ba8-121">You can also set the target frameworks however you like.</span></span> <span data-ttu-id="66ba8-122">Örneğin, [UWP](../guides/create-uwp-packages.md) ve [Xamarin](../guides/create-packages-for-xamarin.md)kılavuzlarına bakın.</span><span class="sxs-lookup"><span data-stu-id="66ba8-122">For example, see the guides for [UWP](../guides/create-uwp-packages.md) and [Xamarin](../guides/create-packages-for-xamarin.md).</span></span>

<span data-ttu-id="66ba8-123">Ancak bu geçiş için, şablondan bir sınıf kitaplığı bir paket oluşturmak için yeterli olduğundan, ek kod yazmazsınız.</span><span class="sxs-lookup"><span data-stu-id="66ba8-123">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="66ba8-124">Yine de, paket için bazı işlevsel kod istiyorsanız, aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="66ba8-124">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="66ba8-125">Aksini seçmek için bir nedeniniz yoksa, .NET Standard, en geniş tüketici proje yelpazesiyle uyumluluk sağladığından NuGet paketleri için tercih edilen hedeftir.</span><span class="sxs-lookup"><span data-stu-id="66ba8-125">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="66ba8-126">Bkz. [Visual Studio (.NET Standard) kullanarak bir paket oluşturun ve yayımlayın.](create-and-publish-a-package-using-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="66ba8-126">See [Create and publish a package using Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).</span></span>

## <a name="configure-project-properties-for-the-package"></a><span data-ttu-id="66ba8-127">Paket için proje özelliklerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="66ba8-127">Configure project properties for the package</span></span>

<span data-ttu-id="66ba8-128">NuGet paketi, paket tanımlayıcısı, sürüm numarası, açıklama ve daha fazlası gibi ilgili meta verileri içeren bir bildirim `.nuspec` (dosya) içerir.</span><span class="sxs-lookup"><span data-stu-id="66ba8-128">A NuGet package contains a manifest (a `.nuspec` file), that contains relevant metadata such as the package identifier, version number, description, and more.</span></span> <span data-ttu-id="66ba8-129">Bunlardan bazıları doğrudan proje özelliklerinden çıkarılabilir, bu da bunları hem projede hem de bildirimde ayrı ayrı güncelleştirmekten kaçınır.</span><span class="sxs-lookup"><span data-stu-id="66ba8-129">Some of these can be drawn from the project properties directly, which avoids having to separately update them in both the project and the manifest.</span></span> <span data-ttu-id="66ba8-130">Bu bölümde, ilgili özelliklerin nerede ayarlandığı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="66ba8-130">This section describes where to set the applicable properties.</span></span>

1. <span data-ttu-id="66ba8-131">Project **> Properties** menüsü komutunu seçin ve ardından **Uygulama** sekmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="66ba8-131">Select the **Project > Properties** menu command, then select the **Application** tab.</span></span>

1. <span data-ttu-id="66ba8-132">Assembly **ad** alanında, paketinize benzersiz bir tanımlayıcı verin.</span><span class="sxs-lookup"><span data-stu-id="66ba8-132">In the **Assembly name** field, give your package a unique identifier.</span></span>

    > [!Important]
    > <span data-ttu-id="66ba8-133">Pakete, nuget.org veya kullandığınız ana bilgisayarda benzersiz bir tanımlayıcı vermelisiniz.</span><span class="sxs-lookup"><span data-stu-id="66ba8-133">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="66ba8-134">Bu izlenecek yol için, daha sonraki yayımlama adımı paketi herkese açık hale getirebildiğinden (kimsenin gerçekten kullanması pek olası olmasa da) adına "Örnek" veya "Test" eklenmesini öneririz.</span><span class="sxs-lookup"><span data-stu-id="66ba8-134">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="66ba8-135">Zaten var olan bir ada sahip bir paketi yayımlamaya çalışırsanız, bir hata görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="66ba8-135">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="66ba8-136">Bildirime giren diğer özellikleri girebileceğiniz bir iletişim kutusu oluşturan **Derleme Bilgileri...** düğmesini seçin (bkz. [.nuspec dosya başvurusu - değiştirme belirteçleri).](../reference/nuspec.md#replacement-tokens)</span><span class="sxs-lookup"><span data-stu-id="66ba8-136">Select the **Assembly Information...** button, which brings up a dialog box in which you can enter other properties that carry into the manifest (see [.nuspec file reference - replacement tokens](../reference/nuspec.md#replacement-tokens)).</span></span> <span data-ttu-id="66ba8-137">En sık kullanılan alanlar **Başlık**, **Açıklama**, **Şirket**, **Telif Hakkı**ve Montaj **sürümü.**</span><span class="sxs-lookup"><span data-stu-id="66ba8-137">The most commonly used fields are **Title**, **Description**, **Company**, **Copyright**, and **Assembly version**.</span></span> <span data-ttu-id="66ba8-138">Bu özellikler sonuçta paketiniz nuget.org gibi bir ana bilgisayarda görünür, bu nedenle tamamen açıklayıcı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="66ba8-138">These properties ultimately appear with your package on a host like nuget.org, so make sure they're fully descriptive.</span></span>

    ![Visual Studio'da bir .NET Framework projesinde montaj bilgileri](media/qs_create-vs-01b-project-properties.png)

1. <span data-ttu-id="66ba8-140">İsteğe bağlı: Özellikleri doğrudan görmek ve `Properties/AssemblyInfo.cs` denetlemek için projedeki dosyayı açın.</span><span class="sxs-lookup"><span data-stu-id="66ba8-140">Optional: to see and edit the properties directly, open the `Properties/AssemblyInfo.cs` file in the project.</span></span>

1. <span data-ttu-id="66ba8-141">Özellikler ayarlandığında, proje yapılandırmasını **Release'e** ayarlayın ve güncelleştirilmiş DLL'yi oluşturmak için projeyi yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="66ba8-141">When the properties are set, set the project configuration to **Release** and rebuild the project to generate the updated DLL.</span></span>

## <a name="generate-the-initial-manifest"></a><span data-ttu-id="66ba8-142">İlk bildirimi oluşturma</span><span class="sxs-lookup"><span data-stu-id="66ba8-142">Generate the initial manifest</span></span>

<span data-ttu-id="66ba8-143">Elinde bir DLL ve proje özellikleri kümesi `nuget spec` yle, artık `.nuspec` projeden bir başlangıç dosyası oluşturmak için komutu kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="66ba8-143">With a DLL in hand and project properties set, you now use the `nuget spec` command to generate an initial `.nuspec` file from the project.</span></span> <span data-ttu-id="66ba8-144">Bu adım, proje dosyasından bilgi çekmek için ilgili değiştirme belirteçlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="66ba8-144">This step includes the relevant replacement tokens to draw information from the project file.</span></span>

<span data-ttu-id="66ba8-145">İlk `nuget spec` bildirimi oluşturmak için yalnızca bir kez çalışırsınız.</span><span class="sxs-lookup"><span data-stu-id="66ba8-145">You run `nuget spec` only once to generate the initial manifest.</span></span> <span data-ttu-id="66ba8-146">Paketi güncellerken, projenizdeki değerleri değiştirir veya doğrudan bildirimi değiştirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66ba8-146">When updating the package, you either change values in your project or edit the manifest directly.</span></span>

1. <span data-ttu-id="66ba8-147">Komut istemini açın ve dosya `AppLogger.csproj` içeren proje klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="66ba8-147">Open a command prompt and navigate to the project folder containing `AppLogger.csproj` file.</span></span>

1. <span data-ttu-id="66ba8-148">Aşağıdaki komutu `nuget spec AppLogger.csproj`çalıştırın: .</span><span class="sxs-lookup"><span data-stu-id="66ba8-148">Run the following command: `nuget spec AppLogger.csproj`.</span></span> <span data-ttu-id="66ba8-149">NuGet, bir proje belirterek, bu durumda `AppLogger.nuspec`projenin adı ile eşleşen bir bildirim oluşturur.</span><span class="sxs-lookup"><span data-stu-id="66ba8-149">By specifying a project, NuGet creates a manifest that matches the name of the project, in this case `AppLogger.nuspec`.</span></span> <span data-ttu-id="66ba8-150">Ayrıca, bildirimde yedek belirteçler de içerir.</span><span class="sxs-lookup"><span data-stu-id="66ba8-150">It also include replacement tokens in the manifest.</span></span>

1. <span data-ttu-id="66ba8-151">`AppLogger.nuspec` Aşağıdaki gibi görünmesi gereken içeriğini incelemek için bir metin düzenleyicisi açın:</span><span class="sxs-lookup"><span data-stu-id="66ba8-151">Open `AppLogger.nuspec` in a text editor to examine its contents, which should appear as follows:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
      <metadata>
        <id>Package</id>
        <version>1.0.0</version>
        <authors>YourUsername</authors>
        <owners>YourUsername</owners>
        <license type="expression">MIT</license>
        <projectUrl>http://PROJECT_URL_HERE_OR_DELETE_THIS_LINE</projectUrl>
        <iconUrl>http://ICON_URL_HERE_OR_DELETE_THIS_LINE</iconUrl>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Package description</description>
        <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
        <copyright>Copyright 2019</copyright>
        <tags>Tag1 Tag2</tags>
      </metadata>
    </package>
    ```

## <a name="edit-the-manifest"></a><span data-ttu-id="66ba8-152">Bildirimi edin</span><span class="sxs-lookup"><span data-stu-id="66ba8-152">Edit the manifest</span></span>

1. <span data-ttu-id="66ba8-153">NuGet, dosyanızda `.nuspec` varsayılan değerler içeren bir paket oluşturmaya çalışırsanız bir hata oluşturur, bu nedenle devam etmeden önce aşağıdaki alanları yeniden oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="66ba8-153">NuGet produces an error if you try to create a package with default values in your `.nuspec` file, so you must edit the following fields before proceeding.</span></span> <span data-ttu-id="66ba8-154">Bkz. .nuspec dosya başvurusu - bunların nasıl kullanıldığına yönelik bir açıklama için [isteğe bağlı meta veri öğeleri.](../reference/nuspec.md#optional-metadata-elements)</span><span class="sxs-lookup"><span data-stu-id="66ba8-154">See [.nuspec file reference - optional metadata elements](../reference/nuspec.md#optional-metadata-elements) for a description of how these are used.</span></span>

    - <span data-ttu-id="66ba8-155">lisansUrl</span><span class="sxs-lookup"><span data-stu-id="66ba8-155">licenseUrl</span></span>
    - <span data-ttu-id="66ba8-156">projeUrl</span><span class="sxs-lookup"><span data-stu-id="66ba8-156">projectUrl</span></span>
    - <span data-ttu-id="66ba8-157">iconUrl</span><span class="sxs-lookup"><span data-stu-id="66ba8-157">iconUrl</span></span>
    - <span data-ttu-id="66ba8-158">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="66ba8-158">releaseNotes</span></span>
    - <span data-ttu-id="66ba8-159">etiketler</span><span class="sxs-lookup"><span data-stu-id="66ba8-159">tags</span></span>

1. <span data-ttu-id="66ba8-160">Genel tüketim için oluşturulmuş paketler için, etiketler diğerlerinin paketinizi nuget.org gibi kaynaklarda bulmasına ve ne işe yaradığına yardımcı olduğundan, **Etiketler** özelliğine özel olarak dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="66ba8-160">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package on sources like nuget.org and understand what it does.</span></span>

1. <span data-ttu-id="66ba8-161">[.nuspec dosya başvurusunda](../reference/nuspec.md)açıklandığı gibi, şu anda bildirime başka öğeler de ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66ba8-161">You can also add any other elements to the manifest at this time, as described on [.nuspec file reference](../reference/nuspec.md).</span></span>

1. <span data-ttu-id="66ba8-162">İşleme başlamadan önce dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="66ba8-162">Save the file before proceeding.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="66ba8-163">Sürü komutunu çalıştırın</span><span class="sxs-lookup"><span data-stu-id="66ba8-163">Run the pack command</span></span>

1. <span data-ttu-id="66ba8-164">Dosyanızı `.nuspec` içeren klasördeki bir komut isteminden `nuget pack`komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="66ba8-164">From a command prompt in the folder containing your `.nuspec` file, run the command `nuget pack`.</span></span>

1. <span data-ttu-id="66ba8-165">NuGet, geçerli `.nupkg` klasörde bulacağınız *tanımlayıcı-version.nupkg*şeklinde bir dosya oluşturur.</span><span class="sxs-lookup"><span data-stu-id="66ba8-165">NuGet generates a `.nupkg` file in the form of *identifier-version.nupkg*, which you'll find in the current folder.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="66ba8-166">Paketi yayımlama</span><span class="sxs-lookup"><span data-stu-id="66ba8-166">Publish the package</span></span>

<span data-ttu-id="66ba8-167">Bir `.nupkg` dosyaya sahip olduktan sonra, `nuget.exe` nuget.org'dan edinilen bir API anahtarıyla dosyayı nuget.org olarak yayımlarsınız. nuget.org için 4.1.0 veya daha yüksek kullanmanız `nuget.exe` gerekir.</span><span class="sxs-lookup"><span data-stu-id="66ba8-167">Once you have a `.nupkg` file, you publish it to nuget.org using `nuget.exe` with an API key acquired from nuget.org. For nuget.org you must use `nuget.exe` 4.1.0 or higher.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="66ba8-168">API anahtarınızı edinin</span><span class="sxs-lookup"><span data-stu-id="66ba8-168">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="66ba8-169">Nuget push ile yayımla</span><span class="sxs-lookup"><span data-stu-id="66ba8-169">Publish with nuget push</span></span>

1. <span data-ttu-id="66ba8-170">Bir komut satırı açın ve dosyayı içeren klasöre değiştirin. `.nupkg`</span><span class="sxs-lookup"><span data-stu-id="66ba8-170">Open a command line and change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="66ba8-171">Paket adınızı belirterek ve anahtar değerini API anahtarınızla değiştirerek aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="66ba8-171">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="66ba8-172">nuget.exe yayımlama sürecinin sonuçlarını görüntüler:</span><span class="sxs-lookup"><span data-stu-id="66ba8-172">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="66ba8-173">Nuget [itme](../reference/cli-reference/cli-ref-push.md)bakın .</span><span class="sxs-lookup"><span data-stu-id="66ba8-173">See [nuget push](../reference/cli-reference/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="66ba8-174">Hataları yayımlama</span><span class="sxs-lookup"><span data-stu-id="66ba8-174">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="66ba8-175">Yayımlanmış paketi yönetme</span><span class="sxs-lookup"><span data-stu-id="66ba8-175">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="next-steps"></a><span data-ttu-id="66ba8-176">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="66ba8-176">Next steps</span></span>

<span data-ttu-id="66ba8-177">İlk NuGet paketinizi oluşturduğunuz için tebrikler!</span><span class="sxs-lookup"><span data-stu-id="66ba8-177">Congratulations on creating your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="66ba8-178">Paket Oluşturma</span><span class="sxs-lookup"><span data-stu-id="66ba8-178">Create a Package</span></span>](../create-packages/creating-a-package.md)

<span data-ttu-id="66ba8-179">NuGet'in sunduğu daha fazlasını keşfetmek için aşağıdaki bağlantıları seçin.</span><span class="sxs-lookup"><span data-stu-id="66ba8-179">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="66ba8-180">Paket Yayınlama</span><span class="sxs-lookup"><span data-stu-id="66ba8-180">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="66ba8-181">Ön Sürüm Paketleri</span><span class="sxs-lookup"><span data-stu-id="66ba8-181">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="66ba8-182">Birden çok hedef çerçeveyi destekleme</span><span class="sxs-lookup"><span data-stu-id="66ba8-182">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="66ba8-183">Paket sürüm</span><span class="sxs-lookup"><span data-stu-id="66ba8-183">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="66ba8-184">Yerelleştirilmiş paketler oluşturma</span><span class="sxs-lookup"><span data-stu-id="66ba8-184">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
