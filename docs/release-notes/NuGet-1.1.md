---
title: NuGet 1,0 ve 1,1 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 1,1 sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4f90888eae4d039c99d6f6879a06107ec5a31a82
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384703"
---
# <a name="nuget-10-and-11-release-notes"></a>NuGet 1,0 ve 1,1 sürüm notları

[NuGet 1,2 sürüm notları](../release-notes/nuget-1.2.md)

NuGet 1,0, 13 Ocak 2011 tarihinde yayınlanmıştır.  NuGet 1,1, 12 Şubat 2011 ' de yayımlanmıştır.

## <a name="overview"></a>Genel bakış

Bu belge, büyük önizleme sürümüne göre gruplandırılan çeşitli NuGet 1,0 sürümleri için sürüm notlarını içerir.

NuGet aşağıdaki bileşenleri içerir:

* *NuGet. Tools. vsix* * aşağıdakilerden oluşur:
  * Paketlere gözatıp yüklemek için kullanılan Visual Studio içinde **kitaplık paketi Iletişim kutusu** * Iletişim kutusu ekleyin.
  * **Paket Yöneticisi konsolu** * Visual Studio 'da PowerShell tabanlı konsol.
* Paketleri oluşturmak (ve sonunda yayımlamak) için kullanılan *NuGet komut satırı aracı* * aracı.

NuGet araçları Visual Studio uzantısı (*NuGet. Tools. vsix*) şunları gerektirir:

* Visual Studio 2010 veya Visual Web Developer 2010 Express.

NuGet komut satırı aracı şunları gerektirir:

* .NET Framework sürüm 4

## <a name="installation"></a>Yükleme

Bu [en son sürümü](http://nuget.codeplex.com/releases/view/52018)kullanmak için:

* Önce eski derlemenizi kaldırın. Bunu yapmak için yönetici olarak ' i çalıştırmanız gerekir.
* Sahip olduğunuz tüm mevcut akışları kaldırın.
* <https://go.microsoft.com/fwlink/?LinkId=206669>işaret eden yeni bir akış ekleyin.

## <a name="nuget-11"></a>NuGet 1.1

Bu sürümde düzeltilen sorunların listesi [burada bulunabilir](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0)

## <a name="nuget-10-rtm"></a>NuGet 1,0 RTM

RC 'den beri RTM için bir sorun düzeltildi.

* [Sorun 474: paketlerin kaldırılması Çözümdeki tüm projeyi etkiler](http://nuget.codeplex.com/workitem/474)

## <a name="release-candidate"></a>Sürüm adayı

Bu sürüm, CTP 2 ' den beri yapılan değişiklikler aşağıda verilmiştir. Hataların tam listesini görmek için sorun Izleyicisi ' ni ziyaret edin.

* [Paketin konsolundan güncelleştirilmesi bağımlılıklar güncellemez.](http://nuget.codeplex.com/workitem/443)
* [Paket çekmeleri ekleme bin paket başvurusu yok (CTP1)](http://nuget.codeplex.com/workitem/442)
* [Bir paketin güncelleştirilmesi bozuk başvuruları bırakır](http://nuget.codeplex.com/workitem/440)
* [Get-Package-güncelleştirmeler iletişim kutusunda başarısız oluyor veya konsolda ' tümü ' Birleşik kaynağı seçili olduğunda](http://nuget.codeplex.com/workitem/439)
* [Paket doğrulama hatalarını alma](http://nuget.codeplex.com/workitem/426)
* [Paket ekle Iletişim kutusundan bir paket yükleneolmadığında kullanıcıları uyar](http://nuget.codeplex.com/workitem/425)
* [Paket al-çok sayıda paket güncelleştirilirken güncelleştirmeler oluşturur](http://nuget.codeplex.com/workitem/424)
* [Nuspec dosyaları hatalı olarak yazıldığınızda hata işlemeyi geliştir](http://nuget.codeplex.com/workitem/423)
* [NuGet paketi belirtilen dosyaları yok sayıyor](http://nuget.codeplex.com/workitem/422)
* [İkinci-son paket kaynağını kaldırıp "aşağı taşı" kilitlenmelerine](http://nuget.codeplex.com/workitem/418)
* [Paketler yüklenirken derleme başvurusunu kaldır](http://nuget.codeplex.com/workitem/413)
* [Ayarları açarken InvalidOperationException iletişim kutusu](http://nuget.codeplex.com/workitem/411)
* [Paket Yöneticisi konsolundaki paket kaynağı için erişim anahtarı çalışmıyor](http://nuget.codeplex.com/workitem/410)
* [NuGet VS ayarları Iletişim kutusu erişim tuşları, yanlış alanlara odaklanmayı sağlar](http://nuget.codeplex.com/workitem/409)
* [Paket KIMLIĞI IntelliSense çok fazla öğe sorgulayamamalıdır](http://nuget.codeplex.com/workitem/404)
* [Proje adında nokta karakteri olan projeye paket ekleme hatası](http://nuget.codeplex.com/workitem/403)
* [Nuspec içinde belirtilen dosyalarla ilgili sorun](http://nuget.codeplex.com/workitem/400)
* [Daha yeni derleme kullanılırken, doğru resmi akış kaydedilmelidir](http://nuget.codeplex.com/workitem/399)
* [Etiketler yerine boşluklar kullanmalıdır #](http://nuget.codeplex.com/workitem/397)
* [Ipackagemetadata bazı yararlı bilgiler eksik](http://nuget.codeplex.com/workitem/388)
* [Iletişim kutusuna uygunsuz kullanım bağlantısı ekle](http://nuget.codeplex.com/workitem/386)
* [Visual Studio 'da paket sonlarını açmak için App_Data kullanma](http://nuget.codeplex.com/workitem/380)
* [Etiketleri Uygula](http://nuget.codeplex.com/workitem/376)
* [PackageBuilder, hiçbir bağımlılığı oluşturulacak boş pakete izin veriyor](http://nuget.codeplex.com/workitem/373)
* [Paket için sahipler alanı Ekle](http://nuget.codeplex.com/workitem/365)
* [VSıX bildirimini, VSıX araçları yerine NuGet Paket Yöneticisi olarak güncelleştirin](http://nuget.codeplex.com/workitem/364)
* [Tüm kaynak seçildiğinde Get-Package komutu bir hata oluşturur](http://nuget.codeplex.com/workitem/359)
* [Seçenekler iletişim kutusunda paket kaynaklarının sıralamasına izin ver](http://nuget.codeplex.com/workitem/356)
* [Güncelleştirme-paket eski sürümü kaldırmaz](http://nuget.codeplex.com/workitem/352)
* [Bağımlılıklar için sürüm aralığı belirtimini Uygula](http://nuget.codeplex.com/workitem/347)
* ["Yeni paket Ekle" tıklarken Visual Studio kilitleniyor](http://nuget.codeplex.com/workitem/346)
* [Paket ekle Iletişim kutusunda Indirmeleri ve derecelendirmeleri görüntüleme](http://nuget.codeplex.com/workitem/345)
* [Iletişim kutusundaki paket kaynakları arasında değişiklik yapmak etkin kaynağı güncelleştirmiyor](http://nuget.codeplex.com/workitem/344)
* [Paket Yöneticisi konsol penceresi için anahtar bağlamasını kaldır](http://nuget.codeplex.com/workitem/339)
* [Install-Package, bir cmdlet 'in adı olarak tanınmıyor...](http://nuget.codeplex.com/workitem/338)
* [Yerel akıştan paket yükleme normal akışlardaki bağımlılıklar çözümlenmiyor](http://nuget.codeplex.com/workitem/332)
* [RemoveDependencies hala kullanımda olan bağımlılıkları atmalıdır](http://nuget.codeplex.com/workitem/331)
* [Sayfa gezintisi iptal edilirse, Özgün sayfa isteği döndürüldüğünde Kullanıcı farklı bir sayfaya gidemezsiniz](http://nuget.codeplex.com/workitem/325)
* [Çok sayıda paket içeren akışlara hizmet vermek için NuPack. Server performansını araştırın.](http://nuget.codeplex.com/workitem/324)
* [Bir paket için ikinci kez filtreleyediğimde, daha önce seçilen kaynak yerine "yeni" paket kaynağını kullanır.](http://nuget.codeplex.com/workitem/321)
* [İletişim kutusunda "çevrimiçi" sekmesi seçilirken varsayılan paket kaynağı seçilmelidir.](http://nuget.codeplex.com/workitem/320)
* [List-Package yüklü paketleri varsayılan olarak göstermelidir](http://nuget.codeplex.com/workitem/309)
* [Derleme başvurusu HintPaths](http://nuget.codeplex.com/workitem/294)
* [Paket Yöneticisi konsolu açılırken özel durum oluştu](http://nuget.codeplex.com/workitem/268)
* [Konsol IntelliSense tüm akışı indirir](http://nuget.codeplex.com/workitem/259)
* [' Default ' paket kaynağı ' Active ' olarak yeniden adlandırılmalıdır](http://nuget.codeplex.com/workitem/258)
* [Paket kaynakları kullanıcı arabirimi: ad/kaynak alanları boş değilse tamam 'a basıldığında yeni kaynağı eklemesi gerekir](http://nuget.codeplex.com/workitem/257)
* [Yüklü paketlerin sayısı büyükse iletişim kutusu süper yavaşlamaya neden olur](http://nuget.codeplex.com/workitem/243)
* [Tanımlayıcı adlandırılmış derlemeler için bağlama yeniden yönlendirmelerini destekleme](http://nuget.codeplex.com/workitem/238)
* [Paket başvurusu Ekle... Paket kaynağına yönelik açılan liste eklemek için Kullanıcı arabirimi](http://nuget.codeplex.com/workitem/226)
* [NuPack 'in yapılandırma dosyası adının belirsiz şekilde yapılandırma dönüşümünü desteklemesi gerekir](http://nuget.codeplex.com/workitem/224)
* [BasePath 'nin NuPack. exe içinde geçersiz Kılınılmasına izin verir](http://nuget.codeplex.com/workitem/222)
* [Paket kaynağı geri dönüş davranışı](http://nuget.codeplex.com/workitem/204)
* [GUI üzerinde kilitlenme](http://nuget.codeplex.com/workitem/201)
* [Paket ekle Iletişim kutusuna sıralama seçenekleri ekleme](http://nuget.codeplex.com/workitem/179)
* [Paket Yöneticisi konsolunu temizlemek için kısayol tuşu](http://nuget.codeplex.com/workitem/174)
* [PowerConsole, NuPack konsolunun başarısız olmasına neden oluyor](http://nuget.codeplex.com/workitem/166)
* [Konsol ve paket Ekle Iletişim kutusu isteklerde Kullanıcı Aracısı 'nı ayarlaması gerekir](http://nuget.codeplex.com/workitem/141)
* [Derlemede VSıX ve NuPack. exe sürüm numarasını ayarlayın.](http://nuget.codeplex.com/workitem/134)
* [Ortak PowerShell parametreleri-? ile gizlensin](http://nuget.codeplex.com/workitem/118)
* [Konsol komutları için ayrıntılı yardım ekleme](http://nuget.codeplex.com/workitem/110)
* [Paket ekle Iletişim kutusu geçerli paket kaynağını seçmeye Izin verilmelidir](http://nuget.codeplex.com/workitem/88)
* [NuPack. Core sınıflarını farklı ad alanlarına taşıyın](http://nuget.codeplex.com/workitem/50)
* [Cmdlet 'lere yardım ekleme](http://nuget.codeplex.com/workitem/23)
* [Paket indirdikten sonra akıştan karmayı doğrula](http://nuget.codeplex.com/workitem/18)

## <a name="ctp-2"></a>CTP 2

CTP 2 ' de yapılan en önemli değişiklikler aşağıda verilmiştir:

* Paket akışı ATOM 'dan OData hizmeti uç noktasına geçildi: NuGet 'in CTP2 sürümüne yükseltirseniz, şu URL 'YI bir paket kaynağı olarak eklediğinizden emin olun: `https://feed.nuget.org/ctp2/odata/v1/`.
* *Install*-Package için Add-Package komutu yeniden adlandırıldı.
* `.nuspec` biçimi güncelleştirildi. `.nuspec` biçimi artık paket Ekle Iletişim kutusunda görünecek bir 32x32 png simgesi belirtmek için *Iurl* alanını içerir. Bu nedenle, paketinizi ayırt etmek için bunu ayarladığınızdan emin olun. `.nuspec` biçimi, paketiniz hakkında daha fazla bilgi sağlayan bir Web sayfasına işaret etmek için kullanabileceğiniz yeni *Projecturl* alanını da içerir.

Bu derleme eski `.nupkg` dosyaları ile çalışmayacaktır. Null başvuru özel durumları alırsanız, eski bir `.nupkg` dosyası kullanıyorsunuz ve güncelleştirilmiş [NuGet komut satırı aracı](http://nuget.codeplex.com/releases/52017/download/165468)ile yeniden oluşturmanız gerekiyor.

Aşağıda, NuGet CTP 2 için düzeltilen Özellikler ve hataların listesi verilmiştir (küçük kod temizleme işlemleri için hata içermez vb.).

* [Bir bütünleştirilmiş kod için TargetFramework oluştururken Paket derlemeleri açılırken hata oluştu.](http://nuget.codeplex.com/workitem/10)
* [NuPack konsol penceresini daha fazla bulunabilir yap](http://nuget.codeplex.com/workitem/14)
* [Nupack. exe yayınını ılmerge](http://nuget.codeplex.com/workitem/19)
* [Daha iyi hata/özel durum işleme](http://nuget.codeplex.com/workitem/24)
* [[Nupack. Core]: PackageManager akış ile ilgili hataları düzgün şekilde işlemelidir](http://nuget.codeplex.com/workitem/28)
* [Konsol için yeni bir simge gerekiyor](http://nuget.codeplex.com/workitem/29)
* [Iletişim kutusunda dizeleri yerelleştirin](http://nuget.codeplex.com/workitem/38)
* [NuPack önbellekler. nupack dosyaları bellekte indirildi](http://nuget.codeplex.com/workitem/40)
* [NuPack konsolu: konsolu görüntülemek için varsayılan kısayolu değiştirin](http://nuget.codeplex.com/workitem/48)
* [ProjectSystem ortak özellikler için varsayılan değerleri desteklemelidir](http://nuget.codeplex.com/workitem/49)
* [Yalnızca bir nuspec dosyası olan bir klasörde nupack. exe ' nin çalıştırılması bu nuspec 'i kullanmalıdır](http://nuget.codeplex.com/workitem/52)
* [Proje menüsü, proje/çözüm yüklü olmadığında bile görüntülenir](http://nuget.codeplex.com/workitem/54)
* [CodeBase 'in temiz bir kopyası üzerinde Build. cmd başarısız oluyor](http://nuget.codeplex.com/workitem/56)
* [Güncelleştirmeler kullanılabilir özelliği](http://nuget.codeplex.com/workitem/57)
* [İletişim kutusu: iletişim kutusu aracılığıyla paket ekleme, istemi konsolda kaldırır](http://nuget.codeplex.com/workitem/73)
* [' Install ' öğesine tıklayarak bir paket eklemek, görsel geri bildirimde bulunmamakla genellikle yavaştır](http://nuget.codeplex.com/workitem/80)
* [Yüklü paketlerimin hangilerinin güncelleştirme olduğunu keşfetmenin bir yolu yoktur.](http://nuget.codeplex.com/workitem/82)
* [İletişim kutusunda yüklü bir paketi güncelleştirmenin bir yolu yoktur.](http://nuget.codeplex.com/workitem/83)
* [İletişim kutusunda yüklü bir paketi kaldırmanın bir yolu yoktur](http://nuget.codeplex.com/workitem/84)
* [&ldquo;paket başvurusu ekleme&hellip;&rdquo;, yüklü başvuruların bağlam menüsünde görünür](http://nuget.codeplex.com/workitem/85)
* [Konsolundan bir paket güncelleştirildikten sonra, hem eski sürümü hem de yeni sürümü yüklü olarak gösterir](http://nuget.codeplex.com/workitem/86)
* [İletişim kutusu kullanılırken konsolundaki etkinlik, kullanıldıktan sonra kayboluyor](http://nuget.codeplex.com/workitem/87)
* [Nupack. exe ' de temizleme komut satırı ayrıştırma](http://nuget.codeplex.com/workitem/89)
* [Paket kaynaklarına kolay bir ad ekleyin](http://nuget.codeplex.com/workitem/98)
* [Package simgeleri dahil olmak üzere. nuspec öğesini destekleyecek şekilde Güncelleştir](http://nuget.codeplex.com/workitem/103)
* [Akış Kullanıcı arabirimi URL 'YI kopyalamaya izin vermiyor](http://nuget.codeplex.com/workitem/105)
* [Daha iyi kaldırma-paket hatası işleme.](http://nuget.codeplex.com/workitem/107)
* [Konsol penceresine yazma, imleç odağa bağlıdır](http://nuget.codeplex.com/workitem/112)
* [Hata iletileri görünüyor](http://nuget.codeplex.com/workitem/116)
* [Yüklü olmayan bir paket için Remove-Package performansı hatalı](http://nuget.codeplex.com/workitem/117)
* [Paket kaynağı olmadığında bir paketin kaldırılması başarısız olur](http://nuget.codeplex.com/workitem/119)
* [Paket kaynağı kullanılamadığında, Remove-Package başarısız olur](http://nuget.codeplex.com/workitem/120)
* [Paket meta verilerine ve akışına başlık ekleyin.](http://nuget.codeplex.com/workitem/125)
* [-Source parametresini Add-Package öğesine geri ekleyin](http://nuget.codeplex.com/workitem/127)
* [List-Package bir-Source parametresine sahip olmalıdır](http://nuget.codeplex.com/workitem/128)
* [NuPack. Server 'ı, NuPack Kullanıcı aracısının paketi Indirmesini gerektirecek şekilde Güncelleştir](http://nuget.codeplex.com/workitem/142)
* [Lisans kabulü Iletişim kutusu kabul gerektiren tüm bağımlılıklara yönelik lisansların listesini almalıdır](http://nuget.codeplex.com/workitem/145)
* [Akışta bir paket oluşturduğunda hata kaydetme](http://nuget.codeplex.com/workitem/150)
* [NuPack. exe boş bir &lt;licenseurl&gt; öğesine izin içermemelidir](http://nuget.codeplex.com/workitem/152)
* [List-Install-Package, Install-Package ve Remove-Package to Install-Package olarak yeniden adlandır](http://nuget.codeplex.com/workitem/155)
* [Çözüm Gezgini kilitleniyor Visual Studio 'dan paket başvurusu Ekle menü öğesini kullanma](http://nuget.codeplex.com/workitem/158)
* ["Kullanılabilir paket kaynakları" etiketinde iki nokta eksik](http://nuget.codeplex.com/workitem/160)
* [. Nuspec XML öğesi büyük küçük harfe sürekli beyaz bir şekilde yapılır](http://nuget.codeplex.com/workitem/161)
* [NuPack VSıX bildiriminin ' admin' bit ' i açması gerekir](http://nuget.codeplex.com/workitem/162)
* [Liste paketini akışsız çalıştırırsanız, null başvuru hatası alırsınız](http://nuget.codeplex.com/workitem/164)
* [NuGet. exe: hedef yolu belirtin](http://nuget.codeplex.com/workitem/171)
* [WinXP üzerinde Paket Yönetimi konsolunu açan PowerShell hataları](http://nuget.codeplex.com/workitem/175)
* [Paket listesi yüklenmeye çalışılırken VS kilitleniyor](http://nuget.codeplex.com/workitem/176)
* [meta paketlere izin ver (dosya yok, yalnızca bağımlılıklar)](http://nuget.codeplex.com/workitem/180)
* [PowerShell betiğini PowerShell 2,0 modülüne Dönüştür](http://nuget.codeplex.com/workitem/181)
* [PathResolver, hedef belirtildiğinde Joker karakterlerden yola çıkar.](http://nuget.codeplex.com/workitem/183)
* [Bağımlılık yok](http://nuget.codeplex.com/workitem/186)
* [ELMAH yükleme hatası](http://nuget.codeplex.com/workitem/192)
* [Yapılandırma dönüştürmeleri &lt;configSections ile düzgün çalışmıyor&gt;](http://nuget.codeplex.com/workitem/194)
* [' $Global:p rojectCache ' değişkeni ayarlanmadığından alınamıyor](http://nuget.codeplex.com/workitem/203)
* [NuPack paketleri oluşturmak için MSBuild görevi ekleme](http://nuget.codeplex.com/workitem/205)
* [List-Package aramayı/filtrelemeyi desteklemesi gerekir](http://nuget.codeplex.com/workitem/206)
* [Paket yazarı bir lisans URL 'SI sağlıyorsa, her zaman lisansa bir bağlantı görüntüle](http://nuget.codeplex.com/workitem/208)
* [Remove-Package ile zaman zaman "erişim engellendi" özel durumu](http://nuget.codeplex.com/workitem/213)
* [Birim testleri başarısız: ınvalidpackageısexcludedfromfeeditems &amp; Creatingfeedconvertspackagestoatomendenemeler](http://nuget.codeplex.com/workitem/214)
* [Yansımalı bir çerçeve sürümü bulunamazsa, geri dönüş/varsayılan dosya kümesine izin ver](http://nuget.codeplex.com/workitem/223)
* [Paket başvurusu Ekle... Kullanıcı arabirimi bir paketi kaldıramıyor](http://nuget.codeplex.com/workitem/225)
* [Bir veya daha fazla proje kaldırıldığında paket başvurusu kilitleniyor Studio Ekle](http://nuget.codeplex.com/workitem/228)
* [Yapılandırma dönüştürmesi Web. Debug. config dosyasında çalışmıyor gibi görünüyor](http://nuget.codeplex.com/workitem/229)
* [init. ps1 özel pakette tetikmedi](http://nuget.codeplex.com/workitem/237)
* [Feedlist 'e yollar eklenirken, varsayılan düğme Tamam olarak ayarlanır, bu nedenle ENTER tuşuna Bassam otomatik olarak kapanır](http://nuget.codeplex.com/workitem/240)
* [Bir satırda 2 kez denendiğinde, bağımlılığı kaldırma girişimi kilitlenme Ile sonuçlanır](http://nuget.codeplex.com/workitem/241)
* [Paket Ekle iletişim kutusunda proje URL 'sini görüntüle](http://nuget.codeplex.com/workitem/253)
* [Yüklü paketlere varsayılan yükleme paketi Ekle iletişim kutusu](http://nuget.codeplex.com/workitem/254)
* [Paket ekle Iletişim menü öğesi değiştir.](http://nuget.codeplex.com/workitem/261)
* [Ad alanlarını ve derlemeleri yeniden adlandırma](http://nuget.codeplex.com/workitem/274)
* [NuPack projesini NuGet olarak yeniden adlandırma](http://nuget.codeplex.com/workitem/282)
* [Bağımlılıklar listesinin altına aşağıdaki metni ekleyin](http://nuget.codeplex.com/workitem/288)
* [Lisans kabulü Iletişim kutusunda lisans kabul metnini değiştirme](http://nuget.codeplex.com/workitem/291)
* [Paket listesinin üzerindeki lisans kabulü Iletişim kutusunda bulunan metni değiştirin](http://nuget.codeplex.com/workitem/292)
* [OData bir fwlink URL 'SI ile çalışmıyor](http://nuget.codeplex.com/workitem/304)
* [Paket Yöneticisi Kullanıcı arabirimi: sayfalama için kullanılan paket sayısının agresif önbelleklemesi](http://nuget.codeplex.com/workitem/317)
* [NuPack/NuGet-&gt; Paket Yöneticisi konsol hatası](http://nuget.codeplex.com/workitem/335)
* [Paket ekle Iletişim kutusu, önceden yüklenmiş paketlenmiş Için lisans kabulünü gösterir](http://nuget.codeplex.com/workitem/336)

## <a name="ctp-1"></a>CTP 1

Aşağıda, NuGet CTP 1 için düzeltilen Özellikler ve hataların bir listesi verilmiştir.

* [Paket uzantısının yeniden adlandırılması gerekir. nupack](http://nuget.codeplex.com/workitem/1)
* [Paket dosyasını klasöre taşı](http://nuget.codeplex.com/workitem/2)
* [Birleştirme Install &amp; PS komutları ekleme](http://nuget.codeplex.com/workitem/3)
* [Fiil-adı cmdlet 'leri için diğer adlar oluşturma](http://nuget.codeplex.com/workitem/4)
* [VS 'de çözüm değiştirilirken NuPack karıştırılır](http://nuget.codeplex.com/workitem/6)
* [' Packages ' çözüm klasörünü varsayılan olarak gizliyoruz](http://nuget.codeplex.com/workitem/11)
* [İçerik öğelerinde belirteç değiştirme desteği ekleyin.](http://nuget.codeplex.com/workitem/12)
* [NuPack. UI, PackageSource API 'sini kullanmalıdır](http://nuget.codeplex.com/workitem/26)
* [[Nupack. Core]: PackageManager paketleri yüklemeden önce yüklü olarak işaretler](http://nuget.codeplex.com/workitem/27)
* [Varsayılan projeyi çözümden silmek hala silinen projeyi varsayılan olarak gösterir](http://nuget.codeplex.com/workitem/30)
* [New-Package, "zaten pakette olduğundan belirtilen URI için bölüm eklenemiyor" ile başarısız olur.](http://nuget.codeplex.com/workitem/32)
* [Visual Studio GUI 'sinden "NuPack" dizelerini kaldırma](http://nuget.codeplex.com/workitem/35)
* [Bir TELIF hakkı. txt dosyasına Apache üstbilgisi ekleme](http://nuget.codeplex.com/workitem/36)
* [Update-PackageSource komutunu kaldır](http://nuget.codeplex.com/workitem/37)
* [Profil yüklenirken paket yöneticisi kullanılamıyor bir özel durum oluşturur](http://nuget.codeplex.com/workitem/39)
* [init. ps1, Install. ps1 ve Uninstall. ps1 ek durum almak için gerekir](http://nuget.codeplex.com/workitem/41)
* [Konsol ve GUI paketlerini tek bir pakette birleştirin](http://nuget.codeplex.com/workitem/42)
* [Kökte olmayan XML 'e uygulanırsa XML Transform mantığı çalışmaz](http://nuget.codeplex.com/workitem/43)
* [Paket kaynakları ayarlarını yönetme iletişim kutusu NuPack konsolu güncelleştirilmiyor](http://nuget.codeplex.com/workitem/44)
* [NuPack Console Kullanıcı arabirimi: ' paket akışı ' açılan listesini ' paket kaynağı ' olarak yeniden adlandır](http://nuget.codeplex.com/workitem/45)
* [NuPack konsol seçenekleri: ' depo Kullanıcı arabirimi ' NuPack konsolu ile tutarlı olacak şekilde yeniden adlandırma](http://nuget.codeplex.com/workitem/46)
* [Add-Package, IIS veya URL 'den açılan bir Web sitesine karşı başarısız oluyor](http://nuget.codeplex.com/workitem/53)
* [Paket Yöneticisi kaynağı FwLink Ile çalışmıyor](http://nuget.codeplex.com/workitem/55)
* [Varsayılan paket kaynağını ayarla](http://nuget.codeplex.com/workitem/59)
* [Seçeneğe yalnızca bir kaynak sağlandığında paket kaynakları eklenirken, varsayılan değer olarak kabul edilir.](http://nuget.codeplex.com/workitem/60)
* [Iletişim kutusu kullanıcı arabirimi sahte "son" paketleri gösterir](http://nuget.codeplex.com/workitem/62)
* [Seçenekler: iptal ' i tıklatmak değişiklikleri iptal etmez](http://nuget.codeplex.com/workitem/63)
* [Paket başvurusu ekleme Iletişim kutusu arama büyük/küçük harfe duyarsız olmalıdır](http://nuget.codeplex.com/workitem/65)
* [AssemblyInfo.cs dosyalarındaki şirket meta verilerini çözme](http://nuget.codeplex.com/workitem/67)
* [VSıX için sürüm numarası](http://nuget.codeplex.com/workitem/71)
* [Remove-Package: Using-? Yardım 'ı iki kez görüntüler](http://nuget.codeplex.com/workitem/72)
* [Proje düzeyi paketleri için yükleme/kaldırma paketleri yürütün](http://nuget.codeplex.com/workitem/74)
* [Bir nupack doğrulaması başarısız olduğunda sunucu akış oluşturamıyor](http://nuget.codeplex.com/workitem/90)
* [NuPack simgelerinden değiştirme gerekiyor](http://nuget.codeplex.com/workitem/94)
* [NTLM http proxy, paket akışında kimlik doğrulaması yapmaz.](http://nuget.codeplex.com/workitem/96)
* [İletişim kutusu, VS penceresinde her zaman ortalanmış olarak başlatılmaz](http://nuget.codeplex.com/workitem/100)
* [Paket ayrıntılarında alanların birçoğu iletişim kutusunda doldurulmuyor](http://nuget.codeplex.com/workitem/102)
* [İletişim kutusu kullanıcı arabirimi yazarların adlarını göstermiyor](http://nuget.codeplex.com/workitem/108)
* [Remove-Package için neden-Version](http://nuget.codeplex.com/workitem/113)
* [Iletişim kutusu kullanıcı arabirimindeki son sekmeyi kaldır](http://nuget.codeplex.com/workitem/115)
* [Iletişim kutusu kullanıcı arabirimi en az bir açıldıktan sonra çözüm klasörüne sağ tıkladığınızda VS kilitlenmesi.](http://nuget.codeplex.com/workitem/126)
* [Liste paketinin-yerel parametresini-yüklü olarak değiştir](http://nuget.codeplex.com/workitem/129)
* [Packages. xml ' i NuPack. config olarak yeniden adlandırın](http://nuget.codeplex.com/workitem/132)
* [Konsol, imleci satır sonuna zorlar](http://nuget.codeplex.com/workitem/135)
* [Remove-Package IntelliSense bozuk](http://nuget.codeplex.com/workitem/136)
* [Requirelicensekabulünü bayrağını. nuspec ve Feed ekleyin](http://nuget.codeplex.com/workitem/137)
* [LicenseUrl 'yi. nuspec biçimine ve paket akışına ekleyin](http://nuget.codeplex.com/workitem/138)
* [Kabul gerektiren pakete yönelik Install öğesine tıkladığınızda kabul Iletişim kutusu gösterilmelidir](http://nuget.codeplex.com/workitem/139)
* [Paket ekle Iletişim kutusuna vazgeçme metni ekleme](http://nuget.codeplex.com/workitem/140)
* [Paket Konsolu ilk kez çalıştırıldığında bir vazgeçme belgesi ekleyin](http://nuget.codeplex.com/workitem/143)
* [Paketi konsola yükledikten sonra vazgeçme belgesi görüntüle](http://nuget.codeplex.com/workitem/144)
* [. Nupack uzantısını. nupkg olarak yeniden adlandırın](http://nuget.codeplex.com/workitem/146)