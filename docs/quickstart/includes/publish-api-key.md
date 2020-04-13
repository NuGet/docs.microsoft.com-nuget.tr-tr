---
ms.openlocfilehash: 20851cd71cc5eb6735fe5e0cd8b0f314f9100be4
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "68419909"
---
1. [nuget.org hesabınızda oturum açın](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) veya hesabınız yoksa bir hesap oluşturun.

   Hesabınızı oluşturma hakkında daha fazla bilgi için [Bireysel hesaplara](../../nuget-org/individual-accounts.md)bakın.

1. Kullanıcı adınızı seçin (sağ üstte), ardından **API Tuşlarını**seçin.

1. **Oluştur'u**seçin, anahtarınız için bir ad sağlayın, İtme > **Kapsamları Seçin'i**seçin. **Glob deseni**için * girin, sonra **Oluştur'u**seçin. (Kapsamlar hakkında daha fazla şey için aşağıya bakın.)

1. Anahtar oluşturulduktan sonra **Copy** CLI'de ihtiyacınız olan erişim anahtarını almak için Kopyala'yı seçin:

    ![API anahtarını panoya kopyalama](../media/QS_Create-02-APIKey.png)

1. **Önemli**: Anahtarınızı daha sonra tekrar kopyalayamayacağınız için anahtarınızı güvenli bir yere kaydedin. API anahtar sayfasına geri dönerseniz, kopyalamak için anahtarı yeniden oluşturmanız gerekir. Paketleri artık CLI üzerinden itmek istemiyorsanız API anahtarını da kaldırabilirsiniz.

Kapsam, farklı amaçlar için ayrı API anahtarları oluşturmanıza olanak tanır. Her anahtarın son kullanma süresi vardır ve belirli paketlere (veya glob desenlerine) kapsamlandırılabilir. Her anahtar belirli işlemlere de yöneliktir: yeni paketlerin ve güncelleştirmelerin itilmesi, yalnızca güncelleştirmelerin itilmesi veya liste dışı bırakma. Kapsam oluşturma yoluyla, kuruluşunuz için paketleri yöneten farklı kişiler için yalnızca gereksinim duydukları izinlere sahip olacak şekilde API anahtarları oluşturabilirsiniz. Daha fazla bilgi için [kapsamlı API anahtarlarına](../../nuget-org/scoped-api-keys.md)bakın.