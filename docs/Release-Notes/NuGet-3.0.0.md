---
title: NuGet 3.0 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr NuGet 3.0.0 dahil etmek için sürüm notları.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 26236c2db0e1a6be9c660905db567d9ebbbbe377
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-30-release-notes"></a><span data-ttu-id="f00ed-103">NuGet 3.0 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="f00ed-103">NuGet 3.0 Release Notes</span></span>

<span data-ttu-id="f00ed-104">[NuGet 3.0 RC2 sürüm notları](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 sürüm notları](../release-notes/nuget-3.1.md)</span><span class="sxs-lookup"><span data-stu-id="f00ed-104">[NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 Release Notes](../release-notes/nuget-3.1.md)</span></span>

<span data-ttu-id="f00ed-105">NuGet 3.0 20 Temmuz 2015 tarihinde Visual Studio 2015 için bir paket uzantısı olarak yayımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="f00ed-105">NuGet 3.0 was released on July 20, 2015 as a bundle extension to Visual Studio 2015.</span></span> <span data-ttu-id="f00ed-106">Eksiksiz güncelleştirilmiş NuGet 3.0 deneyimi yeni Visual Studio kullanıcılar için kullanılabilir olması için bu sürüm Visual Studio ile sağlamak için gönderilir.</span><span class="sxs-lookup"><span data-stu-id="f00ed-106">We pushed to deliver this release with Visual Studio so that the complete updated NuGet 3.0 experience would be available for new Visual Studio users.</span></span> <span data-ttu-id="f00ed-107">Bu NuGet uzantısı sürüm yalnızca Visual Studio 2015 için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f00ed-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="f00ed-108">Visual Studio Galerisi güncelleştirme biz bir güncelleştirme, Windows 10 geliştirme desteği içeren Visual Studio 2015 kısa süre sonra yayımlama olarak kullanılabilir olan, en son sürüme erişimi bu geliştiriciler öneririz.</span><span class="sxs-lookup"><span data-stu-id="f00ed-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are publishing an update shortly after the release of Visual Studio 2015 that contains support for Windows 10 development.</span></span>

<span data-ttu-id="f00ed-109">Toplam 240 sorunları 3.0 sürümünde biz kapalı ve gözden geçirebilirsiniz [github'da sorunların tam listesi](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="f00ed-109">In total, we closed 240 issues in the 3.0 release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span></span>

## <a name="known-issues"></a><span data-ttu-id="f00ed-110">Bilinen Sorunlar</span><span class="sxs-lookup"><span data-stu-id="f00ed-110">Known Issues</span></span>

<span data-ttu-id="f00ed-111">Bu sürüm ile birlikte sunulan bilinen sorunlar sayısı yoktu ve bu öğelerin tümünü sürümünde Windows 10 sürümünü 29 Temmuz çakıştığı bizim zamanlanmış 3.1 düzeltilen.</span><span class="sxs-lookup"><span data-stu-id="f00ed-111">There were a number of known issues delivered with this release, and all of these items are fixed in our scheduled 3.1 release to coincide with the release of Windows 10 on July 29th.</span></span>  <span data-ttu-id="f00ed-112">Visual Studio uzantınızın ya da bu bilinen sorunları gidermek için bu tarihten sonra galerisinden güncelleştiremiyor.</span><span class="sxs-lookup"><span data-stu-id="f00ed-112">You are able to update your Visual Studio extension from the gallery on or after that date to fix these known issues.</span></span>

*  <span data-ttu-id="f00ed-113">Çeviri önizleme penceresi "bunu tekrar gösterme" etiketi ve Paket açıklaması penceresinde "Yazar" etiketi için sağlanmaz.</span><span class="sxs-lookup"><span data-stu-id="f00ed-113">Translation is not provided for the "Do not show this again" label on the preview window and the "Authors" label in the package description window.</span></span>
*  <span data-ttu-id="f00ed-114">TFS kullanarak bir proje üzerinde çalışan denetim kaynağı, Nuget.Config dosya salt okunur olarak işaretlenmiş NuGet Paket Yöneticisi kullanıcı arabirimi varsa olamaz.</span><span class="sxs-lookup"><span data-stu-id="f00ed-114">When you working on a project by using TFS source control, NuGet cannot present the package manager user interface if the Nuget.Config file is marked as read-only.</span></span>
   * <span data-ttu-id="f00ed-115">**Geçici çözüm** TFS dosyasından göz atın.</span><span class="sxs-lookup"><span data-stu-id="f00ed-115">**Workaround** Check out the file from TFS.</span></span>
*  <span data-ttu-id="f00ed-116">Visual Studio koyu tema kullandığınızda metni NuGet Powershell penceresinde "yeniden başlatma çubuğu" sarı görünür değil.</span><span class="sxs-lookup"><span data-stu-id="f00ed-116">Text in the yellow "restart bar" in the NuGet Powershell window is not visible when you use the Visual Studio dark theme.</span></span>
   * <span data-ttu-id="f00ed-117">**Geçici çözüm** Visual Studio açık tema kullanın.</span><span class="sxs-lookup"><span data-stu-id="f00ed-117">**Workaround** Use the Visual Studio light theme.</span></span>


## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="f00ed-118">Üst Sorunlar çözüldüğünde özeti</span><span class="sxs-lookup"><span data-stu-id="f00ed-118">Summary of top issues resolved</span></span>

* [<span data-ttu-id="f00ed-119">Paket Yöneticisi penceresi yenilendiğinde sık ağ güncelleştirme çağırır</span><span class="sxs-lookup"><span data-stu-id="f00ed-119">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="f00ed-120">Değiştirerek görünümü Paket Yöneticisi'nde yüklendiğinde kaydırma ertelendi</span><span class="sxs-lookup"><span data-stu-id="f00ed-120">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="f00ed-121">Ağ çağrıları arka plan iş parçacığında çalıştırılmalıdır</span><span class="sxs-lookup"><span data-stu-id="f00ed-121">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="f00ed-122">Eklenen 'önizleme penceresi gösterme' onay kutusu</span><span class="sxs-lookup"><span data-stu-id="f00ed-122">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="f00ed-123">Eklenen işlemi işlemci kullanımını azaltmak için azaltma</span><span class="sxs-lookup"><span data-stu-id="f00ed-123">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="f00ed-124">Geliştirilmiş taşınabilir sınıf kitaplığı başvurusu işleme</span><span class="sxs-lookup"><span data-stu-id="f00ed-124">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="f00ed-125">Otomatik Tamamlama hizmet büyük küçük harfe duyarlı</span><span class="sxs-lookup"><span data-stu-id="f00ed-125">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="f00ed-126">Temel kimlik doğrulama kimlik bilgilerini yeniden etkilenmesine neden güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="f00ed-126">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="f00ed-127">Geliştirilmiş hata günlüğü</span><span class="sxs-lookup"><span data-stu-id="f00ed-127">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="f00ed-128">Güncelleştirme paketi çağrılırken geliştirilmiş powershell hata iletileri</span><span class="sxs-lookup"><span data-stu-id="f00ed-128">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)
* [<span data-ttu-id="f00ed-129">Windows 10 kilitlenen önlemek için 'Seçenekleri hakkında bilgi edinin' bağlantı sabit</span><span class="sxs-lookup"><span data-stu-id="f00ed-129">Fixed the 'Learn about Options' link to prevent crashing on Windows 10</span></span>](https://github.com/NuGet/Home/issues/822)
* [<span data-ttu-id="f00ed-130">Yayın öncesi onay kutusunu ayarını unutmayın</span><span class="sxs-lookup"><span data-stu-id="f00ed-130">Remember pre-release checkbox setting</span></span>](https://github.com/NuGet/Home/issues/732)
* [<span data-ttu-id="f00ed-131">Sonuçları bir Çözümdeki projeler arasında önbelleğe alma geliştirilmiş toplama performansı</span><span class="sxs-lookup"><span data-stu-id="f00ed-131">Improved gather performance by caching results across projects in a solution</span></span>](https://github.com/NuGet/Home/issues/721)
* [<span data-ttu-id="f00ed-132">Paralel olarak birden çok paket toplanabilir</span><span class="sxs-lookup"><span data-stu-id="f00ed-132">Multiple Packages can be gathered in parallel</span></span>](https://github.com/NuGet/Home/issues/713)
* [<span data-ttu-id="f00ed-133">Install-package kaldırıldı-komutu zorla</span><span class="sxs-lookup"><span data-stu-id="f00ed-133">Removed install-package -force command</span></span>](https://github.com/NuGet/Home/issues/697)

<span data-ttu-id="f00ed-134">Lütfen takip [bizim blog](http://blog.nuget.org) daha fazla ilerleme ve duyuruları biz Windows 10 geliştirme desteği sunmaya hazır olarak.</span><span class="sxs-lookup"><span data-stu-id="f00ed-134">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements as we get ready to deliver support for Windows 10 development.</span></span>