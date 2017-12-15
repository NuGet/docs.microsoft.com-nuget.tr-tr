---
title: "NuGet 3.0 RC sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: cd0c102f-bc33-4aa2-a921-61fa21d42b28
description: "NuGet 3.0 bilinen sorunları, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere RC sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 3.0 RC sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5d0eeae479617bc30901b599251628f72950cc67
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-30-rc-release-notes"></a><span data-ttu-id="ea1d5-104">NuGet 3.0 RC sürüm notları</span><span class="sxs-lookup"><span data-stu-id="ea1d5-104">NuGet 3.0 RC Release Notes</span></span>

<span data-ttu-id="ea1d5-105">[NuGet 3.0 Beta sürüm notları](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 sürüm notları](../release-notes/nuget-3.0-RC2.md)</span><span class="sxs-lookup"><span data-stu-id="ea1d5-105">[NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md)</span></span>

<span data-ttu-id="ea1d5-106">NuGet 3.0 RC 29 Nisan 2015 tarihinde Visual Studio 2015 RC sürüm ile serbest bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="ea1d5-106">NuGet 3.0 RC was released on April 29, 2015 with the Visual Studio 2015 RC release.</span></span> <span data-ttu-id="ea1d5-107">Bu sürüm çeşitli önemli hata düzeltmeleri, performans iyileştirmeleri ve yeni çerçeveleri desteklemek için güncelleştirmeleri vardır.</span><span class="sxs-lookup"><span data-stu-id="ea1d5-107">This release has a number of important bug fixes, performance improvements and updates to support the new frameworks.</span></span>  <span data-ttu-id="ea1d5-108">Yalnızca, Visual Studio 2015 için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ea1d5-108">It is only available for Visual Studio 2015.</span></span>

### <a name="continued-focus-on-performance"></a><span data-ttu-id="ea1d5-109">Devam eden odak performansı</span><span class="sxs-lookup"><span data-stu-id="ea1d5-109">Continued Focus on Performance</span></span>

<span data-ttu-id="ea1d5-110">Kararlılık ve performans NuGet sorguların biz üzerine odaklanan bir konudur devam etmektedir.</span><span class="sxs-lookup"><span data-stu-id="ea1d5-110">Stability and performance of NuGet queries continue to be a hot topic that we are focusing on.</span></span>  <span data-ttu-id="ea1d5-111">Bu sürümle birlikte, NuGet kullanıcı Arabirimi ve Web sitesi çok hızlı arama işlemlerinin görmeye başlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea1d5-111">With this release, you should start to see very quick search operations in the NuGet UI and website.</span></span>  <span data-ttu-id="ea1d5-112">Hizmet ve biz bu işlemlerin ayarlamaya devam edebilmesi için bu hizmetin kullanımı izleme.</span><span class="sxs-lookup"><span data-stu-id="ea1d5-112">We're monitoring the service and how you use the service so that we can continue to tune these operations.</span></span>

## <a name="significant-issues-resolved"></a><span data-ttu-id="ea1d5-113">Önemli sorunlar çözüldüğünde</span><span class="sxs-lookup"><span data-stu-id="ea1d5-113">Significant Issues Resolved</span></span>

<span data-ttu-id="ea1d5-114">NuGet istemcileri Sabitle için bu sürümde bir parçası olarak çoğu sorunu biz çözümlendi.</span><span class="sxs-lookup"><span data-stu-id="ea1d5-114">In order to stabilize the NuGet clients, we resolved many issues as part of this release.</span></span>  <span data-ttu-id="ea1d5-115">Aşağıda, daha önemli sorunlar çözüldüğünde bazılarının yalnızca kısa bir listesi verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="ea1d5-115">Here is just a brief list of some of the more important issues resolved:</span></span>

* <span data-ttu-id="ea1d5-116">ASP.NET 5 K framework'ün yeniden adlandırma işleminin bir parçası olarak, framework adlar dnx ve dnxcore işlemek için güncelleştirilmiş [bağlantı](https://github.com/NuGet/Home/issues/215)</span><span class="sxs-lookup"><span data-stu-id="ea1d5-116">As part of the rename of the K framework for ASP.NET 5, framework monikers have been updated to handle dnx and dnxcore [link](https://github.com/NuGet/Home/issues/215)</span></span>
* <span data-ttu-id="ea1d5-117">Visual Studio kullanıcı arabiriminde bağlantılardan Yardım belgelerine eklenen [bağlantı](https://github.com/NuGet/Home/issues/232)</span><span class="sxs-lookup"><span data-stu-id="ea1d5-117">Added help documentation from links in the Visual Studio UI [link](https://github.com/NuGet/Home/issues/232)</span></span>
* <span data-ttu-id="ea1d5-118">Karmaşık başvurularında, daha iyi işleme `.nuspec` virgülle ayrılmış framework başvurularıyla [bağlantı](https://github.com/NuGet/Home/issues/276)</span><span class="sxs-lookup"><span data-stu-id="ea1d5-118">Better handling of complex references in `.nuspec` with comma-delimited framework references [link](https://github.com/NuGet/Home/issues/276)</span></span>
* <span data-ttu-id="ea1d5-119">Japonca kültürler için destek sabit [bağlantı](https://github.com/NuGet/Home/issues/253)</span><span class="sxs-lookup"><span data-stu-id="ea1d5-119">Fixed support for Japanese cultures [link](https://github.com/NuGet/Home/issues/253)</span></span>
* <span data-ttu-id="ea1d5-120">Yeni v3 uç nokta kullanmak ASP.NET 5 projeleri izin vermek için güncelleştirilmiş istemci [bağlantı](https://github.com/NuGet/Home/issues/219)</span><span class="sxs-lookup"><span data-stu-id="ea1d5-120">Updated client to allow ASP.NET 5 projects to use new v3 endpoints [link](https://github.com/NuGet/Home/issues/219)</span></span>
* <span data-ttu-id="ea1d5-121">Kaynak denetimi ile daha iyi güncelleştirilmiş tanıtıcı paketler klasörü [bağlantı](https://github.com/NuGet/Home/issues/56)</span><span class="sxs-lookup"><span data-stu-id="ea1d5-121">Updated to better handle packages folder with source control [link](https://github.com/NuGet/Home/issues/56)</span></span>
* <span data-ttu-id="ea1d5-122">Uydu paketleri için destek sabit [bağlantı](https://github.com/NuGet/Home/issues/17)</span><span class="sxs-lookup"><span data-stu-id="ea1d5-122">Fixed support for satellite packages [link](https://github.com/NuGet/Home/issues/17)</span></span>
* <span data-ttu-id="ea1d5-123">Çerçeveye özel içerik dosyaları için destek düzeltildi [bağlantı](https://github.com/NuGet/Home/issues/18)</span><span class="sxs-lookup"><span data-stu-id="ea1d5-123">Corrected support for framework-specific content files [link](https://github.com/NuGet/Home/issues/18)</span></span>

## <a name="github-presence-overhaul"></a><span data-ttu-id="ea1d5-124">GitHub varlığı onarımı</span><span class="sxs-lookup"><span data-stu-id="ea1d5-124">GitHub presence overhaul</span></span>

<span data-ttu-id="ea1d5-125">Bazı değişiklikler yaptık bizim [kaynak kodu depolarına github'da](http://github.com/nuget/home).</span><span class="sxs-lookup"><span data-stu-id="ea1d5-125">We've made some changes to our [source code repositories on GitHub](http://github.com/nuget/home).</span></span>  <span data-ttu-id="ea1d5-126">NuGet Visual Studio istemcisi, Powershell komutlarını veya komut satırı ile ilgili sorununuz olursa yürütülebilir, bu sorunları oturum ve üzerinde kendi ilerleme durumunu izlemek bizim [GitHub giriş depo sorunlar listesine](http://github.com/nuget/home/issues).</span><span class="sxs-lookup"><span data-stu-id="ea1d5-126">If you have any issues with the NuGet Visual Studio client, the Powershell commands, or the command-line executable you can log those issues and monitor their progress on our [GitHub Home repository issues list](http://github.com/nuget/home/issues).</span></span>  <span data-ttu-id="ea1d5-127">Galeride sorunlarda takip ettiğimiz bizim [GitHub NuGetGallery depo](http://github.com/nuget/NuGetGallery/issues).</span><span class="sxs-lookup"><span data-stu-id="ea1d5-127">We are tracking issues for the gallery in our [GitHub NuGetGallery repository](http://github.com/nuget/NuGetGallery/issues).</span></span>


## <a name="stay-tuned"></a><span data-ttu-id="ea1d5-128">Bizi izlemeye devam edin</span><span class="sxs-lookup"><span data-stu-id="ea1d5-128">Stay Tuned</span></span>

<span data-ttu-id="ea1d5-129">Lütfen takip [bizim blog](http://blog.nuget.org) daha fazla ilerleme ve duyuruları NuGet 3.0 için!</span><span class="sxs-lookup"><span data-stu-id="ea1d5-129">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>