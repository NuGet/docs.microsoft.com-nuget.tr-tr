---
title: "NuGet nedir ve ne işe yarar? | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/10/2018
ms.topic: hero-article
ms.prod: nuget
ms.technology: 
description: "Hangi NuGet kapsamlı bir giriş olduğunu ve yapar"
keywords: "NuGet Paket Yöneticisi, tüketim, paket oluşturma paketini barındırma"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e670fa6174f8dc9954ef9eebc06f61e84112117d
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2018
---
# <a name="an-introduction-to-nuget"></a>NuGet giriş

Tüm modern geliştirme platformu için temel bir aracı üzerinden geliştiriciler oluşturabilir, paylaşmak ve yararlı kod tüketen bir mekanizmadır. Genellikle "(dll) olarak derlenmiş kod bu paketleri tüketen projelerinde gereken diğer içeriği ile birlikte içeren paketler" içine kodun paketlenebilir.

.NET için kod paylaşmak için Microsoft tarafından desteklenen mekanizmasıdır **NuGet**, hangi nasıl paketleri .NET oluşturulur için barındırılan ve tüketilen tanımlar ve bu rollerin her birine araçlar sağlar.

Basitçe, bir NuGet paketi ile tek bir ZIP dosyası olan `.nupkg` derlenmiş kod (DLL'ler), bu kod, ilgili diğer dosyaları içeren uzantısı ve paketin sürüm numarası gibi bilgileri içeren bir açıklayıcı bildirimi. Kod paylaşmak için geliştiricilere paketleri oluşturmak ve bunları ortak veya özel bir ana bilgisayara yayımlayın. Paket tüketicileri bu paketleri uygun ana bilgisayarlardan edinmek, kendi projelerine ekleme ve ardından bir paketin işlevselliği ve proje kodunu çağırın. NuGet kendisini ardından Ara ayrıntıları işler.

NuGet ortak nuget.org konak yanında özel konaklar desteklediğinden, bir kuruluş veya bir çalışma grubu için özel kod paylaşmak için NuGet paketlerini kullanabilirsiniz. Kendi kodunuzu kullanılmak üzere kendi projeleri ancak hiçbir şey faktörü için kullanışlı bir yol olarak NuGet paketlerini de kullanabilirsiniz. Kısacası, bir NuGet paketi kodu paylaşılabilir birimidir ancak değil gerektirir ve paylaşımı belirli anlamına gelir gelmez.

## <a name="the-flow-of-packages-between-creators-hosts-and-consumers"></a>Oluşturucular, konakları ve tüketicileri arasında paketlerin akışı

Ortak bir konak olarak kendi rolünde NuGet kendisini merkezi bir depoya 100.000 benzersiz paketlerin tutar [nuget.org](https://www.nuget.org). Bu paketleri .NET geliştiricilerinin milyonlarca tarafından her gün görevli olduğu. NuGet ayrıca sağlar, özel olarak bulutta paketlerini barındıracak (gibi Visual Studio Team Services), özel bir ağda veya hatta yalnızca, yerel dosya sisteminde. Bunu yaparak, bu paketleri paketler belirli bir tüketici grubu için kullanılabilir hale getirme olanağı veren, ana bilgisayar erişimi geliştiricilerin kullanımına sunulur. Seçenekleri üzerinde açıklanacak [kendi NuGet akışlarını barındıran](Hosting-Packages/Overview.md). Yapılandırma seçenekleri ile tam olarak hangi ana bilgisayarların herhangi belirli bir bilgisayar tarafından böylece paketler nuget.org gibi genel bir depo yerine belirli kaynaklar elde edilen sağlar erişilebilir denetleyebilirsiniz.

Her bir ana bilgisayar doğası işlevi görür paket arasında bir bağlantı noktası *oluşturucuları* ve paket *tüketicileri*. Oluşturucuları yararlı NuGet paketlerini oluşturmak ve bunları bir konağa yayımlayın. Tüketiciler kullanışlı ve uyumlu paketleri karşıdan yükleniyor ve bunların projelerde bu paketleri de dahil olmak üzere erişilebilir konaklarda arayın. Bir projeye yüklendiğinde paketleri API'leri proje kodunu geri kalanı için kullanılabilir.

![Paket oluşturucuları, paket konakları ve paket tüketicileri arasındaki ilişki](media/nuget-roles.png)

## <a name="package-targeting-compatibility"></a>Paket uyumluluk hedefleme

"Uyumlu" bir paket kaybı projenin hedef çerçevesi ile uyumlu olan en az bir hedef .NET framework için oluşturulmuş derlemeler içerdiği anlamına gelir. Geliştiriciler, UWP denetimleriyle gibi bir framework belirli paketleri oluşturabilir veya hedefleri daha geniş ölçüdeki destekleyebilir. Bir paketin uyumluluk, geliştiricilerin hedef en üst düzeye çıkarmak için [.NET standart](/dotnet/standard/net-standard), hangi tüm .NET projeleri kullanmasını sağlayabilirsiniz. (Genellikle tek bir derleme içeren) tek bir paket için tüm süren projeleri çalışırken bu oluşturucuları ve tüketicileri için en verimli anlamına gelir.

.NET standart dışında API'leri gerektiren paket geliştiriciler diğer taraftan, bunlar destekler ve bu derlemelerin tümünü (hangi "çoklu sürüm desteği" olarak adlandırılır) aynı pakete dahil etmek istediğiniz farklı hedef çerçeve için ayrı derlemeler oluşturun. Bir tüketici böyle bir paketi yüklendiğinde, NuGet proje tarafından gerekli olan derlemeleri ayıklar. Bu paketin ayak izini son uygulamada en aza indirir ve/veya derlemeleri proje tarafından üretilen. Çoklu sürüm desteği paketi IF kuşkusuz oluşturana korumak daha zordur.

> [!Note]
> .NET standardını hedefleyen çeşitli "taşınabilir sınıf kitaplığı" kullanarak önceki yaklaşım yerini alır (PCL) hedefler. Bu belge, bu nedenle paketleri için standart .NET oluşturma odaklanır.

## <a name="nuget-tools"></a>NuGet araçları

Destek barındırma yanı sıra, NuGet ayrıca çeşitli oluşturucuları ve tüketicileri tarafından kullanılan araçları sağlar:

| Aracı | Platformlar | İlgili senaryolar | Açıklama |
| --- | --- | --- | --- |
| [nuget.exe CLI](Tools/nuget-exe-CLI-Reference.md) | Tümü | Oluşturma, tüketim | Özellikle bazı yalnızca tüketicileri için uygulama paketi oluşturucuları uygulayarak bazı komutlar tüm NuGet yetenekleri sağlar ve diğerleri hem de uygulama. Örneğin, oluşturucuları kullanma paketini `nuget pack` çeşitli derlemeler ve ilişkili dosyaları bir paket oluşturmak için tüketiciler kullanım paketini komutu `nuget install` proje klasörünü ve herkesin paketleri dahil için kullanır `nuget config` NuGet yapılandırmayı ayarlamak için değişkenleri. Bir platform belirsiz aracı olarak NuGet CLI Visual Studio projeleri ile etkileşime girmez. |
| [dotnet CLI](Tools/dotnet-Commands.md) | Tümü | Oluşturma, tüketim | Bazı NuGet CLI doğrudan .NET Core araç zinciri içinde özellikleri sağlar. NuGet CLI olduğu gibi CLI dotnet Visual Studio projeleri ile etkileşime girmez. |
| [Paket Yöneticisi Konsolu](Tools/Package-Manager-Console.md) | Visual Studio Windows | Tüketim | Sağlar [PowerShell komutlarını](Tools/Powershell-Reference.md) yükleme ve Visual Studio projelerinde paketlerini yönetme. |
| [Paket Yöneticisi UI](Tools/Package-Manager-UI.md) | Visual Studio Windows | Tüketim | Yükleme ve Visual Studio projelerinde paketlerini yönetme için kullanımı kolay kullanıcı Arabirimi sağlar. |
| [NuGet UI yönetme](/visualstudio/mac/nuget-walkthrough) | Mac için Visual Studio | Tüketim | Yükleme ve yönetme Mac projeler için paketler Visual Studio için kullanımı kolay kullanıcı Arabirimi sağlar. |
| [MSBuild](Schema/msbuild-targets.md) | Windows | Oluşturma, tüketim | Paketleri oluşturma ve MSBuild araç zinciri aracılığıyla doğrudan projesinde kullanılan paketleri geri yükleme yeteneği sağlar. |

Gördüğünüz gibi birlikte çalıştığınız NuGet araçları, oluşturma, kullanma veya paketler ve üzerinde çalıştığınız platforma yayımlama üzerinde önemli ölçüde bağlıdır. Diğer NuGet paketlerde mevcut işlevselliği üstünde oluştururken paket oluşturucuları genellikle ayrıca tüketicileri değildir. Ve bu paketleri doğal olarak, sırayla hala diğerlerine bağlı.

Daha fazla bilgi için başlayın [paket oluşturma iş akışı](Create-Packages/Overview-and-Workflow.md) ve [paket tüketimi iş akışı](Consume-Packages/Overview-and-Workflow.md) makaleleri.

## <a name="managing-dependencies"></a>Bağımlılıkları yönetme

Diğer iş üzerinde kolayca oluşturma yeteneği paket yönetim sistemi en güçlü özelliklerden biridir. Buna göre NuGet yaptığı çoğunu bu bağımlılığı ağacı veya bir proje adına "Grafik" yönetiyor. Kısaca, size yalnızca kendiniz bir proje ile doğrudan kullanıyorsanız bu paketleri ile ilgili. Bu paketleri (hangi sırayla hala başkalarının tüketebileceği) diğer paketleri kullanılmasına neden varsa, NuGet bu tüm alt düzey bağımlılıkları mvc'deki.

Aşağıdaki resimde sırayla birkaç diğer bağımlı beş paketleri bağımlı bir proje gösterir.

![Bir .NET projesi için bir örnek NuGet bağımlılık grafiği](media/dependency-graph.png)

Bazı paketler bağımlılık grafikte birden çok kez görüntülendiğine dikkat edin. Örneğin, paket B üç farklı tüketicileri vardır ve her bir tüketici (gösterilmez) Bu paket için farklı bir sürüm belirtmiş olabilir. Yaygın olarak kullanılan paketler için özellikle bir ortak olay budur. NuGet Paket B hangi sürümünün tüm tüketicilere tam olarak karşılayan belirlemek için sabit tüm iş Neyse yapar. NuGet sonra nasıl olursa olsun tüm diğer paketleri, aynı derin bağımlılık grafiğinin yapar.

Bu hizmet NuGet nasıl gerçekleştireceğini ile ilgili daha fazla ayrıntı için bkz: [bağımlılık çözümlemesi](Consume-Packages/Dependency-Resolution.md).

## <a name="tracking-references-and-restoring-packages"></a>İzleme başvuruları ve paketleri geri yükleniyor

Projeleri kaynak denetimi depoları, geliştirici bilgisayarlar arasında kolayca geçiş yapabilirsiniz çünkü sunucuları oluşturun ve diğerleri onu ikili derlemelerden NuGet paketleri doğrudan bir projeye bağlı tutmak için yüksek oranda zordur. Bunun yapılması bu gereksiz yere bloated proje her kopyasını (ve dolayısıyla kaynak denetimi depoları alanı boşa harcanmasına). Ayrıca, çok projeyi tüm kopyalarını arasında uygulanacak güncelleştirmeleri yaptığınız gibi daha yeni sürümlerle paket ikili dosyaları güncelleştirmek zorlaştıran.

NuGet, bunun yerine bir proje, en üst düzey ve alt düzey bağımlılıkları bağlı olan paketlerin basit başvuru listesini tutar. Her bir paket bir projeye bazı ana bilgisayardan yüklediğinizde, diğer bir deyişle, NuGet paket tanımlayıcısı ve sürüm numarası referans listesindeki kaydeder. (Bir paket kaldırma doğal olarak, listeden kaldırır.) NuGet açıklandığı gibi istek üzerine tüm başvurulmuş paketlerini geri yüklemek için bir yol ardından sağlar [paket geri yüklemesi](Consume-Packages/Package-Restore.md).

![NuGet başvuru listesini paket yüklemesinde oluşturulur ve başka bir yerde paketlerini geri yüklemek için kullanılabilir](media/nuget-restore.png)

Yalnızca başvuru listesi ile NuGet daha sonra yeniden yükleyebilirsiniz&mdash;diğer bir deyişle, *geri*&mdash;tüm ortak ve/veya özel konakları sonraki bir zamanda bu paketlerin. Kaynak denetimi veya diğer herhangi bir yolla paylaşımı için bir proje yürüten yaptığınızda, yalnızca başvuru listesi içerir ve herhangi bir paket ikili hariç tutmak (bkz [paketler ve kaynak denetimi](Consume-Packages/Packages-and-Source-Control.md).)

Bir otomatik dağıtım sisteminin bir parçası proje bir kopyasını alma bir yapı sunucusu gibi bir proje alan bilgisayar yalnızca bunlar gerekli olduğunda bağımlılıkları geri yüklemek için NuGet sorar. Visual Studio Team Services "NuGet geri yükleme" adımları tam bu amaçla sağlamak gibi sistemler oluşturabilir. Benzer şekilde, ne zaman geliştiriciler elde proje bir kopyasını (olarak depo kopyalarken) gibi bir komutu çağırabileceği `nuget restore` (NuGet CLI) `dotnet restore` (dotnet CLI) veya `Install-Package` tüm gerekli bir paketi de almak için (Paket Yöneticisi Konsolu). Kendi bölümü için Visual Studio Proje oluşturulurken paketleri otomatik olarak geri yükler.

Açıkçası, daha sonra geliştiriciler ilgilenen nerede NuGet birincil rolü projenizin adına başvuru listeleyen Bakımı ve sağlayarak bu başvurulan bir paket verimli bir şekilde geri yükleme (ve güncelleştirmek için) anlamına gelir. Bu liste, iki birinde tutulur *paket Yönetimi biçimleri*adlı gibi:

- [`packages.config`](Schema/packages-config.md): *(NuGet 1.0 +)* projesinde, diğer bağımlılıklar dahil olmak üzere tüm bağımlılıkları düz bir listesini tutar bir XML dosyası yüklü paketler.
- [PackageReference](Consume-Packages/Package-References-in-Project-Files.md) (veya "paketini proje dosyalarını başvurularında") | *(NuGet 4.0 +)* ayrı bir dosya gerektiği şekilde bir projenin en üst düzey bağımlılıkları doğrudan proje dosyası listesini tutar. İlişkili bir dosya `project.assets.json`, genel bağımlılık grafiğinin yönetmek için dinamik olarak oluşturulur.

Hangi paket Yönetimi biçimi herhangi belirli bir projede işe proje türü ve kullanılabilir bir NuGet (ve/veya Visual Studio) sürümü bağlıdır. Hangi biçimi kullanılan denetlemek için yalnızca Ara `packages.config` ilk paketinizi yükledikten sonra proje kök. Bu dosyayı yapmazsanız, doğrudan için proje dosyası bakın bir &lt;PackageReference&gt;öğesi.

## <a name="what-else-does-nuget-do"></a>Else NuGet ne yapar?

Şu ana kadar olan NuGet aşağıdaki özelliklere öğrendiniz:
- NuGet özel barındırma için Destek Merkezi nuget.org deposuyla sağlar.
- NuGet araçları geliştiriciler oluşturma, yayımlama ve paketleri kullanma için gereken sağlar.
- En önemlisi, NuGet paketleri geri yükleyin ve bu listeden bu paketleri güncelleştirmek için kullanılan bir proje ve özelliği başvuru listesini tutar.

Verimli çalışmak bu işlemleri yapmak için bazı Perde Arkası iyileştirmeleri NuGet yapar. Özellikle, her iki bilgisayar genelinde NuGet yönetir ve kısayol yükleme ve yeniden projeye özgü paketi önbelleğe alır. Bilgisayar genelinde önbellek söz konusu olduğu yerlerdeki başka bir projede aynı paket yükleme başka bir yükleme tabi değil gibi bir proje ile yükleyip herhangi bir paket önbellekte depolanır. Çok sayıda paketleri, sık sık geri yüklerken bu gibi bir derleme sunucusundaki açıkça çok yararlıdır. Mekanizması ve nasıl çalışacağınız hakkında daha fazla bilgi için bkz: [NuGet önbelleği yönetme](Consume-Packages/Managing-the-Nuget-Cache.md).

Tek bir proje içinde tekrar aynı paketin farklı sürümleri için birden çok başvuru çözme içeren genel bağımlılık grafiğinin NuGet yönetir. Bir proje kendilerini aynı bağımlılıklara sahip bir veya daha fazla paket üzerinde bir bağımlılık alır oldukça yaygındır. Bazı nuget.org en yararlı yardımcı programı paketleri tarafından birçok diğer paketleri görevli olduğu. Tüm bağımlılık grafiğinde daha sonra kolayca on farklı başvuruları aynı paketin farklı sürümlerine sahip olabilir. Bu paket birden fazla sürümünü uygulamasına getiren önlemek için hangi tek sürüm tüm tüketiciler tarafından kullanılabilir çıkışı NuGet sıralar. (Daha fazla bilgi için bkz: [bağımlılık çözümlemesi](Consume-Packages/Dependency-Resolution.md).)

Bunun ötesinde, NuGet paketleri nasıl yapılandırıldığı için ilgili tüm belirtimleri tutar (de dahil olmak üzere [yerelleştirme](Create-Packages/Creating-Localized-Packages.md) ve [hata ayıklama simgeleri](Create-Packages/Symbol-Packages.md)) ve nasıl başvurulan (de dahil olmak üzere [ Sürüm aralıkları](reference/package-versioning.md#version-ranges-and-wildcards) ve [yayın öncesi sürümleri](create-packages/Prerelease-Packages.md).) NuGet Ayrıca kendi hizmetleriyle program aracılığıyla çalışma için çeşitli API'ler sağlar ve Visual Studio uzantıları ve proje şablonları yazma geliştiriciler için destek sağlar.

Bu belge için içindekiler göz atmak için bir dakikanızı ayırın ve tüm bu özellikler, sürüm notları geri NuGet beginnings dating birlikte temsil görürsünüz.

## <a name="comments-contributions-and-issues"></a>Açıklamalar, katkı ve sorunları

Son olarak, biz çok açıklamaları ve bu belgelerine katkıda Hoş Geldiniz&mdash;yalnızca select **geri bildirim** ve **Düzenle** herhangi bir üst kısmında komutları sayfa veya ziyaret [belgeleri Depo](https://github.com/NuGet/docs.microsoft.com-nuget/) ve [belgeleri sorun listesi](https://github.com/NuGet/docs.microsoft.com-nuget/issues) github'da.

Biz de NuGet kendisini Katkıları Hoş Geldiniz aracılığıyla kendi [çeşitli GitHub depolarının](https://github.com/NuGet/Home); NuGet sorunları bulunabilir [https://github.com/NuGet/home/issues](https://github.com/NuGet/home/issues).

NuGet deneyiminizi keyfini çıkarın!
