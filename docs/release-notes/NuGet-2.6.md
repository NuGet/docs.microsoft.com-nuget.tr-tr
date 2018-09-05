---
title: NuGet 2.6 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr WebMatrix için NuGet 2.6.1 için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f011a8db7ac2067a2ed7db67849d63f7dd40d1ce
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551949"
---
# <a name="nuget-26-release-notes"></a>NuGet 2.6 sürüm notları

[NuGet 2.5 sürüm notları](../release-notes/nuget-2.5.md) | [WebMatrix sürüm notları için NuGet 2.6.1](../release-notes/nuget-2.6.1-for-webmatrix.md)

NuGet 2.6 26 Haziran 2013 tarihinde yayınlanmıştır.

## <a name="notable-features-in-the-release"></a>Sürümündeki önemli özelliklere

### <a name="support-for-visual-studio-2013"></a>Visual Studio 2013 desteği

NuGet 2.6 Visual Studio 2013 için destek sağlayan ilk sürümdür. Ve Visual Studio 2012 gibi NuGet Paket Yöneticisi uzantısını Visual Studio'nun her sürümü dahildir.

Hala Visual Studio 2010 hem Visual Studio 2012 desteği ve uzantı boyutları olabildiğince küçük tutmak sırasında Visual Studio 2013 için en iyi olası desteği sağlamak amacıyla, biz sırasında Visual Studio 2013 için ayrı bir uzantı oluşturduğunu özgün uzantı hem Visual Studio 2010 ve 2012 hedefleyecek şekilde devam eder.

NuGet 2.6 ile başlayarak, aşağıda gösterildiği gibi iki uzantıları yayımlarız:

1. [NuGet Paket Yöneticisi](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) (Visual Studio 2010 ve 2012 için geçerlidir)
1. [Visual Studio 2013 için NuGet Paket Yöneticisi](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

Bu bölme ile [nuget.org](https://nuget.org) giriş sayfasının "Nuget'i Yükle" düğmesine alır, [NuGet yükleme](../install-nuget-client-tools.md) sayfasında, şunları bulabileceğiniz farklı NuGet istemcileri yükleme hakkında daha fazla bilgi.

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a>XDT Web.config dönüşümü desteği

NuGet istemci için en çok istenen özelliklerden biri, Visual Studio derleme yapılandırma dönüşümleri kullanılan XDT dönüştürme motorunu kullanarak daha güçlü XML dönüştürmeleri desteklemek için bırakıldı.

Nisan 2013'te XDT için NuGet desteği ile ilgili iki büyük duyurularını yaptık. XDT kitaplığının kendisi değiştirilirken, ilk kuruluştur [bir NuGet paketi olarak yayımlanan](https://nuget.org/packages/Microsoft.Web.Xdt) ve [açık kaynağı Codeplex'te](http://xdt.codeplex.com/). Bu adım, NuGet istemcisi de dahil olmak üzere diğer açık kaynak yazılım tarafından ücretsiz olarak kullanılacak XDT altyapısı etkin. NuGet istemci dönüşümlerini XDT altyapısı desteklemek için plan ikinci duyuruyu oluştu. NuGet 2.6 Bu tümleştirmeyi içerir.

#### <a name="how-it-works"></a>Nasıl çalışır?

NuGet'ın XDT desteğinden yararlanmak için mekanizması gereksinimlerine aşağıdakine benzer [geçerli yapılandırma dönüşümü özellik](../create-packages/source-and-config-file-transformations.md).
Dönüştürme dosyalar paket içerik klasörüne eklenir. Ancak, yapılandırma dönüşümleri yükleme ve kaldırma için tek bir dosyayı kullanırken aşağıdaki dosyaları kullanarak bu işlemlerin ikisinin üzerinde ayrıntılı denetim XDT dönüşümleri etkinleştir:

- Web.config.install.xdt
- Web.config.uninstall.xdt

Ayrıca, NuGet dosya soneki dönüştürmeleri için mevcut web.config.transforms kullanarak paketleri çalışmaya devam edecek şekilde çalıştırmak için hangi altyapısı belirlemek için kullanır. XDT dönüştürmeleri tüm XML dosyası (yalnızca web.config) için de uygulanabilir şekilde bu projenizde diğer uygulamalar için yararlanabilirsiniz.

#### <a name="what-you-can-do-with-xdt"></a>XDT ile yapabilecekleriniz

XDT'ın en güçlü biri kendi [basit ama güçlü bir söz dizimi](http://msdn.microsoft.com/library/dd465326.aspx) bir XML DOM yapısını düzenlemek için Yalnızca bir sabit belge yapısı üzerine başka bir yapı planlamanızda yerine, çeşitli yollarla, XPath desteği tam basit bir öznitelik adı ile eşleşen öğesinden öğeleri eşleştirmek için XDT denetimleri sağlar. Eşleşen öğe veya öğe kümesini bulunduğunda, ekleme, güncelleştirme veya öznitelikleri kaldırma, belirli bir konumda yeni bir öğe yerleştirme veya değiştirme veya tüm kaldırma anlamına olmadığını XDT zengin işlevleri öğeleri işlemek için sağlar öğe ve alt öğeleri.

### <a name="machine-wide-configuration"></a>Makine genelindeki yapılandırma

NuGet'ın harika gücünü aksi büyük yürütülebilir dosya veya bir dizi bağımsız olarak tümleşik ve en önemlisi tutulan ve tutulan olabilir modüler bileşenleri kitaplığa aşağı keser biridir. Bu, bir yan etkisi, ancak geleneksel amaçlanan bir ürün veya ürün ailesi, büyük olasılıkla parçalandıkça emin olur.
NuGet'ın özel paket kaynağı özelliği paketleri düzenleme bir yol sağlar. Ancak, özel paket kaynaklarını bulunabilir, kendi değildir.

NuGet 2.6 yolu % ProgramData%/NuGet/Config klasör hiyerarşisiyle arayarak NuGet yapılandırma mantığı genişletir. Ürün yükleyicilerini ürünlerini özel paket kaynağını kaydetmek için bu klasör altındaki özel NuGet yapılandırma dosyaları ekleyebilirsiniz. Ayrıca, klasör yapısını semantiği, ürün, sürümü ve hatta SKU IDE'nin destekler. Bu dizinlerden ayarlar ile bir "en son WINS'te" öncelik stratejisi aşağıdaki sırayla uygulanır.

1. %ProgramData%\NuGet\Config\*.config
2. %ProgramData%\NuGet\Config\{IDE}\*.config
3. %ProgramData%\NuGet\Config\{IDE}\{sürüm}\*.config
4. %ProgramData%\NuGet\Config\{IDE}\{sürüm}\{SKU}\*.config

Bu listede, Visual Studio söz konusu olduğunda, "VisualStudio" olacak şekilde {IDE} yer tutucusunu NuGet çalıştığı IDE özeldir. {Version} ve {SKU} yer tutucuları sağlanan IDE tarafından (örn.) "11.0" ve "WDExpress", "VWDExpress" ve "Pro" sırasıyla). Klasör sonra birçok farklı *.config dosyaları içerebilir.
Bu nedenle, bileşen ACME şirket, ürün yükleyicisi bir parçası, şu dosya yolunu oluşturarak yalnızca Professional ve Ultimate sürümleri Visual Studio 2012 ' görünür olacak bir özel paket kaynağı ekleyin olabilir:

%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config

Klasör yapısı gibi yazılım yükleyicileri, makine genelindeki paket kaynaklarını NuGet'ın yapılandırmasına eklemek için programlar için basit olmasını sağlarken, NuGet yapılandırma iletişim kutusu de izin vermek için paket kaynağı olarak kaydını güncelleştirildi (örneğin % AppData%/NuGet/NuGet.Config kayıtlı) ya da kullanıcıya özel ya da makine genelindeki.

Bu özellik, Visual Studio 2013, bir dosya konumunda yüklendiği tarafından kullanılır:

%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config

Bu dosya içinde ".NET Framework paketleri" olarak adlandırılan yeni bir paket kaynağı olarak yapılandırılır.

![NuGet yapılandırma dosyası makine genelinde ayarları](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a>Contextualizing arama

NuGet Galerisi tarafından sunulan paket sayısı bir üstel yükselmeye devam ettikçe aramasını geliştirme NuGet öncelik listenin en üstünde hiç kalır. NuGet için planlanan özelliklerden biri, bağlamsal arama, NuGet sürümü, SKU, kullanmakta olduğunuz VisualStudio ve oluşturmakta olduğunuz proje türü hakkında bilgi olası aramanın ilgi belirlemek için ölçüt olarak kullanacağı anlamına gelir Sonuç.

NuGet 2.6 ile başlayarak, bir paket yüklü olduğu her saat için yükleme bağlamı'nı yükleme işlemi verileri bir parçası olarak kaydedilir.  Arama, arama sonuçlarını bağlamsal yükleme eğilimleri artırmak NuGet galerisinde sağlayacak aynı bağlam bilgilerini de gönderir.  NuGet galerisinde gelecekte yapılacak bir güncelleştirmenin bu içeriğe duyarlı ilgi artırma olanak sağlar.

### <a name="tracking-direct-installs-vs-dependency-installs"></a>İzleme ile doğrudan yükler. Bağımlılık yükler

Paket yazarlarının bağlı olan daha üzerinde [paket istatistikleri](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html) NuGet galerisinde sağlanan.  Yazarlar için istediniz önemli eksik veri noktası doğrudan paketini yükler ve bağımlılık yükler arasında bir ayrım biridir.  Şimdiye kadar NuGet istemci yükleme işlemi için geliştirici doğrudan paketin yüklü olup olmadığını veya bir bağımlılık karşılamak için yüklendiğini etrafında her bağlam göndermedi.
Başlangıç NuGet 2.6 ile veri yükleme işlemi için artık gönderilir.  Paketi NuGet galerisinde istatistiklerle kullanıma verileri ayrı yükleme işlemleri olarak ile bir "-bağımlılık" soneki.

* Yükleme
* Bağımlılık yükleme
* Güncelleştirme
* Güncelleştirme bağımlılık
* Yeniden yükleyin
* Yeniden bağımlılık

Farklı işlem adı ek olarak, bağımlı bir paket kimliği yükleme için ayrıca kaydedilir.  NuGet galerisinde gelecekte yapılacak bir güncelleştirmenin paket yazarlarının paketlerini geliştiricilerin nasıl yüklüyorsanız tam olarak anlamak izin verme, raporlar içindeki verilerin açığa çıkarır.

## <a name="bug-fixes"></a>Hata Düzeltmeleri

NuGet 2.6 ayrıca çeşitli hata düzeltmeleri içerir. Tam bir listesi için iş öğeleri NuGet 2.6 Lütfen görünümü sabit [bu sürüm için NuGet sorun İzleyicisi](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).