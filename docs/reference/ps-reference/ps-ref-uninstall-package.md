---
title: NuGet Uninstall-Package PowerShell Başvurusu
description: Visual Studio 'daki NuGet Paket Yöneticisi konsolundaki Uninstall-Package PowerShell komutuna yönelik başvuru.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: d164176355e32e5bbe0a017fc2b291cbc9ef326a
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237133"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="28a78-103">Uninstall-Package (Visual Studio 'da Paket Yöneticisi konsolu)</span><span class="sxs-lookup"><span data-stu-id="28a78-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="28a78-104">*Bu konuda, Windows üzerinde Visual Studio 'da [Paket Yöneticisi konsolu](../../consume-packages/install-use-packages-powershell.md) içindeki komut açıklanmaktadır. Genel PowerShell Uninstall-Package komutu için bkz. [PowerShell PackageManagement başvurusu](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="28a78-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="28a78-105">, İsteğe bağlı olarak bağımlılıklarını kaldırarak bir projeden paket kaldırır.</span><span class="sxs-lookup"><span data-stu-id="28a78-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="28a78-106">Diğer paketler bu pakete bağımlıysa, – zorlama seçeneği belirtilmediği takdirde komut başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="28a78-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="28a78-107">Syntax</span><span class="sxs-lookup"><span data-stu-id="28a78-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="28a78-108">Diğer paketler bu pakete bağımlıysa, – zorlama seçeneği belirtilmediği takdirde komut başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="28a78-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="28a78-109">Parametreler</span><span class="sxs-lookup"><span data-stu-id="28a78-109">Parameters</span></span>

| <span data-ttu-id="28a78-110">Parametre</span><span class="sxs-lookup"><span data-stu-id="28a78-110">Parameter</span></span> | <span data-ttu-id="28a78-111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="28a78-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="28a78-112">Id</span><span class="sxs-lookup"><span data-stu-id="28a78-112">Id</span></span> | <span data-ttu-id="28a78-113">Istenir Kaldırılacak paketin tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="28a78-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="28a78-114">-ID anahtarı isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="28a78-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="28a78-115">Sürüm</span><span class="sxs-lookup"><span data-stu-id="28a78-115">Version</span></span> | <span data-ttu-id="28a78-116">Kaldırılacak paketin sürümü, şu anda yüklü olan sürüme varsayılan olarak ayarlanıyor.</span><span class="sxs-lookup"><span data-stu-id="28a78-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="28a78-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="28a78-117">RemoveDependencies</span></span> | <span data-ttu-id="28a78-118">Paketi ve kullanılmayan bağımlılıklarını kaldırın.</span><span class="sxs-lookup"><span data-stu-id="28a78-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="28a78-119">Diğer bir deyişle, herhangi bir bağımlılığın kendisine bağımlı başka bir paketi varsa, bu atlanır.</span><span class="sxs-lookup"><span data-stu-id="28a78-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="28a78-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="28a78-120">ProjectName</span></span> | <span data-ttu-id="28a78-121">Paketin kaldırılacağı proje, varsayılan proje varsayılan olarak ayarlanıyor.</span><span class="sxs-lookup"><span data-stu-id="28a78-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="28a78-122">Force</span><span class="sxs-lookup"><span data-stu-id="28a78-122">Force</span></span> | <span data-ttu-id="28a78-123">Başka paketler buna bağımlı olsa bile, bir paketi kaldırılmasına zorlar.</span><span class="sxs-lookup"><span data-stu-id="28a78-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="28a78-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="28a78-124">WhatIf</span></span> | <span data-ttu-id="28a78-125">, Kaldırma işlemi yapılmadan komutu çalıştırırken ne olacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="28a78-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="28a78-126">Bu parametrelerin hiçbiri, işlem hattı girişi veya joker karakterler kabul etmez.</span><span class="sxs-lookup"><span data-stu-id="28a78-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="28a78-127">Ortak Parametreler</span><span class="sxs-lookup"><span data-stu-id="28a78-127">Common Parameters</span></span>

<span data-ttu-id="28a78-128">`Uninstall-Package` Şu [ortak PowerShell parametrelerini](/powershell/module/microsoft.powershell.core/about/about_commonparameters)destekler: Hata Ayıkla, hata eylemi, ErrorVariable, OutBuffer, OutVariable, Pipelinevariable, verbose, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="28a78-128">`Uninstall-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="28a78-129">Örnekler</span><span class="sxs-lookup"><span data-stu-id="28a78-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```