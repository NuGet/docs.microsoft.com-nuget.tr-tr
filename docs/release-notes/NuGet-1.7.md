---
title: NuGet 1,7 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 1,7 sürüm notları.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 50eb326c5ada4f74685b07c0d1b0f84b14e547ac
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777073"
---
# <a name="nuget-17-release-notes"></a><span data-ttu-id="838c0-103">NuGet 1,7 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="838c0-103">NuGet 1.7 Release Notes</span></span>

<span data-ttu-id="838c0-104">[NuGet 1,6 sürüm notları](../release-notes/nuget-1.6.md)  |  [NuGet 1,8 sürüm notları](../release-notes/nuget-1.8.md)</span><span class="sxs-lookup"><span data-stu-id="838c0-104">[NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md) | [NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md)</span></span>

<span data-ttu-id="838c0-105">NuGet 1,7, 4 Nisan 2012 ' de yayımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="838c0-105">NuGet 1.7 was released on April 4, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="838c0-106">Bilinen yükleme sorunu</span><span class="sxs-lookup"><span data-stu-id="838c0-106">Known Installation Issue</span></span>
<span data-ttu-id="838c0-107">VS 2010 SP1 çalıştırıyorsanız, daha eski bir sürümü yüklüyse NuGet 'i yükseltmeye çalışırken yükleme hatası ile karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="838c0-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="838c0-108">Geçici çözüm, NuGet 'i kaldırmak ve ardından VS uzantısı galerisinden yüklemek olacaktır.</span><span class="sxs-lookup"><span data-stu-id="838c0-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="838c0-109">Daha fazla bilgi edinmek için bkz. <https://support.microsoft.com/kb/2581019>.</span><span class="sxs-lookup"><span data-stu-id="838c0-109">See <https://support.microsoft.com/kb/2581019> for more information.</span></span>

<span data-ttu-id="838c0-110">Note: Visual Studio uzantıyı kaldırmanızı izin vermediğinden (kaldırma düğmesi devre dışıdır), büyük olasılıkla "yönetici olarak çalıştır" seçeneğini kullanarak Visual Studio 'Yu yeniden başlatmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="838c0-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="838c0-111">Özellikler</span><span class="sxs-lookup"><span data-stu-id="838c0-111">Features</span></span>

### <a name="support-opening-readmetxt-file-after-installation"></a><span data-ttu-id="838c0-112">Yüklemeden sonra readme.txt dosyası açmayı destekleme</span><span class="sxs-lookup"><span data-stu-id="838c0-112">Support opening readme.txt file after installation</span></span>
<span data-ttu-id="838c0-113">1,7 ' de yeni, paketiniz `readme.txt` paketin kökünde bir dosya içeriyorsa, bu dosya paketinizi yükleme bittikten sonra otomatik olarak bu dosyayı açar.</span><span class="sxs-lookup"><span data-stu-id="838c0-113">New in 1.7, if your package includes a `readme.txt` file at the root of the package, NuGet will automatically open this file after it's finished installing your package.</span></span>

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a><span data-ttu-id="838c0-114">NuGet Paketlerini Yönet iletişim kutusunda yayın öncesi paketleri göster</span><span class="sxs-lookup"><span data-stu-id="838c0-114">Show prerelease packages in the Manage NuGet packages dialog</span></span>
<span data-ttu-id="838c0-115">NuGet Paketlerini Yönet iletişim kutusu artık, ön sürüm paketlerini gösterme seçeneği sağlayan bir açılan menü içerir.</span><span class="sxs-lookup"><span data-stu-id="838c0-115">The Manage NuGet Packages dialog now includes a dropdown which provides option to show prerelease packages.</span></span>

![Ön sürüm paketleri gösteriliyor](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a><span data-ttu-id="838c0-117">Paket dosyaları eksik olduğunda paket geri yükleme düğmesini göster</span><span class="sxs-lookup"><span data-stu-id="838c0-117">Show Package Restore button when package files are missing</span></span>
<span data-ttu-id="838c0-118">Paket Yöneticisi konsolunu veya yönetici NuGet paketleri iletişim kutusunu açtığınızda, NuGet geçerli çözümün paket geri yükleme modunu etkinleştirmiştir ve klasörde herhangi bir paket dosyası eksikse, bu çözüm denetlenir `packages` .</span><span class="sxs-lookup"><span data-stu-id="838c0-118">When you open the Package Manager console or the Manager NuGet packages dialog, NuGet will check if the current solution has enabled the Package Restore mode and if any package files are missing from the `packages` folder.</span></span> <span data-ttu-id="838c0-119">Bu iki koşul karşılanıyorsa, NuGet size bildirimde bulunur ve uygun bir geri yükleme düğmesi gösterir.</span><span class="sxs-lookup"><span data-stu-id="838c0-119">If these two conditions are met, NuGet will notify you and will show a convenient Restore button.</span></span> <span data-ttu-id="838c0-120">Bu düğmeye tıkladığınızda, tüm eksik paketleri geri yüklemek için NuGet tetiklenecek.</span><span class="sxs-lookup"><span data-stu-id="838c0-120">Clicking this button will trigger NuGet to restore all the missing packages.</span></span>

![İletişim kutusunda paket geri yükleme düğmesi](./media/packagerestore-dialog.png)

![Konsolda paket geri yükleme düğmesi](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a><span data-ttu-id="838c0-123">Çözüm düzeyi packages.config dosyası Ekle</span><span class="sxs-lookup"><span data-stu-id="838c0-123">Add solution-level packages.config file</span></span>
<span data-ttu-id="838c0-124">NuGet 'in önceki sürümlerinde her proje, `packages.config` Bu projeye hangi NuGet paketlerinin yüklendiğini izleyen bir dosya içerir.</span><span class="sxs-lookup"><span data-stu-id="838c0-124">In previous versions of NuGet, each project has a `packages.config` file which keeps track of what NuGet packages are installed in that project.</span></span> <span data-ttu-id="838c0-125">Ancak çözüm düzeyinde çözüm düzeyinde paketleri izlemek için benzer bir dosya yoktu.</span><span class="sxs-lookup"><span data-stu-id="838c0-125">However, there was no similar file at the solution level to keep track of solution-level packages.</span></span> <span data-ttu-id="838c0-126">Sonuç olarak, çözüm düzeyi paketleri geri yüklemenin bir yolu yoktu.</span><span class="sxs-lookup"><span data-stu-id="838c0-126">As a result, there was no way to restore solution-level packages.</span></span>
<span data-ttu-id="838c0-127">Bu özellik artık NuGet 1,7 ' de uygulanır.</span><span class="sxs-lookup"><span data-stu-id="838c0-127">This feature is now implemented in NuGet 1.7.</span></span> <span data-ttu-id="838c0-128">Çözüm düzeyi dosya, `packages.config` `.nuget` çözüm kökü altındaki klasörün altına yerleştirilir ve yalnızca çözüm düzeyi paketleri depolar.</span><span class="sxs-lookup"><span data-stu-id="838c0-128">The solution-level `packages.config` file is placed under the `.nuget` folder under solution root and will store only solution-level packages.</span></span>

### <a name="remove-new-package-command"></a><span data-ttu-id="838c0-129">New-Package komutu kaldır</span><span class="sxs-lookup"><span data-stu-id="838c0-129">Remove New-Package command</span></span>
<span data-ttu-id="838c0-130">Düşük kullanım nedeniyle New-Package komutu kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="838c0-130">Due to low usage, the New-Package command has been removed.</span></span> <span data-ttu-id="838c0-131">Geliştiricilerin, paketler oluşturmak için nuget.exe veya yararlı NuGet paket Gezginini kullanması önerilir.</span><span class="sxs-lookup"><span data-stu-id="838c0-131">Developers are recommended to use nuget.exe or the handy NuGet Package Explorer to create packages.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="838c0-132">Hata Düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="838c0-132">Bug Fixes</span></span>
<span data-ttu-id="838c0-133">NuGet 1,7, paket geri yükleme iş akışı ve ağ/kaynak denetimi senaryolarında birçok hatayı düzeltti.</span><span class="sxs-lookup"><span data-stu-id="838c0-133">NuGet 1.7 has fixed many bugs around the Package Restore workflow and Network/Source Control scenarios.</span></span>

<span data-ttu-id="838c0-134">NuGet 1,7 ' de düzeltilen iş öğelerinin tam listesi için lütfen [Bu sürüm Için NuGet sorun İzleyicisi](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)' ni görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="838c0-134">For a full list of work items fixed in NuGet 1.7, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
