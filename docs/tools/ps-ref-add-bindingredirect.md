---
title: NuGet ekleme BindingRedirect PowerShell başvurusu
description: Visual Studio'da NuGet Paket Yöneticisi konsolu Ekle BindingRedirect PowerShell komutunda referansı.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a5f318ddfb2bb8498ab3e608f8036be05dcb0706
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842534"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="983af-103">Add-BindingRedirect (Visual Studio'da Paket Yöneticisi Konsolu)</span><span class="sxs-lookup"><span data-stu-id="983af-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="983af-104">*Yalnızca içinde kullanılabilir [Paket Yöneticisi Konsolu](package-manager-console.md) Windows üzerinde Visual Studio'da.*</span><span class="sxs-lookup"><span data-stu-id="983af-104">*Available only within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="983af-105">Çıkış yolu için bir proje içindeki tüm derlemeleri inceler ve gerektiğinde uygulama veya web yapılandırma dosyasına bağlama yeniden yönlendirmeleri ekler.</span><span class="sxs-lookup"><span data-stu-id="983af-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="983af-106">Bu komut, bir paket yükleme sırasında otomatik olarak çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="983af-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="983af-107">Yeniden yönlendirir ve neden kullanılır bağlama hakkında daha fazla bilgi için bkz [derleme sürümlerini yeniden yönlendirme](/dotnet/framework/configure-apps/redirect-assembly-versions) .NET belgelerinde.</span><span class="sxs-lookup"><span data-stu-id="983af-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="983af-108">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="983af-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="983af-109">Parametreler</span><span class="sxs-lookup"><span data-stu-id="983af-109">Parameters</span></span>

| <span data-ttu-id="983af-110">Parametre</span><span class="sxs-lookup"><span data-stu-id="983af-110">Parameter</span></span> | <span data-ttu-id="983af-111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="983af-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="983af-112">ProjectName</span><span class="sxs-lookup"><span data-stu-id="983af-112">ProjectName</span></span> | <span data-ttu-id="983af-113">(Gerekli) Hangi bağlama yeniden yönlendirmeleri eklemek proje.</span><span class="sxs-lookup"><span data-stu-id="983af-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="983af-114">-ProjectName anahtar isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="983af-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="983af-115">Hiçbiri bu parametre ardışık düzen giriş veya joker karakterler kabul edin.</span><span class="sxs-lookup"><span data-stu-id="983af-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="983af-116">Ortak parametreleri</span><span class="sxs-lookup"><span data-stu-id="983af-116">Common Parameters</span></span>

<span data-ttu-id="983af-117">`Add-BindingRedirect` şunları desteklemektedir [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): Hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, ayrıntılı PipelineVariable, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="983af-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="983af-118">Örnekler</span><span class="sxs-lookup"><span data-stu-id="983af-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```