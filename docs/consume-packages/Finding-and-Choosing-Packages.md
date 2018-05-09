---
title: Bulma ve NuGet paketlerini seçme
description: Genel Bakış nasıl bulacağınızı ve Ayrıntılar NuGet arama söz dizimi dahil olmak üzere bir proje için en iyi NuGet paketlerini seçin.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 94d851cfbc860e50b02ca99595ca41bbf4ce21ef
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="finding-and-evaluating-nuget-packages-for-your-project"></a>Bulma ve projenizin NuGet paketlerini değerlendirme

Herhangi bir .NET projesinin başlatırken veya uygulama veya hizmet işlevsel gereksinimini tanımlamak olduğunda bu gereksinimi karşılayan mevcut NuGet paketlerini kullanarak kendiniz pek çok zaman ve sorun kaydedebilirsiniz. Bu paketleri ortak koleksiyonundan gelen [nuget.org](http://www.nuget.org/packages/), ya da kuruluşunuzun veya başka bir üçüncü taraf tarafından sağlanan özel bir kaynak.

## <a name="finding-packages"></a>Paketleri bulma

Visual Studio'da Paket Yöneticisi kullanıcı Arabirimi nuget.org ziyaret edin veya açtığınızda, paketlerin toplam indirmeleri tarafından sıralanan listesini görürsünüz. Bu hemen, en yaygın olarak kullanılan paketler arasında .NET projeleri milyonlarca gösterir. Yoktur şansı, böylece, en az ilk birkaç sayfalarında listelenen paketler bazıları projelerinizde yararlı olacaktır.

![En popüler paketleri gösteren nuget.org/packages varsayılan görünümü](media/Finding-01-Popularity.png)

Bildirim **dahil et** sayfasının sağ üst seçeneği. Seçili olduğunda, nuget.org paketlerini beta ve diğer sürümleri erken dahil tüm sürümleri gösterilir. Yalnızca kararlı göstermek için yayımlanan, seçeneğini kaldırın.

Özel gereksinimlerinizi karşılamak için etiketler (içinde Visual Studio Paket Yöneticisi veya bir portal nuget.org gibi) kriteri uygun paket keşfinde en yaygın anlamına gelir. Örneğin, "json" üzerinde arama bu anahtar sözcüğü ile etiketlenir ve bu nedenle bazı JSON veri biçimi ilişkisi tüm NuGet paketlerini listeler.

![Nuget.org 'json' için arama sonuçları](media/Finding-02-SearchResults.png)

Biliyorsanız paket Kimliğini kullanarak da arama yapabilirsiniz. Bkz: [arama söz dizimi](#search-syntax) aşağıda.

Genellikle sonuçları gereksinimlerinize uygun paketler için en az ilk birkaç sayfalarına bakın veya daha belirgin olması için arama terimleri iyileştirmek istediğiniz şekilde şu anda arama sonuçları yalnızca ilgi göre sıralanır.

### <a name="does-the-package-support-my-projects-target-framework"></a>Paket my projenin hedef çerçevesi destekliyor mu?

Yalnızca bu paketin desteklenen çerçeveleri projenin hedef çerçevesi eklerseniz NuGet paket bir projeye yükler. NuGet paket uyumlu değilse, bir hata verir.

Bazı paketler kendi desteklenen çerçeveleri doğrudan nuget.org galerisinde listelemek, ancak bu tür veriler gerekli olmadığı için bu listeyi birçok paketleri dahil etmeyin. Şu anda nuget.org belirli hedef çerçevesini destekleyen paketler için arama için hiçbir yol yok (husustur altında özelliği, bkz: [NuGet sorunu 2936](https://github.com/NuGet/NuGetGallery/issues/2936)).

Neyse ki, desteklenen çerçeveler arasında başka yollarla iki belirleyebilirsiniz:

1. Bir proje kullanarak bir paket yükleme girişimi [ `Install-Package` ](../tools/ps-ref-install-package.md) NuGet Paket Yöneticisi konsolunda komutu. Paket uyumlu değilse, bu komut, paketin desteklenen çerçeveleri gösterir.

1. Nuget.org kullanarak kendi sayfasından paketini indirin **el ile yükleme** altında bağlantı **bilgisi**. Uzantı değiştirme `.nupkg` için `.zip`ve içeriğini incelemek için dosyayı açın, `lib` klasörü. Her biri her alt bir hedef framework ad ile adlandırılan burada desteklenen çerçeveleri için alt klasörler görüşmek (TFM; bkz [hedef çerçeveyi](../reference/target-frameworks.md)). Hiçbir alt görürseniz `lib` yalnızca tek bir DLL olduktan sonra paketi uyumluluğunu bulmak için projenizde yüklemeyi denerseniz gerekir.

## <a name="pre-release-packages"></a>Ön yayın paketleri

Çok sayıda paket yazarlar önizleme yapın ve geliştirmeler yapmak ve bunların en son düzeltmeler geribildirim arama devam ederken beta kullanılabilir serbest bırakır.

Varsayılan olarak, nuget.org arama sonuçlarında ön sürüm paketlerini gösterir. Yalnızca kalıcı sürümleri arama yapmak için temizleyin **dahil et** sayfasının sağ üst seçeneği

![Nuget.org Ön onay kutusuna içerir](media/Finding-06-include-prerelease.png)

NuGet Visual Studio ve NuGet ve dotnet CLI araçlarını kullanırken, yayın öncesi sürümleri varsayılan olarak içermez. Bu davranışı değiştirmek için aşağıdaki adımları uygulayın:

- **Visual Studio'da Paket Yöneticisi kullanıcı Arabirimi**: içinde **NuGet paketlerini Yönet** UI, ayarlamak **dahil et** kutusu. Ayarlama ya da bu kutusunu temizleyerek Paket Yöneticisi kullanıcı Arabirimi ve yükleyebileceğiniz kullanılabilir sürümlerin listesini yeniler.

    ![Visual Studio INCLUDE Ön onay kutusu](media/Prerelease_02-CheckPrerelease.png)

- **Paket Yöneticisi Konsolu**: kullanım `-IncludePrerelease` anahtarı ile `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, ve `Update-Package` komutları. Başvurmak [PowerShell başvurusu](../tools/powershell-reference.md).

- **nuget.exe CLI**: kullanım `-prerelease` anahtarı ile `install`, `update`, `delete`, ve `mirror` komutları. Başvurmak [NuGet CLI başvurusu](../tools/nuget-exe-cli-reference.md)

- **DotNet.exe CLI**: tam yayım öncesi sürümünü kullanarak belirtin `-v` bağımsız değişkeni. Başvurmak [dotnet paketi Başvurusu Ekle](/dotnet/core/tools/dotnet-add-package).

<a name="native-cpp-packages"></a>

### <a name="native-c-packages"></a>Yerel C++ paketleri

Visual Studio'da C++ projelerinde kullanılan yerel C++ paketler için NuGet destekler. Böylece **NuGet paketlerini Yönet** projeleri için bağlam menüsü komutu tanıtır bir `native` hedef çerçevesi ve MSBuild tümleştirme sağlar.

Yerel paketleri bulunamadı [nuget.org](https://www.nuget.org/packages), kullanarak arama `tag:native`. Bu tür paketleri genellikle sağlamak `.targets` ve `.props` paket bir projeye eklendiğinde, NuGet otomatik olarak içeri aktarır dosyaları.

## <a name="evaluating-packages"></a>Paketleri değerlendirme

Bir paket yararlılığı değerlendirmek için en iyi indirip (nuget.org tüm paketleri düzenli olarak virüslere karşı şekilde taranır) kodunuzda denemek için yoludur. Sonuçta, her son derece popüler paket yalnızca kullanmadan birkaç geliştiricilere kullanmaya ve erken Benimseyenler biri olabilir!

Bir NuGet paketi kullanarak aynı anda emin olmak istediğiniz şekilde bir bağımlılık üzerinde alma güçlü ve güvenilir olduğu anlamına gelir. Yükleme ve doğrudan bir paketi test zaman olduğundan da çok bir paketin kalite hakkında bir paketin listeleme sayfasında bilgileri kullanarak bilgi alabilirsiniz:

- *İstatistikleri indirmeleri*: nuget.org, paket sayfasında **istatistikleri** bölüm toplam yüklemeleri, en son sürümü karşıdan yüklemeleri gösterir ve ortalama günde indirir. Büyük sayılar diğer birçok geliştiriciler, kendini kanıtlamış anlamı paketi bir bağımlılık önlemlerin gösterir.

    ![Bir paketin listeleme sayfasında istatistikleri indirin](media/Finding-03-Downloads.png)

- *Sürüm Geçmişi*: Paket sayfasında altında görüneceğini **bilgisi** en son tarihini güncelleştirme ve incelemek **sürüm geçmişi**. İyi tutulan paketin en son güncelleştirmeleri ve zengin sürüm geçmişi vardır. İhmal paketleri birkaç güncelleştirmelerine sahip olması ve genellikle biraz zaman güncelleştirilmedi.

    ![Bir paketin listeleme sayfasında sürüm geçmişi](media/Finding-04-VersionHistory.png)

- *Son yükler*: altında paketi sayfasında **istatistikleri**seçin **görüntülemek tam istatistiği**. Son altı hafta sürüm numarasına göre içindeki paketi yükler tam istatistikleri sayfası gösterir. Diğer geliştiriciler etkin olarak kullanan bir genellikle olmayan olandan daha iyi bir seçim paketidir.

- *Destek*: altında paketi sayfasında **bilgisi**seçin **proje sitesi** (varsa) Yazar hangi destek seçeneklerini görmek için sağlar. Ayrılmış bir site içeren bir proje genellikle daha iyi desteklenir.

- *Geliştirici geçmişi*: altında paketi sayfasında **sahipleri**, sahip yayımlanan diğer paketleri görmek için seçin. Birden çok paket olanlar işlerine gelecekte desteklemeye devam olasılığı daha yüksektir.

- *Kaynak Katkıları açmak*: birçok paketleri doğrudan hata düzeltmeleri katkıda ve özellik geliştirmeleri bunları bağlı olarak geliştiriciler edinerek açık kaynak depoları korunur. Verilen herhangi bir paket katkı geçmişini ayrıca kaç geliştiriciler etkin olarak dahil edilen, iyi bir göstergesidir.

- *Sahipleri görüşme*: yeni geliştiriciler kesinlikle kullanabilmeniz için harika paketleri oluşturan için eşit olarak kaydedilmiş olabilir ve NuGet ekosistemi yeni bir şey getirme olanağı vermek uygundur. Bu durum dikkate alınarak, doğrudan aracılığıyla paket geliştiricilerin ulaşmak **kişi sahipleri** altında seçeneği **bilgisi** listeleme sayfasında. Olasılığı olan gereksinimlerinizi sunmak için sizinle birlikte çalışma mutluluk!

- *Ayrılmış paket kimliği önekleri*: çok sayıda paket sahipleri için uyguladığınız ve verilmiş bir [ayrılmış paket kimliği öneki](../reference/id-prefix-reservation.md). Üzerinde bir paket kimliği yanındaki visual onay işaretine gördüğünüzde [nuget.org](https://www.nuget.org/), veya Visual Studio'da anlamına paket sahibinden karşıladığı bizim [ölçütleri](../reference/id-prefix-reservation.md#id-prefix-reservation-criteria) kimliği öneki ayırma. Bu, paket sahibinden kendilerini ve bunların paket tanımlamaya Temizle anlamına gelir.

> [!Note]
> Her zaman seçerek görebileceğiniz bir paketin lisans koşullarını dikkatli olmanızı **lisans bilgilerini** bir paketin listeleme nuget.org sayfasında. Bir paketi Lisans Koşulları'nı belirtmiyorsa kullanarak doğrudan paketi sahibine başvurun **sahipleri başvurun** bağlantı paketi sayfasında. Microsoft hiçbir fikri mülkiyet, üçüncü taraf paket sağlayıcılardan lisans değildir ve üçüncü taraflar tarafından sağlanan bilgileri sorumlu değildir.

## <a name="search-syntax"></a>Search sözdizimi

NuGet paket arama aynı nuget.org, NuGet clı'dan ve Visual Studio'da NuGet Paket Yöneticisi uzantısı içinde çalışır. Genel olarak, arama paket açıklamaları yanı sıra anahtar sözcükleri uygulanır.

- **Anahtar sözcükler**: arama için sağlanan tüm anahtar sözcükler içeren ilgili paketleri arar. Örnek: `modern UI javascript`
- **Tümcecikleri**: tırnak işaretleri içindeki koşulları girmeniz arar bu koşulları büyük küçük harf duyarsız tam eşleşme. Örnek: `"modern UI" package`
- **Filtreleme**: sözdizimini kullanarak belirli bir özellik için bir arama terimi uygulayabilirsiniz `<property>:<term>` nerede `<property>` (büyük küçük harf duyarsız) olabilir `id`, `packageid`, `version`, `title`, `tags`, `author`, `description`, `summary`, ve `owner`. Koşulları gerekirse tırnak içine bulunabilir ve aynı anda birden çok özellikleri için arama yapabilirsiniz. Ayrıca, üzerinde arar `id` özelliği olan eşleşmelerini, ancak `packageid` tam bir eşleşme kullanır. Örnekler:

    ```
    id:NuGet.Core                # Match any part of the id property
    Id:"Nuget.Core"
    ID:jQuery
    title:jquery                 # Searches title as shown on the package listing
    PackageId:jquery             # Match the package id exactly
    id:jquery id:ui              # Search for multiple terms in the id
    id:jquery tags:validation    # Search multiple properties
    id:"jquery.ui"               # Phrase search
    invalid:jquery ui            # Unsupported properties are ignored, so this
                                 # is the same as searching on jquery ui
    ```
