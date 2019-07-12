---
title: NuGet açık-PackagePage PowerShell başvurusu
description: Visual Studio'da NuGet Paket Yöneticisi konsolu aç PackagePage PowerShell komutunda referansı.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: fd738f15b461051c4e9413b3035456c687979b97
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842261"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="15ce2-103">Open-PackagePage (Visual Studio'da Paket Yöneticisi Konsolu)</span><span class="sxs-lookup"><span data-stu-id="15ce2-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="15ce2-104">*3.0 +'da kullanım dışı; yalnızca içinde kullanılabilir [Paket Yöneticisi Konsolu](package-manager-console.md) Windows üzerinde Visual Studio'da.*</span><span class="sxs-lookup"><span data-stu-id="15ce2-104">*Deprecated in 3.0+; available only within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="15ce2-105">Proje, lisans veya rapor Uygunsuz kullanım bildirme URL'si belirtilen paket için varsayılan tarayıcıda başlatır.</span><span class="sxs-lookup"><span data-stu-id="15ce2-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="15ce2-106">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="15ce2-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="15ce2-107">Parametreler</span><span class="sxs-lookup"><span data-stu-id="15ce2-107">Parameters</span></span>

| <span data-ttu-id="15ce2-108">Parametre</span><span class="sxs-lookup"><span data-stu-id="15ce2-108">Parameter</span></span> | <span data-ttu-id="15ce2-109">Açıklama</span><span class="sxs-lookup"><span data-stu-id="15ce2-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="15ce2-110">Id</span><span class="sxs-lookup"><span data-stu-id="15ce2-110">Id</span></span> | <span data-ttu-id="15ce2-111">İstenen paketin paket kimliği.</span><span class="sxs-lookup"><span data-stu-id="15ce2-111">The package ID of the desired package.</span></span> <span data-ttu-id="15ce2-112">Kimliği anahtarın kendisinde, isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="15ce2-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="15ce2-113">Sürüm</span><span class="sxs-lookup"><span data-stu-id="15ce2-113">Version</span></span> | <span data-ttu-id="15ce2-114">En son sürüme varsayarak paketinin sürümü.</span><span class="sxs-lookup"><span data-stu-id="15ce2-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="15ce2-115">Source</span><span class="sxs-lookup"><span data-stu-id="15ce2-115">Source</span></span> | <span data-ttu-id="15ce2-116">Aşağı açılan kaynakta seçilen kaynak varsayarak paketinin kaynağı.</span><span class="sxs-lookup"><span data-stu-id="15ce2-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="15ce2-117">Lisans</span><span class="sxs-lookup"><span data-stu-id="15ce2-117">License</span></span> | <span data-ttu-id="15ce2-118">Paketin lisans URL'si için bir tarayıcı açar.</span><span class="sxs-lookup"><span data-stu-id="15ce2-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="15ce2-119">-Lisans ne - ReportAbuse belirtilirse, tarayıcı paketin proje URL'sini açar.</span><span class="sxs-lookup"><span data-stu-id="15ce2-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="15ce2-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="15ce2-120">ReportAbuse</span></span> | <span data-ttu-id="15ce2-121">Paketin rapor Uygunsuz kullanım bildirme URL'si için bir tarayıcı açar.</span><span class="sxs-lookup"><span data-stu-id="15ce2-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="15ce2-122">-Lisans ne - ReportAbuse belirtilirse, tarayıcı paketin proje URL'sini açar.</span><span class="sxs-lookup"><span data-stu-id="15ce2-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="15ce2-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="15ce2-123">PassThru</span></span> | <span data-ttu-id="15ce2-124">URL'yi görüntüler. -WhatIf ile tarayıcıyı açmalarını engellemek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="15ce2-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="15ce2-125">Hiçbiri bu parametre ardışık düzen giriş veya joker karakterler kabul edin.</span><span class="sxs-lookup"><span data-stu-id="15ce2-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="15ce2-126">Ortak parametreleri</span><span class="sxs-lookup"><span data-stu-id="15ce2-126">Common Parameters</span></span>

<span data-ttu-id="15ce2-127">`Open-PackagePage` şunları desteklemektedir [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): Hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, ayrıntılı PipelineVariable, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="15ce2-127">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="15ce2-128">Örnekler</span><span class="sxs-lookup"><span data-stu-id="15ce2-128">Examples</span></span>

```ps
# Opens a browser with the Ninject package's project page
Open-PackagePage Ninject

# Opens a browser with the Ninject package's license page
Open-PackagePage Ninject -License

# Opens a browser with the Ninject package's report abuse page  
Open-PackagePage Ninject -ReportAbuse

# Assigns the license URL to the variable, $url, without launching the browser
$url = Open-PackagePage Ninject -License -PassThru -WhatIf
```