---
ms.openlocfilehash: 20851cd71cc5eb6735fe5e0cd8b0f314f9100be4
ms.sourcegitcommit: e65180e622f6233b51bb0b41d0e919688083eb26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419909"
---
1. [NuGet.org hesabınızda oturum açın](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) veya henüz yoksa bir hesap oluşturun.

   Hesabınızı oluşturma hakkında daha fazla bilgi için bkz. [bireysel hesaplar](../../nuget-org/individual-accounts.md).

1. Kullanıcı adınızı (sağ üst köşedeki) seçin ve ardından **API anahtarları**' nı seçin.

1. **Oluştur**' u seçin, anahtarınız için bir ad sağlayın, **kapsamları Seç > Gönder**' i seçin. **Glob deseninin*** girin ve ardından **Oluştur**' u seçin. (Kapsamlar hakkında daha fazla bilgi için aşağıya bakın.)

1. Anahtar oluşturulduktan sonra, CLı 'de ihtiyacınız olan erişim anahtarını almak için **Kopyala** ' yı seçin:

    ![API anahtarını panoya kopyalama](../media/QS_Create-02-APIKey.png)

1. **Önemli**: Anahtarı daha sonra tekrar kopyalayamadığından Anahtarınızı güvenli bir konuma kaydedin. API anahtarı sayfasına geri dönerseniz, kopyalamak için anahtarı yeniden oluşturmanız gerekir. Artık paketleri CLı aracılığıyla göndermek istemiyorsanız API anahtarını da kaldırabilirsiniz.

Kapsam oluşturma, farklı amaçlar için ayrı API anahtarları oluşturmanıza olanak sağlar. Her anahtarın süre sonu zaman çerçevesi vardır ve belirli paketlere (veya glob desenlerine) kapsamı atanabilir. Her anahtar Ayrıca belirli işlemlere göre kapsamlandırılır: yeni paketleri ve güncelleştirmeleri gönderme, yalnızca güncelleştirmelerin gönderimi veya listesini kaldırma. Kapsam aracılığıyla, kuruluşunuzda yalnızca ihtiyaç duydukları izinlere sahip olmaları için paketleri yöneten farklı kişiler için API anahtarları oluşturabilirsiniz. Daha fazla bilgi için bkz. [KAPSAMLı API anahtarları](../../nuget-org/scoped-api-keys.md).