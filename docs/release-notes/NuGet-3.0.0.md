---
title: NuGet 3,0 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 3.0.0 için sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4d4ce17c33dc38df5504a77d9cc3530d466d70af
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776550"
---
# <a name="nuget-30-release-notes"></a><span data-ttu-id="fa268-103">NuGet 3,0 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="fa268-103">NuGet 3.0 Release Notes</span></span>

<span data-ttu-id="fa268-104">[NuGet 3,0 RC2 sürüm notları](../release-notes/nuget-3.0-RC2.md)  |  [NuGet 3,1 sürüm notları](../release-notes/nuget-3.1.md)</span><span class="sxs-lookup"><span data-stu-id="fa268-104">[NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 Release Notes](../release-notes/nuget-3.1.md)</span></span>

<span data-ttu-id="fa268-105">NuGet 3,0, Visual Studio 2015 için bir paket uzantısı olarak 20 Temmuz 2015 tarihinde yayınlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="fa268-105">NuGet 3.0 was released on July 20, 2015 as a bundle extension to Visual Studio 2015.</span></span> <span data-ttu-id="fa268-106">Bu sürümü Visual Studio ile sunmaya itiyoruz, böylece tüm güncelleştirilmiş NuGet 3,0 deneyimi yeni Visual Studio kullanıcıları için kullanılabilir olacaktır.</span><span class="sxs-lookup"><span data-stu-id="fa268-106">We pushed to deliver this release with Visual Studio so that the complete updated NuGet 3.0 experience would be available for new Visual Studio users.</span></span> <span data-ttu-id="fa268-107">Bu NuGet uzantısı sürümü yalnızca Visual Studio 2015 için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="fa268-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="fa268-108">Windows 10 geliştirme desteği içeren Visual Studio 2015 yayımlandıktan hemen sonra bir güncelleştirme yayımladığımızda, Visual Studio Galerisi güncelleştirmesine erişimi olan geliştiricilerin, mevcut en son sürüme, bir güncelleştirmeyi yayımladığımız için, bu geliştiricilerin kullanılabilir en son sürüme erişimi önerilir.</span><span class="sxs-lookup"><span data-stu-id="fa268-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are publishing an update shortly after the release of Visual Studio 2015 that contains support for Windows 10 development.</span></span>

<span data-ttu-id="fa268-109">Total, 3,0 sürümündeki 240 sorunu kapattık ve [GitHub 'daki sorunların tam listesini](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed)inceleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fa268-109">In total, we closed 240 issues in the 3.0 release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span></span>

## <a name="known-issues"></a><span data-ttu-id="fa268-110">Bilinen Sorunlar</span><span class="sxs-lookup"><span data-stu-id="fa268-110">Known Issues</span></span>

<span data-ttu-id="fa268-111">Bu sürümle birlikte sunulan bazı bilinen sorunlar vardı ve bu öğelerin tümü, 29 Temmuz 'da Windows 10 ' un yayınlanmasıyla çakıştığı için zamanlanmış 3,1 sürümümüzde düzeltildi.</span><span class="sxs-lookup"><span data-stu-id="fa268-111">There were a number of known issues delivered with this release, and all of these items are fixed in our scheduled 3.1 release to coincide with the release of Windows 10 on July 29th.</span></span>  <span data-ttu-id="fa268-112">Bu bilinen sorunları çözmek için Visual Studio uzantınızı bu tarihten sonra veya sonra Galeriden güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fa268-112">You are able to update your Visual Studio extension from the gallery on or after that date to fix these known issues.</span></span>

*  <span data-ttu-id="fa268-113">"Bunu bir daha gösterme" etiketini önizleme penceresinde ve paket açıklaması penceresinde "yazarlar" etiketi için çeviri sağlanmaz.</span><span class="sxs-lookup"><span data-stu-id="fa268-113">Translation is not provided for the "Do not show this again" label on the preview window and the "Authors" label in the package description window.</span></span>
*  <span data-ttu-id="fa268-114">TFS kaynak denetimini kullanarak bir proje üzerinde çalışırken, Nuget.Config dosyası salt okunurdur olarak işaretlenmişse, NuGet Paket Yöneticisi Kullanıcı arabirimini sunamaz.</span><span class="sxs-lookup"><span data-stu-id="fa268-114">When you working on a project by using TFS source control, NuGet cannot present the package manager user interface if the Nuget.Config file is marked as read-only.</span></span>
   * <span data-ttu-id="fa268-115">**Geçici çözüm** TFS 'den dosyaya göz atın.</span><span class="sxs-lookup"><span data-stu-id="fa268-115">**Workaround** Check out the file from TFS.</span></span>
*  <span data-ttu-id="fa268-116">NuGet PowerShell penceresindeki sarı "yeniden başlatma çubuğunda" metin, Visual Studio koyu temasını kullandığınızda görünür değildir.</span><span class="sxs-lookup"><span data-stu-id="fa268-116">Text in the yellow "restart bar" in the NuGet Powershell window is not visible when you use the Visual Studio dark theme.</span></span>
   * <span data-ttu-id="fa268-117">**Geçici çözüm** Visual Studio Light temasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="fa268-117">**Workaround** Use the Visual Studio light theme.</span></span>


## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="fa268-118">Çözümlenen başlıca sorunların Özeti</span><span class="sxs-lookup"><span data-stu-id="fa268-118">Summary of top issues resolved</span></span>

* [<span data-ttu-id="fa268-119">Paket Yöneticisi penceresi yenilendiğinde sık kullanılan ağ güncelleştirme çağrıları</span><span class="sxs-lookup"><span data-stu-id="fa268-119">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="fa268-120">Paket Yöneticisi 'nde yüklü görünüme geçiş yaparken gecikmeli kaydırma</span><span class="sxs-lookup"><span data-stu-id="fa268-120">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="fa268-121">Ağ çağrıları bir arka plan iş parçacığında çalıştırılmalıdır</span><span class="sxs-lookup"><span data-stu-id="fa268-121">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="fa268-122">' Önizleme penceresini gösterme ' onay kutusu eklendi</span><span class="sxs-lookup"><span data-stu-id="fa268-122">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="fa268-123">İşlemci kullanımını azaltmak için işlem azaltma eklendi</span><span class="sxs-lookup"><span data-stu-id="fa268-123">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="fa268-124">İyileştirilmiş taşınabilir sınıf kitaplığı başvuru işleme</span><span class="sxs-lookup"><span data-stu-id="fa268-124">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="fa268-125">Otomatik tamamlama hizmeti büyük/küçük harfe duyarlıdır</span><span class="sxs-lookup"><span data-stu-id="fa268-125">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="fa268-126">Temel kimlik doğrulama kimlik bilgilerini yeniden tanıtmak için Güncelleştir</span><span class="sxs-lookup"><span data-stu-id="fa268-126">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="fa268-127">İyileştirilmiş hata günlüğü</span><span class="sxs-lookup"><span data-stu-id="fa268-127">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="fa268-128">Update-Package çağrılırken geliştirilmiş PowerShell hata iletileri</span><span class="sxs-lookup"><span data-stu-id="fa268-128">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)
* [<span data-ttu-id="fa268-129">Windows 10 ' da kilitlenme oluşmasını engellemek için ' Seçenekler hakkında bilgi edinin ' bağlantısı düzeltildi</span><span class="sxs-lookup"><span data-stu-id="fa268-129">Fixed the 'Learn about Options' link to prevent crashing on Windows 10</span></span>](https://github.com/NuGet/Home/issues/822)
* [<span data-ttu-id="fa268-130">Yayın öncesi onay kutusu ayarı</span><span class="sxs-lookup"><span data-stu-id="fa268-130">Remember pre-release checkbox setting</span></span>](https://github.com/NuGet/Home/issues/732)
* [<span data-ttu-id="fa268-131">Bir çözümdeki projeler arasında sonuçları önbelleğe alarak geliştirilmiş toplama performansı</span><span class="sxs-lookup"><span data-stu-id="fa268-131">Improved gather performance by caching results across projects in a solution</span></span>](https://github.com/NuGet/Home/issues/721)
* [<span data-ttu-id="fa268-132">Paralel olarak birden çok paket toplaneklenebilir</span><span class="sxs-lookup"><span data-stu-id="fa268-132">Multiple Packages can be gathered in parallel</span></span>](https://github.com/NuGet/Home/issues/713)
* [<span data-ttu-id="fa268-133">Install-Package-zorlama komutu kaldırıldı</span><span class="sxs-lookup"><span data-stu-id="fa268-133">Removed install-package -force command</span></span>](https://github.com/NuGet/Home/issues/697)

<span data-ttu-id="fa268-134">Windows 10 geliştirme desteği sunmaya hazırlanma konusunda daha fazla ilerleme ve duyuru için lütfen [blogumuza](http://blog.nuget.org) göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="fa268-134">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements as we get ready to deliver support for Windows 10 development.</span></span>