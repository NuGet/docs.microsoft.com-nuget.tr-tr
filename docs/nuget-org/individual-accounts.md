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
# <a name="individual-accounts-on-nugetorg"></a><span data-ttu-id="2a7d6-103">NuGet.org bireysel hesaplar</span><span class="sxs-lookup"><span data-stu-id="2a7d6-103">Individual accounts on NuGet.org</span></span>

<span data-ttu-id="2a7d6-104">Paketleri NuGet.org yayınlamak ve yönetmek için ayrı bir hesap oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a7d6-104">You must create an individual account to publish and manage packages on NuGet.org.</span></span>

## <a name="individual-accounts-vs-organization-accounts"></a><span data-ttu-id="2a7d6-105">Bireysel hesaplar ve kuruluş hesapları</span><span class="sxs-lookup"><span data-stu-id="2a7d6-105">Individual accounts vs. organization accounts</span></span>

<span data-ttu-id="2a7d6-106">Bireysel (kullanıcı) hesabınız NuGet.org'daki kimliğinizdir ve herhangi bir sayıda kuruluşun üyesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="2a7d6-106">Your individual (user) account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="2a7d6-107">Paket, tek bir hesaba ait olduğu gibi bir kuruluş hesabına ait olabilir.</span><span class="sxs-lookup"><span data-stu-id="2a7d6-107">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="2a7d6-108">Paket tüketicileri tek bir hesap la kuruluş hesabı arasında herhangi `owners`bir fark görmezler: her ikisi de paket olarak görünür.</span><span class="sxs-lookup"><span data-stu-id="2a7d6-108">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="2a7d6-109">Kuruluş hesabının üyeleri olarak bir veya daha fazla ayrı hesabı vardır.</span><span class="sxs-lookup"><span data-stu-id="2a7d6-109">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="2a7d6-110">Bu üyeler, sahiplik için tek bir kimlik korurken bir dizi paketi yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="2a7d6-110">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="add-a-new-individual-account"></a><span data-ttu-id="2a7d6-111">Yeni bir bireysel hesap ekleme</span><span class="sxs-lookup"><span data-stu-id="2a7d6-111">Add a new individual account</span></span>

<span data-ttu-id="2a7d6-112">NuGet.org bir hesap oluşturmak için kişisel bir Microsoft hesabınız (MSA) veya Azure Etkin Dizin (AAD) hesabınız olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a7d6-112">To create a NuGet.org account, you need to have a personal Microsoft account (MSA) or an Azure Active Directory (AAD) account.</span></span> <span data-ttu-id="2a7d6-113">Eğer yoksa, bir [oluşturabilirsiniz.](https://signup.live.com)</span><span class="sxs-lookup"><span data-stu-id="2a7d6-113">If you do not have one, you can [create](https://signup.live.com) one.</span></span> <span data-ttu-id="2a7d6-114">MSA veya AAD hesabınız varsa aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="2a7d6-114">Follow the following steps if you have an MSA or AAD account.</span></span>

1. <span data-ttu-id="2a7d6-115">[giriş NuGet.org sayfasına](https://www.nuget.org/users/account/LogOn)gidin.</span><span class="sxs-lookup"><span data-stu-id="2a7d6-115">Go to the [NuGet.org login page](https://www.nuget.org/users/account/LogOn).</span></span>

1. <span data-ttu-id="2a7d6-116">Microsoft **ile Oturum Aç** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2a7d6-116">Click on **Sign in with Microsoft** button.</span></span>

1. <span data-ttu-id="2a7d6-117">Microsoft hesabınızı veya Azure Active Directory hesap bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="2a7d6-117">Enter your Microsoft account or Azure Active Directory account details.</span></span>

1. <span data-ttu-id="2a7d6-118">*NuGet.org* başvurusuna verilecek izinleri kabul etmek için lütfen **Evet'i** tıklatın.</span><span class="sxs-lookup"><span data-stu-id="2a7d6-118">Please click **Yes** to accept the permissions to be given to the *NuGet.org* application.</span></span>

   ![NuGet.org izin verme](media/nuget-org-permissions.png)

1. <span data-ttu-id="2a7d6-120">*nuget.org*yönlendirilirsiniz ve bir kullanıcı adı kaydetmeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="2a7d6-120">You will be redirected to *nuget.org*, and asked to register a username.</span></span>

1. <span data-ttu-id="2a7d6-121">Giriş kutusundaki kullanıcı adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="2a7d6-121">Specify the username in the input box.</span></span> <span data-ttu-id="2a7d6-122">Kullanıcı adının büyük/küçük harf **duyarlı olduğunu** ve daha sonra değiştirilemeyeceğini veya değiştirilemeyeceğini lütfen unutmayın.</span><span class="sxs-lookup"><span data-stu-id="2a7d6-122">Please note that the username **is** case sensitive and cannot be changed or renamed later.</span></span>

   ![NuGet.org bir kullanıcı adı belirtin](media/nuget-org-register.png) 

1. <span data-ttu-id="2a7d6-124">**Kaydol** düğmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="2a7d6-124">Click the **Register** button.</span></span>

<span data-ttu-id="2a7d6-125">Artık NuGet.org bir hesabınız var.</span><span class="sxs-lookup"><span data-stu-id="2a7d6-125">You now have a NuGet.org account.</span></span> <span data-ttu-id="2a7d6-126">[Hesap ayarları](https://www.nuget.org/account) sayfasında hesap yönetimi gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a7d6-126">You can perform account management on the [account settings](https://www.nuget.org/account) page.</span></span>

## <a name="enable-two-factor-authentication-2fa"></a><span data-ttu-id="2a7d6-127">İki faktörlü kimlik doğrulamayı etkinleştirme (2FA)</span><span class="sxs-lookup"><span data-stu-id="2a7d6-127">Enable two-factor authentication (2FA)</span></span>

<span data-ttu-id="2a7d6-128">İki faktörlü kimlik doğrulama veya 2FA, web sitelerine veya uygulamalara giriş yaparken kullanılan ek bir güvenlik katmanıdır.</span><span class="sxs-lookup"><span data-stu-id="2a7d6-128">Two-factor authentication, or 2FA, is an extra layer of security used when logging into websites or apps.</span></span> <span data-ttu-id="2a7d6-129">2FA ile Microsoft Hesabınızla (MSA) oturum açmanız ve yalnızca sizin bildiğiniz veya erişebildiğiniz başka bir kimlik doğrulama biçimi sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2a7d6-129">With 2FA, you have to log in with your Microsoft Account (MSA) and provide another form of authentication that only you know or have access to.</span></span> <span data-ttu-id="2a7d6-130">Hesabınızı daha iyi korumak için iki faktörlü kimlik doğrulamayı (önerilir) etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="2a7d6-130">To better protect your account, enable two-factor authentication (recommended).</span></span>

1. <span data-ttu-id="2a7d6-131">Hesabınıza giriş yaptığınızda, profilinizi açın ve **Giriş Hesabı**altında **Etkinleştir'i** seçin.</span><span class="sxs-lookup"><span data-stu-id="2a7d6-131">When logged into your account, open your profile and choose **Enable** under **Login Account**.</span></span>

   ![2FA'yı etkinleştir](media/nuget-org-register-2fa.png)

   <span data-ttu-id="2a7d6-133">*nuget.org'da*bir sonraki oturum açtığınızda ek kimlik bilgilerinin isteneceğini belirten bir ileti görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="2a7d6-133">You will see a message that tells you that the next time you sign in to *nuget.org*, you will be asked for additional credentials.</span></span>

2. <span data-ttu-id="2a7d6-134">Kimlik doğrulamasını şu anda tamamlamak için oturumaçın ve sonra yeniden oturum açın.</span><span class="sxs-lookup"><span data-stu-id="2a7d6-134">To complete the authentication at this time, sign out and then sign in again.</span></span>

3. <span data-ttu-id="2a7d6-135">Oturum açken, ikinci bir kimlik doğrulama biçimi olarak metin veya e-posta yı seçin.</span><span class="sxs-lookup"><span data-stu-id="2a7d6-135">When you sign in, choose either text or e-mail as a second form of authentication.</span></span>

   <span data-ttu-id="2a7d6-136">Microsoft hesabınızla zaten ilişkili olan telefon numarasını veya e-postayı doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="2a7d6-136">Verify the phone number or e-mail that is already associated with your Microsoft account.</span></span> <span data-ttu-id="2a7d6-137">Hesabınız için yeni bir telefon numarası veya e-posta girmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="2a7d6-137">You may need to enter a new phone number or e-mail for your account.</span></span> <span data-ttu-id="2a7d6-138">Bu durumda, gerekli bilgileri talimat olarak girin ve **İleri'yi**tıklatın.</span><span class="sxs-lookup"><span data-stu-id="2a7d6-138">If so, enter the required information as instructed, and click **Next**.</span></span>

   ![2FA'yı etkinleştir](media/nuget-org-sign-in-2fa.png)

4. <span data-ttu-id="2a7d6-140">Cihazınızı veya e-posta hesabınızı kontrol edin ve size gönderilen kodu girin.</span><span class="sxs-lookup"><span data-stu-id="2a7d6-140">Check your device or e-mail account, and enter the code that you were just sent.</span></span>

   ![2FA'yı etkinleştir](media/nuget-org-enter-code-2fa.png)

5. <span data-ttu-id="2a7d6-142">İki faktörlü kimlik doğrulamasını tamamlamak için ek yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="2a7d6-142">Follow any additional instructions to complete Two-factor authentication.</span></span>

> [!Tip]
> <span data-ttu-id="2a7d6-143">NuGet.org hesabınız için 2FA'yı etkinleştirmek, NuGet.org oturum açmak için kullandığınız Microsoft hesabıyla bağlantılı olabilecek diğer hesaplar veya hizmetler için kimlik doğrulama ayarlarını etkilemez.</span><span class="sxs-lookup"><span data-stu-id="2a7d6-143">Enabling 2FA for your NuGet.org account does not impact authentication settings for other accounts or services that may be linked to the Microsoft account you use to login to NuGet.org.</span></span>

## <a name="delete-a-nugetorg-account"></a><span data-ttu-id="2a7d6-144">NuGet.org hesabı nı silme</span><span class="sxs-lookup"><span data-stu-id="2a7d6-144">Delete a NuGet.org account</span></span>

<span data-ttu-id="2a7d6-145">NuGet.org hesabını silme gibi hesapla ilgili ek görevlerle ilgili yardım için NuGet.org [hesap yönetimine](nuget-org-faq.md#nugetorg-account-management)bakın.</span><span class="sxs-lookup"><span data-stu-id="2a7d6-145">For help with additional account-related tasks, such as deleting a NuGet.org account, see [NuGet.org account management](nuget-org-faq.md#nugetorg-account-management).</span></span>
