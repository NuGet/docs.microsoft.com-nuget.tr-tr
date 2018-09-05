---
title: NuGet 3.4.3 sürüm notları
description: NuGet 3.4.3 dahil etmek için sürüm notları, sorunları, hata düzeltmeleri, eklenen özellikler ve dcr bilinir.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6ee4ecc06eb5119e24108d1cd6d2050254c45817
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549171"
---
# <a name="nuget-343-release-notes"></a><span data-ttu-id="d3c7a-103">NuGet 3.4.3 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="d3c7a-103">NuGet 3.4.3 Release Notes</span></span>

<span data-ttu-id="d3c7a-104">[3.4.2 NuGet sürüm notları](../release-notes/nuget-3.4.2.md) | [3.4.4 NuGet sürüm notları](../release-notes/nuget-3.4.4.md)</span><span class="sxs-lookup"><span data-stu-id="d3c7a-104">[NuGet 3.4.2 Release Notes](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4 Release Notes](../release-notes/nuget-3.4.4.md)</span></span>

<span data-ttu-id="d3c7a-105">NuGet 3.4.3 22 Nisan 3.4 ve sonraki sürümlerde tanımlanmış olan çeşitli sorunları ele almak için 2016 yayınlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="d3c7a-105">NuGet 3.4.3 was released on April 22, 2016 to address several issues that were identified in the 3.4 and subsequent releases.</span></span>

<span data-ttu-id="d3c7a-106">VSIX ve nuget.exe indirebileceğiniz [burada](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="d3c7a-106">You can download both the VSIX and nuget.exe [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="d3c7a-107">Güncelleştirmeler ve iyileştirmeler</span><span class="sxs-lookup"><span data-stu-id="d3c7a-107">Updates and Improvements</span></span>

* <span data-ttu-id="d3c7a-108">Visual Studio güvenilirlik düzeyi artırıldı.</span><span class="sxs-lookup"><span data-stu-id="d3c7a-108">Improved Visual Studio reliability.</span></span> <span data-ttu-id="d3c7a-109">Visual Studio'da kilitlenmelere neden nuget'te bazı sorunları düzelttik.</span><span class="sxs-lookup"><span data-stu-id="d3c7a-109">We have fixed some issues in NuGet that caused crashes in Visual Studio.</span></span>

## <a name="fixes"></a><span data-ttu-id="d3c7a-110">Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="d3c7a-110">Fixes</span></span>

* <span data-ttu-id="d3c7a-111">Bazı yetkilendirme sorunları ile parola korumalı özel nuget akışları düzeltildi.</span><span class="sxs-lookup"><span data-stu-id="d3c7a-111">Fixed some authorization issues with password protected private nuget feeds.</span></span>
* <span data-ttu-id="d3c7a-112">PCL'ın gelen geri erişememe geçici bir sorun düzeltildi `project.json` belirtilen çalışma zamanları ile.</span><span class="sxs-lookup"><span data-stu-id="d3c7a-112">Fixed an issue around being unable to restore PCL's from `project.json` with runtimes specified.</span></span>
* <span data-ttu-id="d3c7a-113">Bazı müşteriler, paketleri yüklerken aralıklı hatalar çalışıyordu.</span><span class="sxs-lookup"><span data-stu-id="d3c7a-113">Some customers were running into intermittent failures when installing packages.</span></span> <span data-ttu-id="d3c7a-114">Bu, bu sürümde artık düzeltildi.</span><span class="sxs-lookup"><span data-stu-id="d3c7a-114">This has now been fixed in this release.</span></span>
* <span data-ttu-id="d3c7a-115">Geri yükleme hatalarının C + kaynaklanan bir sorun düzeltildi +/ CLI projeleri ile `project.json`.</span><span class="sxs-lookup"><span data-stu-id="d3c7a-115">Fixed an issue that caused restore failures in C++/CLI projects with `project.json`.</span></span>
* <span data-ttu-id="d3c7a-116">Burada değil olan doğru mono'da nuget kullanırken sıkıştırması açılan bazı paketler (ör. ModernHttpClient).</span><span class="sxs-lookup"><span data-stu-id="d3c7a-116">Some packages (E.g ModernHttpClient) where not being unzipped correctly when you use nuget in mono.</span></span> <span data-ttu-id="d3c7a-117">Bu, bu sürümde artık düzeltildi.</span><span class="sxs-lookup"><span data-stu-id="d3c7a-117">This has now been fixed in this release.</span></span>

<span data-ttu-id="d3c7a-118">Düzeltmeleri ve geliştirmeleri bu sürümde tam listesi için sorunların listeye bir göz atın [burada](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="d3c7a-118">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).</span></span>