---
title: NuGet Get-Project PowerShell Başvurusu
description: Visual Studio 'daki NuGet Paket Yöneticisi konsolundaki GetProject PowerShell komutu için başvuru.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 830746f032bb4eb916508ef320c5b3d0486b89a4
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328212"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="feecb-103">Get-Project (Visual Studio'da Paket Yöneticisi Konsolu)</span><span class="sxs-lookup"><span data-stu-id="feecb-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="feecb-104">*Yalnızca Windows üzerinde Visual Studio 'da bulunan [Paket Yöneticisi konsolu](../../consume-packages/install-use-packages-powershell.md) içinde kullanılabilir.*</span><span class="sxs-lookup"><span data-stu-id="feecb-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="feecb-105">Varsayılan veya belirtilen proje hakkındaki bilgileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="feecb-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="feecb-106">`Get-Project`Özellikle, projenin Visual Studio DTE (geliştirme araçları ortamı) nesnesine bir başvuru döndürür.</span><span class="sxs-lookup"><span data-stu-id="feecb-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="feecb-107">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="feecb-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="feecb-108">Parametreler</span><span class="sxs-lookup"><span data-stu-id="feecb-108">Parameters</span></span>

| <span data-ttu-id="feecb-109">Parametre</span><span class="sxs-lookup"><span data-stu-id="feecb-109">Parameter</span></span> | <span data-ttu-id="feecb-110">Açıklama</span><span class="sxs-lookup"><span data-stu-id="feecb-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="feecb-111">Ad</span><span class="sxs-lookup"><span data-stu-id="feecb-111">Name</span></span> | <span data-ttu-id="feecb-112">Görüntülenecek projeyi, varsayılan projenin Paket Yöneticisi konsolunda seçili olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="feecb-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="feecb-113">-Name anahtarının kendisi isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="feecb-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="feecb-114">Tümü</span><span class="sxs-lookup"><span data-stu-id="feecb-114">All</span></span> | <span data-ttu-id="feecb-115">Çözümdeki her proje için bilgi görüntüler; projelerin sırası belirleyici değildir.</span><span class="sxs-lookup"><span data-stu-id="feecb-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="feecb-116">Bu parametrelerin hiçbiri, işlem hattı girişi veya joker karakterler kabul etmez.</span><span class="sxs-lookup"><span data-stu-id="feecb-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="feecb-117">Ortak Parametreler</span><span class="sxs-lookup"><span data-stu-id="feecb-117">Common Parameters</span></span>

<span data-ttu-id="feecb-118">`Get-Project`Aşağıdaki [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216)destekler: Hata Ayıkla, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, verbose, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="feecb-118">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="feecb-119">Örnekler</span><span class="sxs-lookup"><span data-stu-id="feecb-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```