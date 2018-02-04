---
title: "Visual Studio şablonları NuGet paketlerine | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/03/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet paketlerini Visual Studio Proje ve öğe şablonları bir parçası olarak dahil etmek için yönergeler."
keywords: NuGet in Visual Studio, Visual Studio project templates, Visual Studio item templates, packages in project templates, packages in item templates
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 65b914e1fa59c28615f195b470880a12bf80efbb
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/02/2018
---
# <a name="packages-in-visual-studio-templates"></a><span data-ttu-id="2be58-104">Visual Studio şablonları paketler</span><span class="sxs-lookup"><span data-stu-id="2be58-104">Packages in Visual Studio templates</span></span>

<span data-ttu-id="2be58-105">Visual Studio Proje ve öğe şablonları, genellikle bir proje veya öğesi oluşturulduğunda belirli paketleri yüklü olduğundan emin olun gerekir.</span><span class="sxs-lookup"><span data-stu-id="2be58-105">Visual Studio project and item templates often need to ensure that certain packages are installed when a project or item is created.</span></span> <span data-ttu-id="2be58-106">Örneğin, ASP.NET MVC 3 şablonu jQuery, Modernizr ve diğer paketleri yükler.</span><span class="sxs-lookup"><span data-stu-id="2be58-106">For example, the ASP.NET MVC 3 template installs jQuery, Modernizr, and other packages.</span></span>

<span data-ttu-id="2be58-107">Bunu desteklemek için şablon yazarlar tek tek kitaplıklarda yerine gerekli paketleri yüklemek için NuGet söyleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2be58-107">To support this, template authors can instruct NuGet to install the necessary packages, rather than individual libraries.</span></span> <span data-ttu-id="2be58-108">Geliştiriciler sonra kolayca bu paketleri daha sonraki bir zamanda güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2be58-108">Developers can then easily update those packages at any later time.</span></span>

<span data-ttu-id="2be58-109">Şablonların kendilerine yazma hakkında daha fazla bilgi için bkz [nasıl yapılır: Proje şablonları oluşturma](/visualstudio/ide/how-to-create-project-templates) veya [oluşturma özel Proje ve öğe şablonlarını](/visualstudio/extensibility/creating-custom-project-and-item-templates).</span><span class="sxs-lookup"><span data-stu-id="2be58-109">To learn more about authoring templates themselves, refer to [How to: Create Project Templates](/visualstudio/ide/how-to-create-project-templates) or [Creating Custom Project and Item Templates](/visualstudio/extensibility/creating-custom-project-and-item-templates).</span></span>

<span data-ttu-id="2be58-110">Bu bölüm geri kalanı düzgün NuGet paketleri dahil etmek için bir şablon yazarken uygulanacak belirli adımlar açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="2be58-110">The remainder of this section describes the specific steps to take when authoring a template to properly include NuGet packages.</span></span>

- [<span data-ttu-id="2be58-111">Bir şablona paketleri ekleme</span><span class="sxs-lookup"><span data-stu-id="2be58-111">Adding packages to a template</span></span>](#adding-packages-to-a-template)
- [<span data-ttu-id="2be58-112">En iyi uygulamalar</span><span class="sxs-lookup"><span data-stu-id="2be58-112">Best practices</span></span>](#best-practices)

<span data-ttu-id="2be58-113">Bir örnek için bkz: [NuGetInVsTemplates örnek](https://bitbucket.org/marcind/nugetinvstemplates).</span><span class="sxs-lookup"><span data-stu-id="2be58-113">For an example, see the [NuGetInVsTemplates sample](https://bitbucket.org/marcind/nugetinvstemplates).</span></span>

## <a name="adding-packages-to-a-template"></a><span data-ttu-id="2be58-114">Bir şablona paketleri ekleme</span><span class="sxs-lookup"><span data-stu-id="2be58-114">Adding packages to a template</span></span>

<span data-ttu-id="2be58-115">Şablon örneği oluşturulduğunda bir [Şablon Sihirbazı](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) bu paketleri nerede bulacağını hakkında bilgilerle birlikte yüklemek için olan paketlerin listesini yüklemek için çağrılır.</span><span class="sxs-lookup"><span data-stu-id="2be58-115">When a template is instantiated, a [template wizard](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) is invoked to load the list of packages to install along with information about where to find those packages.</span></span> <span data-ttu-id="2be58-116">Paket içinde VSIX içine katıştırılmış, şablonda katıştırılmış veya yerel sabit sürücüsünde bulunan bir kayıt defteri anahtarı dosya yolu başvurma kullanın; Bu durumda.</span><span class="sxs-lookup"><span data-stu-id="2be58-116">Packages can be embedded in the VSIX, embedded in the template, or located on the local hard drive in which case you use a registry key to reference the file path.</span></span> <span data-ttu-id="2be58-117">Bu konumları hakkında ayrıntılar daha sonra bu bölümde verilir.</span><span class="sxs-lookup"><span data-stu-id="2be58-117">Details on these locations are given later in this section.</span></span>

<span data-ttu-id="2be58-118">Önceden yüklenen paketler iş kullanarak [şablon sihirbazları](/visualstudio/extensibility/how-to-use-wizards-with-project-templates).</span><span class="sxs-lookup"><span data-stu-id="2be58-118">Preinstalled packages work using [template wizards](/visualstudio/extensibility/how-to-use-wizards-with-project-templates).</span></span> <span data-ttu-id="2be58-119">Şablon örneği özel sihirbaz çağrılır.</span><span class="sxs-lookup"><span data-stu-id="2be58-119">A special wizard gets invoked when the template gets instantiated.</span></span> <span data-ttu-id="2be58-120">Sihirbaz yüklenmesi gereken paketlerin listesini yükler ve bu bilgileri uygun NuGet API'leri geçirir.</span><span class="sxs-lookup"><span data-stu-id="2be58-120">The wizard loads the list of packages that need to be installed and passes that information to the appropriate NuGet APIs.</span></span>

<span data-ttu-id="2be58-121">Paketleri bir şablona dahil adımlar:</span><span class="sxs-lookup"><span data-stu-id="2be58-121">Steps to include packages in a template:</span></span>

1. <span data-ttu-id="2be58-122">İçinde `vstemplate` dosya, NuGet Şablon Sihirbazı'nı bir başvuru ekleyerek bir [ `WizardExtension` ](/visualstudio/extensibility/wizardextension-element-visual-studio-templates) öğe:</span><span class="sxs-lookup"><span data-stu-id="2be58-122">In your `vstemplate` file, add a reference to the NuGet template wizard by adding a [`WizardExtension`](/visualstudio/extensibility/wizardextension-element-visual-studio-templates) element:</span></span>

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    <span data-ttu-id="2be58-123">`NuGet.VisualStudio.Interop.dll`yalnızca içeren bir derleme `TemplateWizard` gerçek uygulamasında içine çağıran basit bir sarmalayıcı sınıfı `NuGet.VisualStudio.dll`.</span><span class="sxs-lookup"><span data-stu-id="2be58-123">`NuGet.VisualStudio.Interop.dll` is an assembly that contains only the `TemplateWizard` class, which is a simple wrapper that calls into the actual implementation in `NuGet.VisualStudio.dll`.</span></span> <span data-ttu-id="2be58-124">Proje/öğe şablonları NuGet yeni sürümleri ile çalışmaya devam derleme sürümünü hiçbir zaman değiştireceksiniz.</span><span class="sxs-lookup"><span data-stu-id="2be58-124">The assembly version will never change so that project/item templates continue to work with new versions of NuGet.</span></span>

1. <span data-ttu-id="2be58-125">Projede yüklemek için olan paketlerin listesini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="2be58-125">Add the list of packages to install in the project:</span></span>

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    <span data-ttu-id="2be58-126">*(NuGet 2.2.1+)*  Birden çok sihirbaz destekler `<package>` öğeleri birden çok paket kaynaklarını destekleyecek şekilde.</span><span class="sxs-lookup"><span data-stu-id="2be58-126">*(NuGet 2.2.1+)* The wizard supports multiple `<package>` elements to support multiple package sources.</span></span> <span data-ttu-id="2be58-127">Hem `id` ve `version` , belirli bir paketin sürümü anlamına yüklenecek daha yeni bir sürümü kullanılabilir olsa bile, öznitelikler gereklidir.</span><span class="sxs-lookup"><span data-stu-id="2be58-127">Both the `id` and `version` attributes are required, meaning that specific version of a package will be installed even if a newer version is available.</span></span> <span data-ttu-id="2be58-128">Bu, paket güncelleştirmesi şablon kullanılarak Geliştirici paketi güncelleştirmeye seçimi bırakarak şablon bozmasını engeller.</span><span class="sxs-lookup"><span data-stu-id="2be58-128">This prevents package updates from breaking the template, leaving the choice to update the package to the developer using the template.</span></span>

1. <span data-ttu-id="2be58-129">NuGet paketleri aşağıdaki bölümlerde açıklandığı gibi bulabileceğiniz deposu belirtin.</span><span class="sxs-lookup"><span data-stu-id="2be58-129">Specify the repository where NuGet can find the packages as described in the following sections.</span></span>

### <a name="vsix-package-repository"></a><span data-ttu-id="2be58-130">VSIX Paket Deposu</span><span class="sxs-lookup"><span data-stu-id="2be58-130">VSIX package repository</span></span>

<span data-ttu-id="2be58-131">Visual Studio Proje/öğesi şablonları için önerilen dağıtım yaklaşımdır bir [VSIX uzantısı](/visualstudio/extensibility/shipping-visual-studio-extensions) çünkü birden çok proje/öğe şablonları birlikte paketlemenize olanak sağlar ve geliştiricilerin şablonlarınızı kolay bulmasına olanak tanır VS Uzantı Yöneticisi'ni veya Visual Studio Galerisi kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="2be58-131">The recommended deployment approach for Visual Studio project/item templates is a [VSIX extension](/visualstudio/extensibility/shipping-visual-studio-extensions) because it allows you to package multiple project/item templates together and allows developers to easily discover your templates using the VS Extension Manager or the Visual Studio Gallery.</span></span> <span data-ttu-id="2be58-132">Uzantı için güncelleştirmelerin de kullanarak dağıtmak kolay [Visual Studio Uzantı Yöneticisi otomatik güncelleştirme mekanizmasını](/visualstudio/extensibility/how-to-update-a-visual-studio-extension).</span><span class="sxs-lookup"><span data-stu-id="2be58-132">Updates to the extension are also easy to deploy using the [Visual Studio Extension Manager automatic update mechanism](/visualstudio/extensibility/how-to-update-a-visual-studio-extension).</span></span>

<span data-ttu-id="2be58-133">VSIX şablon tarafından gereken paketler için kaynak olarak hizmet verebilir:</span><span class="sxs-lookup"><span data-stu-id="2be58-133">The VSIX itself can serve as the source for packages required by the template:</span></span>

1. <span data-ttu-id="2be58-134">Değiştirme `<packages>` öğesinde `.vstemplate` gibi dosya:</span><span class="sxs-lookup"><span data-stu-id="2be58-134">Modify the `<packages>` element in the `.vstemplate` file as follows:</span></span>

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    <span data-ttu-id="2be58-135">`repository` Öznitelik deposu olarak türünü belirtir `extension` sırada `repositoryId` VSIX benzersiz tanıtıcısı (Bu değeri `ID` uzantının özniteliğinde `vsixmanifest` dosya için bkz: [ VSIX uzantı şema 2.0 başvurusu](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).</span><span class="sxs-lookup"><span data-stu-id="2be58-135">The `repository` attribute specifies the type of repository as `extension` while `repositoryId` is the unique identifier of the VSIX itself (This is the value of the `ID` attribute in the extension’s `vsixmanifest` file, see [VSIX Extension Schema 2.0 Reference](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).</span></span>

1. <span data-ttu-id="2be58-136">Yerleştir, `nupkg` bir klasördeki dosyaları adlı `Packages` VSIX içinde.</span><span class="sxs-lookup"><span data-stu-id="2be58-136">Place your `nupkg` files in a folder called `Packages` within the VSIX.</span></span>

1. <span data-ttu-id="2be58-137">Gerekli paket dosyaları olarak ekleme `<Asset>` içinde `vsixmanifest` dosyası (bkz [VSIX uzantı şema 2.0 başvurusu](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)):</span><span class="sxs-lookup"><span data-stu-id="2be58-137">Add the necessary package files as `<Asset>` in your `vsixmanifest` file (see [VSIX Extension Schema 2.0 Reference](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)):</span></span>

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

1. <span data-ttu-id="2be58-138">Proje şablonları olarak aynı VSIX içinde paketler sağlayabilir veya, daha fazla senaryonuz için mantıklı varsa bunları ayrı içinde VSIX içine koyabilirsiniz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="2be58-138">Note that you can deliver packages in the same VSIX as your project templates or you can put them in a separate VSIX if that makes more sense for your scenario.</span></span> <span data-ttu-id="2be58-139">Ancak, uzantının değişiklikler şablonunuzu uğratabilir olduğundan üzerinde denetim, elinizde VSIX başvuruda bulunmayın.</span><span class="sxs-lookup"><span data-stu-id="2be58-139">However, do not reference any VSIX over which you do not have control, because changes to that extension could break your template.</span></span>

### <a name="template-package-repository"></a><span data-ttu-id="2be58-140">Şablon Paket Deposu</span><span class="sxs-lookup"><span data-stu-id="2be58-140">Template package repository</span></span>

<span data-ttu-id="2be58-141">Yalnızca bir tek proje öğesi şablon dağıtma ve birden fazla şablon birlikte paketini gerekmez, doğrudan proje/öğesi şablon ZIP dosyasında paketlerini içeren daha basit ancak daha kısıtlı bir yaklaşım kullanarak şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2be58-141">If you are distributing only a single project/item template and do not need to package multiple templates together, you can use a simpler but more limited approach that includes packages directly in the project/item template ZIP file:</span></span>

1. <span data-ttu-id="2be58-142">Değiştirme `<packages>` öğesinde `.vstemplate` gibi dosya:</span><span class="sxs-lookup"><span data-stu-id="2be58-142">Modify the `<packages>` element in the `.vstemplate` file as follows:</span></span>

    ```xml
    <packages repository="template"">
        <!-- ... -->
    </packages>
    ```

    <span data-ttu-id="2be58-143">`repository` Özniteliğine sahip değer `template` ve `repositoryId` özniteliği gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="2be58-143">The `repository` attribute has the value `template` and the `repositoryId` attribute is not required.</span></span>

1. <span data-ttu-id="2be58-144">Paketler proje/öğesi şablon ZIP dosyası kök klasörüne yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="2be58-144">Place packages in the root folder of the project/item template ZIP file.</span></span>

<span data-ttu-id="2be58-145">Bir veya daha fazla paket şablonların ortak olduğunda bu yaklaşımı kullanarak birden fazla şablon içeren bir VSIX gereksiz oluşan şişirmeyi müşteri adayları olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="2be58-145">Note that using this approach in a VSIX that contains multiple templates leads to unnecessary bloat when one or more packages are common to the templates.</span></span> <span data-ttu-id="2be58-146">Bu gibi durumlarda kullanmak [VSIX deposu olarak](#vsix-package-repository) önceki bölümde açıklandığı gibi.</span><span class="sxs-lookup"><span data-stu-id="2be58-146">In such cases, use the [VSIX as the repository](#vsix-package-repository) as described in the previous section.</span></span>

### <a name="registry-specified-folder-path"></a><span data-ttu-id="2be58-147">Kayıt defteri tarafından belirtilen klasör yolu</span><span class="sxs-lookup"><span data-stu-id="2be58-147">Registry-specified folder path</span></span>

<span data-ttu-id="2be58-148">Bir MSI kullanılarak yüklenen SDK'ları doğrudan geliştiricinin makinesinde NuGet paketlerini yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2be58-148">SDKs that are installed using an MSI can install NuGet packages directly on the developer's machine.</span></span> <span data-ttu-id="2be58-149">Bunları hemen kullanılabilir bir öğe veya proje şablonu kullanılır bu yapar yerine bu süre boyunca ayıklanacak sahip.</span><span class="sxs-lookup"><span data-stu-id="2be58-149">This makes them immediately available when a project or item template is used, rather than having to extract them during that time.</span></span> <span data-ttu-id="2be58-150">ASP.NET şablonlar bu yaklaşımı kullanın.</span><span class="sxs-lookup"><span data-stu-id="2be58-150">ASP.NET templates use this approach.</span></span>

1. <span data-ttu-id="2be58-151">Paketleri yüklemek için makine MSI vardır.</span><span class="sxs-lookup"><span data-stu-id="2be58-151">Have the MSI install packages to the machine.</span></span> <span data-ttu-id="2be58-152">Yalnızca yükleyebilirsiniz `.nupkg` dosyaları, veya yükleyebilirsiniz genişletilmiş içeriği yanı sıra bu şablon kullanıldığında, ek bir adım kaydeder.</span><span class="sxs-lookup"><span data-stu-id="2be58-152">You can install only the `.nupkg` files, or you can install those along with the expanded contents, which saves an additional step when the template is used.</span></span> <span data-ttu-id="2be58-153">Bu durumda, NuGet'ın standart klasör yapısı; burada görüntülerle izleyin `.nupkg` dosyaları kök klasöründe ve ardından her bir paket kimliği/sürüm çifti alt klasör adı olarak bir alt klasörü vardır.</span><span class="sxs-lookup"><span data-stu-id="2be58-153">In this case, follow NuGet's standard folder structure wherein the `.nupkg` files are in the root folder, and then each package has a subfolder with the id/version pair as the subfolder name.</span></span>

1. <span data-ttu-id="2be58-154">Paket konumu tanımlamak için bir kayıt defteri anahtarı yazın:</span><span class="sxs-lookup"><span data-stu-id="2be58-154">Write a registry key to identify the package location:</span></span>

    - <span data-ttu-id="2be58-155">Anahtar konumu: her iki makine genelinde `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` veya kullanıcı başına yüklenmiş şablonlar ve paketleri ise, bunun yerine kullanın`HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`</span><span class="sxs-lookup"><span data-stu-id="2be58-155">Key location: Either the machine-wide `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` or if it's per-user installed templates and packages, alternatively use `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`</span></span>
    - <span data-ttu-id="2be58-156">Anahtar adı: için benzersiz bir ad kullanın.</span><span class="sxs-lookup"><span data-stu-id="2be58-156">Key name: use a name that's unique to you.</span></span> <span data-ttu-id="2be58-157">Örneğin, VS 2012 kullanmak için ASP.NET MVC 4 şablonları `AspNetMvc4VS11`.</span><span class="sxs-lookup"><span data-stu-id="2be58-157">For example, the ASP.NET MVC 4 templates for VS 2012 use `AspNetMvc4VS11`.</span></span>
    - <span data-ttu-id="2be58-158">Değerler: klasörün tam yolunu paketler.</span><span class="sxs-lookup"><span data-stu-id="2be58-158">Values: the full path to the packages folder.</span></span>

1. <span data-ttu-id="2be58-159">İçinde `<packages>` öğesinde `.vstemplate` dosya, öznitelik Ekle `repository="registry"` ve kayıt defteri anahtarı adınızı belirtmek `keyName` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="2be58-159">In the `<packages>` element in the `.vstemplate` file, add the attribute `repository="registry"` and specify your registry key name in the `keyName` attribute.</span></span>

    - <span data-ttu-id="2be58-160">Paketlerinizi önceden unzipped kullanırsanız `isPreunzipped="true"` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="2be58-160">If you have pre-unzipped your packages, use the `isPreunzipped="true"` attribute.</span></span>
    - <span data-ttu-id="2be58-161">*(NuGet 3.2 +)*  Tasarım zamanı yapı paket yükleme işleminin sonunda zorlamak istiyorsanız, eklemeniz `forceDesignTimeBuild="true"` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="2be58-161">*(NuGet 3.2+)* If you want to force a design-time build at the end of package installation, add the `forceDesignTimeBuild="true"` attribute.</span></span>
    - <span data-ttu-id="2be58-162">Bir iyileştirme ekleme `skipAssemblyReferences="true"` şablon gerekli başvurular içerdiğinden.</span><span class="sxs-lookup"><span data-stu-id="2be58-162">As an optimization, add `skipAssemblyReferences="true"` because the template itself already includes the necessary references.</span></span>

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a><span data-ttu-id="2be58-163">En İyi Yöntemler</span><span class="sxs-lookup"><span data-stu-id="2be58-163">Best Practices</span></span>

1. <span data-ttu-id="2be58-164">Bir bağımlılık VSIX bildiriminizi bir başvuru ekleyerek NuGet VSIX bildirin:</span><span class="sxs-lookup"><span data-stu-id="2be58-164">Declare a dependency on the NuGet VSIX by adding a reference to it in your VSIX manifest:</span></span>

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. <span data-ttu-id="2be58-165">Proje/öğe şablonları oluşturma dahil ederek kaydedilmesini gerektirir [ `<PromptForSaveOnCreation>true</PromptForSaveOnCreation>` ](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) içinde `.vstemplate` dosya.</span><span class="sxs-lookup"><span data-stu-id="2be58-165">Require project/item templates to be saved on creation by including [`<PromptForSaveOnCreation>true</PromptForSaveOnCreation>`](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) in the `.vstemplate` file.</span></span>

1. <span data-ttu-id="2be58-166">Şablonları içermeyen bir `packages.config` dosya ve eklemeyin veya tüm başvuruları veya NuGet paketleri yüklendiğinde ekleneceği içerik.</span><span class="sxs-lookup"><span data-stu-id="2be58-166">Templates do not include a `packages.config` file, and do not include or any references or content that would be added when NuGet packages are installed.</span></span>
