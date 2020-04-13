---
title: Mac için Visual Studio'da nuget paketi yükleyin ve kullanın
description: Mac projesi için Visual Studio'da bir NuGet paketini yükleme ve kullanma süreci hakkında bir iz geçidi öğreticisi.
author: jmatthiesen
ms.author: jomatthi
ms.date: 08/14/2019
ms.topic: quickstart
ms.openlocfilehash: 6f3fd4f2ffec0037a48aec845fddee258b5c1e7f
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "70238527"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-for-mac"></a>Quickstart: Mac için Visual Studio'da bir paket yükleyin ve kullanın

NuGet paketleri, diğer geliştiricilerin projelerinizde kullanmak üzere kullanabileceğiniz yeniden kullanılabilir kodlar içerir. NuGet [nedir?](../What-is-NuGet.md) Paketler NuGet Paket Yöneticisi kullanılarak Mac projesi için bir Visual Studio'ya yüklenir. Bu makale, popüler [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) paketi ve .NET Core konsol projesini kullanarak süreci göstermektedir. Aynı işlem diğer Xamarin veya .NET Core projesi için de geçerlidir.

Yüklendikten sonra, ad alanının `using <namespace>` \<\> kullanmakta olduğunuz pakete özgü olduğu koddaki pakete bakın. Başvuru yapıldıktan sonra, paketi API'si aracılığıyla arayabilirsiniz.

> [!Tip]
> **nuget.org ile başlayın**: nuget.org göz *atma* ,NET geliştiricilerin genellikle kendi uygulamalarında yeniden kullanabilecekleri bileşenleri nasıl bulduklarıdır. Bu makalede gösterildiği gibi *doğrudan nuget.org* arayabilir veya Visual Studio'daki paketleri bulabilir ve yükleyebilirsiniz. Genel bilgi için [NuGet paketlerini bul ve değerlendirin.](../consume-packages/finding-and-choosing-packages.md)

## <a name="prerequisites"></a>Ön koşullar

- Mac için Visual Studio 2019.

2019 Topluluk sürümünü [visualstudio.com](https://www.visualstudio.com/) ücretsiz olarak yükleyebilir veya Professional veya Enterprise sürümlerini kullanabilirsiniz.

Windows'da Visual Studio kullanıyorsanız, [Visual Studio'da (Yalnızca Windows) bir paketi yükle'ye](install-and-use-a-package-in-visual-studio.md)bakın ve kullanın.

## <a name="create-a-project"></a>Proje oluşturma

NuGet paketleri, paketin projeyle aynı hedef çerçeveyi desteklemesi koşuluyla herhangi bir .NET projesine yüklenebilir.

Bu iz için basit bir .NET Core Console uygulamasını kullanın. Dosya > Yeni Çözüm'> kullanarak Mac için Visual Studio'da bir proje **oluşturun...** **.NET Core > App > Console Application** şablonu'nu seçin. **İleri**’ye tıklayın. İstendiğinde **Hedef Çerçeve** için varsayılan değerleri kabul edin.

Visual Studio, Solution Explorer'da açılan projeyi oluşturur.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Newtonsoft.Json NuGet paketini ekleyin

Paketi yüklemek için NuGet Paket Yöneticisi'ni kullanırsınız. Bir paket yüklediğinizde, NuGet bağımlılıkları proje dosyanıza `packages.config` veya dosyanızda kaydeder (proje biçimine bağlı olarak). Daha fazla bilgi için [bkz: Paket tüketimine genel bakış ve iş akışı.](../consume-packages/Overview-and-Workflow.md)

### <a name="nuget-package-manager"></a>NuGet Paket Yöneticisi

1. Çözüm Gezgini'nde, **Bağımlılıklar'ı** sağ tıklatın ve **Paket Ekle'yi seçin...** seçeneğini belirleyin.

    ![Proje Başvuruları için NuGet Paketleri komutunu yönetme](media/QS_Use_Mac-02-ManageNuGetPackages.png)

1. İletişim kutusunun sol üst **köşesindeki Paket kaynağı** olarak "nuget.org" seçeneğini belirleyin ve **Newtonsoft.Json'ı**arayın, listedeki paketi seçin ve **Paket Ekle'yi seçin...**

    ![Newtonsoft.Json paketinin bulunması](media/QS_Use_Mac-03-NewtonsoftJson.png)

    NuGet Paket Yöneticisi hakkında daha fazla bilgi istiyorsanız, [Mac için Visual Studio'yu kullanarak paketleri yükle ve yönet'](../consume-packages/install-use-packages-visual-studio.md)e bakın.

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Uygulamada Newtonsoft.Json API'yi kullanın

Projedeki Newtonsoft.Json paketi yle, bir `JsonConvert.SerializeObject` nesneyi insan tarafından okunabilir bir dize dönüştürme yöntemini arayabilirsiniz.

1. Dosyayı `Program.cs` açın (Çözüm Defteri'nde bulunan) ve dosya içeriğini aşağıdaki kodla değiştirin:

    ```cs
    using System;
    using Newtonsoft.Json;

    namespace NuGetDemo
    {
        public class Account
        {
            public string Name { get; set; }
            public string Email { get; set; }
            public DateTime DOB { get; set; }
        }
    
        class Program
        {
            static void Main(string[] args)
            {
                Account account = new Account()
                {
                    Name = "Joe Doe",
                    Email = "joe@test.com",
                    DOB = new DateTime(1976, 3, 24)
                };
                string json = JsonConvert.SerializeObject(account);
                Console.WriteLine(json);
            }
        }
    }
    ```

1. Hata Ayıklama yı **başlat'> çalıştır'ı**seçerek uygulamayı oluşturun ve çalıştırın:

1. Uygulama çalıştırıldıktan sonra, seri leştirilmiş JSON çıkışının konsolda göründüğünü görürsünüz:

  ![Konsol uygulamasının çıktısı](media/QS_Use_Mac-06-AppStart.png)

## <a name="next-steps"></a>Sonraki adımlar
İlk NuGet paketinizi yükledikten ve kullandığınız için tebrikler!

> [!div class="nextstepaction"]
> [Mac için Visual Studio'u kullanarak paketleri yükleyin ve yönetin](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)

NuGet'in sunduğu daha fazlasını keşfetmek için aşağıdaki bağlantıları seçin.

- [Paket tüketimine genel bakış ve iş akışı](../consume-packages/overview-and-workflow.md)
- [Proje dosyalarında paket başvuruları](../consume-packages/package-references-in-project-files.md)
