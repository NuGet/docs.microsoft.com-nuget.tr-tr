---
title: NuGet paketlerini bulma ve seçme
description: NuGet arama söz dizimi hakkında ayrıntılar dahil olmak üzere bir proje için en iyi NuGet paketlerini bulma ve seçme hakkında genel bakış.
author: karann-msft
ms.author: karann
ms.date: 06/04/2018
ms.topic: conceptual
ms.openlocfilehash: 3af29e2f9b09ba5bd82779f9aacf314bd8933436
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317021"
---
# <a name="finding-and-evaluating-nuget-packages-for-your-project"></a>Projeniz için NuGet paketlerini bulma ve değerlendirme

Herhangi bir .NET projesi başlatırken veya uygulamanız veya hizmetiniz için bir işlevsel ihtiyacı her belirlediğinizde, bu ihtiyacı karşılayan mevcut NuGet paketlerini kullanarak kendinize ait birçok zaman ve sorunu kaydedebilirsiniz. Bu paketler, [NuGet.org](http://www.nuget.org/packages/)üzerindeki genel koleksiyondan veya kuruluşunuz ya da başka bir üçüncü taraf tarafından sunulan özel bir kaynaktan gelebilir.

## <a name="finding-packages"></a>Paketleri bulma

Visual Studio 'da nuget.org 'i ziyaret ettiğinizde veya paket yöneticisi Kullanıcı arabirimini açtığınızda, toplam indirmelere göre sıralanan paketlerin bir listesini görürsünüz. Bu, neredeyse milyonlarca .NET projesi genelinde en yaygın olarak kullanılan paketleri gösterir. Daha sonra, ilk birkaç sayfada listelenen paketlerin en az bir kısmı projelerinizde yararlı olacaktır.

![En popüler paketleri gösteren nuget.org/packages varsayılan görünümü](media/Finding-01-Popularity.png)

Sayfanın sağ üst kısmındaki **ön sürümü dahil et** seçeneğine dikkat edin. Seçildiğinde, nuget.org Beta ve diğer erken sürümler dahil tüm paketlerin sürümlerini gösterir. Yalnızca kararlı olarak yayınlanan öğesini göstermek için seçeneği temizleyin.

Belirli gereksinimler için, etiketlere göre arama (Visual Studio Paket Yöneticisi veya nuget.org gibi bir portal içinde) uygun bir paket bulmak için en yaygın yollardan biridir. Örneğin, "JSON" araması, bu anahtar sözcükle etiketlenmiş tüm NuGet paketlerini listeler ve bu nedenle JSON veri biçimiyle bir ilişki bulunur.

![Nuget.org üzerinde ' JSON ' için arama sonuçları](media/Finding-02-SearchResults.png)

Biliyorsanız, paket KIMLIĞINI kullanarak da arama yapabilirsiniz. Aşağıdaki [arama sözdizimine](#search-syntax) bakın.

Şu anda arama sonuçları yalnızca ilgiye göre sıralanır. bu nedenle, gereksinimlerinize uyan paketlerin en az ilk birkaç sayfasına bakmak veya arama terimlerinizi daha belirgin olacak şekilde daraltmak isteyeceksiniz.

### <a name="does-the-package-support-my-projects-target-framework"></a>Paket, projem 'ın hedef çerçevesini destekliyor mu?

NuGet yalnızca paketin desteklenen çerçeveleri projenin hedef çerçevesini içeriyorsa bir projeyi bir projeye ekler. Paket uyumlu değilse, NuGet bir hata yayınlar.

Bazı paketler desteklenen çerçeveleri doğrudan nuget.org galerisinde listeler, ancak bu tür veriler gerekli olmadığından birçok paket bu listeyi içermez. Mevcut olduğunda, belirli bir hedef Framework 'ü destekleyen paketler için nuget.org araması yapmanız gerekir (özellik dikkate alınmaz, bkz. [NuGet sorunu 2936](https://github.com/NuGet/NuGetGallery/issues/2936)).

Neyse ki, desteklenen çerçeveleri iki farklı yöntemle de belirleyebilirsiniz:

1. NuGet Paket Yöneticisi konsolundaki [`Install-Package`](../reference/ps-reference/ps-ref-install-package.md) komutunu kullanarak bir projeye paket yüklemeyi deneyin. Paket uyumsuzsa, bu komutta paketin desteklenen çerçeveleri gösterilir.

1. **Bilgi**altında **el ile indirme** bağlantısını kullanarak paketi NuGet.org sayfasındaki sayfasından indirin. Uzantısını `.nupkg` `lib` olarak `.zip`değiştirin ve klasörünün içeriğini incelemek için dosyayı açın. Her bir alt klasörün bir hedef çerçeve adıyla (tfd; bkz. [hedef çerçeveler](../reference/target-frameworks.md)) adlandırılmış olduğu her bir desteklenen çerçeve için alt klasörler görürsünüz. Ve yalnızca tek bir dll altında `lib` alt klasör yoksa, uyumluluğunu öğrenmek için bu paketi projenize yüklemeyi denemeniz gerekir.

## <a name="pre-release-packages"></a>Yayın öncesi paketler

Birçok paket yazarı, önizleme ve Beta yayınları, en son düzeltmelerinde iyileştirmeler yapmaya ve geri bildirimde bulunmalarına devam ederken kullanılabilir hale getirir.

Nuget.org, varsayılan olarak, arama sonuçlarında yayın öncesi paketleri gösterir. Yalnızca kararlı sürümlerde arama yapmak için sayfanın sağ üst kısmındaki **ön sürümü dahil et** seçeneğini temizleyin

![Nuget.org üzerine yayın öncesi onay kutusunu Ekle](media/Finding-06-include-prerelease.png)

Visual Studio 'da ve NuGet ve DotNet CLı araçları kullanılırken, NuGet varsayılan olarak yayın öncesi sürümleri içermez. Bu davranışı değiştirmek için aşağıdaki adımları uygulayın:

- **Visual Studio 'Da Paket Yöneticisi Kullanıcı arabirimi**: **NuGet Paketlerini Yönet** Kullanıcı arabiriminde, **ön sürümü dahil et** kutusunu belirleyin. Bu kutuyu ayarlama veya Temizleme, Paket Yöneticisi Kullanıcı arabirimini ve yükleyebileceğiniz sürümlerin listesini yeniler.

    ![Visual Studio 'da ön sürümü dahil et onay kutusu](media/Prerelease_02-CheckPrerelease.png)

- **Paket Yöneticisi konsolu**: `Find-Package`, `-IncludePrerelease` ,,`Install-Package`Ve komutlarıyla`Update-Package` anahtarı kullanın. `Get-Package` `Sync-Package` [PowerShell başvurusuna](../reference/powershell-reference.md)bakın.

- **NuGet. exe CLI**: `install` `-prerelease` , ,`update`Vekomutlarıyla anahtarıkullanın`mirror` . `delete` [NUGET CLI başvurusuna](../reference/nuget-exe-cli-reference.md) bakın

- **DotNet. exe CLI**: `-v` Bağımsız değişkenini kullanarak tam yayın öncesi sürümü belirtin. [DotNet paket başvurusu Ekle](/dotnet/core/tools/dotnet-add-package)' ye başvurun.

<a name="native-cpp-packages"></a>

### <a name="native-c-packages"></a>Yerel C++ paketler

NuGet, yerel C++ paketleri destekler ve bu, Visual Studio C++ 'da projelerde kullanılabilir. Bu, projeler için **NuGet Paketlerini Yönet** bağlam-menü komutunu sağlar, bir `native` hedef çerçeve sunar ve MSBuild tümleştirmesi sağlar.

[NuGet.org](https://www.nuget.org/packages)üzerindeki yerel paketleri bulmak için kullanarak `tag:native`arama yapın. Bu tür paketler genellikle `.targets` ve `.props` dosyalarını sağlar ve paket bir projeye eklendiğinde otomatik olarak NuGet içeri aktarır.

## <a name="evaluating-packages"></a>Paketler değerlendiriliyor

Bir paketin kullanışlılığını değerlendirmek için en iyi yol, bunu indirmek ve kodunuzda denemek (nuget.org üzerindeki tüm paketler düzenli olarak virüsler için taranır). Her ne kadar popüler olan her paket, kendisini kullanan birkaç geliştirici ile başlatılır ve ilk benimseyenlerden biri olabilirsiniz!

Aynı zamanda, bir NuGet paketinin kullanılması, bunun sağlam ve güvenilir olduğundan emin olmak için buna bir bağımlılık alınması anlamına gelir. Bir paketin yüklenmesi ve doğrudan sınanması zaman alıcı olduğundan, bir paketin liste sayfasındaki bilgileri kullanarak bir paketin kalitesi hakkında çok fazla bilgi edinebilirsiniz:

- *İndirmeler istatistikleri*: NuGet.org üzerindeki paket sayfasında, **İstatistikler** bölümünde Toplam indirme, en son sürüm indirmeleri ve günde ortalama indirme işlemleri gösterilir. Daha büyük sayılar, diğer birçok geliştiricinin pakete bağımlılığı olduğunu, yani kendini kanıtlamış olduğunu gösterir.

    ![Bir paketin listeleme sayfasına istatistik yükleme](media/Finding-03-Downloads.png)

- *Sürüm geçmişi*: Paket sayfasında, en son güncelleştirme tarihi için **bilgi** ' yi arayın ve **sürüm geçmişini**inceleyin. İyi tutulan bir pakette, son güncelleştirmeler ve zengin bir sürüm geçmişi bulunur. İhmal edilen paketlerin birkaç güncelleştirmesi vardır ve genellikle bir süre güncelleştirilmemiş demektir.

    ![Paketin listeleme sayfasında sürüm geçmişi](media/Finding-04-VersionHistory.png)

- *Son yüklemeler*: Paket sayfasında **İstatistikler**altında, **tam istatistikleri görüntüle**' yi seçin. Tüm İstatistikler sayfasında, paketin sürüm numarasına göre son altı haftaya göre yüklemesi gösterilmektedir. Diğer geliştiricilerin etkin şekilde kullandığı bir paket, genellikle daha iyi bir seçenektir.

- *Destek*: Yazar **' ın altındaki**paket sayfasında, yazarın sağladığı destek seçeneklerini görmek için **Proje sitesi** ' ni (varsa) seçin. Adanmış bir siteye sahip bir proje genellikle daha iyi desteklenir.

- *Geliştirici geçmişi*: **sahipler**altındaki paket sayfasında, yayımladıkları diğer paketleri görmek için bir sahip seçin. Birden çok pakete sahip olanlar, işlerini daha sonra desteklemeye devam edememe olasılığı yüksektir.

- *Açık kaynak katkıları*: birçok paket açık kaynaklı depolarda tutulur ve bunlar, geliştiricilerin doğrudan hata düzeltmeleri ve özellik iyileştirmeleri katkıda bulunmasına olanak tanır. Belirli bir paketin katkı geçmişi Ayrıca, kaç geliştirici etkin bir şekilde dahil olduğu konusunda iyi bir göstergedir.

- *Sahipleri*arayın: yeni geliştiriciler, sizin için harika paketler oluşturmaya tamamen eşit bir şekilde kararlıdır ve bu kullanıcılara NuGet ekosistemine yeni bir şey getirmenin bir şansı vermek iyi olabilir. Bu göz önünde bulundurularak, liste sayfasında **bilgi** altında **kişi sahipleri** ' nı kullanarak doğrudan paket geliştiricilerine ulaşın. Olasılığınızı karşılamak için sizinle birlikte çalışmak iyi olacaktır!

- *Ayrılmış paket kimliği önekleri*: için çok sayıda paket sahibi uygulandı ve [ayrılmış bir paket kimliği öneki](../nuget-org/id-prefix-reservation.md)verdi. [NuGet.org](https://www.nuget.org/)veya Visual Studio 'daki BIR paket kimliğinin yanındaki görsel onay işaretini gördüğünüzde, bu, paket sahibinin kimlik ön eki ayırma ölçütlerimizi karşıladığı anlamına [](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria) gelir. Bu, paket sahibinin kendilerini ve paketini tanımlamaya açık olduğu anlamına gelir.

> [!Note]
> Her zaman bir paketin lisans koşullarına sahip olun, bu, nuget.org üzerindeki bir paketin liste sayfasında **Lisans bilgileri** ' ni seçerek görebilirsiniz. Bir paket lisans koşulları belirtmezse, paket sayfasındaki **kişi sahipleri** bağlantısını kullanarak doğrudan paket sahibine başvurun. Microsoft, üçüncü taraf paket sağlayıcılarından sizin için herhangi bir fikri mülkiyet hakkı vermez ve üçüncü taraflar tarafından sunulan bilgilerden sorumlu değildir.

## <a name="license-url-deprecation"></a>Lisans URL 'sinin kullanımdan kaldırılması
[Licenseurl](../reference/nuspec.md#licenseurl) 'den [lisansa](../reference/nuspec.md#license)geçiş yaptığımız gibi, bazı NuGet istemcileri ve NuGet akışları, bazı durumlarda lisanslama bilgilerini henüz yüzeye sunmayabilir. Geriye dönük uyumluluğu sürdürmek için lisans URL 'SI bu belgeyi işaret eder ve bu nedenle lisans bilgilerinin bu gibi durumlarda nasıl alınacağı ele alınır.

Bu sayfaya getirilen bir paketin lisans URL 'sine tıkladığınızda, paketin bir lisans dosyası içermesi ve
* Henüz yeni lisans bilgilerini nasıl yorumlayabileceğinizi ve bu bilgileri istemciye **ya** da
* Henüz akış tarafından sağlanmış olan yeni lisans bilgilerini nasıl yorumlayacağını ve okuyabileceğinizi bilmiyor olmayan bir istemci kullanıyorsunuz **veya**
* Her ikisinin birleşimi

Paketin içindeki lisans dosyasında yer alan bilgileri şu şekilde okuyabilirsiniz:
1. NuGet paketini indirin ve içeriğini bir klasöre ayıklayın.
1. Bu klasörün kökünde olacak dosyayıaçın.`.nuspec`
1. Şöyle `<license type="file">license\license.txt</license>`bir etiketi olmalıdır. Bu, lisans dosyasının adlandırıldığını `license.txt` ve bu klasörün kökünde de olacak adlı `license` bir klasörün içinde olduğunu gösterir.
1. Klasöre gidin ve `license.txt` dosyayı açın. `license`


## <a name="search-syntax"></a>Arama söz dizimi

NuGet paket araması, NuGet CLı ve Visual Studio 'daki NuGet Paket Yöneticisi uzantısı içindeki nuget.org üzerinde aynı şekilde çalışmaktadır. Genel olarak, arama anahtar sözcüklere ve paket açıklamalarına uygulanır.

- **Anahtar sözcükler**: Arama, belirtilen anahtar sözcüklerden herhangi birini içeren ilgili paketleri arar. Örnek: `modern UI`. Tüm sunulan anahtar kelimeleri içeren paketleri aramak için, gibi terimler `modern+UI`arasında "+" kullanın.
- **Tümcecikler**: Tırnak işaretleri içine terimleri girmek, bu şartların tam büyük/küçük harf duyarsız eşleşmelerini arar. Örnek: `"modern UI" package`
- **Filtreleme**: `packageid` `id` (Büyük`version`/küçük harf duyarsız) ,`tags`,,,,,,,,,,,,,,,,,,,,,,,, `title` `<property>:<term>` `<property>` `author` `description` ,`summary`ve .`owner` Şartlar gerektiğinde tırnak içinde bulunabilir ve aynı anda birden çok özellik arayabilirsiniz. Ayrıca, `id` özelliğindeki aramalar alt dize eşleşmelerinde `packageid` , tam eşleşme kullanır. Örnekler:

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
