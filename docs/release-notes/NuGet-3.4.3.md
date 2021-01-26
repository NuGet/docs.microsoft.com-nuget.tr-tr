---
title: NuGet 3.4.3 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 3.4.3 için sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f0d9740aaf0a82b9e4023b5e4990c8f4adbea63c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776473"
---
# <a name="nuget-343-release-notes"></a><span data-ttu-id="177b8-103">NuGet 3.4.3 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="177b8-103">NuGet 3.4.3 Release Notes</span></span>

<span data-ttu-id="177b8-104">[NuGet 3.4.2 sürüm notları](../release-notes/nuget-3.4.2.md)  |  [NuGet 3.4.4 sürüm notları](../release-notes/nuget-3.4.4.md)</span><span class="sxs-lookup"><span data-stu-id="177b8-104">[NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Release Notes](../release-notes/nuget-3.4.4.md)</span></span>

<span data-ttu-id="177b8-105">NuGet 3.4.3, 3,4 Nisan 2016 ' de, ve sonraki sürümlerde tanımlanmış birçok sorunu gidermek için yayımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="177b8-105">NuGet 3.4.3 was released on April 22, 2016 to address several issues that were identified in the 3.4 and subsequent releases.</span></span>

<span data-ttu-id="177b8-106">Hem VSıX hem [de nuget.exe yükleyebilirsiniz](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="177b8-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="177b8-107">Güncelleştirmeler ve geliştirmeler</span><span class="sxs-lookup"><span data-stu-id="177b8-107">Updates and Improvements</span></span>

* <span data-ttu-id="177b8-108">Geliştirilmiş Visual Studio güvenilirliği.</span><span class="sxs-lookup"><span data-stu-id="177b8-108">Improved Visual Studio reliability.</span></span> <span data-ttu-id="177b8-109">NuGet 'de Visual Studio 'da kilitlenmelere neden olan bazı sorunlar düzeltildi.</span><span class="sxs-lookup"><span data-stu-id="177b8-109">We have fixed some issues in NuGet that caused crashes in Visual Studio.</span></span>

## <a name="fixes"></a><span data-ttu-id="177b8-110">Düzeltmeler</span><span class="sxs-lookup"><span data-stu-id="177b8-110">Fixes</span></span>

* <span data-ttu-id="177b8-111">Parola korumalı özel NuGet akışlarıyla bazı yetkilendirme sorunları düzeltildi.</span><span class="sxs-lookup"><span data-stu-id="177b8-111">Fixed some authorization issues with password protected private nuget feeds.</span></span>
* <span data-ttu-id="177b8-112">PCL 'in `project.json` belirtilen çalışma zamanları ile birlikte geri yükleme sorunu düzeltildi.</span><span class="sxs-lookup"><span data-stu-id="177b8-112">Fixed an issue around being unable to restore PCL's from `project.json` with runtimes specified.</span></span>
* <span data-ttu-id="177b8-113">Bazı müşteriler, paket yüklenirken aralıklı hatalara karşı çalışmaktadır.</span><span class="sxs-lookup"><span data-stu-id="177b8-113">Some customers were running into intermittent failures when installing packages.</span></span> <span data-ttu-id="177b8-114">Bu, şimdi bu sürümde düzeltildi.</span><span class="sxs-lookup"><span data-stu-id="177b8-114">This has now been fixed in this release.</span></span>
* <span data-ttu-id="177b8-115">C++/CLı projelerinde ile geri yükleme hatalarının oluşmasına neden olan bir sorun düzeltildi `project.json` .</span><span class="sxs-lookup"><span data-stu-id="177b8-115">Fixed an issue that caused restore failures in C++/CLI projects with `project.json`.</span></span>
* <span data-ttu-id="177b8-116">Mono 'da NuGet kullandığınızda bazı paketler (ör. ModernHttpClient), sıkıştırılmayan bir biçimde.</span><span class="sxs-lookup"><span data-stu-id="177b8-116">Some packages (E.g ModernHttpClient) where not being unzipped correctly when you use nuget in mono.</span></span> <span data-ttu-id="177b8-117">Bu, şimdi bu sürümde düzeltildi.</span><span class="sxs-lookup"><span data-stu-id="177b8-117">This has now been fixed in this release.</span></span>

<span data-ttu-id="177b8-118">Bu sürümdeki düzeltmelerin ve geliştirmelerin tüm listesi için [buradaki](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed)sorun listesini inceleyin.</span><span class="sxs-lookup"><span data-stu-id="177b8-118">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span></span>