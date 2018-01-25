---
title: "NuGet paketi yazarları Project.JSON etkisini | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Nasıl NuGet 3.x etkiler project.json uygulama paketini desteklenmeyen özellikler, içerik ve paket biçimi gibi yazarlar ayrıntılar."
keywords: "NuGet ve project.json, project.json etkisi yazma konuları, project.json özellik paketi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6104b4dac330869bc5724ffcf15cc0ac9ee26c1f
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2018
---
# <a name="impact-of-projectjson-when-creating-packages"></a>Paket oluştururken project.json etkisi

> [!Important]
> Bu içerik kullanım dışı bırakılmıştır. Projeleri ya da kullanması gereken `packages.config` veya PackageReference biçimleri.

`project.json` NuGet içinde 3 + kullanılan sistem aşağıdaki bölümlerde açıklandığı gibi çeşitli şekillerde paketi yazarları etkiler.

## <a name="changes-affecting-existing-packages-usage"></a>Var olan paketler kullanım etkileyen değişiklikleri

Geleneksel NuGet paketlerini geçişli dünyasına taşınır olmayan özellikler kümesini destekler.

### <a name="install-and-uninstall-scripts-are-ignored"></a>Yükleme ve kaldırma betikleri yok sayılır

Açıklanan geçişli geri yükleme modeli [bağımlılık çözümlemesi](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference), "paketini yükle zaman" kavramını yok. Bir pakettir mevcut ya da mevcut değil, ancak bir paket yüklendiğinde oluşan tutarlı hiçbir işlem yok.

Ayrıca, komut dosyaları yalnızca Visual Studio'da desteklenen yükleyin. Diğer IDE Visual Studio genişletilebilirlik gibi komut dosyalarını destekleyen girişimi için API gerekiyordu ve Destek yok ortak düzenleyicileri ve komut satırı araçları kullanılabilir.

### <a name="content-transforms-are-not-supported"></a>İçerik dönüştürmeleri desteklenmez.

Benzer komut dosyaları yüklemek için paketi çalıştırmak dönüşümler yükleyin ve genellikle ıdempotent değildir. Artık hiçbir yükleme saatini olduğundan XDT dönüştürme ve benzer özellikleri desteklenmez ve böyle bir paket geçişli bir senaryoda kullanılırsa, göz ardı edilir.

### <a name="content"></a>İçerik

Geleneksel NuGet paketlerini kaynak kodu gibi içerik dosyalarını ve yapılandırma dosyalarını yayımlayan. Var. genellikle iki senaryolarda kullanılır:

1. Kullanıcı daha sonra düzenleyebilmeniz başlangıç dosyalarını projeye bırakıldı. Varsayılan yapılandırma dosyalarını ortak örnektir.

1. Projede yüklü derlemelerine arkadaşlarımız olarak kullanılan içerik dosyaları. Örnek bir derlemesi tarafından kullanılan bir logo görüntüsü olacaktır.

Komut dosyaları ve dönüşümler benzer nedenlerle içerik şu anda devre dışıdır, ancak içerik desteğini tasarlama sürecinde olan desteği.

İçerik dosyaları hala paketleri aktarılabilen ve şu anda göz ardı edilir, ancak son kullanıcı hala bunları sağ nokta kopyalayabilirsiniz.

İçerik dosyalarını geri getiren teklifleri birine bakın ve ilerleme durumunu, burada izleyin: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627).

## <a name="impact-for-package-authors"></a>Paketi yazarları için etkisi

Yukarıdaki özellikleri kullanarak paketleri farklı mekanizmasını kullanmanız gerekir. Bunun en yaygın olarak yararlı mekanizması MSBuild hedefleri/tam olarak desteklenen için devam eden özellik olacaktır. Derleme sistemi diğer kuralları paketindeki alması seçebilirsiniz. MSBuild hedefleri Roslyn çözümleyiciler yanı sıra nasıl desteklendiğini budur. Hedefleri ve çözümleyiciler için destekleyen paketleri oluşturmak mümkün müdür `packages.config` ve `project.json` senaryoları.

Başlangıç genellikle kolaylaştırmak için proje değiştirme girişimi paketleri çok sınırlı sayıda senaryoları iş ve bunun yerine bir benioku veya kılavuz paketin nasıl kullanılacağı hakkında sağlaması gerekir.

Çoğu mevcut paketleri aşağıda açıklanan paket biçimi kullanmanız gerekmez.

Yerel içerik biçimi birinci sınıf bir senaryo sağlar. Hedef platformu temel alarak Yönetilen derlemeler yanında ikili uygulamaları dağıtmayı bağlı olarak donanım uygulamaları yakın derlemeleri yönetilen anlamına gelir. Örneğin System.IO.Compression paket bu teknoloji kullanılarak. [https://www.nuget.org/packages/System.IO.Compression](https://www.nuget.org/packages/System.IO.Compression)

Yukarıdaki işlevselliği kesinlikle gerekli değilse, burada açıklanan biçimde yalnızca NuGet 3.x+ tarafından desteklenen olarak Özet olarak var olan paketi biçimiyle kalmanız öneririz.

Her ikisi için çalışmaya paketleri oluşturmak mümkün `packages.config` ve `project.json` shimming, ancak genellikle yalnızca yukarıda belirtilen kullanım dışı özellikler olmadan geleneksel şekilde paketleri yapısı daha basit olduğu aracılığıyla senaryoları.

## <a name="3x-package-format"></a>3.x paket biçimi

3.x paket biçimi NuGet ötesinde çeşitli ek özellikler sağlar 2.x:

1. Derleme ve bir dizi farklı platformlar/cihaz üzerinde çalışma zamanı için kullanılan uygulama derlemeler için kullanılan bir referans derlemesini tanımlama. Platform özel yararlanmak verir tüketicileriniz için ortak bir yüzey alanını sağlarken API'leri. Özellikle bu şekilde, daha kolay Ara taşınabilir kitaplıklara yazmayı kolaylaştırır.

1. İşletim sistemleri veya CPU mimarisi platformlarda Örneğin Özet paketleri sağlar.

1. Platform belirli uygulamaları Yardımcısı paketlere ayrımı sağlar.

1. Yerel bağımlılıkları birinci sınıf vatandaşı destekler.