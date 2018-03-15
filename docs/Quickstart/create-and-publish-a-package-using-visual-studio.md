---
title: "Oluşturma ve bir .NET standart Visual Studio kullanarak yayımlama NuGet paketi tanıtım Kılavuzu | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/18/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Oluşturma ve yayımlama Visual Studio 2017 kullanarak bir .NET standart NuGet paketi bir gözden geçirme Öğreticisi."
keywords: "NuGet paketini oluşturma, NuGet paketi yayımlama, NuGet öğretici, Visual Studio NuGet paketi, msbuild paketi oluşturma"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 733fee616601e1d15d8fb5814b5bfb7905ff4a33
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/15/2018
---
# <a name="create-and-publish-a-package-using-visual-studio-net-standard"></a>Oluşturma ve Visual Studio (.NET standart) kullanarak bir paket yayımlama

Bir .NET standart sınıf kitaplığı Visual Studio'da NuGet paketi oluşturun ve ardından CLI aracını kullanarak nuget.org yayımlamak için basit bir işlemdir.

## <a name="prerequisites"></a>Önkoşullar

1. Visual Studio 2017 ' herhangi bir sürümünü yüklemek [visualstudio.com](https://www.visualstudio.com/) herhangi biriyle. NET ilgili iş yükü. .NET iş yükü yüklendikten sonra visual Studio 2017 otomatik olarak NuGet yetenekleri içerir.

1. Yükleme `nuget.exe` buradan yükleyerek CLI [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), kaydetme `.exe` dosya için uygun bir klasör ve bu klasörü PATH ortam değişkenine ekleme.

    Alternatif olarak, varsa [.NET Core SDK](https://www.microsoft.com/net/download/) yüklü, kullanabileceğiniz `dotnet` CLI.

1. [Kayıt nuget.org ücretsiz bir hesap için](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) zaten yoksa. Yeni bir hesap oluşturmadan bir onay e-posta gönderir. Bir paket karşıya yüklemeden önce hesap onaylamanız gerekir.

## <a name="create-a-class-library-project"></a>Sınıf kitaplığı proje oluşturma

Varolan bir .NET standart sınıf kitaplığı proje paketini veya basit bir şekilde oluşturmak için istediğiniz kodu kullanabilirsiniz:

1. Visual Studio'da, **Dosya > Yeni > Proje**, genişletin **Visual C# > .NET standart** düğümü, "Sınıf kitaplığı (.NET standart)" şablonunu seçin, AppLogger proje adı ve **Tamam**.

1. Sonuçta elde edilen proje dosyasını sağ tıklatın ve seçin **yapı** projeyi düzgün bir şekilde oluşturuldu emin olmak için. DLL Debug klasörüne (veya bunun yerine bu yapılandırma yapı sürüm) içinde bulunur.

Gerçek bir NuGet paketi içinde doğal olarak, çok sayıda kullanışlı özellikle ile diğer uygulamaları derleme uygulayın. Bir sınıf kitaplığı şablondan bir paket oluşturmak yeterli olduğundan bu kılavuzda ancak, herhangi bir ek kod yazma olmaz. Yine de, bazı işlevsel kod paketi için isterseniz, aşağıdakileri kullanın:

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
> Aksi takdirde seçmek için bir nedeniniz yoksa projeleri tüketen geniş kapsamlı bir uyum sağlar gibi .NET standart tercih edilen NuGet paketlerini hedefidir.

## <a name="configure-package-properties"></a>Paket özelliklerini yapılandır

1. Seçin **Proje > Özellikler** menü komutunu ve ardından **paket** sekmesi. ( **Paket** sekmesi yalnızca .NET standart Sınıf Kitaplığı projelerinde; .NET Framework hedefliyorsanız, görüntülenir [oluşturma ve .NET Framework Paketi Yayımlama](create-and-publish-a-package-using-visual-studio-net-framework.md) yerine.)

    ![NuGet paket özelliklerinde bir Visual Studio projesi](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > Ortak tüketim için oluşturulan paketler için özellikle dikkat edin **etiketleri** özelliği gibi etiketler başkalarının paketinizi bulun ve neler yaptığını anlamanıza yardımcı olur.

1. Benzersiz bir tanımlayıcı paketinizi verin ve istenen diğer özelliklerini doldurun. Farklı özellikleri açıklaması için bkz: [.nuspec dosyası başvurusu](../reference/nuspec.md). Tüm özellikleri burada yerleştirilmesini `.nuspec` projesi için Visual Studio oluşturur bildirimi.

    > [!Important]
    > Nuget.org veya ne olursa olsun, ana bilgisayar genelinde benzersiz bir tanımlayıcı kullanmakta olduğunuz paket vermeniz gerekir. Bu kılavuz için (Bu herkes gerçekte kullanacağı olsa da) sonraki yayımlama adım paketi herkese görünür hale "Sample" veya "Test" adı dahil olmak üzere öneririz.
    >
    > Zaten bir ada sahip bir paketi yayımlamaya çalışırsanız, bir hata görürsünüz.

1. İsteğe bağlı: Proje dosyası özelliklerinde doğrudan görmek için Çözüm Gezgini'nde projeye sağ tıklayın ve seçin **Düzenle AppLogger.csproj**.

## <a name="run-the-pack-command"></a>Paketi komutunu çalıştırın

1. Yapılandırma kümesi **sürüm**.

1. Projeye sağ tıklayın **Çözüm Gezgini** seçip **paketi** komutu:

    ![Visual Studio Proje bağlam menüsünde NuGet Paketi komutu](media/qs_create-vs-02-pack-command.png)

1. Visual Studio projesi oluşturur ve oluşturur `.nupkg` dosya. İncelemek **çıkış** ayrıntıları (aşağıdakine benzer), paket dosyası yolu içeren penceresi. Ayrıca, yerleşik bütünleştirilmiş olduğunu unutmayın `bin\Release\netstandard2.0` olarak neden önemli olduğuna .NET standart 2.0 hedef.

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a>Diğer seçenek: MSBuild paketiyle

Kullanmaya alternatif olarak **paketi** menü komutu, NuGet 4.x+ ve MSBuild 15.1 + destekleyen bir `pack` hedef proje gerekli paketi veri içerdiğinde. Bir komut istemi açın, proje klasörüne gidin ve aşağıdaki komutu çalıştırın. (MSBuild için tüm gerekli yollarının yapılandırılacak gibi genellikle "Geliştirici komut istemi için Visual Studio" Başlat menüsünden başlatmak istediğiniz.)

```cli
msbuild /t:pack /p:Configuration=Release
```

Paket sonra bulunabilir `bin\Release` klasör.

Ek seçeneklerle için `msbuild /t:pack`, bkz: [NuGet paketi ve geri yükleme MSBuild hedefleri olarak](../reference/msbuild-targets.md#pack-target).

## <a name="publish-the-package"></a>Paket yayımlama

Bulduktan sonra bir `.nupkg` dosyası, yayımlama, kullanarak nuget.org `nuget.exe` CLI veya `dotnet.exe` CLI nuget.org alınan bir API anahtarı ile birlikte.

[!INCLUDE[publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>API anahtarınızı edinin

[!INCLUDE[publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a>Nuget itme ile yayımlama

Bu adım bir alternatifidir `dotnet.exe`.

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

### <a name="publish-with-dotnet-nuget-push"></a>DotNet nuget itme ile yayımlama

Bu adım bir alternatifidir `nuget.exe`.

[!INCLUDE[publish-dotnet](includes/publish-dotnet.md)]

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
- [.NET standart kitaplığı belgeleri](/dotnet/articles/standard/library)
- [.NET Core için .NET Framework'bağlantı noktası oluşturma](/dotnet/articles/core/porting/index)