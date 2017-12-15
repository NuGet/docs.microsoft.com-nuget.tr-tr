---
title: "NuGet kaldırma paketi PowerShell başvurusu | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 6/1/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: f4f5dc79-8e8e-4012-8986-873a5d9283d9
description: "Visual Studio'da NuGet Paket Yöneticisi konsolunda Uninstall-Package PowerShell komut başvurusu."
keywords: "NuGet Paket Yöneticisi konsolu, NuGet Powershell komutlarını NuGet Powershell başvurusu, Uninstall-Package"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 679e89e9cfb16dbe484f133b0b6431313b9d87ac
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="3878c-104">Kaldırma paket (Visual Studio'da Paket Yöneticisi Konsolu)</span><span class="sxs-lookup"><span data-stu-id="3878c-104">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="3878c-105">*Bu konu içindeki komut açıklar [NuGet Paket Yöneticisi Konsolu](Package-Manager-Console.md) Windows Visual Studio'da. Genel PowerShell Uninstall-Package komutu için bkz: [PowerShell PackageManagement başvuru](https://docs.microsoft.com/powershell/module/packagemanagement/?view=powershell-6).*</span><span class="sxs-lookup"><span data-stu-id="3878c-105">*This topic describes the command within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](https://docs.microsoft.com/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="3878c-106">Bir paket bağımlılıklarını isteğe bağlı olarak kaldırarak bir projeden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="3878c-106">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="3878c-107">Diğer paketler bu pakete bağlıysa, komut sürece başarısız olur – Force seçeneği.</span><span class="sxs-lookup"><span data-stu-id="3878c-107">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="3878c-108">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="3878c-108">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="3878c-109">Diğer paketler bu pakete bağlıysa, komut sürece başarısız olur – Force seçeneği.</span><span class="sxs-lookup"><span data-stu-id="3878c-109">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="3878c-110">Parametreler</span><span class="sxs-lookup"><span data-stu-id="3878c-110">Parameters</span></span>

| <span data-ttu-id="3878c-111">Parametre</span><span class="sxs-lookup"><span data-stu-id="3878c-111">Parameter</span></span> | <span data-ttu-id="3878c-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3878c-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3878c-113">Kimliği</span><span class="sxs-lookup"><span data-stu-id="3878c-113">Id</span></span> | <span data-ttu-id="3878c-114">(Gerekli) Kaldırılacak paketin tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="3878c-114">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="3878c-115">Kimliği anahtarı kendisini isteğe bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="3878c-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="3878c-116">Sürüm</span><span class="sxs-lookup"><span data-stu-id="3878c-116">Version</span></span> | <span data-ttu-id="3878c-117">Kaldırmak için paketin sürümü şu anda yüklü olan sürümle varsayılan olarak ayarlanıyor.</span><span class="sxs-lookup"><span data-stu-id="3878c-117">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="3878c-118">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="3878c-118">RemoveDependencies</span></span> | <span data-ttu-id="3878c-119">Paketi ve kullanılmayan bağımlılıklarını kaldırın.</span><span class="sxs-lookup"><span data-stu-id="3878c-119">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="3878c-120">Diğer bir deyişle, herhangi bir bağımlılığı bağımlı başka bir paket varsa atlanır.</span><span class="sxs-lookup"><span data-stu-id="3878c-120">That is, if any dependency has another package that depends on it, it is skipped.</span></span> |
| <span data-ttu-id="3878c-121">ProjectName</span><span class="sxs-lookup"><span data-stu-id="3878c-121">ProjectName</span></span> | <span data-ttu-id="3878c-122">Proje, varsayılan proje için varsayılan değer olarak bu paketi kaldırmak.</span><span class="sxs-lookup"><span data-stu-id="3878c-122">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="3878c-123">Zorla</span><span class="sxs-lookup"><span data-stu-id="3878c-123">Force</span></span> | <span data-ttu-id="3878c-124">Diğer paket bağımlı olsa bile kaldırılması için bir paket zorlar.</span><span class="sxs-lookup"><span data-stu-id="3878c-124">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="3878c-125">WhatIf</span><span class="sxs-lookup"><span data-stu-id="3878c-125">WhatIf</span></span> | <span data-ttu-id="3878c-126">Kaldırma işlemini gerçekleştirmeden çalıştırırken ne olacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="3878c-126">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="3878c-127">Hiçbiri bu parametre ardışık düzen giriş veya joker karakter kabul edin.</span><span class="sxs-lookup"><span data-stu-id="3878c-127">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="3878c-128">Ortak parametreleri</span><span class="sxs-lookup"><span data-stu-id="3878c-128">Common Parameters</span></span>

<span data-ttu-id="3878c-129">`Uninstall-Package`Aşağıdaki destekleyen [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, ayrıntı, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="3878c-129">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="3878c-130">Örnekler</span><span class="sxs-lookup"><span data-stu-id="3878c-130">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
