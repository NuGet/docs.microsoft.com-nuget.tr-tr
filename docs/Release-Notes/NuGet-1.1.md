---
title: NuGet 1.0 ve 1.1 sürüm notları | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: NuGet bilinen sorunları, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere 1.1 için sürüm notları.
keywords: Özellikler, dcr bilinen sorunlar, NuGet 1.1 sürüm notları, hata düzeltmeleri eklendi
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: dd320df2d725e58182cd908ce621571ea018b350
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-10-and-11-release-notes"></a>NuGet 1.0 ve 1.1 sürüm notları

[NuGet 1.2 sürüm notları](../release-notes/nuget-1.2.md)

NuGet 1.0 13 Ocak 2011'de serbest bırakıldı.  NuGet 1.1 12 Şubat 2011'de serbest bırakıldı.

## <a name="overview"></a>Genel Bakış

Bu belge, çeşitli yayınları NuGet ana Önizleme sürümü göre gruplandırılmış 1.0 için sürüm notları içeriyor.

NuGet aşağıdaki bileşenleri içerir:

* *NuGet.Tools.vsix* * hangi oluşur:
  * **Kitaplık Paketi iletişim ekleyin** * iletişim Visual Studio'dan göz atın ve paketleri yüklemek için kullanılır.
  * **Paket Yöneticisi Konsolu** * Powershell tabanlı Visual Studio içinde Konsolu.
* *NuGet komut satırı aracı* * aracı kullanılan paketleri oluşturmak (ve sonunda yayımlamak için).

NuGet araçları Visual Studio Uzantısı (*NuGet.Tools.vsix*) gerektirir:

* Visual Studio 2010 veya Visual Web Developer 2010 Express.

NuGet komut satırı aracını gerektirir:

* .NET framework sürüm 4

## <a name="installation"></a>Yükleme

Bunu kullanmak için [en son sürüm](http://nuget.codeplex.com/releases/view/52018):

* Önce eski yapınızın kaldırın. VS Bunu yapmak için yönetici olarak çalıştırmanız gerekir.
* Sahip olduğunuz tüm mevcut akışları kaldırın.
* İşaret eden yeni bir akış eklemek [ http://go.microsoft.com/fwlink/?LinkId=206669 ](http://go.microsoft.com/fwlink/?LinkId=206669).

## <a name="nuget-11"></a>NuGet 1.1

Bu sürümde giderilen sorunların listesi [burada bulunabilir](http://nuget.codeplex.com/workitem/list/advanced?keyword=&amp;status=All&amp;type=All&amp;priority=All&amp;release=NuGet%201.1&amp;assignedTo=All&amp;component=All&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0)

## <a name="nuget-10-rtm"></a>NuGet 1.0 RTM

Bir sorun RTM için bu yana RC giderilmiştir.

* [Sorun 474: Paketlerini kaldırma Çözümdeki tüm proje etkiler](http://nuget.codeplex.com/workitem/474)

## <a name="release-candidate"></a>Sürüm Adayı

Bu Sürüm Adayı'nda CTP 2'den yapılan değişiklikleri şunlardır: Hataların tam listesini görmek için sorun İzleyicisi'ni ziyaret edin.

* [Konsolundan paketi güncellemeden bağımlılıkları güncelleştirmez.](http://nuget.codeplex.com/workitem/443)
* [Depo yukarı ekleme paket Çekmeleri başvurusu (CTP1) paketini değil](http://nuget.codeplex.com/workitem/442)
* [Bir paketi güncellemeden bozuk başvurularda bırakır](http://nuget.codeplex.com/workitem/440)
* [Get-Package-güncelleştirmeler başarısız iletişim kutusu veya 'Tümü' birleşik kaynak konsolda seçildiğinde](http://nuget.codeplex.com/workitem/439)
* [Paket doğrulama hataları alma](http://nuget.codeplex.com/workitem/426)
* [Bir paketi paket Ekle iletişim kutusundan yüklendiğinde kullanıcıları uyarın.](http://nuget.codeplex.com/workitem/425)
* [Get-Package-sayıda paket güncelleştirilirken atar güncelleştirir](http://nuget.codeplex.com/workitem/424)
* [Nuspec dosyası yanlış yazılan sırasında hata işleme geliştirmek](http://nuget.codeplex.com/workitem/423)
* [Belirtilen dosyaları Nuget paketi yoksayar](http://nuget.codeplex.com/workitem/422)
* [İkinci son paket kaynağı kaldırarak ve ardından "Aşağı Taşı" VS kilitleniyor](http://nuget.codeplex.com/workitem/418)
* [Paketler yüklenirken derleme başvurusunu kaldırın](http://nuget.codeplex.com/workitem/413)
* [Ayarları iletişim kutusu açarken InvalidOperationException](http://nuget.codeplex.com/workitem/411)
* [Paket Yöneticisi konsolunda paket kaynağı için erişim anahtarı çalışmıyor](http://nuget.codeplex.com/workitem/410)
* [NuGet VS Ayarları iletişim erişim tuşları yanlış alanlarına odaklanmak](http://nuget.codeplex.com/workitem/409)
* [Paket kimliği IntelliSense çok sayıda öğe sorgu değil](http://nuget.codeplex.com/workitem/404)
* [Proje adı bir nokta karakteriyle projeye paket ekleme başarısız oldu](http://nuget.codeplex.com/workitem/403)
* [Sorun nuspec dosyaları belirtilen](http://nuget.codeplex.com/workitem/400)
* [Doğru resmi akışı yeni derleme kullanırken kayıtlı](http://nuget.codeplex.com/workitem/399)
* [Etiketler alanları yerine # kullanmalıdır](http://nuget.codeplex.com/workitem/397)
* [IPackageMetadata bazı yararlı bilgiler eksik](http://nuget.codeplex.com/workitem/388)
* [Rapor kötüye Bağlantısı Ekle iletişim kutusu için](http://nuget.codeplex.com/workitem/386)
* [Visual Studio'da paketleri sonları sıkıştırmasını App_Data kullanma](http://nuget.codeplex.com/workitem/380)
* [Uygulama etiketleri](http://nuget.codeplex.com/workitem/376)
* [Oluşturulacak bağımlılık boş paketiyle PackageBuilder sağlar](http://nuget.codeplex.com/workitem/373)
* [Paket sahipleri alan ekleme](http://nuget.codeplex.com/workitem/365)
* [VSIX araçları yerine NuGet Paket Yöneticisi söylemek için VSIX bildirimini güncelleştir](http://nuget.codeplex.com/workitem/364)
* [Tüm kaynak seçildiğinde get-Package komutu hata oluşturur.](http://nuget.codeplex.com/workitem/359)
* [Paket kaynakları Seçenekleri iletişim kutusunda sıralanmasına izin vermek](http://nuget.codeplex.com/workitem/356)
* [Güncelleştirme paketini eski sürümü kaldırmaz](http://nuget.codeplex.com/workitem/352)
* [Bağımlılıklar için uygulama sürüm aralığı belirtimi](http://nuget.codeplex.com/workitem/347)
* ["Yeni bir paket Ekle" tıklayarak Visual Studio kilitleniyor](http://nuget.codeplex.com/workitem/346)
* [Yüklemeleri ve derecelendirmeleri Ekle paket iletişim kutusunda görüntüleyin](http://nuget.codeplex.com/workitem/345)
* [Paket kaynaklarını iletişim arasında değiştirme etkin kaynak güncelleştirmez](http://nuget.codeplex.com/workitem/344)
* [Paket Yöneticisi konsol penceresi için anahtar bağlamayı kaldırın](http://nuget.codeplex.com/workitem/339)
* [Install-Package bir cmdlet adı olarak tanınmıyor...](http://nuget.codeplex.com/workitem/338)
* [Bir paket bağımlılıkları normal akışlarına akışı yerel bir yükleme güvenilmedi](http://nuget.codeplex.com/workitem/332)
* [RemoveDependencies hala kullanımda olan bağımlılıkları atlayın](http://nuget.codeplex.com/workitem/331)
* [Özgün sayfa isteği verir ancak sayfa gezintisi iptal edilirse, kullanıcı başka bir sayfaya gidilemiyor](http://nuget.codeplex.com/workitem/325)
* [NuPack.Server performansını akışları hizmet vermek için çok sayıda paketleri araştırın.](http://nuget.codeplex.com/workitem/324)
* [I filtre ikinci kez bir paket için "Yeni" Paket kaynağı yerine daha önce seçilen kaynağı kullanır.](http://nuget.codeplex.com/workitem/321)
* [Varsayılan paket kaynağı iletişim kutusu "Çevrimiçi" sekmesinde seçerken seçilmelidir.](http://nuget.codeplex.com/workitem/320)
* [Varsayılan olarak yüklü paketleri paket listeleme göstermelidir](http://nuget.codeplex.com/workitem/309)
* [Derleme başvurusu HintPaths](http://nuget.codeplex.com/workitem/294)
* [Paket Yöneticisi konsolu açılırken özel durumu](http://nuget.codeplex.com/workitem/268)
* [Konsol IntelliSense tüm akış indirir](http://nuget.codeplex.com/workitem/259)
* ['Default' paket kaynağı 'Active' adlandırılmamalıdır.](http://nuget.codeplex.com/workitem/258)
* [Paket kaynaklarını UI: Tamam tuşuna basarak eklerseniz yeni kaynak adı/kaynak alanları boş](http://nuget.codeplex.com/workitem/257)
* [Yüklü paketler sayısı büyük olduğunda iletişim Süper yavaş olur](http://nuget.codeplex.com/workitem/243)
* [Tanımlayıcı adlı derlemeler için bağlama yeniden yönlendirmeleri desteği](http://nuget.codeplex.com/workitem/238)
* [Paketi Başvurusu Ekle... Paket kaynağı için aşağı açılan eklemek için kullanıcı Arabirimi](http://nuget.codeplex.com/workitem/226)
* [NuPack yapılandırma dönüştürme config dosya adının agnostically desteklemesi gerekir](http://nuget.codeplex.com/workitem/224)
* [Ana yolu NuPack.exe kılınmadı olmasını sağlar](http://nuget.codeplex.com/workitem/222)
* [Paket kaynak geri dönüş davranışı](http://nuget.codeplex.com/workitem/204)
* [GUI üzerinde kilitlenme](http://nuget.codeplex.com/workitem/201)
* [Sıralama seçenekleri paket iletişim eklemek için Ekle](http://nuget.codeplex.com/workitem/179)
* [Paket Yöneticisi konsolu temizlemek için kısayol tuşu](http://nuget.codeplex.com/workitem/174)
* [PowerConsole NuPack konsolu, başarısız olmasına neden olur.](http://nuget.codeplex.com/workitem/166)
* [Konsol ve paket iletişim kutusu Ekle kullanıcı aracısı isteklerinde ayarlamanız gerekir](http://nuget.codeplex.com/workitem/141)
* [Sürüm numarasını VSIX ve NuPack.exe yapı ayarlayın.](http://nuget.codeplex.com/workitem/134)
* [Ortak PowerShell parametrelerini gizlemek-?](http://nuget.codeplex.com/workitem/118)
* [Ekle - konsol komutları için ayrıntılı Yardım](http://nuget.codeplex.com/workitem/110)
* [Geçerli paket kaynağında seçme paket iletişim sağlamalıdır ekleme](http://nuget.codeplex.com/workitem/88)
* [Taşıma NuPack.Core sınıflara farklı ad alanları](http://nuget.codeplex.com/workitem/50)
* [Cmdlet'leri için Yardım ekleme](http://nuget.codeplex.com/workitem/23)
* [Paketi yükledikten sonra karma akış değerden doğrulayın](http://nuget.codeplex.com/workitem/18)

## <a name="ctp-2"></a>CTP 2

CTP 2'de yapılan en önemli değişiklikler şunlardır:

* Bir OData Hizmeti uç noktası için ATOM akışı paket anahtarlamalı: NuGet CTP2 sürümüne yükseltirseniz, bir paket kaynağı olarak aşağıdaki URL'yi eklediğinizden emin olun: `https://feed.nuget.org/ctp2/odata/v1/`.
* Add-Package komutu yeniden adlandırılmış *Install-Package*.
* Güncelleştirilmiş `.nuspec` biçimi. `.nuspec` Biçimi artık içerir *iconUrl* Paketi Ekle iletişim kutusunda görüntülenecek bir 32 x 32 png simgesi belirtmek için alan. Bu nedenle, paketinizi ayırt etmek için ayarladığınızdan emin olun. `.nuspec` Biçimi de içeren yeni *projectUrl* paketinizi hakkında daha fazla bilgi sağlayan bir web sayfasında işaret etmek için kullanabileceğiniz alan.

Bu yapı ile eski çalışmaz `.nupkg` dosyaları. Null başvuru özel durumları alırsanız, eski kullanmakta olduğunuz `.nupkg` dosya ve güncelleştirilmiş ile yeniden oluşturmak gereken [NuGet komut satırı aracı](http://nuget.codeplex.com/releases/52017/download/165468).

NuGet CTP (küçük kod Temizlemeler vb. için hatalar dahil değildir.) 2 için düzeltilen hatalar ve özelliklerinin bir listesi verilmiştir.

* [Hata unpacking paket derlemeleri zaman WINS'te bir derlemenin TargetFramework.](http://nuget.codeplex.com/workitem/10)
* [Daha fazla bulunabilir NuPack konsol penceresi oluşturma](http://nuget.codeplex.com/workitem/14)
* [ILMerge nupack.exe sürüm](http://nuget.codeplex.com/workitem/19)
* [Daha iyi hata/özel durum işleme](http://nuget.codeplex.com/workitem/24)
* [[Nupack.Core]: PackageManager akış ile ilgili hataları kolaylıkla idare](http://nuget.codeplex.com/workitem/28)
* [Yeni bir simge için konsolu gerekir](http://nuget.codeplex.com/workitem/29)
* [İletişim kutusunda dizeleri yerelleştirme](http://nuget.codeplex.com/workitem/38)
* [NuPack önbellekleri indirilen bellekte .nupack dosyaları](http://nuget.codeplex.com/workitem/40)
* [NuPack konsolu: konsol görüntüleme için varsayılan kısayol değiştirme](http://nuget.codeplex.com/workitem/48)
* [ProjectSystem ortak özellikleri için varsayılan değerleri desteklemesi gerekir](http://nuget.codeplex.com/workitem/49)
* [Yalnızca bir nuspec dosyası ile bir klasörde nupack.exe çalıştıran bu nuspec kullanmanız gerekir](http://nuget.codeplex.com/workitem/52)
* [Proje menüsü bile zaman proje/çözüm yüklenen gösterir](http://nuget.codeplex.com/workitem/54)
* [codebase temiz bir kopyası üzerinde Build.cmd başarısız](http://nuget.codeplex.com/workitem/56)
* [Güncelleştirmeler kullanılabilir özelliği](http://nuget.codeplex.com/workitem/57)
* [İletişim kutusunda: iletişim kutusu üzerinden bir paket ekleme istemi konsolda kaldırır](http://nuget.codeplex.com/workitem/73)
* [Bir paketi 'Yükle' ye tıklayıp ekleme genellikle hiçbir görsel geribildirim ile yavaş](http://nuget.codeplex.com/workitem/80)
* [My yüklü paketleri hangisinin güncelleştirmelerine sahip bulmak için bir yolu yoktur.](http://nuget.codeplex.com/workitem/82)
* [İletişim kutusunda yüklü bir paketle güncelleştirmek için bir yolu yoktur.](http://nuget.codeplex.com/workitem/83)
* [Yüklü bir paketle iletişim kutusunda kaldırmak için bir yolu yoktur](http://nuget.codeplex.com/workitem/84)
* [&ldquo;Paketi Başvurusu Ekle&hellip; &rdquo; yüklü başvuruları bağlam menüsünde görüntülenir](http://nuget.codeplex.com/workitem/85)
* [Bir paket konsolundan güncelleştirdikten sonra bu sürümü eski ve yeni sürümü yüklü olarak gösterir](http://nuget.codeplex.com/workitem/86)
* [Konsolda etkinliğini iletişim kullanılırken, kullanımdan sonra kaybolur](http://nuget.codeplex.com/workitem/87)
* [Temizleme komut satırı nupack.exe içinde ayrıştırma](http://nuget.codeplex.com/workitem/89)
* [Paket kaynaklarını için kolay bir ad ekleyin](http://nuget.codeplex.com/workitem/98)
* [Güncelleştirme .nuspec de dahil olmak üzere paket simgeler desteklemek için](http://nuget.codeplex.com/workitem/103)
* [Akış UI URL kopyalanması izin vermez](http://nuget.codeplex.com/workitem/105)
* [Daha iyi remove-package hata işleme.](http://nuget.codeplex.com/workitem/107)
* [Konsol penceresinde yazarak imleç odaklanmak bağlıdır](http://nuget.codeplex.com/workitem/112)
* [Hata iletileri awful arayın](http://nuget.codeplex.com/workitem/116)
* [Remove-Package performans yüklü olmayan bir paket için bozuk](http://nuget.codeplex.com/workitem/117)
* [Hiçbir paket kaynaklarını olduğunda bir paketi kaldırma başarısız](http://nuget.codeplex.com/workitem/119)
* [Paket kaynağı kullanılamadığında remove-Package başarısız](http://nuget.codeplex.com/workitem/120)
* [Paket meta verileri ve akış başlık ekleyin.](http://nuget.codeplex.com/workitem/125)
* [Add kaynak parametresi Ekle-Package dön](http://nuget.codeplex.com/workitem/127)
* [Paket listeleme olmalıdır - kaynak parametresi](http://nuget.codeplex.com/workitem/128)
* [Güncelleştirme NuPack.Server NuPack kullanıcı aracısı için yükleme paketi gerektirir](http://nuget.codeplex.com/workitem/142)
* [Lisans kabulünü iletişim lisansları kabul gerektiren tüm bağımlılıkları listesinde gerekir](http://nuget.codeplex.com/workitem/145)
* [Bir paket akışta oluşturduğunda hatayla oturum](http://nuget.codeplex.com/workitem/150)
* [NuPack.exe boş değil izin vermelidir &lt;licenseurl&gt; öğesi](http://nuget.codeplex.com/workitem/152)
* [Get-Package, Add-Package Install-Package ve Remove-Package kaldırma paketi için paket listeleme yeniden adlandırın](http://nuget.codeplex.com/workitem/155)
* [Çözüm Gezgini gelen paket Başvuru Ekle menü öğesini kullanarak Visual Studio kilitleniyor](http://nuget.codeplex.com/workitem/158)
* ["Kullanılabilir paket kaynakları" etiketli bir iki nokta üst üste eksik](http://nuget.codeplex.com/workitem/160)
* [Ortası .nuspec xml öğesi büyük/küçük harf tutarlı bir şekilde ortası büyük olmak](http://nuget.codeplex.com/workitem/161)
* ['Yönetici' bit açmak NuPack VSIX'ın bildirimi gerekiyor](http://nuget.codeplex.com/workitem/162)
* [Hiçbir akışlarıyla paket listeleme çalıştırırsanız, null ref hata Al](http://nuget.codeplex.com/workitem/164)
* [nuget.exe: specify destination path](http://nuget.codeplex.com/workitem/171)
* [Powershell hataları WinXP paketi Yönetimi konsolunu açma](http://nuget.codeplex.com/workitem/175)
* [Paket listesi yüklemeye çalışırken VS kilitleniyor](http://nuget.codeplex.com/workitem/176)
* [Meta paket (hiçbir dosya, yalnızca bağımlılıklar) izin ver](http://nuget.codeplex.com/workitem/180)
* [Powershell 2.0 modülü PowerShell Betiği Dönüştür](http://nuget.codeplex.com/workitem/181)
* [Hedef belirtildiğinde PathResolver yol bölümü önce gelen joker karakterleri atmak](http://nuget.codeplex.com/workitem/183)
* [Hiçbir bağımlılık](http://nuget.codeplex.com/workitem/186)
* [Elmah yüklenirken hata oluştu](http://nuget.codeplex.com/workitem/192)
* [Config dönüşümler çalışmıyor doğru ile &lt;configsections&gt;](http://nuget.codeplex.com/workitem/194)
* [Değişkeni ' $genel: projectCache' değil ayarlanmış olduğundan alınamıyor](http://nuget.codeplex.com/workitem/203)
* [MSBuild görevi NuPack paketleri oluşturmak için](http://nuget.codeplex.com/workitem/205)
* [Paket listeleme arama ve filtreleme desteklemesi gerekir](http://nuget.codeplex.com/workitem/206)
* [Her zaman bir lisans URL'si için paket yazarına sağlıyorsa, bir bağlantı için lisans görüntüleme](http://nuget.codeplex.com/workitem/208)
* [Bazen "Erişim engellendi" özel durumuyla Remove-Package](http://nuget.codeplex.com/workitem/213)
* [Birim testleri başarısız: InvalidPackageIsExcludedFromFeedItems &amp; CreatingFeedConvertsPackagesToAtomEntries](http://nuget.codeplex.com/workitem/214)
* [Belirli framework sürümü bulunamazsa dosyaları için bir geri dönüş/varsayılan kümesi izin ver](http://nuget.codeplex.com/workitem/223)
* [Paketi Başvurusu Ekle... Kullanıcı Arabirimi bir paket kaldırılamıyor](http://nuget.codeplex.com/workitem/225)
* [Paketi başvurusu varsa Studio'nun kilitlenmesine veya daha fazla proje kaldırılmadan ekleme](http://nuget.codeplex.com/workitem/228)
* [Config dönüştürmesi web.debug.config dosya üzerinde çalıştığınız görünmüyor](http://nuget.codeplex.com/workitem/229)
* [init.ps1 özel paketi tetikleme değil](http://nuget.codeplex.com/workitem/237)
* [ENTER tuşuna basarsanız otomatik olarak kapanır şekilde yolları feedlist eklerken, varsayılan düğme Tamam olarak ayarlanır](http://nuget.codeplex.com/workitem/240)
* [Kaldırma girişimi bir bağımlılık VS 2 katı bir satırda denediyseniz kilitleniyor](http://nuget.codeplex.com/workitem/241)
* [Proje URL'sini Paketi Ekle iletişim kutusunda görüntüleyin](http://nuget.codeplex.com/workitem/253)
* [Varsayılan yüklenen paketler için Add-Package iletişim](http://nuget.codeplex.com/workitem/254)
* [Paket iletişim kutusu Ekle menü öğesini değiştirin.](http://nuget.codeplex.com/workitem/261)
* [Ad alanları ve derlemeler yeniden adlandırın](http://nuget.codeplex.com/workitem/274)
* [Nuget'e NuPack projesini yeniden adlandırma](http://nuget.codeplex.com/workitem/282)
* [Bağımlılıkları listesi altında aşağıdaki metni ekleyin](http://nuget.codeplex.com/workitem/288)
* [Lisans kabulünü iletişim kutusunda lisans kabulü metni değiştirme](http://nuget.codeplex.com/workitem/291)
* [Lisans kabulünü iletişim paketlerin listesini yukarıda metinde değiştirme](http://nuget.codeplex.com/workitem/292)
* [OData fwlink URL ile çalışmıyor](http://nuget.codeplex.com/workitem/304)
* [Paket Yöneticisi kullanıcı Arabirimi: agresif disk belleği için kullanılan paket sayısı önbelleğe alınmasını üzerinden](http://nuget.codeplex.com/workitem/317)
* [NuPack / NuGet -&gt; Paket Yöneticisi konsolu hata](http://nuget.codeplex.com/workitem/335)
* [Lisans kabulünü için zaten yüklü paketlenmiş paket iletişim kutusu görüntüler ekleme](http://nuget.codeplex.com/workitem/336)

## <a name="ctp-1"></a>CTP 1

NuGet CTP 1 için düzeltilen hatalar ve özelliklerinin bir listesi verilmiştir.

* [Paket uzantısı .nupack yeniden adlandırılmamalıdır](http://nuget.codeplex.com/workitem/1)
* [Paket dosyası klasöre taşıyın](http://nuget.codeplex.com/workitem/2)
* [Yükleme birleştirme &amp; PS Ekle komutları](http://nuget.codeplex.com/workitem/3)
* [Fiil-isim cmdlet'leri için diğer adlar oluşturma](http://nuget.codeplex.com/workitem/4)
* [NuPack içinde VS çözüm geçiş yaparken kafası](http://nuget.codeplex.com/workitem/6)
* [Biz 'packages' çözüm klasörü varsayılan olarak gizler](http://nuget.codeplex.com/workitem/11)
* [Belirteç değiştirme desteği içerik öğelerinde ekleyin.](http://nuget.codeplex.com/workitem/12)
* [NuPack.UI PackageSource API'sini kullanmanız gerekir](http://nuget.codeplex.com/workitem/26)
* [[Nupack.Core]: PackageManager paketler yüklenmeden önce yüklü olarak işaretler](http://nuget.codeplex.com/workitem/27)
* [Çözüm silme varsayılan projeden silinmiş projenin varsayılan olarak hala gösterir.](http://nuget.codeplex.com/workitem/30)
* [Yeni paket başarısız "paketin içinde olduğundan ile bölümü belirtilen URI için eklenemiyor."](http://nuget.codeplex.com/workitem/32)
* [Visual Studio GUI "NuPack" dizeleri Kaldır](http://nuget.codeplex.com/workitem/35)
* [Apache üst bilgisi için bir COPYRIGHT.txt dosyası ekleme](http://nuget.codeplex.com/workitem/36)
* [Güncelleştirme PackageSource komutu kaldırın](http://nuget.codeplex.com/workitem/37)
* [Paket Yöneticisi profili yüklenirken bir durum oluşturduğunda kullanılamaz](http://nuget.codeplex.com/workitem/39)
* [Ek durum almak için init.ps1, install.ps1 ve uninstall.ps1 gerekir](http://nuget.codeplex.com/workitem/41)
* [Konsol ve GUI paketleri bir pakete birleştirin](http://nuget.codeplex.com/workitem/42)
* [XML dönüştürme mantığı kök dizininde değilse XML uyguladıysanız çalışmıyor](http://nuget.codeplex.com/workitem/43)
* [Paket kaynağı Ayarları iletişim kutusu NuPack konsol güncelleştirmemeyi yönetme](http://nuget.codeplex.com/workitem/44)
* [NuPack konsolu kullanıcı arabirimini: 'Paket kaynağı' için 'paket akışı' açılan listeyi yeniden adlandırma](http://nuget.codeplex.com/workitem/45)
* [NuPack konsol seçenekleri: 'Depo NuPack konsolu ile tutarlı olacak şekilde UI' Yeniden Adlandır](http://nuget.codeplex.com/workitem/46)
* [IIS veya bir URL açılmış bir Web sitesi karşı Paketi Ekle başarısız](http://nuget.codeplex.com/workitem/53)
* [Paket Yöneticisi kaynak FwLink ile çalışmıyor](http://nuget.codeplex.com/workitem/55)
* [Varsayılan paket kaynağı ayarla](http://nuget.codeplex.com/workitem/59)
* [Yalnızca bir kaynak sağlandığında paket kaynaklarını seçeneğinde, eklerken, varsayılan olduğunu varsayalım.](http://nuget.codeplex.com/workitem/60)
* [Sahte "son" paketleri iletişim UI gösterir](http://nuget.codeplex.com/workitem/62)
* [Seçenekler: İptal'i tıklatarak değişiklikleri iptal etmez](http://nuget.codeplex.com/workitem/63)
* [Paket başvuru iletişim arama büyük küçük harfe duyarlı ekleme](http://nuget.codeplex.com/workitem/65)
* [Şirket meta verileri AssemblyInfo.cs dosyalarında Düzelt](http://nuget.codeplex.com/workitem/67)
* [VSIX için sürüm numarası](http://nuget.codeplex.com/workitem/71)
* [Remove-Package: Kullanma-? iki kez görüntüler Yardım](http://nuget.codeplex.com/workitem/72)
* [Yükleme ve kaldırma paketler proje düzeyi paketler için yürütme](http://nuget.codeplex.com/workitem/74)
* [Sunucu bir nupack doğrulama başarısız olduğunda akış oluşturamıyor](http://nuget.codeplex.com/workitem/90)
* [NuPack simgeler değiştirmeniz gerekiyor](http://nuget.codeplex.com/workitem/94)
* [NTLM http proxy akış paket kimliğini doğrulamaz.](http://nuget.codeplex.com/workitem/96)
* [İletişim kutusu her zaman VS penceresinde ortalanmış başlamıyor](http://nuget.codeplex.com/workitem/100)
* [Paketleri ayrıntıları alanların çoğu iletişim kutusunda doldurulmaz](http://nuget.codeplex.com/workitem/102)
* [Yazarların adları iletişim UI göstermez](http://nuget.codeplex.com/workitem/108)
* [Neden - Remove-Package için sürüm](http://nuget.codeplex.com/workitem/113)
* [Son iletişim UI sekmesinde kaldırın](http://nuget.codeplex.com/workitem/115)
* [VS kilitlenme sağ tıklattığınızda iletişim UI en az bir açtıktan sonra Çözüm klasörü tıklatın.](http://nuget.codeplex.com/workitem/126)
* [Değişiklik listesi paket yerel parametresinin-yüklü](http://nuget.codeplex.com/workitem/129)
* [Packages.XML NuPack.config için yeniden adlandırma](http://nuget.codeplex.com/workitem/132)
* [Konsol imleç satırın sonuna zorlar.](http://nuget.codeplex.com/workitem/135)
* [Remove-Package IntelliSense bozuluyor](http://nuget.codeplex.com/workitem/136)
* [RequireLicenseAcceptance bayrağı .nuspec ve akış ekleme](http://nuget.codeplex.com/workitem/137)
* [LicenseUrl .nuspec biçimlendirmek ve paket akışı Ekle](http://nuget.codeplex.com/workitem/138)
* [Kabul gerektiren paketi için Yükle'yi tıklayarak kabul iletişim göstermesi gerekir](http://nuget.codeplex.com/workitem/139)
* [Vazgeçme Ekle paket iletişim kutusuna ekleme](http://nuget.codeplex.com/workitem/140)
* [Vazgeçme zaman paket konsol ilk kez çalıştırma ekleme](http://nuget.codeplex.com/workitem/143)
* [Konsolunda paketi yüklendikten sonra sorumluluk reddi görüntüleme](http://nuget.codeplex.com/workitem/144)
* [.Nupack uzantısı için .nupkg yeniden adlandır](http://nuget.codeplex.com/workitem/146)