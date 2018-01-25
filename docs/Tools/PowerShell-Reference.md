---
title: "NuGet PowerShell başvurusu | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/02/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Visual Studio'da NuGet Paket Yöneticisi konsolunda kullanılabilir PowerShell komutlarını tam referansı."
keywords: "NuGet Paket Yöneticisi konsolu, NuGet Powershell komutlarını NuGet Powershell başvurusu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0cbd9b13b34bd93fea6c6684c03bca9cff5d9e5e
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2018
---
# <a name="powershell-reference"></a><span data-ttu-id="c8d9b-104">PowerShell başvurusu</span><span class="sxs-lookup"><span data-stu-id="c8d9b-104">PowerShell reference</span></span>

<span data-ttu-id="c8d9b-105">Paket Yöneticisi konsolu, bir PowerShell arabirimi belirli komutları NuGet ile etkileşim kurmak için Windows Visual Studio'dan aşağıda listelenen sağlar.</span><span class="sxs-lookup"><span data-stu-id="c8d9b-105">The Package Manager Console provides a PowerShell interface within Visual Studio on Windows to interact with NuGet through the specific commands listed below.</span></span> <span data-ttu-id="c8d9b-106">(Konsol Mac için Visual Studio şu anda kullanılabilir değil) Konsolunu kullanarak için bir kılavuz için bkz: [Paket Yöneticisi Konsolu](../tools/package-manager-console.md) konu.</span><span class="sxs-lookup"><span data-stu-id="c8d9b-106">(The console is not presently available in Visual Studio for Mac.) For a guide to using the console, see the [Package Manager Console](../tools/package-manager-console.md) topic.</span></span>

> [!Tip]
> <span data-ttu-id="c8d9b-107">Tüm PowerShell komutları yalnızca paket tüketimi ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="c8d9b-107">All PowerShell commands relate only to package consumption.</span></span> <span data-ttu-id="c8d9b-108">PowerShell komutlarını oluşturmak ve bir paket ayrıca diğer paketleri tüketicisi olarak toplasa bile dışında paketleri yayımlamak için ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="c8d9b-108">No PowerShell commands relate to creating and publishing packages except to the extent that a package can also be a consumer of other packages.</span></span>

> [!Important]
> <span data-ttu-id="c8d9b-109">Burada listelenen komutlar Visual Studio'da Paket Yöneticisi konsolu özgüdür ve farklı [paket Yönetimi Modülü komutları](/powershell/module/packagemanagement/?view=powershell-6) genel bir PowerShell ortamında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c8d9b-109">The commands listed here are specific to the Package Manager Console in Visual Studio, and differ from the [Package Management module commands](/powershell/module/packagemanagement/?view=powershell-6) that are available in a general PowerShell environment.</span></span> <span data-ttu-id="c8d9b-110">Özellikle, her bir ortamda, diğer kullanılabilir olmayan komutlar sahip ve aynı ada sahip komutları kendi belirli değişkenlerinde farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="c8d9b-110">Specifically, each environment has commands that are not available in the other, and commands with the same name may also differ in their specific arguments.</span></span> <span data-ttu-id="c8d9b-111">Visual Studio'da paket Yönetimi konsolunu kullanarak, komutları ve mevcut bu konudaki belgelenen bağımsız değişkenleri uygulanır.</span><span class="sxs-lookup"><span data-stu-id="c8d9b-111">When using the Package Management Console in Visual Studio, the commands and arguments documented in this present topic apply.</span></span>

| <span data-ttu-id="c8d9b-112">Sık kullanılan komutlar</span><span class="sxs-lookup"><span data-stu-id="c8d9b-112">Common Commands</span></span> | <span data-ttu-id="c8d9b-113">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8d9b-113">Description</span></span> | <span data-ttu-id="c8d9b-114">NuGet sürümü</span><span class="sxs-lookup"><span data-stu-id="c8d9b-114">NuGet Version</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="c8d9b-115">Install-Package</span><span class="sxs-lookup"><span data-stu-id="c8d9b-115">Install-Package</span></span>](ps-ref-install-package.md) | <span data-ttu-id="c8d9b-116">Bir paketi ve bağımlılıklarını projeye yükler.</span><span class="sxs-lookup"><span data-stu-id="c8d9b-116">Installs a package and its dependencies into the project.</span></span> | <span data-ttu-id="c8d9b-117">Tümü</span><span class="sxs-lookup"><span data-stu-id="c8d9b-117">All</span></span> |
| [<span data-ttu-id="c8d9b-118">Update-Package</span><span class="sxs-lookup"><span data-stu-id="c8d9b-118">Update-Package</span></span>](ps-ref-update-package.md) | <span data-ttu-id="c8d9b-119">Bir paketi ve bağımlılıklarını veya projesindeki tüm paketleri güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="c8d9b-119">Updates a package and its dependencies, or all packages in a project.</span></span> | <span data-ttu-id="c8d9b-120">Tümü</span><span class="sxs-lookup"><span data-stu-id="c8d9b-120">All</span></span> |
| [<span data-ttu-id="c8d9b-121">Find-Package</span><span class="sxs-lookup"><span data-stu-id="c8d9b-121">Find-Package</span></span>](ps-ref-find-package.md) | <span data-ttu-id="c8d9b-122">Bir paket kimliği veya anahtar sözcükleri kullanarak paket kaynağını arar.</span><span class="sxs-lookup"><span data-stu-id="c8d9b-122">Searches a package source using a package ID or keywords.</span></span> | <span data-ttu-id="c8d9b-123">3.0+</span><span class="sxs-lookup"><span data-stu-id="c8d9b-123">3.0+</span></span> |
| [<span data-ttu-id="c8d9b-124">Get-Package</span><span class="sxs-lookup"><span data-stu-id="c8d9b-124">Get-Package</span></span>](ps-ref-get-package.md) | <span data-ttu-id="c8d9b-125">Yerel depoda yüklü olan paketlerin listesini alır veya paket kaynağındaki paketleri listeler.</span><span class="sxs-lookup"><span data-stu-id="c8d9b-125">Retrieves the list of packages installed in the local repository, or lists packages available from a package source.</span></span> | <span data-ttu-id="c8d9b-126">Tümü</span><span class="sxs-lookup"><span data-stu-id="c8d9b-126">All</span></span> |

| <span data-ttu-id="c8d9b-127">İkincil komutları</span><span class="sxs-lookup"><span data-stu-id="c8d9b-127">Secondary Commands</span></span> | <span data-ttu-id="c8d9b-128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8d9b-128">Description</span></span> | <span data-ttu-id="c8d9b-129">NuGet sürümü</span><span class="sxs-lookup"><span data-stu-id="c8d9b-129">NuGet Version</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="c8d9b-130">Add-BindingRedirect</span><span class="sxs-lookup"><span data-stu-id="c8d9b-130">Add-BindingRedirect</span></span>](ps-ref-add-bindingredirect.md) | <span data-ttu-id="c8d9b-131">Bir proje için çıkış yolu içindeki tüm derlemelerde inceler ve bağlama yeniden yönlendirmelerini ekler `app.config` veya `web.config` gerektiğinde.</span><span class="sxs-lookup"><span data-stu-id="c8d9b-131">Examines all assemblies within the output path for a project and adds binding redirects to the `app.config` or `web.config` where necessary.</span></span> | <span data-ttu-id="c8d9b-132">Tümü</span><span class="sxs-lookup"><span data-stu-id="c8d9b-132">All</span></span> |
| [<span data-ttu-id="c8d9b-133">Get-Project</span><span class="sxs-lookup"><span data-stu-id="c8d9b-133">Get-Project</span></span>](ps-ref-get-project.md) | <span data-ttu-id="c8d9b-134">Varsayılan ya da belirtilen proje hakkındaki bilgileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="c8d9b-134">Displays information about the default or specified project.</span></span> | <span data-ttu-id="c8d9b-135">3.0+</span><span class="sxs-lookup"><span data-stu-id="c8d9b-135">3.0+</span></span> |
| [<span data-ttu-id="c8d9b-136">Open-PackagePage</span><span class="sxs-lookup"><span data-stu-id="c8d9b-136">Open-PackagePage</span></span>](ps-ref-open-packagepage.md) | <span data-ttu-id="c8d9b-137">Proje, lisans veya belirtilen paket için rapor kötüye URL'si ile varsayılan tarayıcı başlatır.</span><span class="sxs-lookup"><span data-stu-id="c8d9b-137">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span> | <span data-ttu-id="c8d9b-138">3.0 +'da kullanım dışıdır</span><span class="sxs-lookup"><span data-stu-id="c8d9b-138">Deprecated in 3.0+</span></span> |
| [<span data-ttu-id="c8d9b-139">Register-TabExpansion</span><span class="sxs-lookup"><span data-stu-id="c8d9b-139">Register-TabExpansion</span></span>](ps-ref-register-tabexpansion.md) | <span data-ttu-id="c8d9b-140">Bir sekme genişlemesi parametreler için yaygın olarak kullanılan parametre değerleri için özelleştirilmiş genişletmeleri oluşturmanızı sağlayan bir komut kaydeder.</span><span class="sxs-lookup"><span data-stu-id="c8d9b-140">Registers a tab expansion for the parameters of a command, allowing you to create customized expansions for commonly-used parameter values.</span></span> | <span data-ttu-id="c8d9b-141">Tümü</span><span class="sxs-lookup"><span data-stu-id="c8d9b-141">All</span></span> |
| [<span data-ttu-id="c8d9b-142">Sync-Package</span><span class="sxs-lookup"><span data-stu-id="c8d9b-142">Sync-Package</span></span>](ps-ref-sync-package.md) | <span data-ttu-id="c8d9b-143">Get paketinden yüklü sürümü proje belirtilen ve sürümü çözümdeki projelerin geri kalanına eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="c8d9b-143">Get the version of installed package from specified project and syncs the version to the rest of projects in the solution.</span></span> | <span data-ttu-id="c8d9b-144">3.0+</span><span class="sxs-lookup"><span data-stu-id="c8d9b-144">3.0+</span></span> |
| [<span data-ttu-id="c8d9b-145">Uninstall-Package</span><span class="sxs-lookup"><span data-stu-id="c8d9b-145">Uninstall-Package</span></span>](ps-ref-uninstall-package.md) | <span data-ttu-id="c8d9b-146">Bir paket bağımlılıklarını isteğe bağlı olarak kaldırarak bir projeden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="c8d9b-146">Removes a package from a project, optionally removing its dependencies.</span></span> | <span data-ttu-id="c8d9b-147">Tümü</span><span class="sxs-lookup"><span data-stu-id="c8d9b-147">All</span></span> |

<span data-ttu-id="c8d9b-148">Konsolu içinden aşağıdaki komutlardan birini ilgili eksiksiz, ayrıntılı yardım için yalnızca söz konusu komut adı ile aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c8d9b-148">For complete, detailed help on any of these commands within the console, just run the following with the command name in question:</span></span>

```ps
Get-Help <command> -full
```

<span data-ttu-id="c8d9b-149">Tüm Paket Yöneticisi Konsolu komutları aşağıdaki desteği [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216):</span><span class="sxs-lookup"><span data-stu-id="c8d9b-149">All Package Manager Console commands support the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216):</span></span>

- <span data-ttu-id="c8d9b-150">Hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="c8d9b-150">Debug</span></span>
- <span data-ttu-id="c8d9b-151">ErrorAction</span><span class="sxs-lookup"><span data-stu-id="c8d9b-151">ErrorAction</span></span>
- <span data-ttu-id="c8d9b-152">ErrorVariable</span><span class="sxs-lookup"><span data-stu-id="c8d9b-152">ErrorVariable</span></span>
- <span data-ttu-id="c8d9b-153">OutBuffer</span><span class="sxs-lookup"><span data-stu-id="c8d9b-153">OutBuffer</span></span>
- <span data-ttu-id="c8d9b-154">OutVariable</span><span class="sxs-lookup"><span data-stu-id="c8d9b-154">OutVariable</span></span>
- <span data-ttu-id="c8d9b-155">PipelineVariable</span><span class="sxs-lookup"><span data-stu-id="c8d9b-155">PipelineVariable</span></span>
- <span data-ttu-id="c8d9b-156">Ayrıntılı</span><span class="sxs-lookup"><span data-stu-id="c8d9b-156">Verbose</span></span>
- <span data-ttu-id="c8d9b-157">WarningAction</span><span class="sxs-lookup"><span data-stu-id="c8d9b-157">WarningAction</span></span>
- <span data-ttu-id="c8d9b-158">WarningVariable</span><span class="sxs-lookup"><span data-stu-id="c8d9b-158">WarningVariable</span></span>

<span data-ttu-id="c8d9b-159">Ayrıntılar için başvurmak [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) PowerShell belgelerinde.</span><span class="sxs-lookup"><span data-stu-id="c8d9b-159">For details, refer to [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) in the PowerShell documentation.</span></span>
