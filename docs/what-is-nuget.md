---
title: NuGet nedir ve ne işe yarar?
description: Hangi NuGet kapsamlı bir giriş olduğundan ve mi?
author: karann-msft
ms.author: karann
ms.date: 01/10/2018
ms.topic: overview
ms.openlocfilehash: 0b7105ea5d183d139c8bac915378924ba9c0874a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548825"
---
# <a name="an-introduction-to-nuget"></a>NuGet giriş

Herhangi bir modern geliştirme platformu için gerekli bir araç üzerinden geliştiriciler oluşturabilir, paylaşın ve faydalı kod tüketen bir mekanizmadır. Genellikle bu kod, "(dll) olarak derlenmiş kod birlikte bu paketleri kullanan projelerde gereken diğer içeriği içeren paketleri" olarak sunulur.

(.NET Core dahil), .NET için kod paylaşmak için Microsoft tarafından desteklenen mekanizmadır **NuGet**, nasıl paketleri .NET oluşturulur, barındırılan ve tüketilen tanımlar ve bu rollerin her biriyle için araçlar sağlar.

Basitçe, bir NuGet paketi ile tek bir ZIP dosyasına olan `.nupkg` derlenmiş kodda (DLL'ler), bu kod, ilgili diğer dosyaları içeren bir uzantı ve paketin sürüm numarası gibi bilgileri içeren bir açıklayıcı bildirim. Kod geliştiricilerle paylaşmak için paketler oluşturmak ve bunları genel veya özel bir ana bilgisayara yayımlayın. Paketi tüketicileri bu paketleri, uygun konakları elde, bunları kendi projelerine ekleyin ve ardından Proje kodlarını bir paketin işlevi çağırabilir. NuGet kendisini ardından Ara ayrıntılarını işler.

NuGet genel nuget.org konak yanı sıra özel konaklar desteklediğinden, bir kuruluş veya iş grubu için özel kod paylaşmak için NuGet paketlerini kullanabilirsiniz. NuGet paketlerini, kendi kodunuzu kullanılmak üzere kendi projeleriniz ancak hiçbir şey faktörü için kullanışlı bir yol olarak da kullanabilirsiniz. Kısacası, bir NuGet paketi kodu paylaşılabilir birimidir ancak değil gerektirir veya paylaşım herhangi belirli anlamına gelmez.

## <a name="the-flow-of-packages-between-creators-hosts-and-consumers"></a>Oluşturucular, konaklar ve tüketicileri arasında paketlerin akışı

Ortak bir konak olarak kendi rolünde merkezi depo 100. 000'den benzersiz paket NuGet kendisi tutar [nuget.org](https://www.nuget.org). Bu paketler milyonlarca.NET/.NET Core geliştirici tarafından her gün çalışan. NuGet ayrıca sağlar, özel olarak bulutta paketlerini barındıracak (gibi Visual Studio Team Services üzerinde), özel bir ağda veya hatta yalnızca yerel dosya sisteminize. Bunu yaptığınızda, bu paketleri paketlerini belirli bir tüketici grubu için kullanılabilir hale olanağı sağlayan, konak erişimi geliştiricilerin kullanımına sunulur. Seçenekler üzerinde açıklanmıştır [kendi NuGet akışlarınızı barındırma](hosting-packages/overview.md). Yapılandırma seçenekleri ile tam olarak hangi konakların herhangi belirli bir bilgisayar tarafından böylece paketleri nuget.org gibi ortak bir depoya yerine, belirli kaynakları edinilir sağlama erişilebilir denetleyebilirsiniz.

Her bir konak doğası hizmet paket arasında bir bağlantı noktası olarak *creators* ve paket *tüketiciler*. Creators yararlı NuGet paketleri oluşturun ve bunları bir konağa yayımlayın. Tüketiciler kullanışlı ve uyumlu paketleri indirme ve bu paketleri, projelere dahil etme erişilebilen konaklarda öğesini arayın. Bir projede yüklendikten sonra paketleri API'leri proje kodunu geri kalanı için kullanılabilir.

![Paket oluşturucuları, paket konaklar ve paketi tüketicileri arasındaki ilişki](media/nuget-roles.png)

## <a name="package-targeting-compatibility"></a>Paket uyumluluğu hedefleme

"Uyumlu" bir paket kaybı projenin hedef çerçevesi ile uyumlu olan en az bir hedef .NET framework için oluşturulmuş derlemeler içerdiği anlamına gelir. Geliştiriciler, paketleri olarak UWP denetimleri ile bir çerçevesine özgü oluşturabilir veya geniş bir hedeflerini destekler. Bir paketin uyumluluk, geliştiricilerin hedef en üst düzeye çıkarmak için [.NET Standard](/dotnet/standard/net-standard), hangi tüm .NET ve .NET Core projeleri kullanabilir. Tek bir paket (genellikle tek bir derleme içeren) kullanan tüm projeler için çalıştığı oluşturucuları hem tüketicileri için en verimli yol budur.

.NET Standard dışında API'leri gerektiren paket geliştiriciler, öte yandan, destek ve tüm bu derlemeleri (hangi "multi-targeting'e" olarak adlandırılır) aynı paket içerisine dâhil istedikleri farklı bir hedef çerçeveler için ayrı derlemeler oluşturun. Tüketici bu tür bir paketi yüklendiğinde, proje tarafından gerekli olan derlemeleri NuGet ayıklar. Bu paketin son uygulama yükümlülüğünden en aza indirir ve/veya derlemeleri bu proje tarafından üretilen. Bir çoklu sürüm desteği paketi Elbette oluşturana korumak daha zor olduğu.

> [!Note]
> .NET Standard desteği, çeşitli taşınabilir sınıf kitaplığı (PCL) hedefleri kullanarak önceki yaklaşımına yerini alır. Bu belgeler, bu nedenle .NET Standard için paketleri oluşturmaya odaklıdır.

## <a name="nuget-tools"></a>NuGet araçları

Destek barındırma ek olarak, NuGet çeşitli oluşturucuları ve tüketiciler tarafından kullanılan araçlar da sağlar. Bkz: [yükleme NuGet istemci araçları](install-nuget-client-tools.md) için belirli araçları edinme.

| Aracı | Platformlar | İlgili senaryolar | Açıklama |
| --- | --- | --- | --- |
| [nuget.exe CLI](tools/nuget-exe-cli-reference.md) | Tümü | Oluşturma, tüketim | Özellikle bazı Tüketiciler, yalnızca uygulama paketini creators uygulama bazı komutlarla tüm NuGet yetenekleri sağlar ve diğerleri hem de uygulama. Oluşturucuları kullanma gibi paket `nuget pack` çeşitli derlemeler ve ilişkili dosyaları bir paket oluşturun, tüketicilerin kullanım paket için komutu `nuget install` kullanan bir proje klasörü ve herkesin paketlerini içerecek şekilde `nuget config` NuGet yapılandırmayı ayarlamak için değişkenler. Bir platformdan aracı olarak NuGet CLI'yı Visual Studio projeleri ile etkileşime girmez. |
| [dotnet CLI](tools/dotnet-Commands.md) | Tümü | Oluşturma, tüketim | Belirli NuGet CLI, .NET Core araç zincirinizi içinde doğrudan özellikleri sağlar. NuGet CLI olduğu gibi dotnet CLI Visual Studio projeleri ile etkileşime girmez. |
| [Paket Yöneticisi Konsolu](tools/package-manager-console.md) | Windows üzerinde Visual Studio | Tüketim | Sağlar [PowerShell komutlarını](tools/Powershell-Reference.md) yükleme ve Visual Studio projelerinde paketleri yönetme. |
| [Paket Yöneticisi UI](tools/package-manager-ui.md) | Windows üzerinde Visual Studio | Tüketim | Yükleme ve Visual Studio projelerinde paketler yönetmeye yönelik kullanımı kolay bir kullanıcı Arabirimi sağlar. |
| [NuGet UI'ı yönetme](/visualstudio/mac/nuget-walkthrough) | Mac için Visual Studio | Tüketim | Yükleme ve Mac proje Visual Studio'da paketlerini yönetmek için kullanımı kolay bir kullanıcı Arabirimi sağlar. |
| [MSBuild](reference/msbuild-targets.md) | Windows | Oluşturma, tüketim | MSBuild araç zinciri üzerinden doğrudan projesinde kullanılan paketleri geri yükle ve paketleri oluşturma olanağı sağlar. |

Gördüğünüz gibi birlikte çalıştığınız NuGet araçları, oluşturma, kullanma veya paketler ve üzerinde çalıştığınız platforma yayımlama üzerinde büyük ölçüde bağlıdır. Diğer NuGet paketlerinde var olan işlevselliği üzerine oluşturdukça paket creators genellikle ayrıca tüketicileri olur. Ve bu paketleri, sırayla hala bazılarında bağlı olabilir.

Daha fazla bilgi için başlayan [paket oluşturma iş akışı](create-packages/Overview-and-Workflow.md) ve [paket tüketim iş akışı](consume-packages/Overview-and-Workflow.md) makaleler.

## <a name="managing-dependencies"></a>Bağımlılık Yönetimi

Başkalarının çalışmalarını kolayca oluşturma imkanı bir paket yönetim sistemi en güçlü özelliklerinden biridir. Buna göre NuGet yaptığı çoğunu, bağımlılık ağacı ya da bir proje adına "Grafik" yönetiyor. Kısaca, size yalnızca kendiniz doğrudan bir projede kullanıyorsanız bu paketleri ile ilgili. Bu paketleri birini (bu sırayla hala diğerleri kullanabilir) diğer paketleri kullanma, NuGet bu tüm alt düzey bağımlılıklarını üstlenir.

Aşağıdaki görüntüde, sırayla birkaç diğer bağlı beş paketleri bağımlı bir proje gösterilmektedir.

![Bir .NET projesi için bir örnek NuGet bağımlılık grafiği](media/dependency-graph.png)

Bazı paketler, birden çok kez bağımlılık grafiğinde görüntülendiğine dikkat edin. Örneğin, üç farklı tüketicilerinin Paket B vardır ve her tüketici, paketin (gösterilmemiştir) için farklı bir sürüm de belirtebilir. Bu, özellikle yaygın olarak kullanılan paketler için ortak bir yinelenme zamanıdır. NuGet Paket B hangi sürümünün tüm tüketicilere tam olarak karşılayan belirlemek için tüm zorlu işler Neyse yapar. NuGet sonra nasıl olursa olsun tüm diğer paketleri, aynı ayrıntılı bağımlılık grafiği yapar.

NuGet bu hizmetin performansını daha fazla ayrıntı için bkz: [bağımlılık çözümlemesi](consume-packages/dependency-resolution.md).

## <a name="tracking-references-and-restoring-packages"></a>İzleme başvurularını ve paketler geri yükleniyor

Projeler kaynak denetimi depolarından Geliştirici bilgisayarlar arasında kolayca taşıyabilirsiniz için yapı sunucusu ve diğerleri, NuGet paketlerini doğrudan bir projeye bağlı ikili derlemeleri tutmak oldukça zordur. Bunun yapılması gereksiz yere bloated projeyi her kopyasını (ve böylece kaynak denetim depolarından alanı boşa). Bu ayrıca, güncelleştirmeleri, tüm projenin kopyalarını uygulanacak yaptığınız gibi yeni sürümlere paketi ikili dosyaları güncelleştirmek oldukça zor hale getirir.

NuGet, bunun yerine bir proje, üst düzey ve alt düzey bağımlılıklar dahil olmak üzere bağımlı olduğu paketleri basit başvuru listesini tutar. Bir projeye bazı konaktan bir paketi yüklediğinizde, diğer bir deyişle, NuGet paket tanımlayıcısı ve sürüm numarasını başvuru listesinde kaydeder. (Bir paket kaldırılıyor, listeden kaldırır.) NuGet üzerinde açıklandığı istek, başvurulan tüm paketlerini geri yüklemek için bir yol ardından sağlar [paket geri yükleme](consume-packages/package-restore.md).

![NuGet başvuru listesini paket yüklemesinde oluşturulur ve başka bir yerde paketlerini geri yüklemek için kullanılabilir](media/nuget-restore.png)

Yalnızca başvuru listesi ile NuGet daha sonra yeniden&mdash;diğer bir deyişle, *geri*&mdash;tüm genel ve/veya özel konakları daha sonra dilediğiniz zaman bu paketleri. Bir proje kaynak denetimi veya başka bir şekilde paylaşımı geliştirme yaptığınızda, yalnızca başvuru listesi dahil ve hariç herhangi bir paketi ikili (bkz [paketleri ve kaynak denetimi](consume-packages/packages-and-source-control.md).)

Bir yapı sunucusunda bir otomatik dağıtım sisteminin bir parçası olarak projenin bir kopyasını almak gibi bir proje alan bilgisayar yalnızca ihtiyaç duyulan her bağımlılıkları geri yüklemek için NuGet ister. Visual Studio Team Services "NuGet geri yükleme" adımları tam bu amaçla sağlayan sistemler oluşturabilir. Benzer şekilde, ne zaman geliştiriciler elde bir projenin bir kopyasını (gibi bir depoyu kopyalarken), bunlar gibi komutunu çağırabilirsiniz `nuget restore` (NuGet CLI) `dotnet restore` (dotnet CLI) veya `Install-Package` tüm gerekli paketlerini almak için (Paket Yöneticisi Konsolu). Visual Studio, kendi bölümü için bir proje derlenirken paketleri otomatik olarak yükler (Otomatik geri yükleme etkin, üzerinde açıklandığı olması koşuluyla [paket geri yükleme](consume-packages/package-restore.md)).

NET bir şekilde, daha sonra NuGet'ın birincil role geliştiriciler endişe nerede projenizin adına bu başvuru listesini koruma ve sağlayarak bu başvurulan bir paket verimli bir şekilde geri yükleme (ve güncelleştirmek için) anlamına gelir. Bu liste, iki birinde tutulur *paket Yönetimi biçimleri*adlı gibi:

- [`packages.config`](reference/packages-config.md): *(NuGet 1.0 +)* projedeki diğer bağımlılıklar dahil olmak üzere tüm bağımlılıkları düz bir listesini tutar bir XML dosyası yüklü paketler. Yüklü veya geri yüklenen paketler depolanır bir `packages` klasör.

- [PackageReference](consume-packages/package-references-in-project-files.md) (veya "paket başvuruları proje dosyalarındaki") | *(NuGet 4.0 +)* ayrı bir dosya gerektiği şekilde doğrudan proje dosyası içinde bir projenin üst düzey bağımlılıkların bir listesini tutar. İlişkili bir dosya `obj/project.assets.json`, genel bir bağımlılık grafiği yanı sıra tüm alt düzey bağımlılıkları kullanan bir proje paketlerini yönetmek için dinamik olarak oluşturulur. PackageReference her zaman .NET Core projeleri tarafından kullanılır.

Herhangi bir proje içinde hangi paket Yönetimi biçimi işe proje türü ve sürümünü NuGet (ve/veya Visual Studio) bağlıdır. Hangi biçimde kullanılan denetlemek için yalnızca Ara `packages.config` ilk paketinizi yükledikten sonra proje kökündeki. Bu dosya yoksa, doğrudan proje dosyasında konum bir \<PackageReference\> öğesi.

Bir seçenek varsa PackageReference kullanmanızı öneririz. `packages.config` eski amacıyla korunur ve artık etkin geliştirilme aşamasındadır.

> [!Tip]
> Çeşitli `nuget.exe` gibi CLI komutları `nuget install`, otomatik olarak paket başvurusu listesine eklemeyin. Listeden bir paket ve Visual Studio Paket Yöneticisi ile (kullanıcı Arabirimi veya konsol) ile yüklerken güncelleştirilir `dotnet.exe` CLI.

## <a name="what-else-does-nuget-do"></a>Başka NuGet ne yapar?

Şu ana kadar NuGet aşağıdaki özelliklerini öğrendiniz:

- NuGet, Destek Merkezi nuget.org deposuyla özel barındırma için sağlar.
- NuGet araçları geliştiricilerin oluşturmak, yayımlamak ve paketleri kullanma için gereken sağlar.
- En önemlisi, NuGet paketlerini geri yükleyin ve bu paketleri, listeden güncelleştirmek için bir proje ve özelliği kullanılan başvuru listesini tutar.

Bu işlemlerin verimli bir şekilde çalışmasını sağlamak için NuGet Sahne Arkası bazı iyileştirmeler yapar. En önemlisi, NuGet paket önbelleğini ve genel paketleri klasör kısayol yükleme ve yeniden yönetir. Makinede zaten yüklü bir paket indirme önbelleği önler. Genel packages klasörünü, böylece bilgisayarda NuGet'ın bütün kapladığı alanı azaltmak aynı yüklü paket paylaşımı birden çok proje sağlar. Çok sayıda paketleri, sık geri yüklerken önbellek ve genel paketleri klasör ayrıca gibi bir yapı sunucusunda çok yararlı olur. Bu mekanizmaları hakkında daha fazla bilgi için bkz. [genel paketleri ve önbellek klasörlerini yönetme](consume-packages/managing-the-global-packages-and-cache-folders.md).

Tek bir proje içinde NuGet tekrar birden fazla aynı paketin farklı sürümlerine başvuruları çözümleniyor içeren genel bir bağımlılık grafiği yönetir. Bir proje bir bağımlılık kendileri aynı bağımlılıkları olan bir veya daha fazla paketleri alır oldukça yaygındır. Tarafından birçok diğer paketleri bazı faydalı yardımcı programı paketleri nuget.org üzerinde çalışan. Tüm bağımlılık grafiğinde, daha sonra kolayca on farklı aynı paketin farklı sürümlerine başvuruları olabilir. Bu paket birden çok sürümünü uygulamasına getirmekten kaçının için NuGet tek hangi sürümünün tüm tüketicileri tarafından kullanılan çıkış sıralar. (Daha fazla bilgi için [bağımlılık çözümlemesi](consume-packages/dependency-resolution.md).)

Bundan sonraki miktarlar NuGet paketleri nasıl yapılandırılmıştır için ilgili özellikleri tutar (dahil olmak üzere [yerelleştirme](create-packages/creating-localized-packages.md) ve [hata ayıklama sembolleri](create-packages/symbol-packages.md)) ve nasıl başvurulan (dahil olmak üzere [ Sürüm aralıklarını](reference/package-versioning.md#version-ranges-and-wildcards) ve [yayın öncesi sürümleri](create-packages/prerelease-packages.md).) NuGet Ayrıca kendi Hizmetleri ile program aracılığıyla çalışma için çeşitli API'ler sağlar ve geliştiriciler için Visual Studio uzantıları ve proje şablonları yazma desteği sağlar.

Bu belge için içindekiler tablosunu göz atmak için bir dakikanızı ayırın ve sürüm notları için NuGet beginnings geri ilk yanı sıra, gösterilen bu özelliklerin tümünü görürsünüz.

## <a name="comments-contributions-and-issues"></a>Açıklamalar, Katkıları ve sorunları

Son olarak, bizim için çok büyük oranda yorumlar ve bu belgede yapılan katkılar önemli&mdash;yalnızca select **geri bildirim** ve **Düzenle** herhangi üst kısmındaki komutları sayfasında veya ziyaret [belgeleri Depo](https://github.com/NuGet/docs.microsoft.com-nuget/) ve [docs sorun listesi](https://github.com/NuGet/docs.microsoft.com-nuget/issues) GitHub üzerinde.

Katkılar NuGet'ın kendisi için de bizim için çok önemli aracılığıyla kendi [çeşitli GitHub depoları](https://github.com/NuGet/Home); NuGet sorunları bulunabilir [ https://github.com/NuGet/home/issues ](https://github.com/NuGet/home/issues).

NuGet deneyiminizi keyfini çıkarın!
