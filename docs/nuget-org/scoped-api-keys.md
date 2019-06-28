---
title: Kapsamlı API anahtarları
description: Paketleri göndermek için kullandığınız API anahtarları denetimini elinize alın
author: mikejo5000
ms.author: mikejo
ms.date: 06/04/2019
ms.topic: conceptual
ms.openlocfilehash: 12d12d5294a474c4d3e4f5d3cad468bb515d21d5
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427502"
---
# <a name="scoped-api-keys"></a>Kapsamlı API anahtarları

NuGet paket dağıtımı için daha güvenli bir ortam sağlamak için API anahtarları denetiminizde kapsamları ekleyerek alabilir.

API'leri daha iyi denetim API anahtarlarınızı kapsamına olanağı sağlar. Şunları yapabilirsiniz:

- Farklı paketlerle değişen sona erme zaman dilimleri için kullanılabilecek birden çok kapsamı belirlenmiş API anahtarları oluşturun.
- API anahtarları güvenli bir şekilde edinin.
- Paket Uygulanabilirlik değiştirmek için mevcut API anahtarları düzenleyin.
- Yenileyin veya diğer anahtarlar kullanarak işlemleri hampering olmadan var olan API anahtarlarını silin.

## <a name="why-do-we-support-scoped-api-keys"></a>Kapsamlı API anahtarları neden destekliyoruz?

Daha hassas izinlere sahip olmasını sağlamak API anahtarları için kapsamları destekliyoruz. Daha önce bir hesap için tek bir API anahtarı NuGet sunulur ve bu yaklaşımı birkaç sakıncaları vardı:

- **Tüm paketleri denetlemek için bir API anahtarı**. Tüm paketleri yönetmek için kullanılan tek bir API anahtarı ile birden fazla Geliştirici farklı paketlerle ilgili olduğunda ve bir yayımcı hesabı paylaştıkları anahtarı güvenli bir şekilde paylaşmak zor olabilir.
- **Tüm izinleri veya hiçbiri**. API anahtarı erişimi olan herkes tüm izinlere sahiptir (yayımlama, gönderme ve un listesi) paketleri. Bu ortamda birden fazla takımlı arzu değil genellikle.
- **Tek hata noktası**. Tek bir API anahtarı, aynı zamanda bir tek hata noktası anlamına gelir. Anahtar tehlikedeyse, hesapla ilişkili tüm paketleri olası tehlikeye girebilir. API anahtarını yenileme sızıntısı Tak ve Kullan bir CI/CD akışınızı kesintiye uğramasını önlemek için tek yoludur. Ayrıca, bir kişi (örneğin, bir çalışan kuruluştan ayrılıyor) için API anahtarı erişimi iptal etmek istediğinizde durumlar olabilir. Bugün bu durumu çözmek için temiz bir yol değil.

Mevcut iş akışları hiçbiri ihlal emin olmasını sağlarken bu sorunları gidermeye yönelik kapsamlı API anahtarları ile sizi çalışırız.

## <a name="acquire-an-api-key"></a>Bir API anahtarı alma

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

## <a name="create-scoped-api-keys"></a>Kapsamlı API anahtarları oluşturma

Gereksinimlerinize göre birden çok API anahtarları oluşturabilirsiniz. Bir API anahtarı bir veya daha fazla paketlere uygulamaları, belirli ayrıcalıkları değişen kapsamlar ve ilişkili bir sona erme tarihi vardır.

Aşağıdaki örnekte adlı bir API anahtarı sahip `Contoso service CI` belirli paketleri göndermek için kullanılabilir `Contoso.Service` paketler ve 365 gün boyunca geçerli olur. Bu, farklı paketler aynı kuruluş çalışma ve takım üyeleri farklı ekipler yalnızca üzerinde çalıştıkları paket için ayrıcalıkları verir anahtarı nerede sağlanır, tipik bir senaryodur. Sona erme eski veya unutulan anahtarları önlemek için bir mekanizma işlev görür.

![API anahtarları oluşturma](media/scoped-api-keys-create-new.png)

## <a name="use-glob-patterns"></a>Glob desenleri kullanın

Birden çok paket üzerinde çalışıyorsanız ve paketleri yönetmek için büyük bir listeniz varsa, birlikte birden fazla paket seçmek için Glob desenlerinin kullanmayı da tercih edebilirsiniz. Örneğin, belirli kapsamına vermek isterseniz, tümü için bir anahtar ile olan kimliği başlar paketleri `Fabrikam.Service`, belirterek bunu yapabilirsiniz `fabrikam.service.*` içinde **Glob deseni** metin kutusu.

![API anahtarları oluşturma](media/scoped-api-keys-glob-pattern.png)

API anahtarı izinlerini belirlemek için Glob desenleri kullanarak glob deseni ile eşleşen yeni paketler için de geçerlidir. Örneğin, adlı yeni bir paket göndermeyi denerseniz `Fabrikam.Service.Framework`, paket glob deseni ile eşleşen itibaren daha önce oluşturulan anahtar ile bunu yapabilirsiniz `fabrikam.service.*`.

## <a name="obtain-api-keys-securely"></a>Güvenli bir şekilde API anahtarlarını edinin

Güvenlik için yeni oluşturulan anahtarı ekranda asla gösterilir ve yalnızca kullanılabilir kullanarak **kopyalama** düğmesi. Benzer şekilde, sayfa yenilendikten sonra anahtarın erişilebilir değil.

![API anahtarları oluşturma](media/scoped-api-keys-obtain-keys.png)

## <a name="edit-existing-api-keys"></a>Var olan API anahtarlarını Düzenle

Anahtar izinler ve kapsamlar anahtarın kendisini değiştirmeden güncelleştirmek isteyebilirsiniz. Tek bir paket için belirli kapsamlar ile bir anahtar varsa, bir veya daha çok diğer paketleri aynı kapsamlar uygulamak seçebilirsiniz.

![API anahtarları oluşturma](media/scoped-api-keys-edit.png)

## <a name="refresh-or-delete-existing-api-keys"></a>Yenileme veya var olan API anahtarları silme

Anahtar yenilemek hesap sahibi seçebilirsiniz, durumda izninin (paket), kapsam ve bitiş tarihi aynı kalır, ancak yeni bir anahtar eski anahtarı kullanılabilmesini verilir. Bu eski anahtarları yönetme konusunda yararlı olur ya da herhangi bir API anahtarı sızıntı potansiyeli olduğu.

![API anahtarları oluşturma](media/scoped-api-keys-refresh.png)

Bu anahtarlar artık gerekmeyen silmeyi seçebilirsiniz. Bir anahtarı silme, anahtar kaldırır ve kullanılamaz hale getirir.

## <a name="faqs"></a>SSS

### <a name="what-happens-to-my-old-legacy-api-key"></a>Eski hesabımın (eski) API anahtarı ne olacak?

Eski API anahtarınızı (eski) çalışmaya devam eder ve çalışmak istediğiniz sürece çalışabilir. Ancak, bunlar 365 günden fazla bir süre için bir paket göndermeye kullanılmamış, bu anahtarlar kullanımdan kaldırılacaktır. Diğer ayrıntılar için blog gönderisine bakın [değişiklikleri için süresi dolan API anahtarları](https://blog.nuget.org/20160825/Changes-to-Expiring-API-Keys.html). Bu anahtar artık yenileyebilirsiniz. Eski anahtarı silin ve yeni bir kapsamı belirlenmiş anahtar yerine oluşturmanız gerekir.

> [!NOTE]
> Bu anahtar, tüm paketleri tüm izinlere sahiptir ve her zaman geçerli olsun. Bu anahtarı siliniyor ve kapsamlı izinlere ve kesin süre sonu ile yeni anahtarları oluşturma dikkate almalısınız.

### <a name="how-many-api-keys-can-i-create"></a>Kaç tane API anahtarları oluşturabilirim?

API anahtarları oluşturabileceğiniz, sayısına bir sınır yoktur. Ancak biz, size burada bilgi ve bunları kullanan birçok eski anahtarlarla sonunda değil, yönetilebilir bir sayıya tutmak önerin.

### <a name="can-i-delete-my-legacy-api-key-or-discontinue-using-now"></a>Ben hesabımın eski bir API anahtarı silebilir veya artık kullanmayı Sonlandırabileceğiniz?

Evet. Yapabilecekleriniz--ve büyük olasılıkla eski API anahtarınızı silmeniz gerekir.

### <a name="can-i-get-back-my-api-key-that-i-deleted-by-mistake"></a>Yanlışlıkla silinen hesabımın API anahtarı geri alabilirim?

Hayır. Silindikten sonra yalnızca yeni anahtarları oluşturabilirsiniz. Yanlışlıkla silinen anahtarlar için olası hiçbir kurtarma yok.

### <a name="does-the-old-api-key-continue-to-work-upon-api-key-refresh"></a>Eski API anahtarını API anahtarı yenileme sırasında çalışmaya devam eder mi?

Hayır. Bir anahtarı'nı yenilemeyi sonra yeni bir anahtar kapsamını, izni ve geçerlilik eskisi sahip oluşturulan. Eski anahtarı mevcut olmaktan çıkar.

### <a name="can-i-give-more-permissions-to-an-existing-api-key"></a>Ben, var olan bir API anahtarı için daha fazla izin verebilir misiniz?

Kapsam değiştirilemedi. ancak geçerli değildir paket listesi düzenleyebilirsiniz.

### <a name="how-do-i-know-if-any-of-my-keys-expired-or-are-getting-expired"></a>Herhangi bir anahtarlarımı süresi doldu veya süresi dolmuş nasıl anlarım?

Herhangi bir tuşa süresi dolarsa, sayfanın üstünde bir uyarı iletisi aracılığıyla bildirin olanak tanır. Üzerinde önceden çalışabilir, böylece biz de uyarı e-posta için hesap sahibi anahtarın süresi dolmadan önce on gün gönderin.