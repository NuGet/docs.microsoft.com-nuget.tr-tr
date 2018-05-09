---
title: NuGet 3.0 Preview sürüm notları
description: NuGet 3.0 bilinen sorunları, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere önizleme için sürüm notları.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 67c217e52d975ed8f6889cd69f9b7e0d52b3a119
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-30-preview-release-notes"></a>NuGet 3.0 Preview sürüm notları

[NuGet 2.9 RC sürüm notları](../release-notes/nuget-2.9-rc.md) | [NuGet 3.0 Beta sürüm notları](../release-notes/nuget-3.0-beta.md)

NuGet 3.0 Önizleme 12 Kasım 2014 Visual Studio 2015 Preview sürümünün bir parçası olarak serbest bırakıldı. NuGet 3.0 Önizleme yayımladık. Bu (Önizleme barındırabilir) bize için büyük bir sürüm olduğundan, ve bizim değişiklikleri geri alma Başlat mutluluk çalışıyoruz.

## <a name="visual-studio-2012"></a>Visual Studio 2012+

Bu NuGet 3.0 Önizleme Visual Studio 2015 Preview sürümünde dahil edilir. Önizleme düşme Visual Studio 2012 ve Visual Studio 2013 için çok yakında ulaşmak için çalışıyoruz. Bizim hedefi daha önce paylaşılmıştı [Visual Studio 2010 için güncelleştirmeleri Durdur](http://blog.nuget.org/20141002/visual-studio-2010.html), ve zor kararı vermiyoruz.

## <a name="brand-new-ui"></a>Yeni kullanıcı Arabirimi

NuGet 3.0 önizleme hakkında fark ilk şey bizim yepyeni UI'dır. Artık, kalıcı bir iletişim kutusu değil; Bu tam bir Visual Studio belge penceresine sunulmuştur. Bu, birden çok proje (ve/veya çözüm) ilişkin kullanıcı Arabirimi seferde açmak için başka bir izleme penceresi kesmeden devre dışı, yaptığınız gibi vb. ancak yerleştirme olanak sağlar.

![Yeni NuGet kullanıcı Arabirimi](./media/NuGet-3.0-Preview/new-ui.png)

Kalıcı iletişim terk nedeniyle kullanılabilirlik farklar, biz de yeni kullanıcı Arabiriminde çok sayıda yeni özellikler vardır.

### <a name="version-selection"></a>Sürüm seçimi

Belki de UI özelliktir paketi yükleme ve güncelleştirme--sürüm seçimi izin vermek için en çok istenen bu kullanıma sunulmuştur.

![Paket sürümü seçimi](./media/NuGet-3.0-Preview/version-selection.png)

Yükleme veya bir paket güncelleştirme olup olmadığını sürümü açılır listenin kolay seçimi için yükseltilen bazı önemli sürümleriyle paket için kullanılabilir sürümlerin tümünü görmenizi sağlar. Artık son olmayan belirli sürümlerini almak için PowerShell konsolunu kullanmanız gerekir.

### <a name="combined-installedonlineupdates-workflows"></a>Birleşik yüklü/Online/güncelleştirmeleri iş akışları

Önceki kullanıcı arabirimimizi yüklü, çevrimiçi ve güncelleştirmeleri için 3 sekmeleri vardı. Listelenen paketler bu iş akışları için belirli ve iş akışları için belirli eylemler kullanılabilir. Mantıksal birçoğu genellikle olur, heard seemed sırada Bu ayrım tarafından dönüş.

Şimdi buradan yüklemek, güncelleştirme veya seçilen paketin nasıl aldığınız bakılmaksızın bir paketi kaldırma birleşik bir deneyim sunuyoruz. Belirli iş akışlarıyla yardımcı olmak için artık görünür paketleri filtrelemek olanak sağlayan bir filtre açılan sahibiz, ancak paket için kullanılabilir eylemleri tutarlı.

![Bir paketi kaldırma](./media/NuGet-3.0-Preview/uninstall-package.png)

"Yüklü" filtreyi kullanarak, daha sonra kolayca hangilerinin güncelleştirmelere sahip, paketlerinizi yüklü görebilirsiniz ve ardından kaldırmak veya güncelleştirme paketi görmek için sürüm seçimi değiştirerek eylemi kullanılabilir değiştirin.

![Güncelleştirme paketi](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a>Sürüm birleştirme

Birden çok projelerine çözümünüzdeki yüklü aynı paketin yaygındır. Bazen her projeye yüklü sürümleri parçalayın kayma ve kullanımda sürümleri birleştirmek gereklidir. NuGet 3.0 Önizleme yalnızca bu senaryo için yeni bir özellik sunmaktadır.

Çözüm düzeyi paket Yönetimi penceresi, çözüm üzerinde sağ tıklayıp çözüm için NuGet paketlerini Yönet'i seçerek tarafından erişilebilir. Buradan, birden çok projelerine ancak kullanılıyor, farklı sürümlerle yüklü bir paket seçerseniz yeni bir "Birleştir" eylemi kullanılabilir hale gelir. Aşağıdaki ekran içinde `Newtonsoft.Json` içine yüklenmiş `SamplesClassLibrary` sürümüyle `6.0.4` içine yüklenmiş `SamplesConsoleApp` sürümüyle `5.0.4`.

![Sürümleri birleştirin](./media/NuGet-3.0-Preview/consolidate.png)

Tek sürümü birleştirilmesi için iş akışı aşağıda verilmiştir.

1. Seçin `Newtonsoft.Json` paket listesinde
1. Seçin `Consolidate` gelen `Action` açılır
1. Kullanım `Version` üzerine birleştirilecek sürümü seçmek için açılır
1. (Seçili sürümü zaten projelerde gri unutmayın) sürümünün üzerine Birleştirilmiş projeler için kutuları işaretleyin
1. Tıklatın `Consolidate` birleştirme gerçekleştirmek için düğmesi

### <a name="operation-previews"></a>İşlemi önizlemeleri

Gerçekleştirmekte--hangi işlemi bağımsız olarak yükleme/Güncelleştirme/kaldırma--yeni kullanıcı Arabirimi şimdi projenize yapılan değişiklikleri önizlemek için bir yol sunar. Bu önizleme yüklenecek, tüm yeni paketler güncelleştirilir ve paketler, işlemi sırasında değiştirilmez paketleri birlikte kaldırılacak paketleri gösterir.

Aşağıdaki örnekte Microsoft.AspNet.SignalR yükleme oldukça birkaç değişiklikleri projeye neden olacağını görebilirsiniz.

![SignalR yükleme Önizleme](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a>Yükleme Seçenekleri

PowerShell konsolunu kullanarak, birkaç önemli yükleme seçenekleri üzerinde denetim karşılaşmışsınız. Bu özellikleri artık UI getirdik. Şimdi bağımlılıkları sürümlerini nasıl seçileceğini bağımlılık çözümlemesi davranışını kontrol edebilirsiniz.

![Bağımlılık davranışı](./media/NuGet-3.0-Preview/dependency-behavior.png)

Ayrıca, içerik dosyaları paketlerinden projeniz zaten dosyalarında çakışıyor olduğunda gerçekleştirilecek eylem belirtebilirsiniz.

![Dosya çakışma eylemi](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a>Sonsuz kaydırma

Bir bit Geri bildiriminiz bizim kullanıcı Arabirimi üzerindeki iki kaydırma sahip almak ve paketleri listelerken örneklerinde disk belleği için kullanılır. Kısa listenin alt kısmına kaydırın, sonraki sayfa numarası tıklayın ve ardından yeniden kaydırın zorunda oldukça ortak. Yeni kullanıcı Arabirimi olmadan yalnızca kaydırma--daha fazla disk belleği gerekir böylece sonsuz paket listesinde kaydırma uyguladık.

![Sonsuz kaydırma](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a>İş Oluştur, hızlı, Pretty olun oluştur

Denemek size bu yeni UI alacağınızı Mutluluk duyuyoruz. Bu önizleme kilometre taşı sırasında biz edilmiş iyi eski adage, aşağıdaki "olun, iş, hızlı olun, oldukça kolaylaştırır." Bu Önizleme'de, biz çoğu elde bu ilk amacı--çalışır. Bu oldukça hızlı henüz değildir ve bu oldukça oldukça henüz değil biliyoruz biliyoruz. Biz bu hedefleri RC sürüm arasındaki üzerinde çalışan güven. Bu arada, biz hakkındaki görüşlerinizi almak isteriz *kullanılabilirlik* yeni UI--iş akışları, işlemleri ve nasıl onu *hissi* yeni kullanıcı arabirimini kullanmak için.

Birkaç eski UI karşılaştırıldığında kaldırdık işlevleri vardır. Bunlardan birini bilerek ve diğeri yalnızca zamanında tamamlamalarını alamadık.

#### <a name="searching-all-package-sources"></a>"Tümü" Paket kaynaklarını arama

Eski kullanıcı Arabirimi, tüm paket kaynaklarınız karşı paket arama yapmak izin verilen. Bu özellik kullanıcı Arabiriminde kaldırdık ve size geri hale getirme olmaz. Tüm paket kaynaklarınız karşı arama işlemleri gerçekleştirmek için kullanılan bu özellik, sonuçları birlikte weave ve sıralama seçiminize bağlı sonuçları sıralamak çalışır.

Arama kesinliğini birlikte weave gerçekten sabit olduğunu buldu. Google ve Bing karşı aramadan ve sonuçları birlikte weaving düşünün? Bu özellik ayrıca, yavaş, kolay *yanlışlıkla* kullanın ve biz düşünüyorsanız, nadiren gerçekten yararlı. Sorunları nedeniyle sunulan, özelliğinin hiçbir zaman Düzeltilen hata raporları üzerindeki çeşitli aldık.

#### <a name="update-all"></a>Tümünü Güncelleştir

Bir "Tümünü Güncelleştir" düğmesi yeni kullanıcı Arabiriminde henüz hiç eski Arabiriminde sağlamak için kullanılır. Biz bu özellik bizim RC sürüm için resurrect.

## <a name="new-clientserver-api"></a>Yeni istemci/sunucu API'si

Tüm yeni bizim paket Yönetimi UI'deki yeni özelliklerin yanı sıra, biz de NuGet istemci/sunucu protokolü için bazı uygulama ayrıntılarını çalışmakta. Biz yaptığınız işi "API v3" için paket geri yüklemesi ve paketlerin yüklenmesi gibi kritik senaryolar için yüksek kullanılabilirlik geçici tasarlanmış NuGet oluşturmaktır. Yeni API REST üzerinde temel alır ve iletilir ve biz seçtiğiniz [JSON-LD](http://json-ld.org) bizim kaynak biçiminde.

NuGet 3.0 Önizleme bitleri paket kaynağı açılır listede "preview.nuget.org" adlı yeni bir paket kaynağı bakın. Bu paket kaynağını seçerseniz, yeni API'mize yerine nuget.org için bağlanmak için kullanacağız. Önizleme kaynak kullanıcı arabiriminde kullanılabilir yaptık, biz sınamak için gözden geçirebilir ve yeni API geliştirmeye devam ederken. NuGet 3.0 RC'de bu yeni API v3 tabanlı paket kaynağı v2 tabanlı "nuget.org" Paket kaynağı yerini alır.

API v3 koyma yatırım rağmen bu özelliklerin tümü, yeni nuget.org de dışında varolan paket kaynaklarını birlikte çalışacağı anlamına gelir, varolan API v2 protokolü ile de çalışır yaptık.

## <a name="new-features-coming"></a>Gelen yeni özellikleri

Şimdi arasında 3.0 RTM, ayrıca kullanıcı Arabiriminde görmek ötesinde bazı temel yeni NuGet özellikler üzerinde çalışıyoruz. Belirgin yatırım alanlarının kısa bir listesi aşağıda verilmiştir:

1. Visual Studio ile ortaklık ve MSBuild ekipleri almak için [NuGet platformuna derin](http://blog.nuget.org/20141014/in-the-platform.html).
1. Yükleme zamanı paket kuralları bırakın ve bunun yerine yeni bir sunarak bu kuralları paketleme aynı anda uygulamak için çalışıyoruz "yetkili" [paket bildirimi](http://blog.nuget.org/20141023/package-manifests.html).
1. NuGet codebase istemci ve sunucu bileşenleri Visual Studio'da paket Yönetimi ötesinde farklı etki alanlarında yeniden kullanılabilir yapmak için düzenleme için çalışıyoruz.
1. "Özel bağımlılıkları burada bir paket belirtebilirsiniz, BT'nin" kavramı araştırmakta uygulama ayrıntılarını yalnızca diğer paketleri üzerinde bağımlılıklara sahiptir ve bu bağımlılıkların en üst düzey bağımlılıklar olarak ortaya çıkması döndürmemelidir.

## <a name="stay-tuned"></a>Bizi izlemeye devam edin

Lütfen takip [bizim blog](http://blog.nuget.org) daha fazla ilerleme ve duyuruları NuGet 3.0 için!