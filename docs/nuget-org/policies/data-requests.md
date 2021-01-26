---
title: Kullanıcı veri Istekleri
description: Kullanıcı verilerini dışa ve silmeyi isteme ilkeleri
author: JonDouglas
ms.author: jodou
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: e0ec429469a992c9558d1635890fd568398206a1
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775723"
---
# <a name="user-data-requests"></a><span data-ttu-id="2d255-103">Kullanıcı veri Istekleri</span><span class="sxs-lookup"><span data-stu-id="2d255-103">User Data Requests</span></span>

<span data-ttu-id="2d255-104">nuget.org kullanıcılar, [NuGet.org](https://www.nuget.org)aracılığıyla bilgi silme isteklerini ve bilgi dışarı aktarma isteklerini gönderebilir. Her iki tür de destek istekleri biçiminde gönderilir ve 30 gün içinde nuget.org yöneticileri tarafından yürütülür.</span><span class="sxs-lookup"><span data-stu-id="2d255-104">nuget.org users can submit information delete requests and information export requests through [nuget.org](https://www.nuget.org). Both types are submitted in the form of support requests and are be executed by the nuget.org administrators within 30 days.</span></span>

<span data-ttu-id="2d255-105">Aşağıdaki kullanıcı verilerine doğrudan nuget.org üzerinden erişilebilir:</span><span class="sxs-lookup"><span data-stu-id="2d255-105">The following user data is directly accessible through nuget.org:</span></span>

* <span data-ttu-id="2d255-106">E-posta adresi, oturum açma hesabı, profil resmi ve e-posta bildirim ayarları gibi hesap ile ilgili veriler</span><span class="sxs-lookup"><span data-stu-id="2d255-106">Account related data such as email address, login account, profile picture, and email notification settings</span></span>
* <span data-ttu-id="2d255-107">Sahip olan API anahtarları</span><span class="sxs-lookup"><span data-stu-id="2d255-107">Owned API Keys</span></span>
* <span data-ttu-id="2d255-108">Sahip olunan paketlerin listesi</span><span class="sxs-lookup"><span data-stu-id="2d255-108">List of owned packages</span></span>

<span data-ttu-id="2d255-109">Bu veriler, destek isteği aracılığıyla dışarıya aktarılmış verilere dahil değildir.</span><span class="sxs-lookup"><span data-stu-id="2d255-109">This data is not included in data exported through the support request.</span></span>

## <a name="identifying-customer-data"></a><span data-ttu-id="2d255-110">Müşteri verilerini tanımlama</span><span class="sxs-lookup"><span data-stu-id="2d255-110">Identifying customer data</span></span>

<span data-ttu-id="2d255-111">Müşteri verileri, nuget.org Kullanıcı hesabı adı olarak tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="2d255-111">Customer data can be identified as nuget.org user account names.</span></span>

## <a name="deleting-customer-data"></a><span data-ttu-id="2d255-112">Müşteri verilerini silme</span><span class="sxs-lookup"><span data-stu-id="2d255-112">Deleting customer data</span></span>

<span data-ttu-id="2d255-113">Nuget.org 'ten Kullanıcı verilerini silme isteğinde bulunan:</span><span class="sxs-lookup"><span data-stu-id="2d255-113">To request deleting user data from nuget.org:</span></span>

1. <span data-ttu-id="2d255-114">Kullanıcının [NuGet.org](https://www.nuget.org) 'de oturum açması gerekir</span><span class="sxs-lookup"><span data-stu-id="2d255-114">The user must sign-in to [nuget.org](https://www.nuget.org)</span></span>
1. <span data-ttu-id="2d255-115">Kullanıcının, hesabı için bir istek göndermesi gerekir [NuGet.org/Account/Delete](https://www.nuget.org/account/delete)</span><span class="sxs-lookup"><span data-stu-id="2d255-115">The user must submit a request for their account to be deleted [nuget.org/account/delete](https://www.nuget.org/account/delete)</span></span>

<span data-ttu-id="2d255-116">Yalnızca paketlerin sahibi olan kullanıcıların, hesaplarının silinmesini istemeden önce yeni sahipleri bulması önerilir.</span><span class="sxs-lookup"><span data-stu-id="2d255-116">Users that are sole owners of packages are encouraged to find new owners before asking to have their account deleted.</span></span> <span data-ttu-id="2d255-117">Paket sahipliği aktarılmadıysa, NuGet paketi listelenmemiş olur ve sonuç olarak, Visual Studio 'da veya nuget.org web sitesinde arama sorgularında artık kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="2d255-117">If package ownership is not transferred, the NuGet package is unlisted and, as a result, it is no longer available in search queries in Visual Studio or on the nuget.org website.</span></span> <span data-ttu-id="2d255-118">Hesabı silmeden önce, nuget.org yöneticileri sahip oldukları paketlerin yeni sahiplerini bulmak için kullanıcıyla birlikte çalışır.</span><span class="sxs-lookup"><span data-stu-id="2d255-118">Before deleting the account, the nuget.org administrators work with the user to find new owners for the packages they own.</span></span>

<span data-ttu-id="2d255-119">Hesap silme eylemi, istek tarihinden itibaren 30 gün içinde nuget.org Yöneticisi tarafından tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="2d255-119">The account delete action is completed by the nuget.org administrator within 30 days from the date of the request.</span></span>

<span data-ttu-id="2d255-120">Hesap silme işleminden sonra, tüm Kullanıcı verileri nuget.org sisteminden kaldırılır ve aşağıdaki eylemler gerçekleştirilir:</span><span class="sxs-lookup"><span data-stu-id="2d255-120">Upon account deletion, all of the user's data is be removed from the nuget.org system and the following actions are taken:</span></span>

* <span data-ttu-id="2d255-121">Silinen hesabın kaydı nuget.org olur</span><span class="sxs-lookup"><span data-stu-id="2d255-121">The deleted account becomes unregistered with nuget.org</span></span>
* <span data-ttu-id="2d255-122">Sahip olunan tüm API anahtarları silinir</span><span class="sxs-lookup"><span data-stu-id="2d255-122">All owned API Keys are deleted</span></span>
* <span data-ttu-id="2d255-123">Tüm ayrılmış ad alanları serbest bırakılır</span><span class="sxs-lookup"><span data-stu-id="2d255-123">All reserved namespaces are released</span></span>
* <span data-ttu-id="2d255-124">Tüm paket sahipliği kaldırılır</span><span class="sxs-lookup"><span data-stu-id="2d255-124">Any package ownership are removed</span></span>

<span data-ttu-id="2d255-125">Sahip olunan *paketler silinmez.*</span><span class="sxs-lookup"><span data-stu-id="2d255-125">The owned packages are *not* deleted.</span></span> <span data-ttu-id="2d255-126">Arama sonuçlarından etkilenmese de, bunlara bağlı projelere paket geri yüklemesi aracılığıyla erişilebilir kalırlar.</span><span class="sxs-lookup"><span data-stu-id="2d255-126">Though unlisted from search results, they remain available through package restore to projects that depend on them.</span></span>

## <a name="exporting-customer-data"></a><span data-ttu-id="2d255-127">Müşteri verilerini dışa aktarma</span><span class="sxs-lookup"><span data-stu-id="2d255-127">Exporting customer data</span></span>

<span data-ttu-id="2d255-128">Nuget.org 'de oturum açtıktan sonra, Kullanıcı [NuGet.org/policies/Contact](https://www.nuget.org/policies/Contact) aracılığıyla bir dışarı aktarma isteği gönderebilir</span><span class="sxs-lookup"><span data-stu-id="2d255-128">After sign-in to nuget.org, a user can submit an export request through [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)</span></span>

<span data-ttu-id="2d255-129">İçe aktarılmış veriler, kullanıcının bir Azure blobu aracılığıyla indirileceği 48 saat için kullanılabilir hale getirilir.</span><span class="sxs-lookup"><span data-stu-id="2d255-129">The data exported is made available for 48 hours to the user for download through an Azure Blob.</span></span> <span data-ttu-id="2d255-130">48 saat sonra, erişim süresi dolar ve Kullanıcı gerektiğinde yeni bir dışarı aktarma isteği göndermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="2d255-130">After 48 hours, access expires and the user must submit a new export request as needed.</span></span>

<span data-ttu-id="2d255-131">İçe aktarılmış veriler şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="2d255-131">The exported data includes:</span></span>

* <span data-ttu-id="2d255-132">Kullanıcının destek istekleri</span><span class="sxs-lookup"><span data-stu-id="2d255-132">The user's support requests</span></span>
* <span data-ttu-id="2d255-133">Kullanıcı eylemleri (paketi Yayımla, hesabı oluştur) denetim günlüklerinde kalıcı olarak</span><span class="sxs-lookup"><span data-stu-id="2d255-133">The user's actions (publish package, create account) as persisted in the audit logs</span></span>
* <span data-ttu-id="2d255-134">IIS günlüklerinde kalıcı olarak herhangi bir Kullanıcı bilgisi</span><span class="sxs-lookup"><span data-stu-id="2d255-134">Any user information as persisted in the IIS logs</span></span>
