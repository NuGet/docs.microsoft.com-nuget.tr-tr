---
title: NuGet 3.0 RC2 sürüm notları
description: NuGet 3.0 RC2 için bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere sürüm notları.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: eb8b514fa967cc6ef850483b6b2a5df3ab27a550
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819890"
---
# <a name="nuget-30-rc2-release-notes"></a><span data-ttu-id="cf77c-103">NuGet 3.0 RC2 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="cf77c-103">NuGet 3.0 RC2 Release Notes</span></span>

<span data-ttu-id="cf77c-104">[NuGet 3.0 RC sürüm notları](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 sürüm notları](../release-notes/nuget-3.0.0.md)</span><span class="sxs-lookup"><span data-stu-id="cf77c-104">[NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md)</span></span>

<span data-ttu-id="cf77c-105">NuGet 3.0 RC2 yayımlanan 3 Haziran 2015 tarihinde Visual Studio 2015 uzantısı galerisinden kullanılabilir sürüm bir geçici olarak ve [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span><span class="sxs-lookup"><span data-stu-id="cf77c-105">NuGet 3.0 RC2 was released on June 3, 2015 as an interim release available from the Visual Studio 2015 Extension Gallery and [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span></span> <span data-ttu-id="cf77c-106">Önemli hata düzeltmeleri sayısı bu sürümde var ve biz Keçeli performans iyileştirmeleri tamamlanmış Visual Studio 2015 yayımlanmadan önce serbest bırakmak önemli.</span><span class="sxs-lookup"><span data-stu-id="cf77c-106">This release has a number of important bug fixes and performance improvements that we felt were important to release before the completed Visual Studio 2015 release.</span></span> <span data-ttu-id="cf77c-107">Bu NuGet uzantısı sürüm yalnızca Visual Studio 2015 için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="cf77c-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="cf77c-108">Toplam, biz bu sürümde 158 sorunları kapalı ve gözden geçirebilirsiniz [github'da sorunların tam listesi](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span><span class="sxs-lookup"><span data-stu-id="cf77c-108">In total, we closed 158 issues in this release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span></span>

## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="cf77c-109">Üst Sorunlar çözüldüğünde özeti</span><span class="sxs-lookup"><span data-stu-id="cf77c-109">Summary of top issues resolved</span></span>

* [<span data-ttu-id="cf77c-110">Paket Yöneticisi penceresi yenilendiğinde sık ağ güncelleştirme çağırır</span><span class="sxs-lookup"><span data-stu-id="cf77c-110">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="cf77c-111">Değiştirerek görünümü Paket Yöneticisi'nde yüklendiğinde kaydırma ertelendi</span><span class="sxs-lookup"><span data-stu-id="cf77c-111">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="cf77c-112">Ağ çağrıları arka plan iş parçacığında çalıştırılmalıdır</span><span class="sxs-lookup"><span data-stu-id="cf77c-112">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="cf77c-113">Eklenen 'önizleme penceresi gösterme' onay kutusu</span><span class="sxs-lookup"><span data-stu-id="cf77c-113">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="cf77c-114">Eklenen işlemi işlemci kullanımını azaltmak için azaltma</span><span class="sxs-lookup"><span data-stu-id="cf77c-114">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="cf77c-115">Geliştirilmiş taşınabilir sınıf kitaplığı başvurusu işleme</span><span class="sxs-lookup"><span data-stu-id="cf77c-115">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="cf77c-116">Otomatik Tamamlama hizmet büyük küçük harfe duyarlı</span><span class="sxs-lookup"><span data-stu-id="cf77c-116">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="cf77c-117">Temel kimlik doğrulama kimlik bilgilerini yeniden etkilenmesine neden güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="cf77c-117">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="cf77c-118">Geliştirilmiş hata günlüğü</span><span class="sxs-lookup"><span data-stu-id="cf77c-118">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="cf77c-119">Güncelleştirme paketi çağrılırken geliştirilmiş powershell hata iletileri</span><span class="sxs-lookup"><span data-stu-id="cf77c-119">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)

<span data-ttu-id="cf77c-120">Bu karşıdan [güncelleştirmek için NuGet uzantısı](https://nuget.codeplex.com/releases/view/615507) Codeplex ve Lütfen takip [bizim blog](http://blog.nuget.org) daha fazla ilerleme ve duyuruları NuGet 3.0 için!</span><span class="sxs-lookup"><span data-stu-id="cf77c-120">Download this [update to the NuGet extension](https://nuget.codeplex.com/releases/view/615507) from Codeplex and please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>