---
title: Kullanıcı veri istekleri
description: Kullanıcı verileri isteyen ilkeleri dışarı aktarma ve silin
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: 595a47da59c9b2672a10fc0f19e528c36a790134
ms.sourcegitcommit: 68c8a494a11c892ac671fec3170ba7be97fb044d
ms.contentlocale: tr-TR
ms.lasthandoff: 05/04/2018
---
# <a name="user-data-requests"></a><span data-ttu-id="a42da-103">Kullanıcı veri istekleri</span><span class="sxs-lookup"><span data-stu-id="a42da-103">User Data Requests</span></span>

<span data-ttu-id="a42da-104">nuget.org kullanıcılar bilgi delete isteklerini ve yanıtlarını bilgileri verme aracılığıyla gönderebilir [nuget.org](https://www.nuget.org). Her iki tür destek biçiminde gönderilen istekleri ve bu yürütülebilir nuget.org yöneticiler tarafından 30 gün içinde.</span><span class="sxs-lookup"><span data-stu-id="a42da-104">nuget.org users can submit information delete requests and information export requests through [nuget.org](https://www.nuget.org). Both types are submitted in the form of support requests and are be executed by the nuget.org administrators within 30 days.</span></span>

<span data-ttu-id="a42da-105">Aşağıdaki kullanıcı verilerini nuget.org doğrudan erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="a42da-105">The following user data is directly accessible through nuget.org:</span></span>

* <span data-ttu-id="a42da-106">E-posta adresi, oturum açma hesabı, profil resmi ve e-posta bildirim ayarları gibi veri hesabıyla ilgili</span><span class="sxs-lookup"><span data-stu-id="a42da-106">Account related data such as email address, login account, profile picture, and email notification settings</span></span>
* <span data-ttu-id="a42da-107">Ait API anahtarları</span><span class="sxs-lookup"><span data-stu-id="a42da-107">Owned API Keys</span></span>
* <span data-ttu-id="a42da-108">Sahibi olan paketlerin listesini</span><span class="sxs-lookup"><span data-stu-id="a42da-108">List of owned packages</span></span>

<span data-ttu-id="a42da-109">Bu verileri destek isteği verilen verileri bulunmamaktadır.</span><span class="sxs-lookup"><span data-stu-id="a42da-109">This data is not included in data exported through the support request.</span></span>

## <a name="identifying-customer-data"></a><span data-ttu-id="a42da-110">Müşteri verileri tanımlama</span><span class="sxs-lookup"><span data-stu-id="a42da-110">Identifying customer data</span></span>

<span data-ttu-id="a42da-111">Müşteri verileri nuget.org kullanıcı hesabı adları tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="a42da-111">Customer data can be identified as nuget.org user account names.</span></span>

## <a name="deleting-customer-data"></a><span data-ttu-id="a42da-112">Müşteri verileri silme</span><span class="sxs-lookup"><span data-stu-id="a42da-112">Deleting customer data</span></span>

<span data-ttu-id="a42da-113">Nuget.org silme kullanıcı verilerini istemek için:</span><span class="sxs-lookup"><span data-stu-id="a42da-113">To request deleting user data from nuget.org:</span></span>

1. <span data-ttu-id="a42da-114">Kullanıcı oturumu için açma gerekir [nuget.org](https://www.nuget.org)</span><span class="sxs-lookup"><span data-stu-id="a42da-114">The user must sign-in to [nuget.org](https://www.nuget.org)</span></span>
1. <span data-ttu-id="a42da-115">Kullanıcı hesaplarında silinmesi için bir istek göndermelisiniz [nuget.org/account/delete](https://www.nuget.org/account/delete)</span><span class="sxs-lookup"><span data-stu-id="a42da-115">The user must submit a request for their account to be deleted [nuget.org/account/delete](https://www.nuget.org/account/delete)</span></span>

<span data-ttu-id="a42da-116">Paketleri tek sahipleri olan kullanıcılar, silinen kendi hesabınız için onay isteyen önce yeni sahipleri bulmak için önerilir.</span><span class="sxs-lookup"><span data-stu-id="a42da-116">Users that are sole owners of packages are encouraged to find new owners before asking to have their account deleted.</span></span> <span data-ttu-id="a42da-117">Paket sahipliği aktarılmayan ise NuGet paketi listelenmemiş olur ve sonuç olarak, artık Visual Studio veya nuget.org Web sitesinde arama sorgularında kullanılabilir değildir.</span><span class="sxs-lookup"><span data-stu-id="a42da-117">If package ownership is not transferred, the NuGet package is unlisted and, as a result, it is no longer available in search queries in Visual Studio or on the nuget.org website.</span></span> <span data-ttu-id="a42da-118">Hesabı silmeden önce oldukları paketleri yeni sahipleri bulmak için kullanıcıyla nuget.org Yöneticiler çalışır.</span><span class="sxs-lookup"><span data-stu-id="a42da-118">Before deleting the account, the nuget.org administrators work with the user to find new owners for the packages they own.</span></span>

<span data-ttu-id="a42da-119">Hesap silme eylemi nuget.org yönetici tarafından istek tarihten itibaren 30 gün içinde tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="a42da-119">The account delete action is completed by the nuget.org administrator within 30 days from the date of the request.</span></span>

<span data-ttu-id="a42da-120">Hesap silme, üzerine kullanıcının verilerin tümü olduğu kaldırılması nuget.org sistemden ve şu işlemler uygulanır:</span><span class="sxs-lookup"><span data-stu-id="a42da-120">Upon account deletion, all of the user's data is be removed from the nuget.org system and the following actions are taken:</span></span>

* <span data-ttu-id="a42da-121">Silinen hesap ile nuget.org kaydı olur</span><span class="sxs-lookup"><span data-stu-id="a42da-121">The deleted account becomes unregistered with nuget.org</span></span>
* <span data-ttu-id="a42da-122">Tüm API anahtarları silinmiş ait</span><span class="sxs-lookup"><span data-stu-id="a42da-122">All owned API Keys are deleted</span></span>
* <span data-ttu-id="a42da-123">Tüm ayrılmış ad alanlarından yayımlanan</span><span class="sxs-lookup"><span data-stu-id="a42da-123">All reserved namespaces are released</span></span>
* <span data-ttu-id="a42da-124">Tüm paket sahipliği kaldırılır</span><span class="sxs-lookup"><span data-stu-id="a42da-124">Any package ownership are removed</span></span>

<span data-ttu-id="a42da-125">Ait paketleri *değil* silindi.</span><span class="sxs-lookup"><span data-stu-id="a42da-125">The owned packages are *not* deleted.</span></span> <span data-ttu-id="a42da-126">Listede bulunmayan Arama sonuçlarından rağmen bunlara bağımlı projeleri için paket geri yüklemesi aracılığıyla kullanılabilen kalırlar.</span><span class="sxs-lookup"><span data-stu-id="a42da-126">Though unlisted from search results, they remain available through package restore to projects that depend on them.</span></span>

## <a name="exporting-customer-data"></a><span data-ttu-id="a42da-127">Müşteri verileri dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="a42da-127">Exporting customer data</span></span>

<span data-ttu-id="a42da-128">Oturum açma işleminden sonra nuget.org için bir kullanıcı bir dışarı aktarma isteği aracılığıyla gönderebilirsiniz [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)</span><span class="sxs-lookup"><span data-stu-id="a42da-128">After sign-in to nuget.org, a user can submit an export request through [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)</span></span>

<span data-ttu-id="a42da-129">Verilen verileri 48 saat için bir Azure Blob üzerinden yükleme için kullanıcıya kullanılabilir hale getirilir.</span><span class="sxs-lookup"><span data-stu-id="a42da-129">The data exported is made available for 48 hours to the user for download through an Azure Blob.</span></span> <span data-ttu-id="a42da-130">48 saat sonra erişim süresi ve kullanıcı, gerektiğinde yeni bir dışarı aktarma isteği göndermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a42da-130">After 48 hours, access expires and the user must submit a new export request as needed.</span></span>

<span data-ttu-id="a42da-131">Dışarı aktarılan verileri şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="a42da-131">The exported data includes:</span></span>

* <span data-ttu-id="a42da-132">Kullanıcının destek istekleri</span><span class="sxs-lookup"><span data-stu-id="a42da-132">The user's support requests</span></span>
* <span data-ttu-id="a42da-133">Kullanıcının Eylemler (paket yayımlama, hesabı oluşturun) denetim günlüklerini kalıcı olarak</span><span class="sxs-lookup"><span data-stu-id="a42da-133">The user's actions (publish package, create account) as persisted in the audit logs</span></span>
* <span data-ttu-id="a42da-134">IIS günlüklerine kalıcı olarak herhangi bir kullanıcı bilgisi</span><span class="sxs-lookup"><span data-stu-id="a42da-134">Any user information as persisted in the IIS logs</span></span>
