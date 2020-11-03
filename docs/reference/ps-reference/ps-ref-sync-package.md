---
title: NuGet Sync-Package PowerShell Başvurusu
description: Visual Studio 'daki NuGet Paket Yöneticisi konsolundaki Sync-Package PowerShell komutuna yönelik başvuru.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: fc4c875b5dcb0b90e4d048daf5984ed265370090
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238055"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="63444-103">Sync-Package (Visual Studio 'da Paket Yöneticisi konsolu)</span><span class="sxs-lookup"><span data-stu-id="63444-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="63444-104">*Sürüm 3.0 +; yalnızca Windows üzerinde Visual Studio 'da bulunan [Paket Yöneticisi konsolu](../../consume-packages/install-use-packages-powershell.md) içinde kullanılabilir.*</span><span class="sxs-lookup"><span data-stu-id="63444-104">*Version 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="63444-105">Belirtilen (veya varsayılan) projeden yüklü paketin sürümünü alır ve sürümü çözümdeki diğer projelere eşitler.</span><span class="sxs-lookup"><span data-stu-id="63444-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="63444-106">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="63444-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="63444-107">Parametreler</span><span class="sxs-lookup"><span data-stu-id="63444-107">Parameters</span></span>

| <span data-ttu-id="63444-108">Parametre</span><span class="sxs-lookup"><span data-stu-id="63444-108">Parameter</span></span> | <span data-ttu-id="63444-109">Açıklama</span><span class="sxs-lookup"><span data-stu-id="63444-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="63444-110">Id</span><span class="sxs-lookup"><span data-stu-id="63444-110">Id</span></span> | <span data-ttu-id="63444-111">Istenir Eşitlenecek paketin tanımlayıcısı. -ID anahtarı isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="63444-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="63444-112">Ignoredependencies</span><span class="sxs-lookup"><span data-stu-id="63444-112">IgnoreDependencies</span></span> | <span data-ttu-id="63444-113">Yalnızca bu paketi yükler ve bağımlılıklarını değil.</span><span class="sxs-lookup"><span data-stu-id="63444-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="63444-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="63444-114">ProjectName</span></span> | <span data-ttu-id="63444-115">Paketi eşitlenecek proje, varsayılan proje varsayılan olarak varsayılan projem.</span><span class="sxs-lookup"><span data-stu-id="63444-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="63444-116">Sürüm</span><span class="sxs-lookup"><span data-stu-id="63444-116">Version</span></span> | <span data-ttu-id="63444-117">Eşitlenecek paketin sürümü, şu anda yüklü olan sürüme dönülüyor.</span><span class="sxs-lookup"><span data-stu-id="63444-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="63444-118">Kaynak</span><span class="sxs-lookup"><span data-stu-id="63444-118">Source</span></span> | <span data-ttu-id="63444-119">Aranacak paket kaynağının URL veya klasör yolu.</span><span class="sxs-lookup"><span data-stu-id="63444-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="63444-120">Yerel klasör yolları mutlak veya geçerli klasöre göreli olabilir.</span><span class="sxs-lookup"><span data-stu-id="63444-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="63444-121">Atlanırsa, `Sync-Package` Şu anda seçili olan paket kaynağını arar.</span><span class="sxs-lookup"><span data-stu-id="63444-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="63444-122">Includeönsürümü</span><span class="sxs-lookup"><span data-stu-id="63444-122">IncludePrerelease</span></span> | <span data-ttu-id="63444-123">Eşitlenmiş yayın öncesi paketleri içerir.</span><span class="sxs-lookup"><span data-stu-id="63444-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="63444-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="63444-124">FileConflictAction</span></span> | <span data-ttu-id="63444-125">Proje tarafından başvurulan var olan dosyaların üzerine yazılması veya yoksayılması istendiğinde gerçekleştirilecek eylem.</span><span class="sxs-lookup"><span data-stu-id="63444-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="63444-126">Olası değerler *üzerine yazılır, Yoksay, None, overwriteall* ve *(3,0 +)* *IgnoreAll* .</span><span class="sxs-lookup"><span data-stu-id="63444-126">Possible values are *Overwrite, Ignore, None, OverwriteAll* , and *(3.0+)* *IgnoreAll* .</span></span> |
| <span data-ttu-id="63444-127">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="63444-127">DependencyVersion</span></span> | <span data-ttu-id="63444-128">Kullanılacak bağımlılık paketlerinin sürümü, bu, aşağıdakilerden biri olabilir:</span><span class="sxs-lookup"><span data-stu-id="63444-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="63444-129">*En düşük* (varsayılan): en düşük sürüm</span><span class="sxs-lookup"><span data-stu-id="63444-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="63444-130">*HighestPatch* : en düşük ana, en düşük ikincil, en yüksek düzeltme eki olan sürüm</span><span class="sxs-lookup"><span data-stu-id="63444-130">*HighestPatch* : the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="63444-131">*HighestMinor* : en düşük ana, en yüksek ikincil, en yüksek düzeltme eki olan sürüm</span><span class="sxs-lookup"><span data-stu-id="63444-131">*HighestMinor* : the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="63444-132">*En yüksek* (parametresiz Update-Package için varsayılan): en yüksek sürüm</span><span class="sxs-lookup"><span data-stu-id="63444-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="63444-133">Varsayılan değeri, [`dependencyVersion`](../nuget-config-file.md#config-section) dosyadaki ayarını kullanarak ayarlayabilirsiniz `Nuget.Config` .</span><span class="sxs-lookup"><span data-stu-id="63444-133">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="63444-134">WhatIf</span><span class="sxs-lookup"><span data-stu-id="63444-134">WhatIf</span></span> | <span data-ttu-id="63444-135">Komutu, eşitlemeyi gerçekten gerçekleştirmeden çalışırken ne olacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="63444-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="63444-136">Bu parametrelerin hiçbiri, işlem hattı girişi veya joker karakterler kabul etmez.</span><span class="sxs-lookup"><span data-stu-id="63444-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="63444-137">Ortak Parametreler</span><span class="sxs-lookup"><span data-stu-id="63444-137">Common Parameters</span></span>

<span data-ttu-id="63444-138">`Sync-Package` Şu [ortak PowerShell parametrelerini](/powershell/module/microsoft.powershell.core/about/about_commonparameters)destekler: Hata Ayıkla, hata eylemi, ErrorVariable, OutBuffer, OutVariable, Pipelinevariable, verbose, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="63444-138">`Sync-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="63444-139">Örnekler</span><span class="sxs-lookup"><span data-stu-id="63444-139">Examples</span></span>

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