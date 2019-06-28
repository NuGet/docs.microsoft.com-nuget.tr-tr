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
# <a name="individual-accounts"></a><span data-ttu-id="1cc44-103">Bireysel hesaplar</span><span class="sxs-lookup"><span data-stu-id="1cc44-103">Individual accounts</span></span>

<span data-ttu-id="1cc44-104">Paketleri NuGet.org üzerinde yönetmek ve yayımlamak için ayrı bir hesap oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1cc44-104">You must create an individual account to publish and manage packages on NuGet.org.</span></span>

## <a name="individual-accounts-vs-organization-accounts"></a><span data-ttu-id="1cc44-105">Kuruluş hesapları ve bireysel hesaplar</span><span class="sxs-lookup"><span data-stu-id="1cc44-105">Individual accounts vs. organization accounts</span></span>

<span data-ttu-id="1cc44-106">(Kullanıcı) bireysel hesabınızın kimliğinizi nuget.org ve kuruluşların herhangi bir sayıda üyesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="1cc44-106">Your individual (user) account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="1cc44-107">Bir paketi tek bir hesaba ait olabilir gibi bir kuruluş hesabına ait olabilir.</span><span class="sxs-lookup"><span data-stu-id="1cc44-107">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="1cc44-108">Paketi tüketicileri bir bireysel hesabı veya kuruluş hesabı arasındaki fark görmüyorum: her ikisi de paketi olarak görünen `owners`.</span><span class="sxs-lookup"><span data-stu-id="1cc44-108">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="1cc44-109">Bir kuruluş hesabı, bir veya daha fazla bireysel hesaplar, üyelere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="1cc44-109">An organization account has one or more individual accounts as its members.</span></span> <span data-ttu-id="1cc44-110">Bu üyeleri, sahipliği için tek bir kimlik korurken bir dizi paketleri yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1cc44-110">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="add-a-new-individual-account"></a><span data-ttu-id="1cc44-111">Yeni tek bir Hesap Ekle</span><span class="sxs-lookup"><span data-stu-id="1cc44-111">Add a new individual account</span></span>

<span data-ttu-id="1cc44-112">NuGet.org hesabı oluşturmak için kişisel bir Microsoft hesabı (MSA) veya bir Azure Active Directory (AAD) hesabı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1cc44-112">To create a NuGet.org account, you need to have a personal Microsoft account (MSA) or an Azure Active Directory (AAD) account.</span></span> <span data-ttu-id="1cc44-113">Biri yoksa yapabilecekleriniz [oluşturma](https://signup.live.com) biri.</span><span class="sxs-lookup"><span data-stu-id="1cc44-113">If you do not have one, you can [create](https://signup.live.com) one.</span></span> <span data-ttu-id="1cc44-114">MSA veya AAD hesabınız varsa, aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="1cc44-114">Follow the following steps if you have an MSA or AAD account.</span></span>

1. <span data-ttu-id="1cc44-115">Git [NuGet.org oturum açma sayfasına](https://www.nuget.org/users/account/LogOn).</span><span class="sxs-lookup"><span data-stu-id="1cc44-115">Go to the [NuGet.org login page](https://www.nuget.org/users/account/LogOn).</span></span>

1. <span data-ttu-id="1cc44-116">Tıklayarak **Microsoft'ta oturum açma** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1cc44-116">Click on **Sign in with Microsoft** button.</span></span>

1. <span data-ttu-id="1cc44-117">Microsoft hesabınızı veya Azure Active Directory hesabı ayrıntılarını girin.</span><span class="sxs-lookup"><span data-stu-id="1cc44-117">Enter your Microsoft account or Azure Active Directory account details.</span></span>

1. <span data-ttu-id="1cc44-118">Lütfen tıklayın **Evet** için verilecek izinlerini kabul etmenizi *NuGet.org* uygulama.</span><span class="sxs-lookup"><span data-stu-id="1cc44-118">Please click **Yes** to accept the permissions to be given to the *NuGet.org* application.</span></span>

   ![NuGet.org için izinleri verme](media/nuget-org-permissions.png)

1. <span data-ttu-id="1cc44-120">İçin yönlendirilirsiniz *nuget.org*ve bir kullanıcı adı kayıt istenir.</span><span class="sxs-lookup"><span data-stu-id="1cc44-120">You will be redirected to *nuget.org*, and asked to register a username.</span></span>

1. <span data-ttu-id="1cc44-121">Giriş kutusuna kullanıcı adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="1cc44-121">Specify the username in the input box.</span></span> <span data-ttu-id="1cc44-122">Lütfen unutmayın kullanıcıadı **olduğu** hassas durumda ve değiştirilemez ya da daha sonra yeniden adlandırıldı.</span><span class="sxs-lookup"><span data-stu-id="1cc44-122">Please note that the username **is** case sensitive and cannot be changed or renamed later.</span></span>

   ![NuGet.org bir kullanıcı adı belirtin](media/nuget-org-register.png) 

1. <span data-ttu-id="1cc44-124">Tıklayın **kaydetme** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1cc44-124">Click the **Register** button.</span></span>

<span data-ttu-id="1cc44-125">Artık bir NuGet.org hesabı var.</span><span class="sxs-lookup"><span data-stu-id="1cc44-125">You now have a NuGet.org account.</span></span> <span data-ttu-id="1cc44-126">Hesap Yönetimi gerçekleştirebileceğiniz [hesap ayarları](https://www.nuget.org/account) sayfası.</span><span class="sxs-lookup"><span data-stu-id="1cc44-126">You can perform account management on the [account settings](https://www.nuget.org/account) page.</span></span>
