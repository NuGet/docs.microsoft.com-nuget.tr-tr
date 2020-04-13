---
title: Visual Studio'da NuGet paketi yükleyin ve kullanın
description: Visual Studio projesinde nuget paketini yükleme ve kullanma süreci hakkında bir iz geçidi öğreticisi.
author: karann-msft
ms.author: karann
ms.date: 07/24/2018
ms.topic: quickstart
ms.openlocfilehash: 10bc34653d294cf70b5c91ce79a79cf6532fba1b
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "80147493"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-windows-only"></a>Quickstart: Visual Studio'da bir paket yükleyin ve kullanın (yalnızca Windows)

NuGet paketleri, diğer geliştiricilerin projelerinizde kullanmak üzere kullanabileceğiniz yeniden kullanılabilir kodlar içerir. NuGet [nedir?](../What-is-NuGet.md) Paketler NuGet Paket Yöneticisi, [Paket Yöneticisi Konsolu](../consume-packages/install-use-packages-powershell)veya [dotnet CLI](install-and-use-a-package-using-the-dotnet-cli.md)kullanılarak Visual Studio projesine yüklenir. Bu makale, popüler [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) paketi ve Bir Windows Sunum Vakfı (WPF) projesini kullanarak süreci göstermektedir. Aynı işlem diğer .NET veya .NET Core projesi için de geçerlidir.

Yüklendikten sonra, ad alanının `using <namespace>` \<\> kullanmakta olduğunuz pakete özgü olduğu koddaki pakete bakın. Başvuru yapıldıktan sonra, paketi API'si aracılığıyla arayabilirsiniz.

> [!Tip]
> **nuget.org ile başlayın**: nuget.org göz *atma* ,NET geliştiricilerin genellikle kendi uygulamalarında yeniden kullanabilecekleri bileşenleri nasıl bulduklarıdır. Bu makalede gösterildiği gibi *doğrudan nuget.org* arayabilir veya Visual Studio'daki paketleri bulabilir ve yükleyebilirsiniz. Genel bilgi için [NuGet paketlerini bul ve değerlendirin.](../consume-packages/finding-and-choosing-packages.md)

## <a name="prerequisites"></a>Ön koşullar

- .NET Masaüstü Geliştirme iş yükü ile Visual Studio 2019.

2019 Topluluk sürümünü [visualstudio.com](https://www.visualstudio.com/) ücretsiz olarak yükleyebilir veya Professional veya Enterprise sürümlerini kullanabilirsiniz.

Mac için Visual Studio kullanıyorsanız, Visual Studio for Mac için [bir paket yükleyin ve kullanın.](install-and-use-a-package-in-visual-studio-mac.md)

## <a name="create-a-project"></a>Proje oluşturma

NuGet paketleri, paketin projeyle aynı hedef çerçeveyi desteklemesi koşuluyla herhangi bir .NET projesine yüklenebilir.

Bu geçiş için basit bir WPF uygulaması kullanın. **Visual** > Studio'da Dosya**Yeni Projesi'ni**kullanarak bir proje oluşturun, arama kutusuna **.NET** yazarak ve ardından **WPF Uygulamasını (.NET Framework)** seçerek. **İleri**’ye tıklayın. İstendiğinde **Framework** için varsayılan değerleri kabul edin.

Visual Studio, Solution Explorer'da açılan projeyi oluşturur.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Newtonsoft.Json NuGet paketini ekleyin

Paketi yüklemek için NuGet Paket Yöneticisi'ni veya Paket Yöneticisi Konsolu'nu kullanabilirsiniz. Bir paket yüklediğinizde, NuGet bağımlılıkları proje dosyanıza `packages.config` veya dosyanızda kaydeder (proje biçimine bağlı olarak). Daha fazla bilgi için [bkz: Paket tüketimine genel bakış ve iş akışı.](../consume-packages/Overview-and-Workflow.md)

### <a name="nuget-package-manager"></a>NuGet Paket Yöneticisi

1. Çözüm Gezgini'nde, **Başvurular'a** sağ tıklayın ve **NuGet Paketlerini Yönet'i**seçin.

    ![Proje Başvuruları için NuGet Paketleri komutunu yönetme](media/QS_Use-02-ManageNuGetPackages.png)

1. **Paket kaynağı**olarak "nuget.org" seçeneğini belirleyin, **Gözat** sekmesini seçin, **Newtonsoft.Json'u**arayın, listedeki paketi seçin ve **Yükle'yi**seçin:

    ![Newtonsoft.Json paketinin bulunması](media/QS_Use-03-NewtonsoftJson.png)

    NuGet Paket Yöneticisi hakkında daha fazla bilgi istiyorsanız Visual [Studio'yu kullanarak paketleri yükle ve yönet'](../consume-packages/install-use-packages-visual-studio.md)e bakın.

1. Herhangi bir lisans istemlerini kabul edin.

1. (Sadece Visual Studio 2017) Paket yönetim biçimi seçmek istenirse, **proje dosyasında PackageReference'ı**seçin:

    ![Paket yönetim biçimi seçme](media/QS_Use-03b-SelectFormat.png)

1. Değişiklikleri gözden geçirmek istenirse, **Tamam'ı**seçin.

### <a name="package-manager-console"></a>Paket Yöneticisi Konsolu

1. **Araçlar** > **NuGet Paket Yöneticisi** > **Paket Yöneticisi Konsol** menü komutunu seçin.

1. Konsol açıldıktan sonra, **Varsayılan proje** açılır listesinin paketi yüklemek istediğiniz projeyi gösterip gösterdiğini denetleyin. Çözümde tek bir proje varsa, zaten seçilir.

    ![Newtonsoft.Json paketinin bulunması](media/QS_Use-08-Console1.png)

1. Komutu `Install-Package Newtonsoft.Json` girin (bkz. [Yükle-Paket](../reference/ps-reference/ps-ref-install-package.md)). Konsol penceresi komut için çıktı gösterir. Hatalar genellikle paketin projenin hedef çerçevesiyle uyumlu olmadığını gösterir.

   Paket Yöneticisi Konsolu hakkında daha fazla bilgi istiyorsanız, [Paket Yöneticisi Konsolu'nu kullanarak paketleri yükle ve yönet'](../consume-packages/install-use-packages-powershell.md)e bakın.

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Uygulamada Newtonsoft.Json API'yi kullanın

Projedeki Newtonsoft.Json paketi yle, bir `JsonConvert.SerializeObject` nesneyi insan tarafından okunabilir bir dize dönüştürme yöntemini arayabilirsiniz.

1. Varolan `MainWindow.xaml` `Grid` öğeyi aşağıdakilerle açın ve değiştirin:

    ```xaml
    <Grid Background="White">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Width="100px" HorizontalAlignment="Center" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" HorizontalAlignment="Center" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. Dosyayı `MainWindow.xaml.cs` açın (düğüm altında `MainWindow.xaml` Çözüm Gezgini'nde bulunan) ve `MainWindow` sınıfın içine aşağıdaki kodu ekleyin:

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }

    private void Button_Click(object sender, RoutedEventArgs e)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@microsoft.com",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };
        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        TextBlock.Text = json;
    }
    ```

1. Newtonsoft.Json paketini projeye eklemiş olsanız bile, kod dosyasının üst `using` kısmında bir ifadeye ihtiyacınız olduğundan kırmızı dalgalı lar altında `JsonConvert` görünür:

    ```cs
    using Newtonsoft.Json;
    ```

1. F5 tuşuna basarak veya **Hata Ayıklama** > **Başlatma Hata Ayıklama'yı**seçerek uygulamayı oluşturun ve çalıştırın:

    ![WPF uygulamasının ilk çıktısı](media/QS_Use-06-AppStart.png)

1. TextBlock'un içeriğinin bazı JSON metinleri ile değiştirilmesini görmek için düğmeyi seçin:

    ![Düğmeyi seçtikten sonra WPF uygulamasının çıktısı](media/QS_Use-07-AppEnd.png)

## <a name="related-video"></a>İlgili video

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-Visual-Studio-2-of-5/player]

[Kanal 9](https://channel9.msdn.com/Series/NuGet-101) ve [YouTube'da](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_)daha fazla NuGet videosu bulun.

## <a name="next-steps"></a>Sonraki adımlar

İlk NuGet paketinizi yükledikten ve kullandığınız için tebrikler!

> [!div class="nextstepaction"]
> [Visual Studio'u kullanarak paketleri yükleyin ve yönetin](../consume-packages/install-use-packages-visual-studio.md)

> [!div class="nextstepaction"]
> [Paket Yöneticisi Konsolu'nu kullanarak paketleri yükleme ve yönetme](../consume-packages/install-use-packages-powershell.md)

NuGet'in sunduğu daha fazlasını keşfetmek için aşağıdaki bağlantıları seçin.

- [Paket tüketimine genel bakış ve iş akışı](../consume-packages/overview-and-workflow.md)
- [Paketleri bulma ve seçme](../consume-packages/finding-and-choosing-packages.md)
- [Proje dosyalarında paket başvuruları](../consume-packages/package-references-in-project-files.md)
