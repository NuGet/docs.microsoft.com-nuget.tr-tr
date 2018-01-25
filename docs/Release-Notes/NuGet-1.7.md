---
title: "NuGet 1.7 Sürüm Notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet bilinen sorunları, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere 1.7 için sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 1.7 Sürüm Notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7b16bea8c6bcc77f814dd32a43b895b5e656c95d
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-17-release-notes"></a><span data-ttu-id="cbaa1-104">NuGet 1,7 Sürüm Notları</span><span class="sxs-lookup"><span data-stu-id="cbaa1-104">NuGet 1.7 Release Notes</span></span>

<span data-ttu-id="cbaa1-105">[NuGet 1.6 sürüm notları](../release-notes/nuget-1.6.md) | [NuGet 1.8 sürüm notları](../release-notes/nuget-1.8.md)</span><span class="sxs-lookup"><span data-stu-id="cbaa1-105">[NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md) | [NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md)</span></span>

<span data-ttu-id="cbaa1-106">NuGet 1.7 4 Nisan 2012'de serbest bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="cbaa1-106">NuGet 1.7 was released on April 4, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="cbaa1-107">Bilinen yükleme sorunu</span><span class="sxs-lookup"><span data-stu-id="cbaa1-107">Known Installation Issue</span></span>
<span data-ttu-id="cbaa1-108">VS 2010 SP1 çalıştırıyorsanız, yüklü eski bir sürüm varsa, NuGet yükseltmeye çalışırken yükleme hatayla karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cbaa1-108">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="cbaa1-109">Yalnızca NuGet kaldırın ve VS uzantısı Galeriden yükleyin için geçici bir çözüm değildir.</span><span class="sxs-lookup"><span data-stu-id="cbaa1-109">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="cbaa1-110">Bkz: [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="cbaa1-110">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="cbaa1-111">Not: Visual Studio (Kaldır düğmesi devre dışıdır) uzantısını Kaldır izin vermiyor olasılıkla "Yönetici olarak çalıştır" kullanarak Visual Studio yeniden başlatmanız gerekir</span><span class="sxs-lookup"><span data-stu-id="cbaa1-111">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="cbaa1-112">Özellikler</span><span class="sxs-lookup"><span data-stu-id="cbaa1-112">Features</span></span>

### <a name="support-opening-readmetxt-file-after-installation"></a><span data-ttu-id="cbaa1-113">Yükleme sonrasında Readme.txt dosyası açılırken desteği</span><span class="sxs-lookup"><span data-stu-id="cbaa1-113">Support opening readme.txt file after installation</span></span>
<span data-ttu-id="cbaa1-114">Paketiniz varsa 1.7, yeni bir `readme.txt` dosyası NuGet paketi kökünde otomatik olarak açılır bu dosya, paket yükleme tamamlandıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="cbaa1-114">New in 1.7, if your package includes a `readme.txt` file at the root of the package, NuGet will automatically open this file after it's finished installing your package.</span></span>

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a><span data-ttu-id="cbaa1-115">Manage NuGet paketlerini iletişim kutusundaki ön sürüm paketlerini Göster</span><span class="sxs-lookup"><span data-stu-id="cbaa1-115">Show prerelease packages in the Manage NuGet packages dialog</span></span>
<span data-ttu-id="cbaa1-116">NuGet paketlerini Yönet iletişim kutusu artık ön sürüm paketlerini göstermek için seçeneği sağlayan bir açılır içerir.</span><span class="sxs-lookup"><span data-stu-id="cbaa1-116">The Manage NuGet Packages dialog now includes a dropdown which provides option to show prerelease packages.</span></span>

![Ön sürüm paketlerini gösterme](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a><span data-ttu-id="cbaa1-118">Paket dosyaları eksik olduğunda paket geri düğmesini göster</span><span class="sxs-lookup"><span data-stu-id="cbaa1-118">Show Package Restore button when package files are missing</span></span>
<span data-ttu-id="cbaa1-119">Paket Yöneticisi Konsolu'nu açın veya iletişim Yöneticisi NuGet paketleri, NuGet geçerli çözümü paket geri yükleme modu etkin olmadığını denetler ve paket dosyaları eksik olması durumunda `packages` klasör.</span><span class="sxs-lookup"><span data-stu-id="cbaa1-119">When you open the Package Manager console or the Manager NuGet packages dialog, NuGet will check if the current solution has enabled the Package Restore mode and if any package files are missing from the `packages` folder.</span></span> <span data-ttu-id="cbaa1-120">Bu iki koşul karşılanıyorsa NuGet size bildirir ve uygun Geri Yükle düğmesi gösterilir.</span><span class="sxs-lookup"><span data-stu-id="cbaa1-120">If these two conditions are met, NuGet will notify you and will show a convenient Restore button.</span></span> <span data-ttu-id="cbaa1-121">Bu düğmeye tıkladığınızda, tüm eksik paketleri geri yüklemek için NuGet tetikler.</span><span class="sxs-lookup"><span data-stu-id="cbaa1-121">Clicking this button will trigger NuGet to restore all the missing packages.</span></span>

![İletişim kutusundaki paket Geri Yükle düğmesi](./media/packagerestore-dialog.png)

![Konsolunda paket Geri Yükle düğmesi](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a><span data-ttu-id="cbaa1-124">Çözüm düzeyi packages.config dosyasına Ekle</span><span class="sxs-lookup"><span data-stu-id="cbaa1-124">Add solution-level packages.config file</span></span>
<span data-ttu-id="cbaa1-125">NuGet önceki sürümlerinde her proje içeren bir `packages.config` bu projede yüklü hangi NuGet paketlerini izler dosya.</span><span class="sxs-lookup"><span data-stu-id="cbaa1-125">In previous versions of NuGet, each project has a `packages.config` file which keeps track of what NuGet packages are installed in that project.</span></span> <span data-ttu-id="cbaa1-126">Ancak, çözüm düzeyi paketleri izlemek için çözüm düzeyinde benzer dosya vardı.</span><span class="sxs-lookup"><span data-stu-id="cbaa1-126">However, there was no similar file at the solution level to keep track of solution-level packages.</span></span> <span data-ttu-id="cbaa1-127">Sonuç olarak, çözümü düzeyi paketlerini geri yüklemek için hiçbir yolu yoktu.</span><span class="sxs-lookup"><span data-stu-id="cbaa1-127">As a result, there was no way to restore solution-level packages.</span></span>
<span data-ttu-id="cbaa1-128">Bu özellik artık NuGet 1.7 uygulanır.</span><span class="sxs-lookup"><span data-stu-id="cbaa1-128">This feature is now implemented in NuGet 1.7.</span></span> <span data-ttu-id="cbaa1-129">Çözüm düzeyi `packages.config` dosya altında yerleştirilir `.nuget` çözüm altında klasör kök ve yalnızca çözüm düzeyi paketleri depolar.</span><span class="sxs-lookup"><span data-stu-id="cbaa1-129">The solution-level `packages.config` file is placed under the `.nuget` folder under solution root and will store only solution-level packages.</span></span>

### <a name="remove-new-package-command"></a><span data-ttu-id="cbaa1-130">Yeni paket komutu kaldırın</span><span class="sxs-lookup"><span data-stu-id="cbaa1-130">Remove New-Package command</span></span>
<span data-ttu-id="cbaa1-131">Düşük kullanım nedeniyle, yeni paketi komutu kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="cbaa1-131">Due to low usage, the New-Package command has been removed.</span></span> <span data-ttu-id="cbaa1-132">Geliştiriciler, nuget.exe ya da kullanışlı NuGet paketi Gezgini'nden paketleri oluşturmak üzere kullanmak için önerilir.</span><span class="sxs-lookup"><span data-stu-id="cbaa1-132">Developers are recommended to use nuget.exe or the handy NuGet Package Explorer to create packages.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="cbaa1-133">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="cbaa1-133">Bug Fixes</span></span>
<span data-ttu-id="cbaa1-134">NuGet 1.7 birçok ağ/kaynak denetimi senaryoları ve paket geri yükleme iş akışını geçici düzeltilen.</span><span class="sxs-lookup"><span data-stu-id="cbaa1-134">NuGet 1.7 has fixed many bugs around the Package Restore workflow and Network/Source Control scenarios.</span></span>

<span data-ttu-id="cbaa1-135">Tam bir listesi için iş öğeleri NuGet 1.7 Lütfen görünüm sabit [NuGet sorun İzleyicisi bu sürüm için](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="cbaa1-135">For a full list of work items fixed in NuGet 1.7, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
