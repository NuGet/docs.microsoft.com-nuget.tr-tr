---
title: NuGet 3.3 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr NuGet 3.3 sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5fb840ab6a1329611e9cf417724bcdcd75efe2df
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546653"
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="e37f6-103">NuGet 3.3 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="e37f6-103">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="e37f6-104">[NuGet 3.2.1 sürüm notları](../release-notes/nuget-3.2.1.md) | [NuGet 3.4 RC sürüm notları](../release-notes/nuget-3.4-RC.md)</span><span class="sxs-lookup"><span data-stu-id="e37f6-104">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="e37f6-105">NuGet 3.3, 30 Kasım 2015 ile çok sayıda kullanışlı düzeltmeleri NuGet istemcilere koleksiyonunu yanı sıra kullanıcı arabirimi güncelleştirmeleri ve komut satırı özellikleri olarak yayımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="e37f6-105">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="e37f6-106">Yeni Özellikler</span><span class="sxs-lookup"><span data-stu-id="e37f6-106">New Features</span></span>

* <span data-ttu-id="e37f6-107">Sorunsuz bir şekilde kimliği doğrulanmış bir akışı ile çalışmak komut satırı istemcilerin NuGet kimlik bilgisi sağlayıcıları tanıtılmıştır.</span><span class="sxs-lookup"><span data-stu-id="e37f6-107">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="e37f6-108">[Visual Studio Team Services'ı yüklemek yönergeler kimlik bilgisi sağlayıcısı ](../api/nuget-exe-credential-providers.md) ve NuGet yapılandırma kullanmak için istemcileri üzerinde NuGet belgeleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e37f6-108">[Instructions on how to install the Visual Studio Team Services credential provider ](../api/nuget-exe-credential-providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="e37f6-109">Yeni kullanıcı arabirimi özellikleri</span><span class="sxs-lookup"><span data-stu-id="e37f6-109">New User Interface Features</span></span>

* <span data-ttu-id="e37f6-110">Göz atma, yüklü ve güncelleştirmeleri kullanılabilir ayrı sekmeler</span><span class="sxs-lookup"><span data-stu-id="e37f6-110">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="e37f6-111">Kullanılabilir güncelleştirmeleri olan paketleri sayısını gösteren güncelleştirmeleri kullanılabilir rozeti</span><span class="sxs-lookup"><span data-stu-id="e37f6-111">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="e37f6-112">Paket yüklü değil veya güncelleştirmesi mevcut olmadığını belirtmek için paket listesinde paket rozetlerini</span><span class="sxs-lookup"><span data-stu-id="e37f6-112">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="e37f6-113">Sayısı ve paket listesine Yazar indirin</span><span class="sxs-lookup"><span data-stu-id="e37f6-113">Download count and author added to the package list</span></span>
* <span data-ttu-id="e37f6-114">Yüksek kullanılabilir sürüm numarasını ve paket listesi üzerinde şu anda yüklü sürüm numarası</span><span class="sxs-lookup"><span data-stu-id="e37f6-114">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="e37f6-115">Hızlı yükleme izin vermek için komut düğmeleri güncelleştirmek ve paketi listeden kaldırma</span><span class="sxs-lookup"><span data-stu-id="e37f6-115">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="e37f6-116">Paket Ayrıntıları paneline üzerinde NET eylem düğmeleri</span><span class="sxs-lookup"><span data-stu-id="e37f6-116">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="e37f6-117">Paket Ayrıntıları paneline paket güncelleştirme tarihi</span><span class="sxs-lookup"><span data-stu-id="e37f6-117">Package update date on the package detail panel</span></span>
* <span data-ttu-id="e37f6-118">Çözüm görünümünde panelinde birleştirin</span><span class="sxs-lookup"><span data-stu-id="e37f6-118">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="e37f6-119">Proje ve çözüm görünümü üzerinde yüklü sürüm numaraları sıralanabilir kılavuz</span><span class="sxs-lookup"><span data-stu-id="e37f6-119">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="e37f6-120">Yeni komut satırı özellikleri</span><span class="sxs-lookup"><span data-stu-id="e37f6-120">New Command-line Features</span></span>

<span data-ttu-id="e37f6-121">Bu sürümde sunduk `add` ve `init` açıklandığı gibi klasör tabanlı depoları başlatmak için komutları [nuget.exe başvurusu](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="e37f6-121">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="e37f6-122">Oluşturulur ve bu klasörü tutulan depolar yapısı [önemli performans avantajlarının teslim](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) blogumuzu özetlenen.</span><span class="sxs-lookup"><span data-stu-id="e37f6-122">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="e37f6-123">contentFiles</span><span class="sxs-lookup"><span data-stu-id="e37f6-123">ContentFiles</span></span>

<span data-ttu-id="e37f6-124">İçerik desteklenen artık `project.json` projelerini yeni aracılığıyla yönetilen `contentFiles` klasörü ve `.nuspec` `contentFiles` öğesi gösterimi.</span><span class="sxs-lookup"><span data-stu-id="e37f6-124">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="e37f6-125">Bu içerik daha doğrudan proje sistemleri ile etkileşim için paket yazarı tarafından belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="e37f6-125">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="e37f6-126">ContentFiles içinde yapılandırma hakkında daha fazla bilgi bir `.nuspec` belge bulunabilir [.nuspec başvuru](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="e37f6-126">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../reference/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="e37f6-127">Yönetim NuGet yerel önbellek</span><span class="sxs-lookup"><span data-stu-id="e37f6-127">NuGet Locals Cache Management</span></span>

<span data-ttu-id="e37f6-128">NuGet komut satırı, bir iş istasyonundaki yerel önbelleklerini nasıl yönetecekleri hakkındaki bilgileri içerecek şekilde güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="e37f6-128">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="e37f6-129">Yerel öğeler komut hakkında daha fazla bilgi kullanılabilir [NuGet komut satırı başvurusu](../tools/cli-ref-locals.md).</span><span class="sxs-lookup"><span data-stu-id="e37f6-129">More information about the locals command is available in the [NuGet command-line reference](../tools/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="e37f6-130">Giderilen sorunlar</span><span class="sxs-lookup"><span data-stu-id="e37f6-130">Fixed Issues</span></span>

<span data-ttu-id="e37f6-131">**Önemli sorunlar**</span><span class="sxs-lookup"><span data-stu-id="e37f6-131">**Notable Issues**</span></span>

* <span data-ttu-id="e37f6-132">Geri yükleme için NuGet komut satırı geri yüklenen desteği paketleri ile bir çözüm dosyası üzerinde Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span><span class="sxs-lookup"><span data-stu-id="e37f6-132">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="e37f6-133">3.3 sürümünde giderilen sorunların tam listesi altında github'da bulunabilir [3.3 kilometre](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="e37f6-133">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="e37f6-134">3.3 komut satırı sürümde giderilen sorunlar listesinde kaydedilir [3.3 komut satırı kilometre](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span><span class="sxs-lookup"><span data-stu-id="e37f6-134">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="e37f6-135">Bilinen Sorunlar</span><span class="sxs-lookup"><span data-stu-id="e37f6-135">Known Issues</span></span>

<span data-ttu-id="e37f6-136">Şurada bulunabilir bizim GitHub sorunlar listesinde sorunları izlemek devam ediyoruz: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="e37f6-136">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>