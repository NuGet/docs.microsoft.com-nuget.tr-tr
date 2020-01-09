---
title: NuGet Uninstall-Package PowerShell Başvurusu
description: Visual Studio 'daki NuGet Paket Yöneticisi konsolundaki Uninstall-Package PowerShell komutu için başvuru.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 05b7bf0e8abad0904b9e851ea6b7a5317e74229d
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384421"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="090a6-103">Uninstall-Package (Visual Studio'da Paket Yöneticisi Konsolu)</span><span class="sxs-lookup"><span data-stu-id="090a6-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="090a6-104">*Bu konuda, Windows üzerinde Visual Studio 'da [Paket Yöneticisi konsolu](../../consume-packages/install-use-packages-powershell.md) içindeki komut açıklanmaktadır. Genel PowerShell Uninstall-Package komutu için bkz. [PowerShell PackageManagement başvurusu](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="090a6-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="090a6-105">, İsteğe bağlı olarak bağımlılıklarını kaldırarak bir projeden paket kaldırır.</span><span class="sxs-lookup"><span data-stu-id="090a6-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="090a6-106">Diğer paketler bu pakete bağımlıysa, – zorlama seçeneği belirtilmediği takdirde komut başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="090a6-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="090a6-107">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="090a6-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="090a6-108">Diğer paketler bu pakete bağımlıysa, – zorlama seçeneği belirtilmediği takdirde komut başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="090a6-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="090a6-109">Parametreler</span><span class="sxs-lookup"><span data-stu-id="090a6-109">Parameters</span></span>

| <span data-ttu-id="090a6-110">Parametre</span><span class="sxs-lookup"><span data-stu-id="090a6-110">Parameter</span></span> | <span data-ttu-id="090a6-111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="090a6-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="090a6-112">Id</span><span class="sxs-lookup"><span data-stu-id="090a6-112">Id</span></span> | <span data-ttu-id="090a6-113">Istenir Kaldırılacak paketin tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="090a6-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="090a6-114">-ID anahtarı isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="090a6-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="090a6-115">Sürüm</span><span class="sxs-lookup"><span data-stu-id="090a6-115">Version</span></span> | <span data-ttu-id="090a6-116">Kaldırılacak paketin sürümü, şu anda yüklü olan sürüme varsayılan olarak ayarlanıyor.</span><span class="sxs-lookup"><span data-stu-id="090a6-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="090a6-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="090a6-117">RemoveDependencies</span></span> | <span data-ttu-id="090a6-118">Paketi ve kullanılmayan bağımlılıklarını kaldırın.</span><span class="sxs-lookup"><span data-stu-id="090a6-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="090a6-119">Diğer bir deyişle, herhangi bir bağımlılığın kendisine bağımlı başka bir paketi varsa, bu atlanır.</span><span class="sxs-lookup"><span data-stu-id="090a6-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="090a6-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="090a6-120">ProjectName</span></span> | <span data-ttu-id="090a6-121">Paketin kaldırılacağı proje, varsayılan proje varsayılan olarak ayarlanıyor.</span><span class="sxs-lookup"><span data-stu-id="090a6-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="090a6-122">Force</span><span class="sxs-lookup"><span data-stu-id="090a6-122">Force</span></span> | <span data-ttu-id="090a6-123">Başka paketler buna bağımlı olsa bile, bir paketi kaldırılmasına zorlar.</span><span class="sxs-lookup"><span data-stu-id="090a6-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="090a6-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="090a6-124">WhatIf</span></span> | <span data-ttu-id="090a6-125">, Kaldırma işlemi yapılmadan komutu çalıştırırken ne olacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="090a6-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="090a6-126">Bu parametrelerin hiçbiri, işlem hattı girişi veya joker karakterler kabul etmez.</span><span class="sxs-lookup"><span data-stu-id="090a6-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="090a6-127">Ortak Parametreler</span><span class="sxs-lookup"><span data-stu-id="090a6-127">Common Parameters</span></span>

<span data-ttu-id="090a6-128">`Uninstall-Package`, şu [ortak PowerShell parametrelerini](https://go.microsoft.com/fwlink/?LinkID=113216)destekler: Hata Ayıkla, hata eylemi, ErrorVariable, OutBuffer, OutVariable, Pipelinevariable, verbose, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="090a6-128">`Uninstall-Package` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="090a6-129">Örnekler</span><span class="sxs-lookup"><span data-stu-id="090a6-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
