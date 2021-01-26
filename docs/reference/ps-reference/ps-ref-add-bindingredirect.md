---
title: NuGet Add-BindingRedirect PowerShell Başvurusu
description: Visual Studio 'daki NuGet Paket Yöneticisi konsolundaki Add-BindingRedirect PowerShell komutuna yönelik başvuru.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 62edf1bf8995a4e1ffb83acc7a7621a786cc53e4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777612"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="d8bc3-103">Add-BindingRedirect (Visual Studio 'da Paket Yöneticisi konsolu)</span><span class="sxs-lookup"><span data-stu-id="d8bc3-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="d8bc3-104">*Yalnızca Windows üzerinde Visual Studio 'da bulunan [Paket Yöneticisi konsolu](../../consume-packages/install-use-packages-powershell.md) içinde kullanılabilir.*</span><span class="sxs-lookup"><span data-stu-id="d8bc3-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="d8bc3-105">Bir projenin çıkış yolundaki tüm derlemeleri inceler ve gerektiğinde uygulamaya veya Web yapılandırma dosyasına bağlama yeniden yönlendirmeleri ekler.</span><span class="sxs-lookup"><span data-stu-id="d8bc3-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="d8bc3-106">Bu komut, bir paket yüklenirken otomatik olarak çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="d8bc3-106">This command is run automatically when installing a package.</span></span>

> [!NOTE]
> <span data-ttu-id="d8bc3-107">Bu yalnızca bir packages.config dosyası kullanan senaryolar için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="d8bc3-107">This only applies to scenarios using a packages.config file.</span></span> <span data-ttu-id="d8bc3-108">Daha fazla bilgi için bkz. [NuGet packages.config dosya başvurusu](~/reference/packages-config.md).</span><span class="sxs-lookup"><span data-stu-id="d8bc3-108">For more information, see [NuGet packages.config file reference](~/reference/packages-config.md).</span></span>

<span data-ttu-id="d8bc3-109">Bağlama yeniden yönlendirmeleri ve bunların kullanılma nedenleri hakkında daha fazla bilgi için bkz. .NET belgelerindeki [derleme sürümlerini yeniden yönlendirme](/dotnet/framework/configure-apps/redirect-assembly-versions) .</span><span class="sxs-lookup"><span data-stu-id="d8bc3-109">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="d8bc3-110">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="d8bc3-110">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="d8bc3-111">Parametreler</span><span class="sxs-lookup"><span data-stu-id="d8bc3-111">Parameters</span></span>

| <span data-ttu-id="d8bc3-112">Parametre</span><span class="sxs-lookup"><span data-stu-id="d8bc3-112">Parameter</span></span> | <span data-ttu-id="d8bc3-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d8bc3-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d8bc3-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="d8bc3-114">ProjectName</span></span> | <span data-ttu-id="d8bc3-115">Istenir Bağlama yeniden yönlendirmelerinin ekleneceği proje.</span><span class="sxs-lookup"><span data-stu-id="d8bc3-115">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="d8bc3-116">-ProjectName anahtarı isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="d8bc3-116">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="d8bc3-117">Bu parametrelerin hiçbiri, işlem hattı girişi veya joker karakterler kabul etmez.</span><span class="sxs-lookup"><span data-stu-id="d8bc3-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="d8bc3-118">Ortak Parametreler</span><span class="sxs-lookup"><span data-stu-id="d8bc3-118">Common Parameters</span></span>

<span data-ttu-id="d8bc3-119">`Add-BindingRedirect` Şu [ortak PowerShell parametrelerini](/powershell/module/microsoft.powershell.core/about/about_commonparameters)destekler: Hata Ayıkla, hata eylemi, ErrorVariable, OutBuffer, OutVariable, Pipelinevariable, verbose, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="d8bc3-119">`Add-BindingRedirect` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="d8bc3-120">Örnekler</span><span class="sxs-lookup"><span data-stu-id="d8bc3-120">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```