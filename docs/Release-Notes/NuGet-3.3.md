---
title: "NuGet 3.3 sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 4110a36a-cffe-4038-8da4-e841bce6e94b
description: "NuGet bilinen sorunları, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere 3.3 için sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 3.3 sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f35f7621db324957b0af8329cf9faa11493835e2
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="b518d-104">NuGet 3.3 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="b518d-104">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="b518d-105">[NuGet 3.2.1 sürüm notları](../release-notes/nuget-3.2.1.md) | [NuGet 3.4 RC sürüm notları](../release-notes/nuget-3.4-RC.md)</span><span class="sxs-lookup"><span data-stu-id="b518d-105">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="b518d-106">NuGet 3.3 30 Kasım 2015 çok sayıda kullanışlı düzeltmeleri NuGet istemcilere koleksiyonu yanı sıra kullanıcı arabirimi güncelleştirmeleri ve komut satırı özellikleri ile serbest bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="b518d-106">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="b518d-107">Yeni Özellikler</span><span class="sxs-lookup"><span data-stu-id="b518d-107">New Features</span></span>

* <span data-ttu-id="b518d-108">Kimlik bilgisi sağlayıcıları sorunsuz bir şekilde kimliği doğrulanmış bir akış ile çalışabilmek için NuGet komut satırı istemcilerin sağlayan tanıtılmıştır.</span><span class="sxs-lookup"><span data-stu-id="b518d-108">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="b518d-109">[Visual Studio Team Services yükleme konusunda yönergeler kimlik bilgisi sağlayıcısı ](../API/nuget-exe-Credential-Providers.md) ve NuGet yapılandırma kullanmak için istemciler üzerinde NuGet belgeleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b518d-109">[Instructions on how to install the Visual Studio Team Services credential provider ](../API/nuget-exe-Credential-Providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="b518d-110">Yeni kullanıcı arabirimi özellikleri</span><span class="sxs-lookup"><span data-stu-id="b518d-110">New User Interface Features</span></span>

* <span data-ttu-id="b518d-111">Ayrı Gözat, yüklü ve güncelleştirmeleri kullanılabilir sekmeler</span><span class="sxs-lookup"><span data-stu-id="b518d-111">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="b518d-112">Kullanılabilir güncelleştirme içeren paketler sayısını gösteren kullanılabilir rozet güncelleştirir</span><span class="sxs-lookup"><span data-stu-id="b518d-112">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="b518d-113">Paket paketin yüklü olup olmadığını belirtmek için paket listesinde rozetleri veya güncelleştirmesi mevcut</span><span class="sxs-lookup"><span data-stu-id="b518d-113">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="b518d-114">Sayı ve paket listesine eklenen Yazar indirin</span><span class="sxs-lookup"><span data-stu-id="b518d-114">Download count and author added to the package list</span></span>
* <span data-ttu-id="b518d-115">Yüksek kullanılabilir sürüm numarası ve paket listesi üzerinde şu anda yüklü olan sürüm numarası</span><span class="sxs-lookup"><span data-stu-id="b518d-115">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="b518d-116">Hızlı yükleme izin vermek için eylem düğmeleri güncelleştirin ve paket listeden kaldırın</span><span class="sxs-lookup"><span data-stu-id="b518d-116">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="b518d-117">Paket ayrıntı panelindeki daha anlaşılır eylem düğmeleri</span><span class="sxs-lookup"><span data-stu-id="b518d-117">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="b518d-118">Paket ayrıntı panelindeki paket güncelleştirme tarihi</span><span class="sxs-lookup"><span data-stu-id="b518d-118">Package update date on the package detail panel</span></span>
* <span data-ttu-id="b518d-119">Çözüm Görünümü panelinde birleştirin</span><span class="sxs-lookup"><span data-stu-id="b518d-119">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="b518d-120">Proje ve çözüm görünümü yüklü sürüm numaralarında sıralanabilir kılavuz</span><span class="sxs-lookup"><span data-stu-id="b518d-120">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="b518d-121">Yeni komut satırı özellikleri</span><span class="sxs-lookup"><span data-stu-id="b518d-121">New Command-line Features</span></span>

<span data-ttu-id="b518d-122">Bu sürümde gösterdiğimizi `add` ve `init` açıklandığı gibi klasör tabanlı depoları başlatmak için komutları [nuget.exe başvuru](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="b518d-122">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="b518d-123">Oluşturulan ve bu klasörü ile korunan depoları yapısı [önemli performans avantajı teslim](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) bizim blogunda özetlendiği gibi.</span><span class="sxs-lookup"><span data-stu-id="b518d-123">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="b518d-124">Content dosyaları</span><span class="sxs-lookup"><span data-stu-id="b518d-124">ContentFiles</span></span>

<span data-ttu-id="b518d-125">İçerik desteklenen şimdi `project.json` yönetilen projeleri yeni aracılığıyla `contentFiles` klasör ve `.nuspec` `contentFiles` öğesi gösterimi.</span><span class="sxs-lookup"><span data-stu-id="b518d-125">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="b518d-126">Bu içerik daha doğrudan proje sistemlerle etkileşim için paket yazarına tarafından belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="b518d-126">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="b518d-127">Content dosyaları içinde yapılandırma hakkında daha fazla bilgi bir `.nuspec` belge bulunabilir [.nuspec başvuru](../schema/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="b518d-127">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../schema/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="b518d-128">NuGet yerel yönetim önbelleğe alma</span><span class="sxs-lookup"><span data-stu-id="b518d-128">NuGet Locals Cache Management</span></span>

<span data-ttu-id="b518d-129">Komut satırı NuGet, bir iş istasyonunda yerel önbellekleri yönetme hakkında bilgiler eklenerek güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="b518d-129">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="b518d-130">Yerel öğeler komut hakkında daha fazla bilgi kullanılabilir [NuGet komut satırı başvurusu](../tools/cli-ref-locals.md).</span><span class="sxs-lookup"><span data-stu-id="b518d-130">More information about the locals command is available in the [NuGet command-line reference](../tools/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="b518d-131">Giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="b518d-131">Fixed Issues</span></span>

<span data-ttu-id="b518d-132">**Önem düzeyindeki sorunlar**</span><span class="sxs-lookup"><span data-stu-id="b518d-132">**Notable Issues**</span></span>

* <span data-ttu-id="b518d-133">Mono - bir çözüm dosyasını içeren paketleri geri yüklemek için NuGet komut satırı geri yüklenen desteği [1543](https://github.com/NuGet/Home/issues/1543)</span><span class="sxs-lookup"><span data-stu-id="b518d-133">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="b518d-134">3.3 sürümde değinilen sorunların tam listesi GitHub altında bulunabilir [3.3 Kilometre Taşı](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="b518d-134">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="b518d-135">3.3 komut satırı sürümde giderilen sorunların listesi kaydedilir [3.3 komut satırı Kilometre Taşı](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span><span class="sxs-lookup"><span data-stu-id="b518d-135">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="b518d-136">Bilinen Sorunlar</span><span class="sxs-lookup"><span data-stu-id="b518d-136">Known Issues</span></span>

<span data-ttu-id="b518d-137">Bizim GitHub sorunları listedeki konumunda bulunan sorunları izlemek devam: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="b518d-137">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>