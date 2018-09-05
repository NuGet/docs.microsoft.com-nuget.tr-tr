---
title: NuGet Bul-Package PowerShell başvurusu
description: Visual Studio'da NuGet Paket Yöneticisi konsolu Bul-Package PowerShell komutunda referansı.
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: c6797e3778c7095a9abfc6cd87e2337313988c20
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550984"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="d1557-103">Find-Package (Visual Studio'da Paket Yöneticisi Konsolu)</span><span class="sxs-lookup"><span data-stu-id="d1557-103">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="d1557-104">*Sürüm 3.0 +; Bu konu içindeki komut açıklar [NuGet Paket Yöneticisi Konsolu](package-manager-console.md) Windows üzerinde Visual Studio'da. Genel PowerShell Bul-Package komutu için bkz: [PowerShell PackageManagement başvuru](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="d1557-104">*Version 3.0+; this topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="d1557-105">Belirtilen kimliği veya anahtar sözcükleri ile uzak paketleri paket kaynağından alır.</span><span class="sxs-lookup"><span data-stu-id="d1557-105">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="d1557-106">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="d1557-106">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="d1557-107">Parametreler</span><span class="sxs-lookup"><span data-stu-id="d1557-107">Parameters</span></span>

| <span data-ttu-id="d1557-108">Parametre</span><span class="sxs-lookup"><span data-stu-id="d1557-108">Parameter</span></span> | <span data-ttu-id="d1557-109">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1557-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d1557-110">Kimliği &lt;anahtar sözcükleri&gt;</span><span class="sxs-lookup"><span data-stu-id="d1557-110">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="d1557-111">(Gerekli) Paket kaynağı ararken kullanmak için anahtar sözcükler.</span><span class="sxs-lookup"><span data-stu-id="d1557-111">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="d1557-112">Paket kimliği anahtar sözcüklerle eşleşen paketleri döndürülecek - ExactMatch kullanın.</span><span class="sxs-lookup"><span data-stu-id="d1557-112">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="d1557-113">Anahtar sözcük verilirse `Find-Package` ilk belirtilen-ilk 20 paketleri indirme veya sayı listesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="d1557-113">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="d1557-114">Kimliği isteğe bağlıdır ve İşlemsiz - unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d1557-114">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="d1557-115">Kaynak</span><span class="sxs-lookup"><span data-stu-id="d1557-115">Source</span></span> | <span data-ttu-id="d1557-116">Aranacak paket kaynağı için URL veya klasör yolu.</span><span class="sxs-lookup"><span data-stu-id="d1557-116">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="d1557-117">Yerel klasör yol mutlak veya göreli geçerli klasörde olabilir.</span><span class="sxs-lookup"><span data-stu-id="d1557-117">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="d1557-118">Atlanırsa, `Find-Package` seçili paket kaynağı arar.</span><span class="sxs-lookup"><span data-stu-id="d1557-118">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="d1557-119">AllVersions</span><span class="sxs-lookup"><span data-stu-id="d1557-119">AllVersions</span></span> | <span data-ttu-id="d1557-120">Tüm kullanılabilir sürümlerin her paketin yerine yalnızca en son sürümünü görüntüler.</span><span class="sxs-lookup"><span data-stu-id="d1557-120">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="d1557-121">ilk</span><span class="sxs-lookup"><span data-stu-id="d1557-121">First</span></span> | <span data-ttu-id="d1557-122">Listeye başlangıcından itibaren döndürülecek paket sayısı; Varsayılan değer 20'dir.</span><span class="sxs-lookup"><span data-stu-id="d1557-122">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="d1557-123">Atla</span><span class="sxs-lookup"><span data-stu-id="d1557-123">Skip</span></span> | <span data-ttu-id="d1557-124">İlk atlar &lt;int&gt; görüntülenen listeden paketleri.</span><span class="sxs-lookup"><span data-stu-id="d1557-124">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="d1557-125">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="d1557-125">IncludePrerelease</span></span> | <span data-ttu-id="d1557-126">Yayın öncesi paketleri sonuçları içerir.</span><span class="sxs-lookup"><span data-stu-id="d1557-126">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="d1557-127">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="d1557-127">ExactMatch</span></span> | <span data-ttu-id="d1557-128">Belirtilen kullanılacak &lt;anahtar sözcükleri&gt; olarak büyük küçük harfe duyarlı paket kimliği</span><span class="sxs-lookup"><span data-stu-id="d1557-128">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="d1557-129">StartWith</span><span class="sxs-lookup"><span data-stu-id="d1557-129">StartWith</span></span> | <span data-ttu-id="d1557-130">Paketler, paket kimliği ile başlayan döndürür &lt;anahtar sözcükleri&gt;.</span><span class="sxs-lookup"><span data-stu-id="d1557-130">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="d1557-131">Hiçbiri bu parametre ardışık düzen giriş veya joker karakterler kabul edin.</span><span class="sxs-lookup"><span data-stu-id="d1557-131">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="d1557-132">Ortak parametreleri</span><span class="sxs-lookup"><span data-stu-id="d1557-132">Common Parameters</span></span>

<span data-ttu-id="d1557-133">`Find-Package` şunları desteklemektedir [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, ayrıntılı, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="d1557-133">`Find-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="d1557-134">Örnekler</span><span class="sxs-lookup"><span data-stu-id="d1557-134">Examples</span></span>

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```
