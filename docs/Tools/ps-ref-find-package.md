---
title: "NuGet Bul-Package PowerShell başvurusu | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 6/1/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Visual Studio'da NuGet Paket Yöneticisi konsolunda Bul-Package PowerShell komut başvurusu."
keywords: "NuGet Paket Yöneticisi konsolunda, NuGet Powershell komutları Bul paket NuGet Powershell başvurusu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 47b8420cc49d0a76709cf3268af69fcff310d165
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2018
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="f03c6-104">Bul-Package (Visual Studio'da Paket Yöneticisi Konsolu)</span><span class="sxs-lookup"><span data-stu-id="f03c6-104">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="f03c6-105">*Sürüm 3.0 +; Bu konu içindeki komut açıklar [NuGet Paket Yöneticisi Konsolu](Package-Manager-Console.md) Windows Visual Studio'da. Genel PowerShell Bul-Package komutu için bkz: [PowerShell PackageManagement başvuru](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="f03c6-105">*Version 3.0+; this topic describes the command within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="f03c6-106">Belirtilen kimliği veya anahtar sözcükleri sahip uzak paket kümesini paket kaynağından alır.</span><span class="sxs-lookup"><span data-stu-id="f03c6-106">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="f03c6-107">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="f03c6-107">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="f03c6-108">Parametreler</span><span class="sxs-lookup"><span data-stu-id="f03c6-108">Parameters</span></span>

| <span data-ttu-id="f03c6-109">Parametre</span><span class="sxs-lookup"><span data-stu-id="f03c6-109">Parameter</span></span> | <span data-ttu-id="f03c6-110">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f03c6-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f03c6-111">Kimliği &lt;anahtar sözcükler&gt;</span><span class="sxs-lookup"><span data-stu-id="f03c6-111">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="f03c6-112">(Gerekli) Paket kaynağı ararken kullanılacak anahtar sözcükler.</span><span class="sxs-lookup"><span data-stu-id="f03c6-112">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="f03c6-113">Yalnızca paket Kimliğine anahtar sözcüklerle eşleşen paketleri döndürmek için - ExactMatch kullanın.</span><span class="sxs-lookup"><span data-stu-id="f03c6-113">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="f03c6-114">Hiçbir anahtar sözcükleri verilirse, `Find-Package` ilk belirtilen-yüklemeleri veya sayı ilk 20 paketlerin listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="f03c6-114">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="f03c6-115">Kimliği isteğe bağlıdır ve no-op a - unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f03c6-115">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="f03c6-116">Kaynak</span><span class="sxs-lookup"><span data-stu-id="f03c6-116">Source</span></span> | <span data-ttu-id="f03c6-117">Aranacak paket kaynağının URL'sini veya klasör yolu.</span><span class="sxs-lookup"><span data-stu-id="f03c6-117">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="f03c6-118">Yerel klasör yolları mutlak veya göreli geçerli klasörde olabilir.</span><span class="sxs-lookup"><span data-stu-id="f03c6-118">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="f03c6-119">Atlanırsa, `Find-Package` şu anda seçili paket kaynağını arar.</span><span class="sxs-lookup"><span data-stu-id="f03c6-119">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="f03c6-120">AllVersions</span><span class="sxs-lookup"><span data-stu-id="f03c6-120">AllVersions</span></span> | <span data-ttu-id="f03c6-121">Yalnızca en son sürümü yerine her paketin tüm kullanılabilir sürümlerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="f03c6-121">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="f03c6-122">ilk</span><span class="sxs-lookup"><span data-stu-id="f03c6-122">First</span></span> | <span data-ttu-id="f03c6-123">Listenin başlangıcından döndürülecek paket sayısı; Varsayılan değer 20'dir.</span><span class="sxs-lookup"><span data-stu-id="f03c6-123">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="f03c6-124">Atla</span><span class="sxs-lookup"><span data-stu-id="f03c6-124">Skip</span></span> | <span data-ttu-id="f03c6-125">İlk atlar &lt;int&gt; görüntülenen listeden paketler.</span><span class="sxs-lookup"><span data-stu-id="f03c6-125">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="f03c6-126">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="f03c6-126">IncludePrerelease</span></span> | <span data-ttu-id="f03c6-127">Sonuçlarda Önsürüm paketlerinin içerir.</span><span class="sxs-lookup"><span data-stu-id="f03c6-127">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="f03c6-128">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="f03c6-128">ExactMatch</span></span> | <span data-ttu-id="f03c6-129">Kullanmak için belirtilen &lt;anahtar sözcükleri&gt; büyük küçük harfe duyarlı paket kimliği olarak</span><span class="sxs-lookup"><span data-stu-id="f03c6-129">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="f03c6-130">StartWith</span><span class="sxs-lookup"><span data-stu-id="f03c6-130">StartWith</span></span> | <span data-ttu-id="f03c6-131">Döndürür paketler, paket kimliği ile başlayıp &lt;anahtar sözcükleri&gt;.</span><span class="sxs-lookup"><span data-stu-id="f03c6-131">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="f03c6-132">Hiçbiri bu parametre ardışık düzen giriş veya joker karakter kabul edin.</span><span class="sxs-lookup"><span data-stu-id="f03c6-132">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="f03c6-133">Ortak parametreleri</span><span class="sxs-lookup"><span data-stu-id="f03c6-133">Common Parameters</span></span>

<span data-ttu-id="f03c6-134">`Find-Package`Aşağıdaki destekleyen [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, ayrıntı, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="f03c6-134">`Find-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="f03c6-135">Örnekler</span><span class="sxs-lookup"><span data-stu-id="f03c6-135">Examples</span></span>

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
