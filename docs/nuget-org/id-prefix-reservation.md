---
title: Kimlik Önek Rezervasyonu
description: Paket Kimliği Önek Rezervasyon özelliği açıklaması ve yazar kılavuzu.
author: karann-msft
ms.author: karann
ms.date: 09/07/2019
ms.topic: reference
ms.reviewer: karann
ms.openlocfilehash: da464cc44d8c874e13c0cdfab871f31e643b577f
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "73610506"
---
# <a name="package-id-prefix-reservation"></a>Paketleme kimlik ön eki ayırma

Paket sahipleri kimlik önekleri ayırarak kimliklerini rezerve edebilir ve koruyabilirler. Paket tüketicilerine, tükettikleri paketler tanımlayıcı özelliklerinde aldatıcı olmadığında ek bilgiler verilir. 

[nuget.org](https://www.nuget.org/) ve Visual Studio 2017 sürüm 15.4 veya daha sonraki sürüm, paket ayrılmış kimlik öneki adlandırma desenine uygun olduğu sürece, sahipleri tarafından ayrılmış paket kimliği önekiyle gönderilen paketler için görsel bir gösterge gösterir. Aşağıdaki başvuru, kimlik öneki rezervasyonunun ne gerektirdiğini ve sahibinin kimlik önekiiçin nasıl başvurabileceğini açıklar.

## <a name="id-prefix-reservation-details"></a>Kimlik öneki rezervasyon detayları

Paket kimliği öneki rezerve edildiğinde, [nuget.org](https://www.nuget.org/) galerisinde ve Visual Studio'da birkaç şey olur. Ayrıca, önek alt kümelerini birden çok sahipe atamak, önek 'ortak' olarak ayarlamak gibi KIMLIK öneki rezervasyonları tarafından desteklenen gelişmiş senaryolar da vardır.

### <a name="id-prefix-reservation-on-nugetorg"></a>nuget.org'da kimlik öneki rezervasyonu

bir önek [nuget.org](https://www.nuget.org/)ayrılmışsa, aşağıdakiler gerçekleşir:

1. Önek ayırma, [nuget.org'daki](https://www.nuget.org/)bir sahibi veya sahip ler kümesiyle ilişkilidir.

1. Ayrılmış kimlik önekiyle eşleşen bir kimlikle [nuget.org](https://www.nuget.org/) bir paket gönderildiğinde, paket kimlik önekini rezerve eden sahibinden (ler) kaynaklanmadığı sürece reddedilir.

1. Ayrılmış kimlik önekiyle eşleşen ve kimlik önekini rezerve eden sahip(ler)den kaynaklanan herhangi bir paketin Visual Studio 2017 sürümü 15.4 veya sonraki sürümde ve paketin ayrılmış bir kimlik öneki altında olduğunu belirten [nuget.org](https://www.nuget.org/) görsel bir göstergeye sahip olacaktır. Bu, hem yeni paket gönderimleri hem de sahibi (ler) altındaki mevcut paketler için geçerlidir. **Not:** Visual Studio'daki gösterge yalnızca paket kaynağı olarak tek bir akış seçilirse görüntülenir.

1. Ayrılmış kimlik önekiyle eşleşen ancak ayrılmış önek sahibine ait *olmayan* önceden varolan tüm paketler değişmeden kalır (listedışı kalmazlar, ancak görsel göstergeye de sahip olmazlar). Buna ek olarak, bu paketlerin sahipleri pakete yeni sürümler göndermeye devam edebilecektir.

Bu değişiklikler aşağıdaki koşullara dayanır ve birkaç ek kısıtlama uygular:

- Bir paketin yalnızca bir sahibinin, görsel göstergenin görünmesi için ayrılmış öneki (birden çok sahibi olan paketler için) olması gerekir.

- Bir veya daha fazla sahibin ayrılmış önek olduğu ve bir veya daha fazla sahibin ayrılmış önek olmadığı bir paketin birden fazla sahibi varsa, yalnızca ayrılmış öneki olan sahip(ler) ayrılmış bir önek ile diğer sahibi(ler) kaldırabilir. Önek rezerve edilmedi, önek rezerve edildi. Yine de önek ayrılmış olmayan diğer sahipleri kaldırabilirsiniz.

- Bir paket görsel göstergeye sahip olduğunda, *her zaman* görsel göstergeye sahip olmalıdır (ayrılmış önekiyle en az bir sahibin her zaman sahip olarak kalacağını garanti eder)

### <a name="advanced-prefix-reservation-scenarios"></a>Gelişmiş önek rezervasyon senaryoları

Aşağıda açıklanan sub prefix delegasyonu ve önekleri genel olarak işaretleme dahil olmak üzere birkaç daha gelişmiş önek rezervasyon senaryoları vardır. Aşağıda yapılabilir daha gelişmiş önek rezervasyonları vardır. 

- Önek ayırma sırasında, sahibi diğer sahiplerine önek alt kümeleri (veya önek) delegasyonu isteyebilir. Örneğin, '[Microsoft](https://www.nuget.org/profiles/microsoft)' microsoft ' sahibi 'Microsoft. \*', ama '[aspnet](https://www.nuget.org/profiles/aspnet)' 'Microsoft.AspNet rezerv istiyor. \*', '[Microsoft](https://www.nuget.org/profiles/microsoft)' 'microsoft.AspNet'i temsilci olarak seçebilir. \*' [aspnet](https://www.nuget.org/profiles/aspnet) hesabına.

- Önek ayırma sırasında, sahibi bir önek genel yapmayı seçebilirsiniz. Bu, paketin ayrılmış bir önek olduğunu gösteren görsel göstergeyi vermeye devam eder, ancak herhangi bir sahip için önek üzerindeki gelecekteki paket gönderimlerini **engellemez.** Bu, birçok katılımcısı olan açık kaynak projeleri için yararlıdır - en iyi veya temel katkıda bulunanlar önek rezerve edilebilir, ancak yine de tüm katkıda bulunanlara açık olabilir. 

### <a name="prefix-reservation-visual-indicator"></a>Önek rezervasyon görsel göstergesi

Bir paket ayrılmış bir önek geldiğinde, [nuget.org](https://www.nuget.org/) galerisinde ve Visual Studio 2017 sürüm 15.4 veya sonraki sürümde aşağıdaki görsel göstergeleri görürsünüz:

**nuget.org Galeri**
![nuget.org Galerisi](media/nuget-gallery-reserved-prefix.png)

**Görsel Stüdyo**
![Görsel Stüdyo](media/visual-studio-reserved-prefix.png)

## <a name="id-prefix-reservation-application-process"></a>Kimlik öneki rezervasyon başvuru süreci

1. Önek kimliği rezervasyonu için kabul [ölçütlerini](#id-prefix-reservation-criteria)gözden geçirin.

2. Gerektirebilecek [gelişmiş önek rezervasyon senaryolarına](#advanced-prefix-reservation-scenarios) ek olarak, ayırmak istediğiniz önekleri belirleyin.

3. nuget.org'da [account@nuget.org](mailto:account@nuget.org) sahibinin görüntü adı [nuget.org](https://www.nuget.org/)ile birlikte bir posta ve istediğiniz ayrılmış önekleri gönderin. Önek alt kümelerini birden çok sahipe atadıysanız, tüm sahip görüntüleme adlarından ve öneki alt kümelerinden bahsettiğinden emin olun.

Başvuru sunulduktan sonra, kabul veya ret (reddedilmeye neden olan kriterler ile) bildirilir. Sahip kimliğini doğrulamak için ek tanımlayıcı sorular sormamız gerekebilir.

### <a name="id-prefix-reservation-criteria"></a>Kimlik öneki rezervasyon kriterleri

Kimlik öneki rezervasyonu için herhangi bir başvuruyu incelerken, [nuget.org](https://www.nuget.org/) ekibi başvuruyu aşağıdaki kriterlere göre değerlendirecektir. Bir önekinin rezerve edilebilmesi için tüm kriterlerin karşılanması gerekmez, ancak karşılanan kriterlere dair önemli bir kanıt yoksa (bir açıklama ile) başvuru reddedilebilir:

1. Paket kimliği öneki düzgün ve net bir şekilde paket sahibini tanımlıyor mu?

1. Paket sahibi [NuGet.org hesabı için 2FA'yı etkinleştirmiş](individual-accounts.md#enable-two-factor-authentication-2fa)mi?

1. Paket kimliği öneki altında sahibi tarafından zaten gönderilmiş olan paketlerin önemli bir kısmı var mı?

1. Paket kimliği öneki, herhangi bir bireysel sahibine veya kuruluşa ait olmaması gereken yaygın bir şey midir?

1. Paket kimlik önekinin rezerve edilmemesi topluluk için belirsizlik ve karışıklığa neden *olmaz* mı?

1. Paket kimliği önekiyle eşleşen paketlerin tanımlayıcı özellikleri açık ve tutarlı mıdır (özellikle paket yazarı)?

1. Paketlerin bir lisansı var mı [(lisans](../reference/nuspec.md#license) meta veri öğesini ve amortismana alınmayan NOT licenseUrl'sini kullanarak)?

1. Paketlerde bir simge varsa (iconUrl meta veri öğesini kullanarak), [simge](../reference/nuspec.md#icon) meta veri öğesini de kullanıyorlar (simgeUrl'yi kaldırmak için bir gereklilik değildir)?

## <a name="third-party-feed-provider-scenarios"></a>Üçüncü taraf akış sağlayıcısı senaryoları

Bir üçüncü taraf özet akışı sağlayıcısı önek rezervasyonları sağlamak için kendi hizmetini uygulamakla ilgileniyorsa, bunu NuGet V3 besleme sağlayıcılarındaki arama hizmetini değiştirerek yapabilir. Özet akışı arama hizmetindeki değişiklik `verified` özelliği eklemektir. NuGet istemcisi V2 akışındaki eklenen özelliği desteklemez.

Daha fazla bilgi için [API'nin arama hizmeti yle ilgili belgelere](../api/search-query-service-resource.md)bakın.

## <a name="package-id-prefix-reservation-dispute-policy"></a>Paket Kimlik Önek Rezervasyon İtiraz Politikası
[NuGet.org'daki](https://www.nuget.org) bir sahibine yukarıda listelenen ölçütlere aykırı bir paket kimlik öneki rezervasyonu atandığını veya ticari [support@nuget.org](mailto:support@nuget.org) marka veya telif haklarını ihlal ettiğini düşünüyorsanız, lütfen söz konusu kimlik öneki, kimlik önekinin sahibi ve atanan önek rezervasyonun tartışımının nedenini içeren bir e-posta gönderin.

