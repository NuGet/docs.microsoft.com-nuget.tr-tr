---
title: NuGet Update-Package PowerShell Başvurusu
description: Visual Studio 'daki NuGet Paket Yöneticisi konsolundaki Update-Package PowerShell komutu için başvuru.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 57e50ed805496b3511bc3b808f89da6f7ad413fc
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328185"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="fe8b4-103">Update-Package (Visual Studio'da Paket Yöneticisi Konsolu)</span><span class="sxs-lookup"><span data-stu-id="fe8b4-103">Update-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="fe8b4-104">*Yalnızca Windows üzerinde Visual Studio 'daki [NuGet Paket Yöneticisi konsolu](../../consume-packages/install-use-packages-powershell.md) içinde kullanılabilir.*</span><span class="sxs-lookup"><span data-stu-id="fe8b4-104">*Available only within the [NuGet Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="fe8b4-105">Bir paketi ve onun bağımlılıklarını veya bir projedeki tüm paketleri daha yeni bir sürüme güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="fe8b4-105">Updates a package and its dependencies, or all packages in a project, to a newer version.</span></span>

## <a name="syntax"></a><span data-ttu-id="fe8b4-106">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="fe8b4-106">Syntax</span></span>

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="fe8b4-107">NuGet 2.8 + ' de `Update-Package` , projenizde var olan bir paketin indirgenmesini sağlamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="fe8b4-107">In NuGet 2.8+, `Update-Package` can be used to downgrade an existing package in your project.</span></span> <span data-ttu-id="fe8b4-108">Örneğin, Microsoft. AspNet. MVC 5.1.0-RC1 yüklüyse, aşağıdaki komut bunu 5.0.0 'e indirgeyebilecek:</span><span class="sxs-lookup"><span data-stu-id="fe8b4-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="fe8b4-109">Parametreler</span><span class="sxs-lookup"><span data-stu-id="fe8b4-109">Parameters</span></span>

|  <span data-ttu-id="fe8b4-110">Parametre</span><span class="sxs-lookup"><span data-stu-id="fe8b4-110">Parameter</span></span> | <span data-ttu-id="fe8b4-111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fe8b4-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fe8b4-112">Id</span><span class="sxs-lookup"><span data-stu-id="fe8b4-112">Id</span></span> | <span data-ttu-id="fe8b4-113">Güncelleştirilecek paketin tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="fe8b4-113">The identifier of the package to update.</span></span> <span data-ttu-id="fe8b4-114">Atlanırsa, tüm paketleri güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="fe8b4-114">If omitted, updates all packages.</span></span> <span data-ttu-id="fe8b4-115">-ID anahtarı isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="fe8b4-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="fe8b4-116">Ignoredependencies</span><span class="sxs-lookup"><span data-stu-id="fe8b4-116">IgnoreDependencies</span></span> | <span data-ttu-id="fe8b4-117">Paketin bağımlılıklarını güncelleştirmeyi atlar.</span><span class="sxs-lookup"><span data-stu-id="fe8b4-117">Skips updating the package's dependencies.</span></span> |
| <span data-ttu-id="fe8b4-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="fe8b4-118">ProjectName</span></span> | <span data-ttu-id="fe8b4-119">Güncelleştirilecek paketleri içeren projenin adı, tüm projeleri varsayılan olarak içerir.</span><span class="sxs-lookup"><span data-stu-id="fe8b4-119">The name of the project containing the packages to update, defaulting to all projects.</span></span> |
| <span data-ttu-id="fe8b4-120">Sürüm</span><span class="sxs-lookup"><span data-stu-id="fe8b4-120">Version</span></span> | <span data-ttu-id="fe8b4-121">Yükseltme için kullanılacak sürüm, en son sürüme varsayılan olarak ayarlanıyor.</span><span class="sxs-lookup"><span data-stu-id="fe8b4-121">The version to use for the upgrade, defaulting to the latest version.</span></span> <span data-ttu-id="fe8b4-122">NuGet 3.0 + sürümünde sürüm değeri *En düşük, en yüksek, HighestMinor*veya *HighestPatch* (-Safe) olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="fe8b4-122">In NuGet 3.0+, the version value must be one of *Lowest, Highest, HighestMinor*, or *HighestPatch* (equivalent to -Safe).</span></span> |
| <span data-ttu-id="fe8b4-123">Güven</span><span class="sxs-lookup"><span data-stu-id="fe8b4-123">Safe</span></span> | <span data-ttu-id="fe8b4-124">Yükseltmeleri, şu anda yüklü olan paket ile aynı ana ve alt sürümü olan sürümlerle kısıtlar.</span><span class="sxs-lookup"><span data-stu-id="fe8b4-124">Constrains upgrades to only versions with the same Major and Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="fe8b4-125">Source</span><span class="sxs-lookup"><span data-stu-id="fe8b4-125">Source</span></span> | <span data-ttu-id="fe8b4-126">Aranacak paket kaynağının URL veya klasör yolu.</span><span class="sxs-lookup"><span data-stu-id="fe8b4-126">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="fe8b4-127">Yerel klasör yolları mutlak veya geçerli klasöre göreli olabilir.</span><span class="sxs-lookup"><span data-stu-id="fe8b4-127">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="fe8b4-128">Atlanırsa, `Update-Package` Şu anda seçili olan paket kaynağını arar.</span><span class="sxs-lookup"><span data-stu-id="fe8b4-128">If omitted, `Update-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="fe8b4-129">Includeönsürümü</span><span class="sxs-lookup"><span data-stu-id="fe8b4-129">IncludePrerelease</span></span> | <span data-ttu-id="fe8b4-130">Güncelleştirmeler için yayın öncesi paketleri içerir.</span><span class="sxs-lookup"><span data-stu-id="fe8b4-130">Includes prerelease packages for updates.</span></span> |
| <span data-ttu-id="fe8b4-131">Yeniden yükleyin</span><span class="sxs-lookup"><span data-stu-id="fe8b4-131">Reinstall</span></span> | <span data-ttu-id="fe8b4-132">Paketleri şu anda yüklü sürümlerini kullanarak resintalls.</span><span class="sxs-lookup"><span data-stu-id="fe8b4-132">Resintalls packages using their currently installed versions.</span></span> <span data-ttu-id="fe8b4-133">Bkz. [paketleri yeniden yükleme ve güncelleştirme](../../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="fe8b4-133">See [Reinstalling and updating packages](../../consume-packages/reinstalling-and-updating-packages.md).</span></span> |
| <span data-ttu-id="fe8b4-134">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="fe8b4-134">FileConflictAction</span></span> | <span data-ttu-id="fe8b4-135">Proje tarafından başvurulan var olan dosyaların üzerine yazılması veya yoksayılması istendiğinde gerçekleştirilecek eylem.</span><span class="sxs-lookup"><span data-stu-id="fe8b4-135">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="fe8b4-136">Olası değerler *üzerine yazılır, Yoksay, None, overwriteall*ve *IgnoreAll* (3.0 +).</span><span class="sxs-lookup"><span data-stu-id="fe8b4-136">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *IgnoreAll* (3.0+).</span></span> |
| <span data-ttu-id="fe8b4-137">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="fe8b4-137">DependencyVersion</span></span> | <span data-ttu-id="fe8b4-138">Kullanılacak bağımlılık paketlerinin sürümü, bu, aşağıdakilerden biri olabilir:</span><span class="sxs-lookup"><span data-stu-id="fe8b4-138">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="fe8b4-139">*En düşük* (varsayılan): en düşük sürüm</span><span class="sxs-lookup"><span data-stu-id="fe8b4-139">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="fe8b4-140">*HighestPatch*: en düşük ana, en düşük ikincil, en yüksek düzeltme eki olan sürüm</span><span class="sxs-lookup"><span data-stu-id="fe8b4-140">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="fe8b4-141">*HighestMinor*: en düşük ana, en yüksek ikincil, en yüksek düzeltme eki olan sürüm</span><span class="sxs-lookup"><span data-stu-id="fe8b4-141">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="fe8b4-142">*En yüksek* (parametresi olmayan Update-Package için varsayılan): en yüksek sürüm</span><span class="sxs-lookup"><span data-stu-id="fe8b4-142">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="fe8b4-143">Varsayılan değeri, [`dependencyVersion`](../nuget-config-file.md#config-section) `Nuget.Config` dosyadaki ayarını kullanarak ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe8b4-143">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="fe8b4-144">ToHighestPatch</span><span class="sxs-lookup"><span data-stu-id="fe8b4-144">ToHighestPatch</span></span> | <span data-ttu-id="fe8b4-145">-Safe ile eşdeğerdir.</span><span class="sxs-lookup"><span data-stu-id="fe8b4-145">equivalent to -Safe.</span></span> |
| <span data-ttu-id="fe8b4-146">ToHighestMinor</span><span class="sxs-lookup"><span data-stu-id="fe8b4-146">ToHighestMinor</span></span> | <span data-ttu-id="fe8b4-147">Yükseltmeleri yalnızca, yüklü olan paketle aynı ana sürüme sahip sürümlere kısıtlar.</span><span class="sxs-lookup"><span data-stu-id="fe8b4-147">Constrains upgrades to only versions with the same Major version as the currently installed package.</span></span> |
| <span data-ttu-id="fe8b4-148">WhatIf</span><span class="sxs-lookup"><span data-stu-id="fe8b4-148">WhatIf</span></span> | <span data-ttu-id="fe8b4-149">Gerçekten güncelleştirmeyi gerçekleştirmeden, komutu çalıştırırken ne olacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="fe8b4-149">Shows what would happen when running the command without actually performing the update.</span></span> |

<span data-ttu-id="fe8b4-150">Bu parametrelerin hiçbiri, işlem hattı girişi veya joker karakterler kabul etmez.</span><span class="sxs-lookup"><span data-stu-id="fe8b4-150">None of these parameters accept pipeline input or wildcard characters.</span></span>

### <a name="common-parameters"></a><span data-ttu-id="fe8b4-151">Ortak Parametreler</span><span class="sxs-lookup"><span data-stu-id="fe8b4-151">Common Parameters</span></span>

<span data-ttu-id="fe8b4-152">`Update-Package`Aşağıdaki [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216)destekler: Hata Ayıkla, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, verbose, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="fe8b4-152">`Update-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

### <a name="examples"></a><span data-ttu-id="fe8b4-153">Örnekler</span><span class="sxs-lookup"><span data-stu-id="fe8b4-153">Examples</span></span>

```ps
# Updates all packages in every project of the solution
Update-Package

# Updates every package in the MvcApplication1 project
Update-Package -ProjectName MvcApplication1

# Updates the Elmah package in every project to the latest version
Update-Package Elmah

# Updates the Elmah package to version 1.1.0 in every project showing optional -Id usage
Update-Package -Id Elmah -Version 1.1.0

# Updates the Elmah package within the MvcApplication1 project to the highest "safe" version.
# For example, if Elmah version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2,
# and 1.1 are available in the feed, the -Safe parameter updates the package to 1.0.2 instead
# of 1.1 as it would otherwise.
Update-Package Elmah -ProjectName MvcApplication1 -Safe

# Reinstall the same version of the original package, but with the latest version of dependencies
# (subject to version constraints). If this command rolls a dependency back to an earlier version,
# use Update-Package <dependency_name> to reinstall that one dependency without affecting the
# dependent package.
Update-Package ELmah –reinstall 

# Reinstall the Elmah package in just MyProject
Update-Package Elmah -ProjectName MyProject -reinstall

# Reinstall the same version of the original package without touching dependencies.
Update-Package ELmah –reinstall -ignoreDependencies
```
