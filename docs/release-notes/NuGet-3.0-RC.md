---
title: NuGet 3.0 RC sürüm notları
description: NuGet 3.0 bilinen sorunları, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr RC sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0575cb1598f259a1cf1597f67123b644d67c31b5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551725"
---
# <a name="nuget-30-rc-release-notes"></a><span data-ttu-id="1d927-103">NuGet 3.0 RC sürüm notları</span><span class="sxs-lookup"><span data-stu-id="1d927-103">NuGet 3.0 RC Release Notes</span></span>

<span data-ttu-id="1d927-104">[NuGet 3.0 Beta sürüm notları](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 sürüm notları](../release-notes/nuget-3.0-RC2.md)</span><span class="sxs-lookup"><span data-stu-id="1d927-104">[NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md)</span></span>

<span data-ttu-id="1d927-105">NuGet 3.0 RC ile Visual Studio 2015 RC sürüm 29 Nisan 2015 tarihinde yayınlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="1d927-105">NuGet 3.0 RC was released on April 29, 2015 with the Visual Studio 2015 RC release.</span></span> <span data-ttu-id="1d927-106">Bu sürüm, birkaç önemli hata düzeltmeleri ve performans iyileştirmeleri yeni çerçeveleri desteklemek için güncelleştirmeleri sahiptir.</span><span class="sxs-lookup"><span data-stu-id="1d927-106">This release has a number of important bug fixes, performance improvements and updates to support the new frameworks.</span></span>  <span data-ttu-id="1d927-107">Yalnızca, Visual Studio 2015 için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1d927-107">It is only available for Visual Studio 2015.</span></span>

### <a name="continued-focus-on-performance"></a><span data-ttu-id="1d927-108">Devam eden performansa odaklanan</span><span class="sxs-lookup"><span data-stu-id="1d927-108">Continued Focus on Performance</span></span>

<span data-ttu-id="1d927-109">Kararlılık ve NuGet sorguların performansını üzerinde odaklanıyorsunuz rastladığımız devam etmektedir.</span><span class="sxs-lookup"><span data-stu-id="1d927-109">Stability and performance of NuGet queries continue to be a hot topic that we are focusing on.</span></span>  <span data-ttu-id="1d927-110">Bu sürümle birlikte, çok hızlı arama işlemleri NuGet UI ve Web sitesi görmeye başlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1d927-110">With this release, you should start to see very quick search operations in the NuGet UI and website.</span></span>  <span data-ttu-id="1d927-111">Hizmet ve biz bu işlemleri ayarlamaya devam edebilmesi için hizmet kullanımını izleme yapıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="1d927-111">We're monitoring the service and how you use the service so that we can continue to tune these operations.</span></span>

## <a name="significant-issues-resolved"></a><span data-ttu-id="1d927-112">Çözümlenen önemli sorunlar</span><span class="sxs-lookup"><span data-stu-id="1d927-112">Significant Issues Resolved</span></span>

<span data-ttu-id="1d927-113">NuGet istemcileri Sabitle için bu yayının bir parçası çok sayıda sorunu biz çözüldü.</span><span class="sxs-lookup"><span data-stu-id="1d927-113">In order to stabilize the NuGet clients, we resolved many issues as part of this release.</span></span>  <span data-ttu-id="1d927-114">Çözümlenen daha önemli sorunlar bazılarının yalnızca kısa bir listesi aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="1d927-114">Here is just a brief list of some of the more important issues resolved:</span></span>

* <span data-ttu-id="1d927-115">ASP.NET 5 K framework'ün yeniden adlandırma işleminin bir parçası olarak framework adlar dnx ve dnxcore işlemeye güncelleştirildi [bağlantı](https://github.com/NuGet/Home/issues/215)</span><span class="sxs-lookup"><span data-stu-id="1d927-115">As part of the rename of the K framework for ASP.NET 5, framework monikers have been updated to handle dnx and dnxcore [link](https://github.com/NuGet/Home/issues/215)</span></span>
* <span data-ttu-id="1d927-116">Visual Studio kullanıcı arabiriminde bağlantılardan Yardım belgeleri eklenen [bağlantı](https://github.com/NuGet/Home/issues/232)</span><span class="sxs-lookup"><span data-stu-id="1d927-116">Added help documentation from links in the Visual Studio UI [link](https://github.com/NuGet/Home/issues/232)</span></span>
* <span data-ttu-id="1d927-117">Karmaşık bir başvuru daha iyi işleme `.nuspec` virgülle ayrılmış framework başvurularıyla [bağlantı](https://github.com/NuGet/Home/issues/276)</span><span class="sxs-lookup"><span data-stu-id="1d927-117">Better handling of complex references in `.nuspec` with comma-delimited framework references [link](https://github.com/NuGet/Home/issues/276)</span></span>
* <span data-ttu-id="1d927-118">Sabit kültür Japonca desteği [bağlantı](https://github.com/NuGet/Home/issues/253)</span><span class="sxs-lookup"><span data-stu-id="1d927-118">Fixed support for Japanese cultures [link](https://github.com/NuGet/Home/issues/253)</span></span>
* <span data-ttu-id="1d927-119">ASP.NET 5 projelerine yeni v3 uç noktalarını kullanacak şekilde izin vermek için güncelleştirilmiş istemci [bağlantı](https://github.com/NuGet/Home/issues/219)</span><span class="sxs-lookup"><span data-stu-id="1d927-119">Updated client to allow ASP.NET 5 projects to use new v3 endpoints [link](https://github.com/NuGet/Home/issues/219)</span></span>
* <span data-ttu-id="1d927-120">Kaynak denetimi ile daha iyi güncelleştirilmiş tanıtıcı paketler klasörü [bağlantı](https://github.com/NuGet/Home/issues/56)</span><span class="sxs-lookup"><span data-stu-id="1d927-120">Updated to better handle packages folder with source control [link](https://github.com/NuGet/Home/issues/56)</span></span>
* <span data-ttu-id="1d927-121">Uydu paketleri için destek sabit [bağlantı](https://github.com/NuGet/Home/issues/17)</span><span class="sxs-lookup"><span data-stu-id="1d927-121">Fixed support for satellite packages [link](https://github.com/NuGet/Home/issues/17)</span></span>
* <span data-ttu-id="1d927-122">Çerçeveye özgü içerik dosyaları için desteği düzeltildi [bağlantı](https://github.com/NuGet/Home/issues/18)</span><span class="sxs-lookup"><span data-stu-id="1d927-122">Corrected support for framework-specific content files [link](https://github.com/NuGet/Home/issues/18)</span></span>

## <a name="github-presence-overhaul"></a><span data-ttu-id="1d927-123">GitHub varlığı bir revizyona imza attı</span><span class="sxs-lookup"><span data-stu-id="1d927-123">GitHub presence overhaul</span></span>

<span data-ttu-id="1d927-124">Bazı değişiklikler yaptık bizim [kaynak kod deposu github'da](http://github.com/nuget/home).</span><span class="sxs-lookup"><span data-stu-id="1d927-124">We've made some changes to our [source code repositories on GitHub](http://github.com/nuget/home).</span></span>  <span data-ttu-id="1d927-125">NuGet Visual Studio istemcisinde, Powershell komutlarını veya komut satırı ile herhangi bir sorun varsa yürütülebilir bu sorunların oturum açıp üzerinde ilerlemelerini izlemeye bizim [GitHub giriş depo sorunlar listesini](http://github.com/nuget/home/issues).</span><span class="sxs-lookup"><span data-stu-id="1d927-125">If you have any issues with the NuGet Visual Studio client, the Powershell commands, or the command-line executable you can log those issues and monitor their progress on our [GitHub Home repository issues list](http://github.com/nuget/home/issues).</span></span>  <span data-ttu-id="1d927-126">Galeride sorunlarda takip ettiğimiz bizim [GitHub NuGetGallery depo](http://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="1d927-126">We are tracking issues for the gallery in our [GitHub NuGetGallery repository](http://github.com/nuget/NuGetGallery/issues).</span></span>


## <a name="stay-tuned"></a><span data-ttu-id="1d927-127">Bizi izlemeye devam edin</span><span class="sxs-lookup"><span data-stu-id="1d927-127">Stay Tuned</span></span>

<span data-ttu-id="1d927-128">Lütfen gözünüzü [blogumuzu](http://blog.nuget.org) daha fazla ilerleme ve NuGet 3.0 duyuruları!</span><span class="sxs-lookup"><span data-stu-id="1d927-128">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>