---
title: Visual Studio şablonları NuGet paketleri
description: NuGet paketlerini Visual Studio'nun proje ve öğe şablonlarını bir parçası olarak dahil etmek için yönergeler.
author: karann-msft
ms.author: karann
ms.date: 01/03/2018
ms.topic: conceptual
ms.openlocfilehash: be7c10fb6ce60375f77e38f9b604ec33063e52fc
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550516"
---
# <a name="packages-in-visual-studio-templates"></a><span data-ttu-id="9ca16-103">Visual Studio şablonları paketleri</span><span class="sxs-lookup"><span data-stu-id="9ca16-103">Packages in Visual Studio templates</span></span>

<span data-ttu-id="9ca16-104">Visual Studio Proje ve öğe şablonları, genellikle bir proje veya öğe oluşturulduğunda, bazı paketlerden yüklendiğinden emin emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ca16-104">Visual Studio project and item templates often need to ensure that certain packages are installed when a project or item is created.</span></span> <span data-ttu-id="9ca16-105">Örneğin, ASP.NET MVC 3 şablonu, jQuery, Modernize ve diğer paketleri yükler.</span><span class="sxs-lookup"><span data-stu-id="9ca16-105">For example, the ASP.NET MVC 3 template installs jQuery, Modernizr, and other packages.</span></span>

<span data-ttu-id="9ca16-106">Bunu desteklemek için şablonu yazarlar, tek tek kitaplıklarda yerine gerekli paketleri yüklemek için NuGet bildirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ca16-106">To support this, template authors can instruct NuGet to install the necessary packages, rather than individual libraries.</span></span> <span data-ttu-id="9ca16-107">Geliştiriciler daha sonra kolayca bu paketleri daha sonraki bir zamanda güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ca16-107">Developers can then easily update those packages at any later time.</span></span>

<span data-ttu-id="9ca16-108">Şablonlar yazma hakkında daha fazla bilgi için bkz [nasıl yapılır: Proje şablonları oluşturma](/visualstudio/ide/how-to-create-project-templates) veya [oluşturma özel Proje ve öğe şablonlarını](/visualstudio/extensibility/creating-custom-project-and-item-templates).</span><span class="sxs-lookup"><span data-stu-id="9ca16-108">To learn more about authoring templates themselves, refer to [How to: Create Project Templates](/visualstudio/ide/how-to-create-project-templates) or [Creating Custom Project and Item Templates](/visualstudio/extensibility/creating-custom-project-and-item-templates).</span></span>

<span data-ttu-id="9ca16-109">Bu bölümün geri kalanında, bir şablon yazma düzgün şekilde NuGet paketlerini içerecek şekilde gerçekleştirilecek belirli adımlar açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9ca16-109">The remainder of this section describes the specific steps to take when authoring a template to properly include NuGet packages.</span></span>

- [<span data-ttu-id="9ca16-110">Bir şablona paketleri ekleme</span><span class="sxs-lookup"><span data-stu-id="9ca16-110">Adding packages to a template</span></span>](#adding-packages-to-a-template)
- [<span data-ttu-id="9ca16-111">En iyi uygulamalar</span><span class="sxs-lookup"><span data-stu-id="9ca16-111">Best practices</span></span>](#best-practices)

<span data-ttu-id="9ca16-112">Bir örnek için bkz. [NuGetInVsTemplates örnek](https://bitbucket.org/marcind/nugetinvstemplates).</span><span class="sxs-lookup"><span data-stu-id="9ca16-112">For an example, see the [NuGetInVsTemplates sample](https://bitbucket.org/marcind/nugetinvstemplates).</span></span>

## <a name="adding-packages-to-a-template"></a><span data-ttu-id="9ca16-113">Bir şablona paketleri ekleme</span><span class="sxs-lookup"><span data-stu-id="9ca16-113">Adding packages to a template</span></span>

<span data-ttu-id="9ca16-114">Bir şablon örneği başlatıldığında bir [Şablon Sihirbazı](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) bu paketleri nerede bulunacağı hakkında bilgi ile birlikte yüklemek için paketler listesini yüklemek için çağrılır.</span><span class="sxs-lookup"><span data-stu-id="9ca16-114">When a template is instantiated, a [template wizard](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) is invoked to load the list of packages to install along with information about where to find those packages.</span></span> <span data-ttu-id="9ca16-115">Paket içinde VSIX içine katıştırılmış, şablonda katıştırılmış veya yerel sabit sürücüsünde bulunan bu durumda dosya yolu başvurmak için bir kayıt defteri anahtarı kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="9ca16-115">Packages can be embedded in the VSIX, embedded in the template, or located on the local hard drive in which case you use a registry key to reference the file path.</span></span> <span data-ttu-id="9ca16-116">Bu konumlar hakkında ayrıntılı bilgi, daha sonra bu bölümde verilir.</span><span class="sxs-lookup"><span data-stu-id="9ca16-116">Details on these locations are given later in this section.</span></span>

<span data-ttu-id="9ca16-117">Önceden yüklenmiş paketler çalışma kullanarak [şablon sihirbazları](/visualstudio/extensibility/how-to-use-wizards-with-project-templates).</span><span class="sxs-lookup"><span data-stu-id="9ca16-117">Preinstalled packages work using [template wizards](/visualstudio/extensibility/how-to-use-wizards-with-project-templates).</span></span> <span data-ttu-id="9ca16-118">Şablon örneği, özel sihirbaz çağrılır.</span><span class="sxs-lookup"><span data-stu-id="9ca16-118">A special wizard gets invoked when the template gets instantiated.</span></span> <span data-ttu-id="9ca16-119">Sihirbazın yüklenmesi gereken paketler listesini yükler ve uygun NuGet API'leri için bu bilgileri geçirir.</span><span class="sxs-lookup"><span data-stu-id="9ca16-119">The wizard loads the list of packages that need to be installed and passes that information to the appropriate NuGet APIs.</span></span>

<span data-ttu-id="9ca16-120">Bir şablonda paketlerini içerecek şekilde adımlar:</span><span class="sxs-lookup"><span data-stu-id="9ca16-120">Steps to include packages in a template:</span></span>

1. <span data-ttu-id="9ca16-121">İçinde `vstemplate` dosya, NuGet şablon sihirbazında yapılan bir başvuru ekleyerek bir [ `WizardExtension` ](/visualstudio/extensibility/wizardextension-element-visual-studio-templates) öğesi:</span><span class="sxs-lookup"><span data-stu-id="9ca16-121">In your `vstemplate` file, add a reference to the NuGet template wizard by adding a [`WizardExtension`](/visualstudio/extensibility/wizardextension-element-visual-studio-templates) element:</span></span>

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    <span data-ttu-id="9ca16-122">`NuGet.VisualStudio.Interop.dll` yalnızca içeren bir derleme `TemplateWizard` gerçek uygulamasında içine yapılan çağrılar basit bir sarmalayıcı sınıfının `NuGet.VisualStudio.dll`.</span><span class="sxs-lookup"><span data-stu-id="9ca16-122">`NuGet.VisualStudio.Interop.dll` is an assembly that contains only the `TemplateWizard` class, which is a simple wrapper that calls into the actual implementation in `NuGet.VisualStudio.dll`.</span></span> <span data-ttu-id="9ca16-123">Proje/öğe şablonları yeni NuGet sürümlerini ile çalışmaya devam eder, derleme sürümü asla değiştirmez.</span><span class="sxs-lookup"><span data-stu-id="9ca16-123">The assembly version will never change so that project/item templates continue to work with new versions of NuGet.</span></span>

1. <span data-ttu-id="9ca16-124">Projeye yüklemek için paketler listesini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9ca16-124">Add the list of packages to install in the project:</span></span>

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    <span data-ttu-id="9ca16-125">Birden çok sihirbaz destekler `<package>` birden çok paket kaynaklarını desteklemek için öğeleri.</span><span class="sxs-lookup"><span data-stu-id="9ca16-125">The wizard supports multiple `<package>` elements to support multiple package sources.</span></span> <span data-ttu-id="9ca16-126">Hem `id` ve `version` , belirli bir paketin sürümü anlamı yükleneceği daha yeni bir sürüm kullanılabilir olsa bile, öznitelikleri gereklidir.</span><span class="sxs-lookup"><span data-stu-id="9ca16-126">Both the `id` and `version` attributes are required, meaning that specific version of a package will be installed even if a newer version is available.</span></span> <span data-ttu-id="9ca16-127">Bu paket güncelleştirmeleri paketi güncelleştirmeye şablonuyla Geliştirici seçimi bırakın, şablon bozmasını engeller.</span><span class="sxs-lookup"><span data-stu-id="9ca16-127">This prevents package updates from breaking the template, leaving the choice to update the package to the developer using the template.</span></span>

1. <span data-ttu-id="9ca16-128">NuGet paketleri aşağıdaki bölümlerde açıklandığı gibi bulabileceğiniz havuz belirtin.</span><span class="sxs-lookup"><span data-stu-id="9ca16-128">Specify the repository where NuGet can find the packages as described in the following sections.</span></span>

### <a name="vsix-package-repository"></a><span data-ttu-id="9ca16-129">VSIX Paket Deposu</span><span class="sxs-lookup"><span data-stu-id="9ca16-129">VSIX package repository</span></span>

<span data-ttu-id="9ca16-130">Visual Studio Proje/öğe şablonları için önerilen dağıtım yaklaşımdır bir [VSIX uzantısı](/visualstudio/extensibility/shipping-visual-studio-extensions) çünkü birden çok proje/öğe şablon birlikte paketlemenize olanak sağlar ve geliştiricilerin şablonlarınızı kolayca keşfedin olanak tanır VS uzantısı Yöneticisi veya Visual Studio Galerisi kullanma.</span><span class="sxs-lookup"><span data-stu-id="9ca16-130">The recommended deployment approach for Visual Studio project/item templates is a [VSIX extension](/visualstudio/extensibility/shipping-visual-studio-extensions) because it allows you to package multiple project/item templates together and allows developers to easily discover your templates using the VS Extension Manager or the Visual Studio Gallery.</span></span> <span data-ttu-id="9ca16-131">Uzantı için güncelleştirmeleri kullanarak kolayca ayrıca [Visual Studio Uzantı Yöneticisi'ni otomatik güncelleştirme mekanizmasını](/visualstudio/extensibility/how-to-update-a-visual-studio-extension).</span><span class="sxs-lookup"><span data-stu-id="9ca16-131">Updates to the extension are also easy to deploy using the [Visual Studio Extension Manager automatic update mechanism](/visualstudio/extensibility/how-to-update-a-visual-studio-extension).</span></span>

<span data-ttu-id="9ca16-132">VSIX şablon için gerekli paketleri için kaynak olarak hizmet verebilen:</span><span class="sxs-lookup"><span data-stu-id="9ca16-132">The VSIX itself can serve as the source for packages required by the template:</span></span>

1. <span data-ttu-id="9ca16-133">Değiştirme `<packages>` öğesinde `.vstemplate` aşağıdaki gibi:</span><span class="sxs-lookup"><span data-stu-id="9ca16-133">Modify the `<packages>` element in the `.vstemplate` file as follows:</span></span>

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    <span data-ttu-id="9ca16-134">`repository` Öznitelik deposu olarak türünü belirten `extension` sırada `repositoryId` VSIX benzersiz tanıtıcısı (Bu değeri `ID` uzantının özniteliğinde `vsixmanifest` bkz [ VSIX Uzantı Şeması 2.0 başvurusu](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).</span><span class="sxs-lookup"><span data-stu-id="9ca16-134">The `repository` attribute specifies the type of repository as `extension` while `repositoryId` is the unique identifier of the VSIX itself (This is the value of the `ID` attribute in the extension’s `vsixmanifest` file, see [VSIX Extension Schema 2.0 Reference](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).</span></span>

1. <span data-ttu-id="9ca16-135">Bir yerde, `nupkg` adlı bir klasördeki dosyaları `Packages` VSIX içinde.</span><span class="sxs-lookup"><span data-stu-id="9ca16-135">Place your `nupkg` files in a folder called `Packages` within the VSIX.</span></span>

1. <span data-ttu-id="9ca16-136">Gerekli paket dosyaları olarak ekleme `<Asset>` içinde `vsixmanifest` dosyası (bkz [VSIX Uzantı Şeması 2.0 başvurusu](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)):</span><span class="sxs-lookup"><span data-stu-id="9ca16-136">Add the necessary package files as `<Asset>` in your `vsixmanifest` file (see [VSIX Extension Schema 2.0 Reference](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)):</span></span>

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

1. <span data-ttu-id="9ca16-137">Paketler, proje şablonları olarak aynı VSIX içinde sağlayabileceğiniz veya, senaryonuz için daha anlamlı olur, bunları ayrı bir VSIX'e koyabilirsiniz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="9ca16-137">Note that you can deliver packages in the same VSIX as your project templates or you can put them in a separate VSIX if that makes more sense for your scenario.</span></span> <span data-ttu-id="9ca16-138">Ancak, bu uzantı değişiklikleri şablonunuzu uğratabilir olduğundan üzerinde denetimi sizde değil herhangi bir VSIX başvuruda bulunmayın.</span><span class="sxs-lookup"><span data-stu-id="9ca16-138">However, do not reference any VSIX over which you do not have control, because changes to that extension could break your template.</span></span>

### <a name="template-package-repository"></a><span data-ttu-id="9ca16-139">Şablon Paket Deposu</span><span class="sxs-lookup"><span data-stu-id="9ca16-139">Template package repository</span></span>

<span data-ttu-id="9ca16-140">Yalnızca tek proje/öğe şablon dağıtma ve birden fazla şablon birlikte paketini gerekmez, doğrudan proje/öğe şablon ZIP dosyasında paketlerini içeren daha basit ancak daha sınırlı bir yaklaşımı kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9ca16-140">If you are distributing only a single project/item template and do not need to package multiple templates together, you can use a simpler but more limited approach that includes packages directly in the project/item template ZIP file:</span></span>

1. <span data-ttu-id="9ca16-141">Değiştirme `<packages>` öğesinde `.vstemplate` aşağıdaki gibi:</span><span class="sxs-lookup"><span data-stu-id="9ca16-141">Modify the `<packages>` element in the `.vstemplate` file as follows:</span></span>

    ```xml
    <packages repository="template"">
        <!-- ... -->
    </packages>
    ```

    <span data-ttu-id="9ca16-142">`repository` Özniteliğinin değeri `template` ve `repositoryId` öznitelik gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="9ca16-142">The `repository` attribute has the value `template` and the `repositoryId` attribute is not required.</span></span>

1. <span data-ttu-id="9ca16-143">Paketleri proje/öğe şablon ZIP dosyasının kök klasörüne yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="9ca16-143">Place packages in the root folder of the project/item template ZIP file.</span></span>

<span data-ttu-id="9ca16-144">Bir veya daha fazla paket şablonları için ortak olduğunda bu yaklaşımı kullanarak birden fazla şablon içeren bir VSIX için gereksiz Şişirme müşteri adayları olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="9ca16-144">Note that using this approach in a VSIX that contains multiple templates leads to unnecessary bloat when one or more packages are common to the templates.</span></span> <span data-ttu-id="9ca16-145">Böyle durumlarda kullanmak [deposu olarak VSIX](#vsix-package-repository) önceki bölümde açıklandığı gibi.</span><span class="sxs-lookup"><span data-stu-id="9ca16-145">In such cases, use the [VSIX as the repository](#vsix-package-repository) as described in the previous section.</span></span>

### <a name="registry-specified-folder-path"></a><span data-ttu-id="9ca16-146">Kayıt defteri belirtilen klasör yolu</span><span class="sxs-lookup"><span data-stu-id="9ca16-146">Registry-specified folder path</span></span>

<span data-ttu-id="9ca16-147">MSI kullanarak yüklü SDK'ları NuGet paketlerini doğrudan Geliştirici makineye yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ca16-147">SDKs that are installed using an MSI can install NuGet packages directly on the developer's machine.</span></span> <span data-ttu-id="9ca16-148">Hemen kullanılamıyorsa, bir proje veya öğe şablonu, bunları kullanılan bu yapar, yerine bu süre boyunca ayıklanacak.</span><span class="sxs-lookup"><span data-stu-id="9ca16-148">This makes them immediately available when a project or item template is used, rather than having to extract them during that time.</span></span> <span data-ttu-id="9ca16-149">ASP.NET şablonları, bu yaklaşımı kullanın.</span><span class="sxs-lookup"><span data-stu-id="9ca16-149">ASP.NET templates use this approach.</span></span>

1. <span data-ttu-id="9ca16-150">MSI paketleri yüklemek için makine var.</span><span class="sxs-lookup"><span data-stu-id="9ca16-150">Have the MSI install packages to the machine.</span></span> <span data-ttu-id="9ca16-151">Yalnızca yükleyebilirsiniz `.nupkg` dosyaları veya yükleyebilir genişletilmiş içeriği ile birlikte bu şablonu kullanıldığında ek bir adım kaydeder.</span><span class="sxs-lookup"><span data-stu-id="9ca16-151">You can install only the `.nupkg` files, or you can install those along with the expanded contents, which saves an additional step when the template is used.</span></span> <span data-ttu-id="9ca16-152">Bu durumda, NuGet'ın standart klasör yapısını burada görüntülerle izleyin `.nupkg` dosyaları kök klasöründe ve ardından her paket kimliği/VERSION çifti alt klasör adı ile bir alt sahip.</span><span class="sxs-lookup"><span data-stu-id="9ca16-152">In this case, follow NuGet's standard folder structure wherein the `.nupkg` files are in the root folder, and then each package has a subfolder with the id/version pair as the subfolder name.</span></span>

1. <span data-ttu-id="9ca16-153">Paket konumunu tanımlamak için bir kayıt defteri anahtarı yazın:</span><span class="sxs-lookup"><span data-stu-id="9ca16-153">Write a registry key to identify the package location:</span></span>

    - <span data-ttu-id="9ca16-154">Anahtar konumu: ya da makine genelindeki `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` veya kullanıcı başına yüklü şablonları ve paketleri ise, alternatif olarak kullanın `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`</span><span class="sxs-lookup"><span data-stu-id="9ca16-154">Key location: Either the machine-wide `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` or if it's per-user installed templates and packages, alternatively use `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`</span></span>
    - <span data-ttu-id="9ca16-155">Anahtar adı: sizin için benzersiz bir ad kullanın.</span><span class="sxs-lookup"><span data-stu-id="9ca16-155">Key name: use a name that's unique to you.</span></span> <span data-ttu-id="9ca16-156">Örneğin, VS 2012 kullanmak için ASP.NET MVC 4 şablonları `AspNetMvc4VS11`.</span><span class="sxs-lookup"><span data-stu-id="9ca16-156">For example, the ASP.NET MVC 4 templates for VS 2012 use `AspNetMvc4VS11`.</span></span>
    - <span data-ttu-id="9ca16-157">Değerler: paketleri klasörün tam yolu.</span><span class="sxs-lookup"><span data-stu-id="9ca16-157">Values: the full path to the packages folder.</span></span>

1. <span data-ttu-id="9ca16-158">İçinde `<packages>` öğesinde `.vstemplate` öznitelik ekleyin `repository="registry"` ve kayıt defteri anahtarı adınızı belirtin `keyName` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="9ca16-158">In the `<packages>` element in the `.vstemplate` file, add the attribute `repository="registry"` and specify your registry key name in the `keyName` attribute.</span></span>

    - <span data-ttu-id="9ca16-159">Paketlerinizi önceden geçin kullanırsanız `isPreunzipped="true"` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="9ca16-159">If you have pre-unzipped your packages, use the `isPreunzipped="true"` attribute.</span></span>
    - <span data-ttu-id="9ca16-160">*(NuGet 3.2 +)*  Paket yükleme sonunda bir tasarım zamanı derleme zorlamak istiyorsanız ekleme `forceDesignTimeBuild="true"` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="9ca16-160">*(NuGet 3.2+)* If you want to force a design-time build at the end of package installation, add the `forceDesignTimeBuild="true"` attribute.</span></span>
    - <span data-ttu-id="9ca16-161">Bir iyileştirme ekleme `skipAssemblyReferences="true"` çünkü şablon zaten gerekli başvuruları içerir.</span><span class="sxs-lookup"><span data-stu-id="9ca16-161">As an optimization, add `skipAssemblyReferences="true"` because the template itself already includes the necessary references.</span></span>

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a><span data-ttu-id="9ca16-162">En İyi Yöntemler</span><span class="sxs-lookup"><span data-stu-id="9ca16-162">Best Practices</span></span>

1. <span data-ttu-id="9ca16-163">Bir bağımlılık, VSIX bildiriminizi buna bir başvuru ekleyerek NuGet VSIX üzerinde bildirin:</span><span class="sxs-lookup"><span data-stu-id="9ca16-163">Declare a dependency on the NuGet VSIX by adding a reference to it in your VSIX manifest:</span></span>

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. <span data-ttu-id="9ca16-164">Proje/öğe şablonları oluşturma dahil ederek kaydedilmesini gerektirir [ `<PromptForSaveOnCreation>true</PromptForSaveOnCreation>` ](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) içinde `.vstemplate` dosya.</span><span class="sxs-lookup"><span data-stu-id="9ca16-164">Require project/item templates to be saved on creation by including [`<PromptForSaveOnCreation>true</PromptForSaveOnCreation>`](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) in the `.vstemplate` file.</span></span>

1. <span data-ttu-id="9ca16-165">Şablonlar içermez bir `packages.config` dosya ve ekleme veya tüm başvuruları veya NuGet paketleri yüklendiğinde eklenir içeriği.</span><span class="sxs-lookup"><span data-stu-id="9ca16-165">Templates do not include a `packages.config` file, and do not include or any references or content that would be added when NuGet packages are installed.</span></span>
