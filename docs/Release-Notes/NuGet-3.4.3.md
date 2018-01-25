---
title: "NuGet 3.4.3 sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr NuGet 3.4.3 dahil etmek için sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 3.4.3 sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 68aab607659d15f96aefeab7bb90afc787710824
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-343-release-notes"></a><span data-ttu-id="b1132-104">NuGet 3.4.3 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="b1132-104">NuGet 3.4.3 Release Notes</span></span>

<span data-ttu-id="b1132-105">[NuGet 3.4.2 sürüm notları](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 sürüm notları](../release-notes/nuget-3.4.4.md)</span><span class="sxs-lookup"><span data-stu-id="b1132-105">[NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Release Notes](../release-notes/nuget-3.4.4.md)</span></span>

<span data-ttu-id="b1132-106">NuGet 3.4.3 22 Nisan, 3.4 ve sonraki sürümlerde belirlendi birkaç sorunlarını gidermek üzere 2016 yayımlandı.</span><span class="sxs-lookup"><span data-stu-id="b1132-106">NuGet 3.4.3 was released on April 22, 2016 to address several issues that were identified in the 3.4 and subsequent releases.</span></span>

<span data-ttu-id="b1132-107">VSIX ve nuget.exe indirebilirsiniz [burada](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="b1132-107">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="b1132-108">Güncelleştirmeleri ve geliştirmeleri</span><span class="sxs-lookup"><span data-stu-id="b1132-108">Updates and Improvements</span></span>

* <span data-ttu-id="b1132-109">Geliştirilmiş Visual Studio güvenilirlik.</span><span class="sxs-lookup"><span data-stu-id="b1132-109">Improved Visual Studio reliability.</span></span> <span data-ttu-id="b1132-110">Visual Studio'da kilitlenme nedeniyle NuGet biz bazı sorunlar sabit.</span><span class="sxs-lookup"><span data-stu-id="b1132-110">We have fixed some issues in NuGet that caused crashes in Visual Studio.</span></span>

## <a name="fixes"></a><span data-ttu-id="b1132-111">Düzeltmeler</span><span class="sxs-lookup"><span data-stu-id="b1132-111">Fixes</span></span>

* <span data-ttu-id="b1132-112">Bazı yetkilendirme sorunları parola korumalı özel nuget ile akışları sabit.</span><span class="sxs-lookup"><span data-stu-id="b1132-112">Fixed some authorization issues with password protected private nuget feeds.</span></span>
* <span data-ttu-id="b1132-113">PCL ait gelen geri yüklemek erişememe geçici bir sorun sabit `project.json` belirtilen çalışma zamanları ile.</span><span class="sxs-lookup"><span data-stu-id="b1132-113">Fixed an issue around being unable to restore PCL's from `project.json` with runtimes specified.</span></span>
* <span data-ttu-id="b1132-114">Bazı müşteriler, paketleri yüklerken aralıklı hatalar çalışıyordu.</span><span class="sxs-lookup"><span data-stu-id="b1132-114">Some customers were running into intermittent failures when installing packages.</span></span> <span data-ttu-id="b1132-115">Bu, artık bu sürümde düzeltilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b1132-115">This has now been fixed in this release.</span></span>
* <span data-ttu-id="b1132-116">Geri yükleme hataları C + neden olan sorunu sabit +/ CLI projeleri ile `project.json`.</span><span class="sxs-lookup"><span data-stu-id="b1132-116">Fixed an issue that caused restore failures in C++/CLI projects with `project.json`.</span></span>
* <span data-ttu-id="b1132-117">Burada değil olan doğru nuget mono seçeneğini kullandığınızda sıkıştırması açılmış bazı paketler (örneğin ModernHttpClient).</span><span class="sxs-lookup"><span data-stu-id="b1132-117">Some packages (E.g ModernHttpClient) where not being unzipped correctly when you use nuget in mono.</span></span> <span data-ttu-id="b1132-118">Bu, artık bu sürümde düzeltilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b1132-118">This has now been fixed in this release.</span></span>

<span data-ttu-id="b1132-119">Düzeltmeler ve bu sürümdeki yenilikleri tam listesi için sorunların listesini kontrol [burada](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="b1132-119">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span></span>