---
title: NuGet 2,6 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 2,6 sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6b25b9df062afc88466ad107e718f632878debfc
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901427"
---
# <a name="nuget-26-release-notes"></a>NuGet 2,6 sürüm notları

[NuGet 2,5 sürüm notları](../release-notes/nuget-2.5.md)  |  [WebMatrix Için NuGet 2.6.1 sürüm notları](../release-notes/nuget-2.6.1-for-webmatrix.md)

NuGet 2,6, 26 Haziran 2013 tarihinde yayınlanmıştır.

## <a name="notable-features-in-the-release"></a>Yayındaki önemli özellikler

### <a name="support-for-visual-studio-2013"></a>Visual Studio 2013 için destek

NuGet 2,6, Visual Studio 2013 için destek sağlayan ilk sürümdür. Visual Studio 2012 gibi, NuGet Paket Yöneticisi uzantısı, Visual Studio 'nun her sürümünde de bulunur.

Hem Visual Studio 2010 hem de Visual Studio 2012 'yi desteklemeye devam ederken Visual Studio 2013 için en iyi desteği sağlamak ve uzantı boyutlarını mümkün olduğunca küçük tutmak için, özgün uzantı hem Visual Studio 2010 hem de 2012 hedeflemeye devam ederken Visual Studio 2013 için ayrı bir uzantı ürettik.

NuGet 2,6 ' den başlayarak, aşağıdaki gibi iki uzantı yayımlayacağız:

1. [NuGet Paket Yöneticisi](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) (Visual Studio 2010 ve 2012 için geçerlidir)
1. [Visual Studio 2013 için NuGet Paket Yöneticisi](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

Bu bölme ile, [NuGet.org](https://nuget.org) ana sayfasının "NuGet yükleme" düğmesi sizi, farklı NuGet istemcilerinin yüklenmesiyle ilgili daha fazla bilgi bulabileceğiniz [NuGet yükleme](../install-nuget-client-tools.md) sayfasına götürür.

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a>XDT Web.config dönüştürme desteği

NuGet istemcisi için en yüksek düzeyde istenmiş özelliklerden biri, Visual Studio derleme yapılandırma dönüşümlerimizde kullanılan XDT dönüştürme altyapısını kullanarak daha güçlü XML dönüştürmeleri destekliyoruz.

Nisan 2013 ' de, XDT için NuGet desteğiyle ilgili iki büyük duyuru yaptık. İlk olarak XDT kitaplığı 'nın kendisi [bir NuGet paketi olarak yayınlanmakta](https://nuget.org/packages/Microsoft.Web.Xdt) ve [CodePlex üzerinde açık kaynaklandı](http://xdt.codeplex.com/). Bu adım, NuGet istemcisi de dahil olmak üzere diğer açık kaynaklı yazılımlar tarafından serbestçe kullanılmak üzere XDT altyapısını etkinleştirdi. İkinci duyuru, NuGet istemcisinde Dönüşümlere yönelik XDT altyapısının kullanımını desteklemeye yönelik bir plandır. NuGet 2,6, bu tümleştirmeyi içerir.

#### <a name="how-it-works"></a>Nasıl çalışır?

NuGet 'in XDT desteğinin avantajlarından yararlanmak için, mekanizması [geçerli yapılandırma dönüştürme özelliğinden](../create-packages/source-and-config-file-transformations.md)benzer şekilde görünür.
Dönüştürme dosyaları paketin içerik klasörüne eklenir. Ancak, yapılandırma dönüştürmeleri hem yükleme hem de kaldırma için tek bir dosya kullanırken, XDT dönüştürmeleri aşağıdaki dosyaları kullanarak bu işlemlerin her ikisi üzerinde ayrıntılı denetim sağlar:

- Web.config. Install. xdt
- Web.config. Uninstall. xdt

Ayrıca, NuGet, dönüşümler için hangi altyapının çalıştırılacağını belirleyen dosya sonekini kullanır, bu nedenle mevcut web.config kullanan paketler. dönüşümler çalışmaya devam edecektir. XDT dönüştürmeleri Ayrıca herhangi bir XML dosyasına da uygulanabilir (yalnızca web.config değil), bu sayede projenizdeki diğer uygulamalar için bunu kullanabilirsiniz.

#### <a name="what-you-can-do-with-xdt"></a>XDT ile yapabilecekleriniz

XDT 'nin en büyük güçlerinden biri, bir XML DOM yapısını işlemek için [basit ancak güçlü bir sözdizimidir](/previous-versions/aspnet/dd465326(v=vs.110)) . Tek bir sabit belge yapısını başka bir yapıya eklemek yerine, XDT, basit öznitelik adı eşleştirmesinin tam XPath desteğiyle eşleşen öğeler için çeşitli yollarla denetimler sağlar. Eşleşen bir öğe veya öğe kümesi bulunduğunda, XDT öğeleri işlemek için zengin bir işlev kümesi sağlar. Bu, öznitelikleri ekleme, güncelleştirme veya kaldırma, belirli bir konuma yeni bir öğe yerleştirme veya tüm öğeyi ve alt öğelerini değiştirme veya kaldırma anlamına gelir.

### <a name="machine-wide-configuration"></a>Machine-Wide yapılandırması

NuGet 'in harika olan en güçlü yanlarından biri, başka bir şekilde büyük bir yürütülebiliri veya kitaplığı, tümleştirilebilen ve en önemlisi bağımsız olarak korunan ve sürümlü bir dizi modüler bileşene bölmelidir. Bununla birlikte, bunun yan etkisi, bir ürünün veya ürün ailesinin geleneksel fikrini daha fazla parçalanmış hale getiriledir.
NuGet 'in özel paket kaynak özelliği, paketlerin düzenlenmesinin bir yolunu sağlar; Ancak, özel paket kaynakları kendi kendine keşfedilemez.

NuGet 2,6,% ProgramData%/NuGet/configyolundaki klasör hiyerarşisini arayarak NuGet yapılandırma mantığını genişletir. Ürün yükleyicileri, ürünleri için özel bir paket kaynağını kaydetmek üzere bu klasör altına özel NuGet yapılandırma dosyaları ekleyebilir. Ayrıca, klasör yapısı, IDE 'nin ürün, sürüm ve hatta SKU 'SU için semantiğini destekler. Bu dizinlerin ayarları, "son WINS" önceliği stratejisi ile aşağıdaki sırayla uygulanır.

1. %ProgramData%\NuGet\Config \* . config
2. %ProgramData%\NuGet\Config \{ IDE} \* . config
3. %ProgramData%\NuGet\Config \{ IDE} \{ Sürüm} \* . config
4. %ProgramData%\NuGet\Config \{ IDE} \{ Sürüm} \{ SKU} \* . config

Bu listede, {IDE} yer tutucusu, NuGet 'in çalıştığı IDE 'ye özgüdür, bu nedenle Visual Studio 'nun "VisualStudio" olması gerekir. {Version} ve {SKU} yer tutucuları IDE tarafından sağlanır (örneğin, "11,0" ve "WDExpress", "Medexpress" ve "Pro" sırasıyla). Daha sonra klasör birçok farklı *. config dosyası içerebilir.
Bu nedenle, ACME bileşen şirketi ürün yükleyicisindeki bir parçası olarak, yalnızca aşağıdaki dosya yolunu oluşturarak yalnızca Visual Studio 2012 ' in Professional ve Ultimate sürümlerinde görünür olacak özel bir paket kaynağı ekleyebilirsiniz:

% ProgramData% \NuGet\Config\VisualStudio\11.0\Pro\acme.config

Klasör yapısı, yazılım yükleyicileri gibi programların NuGet yapılandırmasına makine genelinde paket kaynakları eklemesine olanak sağlarken, NuGet yapılandırma iletişim kutusu ayrıca paket kaynaklarının kullanıcıya özgü (ör .% AppData%/NuGet/NuGet.Config) veya makine genelinde kaydedilmesine izin verecek şekilde güncelleştirilmiştir.

Bu özellik, bir dosyanın yüklendiği Visual Studio 2013 tarafından kullanılır:

% ProgramData% \NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config

Bu dosya içinde, ".NET Framework paketleri" adlı yeni bir paket kaynağı yapılandırılır.

![NuGet yapılandırma dosyası makine genelindeki ayarlar](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a>Contextualize arama

NuGet Galerisi tarafından sunulan paketlerin sayısı üstel bir hızda büyümeye devam ediyorsa, arama iyileştirmek NuGet öncelik listesinin en üstünde hiç kalır. NuGet 'in planlı özelliklerinden biri bağlamsal aramadır, yani NuGet, kullanmakta olduğunuz Visual Studio sürümü ve SKU 'SU ve olası arama sonuçlarının uygunluğunu belirlemek için ölçüt olarak oluşturmakta olduğunuz proje türü hakkında bilgi kullanacaktır.

NuGet 2,6 ile başlayarak, paket her yüklendiğinde yükleme bağlamı, yükleme işlemi verilerinin bir parçası olarak kaydedilir.  Aramalar Ayrıca, NuGet galerisinin arama sonuçlarını bağlamsal yükleme eğilimlerini ile artışmasına imkan tanıyan bağlam bilgilerini de gönderir.  NuGet galerisine gelecek bir güncelleştirme, bu bağlama duyarlı ilgi düzeyini etkinleştirir.

### <a name="tracking-direct-installs-vs-dependency-installs"></a>Doğrudan yüklemeler ve bağımlılık yüklemeleri izleniyor

Paket yazarları, NuGet galerisinde sunulan [paket istatistikleri](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html) üzerine daha fazla ve daha fazla bağlı.  Yazarların istediği önemli bir eksik veri noktası, doğrudan paket yüklemeleri ve bağımlılık yüklemeleri arasında bir ayrım olur.  Bu aşamada, NuGet istemcisi geliştiricinin doğrudan paketi yükleyip yüklememediği veya bir bağımlılığı karşılamak üzere yüklenmiş olup olmadığı için yükleme işleminin etrafında hiç bağlam göndermedi.
NuGet 2,6 ' den başlayarak, bu veriler artık yükleme işlemi için gönderilir.  NuGet galerisindeki paket Istatistikleri, bu verileri "-Dependency" sonekiyle ayrı bir yük işlemi olarak kullanıma sunar.

* Yükleme
* Install-Dependency
* Güncelleştir
* Update-Dependency
* Yeniden yükleme
* Reinstall-Dependency

Farklı işlem adına ek olarak, bağımlı paket kimliği de yükleme için kaydedilir.  NuGet galerisine gelecek bir güncelleştirme, paket yazarlarının geliştiricilerin paketleri nasıl yüklediğini tamamen anlayabilmesine olanak tanıyan verileri raporlar içinde kullanıma sunacaktır.

## <a name="bug-fixes"></a>Hata Düzeltmeleri

NuGet 2,6 Ayrıca çeşitli hata düzeltmeleri içerir. NuGet 2,6 ' de düzeltilen iş öğelerinin tam listesi için lütfen [Bu sürüm Için NuGet sorun İzleyicisi](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)' ni görüntüleyin.