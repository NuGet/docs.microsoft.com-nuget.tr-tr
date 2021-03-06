---
title: Visual Studio 'da bir NuGet paketi yükleyip kullanma
description: Visual Studio projesindeki bir NuGet paketini yükleme ve kullanma işleminde izlenecek yol.
author: JonDouglas
ms.author: jodou
ms.date: 07/24/2018
ms.topic: quickstart
ms.openlocfilehash: 55f6a64d90ce8ca628d1ac5c68f8133872a214e0
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775522"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-windows-only"></a>Hızlı başlangıç: Visual Studio 'da paket yükleyip kullanma (yalnızca Windows)

NuGet paketleri, diğer geliştiricilerin projelerinizde kullanabileceğiniz bir yeniden kullanılabilir kod içerir. Arka plan için bkz. [NuGet nedir?](../What-is-NuGet.md) . Paketler, NuGet Paket Yöneticisi, [Paket Yöneticisi konsolu](../consume-packages/install-use-packages-powershell.md)veya [DotNet CLI](install-and-use-a-package-using-the-dotnet-cli.md)kullanılarak Visual Studio projesine yüklenir. Bu makalede, popüler [Newtonsoft.Js](https://www.nuget.org/packages/Newtonsoft.Json/) paketini ve bir WINDOWS PRESENTATION FOUNDATION (WPF) projesini kullanan işlem gösterilmektedir. Aynı işlem, diğer tüm .NET veya .NET Core projeleri için de geçerlidir.

Yüklendikten sonra, `using <namespace>` kullandığınız pakete özgü olan koddaki pakete bakın \<namespace\> . Başvuru yapıldıktan sonra, paketini API 'SI aracılığıyla çağırabilirsiniz.

> [!Tip]
> **NuGet.org Ile başlayın**: gözatma *NuGet.org* , .NET geliştiricilerinin kendi uygulamalarında yeniden kullanabilecekleri bileşenleri genellikle nasıl buldukları. Bu makalede gösterildiği gibi, *NuGet.org* doğrudan arayabilir veya Visual Studio içinde paketleri bulabilir ve yükleyebilirsiniz. Genel bilgi için bkz. [NuGet paketlerini bulma ve değerlendirme](../consume-packages/finding-and-choosing-packages.md).

## <a name="prerequisites"></a>Ön koşullar

- .NET masaüstü geliştirme iş yüküyle Visual Studio 2019.

2019 Community Edition 'ı [VisualStudio.com](https://www.visualstudio.com/) adresinden ücretsiz olarak yükleyebilir veya profesyonel ya da Enterprise sürümlerini kullanabilirsiniz.

Mac için Visual Studio kullanıyorsanız, bkz. [Mac için Visual Studio bir paketi yükleyip kullanma](install-and-use-a-package-in-visual-studio-mac.md).

## <a name="create-a-project"></a>Proje oluşturma

NuGet paketleri, paketin proje ile aynı hedef Framework 'ü desteklemesi kaydıyla herhangi bir .NET projesine yüklenebilir.

Bu izlenecek yol için basit bir WPF uygulaması kullanın. Visual Studio 'da **Dosya**  >  **Yeni proje**' yi kullanarak bir proje oluşturun, arama kutusuna **.net** yazın ve ardından **WPF uygulamasını (.NET Framework)** seçin. **İleri**’ye tıklayın. İstendiğinde **Framework** için varsayılan değerleri kabul edin.

Visual Studio, Çözüm Gezgini ' de açılan projeyi oluşturur.

## <a name="add-the-newtonsoftjson-nuget-package"></a>NuGet paketine Newtonsoft.Jsekleyin

Paketi yüklemek için, NuGet Paket Yöneticisi 'Ni ya da Paket Yöneticisi konsolunu kullanabilirsiniz. Bir paket yüklediğinizde, NuGet, proje dosyanıza ya da bir `packages.config` dosyaya (proje biçimine bağlı olarak) bağımlılığı kaydeder. Daha fazla bilgi için bkz. [paket tüketimine genel bakış ve iş akışı](../consume-packages/Overview-and-Workflow.md).

### <a name="nuget-package-manager"></a>NuGet Paket Yöneticisi

1. Çözüm Gezgini ' de, **Başvurular** ' a sağ tıklayın ve **NuGet Paketlerini Yönet**' i seçin.

    ![Proje başvuruları için NuGet Paketlerini Yönet komutu](media/QS_Use-02-ManageNuGetPackages.png)

1. **Paket kaynağı** olarak "NuGet.org" öğesini seçin, **Gözden** geçirme sekmesini seçin, **üzerindeNewtonsoft.Js** arayın, listeden bu paketi seçin ve **yüklemeyi** seçin:

    ![Newtonsoft.Jspakette bulunuyor](media/QS_Use-03-NewtonsoftJson.png)

    NuGet Paket Yöneticisi hakkında daha fazla bilgi edinmek istiyorsanız bkz. [Visual Studio kullanarak paketleri yükleyip yönetme](../consume-packages/install-use-packages-visual-studio.md).

1. Tüm lisans istemlerini kabul edin.

1. (Yalnızca Visual Studio 2017) Paket Yönetimi biçimi seçmek isteyip istemediğiniz sorulursa **Proje dosyasında Packagereference** öğesini seçin:

    ![Paket yönetim biçimi seçme](media/QS_Use-03b-SelectFormat.png)

1. Değişiklikleri gözden geçirmeniz istenirse **Tamam**' ı seçin.

### <a name="package-manager-console"></a>Paket Yöneticisi Konsolu

1. **Araçlar**  >  **NuGet Paket Yöneticisi**  >  **Paket Yöneticisi konsolu** menü komutunu seçin.

1. Konsol açıldıktan sonra, **varsayılan proje** açılan listesinin paketi yüklemek istediğiniz projeyi gösterdiğini kontrol edin. Çözümde tek bir projeniz varsa, zaten seçilidir.

    ![Paket için bir proje seçin](media/QS_Use-08-Console1.png)

1. Komutu girin `Install-Package Newtonsoft.Json` (bkz. [Install-Package](../reference/ps-reference/ps-ref-install-package.md)). Konsol penceresinde komutun çıktısı gösterilir. Hatalar genellikle paketin projenin hedef çerçevesiyle uyumlu olmadığını gösterir.

   Paket Yöneticisi Konsolu hakkında daha fazla bilgi edinmek istiyorsanız bkz. [Paket Yöneticisi konsolu kullanılarak paketleri yükleyip yönetme](../consume-packages/install-use-packages-powershell.md).

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Uygulamadaki API Newtonsoft.Jskullanın

Projedeki Newtonsoft.Jspakette, `JsonConvert.SerializeObject` bir nesneyi insan tarafından okunabilen bir dizeye dönüştürmek için yöntemini çağırabilirsiniz.

1. `MainWindow.xaml`Öğesini açın ve var olan `Grid` öğeyi şu şekilde değiştirin:

    ```xaml
    <Grid Background="White">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Width="100px" HorizontalAlignment="Center" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" HorizontalAlignment="Center" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. Dosyasını açın `MainWindow.xaml.cs` (düğüm altında Çözüm Gezgini bulunur `MainWindow.xaml` ) ve aşağıdaki kodu `MainWindow` sınıfına ekleyin:

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

1. Newtonsoft.Jspakete eklenmiş olsa da, `JsonConvert` `using` kod dosyasının en üstünde bir ifadeye ihtiyacınız olduğu için kırmızı dalgalı çizgiler altında görünür:

    ```cs
    using Newtonsoft.Json;
    ```

1. F5 tuşuna basarak **veya hata ayıklama**  >  **başlatma hata ayıklamayı** seçerek uygulamayı derleyin ve çalıştırın:

    ![WPF uygulamasının ilk çıkışı](media/QS_Use-06-AppStart.png)

1. Bir JSON metniyle değiştirilmiş olan TextBlock içeriğini görmek için düğmeyi seçin:

    ![Düğmeyi seçtikten sonra WPF uygulamasının çıkışı](media/QS_Use-07-AppEnd.png)

## <a name="related-video"></a>İlgili video

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-Visual-Studio-2-of-5/player]

[Channel 9](https://channel9.msdn.com/Series/NuGet-101) ve [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_)'da daha fazla NuGet videoları bulun.

## <a name="next-steps"></a>Sonraki adımlar

İlk NuGet paketinizi yükleme ve kullanma hakkında Tebrikler!

> [!div class="nextstepaction"]
> [Visual Studio kullanarak paketleri yükleyip yönetme](../consume-packages/install-use-packages-visual-studio.md)

> [!div class="nextstepaction"]
> [Paket Yöneticisi konsolu 'Nu kullanarak paket yükleyip yönetme](../consume-packages/install-use-packages-powershell.md)

NuGet 'in sunabileceği daha fazlasını araştırmak için aşağıdaki bağlantıları seçin.

- [Paket tüketiminin genel bakış ve iş akışı](../consume-packages/overview-and-workflow.md)
- [Paketleri bulma ve seçme](../consume-packages/finding-and-choosing-packages.md)
- [Proje dosyalarında paket başvuruları](../consume-packages/package-references-in-project-files.md)
