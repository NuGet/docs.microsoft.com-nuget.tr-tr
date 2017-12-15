---
title: "NuGet Install-Package PowerShell başvurusu | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 6/1/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 879db0ef-6b72-4a4a-bb68-f9e3a00f64b8
description: "Visual Studio'da NuGet Paket Yöneticisi konsolunda Install-Package PowerShell komut başvurusu."
keywords: "NuGet Paket Yöneticisi konsolu, NuGet Powershell komutlarını NuGet Powershell başvurusu, Install-Package"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d51cce6223cd2d89c555ca9d6e936eaadf3757bb
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="3166e-104">Install-Package (Visual Studio'da Paket Yöneticisi Konsolu)</span><span class="sxs-lookup"><span data-stu-id="3166e-104">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="3166e-105">*Bu konu içindeki komut açıklar [NuGet Paket Yöneticisi Konsolu](Package-Manager-Console.md) Windows Visual Studio'da. Genel PowerShell Install-Package komutu için bkz: [PowerShell PackageManagement başvuru](https://docs.microsoft.com/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="3166e-105">*This topic describes the command within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](https://docs.microsoft.com/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="3166e-106">Bir paketi ve bağımlılıklarını projeye yükler.</span><span class="sxs-lookup"><span data-stu-id="3166e-106">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="3166e-107">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="3166e-107">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="3166e-108">NuGet 2.8 + içinde `Install-Package` projenizi mevcut bir pakete düşebilen.</span><span class="sxs-lookup"><span data-stu-id="3166e-108">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="3166e-109">Microsoft.AspNet.MVC 5.1.0-rc1 yüklü varsa, örneğin, aşağıdaki komut, 5.0.0 için düşürmek:</span><span class="sxs-lookup"><span data-stu-id="3166e-109">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

<span data-ttu-id="3166e-110">NuGet 2.7 ve daha önceki bir sürümü zaten yüklü olduğunu bildiren bir hata verir.</span><span class="sxs-lookup"><span data-stu-id="3166e-110">NuGet 2.7 and earlier gives an error saying that a newer version is already installed.</span></span>
  
## <a name="parameters"></a><span data-ttu-id="3166e-111">Parametreler</span><span class="sxs-lookup"><span data-stu-id="3166e-111">Parameters</span></span>

| <span data-ttu-id="3166e-112">Parametre</span><span class="sxs-lookup"><span data-stu-id="3166e-112">Parameter</span></span> | <span data-ttu-id="3166e-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3166e-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3166e-114">Kimliği</span><span class="sxs-lookup"><span data-stu-id="3166e-114">Id</span></span> | <span data-ttu-id="3166e-115">(Gerekli) Yüklenecek paket tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="3166e-115">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="3166e-116">(*3.0 +*) tanımlayıcı bir yolu veya URL'si olabilir bir `packages.config` dosya veya bir `.nupkg` dosyası.</span><span class="sxs-lookup"><span data-stu-id="3166e-116">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="3166e-117">Kimliği anahtarı kendisini isteğe bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="3166e-117">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="3166e-118">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="3166e-118">IgnoreDependencies</span></span> | <span data-ttu-id="3166e-119">Yalnızca bu paketi ve bağımlılıklarını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="3166e-119">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="3166e-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="3166e-120">ProjectName</span></span> | <span data-ttu-id="3166e-121">Projeye varsayılan proje için varsayılan değer olarak paketin yükleneceği.</span><span class="sxs-lookup"><span data-stu-id="3166e-121">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="3166e-122">Kaynak</span><span class="sxs-lookup"><span data-stu-id="3166e-122">Source</span></span> | <span data-ttu-id="3166e-123">Aranacak paket kaynağının URL'sini veya klasör yolu.</span><span class="sxs-lookup"><span data-stu-id="3166e-123">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="3166e-124">Yerel klasör yolları mutlak veya göreli geçerli klasörde olabilir.</span><span class="sxs-lookup"><span data-stu-id="3166e-124">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="3166e-125">Atlanırsa, `Install-Package` şu anda seçili paket kaynağını arar.</span><span class="sxs-lookup"><span data-stu-id="3166e-125">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="3166e-126">Sürüm</span><span class="sxs-lookup"><span data-stu-id="3166e-126">Version</span></span> | <span data-ttu-id="3166e-127">Yüklemek için paketin sürümü en son sürüm varsayılan olarak ayarlanıyor.</span><span class="sxs-lookup"><span data-stu-id="3166e-127">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="3166e-128">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="3166e-128">IncludePrerelease</span></span> | <span data-ttu-id="3166e-129">Yükleme için ön sürüm paketlerini göz önünde bulundurur.</span><span class="sxs-lookup"><span data-stu-id="3166e-129">Considers prerelease packages for the install.</span></span> <span data-ttu-id="3166e-130">Atlanırsa, yalnızca kalıcı paketler değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="3166e-130">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="3166e-131">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="3166e-131">FileConflictAction</span></span> | <span data-ttu-id="3166e-132">Üzerine veya varolan dosyaları proje tarafından başvurulan yoksayar istenir olduğunda gerçekleştirilecek eylem.</span><span class="sxs-lookup"><span data-stu-id="3166e-132">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="3166e-133">Olası değerler şunlardır: *üzerine yazma, yoksay, None, OverwriteAll*, ve *(3.0 +)* *IgnoreAll*.</span><span class="sxs-lookup"><span data-stu-id="3166e-133">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="3166e-134">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="3166e-134">DependencyVersion</span></span> | <span data-ttu-id="3166e-135">Şunlardan biri olabilen kullanmak için bağımlılık Paket sürümü:</span><span class="sxs-lookup"><span data-stu-id="3166e-135">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="3166e-136">*En düşük* (varsayılan): en düşük sürüm</span><span class="sxs-lookup"><span data-stu-id="3166e-136">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="3166e-137">*HighestPatch*: en düşük ana, en düşük küçük, en yüksek düzeltme eki sürümüyle</span><span class="sxs-lookup"><span data-stu-id="3166e-137">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="3166e-138">*HighestMinor*: en düşük ana sürümle, en yüksek ikincil, en yüksek düzeltme eki</span><span class="sxs-lookup"><span data-stu-id="3166e-138">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="3166e-139">*En yüksek* (hiçbir parametre güncelleştirme paketi için varsayılan): en yüksek sürüm</span><span class="sxs-lookup"><span data-stu-id="3166e-139">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="3166e-140">Varsayılan değer kullanılarak ayarlayabilirsiniz [ `dependencyVersion` ](../Schema/nuget-config-file.md#config-section) ayarı `Nuget.Config` dosya.</span><span class="sxs-lookup"><span data-stu-id="3166e-140">You can set the default value using the [`dependencyVersion`](../Schema/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="3166e-141">WhatIf</span><span class="sxs-lookup"><span data-stu-id="3166e-141">WhatIf</span></span> | <span data-ttu-id="3166e-142">Komut gerçekte yükleme yapmadan çalıştırırken ne olacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="3166e-142">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="3166e-143">Hiçbiri bu parametre ardışık düzen giriş veya joker karakter kabul edin.</span><span class="sxs-lookup"><span data-stu-id="3166e-143">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="3166e-144">Ortak parametreleri</span><span class="sxs-lookup"><span data-stu-id="3166e-144">Common Parameters</span></span>

<span data-ttu-id="3166e-145">`Install-Package`Aşağıdaki destekleyen [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, ayrıntı, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="3166e-145">`Install-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="3166e-146">Örnekler</span><span class="sxs-lookup"><span data-stu-id="3166e-146">Examples</span></span>

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project.
Install-package https://raw.githubusercontent.com/json-ld.net/master/src/JsonLD/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages.
Install-package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
Install-package https://az320820.vo.msecnd.net/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
