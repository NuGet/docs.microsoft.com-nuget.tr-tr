---
title: "NuGet Aç-PackagePage PowerShell başvurusu | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Visual Studio'da NuGet Paket Yöneticisi konsolunda Aç PackagePage PowerShell komut başvurusu."
keywords: "NuGet Paket Yöneticisi konsolu, NuGet Powershell komutlarını NuGet Powershell başvurusu, açık PackagePage"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 389bad37940f05dd864adfc06080bf746464365d
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2018
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="2d1e8-104">Açık PackagePage (Visual Studio'da Paket Yöneticisi Konsolu)</span><span class="sxs-lookup"><span data-stu-id="2d1e8-104">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="2d1e8-105">*3.0 + kullanım dışı; yalnızca içinde kullanılabilir [NuGet Paket Yöneticisi Konsolu](Package-Manager-Console.md) Windows Visual Studio'da.*</span><span class="sxs-lookup"><span data-stu-id="2d1e8-105">*Deprecated in 3.0+; available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="2d1e8-106">Proje, lisans veya belirtilen paket için rapor kötüye URL'si ile varsayılan tarayıcı başlatır.</span><span class="sxs-lookup"><span data-stu-id="2d1e8-106">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="2d1e8-107">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="2d1e8-107">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="2d1e8-108">Parametreler</span><span class="sxs-lookup"><span data-stu-id="2d1e8-108">Parameters</span></span>

| <span data-ttu-id="2d1e8-109">Parametre</span><span class="sxs-lookup"><span data-stu-id="2d1e8-109">Parameter</span></span> | <span data-ttu-id="2d1e8-110">Açıklama</span><span class="sxs-lookup"><span data-stu-id="2d1e8-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2d1e8-111">Kimliği</span><span class="sxs-lookup"><span data-stu-id="2d1e8-111">Id</span></span> | <span data-ttu-id="2d1e8-112">İstenen paketin paket Kimliğini.</span><span class="sxs-lookup"><span data-stu-id="2d1e8-112">The package ID of the desired package.</span></span> <span data-ttu-id="2d1e8-113">Kimliği anahtarı kendisini isteğe bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="2d1e8-113">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="2d1e8-114">Sürüm</span><span class="sxs-lookup"><span data-stu-id="2d1e8-114">Version</span></span> | <span data-ttu-id="2d1e8-115">En son sürüm varsayılan değer olarak paketin sürümü.</span><span class="sxs-lookup"><span data-stu-id="2d1e8-115">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="2d1e8-116">Kaynak</span><span class="sxs-lookup"><span data-stu-id="2d1e8-116">Source</span></span> | <span data-ttu-id="2d1e8-117">Seçili kaynağı aşağı açılan kaynağındaki varsayılan değer olarak paket kaynağı.</span><span class="sxs-lookup"><span data-stu-id="2d1e8-117">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="2d1e8-118">Lisans</span><span class="sxs-lookup"><span data-stu-id="2d1e8-118">License</span></span> | <span data-ttu-id="2d1e8-119">Paketin lisans URL'sini tarayıcı penceresinde açar.</span><span class="sxs-lookup"><span data-stu-id="2d1e8-119">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="2d1e8-120">-Lisans ne - ReportAbuse belirtilirse, tarayıcı paketin proje URL'sini açar.</span><span class="sxs-lookup"><span data-stu-id="2d1e8-120">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="2d1e8-121">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="2d1e8-121">ReportAbuse</span></span> | <span data-ttu-id="2d1e8-122">Paketin rapor kötüye URL'si tarayıcıda açılır.</span><span class="sxs-lookup"><span data-stu-id="2d1e8-122">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="2d1e8-123">-Lisans ne - ReportAbuse belirtilirse, tarayıcı paketin proje URL'sini açar.</span><span class="sxs-lookup"><span data-stu-id="2d1e8-123">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="2d1e8-124">Geçiş</span><span class="sxs-lookup"><span data-stu-id="2d1e8-124">PassThru</span></span> | <span data-ttu-id="2d1e8-125">URL'yi görüntüler; Tarayıcı açma bastırmak için - whatIf kullanın.</span><span class="sxs-lookup"><span data-stu-id="2d1e8-125">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="2d1e8-126">Hiçbiri bu parametre ardışık düzen giriş veya joker karakter kabul edin.</span><span class="sxs-lookup"><span data-stu-id="2d1e8-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="2d1e8-127">Ortak parametreleri</span><span class="sxs-lookup"><span data-stu-id="2d1e8-127">Common Parameters</span></span>

<span data-ttu-id="2d1e8-128">`Open-PackagePage`Aşağıdaki destekleyen [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, ayrıntı, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="2d1e8-128">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="2d1e8-129">Örnekler</span><span class="sxs-lookup"><span data-stu-id="2d1e8-129">Examples</span></span>

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