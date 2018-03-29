---
title: NuGet Install-Package PowerShell başvurusu | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 06/01/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Visual Studio'da NuGet Paket Yöneticisi konsolunda Install-Package PowerShell komut başvurusu.
keywords: NuGet Paket Yöneticisi konsolu, NuGet Powershell komutlarını NuGet Powershell başvurusu, Install-Package
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 99c965c2f8c12c7a59ee48e270172b719c1482ea
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="344c6-104">Install-Package (Visual Studio'da Paket Yöneticisi Konsolu)</span><span class="sxs-lookup"><span data-stu-id="344c6-104">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="344c6-105">*Bu konu içindeki komut açıklar [NuGet Paket Yöneticisi Konsolu](package-manager-console.md) Windows Visual Studio'da. Genel PowerShell Install-Package komutu için bkz: [PowerShell PackageManagement başvuru](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="344c6-105">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="344c6-106">Bir paketi ve bağımlılıklarını projeye yükler.</span><span class="sxs-lookup"><span data-stu-id="344c6-106">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="344c6-107">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="344c6-107">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="344c6-108">NuGet 2.8 + içinde `Install-Package` projenizi mevcut bir pakete düşebilen.</span><span class="sxs-lookup"><span data-stu-id="344c6-108">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="344c6-109">Microsoft.AspNet.MVC 5.1.0-rc1 yüklü varsa, örneğin, aşağıdaki komut, 5.0.0 için düşürmek:</span><span class="sxs-lookup"><span data-stu-id="344c6-109">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="344c6-110">Parametreler</span><span class="sxs-lookup"><span data-stu-id="344c6-110">Parameters</span></span>

| <span data-ttu-id="344c6-111">Parametre</span><span class="sxs-lookup"><span data-stu-id="344c6-111">Parameter</span></span> | <span data-ttu-id="344c6-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="344c6-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="344c6-113">Kimliği</span><span class="sxs-lookup"><span data-stu-id="344c6-113">Id</span></span> | <span data-ttu-id="344c6-114">(Gerekli) Yüklenecek paket tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="344c6-114">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="344c6-115">(*3.0 +*) tanımlayıcı bir yolu veya URL'si olabilir bir `packages.config` dosya veya bir `.nupkg` dosyası.</span><span class="sxs-lookup"><span data-stu-id="344c6-115">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="344c6-116">Kimliği anahtarı kendisini isteğe bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="344c6-116">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="344c6-117">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="344c6-117">IgnoreDependencies</span></span> | <span data-ttu-id="344c6-118">Yalnızca bu paketi ve bağımlılıklarını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="344c6-118">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="344c6-119">ProjectName</span><span class="sxs-lookup"><span data-stu-id="344c6-119">ProjectName</span></span> | <span data-ttu-id="344c6-120">Projeye varsayılan proje için varsayılan değer olarak paketin yükleneceği.</span><span class="sxs-lookup"><span data-stu-id="344c6-120">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="344c6-121">Kaynak</span><span class="sxs-lookup"><span data-stu-id="344c6-121">Source</span></span> | <span data-ttu-id="344c6-122">Aranacak paket kaynağının URL'sini veya klasör yolu.</span><span class="sxs-lookup"><span data-stu-id="344c6-122">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="344c6-123">Yerel klasör yolları mutlak veya göreli geçerli klasörde olabilir.</span><span class="sxs-lookup"><span data-stu-id="344c6-123">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="344c6-124">Atlanırsa, `Install-Package` şu anda seçili paket kaynağını arar.</span><span class="sxs-lookup"><span data-stu-id="344c6-124">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="344c6-125">Sürüm</span><span class="sxs-lookup"><span data-stu-id="344c6-125">Version</span></span> | <span data-ttu-id="344c6-126">Yüklemek için paketin sürümü en son sürüm varsayılan olarak ayarlanıyor.</span><span class="sxs-lookup"><span data-stu-id="344c6-126">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="344c6-127">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="344c6-127">IncludePrerelease</span></span> | <span data-ttu-id="344c6-128">Yükleme için ön sürüm paketlerini göz önünde bulundurur.</span><span class="sxs-lookup"><span data-stu-id="344c6-128">Considers prerelease packages for the install.</span></span> <span data-ttu-id="344c6-129">Atlanırsa, yalnızca kalıcı paketler değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="344c6-129">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="344c6-130">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="344c6-130">FileConflictAction</span></span> | <span data-ttu-id="344c6-131">Üzerine veya varolan dosyaları proje tarafından başvurulan yoksayar istenir olduğunda gerçekleştirilecek eylem.</span><span class="sxs-lookup"><span data-stu-id="344c6-131">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="344c6-132">Olası değerler şunlardır: *üzerine yazma, yoksay, None, OverwriteAll*, ve *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="344c6-132">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="344c6-133">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="344c6-133">DependencyVersion</span></span> | <span data-ttu-id="344c6-134">Şunlardan biri olabilen kullanmak için bağımlılık Paket sürümü:</span><span class="sxs-lookup"><span data-stu-id="344c6-134">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="344c6-135">*En düşük* (varsayılan): en düşük sürüm</span><span class="sxs-lookup"><span data-stu-id="344c6-135">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="344c6-136">*HighestPatch*: en düşük ana, en düşük küçük, en yüksek düzeltme eki sürümüyle</span><span class="sxs-lookup"><span data-stu-id="344c6-136">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="344c6-137">*HighestMinor*: en düşük ana sürümle, en yüksek ikincil, en yüksek düzeltme eki</span><span class="sxs-lookup"><span data-stu-id="344c6-137">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="344c6-138">*En yüksek* (hiçbir parametre güncelleştirme paketi için varsayılan): en yüksek sürüm</span><span class="sxs-lookup"><span data-stu-id="344c6-138">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="344c6-139">Varsayılan değer kullanılarak ayarlayabilirsiniz [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) ayarı `Nuget.Config` dosya.</span><span class="sxs-lookup"><span data-stu-id="344c6-139">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="344c6-140">WhatIf</span><span class="sxs-lookup"><span data-stu-id="344c6-140">WhatIf</span></span> | <span data-ttu-id="344c6-141">Komut gerçekte yükleme yapmadan çalıştırırken ne olacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="344c6-141">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="344c6-142">Hiçbiri bu parametre ardışık düzen giriş veya joker karakter kabul edin.</span><span class="sxs-lookup"><span data-stu-id="344c6-142">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="344c6-143">Ortak parametreleri</span><span class="sxs-lookup"><span data-stu-id="344c6-143">Common Parameters</span></span>

<span data-ttu-id="344c6-144">`Install-Package` Aşağıdaki destekleyen [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, ayrıntı, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="344c6-144">`Install-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="344c6-145">Örnekler</span><span class="sxs-lookup"><span data-stu-id="344c6-145">Examples</span></span>

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
