---
title: NuGet ekleme BindingRedirect PowerShell başvurusu
description: Visual Studio'da NuGet Paket Yöneticisi konsolu Ekle BindingRedirect PowerShell komutunda referansı.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: dec7db04c5cf239863b9c00e9f5bc0dde42c7e47
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551663"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="b2504-103">Add-BindingRedirect (Visual Studio'da Paket Yöneticisi Konsolu)</span><span class="sxs-lookup"><span data-stu-id="b2504-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="b2504-104">*Yalnızca içinde kullanılabilir [NuGet Paket Yöneticisi Konsolu](package-manager-console.md) Windows üzerinde Visual Studio'da.*</span><span class="sxs-lookup"><span data-stu-id="b2504-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="b2504-105">Çıkış yolu için bir proje içindeki tüm derlemeleri inceler ve gerektiğinde uygulama veya web yapılandırma dosyasına bağlama yeniden yönlendirmeleri ekler.</span><span class="sxs-lookup"><span data-stu-id="b2504-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="b2504-106">Bu komut, bir paket yükleme sırasında otomatik olarak çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="b2504-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="b2504-107">Yeniden yönlendirir ve neden kullanılır bağlama hakkında daha fazla bilgi için bkz [derleme sürümlerini yeniden yönlendirme](/dotnet/framework/configure-apps/redirect-assembly-versions) .NET belgelerinde.</span><span class="sxs-lookup"><span data-stu-id="b2504-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="b2504-108">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="b2504-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="b2504-109">Parametreler</span><span class="sxs-lookup"><span data-stu-id="b2504-109">Parameters</span></span>

| <span data-ttu-id="b2504-110">Parametre</span><span class="sxs-lookup"><span data-stu-id="b2504-110">Parameter</span></span> | <span data-ttu-id="b2504-111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b2504-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b2504-112">ProjectName</span><span class="sxs-lookup"><span data-stu-id="b2504-112">ProjectName</span></span> | <span data-ttu-id="b2504-113">(Gerekli) Hangi bağlama yeniden yönlendirmeleri eklemek proje.</span><span class="sxs-lookup"><span data-stu-id="b2504-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="b2504-114">-ProjectName anahtar isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="b2504-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="b2504-115">Hiçbiri bu parametre ardışık düzen giriş veya joker karakterler kabul edin.</span><span class="sxs-lookup"><span data-stu-id="b2504-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="b2504-116">Ortak parametreleri</span><span class="sxs-lookup"><span data-stu-id="b2504-116">Common Parameters</span></span>

<span data-ttu-id="b2504-117">`Add-BindingRedirect` şunları desteklemektedir [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, ayrıntılı, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="b2504-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="b2504-118">Örnekler</span><span class="sxs-lookup"><span data-stu-id="b2504-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```