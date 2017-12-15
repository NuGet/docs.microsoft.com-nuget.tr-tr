---
title: "NuGet ekleme BindingRedirect PowerShell başvurusu | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 90f4dcb0-6e5a-4948-8ea9-62e0d061d95a
description: "Visual Studio'da NuGet Paket Yöneticisi konsolunda Ekle BindingRedirect PowerShell komut başvurusu."
keywords: "NuGet Paket Yöneticisi konsolu, NuGet Powershell komutlarını NuGet Powershell başvurusu, Add-BindingRedirect"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7bf8cdb938195f4747932b38ef0d5bb6c34b9137
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="c1117-104">Ekleme BindingRedirect (Visual Studio'da Paket Yöneticisi Konsolu)</span><span class="sxs-lookup"><span data-stu-id="c1117-104">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="c1117-105">*Yalnızca içinde kullanılabilir [NuGet Paket Yöneticisi Konsolu](Package-Manager-Console.md) Windows Visual Studio'da.*</span><span class="sxs-lookup"><span data-stu-id="c1117-105">*Available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="c1117-106">Bir proje için çıkış yolu içindeki tüm derlemelerde arar ve gerektiğinde uygulama veya web yapılandırma dosyasına bağlama yeniden yönlendirmelerini ekler.</span><span class="sxs-lookup"><span data-stu-id="c1117-106">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="c1117-107">Bu komut, bir paket yüklerken otomatik olarak çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="c1117-107">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="c1117-108">Bağlama yeniden yönlendirmeleri ve neden kullanıldıkları hakkında ayrıntılar için bkz: [derleme sürümlerini yönlendirme](https://docs.microsoft.com/dotnet/framework/configure-apps/redirect-assembly-versions) .NET belgelerinde.</span><span class="sxs-lookup"><span data-stu-id="c1117-108">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](https://docs.microsoft.com/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="c1117-109">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="c1117-109">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="c1117-110">Parametreler</span><span class="sxs-lookup"><span data-stu-id="c1117-110">Parameters</span></span>

| <span data-ttu-id="c1117-111">Parametre</span><span class="sxs-lookup"><span data-stu-id="c1117-111">Parameter</span></span> | <span data-ttu-id="c1117-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c1117-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c1117-113">ProjectName</span><span class="sxs-lookup"><span data-stu-id="c1117-113">ProjectName</span></span> | <span data-ttu-id="c1117-114">(Gerekli) Bağlama yeniden yönlendirmeleri eklenecek projesi.</span><span class="sxs-lookup"><span data-stu-id="c1117-114">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="c1117-115">-ProjectName anahtar isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="c1117-115">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="c1117-116">Hiçbiri bu parametre ardışık düzen giriş veya joker karakter kabul edin.</span><span class="sxs-lookup"><span data-stu-id="c1117-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="c1117-117">Ortak parametreleri</span><span class="sxs-lookup"><span data-stu-id="c1117-117">Common Parameters</span></span>

<span data-ttu-id="c1117-118">`Add-BindingRedirect`Aşağıdaki destekleyen [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, ayrıntı, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="c1117-118">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="c1117-119">Örnekler</span><span class="sxs-lookup"><span data-stu-id="c1117-119">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```