---
title: Visual Studio şablonlarındaki NuGet paketleri
description: NuGet paketlerinin Visual Studio proje ve öğe şablonlarının bir parçası olarak dahil edilmesi için yönergeler.
author: karann-msft
ms.author: karann
ms.date: 01/03/2018
ms.topic: conceptual
ms.openlocfilehash: 2dfbd793eee05169f051d9c8943bc065945b92da
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622648"
---
# <a name="packages-in-visual-studio-templates"></a><span data-ttu-id="ceac2-103">Visual Studio şablonlarındaki paketler</span><span class="sxs-lookup"><span data-stu-id="ceac2-103">Packages in Visual Studio templates</span></span>

<span data-ttu-id="ceac2-104">Visual Studio proje ve öğe şablonları genellikle belirli paketlerin bir proje veya öğe oluşturulduğunda yüklendiğinden emin olunması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ceac2-104">Visual Studio project and item templates often need to ensure that certain packages are installed when a project or item is created.</span></span> <span data-ttu-id="ceac2-105">Örneğin, ASP.NET MVC 3 şablonu jQuery, Modernizr ve diğer paketleri de yüklüyor.</span><span class="sxs-lookup"><span data-stu-id="ceac2-105">For example, the ASP.NET MVC 3 template installs jQuery, Modernizr, and other packages.</span></span>

<span data-ttu-id="ceac2-106">Bunu desteklemek için, şablon yazarları NuGet 'e ayrı kitaplıklar yerine gerekli paketleri yüklemesini sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="ceac2-106">To support this, template authors can instruct NuGet to install the necessary packages, rather than individual libraries.</span></span> <span data-ttu-id="ceac2-107">Geliştiriciler daha sonra bu paketleri daha sonra kolayca güncelleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="ceac2-107">Developers can then easily update those packages at any later time.</span></span>

<span data-ttu-id="ceac2-108">Şablon yazma hakkında daha fazla bilgi edinmek için [nasıl yapılır: proje şablonları oluşturma](/visualstudio/ide/how-to-create-project-templates) veya [özel proje ve öğe şablonları oluşturma](/visualstudio/extensibility/creating-custom-project-and-item-templates)bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="ceac2-108">To learn more about authoring templates themselves, refer to [How to: Create Project Templates](/visualstudio/ide/how-to-create-project-templates) or [Creating Custom Project and Item Templates](/visualstudio/extensibility/creating-custom-project-and-item-templates).</span></span>

<span data-ttu-id="ceac2-109">Bu bölümün geri kalanında, NuGet paketlerini düzgün bir şekilde içerecek şekilde bir şablon yazarken yapmanız gereken belirli adımlar açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ceac2-109">The remainder of this section describes the specific steps to take when authoring a template to properly include NuGet packages.</span></span>

- [<span data-ttu-id="ceac2-110">Bir şablona paket ekleme</span><span class="sxs-lookup"><span data-stu-id="ceac2-110">Adding packages to a template</span></span>](#adding-packages-to-a-template)
- [<span data-ttu-id="ceac2-111">En iyi uygulamalar</span><span class="sxs-lookup"><span data-stu-id="ceac2-111">Best practices</span></span>](#best-practices)

<span data-ttu-id="ceac2-112">Bir örnek için, bkz. [Nugetfaturalanmış Stempsyonlar örneği](https://bitbucket.org/marcind/nugetinvstemplates).</span><span class="sxs-lookup"><span data-stu-id="ceac2-112">For an example, see the [NuGetInVsTemplates sample](https://bitbucket.org/marcind/nugetinvstemplates).</span></span>

## <a name="adding-packages-to-a-template"></a><span data-ttu-id="ceac2-113">Bir şablona paket ekleme</span><span class="sxs-lookup"><span data-stu-id="ceac2-113">Adding packages to a template</span></span>

<span data-ttu-id="ceac2-114">Bir şablon örneği oluşturulduğunda, yüklenecek paketlerin listesini, bu paketlerin nerede bulunacağı hakkında bilgi içeren bir [Şablon Sihirbazı](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) çağırılır.</span><span class="sxs-lookup"><span data-stu-id="ceac2-114">When a template is instantiated, a [template wizard](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) is invoked to load the list of packages to install along with information about where to find those packages.</span></span> <span data-ttu-id="ceac2-115">Paketler VSıX 'e gömülebilir, şablona katıştırılabilir veya yerel sabit sürücüde bulunabilir ve bu durumda dosya yoluna başvurmak için bir kayıt defteri anahtarı kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="ceac2-115">Packages can be embedded in the VSIX, embedded in the template, or located on the local hard drive in which case you use a registry key to reference the file path.</span></span> <span data-ttu-id="ceac2-116">Bu konumların ayrıntıları bu bölümde daha sonra verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ceac2-116">Details on these locations are given later in this section.</span></span>

<span data-ttu-id="ceac2-117">Önceden yüklenmiş paketler, [şablon sihirbazları](/visualstudio/extensibility/how-to-use-wizards-with-project-templates)kullanılarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="ceac2-117">Preinstalled packages work using [template wizards](/visualstudio/extensibility/how-to-use-wizards-with-project-templates).</span></span> <span data-ttu-id="ceac2-118">Şablon örneği oluşturulduğunda özel bir sihirbaz çağrılır.</span><span class="sxs-lookup"><span data-stu-id="ceac2-118">A special wizard gets invoked when the template gets instantiated.</span></span> <span data-ttu-id="ceac2-119">Sihirbaz yüklenmesi gereken paketlerin listesini yükler ve ilgili bilgileri uygun NuGet API 'Lerine geçirir.</span><span class="sxs-lookup"><span data-stu-id="ceac2-119">The wizard loads the list of packages that need to be installed and passes that information to the appropriate NuGet APIs.</span></span>

<span data-ttu-id="ceac2-120">Bir şablona paket ekleme adımları:</span><span class="sxs-lookup"><span data-stu-id="ceac2-120">Steps to include packages in a template:</span></span>

1. <span data-ttu-id="ceac2-121">`vstemplate`Dosyanızda, bir öğe ekleyerek NuGet şablon sihirbazına bir başvuru ekleyin [`WizardExtension`](/visualstudio/extensibility/wizardextension-element-visual-studio-templates) :</span><span class="sxs-lookup"><span data-stu-id="ceac2-121">In your `vstemplate` file, add a reference to the NuGet template wizard by adding a [`WizardExtension`](/visualstudio/extensibility/wizardextension-element-visual-studio-templates) element:</span></span>

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    <span data-ttu-id="ceac2-122">`NuGet.VisualStudio.Interop.dll` , yalnızca `TemplateWizard` içindeki gerçek uygulamaya çağıran basit bir sarmalayıcı olan sınıfını içeren bir derlemedir `NuGet.VisualStudio.dll` .</span><span class="sxs-lookup"><span data-stu-id="ceac2-122">`NuGet.VisualStudio.Interop.dll` is an assembly that contains only the `TemplateWizard` class, which is a simple wrapper that calls into the actual implementation in `NuGet.VisualStudio.dll`.</span></span> <span data-ttu-id="ceac2-123">Proje/öğe şablonlarının NuGet 'in yeni sürümleriyle çalışmaya devam etmesi için derleme sürümü hiçbir şekilde değişmeyecektir.</span><span class="sxs-lookup"><span data-stu-id="ceac2-123">The assembly version will never change so that project/item templates continue to work with new versions of NuGet.</span></span>

1. <span data-ttu-id="ceac2-124">Projeye yüklenecek paketlerin listesini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ceac2-124">Add the list of packages to install in the project:</span></span>

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    <span data-ttu-id="ceac2-125">Sihirbaz `<package>` birden çok paket kaynağını desteklemek için birden çok öğeyi destekler.</span><span class="sxs-lookup"><span data-stu-id="ceac2-125">The wizard supports multiple `<package>` elements to support multiple package sources.</span></span> <span data-ttu-id="ceac2-126">Ve özniteliklerinin her ikisi de `id` `version` gereklidir; yani, daha yeni bir sürüm kullanılabilir olsa bile paketin belirli bir sürümünün yükleneceği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="ceac2-126">Both the `id` and `version` attributes are required, meaning that specific version of a package will be installed even if a newer version is available.</span></span> <span data-ttu-id="ceac2-127">Bu, paket güncelleştirmelerinin şablonu bozmasını engeller ve şablonu kullanarak paketi geliştiriciye güncelleştirme seçeneğini bırakır.</span><span class="sxs-lookup"><span data-stu-id="ceac2-127">This prevents package updates from breaking the template, leaving the choice to update the package to the developer using the template.</span></span>

1. <span data-ttu-id="ceac2-128">Aşağıdaki bölümlerde açıklandığı gibi, NuGet 'in paketleri bulabileceği depoyu belirtin.</span><span class="sxs-lookup"><span data-stu-id="ceac2-128">Specify the repository where NuGet can find the packages as described in the following sections.</span></span>

### <a name="vsix-package-repository"></a><span data-ttu-id="ceac2-129">VSıX paket deposu</span><span class="sxs-lookup"><span data-stu-id="ceac2-129">VSIX package repository</span></span>

<span data-ttu-id="ceac2-130">Visual Studio proje/öğe şablonları için önerilen dağıtım yaklaşımı bir [VSIX uzantısıdır](/visualstudio/extensibility/shipping-visual-studio-extensions) , çünkü birden fazla proje/öğe şablonunu birlikte paketlemenize ve geliştiricilerin vs uzantısı yöneticisini veya Visual Studio galerisini kullanarak şablonlarınızı kolayca bulmasına olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="ceac2-130">The recommended deployment approach for Visual Studio project/item templates is a [VSIX extension](/visualstudio/extensibility/shipping-visual-studio-extensions) because it allows you to package multiple project/item templates together and allows developers to easily discover your templates using the VS Extension Manager or the Visual Studio Gallery.</span></span> <span data-ttu-id="ceac2-131">Uzantı güncelleştirmelerinin [Visual Studio Uzantı Yöneticisi otomatik güncelleştirme mekanizması](/visualstudio/extensibility/how-to-update-a-visual-studio-extension)kullanılarak dağıtılması da kolaydır.</span><span class="sxs-lookup"><span data-stu-id="ceac2-131">Updates to the extension are also easy to deploy using the [Visual Studio Extension Manager automatic update mechanism](/visualstudio/extensibility/how-to-update-a-visual-studio-extension).</span></span>

<span data-ttu-id="ceac2-132">VSıX, şablonun gerektirdiği paketlere yönelik kaynak olarak görev yapabilir:</span><span class="sxs-lookup"><span data-stu-id="ceac2-132">The VSIX itself can serve as the source for packages required by the template:</span></span>

1. <span data-ttu-id="ceac2-133">`<packages>` `.vstemplate` Dosyadaki öğesini aşağıdaki gibi değiştirin:</span><span class="sxs-lookup"><span data-stu-id="ceac2-133">Modify the `<packages>` element in the `.vstemplate` file as follows:</span></span>

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    <span data-ttu-id="ceac2-134">Özniteliği,, `repository` `extension` `repositoryId` VSIX 'in benzersiz tanımlayıcısı olduğu gibi, deponun türünü belirtir (Bu, `ID` uzantının dosyasındaki özniteliğin değeridir `vsixmanifest` , bkz. [VSIX uzantı Şeması 2,0 başvurusu](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).</span><span class="sxs-lookup"><span data-stu-id="ceac2-134">The `repository` attribute specifies the type of repository as `extension` while `repositoryId` is the unique identifier of the VSIX itself (This is the value of the `ID` attribute in the extension’s `vsixmanifest` file, see [VSIX Extension Schema 2.0 Reference](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).</span></span>

1. <span data-ttu-id="ceac2-135">`nupkg`DOSYALARıNıZı VSIX içinde adlı bir klasöre yerleştirin `Packages` .</span><span class="sxs-lookup"><span data-stu-id="ceac2-135">Place your `nupkg` files in a folder called `Packages` within the VSIX.</span></span>

1. <span data-ttu-id="ceac2-136">Gerekli paket dosyalarını `<Asset>` `vsixmanifest` dosyanıza ekleyin (bkz. [vsıx uzantı Şeması 2,0 başvurusu](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)):</span><span class="sxs-lookup"><span data-stu-id="ceac2-136">Add the necessary package files as `<Asset>` in your `vsixmanifest` file (see [VSIX Extension Schema 2.0 Reference](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)):</span></span>

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

1. <span data-ttu-id="ceac2-137">Aynı VSıX içindeki paketleri proje şablonlarınızla sunabilmenizi veya bu, senaryonuza daha anlamlı bir şekilde bir VSıX 'e koyabileceğinizi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ceac2-137">Note that you can deliver packages in the same VSIX as your project templates or you can put them in a separate VSIX if that makes more sense for your scenario.</span></span> <span data-ttu-id="ceac2-138">Ancak, bu uzantıdaki değişiklikler şablonunuzu bozabileceğinden, denetiminiz olmayan herhangi bir VSıX 'e başvurmayın.</span><span class="sxs-lookup"><span data-stu-id="ceac2-138">However, do not reference any VSIX over which you do not have control, because changes to that extension could break your template.</span></span>

### <a name="template-package-repository"></a><span data-ttu-id="ceac2-139">Şablon paket deposu</span><span class="sxs-lookup"><span data-stu-id="ceac2-139">Template package repository</span></span>

<span data-ttu-id="ceac2-140">Yalnızca tek bir proje/öğe şablonunu dağıtıyorsanız ve birden çok şablonu birlikte paketlemenize gerek yoksa, doğrudan proje/öğe şablonu ZIP dosyasında paketleri içeren daha basit ancak daha sınırlı bir yaklaşım kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ceac2-140">If you are distributing only a single project/item template and do not need to package multiple templates together, you can use a simpler but more limited approach that includes packages directly in the project/item template ZIP file:</span></span>

1. <span data-ttu-id="ceac2-141">`<packages>` `.vstemplate` Dosyadaki öğesini aşağıdaki gibi değiştirin:</span><span class="sxs-lookup"><span data-stu-id="ceac2-141">Modify the `<packages>` element in the `.vstemplate` file as follows:</span></span>

    ```xml
    <packages repository="template">
        <!-- ... -->
    </packages>
    ```

    <span data-ttu-id="ceac2-142">`repository`Özniteliğin değeri vardır `template` ve `repositoryId` özniteliği gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="ceac2-142">The `repository` attribute has the value `template` and the `repositoryId` attribute is not required.</span></span>

1. <span data-ttu-id="ceac2-143">Paketleri proje/öğe şablonu ZIP dosyasının kök klasörüne yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="ceac2-143">Place packages in the root folder of the project/item template ZIP file.</span></span>

<span data-ttu-id="ceac2-144">Bu yaklaşımı birden çok şablon içeren bir VSIX içinde kullanmanın, bir veya daha fazla paket şablonlarda ortak olduğunda gereksiz oluşan şişirmeyi 'a yol açar.</span><span class="sxs-lookup"><span data-stu-id="ceac2-144">Note that using this approach in a VSIX that contains multiple templates leads to unnecessary bloat when one or more packages are common to the templates.</span></span> <span data-ttu-id="ceac2-145">Bu gibi durumlarda, önceki bölümde açıklandığı gibi [VSIX 'i depo olarak](#vsix-package-repository) kullanın.</span><span class="sxs-lookup"><span data-stu-id="ceac2-145">In such cases, use the [VSIX as the repository](#vsix-package-repository) as described in the previous section.</span></span>

### <a name="registry-specified-folder-path"></a><span data-ttu-id="ceac2-146">Kayıt defteri-belirtilen klasör yolu</span><span class="sxs-lookup"><span data-stu-id="ceac2-146">Registry-specified folder path</span></span>

<span data-ttu-id="ceac2-147">MSI kullanılarak yüklenen SDK 'lar, NuGet paketlerini doğrudan geliştiricinin makinesine yükleyebilir.</span><span class="sxs-lookup"><span data-stu-id="ceac2-147">SDKs that are installed using an MSI can install NuGet packages directly on the developer's machine.</span></span> <span data-ttu-id="ceac2-148">Bu, bir proje veya öğe şablonu kullanıldığında, bu süre içinde ayıklanmaları yerine bunları hemen kullanılabilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="ceac2-148">This makes them immediately available when a project or item template is used, rather than having to extract them during that time.</span></span> <span data-ttu-id="ceac2-149">ASP.NET şablonları bu yaklaşımı kullanır.</span><span class="sxs-lookup"><span data-stu-id="ceac2-149">ASP.NET templates use this approach.</span></span>

1. <span data-ttu-id="ceac2-150">MSI paketlerini makineye yüklemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="ceac2-150">Have the MSI install packages to the machine.</span></span> <span data-ttu-id="ceac2-151">Yalnızca `.nupkg` dosyaları yükleyebilir veya bunları genişletilmiş içerikle birlikte yükleyebilirsiniz ve bu da şablon kullanıldığında ek bir adım kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="ceac2-151">You can install only the `.nupkg` files, or you can install those along with the expanded contents, which saves an additional step when the template is used.</span></span> <span data-ttu-id="ceac2-152">Bu durumda, dosyaların kök klasörde olduğu, NuGet 'in standart klasör yapısını izleyin `.nupkg` ve sonra her pakette alt klasör adı olarak kimlik/sürüm çiftinin bulunduğu bir alt klasör bulunur.</span><span class="sxs-lookup"><span data-stu-id="ceac2-152">In this case, follow NuGet's standard folder structure wherein the `.nupkg` files are in the root folder, and then each package has a subfolder with the id/version pair as the subfolder name.</span></span>

1. <span data-ttu-id="ceac2-153">Paket konumunu tanımlamak için bir kayıt defteri anahtarı yazın:</span><span class="sxs-lookup"><span data-stu-id="ceac2-153">Write a registry key to identify the package location:</span></span>

    - <span data-ttu-id="ceac2-154">Anahtar konumu: makine genelinde `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` veya Kullanıcı başına yüklenmiş şablonlar ve paketler, alternatif olarak `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`</span><span class="sxs-lookup"><span data-stu-id="ceac2-154">Key location: Either the machine-wide `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` or if it's per-user installed templates and packages, alternatively use `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`</span></span>
    - <span data-ttu-id="ceac2-155">Anahtar adı: sizin için benzersiz olan bir ad kullanın.</span><span class="sxs-lookup"><span data-stu-id="ceac2-155">Key name: use a name that's unique to you.</span></span> <span data-ttu-id="ceac2-156">Örneğin, VS 2012 için ASP.NET MVC 4 şablonları kullanılır `AspNetMvc4VS11` .</span><span class="sxs-lookup"><span data-stu-id="ceac2-156">For example, the ASP.NET MVC 4 templates for VS 2012 use `AspNetMvc4VS11`.</span></span>
    - <span data-ttu-id="ceac2-157">Değerler: paketler klasörünün tam yolu.</span><span class="sxs-lookup"><span data-stu-id="ceac2-157">Values: the full path to the packages folder.</span></span>

1. <span data-ttu-id="ceac2-158">`<packages>` `.vstemplate` Dosyadaki öğesinde, özniteliğini ekleyin `repository="registry"` ve özniteliğinde kayıt defteri anahtarı adını belirtin `keyName` .</span><span class="sxs-lookup"><span data-stu-id="ceac2-158">In the `<packages>` element in the `.vstemplate` file, add the attribute `repository="registry"` and specify your registry key name in the `keyName` attribute.</span></span>

    - <span data-ttu-id="ceac2-159">Paketlerinizi önceden sıkıştırdıysanız, `isPreunzipped="true"` özniteliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="ceac2-159">If you have pre-unzipped your packages, use the `isPreunzipped="true"` attribute.</span></span>
    - <span data-ttu-id="ceac2-160">*(NuGet 3.2 +)* Paket yüklemesinin sonunda bir tasarım zamanı oluşturmaya zorlamak isterseniz, `forceDesignTimeBuild="true"` özniteliğini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ceac2-160">*(NuGet 3.2+)* If you want to force a design-time build at the end of package installation, add the `forceDesignTimeBuild="true"` attribute.</span></span>
    - <span data-ttu-id="ceac2-161">Bir iyileştirme olarak, `skipAssemblyReferences="true"` şablon zaten gerekli başvuruları içerdiğinden ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ceac2-161">As an optimization, add `skipAssemblyReferences="true"` because the template itself already includes the necessary references.</span></span>

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a><span data-ttu-id="ceac2-162">En İyi Uygulamalar</span><span class="sxs-lookup"><span data-stu-id="ceac2-162">Best Practices</span></span>

1. <span data-ttu-id="ceac2-163">VSıX bildiriminizde buna bir başvuru ekleyerek NuGet VSıX üzerinde bir bağımlılık bildirin:</span><span class="sxs-lookup"><span data-stu-id="ceac2-163">Declare a dependency on the NuGet VSIX by adding a reference to it in your VSIX manifest:</span></span>

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. <span data-ttu-id="ceac2-164">Dosyasına dahil ederek proje/öğe şablonlarının oluşturma sırasında kaydedilmesini gerektir [`<PromptForSaveOnCreation>true</PromptForSaveOnCreation>`](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) `.vstemplate` .</span><span class="sxs-lookup"><span data-stu-id="ceac2-164">Require project/item templates to be saved on creation by including [`<PromptForSaveOnCreation>true</PromptForSaveOnCreation>`](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) in the `.vstemplate` file.</span></span>

1. <span data-ttu-id="ceac2-165">Şablonlar bir `packages.config` dosya içermez ve NuGet paketleri yüklendiğinde eklenecek başvuruları ya da içeriği içermez.</span><span class="sxs-lookup"><span data-stu-id="ceac2-165">Templates do not include a `packages.config` file, and do not include or any references or content that would be added when NuGet packages are installed.</span></span>
