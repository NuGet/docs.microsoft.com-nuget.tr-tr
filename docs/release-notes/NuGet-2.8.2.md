---
title: 2.8.2 NuGet sürüm notları
description: NuGet 2.8.2 dahil etmek için sürüm notları, sorunları, hata düzeltmeleri, eklenen özellikler ve dcr bilinir.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ed22aef6766bbe8e4b688e0587304a18eaeb8895
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551154"
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="63e5d-103">2.8.2 NuGet sürüm notları</span><span class="sxs-lookup"><span data-stu-id="63e5d-103">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="63e5d-104">[2.8.1 NuGet sürüm notları](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 sürüm notları](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="63e5d-104">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="63e5d-105">NuGet 2.8.2 22 Mayıs 2014'te yayımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="63e5d-105">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="63e5d-106">Bu sürüm yalnızca değişiklikleri nuget.exe komut satırı, NuGet.Server paket ve diğer NuGet paketleri dahil.</span><span class="sxs-lookup"><span data-stu-id="63e5d-106">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="63e5d-107">Yayın, bir Visual Studio Uzantısı'nı güncelleştirilmiş veya WebMatrix genişletmesi içermiyordu.</span><span class="sxs-lookup"><span data-stu-id="63e5d-107">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="63e5d-108">Önemli güncelleştirmeler</span><span class="sxs-lookup"><span data-stu-id="63e5d-108">Notable Updates</span></span>

<span data-ttu-id="63e5d-109">Nuget.exe komut satırı ve NuGet.Server paket (şirket içinde barındırılan NuGet akışları için) en önemli güncelleştirmeler yoktu.</span><span class="sxs-lookup"><span data-stu-id="63e5d-109">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="63e5d-110">Önemli nuget.exe hata düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="63e5d-110">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="63e5d-111">nuget.exe gönderme başarısız olur ve yeniden deneniyor tutar</span><span class="sxs-lookup"><span data-stu-id="63e5d-111">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="63e5d-112">Temel kimlik doğrulama kimlik bilgileri doğru biçimde göndermez nuget.exe anında iletme</span><span class="sxs-lookup"><span data-stu-id="63e5d-112">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="63e5d-113">nuget.exe anında iletme geçici yeniden yönlendirme izleyin gerekmez</span><span class="sxs-lookup"><span data-stu-id="63e5d-113">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="63e5d-114">Önemli NuGet.Server hata düzeltmesi</span><span class="sxs-lookup"><span data-stu-id="63e5d-114">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="63e5d-115">Yanlış değerini NuGet.Server tarafından döndürülen IsAbsoluteLatestVersion</span><span class="sxs-lookup"><span data-stu-id="63e5d-115">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="63e5d-116">Güncelleştirme paketleri</span><span class="sxs-lookup"><span data-stu-id="63e5d-116">Packages Updated</span></span>

<span data-ttu-id="63e5d-117">Nuget.exe komut satırı ve NuGet.Server düzeltmeleri NuGet paket güncelleştirmelerini gönderilir.</span><span class="sxs-lookup"><span data-stu-id="63e5d-117">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="63e5d-118">Diğer paketler de 2.8.2 ile güncelleştirildi vardı.</span><span class="sxs-lookup"><span data-stu-id="63e5d-118">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="63e5d-119">Güncelleştirilmiş paket listesi aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="63e5d-119">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="63e5d-120">NuGet.Core</span><span class="sxs-lookup"><span data-stu-id="63e5d-120">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="63e5d-121">NuGet.CommandLine</span><span class="sxs-lookup"><span data-stu-id="63e5d-121">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="63e5d-122">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="63e5d-122">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="63e5d-123">NuGet.Build</span><span class="sxs-lookup"><span data-stu-id="63e5d-123">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="63e5d-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (paket, uzantı)</span><span class="sxs-lookup"><span data-stu-id="63e5d-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="63e5d-125">Tüm değişiklikler</span><span class="sxs-lookup"><span data-stu-id="63e5d-125">All Changes</span></span>
<span data-ttu-id="63e5d-126">Sürümünde giderilen 10 sorunlar oluştu.</span><span class="sxs-lookup"><span data-stu-id="63e5d-126">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="63e5d-127">Tam bir listesi için iş öğeleri Nuget'te 2.8.2, lütfen görünümü sabit [bu sürüm için NuGet sorun İzleyicisi](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="63e5d-127">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
