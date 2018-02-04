---
title: "NuGet 2.8.6 sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 920c551c-18a7-40f4-a32b-ce84de6ea766
description: "Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr NuGet 2.8.6 dahil etmek için sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 2.8.6 sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4dfd0a76967280cc6a16b37fe2b2a3362231fce5
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-286-release-notes"></a><span data-ttu-id="cdc3f-104">NuGet 2.8.6 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="cdc3f-104">NuGet 2.8.6 Release Notes</span></span>

<span data-ttu-id="cdc3f-105">[NuGet 2.8.5 sürüm notları](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Sürüm Notları](../release-notes/nuget-2.8.7.md)</span><span class="sxs-lookup"><span data-stu-id="cdc3f-105">[NuGet 2.8.5 Release Notes](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md)</span></span>

<span data-ttu-id="cdc3f-106">NuGet 2.8.6 yayımlanan 20 Temmuz 2015 bizim 2.8.5 için ikincil bir güncelleştirme olarak bazı VSIX hedeflenen düzeltmeler ve iyileştirmeler Windows 10 UWP geliştirme modeli desteğiyle teslim edilebilir paketleri destekler.</span><span class="sxs-lookup"><span data-stu-id="cdc3f-106">NuGet 2.8.6 was released July 20, 2015 as a minor update to our 2.8.5 VSIX with some targeted fixes and improvements to support packages that may be delivered with support for the Windows 10 UWP development model.</span></span>

<span data-ttu-id="cdc3f-107">NuGet Paket Yöneticisi uzantısı'nın bu sürümü yalnızca Visual Studio 2013 için destek sağlar.</span><span class="sxs-lookup"><span data-stu-id="cdc3f-107">This version of the NuGet package manager extension provides support for Visual Studio 2013 only.</span></span>

<span data-ttu-id="cdc3f-108">Bu sürümde, NuGet Paket Yöneticisi iletişim için eklenen destek vardı:</span><span class="sxs-lookup"><span data-stu-id="cdc3f-108">In this release, the NuGet Package Manager dialog had support added for:</span></span>

* <span data-ttu-id="cdc3f-109">Windows 10 uygulaması geliştirme desteklemek için UAP hedef Framework ad kullanıma sunuldu.</span><span class="sxs-lookup"><span data-stu-id="cdc3f-109">Introduced the UAP Target Framework Moniker to support Windows 10 Application Development.</span></span>
* <span data-ttu-id="cdc3f-110">NuGet Protokolü sürüm 3 uç noktaları</span><span class="sxs-lookup"><span data-stu-id="cdc3f-110">NuGet protocol version 3 endpoints</span></span>
* <span data-ttu-id="cdc3f-111">Desteği [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) depo kaynakları protocolVersion özniteliği.</span><span class="sxs-lookup"><span data-stu-id="cdc3f-111">Support for [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion attribute on repository sources.</span></span> <span data-ttu-id="cdc3f-112">Varsayılan değer "2".</span><span class="sxs-lookup"><span data-stu-id="cdc3f-112">Default value is "2"</span></span>
* <span data-ttu-id="cdc3f-113">Gerekli Paket sürümü yerel önbellekte kullanılabilir değilse, uzak depoya geri dönmeden</span><span class="sxs-lookup"><span data-stu-id="cdc3f-113">Falling back to remote repository if a required package version is not available in the local cache</span></span>