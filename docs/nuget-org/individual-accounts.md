---
title: Bireysel hesaplar
description: NuGet.org üzerindeki tek acccounts paketlerini yayımlamak için gereklidir
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: e1e31e0534706dab43f8d7b1b0db059cd6f29b80
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427559"
---
# <a name="individual-accounts"></a>Bireysel hesaplar

Paketleri NuGet.org üzerinde yönetmek ve yayımlamak için ayrı bir hesap oluşturmanız gerekir.

## <a name="individual-accounts-vs-organization-accounts"></a>Kuruluş hesapları ve bireysel hesaplar

(Kullanıcı) bireysel hesabınızın kimliğinizi nuget.org ve kuruluşların herhangi bir sayıda üyesi olabilir. Bir paketi tek bir hesaba ait olabilir gibi bir kuruluş hesabına ait olabilir. Paketi tüketicileri bir bireysel hesabı veya kuruluş hesabı arasındaki fark görmüyorum: her ikisi de paketi olarak görünen `owners`.

Bir kuruluş hesabı, bir veya daha fazla bireysel hesaplar, üyelere sahiptir. Bu üyeleri, sahipliği için tek bir kimlik korurken bir dizi paketleri yönetebilirsiniz.

## <a name="add-a-new-individual-account"></a>Yeni tek bir Hesap Ekle

NuGet.org hesabı oluşturmak için kişisel bir Microsoft hesabı (MSA) veya bir Azure Active Directory (AAD) hesabı olması gerekir. Biri yoksa yapabilecekleriniz [oluşturma](https://signup.live.com) biri. MSA veya AAD hesabınız varsa, aşağıdaki adımları izleyin.

1. Git [NuGet.org oturum açma sayfasına](https://www.nuget.org/users/account/LogOn).

1. Tıklayarak **Microsoft'ta oturum açma** düğmesi.

1. Microsoft hesabınızı veya Azure Active Directory hesabı ayrıntılarını girin.

1. Lütfen tıklayın **Evet** için verilecek izinlerini kabul etmenizi *NuGet.org* uygulama.

   ![NuGet.org için izinleri verme](media/nuget-org-permissions.png)

1. İçin yönlendirilirsiniz *nuget.org*ve bir kullanıcı adı kayıt istenir.

1. Giriş kutusuna kullanıcı adını belirtin. Lütfen unutmayın kullanıcıadı **olduğu** hassas durumda ve değiştirilemez ya da daha sonra yeniden adlandırıldı.

   ![NuGet.org bir kullanıcı adı belirtin](media/nuget-org-register.png) 

1. Tıklayın **kaydetme** düğmesi.

Artık bir NuGet.org hesabı var. Hesap Yönetimi gerçekleştirebileceğiniz [hesap ayarları](https://www.nuget.org/account) sayfası.
