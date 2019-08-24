---
title: Bireysel hesaplar-NuGet.org
description: Paketleri yayımlamak için NuGet.org üzerindeki ayrı hesaplar gereklidir
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 63c6b5eb5ad635e436b4d53a5f833af35f72d76f
ms.sourcegitcommit: 7c9f157ba02d9be543de34ab06813ab1ec10192a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/23/2019
ms.locfileid: "69999974"
---
# <a name="individual-accounts-on-nugetorg"></a>NuGet.org üzerinde ayrı hesaplar

NuGet.org 'de paketleri yayımlamak ve yönetmek için tek bir hesap oluşturmanız gerekir.

## <a name="individual-accounts-vs-organization-accounts"></a>Bireysel hesaplar ve kuruluş hesapları

Bireysel (Kullanıcı) hesabınız NuGet.org üzerinde kimliğiniz ve herhangi bir sayıda kuruluşun üyesi olabilir. Bir paket, tek bir hesaba ait olabilir gibi bir kuruluş hesabına ait olabilir. Paket tüketicileri, tek bir hesap veya kuruluş hesabı arasında herhangi bir farklılık görmez: her ikisi de `owners`paket olarak görünürler.

Bir kuruluş hesabının üyeleri olarak bir veya daha fazla bireysel hesabı vardır. Bu Üyeler, sahiplik için tek bir kimlik sağlarken bir paket kümesini yönetebilir.

## <a name="add-a-new-individual-account"></a>Yeni bir bireysel hesap ekleyin

Bir NuGet.org hesabı oluşturmak için bir kişisel Microsoft hesabı (MSA) veya bir Azure Active Directory (AAD) hesabınız olması gerekir. Bir tane yoksa, bir tane [oluşturabilirsiniz](https://signup.live.com) . MSA veya AAD hesabınız varsa aşağıdaki adımları izleyin.

1. [NuGet.org oturum açma sayfasına](https://www.nuget.org/users/account/LogOn)gidin.

1. **Microsoft hesabıyla oturum açın** düğmesine tıklayın.

1. Microsoft hesabı veya Azure Active Directory hesabı ayrıntılarınızı girin.

1. *NuGet.org* uygulamasına verilecek izinleri kabul etmek Için lütfen **Evet** ' e tıklayın.

   ![NuGet.org için izinler verme](media/nuget-org-permissions.png)

1. *NuGet.org*'e yönlendirilirsiniz ve bir Kullanıcı adı kaydetmeniz istenir.

1. Giriş kutusunda Kullanıcı adını belirtin. Kullanıcı adının büyük/küçük harfe duyarlı olduğunu ve daha sonra değiştirilemeyeceğini veya yeniden adlandırılamayacağını lütfen unutmayın.

   ![NuGet.org üzerinde bir Kullanıcı adı belirtin](media/nuget-org-register.png) 

1. **Kaydet** düğmesine tıklayın.

Artık bir NuGet.org hesabınız var. Hesap yönetimi 'ni [Hesap ayarları](https://www.nuget.org/account) sayfasında gerçekleştirebilirsiniz.

## <a name="enable-two-factor-authentication-2fa"></a>İki öğeli kimlik doğrulamayı etkinleştirme (2FA)

Hesabınızı daha iyi korumak için iki öğeli kimlik doğrulamayı etkinleştirin (önerilir).

1. Hesabınızda oturum açarken profilinizi açın ve **oturum açma hesabı**altında **Etkinleştir** ' i seçin.

   ![2FA 'yı etkinleştir](media/nuget-org-register-2fa.png)

   *NuGet.org*' de bir sonraki oturum açışınızda sizden ek kimlik bilgileri istenmeyeceğini belirten bir ileti görürsünüz.

2. Kimlik doğrulamasını Şu anda tamamladıktan sonra oturumunuzu kapatıp yeniden oturum açın.

3. Oturum açtığınızda, ikinci bir kimlik doğrulama biçimi olarak metin veya e-posta seçin.

   Microsoft hesabı zaten ilişkilendirilmiş telefon numarasını veya e-postayı doğrulayın. Hesabınız için yeni bir telefon numarası veya e-posta girmeniz gerekebilir. Bu durumda, istenen bilgileri belirtildiği gibi girin ve **İleri**' ye tıklayın.

   ![2FA 'yı etkinleştir](media/nuget-org-sign-in-2fa.png)

4. Cihazınızı veya e-posta hesabınızı denetleyin ve az önce gönderdiğiniz kodu girin.

   ![2FA 'yı etkinleştir](media/nuget-org-enter-code-2fa.png)

5. Iki öğeli kimlik doğrulamayı tamamlamaya yönelik ek yönergeleri izleyin.

## <a name="delete-a-nugetorg-account"></a>Bir NuGet.org hesabını silme

NuGet.org hesabını silme gibi hesapla ilgili ek görevlerle ilgili yardım için bkz. [NuGet.org Account Management](nuget-org-faq.md#nugetorg-account-management).
