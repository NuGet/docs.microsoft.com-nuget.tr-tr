---
title: Kullanıcı Veri İstekleri
description: Kullanıcı verilerinin dışa aktarılmasını ve silinilmesini isteme ilkeleri
author: karann-msft
ms.author: karann
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: ef054f741755bccf56eedfd462915b8e9fd6931a
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427514"
---
# <a name="user-data-requests"></a><span data-ttu-id="f80c8-103">Kullanıcı Veri İstekleri</span><span class="sxs-lookup"><span data-stu-id="f80c8-103">User Data Requests</span></span>

<span data-ttu-id="f80c8-104">nuget.org kullanıcılar [nuget.org](https://www.nuget.org)üzerinden bilgi silme isteklerini ve bilgi verme isteklerini gönderebilirler. Her iki tür de destek istekleri şeklinde gönderilir ve 30 gün içinde nuget.org yöneticileri tarafından yürütülür.</span><span class="sxs-lookup"><span data-stu-id="f80c8-104">nuget.org users can submit information delete requests and information export requests through [nuget.org](https://www.nuget.org). Both types are submitted in the form of support requests and are be executed by the nuget.org administrators within 30 days.</span></span>

<span data-ttu-id="f80c8-105">Aşağıdaki kullanıcı verilerine nuget.org aracılığıyla doğrudan erişilebilir:</span><span class="sxs-lookup"><span data-stu-id="f80c8-105">The following user data is directly accessible through nuget.org:</span></span>

* <span data-ttu-id="f80c8-106">E-posta adresi, giriş hesabı, profil resmi ve e-posta bildirim ayarları gibi hesapla ilgili veriler</span><span class="sxs-lookup"><span data-stu-id="f80c8-106">Account related data such as email address, login account, profile picture, and email notification settings</span></span>
* <span data-ttu-id="f80c8-107">Sahip OLUNan API Anahtarları</span><span class="sxs-lookup"><span data-stu-id="f80c8-107">Owned API Keys</span></span>
* <span data-ttu-id="f80c8-108">Sahip olunan paketler listesi</span><span class="sxs-lookup"><span data-stu-id="f80c8-108">List of owned packages</span></span>

<span data-ttu-id="f80c8-109">Bu veriler, destek isteği yoluyla dışa aktarılan verilere dahil edilmez.</span><span class="sxs-lookup"><span data-stu-id="f80c8-109">This data is not included in data exported through the support request.</span></span>

## <a name="identifying-customer-data"></a><span data-ttu-id="f80c8-110">Müşteri verilerinin tanımlanması</span><span class="sxs-lookup"><span data-stu-id="f80c8-110">Identifying customer data</span></span>

<span data-ttu-id="f80c8-111">Müşteri verileri nuget.org kullanıcı hesabı adları olarak tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="f80c8-111">Customer data can be identified as nuget.org user account names.</span></span>

## <a name="deleting-customer-data"></a><span data-ttu-id="f80c8-112">Müşteri verilerini silme</span><span class="sxs-lookup"><span data-stu-id="f80c8-112">Deleting customer data</span></span>

<span data-ttu-id="f80c8-113">Kullanıcı verilerinin nuget.org silen isteği için:</span><span class="sxs-lookup"><span data-stu-id="f80c8-113">To request deleting user data from nuget.org:</span></span>

1. <span data-ttu-id="f80c8-114">Kullanıcı [nuget.org](https://www.nuget.org) oturum açmalı</span><span class="sxs-lookup"><span data-stu-id="f80c8-114">The user must sign-in to [nuget.org](https://www.nuget.org)</span></span>
1. <span data-ttu-id="f80c8-115">Kullanıcı, hesabının [silinmesi](https://www.nuget.org/account/delete) için bir istek nuget.org/account/delete</span><span class="sxs-lookup"><span data-stu-id="f80c8-115">The user must submit a request for their account to be deleted [nuget.org/account/delete](https://www.nuget.org/account/delete)</span></span>

<span data-ttu-id="f80c8-116">Paketlerin tek sahibi olan kullanıcıların, hesaplarının silinmesini istemeden önce yeni sahipler bulmaları tavsiye edilir.</span><span class="sxs-lookup"><span data-stu-id="f80c8-116">Users that are sole owners of packages are encouraged to find new owners before asking to have their account deleted.</span></span> <span data-ttu-id="f80c8-117">Paket sahipliği aktarılamazsa, NuGet paketi liste dışı kalır ve sonuç olarak Visual Studio'daki arama sorgularında veya nuget.org web sitesinde kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="f80c8-117">If package ownership is not transferred, the NuGet package is unlisted and, as a result, it is no longer available in search queries in Visual Studio or on the nuget.org website.</span></span> <span data-ttu-id="f80c8-118">Hesabı silmeden önce, nuget.org yöneticileri sahip oldukları paketler için yeni sahipler bulmak için kullanıcıyla birlikte çalışır.</span><span class="sxs-lookup"><span data-stu-id="f80c8-118">Before deleting the account, the nuget.org administrators work with the user to find new owners for the packages they own.</span></span>

<span data-ttu-id="f80c8-119">Hesap silme eylemi, istek tarihinden itibaren 30 gün içinde nuget.org yöneticisi tarafından tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="f80c8-119">The account delete action is completed by the nuget.org administrator within 30 days from the date of the request.</span></span>

<span data-ttu-id="f80c8-120">Hesap silme işleminde, kullanıcının tüm verileri nuget.org sisteminden kaldırılır ve aşağıdaki işlemler yapılır:</span><span class="sxs-lookup"><span data-stu-id="f80c8-120">Upon account deletion, all of the user's data is be removed from the nuget.org system and the following actions are taken:</span></span>

* <span data-ttu-id="f80c8-121">Silinen hesap nuget.org ile kayıt dışı olur</span><span class="sxs-lookup"><span data-stu-id="f80c8-121">The deleted account becomes unregistered with nuget.org</span></span>
* <span data-ttu-id="f80c8-122">Sahip olunan tüm API Anahtarları silinir</span><span class="sxs-lookup"><span data-stu-id="f80c8-122">All owned API Keys are deleted</span></span>
* <span data-ttu-id="f80c8-123">Tüm ayrılmış ad alanları serbest bırakılır</span><span class="sxs-lookup"><span data-stu-id="f80c8-123">All reserved namespaces are released</span></span>
* <span data-ttu-id="f80c8-124">Herhangi bir paket sahipliği kaldırılır</span><span class="sxs-lookup"><span data-stu-id="f80c8-124">Any package ownership are removed</span></span>

<span data-ttu-id="f80c8-125">Sahip olunan paketler *silinmez.*</span><span class="sxs-lookup"><span data-stu-id="f80c8-125">The owned packages are *not* deleted.</span></span> <span data-ttu-id="f80c8-126">Arama sonuçlarından listelenmemiş olsalar da, bunlar paket geri yükleme yoluyla bunlara bağlı projelere kullanılabilir durumda kalır.</span><span class="sxs-lookup"><span data-stu-id="f80c8-126">Though unlisted from search results, they remain available through package restore to projects that depend on them.</span></span>

## <a name="exporting-customer-data"></a><span data-ttu-id="f80c8-127">Müşteri verilerini dışa aktarma</span><span class="sxs-lookup"><span data-stu-id="f80c8-127">Exporting customer data</span></span>

<span data-ttu-id="f80c8-128">nuget.org oturum açmadan sonra, kullanıcı [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact) aracılığıyla bir dışa aktarma isteği gönderebilir</span><span class="sxs-lookup"><span data-stu-id="f80c8-128">After sign-in to nuget.org, a user can submit an export request through [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)</span></span>

<span data-ttu-id="f80c8-129">İhraç edilen veriler, Azure Blob üzerinden indirilebilmek için kullanıcıya 48 saat süreyle kullanıma sunulur.</span><span class="sxs-lookup"><span data-stu-id="f80c8-129">The data exported is made available for 48 hours to the user for download through an Azure Blob.</span></span> <span data-ttu-id="f80c8-130">48 saat sonra erişimin süresi doluyor ve kullanıcı nın gerektiğinde yeni bir dışa aktarma isteği göndermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="f80c8-130">After 48 hours, access expires and the user must submit a new export request as needed.</span></span>

<span data-ttu-id="f80c8-131">Dışa aktarılan veriler şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="f80c8-131">The exported data includes:</span></span>

* <span data-ttu-id="f80c8-132">Kullanıcının destek istekleri</span><span class="sxs-lookup"><span data-stu-id="f80c8-132">The user's support requests</span></span>
* <span data-ttu-id="f80c8-133">Denetim günlüklerinde kalıcı olarak kullanıcının eylemleri (paket yayınlama, hesap oluşturma)</span><span class="sxs-lookup"><span data-stu-id="f80c8-133">The user's actions (publish package, create account) as persisted in the audit logs</span></span>
* <span data-ttu-id="f80c8-134">IIS günlüklerinde kalıcı olan tüm kullanıcı bilgileri</span><span class="sxs-lookup"><span data-stu-id="f80c8-134">Any user information as persisted in the IIS logs</span></span>
