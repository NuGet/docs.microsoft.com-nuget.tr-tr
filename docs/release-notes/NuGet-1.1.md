---
title: NuGet 1.0 ve 1.1 sürüm notları
description: NuGet bilinen sorunları, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr 1.1 sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6222a996f2fdcaaa81a1b16d1c6da2749936712a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547027"
---
# <a name="nuget-10-and-11-release-notes"></a>NuGet 1.0 ve 1.1 sürüm notları

[NuGet 1.2 sürüm notları](../release-notes/nuget-1.2.md)

NuGet 1.0 13 Ocak 2011'de yayınlanmıştır.  NuGet 1.1 12 Şubat 2011'de yayınlanmıştır.

## <a name="overview"></a>Genel Bakış

Bu belge, NuGet önemli bir önizleme sürümü göre gruplandırılmış 1.0 çeşitli sürümleri için sürüm notlarını içermektedir.

NuGet, aşağıdaki bileşenleri içerir:

* *NuGet.Tools.vsix* * şu şekildedir:
  * **Kitaplık Paketi iletişim kutusu Ekle** * göz atın ve paketleri yüklemek için kullanılan Visual Studio içinde iletişim.
  * **Paket Yöneticisi Konsolu** * Powershell konsolunda Visual Studio temel.
* *NuGet komut satırı aracını* * araç paketleri oluşturma (ve sonunda yayımlama için) kullanılır.

NuGet araçları Visual Studio Uzantısı (*NuGet.Tools.vsix*) gerektirir:

* Visual Studio 2010 veya Visual Web Developer 2010 Express.

NuGet komut satırı aracını gerektirir:

* .NET framework sürüm 4

## <a name="installation"></a>Yükleme

Bunu kullanmak için [en son sürüm](http://nuget.codeplex.com/releases/view/52018):

* Öncelikle eski yapı kaldırın. VS Bunu yapmak için yönetici olarak çalıştırmanız gerekir.
* Sahip olduğunuz tüm mevcut akışları kaldırın.
* İşaret eden yeni bir akış ekleyin [ http://go.microsoft.com/fwlink/?LinkId=206669 ](http://go.microsoft.com/fwlink/?LinkId=206669).

## <a name="nuget-11"></a>NuGet 1.1

Bu sürümde giderilen sorunlar listesinde [buradan ulaşabilirsiniz](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0)

## <a name="nuget-10-rtm"></a>NuGet 1.0 RTM

Bir sorun, RC'den bu yana RTM için düzeltildi.

* [Sorun 474: Çözümdeki tüm proje paketlerini kaldırma etkiler](http://nuget.codeplex.com/workitem/474)

## <a name="release-candidate"></a>Sürüm Adayı

CTP 2'den bu Sürüm Adayı'nda yapılan değişiklikler şunlardır: Hataların tam listesini görmek için sorun İzleyicisi'ni ziyaret edin.

* [Konsolundan paketin güncelleştirilmesi, bağımlılıkları güncelleştirmez.](http://nuget.codeplex.com/workitem/443)
* [Depo ayarlama ekleme paket çekme başvurusu (CTP1) paketi değil](http://nuget.codeplex.com/workitem/442)
* [Bozuk başvurularda ayrıldığında bir paketi güncelleştiriliyor](http://nuget.codeplex.com/workitem/440)
* [Get-Package-güncelleştirmeleri başarısız iletişim kutusu veya 'Tüm' toplama kaynak konsolda seçildiğinde](http://nuget.codeplex.com/workitem/439)
* [Paket doğrulama hataları alma](http://nuget.codeplex.com/workitem/426)
* [Kullanıcılar bir paketi paket Ekle iletişim kutusundan yüklenemediğinde uyar](http://nuget.codeplex.com/workitem/425)
* [Get-Package-paketleri çok sayıda güncelleştirme yapılırken güncelleştirmeleri oluşturur](http://nuget.codeplex.com/workitem/424)
* [Yanlış yazılmış nuspec dosyaları sırasında hata işleme geliştirin](http://nuget.codeplex.com/workitem/423)
* [Nuget paketi belirtilen dosya yok sayar.](http://nuget.codeplex.com/workitem/422)
* [İkinci son paket kaynağı kaldırarak ve ardından "Aşağı Taşı" VS kilitleniyor](http://nuget.codeplex.com/workitem/418)
* [Paketler yüklenirken derleme başvurusunu kaldırın.](http://nuget.codeplex.com/workitem/413)
* [Ayarları iletişim kutusu açılırken InvalidOperationException](http://nuget.codeplex.com/workitem/411)
* [Paket Yöneticisi konsolunda paket kaynağı için erişim anahtarı çalışmıyor](http://nuget.codeplex.com/workitem/410)
* [NuGet VS Ayarları iletişim erişim anahtarlarını yanlış alanlarına odaklanmak](http://nuget.codeplex.com/workitem/409)
* [Paket kimliği IntelliSense çok fazla öğe sorgu değil](http://nuget.codeplex.com/workitem/404)
* [Proje adı bir nokta karakteri ile Project paketi eklenirken hata](http://nuget.codeplex.com/workitem/403)
* [Sorun sınıflandırmalarına dosyaları belirtilen](http://nuget.codeplex.com/workitem/400)
* [Doğru resmi akış daha yeni bir yapı kullanırken kayıtlı](http://nuget.codeplex.com/workitem/399)
* [Etiket alanları yerine # kullanmalıdır](http://nuget.codeplex.com/workitem/397)
* [IPackageMetadata bazı yararlı bilgiler eksik](http://nuget.codeplex.com/workitem/388)
* [Rapor kötüye bağlantısı ekleme](http://nuget.codeplex.com/workitem/386)
* [Visual Studio'da paketleri sonları sıkıştırmasını App_Data kullanma](http://nuget.codeplex.com/workitem/380)
* [Etiket uygulama](http://nuget.codeplex.com/workitem/376)
* [Oluşturulacak bağımlılık boş paketiyle PackageBuilder sağlar](http://nuget.codeplex.com/workitem/373)
* [Paket sahipleri alan ekleme](http://nuget.codeplex.com/workitem/365)
* [VSIX araçları yerine NuGet Paket Yöneticisi söylemek VSIX bildirimini güncelleştir](http://nuget.codeplex.com/workitem/364)
* [Tüm kaynak seçildiğinde get-Package komutu hata oluşturur.](http://nuget.codeplex.com/workitem/359)
* [Paket kaynaklarının Seçenekleri iletişim kutusunda sıralanmasına izin vermek](http://nuget.codeplex.com/workitem/356)
* [Update-Package eski sürümü kaldırmaz](http://nuget.codeplex.com/workitem/352)
* [Bağımlılıklar için uygulama sürüm aralığı belirtimi](http://nuget.codeplex.com/workitem/347)
* ["Yeni paketi Ekle" tıklandığında Visual Studio kilitleniyor.](http://nuget.codeplex.com/workitem/346)
* [Paket Ekle iletişim kutusunda indirmeleri ve derecelendirmeleri görüntüle](http://nuget.codeplex.com/workitem/345)
* [Etkin kaynak iletişim kutusunda paket kaynaklarını arasında değiştirme güncelleştirmez](http://nuget.codeplex.com/workitem/344)
* [Paket Yöneticisi konsolu penceresinde tuş bağlamasını kaldırma](http://nuget.codeplex.com/workitem/339)
* [Install-Package, bir cmdlet adı olarak tanınmıyor...](http://nuget.codeplex.com/workitem/338)
* [Yerel bağımlılıkları normal akışlarına akışın bir paket yükleme çözümlenmedi](http://nuget.codeplex.com/workitem/332)
* [Hala kullanımda olan bağımlılıkların RemoveDependencies atlayın](http://nuget.codeplex.com/workitem/331)
* [Özgün sayfa isteği döndürür ancak sayfa gezintisi iptal ediliyor, kullanıcı farklı bir sayfasına gidilemiyor](http://nuget.codeplex.com/workitem/325)
* [Akışları paketleri çok sayıda hizmet vermek için NuPack.Server performansını araştırın.](http://nuget.codeplex.com/workitem/324)
* [Ben filtre ikinci kez bir paket için "Yeni" Paket kaynağı yerine daha önce seçilen kaynak kullanır.](http://nuget.codeplex.com/workitem/321)
* [Varsayılan paket kaynağı iletişim kutusu "Çevrimiçi" sekmesine seçerken seçilmesi gerekir.](http://nuget.codeplex.com/workitem/320)
* [Paket listesi, varsayılan olarak yüklü paketleri göstermelidir](http://nuget.codeplex.com/workitem/309)
* [Bütünleştirilmiş kod başvurusu HintPaths](http://nuget.codeplex.com/workitem/294)
* [Paket Yöneticisi konsolu açılırken özel durum](http://nuget.codeplex.com/workitem/268)
* [Konsol IntelliSense tüm akışı indirir.](http://nuget.codeplex.com/workitem/259)
* [Paket kaynağı 'Default' 'Etkin' adlandırılmamalıdır.](http://nuget.codeplex.com/workitem/258)
* [Paketi UI kaynakları: Tamam basarak eklemelidir yeni kaynak adı/kaynak alanları boş ise](http://nuget.codeplex.com/workitem/257)
* [Yüklü paketleri sayısı büyük olduğunda iletişim çok yavaş olur](http://nuget.codeplex.com/workitem/243)
* [Tanımlayıcı adlandırılmış derlemeler için bağlama yeniden yönlendirmeleri desteği](http://nuget.codeplex.com/workitem/238)
* [Paket Başvurusu Ekle... Paket kaynağı için aşağı açılan içerecek şekilde kullanıcı Arabirimi](http://nuget.codeplex.com/workitem/226)
* [NuPack config dosya adının agnostically yapılandırma dönüştürme desteği gerekiyor](http://nuget.codeplex.com/workitem/224)
* [BasePath NuPack.exe Derleme'den olmasını sağlar](http://nuget.codeplex.com/workitem/222)
* [Paket kaynak geri dönüş davranışı](http://nuget.codeplex.com/workitem/204)
* [GUI üzerinde kilitlenme](http://nuget.codeplex.com/workitem/201)
* [Sıralama seçenekleri paket iletişim eklemek için Ekle](http://nuget.codeplex.com/workitem/179)
* [Paket Yöneticisi konsolu temizlemek için kısayol tuşu](http://nuget.codeplex.com/workitem/174)
* [PowerConsole NuPack konsolu, başarısız olmasına neden olur.](http://nuget.codeplex.com/workitem/166)
* [Konsol ve paket iletişim kutusu Ekle, kullanıcı aracısı istekleri ayarlamanız gerekir](http://nuget.codeplex.com/workitem/141)
* [Yapı NuPack.exe ve VSIX sürüm numarasını ayarlayın.](http://nuget.codeplex.com/workitem/134)
* [Ortak PowerShell parametrelerini Gizle-?](http://nuget.codeplex.com/workitem/118)
* [Ekle - Konsolu komutları için ayrıntılı Yardımı](http://nuget.codeplex.com/workitem/110)
* [Geçerli paket kaynağı seçme paket iletişim izin Ekle](http://nuget.codeplex.com/workitem/88)
* [Taşıma NuPack.Core sınıflara farklı bir ad alanları](http://nuget.codeplex.com/workitem/50)
* [Cmdlet'leri için Yardım'ı Ekle](http://nuget.codeplex.com/workitem/23)
* [Paketi yükledikten sonra karma akışındaki doğrulayın](http://nuget.codeplex.com/workitem/18)

## <a name="ctp-2"></a>CTP 2

CTP 2'de yapılan en önemli değişiklikler şunlardır:

* Bir OData hizmet uç noktasına ATOM akışı paket anahtarlamalı: NuGet CTP2 sürümüne yükseltirseniz, aşağıdaki URL bir paket kaynağı olarak eklemeyi unutmayın: `https://feed.nuget.org/ctp2/odata/v1/`.
* Add-Package komutu yeniden adlandırıldı *Install-Package*.
* Güncelleştirilmiş `.nuspec` biçimi. `.nuspec` Biçimi artık içerir *iconUrl* alan paket Ekle iletişim kutusunda görüntülenecek bir 32 x 32 png simgesi belirtmek için. Bu nedenle, paketiniz ayırt etmek için ayarladığınızdan emin olun. `.nuspec` Biçimi de içeren yeni *projectUrl* alanı, paket hakkında daha fazla bilgi sağlayan bir web sayfası işaret edecek şekilde kullanabilirsiniz.

Bu derleme ile eski çalışmaz `.nupkg` dosyaları. Null başvuru özel durumları alırsanız, eski kullanmakta olduğunuz `.nupkg` dosya ve güncelleştirilmiş ile yeniden oluşturmanız [NuGet komut satırı aracını](http://nuget.codeplex.com/releases/52017/download/165468).

Özellikler (hatalar için küçük kod göndermediklerini vb. dahil değildir.) NuGet CTP 2 için düzeltilen hatalar ve bir listesi verilmiştir.

* [Hata unpacking paket bütünleştirilmiş kodlarının olduğunda TargetFramework bir derleme için belirtilemez.](http://nuget.codeplex.com/workitem/10)
* [NuPack konsol penceresi daha bulunabilir olmasını sağlayın](http://nuget.codeplex.com/workitem/14)
* [ILMerge nupack.exe sürüm](http://nuget.codeplex.com/workitem/19)
* [Daha iyi hata/özel durum işleme](http://nuget.codeplex.com/workitem/24)
* [[Nupack.Core]: PackageManager akışı ile ilgili hataları düzgün biçimde işlemesi](http://nuget.codeplex.com/workitem/28)
* [Konsolu için yeni bir simge gerekir](http://nuget.codeplex.com/workitem/29)
* [İletişim kutusunda dizeleri yerelleştirme](http://nuget.codeplex.com/workitem/38)
* [İndirilen .nupack dosyaları bellekte NuPack önbellekler](http://nuget.codeplex.com/workitem/40)
* [NuPack konsolu: konsol görüntülemek için varsayılan kısayol değiştirme](http://nuget.codeplex.com/workitem/48)
* [Proje sistemi, ortak özellikler için varsayılan değerleri desteklemelidir](http://nuget.codeplex.com/workitem/49)
* [Nupack.exe ile soubor nuspec tek bir klasörde çalıştıran bu nuspec kullanmalıdır](http://nuget.codeplex.com/workitem/52)
* [Proje menüsü bile, proje/çözüm yüklendikten gösterir.](http://nuget.codeplex.com/workitem/54)
* [temiz bir kod temeli kopyada Build.cmd başarısız](http://nuget.codeplex.com/workitem/56)
* [Kullanılabilir özellik güncelleştirmeleri](http://nuget.codeplex.com/workitem/57)
* [İletişim kutusu: iletişim kutusu aracılığıyla bir paketi eklenirken istemi konsolda kaldırır](http://nuget.codeplex.com/workitem/73)
* [Bir paketi 'Yükle' ye tıklayıp ekleme genellikle hiçbir görsel geri bildirim ile yavaş](http://nuget.codeplex.com/workitem/80)
* [Güncelleştirmeleri my yüklü paketleri olan bulmak için hiçbir yolu yoktur.](http://nuget.codeplex.com/workitem/82)
* [İletişim kutusunda yüklü paketi güncelleştirmek için hiçbir yolu yoktur.](http://nuget.codeplex.com/workitem/83)
* [İletişim kutusunda yüklü paketi kaldırmak için bir yolu yoktur](http://nuget.codeplex.com/workitem/84)
* [&ldquo;Paket başvurusu ekleme&hellip; &rdquo; yüklü başvuruları bağlam menüsünde görünür](http://nuget.codeplex.com/workitem/85)
* [Konsolundan bir paket güncelleştirdikten sonra hem eski sürümü ve yeni sürümü yüklü olarak gösterir](http://nuget.codeplex.com/workitem/86)
* [Konsolda etkinliğini iletişim kullanılırken, kullanımdan sonra kaybolur.](http://nuget.codeplex.com/workitem/87)
* [Temizleme komut satırı içinde nupack.exe ayrıştırma](http://nuget.codeplex.com/workitem/89)
* [Paket kaynaklarını bir kolay ad ekleyin](http://nuget.codeplex.com/workitem/98)
* [Paket simgeleri dahil olmak üzere desteklemek için .nuspec güncelleştir](http://nuget.codeplex.com/workitem/103)
* [Akış UI URL'sini kopyalama izin vermez](http://nuget.codeplex.com/workitem/105)
* [Daha iyi remove-package hata işleme.](http://nuget.codeplex.com/workitem/107)
* [Konsol penceresine yazarak imleç odaklanmak bağlıdır](http://nuget.codeplex.com/workitem/112)
* [Hata iletileri awful arayın](http://nuget.codeplex.com/workitem/116)
* [Remove-Package performansını yüklü olmayan bir paket için bozuk](http://nuget.codeplex.com/workitem/117)
* [Hiçbir paket kaynaklarını olduğunda bir paket kaldırma başarısız](http://nuget.codeplex.com/workitem/119)
* [Paket kaynağı kullanılamadığında remove-Package başarısız olur.](http://nuget.codeplex.com/workitem/120)
* [Paket meta veriler ve akış başlığı ekleyin.](http://nuget.codeplex.com/workitem/125)
* [Add kaynak parametresi Add-Package geri dön](http://nuget.codeplex.com/workitem/127)
* [Paket listesi olmalıdır - kaynak parametresi](http://nuget.codeplex.com/workitem/128)
* [Güncelleştirme NuPack.Server NuPack kullanıcı aracısı için yükleme paketi gerektirmek için](http://nuget.codeplex.com/workitem/142)
* [Lisans kabulü gerektiren tüm bağımlılıklar için lisans kabulü iletişim kutusu listelemesi gerekir](http://nuget.codeplex.com/workitem/145)
* [Bir paket akışta oluşturduğunda günlüğe hata kaydedin](http://nuget.codeplex.com/workitem/150)
* [NuPack.exe boş olmayan izin vermelidir &lt;licenseurl&gt; öğesi](http://nuget.codeplex.com/workitem/152)
* [Paket listesi, Get-Package ekleyin-Package Install-Package ve Remove-Package paketini kaldırmak için yeniden adlandır](http://nuget.codeplex.com/workitem/155)
* [Çözüm Gezgini paket başvurusu ekleme menüsü öğesinden kullanarak Visual Studio kilitleniyor](http://nuget.codeplex.com/workitem/158)
* [Bir iki nokta üst üste "kullanılabilir paket kaynaklarını" etiketi eksik](http://nuget.codeplex.com/workitem/160)
* [Büyük/küçük harfleri .nuspec xml öğesi büyük/küçük harf tutarlı bir şekilde ortası büyük olmak](http://nuget.codeplex.com/workitem/161)
* [NuPack VSIX'in bildirimi 'admin' bit kapatma gerekiyor](http://nuget.codeplex.com/workitem/162)
* [Liste-Package ile yoktur akışları çalıştırırsanız, null başvuru hatası alıyorum](http://nuget.codeplex.com/workitem/164)
* [nuget.exe: hedef yolu belirtin](http://nuget.codeplex.com/workitem/171)
* [Powershell hataları WinXP üzerinde paket Yönetimi konsolunu açma](http://nuget.codeplex.com/workitem/175)
* [Paket listesi yüklenmeye çalışılırken hatayla VS kilitlenmeleri](http://nuget.codeplex.com/workitem/176)
* [Meta paket (hiçbir dosya, yalnızca bağımlılıkları) izin ver](http://nuget.codeplex.com/workitem/180)
* [Powershell 2.0 modülü için PowerShell Betiği Dönüştür](http://nuget.codeplex.com/workitem/181)
* [Hedef belirtilmediğinde PathResolver yol bölümü önceki joker karakterleri atmalıdır](http://nuget.codeplex.com/workitem/183)
* [Hiçbir bağımlılık](http://nuget.codeplex.com/workitem/186)
* [Elmah yüklenirken hata oluştu](http://nuget.codeplex.com/workitem/192)
* [Yapılandırma dönüşümleri çalışmıyor doğru ile &lt;configsections&gt;](http://nuget.codeplex.com/workitem/194)
* [Değişkeni ' $global: projectCache' değil ayarlandığından alınamıyor](http://nuget.codeplex.com/workitem/203)
* [MSBuild görevi NuPack paketleri oluşturmak için](http://nuget.codeplex.com/workitem/205)
* [Paket listeleme aramayı ve filtrelemeyi desteklemesi gerekir](http://nuget.codeplex.com/workitem/206)
* [Lisans URL'si paket yazarı sağlıyorsa, bağlantı için lisans her zaman görüntüleme](http://nuget.codeplex.com/workitem/208)
* [Bazen "Erişim engellendi" özel durumuyla Remove-Package](http://nuget.codeplex.com/workitem/213)
* [Birim testleri başarısız: InvalidPackageIsExcludedFromFeedItems &amp; CreatingFeedConvertsPackagesToAtomEntries](http://nuget.codeplex.com/workitem/214)
* [Belirli framework sürümü bulunamazsa dosyaları geri dönüş/varsayılan bir dizi için izin ver](http://nuget.codeplex.com/workitem/223)
* [Paket Başvurusu Ekle... Bir paketi UI kaldırılamıyor](http://nuget.codeplex.com/workitem/225)
* [Paket başvurusu varsa studio kilitleniyor veya daha fazla proje kaldırılmadan ekleyin](http://nuget.codeplex.com/workitem/228)
* [Yapılandırma dönüşümü web.debug.config dosya üzerinde görünmüyor](http://nuget.codeplex.com/workitem/229)
* [init.ps1 özel paketini tetikleme değil](http://nuget.codeplex.com/workitem/237)
* [Ben ENTER tuşuna basarsanız, otomatik olarak kapanır. Bu nedenle yolları için feedlist eklerken, varsayılan düğme Tamam olarak ayarlanır](http://nuget.codeplex.com/workitem/240)
* [Kaldırmayı denemek bağımlılık VS 2 katı bir satır denenirse kilitlenir](http://nuget.codeplex.com/workitem/241)
* [Paket Ekle iletişim kutusunda proje URL'si görüntüle](http://nuget.codeplex.com/workitem/253)
* [Varsayılan yüklü paketleri için Add-Package iletişim kutusu](http://nuget.codeplex.com/workitem/254)
* [Paket iletişim kutusu Ekle menü öğesini değiştirin.](http://nuget.codeplex.com/workitem/261)
* [Ad alanları ve derlemeler yeniden adlandır](http://nuget.codeplex.com/workitem/274)
* [NuGet için NuPack projeyi yeniden adlandır](http://nuget.codeplex.com/workitem/282)
* [Bağımlılıklar listesine altında aşağıdaki metni ekleyin](http://nuget.codeplex.com/workitem/288)
* [Lisans kabulü iletişim kutusunda lisans kabulü metni değiştirme](http://nuget.codeplex.com/workitem/291)
* [Lisans kabulü iletişim paketleri listesinin üzerindeki metni değiştirme](http://nuget.codeplex.com/workitem/292)
* [Bir fwlink URL'si ile OData çalışmıyor](http://nuget.codeplex.com/workitem/304)
* [Paket Yöneticisi UI: agresif sayfalama kullanılan paket sayısı önbelleğe alma üzerinde](http://nuget.codeplex.com/workitem/317)
* [NuPack / NuGet -&gt; Paket Yöneticisi konsolu hata](http://nuget.codeplex.com/workitem/335)
* [Lisans kabulü için zaten yüklü paketlenmiş paket iletişim kutusunu gösterir Ekle](http://nuget.codeplex.com/workitem/336)

## <a name="ctp-1"></a>CTP 1

Özellikler ve NuGet CTP 1 için düzeltilen hataların listesi verilmiştir.

* [Paket uzantısı için .nupack adlandırılacak](http://nuget.codeplex.com/workitem/1)
* [Paket dosyası klasörüne taşıyın.](http://nuget.codeplex.com/workitem/2)
* [Yükleme birleştirme &amp; PS Ekle komutları](http://nuget.codeplex.com/workitem/3)
* [Fiil-isim cmdlet'leri için diğer adlar oluşturma](http://nuget.codeplex.com/workitem/4)
* [VS çözüm geçiş yaparken NuPack yanıltıcı](http://nuget.codeplex.com/workitem/6)
* [Biz 'paketleri' çözüm klasörü varsayılan olarak gizle](http://nuget.codeplex.com/workitem/11)
* [İçerik öğeleri ile belirteç değiştirme desteği ekleyin.](http://nuget.codeplex.com/workitem/12)
* [NuPack.UI PackageSource API'sini kullanmanız gerekir](http://nuget.codeplex.com/workitem/26)
* [[Nupack.Core]: PackageManager paketleri yüklemeden önce yüklü olarak işaretler](http://nuget.codeplex.com/workitem/27)
* [Silme varsayılan projeyi çözümden silinmiş projenin varsayılan yine de gösterir.](http://nuget.codeplex.com/workitem/30)
* ["Bu pakette zaten olduğundan bölümü belirtilen URI için eklenemiyor." Yeni paket hatası ile başarısız oluyor](http://nuget.codeplex.com/workitem/32)
* [Visual Studio GUI "NuPack" dizeleri Kaldır](http://nuget.codeplex.com/workitem/35)
* [Apache üst bilgisi için bir COPYRIGHT.txt dosyası ekleme](http://nuget.codeplex.com/workitem/36)
* [Güncelleştirme PackageSource komutunu Kaldır](http://nuget.codeplex.com/workitem/37)
* [Paket Yöneticisi profili yüklenirken bir özel durum oluşturduğunda kullanılamaz](http://nuget.codeplex.com/workitem/39)
* [init.ps1, install.ps1 ve uninstall.ps1 ek durumunu almak ihtiyacınız vardır](http://nuget.codeplex.com/workitem/41)
* [Konsol ve GUI paketleri tek bir pakette birleştirin](http://nuget.codeplex.com/workitem/42)
* [XML dönüştürme mantığını kökte XML uyguladıysanız çalışmıyor](http://nuget.codeplex.com/workitem/43)
* [Paket kaynağı Ayarları iletişim kutusu NuPack konsol güncelleştirilmiyor yönetme](http://nuget.codeplex.com/workitem/44)
* [NuPack konsolu kullanıcı Arabirimi: 'Paket kaynağı' 'paket akışı' açılan listeye yeniden adlandır](http://nuget.codeplex.com/workitem/45)
* [NuPack konsol seçenekleri: 'Deposu NuPack konsolu ile tutarlı olmasını UI' Yeniden Adlandır](http://nuget.codeplex.com/workitem/46)
* [IIS veya bir URL'den açıldı bir Web sitesi karşı Ekle-Package başarısız](http://nuget.codeplex.com/workitem/53)
* [Paket Yöneticisi kaynak FwLink ile çalışmıyor](http://nuget.codeplex.com/workitem/55)
* [Varsayılan paket kaynağı ayarla](http://nuget.codeplex.com/workitem/59)
* [Paket kaynaklarını seçeneğinde, yalnızca bir kaynak sağlandığında eklerken, varsayılan olduğu varsayılır.](http://nuget.codeplex.com/workitem/60)
* [Sahte "son" paketleri iletişim UI gösterir](http://nuget.codeplex.com/workitem/62)
* [Seçenekler: İptal'i tıklatarak değişiklikleri iptal etmez](http://nuget.codeplex.com/workitem/63)
* [Paket başvurusu iletişim arama büyük/küçük harfe duyarsız Ekle](http://nuget.codeplex.com/workitem/65)
* [AssemblyInfo.cs dosyalarında şirket meta verilerini düzeltin](http://nuget.codeplex.com/workitem/67)
* [VSIX için sürüm numarası](http://nuget.codeplex.com/workitem/71)
* [Remove-Package: Kullanma-? iki kez görüntüler Yardım](http://nuget.codeplex.com/workitem/72)
* [Yürütmek için proje düzeyi paketleri paketleri yükleme ve kaldırma](http://nuget.codeplex.com/workitem/74)
* [Sunucu bir nupack doğrulama başarısız olduğunda akışı oluşturamıyor](http://nuget.codeplex.com/workitem/90)
* [NuPack simgeler değiştirmeniz gerekiyor](http://nuget.codeplex.com/workitem/94)
* [NTLM http proxy akış paketi kimlik doğrulamasını yapmaz.](http://nuget.codeplex.com/workitem/96)
* [İletişim kutusunda her zaman VS penceresinde ortalanmış başlamıyor](http://nuget.codeplex.com/workitem/100)
* [Paket Ayrıntıları alanların çoğu iletişim kutusunda dolduruluyor değil](http://nuget.codeplex.com/workitem/102)
* [Kullanıcı Arabirimi iletişim yazarların adları göstermiyor](http://nuget.codeplex.com/workitem/108)
* [Neden - Remove-Paket sürümü](http://nuget.codeplex.com/workitem/113)
* [İletişim kullanıcı arabiriminde son sekmeyi Kaldır](http://nuget.codeplex.com/workitem/115)
* [VS kilitlenme doğru olduğunda iletişim UI en az bir açtıktan sonra çözüm klasörüne tıklayın.](http://nuget.codeplex.com/workitem/126)
* [Değişiklik listesi-Package yerel parametresinin-yüklü](http://nuget.codeplex.com/workitem/129)
* [Packages.XML NuPack.config için yeniden adlandırın.](http://nuget.codeplex.com/workitem/132)
* [Konsol imleci satırın sonuna zorlar.](http://nuget.codeplex.com/workitem/135)
* [Remove-Package IntelliSense bozuk](http://nuget.codeplex.com/workitem/136)
* [RequireLicenseAcceptance bayrağı .nuspec ve akış ekleme](http://nuget.codeplex.com/workitem/137)
* [LicenseUrl .nuspec biçimlendirmek ve paket akışı Ekle](http://nuget.codeplex.com/workitem/138)
* [Onay gerektiren paketi için Yükle'yi tıklayarak kabulü iletişim kutusu göstermelidir](http://nuget.codeplex.com/workitem/139)
* [Paket Ekle iletişim için sorumluluk reddi metnini ekleyin](http://nuget.codeplex.com/workitem/140)
* [Sorumluluk reddi, paket Konsolu ilk kez çalıştırılan Ekle](http://nuget.codeplex.com/workitem/143)
* [Konsolunda paket yüklendikten sonra yer alan sorumluluk reddi görüntüleme](http://nuget.codeplex.com/workitem/144)
* [.Nupack uzantısı için .nupkg yeniden adlandır](http://nuget.codeplex.com/workitem/146)