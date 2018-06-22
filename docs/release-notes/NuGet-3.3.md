---
title: NuGet 3.3 sürüm notları
description: NuGet bilinen sorunları, hata düzeltmeleri, eklenen özellikleri ve dcr dahil olmak üzere 3.3 için sürüm notları.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: adf193437de237ed32da481e627552a8dba6f656
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31821570"
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="25972-103">NuGet 3.3 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="25972-103">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="25972-104">[NuGet 3.2.1 sürüm notları](../release-notes/nuget-3.2.1.md) | [NuGet 3.4 RC sürüm notları](../release-notes/nuget-3.4-RC.md)</span><span class="sxs-lookup"><span data-stu-id="25972-104">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="25972-105">NuGet 3.3 30 Kasım 2015 çok sayıda kullanışlı düzeltmeleri NuGet istemcilere koleksiyonu yanı sıra kullanıcı arabirimi güncelleştirmeleri ve komut satırı özellikleri ile serbest bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="25972-105">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="25972-106">Yeni Özellikler</span><span class="sxs-lookup"><span data-stu-id="25972-106">New Features</span></span>

* <span data-ttu-id="25972-107">Kimlik bilgisi sağlayıcıları sorunsuz bir şekilde kimliği doğrulanmış bir akış ile çalışabilmek için NuGet komut satırı istemcilerin sağlayan tanıtılmıştır.</span><span class="sxs-lookup"><span data-stu-id="25972-107">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="25972-108">[Visual Studio Team Services yükleme konusunda yönergeler kimlik bilgisi sağlayıcısı ](../api/nuget-exe-credential-providers.md) ve NuGet yapılandırma kullanmak için istemciler üzerinde NuGet belgeleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="25972-108">[Instructions on how to install the Visual Studio Team Services credential provider ](../api/nuget-exe-credential-providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="25972-109">Yeni kullanıcı arabirimi özellikleri</span><span class="sxs-lookup"><span data-stu-id="25972-109">New User Interface Features</span></span>

* <span data-ttu-id="25972-110">Ayrı Gözat, yüklü ve güncelleştirmeleri kullanılabilir sekmeler</span><span class="sxs-lookup"><span data-stu-id="25972-110">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="25972-111">Kullanılabilir güncelleştirme içeren paketler sayısını gösteren kullanılabilir rozet güncelleştirir</span><span class="sxs-lookup"><span data-stu-id="25972-111">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="25972-112">Paket paketin yüklü olup olmadığını belirtmek için paket listesinde rozetleri veya güncelleştirmesi mevcut</span><span class="sxs-lookup"><span data-stu-id="25972-112">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="25972-113">Sayı ve paket listesine eklenen Yazar indirin</span><span class="sxs-lookup"><span data-stu-id="25972-113">Download count and author added to the package list</span></span>
* <span data-ttu-id="25972-114">Yüksek kullanılabilir sürüm numarası ve paket listesi üzerinde şu anda yüklü olan sürüm numarası</span><span class="sxs-lookup"><span data-stu-id="25972-114">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="25972-115">Hızlı yükleme izin vermek için eylem düğmeleri güncelleştirin ve paket listeden kaldırın</span><span class="sxs-lookup"><span data-stu-id="25972-115">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="25972-116">Paket ayrıntı panelindeki daha anlaşılır eylem düğmeleri</span><span class="sxs-lookup"><span data-stu-id="25972-116">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="25972-117">Paket ayrıntı panelindeki paket güncelleştirme tarihi</span><span class="sxs-lookup"><span data-stu-id="25972-117">Package update date on the package detail panel</span></span>
* <span data-ttu-id="25972-118">Çözüm Görünümü panelinde birleştirin</span><span class="sxs-lookup"><span data-stu-id="25972-118">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="25972-119">Proje ve çözüm görünümü yüklü sürüm numaralarında sıralanabilir kılavuz</span><span class="sxs-lookup"><span data-stu-id="25972-119">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="25972-120">Yeni komut satırı özellikleri</span><span class="sxs-lookup"><span data-stu-id="25972-120">New Command-line Features</span></span>

<span data-ttu-id="25972-121">Bu sürümde gösterdiğimizi `add` ve `init` açıklandığı gibi klasör tabanlı depoları başlatmak için komutları [nuget.exe başvuru](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="25972-121">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="25972-122">Oluşturulan ve bu klasörü ile korunan depoları yapısı [önemli performans avantajı teslim](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) bizim blogunda özetlendiği gibi.</span><span class="sxs-lookup"><span data-stu-id="25972-122">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="25972-123">Content dosyaları</span><span class="sxs-lookup"><span data-stu-id="25972-123">ContentFiles</span></span>

<span data-ttu-id="25972-124">İçerik desteklenen şimdi `project.json` yönetilen projeleri yeni aracılığıyla `contentFiles` klasör ve `.nuspec` `contentFiles` öğesi gösterimi.</span><span class="sxs-lookup"><span data-stu-id="25972-124">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="25972-125">Bu içerik daha doğrudan proje sistemlerle etkileşim için paket yazarına tarafından belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="25972-125">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="25972-126">Content dosyaları içinde yapılandırma hakkında daha fazla bilgi bir `.nuspec` belge bulunabilir [.nuspec başvuru](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="25972-126">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../reference/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="25972-127">NuGet yerel yönetim önbelleğe alma</span><span class="sxs-lookup"><span data-stu-id="25972-127">NuGet Locals Cache Management</span></span>

<span data-ttu-id="25972-128">Komut satırı NuGet, bir iş istasyonunda yerel önbellekleri yönetme hakkında bilgiler eklenerek güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="25972-128">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="25972-129">Yerel öğeler komut hakkında daha fazla bilgi kullanılabilir [NuGet komut satırı başvurusu](../tools/cli-ref-locals.md).</span><span class="sxs-lookup"><span data-stu-id="25972-129">More information about the locals command is available in the [NuGet command-line reference](../tools/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="25972-130">Giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="25972-130">Fixed Issues</span></span>

<span data-ttu-id="25972-131">**Önem düzeyindeki sorunlar**</span><span class="sxs-lookup"><span data-stu-id="25972-131">**Notable Issues**</span></span>

* <span data-ttu-id="25972-132">Mono - bir çözüm dosyasını içeren paketleri geri yüklemek için NuGet komut satırı geri yüklenen desteği [1543](https://github.com/NuGet/Home/issues/1543)</span><span class="sxs-lookup"><span data-stu-id="25972-132">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="25972-133">3.3 sürümde değinilen sorunların tam listesi GitHub altında bulunabilir [3.3 Kilometre Taşı](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="25972-133">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="25972-134">3.3 komut satırı sürümde giderilen sorunların listesi kaydedilir [3.3 komut satırı Kilometre Taşı](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span><span class="sxs-lookup"><span data-stu-id="25972-134">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="25972-135">Bilinen Sorunlar</span><span class="sxs-lookup"><span data-stu-id="25972-135">Known Issues</span></span>

<span data-ttu-id="25972-136">Bizim GitHub sorunları listedeki konumunda bulunan sorunları izlemek devam: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="25972-136">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>