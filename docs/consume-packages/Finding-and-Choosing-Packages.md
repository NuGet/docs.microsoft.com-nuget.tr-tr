---
title: NuGet paketlerini bulma ve seçme
description: NuGet arama söz dizimi hakkında ayrıntılar dahil olmak üzere bir proje için en iyi NuGet paketlerini bulma ve seçme hakkında genel bakış.
author: JonDouglas
ms.author: jodou
ms.date: 06/04/2018
ms.topic: conceptual
ms.openlocfilehash: 4ba51028c1a69a3466cec655db19c2c498e29d9b
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775174"
---
# <a name="finding-and-evaluating-nuget-packages-for-your-project"></a>Projeniz için NuGet paketlerini bulma ve değerlendirme

Herhangi bir .NET projesi başlatırken veya uygulamanız veya hizmetiniz için bir işlevsel ihtiyacı her belirlediğinizde, bu ihtiyacı karşılayan mevcut NuGet paketlerini kullanarak kendinize ait birçok zaman ve sorunu kaydedebilirsiniz. Bu paketler, [NuGet.org](https://www.nuget.org/packages/)üzerindeki genel koleksiyondan veya kuruluşunuz ya da başka bir üçüncü taraf tarafından sunulan özel bir kaynaktan gelebilir.

## <a name="finding-packages"></a>Paketleri bulma

Visual Studio 'da nuget.org 'i ziyaret ettiğinizde veya paket yöneticisi Kullanıcı arabirimini açtığınızda, yeniden dengelenecek paketlerin bir listesini görürsünüz. Bu, tüm .NET projeleri genelinde en yaygın olarak kullanılan paketleri gösterir. Bu paketlerin bazılarının kendi projeleriniz için yararlı olabileceğinden iyi bir fikir var!

![En popüler paketleri gösteren nuget.org/packages varsayılan görünümü](media/Finding-01-Popularity.png)

Nuget.org üzerinde, sayfanın sağ üst kısmındaki **filtre** düğmesine dikkat edin. Tıklandığında, gelişmiş arama paneli, sıralama ve filtreleme seçeneklerini sunmak üzere genişletilir.

![Nuget.org üzerinde ' JSON ' için arama sonuçları](media/Finding-02-SearchResults.png)

Belirli bir türün paketlerini göstermek için **paket türü** filtresini kullanabilirsiniz:
- **`All types`**: Bu, varsayılan davranıştır. Türlerine bakılmaksızın tüm paketleri gösterir.
- **`Dependency`**: Projenize yüklenebilen, normal NuGet paketleri.
- **`.NET tool`**: Bu, konsol uygulaması içeren bir NuGet paketi olan [.net araçlarına](/dotnet/core/tools/global-tools)filtre uygular.
- **`Template`**: Bu, komutunu kullanarak yeni projeler oluşturmak için kullanılabilen [.net şablonlarına](/dotnet/core/install/templates)filtre uygular [`dotnet new`](/dotnet/core/tools/dotnet-new) .

Arama sonuçlarını sıralamak için **sıralama ölçütü** seçeneğini kullanabilirsiniz:
- **`Relevance`**: Bu, varsayılan davranıştır. Sonuçları bir iç Puanlama algoritmasına göre sıralar.
- **`Downloads`**: Arama sonuçlarını, Toplam indirme sayısına göre azalan sırayla sıralar.
- **`Recently updated`**: Arama sonuçlarını, en son sürümünün oluşturulma tarihine göre azalan kronolojik düzende sıralar.

**Seçenekler** bölümünde, **`Include prerelease`** onay kutusunu bulabilirsiniz.
İşaretlendiğinde, nuget.org ön sürümler dahil tüm paketlerin sürümlerini gösterir. Yalnızca kararlı sürümleri göstermek için seçeneği temizleyin.

Arama filtrelerini uygulamak için **`Apply`** düğmeye tıklayın. Düğmeye tıklayarak her zaman varsayılan davranışa geri dönebilirsiniz **`Reset`** .

Etiketleri, sahipleri ve paket kimliklerini filtrelemek için [arama sözdizimini](#search-syntax) de kullanabilirsiniz.

### <a name="does-the-package-support-my-projects-target-framework"></a>Paket, projem 'ın hedef çerçevesini destekliyor mu?

NuGet yalnızca paketin desteklenen çerçeveleri projenin hedef çerçevesini içeriyorsa bir projeyi bir projeye ekler. Paket uyumlu değilse, NuGet bir hata yayınlar.

Bazı paketler desteklenen çerçeveleri doğrudan nuget.org galerisinde listeler, ancak bu tür veriler gerekli olmadığından birçok paket bu listeyi içermez. Mevcut olduğunda, belirli bir hedef Framework 'ü destekleyen paketler için nuget.org araması yapmanız gerekir (özellik dikkate alınmaz, bkz. [NuGet sorunu 2936](https://github.com/NuGet/NuGetGallery/issues/2936)).

Neyse ki, desteklenen çerçeveleri iki farklı yöntemle de belirleyebilirsiniz:

1. NuGet Paket Yöneticisi konsolundaki komutunu kullanarak bir projeye paket yüklemeyi deneyin [`Install-Package`](../reference/ps-reference/ps-ref-install-package.md) . Paket uyumsuzsa, bu komutta paketin desteklenen çerçeveleri gösterilir.

1. **Bilgi** altında **el ile indirme** bağlantısını kullanarak paketi NuGet.org sayfasındaki sayfasından indirin. Uzantısını `.nupkg` olarak değiştirin `.zip` ve klasörünün içeriğini incelemek için dosyayı açın `lib` . Her bir alt klasörün bir hedef çerçeve adıyla (tfd; bkz. [hedef çerçeveler](../reference/target-frameworks.md)) adlandırılmış olduğu her bir desteklenen çerçeve için alt klasörler görürsünüz. `lib`Ve yalnızca tek BIR DLL altında alt klasör yoksa, uyumluluğunu öğrenmek için bu paketi projenize yüklemeyi denemeniz gerekir.

## <a name="pre-release-packages"></a>Yayın öncesi paketler

Birçok paket yazarı, önizleme ve Beta yayınları, en son düzeltmelerinde iyileştirmeler yapmaya ve geri bildirimde bulunmalarına devam ederken kullanılabilir hale getirir.

Nuget.org, varsayılan olarak, arama sonuçlarında yayın öncesi paketleri gösterir. Yalnızca kararlı sürümlerde arama yapmak için, sayfanın sağ üst kısmındaki **filtre** düğmesinden erişilebilen gelişmiş arama panelinde, **ön sürümü dahil et** seçeneğini temizleyin

![Nuget.org üzerine yayın öncesi onay kutusunu Ekle](media/Finding-06-include-prerelease.png)

Visual Studio 'da ve NuGet ve DotNet CLı araçları kullanılırken, NuGet varsayılan olarak yayın öncesi sürümleri içermez. Bu davranışı değiştirmek için aşağıdaki adımları uygulayın:

- **Visual Studio 'Da Paket Yöneticisi Kullanıcı arabirimi**: **NuGet Paketlerini Yönet** Kullanıcı arabiriminde, **ön sürümü dahil et** kutusunu belirleyin. Bu kutuyu ayarlama veya Temizleme, Paket Yöneticisi Kullanıcı arabirimini ve yükleyebileceğiniz sürümlerin listesini yeniler.

    ![Visual Studio 'da ön sürümü dahil et onay kutusu](media/Prerelease_02-CheckPrerelease.png)

- **Paket Yöneticisi konsolu**:,,, `-IncludePrerelease` `Find-Package` `Get-Package` `Install-Package` `Sync-Package` ve `Update-Package` komutlarıyla anahtarı kullanın. [PowerShell başvurusuna](../reference/powershell-reference.md)bakın.

- **CLInuget.exe**:,, `-prerelease` `install` `update` `delete` ve komutlarıyla anahtarı kullanın `mirror` . [NUGET CLI başvurusuna](../reference/nuget-exe-cli-reference.md) bakın

- **Clıdotnet.exe**: bağımsız değişkenini kullanarak tam yayın öncesi sürümü belirtin `-v` . [DotNet paket başvurusu Ekle](/dotnet/core/tools/dotnet-add-package)' ye başvurun.

<a name="native-cpp-packages"></a>

### <a name="native-c-packages"></a>Yerel C++ paketleri

NuGet, Visual Studio 'da C++ projelerinde kullanılabilmesi için yerel C++ paketlerini destekler. Bu, projeler için **NuGet Paketlerini Yönet** bağlam-menü komutunu sağlar, bir `native` hedef çerçeve sunar ve MSBuild tümleştirmesi sağlar.

[NuGet.org](https://www.nuget.org/packages)üzerindeki yerel paketleri bulmak için kullanarak arama yapın `tag:native` . Bu tür paketler genellikle `.targets` ve `.props` dosyalarını sağlar ve paket bir projeye eklendiğinde otomatik olarak NuGet içeri aktarır.

## <a name="evaluating-packages"></a>Paketler değerlendiriliyor

Bir paketin kullanışlılığını değerlendirmek için en iyi yol, bunu indirmek ve kodunuzda denemek (nuget.org üzerindeki tüm paketler düzenli olarak virüsler için taranır). Her ne kadar popüler olan her paket, kendisini kullanan birkaç geliştirici ile başlatılır ve ilk benimseyenlerden biri olabilirsiniz!

Aynı zamanda, bir NuGet paketinin kullanılması, bunun sağlam ve güvenilir olduğundan emin olmak için buna bir bağımlılık alınması anlamına gelir. Bir paketin yüklenmesi ve doğrudan sınanması zaman alıcı olduğundan, bir paketin liste sayfasındaki bilgileri kullanarak bir paketin kalitesi hakkında çok fazla bilgi edinebilirsiniz:

- **İndirmeler istatistikleri**: NuGet.org üzerindeki paket sayfasında, **İstatistikler** bölümünde Toplam indirme, en son sürüm indirmeleri ve günde ortalama indirme işlemleri gösterilir. Daha büyük sayılar, diğer birçok geliştiricinin pakete bağımlılığı olduğunu, yani kendini kanıtlamış olduğunu gösterir.

    ![Bir paketin listeleme sayfasına istatistik yükleme](media/Finding-03-Downloads.png)

- **Kullanan**: Paket sayfasında **, bölümünde en** popüler 5 NuGet.org paketi ve bu pakete bağımlı olan popüler GitHub depoları listelenir. Bu pakete bağımlı paketlere ve depoya bu paketin "bağımlıları" adı verilir. Bağımlı paketler ve depolar bu paketin "onaylama" olarak görülebilir, çünkü paket yazarları güvenmeyi ve buna bağımlı olur.
  - Bağımlı bir paket, bu paketin *en son kalıcı listelenen sürümünde* *herhangi bir sürümüne* bağlı olmalıdır. Bu tanım, görüntülenen bağımlı paketlerin, güvenilir ve bu pakete bağımlı olan paket yazarının güncel bir yansıması olmasını sağlar. Ön sürüm bağımlılıkları henüz tam olarak düşünülmemiş olduklarından listelenmez. Örnekler için aşağıdaki tabloya bakın:

    | Sürümleri paketleyin | A paketi B paketi 'ne bağlı olarak listelendi mi? |
    |-|-|
    | v 1.0.0<br>v 1.1.0 (en son kararlı)--> Paket B<br>v 1.2.0-Önizleme | DOĞRU, en son kararlı sürüm B paketine bağlıdır |
    | v 1.0.0--> paketi B<br>v 1.1.0 (en son kararlı)<br>v 1.2.0-Önizleme | YANLıŞ, en son kararlı sürüm B paketine bağlı değildir |
    | v 1.0.0--> paketi B<br>v 1.1.0 (en son kararlı)<br>v 1.2.0-Preview--> Paket B | YANLıŞ, en son kararlı sürüm B paketine bağlı değildir |

  - GitHub deposunun yıldız sayısı genellikle bu deponun GitHub kullanıcılarıyla ne kadar popüler olduğunu gösterir (daha fazla yıldız genellikle daha popüler anlamına gelir). GitHub 'ın yıldızı ve depo derecelendirme sistemi hakkında daha fazla bilgi için lütfen [GitHub 'ın başlangıç sayfasını](https://help.github.com/en/github/getting-started-with-github/saving-repositories-with-stars#about-stars) ziyaret edin.

    ![Kullanan](media/Used-By-section-Humanizer.png)

    > [!Note]
    > Bölüm tarafından kullanılan bir paket, tek tek depoların insan tarafından incelenmesi gerekmeden otomatik olarak oluşturulur ve yalnızca NuGet.org paketlerini ve pakete bağlı olan popüler GitHub depolarını göstermek için bilgilendirme amaçlıdır.

- **Sürüm geçmişi**: Paket sayfasında, en son güncelleştirme tarihi için **bilgi** ' yi arayın ve **sürüm geçmişini** inceleyin. İyi tutulan bir pakette, son güncelleştirmeler ve zengin bir sürüm geçmişi bulunur. İhmal edilen paketlerin birkaç güncelleştirmesi vardır ve genellikle bir süre güncelleştirilmemiş demektir.

    ![Paketin listeleme sayfasında sürüm geçmişi](media/Finding-04-VersionHistory.png)

- **Son yüklemeler**: Paket sayfasında **İstatistikler** altında, **tam istatistikleri görüntüle**' yi seçin. Tüm İstatistikler sayfasında, paketin sürüm numarasına göre son altı haftaya göre yüklemesi gösterilmektedir. Diğer geliştiricilerin etkin şekilde kullandığı bir paket, genellikle daha iyi bir seçenektir.

- **Destek**: Yazar **' ın altındaki** paket sayfasında, yazarın sağladığı destek seçeneklerini görmek için **Proje sitesi** ' ni (varsa) seçin. Adanmış bir siteye sahip bir proje genellikle daha iyi desteklenir.

- **Geliştirici geçmişi**: **sahipler** altındaki paket sayfasında, yayımladıkları diğer paketleri görmek için bir sahip seçin. Birden çok pakete sahip olanlar, işlerini daha sonra desteklemeye devam edememe olasılığı yüksektir.

- **Açık kaynak katkıları**: birçok paket açık kaynaklı depolarda tutulur ve bunlar, geliştiricilerin doğrudan hata düzeltmeleri ve özellik iyileştirmeleri katkıda bulunmasına olanak tanır. Belirli bir paketin katkı geçmişi Ayrıca, kaç geliştirici etkin bir şekilde dahil olduğu konusunda iyi bir göstergedir.

- **Sahipleri** arayın: yeni geliştiriciler, sizin için harika paketler oluşturmaya tamamen eşit bir şekilde kararlıdır ve bu kullanıcılara NuGet ekosistemine yeni bir şey getirmenin bir şansı vermek iyi olabilir. Bu göz önünde bulundurularak, liste sayfasında **bilgi** altında **kişi sahipleri** ' nı kullanarak doğrudan paket geliştiricilerine ulaşın. Olasılığınızı karşılamak için sizinle birlikte çalışmak iyi olacaktır!

- **Ayrılmış paket kimliği önekleri**: için çok sayıda paket sahibi uygulandı ve [ayrılmış bir paket kimliği öneki](../nuget-org/id-prefix-reservation.md)verdi. [NuGet.org](https://www.nuget.org/)veya Visual Studio 'daki BIR paket kimliğinin yanındaki görsel onay işaretini gördüğünüzde, bu, paket sahibinin kimlik ön eki ayırma [ölçütlerimizi](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria) karşıladığı anlamına gelir. Bu, paket sahibinin kendilerini ve paketini tanımlamaya açık olduğu anlamına gelir.

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
1. `.nuspec`Bu klasörün kökünde olacak dosyayı açın.
1. Şöyle bir etiketi olmalıdır `<license type="file">license\license.txt</license>` . Bu, lisans dosyasının adlandırıldığını `license.txt` ve bu `license` klasörün kökünde de olacak adlı bir klasörün içinde olduğunu gösterir.
1. `license`Klasöre gidin ve `license.txt` dosyayı açın.

İçinde lisansı ayarlamaya yönelik MSBuild eşdeğeri için `.nuspec` [Lisans ifadesi veya lisans dosyası paketleme](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file)konusuna göz atın.

## <a name="search-syntax"></a>Arama söz dizimi

NuGet paket araması, NuGet CLı ve Visual Studio 'daki NuGet Paket Yöneticisi uzantısı içindeki nuget.org üzerinde aynı şekilde çalışmaktadır. Genel olarak, arama anahtar sözcüklere ve paket açıklamalarına uygulanır.

- **Filtreleme**: `<property>:<term>` `<property>` (büyük/küçük harf duyarsız),,,,,,, `id` `packageid` `version` `title` `tags` `author` `description` `summary` ve `owner` gibi bir söz dizimini kullanarak belirli bir özelliğe arama terimi uygulayabilirsiniz. Aynı anda birden çok özellik arayabilirsiniz. Özelliğindeki aramalar alt `id` Dize eşleşmelerinde, ancak `packageid` `owner` tam büyük/küçük harf duyarsız eşleşme kullanır. Örnekler:

```
PackageId:jquery             # Match the package ID in an exact, case-insensitive manner

owner:microsoft              # Match the owner in an exact, case-insensitive manner

id:NuGet.Core                # Match any part of the ID property
Id:"Nuget.Core"
ID:jQuery
id:jquery id:ui              # Search for multiple terms in the ID
id:jquery tags:validation    # Search multiple properties

invalid:jquery ui            # Unsupported properties are ignored, so this
                             # is the same as searching on ui
```
