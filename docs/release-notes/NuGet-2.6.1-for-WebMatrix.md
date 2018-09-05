---
title: WebMatrix sürüm notları için NuGet 2.6.1
description: Bilinen sorunlar, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr WebMatrix için NuGet 2.6.1 için sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 10d80a921cbc34b537f91644da97efc44530fa75
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550323"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a><span data-ttu-id="6784f-103">WebMatrix sürüm notları için NuGet 2.6.1</span><span class="sxs-lookup"><span data-stu-id="6784f-103">NuGet 2.6.1 for WebMatrix Release Notes</span></span>

<span data-ttu-id="6784f-104">[NuGet 2.6 sürüm notları](../release-notes/nuget-2.6.md) | [NuGet 2.7 Sürüm Notları](../release-notes/nuget-2.7.md)</span><span class="sxs-lookup"><span data-stu-id="6784f-104">[NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md) | [NuGet 2.7 Release Notes](../release-notes/nuget-2.7.md)</span></span>

<span data-ttu-id="6784f-105">NuGet takım, 26 Mart 2014'te WebMatrix için güncelleştirilmiş bir NuGet paket yöneticisini uzantısı yayımladı.</span><span class="sxs-lookup"><span data-stu-id="6784f-105">The NuGet team released an updated NuGet Package Manager extension for WebMatrix on March 26, 2014.</span></span>  <span data-ttu-id="6784f-106">Bu güncelleştirme yüklenebilir [WebMatrix uzantı Galerisi](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) aşağıdaki adımları kullanarak:</span><span class="sxs-lookup"><span data-stu-id="6784f-106">This update can be installed from the [WebMatrix Extension Gallery](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) using the following steps:</span></span>

1. <span data-ttu-id="6784f-107">WebMatrix 3'ı açın</span><span class="sxs-lookup"><span data-stu-id="6784f-107">Open WebMatrix 3</span></span>
1. <span data-ttu-id="6784f-108">Giriş şeridinde uzantıları simgesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="6784f-108">Click the Extensions icon in the Home ribbon</span></span>
1. <span data-ttu-id="6784f-109">Güncelleştirmeler sekmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="6784f-109">Select the Updates tab</span></span>
1. <span data-ttu-id="6784f-110">2.6.1 için NuGet Paket Yöneticisi güncelleştirmek için tıklayın</span><span class="sxs-lookup"><span data-stu-id="6784f-110">Click to update NuGet Package Manager to 2.6.1</span></span>
1. <span data-ttu-id="6784f-111">WebMatrix 3'ü yeniden başlatın ve kapatın</span><span class="sxs-lookup"><span data-stu-id="6784f-111">Close and restart WebMatrix 3</span></span>

## <a name="notable-changes"></a><span data-ttu-id="6784f-112">Önemli değişiklikler</span><span class="sxs-lookup"><span data-stu-id="6784f-112">Notable Changes</span></span>

<span data-ttu-id="6784f-113">Bu uzantı güncelleştirme adreslerini iki büyük sorunları kullanıcılar webmatrix'de alıcı NuGet paketlerini karşılaştığı.</span><span class="sxs-lookup"><span data-stu-id="6784f-113">This extension update addresses two of the biggest issues users have faced consuming NuGet packages within WebMatrix.</span></span>  <span data-ttu-id="6784f-114">İlk NuGet şema sürümü hatası ve ikinci sıfır bayt DLL'ler için önde gelen bir hatayı şeklindeydi `bin` klasör.</span><span class="sxs-lookup"><span data-stu-id="6784f-114">The first was a NuGet schema version error and the second was a bug leading to zero-byte DLLs in the `bin` folder.</span></span>

### <a name="nuget-schema-version-error"></a><span data-ttu-id="6784f-115">NuGet şema sürümü hatası</span><span class="sxs-lookup"><span data-stu-id="6784f-115">NuGet Schema Version Error</span></span>

<span data-ttu-id="6784f-116">WebMatrix 3'ü yayınlandıktan sonra yeni bir şema sürümüne yönelik NuGet paketlerini gerektiren NuGet içine yeni özellikler tanıtılmıştır.</span><span class="sxs-lookup"><span data-stu-id="6784f-116">Since WebMatrix 3 was released, new features have been introduced into NuGet that require a new schema version for the NuGet packages.</span></span>  <span data-ttu-id="6784f-117">NuGet paketlerinizi web sitenizi yönetmek çalışırken, bu yeni paketler Webmatrix'te gördüğünüz hatalara yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="6784f-117">When trying to manage your NuGet packages in your web site, these new packages can lead to errors that you see in WebMatrix.</span></span>

![Bir hata oluşmuştur.](./media/NuGet-2.8/webmatrix-schema-version.png)

<span data-ttu-id="6784f-121">Bu en son sürüm, bu hata oluşmasını engelliyor en yeni NuGet paketleri ile uyumluluk sağlar.</span><span class="sxs-lookup"><span data-stu-id="6784f-121">This latest release provides compatibility with the newest NuGet packages, preventing this error from occurring.</span></span> <span data-ttu-id="6784f-122">Microsoft.AspNet.WebPages dahil olmak üzere paketlerin yeni sürümlerini Webmatrix'te artık yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="6784f-122">New versions of packages including Microsoft.AspNet.WebPages can now be installed in WebMatrix.</span></span>  <span data-ttu-id="6784f-123">Bu paketler bazıları NuGet özellikleri gibi kullandığınız [XDT yapılandırma dönüşümleri](../release-notes/nuget-2.6.md#xdt), şimdiye kadar Webmatrix'te desteklenen değildi.</span><span class="sxs-lookup"><span data-stu-id="6784f-123">Some of these packages were using NuGet features such as [XDT config transforms](../release-notes/nuget-2.6.md#xdt), which wasn't supported in WebMatrix until now.</span></span>

### <a name="zero-byte-dlls-in-bin-folder"></a><span data-ttu-id="6784f-124">Bin klasörü sıfır bayt DLL'leri</span><span class="sxs-lookup"><span data-stu-id="6784f-124">Zero-Byte DLLs in bin Folder</span></span>

<span data-ttu-id="6784f-125">NuGet yükleme depo, kopyalanmasını DLL'leri içermektedir Webmatrix'te DLL'leri Göster, paketleri sonra bazı kullanıcılar, bildirdiniz `bin` 0 bayt dosyalarıyla klasörde.</span><span class="sxs-lookup"><span data-stu-id="6784f-125">Some users have reported that after installing NuGet packages in WebMatrix that include DLLs that get copied to bin, that the DLLs show up in the `bin` folder as 0-byte files.</span></span>  <span data-ttu-id="6784f-126">Bu uygulama çalışma zamanında keser.</span><span class="sxs-lookup"><span data-stu-id="6784f-126">This breaks the application at runtime.</span></span>

<span data-ttu-id="6784f-127">[Bu sorunu](https://nuget.codeplex.com/workitem/4060) artık düzeltildi.</span><span class="sxs-lookup"><span data-stu-id="6784f-127">[This issue](https://nuget.codeplex.com/workitem/4060) has now been fixed.</span></span>

## <a name="other-recent-improvements"></a><span data-ttu-id="6784f-128">Son diğer iyileştirmeler</span><span class="sxs-lookup"><span data-stu-id="6784f-128">Other Recent Improvements</span></span>

<span data-ttu-id="6784f-129">Visual Studio için NuGet Paket Yöneticisi 2.8 yayımlandığında, WebMatrix için NuGet Paket Yöneticisi 2.5.0 de yayımlandı.</span><span class="sxs-lookup"><span data-stu-id="6784f-129">When NuGet Package Manager 2.8 was released for Visual Studio, we also released NuGet Package Manager 2.5.0 for WebMatrix.</span></span>  <span data-ttu-id="6784f-130">Bu içinde bahsedilen sırada [NuGet 2.8 sürüm notları](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), şu yeni özellikleri kullanıma sunulan bu güncelleştirmeyi belirli bahsetmek kaydetmedi.</span><span class="sxs-lookup"><span data-stu-id="6784f-130">While this was mentioned in the [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), we didn't mention the specific new features that update introduced.</span></span>

### <a name="update-all"></a><span data-ttu-id="6784f-131">Tümünü Güncelleştir</span><span class="sxs-lookup"><span data-stu-id="6784f-131">Update All</span></span>

<span data-ttu-id="6784f-132">Ayrıca, tüm web sitenizin paketleri tek bir adımda şimdi güncelleştirebilirsiniz!</span><span class="sxs-lookup"><span data-stu-id="6784f-132">You can now update all of your web site's packages in one step!</span></span>  <span data-ttu-id="6784f-133">Webmatrix'te NuGet uzantısı açtığınızda, Galeri, yüklenenler ve güncelleştirmeleri kullanılabilir olanlarla tüm paketlerin listesi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="6784f-133">When you open the NuGet extension in WebMatrix, you see the list of all packages on the gallery, those installed, and the ones with updates available.</span></span>  <span data-ttu-id="6784f-134">Daha önce her paket, ayrı ayrı olarak güncelleştirilmesi gerekir, ancak artık Güncelleştirmeler sekmesinde gösterilir kullanışlı bir "Tümünü Güncelleştir" düğmesi yoktur.</span><span class="sxs-lookup"><span data-stu-id="6784f-134">Previously, every package would have to be updated individually but now there is a useful "Update All" button that shows up on the Updates tab.</span></span>

![Tüm kullanılabilir güncelleştirmeleri tüm paketleri güncelleştirmek için Güncelleştir'e tıklayın](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a><span data-ttu-id="6784f-136">Varolan dosyaların üzerine yaz</span><span class="sxs-lookup"><span data-stu-id="6784f-136">Overwrite Existing Files</span></span>

<span data-ttu-id="6784f-137">Web sitenizdeki mevcut dosyaları içeren paketleri yüklerken, NuGet (varolan dosyalarınızı tek başına bırakarak) bu dosyaları her zaman sadece sessizce yoksaydı.</span><span class="sxs-lookup"><span data-stu-id="6784f-137">When installing packages that contain files that already exist in your web site, NuGet has always just silently ignored those files (leaving your existing files alone).</span></span>  <span data-ttu-id="6784f-138">Bu, bir paket yüklenip yüklenmediğini veya doğru aslında bölümdü güncelleştirilmiş izlenim neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="6784f-138">This could lead to the impression that a package was installed or updated correctly when in fact it wasn't.</span></span>  <span data-ttu-id="6784f-139">NuGet artık dosyaların üzerine için ister.</span><span class="sxs-lookup"><span data-stu-id="6784f-139">NuGet will now prompt for files to be overwritten.</span></span>

![Dosya çakışması çözümleme](./media/NuGet-2.8/webmatrix-overwrite-file.png)
