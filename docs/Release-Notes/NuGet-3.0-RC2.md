---
title: "NuGet 3.0 RC2 sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet 3.0 RC2 için bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 3.0 RC2 sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 67299408170ae3c3676c2866bec2945b41ad4184
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-30-rc2-release-notes"></a><span data-ttu-id="d0bdd-104">NuGet 3.0 RC2 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="d0bdd-104">NuGet 3.0 RC2 Release Notes</span></span>

<span data-ttu-id="d0bdd-105">[NuGet 3.0 RC sürüm notları](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 sürüm notları](../release-notes/nuget-3.0.0.md)</span><span class="sxs-lookup"><span data-stu-id="d0bdd-105">[NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md)</span></span>

<span data-ttu-id="d0bdd-106">NuGet 3.0 RC2 yayımlanan 3 Haziran 2015 tarihinde Visual Studio 2015 uzantısı galerisinden kullanılabilir sürüm bir geçici olarak ve [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span><span class="sxs-lookup"><span data-stu-id="d0bdd-106">NuGet 3.0 RC2 was released on June 3, 2015 as an interim release available from the Visual Studio 2015 Extension Gallery and [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span></span> <span data-ttu-id="d0bdd-107">Önemli hata düzeltmeleri sayısı bu sürümde var ve biz Keçeli performans iyileştirmeleri tamamlanmış Visual Studio 2015 yayımlanmadan önce serbest bırakmak önemli.</span><span class="sxs-lookup"><span data-stu-id="d0bdd-107">This release has a number of important bug fixes and performance improvements that we felt were important to release before the completed Visual Studio 2015 release.</span></span> <span data-ttu-id="d0bdd-108">Bu NuGet uzantısı sürüm yalnızca Visual Studio 2015 için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d0bdd-108">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="d0bdd-109">Toplam, biz bu sürümde 158 sorunları kapalı ve gözden geçirebilirsiniz [github'da sorunların tam listesi](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span><span class="sxs-lookup"><span data-stu-id="d0bdd-109">In total, we closed 158 issues in this release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span></span>

## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="d0bdd-110">Üst Sorunlar çözüldüğünde özeti</span><span class="sxs-lookup"><span data-stu-id="d0bdd-110">Summary of top issues resolved</span></span>

* [<span data-ttu-id="d0bdd-111">Paket Yöneticisi penceresi yenilendiğinde sık ağ güncelleştirme çağırır</span><span class="sxs-lookup"><span data-stu-id="d0bdd-111">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="d0bdd-112">Değiştirerek görünümü Paket Yöneticisi'nde yüklendiğinde kaydırma ertelendi</span><span class="sxs-lookup"><span data-stu-id="d0bdd-112">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="d0bdd-113">Ağ çağrıları arka plan iş parçacığında çalıştırılmalıdır</span><span class="sxs-lookup"><span data-stu-id="d0bdd-113">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="d0bdd-114">Eklenen 'önizleme penceresi gösterme' onay kutusu</span><span class="sxs-lookup"><span data-stu-id="d0bdd-114">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="d0bdd-115">Eklenen işlemi işlemci kullanımını azaltmak için azaltma</span><span class="sxs-lookup"><span data-stu-id="d0bdd-115">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="d0bdd-116">Geliştirilmiş taşınabilir sınıf kitaplığı başvurusu işleme</span><span class="sxs-lookup"><span data-stu-id="d0bdd-116">Improved portable-class-library reference handling</span></span>
    * [<span data-ttu-id="d0bdd-117">https://github.com/NuGet/Home/issues/562</span><span class="sxs-lookup"><span data-stu-id="d0bdd-117">https://github.com/NuGet/Home/issues/562</span></span>](https://github.com/NuGet/Home/issues/562)
    * [<span data-ttu-id="d0bdd-118">https://github.com/NuGet/Home/issues/454</span><span class="sxs-lookup"><span data-stu-id="d0bdd-118">https://github.com/NuGet/Home/issues/454</span></span>](https://github.com/NuGet/Home/issues/454)
    * [<span data-ttu-id="d0bdd-119">https://github.com/NuGet/Home/issues/440</span><span class="sxs-lookup"><span data-stu-id="d0bdd-119">https://github.com/NuGet/Home/issues/440</span></span>](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="d0bdd-120">Otomatik Tamamlama hizmet büyük küçük harfe duyarlı</span><span class="sxs-lookup"><span data-stu-id="d0bdd-120">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="d0bdd-121">Temel kimlik doğrulama kimlik bilgilerini yeniden etkilenmesine neden güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="d0bdd-121">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="d0bdd-122">Geliştirilmiş hata günlüğü</span><span class="sxs-lookup"><span data-stu-id="d0bdd-122">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="d0bdd-123">Güncelleştirme paketi çağrılırken geliştirilmiş powershell hata iletileri</span><span class="sxs-lookup"><span data-stu-id="d0bdd-123">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)

<span data-ttu-id="d0bdd-124">Bu karşıdan [güncelleştirmek için NuGet uzantısı](https://nuget.codeplex.com/releases/view/615507) Codeplex ve Lütfen takip [bizim blog](http://blog.nuget.org) daha fazla ilerleme ve duyuruları NuGet 3.0 için!</span><span class="sxs-lookup"><span data-stu-id="d0bdd-124">Download this [update to the NuGet extension](https://nuget.codeplex.com/releases/view/615507) from Codeplex and please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>