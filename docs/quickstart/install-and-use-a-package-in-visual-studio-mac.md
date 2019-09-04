---
title: Mac için Visual Studio bir NuGet paketi yükleyip kullanın
description: Bir Mac için Visual Studio projesindeki NuGet paketini yükleme ve kullanma işlemi hakkında bir adım adım öğretici.
author: jmatthiesen
ms.author: jomatthi
ms.date: 08/14/2019
ms.topic: quickstart
ms.openlocfilehash: 6f3fd4f2ffec0037a48aec845fddee258b5c1e7f
ms.sourcegitcommit: ac9a00ccaf90e539a381e92b650074910b21eb0d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/03/2019
ms.locfileid: "70238527"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-for-mac"></a>Hızlı Başlangıç: Mac için Visual Studio bir paketi yükleyip kullanma

NuGet paketleri, diğer geliştiricilerin projelerinizde kullanabileceğiniz bir yeniden kullanılabilir kod içerir. Arka plan için bkz. [NuGet nedir?](../What-is-NuGet.md) . Paketler, NuGet Paket Yöneticisi kullanılarak bir Mac için Visual Studio projesine yüklenir. Bu makalede, popüler [Newtonsoft. JSON](https://www.nuget.org/packages/Newtonsoft.Json/) paketini ve bir .NET Core konsol projesini kullanan işlem gösterilmektedir. Aynı işlem diğer Xamarin veya .NET Core projeleri için de geçerlidir.

Yüklendikten sonra, koddaki `using <namespace>` \<pakete, ad alanının\> kullandığınız pakete özgü olduğunu bakın. Başvuru yapıldıktan sonra, paketini API 'SI aracılığıyla çağırabilirsiniz.

> [!Tip]
> **NuGet.org Ile Başlat**: *NuGet.org* gözatma, .NET geliştiricilerinin kendi uygulamalarında yeniden kullanabilecekleri bileşenleri genellikle bulmasıdır. Bu makalede gösterildiği gibi, *NuGet.org* doğrudan arayabilir veya Visual Studio içinde paketleri bulabilir ve yükleyebilirsiniz. Genel bilgi için bkz. [NuGet paketlerini bulma ve değerlendirme](../consume-packages/finding-and-choosing-packages.md).

## <a name="prerequisites"></a>Önkoşullar

- Mac için Visual Studio 2019.

2019 Community Edition 'ı [VisualStudio.com](https://www.visualstudio.com/) adresinden ücretsiz olarak yükleyebilir veya profesyonel ya da Enterprise sürümlerini kullanabilirsiniz.

Windows üzerinde Visual Studio kullanıyorsanız bkz. [Visual Studio 'da paket yükleyip kullanma (yalnızca Windows)](install-and-use-a-package-in-visual-studio.md).

## <a name="create-a-project"></a>Proje oluşturma

NuGet paketleri, paketin proje ile aynı hedef Framework 'ü desteklemesi kaydıyla herhangi bir .NET projesine yüklenebilir.

Bu izlenecek yol için basit bir .NET Core konsol uygulaması kullanın. **Dosya > yeni çözüm...** ' yi kullanarak Mac için Visual Studio bir proje oluşturun, **.NET Core > uygulama > konsol uygulaması** şablonunu seçin. **İleri**'ye tıklayın. İstendiğinde **hedef Framework** için varsayılan değerleri kabul edin.

Visual Studio, Çözüm Gezgini ' de açılan projeyi oluşturur.

## <a name="add-the-newtonsoftjson-nuget-package"></a>Newtonsoft. JSON NuGet paketini ekleyin

Paketi yüklemek için NuGet Paket Yöneticisi 'Ni kullanırsınız. Bir paket yüklediğinizde, NuGet, proje dosyanıza ya da bir `packages.config` dosyaya (proje biçimine bağlı olarak) bağımlılığı kaydeder. Daha fazla bilgi için bkz. [paket tüketimine genel bakış ve iş akışı](../consume-packages/Overview-and-Workflow.md).

### <a name="nuget-package-manager"></a>NuGet Paket Yöneticisi

1. Çözüm Gezgini ' de **Bağımlılıklar** ' a sağ tıklayın ve **paket Ekle...** öğesini seçin.

    ![Proje başvuruları için NuGet Paketlerini Yönet komutu](media/QS_Use_Mac-02-ManageNuGetPackages.png)

1. İletişim kutusunun sol üst köşesindeki **paket kaynağı** olarak "NuGet.org" öğesini seçin ve **Newtonsoft. JSON**için arama yapın, listeden bu paketi seçin ve **paket Ekle...** ' yi seçin:

    ![Newtonsoft. JSON paketi bulunuyor](media/QS_Use_Mac-03-NewtonsoftJson.png)

    NuGet Paket Yöneticisi hakkında daha fazla bilgi edinmek istiyorsanız, bkz. [Mac için Visual Studio kullanarak paketleri yükleyip yönetme](../consume-packages/install-use-packages-visual-studio.md).

## <a name="use-the-newtonsoftjson-api-in-the-app"></a>Uygulamada Newtonsoft. JSON API 'sini kullanma

Projedeki Newtonsoft. JSON paketiyle, bir nesneyi insan tarafından okunabilen bir dizeye dönüştürmek `JsonConvert.SerializeObject` için yöntemini çağırabilirsiniz.

1. `Program.cs` Dosyayı açın (çözüm bölmesi) ve dosya içeriğini aşağıdaki kodla değiştirin:

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

1. **Çalıştır > hata ayıklamayı Başlat**öğesini seçerek uygulamayı derleyin ve çalıştırın:

1. Uygulama çalıştıktan sonra, serileştirilmiş JSON çıkışının konsolunda göründüğünü görürsünüz:

  ![Konsol uygulamasının çıkışı](media/QS_Use_Mac-06-AppStart.png)

## <a name="next-steps"></a>Sonraki adımlar
İlk NuGet paketinizi yükleme ve kullanma hakkında Tebrikler!

> [!div class="nextstepaction"]
> [Mac için Visual Studio kullanarak paket yükleyip yönetme](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)

NuGet 'in sunabileceği daha fazlasını araştırmak için aşağıdaki bağlantıları seçin.

- [Paket tüketiminin genel bakış ve iş akışı](../consume-packages/overview-and-workflow.md)
- [Proje dosyalarında paket başvuruları](../consume-packages/package-references-in-project-files.md)
