---
title: "NuGet eşitleme-Package PowerShell başvurusu | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 1b980b93-fa58-430c-b663-78ce069b1603
description: "Visual Studio'da NuGet Paket Yöneticisi konsolunda eşitleme paket PowerShell komut başvurusu."
keywords: "NuGet Paket Yöneticisi konsolu, NuGet Powershell komutlarını NuGet Powershell başvurusu, eşitleme paket"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4dc542714f14f0e6d3e827292f8fce06561fe270
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="10976-104">Eşitleme-Package (Visual Studio'da Paket Yöneticisi Konsolu)</span><span class="sxs-lookup"><span data-stu-id="10976-104">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="10976-105">*Sürüm 3.0 +; yalnızca içinde kullanılabilir [NuGet Paket Yöneticisi Konsolu](Package-Manager-Console.md) Windows Visual Studio'da.*</span><span class="sxs-lookup"><span data-stu-id="10976-105">*Version 3.0+; available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="10976-106">Yüklü paketin sürümünü belirtilen (veya varsayılan) alır, proje ve sürümü çözümdeki projelerin geri kalanına eşitler.</span><span class="sxs-lookup"><span data-stu-id="10976-106">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="10976-107">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="10976-107">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="10976-108">Parametreler</span><span class="sxs-lookup"><span data-stu-id="10976-108">Parameters</span></span>

| <span data-ttu-id="10976-109">Parametre</span><span class="sxs-lookup"><span data-stu-id="10976-109">Parameter</span></span> | <span data-ttu-id="10976-110">Açıklama</span><span class="sxs-lookup"><span data-stu-id="10976-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="10976-111">Kimliği</span><span class="sxs-lookup"><span data-stu-id="10976-111">Id</span></span> | <span data-ttu-id="10976-112">(Gerekli) Eşitlemek için paket tanımlayıcısı. Kimliği anahtarı kendisini isteğe bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="10976-112">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="10976-113">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="10976-113">IgnoreDependencies</span></span> | <span data-ttu-id="10976-114">Yalnızca bu paketi ve bağımlılıklarını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="10976-114">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="10976-115">ProjectName</span><span class="sxs-lookup"><span data-stu-id="10976-115">ProjectName</span></span> | <span data-ttu-id="10976-116">Varsayılan proje için varsayılan değer olarak paketinden, eşitleme projesi.</span><span class="sxs-lookup"><span data-stu-id="10976-116">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="10976-117">Sürüm</span><span class="sxs-lookup"><span data-stu-id="10976-117">Version</span></span> | <span data-ttu-id="10976-118">Eşitlemek için paketin sürümü şu anda yüklü olan sürümle varsayılan olarak ayarlanıyor.</span><span class="sxs-lookup"><span data-stu-id="10976-118">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="10976-119">Kaynak</span><span class="sxs-lookup"><span data-stu-id="10976-119">Source</span></span> | <span data-ttu-id="10976-120">Aranacak paket kaynağının URL'sini veya klasör yolu.</span><span class="sxs-lookup"><span data-stu-id="10976-120">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="10976-121">Yerel klasör yolları mutlak veya göreli geçerli klasörde olabilir.</span><span class="sxs-lookup"><span data-stu-id="10976-121">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="10976-122">Atlanırsa, `Sync-Package` şu anda seçili paket kaynağını arar.</span><span class="sxs-lookup"><span data-stu-id="10976-122">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="10976-123">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="10976-123">IncludePrerelease</span></span> | <span data-ttu-id="10976-124">Ön sürüm paketlerini eşitleme içerir.</span><span class="sxs-lookup"><span data-stu-id="10976-124">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="10976-125">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="10976-125">FileConflictAction</span></span> | <span data-ttu-id="10976-126">Üzerine veya varolan dosyaları proje tarafından başvurulan yoksayar istenir olduğunda gerçekleştirilecek eylem.</span><span class="sxs-lookup"><span data-stu-id="10976-126">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="10976-127">Olası değerler şunlardır: *üzerine yazma, yoksay, None, OverwriteAll*, ve *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="10976-127">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="10976-128">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="10976-128">DependencyVersion</span></span> | <span data-ttu-id="10976-129">Şunlardan biri olabilen kullanmak için bağımlılık Paket sürümü:</span><span class="sxs-lookup"><span data-stu-id="10976-129">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="10976-130">*En düşük* (varsayılan): en düşük sürüm</span><span class="sxs-lookup"><span data-stu-id="10976-130">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="10976-131">*HighestPatch*: en düşük ana, en düşük küçük, en yüksek düzeltme eki sürümüyle</span><span class="sxs-lookup"><span data-stu-id="10976-131">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="10976-132">*HighestMinor*: en düşük ana sürümle, en yüksek ikincil, en yüksek düzeltme eki</span><span class="sxs-lookup"><span data-stu-id="10976-132">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="10976-133">*En yüksek* (hiçbir parametre güncelleştirme paketi için varsayılan): en yüksek sürüm</span><span class="sxs-lookup"><span data-stu-id="10976-133">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="10976-134">Varsayılan değer kullanılarak ayarlayabilirsiniz [ `dependencyVersion` ](../Schema/nuget-config-file.md#config-section) ayarı `Nuget.Config` dosya.</span><span class="sxs-lookup"><span data-stu-id="10976-134">You can set the default value using the [`dependencyVersion`](../Schema/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="10976-135">WhatIf</span><span class="sxs-lookup"><span data-stu-id="10976-135">WhatIf</span></span> | <span data-ttu-id="10976-136">Komut gerçekte eşitleme yapmadan çalıştırırken ne olacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="10976-136">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="10976-137">Hiçbiri bu parametre ardışık düzen giriş veya joker karakter kabul edin.</span><span class="sxs-lookup"><span data-stu-id="10976-137">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="10976-138">Ortak parametreleri</span><span class="sxs-lookup"><span data-stu-id="10976-138">Common Parameters</span></span>

<span data-ttu-id="10976-139">`Sync-Package`Aşağıdaki destekleyen [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, ayrıntı, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="10976-139">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="10976-140">Örnekler</span><span class="sxs-lookup"><span data-stu-id="10976-140">Examples</span></span>

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
