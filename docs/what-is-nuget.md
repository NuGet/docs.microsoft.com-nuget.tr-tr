---
title: NuGet nedir ve ne işe yarar?
description: NuGet'in ne olduğunu ve ne yaptığına kapsamlı bir giriş
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: overview
ms.openlocfilehash: c326cf184ff20fb798a5770f0a4cf9bf42bed3f5
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "78230700"
---
# <a name="an-introduction-to-nuget"></a>NuGet'e giriş

Herhangi bir modern geliştirme platformu için önemli bir araç, geliştiricilerin yararlı kodlar oluşturabileceği, paylaşabileceği ve tüketebileceği bir mekanizmadır. Bu tür kodlar genellikle derlenmiş kod (DLs olarak) içeren "paketler" ve bu paketleri tüketen projelerde gerekli olan diğer içerikler içine paketlenir.

.NET için (.NET Core dahil), kod paylaşımı için Microsoft tarafından desteklenen mekanizma **NuGet'dir**, .NET paketlerinin nasıl oluşturulduğunu, barındırıldığını ve tüketilmesini tanımlar ve bu rollerin her biri için [araçlar sağlar.](install-nuget-client-tools.md)

Basitçe söylemek gerekirse, NuGet paketi derlenmiş `.nupkg` kod (DLS), bu kodla ilgili diğer dosyaları ve paketin sürüm numarası gibi bilgileri içeren açıklayıcı bir manifesto içeren uzantılı tek bir ZIP dosyasıdır. Paketleri paylaşmak ve bunları ortak veya özel bir ana bilgisayarda yayımlamak için koda sahip geliştiriciler. Paket tüketicileri bu paketleri uygun ana bilgisayarlardan alır, projelerine ekler ve proje kodlarında bir paketin işlevselliğini arar. NuGet kendisi sonra tüm ara ayrıntıları işler.

NuGet, ortak nuget.org ana bilgisayarla birlikte özel ana bilgisayarları desteklediği nden, bir kuruluşa veya çalışma grubuna özel kodu paylaşmak için NuGet paketlerini kullanabilirsiniz. NuGet paketlerini, kendi projelerinizden başka hiçbir şeyde kullanım için kendi kodunuzu hesaba katmanın uygun bir yolu olarak da kullanabilirsiniz. Kısacası, NuGet paketi paylaşılabilir bir kod birimidir, ancak belirli bir paylaşım aracı gerektirmez veya ima etmez.

## <a name="the-flow-of-packages-between-creators-hosts-and-consumers"></a>İçerik oluşturucular, ev sahipleri ve tüketiciler arasındaki paketlerin akışı

Bir kamu ev sahibi olarak rolü, NuGet kendisi [nuget.org](https://www.nuget.org)100.000'den fazla benzersiz paketlerin merkezi deposu tutar. Bu paketler her gün milyonlarca .NET/.NET Core geliştiricisi tarafından kullanılmaktadır. NuGet ayrıca paketleri bulutta (Azure DevOps'lerde gibi) özel olarak barındırmanızı, özel bir ağda veya hatta yalnızca yerel dosya sisteminizde barındırmanızı sağlar. Bunu yaparak, bu paketler yalnızca ana bilgisayara erişimi olan geliştiriciler tarafından kullanılabilir ve böylece paketleri belirli bir tüketici grubu tarafından kullanılabilir hale getirme olanağı sağlar. Seçenekler [kendi NuGet beslemeleri Barındırma](hosting-packages/overview.md)açıklanmıştır. Yapılandırma seçenekleri sayesinde, belirli bir bilgisayar tarafından erişilebilen tam olarak hangi ana bilgisayarların erişebileceğini de kontrol ederek paketlerin nuget.org gibi genel bir depo yerine belirli kaynaklardan elde edilmesini sağlayabilirsiniz.

Doğası ne olursa olsun, bir ev sahibi paket *yaratıcıları* ve paket *tüketiciler*arasında bağlantı noktası olarak hizmet vermektedir. İçerik oluşturucular yararlı NuGet paketleri oluşturur ve bunları bir ana bilgisayarda yayımlar. Tüketiciler daha sonra erişilebilir ana bilgisayarlarda, bu paketleri indirirken ve projelerine dahil ederek kullanışlı ve uyumlu paketleri ararlar. Bir projeye yüklendikten sonra, paketlerin API'leri proje kodunun geri kalanı için kullanılabilir.

![Paket oluşturucular, paket ana bilgisayarlar ve paket tüketicileri arasındaki ilişki](media/nuget-roles.png)

## <a name="package-targeting-compatibility"></a>Paket hedefleme uyumluluğu

"Uyumlu" paket, en az bir hedef .NET çerçevesi için oluşturulmuş ve tüketen projenin hedef çerçevesiyle uyumlu derlemeler içerdiği anlamına gelir. Geliştiriciler, UWP denetimlerde olduğu gibi tek bir çerçeveye özgü paketler oluşturabilir veya daha geniş bir hedef aralığını destekleyebilir. Bir paketin uyumluluğunu en üst düzeye çıkarmak için geliştiriciler, tüm .NET ve .NET Core projelerinin tüketebileceği [.NET Standard'ı](/dotnet/standard/net-standard)hedefler. Bu, tek bir paket (genellikle tek bir derleme içeren) tüm tüketen projeler için çalıştığından, hem içerik oluşturucular hem de tüketiciler için en etkili araçtır.

Diğer taraftan, .NET Standard dışında API'lere ihtiyaç duyan paket geliştiriciler, desteklemek istedikleri farklı hedef çerçeveler için ayrı derlemeler oluşturur ve tüm bu derlemeleri aynı pakete dahil eder (buna "çoklu hedefleme" denir). Bir tüketici böyle bir paket yüklediğinde, NuGet yalnızca projenin ihtiyaç duyduğu derlemeleri ayıklar. Bu, paketin son uygulamadaki ayak izini ve/veya bu proje tarafından üretilen derlemeleri en aza indirir. Çok hedefli bir paket, tabii ki, yaratıcısı için korumak için daha zordur.

> [!Note]
> Hedefleme .NET Standart çeşitli taşınabilir sınıf kitaplığı (PCL) hedefleri kullanarak önceki yaklaşım yerini alır. Bu nedenle bu dokümantasyon .NET Standard için paketler oluşturmaya odaklanır.

## <a name="nuget-tools"></a>NuGet araçları

NuGet, barındırma desteğinin yanı sıra hem içerik oluşturucular hem de tüketiciler tarafından kullanılan çeşitli araçlar da sağlar. Belirli araçları nasıl elde edineceklerine yönelik [NuGet istemci araçlarını yükleme](install-nuget-client-tools.md) konusuna bakın.

| Araç | Platformlar | Uygulanabilir Senaryolar | Açıklama |
| --- | --- | --- | --- |
| [dotnet CLI](consume-packages/install-use-packages-dotnet-cli.md) | Tümü | Oluşturma, Tüketim | .NET Core ve .NET Standart kitaplıkları ve .NET Framework'ü hedefleyen SDK tarzı projeler için CLI aracı (bkz. [SDK özniteliği).](/dotnet/core/tools/csproj#additions) Doğrudan .NET Core takım zinciri içinde belirli NuGet CLI özellikleri sağlar. `nuget.exe` CLI'de olduğu gibi, dotnet CLI Visual Studio projeleri ile etkileşime girmez. |
| [nuget.exe CLI](consume-packages/install-use-packages-nuget-cli.md) | Tümü | Oluşturma, Tüketim | .NET Framework kitaplıkları ve .NET Standart kitaplıklarını hedefleyen SDK tarzı olmayan projeler için CLI aracı. Bazı komutlar özellikle paket oluşturuculara, bazıları yalnızca tüketicilere, bazıları da her ikisine de uygulanırken, tüm NuGet özelliklerini sağlar. Örneğin, paket oluşturucular `nuget pack` komutu çeşitli derlemelerden ve ilgili dosyalardan `nuget install` bir paket oluşturmak için kullanır, `nuget config` paket tüketicilerinin proje klasörüne paketleri eklemek için kullandığı ve herkesin NuGet yapılandırma değişkenlerini ayarlamak için kullandığı. Platform-agnostik bir araç olarak NuGet CLI Visual Studio projeleri ile etkileşime girmez. |
| [Paket Yöneticisi Konsolu](consume-packages/install-use-packages-powershell.md) | Windows'da Görsel Stüdyo | Tüketim | Visual Studio projelerinde paketleri yüklemek ve yönetmek için [PowerShell komutları](reference/Powershell-Reference.md) sağlar. |
| [Paket Yöneticisi UI](consume-packages/install-use-packages-visual-studio.md) | Windows'da Görsel Stüdyo | Tüketim | Visual Studio projelerinde paketleri yüklemek ve yönetmek için kullanımı kolay bir kullanıcı arabirimi sağlar. |
| [NuGet UI'yi yönet](/visualstudio/mac/nuget-walkthrough) | Mac için Visual Studio | Tüketim | Mac projeleri için Visual Studio'da paketleri yüklemek ve yönetmek için kullanımı kolay bir ui sağlayın. |
| [MSBuild](reference/msbuild-targets.md) | Windows | Oluşturma, Tüketim | Doğrudan MSBuild takım zinciri aracılığıyla bir projede kullanılan paketleri oluşturma ve geri yükleme olanağı sağlar. |

Gördüğünüz gibi, birlikte çalıştığınız NuGet araçları büyük ölçüde paketleri oluşturup oluşturmadığınıza, tüketirken veya yayımlarken ve üzerinde çalıştığınız platforma bağlıdır. Paket oluşturucular, diğer NuGet paketlerinde bulunan işlevlerin üzerine inşa ettikleri için genellikle tüketicilerdir. Ve bu paketler, tabii ki, sırayla hala başkalarına bağlı olabilir.

Daha fazla bilgi için [Paket oluşturma iş akışı](create-packages/Overview-and-Workflow.md) ve Paket tüketim iş [akışı](consume-packages/Overview-and-Workflow.md) makaleleriyle başlayın.

## <a name="managing-dependencies"></a>Bağımlılıkları yönetme

Kolayca başkalarının çalışmaları üzerine inşa yeteneği bir paket yönetim sisteminin en güçlü özelliklerinden biridir. Buna göre, NuGet'in yaptığı çoğu şey, bir proje adına bu bağımlılık ağacını veya "grafiği" yönetmektir. Basitçe söylemek gerekirse, sadece doğrudan bir projede kullandığınız bu paketler ile kendinizi endişe gerekir. Bu paketlerden herhangi biri diğer paketleri tüketirse (ki bu da başkalarını tüketebilir), NuGet tüm bu alt düzey bağımlılıklarla ilgilenir.

Aşağıdaki resimde, beş pakete bağlı olan ve sırayla diğer bir dizi pakete bağlı olan bir proje gösterilmektedir.

![Bir .NET projesi için örnek NuGet bağımlılık grafiği](media/dependency-graph.png)

Bağımlılık grafiğinde bazı paketlerin birden çok kez göründüğüne dikkat edin. Örneğin, B paketinin üç farklı tüketicisi vardır ve her tüketici bu paket için farklı bir sürüm de belirtebilir (gösterilmez). Bu, özellikle yaygın olarak kullanılan paketler için sık karşılaşılan bir durumdur. NuGet neyse ki b paketinin tam olarak hangi sürümü tüm tüketicilerin tatmin belirlemek için tüm zor işi yapar. NuGet, bağımlılık grafiği ne kadar derin olursa olsun, diğer tüm paketler için aynı şeyi yapar.

NuGet'in bu hizmeti nasıl gerçekleştirdiği hakkında daha fazla bilgi için [Bağımlılık çözümü'ne](concepts/dependency-resolution.md)bakın.

## <a name="tracking-references-and-restoring-packages"></a>Başvuruları izleme ve paketleri geri alma

Projeler geliştirici bilgisayarlar, kaynak denetim depoları, sunucular oluşturma vb. arasında kolayca taşınabildiği için, NuGet paketlerinin ikili derlemelerini doğrudan bir projeye bağlı tutmak son derece pratik değildir. Bunu yapmak, projenin her bir kopyasını gereksiz yere şişirecek (ve böylece kaynak kontrol depolarında yer atığı). Güncelleştirmelerin projenin tüm kopyalarına uygulanması gerekeceği için paket ikililerini yeni sürümlere güncellemeyi de çok zorlaştırır.

NuGet bunun yerine, hem üst düzey hem de alt düzey bağımlılıklar da dahil olmak üzere, projenin bağlı olduğu paketlerin basit bir başvuru listesini tutar. Diğer bir deyişle, bazı ana bilgisayardan bir paketi projeye yüklediğinizde, NuGet paket tanımlayıcısını ve sürüm numarasını başvuru listesine kaydeder. (Bir paketi kaldırma, tabii ki, listeden kaldırır.) NuGet daha sonra [Paket geri yüklemede](consume-packages/package-restore.md)açıklandığı gibi, istek üzerine başvurulan tüm paketleri geri yüklemek için bir araç sağlar.

![Paket kurulumunda NuGet referans listesi oluşturulur ve paketleri başka bir yerde geri yüklemek için kullanılabilir](media/nuget-restore.png)

NuGet, yalnızca başvuru listesiyle,&mdash;daha sonra tüm bu paketleri daha sonra genel ve/veya özel ana bilgisayarlardan *geri*&mdash;yükleyebilir. Bir projeyi kaynak denetimine taahhüt ederken veya başka bir şekilde paylaşırken, yalnızca başvuru listesini ekler ve paket ikililerini hariç tutarsınız [(Bkz. Paketler ve kaynak denetimi](consume-packages/packages-and-source-control.md).)

Otomatik dağıtım sisteminin bir parçası olarak projenin bir kopyasını alan yapı sunucusu gibi bir proje alan bilgisayar, NuGet'den gerektiğinde bağımlılıkları geri yüklemesini ister. Azure DevOps gibi yapı sistemleri, bu amaç için "NuGet geri yükleme" adımları sağlar. Benzer şekilde, geliştiriciler bir projenin bir kopyasını (bir depoyu klonlarken olduğu gibi) `nuget restore` elde ettiklerinde, `dotnet restore` gerekli tüm paketleri elde `Install-Package` etmek için (NuGet CLI), (dotnet CLI) veya (Package Manager Console) gibi komutları çağırabilirler. Visual Studio, kendi adına, bir proje inşa ederken paketleri otomatik olarak geri yükler [(Paket geri yüklemede](consume-packages/package-restore.md)açıklandığı gibi otomatik geri yükleme etkin olması koşuluyla).

Açıkçası, o zaman, geliştiriciler söz konusu olduğunda NuGet birincil rolü projeniz adına bu referans listesini korumak ve verimli bir şekilde bu başvurulan paketleri geri yüklemek (ve güncelleştirmek) anlamına gelir sağlamaktır. Bu liste, çağrıldıkları gibi iki *paket yönetim biçiminden*birinde tutulur:

- [PackageReference](consume-packages/package-references-in-project-files.md) (veya "proje dosyalarındaki paket başvuruları") | *(NuGet 4.0+)* Projenin üst düzey bağımlılıklarının listesini doğrudan proje dosyası içinde tutar, bu nedenle ayrı bir dosya gerekmez. İlişkili bir `obj/project.assets.json`dosya, bir projenin tüm alt düzey bağımlılıklarla birlikte kullandığı paketlerin genel bağımlılık grafiğini yönetmek için dinamik olarak oluşturulur. PackageReference her zaman .NET Core projeleri tarafından kullanılır.

- [`packages.config`](reference/packages-config.md): *(NuGet 1.0+)* Diğer yüklü paketlerin bağımlılıkları da dahil olmak üzere projedeki tüm bağımlılıkların düz bir listesini tutan bir XML dosyası. Yüklenen veya geri yüklenen paketler bir `packages` klasörde depolanır.

Herhangi bir projede hangi paket yönetim biçiminin kullanılırı proje türüne ve NuGet'in (ve/veya Visual Studio) mevcut sürümüne bağlıdır. Hangi biçimin kullanıldığını kontrol etmek `packages.config` için, ilk paketinizi yükledikten sonra proje kökünde aramanız yeterlidir. Bu dosya yoksa, doğrudan bir \<PackageReference\> öğesi için proje dosyasına bakın.

Bir seçeneğiniz olduğunda PackageReference kullanmanızı öneririz. `packages.config`eski amaçlar için korunur ve artık aktif geliştirme altındadır.

> [!Tip]
> Çeşitli `nuget.exe` CLI komutları, örneğin, `nuget install`paketi otomatik olarak başvuru listesine eklemez. Liste, Visual Studio Package Manager (UI veya Console) ile `dotnet.exe` ve CLI ile bir paket yüklerken güncelleştirilir.

## <a name="what-else-does-nuget-do"></a>NuGet başka ne yapar?

Şimdiye kadar NuGet aşağıdaki özelliklerini öğrendim:

- NuGet, merkezi nuget.org deposunu özel barındırma desteği ile sağlar.
- NuGet, geliştiricilerin paket oluşturma, yayımlama ve tüketim için ihtiyaç duydukları araçları sağlar.
- En önemlisi, NuGet bir projede kullanılan paketlerin bir referans listesini ve bu paketleri bu listeden geri yükleme ve güncelleştirme yeteneğini korur.

Bu işlemlerin verimli bir şekilde çalışmasını sağlamak için, NuGet bazı sahne arkası optimizasyonları yapar. En önemlisi, NuGet kısayol yükleme ve yeniden yükleme için bir paket önbelleği ve küresel paketler klasörü yönetir. Önbellek, makineye zaten yüklenmiş bir paketi karşıdan yükler. Genel paketler klasörü, birden çok projenin aynı yüklü paketi paylaşmasına izin vererek NuGet'in bilgisayardaki genel ayak izini azaltır. Önbellek ve genel paketler klasörü, yapı sunucusunda olduğu gibi sık sık daha fazla sayıda paketi geri geri gönderirken de çok yararlıdır. Bu mekanizmalar hakkında daha fazla bilgi için [bkz.](consume-packages/managing-the-global-packages-and-cache-folders.md)

Tek bir proje de NuGet, yine aynı paketin farklı sürümlerine birden çok başvuruçözmeyi içeren genel bağımlılık grafiğini yönetir. Bir projenin, kendilerinin de aynı bağımlılıklara sahip olduğu bir veya daha fazla pakete bağımlı olması oldukça yaygındır. nuget.org en yararlı yardımcı program paketlerinden bazıları diğer birçok paket tarafından kullanılmaktadır. Tüm bağımlılık grafiğinde, aynı paketin farklı sürümlerine kolayca on farklı başvurunuz olabilir. Bu paketin birden çok sürümünü uygulamanın kendisine getirmemek için NuGet, tüm tüketiciler tarafından hangi tek sürümün kullanılabileceğini sıralar. (Daha fazla bilgi için [bkz.](concepts/dependency-resolution.md)

Bunun ötesinde, NuGet paketlerin nasıl yapılandırıldığı [(yerelleştirme](create-packages/creating-localized-packages.md) ve [hata ayıklama sembolleri](create-packages/symbol-packages-snupkg.md)dahil) ve bunların nasıl [başvurulup başvurulup](consume-packages/package-references-in-project-files.md) başvurulması [(sürüm aralıkları](concepts/package-versioning.md#version-ranges) ve [ön sürüm sürümleri](create-packages/prerelease-packages.md)dahil) ile ilgili tüm özellikleri korur. NuGet ayrıca hizmetleriyle programlı olarak çalışmak için çeşitli API'ler sağlar ve Visual Studio uzantıları ve proje şablonları yazan geliştiriciler için destek sağlar.

Bu belgelerin içindekiler tablosuna göz atmak için bir dakikanızı ayırın ve nuget'in başlangıçlarına kadar uzanan sürüm notları ile birlikte tüm bu özelliklerin orada temsil edildiğini görürsünüz.

## <a name="related-video"></a>İlgili video

> [!Video https://channel9.msdn.com/Series/NuGet-101/What-is-NuGet-1-of-5/player]

[Kanal 9](https://channel9.msdn.com/Series/NuGet-101) ve [YouTube'da](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_)daha fazla NuGet videosu bulun.

## <a name="comments-contributions-and-issues"></a>Yorumlar, katkılar ve sorunlar

Son olarak,&mdash;bu belgelere yapılan yorumları ve katkıları memnuniyetle karşılıyoruz, herhangi bir sayfanın üst kısmındaki Geri **Bildirim** ve **Düzenleme** komutlarını seçin veya GitHub'daki doküman [deposu](https://github.com/NuGet/docs.microsoft.com-nuget/) ve [dokümanlar sorunu listesini](https://github.com/NuGet/docs.microsoft.com-nuget/issues) ziyaret edin.

Ayrıca çeşitli [GitHub depoları](https://github.com/NuGet/Home)aracılığıyla NuGet kendisi için katkıları bekliyoruz; NuGet sorunları bulunabilir. [https://github.com/NuGet/home/issues](https://github.com/NuGet/home/issues)

NuGet deneyiminin tadını çıkarın!
