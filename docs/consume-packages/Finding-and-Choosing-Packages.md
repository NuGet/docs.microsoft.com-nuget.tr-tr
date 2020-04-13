---
title: NuGet Paketlerini Bulma ve Seçme
description: NuGet arama sözdizimi ayrıntıları da dahil olmak üzere bir proje için en iyi NuGet paketlerini nasıl bulabileceğinize ve seçeceğinizhakkında genel bir bakış.
author: karann-msft
ms.author: karann
ms.date: 06/04/2018
ms.topic: conceptual
ms.openlocfilehash: 9f427005251bc2bf7a8a79285e39b4bd49062dbf
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428858"
---
# <a name="finding-and-evaluating-nuget-packages-for-your-project"></a>Projeniz için NuGet paketlerini bulma ve değerlendirme

Herhangi bir .NET projesini başlatırken veya uygulamanız veya hizmetiniz için işlevsel bir gereksinimi tanımladığınızda, bu ihtiyacı karşılayan mevcut NuGet paketlerini kullanarak kendinize çok fazla zaman ve sorun dan tasarruf edebilirsiniz. Bu paketler [nuget.org](https://www.nuget.org/packages/)veya kuruluşunuz veya başka bir üçüncü taraf tarafından sağlanan özel bir kaynaktan genel koleksiyondan gelebilir.

## <a name="finding-packages"></a>Paketleri bulma

Visual Studio'da nuget.org ziyaret ettiğinizde veya Paket Yöneticisi UI'yi açtığınızda, toplam indirmelere göre sıralanmış paketlerin bir listesini görürsünüz. Bu, milyonlarca .NET projesinde en çok kullanılan paketleri hemen gösterir. O halde, ilk birkaç sayfada listelenen paketlerden en azından bazılarının projelerinizde yararlı olma olasılığı yüksektir.

![En popüler paketleri gösteren nuget.org/packages varsayılan görünümü](media/Finding-01-Popularity.png)

Sayfanın sağ üst kısmında **ki ön sürüm** seçeneğine dikkat edin. Seçildiğinde, nuget.org beta ve diğer erken sürümler de dahil olmak üzere paketlerin tüm sürümlerini gösterir. Yalnızca kararlı bir şekilde serbest bırakıldığını göstermek için seçeneği temizleyin.

Belirli ihtiyaçlar için etiketlere göre arama (Visual Studio Package Manager içinde veya nuget.org gibi bir portalda) uygun bir paketi keşfetmenin en yaygın yoludur. Örneğin, "json" üzerinde arama, bu anahtar kelimeyle etiketlenen ve böylece JSON veri biçimiyle bazı ilişkileri olan tüm NuGet paketlerini listeler.

![nuget.org'da 'json' arama sonuçları](media/Finding-02-SearchResults.png)

İsterseniz paket kimliğini kullanarak da arama yapabilirsiniz. Aşağıdaki [Arama Sözdizimine](#search-syntax) bakın.

Şu anda, arama sonuçları yalnızca alaka düzeyine göre sıralanır, bu nedenle genellikle gereksinimlerinize uygun paketler için sonuçların en az ilk birkaç sayfasını gözden geçirmek veya arama terimlerinizi daha spesifik olması için hassaslaştırmak istersiniz.

### <a name="does-the-package-support-my-projects-target-framework"></a>Paket projemin hedef çerçevesini destekliyor mu?

NuGet, yalnızca bu paketin desteklenen çerçeveleri projenin hedef çerçevesini içeriyorsa, bir paketi projeye yükler. Paket uyumlu değilse, NuGet bir hata sorunu yayınlar.

Bazı paketler desteklenen çerçeveleri doğrudan nuget.org galerisinde listelemektedir, ancak bu tür veriler gerekli olmadığından, birçok paket bu listeyi içermez. Şu anda belirli bir hedef çerçeveyi destekleyen paketler için nuget.org arama yapmak için hiçbir yol yoktur (özellik göz önünde bulunduruluyor, [Bkz. NuGet Issue 2936).](https://github.com/NuGet/NuGetGallery/issues/2936)

Neyse ki, desteklenen çerçeveleri diğer iki yolla belirleyebilirsiniz:

1. NuGet Paket Yöneticisi Konsolu'ndaki komutu [`Install-Package`](../reference/ps-reference/ps-ref-install-package.md) kullanarak bir projeye paket yüklemeyi dene. Paket uyumsuzsa, bu komut paketin desteklenen çerçevelerini gösterir.

1. **Info**altında **Manuel indirme** bağlantısını kullanarak nuget.org kendi sayfasından paketi indirin. Uzantıyı `.nupkg` 'dan ' a `.zip`değiştirin ve `lib` klasörünün içeriğini incelemek için dosyayı açın. Burada, desteklenen çerçevelerin her biri için, her alt klasörün hedef çerçeve takma adıyla adlandırıldığı alt klasörleri görürsünüz (TFM; bkz. [Hedef Çerçeveler).](../reference/target-frameworks.md) Altında `lib` hiçbir alt klasör ve yalnızca tek bir DLL görürseniz, uyumluluğunu keşfetmek için paketi projenize yüklemeyi denemeniz gerekir.

## <a name="pre-release-packages"></a>Ön sürüm paketleri

Birçok paket yazarı, iyileştirmeler yapmaya ve en son revizyonları hakkında geri bildirim almaya devam ederken önizleme ve beta sürümlerini kullanıma sunar.

Varsayılan olarak, nuget.org arama sonuçlarında ön sürüm paketleri gösterir. Yalnızca kararlı sürümlerde arama yapmak için, sayfanın sağ üst kısmındaki **ön sürüm ekle** seçeneğini temizleyin

![nuget.org'ye yayın öncesi onay kutusu ekleme](media/Finding-06-include-prerelease.png)

Visual Studio'da ve NuGet ve dotnet CLI araçlarını kullanırken, NuGet varsayılan olarak ön sürüm sürümlerini içermez. Bu davranışı değiştirmek için aşağıdaki adımları yapın:

- **Visual Studio'da Paket Yöneticisi UI**: **NuGet Paketlerini** Yönet'te, **Ön Sürüm Kutusunu Dahil'i** ayarlayın. Bu kutuyu ayarlamak veya temizlemek, Paket Yöneticisi Arabirimi'ni ve yükleyebileceğiniz kullanılabilir sürümlerin listesini yeniler.

    ![Visual Studio'ya yayın öncesi onay kutusu ekle](media/Prerelease_02-CheckPrerelease.png)

- **Paket Yöneticisi Konsolu** `-IncludePrerelease` : `Find-Package`Anahtarı `Get-Package` `Install-Package`, `Sync-Package`, `Update-Package` , ve komutlarla kullanın. [PowerShell Referans](../reference/powershell-reference.md)bakın.

- **nuget.exe CLI**: `-prerelease` Anahtarı `install`, `update` `delete`, `mirror` , ve komutlarla kullanın. [NuGet CLI referansına](../reference/nuget-exe-cli-reference.md) bakın

- **dotnet.exe CLI**: Bağımsız değişkeni kullanarak `-v` tam ön sürüm sürümünü belirtin. [Dotnet ekle paket başvurusuna](/dotnet/core/tools/dotnet-add-package)bakın.

<a name="native-cpp-packages"></a>

### <a name="native-c-packages"></a>Yerli C++ paketleri

NuGet, Visual Studio'daki C++ projelerinde kullanılabilecek yerel C++ paketlerini destekler. Bu, projeler için **NuGet Paketlerini Yönet** bağlam menüsü `native` komutunu etkinleştiri, bir hedef çerçevesi sunar ve MSBuild tümleştirmesi sağlar.

[nuget.org'da](https://www.nuget.org/packages)yerel paketleri bulmak `tag:native`için, kullanarak arama yapın. Bu tür paketler `.targets` `.props` genellikle, paket projeye eklendiğinde NuGet'in otomatik olarak içe aktettiği dosyaları sağlar ve sağlar.

## <a name="evaluating-packages"></a>Paketleri değerlendirme

Bir paketin kullanışlılığını değerlendirmenin en iyi yolu paketi indirmek ve kodunuzda denemektir (nuget.org tüm paketler bu arada, virüsler için rutin olarak taranır). Sonuçta, her son derece popüler paket sadece birkaç geliştiriciler kullanarak başladı ve erken benimseyenlerden biri olabilir!

Aynı zamanda, NuGet paketini kullanmak, pakete bağımlı olmak anlamına gelir, bu nedenle paketin sağlam ve güvenilir olduğundan emin olmak istersiniz. Bir paketi yüklemek ve doğrudan test etmek zaman aldığından, paketin listeleme sayfasındaki bilgileri kullanarak paketin kalitesi hakkında çok şey öğrenebilirsiniz:

- *İndirme istatistikleri*: nuget.org'daki paket sayfasında, **İstatistikler** bölümünde toplam indirme, en son sürümün indirmeleri ve günlük ortalama indirmeler gösterilmektedir. Daha büyük sayılar, diğer birçok geliştiricinin pakete bağımlı olduğunu gösterir, bu da kendisinin kendini kanıtladığı anlamına gelir.

    ![Bir paketin listeleme sayfasındaki istatistikleri indirme](media/Finding-03-Downloads.png)

- *GitHub Kullanımı*: paket **sayfasında, GitHub Kullanımı** bölümünde, bu pakete bağlı olan ve GitHub'da çok sayıda yıldıza sahip herkese açık GitHub depolarını listeler. GitHub deposunun yıldız sayısı genellikle deponun GitHub kullanıcıları için ne kadar popüler olduğunu gösterir (daha fazla yıldız genellikle daha popüler anlamına gelir). GitHub'ın yıldızı ve depo sıralama sistemi hakkında daha fazla bilgi için lütfen [GitHub'ın Başlangıç Sayfasına](https://help.github.com/en/github/getting-started-with-github/saving-repositories-with-stars#about-stars) gidin.

    ![GitHub Kullanımı](media/GitHub-Usage.png)

    > [!Note]
    > Bir paketin GitHub Kullanımı bölümü, tek tek depoların insan tarafından incelenmesi olmaksızın ve yalnızca pakete dayanan ve GitHub kullanıcıları arasında popüler olan GitHub depolarını göstermek için yalnızca bilgilendirme amacıyla otomatik olarak oluşturulur.

- *Sürüm geçmişi*: paket sayfasında, en son güncelleştirme tarihi için **Bilgi** altına bakın ve **Sürüm Geçmişini**inceleyin. Bakımlı bir paketin son güncelleştirmeleri ve zengin bir sürüm geçmişi vardır. İhmal edilen paketlerde birkaç güncelleştirme var ve genellikle bir süredir güncelleştirilememiş.

    ![Paketin giriş sayfasındasürüm geçmişi](media/Finding-04-VersionHistory.png)

- *Son yüklemeler*: **İstatistikler**altındaki paket sayfasında, **tam istatistikleri görüntüle'yi**seçin. Tam istatistikler sayfası, paketin son altı hafta içinde sürüm numarasına göre yüklenmesini gösterir. Diğer geliştiricilerin etkin olarak kullandığı bir paket genellikle olmayan paketten daha iyi bir seçimdir.

- *Destek*: **Bilgi**altındaki paket sayfasında, yazarın hangi destek seçeneklerini sağladığını görmek için **Proje Sitesi'ni** (varsa) seçin. Özel bir siteye sahip bir proje genellikle daha iyi desteklenir.

- *Geliştirici geçmişi*: **Sahipleri**altında paket sayfasında, onlar yayınlanan diğer paketleri görmek için bir sahibi seçin. Birden fazla paketi olanlar gelecekte işlerini desteklemeye devam etme olasılığı daha yüksektir.

- *Açık kaynak katkıları*: birçok paket açık kaynak depolarında muhafaza edilir ve bu da onlara bağlı geliştiricilerin hata düzeltmelerine ve özellik iyileştirmelerine doğrudan katkıda bulunmalarını mümkün kılar. Belirli bir paketin katkı geçmişi, aynı zamanda kaç geliştiricinin etkin olarak yer aldığının iyi bir göstergesidir.

- *Röportaj sahipleri*: yeni geliştiriciler kesinlikle eşit kullanmak için büyük paketler üreten kararlı olabilir, ve onları NuGet ekosistemiçin yeni bir şey getirmek için bir şans vermek için iyi. Bunu göz önünde bulundurarak, giriş sayfasındaki **Bilgi** altındaki **İletişim Sahipleri** seçeneği aracılığıyla doğrudan paket geliştiricilere ulaşın. Büyük olasılıkla, onlar ihtiyaçlarınıza hizmet etmek için sizinle çalışmak için mutlu olacak!

- *Ayrılmış Paket Kimliği Önekleri*: Birçok paket sahibi başvuruda bulunmuş ve [ayrılmış paket kimliği öneki](../nuget-org/id-prefix-reservation.md)verilmiştir. [nuget.org](https://www.nuget.org/)veya Visual Studio'da bir paket kimliğinin yanında görsel onay işaretini gördüğünüzde, paket sahibinin kimlik öneki rezervasyonu [için ölçütlerimizi](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria) karşıladığını görürsünüz. Bu, paket sahibinin kendilerini ve paketlerini tanımlama konusunda açık olduğu anlamına gelir.

> [!Note]
> nuget.org'da bir paketin giriş sayfasında **Lisans Bilgilerini** seçerek görebileceğiniz bir paketin lisans koşullarına her zaman dikkat edin. Bir paket lisans koşullarını belirtmiyorsa, paket sayfasındaki **İlgili Kişi sahipleri** bağlantısını kullanarak doğrudan paket sahibine başvurun. Microsoft, üçüncü taraf paket sağlayıcılardan size herhangi bir fikri mülkiyet lisansı vermez ve üçüncü taraflarca sağlanan bilgilerden sorumlu değildir.

## <a name="license-url-deprecation"></a>Lisans URL amortismanı
[LisansUrl'den](../reference/nuspec.md#licenseurl) [lisansa](../reference/nuspec.md#license)geçiş yaptığımızda, bazı NuGet istemcileri ve NuGet akışları henüz bazı durumlarda lisans bilgilerini yüzeye çıkaramayabilir. Geriye dönük uyumluluğu korumak için, lisans URL'si bu gibi durumlarda lisans bilgilerinin nasıl alınılabildiğini anlatan bu belgeye işaret edin.

Bir paketin lisans URL'sine tıkladığınızda, paketin bir lisans dosyası içerdiği ve
* Yeni lisans bilgilerini istemciye nasıl yorumlayıp yüzleyeceğini henüz bilmeyen bir akışa bağlısınız **veya**
* Akış veya tarafından sağlanan yeni lisans bilgilerini nasıl yorumlayacağınızda niçin ve **OR** okumayı henüz bilmeyen bir istemci kullanıyorsunuz
* Her ikisinin birleşimi

Paketin içindeki lisans dosyasında yer alan bilgileri şu şekilde okuyabilirsiniz:
1. NuGet paketini indirin ve içeriğini bir klasöre çekin.
1. Bu `.nuspec` klasörün kökünde olacak dosyayı açın.
1. Gibi bir etiketi `<license type="file">license\license.txt</license>`olmalı. Bu, lisans dosyasının `license.txt` adının verildiği anlamına `license` gelir ve bu klasörün kökünde de olacak bir klasörün içindedir.
1. Klasöre `license` gidin ve `license.txt` dosyayı açın.

MSBuild lisans ayarı eşdeğer için `.nuspec`, bir [lisans ifadesi veya bir lisans dosyası ambalaj](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file)bir göz atın.

## <a name="search-syntax"></a>Sözdizimini Ara

NuGet paket araması nuget.org'da, NuGet CLI'den ve Visual Studio'daki NuGet Paket Yöneticisi uzantısında aynı şekilde çalışır. Genel olarak, arama anahtar kelimelere ve paket açıklamalarına uygulanır.

- **Filtreleme**: Sözdizimi `<property>:<term>` kullanarak belirli bir özelliğe `<property>` arama terimi uygulayabilirsiniz. `id` `packageid` `version` `title` `tags` `author` `description` `summary` `owner` Aynı anda birden çok özelliği arayabilirsiniz. `id` Özellik teki aramalar substring eşleşmeleridir, oysa `packageid` kesin, büyük/küçük harf duyarsız bir eşleşme `owner` kullanır. Örnekler:

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
