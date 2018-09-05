---
title: NuGet paketleri bulma ve seçme
description: Genel Bakış nasıl bulacağınızı ve NuGet arama söz dizimi hakkında ayrıntılar dahil olmak üzere bir proje için en iyi NuGet paketlerini seçin.
author: karann-msft
ms.author: karann
ms.date: 06/04/2018
ms.topic: conceptual
ms.openlocfilehash: 81672abf0362e053da2b71c8bd39bd7f96ddf73b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549421"
---
# <a name="finding-and-evaluating-nuget-packages-for-your-project"></a>Bulma ve projenizin NuGet paketlerini değerlendiriliyor

Herhangi bir .NET projesine başlatırken veya uygulamanızı veya hizmetinizi işlevsel bir gereksinimi tanımlamak olduğunda, bu gereksinimi karşılayan mevcut NuGet paketlerini kullanarak kendiniz zaman ve sorun çok sayıda kaydedebilirsiniz. Bu paketler genel koleksiyondan gelen [nuget.org](http://www.nuget.org/packages/), ya da kuruluşunuzun veya başka bir üçüncü taraf tarafından sağlanan özel bir kaynak.

## <a name="finding-packages"></a>Paketleri bulma

Visual Studio'da Paket Yöneticisi UI nuget.org ziyaret edin veya açtığınızda, paketlerin toplam yüklemeleri tarafından sıralanan listesini görürsünüz. Bu hemen, en yaygın olarak kullanılan paketler arasında .NET projeleri milyonlarca gösterir. Yok şansı ve sonra en az ilk birkaç sayfalarında listelenen paketlerin bazıları projelerinizde yararlı olacaktır.

![En popüler paketlerin gösteren nuget.org/packages varsayılan görünümü](media/Finding-01-Popularity.png)

Bildirim **ön sürümü dahil et** sayfanın sağ üst seçeneği. Bu onay kutusu seçildiğinde, nuget.org beta ve erken diğer sürümleri de dahil olmak üzere paketlerin tüm sürümlerini gösterir. Yalnızca kararlı gösterecek şekilde serbest bırakıldı, seçeneğini kaldırın.

Belirli gereksinimleriniz için etiketler (Visual Studio Paket Yöneticisi içinde veya portal nuget.org gibi) ile aramayı uygun paket keşfetme en yaygın yoludur. Örneğin, "json" üzerinde arama bu anahtar sözcüğü ile etiketlenir ve bu nedenle bazı ilişki JSON veri biçimine sahip tüm NuGet paketlerini listeler.

![Nuget.org 'json' için arama sonuçları](media/Finding-02-SearchResults.png)

Biliyorsanız paket Kimliğini kullanarak da arama yapabilirsiniz. Bkz: [arama söz dizimi](#search-syntax) aşağıda.

Şu anda genel sonuçları ihtiyaçlarınızı paketler için en az ilk birkaç sayfalarına bakın veya arama terimlerinizi daha belirgin iyileştirmek istediğiniz şekilde arama sonuçları yalnızca uygunluğa göre sıralanır.

### <a name="does-the-package-support-my-projects-target-framework"></a>Paket Projemin hedef Framework'ü destekliyor mu?

Bu paketin desteklenen çerçeveler projenin hedef çerçevesi eklerseniz NuGet bir projeye bir paketi yükler. NuGet, paket uyumlu değilse, bir hata verir.

Bazı paketler kendi desteklenen çerçeveler doğrudan nuget.org galerisinde listelemek, ancak bu tür veriler gerekli olmadığından, birçok paketi listeleyen içermez. Şu anda belirli hedef Framework'ü destekleyen paketleri nuget.org aramak için hiçbir yol yok (değerlendirilmektedir özelliğidir, bkz: [NuGet sorunu 2936](https://github.com/NuGet/NuGetGallery/issues/2936)).

Neyse ki, desteklenen çerçeveler iki diğer araçlarla belirleyebilirsiniz:

1. Bir proje kullanarak paket yüklemeye çalışırsanız [ `Install-Package` ](../tools/ps-ref-install-package.md) NuGet Paket Yöneticisi konsolunda komutu. Paket uyumlu değilse, bu komut paketin desteklenen çerçeveler gösterir.

1. Nuget.org kullanarak kendi sayfasından paketini indirme **el ile yükleme** altında bağlantı **bilgisi**. Uzantı değiştirme `.nupkg` için `.zip`, içeriğini incelemek için dosyasını açın, `lib` klasör. Alt klasörleri her desteklenen çerçeveler, her alt bir hedef çerçeve adı ile adlandırılan burada görmek vardır (TFM; bkz [hedef çerçeve](../reference/target-frameworks.md)). Hiçbir alt klasör altında görürseniz `lib` ve yalnızca tek bir DLL'nin olduktan sonra paketi yükleyin uyumluluğunu bulmak için projenizde denemelidir.

## <a name="pre-release-packages"></a>Yayın öncesi paketleri

Çok sayıda paket yazarlarının önizleme yapın ve iyileştirme yapın ve en son düzeltmeleri hakkında geri bildirim arama indikçe beta sürümleri kullanılabilir.

Varsayılan olarak, arama sonuçlarına yayın öncesi paketleri nuget.org gösterir. Yalnızca kararlı sürümler aramak için temizleyin **ön sürümü dahil et** sayfanın sağ üst seçeneği

![Nuget.org üzerindeki ön onay kutusu Ekle](media/Finding-06-include-prerelease.png)

Visual Studio'da ve NuGet ve dotnet CLI araçlarını kullanırken, NuGet yayın öncesi sürümleri varsayılan olarak içermez. Bu davranışı değiştirmek için aşağıdaki adımları uygulayın:

- **Visual Studio'da Paket Yöneticisi UI**: içinde **NuGet paketlerini Yönet** kullanıcı Arabirimi ayarlama **ön sürümü dahil et** kutusu. Ayarlama ya da bu kutuyu temizleyerek Paket Yöneticisi UI ve yükleyebileceğiniz kullanılabilir sürümlerin listesini yeniler.

    ![Visual Studio'da INCLUDE Ön onay kutusu](media/Prerelease_02-CheckPrerelease.png)

- **Paket Yöneticisi Konsolu**: kullanım `-IncludePrerelease` anahtarı ile `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, ve `Update-Package` komutları. Başvurmak [PowerShell başvurusu](../tools/powershell-reference.md).

- **nuget.exe CLI**: kullanım `-prerelease` anahtarı ile `install`, `update`, `delete`, ve `mirror` komutları. Başvurmak [NuGet CLI başvurusu](../tools/nuget-exe-cli-reference.md)

- **CLI dotnet.exe**: tam yayın öncesi sürümünü kullanarak belirttiğiniz `-v` bağımsız değişken. Başvurmak [dotnet paket başvurusu ekleme](/dotnet/core/tools/dotnet-add-package).

<a name="native-cpp-packages"></a>

### <a name="native-c-packages"></a>Yerel C++ paketleri

Visual Studio'da C++ projelerinde kullanılan yerel C++ paketler için NuGet destekler. Böylece **NuGet paketlerini Yönet** projeleri için bağlam menüsü komutu tanıtır bir `native` hedef framework ve MSBuild tümleştirme sağlar.

Yerel paketler bulmak için [nuget.org](https://www.nuget.org/packages), kullanarak arama `tag:native`. Bu paketleri genellikle sağlar `.targets` ve `.props` dosyaları paket için bir proje eklendiğinde, NuGet otomatik olarak içeri aktarır.

## <a name="evaluating-packages"></a>Paketleri değerlendiriliyor

Bir paket kullanışlılığını değerlendirmek için en iyi yolu, indirin ve deneyin (tüm paketleri nuget.org üzerinde düzenli olarak virüs, biçimde taranır) kodunuzda sağlamaktır. Sonuçta, son derece popüler her paketi kullanmadan yalnızca birkaç geliştiricilere çalışmaya başladınız ve erken Benimseyenler biri olabilir!

Aynı anda bir NuGet paketi kullanarak emin olmak, istediğiniz şekilde üzerine bağımlılık almak, sağlam ve güvenilir olduğu anlamına gelir. Zaman alan yükleme ve doğrudan bir paketi test olduğundan da çok paketin kalitesi hakkında bir paketin Listesi sayfasında bilgileri kullanarak bilgi alabilirsiniz:

- *İstatistikleri indirir*: nuget.org, paket sayfasında **istatistikleri** bölüm toplam yüklemeler, indirmeler en son sürümünün gösterir ve ortalama günlük indirir. Diğer birçok geliştirici, kendini kanıtlamış yani paket bağımlılık gerçekleştirdiğinizden daha büyük bir sayı belirtin.

    ![Bir paketin Listesi sayfasında istatistikleri indirin](media/Finding-03-Downloads.png)

- *Sürüm Geçmişi*: altına paketi sayfasında bakın **bilgisi** en son tarih için güncelleştirme ve incelemek **sürüm geçmişi**. En son güncelleştirmeleri ve zengin sürüm geçmişi iyi tutulan bir paket vardır. İhmal edilen paketler birkaç güncelleştirmelerine sahip olması ve genellikle bir süre içinde güncelleştirilmedi.

    ![Bir paketin Listesi sayfasında sürüm geçmişi](media/Finding-04-VersionHistory.png)

- *Son yükler*: Paket sayfasında altında **istatistikleri**seçin **tam istatistikleri görüntüleme**. Tam istatistikleri sayfası, paketin sürüm numarası tarafından son altı hafta boyunca yükler gösterir. Diğer geliştiriciler etkin olarak kullanan bir genellikle daha iyi bir seçenek değil bir pakettir.

- *Destek*: Paket sayfasında altında **bilgisi**seçin **proje sitesi** (varsa) Yazar hangi destek seçeneklerini görmek için sağlar. Adanmış bir siteyse projesiyle genellikle daha iyi desteklenir.

- *Geliştirici geçmişi*: Paket sayfasında altında **sahipleri**, sahip yayımlanan diğer paketleri görmek için seçin. Birden çok paket olanlar işlerini gelecekte desteklemeye devam olasılığı daha yüksektir.

- *Açık kaynak katkı*: birçok paketi, doğrudan katkıda hata düzeltmeleri ve özellik geliştirmeleri bağlı olarak bunları geliştiricilere edinerek açık kaynaklı depolarında korunur. Herhangi bir paket katkı geçmişini ayrıca geliştiricilerin kaç tane aktif, iyi bir göstergesidir.

- *Sahipleri görüşme*: yeni geliştiriciler kesinlikle kullanabilmeniz için harika paketleri üretmek için eşit olarak kaydedilmiş olabilir ve bunları NuGet ekosistemi için yeni bir şeyler getirmek için bir şans verin daha iyidir. Bunu aklınızda, doğrudan paket geliştiricilere ulaşın **kişi sahipleri** altındaki **bilgisi** Listesi sayfasında. Büyük olasılıkla, size ihtiyaçlarınızı karşılamak için sizi mutlu edecektir demektir!

- *Ayrılmış paket kimliği ön ekleri*: çok sayıda paket sahipleri için uygulanan ve verilmiş bir [ayrılmış paket kimliği öneki](../reference/id-prefix-reservation.md). Üzerinde bir paket kimliği yanındaki visual onay kutusunu gördüğünüzde [nuget.org](https://www.nuget.org/), veya Visual Studio'da anlamına paket sahibinden karşılaşmış bizim [ölçütleri](../reference/id-prefix-reservation.md#id-prefix-reservation-criteria) rezervasyon kimliği öneki. Bu, paket sahibinden kendilerini ve bunların paket tanımlamaya Temizle anlamına gelir.

> [!Note]
> Her zaman seçerek gördüğünüz bir paketin Lisans Koşulları'nın dikkatli olmanızı **lisans bilgilerini** bir paketin listeleme nuget.org sayfasında. Bir paketi lisans koşulları belirtmezse kullanarak doğrudan paket sahibiyle iletişime geçin **sahipleriyle temas** bağlantı paketi sayfasında. Microsoft hiçbir fikri mülkiyet, üçüncü taraf paketi sağlayıcılarından lisans değil ve üçüncü taraflarca sağlanan bilgileri sorumlu değildir.

## <a name="search-syntax"></a>Arama söz dizimi

NuGet paket arama aynı nuget.org, NuGet CLI ve Visual Studio'da NuGet paket yöneticisini uzantısı içinde çalışır. Genel olarak, arama paket açıklamaları yanı sıra anahtar sözcükleri uygulanır.

- **Anahtar sözcükler**: arama için sağlanan anahtar sözcükleri içeremez ilgili paketleri arar. Örnek: `modern UI`. Bir hüküm arasında paketlerin tüm sağlanan anahtar sözcükleri içeren, kullanmak için "+" gibi aranacak `modern+UI`.
- **İfadeleri**: Bu koşulları tam duyarlı eşleşme yapar terimleri tırnak içine girme. Örnek: `"modern UI" package`
- **Filtreleme**: sözdizimini kullanarak, belirli bir özellik için bir arama terimi uygulayabilirsiniz `<property>:<term>` burada `<property>` (büyük-küçük harf duyarsız) olabilir `id`, `packageid`, `version`, `title`, `tags`, `author`, `description`, `summary`, ve `owner`. Koşulları gerekirse tırnak içinde yer alabilir ve aynı anda birden çok özellik için arama yapabilirsiniz. Ayrıca, arama yapar `id` özelliği olan eşleşmelerini, oysa `packageid` tam bir eşleşme kullanır. Örnekler:

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
