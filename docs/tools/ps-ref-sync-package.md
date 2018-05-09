---
title: NuGet eşitleme-Package PowerShell başvurusu
description: Visual Studio'da NuGet Paket Yöneticisi konsolunda eşitleme paket PowerShell komut başvurusu.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 424c4fbe3ff4b61c665bf7353976d4fb09268185
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="7035d-103">Eşitleme-Package (Visual Studio'da Paket Yöneticisi Konsolu)</span><span class="sxs-lookup"><span data-stu-id="7035d-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="7035d-104">*Sürüm 3.0 +; yalnızca içinde kullanılabilir [NuGet Paket Yöneticisi Konsolu](package-manager-console.md) Windows Visual Studio'da.*</span><span class="sxs-lookup"><span data-stu-id="7035d-104">*Version 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="7035d-105">Yüklü paketin sürümünü belirtilen (veya varsayılan) alır, proje ve sürümü çözümdeki projelerin geri kalanına eşitler.</span><span class="sxs-lookup"><span data-stu-id="7035d-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="7035d-106">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="7035d-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="7035d-107">Parametreler</span><span class="sxs-lookup"><span data-stu-id="7035d-107">Parameters</span></span>

| <span data-ttu-id="7035d-108">Parametre</span><span class="sxs-lookup"><span data-stu-id="7035d-108">Parameter</span></span> | <span data-ttu-id="7035d-109">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7035d-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7035d-110">Kimliği</span><span class="sxs-lookup"><span data-stu-id="7035d-110">Id</span></span> | <span data-ttu-id="7035d-111">(Gerekli) Eşitlemek için paket tanımlayıcısı. Kimliği anahtarı kendisini isteğe bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="7035d-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="7035d-112">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="7035d-112">IgnoreDependencies</span></span> | <span data-ttu-id="7035d-113">Yalnızca bu paketi ve bağımlılıklarını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="7035d-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="7035d-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="7035d-114">ProjectName</span></span> | <span data-ttu-id="7035d-115">Varsayılan proje için varsayılan değer olarak paketinden, eşitleme projesi.</span><span class="sxs-lookup"><span data-stu-id="7035d-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="7035d-116">Sürüm</span><span class="sxs-lookup"><span data-stu-id="7035d-116">Version</span></span> | <span data-ttu-id="7035d-117">Eşitlemek için paketin sürümü şu anda yüklü olan sürümle varsayılan olarak ayarlanıyor.</span><span class="sxs-lookup"><span data-stu-id="7035d-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="7035d-118">Kaynak</span><span class="sxs-lookup"><span data-stu-id="7035d-118">Source</span></span> | <span data-ttu-id="7035d-119">Aranacak paket kaynağının URL'sini veya klasör yolu.</span><span class="sxs-lookup"><span data-stu-id="7035d-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="7035d-120">Yerel klasör yolları mutlak veya göreli geçerli klasörde olabilir.</span><span class="sxs-lookup"><span data-stu-id="7035d-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="7035d-121">Atlanırsa, `Sync-Package` şu anda seçili paket kaynağını arar.</span><span class="sxs-lookup"><span data-stu-id="7035d-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="7035d-122">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="7035d-122">IncludePrerelease</span></span> | <span data-ttu-id="7035d-123">Ön sürüm paketlerini eşitleme içerir.</span><span class="sxs-lookup"><span data-stu-id="7035d-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="7035d-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="7035d-124">FileConflictAction</span></span> | <span data-ttu-id="7035d-125">Üzerine veya varolan dosyaları proje tarafından başvurulan yoksayar istenir olduğunda gerçekleştirilecek eylem.</span><span class="sxs-lookup"><span data-stu-id="7035d-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="7035d-126">Olası değerler şunlardır: *üzerine yazma, yoksay, None, OverwriteAll*, ve *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="7035d-126">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="7035d-127">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="7035d-127">DependencyVersion</span></span> | <span data-ttu-id="7035d-128">Şunlardan biri olabilen kullanmak için bağımlılık Paket sürümü:</span><span class="sxs-lookup"><span data-stu-id="7035d-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="7035d-129">*En düşük* (varsayılan): en düşük sürüm</span><span class="sxs-lookup"><span data-stu-id="7035d-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="7035d-130">*HighestPatch*: en düşük ana, en düşük küçük, en yüksek düzeltme eki sürümüyle</span><span class="sxs-lookup"><span data-stu-id="7035d-130">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="7035d-131">*HighestMinor*: en düşük ana sürümle, en yüksek ikincil, en yüksek düzeltme eki</span><span class="sxs-lookup"><span data-stu-id="7035d-131">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="7035d-132">*En yüksek* (hiçbir parametre güncelleştirme paketi için varsayılan): en yüksek sürüm</span><span class="sxs-lookup"><span data-stu-id="7035d-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="7035d-133">Varsayılan değer kullanılarak ayarlayabilirsiniz [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) ayarı `Nuget.Config` dosya.</span><span class="sxs-lookup"><span data-stu-id="7035d-133">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="7035d-134">WhatIf</span><span class="sxs-lookup"><span data-stu-id="7035d-134">WhatIf</span></span> | <span data-ttu-id="7035d-135">Komut gerçekte eşitleme yapmadan çalıştırırken ne olacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="7035d-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="7035d-136">Hiçbiri bu parametre ardışık düzen giriş veya joker karakter kabul edin.</span><span class="sxs-lookup"><span data-stu-id="7035d-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="7035d-137">Ortak parametreleri</span><span class="sxs-lookup"><span data-stu-id="7035d-137">Common Parameters</span></span>

<span data-ttu-id="7035d-138">`Sync-Package` Aşağıdaki destekleyen [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, ayrıntı, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="7035d-138">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="7035d-139">Örnekler</span><span class="sxs-lookup"><span data-stu-id="7035d-139">Examples</span></span>

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
