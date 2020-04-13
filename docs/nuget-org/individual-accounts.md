---
title: Bireysel hesaplar - NuGet.org
description: paketleri yayınlamak için NuGet.org bireysel acccounts gereklidir
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 7951b3db0cdcaee0a1eb955a5bf6fedce24c79c9
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79429019"
---
# <a name="individual-accounts-on-nugetorg"></a>NuGet.org bireysel hesaplar

Paketleri NuGet.org yayınlamak ve yönetmek için ayrı bir hesap oluşturmanız gerekir.

## <a name="individual-accounts-vs-organization-accounts"></a>Bireysel hesaplar ve kuruluş hesapları

Bireysel (kullanıcı) hesabınız NuGet.org'daki kimliğinizdir ve herhangi bir sayıda kuruluşun üyesi olabilir. Paket, tek bir hesaba ait olduğu gibi bir kuruluş hesabına ait olabilir. Paket tüketicileri tek bir hesap la kuruluş hesabı arasında herhangi `owners`bir fark görmezler: her ikisi de paket olarak görünür.

Kuruluş hesabının üyeleri olarak bir veya daha fazla ayrı hesabı vardır. Bu üyeler, sahiplik için tek bir kimlik korurken bir dizi paketi yönetebilir.

## <a name="add-a-new-individual-account"></a>Yeni bir bireysel hesap ekleme

NuGet.org bir hesap oluşturmak için kişisel bir Microsoft hesabınız (MSA) veya Azure Etkin Dizin (AAD) hesabınız olması gerekir. Eğer yoksa, bir [oluşturabilirsiniz.](https://signup.live.com) MSA veya AAD hesabınız varsa aşağıdaki adımları izleyin.

1. [giriş NuGet.org sayfasına](https://www.nuget.org/users/account/LogOn)gidin.

1. Microsoft **ile Oturum Aç** düğmesine tıklayın.

1. Microsoft hesabınızı veya Azure Active Directory hesap bilgilerinizi girin.

1. *NuGet.org* başvurusuna verilecek izinleri kabul etmek için lütfen **Evet'i** tıklatın.

   ![NuGet.org izin verme](media/nuget-org-permissions.png)

1. *nuget.org*yönlendirilirsiniz ve bir kullanıcı adı kaydetmeniz istenir.

1. Giriş kutusundaki kullanıcı adını belirtin. Kullanıcı adının büyük/küçük harf **duyarlı olduğunu** ve daha sonra değiştirilemeyeceğini veya değiştirilemeyeceğini lütfen unutmayın.

   ![NuGet.org bir kullanıcı adı belirtin](media/nuget-org-register.png) 

1. **Kaydol** düğmesini tıklatın.

Artık NuGet.org bir hesabınız var. [Hesap ayarları](https://www.nuget.org/account) sayfasında hesap yönetimi gerçekleştirebilirsiniz.

## <a name="enable-two-factor-authentication-2fa"></a>İki faktörlü kimlik doğrulamayı etkinleştirme (2FA)

İki faktörlü kimlik doğrulama veya 2FA, web sitelerine veya uygulamalara giriş yaparken kullanılan ek bir güvenlik katmanıdır. 2FA ile Microsoft Hesabınızla (MSA) oturum açmanız ve yalnızca sizin bildiğiniz veya erişebildiğiniz başka bir kimlik doğrulama biçimi sağlamanız gerekir. Hesabınızı daha iyi korumak için iki faktörlü kimlik doğrulamayı (önerilir) etkinleştirin.

1. Hesabınıza giriş yaptığınızda, profilinizi açın ve **Giriş Hesabı**altında **Etkinleştir'i** seçin.

   ![2FA'yı etkinleştir](media/nuget-org-register-2fa.png)

   *nuget.org'da*bir sonraki oturum açtığınızda ek kimlik bilgilerinin isteneceğini belirten bir ileti görürsünüz.

2. Kimlik doğrulamasını şu anda tamamlamak için oturumaçın ve sonra yeniden oturum açın.

3. Oturum açken, ikinci bir kimlik doğrulama biçimi olarak metin veya e-posta yı seçin.

   Microsoft hesabınızla zaten ilişkili olan telefon numarasını veya e-postayı doğrulayın. Hesabınız için yeni bir telefon numarası veya e-posta girmeniz gerekebilir. Bu durumda, gerekli bilgileri talimat olarak girin ve **İleri'yi**tıklatın.

   ![2FA'yı etkinleştir](media/nuget-org-sign-in-2fa.png)

4. Cihazınızı veya e-posta hesabınızı kontrol edin ve size gönderilen kodu girin.

   ![2FA'yı etkinleştir](media/nuget-org-enter-code-2fa.png)

5. İki faktörlü kimlik doğrulamasını tamamlamak için ek yönergeleri izleyin.

> [!Tip]
> NuGet.org hesabınız için 2FA'yı etkinleştirmek, NuGet.org oturum açmak için kullandığınız Microsoft hesabıyla bağlantılı olabilecek diğer hesaplar veya hizmetler için kimlik doğrulama ayarlarını etkilemez.

## <a name="delete-a-nugetorg-account"></a>NuGet.org hesabı nı silme

NuGet.org hesabını silme gibi hesapla ilgili ek görevlerle ilgili yardım için NuGet.org [hesap yönetimine](nuget-org-faq.md#nugetorg-account-management)bakın.
