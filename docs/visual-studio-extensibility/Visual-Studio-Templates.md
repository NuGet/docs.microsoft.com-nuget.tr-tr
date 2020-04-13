---
title: Görsel Stüdyo şablonlarında NuGet Paketleri
description: Visual Studio projesinin ve öğe şablonlarının bir parçası olarak NuGet paketlerini dahil etme yönergeleri.
author: karann-msft
ms.author: karann
ms.date: 01/03/2018
ms.topic: conceptual
ms.openlocfilehash: be7c10fb6ce60375f77e38f9b604ec33063e52fc
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64498244"
---
# <a name="packages-in-visual-studio-templates"></a><span data-ttu-id="bc8a3-103">Visual Studio şablonlarında paketler</span><span class="sxs-lookup"><span data-stu-id="bc8a3-103">Packages in Visual Studio templates</span></span>

<span data-ttu-id="bc8a3-104">Visual Studio proje ve öğe şablonları genellikle bir proje veya öğe oluşturulduğunda belirli paketlerin yüklendiğinden emin olmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="bc8a3-104">Visual Studio project and item templates often need to ensure that certain packages are installed when a project or item is created.</span></span> <span data-ttu-id="bc8a3-105">Örneğin, ASP.NET MVC 3 şablonu jQuery, Modernizr ve diğer paketleri yükler.</span><span class="sxs-lookup"><span data-stu-id="bc8a3-105">For example, the ASP.NET MVC 3 template installs jQuery, Modernizr, and other packages.</span></span>

<span data-ttu-id="bc8a3-106">Bunu desteklemek için, şablon yazarları NuGet'e tek tek kitaplıklar yerine gerekli paketleri yüklemesini talimat verebilir.</span><span class="sxs-lookup"><span data-stu-id="bc8a3-106">To support this, template authors can instruct NuGet to install the necessary packages, rather than individual libraries.</span></span> <span data-ttu-id="bc8a3-107">Geliştiriciler daha sonra bu paketleri kolayca güncelleyebilir.</span><span class="sxs-lookup"><span data-stu-id="bc8a3-107">Developers can then easily update those packages at any later time.</span></span>

<span data-ttu-id="bc8a3-108">Şablonları yazma hakkında daha fazla bilgi edinmek için nasıl [yazabilirsiniz: Proje Şablonları Oluşturma](/visualstudio/ide/how-to-create-project-templates) veya [Özel Proje ve Öğe Şablonları Oluşturma'ya](/visualstudio/extensibility/creating-custom-project-and-item-templates)bakın.</span><span class="sxs-lookup"><span data-stu-id="bc8a3-108">To learn more about authoring templates themselves, refer to [How to: Create Project Templates](/visualstudio/ide/how-to-create-project-templates) or [Creating Custom Project and Item Templates](/visualstudio/extensibility/creating-custom-project-and-item-templates).</span></span>

<span data-ttu-id="bc8a3-109">Bu bölümün geri kalanı, NuGet paketlerini düzgün bir şekilde içerecek şekilde bir şablon yazarken atılması gereken belirli adımları açıklar.</span><span class="sxs-lookup"><span data-stu-id="bc8a3-109">The remainder of this section describes the specific steps to take when authoring a template to properly include NuGet packages.</span></span>

- [<span data-ttu-id="bc8a3-110">Şablona paket ekleme</span><span class="sxs-lookup"><span data-stu-id="bc8a3-110">Adding packages to a template</span></span>](#adding-packages-to-a-template)
- [<span data-ttu-id="bc8a3-111">En iyi uygulamalar</span><span class="sxs-lookup"><span data-stu-id="bc8a3-111">Best practices</span></span>](#best-practices)

<span data-ttu-id="bc8a3-112">Örneğin, [NuGetInVsTemplates örneğine](https://bitbucket.org/marcind/nugetinvstemplates)bakın.</span><span class="sxs-lookup"><span data-stu-id="bc8a3-112">For an example, see the [NuGetInVsTemplates sample](https://bitbucket.org/marcind/nugetinvstemplates).</span></span>

## <a name="adding-packages-to-a-template"></a><span data-ttu-id="bc8a3-113">Şablona paket ekleme</span><span class="sxs-lookup"><span data-stu-id="bc8a3-113">Adding packages to a template</span></span>

<span data-ttu-id="bc8a3-114">Bir şablon anında çağrıldığında, bu paketlerin nerede bulunacağı yla ilgili bilgilerle birlikte yüklenmesi gereken paketlerlistesini yüklemek için bir [şablon sihirbazı](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) çağrılır.</span><span class="sxs-lookup"><span data-stu-id="bc8a3-114">When a template is instantiated, a [template wizard](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) is invoked to load the list of packages to install along with information about where to find those packages.</span></span> <span data-ttu-id="bc8a3-115">Paketler VSIX'ye katıştılabilir, şablona katıştılabilir veya yerel sabit diskte bulunabilir ve bu durumda dosya yoluna başvurmak için bir kayıt defteri anahtarı kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="bc8a3-115">Packages can be embedded in the VSIX, embedded in the template, or located on the local hard drive in which case you use a registry key to reference the file path.</span></span> <span data-ttu-id="bc8a3-116">Bu konumlarla ilgili ayrıntılar daha sonra bu bölümde verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="bc8a3-116">Details on these locations are given later in this section.</span></span>

<span data-ttu-id="bc8a3-117">Önceden yüklenmiş paketler [şablon sihirbazlarını](/visualstudio/extensibility/how-to-use-wizards-with-project-templates)kullanarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="bc8a3-117">Preinstalled packages work using [template wizards](/visualstudio/extensibility/how-to-use-wizards-with-project-templates).</span></span> <span data-ttu-id="bc8a3-118">Şablon anında olduğunda özel bir sihirbaz çağrılır.</span><span class="sxs-lookup"><span data-stu-id="bc8a3-118">A special wizard gets invoked when the template gets instantiated.</span></span> <span data-ttu-id="bc8a3-119">Sihirbaz, yüklenmesi gereken paketlerin listesini yükler ve bu bilgileri ilgili NuGet API'lerine aktarır.</span><span class="sxs-lookup"><span data-stu-id="bc8a3-119">The wizard loads the list of packages that need to be installed and passes that information to the appropriate NuGet APIs.</span></span>

<span data-ttu-id="bc8a3-120">Şablona paketleri ekleme adımları:</span><span class="sxs-lookup"><span data-stu-id="bc8a3-120">Steps to include packages in a template:</span></span>

1. <span data-ttu-id="bc8a3-121">Dosyanızda, `vstemplate` bir [`WizardExtension`](/visualstudio/extensibility/wizardextension-element-visual-studio-templates) öğe ekleyerek NuGet şablonu sihirbazına bir başvuru ekleyin:</span><span class="sxs-lookup"><span data-stu-id="bc8a3-121">In your `vstemplate` file, add a reference to the NuGet template wizard by adding a [`WizardExtension`](/visualstudio/extensibility/wizardextension-element-visual-studio-templates) element:</span></span>

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    <span data-ttu-id="bc8a3-122">`NuGet.VisualStudio.Interop.dll`yalnızca `TemplateWizard` sınıfı içeren bir derlemedir, bu da `NuGet.VisualStudio.dll`'daki gerçek uygulamaya çağıran basit bir sarıcıdır.</span><span class="sxs-lookup"><span data-stu-id="bc8a3-122">`NuGet.VisualStudio.Interop.dll` is an assembly that contains only the `TemplateWizard` class, which is a simple wrapper that calls into the actual implementation in `NuGet.VisualStudio.dll`.</span></span> <span data-ttu-id="bc8a3-123">Proje/öğe şablonlarının NuGet'in yeni sürümleriyle çalışmaya devam etmesi için derleme sürümü asla değişmez.</span><span class="sxs-lookup"><span data-stu-id="bc8a3-123">The assembly version will never change so that project/item templates continue to work with new versions of NuGet.</span></span>

1. <span data-ttu-id="bc8a3-124">Projeye yüklenmesi gereken paketlerin listesini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="bc8a3-124">Add the list of packages to install in the project:</span></span>

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    <span data-ttu-id="bc8a3-125">Sihirbaz, birden `<package>` çok paket kaynağını desteklemek için birden çok öğeyi destekler.</span><span class="sxs-lookup"><span data-stu-id="bc8a3-125">The wizard supports multiple `<package>` elements to support multiple package sources.</span></span> <span data-ttu-id="bc8a3-126">Hem `id` öznitelikleri hem `version` de öznitelikleri gereklidir, yani yeni bir sürüm mevcut olsa bile paketin belirli bir sürümü yüklenir.</span><span class="sxs-lookup"><span data-stu-id="bc8a3-126">Both the `id` and `version` attributes are required, meaning that specific version of a package will be installed even if a newer version is available.</span></span> <span data-ttu-id="bc8a3-127">Bu, paket güncelleştirmelerinin şablonu bozmasını önler ve şablonu kullanarak paketi geliştiriciye güncelleştirme seçeneğibırakır.</span><span class="sxs-lookup"><span data-stu-id="bc8a3-127">This prevents package updates from breaking the template, leaving the choice to update the package to the developer using the template.</span></span>

1. <span data-ttu-id="bc8a3-128">NuGet'in aşağıdaki bölümlerde açıklandığı şekilde paketleri bulabileceği depoyu belirtin.</span><span class="sxs-lookup"><span data-stu-id="bc8a3-128">Specify the repository where NuGet can find the packages as described in the following sections.</span></span>

### <a name="vsix-package-repository"></a><span data-ttu-id="bc8a3-129">VSIX paket deposu</span><span class="sxs-lookup"><span data-stu-id="bc8a3-129">VSIX package repository</span></span>

<span data-ttu-id="bc8a3-130">Visual Studio proje/öğe şablonları için önerilen dağıtım yaklaşımı, birden çok proje/öğe şablonunu birlikte paketlemenize ve geliştiricilerin VS Extension Manager veya Visual Studio Gallery'yi kullanarak şablonlarınızı kolayca keşfetmenize olanak sağladığından bir [VSIX uzantısıdır.](/visualstudio/extensibility/shipping-visual-studio-extensions)</span><span class="sxs-lookup"><span data-stu-id="bc8a3-130">The recommended deployment approach for Visual Studio project/item templates is a [VSIX extension](/visualstudio/extensibility/shipping-visual-studio-extensions) because it allows you to package multiple project/item templates together and allows developers to easily discover your templates using the VS Extension Manager or the Visual Studio Gallery.</span></span> <span data-ttu-id="bc8a3-131">Uzantı güncellemeleri de Visual Studio [Extension Manager otomatik güncelleme mekanizmasını](/visualstudio/extensibility/how-to-update-a-visual-studio-extension)kullanarak dağıtmak kolaydır.</span><span class="sxs-lookup"><span data-stu-id="bc8a3-131">Updates to the extension are also easy to deploy using the [Visual Studio Extension Manager automatic update mechanism](/visualstudio/extensibility/how-to-update-a-visual-studio-extension).</span></span>

<span data-ttu-id="bc8a3-132">VSIX kendisi şablon tarafından gerekli paketler için kaynak olarak hizmet verebilir:</span><span class="sxs-lookup"><span data-stu-id="bc8a3-132">The VSIX itself can serve as the source for packages required by the template:</span></span>

1. <span data-ttu-id="bc8a3-133">Dosyadaki `<packages>` öğeyi `.vstemplate` aşağıdaki gibi değiştirin:</span><span class="sxs-lookup"><span data-stu-id="bc8a3-133">Modify the `<packages>` element in the `.vstemplate` file as follows:</span></span>

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    <span data-ttu-id="bc8a3-134">Öznitelik, `repository` Depo türünü VSIX'nin kendisinin `extension` `repositoryId` benzersiz tanımlayıcısı olarak belirtir (Bu, uzantının `ID` `vsixmanifest` dosyasındaki özniteliğin değeridir, bkz. [VSIX Extension Schema 2.0 Reference).](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)</span><span class="sxs-lookup"><span data-stu-id="bc8a3-134">The `repository` attribute specifies the type of repository as `extension` while `repositoryId` is the unique identifier of the VSIX itself (This is the value of the `ID` attribute in the extension’s `vsixmanifest` file, see [VSIX Extension Schema 2.0 Reference](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).</span></span>

1. <span data-ttu-id="bc8a3-135">Dosyalarınızı `nupkg` VSIX içinde `Packages` adı verilen bir klasöre yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="bc8a3-135">Place your `nupkg` files in a folder called `Packages` within the VSIX.</span></span>

1. <span data-ttu-id="bc8a3-136">Dosyanızda `vsixmanifest` olduğu gibi `<Asset>` gerekli paket dosyalarını ekleyin (bkz. [VSIX Extension Schema 2.0 Reference):](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)</span><span class="sxs-lookup"><span data-stu-id="bc8a3-136">Add the necessary package files as `<Asset>` in your `vsixmanifest` file (see [VSIX Extension Schema 2.0 Reference](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)):</span></span>

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

1. <span data-ttu-id="bc8a3-137">Paketleri proje şablonlarınızla aynı VSIX'de teslim edebileceğinizi veya senaryonuz için daha mantıklıysa bunları ayrı bir VSIX'ye koyabileceğinizi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="bc8a3-137">Note that you can deliver packages in the same VSIX as your project templates or you can put them in a separate VSIX if that makes more sense for your scenario.</span></span> <span data-ttu-id="bc8a3-138">Ancak, bu uzantıdaki değişiklikler şablonunuzu kırabileceğinden, üzerinde denetiminiz olmayan herhangi bir VSIX'ye başvuruyapmayın.</span><span class="sxs-lookup"><span data-stu-id="bc8a3-138">However, do not reference any VSIX over which you do not have control, because changes to that extension could break your template.</span></span>

### <a name="template-package-repository"></a><span data-ttu-id="bc8a3-139">Şablon paket deposu</span><span class="sxs-lookup"><span data-stu-id="bc8a3-139">Template package repository</span></span>

<span data-ttu-id="bc8a3-140">Yalnızca tek bir proje/öğe şablonu dağıtıyorsanız ve birden çok şablonu birlikte paketlemeniz gerekmiyorsa, paketleri doğrudan proje/öğe şablonu ZIP dosyasında içeren daha basit ancak daha sınırlı bir yaklaşım kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bc8a3-140">If you are distributing only a single project/item template and do not need to package multiple templates together, you can use a simpler but more limited approach that includes packages directly in the project/item template ZIP file:</span></span>

1. <span data-ttu-id="bc8a3-141">Dosyadaki `<packages>` öğeyi `.vstemplate` aşağıdaki gibi değiştirin:</span><span class="sxs-lookup"><span data-stu-id="bc8a3-141">Modify the `<packages>` element in the `.vstemplate` file as follows:</span></span>

    ```xml
    <packages repository="template"">
        <!-- ... -->
    </packages>
    ```

    <span data-ttu-id="bc8a3-142">Öznitelik `repository` değeri `template` vardır ve `repositoryId` öznitelik gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="bc8a3-142">The `repository` attribute has the value `template` and the `repositoryId` attribute is not required.</span></span>

1. <span data-ttu-id="bc8a3-143">Paketleri proje/öğe şablonu ZIP dosyasının kök klasörüne yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="bc8a3-143">Place packages in the root folder of the project/item template ZIP file.</span></span>

<span data-ttu-id="bc8a3-144">Birden çok şablon içeren bir VSIX'de bu yaklaşımın kullanılmasının, şablonlarda bir veya daha fazla paket ortak olduğunda gereksiz şişkinliğe yol açtığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="bc8a3-144">Note that using this approach in a VSIX that contains multiple templates leads to unnecessary bloat when one or more packages are common to the templates.</span></span> <span data-ttu-id="bc8a3-145">Bu gibi durumlarda, önceki bölümde açıklandığı [gibi depo olarak VSIX](#vsix-package-repository) kullanın.</span><span class="sxs-lookup"><span data-stu-id="bc8a3-145">In such cases, use the [VSIX as the repository](#vsix-package-repository) as described in the previous section.</span></span>

### <a name="registry-specified-folder-path"></a><span data-ttu-id="bc8a3-146">Kayıt defteri tarafından belirtilen klasör yolu</span><span class="sxs-lookup"><span data-stu-id="bc8a3-146">Registry-specified folder path</span></span>

<span data-ttu-id="bc8a3-147">MSI kullanılarak yüklenen SDK'lar NuGet paketlerini doğrudan geliştiricinin makinesine yükleyebilir.</span><span class="sxs-lookup"><span data-stu-id="bc8a3-147">SDKs that are installed using an MSI can install NuGet packages directly on the developer's machine.</span></span> <span data-ttu-id="bc8a3-148">Bu, bu süre içinde ayıklamak zorunda kalmak yerine, bir proje veya öğe şablonu kullanıldığında onları hemen kullanılabilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="bc8a3-148">This makes them immediately available when a project or item template is used, rather than having to extract them during that time.</span></span> <span data-ttu-id="bc8a3-149">ASP.NET şablonları bu yaklaşımı kullanır.</span><span class="sxs-lookup"><span data-stu-id="bc8a3-149">ASP.NET templates use this approach.</span></span>

1. <span data-ttu-id="bc8a3-150">MSI'ın paketlerini makineye yüklemesini.</span><span class="sxs-lookup"><span data-stu-id="bc8a3-150">Have the MSI install packages to the machine.</span></span> <span data-ttu-id="bc8a3-151">Yalnızca `.nupkg` dosyaları yükleyebilirsiniz veya şablon kullanıldığında ek bir adım kaydeden genişletilmiş içeriklerle birlikte bunları yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc8a3-151">You can install only the `.nupkg` files, or you can install those along with the expanded contents, which saves an additional step when the template is used.</span></span> <span data-ttu-id="bc8a3-152">Bu durumda, `.nupkg` dosyaların kök klasöründe olduğu NuGet'in standart klasör yapısını izleyin ve ardından her paketin alt klasör adı olarak id/sürüm çiftinin yer aldığı bir alt klasörü vardır.</span><span class="sxs-lookup"><span data-stu-id="bc8a3-152">In this case, follow NuGet's standard folder structure wherein the `.nupkg` files are in the root folder, and then each package has a subfolder with the id/version pair as the subfolder name.</span></span>

1. <span data-ttu-id="bc8a3-153">Paket konumunu belirlemek için bir kayıt defteri anahtarı yazın:</span><span class="sxs-lookup"><span data-stu-id="bc8a3-153">Write a registry key to identify the package location:</span></span>

    - <span data-ttu-id="bc8a3-154">Anahtar konumu: Makine genelinde `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` veya kullanıcı başına yüklenen şablonlar ve paketler varsa, alternatif olarak`HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`</span><span class="sxs-lookup"><span data-stu-id="bc8a3-154">Key location: Either the machine-wide `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` or if it's per-user installed templates and packages, alternatively use `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`</span></span>
    - <span data-ttu-id="bc8a3-155">Anahtar adı: size özgü bir ad kullanın.</span><span class="sxs-lookup"><span data-stu-id="bc8a3-155">Key name: use a name that's unique to you.</span></span> <span data-ttu-id="bc8a3-156">Örneğin, VS 2012 için mvc 4 `AspNetMvc4VS11`şablonları ASP.NET kullanın.</span><span class="sxs-lookup"><span data-stu-id="bc8a3-156">For example, the ASP.NET MVC 4 templates for VS 2012 use `AspNetMvc4VS11`.</span></span>
    - <span data-ttu-id="bc8a3-157">Değerler: paketler klasörüne tam yol.</span><span class="sxs-lookup"><span data-stu-id="bc8a3-157">Values: the full path to the packages folder.</span></span>

1. <span data-ttu-id="bc8a3-158">Dosyadaki `<packages>` öğede `repository="registry"` özniteliği ekleyin ve öznitelikte kayıt defteri anahtar adınızı belirtin. `keyName` `.vstemplate`</span><span class="sxs-lookup"><span data-stu-id="bc8a3-158">In the `<packages>` element in the `.vstemplate` file, add the attribute `repository="registry"` and specify your registry key name in the `keyName` attribute.</span></span>

    - <span data-ttu-id="bc8a3-159">Paketlerinizi önceden fermuarsız olarak açtıysanız, özniteliği kullanın. `isPreunzipped="true"`</span><span class="sxs-lookup"><span data-stu-id="bc8a3-159">If you have pre-unzipped your packages, use the `isPreunzipped="true"` attribute.</span></span>
    - <span data-ttu-id="bc8a3-160">*(NuGet 3.2+)* Paket yüklemesinin sonunda bir tasarım zamanı oluşturmayı zorlamak istiyorsanız, özniteliği ekleyin. `forceDesignTimeBuild="true"`</span><span class="sxs-lookup"><span data-stu-id="bc8a3-160">*(NuGet 3.2+)* If you want to force a design-time build at the end of package installation, add the `forceDesignTimeBuild="true"` attribute.</span></span>
    - <span data-ttu-id="bc8a3-161">Bir optimizasyon olarak, `skipAssemblyReferences="true"` şablonun kendisi zaten gerekli başvuruları içerdiğinden ekleyin.</span><span class="sxs-lookup"><span data-stu-id="bc8a3-161">As an optimization, add `skipAssemblyReferences="true"` because the template itself already includes the necessary references.</span></span>

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a><span data-ttu-id="bc8a3-162">En İyi Uygulamalar</span><span class="sxs-lookup"><span data-stu-id="bc8a3-162">Best Practices</span></span>

1. <span data-ttu-id="bc8a3-163">VSIX bildiriminizde bir referans ekleyerek NuGet VSIX'ye bir bağımlılık bildirin:</span><span class="sxs-lookup"><span data-stu-id="bc8a3-163">Declare a dependency on the NuGet VSIX by adding a reference to it in your VSIX manifest:</span></span>

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. <span data-ttu-id="bc8a3-164">`.vstemplate` Dosyaya ekleyerek [`<PromptForSaveOnCreation>true</PromptForSaveOnCreation>`](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) proje/öğe şablonlarının oluşturma üzerine kaydedilmesini zorunlu kılmasını zorunlu kınla.</span><span class="sxs-lookup"><span data-stu-id="bc8a3-164">Require project/item templates to be saved on creation by including [`<PromptForSaveOnCreation>true</PromptForSaveOnCreation>`](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) in the `.vstemplate` file.</span></span>

1. <span data-ttu-id="bc8a3-165">Şablonlar bir `packages.config` dosya içermez ve NuGet paketleri yüklendiğinde eklenecek başvuruları veya içeriği içermez.</span><span class="sxs-lookup"><span data-stu-id="bc8a3-165">Templates do not include a `packages.config` file, and do not include or any references or content that would be added when NuGet packages are installed.</span></span>
