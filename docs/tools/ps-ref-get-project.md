---
title: NuGet Get-proje PowerShell başvurusu
description: Visual Studio'da NuGet Paket Yöneticisi konsolu GetProject PowerShell komutunda referansı.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 849261711fafcadbab38bf6fe99340c4b79e1e21
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550443"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="f1a4d-103">Get-Project (Visual Studio'da Paket Yöneticisi Konsolu)</span><span class="sxs-lookup"><span data-stu-id="f1a4d-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="f1a4d-104">*Yalnızca içinde kullanılabilir [NuGet Paket Yöneticisi Konsolu](package-manager-console.md) Windows üzerinde Visual Studio'da.*</span><span class="sxs-lookup"><span data-stu-id="f1a4d-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="f1a4d-105">Varsayılan veya belirtilen proje hakkında bilgileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="f1a4d-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="f1a4d-106">`Get-Project` özellikle bir grup projesi için Visual Studio DTE (geliştirme araçları ortamı) nesnesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="f1a4d-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="f1a4d-107">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="f1a4d-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="f1a4d-108">Parametreler</span><span class="sxs-lookup"><span data-stu-id="f1a4d-108">Parameters</span></span>

| <span data-ttu-id="f1a4d-109">Parametre</span><span class="sxs-lookup"><span data-stu-id="f1a4d-109">Parameter</span></span> | <span data-ttu-id="f1a4d-110">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f1a4d-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f1a4d-111">Ad</span><span class="sxs-lookup"><span data-stu-id="f1a4d-111">Name</span></span> | <span data-ttu-id="f1a4d-112">Görüntülenecek, proje, Paket Yöneticisi Konsolu'nda seçili varsayılan proje varsayarak belirtir.</span><span class="sxs-lookup"><span data-stu-id="f1a4d-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="f1a4d-113">Ad anahtarı, kendisi isteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="f1a4d-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="f1a4d-114">Tümü</span><span class="sxs-lookup"><span data-stu-id="f1a4d-114">All</span></span> | <span data-ttu-id="f1a4d-115">Çözümde her proje için bilgileri görüntüler; projelerin sırası belirleyici değildir.</span><span class="sxs-lookup"><span data-stu-id="f1a4d-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="f1a4d-116">Hiçbiri bu parametre ardışık düzen giriş veya joker karakterler kabul edin.</span><span class="sxs-lookup"><span data-stu-id="f1a4d-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="f1a4d-117">Ortak parametreleri</span><span class="sxs-lookup"><span data-stu-id="f1a4d-117">Common Parameters</span></span>

<span data-ttu-id="f1a4d-118">`Get-Project` şunları desteklemektedir [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, ayrıntılı, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="f1a4d-118">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="f1a4d-119">Örnekler</span><span class="sxs-lookup"><span data-stu-id="f1a4d-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```