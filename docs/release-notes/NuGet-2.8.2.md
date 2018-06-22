---
title: NuGet 2.8.2 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr NuGet 2.8.2 dahil etmek için sürüm notları.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a004c250d60a4ed1ca8dede1e83b2a68e10299bf
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31821336"
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="5ac0d-103">NuGet 2.8.2 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="5ac0d-103">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="5ac0d-104">[NuGet 2.8.1 ile sürüm notları](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 sürüm notları](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="5ac0d-104">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="5ac0d-105">NuGet 2.8.2 22 Mayıs 2014'te yayımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="5ac0d-105">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="5ac0d-106">Bu sürüm yalnızca komut satırı nuget.exe, NuGet.Server paket ve diğer NuGet paketleri yapılan değişiklikler dahil.</span><span class="sxs-lookup"><span data-stu-id="5ac0d-106">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="5ac0d-107">Yayın güncelleştirilmiş Visual Studio uzantısı veya WebMatrix genişletmesi içermiyordu.</span><span class="sxs-lookup"><span data-stu-id="5ac0d-107">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="5ac0d-108">Önemli güncelleştirmeleri</span><span class="sxs-lookup"><span data-stu-id="5ac0d-108">Notable Updates</span></span>

<span data-ttu-id="5ac0d-109">Komut satırı nuget.exe ve NuGet.Server paket (kendi kendini barındıran NuGet akışlarını için) en önemli güncelleştirmeleri yoktu.</span><span class="sxs-lookup"><span data-stu-id="5ac0d-109">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="5ac0d-110">Önemli nuget.exe hata düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="5ac0d-110">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="5ac0d-111">nuget.exe gönderme başarısız olur ve yeniden deneniyor tutar</span><span class="sxs-lookup"><span data-stu-id="5ac0d-111">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="5ac0d-112">nuget.exe itme temel kimlik doğrulama kimlik bilgileri doğru biçimde göndermez</span><span class="sxs-lookup"><span data-stu-id="5ac0d-112">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="5ac0d-113">nuget.exe itme geçici yeniden yönlendirme izleyin olmaz</span><span class="sxs-lookup"><span data-stu-id="5ac0d-113">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="5ac0d-114">Önemli NuGet.Server hata düzeltmesi</span><span class="sxs-lookup"><span data-stu-id="5ac0d-114">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="5ac0d-115">NuGet.Server tarafından döndürülen IsAbsoluteLatestVersion yanlış değeri</span><span class="sxs-lookup"><span data-stu-id="5ac0d-115">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="5ac0d-116">Güncelleştirme paketleri</span><span class="sxs-lookup"><span data-stu-id="5ac0d-116">Packages Updated</span></span>

<span data-ttu-id="5ac0d-117">NuGet.Server düzeltmeler ve komut satırı nuget.exe NuGet paketi güncelleştirme gönderilir.</span><span class="sxs-lookup"><span data-stu-id="5ac0d-117">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="5ac0d-118">Diğer paketleri de 2.8.2 ile güncelleştirilmiş vardı.</span><span class="sxs-lookup"><span data-stu-id="5ac0d-118">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="5ac0d-119">Güncelleştirilmiş paketleri listesi aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="5ac0d-119">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="5ac0d-120">NuGet.Core</span><span class="sxs-lookup"><span data-stu-id="5ac0d-120">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="5ac0d-121">NuGet.CommandLine</span><span class="sxs-lookup"><span data-stu-id="5ac0d-121">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="5ac0d-122">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="5ac0d-122">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="5ac0d-123">NuGet.Build</span><span class="sxs-lookup"><span data-stu-id="5ac0d-123">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="5ac0d-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (paket, uzantısını değil)</span><span class="sxs-lookup"><span data-stu-id="5ac0d-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="5ac0d-125">Tüm değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="5ac0d-125">All Changes</span></span>
<span data-ttu-id="5ac0d-126">Sürümde ele 10 sorunları vardı.</span><span class="sxs-lookup"><span data-stu-id="5ac0d-126">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="5ac0d-127">Tam bir listesi için iş öğeleri NuGet 2.8.2, lütfen Görünüm sabit [NuGet sorun İzleyicisi bu sürüm için](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="5ac0d-127">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
