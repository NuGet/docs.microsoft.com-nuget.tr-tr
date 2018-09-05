---
title: NuGet 3.0 sürüm notları
description: NuGet 3.0.0 dahil etmek için sürüm notları, sorunları, hata düzeltmeleri, eklenen özellikler ve dcr bilinir.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1ade2b5b5ff7d57d756829c1c1853b5573c17d6d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551869"
---
# <a name="nuget-30-release-notes"></a><span data-ttu-id="9794d-103">NuGet 3.0 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="9794d-103">NuGet 3.0 Release Notes</span></span>

<span data-ttu-id="9794d-104">[NuGet 3.0 RC2 sürüm notları](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 sürüm notları](../release-notes/nuget-3.1.md)</span><span class="sxs-lookup"><span data-stu-id="9794d-104">[NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 Release Notes](../release-notes/nuget-3.1.md)</span></span>

<span data-ttu-id="9794d-105">NuGet 3.0, Visual Studio 2015 için bir paket uzantısı olarak 20 Temmuz 2015 tarihinde yayınlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="9794d-105">NuGet 3.0 was released on July 20, 2015 as a bundle extension to Visual Studio 2015.</span></span> <span data-ttu-id="9794d-106">Bu sürüm Visual Studio ile böylece eksiksiz güncelleştirilmiş NuGet 3.0 deneyimi yeni Visual Studio kullanıcıların kullanımına sunmak için gönderildi.</span><span class="sxs-lookup"><span data-stu-id="9794d-106">We pushed to deliver this release with Visual Studio so that the complete updated NuGet 3.0 experience would be available for new Visual Studio users.</span></span> <span data-ttu-id="9794d-107">Bu NuGet uzantısı sürüm, yalnızca Visual Studio 2015 için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="9794d-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="9794d-108">Biz güncelleştirilmiş Windows 10 için geliştirme desteği içeren Visual Studio 2015'in kısa süre sonra yayımlama gibi kullanılabilir en son sürümü için Visual Studio Galerisi Update'e erişecek bu geliştiriciler öneririz.</span><span class="sxs-lookup"><span data-stu-id="9794d-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are publishing an update shortly after the release of Visual Studio 2015 that contains support for Windows 10 development.</span></span>

<span data-ttu-id="9794d-109">Toplam 240 sorunları 3.0 sürümündeki biz kapalı ve gözden geçirebilirsiniz [github'da sorunların tam listesi](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="9794d-109">In total, we closed 240 issues in the 3.0 release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span></span>

## <a name="known-issues"></a><span data-ttu-id="9794d-110">Bilinen Sorunlar</span><span class="sxs-lookup"><span data-stu-id="9794d-110">Known Issues</span></span>

<span data-ttu-id="9794d-111">Bu sürümle birlikte sunulan bilinen sorunlara ilişkin birkaç vardı ve bu öğelerin tümünü Windows 10'ın yayınlanmasıyla birlikte 29 Temmuz tarihinde başlayacak şekilde zamanlanmış 3.1 sürümümüzü giderilen.</span><span class="sxs-lookup"><span data-stu-id="9794d-111">There were a number of known issues delivered with this release, and all of these items are fixed in our scheduled 3.1 release to coincide with the release of Windows 10 on July 29th.</span></span>  <span data-ttu-id="9794d-112">Bu bilinen sorunları düzeltmek için bu tarihte veya daha sonra Galerisi, Visual Studio uzantısı güncelleştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="9794d-112">You are able to update your Visual Studio extension from the gallery on or after that date to fix these known issues.</span></span>

*  <span data-ttu-id="9794d-113">Önizleme penceresini "bunu bir daha gösterme" etiketi ve Paket açıklaması penceresinde "Yazar" etiketi için çeviri sağlanmadı.</span><span class="sxs-lookup"><span data-stu-id="9794d-113">Translation is not provided for the "Do not show this again" label on the preview window and the "Authors" label in the package description window.</span></span>
*  <span data-ttu-id="9794d-114">TFS kullanarak bir proje üzerinde çalışan, kaynak denetimi, Nuget.Config dosyası salt okunur olarak işaretlenmişse NuGet Paket Yöneticisi kullanıcı arabirimi var olamaz.</span><span class="sxs-lookup"><span data-stu-id="9794d-114">When you working on a project by using TFS source control, NuGet cannot present the package manager user interface if the Nuget.Config file is marked as read-only.</span></span>
   * <span data-ttu-id="9794d-115">**Geçici çözüm** TFS dosyasından göz atın.</span><span class="sxs-lookup"><span data-stu-id="9794d-115">**Workaround** Check out the file from TFS.</span></span>
*  <span data-ttu-id="9794d-116">Visual Studio koyu tema kullandığınızda, "yeniden başlatma çubuğu" NuGet Powershell penceresinde sarı metinde görünür değil.</span><span class="sxs-lookup"><span data-stu-id="9794d-116">Text in the yellow "restart bar" in the NuGet Powershell window is not visible when you use the Visual Studio dark theme.</span></span>
   * <span data-ttu-id="9794d-117">**Geçici çözüm** Visual Studio açık tema kullanın.</span><span class="sxs-lookup"><span data-stu-id="9794d-117">**Workaround** Use the Visual Studio light theme.</span></span>


## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="9794d-118">Çözümlenen üst sorunların özeti</span><span class="sxs-lookup"><span data-stu-id="9794d-118">Summary of top issues resolved</span></span>

* [<span data-ttu-id="9794d-119">Paket Yöneticisi penceresini yenilediğinde ağ sık sık güncelleştirme çağırır.</span><span class="sxs-lookup"><span data-stu-id="9794d-119">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="9794d-120">Kaydırma değiştirerek görünümü Paket Yöneticisi'nde yüklendiğinde Gecikmeli</span><span class="sxs-lookup"><span data-stu-id="9794d-120">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="9794d-121">Ağ çağrıları arka plan iş parçacığında çalıştırılmalıdır</span><span class="sxs-lookup"><span data-stu-id="9794d-121">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="9794d-122">Eklenen 'Önizleme penceresini gösterme' onay kutusu</span><span class="sxs-lookup"><span data-stu-id="9794d-122">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="9794d-123">Ek işlem işlemci kullanımını azaltmak için azaltma</span><span class="sxs-lookup"><span data-stu-id="9794d-123">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="9794d-124">Geliştirilmiş işleme taşınabilir sınıf kitaplığı başvurusu</span><span class="sxs-lookup"><span data-stu-id="9794d-124">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="9794d-125">Otomatik Tamamlama hizmeti büyük küçük harfe duyarlı</span><span class="sxs-lookup"><span data-stu-id="9794d-125">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="9794d-126">Temel kimlik doğrulama kimlik bilgileri güçlendirebilir güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="9794d-126">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="9794d-127">Geliştirilmiş hata günlüğü</span><span class="sxs-lookup"><span data-stu-id="9794d-127">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="9794d-128">Update-Package çağırırken powershell geliştirilmiş hata iletileri</span><span class="sxs-lookup"><span data-stu-id="9794d-128">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)
* [<span data-ttu-id="9794d-129">Windows 10'da kilitlenen önlemek için 'Seçenekleri hakkında bilgi edinin' bağlantıyı düzeltildi</span><span class="sxs-lookup"><span data-stu-id="9794d-129">Fixed the 'Learn about Options' link to prevent crashing on Windows 10</span></span>](https://github.com/NuGet/Home/issues/822)
* [<span data-ttu-id="9794d-130">Yayın öncesi onay kutusunu ayarını unutmayın</span><span class="sxs-lookup"><span data-stu-id="9794d-130">Remember pre-release checkbox setting</span></span>](https://github.com/NuGet/Home/issues/732)
* [<span data-ttu-id="9794d-131">Bir Çözümdeki projeler arasında sonuçları önbelleğe alma geliştirilmiş toplama performansı</span><span class="sxs-lookup"><span data-stu-id="9794d-131">Improved gather performance by caching results across projects in a solution</span></span>](https://github.com/NuGet/Home/issues/721)
* [<span data-ttu-id="9794d-132">Paralel olarak birden çok paket toplanabilir</span><span class="sxs-lookup"><span data-stu-id="9794d-132">Multiple Packages can be gathered in parallel</span></span>](https://github.com/NuGet/Home/issues/713)
* [<span data-ttu-id="9794d-133">Install-package kaldırıldı-komut zorla</span><span class="sxs-lookup"><span data-stu-id="9794d-133">Removed install-package -force command</span></span>](https://github.com/NuGet/Home/issues/697)

<span data-ttu-id="9794d-134">Lütfen gözünüzü [blogumuzu](http://blog.nuget.org) daha fazla ilerleme ve duyuruları biz Windows 10 için geliştirme için destek sunmaya hazır olarak.</span><span class="sxs-lookup"><span data-stu-id="9794d-134">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements as we get ready to deliver support for Windows 10 development.</span></span>