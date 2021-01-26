---
title: NuGet nedir ve ne yapar?
description: NuGet 'in ne olduğunu ve ne yaptığını kapsamlı bir giriş
author: JonDouglas
ms.author: jodou
ms.date: 05/24/2019
ms.topic: overview
ms.openlocfilehash: 446a1ad4d07d0338a996ad93823ac20386620c0d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780093"
---
# <a name="an-introduction-to-nuget"></a>NuGet 'e giriş

Tüm modern geliştirme platformları için gerekli olan bir araç, geliştiricilerin yararlı kod oluşturma, paylaşma ve kullanma konusunda bir mekanizmadır. Bu tür kodlar genellikle derlenen kodu (dll 'Ler olarak) içeren "paketler" şeklinde paketlenmiştir ve bu paketleri kullanan projelerde gereken diğer içeriklerle birlikte paketlenir.

.NET için (.NET Core dahil), .NET için Microsoft tarafından desteklenen kod paylaşma **mekanizması, .net** için paketlerin oluşturulma, barındırılan ve tüketilen şeklini tanımlar ve bu rollerin her biri için [Araçlar sağlar](install-nuget-client-tools.md) .

Yalnızca bir NuGet paketi, `.nupkg` derlenen kod (dll 'ler), bu kodla ilgili diğer dosyalar ve paketin sürüm numarası gibi bilgileri içeren açıklayıcı bir bildirimle birlikte bulunan uzantıya sahip tek BIR ZIP dosyasıdır. Kod içeren geliştiriciler, paket oluşturma ve bunları herkese açık veya özel bir konakta yayımlamaktır. Paket tüketicileri, bu paketleri uygun konaklardan elde eder, projelerine ekler ve ardından Proje kodlarında bir paketin işlevini çağırır. Ardından NuGet, tüm ara ayrıntıları işler.

NuGet ortak nuget.org ana bilgisayarıyla birlikte özel Konakları desteklediğinden, bir kuruluşa veya bir iş grubuna özel kod paylaşmak için NuGet paketlerini kullanabilirsiniz. NuGet paketlerini aynı zamanda kendi projelerinizi herhangi bir yerde kullanmak üzere kendi kodunuzu çarpanlara katmanın kolay bir yolu olarak da kullanabilirsiniz. Kısaca, bir NuGet paketi paylaşılabilir bir kod birimidir, ancak belirli bir paylaşım yolu gerektirmez veya göstermez.

## <a name="the-flow-of-packages-between-creators-hosts-and-consumers"></a>Oluşturucular, konaklar ve tüketiciler arasındaki paketlerin akışı

Ortak ana bilgisayar rolünde olan NuGet, [NuGet.org](https://www.nuget.org)adresinde 100.000 benzersiz paketin üzerinden merkezi depoyu saklar. Bu paketler, her gün milyonlarca .NET/.NET Core geliştiricisi tarafından işe alınır. NuGet Ayrıca, paketleri bulutta (Azure DevOps gibi), özel bir ağda veya hatta yalnızca yerel dosya sisteminizde barındırmanıza olanak sağlar. Bu şekilde, bu paketler yalnızca konağa erişimi olan geliştiriciler tarafından kullanılabilir ve paketleri belirli bir tüketici grubu için kullanılabilir hale getirme olanağı sunar. Seçenekler [kendi NuGet akışlarınızı barındırırken](hosting-packages/overview.md)açıklanmıştır. Yapılandırma seçenekleri sayesinde, belirli bir bilgisayar tarafından hangi konaklara erişilebileceğini de denetleyebilir ve böylece paketlerin, nuget.org gibi bir genel depo yerine belirli kaynaklardan elde edildiğine emin olabilirsiniz.

Doğası ne olursa olsun, ana bilgisayar paket *oluşturucular* ve paket *tüketicileri* arasındaki bağlantı noktası görevi görür. Creators Build yararlı NuGet paketleri ve bunları bir konakta yayımlayın. Müşteriler daha sonra, bu paketleri projelerinde, indirerek ve dahil olmak üzere erişilebilir konaklarda kullanışlı ve uyumlu paketler arar. Bir projeye yüklendikten sonra paketlerin API 'Leri proje kodunun geri kalanı tarafından kullanılabilir.

![Paket oluşturucular, paket konakları ve paket tüketicileri arasındaki ilişki](media/nuget-roles.png)

## <a name="package-targeting-compatibility"></a>Paket hedefleme uyumluluğu

"Uyumlu" bir paket, en az bir hedef .NET Framework için oluşturulmuş derlemeleri, tüketen projenin hedef çerçevesiyle uyumlu olarak içerir. Geliştiriciler, UWP denetimlerinde olduğu gibi, bir çerçeveye özgü paketler oluşturabilir veya daha geniş bir hedef yelpazesi destekleyebilir. Bir paketin uyumluluğunu en üst düzeye çıkarmak için, geliştiriciler tüm .NET ve .NET Core projelerinin kullanabileceği [.NET Standard](/dotnet/standard/net-standard)hedef alabilir. Bu, tek bir paket (genellikle tek bir derleme içeren) tüm projeler için çalışarak, hem oluşturucular hem de tüketiciler için en verimli yoldur.

.NET Standard dışında API 'Leri gerektiren paket geliştiricileri, diğer yandan, desteklemek istedikleri farklı hedef çerçeveler için ayrı derlemeler oluşturun ve bu derlemelerin tümünü aynı pakette ("Çoklu hedefleme" olarak adlandırılır) dahil eder. Bir tüketici böyle bir paketi yüklediğinde, NuGet yalnızca proje için gereken derlemeleri ayıklar. Bu, paketin, son uygulamada ve/veya bu proje tarafından oluşturulan derlemelerdeki parmak izini en aza indirir. Birden çok hedefleme paketinin, oluşturucusunun bakımını yapmak için daha zordur.

> [!Note]
> .NET Standard hedefleme, çeşitli taşınabilir sınıf kitaplığı (PCL) hedeflerini kullanmanın önceki yaklaşımının yerini alır. Bu belge, .NET Standard için paket oluşturmaya odaklanır.

## <a name="nuget-tools"></a>NuGet araçları

NuGet, barındırma desteğinin yanı sıra hem oluşturucular hem de tüketiciler tarafından kullanılan çeşitli araçlar da sağlar. Bkz. belirli araçları edinme için [NuGet istemci araçları 'Nı yükleme](install-nuget-client-tools.md) .

| Araç | Platformlar | İlgili senaryolar | Açıklama |
| --- | --- | --- | --- |
| [dotnet CLI](consume-packages/install-use-packages-dotnet-cli.md) | Tümü | Oluşturma, tüketim | .NET Core ve .NET Standard kitaplıkları için CLı aracı ve .NET Framework hedefi olan SDK stili projeler için (bkz. [SDK özniteliği](/dotnet/core/tools/csproj#additions)). , Doğrudan .NET Core araç zinciri içinde belirli NuGet CLı özellikleri sağlar. CLI ile birlikte `nuget.exe` DotNet CLI, Visual Studio projeleriyle etkileşime girmiyor. |
| [nuget.exe CLI](consume-packages/install-use-packages-nuget-cli.md) | Tümü | Oluşturma, tüketim | .NET Standard kitaplıklarını hedefleyen .NET Framework kitaplıkları ve SDK olmayan projeler için CLı aracı. Özellikle paket oluşturucuları, bazı ve yalnızca tüketicilere uygulanan ve her ikisine de uygulanan bazı komutlarla, tüm NuGet yeteneklerini sağlar. Örneğin, paket oluşturucuları, `nuget pack` çeşitli derlemelerden ve ilgili dosyalardan bir paket oluşturmak için komutunu kullanır, paket tüketicileri `nuget install` bir proje klasörüne paketleri eklemek için kullanır ve herkes `nuget config` NuGet yapılandırma değişkenlerini ayarlamak için kullanır. Platformdan bağımsız bir araç olan NuGet CLı, Visual Studio projeleriyle etkileşime girmiyor. |
| [Paket Yöneticisi Konsolu](consume-packages/install-use-packages-powershell.md) | Windows üzerinde Visual Studio | Tüketim | Visual Studio projelerindeki paketleri yüklemek ve yönetmek için [PowerShell komutları](reference/Powershell-Reference.md) sağlar. |
| [Paket Yöneticisi UI](consume-packages/install-use-packages-visual-studio.md) | Windows üzerinde Visual Studio | Tüketim | , Visual Studio projelerindeki paketleri yüklemek ve yönetmek için kullanımı kolay bir kullanıcı arabirimi sağlar. |
| [NuGet Kullanıcı arabirimini yönetme](/visualstudio/mac/nuget-walkthrough) | Mac için Visual Studio | Tüketim | Mac için Visual Studio projelerindeki paketleri yüklemek ve yönetmek için kullanımı kolay bir kullanıcı arabirimi sağlar. |
| [MSBuild](reference/msbuild-targets.md) | Windows | Oluşturma, tüketim | Doğrudan MSBuild araç zinciri aracılığıyla bir projede kullanılan paketleri ve geri yükleme paketlerini oluşturma yeteneği sağlar. |

Gördüğünüz gibi, birlikte çalıştığınız NuGet araçları, paketleri oluşturma, kullanma veya yayımlama ve üzerinde çalıştığınız platformu önemli ölçüde temel alır. Paket oluşturucuları, genellikle diğer NuGet paketlerinde bulunan işlevselliğin üzerine inşa ettikleri tüketicilerlerdir. Tabii ki bu paketler yine de diğerleri için de değişebilir.

Daha fazla bilgi için [paket oluşturma iş akışı](create-packages/Overview-and-Workflow.md) ve [paket tüketimi iş akışı](consume-packages/Overview-and-Workflow.md) makaleleriyle başlayın.

## <a name="managing-dependencies"></a>Bağımlılıkları yönetme

Başkalarının çalışmasına kolayca derleme yeteneği, bir paket yönetim sistemi en güçlü özelliklerinden biridir. Buna uygun olarak, NuGet 'in bu bağımlılık ağacını veya bir proje adına "Graph" i yönetdiklediğine benzer. Yalnızca bir projede doğrudan kullandığınız paketlerle sorun olması gerektiğini söyleriz. Bu paketlerin herhangi biri diğer paketleri kullanıyorsa (Bu durumda, hala diğerleri de kullanılabilir), NuGet bu alt düzey bağımlılıklardan yararlanır.

Aşağıdaki görüntüde, beş pakete bağımlı olan bir proje gösterilmektedir ve bu da başka bir sayıya göre değişir.

![.NET projesi için örnek bir NuGet bağımlılığı grafiği](media/dependency-graph.png)

Bazı paketlerin bağımlılık grafiğinde birden çok kez göründüğünü unutmayın. Örneğin, B paketinin üç farklı tüketicisi vardır ve her tüketici bu paket için farklı bir sürüm (gösterilmez) belirtebilir. Bu, özellikle yaygın olarak kullanılan paketler için yaygın bir oluşumdır. NuGet neyse ki, tüm tüketicilere, B paketinin hangi sürümünün tüm müşterileri karşılayıp karşılamadığını tespit etmek için tüm sabit çalışmalarınız. Ardından NuGet, bağımlılık grafiğinin ne kadar derin olduğuna bakılmaksızın diğer tüm paketler için de aynı şekilde yapılır.

NuGet 'in bu hizmeti nasıl gerçekleştirdiği hakkında daha fazla bilgi için bkz. [bağımlılık çözünürlüğü](concepts/dependency-resolution.md).

## <a name="tracking-references-and-restoring-packages"></a>Başvuruları izleme ve paketleri geri yükleme

Projeler geliştirici bilgisayarları, kaynak denetimi depoları, derleme sunucuları ve benzeri kolay bir şekilde hareket edebildiğinden, NuGet paketlerinin ikili derlemelerinin doğrudan bir projeye bağlanmasını sağlamak son derece pratik değildir. Bunu yaptığınızda, projenin her bir kopyasının gereksiz yere eşit hale getirilmiş olması (ve böylece kaynak denetimi depolarında alan olması) sağlanır. Güncelleştirme, projenin tüm kopyalarına uygulanması gerektiği için paket ikililerini daha yeni sürümlere güncelleştirmeyi de zorlaştırır.

Bunun yerine NuGet, üst düzey ve alt düzey bağımlılıklar dahil olmak üzere bir projenin bağımlı olduğu paketlerin basit başvuru listesini tutar. Diğer bir deyişle, bir ana bilgisayardan bir projeye paket yüklediğinizde NuGet, başvuru listesindeki paket tanımlayıcısını ve sürüm numarasını kaydeder. (Bir paket kaldırıldığında, bunu listeden kaldırır.) NuGet daha sonra, [paket geri yükleme](consume-packages/package-restore.md)bölümünde anlatıldığı gibi istek üzerine tüm başvurulan paketleri geri yüklemek için bir yol sağlar.

![Paket yüklemesinde bir NuGet başvuru listesi oluşturulur ve paketleri başka bir yerde geri yüklemek için kullanılabilir](media/nuget-restore.png)

Yalnızca başvuru listesi ile NuGet bunu yeniden yükleyebilir &mdash; , bu paketlerin tümünü daha  &mdash; sonra herkese açık ve/veya özel konaklardan geri yükleyebilir. Kaynak denetimine bir proje kaydederken veya başka bir şekilde paylaşılırken, yalnızca başvuru listesini dahil edersiniz ve paket ikililerini hariç tut (bkz. [paketleri ve kaynak denetimi](consume-packages/packages-and-source-control.md).)

Otomatik dağıtım sisteminin bir parçası olarak projenin bir kopyasını elde eden bir yapı sunucusu gibi bir projeyi alan bilgisayar, her gerektiğinde yalnızca bir NuGet bağımlılıkları geri yüklemeyi ister. Azure DevOps gibi derleme sistemleri, bu tam amaçla "NuGet geri yükleme" adımlarını sağlar. Benzer şekilde, geliştiriciler projenin bir kopyasını edindiklerinde (bir depoyu kopyalarken olduğu gibi), `nuget restore` `dotnet restore` gerekli tüm paketleri elde etmek için (NuGet CLI), (DotNet CLI) veya `Install-Package` (Paket Yöneticisi konsolu) gibi komutları çağırabilir. Visual Studio 'Nun parçası olarak, bir proje oluştururken paketleri otomatik olarak geri yükler ( [paket geri yükleme](consume-packages/package-restore.md)bölümünde açıklandığı gibi otomatik geri yükleme özelliği etkin olur).

Daha sonra, NuGet 'in geliştiricilerin ilgilenmediği birincil rolü, projeniz adına başvuru listesinin saklanması ve bu başvurulan paketleri etkin bir şekilde geri yükleme (ve güncelleştirme) araçlarını sağlamaktır. Bu liste, çağrıldıklarında iki *paket yönetim biçiminden* birinde tutulur:

- [Packagereference](consume-packages/package-references-in-project-files.md) (veya "proje dosyalarında paket başvuruları") | *(NuGet 4.0 +)* Projenin en üst düzey bağımlılıklarının listesini doğrudan proje dosyasında tutar, bu yüzden ayrı bir dosya gerekmez. İlişkili bir dosya, `obj/project.assets.json` bir projenin tüm alt düzey bağımlılıklarla birlikte kullandığı paketlerin genel bağımlılık grafiğini yönetmek için dinamik olarak oluşturulur. PackageReference, her zaman .NET Core projeleri tarafından kullanılır.

- [`packages.config`](reference/packages-config.md): *(NuGet 1.0 +)* diğer yüklü paketlerin bağımlılıkları da dahil olmak üzere, projedeki tüm bağımlılıkların düz bir listesini tutan bir XML dosyası. Yüklenen veya geri yüklenen paketler bir klasörde depolanır `packages` .

Herhangi bir projede hangi paket yönetimi biçiminin çalıştırıldığı, proje türüne ve NuGet (ve/veya Visual Studio) sürümüne bağlıdır. Hangi biçimin kullanıldığını denetlemek için, `packages.config` ilk paketinizi yükledikten sonra proje kökünde öğesine bakmanız yeterlidir. Bu dosyaya sahip değilseniz, proje dosyasında doğrudan bir öğe için bakın \<PackageReference\> .

Bir seçiminiz olduğunda, PackageReference kullanmanızı öneririz. `packages.config` , eski amaçlar için korunur ve artık etkin geliştirme aşamasındadır.

> [!Tip]
> `nuget.exe`Gibi çeşitli CLI komutları, `nuget install` paketi otomatik olarak başvuru listesine eklemez. Bu liste, Visual Studio Paket Yöneticisi (UI veya konsol) ile ve CLI ile bir paket yüklenirken güncelleştirilir `dotnet.exe` .

## <a name="what-else-does-nuget-do"></a>NuGet ne yapmalıyım?

Şu ana kadar NuGet 'in aşağıdaki özelliklerini öğrendiniz:

- NuGet, merkezi nuget.org deposunu özel barındırma desteğiyle sağlar.
- NuGet, geliştiricilerin paket oluşturmak, yayımlamak ve tüketmesi için ihtiyacı olan araçları sağlar.
- En önemlisi, NuGet bir projede kullanılan paketlerin başvuru listesini ve bu paketleri ilgili listeden geri yükleme ve güncelleştirme olanağı sağlar.

Bu işlemlerin verimli bir şekilde çalışmasını sağlamak için NuGet, bazı arka planda iyileştirmeler yapar. En önemlisi, NuGet bir paket önbelleğini ve bir genel paketler klasörünü, kısayol yükleme ve yeniden yükleme için yönetir. Önbellek zaten makinede yüklü olan bir paketin indirilmesini önler. Genel paketler klasörü, birden çok projenin aynı yüklü paketi paylaşmasına olanak tanır ve böylece NuGet 'in bilgisayardaki genel ayak izini azaltır. Önbellek ve genel paketler klasörü, bir yapı sunucusunda olduğu gibi daha fazla sayıda paketi sık geri yüklerken de çok yararlı olur. Bu mekanizmalar hakkında daha fazla bilgi için bkz. [genel paketleri ve önbellek klasörlerini yönetme](consume-packages/managing-the-global-packages-and-cache-folders.md).

Tek bir projede, NuGet genel bağımlılık grafiğini yönetir, bu da aynı paketin farklı sürümlerine birden fazla başvuruyu çözmeyi içerir. Projenin aynı bağımlılıklara sahip bir veya daha fazla pakete bağımlılığı olması oldukça yaygındır. Nuget.org üzerindeki en faydalı yardımcı program paketlerinin bazıları diğer birçok paket tarafından kullanılabilir. Tüm bağımlılık grafiğinde, aynı paketin farklı sürümlerine yönelik olarak kolayca on farklı başvuruya sahip olabilirsiniz. Bu paketin birden çok sürümünün uygulamaya ait olmasını önlemek için, NuGet tüm tüketiciler tarafından hangi tek sürümün kullanılabileceğini sıralar. (Daha fazla bilgi için bkz. [bağımlılık çözünürlüğü](concepts/dependency-resolution.md).)

Bunun ötesinde, NuGet paketlerin nasıl yapılandırıldığı ( [Yerelleştirme](create-packages/creating-localized-packages.md) ve [hata ayıklama sembolleri](create-packages/symbol-packages-snupkg.md)dahil) ve nasıl [başvurulduğu](consume-packages/package-references-in-project-files.md) ( [Sürüm aralıkları](concepts/package-versioning.md#version-ranges) ve [yayın öncesi sürümler](create-packages/prerelease-packages.md)dahil) ile ilgili tüm belirtimleri korur. NuGet Ayrıca, hizmetleriyle birlikte çalışmaya yönelik çeşitli API 'Ler sağlar ve Visual Studio uzantıları ve proje şablonları yazan geliştiriciler için destek sağlar.

Bu belgelerin içindekiler tablosuna göz atabilmeniz için bir dakikanızı ayırın ve bu özellikleri, NuGet 'in Beginnings 'e geri dönme sürüm notlarıyla birlikte görebilirsiniz.

## <a name="related-video"></a>İlgili video

> [!Video https://channel9.msdn.com/Series/NuGet-101/What-is-NuGet-1-of-5/player]

[Channel 9](https://channel9.msdn.com/Series/NuGet-101) ve [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_)'da daha fazla NuGet videoları bulun.

## <a name="comments-contributions-and-issues"></a>Yorumlar, katılımlar ve sorunlar

Son olarak, bu belgelerde çok fazla hoş geldiniz açıklamaları ve katkımız yapmanız &mdash; yeterlidir, her sayfanın üst kısmında **geri bildirim** ve **düzenleme** komutlarını seçin ya da GitHub 'daki [docs Repository](https://github.com/NuGet/docs.microsoft.com-nuget/) ve [docs sorun listesini](https://github.com/NuGet/docs.microsoft.com-nuget/issues) ziyaret edin.

Ayrıca, [çeşitli GitHub depoları](https://github.com/NuGet/Home)aracılığıyla NuGet 'e katkılara katkıda bulunuyoruz; NuGet sorunları üzerinde bulunabilir [https://github.com/NuGet/home/issues](https://github.com/NuGet/home/issues) .

NuGet deneyiminizin keyfini çıkarın!
