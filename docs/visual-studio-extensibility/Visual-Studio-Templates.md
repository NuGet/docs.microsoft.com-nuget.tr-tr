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
# <a name="packages-in-visual-studio-templates"></a>Visual Studio şablonlarında paketler

Visual Studio proje ve öğe şablonları genellikle bir proje veya öğe oluşturulduğunda belirli paketlerin yüklendiğinden emin olmak gerekir. Örneğin, ASP.NET MVC 3 şablonu jQuery, Modernizr ve diğer paketleri yükler.

Bunu desteklemek için, şablon yazarları NuGet'e tek tek kitaplıklar yerine gerekli paketleri yüklemesini talimat verebilir. Geliştiriciler daha sonra bu paketleri kolayca güncelleyebilir.

Şablonları yazma hakkında daha fazla bilgi edinmek için nasıl [yazabilirsiniz: Proje Şablonları Oluşturma](/visualstudio/ide/how-to-create-project-templates) veya [Özel Proje ve Öğe Şablonları Oluşturma'ya](/visualstudio/extensibility/creating-custom-project-and-item-templates)bakın.

Bu bölümün geri kalanı, NuGet paketlerini düzgün bir şekilde içerecek şekilde bir şablon yazarken atılması gereken belirli adımları açıklar.

- [Şablona paket ekleme](#adding-packages-to-a-template)
- [En iyi uygulamalar](#best-practices)

Örneğin, [NuGetInVsTemplates örneğine](https://bitbucket.org/marcind/nugetinvstemplates)bakın.

## <a name="adding-packages-to-a-template"></a>Şablona paket ekleme

Bir şablon anında çağrıldığında, bu paketlerin nerede bulunacağı yla ilgili bilgilerle birlikte yüklenmesi gereken paketlerlistesini yüklemek için bir [şablon sihirbazı](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) çağrılır. Paketler VSIX'ye katıştılabilir, şablona katıştılabilir veya yerel sabit diskte bulunabilir ve bu durumda dosya yoluna başvurmak için bir kayıt defteri anahtarı kullanırsınız. Bu konumlarla ilgili ayrıntılar daha sonra bu bölümde verilmiştir.

Önceden yüklenmiş paketler [şablon sihirbazlarını](/visualstudio/extensibility/how-to-use-wizards-with-project-templates)kullanarak çalışır. Şablon anında olduğunda özel bir sihirbaz çağrılır. Sihirbaz, yüklenmesi gereken paketlerin listesini yükler ve bu bilgileri ilgili NuGet API'lerine aktarır.

Şablona paketleri ekleme adımları:

1. Dosyanızda, `vstemplate` bir [`WizardExtension`](/visualstudio/extensibility/wizardextension-element-visual-studio-templates) öğe ekleyerek NuGet şablonu sihirbazına bir başvuru ekleyin:

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    `NuGet.VisualStudio.Interop.dll`yalnızca `TemplateWizard` sınıfı içeren bir derlemedir, bu da `NuGet.VisualStudio.dll`'daki gerçek uygulamaya çağıran basit bir sarıcıdır. Proje/öğe şablonlarının NuGet'in yeni sürümleriyle çalışmaya devam etmesi için derleme sürümü asla değişmez.

1. Projeye yüklenmesi gereken paketlerin listesini ekleyin:

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    Sihirbaz, birden `<package>` çok paket kaynağını desteklemek için birden çok öğeyi destekler. Hem `id` öznitelikleri hem `version` de öznitelikleri gereklidir, yani yeni bir sürüm mevcut olsa bile paketin belirli bir sürümü yüklenir. Bu, paket güncelleştirmelerinin şablonu bozmasını önler ve şablonu kullanarak paketi geliştiriciye güncelleştirme seçeneğibırakır.

1. NuGet'in aşağıdaki bölümlerde açıklandığı şekilde paketleri bulabileceği depoyu belirtin.

### <a name="vsix-package-repository"></a>VSIX paket deposu

Visual Studio proje/öğe şablonları için önerilen dağıtım yaklaşımı, birden çok proje/öğe şablonunu birlikte paketlemenize ve geliştiricilerin VS Extension Manager veya Visual Studio Gallery'yi kullanarak şablonlarınızı kolayca keşfetmenize olanak sağladığından bir [VSIX uzantısıdır.](/visualstudio/extensibility/shipping-visual-studio-extensions) Uzantı güncellemeleri de Visual Studio [Extension Manager otomatik güncelleme mekanizmasını](/visualstudio/extensibility/how-to-update-a-visual-studio-extension)kullanarak dağıtmak kolaydır.

VSIX kendisi şablon tarafından gerekli paketler için kaynak olarak hizmet verebilir:

1. Dosyadaki `<packages>` öğeyi `.vstemplate` aşağıdaki gibi değiştirin:

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    Öznitelik, `repository` Depo türünü VSIX'nin kendisinin `extension` `repositoryId` benzersiz tanımlayıcısı olarak belirtir (Bu, uzantının `ID` `vsixmanifest` dosyasındaki özniteliğin değeridir, bkz. [VSIX Extension Schema 2.0 Reference).](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)

1. Dosyalarınızı `nupkg` VSIX içinde `Packages` adı verilen bir klasöre yerleştirin.

1. Dosyanızda `vsixmanifest` olduğu gibi `<Asset>` gerekli paket dosyalarını ekleyin (bkz. [VSIX Extension Schema 2.0 Reference):](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

1. Paketleri proje şablonlarınızla aynı VSIX'de teslim edebileceğinizi veya senaryonuz için daha mantıklıysa bunları ayrı bir VSIX'ye koyabileceğinizi unutmayın. Ancak, bu uzantıdaki değişiklikler şablonunuzu kırabileceğinden, üzerinde denetiminiz olmayan herhangi bir VSIX'ye başvuruyapmayın.

### <a name="template-package-repository"></a>Şablon paket deposu

Yalnızca tek bir proje/öğe şablonu dağıtıyorsanız ve birden çok şablonu birlikte paketlemeniz gerekmiyorsa, paketleri doğrudan proje/öğe şablonu ZIP dosyasında içeren daha basit ancak daha sınırlı bir yaklaşım kullanabilirsiniz:

1. Dosyadaki `<packages>` öğeyi `.vstemplate` aşağıdaki gibi değiştirin:

    ```xml
    <packages repository="template"">
        <!-- ... -->
    </packages>
    ```

    Öznitelik `repository` değeri `template` vardır ve `repositoryId` öznitelik gerekli değildir.

1. Paketleri proje/öğe şablonu ZIP dosyasının kök klasörüne yerleştirin.

Birden çok şablon içeren bir VSIX'de bu yaklaşımın kullanılmasının, şablonlarda bir veya daha fazla paket ortak olduğunda gereksiz şişkinliğe yol açtığını unutmayın. Bu gibi durumlarda, önceki bölümde açıklandığı [gibi depo olarak VSIX](#vsix-package-repository) kullanın.

### <a name="registry-specified-folder-path"></a>Kayıt defteri tarafından belirtilen klasör yolu

MSI kullanılarak yüklenen SDK'lar NuGet paketlerini doğrudan geliştiricinin makinesine yükleyebilir. Bu, bu süre içinde ayıklamak zorunda kalmak yerine, bir proje veya öğe şablonu kullanıldığında onları hemen kullanılabilir hale getirir. ASP.NET şablonları bu yaklaşımı kullanır.

1. MSI'ın paketlerini makineye yüklemesini. Yalnızca `.nupkg` dosyaları yükleyebilirsiniz veya şablon kullanıldığında ek bir adım kaydeden genişletilmiş içeriklerle birlikte bunları yükleyebilirsiniz. Bu durumda, `.nupkg` dosyaların kök klasöründe olduğu NuGet'in standart klasör yapısını izleyin ve ardından her paketin alt klasör adı olarak id/sürüm çiftinin yer aldığı bir alt klasörü vardır.

1. Paket konumunu belirlemek için bir kayıt defteri anahtarı yazın:

    - Anahtar konumu: Makine genelinde `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` veya kullanıcı başına yüklenen şablonlar ve paketler varsa, alternatif olarak`HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`
    - Anahtar adı: size özgü bir ad kullanın. Örneğin, VS 2012 için mvc 4 `AspNetMvc4VS11`şablonları ASP.NET kullanın.
    - Değerler: paketler klasörüne tam yol.

1. Dosyadaki `<packages>` öğede `repository="registry"` özniteliği ekleyin ve öznitelikte kayıt defteri anahtar adınızı belirtin. `keyName` `.vstemplate`

    - Paketlerinizi önceden fermuarsız olarak açtıysanız, özniteliği kullanın. `isPreunzipped="true"`
    - *(NuGet 3.2+)* Paket yüklemesinin sonunda bir tasarım zamanı oluşturmayı zorlamak istiyorsanız, özniteliği ekleyin. `forceDesignTimeBuild="true"`
    - Bir optimizasyon olarak, `skipAssemblyReferences="true"` şablonun kendisi zaten gerekli başvuruları içerdiğinden ekleyin.

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a>En İyi Uygulamalar

1. VSIX bildiriminizde bir referans ekleyerek NuGet VSIX'ye bir bağımlılık bildirin:

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. `.vstemplate` Dosyaya ekleyerek [`<PromptForSaveOnCreation>true</PromptForSaveOnCreation>`](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) proje/öğe şablonlarının oluşturma üzerine kaydedilmesini zorunlu kılmasını zorunlu kınla.

1. Şablonlar bir `packages.config` dosya içermez ve NuGet paketleri yüklendiğinde eklenecek başvuruları veya içeriği içermez.
