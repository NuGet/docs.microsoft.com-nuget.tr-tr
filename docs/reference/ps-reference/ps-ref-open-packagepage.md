---
title: NuGet Open-PackagePage PowerShell Başvurusu
description: Visual Studio 'daki NuGet Paket Yöneticisi konsolundaki Open-PackagePage PowerShell komutuna yönelik başvuru.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: ba90e09c017ec66d73c35a60025474bc77cf65a7
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238068"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="d8286-103">Open-PackagePage (Visual Studio 'da Paket Yöneticisi konsolu)</span><span class="sxs-lookup"><span data-stu-id="d8286-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="d8286-104">*3.0 + ' da kullanımdan kaldırılmıştır; yalnızca Windows üzerinde Visual Studio 'da bulunan [Paket Yöneticisi konsolu](../../consume-packages/install-use-packages-powershell.md) içinde kullanılabilir.*</span><span class="sxs-lookup"><span data-stu-id="d8286-104">*Deprecated in 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="d8286-105">Belirtilen paket için proje, lisans veya uygunsuz kullanım URL 'SI ile varsayılan tarayıcıyı başlatır.</span><span class="sxs-lookup"><span data-stu-id="d8286-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="d8286-106">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="d8286-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="d8286-107">Parametreler</span><span class="sxs-lookup"><span data-stu-id="d8286-107">Parameters</span></span>

| <span data-ttu-id="d8286-108">Parametre</span><span class="sxs-lookup"><span data-stu-id="d8286-108">Parameter</span></span> | <span data-ttu-id="d8286-109">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d8286-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d8286-110">Id</span><span class="sxs-lookup"><span data-stu-id="d8286-110">Id</span></span> | <span data-ttu-id="d8286-111">İstenen paketin paket KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="d8286-111">The package ID of the desired package.</span></span> <span data-ttu-id="d8286-112">-ID anahtarı isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="d8286-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="d8286-113">Sürüm</span><span class="sxs-lookup"><span data-stu-id="d8286-113">Version</span></span> | <span data-ttu-id="d8286-114">Paketin sürümü, en son sürümü varsayılan olarak sağlar.</span><span class="sxs-lookup"><span data-stu-id="d8286-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="d8286-115">Kaynak</span><span class="sxs-lookup"><span data-stu-id="d8286-115">Source</span></span> | <span data-ttu-id="d8286-116">Kaynak açılan kutusunda seçilen kaynağı varsayılan olarak, paket kaynağı.</span><span class="sxs-lookup"><span data-stu-id="d8286-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="d8286-117">Lisans</span><span class="sxs-lookup"><span data-stu-id="d8286-117">License</span></span> | <span data-ttu-id="d8286-118">Tarayıcıyı paketin lisans URL 'SI için açar.</span><span class="sxs-lookup"><span data-stu-id="d8286-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="d8286-119">Lisans ya da-ReportAbuse belirtilmediyse, tarayıcı paketin proje URL 'sini açar.</span><span class="sxs-lookup"><span data-stu-id="d8286-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="d8286-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="d8286-120">ReportAbuse</span></span> | <span data-ttu-id="d8286-121">Tarayıcıyı paketin uygunsuz kullanım URL 'SI için açar.</span><span class="sxs-lookup"><span data-stu-id="d8286-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="d8286-122">Lisans ya da-ReportAbuse belirtilmediyse, tarayıcı paketin proje URL 'sini açar.</span><span class="sxs-lookup"><span data-stu-id="d8286-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="d8286-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="d8286-123">PassThru</span></span> | <span data-ttu-id="d8286-124">URL 'YI görüntüler; tarayıcının açılmasını engellemek için-whatIf ile kullanın.</span><span class="sxs-lookup"><span data-stu-id="d8286-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="d8286-125">Bu parametrelerin hiçbiri, işlem hattı girişi veya joker karakterler kabul etmez.</span><span class="sxs-lookup"><span data-stu-id="d8286-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="d8286-126">Ortak Parametreler</span><span class="sxs-lookup"><span data-stu-id="d8286-126">Common Parameters</span></span>

<span data-ttu-id="d8286-127">`Open-PackagePage` Şu [ortak PowerShell parametrelerini](/powershell/module/microsoft.powershell.core/about/about_commonparameters)destekler: Hata Ayıkla, hata eylemi, ErrorVariable, OutBuffer, OutVariable, Pipelinevariable, verbose, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="d8286-127">`Open-PackagePage` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="d8286-128">Örnekler</span><span class="sxs-lookup"><span data-stu-id="d8286-128">Examples</span></span>

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