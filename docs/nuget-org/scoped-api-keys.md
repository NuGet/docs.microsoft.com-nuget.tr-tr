---
title: Kapsamlı API anahtarları
description: Paketleri göndermek için kullandığınız API anahtarlarının denetimini al
author: mikejo5000
ms.author: mikejo
ms.date: 06/04/2019
ms.topic: conceptual
ms.openlocfilehash: a3d2504528249f3545e2eb5d9bce7713029638db
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901596"
---
# <a name="scoped-api-keys"></a>Kapsamlı API anahtarları

NuGet 'i paket dağıtımı için daha güvenli bir ortam yapmak üzere kapsamlar ekleyerek API anahtarlarının denetimini alabilirsiniz.

API Anahtarlarınıza kapsam sağlama özelliği, API 'lerinize daha iyi denetim sağlar. Seçenekleriniz şunlardır:

- Değişen süre sonu zaman çerçevelerine sahip farklı paketler için kullanılabilen birden çok kapsamlı API anahtarı oluşturun.
- API anahtarlarını güvenli bir şekilde edinin.
- Paket uygulanabilirliğini değiştirmek için mevcut API anahtarlarını düzenleyin.
- Diğer anahtarları kullanarak işlemleri etkilemeden mevcut API anahtarlarını yenileyin veya silin.

## <a name="why-do-we-support-scoped-api-keys"></a>Neden kapsamlı API anahtarlarını destekliyoruz?

Daha ayrıntılı izinleriniz olmasını sağlamak için API anahtarları için kapsamları destekliyoruz. Daha önce, NuGet bir hesap için tek bir API anahtarı önerdi ve bu yaklaşım birkaç dezavantaja sahipti:

- **Tüm paketleri denetlemek Için BIR API anahtarı**. Tüm paketleri yönetmek için kullanılan tek bir API anahtarı ile, birden çok geliştirici farklı paketlere dahil edildiğinde ve bir yayımcı hesabını paylaştıklarında, anahtarı güvenli bir şekilde paylaşmak zordur.
- **Tüm izinler veya hiçbiri**. API anahtarına erişimi olan herkes, paketler üzerinde tüm izinlere (yayımlama, gönderme ve kaldırma) sahiptir. Bu, genellikle birden çok ekibin bulunduğu ortamda istenmez.
- **Tek hata noktası**. Tek bir API anahtarı aynı zamanda tek bir hata noktası anlamına gelir. Anahtar tehlikeye girerse, hesapla ilişkili tüm paketlerin güvenliği tehlikeye girebilir. API anahtarını yenilemek, sızıntıyı eklemenin ve CI/CD iş akışınıza kesintiye uğramaktan kaçınmanın tek yoludur. Ayrıca, bir kişiye ait API anahtarına erişimi iptal etmek istediğiniz durumlar olabilir (örneğin, bir çalışan kuruluştan ayrıldığında). Bunu bugün işlemek için temiz bir yol yoktur.

Kapsamlı API anahtarları sayesinde bu sorunları gidermek için mevcut iş akışlarının hiçbirini bozmadığından emin olun.

## <a name="acquire-an-api-key"></a>API anahtarı alma

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

## <a name="create-scoped-api-keys"></a>Kapsamlı API anahtarları oluşturma

Gereksinimlerinize göre birden çok API anahtarı oluşturabilirsiniz. Bir API anahtarı bir veya daha fazla pakete uygulanabilir, belirli ayrıcalıklar veren ve bunlarla ilişkili bir sona erme tarihi olan farklı kapsamlara sahip olabilir.

Aşağıdaki örnekte, `Contoso service CI` belirli paketlere yönelik paketleri göndermek için kullanılabilecek adlı BIR API anahtarınız vardır `Contoso.Service` ve 365 gün için geçerlidir. Bu, aynı kuruluştaki farklı takımların farklı paketlerde çalıştığı tipik bir senaryodur ve takımın üyelerine, yalnızca üzerinde çalıştıkları paket için kendilerine ayrıcalık veren anahtarı sağlarlar. Süre sonu eski veya unutulan anahtarları önleme mekanizması olarak görev yapar.

![API anahtarları oluşturma](media/scoped-api-keys-create-new.png)

## <a name="use-glob-patterns"></a>Glob desenlerini kullanma

Birden çok paket üzerinde çalışıyorsanız ve yönetmek üzere büyük bir paket listeniz varsa, birden fazla paketi birlikte seçmek için glob desenlerini kullanmayı seçebilirsiniz. Örneğin, KIMLIĞI ile başlayan tüm paketler için bir anahtara belirli kapsamlar vermek isterseniz `Fabrikam.Service` , bunu, `fabrikam.service.*` **Glob deseninin** metin kutusunda belirterek yapabilirsiniz.

![API anahtarları oluşturma-2](media/scoped-api-keys-glob-pattern.png)

API anahtarı izinlerinin belirlenmesi için glob desenlerinin kullanılması, glob deseniyle eşleşen yeni paketler için de geçerlidir. Örneğin, adlı yeni bir paket göndermeye çalışırsanız `Fabrikam.Service.Framework` , paket glob düzeniyle eşleştiğinden bu anahtarı daha önce oluşturulan anahtarla yapabilirsiniz `fabrikam.service.*` .

## <a name="obtain-api-keys-securely"></a>API anahtarlarını güvenli bir şekilde edinin

Güvenlik için, yeni oluşturulan bir anahtar ekranda hiçbir şekilde gösterilmez ve yalnızca **Kopyala** düğmesi kullanılarak kullanılabilir. Benzer şekilde, sayfa yenilendikten sonra anahtara erişilemez.

![API anahtarları oluştur-3](media/scoped-api-keys-obtain-keys.png)

## <a name="edit-existing-api-keys"></a>Mevcut API anahtarlarını Düzenle

Anahtarı değiştirmeden anahtar izinlerini ve kapsamları da güncelleştirmek isteyebilirsiniz. Tek bir paket için belirli kapsamlarla bir anahtarınız varsa, aynı kapsamları bir veya daha fazla pakete uygulamayı seçebilirsiniz.

![API anahtarları oluşturma-4](media/scoped-api-keys-edit.png)

## <a name="refresh-or-delete-existing-api-keys"></a>Mevcut API anahtarlarını yenileme veya silme

Hesap sahibi anahtarı yenilemeyi seçebilir ve bu durumda izin (paketlerdeki), kapsam ve süre sonu aynı kalır, ancak eski anahtarı kullanılamaz hale getirmek için yeni bir anahtar verilir. Bu, eski anahtarları yönetirken veya bir API anahtarı sızıntısı için olası bir sorun olduğu durumlarda faydalıdır.

![API anahtarları oluşturma-5](media/scoped-api-keys-refresh.png)

Artık gerekmiyorsa bu anahtarları silmeyi de tercih edebilirsiniz. Anahtar silindiğinde anahtar kaldırılır ve kullanılamaz hale gelir.

## <a name="faqs"></a>SSS

### <a name="what-happens-to-my-old-legacy-api-key"></a>Eski (eski) API anahtarım için ne olur?

Eski API anahtarınız (eski) çalışmaya devam eder ve çalışmasını istediğiniz sürece çalışabilir. Ancak, bir paketi göndermek için 365 günden daha uzun bir süre kullanılmadığından bu anahtarlar devre dışı bırakılır. Daha ayrıntılı bilgi için bkz. blog gönderisi [süresi dolan API anahtarları](https://blog.nuget.org/20160825/Changes-to-Expiring-API-Keys.html). Bu anahtarı artık yenileyemezsiniz. Bunun yerine eski anahtarı silmeniz ve yeni bir kapsamlı anahtar oluşturmanız gerekir.

> [!NOTE]
> Bu anahtar tüm paketlerde tüm izinlere sahiptir ve süresi dolmayacaktır. Bu anahtarı silmeyi ve kapsamlı izinlerle yeni anahtar oluşturmayı ve kesin süre sonu kullanmayı göz önünde bulundurmanız gerekir.

### <a name="how-many-api-keys-can-i-create"></a>Kaç tane API anahtarı oluşturabilirim?

Oluşturabileceğiniz API anahtarı sayısı için bir sınır yoktur. Bununla birlikte, bu süreyi yönetilebilir bir sayıya tutmanızı öneririz; Böylece, nerede ve kim tarafından kullanıldığı hakkında bilgi sahibi olmadan çok sayıda eski anahtara sahip olabilirsiniz.

### <a name="can-i-delete-my-legacy-api-key-or-discontinue-using-now"></a>Eski API anahtarımı silebilir veya şimdi kullanmaya devam edebilir miyim?

Evet. Ve büyük olasılıkla eski API anahtarınızı silmeniz gerekir.

### <a name="can-i-get-back-my-api-key-that-i-deleted-by-mistake"></a>Yanlışlıkla sildiğim API anahtarımı geri alabilir miyim?

Hayır. Silindikten sonra yalnızca yeni anahtarlar oluşturabilirsiniz. Yanlışlıkla silinen anahtarlar için bir kurtarma mümkün değildir.

### <a name="does-the-old-api-key-continue-to-work-upon-api-key-refresh"></a>Eski API anahtarı API anahtarı yenileme sonrasında çalışmaya devam eder mi?

Hayır. Bir anahtarı yeniledikten sonra, eskisiyle aynı kapsam, izin ve süre sonu olan yeni bir anahtar oluşturulur. Eski anahtar mevcut olmaya sona erer.

### <a name="can-i-give-more-permissions-to-an-existing-api-key"></a>Var olan bir API anahtarına daha fazla izin verebilir miyim?

Kapsamı değiştiremezsiniz, ancak geçerli olduğu paket listesini düzenleyebilirsiniz.

### <a name="how-do-i-know-if-any-of-my-keys-expired-or-are-getting-expired"></a>Nasıl yaparım? anahtarlarım zaman aşımına uğradı veya zaman aşımına uğradı.

Herhangi bir anahtarın süresi dolarsa, sayfanın üst kısmında bir uyarı iletisi aracılığıyla size bilgi vereceğiz. Ayrıca, anahtar sona ermeden önce bir uyarı e-postası göndeririz ve bu sayede, daha iyi bir şekilde hareket edebilirsiniz.