---
title: WebMatrix için NuGet 2.6.1 sürüm notları
description: ", Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil, WebMatrix için NuGet 2.6.1 sürüm notları."
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: de568829efd5060f3b02c3129ccfee2b27782821
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780426"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a><span data-ttu-id="513d6-103">WebMatrix için NuGet 2.6.1 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="513d6-103">NuGet 2.6.1 for WebMatrix Release Notes</span></span>

<span data-ttu-id="513d6-104">[NuGet 2,6 sürüm notları](../release-notes/nuget-2.6.md)  |  [NuGet 2,7 sürüm notları](../release-notes/nuget-2.7.md)</span><span class="sxs-lookup"><span data-stu-id="513d6-104">[NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md) | [NuGet 2.7 Release Notes](../release-notes/nuget-2.7.md)</span></span>

<span data-ttu-id="513d6-105">NuGet ekibi, 26 Mart 2014 ' de WebMatrix için güncelleştirilmiş bir NuGet Paket Yöneticisi uzantısı yayımlamıştır.</span><span class="sxs-lookup"><span data-stu-id="513d6-105">The NuGet team released an updated NuGet Package Manager extension for WebMatrix on March 26, 2014.</span></span>  <span data-ttu-id="513d6-106">Bu güncelleştirme, aşağıdaki adımlar kullanılarak [WebMatrix uzantı galerisinden](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) yüklenebilir:</span><span class="sxs-lookup"><span data-stu-id="513d6-106">This update can be installed from the [WebMatrix Extension Gallery](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) using the following steps:</span></span>

1. <span data-ttu-id="513d6-107">WebMatrix 'i aç 3</span><span class="sxs-lookup"><span data-stu-id="513d6-107">Open WebMatrix 3</span></span>
1. <span data-ttu-id="513d6-108">Giriş şeridinde uzantılar simgesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="513d6-108">Click the Extensions icon in the Home ribbon</span></span>
1. <span data-ttu-id="513d6-109">Güncelleştirmeler sekmesini seçin</span><span class="sxs-lookup"><span data-stu-id="513d6-109">Select the Updates tab</span></span>
1. <span data-ttu-id="513d6-110">NuGet paket yöneticisini 2.6.1 olarak güncelleştirmek için tıklayın</span><span class="sxs-lookup"><span data-stu-id="513d6-110">Click to update NuGet Package Manager to 2.6.1</span></span>
1. <span data-ttu-id="513d6-111">WebMatrix 'i kapat ve yeniden Başlat 3</span><span class="sxs-lookup"><span data-stu-id="513d6-111">Close and restart WebMatrix 3</span></span>

## <a name="notable-changes"></a><span data-ttu-id="513d6-112">Önemli değişiklikler</span><span class="sxs-lookup"><span data-stu-id="513d6-112">Notable Changes</span></span>

<span data-ttu-id="513d6-113">Bu uzantı güncelleştirme, kullanıcıların WebMatrix içinde NuGet paketleri tüketen karşılaştığı en büyük sorunlardan ikisi ele alır.</span><span class="sxs-lookup"><span data-stu-id="513d6-113">This extension update addresses two of the biggest issues users have faced consuming NuGet packages within WebMatrix.</span></span>  <span data-ttu-id="513d6-114">Birincisi bir NuGet şema sürümü hatasıdır ve ikincisi, klasördeki sıfır baytlık dll 'Ler için bir hata ile önde gelen bir hatadır `bin` .</span><span class="sxs-lookup"><span data-stu-id="513d6-114">The first was a NuGet schema version error and the second was a bug leading to zero-byte DLLs in the `bin` folder.</span></span>

### <a name="nuget-schema-version-error"></a><span data-ttu-id="513d6-115">NuGet şema sürümü hatası</span><span class="sxs-lookup"><span data-stu-id="513d6-115">NuGet Schema Version Error</span></span>

<span data-ttu-id="513d6-116">WebMatrix 3 yayınlandığından, NuGet paketleri için yeni bir şema sürümü gerektiren NuGet 'e yeni özellikler eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="513d6-116">Since WebMatrix 3 was released, new features have been introduced into NuGet that require a new schema version for the NuGet packages.</span></span>  <span data-ttu-id="513d6-117">Web sitenizde NuGet paketlerinizi yönetmeye çalışırken, bu yeni paketler WebMatrix 'te gördüğünüz hatalara yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="513d6-117">When trying to manage your NuGet packages in your web site, these new packages can lead to errors that you see in WebMatrix.</span></span>

![Bir hata oluşmuştur.](./media/NuGet-2.8/webmatrix-schema-version.png)

<span data-ttu-id="513d6-121">Bu en yeni sürüm en yeni NuGet paketleriyle uyumluluk sağlar ve bu hatanın oluşmasını önler.</span><span class="sxs-lookup"><span data-stu-id="513d6-121">This latest release provides compatibility with the newest NuGet packages, preventing this error from occurring.</span></span> <span data-ttu-id="513d6-122">Microsoft. AspNet. Web sayfaları da dahil olmak üzere paketlerin yeni sürümleri, artık WebMatrix 'e yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="513d6-122">New versions of packages including Microsoft.AspNet.WebPages can now be installed in WebMatrix.</span></span>  <span data-ttu-id="513d6-123">Bu paketlerin bazıları, artık WebMatrix 'te desteklenmeyen [xdt yapılandırma dönüştürmeleri](../release-notes/nuget-2.6.md#xdt)gibi NuGet özelliklerini kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="513d6-123">Some of these packages were using NuGet features such as [XDT config transforms](../release-notes/nuget-2.6.md#xdt), which wasn't supported in WebMatrix until now.</span></span>

### <a name="zero-byte-dlls-in-bin-folder"></a><span data-ttu-id="513d6-124">Bin klasöründe Zero-Byte dll 'Leri</span><span class="sxs-lookup"><span data-stu-id="513d6-124">Zero-Byte DLLs in bin Folder</span></span>

<span data-ttu-id="513d6-125">Bazı kullanıcılar, bin 'e kopyalanan dll 'Leri içeren WebMatrix 'e NuGet paketleri yükledikten sonra, dll 'Lerin `bin` klasörde 0 baytlık dosyalar olarak görünür olduğunu raporladı.</span><span class="sxs-lookup"><span data-stu-id="513d6-125">Some users have reported that after installing NuGet packages in WebMatrix that include DLLs that get copied to bin, that the DLLs show up in the `bin` folder as 0-byte files.</span></span>  <span data-ttu-id="513d6-126">Bu, çalışma zamanında uygulamayı keser.</span><span class="sxs-lookup"><span data-stu-id="513d6-126">This breaks the application at runtime.</span></span>

<span data-ttu-id="513d6-127">[Bu sorun](https://nuget.codeplex.com/workitem/4060) artık düzeltildi.</span><span class="sxs-lookup"><span data-stu-id="513d6-127">[This issue](https://nuget.codeplex.com/workitem/4060) has now been fixed.</span></span>

## <a name="other-recent-improvements"></a><span data-ttu-id="513d6-128">Diğer son geliştirmeler</span><span class="sxs-lookup"><span data-stu-id="513d6-128">Other Recent Improvements</span></span>

<span data-ttu-id="513d6-129">NuGet Paket Yöneticisi 2,8, Visual Studio için yayınlandığında, WebMatrix için NuGet Paket Yöneticisi 2.5.0 de yayımlandık.</span><span class="sxs-lookup"><span data-stu-id="513d6-129">When NuGet Package Manager 2.8 was released for Visual Studio, we also released NuGet Package Manager 2.5.0 for WebMatrix.</span></span>  <span data-ttu-id="513d6-130">Bu, [NuGet 2,8 sürüm notlarında](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates)bahsedilirken, bu güncelleştirmenin tanıtılmasıyla ilgili yeni özelliklerden bahsetmedik.</span><span class="sxs-lookup"><span data-stu-id="513d6-130">While this was mentioned in the [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), we didn't mention the specific new features that update introduced.</span></span>

### <a name="update-all"></a><span data-ttu-id="513d6-131">Tümünü Güncelleştir</span><span class="sxs-lookup"><span data-stu-id="513d6-131">Update All</span></span>

<span data-ttu-id="513d6-132">Artık tüm Web sitenizin paketlerini tek bir adımda güncelleştirebilirsiniz!</span><span class="sxs-lookup"><span data-stu-id="513d6-132">You can now update all of your web site's packages in one step!</span></span>  <span data-ttu-id="513d6-133">NuGet uzantısını WebMatrix 'te açtığınızda, galerideki tüm paketlerin listesini, yüklü olanları ve güncelleştirmeleri kullanılabilir olanları görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="513d6-133">When you open the NuGet extension in WebMatrix, you see the list of all packages on the gallery, those installed, and the ones with updates available.</span></span>  <span data-ttu-id="513d6-134">Daha önce her paketin ayrı ayrı güncelleştirilmesi gerekir, ancak artık Güncelleştirmeler sekmesinde görüntülenen faydalı bir "Tümünü Güncelleştir" düğmesi vardır.</span><span class="sxs-lookup"><span data-stu-id="513d6-134">Previously, every package would have to be updated individually but now there is a useful "Update All" button that shows up on the Updates tab.</span></span>

![Tüm paketleri kullanılabilir güncelleştirmelerle güncelleştirmek için Tümünü Güncelleştir ' e tıklayın](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a><span data-ttu-id="513d6-136">Varolan dosyaların üzerine yaz</span><span class="sxs-lookup"><span data-stu-id="513d6-136">Overwrite Existing Files</span></span>

<span data-ttu-id="513d6-137">Web sitenizde zaten var olan dosyaları içeren paketleri yüklerken, NuGet bu dosyaları her zaman sessizce yok saymıştır (var olan dosyaları tek başına bırakır).</span><span class="sxs-lookup"><span data-stu-id="513d6-137">When installing packages that contain files that already exist in your web site, NuGet has always just silently ignored those files (leaving your existing files alone).</span></span>  <span data-ttu-id="513d6-138">Bu, aslında bir paketin yüklenmiş veya aslında doğru şekilde güncelleştirildiği izlenimi ortaya çıkmasına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="513d6-138">This could lead to the impression that a package was installed or updated correctly when in fact it wasn't.</span></span>  <span data-ttu-id="513d6-139">NuGet artık dosyaların üzerine yazılmasını ister.</span><span class="sxs-lookup"><span data-stu-id="513d6-139">NuGet will now prompt for files to be overwritten.</span></span>

![Dosya çakışması çözümü](./media/NuGet-2.8/webmatrix-overwrite-file.png)
