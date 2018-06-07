---
title: NuGet ekleme BindingRedirect PowerShell başvurusu
description: Visual Studio'da NuGet Paket Yöneticisi konsolunda Ekle BindingRedirect PowerShell komut başvurusu.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: f3addd95b64d78eac201deeb2c64915ea935cd71
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817629"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="46bc3-103">Add-BindingRedirect (Visual Studio'da Paket Yöneticisi Konsolu)</span><span class="sxs-lookup"><span data-stu-id="46bc3-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="46bc3-104">*Yalnızca içinde kullanılabilir [NuGet Paket Yöneticisi Konsolu](package-manager-console.md) Windows Visual Studio'da.*</span><span class="sxs-lookup"><span data-stu-id="46bc3-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="46bc3-105">Bir proje için çıkış yolu içindeki tüm derlemelerde arar ve gerektiğinde uygulama veya web yapılandırma dosyasına bağlama yeniden yönlendirmelerini ekler.</span><span class="sxs-lookup"><span data-stu-id="46bc3-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="46bc3-106">Bu komut, bir paket yüklerken otomatik olarak çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="46bc3-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="46bc3-107">Bağlama yeniden yönlendirmeleri ve neden kullanıldıkları hakkında ayrıntılar için bkz: [derleme sürümlerini yönlendirme](/dotnet/framework/configure-apps/redirect-assembly-versions) .NET belgelerinde.</span><span class="sxs-lookup"><span data-stu-id="46bc3-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="46bc3-108">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="46bc3-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="46bc3-109">Parametreler</span><span class="sxs-lookup"><span data-stu-id="46bc3-109">Parameters</span></span>

| <span data-ttu-id="46bc3-110">Parametre</span><span class="sxs-lookup"><span data-stu-id="46bc3-110">Parameter</span></span> | <span data-ttu-id="46bc3-111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="46bc3-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="46bc3-112">ProjectName</span><span class="sxs-lookup"><span data-stu-id="46bc3-112">ProjectName</span></span> | <span data-ttu-id="46bc3-113">(Gerekli) Bağlama yeniden yönlendirmeleri eklenecek projesi.</span><span class="sxs-lookup"><span data-stu-id="46bc3-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="46bc3-114">-ProjectName anahtar isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="46bc3-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="46bc3-115">Hiçbiri bu parametre ardışık düzen giriş veya joker karakter kabul edin.</span><span class="sxs-lookup"><span data-stu-id="46bc3-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="46bc3-116">Ortak parametreleri</span><span class="sxs-lookup"><span data-stu-id="46bc3-116">Common Parameters</span></span>

<span data-ttu-id="46bc3-117">`Add-BindingRedirect` Aşağıdaki destekleyen [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, ayrıntı, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="46bc3-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="46bc3-118">Örnekler</span><span class="sxs-lookup"><span data-stu-id="46bc3-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```