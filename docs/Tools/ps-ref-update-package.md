---
title: "NuGet paket PowerShell başvurusu | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Visual Studio'da NuGet Paket Yöneticisi konsolunda güncelleştirme paketini PowerShell komut başvurusu."
keywords: "NuGet Paket Yöneticisi konsolu, NuGet Powershell komutlarını NuGet Powershell başvurusu, güncelleştirme paketi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7ebb5a420e469c70a9dd790231a92fedbc4713b6
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/14/2018
---
# <a name="update-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="dbdb1-104">Güncelleştirme Paketi (Visual Studio'da Paket Yöneticisi Konsolu)</span><span class="sxs-lookup"><span data-stu-id="dbdb1-104">Update-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="dbdb1-105">*Yalnızca içinde kullanılabilir [NuGet Paket Yöneticisi Konsolu](package-manager-console.md) Windows Visual Studio'da.*</span><span class="sxs-lookup"><span data-stu-id="dbdb1-105">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="dbdb1-106">Bir paketi ve bağımlılıklarını ya da bir projesindeki tüm paketleri daha yeni bir sürüme güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="dbdb1-106">Updates a package and its dependencies, or all packages in a project, to a newer version.</span></span>

## <a name="syntax"></a><span data-ttu-id="dbdb1-107">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="dbdb1-107">Syntax</span></span>

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="dbdb1-108">NuGet 2.8 + içinde `Update-Package` var olan bir paketini projenize düşürmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="dbdb1-108">In NuGet 2.8+, `Update-Package` can be used to downgrade an existing package in your project.</span></span> <span data-ttu-id="dbdb1-109">Microsoft.AspNet.MVC 5.1.0-rc1 yüklü varsa, örneğin, aşağıdaki komut, 5.0.0 için düşürmek:</span><span class="sxs-lookup"><span data-stu-id="dbdb1-109">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

<span data-ttu-id="dbdb1-110">NuGet 2.7 ve daha önceki bir sürümü zaten yüklü olduğunu bildiren bir hata verir.</span><span class="sxs-lookup"><span data-stu-id="dbdb1-110">NuGet 2.7 and earlier gives an error saying that a newer version is already installed.</span></span>

## <a name="parameters"></a><span data-ttu-id="dbdb1-111">Parametreler</span><span class="sxs-lookup"><span data-stu-id="dbdb1-111">Parameters</span></span>

|  <span data-ttu-id="dbdb1-112">Parametre</span><span class="sxs-lookup"><span data-stu-id="dbdb1-112">Parameter</span></span> | <span data-ttu-id="dbdb1-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="dbdb1-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="dbdb1-114">Kimliği</span><span class="sxs-lookup"><span data-stu-id="dbdb1-114">Id</span></span> | <span data-ttu-id="dbdb1-115">Güncelleştirilecek paket tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="dbdb1-115">The identifier of the package to update.</span></span> <span data-ttu-id="dbdb1-116">Atlanırsa, tüm paketleri güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="dbdb1-116">If omitted, updates all packages.</span></span> <span data-ttu-id="dbdb1-117">Kimliği anahtarı kendisini isteğe bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="dbdb1-117">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="dbdb1-118">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="dbdb1-118">IgnoreDependencies</span></span> | <span data-ttu-id="dbdb1-119">Paketin bağımlılıklarını güncelleştirme atlar.</span><span class="sxs-lookup"><span data-stu-id="dbdb1-119">Skips updating the package's dependencies.</span></span> |
| <span data-ttu-id="dbdb1-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="dbdb1-120">ProjectName</span></span> | <span data-ttu-id="dbdb1-121">Güncelleştirilecek paketi içeren, tüm projeler için varsayılan değer olarak projesinin adı.</span><span class="sxs-lookup"><span data-stu-id="dbdb1-121">The name of the project containing the packages to update, defaulting to all projects.</span></span> |
| <span data-ttu-id="dbdb1-122">Sürüm</span><span class="sxs-lookup"><span data-stu-id="dbdb1-122">Version</span></span> | <span data-ttu-id="dbdb1-123">En son sürüm varsayılan değer olarak, yükseltme için kullanılacak sürümü.</span><span class="sxs-lookup"><span data-stu-id="dbdb1-123">The version to use for the upgrade, defaulting to the latest version.</span></span> <span data-ttu-id="dbdb1-124">NuGet içinde 3.0 +, sürüm değeri şunlardan biri olmalıdır *en düşük, en yüksek, HighestMinor*, veya *HighestPatch* (eşdeğer - güvenli).</span><span class="sxs-lookup"><span data-stu-id="dbdb1-124">In NuGet 3.0+, the version value must be one of *Lowest, Highest, HighestMinor*, or *HighestPatch* (equivalent to -Safe).</span></span> |
| <span data-ttu-id="dbdb1-125">Güvenli</span><span class="sxs-lookup"><span data-stu-id="dbdb1-125">Safe</span></span> | <span data-ttu-id="dbdb1-126">Yükseltmeleri aynı birincil ve ikincil sürüme yüklü paketi içeren yalnızca sürümlerle kısıtlar.</span><span class="sxs-lookup"><span data-stu-id="dbdb1-126">Constrains upgrades to only versions with the same Major and Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="dbdb1-127">Kaynak</span><span class="sxs-lookup"><span data-stu-id="dbdb1-127">Source</span></span> | <span data-ttu-id="dbdb1-128">Aranacak paket kaynağının URL'sini veya klasör yolu.</span><span class="sxs-lookup"><span data-stu-id="dbdb1-128">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="dbdb1-129">Yerel klasör yolları mutlak veya göreli geçerli klasörde olabilir.</span><span class="sxs-lookup"><span data-stu-id="dbdb1-129">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="dbdb1-130">Atlanırsa, `Uninstall-Package` şu anda seçili paket kaynağını arar.</span><span class="sxs-lookup"><span data-stu-id="dbdb1-130">If omitted, `Uninstall-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="dbdb1-131">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="dbdb1-131">IncludePrerelease</span></span> | <span data-ttu-id="dbdb1-132">Yayın öncesi paketleri için güncelleştirmeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="dbdb1-132">Includes prerelease packages for updates.</span></span> |
| <span data-ttu-id="dbdb1-133">Yeniden yükleme</span><span class="sxs-lookup"><span data-stu-id="dbdb1-133">Reinstall</span></span> | <span data-ttu-id="dbdb1-134">Şu anda yüklü sürümlerine kullanarak Resintalls paketler.</span><span class="sxs-lookup"><span data-stu-id="dbdb1-134">Resintalls packages using their currently installed versions.</span></span> <span data-ttu-id="dbdb1-135">Bkz: [Reinstalling ve paketleri güncelleştiriliyor](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="dbdb1-135">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span> |
| <span data-ttu-id="dbdb1-136">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="dbdb1-136">FileConflictAction</span></span> | <span data-ttu-id="dbdb1-137">Üzerine veya varolan dosyaları proje tarafından başvurulan yoksayar istenir olduğunda gerçekleştirilecek eylem.</span><span class="sxs-lookup"><span data-stu-id="dbdb1-137">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="dbdb1-138">Olası değerler şunlardır: *üzerine yazma, yoksay, None, OverwriteAll*, ve *IgnoreAll* (3.0 +).</span><span class="sxs-lookup"><span data-stu-id="dbdb1-138">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *IgnoreAll* (3.0+).</span></span> |
| <span data-ttu-id="dbdb1-139">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="dbdb1-139">DependencyVersion</span></span> | <span data-ttu-id="dbdb1-140">Şunlardan biri olabilen kullanmak için bağımlılık Paket sürümü:</span><span class="sxs-lookup"><span data-stu-id="dbdb1-140">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="dbdb1-141">*En düşük* (varsayılan): en düşük sürüm</span><span class="sxs-lookup"><span data-stu-id="dbdb1-141">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="dbdb1-142">*HighestPatch*: en düşük ana, en düşük küçük, en yüksek düzeltme eki sürümüyle</span><span class="sxs-lookup"><span data-stu-id="dbdb1-142">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="dbdb1-143">*HighestMinor*: en düşük ana sürümle, en yüksek ikincil, en yüksek düzeltme eki</span><span class="sxs-lookup"><span data-stu-id="dbdb1-143">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="dbdb1-144">*En yüksek* (hiçbir parametre güncelleştirme paketi için varsayılan): en yüksek sürüm</span><span class="sxs-lookup"><span data-stu-id="dbdb1-144">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="dbdb1-145">Varsayılan değer kullanılarak ayarlayabilirsiniz [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) ayarı `Nuget.Config` dosya.</span><span class="sxs-lookup"><span data-stu-id="dbdb1-145">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="dbdb1-146">ToHighestPatch</span><span class="sxs-lookup"><span data-stu-id="dbdb1-146">ToHighestPatch</span></span> | <span data-ttu-id="dbdb1-147">Yalnızca şu anda yüklenmiş paket ile aynı ikincil sürümle sürümlerine yükseltme kısıtlar.</span><span class="sxs-lookup"><span data-stu-id="dbdb1-147">Constrains upgrades to only versions with the same Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="dbdb1-148">ToHighestMinor</span><span class="sxs-lookup"><span data-stu-id="dbdb1-148">ToHighestMinor</span></span> | <span data-ttu-id="dbdb1-149">Yalnızca şu anda yüklü paketi olarak aynı ana sürümüne sürümleriyle yükseltmeleri kısıtlar.</span><span class="sxs-lookup"><span data-stu-id="dbdb1-149">Constrains upgrades to only versions with the same Major version as the currently installed package.</span></span> |
| <span data-ttu-id="dbdb1-150">WhatIf</span><span class="sxs-lookup"><span data-stu-id="dbdb1-150">WhatIf</span></span> | <span data-ttu-id="dbdb1-151">Komut gerçekte güncelleştirme yapmadan çalıştırırken ne olacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="dbdb1-151">Shows what would happen when running the command without actually performing the update.</span></span> |

<span data-ttu-id="dbdb1-152">Hiçbiri bu parametre ardışık düzen giriş veya joker karakter kabul edin.</span><span class="sxs-lookup"><span data-stu-id="dbdb1-152">None of these parameters accept pipeline input or wildcard characters.</span></span>

### <a name="common-parameters"></a><span data-ttu-id="dbdb1-153">Ortak parametreleri</span><span class="sxs-lookup"><span data-stu-id="dbdb1-153">Common Parameters</span></span>

<span data-ttu-id="dbdb1-154">`Update-Package` Aşağıdaki destekleyen [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, ayrıntı, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="dbdb1-154">`Update-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

### <a name="examples"></a><span data-ttu-id="dbdb1-155">Örnekler</span><span class="sxs-lookup"><span data-stu-id="dbdb1-155">Examples</span></span>

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