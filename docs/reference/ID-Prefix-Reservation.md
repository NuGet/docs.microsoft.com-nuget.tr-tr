---
title: Kimlik öneki ayırma başvurusu
description: Paket kimliği öneki ayırma özelliği açıklama ve yazar Kılavuzu.
author: diverdan92
ms.author: diverdan92
manager: unnir
ms.date: 10/09/2017
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 10d017d67cf2bd49812c5d54f9fca063f32cc052
ms.sourcegitcommit: 6cffa6ef59b922df2d87aa9c24034d00542983cd
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/10/2018
ms.locfileid: "37948401"
---
# <a name="package-id-prefix-reservation"></a>Paket kimliği ön eki ayırma

Paket sahipleri, ayırabilir ve kimliği ön ekleri ayırarak kimliklerini koruyun. Ek bilgilerle kullanma, paketler, bunlar tüketen paket olmayan tanımlayıcı özelliklerini aldatıcı paketi tüketicileri sağlanır. 

[nuget.org](https://www.nuget.org/) ve Visual Studio 2017 sürüm 15.4 veya üzeri ayırtılan ID paket eşleştiği sürece, ayrılmış bir paket kimliği öneki ile sahipleri tarafından gönderilen paketleri adlandırma deseni önek için görsel Gösterge Göster. Hangi kimlik ön eki ayırma kapsar ve sahibi için bir kimlik öneki nasıl uygulanabilir başvuru açıklanmaktadır.

## <a name="id-prefix-reservation-details"></a>Kimlik ön eki ayırma ayrıntıları

Bir paket kimliği öneki ayrılmıştır, üzerinde olacaklar [nuget.org](https://www.nuget.org/) galeri de Visual Studio olduğu gibi. Ek olarak, var. birden fazla sahibe önek alt kümeleri için temsilci seçme ön eki 'public' olarak ayarlamak gibi kimliği öneki ayırmaları tarafından desteklenen Gelişmiş senaryolar.

### <a name="id-prefix-reservation-on-nugetorg"></a>Nuget.org kimlik ön eki ayırma

Ne zaman bir öneki ayrılmıştır üzerinde [nuget.org](https://www.nuget.org/), aşağıdakiler olur:

1. Ön eki ayırma sahibi veya sahipleri kümesi ile ilişkili [nuget.org](https://www.nuget.org/).

1. Her bir paket gönderildi için [nuget.org](https://www.nuget.org/) kimliği öneki ayrılmış sahip kaynaklı sürece, ayrılmış kimliği öneki ile eşleşen bir kimliği ile paket reddedilir.

1. Ayrılmış kimliği öneki eşleşir ve kimliği öneki ayrılmış sahip kaynaklı herhangi bir paket, Visual Studio 2017 sürüm 15.4 veya sonraki bir sürümü ve üzerinde bir gösterge sahip olacaktır [nuget.org](https://www.nuget.org/) paket altında olduğunu gösteren ayrılmış bir kimliği öneki. Bu, hem yeni paket gönderimleri, aynı zamanda mevcut paketleri sahip altında için geçerlidir. **Not:** paket kaynağı olarak yalnızca tek bir akış seçili değilse, Visual Studio'da göstergesi görünür.

1. Ayrılmış kimlik öneki, eşleşen tüm önceden var olan ancak paketlerin *değil* ayrılmış sahibini ait ön eki değişmeden kalır (bunlar listede bulunmayan olmayacak, ancak ayrıca görsel gösterge olmaz). Ayrıca, bu paketlerin sahipleri yine de paketinin yeni sürümlerini göndermek oluşturabileceksiniz.

Bu değişiklikler, aşağıdaki koşullara göre ve birkaç ek kısıtlamaları dayatır:

- Bir paketi tek sahibini (için birden çok sahipleri paketlerle) görünmesini görsel gösterge ayrılmış öneki olmalıdır.

- Ardından birden fazla sahibi olduğu bir veya daha fazla sahip ayrılmış önek içeriyor ve bir veya daha fazla sahip ayrılmış önek yok bir paket yoksa, yalnızca sahip ayrılmış önek ile diğer sahip ayrılmış bir önek ile kaldırabilirsiniz. Ayrılmış öneki almaz sahiplerine ön eki ayrılmış sahipler kaldırılamaz. Bunlar yine de ayrılmış önek olmayan diğer sahipleri kaldırabilirsiniz.

- Bir paket görsel gösterge olduğunda, olması gerektiği *her zaman* görsel gösterge sahip (en az bir sahibi ayrılmış önekiyle güvence altına almak her zaman kalır sahibi)

### <a name="advanced-prefix-reservation-scenarios"></a>Gelişmiş ön eki ayırma senaryoları

Subprefix temsilci ve genel olarak işaretleme ön ekleri dahil olmak üzere aşağıda açıklanan daha gelişmiş birkaç ön eki ayırma senaryo vardır. Yapılabilecek daha gelişmiş önek ayırmaları aşağıda verilmiştir. 

- Ön eki ayırma sırasında sahibi önek alt kümeleri için temsilci seçme (veya ön ek) diğer sahiplerine isteyebilir. Örneğin, '[Microsoft](https://www.nuget.org/profiles/microsoft)' sahibi ' Microsoft\*', ancak '[aspnet](https://www.nuget.org/profiles/aspnet)' ayırmak istiyor ' Microsoft.AspNet.\*','[Microsoft](https://www.nuget.org/profiles/microsoft)' can temsilci olarak seçin ' Microsoft.AspNet. \*' için [aspnet](https://www.nuget.org/profiles/aspnet) hesabı.

- Ön eki ayırma sırasında sahibi bir önek genel hale getirmek üzere seçebilirsiniz. Bu yine de bunları ayrılmış bir önekten paket kaynağı, ancak olacak gösteren bir görsel gösterge verecektir **değil** herhangi bir sahip için gelecekteki paket gönderimler önekini engelleyin. Bu birçok katılımcının açık kaynak projeleri için kullanışlıdır - top veya çekirdek Katkıda Bulunanlar, ayrılmış bir önek olabilir ancak yine de tüm katkıda bulunanlar için açık olabilir. 

### <a name="prefix-reservation-visual-indicator"></a>Ön eki ayırma görsel gösterge

Bir paket ayrılmış bir önekten geldiğinde, gördüğünüz visual göstergelerini aşağıda [nuget.org](https://www.nuget.org/) Galerisi ve Visual Studio 2017 sürüm 15.4 veya sonraki bir sürümü:

**nuget.org galeri**
![nuget.org Galerisi](media/nuget-gallery-reserved-prefix.png)

**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)

## <a name="id-prefix-reservation-application-process"></a>Kimlik ön eki ayırma uygulama işlemi

1. Kabul gözden [ön eki kimliği ayırma ölçütlerine](#id-prefix-reservation-criteria).

2. Herhangi bir ek olarak ayırmak istediğiniz ad alanları belirlemek [Gelişmiş ön eki ayırma senaryoları](#advanced-prefix-reservation-scenarios) gerektirebilir.

3. Bir e-posta Gönder [ account@nuget.org ](mailto:account@nuget.org) üzerinde görünen adı sahibiyle [nuget.org](https://www.nuget.org/), istediğiniz herhangi bir ayrılmış önekler yanı sıra. Ön ek alt kümeleri birden fazla sahibe temsilci, tüm sahibi görünen adları bahsedin ve alt kümelerini önek emin olun.

Uygulamayı gönderdikten sonra size onay veya ret (reddetme nedeni ölçütleri ile) bildirilir. Sahibi kimlik doğrulamak için ek tanımlayıcı soru sormak gerekebilir.

### <a name="id-prefix-reservation-criteria"></a>Kimlik ön eki ayırma ölçütü

Kimlik ön eki ayırma için herhangi bir uygulama incelerken [nuget.org](https://www.nuget.org/) takım uygulamaya karşı değerlendirin aşağıdaki ölçütleri. Tüm ölçütleri ayrılacak için bir önek karşılanması gerekir, ancak önemli kanıt (verilen bir açıklamayı içeren) karşılanıyor ölçüt ise, uygulama engellenebilir:

1. Paket kimliği öneki, paket sahibinden düzgün bir şekilde ve net bir şekilde gösteriyor mu?

1. Çok sayıda zaten gönderilen paketleri paket kimliği öneki altında sahibi tarafından misiniz?

1. Paket kimliği öneki olan bir şey ortak herhangi bir tek sahibi veya kuruluşa ait değil mi?

1. İstediğiniz *değil* paket kimliği öneki ayırma belirsizlik ve topluluk için Kafa karışıklığına neden?

1. Paket kimliği öneki NET ve tutarlı (özellikle paket yazarı) eşleşen paketleri tanımlayıcı özelliklerini misiniz?

## <a name="third-party-feed-provider-scenarios"></a>Üçüncü taraf sağlayıcı senaryoları akışı

Bir üçüncü taraf sağlayıcı akış ön eki ayırmaları sağlamak için kendi hizmet uygulama ilgileniyorsa değiştirerek sağlayıcıları NuGet V3 arama hizmetinizdeki akış için bunu yapabilirsiniz. Akış arama hizmetinin ek eklemektir *doğrulandı* özelliğiyle V3 Özet akışları için örnekler. NuGet istemci akışı V2'de eklenen özellik desteklemez.

Daha fazla bilgi için [API'nin arama hizmeti hakkında belgeler](../api/search-query-service-resource.md).

## <a name="package-id-prefix-reservation-dispute-policy"></a>Paket kimliği öneki ayırma itiraz İlkesi
Sahibi düşünüyorsanız [NuGet.org](https://www.nuget.org) yukarıda listelenen ölçütlerine göre giden veya tüm ticari markalarınızın ya da telif hakları, e-posta Lütfen ihlal eden bir paket kimliği ön eki ayırma atandığı [ support@nuget.org ](mailto:support@nuget.org)söz konusu kimlik öneki, kimlik öneki ve atanan ön eki ayırma disputing nedenini sahibi.

