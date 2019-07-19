---
title: Visual Studio içinden NuGet paketlerini kullanmaya yönelik tanıtım Kılavuzu
description: Visual Studio projesindeki bir NuGet paketini yükleme ve kullanma işleminde izlenecek yol.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: deedc251b605b5b58659d3b70e1ca01b19c72865
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317563"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio"></a>Hızlı Başlangıç: Visual Studio 'da paket yükleyip kullanma

NuGet paketleri, diğer geliştiricilerin projelerinizde kullanabileceğiniz bir yeniden kullanılabilir kod içerir. Arka plan için bkz. [NuGet nedir?](../What-is-NuGet.md) . Paketler bir Visual Studio projesine Paket Yöneticisi Kullanıcı arabirimi veya paket Yöneticisi konsolu kullanılarak yüklenir. Bu makalede, popüler [Newtonsoft. JSON](https://www.nuget.org/packages/Newtonsoft.Json/) paketini ve bir evrensel WINDOWS platformu (UWP) projesini kullanan işlem gösterilmektedir. Aynı işlem, diğer tüm .NET veya .NET Core projeleri için de geçerlidir.

Yüklendikten sonra, koddaki `using <namespace>` \<pakete, ad alanının\> kullandığınız pakete özgü olduğunu bakın. Başvuru yapıldıktan sonra, paketini API 'SI aracılığıyla çağırabilirsiniz.

> [!Tip]
> **NuGet.org Ile Başlat**: Nuget.org gözatma, .NET geliştiricilerinin kendi uygulamalarında yeniden kullanabilecekleri bileşenleri genellikle bulmasıdır. Bu makalede gösterildiği gibi, nuget.org doğrudan arayabilir veya Visual Studio içinde paketleri bulabilir ve yükleyebilirsiniz.

## <a name="prerequisites"></a>Önkoşullar

- Evrensel Windows Platformu geliştirme iş yüküyle Visual Studio 2017 veya
- Evrensel Windows uygulamaları için araçlar içeren Visual Studio 2015 güncelleştirme 3.

2017 Community Edition 'ı [VisualStudio.com](https://www.visualstudio.com/) adresinden ücretsiz olarak yükleyebilir veya profesyonel ya da Enterprise sürümlerini kullanabilirsiniz.

Mac için Visual Studio kullanıyorsanız, bkz. [projenize bir NuGet paketi ekleme](/visualstudio/mac/nuget-walkthrough).

## <a name="create-a-project"></a>Proje oluşturma

NuGet paketleri, paketin proje ile aynı hedef Framework 'ü desteklemesi kaydıyla herhangi bir .NET projesine yüklenebilir.

Bu izlenecek yol için basit bir Evrensel Windows (UWP) uygulaması kullanın. Visual Studio 'da **dosya > yeni proje...** öğesini kullanarak ve **Windows Evrensel > boş uygulamasını (Evrensel Windows)** seçerek bir proje oluşturun. İstendiğinde, hedef sürüm için varsayılan değerleri ve en düşük sürümü kabul edin.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Newtonsoft. JSON NuGet paketini ekleyin

Paketi yüklemek için Paket Yöneticisi Kullanıcı arabirimini ya da Paket Yöneticisi konsolunu kullanabilirsiniz. Bir paket yüklediğinizde NuGet, proje dosyanıza ya da bir `packages.config` dosyaya bağımlılığı kaydeder. Daha fazla bilgi için bkz. [paket tüketimine genel bakış ve iş akışı](../consume-packages/Overview-and-Workflow.md).

### <a name="package-manager-ui"></a>Paket Yöneticisi UI

1. Çözüm Gezgini ' de, **Başvurular** ' a sağ tıklayın ve **NuGet Paketlerini Yönet**' i seçin.

    ![Proje başvuruları için NuGet Paketlerini Yönet komutu](media/QS_Use-02-ManageNuGetPackages.png)

1. **Paket kaynağı**olarak "NuGet.org" öğesini seçin, **Gözden** geçirme sekmesini seçin, **Newtonsoft. JSON**' ı arayın, listeden bu paketi seçin ve sonra da **yüklemeyi**seçin:

    ![Newtonsoft. JSON paketi bulunuyor](media/QS_Use-03-NewtonsoftJson.png)

1. Tüm lisans istemlerini kabul edin.

1. (Visual Studio 2017) Paket Yönetimi biçimi seçmek isteyip istemediğiniz sorulursa **Proje dosyasında Packagereference**öğesini seçin:

    ![Paket yönetim biçimi seçme](media/QS_Use-03b-SelectFormat.png)

1. Değişiklikleri gözden geçirmeniz istenirse **Tamam**' ı seçin.

### <a name="package-manager-console"></a>Paket Yöneticisi Konsolu

1. **NuGet paket yöneticisi > Paket Yöneticisi konsolu menü komutunu > araçlar** ' ı seçin.

1. Konsol açıldıktan sonra, **varsayılan proje** açılan listesinin paketi yüklemek istediğiniz projeyi gösterdiğini kontrol edin. Çözümde tek bir projeniz varsa, zaten seçilidir.

    ![Newtonsoft. JSON paketi bulunuyor](media/QS_Use-08-Console1.png)

1. Komutu `Install-Package Newtonsoft.Json` girin (bkz. [Install-Package](../reference/ps-reference/ps-ref-install-package.md)). Konsol penceresinde komutun çıktısı gösterilir. Hatalar genellikle paketin projenin hedef çerçevesiyle uyumlu olmadığını gösterir.

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Uygulamada Newtonsoft. JSON API 'sini kullanma

Projedeki Newtonsoft. JSON paketiyle, bir nesneyi insan tarafından okunabilen bir dizeye dönüştürmek `JsonConvert.SerializeObject` için yöntemini çağırabilirsiniz.

1. Öğesini `MainPage.xaml` açın ve var olan `Grid` öğeyi şu şekilde değiştirin:

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. Dosyasını açın ( `MainPage.xaml` düğüm altında Çözüm Gezgini bulunur) ve aşağıdaki kodu `MainPage` oluşturucunun içine ekleyin: `MainPage.xaml.cs`

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

1. Newtonsoft. JSON paketini projeye ekleseniz de, kod dosyasının en üstünde bir `JsonConvert` `using` deyime ihtiyacınız olduğu için kırmızı dalgalı çizgiler altında görünür:

    ```cs
    using Newtonsoft.Json;
    ```

1. F5 tuşuna basarak veya **hata ayıklamayı başlatmak > hata ayıkla**' yı seçerek uygulamayı derleyin ve çalıştırın:

    ![UWP uygulamasının ilk çıkışı](media/QS_Use-06-AppStart.png)

1. Bir JSON metniyle değiştirilmiş olan TextBlock içeriğini görmek için düğmeyi seçin:

    ![Düğmeyi seçtikten sonra UWP uygulamasının çıkışı](media/QS_Use-07-AppEnd.png)

## <a name="related-articles"></a>İlgili makaleler

- [Paket tüketiminin genel bakış ve iş akışı](../consume-packages/overview-and-workflow.md)
- [Paketleri bulma ve seçme](../consume-packages/finding-and-choosing-packages.md)
- [Ortak NuGet yapılandırmaları](../consume-packages/configuring-nuget-behavior.md)
