---
title: Bireysel hesaplar-NuGet.org
description: Paketleri yayımlamak için NuGet.org üzerindeki ayrı hesaplar gereklidir
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 7951b3db0cdcaee0a1eb955a5bf6fedce24c79c9
ms.sourcegitcommit: fc0f8c950829ee5c96e3f3f32184bc727714cfdb
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/20/2019
ms.locfileid: "74253948"
---
# <a name="individual-accounts-on-nugetorg"></a><span data-ttu-id="902e7-103">NuGet.org üzerinde ayrı hesaplar</span><span class="sxs-lookup"><span data-stu-id="902e7-103">Individual accounts on NuGet.org</span></span>

<span data-ttu-id="902e7-104">NuGet.org 'de paketleri yayımlamak ve yönetmek için tek bir hesap oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="902e7-104">You must create an individual account to publish and manage packages on NuGet.org.</span></span>

## <a name="individual-accounts-vs-organization-accounts"></a><span data-ttu-id="902e7-105">Bireysel hesaplar ve kuruluş hesapları</span><span class="sxs-lookup"><span data-stu-id="902e7-105">Individual accounts vs. organization accounts</span></span>

<span data-ttu-id="902e7-106">Bireysel (Kullanıcı) hesabınız NuGet.org üzerinde kimliğiniz ve herhangi bir sayıda kuruluşun üyesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="902e7-106">Your individual (user) account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="902e7-107">Bir paket, tek bir hesaba ait olabilir gibi bir kuruluş hesabına ait olabilir.</span><span class="sxs-lookup"><span data-stu-id="902e7-107">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="902e7-108">Paket tüketicileri, tek bir hesap veya kuruluş hesabı arasında herhangi bir farklılık görmez: her ikisi de paket `owners`olarak görünürler.</span><span class="sxs-lookup"><span data-stu-id="902e7-108">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="902e7-109">Bir kuruluş hesabının üyeleri olarak bir veya daha fazla bireysel hesabı vardır.</span><span class="sxs-lookup"><span data-stu-id="902e7-109">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="902e7-110">Bu Üyeler, sahiplik için tek bir kimlik sağlarken bir paket kümesini yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="902e7-110">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="add-a-new-individual-account"></a><span data-ttu-id="902e7-111">Yeni bir bireysel hesap ekleyin</span><span class="sxs-lookup"><span data-stu-id="902e7-111">Add a new individual account</span></span>

<span data-ttu-id="902e7-112">Bir NuGet.org hesabı oluşturmak için bir kişisel Microsoft hesabı (MSA) veya bir Azure Active Directory (AAD) hesabınız olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="902e7-112">To create a NuGet.org account, you need to have a personal Microsoft account (MSA) or an Azure Active Directory (AAD) account.</span></span> <span data-ttu-id="902e7-113">Bir tane yoksa, bir tane [oluşturabilirsiniz](https://signup.live.com) .</span><span class="sxs-lookup"><span data-stu-id="902e7-113">If you do not have one, you can [create](https://signup.live.com) one.</span></span> <span data-ttu-id="902e7-114">MSA veya AAD hesabınız varsa aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="902e7-114">Follow the following steps if you have an MSA or AAD account.</span></span>

1. <span data-ttu-id="902e7-115">[NuGet.org oturum açma sayfasına](https://www.nuget.org/users/account/LogOn)gidin.</span><span class="sxs-lookup"><span data-stu-id="902e7-115">Go to the [NuGet.org login page](https://www.nuget.org/users/account/LogOn).</span></span>

1. <span data-ttu-id="902e7-116">**Microsoft hesabıyla oturum açın** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="902e7-116">Click on **Sign in with Microsoft** button.</span></span>

1. <span data-ttu-id="902e7-117">Microsoft hesabı veya Azure Active Directory hesabı ayrıntılarınızı girin.</span><span class="sxs-lookup"><span data-stu-id="902e7-117">Enter your Microsoft account or Azure Active Directory account details.</span></span>

1. <span data-ttu-id="902e7-118">*NuGet.org* uygulamasına verilecek izinleri kabul etmek Için lütfen **Evet** ' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="902e7-118">Please click **Yes** to accept the permissions to be given to the *NuGet.org* application.</span></span>

   ![NuGet.org için izinler verme](media/nuget-org-permissions.png)

1. <span data-ttu-id="902e7-120">*NuGet.org*'e yönlendirilirsiniz ve bir Kullanıcı adı kaydetmeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="902e7-120">You will be redirected to *nuget.org*, and asked to register a username.</span></span>

1. <span data-ttu-id="902e7-121">Giriş kutusunda Kullanıcı adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="902e7-121">Specify the username in the input box.</span></span> <span data-ttu-id="902e7-122">Kullanıcı adının büyük/küçük harfe **duyarlı olduğunu ve** daha sonra değiştirilemeyeceğini veya yeniden adlandırılamayacağını lütfen unutmayın.</span><span class="sxs-lookup"><span data-stu-id="902e7-122">Please note that the username **is** case sensitive and cannot be changed or renamed later.</span></span>

   ![NuGet.org üzerinde bir Kullanıcı adı belirtin](media/nuget-org-register.png) 

1. <span data-ttu-id="902e7-124">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="902e7-124">Click the **Register** button.</span></span>

<span data-ttu-id="902e7-125">Artık bir NuGet.org hesabınız var.</span><span class="sxs-lookup"><span data-stu-id="902e7-125">You now have a NuGet.org account.</span></span> <span data-ttu-id="902e7-126">Hesap yönetimi 'ni [Hesap ayarları](https://www.nuget.org/account) sayfasında gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="902e7-126">You can perform account management on the [account settings](https://www.nuget.org/account) page.</span></span>

## <a name="enable-two-factor-authentication-2fa"></a><span data-ttu-id="902e7-127">İki öğeli kimlik doğrulamayı etkinleştirme (2FA)</span><span class="sxs-lookup"><span data-stu-id="902e7-127">Enable two-factor authentication (2FA)</span></span>

<span data-ttu-id="902e7-128">İki öğeli kimlik doğrulama veya 2FA, Web siteleri veya uygulamalar üzerinde oturum açarken kullanılan ek bir güvenlik katmanıdır.</span><span class="sxs-lookup"><span data-stu-id="902e7-128">Two-factor authentication, or 2FA, is an extra layer of security used when logging into websites or apps.</span></span> <span data-ttu-id="902e7-129">2FA sayesinde, Microsoft hesabınızla (MSA) oturum açmanız ve yalnızca bildiğiniz veya erişiminiz olan başka bir kimlik doğrulama biçimi sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="902e7-129">With 2FA, you have to log in with your Microsoft Account (MSA) and provide another form of authentication that only you know or have access to.</span></span> <span data-ttu-id="902e7-130">Hesabınızı daha iyi korumak için iki öğeli kimlik doğrulamayı etkinleştirin (önerilir).</span><span class="sxs-lookup"><span data-stu-id="902e7-130">To better protect your account, enable two-factor authentication (recommended).</span></span>

1. <span data-ttu-id="902e7-131">Hesabınızda oturum açarken profilinizi açın ve **oturum açma hesabı**altında **Etkinleştir** ' i seçin.</span><span class="sxs-lookup"><span data-stu-id="902e7-131">When logged into your account, open your profile and choose **Enable** under **Login Account**.</span></span>

   ![2FA 'yı etkinleştir](media/nuget-org-register-2fa.png)

   <span data-ttu-id="902e7-133">*NuGet.org*' de bir sonraki oturum açışınızda sizden ek kimlik bilgileri istenmeyeceğini belirten bir ileti görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="902e7-133">You will see a message that tells you that the next time you sign in to *nuget.org*, you will be asked for additional credentials.</span></span>

2. <span data-ttu-id="902e7-134">Kimlik doğrulamasını Şu anda tamamladıktan sonra oturumunuzu kapatıp yeniden oturum açın.</span><span class="sxs-lookup"><span data-stu-id="902e7-134">To complete the authentication at this time, sign out and then sign in again.</span></span>

3. <span data-ttu-id="902e7-135">Oturum açtığınızda, ikinci bir kimlik doğrulama biçimi olarak metin veya e-posta seçin.</span><span class="sxs-lookup"><span data-stu-id="902e7-135">When you sign in, choose either text or e-mail as a second form of authentication.</span></span>

   <span data-ttu-id="902e7-136">Microsoft hesabı zaten ilişkilendirilmiş telefon numarasını veya e-postayı doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="902e7-136">Verify the phone number or e-mail that is already associated with your Microsoft account.</span></span> <span data-ttu-id="902e7-137">Hesabınız için yeni bir telefon numarası veya e-posta girmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="902e7-137">You may need to enter a new phone number or e-mail for your account.</span></span> <span data-ttu-id="902e7-138">Bu durumda, istenen bilgileri belirtildiği gibi girin ve **İleri**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="902e7-138">If so, enter the required information as instructed, and click **Next**.</span></span>

   ![2FA 'yı etkinleştir](media/nuget-org-sign-in-2fa.png)

4. <span data-ttu-id="902e7-140">Cihazınızı veya e-posta hesabınızı denetleyin ve az önce gönderdiğiniz kodu girin.</span><span class="sxs-lookup"><span data-stu-id="902e7-140">Check your device or e-mail account, and enter the code that you were just sent.</span></span>

   ![2FA 'yı etkinleştir](media/nuget-org-enter-code-2fa.png)

5. <span data-ttu-id="902e7-142">Iki öğeli kimlik doğrulamayı tamamlamaya yönelik ek yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="902e7-142">Follow any additional instructions to complete Two-factor authentication.</span></span>

> [!Tip]
> <span data-ttu-id="902e7-143">NuGet.org hesabınız için 2FA 'yı etkinleştirmek, NuGet.org 'de oturum açmak için kullandığınız Microsoft hesabı bağlantılı olabilecek diğer hesaplar veya hizmetler için kimlik doğrulama ayarlarını etkilemez.</span><span class="sxs-lookup"><span data-stu-id="902e7-143">Enabling 2FA for your NuGet.org account does not impact authentication settings for other accounts or services that may be linked to the Microsoft account you use to login to NuGet.org.</span></span>

## <a name="delete-a-nugetorg-account"></a><span data-ttu-id="902e7-144">Bir NuGet.org hesabını silme</span><span class="sxs-lookup"><span data-stu-id="902e7-144">Delete a NuGet.org account</span></span>

<span data-ttu-id="902e7-145">NuGet.org hesabını silme gibi hesapla ilgili ek görevlerle ilgili yardım için bkz. [NuGet.org Account Management](nuget-org-faq.md#nugetorg-account-management).</span><span class="sxs-lookup"><span data-stu-id="902e7-145">For help with additional account-related tasks, such as deleting a NuGet.org account, see [NuGet.org account management](nuget-org-faq.md#nugetorg-account-management).</span></span>
