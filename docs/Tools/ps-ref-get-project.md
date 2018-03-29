---
title: NuGet Get-proje PowerShell başvurusu | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Visual Studio'da NuGet Paket Yöneticisi konsolunda GetProject PowerShell komut başvurusu.
keywords: NuGet Paket Yöneticisi konsolu, NuGet Powershell komutlarını NuGet Powershell başvurusu, Get-proje
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 9fcdcf7c550408cd7dfd73787ee14821c46a1df9
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="dc6eb-104">Get-proje (Visual Studio'da Paket Yöneticisi Konsolu)</span><span class="sxs-lookup"><span data-stu-id="dc6eb-104">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="dc6eb-105">*Yalnızca içinde kullanılabilir [NuGet Paket Yöneticisi Konsolu](package-manager-console.md) Windows Visual Studio'da.*</span><span class="sxs-lookup"><span data-stu-id="dc6eb-105">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="dc6eb-106">Varsayılan ya da belirtilen proje hakkındaki bilgileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="dc6eb-106">Displays information about the default or specified project.</span></span> <span data-ttu-id="dc6eb-107">`Get-Project` özellikle bir tfs'deki projesi için Visual Studio DTE (geliştirme araçları ortamı) nesnesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="dc6eb-107">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="dc6eb-108">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="dc6eb-108">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="dc6eb-109">Parametreler</span><span class="sxs-lookup"><span data-stu-id="dc6eb-109">Parameters</span></span>

| <span data-ttu-id="dc6eb-110">Parametre</span><span class="sxs-lookup"><span data-stu-id="dc6eb-110">Parameter</span></span> | <span data-ttu-id="dc6eb-111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="dc6eb-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="dc6eb-112">Ad</span><span class="sxs-lookup"><span data-stu-id="dc6eb-112">Name</span></span> | <span data-ttu-id="dc6eb-113">Paket Yöneticisi Konsolu'nda seçili olan varsayılan projeyi varsayarak görüntülemek için projeyi belirtir.</span><span class="sxs-lookup"><span data-stu-id="dc6eb-113">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="dc6eb-114">-Name anahtarı kendisini isteğe bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="dc6eb-114">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="dc6eb-115">Tümü</span><span class="sxs-lookup"><span data-stu-id="dc6eb-115">All</span></span> | <span data-ttu-id="dc6eb-116">Çözümdeki her projeye ilgili bilgileri görüntüler; projelerin sırası belirleyici değildir.</span><span class="sxs-lookup"><span data-stu-id="dc6eb-116">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="dc6eb-117">Hiçbiri bu parametre ardışık düzen giriş veya joker karakter kabul edin.</span><span class="sxs-lookup"><span data-stu-id="dc6eb-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="dc6eb-118">Ortak parametreleri</span><span class="sxs-lookup"><span data-stu-id="dc6eb-118">Common Parameters</span></span>

<span data-ttu-id="dc6eb-119">`Get-Project` Aşağıdaki destekleyen [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, ayrıntı, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="dc6eb-119">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="dc6eb-120">Örnekler</span><span class="sxs-lookup"><span data-stu-id="dc6eb-120">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```