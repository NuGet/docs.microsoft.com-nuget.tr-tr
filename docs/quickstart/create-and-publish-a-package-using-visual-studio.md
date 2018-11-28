---
title: Windows üzerinde Visual Studio kullanarak bir .NET Standard paketi oluşturma ve yayımlama
description: Oluşturma ve Windows üzerinde Visual Studio 2017 kullanılarak bir standart .NET NuGet Paketi Yayımlama Kılavuzu öğretici.
author: karann-msft
ms.author: karann
ms.date: 05/18/2018
ms.topic: quickstart
ms.openlocfilehash: faea00372bd387aee1502e388ad1ea88de07b95d
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453526"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a>Hızlı Başlangıç: Oluşturma ve Visual Studio (.NET Standard, yalnızca Windows) kullanarak bir NuGet paketi Yayımla

Bir .NET standart sınıf kitaplığı Windows üzerinde Visual Studio'da NuGet paketi oluşturun ve ardından bir CLI aracını kullanarak nuget.org için yayımlama için basit bir işlemdir.

> [!Note]
> Bu hızlı başlangıçta, Visual Studio 2017'ye yalnızca Windows için geçerlidir. Mac için Visual Studio, burada açıklanan özellikleri içermez. Kullanım [dotnet CLI Araçları](create-and-publish-a-package-using-the-dotnet-cli.md) yerine.

## <a name="prerequisites"></a>Önkoşullar

1. Visual Studio 2017'den herhangi bir sürümünü yükleme [visualstudio.com](https://www.visualstudio.com/) herhangi. AĞ ile ilgili bir iş yükü. .NET iş yükü yüklendiğinde visual Studio 2017, NuGet özellikleri otomatik olarak içerir.

1. Yükleme `nuget.exe` ondan indirerek CLI [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), kaydetme `.exe` uygun bir klasöre dosya ve klasörün PATH ortam değişkeninize ekleme.

    Alternatif olarak, varsa [.NET Core SDK'sı](https://www.microsoft.com/net/download/) kullanabileceğiniz yüklü `dotnet` CLI.

1. [Nuget.org üzerindeki bir ücretsiz hesaba kaydolun](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) zaten yoksa. Yeni bir hesap oluşturmadan bir onay e-posta gönderir. Bir paketi karşıya yükleyebilmeniz, hesap onaylamanız gerekir.

## <a name="create-a-class-library-project"></a>Bir sınıf kitaplığı projesi oluşturun

Mevcut .NET standart sınıf kitaplığı projesinde paketini veya basit bir şekilde oluşturmak istediğiniz kodu kullanabilirsiniz:

1. Visual Studio'da **Dosya > Yeni > Proje**, genişletme **Visual C# > .NET Standard** düğümü, "Sınıf kitaplığı (.NET Standard)" şablonu seçin, AppLogger Projeyi adlandırın ve **Tamam**.

1. Sonuçta elde edilen proje dosyasını sağ tıklatın ve seçin **derleme** proje düzgün oluşturulduğu emin olmak için. DLL hata ayıklama klasörü (veya bunun yerine, yapılandırma derleme yaparsanız sürüm) içinde bulunur.

Gerçek bir NuGet paketi içinde Elbette ile diğer uygulamaları oluşturabileceğiniz birçok yararlı özellik uygulayın. Şablon sınıf kitaplığından bir paketi oluşturmak yeterli olduğundan bu kılavuz için ancak herhangi bir ek kod yazmanız gerekmez. Yine de bazı işlevsel kod paketi için isterseniz aşağıdakini kullanın:

```cs
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
> Aksi takdirde seçmek için bir nedeniniz yoksa projeleri kullanan geniş kapsamlı uyumluluk sağlar .NET Standard NuGet paketlerini tercih edilen hedef aynıdır.

## <a name="configure-package-properties"></a>Paket özelliklerini yapılandırma

1. Seçin **Proje > Özellikleri** menü komutunu ve ardından **paket** sekmesi. ( **Paket** .NET Framework hedefliyorsanız, yalnızca .NET Standard sınıf kitaplığı projeleri için; sekmesi görünür bkz [oluşturma ve bir .NET Framework Paketi Yayımlama](create-and-publish-a-package-using-visual-studio-net-framework.md) bunun yerine. .NET Standard projesi görünmüyorsa, Visual Studio 2017 en son sürüme güncelleştirmeniz gerekebilir.)

    ![Visual Studio projesinde NuGet paket özellikleri](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > Ortak tüketim için oluşturulan paketler için özel dikkat **etiketleri** özelliği olarak etiketler diğerlerinin paketinize bulun ve ne yaptığını anlamanıza yardımcı olur.

1. Benzersiz bir tanımlayıcı paketinizi vermek ve diğer istenen özellikleri doldurun. Farklı özellikleri açıklaması için bkz: [.nuspec dosyası başvurusu](../reference/nuspec.md). Burada tüm özellikler kısımlarda `.nuspec` Visual Studio projesi için oluşturduğu bildirimi.

    > [!Important]
    > Nuget.org veya, konak arasında benzersiz bir tanımlayıcı kullanmakta olduğunuz paket vermeniz gerekir. Bu kılavuz için (Bu herkes gerçekten kullanacağı olsa da) yayımlama sonraki adım paketi herkese görünür hale "Örnek" veya "Test" adı dahil olmak üzere öneririz.
    >
    > Zaten bir ada sahip bir paketi yayımlamaya çalışırsanız, bir hata görürsünüz.

1. İsteğe bağlı: doğrudan proje dosyasındaki özellikleri görmek için Çözüm Gezgini'nde projeye sağ tıklayıp **Düzenle AppLogger.csproj**.

## <a name="run-the-pack-command"></a>Paketi komutunu çalıştırın

1. Yapılandırmayı ayarlamak **yayın**.

1. Projeye sağ tıklayın **Çözüm Gezgini** seçip **paketi** komutu:

    ![Visual Studio Proje bağlam menüsündeki NuGet Paketi komutu](media/qs_create-vs-02-pack-command.png)

1. Visual Studio projeyi derler ve oluşturur `.nupkg` dosya. İnceleme **çıkış** paketi dosyasının yolunu içeren pencere Ayrıntılar (aşağıdakine benzer). Ayrıca derlemesi olduğunu unutmayın. `bin\Release\netstandard2.0` olarak neden önemli olduğuna .NET Standard 2.0 hedef.

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a>Diğer seçenek: MSBuild paketi

Kullanmaya alternatif olarak **paketi** menü komutu, NuGet 4.x+ ve MSBuild 15.1 + destekleyen bir `pack` hedef proje gerekli paket verilerini içerdiğinde. Bir komut istemi açın, proje klasörüne gidin ve aşağıdaki komutu çalıştırın. (MSBuild için gerekli tüm yolları ile yapılandırılacak gibi genellikle "Geliştirici komut istemi için Visual Studio" Başlat Menüsü'nden başlatmak istediğiniz.)

```cli
msbuild -t:pack -p:Configuration=Release
```

Paket ardından bulunabilir `bin\Release` klasör.

Ek seçeneklerle için `msbuild -t:pack`, bkz: [NuGet paketi ve geri yükleme, MSBuild hedefleri](../reference/msbuild-targets.md#pack-target).

## <a name="publish-the-package"></a>Paket yayımlama

Sonra bir `.nupkg` dosyası yayımladığınızda, kullanarak nuget.org için `nuget.exe` CLI veya `dotnet.exe` nuget.org adresinden alınan bir API anahtarı ile birlikte CLI.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>API anahtarınızı alma

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a>Nuget itme ile yayımlama

Bu adım bir alternatifidir `dotnet.exe`.

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

### <a name="publish-with-dotnet-nuget-push"></a>DotNet nuget itme ile yayımlama

Bu adım bir alternatifidir `nuget.exe`.

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a>Hataları yayımlama

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Yayımlanan paket yönetme

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a>Benioku ve diğer dosyaları ekleme

Pakete dahil edilecek dosyalar doğrudan belirtmek için proje dosyasını düzenleyin ve kullanın `content` özelliği:

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

Bu adlı bir dosya dahil eder `readme.txt` paket kökünde. Visual Studio, hemen paket doğrudan yüklendikten sonra düz metin olarak bu dosyanın içeriğini görüntüler. (Benioku dosyaları bağımlılıkların yüklü paketler için görüntülenmez). Örneğin, işte HtmlAgilityPack paketinin Benioku dosyasını nasıl görünür:

![Yükleme sonrasında bir NuGet paketi için bir benioku dosyası görüntüsü](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> Yalnızca proje kök dizininde readme.txt ekleme sonuç paketine dahil açmayacaktır.

## <a name="related-topics"></a>İlgili konular

- [Paket oluşturma](../create-packages/creating-a-package.md)
- [Paket Yayımlama](../create-packages/publish-a-package.md)
- [Yayın öncesi paketleri](../create-packages/Prerelease-Packages.md)
- [Birden çok hedef çerçeve desteği](../create-packages/supporting-multiple-target-frameworks.md)
- [Paket sürümü oluşturma](../reference/package-versioning.md)
- [Yerelleştirilmiş paketler oluşturma](../create-packages/creating-localized-packages.md)
- [.NET standard kitaplığı belgeleri](/dotnet/articles/standard/library)
- [.NET Core ile .NET Framework'ten taşıma](/dotnet/articles/core/porting/index)
