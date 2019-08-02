---
title: NuGet Install-Package PowerShell Başvurusu
description: Visual Studio 'daki NuGet Paket Yöneticisi konsolundaki Install-Package PowerShell komutu için başvuru.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 1899662049735189ab4dcb728df5d56afdc5f7c5
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328206"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="e3845-103">Install-Package (Visual Studio'da Paket Yöneticisi Konsolu)</span><span class="sxs-lookup"><span data-stu-id="e3845-103">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="e3845-104">*Bu konuda, Windows üzerinde Visual Studio 'da [Paket Yöneticisi konsolu](../../consume-packages/install-use-packages-powershell.md) içindeki komut açıklanmaktadır. Genel PowerShell Install-Package komutu için bkz. [PowerShell PackageManagement başvurusu](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="e3845-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="e3845-105">Bir paketi ve bağımlılıklarını bir projeye kurar.</span><span class="sxs-lookup"><span data-stu-id="e3845-105">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="e3845-106">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="e3845-106">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="e3845-107">NuGet 2.8 + ' de `Install-Package` , projenizdeki mevcut bir paketin indirgenmesini sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="e3845-107">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="e3845-108">Örneğin, Microsoft. AspNet. MVC 5.1.0-RC1 yüklüyse, aşağıdaki komut bunu 5.0.0 'e indirgeyebilecek:</span><span class="sxs-lookup"><span data-stu-id="e3845-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="e3845-109">Parametreler</span><span class="sxs-lookup"><span data-stu-id="e3845-109">Parameters</span></span>

| <span data-ttu-id="e3845-110">Parametre</span><span class="sxs-lookup"><span data-stu-id="e3845-110">Parameter</span></span> | <span data-ttu-id="e3845-111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e3845-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e3845-112">Id</span><span class="sxs-lookup"><span data-stu-id="e3845-112">Id</span></span> | <span data-ttu-id="e3845-113">Istenir Yüklenecek paketin tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="e3845-113">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="e3845-114">(*3.0 +* ) Tanımlayıcı, bir `packages.config` dosyanın `.nupkg` veya dosyanın bir yolu veya URL 'si olabilir.</span><span class="sxs-lookup"><span data-stu-id="e3845-114">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="e3845-115">-ID anahtarı isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="e3845-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="e3845-116">Ignoredependencies</span><span class="sxs-lookup"><span data-stu-id="e3845-116">IgnoreDependencies</span></span> | <span data-ttu-id="e3845-117">Yalnızca bu paketi yükler ve bağımlılıklarını değil.</span><span class="sxs-lookup"><span data-stu-id="e3845-117">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="e3845-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="e3845-118">ProjectName</span></span> | <span data-ttu-id="e3845-119">Paketin yükleneceği proje, varsayılan projenin varsayılan bir proje olur.</span><span class="sxs-lookup"><span data-stu-id="e3845-119">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="e3845-120">Source</span><span class="sxs-lookup"><span data-stu-id="e3845-120">Source</span></span> | <span data-ttu-id="e3845-121">Aranacak paket kaynağının URL veya klasör yolu.</span><span class="sxs-lookup"><span data-stu-id="e3845-121">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="e3845-122">Yerel klasör yolları mutlak veya geçerli klasöre göreli olabilir.</span><span class="sxs-lookup"><span data-stu-id="e3845-122">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="e3845-123">Atlanırsa, `Install-Package` Şu anda seçili olan paket kaynağını arar.</span><span class="sxs-lookup"><span data-stu-id="e3845-123">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="e3845-124">Sürüm</span><span class="sxs-lookup"><span data-stu-id="e3845-124">Version</span></span> | <span data-ttu-id="e3845-125">Yüklenecek paketin sürümü, en son sürümü varsayılan olarak sağlar.</span><span class="sxs-lookup"><span data-stu-id="e3845-125">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="e3845-126">Includeönsürümü</span><span class="sxs-lookup"><span data-stu-id="e3845-126">IncludePrerelease</span></span> | <span data-ttu-id="e3845-127">Yüklemenin yayın öncesi paketlerini dikkate alır.</span><span class="sxs-lookup"><span data-stu-id="e3845-127">Considers prerelease packages for the install.</span></span> <span data-ttu-id="e3845-128">Atlanırsa, yalnızca kararlı paketler değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="e3845-128">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="e3845-129">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="e3845-129">FileConflictAction</span></span> | <span data-ttu-id="e3845-130">Proje tarafından başvurulan var olan dosyaların üzerine yazılması veya yoksayılması istendiğinde gerçekleştirilecek eylem.</span><span class="sxs-lookup"><span data-stu-id="e3845-130">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="e3845-131">Olası değerler *üzerine yazılır, Yoksay, None, overwriteall*ve *(3,0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="e3845-131">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="e3845-132">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="e3845-132">DependencyVersion</span></span> | <span data-ttu-id="e3845-133">Kullanılacak bağımlılık paketlerinin sürümü, bu, aşağıdakilerden biri olabilir:</span><span class="sxs-lookup"><span data-stu-id="e3845-133">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="e3845-134">*En düşük* (varsayılan): en düşük sürüm</span><span class="sxs-lookup"><span data-stu-id="e3845-134">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="e3845-135">*HighestPatch*: en düşük ana, en düşük ikincil, en yüksek düzeltme eki olan sürüm</span><span class="sxs-lookup"><span data-stu-id="e3845-135">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="e3845-136">*HighestMinor*: en düşük ana, en yüksek ikincil, en yüksek düzeltme eki olan sürüm</span><span class="sxs-lookup"><span data-stu-id="e3845-136">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="e3845-137">*En yüksek* (parametresi olmayan Update-Package için varsayılan): en yüksek sürüm</span><span class="sxs-lookup"><span data-stu-id="e3845-137">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="e3845-138">Varsayılan değeri, [`dependencyVersion`](../nuget-config-file.md#config-section) `Nuget.Config` dosyadaki ayarını kullanarak ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e3845-138">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="e3845-139">WhatIf</span><span class="sxs-lookup"><span data-stu-id="e3845-139">WhatIf</span></span> | <span data-ttu-id="e3845-140">Yüklemeyi yapmadan komutu çalıştırırken ne olacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="e3845-140">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="e3845-141">Bu parametrelerin hiçbiri, işlem hattı girişi veya joker karakterler kabul etmez.</span><span class="sxs-lookup"><span data-stu-id="e3845-141">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="e3845-142">Ortak Parametreler</span><span class="sxs-lookup"><span data-stu-id="e3845-142">Common Parameters</span></span>

<span data-ttu-id="e3845-143">`Install-Package`Aşağıdaki [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216)destekler: Hata Ayıkla, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, verbose, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="e3845-143">`Install-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="e3845-144">Örnekler</span><span class="sxs-lookup"><span data-stu-id="e3845-144">Examples</span></span>

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
# Note: the URL must end with "packages.config"
Install-Package https://raw.githubusercontent.com/linked-data-dotnet/json-ld.net/master/.nuget/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-Package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
# Note: the URL must end with ".nupkg"
Install-Package https://globalcdn.nuget.org/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```