---
title: NuGet 1.7 Sürüm Notları
description: NuGet bilinen sorunları, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr 1.7 için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 07cd541ef215d2a1bacc45995a22dadb6dfeac6d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551473"
---
# <a name="nuget-17-release-notes"></a><span data-ttu-id="482cd-103">NuGet 1.7 Sürüm Notları</span><span class="sxs-lookup"><span data-stu-id="482cd-103">NuGet 1.7 Release Notes</span></span>

<span data-ttu-id="482cd-104">[1.6 NuGet sürüm notları](../release-notes/nuget-1.6.md) | [1.8 NuGet sürüm notları](../release-notes/nuget-1.8.md)</span><span class="sxs-lookup"><span data-stu-id="482cd-104">[NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md) | [NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md)</span></span>

<span data-ttu-id="482cd-105">NuGet 1.7 4 Nisan 2012 tarihinde yayınlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="482cd-105">NuGet 1.7 was released on April 4, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="482cd-106">Bilinen yükleme sorunu</span><span class="sxs-lookup"><span data-stu-id="482cd-106">Known Installation Issue</span></span>
<span data-ttu-id="482cd-107">VS 2010 SP1 çalıştırıyorsanız, yüklü eski bir sürümü varsa, NuGet yükseltmeye çalışırken bir yükleme hata ile karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="482cd-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="482cd-108">Geçici çözüm, yalnızca NuGet kaldırıp VS uzantısı Galeriden yükleyin sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="482cd-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="482cd-109">Bkz: [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="482cd-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="482cd-110">Not: Visual Studio (Kaldır düğmesi devre dışıdır) uzantıyı kaldırmak izin vermiyor olasılıkla "Yönetici olarak çalıştır" kullanarak Visual Studio'yu yeniden başlatmanız gerekir</span><span class="sxs-lookup"><span data-stu-id="482cd-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="482cd-111">Özellikler</span><span class="sxs-lookup"><span data-stu-id="482cd-111">Features</span></span>

### <a name="support-opening-readmetxt-file-after-installation"></a><span data-ttu-id="482cd-112">Yükleme sonrasında Readme.txt dosyasını açma desteği</span><span class="sxs-lookup"><span data-stu-id="482cd-112">Support opening readme.txt file after installation</span></span>
<span data-ttu-id="482cd-113">Paketiniz varsa 1.7, yeni bir `readme.txt` dosyası NuGet paket kökünde otomatik olarak açılır bu dosya, paket yükleme tamamlandıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="482cd-113">New in 1.7, if your package includes a `readme.txt` file at the root of the package, NuGet will automatically open this file after it's finished installing your package.</span></span>

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a><span data-ttu-id="482cd-114">Manage NuGet paketleri iletişim kutusunda yayın öncesi paketleri Göster</span><span class="sxs-lookup"><span data-stu-id="482cd-114">Show prerelease packages in the Manage NuGet packages dialog</span></span>
<span data-ttu-id="482cd-115">NuGet paketlerini Yönet iletişim kutusunda yayın öncesi paketleri göstermek için seçeneği sağlayan bir açılan artık içerir.</span><span class="sxs-lookup"><span data-stu-id="482cd-115">The Manage NuGet Packages dialog now includes a dropdown which provides option to show prerelease packages.</span></span>

![Yayın öncesi paketleri gösteriliyor](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a><span data-ttu-id="482cd-117">Paket dosyaları eksik olduğunda, paket geri düğmesini göster</span><span class="sxs-lookup"><span data-stu-id="482cd-117">Show Package Restore button when package files are missing</span></span>
<span data-ttu-id="482cd-118">Paket Yöneticisi konsolu veya iletişim Yöneticisi NuGet paketleri, NuGet geçerli çözüm paket geri yükleme modu etkin olmadığını denetler ve herhangi bir paket dosyaları eksik olması durumunda `packages` klasör.</span><span class="sxs-lookup"><span data-stu-id="482cd-118">When you open the Package Manager console or the Manager NuGet packages dialog, NuGet will check if the current solution has enabled the Package Restore mode and if any package files are missing from the `packages` folder.</span></span> <span data-ttu-id="482cd-119">Bu iki koşul karşılanıyorsa, NuGet size bildirir ve uygun bir Ekranı Kapla düğmesini gösterir.</span><span class="sxs-lookup"><span data-stu-id="482cd-119">If these two conditions are met, NuGet will notify you and will show a convenient Restore button.</span></span> <span data-ttu-id="482cd-120">Bu düğmeye tıklandığında, tüm eksik paketleri geri yüklemek için NuGet tetikler.</span><span class="sxs-lookup"><span data-stu-id="482cd-120">Clicking this button will trigger NuGet to restore all the missing packages.</span></span>

![İletişim kutusundaki paket Geri Yükle düğmesi](./media/packagerestore-dialog.png)

![Konsolunda paket Geri Yükle düğmesi](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a><span data-ttu-id="482cd-123">Çözüm düzeyinde packages.config dosyası ekleme</span><span class="sxs-lookup"><span data-stu-id="482cd-123">Add solution-level packages.config file</span></span>
<span data-ttu-id="482cd-124">NuGet önceki sürümlerinde, her proje içeren bir `packages.config` dosyasını o proje içinde NuGet paketleri yüklü izler.</span><span class="sxs-lookup"><span data-stu-id="482cd-124">In previous versions of NuGet, each project has a `packages.config` file which keeps track of what NuGet packages are installed in that project.</span></span> <span data-ttu-id="482cd-125">Ancak, çözüm düzeyinde paketlerini izlemek için çözüm düzeyinde benzer dosya vardı.</span><span class="sxs-lookup"><span data-stu-id="482cd-125">However, there was no similar file at the solution level to keep track of solution-level packages.</span></span> <span data-ttu-id="482cd-126">Sonuç olarak, çözüm düzeyinde paketlerini geri yüklemek için hiçbir yolu yoktu.</span><span class="sxs-lookup"><span data-stu-id="482cd-126">As a result, there was no way to restore solution-level packages.</span></span>
<span data-ttu-id="482cd-127">Bu özellik artık NuGet 1.7 içinde uygulanır.</span><span class="sxs-lookup"><span data-stu-id="482cd-127">This feature is now implemented in NuGet 1.7.</span></span> <span data-ttu-id="482cd-128">Çözüm düzeyinde `packages.config` dosya altına yerleştirilir `.nuget` klasörü altında çözüm kök ve yalnızca çözüm düzeyinde paketleri depolar.</span><span class="sxs-lookup"><span data-stu-id="482cd-128">The solution-level `packages.config` file is placed under the `.nuget` folder under solution root and will store only solution-level packages.</span></span>

### <a name="remove-new-package-command"></a><span data-ttu-id="482cd-129">New-Package komutunu Kaldır</span><span class="sxs-lookup"><span data-stu-id="482cd-129">Remove New-Package command</span></span>
<span data-ttu-id="482cd-130">Düşük kullanım nedeniyle, New-Package komutu kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="482cd-130">Due to low usage, the New-Package command has been removed.</span></span> <span data-ttu-id="482cd-131">Geliştiriciler, nuget.exe veya kullanışlı NuGet paket Gezgini, paket oluşturmak üzere kullanmak için önerilir.</span><span class="sxs-lookup"><span data-stu-id="482cd-131">Developers are recommended to use nuget.exe or the handy NuGet Package Explorer to create packages.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="482cd-132">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="482cd-132">Bug Fixes</span></span>
<span data-ttu-id="482cd-133">NuGet 1.7 paket geri yükleme iş akışı ve ağ/kaynak denetimi senaryoları birçok hataları düzeltmiştir.</span><span class="sxs-lookup"><span data-stu-id="482cd-133">NuGet 1.7 has fixed many bugs around the Package Restore workflow and Network/Source Control scenarios.</span></span>

<span data-ttu-id="482cd-134">Tam bir listesi için iş öğeleri NuGet 1.7 Lütfen görünümü sabit [bu sürüm için NuGet sorun İzleyicisi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="482cd-134">For a full list of work items fixed in NuGet 1.7, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
