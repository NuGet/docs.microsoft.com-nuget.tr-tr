---
title: NuGet Sync-Package PowerShell Başvurusu
description: Visual Studio 'daki NuGet Paket Yöneticisi konsolundaki Sync-Package PowerShell komutu için başvuru.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a48a09a27b6db9b774e59b9a10652067179e2c27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328197"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="93c75-103">Sync-Package (Visual Studio'da Paket Yöneticisi Konsolu)</span><span class="sxs-lookup"><span data-stu-id="93c75-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="93c75-104">*Sürüm 3.0 +; yalnızca Windows üzerinde Visual Studio 'da bulunan [Paket Yöneticisi konsolu](../../consume-packages/install-use-packages-powershell.md) içinde kullanılabilir.*</span><span class="sxs-lookup"><span data-stu-id="93c75-104">*Version 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="93c75-105">Belirtilen (veya varsayılan) projeden yüklü paketin sürümünü alır ve sürümü çözümdeki diğer projelere eşitler.</span><span class="sxs-lookup"><span data-stu-id="93c75-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="93c75-106">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="93c75-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="93c75-107">Parametreler</span><span class="sxs-lookup"><span data-stu-id="93c75-107">Parameters</span></span>

| <span data-ttu-id="93c75-108">Parametre</span><span class="sxs-lookup"><span data-stu-id="93c75-108">Parameter</span></span> | <span data-ttu-id="93c75-109">Açıklama</span><span class="sxs-lookup"><span data-stu-id="93c75-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="93c75-110">Id</span><span class="sxs-lookup"><span data-stu-id="93c75-110">Id</span></span> | <span data-ttu-id="93c75-111">Istenir Eşitlenecek paketin tanımlayıcısı. -ID anahtarı isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="93c75-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="93c75-112">Ignoredependencies</span><span class="sxs-lookup"><span data-stu-id="93c75-112">IgnoreDependencies</span></span> | <span data-ttu-id="93c75-113">Yalnızca bu paketi yükler ve bağımlılıklarını değil.</span><span class="sxs-lookup"><span data-stu-id="93c75-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="93c75-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="93c75-114">ProjectName</span></span> | <span data-ttu-id="93c75-115">Paketi eşitlenecek proje, varsayılan proje varsayılan olarak varsayılan projem.</span><span class="sxs-lookup"><span data-stu-id="93c75-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="93c75-116">Sürüm</span><span class="sxs-lookup"><span data-stu-id="93c75-116">Version</span></span> | <span data-ttu-id="93c75-117">Eşitlenecek paketin sürümü, şu anda yüklü olan sürüme dönülüyor.</span><span class="sxs-lookup"><span data-stu-id="93c75-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="93c75-118">Source</span><span class="sxs-lookup"><span data-stu-id="93c75-118">Source</span></span> | <span data-ttu-id="93c75-119">Aranacak paket kaynağının URL veya klasör yolu.</span><span class="sxs-lookup"><span data-stu-id="93c75-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="93c75-120">Yerel klasör yolları mutlak veya geçerli klasöre göreli olabilir.</span><span class="sxs-lookup"><span data-stu-id="93c75-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="93c75-121">Atlanırsa, `Sync-Package` Şu anda seçili olan paket kaynağını arar.</span><span class="sxs-lookup"><span data-stu-id="93c75-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="93c75-122">Includeönsürümü</span><span class="sxs-lookup"><span data-stu-id="93c75-122">IncludePrerelease</span></span> | <span data-ttu-id="93c75-123">Eşitlenmiş yayın öncesi paketleri içerir.</span><span class="sxs-lookup"><span data-stu-id="93c75-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="93c75-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="93c75-124">FileConflictAction</span></span> | <span data-ttu-id="93c75-125">Proje tarafından başvurulan var olan dosyaların üzerine yazılması veya yoksayılması istendiğinde gerçekleştirilecek eylem.</span><span class="sxs-lookup"><span data-stu-id="93c75-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="93c75-126">Olası değerler *üzerine yazılır, Yoksay, None, overwriteall*ve *(3,0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="93c75-126">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="93c75-127">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="93c75-127">DependencyVersion</span></span> | <span data-ttu-id="93c75-128">Kullanılacak bağımlılık paketlerinin sürümü, bu, aşağıdakilerden biri olabilir:</span><span class="sxs-lookup"><span data-stu-id="93c75-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="93c75-129">*En düşük* (varsayılan): en düşük sürüm</span><span class="sxs-lookup"><span data-stu-id="93c75-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="93c75-130">*HighestPatch*: en düşük ana, en düşük ikincil, en yüksek düzeltme eki olan sürüm</span><span class="sxs-lookup"><span data-stu-id="93c75-130">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="93c75-131">*HighestMinor*: en düşük ana, en yüksek ikincil, en yüksek düzeltme eki olan sürüm</span><span class="sxs-lookup"><span data-stu-id="93c75-131">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="93c75-132">*En yüksek* (parametresi olmayan Update-Package için varsayılan): en yüksek sürüm</span><span class="sxs-lookup"><span data-stu-id="93c75-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="93c75-133">Varsayılan değeri, [`dependencyVersion`](../nuget-config-file.md#config-section) `Nuget.Config` dosyadaki ayarını kullanarak ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="93c75-133">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="93c75-134">WhatIf</span><span class="sxs-lookup"><span data-stu-id="93c75-134">WhatIf</span></span> | <span data-ttu-id="93c75-135">Komutu, eşitlemeyi gerçekten gerçekleştirmeden çalışırken ne olacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="93c75-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="93c75-136">Bu parametrelerin hiçbiri, işlem hattı girişi veya joker karakterler kabul etmez.</span><span class="sxs-lookup"><span data-stu-id="93c75-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="93c75-137">Ortak Parametreler</span><span class="sxs-lookup"><span data-stu-id="93c75-137">Common Parameters</span></span>

<span data-ttu-id="93c75-138">`Sync-Package`Aşağıdaki [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216)destekler: Hata Ayıkla, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, verbose, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="93c75-138">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="93c75-139">Örnekler</span><span class="sxs-lookup"><span data-stu-id="93c75-139">Examples</span></span>

```ps
# Sync the Elmah package installed in the default project into the other projects in the solution
Sync-Package Elmah

# Sync the Elmah package installed in the ClassLibrary1 project into other projects in the solution
Sync-Package Elmah -ProjectName ClassLibrary1

# Sync Microsoft.Aspnet.package but not its dependencies into the other projects in the solution
Sync-Package Microsoft.Aspnet.Mvc -IgnoreDependencies

# Sync jQuery.Validation and install the highest version of jQuery (a dependency) from the package source    
Sync-Package jQuery.Validation -DependencyVersion highest
```
