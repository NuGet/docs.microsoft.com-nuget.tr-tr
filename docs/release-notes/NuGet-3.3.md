---
title: NuGet 3,3 sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri, eklenen özellikler ve CCR 'ler dahil olmak üzere NuGet 3,3 sürüm notları.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: aa8290c80cc500b59d1779bf76662c07382fd277
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813786"
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="62af5-103">NuGet 3,3 sürüm notları</span><span class="sxs-lookup"><span data-stu-id="62af5-103">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="62af5-104">[NuGet 3.2.1 sürüm notları](../release-notes/nuget-3.2.1.md) | [NUGET 3,4-RC sürüm notları](../release-notes/nuget-3.4-RC.md)</span><span class="sxs-lookup"><span data-stu-id="62af5-104">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="62af5-105">NuGet 3,3, önemli sayıda kullanıcı arabirimi güncelleştirmesi ve komut satırı özelliği ve NuGet istemcilerinde yararlı düzeltmelerin toplanması ile 30 Kasım 2015 ' de yayımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="62af5-105">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="62af5-106">Yeni Özellikler</span><span class="sxs-lookup"><span data-stu-id="62af5-106">New Features</span></span>

* <span data-ttu-id="62af5-107">NuGet komut satırı istemcilerinin kimliği doğrulanmış bir akış ile sorunsuz bir şekilde çalışmasına izin veren kimlik bilgileri sağlayıcıları tanıtılmıştır.</span><span class="sxs-lookup"><span data-stu-id="62af5-107">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="62af5-108">[Visual Studio Team Services kimlik bilgisi sağlayıcısının nasıl yükleneceğine](../reference/extensibility/nuget-exe-credential-providers.md) ve NuGet istemcilerinin onu kullanmak üzere nasıl yapılandırılacağına Ilişkin yönergeler NuGet docs ' da kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="62af5-108">[Instructions on how to install the Visual Studio Team Services credential provider ](../reference/extensibility/nuget-exe-credential-providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="62af5-109">Yeni Kullanıcı arabirimi özellikleri</span><span class="sxs-lookup"><span data-stu-id="62af5-109">New User Interface Features</span></span>

* <span data-ttu-id="62af5-110">Ayrı tarama, yükleme ve güncelleştirmeleri kullanılabilir sekmeleri</span><span class="sxs-lookup"><span data-stu-id="62af5-110">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="62af5-111">Kullanılabilir güncelleştirmeleri olan paket sayısını gösteren rozet 'yi güncelleştirir</span><span class="sxs-lookup"><span data-stu-id="62af5-111">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="62af5-112">Paket, paketin yüklenip yüklenmediğini veya kullanılabilir bir güncelleştirme olup olmadığını belirtmek için paket listesinde</span><span class="sxs-lookup"><span data-stu-id="62af5-112">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="62af5-113">Paket listesine eklenen indirme sayısı ve yazar</span><span class="sxs-lookup"><span data-stu-id="62af5-113">Download count and author added to the package list</span></span>
* <span data-ttu-id="62af5-114">Paket listesinde en yüksek kullanılabilir sürüm numarası ve yüklü olan sürüm numarası</span><span class="sxs-lookup"><span data-stu-id="62af5-114">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="62af5-115">Paket listesinden hızlı yüklemeye, güncelleştirmeye ve kaldırmaya izin veren eylem düğmeleri</span><span class="sxs-lookup"><span data-stu-id="62af5-115">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="62af5-116">Paket ayrıntısı panelinde eylem düğmelerini daha net olarak göster</span><span class="sxs-lookup"><span data-stu-id="62af5-116">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="62af5-117">Paket ayrıntı panelinde paket güncelleştirme tarihi</span><span class="sxs-lookup"><span data-stu-id="62af5-117">Package update date on the package detail panel</span></span>
* <span data-ttu-id="62af5-118">Çözüm görünümünde Birleştirme paneli</span><span class="sxs-lookup"><span data-stu-id="62af5-118">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="62af5-119">Çözüm görünümündeki proje ve yüklü sürüm numaraları için sıralanabilir kılavuz</span><span class="sxs-lookup"><span data-stu-id="62af5-119">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="62af5-120">Yeni komut satırı özellikleri</span><span class="sxs-lookup"><span data-stu-id="62af5-120">New Command-line Features</span></span>

<span data-ttu-id="62af5-121">Bu sürümde, [NuGet. exe başvurusunda](../reference/nuget-exe-cli-reference.md)açıklandığı gibi klasör tabanlı depoları başlatmak için `add` ve `init` komutlarını kullanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="62af5-121">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../reference/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="62af5-122">Bu klasör yapısıyla oluşturulan ve tutulan depolar, blogumuza göre [önemli performans avantajları sunar](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) .</span><span class="sxs-lookup"><span data-stu-id="62af5-122">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="62af5-123">ContentFiles</span><span class="sxs-lookup"><span data-stu-id="62af5-123">ContentFiles</span></span>

<span data-ttu-id="62af5-124">İçerik artık yeni `contentFiles` klasörü aracılığıyla `project.json` yönetilen projelerde destekleniyor ve `contentFiles` öğesi gösterimi `.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="62af5-124">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="62af5-125">Bu içerik, proje sistemleriyle etkileşimler için paket yazarı tarafından daha doğrudan belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="62af5-125">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="62af5-126">`.nuspec` bir belgedeki contentFiles 'ın nasıl yapılandırılacağı hakkında daha fazla bilgi [. nuspec başvurusunda](../reference/nuspec.md)bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="62af5-126">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../reference/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="62af5-127">NuGet Yereller önbellek yönetimi</span><span class="sxs-lookup"><span data-stu-id="62af5-127">NuGet Locals Cache Management</span></span>

<span data-ttu-id="62af5-128">NuGet komut satırı, bir iş istasyonunda yerel önbellekleri yönetme hakkında bilgi içerecek şekilde güncelleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="62af5-128">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="62af5-129">Yerel öğeler komutu hakkında daha fazla bilgi [NuGet komut satırı başvurusunda](../reference/cli-reference/cli-ref-locals.md)bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="62af5-129">More information about the locals command is available in the [NuGet command-line reference](../reference/cli-reference/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="62af5-130">Sorun düzeltildi</span><span class="sxs-lookup"><span data-stu-id="62af5-130">Fixed Issues</span></span>

<span data-ttu-id="62af5-131">**Önemli sorunlar**</span><span class="sxs-lookup"><span data-stu-id="62af5-131">**Notable Issues**</span></span>

* <span data-ttu-id="62af5-132">NuGet komut satırı, mono- [1543](https://github.com/NuGet/Home/issues/1543) ' de çözüm dosyası ile paket geri yükleme desteğini geri yükledi</span><span class="sxs-lookup"><span data-stu-id="62af5-132">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="62af5-133">3,3 sürümünde ele alınan sorunların tüm listesi, GitHub 'da [3,3 kilometre taşı](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed)altında bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="62af5-133">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="62af5-134">3,3 komut satırı sürümünde düzeltilen sorunların listesi [3,3 komut satırı kilometre taşına](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline)kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="62af5-134">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="62af5-135">Bilinen Sorunlar</span><span class="sxs-lookup"><span data-stu-id="62af5-135">Known Issues</span></span>

<span data-ttu-id="62af5-136">Şu adreste bulunan GitHub sorunları listemizdeki sorunları izlemeye devam ediyoruz: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="62af5-136">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>