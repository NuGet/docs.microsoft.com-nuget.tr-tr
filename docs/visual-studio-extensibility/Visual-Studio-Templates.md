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
# <a name="packages-in-visual-studio-templates"></a>Visual Studio şablonları paketleri

Visual Studio Proje ve öğe şablonları, genellikle bir proje veya öğe oluşturulduğunda, bazı paketlerden yüklendiğinden emin emin olmanız gerekir. Örneğin, ASP.NET MVC 3 şablonu, jQuery, Modernize ve diğer paketleri yükler.

Bunu desteklemek için şablonu yazarlar, tek tek kitaplıklarda yerine gerekli paketleri yüklemek için NuGet bildirebilirsiniz. Geliştiriciler daha sonra kolayca bu paketleri daha sonraki bir zamanda güncelleştirebilirsiniz.

Şablonlar yazma hakkında daha fazla bilgi için bkz [nasıl yapılır: Proje şablonları oluşturma](/visualstudio/ide/how-to-create-project-templates) veya [oluşturma özel Proje ve öğe şablonlarını](/visualstudio/extensibility/creating-custom-project-and-item-templates).

Bu bölümün geri kalanında, bir şablon yazma düzgün şekilde NuGet paketlerini içerecek şekilde gerçekleştirilecek belirli adımlar açıklanmaktadır.

- [Bir şablona paketleri ekleme](#adding-packages-to-a-template)
- [En iyi uygulamalar](#best-practices)

Bir örnek için bkz. [NuGetInVsTemplates örnek](https://bitbucket.org/marcind/nugetinvstemplates).

## <a name="adding-packages-to-a-template"></a>Bir şablona paketleri ekleme

Bir şablon örneği başlatıldığında bir [Şablon Sihirbazı](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) bu paketleri nerede bulunacağı hakkında bilgi ile birlikte yüklemek için paketler listesini yüklemek için çağrılır. Paket içinde VSIX içine katıştırılmış, şablonda katıştırılmış veya yerel sabit sürücüsünde bulunan bu durumda dosya yolu başvurmak için bir kayıt defteri anahtarı kullanırsınız. Bu konumlar hakkında ayrıntılı bilgi, daha sonra bu bölümde verilir.

Önceden yüklenmiş paketler çalışma kullanarak [şablon sihirbazları](/visualstudio/extensibility/how-to-use-wizards-with-project-templates). Şablon örneği, özel sihirbaz çağrılır. Sihirbazın yüklenmesi gereken paketler listesini yükler ve uygun NuGet API'leri için bu bilgileri geçirir.

Bir şablonda paketlerini içerecek şekilde adımlar:

1. İçinde `vstemplate` dosya, NuGet şablon sihirbazında yapılan bir başvuru ekleyerek bir [ `WizardExtension` ](/visualstudio/extensibility/wizardextension-element-visual-studio-templates) öğesi:

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    `NuGet.VisualStudio.Interop.dll` yalnızca içeren bir derleme `TemplateWizard` gerçek uygulamasında içine yapılan çağrılar basit bir sarmalayıcı sınıfının `NuGet.VisualStudio.dll`. Proje/öğe şablonları yeni NuGet sürümlerini ile çalışmaya devam eder, derleme sürümü asla değiştirmez.

1. Projeye yüklemek için paketler listesini ekleyin:

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    Birden çok sihirbaz destekler `<package>` birden çok paket kaynaklarını desteklemek için öğeleri. Hem `id` ve `version` , belirli bir paketin sürümü anlamı yükleneceği daha yeni bir sürüm kullanılabilir olsa bile, öznitelikleri gereklidir. Bu paket güncelleştirmeleri paketi güncelleştirmeye şablonuyla Geliştirici seçimi bırakın, şablon bozmasını engeller.

1. NuGet paketleri aşağıdaki bölümlerde açıklandığı gibi bulabileceğiniz havuz belirtin.

### <a name="vsix-package-repository"></a>VSIX Paket Deposu

Visual Studio Proje/öğe şablonları için önerilen dağıtım yaklaşımdır bir [VSIX uzantısı](/visualstudio/extensibility/shipping-visual-studio-extensions) çünkü birden çok proje/öğe şablon birlikte paketlemenize olanak sağlar ve geliştiricilerin şablonlarınızı kolayca keşfedin olanak tanır VS uzantısı Yöneticisi veya Visual Studio Galerisi kullanma. Uzantı için güncelleştirmeleri kullanarak kolayca ayrıca [Visual Studio Uzantı Yöneticisi'ni otomatik güncelleştirme mekanizmasını](/visualstudio/extensibility/how-to-update-a-visual-studio-extension).

VSIX şablon için gerekli paketleri için kaynak olarak hizmet verebilen:

1. Değiştirme `<packages>` öğesinde `.vstemplate` aşağıdaki gibi:

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    `repository` Öznitelik deposu olarak türünü belirten `extension` sırada `repositoryId` VSIX benzersiz tanıtıcısı (Bu değeri `ID` uzantının özniteliğinde `vsixmanifest` bkz [ VSIX Uzantı Şeması 2.0 başvurusu](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).

1. Bir yerde, `nupkg` adlı bir klasördeki dosyaları `Packages` VSIX içinde.

1. Gerekli paket dosyaları olarak ekleme `<Asset>` içinde `vsixmanifest` dosyası (bkz [VSIX Uzantı Şeması 2.0 başvurusu](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)):

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

1. Paketler, proje şablonları olarak aynı VSIX içinde sağlayabileceğiniz veya, senaryonuz için daha anlamlı olur, bunları ayrı bir VSIX'e koyabilirsiniz unutmayın. Ancak, bu uzantı değişiklikleri şablonunuzu uğratabilir olduğundan üzerinde denetimi sizde değil herhangi bir VSIX başvuruda bulunmayın.

### <a name="template-package-repository"></a>Şablon Paket Deposu

Yalnızca tek proje/öğe şablon dağıtma ve birden fazla şablon birlikte paketini gerekmez, doğrudan proje/öğe şablon ZIP dosyasında paketlerini içeren daha basit ancak daha sınırlı bir yaklaşımı kullanabilirsiniz:

1. Değiştirme `<packages>` öğesinde `.vstemplate` aşağıdaki gibi:

    ```xml
    <packages repository="template"">
        <!-- ... -->
    </packages>
    ```

    `repository` Özniteliğinin değeri `template` ve `repositoryId` öznitelik gerekli değildir.

1. Paketleri proje/öğe şablon ZIP dosyasının kök klasörüne yerleştirin.

Bir veya daha fazla paket şablonları için ortak olduğunda bu yaklaşımı kullanarak birden fazla şablon içeren bir VSIX için gereksiz Şişirme müşteri adayları olduğunu unutmayın. Böyle durumlarda kullanmak [deposu olarak VSIX](#vsix-package-repository) önceki bölümde açıklandığı gibi.

### <a name="registry-specified-folder-path"></a>Kayıt defteri belirtilen klasör yolu

MSI kullanarak yüklü SDK'ları NuGet paketlerini doğrudan Geliştirici makineye yükleyebilirsiniz. Hemen kullanılamıyorsa, bir proje veya öğe şablonu, bunları kullanılan bu yapar, yerine bu süre boyunca ayıklanacak. ASP.NET şablonları, bu yaklaşımı kullanın.

1. MSI paketleri yüklemek için makine var. Yalnızca yükleyebilirsiniz `.nupkg` dosyaları veya yükleyebilir genişletilmiş içeriği ile birlikte bu şablonu kullanıldığında ek bir adım kaydeder. Bu durumda, NuGet'ın standart klasör yapısını burada görüntülerle izleyin `.nupkg` dosyaları kök klasöründe ve ardından her paket kimliği/VERSION çifti alt klasör adı ile bir alt sahip.

1. Paket konumunu tanımlamak için bir kayıt defteri anahtarı yazın:

    - Anahtar konumu: ya da makine genelindeki `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` veya kullanıcı başına yüklü şablonları ve paketleri ise, alternatif olarak kullanın `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`
    - Anahtar adı: sizin için benzersiz bir ad kullanın. Örneğin, VS 2012 kullanmak için ASP.NET MVC 4 şablonları `AspNetMvc4VS11`.
    - Değerler: paketleri klasörün tam yolu.

1. İçinde `<packages>` öğesinde `.vstemplate` öznitelik ekleyin `repository="registry"` ve kayıt defteri anahtarı adınızı belirtin `keyName` özniteliği.

    - Paketlerinizi önceden geçin kullanırsanız `isPreunzipped="true"` özniteliği.
    - *(NuGet 3.2 +)*  Paket yükleme sonunda bir tasarım zamanı derleme zorlamak istiyorsanız ekleme `forceDesignTimeBuild="true"` özniteliği.
    - Bir iyileştirme ekleme `skipAssemblyReferences="true"` çünkü şablon zaten gerekli başvuruları içerir.

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a>En İyi Yöntemler

1. Bir bağımlılık, VSIX bildiriminizi buna bir başvuru ekleyerek NuGet VSIX üzerinde bildirin:

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. Proje/öğe şablonları oluşturma dahil ederek kaydedilmesini gerektirir [ `<PromptForSaveOnCreation>true</PromptForSaveOnCreation>` ](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) içinde `.vstemplate` dosya.

1. Şablonlar içermez bir `packages.config` dosya ve ekleme veya tüm başvuruları veya NuGet paketleri yüklendiğinde eklenir içeriği.
