---
title: Bir .NET Standart NuGet paketi oluşturun ve yayımlayın - Windows'ta Visual Studio
description: Windows'da Visual Studio'u kullanarak bir .NET Standart NuGet paketi oluşturma ve yayımlama konusunda bir iz geçidi öğretici.
author: karann-msft
ms.author: karann
ms.date: 08/16/2019
ms.topic: quickstart
ms.openlocfilehash: 32dcc1d233154463e2950b1ce46554b1cb89956e
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79429033"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a>Quickstart: Visual Studio 'yı kullanarak bir NuGet paketi oluşturun ve yayımlayın (.NET Standardı, yalnızca Windows)

Windows'daki Visual Studio'daki .NET Standart Sınıf Kitaplığı'ndan bir NuGet paketi oluşturmak ve ardından cli aracını kullanarak nuget.org yayınlamak basit bir işlemdir.

> [!Note]
> Mac için Visual Studio kullanıyorsanız, nuget paketi oluşturma yla ilgili [bu bilgilere](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) bakın veya [dotnet CLI araçlarını](create-and-publish-a-package-using-the-dotnet-cli.md)kullanın.

## <a name="prerequisites"></a>Ön koşullar

1. .NET Core ile ilgili iş yüküne [sahip visualstudio.com](https://www.visualstudio.com/) Visual Studio 2019'un herhangi bir sürümünü yükleyin.

1. Zaten yüklü değilse, CLI'yi `dotnet` yükleyin.

   `dotnet` Visual Studio 2017'den `dotnet` başlayarak CLI için ,NET Core ile ilgili iş yükleriyle otomatik olarak yüklenir. Aksi takdirde, CLI almak için `dotnet` [.NET Core SDK'yı](https://www.microsoft.com/net/download/) yükleyin. [CLI, SDK stili biçimini (SDK](../resources/check-project-format.md) özniteliği) kullanan .NET Standard projeleri için gereklidir. `dotnet` Visual Studio 2017 ve üzeri'nde bu makalede kullanılan varsayılan .NET Standart sınıf kitaplığı şablonu SDK özniteliğini kullanır.
   
   > [!Important]
   > SDK tarzı olmayan bir projeyle çalışıyorsanız, paketi oluşturmak ve yayınlamak için [bir .NET Framework paketi (Visual Studio) oluştur'daki](create-and-publish-a-package-using-visual-studio-net-framework.md) yordamları izleyin ve yayımlayın. Bu makale için `dotnet` CLI önerilir. `nuget.exe` CLI'yi kullanarak herhangi bir NuGet paketini yayımlayabilirsiniz, ancak bu makaledeki bazı adımlar SDK tarzı projelere ve dotnet CLI'ye özgüdür. nuget.exe CLI, [SDK tarzı olmayan projeler](../resources/check-project-format.md) için kullanılır (genellikle .NET Framework).

1. Zaten bir hesabınız yoksa [nuget.org ücretsiz bir hesaba kaydolun.](../nuget-org/individual-accounts.md#add-a-new-individual-account) Yeni bir hesap oluşturmak bir onay e-postası gönderir. Bir paket yükleyemeden önce hesabı onaylamanız gerekir.

## <a name="create-a-class-library-project"></a>Sınıf kitaplığı projesi oluşturma

Paketlemek istediğiniz kod için varolan bir .NET Standart Sınıf Kitaplığı projesini kullanabilir veya aşağıdaki gibi basit bir kitap oluşturabilirsiniz:

1. Visual **Studio'da, Yeni > Projesi > Dosya'yı**seçin, **Visual C# > .NET Standard** düğümünü genişletin, "Sınıf Kitaplığı (.NET Standart)" şablonuna tıklayın, proje AppLogger'ı adlandırın ve **Tamam'ı**tıklatın.

   > [!Tip]
   > Aksini seçmek için bir nedeniniz yoksa, .NET Standard, en geniş tüketici proje yelpazesiyle uyumluluk sağladığından NuGet paketleri için tercih edilen hedeftir.

1. Projenin düzgün oluşturulduğundan emin olmak için ortaya çıkan proje dosyasına sağ tıklayın ve **Yapı'yı** seçin. DLL Hata Ayıklama klasöründe bulunur (veya bu yapılandırmayı oluşturursanız serbest bırakın).

Gerçek bir NuGet paketi içinde, tabii ki, başkalarının uygulamaları oluşturabilirsiniz birçok yararlı özellikleri uygulamak. Ancak bu geçiş için, şablondan bir sınıf kitaplığı bir paket oluşturmak için yeterli olduğundan, ek kod yazmazsınız. Yine de, paket için bazı işlevsel kod istiyorsanız, aşağıdakileri kullanın:

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

1. Solution Explorer'da projeyi sağ tıklatın ve **Özellikler** menüsü komutunu seçin ve ardından **Paket** sekmesini seçin.

   **Paket** sekmesi yalnızca Visual Studio'daki SDK tarzı projeler için görünür, genellikle .NET Standardı veya .NET Core sınıf kitaplık projeleri; SDK tarzı olmayan bir projeyi (genellikle .NET Framework) hedefliyorsanız, [projeyi geçirin](../consume-packages/migrate-packages-config-to-package-reference.md) veya adım adım yönergeler yerine [bir .NET Framework paketi oluştur ve yayımlama](create-and-publish-a-package-using-visual-studio-net-framework.md) yı görün.

    ![Görsel Stüdyo projesinde NuGet paket özellikleri](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > Genel tüketim için oluşturulmuş paketler için, etiketler başkalarının paketinizi bulmasına ve ne işe yaradığına yardımcı olduğundan, **Etiketler** özelliğine özel olarak dikkat edin.

1. Paketinize benzersiz bir tanımlayıcı verin ve istediğiniz diğer özellikleri doldurun. MSBuild özelliklerinin (SDK stili proje) bir *.nuspec'teki*özelliklere eşlenemeiçin [paket hedeflerine](../reference/msbuild-targets.md#pack-target)bakın. Özelliklerin açıklamaları için [.nuspec dosya başvurusuna](../reference/nuspec.md)bakın. Buradaki tüm özellikler Visual `.nuspec` Studio'nun proje için oluşturduğu manifestoya gidiyor.

    > [!Important]
    > Pakete, nuget.org veya kullandığınız ana bilgisayarda benzersiz bir tanımlayıcı vermelisiniz. Bu izlenecek yol için, daha sonraki yayımlama adımı paketi herkese açık hale getirebildiğinden (kimsenin gerçekten kullanması pek olası olmasa da) adına "Örnek" veya "Test" eklenmesini öneririz.
    >
    > Zaten var olan bir ada sahip bir paketi yayımlamaya çalışırsanız, bir hata görürsünüz.

1. (İsteğe bağlı) Özellikleri doğrudan proje dosyasında görmek için Solution Explorer'da projeyi sağ tıklatın ve **AppLogger.csproj'u edit'i**seçin.

   Bu seçenek yalnızca Visual Studio 2017'den itibaren SDK stili özniteliği kullanan projeler için kullanılabilir. Aksi takdirde, projeyi sağ tıklatın ve **Project'i Boşalt'ı**seçin. Sonra sağ boşproje tıklayın ve **AppLogger.csproj edit**seçin.

## <a name="run-the-pack-command"></a>Sürü komutunu çalıştırın

1. Yapılandırmayı **Release**olarak ayarlayın.

1. **Solution Explorer'da** projeyi sağ tıklatın ve **Paket** komutunu seçin:

    ![Visual Studio proje bağlam menüsünde NuGet paketi komutu](media/qs_create-vs-02-pack-command.png)

    **Paket** komutunu görmüyorsanız, projeniz büyük olasılıkla SDK tarzı bir proje değildir `nuget.exe` ve CLI'yi kullanmanız gerekir. [Projeyi geçirin](../consume-packages/migrate-packages-config-to-package-reference.md) ve `dotnet` CLI'yi kullanın veya adım adım yönergeler yerine [bir .NET Framework paketi oluştur ve yayımla'ya](create-and-publish-a-package-using-visual-studio-net-framework.md) bakın.

1. Visual Studio projeyi oluşturur ve `.nupkg` dosyayı oluşturur. Paket dosyasına giden yolu içeren ayrıntılar (aşağıdakilere benzer) **Çıktı** penceresini inceleyin. Yapılı derlemenin .NET `bin\Release\netstandard2.0` Standart 2.0 hedefine yakışır şekilde olduğunu da unutmayın.

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="optional-generate-package-on-build"></a>(İsteğe bağlı) Yapı da paket oluşturma

Projeyi oluştururken Visual Studio'yu NuGet paketini otomatik olarak oluşturacak şekilde yapılandırabilirsiniz.

1. Çözüm Gezgini'nde projeyi sağ tıklatın ve **Özellikler'i**seçin.

2. **Paket** sekmesinde, **yapıda NuGet paketi**oluştur'u'nu seçin.

   ![Otomatik olarak yapı üzerinde paket oluşturmak](media/qs_create-vs-05-generate-on-build.png)

> [!NOTE]
> Paketi otomatik olarak oluşturduğunuzda, paketi hazırlama süresi projenizin oluşturma süresini artırır.

### <a name="optional-pack-with-msbuild"></a>MSBuild ile (İsteğe bağlı) paket

**Paket** menüsü komutunu kullanmaya alternatif olarak, NuGet 4.x+ ve MSBuild `pack` 15.1+ proje gerekli paket verilerini içerdiğinde bir hedefi destekler. Komut istemini açın, proje klasörünüze gidin ve aşağıdaki komutu çalıştırın. (MsBuild için gerekli tüm yollarla yapılandırılacak gibi, genellikle Başlat menüsünden "Visual Studio için Geliştirici Komut Komut Ustem"i başlatmak istersiniz.)

Daha fazla bilgi için [bkz.](../create-packages/creating-a-package-msbuild.md)

## <a name="publish-the-package"></a>Paketi yayımlama

Bir `.nupkg` dosyaya sahip olduktan sonra, nuget.org'dan edinilen bir API anahtarıyla birlikte `nuget.exe` CLI veya `dotnet.exe` CLI'yi kullanarak dosyayı nuget.org yayımlarsınız.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>API anahtarınızı edinin

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-the-dotnet-cli-or-nugetexe-cli"></a>dotnet CLI veya nuget.exe CLI ile yayımlayın

CLI aracınızın sekmesini seçin, **yani .NET Core CLI** (dotnet CLI) veya **NuGet** (nuget.exe CLI).

# <a name="net-core-cli"></a>[.NET Core CLI](#tab/netcore-cli)

Bu adım kullanarak `nuget.exe`önerilen bir alternatiftir.

Paketi yayımlamadan önce bir komut satırı açmanız gerekir.

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

# <a name="nuget"></a>[NuGet](#tab/nuget)

Bu adım kullanarak `dotnet.exe`bir alternatiftir.

1. Bir komut satırı açın ve dosyayı içeren klasöre değiştirin. `.nupkg`

1. Paket adınızı (benzersiz paket kimliğinizi) belirterek ve anahtar değerini API anahtarınızla değiştirerek aşağıdaki komutu çalıştırın:

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

---

### <a name="publish-errors"></a>Hataları yayımlama

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Yayımlanmış paketi yönetme

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a>Okuma meme ve diğer dosyalar ekleme

Pakete dahil olacak dosyaları doğrudan belirtmek için proje dosyasını edin ve `content` özelliği kullanın:

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

Bu, paket kökünde adlı `readme.txt` bir dosya içerir. Visual Studio, paketi doğrudan yükledikten hemen sonra dosyanın içeriğini düz metin olarak görüntüler. (Bağımlılık olarak yüklenen paketler için Okuma dosyaları görüntülenmez). Örneğin, HtmlAgilityPack paketinin okuma sı şu şekilde görünür:

![Yükleme üzerine NuGet paketi için okuma dosyasının görüntülenmesi](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> Proje köküne readme.txt eklenmesi, yalnızca ortaya çıkan pakete eklenmesine neden olmaz.

## <a name="related-video"></a>İlgili video

> [!Video https://channel9.msdn.com/Series/NuGet-101/Create-and-Publish-a-NuGet-Package-with-Visual-Studio-4-of-5/player]

[Kanal 9](https://channel9.msdn.com/Series/NuGet-101) ve [YouTube'da](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_)daha fazla NuGet videosu bulun.

## <a name="related-topics"></a>İlgili konular

- [Paket Oluşturma](../create-packages/creating-a-package-dotnet-cli.md)
- [Paket Yayınlama](../nuget-org/publish-a-package.md)
- [Ön Sürüm Paketleri](../create-packages/Prerelease-Packages.md)
- [Birden çok hedef çerçeveyi destekleme](../create-packages/multiple-target-frameworks-project-file.md)
- [Paket sürüm](../concepts/package-versioning.md)
- [Yerelleştirilmiş paketler oluşturma](../create-packages/creating-localized-packages.md)
- [.NET Standart Kütüphane belgeleri](/dotnet/articles/standard/library)
- [.NET Framework'den .NET Core'a taşıma](/dotnet/articles/core/porting/index)
