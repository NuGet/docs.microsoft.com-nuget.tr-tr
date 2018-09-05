---
title: NuGet 3.0 RC2 sürüm notları
description: NuGet 3.0 RC2 için bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve dcr dahil olmak üzere sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 863e48e632387b768a43530b987683605baf6db7
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545827"
---
# <a name="nuget-30-rc2-release-notes"></a><span data-ttu-id="7eb4d-103">NuGet 3.0 RC2 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="7eb4d-103">NuGet 3.0 RC2 Release Notes</span></span>

<span data-ttu-id="7eb4d-104">[NuGet 3.0 RC sürüm notları](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 sürüm notları](../release-notes/nuget-3.0.0.md)</span><span class="sxs-lookup"><span data-stu-id="7eb4d-104">[NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md)</span></span>

<span data-ttu-id="7eb4d-105">NuGet 3.0 RC2 bırakıldığını 3 Haziran 2015'te Visual Studio 2015 uzantı Galerisi kullanılabilir sürüm bir geçici olarak ve [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span><span class="sxs-lookup"><span data-stu-id="7eb4d-105">NuGet 3.0 RC2 was released on June 3, 2015 as an interim release available from the Visual Studio 2015 Extension Gallery and [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span></span> <span data-ttu-id="7eb4d-106">Bu sürüm önemli hata düzeltmeleri vardır ve biz düşünmüştür performans geliştirmeleri tamamlandı Visual Studio 2015 sürüm önce serbest bırakmak önemli.</span><span class="sxs-lookup"><span data-stu-id="7eb4d-106">This release has a number of important bug fixes and performance improvements that we felt were important to release before the completed Visual Studio 2015 release.</span></span> <span data-ttu-id="7eb4d-107">Bu NuGet uzantısı sürüm, yalnızca Visual Studio 2015 için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7eb4d-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="7eb4d-108">Biz bu sürümde 158 sorunları toplam kapalı ve gözden geçirebilirsiniz [github'da sorunların tam listesi](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span><span class="sxs-lookup"><span data-stu-id="7eb4d-108">In total, we closed 158 issues in this release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span></span>

## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="7eb4d-109">Çözümlenen üst sorunların özeti</span><span class="sxs-lookup"><span data-stu-id="7eb4d-109">Summary of top issues resolved</span></span>

* [<span data-ttu-id="7eb4d-110">Paket Yöneticisi penceresini yenilediğinde ağ sık sık güncelleştirme çağırır.</span><span class="sxs-lookup"><span data-stu-id="7eb4d-110">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="7eb4d-111">Kaydırma değiştirerek görünümü Paket Yöneticisi'nde yüklendiğinde Gecikmeli</span><span class="sxs-lookup"><span data-stu-id="7eb4d-111">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="7eb4d-112">Ağ çağrıları arka plan iş parçacığında çalıştırılmalıdır</span><span class="sxs-lookup"><span data-stu-id="7eb4d-112">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="7eb4d-113">Eklenen 'Önizleme penceresini gösterme' onay kutusu</span><span class="sxs-lookup"><span data-stu-id="7eb4d-113">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="7eb4d-114">Ek işlem işlemci kullanımını azaltmak için azaltma</span><span class="sxs-lookup"><span data-stu-id="7eb4d-114">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="7eb4d-115">Geliştirilmiş işleme taşınabilir sınıf kitaplığı başvurusu</span><span class="sxs-lookup"><span data-stu-id="7eb4d-115">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="7eb4d-116">Otomatik Tamamlama hizmeti büyük küçük harfe duyarlı</span><span class="sxs-lookup"><span data-stu-id="7eb4d-116">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="7eb4d-117">Temel kimlik doğrulama kimlik bilgileri güçlendirebilir güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="7eb4d-117">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="7eb4d-118">Geliştirilmiş hata günlüğü</span><span class="sxs-lookup"><span data-stu-id="7eb4d-118">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="7eb4d-119">Update-Package çağırırken powershell geliştirilmiş hata iletileri</span><span class="sxs-lookup"><span data-stu-id="7eb4d-119">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)

<span data-ttu-id="7eb4d-120">Bu indirme [güncelleştirmek için NuGet uzantısı](https://nuget.codeplex.com/releases/view/615507) codeplex'ten ve Lütfen gözünüzü [blogumuzu](http://blog.nuget.org) daha fazla ilerleme ve NuGet 3.0 duyuruları!</span><span class="sxs-lookup"><span data-stu-id="7eb4d-120">Download this [update to the NuGet extension](https://nuget.codeplex.com/releases/view/615507) from Codeplex and please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>