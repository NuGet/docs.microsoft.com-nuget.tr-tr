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
# <a name="packages-in-visual-studio-templates"></a>Visual Studio şablonları paketler

Visual Studio Proje ve öğe şablonları, genellikle bir proje veya öğesi oluşturulduğunda belirli paketleri yüklü olduğundan emin olun gerekir. Örneğin, ASP.NET MVC 3 şablonu jQuery, Modernizr ve diğer paketleri yükler.

Bunu desteklemek için şablon yazarlar tek tek kitaplıklarda yerine gerekli paketleri yüklemek için NuGet söyleyebilirsiniz. Geliştiriciler sonra kolayca bu paketleri daha sonraki bir zamanda güncelleştirebilirsiniz.

Şablonların kendilerine yazma hakkında daha fazla bilgi için bkz [nasıl yapılır: Proje şablonları oluşturma](/visualstudio/ide/how-to-create-project-templates) veya [oluşturma özel Proje ve öğe şablonlarını](/visualstudio/extensibility/creating-custom-project-and-item-templates).

Bu bölüm geri kalanı düzgün NuGet paketleri dahil etmek için bir şablon yazarken uygulanacak belirli adımlar açıklanmaktadır.

- [Bir şablona paketleri ekleme](#adding-packages-to-a-template)
- [En iyi uygulamalar](#best-practices)

Bir örnek için bkz: [NuGetInVsTemplates örnek](https://bitbucket.org/marcind/nugetinvstemplates).

## <a name="adding-packages-to-a-template"></a>Bir şablona paketleri ekleme

Şablon örneği oluşturulduğunda bir [Şablon Sihirbazı](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) bu paketleri nerede bulacağını hakkında bilgilerle birlikte yüklemek için olan paketlerin listesini yüklemek için çağrılır. Paket içinde VSIX içine katıştırılmış, şablonda katıştırılmış veya yerel sabit sürücüsünde bulunan bir kayıt defteri anahtarı dosya yolu başvurma kullanın; Bu durumda. Bu konumları hakkında ayrıntılar daha sonra bu bölümde verilir.

Önceden yüklenen paketler iş kullanarak [şablon sihirbazları](/visualstudio/extensibility/how-to-use-wizards-with-project-templates). Şablon örneği özel sihirbaz çağrılır. Sihirbaz yüklenmesi gereken paketlerin listesini yükler ve bu bilgileri uygun NuGet API'leri geçirir.

Paketleri bir şablona dahil adımlar:

1. İçinde `vstemplate` dosya, NuGet Şablon Sihirbazı'nı bir başvuru ekleyerek bir [ `WizardExtension` ](/visualstudio/extensibility/wizardextension-element-visual-studio-templates) öğe:

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    `NuGet.VisualStudio.Interop.dll`yalnızca içeren bir derleme `TemplateWizard` gerçek uygulamasında içine çağıran basit bir sarmalayıcı sınıfı `NuGet.VisualStudio.dll`. Proje/öğe şablonları NuGet yeni sürümleri ile çalışmaya devam derleme sürümünü hiçbir zaman değiştireceksiniz.

1. Projede yüklemek için olan paketlerin listesini ekleyin:

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    *(NuGet 2.2.1+)*  Birden çok sihirbaz destekler `<package>` öğeleri birden çok paket kaynaklarını destekleyecek şekilde. Hem `id` ve `version` , belirli bir paketin sürümü anlamına yüklenecek daha yeni bir sürümü kullanılabilir olsa bile, öznitelikler gereklidir. Bu, paket güncelleştirmesi şablon kullanılarak Geliştirici paketi güncelleştirmeye seçimi bırakarak şablon bozmasını engeller.

1. NuGet paketleri aşağıdaki bölümlerde açıklandığı gibi bulabileceğiniz deposu belirtin.

### <a name="vsix-package-repository"></a>VSIX Paket Deposu

Visual Studio Proje/öğesi şablonları için önerilen dağıtım yaklaşımdır bir [VSIX uzantısı](/visualstudio/extensibility/shipping-visual-studio-extensions) çünkü birden çok proje/öğe şablonları birlikte paketlemenize olanak sağlar ve geliştiricilerin şablonlarınızı kolay bulmasına olanak tanır VS Uzantı Yöneticisi'ni veya Visual Studio Galerisi kullanıyor. Uzantı için güncelleştirmelerin de kullanarak dağıtmak kolay [Visual Studio Uzantı Yöneticisi otomatik güncelleştirme mekanizmasını](/visualstudio/extensibility/how-to-update-a-visual-studio-extension).

VSIX şablon tarafından gereken paketler için kaynak olarak hizmet verebilir:

1. Değiştirme `<packages>` öğesinde `.vstemplate` gibi dosya:

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    `repository` Öznitelik deposu olarak türünü belirtir `extension` sırada `repositoryId` VSIX benzersiz tanıtıcısı (Bu değeri `ID` uzantının özniteliğinde `vsixmanifest` dosya için bkz: [ VSIX uzantı şema 2.0 başvurusu](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).

1. Yerleştir, `nupkg` bir klasördeki dosyaları adlı `Packages` VSIX içinde.

1. Gerekli paket dosyaları olarak ekleme `<Asset>` içinde `vsixmanifest` dosyası (bkz [VSIX uzantı şema 2.0 başvurusu](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)):

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

1. Proje şablonları olarak aynı VSIX içinde paketler sağlayabilir veya, daha fazla senaryonuz için mantıklı varsa bunları ayrı içinde VSIX içine koyabilirsiniz unutmayın. Ancak, uzantının değişiklikler şablonunuzu uğratabilir olduğundan üzerinde denetim, elinizde VSIX başvuruda bulunmayın.

### <a name="template-package-repository"></a>Şablon Paket Deposu

Yalnızca bir tek proje öğesi şablon dağıtma ve birden fazla şablon birlikte paketini gerekmez, doğrudan proje/öğesi şablon ZIP dosyasında paketlerini içeren daha basit ancak daha kısıtlı bir yaklaşım kullanarak şunları yapabilirsiniz:

1. Değiştirme `<packages>` öğesinde `.vstemplate` gibi dosya:

    ```xml
    <packages repository="template"">
        <!-- ... -->
    </packages>
    ```

    `repository` Özniteliğine sahip değer `template` ve `repositoryId` özniteliği gerekli değildir.

1. Paketler proje/öğesi şablon ZIP dosyası kök klasörüne yerleştirin.

Bir veya daha fazla paket şablonların ortak olduğunda bu yaklaşımı kullanarak birden fazla şablon içeren bir VSIX gereksiz oluşan şişirmeyi müşteri adayları olduğunu unutmayın. Bu gibi durumlarda kullanmak [VSIX deposu olarak](#vsix-package-repository) önceki bölümde açıklandığı gibi.

### <a name="registry-specified-folder-path"></a>Kayıt defteri tarafından belirtilen klasör yolu

Bir MSI kullanılarak yüklenen SDK'ları doğrudan geliştiricinin makinesinde NuGet paketlerini yükleyebilirsiniz. Bunları hemen kullanılabilir bir öğe veya proje şablonu kullanılır bu yapar yerine bu süre boyunca ayıklanacak sahip. ASP.NET şablonlar bu yaklaşımı kullanın.

1. Paketleri yüklemek için makine MSI vardır. Yalnızca yükleyebilirsiniz `.nupkg` dosyaları, veya yükleyebilirsiniz genişletilmiş içeriği yanı sıra bu şablon kullanıldığında, ek bir adım kaydeder. Bu durumda, NuGet'ın standart klasör yapısı; burada görüntülerle izleyin `.nupkg` dosyaları kök klasöründe ve ardından her bir paket kimliği/sürüm çifti alt klasör adı olarak bir alt klasörü vardır.

1. Paket konumu tanımlamak için bir kayıt defteri anahtarı yazın:

    - Anahtar konumu: her iki makine genelinde `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` veya kullanıcı başına yüklenmiş şablonlar ve paketleri ise, bunun yerine kullanın`HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`
    - Anahtar adı: için benzersiz bir ad kullanın. Örneğin, VS 2012 kullanmak için ASP.NET MVC 4 şablonları `AspNetMvc4VS11`.
    - Değerler: klasörün tam yolunu paketler.

1. İçinde `<packages>` öğesinde `.vstemplate` dosya, öznitelik Ekle `repository="registry"` ve kayıt defteri anahtarı adınızı belirtmek `keyName` özniteliği.

    - Paketlerinizi önceden unzipped kullanırsanız `isPreunzipped="true"` özniteliği.
    - *(NuGet 3.2 +)*  Tasarım zamanı yapı paket yükleme işleminin sonunda zorlamak istiyorsanız, eklemeniz `forceDesignTimeBuild="true"` özniteliği.
    - Bir iyileştirme ekleme `skipAssemblyReferences="true"` şablon gerekli başvurular içerdiğinden.

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a>En İyi Yöntemler

1. Bir bağımlılık VSIX bildiriminizi bir başvuru ekleyerek NuGet VSIX bildirin:

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. Proje/öğe şablonları oluşturma dahil ederek kaydedilmesini gerektirir [ `<PromptForSaveOnCreation>true</PromptForSaveOnCreation>` ](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) içinde `.vstemplate` dosya.

1. Şablonları içermeyen bir `packages.config` dosya ve eklemeyin veya tüm başvuruları veya NuGet paketleri yüklendiğinde ekleneceği içerik.
