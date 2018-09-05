---
title: NuGet kaldırma-Package PowerShell başvurusu
description: Visual Studio'da NuGet Paket Yöneticisi konsolunda paket kaldırma PowerShell komutunu referansı.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: ae60473fbb716b23f40b0605be8aaa8515802315
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551649"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="1cda4-103">Uninstall-Package (Visual Studio'da Paket Yöneticisi Konsolu)</span><span class="sxs-lookup"><span data-stu-id="1cda4-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="1cda4-104">*Bu konu içindeki komut açıklar [NuGet Paket Yöneticisi Konsolu](package-manager-console.md) Windows üzerinde Visual Studio'da. Genel PowerShell paket kaldırma komutu için bkz: [PowerShell PackageManagement başvuru](/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="1cda4-104">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="1cda4-105">Bir paket bağımlılıklarını isteğe bağlı olarak kaldırarak bir projeden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="1cda4-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="1cda4-106">Diğer paketleri bu pakete bağlıdır, komut sürece başarısız olur Force seçeneği belirtildi.</span><span class="sxs-lookup"><span data-stu-id="1cda4-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="1cda4-107">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="1cda4-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="1cda4-108">Diğer paketleri bu pakete bağlıdır, komut sürece başarısız olur Force seçeneği belirtildi.</span><span class="sxs-lookup"><span data-stu-id="1cda4-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="1cda4-109">Parametreler</span><span class="sxs-lookup"><span data-stu-id="1cda4-109">Parameters</span></span>

| <span data-ttu-id="1cda4-110">Parametre</span><span class="sxs-lookup"><span data-stu-id="1cda4-110">Parameter</span></span> | <span data-ttu-id="1cda4-111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1cda4-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1cda4-112">Kimliği</span><span class="sxs-lookup"><span data-stu-id="1cda4-112">Id</span></span> | <span data-ttu-id="1cda4-113">(Gerekli) Kaldırmak için paket tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="1cda4-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="1cda4-114">Kimliği anahtarın kendisinde, isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="1cda4-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="1cda4-115">Sürüm</span><span class="sxs-lookup"><span data-stu-id="1cda4-115">Version</span></span> | <span data-ttu-id="1cda4-116">Kaldırmak için paket sürümünü şu anda yüklü sürümü için varsayılan olarak ayarlanıyor.</span><span class="sxs-lookup"><span data-stu-id="1cda4-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="1cda4-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="1cda4-117">RemoveDependencies</span></span> | <span data-ttu-id="1cda4-118">Paket ve kullanılmayan bağımlılıkları kaldırın.</span><span class="sxs-lookup"><span data-stu-id="1cda4-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="1cda4-119">Diğer bir deyişle, herhangi bir bağımlılık bağımlı başka bir paket varsa atlanır.</span><span class="sxs-lookup"><span data-stu-id="1cda4-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="1cda4-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="1cda4-120">ProjectName</span></span> | <span data-ttu-id="1cda4-121">Projeden olduğu için varsayılan proje varsayılan olarak ayarlanıyor. Bu paketi kaldırın.</span><span class="sxs-lookup"><span data-stu-id="1cda4-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="1cda4-122">Zorla</span><span class="sxs-lookup"><span data-stu-id="1cda4-122">Force</span></span> | <span data-ttu-id="1cda4-123">Diğer paketleri bağımlı bile paketini kaldırılması için zorlar.</span><span class="sxs-lookup"><span data-stu-id="1cda4-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="1cda4-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="1cda4-124">WhatIf</span></span> | <span data-ttu-id="1cda4-125">Kaldırma işlemini gerçekleştirmeden komutu çalıştırırken ne olacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="1cda4-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="1cda4-126">Hiçbiri bu parametre ardışık düzen giriş veya joker karakterler kabul edin.</span><span class="sxs-lookup"><span data-stu-id="1cda4-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="1cda4-127">Ortak parametreleri</span><span class="sxs-lookup"><span data-stu-id="1cda4-127">Common Parameters</span></span>

<span data-ttu-id="1cda4-128">`Uninstall-Package` şunları desteklemektedir [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, ayrıntılı, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="1cda4-128">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="1cda4-129">Örnekler</span><span class="sxs-lookup"><span data-stu-id="1cda4-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
