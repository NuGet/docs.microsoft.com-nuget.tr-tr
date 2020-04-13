---
title: Kapsamlı API anahtarları
description: Paketleri itmek için kullandığınız API anahtarlarını kontrol altına alın
author: mikejo5000
ms.author: mikejo
ms.date: 06/04/2019
ms.topic: conceptual
ms.openlocfilehash: 12d12d5294a474c4d3e4f5d3cad468bb515d21d5
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427502"
---
# <a name="scoped-api-keys"></a>Kapsamlı API anahtarları

NuGet'i paket dağıtımı için daha güvenli bir ortam haline getirmek için kapsam ekleyerek API anahtarlarının denetimini alabilirsiniz.

API tuşlarınıza kapsam sağlama özelliği, API'leriniz üzerinde daha iyi denetim sağlar. Şunları yapabilirsiniz:

- Değişen son kullanma tarihlerine sahip farklı paketler için kullanılabilecek birden çok kapsamlı API anahtarı oluşturun.
- API tuşlarını güvenli bir şekilde edinin.
- Paket uygulanabilirliğini değiştirmek için varolan API anahtarlarını edin.
- Diğer anahtarları kullanarak işlemleri aksatmadan varolan API tuşlarını yenileyin veya silin.

## <a name="why-do-we-support-scoped-api-keys"></a>Kapsamlı API anahtarlarını neden destekliyoruz?

Daha ince taneli izinlere sahip olmak için API anahtarlarının kapsamlarını destekliyoruz. Daha önce, NuGet bir hesap için tek bir API anahtarı sundu ve bu yaklaşımın birkaç dezavantajı vardı:

- **Tüm paketleri kontrol etmek için bir API anahtarı.** Tüm paketleri yönetmek için kullanılan tek bir API anahtarıyla, birden çok geliştirici farklı paketlerle ilgili olduğunda ve bir yayımcı hesabını paylaştıklarında anahtarı güvenli bir şekilde paylaşmak zordur.
- **Tüm izinler veya hiçbiri.** API anahtarına erişimi olan herkes paketlerdeki tüm izinlere (yayımlama, itme ve listeyi açma) sahiptir. Bu genellikle birden çok takım ile ortamda istenmez.
- **Tek hata noktası.** Tek bir API anahtarı da tek bir hata noktası anlamına gelir. Anahtar ele geçirilirse, hesapla ilişkili tüm paketler tehlikeye atılabilir. API anahtarının yenilenmesi, sızıntıyı kapatmanın ve CI/CD iş akışınızda bir kesintiyi önlemenin tek yoludur. Ayrıca, bir birey için API anahtarına erişimi iptal etmek istediğiniz durumlar da olabilir (örneğin, bir çalışan kuruluştur). Bugün bunu halletmenin temiz bir yolu yok.

Kapsamlı API anahtarlarıyla, varolan iş akışlarının hiçbirinin kırılmadığından emin olurken bu sorunları gidermeye çalışırız.

## <a name="acquire-an-api-key"></a>BIR API anahtarı edinme

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

## <a name="create-scoped-api-keys"></a>Kapsamlı API anahtarları oluşturma

Gereksinimlerinize göre birden çok API anahtarı oluşturabilirsiniz. API anahtarı bir veya daha fazla pakete uygulanabilir, belirli ayrıcalıklar veren farklı kapsamlara sahip ve bununla ilişkili bir son kullanma tarihi ne olabilir.

Aşağıdaki örnekte, belirli `Contoso service CI` `Contoso.Service` paketler için paketleri itmek için kullanılabilecek ve 365 gün boyunca geçerli olan bir API anahtarınız var. Bu, aynı kuruluştaki farklı ekiplerin farklı paketler üzerinde çalıştığı ve takım üyelerinin yalnızca üzerinde çalıştıkları paket için ayrıcalık sağlayan anahtar sağlandığı tipik bir senaryodur. Sona erme, eski veya unutulmuş anahtarları önlemek için bir mekanizma görevi görür.

![API tuşlarını oluşturma](media/scoped-api-keys-create-new.png)

## <a name="use-glob-patterns"></a>Glob desenleri kullanın

Birden çok paket üzerinde çalışıyorsanız ve yönetilecek büyük bir paket listesi varsa, birlikte birden çok paket seçmek için globbing desenleri kullanmayı seçebilirsiniz. Örneğin, kimliği ile başlayan tüm paketler için bir anahtara belirli `Fabrikam.Service`kapsamlar vermek isterseniz, `fabrikam.service.*` bunu **Glob desen** metin kutusunda belirterek yapabilirsiniz.

![API tuşlarını oluşturma](media/scoped-api-keys-glob-pattern.png)

API anahtar izinlerini belirlemek için glob desenleri kullanarak glob deseni eşleşen yeni paketler için de geçerlidir. Örneğin, adlı `Fabrikam.Service.Framework`yeni bir paket itmeye çalışırsanız, paket glob deseniyle `fabrikam.service.*`eşleştiğinden, bunu daha önce oluşturulan anahtarla yapabilirsiniz.

## <a name="obtain-api-keys-securely"></a>API tuşlarını güvenli bir şekilde edinin

Güvenlik için, yeni oluşturulan bir anahtar ekranda asla gösterilmez ve yalnızca **Kopyala** düğmesini kullanarak kullanılabilir. Benzer şekilde, sayfa yenilendikten sonra anahtara erişilemez.

![API tuşlarını oluşturma](media/scoped-api-keys-obtain-keys.png)

## <a name="edit-existing-api-keys"></a>Varolan API anahtarlarını edin

Anahtar izinlerini ve kapsamlarını anahtarın kendisini değiştirmeden de güncelleştirmek isteyebilirsiniz. Tek bir paket için belirli kapsam(lar) içeren bir anahtarınız varsa, aynı kapsam(lar)ı bir veya daha birçok pakete uygulamayı seçebilirsiniz.

![API tuşlarını oluşturma](media/scoped-api-keys-edit.png)

## <a name="refresh-or-delete-existing-api-keys"></a>Varolan API tuşlarını yenileme veya silme

Hesap sahibi anahtarı yenilemeyi seçebilir, bu durumda izin (paketlerde), kapsam ve son kullanma süresi aynı kalır, ancak eski anahtarı kullanılamaz hale getiren yeni bir anahtar verilir. Bu, eski anahtarları veya BIR API anahtarı sızıntısı için herhangi bir potansiyel olduğu durumlarda yönetilmesinde yararlıdır.

![API tuşlarını oluşturma](media/scoped-api-keys-refresh.png)

Artık gerekli değilse, bu anahtarları silmeyi de seçebilirsiniz. Bir anahtarı siler ve kullanılamaz hale getirir.

## <a name="faqs"></a>SSS

### <a name="what-happens-to-my-old-legacy-api-key"></a>Eski (eski) API anahtarıma ne olur?

Eski API anahtarınız (eski) çalışmaya devam eder ve istediğiniz sürece çalışabilir. Ancak, bir paketi itmek için 365 günden fazla kullanılmamışsa, bu anahtarlar kullanımdan kaldırılacaktır. Daha fazla bilgi için, süresi dolan API tuşlarına yapılan blog [gönderisi Değişiklikleri'ne](https://blog.nuget.org/20160825/Changes-to-Expiring-API-Keys.html)bakın. Bu anahtarı artık yenileyemezsiniz. Eski anahtarı silmeniz ve bunun yerine yeni bir kapsamlı anahtar oluşturmanız gerekir.

> [!NOTE]
> Bu anahtar tüm paketlerde tüm izinlere sahiptir ve süresi asla dolmaz. Bu anahtarı silmeyi ve kapsamlı izinler ve kesin son kullanma tarihi yle yeni anahtarlar oluşturmayı düşünmelisiniz.

### <a name="how-many-api-keys-can-i-create"></a>Kaç API anahtarı oluşturabilirim?

Oluşturabileceğiniz API anahtarlarının sayısında bir sınır yoktur. Ancak, nerede ve kim kullanıyor hiçbir bilgi ile çok bayat anahtarları sahip sona ermemek için yönetilebilir bir sayı tutmak için tavsiye ederiz.

### <a name="can-i-delete-my-legacy-api-key-or-discontinue-using-now"></a>Eski API anahtarımı silebilir miyim veya şimdi kullanmayı durdurabilir miyim?

Evet. Eski API anahtarınızı silebilirsiniz ve muhtemelen silmelisiniz.

### <a name="can-i-get-back-my-api-key-that-i-deleted-by-mistake"></a>Yanlışlıkla sildiğim API anahtarımı geri alabilir miyim?

Hayır. Silindikten sonra yalnızca yeni anahtarlar oluşturabilirsiniz. Yanlışlıkla silinen anahtarlar için kurtarma mümkün değildir.

### <a name="does-the-old-api-key-continue-to-work-upon-api-key-refresh"></a>Eski API anahtarı API anahtar yenileme üzerinde çalışmaya devam ediyor mu?

Hayır. Bir anahtarı yeniledikten sonra, eskiyle aynı kapsam, izin ve son kullanma süresine sahip yeni bir anahtar oluşturulur. Eski anahtar yok.

### <a name="can-i-give-more-permissions-to-an-existing-api-key"></a>Varolan bir API anahtarına daha fazla izin verebilir miyim?

Kapsamı değiştiremezsiniz, ancak geçerli olduğu paket listesini değiştirebilirsiniz.

### <a name="how-do-i-know-if-any-of-my-keys-expired-or-are-getting-expired"></a>Anahtarlarımın süresinin dolduğunu veya süresinin dolduğunu nasıl anlarım?

Herhangi bir anahtarın süresi dolursa, sayfanın üst kısmındaki bir uyarı iletisi aracılığıyla size haber vereceksiniz. Ayrıca, anahtarın süresinin bitiminden on gün önce hesap sahibine bir uyarı e-postası göndeririz, böylece bu konuda önceden iyi davranabilirsiniz.