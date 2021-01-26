---
title: NuGet 3,0 Preview sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 3,0 Preview için sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ecaed21c5e689a488e033404f8042cd1f17eed0d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780334"
---
# <a name="nuget-30-preview-release-notes"></a>NuGet 3,0 Preview sürüm notları

[NuGet 2,9 RC sürüm notları](../release-notes/nuget-2.9-rc.md)  |  [NuGet 3,0 beta sürüm notları](../release-notes/nuget-3.0-beta.md)

NuGet 3,0 Önizlemesi, Visual Studio 2015 Preview sürümünün bir parçası olarak 12 Kasım 2014 ' de yayımlanmıştır. NuGet 3,0 Önizlemesi yayımlandı. Bu, bizim için büyük bir sürümdür (bir önizleme) ve değişikliklerimiz hakkında geri bildirimde bulunmak için heyecanlıyız.

## <a name="visual-studio-2012"></a>Visual Studio 2012 +

Bu NuGet 3,0 Önizlemesi, Visual Studio 2015 önizlemesine dahildir. Visual Studio 2012 ve çok yakında Visual Studio 2013 Önizleme altına almak için çalışıyoruz. Daha önce [Visual Studio 2010 güncelleştirmelerini sona erdirme](http://blog.nuget.org/20141002/visual-studio-2010.html)amacımızı paylaştık ve bu zor kararı veriyoruz.

## <a name="brand-new-ui"></a>Yepyeni yeni kullanıcı arabirimi

NuGet 3,0 Preview hakkında fark ettiğiniz ilk şey, Yeni Kullanıcı arabirimimiz. Artık kalıcı bir iletişim kutusu değildir; Artık tam bir Visual Studio belge penceresidir. Bu, birden çok proje (ve/veya çözüm) için Kullanıcı arabirimini tek seferde açmanıza, pencereyi başka bir monitöre sabitleyebilmeniz, ancak istediğiniz gibi, vb.

![Yeni NuGet Kullanıcı arabirimi](./media/NuGet-3.0-Preview/new-ui.png)

Kalıcı iletişim kutusunu terk ettiğinden kullanılabilirlik farklılıklarını aşarak Yeni Kullanıcı arabiriminde çok sayıda yeni özellik de vardır.

### <a name="version-selection"></a>Sürüm seçimi

Belki de en çok istenen kullanıcı arabirimi özelliği, paket yükleme ve güncelleştirme için sürüm seçimine izin vermektedir; Bu özellik artık kullanılabilir.

![Paket sürümü seçimi](./media/NuGet-3.0-Preview/version-selection.png)

Bir paketi yükleme veya güncelleştirme sırasında, sürüm açılan menüsü, bazı önemli sürümlerde, kolay seçim için listenin en üstüne yükseltilme olanağı sunan paketin kullanabildiği tüm sürümleri görmenizi sağlar. Artık en son olmayan belirli sürümleri almak için PowerShell konsolunu kullanmanız gerekmez.

### <a name="combined-installedonlineupdates-workflows"></a>Birleşik yüklü/çevrimiçi/güncelleştirmeler Iş akışları

Önceki Kullanıcı arabirimimiz yüklü, çevrimiçi ve güncelleştirmeler için 3 sekmeye sahipti. Listelenen paketler bu iş akışlarına özeldir ve kullanılabilir eylemler iş akışlarına da özgüdür. Bu, mantıklı olsa da, çoğu zaman bu ayrım tarafından bir kaç tane daha alındığını duyduk.

Artık paketin seçili olmasından bağımsız olarak bir paketi yükleyebileceğiniz, güncelleştiren veya kaldırabileceğiniz birleştirilmiş bir deneyimimiz vardır. Belirli iş akışlarıyla yardım almak için artık paketleri görünür halde filtrelemenizi sağlayan bir filtre açılır listesi sunuyoruz, ancak paket için kullanılabilen eylemler tutarlıdır.

![Bir paketi kaldırma](./media/NuGet-3.0-Preview/uninstall-package.png)

"Yüklü" filtresini kullanarak, yüklü paketlerinizi kolayca görebilir ve güncelleştirmelerin kullanılabilir olmasını sağlayabilir ve ardından sürüm seçimini değiştirerek paketi kaldırabilir ya da güncelleştirebilirsiniz.

![Bir paketi güncelleştirme](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a>Sürüm birleştirme

Çözümünüz içinde birden çok projeye aynı paketin yüklenmesi yaygındır. Bazen her bir projede yüklü olan sürümler birbirinden ayrılabilir ve kullanımda olan sürümleri birleştirmek gerekir. NuGet 3,0 Önizlemesi yalnızca bu senaryo için yeni bir özellik sunar.

Çözüm düzeyi paket yönetimi penceresine, çözüme sağ tıklayıp çözüm için NuGet Paketlerini Yönet ' i seçerek erişilebilir. Buradan, birden çok projeye yüklenmiş olan ancak farklı sürümlerde kullanılan bir paket seçerseniz, yeni bir "Birleştir" eylemi kullanılabilir hale gelir. Aşağıdaki ekran görüntüsünde, `Newtonsoft.Json` `SamplesClassLibrary` ile sürümüne yüklenmiş `6.0.4` ve `SamplesConsoleApp` sürümüne yüklenmiş `5.0.4` .

![Sürümleri Birleştir](./media/NuGet-3.0-Preview/consolidate.png)

Tek bir sürüm üzerinde birleştirme için iş akışı aşağıda verilmiştir.

1. `Newtonsoft.Json`Listeden paketi seçin
1. `Consolidate`Açılan menüden Seç `Action`
1. `Version`Üzerine birleştirilecek sürümü seçmek için açılan menüyü kullanın
1. Bu sürüme birleştirilecektir projeler için kutulara göz atın (seçilen sürümde zaten seçili olan projelerin gri olacağını unutmayın)
1. `Consolidate`Birleştirme işlemini gerçekleştirmek için düğmeye tıklayın

### <a name="operation-previews"></a>İşlem önizlemeleri

Çalıştırdığınız işlemden bağımsız olarak, yükleme/güncelleştirme/kaldırma--yeni kullanıcı arabirimi artık projenizde yapılacak değişiklikleri önizlemek için bir yol sunar. Bu önizleme, yüklenecek tüm yeni paketleri, güncellenen paketleri ve işlem sırasında değişmeden olacak paketlerle birlikte kaldırılacak paketleri gösterir.

Aşağıdaki örnekte, Microsoft. AspNet. SignalR yükleme ' nin projede çok az değişiklikle sonuçlanabileceğini görebiliriz.

![Önizleme yükleme SignalR](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a>Yükleme seçenekleri

PowerShell konsolunu kullanarak, birkaç önemli yükleme seçeneği üzerinde denetiminiz vardı. Bu özellikleri artık Kullanıcı arabirimine de hazırlıyoruz. Artık bağımlılıkların sürümlerinin seçilme şekli için bağımlılık çözümleme davranışını kontrol edebilirsiniz.

![Bağımlılık davranışı](./media/NuGet-3.0-Preview/dependency-behavior.png)

Ayrıca, paketlerdeki içerik dosyaları projenizde zaten bulunan dosyalarla çakışıyorsa gerçekleştirilecek eylemi de belirtebilirsiniz.

![Dosya çakışması eylemi](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a>Sonsuz kaydırma

Paketler listelenirken yalnızca kaydırma ve sayfalama paradigmalarına sahibi olan Kullanıcı arabirimimiz hakkında biraz geri bildirim almak için kullanıyoruz. Kısa listenin en altına kaymanız, sonraki sayfa numarasına tıklanır ve sonra tekrar kaydırılacak. Yeni Kullanıcı arabirimi ile, yalnızca daha fazla sayfalama olmadan kaydırma yapmanız gerekeceğinden paket listesinde sonsuz kaydırma gerçekleştirdik.

![Sonsuz kaydırma](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a>Çalışır duruma getirin, hızlı bir şekilde yapın

Denemeniz için bu yeni kullanıcı arabirimini almak için heyecanlıyız. Bu önizleme kilometre taşı sırasında, "çalışır duruma getirin, hızlı bir şekilde yapın, iyi hale getirin." Bu önizlemede, bu ilk hedefin çoğunu kullanıyoruz. Bu, işe yarar. Henüz hızlı olmadığını biliyoruz, ancak henüz oldukça emin biliyoruz. Şimdi ve RC sürümü arasındaki amaçlar üzerinde çalışabileceğiz güveneceğiz. Bu sırada, Yeni Kullanıcı arabiriminin *kullanılabilirliği* hakkında görüşlerinizi duymak istiyoruz. iş akışları, işlemler ve Yeni Kullanıcı *arabirimini nasıl kullanacağınızı* öğrenin.

Eski Kullanıcı arabirimine kıyasla kaldırdığımız birkaç işlev vardır. Bunlardan biri bilerek yapılmıştı ve diğeri zamanında henüz bitmedi.

#### <a name="searching-all-package-sources"></a>"Tüm" paket kaynaklarını arama

Eski Kullanıcı arabirimi, tüm paket kaynaklarınızda bir paket araması gerçekleştirmenize izin verildi. Bu özelliği Kullanıcı arabiriminde kaldırdık ve geri getiriyoruz. Bu özellik, tüm paket kaynaklarınızda arama işlemlerini gerçekleştirmek, sonuçları birlikte Weave ve sıralama seçiminize göre sonuçları sıralamayı denemek için kullanılır.

Arama ilgisi gerçekten Weave bir arada olduğunu tespit ettik. Google ve Bing 'e yönelik bir arama gerçekleştirmeyi ve sonuçların birlikte ne kadar olduğunu tahmin etmek ister misiniz? Ayrıca, bu özellik yavaş, *yanlışlıkla* kullanımı kolaydır ve nadiren gerçekten yararlı olduğunu düşüntik. Özelliğin tanıtıldığı sorunlar nedeniyle, üzerinde hiçbir şekilde düzeltilmeyen bir dizi hata raporu aldık.

#### <a name="update-all"></a>Tümünü Güncelleştir

Eski Kullanıcı arabirimindeki, henüz yeni kullanıcı arabiriminde olmayan bir "Tümünü Güncelleştir" düğmesine sahip olmak için kullandık. Bu özelliği RC sürümümüzü yeniden örnekliyoruz.

## <a name="new-clientserver-api"></a>Yeni Istemci/sunucu API 'SI

Yeni paket yönetimi Kullanıcı arabirimimizin tüm yeni özelliklerine ek olarak, NuGet istemci/sunucu protokolü için bazı uygulama ayrıntıları üzerinde de çalışıyoruz. Yaptığımız iş, paket geri yükleme ve paketleri yükleme gibi kritik senaryolar için yüksek kullanılabilirlik çevresinde tasarlanan NuGet için "API v3" oluşturmaktır. Yeni API, REST ve hiper medyayı temel alır ve kaynak biçimimiz olarak [JSON-ld](http://json-ld.org) ' i seçtik.

NuGet 3,0 Önizleme bitleriyle, paket kaynak açılan menüsünde "preview.nuget.org" adlı yeni bir paket kaynağı görürsünüz. Bu paket kaynağını seçerseniz, nuget.org 'e bağlanmak yerine yeni API 'imizi kullanacağız. Yeni API 'yi sınamaya devam ediyoruz, gözden geçirmemiz ve iyileştirirken, önizleme kaynağını Kullanıcı arabiriminde kullanılabilir hale geçirdik. NuGet 3,0 RC 'de, bu yeni API v3 tabanlı paket kaynağı v2 tabanlı "nuget.org" paket kaynağının yerini alır.

API v3 'e yerleştirdiğimiz yatırım sayesinde, bu yeni özelliklerin hepsi var olan API v2 protokolümüzde de çalıştık ve bu da nuget.org dışındaki mevcut paket kaynaklarıyla çalışacağız.

## <a name="new-features-coming"></a>Yeni özellikler geliyor

Şimdi ve 3,0 RTM arasında, Kullanıcı arabiriminde gördüklerinizin ötesinde, bazı temel yeni NuGet özellikleri üzerinde de çalışıyoruz. Aşağıda, salya yatırım alanlarının kısa bir listesi verilmiştir:

1. Visual Studio ve MSBuild ekipleriyle işbirliği yaptığımız için, [platforma daha ayrıntılı](http://blog.nuget.org/20141014/in-the-platform.html)bir şekilde ulaşın.
1. Yükleme zamanı paket kurallarını bırakmaya çalışıyoruz ve bunun yerine, yeni bir "yetkili" [paket bildirimi](http://blog.nuget.org/20141023/package-manifests.html)sunarak bu kuralları paketleme zamanına uygular.
1. Visual Studio 'da paket yönetiminin ötesinde, istemci ve sunucu bileşenlerini farklı etki alanlarında yeniden kullanılabilir hale getirmek için NuGet kod temelini yeniden düzenleme konusunda çalışıyoruz.
1. Bir paketin yalnızca uygulama ayrıntıları için diğer paketlere yönelik bağımlılıklara sahip olduğunu gösterebilen ve bu bağımlılıkların en üst düzey bağımlılıklar olarak kullanıma sunulamadığını belirtebileceği "özel bağımlılıklar" kavramı araştırıyoruz.

## <a name="stay-tuned"></a>Ayarlanmış durumda kal

NuGet 3,0 için daha fazla ilerleme ve duyuru için lütfen [blogumuza](http://blog.nuget.org) göz önünde bulundurun!