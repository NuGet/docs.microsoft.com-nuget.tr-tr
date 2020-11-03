---
title: NuGet Get-Project PowerShell Başvurusu
description: Visual Studio 'daki NuGet Paket Yöneticisi konsolundaki GetProject PowerShell komutu için başvuru.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 6d9e1d48c8e1838f193878cab3483b1bfba7d7f0
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238081"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="e7e50-103">Get-Project (Visual Studio 'da Paket Yöneticisi konsolu)</span><span class="sxs-lookup"><span data-stu-id="e7e50-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="e7e50-104">*Yalnızca Windows üzerinde Visual Studio 'da bulunan [Paket Yöneticisi konsolu](../../consume-packages/install-use-packages-powershell.md) içinde kullanılabilir.*</span><span class="sxs-lookup"><span data-stu-id="e7e50-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="e7e50-105">Varsayılan veya belirtilen proje hakkındaki bilgileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="e7e50-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="e7e50-106">`Get-Project` Özellikle, projenin Visual Studio DTE (geliştirme araçları ortamı) nesnesine bir başvuru döndürür.</span><span class="sxs-lookup"><span data-stu-id="e7e50-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="e7e50-107">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="e7e50-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="e7e50-108">Parametreler</span><span class="sxs-lookup"><span data-stu-id="e7e50-108">Parameters</span></span>

| <span data-ttu-id="e7e50-109">Parametre</span><span class="sxs-lookup"><span data-stu-id="e7e50-109">Parameter</span></span> | <span data-ttu-id="e7e50-110">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e7e50-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e7e50-111">Ad</span><span class="sxs-lookup"><span data-stu-id="e7e50-111">Name</span></span> | <span data-ttu-id="e7e50-112">Görüntülenecek projeyi, varsayılan projenin Paket Yöneticisi konsolunda seçili olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="e7e50-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="e7e50-113">-Name anahtarının kendisi isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="e7e50-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="e7e50-114">Tümü</span><span class="sxs-lookup"><span data-stu-id="e7e50-114">All</span></span> | <span data-ttu-id="e7e50-115">Çözümdeki her proje için bilgi görüntüler; projelerin sırası belirleyici değildir.</span><span class="sxs-lookup"><span data-stu-id="e7e50-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="e7e50-116">Bu parametrelerin hiçbiri, işlem hattı girişi veya joker karakterler kabul etmez.</span><span class="sxs-lookup"><span data-stu-id="e7e50-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="e7e50-117">Ortak Parametreler</span><span class="sxs-lookup"><span data-stu-id="e7e50-117">Common Parameters</span></span>

<span data-ttu-id="e7e50-118">`Get-Project` Şu [ortak PowerShell parametrelerini](/powershell/module/microsoft.powershell.core/about/about_commonparameters)destekler: Hata Ayıkla, hata eylemi, ErrorVariable, OutBuffer, OutVariable, Pipelinevariable, verbose, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="e7e50-118">`Get-Project` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="e7e50-119">Örnekler</span><span class="sxs-lookup"><span data-stu-id="e7e50-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```