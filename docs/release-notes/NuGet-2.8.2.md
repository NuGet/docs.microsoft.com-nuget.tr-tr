---
title: NuGet 2.8.2 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 2.8.2 için sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d39f2dc9a429ed264461174325c2080468fa8aae
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780368"
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="5e00e-103">NuGet 2.8.2 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="5e00e-103">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="5e00e-104">[NuGet 2.8.1 sürüm notları](../release-notes/nuget-2.8.1.md)  |  [NuGet 2.8.3 sürüm notları](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="5e00e-104">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="5e00e-105">NuGet 2.8.2, 22 Mayıs 2014 tarihinde yayınlandı.</span><span class="sxs-lookup"><span data-stu-id="5e00e-105">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="5e00e-106">Bu sürüm yalnızca nuget.exe komut satırına, NuGet. Server paketine ve diğer NuGet paketlerine yapılan değişiklikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="5e00e-106">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="5e00e-107">Sürüm, güncelleştirilmiş bir Visual Studio uzantısı veya WebMatrix uzantısı içermiyordu.</span><span class="sxs-lookup"><span data-stu-id="5e00e-107">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="5e00e-108">Önemli güncelleştirmeler</span><span class="sxs-lookup"><span data-stu-id="5e00e-108">Notable Updates</span></span>

<span data-ttu-id="5e00e-109">En önemli güncelleştirmeler nuget.exe komut satırı ve NuGet. Server paketidir (Şirket içinde barındırılan NuGet akışları için).</span><span class="sxs-lookup"><span data-stu-id="5e00e-109">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="5e00e-110">Önemli nuget.exe hata düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="5e00e-110">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="5e00e-111">nuget.exe gönderimi başarısız oluyor ve yeniden denemeyi sürdüyor</span><span class="sxs-lookup"><span data-stu-id="5e00e-111">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="5e00e-112">nuget.exe gönderimi temel kimlik doğrulama kimlik bilgilerini doğru göndermez</span><span class="sxs-lookup"><span data-stu-id="5e00e-112">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="5e00e-113">nuget.exe gönderimi geçici yeniden yönlendirmeye uymalıdır</span><span class="sxs-lookup"><span data-stu-id="5e00e-113">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="5e00e-114">Önemli NuGet. sunucu hata onarımı</span><span class="sxs-lookup"><span data-stu-id="5e00e-114">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="5e00e-115">NuGet. Server tarafından döndürülen yanlış IsAbsoluteLatestVersion değeri</span><span class="sxs-lookup"><span data-stu-id="5e00e-115">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="5e00e-116">Paketler güncelleştirildi</span><span class="sxs-lookup"><span data-stu-id="5e00e-116">Packages Updated</span></span>

<span data-ttu-id="5e00e-117">nuget.exe komut satırı ve NuGet. Server düzeltmeleri NuGet paket güncelleştirmeleri olarak gönderilir.</span><span class="sxs-lookup"><span data-stu-id="5e00e-117">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="5e00e-118">2.8.2 ile güncelleştirilmiş başka paketler de vardı.</span><span class="sxs-lookup"><span data-stu-id="5e00e-118">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="5e00e-119">Güncelleştirilmiş paketlerin listesi aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="5e00e-119">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="5e00e-120">NuGet. Core</span><span class="sxs-lookup"><span data-stu-id="5e00e-120">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="5e00e-121">NuGet. CommandLine</span><span class="sxs-lookup"><span data-stu-id="5e00e-121">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="5e00e-122">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="5e00e-122">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="5e00e-123">NuGet. Build</span><span class="sxs-lookup"><span data-stu-id="5e00e-123">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="5e00e-124">[NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (uzantı değil, paket)</span><span class="sxs-lookup"><span data-stu-id="5e00e-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="5e00e-125">Tüm değişiklikler</span><span class="sxs-lookup"><span data-stu-id="5e00e-125">All Changes</span></span>
<span data-ttu-id="5e00e-126">Yayında ele alınan 10 sorun oluştu.</span><span class="sxs-lookup"><span data-stu-id="5e00e-126">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="5e00e-127">NuGet 2.8.2 'te düzeltilen iş öğelerinin tam listesi için lütfen [Bu sürüm Için NuGet sorun İzleyicisi](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)' ni görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="5e00e-127">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
