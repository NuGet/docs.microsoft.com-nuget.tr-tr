---
title: NuGet Add-BindingRedirect PowerShell Başvurusu
description: Visual Studio 'daki NuGet Paket Yöneticisi konsolundaki Add-BindingRedirect PowerShell komutu için başvuru.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: b1e88d32deb3ff34833ef22a9cbb8cad3f0d4354
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68328242"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="341af-103">Add-BindingRedirect (Visual Studio'da Paket Yöneticisi Konsolu)</span><span class="sxs-lookup"><span data-stu-id="341af-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="341af-104">*Yalnızca Windows üzerinde Visual Studio 'da bulunan [Paket Yöneticisi konsolu](../../consume-packages/install-use-packages-powershell.md) içinde kullanılabilir.*</span><span class="sxs-lookup"><span data-stu-id="341af-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="341af-105">Bir projenin çıkış yolundaki tüm derlemeleri inceler ve gerektiğinde uygulamaya veya Web yapılandırma dosyasına bağlama yeniden yönlendirmeleri ekler.</span><span class="sxs-lookup"><span data-stu-id="341af-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="341af-106">Bu komut, bir paket yüklenirken otomatik olarak çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="341af-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="341af-107">Bağlama yeniden yönlendirmeleri ve bunların kullanılma nedenleri hakkında daha fazla bilgi için bkz. .NET belgelerindeki [derleme sürümlerini yeniden yönlendirme](/dotnet/framework/configure-apps/redirect-assembly-versions) .</span><span class="sxs-lookup"><span data-stu-id="341af-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="341af-108">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="341af-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="341af-109">Parametreler</span><span class="sxs-lookup"><span data-stu-id="341af-109">Parameters</span></span>

| <span data-ttu-id="341af-110">Parametre</span><span class="sxs-lookup"><span data-stu-id="341af-110">Parameter</span></span> | <span data-ttu-id="341af-111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="341af-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="341af-112">ProjectName</span><span class="sxs-lookup"><span data-stu-id="341af-112">ProjectName</span></span> | <span data-ttu-id="341af-113">Istenir Bağlama yeniden yönlendirmelerinin ekleneceği proje.</span><span class="sxs-lookup"><span data-stu-id="341af-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="341af-114">-ProjectName anahtarı isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="341af-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="341af-115">Bu parametrelerin hiçbiri, işlem hattı girişi veya joker karakterler kabul etmez.</span><span class="sxs-lookup"><span data-stu-id="341af-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="341af-116">Ortak Parametreler</span><span class="sxs-lookup"><span data-stu-id="341af-116">Common Parameters</span></span>

<span data-ttu-id="341af-117">`Add-BindingRedirect`Aşağıdaki [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216)destekler: Hata Ayıkla, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, verbose, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="341af-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="341af-118">Örnekler</span><span class="sxs-lookup"><span data-stu-id="341af-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```