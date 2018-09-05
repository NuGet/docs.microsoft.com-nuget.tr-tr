---
title: Kullanıcı veri isteği sayısı
description: Kullanıcı verileri istemeye ilişkin ilkeler dışarı aktarma ve silme
author: karann-msft
ms.author: karann
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: ef054f741755bccf56eedfd462915b8e9fd6931a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548060"
---
# <a name="user-data-requests"></a><span data-ttu-id="e826d-103">Kullanıcı veri isteği sayısı</span><span class="sxs-lookup"><span data-stu-id="e826d-103">User Data Requests</span></span>

<span data-ttu-id="e826d-104">nuget.org kullanıcılar bilgi delete isteklerini ve bilgi dışarı aktarma isteklerini gönderebildiği [nuget.org](https://www.nuget.org). Her iki türü de destek biçiminde gönderilen istekleri ve bu yürütülebilir nuget.org yöneticileri tarafından 30 gün içinde.</span><span class="sxs-lookup"><span data-stu-id="e826d-104">nuget.org users can submit information delete requests and information export requests through [nuget.org](https://www.nuget.org). Both types are submitted in the form of support requests and are be executed by the nuget.org administrators within 30 days.</span></span>

<span data-ttu-id="e826d-105">Aşağıdaki kullanıcı verilerini doğrudan nuget.org erişilebilir:</span><span class="sxs-lookup"><span data-stu-id="e826d-105">The following user data is directly accessible through nuget.org:</span></span>

* <span data-ttu-id="e826d-106">E-posta adresi, oturum açma hesabı, profil resminizi ve e-posta bildirimi ayarları gibi veri hesabıyla ilgili</span><span class="sxs-lookup"><span data-stu-id="e826d-106">Account related data such as email address, login account, profile picture, and email notification settings</span></span>
* <span data-ttu-id="e826d-107">Sahip olunan API anahtarları</span><span class="sxs-lookup"><span data-stu-id="e826d-107">Owned API Keys</span></span>
* <span data-ttu-id="e826d-108">Sahip olunan paketlerin listesi</span><span class="sxs-lookup"><span data-stu-id="e826d-108">List of owned packages</span></span>

<span data-ttu-id="e826d-109">Bu veriler üzerinden destek isteği dışarı aktarılan verileri bulunmamaktadır.</span><span class="sxs-lookup"><span data-stu-id="e826d-109">This data is not included in data exported through the support request.</span></span>

## <a name="identifying-customer-data"></a><span data-ttu-id="e826d-110">Müşteri verileri tanımlama</span><span class="sxs-lookup"><span data-stu-id="e826d-110">Identifying customer data</span></span>

<span data-ttu-id="e826d-111">Müşteri verilerini nuget.org kullanıcı hesabı adları tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="e826d-111">Customer data can be identified as nuget.org user account names.</span></span>

## <a name="deleting-customer-data"></a><span data-ttu-id="e826d-112">Müşteri verileri silme</span><span class="sxs-lookup"><span data-stu-id="e826d-112">Deleting customer data</span></span>

<span data-ttu-id="e826d-113">Nuget.org adresinden kullanıcı verilerini silme isteği için:</span><span class="sxs-lookup"><span data-stu-id="e826d-113">To request deleting user data from nuget.org:</span></span>

1. <span data-ttu-id="e826d-114">Kullanıcı için oturum gerekir [nuget.org](https://www.nuget.org)</span><span class="sxs-lookup"><span data-stu-id="e826d-114">The user must sign-in to [nuget.org](https://www.nuget.org)</span></span>
1. <span data-ttu-id="e826d-115">Kullanıcı hesabı silinecek bir istek göndermeniz gerekir [nuget.org/account/delete](https://www.nuget.org/account/delete)</span><span class="sxs-lookup"><span data-stu-id="e826d-115">The user must submit a request for their account to be deleted [nuget.org/account/delete](https://www.nuget.org/account/delete)</span></span>

<span data-ttu-id="e826d-116">Paketleri tek sahipleri olan kullanıcı hesabı silindi olmasını isteyen önce yeni sahipleri bulun önerilir.</span><span class="sxs-lookup"><span data-stu-id="e826d-116">Users that are sole owners of packages are encouraged to find new owners before asking to have their account deleted.</span></span> <span data-ttu-id="e826d-117">Paket Sahiplik devredildikten değil, NuGet paketi listelenmemiş ve sonuç olarak, artık Visual Studio'da veya nuget.org Web sitesinde arama sorgularında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e826d-117">If package ownership is not transferred, the NuGet package is unlisted and, as a result, it is no longer available in search queries in Visual Studio or on the nuget.org website.</span></span> <span data-ttu-id="e826d-118">Hesabı silmeden önce nuget.org Yöneticiler kullanıcı oldukları paketleri yeni sahipleri bulun çalışın.</span><span class="sxs-lookup"><span data-stu-id="e826d-118">Before deleting the account, the nuget.org administrators work with the user to find new owners for the packages they own.</span></span>

<span data-ttu-id="e826d-119">Hesap silme eylemi nuget.org yönetici tarafından istek tarihten itibaren 30 gün içinde tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="e826d-119">The account delete action is completed by the nuget.org administrator within 30 days from the date of the request.</span></span>

<span data-ttu-id="e826d-120">Temel hesabını silme işlemi, tüm kullanıcı verilerini olması kaldırıldı nuget.org sistemden ve şu işlemler uygulanır:</span><span class="sxs-lookup"><span data-stu-id="e826d-120">Upon account deletion, all of the user's data is be removed from the nuget.org system and the following actions are taken:</span></span>

* <span data-ttu-id="e826d-121">Silinmiş hesap ile nuget.org kaydı olur</span><span class="sxs-lookup"><span data-stu-id="e826d-121">The deleted account becomes unregistered with nuget.org</span></span>
* <span data-ttu-id="e826d-122">Tüm API anahtarları silinir ait</span><span class="sxs-lookup"><span data-stu-id="e826d-122">All owned API Keys are deleted</span></span>
* <span data-ttu-id="e826d-123">Tüm ayrılmış ad alanlarından yayımlanan</span><span class="sxs-lookup"><span data-stu-id="e826d-123">All reserved namespaces are released</span></span>
* <span data-ttu-id="e826d-124">Herhangi bir paket sahipliği kaldırılır</span><span class="sxs-lookup"><span data-stu-id="e826d-124">Any package ownership are removed</span></span>

<span data-ttu-id="e826d-125">Sahip olunan paketleri *değil* silindi.</span><span class="sxs-lookup"><span data-stu-id="e826d-125">The owned packages are *not* deleted.</span></span> <span data-ttu-id="e826d-126">Listelenmemiş Arama sonuçlarından rağmen bunlara bağımlı projeler için paket geri yükleme yoluyla kullanılabilir kalır.</span><span class="sxs-lookup"><span data-stu-id="e826d-126">Though unlisted from search results, they remain available through package restore to projects that depend on them.</span></span>

## <a name="exporting-customer-data"></a><span data-ttu-id="e826d-127">Müşteri verilerini dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="e826d-127">Exporting customer data</span></span>

<span data-ttu-id="e826d-128">Oturum açma işleminden sonra nuget.org için bir kullanıcı bir dışarı aktarma isteği aracılığıyla gönderebilir [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)</span><span class="sxs-lookup"><span data-stu-id="e826d-128">After sign-in to nuget.org, a user can submit an export request through [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)</span></span>

<span data-ttu-id="e826d-129">Dışarı aktarılan verileri 48 saattir kullanıcıya aracılığıyla bir Azure Blob indirme için kullanılabilir hale getirilir.</span><span class="sxs-lookup"><span data-stu-id="e826d-129">The data exported is made available for 48 hours to the user for download through an Azure Blob.</span></span> <span data-ttu-id="e826d-130">48 saat sonra erişim süresi ve kullanıcı, gerektiği gibi yeni bir dışa aktarma isteği göndermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e826d-130">After 48 hours, access expires and the user must submit a new export request as needed.</span></span>

<span data-ttu-id="e826d-131">Dışarı aktarılan verileri içerir:</span><span class="sxs-lookup"><span data-stu-id="e826d-131">The exported data includes:</span></span>

* <span data-ttu-id="e826d-132">Kullanıcının destek istekleri</span><span class="sxs-lookup"><span data-stu-id="e826d-132">The user's support requests</span></span>
* <span data-ttu-id="e826d-133">Kullanıcının eylemlerini (paket yayımlama, hesabı oluşturma) denetim günlüklerinde kalıcı olarak</span><span class="sxs-lookup"><span data-stu-id="e826d-133">The user's actions (publish package, create account) as persisted in the audit logs</span></span>
* <span data-ttu-id="e826d-134">IIS günlükleri kalıcı olarak herhangi bir kullanıcı bilgisi</span><span class="sxs-lookup"><span data-stu-id="e826d-134">Any user information as persisted in the IIS logs</span></span>
