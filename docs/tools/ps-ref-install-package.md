---
title: NuGet Install-Package PowerShell başvurusu
description: Visual Studio'da NuGet Paket Yöneticisi konsolu Install-Package PowerShell komutunda referansı.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 755c87bbc68d3b688c81e16edbc1faabdc9e0520
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842493"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="9e94c-103">Install-Package (Visual Studio'da Paket Yöneticisi Konsolu)</span><span class="sxs-lookup"><span data-stu-id="9e94c-103">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="9e94c-104">*Bu konu içindeki komut açıklar [Paket Yöneticisi Konsolu](package-manager-console.md) Windows üzerinde Visual Studio'da. Genel PowerShell Install-Package komutu için bkz: [PowerShell PackageManagement başvuru](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="9e94c-104">*This topic describes the command within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="9e94c-105">Bir projeye bir paketi ve bağımlılıkları yükler.</span><span class="sxs-lookup"><span data-stu-id="9e94c-105">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="9e94c-106">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="9e94c-106">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="9e94c-107">Nuget'te 2.8 + `Install-Package` projenizdeki varolan paketi düşürebilir.</span><span class="sxs-lookup"><span data-stu-id="9e94c-107">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="9e94c-108">Yüklü Microsoft.AspNet.MVC 5.1.0-rc1 varsa, örneğin, aşağıdaki komut, 5.0.0 için düşürme:</span><span class="sxs-lookup"><span data-stu-id="9e94c-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="9e94c-109">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9e94c-109">Parameters</span></span>

| <span data-ttu-id="9e94c-110">Parametre</span><span class="sxs-lookup"><span data-stu-id="9e94c-110">Parameter</span></span> | <span data-ttu-id="9e94c-111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9e94c-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9e94c-112">Id</span><span class="sxs-lookup"><span data-stu-id="9e94c-112">Id</span></span> | <span data-ttu-id="9e94c-113">(Gerekli) Yüklenecek paket tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="9e94c-113">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="9e94c-114">(*3.0 +* ) tanımlayıcı bir yol veya URL'sini olabilir bir `packages.config` dosya veya `.nupkg` dosya.</span><span class="sxs-lookup"><span data-stu-id="9e94c-114">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="9e94c-115">Kimliği anahtarın kendisinde, isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="9e94c-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="9e94c-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="9e94c-116">IgnoreDependencies</span></span> | <span data-ttu-id="9e94c-117">Yalnızca bu paket ve onun bağımlılıklarını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="9e94c-117">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="9e94c-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="9e94c-118">ProjectName</span></span> | <span data-ttu-id="9e94c-119">Projeye varsayılan proje için varsayılan olarak ayarlanıyor, paketi yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="9e94c-119">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="9e94c-120">Source</span><span class="sxs-lookup"><span data-stu-id="9e94c-120">Source</span></span> | <span data-ttu-id="9e94c-121">Aranacak paket kaynağı için URL veya klasör yolu.</span><span class="sxs-lookup"><span data-stu-id="9e94c-121">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="9e94c-122">Yerel klasör yol mutlak veya göreli geçerli klasörde olabilir.</span><span class="sxs-lookup"><span data-stu-id="9e94c-122">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="9e94c-123">Atlanırsa, `Install-Package` seçili paket kaynağı arar.</span><span class="sxs-lookup"><span data-stu-id="9e94c-123">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="9e94c-124">Sürüm</span><span class="sxs-lookup"><span data-stu-id="9e94c-124">Version</span></span> | <span data-ttu-id="9e94c-125">Yüklemek için paketin sürümü en son sürüme varsayılan olarak ayarlanıyor.</span><span class="sxs-lookup"><span data-stu-id="9e94c-125">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="9e94c-126">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="9e94c-126">IncludePrerelease</span></span> | <span data-ttu-id="9e94c-127">Yayın öncesi paketleri yükleme için göz önünde bulundurur.</span><span class="sxs-lookup"><span data-stu-id="9e94c-127">Considers prerelease packages for the install.</span></span> <span data-ttu-id="9e94c-128">Atlanırsa, yalnızca kararlı paket olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="9e94c-128">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="9e94c-129">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="9e94c-129">FileConflictAction</span></span> | <span data-ttu-id="9e94c-130">Üzerine ya da proje tarafından başvurulan mevcut dosyaları yoksaymak için sorulan olduğunda gerçekleştirilecek eylem.</span><span class="sxs-lookup"><span data-stu-id="9e94c-130">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="9e94c-131">Olası değerler *üzerine yaz, yoksay, None, OverwriteAll*, ve *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="9e94c-131">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="9e94c-132">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="9e94c-132">DependencyVersion</span></span> | <span data-ttu-id="9e94c-133">Aşağıdakilerden biri olabilen kullanmak için bağımlılık paketlerini sürümü:</span><span class="sxs-lookup"><span data-stu-id="9e94c-133">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="9e94c-134">*En düşük* (varsayılan): en düşük sürüm</span><span class="sxs-lookup"><span data-stu-id="9e94c-134">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="9e94c-135">*HighestPatch*: en düşük büyük, en düşük küçük, yüksek düzeltme sürümü</span><span class="sxs-lookup"><span data-stu-id="9e94c-135">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="9e94c-136">*HighestMinor*: en düşük ana sürümle, en yüksek ikincil, yüksek düzeltme eki</span><span class="sxs-lookup"><span data-stu-id="9e94c-136">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="9e94c-137">*En yüksek* (parametre olmadan Update-Package için varsayılan): en yüksek sürüm</span><span class="sxs-lookup"><span data-stu-id="9e94c-137">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="9e94c-138">Varsayılan değer kullanarak ayarlayabilirsiniz [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) ayarı `Nuget.Config` dosya.</span><span class="sxs-lookup"><span data-stu-id="9e94c-138">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="9e94c-139">WhatIf</span><span class="sxs-lookup"><span data-stu-id="9e94c-139">WhatIf</span></span> | <span data-ttu-id="9e94c-140">Komut yükleme işlemi yapmadan çalıştırılırken ne olacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="9e94c-140">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="9e94c-141">Hiçbiri bu parametre ardışık düzen giriş veya joker karakterler kabul edin.</span><span class="sxs-lookup"><span data-stu-id="9e94c-141">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="9e94c-142">Ortak parametreleri</span><span class="sxs-lookup"><span data-stu-id="9e94c-142">Common Parameters</span></span>

<span data-ttu-id="9e94c-143">`Install-Package` şunları desteklemektedir [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): Hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, ayrıntılı PipelineVariable, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="9e94c-143">`Install-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="9e94c-144">Örnekler</span><span class="sxs-lookup"><span data-stu-id="9e94c-144">Examples</span></span>

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
Install-package https://raw.githubusercontent.com/json-ld.net/master/src/JsonLD/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
Install-package https://az320820.vo.msecnd.net/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
