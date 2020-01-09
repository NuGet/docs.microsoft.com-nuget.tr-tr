---
title: NuGet Install-Package PowerShell Başvurusu
description: Visual Studio 'daki NuGet Paket Yöneticisi konsolundaki Install-Package PowerShell komutu için başvuru.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: a65ba63ed070f40e82c43d12e5fad12d86f28112
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384447"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="9468e-103">Install-Package (Visual Studio'da Paket Yöneticisi Konsolu)</span><span class="sxs-lookup"><span data-stu-id="9468e-103">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="9468e-104">*Bu konuda, Windows üzerinde Visual Studio 'da [Paket Yöneticisi konsolu](../../consume-packages/install-use-packages-powershell.md) içindeki komut açıklanmaktadır. Genel PowerShell Install-Package komutu için bkz. [PowerShell PackageManagement başvurusu](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="9468e-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="9468e-105">Bir paketi ve bağımlılıklarını bir projeye kurar.</span><span class="sxs-lookup"><span data-stu-id="9468e-105">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="9468e-106">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="9468e-106">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="9468e-107">NuGet 2.8 + ' de `Install-Package`, projenizdeki mevcut bir paketin indirgenmesini sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="9468e-107">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="9468e-108">Örneğin, Microsoft. AspNet. MVC 5.1.0-RC1 yüklüyse, aşağıdaki komut bunu 5.0.0 'e indirgeyebilecek:</span><span class="sxs-lookup"><span data-stu-id="9468e-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="9468e-109">Parametreler</span><span class="sxs-lookup"><span data-stu-id="9468e-109">Parameters</span></span>

| <span data-ttu-id="9468e-110">Parametre</span><span class="sxs-lookup"><span data-stu-id="9468e-110">Parameter</span></span> | <span data-ttu-id="9468e-111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9468e-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9468e-112">Id</span><span class="sxs-lookup"><span data-stu-id="9468e-112">Id</span></span> | <span data-ttu-id="9468e-113">Istenir Yüklenecek paketin tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="9468e-113">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="9468e-114">(*3.0 +* ) Tanımlayıcı, bir `packages.config` dosyasının veya bir `.nupkg` dosyasının bir yolu veya URL 'SI olabilir.</span><span class="sxs-lookup"><span data-stu-id="9468e-114">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="9468e-115">-ID anahtarı isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="9468e-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="9468e-116">Ignoredependencies</span><span class="sxs-lookup"><span data-stu-id="9468e-116">IgnoreDependencies</span></span> | <span data-ttu-id="9468e-117">Yalnızca bu paketi yükler ve bağımlılıklarını değil.</span><span class="sxs-lookup"><span data-stu-id="9468e-117">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="9468e-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="9468e-118">ProjectName</span></span> | <span data-ttu-id="9468e-119">Paketin yükleneceği proje, varsayılan projenin varsayılan bir proje olur.</span><span class="sxs-lookup"><span data-stu-id="9468e-119">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="9468e-120">Kaynak</span><span class="sxs-lookup"><span data-stu-id="9468e-120">Source</span></span> | <span data-ttu-id="9468e-121">Aranacak paket kaynağının URL veya klasör yolu.</span><span class="sxs-lookup"><span data-stu-id="9468e-121">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="9468e-122">Yerel klasör yolları mutlak veya geçerli klasöre göreli olabilir.</span><span class="sxs-lookup"><span data-stu-id="9468e-122">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="9468e-123">Atlanırsa, `Install-Package` Şu anda seçili olan paket kaynağını arar.</span><span class="sxs-lookup"><span data-stu-id="9468e-123">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="9468e-124">Sürüm</span><span class="sxs-lookup"><span data-stu-id="9468e-124">Version</span></span> | <span data-ttu-id="9468e-125">Yüklenecek paketin sürümü, en son sürümü varsayılan olarak sağlar.</span><span class="sxs-lookup"><span data-stu-id="9468e-125">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="9468e-126">Includeönsürümü</span><span class="sxs-lookup"><span data-stu-id="9468e-126">IncludePrerelease</span></span> | <span data-ttu-id="9468e-127">Yüklemenin yayın öncesi paketlerini dikkate alır.</span><span class="sxs-lookup"><span data-stu-id="9468e-127">Considers prerelease packages for the install.</span></span> <span data-ttu-id="9468e-128">Atlanırsa, yalnızca kararlı paketler değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="9468e-128">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="9468e-129">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="9468e-129">FileConflictAction</span></span> | <span data-ttu-id="9468e-130">Proje tarafından başvurulan var olan dosyaların üzerine yazılması veya yoksayılması istendiğinde gerçekleştirilecek eylem.</span><span class="sxs-lookup"><span data-stu-id="9468e-130">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="9468e-131">Olası değerler *üzerine yazılır, Yoksay, None, overwriteall*ve *(3,0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="9468e-131">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="9468e-132">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="9468e-132">DependencyVersion</span></span> | <span data-ttu-id="9468e-133">Kullanılacak bağımlılık paketlerinin sürümü, bu, aşağıdakilerden biri olabilir:</span><span class="sxs-lookup"><span data-stu-id="9468e-133">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="9468e-134">*En düşük* (varsayılan): en düşük sürüm</span><span class="sxs-lookup"><span data-stu-id="9468e-134">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="9468e-135">*HighestPatch*: en düşük ana, en düşük ikincil, en yüksek düzeltme eki olan sürüm</span><span class="sxs-lookup"><span data-stu-id="9468e-135">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="9468e-136">*HighestMinor*: en düşük ana, en yüksek ikincil, en yüksek düzeltme eki olan sürüm</span><span class="sxs-lookup"><span data-stu-id="9468e-136">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="9468e-137">*En yüksek* (parametresi olmayan Update-Package için varsayılan): en yüksek sürüm</span><span class="sxs-lookup"><span data-stu-id="9468e-137">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="9468e-138">`Nuget.Config` dosyasındaki [`dependencyVersion`](../nuget-config-file.md#config-section) ayarını kullanarak varsayılan değeri ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9468e-138">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="9468e-139">WhatIf</span><span class="sxs-lookup"><span data-stu-id="9468e-139">WhatIf</span></span> | <span data-ttu-id="9468e-140">Yüklemeyi yapmadan komutu çalıştırırken ne olacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="9468e-140">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="9468e-141">Bu parametrelerin hiçbiri, işlem hattı girişi veya joker karakterler kabul etmez.</span><span class="sxs-lookup"><span data-stu-id="9468e-141">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="9468e-142">Ortak Parametreler</span><span class="sxs-lookup"><span data-stu-id="9468e-142">Common Parameters</span></span>

<span data-ttu-id="9468e-143">`Install-Package`, şu [ortak PowerShell parametrelerini](https://go.microsoft.com/fwlink/?LinkID=113216)destekler: Hata Ayıkla, hata eylemi, ErrorVariable, OutBuffer, OutVariable, Pipelinevariable, verbose, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="9468e-143">`Install-Package` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="9468e-144">Örnekler</span><span class="sxs-lookup"><span data-stu-id="9468e-144">Examples</span></span>

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
