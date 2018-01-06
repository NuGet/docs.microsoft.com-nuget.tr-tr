---
title: "NuGet nedir ve ne işe yarar? | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/26/2017
ms.topic: hero-article
ms.prod: nuget
ms.technology: 
ms.assetid: c3faf278-4cbf-4733-96f6-9ee9f7203af9
description: "Hangi NuGet kapsamlı bir giriş olduğunu ve yapar"
keywords: "NuGet Paket Yöneticisi, tüketim, paket oluşturma paketini barındırma"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2bc6a9e154df287fee6a7e00cc1349dfa2100643
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/05/2018
---
# <a name="an-introduction-to-nuget"></a>NuGet giriş

Tüm modern geliştirme platformu için temel bir aracı üzerinden geliştiriciler oluşturabilir, paylaşmak ve yararlı kod tüketen bir mekanizmadır. Genellikle "(dll) olarak derlenmiş kod bu paketleri tüketen projelerinde gereken diğer içeriği ile birlikte içeren paketler" içine kodun paketlenebilir.

.NET için kod paylaşım mekanizmasıdır **NuGet**, hangi nasıl paketleri .NET oluşturulur için barındırılan ve tüketilen tanımlar ve bu rollerin her birine araçlar sağlar. 

Basitçe, bir NuGet paketi ile tek bir ZIP dosyası olan `.nupkg` derlenmiş kod (DLL'ler), bu kod, ilgili diğer dosyaları içeren uzantısı ve paketin sürüm numarası gibi bilgileri içeren bir açıklayıcı bildirimi. Kitaplık geliştiriciler paket dosyalarını oluşturmak ve bunları bir konağa yayımlayın. Paket tüketicileri bu paketleri almak, kendi projelerine ekleme ve ardından kitaplığın işlevselliği ve proje kodunu çağırın. NuGet kendisini ardından Ara ayrıntıları işler.

## <a name="the-flow-of-packages-between-creators-hosts-and-consumers"></a>Oluşturucular, konakları ve tüketicileri arasında paketlerin akışı

Ana bilgisayar olarak kendi rolünde NuGet kendisini üstünde 60.000 benzersiz, genel kullanıma paketlerin merkezi bir depoya tutar [nuget.org](https://www.nuget.org). Bu paketleri .NET geliştiricilerinin milyonlarca tarafından her gün görevli olduğu. NuGet paketlerini barındıracak özel olarak bulutta, özel bir ağda veya hatta yalnızca, yerel dosya sisteminde sağlar. Bunu yaparak, bu paketler yalnızca belirli bir kuruluş ya da müşteri grubundaki geliştiriciler için kullanılabilir. Seçenekleri üzerinde açıklanacak [kendi NuGet akışlarını barındıran](Hosting-Packages/Overview.md).

Ne olursa olsun doğası, bir ana bilgisayar hizmet paketi arasındaki bağlantı noktası olarak *oluşturucuları* ve paket *tüketicileri*. Oluşturucuları yararlı NuGet paketlerini oluşturmak ve bunları bir konağa yayımlayın. Tüketiciler kullanışlı ve uyumlu paketleri karşıdan yükleniyor ve bunların projelerde bu paketleri de dahil olmak üzere erişilebilir konaklarda arayın. Bir projeye yüklendiğinde paketleri API'leri proje kodunu geri kalanı için kullanılabilir.

![Paket oluşturucuları, paket konakları ve paket tüketicileri arasındaki ilişki](media/nuget-roles.png)

Bu durumda "uyumlu" bir paket kaybı projenin hedef çerçevesi ile uyumlu olan en az bir hedef .NET framework için oluşturulmuş derlemeler içerdiği anlamına gelir. Bir paket yaygın uyumlu hale getirmek için oluşturana çeşitli hedef çerçeve için ayrı derlemeler derler ve bunların tümünün aynı pakette içerir. Bir tüketici bu paketi yüklendiğinde, NuGet proje tarafından gerekli olan derlemeleri ayıklar. Bu paketin ayak izini son uygulamada en aza indirir ve/veya derlemeleri proje tarafından üretilen.

## <a name="nuget-tools"></a>NuGet araçları

Destek barındırma yanı sıra, NuGet ayrıca çeşitli oluşturucuları ve tüketicileri tarafından kullanılan araçları sağlar:

| Aracı | Platformlar | İlgili senaryolar | Açıklama |
| --- | --- | --- | --- |
| [nuget.exe CLI](Tools/nuget-exe-CLI-Reference.md) | Tümü | Oluşturma, tüketim | Özellikle bazı yalnızca tüketicileri için uygulama paketi oluşturucuları uygulayarak bazı komutlar tüm NuGet yetenekleri sağlar ve diğerleri hem de uygulama. Örneğin, oluşturucuları kullanma paketini `nuget pack` çeşitli derlemeler ve ilişkili dosyaları bir paket oluşturmak için tüketiciler kullanım paketini komutu `nuget install` bir proje ve herkesin paketleri dahil için kullanır `nuget config` NuGet yapılandırmayı ayarlamak için değişkenleri.  |
| [Paket Yöneticisi UI](Tools/Package-Manager-UI.md) | Visual Studio Windows | Tüketim | Yükleme ve .NET projelerinde paketlerini yönetme için kullanımı kolay kullanıcı Arabirimi sağlar. | 
| [NuGet UI yönetme](/visualstudio/mac/nuget-walkthrough) | Mac için Visual Studio | Tüketim | Yükleme ve .NET projelerinde paketlerini yönetme için kullanımı kolay kullanıcı Arabirimi sağlar. |
| [Paket Yöneticisi Konsolu](Tools/Package-Manager-Console.md) | Visual Studio Windows | Tüketim | Sağlar [PowerShell komutlarını](Tools/Powershell-Reference.md) yükleme ve .NET projelerinde paketlerini yönetme. | 
| [DotNet CLI](Tools/dotnet-Commands.md) | Tümü | Oluşturma, tüketim | Bazı NuGet CLI doğrudan .NET Core zincirinin içinde özellikleri sağlar. |
| [MSBuild](Schema/msbuild-targets.md) | Windows | Oluşturma, tüketim | Paketleri oluşturma ve MSBuild araç zinciri aracılığıyla doğrudan projesinde kullanılan paketleri geri yükleme yeteneği sağlar. |

Gördüğünüz gibi NuGet ile çalıştığınız araçları büyük ölçüde üzerinde bağımlı oluşturma (Yayımlama ve olup olmadığını) paketleri veya bunları ve platformu tüketen üzerinde çalıştığınız. Daha belirli Ayrıntılar bulunabilir [paket oluşturma iş akışı](Create-Packages/Overview-and-Workflow.md) ve [paket tüketimi iş akışı](Consume-Packages/Overview-and-Workflow.md) diğer konular bu bölümlerdeki birlikte Konular. 

Diğer NuGet paketlerde mevcut işlevselliği üstünde oluştururken paket oluşturucuları genellikle ayrıca tüketicileri değildir. Ve bu paketleri doğal olarak, sırayla hala diğerlerine bağlı.

## <a name="managing-dependencies"></a>Bağımlılıkları yönetme

Diğer iş üzerinde kolayca oluşturma yeteneği paket yönetim sistemi kadar güçlü yapan şeylerden biridir. Buna göre NuGet yaptığı çoğunu bu bağımlılığı ağacı veya projenizin adına "Grafik" yönetiyor. Kısaca, size yalnızca kendiniz bir proje ile doğrudan kullanıyorsanız bu paketleri ile ilgili. Bu paketleri (paketleri tüketebileceği) diğer paketler kullanılmasına neden varsa, NuGet bu tüm alt düzey bağımlılıkları mvc'deki.

Aşağıdaki resimde sırayla birkaç diğer bağımlı beş paketleri bağımlı bir proje gösterir.  

![Bir .NET projesi için bir örnek NuGet bağımlılık grafiği](media/dependency-graph.png)

Bazı paketler bağımlılık grafikte birden çok kez görüntülendiğine dikkat edin. Örneğin, paket B üç farklı tüketicileri vardır ve her bir tüketici (gösterilmez) Bu paket için farklı bir sürüm belirtmiş olabilir. Bu sık karşılaştıkları olduğundan, NuGet Paket B hangi sürümünün tüm tüketicilere tam olarak karşılayan belirlemek için sabit tüm iş Neyse yapar. NuGet sonra nasıl derin bağımlılık grafiğinin hale olursa olsun tüm diğer paketler için aynı yapar.

Bu hizmet NuGet nasıl gerçekleştireceğini ile ilgili daha fazla ayrıntı için bkz: [bağımlılık çözümlemesi](Consume-Packages/Dependency-Resolution.md).

## <a name="tracking-references-and-restoring-packages"></a>İzleme başvuruları ve paketleri geri yükleniyor

Projeleri kaynak denetimi depoları, geliştirici bilgisayarlar arasında kolayca geçiş yapabilirsiniz çünkü sunucuları oluşturun ve diğerleri onu ikili derlemelerden NuGet paketleri doğrudan bir projeye bağlı tutmak için yüksek oranda zordur. Yalnızca bunu yap her gereksiz yere bloated projenin kopyalayın (ve dolayısıyla kaynak denetimi depoları alanı boşa harcanmasına), bu da onu çok bu tüm kopyalarını yapılması gerekir gibi daha yeni sürümlerle paket ikili dosyaları güncelleştirmek zorlaştıracak Proje. 

Bunun yerine, NuGet paketleri bağlı bir proje (en üst düzey ve alt düzey bağımlılıklar dahil olmak üzere) bağlıdır ve istek üzerine tüm başvurulan bir paket açıklandığı gibi geri yüklemek için gereken araçları sağlar, başvuru listesini yalnızca korur [paketi geri yükleme](Consume-Packages/Package-Restore.md). Her bir paket bir projeye bazı ana bilgisayardan yüklediğinizde, diğer bir deyişle, NuGet paket tanımlayıcısı ve sürüm numarasını bu başvuru listesinde kaydeder. (Bir paket kaldırma doğal olarak, listeden kaldırır.) 

![NuGet başvuru listesini paket yüklemesinde oluşturulur ve başka bir yerde paketlerini geri yüklemek için kullanılabilir](media/nuget-restore.png)

Yalnızca başvuru listesi ile NuGet daha sonra yeniden yükleyebilirsiniz&mdash;diğer bir deyişle, geri&mdash;tüm ortak ve/veya özel konakları sonraki bir zamanda bu paketlerin. (Bunların gizli rağmen; bu nedenle, nuget.org yayımlanan paketleri kalıcı silinmesini izin verme bkz [paketlerin silinmesi](Policies/deleting-packages.md).) Kaynak denetimi veya diğer herhangi bir yolla paylaşımı için bir proje yürüten yaptığınızda, yalnızca başvuru listesi dahil ve herhangi bir paket ikili içermemesi (bkz [paketler ve kaynak denetimi](Consume-Packages/Packages-and-Source-Control.md).)

Bir otomatik dağıtım sisteminin bir parçası proje bir kopyasını alma bir yapı sunucusu gibi bir proje alan bilgisayar yalnızca bunlar gerekli olduğunda bağımlılıkları geri yüklemek için NuGet sorar. Visual Studio Team Services "NuGet geri yükleme" adımları tam bu amaçla sağlamak gibi sistemler oluşturabilir. Benzer şekilde, ne zaman geliştiriciler elde proje bir kopyasını (gibi bir depo kopyalarken) sonra projeyi Visual Studio'da açın ve bir yapı çalıştırın, Visual Studio otomatik olarak gerekli NuGet paketleri geri yükler. Geliştiriciler ayrıca kullanarak istediğiniz zaman paketlerini geri yüklemek için NuGet söyleyin `nuget restore` CLI komut veya `Install-Package` Paket Yöneticisi konsolunda cmdlet'i.

Açıkçası, daha sonra geliştiriciler ilgilenen nerede NuGet birincil rolü projenizin adına başvuru listeleyen Bakımı ve sağlayarak bu başvurulan bir paket verimli bir şekilde geri yükleme (ve güncelleştirmek için) anlamına gelir.

Bu tam olarak nasıl gerçekleştiğini birkaç içinde kaynaklanan NuGet farklı sürümlerini üzerinden gelişen *paket Yönetimi biçimleri*adlı gibi:

- [`packages.config`](Schema/packages-config.md): *(NuGet 1.0 +)* projesinde, diğer bağımlılıklar dahil olmak üzere tüm bağımlılıkları düz bir listesini tutar bir XML dosyası yüklü paketler. 
- [`project.json`](Schema/project-json.md): *(NuGet 3.0 +)* proje bağımlılıkları ile ilişkili bir dosyası bir genel paket grafiğinde bir listesini tutar bir JSON dosyası `project.lock.json`. Bu yapı üzerinden Gelişmiş performans sağlayan `packages.config` açıklandığı gibi [bağımlılık çözümlemesi](Consume-Packages/Dependency-Resolution.md), geçişli geri yükleme de dahil olmak üzere, ancak kendisi genellikle PackageReference aşağıdaki tarafından değiştirildi.
- [Proje dosyalarını başvurularında paketini](Consume-Packages/Package-References-in-Project-Files.md) (olarak da bilinen "PackageReference") | *(NuGet 4.0 +)* ayrı bir dosya gerektiği şekilde bir projenin en üst düzey bağımlılıkları doğrudan proje dosyası listesini tutar. İlişkili bir dosya `project.assets.json`, gibi dinamik olarak üretilen `project.lock.json` genel bağımlılık grafiğinin yönetmek için.

Hangi paket Yönetimi biçimi herhangi belirli bir projede işe proje türü ve kullanılabilir bir NuGet ve Visual Studio sürümü bağlıdır. Hangi biçimi kullanılan denetlemek için yalnızca Ara `packages.config` veya `project.json` ilk paketinizi yükledikten sonra proje kök. Proje dosyası için doğrudan ya da dosya görmüyorsanız, bakın bir &lt;PackageReference&gt;öğesi.

Visual Studio 2017 ', örneğin, çoğu proje kullanım türleri `packages.config` PackageReference kullanacağınız UWP C# ve .NET Core projeleri dışında. 

## <a name="what-else-does-nuget-do"></a>Else NuGet ne yapar?

Ne biz kadarki kapsamdaki özetlemek için NuGet (kendi barındırma rolünde) merkezi nuget.org deposu sağlar ve özel barındırma destekler. NuGet araçları geliştiriciler oluşturma, yayımlama ve paketleri kullanma için gereken sağlar. Ve en önemlisi, NuGet paketleri geri yükleyin ve bu listeden bu paketleri güncelleştirmek için kullanılan bir proje ve özelliği bir başvuru listesini tutar.

Verimli çalışmak bu işlemleri yapmak için bazı Perde Arkası iyileştirmeleri NuGet yapar. Özellikle, her iki bilgisayar genelinde NuGet yönetir ve kısayol yükleme ve yeniden projeye özgü paketi önbelleğe alır. Burada bilgisayar genelinde önbellek ilgilidir, projede yükleyip herhangi bir paket önbellekte depolanır, yeniden indirmek başka bir projede aynı paket yükleme şekilde sahip değil. Çok sayıda paketleri, sık sık geri yüklerken bu gibi bir derleme sunucusundaki açıkça çok yararlıdır. Mekanizması ve nasıl çalışacağınız hakkında daha fazla bilgi için bkz: [NuGet önbelleği yönetme](Consume-Packages/Managing-the-Nuget-Cache.md).

Tek bir proje içinde çok fazla genel bağımlılık grafiğinin yönetmek için iş NuGet yapar. (Kullanırken `project.json` veya &lt;PackageReference&gt;, NuGet tutar ikincil dosyasındaki bilgileri adlı `project.lock.json` ve `project.assets.json`sırasıyla.) Bu, tekrar aynı paketin farklı sürümleri için birden çok başvuru çözme içerir.

Diğer bir deyişle, bir proje kendilerini aynı bağımlılıklara sahip bir veya daha fazla paket üzerinde bir bağımlılık alır oldukça yaygındır. Örneğin, bazı nuget.org en yararlı yardımcı programı paketleri tarafından birçok diğer paketleri görevli olduğu. Tüm bağımlılık grafiğinin, on, kolayca on farklı ve aynı paketin farklı sürümlerini başvuran. Ancak, NuGet herkes kullanabilir hangi tek sürümü sıralar şekilde, paketin birden fazla sürümünü uygulamanın kendisinden, Getir istemiyorsanız. (Bkz [bağımlılık çözümlemesi](Consume-Packages/Dependency-Resolution.md) Bu konu hakkında daha fazla bilgi için.)

Bunun ötesinde, NuGet paketleri nasıl yapılandırıldığı için ilgili tüm belirtimleri tutar (de dahil olmak üzere [yerelleştirme](Create-Packages/Creating-Localized-Packages.md) ve [hata ayıklama simgeleri](Create-Packages/Symbol-Packages.md)) ve nasıl başvurulan (de dahil olmak üzere [ Sürüm aralıkları](reference/package-versioning.md#version-ranges-and-wildcards) ve [yayın öncesi sürümleri](create-packages/Prerelease-Packages.md).) NuGet de sağlar API'leri için kimlik bilgisi sağlayıcıları (özel konaklarına erişim için) ve Visual Studio uzantıları yazma ve proje şablonlarını geliştiriciler için.

Bu belge için içindekiler göz atmak için bir dakikanızı ayırın ve tüm bu özellikler, sürüm notları geri NuGet beginnings dating birlikte temsil görürsünüz.

## <a name="comments-contributions-and-issues"></a>Açıklamalar, katkı ve sorunları

Son olarak, biz çok açıklamaları ve bu belgelerine katkıda Hoş Geldiniz&mdash;yalnızca select **açıklamaları** ve **Düzenle** komutları herhangi bir sayfa veya ziyaret [belgeleri deposu ](https://github.com/NuGet/docs.microsoft.com-nuget/) ve [belgeleri sorun listesi](https://github.com/NuGet/docs.microsoft.com-nuget/issues) github'da.

Biz de NuGet kendisini Katkıları Hoş Geldiniz aracılığıyla kendi [çeşitli GitHub depolarının](https://github.com/NuGet/Home); NuGet sorunları bulunabilir [https://github.com/NuGet/home/issues](https://github.com/NuGet/home/issues).

NuGet deneyiminizi keyfini çıkarın!
