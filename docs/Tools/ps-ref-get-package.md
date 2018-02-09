---
title: "NuGet Get-Package PowerShell başvurusu | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Visual Studio'da NuGet Paket Yöneticisi konsolunda Get-Package PowerShell komut başvurusu."
keywords: "NuGet Paket Yöneticisi konsolu, NuGet Powershell komutlarını NuGet Powershell başvurusu, Get-Package"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c38e0da2e98d2e5bf5b4fc165462e9abcfdd73c0
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2018
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="f40cb-104">Get-Package (Visual Studio'da Paket Yöneticisi Konsolu)</span><span class="sxs-lookup"><span data-stu-id="f40cb-104">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="f40cb-105">*Bu konu içindeki komut açıklar [NuGet Paket Yöneticisi Konsolu](Package-Manager-Console.md) Windows Visual Studio'da. Genel PowerShell Get-Package komutu için bkz: [PowerShell PackageManagement başvuru](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="f40cb-105">*This topic describes the command within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="f40cb-106">Yerel depoda yüklü olan paketlerin listesini alır, - listavailable birlikte anahtarıyla birlikte kullanıldığında bir paket kaynağındaki paketleri listeler veya güncelleştirme anahtarıyla birlikte kullanıldığında kullanılabilir güncelleştirmeleri listeler.</span><span class="sxs-lookup"><span data-stu-id="f40cb-106">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="f40cb-107">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="f40cb-107">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="f40cb-108">Hiçbir parametre `Get-Package` varsayılan projede yüklü olan paketlerin listesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="f40cb-108">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="f40cb-109">Parametreler</span><span class="sxs-lookup"><span data-stu-id="f40cb-109">Parameters</span></span>

| <span data-ttu-id="f40cb-110">Parametre</span><span class="sxs-lookup"><span data-stu-id="f40cb-110">Parameter</span></span> | <span data-ttu-id="f40cb-111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f40cb-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f40cb-112">Kaynak</span><span class="sxs-lookup"><span data-stu-id="f40cb-112">Source</span></span> | <span data-ttu-id="f40cb-113">Paket URL'si veya klasör yolu.</span><span class="sxs-lookup"><span data-stu-id="f40cb-113">The URL or folder path for the package .</span></span> <span data-ttu-id="f40cb-114">Yerel klasör yolları mutlak veya göreli geçerli klasörde olabilir.</span><span class="sxs-lookup"><span data-stu-id="f40cb-114">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="f40cb-115">Atlanırsa, `Get-Package` şu anda seçili paket kaynağını arar.</span><span class="sxs-lookup"><span data-stu-id="f40cb-115">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="f40cb-116">-Listavailable ile birlikte, nuget.org varsayılanlara kullanıldığında.</span><span class="sxs-lookup"><span data-stu-id="f40cb-116">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="f40cb-117">Listavailable birlikte</span><span class="sxs-lookup"><span data-stu-id="f40cb-117">ListAvailable</span></span> | <span data-ttu-id="f40cb-118">Nuget.org için varsayılan değer olarak, bir paket kaynağındaki paketleri listeler. -PageSize ve/veya - ilk belirtilmediği sürece varsayılan 50 paketlerin gösterir.</span><span class="sxs-lookup"><span data-stu-id="f40cb-118">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="f40cb-119">Güncelleştirmeler</span><span class="sxs-lookup"><span data-stu-id="f40cb-119">Updates</span></span> | <span data-ttu-id="f40cb-120">Paket kaynağındaki güncelleştirmeye sahip paketleri listeler.</span><span class="sxs-lookup"><span data-stu-id="f40cb-120">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="f40cb-121">ProjectName</span><span class="sxs-lookup"><span data-stu-id="f40cb-121">ProjectName</span></span> | <span data-ttu-id="f40cb-122">Yüklü paketler alınacağı projesi.</span><span class="sxs-lookup"><span data-stu-id="f40cb-122">The project from which to get installed packages.</span></span> <span data-ttu-id="f40cb-123">Atlanırsa, çözümün tamamı için projeleri döndürür yüklü.</span><span class="sxs-lookup"><span data-stu-id="f40cb-123">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="f40cb-124">Filtrele</span><span class="sxs-lookup"><span data-stu-id="f40cb-124">Filter</span></span> | <span data-ttu-id="f40cb-125">Paket kimliği, açıklamada ve etiketlerde uygulayarak paket listesini daraltmak için kullanılan bir filtre dizesi.</span><span class="sxs-lookup"><span data-stu-id="f40cb-125">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="f40cb-126">ilk</span><span class="sxs-lookup"><span data-stu-id="f40cb-126">First</span></span> | <span data-ttu-id="f40cb-127">Listenin başlangıcından döndürülecek paket sayısı.</span><span class="sxs-lookup"><span data-stu-id="f40cb-127">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="f40cb-128">Belirtilmezse, 50'ye varsayılan olur.</span><span class="sxs-lookup"><span data-stu-id="f40cb-128">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="f40cb-129">Atla</span><span class="sxs-lookup"><span data-stu-id="f40cb-129">Skip</span></span> | <span data-ttu-id="f40cb-130">İlk atlar &lt;int&gt; görüntülenen listeden paketler.</span><span class="sxs-lookup"><span data-stu-id="f40cb-130">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="f40cb-131">AllVersions</span><span class="sxs-lookup"><span data-stu-id="f40cb-131">AllVersions</span></span> | <span data-ttu-id="f40cb-132">Yalnızca en son sürümü yerine her paketin tüm kullanılabilir sürümlerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="f40cb-132">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="f40cb-133">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="f40cb-133">IncludePrerelease</span></span> | <span data-ttu-id="f40cb-134">Sonuçlarda Önsürüm paketlerinin içerir.</span><span class="sxs-lookup"><span data-stu-id="f40cb-134">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="f40cb-135">PageSize</span><span class="sxs-lookup"><span data-stu-id="f40cb-135">PageSize</span></span> | <span data-ttu-id="f40cb-136">*(3.0 +)*  -(Gerekli) listavailable ile birlikte, devam etmek için bir istem vermeden önce listelemek için paket sayısı kullanıldığında.</span><span class="sxs-lookup"><span data-stu-id="f40cb-136">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="f40cb-137">Hiçbiri bu parametre ardışık düzen giriş veya joker karakter kabul edin.</span><span class="sxs-lookup"><span data-stu-id="f40cb-137">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="f40cb-138">Ortak parametreleri</span><span class="sxs-lookup"><span data-stu-id="f40cb-138">Common Parameters</span></span>

<span data-ttu-id="f40cb-139">`Get-Package`Aşağıdaki destekleyen [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, ayrıntı, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="f40cb-139">`Get-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="f40cb-140">Örnekler</span><span class="sxs-lookup"><span data-stu-id="f40cb-140">Examples</span></span>

```ps
# Lists the packages installed in the current solution
Get-Package

# Lists the packages installed in a project
Get-Package -ProjectName MyProject

# Lists packages available in the current package source
Get-Package -ListAvailable

# Lists 30 packages at a time from the current source, and prompts to continue if more are available
Get-Package -ListAvailable -PageSize 30

# Lists packages with the Ninject keyword in the current source, up to 50
Get-Package -ListAvailable -Filter Ninject

# List all versions of packages matching the filter "jquery"
Get-Package -ListAvailable -Filter jquery -AllVersions

# Lists packages installed in the solution that have available updates
Get-Package -Updates

# Lists packages installed in a specific project that have available updates
Get-Package -Updates -ProjectName MyProject
```