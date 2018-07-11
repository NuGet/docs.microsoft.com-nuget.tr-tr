---
title: Windows üzerinde Visual Studio kullanarak bir .NET Framework paketi oluşturma ve yayımlama
description: Oluşturma ve Windows üzerinde Visual Studio 2017'yi kullanarak bir .NET Framework NuGet Paketi Yayımlama Kılavuzu öğretici.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/13/2018
ms.topic: quickstart
ms.openlocfilehash: ffa2128b577673e980f4115f37f8685858c36250
ms.sourcegitcommit: 6cffa6ef59b922df2d87aa9c24034d00542983cd
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/10/2018
ms.locfileid: "37963165"
---
# <a name="quickstart-create-and-publish-a-package-using-visual-studio-net-framework-windows"></a>Hızlı Başlangıç: Oluşturma ve Visual Studio (.NET Framework, Windows) kullanarak bir paket yayımlama

Windows üzerinde Visual Studio'da DLL'i oluşturmak ve ardından paketi oluşturma ve yayımlama için nuget.exe komut satırı aracını kullanarak bir .NET Framework Sınıf Kitaplığı'ndan bir NuGet paketi oluşturma içerir.

> [!Note]
> Bu hızlı başlangıçta, Visual Studio 2017'ye yalnızca Windows için geçerlidir. Mac için Visual Studio, burada açıklanan özellikleri içermez. Kullanım [dotnet CLI Araçları](create-and-publish-a-package-using-the-dotnet-cli.md) yerine.

## <a name="prerequisites"></a>Önkoşullar

1. Visual Studio 2017'den herhangi bir sürümünü yükleme [visualstudio.com](https://www.visualstudio.com/) herhangi. AĞ ile ilgili bir iş yükü. .NET iş yükü yüklendiğinde visual Studio 2017, NuGet özellikleri otomatik olarak içerir.

1. Yükleme `nuget.exe` ondan indirerek CLI [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), kaydetme `.exe` uygun bir klasöre dosya ve klasörün PATH ortam değişkeninize ekleme.

1. [Nuget.org üzerindeki bir ücretsiz hesaba kaydolun](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) zaten yoksa. Yeni bir hesap oluşturmadan bir onay e-posta gönderir. Bir paketi karşıya yükleyebilmeniz, hesap onaylamanız gerekir.

## <a name="create-a-class-library-project"></a>Bir sınıf kitaplığı projesi oluşturun

Mevcut bir .NET Framework sınıf kitaplığı projesi paketini veya basit bir şekilde oluşturmak istediğiniz kodu kullanabilirsiniz:

1. Visual Studio'da **Dosya > Yeni > Proje**seçin **Visual C#** düğümü, "Sınıf kitaplığı (.NET Framework)" şablonu seçin, AppLogger Projeyi adlandırın ve tıklayın **Tamam**.

1. Sonuçta elde edilen proje dosyasını sağ tıklatın ve seçin **derleme** proje düzgün oluşturulduğu emin olmak için. DLL hata ayıklama klasörü (veya bunun yerine, yapılandırma derleme yaparsanız sürüm) içinde bulunur.

Gerçek bir NuGet paketi içinde Elbette ile diğer uygulamaları oluşturabileceğiniz birçok yararlı özellik uygulayın. Ancak, istediğiniz hedef çerçeveleri de ayarlayabilirsiniz. Örneğin, kılavuzları için bkz. [UWP](../guides/create-uwp-packages.md) ve [Xamarin](../guides/create-packages-for-xamarin.md).

Şablon sınıf kitaplığından bir paketi oluşturmak yeterli olduğundan bu kılavuz için ancak herhangi bir ek kod yazmanız gerekmez. Yine de bazı işlevsel kod paketi için isterseniz aşağıdakini kullanın:

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
> Aksi takdirde seçmek için bir nedeniniz yoksa projeleri kullanan geniş kapsamlı uyumluluk sağlar .NET Standard NuGet paketlerini tercih edilen hedef aynıdır. Bkz: [oluşturun ve Visual Studio (.NET Standard) kullanarak bir paket yayımlama](create-and-publish-a-package-using-visual-studio.md).

## <a name="configure-project-properties-for-the-package"></a>Paket için proje özelliklerini yapılandır

Bir NuGet paketi içeren bir bildirime (bir `.nuspec` dosyası), içeren uygulamanın paket tanımlayıcısı, sürüm numarası, açıklama ve diğer ilgili meta verileri. Bunların bazılarını, proje özellikleri doğrudan, hem proje hem de bildirim ayrı ayrı güncelleştirme gereğini ortadan kaldırır kurulabilir. Bu bölümde, ilgili özellikleri ayarlamak nereye açıklanmaktadır.

1. Seçin **Proje > Özellikleri** menü komutunu ve ardından **uygulama** sekmesi.

1. İçinde **derleme adı** alanında, benzersiz bir tanımlayıcı paketinizi verin.

    > [!Important]
    > Nuget.org veya, konak arasında benzersiz bir tanımlayıcı kullanmakta olduğunuz paket vermeniz gerekir. Bu kılavuz için (Bu herkes gerçekten kullanacağı olsa da) yayımlama sonraki adım paketi herkese görünür hale "Örnek" veya "Test" adı dahil olmak üzere öneririz.
    >
    > Zaten bir ada sahip bir paketi yayımlamaya çalışırsanız, bir hata görürsünüz.

1. Seçin **derleme bilgileri...**  içinde girebilirsiniz taşıyan diğer özellikleri bildirimine bir iletişim kutusu getirir düğmesini (bkz [.nuspec dosyası başvurusu - değiştirme belirteçleri](../reference/nuspec.md#replacement-tokens)). En sık kullanılan alanlar **başlık**, **açıklama**, **şirket**, **telif hakkı**, ve **derlemesürümü**. Bu özellikler, nuget.org gibi bir konak üzerinde paket ile sonuçta görünür. Bu nedenle bunlar tamamen açıklayıcı olduğunuzdan emin olun.

    ![Visual Studio .NET Framework projede derleme bilgileri](media/qs_create-vs-01b-project-properties.png)

1. İsteğe bağlı: görmek ve doğrudan özelliklerini düzenlemek için açın `Properties/AssemblyInfo.cs` proje dosyasında.

1. Özellikleri ayarladığınızda, proje yapılandırmasını ayarlayın **yayın** ve güncelleştirilmiş DLL'i oluşturmak için projeyi yeniden derleyin.

## <a name="generate-the-initial-manifest"></a>İlk bildirim oluştur

Şimdi el ve proje özelliklerini kümesindeki bir DLL ile kullanmanız `nuget spec` bir ilk oluşturmak için komutu `.nuspec` proje dosyası. Bu adım, proje dosyasından bilgileri çizmek için ilgili değiştirme belirteçleri içerir.

Çalıştırmadan `nuget spec` ilk bildirim oluşturmak üzere yalnızca bir kez. Paketin güncelleştirilmesi, projenizde değerlerini değiştirmek veya doğrudan bildirimi düzenleyin.

1. Bir komut istemi açın ve projeyi içeren klasöre gidin `AppLogger.csproj` dosya.

1. Aşağıdaki komutu çalıştırın: `nuget spec AppLogger.csproj`. Bir proje belirterek, NuGet bu durumda proje adıyla eşleşen bir bildirim oluşturur `AppLogger.nuspec`. Bunu de değiştirme belirteçleri bildiriminde.

1. Açık `AppLogger.nuspec` içeriğini incelemek için bir metin düzenleyicisinde, aşağıdaki gibi görünmelidir:

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

## <a name="edit-the-manifest"></a>Bildirimi düzenleyin

1. NuGet, varsayılan değerleri içeren bir paket oluşturmayı denerseniz bir hata üretir, `.nuspec` dosya için devam etmeden önce aşağıdaki alanları düzenlemeniz gerekir. Bkz: [.nuspec dosyası başvurusu - tek öğeleri](../reference/nuspec.md#single-elements) için bunların nasıl kullanıldığı bir açıklama.

    - licenseUrl
    - projectUrl
    - iconUrl
    - releaseNotes
    - etiketler

1. Ortak tüketim için oluşturulan paketler için özel dikkat **etiketleri** özelliği etiketleri diğerlerinin nuget.org gibi kaynaklar üzerinde paketinizi bulun ve ne yaptığını anlamanıza yardımcı olarak.

1. De diğer öğeleri için bildirim şu anda üzerinde açıklandığı ekleyebilirsiniz [.nuspec dosyası başvurusu](../reference/nuspec.md).

1. Devam etmeden önce dosyayı kaydedin.

## <a name="run-the-pack-command"></a>Paketi komutunu çalıştırın

1. İçeren klasörü içinde bir komut isteminden, `.nuspec` dosyası komutu Çalıştır `nuget pack`.

1. NuGet oluşturur bir `.nupkg` dosya biçiminde *tanımlayıcı version.nupkg*, geçerli klasörde bulabilirsiniz.

## <a name="publish-the-package"></a>Paket yayımlama

Sonra bir `.nupkg` dosyası yayımladığınızda, nuget.org kullanarak `nuget.exe` sahip bir API anahtarı nuget.org adresinden alındı. Nuget.org için kullanmanız gereken `nuget.exe` 4.1.0 veya üzeri.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>API anahtarınızı alma

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a>Nuget itme ile yayımlama

1. Değiştirmek için içeren klasör `.nupkg` dosya.

1. Paketinizin adını belirterek ve API anahtarınızı anahtar değerini değiştirerek aşağıdaki komutu çalıştırın:

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

Bkz: [nuget anında iletme](../tools/cli-ref-push.md).

### <a name="publish-errors"></a>Hataları yayımlama

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Yayımlanan paket yönetme

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a>İlgili konular

- [Paket oluşturma](../create-packages/creating-a-package.md)
- [Paket Yayımlama](../create-packages/publish-a-package.md)
- [Yayın öncesi paketleri](../create-packages/Prerelease-Packages.md)
- [Birden çok hedef çerçeve desteği](../create-packages/supporting-multiple-target-frameworks.md)
- [Paket sürümü oluşturma](../reference/package-versioning.md)
- [Yerelleştirilmiş paketler oluşturma](../create-packages/creating-localized-packages.md)
