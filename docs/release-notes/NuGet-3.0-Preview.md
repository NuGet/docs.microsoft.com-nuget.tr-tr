---
title: NuGet 3.0 Önizleme sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr NuGet 3.0 Önizleme için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 9389639476172d05556b95d589e429ddfe0e3026
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546471"
---
# <a name="nuget-30-preview-release-notes"></a>NuGet 3.0 Önizleme sürüm notları

[NuGet 2.9 RC sürüm notları](../release-notes/nuget-2.9-rc.md) | [NuGet 3.0 Beta sürüm notları](../release-notes/nuget-3.0-beta.md)

NuGet 3.0 Önizleme, Visual Studio 2015 Preview sürümünün bir parçası olarak 12 Kasım 2014'te yayımlanmıştır. NuGet 3.0 Önizleme yayımladık. Bu bizim için büyük bir yayın (Önizleme barındırabilir), ve değişiklikler hakkında geri bildirim almaya başlamanın heyecan duyuyoruz.

## <a name="visual-studio-2012"></a>Visual Studio 2012+

Bu NuGet 3.0 Önizleme, Visual Studio 2015 önizlemesi dahildir. Önizleme düşme Visual Studio 2012 ve Visual Studio 2013 için çok yakında ulaşmak için çalışıyoruz. Biz Amacımız için daha önce paylaşılan [Visual Studio 2010 için güncelleştirmeleri bulunmayarak](http://blog.nuget.org/20141002/visual-studio-2010.html), ve biz zor kararı yaptı.

## <a name="brand-new-ui"></a>Yeni kullanıcı Arabirimi

NuGet 3.0 önizleme hakkında dikkat edin ilk şey, yeni kullanıcı Arabirimimizi olabilir. Artık, kalıcı bir iletişim kutusu değil; Bu tam Visual Studio belge penceresi sunulmuştur. Bu, bir seferde birden çok proje (ve/veya çözüm) için kullanıcı arabirimini açın, başka bir monitöre penceresi yıkılıp, yaptığınız gibi vb. ancak da sabitleyin sağlar.

![Yeni NuGet kullanıcı Arabirimi](./media/NuGet-3.0-Preview/new-ui.png)

Kalıcı iletişim terk nedeniyle kullanılabilirlik farklılıklar dışında ayrıca yeni özellikleri yeni kullanıcı Arabiriminde bulunmaktadır.

### <a name="version-selection"></a>Sürüm seçimi

Belki de kullanıcı Arabirimi özelliğidir sürüm seçimi paket yükleme ve güncelleştirme--izin vermek için en çok istenen bu kullanıma sunulmuştur.

![Paket sürüm seçimi](./media/NuGet-3.0-Preview/version-selection.png)

Yüklerken veya güncelleştirilirken bir paket sürümü açılır bazı önemli sürümleriyle kolay seçimi için listenin en üstüne yükseltilen paket için kullanılabilir sürümlerin tümünü görmenizi sağlar. Artık en son olmayan belirli sürümlerini almak için PowerShell konsolunu kullanmanız gerekir.

### <a name="combined-installedonlineupdates-workflows"></a>Birleşik/Online/güncelleştirmelerin yüklü iş akışları

Önceki kullanıcı Arabirimimizi yüklü, çevrimiçi ve güncelleştirmeler için 3 sekme vardı. Listelenen paketlerin bu iş akışları için belirli ve akışları için belirli eylemleri kullanılabilir. Birçoğu genellikle gerekir, kullanıcılarımız, mantıksal olduğu görülüyor ancak bu ayrımı tarafından dönüş.

Şimdi burada yükleyebilir, güncelleştirme veya seçilen paketin nasıl aldığınız bağımsız olarak bir paket kaldırma birleşik bir deneyim sunuyoruz. Belirli iş akışlarıyla yardımcı olmak için şimdi görünür paketleri filtrelemek olanak tanıyan bir filtre açılan vardır, ancak paket için kullanılabilir eylemler tutarlı olması.

![Bir paketi Kaldır](./media/NuGet-3.0-Preview/uninstall-package.png)

"Yüklü" filtresini kullanarak, daha sonra kolayca hangilerinin kullanılabilir güncelleştirmeleri olan yüklü paketlerinizi görebilirsiniz ve ardından kaldırmak veya güncelleştirme paketi görmek için sürüm seçimi değiştirerek değiştirme eylemi kullanılabilir.

![Güncelleştirme paketi](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a>Sürüm birleştirme

Çözümünüz içinde birden çok proje içine yüklenmiş aynı paket yaygındır. Bazen her bir projeye yüklü sürümler birbirlerinden farklı ve kullanım verilerindeki sürümlerden birleştirme gereklidir. NuGet 3.0 Önizleme, yalnızca bu senaryo için yeni bir özellik sunmaktadır.

Çözüm düzeyinde paket Yönetimi penceresi, çözüme sağ tıklayıp çözüm için NuGet paketlerini Yönet'i seçerek tarafından erişilebilir. Birden çok proje, ancak kullanılıyor, farklı sürümleri yüklü olan bir paket seçin, burada, yeni bir "Birleştirme" eylemi kullanılabilir hale gelir. İçinde aşağıdaki ekran görüntüsünde `Newtonsoft.Json` içine yüklenmiş `SamplesClassLibrary` sürümüyle `6.0.4` içine yüklenmiş `SamplesConsoleApp` sürümüyle `5.0.4`.

![Sürümleri birleştirin](./media/NuGet-3.0-Preview/consolidate.png)

Tek bir sürüm birleştirilmesi için iş akışı şu şekildedir.

1. Seçin `Newtonsoft.Json` paket listesinde
1. Seçin `Consolidate` gelen `Action` açılan kutusu
1. Kullanım `Version` üzerine birleştirilecek sürümünü seçmek için açılır
1. Bu sürümü (seçili sürümü zaten projelerde gri unutmayın) üzerine birleşik projeleri için onay kutularını işaretleyin
1. Tıklayın `Consolidate` birleştirme gerçekleştirmek için düğme

### <a name="operation-previews"></a>İşlem önizlemeleri

Hangi işlemi gerçekleştiriyorsunuz--bağımsız olarak yükleme/Güncelleştirme/kaldırma--yeni kullanıcı Arabirimi artık projenize yaptığınız değişiklikleri önizlemek için bir yol sunar. Bu önizleme yüklenir, tüm yeni paketler, işlem sırasında değişmeyecektir paketleriyle birlikte kaldırılacak güncelleştirilir ve paketleri paketlerini gösterir.

Aşağıdaki örnekte, Microsoft.AspNet.SignalR yükleme oldukça değişiklikleri projeye sonuçlanacağını görebiliriz.

![SignalR yükleme Önizleme](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a>Yükleme Seçenekleri

PowerShell konsolunu kullanarak, birkaç önemli yükleme seçenekleri üzerinde denetim vardı. Bu özellikler artık UI getirdik. Artık bu bağımlılıkların sürümlerini nasıl seçileceğini bağımlılık çözümlemesi davranışını kontrol edebilirsiniz.

![Bağımlılık davranışı](./media/NuGet-3.0-Preview/dependency-behavior.png)

Ayrıca, projenizdeki dosyaları ile içerik paketleri dosyalarından çakıştığında gerçekleştirilecek eylemi belirtebilirsiniz.

![Dosya çakışması eylemi](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a>Sonsuz kayan

Bir bit Arabirimimizi geribildirim, her iki kaydırma sahip almak ve paketleri listelerken paradigmalarını sayfalama kullandık. Kısa listenin en alt kısma, sonraki sayfa numarası tıklayın ve ardından tekrar gidin oldukça sık kullanılan. Yeni kullanıcı Arabirimi ile kaydırmak--daha fazla disk belleği yeterlidir, böylece paket listesinde sonsuz kayan uyguladık.

![Sonsuz kayan](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a>İş yapmak, hızlı, Pretty olun kolaylaştırır

Bu yeni kullanıcı Arabirimi denemek size ulaşmak büyük bir heyecan duyuyoruz. Bu önizleme kilometre taşında biz kılavuzluğa odaklanmamı iyi eski adage, aşağıdaki "olun, iş, hızlı olun, oldukça kolaylaştırır." Bu önizleme sürümünde, biz çoğu elde bu ilk amacı--çalışır. Bu oldukça hızlı henüz hazır değil ve bu oldukça oldukça henüz hazır değil biliyoruz biliyoruz. Biz bu hedeflerine RC sürümü arasındaki yoğun şekilde kullanacağınız güven. Bu arada, bize hakkında Geri bildirimlerinizi öğrenmekten mutluluk duyarız *kullanılabilirlik* yeni kullanıcı arabirimi--işlemleri, iş akışları ve nasıl bunu *hissettirir* yeni kullanıcı arabirimini kullanma.

Birkaç eski kullanıcı Arabirimine karşılaştırıldığında kaldırdık işlevleri vardır. Bunlardan biri bilerek ve diğeri yalnızca zamanında tamamlamalarını kaydetmedi.

#### <a name="searching-all-package-sources"></a>"Tüm" Paket kaynaklarını arama

Eski kullanıcı Arabirimi tüm paket kaynaklarınız karşı paket arama yapmaya izin. Bu özellik kullanıcı Arabiriminde kaldırdık ve size geri çerçevesinde gerekmez. Tüm paket kaynaklarınız üzerinde arama işlemler gerçekleştirmek için kullanılan bu özellik, sonuçları birlikte dokuyarak ve sıralama seçiminize göre sonuçları sıralamak çalışır.

Aramanın ilgi düzeyini birlikte dokuyarak çok zor olduğunu bulduk. Google ve Bing karşı bir arama gerçekleştirme ve sonuçları birlikte weaving Imagine? Bu özellik ayrıca, yavaş, kolay *yanlışlıkla* kullanın ve biz düşünüyorsanız, nadiren gerçekten kullanışlı. Sorunları nedeniyle sunulan özellik hiçbir zaman Düzeltilen hata raporlarını üzerindeki bir dizi aldık.

#### <a name="update-all"></a>Tümünü Güncelleştir

Bir "Tümünü Güncelleştir" düğmesi yeni kullanıcı Arabiriminde henüz hiç eski Arabiriminde sağlamak için kullanılır. Biz bu özellik için RC sürümümüzü resurrect.

## <a name="new-clientserver-api"></a>Yeni istemci/sunucu API

Tüm müşterilerimize yeni paket Yönetimi kullanıcı ARABİRİMİ'daki yeni özelliklerin yanı sıra, biz de NuGet'ın istemci/sunucu protokolü için bazı uygulama ayrıntıları üzerinde çalışmalar. Yaptığımız iş "API v3" için paket geri yükleme ve paketlerin yüklenmesi gibi kritik senaryolar için yüksek kullanılabilirlik geçici olarak tasarlanmış olan NuGet oluşturmaktır. Yeni API REST üzerinde temel alır ve iletilir ve seçtiğiniz [JSON-LD](http://json-ld.org) bizim kaynak biçimi olarak.

NuGet 3.0 Önizleme bitler, paket kaynak açılır menüde "preview.nuget.org" adlı yeni bir paket kaynağı bakın. Bu paket kaynağını seçerseniz, yeni API'mizi yerine nuget.org için bağlanmak için kullanacağız. Kaynağı Önizle kullanıcı arabiriminde kullanılabilen yaptık, biz sınamak için gözden geçirme ve yeni API geliştirmeye devam ederken. NuGet 3.0 rc'de Yenilik olarak, bu yeni API v3 tabanlı paket kaynağı v2 tabanlı "nuget.org" Paket kaynağı yerini alır.

Biz API v3 haline gelmiştir koyarak yatırımın rağmen bu yeni özelliklerin tümünü de nuget.org dışındaki mevcut paket kaynaklarıyla çalışır anlamına gelir, var olan API v2 protokolü ile de çalışır yaptık.

## <a name="new-features-coming"></a>Kullanıma sunulacak yeni özellikler

Şimdi arasında 3.0 RTM, ayrıca kullanıcı Arabiriminde gördüğünüz bazı temel yeni NuGet özellik üzerinde çalışılmaktadır. Dikkat çekici yatırım alanlarının kısa bir listesi aşağıda verilmiştir:

1. Biz de Visual Studio ile işbirliği yapıyoruz ve almak için MSBuild takımlar [NuGet platformda derin](http://blog.nuget.org/20141014/in-the-platform.html).
1. Yükleme zamanı paket kuralları iptal ve bunun yerine yeni bir giriş tarafından bu kuralları paketleme zaman uygulamak için çalışıyoruz "yetkili" [paket bildirimi](http://blog.nuget.org/20141023/package-manifests.html).
1. NuGet kod tabanınızın farklı etki alanlarında Visual Studio'da paket Yönetimi ötesinde istemci ve sunucu bileşenleri yeniden kullanılabilir olması için yeniden düzenleme için çalışıyoruz.
1. Biz "Burada bir paket belirtebilirsiniz böylece özel bağımlılıklar" kavramı araştırdığınızı yalnızca uygulama ayrıntıları diğer paketleri üzerinde bağımlılıkları vardır ve bu bağımlılıkların en üst düzey bağımlılıkları olarak ortaya çıkması olmamalıdır.

## <a name="stay-tuned"></a>Bizi izlemeye devam edin

Lütfen gözünüzü [blogumuzu](http://blog.nuget.org) daha fazla ilerleme ve NuGet 3.0 duyuruları!