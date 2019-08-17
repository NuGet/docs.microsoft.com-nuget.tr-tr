---
title: .NET Standard NuGet paketi oluşturma ve yayımlama-Visual Studio Windows üzerinde
description: Windows üzerinde Visual Studio kullanarak .NET Standard NuGet paketi oluşturma ve yayımlama hakkında bir adım adım öğretici.
author: karann-msft
ms.author: karann
ms.date: 08/16/2019
ms.topic: quickstart
ms.openlocfilehash: 9552f6c5291f950430bfb723cb713bf76a79ea66
ms.sourcegitcommit: 80cf99f40759911324468be1ec815c96aebf376d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/17/2019
ms.locfileid: "69564601"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a>Hızlı Başlangıç: Visual Studio (.NET Standard, yalnızca Windows) kullanarak bir NuGet paketi oluşturma ve yayımlama

Windows üzerinde Visual Studio 'da bir .NET Standard sınıf kitaplığından bir NuGet paketi oluşturmak ve ardından CLı aracını kullanarak nuget.org 'de yayımlamak basit bir işlemdir.

> [!Note]
> Mac için Visual Studio kullanıyorsanız, bir NuGet paketi oluşturma konusunda [Bu bilgilere](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) bakın veya [DotNet CLI araçlarını](create-and-publish-a-package-using-the-dotnet-cli.md)kullanın.

## <a name="prerequisites"></a>Önkoşullar

1. .NET Core ile ilgili iş yüküyle [VisualStudio.com](https://www.visualstudio.com/) adresinden herhangi bir Visual Studio 2019 sürümünü yükleyin.

1. Zaten yüklü değilse, `dotnet` CLI 'yı yükleme.

   CLI için, Visual Studio 2017 ' den başlayarak `dotnet` , CLI, .NET Core ile ilgili tüm iş yükleri ile otomatik olarak yüklenir. `dotnet` Aksi takdirde, `dotnet` CLI 'yı almak için [.NET Core SDK](https://www.microsoft.com/net/download/) ' yi yüklemelisiniz. CLI `dotnet` , [SDK stili biçimini](../resources/check-project-format.md) kullanan .NET Standard projeleri için gereklidir (SDK özniteliği). Visual Studio 2017 ve üzeri sürümlerde bulunan varsayılan .NET Standard sınıf kitaplığı şablonu, bu makalede kullanılan SDK özniteliğini kullanır.
   
   > [!Important]
   > SDK olmayan bir proje ile çalışıyorsanız, bunun yerine paketi oluşturmak ve yayımlamak için [.NET Framework paketi oluşturma ve yayımlama (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) konusundaki yordamları izleyin. Bu makalede, `dotnet` CLI önerilir. `nuget.exe` CLI kullanarak herhangi bir NuGet paketini yayımlayabilseniz de, bu makaledeki adımların bazıları SDK stilindeki projelere ve DotNet CLI 'ya özeldir. NuGet. exe CLı, [SDK olmayan-stil projeleri](../resources/check-project-format.md) için kullanılır (genellikle .NET Framework).

1. Henüz bir [hesabınız yoksa NuGet.org üzerinde ücretsiz bir hesaba kaydolun](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account) . Yeni hesap oluşturma onay e-postası gönderir. Bir paketi karşıya yükleyebilmek için önce hesabı onaylamanız gerekir.

## <a name="create-a-class-library-project"></a>Sınıf kitaplığı projesi oluşturma

Paketlemek istediğiniz kod için mevcut bir .NET Standard Sınıf Kitaplığı projesini kullanabilir veya basit bir tane oluşturabilirsiniz:

1. Visual Studio 'da **dosya > yeni > proje**' yi seçin, **Visual C# > .NET Standard** düğümünü genişletin, "sınıf kitaplığı (.NET Standard)" şablonunu seçin, projeyi appgünlükçü olarak adlandırın ve **Tamam**' a tıklayın.

   > [!Tip]
   > Aksi takdirde seçim yapmanız gerekmediğiniz sürece, en geniş kapsamlı proje yelpazğuyla uyumluluk sağladığından NuGet paketleri için tercih edilen hedef .NET Standard.

1. Ortaya çıkan proje dosyasına sağ tıklayın ve projenin düzgün oluşturulduğundan emin olmak için **Oluştur** ' u seçin. DLL, hata ayıklama klasöründe bulunur (veya bunun yerine bu yapılandırmayı oluşturursanız sürüm).

Gerçek bir NuGet paketi içinde, diğerlerinin uygulama derleyebileceği birçok yararlı özelliği uygulayacağınızı görürsünüz. Ancak bu izlenecek yol için, şablondan bir sınıf kitaplığı bir paket oluşturmak için yeterli olduğundan ek kod yazmayacaktır. Hala, paket için bir işlev kodu isterseniz, aşağıdakileri kullanın:

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

## <a name="configure-package-properties"></a>Paket özelliklerini yapılandırma

1. Çözüm Gezgini ' de projeye sağ tıklayın, **Özellikler** menü komutu ' nı ve ardından **paket** sekmesini seçin.

   **Paket** sekmesi yalnızca Visual STUDIO 'da SDK stilindeki projeler için, genellikle .NET Standard veya .NET Core sınıf kitaplığı projelerinde görünür; SDK olmayan bir stil projesini hedefliyorsanız (genellikle .NET Framework), [projeyi geçirin](../consume-packages/migrate-packages-config-to-package-reference.md) ya da adım adım yönergeler için [bir .NET Framework paketi oluşturma ve yayımlama](create-and-publish-a-package-using-visual-studio-net-framework.md) konusuna bakın.

    ![Visual Studio projesindeki NuGet paket özellikleri](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > Genel tüketim için oluşturulmuş paketler için Etiketler özelliğine özel dikkat edin, Etiketler başkalarının paketinizi bulmasına ve ne yaptığını anlamasına yardımcı olur.

1. Paketinize benzersiz bir tanımlayıcı verin ve istediğiniz diğer özellikleri doldurun. MSBuild özelliklerinin (SDK stili proje) bir *. nuspec*içindeki özelliklere eşlenmesi için bkz. [paket hedefleri](../reference/msbuild-targets.md#pack-target). Özelliklerinin açıklamaları için bkz [. nuspec dosya başvurusu](../reference/nuspec.md). Buradaki tüm özellikler, Visual Studio 'nun proje `.nuspec` için oluşturduğu bildirime gider.

    > [!Important]
    > Pakete, nuget.org genelinde veya kullandığınız herhangi bir konakta benzersiz bir tanımlayıcı vermeniz gerekir. Bu izlenecek yol için, "örnek" veya "test" adını, sonraki yayımlama adımı, paketi herkese açık hale getirir (ancak gerçekten onu kullanacağından çok fazla olabilir).
    >
    > Zaten var olan bir ada sahip bir paketi yayımlamayı denerseniz, bir hata görürsünüz.

1. Seçim Doğrudan proje dosyasında özellikleri görmek için Çözüm Gezgini içinde projeye sağ tıklayın ve **Appgünlükçü. csproj öğesini Düzenle**' yi seçin.

   Bu seçenek yalnızca SDK stili özniteliği kullanan projeler için Visual Studio 2017 ' den itibaren kullanılabilir. Aksi takdirde, projeye sağ tıklayın ve **Projeyi Kaldır**' ı seçin. Ardından, kaldırılan projeye sağ tıklayın ve **Appgünlükçü. csproj öğesini Düzenle**' yi seçin.

## <a name="run-the-pack-command"></a>Pack komutunu çalıştırın

1. Yapılandırmayı **serbest**olarak ayarlayın.

1. **Çözüm Gezgini** projeye sağ tıklayın ve ardından **paket** komutunu seçin:

    ![Visual Studio proje bağlam menüsünde NuGet paketi komutu](media/qs_create-vs-02-pack-command.png)

    **Paket** komutunu görmüyorsanız, projeniz muhtemelen bir SDK stili proje değildir ve `nuget.exe` CLI kullanmanız gerekir. [Projeyi geçirin](../consume-packages/migrate-packages-config-to-package-reference.md) ve CLI kullanın `dotnet` ya da adım adım yönergeler için [.NET Framework paketi oluşturma ve yayımlama](create-and-publish-a-package-using-visual-studio-net-framework.md) konusuna bakın.

1. Visual Studio projeyi oluşturur ve `.nupkg` dosyayı oluşturur. Paket dosyasının yolunu içeren ayrıntılar için **Çıkış** penceresini inceleyin (aşağıdakine benzer). Ayrıca, derlenmiş derlemenin `bin\Release\netstandard2.0` .NET Standard 2,0 hedefine uygun olduğunu unutmayın.

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="optional-generate-package-on-build"></a>Seçim Derleme üzerinde paket oluştur

Visual Studio 'Yu, projeyi oluşturduğunuzda NuGet paketini otomatik olarak oluşturacak şekilde yapılandırabilirsiniz.

1. Çözüm Gezgini'nde projeye sağ tıklayıp seçin **özellikleri**.

2. **Paket** sekmesinde **derlemede NuGet paketi oluştur**' u seçin.

   ![Derleme üzerinde otomatik olarak paket oluştur](media/qs_create-vs-05-generate-on-build.png)

> [!NOTE]
> Paketi otomatik olarak oluşturduğunuzda, paketlenecek süre projenizin derleme süresini arttırır.

### <a name="optional-pack-with-msbuild"></a>MSBuild ile (isteğe bağlı) paket

**Paket** menü komutunun kullanılmasına alternatif olarak, NuGet 4. x + ve MSBuild 15.1 +, proje gerekli paket verilerini `pack` içerdiğinde bir hedefi destekler. Bir komut istemi açın, proje klasörünüze gidin ve aşağıdaki komutu çalıştırın. (MSBuild için gereken tüm yollarla yapılandırıldıklarında, genellikle başlangıç menüsünden "Visual Studio için Geliştirici Komut İstemi" başlatmak istersiniz.)

Daha fazla bilgi için bkz. [MSBuild kullanarak paket oluşturma](../create-packages/creating-a-package-msbuild.md).

## <a name="publish-the-package"></a>Paketi Yayımla

Bir `.nupkg` dosyaya sahip olduktan sonra, NuGet.org ' den alınan bir API anahtarı ile `nuget.exe` birlikte CLI veya `dotnet.exe` CLI kullanarak NuGet.org 'de yayımlayın.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>API anahtarınızı alın

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-the-dotnet-cli-or-nugetexe-cli"></a>DotNet CLı veya NuGet. exe CLı ile yayımlama

CLı aracınız için **.NET Core CLI** (DotNet CLI) veya **NuGet** (NuGet. exe CLI) sekmesini seçin.

# <a name="net-core-clitabnetcore-cli"></a>[.NET Core CLI](#tab/netcore-cli)

Bu adım, kullanmanın `nuget.exe`önerilen alternatifi.

Paketi yayımlayabilmeniz için önce bir komut satırı açmanız gerekir.

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

# <a name="nugettabnuget"></a>[NuGet](#tab/nuget)

Bu adım, kullanmanın `dotnet.exe`bir alternatifidir.

1. Bir komut satırı açın ve `.nupkg` dosyayı içeren klasöre geçin.

1. Aşağıdaki komutu çalıştırarak paket adınızı (benzersiz paket KIMLIĞI) belirtip anahtar değerini API anahtarınızla değiştirin:

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. NuGet. exe yayımlama işleminin sonuçlarını görüntüler:

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

Bkz. [NuGet Push](../reference/cli-reference/cli-ref-push.md).

---

### <a name="publish-errors"></a>Yayımlama hataları

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Yayınlanan paketi yönetme

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a>Benioku dosyası ve diğer dosyalar ekleme

Pakete dahil edilecek dosyaları doğrudan belirtmek için, proje dosyasını düzenleyin ve `content` özelliğini kullanın:

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

Bu, paket kökünde adlı `readme.txt` bir dosya içerir. Visual Studio, paketi doğrudan yükledikten hemen sonra bu dosyanın içeriğini düz metin olarak görüntüler. (Benioku dosyaları, bağımlılıklar olarak yüklenen paketler için gösterilmez). Örneğin, HtmlAgilityPack paketinin Benioku dosyası şöyle görünür:

![Yükleme sonrasında bir NuGet paketi için Benioku dosyası görüntüleme](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> Yalnızca proje kökündeki Readme. txt ' i eklemek, sonuçta elde edilen pakete eklenmeyecektir.

## <a name="related-topics"></a>İlgili konular

- [Paket oluşturma](../create-packages/creating-a-package-dotnet-cli.md)
- [Paket Yayımlama](../nuget-org/publish-a-package.md)
- [Yayın öncesi paketler](../create-packages/Prerelease-Packages.md)
- [Birden çok hedef çerçeveyi destekleme](../create-packages/multiple-target-frameworks-project-file.md)
- [Paket sürümü oluşturma](../concepts/package-versioning.md)
- [Yerelleştirilmiş paketler oluşturma](../create-packages/creating-localized-packages.md)
- [.NET Standard kitaplığı belgeleri](/dotnet/articles/standard/library)
- [.NET Framework .NET Core 'a taşıma](/dotnet/articles/core/porting/index)
