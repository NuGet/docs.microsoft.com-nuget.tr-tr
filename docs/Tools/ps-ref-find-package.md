---
title: NuGet Bul-Package PowerShell başvurusu
description: Visual Studio'da NuGet Paket Yöneticisi konsolunda Bul-Package PowerShell komut başvurusu.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 0faf5c5cf9ae99105e3d76a4f5e37f164c4f4ff3
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="b9dc6-103">Bul-Package (Visual Studio'da Paket Yöneticisi Konsolu)</span><span class="sxs-lookup"><span data-stu-id="b9dc6-103">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="b9dc6-104">*Sürüm 3.0 +; Bu konu içindeki komut açıklar [NuGet Paket Yöneticisi Konsolu](package-manager-console.md) Windows Visual Studio'da. Genel PowerShell Bul-Package komutu için bkz: [PowerShell PackageManagement başvuru](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="b9dc6-104">*Version 3.0+; this topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="b9dc6-105">Belirtilen kimliği veya anahtar sözcükleri sahip uzak paket kümesini paket kaynağından alır.</span><span class="sxs-lookup"><span data-stu-id="b9dc6-105">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="b9dc6-106">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="b9dc6-106">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="b9dc6-107">Parametreler</span><span class="sxs-lookup"><span data-stu-id="b9dc6-107">Parameters</span></span>

| <span data-ttu-id="b9dc6-108">Parametre</span><span class="sxs-lookup"><span data-stu-id="b9dc6-108">Parameter</span></span> | <span data-ttu-id="b9dc6-109">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b9dc6-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b9dc6-110">Kimliği &lt;anahtar sözcükler&gt;</span><span class="sxs-lookup"><span data-stu-id="b9dc6-110">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="b9dc6-111">(Gerekli) Paket kaynağı ararken kullanılacak anahtar sözcükler.</span><span class="sxs-lookup"><span data-stu-id="b9dc6-111">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="b9dc6-112">Yalnızca paket Kimliğine anahtar sözcüklerle eşleşen paketleri döndürmek için - ExactMatch kullanın.</span><span class="sxs-lookup"><span data-stu-id="b9dc6-112">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="b9dc6-113">Hiçbir anahtar sözcükleri verilirse, `Find-Package` ilk belirtilen-yüklemeleri veya sayı ilk 20 paketlerin listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="b9dc6-113">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="b9dc6-114">Kimliği isteğe bağlıdır ve no-op a - unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b9dc6-114">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="b9dc6-115">Kaynak</span><span class="sxs-lookup"><span data-stu-id="b9dc6-115">Source</span></span> | <span data-ttu-id="b9dc6-116">Aranacak paket kaynağının URL'sini veya klasör yolu.</span><span class="sxs-lookup"><span data-stu-id="b9dc6-116">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="b9dc6-117">Yerel klasör yolları mutlak veya göreli geçerli klasörde olabilir.</span><span class="sxs-lookup"><span data-stu-id="b9dc6-117">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="b9dc6-118">Atlanırsa, `Find-Package` şu anda seçili paket kaynağını arar.</span><span class="sxs-lookup"><span data-stu-id="b9dc6-118">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="b9dc6-119">AllVersions</span><span class="sxs-lookup"><span data-stu-id="b9dc6-119">AllVersions</span></span> | <span data-ttu-id="b9dc6-120">Yalnızca en son sürümü yerine her paketin tüm kullanılabilir sürümlerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="b9dc6-120">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="b9dc6-121">ilk</span><span class="sxs-lookup"><span data-stu-id="b9dc6-121">First</span></span> | <span data-ttu-id="b9dc6-122">Listenin başlangıcından döndürülecek paket sayısı; Varsayılan değer 20'dir.</span><span class="sxs-lookup"><span data-stu-id="b9dc6-122">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="b9dc6-123">Atla</span><span class="sxs-lookup"><span data-stu-id="b9dc6-123">Skip</span></span> | <span data-ttu-id="b9dc6-124">İlk atlar &lt;int&gt; görüntülenen listeden paketler.</span><span class="sxs-lookup"><span data-stu-id="b9dc6-124">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="b9dc6-125">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="b9dc6-125">IncludePrerelease</span></span> | <span data-ttu-id="b9dc6-126">Sonuçlarda Önsürüm paketlerinin içerir.</span><span class="sxs-lookup"><span data-stu-id="b9dc6-126">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="b9dc6-127">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="b9dc6-127">ExactMatch</span></span> | <span data-ttu-id="b9dc6-128">Kullanmak için belirtilen &lt;anahtar sözcükleri&gt; büyük küçük harfe duyarlı paket kimliği olarak</span><span class="sxs-lookup"><span data-stu-id="b9dc6-128">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="b9dc6-129">StartWith</span><span class="sxs-lookup"><span data-stu-id="b9dc6-129">StartWith</span></span> | <span data-ttu-id="b9dc6-130">Döndürür paketler, paket kimliği ile başlayıp &lt;anahtar sözcükleri&gt;.</span><span class="sxs-lookup"><span data-stu-id="b9dc6-130">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="b9dc6-131">Hiçbiri bu parametre ardışık düzen giriş veya joker karakter kabul edin.</span><span class="sxs-lookup"><span data-stu-id="b9dc6-131">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="b9dc6-132">Ortak parametreleri</span><span class="sxs-lookup"><span data-stu-id="b9dc6-132">Common Parameters</span></span>

<span data-ttu-id="b9dc6-133">`Find-Package` Aşağıdaki destekleyen [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, ayrıntı, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="b9dc6-133">`Find-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="b9dc6-134">Örnekler</span><span class="sxs-lookup"><span data-stu-id="b9dc6-134">Examples</span></span>

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
