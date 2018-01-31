---
title: "Tanıtım kılavuzu oluşturma ve yayımlama NuGet paketi | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/03/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Oluşturma ve yayımlama nuget.exe komut satırı arabirimi ve Visual Studio kullanarak bir NuGet paketi bir gözden geçirme Öğreticisi."
keywords: "NuGet paket oluşturma, yayımlama, NuGet paketi NuGet Öğreticisi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 53d29283c9e786fc27e9a608d7d251d8d0b5b0b2
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2018
---
# <a name="create-and-publish-a-package"></a>Oluşturma ve bir paket yayımlama

Bir .NET sınıf kitaplığı'ndan bir NuGet paketi oluşturmak ve nuget.org için yayımlamak için basit bir işlemdir. Bu makalede NuGet komut satırı arabirimi (CLI) ve Visual Studio kullanarak işleminde size kılavuzluk eder.

## <a name="pre-requisites"></a>Ön koşullar

1. Visual Studio 2017 ' herhangi bir sürümünü yüklemek [visualstudio.com](https://www.visualstudio.com/).

1. NuGet CLI Aracı'nı yüklemeden `nuget.exe`, en son sürümünü yükleyerek `nuget.exe` gelen [nuget.org/downloads](https://nuget.org/downloads)ve kaydetme `.exe` yolda bir konuma. Unutmayın indirme *olan* aracı, bir yükleyici.

1. Paket istediğiniz kod için uygun bir .NET sınıf kitaplığı projesi oluşturun. Bir proje zaten sahip değilseniz, basit bir şekilde oluşturabilirsiniz:
    1. Visual Studio'da, **Dosya > Yeni > Proje**, genişletin **Visual C# > Windows** düğümü, "Sınıf kitaplığı" şablonunu seçin, AppLogger proje adı ve tıklayın **Tamam**.
    1. Sonuçta elde edilen proje dosyasını sağ tıklatın ve seçin **yapı** projeyi düzgün bir şekilde oluşturuldu emin olmak için. DLL Debug klasörüne (veya bunun yerine bu yapılandırma yapı sürüm) içinde bulunur.

    Gerçek bir NuGet paketi içinde doğal olarak, bağlı diğer uygulamaları geliştirmek çok sayıda kullanışlı özellikle uygulaması. Bir sınıf kitaplığı şablondan bir paket oluşturmak yeterli olduğundan bu kılavuzda ancak, herhangi bir ek kod yazma olmaz.

## <a name="create-the-nuspec-package-manifest-file"></a>.Nuspec paket bildirim dosyası oluştur

Bir bildirim her NuGet paketi gerekir&mdash;bir `.nuspec` dosya&mdash;içeriğini ve onun bağımlılıklarını açıklamak için. `nuget spec` Komutu, sizin için hangi sonra özelleştirin bu dosyası oluşturur. Bu örnekte, oluşturduğunuz `.nuspec` proje dosyasından; ayrıca arasında başka yollarla bildirimi açıklandığı gibi oluşturabilirsiniz [bir paket oluşturun](../create-packages/creating-a-package.md).

1. Bir komut istemi açın ve proje dosyasını içeren klasöre gidin (`.csproj`).

1. NuGet CLI çalıştırmak `spec` projenizi sonra gibi adlı bildirim oluşturmak üzere komut `AppLogger.nuspec`:

    ```cli
    nuget spec
    ```

1. Dosyayı bir metin düzenleyicisinde açın. Bildirim yere aşağıdaki kod şöyle görünür belirteçleri biçiminde `<token>` (gibi `$id$`) olması değiştirilir paket oluşturma işlemi sırasında projenin Properties/AssemblyInfo.cs dosyasından gelen değerlerle. Belirteçleri hakkında daha fazla bilgi için bkz: [.nuspec dosyası oluşturma](../create-packages/creating-a-package.md#creating-the-nuspec-file).

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>$id$</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>$author$</authors>
        <owners>$author$</owners>
        <licenseUrl>http://LICENSE_URL_HERE_OR_DELETE_THIS_LINE</licenseUrl>
        <projectUrl>http://PROJECT_URL_HERE_OR_DELETE_THIS_LINE</projectUrl>
        <iconUrl>http://ICON_URL_HERE_OR_DELETE_THIS_LINE</iconUrl>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>$description$</description>
        <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>Tag1 Tag2</tags>
        </metadata>
    </package>
    ```

1. Nuget.org arasında benzersiz olan bir paket kimliği seçin. Açıklanan adlandırma kuralları kullanmanızı öneririz [paket oluşturma](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number). Yazar ve açıklama etiketleri güncelleştirdiğinizden emin olun veya sonraki adımda bir hata alıyorsunuz. İşte güncelleştirilmiş `.nuspec` dosyası bir örnek olarak:

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>MyCompanyName.MyProductName.MyPackageName</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>kraigb</authors>
        <owners>kraigb</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>application app logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Note]
> Ortak tüketim için oluşturulan paketler için özel dikkat `<tags>` öğesi, bu etiketler başkalarının paketinizi bulun ve neler yaptığını anlamanıza yardımcı olmak gibi.

## <a name="run-the-pack-command"></a>Paketi komutunu çalıştırın

Bir NuGet paketi oluşturmak için (bir `.nupkg` dosyası) bir projeden çalıştırmak `pack` komutu:

```cli
nuget pack AppLogger.csproj
```

Bu komut oluşturur `AppLogger.1.0.0.0.nupkg` paket adı ve sürüm numarası kullanarak `.nuspec` dosya. Çeşitli alanları güncelleştirmediyseniz uyarıları komutu verdiğinde `.nuspec` varsayılan değerlerine dosyasından.

## <a name="publish-the-package"></a>Paket yayımlama

Bulduktan sonra bir `.nupkg` dosyası, yayımlama, nuget.org kullanmaya `push` komutu. (Alternatif olarak, kullanabileceğiniz [nuget.org yayımlama iş akışı](../create-packages/publish-a-package.md#publish-to-nugetorg).

> [!Warning]
> Nuget.org için yayımlama paketleri diğer geliştiricilerine herkese görünür. Paketleri özel olarak barındırmak için bkz: [paketleri barındırma](../hosting-packages/overview.md).

1. Ücretsiz bir hesap oluşturmak [nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), veya zaten varsa oturum açın. Yeni bir hesap oluşturmadan bir onay e-posta gönderir. Bir paket karşıya yüklemeden önce hesap onaylamanız gerekir.

1. Oturum açtıktan sonra kullanıcı adınızın (sağ üstte) seçin ve ardından **API anahtarları**.

1. Seçin **oluşturma**, anahtarınız için bir ad, seçin **kapsamları seçin > anında** altında **API anahtarı**, girin * için **Glob düzeni**, ardından seçin **oluşturma**.

1. Anahtar oluşturulduktan sonra Seç **kopyalama** erişim almak için anahtar CLI sahip olmanız gerekir:

    ![API anahtarını Panoya kopyalama](media/QS_Create-02-APIKey.png)

    > [!Warning]
    > Anahtarınızı güvenli bir konuma kaydedin ve gizli tutun. Anahtarınızı yanlışlıkla açığa, herhangi bir zamanda yeniden oluşturabilirsiniz. Artık paketleri CLI itmek istiyorsanız, API anahtarını da kaldırabilirsiniz.

1. Aşağıdaki komutu çalıştırın istemine, paket adı belirtme ve anahtar değeri ile değiştirerek 4. adımda kopyalanan:

    ```cli
    nuget push AppLogger.1.0.0.0.nupkg 47be3377-c434-4c29-8576-af7f6993a54b -Source https://api.nuget.org/v3/index.json
    ```

1. nuget.exe yayımlama işleminin sonuçlarını görüntüler:

    ```output
    Pushing AppLogger.1.0.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed. 
    ```

1. Profilinizdeki nuget.org üzerinde seçin **paketlerini Yönet** bir görmek için yalnızca yayımlanmış. Aynı zamanda bir onay e-posta alırsınız. Biraz sıralanması ve diğerleri bulabileceğiniz arama sonuçlarında görüntülenmesi paketinize sürebileceğini unutmayın. Bu işlem sırasında paket sayfanızı aşağıdaki iletiyi gösterir:

    ![Bu paket henüz dizin değil. Arama sonuçlarında görünür ve dizin oluşturma işlemi tamamlandıktan sonra yükleme/geri yükleme için kullanılabilir duruma gelir.](media/QS_Create-03-NotIndexed.png)

> [!Note]
> **Virüs tarama**: tüm paketler için nuget.org karşıya virüs taraması ve herhangi bir virüs bulunursa reddetti. Nuget.org üzerinde listelenen tüm paketler de düzenli aralıklarla taranır.

Ve bu kadar! Yalnızca ilk NuGet paketinizi yayımladıktan [nuget.org](https://www.nuget.org/), diğer geliştiricilerin kendi projelerinde kullanabileceğiniz.

## <a name="related-topics"></a>İlgili konular

- [Bir paket oluşturun](../create-packages/creating-a-package.md)
- [Paket Yayımlama](../create-packages/publish-a-package.md)
- [Birden çok hedef çerçeveyi desteği](../create-packages/supporting-multiple-target-frameworks.md)
- [Paket sürümü oluşturma](../reference/package-versioning.md)
- [Yerelleştirilmiş paketleri oluşturma](../create-packages/creating-localized-packages.md)
