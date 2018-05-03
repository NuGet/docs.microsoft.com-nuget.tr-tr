---
title: NuGet 2.6 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere WebMatrix için NuGet 2.6.1 için sürüm notları.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 39ce6ac3d36464d26966b0dabb0893f09ad4afdc
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-26-release-notes"></a>NuGet 2.6 sürüm notları

[NuGet 2.5 sürüm notları](../release-notes/nuget-2.5.md) | [NuGet 2.6.1 WebMatrix sürüm notları](../release-notes/nuget-2.6.1-for-webmatrix.md)

NuGet 2.6 26 Haziran 2013'te yayımlanmıştır.

## <a name="notable-features-in-the-release"></a>Sürümdeki dikkat çekici özellikleri

### <a name="support-for-visual-studio-2013"></a>Visual Studio 2013 için destek

NuGet 2.6 Visual Studio 2013 için destek sağlayan ilk sürümüdür. Ve Visual Studio 2012 gibi her Visual Studio sürümünde NuGet Paket Yöneticisi uzantısı dahil edilir.

Hala Visual Studio 2010 ve Visual Studio 2012 destekleme ve olabildiğince küçük uzantısı boyutları tutma Visual Studio 2013 için en iyi olası desteği sağlamak için şu Visual Studio 2013 için ayrı bir uzantı oluşturduğunu özgün uzantısı hedef Visual Studio 2010 ve 2012 devam eder.

NuGet 2.6 ile başlayarak, aşağıdaki şekilde iki uzantıları yayımlayacak:

1. [NuGet Paket Yöneticisi](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManager) (Visual Studio 2010 ve 2012 için geçerlidir)
1. [Visual Studio 2013 için NuGet Paket Yöneticisi](https://marketplace.visualstudio.com/items?itemName=NuGetTeam.NuGetPackageManagerforVisualStudio2013)

Bu bölme ile [nuget.org](https://nuget.org) giriş sayfasının "Nuget'i Yükle" düğmesini alır, [NuGet yükleme](../install-nuget-client-tools.md) sayfasında, şunları bulabileceğiniz farklı NuGet istemcileri yükleme hakkında daha fazla bilgi.

<a name="xdt"></a>

### <a name="xdt-webconfig-transformation-support"></a>XDT Web.config dönüşümü desteği

NuGet istemci için en çok istenen özelliklerden biri, Visual Studio derleme yapılandırma dönüşümler kullanılan XDT dönüştürme altyapısı kullanan daha güçlü XML dönüşümleri desteklemek için bırakıldı.

Nisan 2013'te XDT NuGet desteği ile ilgili iki büyük duyuruları yapılan. İlk XDT kitaplığı kendisini çalıştırılmakta emin olan [bir NuGet paketi olarak yayımlanan](https://nuget.org/packages/Microsoft.Web.Xdt) ve [açık kaynaklıdır CodePlex üzerinde](http://xdt.codeplex.com/). Bu adım NuGet istemcisi de dahil olmak üzere diğer açık kaynaklı yazılım tarafından ücretsiz olarak kullanılacak XDT altyapısı etkin. İkinci duyuru için NuGet istemci dönüşümler XDT Altyapısı'nın kullanımını desteklemek için plan oluştu. Bu tümleştirme NuGet 2.6 içerir.

#### <a name="how-it-works"></a>Nasıl çalışır?

NuGet XDT destek yararlanmak için mekanizması gereksinimlerine şuna benzer [geçerli config dönüştürmesi özelliği](../create-packages/source-and-config-file-transformations.md).
Dönüştürme dosyaları paketin içerik klasöründe eklenir. Ancak, Config dönüşümleri yükleme ve kaldırma için tek bir dosya kullanırken, aşağıdaki dosyaları kullanarak bu işlemlerin ikisinin üzerinde ayrıntılı denetim XDT dönüşümleri etkinleştirin:

- Web.config.install.xdt
- Web.config.uninstall.xdt

Ayrıca, NuGet Dosya sonekini dönüştürmeleri için varolan web.config.transforms kullanarak paketleri çalışmaya devam edecek şekilde çalıştırmak için hangi altyapısı belirlemek için kullanır. XDT dönüşümleri ayrıca tüm XML dosyası (yalnızca web.config) uygulanması bu projenizde diğer uygulamalar için yararlanabileceğiniz şekilde.

#### <a name="what-you-can-do-with-xdt"></a>XDT ile yapabilecekleriniz

XDT'ın en güçlü biri kendi [basit ancak güçlü sözdizimi](http://msdn.microsoft.com/library/dd465326.aspx) bir XML DOM yapısını işlemek için Yalnızca başka bir yapı üzerine bir sabit belge yapısı üst üste getirme yerine, bir basit öznitelik XPath destek tam adıyla eşleşen gelen, çeşitli şekillerde öğelerinde eşleştirmek için XDT denetimleri sağlar. Eşleşen bir öğe veya öğelerin bulunduğunda, ekleme, güncelleştirme, veya özniteliklerin kaldırılması, belirli bir konumda yeni bir öğe yerleştirme veya değiştirme veya tüm kaldırma anlamına olup olmadığını XDT işlevleri zengin bir dizi öğeleri yönlendirmek için sağlar öğe ve alt öğelerini.

### <a name="machine-wide-configuration"></a>Makine genelinde yapılandırma

NuGet harika gücü, aksi takdirde büyük yürütülebilir dosya veya bir dizi olabilen bağımsız olarak tümleşik ve en önemlisi tutulan ve sürümü tutulan modüler bileşenleri kitaplığa aşağı keser biridir. Bu, bir yan etkisi, ancak bir ürün veya ürün ailesi geleneksel fikrini potansiyel olarak daha parçalanmış olur.
NuGet özel paket kaynak özellik paketleri düzenlenmesi bir yolunu sunar; Ancak, özel pakette kaynakları, kendi bulunabilirlik değil.

NuGet %2.6 ProgramData%/NuGet/Config yolu klasör hiyerarşisiyle arayarak NuGet yapılandırma mantığı genişletir. Ürün yükleyicilerini ürünlerini özel paket kaynağını kaydetmek için bu klasörün altında özel NuGet yapılandırma dosyaları ekleyebilirsiniz. Ayrıca, klasör yapısı, ürün, sürüm ve IDE bile SKU'su semantiği destekler. Bu dizinleri ayarlarından bir "en son WINS'de" öncelik stratejisi ile aşağıdaki sırayla uygulanır.

1. %ProgramData%\NuGet\Config\*.config
2. %ProgramData%\NuGet\Config\{IDE}\*.config
3. %ProgramData%\NuGet\Config\{IDE}\{sürüm}\*.config
4. %ProgramData%\NuGet\Config\{IDE}\{sürüm}\{SKU}\*.config

Bu listede, Visual Studio söz konusu olduğunda, "Visual Studio" olacak şekilde {IDE} yer tutucusu NuGet çalışan IDE özeldir. {Version} ve {SKU} yer tutucuları sağlanmıştır tarafından IDE (örn. "11.0" ve "WDExpress", "VWDExpress" ve "Pro", sırasıyla). Klasör sonra birçok farklı *.config dosyaları içerebilir.
Bu nedenle, ACME bileşen şirket kendi ürün yükleyicisi parçası olarak, aşağıdaki dosya yolu oluşturarak yalnızca Professional ve Ultimate sürümleri Visual Studio 2012 içinde görünür olacak bir özel paket kaynağı ekleyebilirsiniz:

%ProgramData%\NuGet\Config\VisualStudio\11.0\Pro\acme.config

Klasör yapısı programları makine genelinde paket kaynaklarını NuGet yapılandırmasına eklemek için yazılım yükleyicileri gibi basit olmasını sağlarken NuGet yapılandırma iletişim ayrıca izin vermek için paket kaynağı olarak kaydını güncelleştirildi (örneğin % AppData%/NuGet/NuGet.Config kayıtlı) ya da kullanıcıya özel veya makine genelinde.

Bu özellik, Visual Studio 2013, bir dosya konumunda yüklendiği tarafından kullanılan:

%ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config

Bu dosya içinde ".NET Framework paketleri" olarak adlandırılan yeni bir paket kaynağı yapılandırılır.

![NuGet yapılandırma dosyası makine geniş ayarları](./media/NuGet-Config-File-Machine-Wide.png)

### <a name="contextualizing-search"></a>Contextualizing arama

NuGet Galerisi tarafından sunulan paket sayısı büyük bir hızla büyümeye devam ettikçe, aramasını geliştirme NuGet öncelik listesinin başında şimdiye kadar kalır. NuGet sürümü ve SKU biri görsel kullanmakta olduğunuz Studio ve oluşturmakta olduğunuz proje türü hakkında bilgi olası arama alaka belirlemek için ölçüt olarak kullanacağı anlamına gelir, bağlamsal arama NuGet için planlanan özelliklerden biridir sonuçları.

NuGet 2.6 ile başlayarak, her bir paketi yüklendiğinde, yeniden yükleme bağlamının yükleme işlemi verileri bir parçası olarak kaydedilir.  Aramaları de arama sonuçları tarafından bağlamsal yükleme eğilimleri artırmak NuGet galerisinde sağlayacak aynı bağlam bilgilerini gönderir.  NuGet galerisinde için gelecekteki bir güncelleştirme bu bağlama duyarlı ilgi artırmanın olanak sağlar.

### <a name="tracking-direct-installs-vs-dependency-installs"></a>İzleme vs doğrudan yükler. Bağımlılık yükler

Paketi yazarları bağlı olan daha da fazla üzerinde [paket istatistikleri](http://blog.nuget.org/20130226/Introducing-Package-Statistics.html) NuGet galerisinde sağlanan.  Yazarları için istediniz önemli eksik veri noktası doğrudan paketini yükler ve bağımlılık yükleyen arasında ayrım biridir.  Şimdiye kadar her bağlam için geliştirici doğrudan paketin yüklü olup olmadığını veya bir bağımlılık karşılamak için yüklü olduğu, yükleme işlemi geçici NuGet istemci göndermedi.
Başlangıç NuGet 2.6 ile veri yükleme işlemi için şimdi gönderilir.  NuGet galerisinde paket istatistik kullanıma verilerin ayrı yükleme işlemleri olarak ile bir "-bağımlılık" soneki.

* Yükleme
* Yükleme bağımlılığını
* Güncelleştirme
* Güncelleştirme bağımlılık
* Yeniden yükleme
* Yeniden bağımlılık

Farklı işlem adı yanı sıra bağımlı paket kimliğini de yükleme için kaydedilir.  NuGet galerisinde için gelecekteki bir güncelleştirme raporları, geliştiricilerin kendi paketleri nasıl yüklüyorsanız tam olarak anlamak paketi yazarları izin vererek içinde verilerin açığa çıkarır.

## <a name="bug-fixes"></a>Hata Düzeltmeleri

NuGet 2.6 çeşitli hata düzeltmeleri de içerir. Tam bir listesi için iş öğeleri NuGet 2.6 Lütfen görünüm sabit [NuGet sorun İzleyicisi bu sürüm için](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.6&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).