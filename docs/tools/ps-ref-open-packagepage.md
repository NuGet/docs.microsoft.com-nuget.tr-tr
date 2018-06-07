---
title: NuGet Aç-PackagePage PowerShell başvurusu
description: Visual Studio'da NuGet Paket Yöneticisi konsolunda Aç PackagePage PowerShell komut başvurusu.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: e64a83c01a7baac330c99fe40ba52f328a2133b8
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817726"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="87b3f-103">Open-PackagePage (Visual Studio'da Paket Yöneticisi Konsolu)</span><span class="sxs-lookup"><span data-stu-id="87b3f-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="87b3f-104">*3.0 + kullanım dışı; yalnızca içinde kullanılabilir [NuGet Paket Yöneticisi Konsolu](package-manager-console.md) Windows Visual Studio'da.*</span><span class="sxs-lookup"><span data-stu-id="87b3f-104">*Deprecated in 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="87b3f-105">Proje, lisans veya belirtilen paket için rapor kötüye URL'si ile varsayılan tarayıcı başlatır.</span><span class="sxs-lookup"><span data-stu-id="87b3f-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="87b3f-106">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="87b3f-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="87b3f-107">Parametreler</span><span class="sxs-lookup"><span data-stu-id="87b3f-107">Parameters</span></span>

| <span data-ttu-id="87b3f-108">Parametre</span><span class="sxs-lookup"><span data-stu-id="87b3f-108">Parameter</span></span> | <span data-ttu-id="87b3f-109">Açıklama</span><span class="sxs-lookup"><span data-stu-id="87b3f-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="87b3f-110">Kimliği</span><span class="sxs-lookup"><span data-stu-id="87b3f-110">Id</span></span> | <span data-ttu-id="87b3f-111">İstenen paketin paket Kimliğini.</span><span class="sxs-lookup"><span data-stu-id="87b3f-111">The package ID of the desired package.</span></span> <span data-ttu-id="87b3f-112">Kimliği anahtarı kendisini isteğe bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="87b3f-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="87b3f-113">Sürüm</span><span class="sxs-lookup"><span data-stu-id="87b3f-113">Version</span></span> | <span data-ttu-id="87b3f-114">En son sürüm varsayılan değer olarak paketin sürümü.</span><span class="sxs-lookup"><span data-stu-id="87b3f-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="87b3f-115">Kaynak</span><span class="sxs-lookup"><span data-stu-id="87b3f-115">Source</span></span> | <span data-ttu-id="87b3f-116">Seçili kaynağı aşağı açılan kaynağındaki varsayılan değer olarak paket kaynağı.</span><span class="sxs-lookup"><span data-stu-id="87b3f-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="87b3f-117">Lisans</span><span class="sxs-lookup"><span data-stu-id="87b3f-117">License</span></span> | <span data-ttu-id="87b3f-118">Paketin lisans URL'sini tarayıcı penceresinde açar.</span><span class="sxs-lookup"><span data-stu-id="87b3f-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="87b3f-119">-Lisans ne - ReportAbuse belirtilirse, tarayıcı paketin proje URL'sini açar.</span><span class="sxs-lookup"><span data-stu-id="87b3f-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="87b3f-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="87b3f-120">ReportAbuse</span></span> | <span data-ttu-id="87b3f-121">Paketin rapor kötüye URL'si tarayıcıda açılır.</span><span class="sxs-lookup"><span data-stu-id="87b3f-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="87b3f-122">-Lisans ne - ReportAbuse belirtilirse, tarayıcı paketin proje URL'sini açar.</span><span class="sxs-lookup"><span data-stu-id="87b3f-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="87b3f-123">Geçiş</span><span class="sxs-lookup"><span data-stu-id="87b3f-123">PassThru</span></span> | <span data-ttu-id="87b3f-124">URL'yi görüntüler; Tarayıcı açma bastırmak için - whatIf kullanın.</span><span class="sxs-lookup"><span data-stu-id="87b3f-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="87b3f-125">Hiçbiri bu parametre ardışık düzen giriş veya joker karakter kabul edin.</span><span class="sxs-lookup"><span data-stu-id="87b3f-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="87b3f-126">Ortak parametreleri</span><span class="sxs-lookup"><span data-stu-id="87b3f-126">Common Parameters</span></span>

<span data-ttu-id="87b3f-127">`Open-PackagePage` Aşağıdaki destekleyen [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, ayrıntı, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="87b3f-127">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="87b3f-128">Örnekler</span><span class="sxs-lookup"><span data-stu-id="87b3f-128">Examples</span></span>

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