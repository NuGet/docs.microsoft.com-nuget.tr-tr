---
title: KIMLIK ön eki ayırma
description: Paket KIMLIĞI ön eki ayırma özelliği açıklaması ve yazar Kılavuzu.
author: karann-msft
ms.author: karann
ms.date: 09/07/2019
ms.topic: reference
ms.reviewer: karann
ms.openlocfilehash: 630c2b193500ec0b9aa5a7fe4af3ea95ae52aeec
ms.sourcegitcommit: 5a741f025e816b684ffe44a81ef7d3fbd2800039
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/09/2019
ms.locfileid: "70815285"
---
# <a name="package-id-prefix-reservation"></a>Paket KIMLIĞI ön eki ayırması

Paket sahipleri, kimlik öneklerini ayırarak kimliklerini ayırabilir ve koruyabilir. Paket tüketicileri, kullandıkları paketin kendi tanımlama özelliklerinde yanıltıcı olmadığı durumlarda ek bilgilerle sağlanır. 

[NuGet.org](https://www.nuget.org/) ve Visual Studio 2017 sürüm 15,4 veya üzeri, Paket ayrılmış kimlik ön eki adlandırma düzeniyle eşleşen bir ayrılmış paket kimliği ön ekine sahip sahipler tarafından gönderilen paketler için görsel bir gösterge gösterir. Aşağıdaki başvuru, KIMLIK ön rezervasyonunun ne olduğunu ve bir kimliğin bir kimlik ön eki için nasıl uygulanacağını açıklar.

## <a name="id-prefix-reservation-details"></a>KIMLIK ön eki ayırma ayrıntıları

Bir paket KIMLIĞI öneki ayrıldıysa, [NuGet.org](https://www.nuget.org/) galerisinde ve Visual Studio 'da çeşitli şeyler gerçekleşir. Ayrıca, bir öneki ' genel ' olarak ayarlama, birden çok Sahibe önek alt kümeleri atama gibi KIMLIK ön ek ayırmaları tarafından desteklenen gelişmiş senaryolar da vardır.

### <a name="id-prefix-reservation-on-nugetorg"></a>Nuget.org üzerinde KIMLIK ön eki ayırması

[NuGet.org](https://www.nuget.org/)üzerinde bir ön ek ayrıldıysa aşağıdakiler olur:

1. Önek ayırma, [NuGet.org](https://www.nuget.org/)üzerindeki bir sahip veya sahip kümesi ile ilişkilendirilir.

1. Ayrılmış KIMLIK önekiyle eşleşen bir KIMLIK ile [NuGet.org](https://www.nuget.org/) 'ye her paket gönderildiğinde, paket, kimlik önekini ayıran sahiplerden kaynaklanmadığı takdirde reddedilir.

1. Ayrılmış KIMLIK önekiyle eşleşen ve KIMLIK ön ekini ayıran sahip 'lerden kaynaklanan herhangi bir paket, Visual Studio 2017 sürüm 15,4 veya sonraki sürümlerinde ve paketin ayrılmış bir KIMLIK ön eki altında olduğunu belirten [NuGet.org](https://www.nuget.org/) üzerinde bir görsel göstergeye sahip olur. Bu, hem yeni paket teslimleri hem de sahip (ler) de var olan paketler için geçerlidir. **Not:** Visual Studio 'daki gösterge yalnızca paket kaynağı olarak tek bir akış seçilirse görünür.

1. Ayrılmış KIMLIK önekiyle eşleşen, ancak ayrılmış önek sahibine ait *olmayan* , daha önce varolan tüm paketler değişmeden kalır (bunlar listelenmemiş olmayacaktır, ancak görsel gösterge de yoktur). Ayrıca, bu paketlerin sahipleri yine de pakete yeni sürümler gönderebilecektir.

Bu değişiklikler aşağıdaki koşullara dayanır ve birkaç ek kısıtlama uygulayabilir:

- Bir paketin yalnızca bir sahibinin görsel göstergenin görünmesi için ayrılmış öneki olması gerekir (birden çok sahibe sahip paketler için).

- Bir veya daha fazla sahibin ayrılmış öneki olduğu ve bir veya daha fazla sahibin ayrılmış öneki olmadığı bir paketin birden fazla sahibi varsa, yalnızca ayrılmış ön eke sahip olan sahipler, ayrılmış bir ön eki olan diğer sahipleri kaldırabilir. Öneki ayrılmış olmayan sahipler, ayrılmış ön eke sahip sahipleri kaldıramıyor. Ayrıca, ön eke sahip olmayan diğer sahipleri yine de kaldırabilirler.

- Bir paketin görsel göstergesi varsa, *her zaman* görsel göstergesi olmalıdır (ayrılmış ön eki olan en az bir sahip, her zaman bir sahip olarak kalacak şekilde garanti edilir)

### <a name="advanced-prefix-reservation-scenarios"></a>Gelişmiş önek ayırma senaryoları

Alt ön ek temsili ve ön ekleri ortak olarak işaretleyerek aşağıda açıklanan birkaç gelişmiş ön ek ayırma senaryosu vardır. Aşağıda, yapılabilecek gelişmiş ön ek ayırmaları verilmiştir. 

- Önek ayırma sırasında, sahip önek alt kümelerinin (veya ön ek) diğer sahiplerin temsilciliğini alabilir. Örneğin, '[Microsoft](https://www.nuget.org/profiles/microsoft)', ' Microsoft ' a sahipse. ', ancak ' ASPNET ' ' Microsoft. Aspnet ' öğesini ayırmak istiyor.[](https://www.nuget.org/profiles/aspnet) \* ', ' Microsoft ', ' Microsoft. Aspnet ' yetkisini temsil edebilir.[](https://www.nuget.org/profiles/microsoft) \* ' öğesine gidin. [](https://www.nuget.org/profiles/aspnet) \*

- Önek ayırma sırasında, sahip ön eki bir genel hale getirme seçeneğini belirleyebilir. Bu, paketin ayrılmış bir önekden kaynaklandığını gösteren bir görsel göstergesi sağlar, ancak herhangi bir sahibe ait ön ek için gelecekte yapılan paket gönderilerini **engellemez.** Bu, çok sayıda katkıda bulunan açık kaynak projeleri için yararlıdır; üst veya temel katkıda bulunanlar ön eke sahip olabilir, ancak yine de tüm katkıda bulunanlar için açık olabilir. 

### <a name="prefix-reservation-visual-indicator"></a>Ön ek ayırma görsel göstergesi

Bir paket ayrılmış bir önekden geldiğinde, [NuGet.org](https://www.nuget.org/) galerisinde ve visual Studio 2017 sürüm 15,4 veya üzeri sürümlerde aşağıdaki görsel göstergeleri görürsünüz:

**NuGet.org**
Gallery![NuGet.org Galerisi](media/nuget-gallery-reserved-prefix.png)

**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)

## <a name="id-prefix-reservation-application-process"></a>KIMLIK ön eki ayırma uygulama işlemi

1. [Önek kimliği ayırması için kabul ölçütlerini](#id-prefix-reservation-criteria)gözden geçirin.

2. İstediğiniz ön ek [ön ek ayırma senaryolarına](#advanced-prefix-reservation-scenarios) ek olarak, ayırmak istediğiniz önekleri saptayın.

3. NuGet.org üzerinde sahip görünen [account@nuget.org](mailto:account@nuget.org) adı ve istediğiniz ayrılmış ön eklerin [](https://www.nuget.org/)yanı sıra e-posta gönderin. Birden çok Sahibe önek alt kümeleri temsilci seçtiyseniz, tüm sahip görünen adları ve önek alt kümelerine bahsetdiğinizden emin olun.

Uygulama gönderildikten sonra, kabul veya reddetme (reddetme hatasına neden olan ölçütlerle birlikte) hakkında bilgilendirilirsiniz. Sahip kimliğini onaylamak için ek tanımlama soruları sormamız gerekebilir.

### <a name="id-prefix-reservation-criteria"></a>KIMLIK ön eki ayırma ölçütleri

KIMLIK ön eki ayırma için herhangi bir uygulamayı gözden geçirirken, [NuGet.org](https://www.nuget.org/) ekibi uygulamayı aşağıdaki ölçütlere göre değerlendirir. Bir önekin ayrılması için tüm ölçütlerin sağlanması gerekmez, ancak karşılanmakta olan ölçütlere ilişkin önemli bir kanıt yoksa uygulama reddedilebilir (bir açıklama verilir):

1. Paket KIMLIĞI ön eki doğru bir şekilde ve paket sahibini açıkça tanımlıyor mu?

1. Paket sahibi [NuGet.org hesabı için 2FA etkin](individual-accounts.md#enable-two-factor-authentication-2fa)mi?

1. Paket KIMLIĞI ön eki altında sahip tarafından zaten gönderilen paketlerin önemli bir sayısı mı?

1. Paket KIMLIĞI ön eki, tek bir sahibe veya kuruluşa ait olmaması gereken ortak bir şeydir mi?

1. Paket kimliği ön eki, topluluk için belirsizlik ve karışıklık neden oluyordu?

1. Paket KIMLIĞI öneki ile eşleşen paketlerin tanımlayıcı özellikleri açık ve tutarlı (özellikle paket yazarı)?

1. Paketlerde bir lisans var ( [Lisans](../reference/nuspec.md#license) meta verileri öğesi kullanılıyor ve kullanımdan kaldırılmakta olan LICENSEURL 'si değil)?

1. Paketlerde bir simge varsa (Iurl meta veri öğesi kullanılarak), aynı zamanda [Icon](../reference/nuspec.md#icon) meta veri öğesini de kullanıyor (Iurl 'yi kaldırma gereksinimi değildir)?

## <a name="third-party-feed-provider-scenarios"></a>Üçüncü taraf akış sağlayıcısı senaryoları

Üçüncü taraf bir akış sağlayıcısı, ön ek ayırmaları sağlamak üzere kendi hizmetini uygulamayla ilgileniyorsanız, NuGet v3 akış sağlayıcılarındaki arama hizmetini değiştirerek bunu yapabilirsiniz. Akış arama hizmeti 'nin eklenmesi, aşağıdaki v3 akışlarına yönelik örneklerle *doğrulanmış* özelliği eklemektir. NuGet istemcisi v2 akışındaki eklenen özelliği desteklemez.

Daha fazla bilgi için, [API 'nin arama hizmeti hakkındaki belgelere](../api/search-query-service-resource.md)bakın.

## <a name="package-id-prefix-reservation-dispute-policy"></a>Paket KIMLIĞI önek ayırma Itiraz Ilkesi
[NuGet.org](https://www.nuget.org) üzerinde bir sahibe, yukarıda listelenen ölçütlere karşılık gelen bir paket kimliği ön eki ayırması veya herhangi bir ticari marka ya da telif hakkı üzerinde kuruluşa ait, lütfen söz konusu kimliğe [support@nuget.org](mailto:support@nuget.org) sahip e-posta ile ön ek ve atanan önek ayırmasını görüntüleme nedeni.

