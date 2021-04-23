---
title: Bireysel hesaplar-NuGet.org
description: Paketleri yayımlamak için NuGet.org üzerindeki ayrı hesaplar gereklidir
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 5224a4f5be519e1d72285562c1611d047582f7de
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901570"
---
# <a name="individual-accounts-on-nugetorg"></a>NuGet.org üzerinde ayrı hesaplar

NuGet.org 'de paketleri yayımlamak ve yönetmek için tek bir hesap oluşturmanız gerekir.

## <a name="individual-accounts-vs-organization-accounts"></a>Bireysel hesaplar ve kuruluş hesapları

Bireysel (Kullanıcı) hesabınız NuGet.org üzerinde kimliğiniz ve herhangi bir sayıda kuruluşun üyesi olabilir. Bir paket, tek bir hesaba ait olabilir gibi bir kuruluş hesabına ait olabilir. Paket tüketicileri, tek bir hesap veya kuruluş hesabı arasında herhangi bir farklılık görmez: her ikisi de paket olarak görünürler `owners` .

Bir kuruluş hesabının üyeleri olarak bir veya daha fazla bireysel hesabı vardır. Bu Üyeler, sahiplik için tek bir kimlik sağlarken bir paket kümesini yönetebilir.

## <a name="add-a-new-individual-account"></a>Yeni bir bireysel hesap ekleyin

Bir NuGet.org hesabı oluşturmak için bir kişisel Microsoft hesabı (MSA) veya bir Azure Active Directory (AAD) hesabınız olması gerekir. Bir tane yoksa, bir tane [oluşturabilirsiniz](https://signup.live.com) . MSA veya AAD hesabınız varsa aşağıdaki adımları izleyin.

1. [NuGet.org oturum açma sayfasına](https://www.nuget.org/users/account/LogOn)gidin.

1. **Microsoft hesabıyla oturum açın** düğmesine tıklayın.

1. Microsoft hesabı veya Azure Active Directory hesabı ayrıntılarınızı girin.

1. *NuGet.org* uygulamasına verilecek izinleri kabul etmek Için lütfen **Evet** ' e tıklayın.

   ![NuGet.org için izinler verme](media/nuget-org-permissions.png)

1. *NuGet.org*'e yönlendirilirsiniz ve bir Kullanıcı adı kaydetmeniz istenir.

1. Giriş kutusunda Kullanıcı adını belirtin. Kullanıcı adının büyük/küçük harfe **duyarlı olduğunu ve** daha sonra değiştirilemeyeceğini veya yeniden adlandırılamayacağını lütfen unutmayın.

   ![NuGet.org üzerinde bir Kullanıcı adı belirtin](media/nuget-org-register.png) 

1. **Kaydet** düğmesine tıklayın.

Artık bir NuGet.org hesabınız var. Hesap yönetimi 'ni [Hesap ayarları](https://www.nuget.org/account) sayfasında gerçekleştirebilirsiniz.

## <a name="enable-two-factor-authentication-2fa"></a>İki öğeli kimlik doğrulamayı etkinleştirme (2FA)

İki öğeli kimlik doğrulama veya 2FA, Web siteleri veya uygulamalar üzerinde oturum açarken kullanılan ek bir güvenlik katmanıdır. 2FA sayesinde, Microsoft hesabınızla (MSA) oturum açmanız ve yalnızca bildiğiniz veya erişiminiz olan başka bir kimlik doğrulama biçimi sağlamanız gerekir. Hesabınızı daha iyi korumak için iki öğeli kimlik doğrulamayı etkinleştirin (önerilir).

1. Hesabınızda oturum açarken profilinizi açın ve **oturum açma hesabı** altında **Etkinleştir** ' i seçin.

   ![2FA 'yı etkinleştir](media/nuget-org-register-2fa.png)

   *NuGet.org*' de bir sonraki oturum açışınızda sizden ek kimlik bilgileri istenmeyeceğini belirten bir ileti görürsünüz.

2. Kimlik doğrulamasını Şu anda tamamladıktan sonra oturumunuzu kapatıp yeniden oturum açın.

3. Oturum açtığınızda, ikinci bir kimlik doğrulama biçimi olarak metin veya e-posta seçin.

   Microsoft hesabı zaten ilişkilendirilmiş telefon numarasını veya e-postayı doğrulayın. Hesabınız için yeni bir telefon numarası veya e-posta girmeniz gerekebilir. Bu durumda, istenen bilgileri belirtildiği gibi girin ve **İleri**' ye tıklayın.

   ![2FA 'yı etkinleştirin ve telefon girin](media/nuget-org-sign-in-2fa.png)

4. Cihazınızı veya e-posta hesabınızı denetleyin ve az önce gönderdiğiniz kodu girin.

   ![2FA 'yı etkinleştirin ve kodu girin](media/nuget-org-enter-code-2fa.png)

5. Iki öğeli kimlik doğrulamayı tamamlamaya yönelik ek yönergeleri izleyin.

> [!Tip]
> NuGet.org hesabınız için 2FA 'yı etkinleştirmek, NuGet.org 'de oturum açmak için kullandığınız Microsoft hesabı bağlantılı olabilecek diğer hesaplar veya hizmetler için kimlik doğrulama ayarlarını etkilemez.

## <a name="delete-a-nugetorg-account"></a>Bir NuGet.org hesabını silme

NuGet.org hesabını silme gibi hesapla ilgili ek görevlerle ilgili yardım için bkz. [NuGet.org Account Management](nuget-org-faq.md#nugetorg-account-management).
