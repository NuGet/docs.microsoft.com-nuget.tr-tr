---
title: NuGet 3.4.3 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr NuGet 3.4.3 dahil etmek için sürüm notları.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6c25d3b678e6e72eca3e1157f91a75bfa8cbb18e
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-343-release-notes"></a><span data-ttu-id="4aa07-103">NuGet 3.4.3 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="4aa07-103">NuGet 3.4.3 Release Notes</span></span>

<span data-ttu-id="4aa07-104">[NuGet 3.4.2 sürüm notları](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 sürüm notları](../release-notes/nuget-3.4.4.md)</span><span class="sxs-lookup"><span data-stu-id="4aa07-104">[NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Release Notes](../release-notes/nuget-3.4.4.md)</span></span>

<span data-ttu-id="4aa07-105">NuGet 3.4.3 22 Nisan, 3.4 ve sonraki sürümlerde belirlendi birkaç sorunlarını gidermek üzere 2016 yayımlandı.</span><span class="sxs-lookup"><span data-stu-id="4aa07-105">NuGet 3.4.3 was released on April 22, 2016 to address several issues that were identified in the 3.4 and subsequent releases.</span></span>

<span data-ttu-id="4aa07-106">VSIX ve nuget.exe indirebilirsiniz [burada](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="4aa07-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="4aa07-107">Güncelleştirmeleri ve geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="4aa07-107">Updates and Improvements</span></span>

* <span data-ttu-id="4aa07-108">Geliştirilmiş Visual Studio güvenilirlik.</span><span class="sxs-lookup"><span data-stu-id="4aa07-108">Improved Visual Studio reliability.</span></span> <span data-ttu-id="4aa07-109">Visual Studio'da kilitlenme nedeniyle NuGet biz bazı sorunlar sabit.</span><span class="sxs-lookup"><span data-stu-id="4aa07-109">We have fixed some issues in NuGet that caused crashes in Visual Studio.</span></span>

## <a name="fixes"></a><span data-ttu-id="4aa07-110">Düzeltmeler</span><span class="sxs-lookup"><span data-stu-id="4aa07-110">Fixes</span></span>

* <span data-ttu-id="4aa07-111">Bazı yetkilendirme sorunları parola korumalı özel nuget ile akışları sabit.</span><span class="sxs-lookup"><span data-stu-id="4aa07-111">Fixed some authorization issues with password protected private nuget feeds.</span></span>
* <span data-ttu-id="4aa07-112">PCL ait gelen geri yüklemek erişememe geçici bir sorun sabit `project.json` belirtilen çalışma zamanları ile.</span><span class="sxs-lookup"><span data-stu-id="4aa07-112">Fixed an issue around being unable to restore PCL's from `project.json` with runtimes specified.</span></span>
* <span data-ttu-id="4aa07-113">Bazı müşteriler, paketleri yüklerken aralıklı hatalar çalışıyordu.</span><span class="sxs-lookup"><span data-stu-id="4aa07-113">Some customers were running into intermittent failures when installing packages.</span></span> <span data-ttu-id="4aa07-114">Bu, artık bu sürümde düzeltilmiştir.</span><span class="sxs-lookup"><span data-stu-id="4aa07-114">This has now been fixed in this release.</span></span>
* <span data-ttu-id="4aa07-115">Geri yükleme hataları C + neden olan sorunu sabit +/ CLI projeleri ile `project.json`.</span><span class="sxs-lookup"><span data-stu-id="4aa07-115">Fixed an issue that caused restore failures in C++/CLI projects with `project.json`.</span></span>
* <span data-ttu-id="4aa07-116">Burada değil olan doğru nuget mono seçeneğini kullandığınızda sıkıştırması açılmış bazı paketler (örneğin ModernHttpClient).</span><span class="sxs-lookup"><span data-stu-id="4aa07-116">Some packages (E.g ModernHttpClient) where not being unzipped correctly when you use nuget in mono.</span></span> <span data-ttu-id="4aa07-117">Bu, artık bu sürümde düzeltilmiştir.</span><span class="sxs-lookup"><span data-stu-id="4aa07-117">This has now been fixed in this release.</span></span>

<span data-ttu-id="4aa07-118">Düzeltmeler ve bu sürümdeki yenilikleri tam listesi için sorunların listesini kontrol [burada](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="4aa07-118">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span></span>