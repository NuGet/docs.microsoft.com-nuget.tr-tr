---
title: NuGet ekleme BindingRedirect PowerShell başvurusu | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Visual Studio'da NuGet Paket Yöneticisi konsolunda Ekle BindingRedirect PowerShell komut başvurusu.
keywords: NuGet Paket Yöneticisi konsolu, NuGet Powershell komutlarını NuGet Powershell başvurusu, Add-BindingRedirect
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 2a337bd61295f436b49c56c1680d07ccc6a8c403
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="de9a9-104">Ekleme BindingRedirect (Visual Studio'da Paket Yöneticisi Konsolu)</span><span class="sxs-lookup"><span data-stu-id="de9a9-104">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="de9a9-105">*Yalnızca içinde kullanılabilir [NuGet Paket Yöneticisi Konsolu](package-manager-console.md) Windows Visual Studio'da.*</span><span class="sxs-lookup"><span data-stu-id="de9a9-105">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="de9a9-106">Bir proje için çıkış yolu içindeki tüm derlemelerde arar ve gerektiğinde uygulama veya web yapılandırma dosyasına bağlama yeniden yönlendirmelerini ekler.</span><span class="sxs-lookup"><span data-stu-id="de9a9-106">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="de9a9-107">Bu komut, bir paket yüklerken otomatik olarak çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="de9a9-107">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="de9a9-108">Bağlama yeniden yönlendirmeleri ve neden kullanıldıkları hakkında ayrıntılar için bkz: [derleme sürümlerini yönlendirme](/dotnet/framework/configure-apps/redirect-assembly-versions) .NET belgelerinde.</span><span class="sxs-lookup"><span data-stu-id="de9a9-108">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="de9a9-109">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="de9a9-109">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="de9a9-110">Parametreler</span><span class="sxs-lookup"><span data-stu-id="de9a9-110">Parameters</span></span>

| <span data-ttu-id="de9a9-111">Parametre</span><span class="sxs-lookup"><span data-stu-id="de9a9-111">Parameter</span></span> | <span data-ttu-id="de9a9-112">Açıklama</span><span class="sxs-lookup"><span data-stu-id="de9a9-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="de9a9-113">ProjectName</span><span class="sxs-lookup"><span data-stu-id="de9a9-113">ProjectName</span></span> | <span data-ttu-id="de9a9-114">(Gerekli) Bağlama yeniden yönlendirmeleri eklenecek projesi.</span><span class="sxs-lookup"><span data-stu-id="de9a9-114">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="de9a9-115">-ProjectName anahtar isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="de9a9-115">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="de9a9-116">Hiçbiri bu parametre ardışık düzen giriş veya joker karakter kabul edin.</span><span class="sxs-lookup"><span data-stu-id="de9a9-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="de9a9-117">Ortak parametreleri</span><span class="sxs-lookup"><span data-stu-id="de9a9-117">Common Parameters</span></span>

<span data-ttu-id="de9a9-118">`Add-BindingRedirect` Aşağıdaki destekleyen [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, ayrıntı, WarningAction ve WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="de9a9-118">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="de9a9-119">Örnekler</span><span class="sxs-lookup"><span data-stu-id="de9a9-119">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```