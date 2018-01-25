---
title: "NuGet paketlerini kullanarak tanıtım Kılavuzu | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/04/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Yükleme ve bir NuGet paketi projede kullanma sürecini bir gözden geçirme öğretici."
keywords: "NuGet paketlerini kullanarak NuGet paketleri, NuGet paket referanslarını yükleme NuGet, NuGet paketi tüketim yükleyin"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 897419d1e49f12d54fbb996a2462e06e32933e65
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2018
---
# <a name="install-and-use-a-package"></a>Yükleme ve bir paket kullanma

NuGet paketleri diğer geliştiriciler projelerinizi kullanmak için kullanılabilir hale yeniden kullanılabilir kod birimleridir. Bkz: [NuGet nedir?](../What-is-NuGet.md) arka planı için.

[!INCLUDE [install-methods](../includes/install-methods.md)]

Koduyla paketinde yüklendikten sonra başvurmak `using <namespace>` nerede \<ad alanı\> kullanmakta olduğunuz paket özeldir. Başvuru yapıldığında, kendi API aracılığıyla paket çağırabilirsiniz.

Bu konunun geri kalanında popüler yüklemek için Paket Yöneticisi kullanıcı arabirimini kullanarak sürecinde yardımcı olur [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) bir evrensel Windows Platformu (UWP) proje paketinde. Ardından, paketi kullanarak bir örnek gösterilmektedir. Benzer bir iş akışı için diğer NuGet paketlerini kullanın.

- [Önkoşulları yüklemek](#install-pre-requisites)
- [Proje oluşturma](#create-a-project)
- [Newtonsoft.Json NuGet paketi ekleme](#add-the-newtonsoftjson-nuget-package)
- [' % S ' Newtonsoft.Json API uygulamasında kullanma](#use-the-newtonsoftjson-api-in-the-app)

> [!Tip]
> **Başlat nuget.org ile**: nuget.org paket yükleme olan kendi uygulamalarında kullanabilecekleri bileşenleri bulmak için .NET geliştiricilerinin kullanan ortak bir iş akışı. Her zaman nuget.org doğrudan arama ya da bulmak ve bu konu başlığı altında gösterildiği gibi Visual Studio içindeki paketleri yükleyin.

## <a name="install-pre-requisites"></a>Önkoşulları yüklemek

Bu öğretici araçları ile Visual Studio 2015 güncelleştirme 3, Evrensel Windows uygulamaları ya da Visual Studio 2017 için evrensel Windows platformu geliştirme yüküyle gerektirir. Visual Studio zaten yüklüyse, UWP araçları tekrar eklemeyi yükleyici çalıştırabilirsiniz.

Community edition ücretsiz nden yüklenebilecek [visualstudio.com](https://www.visualstudio.com/) ya da Professional veya Enterprise sürümü kullanın. 

## <a name="create-a-project"></a>Proje oluşturma

Bir NuGet paketi yüklemek için bazı tür gerekir. Visual Studio'da NET tabanlı projesi. Bu kılavuz için kullanabileceğiniz basit bir Windows Presentation Foundation (WPF) veya evrensel Windows (UWP) uygulamasını kullanın:

- WPF (Windows 7 +) seçin **Dosya > Yeni > Proje**, genişletin **Visual C#**seçin **Windows Klasik Masaüstü > WPF uygulaması (.NET Framework)**, seçip**Tamam**.
- UWP (Windows 10) kullanma **Windows Evrensel > boş uygulama (Evrensel Windows)** yerine. Hedef sürüm ve Minimum istendiğinde sürüm için varsayılan değerleri kabul.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Newtonsoft.Json NuGet paketi ekleme

1. Çözüm Gezgini'nde sağ **başvuruları** ve **NuGet paketlerini Yönet**.

    ![NuGet paketlerini komutu için proje başvuruları yönetme](media/QS_Use-02-ManageNuGetPackages.png)

1. "Nuget.org" olarak seçin **paket kaynağı**seçin **Gözat** sekmesinde, arama **Newtonsoft.Json**, listesinde o paketi seçin ve seçin  **Yükleme**:

    ![Newtonsoft.Json paket bulma](media/QS_Use-03-NewtonsoftJson.png)

1. Paket Yönetimi biçimi seçin isteyip istemediğiniz sorulduğunda (önerilen) PackageReference arasında seçin ve `packages.config`:

    ![Bir paket başvuru biçimi seçme](media/QS_Use-03b-SelectFormat.png)

1. Değişiklikleri gözden geçirmek için istenirse seçin **Tamam**.

1. Çözüm Gezgini'ndeki çözüme sağ tıklayın ve **yapı çözümü**. Bu altında listelenen herhangi bir NuGet paketinin geri yükler **başvurular**. Daha fazla ayrıntı için bkz: [paketi geri yüklemesi](../consume-packages/package-restore.md).

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>' % S ' Newtonsoft.Json API uygulamasında kullanma

Projedeki Newtonsoft.Json paketiyle çağırabilirsiniz kendi `JsonConvert.SerializeObject` bir nesne okunabilir bir dizeye dönüştürmek için yöntem.

1. Açık `MainWindow.xaml` (WPF) veya `MainPage.xaml` (UWP) ve varolan `Grid` aşağıdaki öğeyle:

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. Genişletme `MainWindow.xaml` (WPF) veya `MainPage.xaml` Çözüm Gezgini'nde Aç (UWP) düğüm `.cs` dosya ve aşağıdaki kodu ekleyin `MainWindow` veya `MainPage` Oluşturucusu sonra sınıfı:

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

1. Newtonsoft.Json paketini projeye eklenen olsa da, kırmızı dalgalı çizgiler altında görünür `JsonConvert` , gerektiğinden bir `using` deyimi. Altı çizili getirin `JsonConvert` ampul ve seçeneğini görürsünüz **olası düzeltmeleri göster**:

    ![Ampul Göster olası ile komut giderir](media/QS_Use-04-ShowPotentialFixes.png)


1. Tıklayın **olası düzeltmeleri göster** (veya ampul) ve ilk önerilen düzeltmeyi seçin `using Newtonsoft.Json;`. Bu gerekli satır dosyanın üst kısmına ekler.

    ![Kullanarak bir eklemek için seçeneği vermiş ampul deyimi](media/QS_Use-05-AddUsing.png)

1. Derleme ve F5 tuşuna basarak veya seçerek uygulamayı çalıştırma **hata ayıklama > hata ayıklamayı Başlat** (UWP burada; gösterilen WPF benzer):

    ![UWP uygulaması ilk çıktısı](media/QS_Use-06-AppStart.png)

1. İle bazı JSON metnin yerine TextBlock içeriğini görmek için düğmeyi seçin:

    ![Düğme seçtikten sonra UWP uygulamasında çıktısı](media/QS_Use-07-AppEnd.png)

## <a name="related-topics"></a>İlgili konular

- [Genel bakış ve iş akışı paket tüketimi](../consume-packages/overview-and-workflow.md)
- [Bulma ve paketleri seçme](../consume-packages/finding-and-choosing-packages.md)
- [NuGet Davranışını Yapılandırma](../consume-packages/configuring-nuget-behavior.md)
