---
title: NuGet 3,0 RC2 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 3,0 RC2 için sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 355c200481f4acba9931dc3bcd85e99c5ffbf224
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780276"
---
# <a name="nuget-30-rc2-release-notes"></a><span data-ttu-id="17e60-103">NuGet 3,0 RC2 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="17e60-103">NuGet 3.0 RC2 Release Notes</span></span>

<span data-ttu-id="17e60-104">[NuGet 3,0 RC sürüm notları](../release-notes/nuget-3.0-RC.md)  |  [NuGet 3,0 sürüm notları](../release-notes/nuget-3.0.0.md)</span><span class="sxs-lookup"><span data-stu-id="17e60-104">[NuGet 3.0 RC Release Notes](../release-notes/nuget-3.0-RC.md) | [NuGet 3.0 Release Notes](../release-notes/nuget-3.0.0.md)</span></span>

<span data-ttu-id="17e60-105">NuGet 3,0 RC2, Visual Studio 2015 uzantı Galerisi ve [CodePlex](https://nuget.codeplex.com/releases/view/615507)'te kullanıma sunulan bir geçici yayın olarak 3 Haziran 2015 tarihinde yayınlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="17e60-105">NuGet 3.0 RC2 was released on June 3, 2015 as an interim release available from the Visual Studio 2015 Extension Gallery and [Codeplex](https://nuget.codeplex.com/releases/view/615507).</span></span> <span data-ttu-id="17e60-106">Bu sürümde, tamamlanmış Visual Studio 2015 sürümünden önce yayınlanmakta önemli olan önemli hata düzeltmeleri ve performans iyileştirmeleri vardır.</span><span class="sxs-lookup"><span data-stu-id="17e60-106">This release has a number of important bug fixes and performance improvements that we felt were important to release before the completed Visual Studio 2015 release.</span></span> <span data-ttu-id="17e60-107">Bu NuGet uzantısı sürümü yalnızca Visual Studio 2015 için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="17e60-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="17e60-108">Toplam olarak, bu sürümdeki 158 sorunu kapattık ve [GitHub 'daki sorunların tam listesini](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01)inceleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="17e60-108">In total, we closed 158 issues in this release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01).</span></span>

## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="17e60-109">Çözümlenen başlıca sorunların Özeti</span><span class="sxs-lookup"><span data-stu-id="17e60-109">Summary of top issues resolved</span></span>

* [<span data-ttu-id="17e60-110">Paket Yöneticisi penceresi yenilendiğinde sık kullanılan ağ güncelleştirme çağrıları</span><span class="sxs-lookup"><span data-stu-id="17e60-110">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="17e60-111">Paket Yöneticisi 'nde yüklü görünüme geçiş yaparken gecikmeli kaydırma</span><span class="sxs-lookup"><span data-stu-id="17e60-111">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="17e60-112">Ağ çağrıları bir arka plan iş parçacığında çalıştırılmalıdır</span><span class="sxs-lookup"><span data-stu-id="17e60-112">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="17e60-113">' Önizleme penceresini gösterme ' onay kutusu eklendi</span><span class="sxs-lookup"><span data-stu-id="17e60-113">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="17e60-114">İşlemci kullanımını azaltmak için işlem azaltma eklendi</span><span class="sxs-lookup"><span data-stu-id="17e60-114">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="17e60-115">İyileştirilmiş taşınabilir sınıf kitaplığı başvuru işleme</span><span class="sxs-lookup"><span data-stu-id="17e60-115">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="17e60-116">Otomatik tamamlama hizmeti büyük/küçük harfe duyarlıdır</span><span class="sxs-lookup"><span data-stu-id="17e60-116">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="17e60-117">Temel kimlik doğrulama kimlik bilgilerini yeniden tanıtmak için Güncelleştir</span><span class="sxs-lookup"><span data-stu-id="17e60-117">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="17e60-118">İyileştirilmiş hata günlüğü</span><span class="sxs-lookup"><span data-stu-id="17e60-118">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="17e60-119">Update-Package çağrılırken geliştirilmiş PowerShell hata iletileri</span><span class="sxs-lookup"><span data-stu-id="17e60-119">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)

<span data-ttu-id="17e60-120">Bu güncelleştirmeyi CodePlex 'ten [NuGet uzantısına](https://nuget.codeplex.com/releases/view/615507) Indirin ve NuGet 3,0 için daha fazla ilerleme ve duyuru için [blogumuza](http://blog.nuget.org) göz önünde bulundurun!</span><span class="sxs-lookup"><span data-stu-id="17e60-120">Download this [update to the NuGet extension](https://nuget.codeplex.com/releases/view/615507) from Codeplex and please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>