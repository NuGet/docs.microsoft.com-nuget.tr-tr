---
title: NuGet paket yazarlarının Project.JSON etkisi
description: Nasıl NuGet 3.x etkiler project.json uygulama paketini yazar, desteklenmeyen özellikler, içerik ve paket biçimi gibi ayrıntılar.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 8c85c1a89469c491c6be1f81961197450744349c
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545579"
---
# <a name="impact-of-projectjson-when-creating-packages"></a>Paket oluştururken project.json etkisi

> [!Important]
> Bu içerik kullanım dışı bırakılmıştır. Projeleri ya da kullanması gereken `packages.config` veya PackageReference biçimleri.

`project.json` Nuget'te 3 + kullanılan sistem aşağıdaki bölümlerde açıklandığı gibi çeşitli şekillerde paket yazarlarının etkiler.

## <a name="changes-affecting-existing-packages-usage"></a>Var olan paketler kullanım etkileyen değişiklikler

Geleneksel NuGet paketlerini geçişli dünya taşınmaz özellikleriyle destekler.

### <a name="install-and-uninstall-scripts-are-ignored"></a>Yükleme ve kaldırma betiklerini yoksayıldı

Açıklanan geçişli geri yükleme modeli [bağımlılık çözümlemesi](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference), "paket yükleme saati" kavramını sahip değil. Mevcut değil ya da mevcut bir pakettir, ancak bir paket yüklendikten sonra gerçekleşen tutarlı işlem yok.

Ayrıca, komut dosyaları yalnızca Visual Studio ile desteklenen yükleyin. Diğer Ide'leri API gibi komut dosyalarını destekleyen denemek için Visual Studio genişletilebilirlik gerekiyordu ve ortak düzenleyiciler ve komut satırı araçları desteği yoktu.

### <a name="content-transforms-are-not-supported"></a>İçerik dönüştürmeleri desteklenmez.

Benzer betikleri yüklemek için paketi üzerinde çalıştırılan dönüşümler yükleyin ve genellikle etkili değildir. Artık hiçbir yükleme zamanı olduğundan, XDT dönüştürün ve benzer özellikleri desteklenmez ve bu tür bir paket geçişli bir senaryoda kullanılıyorsa, göz ardı edilir.

### <a name="content"></a>İçerik

Kaynak kodu gibi içerik dosyaları ve yapılandırma dosyaları geleneksel NuGet paketlerini yayımlayan. Var. tipik olarak iki senaryolarda kullanılır:

1. Kullanıcı daha sonraki bir zamanda düzenleyebilmeniz ilk dosyalar projeye bırakıldı. Varsayılan yapılandırma dosyalarını ortak örnektir.

1. İçerik dosyalarının projede yüklü derlemelere arkadaşlarımız olarak kullanılır. Örnek, bir derleme tarafından kullanılan bir logo resmi olacaktır.

İçerik betikleri ve dönüştürmeler için benzer nedeniyle şu anda devre dışıdır, ancak içerik desteğini tasarlama aşamasında olan desteği.

İçerik dosyaları yine de paketleri aktarılabilen ve şu anda göz ardı edilir, ancak son kullanıcı yine de bunları doğru nokta kopyalayabilirsiniz.

İçerik dosyalarını geri getirmek için teklifleri birine bakın ve ilerleme durumunu, burada izleyin: [ https://github.com/NuGet/Home/issues/627 ](https://github.com/NuGet/Home/issues/627).

## <a name="impact-for-package-authors"></a>Paket yazarlarının için etkisi

Yukarıdaki özellikleri kullanarak paketleri farklı mekanizmasının kullanılması gerekir. Bunun en yaygın olarak yararlı mekanizması, MSBuild hedefleri/tam olarak desteklenen için devam eden özellikler olacaktır. Derleme sistemi paketi diğer kuralları yerden devam edebiliyorduk seçebilirsiniz. MSBuild hedefleri Roslyn Çözümleyicileri yanı sıra nasıl desteklenen budur. Hedefleri ve çözümleyiciler için destekleyen paketleri oluşturmak mümkündür `packages.config` ve `project.json` senaryoları.

Başlangıç genellikle kolaylaştırmak için proje değiştirmeyi deneyen paketleri senaryoları çok sınırlı kümesi içinde çalışır ve paketin nasıl kullanılacağı hakkında bir Benioku ya da yönergeler yerine sağlamalıdır.

Birçok var olan paketi aşağıda açıklanan paket biçimi kullanmanız gerekmez.

Biçim, birinci sınıf bir senaryo yerel içerik sağlar. Bu, yönetilen bütünleştirilmiş kodların donanım uygulamaları, hedef platforma göre Yönetilen derlemeler yanı sıra ikili uygulamaları dağıtmayı yakın bağımlı olduğunu gösterir. Örneğin System.IO.Compression paketi bu teknoloji kullanılmaktadır. [https://www.nuget.org/packages/System.IO.Compression](https://www.nuget.org/packages/System.IO.Compression)

Yukarıdaki işlevselliğini kesinlikle gerekli değilse, burada açıklanan biçimde yalnızca NuGet 3.x+ tarafından desteklenmediğinden özetinde kalmanız mevcut paket biçimi öneririz.

Hem çalışma için paketler oluşturmak mümkün `packages.config` ve `project.json` senaryolar aracılığıyla için dolgu oluşturuluyor, ancak bu genellikle yalnızca yukarıdaki kullanım dışı bırakılan özellikler olmadan geleneksel paketleri yapı daha kolaydır.

## <a name="3x-package-format"></a>3.x paket biçimi

Birkaç ek özelliklerin ötesinde NuGet 3.x paket biçimi sağlar 2.x:

1. Derleme ve farklı platformları/cihaz üzerinde çalışma zamanı için kullanılan bir uygulama derleme kümesi için kullanılan bir başvuru bütünleştirilmiş kodu tanımlama. Belirli platformunun avantajlarından yararlanmanıza olanak tanıyan tüketicileriniz için ortak bir yüzey alanı sağlarken API'leri. Özellikle bu şekilde, daha kolay Ara taşınabilir kitaplıklar yazmayı kolaylaştırır.

1. İşletim sistemleri veya CPU mimarisi platformlarda örn Özet paketleri sağlar.

1. Belirli platform uygulamalarını Yardımcısı paketlerine ayrımı sağlar.

1. Yerel bağımlılıkları öncelikli bir yere destekler.
