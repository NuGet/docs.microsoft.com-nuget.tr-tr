---
title: Visual Studio'da NuGet paketleri kullanmaya tanıtım Kılavuzu
description: Yükleme ve bir NuGet paketi kullanarak bir Visual Studio projesinde işlemini bir gözden geçirme öğretici.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: 7b30fce4a2d9ad0bd7bc2b97f69b8d5d25101b72
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545232"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio"></a>Hızlı Başlangıç: Yükleme ve Visual Studio'da paket kullanma

NuGet paketleri diğer geliştiriciler projelerinizde kullanmak için kullanılabilir hale yeniden kullanılabilir bir kod içerir. Bkz: [NuGet nedir?](../What-is-NuGet.md) arka planı. Paket Yöneticisi UI veya Paket Yöneticisi konsolunu kullanarak bir Visual Studio projesine paketleri yüklenir. Bu makalede, popüler kullanma işlemi gösterilmektedir. [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) paket ve evrensel Windows Platformu (UWP) projesi. Aynı işlem, diğer tüm .NET veya .NET Core projeleri için geçerlidir.

Kod ile paket yüklendikten sonra başvurmak `using <namespace>` burada \<ad alanı\> kullanmakta olduğunuz paket özgüdür. Başvuru yaptıktan sonra paketi API'si aracılığıyla çağırabilirsiniz.

> [!Tip]
> **Nuget.org ile Başlat**: gözatma nuget.org'nin olduğundan nasıl .NET geliştiricilerinin bileşenler genellikle bulun, kendi uygulamalarında yeniden kullanabilirsiniz. Nuget.org doğrudan arama veya bulabilir ve bu makalede gösterilen şekilde Visual Studio içindeki paketleri yükleyin.

## <a name="prerequisites"></a>Önkoşullar

- Evrensel Windows platformu geliştirme iş yüküyle Visual Studio 2017 veya
- Visual Studio 2015 güncelleştirme 3 ile Evrensel Windows uygulamaları için Araçlar.

2017 Community edition ücretsiz nden yüklenebilecek [visualstudio.com](https://www.visualstudio.com/) veya Professional veya Enterprise Edition'ı kullanın.

## <a name="create-a-project"></a>Proje oluşturma

Paket projesi olarak aynı hedef Framework'ü destekliyorsa, NuGet paketlerini herhangi bir .NET projesine yüklenebilir.

Bu kılavuz için basit bir evrensel Windows (UWP) uygulamasını kullanın. Visual Studio kullanarak bir proje oluşturun **Dosya > Yeni proje...**  seçerek **Windows Evrensel > boş uygulama (Evrensel Windows)**. Hedef sürümü ve en düşük istendiğinde sürümü için varsayılan değerleri kabul.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Newtonsoft.Json NuGet paketi ekleme

Paketi yüklemek için Paket Yöneticisi kullanıcı Arabirimi veya Paket Yöneticisi konsolu kullanabilirsiniz. Bir paketi yüklediğinizde, NuGet bağımlılık ya da proje dosyanız kaydeder veya `packages.config` dosya. Daha fazla bilgi için [paket tüketim genel bakış ve iş akışı](../consume-packages/Overview-and-Workflow.md).

### <a name="package-manager-ui"></a>Paket Yöneticisi UI

1. Çözüm Gezgini'nde sağ **başvuruları** ve **NuGet paketlerini Yönet**.

    ![NuGet paketlerini komutu için proje başvurularını yönetme](media/QS_Use-02-ManageNuGetPackages.png)

1. "Nuget.org" olarak seçin **paket kaynağı**seçin **Gözat** sekmesinde, arama **Newtonsoft.Json**, bu paket listesinde seçip  **Yükleme**:

    ![Newtonsoft.Json paketini bulma](media/QS_Use-03-NewtonsoftJson.png)

1. Herhangi bir lisans istemi kabul edin.

1. (Visual Studio 2017) Paket Yönetimi biçimi seçin istenirse seçin **packagereference v souboru projektu**:

    ![Paket Yönetimi biçimini seçme](media/QS_Use-03b-SelectFormat.png)

1. Değişiklikleri gözden geçirmek için istenirse seçin **Tamam**.

### <a name="package-manager-console"></a>Paket Yöneticisi Konsolu

1. Seçin **Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Konsolu** menü komutu.

1. Konsol açıldıktan sonra bu maddeyi **varsayılan proje** aşağı açılan listesinde istediğiniz paketi yüklemek projeyi gösterir. Tek bir proje çözümde varsa, bu zaten seçilir.

    ![Newtonsoft.Json paketini bulma](media/QS_Use-08-Console1.png)

1. Komutu girdikten `Install-Package Newtonsoft.json` (bkz [Install-Package](../tools/ps-ref-install-package.md)). Konsol penceresinde komutunun çıktısını gösterir. Hatalar genellikle paket projenin hedef çerçevesi ile uyumlu olmadığını gösterir.

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>' % S ' Newtonsoft.Json API uygulamasında kullanma

Projesinde Newtonsoft.Json paketiyle çağırabilirsiniz kendi `JsonConvert.SerializeObject` bir nesneyi bir kullanıcı tarafından okunabilen bir dizeye dönüştürmek için yöntemi.

1. Açık `MainPage.xaml` ve varolan `Grid` aşağıdaki öğe:

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. Açık `MainPage.xaml.cs` dosyası (altında Çözüm Gezgini'nde bulunan `MainPage.xaml` düğümü) ve içine aşağıdaki kodu ekleyin `MainPage` Oluşturucusu:

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

1. Newtonsoft.Json paketini projeye eklenen olsa da, kırmızı dalgalı çizgiler altında görünür `JsonConvert` ihtiyacınız olduğundan bir `using` kod dosyasının üst deyimi:

    ```cs
    using Newtonsoft.json;
    ```

1. F5 tuşuna basarak veya seçerek uygulaması derleyebilir ve **hata ayıklama > hata ayıklamayı Başlat**:

    ![UWP uygulamasının ilk çıkış](media/QS_Use-06-AppStart.png)

1. İle bazı JSON metnin yerine geçen TextBlock içeriğini görmek için düğmesini seçin:

    ![Çıkış düğmesi seçildikten sonra UWP uygulaması](media/QS_Use-07-AppEnd.png)

## <a name="related-articles"></a>İlgili makaleler

- [Genel bakış ve paket tüketim iş akışı](../consume-packages/overview-and-workflow.md)
- [Paketleri bulma ve seçme](../consume-packages/finding-and-choosing-packages.md)
- [Paket yükleme yolu](../consume-packages/ways-to-install-a-package.md)
- [NuGet Davranışını Yapılandırma](../consume-packages/configuring-nuget-behavior.md)
