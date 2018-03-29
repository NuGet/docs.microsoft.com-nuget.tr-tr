---
title: NuGet 2.6.1 WebMatrix sürüm notları | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere WebMatrix için NuGet 2.6.1 için sürüm notları.
keywords: WebMatrix sürüm notları, hata düzeltmeleri ve bilinen sorunlar için NuGet 2.6.1 özellikleri, dcr ekledi
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 505054e42234f313bade496315e94ad485050dbb
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-261-for-webmatrix-release-notes"></a><span data-ttu-id="6242c-104">NuGet 2.6.1 WebMatrix sürüm notları</span><span class="sxs-lookup"><span data-stu-id="6242c-104">NuGet 2.6.1 for WebMatrix Release Notes</span></span>

<span data-ttu-id="6242c-105">[NuGet 2.6 sürüm notları](../release-notes/nuget-2.6.md) | [NuGet 2.7 Sürüm Notları](../release-notes/nuget-2.7.md)</span><span class="sxs-lookup"><span data-stu-id="6242c-105">[NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md) | [NuGet 2.7 Release Notes](../release-notes/nuget-2.7.md)</span></span>

<span data-ttu-id="6242c-106">NuGet takım güncelleştirilmiş bir NuGet Paket Yöneticisi uzantısı WebMatrix için 26 Mart 2014'te yayımladı.</span><span class="sxs-lookup"><span data-stu-id="6242c-106">The NuGet team released an updated NuGet Package Manager extension for WebMatrix on March 26, 2014.</span></span>  <span data-ttu-id="6242c-107">Bu güncelleştirme yüklenebilir [WebMatrix uzantı Galerisi](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) aşağıdaki adımları kullanarak:</span><span class="sxs-lookup"><span data-stu-id="6242c-107">This update can be installed from the [WebMatrix Extension Gallery](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) using the following steps:</span></span>

1. <span data-ttu-id="6242c-108">WebMatrix 3 açın</span><span class="sxs-lookup"><span data-stu-id="6242c-108">Open WebMatrix 3</span></span>
1. <span data-ttu-id="6242c-109">Giriş Şeritte uzantıları simgesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="6242c-109">Click the Extensions icon in the Home ribbon</span></span>
1. <span data-ttu-id="6242c-110">Güncelleştirmeler sekmesini seçin</span><span class="sxs-lookup"><span data-stu-id="6242c-110">Select the Updates tab</span></span>
1. <span data-ttu-id="6242c-111">2.6.1 için NuGet Paket Yöneticisi güncelleştirmek için tıklatın</span><span class="sxs-lookup"><span data-stu-id="6242c-111">Click to update NuGet Package Manager to 2.6.1</span></span>
1. <span data-ttu-id="6242c-112">Kapatın ve WebMatrix 3 başlatın</span><span class="sxs-lookup"><span data-stu-id="6242c-112">Close and restart WebMatrix 3</span></span>

## <a name="notable-changes"></a><span data-ttu-id="6242c-113">Önemli değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="6242c-113">Notable Changes</span></span>

<span data-ttu-id="6242c-114">En büyük sorunları kullanıcıların bu uzantı güncelleştirme adresini iki WebMatrix içindeki Süren NuGet paketleri karşılaştığı.</span><span class="sxs-lookup"><span data-stu-id="6242c-114">This extension update addresses two of the biggest issues users have faced consuming NuGet packages within WebMatrix.</span></span>  <span data-ttu-id="6242c-115">NuGet şeması sürüm hatası ilk ve ikinci sıfır bayt DLL'lerde önde gelen bir hata şeklindeydi `bin` klasör.</span><span class="sxs-lookup"><span data-stu-id="6242c-115">The first was a NuGet schema version error and the second was a bug leading to zero-byte DLLs in the `bin` folder.</span></span>

### <a name="nuget-schema-version-error"></a><span data-ttu-id="6242c-116">NuGet şeması sürüm hatası</span><span class="sxs-lookup"><span data-stu-id="6242c-116">NuGet Schema Version Error</span></span>

<span data-ttu-id="6242c-117">WebMatrix 3 yayımlandıktan yeni özellikler, yeni bir şema sürümüne yönelik NuGet paketlerini gerektiren NuGet içine tanıtılmıştır.</span><span class="sxs-lookup"><span data-stu-id="6242c-117">Since WebMatrix 3 was released, new features have been introduced into NuGet that require a new schema version for the NuGet packages.</span></span>  <span data-ttu-id="6242c-118">Web sitenizde NuGet paketlerinizi yönetmenizi çalışırken bu yeni paketleri Webmatrix'te gördüğünüz hatalara yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="6242c-118">When trying to manage your NuGet packages in your web site, these new packages can lead to errors that you see in WebMatrix.</span></span>

![Bir hata oluşmuştur.](./media/NuGet-2.8/webmatrix-schema-version.png)

<span data-ttu-id="6242c-122">Bu en son sürüm bu hata meydana gelmesini önleme yeni NuGet paketleri ile uyumluluk sağlar.</span><span class="sxs-lookup"><span data-stu-id="6242c-122">This latest release provides compatibility with the newest NuGet packages, preventing this error from occurring.</span></span> <span data-ttu-id="6242c-123">Microsoft.AspNet.WebPages dahil olmak üzere paketleri yeni sürümleri artık Webmatrix'te yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="6242c-123">New versions of packages including Microsoft.AspNet.WebPages can now be installed in WebMatrix.</span></span>  <span data-ttu-id="6242c-124">Bu paketleri bazıları NuGet özellikleri gibi kullandığınız [XDT config dönüştüren](../release-notes/nuget-2.6.md#xdt), şimdiye kadar Webmatrix'te desteklenen değildi.</span><span class="sxs-lookup"><span data-stu-id="6242c-124">Some of these packages were using NuGet features such as [XDT config transforms](../release-notes/nuget-2.6.md#xdt), which wasn't supported in WebMatrix until now.</span></span>

### <a name="zero-byte-dlls-in-bin-folder"></a><span data-ttu-id="6242c-125">Bin klasörü sıfır bayt DLL'leri</span><span class="sxs-lookup"><span data-stu-id="6242c-125">Zero-Byte DLLs in bin Folder</span></span>

<span data-ttu-id="6242c-126">NuGet yükleme eklemek gözü için bu kopyalanan DLL'leri Webmatrix'te DLL'leri Göster içinde paketler sonra bazı kullanıcılar, raporladı `bin` klasörü 0 baytlık dosyaları olarak.</span><span class="sxs-lookup"><span data-stu-id="6242c-126">Some users have reported that after installing NuGet packages in WebMatrix that include DLLs that get copied to bin, that the DLLs show up in the `bin` folder as 0-byte files.</span></span>  <span data-ttu-id="6242c-127">Bu uygulamanın çalışma zamanında keser.</span><span class="sxs-lookup"><span data-stu-id="6242c-127">This breaks the application at runtime.</span></span>

<span data-ttu-id="6242c-128">[Bu sorunu](https://nuget.codeplex.com/workitem/4060) şimdi düzeltilmiştir.</span><span class="sxs-lookup"><span data-stu-id="6242c-128">[This issue](https://nuget.codeplex.com/workitem/4060) has now been fixed.</span></span>

## <a name="other-recent-improvements"></a><span data-ttu-id="6242c-129">Son diğer geliştirmeler</span><span class="sxs-lookup"><span data-stu-id="6242c-129">Other Recent Improvements</span></span>

<span data-ttu-id="6242c-130">Ayrıca, Visual Studio için NuGet Paket Yöneticisi 2.8 yayımlandığında, NuGet Paket Yöneticisi 2.5.0 WebMatrix için yayımladı.</span><span class="sxs-lookup"><span data-stu-id="6242c-130">When NuGet Package Manager 2.8 was released for Visual Studio, we also released NuGet Package Manager 2.5.0 for WebMatrix.</span></span>  <span data-ttu-id="6242c-131">Bu belirtilen sırada [NuGet 2.8 sürüm notları](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), biz belirli yeni özellikleri sunulan bu güncelleştirmeyi Bahsediyor alamadık.</span><span class="sxs-lookup"><span data-stu-id="6242c-131">While this was mentioned in the [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), we didn't mention the specific new features that update introduced.</span></span>

### <a name="update-all"></a><span data-ttu-id="6242c-132">Tümünü Güncelleştir</span><span class="sxs-lookup"><span data-stu-id="6242c-132">Update All</span></span>

<span data-ttu-id="6242c-133">Tüm tek bir adımda, web sitenizin paketlerin şimdi güncelleştirebilirsiniz!</span><span class="sxs-lookup"><span data-stu-id="6242c-133">You can now update all of your web site's packages in one step!</span></span>  <span data-ttu-id="6242c-134">WebMatrix NuGet uzantısı açtığınızda Galerisi, yüklediyseniz ve kullanılabilir güncelleştirmeleri raporlarla tüm paketlerin listesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="6242c-134">When you open the NuGet extension in WebMatrix, you see the list of all packages on the gallery, those installed, and the ones with updates available.</span></span>  <span data-ttu-id="6242c-135">Daha önce her paketi tek tek güncelleştirilmesi gerekiyor ancak şimdi Güncelleştirmeler sekmesinde görüntülenir yararlı bir "Tümünü Güncelleştir" düğmesi yoktur.</span><span class="sxs-lookup"><span data-stu-id="6242c-135">Previously, every package would have to be updated individually but now there is a useful "Update All" button that shows up on the Updates tab.</span></span>

![Tüm kullanılabilir güncelleştirmelerle tüm paketler güncelleştirmek için Güncelleştir'i tıklatın](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a><span data-ttu-id="6242c-137">Var olan dosyaların üzerine yaz</span><span class="sxs-lookup"><span data-stu-id="6242c-137">Overwrite Existing Files</span></span>

<span data-ttu-id="6242c-138">Web sitenizde zaten mevcut dosyaların içeren paketleri yüklerken, NuGet (varolan dosyalarınızı tek başına bırakarak) bu dosyaları her zaman sadece sessizce yoksaydı.</span><span class="sxs-lookup"><span data-stu-id="6242c-138">When installing packages that contain files that already exist in your web site, NuGet has always just silently ignored those files (leaving your existing files alone).</span></span>  <span data-ttu-id="6242c-139">Bu bir paket yüklenir veya doğru olduğunda aslında ancak değildi güncelleştirilmiş izlenim neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="6242c-139">This could lead to the impression that a package was installed or updated correctly when in fact it wasn't.</span></span>  <span data-ttu-id="6242c-140">NuGet şimdi dosyaların üzerine yazılmasına ister.</span><span class="sxs-lookup"><span data-stu-id="6242c-140">NuGet will now prompt for files to be overwritten.</span></span>

![Dosya çakışma çözümü](./media/NuGet-2.8/webmatrix-overwrite-file.png)
