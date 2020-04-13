---
title: Windows'da Visual Studio'u kullanarak bir .NET Framework NuGet paketi oluşturun ve yayımlayın
description: Windows'da Visual Studio'u kullanarak bir .NET Framework NuGet paketi oluşturma ve yayımlama hakkında bir iz geçidi öğretici.
author: karann-msft
ms.author: karann
ms.date: 05/13/2018
ms.topic: quickstart
ms.openlocfilehash: e00aac83a710e2f745d5e4bb9aec741ee686e595
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "72380639"
---
# <a name="quickstart-create-and-publish-a-package-using-visual-studio-net-framework-windows"></a>Quickstart: Visual Studio (.NET Framework, Windows) kullanarak bir paket oluşturun ve yayımlayın

.NET Framework Class Kitaplığı'ndan bir NuGet paketi oluşturmak, Windows'da Visual Studio'da DLL oluşturmayı ve paketi oluşturmak ve yayımlamak için nuget.exe komut satırı aracını kullanmayı içerir.

> [!Note]
> Bu Quickstart Visual Studio 2017 ve yalnızca Windows için daha yüksek sürümler için geçerlidir. Mac için Visual Studio burada açıklanan yetenekleri içermez. Bunun yerine [dotnet CLI araçlarını](create-and-publish-a-package-using-the-dotnet-cli.md) kullanın.

## <a name="prerequisites"></a>Ön koşullar

1. Visual Studio 2017 veya daha yüksek herhangi bir sürümünü [visualstudio.com](https://www.visualstudio.com/) herhangi bir . NET ile ilgili iş yükü. Visual Studio 2017, bir .NET iş yükü yüklendiğinde NuGet özelliklerini otomatik olarak içerir.

1. CLI'yi `nuget.exe` [nuget.org'dan](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe)indirerek yükleyin, dosyayı `.exe` uygun bir klasöre kaydedin ve bu klasörü PATH ortamı değişkeninize eklediniz.

1. Zaten bir hesabınız yoksa [nuget.org ücretsiz bir hesaba kaydolun.](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) Yeni bir hesap oluşturmak bir onay e-postası gönderir. Bir paket yükleyemeden önce hesabı onaylamanız gerekir.

## <a name="create-a-class-library-project"></a>Sınıf kitaplığı projesi oluşturma

Paketlemek istediğiniz kod için varolan bir .NET Framework Class Kitaplığı projesini kullanabilir veya aşağıdaki gibi basit bir kitap oluşturabilirsiniz:

1. Visual **Studio'da, Dosya > Yeni > Projesi'ni**seçin, **Visual C#** düğümünü seçin, "Sınıf Kitaplığı (.NET Framework)" şablonuna tıklayın, proje AppLogger'ı adlandırın ve **Tamam'ı**tıklatın.

1. Projenin düzgün oluşturulduğundan emin olmak için ortaya çıkan proje dosyasına sağ tıklayın ve **Yapı'yı** seçin. DLL Hata Ayıklama klasöründe bulunur (veya bu yapılandırmayı oluşturursanız serbest bırakın).

Gerçek bir NuGet paketi içinde, tabii ki, başkalarının uygulamaları oluşturabilirsiniz birçok yararlı özellikleri uygulamak. Hedef çerçeveleri istediğiniz gibi de ayarlayabilirsiniz. Örneğin, [UWP](../guides/create-uwp-packages.md) ve [Xamarin](../guides/create-packages-for-xamarin.md)kılavuzlarına bakın.

Ancak bu geçiş için, şablondan bir sınıf kitaplığı bir paket oluşturmak için yeterli olduğundan, ek kod yazmazsınız. Yine de, paket için bazı işlevsel kod istiyorsanız, aşağıdakileri kullanın:

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
> Aksini seçmek için bir nedeniniz yoksa, .NET Standard, en geniş tüketici proje yelpazesiyle uyumluluk sağladığından NuGet paketleri için tercih edilen hedeftir. Bkz. [Visual Studio (.NET Standard) kullanarak bir paket oluşturun ve yayımlayın.](create-and-publish-a-package-using-visual-studio.md)

## <a name="configure-project-properties-for-the-package"></a>Paket için proje özelliklerini yapılandırma

NuGet paketi, paket tanımlayıcısı, sürüm numarası, açıklama ve daha fazlası gibi ilgili meta verileri içeren bir bildirim `.nuspec` (dosya) içerir. Bunlardan bazıları doğrudan proje özelliklerinden çıkarılabilir, bu da bunları hem projede hem de bildirimde ayrı ayrı güncelleştirmekten kaçınır. Bu bölümde, ilgili özelliklerin nerede ayarlandığı açıklanmaktadır.

1. Project **> Properties** menüsü komutunu seçin ve ardından **Uygulama** sekmesini seçin.

1. Assembly **ad** alanında, paketinize benzersiz bir tanımlayıcı verin.

    > [!Important]
    > Pakete, nuget.org veya kullandığınız ana bilgisayarda benzersiz bir tanımlayıcı vermelisiniz. Bu izlenecek yol için, daha sonraki yayımlama adımı paketi herkese açık hale getirebildiğinden (kimsenin gerçekten kullanması pek olası olmasa da) adına "Örnek" veya "Test" eklenmesini öneririz.
    >
    > Zaten var olan bir ada sahip bir paketi yayımlamaya çalışırsanız, bir hata görürsünüz.

1. Bildirime giren diğer özellikleri girebileceğiniz bir iletişim kutusu oluşturan **Derleme Bilgileri...** düğmesini seçin (bkz. [.nuspec dosya başvurusu - değiştirme belirteçleri).](../reference/nuspec.md#replacement-tokens) En sık kullanılan alanlar **Başlık**, **Açıklama**, **Şirket**, **Telif Hakkı**ve Montaj **sürümü.** Bu özellikler sonuçta paketiniz nuget.org gibi bir ana bilgisayarda görünür, bu nedenle tamamen açıklayıcı olduğundan emin olun.

    ![Visual Studio'da bir .NET Framework projesinde montaj bilgileri](media/qs_create-vs-01b-project-properties.png)

1. İsteğe bağlı: Özellikleri doğrudan görmek ve `Properties/AssemblyInfo.cs` denetlemek için projedeki dosyayı açın.

1. Özellikler ayarlandığında, proje yapılandırmasını **Release'e** ayarlayın ve güncelleştirilmiş DLL'yi oluşturmak için projeyi yeniden oluşturun.

## <a name="generate-the-initial-manifest"></a>İlk bildirimi oluşturma

Elinde bir DLL ve proje özellikleri kümesi `nuget spec` yle, artık `.nuspec` projeden bir başlangıç dosyası oluşturmak için komutu kullanırsınız. Bu adım, proje dosyasından bilgi çekmek için ilgili değiştirme belirteçlerini içerir.

İlk `nuget spec` bildirimi oluşturmak için yalnızca bir kez çalışırsınız. Paketi güncellerken, projenizdeki değerleri değiştirir veya doğrudan bildirimi değiştirirsiniz.

1. Komut istemini açın ve dosya `AppLogger.csproj` içeren proje klasörüne gidin.

1. Aşağıdaki komutu `nuget spec AppLogger.csproj`çalıştırın: . NuGet, bir proje belirterek, bu durumda `AppLogger.nuspec`projenin adı ile eşleşen bir bildirim oluşturur. Ayrıca, bildirimde yedek belirteçler de içerir.

1. `AppLogger.nuspec` Aşağıdaki gibi görünmesi gereken içeriğini incelemek için bir metin düzenleyicisi açın:

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

## <a name="edit-the-manifest"></a>Bildirimi edin

1. NuGet, dosyanızda `.nuspec` varsayılan değerler içeren bir paket oluşturmaya çalışırsanız bir hata oluşturur, bu nedenle devam etmeden önce aşağıdaki alanları yeniden oluşturmanız gerekir. Bkz. .nuspec dosya başvurusu - bunların nasıl kullanıldığına yönelik bir açıklama için [isteğe bağlı meta veri öğeleri.](../reference/nuspec.md#optional-metadata-elements)

    - lisansUrl
    - projeUrl
    - iconUrl
    - releaseNotes
    - etiketler

1. Genel tüketim için oluşturulmuş paketler için, etiketler diğerlerinin paketinizi nuget.org gibi kaynaklarda bulmasına ve ne işe yaradığına yardımcı olduğundan, **Etiketler** özelliğine özel olarak dikkat edin.

1. [.nuspec dosya başvurusunda](../reference/nuspec.md)açıklandığı gibi, şu anda bildirime başka öğeler de ekleyebilirsiniz.

1. İşleme başlamadan önce dosyayı kaydedin.

## <a name="run-the-pack-command"></a>Sürü komutunu çalıştırın

1. Dosyanızı `.nuspec` içeren klasördeki bir komut isteminden `nuget pack`komutu çalıştırın.

1. NuGet, geçerli `.nupkg` klasörde bulacağınız *tanımlayıcı-version.nupkg*şeklinde bir dosya oluşturur.

## <a name="publish-the-package"></a>Paketi yayımlama

Bir `.nupkg` dosyaya sahip olduktan sonra, `nuget.exe` nuget.org'dan edinilen bir API anahtarıyla dosyayı nuget.org olarak yayımlarsınız. nuget.org için 4.1.0 veya daha yüksek kullanmanız `nuget.exe` gerekir.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>API anahtarınızı edinin

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a>Nuget push ile yayımla

1. Bir komut satırı açın ve dosyayı içeren klasöre değiştirin. `.nupkg`

1. Paket adınızı belirterek ve anahtar değerini API anahtarınızla değiştirerek aşağıdaki komutu çalıştırın:

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. nuget.exe yayımlama sürecinin sonuçlarını görüntüler:

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

Nuget [itme](../reference/cli-reference/cli-ref-push.md)bakın .

### <a name="publish-errors"></a>Hataları yayımlama

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Yayımlanmış paketi yönetme

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="next-steps"></a>Sonraki adımlar

İlk NuGet paketinizi oluşturduğunuz için tebrikler!

> [!div class="nextstepaction"]
> [Paket Oluşturma](../create-packages/creating-a-package.md)

NuGet'in sunduğu daha fazlasını keşfetmek için aşağıdaki bağlantıları seçin.

- [Paket Yayınlama](../nuget-org/publish-a-package.md)
- [Ön Sürüm Paketleri](../create-packages/Prerelease-Packages.md)
- [Birden çok hedef çerçeveyi destekleme](../create-packages/supporting-multiple-target-frameworks.md)
- [Paket sürüm](../concepts/package-versioning.md)
- [Yerelleştirilmiş paketler oluşturma](../create-packages/creating-localized-packages.md)
