---
title: NuGet açık PackagePage PowerShell Başvurusu
description: Visual Studio 'daki NuGet Paket Yöneticisi konsolunda Open-PackagePage PowerShell komutu için başvuru.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 39199ebfc37756ed40158a1c07afca7709067350
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384434"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="1c0ad-103">Open-PackagePage (Visual Studio'da Paket Yöneticisi Konsolu)</span><span class="sxs-lookup"><span data-stu-id="1c0ad-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="1c0ad-104">*3.0 + ' da kullanımdan kaldırılmıştır; yalnızca Windows üzerinde Visual Studio 'da bulunan [Paket Yöneticisi konsolu](../../consume-packages/install-use-packages-powershell.md) içinde kullanılabilir.*</span><span class="sxs-lookup"><span data-stu-id="1c0ad-104">*Deprecated in 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="1c0ad-105">Belirtilen paket için proje, lisans veya uygunsuz kullanım URL 'SI ile varsayılan tarayıcıyı başlatır.</span><span class="sxs-lookup"><span data-stu-id="1c0ad-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="1c0ad-106">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="1c0ad-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="1c0ad-107">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c0ad-107">Parameters</span></span>

| <span data-ttu-id="1c0ad-108">Parametre</span><span class="sxs-lookup"><span data-stu-id="1c0ad-108">Parameter</span></span> | <span data-ttu-id="1c0ad-109">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1c0ad-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1c0ad-110">Id</span><span class="sxs-lookup"><span data-stu-id="1c0ad-110">Id</span></span> | <span data-ttu-id="1c0ad-111">İstenen paketin paket KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="1c0ad-111">The package ID of the desired package.</span></span> <span data-ttu-id="1c0ad-112">-ID anahtarı isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="1c0ad-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="1c0ad-113">Sürüm</span><span class="sxs-lookup"><span data-stu-id="1c0ad-113">Version</span></span> | <span data-ttu-id="1c0ad-114">Paketin sürümü, en son sürümü varsayılan olarak sağlar.</span><span class="sxs-lookup"><span data-stu-id="1c0ad-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="1c0ad-115">Kaynak</span><span class="sxs-lookup"><span data-stu-id="1c0ad-115">Source</span></span> | <span data-ttu-id="1c0ad-116">Kaynak açılan kutusunda seçilen kaynağı varsayılan olarak, paket kaynağı.</span><span class="sxs-lookup"><span data-stu-id="1c0ad-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="1c0ad-117">Lisans</span><span class="sxs-lookup"><span data-stu-id="1c0ad-117">License</span></span> | <span data-ttu-id="1c0ad-118">Tarayıcıyı paketin lisans URL 'SI için açar.</span><span class="sxs-lookup"><span data-stu-id="1c0ad-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="1c0ad-119">Lisans ya da-ReportAbuse belirtilmediyse, tarayıcı paketin proje URL 'sini açar.</span><span class="sxs-lookup"><span data-stu-id="1c0ad-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="1c0ad-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="1c0ad-120">ReportAbuse</span></span> | <span data-ttu-id="1c0ad-121">Tarayıcıyı paketin uygunsuz kullanım URL 'SI için açar.</span><span class="sxs-lookup"><span data-stu-id="1c0ad-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="1c0ad-122">Lisans ya da-ReportAbuse belirtilmediyse, tarayıcı paketin proje URL 'sini açar.</span><span class="sxs-lookup"><span data-stu-id="1c0ad-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="1c0ad-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="1c0ad-123">PassThru</span></span> | <span data-ttu-id="1c0ad-124">URL 'YI görüntüler; tarayıcının açılmasını engellemek için-whatIf ile kullanın.</span><span class="sxs-lookup"><span data-stu-id="1c0ad-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="1c0ad-125">Bu parametrelerin hiçbiri, işlem hattı girişi veya joker karakterler kabul etmez.</span><span class="sxs-lookup"><span data-stu-id="1c0ad-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="1c0ad-126">Ortak Parametreler</span><span class="sxs-lookup"><span data-stu-id="1c0ad-126">Common Parameters</span></span>

<span data-ttu-id="1c0ad-127">`Open-PackagePage`, şu [ortak PowerShell parametrelerini](https://go.microsoft.com/fwlink/?LinkID=113216)destekler: Hata Ayıkla, hata eylemi, ErrorVariable, OutBuffer, OutVariable, Pipelinevariable, verbose, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="1c0ad-127">`Open-PackagePage` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="1c0ad-128">Örnekler</span><span class="sxs-lookup"><span data-stu-id="1c0ad-128">Examples</span></span>

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