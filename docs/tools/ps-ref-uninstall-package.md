---
title: NuGet kaldırma paketi PowerShell başvurusu
description: Visual Studio'da NuGet Paket Yöneticisi konsolunda Uninstall-Package PowerShell komut başvurusu.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 5969526a12cb6e06f23f35a2481d0385bb9780ab
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="83dc9-103">Uninstall-Package (Visual Studio'da Paket Yöneticisi Konsolu)</span><span class="sxs-lookup"><span data-stu-id="83dc9-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="83dc9-104">*Bu konu içindeki komut açıklar [NuGet Paket Yöneticisi Konsolu](package-manager-console.md) Windows Visual Studio'da. Genel PowerShell Uninstall-Package komutu için bkz: [PowerShell PackageManagement başvuru](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="83dc9-104">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="83dc9-105">Bir paket bağımlılıklarını isteğe bağlı olarak kaldırarak bir projeden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="83dc9-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="83dc9-106">Diğer paketler bu pakete bağlıysa, komut sürece başarısız olur – Force seçeneği.</span><span class="sxs-lookup"><span data-stu-id="83dc9-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="83dc9-107">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="83dc9-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="83dc9-108">Diğer paketler bu pakete bağlıysa, komut sürece başarısız olur – Force seçeneği.</span><span class="sxs-lookup"><span data-stu-id="83dc9-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="83dc9-109">Parametreler</span><span class="sxs-lookup"><span data-stu-id="83dc9-109">Parameters</span></span>

| <span data-ttu-id="83dc9-110">Parametre</span><span class="sxs-lookup"><span data-stu-id="83dc9-110">Parameter</span></span> | <span data-ttu-id="83dc9-111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="83dc9-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="83dc9-112">Kimliği</span><span class="sxs-lookup"><span data-stu-id="83dc9-112">Id</span></span> | <span data-ttu-id="83dc9-113">(Gerekli) Kaldırılacak paketin tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="83dc9-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="83dc9-114">Kimliği anahtarı kendisini isteğe bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="83dc9-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="83dc9-115">Sürüm</span><span class="sxs-lookup"><span data-stu-id="83dc9-115">Version</span></span> | <span data-ttu-id="83dc9-116">Kaldırmak için paketin sürümü şu anda yüklü olan sürümle varsayılan olarak ayarlanıyor.</span><span class="sxs-lookup"><span data-stu-id="83dc9-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="83dc9-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="83dc9-117">RemoveDependencies</span></span> | <span data-ttu-id="83dc9-118">Paketi ve kullanılmayan bağımlılıklarını kaldırın.</span><span class="sxs-lookup"><span data-stu-id="83dc9-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="83dc9-119">Diğer bir deyişle, herhangi bir bağımlılığı bağımlı başka bir paket varsa atlanır.</span><span class="sxs-lookup"><span data-stu-id="83dc9-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="83dc9-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="83dc9-120">ProjectName</span></span> | <span data-ttu-id="83dc9-121">Proje, varsayılan proje için varsayılan değer olarak bu paketi kaldırmak.</span><span class="sxs-lookup"><span data-stu-id="83dc9-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="83dc9-122">Zorla</span><span class="sxs-lookup"><span data-stu-id="83dc9-122">Force</span></span> | <span data-ttu-id="83dc9-123">Diğer paket bağımlı olsa bile kaldırılması için bir paket zorlar.</span><span class="sxs-lookup"><span data-stu-id="83dc9-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="83dc9-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="83dc9-124">WhatIf</span></span> | <span data-ttu-id="83dc9-125">Kaldırma işlemini gerçekleştirmeden çalıştırırken ne olacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="83dc9-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="83dc9-126">Hiçbiri bu parametre ardışık düzen giriş veya joker karakter kabul edin.</span><span class="sxs-lookup"><span data-stu-id="83dc9-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="83dc9-127">Ortak parametreleri</span><span class="sxs-lookup"><span data-stu-id="83dc9-127">Common Parameters</span></span>

<span data-ttu-id="83dc9-128">`Uninstall-Package` Aşağıdaki destekleyen [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, ayrıntı, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="83dc9-128">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="83dc9-129">Örnekler</span><span class="sxs-lookup"><span data-stu-id="83dc9-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
