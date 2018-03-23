---
title: "Oluşturma ve yayımlama Visual Studio kullanarak bir .NET Framework NuGet paketi tanıtım Kılavuzu | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/13/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Oluşturma ve yayımlama Visual Studio 2017 kullanarak bir .NET Framework NuGet paketi bir gözden geçirme Öğreticisi."
keywords: "NuGet paketini oluşturma, NuGet paketi yayımlama, NuGet öğretici, Visual Studio NuGet paketi, msbuild paketi oluşturma"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 613cb6e8cf5762f354d69aa271c1e2f0d4851c97
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/15/2018
---
# <a name="create-and-publish-a-package-using-visual-studio-net-framework"></a>Oluşturma ve Visual Studio (.NET Framework) kullanarak bir paket yayımlama

Bir NuGet paketi bir .NET Framework Sınıf Kitaplığı'ndan Visual Studio'da DLL oluşturma ve ardından oluşturmak ve paket yayımlamak için nuget.exe komut satırı aracını kullanarak oluşturursunuz.

## <a name="prerequisites"></a>Önkoşullar

1. Visual Studio 2017 ' herhangi bir sürümünü yüklemek [visualstudio.com](https://www.visualstudio.com/) herhangi biriyle. NET ilgili iş yükü. .NET iş yükü yüklendikten sonra visual Studio 2017 otomatik olarak NuGet yetenekleri içerir.

1. Yükleme `nuget.exe` buradan yükleyerek CLI [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), kaydetme `.exe` dosya için uygun bir klasör ve bu klasörü PATH ortam değişkenine ekleme.

1. [Kayıt nuget.org ücretsiz bir hesap için](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) zaten yoksa. Yeni bir hesap oluşturmadan bir onay e-posta gönderir. Bir paket karşıya yüklemeden önce hesap onaylamanız gerekir.

## <a name="create-a-class-library-project"></a>Sınıf kitaplığı proje oluşturma

Varolan bir .NET Framework sınıf kitaplığı proje paketini veya basit bir şekilde oluşturmak için istediğiniz kodu kullanabilirsiniz:

1. Visual Studio'da, **Dosya > Yeni > Proje**seçin **Visual C#** düğümü, "Sınıf kitaplığı (.NET Framework)" şablonunu seçin, AppLogger proje adı ve tıklatın **Tamam**.

1. Sonuçta elde edilen proje dosyasını sağ tıklatın ve seçin **yapı** projeyi düzgün bir şekilde oluşturuldu emin olmak için. DLL Debug klasörüne (veya bunun yerine bu yapılandırma yapı sürüm) içinde bulunur.

Gerçek bir NuGet paketi içinde doğal olarak, çok sayıda kullanışlı özellikle ile diğer uygulamaları derleme uygulayın. Ancak, istediğiniz bir hedef çerçeveyi de ayarlayabilirsiniz. Örneğin, bkz. kılavuzları için [UWP](../guides/create-uwp-packages.md) ve [Xamarin](../guides/create-packages-for-xamarin.md).

Bir sınıf kitaplığı şablondan bir paket oluşturmak yeterli olduğundan bu kılavuzda ancak, herhangi bir ek kod yazma olmaz. Yine de, bazı işlevsel kod paketi için isterseniz, aşağıdakileri kullanın:

```cs
using System;

namespace AppLogger
{
    public class Logger
    {
        public void Log(string text)
        {
            Console.WriteLine(text);
        }
    }
}
```

> [!Tip]
> Aksi takdirde seçmek için bir nedeniniz yoksa projeleri tüketen geniş kapsamlı bir uyum sağlar gibi .NET standart tercih edilen NuGet paketlerini hedefidir. Bkz: [oluşturma ve Visual Studio (.NET standart) kullanarak bir paketi yayımlamaya](create-and-publish-a-package-using-visual-studio.md).

## <a name="configure-project-properties-for-the-package"></a>Paket proje özelliklerini yapılandırın

Bir NuGet paketi içeren bir bildirime (bir `.nuspec` dosyası), paket tanımlayıcısı, sürüm numarası, açıklama ve daha fazlası gibi ilgili meta veriler içeriyor. Bunlardan bazıları proje özellikleri doğrudan, hem proje hem de bildirim ayrı ayrı güncelleştirme gereğini ortadan kaldırır çizilebilir. Bu bölümde ilgili özelliklerini ayarlamak nereye açıklanmaktadır.

1. Seçin **Proje > Özellikler** menü komutunu ve ardından **uygulama** sekmesi.

1. İçinde **derleme adı** alan, benzersiz bir tanımlayıcı paketinizi verin.

    > [!Important]
    > Nuget.org veya ne olursa olsun, ana bilgisayar genelinde benzersiz bir tanımlayıcı kullanmakta olduğunuz paket vermeniz gerekir. Bu kılavuz için (Bu herkes gerçekte kullanacağı olsa da) sonraki yayımlama adım paketi herkese görünür hale "Sample" veya "Test" adı dahil olmak üzere öneririz.
    >
    > Zaten bir ada sahip bir paketi yayımlamaya çalışırsanız, bir hata görürsünüz.

1. Seçin **derleme bilgilerini...**  içinde girebilirsiniz taşımak diğer özellikleri bildirimine bir iletişim kutusu getirir düğmesi (bkz [.nuspec dosyası başvurusu - değiştirme belirteçleri](../reference/nuspec.md#replacement-tokens)). En yaygın kullanılan alanları **başlık**, **açıklama**, **şirket**, **telif hakkı**, ve **derleme sürümü**. Bu özellikleri sonuçta paketinizi nuget.org gibi bir ana bilgisayarda görünür şekilde tam olarak açıklayıcı emin olun.

    ![Visual Studio'da .NET Framework projesi derleme bilgileri](media/qs_create-vs-01b-project-properties.png)

1. İsteğe bağlı: görmek ve doğrudan özellikleri düzenlemek için açın `Properties/AssemblyInfo.cs` proje dosyasında.

1. Özellikleri ayarladığınızda, proje yapılandırması kümesine **sürüm** ve güncelleştirilmiş DLL'sini üretmek için projeyi derleyin.

## <a name="generate-the-initial-manifest"></a>İlk bildirim oluşturmak

Şimdi el ve proje özelliklerini kümesindeki bir DLL ile kullanmanız `nuget spec` bir ilk oluşturmak için komutu `.nuspec` proje dosyasından. Bu adım, proje dosyasından bilgileri çizmek için ilgili değiştirme belirteçleri içerir.

Çalıştırmadan `nuget spec` ilk bildirimi oluşturmak için yalnızca bir kez. Paket güncelleştirilirken projenizde değerlerini değiştirmek veya bildirim doğrudan düzenleyin.

1. Bir komut istemi açın ve projeyi içeren klasöre gidin `AppLogger.csproj` dosya.

1. Aşağıdaki komutu çalıştırın: `nuget spec AppLogger.csproj`. Bir proje belirterek, NuGet bu durumda proje adıyla eşleşen bir bildirim oluşturur `AppLogger.nuspec`. Ayrıca dahil değiştirme belirteçleri bildiriminde.

1. Açık `AppLogger.nuspec` içeriğini incelemek için bir metin Düzenleyicisi'nde, aşağıdaki gibi görünmelidir:

    ```xml
    <?xml version="1.0"?>
    <package >
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
        <copyright>Copyright 2018</copyright>
        <tags>Tag1 Tag2</tags>
      </metadata>
    </package>
    ```

## <a name="edit-the-manifest"></a>Bildirim Düzenle

1. NuGet üreten bir hata varsayılan değerleri içeren bir paket oluşturmayı denerseniz, `.nuspec` devam etmeden önce aşağıdaki alanları düzenlemek için dosya. Bkz: [.nuspec dosyası başvurusu - tek öğeleri](../reference/nuspec.md#single-elements) bunların nasıl kullanıldığı bir açıklaması için.

    - licenseUrl
    - projectUrl
    - iconUrl
    - releaseNotes
    - etiketler

1. Ortak tüketim için oluşturulan paketler için özellikle dikkat edin **etiketleri** özelliği gibi etiketler başkalarının nuget.org gibi kaynaklarında paketinizi bulun ve neler yaptığını anlamanıza yardımcı olur.

1. Ayrıca diğer öğeleri bildirime şu anda açıklandığı gibi ekleyebileceğiniz [.nuspec dosyası başvurusu](../reference/nuspec.md).

1. Devam etmeden önce dosyayı kaydedin.

## <a name="run-the-pack-command"></a>Paketi komutunu çalıştırın

1. İçeren klasör, bir komut isteminden, `.nuspec` komutunu çalıştırın, dosyayı `nuget pack`.

1. NuGet oluşturan bir `.nupkg` dosya biçiminde *tanımlayıcısı version.nupkg*, hangi geçerli klasörde bulacaksınız.

## <a name="publish-the-package"></a>Paket yayımlama

Bulduktan sonra bir `.nupkg` dosyası, yayımlama, nuget.org kullanmaya `nuget.exe` bir API anahtarı ile nuget.org alınan. Nuget.org için kullanmanız gerekir `nuget.exe` 4.1.0'da ya da daha yüksek.

[!INCLUDE[publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>API anahtarınızı edinin

[!INCLUDE[publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a>Nuget itme ile yayımlama

1. Değiştirmek için içeren klasör `.nupkg` dosya.

1. Paket adı belirtme ve API anahtarınızı anahtar değerini değiştirerek aşağıdaki komutu çalıştırın:

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. nuget.exe yayımlama işleminin sonuçlarını görüntüler:

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

Bkz: [nuget itme](../tools/cli-ref-push.md).

### <a name="publish-errors"></a>Hataları yayımlama

[!INCLUDE[publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Yayımlanan paket yönetme

[!INCLUDE[publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a>İlgili konular

- [Bir paket oluşturun](../create-packages/creating-a-package.md)
- [Paket Yayımlama](../create-packages/publish-a-package.md)
- [Birden çok hedef çerçeveyi desteği](../create-packages/supporting-multiple-target-frameworks.md)
- [Paket sürümü oluşturma](../reference/package-versioning.md)
- [Yerelleştirilmiş paketler oluşturma](../create-packages/creating-localized-packages.md)
