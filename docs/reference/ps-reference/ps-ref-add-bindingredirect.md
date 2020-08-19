---
title: NuGet Add-BindingRedirect PowerShell Başvurusu
description: Visual Studio 'daki NuGet Paket Yöneticisi konsolundaki Add-BindingRedirect PowerShell komutu için başvuru.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: f5ba4bd8140fa8cac7da8bf1351ad5448671b768
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623129"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="60c40-103">Add-BindingRedirect (Visual Studio 'da Paket Yöneticisi konsolu)</span><span class="sxs-lookup"><span data-stu-id="60c40-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="60c40-104">*Yalnızca Windows üzerinde Visual Studio 'da bulunan [Paket Yöneticisi konsolu](../../consume-packages/install-use-packages-powershell.md) içinde kullanılabilir.*</span><span class="sxs-lookup"><span data-stu-id="60c40-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="60c40-105">Bir projenin çıkış yolundaki tüm derlemeleri inceler ve gerektiğinde uygulamaya veya Web yapılandırma dosyasına bağlama yeniden yönlendirmeleri ekler.</span><span class="sxs-lookup"><span data-stu-id="60c40-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="60c40-106">Bu komut, bir paket yüklenirken otomatik olarak çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="60c40-106">This command is run automatically when installing a package.</span></span>

> [!NOTE]
> <span data-ttu-id="60c40-107">Bu yalnızca bir packages.config dosyası kullanan senaryolar için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="60c40-107">This only applies to scenarios using a packages.config file.</span></span> <span data-ttu-id="60c40-108">Daha fazla bilgi için bkz. [NuGet packages.config dosya başvurusu](~/reference/packages-config.md).</span><span class="sxs-lookup"><span data-stu-id="60c40-108">For more information, see [NuGet packages.config file reference](~/reference/packages-config.md).</span></span>

<span data-ttu-id="60c40-109">Bağlama yeniden yönlendirmeleri ve bunların kullanılma nedenleri hakkında daha fazla bilgi için bkz. .NET belgelerindeki [derleme sürümlerini yeniden yönlendirme](/dotnet/framework/configure-apps/redirect-assembly-versions) .</span><span class="sxs-lookup"><span data-stu-id="60c40-109">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="60c40-110">Söz dizimi</span><span class="sxs-lookup"><span data-stu-id="60c40-110">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="60c40-111">Parametreler</span><span class="sxs-lookup"><span data-stu-id="60c40-111">Parameters</span></span>

| <span data-ttu-id="60c40-112">Parametre</span><span class="sxs-lookup"><span data-stu-id="60c40-112">Parameter</span></span> | <span data-ttu-id="60c40-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="60c40-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="60c40-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="60c40-114">ProjectName</span></span> | <span data-ttu-id="60c40-115">Istenir Bağlama yeniden yönlendirmelerinin ekleneceği proje.</span><span class="sxs-lookup"><span data-stu-id="60c40-115">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="60c40-116">-ProjectName anahtarı isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="60c40-116">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="60c40-117">Bu parametrelerin hiçbiri, işlem hattı girişi veya joker karakterler kabul etmez.</span><span class="sxs-lookup"><span data-stu-id="60c40-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="60c40-118">Ortak Parametreler</span><span class="sxs-lookup"><span data-stu-id="60c40-118">Common Parameters</span></span>

<span data-ttu-id="60c40-119">`Add-BindingRedirect` Şu [ortak PowerShell parametrelerini](https://go.microsoft.com/fwlink/?LinkID=113216)destekler: Hata Ayıkla, hata eylemi, ErrorVariable, OutBuffer, OutVariable, Pipelinevariable, verbose, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="60c40-119">`Add-BindingRedirect` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="60c40-120">Örnekler</span><span class="sxs-lookup"><span data-stu-id="60c40-120">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```
