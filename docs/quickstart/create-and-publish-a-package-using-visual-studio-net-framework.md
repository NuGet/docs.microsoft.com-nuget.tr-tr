---
title: Windows üzerinde Visual Studio 'Yu kullanarak .NET Framework NuGet paketi oluşturma ve yayımlama
description: Windows üzerinde Visual Studio kullanarak .NET Framework NuGet paketi oluşturma ve yayımlama hakkında bir adım adım öğretici.
author: JonDouglas
ms.author: jodou
ms.date: 05/13/2018
ms.topic: quickstart
ms.openlocfilehash: 7c030db769973e3b3c41da6523d57ab2cd769a9d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775754"
---
# <a name="quickstart-create-and-publish-a-package-using-visual-studio-net-framework-windows"></a>Hızlı başlangıç: Visual Studio (.NET Framework, Windows) kullanarak paket oluşturma ve yayımlama

Bir .NET Framework sınıf kitaplığından bir NuGet paketi oluşturma işlemi, Windows üzerinde Visual Studio 'da DLL oluşturmayı, ardından paketi oluşturmak ve yayımlamak için nuget.exe komut satırı aracını kullanmayı içerir.

> [!Note]
> Bu hızlı başlangıç yalnızca Windows için Visual Studio 2017 ve sonraki sürümleri için geçerlidir. Mac için Visual Studio burada açıklanan özellikleri içermez. Bunun yerine [DotNet CLI araçlarını](create-and-publish-a-package-using-the-dotnet-cli.md) kullanın.

## <a name="prerequisites"></a>Ön koşullar

1. [VisualStudio.com](https://www.visualstudio.com/) ' den herhangi bir Visual Studio 2017 veya üzeri sürümü ile yükleyin. NET ilgili iş yükü. Visual Studio 2017, .NET iş yükü yüklendiğinde NuGet yeteneklerini otomatik olarak içerir.

1. `nuget.exe` [NuGet.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe)adresinden indirerek, bu `.exe` dosyayı uygun bir klasöre KAYDEDEREK ve bu klasörü PATH ortam değişkeninizden ekleyerek CLI 'yı yükleme.

1. Henüz bir [hesabınız yoksa NuGet.org üzerinde ücretsiz bir hesaba kaydolun](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) . Yeni hesap oluşturma onay e-postası gönderir. Bir paketi karşıya yükleyebilmek için önce hesabı onaylamanız gerekir.

## <a name="create-a-class-library-project"></a>Sınıf kitaplığı projesi oluşturma

Paketlemek istediğiniz kod için mevcut bir .NET Framework sınıf kitaplığı projesini kullanabilir veya basit bir tane oluşturabilirsiniz:

1. Visual Studio 'da **dosya > yeni > proje**' yi seçin, **Visual C#** düğümünü seçin, "sınıf kitaplığı (.NET Framework)" şablonunu seçin, projeyi appgünlükçü olarak adlandırın ve **Tamam**' a tıklayın.

1. Ortaya çıkan proje dosyasına sağ tıklayın ve projenin düzgün oluşturulduğundan emin olmak için **Oluştur** ' u seçin. DLL, hata ayıklama klasöründe bulunur (veya bunun yerine bu yapılandırmayı oluşturursanız sürüm).

Gerçek bir NuGet paketi içinde, diğerlerinin uygulama derleyebileceği birçok yararlı özelliği uygulayacağınızı görürsünüz. Hedef çerçeveleri de istediğiniz şekilde ayarlayabilirsiniz. Örneğin, [UWP](../guides/create-uwp-packages.md) ve [Xamarin](../guides/create-packages-for-xamarin.md)kılavuzlarını inceleyin.

Ancak bu izlenecek yol için, şablondan bir sınıf kitaplığı bir paket oluşturmak için yeterli olduğundan ek kod yazmayacaktır. Hala, paket için bir işlev kodu isterseniz, aşağıdakileri kullanın:

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
> Aksi takdirde seçim yapmanız gerekmediğiniz sürece, en geniş kapsamlı proje yelpazğuyla uyumluluk sağladığından NuGet paketleri için tercih edilen hedef .NET Standard. Bkz. [Visual Studio kullanarak paket oluşturma ve yayımlama (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).

## <a name="configure-project-properties-for-the-package"></a>Paket için proje özelliklerini yapılandırma

Bir NuGet paketi, `.nuspec` paket tanımlayıcısı, sürüm numarası, açıklama ve daha fazlası gibi ilgili meta verileri içeren bir bildirim (dosya) içerir. Bunlardan bazıları proje özelliklerinden doğrudan çizilebilirler ve bu, hem projede hem de bildirimde ayrı ayrı güncelleştirilmesini önler. Bu bölümde, uygulanabilir özelliklerin nerede ayarlanacağı açıklanır.

1. **Proje > Özellikler** menü komutunu seçin, sonra **uygulama** sekmesini seçin.

1. **Derleme adı** alanında, paketinize benzersiz bir tanımlayıcı verin.

    > [!Important]
    > Pakete, nuget.org genelinde veya kullandığınız herhangi bir konakta benzersiz bir tanımlayıcı vermeniz gerekir. Bu izlenecek yol için, "örnek" veya "test" adını, sonraki yayımlama adımı, paketi herkese açık hale getirir (ancak gerçekten onu kullanacağından çok fazla olabilir).
    >
    > Zaten var olan bir ada sahip bir paketi yayımlamayı denerseniz, bir hata görürsünüz.

1. Bildirimde bulunan diğer özellikleri girebileceğiniz bir iletişim kutusu getiren **derleme bilgileri...** düğmesini seçin (bkz [. nuspec dosya başvurusu-değiştirme belirteçleri](../reference/nuspec.md#replacement-tokens)). En yaygın olarak kullanılan alanlar **başlık**, **Açıklama**, **Şirket**, **telif hakkı** ve **derleme sürümüdür**. Bu özellikler, nuget.org gibi bir konakta paket ile birlikte görüntülenir, bu nedenle tamamen açıklayıcı olduklarından emin olun.

    ![Visual Studio 'da bir .NET Framework projesindeki derleme bilgileri](media/qs_create-vs-01b-project-properties.png)

1. İsteğe bağlı: özellikleri doğrudan görmek ve düzenlemek için `Properties/AssemblyInfo.cs` dosyayı projede açın.

1. Özellikler ayarlandığında, proje yapılandırmasını **serbest bırak** olarak ayarlayın ve güncelleştirilmiş dll 'yi oluşturmak için projeyi yeniden derleyin.

## <a name="generate-the-initial-manifest"></a>Başlangıç bildirimini oluşturma

Birlikte ve proje özellikleri ayarlanmış bir DLL ile, bundan sonra `nuget spec` projeden bir başlangıç dosyası oluşturmak için komutunu kullanırsınız `.nuspec` . Bu adım, proje dosyasından bilgi çizmek için ilgili değiştirme belirteçlerini içerir.

`nuget spec`İlk bildirimi oluşturmak için yalnızca bir kez çalıştırırsınız. Paketi güncelleştirirken, projenizdeki değerleri değiştirirsiniz ya da bildirimi doğrudan düzenleyebilirsiniz.

1. Bir komut istemi açın ve dosyayı içeren proje klasörüne gidin `AppLogger.csproj` .

1. Şu komutu çalıştırın: `nuget spec AppLogger.csproj` . NuGet bir proje belirterek, bu durumda projenin adıyla eşleşen bir bildirim oluşturur `AppLogger.nuspec` . Ayrıca, bildirimde değiştirme belirteçleri de bulunur.

1. `AppLogger.nuspec`İçeriğini incelemek için bir metin düzenleyicisinde açın ve aşağıdaki gibi görünmelidir:

    ```xml
    <?xml version="1.0"?>
    <package >
      <metadata>
        <id>Package</id>
        <version>1.0.0</version>
        <authors>YourUsername</authors>
        <owners>YourUsername</owners>
        <license type="expression">MIT</license>
        <projectUrl>http://PROJECT_URL_HERE_OR_DELETE_THIS_LINE</projectUrl>
        <iconUrl>http://ICON_URL_HERE_OR_DELETE_THIS_LINE</iconUrl>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Package description</description>
        <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
        <copyright>Copyright 2019</copyright>
        <tags>Tag1 Tag2</tags>
      </metadata>
    </package>
    ```

## <a name="edit-the-manifest"></a>Bildirimi düzenleme

1. Dosyanızdaki varsayılan değerlerle bir paket oluşturmayı denerseniz NuGet bir hata oluşturur `.nuspec` , bu nedenle devam etmeden önce aşağıdaki alanları düzenlemeniz gerekir. Bunların nasıl kullanıldığına ilişkin bir açıklama için bkz [.. nuspec dosya başvurusu-isteğe bağlı meta veri öğeleri](../reference/nuspec.md#optional-metadata-elements) .

    - licenseUrl
    - projectUrl
    - Iurl
    - relet 'ler
    - etiketler

1. Genel kullanım için oluşturulmuş paketler için Etiketler özelliğine özel dikkat edin, **Etiketler başkalarının** paketinizi NuGet.org gibi kaynaklar üzerinde bulmasına yardımcı olur ve ne yaptığını anlayın.

1. Ayrıca, [. nuspec dosya başvurusu](../reference/nuspec.md)bölümünde açıklandığı gibi, şu anda bildirime başka öğeler de ekleyebilirsiniz.

1. Devam etmeden önce dosyayı kaydedin.

## <a name="run-the-pack-command"></a>Pack komutunu çalıştırın

1. Dosyanızı içeren klasörde bir komut isteminden `.nuspec` komutunu çalıştırın `nuget pack` .

1. NuGet `.nupkg` , geçerli klasörde bulacağınız *Identifier-Version. nupkg* biçiminde bir dosya oluşturur.

## <a name="publish-the-package"></a>Paketi Yayımla

Bir dosyaya sahip olduktan sonra `.nupkg` , `nuget.exe` NuGet.org ' den ALıNAN bir API anahtarı ile kullanarak NuGet.org 'e yayımlayabilirsiniz. Nuget.org için `nuget.exe` 4.1.0 veya üzeri bir sürümü kullanmanız gerekir.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>API anahtarınızı alın

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a>NuGet Push ile yayımlama

1. Bir komut satırı açın ve dosyayı içeren klasöre geçin `.nupkg` .

1. Aşağıdaki komutu çalıştırarak, paket adınızı belirtip anahtar değerini API anahtarınızla değiştirin:

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

Bkz. [NuGet Push](../reference/cli-reference/cli-ref-push.md).

### <a name="publish-errors"></a>Yayımlama hataları

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Yayınlanan paketi yönetme

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="next-steps"></a>Sonraki adımlar

İlk NuGet paketinizi oluştururken Tebrikler!

> [!div class="nextstepaction"]
> [Paket oluşturma](../create-packages/creating-a-package.md)

NuGet 'in sunabileceği daha fazlasını araştırmak için aşağıdaki bağlantıları seçin.

- [Paket yayımlama](../nuget-org/publish-a-package.md)
- [Yayın öncesi paketler](../create-packages/Prerelease-Packages.md)
- [Birden çok hedef çerçeveyi destekleme](../create-packages/supporting-multiple-target-frameworks.md)
- [Paket sürümü oluşturma](../concepts/package-versioning.md)
- [Yerelleştirilmiş paketler oluşturma](../create-packages/creating-localized-packages.md)
