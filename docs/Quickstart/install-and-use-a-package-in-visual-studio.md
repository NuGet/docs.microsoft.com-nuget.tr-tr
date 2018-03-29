---
title: Visual Studio içinde NuGet paketi kullanarak tanıtım Kılavuzu | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: quickstart
ms.prod: nuget
ms.technology: ''
description: İzlenecek yol öğretici yükleme ve bir NuGet paketi kullanarak bir Visual Studio projesi işleme.
keywords: NuGet paketlerini kullanarak NuGet paketleri, NuGet paket referanslarını yükleme NuGet, NuGet paketi tüketim yükleyin
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 4205893cc02cffff8926513a555393d10c046f43
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="install-and-use-a-package-in-visual-studio"></a>Yükleyin ve Visual Studio'da bir paket kullanın

NuGet paketleri diğer geliştiriciler projelerinizi kullanmak için kullanılabilir hale yeniden kullanılabilir kod içerir. Bkz: [NuGet nedir?](../What-is-NuGet.md) arka planı için. Paketler, Paket Yöneticisi kullanıcı Arabirimi veya Paket Yöneticisi konsolu kullanarak bir Visual Studio projesi yüklenir. Bu makalede, popüler kullanma işlemi gösterilmektedir [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) paket ve bir evrensel Windows Platformu (UWP) projesi. Aynı işlemde herhangi diğer .NET veya .NET Core proje için de geçerlidir.

Koduyla paketinde yüklendikten sonra başvurmak `using <namespace>` nerede \<ad alanı\> kullanmakta olduğunuz paket özeldir. Başvuru yapıldığında, kendi API aracılığıyla paket çağırabilirsiniz.

> [!Tip]
> **Başlat nuget.org ile**: Tarama nuget.org olan nasıl .NET geliştiricilerinin bileşenleri genellikle bulmak, kendi uygulamalarında yeniden kullanabilirsiniz. Nuget.org doğrudan arama veya bulabilir ve bu makalede gösterilen şekilde Visual Studio içindeki paketleri yükleyin.

## <a name="prerequisites"></a>Önkoşullar

- Evrensel Windows platformu geliştirme iş yükü ile Visual Studio 2017 veya
- Visual Studio 2015 güncelleştirme 3 Evrensel Windows uygulamaları için Araçlar ile.

2017 Community edition ücretsiz nden yüklenebilecek [visualstudio.com](https://www.visualstudio.com/) ya da Professional veya Enterprise sürümü kullanın.

## <a name="create-a-project"></a>Proje oluşturma

Aynı hedef framework projesi olarak paket desteklediğini varsayarak NuGet paketlerini herhangi .NET projeye yüklenebilir.

Bu kılavuz için basit bir evrensel Windows (UWP) uygulamasını kullanın. Visual Studio kullanarak bir proje oluşturun. **Dosya > Yeni proje...**  ve seçerek **Windows Evrensel > boş uygulama (Evrensel Windows)**. Hedef sürüm ve Minimum istendiğinde sürüm için varsayılan değerleri kabul.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Newtonsoft.Json NuGet paketi ekleme

Paketi yüklemek için Paket Yöneticisi kullanıcı Arabirimi veya Paket Yöneticisi konsolu kullanabilirsiniz. Bir paketi yüklediğinizde, NuGet bağımlılık ya da proje dosyanızı kaydeder veya `packages.config` dosyası. Daha fazla bilgi için bkz: [paket tüketimi genel bakış ve iş akışı](../consume-packages/Overview-and-Workflow.md).

### <a name="package-manager-ui"></a>Paket Yöneticisi kullanıcı Arabirimi

1. Çözüm Gezgini'nde sağ **başvuruları** ve **NuGet paketlerini Yönet**.

    ![NuGet paketlerini komutu için proje başvuruları yönetme](media/QS_Use-02-ManageNuGetPackages.png)

1. "Nuget.org" olarak seçin **paket kaynağı**seçin **Gözat** sekmesinde, arama **Newtonsoft.Json**, listesinde o paketi seçin ve seçin  **Yükleme**:

    ![Newtonsoft.Json paket bulma](media/QS_Use-03-NewtonsoftJson.png)

1. Lisans sizden kabul edin.

1. (Visual Studio 2017) Paket Yönetimi biçimi seçin isteyip istemediğiniz sorulduğunda seçin **PackageReference proje dosyasında**:

    ![Paket Yönetimi biçimi seçme](media/QS_Use-03b-SelectFormat.png)

1. Değişiklikleri gözden geçirmek için istenirse seçin **Tamam**.

### <a name="package-manager-console"></a>Paket Yöneticisi Konsolu

1. Seçin **Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Konsolu** menü komutu.

1. İçin konsolu açar sonra denetleyin **varsayılan proje** aşağı açılan liste içine paket yüklemek istediğiniz proje gösterir. Tek bir proje çözümde varsa, zaten seçilidir.

    ![Newtonsoft.Json paket bulma](media/QS_Use-08-Console1.png)

1. Aşağıdaki komutu girin `Install-Package Newtonsoft.json` (bkz [Install-Package](../tools/ps-ref-install-package.md)). Konsol penceresinde komutunun çıktısını gösterir. Hatalar genellikle paket projenin hedef çerçevesi ile uyumlu değil işaret eder.

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>' % S ' Newtonsoft.Json API uygulamasında kullanma

Projedeki Newtonsoft.Json paketiyle çağırabilirsiniz kendi `JsonConvert.SerializeObject` bir nesne okunabilir bir dizeye dönüştürmek için yöntem.

1. Açık `MainPage.xaml` ve varolan `Grid` aşağıdaki öğeyle:

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. Açık `MainPage.xaml.cs` dosyası (Çözüm Gezgini altında bulunan `MainPage.xaml` düğüm) ve aşağıdaki kodu ekleyin `MainPage` Oluşturucusu:

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

1. Newtonsoft.Json paketini projeye eklenen olsa da, kırmızı dalgalı çizgiler altında görünür `JsonConvert` , gerektiğinden bir `using` kod dosyasının üst deyimi:

    ```cs
    using Newtonsoft.json;
    ```

1. Derleme ve F5 tuşuna basarak veya seçerek uygulamayı çalıştırma **hata ayıklama > hata ayıklamayı Başlat**:

    ![UWP uygulaması ilk çıktısı](media/QS_Use-06-AppStart.png)

1. İle bazı JSON metnin yerine TextBlock içeriğini görmek için düğmeyi seçin:

    ![Düğme seçtikten sonra UWP uygulamasında çıktısı](media/QS_Use-07-AppEnd.png)

## <a name="related-articles"></a>İlgili makaleler

- [Genel bakış ve iş akışı paket tüketimi](../consume-packages/overview-and-workflow.md)
- [Paketleri bulma ve seçme](../consume-packages/finding-and-choosing-packages.md)
- [Bir paketi yüklemek için yollar](../consume-packages/ways-to-install-a-package.md)
- [NuGet Davranışını Yapılandırma](../consume-packages/configuring-nuget-behavior.md)
