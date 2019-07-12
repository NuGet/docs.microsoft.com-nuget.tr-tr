---
title: NuGet Get-Package PowerShell başvurusu
description: Visual Studio'da NuGet Paket Yöneticisi konsolu Get-Package PowerShell komutunda referansı.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d0d25cb6e21f6d0d42389e08340b6f1e1baf8a64
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842512"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="70de3-103">Get-Package (Visual Studio'da Paket Yöneticisi Konsolu)</span><span class="sxs-lookup"><span data-stu-id="70de3-103">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="70de3-104">*Bu konu içindeki komut açıklar [Paket Yöneticisi Konsolu](package-manager-console.md) Windows üzerinde Visual Studio'da. Genel PowerShell Get-Package komutu için bkz: [PowerShell PackageManagement başvuru](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="70de3-104">*This topic describes the command within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="70de3-105">Yerel depoda yüklü paketler listesini alır, - ListAvailable anahtarla kullanıldığında bir paket kaynağından paketleri listeler veya güncelleştirme anahtarıyla birlikte kullanıldığında kullanılabilir güncelleştirmeleri listeler.</span><span class="sxs-lookup"><span data-stu-id="70de3-105">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="70de3-106">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="70de3-106">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="70de3-107">Parametre olmadan `Get-Package` varsayılan projede yüklü paketler listesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="70de3-107">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="70de3-108">Parametreler</span><span class="sxs-lookup"><span data-stu-id="70de3-108">Parameters</span></span>

| <span data-ttu-id="70de3-109">Parametre</span><span class="sxs-lookup"><span data-stu-id="70de3-109">Parameter</span></span> | <span data-ttu-id="70de3-110">Açıklama</span><span class="sxs-lookup"><span data-stu-id="70de3-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="70de3-111">Source</span><span class="sxs-lookup"><span data-stu-id="70de3-111">Source</span></span> | <span data-ttu-id="70de3-112">Paket URL'si veya klasör yolu.</span><span class="sxs-lookup"><span data-stu-id="70de3-112">The URL or folder path for the package .</span></span> <span data-ttu-id="70de3-113">Yerel klasör yol mutlak veya göreli geçerli klasörde olabilir.</span><span class="sxs-lookup"><span data-stu-id="70de3-113">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="70de3-114">Atlanırsa, `Get-Package` seçili paket kaynağı arar.</span><span class="sxs-lookup"><span data-stu-id="70de3-114">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="70de3-115">-ListAvailable ile nuget.org varsayılan olarak kullanıldığında.</span><span class="sxs-lookup"><span data-stu-id="70de3-115">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="70de3-116">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="70de3-116">ListAvailable</span></span> | <span data-ttu-id="70de3-117">Nuget.org için varsayılan bir paket kaynağından paketleri listeler. -PageSize ve/veya - ilk belirtilmediği sürece varsayılan olarak 50 paketler gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="70de3-117">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="70de3-118">Güncelleştirmeler</span><span class="sxs-lookup"><span data-stu-id="70de3-118">Updates</span></span> | <span data-ttu-id="70de3-119">Paket kaynağından bir güncelleştirmenin kullanılabilir olduğu paketleri listeler.</span><span class="sxs-lookup"><span data-stu-id="70de3-119">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="70de3-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="70de3-120">ProjectName</span></span> | <span data-ttu-id="70de3-121">Yüklü paketleri alınmaya başlanacağı proje.</span><span class="sxs-lookup"><span data-stu-id="70de3-121">The project from which to get installed packages.</span></span> <span data-ttu-id="70de3-122">Atlanırsa, tüm çözüm için projeleri döndürür yüklü.</span><span class="sxs-lookup"><span data-stu-id="70de3-122">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="70de3-123">Filtrele</span><span class="sxs-lookup"><span data-stu-id="70de3-123">Filter</span></span> | <span data-ttu-id="70de3-124">Paket kimliği, açıklama ve etiket uygulayarak paketlerin listesini sınırlamak için kullanılan bir filtre dizesi.</span><span class="sxs-lookup"><span data-stu-id="70de3-124">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="70de3-125">ilk</span><span class="sxs-lookup"><span data-stu-id="70de3-125">First</span></span> | <span data-ttu-id="70de3-126">Listeye başlangıcından itibaren döndürülecek paket sayısı.</span><span class="sxs-lookup"><span data-stu-id="70de3-126">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="70de3-127">50'ye belirtilmezse, varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="70de3-127">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="70de3-128">Atla</span><span class="sxs-lookup"><span data-stu-id="70de3-128">Skip</span></span> | <span data-ttu-id="70de3-129">İlk atlar &lt;int&gt; görüntülenen listeden paketleri.</span><span class="sxs-lookup"><span data-stu-id="70de3-129">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="70de3-130">AllVersions</span><span class="sxs-lookup"><span data-stu-id="70de3-130">AllVersions</span></span> | <span data-ttu-id="70de3-131">Tüm kullanılabilir sürümlerin her paketin yerine yalnızca en son sürümünü görüntüler.</span><span class="sxs-lookup"><span data-stu-id="70de3-131">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="70de3-132">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="70de3-132">IncludePrerelease</span></span> | <span data-ttu-id="70de3-133">Yayın öncesi paketleri sonuçları içerir.</span><span class="sxs-lookup"><span data-stu-id="70de3-133">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="70de3-134">PageSize</span><span class="sxs-lookup"><span data-stu-id="70de3-134">PageSize</span></span> | <span data-ttu-id="70de3-135">*(3.0 +)*  - İle ListAvailable (gerekli), devam etmek için bir istem yapmadan önce listelemek için paket sayısı kullanıldığında.</span><span class="sxs-lookup"><span data-stu-id="70de3-135">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="70de3-136">Hiçbiri bu parametre ardışık düzen giriş veya joker karakterler kabul edin.</span><span class="sxs-lookup"><span data-stu-id="70de3-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="70de3-137">Ortak parametreleri</span><span class="sxs-lookup"><span data-stu-id="70de3-137">Common Parameters</span></span>

<span data-ttu-id="70de3-138">`Get-Package` şunları desteklemektedir [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): Hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, ayrıntılı PipelineVariable, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="70de3-138">`Get-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="70de3-139">Örnekler</span><span class="sxs-lookup"><span data-stu-id="70de3-139">Examples</span></span>

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
