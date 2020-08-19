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
# <a name="packages-in-visual-studio-templates"></a>Visual Studio şablonlarındaki paketler

Visual Studio proje ve öğe şablonları genellikle belirli paketlerin bir proje veya öğe oluşturulduğunda yüklendiğinden emin olunması gerekir. Örneğin, ASP.NET MVC 3 şablonu jQuery, Modernizr ve diğer paketleri de yüklüyor.

Bunu desteklemek için, şablon yazarları NuGet 'e ayrı kitaplıklar yerine gerekli paketleri yüklemesini sağlayabilir. Geliştiriciler daha sonra bu paketleri daha sonra kolayca güncelleştirebilir.

Şablon yazma hakkında daha fazla bilgi edinmek için [nasıl yapılır: proje şablonları oluşturma](/visualstudio/ide/how-to-create-project-templates) veya [özel proje ve öğe şablonları oluşturma](/visualstudio/extensibility/creating-custom-project-and-item-templates)bölümüne bakın.

Bu bölümün geri kalanında, NuGet paketlerini düzgün bir şekilde içerecek şekilde bir şablon yazarken yapmanız gereken belirli adımlar açıklanmaktadır.

- [Bir şablona paket ekleme](#adding-packages-to-a-template)
- [En iyi uygulamalar](#best-practices)

Bir örnek için, bkz. [Nugetfaturalanmış Stempsyonlar örneği](https://bitbucket.org/marcind/nugetinvstemplates).

## <a name="adding-packages-to-a-template"></a>Bir şablona paket ekleme

Bir şablon örneği oluşturulduğunda, yüklenecek paketlerin listesini, bu paketlerin nerede bulunacağı hakkında bilgi içeren bir [Şablon Sihirbazı](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) çağırılır. Paketler VSıX 'e gömülebilir, şablona katıştırılabilir veya yerel sabit sürücüde bulunabilir ve bu durumda dosya yoluna başvurmak için bir kayıt defteri anahtarı kullanırsınız. Bu konumların ayrıntıları bu bölümde daha sonra verilmiştir.

Önceden yüklenmiş paketler, [şablon sihirbazları](/visualstudio/extensibility/how-to-use-wizards-with-project-templates)kullanılarak çalışır. Şablon örneği oluşturulduğunda özel bir sihirbaz çağrılır. Sihirbaz yüklenmesi gereken paketlerin listesini yükler ve ilgili bilgileri uygun NuGet API 'Lerine geçirir.

Bir şablona paket ekleme adımları:

1. `vstemplate`Dosyanızda, bir öğe ekleyerek NuGet şablon sihirbazına bir başvuru ekleyin [`WizardExtension`](/visualstudio/extensibility/wizardextension-element-visual-studio-templates) :

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    `NuGet.VisualStudio.Interop.dll` , yalnızca `TemplateWizard` içindeki gerçek uygulamaya çağıran basit bir sarmalayıcı olan sınıfını içeren bir derlemedir `NuGet.VisualStudio.dll` . Proje/öğe şablonlarının NuGet 'in yeni sürümleriyle çalışmaya devam etmesi için derleme sürümü hiçbir şekilde değişmeyecektir.

1. Projeye yüklenecek paketlerin listesini ekleyin:

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    Sihirbaz `<package>` birden çok paket kaynağını desteklemek için birden çok öğeyi destekler. Ve özniteliklerinin her ikisi de `id` `version` gereklidir; yani, daha yeni bir sürüm kullanılabilir olsa bile paketin belirli bir sürümünün yükleneceği anlamına gelir. Bu, paket güncelleştirmelerinin şablonu bozmasını engeller ve şablonu kullanarak paketi geliştiriciye güncelleştirme seçeneğini bırakır.

1. Aşağıdaki bölümlerde açıklandığı gibi, NuGet 'in paketleri bulabileceği depoyu belirtin.

### <a name="vsix-package-repository"></a>VSıX paket deposu

Visual Studio proje/öğe şablonları için önerilen dağıtım yaklaşımı bir [VSIX uzantısıdır](/visualstudio/extensibility/shipping-visual-studio-extensions) , çünkü birden fazla proje/öğe şablonunu birlikte paketlemenize ve geliştiricilerin vs uzantısı yöneticisini veya Visual Studio galerisini kullanarak şablonlarınızı kolayca bulmasına olanak tanır. Uzantı güncelleştirmelerinin [Visual Studio Uzantı Yöneticisi otomatik güncelleştirme mekanizması](/visualstudio/extensibility/how-to-update-a-visual-studio-extension)kullanılarak dağıtılması da kolaydır.

VSıX, şablonun gerektirdiği paketlere yönelik kaynak olarak görev yapabilir:

1. `<packages>` `.vstemplate` Dosyadaki öğesini aşağıdaki gibi değiştirin:

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    Özniteliği,, `repository` `extension` `repositoryId` VSIX 'in benzersiz tanımlayıcısı olduğu gibi, deponun türünü belirtir (Bu, `ID` uzantının dosyasındaki özniteliğin değeridir `vsixmanifest` , bkz. [VSIX uzantı Şeması 2,0 başvurusu](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).

1. `nupkg`DOSYALARıNıZı VSIX içinde adlı bir klasöre yerleştirin `Packages` .

1. Gerekli paket dosyalarını `<Asset>` `vsixmanifest` dosyanıza ekleyin (bkz. [vsıx uzantı Şeması 2,0 başvurusu](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)):

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

1. Aynı VSıX içindeki paketleri proje şablonlarınızla sunabilmenizi veya bu, senaryonuza daha anlamlı bir şekilde bir VSıX 'e koyabileceğinizi unutmayın. Ancak, bu uzantıdaki değişiklikler şablonunuzu bozabileceğinden, denetiminiz olmayan herhangi bir VSıX 'e başvurmayın.

### <a name="template-package-repository"></a>Şablon paket deposu

Yalnızca tek bir proje/öğe şablonunu dağıtıyorsanız ve birden çok şablonu birlikte paketlemenize gerek yoksa, doğrudan proje/öğe şablonu ZIP dosyasında paketleri içeren daha basit ancak daha sınırlı bir yaklaşım kullanabilirsiniz:

1. `<packages>` `.vstemplate` Dosyadaki öğesini aşağıdaki gibi değiştirin:

    ```xml
    <packages repository="template">
        <!-- ... -->
    </packages>
    ```

    `repository`Özniteliğin değeri vardır `template` ve `repositoryId` özniteliği gerekli değildir.

1. Paketleri proje/öğe şablonu ZIP dosyasının kök klasörüne yerleştirin.

Bu yaklaşımı birden çok şablon içeren bir VSIX içinde kullanmanın, bir veya daha fazla paket şablonlarda ortak olduğunda gereksiz oluşan şişirmeyi 'a yol açar. Bu gibi durumlarda, önceki bölümde açıklandığı gibi [VSIX 'i depo olarak](#vsix-package-repository) kullanın.

### <a name="registry-specified-folder-path"></a>Kayıt defteri-belirtilen klasör yolu

MSI kullanılarak yüklenen SDK 'lar, NuGet paketlerini doğrudan geliştiricinin makinesine yükleyebilir. Bu, bir proje veya öğe şablonu kullanıldığında, bu süre içinde ayıklanmaları yerine bunları hemen kullanılabilir hale getirir. ASP.NET şablonları bu yaklaşımı kullanır.

1. MSI paketlerini makineye yüklemesi gerekir. Yalnızca `.nupkg` dosyaları yükleyebilir veya bunları genişletilmiş içerikle birlikte yükleyebilirsiniz ve bu da şablon kullanıldığında ek bir adım kaydedilir. Bu durumda, dosyaların kök klasörde olduğu, NuGet 'in standart klasör yapısını izleyin `.nupkg` ve sonra her pakette alt klasör adı olarak kimlik/sürüm çiftinin bulunduğu bir alt klasör bulunur.

1. Paket konumunu tanımlamak için bir kayıt defteri anahtarı yazın:

    - Anahtar konumu: makine genelinde `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` veya Kullanıcı başına yüklenmiş şablonlar ve paketler, alternatif olarak `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`
    - Anahtar adı: sizin için benzersiz olan bir ad kullanın. Örneğin, VS 2012 için ASP.NET MVC 4 şablonları kullanılır `AspNetMvc4VS11` .
    - Değerler: paketler klasörünün tam yolu.

1. `<packages>` `.vstemplate` Dosyadaki öğesinde, özniteliğini ekleyin `repository="registry"` ve özniteliğinde kayıt defteri anahtarı adını belirtin `keyName` .

    - Paketlerinizi önceden sıkıştırdıysanız, `isPreunzipped="true"` özniteliğini kullanın.
    - *(NuGet 3.2 +)* Paket yüklemesinin sonunda bir tasarım zamanı oluşturmaya zorlamak isterseniz, `forceDesignTimeBuild="true"` özniteliğini ekleyin.
    - Bir iyileştirme olarak, `skipAssemblyReferences="true"` şablon zaten gerekli başvuruları içerdiğinden ekleyin.

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a>En İyi Uygulamalar

1. VSıX bildiriminizde buna bir başvuru ekleyerek NuGet VSıX üzerinde bir bağımlılık bildirin:

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. Dosyasına dahil ederek proje/öğe şablonlarının oluşturma sırasında kaydedilmesini gerektir [`<PromptForSaveOnCreation>true</PromptForSaveOnCreation>`](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) `.vstemplate` .

1. Şablonlar bir `packages.config` dosya içermez ve NuGet paketleri yüklendiğinde eklenecek başvuruları ya da içeriği içermez.
