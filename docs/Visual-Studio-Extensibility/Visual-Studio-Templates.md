---
title: "Visual Studio şablonları NuGet paketlerine | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 2/8/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 0b2cf228-f028-475d-8792-c012dffdb26f
description: "NuGet paketlerini Visual Studio Proje ve öğe şablonları bir parçası olarak dahil etmek için yönergeler."
keywords: "NuGet Visual Studio, Visual Studio Proje şablonları, Visual Studio öğe şablonları, proje şablonları paketlerinde, paketler halinde öğe şablonları"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5b2ad7616578b5f54d917c4555e861c847814da9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="packages-in-visual-studio-templates"></a>Visual Studio şablonları paketler

Visual Studio Proje ve öğe şablonları, genellikle proje ve öğe oluşturulduğunda bazı paketler halinde yüklü olduğundan emin olun gerekir. Örneğin, ASP.NET MVC 3 şablonu jQuery, Modernizr ve diğer paketleri yükler.

Bunu desteklemek için şablon yazarlar tek tek kitaplıklarda yerine gerekli paketleri yüklemek için NuGet söyleyebilirsiniz. Geliştiriciler sonra kolayca bu paketleri daha sonraki bir zamanda güncelleştirebilirsiniz.

Şablonların kendilerine yazma hakkında daha fazla bilgi için bkz [proje oluşturma ve Visual Studio öğe şablonları](https://msdn.microsoft.com/library/s365byhx.aspx) veya [oluşturma özel Proje ve öğe şablonlarını Visual Studio SDK'sı](https://msdn.microsoft.com/library/ff527340.aspx).

Bu bölüm geri kalanı düzgün NuGet paketleri dahil etmek için bir şablon yazarken uygulanacak belirli adımlar açıklanmaktadır.

- [Bir şablona paketleri ekleme](#adding-packages-to-a-template)
- [En iyi uygulamalar](#best-practices)

Bir örnek için bkz: [NuGetInVsTemplates örnek](https://bitbucket.org/marcind/nugetinvstemplates).


## <a name="adding-packages-to-a-template"></a>Bir şablona paketleri ekleme

Şablon örneği oluşturulduğunda bir [Şablon Sihirbazı](https://msdn.microsoft.com/library/ms185301.aspx) bu paketleri nerede bulacağını hakkında bilgilerle birlikte yüklemek için olan paketlerin listesini yüklemek için çağrılır. Paket içinde VSIX içine katıştırılmış, şablonda katıştırılmış veya yerel sabit sürücüsünde bulunan bir kayıt defteri anahtarı dosya yolu başvurma kullanın; Bu durumda. Bu konumları hakkında ayrıntılar daha sonra bu bölümde verilir.

Önceden yüklenen paketler iş kullanarak [şablon sihirbazları](http://msdn.microsoft.com/library/ms185301.aspx). Şablon örneği özel sihirbaz çağrılır. Sihirbaz yüklenmesi gereken paketlerin listesini yükler ve bu bilgileri uygun NuGet API'leri geçirir.

Paketleri bir şablona dahil adımlar:

1. İçinde `vstemplate` dosya, NuGet Şablon Sihirbazı'nı bir başvuru ekleyerek bir [ `WizardExtension` ](http://msdn.microsoft.com/library/ms171411.aspx) öğe:

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

Visual Studio Proje/öğesi şablonları için önerilen dağıtım yaklaşımdır bir [VSIX uzantısı](http://msdn.microsoft.com/library/ff363239.aspx) çünkü birden çok proje/öğe şablonları birlikte paketlemenize olanak sağlar ve geliştiricilerin şablonlarınızı kolay bulmasına olanak tanır VS Uzantı Yöneticisi'ni veya Visual Studio Galerisi kullanıyor. Uzantı için güncelleştirmelerin de kullanarak dağıtmak kolay [Visual Studio Uzantı Yöneticisi otomatik güncelleştirme mekanizmasını](http://msdn.microsoft.com/library/dd997169.aspx).

VSIX şablon tarafından gereken paketler için kaynak olarak hizmet verebilir:

1. Değiştirme `<packages>` öğesinde `.vstemplate` gibi dosya:

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    `repository` Öznitelik deposu olarak türünü belirten `extension` sırada `repositoryId` VSIX benzersiz tanıtıcısı (Bu değeri [ `ID` özniteliği](http://msdn.microsoft.com/library/dd393688.aspx) uzantının içinde`vsixmanifest` dosyası).

1. Yerleştir, `nupkg` bir klasördeki dosyaları adlı `Packages` VSIX içinde.
1. Gerekli paket dosyaları olarak ekleme [özel uzantı içerik](http://msdn.microsoft.com/library/dd393737.aspx) içinde `source.extension.vsixmanifest` dosya. 2.0 şema kullanıyorsanız, aşağıdaki gibi görünmelidir:

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

    1.0 şema kullanıyorsanız, aşağıdaki gibi görünmelidir:

    ```xml
    <CustomExtension Type="Moq.4.0.10827.nupkg">
        packages/Moq.4.0.10827.nupkg
    </CustomExtension>
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

1. Proje/öğe şablonları oluşturma ayarlayarak kaydedilmesini gerektirir [ `<PromptForSaveOnCreation>` ](http://msdn.microsoft.com/library/twfxayz5.aspx) içinde `.vstemplate` dosya.

1. Şablonları içermeyen bir `packages.config` veya `project.json` dosya ve içermeyen veya tüm başvuruları veya NuGet paketleri yüklendiğinde ekleneceği içerik.
