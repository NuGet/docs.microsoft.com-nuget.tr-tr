---
title: NuGet Get-Package PowerShell Başvurusu
description: Visual Studio 'daki NuGet Paket Yöneticisi konsolundaki Get-Package PowerShell komutuna yönelik başvuru.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8394f888ec3d5e57eacd351a4867173da1070ead
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777502"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="bbe38-103">Get-Package (Visual Studio 'da Paket Yöneticisi konsolu)</span><span class="sxs-lookup"><span data-stu-id="bbe38-103">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="bbe38-104">*Bu konuda, Windows üzerinde Visual Studio 'da [Paket Yöneticisi konsolu](../../consume-packages/install-use-packages-powershell.md) içindeki komut açıklanmaktadır. Genel PowerShell Get-Package komutu için bkz. [PowerShell PackageManagement başvurusu](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="bbe38-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="bbe38-105">Yerel depoda yüklü paketlerin listesini alır,-ListAvailable anahtarıyla birlikte kullanıldığında bir paket kaynağından kullanılabilir olan paketleri listeler veya-Update anahtarıyla birlikte kullanıldığında kullanılabilir güncelleştirmeleri listeler.</span><span class="sxs-lookup"><span data-stu-id="bbe38-105">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="bbe38-106">Syntax</span><span class="sxs-lookup"><span data-stu-id="bbe38-106">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="bbe38-107">Parametresiz, `Get-Package` varsayılan projede yüklü paketlerin listesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="bbe38-107">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="bbe38-108">Parametreler</span><span class="sxs-lookup"><span data-stu-id="bbe38-108">Parameters</span></span>

| <span data-ttu-id="bbe38-109">Parametre</span><span class="sxs-lookup"><span data-stu-id="bbe38-109">Parameter</span></span> | <span data-ttu-id="bbe38-110">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bbe38-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bbe38-111">Kaynak</span><span class="sxs-lookup"><span data-stu-id="bbe38-111">Source</span></span> | <span data-ttu-id="bbe38-112">Paketin URL veya klasör yolu.</span><span class="sxs-lookup"><span data-stu-id="bbe38-112">The URL or folder path for the package .</span></span> <span data-ttu-id="bbe38-113">Yerel klasör yolları mutlak veya geçerli klasöre göreli olabilir.</span><span class="sxs-lookup"><span data-stu-id="bbe38-113">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="bbe38-114">Atlanırsa, `Get-Package` Şu anda seçili olan paket kaynağını arar.</span><span class="sxs-lookup"><span data-stu-id="bbe38-114">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="bbe38-115">-ListAvailable ile kullanıldığında varsayılan olarak nuget.org olur.</span><span class="sxs-lookup"><span data-stu-id="bbe38-115">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="bbe38-116">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="bbe38-116">ListAvailable</span></span> | <span data-ttu-id="bbe38-117">Bir paket kaynağından kullanılabilir olan paketleri listeler, varsayılan olarak nuget.org. -PageSize ve/veya-First belirtilmemişse, varsayılan 50 paket gösterir.</span><span class="sxs-lookup"><span data-stu-id="bbe38-117">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="bbe38-118">Güncelleştirmeler</span><span class="sxs-lookup"><span data-stu-id="bbe38-118">Updates</span></span> | <span data-ttu-id="bbe38-119">Paket kaynağından kullanılabilir bir güncelleştirme olan paketleri listeler.</span><span class="sxs-lookup"><span data-stu-id="bbe38-119">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="bbe38-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="bbe38-120">ProjectName</span></span> | <span data-ttu-id="bbe38-121">Yüklü paketlerin alınacağı proje.</span><span class="sxs-lookup"><span data-stu-id="bbe38-121">The project from which to get installed packages.</span></span> <span data-ttu-id="bbe38-122">Atlanırsa, tüm çözüm için yüklü projeleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="bbe38-122">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="bbe38-123">Filtre</span><span class="sxs-lookup"><span data-stu-id="bbe38-123">Filter</span></span> | <span data-ttu-id="bbe38-124">Paket KIMLIĞINE, açıklamaya ve etiketlere uygulayarak paket listesini daraltmak için kullanılan bir filtre dizesi.</span><span class="sxs-lookup"><span data-stu-id="bbe38-124">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="bbe38-125">Birinci</span><span class="sxs-lookup"><span data-stu-id="bbe38-125">First</span></span> | <span data-ttu-id="bbe38-126">Listenin başından döndürülecek paket sayısı.</span><span class="sxs-lookup"><span data-stu-id="bbe38-126">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="bbe38-127">Belirtilmemişse, varsayılan olarak 50 ' dir.</span><span class="sxs-lookup"><span data-stu-id="bbe38-127">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="bbe38-128">Atla</span><span class="sxs-lookup"><span data-stu-id="bbe38-128">Skip</span></span> | <span data-ttu-id="bbe38-129">&lt;Görüntülenmiş listedeki ilk int &gt; paketleri atlar.</span><span class="sxs-lookup"><span data-stu-id="bbe38-129">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="bbe38-130">AllVersions</span><span class="sxs-lookup"><span data-stu-id="bbe38-130">AllVersions</span></span> | <span data-ttu-id="bbe38-131">Her bir paketin yalnızca en son sürümü yerine tüm kullanılabilir sürümlerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="bbe38-131">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="bbe38-132">Includeönsürümü</span><span class="sxs-lookup"><span data-stu-id="bbe38-132">IncludePrerelease</span></span> | <span data-ttu-id="bbe38-133">Sonuçlarda yayın öncesi paketleri içerir.</span><span class="sxs-lookup"><span data-stu-id="bbe38-133">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="bbe38-134">PageSize</span><span class="sxs-lookup"><span data-stu-id="bbe38-134">PageSize</span></span> | <span data-ttu-id="bbe38-135">*(3.0 +)* -ListAvailable (zorunlu) ile kullanıldığında, devam etmek için bir istem vermeden önce listeye eklenecek paket sayısı.</span><span class="sxs-lookup"><span data-stu-id="bbe38-135">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="bbe38-136">Bu parametrelerin hiçbiri, işlem hattı girişi veya joker karakterler kabul etmez.</span><span class="sxs-lookup"><span data-stu-id="bbe38-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="bbe38-137">Ortak Parametreler</span><span class="sxs-lookup"><span data-stu-id="bbe38-137">Common Parameters</span></span>

<span data-ttu-id="bbe38-138">`Get-Package` Şu [ortak PowerShell parametrelerini](/powershell/module/microsoft.powershell.core/about/about_commonparameters)destekler: Hata Ayıkla, hata eylemi, ErrorVariable, OutBuffer, OutVariable, Pipelinevariable, verbose, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="bbe38-138">`Get-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="bbe38-139">Örnekler</span><span class="sxs-lookup"><span data-stu-id="bbe38-139">Examples</span></span>

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