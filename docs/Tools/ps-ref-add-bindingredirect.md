---
title: "NuGet ekleme BindingRedirect PowerShell başvurusu | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Visual Studio'da NuGet Paket Yöneticisi konsolunda Ekle BindingRedirect PowerShell komut başvurusu."
keywords: "NuGet Paket Yöneticisi konsolu, NuGet Powershell komutlarını NuGet Powershell başvurusu, Add-BindingRedirect"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 41f27d7a1b6b363a562f26590b220d9e11e944f1
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/20/2018
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="0b4cb-104">Ekleme BindingRedirect (Visual Studio'da Paket Yöneticisi Konsolu)</span><span class="sxs-lookup"><span data-stu-id="0b4cb-104">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="0b4cb-105">*Yalnızca içinde kullanılabilir [NuGet Paket Yöneticisi Konsolu](package-manager-console.md) Windows Visual Studio'da.*</span><span class="sxs-lookup"><span data-stu-id="0b4cb-105">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="0b4cb-106">Bir proje için çıkış yolu içindeki tüm derlemelerde arar ve gerektiğinde uygulama veya web yapılandırma dosyasına bağlama yeniden yönlendirmelerini ekler.</span><span class="sxs-lookup"><span data-stu-id="0b4cb-106">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="0b4cb-107">Bu komut, bir paket yüklerken otomatik olarak çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="0b4cb-107">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="0b4cb-108">Bağlama yeniden yönlendirmeleri ve neden kullanıldıkları hakkında ayrıntılar için bkz: [derleme sürümlerini yönlendirme](/dotnet/framework/configure-apps/redirect-assembly-versions) .NET belgelerinde.</span><span class="sxs-lookup"><span data-stu-id="0b4cb-108">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="0b4cb-109">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="0b4cb-109">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="0b4cb-110">Parametreler</span><span class="sxs-lookup"><span data-stu-id="0b4cb-110">Parameters</span></span>

| <span data-ttu-id="0b4cb-111">Parametre</span><span class="sxs-lookup"><span data-stu-id="0b4cb-111">Parameter</span></span> | <span data-ttu-id="0b4cb-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0b4cb-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0b4cb-113">ProjectName</span><span class="sxs-lookup"><span data-stu-id="0b4cb-113">ProjectName</span></span> | <span data-ttu-id="0b4cb-114">(Gerekli) Bağlama yeniden yönlendirmeleri eklenecek projesi.</span><span class="sxs-lookup"><span data-stu-id="0b4cb-114">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="0b4cb-115">-ProjectName anahtar isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="0b4cb-115">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="0b4cb-116">Hiçbiri bu parametre ardışık düzen giriş veya joker karakter kabul edin.</span><span class="sxs-lookup"><span data-stu-id="0b4cb-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="0b4cb-117">Ortak parametreleri</span><span class="sxs-lookup"><span data-stu-id="0b4cb-117">Common Parameters</span></span>

<span data-ttu-id="0b4cb-118">`Add-BindingRedirect` Aşağıdaki destekleyen [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, ayrıntı, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="0b4cb-118">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="0b4cb-119">Örnekler</span><span class="sxs-lookup"><span data-stu-id="0b4cb-119">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```