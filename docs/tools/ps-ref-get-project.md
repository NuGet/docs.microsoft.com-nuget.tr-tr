---
title: NuGet Get-proje PowerShell başvurusu
description: Visual Studio'da NuGet Paket Yöneticisi konsolunda GetProject PowerShell komut başvurusu.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: afdf9f762bbd34531f9d9093238a2fed27e3f4d3
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817762"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="3d8b7-103">Get-Project (Visual Studio'da Paket Yöneticisi Konsolu)</span><span class="sxs-lookup"><span data-stu-id="3d8b7-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="3d8b7-104">*Yalnızca içinde kullanılabilir [NuGet Paket Yöneticisi Konsolu](package-manager-console.md) Windows Visual Studio'da.*</span><span class="sxs-lookup"><span data-stu-id="3d8b7-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="3d8b7-105">Varsayılan ya da belirtilen proje hakkındaki bilgileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="3d8b7-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="3d8b7-106">`Get-Project` özellikle bir tfs'deki projesi için Visual Studio DTE (geliştirme araçları ortamı) nesnesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d8b7-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="3d8b7-107">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="3d8b7-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="3d8b7-108">Parametreler</span><span class="sxs-lookup"><span data-stu-id="3d8b7-108">Parameters</span></span>

| <span data-ttu-id="3d8b7-109">Parametre</span><span class="sxs-lookup"><span data-stu-id="3d8b7-109">Parameter</span></span> | <span data-ttu-id="3d8b7-110">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3d8b7-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3d8b7-111">Ad</span><span class="sxs-lookup"><span data-stu-id="3d8b7-111">Name</span></span> | <span data-ttu-id="3d8b7-112">Paket Yöneticisi Konsolu'nda seçili olan varsayılan projeyi varsayarak görüntülemek için projeyi belirtir.</span><span class="sxs-lookup"><span data-stu-id="3d8b7-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="3d8b7-113">-Name anahtarı kendisini isteğe bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="3d8b7-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="3d8b7-114">Tümü</span><span class="sxs-lookup"><span data-stu-id="3d8b7-114">All</span></span> | <span data-ttu-id="3d8b7-115">Çözümdeki her projeye ilgili bilgileri görüntüler; projelerin sırası belirleyici değildir.</span><span class="sxs-lookup"><span data-stu-id="3d8b7-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="3d8b7-116">Hiçbiri bu parametre ardışık düzen giriş veya joker karakter kabul edin.</span><span class="sxs-lookup"><span data-stu-id="3d8b7-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="3d8b7-117">Ortak parametreleri</span><span class="sxs-lookup"><span data-stu-id="3d8b7-117">Common Parameters</span></span>

<span data-ttu-id="3d8b7-118">`Get-Project` Aşağıdaki destekleyen [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, ayrıntı, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="3d8b7-118">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="3d8b7-119">Örnekler</span><span class="sxs-lookup"><span data-stu-id="3d8b7-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```