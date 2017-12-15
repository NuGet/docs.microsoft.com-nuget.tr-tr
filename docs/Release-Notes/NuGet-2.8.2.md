---
title: "NuGet 2.8.2 sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: bb547f5d-3c0e-4721-b2c7-3fc7e09c34de
description: "Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr NuGet 2.8.2 dahil etmek için sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 2.8.2 sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 221b8970663ca80a986fc3ee542b99971c5e2018
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="0616b-104">NuGet 2.8.2 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="0616b-104">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="0616b-105">[NuGet 2.8.1 ile sürüm notları](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 sürüm notları](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="0616b-105">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="0616b-106">NuGet 2.8.2 22 Mayıs 2014'te yayımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="0616b-106">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="0616b-107">Bu sürüm yalnızca komut satırı nuget.exe, NuGet.Server paket ve diğer NuGet paketleri yapılan değişiklikler dahil.</span><span class="sxs-lookup"><span data-stu-id="0616b-107">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="0616b-108">Yayın güncelleştirilmiş Visual Studio uzantısı veya WebMatrix genişletmesi içermiyordu.</span><span class="sxs-lookup"><span data-stu-id="0616b-108">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="0616b-109">Önemli güncelleştirmeleri</span><span class="sxs-lookup"><span data-stu-id="0616b-109">Notable Updates</span></span>

<span data-ttu-id="0616b-110">Komut satırı nuget.exe ve NuGet.Server paket (kendi kendini barındıran NuGet akışlarını için) en önemli güncelleştirmeleri yoktu.</span><span class="sxs-lookup"><span data-stu-id="0616b-110">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="0616b-111">Önemli nuget.exe hata düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="0616b-111">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="0616b-112">nuget.exe gönderme başarısız olur ve yeniden deneniyor tutar</span><span class="sxs-lookup"><span data-stu-id="0616b-112">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="0616b-113">nuget.exe itme temel kimlik doğrulama kimlik bilgileri doğru biçimde göndermez</span><span class="sxs-lookup"><span data-stu-id="0616b-113">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="0616b-114">nuget.exe itme geçici yeniden yönlendirme izleyin olmaz</span><span class="sxs-lookup"><span data-stu-id="0616b-114">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="0616b-115">Önemli NuGet.Server hata düzeltmesi</span><span class="sxs-lookup"><span data-stu-id="0616b-115">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="0616b-116">NuGet.Server tarafından döndürülen IsAbsoluteLatestVersion yanlış değeri</span><span class="sxs-lookup"><span data-stu-id="0616b-116">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="0616b-117">Güncelleştirme paketleri</span><span class="sxs-lookup"><span data-stu-id="0616b-117">Packages Updated</span></span>

<span data-ttu-id="0616b-118">NuGet.Server düzeltmeler ve komut satırı nuget.exe NuGet paketi güncelleştirme gönderilir.</span><span class="sxs-lookup"><span data-stu-id="0616b-118">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="0616b-119">Diğer paketleri de 2.8.2 ile güncelleştirilmiş vardı.</span><span class="sxs-lookup"><span data-stu-id="0616b-119">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="0616b-120">Güncelleştirilmiş paketleri listesi aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="0616b-120">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="0616b-121">NuGet.Core</span><span class="sxs-lookup"><span data-stu-id="0616b-121">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="0616b-122">NuGet.CommandLine</span><span class="sxs-lookup"><span data-stu-id="0616b-122">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="0616b-123">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="0616b-123">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="0616b-124">NuGet.Build</span><span class="sxs-lookup"><span data-stu-id="0616b-124">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="0616b-125">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (paket, uzantısını değil)</span><span class="sxs-lookup"><span data-stu-id="0616b-125">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="0616b-126">Tüm değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="0616b-126">All Changes</span></span>
<span data-ttu-id="0616b-127">Sürümde ele 10 sorunları vardı.</span><span class="sxs-lookup"><span data-stu-id="0616b-127">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="0616b-128">Tam bir listesi için iş öğeleri NuGet 2.8.2, lütfen Görünüm sabit [NuGet sorun İzleyicisi bu sürüm için](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="0616b-128">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
